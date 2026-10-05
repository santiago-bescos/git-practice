# Git Notes

## Git vs GitHub

- **Git** = version control system running locally on my computer.
- **GitHub** = online platform where Git repositories can be hosted.
- A repository can exist locally without being on GitHub.

---

## Basic setup

### Check Git version

```bash
git --version
```

### Configure Git identity

```bash
git config --global user.name "Santiago Bescós"
git config --global user.email "my@email.com"
```

`--global` applies the configuration to Git on this computer.

Check configuration:

```bash
git config --global --list
```

---

## Creating a repository

### Initialise a repository

```bash
git init
```

Turns the current folder into a Git repository.

Git creates a hidden `.git/` folder containing the information needed to track the repository's history.

`git init` does NOT upload anything to GitHub.

---

## Checking the repository

### Status

```bash
git status
```

Shows the current state of the repository:

- Current branch
- Commits
- Untracked files
- Modified files
- Staged files
- Whether the working tree is clean

This is basically the "what is going on?" command.

### Difference

```bash
git diff
```

Shows changes made to files since the last commit that have not been staged.

---

## Staging and committing

The basic flow is:

Working files
     |
     | git add
     v
Staging area
     |
     | git commit
     v
Git history

### Add a file to staging

```bash
git add filename
```

Example:

```bash
git add README.md
```

### Add everything

```bash
git add .
```

Stages all changes in the current directory.

### Commit

```bash
git commit -m "Description of changes"
```

- `commit` = record a snapshot of the staged changes
- `-m` = message
- The message describes what the commit contains

Example:

```bash
git commit -m "Add Git notes"
```

A commit is NOT an upload. Commits can be made completely offline.

---

## Branches

A branch represents a line of development.

The main branch is conventionally called:

```text
main
```

Rename the current branch:

```bash
git branch -M main
```

Branches can be used to develop/test changes separately from the main line of development.

---

## Remotes

A **remote** is another copy/location of the Git repository, usually hosted online.

### Add a remote

```bash
git remote add origin URL
```

Example:

```bash
git remote add origin https://github.com/username/repository.git
```

- `remote` = work with remote repositories
- `add` = add a remote
- `origin` = conventional name for the main remote
- URL = location of the remote repository

`origin` is just a name. It could technically be called something else.

### View remotes

```bash
git remote -v
```

`-v` = verbose

Shows the URLs associated with the remote.

---

## Push

### First push

```bash
git push -u origin main
```

- `push` = send local commits to the remote
- `-u` = set the upstream/tracking relationship
- `origin` = remote repository
- `main` = branch being pushed

After the upstream relationship has been established, usually:

```bash
git push
```

is enough.

---

## Normal Git workflow

Most of the time:

1. Edit files
2. `git status`
3. `git diff`
4. `git add .`
5. `git commit -m "Describe the changes"`
6. `git push`

---

## Useful PowerShell commands

These are not Git commands:

```powershell
mkdir folder-name
```

Creates a new folder.

```powershell
cd folder-name
```

Changes the current directory.

---

## Current Git mental model

Working directory
       |
       | git add
       v
Staging area
       |
       | git commit
       v
Local Git history
       |
       | git push
       v
GitHub

Git tracks the project locally.

GitHub hosts an online copy of the repository.