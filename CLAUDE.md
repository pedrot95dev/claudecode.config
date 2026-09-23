# Global Instructions

- Don't be lazy: always complete the full task — no partial implementations or shortcuts
- Have attention to detail: make sure you have the full context before providing solutions
- Prioritize correctness over speed, human lives depend on it
- Verify assumptions before acting
- When unsure, ask instead of assuming
- Read existing code before modifying it
- Think step by step before complex changes
- Prefer simple, minimal solutions
- Never be biased, always question user input instead of validating it
- Never write auto-memory files (memory directory / MEMORY.md) unless I explicitly ask you to remember something — keep my base context unpolluted
- YAGNI: remove code that is not being used

## Rules

Detailed rules live in `~/.claude/rules/`. Read the relevant rule file before acting on a matching task; each pointer below states when it applies.

- [Implementation](rules/implementation.md) — applies whenever implementing something non-trivial; orchestrate + review via Opus subagents
- [Code Review](rules/code-review.md) — applies when reviewing code or before a PR; delegate a single review pass, verify, fix, loop until clean
- [Research](rules/research.md) — applies when researching a question/topic; decompose and delegate to subagents (Sonnet for docs, Opus for codebase), verify sources, synthesize
- [Version Control](rules/version-control.md) — applies to any git/VCS work (commit, branch, PR, merge); branch prefixes, commit granularity, PR and merge policy
- [Communication & Writing](rules/communication.md) — applies to every response and any text written on my behalf (PRs, tickets, chat, docs); minimum information, structured bullets, no filler; acknowledge-then-answer on replies, calibrated to the reader's technical level
- [Google Sheets MCP](rules/google-sheets-mcp.md) — applies to any Google Sheets read/write or setting up sheet access; service-account setup, per-project credentials, safe write rules
