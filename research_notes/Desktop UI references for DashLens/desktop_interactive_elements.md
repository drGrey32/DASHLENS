# Desktop interactive-element guidelines for DashLens (mouse, trackpad, keyboard)

> **How these notes were made, and their limits (read first).**
> Page fetches were blocked in this session: `www.w3.org`, `learn.microsoft.com`, `carbondesignsystem.com`,
> `primer.style` and `spectrum.adobe.com` all failed with "host not allowed" (DNS ENOTFOUND). These hosts have to be
> added to the session's allowed network hosts before anyone can fetch the pages directly. Everything marked
> **[search-verified]** comes from web-search results and their snippets. It was **not** checked against the full page
> text, so the wording may be paraphrased rather than an exact quote. Items marked **[UNVERIFIED, prior knowledge]**
> appear only in the Gaps sections. Each one names the URL to check before DashLens relies on it.
> Date of research: 2026-11-26.

## 1. Pointer target sizes on desktop (WCAG 2.5.8, 2.5.5, Fitts's law)

### Takeaway
On desktop, the binding AA rule is WCAG 2.2 SC 2.5.8: every pointer target must be at least 24 x 24 CSS px, or an undersized target must pass the 24 px circle spacing test. The 44 x 44 px figure is the AAA criterion 2.5.5 and is a touch-oriented goal, not a desktop minimum. DashLens's 26, 30 and 36 px controls already pass. Its 80 x 16 px volume slider is under 24 px tall, so it passes only through the spacing exception or a larger invisible hit area.

### Cited Findings
- [search-verified] SC 2.5.8 (AA) requires pointer targets of at least 24 by 24 CSS px. Sufficient spacing is the alternative. — [W3C Understanding 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
- [search-verified] Spacing exception: an undersized target passes if a 24 px diameter circle centered on its bounding box does not intersect another target or another undersized target's circle. The criterion also has exceptions for inline targets in a sentence or block of text and for essential presentation. — [W3C Understanding 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html); text reproduced in [Smashing Magazine, 2024-07](https://smashingmagazine.com/2024/07/getting-bottom-minimum-wcag-conformant-interactive-element-size/)
- [search-verified] Worked example: a 16 x 16 icon with 4 px of padding becomes a 24 x 24 bounding box, which satisfies SC 2.5.8. — [Smashing Magazine, 2024-07](https://smashingmagazine.com/2024/07/getting-bottom-minimum-wcag-conformant-interactive-element-size/)
- [search-verified] The 44 x 44 CSS px figure belongs to the stricter AAA criterion 2.5.5 (Target Size, Enhanced). Earlier 2.2 drafts ("Pointer Target Spacing") used 44 px, but the published 2.5.8 uses 24 px. — [W3C editor's draft, archived "Pointer Target Spacing"](https://w3c.github.io/wcag/understanding/pointer-target-spacing); [Adrian Roselli, Target Size and 2.5.5](http://adrianroselli.com/2019/06/target-size-and-2-5-5.html)
- [search-verified] axe-core implements the rule as "All touch targets must be 24px large, or leave sufficient space". It runs automatically, so DashLens can test this in CI. — [Deque axe rule target-size](https://dequeuniversity.com/rules/axe/4.8/target-size)
- [search-verified] Primer's documentation says its **small** buttons may fall below the 24 x 24 CSS px minimum target size, while medium and large meet it. A major design system therefore treats sub-24 px controls as an accessibility exception, not a default. — [Primer Button](https://primer.style/design/components/button)

### Inferences
- For DashLens, the practical floor is 24 x 24 CSS px of **hit area** per control. The visible control can be smaller, such as a 16 px icon or a thin slider track, as long as its padding or a transparent pseudo-element brings the hit box to 24 px.
- WCAG measures in CSS px, so 200 % browser zoom doubles physical size and helps. Zoom does not change conformance, which is judged at the default zoom level.
- 44 px is not a desktop requirement. Adopting it everywhere would cost density without a matching gain for mouse users.

### Gaps
- Exact normative wording of 2.5.8 could not be fetched. [UNVERIFIED, prior knowledge] The SC text reads: "The size of the target for pointer inputs is at least 24 by 24 CSS pixels, except when: Spacing … Equivalent … Inline … User agent control … Essential". Verify at https://www.w3.org/TR/WCAG22/#target-size-minimum.
- I found no free primary Fitts's law source in the search budget. [UNVERIFIED, prior knowledge] NN/g's free article "Fitts's Law and Its Applications in UX" (https://www.nngroup.com/articles/fitts-law/) says time to acquire a target grows with distance and shrinks with target size. It also says screen edges and corners act as targets of effectively infinite size. Verify before quoting.

## 2. Control heights in desktop design systems (exact numbers)

### Takeaway
Desktop systems cluster on a **32 px default** control, with 24 px (compact or extra small) and 40 px (large or touch) on either side. Carbon is 24/32/40/48, Spectrum's desktop (medium) scale is 32 px with the touch (large) scale at 40 px, and Windows/WinUI density is Standard 40 and Compact 32 epx layout targets. Fluent 2 web is reported as 32 normal and 24 compact.

### Cited Findings
- **IBM Carbon (current docs)** [search-verified]: seven button sizes: extra small, small, medium, large (productive), large (expressive), extra large and 2XL. "Small" is for buttons next to 32 px inputs, and "medium" is for buttons next to 40 px inputs. Large (productive) is the most common size in software products. Large (expressive) pairs with 16 px body copy. — [Carbon Button usage](https://carbondesignsystem.com/components/button/usage/)
- **Carbon heights** [search-verified]: extra small 24 px, small 32 px, medium 40 px, large 48 px. The size table on the style page lists XS 24, S 32 and both large sizes at 48. — [Carbon Button style](https://carbondesignsystem.com/components/button/style/)
- **Carbon v10 (older)** [search-verified]: Default 48 px, Large expressive 48 px (16 px type), Field 40 px (14 px type), Small 32 px (14 px type). Even the 32 px small button uses 14 px type. — [Carbon v10 Button style](https://v10.carbondesignsystem.com/components/button/style/)
- **Carbon form inputs** [search-verified]: default inputs come in small 32 px, medium 40 px and large 48 px. Fluid inputs are a single 64 px height. — [Carbon Form usage](https://carbondesignsystem.com/components/form/usage/)
- **Adobe Spectrum** [search-verified]: medium scale is the desktop default and large scale targets touch devices. `--spectrum-component-height-100` is **32 px in medium and 40 px in large**, and button heights are among the dimensions that change by scale. — [Spectrum Web Components: Styles](https://opensource.adobe.com/spectrum-web-components/tools/styles/); [spectrum-css wiki: T-shirt sizing](https://github.com/adobe/spectrum-css/wiki/How-to:-T-shirt-sizing-in-Spectrum-CSS)
- **Windows / WinUI** [search-verified]: Standard sizing aligns items to a **40 x 40 epx** target and Compact sizing to a **32 x 32 epx** target. These are layout targets, not literal control heights. — [Microsoft "Spacing and Sizes" (staging mirror of learn.microsoft.com)](https://docstaging.z5.web.core.windows.net/aleader/reunion/design/style/spacing.html)
- **WinUI TableView** [search-verified]: a microsoft-ui-xaml pull request raises Compact row/header minimum height to 32 (from 30), keeping Standard 40 and Comfortable 48. — [microsoft-ui-xaml PR #12587](https://github.com/microsoft/microsoft-ui-xaml/pull/12587)
- **Fluent 2 (web)** [search-verified, secondary only]: a GitHub issue in an unofficial Fluent port cites "Fluent 2 metrics" of 32 px normal and 24 px compact button heights. It also notes a bug where heights drift (28 vs 30) between appearances, a reminder to keep one height per size. — [fluent-gpui issue #81](https://github.com/thedancingdeveloper/fluent-gpui/issues/81) (not an official Microsoft source)
- **Primer** [search-verified]: medium is the default and fits most interfaces. Small suits compact spaces and less important actions. Large is for emphasis and should be used sparingly. — [Primer Button](https://primer.style/design/components/button)
- **macOS** [search-verified, secondary/legacy]: legacy Apple HIG (Leopard era) defines regular, small and mini sizes for many controls, with fixed height per size and free length. — [Apple HIG: Controls (legacy mirror)](https://leopard-adc.pepas.com/documentation/UserExperience/Conceptual/AppleHIGuidelines/XHIGControls/XHIGControls.html). A third-party layout guide lists 32 pt bottom bars for regular controls and 22 pt bars for small/mini controls. — [Mario Aguzman, Layout Guidelines](https://marioaguzman.github.io/design/layoutguidelines/). A third-party summary gives macOS 28 x 28 pt default and 20 x 20 pt minimum hit size. — [ehmo platform-design-skills macOS](https://github.com/ehmo/platform-design-skills/blob/main/skills/macos/SKILL.md) (secondary; not Apple)

### Inferences
- A 32 px default fits a pro desktop tool: it is Spectrum's desktop size, Carbon's "small" and Primer's default. Use 24 px for dense toolbars and table rows and 40 px only for rare primary or empty-state actions.
- DashLens's 26/30/36 px set is close to the industry grid but off it. Moving to **24 / 32 (/ 40)** would match Carbon, Spectrum and Fluent 2 tokens and make the sizes easier to reason about.

### Gaps
- Primer exact heights could not be verified. [UNVERIFIED, prior knowledge] Primer control sizes are xsmall 24, small 28, medium 32, large 40 and xlarge 48 px. Check https://primer.style/product/components/button/ or `@primer/primitives` size tokens.
- Fluent 2 web exact button heights could not be fetched. [UNVERIFIED, prior knowledge] Small 24, medium 32 and large 40 px. Check https://fluent2.microsoft.design/components/web/react/core/button/usage.
- Current Apple HIG table could not be fetched. [UNVERIFIED, prior knowledge] Current macOS HIG lists mini, small, regular and large control sizes, with an extra-large size added for macOS 26. Exact point heights are not reliably stated on the free HIG pages. Check https://developer.apple.com/design/human-interface-guidelines/buttons.
- Spectrum per-size button heights could not be fetched. [UNVERIFIED, prior knowledge] Desktop S 24, M 32, L 40 and XL 48. Large (touch) scale is about 1.25x. Check https://spectrum.adobe.com/page/button/.
- No data was retrieved for GNOME HIG, Atlassian or Shopify Polaris in the tool budget.

## 3. How many control heights, and how to pair height with font and icon size

### Takeaway
Systems ship 3 to 4 heights, with one default carrying most of the UI. Desktop pairings are consistent: 14 px text and 16 px icons sit in 32 px controls, and 12 px text with 16 px icons fits the 24 px tier.

### Cited Findings
- [search-verified] Carbon pairs 14 px type with both its 32 px (Small) and 40 px (Field) buttons, and 16 px type with the 48 px expressive button. — [Carbon v10 Button style](https://v10.carbondesignsystem.com/components/button/style/)
- [search-verified] Carbon ties button size to the adjacent input height: small buttons go beside 32 px inputs and medium beside 40 px inputs. — [Carbon Button usage](https://carbondesignsystem.com/components/button/usage/)
- [search-verified] Primer names one default (medium) for most interfaces and uses small and large sparingly. — [Primer Button](https://primer.style/design/components/button)
- [search-verified] A height mismatch between button appearances (28 vs 30 px) is logged as a bug against Fluent metrics, so systems treat "one height per size tier" as a rule. — [fluent-gpui issue #81](https://github.com/thedancingdeveloper/fluent-gpui/issues/81)

### Inferences
- Recommendation for DashLens: three heights. 24 px for compact toolbar, icon and table-row controls (12 to 13 px text, 16 px icon). 32 px as the default for buttons, selects and inputs (13 to 14 px text, 16 px icon). 40 px only for a few primary or empty-state actions (14 px text, 16 to 20 px icon).
- Put controls in the same row at the same height. A button beside an input should match the input's height, as Carbon specifies.

### Gaps
- No primary source in budget gave an explicit "use at most N heights" rule. The 3 to 4 figure is inferred from the size lists above.

## 4. Sliders, scrubbers and thin controls

### Takeaway
The pattern across systems is a thin visible track (4 to 8 px) with a larger thumb (12 to 20 px) and an **invisible hit area of at least 24 px on fine pointers**. Video scrubbers use the same idea: a thin bar inside a taller hover zone that grows on hover.

### Cited Findings
- [search-verified] An open-source design system fix keeps a 20 px visible thumb but adds an invisible pseudo-element hit area. The hit area is 24 x 24 px for `pointer: fine` and 44 x 44 px under `@media (pointer: coarse)`. For range sliders, each thumb's hit area stops at the midpoint so the nearest thumb is grabbed. — [common-origin design system PR #243](https://github.com/common-origin/common-origin-design-system/pull/243); [issue #231 "Slider thumb is under the 24px target size"](https://github.com/common-origin/common-origin-design-system/issues/231)
- [search-verified] A proposed tiered slider spec: sm track 4 px with 12 px thumb, md track 8 px with 16 px thumb, lg track 12 px with 20 px thumb. The thumb is always larger than the track. — [ora-ui issue #342](https://github.com/ora-ui/ora-ui/issues/342) (community proposal, not a major system)
- [search-verified] Another library proposes a compact slider with a 6 px control/track and a 16 px thumb. — [codeatlasdev/ui issue #704](https://github.com/codeatlasdev/ui/issues/704) (community)
- [search-verified] Material 2 sliders: active track 6 dp, inactive track 4 dp, thumb radius about 10 dp (the search snippet said "20dp", possibly meaning diameter; unresolved). — [Material 2 Sliders](https://m2.material.io/components/sliders)
- [search-verified] Smashing's slider UX article treats the visible thumb and the actual target as separate: the target should be larger than the drawn thumb. — [Smashing Magazine, Designing The Perfect Slider UX](https://www.smashingmagazine.com/2017/07/designing-perfect-slider/)

### Inferences
- DashLens volume slider (80 x 16 px): keep the drawn track at 4 px and the thumb at 12 to 14 px. Grow the element's hit box to at least 24 px tall with padding or a transparent `::before`. This passes 2.5.8 without the spacing exception.
- Timeline/scrubber canvas: use a hit zone of at least 24 px tall around the playhead and track, even if the drawn progress line is 3 to 4 px. Thicken the drawn line and show a scrub-preview time on hover. Make the playhead handle at least 12 px wide visually with a 24 px hit width.

### Gaps
- Fluent 2, Carbon, Spectrum and macOS slider token values could not be retrieved (fetch blocked; search returned nothing specific). [UNVERIFIED, prior knowledge] Fluent 2 medium slider: thumb 20 px, rail 4 px. Spectrum slider: track 2 px, handle 16 px. Check https://fluent2.microsoft.design/components/web/react/core/slider/usage and https://spectrum.adobe.com/page/slider/.
- YouTube, Vimeo and Frame.io scrubber hit zones are not documented publicly. [UNVERIFIED, observation] The YouTube progress bar is about 3 px and grows to about 5 px on hover inside a taller hover strip. It would need measuring in DevTools.

## 5. Hover, focus, active, selected and disabled states; tooltips; cursors

### Takeaway
At AA, the focus indicator must be visible (2.4.7) and the focused item must not be completely hidden by sticky UI (2.4.11). The AAA rule 2.4.13 gives a concrete target worth adopting anyway: an indicator at least the area of a 2 CSS px perimeter with at least 3:1 change between states. Tooltips must be dismissible (Esc), hoverable and persistent (1.4.13). A ~300 ms hover delay is a common default, with no delay on keyboard focus.

### Cited Findings
- [search-verified] **2.4.11 Focus Not Obscured (Minimum), AA**: the focused component may be partly covered and still pass. Only being completely hidden by author content fails. If the indicator is fully obscured, it would likely also fail 2.4.7. — [W3C Understanding 2.4.11](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured.html)
- [search-verified] **2.4.13 Focus Appearance, AAA**: the focus indicator must be at least as large as the area of a 2 CSS px thick perimeter of the unfocused component, with at least 3:1 contrast **between focused and unfocused states**. This is a change of contrast, not a flat 3:1 against the background. Meeting 1.4.11 does not automatically satisfy 2.4.13. — [Deque WCAG 2.2 updates](https://dequeuniversity.com/resources/wcag-2.2/); [Level Access, Focus indicators](https://www.levelaccess.com/blog/focus-indicators-wcag-requirements-and-best-practices/)
- [search-verified] **1.4.13 Content on Hover or Focus, AA**: dismissible (a mechanism to dismiss without moving pointer hover or keyboard focus, such as Esc), hoverable (the pointer can move onto the content without it vanishing) and persistent (it stays until dismissed, hover/focus is removed, or it is no longer valid). — [W3C Understanding 1.4.13](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html)
- [search-verified] Tooltip hover delay: PatternFly defaults to a **300 ms** entry delay and allows 0 ms for icon tooltips. — [PatternFly Tooltip guidelines](https://www.patternfly.org/components/tooltip/design-guidelines/). ServiceNow Horizon also defaults to 300 ms. — [Horizon now-tooltip](https://horizon.servicenow.com/workspace/components/now-tooltip)
- [search-verified] Once one tooltip is open, the next should open with no delay as the pointer moves along a toolbar (the "warm-up then skip" pattern). — [master.dev, Tooltips need a delay, and then they need to skip it](https://blog.master.dev/tooltips-need-a-delay-and-then-they-need-to-skip-it/)
- [search-verified] Show tooltips on keyboard focus as well as hover, without a delay, because keyboard users do not "mouse past" targets. A hide delay of about 100 to 200 ms after the pointer leaves is suggested. — [uxpickle, Tooltip delay](https://uxpickle.com/delay-before-the-tooltip-shows-up/) (secondary blog)
- [search-verified] GitLab's design system has an issue to add a default tooltip hover delay when none is specified. — [GitLab design.gitlab.com issue #235](https://gitlab.com/gitlab-org/gitlab-services/design.gitlab.com/issues/235)

### Inferences
- DashLens focus ring: use `:focus-visible` with a 2 px solid outline, offset 2 px, in a colour with at least 3:1 against both the control and the dark background. This meets 2.4.13 (AAA), not just 2.4.7. Make sure drawers and the sticky timeline never fully cover a focused control, or call `scrollIntoView`.
- Tooltips: 300 to 500 ms show delay on hover, 0 ms on focus, skip the delay while moving between toolbar buttons, close on Esc, and keep them open while hovered. Never put essential information only in a tooltip.

### Gaps
- No free primary source in budget for cursor conventions (pointer vs default on buttons, `grab`/`grabbing` for drag handles, `ew-resize`/`col-resize` for splitters), context menus or double-click. [UNVERIFIED, prior knowledge] Native desktop convention (macOS and Windows) keeps the arrow cursor on buttons and reserves the hand cursor for links. Many web design systems use `pointer` on all clickables. Decide one rule and apply it everywhere.
- 2.4.7 exact text not fetched. [UNVERIFIED, prior knowledge] "Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible." Verify at https://www.w3.org/TR/WCAG22/#focus-visible.
- No NN/g tooltip article was returned by search.

## 6. Keyboard-first desktop patterns

### Takeaway
Group toolbar buttons as one Tab stop with a roving tabindex and arrow-key movement (APG toolbar). Tab moves between groups, and focus returns to the last-used item.

### Cited Findings
- [search-verified] APG Toolbar pattern: in horizontal toolbars, Left and Right Arrow move between controls. In vertical toolbars, Up and Down Arrow do. Left and Right can be left free for controls such as a horizontal slider inside the toolbar. In multi-row toolbars, Left and Right may wrap between rows. — [WAI-ARIA APG Toolbar Pattern](https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/)
- [search-verified] The APG toolbar example: the toolbar container itself is not focusable because it uses a roving tabindex. Focus returns to the control that last had focus when Tab re-enters the toolbar. — [APG Toolbar Example](https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/examples/toolbar/)
- [search-verified] Roving tabindex mechanics: the first item gets `tabindex="0"` and all others `tabindex="-1"`. On move, the new item takes `0`, the old one gets `-1`, and `element.focus()` is called. — [MDN ARIA toolbar role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/toolbar_role)

### Inferences
- DashLens's playback bar fits the APG toolbar pattern well (`role="toolbar"`, `aria-label`, roving tabindex). The volume slider inside it should keep Left and Right for itself, and the APG explicitly allows this.
- Show the shortcut in each tooltip and menu item (for example "Play/Pause  Space"). If a command palette is added, Ctrl+K or Ctrl+Shift+P are the common conventions [UNVERIFIED].

### Gaps
- Home/End behaviour in toolbars and `aria-keyshortcuts` guidance were not returned by search. [UNVERIFIED, prior knowledge] The APG lists Home/End as optional for moving to the first/last toolbar item, and `aria-keyshortcuts` exposes shortcuts to assistive technology. Verify at https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/ and https://www.w3.org/TR/wai-aria-1.2/#aria-keyshortcuts.
- No sources gathered on command palettes or on displaying shortcuts in tooltips.

## 7. Desktop density: compact vs comfortable, user-selectable density

### Takeaway
Enterprise desktop apps offer a user-selectable density with two (Salesforce) or three (Gmail, WinUI tables) levels. The default is the roomier one, and each user's choice persists.

### Cited Findings
- [search-verified] Salesforce Lightning has two settings, **Comfy** (default: labels above fields, more space) and **Compact** (labels beside fields, less spacing). Admins set an org default, but each user can choose their own and admins cannot override it. Changes don't apply to Classic, Experience Builder sites or the mobile app. — [Lightning Design System: Display Density](https://www.lightningdesignsystem.com/2e1ef8501/p/805bbe); [Salesforce Aura: Changing the Display Density](https://developer.salesforce.com/docs/platform/aura-platform/guide/data-service-display-density.html); [LWC: Change the Form Display Density](https://developer.salesforce.com/docs/platform/lwc/guide/data-display-density.html)
- [search-verified, secondary] Compact is said to fit about 30 % more information on screen. This comes from community blogs, not Salesforce. — [The Marks Group](https://www.marksgroup.net/blog/salesforce-lightning-density-settings/)
- [search-verified] WinUI TableView has three densities: Compact (min row 32), Standard 40 and Comfortable 48. — [microsoft-ui-xaml PR #12587](https://github.com/microsoft/microsoft-ui-xaml/pull/12587)
- [search-verified] Windows offers Standard (40 epx target) and Compact (32 epx target) sizing for apps. — [Microsoft Spacing and Sizes (staging mirror)](https://docstaging.z5.web.core.windows.net/aleader/reunion/design/style/spacing.html)
- [search-verified, weak] Gmail's Default / Comfortable / Compact density names are confirmed only through a third-party post that cites them. — [Zoho community](https://help.zoho.com/portal/en/community/topic/switch-display-density-from-default-to-comfortable-to-compact?page=44)

### Inferences
- DashLens is a review tool used for long sessions on large monitors, much like pro video tools, so a compact default (24 px toolbar controls, 32 px default controls) is reasonable. An optional "Comfortable" setting (32/40) helps laptop trackpad users and people who zoom. Store the choice per viewer in localStorage and switch it with one CSS custom-property set (`--ctl-h-sm`, `--ctl-h-md`).

### Gaps
- Carbon's density/grid guidance, Atlassian density, Gmail's own help page and pro-tool references (DaVinci Resolve, Premiere, Frame.io) were not retrieved in budget.
- [UNVERIFIED, prior knowledge] Carbon's data table offers row heights of xs 24, sm 32, md 40, lg 48 and xl 64 px. Check https://carbondesignsystem.com/components/data-table/style/.
