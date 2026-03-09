Commit all current changes, push to a new branch, create a PR, merge it, and update local main.

1. Run `git status` and `git diff --stat`. If no changes, stop.
2. Run `git log --oneline -5` to match commit style.
3. If on `main`, create a descriptive branch name based on the changes. If already on a feature branch, use it.
4. Stage relevant files (prefer specific files over `git add -A`; never stage `.env` or credentials).
5. Draft a concise conventional commit message and commit.
6. Push with `-u origin <branch>`.
7. Create a PR with `gh pr create` — short title, body with `## Summary` bullets and `## Test plan`.
8. Merge with `gh pr merge --merge --delete-branch`.
9. `git checkout main && git pull`.
10. Report the merged PR URL.
