# Git

## Version Control System (VCS)

A **Version Control System (VCS)** helps developers track and manage changes to code over time. It enables collaboration, rollback to previous versions, and maintains the complete history of a project.

There are two main types of VCS:

### Centralized vs Distributed VCS

|Feature|Centralized VCS (CVCS)|Distributed VCS (DVCS)|
|---|---|---|
|**Architecture**|Single central repository|Each developer has a full copy of the repository|
|**Examples**|SVN, Perforce|Git, Mercurial|
|**Working Model**|Developers push/pull from a central server|Developers clone the repository, work locally, then push changes|
|**Speed**|Slower (server-dependent)|Faster (most operations are local)|
|**Offline Work**|Limited|Fully possible (local commits and branches)|
|**Collaboration**|Depends on server uptime|Peer-to-peer, more fault-tolerant|
|**Backup & Failure**|Single point of failure|Each clone is a full backup|
|**Branching & Merging**|Harder and slower|Easier and efficient|

---

## Introduction to Git

### What is Git?

Git is a **distributed version control system (DVCS)** that allows developers to track, share, and manage source code efficiently. It enables local work without network dependency and supports branching, merging, and version rollback.

---

### Git Levels: High-Level (Porcelain) vs Low-Level (Plumbing)

- **High-Level (Porcelain)**: User-facing commands (e.g., `git add`, `git commit`, `git push`)
    
- **Low-Level (Plumbing)**: Internal Git operations that manage data objects.
    

> Developers mostly interact with high-level (porcelain) commands.

---

### Key Git Terms

- **Repository (repo):** A directory tracked by Git. It stores all version history in a hidden `.git` folder.
    
- **Commit:** A snapshot of the project at a given time. Each commit is identified by a unique 40-character SHA hash.
    
- **Index (Staging Area):** Temporary area between working directory and commit history where changes are prepared.
    
- **Working Tree:** Actual project files in your directory.
    
- **Squash:** Combine multiple commits into one.
    
- **HEAD:** Pointer to the current commit or branch.
    

```flow
Untracked → Staging Area → Tracked (Committed)
```

---

### Key Facts About Git

1. Git uses a **Directed Acyclic Graph (DAG)** to represent commit history.
    
2. Each commit points to its parent(s).
    
3. Untracked files are not recoverable if deleted.
    
4. Commit frequently; history can be rewritten later if needed.
    
5. Use `man git <command>` for command documentation.
    

---

## Configuring Git

### Basic Setup

- All configuration keys follow the format `<section>.<key>`.
    
- The `--global` flag applies settings across all repositories.
    

#### Set Username and Email

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

#### View Configuration

```bash
git config --list
git config --get <key>
```

#### Unset Configuration

```bash
git config --unset <key>
git config --remove-section <section>
```

#### Config Scopes

- `--local`: Current repository
    
- `--global`: Current user
    
- `--system`: System-wide configuration
    

---

## Basic Git Commands

### Creating a New Repository

```bash
git init
```

> This creates a `.git` folder that stores the entire repository’s history.

To remove version control:

```bash
rm -rf .git
```

---

### Common Commands

- `git add <file>` → Stage file(s) for commit
    
- `git commit -m "message"` → Commit staged changes
    
- `git status` → Show working tree status
    
- `git log` → View commit history
    

---

### Understanding SHAs (Secure Hash Algorithm)

Each commit in Git is represented by a unique **SHA-1 hash**.  
You can refer to a commit using the first few characters of its SHA.

View commit details:

```bash
git cat-file -p <commit-sha>
```

> Git stores complete snapshots (not diffs) of the tracked files at each commit.

**Object Types:**

- **Blob:** File contents
    
- **Tree:** Directory structure
    
- **Commit:** Metadata and pointers
    

---

## Branching, Merging, and Rebasing

### Branching Basics

Branches allow isolated development of features or fixes.

#### Create a Branch

```bash
git branch <branch-name>
```

#### Switch to a Branch

```bash
git checkout <branch-name>
```

#### Create and Switch

```bash
git checkout -b <branch-name>
```

#### View Branches

```bash
git branch
```

#### Delete a Branch

```bash
git branch -d <branch-name>     # Safe delete (if merged)
git branch -D <branch-name>     # Force delete
```

---

### Merging Branches

Merge integrates changes from one branch into another.

```bash
git checkout main
git merge <branch-name>
```

If conflicts occur, Git will pause the merge for manual resolution.

**Merge Base:** The most recent common ancestor between two branches.

---

### Rebasing

Rebase replays commits from one branch onto another, producing a cleaner linear history.

```bash
git checkout feature
git rebase main
```

> Use rebase for private branches; avoid rebasing shared branches to prevent history rewriting issues.

---

### HEAD and Reflog

- **HEAD:** Points to the current commit.
    
- **Reflog:** Records movements of HEAD and branches.
    

```bash
git reflog
```

> Use `reflog` to recover lost commits or branches.

---

## Working with Remote Repositories

### Adding and Viewing Remotes

```bash
git remote add <name> <url>
git remote -v
```

**Common conventions:**

- `origin` → your main remote repository
    
- `upstream` → the original project repository (if you forked)
    

---

### Fetching, Pulling, and Pushing

#### Fetch

Downloads changes from a remote but doesn’t merge them.

```bash
git fetch <remote>
```

#### Pull

Fetch + Merge in one step.

```bash
git pull <remote> <branch>
```

#### Push

Uploads local commits to a remote branch.

```bash
git push <remote> <local-branch>:<remote-branch>
```

Delete a remote branch:

```bash
git push <remote> :<remote-branch>
```

---

## Stashing and Conflict Resolution

### Git Stash

Temporarily saves uncommitted changes and reverts your working directory to the last commit.

```bash
git stash
git stash -m "message"
git stash list
git stash pop           # Apply and remove latest stash
git stash apply <id>    # Apply specific stash
```

> Stashes form a **stack** of temporary work.

---

### Resolving Merge Conflicts

1. Identify conflicting files (`git status`).
    
2. Open each file and fix conflicts manually.
    
3. Mark as resolved:
    
    ```bash
    git add <file>
    git commit
    ```
    

---

## Additional Useful Commands

- `git diff` → View unstaged changes
    
- `git log --oneline --graph --all` → Visualize branch structure
    
- `git reset --hard <commit>` → Reset to a specific commit (discard changes)
    
- `git revert <commit>` → Create a new commit that undoes a previous one
    
- `git clone <url>` → Clone an existing repository
    
- `git tag <tagname>` → Mark specific commits (e.g., release points)
    

---
