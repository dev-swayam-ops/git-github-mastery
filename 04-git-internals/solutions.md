# Git Internals - Solutions

## Exercise 1: Explore the .git Directory Structure - Solution

### Commands:
```bash
# Initialize a new repository
git init my-repo
cd my-repo

# List .git contents
ls -la .git

# Explore major directories
ls -la .git/objects
ls -la .git/refs
cat .git/HEAD

# Create and commit a file
echo "Hello World" > message.txt
git add message.txt
git commit -m "Initial commit"

# Check .git again
ls -la .git
ls -la .git/objects/
```

### Example Output:
```
$ ls -la .git
total 40
drwxr-xr-x  HEAD
drwxr-xr-x  config
drwxr-xr-x  description
drwxr-xr-x  hooks
drwxr-xr-x  info
drwxr-xr-x  objects
drwxr-xr-x  refs

$ cat .git/HEAD
ref: refs/heads/main

$ ls -la .git/objects
drwxr-xr-x  pack
drwxr-xr-x  info
drwxr-xr-x  a1  (new after commit)
drwxr-xr-x  c5  (new after commit)
```

### Explanation:
- `.git/HEAD` points to the current branch
- `.git/refs` contains branch and tag references
- `.git/objects` stores all blob, tree, and commit objects
- `.git/config` stores repository configuration
- `.git/hooks` stores hook scripts

---

## Exercise 2: Understand Git Objects (Blobs) - Solution

### Commands:
```bash
# Create and commit a file
echo "Hello World" > message.txt
git add message.txt
git commit -m "Add message"

# Calculate blob hash
git hash-object message.txt
# Output: 557db03de997c86a4a122d1c7ec084

# Find in .git/objects
ls -la .git/objects/55/
cat .git/objects/55/7db03de997c86a4a122d1c7ec084  # Binary output

# View blob content
git cat-file -p 557db03de997c86a4a122d1c7ec084

# Verify it's a blob
git cat-file -t 557db03de997c86a4a122d1c7ec084

# Modify file and compute new hash
echo "Hello World Modified" > message.txt
git hash-object message.txt
# Output: different hash
```

### Example Output:
```
$ git hash-object message.txt
557db03de997c86a4a122d1c7ec084278c4beca

$ ls -la .git/objects/55/
total 8
-rw-r--r--  557db03de997c86a4a122d1c7ec084278c4beca

$ git cat-file -p 557db03
Hello World

$ git cat-file -t 557db03
blob

$ echo "Hello World Modified" > message.txt
$ git hash-object message.txt
8ab686eafeb1f44702738c8b0f24f6b1981cf38a
```

### Explanation:
- Blob hash = SHA-1 of file content
- First 2 chars of hash = directory name in `.git/objects`
- Remaining chars = filename in that directory
- Same content = same hash
- Different content = different hash
- Blobs are immutable and deduplicated by content

---

## Exercise 3: Understand Git Objects (Trees) - Solution

### Commands:
```bash
# Create directory structure
mkdir src
echo "console.log('app');" > src/app.js
echo "module.exports = {};" > src/utils.js
echo "# Project" > README.md

# Commit all files
git add .
git commit -m "Add project files"

# View commit
git cat-file -p HEAD

# View tree
git cat-file -p 4a5c8d2e1f3b6a9c7e2d1f4a

# View subtree (src)
git cat-file -p 5b6d9e3f2a4c7b1d8f3e2a5b
```

### Example Output:
```
$ git cat-file -p HEAD
tree 4a5c8d2e1f3b6a9c7e2d1f4a
author Your Name <email@example.com> 1234567890 +0000
committer Your Name <email@example.com> 1234567890 +0000

Add project files

$ git cat-file -p 4a5c8d2e
100644 blob 557db03de9  README.md
040000 tree 5b6d9e3f2a  src

$ git cat-file -p 5b6d9e3f
100644 blob 3a1c5d8f2e  app.js
100644 blob 7f2a4b1c6d  utils.js
```

### Explanation:
- Trees map filenames to object hashes
- Format: `mode type hash filename`
- `100644` = regular file
- `040000` = directory (tree)
- Trees create the directory hierarchy
- Commits point to the root tree

---

## Exercise 4: Understand Commits and Their Structure - Solution

### Commands:
```bash
# Make a commit
echo "Initial" > file1.txt
git add file1.txt
git commit -m "First commit"

# Get commit hash
FIRST=$(git rev-parse HEAD)
echo $FIRST

# View commit object
git cat-file -p $FIRST

# Make another commit
echo "Second" > file2.txt
git add file2.txt
git commit -m "Second commit"

# View second commit
git cat-file -p HEAD

# Verify parent hash
git cat-file -p HEAD | grep parent
```

### Example Output:
```
$ git cat-file -p a1b2c3d
tree 4a5c8d2e1f3b6a9c7e2d1f4a
author Your Name <email@example.com> 1234567890 +0000
committer Your Name <email@example.com> 1234567890 +0000

First commit

$ git cat-file -p HEAD
tree 8f1d6e4c2b9a3f7e1c5d2a4b
parent a1b2c3d  (matches FIRST)
author Your Name <email@example.com> 1234567890 +0000
committer Your Name <email@example.com> 1234567890 +0000

Second commit
```

### Explanation:
- Commit object contains: tree, parent, author, committer, message
- `tree` = root directory snapshot
- `parent` = previous commit hash (first commit has no parent)
- Author/committer timestamps are included
- Hash is SHA-1 of all this content
- Commits form a linked list via parent pointers

---

## Exercise 5: Examine Git References (Refs) - Solution

### Commands:
```bash
# Create a branch
git branch feature/test

# Check refs/heads
ls -la .git/refs/heads/
cat .git/refs/heads/main
cat .git/refs/heads/feature/test

# Check HEAD
cat .git/HEAD

# Switch branch
git switch feature/test
cat .git/HEAD

# Create lightweight tag
git tag v1.0.0

# Check tags
ls -la .git/refs/tags/
cat .git/refs/tags/v1.0.0

# Create annotated tag
git tag -a v1.1.0 -m "Version 1.1.0"

# Check annotated tag
git cat-file -p v1.1.0
git cat-file -t v1.1.0
```

### Example Output:
```
$ cat .git/refs/heads/main
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6

$ cat .git/HEAD
ref: refs/heads/main

$ git switch feature/test
$ cat .git/HEAD
ref: refs/heads/feature/test

$ ls -la .git/refs/tags/
v1.0.0
v1.1.0

$ cat .git/refs/tags/v1.0.0
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6

$ git cat-file -p v1.1.0
object a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
type commit
tag v1.1.0
tagger Your Name <email@example.com> 1234567890 +0000

Version 1.1.0
```

### Explanation:
- Branches are stored in `.git/refs/heads/`
- Each branch file contains a commit hash
- Tags are stored in `.git/refs/tags/`
- Lightweight tags are just reference files (no object)
- Annotated tags are objects (with tagger and message)
- HEAD points to current branch (or commit in detached state)

---

## Exercise 6: Understand HEAD and Detached HEAD State - Solution

### Commands:
```bash
# Check HEAD on a branch
cat .git/HEAD
# Output: ref: refs/heads/main

# Make a commit
echo "Content" > file.txt
git add file.txt
git commit -m "Add file"

# Get commit hash
COMMIT=$(git rev-parse HEAD)

# Checkout commit directly (detached HEAD)
git checkout $COMMIT

# Check HEAD now
cat .git/HEAD
# Output: the commit hash directly, not a ref

# Make a commit in detached state
echo "Detached" > detached.txt
git add detached.txt
git commit -m "Commit in detached state"

# Return to main
git switch main
# Warning about the detached commit

# Create branch from detached commit
git branch from-detached <detached-commit-hash>

# Check it's created
git branch | grep from-detached
```

### Example Output:
```
$ cat .git/HEAD
ref: refs/heads/main

$ git checkout a1b2c3d
Note: checking out 'a1b2c3d'.
You are in 'detached HEAD' state.

$ cat .git/HEAD
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6

$ git switch main
warning: you are leaving 1 commit behind, not connected to any of your branches

$ git branch from-detached e4f5g6h
$ git branch | grep from-detached
  from-detached
```

### Explanation:
- Normal HEAD = `ref: refs/heads/branch-name`
- Detached HEAD = commit hash directly
- Commits on detached HEAD can be orphaned
- Switching away from detached HEAD warns about orphaned commits
- Create a branch to save detached commits

---

## Exercise 7: Explore Git Object Types - Solution

### Commands:
```bash
# Create repository with commit
echo "Content" > file.txt
git add file.txt
git commit -m "Initial commit"

# Get commit hash
COMMIT=$(git rev-parse HEAD)

# Check commit type
git cat-file -t $COMMIT
# Output: commit

# View commit and get tree hash
git cat-file -p $COMMIT
# Extract tree hash
TREE=$(git cat-file -p $COMMIT | grep ^tree | cut -d' ' -f2)

# Check tree type
git cat-file -t $TREE
# Output: tree

# Get blob hash from tree
git cat-file -p $TREE
# Extract blob hash
BLOB=$(git cat-file -p $TREE | cut -d' ' -f3)

# Check blob type
git cat-file -t $BLOB
# Output: blob

# Create annotated tag
git tag -a v1.0.0 -m "Release 1.0.0"

# Get tag hash
TAG=$(git rev-parse v1.0.0)

# Check tag type
git cat-file -t $TAG
# Output: tag

# List all objects
find .git/objects -type f | wc -l
```

### Example Output:
```
$ git cat-file -t a1b2c3d
commit

$ git cat-file -t 4a5c8d2e
tree

$ git cat-file -t 557db03d
blob

$ git cat-file -t e7f1a3c9
tag

$ find .git/objects -type f | wc -l
4
```

### Explanation:
- 4 object types: blob, tree, commit, tag
- Hierarchy: commit → tree → blob
- Blob = file content
- Tree = directory structure
- Commit = snapshot + metadata
- Tag = annotated tags are objects; lightweight tags are refs

---

## Exercise 8: Calculate SHA-1 Hashes - Solution

### Commands:
```bash
# Create and stage file
echo "Content" > file.txt
git hash-object file.txt
# Output: blob hash

# Stage the file
git add file.txt

# Check it's stored in .git/objects
HASH=$(git hash-object file.txt)
ls -la .git/objects/${HASH:0:2}/${HASH:2}

# Commit with specific message
git commit -m "Test commit"

# Get commit hash
git rev-parse HEAD

# Change git config
git config user.name "Different Author"

# Make another commit with same file and message
echo "Same Content" > file2.txt
git add file2.txt
git commit -m "Same message"

# Compare hashes - they're different due to author
git log --oneline -n 2
# Different commits even with same file

# Verify immutability
git rev-parse HEAD
# Same hash always for same commit
```

### Example Output:
```
$ echo "Content" > file.txt
$ git hash-object file.txt
6dcd4ce23d88e2ee9568ba546c007c63d9131c1b

$ ls -la .git/objects/6d/
-rw-r--r-- 6dcd4ce23d88e2ee9568ba546c007c63d9131c1b

$ git commit -m "Test commit"
[main a1b2c3d] Test commit

$ git rev-parse HEAD
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6

$ git config user.name "Different Author"
$ git commit -m "Same message"
[main e4f5g6h] Same message  <- Different hash

$ git rev-parse HEAD
e4f5g6h7i8j9k0l1m2n3o4p5q6r7s8t9
```

### Explanation:
- Blob hash = SHA-1 of file content only
- Commit hash = SHA-1 of tree + parent + author + committer + message
- Same file + different author = different commit hash
- Commit hash is fully determined by its content
- Hash is immutable - same content = same hash

---

## Exercise 9: Understand Pack Files - Solution

### Commands:
```bash
# Create multiple commits
for i in {1..10}; do
  echo "Content $i" > file$i.txt
  git add file$i.txt
  git commit -m "Commit $i"
done

# Check individual objects
ls -la .git/objects | grep -v "^d" | wc -l

# Run garbage collection
git gc

# Check pack files
ls -la .git/objects/pack/
# Should see .pack and .idx files

# Verify objects still work
git log --oneline

# Verify specific objects
git cat-file -p HEAD

# Inspect pack file
git verify-pack -v .git/objects/pack/*.idx | head -20

# Check space savings
du -sh .git/objects/
```

### Example Output:
```
$ ls -la .git/objects | grep -v "^d"
total objects: 40

$ git gc
Enumerating objects: 20
Counting objects: 100%
Compressing objects: 100%
Writing objects: 100%

$ ls -la .git/objects/pack/
-rw-r--r--  pack-a1b2c3d.pack
-rw-r--r--  pack-a1b2c3d.idx

$ git verify-pack -v .git/objects/pack/pack-a1b2c3d.idx
a1b2c3d4 commit 150 bytes
b2c3d4e5 tree 200 bytes
c3d4e5f6 blob 50 bytes
...
```

### Explanation:
- Pack files compress and deduplicate objects
- `.pack` file contains the compressed objects
- `.idx` file is index for fast lookup
- `git gc` creates pack files automatically
- Saves significant disk space
- All Git operations work transparently with pack files

---

## Exercise 10: Examine Git Configuration Objects - Solution

### Commands:
```bash
# Check local repository config
cat .git/config

# Check global config
cat ~/.gitconfig  # or ~/.config/git/config on some systems

# View with git command
git config --local -l
git config --global -l

# Check the index file (staging area)
ls -la .git/index
file .git/index

# Explore hooks
ls -la .git/hooks/
ls -la .git/hooks/pre-commit.sample

# Look at packed-refs if it exists
cat .git/packed-refs  # May not exist

# View git configuration hierarchy
git config --system -l  # System-wide (if exists)
git config --global -l  # User global
git config --local -l   # Repository local
```

### Example Output:
```
$ cat .git/config
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
[user]
	name = Your Name
	email = your@email.com
[remote "origin"]
	url = https://github.com/user/repo.git
	fetch = +refs/heads/*:refs/remotes/origin/*

$ git config --local -l
core.repositoryformatversion=0
core.filemode=true
user.name=Your Name
user.email=your@email.com

$ ls -la .git/hooks/
applypatch-msg.sample
commit-msg.sample
post-update.sample
pre-commit.sample
...
```

### Explanation:
- `.git/config` stores local repository configuration
- `~/.gitconfig` stores user's global configuration
- Config can be system, global, or local (increasing specificity)
- `.git/index` is binary file tracking staging area
- Hooks in `.git/hooks/` are executable scripts
- `.sample` files show example hooks
- `packed-refs` compresses refs (optimization)

