# Git Internals - Exercises

## Exercise 1: Explore the .git Directory Structure
**Difficulty:** Easy

Understand the basic structure of a Git repository's internal folder.

**Instructions:**
1. Initialize a new Git repository
2. List the contents of the `.git` directory
3. Explore the major subdirectories: `objects`, `refs`, `HEAD`
4. Identify what each main directory contains
5. Create a simple text file and commit it
6. Compare the `.git` directory before and after the commit
7. Note any new files or changes in the `.git` folder

**Expected Outcome:**
- You can navigate the `.git` folder structure
- You understand that `.git/objects` stores commits, trees, and blobs
- You understand that `.git/refs` stores branch references
- You see how commits create new objects

---

## Exercise 2: Understand Git Objects (Blobs)
**Difficulty:** Easy

Learn how Git stores file content as blob objects.

**Instructions:**
1. Create a file `message.txt` with content "Hello World"
2. Stage and commit the file
3. Use `git hash-object` to compute the SHA-1 hash of the file
4. Look in `.git/objects` for the blob file using the hash
5. Extract the first 2 characters of the hash as the directory name
6. Extract the remaining characters as the filename
7. Try to read the blob file directly (it's compressed)
8. Use `git cat-file -p <hash>` to view the blob content
9. Modify the file and compute a new hash - verify it's different

**Expected Outcome:**
- You understand blobs store file content
- You can find blob objects in `.git/objects` by hash
- You know blobs are referenced by SHA-1 hash
- You understand content changes = different hash

---

## Exercise 3: Understand Git Objects (Trees)
**Difficulty:** Medium

Learn how Git stores directory structure as tree objects.

**Instructions:**
1. Create a directory structure with files:
   - `src/app.js`
   - `src/utils.js`
   - `README.md`
2. Commit all files
3. Use `git cat-file -p <commit-hash>` to view the commit
4. Note the tree hash from the commit
5. Use `git cat-file -p <tree-hash>` to view the tree
6. Understand the tree format showing mode, type, hash, and filename
7. Examine a subtree (`src`) in the same way
8. Understand how trees reference blobs and other trees

**Expected Outcome:**
- You understand trees map filenames to blob hashes
- You understand trees can contain other trees
- You can navigate tree structures
- You know commit → tree → blobs hierarchy

---

## Exercise 4: Understand Commits and Their Structure
**Difficulty:** Medium

Examine the internal structure of commit objects.

**Instructions:**
1. Make a commit with a message and author info
2. Get the commit hash using `git log --oneline`
3. Use `git cat-file -p <commit-hash>` to view the commit object
4. Identify the components:
   - tree (root directory snapshot)
   - parent (previous commit)
   - author (name and email)
   - committer (name and email)
   - commit message
5. Make another commit and examine its parent pointer
6. Verify the parent hash matches the previous commit
7. Make a commit on a different branch and examine its structure

**Expected Outcome:**
- You understand commit structure
- You know each commit points to a tree and parent
- You understand commits are immutable (hash = content)
- You see how commits form a linked list

---

## Exercise 5: Examine Git References (Refs)
**Difficulty:** Medium

Learn how branches and tags are stored as references.

**Instructions:**
1. Create a branch `feature/test`
2. Look in `.git/refs/heads/` directory
3. Find and read the `main` file - it contains a commit hash
4. Read the `feature/test` file - it also contains a commit hash
5. Switch to a different branch
6. Check that `.git/HEAD` now points to the new branch
7. Create a lightweight tag
8. Look in `.git/refs/tags/` to see the tag reference
9. Create an annotated tag
10. Verify annotated tags are also stored as objects

**Expected Outcome:**
- You understand branches are just references to commits
- You know `.git/HEAD` points to the current branch
- You understand how switching branches changes HEAD
- You know where tags are stored

---

## Exercise 6: Understand HEAD and Detached HEAD State
**Difficulty:** Medium

Learn what HEAD is and how detached HEAD works.

**Instructions:**
1. Check `.git/HEAD` - it points to `ref: refs/heads/main`
2. Make a commit while on main
3. Check out an older commit directly by hash
4. Notice you're in "detached HEAD" state
5. Verify `.git/HEAD` now contains the commit hash directly (not a ref)
6. Make a commit while detached
7. Notice this commit is on no branch
8. Try to return to main - note the warning about the detached commit
9. Create a branch from the detached commit
10. Return to normal HEAD state pointing to a branch

**Expected Outcome:**
- You understand HEAD usually points to a branch reference
- You understand detached HEAD means HEAD points to a commit
- You know commits on detached HEAD can be orphaned
- You can recover commits with branch creation

---

## Exercise 7: Explore Git Object Types
**Difficulty:** Medium

Examine all four git object types: blob, tree, commit, tag.

**Instructions:**
1. Create a small repository with one commit
2. Get the commit hash from `git log`
3. Use `git cat-file -t <hash>` to see it's type "commit"
4. Use `git cat-file -p <hash>` to view the commit
5. Get the tree hash from the commit
6. Verify `git cat-file -t <tree-hash>` shows type "tree"
7. Get a blob hash from the tree
8. Verify `git cat-file -t <blob-hash>` shows type "blob"
9. Create an annotated tag
10. Get its hash and verify `git cat-file -t` shows type "tag"
11. List all 4 types of objects in your repository

**Expected Outcome:**
- You can identify all 4 object types
- You understand the relationships: commit → tree → blob
- You know tags can be objects (annotated) or references (lightweight)
- You can use `git cat-file` to inspect objects

---

## Exercise 8: Calculate SHA-1 Hashes
**Difficulty:** Medium

Understand how Git calculates commit hashes.

**Instructions:**
1. Create a file and stage it (don't commit yet)
2. Use `git hash-object` to calculate the blob hash manually
3. Compare with what Git stored (look in `.git/objects`)
4. Make a commit with a specific message and author
5. Use `git rev-parse HEAD` to get the commit hash
6. Understand that commit hash = SHA-1 of commit object content
7. Change author name in config and create another commit
8. Note that the same file + message with different author = different hash
9. Verify that commit hash is fully determined by its content

**Expected Outcome:**
- You understand blobs are hashed from file content
- You understand commits are hashed from metadata + tree + message
- You know changing author/date changes the commit hash
- You understand Git's immutability principle

---

## Exercise 9: Understand Pack Files
**Difficulty:** Medium

Learn how Git optimizes storage with pack files.

**Instructions:**
1. Create a repository with multiple commits
2. Look in `.git/objects` - see individual object files
3. Run `git gc` (garbage collection)
4. Check `.git/objects/pack/` - new pack files are created
5. Understand pack files compress and deduplicate objects
6. Look at `.pack` files (binary) and `.idx` files (index)
7. Check file sizes: individual objects vs pack files
8. Verify that `git log` and `git cat-file` still work normally
9. Run `git verify-pack -v <packfile>` to see pack contents

**Expected Outcome:**
- You understand pack files optimize storage
- You know `.pack` contains compressed objects
- You know `.idx` provides fast lookup in pack files
- You understand `git gc` creates pack files
- You see the storage optimization benefits

---

## Exercise 10: Examine Git Configuration Objects
**Difficulty:** Medium

Learn how Git stores configuration and metadata.

**Instructions:**
1. Check `.git/config` - local repository configuration
2. Check `~/.gitconfig` (or `~/.config/git/config`) - global configuration
3. Review sections: `[core]`, `[user]`, `[remote]`, `[branch]`
4. Use `git config --local` to view local config
5. Use `git config --global` to view global config
6. Look at the `index` file in `.git` - this is the staging area
7. Look at `.git/hooks` - directory for Git hooks
8. Check common hooks: `pre-commit`, `post-commit`
9. Understand that hooks are executable scripts
10. Review `.git/packed-refs` if it exists (compressed refs)

**Expected Outcome:**
- You understand `.git/config` stores repository settings
- You know the difference between local and global config
- You understand the index file tracks staging area
- You know hooks are scripts that run at Git events
- You see all the metadata Git stores internally

