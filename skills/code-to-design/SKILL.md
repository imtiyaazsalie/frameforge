---
name: code-to-design
description: Build a Figma design from code or a description — the reverse of design-to-code. Reuses the connected file's existing design system (components, variables, styles) instead of drawing primitives with hardcoded values. Triggers whenever the user wants something created or updated IN Figma from code or a spec — e.g. 'build this in Figma', 'create a Figma design for this', 'push this component/screen to Figma', 'turn this React/Vue into a Figma design', 'recreate this UI in Figma', 'make a Figma version of …', 'design a landing page/screen in Figma' — or whenever a coding artifact (a component, page, or spec) appears alongside a request to author in a connected Figma file. Works for full screens, sections, single components, or design-system assets.
---

# code-to-design

Build a Figma design from code or a description so it looks like it belongs in the file: reuse the
components, variables, and styles that already exist, and create only what's missing. Where
`design-to-code` reads a design into code, this skill applies the same rule — reuse beats regenerate,
reference tokens not literals — in the opposite direction, onto the canvas. This file routes; the
detail sits in [`references/`](./references), one file per step.

Work happens on the **connected** Figma file (the plugin's current session). There is no
fetch-by-URL, so the user must have the target file open. Confirm a plugin is connected (`ping`)
before building.

## Scope

- Creating or updating something in Figma from code or a description: a screen, view,
  modal/dialog/drawer/sidebar/panel, a single component, or a design-system asset.
- Reading a Figma design into code is **not** this skill — that's `design-to-code`.

## Grounding comes first (provider-first)

The write-side mirror of codegen's grounding, and the habit that decides whether the build looks
right: an off-looking build almost always traces to invented values or assumed conventions. Read
this user's actual environment before creating anything; never apply a generic template. Check both
ends:

- **The Figma file** — its existing design system, which you'll reuse and bind to:
  1. **`get_variable_defs`** → the file's variables (colour / spacing / radius / typography) with
     names + values + `hex`. These are the tokens you bind to.
  2. **`scan_components`** / **`get_local_components`** → existing components to **instance** rather
     than rebuild. Match the source UI pattern (a card, a list row, a nav, a button) to a component.
  3. **`get_styles`** → shared paint / text / effect styles to apply.
- **The source you were handed** — when it's code, _which_ stack and styling system (Tailwind /
  Chakra / MUI / CSS modules / vanilla …) and whether it has a config / theme / tokens file. Its
  real values live there — read them from there, don't assume a default.

Then build, tracing every value to a source in priority order: reuse an existing component /
variable / style; else take the exact value from the source's own code — provider-first, resolving
whatever styling system it uses to real px / hex (CSS literally; Tailwind / Chakra / UnoCSS / … via
their config or scale), never eyeballed; only invent from a consistent scale when neither exists.
Full detail and the value-resolution method in `references/write-rules.md`.

## The two build jobs

Both obey the cross-cutting write rules — ground values (design system → source code → scale),
reference tokens (colour via `bind_variable_to_paint`, scalars via `bind_variable_to_node`, shared
looks via `apply_style_to_node`), auto-layout for related children (absolute only for top-level
placement), HUG/FILL/FIXED sizing via `set_layout_props` (let the layout compute sizes — don't
hardcode width/height), and real fonts (a new TEXT node defaults to Inter):
**[`references/write-rules.md`](./references/write-rules.md).**

- **Assemble a screen / component from what exists** (the common case): recognise the UI pattern,
  `create_instance` matching components, bind tokens, build incrementally, screenshot-verify each
  step. → **[`references/assemble-screens.md`](./references/assemble-screens.md).**
- **Author a new design-system asset** (only when grounding found no equivalent): create
  variables/collections, paint/text styles, or components + variant sets, then switch back to the
  reuse path. → **[`references/author-design-system.md`](./references/author-design-system.md).**

## Animation

When the source carries animation — CSS `@keyframes` / `transition`, Framer Motion, GSAP, a
Vue/Svelte transition — author it as Figma **Motion (beta)** on the frame you built instead of
dropping it: `apply_animation_style` (presets from `get_motion_styles`) or
`apply_manual_keyframe_track` per property, `set_timeline_duration` for length. A staggered row is
one atomic `batch` of `apply_animation_style` ops with increasing `config.timelineOffset`, not N
calls. Motion is Figma-Design-only and keyframes attach to a top-level frame's layers, so build the
frame first. → **[`references/motion.md`](./references/motion.md).**

## Screenshot verification

`get_screenshot` the built node, fix discrepancies, re-screenshot — codegen's render-and-diff
discipline, in reverse. Check against the source intent and against objective design health (this
catches problems even when you built from a vague description with no source to compare): nothing
clipped or overflowing, edges aligned, spacing consistent (one scale), a clear type hierarchy. An
`empty: true` export means the node rendered nothing (hidden / off-canvas).

## Standing rules

- **Ground, then build.** Read both the file's design system and the source's stack / styling system
  before creating anything. Every value traces to the design system, the code's own values, or a
  consistent scale — never an invented one.
- **Reuse beats regenerate.** Instance existing components; bind existing variables/styles. Build
  new only what the system lacks, and name/structure it to fit.
- **Tokens, not literals.** Colour via `bind_variable_to_paint`, scalars via
  `bind_variable_to_node`, shared looks via `apply_style_to_node` — never hardcode hex/px when a
  token exists (`get_variable_defs` says which do).
- **Auto-layout for related children**; absolute coordinates only for top-level placement.
- **Incrementally, with screenshots.** Recognise the UI pattern and assemble it from matching
  components rather than reproducing it from primitives; validate as you go.
- **Match the file's conventions** — naming, structure, and the design system's own patterns, the
  way codegen mirrors the project's existing code style.
