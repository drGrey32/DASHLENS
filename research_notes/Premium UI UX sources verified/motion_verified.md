# Motion, micro-interactions and interface states: checked against primary sources

Scope: check every claim in `research_notes/Premium UI UX for DashLens/motion_interaction_states.md` that rested on a search summary or a mirror, plus every item in its Gaps, against the primary page. Each item is marked **CONFIRMED** (short exact quote + URL), **CORRECTED** (what the primary says instead), or **NOT FOUND** (the primary was read and the claim is not in it, or the primary could not be read). All pages below were fetched on 2026-11-26 unless noted. Numbers are given exactly as published.

Method note for the report writer: emilkowal.ski, rauno.me, nngroup.com, w3.org, radix-ui.com, web.dev, developer.apple.com (WWDC transcript and the HIG JSON feed) and valhead.com all returned full text. m3.material.io returned only an Angular app shell with no content, so Material 3 values were checked against Google's own Jetpack Compose source (`MotionTokens.kt` in androidx) and the Material Components Android `Motion.md`. linear.app's CSS files returned 404 to a non-browser fetch.

## Emil Kowalski: durations, easing, frequency rule, press scale, ease-in advice

### Takeaway
The blog posts confirm the core rules: UI motion under 300 ms, ease-out for entering and exiting, no ease-in, never animate keyboard-initiated actions, press scale 0.97, never start from scale(0). They also give the Sonner (400 ms `ease`) and Vaul (500 ms `cubic-bezier(0.32, 0.72, 0, 1)`) values. The tiered duration table, the custom `--ease-out` curve and the 160 ms press transition appear only in his STANDARDS.md file on GitHub, not in the blog prose.

### Cited Findings
Status of earlier claims
- **CONFIRMED** "shorter than 300ms" and ease-out (earlier a search excerpt): "The best type of easing for this purpose is ease-out. It starts fast and slows down at the end … Your animations should also usually be shorter than 300ms." — [Great Animations](https://emilkowal.ski/ui/great-animations)
- **CONFIRMED** the rule of thumb is repeated: "As a rule of thumb, UI animations should generally stay under 300ms." Also: "A 180ms dropdown animation feels more responsive than a 400ms one". — [You Don't Need Animations](https://emilkowal.ski/ui/you-dont-need-animations); same wording with a select example in [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
- **CONFIRMED** ease-out is the default: the easing flowchart from his course skill file, published on his blog, reads "Is the element entering or exiting the viewport? ├── Yes → ease-out … moving/morphing on screen? … ease-in-out … hover change? … ease … constant motion? … linear … Default → ease-out". — [Building an Animation Course](https://emilkowal.ski/ui/building-an-animation-course)
- **CONFIRMED, with different wording** ease-in advice. The blog does not say "Never use ease-in on UI"; it says: "You could decrease the duration to make ease-in work, but this easing is just not made for UI animations. It speeds up at the end, which is the opposite of what we want." Its demo compares two 300 ms dropdowns: "The duration for these dropdowns is identical, 300ms … but the ease-in one feels slower." — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips). The exact phrase "**Never `ease-in` on UI.**" is in his STANDARDS.md. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- **CONFIRMED** press scale: "A scale of 0.97 on the :active pseudo-class should do the job". The 160 ms transition (`transition: transform 160ms var(--ease-out)`) and the 0.95–0.98 range are only in STANDARDS.md. — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips); [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- **CONFIRMED** never start from scale(0): "Try animating from a higher initial scale instead (0.9+)". His demo uses "an initial scale of 0.93". — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
- **CONFIRMED** the frequency rule as prose. The blog states: "never animate keyboard initiated actions. These actions are repeated sometimes hundreds of times a day"; "Remove animations or hover interactions altogether if they are seen tens, maybe even hundreds of times a day"; and "A hover effect is nice, but if used multiple times a day, it would likely benefit the most from having no animation at all." The four-tier table ("100+ times/day … No animation. Ever.") and "a professional dashboard should be crisp and fast" are only in STANDARDS.md. — [Great Animations](https://emilkowal.ski/ui/great-animations); [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips); [You Don't Need Animations](https://emilkowal.ski/ui/you-dont-need-animations); [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)
- **NOT FOUND on the blog** the duration table (button press 100–160 ms, tooltips 125–200 ms, dropdowns 150–250 ms, modals/drawers 200–500 ms) and the custom curves `--ease-out: cubic-bezier(0.23, 1, 0.32, 1)` and `--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1)`. They are still present in STANDARDS.md, which was re-fetched today and is in Emil's own GitHub account (github.com/emilkowalski is linked from [emilkowal.ski](https://emilkowal.ski/)). Treat it as Emil's own writing, but not as blog-published. The spring `{ type: "spring", duration: 0.5, bounce: 0.2 }` and "Keep bounce subtle (0.1–0.3)" are also only in STANDARDS.md. — [STANDARDS.md](https://raw.githubusercontent.com/emilkowalski/skills/main/skills/review-animations/STANDARDS.md)

Sonner post (filled)
- **CONFIRMED** 400 ms `ease`: the CSS is `.sonner-toast { transition: transform 400ms ease; }`. He also gives the reason: "It's a bit slower than usual and uses ease as the easing type rather than ease-out to make it feel more elegant." — [Building a Toast Component](https://emilkowal.ski/ui/building-a-toast-component); [Great Animations](https://emilkowal.ski/ui/great-animations)
- **CONFIRMED** the swipe velocity of 0.11 (px/ms): "If the swipe amount is greater than the threshold or velocity is higher than in this case 0.11, I remove the toast", with the code comment "0.11 is just a number that I ended up on through trial and error". — [Building a Toast Component](https://emilkowal.ski/ui/building-a-toast-component)
- New: he moved from keyframes to transitions because "CSS transitions … can be interrupted and retargeted, even before the first transition has finished"; he notes that `@starting-style` "would make the implementation much simpler"; stacked toasts "scale them down by 0.05 * index"; "By default the toast disappears after 4 seconds unless you hover over it." — [Building a Toast Component](https://emilkowal.ski/ui/building-a-toast-component)

Vaul post (filled)
- **CONFIRMED** the Vaul curve and duration: `transition: transform 0.5s cubic-bezier(0.32, 0.72, 0, 1);` — "The curve used in Vaul closely matches the one used in iOS; it's from the Ionic Framework. Duration of 500ms is also supposed to mimic iOS's Sheet." — [Building a Drawer Component](https://emilkowal.ski/ui/building-a-drawer-component)
- New: "I added a timeout of 100ms, which prevents you from dragging in that time frame after you've reached the top again". He also updated the theme colour over 50 steps "every 10ms … because we have 50 colors and our CSS transition is 500ms". — [Building a Drawer Component](https://emilkowal.ski/ui/building-a-drawer-component)

Tooltips and other details (filled)
- Tooltip CSS from the blog: `transition: transform 0.125s ease-out, opacity 0.125s ease-out; transform-origin: var(--transform-origin);`, start/end state `opacity: 0; transform: scale(0.97)`, and `&[data-instant] { transition-duration: 0ms; }` for subsequent tooltips. "Once a tooltip is open, hovering over other tooltips should open them with no delay and no animation." — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
- Origin-aware popovers: "transform-origin … its default value is center, which is wrong in most cases." — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
- Blur: when a crossfade feels off, "try adding a bit of filter: blur()"; the demo uses "2px of blur". — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)
- Performance: animate "transform and opacity as they only trigger the third rendering step (composite)". Framer Motion "uses requestAnimationFrame under the hood, which is not hardware-accelerated", so it lags when the main thread is busy; "A hardware-accelerated animation will remain smooth, no matter how busy the main thread is." — [Great Animations](https://emilkowal.ski/ui/great-animations)
- Reduced motion example on the blog: `animation: bounce 0.2s` becomes `animation: fade 0.2s` under `prefers-reduced-motion: reduce` ("animates opacity only when the user prefers reduced motion"). — [Great Animations](https://emilkowal.ski/ui/great-animations)
- The course post shows 6 of "a set of 18 custom easings", for example `--ease-breeze: cubic-bezier(.55, .085, .68, .53)` and `--ease-crisp: cubic-bezier(.92, .06, .77, .045)`. All six shown are ease-in-shaped curves, and the post does not say what they are for. — [Building an Animation Course](https://emilkowal.ski/ui/building-an-animation-course)
- animations.dev is public only as a sales page. It lists topics ("How to choose the right easing and duration", "When to use spring animations") but publishes no numbers. — [animations.dev](https://animations.dev/)

### Inferences
- For DashLens, cite the blog for the rules (under 300 ms, ease-out, no ease-in, 0.97 press, no keyboard animation) and STANDARDS.md for the exact table and curves, labelled as Emil's skill file.
- The blog's 125 ms ease-out tooltip with `data-instant` 0 ms is a ready-made pattern for DashLens toolbar tooltips.
- Emil's main-thread point matters directly for DashLens: the canvas timeline, map and chart redraw on rAF, so UI chrome motion should be CSS or WAAPI on transform and opacity, never JS-driven.

### Gaps
- The 100–160 / 125–200 / 150–250 / 200–500 ms table and the `0.23, 1, 0.32, 1` curve are not on any emilkowal.ski page that was fetched; they rest on STANDARDS.md alone.
- animations.dev lesson content is paywalled.

## Rauno Freiberg: interruptibility, frequency, specific details

### Takeaway
The essay "Invisible Details of Interaction Design" (July 2023) confirms the interruptibility point, and its "Frequency & Novelty" section strongly supports no motion on high-frequency menus. It does not discuss safe-triangle submenus or tooltip timing.

### Cited Findings
- **CONFIRMED** interruptibility (earlier a search excerpt): "Great interactions are modeled after properties from the real world, like interruptability. … obviously flipping a page in a book is interruptible. But imagine if it were an animation that you had to wait for!" — [Rauno Freiberg, Invisible Details of Interaction Design](https://rauno.me/craft/interaction-design)
- Non-interruptible counterexample: in iOS Settings, "if you happen to mistap, then swiping back immediately does not interrupt the animation — you have to wait for it to end." — [rauno.me](https://rauno.me/craft/interaction-design)
- Frequency (filled): "if we for a moment consider the interaction frequency being hundreds of times a day, it does start to feel more like cognitive burden after seeing the same animation for the hundredth time." On his bookmarking tool: "After a couple of days they began to feel sluggish … I removed motion from core interactions and suddenly felt like I was moving much faster". — [rauno.me](https://rauno.me/craft/interaction-design)
- Keyboard and mouse: "Sometimes we can get away with not animating mouse or keyboard interactions, without it feeling jarring. … Pressing a key feels less visceral, and more mechanical than touching the screen." — [rauno.me](https://rauno.me/craft/interaction-design)
- Context menus: macOS context menus "appear without motion. Used thousands of times a day … Interestingly enough, the menu subtly fades out", and "the selected item briefly blinks the accent color … to provide assurance that the element was successfully selected." The macOS App Switcher "overlay never animates". — [rauno.me](https://rauno.me/craft/interaction-design)
- Responsive gestures: "Truly fluid gestures are immediately responsive"; apply the delta immediately, "and then performing an animation past a given threshold". — [rauno.me](https://rauno.me/craft/interaction-design)
- Sliders and scrubbing: "It helps to ensure that the dragging gesture does not cancel when moving away from the slider and still pressing down"; "Although seeking video is mostly a visual interaction, there's an unintelligible level of discomfort apparent when interacting with an element that you can't see." — [rauno.me](https://rauno.me/craft/interaction-design)
- Swipe trigger timing: lightweight actions trigger mid-gesture, while destructive ones wait: "triggering on gesture end, regardless of distance, feels right here." — [rauno.me](https://rauno.me/craft/interaction-design)
- Fitts's Law, screen corners and radial menus are discussed. The essay cites "C. Karunamuni, N. Vries, M. Alonso. Designing Fluid Interfaces (2018)", the WWDC18 talk. — [rauno.me](https://rauno.me/craft/interaction-design)
- **NOT FOUND** safe-triangle submenu aiming, tooltip timing and menu durations are not in this essay. The craft index lists only prototypes on related subjects ("Spatial Tooltip", "Toolbar Morph") and one other essay ("Novelty", February 2026), which was not read. — [rauno.me/craft](https://rauno.me/craft)

### Inferences
- DashLens's timeline scrub should keep capturing the pointer when it leaves the track vertically (Rauno's slider point; `setPointerCapture` does this).
- Context-menu style: appear instantly, fade out briefly, and flash the chosen item. This is a good model for DashLens right-click or overflow menus.

### Gaps
- Rauno's "Novelty" essay (Feb 2026) was not fetched; it may add frequency guidance.

## Material 3 motion: duration tokens, easing curves, exit vs entrance

### Takeaway
The 16 duration tokens and the standard and emphasized easing values are confirmed in Google's own Compose source. One earlier claim needs correcting: the "fade 150/75 ms" and "container transform 300/250 ms" defaults in Motion.md are legacy values that contradict that same file's M3 token table. m3.material.io itself could not be read.

### Cited Findings
- **NOT FOUND** (unreadable): m3.material.io/styles/motion/easing-and-duration/tokens-specs and /applying-easing-and-duration returned only an Angular shell (`/static/angular/main…js`) with no text. — [m3.material.io tokens-specs](https://m3.material.io/styles/motion/easing-and-duration/tokens-specs)
- **CONFIRMED** duration tokens in Google's Compose source: `DurationShort1 = 50.0`, `Short2 = 100.0`, `Short3 = 150.0`, `Short4 = 200.0`, `Medium1 = 250.0`, `Medium2 = 300.0`, `Medium3 = 350.0`, `Medium4 = 400.0`, `Long1 = 450.0`, `Long2 = 500.0`, `Long3 = 550.0`, `Long4 = 600.0`, `ExtraLong1 = 700.0` … `ExtraLong4 = 1000.0`. — [androidx MotionTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/MotionTokens.kt); same values in [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- **CONFIRMED** easing in Compose: `EasingStandardCubicBezier = (0.2f, 0.0f, 0.0f, 1.0f)`, `StandardDecelerate = (0.0f, 0.0f, 0.0f, 1.0f)`, `StandardAccelerate = (0.3f, 0.0f, 1.0f, 1.0f)`, `EmphasizedDecelerate = (0.05f, 0.7f, 0.1f, 1.0f)`, `EmphasizedAccelerate = (0.3f, 0.0f, 0.8f, 0.15f)`, `Linear = (0,0,1,1)`. Legacy (M2): `(0.4, 0, 0.2, 1)`, accelerate `(0.4, 0, 1, 1)`, decelerate `(0, 0, 0.2, 1)`. — [MotionTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/MotionTokens.kt)
- **CORRECTED** the "Emphasized in CSS" conflict. Google's own Compose tokens set `EasingEmphasizedCubicBezier = CubicBezierEasing(0.2f, 0.0f, 0.0f, 1.0f)`, the same as Standard, as a single-cubic stand-in. The Android View system uses the two-segment path `M 0,0 C 0.05, 0, 0.133333, 0.06, 0.166666, 0.4 C 0.208333, 0.82, 0.25, 1, 1, 1`. So the third-party packages that map Emphasized to `(0.2, 0, 0, 1)` follow Google's Compose tokens and are not wrong. The earlier note said the Android doc is "authoritative"; in fact both are official, for different platforms. — [MotionTokens.kt](https://raw.githubusercontent.com/androidx/androidx/androidx-main/compose/material3/material3/src/commonMain/kotlin/androidx/compose/material3/tokens/MotionTokens.kt); [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- **CONFIRMED** entrance vs exit roles (Motion.md descriptions): Standard Decelerate is "Easing used for utitlity focused animations that enter the screen"; Standard Accelerate is for those "that exit the screen"; Emphasized Decelerate and Accelerate are for M3-styled animations that "enter the screen" and "exit the screen". Rule: "In general, duration should increase as the area/traversal of an animation increases." — [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- **CORRECTED** component defaults. Motion.md's container transform table lists "Duration (incoming) | `motionDurationLong1` | … | `300ms`", "Duration (outgoing) | `motionDurationMedium2` | … | `250ms`" and easing "`cubic-bezier(0.4, 0.0, 0.2, 1)` `FastOutSlowIn`". The fade table lists "`motionDurationShort2` … `150ms`" in and "`motionDurationShort1` … `75ms`" out. But the same file's token table gives Long1 = 450 ms, Medium2 = 300 ms, Short2 = 100 ms and Short1 = 50 ms, and `(0.4, 0, 0.2, 1)` is the Legacy curve. The 300/250 and 150/75 figures are therefore legacy (M2-era) fallback values, not M3 tokens. The principle that exits are shorter than entrances still holds. — [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)
- **CONFIRMED** the six spring tokens: FastSpatial "`damping: 0.9, stiffness: 1400` | Spring for small components like switches and buttons"; FastEffects "`damping: 1, stiffness: 3800`"; DefaultSpatial "`damping: 0.9, stiffness: 700` | … bottom sheet or nav drawer"; DefaultEffects "`damping: 1, stiffness: 1600`"; SlowSpatial "`damping: 0.9, stiffness: 300` | Spring for full screen animations". SlowEffects (1/800) was not re-read on this pass. — [Motion.md](https://raw.githubusercontent.com/material-components/material-components-android/master/docs/theming/Motion.md)

### Inferences
- For DashLens CSS, `cubic-bezier(0.2, 0, 0, 1)` is a Google-sanctioned single-curve value for both Standard and Emphasized. Use `(0.05, 0.7, 0.1, 1)` for emphasized entrances and `(0.3, 0, 0.8, 0.15)` for exits if M3 parity is wanted.
- For the exit-shorter-than-entrance ratio, cite NN/g (300 vs 200–250 ms, below) rather than M3's legacy 150/75.

### Gaps
- The prose guidance on m3.material.io's "Applying easing and duration" page (for example, which token suits which transition size) could not be read.
- M3 Expressive (2025) spring values beyond the six Android tokens are still unverified.

## Apple: WWDC18 Designing Fluid Interfaces and the current HIG Motion page

### Takeaway
Every WWDC18 quote in the earlier note is confirmed in Apple's transcript except the deceleration constant and projection formula, which were on slides and are not in the transcript. The current HIG Motion page (fetched via Apple's JSON feed; last change September 9, 2025) adds three directly relevant rules: avoid motion on frequent interactions, let people cancel motion, and make motion optional.

### Cited Findings
WWDC18 (session 803) transcript
- **CONFIRMED** "If you introduce any amount of lag, things all of a sudden just kind of fall off a cliff"; "Everything needs to respond instantly." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** "we built a fully redirectable interface"; "the thought and gesture happen in parallel". — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** "It should have a consistent offscreen path as it enters and leaves." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** rubber-banding: "you actually wouldn't know the difference between a frozen phone, and phone that's just at the top of the edge of the screen". — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** frame rate: "two things both moving at 30 frames per second … the one on the right is moving so fast, that it's strobing"; "If we move it up to 60 frames per second, you can see that we can actually go a little bit faster, and still preserve smooth motion"; "it's not just about framerate. It's what's in the frames." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** springs: "damping, which controls how much or little overshoot there is from 100% damping, where there will be no overshoot to 0% damping where the spring would oscillate indefinitely"; "We actually like to avoid using duration when we're describing elastic behaviors, because it reinforces this concept of constant dynamic change"; "we recommend starting with 100% damping, or no overshoot"; "if the gesture that's driving the motion itself has momentum, then you should reward that momentum with a little bit of overshoot"; Music app "we use 100% damping … we use 80% damping"; "bounciness needs to be purposeful". The technical terms are "damping ratio and frequency response". — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **CONFIRMED** touch rules: "the button should highlight immediately when I touch down on it … But, we shouldn't confirm the tap until my touch goes up"; "hysteresis, and is usually 10 points in iOS"; "we don't use the last position. We use the history of the touch"; "the contents should stay attached to the gesture"; "provide continuous feedback during the interaction"; explanations: "Don't use it for a gesture that's used only intermittently." — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)
- **NOT FOUND in transcript** the UIScrollView normal deceleration rate (0.998 per ms) and the projection formula `(v/1000)·r/(1−r)`. The transcript says only "I'm just using the UIScrollView.DecelerationRate"; the code itself was on screen. — [Apple WWDC18](https://developer.apple.com/videos/play/wwdc2018/803/)

HIG Motion (filled; current page)
- "Add motion purposefully, supporting the experience without overshadowing it. Don't add motion for the sake of adding motion." — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion) (text read via [JSON feed](https://developer.apple.com/tutorials/data/design/human-interface-guidelines/motion.json))
- "Make motion optional. … avoid using it as the only way to communicate important information." — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- "Aim for brevity and precision in feedback animations. When animated feedback is brief and precise, it tends to feel lightweight and unobtrusive". — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- "In apps, generally avoid adding motion to UI interactions that occur frequently." — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- "Let people cancel motion. As much as possible, don't make people wait for an animation to complete before they can do anything, especially if they have to experience the animation more than once." — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- Games: "maintaining a consistent frame rate of 30 to 60 fps typically results in a smooth, visually appealing experience." visionOS: avoid sustained oscillation "that has a frequency of around 0.2 Hz". — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)
- The HIG Motion page gives no millisecond durations or curves. On watchOS, built-in easing "You can't turn off or customize". Change log: "September 9, 2025 Added guidance for Liquid Glass." — [Apple HIG, Motion](https://developer.apple.com/design/human-interface-guidelines/motion)

### Inferences
- The HIG's "avoid motion on frequent interactions" and "let people cancel motion" now give Apple-level backing to DashLens having zero animation on frame-step, play/pause, seek and tile focus, and to every drawer or modal transition being interruptible by Escape or a click.

### Gaps
- Apple publishes no ms durations or CSS-equivalent curves in the HIG; SwiftUI default spring numbers were not checked.
- The deceleration constant and projection code from the WWDC18 slides were not verified against Apple's sample code page.

## NN/g: animation duration, skeleton screens, progress indicators, response times

### Takeaway
All three NN/g articles are now read in full. Animation duration: 100–500 ms overall, about 100 ms for simple feedback, 200–300 ms for modals, 100–400 ms "in most cases", and 500 ms "a real drag". Loading: nothing under 1 s; spinner or skeleton for 2–10 s; percent-done for 10 s or more, or under 10 s when processing a known number of items. NN/g, unlike Emil, allows ease-in for exits.

### Cited Findings
Animation duration (Page Laubheimer, February 9, 2020) — gap filled
- "In general, the duration of most animations should be in the range of 100–500 ms, depending on complexity and on how far the element is traveling. As a rule of thumb, look for the shortest time that an animation can take without being jarring." — [NN/g, Executing UX Animations: Duration and Motion Characteristics](https://www.nngroup.com/articles/animation-duration/)
- "Simple feedback animations, such as showing a checkbox or toggle switch, should be roughly 100 ms (0.10 seconds) in total duration." — [NN/g](https://www.nngroup.com/articles/animation-duration/)
- "When animation involves substantial screen changes, such as when a modal window moves into view, a duration of 200–300 ms can be appropriate." — [NN/g](https://www.nngroup.com/articles/animation-duration/)
- "At 500ms, animations start to feel like a real drag for users … In most cases, a range of 100–400 ms is appropriate, with 400ms being a very slow animation, to be used only for big movements across large screens." — [NN/g](https://www.nngroup.com/articles/animation-duration/)
- Entrance vs exit: "objects appearing or entering the screen usually need a subtly longer duration than objects disappearing or exiting the screen: a popup window may take 300ms to appear, but only 200 or 250ms to disappear." — [NN/g](https://www.nngroup.com/articles/animation-duration/)
- Easing: "Most frequently, you'll want to use an ease-out animation … Ease-in and ease-in-out are sometimes used for elements leaving the screen, but that sort of easing curve can feel unresponsive if the initial motion takes a little while to get going." Its demo "uses ease-out when the box enters the frame, and ease-in when the box leaves the frame." This conflicts with Emil's "Never ease-in" and agrees with M3's accelerate-for-exit. — [NN/g](https://www.nngroup.com/articles/animation-duration/)
- Material's toggle: "a short (100ms) bit of feedback for a microinteraction". — [NN/g](https://www.nngroup.com/articles/animation-duration/)

Skeleton screens (Samhita Tankala, June 4, 2023; last reviewed Sep. 2, 2026)
- **CONFIRMED** "If a page takes less than 1 second to load, skeleton screens or spinners aren't necessary … the quick flashing page can cause users to feel like they can't keep up." — [NN/g, Skeleton Screens 101](https://www.nngroup.com/articles/skeleton-screens/)
- New thresholds: spinners "are best used when the page takes 2–10 seconds to load. Similarly, skeleton screens should be used with a wait time that's under 10 seconds. … progress bars are strongly recommended for any page that takes longer that 10 seconds". "Spinners are typically best used on a single module, like a video or a card which is on a dashboard." — [NN/g](https://www.nngroup.com/articles/skeleton-screens/)
- **CONFIRMED** (earlier secondary): "Whenever some other process (e.g., download, upload, convert a file) is involved, it does not make sense … to show a skeleton screen. Instead, show a progress bar". Also: "Do Not Use a Frame-Display Skeleton Screen", that is, one showing only a header, footer and empty background. "This specific type of progress indicator is used exclusively for full-page loads." — [NN/g](https://www.nngroup.com/articles/skeleton-screens/)

Progress indicators (Katie Sherwin, October 26, 2014)
- **CONFIRMED** the AWS secondary summary, with nuance: "Use a progress indicator for any action that takes longer than about 1.0 second." Looped: "This indicator should be reserved for actions that take between 2-10 seconds." Percent-done: "Use for actions that take 10 seconds or more." The summary line says "use a looped indicator for delays of 2–9 seconds and a percent-done indicator for delays of 10 seconds or more". — [NN/g, Progress Indicators Make a Slow System Less Insufferable](https://www.nngroup.com/articles/progress-indicators/)
- Exception relevant to DashLens: "A percent-done indicator may be used for actions that take less than 10 seconds, if the action involves processing a series of documents or registries … include a text explanation of the process, for example 'Updating address 3 of 50.' For actions that take a little while, give users the option to stop the process". — [NN/g](https://www.nngroup.com/articles/progress-indicators/)
- Estimates (fills the earlier gap on remaining-time display): "Start the progressive animation slower and allow it to move faster as it approaches the end"; "Provide a general time estimate. (Don't try to be exact …)", for example "About 3 minutes remaining"; "consider showing the number of steps"; "if the progress moves quickly only to hang on the last percentage remaining, the user will become frustrated". Avoid static "Loading…" indicators. — [NN/g](https://www.nngroup.com/articles/progress-indicators/)

Response times (Jakob Nielsen, 1993)
- **CONFIRMED** "0.1 second is about the limit for having the user feel that the system is reacting instantaneously"; "1.0 second is about the limit for the user's flow of thought to stay uninterrupted"; "10 seconds is about the limit for keeping the user's attention focused on the dialogue." — [NN/g, Response Times: The 3 Important Limits](https://www.nngroup.com/articles/response-times-3-important-limits/)
- **CORRECTED** wording: the earlier quote "to create the illusion of direct manipulation, a user interface must be faster than 0.1 second" is not in the article text (it came from the NN/g video page). The article says: "0.1 second: Limit for users feeling that they are directly manipulating objects in the UI"; "A delay of 0.2–1.0 seconds does mean that users notice the delay"; "Anything slower than 10 seconds needs a percent-done indicator as well as a clearly signposted way for the user to interrupt the operation." — [NN/g](https://www.nngroup.com/articles/response-times-3-important-limits/)

### Inferences
- DashLens loading card: parsing a known set of files fits NN/g's "series of documents" exception, so show "Reading file 3 of 6" with a determinate bar even for waits under 10 s, and offer Cancel.
- Export: percent-done plus a rough estimate ("About 2 minutes remaining") rather than a precise countdown; avoid a bar that stalls at the end.
- Durations: drawers and modals at 200–300 ms are inside both NN/g's and Emil's ranges; toggles at about 100 ms (NN/g), versus Emil's 100–160 ms press.

### Gaps
- None of the three articles gives a show-delay or minimum-display time for indicators; that guidance (150–300 ms delay, 300–500 ms minimum) remains Vercel's only.

## Radix Tooltip defaults

### Takeaway
Both defaults are confirmed on Radix's own page.

### Cited Findings
- **CONFIRMED** the Provider API reference: "delayDuration … number … 700", "skipDelayDuration … number … 300". The docs' example of overriding them globally is `<Tooltip.Provider delayDuration={800} skipDelayDuration={500}>`. — [Radix Primitives, Tooltip](https://www.radix-ui.com/primitives/docs/components/tooltip)
- Related: Emil writes that "Radix and Base UI … skip the delay once a tooltip is shown. Base UI allows you to skip the animation as well." — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)

### Inferences
- DashLens can copy these exactly: 700 ms first-show delay, a 300 ms window in which neighbouring tooltips open instantly, and a 0 ms transition for those instant tooltips.

### Gaps
- None.

## WAI-ARIA APG modal dialog: focus rules

### Takeaway
The APG page is now read. Its focus rules match the earlier note's general-knowledge list, with more detail on initial focus placement and on where focus goes after close.

### Cited Findings
- "When a dialog opens, focus moves to an element inside the dialog." "Generally, focus is initially set on the first focusable element." When the content is long or structured, put `tabindex="-1"` on a static element at the top (such as the title) and focus that. — [WAI-ARIA APG, Dialog (Modal) Pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
- Destructive steps: "it may be advisable to set focus on the least destructive action, especially if undoing the action is difficult or impossible." Informational or continue dialogs: focus "the element that is likely to be most frequently used, such as an OK or Continue button." — [APG](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
- Tab: "If focus is on the last tabbable element inside the dialog, moves focus to the first tabbable element inside the dialog"; Shift+Tab does the reverse; "Escape: Closes the dialog." — [APG](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
- "When a dialog closes, focus returns to the element that invoked the dialog unless either: The invoking element no longer exists … [or] The task completed in the dialog is directly related to a subsequent step in the work flow." — [APG](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
- "It is strongly recommended that the tab sequence of all dialogs include a visible element with role button that closes the dialog". — [APG](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
- Roles: "role of dialog"; "aria-modal set to true"; `aria-labelledby` pointing to a visible title, or `aria-label`; `aria-describedby` optional, and best omitted for structured content. Mark a dialog modal only when "Application code prevents all users from interacting in any way with content outside of it" and "Visual styling obscures the content outside of it." "Windows under a modal dialog are inert." — [APG](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)

### Inferences
- In DashLens, after "Clear all files" the invoking button may no longer exist, so focus should go to the empty-state "Open files" button (the APG "logical work flow" rule).
- For the export dialog's final irreversible step, focus Cancel first.

### Gaps
- None for this pattern. Whether native `<dialog>.showModal()` meets every APG rule (for example, the Tab wrap) was not checked here.

## web.dev: INP thresholds and content-visibility

### Takeaway
Both are confirmed on web.dev.

### Cited Findings
- **CONFIRMED** INP: "An INP below or at 200 milliseconds means a page has good responsiveness. An INP above 200 milliseconds and below or at 500 milliseconds means a page's responsiveness needs improvement. An INP above 500 milliseconds means a page has poor responsiveness", measured at "the 75th percentile of page loads recorded in the field". For pages with many interactions, "we ignore one highest interaction for every 50 interactions." — [web.dev, INP](https://web.dev/articles/inp)
- **CONFIRMED** content-visibility: "rendering times going from 232ms to 30ms on initial page load"; "That's a 7x performance boost"; "content-visibility: auto gains layout, style and paint containment"; with the `auto` keyword "if you specified contain-intrinsic-size: auto 300px", the browser remembers the last rendered size; off-screen content stays in the DOM and accessibility tree. Also: "Facebook engineers observed an up to 250ms improvement in navigation times when going back to previously cached views." — [web.dev, content-visibility](https://web.dev/articles/content-visibility)

### Inferences
- These numbers support the earlier inferences (Worker parsing, `content-visibility` on long event lists) unchanged.

### Gaps
- The "Baseline newly available, September 2024" claim and the "16.7 ms frame budget" wording were not re-checked on this pass.

## Val Head: UI animation guidance

### Takeaway
valhead.com is a portfolio landing page with no guidance of its own; it links to her articles. Her Smashing Magazine article on reduced motion gives guidance that fits DashLens: replace large movement with crossfades, cut parallax, and keep the meaning of the motion.

### Cited Findings
- valhead.com describes her as "the author of Designing Interface Animation and a Principal Designer at Adobe specializing in UX animation" and lists "Designing With Reduced Motion For Motion Sensitivities" under recent articles. — [valhead.com](https://valhead.com/)
- "Can the animation easily be adjusted to use a non-motion effect like an opacity fade or crossfade for reduced motion requests? Would pausing the motion or removing the effect entirely for reduced motion preserve the meaning of the content?"; "You don't want to unintentionally remove content or degrade the overall experience." — [Val Head, Designing With Reduced Motion For Motion Sensitivities (Smashing, Sep 8, 2020)](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/)
- "Large page transition effects can likely be replaced with a crossfade effect for a reduced motion mode. The same is usually true for large zooming or spinning transitions". "Parallax effects and exaggerated smooth scrolling effects are universally triggering … should be significantly reduced or entirely removed". — [Smashing](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/)
- Her code example replaces a looping bounce with `animation: fade 0.5s ease-in both;` under reduced motion. — [Smashing](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/)
- She suggests a visible custom motion toggle for motion-heavy sites, or a setting in an existing preferences panel, which defaults to the OS `prefers-reduced-motion` value. — [Smashing](https://www.smashingmagazine.com/2020/09/design-reduced-motion-sensitivities/)
- NN/g's duration article cites "Head, V. (2016) Designing Interface Animation. Rosenfeld". — [NN/g](https://www.nngroup.com/articles/animation-duration/)

### Inferences
- Under reduced motion, DashLens drawers and modals become crossfades; scrub-following elements are unaffected because they are data, not decoration.

### Gaps
- Her book's duration and easing numbers were not checked (not online).

## Linear and Vercel production easing values; other earlier claims

### Takeaway
vercel.com's live CSS defines three easing variables that equal Tailwind's default easing values. Linear's CSS could not be fetched. The Vercel Web Interface Guidelines and Scott Hurff's UI Stack, both cited earlier, are confirmed.

### Cited Findings
- vercel.com production CSS (fetched from the homepage's stylesheets) defines `--ease-in-out:cubic-bezier(.4, 0, .2, 1)`, `--ease-in:cubic-bezier(.4, 0, 1, 1)` and `--ease-out:cubic-bezier(0, 0, .2, 1)`. — [vercel.com](https://vercel.com) (stylesheets linked from the homepage)
- **NOT FOUND** Linear: the linear.app homepage references `/_next/static/css/*.css`, but each returned "Not Found" (404) to a non-browser fetch. — [linear.app](https://linear.app)
- **NOT FOUND** separate Geist motion tokens were not located.
- **CONFIRMED** Vercel Web Interface Guidelines: "add a short show-delay (~150–300 ms) & a minimum visible time (~300–500 ms) to avoid flicker"; "Delay the first tooltip in a group; subsequent peers have no delay"; "Animations are cancelable by user input"; "`POST/PATCH/DELETE` complete in <500ms". — [Vercel Web Interface Guidelines](https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/README.md)
- **CONFIRMED** Scott Hurff's UI Stack on his own site: "every screen you'll design for your product can have up to five states": Ideal, Empty, Error, Partial, Loading. "There are three broad versions of the empty state": first use, "User-cleared data" and "No results". — [Scott Hurff, Why your UI is awkward](https://www.scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack/)

### Inferences
- The three vercel.com values match Tailwind CSS's default `ease-in`, `ease-out` and `ease-in-out` (and M2's legacy curves in Compose: `(0.4,0,0.2,1)`, `(0.4,0,1,1)`, `(0,0,0.2,1)`). This match is from background knowledge plus the Compose file; it is not stated by Vercel. So Vercel's marketing site uses stock curves; there is no published, Vercel-specific "house curve".
- For DashLens, prefer Emil's stronger ease-out (STANDARDS.md) or M3's `(0.2, 0, 0, 1)` over the weak stock ease-out, consistent with Emil's remark that "The built-in easing curves in CSS are usually not strong enough". — [7 Practical Animation Tips](https://emilkowal.ski/ui/7-practical-animation-tips)

### Gaps
- Linear's production easing values remain unverified; a browser fetch (with cookies and headers) would be needed.
- Undo-window durations (5–8 s) and sound/haptics in pro tools remain unsourced, as in the earlier note.
