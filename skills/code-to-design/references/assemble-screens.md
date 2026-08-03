# Assembling screens & components

Loaded when building a screen, section, or component **from the file's existing design system** — the
common case. Recognise the source UI's pattern, then assemble it from matching components and bound
tokens. Work in small steps and check each; don't emit a huge tree blind. Binding/layout/sizing
mechanics live in `write-rules.md`.

## Frame and auto-layout first

`create_frame` for the container, then `set_auto_layout` (`HORIZONTAL` / `VERTICAL` / `GRID`) with the
padding / itemSpacing / alignment the source layout implies. Children that stack, sit side-by-side, or
are gapped belong in auto-layout — only the top-level container is placed with absolute `x`/`y`.

## Instance components — don't rebuild internals

Match the source pattern (a card, a list row, a nav, a button) to an existing component from
`scan_components` / `get_local_components`, and **`create_instance`** it:

- `componentId` for a local component, `componentKey` for a published / library one.
- Set its variant / properties on the instance rather than rebuilding the component's internals:
  `get_component_api` (on the component or the instance) returns the full property contract — each
  property's type and its **verbatim key** (VARIANT by bare name, BOOLEAN/TEXT/INSTANCE_SWAP suffixed
  `#id`) — then `set_instance_properties` (`instanceId`, `properties`) sets them with those exact keys,
  e.g. `{ "Size": "Large", "Disabled#1:2": true, "Label#2:0": "Sign in" }`. Unspecified props keep
  their value; an INSTANCE_SWAP value is the target component node id.
- One instance per occurrence, each with its own props — the write-side mirror of codegen wiring
  `instances[].props`.

Only build a piece from primitives when no component matches (then consider whether it should _become_
a component — see `author-design-system.md`).

### Icons, logos & images

Same reuse-first order, mirroring codegen's asset path: an icon that already has a component →
`create_instance` it; a **logo / brand mark / one-off or not-yet-in-DS vector** → `import_svg` with
the asset's raw SVG markup (a real editable vector, never a grey box or a blurry raster); a
**raster photo** → `import_image`. Never `import_svg` an icon that exists as a component — that
breaks reuse. Recolour a single-colour vector at the usage site with `set_fills` /
`bind_variable_to_paint`, the same way codegen colours an icon on use.

## Text

`create_text` / `set_text` for content, then `set_text_properties` to set the real font (a new TEXT
node defaults to Inter, not the system font — see `write-rules.md`). Bind `characters` to a `STRING`
variable when the copy is tokenised.

## Append, then size and fill

Append each child into its auto-layout parent **first**, then `set_layout_props` to fill or hug
(`layoutGrow` / `layoutAlign` — see `write-rules.md`). A child can't fill before it's in a layout.

## Bind tokens for every value

Colour via `bind_variable_to_paint`, scalars (size / padding / gap / radius) via
`bind_variable_to_node`, shared looks via `apply_style_to_node`. Don't hardcode a hex/px the file has
a token for (`write-rules.md` has the three paths).

## Screenshot and fix, step by step

`get_screenshot` the built node, fix discrepancies, re-screenshot — codegen's render-and-diff
discipline, in reverse. Check against the source intent and against objective design health, which
catches problems even when you built from a vague description with no source to compare:

- nothing **clipped or overflowing** (a frame stuck at 100×100, text cut off);
- edges **aligned**, not off by a few px;
- **spacing consistent** — gaps / padding from one scale, not a different number each time;
- a clear **type hierarchy** (heading / body / caption actually differ).

An `empty: true` export means the node rendered nothing (hidden / off-canvas / no visible content) —
check it's appended, visible, and on the canvas.

## Large screens: one section at a time

Build a big screen the way codegen grounds one — a section at a time, verifying each before moving
on, rather than emitting the whole tree blind and screenshotting at the end. Assemble the first
section, screenshot, fix, then the next — errors stay local and cheap to correct.
