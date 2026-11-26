# Visual craft of premium dark UIs: claims checked against primary sources (for DashLens)

Checked 2026-11-26. This file re-checks `research_notes/Premium UI UX for DashLens/visual_craft.md` (the "earlier notes"). Context: DashLens is a dark, single-file dashcam video viewer.

How the check was done:
- Every page below was downloaded directly from its primary URL (HTTP 200) and read as text. Pages that need JavaScript (m2.material.io, m3.material.io) were rendered in headless Chrome and the rendered page was read.
- Apple HIG was read from Apple's own JSON data endpoint for the HIG pages, so the tables are exact.
- APCA numbers were computed with the official npm package `apca-w3` version 0.1.9 (its source says "APCA 0.0.98G - 4g - W3 Compatible Constants"), run in Node 22.
- web.archive.org was not reachable (connection reset), so nothing here depends on an archive copy.
- Labels used: **CONFIRMED** (quote matches the primary page), **CORRECTED** (the page says something different, or the earlier note left out an important qualifier), **NOT FOUND** (no primary source found), **NEW** (filled from a primary source; not in the earlier notes).

---

## 1. Linear UI redesign: LCH theme generation, the three inputs, typography, alignment

### Takeaway
Every Linear quote in the earlier notes is confirmed word for word on the primary page, which is dated March 28, 2024. A newer Linear post (March 12, 2026) is important. It says Linear has since moved its default dark and light themes away from the "cool, blue-ish hue" to "a warmer gray that still feels crisp, but less saturated". It also says Linear dimmed the sidebar, cut and shrank icons, and used fewer, softer borders. Linear still publishes no exact type sizes, weights or colour values.

### Cited Findings
- **Page metadata. CONFIRMED.** The title is "How we redesigned the Linear UI (part Ⅱ)". The byline is "Karri Saarinen and 3 others", dated "March 28, 2024". — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Three inputs. CONFIRMED.** "So, instead of having to define 98 specific variables for each theme, we defined three: base color, accent color, and contrast." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **LCH rationale. CONFIRMED, with a note.** "A while back, we rebuilt the system for generating custom themes in Linear, using the LCH color space instead of HSL. LCH has the benefit that it's perpetually uniform, meaning a red and a yellow color with lightness 50 will appear roughly equally light to the human eye."
  - "perpetually" is Linear's own typo for "perceptually". Quote it with [sic].
  - LCH was first built for *custom* themes. With this redesign Linear started "using the new theme generation system not only for custom themes but also for the main light and dark themes".

  — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Elevations. CONFIRMED.** LCH "allowed us to deal with different elevations for our surfaces (e.g. background, foreground, panels, dialogs, and modals)." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Contrast variable. CONFIRMED.** It "defines how contrasty a theme should be. This allows us to automatically include super high-contrast themes for users who need it for accessibility reasons." The figure caption compares "contrast set to 30 and 100". — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Neutral chrome. CONFIRMED.** "return to a more neutral and timeless appearance. The latter was achieved by limiting how much chrome (blue in our case) was used in the calculations applied to our color system. The contrast of the content has also been improved by making our text and neutral icons darker in light mode and lighter in dark mode." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Opacities of black and white. CONFIRMED, with attribution.** These were Karri Saarinen's explorations: "Karri mostly worked with opacities of black and white during his explorations". The engineering side then refined "the core variables and the operations we apply to them to generate our aliases for surfaces, texts, icons, and controls". — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Typography. CONFIRMED.** "We started using Inter Display to add more expression to our headings while maintaining their readability and kept using regular Inter for the rest of the text elements." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Alignment. CONFIRMED.** "I also spent time aligning labels, icons, and buttons, both vertically and horizontally in the sidebar and tabs… This part of the redesign isn't something you'll immediately see but rather something that you'll feel after a few minutes of using the app." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Density and Apple. CONFIRMED.**
  - Goal: "reduce visual noise, maintain visual alignment, and increase the hierarchy and density of navigation elements".
  - "We tested a lot of options, from very condensed to more spacious configurations. I often relied on Apple standards, which also helped get close to the feeling of a native app."

  — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **Care. CONFIRMED.** "This is why we put so much care into even the tiniest details in Linear." — [Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)
- **NEW: Linear 2026 refresh**, "A calmer interface for a product in motion", by Charlie Aufmann and Maxime Heckel, March 12, 2026:
  - Principle: "Don't compete for attention you haven't earned… ones that support orientation and navigation should recede."
  - Sidebar: "it's a few notches dimmer, allowing the main content area—where users work—to take precedence."
  - Tabs: "more compact… with rounded corners and smaller icon and text sizing."
  - Icons: "The refresh reduces icon usage, scales their sizes down, and removes unnecessary visual treatments like colored team icon backgrounds."
  - Borders: they "had quietly proliferated… By rounding out their edges and softening the contrast, the polished interface gives users structure on the page without cluttering their view."
  - Palette: "The old palette was a cool, blue-ish hue, and the aim was to inch toward a warmer gray that still feels crisp, but less saturated. Go too warm, though, and the interface risks looking muddy."
  - Theme inputs still exist: users create themes "by selecting base UI and accent colors and adjusting contrast". An internal tool exposes "hue, chroma, and lightness of individual design tokens".

  — [Linear, A calmer interface for a product in motion](https://linear.app/now/behind-the-latest-design-refresh)

### Inferences
- The earlier notes treated DashLens's slightly blue-tinted neutrals (#141820) as consistent with Linear's approach. Linear's 2024 post does support keeping chroma low. Its 2026 post, however, moved *away* from a cool blue-ish grey towards a warmer, less saturated grey. Either tint is defensible. The firm lesson from both posts is low chroma, applied consistently across every grey step.
- Linear's 2026 move to "softening the contrast" of borders and using fewer separators supports DashLens separating panels mainly by surface steps, with hairlines kept as a quiet secondary cue.

### Gaps
- **NOT FOUND:** Linear's exact type sizes, weights, tracking, LCH values or contrast formula. Neither post publishes them.
- I did not find a separate Linear engineering post on the LCH theme generator. The 2024 post says only "A while back, we rebuilt the system".

---

## 2. Vercel Web Interface Guidelines and Geist: type sizes, radii by elevation, tabular numbers, color-scheme, loading timings

### Takeaway
All Vercel guideline quotes in the earlier notes are confirmed on the primary page, so the GitHub mirror is no longer needed. The Geist typography, materials and colours claims are also confirmed. A few quotes were trimmed and are given in full below. No page date was shown on any of these pages.

### Cited Findings
- **Framing. CONFIRMED.** "Interfaces succeed because of hundreds of choices. This is a living, non-exhaustive list of those decisions." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- **Tabular numbers. CONFIRMED.** "Tabular numbers for comparisons. Use font-variant-numeric: tabular-nums or a monospace like Geist Mono." — [Vercel](https://vercel.com/design/guidelines)
- **color-scheme. CONFIRMED.** "Style the <html> tag with color-scheme: dark in dark themes so that scrollbars and other device UI have proper contrast." The theme-color example given is `<meta name="theme-color" content="#000000">`. — [Vercel](https://vercel.com/design/guidelines)
- **Loading timings. CONFIRMED.** The full text is: "If you show a spinner/skeleton, add a short show-delay (~150–300 ms) & a minimum visible time (~300–500 ms) to avoid flicker on fast responses. The <Suspense> component in React does this automatically." Also: "Loading buttons. Show a loading indicator & keep the original label." — [Vercel](https://vercel.com/design/guidelines)
- **Hit targets. CONFIRMED.** "Match visual & hit targets. Exception: if the visual target is < 24px, expand its hit target to ≥ 24px. On mobile, the minimum size is 44px." — [Vercel](https://vercel.com/design/guidelines)
- **Radii and alignment rules. CONFIRMED.**
  - "Nested radii. Child radius ≤ parent radius & concentric so curves align."
  - "Optical alignment. Adjust ±1px when perception beats geometry."
  - "Deliberate alignment. Every element aligns with something intentionally whether to a grid, baseline, edge, or optical center."
  - "Balance contrast in lockups… a thin-stroke icon may need a bolder stroke next to medium-weight text."

  — [Vercel](https://vercel.com/design/guidelines)
- **Colour and contrast rules. CONFIRMED.**
  - "Layered shadows. Mimic ambient + direct light with at least two layers."
  - "Crisp borders. Combine borders & shadows; semi-transparent borders improve edge clarity."
  - "Hue consistency. On non-neutral backgrounds, tint borders/shadows/text toward the same hue."
  - "Minimum contrast. Prefer APCA over WCAG 2 for more accurate perceptual contrast."
  - "Interactions increase contrast. :hover, :active, :focus have more contrast than rest state."

  — [Vercel](https://vercel.com/design/guidelines)
- **Dark-mode fixes. CONFIRMED.**
  - Native select: "Explicitly set background-color & color on native <select> to avoid dark-mode contrast bugs on Windows."
  - Text rendering: "Scaling text can change smoothing. Prefer animating a wrapper instead of the text node. If artifacts persist set translateZ(0)…"
  - Gradients: "Fading content to dark colors using css masks can cause banding. Background images can be used instead."

  — [Vercel](https://vercel.com/design/guidelines)
- **Focus, interaction and content rules. CONFIRMED.**
  - "Every focusable element shows a visible, unobscured focus ring. Prefer :focus-visible over :focus…"
  - "No dead zones."
  - "Tooltip timing. Delay the first tooltip in a group; subsequent peers have no delay."
  - "All states designed. Empty, sparse, dense, & error states."
  - "Redundant status cues. Don't rely on color alone; include text labels."
  - "Resilient to user-generated content."
  - "Stable skeletons."
  - Ellipsis rules ("Rename…", "Loading…").
  - "Use numerals for counts."
  - "display currency with either 0 or 2 decimal places, never mix both."
  - `10&nbsp;MB`.
  - Curly quotes.

  — [Vercel](https://vercel.com/design/guidelines)
- **Animation rules. CONFIRMED.**
  - "Never transition: all."
  - "Compositor-friendly… transform, opacity."
  - "Interruptible. Animations are cancelable by user input."
  - "Necessity check. Only animate when it clarifies cause & effect or when it adds deliberate delight."
  - Honor `prefers-reduced-motion`.

  — [Vercel](https://vercel.com/design/guidelines)
- **Geist typography. CONFIRMED.** Full usage notes:
  - Label: "Designed for single-lines, and given ample line-height for highlighting & marrying up with icons."
  - Label 14: "Most common text style of all. Used in many menus."
  - Label 13: "Used as a secondary line next to other labels. Tabular is used when conveying numbers for consistent spacing."
  - Label 13 Mono: "Used to pair with Label 14, as the smaller mono size looks better in that pairing."
  - Label 12: "Used for tertiary level text in busy views, like Comments, Show More and the capitals in Calendars."
  - Copy: "Designed for multiple lines of text, having a higher line height than Label."
  - Copy 14: "Most commonly used text style."
  - Copy 13: "For secondary text and views where space is a premium." The earlier notes dropped "secondary text and".
  - Buttons 16 / 14 ("Default button.") / 12 ("Only used when a tiny button is placed inside an input field.").
  - Headings run from 72 down to 14.

  — [Geist Typography](https://vercel.com/geist/typography)
- **Geist radii by elevation. CONFIRMED.**
  - Base: "Everyday use. Radius 6px."
  - Small: "Slightly raised. Radius 6px."
  - Medium and Large: "Radius 12px."
  - Tooltip: "Lightest shadow. Corner 6px. Tooltips will be the only floating element with a triangular stem."
  - Menu and Modal: 12px.
  - Fullscreen: "Biggest lift. Radius 16px."
  - "Don't stack two Materials on the same element."
  - "Favor the lowest elevation that still reads as elevated against its background; over-elevating is a common source of visual noise."
  - "shadow contrast on dark backgrounds is weaker than on light, so confirm separation still reads."
  - **NEW:** "Don't rely on shadow alone to communicate elevation; pair with the matching focus-visible ring on focusable children inside."

  — [Geist Materials](https://vercel.com/geist/materials)
- **Geist colours. CONFIRMED, with additions.**
  - "Gray for text, icons, fills, borders, and dividers by default. Gray-alpha only when the background should show through, such as in shadows or overlays."
  - Background 2 "should be used sparingly".
  - Colors 1–3 are the default, hover and active component backgrounds.
  - Colors 4–6 are the default, hover and active border strengths: "Use solid gray by default. Use the matching gray-alpha step only when the edge needs to blend with its surface."
  - **NEW:** "Draw each border once… Overlapping alpha borders make intersections stand out."
  - **NEW:** "Keep material shadows translucent… Opaque shadows leave a gray halo."
  - "There are 10 color scales… P3 colors are used on supported browsers and displays."

  — [Geist Colors](https://vercel.com/geist/colors)

### Inferences
- For DashLens, Geist's 6 / 12 / 16 radius set is a ready-made, sourced choice:
  - 6 px for tiles, chips and tooltips;
  - 12 px for the settings drawer, menus and modals;
  - 16 px only for a full-screen overlay.
- "Draw each border once" matters for DashLens's tiled video grid. Adjacent tiles should share one divider, not two overlapping borders.

### Gaps
- Geist pages show class names and usage only. The exact line-height and letter-spacing values behind each class are not in the page text. They live in Vercel's Tailwind preset and Figma file, which I did not read.
- No publication or update date is shown on the guidelines or Geist pages.

---

## 3. Material Design dark theme (M2) and Material 3 surface roles

### Takeaway
The M2 figures that earlier came from search summaries are all confirmed on the rendered primary page:
- #121212;
- text at 87 / 60 / 38 %;
- an overlay table running 0–16 %;
- the 200 tone for primary colours.

The page adds a "15.8:1" rule that the earlier notes left out. The M3 gap is now filled: M3 has 26 colour roles, with a surface role plus five surface-container roles. Their dark-theme tones, taken from Google's own colour library, map to neutral greys from about #0e0e0e to #393939.

### Cited Findings
- **#121212. CONFIRMED.** "The recommended dark theme surface color is #121212." Also: "Use dark grey – rather than black – to express elevation and space." — [Material Design 2, Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **Text opacities. CONFIRMED.** "When light text appears on dark backgrounds… High-emphasis text has an opacity of 87%. Medium-emphasis text and hint text have opacities of 60%. Disabled text has an opacity of 38%." — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html); the same values appear in [Google codelab](https://codelabs.developers.google.com/codelabs/design-material-darktheme/)
- **Overlay table. CONFIRMED, now complete.** "Elevation overlay transparencies range from 0% for the lowest level to 16% for the highest level."

  | Elevation | 0dp | 1dp | 2dp | 3dp | 4dp | 6dp | 8dp | 12dp | 16dp | 24dp |
  |---|---|---|---|---|---|---|---|---|---|---|
  | White overlay | 0% | 5% | 7% | 8% | 9% | 11% | 12% | 14% | 15% | 16% |

  The overlay uses "the On Surface color" (white). — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **Flutter formula. CONFIRMED in current Flutter source.** `final double opacity = (4.5 * math.log(elevation + 1) + 2) / 100.0;` — [flutter/flutter elevation_overlay.dart](https://github.com/flutter/flutter/blob/master/packages/flutter/lib/src/material/elevation_overlay.dart)
- **Desaturated accents. CONFIRMED.**
  - "The baseline Material Design dark theme uses the 200 tone of the primary color (passing the WCAG's AA standard of at least 4.5:1 for normal text, at all elevation surfaces)."
  - "it's recommended to use lighter tones (200-50) in dark theme".
  - "Saturated colors also produce optical vibrations against a dark background, which can induce eye strain."
  - Brand colours "can be used at full saturation… limited to one or two branded elements".

  — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **NEW: the 15.8:1 rule.** "Dark theme surfaces must be dark enough to display white text. They should use a contrast level of at least 15.8:1 between text and the background. This ensures that body text passes WCAG's AA standard of at least 4.5:1 when applied to surfaces at the highest (and lightest) elevation." — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **NEW: why dark grey and not black.** "Dark grey surfaces can express a wider range of color, elevation, and depth, because it's easier to see shadows on grey (instead of black)… light text on a dark grey surface has less contrast than light text on a black surface." — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **NEW: branded surface.** "The color #1F1B24 is the result of combining the dark theme surface color #121212 and the 8% Primary color." — [M2 Dark theme](https://m2.material.io/design/color/dark-theme.html)
- **NEW: overlays are superseded.**
  - Android Material Components now says: "Surface with elevation overlays has been replaced in Material components with the tonal surface color system."
  - The older Android overlay used `colorPrimary`, not white.

  — [material-components-android, Dark.md](https://github.com/material-components/material-components-android/blob/master/docs/theming/Dark.md)
- **NEW: M3 surface roles.**
  - "There are 26 standard color roles organized into six groups: primary, secondary, tertiary, error, surface, and outline."
  - "There are three surface roles: Surface: Default color for backgrounds; On surface: Text and icons against any surface or surface container color; On surface variant: Lower-emphasis color for text and icons".
  - "There are also five surface container roles named based on their level of emphasis: Surface container lowest… low… Surface container: Default container color… high… highest".
  - "The most common combination of surface roles uses surface for a background area and surface container for a navigation area."
  - "Container – Roles used as a fill color for foreground elements like buttons. They should not be used for text or icons."

  — [Material 3, Color roles](https://m3.material.io/styles/color/roles)
- **NEW: M3 dark-theme tones** (HCT tone, standard contrast), from Google's material-color-utilities `color_spec_2021.ts`:
  - surface 6, surfaceDim 6, surfaceBright 24
  - surfaceContainerLowest 4, Low 10, Container 12, High 17, Highest 22
  - onSurface 90, onSurfaceVariant 80
  - outline 60, outlineVariant 30

  Higher contrast levels raise them; for example, surfaceContainer becomes 16 and then 20. — [material-color-utilities](https://github.com/material-foundation/material-color-utilities/blob/main/typescript/dynamiccolor/color_spec_2021.ts)

  My conversion of those tones to neutral sRGB greys (tone = CIE L\*):

  | Tone | Grey | Role |
  |---|---|---|
  | 4 | #0e0e0e | container lowest |
  | 6 | #131313 | surface |
  | 10 | #1b1b1b | container low |
  | 12 | #1f1f1f | container |
  | 17 | #2a2a2a | container high |
  | 22 | #353535 | container highest |
  | 24 | #393939 | bright |
  | 30 | #474747 | outline variant |
  | 60 | #919191 | outline |
  | 80 | #c6c6c6 | on-surface variant |
  | 90 | #e2e2e2 | on surface |

  Real M3 schemes add a slight hue tint.

### Inferences
- The earlier notes' DashLens surfaces (#0a0c0f bg, #141820 panel, #1a1f28 panel2) sit in the same range as M3's lowest, surface and container-low/container steps. The mapping is reasonable.
- M3's outlineVariant at tone 30 (about #474747) is noticeably lighter than DashLens's `--line` #20262f. Section 7 shows why the current DashLens hairlines measure as Lc 0.

### Gaps
- The M2 page shows no date. M2 itself dates from 2019 and is now legacy.
- The M3 roles page showed no date in the rendered text.

---

## 4. Apple HIG typography and dark mode: tracking, minimum sizes, media apps always dark

### Takeaway
The sizes, weights and dark-mode quotes are confirmed. Two items are corrected:
- The SF Pro tracking table does not tighten all the way up from 13 pt. It is most negative at 17 pt (−26), crosses back to positive at 24 pt, and peaks at +14 around 28–30 pt.
- The "media apps always dark" guidance is qualified by "In rare cases".

### Cited Findings
- **Default and minimum sizes. CONFIRMED.**

  | Platform | Default | Minimum |
  |---|---|---|
  | iOS, iPadOS | 17 pt | 11 pt |
  | macOS | 13 pt | 10 pt |
  | tvOS | 29 pt | 23 pt |
  | visionOS | 17 pt | 12 pt |
  | watchOS | 16 pt | 12 pt |

  Also: "If you use a custom font with a thin weight, aim for larger than the recommended sizes". — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Tracking table. CORRECTED (incomplete before).** The SF Pro and macOS tracking tables (in 1/1000 em) are identical:

  | Size (pt) | Tracking |
  |---|---|
  | 6 | +41 |
  | 8 | +26 |
  | 10 | +12 |
  | 11 | +6 |
  | 12 | 0 |
  | 13 | −6 |
  | 14 | −11 |
  | 15 | −16 |
  | 16 | −20 |
  | **17** | **−26** |
  | 18 | −25 |
  | 20 | −23 |
  | 22 | −12 |
  | 23 | −4 |
  | **24** | **+3** |
  | 26 | +8 |
  | 28–30 | +14 |
  | 32 | +13 |
  | 40 | +10 |
  | 48 | +8 |
  | 60 | +4 |
  | 72 | +2 |
  | 80–96 | 0 |

  The 6–17 pt values in the earlier notes are right. The claim that "text from 13 pt upward is tightened" holds only from 13 to 23 pt. — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Dynamic optical sizes. CONFIRMED.** "the system fonts support dynamic optical sizes, which merge discrete optical sizes (like Text and Display) and weights into a single, continuous design". — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **macOS built-in text styles. CONFIRMED, with additions.** Style, weight, size/line height in pt, and emphasized weight:

  | Style | Weight | Size / line height | Emphasized |
  |---|---|---|---|
  | Large Title | Regular | 26/32 | Bold |
  | Title 1 | Regular | 22/26 | Bold |
  | Title 2 | Regular | 17/22 | Bold |
  | Title 3 | Regular | 15/20 | Semibold |
  | Headline | Bold | 13/16 | Heavy |
  | Body | Regular | 13/16 | Semibold |
  | Callout | Regular | 12/15 | Semibold |
  | Subheadline | Regular | 11/14 | Semibold |
  | Footnote | Regular | 10/13 | Semibold |
  | Caption 1 | Regular | 10/13 | Medium |
  | Caption 2 | Medium | 10/13 | Semibold |

  The change log says the emphasized weights were "Added… December 16, 2025". — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Weights and typefaces. CONFIRMED.**
  - "In general, avoid light font weights… prefer Regular, Medium, Semibold, or Bold font weights, and avoid Ultralight, Thin, and Light font weights, which can be difficult to see, especially when text is small."
  - "Minimize the number of typefaces you use, even in a highly customized interface. Mixing too many different typefaces can obscure your information hierarchy and hinder readability, in addition to making an interface feel internally inconsistent or poorly designed."
  - "Because SF Symbols use equivalent weights, you can achieve precise weight matching between symbols and adjacent text".

  — [Apple HIG, Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- **Media apps always dark. CORRECTED (qualifier added).** The full sentence is: "In rare cases, consider using only a dark appearance in the interface. For example, it can make sense for an app that supports immersive media viewing to use a permanently dark appearance that lets the UI recede and helps people focus on the media." — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Base and elevated backgrounds. CONFIRMED.** "In Dark Mode, the system uses two sets of background colors — called base and elevated… The base colors are dimmer, making background interfaces appear to recede, and the elevated colors are brighter, making foreground interfaces appear to advance." Also, colours "aren't necessarily inversions of their light counterparts". — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Contrast. CONFIRMED.** "At a minimum, make sure the contrast ratio between colors is no lower than 4.5:1. For custom foreground and background colors, strive for a contrast ratio of 7:1, especially in small text." — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **Icons and images on dark. CONFIRMED.**
  - "an icon that represents a drop of oil might need a slight border to make the edge visible against a dark background."
  - "Soften the color of white backgrounds… consider slightly darkening the image to prevent the background from glowing".

  The Dark Mode change log's last entry is August 6, 2024. — [Apple HIG, Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)

### Inferences
- DashLens is a media-review tool, so Apple's "rare cases" exception fits it. Cite the sentence in full, including the qualifier.
- Apple's table describes SF's own spacing, including the switch to its Display optical design around 20–24 pt. It should not be copied onto Inter or a system stack at heading sizes. Up to about 17 px the table and Inter's own formula agree in sign (positive at 11 px or below, about 0 at 12 px, negative from 13 px). For DashLens's 11–14 px UI text, the earlier tracking advice still holds.

### Gaps
- None for the questions asked.

---

## 5. Radix Colors scale roles, APCA levels and status, NN/g dark-mode articles

### Takeaway
The Radix roles and the claim that Radix text steps are guaranteed Lc 60 and Lc 90 are confirmed. The APCA levels are confirmed, but two corrections matter for DashLens:
- Lc 45 is meant for *large* text: 36 px at normal weight or 24 px bold.
- Lc 15 applies only to non-text at least 5 px thick. Thin 1 px lines "have a higher minimum".

On status, the current W3C WCAG 3 draft (10 September 2026) says its contrast algorithm "is yet to be determined" and does not name APCA. The NN/g quotes are confirmed, with dates.

### Cited Findings
- **Radix scale table. CONFIRMED.** The twelve steps:
  1. App background
  2. Subtle background
  3. UI element background
  4. Hovered UI element background
  5. Active / Selected UI element background
  6. Subtle borders and separators
  7. UI element border and focus rings
  8. Hovered UI element border
  9. Solid backgrounds
  10. Hovered solid backgrounds
  11. Low-contrast text
  12. High-contrast text

  The prose adds:
  - "Step 6 is designed for subtle borders on components which are not interactive. For example sidebars, headers, cards, alerts, and separators."
  - "Step 7 is designed for subtle borders on interactive components."
  - "Step 8 is designed for stronger borders on interactive components and focus rings."
  - "Step 9 has the highest chroma of all steps in the scale."

  — [Radix Colors, Understanding the scale](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **Radix APCA guarantee. CONFIRMED.** "Steps 11 and 12—which are designed for text—are guaranteed to Lc 60 and Lc 90 APCA contrast ratio on top of a step 2 background from the same scale." — [Radix](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **Radix Amber. CONFIRMED, with wording.** "Most step 9 colors are designed for white foreground text. Sky, Mint, Lime, Yellow, and Amber are designed for dark foreground text and steps 9 and 10." — [Radix](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **APCA on WCAG 2 and dark mode. CONFIRMED.** WCAG 2.x "overstates contrast for dark colors to the point that 4.5:1 can be functionally unreadable when one of the colors in a pair is near black. As a result, WCAG 2.x contrast cannot be used for guidance designing 'dark mode'." The page's copyright line is "© 2022". — [APCA in a Nutshell](https://git.apcacontrast.com/documentation/APCA_in_a_Nutshell.html)
- **APCA levels. CONFIRMED, with CORRECTIONS.** Exact text:
  - **Lc 90:** "Preferred level for fluent text and columns of body text with a font no smaller than 18px/weight 300 or 14px/weight 400 (normal), or non-body text with a font no smaller than 12px/400." *New:* "Lc 90 is a suggested maximum for very large and bold fonts (greater than 36px bold), and large areas of color."
  - **Lc 75:** "The minimum level for columns of body text with a font no smaller than 24px/300 weight, 18px/400, 16px/500 and 14px/700. This level may be used with non-body text with a font no smaller than 15px/400."
  - **Lc 60:** "The minimum level recommended for content text that is not body, column, or block text. In other words, text you want people to read. The minimums: no smaller than 48px/200, 36px/300, 24px normal weight (400), 21px/500, 18px/600, 16px/700 (bold)… To use these sizes as body text, add Lc 15."
  - **Lc 45. CORRECTED.** "The minimum for larger, heavier text (36px normal weight or 24px bold) such as headlines… This is also the minimum for pictograms with fine details, or smaller outline icons." The earlier notes said only "large or heavy text".
  - **Lc 30:** "The absolute minimum for any text not listed above, including text considered as 'spot readable'. This includes placeholder text and disabled element text… also the minimum for… 'mostly solid' icons… Generally no less than 5.5px solid in its smallest dimension."
  - **Lc 15. CORRECTED.** "The absolute minimum for any non-semantic non-text that needs to be discernible, and is no less than 5px (solid) in its smallest dimension. This may include dividers… but does not include fine details which have a higher minimum. Designers should treat anything below this level as invisible".

  — [APCA in a Nutshell](https://git.apcacontrast.com/documentation/APCA_in_a_Nutshell.html)
- **APCA status. CONFIRMED as a self-description only.** "APCA is the candidate contrast method for the future WCAG 3, and is also developing as the APCA Readability Criterion, an independent standard hosted by Inclusive Reading Technologies." — [APCA in a Nutshell](https://git.apcacontrast.com/documentation/APCA_in_a_Nutshell.html)
- **NEW: W3C's current position.** The WCAG 3.0 Working Draft of 10 September 2026 says:
  - "Text contrast sufficient (minimum)… The default visual presentation of text meets @@[contrast measure to be determined]."
  - "The contrast algorithm used in WCAG 3 is yet to be determined."
  - APCA is not mentioned anywhere in the draft.

  — [W3C, WCAG 3.0 Working Draft](https://www.w3.org/TR/wcag-3.0/)
- **NN/g, "Dark Mode: How Users Think About It and Issues to Avoid".** Published August 27, 2023; modified June 11, 2026. Quotes **CONFIRMED**:
  - Glowing shadows: "placing a black element on a black background can be problematic because a lighter 'shadow' does not create the same layered effect — it makes the top element look like it's glowing."
  - Depth: "use the darkest colors for the page elements on the bottom, and the lightest colors for the elements on top".
  - Thin and thick fonts: "Thin fonts can be easily 'swallowed up' by a dark background"; "light fonts on dark backgrounds tend to appear bolder".
  - Opacity: "use one color with different levels of opacity".
  - Saturated colour: the Coinbase example is "technically WCAG compliant (4.59:1), but just barely… the saturated blue seems to blur".
  - Dividers: "Thin, gray dividers are easily swallowed up on very dark backgrounds"; "use slight color differentiation to distinguish a card from the background".

  — [NN/g](https://www.nngroup.com/articles/dark-mode-users-issues/)
- **NN/g, "Dark Mode vs. Light Mode: Which Is Better?".** Published February 2, 2020; modified January 24, 2024. Quotes **CONFIRMED**:
  - "the positive-polarity advantage increased linearly as the font size was decreased".
  - "during nighttime it was much harder for people to read small-font text in dark mode than in light mode".
  - "some people with cataract and related disorders may perform better with dark mode".

  — [NN/g](https://www.nngroup.com/articles/dark-mode/)

### Inferences
- The corrected Lc 45 band means a grey at about Lc 45–52 (DashLens #9aa4b2, #9a9a9a) is not enough for 11–13 px labels people need to read. APCA's Lc 60 minimum starts at 16 px/700 or 24 px/400, so small readable text needs to be well above Lc 60. Use Lc 75 or more for 12–14 px text that must be read, and keep Lc 60 for short labels at 12 px and above. Lc 30–45 greys are fine only for placeholder, disabled or decorative text.
- The corrected Lc 15 band means 1 px hairlines are a "fine detail" with a higher minimum than Lc 15. Dark UIs therefore cannot rely on hairlines for structure. That matches NN/g ("swallowed up") and Linear 2026 (softer, fewer borders). Use surface steps as the main separator.
- Call APCA "the contrast method Vercel recommends and Radix designs to", not "the WCAG 3 method". W3C has not chosen an algorithm. WCAG 2.2 AA stays the compliance baseline.

### Gaps
- Radix's page does not state the *dark* step-2 hex values. These are in the Radix package, which I did not read.

---

## 6. Refactoring UI and rauno.me interaction design

### Takeaway
The Refactoring UI preview quotes and the Rauno quotes are confirmed. The Rauno "hundreds of design decisions" quote contains the author's own typo and ends differently from how the earlier notes bracketed it. The corners-and-edges point is narrower in the source: Rauno says corners. Refactoring UI's dark-UI and shadow chapters are still not freely readable.

### Cited Findings
- **Refactoring UI: greys. CONFIRMED.**
  - "True black tends to look pretty unnatural, so start with a really dark grey and work your way up to white in steady increments."
  - "In practice, you want 8-10 shades to choose from".
  - "Text, backgrounds, panels, form controls — almost everything in an interface is grey."

  — [Refactoring UI, Building Your Color Palette](https://www.refactoringui.com/previews/building-your-color-palette)
- **Refactoring UI: shades. CONFIRMED.**
  - "don't get clever using CSS preprocessor functions like 'lighten' or 'darken' to create shades on the fly. That's how you end up with 35 slightly different blues that all look the same."
  - "You can't build anything with five hex codes."
  - Primary colours: "you need a variety (5-10) of lighter and darker shades".
  - "it's not uncommon to need as many as ten different colors with 5-10 shades each for a complex UI."

  The page shows no date. — [Refactoring UI](https://www.refactoringui.com/previews/building-your-color-palette)
- **Rauno: page date. CONFIRMED.** The page is dated "July 2023". — [Rauno Freiberg, Invisible Details of Interaction Design](https://rauno.me/craft/interaction-design)
- **Rauno: "hundreds of design decisions". CORRECTED (exact wording).** "Scientifically or intuitively, there are hundreds of design decisions made by someone obsessesing [sic] over the tiniest margins so that when they work, no one has to think about." The source has no "[them]". — [Rauno](https://rauno.me/craft/interaction-design)
- **Rauno: frequency and novelty. CONFIRMED.**
  - "After a couple of days they began to feel sluggish… I removed motion from core interactions and suddenly felt like I was moving much faster".
  - macOS context menus "appear without motion… the selected item briefly blinks the accent color (pink) to provide assurance".

  — [Rauno](https://rauno.me/craft/interaction-design)
- **Rauno: sliders and seeking. CONFIRMED.**
  - "sliders can be tiny and disappear under the touch of the thumb. It helps to ensure that the dragging gesture does not cancel when moving away from the slider and still pressing down".
  - "Although seeking video is mostly a visual interaction, there's an unintelligible level of discomfort apparent when interacting with an element that you can't see."

  — [Rauno](https://rauno.me/craft/interaction-design)
- **Rauno: Fitts's law. CORRECTED (narrower).** "Operating systems make use of 'magic corners' on the edges of the screen because the target area is infinitely large… The target size is infinite because the pointer can't overshoot past the corner". The source talks about corners, not edges in general. — [Rauno](https://rauno.me/craft/interaction-design)
- **Rauno: interruptibility. CONFIRMED.** "Great interactions are modeled after properties from the real world, like interruptability." — [Rauno](https://rauno.me/craft/interaction-design)

### Inferences
- Rauno's slider point applies directly to the DashLens timeline scrub. Capture the pointer so the drag keeps going after the pointer leaves the track.

### Gaps
- **NOT FOUND (paywalled):** the Refactoring UI chapters on dark UI, shadows and spacing scale. Only preview pages are free.

---

## 7. Recomputed APCA Lc for DashLens colours (official apca-w3)

### Takeaway
Measured with apca-w3 0.1.9:
- #ededed is about Lc 95 on every background.
- #dfe4ea is about Lc 89 (just under the Lc 90 "preferred" level).
- #c9d0d9 is about Lc 77 (meets the Lc 75 body minimum).
- #b4b4b4 is about Lc 61 (just meets Lc 60).
- #9aa4b2 is about Lc 51–52 and #9a9a9a about Lc 47 (both in the Lc 45 band).
- #7f8896 is about Lc 37 (Lc 30 band: placeholder or disabled only).

All three line colours on #171717 return Lc 0 (WCAG 1.18–1.25:1). On a #171717 panel a neutral grey needs to be about #555555 to reach even Lc 15. The earlier hand re-implementation agrees with the official package within 0.5 Lc, so those numbers are **CONFIRMED**.

### Cited Findings
- **Method.** `APCAcontrast(sRGBtoY(text), sRGBtoY(bg))` from npm `apca-w3` 0.1.9, whose source carries the 0.0.98G-4g constants (for example `loClip: 0.1`, `deltaYmin: 0.0005`, `loBoWoffset: 0.027`). APCA reports light-on-dark as a negative Lc; magnitudes are shown below. WCAG 2 ratios use the standard relative-luminance formula. — [apca-w3 on npm](https://www.npmjs.com/package/apca-w3); [APCA in a Nutshell](https://git.apcacontrast.com/documentation/APCA_in_a_Nutshell.html)
- **Text colours.** Each cell is |Lc| / WCAG 2 ratio, computed:

  | Text | on #121212 | on #141820 | on #171717 | on #1a1a1a | APCA band |
  |---|---|---|---|---|---|
  | #ededed | 95.5 / 16.00:1 | 95.0 / 15.19:1 | 95.1 / 15.31:1 | 94.8 / 14.87:1 | ≥ Lc 90 (preferred body) |
  | #dfe4ea | 89.4 / 14.65:1 | 88.9 / 13.90:1 | 89.0 / 14.02:1 | 88.7 / 13.61:1 | Lc 75–90 |
  | #c9d0d9 | 77.0 / 12.05:1 | 76.5 / 11.44:1 | 76.6 / 11.53:1 | 76.3 / 11.19:1 | ≥ Lc 75 (body minimum) |
  | #b4b4b4 | 61.2 / 9.04:1 | 60.7 / 8.57:1 | 60.8 / 8.65:1 | 60.4 / 8.39:1 | ≥ Lc 60 (just) |
  | #9aa4b2 | 51.9 / 7.43:1 | 51.4 / 7.05:1 | 51.5 / 7.11:1 | 51.1 / 6.90:1 | Lc 45–60 |
  | #9a9a9a | 47.1 / 6.66:1 | 46.6 / 6.32:1 | 46.7 / 6.37:1 | 46.4 / 6.19:1 | Lc 45–60 (barely) |
  | #7f8896 | 37.7 / 5.23:1 | 37.1 / 4.96:1 | 37.2 / 5.01:1 | 36.9 / 4.86:1 | Lc 30–45 |

- **Lines on #171717.**

  | Line | Lc | WCAG 2 |
  |---|---|---|
  | #2a2a2a | 0.0 | 1.25:1 |
  | #262626 | 0.0 | 1.18:1 |
  | #20262f | 0.0 | 1.18:1 |

  Lc 0 is the package's real output, not a rounding. apca-w3 sets any raw result below `loClip` 0.1 to 0, so non-zero outputs start at about Lc 7.3. All three lines are below that floor.
- **Earlier table re-check against `--bg` #0a0c0f and `--panel` #141820.**
  - `--text` 89.8 / 88.9
  - `--text2` 77.4 / 76.5
  - `--muted` 52.3 / 51.4
  - `--dim` 38.0 / 37.1
  - `--acc` #ffb020 68.5 / 67.6
  - `--red` #ff5d5d 45.7 / 44.8
  - `--line3` #3d4656 10.2 / 9.3
  - `--line` and `--line2` both 0
  - dark #0a0c0f on `--acc`: Lc 69.7, 10.71:1

  Every value matches the earlier "≈" figures within ±1. **CONFIRMED.**
- **Threshold greys (computed).** The lightest neutral grey needed to reach each level:

  | Background | Lc 15 | Lc 30 | Lc 45 | Lc 60 | Lc 75 | Lc 90 |
  |---|---|---|---|---|---|---|
  | #171717 | #555555 | #787878 | #979797 | #b3b3b3 | #cdcdcd | #e5e5e5 |
  | #121212 | #545454 | #787878 | #969696 | #b2b2b2 | #cccccc | #e5e5e5 |
  | #141820 | #555555 | #797979 | #979797 | #b3b3b3 | #cdcdcd | #e6e6e6 |

### Inferences
- **Primary text.** #ededed (Lc 95) clears APCA's preferred Lc 90 with margin. #dfe4ea (Lc 89) is just under it but well above the Lc 75 body minimum. Either works for primary UI text. #ededed is the safer choice for small text on a video-review tool used at night, given NN/g's small-text finding.
- **Secondary text.**
  - #c9d0d9 (Lc 77) suits secondary text that has to be read, such as metadata, settings labels and the incident summary.
  - #b4b4b4 (Lc 61) sits at the Lc 60 line. It works for short labels at 12 px or larger, but has almost no headroom on #1a1a1a.
- **Tertiary greys.** #9aa4b2 and #9a9a9a (Lc 46–52) should be limited to large or bold text, outline icons with fine detail, or non-essential hints. #7f8896 (Lc 37) is for placeholder or disabled text only. These are the corrected APCA bands from section 5.
- **Hairlines.** #2a2a2a, #262626 and #20262f on #171717 are all below APCA's measurable floor. As 1 px lines they are "fine details" that need more than Lc 15.
  - Treat them as faint texture only. Separate regions by surface step: the M3-style ramp has #131313, #1b1b1b, #1f1f1f, #2a2a2a and #353535 roughly 4–5 L\* apart.
  - Any line that carries meaning (focus ring, selected-tile outline, timeline track edge) needs to be at least about #555555 on #171717, or use the accent.
  - This is consistent with Geist's three border strengths and with Radix step 7–8 for interactive borders.

### Gaps
- These are APCA Bronze ("simple mode") readings. I did not apply the Silver or Gold font lookup tables, which would adjust for DashLens's actual font and weights.
- WCAG 2 ratios were computed by me with the standard formula, not checked in a third-party tool.
