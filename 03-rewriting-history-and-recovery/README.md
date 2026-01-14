# 03-rewriting-history-and-recovery

## What You'll Learn

By the end of this module, you'll understand:
- How to amend commits and fix mistakes
- How to revert changes safely
- How to reset to previous states
- How to use interactive rebase
- How to cherry-pick specific commits
- How to recover lost commits using reflog
- When to use each recovery technique

## Prerequisites

- Completion of Modules 01-02
- Understanding of commits and branches
- Comfortable with git log and git diff

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Amend** | Modify the last commit |
| **Revert** | Create new commit undoing changes |
| **Reset** | Move HEAD to previous commit |
| **Interactive Rebase** | Reorder/squash/edit commits |
| **Cherry-pick** | Apply specific commit to current branch |
| **Reflog** | Record of all Git movements |
| **Hard Reset** | Discard all changes |
| **Soft Reset** | Keep changes, update HEAD |

## Hands-on Lab: Fixing Commits and Recovering Changes

### Scenario
You made commits with mistakes and need to clean them up without affecting collaborators' work.

### Step-by-Step Commands

```bash
# Step 1: Make initial commit
echo "version = 1.0.0" > version.py
git add version.py
git commit -m "Add version file"

# Step 2: Realize message has typo, amend
git commit --amend -m "Add version file with initial version"

# Step 3: Make two more commits
echo "# Config" > config.py
git add config.py
git commit -m "Add config"

echo "debug = True" >> config.py
git add config.py
git commit -m "Update config"

# Step 4: View history
git log --oneline

# Step 5: Realize you want to undo last commit
git reset --soft HEAD~1

# Step 6: Check status (changes still there)
git status

# Step 7: Re-commit properly
git commit -m "Update config with debug mode"

# Step 8: Use reflog to see all movements
git reflog
```

### Expected Output

```
[main abc1234] Add version file with initial version
[main def5678] Add config
[main ghi9012] Update config with debug mode
```

## Validation

You've successfully completed this lab if:
- ✓ Amended commit message without creating new commit
- ✓ Used reset to undo last commit
- ✓ Re-committed with proper message
- ✓ Viewed commit history with git log
- ✓ Understood reflog for recovery

## Cleanup

```bash
# Remove test files
rm -f version.py config.py
git add .
git commit -m "Cleanup: Remove test files"
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Amend after push to shared branch | History rewritten for team | Communicate, force push carefully, use --force-with-lease |
| Hard reset of shared commits | Lost commits for collaborators | Use revert instead for shared history |
| Reset --hard losing work | All changes discarded | Check reflog immediately, restore with reset --hard |
| Rebase of public branch | Team history conflicts | Only rebase your own branches |
| Cherry-pick creating duplicates | Same changes twice | Understand before cherry-picking |

## Troubleshooting

**Q: I amended a commit but pushed it already**
- A: Use `git push --force-with-lease` but inform team. Better: use revert on shared branches

**Q: How do I undo an amend?**
- A: Use `git reflog` to find previous state, then `git reset --hard` to that point

**Q: Can I interactively rebase a shared branch?**
- A: No! Only rebase branches you haven't pushed or pushed privately

**Q: What's the difference between reset, revert, and restore?**
- A: reset moves HEAD; revert creates undo commit; restore discards changes in working directory

**Q: I deleted commits, can I get them back?**
- A: Yes! `git reflog` shows all actions. Find your commit and `git reset --hard <ref>`

## Next Steps

Once comfortable with:
- Amending and reverting commits
- Using reset safely
- Recovering lost commits
- Understanding history manipulation

Move to **Module 04: Git Internals** to learn how Git actually works under the hood.

---

**Time to Complete:** 50 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
