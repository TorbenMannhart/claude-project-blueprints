# Claude Project Blueprints

Blueprints = machine-readable project starter kits that agents fetch (e.g., via GitMCP) and "apply" to the current folder using a Filesystem tool.

## Why
- Repeatable scaffolding (agents + memory + configs)
- Versioned, auditable, easy to improve
- Zero shell: agents write files with Filesystem APIs
- Per-project secrets stay in `.envrc` (direnv)

## How it works
1) A Project Setup agent reads a blueprint JSON (e.g. `blueprints/webapp.json`).
2) It writes files/directories, replacing placeholders like `{{PROJECT_NAME}}`.
3) It seeds the AIM master database (Knowledge Graph MCP).
4) It prints a short checklist (e.g., fill `.envrc`, run `direnv allow`).

## Blueprints
- `webapp.json` – generic web app / monorepo nucleus
- `service.json` – backend service with DB
- `lib.json` – library/package starter (e.g., Node)

## Placeholders
- `{{PROJECT_NAME}}` – human-friendly name
- `{{DB_URL_RO}}` – read-only Postgres URL (optional per blueprint)

## Files written (typical)
- `.aim/memory.jsonl` (with `_aim` safety marker)
- `.gitignore` (appends standard ignores)
- `.envrc` (direnv; secrets here; gitignored)
- `.claude.json` (per-project MCP servers)
- `docs/design.md`, `CLAUDE.md` (starter docs)

## Security
- No secrets in JSON. Agents use `direnv exec . …`
- Tokens/scoped PATs → `.envrc` (ignored)
- Read-only DB creds for Postgres MCP

## Updating a blueprint
Change the JSON/template here → future projects inherit it. Existing repos aren't changed unless re-applied.
