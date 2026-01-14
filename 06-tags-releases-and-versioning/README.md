# 06-tags-releases-and-versioning

## What You'll Learn

By the end of this module, you'll understand:
- Difference between lightweight and annotated tags
- How to create and manage tags
- Creating GitHub releases
- Semantic versioning
- Version numbering schemes
- Release notes best practices
- Managing multiple versions

## Prerequisites

- Completion of Modules 01-05
- Understanding of workflows
- Comfortable with GitHub

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Lightweight Tag** | Simple reference to commit |
| **Annotated Tag** | Full object with metadata |
| **Release** | Tagged version with release notes |
| **Semantic Versioning** | MAJOR.MINOR.PATCH (e.g., 1.2.3) |
| **Changelog** | Record of changes per version |
| **Release Notes** | Description of what changed |
| **Pre-release** | Alpha, beta, rc versions |
| **Version Constraint** | What versions package supports |

## Hands-on Lab: Creating Tags and Releases

### Scenario
You've completed development and want to create a proper release version with documentation.

### Step-by-Step Commands

```bash
# Step 1: Update version file
echo "version = 1.0.0" > VERSION
git add VERSION
git commit -m "Bump version to 1.0.0"

# Step 2: Create lightweight tag
git tag v1.0.0

# Step 3: Create annotated tag (preferred)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Step 4: View tag details
git show v1.0.0

# Step 5: Push tags to remote
git push origin v1.0.0

# Step 6: List all tags
git tag -l

# Step 7: Create next version
echo "version = 1.1.0-dev" > VERSION
git add VERSION
git commit -m "Start development for 1.1.0"

# Step 8: View tags in log
git log --oneline --decorate

# Step 9: Create GitHub release
# Go to GitHub > Releases > Create new release
# Tag: v1.0.0
# Title: Release 1.0.0
# Description: Release notes here
```

### Expected Output

```
tag v1.0.0
tagger Name <email>
date Tue Jan 15 10:00:00 2026 +0000

Release version 1.0.0

commit abc1234567...
```

## Validation

You've successfully completed this lab if:
- ✓ Created lightweight tag
- ✓ Created annotated tag
- ✓ Viewed tag information
- ✓ Pushed tags to remote
- ✓ Listed tags in log
- ✓ Understood version numbering

## Cleanup

```bash
git tag -d v1.0.0
rm -f VERSION
git add .
git commit -m "Cleanup: Remove test files"
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Using lightweight tags everywhere | Loses metadata | Use annotated tags for releases |
| Not pushing tags | Tags only local | `git push origin --tags` |
| Inconsistent version format | Version chaos | Standardize on semantic versioning |
| Releasing without notes | Users don't know what changed | Document all changes |
| Wrong version numbers | Breaking versions | Follow semantic versioning strictly |

## Troubleshooting

**Q: What's the difference between lightweight and annotated tags?**
- A: Annotated has metadata (author, date, message). Use for releases. Lightweight for quick references

**Q: How do I delete a tag?**
- A: `git tag -d tagname` locally, `git push origin --delete tagname` remotely

**Q: What version number should I use?**
- A: Semantic versioning: MAJOR.MINOR.PATCH. Increment MAJOR for breaking changes, MINOR for features, PATCH for bugs

**Q: How do I support multiple versions?**
- A: Maintain release branches for old versions, create tags, document support timeline

**Q: Can I add release notes after tagging?**
- A: Yes! Create GitHub release pointing to existing tag, add release notes there

## Next Steps

Once comfortable with:
- Creating tags
- Managing releases
- Semantic versioning
- Release documentation

Move to **Module 07: GitHub Pull Requests and Code Review** to master the review process.

---

**Time to Complete:** 40 minutes  
**Difficulty Level:** Beginner-Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
