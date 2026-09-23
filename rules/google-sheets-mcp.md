# Google Sheets MCP

The `gsheets` MCP server is registered at user scope, so it loads in every project.
It reads and writes Google Sheets through a Google Cloud **service account**.

## The credential changes per project

The server reads two environment variables:

| Variable | Meaning |
|---|---|
| `GOOGLE_PROJECT_ID` | The Google Cloud project the service account belongs to |
| `GOOGLE_APPLICATION_CREDENTIALS` | Absolute path to its JSON key file |

The user-scope registration supplies a default. A project that needs a different
key overrides both in its own `.claude/settings.json`:

```json
{
  "env": {
    "GOOGLE_PROJECT_ID": "<gcp-project-id>",
    "GOOGLE_APPLICATION_CREDENTIALS": "C:/Users/<you>/.secrets/<name>.json"
  }
}
```

## Registration

Install the server rather than running it through `npx`. A cold `npx` download exceeds
Claude Code's 30s MCP startup budget and the connection times out:

```bash
npm install -g mcp-gsheets@<version>
claude mcp add --scope user gsheets \
  -e GOOGLE_PROJECT_ID=<id> \
  -e GOOGLE_APPLICATION_CREDENTIALS=<path> \
  -- node <npm-root-g>/mcp-gsheets/dist/index.js
```

Pin the version. This package holds a credential, so it should not float on `@latest`.

## Getting a key

1. Google Cloud console → pick or create a project → enable the **Google Sheets API**.
2. **IAM & Admin → Service Accounts → Create.** Grant it **no project roles**.
3. **Keys → Add key → Create new key → JSON.** Save it outside any repo.
4. Open the target sheet → **Share** → paste the service account's `client_email` → **Editor**.

Step 4 is the entire grant. A service account reaches only the files explicitly shared
with it, which is why step 2 grants no roles — a project-level role is the one thing that
would let it see more than intended. Revoking is removing that one share.

## Working rules

- Never commit a key or paste its contents into a repo file.
- Read the target range before writing it. A write replaces without confirming.
- Never widen a write past the range you were asked to change.
- A sheet's locale sets its formula syntax. Check it before writing formulas.
