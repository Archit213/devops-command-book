# GitHub-03-Branching-Merging.md
---

# Table of Contents

- Why Branching?
- What is a Branch?
- HEAD
- Creating Branches
- Switching Branches
- Listing Branches
- Deleting Branches
- Merging Branches
- Fast-Forward Merge
- Three-Way Merge
- Merge Conflicts
- Branching Workflow
- Command Reference
- Practical Exercises
- Best Practices
- Common Mistakes
- Interview Questions

---

# Why Branching?

A branch allows developers to work on new features, bug fixes, or experiments **without affecting the main project**.

Instead of everyone working directly on the `main` or `master` branch, each feature is developed in its own branch.

---

# What is a Branch?

A branch is simply a **pointer to a commit**.

Each branch has its own history while sharing commits with other branches until they diverge.

Example:

```text
main
 │
 ●──●──●

feature-login
        \
         ●──●
```

---

# Why Use Branches?

Branches help you:

- Develop features independently.
- Fix bugs safely.
- Experiment without affecting production.
- Collaborate with team members.
- Merge changes only after testing.

---

# What is HEAD?

HEAD is a pointer that indicates the **currently checked-out branch**.

Example

```text
HEAD
 │
 ▼
main

or

HEAD
 │
 ▼
feature-login
```

To check your current branch:

```bash
git branch
```

Example Output

```text
* main
  feature-login
```

The `*` indicates the active branch.

---

# Create a Branch

## git branch

Creates a new branch.

### Syntax

```bash
git branch feature-login
```

### Example

```bash
git branch payment-module
```

This creates the branch but **does not switch to it**.

---

# List Branches

```bash
git branch
```

Example Output

```text
* main
  login
  payment
```

---

# List All Branches

```bash
git branch -a
```

Shows:

- Local branches
- Remote branches

Example

```text
main

feature-login

remotes/origin/main

remotes/origin/login
```

---

# Switch Branch

## git checkout

Moves from one branch to another.

### Syntax

```bash
git checkout branch-name
```

### Example

```bash
git checkout login
```

---

# Create and Switch

## git checkout -b

Creates a branch and immediately switches to it.

### Syntax

```bash
git checkout -b feature-payment
```

### Example

```bash
git checkout -b feature-dashboard
```

Output

```text
Switched to a new branch 'feature-dashboard'
```

---

# Using git switch

Modern Git recommends using `switch`.

### Switch Branch

```bash
git switch main
```

### Create New Branch

```bash
git switch -c login
```

---

# Delete Branch

## git branch -d

Deletes a merged branch.

### Syntax

```bash
git branch -d feature-login
```

Example

```bash
git branch -d payment
```

Output

```text
Deleted branch payment
```

---

# Force Delete Branch

```bash
git branch -D feature-login
```

Use only if the branch contains work you intentionally want to discard.

---

# Merge Branches

Merging combines changes from one branch into another.

Example

```text
main
 │
 ●──●──●
      \
       ●──● feature
```

After merge

```text
main

●──●──●────●

feature
```

---

# git merge

### Syntax

```bash
git merge branch-name
```

### Example

```bash
git checkout main

git merge feature-login
```

---

# Fast-Forward Merge

Occurs when the destination branch has not changed.

Example

```text
main

●──●

      \
       ●──● feature
```

Merge

```text
main

●──●──●──●
```

Advantages

- Clean history
- No merge commit

---

# Three-Way Merge

Occurs when both branches have new commits.

Example

```text
        feature

        ●

       /

●──●──●

       \

        ●

        main
```

Git creates a merge commit.

---

# Merge Conflict

Occurs when two branches modify the same section of a file.

Example

```text
<<<<<<< HEAD

Hello User

=======

Hello Admin

>>>>>>> feature-login
```

Steps to resolve

1. Open the file.

2. Decide which changes to keep.

3. Remove conflict markers.

4. Save the file.

5. Stage the file.

```bash
git add file.txt
```

6. Complete the merge.

```bash
git commit
```

---

# Branching Workflow

```text
main

 │

 ├─────────────── Feature A

 │

 ├─────────────── Feature B

 │

 └─────────────── Bug Fix
```

Each feature is developed independently.

---

# Command Reference

| Command | Description |
|----------|-------------|
| `git branch` | List branches |
| `git branch feature` | Create branch |
| `git branch -a` | List all branches |
| `git branch -d feature` | Delete merged branch |
| `git branch -D feature` | Force delete branch |
| `git checkout branch` | Switch branch |
| `git checkout -b branch` | Create and switch |
| `git switch branch` | Switch branch (modern Git) |
| `git switch -c branch` | Create and switch (modern Git) |
| `git merge branch` | Merge branch |

---

# Practical Exercises

## Exercise 1

Create a feature branch.

```bash
git checkout -b feature-login
```

---

## Exercise 2

Switch back to main.

```bash
git checkout main
```

---

## Exercise 3

Merge the feature.

```bash
git merge feature-login
```

---

## Exercise 4

Delete merged branch.

```bash
git branch -d feature-login
```

---

# Best Practices

- Never develop directly on `main`.
- Create one branch per feature.
- Merge only after testing.
- Delete merged branches.
- Pull the latest changes before merging.

---

# Common Mistakes

❌ Working directly on `main`.

❌ Force deleting branches accidentally.

❌ Forgetting to switch branches before editing.

❌ Ignoring merge conflicts.

---

# Interview Questions

## Why do we use branches?

Branches allow independent development without affecting the main codebase.

---

## Difference between `git branch` and `git checkout -b`?

`git branch`

Creates a branch only.

`git checkout -b`

Creates a branch and switches to it.

---

## Difference between `git checkout` and `git switch`?

`git checkout`

Can switch branches and restore files.

`git switch`

Used only for branch switching.

---

## What is a merge conflict?

A merge conflict occurs when Git cannot automatically combine changes because multiple branches modified the same part of a file.

---

## What is HEAD?

HEAD is a pointer to the currently checked-out branch.

---

## Difference between Fast-Forward Merge and Three-Way Merge?

| Fast-Forward | Three-Way |
|--------------|-----------|
| No merge commit | Creates merge commit |
| Linear history | Branch histories diverged |
| Cleaner history | Preserves branching history |

---

# Summary

In this chapter, you learned:

- Branching concepts
- HEAD
- Creating branches
- Switching branches
- Deleting branches
- Merging branches
- Fast-forward merge
- Three-way merge
- Merge conflicts
- Branching workflow
- Best practices