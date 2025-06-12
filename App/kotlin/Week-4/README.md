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

### 🔹 **[Mentee Name 1]** - `AuthRepository`
Implement user authentication and registration functionality.

**Responsibilities:**
- User registration with validation
- User login and token management
- Logout functionality
- Token refresh handling

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

### 🔹 **[Mentee Name 2]** - `TaskRepository`
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

### 🔹 **[Mentee Name 3]** - `NotesRepository`
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

## Integration with ViewModels

After implementing repositories, integrate them with your existing UI:

```kotlin
class TaskViewModel(private val taskRepository: TaskRepository) : ViewModel() {
    private val _tasks = mutableStateOf<List<Task>>(emptyList())
    val tasks: State<List<Task>> = _tasks
    
    private val _isLoading = mutableStateOf(false)
    val isLoading: State<Boolean> = _isLoading
    
    fun loadTasks() {
        viewModelScope.launch {
            _isLoading.value = true
            try {
                _tasks.value = taskRepository.getTasks()
            } catch (e: Exception) {
                // Handle error
            } finally {
                _isLoading.value = false
            }
        }
    }
}
```

## Error Handling Best Practices

Implement proper error handling in your repositories:

```kotlin
sealed class NetworkResult<T> {
    data class Success<T>(val data: T) : NetworkResult<T>()
    data class Error<T>(val message: String) : NetworkResult<T>()
    data class Loading<T>(val isLoading: Boolean = true) : NetworkResult<T>()
}

// Usage in repository
suspend fun getTasksWithResult(): NetworkResult<List<Task>> {
    return try {
        val response = ktorHttpClient.get(Constants.BASE_URL + "task/all")
        if (response.status.isSuccess()) {
            NetworkResult.Success(response.body<List<Task>>())
        } else {
            NetworkResult.Error("Failed to fetch tasks: ${response.status.value}")
        }
    } catch (e: Exception) {
        NetworkResult.Error("Network error: ${e.message}")
    }
}
```

## Testing Your Implementation

Basic testing approach for repositories:

```kotlin
@Test
fun `test successful task retrieval`() = runTest {
    // Given
    val mockTasks = listOf(
        Task(1, "Test Task", "Description", "HIGH", "TODO")
    )
    
    // When
    val result = taskRepository.getTasks()
    
    // Then
    assertEquals(1, result.size)
    assertEquals("Test Task", result[0].title)
}
```

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
