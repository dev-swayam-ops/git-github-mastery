# Rewriting History and Recovery - Cheatsheet

## History Rewriting Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `git commit --amend` | Add changes to last commit | `git commit --amend` |
| `git commit --amend --no-edit` | Amend without changing message | `git commit --amend --no-edit` |
| `git reset --soft <commit>` | Move HEAD, keep changes staged | `git reset --soft HEAD~1` |
| `git reset --mixed <commit>` | Move HEAD, unstage changes (default) | `git reset HEAD~1` |
| `git reset --hard <commit>` | Move HEAD, discard all changes | `git reset --hard HEAD~1` |
| `git revert <commit>` | Create new commit that undoes changes | `git revert a1b2c3d` |
| `git cherry-pick <commit>` | Apply specific commit to current branch | `git cherry-pick a1b2c3d` |
| `git cherry-pick <c1>..<c2>` | Apply range of commits | `git cherry-pick a1b2c3d..e4f5g6h` |
| `git rebase -i HEAD~<n>` | Interactive rebase last n commits | `git rebase -i HEAD~3` |
| `git reflog` | Show recent HEAD movements | `git reflog` |
| `git reset --hard HEAD@{<n>}` | Restore to previous HEAD position | `git reset --hard HEAD@{1}` |

---

## Reset vs Revert

### git reset
- **Effect:** Moves HEAD pointer, rewrites history
- **Working Directory:** Can discard or keep changes
- **Safety:** Use only for unpushed commits
- **When to Use:** Private branches, fixing mistakes locally

```bash
git reset --soft HEAD~1   # Undo, keep changes staged
git reset HEAD~1          # Undo, keep changes unstaged
git reset --hard HEAD~1   # Undo, discard changes completely
```

### git revert
- **Effect:** Creates new commit, adds to history
- **Working Directory:** Always safe, creates inverse commit
- **Safety:** Safe for pushed commits
- **When to Use:** Public branches, removing features safely

```bash
git revert <commit>       # Creates new commit undoing the changes
```

---

## Amend Commits

### Amend Last Commit Message
```bash
git commit --amend -m "New message"
```

### Amend with New Changes
```bash
# Make changes
git add .
git commit --amend --no-edit
```

### Amend Without Changing Message
```bash
git add .
git commit --amend --no-edit
```

---

## Cherry-Pick Operations

### Single Commit
```bash
git cherry-pick <commit-hash>
```

### Multiple Commits
```bash
# Apply consecutive commits
git cherry-pick <commit1> <commit2> <commit3>

# Apply range
git cherry-pick <first-commit>..<last-commit>
```

### Handle Conflicts During Cherry-Pick
```bash
# Resolve conflicts in files
git add .
git cherry-pick --continue

# Or abort
git cherry-pick --abort
```

---

## Interactive Rebase Operations

### Start Interactive Rebase
```bash
git rebase -i HEAD~3           # Last 3 commits
git rebase -i <commit>         # All commits after <commit>
git rebase -i --root           # All commits in repository
```

### Interactive Rebase Commands
Inside the editor, each commit line has options:

```
pick   - Use commit
reword - Use commit but edit message
edit   - Use commit but stop for amending
squash - Use commit but combine with previous
fixup  - Like squash but discard commit message
drop   - Remove commit from history
```

### Example Interactive Rebase Session
```
pick a1b2c3d First commit
squash b2c3d4e Fix for first
pick c3d4e5f Second commit
reword d4e5f6g Third commit
```

---

## Reflog (Reference Logs)

### View Reflog
```bash
git reflog                    # Show your recent HEAD movements
git reflog <branch>           # Reflog for specific branch
git log -g                    # Git log style reflog output
```

### Understanding Reflog Output
```
a1b2c3d HEAD@{0}: commit: Add new feature
b2c3d4e HEAD@{1}: reset: moving to HEAD~1
c3d4e5f HEAD@{2}: checkout: moving from main to feature
```

### Recover Using Reflog
```bash
git reset --hard HEAD@{<n>}   # Go to specific reflog entry
git reset --hard <commit>     # Restore using commit hash from reflog
```

---

## Common Scenarios

### Undo Last Commit (Keep Changes)
```bash
git reset --soft HEAD~1
git add .
git commit -m "New message"
```

### Undo Last Commit (Discard Changes)
```bash
git reset --hard HEAD~1
```

### Fix Typo in Last Commit
```bash
# Edit file
git add .
git commit --amend --no-edit
```

### Combine Recent Commits
```bash
git rebase -i HEAD~3
# Change all but first to "squash"
```

### Extract Commits from Wrong Branch
```bash
# On source branch
git log --oneline | head -5  # Find commits

# On destination branch
git cherry-pick <hash1> <hash2>
```

### Remove File from Already-Committed History
```bash
# For unpushed commits
git rm <file>
git commit --amend

# For pushed commits
git revert <commit>
```

---

## Safety Tips

1. **Always work locally first**
   - Never rewrite pushed commits without team agreement
   - Rebase/amend only your own unpushed history

2. **Use reflog as a safety net**
   - `git reflog` preserves history for ~90 days
   - Can recover from almost any mistake

3. **Backup before major operations**
   ```bash
   git branch backup  # Create backup branch
   ```

4. **Use --dry-run when available**
   ```bash
   git rebase -i --dry-run HEAD~3
   ```

5. **Understand the difference**
   - Reset = Rewrite (use locally)
   - Revert = Add (use publicly)

---

## Commit Reference Shortcuts

| Syntax | Meaning |
|--------|---------|
| `HEAD` | Current commit |
| `HEAD~1` | Parent commit |
| `HEAD~2` | Grandparent commit |
| `HEAD@{0}` | Current HEAD (from reflog) |
| `HEAD@{1}` | Previous HEAD position |
| `<branch>~1` | Parent of branch tip |

