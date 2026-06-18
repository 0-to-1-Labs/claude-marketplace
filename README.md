# 0 to 1 Labs — Claude Code Plugin Marketplace

A catalog of Claude Code plugins maintained by 0 to 1 Labs.

## Add this marketplace

In Claude Code:

```
/plugin marketplace add 0-to-1-Labs/claude-marketplace
```

Then browse and install:

```
/plugin                                         # interactive browser
/plugin install codex-pr-review@0to1-labs
/plugin install claude-code-prompt-optimizer@0to1-labs
```

## What's in here

The catalog lives in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json).
Each entry has a `name`, a `source`, and a description.

| Plugin | Source | Description |
|--------|--------|-------------|
| `codex-pr-review` | `johnpsasser/codex-pr-review` | PR review via a dual-family pipeline (OpenAI Codex + Claude Opus) with a cross-family verifier and a deterministic lint/typecheck/test floor |
| `claude-code-prompt-optimizer` | `johnpsasser/claude-code-prompt-optimizer` | Wrap a prompt in `<optimize>…</optimize>` to rewrite it into a sharper prompt before it runs (Claude Opus 4.8) |

## Adding a plugin

A plugin's `source` can point anywhere — it does **not** need to live in this repo
or even this org:

```jsonc
{
  "plugins": [
    // 1. Another GitHub repo (any owner/org) — how the current plugins are referenced
    { "name": "my-tool", "source": "some-owner/my-tool-plugin" },

    // 2. In this repo
    { "name": "in-repo-tool", "source": "./plugins/in-repo-tool" },

    // 3. Self-hosted Git (e.g. GitLab)
    {
      "name": "internal-tool",
      "source": { "source": "git", "url": "https://git.milky.way/0-to-1-labs/internal-tool.git" }
    }
  ]
}
```

For in-repo plugins, each plugin directory needs its own
`.claude-plugin/plugin.json`. Commands, agents, skills, and hooks are
auto-discovered from `commands/`, `agents/`, `skills/`, and `hooks/`.

> Note: if a referenced plugin repo is **private**, anyone installing it still
> needs read access to that repo.
