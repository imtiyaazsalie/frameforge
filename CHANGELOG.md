# Changelog

## v0.3.1

[compare changes](https://github.com/imtiyaazsalie/frameforge/compare/v0.3.0...v0.3.1)

### 🏡 Chore

- Rename published package to `frameforge-mcp` ([cc0a52d](https://github.com/imtiyaazsalie/frameforge/commit/cc0a52d))

## v0.3.0

[compare changes](https://github.com/imtiyaazsalie/frameforge/compare/v0.2.0...v0.3.0)

### 🚀 Enhancements

- **get_design_context:** Surface mixed-text segments + WRAP cross-axis spacing, omit no-op defaults ([#14](https://github.com/imtiyaazsalie/frameforge/pull/14))
- **set_layout_props:** Set layoutSizingHorizontal/Vertical (HUG/FILL/FIXED) ([#19](https://github.com/imtiyaazsalie/frameforge/pull/19))
- **set_position:** Add set_position tool for exact node placement ([#20](https://github.com/imtiyaazsalie/frameforge/pull/20))
- **ping:** Surface leader/follower version skew (zombie-leader warning) ([#21](https://github.com/imtiyaazsalie/frameforge/pull/21))
- **figma-build:** Ground build values in source code + a sensible scale ([#23](https://github.com/imtiyaazsalie/frameforge/pull/23))
- **get_design_context:** Carry non-text overrides on deduped instances ([#24](https://github.com/imtiyaazsalie/frameforge/pull/24))
- Surface layout grids, dashed strokes & rich-text structure; add set_layout_grids ([#31](https://github.com/imtiyaazsalie/frameforge/pull/31))
- Surface per-run design-system token bindings on mixed TEXT runs ([#32](https://github.com/imtiyaazsalie/frameforge/pull/32))
- Add set_text_range — inline rich-text authoring (setRange* writes) ([#33](https://github.com/imtiyaazsalie/frameforge/pull/33))
- **get_screenshot:** Auto-fit default raster scale & report exported size ([#36](https://github.com/imtiyaazsalie/frameforge/pull/36))
- **read:** Carry paragraph fields & textAutoResize, refuse unknown get_design_context roots, widen get_node budgets ([#35](https://github.com/imtiyaazsalie/frameforge/pull/35))
- **set_text_properties:** Write paragraphSpacing / paragraphIndent ([#38](https://github.com/imtiyaazsalie/frameforge/pull/38))
- **read:** Surface Variable.codeSyntax on resolved tokens & variable defs ([#39](https://github.com/imtiyaazsalie/frameforge/pull/39))
- **set_variable_code_syntax:** Declare a variable's code-side token name ([#40](https://github.com/imtiyaazsalie/frameforge/pull/40))
- **token_map:** Surface per-theme values for multi-mode variable collections ([#42](https://github.com/imtiyaazsalie/frameforge/pull/42))
- **design_diff:** Report per-node design changes against a saved baseline ([#43](https://github.com/imtiyaazsalie/frameforge/pull/43))
- **component-property:** Author boolean/text/instance-swap component properties ([#44](https://github.com/imtiyaazsalie/frameforge/pull/44))
- **layout:** Read and author min/max size bounds (minWidth/maxWidth/minHeight/maxHeight) ([#51](https://github.com/imtiyaazsalie/frameforge/pull/51))
- **set_auto_layout:** Author the wrap cross-axis (counterAxisSpacing / counterAxisAlignContent) ([#52](https://github.com/imtiyaazsalie/frameforge/pull/52))
- **save_image_fills:** Extract original image-fill bytes to disk ([#54](https://github.com/imtiyaazsalie/frameforge/pull/54))
- **get_design_context:** Node-count bail, payload-size net, and below-full note on the public path ([#58](https://github.com/imtiyaazsalie/frameforge/pull/58))
- **get_design_context:** Default to the full codegen view with graceful degradation ([#59](https://github.com/imtiyaazsalie/frameforge/pull/59))
- **get_design_context:** Annotate raw colors with the project's design tokens (value-reverse join) ([#60](https://github.com/imtiyaazsalie/frameforge/pull/60))
- **token_map:** Join a document's shared paint styles as design tokens ([#61](https://github.com/imtiyaazsalie/frameforge/pull/61))
- **get_design_context:** Surface aspect-ratio, sticky, stacking, image filters & Dev Mode annotations ([#62](https://github.com/imtiyaazsalie/frameforge/pull/62))
- **component_map,token_map:** Mapping write-back loop + stale-override degradation ([#64](https://github.com/imtiyaazsalie/frameforge/pull/64))
- **component_map,profile:** Flag near-tie component picks + first-class Solid ([#65](https://github.com/imtiyaazsalie/frameforge/pull/65))
- **component_map,profile:** First-class Angular framework support ([#66](https://github.com/imtiyaazsalie/frameforge/pull/66))
- **styles:** Update_text_style + update_effect_style (write-side parity) ([#67](https://github.com/imtiyaazsalie/frameforge/pull/67))

### 🩹 Fixes

- **server:** Self-terminate on stdin EOF to prevent zombie leaders ([#22](https://github.com/imtiyaazsalie/frameforge/pull/22))
- **plugin:** Connect promptly when the plugin is opened before the MCP server ([#28](https://github.com/imtiyaazsalie/frameforge/pull/28))
- **election:** Don't attach as a follower of a non-Frameforge process on :3055 ([#29](https://github.com/imtiyaazsalie/frameforge/pull/29))
- Strip stray NUL byte in set-text-range, tidy types & dedupe binding logic ([#34](https://github.com/imtiyaazsalie/frameforge/pull/34))
- **batch:** Snapshot every field a write mutates so rollback is all-or-nothing ([#45](https://github.com/imtiyaazsalie/frameforge/pull/45))
- **mcp:** Derive destructiveHint from tool specs, not a hand-kept list ([#46](https://github.com/imtiyaazsalie/frameforge/pull/46))
- **mcp:** Normalize pasted Figma URLs on every canvas-id argument ([#47](https://github.com/imtiyaazsalie/frameforge/pull/47))
- **token_map:** Disambiguate color value-matches shared by several project tokens ([#56](https://github.com/imtiyaazsalie/frameforge/pull/56))
- **prompts:** Sync the distilled prompts with current tools and guard tool names ([#57](https://github.com/imtiyaazsalie/frameforge/pull/57))

### 💅 Refactors

- **repo-walk:** Replace experimental node:fs glob with fdir ([#55](https://github.com/imtiyaazsalie/frameforge/pull/55))

### 📖 Documentation

- **agents:** Add Engineering standard — equal-or-better bar, root-cause depth, no gold-plating ([#15](https://github.com/imtiyaazsalie/frameforge/pull/15))
- **tools:** Enrich low-scoring tool descriptions for Glama TDQS ([#16](https://github.com/imtiyaazsalie/frameforge/pull/16))
- **readme:** Collapse duplicated dev section into a CONTRIBUTING pointer ([#17](https://github.com/imtiyaazsalie/frameforge/pull/17))
- **readme:** Add bidirectional demo GIFs and a plugin tour ([#18](https://github.com/imtiyaazsalie/frameforge/pull/18))
- **readme:** Clarify -32000 / Connection closed in the startup FAQ ([#27](https://github.com/imtiyaazsalie/frameforge/pull/27))
- **tools:** Truthful, steering descriptions for the hot read tools ([#37](https://github.com/imtiyaazsalie/frameforge/pull/37))
- Sync npm README tool count with the registry and fix stale manifest reasoning ([#49](https://github.com/imtiyaazsalie/frameforge/pull/49))
- Reword server description and add Codex to client mentions ([#68](https://github.com/imtiyaazsalie/frameforge/pull/68))

### 🏡 Chore

- Skip changelogen GitHub release prompt in pnpm release ([#13](https://github.com/imtiyaazsalie/frameforge/pull/13))

### ✅ Tests

- **design-context:** Guard every serialized dimension against silent projection drops ([#48](https://github.com/imtiyaazsalie/frameforge/pull/48))

### 🤖 CI

- Fail lint on warnings and drop stale tooling leftovers ([#50](https://github.com/imtiyaazsalie/frameforge/pull/50))

### ❤️ Contributors

- Imtiyaaz Salie ([@imtiyaazsalie](https://github.com/imtiyaazsalie))

## v0.2.0

[compare changes](https://github.com/imtiyaazsalie/frameforge/compare/v0.1.0...v0.2.0)

### 🚀 Enhancements

- Add get_component_api and set_instance_properties ([#3](https://github.com/imtiyaazsalie/frameforge/pull/3))
- Add import_svg to place vector logos and icons from SVG markup ([#4](https://github.com/imtiyaazsalie/frameforge/pull/4))
- Let create_component componentize an existing node (fromNodeId) ([#5](https://github.com/imtiyaazsalie/frameforge/pull/5))
- Add set_arc and read ellipse arcData (pie / gauge / ring) ([#6](https://github.com/imtiyaazsalie/frameforge/pull/6))
- Carry pattern fill tiling geometry for faithful codegen ([#8](https://github.com/imtiyaazsalie/frameforge/pull/8))
- Make the plugin window resizable with a drag handle ([#9](https://github.com/imtiyaazsalie/frameforge/pull/9))

### 🩹 Fixes

- **skills:** Drop non-standard min-server-version frontmatter ([10ec3c4](https://github.com/imtiyaazsalie/frameforge/commit/10ec3c4))
- Report version mismatches clearly and validate the leader ping ([#2](https://github.com/imtiyaazsalie/frameforge/pull/2))

### 📖 Documentation

- **skills:** Scope install command to the skills/ subpath ([5277f56](https://github.com/imtiyaazsalie/frameforge/commit/5277f56))
- Rewrite README, add CONTRIBUTING, and polish project metadata ([#1](https://github.com/imtiyaazsalie/frameforge/pull/1))
- Swap Node badge for Glama MCP server score badge ([#11](https://github.com/imtiyaazsalie/frameforge/pull/11))
- Add light/dark logo and simplify README header ([#12](https://github.com/imtiyaazsalie/frameforge/pull/12))

### 🏡 Chore

- Add glama.json for Glama MCP registry listing ([#10](https://github.com/imtiyaazsalie/frameforge/pull/10))

### ❤️ Contributors

- Imtiyaaz Salie ([@imtiyaazsalie](https://github.com/imtiyaazsalie))

## v0.1.0

### 🚀 Enhancements

- **m2:** Write-parity kickoff — idempotency infra + 3 tools ([0eec93a](https://github.com/imtiyaazsalie/frameforge/commit/0eec93a))
- **m2:** Add set_opacity / set_visible / rename_node / delete_nodes ([4eda9d0](https://github.com/imtiyaazsalie/frameforge/commit/4eda9d0))
- **m2:** Add create_text/rectangle, set_corner_radius/strokes, move/resize_nodes ([cb2c3b3](https://github.com/imtiyaazsalie/frameforge/commit/cb2c3b3))
- **m2:** Add set_auto_layout/blend_mode/constraints, rotate/lock/unlock_nodes, clone_node ([9f96d7e](https://github.com/imtiyaazsalie/frameforge/commit/9f96d7e))
- **m2:** Add 8 style + 6 variable write tools (34/52) ([652e855](https://github.com/imtiyaazsalie/frameforge/commit/652e855))
- **m2:** Add structural + bulk-text write tools (40/52) ([0d8b7e0](https://github.com/imtiyaazsalie/frameforge/commit/0d8b7e0))
- **m2:** Add page write tools (44/52) ([4a8d40c](https://github.com/imtiyaazsalie/frameforge/commit/4a8d40c))
- **m2:** Add prototype + component-nav write tools (48/52) ([5405744](https://github.com/imtiyaazsalie/frameforge/commit/5405744))
- **m2:** Add import_image write tool (49/52) ([e6e307e](https://github.com/imtiyaazsalie/frameforge/commit/e6e307e))
- **m2:** Add create_ellipse / create_component / create_section — 52/52 tool count ([bb25810](https://github.com/imtiyaazsalie/frameforge/commit/bb25810))
- **m2:** Add batch atomic write tool — 53 tools, all-or-nothing rollback ([ba6d4d4](https://github.com/imtiyaazsalie/frameforge/commit/ba6d4d4))
- **m2:** Add create_instance — fills the component-side planning gap (54 tools) ([45bad2a](https://github.com/imtiyaazsalie/frameforge/commit/45bad2a))
- **m2.5:** Gradient paints — read + write (round-trippable) ([9341f4a](https://github.com/imtiyaazsalie/frameforge/commit/9341f4a))
- **m2.5:** Text truncation/maxLines (read+write) + FLOAT alias regression test ([3bed475](https://github.com/imtiyaazsalie/frameforge/commit/3bed475))
- **design-context:** P1 surface grounding fields ([52c226e](https://github.com/imtiyaazsalie/frameforge/commit/52c226e))
- **design-context:** P2 resolve token ids to names ([84cd506](https://github.com/imtiyaazsalie/frameforge/commit/84cd506))
- **design-context:** P3 globalVars dedup + structured values + metrics ([69ccea9](https://github.com/imtiyaazsalie/frameforge/commit/69ccea9))
- **design-context:** P3.1 surface + dedup strokes & effects ([3583b60](https://github.com/imtiyaazsalie/frameforge/commit/3583b60))
- **m3:** Analyze_project — JS/TS profile detector (Tailwind v3+v4 aware) ([4a9ce62](https://github.com/imtiyaazsalie/frameforge/commit/4a9ce62))
- **m3:** Scan_components — oxc-based local component scanner ([a460176](https://github.com/imtiyaazsalie/frameforge/commit/a460176))
- **m3:** Component_map — join Figma component names to local code components ([be0fb7c](https://github.com/imtiyaazsalie/frameforge/commit/be0fb7c))
- **m3:** Wire scan_components + component_map; demote analyze_project to internal helper ([7a02671](https://github.com/imtiyaazsalie/frameforge/commit/7a02671))
- **m3:** Expose analyze_project as a standalone MCP tool (revert demotion) ([b12ec5b](https://github.com/imtiyaazsalie/frameforge/commit/b12ec5b))
- **m3:** Token_map — join Figma variables to project design tokens ([87ae2f8](https://github.com/imtiyaazsalie/frameforge/commit/87ae2f8))
- **m3:** Token_map B3 — Tailwind/Figma namespace synonyms ([a58aeda](https://github.com/imtiyaazsalie/frameforge/commit/a58aeda))
- **m3:** Component_map emits per-instance props (instances[]) ([cdaafc1](https://github.com/imtiyaazsalie/frameforge/commit/cdaafc1))
- **m3:** Component_map reports unmatchedProps (component-extension TODOs) ([b15fb89](https://github.com/imtiyaazsalie/frameforge/commit/b15fb89))
- **m3:** Token_map opens size↔text via the variable's collection ([5a437bf](https://github.com/imtiyaazsalie/frameforge/commit/5a437bf))
- **m3:** MCP prompts capability + figma_to_code (cross-client codegen) ([8de7066](https://github.com/imtiyaazsalie/frameforge/commit/8de7066))
- **relay:** Multi-plugin routing on most-recently-active session ([1613dad](https://github.com/imtiyaazsalie/frameforge/commit/1613dad))
- **plugin:** Emit activity on window focus/visibility ([56b8422](https://github.com/imtiyaazsalie/frameforge/commit/56b8422))
- **codegen:** Asset-export step — close the no-codegen fidelity gap ([2f61138](https://github.com/imtiyaazsalie/frameforge/commit/2f61138))
- **token_map:** Framework-builtin scale recognition + codegen effect-fidelity guidance ([5ea3d11](https://github.com/imtiyaazsalie/frameforge/commit/5ea3d11))
- **token_map:** Font-weight framework-builtin (weight/\* → font-bold etc.) ([f8972fd](https://github.com/imtiyaazsalie/frameforge/commit/f8972fd))
- **get_design_context:** Per-instance textOverrides on deduped instances ([f55d3d1](https://github.com/imtiyaazsalie/frameforge/commit/f55d3d1))
- **serializer:** Surface per-side stroke weights for mixed borders ([d34a2b6](https://github.com/imtiyaazsalie/frameforge/commit/d34a2b6))
- **profile:** Svg-handling detection + icon import/use guidance ([838043b](https://github.com/imtiyaazsalie/frameforge/commit/838043b))
- **scan:** Gitignore-aware shared repo walker ([e47ca2a](https://github.com/imtiyaazsalie/frameforge/commit/e47ca2a))
- **screenshot:** Flag empty exports (clipped/off-canvas/hidden nodes) ([9301e89](https://github.com/imtiyaazsalie/frameforge/commit/9301e89))
- **write:** Tier 1 write-surface hardening — typography, per-side strokes, variable CRUD, child layout ([0047d72](https://github.com/imtiyaazsalie/frameforge/commit/0047d72))
- **write:** Add combine_as_variants — combine COMPONENTs into a COMPONENT_SET ([07aa2bb](https://github.com/imtiyaazsalie/frameforge/commit/07aa2bb))
- **codegen:** Gradient + image object-fit fidelity (close two silent grounding misses) ([0b9fae7](https://github.com/imtiyaazsalie/frameforge/commit/0b9fae7))
- **codegen:** StrokeAlign semantics (close the application-side miss behind Framelink #386) ([893ac03](https://github.com/imtiyaazsalie/frameforge/commit/893ac03))
- **grounding:** Surface auto-layout to get_design_context + GRID auto-layout (read+write) ([fcb4028](https://github.com/imtiyaazsalie/frameforge/commit/fcb4028))
- **plugin-ui:** Slim the panel, add "Run in background", fix Context overflow ([0bc5c1d](https://github.com/imtiyaazsalie/frameforge/commit/0bc5c1d))
- **grounding:** Icon_map — reuse curated .svg icons + color contract ([28405b2](https://github.com/imtiyaazsalie/frameforge/commit/28405b2))
- **grounding:** Get_variable_defs emits hex for COLOR values ([30a0aec](https://github.com/imtiyaazsalie/frameforge/commit/30a0aec))
- **grounding:** Surface per-corner radius, blendMode, mask in read path ([cf8f07d](https://github.com/imtiyaazsalie/frameforge/commit/cf8f07d))
- **write:** Per-corner set_corner_radius + new set_mask tool ([7437460](https://github.com/imtiyaazsalie/frameforge/commit/7437460))
- Derive displayed versions from the single product version ([ee176fa](https://github.com/imtiyaazsalie/frameforge/commit/ee176fa))
- **mcp:** Accept a Figma URL or dash-form node id in id args ([e18cb14](https://github.com/imtiyaazsalie/frameforge/commit/e18cb14))
- **mcp:** Bind a color variable to a fill/stroke paint ([dfd740b](https://github.com/imtiyaazsalie/frameforge/commit/dfd740b))
- **skill:** Add figma-build skill + code_to_figma prompt (write direction) ([01e5d11](https://github.com/imtiyaazsalie/frameforge/commit/01e5d11))
- **mcp:** Delete a variable collection by id ([ac5d532](https://github.com/imtiyaazsalie/frameforge/commit/ac5d532))
- **plugin:** Show the payload fed to the LLM in the Activity tab ([12f6734](https://github.com/imtiyaazsalie/frameforge/commit/12f6734))
- **plugin:** Tidy payload row + use vueuse clipboard ([53d44ba](https://github.com/imtiyaazsalie/frameforge/commit/53d44ba))
- **plugin:** Copyable diagnostic bundle for bug reports ([efc87a5](https://github.com/imtiyaazsalie/frameforge/commit/efc87a5))
- **mcp:** Export a node or page to a single PDF file ([4edac47](https://github.com/imtiyaazsalie/frameforge/commit/4edac47))
- **get_design_context:** Warn on multi-breakpoint selection to keep mixed codegen grounded ([adf2505](https://github.com/imtiyaazsalie/frameforge/commit/adf2505))
- Keep the connection alive through heavy operations (busy ≠ dead) ([7ee504d](https://github.com/imtiyaazsalie/frameforge/commit/7ee504d))
- **get_design_context:** Surface text typography so codegen stops eyeballing it ([a0952ec](https://github.com/imtiyaazsalie/frameforge/commit/a0952ec))

### 🔥 Performance

- **component-map:** Resolve set name from grounding, drop doc-wide scan ([0640441](https://github.com/imtiyaazsalie/frameforge/commit/0640441))
- **scan:** Prune ignored dirs at the glob level, not after ([d42264b](https://github.com/imtiyaazsalie/frameforge/commit/d42264b))
- **plugin:** Skip full serialization for minimal/compact get_design_context ([1d8f623](https://github.com/imtiyaazsalie/frameforge/commit/1d8f623))

### 🩹 Fixes

- **m2:** Set_variable_value — type the polymorphic `value` so it isn't stringified ([55a9ea4](https://github.com/imtiyaazsalie/frameforge/commit/55a9ea4))
- **design-context:** Emit node style refs before children ([1025117](https://github.com/imtiyaazsalie/frameforge/commit/1025117))
- **hook:** Scope format-on-edit to files inside the project root ([1ac4f7f](https://github.com/imtiyaazsalie/frameforge/commit/1ac4f7f))
- **m3:** A/B-driven accuracy fixes for component_map + token_map ([3440cac](https://github.com/imtiyaazsalie/frameforge/commit/3440cac))
- **component-map:** Degrade gracefully when get_local_components times out ([84ab5fa](https://github.com/imtiyaazsalie/frameforge/commit/84ab5fa))
- **relay:** Session affinity for multi-call tools ([9b0042b](https://github.com/imtiyaazsalie/frameforge/commit/9b0042b))
- **component-map:** Merge a component across sibling frames into one usage ([96c6d30](https://github.com/imtiyaazsalie/frameforge/commit/96c6d30))
- **routing:** Visibility-gated activity + no-selection scope guards ([af164f7](https://github.com/imtiyaazsalie/frameforge/commit/af164f7))
- **scan:** Single-extension profiles (Vue/Svelte) silently scanned nothing ([0070a84](https://github.com/imtiyaazsalie/frameforge/commit/0070a84))
- **routing:** A reconnect must not steal routing from the active file ([eab1c42](https://github.com/imtiyaazsalie/frameforge/commit/eab1c42))
- **token_map:** Emit var() ref on non-Tailwind projects, not a bogus utility ([300efb7](https://github.com/imtiyaazsalie/frameforge/commit/300efb7))
- **variables:** Parse stringified VARIABLE_ALIAS for FLOAT vars (go #22 last edge) ([92de535](https://github.com/imtiyaazsalie/frameforge/commit/92de535))
- **mcp:** Move @frameforge/shared to devDependencies ([e731482](https://github.com/imtiyaazsalie/frameforge/commit/e731482))
- **plugin:** Auto-reconnect when plugin opens before the relay server ([fa8ac9a](https://github.com/imtiyaazsalie/frameforge/commit/fa8ac9a))
- **plugin:** Recover clipped/off-canvas exports via useAbsoluteBounds ([24dc2d6](https://github.com/imtiyaazsalie/frameforge/commit/24dc2d6))

### 💅 Refactors

- **m2:** Registry guards + honest batch rollback (post-M2 retrospective) ([44cf086](https://github.com/imtiyaazsalie/frameforge/commit/44cf086))
- **server:** Tool-spec helper + first reads to Zod (Phase 1) ([766c6ff](https://github.com/imtiyaazsalie/frameforge/commit/766c6ff))
- **server:** Convert simple read tools to Zod specs (Phase 1) ([f33a056](https://github.com/imtiyaazsalie/frameforge/commit/f33a056))
- **server:** Convert remaining read tools to Zod specs (Phase 1) ([b561c1b](https://github.com/imtiyaazsalie/frameforge/commit/b561c1b))
- **server:** Convert server-local tools to Zod specs (Phase 1) ([7c21003](https://github.com/imtiyaazsalie/frameforge/commit/7c21003))
- **server:** Convert all write tools to Zod specs (Phase 1 complete) ([c4acdba](https://github.com/imtiyaazsalie/frameforge/commit/c4acdba))
- **server:** Cut over to McpServer (registerTool/registerPrompt) ([72824a7](https://github.com/imtiyaazsalie/frameforge/commit/72824a7))
- **server:** Move schema-derivation helper out of src to test-only ([f211529](https://github.com/imtiyaazsalie/frameforge/commit/f211529))
- Convert shared + plugin + election layer to Zod ([387015e](https://github.com/imtiyaazsalie/frameforge/commit/387015e))
- **m3:** Hardening review — SFC props, CSS-var token grounding, cleanup ([ffd44aa](https://github.com/imtiyaazsalie/frameforge/commit/ffd44aa))
- **plugin-ui:** Adopt vueuse composables in App.vue ([83a2531](https://github.com/imtiyaazsalie/frameforge/commit/83a2531))
- **repo:** Rename packages/server → packages/mcp ([6e31a91](https://github.com/imtiyaazsalie/frameforge/commit/6e31a91))
- Move skills to repo root for skills.sh discovery ([3f28078](https://github.com/imtiyaazsalie/frameforge/commit/3f28078))
- **skill:** Split figma-codegen into a router + references ([3587be3](https://github.com/imtiyaazsalie/frameforge/commit/3587be3))
- **skill:** Split figma-build into a router + references ([7770218](https://github.com/imtiyaazsalie/frameforge/commit/7770218))

### 📖 Documentation

- **plan:** Record Framelink borrowed techniques for M3 ([1f49745](https://github.com/imtiyaazsalie/frameforge/commit/1f49745))
- **skills:** Rewrite figma-codegen to orchestrate the shipped M3 tools ([f12b502](https://github.com/imtiyaazsalie/frameforge/commit/f12b502))
- **skills:** Figma-codegen drills repeated unmapped components ([eaba36c](https://github.com/imtiyaazsalie/frameforge/commit/eaba36c))
- **server:** Correct spec bridge comments + record McpServer migration done ([e590564](https://github.com/imtiyaazsalie/frameforge/commit/e590564))
- **codegen:** Tell codegen to read deduped instances' textOverrides ([faf4cdc](https://github.com/imtiyaazsalie/frameforge/commit/faf4cdc))
- **codegen:** Responsive-by-default + breakpoint-discovery guidance ([316266d](https://github.com/imtiyaazsalie/frameforge/commit/316266d))
- **codegen:** Full-bleed pages need a body reset — conditionally ([6f3b313](https://github.com/imtiyaazsalie/frameforge/commit/6f3b313))
- **codegen:** The conditional reset must be complete, not body-only ([54a3bb9](https://github.com/imtiyaazsalie/frameforge/commit/54a3bb9))
- **plan:** M5 re-evaluation — converge visual verification to skill self-verify, cut 2 screenshot tools ([388d8e3](https://github.com/imtiyaazsalie/frameforge/commit/388d8e3))
- **codegen:** Large-design section-by-section + ground-every-section guidance ([82adee5](https://github.com/imtiyaazsalie/frameforge/commit/82adee5))
- Add AGENTS.md (project guide) + CLAUDE.md pointer ([87cebf2](https://github.com/imtiyaazsalie/frameforge/commit/87cebf2))
- **skill:** Broaden figma-codegen trigger description ([8540a27](https://github.com/imtiyaazsalie/frameforge/commit/8540a27))
- **skill:** Note delete_variable_collection in author-design-system ([538ce08](https://github.com/imtiyaazsalie/frameforge/commit/538ce08))
- **skill:** Prefer min-w over hard width for fixed-width hug controls ([a3134eb](https://github.com/imtiyaazsalie/frameforge/commit/a3134eb))
- **skill:** Treat a same-size sibling artboard as an overlay state, not a fixed-width sidebar ([c06c222](https://github.com/imtiyaazsalie/frameforge/commit/c06c222))
- **skill:** Ground each breakpoint's own values for mixed desktop/mobile selection ([0b3f9d5](https://github.com/imtiyaazsalie/frameforge/commit/0b3f9d5))
- **mcp:** Note cornerRadius binds all four corners in bind_variable_to_node ([0335503](https://github.com/imtiyaazsalie/frameforge/commit/0335503))
- Use 2026-present in license copyright ([c04a902](https://github.com/imtiyaazsalie/frameforge/commit/c04a902))
- **figma-codegen:** Translate absolute positioning + constraints in grounding ([1d9ee11](https://github.com/imtiyaazsalie/frameforge/commit/1d9ee11))

### 🏡 Chore

- Pin all `latest` dependency specifiers to caret ranges ([7976012](https://github.com/imtiyaazsalie/frameforge/commit/7976012))
- Align @types/node to the Node 24 major (^24.12.4) ([557dd83](https://github.com/imtiyaazsalie/frameforge/commit/557dd83))
- Auto-format/lint edited files via PostToolUse hook ([9e88144](https://github.com/imtiyaazsalie/frameforge/commit/9e88144))
- Move format-on-edit hook script under .claude/hooks/ ([ddf2c4c](https://github.com/imtiyaazsalie/frameforge/commit/ddf2c4c))
- **server:** Add zod dep for McpServer migration (Phase 0) ([66ef4df](https://github.com/imtiyaazsalie/frameforge/commit/66ef4df))
- Remove routing/timeout debug instrumentation ([c78e939](https://github.com/imtiyaazsalie/frameforge/commit/c78e939))
- **format:** Bump oxfmt 0.51→0.53 and reformat the tree ([197f52d](https://github.com/imtiyaazsalie/frameforge/commit/197f52d))
- Stop tracking PLAN.md (internal dev doc, not for publication) ([ce9bff8](https://github.com/imtiyaazsalie/frameforge/commit/ce9bff8))
- **skills:** Vendor skill-creator under .claude/skills ([eeeb502](https://github.com/imtiyaazsalie/frameforge/commit/eeeb502))
- **skills:** Vendor create-readme skill under .claude/skills ([b501f52](https://github.com/imtiyaazsalie/frameforge/commit/b501f52))
- **rename:** Figma-mcp-relay → frameforge ([cead534](https://github.com/imtiyaazsalie/frameforge/commit/cead534))
- **rename:** Point .mcp.json at ~/Desktop/frameforge ([2c366a9](https://github.com/imtiyaazsalie/frameforge/commit/2c366a9))
- **rename:** Plugin UI color tokens relay-_ → fig-_ ([4618dd9](https://github.com/imtiyaazsalie/frameforge/commit/4618dd9))
- **mcp:** Use repo-relative path in .mcp.json ([262af53](https://github.com/imtiyaazsalie/frameforge/commit/262af53))
- **knip:** Make knip pass so it can gate CI ([0a158ac](https://github.com/imtiyaazsalie/frameforge/commit/0a158ac))
- **knip:** Drop redundant config flagged by knip's own hints ([7e93814](https://github.com/imtiyaazsalie/frameforge/commit/7e93814))
- **lint:** Clear the remaining oxlint warnings ([0ceda52](https://github.com/imtiyaazsalie/frameforge/commit/0ceda52))
- Tidy local-only files into .local/ ([bcd1139](https://github.com/imtiyaazsalie/frameforge/commit/bcd1139))
- Set author/copyright ([395f7e8](https://github.com/imtiyaazsalie/frameforge/commit/395f7e8))
- Remove lefthook git hooks ([3be457d](https://github.com/imtiyaazsalie/frameforge/commit/3be457d))
- Upgrade dev dependencies and quiet new oxlint warning ([69f7323](https://github.com/imtiyaazsalie/frameforge/commit/69f7323))
- **skills:** Mirror skills/ into .claude/skills via postinstall instead of symlinks ([11e6ca0](https://github.com/imtiyaazsalie/frameforge/commit/11e6ca0))
- Upgrade pnpm to 11.8.0 and node to 24.17.0 ([e4cc32c](https://github.com/imtiyaazsalie/frameforge/commit/e4cc32c))
- **vscode:** Run oxc format and fixAll on save ([7387524](https://github.com/imtiyaazsalie/frameforge/commit/7387524))

### 🎨 Styles

- Format sync-skills.mjs with oxfmt ([62cf9e8](https://github.com/imtiyaazsalie/frameforge/commit/62cf9e8))

### 🤖 CI

- Add CI workflow (typecheck, lint, knip, build, test) ([fda58c5](https://github.com/imtiyaazsalie/frameforge/commit/fda58c5))
- Validate PR titles follow Conventional Commits ([99a546c](https://github.com/imtiyaazsalie/frameforge/commit/99a546c))
- Add format:check gate; ignore vendored skills in oxfmt config ([9c9070a](https://github.com/imtiyaazsalie/frameforge/commit/9c9070a))
- Add release pipeline (changelogen + OIDC npm publish) ([ba3985f](https://github.com/imtiyaazsalie/frameforge/commit/ba3985f))
- Product-level CHANGELOG at root + ship the Figma plugin as a release asset ([94a905a](https://github.com/imtiyaazsalie/frameforge/commit/94a905a))
- Validate publish correctness with publint (via tsdown) ([8836af5](https://github.com/imtiyaazsalie/frameforge/commit/8836af5))

### ❤️ Contributors

- Imtiyaaz Salie
