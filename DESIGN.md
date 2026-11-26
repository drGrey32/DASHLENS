# DASHLENS design guidelines

These guidelines come from the design research of the OBD Inject app (`design/apex/RESEARCH.md` and
`design/apex/research/*.md` in that project). Only the rules that apply to a dashcam viewer are here. Each rule shows
its research ID in brackets, so you can find the source.

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

## 4. Telemetry: speed, heading, map, G-sensor

- **Speak the user's language** [FLOW-9]. "Braking 0.22 g" is good. Add a plain word for the owner ("light",
  "firm", "hard"), with the number beside it.
- **Colour only for status or meaning** [BV-1, COLOR rules]. One colour has one meaning everywhere. The brand colour
  is not used for data. The direction words stay on the G-sensor chart, so it reads without colour.
- **No fake precision.** Show GPS speed as recorded ("82 km/h, GPS"), with no decimals. With no GPS fix, show "—",
  never 0.
- **Units.** One visible setting (km/h or mph), from the locale by default.
- **Missing telemetry** [INT-23]. When a camera recorded no GPS or G-sensor data, the panel says so in one quiet
  line. It does not show an empty chart.

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
- **Long actions** [INT-10]: exports and reports show progress and Cancel.

## 7. Keyboard and accessibility

- **Every control works with the keyboard**, in a logical focus order, with a visible focus ring [WCAG 2.1.1, 2.4.7].
- **Player shortcuts:** Space (play/pause), ← and → (one frame), J K L (speed), number keys (cameras), and "?" for a
  list of all shortcuts. Every shortcut action is also a visible control [INT-1].
- **Icon buttons have names** [INT-25]: an `aria-label` on each, and a visible label where there is space.
- **Text size** [TEXT-2]: at least 12 px for all text that the user must read (file names, chart labels, legends).
  The layout still works at 200 % browser zoom.
- **Contrast:** small grey text on the dark background reaches at least 4.5:1 [WCAG 1.4.3].
- **Reduce motion:** with `prefers-reduced-motion`, no decorative animation. Playback and scrubbing never get
  extra animation.

## 8. Visual design

- **One accent, for interaction only** [BV-1]. If orange is the accent, it marks controls (and the playhead). It is
  not also the speed value or a data colour.
- **Few text sizes.** 4 or 5 roles: title, section, body, support, caption.
- **Monospace only for data that people compare:** times, file names, values. Not for labels.
- **No AI-slop decoration** (`ai-slop.md`, `anti-patterns.md`): no gradient glows, no emoji badges, no different
  chip style for each feature.

## 9. Privacy and trust

- **"Private by design" must stay exactly true.** The map tiles come from an external server. Say so at the map
  ("Map tiles are loaded from the internet. Your video stays on this computer.") and give a switch to turn the map
  off.
- **One line in the app says that nothing is uploaded and nothing is tracked.** Keep it true for every new feature.
- **No dark patterns** (ETHIC rules): no paid tier, no nags, no rating prompts, least of all after an incident.
- **Calm words inside the app.** The README's humour fits the project page. In the app, the user may have just had a
  crash (PSY research on stress and trust).

## 10. Evidence

This is the job that the product exists for.

- **Export a clip:** from an in point to an out point, all cameras, with an optional telemetry overlay, as one file
  that can go to an insurer or the police.
- **Incident summary:** date, time, place, speed, peak g, cameras and file names, as a page to print or save as PDF.
- **Originals stay untouched.** Say so at the export step, so that users trust the output.

## Priorities

1. Errors on the screen, not in toasts.
2. Keyboard access, labels, and the 12 px minimum text size.
3. "Next event" and an events list.
4. Event types that read without colour.
5. The map privacy line and a switch to turn the map off.
6. Clip export and the incident summary.
