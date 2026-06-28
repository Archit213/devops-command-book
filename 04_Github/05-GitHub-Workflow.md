# GitHub-05-GitHub-Workflow.md
---

# Table of Contents

- What is GitHub Workflow?
- Creating a Repository
- Forking a Repository
- Cloning a Repository
- Creating Feature Branches
- Commit Workflow
- Push Workflow
- Pull Requests
- Code Review
- Merge Pull Request
- Complete GitHub Collaboration Workflow
- Real-world Example
- Best Practices
- Common Mistakes
- Interview Questions

---

# What is GitHub Workflow?

GitHub Workflow is the process followed by developers to collaborate on software projects using Git and GitHub.

A typical workflow involves:

1. Create/Fork Repository
2. Clone Repository
3. Create Branch
4. Make Changes
5. Commit Changes
6. Push Changes
7. Create Pull Request
8. Code Review
9. Merge Changes

---

# GitHub Collaboration Workflow

```text
GitHub Repository
        │
        ▼
git clone
        │
        ▼
Local Repository
        │
Create Branch
        │
Modify Code
        │
git add
        │
git commit
        │
git push
        │
        ▼
GitHub
        │
Pull Request
        │
Code Review
        │
Merge
```

---

# Creating a Repository

Repositories store your project and its complete history.

Steps

1. Login to GitHub
2. Click **New Repository**
3. Enter Repository Name
4. Choose Public or Private
5. Create Repository

Repository Structure

```text
Repository

├── README.md

├── LICENSE

├── .gitignore

└── Source Code
```

---

# Clone Repository

Downloads the repository to your computer.

```bash
git clone https://github.com/user/project.git
```

Example

```bash
git clone https://github.com/devops/sample-app.git
```

---

# Create Feature Branch

Never work directly on **main**.

```bash
git checkout -b feature-login
```

or

```bash
git switch -c feature-login
```

---

# Modify Code

Example

```text
Added Login Page

Updated README

Fixed Bug

Created Dockerfile
```

---

# Stage Changes

```bash
git add .
```

---

# Commit Changes

```bash
git commit -m "Added Login Page"
```

Example Commit Messages

```text
Added User Authentication

Created Jenkins Pipeline

Updated README

Fixed Docker Build

Resolved Merge Conflict
```

---

# Push Branch

```bash
git push origin feature-login
```

Output

```text
Writing objects...

Done

remote:

Create Pull Request
```

---

# Create Pull Request

A Pull Request (PR) requests permission to merge your branch into another branch.

Most organizations require:

- Automated CI checks
- Code review
- Approval
- Merge

---

# Pull Request Workflow

```text
Feature Branch

↓

Push

↓

GitHub

↓

Open Pull Request

↓

Code Review

↓

Approval

↓

Merge

↓

Delete Branch
```

---

# Code Review

Reviewers check

- Code Quality
- Naming Convention
- Security
- Performance
- Best Practices
- Test Results

Possible Review Results

✅ Approved

🟡 Changes Requested

❌ Rejected

---

# Merge Pull Request

Once approved

GitHub merges

```text
feature-login

↓

main
```

Developers then update local repository

```bash
git checkout main

git pull origin main
```

---

# Delete Feature Branch

After merge

Delete locally

```bash
git branch -d feature-login
```

Delete remotely

```bash
git push origin --delete feature-login
```

---

# Complete GitHub Workflow

```text
Create Repository

↓

Clone Repository

↓

Create Branch

↓

Modify Files

↓

git status

↓

git add

↓

git commit

↓

git push

↓

Pull Request

↓

Code Review

↓

Merge

↓

Pull Latest Code

↓

Repeat
```

---

# Real-world Example

Suppose your team is developing an e-commerce application.

Developer A

Works on

```text
Login Feature
```

Developer B

Works on

```text
Payment Gateway
```

Developer C

Works on

```text
Order History
```

Each developer creates a separate branch.

```text
main

│

├── login-feature

├── payment-feature

└── orders-feature
```

Each branch is reviewed separately before merging.

---

# GitHub Best Practices

✅ Create one branch per feature.

✅ Never commit directly to main.

✅ Pull latest changes before starting work.

✅ Keep Pull Requests small.

✅ Write meaningful commit messages.

✅ Delete merged branches.

✅ Review code before approving.

---

# Common Mistakes

❌ Working directly on main.

❌ Creating huge Pull Requests.

❌ Forgetting to pull latest changes.

❌ Merging without code review.

❌ Ignoring merge conflicts.

❌ Poor commit messages.

---

# GitHub Workflow Cheat Sheet

```bash
git clone URL

git checkout -b feature

git status

git add .

git commit -m "message"

git push origin feature
```

Create Pull Request

↓

Review

↓

Merge

↓

```bash
git checkout main

git pull origin main

git branch -d feature
```

---

# Interview Questions

## What is GitHub?

GitHub is a cloud platform used to host Git repositories and collaborate on software development.

---

## What is a Pull Request?

A Pull Request is a request to merge one branch into another after review.

---

## Why do companies use Pull Requests?

- Code Review
- Team Collaboration
- CI/CD Validation
- Security Checks
- Quality Assurance

---

## Why shouldn't developers commit directly to main?

Direct commits bypass review and testing, increasing the risk of introducing bugs into production.

---

## What happens after a Pull Request is merged?

- The feature branch is merged into the target branch.
- Developers pull the latest changes.
- The feature branch is typically deleted.

---

## Difference between Git and GitHub

| Git | GitHub |
|------|---------|
| Version Control System | Cloud Repository Hosting Platform |
| Local software | Online collaboration platform |
| Tracks changes | Stores repositories |
| Works offline | Requires internet for collaboration |

---

# Summary

In this chapter, you learned:

- GitHub Workflow
- Creating Repositories
- Cloning Repositories
- Feature Branch Workflow
- Commit Workflow
- Push Workflow
- Pull Requests
- Code Review
- Merge Process
- Team Collaboration
- GitHub Best Practices
- Common Mistakes
- Interview Questions