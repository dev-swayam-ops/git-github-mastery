# Git Workflows and Strategies - Solutions

## Exercise 1: Set Up Git Flow Workflow - Solution

### Commands:
```bash
# Initialize repository
git init my-project
cd my-project

# Create main branch (usually exists as default)
git switch -c main
echo "Initial commit" > README.md
git add README.md
git commit -m "Initial commit on main"

# Create develop branch from main
git switch -c develop

# Create feature branch from develop
git switch -c feature/user-registration

# Make commits on feature
echo "User registration code" > auth.js
git add auth.js
git commit -m "Add user registration logic"

# Switch back to develop
git switch develop

# Create another feature branch
git switch -c feature/profile-management
echo "Profile management code" > profile.js
git add profile.js
git commit -m "Add profile management"

# Verify branch structure
git branch -a
```

### Example Output:
```
$ git branch -a
  develop
  feature/profile-management
  feature/user-registration
* main

$ git switch develop
$ git branch -a
  develop
  feature/profile-management
  feature/user-registration
* main
```

### Explanation:
Git Flow has permanent branches (main, develop) and temporary branches (feature, release, hotfix). Main is for releases only, develop is the integration branch.

---

## Exercise 2: GitHub Flow Workflow - Solution

### Commands:
```bash
# Start from main
git switch main

# Create feature branch
git switch -c feature/dark-mode
echo "Dark mode CSS" > style.css
git add style.css
git commit -m "Add dark mode styles"
echo "Dark mode JS" > script.js
git add script.js
git commit -m "Add dark mode toggle"

# Switch to main
git switch main

# Create another feature
git switch -c feature/api-endpoint
echo "def get_users():" > api.py
git add api.py
git commit -m "Add get_users API endpoint"

# Compare branches
git log main..feature/dark-mode --oneline
git log main..feature/api-endpoint --oneline

# Merge first feature
git switch main
git merge feature/dark-mode

# Delete merged branch
git branch -d feature/dark-mode

# Merge second feature
git merge feature/api-endpoint
git branch -d feature/api-endpoint

# View result
git log --oneline
```

### Example Output:
```
$ git log main..feature/dark-mode --oneline
a1b2c3d Add dark mode toggle
b2c3d4e Add dark mode styles

$ git switch main
$ git merge feature/dark-mode
Fast-forward
 script.js | 1 +
 style.css | 1 +
 2 files changed, 2 insertions(+)

$ git branch -d feature/dark-mode
Deleted branch feature/dark-mode

$ git log --oneline
a1b2c3d (main) Add dark mode toggle
b2c3d4e Add dark mode styles
c3d4e5f Initial commit
```

### Explanation:
GitHub Flow is simpler than Git Flow: one main branch, create feature branches, merge back, delete. Better for continuous deployment.

---

## Exercise 3: Trunk-Based Development Workflow - Solution

### Commands:
```bash
# Start from main (the trunk)
git switch main

# Create short-lived branch for small fix
git switch -c feature/bugfix-typo
echo "Fixed typo in README" > README.md
git add README.md
git commit -m "Fix typo in README"

# Merge back quickly
git switch main
git merge feature/bugfix-typo
git branch -d feature/bugfix-typo

# Repeat for other small changes
git switch -c feature/add-log
echo "Logging setup" > log.py
git add log.py
git commit -m "Add basic logging"
git switch main
git merge feature/add-log
git branch -d feature/add-log

# Continue with more short-lived branches
for feature in "update-readme" "add-test" "fix-import"; do
  git switch -c feature/$feature
  echo "Change" > $feature.txt
  git add $feature.txt
  git commit -m "Implement $feature"
  git switch main
  git merge feature/$feature
  git branch -d feature/$feature
done

# View frequent merges
git log --oneline | head -15
```

### Example Output:
```
$ git log --oneline | head -10
f6g7h8i (main) Implement fix-import
e5f6g7h Implement add-test
d4e5f6g Implement update-readme
c3d4e5f Add basic logging
b2c3d4e Fix typo in README
a1b2c3d Initial commit
```

### Explanation:
Trunk-based keeps main always deployable. Short-lived branches reduce merge conflicts and integrate frequently.

---

## Exercise 4: Release Branch Workflow - Solution

### Commands:
```bash
# Develop features on develop
git switch develop
git switch -c feature/new-payment
echo "Payment logic" > payment.py
git add payment.py
git commit -m "Add payment processing"
git switch develop
git merge feature/new-payment

# Create release branch
git switch -c release/1.0.0

# Bug fixes on release
echo "Fixed payment validation" > payment.py
git add payment.py
git commit -m "Fix payment validation bug"

# Create hotfix from release
git switch -c hotfix/1.0.0-critical-bug
echo "Security fix in payment" > security.py
git add security.py
git commit -m "Fix critical security bug"

# Merge hotfix back to release
git switch release/1.0.0
git merge hotfix/1.0.0-critical-bug

# Merge release to main
git switch main
git merge release/1.0.0
git tag v1.0.0

# Merge release back to develop
git switch develop
git merge release/1.0.0

# Verify
git log --oneline main
git log --oneline develop
git tag
```

### Example Output:
```
$ git log --oneline main
a1b2c3d (tag: v1.0.0, main) Merge branch 'release/1.0.0'

$ git tag
v1.0.0

$ git log --oneline develop
b2c3d4e (develop) Merge branch 'release/1.0.0'
a1b2c3d Merge branch 'release/1.0.0'
```

### Explanation:
Release branches separate release preparation from ongoing development. Both main and develop get the updates.

---

## Exercise 5: Hotfix Workflow - Solution

### Commands:
```bash
# Start at v1.0.0 on main
git switch main
git tag v1.0.0

# Create hotfix branch
git switch -c hotfix/critical-security-bug

# Fix the bug
echo "Security patch applied" > security.py
git add security.py
git commit -m "Fix critical security vulnerability"

# Tag the hotfix
git tag v1.0.1

# Merge hotfix to main
git switch main
git merge hotfix/critical-security-bug

# Also merge to develop (critical!)
git switch develop
git merge hotfix/critical-security-bug

# Delete hotfix branch
git branch -d hotfix/critical-security-bug

# Verify
git log --oneline main
git log --oneline develop
git tag
```

### Example Output:
```
$ git log --oneline main
a1b2c3d (tag: v1.0.1, main) Fix critical security vulnerability
b2c3d4e (tag: v1.0.0) Initial commit

$ git log --oneline develop
a1b2c3d (develop) Fix critical security vulnerability
b2c3d4e Initial commit

$ git tag
v1.0.0
v1.0.1
```

### Explanation:
Hotfixes solve production issues immediately. Merging to both main and develop ensures the fix reaches all development branches.

---

## Exercise 6: Feature Branching Strategy - Solution

### Commands:
```bash
# Create main features
git switch develop
git switch -c feature/auth-system
echo "Authentication implementation" > auth.py
git add auth.py
git commit -m "Auth system core"

# Create sub-features
git switch -c feature/auth-system/login
echo "Login logic" > login.py
git add login.py
git commit -m "Add login feature"
git switch feature/auth-system
git merge feature/auth-system/login

# Another sub-feature
git switch -c feature/auth-system/logout
echo "Logout logic" > logout.py
git add logout.py
git commit -m "Add logout feature"
git switch feature/auth-system
git merge feature/auth-system/logout

# Back to develop
git switch develop
git merge feature/auth-system

# Create other features
git switch -c feature/user-dashboard
echo "Dashboard UI" > dashboard.html
git add dashboard.html
git commit -m "Add user dashboard"
git switch develop
git merge feature/user-dashboard

# Clean up branches
git branch -d feature/auth-system
git branch -d feature/auth-system/login
git branch -d feature/auth-system/logout
git branch -d feature/user-dashboard

# Verify
git log --oneline develop
```

### Example Output:
```
$ git log --oneline develop
d4e5f6g (develop) Merge branch 'feature/user-dashboard'
c3d4e5f Merge branch 'feature/auth-system'
b2c3d4e Add logout feature
a1b2c3d Add login feature
```

### Explanation:
Feature branches can be nested for complex features. Sub-features merge into main feature, then main feature merges to develop.

---

## Exercise 7: Parallel Development with Multiple Branches - Solution

### Commands:
```bash
# Create 3 parallel features
git switch develop
git switch -c feature/cache-optimization
echo "Cache code" > cache.py
git add cache.py
git commit -m "Implement caching layer"

git switch develop
git switch -c feature/logging-system
echo "Logging code" > logging.py
git add logging.py
git commit -m "Add logging system"

git switch develop
git switch -c feature/error-handling
echo "Error handling" > errors.py
git add errors.py
git commit -m "Improve error handling"

# Merge features one by one
git switch develop
git merge feature/cache-optimization
git branch -d feature/cache-optimization

# Create new feature from updated develop
git switch -c feature/api-docs
echo "API documentation" > docs.md
git add docs.md
git commit -m "Add API documentation"

# Merge other features
git switch develop
git merge feature/logging-system
git merge feature/error-handling
git merge feature/api-docs

# Verify
git log --oneline develop
```

### Example Output:
```
$ git log --oneline develop
e5f6g7h (develop) Merge branch 'feature/api-docs'
d4e5f6g Merge branch 'feature/error-handling'
c3d4e5f Merge branch 'feature/logging-system'
b2c3d4e Merge branch 'feature/cache-optimization'
a1b2c3d Initial commit
```

### Explanation:
Multiple features can be worked on in parallel. Merging one doesn't block others.

---

## Exercise 8: Merge Strategies and Rebase Workflow - Solution

### Commands:
```bash
# Create scenario
git switch develop
echo "develop change 1" > file1.txt
git add file1.txt
git commit -m "Develop change 1"

git switch -c feature/rebase-demo
echo "feature 1" > feature1.txt
git add feature1.txt
git commit -m "Feature commit 1"
echo "feature 2" > feature2.txt
git add feature2.txt
git commit -m "Feature commit 2"
echo "feature 3" > feature3.txt
git add feature3.txt
git commit -m "Feature commit 3"

git switch develop
echo "develop change 2" > file2.txt
git add file2.txt
git commit -m "Develop change 2"

# Method A: Merge without rebase
git switch feature/rebase-demo
git log --oneline
git switch develop
git merge --no-ff feature/rebase-demo
git log --oneline

# Method B: Rebase then merge (on a copy)
git reset --hard HEAD~1  # Undo previous merge
git switch feature/rebase-demo
git rebase develop
git switch develop
git merge --ff feature/rebase-demo
git log --oneline
```

### Example Output:
```
# Without rebase:
$ git log --oneline develop
a1b2c3d (main) Merge branch 'feature/rebase-demo'
b2c3d4e Develop change 2
c3d4e5f Develop change 1
d4e5f6g Feature commit 3
e5f6g7h Feature commit 2
f6g7h8i Feature commit 1

# With rebase:
$ git log --oneline develop
f6g7h8i (main) Feature commit 3
e5f6g7h Feature commit 2
d4e5f6g Feature commit 1
c3d4e5f Develop change 2
b2c3d4e Develop change 1
```

### Explanation:
Merge creates merge commits (preserves history). Rebase creates linear history (cleaner but rewrites history).

---

## Exercise 9: Feature Toggle / Feature Flags Workflow - Solution

### Commands:
```bash
# Create feature branch
git switch -c feature/new-payment-system

# Implement new payment system
echo """
def process_payment(amount):
    if os.getenv('USE_NEW_PAYMENT') == 'true':
        return new_payment_system(amount)
    else:
        return old_payment_system(amount)
""" > payment.py

git add payment.py
git commit -m "Add new payment system (disabled by default)"

# Merge to main (feature is disabled)
git switch main
git merge feature/new-payment-system

# Test with feature enabled
export USE_NEW_PAYMENT=true
# Test new payment system

# Test with feature disabled
export USE_NEW_PAYMENT=false
# Test old payment system

# Once fully tested, remove flag
git switch -c feature/cleanup-payment-flag
echo """
def process_payment(amount):
    return new_payment_system(amount)  # Removed flag
""" > payment.py
git add payment.py
git commit -m "Remove feature flag, use new payment system"
git switch main
git merge feature/cleanup-payment-flag

# Verify
git log --oneline main
```

### Example Output:
```
$ git log --oneline main
c3d4e5f Remove feature flag, use new payment system
b2c3d4e Add new payment system (disabled by default)
a1b2c3d Initial commit
```

### Explanation:
Feature flags allow merging incomplete features. Enables testing without branching.

---

## Exercise 10: Versioning Strategy with Tags - Solution

### Commands:
```bash
# Create version v1.0.0
git switch main
echo "v1.0.0" > VERSION
git add VERSION
git commit -m "Release v1.0.0"
git tag v1.0.0

# Create patch release v1.0.1
echo "v1.0.1" > VERSION
git add VERSION
git commit -m "Release v1.0.1"
git tag v1.0.1

# Create minor release v1.1.0
echo "v1.1.0" > VERSION
git add VERSION
git commit -m "Release v1.1.0"
git tag v1.1.0

# Create major release v2.0.0
echo "v2.0.0" > VERSION
git add VERSION
git commit -m "Release v2.0.0"
git tag v2.0.0

# List tags
git tag
git tag -l

# Show details of a tag
git show v1.0.0

# Compare versions
git log v1.0.0..v1.1.0 --oneline

# Check current version
cat VERSION
```

### Example Output:
```
$ git tag
v1.0.0
v1.0.1
v1.1.0
v2.0.0

$ git show v1.0.0
commit a1b2c3d
Author: Your Name
Date:   Mon Jan 15 12:00:00 2026 +0000

    Release v1.0.0

$ git log v1.0.0..v1.1.0 --oneline
c3d4e5f Release v1.1.0
b2c3d4e Release v1.0.1
```

### Explanation:
Semantic versioning: MAJOR.MINOR.PATCH. Tags mark stable releases. Easy to track version history and refer to specific versions.

