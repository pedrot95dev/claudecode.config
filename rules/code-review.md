# Code Review

Applies when reviewing code or before opening a PR. You are the orchestrator — delegate the review, aggregate, fix, repeat.

## Review
- Spawn 3 Opus subagents in parallel, each running an independent code review pass against the local changes.
- Each returns a compact report of findings only.

## Aggregate
- Merge findings and dedupe overlaps.
- Verify every finding against the real code. Keep only confirmed issues; discard false positives.

## Fix
- Implement the confirmed fixes.

## Loop
- After fixes land, re-run the review with a fresh set of subagents — never reuse agents across rounds.
- Repeat until a full round finds no confirmed issues.

Keep only the aggregated issue list and verification evidence; drop stale per-round chatter.
