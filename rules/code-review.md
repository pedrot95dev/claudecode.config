# Code Review

Applies when reviewing code or before opening a PR. You are the orchestrator — delegate the review, verify, fix, repeat.

## Review
- Spawn 1 Opus subagent to run a code review pass against the local changes.
- It returns a compact report of findings only.

## Verify
- Verify every finding against the real code. Keep only confirmed issues; discard false positives.

## Fix
- Implement the confirmed fixes.

## Loop
- After fixes land, re-run the review with a fresh subagent — never reuse an agent across rounds.
- Repeat until a full round finds no confirmed issues.

Keep only the confirmed issue list and verification evidence; drop stale per-round chatter.
