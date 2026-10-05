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

---

## `.gitignore`

`.gitignore` is a file that tells Git which files and folders it should **not track**.

This is useful for files that are:

- Automatically generated
- Temporary
- Specific to my computer
- Large/unnecessary
- Sensitive (e.g. passwords or API keys)

Example Python `.gitignore`:

```gitignore
# Python
__pycache__/
*.pyc

# Virtual environments
.venv/
venv/

# Jupyter
.ipynb_checkpoints/

# Environment variables / secrets
.env
```

### Basic `.gitignore` syntax

```gitignore
*.pyc
```

Ignore all files ending in `.pyc`.

```gitignore
__pycache__/
```

Ignore the `__pycache__` directory.

```gitignore
.venv/
```

Ignore the `.venv` directory.

```gitignore
.env
```

Ignore a file called `.env`.

The `/` after a name indicates a directory.



To add stuff all at once:

Set-Content → replace contents
Add-Content → append contents

ex: @(
    "new line"
    "another new line"
) | Add-Content .gitignore


### Important

`.gitignore` does **not** delete files.

It tells Git not to track files matching those patterns.

Also, `.gitignore` itself should normally be committed to the repository so that Git knows what to ignore when the project is used on another computer.

---

## Creating/editing `.gitignore` from PowerShell

Create an empty file:

```powershell
New-Item .gitignore -ItemType File
```

Append a line:

```powershell
"*.pyc" >> .gitignore
```

`>>` means **append to the file**.

`>` would overwrite the file.

Read the file:

```powershell
cat .gitignore
```

For normal projects, editing `.gitignore` directly in VS Code is usually easier.

---

## Testing `.gitignore`

If `.gitignore` contains:

```gitignore
.venv/
```

then creating:

```powershell
mkdir .venv
```

should result in Git ignoring the folder.

Check with:

```powershell
git status
```

The `.venv` directory should not appear as an untracked file.

---

## Line endings

On Windows, Git may show a warning such as:

```text
LF will be replaced by CRLF
```

This refers to different styles of line endings:

- `LF` = commonly used on Linux/macOS
- `CRLF` = commonly used on Windows

This is normally just a warning and does not mean that the Git command failed.


## Useful Commands for terminal 

ls       → list files
cd       → change directory
cd ..    → go up one directory
mkdir    → make directory
mv       → move/rename
ren      → rename
cat      → show file contents
pwd      → show current location
ni       → new item (touch in linux)