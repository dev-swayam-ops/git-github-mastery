# 01-git-basics: Exercises

## Exercise 1: Initialize and Configure a Repository
**Difficulty:** Easy

Create a new directory called `exercise1`, initialize a Git repository, and configure your user name and email locally for this repository only.

**Instructions:**
1. Create a new folder
2. Initialize Git in it
3. Configure name and email locally
4. Verify the configuration was set

**Expected Outcome:** You should be able to see your name and email when you run `git config --list` (with `--local` flag)

---

## Exercise 2: Create and Commit Your First File
**Difficulty:** Easy

Create a file called `notes.txt`, add some text, stage it, and commit it with a meaningful message.

**Instructions:**
1. Create a `notes.txt` file with the content "Learning Git"
2. Check the status with `git status`
3. Stage the file
4. Commit with a clear message
5. View the commit log

**Expected Outcome:** You should see your commit in `git log --oneline`

---

## Exercise 3: Modify and Commit Again
**Difficulty:** Easy

Modify the `notes.txt` file from Exercise 2, add more lines, and create a new commit.

**Instructions:**
1. Open `notes.txt` and add a new line: "Git is version control"
2. Check what changed with `git diff`
3. Stage the file
4. Commit with message: "Add description to notes"
5. View the log to see both commits

**Expected Outcome:** `git log --oneline` should show 2 commits

---

## Exercise 4: Create and Add Multiple Files
**Difficulty:** Easy

Create three files (`index.html`, `style.css`, `script.js`) and commit all of them in a single commit.

**Instructions:**
1. Create three files with any content
2. Stage all three files at once using `git add .`
3. View staged files with `git status`
4. Commit all three with one message

**Expected Outcome:** `git log -p` should show all three files in one commit

---

## Exercise 5: Understand Staging Area
**Difficulty:** Medium

Create two files, stage one, modify both, and see how Git tracks them differently.

**Instructions:**
1. Create `file-a.txt` with content "A"
2. Create `file-b.txt` with content "B"
3. Stage only `file-a.txt` with `git add`
4. Modify both files
5. Run `git status` and observe what's staged vs unstaged
6. Commit and see only `file-a.txt` is committed

**Expected Outcome:** Understand the difference between working directory and staging area

---

## Exercise 6: Use .gitignore
**Difficulty:** Medium

Create a `.gitignore` file to exclude certain files from being tracked.

**Instructions:**
1. Create a `config.json` file
2. Create a `temp.txt` file
3. Create a `.gitignore` file with content `config.json`
4. Run `git status` and notice `config.json` is not listed
5. Stage and commit `.gitignore` and `temp.txt`

**Expected Outcome:** `config.json` should not appear in `git status` after `.gitignore` is created

---

## Exercise 7: View Commit History with Different Formats
**Difficulty:** Medium

Use various `git log` options to view your commit history in different ways.

**Instructions:**
1. View commits with `git log --oneline`
2. View commits with author info: `git log --pretty=format:"%h %an %ad %s"`
3. View a specific number of commits: `git log -2`
4. View a visual graph: `git log --oneline --graph`

**Expected Outcome:** Comfortable using different log formats for various purposes

---

## Exercise 8: Amend Your Last Commit
**Difficulty:** Medium

Create a commit, then fix the commit message using `git commit --amend`.

**Instructions:**
1. Create a file `feature.js` and commit it with message "add feature"
2. Run `git commit --amend -m "Add feature.js for new functionality"`
3. View the log and see the updated message

**Expected Outcome:** The commit message should be updated (original commit still exists, not a new one)

---

## Exercise 9: Separate Commits for Different Changes
**Difficulty:** Medium

Create a file, modify it in two ways, and commit the changes separately to show proper commit separation.

**Instructions:**
1. Create `app.py` with content "# App"
2. Stage and commit: "Initial app file"
3. Add a function definition
4. Stage and commit: "Add function definition"
5. Add another function
6. Stage and commit: "Add another function"
7. View log with `git log -p` to see each change separately

**Expected Outcome:** Three separate, logical commits with clear separation of concerns

---

## Exercise 10: Create Multiple Commits and View Statistics
**Difficulty:** Medium

Create multiple files/commits and use `git log` to view statistics about your repository.

**Instructions:**
1. Create 3 files in separate commits
2. Use `git log --stat` to see file changes in each commit
3. Use `git shortlog` to see commits grouped by author
4. Use `git log --all --oneline | wc -l` to count total commits

**Expected Outcome:** You should see commit statistics and understand the repository's history

---

## Summary

| Exercise | Topic | Difficulty |
|----------|-------|-----------|
| 1 | Repository Setup | Easy |
| 2 | First Commit | Easy |
| 3 | Making Changes | Easy |
| 4 | Multiple Files | Easy |
| 5 | Staging Area | Medium |
| 6 | .gitignore | Medium |
| 7 | Git Log | Medium |
| 8 | Amend Commits | Medium |
| 9 | Logical Commits | Medium |
| 10 | Repository Stats | Medium |
