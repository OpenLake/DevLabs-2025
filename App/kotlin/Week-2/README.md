# Week 2: Jetpack Compose & Android Basics

Welcome to the second week of DevLabs 2025 - App Development Track! This week, we'll focus on building the UI for our Taskify app using Jetpack Compose and learning Android fundamentals. By the end of this week, you'll have created a functional UI for our task management application and gained an understanding of core Android concepts.

## Agenda

### Day 1-3: Jetpack Compose Fundamentals
- Introduction to declarative UI paradigm
- Setting up a Jetpack Compose project
- Understanding Composable functions
- Basic UI components and layouts
- State management in Compose
- Building interactive elements

### Day 4-5: Building the Taskify UI
- Implementing navigation in Compose
- Creating task list screens
- Building forms and input fields
- Implementing authentication screens
- Working with themes and styling
- Integration of UI components

### Day 6-7: Android Basics & Architecture
- Activity lifecycle and configuration changes
- Intent system and navigation
- Android resources and qualifiers
- Background processing with Services and WorkManager
- Data sharing with ContentProviders
- Architecture components (ViewModel)

## Tasks - Jetpack Compose UI Implementation

For the UI implementation of our Taskify app, we'll divide the work into 4 modules. Each mentee will be responsible for implementing one of the following UI components:

### 🔹 Mentee 1 – `Authentication Screens`
- Create a sign-in screen with:
    - Email and password input fields
    - Sign-in button
    - Navigation to registration
    - Error handling and validation
- Create a registration screen with:
    - Username, email, password, and confirmation fields
    - Registration button
    - Navigation back to sign-in
    - Form validation

**Files to create:**
```
presentation/auth/
├── LoginScreen.kt
└── RegisterScreen.kt
```

**Key Composables to use:**
- TextField/OutlinedTextField
- Button
- Text
- Column
- Spacer
- Box

**Reference:** 
<div align="center">
  <img src="/App/kotlin/Week-2/ui/login.jpg" alt="Login Screen" width="200" height="420">
  <img src="/App/kotlin/Week-2/ui/register.jpg" alt="Register Screen" width="200" height="420"> <br/>
</div>

### 🔹 Mentee 2 – `Task feature`
- Create the main task list screen with:
    - Task filtering tabs (To Do, In Progress, Done)
    - Task cards with priority indicators
    - Filter and sort buttons
    - Add task button
- Implement individual task items with:
    - Task title and description
    - Priority indicator
    - Task status controls
    - Edit and delete options

**Files to create:**
```
presentation/tasks/
├── /components
|        └── TaskItem.kt
└── TaskScreen.kt
```

**Key Composables to use:**
- LazyColumn
- Card
- Row
- Icon
- TabRow
- DropdownMenu
- Divider

**Reference:**
<div align="center">
  <img src="/App/kotlin/Week-2/ui/TaskScreen.jpg" alt="Task Screen" width="200" height="420">
</div>


### 🔹 Mentee 3 – `Notes Feature & Navigation Drawer`
- Create the notes list screen with:
    - List of notes
    - Add note button
    - Search functionality
- Implement navigation drawer with:
    - User profile section
    - Navigation items (Tasks, Notes, Settings)
    - Logout option

**Files to create:**
```
presentation/notes/
├── /components
|        └── NoteItem.kt
└── NoteScreen.kt

presentation/components/
└── NavigationDrawer.kt
```

**Key Composables to use:**
- ModalDrawerSheet
- NavigationDrawerItem
- SearchBar
- LazyColumn
- FloatingActionButton
- IconButton

**Reference:**
<div align="center">
  <img src="/App/kotlin/Week-2/ui/NotesScreen.jpg" alt="Task Screen" width="200" height="420">
  <img src="/App/kotlin/Week-2/ui/NavigationDrawer.jpg" alt="Task Screen" width="200" height="420">
</div>

### 🔹 Mentee 4 – `Task/Note Dialog Components`
- Create task/note detail screens with:
    - Editable title and content
    - Save/update functionality
    - Delete confirmation
- Implement reusable dialog components:
    - Add/Edit task dialog
    - Delete confirmation dialog
    - Priority selection dialog

**Files to create:**
```

presentation/tasks/
└── /components
        └── TaskDialog.kt
        
presentation/notes/
└── /components
        └── NotesDialog.kt
```

**Key Composables to use:**
- AlertDialog
- OutlinedTextField
- RadioButton
- Checkbox
- DatePicker
- Slider
- TextButton

**Reference:**
    <div align="center">
      <img src="/App/kotlin/Week-2/ui/TaskDialog.jpg" alt="Task Screen" width="200" height="420">
      <img src="/App/kotlin/Week-2/ui/NotesDialog.jpg" alt="Task Screen" width="200" height="420">
    </div>

[//]: # (## Integration)

[//]: # ()
[//]: # (Each mentee will develop their assigned components independently, but we'll integrate them into a single working application. The integration will be handled through a common navigation graph:)

[//]: # ()
[//]: # (```kotlin)

[//]: # (@Composable)

[//]: # (fun TaskifyNavHost&#40;navController: NavHostController&#41; {)

[//]: # (    NavHost&#40;navController = navController, startDestination = "signin"&#41; {)

[//]: # (        composable&#40;"signin"&#41; { SignInScreen&#40;navController&#41; })

[//]: # (        composable&#40;"register"&#41; { RegisterScreen&#40;navController&#41; })

[//]: # (        composable&#40;"tasks"&#41; { TaskListScreen&#40;navController&#41; })

[//]: # (        composable&#40;"notes"&#41; { NotesScreen&#40;navController&#41; })

[//]: # (        composable&#40;"task_detail/{taskId}"&#41; { backStackEntry ->)

[//]: # (            TaskDetailScreen&#40;navController, backStackEntry.arguments?.getString&#40;"taskId"&#41;&#41;)

[//]: # (        })

[//]: # (        composable&#40;"note_detail/{noteId}"&#41; { backStackEntry ->)

[//]: # (            NoteDetailScreen&#40;navController, backStackEntry.arguments?.getString&#40;"noteId"&#41;&#41;)

[//]: # (        })

[//]: # (    })

[//]: # (})

[//]: # (```)

## Android Basics Tasks

In addition to the UI implementation, you should read about the following topics as a task to understand Android fundamentals:
- Tasks, Back Stack & Launch Modes
- Viewmodel and Configuration changes
- Context
- Resource and Qualifiers
- Intent and Intent Filters
- Broadcast Receivers and Broadcast

## Bonus Tasks

### Jetpack Compose Bonus
1. **Custom Animations**:
    - Implement custom animations between screens
    - Add animated content transitions
    - Create loading animations

2. **Advanced Composables**:
    - Create custom composables with slots API
    - Use remember and derived state
    - Implement draggable elements

3. **Canvas Drawing**:
    - Create custom UI elements using Canvas
    - Implement a simple drawing app
    - Create custom charts/graphs

4. **Accessibility**:
    - Optimize your UI for screen readers
    - Implement content descriptions
    - Test with TalkBack

### Android Basics Bonus
1. **Deep Links**:
    - Implement deep links to specific screens in your app
    - Handle deep link parameters
2. **Work Manager**
    - One time work request
    - Periodic Worker

3. **Content Providers**:
    - Create a custom ContentProvider
    - Access and display data from device contacts

4. **Custom Views**:
    - Create a hybrid app using both XML layouts and Jetpack Compose
    - Compare the approaches

5. **URIS**

## Learning Resources

### Jetpack Compose Resources
1. **Official Documentation**:
    - [Jetpack Compose Documentation](https://developer.android.com/jetpack/compose)
    - [Compose Pathway](https://developer.android.com/courses/pathways/compose)

2. **Interactive Learning**:
    - [Compose Codelab](https://developer.android.com/codelabs/jetpack-compose-basics)
    - [Compose Samples](https://github.com/android/compose-samples)

3. **Video Tutorials**:
    - [Jetpack Compose by Philipp Lackner](https://www.youtube.com/playlist?list=PLQkwcJG4YTCSpJ2NLhDTHhi6XBNfk9WiC)
    - [Compose by Google Developers](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc_L3n1j4ajHjp0AOi4ULs59)

4. **Articles**:
    - [Understanding Compose](https://medium.com/androiddevelopers/understanding-jetpack-compose-part-1-of-2-ca316fe39050)
    - [Thinking in Compose](https://developer.android.com/jetpack/compose/mental-model)

### Android Basics Resources
1. **Official Documentation**:
    - [Android Developer Fundamentals](https://developer.android.com/guide/components/fundamentals)
    - [Android Architecture Components](https://developer.android.com/topic/libraries/architecture)

2. **Video Tutorials**:
    - [Android Fundamentals playlist by Phillip Lackner (Recommended)](https://youtube.com/playlist?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm)
    - [Android Development Patterns](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc-lJo_RGGXL2Psr8vVCTWjM)

3. **Articles**:
    - [Understanding the Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
    - [Guide to App Architecture](https://developer.android.com/topic/architecture)

## Guidelines

1. **Code Organization**: Follow the recommended project structure
2. **Naming Conventions**: Use descriptive names for functions and variables
3. **Comments**: Add comments to explain complex logic
4. **Documentation**: Create a README for your component explaining its functionality
5. **Testing**: Write basic UI tests for your components
6. **Collaboration**: Use Git for version control and follow good branching practices
7. **Reusability**: Create reusable components when possible

## Weekly Checklist
- [ ] Complete assigned UI component implementation
- [ ] Ensure UI matches provided design mockups
- [ ] Successfully integrate your component with others
- [ ] Complete all Android basics tasks
- [ ] Submit PR with your implementation
- [ ] (Optional) Complete bonus tasks

Good luck with implementing the Taskify UI and learning Android fundamentals! By the end of this week, we'll have a complete UI ready for backend integration in the coming weeks.
