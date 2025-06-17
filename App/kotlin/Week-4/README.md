# Week 4: Data Layer & API Integration

Welcome to Week 4 of DevLabs 2025 - App Development Track! This week, we'll build the data layer for our Taskify app, implementing API calls, authentication, and data persistence. By the end of this week, you'll have connected your UI to a real backend and understand how modern Android apps handle data.

## Learning Journey Overview

### Day 1-2: Backend & API Fundamentals
- Understanding client-server architecture
- What are APIs, REST, and HTTP methods
- Database basics and how servers work
- JSON data format and serialization
- Introduction to Ktor HTTP client

### Day 3-4: Authentication & Security
- JWT (JSON Web Tokens) explained
- How authentication works in mobile apps
- Token storage and management
- SharedPreferences for local data storage
- Implementing secure API calls

### Day 4-5: Repository Pattern & Architecture
- Repository pattern explained
- Data Transfer Objects (DTOs)
- HTTP client setup and configuration
- Error handling in network calls
- Connecting repositories to UI

### Day 6-7: Integration & Testing
- Integrating repositories with ViewModels
- Testing API calls
- Handling offline scenarios
- Performance optimization

## Backend & API Concepts Explained

### What is a Backend?
A backend is the server-side of an application that:
- Stores and manages data in databases
- Processes business logic
- Provides APIs for client applications
- Handles user authentication and authorization

### API (Application Programming Interface)
An API is a contract that defines how different software components communicate:
- **Endpoint**: A specific URL where you can access data (e.g., `/auth/login`)
- **HTTP Methods**: GET (retrieve), POST (create), PUT (update), DELETE (remove)
- **Request/Response**: Data sent to and received from the server
- **Status Codes**: 200 (success), 404 (not found), 500 (server error)

### Our Taskify API Structure
```
Base URL: https://localhost:8080
├── /auth
│   ├── POST /register    - Create new user account
│   └── POST /authenticate - Login user
├── /task
│   ├── GET /all         - Get all tasks
│   ├── POST /add        - Create new task
│   ├── PUT /update/{id} - Update existing task
│   └── DELETE /delete/{id} - Delete task
└── /note
    ├── GET /all         - Get all notes
    ├── GET /{id}        - Get specific note
    ├── POST /add        - Create new note
    ├── PUT /update/{id} - Update existing note
    └── DELETE /delete/{id} - Delete note
```

### JWT Authentication Flow
1. **Login**: User sends credentials → Server validates → Returns JWT token
2. **Storage**: App stores token securely in SharedPreferences
3. **API Calls**: Include token in Authorization header for protected endpoints
4. **Validation**: Server validates token for each request

## Required Dependencies

Add these dependencies to your `build.gradle.kts` (Module: app):

```kotlin
// Ktor Client for HTTP networking
implementation(libs.bundles.ktor)

// Lifecycle components for ViewModels
implementation(libs.androidx.lifecycle.runtime.compose)
implementation(libs.androidx.lifecycle.viewmodel.compose)

// Navigation
implementation(libs.androidx.navigation.compose)

// Material Icons
implementation(libs.compose.material.icons.extended)
```

Required version catalog entries (already added to project):
```toml
[versions]
ktor = "2.3.12"
lifecycle-runtime-ktx = "2.8.0"

[libraries]
# Ktor HTTP Client
ktor-client-cio = { module = "io.ktor:ktor-client-cio", version.ref = "ktor" }
ktor-client-auth = { module = "io.ktor:ktor-client-auth", version.ref = "ktor" }
ktor-client-content-negotiation = { module = "io.ktor:ktor-client-content-negotiation", version.ref = "ktor" }
ktor-client-core = { module = "io.ktor:ktor-client-core", version.ref = "ktor" }
ktor-client-logging = { module = "io.ktor:ktor-client-logging", version.ref = "ktor" }
ktor-serialization-kotlinx-json = { module = "io.ktor:ktor-serialization-kotlinx-json", version.ref = "ktor" }

[plugins]
kotlin-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }

[bundles]
ktor = [
    "ktor-client-cio",
    "ktor-client-auth",
    "ktor-client-content-negotiation",
    "ktor-client-core",
    "ktor-client-logging",
    "ktor-serialization-kotlinx-json"
]
```

## Data Models & DTOs

First, create your data models in `data/model/`:

```kotlin
// User authentication models
@Serializable
data class RegistrationRequest(
    val fullName: String,
    val email: String,
    val password: String
)

@Serializable
data class AuthenticationRequest(
    val email: String,
    val password: String
)

@Serializable
data class AuthenticationResponse(
    val access_token: String
)
// Task model
@Serializable
data class Task(
    val id: Int? = null ,
    val title: String,
    val description: String,
    val status: String,
    val priority: Int,
)

// Note model
@Serializable
data class Note(
    val id: Int? = null,
    val title: String,
    val content: String,
)
```

## HTTP Client Setup

Create `network/HttpClientFactory.kt`:

```kotlin
package org.openlake.devlabs2025kotlin1.data.remote

import io.ktor.client.HttpClient
import io.ktor.client.engine.HttpClientEngine
import io.ktor.client.plugins.HttpTimeout
import io.ktor.client.plugins.auth.Auth
import io.ktor.client.plugins.auth.providers.BearerTokens
import io.ktor.client.plugins.auth.providers.bearer
import io.ktor.client.plugins.contentnegotiation.ContentNegotiation
import io.ktor.client.plugins.defaultRequest
import io.ktor.client.plugins.logging.ANDROID
import io.ktor.client.plugins.logging.LogLevel
import io.ktor.client.plugins.logging.Logger
import io.ktor.client.plugins.logging.Logging
import io.ktor.http.ContentType
import io.ktor.http.contentType
import io.ktor.serialization.kotlinx.json.json
import kotlinx.serialization.json.Json
import org.openlake.devlabs2025kotlin1.data.remote.SessionManager

object HttpClientFactory {
    fun create(engine: HttpClientEngine, sessionManager: SessionManager) : HttpClient {
        return HttpClient(engine) {
            install(Logging) {
                level = LogLevel.ALL
                logger = Logger.ANDROID
            }
            install(ContentNegotiation) {
                json(
                    json = Json {
                        prettyPrint = true
                        ignoreUnknownKeys = true
                    }
                )
            }
            install(Auth) {
                bearer {
                    loadTokens {
                        BearerTokens(accessToken = sessionManager.getToken() ?: "", "")
                    }
                }
            }
            defaultRequest {
                contentType(ContentType.Application.Json)
            }
        }
    }
}

```

## SharedPreferences for Token Storage

Create `utils/TokenManager.kt`:

```kotlin
package org.openlake.devlabs2025kotlin1.data.remote
// Now, let's create a SharedPreferences manager to store the token

// SessionManager.kt
import android.content.Context
import android.content.SharedPreferences
import androidx.core.content.edit

class SessionManager(context: Context) {
    private val sharedPreferences: SharedPreferences =
        context.getSharedPreferences("TaskifyPrefs", Context.MODE_PRIVATE)

    companion object {
        private const val KEY_TOKEN = "key_token"
    }

    fun saveToken(token: String) {
        sharedPreferences.edit { putString(KEY_TOKEN, token) }
    }

    fun getToken(): String? {
        return sharedPreferences.getString(KEY_TOKEN, null)
    }

    fun clearToken() {
        sharedPreferences.edit { remove(KEY_TOKEN) }
    }

    fun isLoggedIn(): Boolean {
        return getToken() != null
    }
}
```

## Repository Implementation Tasks

Each mentee will implement one repository following the provided structure:

### 🔹 **Shivangshu Sharma** - `AuthRepository`
Implement user authentication and registration functionality.

**Responsibilities:**
- User registration with validation
- User login and token management
- Logout functionality

**Files to create:**
```
data/repository/
└── AuthRepository.kt

utils/
└── TokenManager.kt (if not created)
```

**Key Methods:**
- `suspend fun register(fullName: String, email: String, password: String): Boolean`
- `suspend fun login(email: String, password: String): String?`
- `fun logout()`
- `fun isLoggedIn(): Boolean`

**Implementation Focus:**
- Proper error handling for network failures
- Secure token storage
- Input validation
- Clear success/failure responses

### 🔹 **Swarit Dixit** - `TaskRepository`
Implement task management operations.

**Responsibilities:**
- Fetch all user tasks
- Create, update, and delete tasks
- Task status management (TODO, IN_PROGRESS, DONE)
- Task filtering and sorting

**Files to create:**
```
data/repository/
└── TaskRepository.kt
```

**Key Methods:**
- `suspend fun getTasks(): List<Task>`
- `suspend fun addTask(task: Task): Boolean`
- `suspend fun updateTask(task: Task, taskId: Int): Boolean`
- `suspend fun deleteTask(taskId: Int): Boolean`
- `suspend fun markTaskAsCompleted(taskId: Int): Boolean`
- `suspend fun markTaskAsInProgress(taskId: Int): Boolean`

**Implementation Focus:**
- Efficient list management
- Status change operations
- Error handling for CRUD operations
- Data consistency

### 🔹 **Akshat Gupta** - `NotesRepository`
Implement notes management functionality.

**Responsibilities:**
- Fetch all user notes
- Create, read, update, and delete notes
- Individual note retrieval
- Search functionality preparation

**Files to create:**
```
data/repository/
└── NotesRepository.kt
```

**Key Methods:**
- `suspend fun getNotes(): List<Note>`
- `suspend fun getNote(noteId: Int): Note?`
- `suspend fun addNote(note: Note): Boolean`
- `suspend fun updateNote(note: Note, noteId: Int): Boolean`
- `suspend fun deleteNoteById(noteId: Int): Boolean`

**Implementation Focus:**
- Individual note operations
- Efficient data retrieval
- Content management
- Error handling for note operations

## Repository Pattern Explained

The Repository pattern provides:
- **Abstraction**: Hides complex API details from UI
- **Testability**: Easy to mock for unit testing
- **Consistency**: Standardized data access methods
- **Error Handling**: Centralized network error management

```kotlin
// Repository Structure Template
class ExampleRepository(private val ktorHttpClient: HttpClient) {
    
    suspend fun getData(): List<DataModel> {
        return try {
            val response = ktorHttpClient.get(Constants.BASE_URL + "endpoint")
            response.body<List<DataModel>>()
        } catch (e: Exception) {
            // Log error appropriately
            emptyList() // Return safe default
        }
    }
}
```

# Week 4: ViewModel Integration & State Management

Welcome to the second part of Week 4 - ViewModel Integration! After implementing your repositories, it's time to connect them to the presentation layer through ViewModels. This week, you'll learn how modern Android apps manage UI state, handle user interactions, and coordinate between different layers of the app.


## ViewModel Architecture Explained

### What is a ViewModel?
A ViewModel is a class designed to store and manage UI-related data in a lifecycle-conscious way:
- **Survives configuration changes** (screen rotation, theme changes)
- **Separates UI logic from business logic**
- **Provides data to UI through observable patterns**
- **Handles user interactions and coordinates with repositories**

### MVVM Pattern in Android
```
View (Composables) ↔ ViewModel ↔ Repository ↔ Data Source (API/Database)
```

### Key Concepts You'll Learn

#### 1. LiveData
- Observable data holder class
- Lifecycle-aware (only updates active observers)
- Automatic UI updates when data changes

#### 2. MutableState (Compose)
- Compose-specific state management
- Triggers recomposition when state changes
- More suitable for Jetpack Compose UIs

#### 3. ViewModelScope
- Coroutine scope tied to ViewModel lifecycle
- Automatically cancels when ViewModel is destroyed
- Perfect for network calls and background operations

## Core ViewModel Structure (Pre-implemented)

The base ViewModel structure is already provided with essential setup:

```kotlin
class TaskifyViewModel(
    private val taskRepository: TaskRepository,
    private val notesRepository: NotesRepository,
    private val authRepository: AuthRepository,
    private val sessionManager: SessionManager
) : ViewModel() {
    
    // Core state variables (already implemented)
    private val _tasks = MutableLiveData<List<Task>>(emptyList())
    val tasks: LiveData<List<Task>> = _tasks
    
    private val _notes = MutableLiveData<List<Note>>(emptyList())
    val notes: LiveData<List<Note>> = _notes
    
    val login = mutableStateOf(false)
    val register = mutableStateOf(false)
    
    // Utility functions (already implemented)
    init {
        loadTasks()
        loadNotes()
    }
    
    fun resetStates() { /* Implementation provided */ }
    fun clearStates() { /* Implementation provided */ }
}
```

## Learning Resources & Concepts

### Essential Concepts to Master

#### LiveData vs MutableState
```kotlin
// LiveData approach (traditional Android)
private val _tasks = MutableLiveData<List<Task>>()
val tasks: LiveData<List<Task>> = _tasks

// MutableState approach (Jetpack Compose)
val login = mutableStateOf(false)
```

#### Coroutines in ViewModels
```kotlin
fun loadData() {
    viewModelScope.launch {
        try {
            // Suspend function call
            val data = repository.getData()
            _data.value = data
        } catch (e: Exception) {
            // Handle error
        }
    }
}
```
## Implementation Tasks

Each mentee will implement specific ViewModel functions following the established patterns:

### 🔹 **Shivangshu Sharma** - Authentication ViewModel Functions

**Learning Focus:**
- User session management
- Form validation in ViewModels
- Boolean state management with MutableState
- Authentication flow coordination

**Functions to Implement:**

#### 1. `login(email: String, password: String)`
```kotlin
fun login(email: String, password: String) {
    viewModelScope.launch {
        // TODO: Implement login logic
        // 1. Call authRepository.login()
        // 2. Handle success/failure
        // 3. Save token using sessionManager
        // 4. Update login state
        // 5. Handle errors appropriately
    }
}
```

#### 2. `register(fullName: String, email: String, password: String)`
```kotlin
fun register(fullName: String, email: String, password: String) {
    viewModelScope.launch {
        // TODO: Implement registration logic
        // 1. Call authRepository.register()
        // 2. Handle success/failure
        // 3. Update register state
        // 4. Handle validation errors
    }
}
```
**Key Learning Points:**
- MutableState for UI state management
- Form validation techniques
- Session management coordination
- Error handling for authentication

**Testing Focus:**
- Test successful login flow
- Test registration validation
- Test error handling scenarios
- Test state updates

---

### 🔹 **Swarit Dixit** - Task Management ViewModel Functions

**Learning Focus:**
- List state management with LiveData
- CRUD operations in ViewModels
- Task status management
- Background operations with coroutines

**Functions to Implement:**

#### 1. `loadTasks()`
```kotlin
fun loadTasks() {
    viewModelScope.launch {
        // TODO: Implement task loading
        // 1. Show loading state (optional)
        // 2. Call taskRepository.getTasks()
        // 3. Update _tasks LiveData
        // 4. Handle errors appropriately
    }
}
```

#### 2. `addTask(task: Task)`
```kotlin
fun addTask(task: Task) {
    viewModelScope.launch {
        // TODO: Implement task addition
        // 1. Call taskRepository.addTask()
        // 2. If successful, reload tasks
        // 3. Handle errors and show appropriate messages
    }
}
```

#### 3. `updateTask(task: Task, taskId: Int)`
```kotlin
fun updateTask(task: Task, taskId: Int) {
    viewModelScope.launch {
        // TODO: Implement task update
        // 1. Call taskRepository.updateTask()
        // 2. Reload tasks on success
        // 3. Handle update failures
    }
}
```

#### 4. `deleteTask(taskId: Int)`
```kotlin
fun deleteTask(taskId: Int) {
    viewModelScope.launch {
        // TODO: Implement task deletion
        // 1. Call taskRepository.deleteTask()
        // 2. Reload tasks on success
        // 3. Handle deletion errors
    }
}
```

#### 5. Task Status Management
```kotlin
fun markTaskAsCompleted(taskId: Int) {
    viewModelScope.launch {
        // TODO: Mark task as completed
        // 1. Call taskRepository.markTaskAsCompleted()
        // 2. Reload tasks to reflect changes
        // 3. Handle status update failures
    }
}

fun moveTaskToInProgress(taskId: Int) {
    viewModelScope.launch {
        // TODO: Move task to in-progress
        // 1. Call taskRepository.markTaskAsInProgress()
        // 2. Reload tasks
        // 3. Handle errors
    }
}
```
**Key Learning Points:**
- LiveData for reactive list updates
- CRUD operation patterns
- Status management strategies
- Efficient data reloading

**Testing Focus:**
- Test task CRUD operations
- Test status change operations
- Test data consistency
- Test error scenarios

---

### 🔹 **Akshat Gupta** - Notes Management ViewModel Functions

**Learning Focus:**
- Content management with ViewModels
- Individual item operations
- Search functionality implementation
- Advanced LiveData transformations

**Functions to Implement:**

#### 1. `loadNotes()`
```kotlin
fun loadNotes() {
    viewModelScope.launch {
        // TODO: Implement notes loading
        // 1. Call notesRepository.getNotes()
        // 2. Update _notes LiveData
        // 3. Handle loading errors
    }
}
```

#### 2. `addNote(note: Note)`
```kotlin
fun addNote(note: Note) {
    viewModelScope.launch {
        // TODO: Implement note addition
        // 1. Call notesRepository.addNote()
        // 2. Reload notes on success
        // 3. Handle creation errors
    }
}
```

#### 3. `updateNote(note: Note, noteId: Int)`
```kotlin
fun updateNote(note: Note, noteId: Int) {
    viewModelScope.launch {
        // TODO: Implement note update
        // 1. Call notesRepository.updateNote()
        // 2. Reload notes
        // 3. Handle update failures
    }
}
```

#### 4. `deleteNote(noteId: Int)`
```kotlin
fun deleteNote(noteId: Int) {
    viewModelScope.launch {
        // TODO: Implement note deletion
        // 1. Call notesRepository.deleteNoteById()
        // 2. Reload notes on success
        // 3. Handle deletion errors
    }
}
```


**Key Learning Points:**
- Individual item management
- LiveData transformations

**Testing Focus:**
- Test note CRUD operations
- Test individual note retrieval
---

## Integration with UI (Compose)

### Observing LiveData in Compose
```kotlin
@Composable
fun TaskScreen(viewModel: TaskifyViewModel) {
    val tasks by viewModel.tasks.observeAsState(emptyList())
    val isLoading by viewModel.isLoading.observeAsState(false)
    
    LazyColumn {
        items(tasks) { task ->
            TaskItem(
                task = task,
                onTaskClick = { viewModel.updateTask(it, task.id!!) },
                onDeleteClick = { viewModel.deleteTask(task.id!!) }
            )
        }
    }
}
```

### Handling MutableState in Compose
```kotlin
@Composable
fun LoginScreen(viewModel: TaskifyViewModel) {
    val loginSuccess by viewModel.login
    
    if (loginSuccess) {
        // Navigate to main screen
        LaunchedEffect(loginSuccess) {
            // Handle navigation
            viewModel.resetStates()
        }
    }
}
```

## Error Handling Best Practices

### Repository Error Handling
```kotlin
try {
    val result = repository.getData()
    _data.value = result
    clearError()
} catch (e: NetworkException) {
    showError("Network error: Please check your connection")
} catch (e: AuthException) {
    showError("Authentication failed: Please login again")
} catch (e: Exception) {
    showError("An unexpected error occurred")
}
```

### UI Error Display
```kotlin
errorMessage.value?.let { message ->
    Snackbar(
        action = {
            TextButton(onClick = { viewModel.clearError() }) {
                Text("Dismiss")
            }
        }
    ) {
        Text(message)
    }
}
```


## Weekly Deliverables

### Individual Implementation (Each Mentee)
1. **Complete assigned ViewModel functions**
2. **Implement proper error handling**
3. **Add comprehensive unit tests**
4. **Document your implementation**
5. **Create integration examples**

### Code Review Checklist
- [ ] All functions implemented with proper coroutine usage
- [ ] Error handling implemented for all operations
- [ ] LiveData/MutableState used correctly
- [ ] No memory leaks or resource leaks
- [ ] Proper separation of concerns
- [ ] Unit tests cover all major scenarios

### Integration Testing
- [ ] ViewModel connects properly with repositories
- [ ] UI updates correctly when state changes
- [ ] Error states are handled gracefully
- [ ] Loading states provide good UX
- [ ] Navigation works with state changes

## Learning Resources

### Essential Reading
- [ViewModel Overview](https://developer.android.com/topic/libraries/architecture/viewmodel)
- [LiveData Overview](https://developer.android.com/topic/libraries/architecture/livedata)
- [State in Jetpack Compose](https://developer.android.com/jetpack/compose/state)
- [Kotlin Coroutines](https://kotlinlang.org/docs/coroutines-overview.html)

### Video Tutorials
- [Android Architecture Components](https://www.youtube.com/watch?v=pErTyQpA390)
- [ViewModels and LiveData](https://www.youtube.com/watch?v=OMcDk2_4LSk)
- [State Management in Compose](https://www.youtube.com/watch?v=mymWGMy9pYI)

### Documentation
- [ViewModelScope Documentation](https://developer.android.com/topic/libraries/architecture/coroutines#viewmodelscope)
- [Testing ViewModels](https://developer.android.com/topic/libraries/architecture/viewmodel#testing)

## Success Criteria

By the end of this week, you should be able to:
- Implement complex ViewModel functions with proper state management
- Handle user interactions through ViewModel methods
- Manage UI state using LiveData and MutableState
- Implement proper error handling and loading states
- Test ViewModel functionality thoroughly
- 
Remember: The goal is not just to make it work, but to understand the underlying patterns and architecture principles. Focus on learning how state flows through your app and how different components communicate with each other.

Good luck with your ViewModel implementation! 🚀

## Security Considerations

1. **Token Storage**: Use SharedPreferences (encrypted in production)
2. **HTTPS Only**: Always use secure connections
3. **Token Expiry**: Handle token refresh gracefully
4. **Input Validation**: Validate all user inputs
5. **Error Messages**: Don't expose sensitive information

## Bonus Tasks

### Advanced Implementation
1. **Offline Support**:
    - Implement local database caching with Room
    - Sync data when connection is restored
    - Handle conflict resolution

2. **Advanced Error Handling**:
    - Implement retry mechanisms
    - Show user-friendly error messages
    - Handle different HTTP status codes

3. **Performance Optimization**:
    - Implement pagination for large lists
    - Add request caching
    - Optimize JSON serialization

4. **Security Enhancements**:
    - Implement biometric authentication
    - Add certificate pinning
    - Implement proper token refresh

### Integration Tasks
1. **ViewModel Integration**:
    - Connect repositories to existing ViewModels
    - Implement proper state management
    - Add loading states

2. **UI Updates**:
    - Show loading indicators
    - Display error messages
    - Implement pull-to-refresh

## Learning Resources

### Networking & APIs
- [Ktor Client Documentation](https://ktor.io/docs/client.html)
- [REST API Best Practices](https://restfulapi.net/)
- [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

### Authentication
- [JWT.io - JWT Explained](https://jwt.io/introduction)
- [Android Security Best Practices](https://developer.android.com/topic/security/best-practices)

### Architecture
- [Repository Pattern](https://developer.android.com/topic/architecture/data-layer)
- [Guide to App Architecture](https://developer.android.com/topic/architecture)

### Video Tutorials
- [Ktor Client by Philipp Lackner](https://www.youtube.com/watch?v=ylWTfBG1SbU)
- [Android Repository Pattern](https://www.youtube.com/watch?v=4L3-DW_jNIk)

## Weekly Checklist

### Core Requirements
- [ ] Complete assigned repository implementation
- [ ] Implement proper error handling
- [ ] Test all API endpoints
- [ ] Integrate with SharedPreferences for token storage
- [ ] Create proper data models with serialization
- [ ] Submit PR with your implementation

### Integration Tasks
- [ ] Connect repository to existing ViewModels
- [ ] Update UI to show loading states
- [ ] Implement error message display
- [ ] Test end-to-end functionality

### Optional Enhancements
- [ ] Implement offline caching
- [ ] Add advanced error handling
- [ ] Create comprehensive unit tests
- [ ] Implement security best practices

## Constants File

Create `utils/Constants.kt`:
```kotlin

object Constants {
    const val BASE_URL = "http://<your-ip>/api/v1/"
}
```

## Project Structure

Your final data layer structure should look like:
```
app/src/main/java/org/openlake/taskify/
├── data/
│   ├── model/
│   │   ├── Token.kt
│   │   ├── Task.kt
│   │   └── Note.kt
│   ├── repository/
│   │   ├── AuthRepository.kt
│   │   ├── TaskRepository.kt
│   │   └── NotesRepository.kt
│   ├── network/
│   │   └── HttpClientFactory.kt
│   └── utils/
│       ├── Constants.kt
│       └── TokenManager.kt


By the end of this week, you'll have a fully functional data layer that connects your beautiful UI to a real backend, making your Taskify app truly dynamic and useful!

Good luck implementing the data layer! Remember: start simple, test frequently, and don't hesitate to ask questions.
