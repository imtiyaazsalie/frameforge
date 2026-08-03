# CLAUDE.md

**[AGENTS.md](./AGENTS.md)** is the single source of guidance for this repo — architecture, layout, tech stack, commands, conventions, release flow, and gotchas. Read it first. What follows is only what applies when working here through Claude Code.

## Editing and verifying

- This repo **is** a Figma MCP server. The project-scoped `.mcp.json` launches the local build (`packages/mcp/dist/index.mjs`), so after changing `packages/mcp` or `packages/shared` you must `pnpm build` and restart the MCP connection before the `frameforge` tools reflect your change.
- There are no git hooks; CI is the gate. When you edit through Claude Code, the PostToolUse hook (`.claude/hooks/format-on-edit.mjs`) auto-formats and lints the file — don't hand-format.
- The canonical checks before pushing are `pnpm typecheck && pnpm lint && pnpm format:check && pnpm knip && pnpm build && pnpm test` (the same gates CI runs).

## Skills that own dependency upgrades

- The **`mcp-sdk-audit`** skill (`.claude/skills/`) owns `@modelcontextprotocol/sdk` upgrades. The SDK is a _runtime_ dependency — it generates every tool's JSON Schema and negotiates the protocol version — so a release can move what clients see while `tsc` stays green, and no gate in this repo covers that (`test/e2e/` never starts an MCP server; `test/tool-schema.ts` re-derives schemas with `z.toJSONSchema` in parallel). The skill sorts each release by which SDK source files it touched (only the `server/` + `stdio` + zod-compat slice reaches us) and its `probe.mjs` snapshots the live wire contract before and after the bump.
- The **`figma-typings-audit`** skill (`.claude/skills/`) owns `@figma/plugin-typings` upgrades end to end: it diffs the `.d.ts` between the installed and target version (that package ships no changelog), maps the result onto the sandbox handlers, the hand-written Zod mirrors in `shared`, and the tool registry, then bumps and implements what's worth having. It diffs _before_ upgrading — the installed version is the baseline. Reach for it on a Renovate bump PR for that package: a green pipeline does **not** mean the update was absorbed, since `shared` mirrors Figma's shapes with no compile-time coupling to the typings.
