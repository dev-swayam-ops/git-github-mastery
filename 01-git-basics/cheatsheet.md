# 01-git-basics: Cheatsheet

## Essential Commands Quick Reference

### Repository Setup

| Command | Purpose | Example |
|---------|---------|---------|
| `git init` | Initialize a new repository | `git init my-project` |
| `git config user.name` | Set your name | `git config user.name "John Doe"` |
| `git config user.email` | Set your email | `git config user.email "john@example.com"` |
| `git config --global` | Set globally for all repos | `git config --global user.name "John"` |
| `git config --list` | View all configurations | `git config --list` |

### Basic Workflow

| Command | Purpose | Example |
|---------|---------|---------|
| `git status` | Show working directory status | `git status` |
| `git add <file>` | Stage a file | `git add README.md` |
| `git add .` | Stage all changes | `git add .` |
| `git commit -m "message"` | Commit staged changes | `git commit -m "Add readme"` |
| `git log` | View commit history | `git log` |
| `git log --oneline` | View commits in one line | `git log --oneline` |

### Viewing Changes

| Command | Purpose | Example |
|---------|---------|---------|
| `git diff` | Show unstaged changes | `git diff` |
| `git diff --cached` | Show staged changes | `git diff --cached` |
| `git diff <commit1> <commit2>` | Compare two commits | `git diff abc123 def456` |
| `git show <commit>` | View specific commit details | `git show abc123` |

### History & Information

| Command | Purpose | Example |
|---------|---------|---------|
| `git log --stat` | Show files changed in commits | `git log --stat` |
| `git log -p` | Show full patch with diffs | `git log -p` |
| `git log -2` | Show last 2 commits | `git log -2` |
| `git log --author="Name"` | Show commits by author | `git log --author="John"` |
| `git log --oneline --graph` | Visual commit graph | `git log --oneline --graph` |
| `git shortlog` | Commits grouped by author | `git shortlog` |

### Fixing Mistakes

| Command | Purpose | Example |
|---------|---------|---------|
| `git restore <file>` | Discard changes in working directory | `git restore file.txt` |
| `git restore --staged <file>` | Unstage a file | `git restore --staged file.txt` |
| `git commit --amend -m "new message"` | Fix last commit message | `git commit --amend -m "Correct message"` |
| `git reset HEAD~1` | Undo last commit (keep changes) | `git reset HEAD~1` |

### Remote Repositories (Introduction)

| Command | Purpose | Example |
|---------|---------|---------|
| `git clone <url>` | Clone a remote repository | `git clone https://github.com/user/repo.git` |
| `git remote -v` | Show remote repositories | `git remote -v` |
| `git push` | Push changes to remote | `git push origin main` |
| `git pull` | Fetch and merge from remote | `git pull origin main` |

### Helpful Information

| Command | Purpose | Example |
|---------|---------|---------|
| `git --version` | Check Git version | `git --version` |
| `git help <command>` | Get help on a command | `git help commit` |
| `git status --short` | Compact status view | `git status --short` |

---

## .gitignore Patterns

```bash
# Ignore a specific file
config.json

# Ignore all files with an extension
*.log
*.tmp
*.pyc

# Ignore a directory
node_modules/
__pycache__/

# Ignore files matching a pattern
logs/*

# Exception - don't ignore this file
!important.log

# Ignore files in any subdirectory
**/temp
```

---

## Common Workflows

### Workflow 1: Adding a New Feature
```bash
git add new-feature.js
git commit -m "Add new feature"
```

### Workflow 2: Modifying Existing Code
```bash
git status                    # Check what changed
git diff                      # Review changes
git add modified-file.js      # Stage changes
git commit -m "Update logic"  # Commit with clear message
```

### Workflow 3: Multiple Changes in Separate Commits
```bash
git add file1.js
git commit -m "Fix issue A"

git add file2.js
git commit -m "Update feature B"

git log --oneline             # View both commits
```

### Workflow 4: Reviewing Before Committing
```bash
git status                    # See what's changed
git diff                      # Review unstaged changes
git add file1.js              # Stage what you want
git diff --cached             # Review staged changes
git commit -m "Specific change"
```

---

## Status Symbols

When you run `git status --short`:

```
 M file.js       # Modified file (staged)
M  file.js       # Modified file (unstaged)
A  file.js       # Added file
D  file.js       # Deleted file
?? file.js       # Untracked file
```

---

## Configuration Examples

```bash
# Set name (one-time)
git config user.name "Your Name"

# Set email (one-time)
git config user.email "your.email@example.com"

# Set globally
git config --global user.name "Your Name"

# View all settings
git config --list

# Set default editor
git config core.editor "vim"

# Set line ending handling (Windows)
git config core.autocrlf true
```

---

## Tips & Tricks

1. **Use tab completion** - Most shells support git command completion
2. **Create aliases** - `git config alias.st status` makes `git st` work
3. **Use meaningful commit messages** - Future you will appreciate it
4. **Commit frequently** - Small, focused commits are easier to understand
5. **Check before you commit** - Use `git diff` to review changes
6. **Learn keyboard shortcuts** - `git log --oneline` is easier than `git log`

---

## Emergency Commands

| Situation | Command | Risk Level |
|-----------|---------|-----------|
| Undo unstaged changes | `git restore <file>` | Low |
| Undo staged changes | `git restore --staged <file>` | Low |
| Fix last commit message | `git commit --amend -m "..."` | Low |
| Undo last commit | `git reset HEAD~1` | Medium |
| Revert to old commit | `git reset --hard <commit>` | High ⚠️ |

---

## File Status Lifecycle

```
Untracked → Staged → Committed
            ↓
         Modified ↔ Staged → Committed
```

1. **Untracked**: New file, Git doesn't know about it
2. **Staged**: File added with `git add`, ready to commit
3. **Committed**: File saved in repository history
4. **Modified**: Previously committed file that changed
5. **Staged**: Modified file added with `git add`

---

## Time-Saving Shortcuts

```bash
# View changes and commit in one command
git diff && git add . && git commit -m "message"

# View log in pretty format
git log --pretty=format:"%h - %an, %ar : %s"

# Count commits
git log --oneline | wc -l

# See who changed what
git log -p --follow -- filename.js
```
