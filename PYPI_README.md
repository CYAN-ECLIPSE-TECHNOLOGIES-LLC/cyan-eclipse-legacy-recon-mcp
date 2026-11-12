# cyan-eclipse-legacy-recon

mcp-name: io.github.CYAN-ECLIPSE-TECHNOLOGIES-LLC/legacy-recon

**What this is:** the MCP server for **Eclipse Legacy Recon** — point
an agent at a local codebase and get a narrowed-scope architecture
map, a dependency/EOL risk list, and modernization-estimate inputs,
in one scoped report. Read-only by design: target code is never
executed, imported, or shelled out to, and there are no network
calls. Within the claim scope in `CLAIM-SCOPE.md`, reported entries
cite the file path plus the manifest line, structural fact, or
inference basis they rest on; standing UNKNOWN categories carry
reasons, never a guessed stack. The dependency inventory keeps
DECLARED (manifest), OBSERVED (import statements), and INFERRED
(labeled inference) in separate lists, never blended; OBSERVED is a
scoped positive inventory, not an exhaustive one.

## Honest scope

- **v0.1.0, local, read-only.** MCP over stdio, Python stdlib only.
- The controlling claim boundary is `CLAIM-SCOPE.md` (narrowed
  observed scope, 2026-10-26). No certification is claimed in this
  README beyond what that document states.
- Modernization outputs are **inputs, not an estimate**: LOC by
  language, test presence/ratio, manifest age signals, coupling
  hotspots by fan-in. No effort, cost, or duration figure is
  produced.

## Run it

```console
$ pip install cyan-eclipse-legacy-recon
$ eclipse-legacy-recon    # MCP over stdio, Python stdlib only
```

MCP client config:

```json
{ "mcpServers": { "cyan-eclipse-legacy-recon": { "command": "uvx", "args": ["--from", "cyan-eclipse-legacy-recon", "eclipse-legacy-recon"] } } }
```

## Tools (4)

`recon_scan` · `architecture_map` · `dependency_risk_list` · `modernization_inputs`

All take `path` (required string) and optional `max_files` (integer).

Powered by Cyan Eclipse Technologies LLC (cetech.ai) — a Veteran-Owned
Small Business. MIT licensed.
