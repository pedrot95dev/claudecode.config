# Version Control

Applies to all git/VCS work — committing, branching, opening pull requests, and merging.

## Branches

| Prefix | Use for |
|---|---|
| `feature/` | New functionality |
| `bugfix/` | Bug fixes on a normal release |
| `refactor/` | Code restructuring with no behavior change (moves, renames, cleanups) |
| `hotfix/` | Urgent production fixes |
| `e2e/` | End-to-end test work |
| `testcases/` | Test-case authoring |

## Commits
- Break every commit into the smallest self-contained piece possible — one atomic, connected changeset per commit. Prefer many small, focused commits over a single large one.
- Follow Conventional Commits. The message states what changed and why; omit the "why" only for obvious routine changes.

## Pull requests
- Open a PR **only** when the user explicitly asks for it. Never open one proactively, even when the work looks done.
- The PR description gives reviewers enough context (what + why), not just the commit messages.

## Merging a PR
- Merge **only** when the user explicitly asks.
- Before merging, check that no build is running on the target branch. After merging, watch the resulting pipeline to completion and report the result; if it fails, analyze and surface the failure instead of leaving it.
