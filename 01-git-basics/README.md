# 01-git-basics

## What You'll Learn

By the end of this module, you'll understand:
- What Git is and why it's essential for version control
- How to initialize and configure a Git repository
- How to stage, commit, and push changes
- How to view commit history and file status
- How to work with remote repositories
- Best practices for meaningful commit messages

## Prerequisites

- A computer with Windows, macOS, or Linux
- Git installed (version 2.0+)
- A text editor (VS Code, Notepad, etc.)
- Basic command-line/terminal knowledge
- A GitHub account (optional for this module)

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Repository** | A folder where Git tracks all changes |
| **Staging Area** | A temporary space to prepare changes before committing |
| **Commit** | A snapshot of your project at a specific point in time |
| **Working Directory** | The actual files on your computer that you're editing |
| **Remote** | A copy of your repository hosted on a server (like GitHub) |
| **Branch** | An independent line of development (we'll cover this in Module 2) |
| **.gitignore** | A file that tells Git which files to ignore |

## Hands-on Lab: Setting Up Your First Git Repository

### Scenario
You're starting a new project called "my-first-app". You'll initialize Git, create a file, stage it, commit it, and view the history.

### Step-by-Step Commands

```bash
# Step 1: Create a project directory
mkdir my-first-app
cd my-first-app

# Step 2: Initialize a Git repository
git init

# Step 3: Configure your Git identity (one-time setup)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Step 4: Create a project file
echo "# Welcome to my first app" > README.md

# Step 5: Check the status
git status

# Step 6: Stage the file
git add README.md

# Step 7: Commit the file with a meaningful message
git commit -m "Initial commit: Add project README"

# Step 8: View commit history
git log

# Step 9: View detailed log
git log --oneline

# Step 10: Check your configuration
git config --list
```

### Expected Output

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git track")

---

On branch master

Initial commit (commits 1)
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

---

[master (root-commit) abc1234] Initial commit: Add project README
 1 file changed, 1 insertion(+)
 create mode 100644 README.md

---

commit abc1234567890abcdef1234567890abcdef1234567
Author: Your Name <your.email@example.com>
Date:   Wed Jan 15 10:30:00 2026 +0000

    Initial commit: Add project README
```

## Validation

You've successfully completed this lab if:
- ✓ Git repository is initialized (`.git` folder exists)
- ✓ You can run `git log --oneline` and see your commit
- ✓ `git status` shows "nothing to commit"
- ✓ Your name and email are configured in Git

## Cleanup

To delete the practice repository:
```bash
cd ..
rm -rf my-first-app
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|-------------|-----------|
| Forgetting `git add` before commit | Files aren't staged, commit fails | Always run `git add` first |
| Using vague commit messages ("update") | Hard to understand what changed | Write descriptive messages |
| Not configuring user.name/email | Commits show "unknown user" | Run `git config user.name "Your Name"` |
| Working in wrong directory | Can't find files or create repo | Use `pwd` to check location, `cd` to navigate |
| Typos in commands | Commands fail silently | Double-check your typing, use tab completion |

## Troubleshooting

**Q: I got "fatal: not a git repository" error**
- A: You're in a folder without Git initialized. Run `git init` or navigate to a folder that has `.git`

**Q: How do I see what's different between my changes and the last commit?**
- A: Run `git diff` to see unstaged changes, or `git diff --cached` for staged changes

**Q: I committed with the wrong name. How do I fix it?**
- A: For the last commit: `git commit --amend --author="New Name <email@example.com>"` (we'll cover this in Module 3)

**Q: Where does Git store all my data?**
- A: In the hidden `.git` folder. Don't delete it!

**Q: Can I undo my last commit?**
- A: Yes! We'll cover this in Module 3 (Rewriting History and Recovery)

## Next Steps

Once you're comfortable with:
- Creating repositories
- Staging and committing files
- Viewing history

Move to **Module 2: Git Branching and Merging** to learn how to work on multiple features simultaneously.

---

**Time to Complete:** 30 minutes  
**Difficulty Level:** Beginner  
**Hands-on Practice:** Yes
