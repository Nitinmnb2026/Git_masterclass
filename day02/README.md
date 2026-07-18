# Day02 — Git & SSH Workflow

This README documents the commands and steps used during Day 02 practice (from `day02/day02practice.txt`) and explains what each command does, why it was run, and common pitfalls. Use this as a reference for creating branches, initializing a repository, configuring SSH, and pushing changes to GitHub.

## Table of contents

- Purpose
- Prerequisites
- SSH key setup
- Initialize repository (local -> remote)
- Typical day-02 workflow (create, commit, branch, push)
- Common issues and fixes (seen in practice history)
- Useful commands reference

## Purpose

This folder contains practice notes and examples for basic Git operations and SSH configuration. The commands recorded in `day02practice.txt` capture common steps taken while setting up a repo and pushing work to GitHub.

## Prerequisites

- Git installed
- Access to a terminal (Git Bash / WSL / macOS / Linux)
- A GitHub account

## SSH key setup

Example commands used during practice:

- Generate a new ed25519 key:

  ssh-keygen -t ed25519 -C "your_email@example.com"

- Start the SSH agent:

  eval "$(ssh-agent -s)"

- Add your private key to the agent (Windows path shown in history):

  ssh-add /c/Users/Administrator/.ssh/id_ed25519

- Print the public key to copy it to GitHub:

  cat /c/Users/Administrator/.ssh/id_ed25519.pub

After you copy the public key, add it to GitHub -> Settings -> SSH and GPG keys.

Why: SSH keys let you authenticate with GitHub securely without typing passwords for every push/pull.

## Initialize repository and connect to remote

Typical steps to create a repo locally and push to GitHub for the first time:

1. Initialize the repo (inside project folder):

   git init

2. (Optional) If you accidentally removed .git with `rm -rf .git`, re-run `git init`.

3. Create files, then stage and commit:

   git add .
   git commit -m "chore: initial commit"

4. Add the remote repository (only once):

   git remote add origin git@github.com:YourUser/YourRepo.git

   - Confirm with `git remote -v`.

5. Rename default branch to `main` (if needed):

   git branch -M main

6. Push and set upstream:

   git push -u origin main

Why: `-u` sets the tracking branch so future `git push`/`git pull` are simpler.

## Branching and feature work

- Create and switch to a feature branch:

  git checkout -b feat/day02

- Work, stage, and commit:

  git add .
  git commit -m "feat: add login details"

- When ready, merge into `main` (locally or via PR) and push:

  git checkout main
  git merge feat/day02
  git push

## Useful commands observed in practice

- Inspect commits (compact):

  git log --oneline

- Show status:

  git status

- Fetch remote updates:

  git fetch

- Pull remote changes:

  git pull

- Show differences:

  git diff origin/main..main

- Delete files/folders (be careful):

  rm -rf day02/login.txt

- Remove Git history (dangerous):

  rm -rf .git/

  If you remove `.git/` you lose all local Git metadata. Re-initialize with `git init`, then re-add remote and re-create commits as needed.

## Common issues & tips (from the recorded session)

- Accidentally deleting `.git` happened multiple times in the history. Avoid `rm -rf .git/` unless you intentionally want to discard the repository metadata.

- Renaming branches: use `git branch -M main` to force rename. Don’t repeatedly create conflicting branch names (e.g., `git branch -m master main` vs `git branch -M main`).

- If you get errors pushing, confirm the remote URL and your SSH key is added to GitHub:

  git remote -v
  ssh -T git@github.com

- If `git push` complains about upstream not set, use `git push -u origin main` once to establish tracking.

- To inspect what you are about to push, use `git log --oneline origin/main..main` and `git diff origin/main..main`.

## Suggested safe workflow

1. Create repository on GitHub (or use existing remote URL).
2. Locally: `git init`, create files, `git add .`, `git commit -m "chore: initial commit"`.
3. Link remote: `git remote add origin <ssh-or-https-url>`.
4. Rename branch if you prefer `main`: `git branch -M main`.
5. Push: `git push -u origin main`.
6. Work on feature branches: `git checkout -b feat/your-feature` → commit → open PR → merge.

## .gitignore note

There is a `.gitignore` in this folder that ignores `day02practice.txt`. This file is intentionally excluded from commits in some steps. You can update `.gitignore` if you want to keep or remove local practice logs from version control.

----

If you want, I can:
- Add examples of resolving merge conflicts
- Create a CONTRIBUTING.md with branch naming conventions
- Add a step-by-step checklist to follow before pushing

