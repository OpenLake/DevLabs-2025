
---

# VS Code Extensions for Web Development

### Core Extensions

1. **Live Server** –

    Launch a local development server with live reload

    [Install Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)

2. **Prettier - Code formatter** –

    Automatically formats HTML/CSS/JS code
    
    [Install Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

3. **Auto Rename Tag** –

    Automatically rename paired HTML tags

    [Install Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)

4. **HTML CSS Support** –

    CSS class name autocomplete in HTML

    [Install HTML CSS Support](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css)

5. **Path Intellisense** –

    Autocompletion for file and folder paths

    [Install Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

6. **CSS Peek** –

    Jump to CSS definitions from HTML

    [Install CSS Peek](https://marketplace.visualstudio.com/items?itemName=pranaygp.vscode-css-peek)

### JavaScript Essentials

7. **ESLint** –

    JavaScript and JSX linting

    [Install ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

8. **JavaScript (ES6) code snippets** –

    Popular JS code snippets

    [Install JS Snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)

 
---
Here’s a clear explanation of how to **install Git** and use it within **VS Code**, based on the two links you shared:

---

# Step-by-Step Guide: Git Installation and Integration with VS Code
## Video:(https://www.youtube.com/watch?v=8HhEupU4iGU)

### 1. **Install Git on Your System**

#### Windows:

1. Go to: [https://git-scm.com/downloads](https://git-scm.com/downloads)
2. Download the **Windows installer**.
3. Run the installer and follow the setup wizard:

   * Keep the default options unless you know what you're changing.
   * Make sure **"Git from the command line and also from 3rd-party software"** is selected.
   * Install Git Bash (default).
4. After installation, restart your computer if prompted.

#### Linux (Ubuntu/Debian-based):

Open a terminal and run:

```bash
sudo apt update
sudo apt install git
```

Then verify installation:

```bash
git --version
```

---

### 2. **Configure Git (First Time Only)**

After installation, configure your name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

This information will be used to label your commits.

---

### 3. **Verify Git Integration in VS Code**

According to the official VS Code source control documentation
([VS Code Git Integration Guide](http://code.visualstudio.com/docs/sourcecontrol/overview#:~:text=The%20Source%20Control%20view%20enables,without%20using%20the%20command%20line.&text=Make%20sure%20that%20Git%20is,before%20you%20get%20these%20features.)):

> “The Source Control view enables you to initialize and manage Git repositories and perform Git operations without using the command line.”

To make sure Git works in VS Code:

1. Open **VS Code**.
2. Go to **View > Source Control** (or press `Ctrl+Shift+G`).
3. If Git is installed and detected, you’ll see **Source Control options**.

   * If you don’t see any Git features, make sure Git is in your system's PATH.

#### If Git is not detected in VS Code:

* Open VS Code Settings → Search for **Git Path**.
* Set it to the path of Git on your system:

**Example (Windows):**

```
C:\Program Files\Git\bin\git.exe
```

**Example (Linux):**
Usually auto-detected if installed via package manager.

---

### 4. **Using Git Inside VS Code**

Once Git is working in VS Code, you can:

* Initialize a repo: `Source Control > Initialize Repository`
* Stage changes: Click the `+` next to changed files
* Commit: Type a message and click the checkmark
* Push/Pull: Use the buttons at the top of the Source Control panel (after connecting a remote)

No need to use the terminal if you prefer GUI.
 