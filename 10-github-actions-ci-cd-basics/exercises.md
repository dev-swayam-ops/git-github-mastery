# 10-github-actions-ci-cd-basics: Exercises

## Exercise 1: Create Your First Workflow
**Difficulty:** Easy

Create a simple GitHub Actions workflow that runs on push.

**Instructions:**
1. Create `.github/workflows/` directory
2. Create `hello.yml` file
3. Add basic workflow (echo "Hello World")
4. Push to repository
5. View Actions tab to see run

**Expected Outcome:** Workflow executes and completes successfully

---

## Exercise 2: Understand Workflow Triggers
**Difficulty:** Easy

Learn different ways to trigger workflows.

**Instructions:**
1. Create workflow triggered on `push`
2. Create workflow triggered on `pull_request`
3. Create workflow triggered on `schedule`
4. Test each trigger type
5. View run history in Actions tab

**Expected Outcome:** Understand trigger types and when each runs

---

## Exercise 3: Add Environment Variables
**Difficulty:** Medium

Use environment variables in workflows.

**Instructions:**
1. Define `env` section in workflow
2. Reference variables in steps
3. Use `secrets` for sensitive data
4. Test variable substitution
5. Verify variables in log output

**Expected Outcome:** Variables correctly substituted in workflow

---

## Exercise 4: Run Tests in Workflow
**Difficulty:** Medium

Set up a workflow that runs tests.

**Instructions:**
1. Create simple test file
2. Set up Node/Python environment
3. Install dependencies
4. Run tests
5. Verify pass/fail status reported

**Expected Outcome:** Tests run and results visible in Actions

---

## Exercise 5: Use GitHub Actions Marketplace
**Difficulty:** Medium

Add a pre-built action to your workflow.

**Instructions:**
1. Find action on GitHub Marketplace
2. Add action to workflow (e.g., checkout, setup)
3. Configure action parameters
4. Run workflow
5. Verify action worked

**Expected Outcome:** Marketplace action integrated successfully

---

## Exercise 6: Create Matrix Strategy
**Difficulty:** Medium

Run workflow across multiple environments.

**Instructions:**
1. Create workflow with matrix strategy
2. Test on Node 14, 16, 18
3. Test on Ubuntu, macOS, Windows
4. View parallel job execution
5. Understand matrix advantages

**Expected Outcome:** Workflow runs on all matrix combinations

---

## Exercise 7: Configure Secrets
**Difficulty:** Medium

Use repository secrets for sensitive data.

**Instructions:**
1. Go to Settings > Secrets and variables
2. Add repository secret
3. Reference secret in workflow
4. Verify secret doesn't print in logs
5. Test secret usage

**Expected Outcome:** Secrets safely used in workflows

---

## Exercise 8: Deploy with Workflow
**Difficulty:** Medium

Create a simple deployment workflow.

**Instructions:**
1. Create deploy workflow
2. Add build step
3. Add deployment step (to test environment)
4. Run workflow
5. Verify deployment successful

**Expected Outcome:** Workflow successfully deploys artifact

---

## Exercise 9: Use Artifacts
**Difficulty:** Medium

Generate and download artifacts from workflow.

**Instructions:**
1. Create artifact in workflow
2. Upload artifact using upload-artifact action
3. View artifact in Actions tab
4. Download artifact
5. Understand artifact use cases

**Expected Outcome:** Artifacts created, uploaded, downloaded

---

## Exercise 10: Create Complex Pipeline
**Difficulty:** Medium

Build multi-job workflow with dependencies.

**Instructions:**
1. Create build job
2. Create test job (depends on build)
3. Create deploy job (depends on test)
4. Run pipeline
5. View job graph showing dependencies

**Expected Outcome:** Multi-job pipeline executes in correct order

---

## Summary

| Exercise | Topic | Difficulty |
|----------|-------|-----------|
| 1 | First Workflow | Easy |
| 2 | Triggers | Easy |
| 3 | Variables | Medium |
| 4 | Testing | Medium |
| 5 | Marketplace | Medium |
| 6 | Matrix | Medium |
| 7 | Secrets | Medium |
| 8 | Deployment | Medium |
| 9 | Artifacts | Medium |
| 10 | Complex Pipeline | Medium |
