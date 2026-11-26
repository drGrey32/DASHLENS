# Spacing scales, layout grids and alignment for dense desktop web apps (DashLens)

Method note: the design-system websites carbondesignsystem.com, atlassian.design, primer.style and fluent2.microsoft.design could not be opened with the WebFetch tool in this session (DNS refused). They were read with curl instead, and the exact token values were taken from each system's own published npm package (the source of truth for the code), read on 2026-11-26. All token URLs below point to the same files on unpkg.com (free, no login). Versions: @carbon/layout 11.63.0, @atlaskit/tokens 20.15.0, @primer/primitives 11.10.0, @adobe/spectrum-tokens 15.9.1, @fluentui/tokens 1.0.0-alpha.25, @shopify/polaris-tokens 9.4.2, @radix-ui/themes 3.3.0, tailwindcss 4.3.5. All are packages current in late 2026. rem values are converted at 1rem = 16px, which is Carbon's stated `baseFontSize = 16` and the browser default.

## Exact spacing tokens and base units of the major design systems

### Takeaway
Every system checked uses a 4 px grid with an 8 px "main" step. Seven of the eight share the same core steps, **4, 8, 12, 16, 24, 32**, and most add **2** (hairline/icon) and some add **6** and **20** as half-steps. Above 32 they jump to 40, 48 and 64. No system has 5, 7, 10 (except Fluent's "nudge"), 11, 14 or 18 as a spacing step. Those are the odd values in the DashLens audit.

### Cited Findings

**IBM Carbon**
- Spacing tokens (verified): `$spacing-01` 0.125rem = 2px, `-02` 0.25rem = 4, `-03` 0.5rem = 8, `-04` 0.75rem = 12, `-05` 1rem = 16, `-06` 1.5rem = 24, `-07` 2rem = 32, `-08` 2.5rem = 40, `-09` 3rem = 48, `-10` 4rem = 64, `-11` 5rem = 80, `-12` 6rem = 96, `-13` 10rem = 160. — [@carbon/layout _spacing.scss](https://unpkg.com/@carbon/layout@11.63.0/scss/generated/_spacing.scss); same table on [Carbon Spacing overview](https://carbondesignsystem.com/elements/spacing/overview/)
- "The Carbon spacing scale complements the 2x Grid and typography scale by using multiples of two, four, and eight. It includes both small increments needed to create appropriate spatial relationships for detail-level designs as well as larger increments used to control the density of a design." — [Carbon Spacing](https://carbondesignsystem.com/elements/spacing/overview/)
- Tokens are not responsive: "the tokens themselves do not change values based on the screen size. However, it is acceptable at page breakpoints to jump a step(s) on the spacing scale (i.e., at 1440 px padding-right: $spacing-05 but at breakpoint 768px padding-right: $spacing-03)." Off-scale values: "deviating from the spacing scales should be avoided whenever possible." — [Carbon Spacing FAQ](https://carbondesignsystem.com/elements/spacing/overview/)
- Mini unit: `export const miniUnit = 8;` with `miniUnits(count) = rem(8 * count)`. — [@carbon/layout src/index.ts](https://unpkg.com/@carbon/layout@11.63.0/src/index.ts)
- 2x Grid: "The basic unit of 2x Grid geometry is the 8-pixel square mini unit. Multiples of mini units compose the dimensions of columns, rows, boxes, along with their margins and padding." "The core concept of the 2x Grid is to divide or multiply by two." "For dense content, use mini units for further alignment and spatial guidance." — [Carbon 2x Grid overview](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Other Carbon layout tokens (verified): `$layout-01..07` = 16, 24, 32, 48, 64, 96, 160 px ([_layout.scss](https://unpkg.com/@carbon/layout@11.63.0/scss/generated/_layout.scss)); control sizes `$size-xs` 24, `sm` 32, `md` 40, `lg` 48, `xl` 64 px ([_size.scss](https://unpkg.com/@carbon/layout@11.63.0/scss/generated/_size.scss)); `$container-01..05` 24, 32, 40, 48, 64 px; `$icon-size-01` 16 px, `-02` 20 px; `$fluid-spacing-01..04` = 0, 2vw, 5vw, 10vw. — [@carbon/layout scss/generated](https://unpkg.com/@carbon/layout@11.63.0/scss/generated/_container.scss)

**Atlassian**
- Base unit 8 px; token number = percent of base: "space.200 is 200% of the size of the base unit, therefore represents 16px." Range "from 0px to 80px". — [Atlassian Spacing](https://atlassian.design/foundations/spacing)
- Tokens (verified): `space.0` 0, `space.025` 2px, `space.050` 4, `space.075` 6, `space.100` 8, `space.150` 12, `space.200` 16, `space.250` 20, `space.300` 24, `space.400` 32, `space.500` 40, `space.600` 48, `space.800` 64, `space.1000` 80. Negative `space.negative.025` to `space.negative.400` (−2 to −32 px). — [@atlaskit/tokens token-default-values.js](https://unpkg.com/@atlaskit/tokens@20.15.0/dist/esm/artifacts/token-default-values.js)
- Three ranges: "space.0 to space.100 (0px to 8px) for small and compact pieces of UI" (badges, icon buttons, table cells; title-to-description in a card; trigger-to-menu gap); "space.150 to space.300 (12px to 24px) for larger and less dense pieces of UI"; "space.400 to space.1000 (32px to 80px) for the largest pieces of UI and for layout elements". — [Atlassian Spacing](https://atlassian.design/foundations/spacing)
- Newer semantic tokens in the 2026 package split **gap** from **inset** (padding): `space.gap.xxsmall` 2, `xsmall` 4, `small` 6, `medium` 8, `large` 12, `xlarge` 16, `xxlarge` 24; `space.inset.xxsmall` 2, `xsmall` 4, `small` 6, `medium` 8, `large` 12, `xlarge` 16, `xxlarge` 20, `3xlarge` 24, `4xlarge` 32, `5xlarge` 48. Their descriptions say gap tokens are "Do not use for component insets or dimensions" and inset tokens are "padding between a surface and its content … Do not use for gaps, margins, or dimensions." — [@atlaskit/tokens token-default-values.js](https://unpkg.com/@atlaskit/tokens@20.15.0/dist/esm/artifacts/token-default-values.js); descriptions in [tokens-raw/atlassian-spacing.js](https://unpkg.com/@atlaskit/tokens@20.15.0/dist/esm/artifacts/tokens-raw/atlassian-spacing.js). (Not verified: whether these semantic tokens are documented as stable on atlassian.design yet.)

**GitHub Primer**
- Base size scale (verified): `--base-size-2` 2px, `-4` 4, `-6` 6, `-8` 8, `-12` 12, `-16` 16, `-20` 20, `-24` 24, `-28` 28, `-32` 32, `-36` 36, `-40` 40, `-44` 44, `-48` 48, `-64` 64, `-80` 80, `-96` 96, `-112` 112, `-128` 128. — [@primer/primitives base/size/size.css](https://unpkg.com/@primer/primitives@11.10.0/dist/css/base/size/size.css)
- Control sizes: `--control-xsmall-size` 24px, `small` 28, `medium` 32, `large` 40, `xlarge` 48. Inline padding for small/medium/large/xlarge controls: `condensed` 8, `normal` 12, `spacious` 16 (xsmall: 4 / 8 / 12). Block padding: xsmall 2, small 4, medium 6, large 10, xlarge 14. Gap between icon and label: xsmall and small 4, medium and up 8. — [@primer/primitives functional/size/size.css](https://unpkg.com/@primer/primitives@11.10.0/dist/css/functional/size/size.css)
- Stack tokens: `--stack-gap-condensed` 8, `normal` 16, `spacious` 24; `--stack-padding-condensed` 8, `normal` 16, `spacious` 24. `--controlStack-*-gap-condensed` 8, `spacious` 12 (small: 16). Overlay: `--overlay-padding-condensed` 8, `normal` 16; `--overlay-width-xsmall` 192, `small` 320, `medium` 480, `large` 640, `xlarge` 960 px. — [same file](https://unpkg.com/@primer/primitives@11.10.0/dist/css/functional/size/size.css)

**Adobe Spectrum**
- Spacing tokens (verified): `spacing-25` 1px, `spacing-50` 2, `spacing-75` 4, `spacing-85` 6, `spacing-100` 8, `spacing-200` 12, `spacing-300` 16, `spacing-350` 20, `spacing-400` 24, `spacing-500` 32, `spacing-600` 40, `spacing-700` 48, `spacing-800` 64, `spacing-900` 80, `spacing-1000` 96. — [@adobe/spectrum-tokens src/layout.json](https://unpkg.com/@adobe/spectrum-tokens@15.9.1/src/layout.json)
- Desktop vs mobile: in the 2026 tokens the `spacing-*` values have **one value** (no desktop/mobile sets). The **component** tokens do change by platform: `component-height-50` 20 (desktop) / 26 (mobile), `-75` 24/30, `-100` 32/40, `-200` 40/50, `-300` 48/60; `component-edge-to-text-75` 9/11, `-100` 12/15; `text-to-visual-100` 6/8. — [layout.json](https://unpkg.com/@adobe/spectrum-tokens@15.9.1/src/layout.json). This contradicts the assumption in the brief that Spectrum has a separate desktop spacing scale. Only control sizes and inner padding scale (mobile is about 1.25× desktop).
- "Not all elements grow at the same rate. Spectrum uses distinct spacing scales, each tuned to the elements they serve." "Closer elements are more associated. Distant elements are more independent." — [Spectrum Spacing](https://spectrum.adobe.com/page/spacing/)

**Microsoft Fluent 2**
- Global spacing ramp (verified on the site): `sizeNone` 0, `size20` 2, `size40` 4, `size60` 6, `size80` 8, `size100` 10, `size120` 12, `size160` 16, `size200` 20, `size240` 24, `size280` 28, `size320` 32, `size360` 36, `size400` 40, `size480` 48, `size520` 52, `size560` 56. — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- "The base unit is four pixels… A 4x system reduces confusion while being easy to implement." "The values 2, 6, and 10 account for extra padding in the Fluent icons and help to align the icons to the four pixel grid. Space is measured from an element's bounding box." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- Fluent UI React v9 code names: `none` 0, `xxs` 2px, `xs` 4, `sNudge` 6, `s` 8, `mNudge` 10, `m` 12, `l` 16, `xl` 20, `xxl` 24, `xxxl` 32 (as `spacingHorizontal*` / `spacingVertical*`). — [@fluentui/tokens lib/global/spacings.js](https://unpkg.com/@fluentui/tokens@1.0.0-alpha.25/lib/global/spacings.js)
- "It's important to use spacers as a tool for creating consistency, rather than blindly using consistent spacers. For example, when creating lists, adjust spacers to left align text and center align icons." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)

**Shopify Polaris**
- Tokens (verified; note the naming: 100 = 4px, not 8px as in Atlassian): `--p-space-0` 0, `-025` 1px, `-050` 2, `-100` 4, `-150` 6, `-200` 8, `-300` 12, `-400` 16, `-500` 20, `-600` 24, `-800` 32, `-1000` 40, `-1200` 48, `-1600` 64, `-2000` 80, `-2400` 96, `-2800` 112, `-3200` 128. Semantic: `--p-space-card-padding` = space-400 (16), `--p-space-card-gap` = space-200/400 (8 or 16 by breakpoint), `--p-space-button-group-gap` = space-200 (8), `--p-space-table-cell-padding` = space-150 (6). — [@shopify/polaris-tokens dist/css/styles.css](https://unpkg.com/@shopify/polaris-tokens@9.4.2/dist/css/styles.css)
- The polaris-react.shopify.com/design/space page now redirects to shopify.dev app docs. No guidance prose was found there. — [polaris-react.shopify.com](https://polaris-react.shopify.com/design/space)

**Radix Themes**
- `--space-1` 4px, `-2` 8, `-3` 12, `-4` 16, `-5` 24, `-6` 32, `-7` 40, `-8` 48, `-9` 64, each `calc(Npx * var(--scaling))`. — [@radix-ui/themes tokens/base.css](https://unpkg.com/@radix-ui/themes@3.3.0/tokens/base.css)
- Scaling options in the stylesheet: `data-scaling` 90%, 95%, 100%, 105%, 110% ([styles.css](https://unpkg.com/@radix-ui/themes@3.3.0/styles.css)). "Values which affect layout (spacing, font size, line height) scale relatively to each other based on the scaling value… This setting allows you to scale the UI density uniformly across your entire application." — [Radix Themes Spacing](https://www.radix-ui.com/themes/docs/theme/spacing)

**Tailwind CSS v4**
- One variable: `--spacing: 0.25rem` (4px); utilities compute `calc(var(--spacing) * <number>)`, so `p-3` = 12px, `p-4` = 16px etc. — [tailwindcss theme.css](https://unpkg.com/tailwindcss@4.3.5/theme.css); [Tailwind padding docs](https://tailwindcss.com/docs/padding)
- Breakpoints `sm` 40rem (640), `md` 48rem (768), `lg` 64rem (1024), `xl` 80rem (1280), `2xl` 96rem (1536). Container widths `3xs` 256, `2xs` 288, `xs` 320, `sm` 384, `md` 448, `lg` 512, `xl` 576, `2xl` 672, `3xl` 768 … `7xl` 1280 px. — [theme.css](https://unpkg.com/tailwindcss@4.3.5/theme.css)

### Inferences
- Steps shared by every system above (Polaris, Radix and Tailwind included): **4, 8, 12, 16, 24, 32**. **2** is in all except Radix. **6** and **20** appear in Atlassian, Primer, Spectrum, Fluent and Polaris but not Carbon or Radix. So a 4-based scale with only those half-steps is the consensus.
- A cross-system scale for DashLens: **0, 2, 4, 6, 8, 12, 16, 20, 24, 32, 48** (11 values, or 10 without 0), with 40/64 kept for large layout gaps only if needed. Mapping the audit's 12 gaps: 2→2, 4→4, 5→4 or 6, 6→6, 7→6 or 8, 8→8, 10→8 or 12, 11→12, 12→12, 14→12 or 16, 16→16, 18→16 or 20. A stricter option with no half-steps, like Carbon or Radix (2, 4, 8, 12, 16, 24, 32), also fits a dense app. Fluent's 2/6/10 exist only to absorb icon padding.
- Name tokens by px value or by step (for example `--space-12` or Atlassian-style `space.150`), not by t-shirt size. Polaris and Atlassian give the same number different px values (100 = 4px vs 8px), so a shared vocabulary only works if names map to px.

### Gaps
- Carbon "productive vs expressive" applies to the **type** tokens (productive/expressive headings). I found no Carbon spacing tokens split by productive/expressive. The Carbon type package was not read in this pass (not verified).
- Material 3 (m3.material.io) pages render only with JavaScript, and the text could not be extracted. The M3 "4dp grid" and spacing guidance are **not verified** here. The Material 2 "spacing methods" page also returned no text.
- Apple HIG Layout (read via its JSON data feed) has no fixed macOS window margin value (for example "20 pt"). It gives tvOS insets (60 pt top/bottom, 80 pt sides) and visionOS "button centers at least 60 points apart". A macOS margin value is **not verified**. — [HIG Layout](https://developer.apple.com/design/human-interface-guidelines/layout)
- Vercel Geist: the [Geist Grid](https://vercel.com/geist/grid) page documents a grid component with 3 breakpoints, but I found no published spacing token list. Linear: no public spacing tokens found. Salesforce Lightning: the token file request to unpkg returned nothing. All three are **not verified**.

## Why 4/8 px bases, and when 4 px half-steps are used

### Takeaway
The free primary sources give practical reasons, not research evidence: even numbers scale cleanly on 1.5× and 2× screens, 8 is divisible enough without too many options, and fewer choices speed up design and build. 4 px is the standard half-step for text line heights (a 4 pt baseline), icons and dense components.

### Cited Findings
- Elliot Dahl (Dec 2016): "Use increments of 8 to size and space out the elements on a page… any defined height or width, margin or padding will be an increment of 8." "Devices that have a 1.5x resolution will have a hard time cleanly rendering an odd number. Scaling 5px by 1.5x will result in a half pixel offset." "Scaling by increments of 8 offers a good amount of options without overloading you with variables like a 6 point system, or limiting you like a 10 point system." — [Intro to The 8-Point Grid System (Medium, Built to Adapt)](https://medium.com/built-to-adapt/intro-to-the-8-point-grid-system-d2573cde8632) (medium.com blocks direct fetch; text read from the publication's free RSS feed, medium.com/feed/@elliotdahl)
- Dahl on 4pt for type: "Material's spacing method is based on an 8pt component grid system and a 4pt baseline grid for typography… Scaling by increments of 8 with your baseline grid can be difficult because the available line-heights are too far apart for some text sizes." "You can always bump the spacing above or below a given line by 4px to make it align with the greater atomic grid." — [8-Point Grid: Typography On The Web (2018)](https://medium.com/free-code-camp/8-point-grid-typography-on-the-web-be5dc97db6bc)
- Dahl on borders: keep 8px padding "and allow the 1px border to hold space outside of the 8px internal padding" rather than "subtract 1px" (7px) logic, which "would only complicate our workflow." — [8-Point Grid: Borders And Layouts (2017)](https://medium.com/built-to-adapt/8-point-grid-borders-and-layouts-e91eb97f5091)
- Dahl on vertical rhythm: he generally measures "element to element" with a soft grid, and measuring by baseline in browsers "will become difficult to maintain and I would not recommend it for large design systems." — [8-Point Grid: Vertical Rhythm (2017)](https://medium.com/built-to-adapt/8-point-grid-vertical-rhythm-90d05ad95032)
- Spec.fm: "Use multiples of 8 to define dimensions, padding, and margin of both block and inline elements." "By removing 7 of every 8 spacing options, you reduce the amount of fiddling available to you and subsequently reduce speed to code." "I like to combine my 8pt UI grid with a 4pt baseline grid." It describes "Hard Grid" (snap containers to an 8pt grid) vs "Soft Grid" (measure 8pt between elements). For buttons: "use padding to determine the size of the block element." — [Spec.fm, The 8-Point Grid](https://spec.fm/specifics/8-pt-grid)
- Dahl credits Bryn Jackson for the idea ("after hearing Bryn Jackson avidly talk about…"). — [Intro to The 8-Point Grid System](https://medium.com/built-to-adapt/intro-to-the-8-point-grid-system-d2573cde8632)
- Fluent: 2, 6 and 10 exist "to account for extra padding in the Fluent icons and help to align the icons to the four pixel grid." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- Carbon: "For dense content, use mini units for further alignment"; "When interior space within a component is cramped, use the minor sizing scale." — [Carbon 2x Grid](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Atlassian assigns 0–8px (incl. 2, 4, 6) to "small and compact pieces of UI… badges, icon buttons, table cells". — [Atlassian Spacing](https://atlassian.design/foundations/spacing)

### Inferences
- For DashLens: use 8-multiples (8, 16, 24, 32) between regions and groups. Keep 2/4/6/12 for inside controls, chips, timeline lane labels and icon-to-text gaps. Snap line heights to 4 (for example 12px text / 16px line, 14 / 20, 16 / 24).
- Don't subtract border widths from padding (Dahl's rule): 1px borders sit outside the token padding.

### Gaps
- Bryn Jackson's own original 8pt post was not found or read. The Spec.fm page shows no author name in its text, so the author is **not verified**.
- No controlled study shows 8 px grids improve usability. The case rests on practice and consistency.

## Relationship rules: internal ≤ external, proximity, spacing instead of lines, spacing that grows with hierarchy

### Takeaway
All the design systems and NN/g state the same proximity rule: space inside a group must be smaller than space between groups, more space means less related, and more space around an element marks higher importance. Spacing (or background change) should replace dividers where possible.

### Cited Findings
- NN/g: "Items close together are likely to be perceived as part of the same group." "Proximity is one of the most important grouping principles and can overpower competing visual cues such as similarity of color or shape." "Using varying amounts of whitespace to either unite or separate elements is key to communicating meaningful groupings." — [NN/g, Proximity Principle in Visual Design](https://www.nngroup.com/articles/gestalt-proximity/)
- NN/g forms: "Place the label closer to the associated text field than to other text fields." — [NN/g, Form Design: White Space](https://www.nngroup.com/articles/form-design-white-space/)
- Carbon: "As more space is added between elements, their perceived relationship weakens." "Space can also be used to denote groups of associated information… without having to use lines or other graphical elements as a divider." "Elements that have more spacing around them tend to be perceived as higher in importance… as the headers descend in importance they receive less space." "Sections of a UI are allowed to be dense, but the whole page should not be crowded." — [Carbon Spacing](https://carbondesignsystem.com/elements/spacing/overview/)
- Fluent says nearly the same: "spacing creates logical sections of content on a page without having to use lines or other graphical elements as a divider." "UI elements that have more spacing around them draw more focus." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- Atlassian: "place more related objects closer together, and less related objects further apart… varying the amount of whitespace around an element can be used to" show hierarchy. — [Atlassian Spacing](https://atlassian.design/foundations/spacing)
- Spectrum: "Consistent proximity within a group signals that all members are equally related." — [Spectrum Spacing](https://spectrum.adobe.com/page/spacing/)
- Steve Schoger / Refactoring UI, "Use fewer borders": "using too many of them can make your design feel busy and cluttered… Use a box shadow… Use two different background colors… Add extra spacing… Spacing things further apart is a great way to create distinction between groups of elements without introducing any new UI at all." — [7 Practical Tips for Cheating at Design (Medium, Feb 2018, free)](https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886) (read from the free feed medium.com/feed/refactoring-ui); the same tactic is on [refactoringui.com](https://www.refactoringui.com/)
- The paywalled Refactoring UI book's chapter titles (visible free on the sales page): "Start with too much white space", "Establish a spacing and sizing system", "Grids are overrated", "Avoid ambiguous spacing". — [refactoringui.com](https://www.refactoringui.com/) (chapter content not readable; titles only)
- Every Layout, The Stack: "margin is really a property of the relationship between two proximate elements." Style the parent, not the child: `.stack > * + *` (the "owl") sets `margin-block-start` only between siblings. A stray last-child margin "combines with the parent's padding to produce double the intended space." — [Every Layout, The Stack](https://every-layout.dev/layouts/stack/)
- Carbon Stack: lets "components to not use margin and instead delegate the responsibility of positioning and layout to parent components." — [Carbon Spacing](https://carbondesignsystem.com/elements/spacing/overview/)
- Every Layout, modular scale: base white space on line-height ("font-size of 1rem, and a line-height of 1.5 creates a default value of 1.5rem. A harmoniously larger space might be 3rem"). — [Every Layout, Modular scale](https://every-layout.dev/rudiments/modular-scale/)
- Carbon 2x Grid: "The margin around each grid box matches its padding, for a total gutter of 32 pixels." — [Carbon 2x Grid](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Atlassian's 2026 tokens keep "gap" (between elements) and "inset" (surface padding) as separate token families. — [@atlaskit/tokens](https://unpkg.com/@atlaskit/tokens@20.15.0/dist/esm/artifacts/tokens-raw/atlassian-spacing.js)

### Inferences
- The "internal ≤ external" rule follows from proximity: padding inside a card must not exceed the gap between that card and its neighbours, or the card's content reads as belonging to the neighbour. Carbon's 2x Grid sets them **equal** (16 padding + 16 margin), which is the limit case.
- For DashLens, a hierarchy ladder could be: inside a control 4–8 → between related controls 8 → card/drawer padding 12–16 → between cards or sections 16–24 → between app regions 0 (shared 1px edge) or 8. Each level should step up at least one token, never down.
- Use `gap` on flex/grid parents (Stack pattern) instead of child margins. That removes most of the 49 padding/margin variants.

### Gaps
- No primary source using the exact phrase "internal ≤ external rule" was found. It is commonly attributed to Gestalt / design-community posts. Here it is stated as an inference from the proximity sources above.
- Rauno Freiberg's "Invisible Details of Interaction Design" (rauno.me) covers interaction, not spacing scales. No spacing rule was found there.

## Density in pro desktop tools: compact vs comfortable, and pairing with 12–14 px text and 24–32 px controls

### Takeaway
Systems handle density by keeping one spacing scale and changing **control height and inner padding**: Primer condensed/normal/spacious, Spectrum desktop/mobile component heights, Radix global scaling at 90–110%. Desktop defaults are 32 px controls with 12 px side padding and 8 px gaps. Dense lists and tables drop to 24–28 px rows with 4–8 px padding.

### Cited Findings
- Primer control heights 24 / 28 / 32 / 40 / 48 px with inline padding condensed 8, normal 12, spacious 16 (xsmall 4/8/12), and stack gap condensed 8 / normal 16 / spacious 24. — [@primer/primitives size.css](https://unpkg.com/@primer/primitives@11.10.0/dist/css/functional/size/size.css)
- Spectrum desktop component heights 20 / 24 / 32 / 40 / 48 vs mobile 26 / 30 / 40 / 50 / 60. Edge-to-text 12 (desktop) vs 15 (mobile) at size 100, 9 vs 11 at size 75. Text-to-icon 6 vs 8. — [@adobe/spectrum-tokens layout.json](https://unpkg.com/@adobe/spectrum-tokens@15.9.1/src/layout.json)
- Carbon control sizes 24 / 32 / 40 / 48 / 64 (`$size-xs`…`xl`). — [@carbon/layout _size.scss](https://unpkg.com/@carbon/layout@11.63.0/scss/generated/_size.scss)
- Radix: one `--scaling` factor (90%–110%) multiplies spacing, font size and line height together "to scale the UI density uniformly". — [Radix Themes Spacing](https://www.radix-ui.com/themes/docs/theme/spacing)
- Polaris table cell padding = 6 px (`--p-space-table-cell-padding: var(--p-space-150)`), card padding 16. — [@shopify/polaris-tokens styles.css](https://unpkg.com/@shopify/polaris-tokens@9.4.2/dist/css/styles.css)
- Atlassian: 0–8 px for "table cells", "icon buttons", "badges". — [Atlassian Spacing](https://atlassian.design/foundations/spacing)
- Atlassian states its spacing system "lays a foundation for responsive design and customisable UI density in the future." — [Atlassian Spacing](https://atlassian.design/foundations/spacing)

### Inferences
- DashLens pairing (desktop): 12px text → 24px controls (4px block, 8px inline padding, 4px icon gap). 13–14px text → 28–32px controls (6px block, 12px inline, 8px gap), as in Primer small/medium and Spectrum desktop 100. Timeline lanes and event rows sit at 24–28 px, toolbar buttons at 32 px.
- If DashLens wants a density switch, follow Radix/Primer: change control height and inline padding (condensed 8 / normal 12), not the scale itself.

### Gaps
- Fluent 2 "compact" sizing was not checked (the Fluent web page lists only the spacing ramp). Carbon "productive vs expressive" type sets were not read (see section 1). Both are **not verified**.

## Layout on wide landscape screens: text widths, panels, gutters, breakpoints, 200 % zoom and Reflow

### Takeaway
Design-system breakpoints near DashLens's range cluster at ~1024–1056, 1280–1366, 1400–1584 and 1920. Text inside drawers/dialogs should be capped at 45–75 characters (WCAG AAA: ≤ 80). WCAG 1.4.10 Reflow is tested at 320 CSS px (= 1280 px at 400 %), but video, maps, data tables and toolbars "necessary to keep in view" are explicitly exempt as two-dimensional content.

### Cited Findings
- Line length: "The Elements Of Typographic Style considers any value between 45 and 75 reasonable"; Every Layout's axiom is "the measure should never exceed 60ch". Enforcing a fixed width would cause "horizontal scrolling and broken zoom". — [Every Layout, Axioms](https://every-layout.dev/rudiments/axioms/)
- WCAG 1.4.8 (AAA): "Width is no more than 80 characters or glyphs (40 if CJK)." — [Understanding SC 1.4.8 Visual Presentation](https://www.w3.org/WAI/WCAG22/Understanding/visual-presentation.html)
- Primer overlay widths 192 / 320 / 480 / 640 / 960 px (a dialog/drawer size ladder). — [@primer/primitives size.css](https://unpkg.com/@primer/primitives@11.10.0/dist/css/functional/size/size.css)
- Breakpoints:
  - Carbon: sm 320, md 672, lg 1056, xlg 1312, max 1584; columns 4/8/16/16/16; margins 0/16/16/16/24. Padding is 16 px at all breakpoints. — [@carbon/layout src/index.ts](https://unpkg.com/@carbon/layout@11.63.0/src/index.ts); [Carbon 2x Grid](https://carbondesignsystem.com/elements/2x-grid/overview/)
  - Fluent 2: small 320–479, medium 480–639, large 640–1023, x-large 1024–1365, xx-large 1366–1919, xxx-large 1920+. — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
  - Primer: xsmall 320, small 544, medium 768, large 1012, xlarge 1280, xxlarge 1400. "The content area on an xlarge breakpoint will have a max-width of 1280px… includes the 24px padding." — [@primer/primitives breakpoints.css](https://unpkg.com/@primer/primitives@11.10.0/dist/css/functional/size/breakpoints.css); [Primer Layout](https://primer.style/product/getting-started/foundations/layout/)
  - Polaris: xs 0, sm 490, md 768, lg 1040, xl 1440. — [@shopify/polaris-tokens](https://unpkg.com/@shopify/polaris-tokens@9.4.2/dist/css/styles.css)
  - Tailwind: 640 / 768 / 1024 / 1280 / 1536. — [tailwindcss theme.css](https://unpkg.com/tailwindcss@4.3.5/theme.css)
- Fluid vs fixed: "Fluid column structures are ideal for editorial content, dashboards, images, video, data visualizations… scaling the size of things is more useful to the user than scaling the number of visible things." "If a user's goal is to see more items, scale column count by tiling fixed boxes." Hybrid boxes: "When a user would resize the browser expecting content to scale in one dimension but not the other." — [Carbon 2x Grid](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Panels: "All vertical panels expand to fill the full height of the browser window." Fixed panels "maintain a static width… exist outside of the responsive grid". Floating panels "conceal any UI elements below them and must be dismissible". — [Carbon 2x Grid, grid influencers](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Primer split page: the pane gets "an independent scrollable area"; "Don't use right-aligned flushed panes as their scrollbar may conflict with the page scrollbar." — [Primer Layout](https://primer.style/product/getting-started/foundations/layout/)
- Fluent: "Gutters are the negative space between columns and their width should be a multiple of the base unit… gutter widths can change at different breakpoints." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- Apple: "Don't change your app's functionality based on the space it occupies. However, you can change the amount of functionality that's visible onscreen." For macOS: "Avoid placing controls or critical information at the bottom of a window. People often move windows so that the bottom edge is below the bottom of the screen." — [Apple HIG Layout](https://developer.apple.com/design/human-interface-guidelines/layout)
- Vercel: "Responsive coverage. Verify on mobile, laptop, & ultra-wide. For ultra-wide, zoom out to 50% to simulate." "Respect zoom. Never disable browser zoom." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- WCAG 1.4.10 Reflow: "Vertical scrolling content at a width equivalent to 320 CSS pixels… Except for parts of the content which require two-dimensional layout." "320 CSS pixels is equivalent to a starting viewport width of 1280 CSS pixels wide at 400% zoom." Exempt examples: "maps and diagrams), video, games, presentations, data tables (not individual cells), and interfaces where it is necessary to keep toolbars in view while manipulating content." Cells inside exempt regions must still reflow. — [Understanding SC 1.4.10 Reflow](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html)
- WCAG 1.4.4: "text can be resized without assistive technology up to 200 percent without loss of content or functionality." — [Understanding SC 1.4.4 Resize Text](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html)

### Inferences
- At 200 % browser zoom a 1280 px laptop has a 640 CSS px viewport, and 1920 becomes 960. So DashLens's "desktop only" layout must still work at 640–960 CSS px. In practice: the side column collapses under or becomes a drawer below ~1024 CSS px, video tiles go 2×2 → 1 column, and drawers cap at min(480px, 100%).
- At 400 % (320 CSS px), the video, map, G-sensor chart and timeline canvas fall under the two-dimensional exception. Drawer and dialog text, event lists, settings and the incident card do not, and must reflow to a single column without horizontal scroll.
- Suggested DashLens breakpoints match the shared cluster: ~1024 (compact: side column becomes drawer), 1280 (default), 1440–1600 (wide: side column widens), 1920+ (extra-wide: let the video area grow, cap text at 60–75ch, don't stretch drawers).
- Drawer widths could follow Primer's ladder: 320 (events) and 480 (settings). Dialogs at 480 / 640. Text blocks capped at `max-width: 65ch`.

### Gaps
- No design system gives specific 2560 px guidance. Carbon's "max" breakpoint (1584) and Fluent's "1920 and up" are the widest found.

## Alignment: baseline and optical alignment, aligning to a grid, "draw each border once"

### Takeaway
The sources agree: every element should align to something on purpose (grid, edge, baseline or optical centre). Nudge ±1 px where optics beat geometry. Text aligns to the padding edge, icons are centred and text left-aligned. A strict baseline grid is advised against for browser UIs.

### Cited Findings
- Vercel: "Optical alignment. Adjust ±1px when perception beats geometry." "Deliberate alignment. Every element aligns with something intentionally whether to a grid, baseline, edge, or optical center. No accidental positioning." "Nested radii. Child radius ≤ parent radius & concentric so curves align." "Crisp borders. Combine borders & shadows; semi-transparent borders improve edge clarity." — [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- Carbon: "Always align type to the edge of box padding." "Ensure the overall layout has visible key lines: vertical and horizontal lines on which multiple objects align." "Horizontal and vertical alignment are equally critical." — [Carbon 2x Grid](https://carbondesignsystem.com/elements/2x-grid/overview/)
- Fluent: "align objects centrally and to align text left." Baseline grids "establish a vertical rhythm… especially useful with content that spans multiple columns." — [Fluent 2 Layout](https://fluent2.microsoft.design/layout)
- Apple: "Align elements to make them easier to scan, and use indentation to convey hierarchy… People assume that aligned items are related to each other, and conversely, they perceive indented items as subordinate." — [Apple HIG Layout](https://developer.apple.com/design/human-interface-guidelines/layout)
- Spec.fm: "Every UI element you create should be aligned to the pixel grid… Text is somewhat of an outlier." It uses a 4pt baseline grid. — [Spec.fm 8-Point Grid](https://spec.fm/specifics/8-pt-grid)
- Dahl: measuring by baseline on the web "will become difficult to maintain… I would not recommend it for large design systems". — [8-Point Grid: Vertical Rhythm](https://medium.com/built-to-adapt/8-point-grid-vertical-rhythm-90d05ad95032)
- Borders: Dahl's rule is that 1px borders sit outside the 8px padding ([Borders And Layouts](https://medium.com/built-to-adapt/8-point-grid-borders-and-layouts-e91eb97f5091)). Schoger: "Use fewer borders" and use spacing or background change instead ([7 Practical Tips](https://medium.com/refactoring-ui/7-practical-tips-for-cheating-at-design-40c736799886)).

### Inferences
- For DashLens: align all region edges and drawer and card padding to one 4 px grid with 8 px key lines. Align text to the padding edge. Centre icons in their 16/20 px box. Use line-height steps of 4 instead of a baseline grid.
- "Draw each border once" for adjacent panels (top bar / video / side column / timeline): give each shared edge to one owner (for example only `border-top` on the lower panel), or use a `gap: 1px` grid over a border-coloured background. This avoids 2 px double lines. This is a common CSS practice, inferred from the "fewer borders" sources. No primary source was found that states it.

### Gaps
- No primary free source using the phrase "draw each border once" was found. It is **not verified** as a quote from any named author.
- Material 3's optical alignment / keyline guidance could not be read (JavaScript-only pages).
