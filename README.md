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
/plugin install codex-pr-review@0-to-1-labs
/plugin install claude-code-prompt-optimizer@0-to-1-labs
```

The marketplace name is `0-to-1-labs`. Use it after the `@` for every plugin.
Plugins are cloned over HTTPS, so no SSH key is needed.

## What's in here

The catalog lives in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json).
Each entry has a `name`, a `source`, and a description.

| Plugin | Source | Description |
|--------|--------|-------------|
| `codex-pr-review` | `0-to-1-Labs/codex-pr-review` | PR review via a dual-family pipeline (OpenAI Codex + Claude Opus) with a cross-family verifier and a deterministic lint/typecheck/test floor |
| `claude-code-prompt-optimizer` | `0-to-1-Labs/claude-code-prompt-optimizer` | Wrap a prompt in `<optimize>…</optimize>` to rewrite it into a sharper prompt with the same model your session is running |
| `frontend-design` | `0-to-1-Labs/claude-frontend-design` | Expanded fork of the stock frontend-design skill: distinctive, production-grade UI with a hard accessibility/responsive quality floor |
| `nanobanana` | `0-to-1-Labs/nanobanana` | Generate and edit photorealistic images with perfect text rendering using Nano Banana Pro (Gemini 3 Pro Image) |
| `iac-diagram-generator` | `0-to-1-Labs/iac-diagram-generator` | Generate professional cloud architecture diagrams from IaC (Terraform, CloudFormation, Kubernetes, Docker Compose) using Nano Banana Pro |
| `iac-security-scan` | `0-to-1-Labs/iac-security-scan` | Scan IaC (Terraform, CloudFormation) for security misconfigurations, map findings to NIST 800-53 / FedRAMP controls, and generate remediation IaC |
| `codex-dispatch` | `0-to-1-Labs/codex-dispatch` | Route a prompt to OpenAI Codex via `/codex` and get a synthesized answer back |
| `memex` | `0-to-1-Labs/memex` | Context-aware documentation: a hook that retrieves and injects the most relevant doc sections under a token budget |
| `elevenlabs` | `0-to-1-Labs/elevenlabs` | Text-to-speech, speech-to-text (Scribe v2), and sound effects with the ElevenLabs API; `/say` command plus an auto-triggering skill |

## Adding a plugin

A plugin's `source` can point anywhere — it does **not** need to live in this repo
or even this org:

```jsonc
{
  "plugins": [
    // 1. Any Git repo over HTTPS (any host, owner, or org) — how the current plugins are referenced
    {
      "name": "my-tool",
      "source": { "source": "url", "url": "https://github.com/some-owner/my-tool-plugin.git" }
    },

    // 2. In this repo (the path must start with "./")
    { "name": "in-repo-tool", "source": "./plugins/in-repo-tool" },

    // 3. GitHub shorthand — clones over SSH, so it fails for users without a GitHub SSH key
    {
      "name": "ssh-tool",
      "source": { "source": "github", "repo": "some-owner/ssh-tool" }
    }
  ]
}
```

For in-repo plugins, each plugin directory needs its own
`.claude-plugin/plugin.json`. Commands, agents, skills, and hooks are
auto-discovered from `commands/`, `agents/`, `skills/`, and `hooks/`.

> Note: if a referenced plugin repo is **private**, anyone installing it still
> needs read access to that repo.

## License

This catalog is MIT licensed. See [LICENSE](LICENSE). Each plugin has its own
license in its own repo.
