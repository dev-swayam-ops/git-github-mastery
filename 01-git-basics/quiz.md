# 01-git-basics: Quiz

## Multiple Choice Questions (7)

### Question 1: What is a Git repository?
A) A website where you store code  
B) A folder where Git tracks all changes to your project  
C) A backup service for your files  
D) A tool for writing code  

**Correct Answer: B**

---

### Question 2: What command initializes a new Git repository?
A) `git start`  
B) `git create`  
C) `git init`  
D) `git new`  

**Correct Answer: C**

---

### Question 3: What is the staging area?
A) The main branch of your repository  
B) A temporary location where you prepare changes before committing  
C) A folder on GitHub  
D) The working directory  

**Correct Answer: B**

---

### Question 4: Which command shows your uncommitted changes?
A) `git log`  
B) `git status`  
C) `git diff`  
D) `git show`  

**Correct Answer: C**

---

### Question 5: What does `git commit` do?
A) Uploads changes to GitHub  
B) Creates a snapshot of your staged changes  
C) Deletes files from your repository  
D) Pushes code to production  

**Correct Answer: B**

---

### Question 6: What is the purpose of .gitignore?
A) To ignore mistakes in your code  
B) To hide branches from Git  
C) To specify which files Git should not track  
D) To remove files from your computer  

**Correct Answer: C**

---

### Question 7: Which command shows your commit history?
A) `git list`  
B) `git history`  
C) `git log`  
D) `git show-all`  

**Correct Answer: C**

---

## Short Answer Questions (3)

### Question 8: Explain the difference between `git add` and `git commit`

**Sample Answer:**
`git add` stages changes - it prepares files to be committed. `git commit` creates a snapshot of the staged changes and saves it to your repository history. You must `add` before you `commit`. Think of `add` as putting things in a box, and `commit` as shipping the box.

**Key Points to Include:**
- `git add` = staging (preparation)
- `git commit` = saving to history
- `add` must come before `commit`
- Multiple `add` commands can happen before one `commit`

---

### Question 9: What information should a good commit message contain?

**Sample Answer:**
A good commit message should:
1. Use imperative mood ("Add feature" not "Added feature")
2. Be concise but descriptive (50 characters or less for first line)
3. Explain WHAT changed and WHY it changed
4. For complex changes, add more details in the body
5. Start with a capital letter
6. Not include periods at the end

Example of a good message: "Add user authentication to login page"
Example of a bad message: "update stuff" or "fix bug"

**Key Points to Include:**
- Be clear and specific
- Explain the "why"
- Use consistent format
- Short first line, detailed body if needed

---

### Question 10: You modified a file but want to discard all changes and go back to the last committed version. Which command do you use and why?

**Sample Answer:**
Use `git restore <filename>` (or `git checkout <filename>` in older Git versions).

This command discards all uncommitted changes to the file and replaces it with the last committed version. 

Example: `git restore app.js`

Why: You use this when:
- You made a mistake and want to start over
- You want to test a previous version
- You accidentally modified a file you didn't want to change

**Warning:** This is irreversible for uncommitted changes!

**Key Points to Include:**
- `git restore` is the safe command for this
- It only affects uncommitted changes
- Once used, changes are permanently lost
- Use `git diff` first to review what you're losing

---

## Answer Key Summary

| Question | Answer | Topic |
|----------|--------|-------|
| 1 | B | Repository Definition |
| 2 | C | Initialization |
| 3 | B | Staging Area |
| 4 | C | Viewing Changes |
| 5 | B | Committing |
| 6 | C | .gitignore |
| 7 | C | History |
| 8 | - | add vs commit |
| 9 | - | Commit Messages |
| 10 | - | Discarding Changes |

---

## Scoring Guide

**Questions 1-7:** 1 point each = 7 points

**Questions 8-10:** 3 points each = 9 points

**Total: 16 points**

### Passing Scores:
- **13+ (81%):** Excellent - Ready for Module 2
- **11-12 (69-75%):** Good - Review weak areas before moving on
- **9-10 (56-63%):** Fair - Recommend re-doing some exercises
- **Below 9:** Need to review core concepts

---

## Review Checklist

After completing the quiz, you should be able to:

- [ ] Explain what a Git repository is
- [ ] Initialize a new repository with `git init`
- [ ] Configure your name and email
- [ ] Stage changes with `git add`
- [ ] Commit changes with `git commit`
- [ ] View history with `git log`
- [ ] See changes with `git diff` and `git status`
- [ ] Use `.gitignore` to exclude files
- [ ] Write clear commit messages
- [ ] Undo uncommitted changes with `git restore`

If you can check all boxes, you're ready to move to Module 2!
