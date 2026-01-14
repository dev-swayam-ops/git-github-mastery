# 10-github-actions-ci-cd-basics: Solutions

## Solution 1: Create Your First Workflow

**File: `.github/workflows/hello.yml`**
```yaml
name: Hello World

on: [push]

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - name: Print hello
        run: echo "Hello World from GitHub Actions!"
```

**Result:** Workflow runs on every push, prints message to logs

---

## Solution 2: Understand Workflow Triggers

```yaml
# Trigger on push
on: push

# Trigger on pull request
on: pull_request

# Trigger on schedule (cron)
on:
  schedule:
    - cron: '0 9 * * *'  # Daily at 9 AM

# Multiple triggers
on: [push, pull_request]

# Conditional
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
```

---

## Solution 3: Add Environment Variables

```yaml
name: With Variables

on: push

env:
  APP_ENV: production
  VERSION: 1.0.0

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Print variables
        run: |
          echo "App: ${{ env.APP_ENV }}"
          echo "Version: ${{ env.VERSION }}"
      - name: Use secret
        run: echo "Secret: ${{ secrets.API_KEY }}"
```

---

## Solution 4: Run Tests in Workflow

```yaml
name: Test Suite

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm install
      
      - name: Run tests
        run: npm test
      
      - name: Generate coverage
        run: npm run coverage
```

---

## Solution 5: Use GitHub Actions Marketplace

```yaml
name: Using Marketplace Action

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Build
        run: npm run build
```

---

## Solution 6: Create Matrix Strategy

```yaml
name: Matrix Test

on: push

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        node-version: [14, 16, 18]
        os: [ubuntu-latest, macos-latest, windows-latest]
    
    steps:
      - uses: actions/checkout@v3
      
      - uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      
      - run: npm install
      - run: npm test
```

**Result:** 9 jobs total (3 node versions × 3 OS combinations)

---

## Solution 7: Configure Secrets

**GitHub UI:**
```
Settings > Secrets and variables > Actions > New repository secret

Name: API_KEY
Value: your-secret-value
```

**In Workflow:**
```yaml
name: Using Secrets

on: push

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        run: |
          curl -X POST \
            -H "Authorization: Bearer ${{ secrets.API_KEY }}" \
            https://api.example.com/deploy
```

**Security:** Secrets never printed in logs (masked automatically)

---

## Solution 8: Deploy with Workflow

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build
        run: npm run build
      
      - name: Deploy to server
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
          SERVER_URL: ${{ secrets.SERVER_URL }}
        run: |
          echo "$DEPLOY_KEY" > deploy.key
          chmod 600 deploy.key
          ssh -i deploy.key user@$SERVER_URL "cd /app && git pull && npm run start"
```

---

## Solution 9: Use Artifacts

```yaml
name: Build and Upload Artifact

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build
        run: |
          mkdir dist
          echo "app content" > dist/app.js
      
      - name: Upload artifact
        uses: actions/upload-artifact@v3
        with:
          name: dist-files
          path: dist/

  download:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Download artifact
        uses: actions/download-artifact@v3
        with:
          name: dist-files
      
      - name: Use artifact
        run: ls -la && cat app.js
```

---

## Solution 10: Create Complex Pipeline

```yaml
name: Complete Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install && npm run build
      - uses: actions/upload-artifact@v3
        with:
          name: build
          path: dist/

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/download-artifact@v3
      - run: npm install && npm test

  security:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm audit

  deploy:
    needs: [test, security]
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/download-artifact@v3
      - run: |
          echo "Deploying to production..."
          # Actual deploy commands here
```

**Pipeline Order:**
1. Build runs first
2. Test and Security run in parallel (after build)
3. Deploy runs last (only if test & security pass)

---

## Key Workflow Concepts

| Concept | Purpose |
|---------|---------|
| Trigger | When workflow runs (push, PR, schedule) |
| Job | Unit of work in workflow |
| Step | Individual command in job |
| Action | Reusable workflow component |
| Artifact | Output files from workflow |
| Secret | Sensitive data (passwords, tokens) |
| Variable | Reusable values in workflow |
| Matrix | Run across multiple configurations |

---

## Common Workflow Patterns

### Simple Test Workflow
```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install && npm test
```

### Deploy on Main
```yaml
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: deploy.sh
```

### Scheduled Task
```yaml
on:
  schedule:
    - cron: '0 * * * *'  # Hourly
jobs:
  cleanup:
    runs-on: ubuntu-latest
    steps:
      - run: cleanup-script.sh
```
