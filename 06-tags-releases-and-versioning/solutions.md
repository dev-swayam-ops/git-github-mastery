# Tags, Releases, and Versioning - Solutions

## Exercise 1: Create Lightweight Tags - Solution

### Commands:
```bash
# Make commits
echo "Feature 1" > feature1.txt
git add feature1.txt
git commit -m "Add feature 1"

echo "Feature 2" > feature2.txt
git add feature2.txt
git commit -m "Add feature 2"

# Create lightweight tag on current commit
git tag v1.0.0

# Get hash of first commit
FIRST=$(git rev-list --all | tail -1)

# Create tag on previous commit
git tag v1.0.1 $FIRST

# List all tags
git tag
git tag -l

# Switch to a tag
git switch v1.0.0

# View tags storage
ls -la .git/refs/tags/
cat .git/refs/tags/v1.0.0
```

### Example Output:
```
$ git tag
v1.0.0
v1.0.1

$ git switch v1.0.0
Note: checking out 'v1.0.0'.
You are in 'detached HEAD' state.

$ cat .git/refs/tags/v1.0.0
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
```

### Explanation:
Lightweight tags are just references to commits, stored as simple files in `.git/refs/tags/`. No metadata, just the commit hash.

---

## Exercise 2: Create Annotated Tags - Solution

### Commands:
```bash
# Make a commit
echo "Release" > release.txt
git add release.txt
git commit -m "Prepare v1.0.0 release"

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Create another annotated tag
git tag -a v1.1.0 -m "Release version 1.1.0 with new features"

# List tags
git tag -l

# View tag details
git show v1.0.0
git show v1.1.0

# Compare with lightweight tag
git tag v1.0.0-light
git show v1.0.0-light

# Create tag with multiline message
git tag -a v2.0.0 -m "Version 2.0.0 Release

Major changes:
- Breaking API changes
- New authentication system
- Performance improvements"

git show v2.0.0
```

### Example Output:
```
$ git show v1.0.0
tag v1.0.0
Tagger: Your Name <your@email.com>
Date:   Mon Jan 15 12:00:00 2026 +0000

Release version 1.0.0

commit a1b2c3d
Author: Your Name <your@email.com>
Date:   Mon Jan 15 11:59:00 2026 +0000

    Prepare v1.0.0 release

$ git tag -l
v1.0.0
v1.0.0-light
v1.1.0
v2.0.0
```

### Explanation:
Annotated tags are full objects with tagger information, date, and message. Better for releases as they provide more metadata.

---

## Exercise 3: Delete and Rename Tags - Solution

### Commands:
```bash
# Create wrong tag
git tag v1.0.0-wrong

# Delete it
git tag -d v1.0.0-wrong

# Create correct tag
git tag v1.0.0-beta

# Create another wrong tag
git tag wrong-tag-name

# Rename by deleting old and creating new
git tag correct-tag-name wrong-tag-name
git tag -d wrong-tag-name

# Verify
git tag -l
git tag -l | grep correct

# Try to delete non-existent tag
git tag -d non-existent
```

### Example Output:
```
$ git tag -d v1.0.0-wrong
Deleted tag 'v1.0.0-wrong' (was abc1234)

$ git tag correct-tag-name wrong-tag-name
$ git tag -d wrong-tag-name
Deleted tag 'wrong-tag-name' (was abc1234)

$ git tag -l
correct-tag-name
v1.0.0-beta

$ git tag -d non-existent
error: tag 'non-existent' not found.
```

### Explanation:
Delete tags with `-d` flag. Rename by creating new tag with old tag's target, then delete old tag.

---

## Exercise 4: Create Release Branches from Tags - Solution

### Commands:
```bash
# Create releases
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Release v1.0.0"
git tag v1.0.0

echo "v1.1.0" > version.txt
git add version.txt
git commit -m "Release v1.1.0"
git tag v1.1.0

echo "v2.0.0" > version.txt
git add version.txt
git commit -m "Release v2.0.0"
git tag v2.0.0

# Create maintenance branch from v1.1.0
git switch -c release/1.1.x v1.1.0

# Make patch commit
echo "v1.1.1" > version.txt
git add version.txt
git commit -m "Release v1.1.1 - patch"
git tag v1.1.1

# Verify branching
git log --oneline main
git log --oneline release/1.1.x

# Merge patch back to main if desired
git switch main
git merge release/1.1.x
```

### Example Output:
```
$ git switch -c release/1.1.x v1.1.0
Switched to a new branch 'release/1.1.x'

$ git commit -m "Release v1.1.1 - patch"
[release/1.1.x b2c3d4e] Release v1.1.1 - patch

$ git log --oneline main
d4e5f6g v2.0.0
c3d4e5f v1.1.0
b2c3d4e v1.0.0

$ git log --oneline release/1.1.x
e5f6g7h v1.1.1
c3d4e5f v1.1.0
```

### Explanation:
Create maintenance branches from tags for ongoing support of released versions. Allows backport fixes while main evolves.

---

## Exercise 5: Semantic Versioning Progression - Solution

### Commands:
```bash
# v1.0.0 - Initial release
echo "Core functionality" > core.txt
git add core.txt
git commit -m "v1.0.0 - Initial release"
git tag v1.0.0

# v1.1.0 - New feature (backward compatible)
echo "Feature A" > featureA.txt
git add featureA.txt
git commit -m "Add feature A"
git tag v1.1.0

# v1.2.0 - Another feature
echo "Feature B" > featureB.txt
git add featureB.txt
git commit -m "Add feature B"
git tag v1.2.0

# v1.2.1 - Bug fix
git commit --allow-empty -m "Bug fix in feature"
git tag v1.2.1

# v1.2.2 - Security patch
git commit --allow-empty -m "Security patch"
git tag v1.2.2

# v2.0.0 - Breaking changes
echo "New API structure" > api.txt
git add api.txt
git commit -m "v2.0.0 - Breaking API changes"
git tag v2.0.0

# v2.1.0 - Feature
git commit --allow-empty -m "Add feature to v2"
git tag v2.1.0

# Show progression
git tag -l | sort -V
git log --oneline main | head -10

# Show changes between versions
git log v1.0.0..v1.2.0 --oneline
```

### Example Output:
```
$ git tag -l | sort -V
v1.0.0
v1.1.0
v1.2.0
v1.2.1
v1.2.2
v2.0.0
v2.1.0

$ git log v1.0.0..v1.2.0 --oneline
c3d4e5f Add feature B
b2c3d4e Add feature A
```

### Explanation:
MAJOR changes when incompatible, MINOR when adding compatible features, PATCH for bug fixes. Clear progression shows development.

---

## Exercise 6: Tag Signed Releases - Solution

### Commands:
```bash
# Setup GPG (if not done)
gpg --list-secret-keys

# Create signed tag
git tag -s v1.0.0 -m "Signed release v1.0.0"

# View signed tag
git show v1.0.0
# Shows: Signature made...

# Verify signature
git verify-tag v1.0.0

# Create another signed tag
git tag -s v2.0.0 -m "Signed release v2.0.0"

# Create unsigned tag for comparison
git tag v2.0.0-unsigned

# List tags
git tag -l

# Show tag details
git show v1.0.0  # Shows signature
git show v2.0.0-unsigned  # No signature

# Verify all signed tags
git tag -l | xargs -n 1 git verify-tag
```

### Example Output:
```
$ git tag -s v1.0.0 -m "Signed release"
# GPG password prompt appears

$ git show v1.0.0
tag v1.0.0
Tagger: Your Name <your@email.com>
Date:   Mon Jan 15 12:00:00 2026 +0000

Signed release v1.0.0
-----BEGIN PGP SIGNATURE-----
...
-----END PGP SIGNATURE-----

$ git verify-tag v1.0.0
object a1b2c3d
type commit
tagger Your Name <your@email.com>
...
gpg: Good signature from "Your Name <your@email.com>"
```

### Explanation:
Signed tags verify commit authenticity with GPG. Important for security-conscious projects and official releases.

---

## Exercise 7: Create Releases with Descriptions - Solution

### Commands:
```bash
# Create v2.1.0 with detailed notes
git tag -a v2.1.0 -m "Release v2.1.0

## New Features
- User authentication system
- Dashboard redesign
- API versioning

## Bug Fixes
- Fix memory leak in cache
- Resolve race condition in workers
- Security: SQL injection prevention

## Known Issues
- Mobile UI needs refinement
- Performance on large datasets"

# Create v2.2.0 with similar detail
git tag -a v2.2.0 -m "Release v2.2.0

## New Features
- WebSocket support
- GraphQL API
- Dark mode UI

## Bug Fixes
- Fixed authentication timeout
- Resolved file upload issue

## Changelog
See CHANGELOG.md for details"

# View full release notes
git show v2.1.0
git show v2.2.0

# Export release notes
git show v2.1.0 | tail -n +6 > RELEASE-2.1.0.md
```

### Example Output:
```
$ git show v2.1.0
tag v2.1.0
Tagger: Your Name
Date: Mon Jan 15 12:00:00 2026 +0000

Release v2.1.0

## New Features
- User authentication system
...
```

### Explanation:
Detailed release notes in tags provide history and documentation. Combined with changelog files for comprehensive release information.

---

## Exercise 8: Pre-Release and Build Metadata - Solution

### Commands:
```bash
# Alpha release
echo "alpha" > status.txt
git add status.txt
git commit -m "Version 1.0.0-alpha"
git tag v1.0.0-alpha

# Beta release
echo "beta" > status.txt
git add status.txt
git commit -m "Version 1.0.0-beta"
git tag v1.0.0-beta

# Release candidate
echo "rc.1" > status.txt
git add status.txt
git commit -m "Version 1.0.0-rc.1"
git tag v1.0.0-rc.1

# Final release
echo "final" > status.txt
git add status.txt
git commit -m "Version 1.0.0"
git tag v1.0.0

# Build metadata
echo "build.123" > status.txt
git add status.txt
git commit -m "Version 1.0.0+build.123"
git tag v1.0.0+build.123

# List all tags
git tag -l | sort -V

# Understand version ordering
# Pre-releases are before final: v1.0.0-alpha < v1.0.0
# Build metadata doesn't affect precedence: v1.0.0 = v1.0.0+build.123
```

### Example Output:
```
$ git tag -l | sort -V
v1.0.0-alpha
v1.0.0-beta
v1.0.0-rc.1
v1.0.0
v1.0.0+build.123
```

### Explanation:
Pre-releases (alpha, beta, rc) mark stages before final. Build metadata provides additional context without affecting version ordering.

---

## Exercise 9: Compare Tags and View Changes - Solution

### Commands:
```bash
# Create v1.0.0
echo "Core features" > core.txt
git add core.txt
git commit -m "v1.0.0 release"
git tag v1.0.0

# Add features for v1.1.0
echo "Feature 1" > feat1.txt
git add feat1.txt
git commit -m "Add feature 1"

echo "Feature 2" > feat2.txt
git add feat2.txt
git commit -m "Add feature 2"

git tag v1.1.0

# Compare versions
git log v1.0.0..v1.1.0 --oneline
git log v1.0.0..v1.1.0 --stat
git log v1.0.0..v1.1.0 --numstat

# View file changes
git diff v1.0.0..v1.1.0
git diff --stat v1.0.0..v1.1.0

# Create v2.0.0 with major changes
echo "New architecture" > arch.txt
git add arch.txt
git commit -m "v2.0.0 breaking changes"
git tag v2.0.0

# Compare v1.1.0 to v2.0.0
git log v1.1.0..v2.0.0 --oneline
git log v1.1.0..v2.0.0 --stat

# Generate summary
git shortlog v1.0.0..v1.1.0
```

### Example Output:
```
$ git log v1.0.0..v1.1.0 --oneline
c3d4e5f Add feature 2
b2c3d4e Add feature 1

$ git diff --stat v1.0.0..v1.1.0
 feat1.txt | 1 +
 feat2.txt | 1 +
 2 files changed, 2 insertions(+)

$ git shortlog v1.0.0..v1.1.0
Your Name (2):
  Add feature 1
  Add feature 2
```

### Explanation:
Use tags to compare versions. Shows commits, files changed, and line changes. Useful for release notes and impact analysis.

---

## Exercise 10: Organize Tags with Naming Conventions - Solution

### Commands:
```bash
# Version tags
git tag v1.0.0
git tag v1.1.0
git tag v2.0.0

# Release date tags
git tag release-2026-01-15
git tag release-2026-02-01

# Milestone tags
git tag milestone/beta
git tag milestone/production

# Environment tags (moveable tags)
git tag -f stable
git tag -f testing
git tag -f development

# Component tags
git tag app-v1.0
git tag api-v2.0
git tag lib-v3.0

# List all tags
git tag -l

# Filter by pattern
git tag -l 'v*'
git tag -l 'release-*'
git tag -l 'milestone/*'
git tag -l '*-v*'

# Sort tags
git tag -l | sort -V

# Document strategy
cat > TAGGING_STRATEGY.md << 'EOF'
# Tagging Strategy

## Version Tags
- Format: v<major>.<minor>.<patch>
- Example: v1.0.0, v1.1.0, v2.0.0

## Release Date Tags
- Format: release-YYYY-MM-DD
- Example: release-2026-01-15

## Milestone Tags
- Format: milestone/<stage>
- Values: beta, production, staging

## Environment Tags
- Format: <env>
- Values: stable, testing, development
- Note: Moveable tags pointing to latest in environment

## Component Tags
- Format: <component>-v<version>
- Example: app-v1.0, api-v2.0, lib-v3.0
EOF
```

### Example Output:
```
$ git tag -l
app-v1.0
api-v2.0
development
lib-v3.0
milestone/beta
milestone/production
release-2026-01-15
release-2026-02-01
stable
testing
v1.0.0
v1.1.0
v2.0.0

$ git tag -l 'v*'
v1.0.0
v1.1.0
v2.0.0

$ git tag -l 'release-*'
release-2026-01-15
release-2026-02-01
```

### Explanation:
Multiple tagging conventions serve different purposes. Version tags for releases, date tags for timeline, milestone/environment tags for current state, component tags for multi-component projects.

