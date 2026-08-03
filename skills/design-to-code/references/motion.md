# Motion → code (animation)

Figma Motion (beta) lets a frame's layers animate — applied **animation-style presets** (fade / slide
in), **manual keyframe tracks** on properties (translate, scale, rotate, opacity, …), and a **timeline**
with a duration. Carry that into the project's animation mechanism instead of dropping it (a static
component from an animated frame is a fidelity miss, the same class as dropping a shadow).

## Detect the animation in the grounding

1. **`get_design_context`** (detail `full`) tags any animated node with a compact `motion` summary:
   - `animationStyles` — applied preset names (e.g. `"Slide In"`).
   - `animatedProperties` — the fields that carry keyframes (`TRANSLATION_X`, `OPACITY`, `SCALE_XY`, …).
   - `timelineDuration` — the containing timeline's length in seconds.
2. When the summary isn't enough, **`get_node_motion`** on that node returns the full detail:
   `animationStyles` (with configured props), `animations` / `manualKeyframeTracks` (every keyframe:
   `timelinePosition` in seconds, typed `value`, `easing`), and `timelines`.

If neither reports motion, there's no animation to carry — don't invent one.

## Emit it in the project's own animation mechanism

Emit animation in the project's existing mechanism (check what's already used before adding a dep):
CSS `@keyframes` / `transition`, Framer Motion, GSAP, Vue `<transition>`, Svelte transitions.

### Property fields to transforms

| Figma field                                                                       | CSS / transform                                        | Framer Motion                 |
| --------------------------------------------------------------------------------- | ------------------------------------------------------ | ----------------------------- |
| `TRANSLATION_X` / `TRANSLATION_Y` / `TRANSLATION_XY`                              | `translateX/Y` (`transform`)                           | `x` / `y`                     |
| `SCALE_X` / `SCALE_Y` / `SCALE_XY`                                                | `scaleX/Y`                                             | `scaleX` / `scaleY` / `scale` |
| `ROTATION`                                                                        | `rotate` (deg; Figma is radians → `deg = rad * 180/π`) | `rotate` (deg)                |
| `OPACITY`                                                                         | `opacity`                                              | `opacity`                     |
| `CORNER_RADIUS`, `STROKE_WEIGHT`, `WIDTH`/`HEIGHT`, `STACK_SPACING`, padding, gap | the matching CSS prop                                  | style value                   |
| effect fields (shadow `OFFSET_X`/`RADIUS`/`COLOR`, …)                             | animate `box-shadow` / `filter`                        | `boxShadow` etc.              |

A `FLOAT` keyframe value is the raw number; `COLOR` is RGBA 0–1 (→ hex/rgb); `VECTOR` is `{x,y}`.

### From tracks to keyframes

- **Two-keyframe track** (base → target) is a **transition/entrance**: emit a `transition` or a
  Framer `initial`/`animate` pair, not a full `@keyframes`.
- **Multi-keyframe track** → CSS `@keyframes` with each `timelinePosition/duration` as a `%` stop, or a
  Framer keyframe array (`animate={{ x: [0, 120, 100] }}`).
- **`timelineDuration`** → `animation-duration` / `transition` duration / Framer `transition.duration`.

### Staggered entrances

A row/list whose siblings share a preset but differ in `timelineOffset` (0, 0.1, 0.2, …) is a
**staggered entrance**. Emit it as stagger, not N hardcoded delays: Framer `staggerChildren`, CSS
`animation-delay: calc(var(--i) * 100ms)`, GSAP `stagger`.

### Easing

| Figma `MotionEasing.type`                                | CSS                                                                     | Framer                                                            |
| -------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `LINEAR`                                                 | `linear`                                                                | `"linear"`                                                        |
| `EASE_IN` / `EASE_OUT` / `EASE_IN_AND_OUT`               | `ease-in` / `ease-out` / `ease-in-out`                                  | `"easeIn"` / `"easeOut"` / `"easeInOut"`                          |
| `EASE_*_BACK`                                            | `cubic-bezier` overshoot (e.g. back-out `cubic-bezier(.34,1.56,.64,1)`) | `[.34,1.56,.64,1]`                                                |
| `CUSTOM_CUBIC_BEZIER`                                    | `cubic-bezier(x1,y1,x2,y2)` from `easingFunctionCubicBezier`            | that array                                                        |
| `GENTLE` / `QUICK` / `BOUNCY` / `SLOW` / `CUSTOM_SPRING` | **spring — no native CSS**; approximate with a bezier and note the gap  | `{ type: "spring", bounce }` (from `easingFunctionSpring.bounce`) |
| `HOLD`                                                   | `steps(1, jump-end)`                                                    | `steps`                                                           |

## Where the mapping is lossy

- **Spring is lossy to CSS.** Figma's `GENTLE`/`BOUNCY`/`CUSTOM_SPRING` have no native CSS equivalent.
  Use a spring-capable lib (Framer/GSAP) when the project has one; otherwise approximate with a bezier
  and flag it rather than pretending it's exact.
- **Rotation is radians in Figma, degrees in CSS/Framer** — always convert.
- Carry only what's animated; don't add motion a static node didn't have.
