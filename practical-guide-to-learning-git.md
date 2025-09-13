# 🚀 Practical Guide to Learning Git (From Scratch)

Git is one of the most important tools for developers, DevOps engineers, and anyone working with code.  
This guide is **hands-on**, so follow along step by step on your own machine.  
---
### What is Git?
- **Git** = A Distributed Version Control System (DVCS).  
- It tracks changes in your code and allows multiple people to collaborate.  
- Think of it like a **"time machine" for your code**.

### Setup Git
Install Git on your system:  
- Linux (Debian/Ubuntu):
   
```bash
  sudo apt update && sudo apt install git -y
```
#### Check installation:

```
git --version
```

#### Configure Git (Important!)

`Set up your identity (used in commits):`
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

`Check config:`
```bash
git config --list
```
#### Initialize a Repository

`Create a new project folder:`

```bash
mkdir my-first-git-project && cd my-first-git-project
```

#### Initialize Git:
```bash
git init
```
- This creates a hidden .git/ folder that stores Git history.

#### Basic Workflow

`Create a file`
```bash
echo "Hello Git" > hello.txt
```

`Check status`
```bash
git status
```

`Add file to staging`
```bash
git add hello.txt
```
`Commit changes`
```bash
git commit -m "Added hello.txt"
```

`See commit history`
```bash
git log --oneline
```

`Making Changes`

`Edit the file:`
```bash
echo "Learning Git is fun!" >> hello.txt
```

`Check status:`
```bash
git status
```

`Stage & commit:`
```bash
git add hello.txt
git commit -m "Updated hello.txt with learnin
```

#### Branching & Merging

`Create a new branch:`
```bash
git branch feature-1
```

`Switch to it:`
```bash
git checkout feature-1
```
`OR directly create & switch:`
```bash
git checkout -b feature-1
```

`Make changes, commit, then go back:`
```bash
git checkout main
git merge feature-1
```

- Branching = experiment safely.
- Merging = bring changes back.

#### Connect to GitHub / GitLab

`Create a repo on GitHub. Copy the URL.`
`Then link it:`
```bash
git remote add origin https://github.com/username/my-first-git-project.git
```

`Push your branch:`
```bash
git push -u origin main
```

`Later just use:`
```bash
git push
```
`Cloning a Repo`

`Instead of starting fresh, you can copy an existing repo:`
```bash
git clone https://github.com/username/repo.git
```

# 📝 Git Commands Cheat Sheet

| Command | Description |
|---------|-------------|
| `git init` | Initialize a new Git repository |
| `git status` | Check file changes in the working directory |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Save staged changes with a message |
| `git log` | View full commit history |
| `git log --oneline` | View short commit history |
| `git branch` | List all branches |
| `git branch <name>` | Create a new branch |
| `git checkout <branch>` | Switch to a branch |
| `git checkout -b <new-branch>` | Create + switch to a new branch |
| `git merge <branch>` | Merge another branch into current |
| `git remote add origin <url>` | Link local repo to remote |
| `git clone <url>` | Copy repo from remote |
| `git push origin <branch>` | Upload commits to remote |
| `git pull origin <branch>` | Download + merge remote changes |
| `git fetch` | Fetch changes from remote (without merging) |
| `git diff` | Show unstaged changes |
| `git reset <file>` | Unstage a file (keep changes) |
| `git revert <commit>` | Undo a commit safely |
| `git stash` | Save work temporarily |
| `git stash pop` | Restore stashed changes |
| `git tag <name>` | Create a tag (release version) |

---
✅ Use this table as a quick reference for daily Git work.
