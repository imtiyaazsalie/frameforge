# Frameforge skills

Agent skills that orchestrate Frameforge's MCP tools. They are model-invoked: your agent loads one
automatically when the task matches the skill's `description`.

> **Prerequisite: the `frameforge-mcp` server.** The skills call Frameforge tools
> (`get_design_context`, `component_map`, …), so install and connect the [MCP server](../packages/mcp)
> first — a skill on its own has no tools to drive.

## The two skills

| Skill                                       | What it does                                                                                                      |
| :------------------------------------------ | :---------------------------------------------------------------------------------------------------------------- |
| [`design-to-code`](./design-to-code/SKILL.md) | Turn a Figma selection into framework-aware code, grounded on the project's stack and existing components/tokens. |
| [`code-to-design`](./code-to-design/SKILL.md)     | Build a Figma design from code or a description, reusing the file's existing components/variables/styles.         |

## Add them with the `skills` CLI

The [`skills`](https://www.skills.sh) CLI pulls straight from this repo into any supported agent
(Claude Code, Cursor, Codex, Copilot, Windsurf, Gemini, …) — no upload or registration:

```bash
# both Frameforge skills
npx skills add imtiyaazsalie/frameforge/skills

# or a single skill
npx skills add https://github.com/imtiyaazsalie/frameforge/tree/main/skills/design-to-code
```
