# Git and GitHub Beginner Notes

> A simple guide based on my hands-on Git exercises and learning journey.

## About These Notes

This documentation summarizes what I learned from **Introduction to Git** and **Intermediate Git**. It covers terminal navigation, version control, commits, branches, merge conflicts, and remote repositories.

## Git vs. GitHub

| Git | GitHub |
|---|---|
| A version control system | A cloud platform for Git repositories |
| Tracks changes on a computer | Stores and shares repositories online |
| Manages commits and branches | Supports pull requests, issues, and collaboration |

## 1. Terminal Navigation

| Command | Purpose |
|---|---|
| `pwd` | Show the current working directory |
| `cd folder_name` | Move into a folder |
| `cd ..` | Move to the parent folder |
| `ls` | List files and folders |

```bash
pwd
cd data
ls
```

## 2. Starting a Git Repository

Check the installed Git version:

```bash
git --version
```

Turn the current directory into a Git repository:

```bash
git init
```

`git init` creates a hidden `.git` folder that stores the repository's history and settings.

## 3. Basic Git Workflow

```text
Working directory → Staging area → Commit history
```

```bash
git status
git add .
git commit -m "Describe the changes"
```

### Check the repository

```bash
git status
```

This shows the current branch, untracked files, modified files, staged changes, and whether the working tree is clean.

### Stage changes

Stage one file:

```bash
git add report.md
```

Stage two named files:

```bash
git add report.md data/mental_health_survey.csv
```

Stage all changes in the current directory and its subdirectories:

```bash
git add .
```

### Commit changes

```bash
git commit -m "Update source code"
```

The `-m` flag lets us include the commit message directly in the command.

Correct the latest commit message:

```bash
git commit --amend -m "Correct commit message"
```

## 4. How Git Stores Data

| Object | Meaning |
|---|---|
| Commit | A saved project version with an author, date, and message |
| Tree | The folder and file structure of a commit |
| Blob | The stored content of a file |

## 5. Viewing History

```bash
git log
```

View only the two most recent commits:

```bash
git log -2
```

View the last two commits involving one file:

```bash
git log -2 report.md
```

Show commits made since yesterday:

```bash
git log --since="yesterday"
```

Inspect a specific commit:

```bash
git show commit_hash
```

Press `q` to exit a long history or comparison view.

## 6. Comparing Changes

| Command | What it compares |
|---|---|
| `git diff` | Unstaged changes vs. the latest commit |
| `git diff report.md` | Unstaged changes in one file vs. the latest commit |
| `git diff --staged` | All staged changes vs. the latest commit |
| `git diff --staged report.md` | Staged changes in one file vs. the latest commit |
| `git diff hash_one hash_two` | Two commits using commit hashes |
| `git diff HEAD~1 HEAD~2` | Two previous commits using `HEAD` |
| `git diff branch_one branch_two` | Two branches |

In the output:

- `+` means content was added.
- `-` means content was removed.
- Unmarked lines provide context.

## 7. Unstaging, Restoring, and Reverting

Unstage a file while keeping its changes:

```bash
git restore --staged mental_health_survey.csv
```

Discard a file's unstaged changes and restore its last committed version:

```bash
git restore file_name
```

Safely reverse the latest commit while preserving history:

```bash
git revert HEAD --no-edit
```

## 8. Working With Branches

A branch is an independent line of development. It lets us work on a feature or fix without immediately changing `main`.

List branches:

```bash
git branch
```

The branch marked with `*` is the current branch.

Create and switch to a new branch:

```bash
git checkout -b llm-upgrade
```

Switch to an existing branch:

```bash
git checkout main
```

Rename a branch:

```bash
git branch -m old_name new_name
```

Safely delete a merged branch:

```bash
git branch -d chatbot
```

Force-delete an unmerged branch:

```bash
git branch -D llm-upgrade
```

Uppercase `-D` can remove unmerged work, so use it carefully.

## 9. Merging Branches

To merge `ai-assistant` into `main`:

```bash
git checkout main
git merge ai-assistant
```

> Switch to the branch that should receive the changes, then merge the source branch into it.

## 10. Resolving a Merge Conflict

A merge conflict happens when two branches change the same part of a file and Git cannot decide which version to keep.

Git adds markers like these:

```text
<<<<<<< HEAD
Content from the current branch
=======
Content from the incoming branch
>>>>>>> documentation
```

Resolution steps:

1. Open the conflicted file.
2. Decide which content should remain.
3. Remove `<<<<<<<`, `=======`, and `>>>>>>>`.
4. Save the file.
5. Stage the resolved file.
6. Commit the resolution.

```bash
git add task_list.txt
git commit -m "Resolve merge conflict in task list"
```

## 11. Remote Repositories

A remote is another version of the repository stored elsewhere, such as GitHub.

Clone a repository:

```bash
git clone repository_location
```

List remote names and locations:

```bash
git remote
git remote -v
```

Add a remote:

```bash
git remote add remote_name repository_location
```

## 12. Fetch, Pull, and Push

Download remote information without merging:

```bash
git fetch origin main
```

Download remote changes and merge them into the current branch:

```bash
git pull origin main
```

Upload local commits:

```bash
git push origin branch_name
```

| Command | Simple meaning |
|---|---|
| Fetch | Check and download updates |
| Pull | Download and merge updates |
| Push | Upload my commits |

## 13. Common Errors and Lessons

### Incorrect filename spacing

Incorrect:

```bash
git add report. md
```

Correct:

```bash
git add report.md
```

Spaces separate command arguments, so Git reads `report.` and `md` as different filenames.

### Missing filename

Incomplete:

```bash
git restore --staged
```

Correct:

```bash
git restore --staged mental_health_survey.csv
```

### Commit-message typo

Automated exercises may require an exact message. Check spelling, capitalization, punctuation, and quotation marks before pressing Enter.

### Including instructions in the command

Only enter the code inside the command block. Git may interpret extra instructional words as filenames.

### Control characters

Symbols such as `^C` or `^A` appear when keyboard control shortcuts are pressed. `Ctrl + C` usually cancels the current command.

## 14. Quick Cheat Sheet

```bash
# Setup and status
git --version
git init
git status

# Save changes
git add file_name
git add .
git commit -m "Commit message"

# History and comparison
git log
git log -2
git show commit_hash
git diff
git diff --staged

# Undo safely
git restore --staged file_name
git revert HEAD --no-edit

# Branches
git branch
git checkout -b new_branch
git checkout main
git branch -m old_name new_name
git branch -d branch_name
git merge source_branch

# Remotes
git clone repository_location
git remote -v
git remote add remote_name repository_location
git fetch origin main
git pull origin main
git push origin branch_name
```

## 15. Recommended GitHub Workflow

```bash
# Start from the latest main branch
git checkout main
git pull origin main

# Create a branch for one task
git checkout -b feature/descriptive-name

# Review and save changes
git status
git diff
git add .
git commit -m "Add a clear description of the change"

# Upload the branch
git push origin feature/descriptive-name
```

After pushing, create a **Pull Request** on GitHub so the changes can be reviewed before merging into `main`.

## Key Takeaway

Git becomes easier through consistent practice. A good habit is to check `git status` before and after important actions, use a separate branch for each task, and write clear commit messages.

---

Created as part of my continuous learning journey in Git, GitHub, and Data Engineering.
