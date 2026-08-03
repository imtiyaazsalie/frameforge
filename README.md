<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/imtiyaazsalie/frameforge/HEAD/.github/logo-full-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/imtiyaazsalie/frameforge/HEAD/.github/logo-full-light.svg">
  <img alt="Frameforge" src="https://raw.githubusercontent.com/imtiyaazsalie/frameforge/HEAD/.github/logo-full-light.svg" width="480">
</picture>

A local MCP server + Figma plugin that lets your agent read designs off the canvas — and put new work back on it.

[![npm](https://img.shields.io/npm/v/frameforge-mcp?logo=npm&color=cb3837)](https://www.npmjs.com/package/frameforge-mcp)
[![CI](https://github.com/imtiyaazsalie/frameforge/actions/workflows/ci.yml/badge.svg)](https://github.com/imtiyaazsalie/frameforge/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Glama MCP server](https://glama.ai/mcp/servers/imtiyaazsalie/frameforge/badges/score.svg)](https://glama.ai/mcp/servers/imtiyaazsalie/frameforge)

</div>

## What it does

Frameforge gives an MCP-capable agent (Claude Code, Cursor, Codex, …) two-way access to Figma:

- **Design → code.** Select anything in Figma and ask for code. The agent receives structured design context — layout, typography, variables, components, de-duplicated across repeated instances — and generates against your actual stack, reusing your existing components, tokens, and icons where it can.
- **Code → design.** Describe a screen or paste a spec and the agent builds it on the canvas: frames, text, auto-layout, styles, variables, components.

Everything runs on your machine over a local relay. Figma's free tier is enough — no Dev Mode seat, no paid plan.

## Highlights

- **Reads and writes.** Most Figma integrations stop at export. Frameforge's **112 MCP tools** cover inspection _and_ authoring, so the same agent that implements a design can also create one.
- **Stack-aware output.** Codegen is grounded on your project: it detects the framework and styling system and maps Figma components, tokens, and icons to the ones you already have.
- **Works offline of Figma's paid features.** The plugin talks to the canvas through the public Plugin API, which is available on every plan.
- **Client-agnostic.** Anything that speaks MCP can drive it; several clients can share one plugin at the same time.
- **Scriptable workflows.** The two core workflows ship as installable [agent skills](#agent-skills) you can adopt or fork.

## Architecture

Your MCP client launches `frameforge-mcp` over stdio. The server keeps a WebSocket link to the Frameforge plugin inside Figma and routes tool calls across it:

```text
  Claude Code · Cursor · Codex · any MCP client
                    │  MCP over stdio
                    ▼
          frameforge-mcp          one leader owns the plugin link;
                    │             extra clients join as followers and
                    │             take over if the leader exits
                    │  WebSocket (msgpack) on 127.0.0.1:3055
                    ▼
          Frameforge plugin ── Figma Plugin API ──► your canvas
```

The relay survives dropped sockets and stale leaders; the [security model](#security) gates what can talk to it.

## Getting started

**1. Point your MCP client at the server.** For Claude Code, add to `.mcp.json` (other clients take the same shape):

```json
{
  "mcpServers": {
    "frameforge": {
      "command": "npx",
      "args": ["-y", "frameforge-mcp@latest"]
    }
  }
}
```

**2. Install the plugin.** Until it's on Figma Community, sideload it: download the plugin zip from the [latest release](https://github.com/imtiyaazsalie/frameforge/releases/latest), unzip, then in the Figma desktop app choose **Plugins → Development → Import plugin from manifest…** and select the `manifest.json`.

**3. Connect.** Run **Plugins → Development → Frameforge** in any file. The panel shows **Connected** once it reaches the server; ask your agent to run `ping` to confirm.

**4. (Optional) Add the skills** so your agent picks up the grounded workflows automatically:

```bash
npx skills add imtiyaazsalie/frameforge/skills
```

**5. Use it.** With a frame selected: _"Code this Figma selection as a React component."_ Or the other way: _"Build a pricing section in Figma from this spec."_

## Agent skills

Skills tell your agent when and how to drive Frameforge. The agent loads one automatically when the task matches:

| Skill                                              | What it does                                                                                        |
| :------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| [`design-to-code`](./skills/design-to-code/SKILL.md) | Turn a Figma selection into framework-aware code, grounded on your stack and existing components.   |
| [`code-to-design`](./skills/code-to-design/SKILL.md) | Build a Figma design from code or a description, reusing the file's existing components and styles. |

Install both, or one at a time, with the [`skills`](https://www.skills.sh) CLI:

```bash
npx skills add imtiyaazsalie/frameforge/skills      # both
npx skills add https://github.com/imtiyaazsalie/frameforge/tree/main/skills/design-to-code  # one
```

> [!NOTE]
> Skills only orchestrate — they need the `frameforge-mcp` server connected to do anything.

## Tool surface

The **112 MCP tools** fall into three groups:

- **Read** — selection and document inspection, styles, variables, components, fonts, reactions, motion state, screenshots, original image-fill assets, PDF export, video export of animated frames (MP4 / GIF / WebM).
- **Write** — frames, text, shapes, auto-layout, effects, styles, variables, components and their properties, pages, reactions, Motion animations (keyframes, presets, timelines), plus a `batch` tool for applying many edits at once.
- **Grounding** — `get_design_context` for de-duplicated design context; `component_map` / `token_map` / `icon_map` to join Figma data with your codebase; `design_diff` to see what changed in a design against a saved baseline.

> [!TIP]
> Your MCP client lists the live tool catalog at connect time — treat that as the source of truth.

## Requirements

- An MCP client (Claude Code, Cursor, …).
- Node.js 20.19+ or 22.12+. The server runs as its own process via `npx`, so this is independent of the Node version your project builds with. (Node 18/21 and 22.0–22.11 are not supported.)
- Figma, free tier. The desktop app is required to import the plugin in development.

## Security

The server binds to `127.0.0.1` only, and nothing leaves your machine. Loopback alone is not a boundary — any web page can reach a local port — so the relay checks headers a browser cannot forge: `Host` must name loopback (blocking DNS rebinding) and `Origin` must match the plugin's sandboxed handshake. See [SECURITY.md](./SECURITY.md) for the full threat model and how to report a vulnerability.

Write tools change your Figma file and export tools write to paths the agent chooses, so keep your MCP client's tool-approval controls on — that, not Frameforge, is the review boundary.

## Troubleshooting

<details>
<summary><strong><code>command not found</code>, or the client reports <code>-32000</code> / "Connection closed" at startup.</strong></summary>

MCP clients spawn `command` directly rather than through your shell, so nothing from your shell profile (version-manager hooks, `PATH` additions) is inherited. That is where both errors come from, and it affects any `npx`-launched MCP server, not just this one.

If the client cannot find `npx` at all (common with fnm/nvm/asdf/volta/mise), use the absolute path from `which npx`:

```json
{
  "mcpServers": {
    "frameforge": {
      "command": "/Users/you/.local/share/fnm/node-versions/v24.x.x/installation/bin/npx",
      "args": ["-y", "frameforge-mcp@latest"]
    }
  }
}
```

If `npx` starts but the server dies before the handshake: `@latest` forces a registry round-trip on every launch, which can stall or fail without your shell's npm config. Install the package once and drop the tag:

```bash
pnpm add -D frameforge-mcp   # or: npm i -D frameforge-mcp
```

```json
{
  "mcpServers": {
    "frameforge": {
      "command": "npx",
      "args": ["-y", "frameforge-mcp"]
    }
  }
}
```

Or install globally (`npm i -g frameforge-mcp`) and point `command` at the path from `which frameforge-mcp` — no `npx` at all.

</details>

<details>
<summary><strong>The plugin sits on "Waiting" and never connects.</strong></summary>

The server only runs while your MCP client is open. Confirm the client is running with Frameforge configured (a `ping` helps), that the plugin is open in the same Figma app on the same machine — the relay is local-only — and that no firewall or security tool is blocking loopback.

</details>

<details>
<summary><strong>Do I need a paid Figma plan or Dev Mode?</strong></summary>

No. The plugin uses Figma's public Plugin API, available on the free tier.

</details>

<details>
<summary><strong>Can several agents share one plugin?</strong></summary>

Yes. Multiple servers elect a leader that owns the plugin connection; the rest forward their calls to it and a follower takes over if the leader exits.

</details>

## Contributing

Issues and pull requests are welcome — see [CONTRIBUTING.md](./CONTRIBUTING.md) for setup and workflow, and [AGENTS.md](./AGENTS.md) for architecture and conventions.

## License

[MIT](./LICENSE) © Imtiyaaz Salie.
