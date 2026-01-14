# 10-github-actions-ci-cd-basics: Cheatsheet

## Workflow File Structure

```yaml
name: Workflow Name

on: [push, pull_request]  # Triggers

env:                       # Environment variables
  VERSION: 1.0.0

jobs:
  job-name:               # Job definition
    runs-on: ubuntu-latest
    steps:
      - uses: action/name  # Use action
        with:
          param: value
      - run: command      # Run command
      - name: Step name
        run: npm test
```

## Common Triggers

| Trigger | Runs | Use |
|---------|------|-----|
| `on: push` | On any push | Tests |
| `on: pull_request` | On PR open/update | Validation |
| `on: release` | On release created | Deploy |
| `on: schedule` | On cron schedule | Cleanup, backups |
| `on: workflow_dispatch` | Manual trigger | On-demand jobs |

## Runners (runs-on)

| Runner | OS | Use |
|--------|----|----|
| `ubuntu-latest` | Linux | Most common |
| `macos-latest` | macOS | iOS/macOS builds |
| `windows-latest` | Windows | Windows builds |
| `self-hosted` | Any | Custom machine |

## Common Actions

| Action | Purpose | Usage |
|--------|---------|-------|
| `actions/checkout` | Clone repository | Always first step |
| `actions/setup-node` | Setup Node.js | Node projects |
| `actions/setup-python` | Setup Python | Python projects |
| `actions/setup-go` | Setup Go | Go projects |
| `actions/upload-artifact` | Save files | Store build outputs |
| `actions/download-artifact` | Get files | Use outputs from build |
| `actions/cache` | Cache dependencies | Speed up builds |

## Using Actions from Marketplace

```yaml
- uses: owner/repo@version
  with:
    param: value
```

Example:
```yaml
- uses: actions/setup-node@v3
  with:
    node-version: '18'
    cache: 'npm'
```

## Variables & Secrets

| Type | Scope | Usage |
|------|-------|-------|
| `env.VAR_NAME` | Workflow level | Public values |
| `secrets.SECRET_NAME` | Repository secret | Sensitive values |
| `matrix.property` | Matrix strategy | In matrix jobs |
| `github.ref` | Git reference | Current branch/tag |

## Matrix Strategy

```yaml
strategy:
  matrix:
    node-version: [14, 16, 18]
    os: [ubuntu-latest, windows-latest]
```

Creates: 3 × 2 = 6 job combinations

## Job Dependencies

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: npm run build

  test:
    needs: build           # Wait for build
    runs-on: ubuntu-latest
    steps:
      - run: npm test

  deploy:
    needs: [build, test]   # Wait for both
    runs-on: ubuntu-latest
    steps:
      - run: npm run deploy
```

## Conditional Execution

```yaml
- name: Deploy
  if: github.ref == 'refs/heads/main'
  run: deploy.sh

- name: PR comment
  if: github.event_name == 'pull_request'
  run: comment.sh

- name: On failure
  if: failure()
  run: notify.sh
```

## Secrets Configuration

```bash
# Add secret via CLI
gh secret set SECRET_NAME --body "secret_value"

# Delete secret
gh secret delete SECRET_NAME

# List secrets
gh secret list
```

## Upload & Download Artifacts

```yaml
# Upload
- uses: actions/upload-artifact@v3
  with:
    name: my-artifact
    path: dist/

# Download
- uses: actions/download-artifact@v3
  with:
    name: my-artifact
    path: ./download/
```

## Cache Dependencies

```yaml
- uses: actions/cache@v3
  with:
    path: node_modules
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-npm-
```

## Workflow Status Badges

Add to README.md:
```markdown
![Tests](https://github.com/owner/repo/workflows/Test/badge.svg)
[![Build Status](https://github.com/owner/repo/actions/workflows/ci.yml/badge.svg)](https://github.com/owner/repo/actions)
```

## Useful Context Variables

| Variable | Value |
|----------|-------|
| `${{ github.repository }}` | owner/repo |
| `${{ github.ref }}` | Full ref (refs/heads/main) |
| `${{ github.sha }}` | Commit SHA |
| `${{ github.event_name }}` | Trigger type (push, pull_request) |
| `${{ runner.os }}` | ubuntu-latest, windows-latest, etc. |

## Debugging Workflows

```yaml
# Enable debug logging
env:
  RUNNER_DEBUG: 1

# Print variables
- run: |
    echo "Repository: ${{ github.repository }}"
    echo "Branch: ${{ github.ref }}"
    echo "Event: ${{ github.event_name }}"
```

## Common Workflow Patterns

### Node.js CI
```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm test
```

### Python CI
```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
          cache: 'pip'
      - run: pip install -r requirements.txt
      - run: pytest
```

### Deploy to Production
```yaml
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci && npm run build
      - run: deploy.sh
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
          SERVER: ${{ secrets.SERVER }}
```

## Performance Tips

- Use `actions/cache` for dependencies
- Use `actions/setup-*` with `cache` parameter
- Use `npm ci` instead of `npm install`
- Run tests in parallel with matrix
- Cache Docker layers
- Use `actions/checkout@v3` with `ref` to specify version

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Action not found | Check action version, use @vX format |
| Secret not working | Ensure secret added to repo, use ${{ secrets.NAME }} |
| Build too slow | Use caching, parallelize jobs |
| Matrix explosion | Limit combinations, use excludes |
| Permissions error | Check token, use GITHUB_TOKEN |
