# Visual hierarchy, type scales and dark-theme surfaces for dense desktop pro apps (DashLens)

Method note: this cloud session's WebFetch could not resolve carbondesignsystem.com, fluent2.microsoft.design or m2.material.io. Most values below were therefore read **directly from the design systems' own published token packages** (downloaded from npm on 2026-11-26 and read as text, not run) and from pages fetched with curl. Package versions: `@carbon/themes` 11.86.0, `@carbon/type` 11.71.0, `@fluentui/tokens` 1.0.0-alpha.25, `@primer/primitives` 11.10.0, `@atlaskit/tokens` 20.15.0, `@adobe/spectrum-tokens` 15.9.1, `@radix-ui/colors` 3.0.0, `@material/web` 2.5.0. npm package pages are cited as the URL. Values marked **[UNVERIFIED]** come from memory, not from a source read in this session.

## 1. Desktop type scales for dense UIs (and why desktop body is 13–14 px)

### Takeaway
Every major desktop system puts default UI/body text at 13–14 px (Apple macOS 13 pt; Carbon, Fluent, Primer, Atlassian, Spectrum-desktop and Material body-medium all 14 px), with 12 px as the smallest "label/caption" step and 16 px as "large body". Spectrum states the desktop/mobile split outright: the same token is 14 px on desktop and 17 px on mobile. Dense scales step 12 → 14 → 16 → 20 → 24/28 → 32, which suggests DashLens's 13, 15 and 18 px are off-scale steps.

### Cited Findings
**IBM Carbon (productive set, from `@carbon/type` source `scss/_styles.scss` and `_scale.scss`)**
- Carbon type scale formula: step 1 = 12 px, each next step = previous + (floor((step−2)/4)+1)×2. That gives 12, 14, 16, 18, 20, 24, 28, 32, 36, 42, 48, 54 … "supports sizes from 12px to 92px". — [@carbon/type](https://www.npmjs.com/package/@carbon/type)
- `label-01` / `helper-text-01` / `legal-01` / `caption-01`: 12 px, line-height 1.33333 (16 px), 400, letter-spacing 0.32 px. — [@carbon/type](https://www.npmjs.com/package/@carbon/type)
- `label-02` / `helper-text-02`: 14 px, lh 1.28572 (18 px), 400, 0.16 px. — same
- `body-compact-01` (= body-short-01): 14 px / 18 px (1.28572), 400, 0.16 px. `body-01` (= body-long-01): 14 px / 20 px (1.42857), 400. — same
- `body-compact-02`: 16 px / 22 px (1.375), 400. `body-02`: 16 px / 24 px (1.5), 400. — same
- `code-01`: mono 12 px / 16 px, 400, 0.32 px. `code-02`: mono 14 px / 20 px, 400, 0.32 px. — same
- `heading-compact-01` (= productive-heading-01): 14 px / 18 px, **600** (semibold), 0.16 px. `heading-compact-02`: 16 px / 22 px, **600**. `heading-01`: 14/20 600; `heading-02`: 16/24 600. — same
- `heading-03`: 20 px / 28 px (1.4), **400**. `heading-04`: 28 px / 36 px, 400. `heading-05`: 32 px / 40 px, 400. `heading-06`: 42 px / 1.199, **300 (light)**. `heading-07`: 54 px / 1.19, **300**. — same
- Carbon font-weight map has only three entries: light 300, regular 400, semibold 600 (no 700). — [@carbon/type `_font-family.scss`](https://www.npmjs.com/package/@carbon/type)

**Microsoft Fluent 2 (from `@fluentui/tokens` `lib/global/typographyStyles.js` and `fonts.js`)**
- Sizes: Base100 10 px, Base200 12, Base300 14, Base400 16, Base500 20, Base600 24, Hero700 28, Hero800 32, Hero900 40, Hero1000 68. Line heights: 14, 16, 20, 22, 28, 32, 36, 40, 52, 92. Weights: Regular 400, Medium 500, Semibold 600, Bold 700. — [@fluentui/tokens](https://www.npmjs.com/package/@fluentui/tokens)
- Ramp: Caption 2 10/14 400; Caption 1 12/16 400 (Strong 600, Stronger 700); **Body 1 14/20 400** (Strong 600, Stronger 700); Body 2 16/22 400; Subtitle 2 16/22 600; Subtitle 1 20/28 600; Title 3 24/32 600; Title 2 28/36 600; Title 1 32/40 600; Large Title 40/52 600; Display 68/92 600. — same
- Every Fluent heading style, Display included, uses Semibold 600. Bold 700 is only offered as a "Stronger" variant of Caption 1/Body 1/Subtitle 2. — same

**Apple macOS (HIG Typography, fetched as Markdown)**
- Default/minimum text size: macOS 13 pt / 10 pt; iOS/iPadOS 17 pt / 11 pt. — [Apple HIG Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- macOS built-in text styles (weight, size/line height pt, emphasized weight): Large Title Regular 26/32 (Bold); Title 1 Regular 22/26 (Bold); Title 2 Regular 17/22 (Bold); Title 3 Regular 15/20 (Semibold); **Headline Bold 13/16 (Heavy)**; **Body Regular 13/16 (Semibold)**; Callout Regular 12/15 (Semibold); Subheadline Regular 11/14 (Semibold); Footnote Regular 10/13 (Semibold); Caption 1 Regular 10/13 (Medium); Caption 2 Medium 10/13 (Semibold). — [Apple HIG Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- Note: macOS headings get their hierarchy at the *same* 13 pt size through weight (Headline = Bold), and titles are Regular weight at a larger size. — same (inference from the table)
- "In general, avoid light font weights … prefer Regular, Medium, Semibold, or Bold … avoid Ultralight, Thin, and Light font weights, which can be difficult to see, especially when text is small." — [Apple HIG Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- "Adjust font weight, size, and color as needed to emphasize important information and help people visualize hierarchy." "Minimize the number of typefaces you use." — same

**GitHub Primer (from `@primer/primitives` `dist/css`)**
- Base sizes: xs 12 px ("Smallest text size for captions and compact UI elements"), sm 14 px ("Default body text size for UI"), md 16, lg 20, xl 32, 2xl 40. Weights: light 300, normal 400, medium 500, semibold 600. — [@primer/primitives](https://www.npmjs.com/package/@primer/primitives)
- Semantic styles: body-medium 14 px 400 ("Default UI font"); body-small 12 px 400 with 20 px line height ("helper, footnote … Should be used sparingly"); caption 12 px/16 px 400 ("use it for single-line scenarios, as the small sizing doesn't pass accessibility requirements"); title small/medium/large 16/20/32 px all **600**; subtitle 20 px 400; display 40 px **500**; codeBlock 13 px (0.8125 rem). — same

**Atlassian (from `@atlaskit/tokens` `atlassian-typography.js`)**
- body-small 12/16 400; **body 14/20 400**; body-large 16/24 400. Headings xxsmall 12/16, xsmall 14/20, small 16/20, medium 20/24, large 24/28, xlarge 28/32, xxlarge 32/36, all weight **653** (= `font-weight-bold`). Weights: regular 400, medium 500, semibold 600, bold 653. Code 0.875 em. — [@atlaskit/tokens](https://www.npmjs.com/package/@atlaskit/tokens)
- **Metric tokens** (for numeric KPIs): metric-small 16/20, metric-medium 24/28, metric-large 28/32, all weight 653. — same

**Adobe Spectrum (from `@adobe/spectrum-tokens` `src/typography.json`, `body.json`)**
- Each font-size token has a desktop and a mobile value: font-size-50 11/13 px, 75 12/15, **100 14/17**, 200 16/19, 300 18/22, 400 20/24, 500 22/27, 700 28/34, 900 36/44 (desktop/mobile). — [@adobe/spectrum-tokens](https://www.npmjs.com/package/@adobe/spectrum-tokens)
- body-size-xs = font-size-75 (12 px desktop), body-size-s = font-size-100 (14), body-size-m = font-size-200 (16 desktop); detail-size-m = font-size-100; heading-size-m = font-size-500 (22). — same

**Vercel Geist (typography page)**
- Classes: label-12, label-13, label-14, label-16, label-18, label-20 (plus -mono 12/13/14), copy-13/14/16/18/20/24 (copy-13-mono), heading-14 … heading-72. — [Geist Typography](https://vercel.com/geist/typography)
- "Label 14 … Most common text style of all." "Label 13 … Used as a secondary line next to other labels" (shown "with Strong, and Tabular (123)"). "Label 12 … Used for tertiary level text in busy views." "Label 13 Mono … pair with Label 14, as the smaller mono size looks better in that pairing." Labels are "Designed for single-lines … marrying up with icons." — [Geist Typography](https://vercel.com/geist/typography)
- Exact line-heights and weights for each Geist class were not visible in the fetched HTML. **[UNVERIFIED]**

**Material 3**
- `@material/web` fallback values: body-large 1 rem/1.5 rem 400; body-medium 0.875 rem (14 px)/1.25 rem (20 px) 400. — [@material/web](https://www.npmjs.com/package/@material/web)
- Rest of the M3 scale (body-small 12/16 400; label-large 14/20 500; label-medium 12/16 500; label-small 11/16 500; title-medium 16/24 500; title-large 22/28 400). **[UNVERIFIED]** The m3.material.io page is rendered by JavaScript, so its text could not be read.

### Inferences
- Agreement across systems: 12 px (label/caption), 14 px (default UI/body), 16 px (large body/subheading), 20 px (section title), 24–32 px (page title/display). For DashLens: **12 / 14 / 16 / 20 px plus one display step (28–32 px)** for the speed readout. Today's 13, 15 and 18 px fall between those steps.
- If DashLens keeps a 13 px step (Apple's macOS body, Geist label-13), keep it as the *only* secondary size. Don't use both 13 and 12.
- Why desktop is smaller: Spectrum's paired tokens (14 desktop vs 17 mobile) and Apple's defaults (13 macOS vs 17 iOS) are the cited evidence. The usual reasons (longer viewing distance on phones, precise mouse pointers, higher information density on large screens) are not explained in the sources read here. **[UNVERIFIED rationale]**

### Gaps
- Fluent 2 web site text (usage guidance) not reachable; values taken from tokens only.
- Carbon type-sets page prose on "productive vs expressive" not reachable. That productive is for product UI and expressive for editorial pages is **[UNVERIFIED]**, though the package does name `productive-heading-*` and `expressive-heading-*`.

## 2. How many sizes and weights; weight vs size vs colour; numeric readouts

### Takeaway
The pro systems use 3–4 weights and keep headings at 600 (Carbon, Fluent, Primer) or a single "bold" of 653 (Atlassian). None needs 900, and Carbon has no 700 at all. Big numerals in these systems are *lighter*, not heavier: Carbon goes 400 at 20–32 px and 300 at 42+ px, and Primer display is 500. Atlassian is the exception with 653 "metric" tokens. Hierarchy comes from size, weight and colour/contrast together (Apple, NN/g).

### Cited Findings
- Weights offered: Carbon 300/400/600 — [@carbon/type](https://www.npmjs.com/package/@carbon/type); Fluent 400/500/600/700 — [@fluentui/tokens](https://www.npmjs.com/package/@fluentui/tokens); Primer 300/400/500/600 — [@primer/primitives](https://www.npmjs.com/package/@primer/primitives); Atlassian 400/500/600/653 — [@atlaskit/tokens](https://www.npmjs.com/package/@atlaskit/tokens).
- Carbon heading weight falls as size rises: 14–16 px headings are 600, 20–32 px are 400, 42–54 px are 300. — [@carbon/type](https://www.npmjs.com/package/@carbon/type)
- Primer display (40 px) uses medium 500, titles 600. — [@primer/primitives](https://www.npmjs.com/package/@primer/primitives)
- Atlassian metric-small/medium/large = 16/24/28 px at 653. — [@atlaskit/tokens](https://www.npmjs.com/package/@atlaskit/tokens)
- Apple: hierarchy is built by "font weight, size, and color"; avoid light weights at small sizes. — [Apple HIG Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- NN/g: visual hierarchy "can be created through variations in color and contrast, scale, and grouping." "It's not the actual color of an element that creates the hierarchy, but rather the contrast in value and saturation between the element and the context." "Typefaces with heavy weight, like bold, stand out against light-weighted or regular typefaces." "Don't use too many colors." "Reserve warm bright colors, like red, for warnings or errors." — [NN/g, Visual Hierarchy in UX](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/)
- Tabular numerals: Geist shows "Label 13 with Strong, and Tabular (123)", a tabular-figure variant for secondary numeric labels. — [Geist Typography](https://vercel.com/geist/typography)
- Grafana Stat panel: the options are Text mode (Value / Value and name / Name …), Color mode ("Value – Applies color to the value and graph area", or background) and Graph mode (sparkline). "If the value is not important, only the name and color is, then change the Text mode to Name." — [Grafana Stat docs](https://grafana.com/docs/grafana/latest/panels-visualizations/visualizations/stat/)
- Grafana's "Text size" auto-fit option for title/value. **[UNVERIFIED]** The option name appeared, but its description was not captured.
- IBM Plex Sans/Mono support OpenType `tnum` (tabular figures) and Plex Mono is fixed-width by definition. **[UNVERIFIED in this session]**
- Car instrument clusters and trading terminals: **no free primary source found** in this session.

### Inferences
- For DashLens: allow **400, 500 and 600 only**. Set `b, strong { font-weight: 600 }` so the browser default `bolder` cannot produce 700/900.
- Speed readout: 30 px/700 is heavier than any reference system's display style. A setting in line with the references would be 28–32 px at 400–500 (Carbon 28 px/400 or 32 px/400; Primer display 500), with `font-variant-numeric: tabular-nums` (or Plex Mono) so digits don't jitter as the value changes. Put units (km/h) at 12–14 px in secondary text colour. Atlassian's 653 metrics are the outlier. If DashLens wants a strong number, 600 is the ceiling.
- Aim for one size per role: tertiary 12, body/label 14 (or 13), panel heading 14–16 at 600, section/dialog title 20, display numerals 28–32. That gives 5 sizes and 3 weights.

### Gaps
- No free primary source on automotive cluster typography (ISO 15008 is paywalled) or on Bloomberg terminal typography.

## 3. Hierarchy without borders: dark surface elevation, shadows, separators

### Takeaway
Dark systems show elevation by making raised surfaces lighter. Carbon steps 10–13 lightness units per layer (#161616 → #262626 → #393939 → #525252). Radix, Atlassian and Fluent use finer steps of about 4–8 units (Radix #111111 → #191919 → #222222 → #2a2a2a). Shadows are weak on dark backgrounds, so they are paired with a 1 px light outline (Primer, Atlassian) or replaced by lightness.

### Cited Findings
- **Carbon Gray 100** (`@carbon/themes` `scss/generated/_themes.scss`): background #161616; layer-01 #262626; layer-02 #393939; layer-03 #525252; layer-hover-01 #333333; layer-selected-01 #393939; field-01 #262626; border-subtle-00 #393939; border-subtle-01 #525252; border-strong-01 #6f6f6f; overlay rgba(0,0,0,0.6); shadow rgba(0,0,0,0.8); focus #ffffff; interactive #4589ff. — [@carbon/themes](https://www.npmjs.com/package/@carbon/themes)
- Carbon Gray 90: background #262626; layer-01 #393939; layer-02 #525252; layer-03 #6f6f6f. — same
- **Fluent 2 web dark** (`alias/darkColor.js` + `global/colors.js`): Background1 grey[16] #292929; Background2 grey[12] #1f1f1f; Background3 grey[8] #141414; Background4 grey[4] #0a0a0a; Background5 black; Background6 grey[20] #333333; Background1Hover grey[24] #3d3d3d; Stroke1 grey[40] #666666; Stroke2 grey[32] #525252; StrokeAccessible grey[68] #adadad. Dark shadows: ambient rgba(0,0,0,0.24), key rgba(0,0,0,0.28); shadow4 = `0 0 2px ambient, 0 2px 4px key`; shadow16 = `0 0 2px, 0 8px 16px`; shadow28 = `0 0 8px, 0 14px 28px`. — [@fluentui/tokens](https://www.npmjs.com/package/@fluentui/tokens)
- **Primer dark**: bgColor-inset #010409; bgColor-default #0d1117; bgColor-muted #151b23; bgColor-emphasis #3d444d; borderColor-default #3d444d; borderColor-muted #3d444db3; shadow-floating-small `0 0 0 1px #3d444d, 0 6px 12px -3px #01040966, 0 6px 18px 0 #01040966`. A floating shadow in dark mode includes a 1 px border ring. — [@primer/primitives](https://www.npmjs.com/package/@primer/primitives)
- **Atlassian dark** (`atlassian-dark.js`, v20.15.0): surface-sunken #18191A; surface #1F1F21; surface-raised #242528; surface-overlay #2B2C2F; border #E3E4F21F (a white-ish border at about 12 % alpha); shadow-raised `0 1px 1px #01040480, 0 0 1px #01040480`; shadow-overlay `0 0 0 1px #BDBDBD1F, 0 8px 12px #0104045C, 0 0 1px 1px #01040480`. — [@atlaskit/tokens](https://www.npmjs.com/package/@atlaskit/tokens)
- **Radix gray dark** steps 1–12: #111111, #191919, #222222, #2a2a2a, #313131, #3a3a3a, #484848, #606060, #6e6e6e, #7b7b7b, #b4b4b4, #eeeeee. — [@radix-ui/colors](https://www.npmjs.com/package/@radix-ui/colors)
- Radix step roles: "Steps 1 and 2 are designed for app backgrounds and subtle component backgrounds. Steps 3, 4, and 5 … UI component backgrounds." "Steps 6, 7, and 8 are designed for borders" (6 subtle non-interactive, 7 interactive, 8 stronger/focus rings). "Steps 9 and 10 … solid backgrounds." "Step 11 … low-contrast text. Step 12 … high-contrast text." — [Radix, Understanding the scale](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)
- **Material (Android MDC docs)**: "The baseline Material Dark theme background and surface colors are dark grey instead of black, which increases visibility for shadows and also reduces eye strain for light text." "Shadows are less effective in an app using a dark theme … Material surfaces become lighter and more colorful at higher elevations … accomplished via elevation overlays, which are semi-transparent (colorPrimary) overlays." Elevation overlays "ha[ve] been replaced in Material 3" by tonal surface colours. — [material-components-android Dark.md](https://github.com/material-components/material-components-android/blob/master/docs/theming/Dark.md)
- M2 dark theme specifics: surface #121212, white overlay at 0 dp 0 %, 1 dp 5 %, 2 dp 7 %, 3 dp 8 %, 4 dp 9 %, 6 dp 11 %, 8 dp 12 %, 12 dp 14 %, 16 dp 15 %, 24 dp 16 %; text at 87 % / 60 % / 38 % white. **[UNVERIFIED]** m2.material.io is rendered by JavaScript and could not be read.
- **Apple**: "Dark Mode is dynamic … the background color automatically changes from base to elevated when an interface is in the foreground, such as a popover or modal sheet." — [Apple HIG Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode). "In rare cases, consider using only a dark appearance … an app that supports immersive media viewing … lets the UI recede and helps people focus on the media." — same. Liquid Glass: "Don't use Liquid Glass in the content layer"; "Use Liquid Glass effects sparingly." — [Apple HIG Materials](https://developer.apple.com/design/human-interface-guidelines/materials)

### Inferences
- DashLens's #121212 base sits between Radix step 1 (#111111) and Atlassian sunken (#18191A). A ladder for panels/drawers/dialogs could be: app #121212 → panel ~#1a1a1a → raised/drawer ~#222222 → dialog/popover ~#2a2a2a, with hover = one step up. Borders would be ~#3a3a3a (Radix 6) for subtle and ~#484848 (Radix 7) for interactive.
- Dialogs: lighter surface + 1 px outline at about 12 % white + a dark shadow (Primer/Atlassian pattern). A shadow alone barely shows on #121212.
- Apple's "permanently dark for immersive media" guidance supports DashLens being dark-only. Video should sit on the darkest surface so the footage is the brightest thing on screen.

### Gaps
- Apple's macOS semantic background hex values (windowBackgroundColor, etc.) are not published in the HIG Markdown read here.

## 4. Colour hierarchy: text emphasis levels, one accent, status and data-vis colours

### Takeaway
Dark systems use 3–4 text levels. Examples: Carbon #f4f4f4 / #c6c6c6 / #a8a8a8 / placeholder 40 % / disabled 25 %; Fluent white / #d6d6d6 / #adadad / #999999 / #5c5c5c; Atlassian #CECFD2 / #A9ABAF / #96999E. Status colours on dark are bright, mid-saturation hues. Radix gives each hue a solid step 9 (fills) and a step 11 (text on dark). The NN/g preattentive guidance is to use colour for category, not magnitude.

### Cited Findings
- **Carbon g100 text**: text-primary #f4f4f4; text-secondary #c6c6c6; text-helper #a8a8a8; text-placeholder rgba(244,244,244,0.4); text-disabled rgba(244,244,244,0.25); text-on-color #ffffff; icon-primary #f4f4f4; icon-secondary #c6c6c6; link-primary #78a9ff. — [@carbon/themes](https://www.npmjs.com/package/@carbon/themes)
- **Carbon g100 support colours**: error #fa4d56; success #42be65; warning #f1c21b; caution-major #ff832b; info #4589ff. — same
- **Fluent dark foregrounds**: Foreground1 white; Foreground2 grey[84]; Foreground3 grey[68] #adadad; Foreground4 grey[60] #999999; Disabled grey[36] #5c5c5c. — [@fluentui/tokens](https://www.npmjs.com/package/@fluentui/tokens). (grey[84] = #d6d6d6 by Fluent's grey-percentage naming. **[UNVERIFIED hex]**: that line was cut off in extraction.)
- **Primer dark text**: fgColor-default #f0f6fc; fgColor-muted #9198a1; fgColor-disabled #656c76; fgColor-accent #4493f8. — [@primer/primitives](https://www.npmjs.com/package/@primer/primitives)
- **Atlassian dark text**: text #CECFD2; text-subtle #A9ABAF; text-subtlest #96999E; text-disabled #E5E9F640. — [@atlaskit/tokens](https://www.npmjs.com/package/@atlaskit/tokens)
- **Radix dark hue steps 9 / 10 / 11 (solid / hover / text)**: amber #ffc53d / #ffd60a / #ffca16; orange #f76b15 / #ff801f / #ffa057; red #e5484d / #ec5d5e / #ff9592; green #30a46c / #33b074 / #3dd68c; blue #0090ff / #3b9eff / #70b8ff. Step 3 (tinted backgrounds): amber #302008, red #3b1219, green #132d21, blue #0d2847. — [@radix-ui/colors](https://www.npmjs.com/package/@radix-ui/colors); roles per [Radix scale docs](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale) ("Step 9 has the highest chroma of all steps").
- **Apple**: "At a minimum, make sure the contrast ratio between colors is no lower than 4.5:1. For custom foreground and background colors, strive for a contrast ratio of 7:1, especially in small text." Use "primary, secondary, tertiary, and quaternary label colors". — [Apple HIG Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- **NN/g preattentive**: "people do not perceive different colors as being in a particular order, so color should not be used to communicate information about quantitative values or magnitude." Colour/shape "can be used to convey categorical information". "Color properties such as hue or saturation are helpful as a secondary grouping cue, rather than as the main way of showing groups"; "2D position and length are the two preattentive attributes that can be naturally mapped onto quantity." — [NN/g, Dashboards: Making Charts and Graphs Easier to Understand](https://www.nngroup.com/articles/dashboards-preattentive/)
- **APCA guidance** (W3 repo README): "For body text, add Lc 15 for any value on the table lower than Lc 75." "For sub-fluent text (i.e. not primary content) Lc values can be lowered by Lc 15, but in no case less than Lc 30." "For non-fluent spot text (copyright bug, disabled text, placeholder) … lowered by Lc25, but in no case less than Lc 30." "Fonts larger than 24px and weight 300 or more have a maximum contrast of Lc 90." — [Myndex/apca-w3 README](https://github.com/Myndex/apca-w3)
- APCA headline targets (Lc 90 preferred body, Lc 75 minimum body, Lc 60 other content text, Lc 45 large/headline text, Lc 30 spot text, Lc 15 non-text minimum). **[UNVERIFIED]** The "APCA in a Nutshell" page did not return text.
- Carbon / Datadog / Grafana dark data-vis palettes: **not read in this session [GAP]**.

### Inferences
- DashLens's #ffb020 accent lies between Radix amber-dark 9 (#ffc53d) and orange-dark 10 (#ff801f). In Radix's system, a hue's step 9 is for solid fills (buttons, the playhead) and step 11 is the text variant. Because the accent is amber, **warning status must not be amber/yellow** or the accent will look like an alert (Carbon's warning #f1c21b and caution #ff832b are close to it). Status colours could be red #e5484d/#ff9592, green #30a46c/#3dd68c and blue #0090ff/#70b8ff, with warning shown through an icon and text rather than hue alone.
- Text levels mapped onto DashLens's #121212 → #ededed range: primary #ededed (Radix 12 #eeeeee), secondary ~#b4b4b4 (Radix 11; Carbon #c6c6c6 is brighter), tertiary/helper ~#a8a8a8 at minimum for 12 px text, disabled ~#6e6e6e. Contrast was not computed here.

### Gaps
- Carbon data-visualization dark palette hex values and Grafana's classic palette were not retrieved because of the network limits.

## 5. Visual weight and scanning in wide landscape layouts; focal point; squint test; grouping

### Takeaway
NN/g treats the F-pattern as a *failure mode*. It is "the default pattern when there are no strong cues", not a layout to design for. Strong visual cues (contrast, size, grouping) decide where people look. The blur/squint test is NN/g's recommended check: with a 5–10 px blur, the intended focal element (here, the video) should still dominate.

### Cited Findings
- "The F-pattern is negative for users and businesses." "The F-pattern is the default pattern when there are no strong cues to attract the eyes towards meaningful information." — [NN/g, F-Shaped Pattern of Reading](https://www.nngroup.com/articles/f-shaped-pattern-reading-web-content/)
- "In design school, we are taught to squint or apply a slight blur to the design to get an idea of the conveyed groupings and hierarchy." Blur at 5 or 10 px showed the intended grouping. At 20 px, "an unintended hierarchy" appeared "due to its strong color". — [NN/g, Visual Hierarchy in UX](https://www.nngroup.com/articles/visual-hierarchy-ux-definition/)
- NN/g counter-example: a page where "the elements … are all relatively equal in size and color and lack breathing room", so the eye has no place to start. — same
- Gestalt similarity: "items that have similar shape or color are usually perceived as related"; "Shape or clear visual grouping are more reliable signals for relatedness." — [NN/g Dashboards preattentive](https://www.nngroup.com/articles/dashboards-preattentive/)
- Apple: a permanently dark UI for media viewing "lets the UI recede and helps people focus on the media." — [Apple HIG Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)

### Inferences
- In DashLens the video is the focal point. Panels (telemetry, map, timeline) should sit on darker or neutral surfaces with secondary-grey labels, so the only bright, saturated items are the video, the accent (playhead/selected event) and the main readout (speed).
- Squint test: blur a screenshot at 5–10 px. Order of prominence should be video → speed readout/playhead → everything else. If an event-colour chip or a bold 900 label wins, the hierarchy is wrong.
- Group by proximity and shared surface (one panel = one surface tone) rather than by borders around every item.

### Gaps
- No free NN/g article specifically on scanning *wide landscape* dashboards was found. Grid/landscape scanning claims remain uncited.

## 6. Iconography on desktop

### Takeaway
Use one icon family, sized at 16 px (dense rows) and 20 px (toolbars), with a single stroke width. Lucide's rule is 24 × 24 px with a 2 px stroke "don't mix stroke widths". Scaled to 16–20 px that becomes about 1.33–1.67 px, so either set Lucide `stroke-width` to about 1.5 at small sizes or use a family drawn for 16/20 (Carbon, Fluent).

### Cited Findings
- Lucide: "Strokes must be 2 pixels wide." "Don't use thicker or thinner strokes, or mix stroke widths." "Icons must have at least 1 pixel of padding between their strokes and the edge of the canvas." "Distinct elements must have at least 2 pixels of visual spacing between them." — [Lucide Icon Design Guide](https://lucide.dev/guide/design/icon-design-guide)
- Lucide canvas is 24 × 24. **[UNVERIFIED in captured text]**, but it is the documented default `size` prop.
- Fluent product icons: "As the product icons scale below 48 pixels, they simplify in detail in favor of readability"; scale up "by factors of four (48, 64, 96…)". — [Fluent 2 Iconography](https://fluent2.microsoft.design/iconography) (fetched via curl; this covers *product/app* icons, not UI icons)
- Fluent System Icons sizes 16/20/24/28/32/48 with Regular/Filled styles. **[UNVERIFIED]** The README text captured did not list them.
- Carbon UI icons on 16/20/24/32 artboards, designed at 16 and 20 for product UI. **[UNVERIFIED]** The page is a Next.js app and the text was not extractable.
- Apple: "Use SF Symbols wherever possible"; symbols "automatically align with text in all weights and sizes". — [Apple HIG Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode), [Apple HIG Typography](https://developer.apple.com/design/human-interface-guidelines/typography)
- Geist "Label" styles are "given ample line-height for … marrying up with icons", so the icon and its text label are treated as one unit. — [Geist Typography](https://vercel.com/geist/typography)

### Inferences
- DashLens: 16 px icons in lists, the timeline and readouts; 20 px in the main toolbar; one stroke width across all icons. Icon-only buttons need a tooltip and an `aria-label`. Infrequent or ambiguous actions (export, privacy) work better as icon + label.
- Match icon weight to text weight. A 2 px stroke at 16 px looks bolder than 400-weight 12–14 px text, so about 1.5 px is closer to Plex at 400–500. This is a visual judgement, not a sourced rule.

### Gaps
- NN/g's free articles on icon-only vs labelled icons ("Icon Usability") were not fetched in this session because of the tool budget.
