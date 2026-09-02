---
name: vestige
description: Use Vestige local memory. Call recall, smart_ingest, and backfill only. Keep data on this machine.
---

# Vestige memory

Vestige is a local-first Rust MCP memory server. After install, Codex talks to it over MCP. Use only these tools:

| Tool | When to use |
|---|---|
| `recall` | Retrieve memories by meaning or prior decision. |
| `smart_ingest` | Store a decision, preference, fix, or contradiction-aware write. |
| `backfill` | Walk backward from a failure to the earlier memory that caused it (Causal Backfill). |

Do not invent other Vestige tool names. Do not send memories to a remote store. Do not claim this is a production hosted service.

## Local / synthetic only

- Store path is local (OS per-user data dir by default).
- There is no `--project` flag. For a per-project store, relaunch with `--data-dir <path>` or set `VESTIGE_DATA_DIR`.
- Use this for local and synthetic workloads. Do not treat it as a production SLA.

## Hygiene

- Never ingest secrets, API keys, passwords, or tokens.
- On first launch the server may download an embedding model once; later runs are offline.
- This plugin pins `vestige-mcp-server@2.7.1`.
