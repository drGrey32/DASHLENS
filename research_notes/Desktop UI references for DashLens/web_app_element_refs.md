# Desktop web app and design-system references for DashLens UI elements

Method note (read first): in this session the network allowlist blocked direct page fetches of carbondesignsystem.com, nngroup.com, linear.app and primer.style (DNS "ENOTFOUND" from WebFetch), and GitHub API access to design-system doc repos was not enabled. All findings below therefore come from web-search result excerpts that point to the cited URLs, not from reading the full pages. Treat every number as "seen in a search excerpt of that page"; anything marked **[unverified]** is from my own prior knowledge or a secondary source and must be checked before it goes into a spec. Hosts that would need allowing to verify: carbondesignsystem.com, nngroup.com, linear.app, primer.style, atlassian.design, design-system.service.gov.uk, fluent2.microsoft.design, vercel.com, code.visualstudio.com, grafana.com, maplibre.org, developer.apple.com, raycast.com.

## 1. Whole-app feel: calm, dense, keyboard-first desktop web apps

### Takeaway
Linear is the closest model for DashLens's "calm dark pro tool" feel: a dimmed sidebar so the work area dominates, reduced visual noise in headers/tabs/panels, and a theme generated from very few inputs (base, accent, contrast) in a perceptual colour space. Vercel Geist is the best model for small components (kbd, toast) with clear, short usage rules.

### Cited Findings
- Linear's 2024 redesign (part II) adjusted "the sidebar, tabs, headers, and panels to reduce visual noise, maintain visual alignment, and increase the hierarchy and density of navigation elements." — [Linear: How we redesigned the Linear UI (part II)](https://linear.app/now/how-we-redesigned-the-linear-ui); mirrored at [Karri Saarinen's blog](https://karrisaarinen.com/posts/how-we-redesigned-the-linear-ui/)
- Linear made the sidebar "a few notches dimmer, allowing the main content area—where users work—to take precedence." — [Linear: A calmer interface for a product in motion](https://linear.app/now/behind-the-latest-design-refresh)
- Linear moved theme generation to LCH instead of HSL because in LCH a red and a yellow at lightness 50 look roughly equally light. — [Karri Saarinen post](https://karrisaarinen.com/posts/how-we-redesigned-the-linear-ui/)
- Conflict on scope of LCH: Saarinen's post says custom themes still used an HSL-based generator and LCH was used for elevated/translucent surfaces; a later Linear post says themes are generated "from a few inputs, like base color, accent color, and contrast, from which we derive more than a hundred color variables in LCH space." — [Saarinen](https://karrisaarinen.com/posts/how-we-redesigned-the-linear-ui/) vs [Linear: calmer interface](https://linear.app/now/behind-the-latest-design-refresh)
- Linear's styling engineering move to StyleX is documented separately (not about visuals per se). — [Linear: Styling Linear for the future with StyleX](https://linear.app/now/styling-linear-for-the-future-stylex)
- Geist (Vercel) publishes per-component pages including Keyboard Input and Toast with short, opinionated rules (details in sections 5 and 8). — [Geist Keyboard Input](https://vercel.com/geist/keyboard-input); [Geist Toast](https://vercel.com/geist/toast); [Geist introduction](https://examples.vercel.com/geist/introduction)

### Inferences
- Borrow from Linear for DashLens: (a) drawers and top bar one step dimmer than the video stage, so footage "takes precedence"; (b) derive the whole dark palette from three tokens (base grey, the one orange accent, contrast) in OKLCH/LCH, which also makes a high-contrast variant cheap; (c) treat header/tab/panel chrome as a noise budget: fewer borders, alignment over boxes.
- Borrow from Geist: one-paragraph "use for / do not use for" rules per component, which suits DashLens's DESIGN.md.
- Avoid: copying Linear's translucent/blurred surfaces over video; blur over moving footage is costly and reduces legibility **[unverified inference]**.

### Gaps
- Raycast, Figma (properties panel density), Notion, Stripe Dashboard, Arc and Things 3 could not be researched with primary sources in this session. From prior knowledge **[unverified]**: Figma's right properties panel uses ~240px wide panels with 11px labels and compact 24–28px rows; Raycast settings use a left list + right form with label/description rows; Stripe Dashboard uses right-hand "drawer" detail panes. Verify at figma.com/blog, raycast.com/manual and docs.stripe.com before relying on these.

## 2. Settings pages and drawers (Settings drawer with sections)

### Takeaway
Use VS Code's settings editor ideas (search box at top, a "Commonly used" group first, a coloured left bar on changed settings, a "modified" filter) inside a Fluent-style inline (non-blocking) drawer so the video stays visible while settings change live.

### Cited Findings
- VS Code: "Modified settings are marked with a colored bar on the left of the setting, similar to modified lines in the editor." — [VS Code docs: User and workspace settings](https://code.visualstudio.com/docs/configure/settings)
- VS Code: a "Commonly Used" group sits at the top and shows popular customization settings; the settings editor has filters including `@modified` to show only changed settings. — [VS Code docs: settings](https://code.visualstudio.com/docs/configure/settings); secondary confirmation of "Show modified settings" in the filter menu: [DEV Community post](https://dev.to/starbist/my-favorite-vs-code-settings-1ll0)
- Fluent 2: inline drawers are passive surfaces beside the page, recommended "when people need to view and act on both the drawer and the main content at once"; overlay drawers block content and should be used "with caution". — [Fluent 2 Drawer usage](https://fluent2.microsoft.design/components/web/react/core/drawer/usage)
- Fluent 2 drawers come in small, medium, large and full widths, small default; full-width is discouraged when users need the main page. — [Fluent 2 Drawer usage](https://fluent2.microsoft.design/components/web/react/core/drawer/usage)
- Fluent 2 labels default to above the control, but may sit inline when layout allows; built-in-label components (switch, checkbox, radio) show disabled state on the label too. — [Fluent 2 Label usage](https://fluent2.microsoft.design/components/web/react/core/label/usage)

### Inferences
- DashLens Settings drawer row pattern: label (13px, primary) + one-line description (12px, secondary) on the left, control right-aligned; changed-from-default rows get a 2px orange left bar (VS Code), plus a "Reset" link appearing on hover/focus for that row.
- Put a search field at the top of the drawer once there are more than ~25 settings; filter rows live and show section headers only for sections with matches (VS Code behaviour) **[threshold unverified]**.
- Keep Settings as an inline/push drawer, not a modal overlay, because Playback/Cameras/Speed settings are judged by watching the video change (Fluent's "view and act on both").
- Avoid: macOS-style full-page settings with a separate window; avoid a full-width drawer.

### Gaps
- Exact Fluent drawer pixel widths (S/M/L) were not in excerpts. Prior knowledge **[unverified]**: 320 / 592 / 940 px.
- Linear and GitHub settings layouts, macOS System Settings and Carbon side panel guidance were not retrieved.

## 3. Dialogs, multi-step progress / export, success screens (Save evidence, Evidence saved, Problem report)

### Takeaway
Model "Save evidence" on Carbon's transactional/progress modal (Cancel + primary, first focus on primary when no inputs) and Primer's dialog footer rules (primary right-aligned, 16px safe area, 296px small size). The "Your evidence is saved" screen is closest to Carbon's acknowledgement (single button) modal.

### Cited Findings
- Carbon modal variants: Passive (info only, closes via X, click outside or Esc), Transactional (Cancel + primary), Danger (destructive), Acknowledgment (single button, commonly OK), Progress (several steps before it can close; Cancel, Previous, Next/completion buttons). — [Carbon Modal usage](https://carbondesignsystem.com/components/modal/usage); [Carbon v10 Modal usage](https://v10.carbondesignsystem.com/components/modal/usage/)
- Carbon modal sizes: xs, small, default (medium), large; short messages should use xs or small "to avoid long single lines"; complex content (e.g. data table) default or large; the large modal's max height is the ceiling before moving to a full page. — [Carbon Modal usage](https://carbondesignsystem.com/components/modal/usage); [Carbon Modal style](https://carbondesignsystem.com/components/modal/style/)
- Carbon: in a transactional modal without form inputs in the body, first focus goes to the primary button; buttons are flush right in a fluid button group footer. — [Carbon Modal usage](https://carbondesignsystem.com/components/modal/usage); [Carbon Modal style](https://carbondesignsystem.com/components/modal/style/)
- Primer: primary actions are aligned to the right of the footer, grouped with related actions; footer may hold confirmation actions, links or specialised actions. — [Primer Dialog guidelines](https://primer.style/product/components/dialog/guidelines)
- Primer: dialog sizes range small to xlarge, medium default; centred dialogs keep a 16px safe area to the viewport; footer buttons sit in the safe area. — [Primer Dialog (preview docs)](https://primer-docs-preview.github.com/product/components/dialog/guidelines) **[draft/preview domain]**
- Primer ConfirmationDialog small width: 296px. — [Primer ConfirmationDialog guidelines](https://primer.style/product/components/confirmation-dialog/guidelines)
- Other systems cap dialog buttons at two. — [Red Hat dialog guidelines](https://ux.redhat.com/elements/dialog/guidelines); [Washington Post dialog](https://build.washingtonpost.com/components/dialog)

### Inferences
- Save evidence: Carbon default/medium width; checkboxes (not switches, since nothing happens until "Save") in the body; footer = ghost "Cancel" + orange primary "Save evidence". When saving starts, swap the body for a progress state in the same dialog (determinate bar, current file name, "Cancel" stays), rather than opening a second modal.
- Evidence saved: acknowledgement pattern: one primary ("Done") plus at most one secondary ("Show in folder"/"Copy summary"); title states the outcome in plain words ("Your evidence is saved"), body lists what was saved and where.
- Problem report: transactional modal with first focus in the first field (Carbon focus rule applies only when no inputs).
- Avoid: three-plus footer buttons; closing a progress dialog on outside click (Carbon passive behaviour only suits passive dialogs); long single-line text in wide dialogs.

### Gaps
- Primer medium/large pixel widths and Carbon exact modal widths were not in excerpts. Figma export panel and HandBrake queue were not researched (HandBrake is video-domain anyway).

## 4. Lists with notes and pins (Events list)

### Takeaway
No primary source retrieved in this session. Patterns below are from prior knowledge and are all **[unverified]**.

### Cited Findings
- None retrieved (Linear issue lists, GitHub review comments, Figma comments panel and Google Docs comments were not reachable or not returned by search).

### Inferences
- **[unverified]** Linear lists: single-line rows (~36px), metadata right-aligned in fixed columns, keyboard J/K or arrow navigation with a visible focused row, actions on hover. Borrow: one-line event rows with the timestamp in a fixed-width tabular-numeral column on the left, type label next, note text truncating, actions (edit, delete) on row hover/focus.
- **[unverified]** Figma/Google Docs comments: clicking a comment jumps the canvas to its location; the active thread is highlighted in both list and canvas. Borrow: selecting an event seeks the video and highlights the timeline pin; the playing position highlights the nearest row.
- **[unverified]** GitHub review comments: inline edit replaces the text with a textarea plus "Cancel"/"Update comment" in place. Borrow inline edit in the row; Enter saves, Esc cancels.

### Gaps
- Need verification from linear.app/docs, docs.github.com, help.figma.com.

## 5. Toasts vs inline messages vs banners; on-screen error box; "Footage loaded" summary

### Takeaway
Use toasts only for brief, non-blocking confirmations of something the user just did (Geist, Carbon); errors and warnings must never auto-dismiss (Atlassian) and belong inline next to their cause or in a persistent box (GOV.UK error summary, Carbon inline). DashLens's existing move of errors out of toasts is consistent with all sources.

### Cited Findings
- Geist Toast: for non-blocking acknowledgments of user-initiated actions; field validation belongs on the input; default toasts auto-dismiss, `preserve` only when the user must read or act before it disappears; polite live region, assertive only for blocking errors. — [Geist Toast](https://vercel.com/geist/toast)
- Carbon v11: inline and toast notifications contain no interactive elements and do not take focus; an "actionable" variant exists for buttons; an actionable notification in toast styling stays until dismissed; use actionable with "View more" when a toast or inline text runs past two lines. — [Carbon Notification usage](https://carbondesignsystem.com/components/notification/usage/); [Carbon Notification accessibility](https://carbondesignsystem.com/components/notification/accessibility); [Carbon notification pattern](https://carbondesignsystem.com/patterns/notification-pattern)
- Carbon v10 said toasts auto-dismiss after 5 seconds; a newer page allows one tertiary action in toasts — versions conflict. — [Carbon v10 notification pattern](https://v10.carbondesignsystem.com/patterns/notification-pattern/) vs [Carbon Notification usage](https://carbondesignsystem.com/components/notification/usage/)
- Atlassian: never auto-dismiss error flags; the same applies to warnings; give enough time to read. — [Atlassian Flag examples](https://atlassian.design/components/flag/examples)
- Atlassian Forge `showFlag` with `isAutoDismiss` closes after 8 seconds. — [Forge showFlag](https://developer.atlassian.com/platform/forge/apis-reference/ui-api-bridge/showFlag/)
- Atlassian AUI: auto-closing flags fade out and still have a close button; some users need more time. — [AUI Flags](https://aui.atlassian.com/aui/latest/docs/flag.html)
- Atlassian message writing guide (overview). — [Atlassian: Designing messages](https://atlassian.design/foundations/content/designing-messages)
- GOV.UK validation: re-show inputs, place an error summary at top and move keyboard focus to it; error messages next to the fields; native HTML5 messages not recommended. — [GOV.UK: Recover from validation errors](https://design-system.service.gov.uk/patterns/validation/)
- GOV.UK-derived guidance: error summary heading "There is a problem"; do not use notification banners for validation errors; green notification banner confirms that something expected has happened. — [projectdelivery.gov.uk error summary (mirror)](https://projectdelivery.gov.uk/get-involved/connect-and-contribute/publishing-content-on-the-government-project-delivery-website/design-system/components/error-summary/); [DfE design history on banners](https://becoming-a-teacher.design-history.education.gov.uk/register-of-training-providers/how-we-show-success-error-and-notification-banners) **[mirrors, not the GOV.UK site itself]**
- GOV.UK publishing success alert: focused on page load, `role="alert"`. — [GOV.UK component guide: success alert](https://components.publishing.service.gov.uk/component-guide/success_alert)
- Shopify advises toast messages of three words or fewer; Workday advises against stacking dismissible toasts. — [Shopify alerts](https://shopify.dev/docs/apps/design/user-experience/alerts); [Workday Canvas notifications](https://canvas.workday.com/v9/patterns/notifications)
- NN/g frames status communication as indicators, validations and notifications; indicators can add clutter. — [NN/g: Indicators, validations, notifications](https://nngroup.com/articles/indicators-validations-notifications) (toast section not seen in excerpt)

### Inferences
- DashLens rules: toast = past-tense confirmation of a user action, ≤ ~5 words ("Pin added", "Link copied"), auto-dismiss ~4–5 s, no buttons except an optional single "Undo" (then keep until dismissed or extend). Error box = persistent, top of the stage, heading in GOV.UK style ("There is a problem with this footage"), one sentence of cause and one of fix, focus moved to it, close button.
- "Footage loaded" summary card = a success/notification-banner analogue: stays until dismissed or until playback starts, lists what was found (cameras, duration, gaps); never a toast, because it has content the user reads.
- Avoid: errors in toasts; stacking toasts; more than one toast visible.

### Gaps
- NN/g's specific toast and error-message articles (nngroup.com/articles/error-message-guidelines/) could not be read; fetch blocked.

## 6. Empty start screen and drag-and-drop target

### Takeaway
Carbon's empty-state anatomy fits the DashLens start screen: a positive title, body that names the next action, one primary action, optional secondary link, left-aligned block, decorative image hidden from screen readers.

### Cited Findings
- Carbon: title a short positive statement ("Start by adding data assets" rather than "You don't have any data assets"); body explains the next action, may say why it is empty and the benefit; primary action below copy, secondary link (e.g. docs) below that; pick the single most important action. — [Carbon Empty states pattern](https://carbondesignsystem.com/patterns/empty-states-pattern/); [Carbon v10 Empty states](https://v10.carbondesignsystem.com/patterns/empty-states-pattern/)
- Carbon: direct users to the control they will use every time afterwards (avoid a button that disappears once filled); elements left-aligned as a block; illustrations usually decorative and skipped by screen readers; the empty state replaces the whole element. — [Carbon Empty states](https://www.carbondesignsystem.com/building-blocks/core/patterns/empty-states)
- Atlassian has design guidelines for Pragmatic drag and drop (drop indicators, feedback). — [Atlassian Pragmatic drag and drop design guidelines](https://atlassian.design/components/pragmatic-drag-and-drop/design-guidelines) (content not seen in excerpt)

### Inferences
- Start screen: title "Open dashcam footage" (positive, action), body "Drop a folder or files here, or choose a drive. Nothing leaves this computer.", primary "Open folder", secondary "Choose drive"; and per Carbon's "control used every time afterwards" rule, the primary should point at (or be the same as) the top-bar Open control.
- Drop target: whole window is the drop zone while dragging (dashed accent outline + "Drop to open" label), not only a small box **[unverified; Dropbox/Drive pattern from prior knowledge]**.

### Gaps
- Dropbox, Google Drive, Vercel deploy and GitHub "drag files here" patterns were not researched in this session.

## 7. Segmented controls, switches, dropdowns

### Takeaway
Switch = instant effect only; checkbox when a Save/Submit step follows (NN/g, Primer, Apple). Segmented control for 2–5 mutually exclusive view modes, used for view-switching in toolbars or inspector panes, not for actions.

### Cited Findings
- NN/g: toggle switches should take immediate effect and not require Save/Submit; when that is not possible use radio buttons or a checkbox; do not mix instant and Save-requiring controls in one group. — [NN/g Toggle switch guidelines](https://www.nngroup.com/articles/toggle-switch-guidelines/); [NN/g video: Checkboxes vs switches in forms](https://www.nngroup.com/videos/checkboxes-vs-switches-forms/)
- Primer: ToggleSwitch is an instant-save control for boolean settings; checkboxes for selections that need an explicit save. — [Primer ToggleSwitch guidelines](https://primer.style/product/components/toggle-switch/guidelines)
- Apple HIG toggles page (official). — [Apple HIG Toggles](https://developer.apple.com/design/human-interface-guidelines/toggles.md) (content not seen beyond title)
- Apple: avoid crowding a segmented control; explicit limit found only for iPhone (five or fewer). — [codershigh mirror of iOS HIG](https://codershigh.github.io/guidelines/ios/human-interface-guidelines/ui-controls/segmented-controls/index.html) **[iOS, older mirror]**
- macOS HIG (via community translation): avoid segmented controls in a toolbar for switching contexts; consider them for view switching in a toolbar or inspector pane. — [Apple HIG Korean translation on GitHub](https://github.com/JHKits/Apple_HIG_Korean/blob/main/translated-markdown/components/selection-and-input/segmented-controls.md) **[unofficial; verify against developer.apple.com]**

### Inferences
- DashLens Settings drawer: all live settings use switches; the Save evidence dialog uses checkboxes. This is a direct rule worth writing into DESIGN.md.
- Segmented control: camera layout or units (km/h | mph) are good fits; do not use it for actions like "Export".
- Dropdowns: no source retrieved; Radix Select/DropdownMenu keyboard behaviour (type-ahead, arrow keys, Esc) is the usual reference **[unverified]**.

### Gaps
- Fluent switch and Carbon toggle/content-switcher specifics, Radix primitives, and slider guidance were not retrieved.

## 8. Command palette and shortcut help (kbd)

### Takeaway
Follow GitHub/Primer: a "?" key opens a dialog listing shortcuts for the current page, generated from one registry of shortcuts; follow Geist for kbd glyphs (⌘ on Mac, Ctrl elsewhere; one key per kbd element).

### Cited Findings
- GitHub: typing `?` opens a dialog listing keyboard shortcuts for the current page. — [GitHub Docs: keyboard shortcuts (source)](https://github.com/github/docs/blob/main/content/get-started/accessibility/keyboard-shortcuts.md)
- Primer: register every shortcut in one list (DEFAULT_KEYBOARD_SHORTCUTS) so it appears in the help dialog and respects a global disable setting; add `aria-keyshortcuts` to targets (space-separated alternatives, "+"-joined chords, full key names, e.g. `Control+K Meta+K`). — [Primer accessibility: Keyboard shortcuts](https://primer.style/accessibility/patterns/keyboard-shortcuts/)
- Geist Keyboard Input: modifiers as props (meta, shift, alt, ctrl); swaps ⌘ for Ctrl on Windows/Linux; children a single key; punctuation belongs in prose. — [Geist Keyboard Input](https://vercel.com/geist/keyboard-input)
- Key sequences rendered with "then" between keys ("G then T"). — [spy4x/preact-components PR #659](https://github.com/spy4x/preact-components/pull/659) **[third-party]**

### Inferences
- DashLens: one shortcut table in code feeds both the handlers and the "?" dialog, grouped (Playback, Navigation, Events, View); a global "Disable single-key shortcuts" setting (Primer). Show Ctrl on Windows (DashLens's Chrome/Edge audience is mostly Windows) and ⌘ only on Mac.
- A command palette (Ctrl+K) is optional; if added, it should search settings and actions from the same registry **[unverified that it is worth the cost]**.

### Gaps
- Linear Cmd+K, Raycast, VS Code command palette and Gmail "?" details not retrieved.

## 9. Charts in dark desktop UIs (speed / G-sensor graphs)

### Takeaway
Grafana's dashboard-level "Shared crosshair" / "Shared tooltip" is the reference for syncing hover across the speed and G-force charts and the video position.

### Cited Findings
- Grafana: Graph Tooltip option in dashboard settings; "Shared crosshair" shows the line at the same time on all panels; "Shared tooltip" also shows values on all panels; Ctrl+O cycles the modes. — [Grafana on X](https://x.com/grafana/status/1062480184731987969?lang=en); [Percona: Designing Grafana dashboards](https://www.percona.com/blog/designing-grafana-dashboards/); [Wikitech Grafana notes](https://wikitech-static.wikimedia.org/wiki/Grafana)
- Grafana per-panel tooltip modes: Single (hovered series), All (all series), Hidden. — [Amazon Managed Grafana v9 docs](https://docs.aws.amazon.com/grafana/latest/userguide/v9-time-series-panel-tooltip.html) **[Grafana 9.x]**

### Inferences
- DashLens: one shared crosshair across speed, G-sensor and timeline, driven by both hover and the playhead; tooltip shows all series at that instant (Grafana "All"/"Shared tooltip").

### Gaps
- Grafana time picker, legend placement and axis labelling guidance; Datadog, Vercel Analytics, Linear Insights were not retrieved. The `dataviz` skill in this environment could be used for chart styling rules instead.

## 10. Maps in web apps

### Takeaway
MapLibre's built-in controls cover DashLens's needs: NavigationControl (zoom, compass can be hidden), a follow/centre toggle modelled on GeolocateControl's `trackUserLocation` toggle behaviour, and a compact responsive AttributionControl.

### Cited Findings
- MapLibre GeolocateControl: with `trackUserLocation: false` it is a one-shot "centre on me" button; with `true` it is a toggle that keeps following; fires `trackuserlocationend` when following stops. — [MapLibre GeolocateControl](https://maplibre.org/maplibre-gl-js/docs/API/classes/GeolocateControl/); [MapLibre: Locate the user example](https://maplibre.org/maplibre-gl-js/docs/examples/locate-the-user/)
- OpenStreetMap's own site groups NavigationControl (`showCompass: false`) and GeolocateControl in one corner. — [OSM rails dashboard.js](https://git.openstreetmap.org/rails.git/blob/a801f7f72d730a1ba2c7916d57cb0aabc4dab583:/app/assets/javascripts/dashboard.js)
- MapLibre AttributionControl collapses on maps narrower than 640px by default; `compact: true` forces compact mode. — [maplibre-gl 4.1.3 source](https://app.unpkg.com/maplibre-gl@4.1.3/files/src/ui/control/attribution_control.ts); [ArcGIS MapLibre AttributionControl](https://developers.arcgis.com/maplibre-gl-js/api-reference/AttributionControl/)

### Inferences
- DashLens map: zoom +/- and a "Follow car" toggle grouped in one corner, compass hidden (north-up); following ends when the user pans (mirror `trackuserlocationend`) and the toggle visibly turns off; compact attribution in the opposite bottom corner, since the map pane is small (<640px).
- Avoid: hiding OSM attribution entirely (licence requirement **[unverified detail]**).

### Gaps
- Mapbox and Google Maps control placement docs, and Strava route-map styling, were not retrieved.

## 11. Layout editor (presets, undo, reset) and progress with cancel

### Takeaway
No primary source retrieved for layout editors. Carbon's progress modal (Cancel stays available) is the only cited reference for progress with cancel.

### Cited Findings
- Carbon progress modal keeps Cancel alongside Previous/Next while steps run. — [Carbon Modal usage](https://carbondesignsystem.com/components/modal/usage)

### Inferences
- **[unverified]** Grafana's dashboard edit mode and VS Code's "Reset view locations" are plausible references: an explicit edit mode with presets, Ctrl+Z undo and a single "Reset layout" that asks for confirmation only if there is no undo.

### Gaps
- Layout editor references (Grafana edit mode, VS Code layout customisation, Figma auto-layout) were not researched.
