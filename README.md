# Qodo for Cursor

Coding rules, local review, and pull request finding resolution for the Cursor agent.

Qodo retired its IDE extension on November 1, 2026. This plugin is the install path that replaced it: the same open-source Agentic Toolbox skills Qodo ships for other coding agents, a Cursor rule, and a connection to Qodo's MCP server. It does not restore the old sidebar, completions, or commit-message generator.

[JovianX](https://github.com/JovianX) maintains this package. Qodo does not publish it.

## Install

From Customize, install **Qodo** once it is listed on the Cursor Marketplace.

To load this repository before it is listed:

```bash
mkdir -p ~/.cursor/plugins/local
rm -rf ~/.cursor/plugins/local/qodo
rsync -a --exclude .git ./ ~/.cursor/plugins/local/qodo/
```

Reload the window. On Enterprise, an admin must allow local plugin imports. That setting is off by default.

## Configure

1. Create a personal API key in the [Qodo portal](https://app.qodo.ai). Using the skills requires a Qodo account. A workspace admin controls Agentic Toolbox access.
2. In Customize, open this plugin and set **Qodo API key**.
3. For Qodo Cloud, leave **Qodo MCP server URL** at `https://sdk.qodo.ai/v1/tools/mcp/`. The trailing slash is required. Single-tenant and on-premises workspaces use the URL shown in the Qodo portal.
4. Reload the window. The server is named `plugin-qodo-qodo-managed-tools`.

Cursor stores the key in plugin configuration. This repository does not contain it.

Rule search goes through that MCP server. Local review uses the `qodo` CLI, because Qodo's review API cannot read the working tree. If `qodo` is not on your PATH, run `/qodo-setup` once. The CLI must be version 2.0.0 or newer.

## Skills

| Skill | When to use it |
| --- | --- |
| `/qodo-get-rules` | Before writing or editing code. The included rule requests this and reuses rules already loaded for the same task. |
| `/qodo-review` | At a substantive milestone, and again before handing work off. |
| `/qodo-review-resolver` | When Qodo has already posted findings on a pull request. |
| `/qodo-codebase-wisdom` | When the question is how this codebase fits together. |
| `/qodo-review-notes` | When publishing or refreshing review notes on an existing commit. |
| `/qodo-manage-standards` | When changing the organization's Review Standards. |
| `/qodo-setup` | When the CLI is missing or Qodo is not signed in. |

## Provenance

The files in `skills/` are copied from [qodo-ai/qodo-skills](https://github.com/qodo-ai/qodo-skills) at `9af23a9cb380d54d3d4fee667a9e0e4c9ce809cb`. Copyright 2025 Qodo Team, MIT. See `NOTICE` and `licenses/qodo-skills/LICENSE`.

The Cursor packaging in this repository is also MIT. See `LICENSE`.
