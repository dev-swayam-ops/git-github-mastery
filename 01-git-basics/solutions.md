# 01-git-basics: Solutions

## Solution 1: Initialize and Configure a Repository

```bash
# Create and navigate to directory
mkdir exercise1
cd exercise1

# Initialize Git repository
git init

# Configure user name and email (local scope)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Verify configuration
git config --list --local
```

**Explanation:** The `--local` flag stores configuration only for this repository in `.git/config`. This allows different repositories to have different user configurations (useful for work vs personal projects).

---

## Solution 2: Create and Commit Your First File

```bash
# Create file with content
echo "Learning Git" > notes.txt

# Check status
git status

# Stage the file
git add notes.txt

# Commit with meaningful message
git commit -m "Add notes.txt with initial content"

# View commit log
git log --oneline
```

**Explanation:** Meaningful commit messages help you and your team understand what changed and why. Use imperative mood ("Add" not "Added") to be consistent.

---

## Solution 3: Modify and Commit Again

```bash
# Modify the file
echo "Git is version control" >> notes.txt

# See what changed
git diff

# Stage the modification
git add notes.txt

# Commit
git commit -m "Add description to notes"

# View log with both commits
git log --oneline
```

**Expected Output:**
```
abc1234 Add description to notes
def5678 Add notes.txt with initial content
```

**Explanation:** `git diff` shows changes in unstaged files. After `git add`, use `git diff --cached` to see staged changes.

---

## Solution 4: Create and Add Multiple Files

```bash
# Create three files
echo "<html></html>" > index.html
echo "body { color: black; }" > style.css
echo "console.log('Hello');" > script.js

# Stage all files at once
git add .

# Check status (all files should be staged)
git status

# Commit all in one commit
git commit -m "Add HTML, CSS, and JavaScript files"

# View changes in this commit
git log -p -1
```

**Explanation:** `git add .` stages all modified and new files in the current directory. `-p -1` in log shows the full patch for the last commit.

---

## Solution 5: Understand Staging Area

```bash
# Create two files
echo "A" > file-a.txt
echo "B" > file-b.txt

# Stage only file-a.txt
git add file-a.txt

# Modify both files
echo "A modified" >> file-a.txt
echo "B modified" >> file-b.txt

# Check status - you'll see different states
git status

# Commit (only staged content is committed)
git commit -m "Update file-a"

# Check what happened
git show
```

**Key Insights:**
- Staged `file-a.txt` is committed
- Modifications to `file-b.txt` remain uncommitted
- You can modify a file after staging; only the staged version is committed
- `git diff` shows unstaged changes
- `git diff --cached` shows staged changes

---

## Solution 6: Use .gitignore

```bash
# Create files
echo "{ 'password': 'secret' }" > config.json
echo "temporary data" > temp.txt

# Create .gitignore
echo "config.json" > .gitignore

# Check status (config.json should not appear)
git status

# Stage .gitignore and temp.txt
git add .gitignore temp.txt

# Commit
git commit -m "Add .gitignore and temp.txt"

# Verify config.json is ignored
git status
```

**Explanation:** `.gitignore` tells Git to ignore specific files. Common patterns include:
- `*.log` - ignore all log files
- `node_modules/` - ignore entire directories
- `*.pyc` - ignore compiled Python files

---

## Solution 7: View Commit History with Different Formats

```bash
# View commits in short format
git log --oneline

# View commits with author and date
git log --pretty=format:"%h %an %ad %s" --date=short

# View last 2 commits
git log -2

# View a visual graph (especially useful with branches)
git log --oneline --graph

# View with statistics (files changed)
git log --stat

# View commits from specific author
git log --author="Your Name"
```

**Output Example:**
```
abc1234 Your Name Add notes to project
def5678 Your Name Initial commit
```

**Explanation:** Different log formats serve different purposes:
- `--oneline`: Quick overview
- `--stat`: See which files were changed
- `--graph`: Visualize branches
- `--pretty=format`: Customize output

---

## Solution 8: Amend Your Last Commit

```bash
# Create and commit a file
echo "def new_feature(): pass" > feature.js
git add feature.js
git commit -m "add feature"

# Fix the commit message
git commit --amend -m "Add feature.js for new functionality"

# Verify
git log --oneline
```

**Expected Output:**
```
abc1234 Add feature.js for new functionality
```

**Explanation:** `--amend` modifies the last commit. This is useful for:
- Fixing typos in commit messages
- Adding forgotten files (with `git add` before `--amend`)
- Improving commit messages

**Warning:** Never amend commits that are already pushed to shared branches!

---

## Solution 9: Separate Commits for Different Changes

```bash
# Create initial file
echo "# App" > app.py
git add app.py
git commit -m "Initial app file"

# Add first function
cat >> app.py << 'EOF'

def calculate(a, b):
    return a + b
EOF
git add app.py
git commit -m "Add calculate function"

# Add second function
cat >> app.py << 'EOF'

def multiply(a, b):
    return a * b
EOF
git add app.py
git commit -m "Add multiply function"

# View each commit's changes
git log -p
```

**Expected Output:**
Three separate commits with:
1. Initial file content
2. One function added
3. Second function added

**Explanation:** Separate logical changes into separate commits. This makes it easier to:
- Review code changes
- Revert specific features
- Find bugs with `git bisect`

---

## Solution 10: Create Multiple Commits and View Statistics

```bash
# Create files in separate commits
echo "Content 1" > file1.txt && git add file1.txt && git commit -m "Add file1"
echo "Content 2" > file2.txt && git add file2.txt && git commit -m "Add file2"
echo "Content 3" > file3.txt && git add file3.txt && git commit -m "Add file3"

# View statistics (files changed per commit)
git log --stat

# View commits by author (useful in teams)
git shortlog

# Count total commits
git log --oneline | wc -l

# View detailed commit information
git log --pretty=format:"%h - %an, %ar : %s"
```

**Output Example:**
```
3  (total commits)

Your Name (3):
  Add file3
  Add file2
  Add file1
```

**Explanation:** These statistics help understand:
- Repository size and activity
- Who contributes most
- Which files change frequently
- Repository growth over time

---

## Common Patterns Used in Solutions

### Pattern 1: Stage and Commit
```bash
git add <file>
git commit -m "Clear message"
```

### Pattern 2: View Changes
```bash
git diff              # Unstaged changes
git diff --cached     # Staged changes
git show <commit>     # View specific commit
```

### Pattern 3: View History
```bash
git log --oneline     # Quick view
git log -p            # Full patch
git log --stat        # File statistics
```

---

## Key Takeaways

1. **Always use clear commit messages** - Your future self will thank you
2. **Stage intentionally** - Don't use `git add .` blindly; stage related changes together
3. **Commit often** - Small, logical commits are easier to understand and revert if needed
4. **Use .gitignore** - Keep sensitive and temporary files out of version control
5. **Know your log options** - Different formats serve different purposes
