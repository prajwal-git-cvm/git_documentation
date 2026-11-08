# Git Commands Documentation

view in webpage formate https://prajwal-git-cvm.github.io/git_documentation/

A beginner-friendly, practical reference for tracking files, saving
versions, exploring commit history, restoring work, and managing
branches.

-   **44 topics**
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

# Additional Git Commands

## 24. Compare Changes Using `git diff`

Compare file changes between your working directory, staging area, commits, or branches.

### Compare unstaged changes

```
git diff
```

Shows changes that have not been staged.

### Compare staged changes

```
git diff --staged
```

Shows changes that are staged but not committed.

### Compare two branches

```
git diff main feature1
```

Shows differences between two branches.

### Compare a branch with the current branch

```
git diff main
```

### Compare a specific file between branches

```
git diff main feature1 -- src/main.c
```

## 25. Understand `HEAD`, `HEAD~1` and Commit References

Git uses `HEAD` to identify the current position in your repository.

```
# Current commit
git log -1

# Previous commit
git show HEAD~1

# Two commits before HEAD
git show HEAD~2

# Show current HEAD reference
git rev-parse HEAD
```

- `HEAD` – Current commit.
- `HEAD~1` – One commit before HEAD.
- `HEAD~2` – Two commits before HEAD.
- `HEAD^` – First parent of the current commit.

## 26. Understand Merge Conflict Sides

When a merge conflict occurs, Git identifies two versions.

| Term   | Meaning                                       |
| ------ | --------------------------------------------- |
| Ours   | Changes from the currently checked-out branch |
| Theirs | Changes coming from the branch being merged   |

### Keep the current branch's version

```
git checkout --ours src/main.c
```

### Keep the incoming branch's version

```
git checkout --theirs src/main.c
```

### Apply to all conflicting files

```
git checkout --ours .
git checkout --theirs .
```

Important: These commands select one side's version. They discard the other side's conflicting content for the selected files.

### Complete conflict resolution

```
git add src/main.c
git commit -m "Resolve merge conflict"
```

## 27. View Details of a Commit

Use `git show` to inspect a particular commit.

```
# Show the latest commit
git show

# Show a specific commit
git show <commit-id>

# Show only the commit summary
git show --stat <commit-id>
```

Displays commit information and the changes introduced by that commit.

## 28. Rename a Branch

Change an existing branch name.

### Rename the current branch

```
git branch -m new-name
```

### Rename another branch

```
git branch -m old-name new-name
```

## 29. Configure the Default Initial Branch

Set the default branch name for newly initialized repositories.

```
git config --global init.defaultBranch main
```

Now, newly initialized repositories will use `main` instead of `master`.

## 30. View Git Configuration Details

### Show where configuration comes from

```
git config --list --show-origin
```

### View username

```
git config user.name
```

### View email

```
git config user.email
```

### Remove a global configuration

```
git config --global --unset user.name
```

# Advanced Git Commands

## 31. Stash – Temporarily save changes

```
# Save current changes
git stash

# Save with a description
git stash push -m "work in progress"

# List saved stashes
git stash list

# Apply latest stash (keep it saved)
git stash apply

# Apply and remove latest stash
git stash pop

# Apply a specific stash
git stash apply stash@{1}

# Delete a specific stash
git stash drop stash@{0}

# Delete all stashes
git stash clear
```

## 32. Rebase – Rewrite commit history

```
# Rebase current branch onto main
git rebase main

# Interactive rebase (last 3 commits)
git rebase -i HEAD~3

# Continue after resolving conflicts
git rebase --continue

# Skip the current commit
git rebase --skip

# Cancel rebase
git rebase --abort
```

## 33. Cherry-pick – Copy a specific commit

```
# Find commit IDs
git log --oneline

# Apply a specific commit to current branch
git cherry-pick <commit-id>

# Apply multiple commits
git cherry-pick <commit-id-1> <commit-id-2>

# Continue after resolving conflicts
git cherry-pick --continue

# Cancel cherry-pick
git cherry-pick --abort
```

## 34. Reflog – Recover previous Git states

```
# Show recent HEAD movements
git reflog

# Show reflog for all references
git reflog show --all

# Recover a previous commit
git reset --hard <commit-id>

# Create a recovery branch from a previous state
git branch recovery <commit-id>
```

## 35. Reset – Move branch history

```
# Undo commit but keep changes staged
git reset --soft HEAD~1

# Undo commit but keep changes unstaged
git reset --mixed HEAD~1

# Undo commit and discard changes
git reset --hard HEAD~1

# Reset to a specific commit
git reset --hard <commit-id>
```



Destructive

`--hard` can permanently discard uncommitted changes.



## 36. Revert – Safely undo commits

```
# Create a new commit that reverses a commit
git revert <commit-id>

# Revert without automatically committing
git revert --no-commit <commit-id>

# Revert a merge commit (choose parent 1)
git revert -m 1 <merge-commit-id>

# Cancel an ongoing revert
git revert --abort
```

## 37. Bisect – Find which commit introduced a bug

```
# Start bisect
git bisect start

# Mark current version as having the bug
git bisect bad

# Mark a known working commit
git bisect good <commit-id>

# Git checks commits between good and bad
# Test the code, then mark the result:
git bisect good
git bisect bad

# Finish bisect
git bisect reset
```

## 38. Worktree – Work on multiple branches simultaneously

```
# List worktrees
git worktree list

# Create a worktree for an existing branch
git worktree add ../project-feature feature

# Create a new branch and worktree
git worktree add -b feature-login ../project-login

# Remove a worktree
git worktree remove ../project-feature

# Clean up worktree references
git worktree prune
```

## 39. Tags – Manage versions and releases

```
# List tags
git tag

# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag
git tag -a v1.0.0 -m "First stable release"

# View tag information
git show v1.0.0

# Delete a local tag
git tag -d v1.0.0

# Push a specific tag
git push origin v1.0.0

# Push all tags
git push origin --tags

# Delete a remote tag
git push origin --delete v1.0.0
```

## 40. Clean – Remove untracked files

```
# Preview files that will be removed
git clean -n

# Remove untracked files
git clean -f

# Preview untracked files and directories
git clean -nd

# Remove untracked files and directories
git clean -fd

# Also remove ignored files (be careful)
git clean -fdx
```

## 41. Advanced Diff and Log

```
# Show changes between two commits
git diff <commit-1> <commit-2>

# Show changes in a specific file
git diff <commit-1> <commit-2> -- src/main.c

# Show commit details
git show <commit-id>

# Show only changed file names
git diff --name-only

# Show changed files in a commit
git diff-tree --no-commit-id --name-only -r <commit-id>

# Show commit history for a specific file
git log --follow -- src/main.c

# Show commits by author
git log --author="Name"

# Show commits within a date range
git log --since="2026-01-01" --until="2026-12-31"
```

## 42. Advanced Remote Commands

```
# Show remote URLs
git remote -v

# Change remote URL
git remote set-url origin <repository-url>

# Fetch all remotes and branches
git fetch --all

# Fetch and remove deleted remote-tracking branches
git fetch --prune

# Download remote changes without merging
git fetch origin

# Show remote branches
git branch -r

# Show local and remote branches
git branch -a

# Push current branch and set upstream
git push -u origin <branch-name>

# Push and delete a remote branch
git push origin --delete <branch-name>
```

## 43. Advanced Branch Commands

```
# Show merged branches
git branch --merged

# Show branches not yet merged
git branch --no-merged

# Delete a merged local branch
git branch -d <branch-name>

# Force-delete a local branch
git branch -D <branch-name>

# Track a remote branch
git branch --track <local-name> origin/<remote-name>

# Set upstream for current branch
git branch --set-upstream-to=origin/main

# Show upstream information
git branch -vv
```

## 44. Useful Advanced Commands

```
# Check repository integrity
git fsck

# Optimize repository storage
git gc

# Show repository information
git count-objects -vH

# Show files tracked by Git
git ls-files

# Find which commit introduced a line
git blame src/main.c

# Export a commit as a ZIP archive
git archive --format=zip HEAD -o project.zip

# Check Git version
git --version

# Show Git command help
git help <command>
```
# Introduction to Github with Git

## 45. Initialize and Connect a Remote Repository

```
# Initialize Git
git init

# Rename branch
git branch -M master

# Add remote repository
git remote add origin <repository-url>

# Check remote
git remote -v
```

## 46. Push a Local Repository to GitHub

```
# Stage and commit files
git add .
git commit -m "Initial commit"

# Push to GitHub
git push -u origin master
```

## 47. Handle Push Rejection

```
# Download remote changes
git fetch origin

# Merge remote changes
git pull origin master

# Push again
git push origin master
```

## 48. Force Push

```
# Force push
git push --force origin master

# Safer force push
git push --force-with-lease origin master
```

Warning: Force pushing can overwrite remote history.

## 49. View Remote Repositories

```
# List remote repositories
git remote

# Show remote URLs
git remote -v

# Show remote details
git remote show origin
```

## 50. Change Remote Repository URL

```
git remote set-url origin <new-repository-url>
```

## 51. Remove a Remote Repository

```
git remote remove origin
```

Removes the remote connection without deleting local files or commits.

## 52. Fetch Remote Changes

```
# Fetch from origin
git fetch origin

# Fetch all remotes
git fetch --all

# View remote branches
git branch -r

# View all branches
git branch -a
```

Downloads remote updates without merging them into the current branch.

## 53. Pull Remote Changes

```
# Pull from origin
git pull origin master

# Pull with rebase
git pull --rebase origin master
```

Downloads remote changes and integrates them into the current branch.

## 54. Clone a GitHub Repository

```
git clone <repository-url>
```

Downloads the repository and creates a local copy.

## 55. Clone with a Custom Directory Name

```
git clone <repository-url> my-project
```

Creates the local repository inside `my-project`.

## 56. Work Inside a Cloned Repository

```
# Open the cloned repository
cd my-project

# Check repository status
git status

# View commit history
git log --oneline
```

Run Git commands from inside the repository.

## 57. Check Repository Status

```
git status
git status -s
git status -sb
```

Shows modified, staged, and untracked files.

## 58. Commit Changes in a Cloned Repository

```
git add .
git commit -m "Update project"
```

Saves local changes as a new commit.

## 59. Amend the Latest Commit

```
git add .
git commit --amend -m "Updated commit"
```

Replaces the latest commit and changes its commit ID.

## 60. Push Changes from a Cloned Repository

```
git push origin master
```

Uploads local commits to the remote repository.

## 61. Set Upstream While Pushing

```
git push -u origin master
```

Connects the local branch to the remote branch.

After setting upstream:

```
git push
git pull
```

## 62. Understand Local and Remote Branches

```
# Local branches
git branch

# Remote branches
git branch -r

# All branches
git branch -a
```

- Local branch: Exists in your local repository.
- Remote-tracking branch: Represents the last fetched state of a remote branch.
- Remote branch: Exists on the remote repository.

## 63. View Commit History with Branch Information

```
git log --oneline --all --graph
```

Shows commits and branch relationships.

## 64. Check the Latest Commit

```
git log -1
```

Shows the latest commit details.

## 65. Compare Local and Remote Commits

```
# Fetch latest remote information
git fetch origin

# Commits available locally but not remotely
git log origin/master..master --oneline

# Commits available remotely but not locally
git log master..origin/master --oneline
```

## 66. Resolve Push Rejection

```
# Fetch remote changes
git fetch origin

# Inspect commit history
git log --oneline --all --graph

# Integrate remote changes
git pull origin master

# Push local changes
git push origin master
```

## 67. Verify Push Results

```
# Check repository status
git status

# View latest commits
git log --oneline -5

# View local and remote branches
git branch -vv
```

## 68. Clone and Practice with Multiple Repositories

```
# Clone a repository
git clone <repository-url>

# Clone with a custom directory
git clone <repository-url> new-project

# Enter the cloned repository
cd new-project

# Check status
git status

# View history
git log --oneline
```

## 69. Common Clone and Push Commands

| Command                           | Purpose                        |
| --------------------------------- | ------------------------------ |
| `git clone <url>`                 | Clone a repository             |
| `git remote -v`                   | View remote URLs               |
| `git fetch`                       | Download remote updates        |
| `git pull`                        | Download and integrate changes |
| `git push`                        | Upload local commits           |
| `git push -u origin master`       | Push and set upstream          |
| `git remote remove origin`        | Remove remote connection       |
| `git remote set-url origin <url>` | Change remote URL              |
