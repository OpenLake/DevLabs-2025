# DevLabs 2025: Git & GitHub Onboarding Guide

Welcome to **DevLabs 2025** by **OpenLake**! This document will help you get started with Git and GitHub, and walk you through an introductory week of structured learning and activities.

---

## Week 1: Introduction to Git & GitHub

### Day 1: Basics

| Topic                    | Description                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------- |
| What is Git?             | Git is a distributed version control system for tracking changes in source code.      |
| Why use version control? | To collaborate efficiently, maintain history, manage features, and prevent conflicts. |
| What is GitHub?          | A cloud-based platform for hosting and collaborating on Git repositories.             |
| Install Git              | Download from [git-scm.com](https://git-scm.com) or use your package manager.         |
| GitHub Account           | Create an account at [github.com](https://github.com).                                |

#### Basic Git Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

#### Initialize a Git Repository

```bash
git init
git add .
git commit -m "Initial commit"
git log
```

---

### Day 2: Core Git Operations

| Topic                | Command/Concept                               |
| -------------------- | --------------------------------------------- |
| Staging Area         | `git add`                                     |
| Commit History       | `git log`                                     |
| Git Workflow         | Working Directory → Staging Area → Repository |
| Connecting to GitHub | HTTPS or SSH                                  |
| Remote Repository    | `git remote add origin <url>`                 |
| Push Code            | `git push origin main`                        |
| Pull Changes         | `git pull origin main`                        |
| Link to GitHub       | Create repo on GitHub, then push from local   |

---

### Day 3: GitHub Issues & Collaboration

| Concept        | Description                                |
| -------------- | ------------------------------------------ |
| Issues         | Track bugs, features, or tasks             |
| Labels         | Categorize issues (bug, enhancement, etc.) |
| Milestones     | Group issues under a goal or release       |
| Project Boards | Kanban-style tracking for tasks            |
| Assign Issues  | Assign teammates to tasks                  |

#### Pull Requests

* Fork a repository or work on a branch
* Open a Pull Request (PR)
* Request reviews and discuss changes
* Merge after approval or resolve merge conflicts if needed

---

### Day 4: Forks, Clones & Open Collaboration

| Term       | Fork                                       | Clone                        |
| ---------- | ------------------------------------------ | ---------------------------- |
| What it is | A copy of a repo under your GitHub account | A local copy on your machine |
| Use Case   | Contribute without access to the original  | Edit and test code locally   |

```bash
git clone git@github.com:your_username/repo-name.git
```

#### Keeping Fork in Sync

```bash
git remote add upstream https://github.com/original_owner/repo.git
git fetch upstream
git merge upstream/main
```

---

## Hands-on Activity: GitStartedWithUs

Practice GitHub collaboration using IIT Bhilai’s interactive repository.

**Activity Repo:** [DevLabs-2025 Canvas](https://github.com/OpenLake/GitStartedWithUs)

### Steps:

1. **Fork** the repository to your GitHub account
2. **Clone** it locally:

   ```bash
   git clone git@github.com:your_username/DevLabs-2025.git
   ```
3. **Make Changes**: Add your name to the appropriate file
4. **Commit and Push**:

   ```bash
   git add .
   git commit -m "Add my name to canvas"
   git push origin main
   ```
5. **Create Pull Request** and get it merged

---

## GitHub & Git Setup Summary

### 1. Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### 2. Add SSH Key to GitHub

```bash
clip < ~/.ssh/id_ed25519.pub  # For Windows
cat ~/.ssh/id_ed25519.pub     # For macOS/Linux
```

* Go to GitHub > Settings > SSH and GPG keys > New SSH Key > Paste and save

---

## Resources for Reference

| Resource                                                                                             | Description                            |
| ---------------------------------------------------------------------------------------------------- | -------------------------------------- |
| [Git & GitHub for Beginners](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners) | Introductory blog by HubSpot           |
| [Git Commands Cheat Sheet](https://github.com/joshnh/Git-Commands)                                   | Common Git commands with explanations  |
| [Git Flight Rules](https://github.com/k88hudson/git-flight-rules)                                    | What to do when things go wrong in Git |
| [Git Tips](https://github.com/git-tips/tips)                                                         | Community-sourced Git tips             |

---

You're now all set to begin your journey with Git, GitHub, and DevLabs 2025. Happy coding!
