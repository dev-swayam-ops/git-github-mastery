# 07-github-pull-requests-and-code-review: Solutions

## Solution 1: Create a Pull Request from GitHub UI

**Steps:**
1. Navigate to your fork on GitHub
2. Click "Contribute" button
3. Click "Open pull request"
4. Ensure base repository is correct
5. Write title and description
6. Click "Create pull request"

**Explanation:** Creating a PR via GitHub UI is the most straightforward way. The base branch should be the original repository's main branch, and the compare branch should be your feature branch.

---

## Solution 2: Create a Pull Request Using GitHub CLI

```bash
# Assuming you're on your feature branch
gh pr create --title "Add authentication feature" --body "This PR adds user login functionality"
```

**Explanation:** GitHub CLI automates PR creation with command-line tools. Useful for automation and scripting.

---

## Solution 3: Add Detailed Description and Comments

```bash
# When creating PR via CLI with file input
gh pr create --title "Feature Title" --body-file pr-description.txt

# Or manually add to existing PR
gh pr comment PR_NUMBER --body "Additional context about this change"
```

**Content of pr-description.txt:**
```
## Description
This PR adds user authentication to the application.

## Changes
- Added login form component
- Integrated password hashing
- Added session management

## Testing
- Tested with Chrome, Firefox, Safari
- Verified password reset flow

## Related Issues
Closes #123
```

**Explanation:** Detailed descriptions help reviewers understand context and requirements.

---

## Solution 4: Request Review from Specific Reviewers

```bash
# Add reviewers to existing PR
gh pr edit PR_NUMBER --add-reviewer username1,username2

# Create PR with specific reviewers
gh pr create --title "Title" --reviewer username1,username2
```

**Explanation:** Requesting reviews from appropriate team members ensures code quality and knowledge sharing.

---

## Solution 5: Review Changes in Pull Request

```bash
# View PR details
gh pr view PR_NUMBER

# View PR diff
gh pr view PR_NUMBER --web  # Opens in browser

# View files changed
gh pr diff PR_NUMBER
```

**Example Output:**
```
diff --git a/app.py b/app.py
index abc..def
--- a/app.py
+++ b/app.py
@@ -10,6 +10,12 @@
     return "Hello"
 
+def login_user(username, password):
+    # Authenticate user
+    return True
```

**Explanation:** Review changes to understand what the PR does before approving.

---

## Solution 6: Add Comments to Code in PR

```bash
# Using GitHub web interface:
# 1. Go to "Files changed" tab
# 2. Hover over the line you want to comment on
# 3. Click the + icon
# 4. Type your comment
# 5. Click "Comment" or "Start a review"

# Using CLI to comment on PR
gh pr review PR_NUMBER --comment --body "This function needs error handling"
```

**Explanation:** Line-specific comments help provide targeted feedback on specific code changes.

---

## Solution 7: Approve a Pull Request

```bash
# Approve PR via CLI
gh pr review PR_NUMBER --approve --body "Looks good! Great work"

# Or without message
gh pr review PR_NUMBER --approve
```

**Explanation:** Approval indicates the reviewer has verified the code meets quality standards.

---

## Solution 8: Request Changes in Code Review

```bash
# Request changes if issues are found
gh pr review PR_NUMBER --request-changes --body "Please add error handling for database failures"

# View all reviews
gh pr review PR_NUMBER --view
```

**Explanation:** "Request changes" is used when improvements are needed before merging.

---

## Solution 9: Merge a Pull Request

```bash
# Merge via CLI
gh pr merge PR_NUMBER --merge  # Create merge commit

# Squash commits before merge
gh pr merge PR_NUMBER --squash

# Rebase and merge
gh pr merge PR_NUMBER --rebase

# Delete branch after merge
gh pr merge PR_NUMBER --delete-branch
```

**Explanation:**
- `--merge`: Creates a merge commit (preserves history)
- `--squash`: Combines all commits into one (cleaner history)
- `--rebase`: Replays commits on top (linear history)

---

## Solution 10: Handle Conflicts During PR Merge

**When conflicts occur:**

```bash
# 1. Update your branch with latest main
git fetch origin
git rebase origin/main

# 2. Resolve conflicts in your files
# 3. Stage resolved files
git add resolved-file.js

# 4. Continue rebase
git rebase --continue

# 5. Force push your branch
git push origin your-branch --force-with-lease

# 6. Now PR can be merged cleanly
```

**Explanation:** Resolve conflicts locally before merging to keep main branch clean.

---

## Key Workflow

```
1. Create feature branch
2. Make commits
3. Push to fork
4. Create PR
5. Respond to reviews
6. Make changes if needed
7. Get approval
8. Merge PR
9. Delete feature branch
```

---

## Best Practices in Code Review

1. **Be specific** - Point to exact lines and explain why
2. **Ask questions** - Don't just criticize
3. **Praise good code** - Acknowledge good practices
4. **Keep it small** - Review PRs with fewer than 400 lines of changes
5. **Be timely** - Review within 24 hours
6. **Test locally** - Pull and test the code if possible
