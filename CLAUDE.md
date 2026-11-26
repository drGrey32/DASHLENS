# DASHLENS

## Commits

- Make every commit with this author and committer:
  `drGrey32 <74193751+drGrey32@users.noreply.github.com>`
  Before the first commit in a session, run:
  `git config user.name "drGrey32"` and
  `git config user.email "74193751+drGrey32@users.noreply.github.com"`
- Use only the GitHub noreply email above. Do not put a private email address in commits.

## Versions and release branch

- Bump `VERSION` in `index.html` (semantic version: major.minor.patch) with every change that is pushed.
- Work on a branch named `release/<VERSION>`, for example `release/1.6.1`. When the version changes, rename the
  branch to the new version: push the new branch name, then delete the old branch name locally and on GitHub.
- After every push, tell the user which version was pushed.
