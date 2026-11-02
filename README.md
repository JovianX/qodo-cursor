# Qodo for Cursor

A Cursor plugin that brings Qodo's Agentic Toolbox into the agent: coding rules before edits, local review, and resolution of Qodo pull request findings.

This replaces the install path that disappeared when Qodo retired its IDE extension on November 1, 2026. It does not restore that extension's sidebar, completions, or commit messages.

The skills under `skills/` are copied from [qodo-ai/qodo-skills](https://github.com/qodo-ai/qodo-skills) (`9af23a9`). See `NOTICE`.

## What you get

| Skill | Use it for |
| --- | --- |
| `qodo-get-rules` | Load the coding rules that apply to the current task. The plugin rule asks for this before code is written or edited. |
| `qodo-review` | Review local changes at a real milestone and before handoff. |
| `qodo-review-resolver` | Fix Qodo findings already posted on a pull request. |
| `qodo-codebase-wisdom` | Ask how this codebase fits together. |
| `qodo-review-notes` | Publish or refresh review notes on an existing commit. |
| `qodo-manage-standards` | Manage Review Standards from the agent. |
| `qodo-setup` | Install the Qodo CLI, sign in, and check that tools respond. |

Invoke a skill with `/qodo-get-rules`, `/qodo-review`, or the other names in chat.

Rules search uses the Qodo MCP server. Local review prefers the `qodo` CLI, because that command collects the working tree. The review skill's MCP path cannot see your files on its own. Run `/qodo-setup` once if `qodo` is not on your PATH. The CLI requirement is Qodo 2.0.0 or newer.

## Configure

1. Create a personal API key in the [Qodo portal](https://app.qodo.ai).
2. Install this plugin, then set **Qodo API key** in Customize → the Qodo plugin → Configure.
3. Leave **Qodo MCP server URL** at `https://sdk.qodo.ai/v1/tools/mcp/` for Qodo Cloud. The trailing slash is required. Single-tenant and on-premises workspaces use the URL from the Qodo portal.
4. Reload the window. The server shows up as `plugin-qodo-qodo-managed-tools`.

The key stays in Cursor's plugin configuration. It is not stored in this repo.

You need a Qodo account to use the skills. Workspace admins control Agentic Toolbox access.

## Try it locally

Cursor only loads a symlink in `~/.cursor/plugins/local` when the target is inside that folder, so copy the plugin:

```bash
mkdir -p ~/.cursor/plugins/local
rm -rf ~/.cursor/plugins/local/qodo
cp -a . ~/.cursor/plugins/local/qodo
```

Run **Developer: Reload Window**. In Customize, confirm the Qodo skills, the use-qodo rule, and the MCP server. Set the API key, then ask the agent to implement a small change and check that it calls `qodo-get-rules` first.

On Enterprise, an admin has to allow local plugin imports. That setting is off by default.

## Publish

Marketplace plugins have to be in a public git repository and are reviewed by Cursor. Submit the repo at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) when you want it listed. This copy is not an official Qodo release.
