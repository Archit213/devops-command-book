# GitHub-06-Advanced-Git.md
---

# Table of Contents

1. Introduction
2. Git Tags
3. Git Stash
4. Git Reset
5. Git Revert
6. Git Cherry-pick
7. Git Reflog
8. Undoing Mistakes
9. Git Troubleshooting
10. Complete Git Workflow
11. Git Best Practices
12. Command Reference
13. Practical Exercises
14. Interview Questions

---

# Introduction

As projects grow larger, developers need more than just commits and branches. Git provides advanced commands that help you:

- Save unfinished work
- Undo mistakes safely
- Restore deleted commits
- Apply specific commits
- Create releases
- Recover lost work

These commands are heavily used in professional DevOps teams.

---

# Git Tags

Tags are used to mark important commits such as software releases.

Example

```text
Version 1.0

↓

Tag → v1.0
```

---

## Create Tag

```bash
git tag v1.0
```

---

## List Tags

```bash
git tag
```

Example

```text
v1.0
v1.1
v2.0
```

---

## Push Tags

```bash
git push origin v1.0
```

Push all tags

```bash
git push origin --tags
```

---

## Delete Local Tag

```bash
git tag -d v1.0
```

---

## Delete Remote Tag

```bash
git push origin --delete v1.0
```

---

# Git Stash

Git Stash temporarily saves unfinished work without committing it.

Useful when:

- Switching branches
- Pulling latest changes
- Fixing production issues

---

## Save Work

```bash
git stash
```

Output

```text
Saved working directory and index state
```

---

## View Stashes

```bash
git stash list
```

---

## Apply Stash

```bash
git stash apply
```

---

## Apply and Remove

```bash
git stash pop
```

---

## Delete Stash

```bash
git stash drop
```

---

## Clear All Stashes

```bash
git stash clear
```

---

# Git Reset

Moves the current branch to a previous commit.

---

## Soft Reset

```bash
git reset --soft HEAD~1
```

Removes commit

Keeps staged changes

---

## Mixed Reset (Default)

```bash
git reset HEAD~1
```

Removes commit

Keeps modified files

---

## Hard Reset

```bash
git reset --hard HEAD~1
```

Removes

- Commit
- Staging
- Local changes

⚠ Warning

This permanently deletes uncommitted work.

---

# Git Revert

Safely undoes a commit.

Instead of deleting history, Git creates a new commit that reverses previous changes.

```bash
git revert COMMIT_ID
```

Example

```bash
git revert a23df98
```

---

# Reset vs Revert

| Reset | Revert |
|--------|---------|
| Removes commits | Creates new commit |
| Rewrites history | Preserves history |
| Dangerous on shared branches | Safe for shared repositories |

---

# Git Cherry-pick

Copies one specific commit from another branch.

Example

```bash
git cherry-pick a23df98
```

Useful when

- One bug fix is needed
- No complete merge required

---

# Git Reflog

Shows every movement of HEAD.

Even deleted commits can often be recovered.

```bash
git reflog
```

Example

```text
HEAD@{0}

HEAD@{1}

HEAD@{2}
```

Recover commit

```bash
git checkout COMMIT_ID
```

or

```bash
git reset --hard COMMIT_ID
```

---

# Undoing Mistakes

Discard local changes

```bash
git restore file.txt
```

Unstage file

```bash
git restore --staged file.txt
```

Delete commit safely

```bash
git revert COMMIT_ID
```

Delete commit permanently

```bash
git reset --hard HEAD~1
```

Recover deleted commit

```bash
git reflog
```

---

# Git Troubleshooting

## Merge Conflict

```text
<<<<<<< HEAD

Current Version

=======

Incoming Version

>>>>>>> feature
```

Resolution

1.

Edit file

2.

Remove conflict markers

3.

Save

4.

```bash
git add file.txt
```

5.

```bash
git commit
```

---

## Detached HEAD

Occurs when checking out a commit instead of a branch.

Solution

```bash
git switch main
```

or

```bash
git checkout main
```

---

## Accidental Commit

Undo

```bash
git reset HEAD~1
```

---

## Deleted Branch

Recover

```bash
git reflog
```

---

# Complete Git Workflow

```text
Clone Repository

↓

Create Branch

↓

Develop Feature

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

Review

↓

Merge

↓

Delete Branch

↓

Pull Latest Code

↓

Continue Development
```

---

# Git Best Practices

- Commit frequently.
- Use meaningful commit messages.
- Pull before pushing.
- Keep Pull Requests small.
- Never force push to production branches.
- Review code before merging.
- Use tags for releases.
- Use stash for temporary work.
- Prefer revert over reset on shared repositories.

---

# Complete Git Command Reference

| Command | Description |
|----------|-------------|
| `git tag` | List tags |
| `git tag v1.0` | Create tag |
| `git push origin --tags` | Push tags |
| `git stash` | Save unfinished work |
| `git stash list` | View stashes |
| `git stash apply` | Apply stash |
| `git stash pop` | Apply and remove stash |
| `git stash clear` | Remove all stashes |
| `git reset --soft` | Soft reset |
| `git reset --hard` | Hard reset |
| `git revert` | Reverse commit |
| `git cherry-pick` | Apply one commit |
| `git reflog` | View HEAD history |

---

# Practical Exercises

## Create Release Tag

```bash
git tag v1.0

git push origin v1.0
```

---

## Save Work

```bash
git stash
```

Switch branch

```bash
git checkout main
```

Restore

```bash
git stash pop
```

---

## Undo Last Commit

```bash
git reset --soft HEAD~1
```

---

## Recover Commit

```bash
git reflog

git reset --hard HEAD@{1}
```

---

# Common Mistakes

❌ Force pushing shared branches

```bash
git push --force
```

❌ Using hard reset without backup

❌ Forgetting to push tags

❌ Leaving multiple stash entries

❌ Cherry-picking incorrect commits

---

# Interview Questions

## Difference between Reset and Revert?

Reset rewrites history.

Revert preserves history by creating a new commit.

---

## What is Git Stash?

Temporary storage for uncommitted changes.

---

## What is Git Reflog?

History of every movement of HEAD.

Used to recover deleted commits.

---

## What is Cherry-pick?

Copies one commit from another branch.

---

## What are Git Tags?

Named references used for releases.

---

## Why is git push --force dangerous?

It rewrites remote history and may overwrite other developers' work.

---

# Complete Git Cheat Sheet

```bash
git init
git status
git add .
git commit -m "message"
git branch
git checkout -b feature
git merge feature
git remote -v
git clone URL
git push origin main
git pull origin main
git fetch origin
git tag
git stash
git reset
git revert
git cherry-pick
git reflog
```

---

# Summary

Congratulations! 🎉

You have completed the complete Git & GitHub reference guide.

You now know:

- Git Fundamentals
- Git Commands
- Branching
- Merging
- Remote Repositories
- GitHub Workflow
- Pull Requests
- Code Reviews
- Tags
- Stash
- Reset
- Revert
- Cherry-pick
- Reflog
- Git Best Practices
- Git Troubleshooting
- Real-world Git workflows

You now have a strong foundation for using Git and GitHub in professional DevOps and software development environments.