# Git Cheatsheet

## 1. What is Git?

Git is a free, open-source, distributed version control system (VCS) used to track changes in source code.

### Important Terminology

| Term | Meaning |
|---|---|
| Git | Version control system |
| Repository | Project tracked by Git |
| Commit | Snapshot of changes |
| Branch | Independent line of development |
| HEAD | Pointer to the current commit |
| Staging Area | Area containing changes prepared for commit |
| Remote | Repository hosted on another server |
| Clone | Copying a remote repository locally |
| Merge | Combining changes from different branches |
| Push | Uploading local commits to remote |
| Pull | Fetching and integrating remote changes |
| Fetch | Downloading remote changes without merging |

---

## 2. Git Installation

Check Git version:

```bash
git --version
```

Install Git on Ubuntu:

```bash
sudo apt update
sudo apt install git
```

---

## 3. Git Configuration

Configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Check configuration:

```bash
git config --list
```

Check specific configuration:

```bash
git config user.name
git config user.email
```

Open Git configuration file:

```bash
nano ~/.gitconfig
```

### Configuration Levels

| Level | Meaning |
|---|---|
| `--system` | Applies to all users |
| `--global` | Applies to your user account |
| `--local` | Applies only to the current repository |

---

## 4. Initialize a Repository

Navigate to your project:

```bash
cd project_name
```

Initialize Git:

```bash
git init
```

This creates a hidden `.git` directory containing Git repository information.

Check repository status:

```bash
git status
```

**Important:** `git init` initializes a local repository. It does not create a GitLab or GitHub repository.

---

## 5. Understanding Git's Three Areas

Git primarily works with three areas:

1. Working Directory
2. Staging Area
3. Local Repository

### Git Workflow

```text
       WORKING DIRECTORY
       (New / Modified Files)
                |
                | git add
                v
          STAGING AREA
       (Changes prepared for
             commit)
                |
                | git commit
                v
         LOCAL REPOSITORY
          (Saved Commits)
                |
                | git push
                v
         REMOTE REPOSITORY
             (GitLab)
```

### Understanding the Movement

| Command | Movement |
|---|---|
| `git add` | Working Directory → Staging Area |
| `git restore --staged` | Staging Area → Working Directory |
| `git commit` | Staging Area → Local Repository |
| `git reset --soft HEAD~1` | Local Repository → Staging Area |
| `git reset HEAD~1` | Local Repository → Working Directory |
| `git push` | Local Repository → Remote Repository |

Git does not physically move files between these locations. It tracks their different states.

---

## 6. Git Status

Check the current state of your repository:

```bash
git status
```

Short status:

```bash
git status -s
```

Common status indicators:

| Indicator | Meaning |
|---|---|
| `??` | Untracked file |
| `M` | Modified file |
| `A` | Added file |
| `D` | Deleted file |
| `R` | Renamed file |

---

## 7. Git Add – Staging Files

Add a specific file:

```bash
git add file.py
```

Add multiple files:

```bash
git add file1.py file2.py README.md
```

Add all files in the current directory:

```bash
git add .
```

Add all changes across the repository:

```bash
git add -A
```

Add files matching an extension:

```bash
git add *.py
```

**Difference:**

- `git add .` stages changes under the current directory.
- `git add -A` stages changes across the entire repository.

---

## 8. Unstage and Untrack Files

### A. Unstage a Single File

```bash
git restore --staged file.py
```

Moves the file from staging back to the working directory.

### B. Unstage All Staged Files

```bash
git restore --staged .
```

### C. Alternative Method Using Reset

Unstage a specific file:

```bash
git reset HEAD file.py
```

Unstage all files:

```bash
git reset
```

### D. Remove a File from Git Tracking but Keep It Locally

```bash
git rm --cached file.py
```

Remove multiple files from tracking:

```bash
git rm --cached file1.py file2.py
```

Remove a directory from tracking:

```bash
git rm -r --cached directory_name/
```

### Difference Between These Commands

| Command | Purpose |
|---|---|
| `git restore --staged file.py` | Unstage a file |
| `git reset HEAD file.py` | Unstage a file |
| `git rm --cached file.py` | Stop tracking but retain local file |
| `git rm file.py` | Remove from Git and delete local file |

**Remember:**

- Unstage = Remove from staging area.
- Untrack = Stop Git from tracking a file.
- Delete = Remove the actual file.

---

## 9. Git Commit

Commit staged changes:

```bash
git commit -m "Initial commit"
```

Example:

```bash
git commit -m "Add IPL analytics solutions"
```

View commit history:

```bash
git log
```

Compact commit history:

```bash
git log --oneline
```

Show the latest commit:

```bash
git log -1
```

Show commit details:

```bash
git show
```

### Amend the Previous Commit

Modify the previous commit message:

```bash
git commit --amend -m "Updated commit message"
```

Add newly staged changes to the previous commit:

```bash
git add file.py
git commit --amend --no-edit
```

**Important:** `--amend` modifies the previous commit rather than creating a new commit.

Avoid amending commits already shared with others unless you understand the implications of rewriting history.

---

## 10. Git Reset

Git reset moves the current branch's HEAD pointer to another commit.

### A. Soft Reset

```bash
git reset --soft HEAD~1
```

Removes the latest commit but keeps its changes staged.

Movement:

```text
Local Repository → Staging Area
```

### B. Mixed Reset (Default)

```bash
git reset HEAD~1
```

Or:

```bash
git reset --mixed HEAD~1
```

Removes the latest commit but keeps changes in the working directory.

Movement:

```text
Local Repository → Working Directory
```

### C. Hard Reset

```bash
git reset --hard HEAD~1
```

Removes the latest commit and discards its associated changes from the working tree and staging area.

**WARNING:** This can permanently discard uncommitted work.

### Reset Comparison

| Command | Commit removed? | Changes retained? | Location |
|---|---|---|---|
| `--soft` | Yes | Yes | Staging |
| `--mixed` | Yes | Yes | Working Directory |
| `--hard` | Yes | No | Discarded |

### Understanding HEAD~1

| Expression | Meaning |
|---|---|
| `HEAD` | Current commit |
| `HEAD~1` | One commit before HEAD |
| `HEAD~2` | Two commits before HEAD |
| `HEAD~3` | Three commits before HEAD |

---

## 11. Git Restore

Restore a modified file:

```bash
git restore file.py
```

Restore all modified files:

```bash
git restore .
```

Restore a file from the staging area:

```bash
git restore --staged file.py
```

**Important:** `git restore file.py` discards unstaged modifications and restores the file to its staged version, or its last committed version if it has no staged changes.

---

## 12. Git Branches

A branch is an independent line of development.

List branches:

```bash
git branch
```

Create a new branch:

```bash
git branch feature
```

Switch to another branch:

```bash
git switch feature
```

Create and switch to a new branch:

```bash
git switch -c feature
```

Alternative older syntax:

```bash
git checkout feature
git checkout -b feature
```

Rename current branch:

```bash
git branch -m new_branch_name
```

Delete a branch:

```bash
git branch -d feature
```

Force delete a branch:

```bash
git branch -D feature
```

---

## 13. Git Merge

Merge combines changes from one branch into another.

Example:

You have two branches:

- `main`
- `feature`

Switch to the branch that should receive the changes:

```bash
git switch main
```

Merge the feature branch:

```bash
git merge feature
```

Delete the feature branch after merging:

```bash
git branch -d feature
```

### Merge Conflicts

A merge conflict occurs when Git cannot automatically combine changes.

Check conflicting files:

```bash
git status
```

Resolve conflicts manually in the files.

After resolving:

```bash
git add .
git commit
```

---

## 14. Git Remote – GitLab / GitHub

A remote is a reference to a repository hosted on another server.

### A. Add Remote Origin

```bash
git remote add origin <repository_url>
```

Example using SSH:

```bash
git remote add origin git@gitlab.com:username/project.git
```

`origin` is the conventional name given to the remote repository.

### B. Check Remote Repositories

```bash
git remote
```

Show remote URLs:

```bash
git remote -v
```

### C. Change Remote URL

```bash
git remote set-url origin <new_repository_url>
```

Useful when you change the GitLab project URL.

### D. Remove Remote

```bash
git remote remove origin
```

### E. Rename Remote
