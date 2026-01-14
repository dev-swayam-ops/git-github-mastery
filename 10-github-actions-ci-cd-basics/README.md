# 10-github-actions-ci-cd-basics

## What You'll Learn

By the end of this module, you'll understand:
- GitHub Actions workflow structure
- Triggers (push, pull request, schedule)
- Jobs and steps
- Actions marketplace
- Environment variables and secrets
- Building and testing CI/CD
- Deploying applications

## Prerequisites

- Completion of Modules 01-09
- Basic understanding of YAML
- Git/GitHub workflow knowledge
- Some programming experience

## Key Concepts

| Component | Purpose | Example |
|-----------|---------|----------|
| **Workflow** | Automated process | Build and test on push |
| **Trigger** | When to run | on: push, on: pull_request |
| **Job** | Task in workflow | Test suite, Deploy app |
| **Step** | Command in job | run: npm test |
| **Action** | Reusable workflow | actions/checkout@v3 |
| **Secret** | Secure variable | API keys, tokens |
| **Artifact** | Build output | Test reports, binaries |

## Hands-on Lab: Creating Your First CI/CD Workflow

### Scenario
You want to automatically run tests and build on every push and PR.

### Step-by-Step Commands

```bash
# Step 1: Create workflow directory
git clone <repo>
cd <repo>
mkdir -p .github/workflows

# Step 2: Create workflow file
cat > .github/workflows/ci.yml << 'EOF'
name: CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    
    - name: Lint with flake8
      run: flake8 src/
    
    - name: Run tests
      run: pytest tests/
    
    - name: Upload coverage
      uses: codecov/codecov-action@v3
EOF

# Step 3: Create requirements.txt
echo "pytest==7.2.0" > requirements.txt
echo "flake8==5.0.4" >> requirements.txt

# Step 4: Create test file
mkdir -p tests
echo "def test_example(): assert True" > tests/test_example.py

# Step 5: Create source
mkdir -p src
echo "print('Hello')" > src/main.py

# Step 6: Commit and push
git add .
git commit -m "Add CI workflow"
git push origin main

# Step 7: View workflow
# GitHub > Actions > CI workflow running

# Step 8: Add secrets (if needed)
# Settings > Secrets > New Repository Secret
# Name: API_KEY
# Value: your-secret-key

# Step 9: Use secret in workflow
cat > .github/workflows/deploy.yml << 'EOF'
name: Deploy

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Deploy
      env:
        API_KEY: ${{ secrets.API_KEY }}
      run: echo "Deploying with $API_KEY"
EOF

# Step 10: Push and watch workflow
git add .github/workflows/deploy.yml
git commit -m "Add deploy workflow"
git push origin main
```

### Expected Output

```
CI workflow started
✓ Set up Python
✓ Install dependencies
✓ Lint with flake8
✓ Run tests
✓ All checks passed
```

## Validation

You've successfully completed this lab if:
- ✓ Created workflow file
- ✓ Set up CI triggers
- ✓ Configured test job
- ✓ Ran tests successfully
- ✓ Handled secrets securely
- ✓ Viewed workflow results in GitHub

## Cleanup

```bash
rm -f requirements.txt
rm -rf tests src
rm -f .github/workflows/ci.yml
git add .
git commit -m "Cleanup: Remove test files"
git push origin main
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Committing secrets | Exposed credentials | Use GitHub secrets |
| Large test artifacts | Slow downloads | Keep artifacts minimal |
| No caching | Slow builds | Cache dependencies |
| Wrong triggers | Runs at wrong time | Use correct: on: clauses |
| Timeout errors | Workflow hangs | Set timeout-minutes |

## Troubleshooting

**Q: How do I view workflow results?**
- A: GitHub > Actions > Select workflow > View logs

**Q: How do I pass secrets to workflow?**
- A: Settings > Secrets > Add secret, then use ${{ secrets.NAME }}

**Q: Can I run workflows locally?**
- A: Yes! Use `act` tool: https://github.com/nektos/act

**Q: What's the maximum workflow duration?**
- A: 6 hours per job. Most should be < 30 minutes

**Q: How do I trigger workflow manually?**
- A: Add `workflow_dispatch` to `on:` section, then GitHub > Actions > Run workflow

## Next Steps

Once comfortable with:
- Creating workflows
- Setting up CI/CD
- Using GitHub Actions
- Handling secrets

Move to **Module 11: GitHub Security Features** to secure your repositories.

---

**Time to Complete:** 60 minutes  
**Difficulty Level:** Intermediate-Advanced  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
