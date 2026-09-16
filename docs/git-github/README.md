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

## Next topics

- Remote repositories and `git clone`
- Branches and pull requests
- Resolving merge conflicts
- `.gitignore` patterns for research projects
- GitHub Actions and GitHub Pages
- Reverting and recovering from mistakes
