# Visual craft of premium dark tool UIs (for DashLens)

Research notes, 2026-11-26. Scope: typography, spacing, colour, depth, icons and fine detail in a dense, dark, data-heavy tool (DashLens: synced video tiles, timeline, GPS map, G-sensor chart, settings drawer, export; dark UI, one accent `#ffb020`).

Method note: WebFetch could not resolve vercel.com, linear.app or rauno.me in this session, so pages were downloaded with curl and read as text. Apple HIG was read from its JSON data endpoint. Material Design 2 dark-theme figures came from search-result summaries, not a direct page read (marked below). Medium and uxdesign.cc returned 403, so Refactoring UI material is limited to its free preview page. Dates are given where known. Sources older than 2020 are flagged.

Current DashLens tokens (from `/home/user/DASHLENS/index.html`, line 30–35): `--bg:#0a0c0f; --bg2:#0f1217; --panel:#141820; --panel2:#1a1f28; --line:#20262f; --line2:#2c3340; --line3:#3d4656; --text:#dfe4ea; --text2:#c9d0d9; --muted:#9aa4b2; --dim:#7f8896; --acc:#ffb020; --teal:#35c3d6; --red:#ff5d5d`. Contrast figures for these are in the colour section.

---

## Typography: typefaces, scales, tabular numerals, optical size, tracking, line-height, weights, smoothing, how many sizes

### Takeaway
Premium tools use one neo-grotesque sans with an optical-size axis (Inter / Inter Display at Linear, SF at Apple, Geist plus Geist Mono at Vercel), a small scale clustered tightly at 12–14 px for UI, size-dependent tracking (slightly positive at 11–12 px, negative from 13 px up), tabular figures for every number that changes or gets compared, and regular-to-semibold weights only. On dark backgrounds, avoid thin weights and use grayscale smoothing on macOS, which makes light text look slightly lighter.

### Cited Findings
- **Linear (Mar 2024 redesign):** "We started using Inter Display to add more expression to our headings while maintaining their readability and kept using regular Inter for the rest of the text elements." — [Linear, How we redesigned the Linear UI (part II)](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Inter has an optical-size axis.** It runs from "text" to "display". The "text" designs have "a tall x-height to aid in legibility of lower-case text, with several contrast-enhancing details like ink traps and bridges". The "display" designs have "clean lines, smooth curves and delicate details". Weights run 100–900, with dedicated masters at 100, 400 and 900. — [Inter (rsms.me)](https://rsms.me/inter/)
- **Inter OpenType features useful for data UIs:**
  - `tnum` gives tabular figures, "the same width across all weights".
  - `zero` gives a slashed zero.
  - `ss01` gives open digits.
  - `ss02` disambiguates characters (with zero) and `ss04` does so without the zero.
  - `case` gives case-sensitive forms.
  - `cv01`–`cv09` are character variants, e.g. alternate 1, open 4/6/9, flat-top 3, lower-case l with tail, serifed capital I.

  — [Inter](https://rsms.me/inter/)
- **Inter "Dynamic Metrics" tracking formula (Inter v3 site, older and archived).** `tracking(em) = a + b·e^(c·z)` with a = −0.0223, b = 0.185, c = −0.1745 and z = font size in px. — [Inter v3 Dynamic Metrics (archived)](https://d.rsms.me/inter-website/v3/dynmetrics/)

  Computed values: 11 px ≈ +0.005 em, 12 px ≈ 0, 13 px ≈ −0.003 em, 14 px ≈ −0.006 em, 16 px ≈ −0.011 em, 20 px ≈ −0.017 em, 24 px ≈ −0.020 em, 32 px ≈ −0.022 em. These are my calculations from the published constants.
- **Apple SF Pro tracking table (current HIG), in 1/1000 em:**

  | Size (pt) | 6 | 8 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 |
  |---|---|---|---|---|---|---|---|---|---|---|
  | Tracking | +41 | +26 | +12 | +6 | 0 | −6 | −11 | −16 | −20 | −26 |

  The rule is that small text is opened up and text from 13 pt upward is tightened. — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Apple dynamic optical sizes:** SF and New York "support dynamic optical sizes, which merge discrete optical sizes (like Text and Display) and weights into a single, continuous design". — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Apple default and minimum text sizes:** macOS default 13 pt, minimum 10 pt; iOS default 17 pt, minimum 11 pt. — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **macOS built-in text styles (the desktop-tool reference), size/line height in pt:**
  - Body Regular 13/16
  - Headline Bold 13/16
  - Callout 12/15
  - Subheadline 11/14
  - Footnote and Caption 10/13
  - Title 3 15/20, Title 2 17/22, Title 1 22/26, Large Title 26/32

  The 13 pt body has a line height of about 1.23. Emphasis is done by weight (Regular to Semibold or Bold), not by a new size. — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Apple on weights and typefaces:** "In general, avoid light font weights… prefer Regular, Medium, Semibold, or Bold… avoid Ultralight, Thin, and Light". Also "Minimize the number of typefaces you use, even in a highly customized interface." — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Vercel Geist type system: separate "Label" and "Copy" styles.**
  - Label is for single lines, "given ample line-height for highlighting & marrying up with icons".
  - Copy is for multi-line text with a higher line height.
  - Label 14 is the "most common text style of all. Used in many menus."
  - Label 13 is "a secondary line next to other labels. Tabular is used when conveying numbers for consistent spacing."
  - Label 12 (with CAPS) is "for tertiary level text in busy views".
  - Copy 14 is the "most commonly used text style". Copy 13 is "for views where space is a premium".
  - Mono sizes 12/13/14 are paired one step down from the sans size: "Label 13 Mono… to pair with Label 14, as the smaller mono size looks better in that pairing".
  - Button sizes are 16/14/12, with 14 as the default.

  — [Vercel Geist, Typography](https://vercel.com/geist/typography)
- **Vercel on numbers:** "Tabular numbers for comparisons. Use `font-variant-numeric: tabular-nums` or a monospace like Geist Mono." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines) (mirror: [GitHub](https://github.com/vercel-labs/web-interface-guidelines))
- **Vercel on text rendering:** "Scaling text can change smoothing. Prefer animating a wrapper instead of the text node. If artifacts persist set `translateZ(0)` or `will-change: transform`". — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Font smoothing (MDN):** `-webkit-font-smoothing: antialiased` and `-moz-osx-font-smoothing: grayscale` work only on macOS. "Switching from subpixel rendering to anti-aliasing for light text on dark backgrounds makes it look lighter." The property is non-standard. — [MDN, font-smooth](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-font-smoothing)
- **Light text on dark looks heavier (NN/g, c. 2023):** "Thin fonts can be easily 'swallowed up' by a dark background… Thick (or bolded) fonts can seem to 'bleed' into the background… light fonts on dark backgrounds tend to appear bolder than dark fonts with the same font weight on light backgrounds." — [NN/g, Dark Mode: How Users Think About It and Issues to Avoid](https://www.nngroup.com/articles/dark-mode-users-issues/)
- **Small text is harder in dark mode (NN/g, 2020).** Research reviewed by NN/g found that "the positive-polarity advantage increased linearly as the font size was decreased". At simulated night-time, "it was much harder for people to read small-font text in dark mode". — [NN/g, Dark Mode vs. Light Mode](https://www.nngroup.com/articles/dark-mode/)
- **Vercel copy and number details:**
  - Use the `…` character, not three periods.
  - Use curly quotes.
  - Put a non-breaking space between number and unit (`10&nbsp;MB`).
  - Use numerals for counts.
  - Format numbers and dates for the user's locale.

  — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)

### Inferences
- **Scale for DashLens:**
  - 11 px for caps micro-labels, using tracking of about +0.04–0.06 em (my extrapolation for all-caps).
  - 12 px for secondary and axis labels.
  - 13 px for default UI text.
  - 14 px for panel titles.
  - 16–20 px only for the drop-zone and empty-state heading.

  That is five sizes and two to three weights (400, 500, 600). It matches the Geist cluster (12/13/14) and macOS (10–13 for body text).
- Use `font-variant-numeric: tabular-nums` on the timecode, speed, G-values, coordinates, file sizes and timeline ticks. Without it, a playing timecode jitters horizontally, which is a very visible amateur tell.
- Optionally use slashed zero (`zero`) on GPS coordinates and timestamps used as evidence, so 0 and O cannot be confused.
- **Self-contained file constraint:** DashLens is one HTML file, so a webfont means embedding or subsetting it. A system stack is a defensible premium choice: `-apple-system, BlinkMacSystemFont, "Segoe UI Variable", "Segoe UI", Inter, system-ui, sans-serif` (SF on Mac gets dynamic optical sizes for free). Then use `ui-monospace, "SF Mono", "Cascadia Mono", Menlo, monospace` for timecodes. The font-stack names are my synthesis, not sourced.
- Apply `-webkit-font-smoothing: antialiased` on the dark UI for a crisper, lighter look on macOS. Compensate by not going below weight 400, and use 500 for small labels.

### Gaps
- I could not read Raycast's, Arc's, Figma's or Stripe's own type specs. Figma's help page downloaded but was not about type.
- Linear's exact sizes, weights and tracking values are not published in the redesign post. Only "Inter Display for headings, Inter for the rest" is confirmed.
- The current Inter v4 site no longer publishes the dynamic-metrics formula (the page now 404s). With v4, optical sizing is meant to be handled by the `opsz` axis plus `font-optical-sizing: auto`. I could not verify whether the old tracking guidance still applies to v4.

---

## Spacing and layout: grids, density, alignment, optical alignment, radii, hit targets

### Takeaway
Hard numbers that are sourced:
- Hit targets of at least 24×24 CSS px (WCAG 2.2 AA; 44 px on touch).
- Child radius no larger than the parent radius, and concentric with it.
- Radii from a small fixed set (Geist uses 6 / 12 / 16 px by elevation).
- Optical ±1 px corrections.
- Every element aligned to something on purpose.

The 4/8-pt grid is industry practice, but I found no primary source for it this session.

### Cited Findings
- **Hit targets (Vercel):** "Match visual & hit targets. Exception: if the visual target is < 24px, expand its hit target to ≥ 24px. On mobile, the minimum size is 44px." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Hit targets (WCAG 2.2, SC 2.5.8 Target Size Minimum, Level AA):** "at least 24 by 24 CSS pixels". The exception is undersized targets spaced so that a 24 px circle centred on each does not intersect another target. — [W3C, Understanding SC 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
- **Nested radii:** "Child radius ≤ parent radius & concentric so curves align." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Geist radius presets tied to elevation:**
  - Base and Small surfaces: 6 px.
  - Medium and Large: 12 px.
  - Tooltip: 6 px ("the only floating element with a triangular stem").
  - Menu and Modal: 12 px.
  - Fullscreen: 16 px.

  Also: "Don't stack two Materials on the same element" and "Favor the lowest elevation that still reads as elevated… over-elevating is a common source of visual noise." — [Vercel Geist, Materials](https://vercel.com/geist/materials)
- **Optical alignment:** "Adjust ±1px when perception beats geometry." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Deliberate alignment:** "Every element aligns with something intentionally whether to a grid, baseline, edge, or optical center. No accidental positioning." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Icon and text lockups:** "When text & icons sit side by side, adjust weight, size, spacing, or color so they don't clash… a thin-stroke icon may need a bolder stroke next to medium-weight text." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Linear's alignment work is felt rather than seen:** "I also spent time aligning labels, icons, and buttons, both vertically and horizontally in the sidebar and tabs… This part of the redesign isn't something you'll immediately see but rather something that you'll feel after a few minutes of using the app." — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Linear on density:** The redesign aimed to "reduce visual noise, maintain visual alignment, and increase the hierarchy and density of navigation elements". The team "tested a lot of options, from very condensed to more spacious configurations" and "often relied on Apple standards". — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Dead zones and forgiving targets:** "No dead zones. If part of a control looks interactive, it should be interactive." The guidelines also call for generous hit targets and prediction cones for menus. — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Fitts's law in practice:** Screen edges and corners are effectively infinite targets. Rauno also notes that a slider drag should not cancel when the pointer leaves the slider while still pressed. — [Rauno Freiberg, Invisible Details of Interaction Design (Jul 2023)](https://rauno.me/craft/interaction-design)
- **Scrollbars:** "Only render useful scrollbars; fix overflow issues… On macOS set 'Show scroll bars' to 'Always' to test what Windows users would see." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)

### Inferences
- **Spacing scale:** Use a 4 px base with steps 4, 8, 12, 16, 24 and 32. Use a 2 px step only inside controls, such as the icon-to-label gap inside a chip. Control heights: 24 px for compact toolbar buttons (the WCAG minimum), 28–32 px for standard buttons, and 32–36 px for the drawer's form rows.
- **Radii:** Use three values, roughly 4 px for chips/inputs, 8 px for panels/tiles and 12 px for drawer/modal. Apply concentricity as outer radius = inner radius + padding. For example, a 6 px button inside a 4 px-padded group gets a 10 px group radius. The formula is common practice and consistent with Vercel's "concentric" rule, but the exact formula is not stated in the fetched sources.
- **Video tiles:** These should have small radii (around 4–6 px) or none. Large radii on video waste picture and look consumer-grade next to pro video tools. This is my judgement, not sourced.
- **Timeline:** The playhead hit area should be much wider than its 1–2 px visual line (at least 24 px wide drag zone), and the scrub should keep tracking when the pointer leaves the track, as Rauno describes for sliders.

### Gaps
- I found no primary source this session for the 4/8-pt grid (e.g. Material's 8 dp grid or Refactoring UI's spacing scale), because Medium returned 403 and the m2/m3 pages are JS-rendered.
- I found no published density specs (row heights) for Linear, Raycast or Figma.

---

## Dark UI colour: no pure black, elevation, neutral ramps, tinted neutrals, accents, contrast (WCAG vs APCA), borders vs shadows, semantic tokens

### Takeaway
- Use dark grey, not black.
- Show elevation with lighter surfaces, not shadows.
- Build colours from a perceptually uniform space (LCH/OKLCH): Linear generates its whole theme from three inputs (base, accent, contrast).
- Map a 12-step ramp to fixed roles (Radix).
- Keep chroma low in the neutrals.
- Measure text against APCA levels, because WCAG 2 overstates contrast near black.

DashLens's current muted greys pass WCAG comfortably but sit at only about Lc 38–52 in APCA.

### Cited Findings
- **Not pure black (Refactoring UI, 2018, older):** "True black tends to look pretty unnatural, so start with a really dark grey". You need "8-10 shades" of grey. "Don't get clever using CSS preprocessor functions like 'lighten' or 'darken'… That's how you end up with 35 slightly different blues". — [Refactoring UI, Building Your Color Palette](https://www.refactoringui.com/previews/building-your-color-palette)
- **Material Design 2 dark theme (2019, older; via search summaries, not a direct page read):**
  - The recommended surface is `#121212`, not black.
  - Text on dark uses white at 87% (high emphasis), 60% (medium) and 38% (disabled).
  - Elevated surfaces get a white overlay from 0% to 16% (1 dp 5%, 4 dp 9%, 24 dp 16%). Flutter's implementation formula is `(4.5·ln(elevation+1)+2)/100`.
  - Accents use the desaturated 200 tone of the primary to keep at least 4.5:1 at all elevations.

  — [Material Design 2, Dark theme](https://m2.material.io/design/color/dark-theme); [Google codelab, Design a dark theme](https://codelabs.developers.google.com/codelabs/design-material-darktheme/); [Flutter commit implementing overlay](https://flutter.googlesource.com/mirrors/flutter/+/e17f8d367d1f1f01b99fd858881c70729fb27318%5E%21)
- **Apple base vs elevated:** "In Dark Mode, the system uses two sets of background colors — called base and elevated… The base colors are dimmer, making background interfaces appear to recede, and the elevated colors are brighter, making foreground interfaces appear to advance." Dark colours "aren't necessarily inversions of their light counterparts". — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Apple on media apps:** "it can make sense for an app that supports immersive media viewing to use a permanently dark appearance that lets the UI recede and helps people focus on the media". This directly justifies DashLens being dark-only. — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Apple contrast targets:** At least 4.5:1, and "For custom foreground and background colors, strive for a contrast ratio of 7:1, especially in small text." Also: "Soften the color of white backgrounds" in images so they don't glow. — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Depth on dark (NN/g):** "placing a black element on a black background can be problematic because a lighter 'shadow'… makes the top element look like it's glowing. The best way to create depth… is to use the darkest colors for the page elements on the bottom, and the lightest colors for the elements on top". — [NN/g, Dark Mode issues](https://www.nngroup.com/articles/dark-mode-users-issues/)
- **Dark-mode issues to avoid (NN/g):**
  - Scrims are "far less visible in dark mode".
  - "Thin, gray dividers are easily swallowed up on very dark backgrounds". Use "slight color differentiation to distinguish a card", not only outlines.
  - "Highly saturated colors on dark backgrounds have poor visibility". The example is a saturated blue at 4.59:1 that "seems to blur".
  - For text, "use one color with different levels of opacity" so it works on several surfaces.

  — [NN/g, Dark Mode issues](https://www.nngroup.com/articles/dark-mode-users-issues/)
- **Linear's theme engine:** "instead of having to define 98 specific variables for each theme, we defined three: base color, accent color, and contrast". LCH was chosen because "a red and a yellow color with lightness 50 will appear roughly equally light". It handles "different elevations for our surfaces (e.g. background, foreground, panels, dialogs, and modals)". The contrast variable auto-generates high-contrast themes. — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Linear's neutrals and process:** Linear reached "a more neutral and timeless appearance… by limiting how much chrome (blue in our case) was used in the calculations". Text and neutral icons were made "lighter in dark mode" for contrast. Early exploration "mostly worked with opacities of black and white" to set elevation and hierarchy. — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Radix 12-step roles:**
  - 1 app background
  - 2 subtle background
  - 3 UI element background
  - 4 hover
  - 5 active/selected
  - 6 subtle borders and separators (non-interactive)
  - 7 UI element border and focus rings
  - 8 hovered border, strong borders and focus rings
  - 9 solid (highest chroma)
  - 10 hovered solid
  - 11 low-contrast text
  - 12 high-contrast text

  "Steps 11 and 12… are guaranteed to Lc 60 and Lc 90 APCA contrast… on top of a step 2 background". Amber and Yellow step 9 "are designed for dark foreground text". — [Radix Colors, Understanding the scale](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **Geist colour usage:**
  - Gray is for "text, icons, fills, borders, and dividers by default".
  - Gray-alpha is used "only when the background should show through, such as in shadows or overlays". Overlapping alpha borders make intersections stand out.
  - Background 1 is the default and Background 2 is used sparingly.
  - Three component backgrounds cover default, hover and active.
  - Three border strengths cover default, hover and active.

  — [Vercel Geist, Colors](https://vercel.com/geist/colors)
- **Vercel colour rules:**
  - "Layered shadows. Mimic ambient + direct light with at least two layers."
  - "Crisp borders. Combine borders & shadows; semi-transparent borders improve edge clarity."
  - "Hue consistency. On non-neutral backgrounds, tint borders/shadows/text toward the same hue."
  - "Interactions increase contrast. `:hover`, `:active`, `:focus` have more contrast than rest state."
  - "Set `color-scheme: dark`… so that scrollbars and other device UI have proper contrast."
  - Set `<meta name="theme-color">` to the page background.
  - Native `<select>` needs explicit `background-color` and `color` to avoid Windows dark-mode bugs.

  — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Vercel on contrast measures:** "Prefer APCA over WCAG 2 for more accurate perceptual contrast." Shadow contrast "on dark backgrounds is weaker than on light, so confirm separation still reads". — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines); [Geist Materials](https://vercel.com/geist/materials)
- **APCA (its own documentation):** WCAG 2.x "overstates contrast for dark colors to the point that 4.5:1 can be functionally unreadable when one of the colors in a pair is near black… WCAG 2.x contrast cannot be used for guidance designing 'dark mode'." Bronze levels:
  - **Lc 90:** preferred body text (≥14 px/400), and non-body text ≥12 px/400.
  - **Lc 75:** minimum for body text at 18 px/400, 16 px/500 or 14 px/700, and for non-body text ≥15 px/400.
  - **Lc 60:** minimum for "text you want people to read" that is not body text. The minimums are 24 px/400, 18 px/600 and 16 px/700; add Lc 15 to use these sizes as body text.
  - **Lc 45:** large or heavy text, and "pictograms with fine details, or smaller outline icons".
  - **Lc 30:** placeholder, disabled and "spot readable" text, and solid icons.
  - **Lc 15:** dividers and non-semantic elements. Below this, treat as invisible.

  — [APCA in a Nutshell](https://git.apcacontrast.com/documentation/APCA_in_a_Nutshell.html)

  Caveat: APCA describes itself as "the candidate contrast method for the future WCAG 3". That status is self-reported. WCAG 2.2 AA (4.5:1 text, 3:1 non-text) remains the legal and accessibility baseline.
- **Stripe (2019, older):** Stripe rebuilt its palette in CIELAB so that "each color… has the same contrast value at a given level" across hues, keeping vibrancy while passing WCAG. "Really dark yellow isn't actually a thing", so yellow and orange scales are gamut-limited at the dark end. — [Stripe, Designing accessible color systems](https://stripe.com/blog/accessible-color-systems)
- **OKLCH in CSS (Evil Martians, updated 2024–25):** `oklch()` lightness is perceptual, "unlike L in hsl()". It suits generated palettes and can express P3 wide-gamut colours, which add about 30% more colours on modern Apple and OLED screens. — [Evil Martians, OKLCH in CSS](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl)
- **Dark mode trade-offs (NN/g):** For normal vision, light mode tends to perform better, especially for small text. Dark mode helps some low-vision users (e.g. cataracts). Many users simply prefer it. — [NN/g, Dark Mode vs. Light Mode (2020)](https://www.nngroup.com/articles/dark-mode/)

**DashLens token contrast.** I calculated WCAG 2 ratios exactly. APCA Lc values come from my own re-implementation of the APCA-W3 0.0.98G constants, so treat them as approximate (±1–2 Lc).

| Token | WCAG on `--bg` #0a0c0f | WCAG on `--panel` #141820 | APCA on `--bg` | APCA on `--panel` |
|---|---|---|---|---|
| `--text` #dfe4ea | 15.3:1 | 13.9:1 | Lc ≈ 90 | Lc ≈ 89 |
| `--text2` #c9d0d9 | 12.6:1 | 11.4:1 | Lc ≈ 77 | Lc ≈ 77 |
| `--muted` #9aa4b2 | 7.8:1 | 7.1:1 | Lc ≈ 52 | Lc ≈ 51 |
| `--dim` #7f8896 | 5.5:1 | 5.0:1 | Lc ≈ 38 | Lc ≈ 37 |
| `--acc` #ffb020 | 10.7:1 | 9.7:1 | Lc ≈ 68 | Lc ≈ 68 |
| `--red` #ff5d5d | 6.5:1 | 5.9:1 | Lc ≈ 46 | Lc ≈ 45 |
| `--line3` #3d4656 | 2.1:1 | 1.9:1 | Lc ≈ 10 | Lc ≈ 9 |

- `--line`/`--line2` against `--bg` and `--panel` come out at 1.2–1.5:1, with APCA reporting Lc 0 (under its clamp).
- Dark text #0a0c0f on `--acc` gives about 10.7:1 and Lc ≈ 70.

### Inferences
- **WCAG and APCA disagree on the muted tokens.** By WCAG every text token passes AA. By APCA, `--dim` (Lc ≈ 38) is fit only for spot-readable or disabled text (Lc 30 band). `--muted` (Lc ≈ 52) is below Lc 60, which APCA asks for in readable secondary text at 12–13 px. To meet Lc 60, secondary text should move lighter, to roughly #aab3bf–#b0b8c4. This is an estimate and should be verified in apcacontrast.com.
- **Hairlines need more contrast.** `--line` and `--line2` are below APCA Lc 15 (invisible to many users). NN/g warns thin grey dividers get swallowed. Panels should therefore be separated mainly by a surface step (bg, then panel, then panel2), with hairlines as a secondary cue, or the hairlines nudged up.
- **Neutral tint.** The current neutrals are slightly blue-tinted (e.g. #141820). That is a valid "tinted neutral" choice, but per Linear, keep chroma very low. A warm accent (amber) next to cool-tinted greys is a classic, deliberate contrast. Keep the tint consistent across every grey step (Vercel's hue-consistency rule).
- **Accent use.**
  - `#ffb020` at Lc ≈ 68 is fine for icons, the playhead and bold labels.
  - As button fill, use dark text on it, as Radix specifies for Amber 9.
  - Do not use it for long small text.
  - Use one hover step (lighter amber, Radix step 10 role) and a 10–20% alpha amber for selected-row and range backgrounds.
- **Semantic tokens:** Name tokens by role (`--surface-1..3`, `--border-subtle/default/strong`, `--text-primary/secondary/tertiary`, `--accent`, `--accent-hover`, `--accent-subtle`, `--danger`, `--focus`), mirroring Radix and Geist roles, rather than by value. Define them in OKLCH so lightness steps are even. CSS `oklch()` is supported in current evergreen browsers; I did not verify the support matrix this session.
- **Video wells:** Use true black or near-black only inside the video tiles (letterbox), and dark grey for chrome. This makes the video read as the brightest, most important layer. Apple and Spotify-style guidance: let the UI recede.

### Gaps
- I could not read Material 3's current tonal "surface container" roles (m3.material.io is JS-rendered). The M2 figures are older and second-hand.
- I could not get Linear's actual dark-theme hex/LCH values or its contrast formula.
- APCA's adoption status within W3C could not be confirmed from a W3C source this session.

---

## Detail polish: hairlines, inner highlights, focus rings, icons, numbers, truncation, cursors, selection, scrollbars, empty and loading states

### Takeaway
The sourced, concrete polish items are:
- Semi-transparent borders combined with layered shadows.
- `:focus-visible` rings of at least 2 px with 3:1 change contrast.
- Icons on a consistent grid: 24 px canvas, 2 px stroke, round caps and joins, at least 2 px gaps, matched visual weight.
- Tabular numerals and locale formatting.
- `…` for truncation and pending states.
- Designed empty, sparse, dense and error states.
- `color-scheme: dark` for native scrollbars.
- Loading states with show-delay and minimum duration.
- Motion only where it clarifies.

### Cited Findings
- **Focus (Vercel):** "Every focusable element shows a visible, unobscured focus ring. Prefer `:focus-visible` over `:focus`… Set `:focus-within` for grouped controls. Sticky headers… never cover the focused element." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Focus (WCAG 2.2, SC 2.4.13 Focus Appearance, Level AAA):** The indicator is "at least as large as the area of a 2 CSS pixel thick perimeter" and has "a contrast ratio of at least 3:1 between the same pixels in the focused and unfocused states". — [W3C, Understanding SC 2.4.13](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance.html)
- **Focus (Radix):** Focus rings use step 7–8 of a scale. — [Radix Colors](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **Borders and shadows (Vercel):** "Combine borders & shadows; semi-transparent borders improve edge clarity". Shadows have "at least two layers" (ambient plus direct). — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Alpha borders (Geist):** Use gray-alpha borders "only when the edge needs to blend with its surface"; overlapping alpha borders make intersections stand out. — [Geist Colors](https://vercel.com/geist/colors)
- **Icon grid (Lucide):**
  - 24×24 canvas with a 1 px safe zone.
  - 2 px stroke, never mixed.
  - Round joins and caps, centred strokes.
  - 2 px corner radius on shapes ≥8 px and 1 px below that.
  - At least 2 px between distinct elements and inside shapes.
  - Consistent visual weight, checked by blurring the icon next to a circle or square.
  - Optical (not geometric) centring for asymmetric icons.
  - Low detail density.

  — [Lucide design language](https://lucide.dev/guide/design/icon-design-guide)
- **Icons beside text (Apple):** SF Symbols use weights equivalent to the text weights, "you can achieve precise weight matching between symbols and adjacent text". — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Icons on dark (Apple):** An icon may need a "slight border to make the edge visible against a dark background". — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Content rules (Vercel):**
  - "All states designed. Empty, sparse, dense, & error states."
  - "No dead ends. Every screen offers a next step or recovery path."
  - "Resilient to user-generated content. Layouts handle short, average, & very long content." This bears directly on truncating long dashcam filenames.
  - "Redundant status cues. Don't rely on color alone".
  - "Stable skeletons" mirror the final content.

  — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Ellipsis:** Use `…` for truncation, follow-up menu items ("Export clip…") and pending states ("Loading…", "Exporting…"). — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Loading:** "add a short show-delay (~150–300 ms) & a minimum visible time (~300–500 ms) to avoid flicker". On a loading button, "Show a loading indicator & keep the original label." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Scrollbars and drawers:** Set `color-scheme: dark` so native scrollbars match. Set `overscroll-behavior: contain` in drawers and modals. Avoid unnecessary scrollbars. — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Drag and cursor states:** "Disable text selection & apply `inert`… while an element is dragged so selection/hover don't occur simultaneously." Use `touch-action: manipulation` and set `-webkit-tap-highlight-color` deliberately. — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Tooltips:** "Delay the first tooltip in a group; subsequent peers have no delay." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Animation:**
  - Animate only `transform`/`opacity`.
  - "Never `transition: all`".
  - Make animations interruptible.
  - Honour `prefers-reduced-motion`.
  - "Only animate when it clarifies cause & effect".

  — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Frequency and novelty (Rauno):** For high-frequency, keyboard-driven actions, remove motion. After a few days the animated bmrks list "began to feel sluggish… I removed motion from core interactions and suddenly felt like I was moving much faster". macOS context menus appear without animation, but the chosen item "briefly blinks the accent color" before the menu fades out. — [Rauno Freiberg, Invisible Details of Interaction Design](https://rauno.me/craft/interaction-design)
- **Seeking under a finger (Rauno):** "Although seeking video is mostly a visual interaction, there's an unintelligible level of discomfort apparent when interacting with an element that you can't see". — [Rauno](https://rauno.me/craft/interaction-design)
- **Gradients:** CSS-mask fades to dark can band; use background images instead. — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)

### Inferences
- **Inner highlight.** A 1 px top inner highlight on raised dark surfaces is a common premium detail: `box-shadow: inset 0 1px 0 rgb(255 255 255 / 0.04–0.06)` plus a 1 px alpha border. It fits Vercel's "semi-transparent borders" and the "lighter = closer" model, but the inner highlight itself was not stated in any fetched source. Treat it as practitioner convention.
- **Focus ring.** Use a 2 px `:focus-visible` outline in the accent, with `outline-offset: 2px`, so it clears video edges and the timeline. Amber on near-black gives about 10:1 change contrast, well above 3:1.
- **Icons.** Use one icon family (Lucide-style 24 grid, rendered at 16 or 20 px, with a 1.5–2 px stroke scaled consistently) for every control. Mixing emoji, Unicode glyphs and SVGs of different stroke weights is a common amateur tell.
- **Numbers.**
  - Right-align numeric columns (G-sensor values, speeds) and keep the decimal count fixed per field (e.g. `0.42 g`, never `0.4 g` then `0.42 g`). This applies Vercel's "0 or 2 decimals, never mix" currency rule to telemetry.
  - Use non-breaking spaces before units (`63&nbsp;km/h`).
  - Show the minus sign as `−` (U+2212), so negative G-values align with positives in tabular figures. This is my suggestion and not sourced.
- **Truncation.**
  - Long filenames get a middle ellipsis, keeping the camera suffix and extension, e.g. `20241012_1432…_F.mp4`.
  - Show the full name in a `title` or tooltip.
- **Selection colour.** Use `::selection { background: rgb(255 176 32 / 0.3) }` to keep text selection on-brand. Unsourced practice.
- **Cursors.** Use `col-resize`/`ew-resize` on the timeline scrub and splitters, `grab`/`grabbing` on the map, and `pointer` only on real actions.
- **Motion for the stressed owner.** Do not animate high-frequency actions: play/pause, frame-step and timeline jumps should respond instantly, per Rauno's frequency rule. Reserve motion for the drawer open/close and one-time onboarding.

### Gaps
- I found no first-party write-up quantifying inner-highlight opacity values, or custom scrollbar dimensions, from Linear, Raycast or Arc.
- I found no source on selection-colour conventions.

---

## What separates amateur from premium: craft details designers point to

### Takeaway
The recurring message from Linear, Vercel, Rauno and Apple is that premium comes from:
- many small, consistent decisions made system-wide (tokens generated from a few inputs, a fixed set of sizes, radii and colours);
- alignment that is felt rather than seen;
- restraint: less chrome colour, low elevation, motion only where it clarifies;
- every state designed.

Decoration is not what makes it premium.

### Cited Findings
- **Vercel's framing:** "Interfaces succeed because of hundreds of choices." The guidelines are "a living, non-exhaustive list of those decisions". — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Linear on care:** "we put so much care into even the tiniest details". The redesign goal was a "more cohesive, timeless UI" that reduces "visual noise", achieved partly by limiting brand-colour chrome in the colour calculations. — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Linear on systems:** It collapsed 98 per-theme variables into 3 generated inputs, so every surface, text, icon and control alias is derived consistently. — [Linear redesign](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Rauno:** "there are hundreds of design decisions made by someone obsessing over the tiniest margins so that when they work, no one has to think about [them]". Great interactions are interruptible and model real-world physics. — [Rauno Freiberg, Invisible Details of Interaction Design](https://rauno.me/craft/interaction-design)
- **Refactoring UI:** Amateur palettes come from five-swatch generators. Real interfaces need around 8–10 greys plus 5–10 shades per colour, chosen up front. — [Refactoring UI preview](https://www.refactoringui.com/previews/building-your-color-palette)
- **Apple:** "Mixing too many different typefaces… [makes] an interface feel internally inconsistent or poorly designed." — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Geist:** "over-elevating is a common source of visual noise". Use "the lowest elevation that still reads as elevated". — [Geist Materials](https://vercel.com/geist/materials)
- **NN/g:** Dark-mode failures are mostly carelessness: invisible dividers, glowing "shadows", saturated colours that blur, thin fonts swallowed by the background. — [NN/g, Dark Mode issues](https://www.nngroup.com/articles/dark-mode-users-issues/)

### Inferences
Amateur tells most relevant to DashLens, ranked:
1. Jittering, proportional-width timecodes and values.
2. Mixed icon styles and stroke weights.
3. Too many grey values that are not on a ramp, plus hard-coded hex values outside tokens.
4. Accent colour used for decoration rather than only for interactive and current-state elements.
5. Inconsistent radii, and non-concentric nested corners.
6. Hairline-only separation that vanishes on dark.
7. Missing hover, active, focus, disabled, empty and error states.
8. Animations on frequent actions.
9. Native light-themed scrollbars or `<select>` popups on a dark page.
10. Text below about 11 px, or weights below 400, on dark.

For the stressed post-incident user, the premium signals that also build trust are:
- calm, low-chroma chrome;
- one unmistakable amber for "where you are" (playhead) and "what you can do" (primary action);
- precise, stable numbers (time, speed, G, GPS) that look like evidence.

### Gaps
- I could not access Raycast's or Arc's design write-ups, Figma's UI3 redesign notes, or the Refactoring UI chapters on dark UI and shadows (paywalled/403).
- Claims attributed to those products in other researchers' notes should be checked separately.
