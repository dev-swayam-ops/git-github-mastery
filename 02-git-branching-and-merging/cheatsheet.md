# Git Branching and Merging - Cheatsheet

## Common Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `git branch` | List all local branches | `git branch` |
| `git branch -a` | List local and remote branches | `git branch -a` |
| `git branch <name>` | Create new branch | `git branch feature/login` |
| `git branch -d <name>` | Delete merged branch | `git branch -d feature/login` |
| `git branch -D <name>` | Force delete branch | `git branch -D feature/old` |
| `git branch -m <old> <new>` | Rename branch | `git branch -m old-name new-name` |
| `git switch <branch>` | Switch to branch | `git switch main` |
| `git switch -c <branch>` | Create and switch to branch | `git switch -c feature/new` |
| `git checkout <branch>` | Switch branch (old syntax) | `git checkout main` |
| `git checkout -b <branch>` | Create and switch (old syntax) | `git checkout -b feature/new` |
| `git merge <branch>` | Merge branch into current | `git merge feature/login` |
| `git merge --no-ff <branch>` | Merge with merge commit | `git merge --no-ff feature/login` |
| `git merge --abort` | Cancel merge in progress | `git merge --abort` |
| `git diff <branch1> <branch2>` | Compare two branches | `git diff main feature/login` |
| `git log <branch1>..<branch2>` | Commits in branch2 not in branch1 | `git log main..feature/login` |
| `git branch -v` | Show branches with last commit | `git branch -v` |

---

## Branch Naming Conventions

```
feature/<description>     - New features
bugfix/<issue>           - Bug fixes
docs/<topic>             - Documentation
refactor/<area>          - Code refactoring
test/<feature>           - Test improvements
release/v<version>       - Release branches
hotfix/<issue>           - Production hotfixes
```

---

## Merge Types

### Fast-Forward Merge
Occurs when the feature branch contains all commits from main plus new ones. Git moves the pointer forward without creating a merge commit.

```bash
git merge feature/simple  # Automatically fast-forwards
```

### Three-Way Merge
Occurs when both branches have diverged. Git creates a merge commit combining changes from both branches.

```bash
git merge --no-ff feature/complex  # Creates merge commit
```

---

## Handling Merge Conflicts

### Identify Conflicts
```bash
git status  # Shows conflicted files
cat conflicted-file.txt  # View conflict markers
```

### Conflict Markers
```
<<<<<<< HEAD
Your current branch changes
=======
Incoming branch changes
>>>>>>> feature/branch
```

### Resolve Conflicts
```bash
# Edit the file manually and remove conflict markers
nano conflicted-file.txt

# Mark as resolved
git add conflicted-file.txt

# Complete the merge
git commit -m "Resolve merge conflict in conflicted-file.txt"
```

### Abort If Needed
```bash
git merge --abort  # Cancels merge, restores working directory
```

---

## Viewing Merge History

```bash
# See all commits with merge commits highlighted
git log --oneline

# See branch structure with graph
git log --graph --oneline --all

# See commits with authors
git log --graph --oneline --all --decorate

# Show merge commits only
git log --merges --oneline
```

---

## Tips & Patterns

### Check What Would Merge
```bash
git diff main feature/test  # See all changes
git diff --stat main feature/test  # Summary only
```

### Compare Specific Files Between Branches
```bash
git diff main feature/test -- path/to/file.js
```

### See Which Branches Are Merged
```bash
git branch --merged        # Merged into current branch
git branch --no-merged     # Not merged into current branch
```

### Undo Recent Merge
```bash
git reset --hard HEAD~1    # Undo last merge commit
git revert -m 1 <merge-commit-hash>  # Revert a merge commit
```

### Delete Multiple Branches at Once
```bash
git branch -d feature/a feature/b feature/c
git branch | grep old | xargs git branch -d  # Delete branches matching pattern
```

---

## Common Workflows

### Feature Branch Workflow
```bash
git switch -c feature/new-feature
# ... make changes and commits ...
git push origin feature/new-feature
# Create pull request on GitHub
git switch main
git merge feature/new-feature
```

### Handling Conflicts Before Merge
```bash
git fetch origin  # Get latest remote branches
git rebase origin/main  # Rebase your branch onto latest main
# Resolve any conflicts
git push origin feature/name -f
```

### Keep Feature Branch Up to Date
```bash
git switch feature/name
git merge main  # Merge latest main into your branch
# Or rebase for cleaner history
git rebase main
```

