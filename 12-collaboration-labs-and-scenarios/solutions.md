# 12-collaboration-labs-and-scenarios: Solutions

## Solution 1: Simulated Team Collaboration

**Setup:**
```bash
# Person A
git checkout -b feature/auth
# Make changes to auth system
git add .
git commit -m "Add authentication system"
git push origin feature/auth
# Create PR on GitHub
```

**Person B (simultaneously):**
```bash
git checkout -b feature/database
# Make changes to database
git add .
git commit -m "Add database layer"
git push origin feature/database
# Create PR on GitHub
```

**Both:**
1. Review each other's PR
2. Approve both PRs
3. Merge both (no conflicts since different files)
4. Main branch now has both features

---

## Solution 2: Conflict Resolution Scenario

**Person A:**
```bash
git checkout develop
git checkout -b feature/userdb
# Edit: Change "name" field type to UUID
git add users.py && git commit -m "Change name to UUID"
git push origin feature/userdb
```

**Person B (simultaneously):**
```bash
git checkout develop
git checkout -b feature/newfields
# Edit: Add new name validation
git add users.py && git commit -m "Add name validation"
git push origin feature/newfields
```

**Resolution:**
```bash
# Person A merges first - no problem
git merge feature/userdb

# Person B tries to merge - CONFLICT!
git merge feature/newfields
# CONFLICT: both modified users.py

# Manual resolution in editor
# Keep: UUID change + validation
# Remove: conflicting markers

git add users.py
git commit -m "Resolve conflict: UUID + validation"
git push origin feature/newfields
```

---

## Solution 3: Code Review Process

**Step 1: Create PR (Person A)**
```bash
git checkout -b feature/api-endpoint
# Create new API endpoint
git add .
git commit -m "Add user endpoint"
git push origin feature/api-endpoint
# Create PR with description
```

**Step 2: Review (Person B)**
```markdown
# PR Review Comments:
1. Missing error handling for invalid user IDs
2. No input validation for request parameters
3. Consider adding rate limiting
4. Add API documentation
```

**Step 3: Update Code (Person A)**
```bash
# Make requested changes
# Add error handling
# Add validation
# Add documentation

git add .
git commit -m "Address review feedback"
git push origin feature/api-endpoint
# Person B's comments dismissed, requests re-review
```

**Step 4: Approve (Person B)**
```
✓ Approved - Changes look good!
```

**Step 5: Merge (Person A)**
```bash
# Click merge button on GitHub
# PR merged to main
```

---

## Solution 4: CI/CD Pipeline in Team

**Workflow File: .github/workflows/ci.yml**
```yaml
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npm test
      - run: npm run lint

  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm audit
```

**Branch Protection:**
```
Settings > Branches > main > Add rule
✓ Require status checks to pass
  - Select: test workflow
  - Select: security workflow
✓ Require branches to be up to date
```

**Team Experience:**
- PR created
- Checks run automatically
- Green checkmark = PR can merge
- Red X = must fix tests first
- Only passing PRs merged

---

## Solution 5: Git Flow Implementation

**Branch Strategy:**
```
main (production-ready)
├─ v1.0.0 (tag)
└─ v1.1.0 (tag)

develop (next release)
├─ feature/auth
├─ feature/database
└─ feature/api

release/1.2.0 (release preparation)
hotfix/1.0.1 (urgent production fix)
```

**Workflow:**
```bash
# New feature
git checkout develop
git checkout -b feature/auth
# Make changes
git push origin feature/auth
# Create PR to develop

# Release preparation
git checkout -b release/1.2.0 origin/develop
# Only bug fixes
git push origin release/1.2.0
# When ready:
git checkout main
git merge release/1.2.0
git tag v1.2.0

# Hotfix for production bug
git checkout -b hotfix/1.0.1 origin/main
# Fix bug
git push origin hotfix/1.0.1
# Merge to main and develop
```

---

## Solution 6: Managing Multiple Releases

**Multiple Version Support:**
```
main (2.0 - stable)
release/2.1 (upcoming)
release/1.9 (previous)
release/1.8 (legacy)
```

**Backporting Fixes:**
```bash
# Found critical bug in 2.0
git checkout -b fix/critical origin/main
# Fix bug
git push origin fix/critical
# Merge to main (merged)

# Backport to 1.9
git checkout -b fix/critical-1.9 origin/release/1.9
# Cherry-pick or manually apply same fix
git cherry-pick <commit-hash>
git push origin fix/critical-1.9
# Merge to release/1.9 (merged)
```

**Version Timeline:**
```
2.1 - In development
2.0 - Current stable (security fixes only)
1.9 - Extended support (critical fixes only)
1.8 - EOL (no support)
```

---

## Solution 7: Documentation

**CONTRIBUTING.md:**
```markdown
# Contributing

## Getting Started
1. Fork repository
2. Create feature branch
3. Make changes
4. Submit PR

## Code Style
- Follow ESLint rules
- Write tests for features
- Document public APIs

## Review Process
- Code review required
- All tests must pass
- 2+ approvals for merge

## Release Cycle
- Features: develop branch
- Releases: release/ branch
- Hotfixes: main branch
```

**DEVELOPMENT.md:**
```markdown
# Development Guide

## Setup
```bash
git clone repo
npm install
npm run dev
```

## Architecture
- Frontend: React
- Backend: Node.js
- Database: PostgreSQL

## Testing
```bash
npm test          # Run tests
npm run coverage  # Coverage report
```

## Debugging
- Use VSCode debugger
- Node debugging: `node --inspect`
```

---

## Solution 8: Large Feature Development

**Plan:**
```
Large Feature: User Management System
├─ Subtask 1: Database schema (Ali)
├─ Subtask 2: API endpoints (Bob)
├─ Subtask 3: Frontend UI (Carol)
├─ Subtask 4: Authentication (Dan)
└─ Subtask 5: Testing & integration (Eve)
```

**Implementation:**
```bash
# Main feature branch
git checkout -b feature/user-management

# Ali creates sub-branch
git checkout -b feature/user-management/database
# ... work ...
# Merge to main feature branch

# Bob creates sub-branch
git checkout -b feature/user-management/api
# ... work ...
# Merge to main feature branch

# Final integration PR from feature/user-management to develop
```

---

## Solution 9: Emergency Hotfix Process

**Issue:** Production bug found on main branch

```bash
# Fast track
git checkout -b hotfix/critical-bug origin/main
# Fix the issue
git add .
git commit -m "HOTFIX: Fix critical bug"
git push origin hotfix/critical-bug

# Skip normal review for critical
# Fast-track approval
git checkout main
git merge hotfix/critical-bug
git tag v1.0.1
git push origin main v1.0.1

# Deploy immediately
# Then merge to develop to keep in sync
git checkout develop
git merge main
git push origin develop
```

---

## Solution 10: Retrospective Improvements

**Retrospective Notes:**
```markdown
## What Went Well
✓ Fast PR reviews (average 2 hours)
✓ Clear documentation helped new members
✓ CI/CD caught most bugs
✓ Good communication in PRs

## Pain Points
✗ Feature branches got stale (3+ days)
✗ Merge conflicts in frequently-changed files
✗ Long-running builds (20 minutes)
✗ Unclear priority for PRs

## Improvements
- Merge to develop daily (avoid staleness)
- Monitor build time, parallelize tests
- Create priority labels (urgent, normal, backlog)
- Pair programming for complex features
```

**Process Improvements Applied:**
1. Daily syncs for open PRs
2. Build time reduced to 5 minutes
3. Priority labels added
4. Pairing guidelines documented
