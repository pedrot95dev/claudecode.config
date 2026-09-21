# Version Control

Applies to all git/VCS work — committing, branching, opening pull requests, handling PR feedback, and merging.

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

## After a PR is open — comment loop
Once a PR is open, you are the delegator: drive reviewer comments to zero without polling the PR yourself.

1. **Detect** — spawn a **Sonnet** subagent whose only job is to check the PR for new/unaddressed reviewer comments and report back (list them, or report none). Detection is cheap read-only work — keep it off the delegator's context.
2. **Delegate the fix** — once the subagent returns:
   - If it reports new comments → address them: valid comments get a fix implemented and pushed; false positives get a reply with the reasoning for why no change is needed.
   - If it reports none → exit the loop.
3. Repeat from step 1 (a fresh Sonnet subagent each round) until a detection round finds no unaddressed comments.

When the build is green **and** every comment has been addressed, let the user know.

## Merging a PR
- Merge **only** when the user explicitly asks.
- Before merging, check that no build is running on the target branch. After merging, watch the resulting pipeline to completion and report the result; if it fails, analyze and surface the failure instead of leaving it.
