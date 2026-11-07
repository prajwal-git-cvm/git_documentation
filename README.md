# Git Commands Documentation

A beginner-friendly, practical reference for tracking files, saving
versions, exploring commit history, restoring work, and managing
branches.

-   **23 topics**
-   Copy-ready commands
-   No external dependencies

------------------------------------------------------------------------

# Git --- Part 1: Basic Commands

## 01. Initialize a Git Repository

Start tracking a project with Git.

### Check Git status

``` bash
git status
```

Shows the current branch and changes in your project.

### Initialize Git

``` bash
git init
```

Creates a new Git repository in the current directory.

### Rename the default branch

``` bash
git branch -m main
```

Renames the current branch to `main`.

------------------------------------------------------------------------

## 02. Track Files

Choose which changes Git should include in the next commit.

### Check untracked files

``` bash
git status
```

Untracked files are files Git knows about but is not tracking yet.

### Add a specific file

``` bash
git add config.js
```

### Add a folder

``` bash
git add src/
```

### Add all changes

``` bash
git add .
```

Stages changes in the current directory and its subdirectories.

### Unstage changes

``` bash
git reset
git reset config.js
```

-   `git reset` unstages all staged changes.
-   `git reset config.js` unstages only `config.js`.
-   Your working files remain unchanged.

------------------------------------------------------------------------

## 03. Configure Git Username and Email

Set the author details recorded in commits.

### Set your global identity

``` bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Applies to all repositories unless a repository-specific setting
overrides it.

### Set identity for one repository

Run these commands inside the repository:

``` bash
git config user.name "Your Name"
git config user.email "you@example.com"
```

### View configuration

``` bash
git config --list
```

### Create a shortcut for status

``` bash
git config --global alias.s "status"

# Use the shortcut
git s
```

------------------------------------------------------------------------

## 04. Create Commits

A commit saves a snapshot of staged changes.

### Create your first commit

``` bash
git add .
git commit -m "Initial commit"
```

### Create another commit

``` bash
git add .
git commit -m "Update project"
```

Use a clear message that describes what changed.

------------------------------------------------------------------------

## 05. View Commit History

Inspect saved versions and how they connect.

### Show commit history

``` bash
git log
```

Shows commit IDs, authors, dates, and messages.

### Show history from all references

``` bash
git log --all
```

### Show history as a graph

``` bash
git log --all --graph
```

### Show a shorter history

``` bash
git log --oneline
```

------------------------------------------------------------------------

## 06. Modify the Previous Commit

Amend the most recent commit.

``` bash
git add .
git commit --amend -m "Updated commit message"
```

Replaces the previous commit with a new one containing the staged
changes and updated message.

**Important:** Amending changes the commit ID. Avoid amending commits
already shared with others unless you understand the effects.

------------------------------------------------------------------------

## 07. Restore Changes

Unstage files or discard local edits.

### Restore a file from staging

``` bash
git restore --staged config.js
```

Unstages the file but keeps its changes in your working directory.

### Discard changes in a file

``` bash
git restore config.js
```

Restores the file from the staging area, or from the last commit if it
is not staged.

**Warning:** This can permanently discard uncommitted changes.

### Restore all tracked files in the current directory

``` bash
git restore .
```

### Restore a file from an older commit

``` bash
git restore --source=<commit-id> -- config.js

# Example: restore from the previous commit
git restore --source=HEAD~1 -- config.js
```

Restores that file without moving the current branch.

------------------------------------------------------------------------

## 08. Switch Between Commits

Inspect a past snapshot or move between branches.

### Switch to a specific commit

``` bash
git checkout <commit-id>

# Example
git checkout a1b2c3d
```

Lets you view the project at that commit. This normally puts Git into a
detached HEAD state.

### Return to the main branch

``` bash
git checkout main
```

### Use the newer switch command

``` bash
git switch main
git switch -
```

-   `git switch main` switches to `main`.
-   `git switch -` returns to the previously checked-out branch.

------------------------------------------------------------------------

## 09. Understand Detached HEAD

A detached HEAD means you checked out a commit directly, not a branch.

### Enter detached HEAD state

``` bash
git checkout <commit-id>
```

You can inspect the project and experiment. New commits made here are
not automatically connected to a branch.

### Create a branch to keep your work

``` bash
git switch -c experiment
```

Creates a branch at the current commit and switches to it.

### Keep an existing detached commit

``` bash
git branch saved-work <commit-id>
```

Creates a branch that points to that commit.

------------------------------------------------------------------------

## 10. Restore an Older Version of the Project

Bring old file contents into your current working tree.

### Restore all tracked files from a commit

``` bash
git restore --source=<commit-id> -- .
```

Updates the working files to match the selected commit. It does not move
the current branch.

### Save the restored version as a new commit

``` bash
git add .
git commit -m "Restore previous version"
```

Creates a new commit while keeping the existing history.

------------------------------------------------------------------------

## 11. Create and Use a `.gitignore` File

Tell Git which untracked files and folders to ignore.

### Example `.gitignore`

``` gitignore
# Environment files
.env

# Python cache
__pycache__/

# Build output
bin/

# Temporary files
*.tmp
```

Already-tracked files are not automatically ignored.

### Stop tracking a file without deleting it

``` bash
git rm --cached config.js
```

Add the file to `.gitignore` as well if you want Git to continue
ignoring it.

------------------------------------------------------------------------

## 12. Remove Git from a Project

Delete the local repository metadata.

**Linux/macOS:**

``` bash
rm -rf .git
```

**Warning:** This deletes the local Git repository and its history. It
does not delete your project files. This is difficult to undo, so make
sure you really want to remove Git.

------------------------------------------------------------------------

## 13. Common Mistakes

  Mistake                        Correct command
  ------------------------------ ----------------------
  `git statuss`                  `git status`
  `git log -graph`               `git log --graph`
  `git add /`                    `git add .`
  `git restore` without a file   `git restore <file>`

### Remember

-   `git add` stages changes.
-   `git commit` saves staged changes.
-   `git status` shows the current state.
-   `git log` shows commit history.
-   `git restore` restores files.
-   `git checkout` can switch branches or commits.
-   `git switch` is the newer command for switching branches.
-   `.gitignore` helps keep selected untracked files out of Git.

------------------------------------------------------------------------

# Git --- Part 2: Branching

## 14. Create a Branch

``` bash
git branch feature1
```

Creates a new branch named `feature1` at the current commit.

Use a separate branch to work on a feature or fix without changing the
main branch.

------------------------------------------------------------------------

## 15. Create and Switch to a Branch

### Create a branch

``` bash
git branch feature1
```

Creates a new branch named `feature1` at the current commit.

### Switch to a branch

``` bash
git switch feature1
```

Switches to the existing `feature1` branch.

### Create and switch in one command

``` bash
git switch -c feature1
```

Creates the branch and switches to it.

------------------------------------------------------------------------

## 16. List Branches

``` bash
git branch
```

Shows local branches. The current branch is marked with `*`.

------------------------------------------------------------------------

## 17. Work on a Separate Branch

Make changes and commit them on the feature branch.

``` bash
echo "New feature" > feature.txt
git add feature.txt
git commit -m "Add new feature"
```

The new commit belongs to `feature1`. The `main` branch remains at its
previous commit.

Example branch history:

``` text
A---B---C (main)
         \
          D (feature1)
```

------------------------------------------------------------------------

## 18. Switch Back to the Main Branch

### Switch to main

``` bash
git switch main
```

Switches back to `main`.

### Return to the previous branch

``` bash
git switch -
```

Switches to the branch you were on before.

------------------------------------------------------------------------

## 19. Merge a Branch

Combine changes from one branch into another.

### Merge a feature branch into main

``` bash
git switch main
git merge feature1
```

Git merges the changes from `feature1` into `main`.

**Important:** Switch to the branch that should receive the changes
before running `git merge`.

### Fast-forward merge

A fast-forward merge happens when `main` has not received new commits
since `feature1` was created.

Before:

``` text
A---B---C (main)
         \
          D---E (feature1)
```

After:

``` text
A---B---C---D---E (main, feature1)
```

Git moves the `main` branch pointer forward. No merge commit is created.

### Three-way merge

A three-way merge happens when both branches have new commits.

Before:

``` text
A---B---C---F (main)
         \
          D---E (feature1)
```

After:

``` text
A---B---C---F---M (main)
         \       /
          D---E
```

Git creates a merge commit (`M`) that connects both histories.

------------------------------------------------------------------------

## 20. Resolve Merge Conflicts

Fix changes Git cannot automatically combine.

### Check the conflicting files

``` bash
git status
```

### Example conflict

``` text
<<<<<<< HEAD
Change from main
=======
Change from feature1
>>>>>>> feature1
```

-   `HEAD` represents the current branch.
-   The section below `=======` contains the incoming changes.
-   `>>>>>>> feature1` marks the end of the incoming changes.

Edit the file to keep the correct content and remove the conflict
markers.

### Complete the merge

``` bash
git add filename.txt
git commit
```

Git creates a merge commit after the conflict is resolved.

### Cancel the merge

``` bash
git merge --abort
```

Attempts to return the working tree to its state before the merge
started.

------------------------------------------------------------------------

## 21. Delete a Branch

Remove a feature branch when it is no longer needed.

### Delete a merged branch

``` bash
git branch -d feature1
```

Deletes the branch only if Git considers it safely merged.

### Force-delete an unmerged branch

``` bash
git branch -D feature1
```

**Warning:** Force-deleting a branch can make its unmerged commits
harder to find.

------------------------------------------------------------------------

## 22. View Branch History

Display commits from all branches in a compact graph.

``` bash
git log --all --graph --oneline
```

Example:

``` text
*   a1b2c3d (HEAD -> main) Merge feature1
|\
| * e4f5g6h Add new feature
* | i7j8k9l Fix a bug
|/
* m1n2o3p Initial commit
```

------------------------------------------------------------------------

## 23. Remember

Quick review of important branching commands:

  Command                             Purpose
  ----------------------------------- --------------------------------------
  `git branch`                        Creates and lists branches
  `git switch`                        Changes branches
  `git switch -c`                     Creates and switches to a branch
  `git merge`                         Combines changes from another branch
  `git merge --abort`                 Cancels an unfinished merge
  `git branch -d`                     Deletes a merged branch
  `git log --all --graph --oneline`   Shows branch history

------------------------------------------------------------------------

## Quick Git Workflow

A common workflow for saving project changes:

``` bash
# Check the current state
git status

# Stage changes
git add .

# Save the changes
git commit -m "Describe your changes"

# View commit history
git log --oneline
```

**Quick reminder:** Stage with `git add`, save with `git commit`, and
inspect with `git status`.
