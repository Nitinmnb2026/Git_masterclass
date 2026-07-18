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
- Deep dive: `git fetch`
- Deep dive: `git diff`
- Fetch vs Pull comparison

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

## Deep dive: git fetch

What `git fetch` does:

- `git fetch` contacts the remote repository and downloads any commits, branches, tags, or other references that are missing locally, but it does not modify your working directory or current branch. It updates the remote-tracking branches (e.g., `origin/main`).

Why use it:

- Safe: since it does not change your working files or current branch, it is a good way to see what changed on the remote before integrating those changes into your local branches.
- Inspect-only workflow: after `git fetch` you can run `git log origin/main..main` or `git diff origin/main..main` to inspect differences and decide how to integrate.

Common forms and examples:

- Fetch default remote:

  git fetch

- Fetch a specific remote and branch (updates `origin/feature`):

  git fetch origin feature-branch

- Fetch and prune deleted branches on the remote (remove stale remote-tracking branches):

  git fetch --prune

- Fetch all remotes and tags:

  git fetch --all --tags

How to use the result:

- See what changed on `origin/main` since your last fetch:

  git log --oneline main..origin/main

- Inspect code differences (non-destructive):

  git diff main..origin/main

- Merge remote changes into your branch manually after inspecting:

  git merge origin/main

- Rebase your work on top of the fetched remote branch:

  git rebase origin/main

When not to use it:

- If you want to automatically update your current branch with the remote state in one step, `git fetch` alone is insufficient — you still need to merge or rebase.

## Deep dive: git diff

What `git diff` does:

- `git diff` shows differences between two points in Git. By default (with no arguments) it shows unstaged changes in the working directory compared to the index (staging area). It is a read-only command that presents line-by-line changes.

Common usages and examples:

- Show unstaged changes (working tree vs index):

  git diff

- Show staged changes (index vs HEAD):

  git diff --staged

  or

  git diff --cached

- Compare current branch with remote-tracking branch:

  git diff origin/main..main

  (shows what differs between the remote `origin/main` and your local `main`)

- Compare two commits:

  git diff COMMIT1..COMMIT2

- Show changes for a specific file:

  git diff origin/main..main -- path/to/file

- Show word or color diff for easier reading:

  git diff --color-words

Interpreting the output:

- Lines beginning with `---` and `+++` indicate file paths being compared.
- `@@ -a,b +c,d @@` gives chunk context: lines removed from the left side and added on the right side.
- Lines starting with `-` are removals; lines starting with `+` are additions.

Practical tips:

- Use `git diff --name-only origin/main..main` to get a list of files changed without the line-level output.
- Use `git diff --stat origin/main..main` for a summary (files changed, insertions, deletions).
- Combine `git fetch` and `git diff` to safely examine remote changes before merging:

  git fetch
  git diff --stat origin/main..main

## Fetch vs Pull — quick comparison

| Operation | What it does | Affects local branch? | Typical workflow | When to use |
|---|---:|:---:|---|---|
| git fetch | Downloads commits and updates remote-tracking branches (e.g., `origin/main`) but does NOT modify your working tree or current branch. | No (by itself) | Fetch → inspect (`git log`, `git diff`) → merge or rebase manually | When you want to review remote changes before integrating them; safer for CI or review workflows |
| git pull | Equivalent to `git fetch` followed by an automatic `git merge` (by default) of the remote-tracking branch into your current branch (or `git rebase` when configured). | Yes — updates current branch (merge or rebase) | Pull (fetch+merge) to quickly bring your branch up to date with remote | When you want a one-step update and are ready to integrate remote changes immediately |

Notes and caveats:

- Because `git pull` performs a merge (or rebase) automatically, it can create merge commits or cause conflicts right in your working tree. If you prefer to resolve and review first, use `git fetch` then `git merge` or `git rebase`.

- You can configure pull to use rebase by default:

  git config --global pull.rebase true

  or per-repo:

  git config pull.rebase true

- Example: review-first workflow

  git fetch origin
  git log --oneline main..origin/main
  git diff --stat main..origin/main
  # If OK:
  git merge origin/main

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

