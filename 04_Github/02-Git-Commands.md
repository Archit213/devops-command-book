# GitHub-02-Git-Commands.md
---

# Table of Contents

- Introduction
- Repository Status
- Staging Files
- Creating Commits
- Viewing History
- Restoring Changes
- Removing Files
- Git Help
- Command Reference
- Practical Exercises
- Best Practices
- Common Mistakes
- Interview Questions

---

# Introduction

Once a Git repository has been initialized, developers perform the following workflow repeatedly:

```text
Modify Files
      │
      ▼
git status
      │
      ▼
git add
      │
      ▼
git commit
      │
      ▼
git push
```

The commands in this chapter are the ones you will use daily.

---

# Check Repository Status

## git status

Displays the current state of the repository.

Shows:

- Modified files
- New files
- Deleted files
- Staged files
- Untracked files

### Syntax

```bash
git status
```

### Example

```bash
git status
```

### Example Output

```text
On branch master

Changes not staged for commit:

modified: app.py

Untracked files:

README.md
```

### Real-world Usage

Always execute `git status` before committing code.

---

# Stage Files

## git add filename

Stages a single file.

### Syntax

```bash
git add file.txt
```

### Example

```bash
git add README.md
```

---

## git add .

Stages every modified and new file.

### Syntax

```bash
git add .
```

### Example

```bash
git add .
```

### When to Use

When you want every change to be included in the next commit.

---

# Create Commits

## git commit -m

Creates a commit using staged files.

### Syntax

```bash
git commit -m "Commit Message"
```

### Example

```bash
git commit -m "Initial commit"
```

### Output

```text
1 file changed
```

---

## Writing Good Commit Messages

Bad

```text
changes
```

Good

```text
Added login functionality

Fixed API timeout issue

Updated README

Created Dockerfile
```

---

## git commit -am

Stages modified tracked files and commits them.

### Syntax

```bash
git commit -am "message"
```

### Example

```bash
git commit -am "Updated login page"
```

### Important

This command **does not stage new files**.

If a file has never been tracked before, you must use

```bash
git add filename
```

first.

---

# View Commit History

## git log

Displays the complete commit history.

### Syntax

```bash
git log
```

### Example Output

```text
commit 8cfd...

Author: John Doe

Date:
```

---

## git log --oneline

Displays one commit per line.

### Syntax

```bash
git log --oneline
```

### Example

```text
4c2212 Initial commit

f91323 Added README

913ab4 Fixed bug
```

---

## git log --graph --decorate

Displays history as a graph.

### Syntax

```bash
git log --graph --decorate
```

### Example

```text
* commit A
|
* commit B
|
* commit C
```

Useful when working with multiple branches.

---

## git log --decorate

Displays branch pointers and HEAD.

### Syntax

```bash
git log --decorate
```

---

# Restore Changes

## git restore filename

Discard local changes.

### Syntax

```bash
git restore app.py
```

### Example

```bash
git restore main.py
```

### Result

Restores the file to its previous committed version.

---

## git restore --staged filename

Unstage a staged file.

### Syntax

```bash
git restore --staged app.py
```

### Example

```bash
git restore --staged README.md
```

Useful when you accidentally stage a file.

---

# Remove Files

## git rm

Deletes a tracked file and stages its removal.

### Syntax

```bash
git rm file.txt
```

### Example

```bash
git rm config.txt
```

---

# Git Help

## git help

Displays detailed documentation.

### Syntax

```bash
git help
```

---

## git help commit

Shows help for commit.

### Syntax

```bash
git help commit
```

---

## git commit --help

Alternative help syntax.

```bash
git commit --help
```

---

# Command Reference

| Command | Description |
|----------|-------------|
| `git status` | Show repository status |
| `git add file` | Stage one file |
| `git add .` | Stage all files |
| `git commit -m` | Commit staged changes |
| `git commit -am` | Commit modified tracked files |
| `git log` | Complete history |
| `git log --oneline` | Compact history |
| `git log --graph --decorate` | Graph view |
| `git log --decorate` | Show references |
| `git restore file` | Restore file |
| `git restore --staged file` | Unstage file |
| `git rm file` | Remove tracked file |
| `git help` | Git documentation |

---

# Practical Exercises

## Exercise 1

Check repository status.

```bash
git status
```

---

## Exercise 2

Stage everything.

```bash
git add .
```

Commit.

```bash
git commit -m "Added new feature"
```

---

## Exercise 3

View history.

```bash
git log --oneline
```

---

## Exercise 4

Restore accidental changes.

```bash
git restore app.py
```

---

## Exercise 5

Unstage a file.

```bash
git restore --staged app.py
```

---

# Best Practices

- Run `git status` before every commit.
- Write meaningful commit messages.
- Keep commits small and focused.
- Review changes before staging.

---

# Common Mistakes

❌ Using `git commit -am` expecting new files to be added.

❌ Making huge commits.

❌ Forgetting to check `git status`.

❌ Writing meaningless commit messages like "update".

---

# Interview Questions

## Difference between git add and git commit?

`git add` stages changes.

`git commit` permanently records staged changes.

---

## Difference between git commit -m and git commit -am?

`git commit -m`

- Commits staged files only.

`git commit -am`

- Automatically stages modified tracked files.
- Does not stage new files.

---

## Difference between git restore and git restore --staged?

`git restore`

Restores file contents.

`git restore --staged`

Removes files from the staging area.

---

## What does git status show?

- Modified files
- Deleted files
- Staged files
- Untracked files

---

# Summary

In this chapter you learned:

- Repository status
- Staging changes
- Creating commits
- Viewing commit history
- Restoring changes
- Removing tracked files
- Using Git help
- Best practices for committing code