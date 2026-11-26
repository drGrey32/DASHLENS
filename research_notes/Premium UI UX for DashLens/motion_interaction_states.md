# Motion, Micro-interactions and Interface States for DashLens

Research note scope: motion rules and numbers, micro-interaction rules, perceived performance, a full state checklist, sound/haptics, and craft references. Target: DashLens, a single-file vanilla-JS dashcam viewer (synced video tiles, canvas timeline/map/G-sensor chart, drawers, modals, toasts, loading card, export progress bar; dark UI; must respect prefers-reduced-motion; animation must never slow playback or scrubbing).

Method note (important for the report writer): this session's network blocked direct fetches of emilkowal.ski, rauno.me, m3.material.io, nngroup.com, w3.org and api.flutter.dev. Primary material was obtained instead from (a) Emil Kowalski's own published animation standards file on GitHub, (b) Vercel's Web Interface Guidelines README on GitHub, (c) Material Components Android's official Motion.md on GitHub (same M3 token values as m3.material.io), (d) the Apple WWDC18 "Designing Fluid Interfaces" session page/transcript on developer.apple.com, and (e) search-result excerpts of NN/g, web.dev and Radix pages. Where only a search excerpt or a secondary summary was available, this is flagged.

## Motion: durations, easing, springs, what and when to animate

### Takeaway
Keep product-UI motion short (roughly 100–300 ms; drawers/modals up to ~400–500 ms), use ease-out (decelerate) for anything entering, accelerate or a faster ease-out for exits, animate only transform and opacity, and do not animate things the user does many times a day or via keyboard. For a pro tool like DashLens, motion should be "crisp and fast", interruptible, and reduced (not removed) under prefers-reduced-motion.

### Cited Findings

Durations
- Emil Kowalski's duration table: button press 100–160 ms; tooltips and small popovers 125–200 ms; dropdowns and selects 150–250 ms; modals and drawers 200–500 ms; general rule "UI animations stay under 300ms", with modals, drawers, sheets and toasts as exceptions; Sonner toasts use 400 ms `ease`. — [Emil Kowalski, animation STANDARDS.md (GitHub)](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Emil's site also states animations "should also usually be shorter than 300ms" and names ease-out as the default (search excerpt). — [emilkowal.ski, Great animations](https://emilkowal.ski/ui/great-animations)
- Material 3 duration tokens (ms): Short1 50, Short2 100, Short3 150, Short4 200; Medium1 250, Medium2 300, Medium3 350, Medium4 400; Long1 450, Long2 500, Long3 550, Long4 600; ExtraLong1 700, ExtraLong2 800, ExtraLong3 900, ExtraLong4 1000. — [Material Components Android, Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- M3 rule of thumb: "duration should increase as the area/traversal of an animation increases." Component defaults: container transform 300 ms in / 250 ms out; shared axis and fade-through 300 ms; fade 150 ms in / 75 ms out (exits faster than entrances). — [Material Components Android, Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)

Easing curves (exact values)
- M3 Standard `cubic-bezier(0.2, 0, 0, 1)` (begins and ends on screen); Standard Decelerate `cubic-bezier(0, 0, 0, 1)` (enter); Standard Accelerate `cubic-bezier(0.3, 0, 1, 1)` (exit); Emphasized = path `M 0,0 C 0.05,0 0.133333,0.06 0.166666,0.4 C 0.208333,0.82 0.25,1 1,1` (not expressible as one cubic-bezier); Emphasized Decelerate `cubic-bezier(0.05, 0.7, 0.1, 1)` (enter); Emphasized Accelerate `cubic-bezier(0.3, 0, 0.8, 0.15)` (exit); Linear `cubic-bezier(0, 0, 1, 1)`. Enter uses decelerate variants; exit uses accelerate variants. — [Material Components Android, Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- Third-party token packages disagree on what "Emphasized" maps to in CSS: some use `(0.2, 0, 0, 1)` for the Emphasized entry, others use the decelerate/accelerate pair above. The official Android doc above is authoritative. — [bevy_material_ui tokens](https://docs.rs/crate/bevy_material_ui/latest/source/src/tokens.rs); [CSS motion tokens guide](https://camoa.github.io/dev-guides/css/css-craft/motion-design-tokens)
- Emil Kowalski's mapping: entering/exiting = ease-out; moving/morphing on screen = ease-in-out; hover/colour = `ease`; constant motion = linear; default = ease-out; "Never use ease-in on UI." Custom curves: `--ease-out: cubic-bezier(0.23, 1, 0.32, 1)`; `--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1)`; `--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1)` (the Vaul drawer curve). — [Emil Kowalski, STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Note the conflict: M3 uses accelerate (ease-in-like) curves for exits; Emil says never ease-in on UI and uses ease-out for exits too. Both agree exits should be short. — [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md); [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: "Match easing to what changes (size, distance, or trigger)"; never use `transition: all`, list properties explicitly. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)

Springs vs curves
- Apple WWDC18: springs are described with two designer parameters, damping (100% = no overshoot, 0% = oscillates forever) and response (how quickly it reaches target); "we recommend starting with 100% damping, or no overshoot"; Music's swipe-to-dismiss uses 80% damping while tap-to-present uses 100%; "if the gesture that's driving the motion itself has momentum, then you should reward that momentum with a little bit of overshoot"; "Bounciness needs to be purposeful"; Apple avoids "duration" for springs because it "reinforces this concept of constant dynamic change." — [Apple WWDC18 Designing Fluid Interfaces](https://developer.apple.com/videos/play/wwdc2018/803/)
- Emil: recommended spring `{ type: "spring", duration: 0.5, bounce: 0.2 }`; keep bounce 0.1–0.3 and avoid it in most UI; use springs for momentum drags, interruptible gestures and pointer-following. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- M3 spring tokens (damping ratio / stiffness): FastSpatial 0.9/1400 (switches, buttons); FastEffects 1/3800 (small colour/opacity); DefaultSpatial 0.9/700 (partial-screen, e.g. bottom sheet); DefaultEffects 1/1600; SlowSpatial 0.9/300 (full screen); SlowEffects 1/800. Effects (colour/opacity) springs use damping 1 so they never overshoot. — [Material Components Android, Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- Nathan Gitter's write-up of the WWDC talk: most animations should use damping 1; don't force a duration on a spring. — [Building Fluid Interfaces (Medium)](https://medium.com/@nathangitter/building-fluid-interfaces-ios-swift-9732bb934bf5)

What to animate / performance
- Animate `transform` and `opacity`; avoid animating `padding`, `margin`, `height`, `width`, `top`, `left` (clip-path and measured height are exceptions). Use CSS for predetermined motion and JS/WAAPI for dynamic interruptible motion. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: prefer CSS, then Web Animations API, then JS libraries; avoid main-thread JS animation; animate GPU-friendly `transform`/`opacity`; animate only "to clarify cause and effect or to add deliberate delight"; motion over 5 s alongside other content needs pause/stop/hide. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Apple: at 30 fps fast motion strobes; at 60 fps it stays smooth; "It's not just about framerate. It's what's in the frames." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)

When NOT to animate (frequency)
- Emil's frequency rule: used 100+ times/day (keyboard shortcuts, command palette) = no animation; tens of times/day (hover, list navigation) = remove or greatly reduce; occasional (modals, drawers, toasts) = standard animation; rare/first-time (onboarding, celebrations) = delight allowed. Dashboards "should be crisp and fast." — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Apple: explanatory/teaching motion only for gestures used often; "Don't use it for a gesture that's used only intermittently." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)

Origin, scale start, stagger
- Never animate from `scale(0)`; start from `scale(0.9–0.97)` with `opacity: 0`. Popovers scale from their trigger (`transform-origin: var(--transform-origin)`); modals keep `center`. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: "Anchor motion to where it physically starts (transform origin)"; for SVG use `transform-box: fill-box; transform-origin: center` on `<g>`. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Apple: an element "should have a consistent offscreen path as it enters and leaves" (spatial consistency). — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- Stagger: 30–80 ms between items; stagger is decorative and "must never block interaction." — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)

Interruptibility
- Use CSS transitions rather than keyframes for rapidly re-triggered UI, because keyframes restart from zero when interrupted; `@starting-style` for JS-free entry animations (fallback: `data-mounted` attribute). Asymmetric timing: fast release (e.g. 200 ms ease-out), slow deliberate press (e.g. 2 s linear for hold-to-confirm). — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: "Keep animations interruptible by user input." — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Apple: "We built a fully redirectable interface"; gestures can be changed mid-flight so "thought and gesture happen in parallel." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- Rauno Freiberg (July 2023): great interactions are modelled on real-world properties like interruptibility; a page flip you had to wait out would feel wrong (search excerpt; full essay not fetchable). — [Rauno Freiberg, Invisible Details of Interaction Design](https://rauno.me/craft/interaction-design)

Reduced motion
- Under `prefers-reduced-motion: reduce`, keep opacity and colour changes, remove transform-based motion; "Reduced motion means fewer, gentler animations, not none." Gate hover transforms behind `@media (hover: hover) and (pointer: fine)`. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: honour `prefers-reduced-motion` with a reduced variant; for looping video provide a still alternative. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)

Tuning
- To judge feel, slow animations 2–5x, use the DevTools Animations panel, test on real devices, review next day with fresh eyes. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)

### Inferences
- A DashLens token set that fits all sources: `--dur-instant: 0ms` (keyboard/frequent), `--dur-press: 120ms`, `--dur-fast: 150ms` (tooltips, hover), `--dur-base: 200ms` (menus, popovers, toast exit), `--dur-panel: 280–320ms` (drawers, modals enter), with exits ~60–75% of entrances (M3 fade 150/75, container 300/250). Easing: `--ease-out: cubic-bezier(0.23,1,0.32,1)` for enters, `--ease-drawer: cubic-bezier(0.32,0.72,0,1)` for drawers, M3 standard `cubic-bezier(0.2,0,0,1)` for on-screen moves.
- Things that should have zero animation in DashLens: frame-step, play/pause keyboard toggles, timeline playhead and map marker during playback or scrub (these must track the media clock 1:1, rendered in the same rAF as canvas drawing), seek via keyboard, tile focus/swap triggered by number keys. These are the "100+ times/day" class.
- Under reduced motion: replace drawer slides and modal scale with short opacity fades (~100–150 ms), remove toast slide (keep fade), keep the export progress bar's width/scale changes (they convey information) but drop shimmer/pulse loops.
- Because DashLens's playback is canvas + video, any UI animation should use compositor-only properties so it never competes with the main-thread rAF loop that draws the timeline, map and chart.

### Gaps
- Apple's own CSS-equivalent curves (e.g. UIKit's default `easeInOut` control points, or SwiftUI's default spring response/damping numbers) were not found in a fetchable primary source; WWDC18 gives damping guidance but no ms figures.
- Linear's and Vercel's (Geist) production cubic-bezier values were not found in a primary source in this session.
- NN/g's animation-duration article (often cited as "100–500 ms, ~200–300 ms typical") could not be fetched; treat any NN/g duration numbers as unverified.
- Val Head's guidance was not retrieved.
- M3 Expressive (2025) motion-scheme spring values beyond the six Android spring tokens above were not verified.

## Micro-interactions: hover, press, loading buttons, toggles, sliders, tooltips, menus, drag, scrubbing, dialog focus

### Takeaway
Press feedback must be immediate (highlight on pointer-down, under 100 ms), with a subtle scale of ~0.97; tooltips use a first-show delay and instant subsequent tooltips; popovers grow from their trigger; drags and scrubs track the pointer 1:1 with soft (rubber-band) boundaries; dialogs move focus in and return it on close.

### Cited Findings
- NN/g: under 0.1 s a response feels instantaneous and the user feels they caused it ("to create the illusion of direct manipulation, a user interface must be faster than 0.1 second"); 0.1–1 s users notice delay but stay in flow; ~10 s is the limit of attention (search excerpt). — [NN/g, Response Times: The 3 Important Limits](https://www.nngroup.com/articles/response-times-3-important-limits/) (excerpt via [NN/g video page](https://www.nngroup.com/videos/3-response-time-limits-interaction-design/))
- Apple: "the button should highlight immediately when I touch down on it," but the action commits on touch-up; "Provide continuous feedback during the interaction"; "the contents should stay attached to the gesture"; "Everything needs to respond instantly"; "if you introduce any amount of lag, things all of a sudden just kind of fall off a cliff." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- Press feedback: `scale(0.97)` on `:active` with a 160 ms ease-out transition, range 0.95–0.98; `scale()` also scales children, useful for press. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Button loading: show the loading indicator on the button while keeping the original label; keep submit enabled until submission starts, then disable during the request; use ellipses in loading labels ("Saving…"). — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Tooltips: Radix defaults `delayDuration` 700 ms (first open) and `skipDelayDuration` 300 ms (window in which moving to another trigger opens instantly). The 700 ms value is on Radix's own page; the 300 ms value was confirmed via the Radix docs mirror and radix-vue, not Radix's own page. — [Radix Tooltip](https://www.radix-ui.com/primitives/docs/components/tooltip); [Mintlify mirror](https://www.mintlify.com/radix-ui/primitives/components/tooltip); [radix-vue](https://8a5af331.radix-vue.pages.dev/components/tooltip)
- Vercel: "Delay the first tooltip in a group. Subsequent peer tooltips have no delay"; prefer inline help, tooltips as last resort. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Tooltip/popover motion: 125–200 ms; dropdowns 150–250 ms; popovers scale from trigger with `transform-origin`, starting at scale 0.9–0.97 + opacity 0. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Drag/gesture: dismiss on flick when velocity (px / ms) exceeds ~0.11, without a distance threshold; damp past boundaries ("friction over hard stops"); use pointer capture once dragging starts; ignore extra touch points after a drag begins. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- Vercel: use `inert` on dragged elements to prevent selection/hover during drag; gestures need a click or keyboard alternative; `touch-action: manipulation`. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Apple: rubber-banding tells the user "there's nothing there" — without it "you actually wouldn't know the difference between a frozen phone, and phone that's just at the top"; use velocity history ("we don't use the last position. We use the history of the touch"); project end points from velocity and deceleration (UIScrollView normal deceleration rate ≈ 0.998/ms; projection = (v/1000)·r/(1−r)); swipe hysteresis is "usually 10 points in iOS." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- Hit targets: expand to at least 24 px if the visual is smaller; 44 px on mobile. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Focus: visible ring on every focusable element via `:focus-visible` (`:focus-within` for groups); overlays must never cover the focused element; "Move and return focus according to WAI-ARIA patterns, using focus traps where appropriate"; confirm destructive actions or provide Undo within a safe window. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Comparison sliders and hold-to-confirm overlays can be done with `clip-path: inset()`. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)

### Inferences
- Timeline scrubbing in DashLens: on pointerdown, immediately (same frame) move the playhead and show a time readout bubble; use `setPointerCapture`; pause rendering of non-essential overlays; seek videos at a throttled rate (e.g. per rAF, using `fastSeek` where available) while the playhead itself follows the pointer 1:1. Hover on the timeline can show a time/preview tooltip with zero delay (it is a direct-manipulation surface, not a hint).
- Map and G-sensor chart: hover crosshair/readout should appear instantly (no fade) because it is data inspection; a 100–150 ms fade is acceptable only for tooltip chrome.
- Toolbar icon buttons: first tooltip after ~500–700 ms, then instant within ~300 ms; tooltips must show the keyboard shortcut; never show tooltips during a drag/scrub.
- Toggles (e.g. map off switch): thumb translate 120–160 ms with M3 FastSpatial-like spring or ease-out; colour change at the same time with no overshoot.
- Dialog focus (standard WAI-ARIA dialog pattern, not fetched in this session): move focus into the dialog on open (first field or the least-destructive button), trap Tab, Escape closes, return focus to the triggering control on close, `role="dialog"` + `aria-modal="true"` + `aria-labelledby`. In vanilla JS, native `<dialog>.showModal()` provides much of this.

### Gaps
- WAI-ARIA APG dialog page (w3.org) could not be fetched; the dialog focus rules above are from general knowledge plus Vercel's pointer to WAI-ARIA, not a fetched primary page.
- No primary source found for a specific "100 ms press feedback" rule beyond NN/g's 0.1 s limit and Apple's "highlight immediately."
- Rauno Freiberg's essay details on menus (e.g. safe-triangle submenu aiming), tooltips and scrubbing could not be verified because rauno.me was blocked.

## Perceived performance: optimistic UI, skeletons vs spinners, progress, content-visibility, layout shift, frame rate

### Takeaway
Respond within 100 ms, show nothing for waits under ~1 s (or delay indicators by 150–300 ms and keep them up ≥300–500 ms to avoid flicker), use skeletons that exactly mirror final layout for content loads, use determinate percent-done bars (with stages/estimates) for long jobs like export, and keep INP ≤200 ms.

### Cited Findings
- Vercel: add a show-delay of ~150–300 ms and a minimum visible time of ~300–500 ms for spinners or skeletons to avoid flicker; mutations should complete within a 500 ms budget. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Vercel optimistic UI: update immediately when success is likely, reconcile later; on failure show an error and roll back or offer Undo. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Vercel layout shift: skeletons must mirror final content exactly; set explicit media dimensions and reserve space; let CSS handle layout rather than measuring in JS; batch DOM reads/writes; move long tasks to Web Workers; virtualize large lists or use `content-visibility: auto`. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- NN/g: skeleton screens or spinners aren't necessary when a page loads in under a second (excerpt). — [NN/g, Skeleton Screens 101](https://nngroup.com/articles/skeleton-screens/)
- NN/g: two kinds of progress indicator, looped animation and percent-done; looped indicators are tempting for long waits because they need no estimate, but long waits warrant percent-done (excerpt). — [NN/g, Progress Indicators](https://nngroup.com/articles/progress-indicators)
- A secondary summary attributes to NN/g: indicator for actions over ~1 s, looped spinners for ~2–10 s, percent-done for longer. Unverified against NN/g directly. — [AWS Builder Center summary](https://builder.aws.com/content/3M2CqltW6KlyigfOOolCKaohj0D/stop-treating-a-spinner-as-a-default-design-loading-feedback-by-how-long-the-wait-is)
- Skeletons backfire when visible for under ~200 ms (developer opinion, not research). — [DEV Community](https://dev.to/helloashish99/skeleton-screens-vs-spinners-perceived-load-time-1nlj)
- File conversions, uploads/downloads and data imports should use progress bars or stage text rather than skeletons (secondary). — [UX Planet, Progress Indicators](https://uxplanet.org/progress-indicators-4-common-styles-91a12b86060c)
- INP: good ≤200 ms, poor >500 ms, measured at p75. — [web.dev, INP](https://web.dev/articles/inp)
- `content-visibility: auto` gives layout/style/paint containment and skips offscreen rendering; web.dev demo went from 232 ms to 30 ms render (~7x). Pair with `contain-intrinsic-size` (use `auto` keyword to remember last size) or elements collapse to 0 px and cause scroll jumps; do not apply to above-the-fold content. Baseline "newly available" since September 2024. — [web.dev, content-visibility](https://web.dev/articles/content-visibility); [Chrome, Defer rendering heavy content](https://developer.chrome.com/docs/modern-web-guidance/guides/performance/defer-rendering-heavy-content); [web.dev Baseline post](https://web.dev/blog/css-content-visibility-baseline.md.txt)
- Apple: 60 fps keeps fast motion smooth where 30 fps strobes. — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)

### Inferences
- DashLens loading card: don't flash it for fast local file parses — show it only after ~200 ms, and once shown keep it ≥400 ms. Prefer a determinate, staged indicator ("Reading 6 files… Parsing GPS 3/6… Building timeline") over a spinner, since file counts are known.
- Export progress bar: determinate percent, current stage, elapsed and estimated remaining time once a stable rate exists (e.g. after 2–3 s), a Cancel button, and a finished state with "Show file"/"Download again". Animate the bar via `transform: scaleX()` rather than `width`.
- Skeletons fit tile placeholders (16:9 boxes at final size), timeline track height and chart area — reserving exact space so nothing shifts when video metadata arrives.
- Events list / clip list with many items: `content-visibility: auto` + `contain-intrinsic-size: auto 48px` on rows, or virtualization if lists exceed a few hundred.
- Optimistic UI applies to local actions (rename, add marker, toggle map) — update instantly; for anything that can fail (export, file access), show a pending state.
- Keep canvas redraws to dirty regions and do heavy parsing (GPS/G-sensor extraction) in a Worker so input stays under the 200 ms INP bar and the 16.7 ms frame budget at 60 Hz.

### Gaps
- No fetched primary source for "16.7 ms frame budget" wording on web.dev (well known: 1000/60 ≈ 16.7 ms, but not cited here).
- NN/g's exact skeleton-vs-spinner thresholds could not be read in full.
- No research-grade source found on time-remaining estimate accuracy/smoothing for progress bars.

## Complete interface state checklist for a pro tool

### Takeaway
Design every surface for ideal, empty (first-run, user-cleared, zero results), loading, partial, and error states (Scott Hurff's "UI Stack"), then add the pro-tool states: offline/permission, disabled-with-reason, success/confirmation, destructive confirm/undo, long text/truncation, very many items, and interrupted/cancelled.

### Cited Findings
- Scott Hurff's UI Stack: ideal, empty/blank (split into first use, user-cleared, and no results), error, partial (sparsely populated; guide toward ideal), loading. Error questions: is data lost? are messages friendly and instructional, telling the user how to resolve? (secondary summaries). — [Scott Hurff, Why your UI is awkward](https://www.scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack/); [uxdesign.cc summary](https://uxdesign.cc/designing-for-different-ui-states-87d60130f85f)
- Vercel: show errors next to their source and focus the first error; use ellipses for placeholders signalling emptiness and for loading labels; warn before navigation when unsaved data could be lost; confirm destructive actions or provide Undo within a safe window; never disable zoom or paste. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- Vercel: don't pre-disable submit buttons — let the user try and show validation feedback instead. — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- NN/g response-time thresholds (0.1 s / 1 s / 10 s) set when loading states are required. — [NN/g](https://www.nngroup.com/articles/response-times-3-important-limits/)

### Inferences
Checklist for DashLens (each item = a designed state, with copy):
1. First-run / empty: drop zone + "Open files" button, supported formats, one-line privacy promise (files never leave the device), sample or keyboard hint. No blank canvases.
2. Drag-over: whole-window drop target highlight on dragenter (instant), distinct "can't use these files" state for unsupported types.
3. Loading: staged determinate loading card (delay ~200 ms, min ~400 ms), skeleton tiles/timeline at final size.
4. Partial data: some channels missing (e.g. rear camera absent), no GPS (map shows "No GPS in this clip" not an empty map), no G-sensor, gaps in timeline (labelled gaps), mismatched durations. Each panel states what is missing and why.
5. Error: per-file errors inline in the load summary (which file, what failed, what to do); codec unsupported; file unreadable; corrupt metadata. Errors on screen, not only in transient toasts.
6. Offline / blocked: map tiles unavailable offline → keep track drawn on plain background with a note; browser permission denied (File System Access) → explain and offer fallback.
7. Disabled with reason: disabled controls carry a tooltip/inline reason ("Export needs a selected range"); prefer enabled-then-explain where possible.
8. Busy / in-progress: export progress (percent, stage, ETA, cancel); buttons in loading state keep their label.
9. Cancelled / interrupted: export cancelled message; tab hidden mid-export.
10. Success: export complete with file name, size, "Show/Download again"; brief toast plus persistent state in the export panel.
11. Destructive confirm / undo: clearing loaded files, removing markers — Undo toast (~5–8 s) preferred over confirm modal for reversible actions; confirm modal with explicit verb button for irreversible ones.
12. Zero results: event filter or search with no matches → "No events match ‘X’" + clear-filter action (distinct from first-run empty).
13. Very many items: hundreds of clips/events → virtualized or `content-visibility` lists, grouped by day/trip, counts in headers, keyboard navigation.
14. Long text / truncation: long file names truncated in the middle (keep extension/timestamp), full name in tooltip/title; numbers in tabular figures so readouts don't jitter.
15. Focus / keyboard states: visible `:focus-visible` rings on canvas controls too; selected vs focused vs hovered distinct.
16. Reduced-motion and high-contrast variants of all the above.
17. Small viewport / narrow window: tiles stack, drawers become full-height sheets.

### Gaps
- No single authoritative, sourced "pro tool state checklist" exists; items 6–17 are synthesized from the sources above plus DashLens context.
- Undo-window durations (e.g. 5–8 s) are not from a fetched source.

## Sound and haptics in pro tools

### Takeaway
No source was found recommending sound or haptics for desktop pro web tools; for DashLens (where the user is listening to dashcam audio) UI sound should be off.

### Cited Findings
- Apple ties haptic/feedback discussion to direct touch and continuous feedback (e.g. Flashlight button tracking pressure), i.e. touch hardware, not desktop web. — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)

### Inferences
- DashLens should not add UI sounds: they would mix with the dashcam's own audio track, which may matter for evidence. The Vibration API is irrelevant on desktop and unsupported on iOS Safari (general knowledge, not sourced here).

### Gaps
- No primary source on sound/haptics usage in pro tools (Figma, Linear, video editors) was found in this session.

## Craft references and what each contributes

### Takeaway
The most actionable sources are Emil Kowalski's published standards (numbers for durations, curves, press scale, springs, frequency rule), Vercel's Web Interface Guidelines (loading-state timing, tooltips, focus, optimistic UI), Material 3 tokens (exact duration and easing scales), and Apple WWDC18 (interruptibility, springs by damping/response, rubber-banding, velocity projection).

### Cited Findings
- Emil Kowalski — creator of Sonner (toasts) and Vaul (drawers); his standards include the Vaul curve `cubic-bezier(0.32, 0.72, 0, 1)` and Sonner's 400 ms `ease` toast timing. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md); [emilkowal.ski](https://emilkowal.ski/ui/building-an-animation-course)
- Rauno Freiberg, "Invisible Details of Interaction Design" (July 2023): interactions modelled on physical properties such as interruptibility; iOS gestures as the reference. — [rauno.me](https://rauno.me/craft/interaction-design)
- Apple WWDC18 session 803 "Designing Fluid Interfaces": redirectable gestures, damping/response springs, rubber-banding, momentum projection, hysteresis 10 pt. — [Apple](https://developer.apple.com/videos/play/wwdc2018/803/); sample re-implementations: [nathangitter/fluid-interfaces](https://github.com/nathangitter/fluid-interfaces)
- Material 3 motion tokens and springs. — [Material Components Android, Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- Vercel Web Interface Guidelines. — [GitHub README](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- NN/g response time limits. — [NN/g](https://www.nngroup.com/articles/response-times-3-important-limits/)

### Inferences
- For DashLens's vanilla-JS single file, the CSS-first path is the right fit: CSS transitions with tokens, `@starting-style` for drawer/modal/toast entry, native `<dialog>`, WAAPI only for interruptible drags, and no animation library.

### Gaps
- Val Head's work, NN/g's animation articles and Emil's blog prose (beyond his standards file) could not be fetched in this session (network allowlist blocked emilkowal.ski, rauno.me, m3.material.io, nngroup.com, w3.org).
