# 07-github-pull-requests-and-code-review: Quiz

## Multiple Choice Questions (7)

### Question 1: What is a Pull Request (PR)?
A) A request to pull files from your computer  
B) A request to merge changes from a feature branch into main  
C) A way to backup your code  
D) A message sent to team members  

**Correct Answer: B**

---

### Question 2: Which command creates a pull request using GitHub CLI?
A) `gh pull create`  
B) `gh pr create`  
C) `git pull request`  
D) `gh merge create`  

**Correct Answer: B**

---

### Question 3: Before creating a PR, what should you do?
A) Push your feature branch to your fork and ensure it has new commits  
B) Delete all other branches  
C) Change the main branch name  
D) Nothing, you can PR directly from local branch  

**Correct Answer: A**

---

### Question 4: What does "Approved" status on a PR mean?
A) The code is merged automatically  
B) A reviewer found the code acceptable  
C) The PR failed all tests  
D) The code is being deployed  

**Correct Answer: B**

---

### Question 5: What should you do when a reviewer requests changes?
A) Ignore the review and merge anyway  
B) Ask another reviewer to override  
C) Make the requested changes, push them, and notify the reviewer  
D) Close the PR and create a new one  

**Correct Answer: C**

---

### Question 6: What's the difference between "Approve" and "Request Changes"?
A) They mean the same thing  
B) Approve means merge now; Request Changes means never merge  
C) Approve means code is acceptable; Request Changes means improvements needed  
D) Request Changes is stronger than Approve  

**Correct Answer: C**

---

### Question 7: Which merge strategy is best for squashing commits?
A) `git merge --ff`  
B) `gh pr merge PR# --squash`  
C) `git rebase`  
D) `git merge --no-ff`  

**Correct Answer: B**

---

## Short Answer Questions (3)

### Question 8: Explain what should be included in a good PR description

**Sample Answer:**
A good PR description should include:
1. Brief summary of what the PR does
2. List of specific changes made
3. How it was tested
4. Related issue numbers (e.g., "Closes #123")
5. Any breaking changes
6. Deployment notes if relevant

This helps reviewers understand the PR's purpose and impact without reading all the code.

**Key Points:**
- Explains the "why" not just the "what"
- Makes code review faster
- Helps with future reference
- Enables tracking related issues

---

### Question 9: You have conflicts in your PR. What steps should you take?

**Sample Answer:**
1. Fetch the latest main branch: `git fetch origin main`
2. Rebase your feature branch: `git rebase origin/main`
3. Fix conflicts in the conflicted files (look for conflict markers: `<<<<<<<`, `=======`, `>>>>>>>`)
4. Stage resolved files: `git add resolved-file.js`
5. Continue rebase: `git rebase --continue`
6. Force push to your branch: `git push origin your-branch --force-with-lease`
7. The PR should now be mergeable

**Key Points:**
- Resolve locally, don't let reviewers fix conflicts
- `--force-with-lease` is safer than `--force`
- Test after resolving conflicts
- Communicate with reviewer if conflicts are significant

---

### Question 10: What's the difference between a regular PR and a Draft PR?

**Sample Answer:**
A **regular PR** is ready for review and can be merged once approved. A **Draft PR** is work-in-progress and signals that:
- You're still working on the changes
- Don't merge yet
- It's open for early feedback
- You want to share ideas before finishing

**When to use Draft:**
- Still implementing features
- Want feedback before completion
- Need discussion before finishing
- Have incomplete tests or docs

**When to convert to regular:**
- All work complete
- All tests passing
- Ready for formal review
- Ready to merge

---

## Answer Key Summary

| Question | Answer | Topic |
|----------|--------|-------|
| 1 | B | PR Definition |
| 2 | B | GitHub CLI |
| 3 | A | PR Preparation |
| 4 | B | PR Status |
| 5 | C | Handling Reviews |
| 6 | C | Review Types |
| 7 | B | Merge Strategies |
| 8 | - | PR Descriptions |
| 9 | - | Conflict Resolution |
| 10 | - | Draft PRs |

---

## Scoring Guide

**Questions 1-7:** 1 point each = 7 points

**Questions 8-10:** 3 points each = 9 points

**Total: 16 points**

### Passing Scores:
- **13+ (81%):** Excellent - Ready for next module
- **11-12 (69-75%):** Good - Review weak areas
- **9-10 (56-63%):** Fair - Need more practice
- **Below 9:** Review core PR concepts

---

## Review Checklist

After completing the quiz, you should be able to:

- [ ] Explain what a PR is and why it's important
- [ ] Create a PR using GitHub CLI or web interface
- [ ] Write clear and detailed PR descriptions
- [ ] Review code and provide constructive feedback
- [ ] Approve or request changes on PRs
- [ ] Understand and resolve merge conflicts
- [ ] Merge PRs using different strategies
- [ ] Handle PR status and checks
- [ ] Know when to use Draft PRs
- [ ] Follow code review best practices

If you can check all boxes, you're ready for the next module!
