# Git & GitHub Fundamentals
---

# Table of Contents

- Introduction
- What is Version Control?
- Types of Version Control Systems
- What is Git?
- What is GitHub?
- Git Architecture
- Git Workflow
- Installing Git
- Configuring Git
- Creating Your First Repository
- Command Reference
- Practical Exercises
- Best Practices
- Common Mistakes
- Interview Questions

---

# Introduction

Software development is an iterative process where code changes frequently. Without a version control system, tracking changes, collaborating with team members, and restoring previous versions becomes difficult.

Git solves these problems by providing a distributed version control system, while GitHub provides a cloud platform to host Git repositories and enable collaboration.

---

# What is Version Control?

A **Version Control System (VCS)** is software that records changes to files over time so you can:

- Track modifications
- Restore previous versions
- Compare changes
- Collaborate with multiple developers
- Resolve conflicts

## Example

```text
Version 1
    │
    ▼
Version 2
    │
    ▼
Version 3
    │
    ▼
Latest Version
```

---

# Types of Version Control Systems

## 1. Local Version Control

Stores project history on a single computer.

### Advantages

- Simple
- Fast

### Disadvantages

- No collaboration
- Data loss if the computer fails

---

## 2. Centralized Version Control (CVCS)

Examples:

- SVN
- Perforce

```text
Developer A
      │
      ▼
Central Repository
      ▲
      │
Developer B
```

### Advantages

- Easy collaboration
- Centralized management

### Disadvantages

- Single point of failure
- Cannot commit when the server is unavailable

---

## 3. Distributed Version Control (DVCS)

Git belongs to this category.

Each developer has a complete copy of the repository.

```text
Developer A
    │
Local Repository
    │
Remote Repository
    │
Developer B
```

### Advantages

- Offline commits
- Full project history on every machine
- Faster operations
- Easy branching and merging
- Better backup and recovery

---

# What is Git?

Git is an open-source distributed version control system created by **Linus Torvalds** in 2005.

Git helps developers:

- Track changes
- Create branches
- Merge code
- Restore previous versions
- Collaborate efficiently

---

# What is GitHub?

GitHub is a cloud-based platform that hosts Git repositories.

## Git

- Version control software

## GitHub

- Repository hosting
- Team collaboration
- Pull Requests
- Issues
- Releases
- GitHub Actions
- Project management

---

# Git Architecture

Git consists of four major areas.

```text
Working Directory
        │
    git add
        ▼
Staging Area
        │
   git commit
        ▼
Local Repository
        │
    git push
        ▼
Remote Repository (GitHub)
```

## Working Directory

Contains files you are currently modifying.

## Staging Area

Contains files prepared for the next commit.

## Local Repository

Stores commit history on your machine.

## Remote Repository

Stores project history on GitHub.

---

# Git Workflow

```text
Create Files
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
      │
      ▼
GitHub Repository
```

---

# Installing Git

## Ubuntu

```bash
sudo apt update
sudo apt install git
```

## CentOS / RHEL

```bash
sudo yum install git
```

## Verify Installation

```bash
git --version
```

Example Output

```text
git version 2.48.1
```

---

# Configuring Git

## Configure Username

```bash
git config --global user.name "John Doe"
```

### Description

Sets the default author name used for commits.

---

## Configure Email

```bash
git config --global user.email "john@example.com"
```

### Description

Sets the email associated with your commits.

---

## View Configuration

```bash
git config --list
```

### Description

Displays all configured Git settings.

---

# Creating Your First Repository

## Step 1

Create a directory.

```bash
mkdir GitDemo
```

## Step 2

Navigate into the directory.

```bash
cd GitDemo
```

## Step 3

Initialize Git.

```bash
git init
```

Example Output

```text
Initialized empty Git repository in /home/user/GitDemo/.git/
```

---

# Command Reference

| Command | Description |
|----------|-------------|
| `git --version` | Displays the installed Git version |
| `git config --global user.name` | Sets the Git username |
| `git config --global user.email` | Sets the Git email |
| `git config --list` | Displays Git configuration |
| `git init` | Initializes a new Git repository |

---

# Practical Exercises

## Exercise 1 – Verify Git Installation

```bash
git --version
```

---

## Exercise 2 – Configure Git

```bash
git config --global user.name "DevOps Engineer"
git config --global user.email "devops@example.com"
git config --list
```

---

## Exercise 3 – Initialize a Repository

```bash
mkdir Demo
cd Demo
git init
```

---

# Best Practices

- Configure Git before making your first commit.
- Use your real name and email address.
- Create one Git repository per project.
- Commit frequently with meaningful messages.

---

# Common Mistakes

- Forgetting to configure username and email.
- Creating nested Git repositories unintentionally.
- Making changes before initializing Git.

---

# Interview Questions

## What is Git?

Git is a distributed version control system that tracks changes to source code.

---

## What is GitHub?

GitHub is a cloud-based platform for hosting Git repositories and collaborating with other developers.

---

## Difference between Git and GitHub?

| Git | GitHub |
|------|---------|
| Version control software | Cloud hosting platform |
| Runs locally | Runs on the web |
| Tracks history | Enables collaboration |

---

## Why is Git called a Distributed Version Control System?

Because every developer has a complete copy of the repository and its history on their local machine.

---

# Summary

In this chapter, you learned:

- Version Control concepts
- Types of Version Control Systems
- Git fundamentals
- GitHub fundamentals
- Git architecture
- Git workflow
- Installing Git
- Configuring Git
- Creating your first repository