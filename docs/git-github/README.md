# Git & GitHub

Git is the version history for a project. GitHub is the place where that history can be shared, reviewed, automated, and published.

## First principles

- A **repository** contains the project and its history.
- A **commit** records a coherent change.
- A **branch** gives a change its own line of development.
- A **pull request** makes a change reviewable before it becomes part of the default branch.
- A `.gitignore` keeps generated files, local environments, and secrets out of version control.

## Start a repository

```bash
git init
git status
git add README.md
git commit -m "Initial project setup"
```

## Daily loop

```bash
git status
git add path/to/changed-file.md
git commit -m "Add a focused change"
git log --oneline --decorate -5
```

Keep commits small enough to explain in one sentence. A commit should leave the project in a usable state.

## Navigating github.com

A repository's page on github.com has the same layout everywhere:

- **Code tab** — file browser for the repo. The branch dropdown (top left of the file list) switches which branch you're viewing. The green **Code** button gives clone URLs (HTTPS/SSH) and a download-ZIP option.
- **Commit history** — click the commit count above the file list (or `<repo-url>/commits/main`) to see every commit, each linking to its diff.
- **Issues tab** — bug reports and task tracking, not code. Each issue has a number (`#12`), a status (open/closed), labels, and a comment thread.
- **Pull requests tab** — proposed changes waiting for review. Each PR shows a **Files changed** diff, a **Conversation** thread for comments, and merge status checks. The **Merge pull request** button (green, enabled once checks pass and conflicts are resolved) merges the branch into the target.
- **Actions tab** — run history for GitHub Actions workflows: green check = passed, red X = failed, yellow dot = in progress. Click a run to see logs per step.
- **Settings tab** (repo owners only) — branch protection rules, collaborators, Pages source, secrets.
- **Star / Watch / Fork buttons** (top right) — star bookmarks a repo, watch subscribes to notifications, fork makes your own copy under your account to propose changes without write access to the original.
- **Raw button** on any file view — the file's plain-text content, useful for `curl`-ing a file directly.

Typing `t` on a repo page opens a fuzzy file finder; pressing `.` opens the repo in a browser-based VS Code editor (github.dev).

## Terminology

| Term | Meaning |
|---|---|
| Repository (repo) | A project's files plus its full history. |
| Clone | A local copy of a repository, linked to its remote. |
| Fork | A copy of someone else's repository under your own account. |
| Remote | A named pointer to a hosted copy of the repo (`origin` by default). |
| `origin` | The conventional name for the remote you cloned from or pushed to. |
| `main` (or `master`) | The default, usually deployable, branch. |
| Branch | A separate line of commits, isolated from `main` until merged. |
| Commit | A saved, described snapshot of changes. |
| Commit hash | The unique ID (e.g. `ae3a854`) identifying a commit. |
| `HEAD` | Pointer to the commit currently checked out. |
| Staging area (index) | Changes marked with `git add`, waiting to be committed. |
| Working tree | The files on disk, including uncommitted changes. |
| Push | Send local commits to a remote. |
| Pull | Fetch and merge a remote's commits into the current branch. |
| Fetch | Download a remote's commits without merging them. |
| Merge | Combine one branch's history into another. |
| Rebase | Replay one branch's commits on top of another, producing linear history. |
| Merge conflict | Two changes to the same lines that Git cannot combine automatically. |
| Pull request (PR) | A request to merge one branch into another, opened for review on GitHub. |
| Issue | A tracked bug report, question, or task, not tied to a specific commit. |
| Fast-forward | A merge where the target branch simply advances, no new merge commit needed. |
| Tag | A fixed, named pointer to a specific commit, usually a release. |
| `.gitignore` | A file listing paths Git should never track. |
| Upstream | The original repository a fork was created from. |
| GitHub Actions | GitHub's automation system for running workflows on repo events. |
| Workflow / job / step | An Actions pipeline (workflow), made of jobs, made of steps. |
| GitHub Pages | Static-site hosting built into GitHub, serving files from a repo/branch. |
| Collaborator | An account granted write access to a repository. |
| Review / approve | A collaborator's comment or sign-off on a pull request. |
| Squash merge | Merge a PR's commits into a single commit on the target branch. |

## Remote repositories

A remote is a copy of the repository hosted elsewhere, usually GitHub. Clone an existing project to get a local copy with the remote already configured:

```bash
git clone https://github.com/EthanBrown-Economics/econ-toolkit.git
cd econ-toolkit
```

To connect a local repository to a new GitHub remote instead:

```bash
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

`git push` sends local commits to the remote. `git pull` fetches and merges the remote's changes into the current branch. Run `git pull` before starting new work so local history does not drift from the shared history.

## Branches and pull requests

A branch isolates work so `main` stays deployable. Create one per change:

```bash
git checkout -b add-panel-data-example
```

Commit on the branch as usual, then push it and open a pull request:

```bash
git push -u origin add-panel-data-example
```

On GitHub, "Compare & pull request" turns that branch into a PR against `main`. A PR shows the diff, invites review comments, and runs any configured checks (see GitHub Actions below) before the branch merges. Delete the branch after merging to keep the branch list readable:

```bash
git branch -d add-panel-data-example
git push origin --delete add-panel-data-example
```

## Resolving merge conflicts

A conflict happens when Git cannot automatically combine two changes to the same lines. Pulling or merging will report which files conflict:

```bash
git pull
# CONFLICT (content): Merge conflict in docs/r/README.md
```

Open the file and look for conflict markers:

```
<<<<<<< HEAD
your local version
=======
the incoming version
>>>>>>> branch-name
```

Edit the file to keep the correct content, remove the markers, then stage and commit:

```bash
git add docs/r/README.md
git commit
```

Small, frequent commits and pulling before starting new work are the best ways to avoid conflicts in the first place.

## `.gitignore` for research projects

Keep generated output, local environments, and raw data out of version control. A typical research `.gitignore`:

```
.venv/
__pycache__/
*.pyc
.Rhistory
.RData
*.log
data/raw/
outputs/
.DS_Store
```

Track code and small reference data; exclude anything regenerable from a script or too large/sensitive to commit. If a file is already tracked, adding it to `.gitignore` will not untrack it — remove it first with `git rm --cached <file>`.

## GitHub Actions and GitHub Pages

GitHub Actions runs workflows — YAML files in `.github/workflows/` — on events like a push or PR. This repository's `.github/workflows/deploy.yml` builds the MkDocs site and publishes it to GitHub Pages on every push to `main`, which is why the site at the top of this README stays in sync with the docs.

A minimal workflow looks like:

```yaml
name: Deploy documentation
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install -r requirements.txt
      - run: mkdocs gh-deploy --force
```

GitHub Pages then serves the built site from the repository, giving the project a URL without separate hosting.

## Reverting and recovering from mistakes

- Undo uncommitted changes to a file: `git checkout -- <file>` (or `git restore <file>` on modern Git).
- Unstage a file without losing changes: `git restore --staged <file>`.
- Fix the most recent commit message or add forgotten changes: `git commit --amend` (only before pushing, or after coordinating with collaborators).
- Undo a commit but keep its changes staged: `git reset --soft HEAD~1`.
- Create a new commit that reverses a specific past commit, safe on shared branches: `git revert <commit-hash>`.
- Recover a deleted branch or lost commit: `git reflog` lists recent HEAD movements, including commits that no longer have a branch pointing to them.

Prefer `git revert` over `git reset` on any branch other people share — reset rewrites history, revert adds to it.
