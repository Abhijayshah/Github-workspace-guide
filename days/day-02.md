# Day 2: Git Basics - Local Setup 💻

## 📋 Overview

Today you'll install Git on your computer, configure it properly, and learn the fundamental commands that form the backbone of version control. Think of today as learning to drive before hitting the highway - we're building essential skills locally before connecting to GitHub.

## 🎯 Learning Objectives

- Understand the difference between Git and GitHub
- Install and configure Git on your operating system
- Learn essential Git commands for local version control
- Create your first local repository
- Master the staging area concept
- Write meaningful commit messages

## 📚 Prerequisites

- Completed Day 1 (GitHub account setup)
- Administrator access to your computer
- Basic command line familiarity (we'll guide you!)
- A text editor (VS Code recommended)

## ⏱️ Estimated Time

Approximately 90-120 minutes

## 🧭 Difficulty Level

🟢 **Easy** - Beginner-friendly with step-by-step guidance

---

## 📖 Theory Section

### Git vs GitHub: The Essential Difference

Many beginners confuse Git and GitHub. Here's the simple explanation:

**Git** = The Tool (like Microsoft Word)
- Version control software that runs on your computer
- Tracks changes in your files
- Works completely offline
- Created by Linus Torvalds (creator of Linux)

**GitHub** = The Platform (like Google Drive)
- Online service that hosts Git repositories
- Provides collaboration features
- Social platform for developers
- Owned by Microsoft

**Analogy**: Git is like a camera that takes snapshots of your code. GitHub is like Instagram where you share those snapshots with the world!

### Why Version Control Matters

Imagine you're writing a research paper:

**Without Version Control**:
```
my-paper.doc
my-paper-final.doc
my-paper-final-v2.doc
my-paper-final-v2-ACTUALLY-FINAL.doc
my-paper-final-v2-ACTUALLY-FINAL-professor-feedback.doc
```

**With Git**:
```
my-paper.doc (with complete history of every change)
```

Git remembers:
- **What** changed
- **When** it changed
- **Who** made the change
- **Why** they made it (commit message)

### The Three States of Git

Git files exist in three states:

1. **Working Directory** 📝: Files you're currently editing
2. **Staging Area** 📦: Files ready to be committed
3. **Repository** 🏛️: Permanently stored snapshots

Think of it like preparing for a trip:
- **Working Directory**: Clothes scattered around your room
- **Staging Area**: Clothes packed in your suitcase
- **Repository**: Suitcase locked and ready for travel

---

## 💻 Hands-On Practice

### Step 1: Installing Git

#### For Windows Users:

1. **Download Git**:
   - Visit [git-scm.com](https://git-scm.com/)
   - Click "Download for Windows"
   - Run the installer

2. **Installation Options** (recommended settings):
   - ✅ Use Git from the command line and also from 3rd-party software
   - ✅ Use the OpenSSL library
   - ✅ Checkout Windows-style, commit Unix-style line endings
   - ✅ Use MinTTY (the default terminal of MSYS2)

3. **Verify Installation**:
   ```bash
   git --version
   ```
   Expected output: `git version 2.x.x`

#### For macOS Users:

**Option 1: Using Homebrew (Recommended)**
```bash
# Install Homebrew if you don't have it
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Git
brew install git
```

**Option 2: Download from Website**
- Visit [git-scm.com](https://git-scm.com/)
- Download for macOS
- Follow installation instructions

**Verify Installation**:
```bash
git --version
```

#### For Linux Users:

**Ubuntu/Debian**:
```bash
sudo apt update
sudo apt install git
```

**CentOS/RHEL/Fedora**:
```bash
sudo yum install git
# or for newer versions
sudo dnf install git
```

**Verify Installation**:
```bash
git --version
```

### Step 2: Configuring Git

Before using Git, you need to tell it who you are:

```bash
# Set your name (use your real name)
git config --global user.name "Your Full Name"

# Set your email (use the same email as your GitHub account)
git config --global user.email "your.email@example.com"

# Set your default editor (optional)
git config --global core.editor "code --wait"  # For VS Code
# or
git config --global core.editor "nano"         # For nano (simple editor)
```

**Verify Your Configuration**:
```bash
git config --list
```

**Understanding --global vs --local**:
- `--global`: Settings apply to all repositories on your computer
- `--local`: Settings apply only to the current repository
- `--system`: Settings apply to all users on the computer

### Step 3: Creating Your First Repository

Let's create a practice project:

1. **Create a Project Directory**:
   ```bash
   # Navigate to your desired location
   cd Desktop
   
   # Create a new directory
   mkdir my-first-repo
   
   # Enter the directory
   cd my-first-repo
   ```

2. **Initialize Git Repository**:
   ```bash
   git init
   ```
   
   Expected output: `Initialized empty Git repository in /path/to/my-first-repo/.git/`

3. **Understand What Happened**:
   ```bash
   # List all files (including hidden ones)
   ls -la
   
   # You'll see a .git folder - this is where Git stores everything!
   ```

### Step 4: Making Your First Commit

1. **Create a File**:
   ```bash
   # Create a simple text file
   echo "# My First Repository" > README.md
   echo "This is my first Git repository!" >> README.md
   ```

2. **Check Repository Status**:
   ```bash
   git status
   ```
   
   Expected output:
   ```
   On branch main
   
   No commits yet
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
       README.md
   
   nothing added to commit but untracked files present (use "git add" to track)
   ```

3. **Add File to Staging Area**:
   ```bash
   git add README.md
   ```

4. **Check Status Again**:
   ```bash
   git status
   ```
   
   Expected output:
   ```
   On branch main
   
   No commits yet
   
   Changes to be committed:
     (use "git rm --cached <file>..." to unstage)
       new file:   README.md
   ```

5. **Make Your First Commit**:
   ```bash
   git commit -m "Add initial README file"
   ```
   
   Expected output:
   ```
   [main (root-commit) a1b2c3d] Add initial README file
    1 file changed, 2 insertions(+)
    create mode 100644 README.md
   ```

### Step 5: Understanding the Staging Area

Let's practice with the staging area:

1. **Modify the README**:
   ```bash
   echo "## About This Project" >> README.md
   echo "Learning Git is awesome!" >> README.md
   ```

2. **Create Another File**:
   ```bash
   echo "print('Hello, Git!')" > hello.py
   ```

3. **Check Status**:
   ```bash
   git status
   ```
   
   You'll see:
   - Modified: README.md
   - Untracked: hello.py

4. **Add Files Selectively**:
   ```bash
   # Add only README.md
   git add README.md
   
   # Check status
   git status
   ```

5. **Add All Files**:
   ```bash
   # Add all files at once
   git add .
   
   # Or add specific file
   git add hello.py
   ```

6. **Commit Changes**:
   ```bash
   git commit -m "Add project description and hello script"
   ```

### Step 6: Viewing History

```bash
# View commit history
git log

# View compact history
git log --oneline

# View history with graph
git log --oneline --graph
```

### Step 7: More Essential Commands

```bash
# See what changed in a file
git diff README.md

# See staged changes
git diff --staged

# Remove file from staging area
git reset README.md

# See current status (use this often!)
git status
```

---

## 🎯 Today's Challenge

### Main Challenge: Create a Personal Project Repository

**Objective**: Create a local Git repository for a simple personal project

**Success Criteria**:
- ✅ Git installed and configured with your information
- ✅ Local repository created and initialized
- ✅ At least 3 files created (README.md, and 2 others)
- ✅ At least 3 meaningful commits made
- ✅ Proper commit messages following best practices

**Project Ideas**:
1. **Recipe Collection**: Create markdown files with your favorite recipes
2. **Learning Journal**: Document your coding journey
3. **Simple Website**: Create HTML/CSS files for a personal page
4. **Code Snippets**: Collect useful code snippets you've learned

**Bonus Challenge**:
- 🌟 Create a .gitignore file to ignore temporary files
- 🌟 Use `git log` to view your commit history
- 🌟 Practice unstaging and restaging files
- 🌟 Write commit messages that explain "why" not just "what"

---

## 📝 Commands Summary

| Command | Purpose | Example |
|---------|---------|---------|
| `git --version` | Check Git installation | `git --version` |
| `git config --global user.name "Name"` | Set your name | `git config --global user.name "John Doe"` |
| `git config --global user.email "email"` | Set your email | `git config --global user.email "john@example.com"` |
| `git init` | Initialize repository | `git init` |
| `git status` | Check repository status | `git status` |
| `git add <file>` | Add file to staging | `git add README.md` |
| `git add .` | Add all files to staging | `git add .` |
| `git commit -m "message"` | Commit changes | `git commit -m "Add new feature"` |
| `git log` | View commit history | `git log --oneline` |
| `git diff` | See changes in files | `git diff README.md` |

---

## 🔍 Common Errors and Solutions

### ❌ "git: command not found"
**Solution**: Git is not installed or not in your PATH. Reinstall Git and restart your terminal.

### ❌ "Please tell me who you are"
**Solution**: Configure your name and email:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### ❌ "fatal: not a git repository"
**Solution**: You're not in a Git repository. Run `git init` or navigate to a Git repository.

### ❌ "nothing to commit, working tree clean"
**Solution**: No changes to commit. Make some changes to files first.

### ❌ "Changes not staged for commit"
**Solution**: Add files to staging area with `git add <filename>` before committing.

---

## 💡 Pro Tips

1. **Use `git status` Frequently**: Make it a habit to check status before and after Git commands.

2. **Commit Often**: Small, frequent commits are better than large, infrequent ones.

3. **Write Good Commit Messages**:
   ```bash
   # Good
   git commit -m "Add user authentication feature"
   
   # Bad
   git commit -m "stuff"
   git commit -m "fix"
   git commit -m "changes"
   ```

4. **Learn Keyboard Shortcuts**: 
   - `↑` arrow key recalls previous commands
   - `Tab` key auto-completes file names

5. **Create a .gitignore File**: Ignore files you don't want to track:
   ```bash
   echo "*.log" > .gitignore
   echo "node_modules/" >> .gitignore
   echo ".DS_Store" >> .gitignore
   ```

---

## 📚 Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Interactive Git Tutorial](https://learngitbranching.js.org/)
- [Git Commit Message Conventions](https://www.conventionalcommits.org/)
- [VS Code Git Integration](https://code.visualstudio.com/docs/editor/versioncontrol)

---

## ✅ Checklist

- [ ] Git installed on my computer
- [ ] Git configured with my name and email
- [ ] Created my first local repository with `git init`
- [ ] Created at least 3 files in my repository
- [ ] Used `git add` to stage files
- [ ] Made at least 3 commits with meaningful messages
- [ ] Used `git status` to check repository state
- [ ] Used `git log` to view commit history
- [ ] Practiced staging and unstaging files
- [ ] Shared progress on LinkedIn with hashtag

---

## 🎉 Reflection

Take a moment to reflect on today's learning:

1. **What did you learn today?**
   - How does the staging area concept make sense to you?
   - Which Git command do you think you'll use most often?

2. **What challenges did you face?**
   - Was the command line intimidating at first?
   - Did any Git concepts confuse you initially?

3. **How did you overcome them?**
   - What helped you understand the staging area?
   - How did practicing with real files help?

4. **What are you excited about for tomorrow?**
   - How do you think we'll connect your local repository to GitHub?

---

## 🔗 Navigation

[← Previous Day: GitHub Account Setup](./day-01.md) | [Back to Main](../README.md) | [Next Day: Remote Connection →](./day-03.md)

---

💡 **Remember**: "The expert in anything was once a beginner." - Helen Hayes

**Congratulations! You now have Git running on your computer and understand the basics of version control. Tomorrow, we'll connect your local repository to GitHub and learn about remote repositories. You're building real developer skills! 🎉**