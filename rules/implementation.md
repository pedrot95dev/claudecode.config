# Implementation

Applies whenever you implement something. You are the orchestrator and reviewer — delegate the work, don't write it directly.

## Plan
- Invoke the `coding-discipline` skill before planning.
- Break the work into small, independent parts.
- Write the plan/spec to a file so any agent can read it. Track parts as tasks.

## Delegate
- Spawn one Opus subagent per part with a self-contained brief: goal, constraints, files, acceptance criteria. Each brief must instruct the subagent to invoke the `coding-discipline` skill before coding.
- Independent parts in parallel; dependent parts in order.
- Keep each subagent under ~200k tokens by scoping parts small. Do not ask agents to self-compact. If a part grows too large, split it — or have the agent return a progress summary and spawn a fresh agent to continue.
- Subagents return a compact report only: files changed, key decisions, how verified, open issues. No full transcripts.

## Review
- Verify each part against its acceptance criteria and the real code/tests — not the agent's claims.
- If a part is misaligned, never reuse that agent. Spawn a new one with a focused brief listing exactly what to fix.
- Keep your own context lean: retain only the plan and the compact reports.

Goal: minimum context, no hallucination, best possible output.
