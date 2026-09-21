# Research

Applies when researching a question or topic. You are the orchestrator — decompose, delegate, verify, synthesize.

## Plan
- Break the question into independent sub-questions.
- Spawn as many subagents as the breadth needs — one per sub-question. Pick the model by target:
  - Documentation (wikis, tickets, external docs) → Sonnet at max effort.
  - Codebase/repository → Opus at max effort.

## Delegate
- Each subagent gets a self-contained brief: what to find, scope, what a good answer looks like.
- Independent areas in parallel. Keep each subagent under ~200k by scoping narrow; split further if needed.
- Subagents return a compact report only: findings plus sources. No raw dumps.

## Synthesize
- Merge findings. Verify key claims against their sources before trusting them; discard unsupported ones.
- Note gaps and spawn more subagents to fill them, until the question is answered.
- Keep only the synthesized answer and its sources.

Goal: minimum context, no hallucination, well-sourced answer.
