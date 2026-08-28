# Vestige Codex plugin

Codex CLI marketplace wrapper for [Vestige](https://github.com/samvallad33/vestige) — local-first Rust MCP memory with Causal Backfill.

This repo is a **GitHub plugin marketplace**, not a hosted production service. It launches `vestige-mcp-server@2.3.0` on your machine and exposes three tools: `recall`, `smart_ingest`, `backfill`.

## Install (Codex plugin)

```bash
codex plugin marketplace add samvallad33/vestige-codex-plugin
codex plugin add vestige@vestige-codex-plugin
```

Requires [Codex CLI](https://github.com/openai/codex) and Node.js (`npx`). After install, start a new Codex session.

Direct MCP equivalent (writes `~/.codex/config.toml` `[mcp_servers.vestige]`):

```bash
codex mcp add vestige -- npx -y vestige-mcp-server
```

If `vestige-mcp` is already on `PATH`, GUI / config-file clients should use its **absolute** path, not a bare command name.

## What you get

| Tool | Role |
|---|---|
| `recall` | Retrieve prior decisions, preferences, and related memories. |
| `smart_ingest` | Write memories with duplicate / contradiction handling. |
| `backfill` | Causal Backfill: reach backward from a failure to the older memory that caused it. |

Memories stay in a local SQLite store. Default location is the OS per-user data directory. There is **no** `--project` flag. Isolate a repo with `--data-dir`:

```bash
codex mcp add vestige -- npx -y vestige-mcp-server -- --data-dir /absolute/path/to/.vestige
```

Or set `VESTIGE_DATA_DIR`. `--data-dir` wins over the env var.

## Requirements

- Node.js (for `npx -y vestige-mcp-server@2.3.0`)
- Codex CLI with plugin support
- Prebuilt server binaries in `2.3.0` for macOS (Apple Silicon and Intel), Linux x86_64, and Windows x86_64
- **Ubuntu 22.04 and Debian 12:** wait for `vestige-mcp-server` **v2.4.0**

First launch may download an embedding model (~130MB). Later runs do not need the network.

This wrapper is for **local and synthetic** use. It is not a production hosted memory service.

## Layout

```
.agents/plugins/marketplace.json   Codex marketplace catalog
plugins/vestige/.codex-plugin/plugin.json
plugins/vestige/.mcp.json          launches npx -y vestige-mcp-server@2.3.0
plugins/vestige/skills/vestige/SKILL.md
```

## Official Plugins Directory

`codex plugin marketplace add` is the public GitHub distribution path. Listing in OpenAI's universal ChatGPT/Codex Plugins Directory is a separate review: submit the plugin through the [plugin submission portal](https://developers.openai.com/plugins/build/plugins) ("Publish official public plugins"). That portal step is not required for the install commands above.

## License

MIT for this wrapper. The launched server (`vestige-mcp-server`) is AGPL-3.0; see [samvallad33/vestige](https://github.com/samvallad33/vestige).
