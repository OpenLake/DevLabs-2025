# Week 1: Git, GitHub & Kotlin Basics

Welcome to the first week of DevLabs 2025 - App Development Track! This week, we'll focus on setting up your development environment, learning Git/GitHub basics, and getting started with Kotlin fundamentals. By the end of this week, you'll have all the tools needed to begin developing our Taskify app using Kotlin and Jetpack Compose.

## Agenda

### Day 1: Development Environment Setup & Git Basics
- Installing necessary tools (Android Studio, Git)
- Understanding version control concepts
- Basic Git commands and workflow

### Day 2-4: GitHub & Collaborative Development
- Creating a GitHub account and setting up SSH keys
- Understanding repositories, branches, and pull requests
- Collaborative development workflow
- Participating in the "GitStartedWithUs" activity

### Day 4-7: Kotlin Fundamentals
- Topics:
    - Introduction
    - Why is Kotlin cool?
    - IntelliJ Installation
    - Creating the project
    - Hello world program
    - val and var

  Arithmetic operators
    - Comparison operators
    - Logical operators
    - Console input
    - Nullability & null-safe operators
    - if conditions
    - when expression
    - Exceptions & try/catch
    - Arrays
    - Loops
    - Normal functions
    - Extension functions
    - Function overloading
    - Lambda functions
    - Normal class & data class
    - Interfaces
    - Abstract classes
    - Sealed interface & sealed class
    - Enum classes
    - Singletons
    - Visibility modifiers
    - Generics

## Tasks

### Git & GitHub Tasks
1. **Install Git**: Download and install Git on your local machine
2. **Basic Git Commands**: Practice using `git init`, `git add`, `git commit`, `git status`, `git log`
3. **GitHub Account**: Create a GitHub account if you don't have one
4. **GitHub Repository**: Create your first repository on GitHub
5. **GitStartedWithUs Activity**:
    - [GitStartedWithUs Repository](https://github.com/OpenLake/GitStartedWithUs)
    - Fork the OpenLake "GitStartedWithUs" repository
    - Clone your forked repository
    - Create a new branch
    - Select a pixel to color in the grid
    - Add your color to the style.css file
    - Commit and push your changes
    - Create a Pull Request
    - Collaborate with team members to resolve any conflicts

### Kotlin Basics Tasks
### 🎯 Everyday Tools – Kotlin Console App

Welcome to your first Kotlin project! 🎉  
This project is a collection of 4 small console-based tools that we’ll build **individually**, then combine into one **modular Kotlin app**.

Each of you will build one part of the app. At the end, we’ll integrate them using a simple menu system.

---

### 📦 Task Summary

You are building a tool that helps users with small daily tasks:

| Tool Name           | Description |
|---------------------|-------------|
| Unit Converter      | Convert values between km↔mi, °C↔°F, kg↔lb |
| Simple Calculator   | Basic math: +, –, ×, ÷ |
| BMI Calculator      | Calculate BMI and give a health category |
| Report Card         | Take marks for 3-5 subjects, show total, average, grade |

---

### 🧠 Goals of the Project

You’ll practice:
- Taking user input and printing output
- Using variables and data types
- Applying conditionals (`if`, `when`)
- Using functions and loops
- Creating simple classes (optional)
- Working in a team & modularizing code

---

### 🗂 Folder Structure
[Repo Link: DevLabs-2025-Kotlin-1](https://github.com/Saurav1375/DevLabs-2025-Kotlin-1)

Each mentee will write their code in their own `.kt` file.
```
DevLabs-2025-Kotlin-1/Week-1/src/main/java/org/openlake/week1/
│
├── EverydayTool.kt                    # Menu-driven CLI app
├── UnitConverter.kt          # Module 1
├── Calculator.kt             # Module 2
├── BMICalculator.kt          # Module 3
└── ReportCard.kt             # Module 4

```

Each file will have a `fun run()` function, which gets called from the main menu.

---

### 👤 Individual Assignments

### 🔹 Akshat Gupta – `UnitConverter.kt`
- Ask user which conversion they want:
    - km ↔ miles
    - °C ↔ °F
    - kg ↔ lb
- Use `when` to handle types
- Create separate functions for each conversion

### 🔹 Swarit dixit – `Calculator.kt`
- Ask user to input two numbers
- Ask for operation: +, –, ×, ÷
- Use `when` or `if` to perform operation
- Handle division by 0 safely
- Allow repeating with a loop

### 🔹 Sourav Singh Yadav – `BMICalculator.kt`
- Take weight (kg) and height (m)
- Calculate BMI = weight / (height × height)
- Use `when` to categorize:
    - < 18.5: Underweight
    - 18.5–24.9: Normal
    - 25–29.9: Overweight
    - 30+: Obese

### 🔹 Shivangshu Sarma – `ReportCard.kt`
- Take marks for 3 to 5 subjects
- Calculate total and average
- Use `when` or `if` to give grade:
    - 90+: A, 80–89: B, etc.
- Store marks in a `List<Int>`

---

## 🧑‍💻 Integration

In `main.kt`, we’ll create a menu like:

```kotlin
fun main() {
    while (true) {
        println("\n🛠 Everyday Tools Menu")
        println("1. Unit Converter")
        println("2. Calculator")
        println("3. BMI Calculator")
        println("4. Report Card")
        println("5. Exit")
        print("Choose an option: ")

        when (readLine()?.toIntOrNull()) {
            1 -> UnitConverter.run()
            2 -> Calculator.run()
            3 -> BMICalculator.run()
            4 -> ReportCard.run()
            5 -> {
                println("Goodbye!")
                return
            }
            else -> println("Invalid option. Try again.")
        }
    }
}
```


## Bonus Tasks

### Git & GitHub Bonus
1. **Git Branching**: Create multiple branches and practice merging them
2. **Git Rebase**: Learn and practice using `git rebase` as an alternative to merging
3. **Git Hooks**: Set up a pre-commit hook to ensure code quality
4. **GitHub Actions**: Explore GitHub Actions by setting up a simple workflow
5. **Contribute to an Open Source Project**: Find a beginner-friendly open source project and submit a small PR

### Kotlin Bonus
1. **Null Safety**: Create examples demonstrating Kotlin's null safety features
2. **Extension Functions**: Write extension functions for existing classes
3. **Higher-Order Functions**: Practice using functions that take functions as parameters
4. **Data Classes**: Create data classes for a simple domain model
5. **Object Expressions**: Use object expressions and singleton objects

## Learning Resources

### Git & GitHub Resources
1. **Official Documentation**:
    - [Git Documentation](https://git-scm.com/doc)
    - [GitHub Docs](https://docs.github.com/en)

2. **Interactive Learning**:
    - [Learn Git Branching](https://learngitbranching.js.org/)
    - [GitHub Learning Lab](https://lab.github.com/)

3. **Video Tutorials**:
    - [Git & GitHub Crash Course by Traversy Media](https://www.youtube.com/watch?v=SWYqp7iY_Tc)
    - [Git Tutorial for Beginners by Programming with Mosh](https://www.youtube.com/watch?v=8JJ101D3knE)

4. **Articles**:
    - [GitHub Flow](https://guides.github.com/introduction/flow/)
    - [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

### Kotlin Resources
1. **Official Documentation**:
    - [Kotlin Official Documentation](https://kotlinlang.org/docs/home.html)
    - [Kotlin Koans](https://play.kotlinlang.org/koans/overview)

2. **Interactive Learning**:
    - [Kotlin Playground](https://play.kotlinlang.org/)
    - [Exercism Kotlin Track](https://exercism.io/tracks/kotlin)

3. **Video Tutorials**:
    - [Kotlin Course by Phillip Lackner (Recommended)](https://www.youtube.com/watch?v=dzUc9vrsldM&t=90s)
    - [Kotlin Course for Beginners by freeCodeCamp](https://www.youtube.com/watch?v=F9UC9DY-vIU)
    - [Kotlin Crash Course by Traversy Media](https://www.youtube.com/watch?v=5flXf8nuq60)

4. **Articles**:
    - [Kotlin From Scratch: Basics and Syntax](https://code.tutsplus.com/tutorials/kotlin-from-scratch-basics-and-syntax--cms-29138)
    - [Android Developers: Kotlin Guide](https://developer.android.com/kotlin/learn)

## Guidelines

1. **Submission Format**: All tasks should be submitted as GitHub repositories with proper documentation
2. **Coding Standards**: Follow Kotlin coding conventions as outlined in the [official style guide](https://kotlinlang.org/docs/coding-conventions.html)
3. **Deadlines**: Complete all tasks by the end of Week 1
4. **Help & Support**: Reach out to mentors through the designated channels if you face any issues
5. **Collaboration**: Feel free to discuss tasks with peers, but ensure your submissions are your own work

## Weekly Checklist
- [ ] Set up development environment
- [ ] Learn basic Git commands
- [ ] Create GitHub account and repository
- [ ] Complete the GitStartedWithUs activity
- [ ] Write first Kotlin program
- [ ] Complete all Kotlin basic exercises
- [ ] Submit all required tasks
- [ ] (Optional) Complete bonus tasks

Good luck, and have fun learning Git, GitHub, and Kotlin basics! These foundational skills will be essential as we progress into app development with Jetpack Compose in the coming weeks.
