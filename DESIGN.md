# DASHLENS design guidelines

These guidelines come from the design research of the OBD Inject app (`design/apex/RESEARCH.md` and
`design/apex/research/*.md` in that project). Only the rules that apply to a dashcam viewer are here. Each rule shows
its research ID in brackets, so you can find the source. Rules marked [R] come from DashLens's own research report,
`reports/Premium UI UX sources verified.md`, which was checked against primary sources, and from
`reports/Desktop UI references for DashLens.md` (desktop numbers: controls, spacing, type, notifications). DashLens is
made for desktops, laptops and landscape monitors, not phones.

## 1. Purpose and users

DASHLENS has one job: **find the moment, understand it, and keep the proof.** Every screen helps the user go from a
full SD card to one clear clip, snapshot or report.

There are two kinds of users:

- **The owner after an incident.** Stressed, in a hurry, maybe the first time with the app. Show this path first.
- **The enthusiast who reviews drives often.** Wants keyboard speed and detail. Give speed with shortcuts and
  details on demand, never by making the first path harder.

The user is parked or at a desk. The in-car glance rules do not apply; precision and reading do.

Fewer choices at each step (Hick's law) [INT-28].

## 2. Opening footage

- **Accept every input** [INT-22]: a folder, single files, drag and drop anywhere, the whole SD card, nested
  folders, duplicates.
- **Show progress during the scan** [INT-10, INT-11]. A scan that takes more than 1 s shows a counter ("Reading
  412 of 1 380 files"), each folder's result as it arrives, and Cancel. At the end, a clear summary: "4 drives,
  3 cameras, 2 events, 31 duplicates hidden".
- **Errors stay on the screen, never in a toast** [INT-16]. Example: "No .MP4 or .MOV files in this folder. Choose
  the folder that holds Normal, Event and Parking." Users miss a toast that closes after a few seconds.
- **Say what the app changed for the user** [FLOW-1, INT-15]. "Corrected the time of 3 clips" and "31 duplicates
  hidden" open to the list of the files concerned.

## 3. Timeline

The timeline is the centre of the product.

- **One meaning for each gesture** [BI-1]. A horizontal drag on the timeline always scrubs. Zoom is a separate
  control (buttons, Ctrl + wheel, pinch).
- **Direct feedback** [INT-10, INT-12]. The frame and the time under the cursor update within 0.1 s while
  scrubbing. If decoding is slow, show the nearest keyframe at once, then the exact frame.
- **Events must be clear without colour** [WCAG 1.4.1, COLOR rules]. Event, parking and driving differ by colour
  **and** by a pattern or shape, and the hover card names the type.
- **Gaps are data** [INT-23]. Keep the hatched gap and label it: "No recording, 08:22 to 12:44". "Skip the gaps"
  stays the default.
- **Jump to what matters** [INT-26]. "Previous event" and "Next event" controls, and an events list with the time,
  the peak g and the speed. This is the owner's main need after an incident.
- **Telemetry on the same time axis** [R]. Speed and G-force are lanes of the timeline, with their names in the lane.
- **Show the frame under the pointer** [R]. Hovering over the timeline shows a picture of that frame and its time.
- **Overview strip** [R] (DaVinci Resolve's Cut page). A 20 px strip above the timeline shows all the footage: drives,
  events, pins, gaps and the part that the timeline shows. A click or a drag on it moves the timeline view. Zoom
  presets: All, Drive, 10 min, 1 min and 10 s.
- **Values beside the lanes** [R] (Strava). The speed and G-force lanes show the value at the pointer, or at the
  playhead when the pointer is not on the timeline.
- **A clip range is a separate gesture** [R]. Shift + drag on the timeline selects a range; a plain drag always
  scrubs. The range chip gives the top speed, the peak G-force and the speed at the start and end. The map shows the
  range in the accent colour, and Save evidence uses the same range.

## 4. Telemetry: speed, heading, map, G-sensor

- **Speak the user's language** [FLOW-9]. "Braking 0.22 g" is good. Add a plain word for the owner ("light",
  "firm", "hard"), with the number beside it.
- **Colour only for status or meaning** [BV-1, COLOR rules]. One colour has one meaning everywhere. The brand colour
  is not used for data. The direction words stay on the G-sensor chart, so it reads without colour.
- **No fake precision.** Show GPS speed as recorded ("82 km/h, GPS"), with no decimals. With no GPS fix, show "—",
  never 0.
- **Units.** One visible setting (km/h or mph), from the locale by default.
- **Draw only what was recorded** [R]. Break the route and the speed line where GPS was lost. Never smooth over a gap:
  smoothed evidence looks more certain than it is.
- **One colour, one meaning** [R]. Teal is GPS (speed, route, heading). Coral and red are an event or a hard moment.
  Driving clips are a soft sky blue (`#79a8f2`): lively, but lighter and less saturated than any colour that carries a
  warning. Parking is sand. Left and right turns on the G-sensor are orchid pink (`#e89ad8`) and violet (`#a18bff`), so
  no turn colour is the driving blue. The user's own pins are light grey numbered tags (1, 2, 3 …), to differ by shape
  from event triangles. A pin has the same number on the timeline, on the map and in the events list and summary.
- **Car data when the car records it.** Tesla writes speed, position, G-force, brake, turn signals, gear and Autopilot
  state into every frame (firmware 2025.44.25 or later, HW3 or later). Read it from the file as the car wrote it, and
  say where it came from.
- **Each G-force lane has its own scale, and says it** ("Sideways, up to 0.10 g"). A shared scale hides a small
  sideways force next to hard braking. The smallest scale is ±0.1 g, so sensor noise stays small. A lane with no
  reading says "nothing recorded".
- **Missing telemetry** [INT-23]. When a camera recorded no GPS or G-sensor data, the panel says so in one quiet
  line. It does not show an empty chart.
- **Name missing data** [R]. Say "No GPS in this clip" or "No GPS in these files" where the speed would be, never 0.
- **Follow on the map has three states** [R] (MapLibre): following (filled), not following after the user pans
  (dashed; C or the button follows again), and disabled when there is no GPS. When the tiles cannot load, say "Map
  tiles need internet. The route is still shown."
- **A small G-sensor panel shows only the lanes** [R], at full width, when the ball chart would be smaller than
  110 px.

## 5. Layout editing

- **A visible control first; drag is a shortcut** [INT-1]. "Edit layout" is a button. Dragging a panel is a faster
  way to do the same.
- **Calm reflow** [BI-46, BI-47]. While a panel is dragged, show its landing place at once. Move the other panels
  only after the pointer rests for about 0.25 s, move only the panels in the way, and swap first.
- **Undo for each change, and "Reset layout"** [BI-45, OBD-6]. A panel can never get lost off the screen, and a
  panel that grows can always get smaller.
- **A way that needs no drag** [WCAG 2.5.7, BI-9]. The layout presets are this way. Give each preset a name
  ("Main and 3 small", "All equal"), in its label and tooltip.
- **Remember the layout** for each number of cameras, and say that it is remembered.

## 6. Feedback and errors

- **Toasts only for short confirmations** [INT-16]: "Snapshot saved". A confirmation can have one action
  ("Show in folder", "Copy").
- **A blocked action says why and what to do** [INT-15]. "Fullscreen not allowed here" also says how to allow it.
- **Prevent slips instead of reporting them** [INT-21]. When one recording type must stay on, disable its switch and
  give the reason beside it, instead of a toast after the click.
- **Long actions** [INT-10]: exports and reports show progress and Cancel. Counted progress ("Step 2 of 5",
  "9 of 14 clips"), never a skeleton screen for a process, and never a fake delay [R].

## 7. Keyboard and accessibility

- **Every control works with the keyboard**, in a logical focus order, with a visible focus ring [WCAG 2.1.1, 2.4.7].
- **Player shortcuts:** Space (play/pause), ← and → (one frame), Shift + ← → (5 s), J K L (speed), I and O (clip
  start and end; Shift + I / O goes there), = and − (timeline zoom; Shift + Z shows all), E (next event), number keys
  (cameras), P (pin this moment), and "?" for a list of all shortcuts. Every shortcut action is also a visible
  control [INT-1], and its key is in the control's tooltip [R].
- **Icon buttons have names** [INT-25]: an `aria-label` on each, and a visible label where there is space.
- **Text size** [TEXT-2]: at least 12 px for all text that the user must read (file names, chart labels, legends).
  The layout still works at 200 % browser zoom.
- **Contrast:** small grey text on the dark background reaches at least 4.5:1 [WCAG 1.4.3]. This is the compliance
  floor. The design targets are APCA [R]: primary text Lc 90, secondary text that people read Lc 75, short labels
  Lc 60 at weight 500 or more. The dimmest grey is only for disabled text and placeholders.
- **Reduce motion:** with `prefers-reduced-motion`, nothing moves or scales. State changes keep a short opacity fade
  (about 120 ms), so that the change is still visible [R]. Playback and scrubbing never get extra animation.
- **Targets:** every pointer target is at least 24 × 24 CSS px [WCAG 2.5.8]. A slider or scrubber is one target,
  so its whole box is at least 24 px tall. The drawn track can be thinner.
- **Toolbar:** a `role="toolbar"` has one Tab stop, and the arrow keys move focus inside it [APG]. A horizontal
  slider is the last control in the toolbar. After a pointer click on a transport button, the focus goes back to
  the player.
- **Focus ring:** 2 px solid accent, offset 2 px. Use -2 px only inside containers that clip [WCAG 2.4.13].
  Sticky parts never cover the focused control [WCAG 2.4.11].
- **Tooltips:** only on icon buttons, with the name and the key. Show after 400 ms; at once if another tooltip
  closed less than 500 ms ago; at once on keyboard focus. Hide on blur and Esc. The pointer can move onto the
  tooltip [WCAG 1.4.13]. Width at most 250 px, 4 px from the target. No tooltip during a drag.
- **Panels and focus:** a dialog keeps Tab inside it, and Esc closes the top panel (also from a text box; in a search
  box the first Esc clears the text). When a panel closes, a keyboard user gets the focus back on the control that
  opened it. After a mouse click the focus is not moved, so the arrow keys still move the video. A closed drawer is
  `inert`, so Tab never goes into it.
- **No error for a normal end:** "no more events" and "end of the footage" are short toasts, and Previous / Next
  event are off when there is no event in that direction. The error box is only for real problems.
- **Zoom:** drawers, dialogs, lists and the summary fit 320 CSS px wide without horizontal scroll [WCAG 1.4.10].
  Video, map and timeline are exempt.

## 8. Visual design

- **One accent, for interaction only** [BV-1]. If orange is the accent, it marks controls (and the playhead). It is
  not also the speed value or a data colour.
- **Few text sizes.** 4 or 5 roles: title, section, body, support, caption.
- **Monospace only for data that people compare:** times, file names, values. Not for labels.
- **No AI-slop decoration** (`ai-slop.md`, `anti-patterns.md`): no gradient glows, no emoji badges, no different
  chip style for each feature. Also [R]: no glass panels, no all-caps eyebrow labels, no monospace labels, no strings
  of words joined by middle dots, no thin border with a wide shadow, one icon family with one stroke width.
- **Closed sets of values** [R]: corner radii 4, 6, 8 and 12 px (and round for switches and dots); two shadow levels;
  the five text roles only; weights 400 to 600. Neutral greys with no tint; surfaces differ by lightness, and a line
  that carries meaning is at least #555 or the accent. `color-scheme: dark`.
- **Type** [R]: IBM Plex Sans and IBM Plex Mono, embedded in the file, so that no font is downloaded. Digits have
  equal width, so changing numbers do not move.
- **The dark theme stays** [R], because it is right for video. "Near-black with one bright accent" is a listed
  AI default, so DashLens's identity comes from the footage, the timeline and the evidence workflow, not from the
  palette.
- **Control heights:** 24, 32 and 40 px only. 24 px for timeline, lane, tile and chip controls (12 px text). 32 px
  for all other controls (14 px text). 40 px only for the start-screen primary action. Square buttons are as wide
  as they are tall. One height in each button group.
- **Spacing:** 2, 4, 6, 8, 12, 16, 20, 24, 32 and 48 px only. Gaps use 2, 4, 6, 8, 12, 16 or 24. Space inside a
  group is smaller than space between groups. Use `gap` on the parent, not margins on the children. Borders sit
  outside the padding.
- **Text sizes:** 12, 14, 16, 20 and 28 px only. 12 px for single lines only. 28 px for the speed readout only.
  Line heights are multiples of 4.
- **Weights:** 400, 500 and 600 only. `b` and `strong` are 600. The speed readout is 500.
- **Radii:** 4 px chips and lane marks; 6 px buttons, inputs and tooltips; 8 px tiles and cards; 12 px menus,
  drawers and dialogs. A child radius is never larger than its parent's.
- **Shadows:** two levels. Each starts with a 1 px ring at 12 % white, because a shadow alone does not show on
  the dark background.
- **Icons:** one family, one stroke width (2 on the 24 px grid). 16 px in 24 px controls and lists, 20 px in 32 px
  icon-only buttons.
- **Camera feeds:** each feed shows only its camera name (Front, Rear …), never the file name; the file name is in the
  ⓘ panel. The main camera has no highlight. Keys 1–9 select a camera; 0 shows the grid.
- **Warnings** use an icon and words, never an amber or orange colour, because orange is the accent.

## 9. Privacy and trust

- **All privacy information is in one place: Settings, Privacy.** No privacy note, badge or status appears on the
  start screen, the main screen, the map or any dialog. The owner's choice: notes on every screen distract.
- **"Private by design" must stay exactly true.** The map tiles come from an external server. Settings, Privacy says
  so, and its "Map tiles" switch turns the map off. The tile credit stays on the map as one small line, because the
  tile provider requires it; it is a credit, not a privacy note.
- **One line in Settings, Privacy says that nothing is uploaded and nothing is tracked.** Keep it true for every new
  feature.
- **Make the claim checkable** [R]. Settings, Privacy counts the internet requests from the browser's own log, names
  their hosts, tells the user how to check it in the browser's Network tab, says what is kept in the browser, and
  has a button to forget it.
- **No dark patterns** (ETHIC rules): no paid tier, no nags, no rating prompts, least of all after an incident.
- **Calm words inside the app.** The README's humour fits the project page. In the app, the user may have just had a
  crash (PSY research on stress and trust).

## 10. Evidence

This is the job that the product exists for.

- **Export a clip:** from an in point to an out point, all cameras, with an optional telemetry overlay, as one file
  that can go to an insurer or the police.
- **Incident summary:** date, time, place, speed, peak g, cameras and file names, as a page to print or save as PDF.
- **Originals stay untouched.** Say so at the export step, so that users trust the output.
- **An evidence package** [R] (NIST IR 8387, SWGDE, the UK dash cam portal): the working clip (re-encoded, say so),
  byte-exact copies of the original files, a SHA-256 checksum of every file in a separate file, the GPS route as GPX,
  and the summary with lossless (PNG) pictures. No enhancement, and no claim that the files will be accepted.
- **Design the end** [R]. The export ends on a screen that stays: "Your evidence is saved", with each file, what it
  is, and which files to send and which to keep.

## 11. Motion [R]

- **Nothing tied to the video clock animates**: the playhead, the time, the speed, the heading arrow and the map
  marker update at once.
- **Frequent actions do not animate**: keyboard actions, play, frame steps and seeks.
- **Durations**: about 100 ms for press feedback, 125–200 ms for tooltips and small menus, 200–300 ms for dialogs and
  drawers; exits are shorter than entrances. Animate only `transform` and `opacity`; never `transition: all`. Progress bars
  grow with `transform: scaleX()`, not `width`.
- **Idle**: when nothing changes (for example, the video is paused), nothing is drawn again. Parts that do not change
  each frame (the overview strip, map tiles and the route) are drawn once into a layer and copied.
- **Loading**: show a loader only after 150–300 ms, and keep it at least 300–500 ms, so it does not flash.
- **Toasts** stay 6 s. Hover or focus stops the timer. A toast with an action stays until the user closes it.

## 12. States [R]

Design every state of every screen: empty, first run, loading (counted), partly loaded, no GPS or G-sensor data,
error (on the screen), offline, disabled with the reason, cancelled, success that stays, very many clips, long file
names. A dialog takes the focus when it opens, keeps it inside, closes with Esc, and gives the focus back to the
control that opened it.
- **Dialogs:** 320, 480 or 640 px wide, never wider than the window minus 32 px. Body padding 16 px. Close
  button 8 px from the edges. Footer on the right, primary button last, at most two buttons. First focus on the
  first input, or on the primary button. Esc closes only the top dialog.
- **Settings drawer:** 480 px. Changes apply at once. A changed setting has a 2 px accent bar and a Reset action.
  Switches for live settings; checkboxes where a Save button follows.

## 13. The incident flow [R]

Find, review, save. Nothing about events opens by itself on startup or after loading: no events list and no
event card (the owner's choice). The events list (the "Events" button) has "Show the strongest moment", which opens a
card that says why it was chosen ("0.64 g. Both cameras saved it as an event recording."). Its main button goes to 5
seconds before the event, paused. The clip range stays
visible as a chip until it is cleared. The flow ends on the "Your evidence is saved" screen. Write this flow to be
calm and plain: no jokes, no exclamation marks, no blame (GOV.UK error rules).

## 14. Notifications [R]

- **Toast:** only to confirm something the user did. Two lines at most. Never an error or a warning.
- **On-screen error:** for anything that went wrong. It stays until fixed or closed. Heading "There is a
  problem", one sentence of cause, one of fix. The focus moves to it.
- **No banner for input errors.** Show the error next to the input and in the error summary.

## Priorities

1. Errors on the screen, not in toasts.
2. Keyboard access, labels, and the 12 px minimum text size.
3. "Next event" and an events list.
4. Event types that read without colour.
5. The privacy information and the switch to turn the map off, in Settings, Privacy.
6. Clip export and the incident summary.
7. Built in 1.6.0 [R]: Tesla's embedded telemetry (SEI); frame pins with notes, carried into the summary; a local
   "resume where you left off" (position, pins and clip range, in this browser only); a CSV export of the telemetry,
   one row for each recorded reading, with nothing filled in or smoothed.
