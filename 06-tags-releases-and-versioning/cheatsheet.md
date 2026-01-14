# Tags, Releases, and Versioning - Cheatsheet

## Tag Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `git tag <name>` | Create lightweight tag | `git tag v1.0.0` |
| `git tag -a <name> -m "msg"` | Create annotated tag | `git tag -a v1.0.0 -m "Release 1.0.0"` |
| `git tag -l` | List all tags | `git tag -l` |
| `git tag -l <pattern>` | List tags matching pattern | `git tag -l 'v1*'` |
| `git show <tag>` | Show tag details | `git show v1.0.0` |
| `git tag -d <name>` | Delete tag | `git tag -d v1.0.0` |
| `git tag -s <name> -m "msg"` | Create signed tag | `git tag -s v1.0.0 -m "Release"` |
| `git verify-tag <name>` | Verify GPG signature | `git verify-tag v1.0.0` |
| `git switch <tag>` | Checkout tag | `git switch v1.0.0` |

---

## Lightweight vs Annotated Tags

| Feature | Lightweight | Annotated |
|---------|-------------|-----------|
| Storage | Reference (simple file) | Full object |
| Tagger | None | Name + email |
| Date | None | Timestamp |
| Message | None | Full message |
| Signature | No | Optional (with `-s`) |
| Size | Minimal | Slightly larger |
| Use Case | Temporary | Official releases |

### Creating Tags
```bash
# Lightweight - just a reference
git tag v1.0.0

# Annotated - with metadata
git tag -a v1.0.0 -m "Release 1.0.0"

# Signed - with GPG signature
git tag -s v1.0.0 -m "Signed release"

# Multiline message
git tag -a v1.0.0 -m "Release 1.0.0

New features:
- Feature A
- Feature B

Bug fixes:
- Fixed issue X"
```

---

## Semantic Versioning (SemVer)

### Format: MAJOR.MINOR.PATCH

| Version Part | When to Increment | Example |
|---|---|---|
| MAJOR | Breaking changes | 1.0.0 → 2.0.0 |
| MINOR | New features (backward compatible) | 1.0.0 → 1.1.0 |
| PATCH | Bug fixes | 1.0.0 → 1.0.1 |

### Pre-Release Versions
```
v1.0.0-alpha     # Alpha version
v1.0.0-beta      # Beta version
v1.0.0-rc.1      # Release candidate 1
v1.0.0           # Final release
```

### Build Metadata
```
v1.0.0+build.123   # With build number
v1.0.0+git.a1b2c3d # With commit hash
```

### Version Ordering
- `v1.0.0-alpha < v1.0.0-beta < v1.0.0-rc.1 < v1.0.0`
- `v1.0.0 = v1.0.0+build.123` (build metadata doesn't affect precedence)

---

## Tagging Strategies

### Version-Based Tagging
```bash
git tag v1.0.0      # Initial release
git tag v1.0.1      # Patch
git tag v1.1.0      # Minor release
git tag v2.0.0      # Major release
```

### Date-Based Tagging
```bash
git tag release-2026-01-15
git tag release-2026-02-01
```

### Component-Based Tagging
```bash
git tag app-v1.0     # Application
git tag api-v2.0     # API
git tag lib-v3.0     # Library
```

### Environment Tagging
```bash
git tag stable       # Production ready
git tag testing      # Testing environment
git tag development  # Development
```

### Milestone Tagging
```bash
git tag milestone/alpha
git tag milestone/beta
git tag milestone/production
```

---

## Working with Tags

### Tag From Previous Commit
```bash
git tag v1.0.0 <commit-hash>
```

### Move a Tag
```bash
git tag -f v1.0.0 <new-commit>  # Force move tag
```

### Create Branch From Tag
```bash
git switch -c release/1.1.x v1.1.0
```

### Compare Versions
```bash
git log v1.0.0..v1.1.0 --oneline       # Commits between
git diff v1.0.0..v1.1.0                # Exact changes
git diff --stat v1.0.0..v1.1.0         # Summary
git diff v1.0.0 v1.1.0 -- path/file    # Specific file
```

### Get Tag Info
```bash
git describe                    # Most recent tag
git describe --tags            # Describe with tag
git rev-parse v1.0.0          # Get commit hash
git for-each-ref --sort=-version:refname --format='%(refname:short)' refs/tags
```

---

## Release Workflow

### 1. Prepare Release
```bash
# Update version numbers
# Update changelog
# Commit changes
git commit -m "Prepare v1.0.0 release"
```

### 2. Create Release Tag
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

### 3. Push Tag
```bash
git push origin v1.0.0         # Push specific tag
git push origin --tags         # Push all tags
```

### 4. Create Release Branch (if needed)
```bash
git switch -c release/1.0.x
```

### 5. Continue Development
```bash
git switch develop
# Continue with v1.1.0 development
```

---

## GPG Signing Tags

### Setup GPG
```bash
gpg --list-secret-keys
# Configure Git to use your key
git config user.signingkey <key-id>
```

### Sign Tags
```bash
git tag -s v1.0.0 -m "Release 1.0.0"  # Prompt for passphrase
git tag -s --no-verify v1.0.0          # Skip passphrase
```

### Verify Signatures
```bash
git verify-tag v1.0.0
git tag -v v1.0.0                      # Verify with key details
```

---

## Naming Conventions

### Good Tag Names
```
v1.0.0              ✓ Version only
v1.0.0-alpha        ✓ With pre-release
app-v1.0            ✓ Component prefix
release-2026-01-15  ✓ Date format
milestone/beta      ✓ Milestone
```

### Avoid
```
v1.0                ✗ Incomplete version
1.0.0               ✗ Missing prefix
Version 1.0.0       ✗ Spaces
v1_0_0              ✗ Underscores instead of dots
```

---

## Tips & Best Practices

1. **Use Annotated Tags for Releases**
   - Contains metadata
   - Verifiable with GPG
   - Readable history

2. **Consistent Naming**
   - Use semantic versioning
   - Stick to one naming convention
   - Document your strategy

3. **Sign Important Tags**
   - Security best practice
   - Verifies author
   - Important for official releases

4. **Push Tags to Remote**
   ```bash
   git push origin v1.0.0     # Specific tag
   git push origin --tags     # All tags
   ```

5. **Delete Old Tags Carefully**
   - Local: `git tag -d v1.0.0`
   - Remote: `git push origin --delete v1.0.0`

6. **Use Moveable Tags**
   - `latest` points to latest stable
   - `stable` for production
   - Update with `-f` flag

