# GitHub Repository Creation Guide

This is the process I used to turn `ZeroToHero` into a GitHub repository under my personal account without touching my machine's global work Git config more than necessary.

## Goal

- Keep my work Git identity untouched
- Use my personal GitHub account for this repo only
- Push with SSH using a separate personal key

## 1. Go to the Project Folder

```bash
cd ~/Desktop/Projects/ZeroToHero
```

## 2. Initialize Git

```bash
git init
git branch -m main
```

Notes:

- `git init` creates the local Git repository
- `git branch -m main` renames the default branch from `master` to `main`

## 3. Set Repo-Local Git Identity

This is important because my machine already has a global work identity.

Set identity only for this repo:

```bash
git config user.name "MAKIENAUT"
git config user.email "mcrayescoto@gmail.com"
```

Check it:

```bash
git config --local --list
```

Expected output should include:

```text
user.name=MAKIENAUT
user.email=mcrayescoto@gmail.com
```

This only changes `.git/config` inside this repo.

## 4. Stage and Commit Files

```bash
git add .
git commit -m "Initial commit"
```

## 5. Create the Repository on GitHub

On GitHub:

1. Login to personal account `MAKIENAUT`
2. Click `New repository`
3. Name it `ZeroToHero`
4. Keep it empty
5. Do not initialize with:
   - `README`
   - `.gitignore`
   - `License`

Reason:

- The project already exists locally
- Initializing the remote with extra files can create an unnecessary conflict on first push

## 6. Add the Remote

First I added:

```bash
git remote add origin git@github.com:MAKIENAUT/ZeroToHero.git
```

But this alone is not enough if the machine already uses a work SSH key for GitHub.

## 7. Create a Separate Personal SSH Key

Generate a new key:

```bash
ssh-keygen -t ed25519 -C "mcrayescoto@gmail.com"
```

When prompted for the file path, enter the full path:

```text
/home/wks-002/.ssh/id_ed25519_github_personal
```

Important:

- Do not type `~/.ssh/...` at that prompt
- `ssh-keygen` may not expand `~` there

## 8. Add the Key to ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add /home/wks-002/.ssh/id_ed25519_github_personal
```

## 9. Copy the Public Key

```bash
cat /home/wks-002/.ssh/id_ed25519_github_personal.pub
```

It should look something like this:

```text
ssh-ed25519 AAAA... mcrayescoto@gmail.com
```

Copy the entire line.

## 10. Add the SSH Key to GitHub

On GitHub:

1. Go to `Settings`
2. Open `SSH and GPG keys`
3. Click `New SSH key`
4. Key type: `Authentication Key`
5. Title: something like `wks-002 personal`
6. Paste the full public key
7. Save

## 11. Create SSH Config Alias

Open:

```bash
nano ~/.ssh/config
```

Put this in the file:

```sshconfig
Host github-personal
  HostName github.com
  User git
  IdentityFile /home/wks-002/.ssh/id_ed25519_github_personal
  IdentitiesOnly yes
```

Save and exit.

Then fix permissions:

```bash
chmod 700 /home/wks-002/.ssh
chmod 600 /home/wks-002/.ssh/config
```

Why this matters:

- My machine may already have another GitHub SSH key loaded
- The alias forces this repo to use the personal key only

## 12. Point This Repo to the Personal SSH Alias

```bash
git remote set-url origin git@github-personal:MAKIENAUT/ZeroToHero.git
```

Check it:

```bash
git remote -v
```

Expected:

```text
origin  git@github-personal:MAKIENAUT/ZeroToHero.git (fetch)
origin  git@github-personal:MAKIENAUT/ZeroToHero.git (push)
```

## 13. Test SSH Authentication

```bash
ssh -T git@github-personal
```

Expected result:

```text
Hi MAKIENAUT! You've successfully authenticated, but GitHub does not provide shell access.
```

That means the SSH key is working correctly.

## 14. Push the Repository

```bash
git push -u origin main
```

The `-u` sets the upstream branch so future pushes can be done with:

```bash
git push
```

## 15. Verify Final State

```bash
git status
git remote -v
```

Expected:

- Working tree clean
- Branch tracking `origin/main`
- Remote uses `github-personal`

## Common Problems

### Problem: `Permission denied (publickey)`

Cause:

- Wrong SSH key
- Key not added to GitHub
- Repo still pointing to `git@github.com` instead of `git@github-personal`

Check:

```bash
ssh -T git@github-personal
git remote -v
```

### Problem: `Repository not found`

Cause:

- Repo does not exist on GitHub yet
- Wrong GitHub username
- Wrong repo name

### Problem: commits use work identity

Cause:

- Repo-local `user.name` and `user.email` were not set before commit

Check:

```bash
git config --local --list
```

## Summary

The clean setup is:

- local repo initialized with `git init`
- branch renamed to `main`
- repo-local Git identity set to personal name/email
- separate personal SSH key created
- personal SSH key added to GitHub
- SSH alias `github-personal` used for this repo

This keeps work Git config mostly untouched while letting this repo live under personal GitHub.
