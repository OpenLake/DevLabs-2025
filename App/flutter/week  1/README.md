
# 🚀 Week 1: Git, GitHub & Dart Fundamentals

Welcome to **Week 1 of Flutter Bootcamp 2025**!  
This week is all about setting up your tools, learning Git/GitHub basics for collaboration, and diving into Dart—the language behind Flutter.

## 🎯 Goals by End of Week
- Collaborate on GitHub projects
- Use essential Git commands
- Write and run Dart programs in Android Studio
- Build small command-line tools with Dart

---

## 📅 Weekly Plan

### 🔹 Days 1–3: Git & GitHub
- ✅ Install Git and Android Studio
- ✅ Learn Git basics (`init`, `add`, `commit`, `push`)
- ✅ Set up your GitHub profile and SSH key
- ✅ Fork and contribute to the `GitStartedWithUs` repo

### 🔹 Days 4–7: Dart Fundamentals
- ✅ Install Dart plugin in Android Studio
- ✅ Write your first Dart program
- ✅ Learn about:
  - Variables (`var`, `final`, `const`)
  - Input/output
  - Conditionals (`if`, `else`, `switch`)
  - Loops (`for`, `while`)
  - Functions
  - Lists, Maps
  - Null safety
  - Classes and objects

---

## ✅ Week 1 Tasks

### 🔧 Git & GitHub Tasks

**Install Git:**  
Download and install Git: https://git-scm.com/downloads

**Basic Git Practice:**
```bash
git init
git add .
git commit -m "First commit"
git status
git log
```

**GitHub Setup:**
- Create a GitHub account: https://github.com
- Set up SSH: [GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

**GitStartedWithUs Activity:**
- Fork [OpenLake/GitStartedWithUs](https://github.com/OpenLake/GitStartedWithUs)
- Clone your fork:
```bash
git clone git@github.com:<your-username>/GitStartedWithUs.git
```
- Create a branch:
```bash
git checkout -b your-branch-name
```
- Pick a pixel and color it in `style.css`
- Commit and push your changes
- Open a pull request
- Collaborate to resolve merge conflicts if needed

---

### 🧮 Dart Tasks – Build “Everyday Tools”

You will build **4 Dart programs**, each solving a basic problem.  
At the end, integrate them using a menu system in `main.dart`.

**🧰 Folder Structure:**
```
everyday_tools/
├── main.dart
├── unit_converter.dart
├── calculator.dart
├── bmi_calculator.dart
└── report_card.dart
```

Each file should expose a `run()` function to be called from `main.dart`.

#### 🔹 Task Descriptions

**unit_converter.dart**
- Convert: km ↔ mi, °C ↔ °F, kg ↔ lb
- Use `switch` to handle type selection

**calculator.dart**
- Ask user for two numbers and an operator (+, –, ×, ÷)
- Handle division by zero

**bmi_calculator.dart**
- Input weight and height
- Calculate BMI and show category

**report_card.dart**
- Input 3–5 marks
- Compute total, average, and grade (A/B/C)

**main.dart**
```dart
void main() {
  while (true) {
    print('\n🧰 Everyday Tools');
    print('1. Unit Converter');
    print('2. Calculator');
    print('3. BMI Calculator');
    print('4. Report Card');
    print('5. Exit');
    stdout.write('Choose an option: ');
    String? input = stdin.readLineSync();

    switch (input) {
      case '1': runUnitConverter(); break;
      case '2': runCalculator(); break;
      case '3': runBMICalculator(); break;
      case '4': runReportCard(); break;
      case '5': exit(0);
      default: print('Invalid option');
    }
  }
}
```

---


### Dart Challenges
- Try extension methods
- Use null-safe features like `?`, `??`, `!`
- Use lambda functions and arrow syntax
- Create a singleton using factory constructors
- Practice writing classes for basic objects (like a `Student` class)

---

## 🧠 Resources

### 🔧 Git & GitHub
- [https://www.youtube.com/watch?v=Ez8F0nW6S-w&t=1218s](https://www.youtube.com/watch?v=Ez8F0nW6S-w&t=1218s)
- [GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)


### 💡 Dart
- [Dart Docs](https://dart.dev/docs)
- [DartPad - Online Playground](https://dartpad.dev)
- [https://www.youtube.com/watch?v=Ej_Pcr4uC2Q](https://www.youtube.com/watch?v=Ej_Pcr4uC2Q)

---

## 📋 Weekly Checklist

- ✅ Installed Git and Android Studio  
- ✅ Practiced Git basics  
- ✅ Contributed to GitStartedWithUs  
- ✅ Ran your first Dart program in Android Studio  
- ✅ Completed 4 Dart mini tools  
- ✅ Integrated tools into `main.dart`  
- ✅ Try Dart Challenges 

---

## 🫱🏽‍🫲🏾 Collaboration Guidelines

- Use meaningful commit messages
- Push code frequently to GitHub
- Keep your code clean and commented
- Don’t hesitate to ask mentors questions