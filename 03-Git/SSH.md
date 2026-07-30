# SSH Authentication

---

## Commands Reference

| Command | Purpose | When I Used It |
|----------|----------|----------------|
| `ssh-keygen -t ed25519` | Generate an SSH key pair | Initial GitHub setup |
| `ls -la ~/.ssh` | List SSH configuration files | Verify key creation |
| `cat ~/.ssh/id_ed25519.pub` | Display public key | Copy key to GitHub |
| `ssh -T git@github.com` | Test GitHub authentication | Verify SSH configuration |
| `code ~/Projects/linux-notes` | Open handbook in VS Code | Edit documentation |
| `git status` | Check repository status | Before every commit |
| `git add .` | Stage all changes | Prepare commit |
| `git commit -m "message"` | Create a snapshot | Save completed work |
| `git push` | Upload commits to GitHub | Publish changes |

# Overview

SSH (Secure Shell) is a secure protocol used to authenticate to remote systems.

Instead of typing your GitHub username and password every time you push code, your computer proves its identity using an SSH key pair.

This is the recommended authentication method for GitHub.

---

# Why it Matters

SSH allows you to:

- Clone repositories
- Push commits
- Pull updates
- Access remote Linux servers
- Connect to home lab machines
- Use VS Code Remote SSH

Without repeatedly entering passwords.

---

# Key Concepts

## Public Key

The key that is shared.

Example:

```
id_ed25519.pub
```

This is uploaded to GitHub.

---

## Private Key

The secret key.

Example:

```
id_ed25519
```

This must NEVER be shared.

Anyone with this file can authenticate as you.

---

## Key Pair

SSH creates two keys:

```
Private Key
        │
        │
        ▼
Public Key
```

They mathematically belong together.

---

# Commands

---

## Generate an SSH key

```bash
ssh-keygen -t ed25519
```

Use case:

Creates a modern ED25519 SSH key pair.

During setup we accepted:

```
~/.ssh/id_ed25519
```

and chose a passphrase.

---

## View your SSH directory

```bash
ls -la ~/.ssh
```

Use case:

Lists every SSH-related file.

Example output:

```
id_ed25519
id_ed25519.pub
known_hosts
```

---

## Display the public key

```bash
cat ~/.ssh/id_ed25519.pub
```

Use case:

Shows the public key so it can be copied into GitHub.

We copied the ENTIRE line beginning with:

```
ssh-ed25519
```

---

## Test the GitHub connection

```bash
ssh -T git@github.com
```

First connection:

```
Are you sure you want to continue connecting?
```

We answered:

```
yes
```

GitHub responded:

```
Hi EMMOFK!
You've successfully authenticated...
```

This confirmed that SSH authentication was working correctly.

---

# Git Commands Used

---

## Clone a repository

```bash
git clone git@github.com:EMMOFK/linux-notes.git
```

Use case:

Downloads a GitHub repository onto your computer.

Creates:

```
linux-notes/
```

---

## Check repository status

```bash
git status
```

Use case:

Shows:

- modified files
- staged files
- untracked files

This is the command you'll run more than any other.

---

## Stage all files

```bash
git add .
```

Use case:

Stages every changed file.

Think of this as selecting which changes should go into the next snapshot.

---

## Create a commit

```bash
git commit -m "Create Linux Engineering Handbook structure"
```

Use case:

Creates a permanent snapshot of your work.

A commit message should describe WHAT changed.

Examples:

```
Update README

Add Docker notes

Fix networking diagram
```

---

## Upload changes

```bash
git push
```

Use case:

Uploads commits to GitHub.

After pushing, your online repository is updated.

---

# Git Workflow

The workflow we followed was:

```
Edit files
        │
        ▼
git status
        │
        ▼
git add .
        │
        ▼
git commit
        │
        ▼
git push
```

This is the standard workflow used by professional software engineers and DevOps engineers.

---

# Repository Organization

We transformed:

```
README.md
```

into:

```
01-Linux-Basics
02-Terminal
03-Git
04-Networking
...
15-Resources
```

This makes the handbook easier to maintain as it grows.

---

# Practical Lab

During this setup I successfully:

✔ Generated an ED25519 SSH key

✔ Uploaded my public key to GitHub

✔ Authenticated using SSH

✔ Created a GitHub repository

✔ Cloned the repository

✔ Edited files

✔ Created commits

✔ Pushed commits

✔ Reorganized the repository into a professional handbook

---

# Troubleshooting

## Repository not found

Cause:

Wrong repository name.

Example:

```
repository-name.git
```

instead of

```
linux-notes.git
```

Solution:

Copy the repository URL directly from GitHub.

---

## Author identity unknown

Error:

```
Please tell me who you are.
```

Solution:

```bash
git config --global user.name "Emmet Fahey Kelly"

git config --global user.email "your@email.com"
```

---

## SSH Authentication

Test using:

```bash
ssh -T git@github.com
```

Successful output:

```
Hi EMMOFK!
You've successfully authenticated...
```

---

# Career Relevance

SSH and Git are used every day by:

- Linux System Administrators
- Network Engineers
- DevOps Engineers
- Cloud Engineers
- Security Engineers
- Software Developers

Understanding this workflow is considered a fundamental engineering skill.

---

# Lessons Learned

- Public keys are safe to share.
- Private keys must never be shared.
- Git records snapshots of work.
- Commits should be small and meaningful.
- Push uploads commits to GitHub.
- SSH is faster and more secure than password authentication.
- Documentation belongs in version control.

---

# Related Topics

- Git Basics
- GitHub
- Linux Commands
- VS Code
- Fish Shell
- Bash