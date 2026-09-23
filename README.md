My personal global Claude Code configuration — the `~/.claude` folder on my machine, under version control.

## What's in here

Two things are tracked:

- **`CLAUDE.md`** — the global instructions Claude Code loads in every session. It stays short and points to the rules below.
- **`rules/`** — one file per kind of task, loaded only when relevant:
  - `implementation.md` — orchestrate implementation via subagents
  - `code-review.md` — single-agent review pass, verify, fix, loop
  - `research.md` — decompose questions and delegate to subagents
  - `version-control.md` — branch prefixes, commit granularity, PR and merge policy
  - `communication.md` — writing style for replies, PRs, tickets, docs
  - `google-sheets-mcp.md` — Google Sheets MCP setup and safe read/write rules

Everything else that lives in `~/.claude` (credentials, session history, caches, plugins, project memory) is **not** tracked. The `.gitignore` works as a whitelist: it ignores everything, then explicitly allows the files above. Nothing gets committed unless it's on that list.

## How it works

This repo *is* the live `~/.claude` directory. There's no copy to keep in sync:

1. Edit `CLAUDE.md` or a rule file.
2. Claude picks it up on the next session.
3. When the change proves useful, commit it. When it doesn't, revert it.

Claude Code also writes its own runtime files into `~/.claude` while running. They're all covered by the whitelist, so `git status` stays clean.

## Want to use this setup?

If you don't have a `~/.claude` folder yet, just clone:

```bash
git clone https://github.com/pedrot95dev/claudecode.config.git ~/.claude
```

If `~/.claude` already exists, init the repo in place:

```bash
cd ~/.claude
git init -b master
git remote add origin https://github.com/pedrot95dev/claudecode.config.git
git fetch origin
git checkout -f -b master origin/master   # careful: replaces your local CLAUDE.md/rules with this repo's
```

## Heads up: this is a Windows setup

I run this on **Windows with PowerShell**, and some rules assume that:

- Windows paths (`C:\...`)
- PowerShell syntax and workarounds

**On macOS or Linux, read through the rules first and adapt or drop the Windows-specific bits.**

## No confidential information

Nothing secret goes in this repo:

- No credentials, tokens, API keys, customer data, or internal secrets — in any tracked file.
- If a rule needs a secret, point to where it lives (vault, env var, untracked local file) — never the value itself.
- Check your diff for sensitive content before every commit.
