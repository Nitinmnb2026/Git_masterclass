# 🚀 Day 01 - Git Practice

A hands-on learning repository documenting the first day of Git fundamentals practice. This repository serves as both a learning exercise and a reference guide for essential Git operations.

---

## 📋 Table of Contents

- [Overview](#overview)
- [What You'll Learn](#what-youll-learn)
- [Repository Structure](#repository-structure)
- [Git Commands Covered](#git-commands-covered)
- [Key Concepts](#key-concepts)
- [Quick Start](#quick-start)
- [Practice Scenarios](#practice-scenarios)

---

## Overview

This is a **beginner-friendly Git practice repository** that documents the learning journey of Git version control fundamentals. The repository showcases real-world Git workflows including:

- Basic repository initialization and staging
- Committing changes with meaningful messages
- Branch creation and switching
- Merging branches and handling merge conflicts
- Resetting and reverting changes
- Understanding Git history and reflog

---

## What You'll Learn

✅ Initialize a Git repository  
✅ Stage and commit changes  
✅ View commit history with `git log`  
✅ Create and manage branches  
✅ Merge branches together  
✅ Handle merge conflicts  
✅ Reset commits and revert changes  
✅ Use `.gitignore` to exclude files  
✅ Understand `git reflog` for recovery  

---

## Repository Structure

```
day01/
├── README.md           # This file - documentation and guide
├── .gitignore         # Files to exclude from version control
├── details.txt        # Sample file tracking user details
├── log.txt            # Sample log file
├── footer.txt         # Sample file modified across branches
└── new.log            # Sample ignored file (per .gitignore)
```

### Files Explained

| File | Purpose |
|------|---------|
| **details.txt** | First file created to practice staging and committing |
| **log.txt** | Demonstrates adding files after staging errors |
| **footer.txt** | Used to practice branching and merge conflict resolution |
| **new.log** | Example of files matched by `.gitignore` |
| **.gitignore** | Prevents `day01_practice.txt` from being tracked |

---

## Git Commands Covered

### Initialization & Status
```bash
git init              # Initialize a new repository
git status            # Check current status
git add <file>        # Stage files for commit
git add .             # Stage all changes
```

### Committing
```bash
git commit -m "message"    # Commit staged changes
git log                    # View commit history
git log --oneline          # Compact view of history
git log --graph            # Visualize branch structure
```

### Branching
```bash
git branch                 # List branches
git branch <branch-name>   # Create new branch
git checkout -b <name>     # Create and switch to branch
git checkout <branch>      # Switch to branch
git branch -d <name>       # Delete branch
```

### Merging & Conflict Resolution
```bash
git merge <branch>         # Merge branch into current branch
git commit -m "Merge: message"  # Complete merge after conflict resolution
```

### History & Recovery
```bash
git reflog                 # View all HEAD changes
git reset <commit>         # Reset to previous commit
git revert <commit>        # Create a new commit undoing changes
```

---

## Key Concepts

### 1. **Commits**
Each commit represents a snapshot of your code at a specific point in time. They should have clear, descriptive messages following conventions like:
- `feat: add new feature`
- `bugfix: resolve issue`
- `chore: initialization`

### 2. **Branches**
Branches allow you to work on features independently without affecting the main code:
- `feat/login` - Feature branch for login functionality
- `bugfix/typo` - Bug fix branch
- `master` - Main branch

### 3. **Merge Conflicts**
When two branches modify the same file, Git requires manual resolution. The repository demonstrates resolving conflicts in `footer.txt` between `master` and `bugfix/typo`.

### 4. **.gitignore**
Prevents certain files from being tracked. In this repo, `day01_practice.txt` is ignored, as is `new.log`.

### 5. **Reflog**
A safety net showing all HEAD changes, useful for recovering lost commits or understanding your Git history.

---

## Quick Start

### Clone this repository
```bash
git clone https://github.com/Nitinmnb2026/day01.git
cd day01
```

### Explore the history
```bash
# View commit history
git log --oneline --graph

# See all HEAD changes
git reflog

# Show specific commit details
git show <commit-hash>
```

### Practice on your own
```bash
# Create your own branch
git checkout -b practice/my-changes

# Make changes
echo "My practice" >> details.txt

# Stage and commit
git add .
git commit -m "feat: my practice changes"

# Switch back to main
git checkout master
```

---

## Practice Scenarios

### Scenario 1: Understanding Commits
The first commits in this repo show basic staging and committing:
- Commit 1: "Chore: initialization of code" - Initial file setup
- Commit 2: "feat: add details" - Modified content
- Commit 3: "feat: login details" - Added new file

### Scenario 2: Branch Management
The `feat/login` branch was created to add footer features independently, then merged back to `master`.

### Scenario 3: Merge Conflicts
Both `master` and `bugfix/typo` modified `footer.txt`:
- `master`: Changed background to red
- `bugfix/typo`: Changed background to green
- Conflict was resolved and merged

### Scenario 4: Reset & Revert
- `git reset` was used to go back to a previous state
- `git revert` was used to undo a specific commit while maintaining history

---

## 🎯 Next Steps

Once you master these fundamentals:

1. **Remote Repositories**: Learn `git push`, `git pull`, and `git fetch`
2. **Pull Requests**: Practice collaborative workflows
3. **Rebasing**: Understand interactive rebase and history cleanup
4. **Tags**: Learn versioning with `git tag`
5. **Stashing**: Save work in progress with `git stash`

---

## 📚 Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [GitHub Learning Lab](https://github.com/skills)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

---

## 📝 Notes

- All file contents are for educational purposes
- The commit history shows real learning progression
- `.gitignore` demonstrates how to exclude files from tracking
- This repository is a great reference for beginners learning Git

---

## 👤 Author

**Nitin Ranjan** (@Nitinmnb2026)  
Learning Git fundamentals and version control best practices.

---

## 📄 License

This repository is open for educational purposes. Feel free to fork and use it for your own learning.

---

**Happy Learning! 🎉**
