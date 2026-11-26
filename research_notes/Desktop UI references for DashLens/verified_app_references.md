# Verified desktop app references for DashLens (video, telemetry, dashcam)

Research date: 2026-11-26. This pass follows up on `video_telemetry_dashcam_refs.md`.

Method: pages were read in full with `curl` (static pages and PDFs, via `pdftotext`) and with Playwright (JavaScript pages). WebSearch was used only to find URLs. Everything marked "(read)" was read in full this session. "(snippet)" means only a search-result snippet was seen. "(unverified)" means background knowledge only, with no source read.

Screenshots viewed: Dashcam Viewer manual v4.0.9 page 1 (main window, Windows) and Thinkware U3000 PRO manual page 31 (PC viewer layout). All other layout judgments rest on text.

One host was rate-limited: dashcamviewer.com/features/ and /whats-new/ returned HTTP 429 to curl. The official manual and version history PDFs linked from dashcamviewer.com/resources/ were read instead.

## Q1. Do the earlier snippet-only claims hold up? (Dashcam Viewer, Frigate, Frame.io)

### Takeaway
Most earlier snippet claims are confirmed. Several should be sharpened:
- Dashcam Viewer is now v4.0.9 (Sep–Oct 2026). Its free tier limits are 2 videos and a 5-second clip export. It shows only 2 channels (front/rear picture-in-picture), and it spreads its UI over 5 separate floating windows.
- The Frigate History view (current docs) is a closer match to DashLens than the Review page cited last time. It has a main player, a row of secondary camera previews, a side panel that switches between Timeline, Events and Detail, and an Actions menu with an Export dialog.
- The Frame.io V4 shortcut list is now fully read. It confirms "?" for shortcut help and adds full transport details, plus user-remappable shortcuts.

### Cited Findings
**Dashcam Viewer (native macOS + Windows; Free / Plus / Pro; Earthshine Software)**
- Current manual is "USER'S MANUAL v4.0.9 28 Sep 2026", 80 pages, covering the macOS and Windows apps. It handles "videos, GPS data, and G-force data recorded by dashcams and action cams", and you can "group your videos into trips, geotag key points … and export your route to … CSV … GPX … KML" — [Dashcam Viewer User's Manual v4.0.9 (PDF, linked from dashcamviewer.com/resources)](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Version history: 4.0.9 (Oct 11, 2026) adds GUI tweaks for macOS 26. 4.0.7 (Sep 2025) adds the PRO "Elevation Grade graph". 4.0.6 (Mar 2025) makes "Click-to-Go … enabled on the Map display by default". 4.0.5 (Dec 2024) adds "a 'Cancel' button to the Video Load progress bar … The video files that have been loaded up to that point will still be processed and displayed" — [Dashcam Viewer Version History PDF](https://www.dropbox.com/s/8yh4b525vrzgv15/history.pdf?dl=0) (read)
- Tier limits:

  | Limit | Free | Plus | Pro |
  |---|---|---|---|
  | Videos | 2 | 600 | 1200 |
  | Geotags | 2 | 10 | 100 |
  | Audio event detection | 1 video | 5 videos | 100 videos |
  | Clip export duration | 5 secs | no limit | no limit |

  OpenStreetMap is Pro only — [Manual v4.0.9, "Dashcam Viewer versions"](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read). This confirms the earlier snippet "free loads up to 2 videos".
- Multicam is limited to 2 channels. You can "select the front or rear channel for display in the main player window", or show both "in a picture-in-picture mode". The "r" key swaps front and rear — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Map (confirms the earlier snippet):
  - Route color shows speed: "Faster speeds are bluish and slower speeds are reddish". The user can choose 1, 5, 10 or 14 colors, and the maximum can be a fixed speed or the trip's top speed.
  - "Follow" checkbox pans with the vehicle. "Click To Go" clicks near the route to seek. An "N Up" toggle controls orientation.
  - Map controls hide themselves when the window is narrow.

  Sources: [Manual v4.0.9, Map Window](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0); [J.J. Keller edition manual v3.3.3 (2019)](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/60428/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf) (both read)
- Graphs: speed, distance (color-coded by speed), bearing, G-force X/Y/Z, and altitude where available. There is an Autoscale button. Clicking a graph jumps the video, and this can be turned off in Preferences. The 2019 manual adds that "two clicks are required in the Windows version" — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0); [JJK v3.3.3](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/60428/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf) (read)
- Geotags (user pins):
  - Press "g" or click the button to create one. The default title is the street address (reverse geocoded).
  - Each tag shows as a numbered marker on the map. The list item shows title, file, time in movie, speed, date/time, lat/long, and line-of-sight and route distance to the current position.
  - Double-click a tag to jump to it. A gear icon renames, and a trash icon deletes.
  - Tags export to and import from a tab-delimited text file.

  Source: [Manual v4.0.9, Geotags](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Trips: videos are binned into trips, with a default gap of 60 s (changeable in Pro, down to 1 s). Each trip shows start, duration, distance, video count and the "Gap time" before it. Trips are color-coded by duration, red for long and green for short — [Manual v4.0.9, Trips](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Audio Event Detection: it scans the audio for sudden loudness. Events show as "little squares along the graph time axis", with blue forward/back buttons to jump between them. A sensitivity control runs from 1 to 10. Squares are colored red, yellow or green by significance, and significance is computed per video — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Data Browser: tabs show the current video's data as CSV, GPX, KML or GeoJSON before you export — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Clip export: you type a start time and a duration. Options cover excluding audio, resizing the PiP frame and changing the playback rate (slow motion "useful for isolating short events, like a collision") — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0); [JJK v3.3.3](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/60428/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf) (read)
- Shortcuts:
  - Space plays or pauses. Arrows jump 1 or 10 files. P takes a snapshot.
  - A/S/W/D pan the zoomed video, Q/E zoom, and 0 resets.
  - g adds a geotag, r swaps front and rear, c copies lat/long. Cmd-F or F11 toggles fullscreen.
  - In graphs, "m , . /" shift the GPS/video time offset by -10, -1, +1 and +10 s.

  Source: [Manual v4.0.9, Shortcuts](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Window model: there are "5 main windows". Menu items "Reset Window Positions", "Sync Window Movement" and "Clean Up" exist because "the windows can become hidden or overlap in an inconvenient way". The recommended screen is 1600x1200 or larger. Maps need an internet connection — [Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Error and empty states:
  - "No GPS Data for this segment" appears on the Graph display, and readouts then show 0.
  - A wrench icon next to a file name flags data-integrity problems. Hovering it explains the issue, for example "Some GPS data points out of chronological order. Sorting required." or "At least one point required an artificial time code."

  Source: [Manual v4.0.9, FAQ and Data Integrity Codes](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (read)
- Marketing site lines: "compatible with over 140 different dashcam models", "Accident Evidence & Accountability … Audio Event Detection allows accident events to be found quickly" — [dashcamviewer.com home](https://dashcamviewer.com/) (read)
- Screenshot judgment (manual p.1, Windows):
  - A large video sits top-left with the rear camera as a picture-in-picture inset, and a big speed readout sits top-center.
  - The control-panel list is top-right and the map fills the right column.
  - The speed graph is bottom-left and the dashboard gauges are bottom-center.
  - The UI is dense and has a light-themed system chrome — [Manual v4.0.9 p.1](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0) (viewed)

**Frigate NVR (web UI; self-hosted; free) — official docs now read**
- History is "Frigate's full-resolution recording viewer". You reach it from Review, from Live, or from a share link, and it opens scrubbed "to just before the activity" — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- Empty state: "If you see 'No recordings found for this time', the most common causes are: recording was not enabled … the retention window has since expired … or storage ran low" — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- The side panel toggles three modes. Timeline is a "scrubbable vertical timeline": motion shows as horizontal lines whose length means more motion, review items show as shaded areas ("red for alerts, orange for detections"), and stretches with no recording have no background. Events is a list where clicking seeks. Detail is an object inspector — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- Scrubbing moves "the main player and any secondary camera previews … together". Zoom buttons change the timeline scale "from coarse to fine segments". On desktop, "a row of secondary previews shows the other cameras at the same moment. Clicking one of them makes it the main camera at the current timestamp" — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- Detail cards show severity, start time, labels, object count and duration. "The active card is highlighted as the video plays, and clicking a card seeks to it." A lifecycle row has "a progress line that follows the current playback position". An "annotation offset" fixes timing drift — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- Calendar: an underline marks days that have recordings. A red or orange dot marks days with unreviewed alerts or detections — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- The Actions menu (a film icon) holds Export: "The dialog pre-selects the last hour; adjust the range or drag the timeline handles". It also holds Share Timestamp, Motion Search and a snapshot of the current frame — [Frigate docs: History](https://docs.frigate.video/usage/history) (read)
- Review page: review items sit on a vertical timeline next to a grid of low-frame-rate previews. "Hovering over or swiping a preview plays the video and marks it as reviewed." A review item bundles overlapping objects into one period, and "Reviews for a single camera cannot overlap" — [Frigate docs: Review configuration](https://docs.frigate.video/configuration/review) (read). This confirms the earlier GitHub #11136 claims.

**Frame.io V4 (web; Adobe) — now read in full**
- The player has "frame-accurate seeking … by hovering over the timeline and seeing a preview of each frame". Playback tools are "pinned in the exact same spot in the bottom of the player" for every media type. A "pocket-sized version of the player" can stay open while you browse. "When you submit a comment, focus immediately shifts back to the player … When you start typing again, the player is immediately paused." Anchored comments let you click a point on the frame — [Frame.io blog, V4 Player and Commenting, 28 May 2024](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/) (read)
- V4 shortcuts (article updated 25 Sep 2026):
  - Help: "?" opens Keyboard Shortcuts Help, which is also reachable from a keyboard icon.
  - Playback: Space or K plays and pauses. J and L play reverse and forward at multiple speeds. Shift+J and Shift+L step the speed incrementally. Ctrl+L loops.
  - Stepping: Left and Right arrows move 1 frame, and Shift+arrows move 10 frames.
  - Ranges and markers: I and O mark in and out points. Shift+I and Shift+O go to them. R marks a range. C adds a comment.
  - View: M mutes, F is fullscreen, G shows guides. Cmd+scroll zooms smoothly, and Z+drag does a marquee zoom.
  - Remapping: "Custom Keyboard Shortcuts allow you to remap any … click the pencil icon … disable … by clicking the 'x' … restore … return arrow."

  Source: [Frame.io Help: Keyboard shortcuts (V4)](https://help.frame.io/en/articles/9105337-keyboard-shortcuts) (read)
- Legacy list confirmed: J/L step through "1x, 2x, 4x, and 8x". Shift+Drag gives "Precision scrubbing", D shows clip info, and R defines a cycle range — [Frame.io Help: Keyboard shortcuts (Legacy)](https://help.frame.io/en/articles/7785-keyboard-shortcuts-legacy) (read)

### Inferences
- The Frigate History layout is the closest documented web analogue to DashLens: main player, secondary camera previews, a side panel switching Timeline/Events/Detail, and an Actions menu with Export. Clicking a secondary preview to make it the main camera at the same timestamp fits DashLens's 4-camera grid "focus" mode.
- Dashcam Viewer proves the domain feature set (speed-colored route, click-to-seek graphs, geotags, trips, audio events, GPS integrity flags). Its 5 floating windows and "Reset Window Positions" escape hatch are a pattern to avoid. DashLens's single-page fixed layout is a real advantage, and its 4 cameras beat DCV's 2-channel picture-in-picture.
- DCV's integrity wrench (hover to explain bad GPS) and Frigate's "No recordings found … common causes are" are the two best-documented error and empty-state references found so far.
- Frigate uses red for alerts and orange for detections. DashLens uses a single orange accent, so it should borrow the shading and gap structure but encode severity with shape or labels rather than a second hue.

### Gaps
- dashcamviewer.com/features/ and /whats-new/ returned 429 to automated requests. The manual and history PDFs cover the same ground.
- No screenshot of the macOS Dark Mode DCV UI was viewed.
- Frigate's Exports page (the list of saved exports) was not read.

## Q2. Players and editors not covered before: IINA, Final Cut Pro, DaVinci Resolve Cut page

### Takeaway
- Final Cut Pro (native macOS) gives the best-documented multicam angle viewer and the skimming model.
- The Resolve Cut page gives the best timeline idea for long drives: an always-full-width overview timeline above a zoomed timeline.
- IINA 1.5 (native macOS, Sep 2026) is a reference for player chrome and settings design (docked vs floating controls, a live Layout sidebar, settings visible at a glance). It is not a reference for review tools.

### Cited Findings
**Final Cut Pro 13 (native macOS; needs macOS 26.6)**
- Current version: "Final Cut Pro 13 introduces new features…". Minimum system "macOS 26.6" — [Apple FCP User Guide: What's new](https://support.apple.com/guide/final-cut-pro/whats-new-ver19637ebab/mac) (read)
- Skimming: "move the pointer forward or backward over a clip … the content under the pointer plays in the viewer. The skimmer (a vertical red line) indicates exactly where the pointer is." Press Space "to play forward from the skimmer position". S toggles skimming and Shift-S toggles audio skimming. Apple notes "you may find skimming distracting", so it can be turned off — [Apple FCP: Skim media](https://support.apple.com/guide/final-cut-pro/skim-media-vere9ba3609/mac) (read)
- Angle viewer:
  - It shows all angles at once, in "banks of 2, 4, 9, or 16 angles". It opens with Shift-Command-7.
  - Click an angle, or press a number key, to cut and switch. Option-click or Option+number switches without cutting.
  - "The active angle is highlighted in yellow, blue, or green" depending on mode: video+audio, video only or audio only.

  Source: [Apple FCP: Cut and switch camera angles](https://support.apple.com/guide/final-cut-pro/cut-and-switch-camera-angles-ver23c76c9c/mac) (read)
- Angle names come from Camera Angle, then Camera Name, then Camera ID metadata. "If none of this information is found, a separate angle is created for each selected clip" — [Apple FCP: Add camera names and angles](https://support.apple.com/guide/final-cut-pro/add-camera-names-and-angles-ver26f5c183/mac) (read)
- Markers: M adds one ("press M while playing" to add on the fly). Option-M adds one and opens its info. Control-M deletes one, as does dragging it out of the clip — [Apple FCP: Add and remove markers](https://support.apple.com/guide/final-cut-pro/add-and-remove-markers-verf3fd3b5c/mac) (read)
- Keyboard help: the Command Editor (Option-Command-K) shows a virtual keyboard. "Key colors correspond with command groups". It has a search field and a "Keyboard Highlight" button that shows the keys for the listed commands — [Apple FCP: View keyboard shortcuts](https://support.apple.com/guide/final-cut-pro/view-keyboard-shortcuts-ver4df74f72/mac) (read)

**DaVinci Resolve Cut page (native Win/Mac/Linux; free and Studio)**
- Dual timeline: "The Upper Timeline always shows the entire program within the full width of your computer's display … serves as a visual reference for keeping track of where you are … while you're editing within the zoomed-in Lower Timeline." The lower timeline "shows you a close-up view … surrounding the playhead. The zoom level is fixed" — [Resolve 18 Reference Manual ch. "The Cut Page" (third-party mirror of the official chapter)](https://ltbits.github.io/davinci-resolve-manuals/DR18/DR18-RM04-TheCutPage.pdf) (read; mirror, DR18 text)
- Fast Review: "begins accelerated playback … where the speed of playback is relative to the length of each clip … Long clips play faster, whereas shorter clips play closer to real time." There is also a jog control "to scrub very precisely" — [DR18 Cut Page chapter](https://ltbits.github.io/davinci-resolve-manuals/DR18/DR18-RM04-TheCutPage.pdf) (read; mirror)
- Boring Detector: it analyzes clip lengths and highlights long clips in light gray and very short ones in red on the Upper Timeline. Thresholds are set in a slider window — [DR18 Cut Page chapter](https://ltbits.github.io/davinci-resolve-manuals/DR18/DR18-RM04-TheCutPage.pdf) (read; mirror)
- Sync Bin: when you scrub, "all of the clips in the Sync Bin will scrub along with the playhead position". It needs common timecode and a "Unique Camera Name" (A, B, C or 1, 2, 3). A Sync Clips window shows "a live multi-camera sync Viewer … and a timeline below that shows the temporal relationship of all the clips" — [DR18 Cut Page chapter](https://ltbits.github.io/davinci-resolve-manuals/DR18/DR18-RM04-TheCutPage.pdf) (read; mirror)
- In Resolve 20 the Cut page still exists. It adds Voiceover, ripple editing on secondary tracks, and Source Tape changes — [DaVinci Resolve 20 New Features Guide (official PDF)](https://documents.blackmagicdesign.com/SupportNotes/DaVinci_Resolve_20_New_Features_Guide.pdf) (read; skimmed for Cut page sections)

**IINA 1.5.1 (native macOS 12+; free, GPLv3; built on mpv)**
- IINA 1.5.0 (28 Sep 2026) is "the biggest interface redesign since IINA's launch":
  - A new Layout sidebar lets you "adjust the layout and appearance while playing, without having to open the Settings window".
  - Sidebars, title bar and on-screen controller "can also be docked so that they remain visible". Left and right sidebars can show at the same time.
  - A "Compact Interface option" brings back the denser layout.
  - Settings was rewritten so that "information [is] visible at a glance rather than hiding it inside drop-down menus, pop-up windows, or secondary pages."

  Source: [IINA blog: IINA 1.5.0 is Released](https://iina.io/blog/150-release/) (read)
- Site: "Download 1.5.1, Requires macOS 12.0". "It does not include tracking or telemetry" — [iina.io](https://iina.io/) (read)

### Inferences
- Timeline: borrow Resolve's two-tier timeline for long drives (often 30–120 min of 1–3 min files). A thin always-full-width overview strip (whole drive, events, pins, viewport box) sits above the zoomed working timeline. It answers "where am I in the drive" without zoom gestures.
- Hover: FCP skimming and the Frame.io hover preview are the same idea at two strengths. FCP moves the viewer itself, while Frame.io shows a thumbnail. For 4 synced cameras, a thumbnail tooltip (Frame.io) is safer than full skimming, because skimming would force 4 decoders to seek on every mouse move. Any skimming should be opt-in behind an "S" toggle, as in FCP (inference).
- Multicam: FCP's number-key angle switch and active-angle highlight map onto DashLens keys 1–4 to focus a camera. Use the accent outline for the active tile, and take tile labels from file metadata or file name, the way FCP falls back from Camera Angle to Camera Name to ID.
- Fast Review (speed relative to clip length) is a good idea for a "skim the whole drive" mode, but it is optional.
- Avoid copying the FCP Command Editor's full virtual keyboard for a roughly 20-shortcut app. Its color-grouped categories and search field are the parts worth borrowing for DashLens's "?" panel.
- IINA's docked vs floating controller choice is a useful Settings toggle for DashLens: overlay controls over the video vs a fixed transport bar. "Visible at a glance" is a good rule for a small settings panel.

### Gaps
- The DR20/21 Reference Manual Cut page chapter (over 4,000 pages, very large PDF) was not downloaded. The DR18 chapter mirror was used, and DR20 changes were checked only against the New Features Guide.
- IINA's thumbnail-preview seekbar was not confirmed in an official source this pass (unverified). docs.iina.io covers the plugin API, not the UI.
- No FCP or Resolve screenshots were viewed.

## Q3. Security video timelines: UniFi Protect (web) and Synology Surveillance Station (web)

### Takeaway
- Synology documents the most concrete review-timeline controls: preset zoom levels (24/12/8/4/2/1 h), a "Show Events Only" filter, previous/next event, frame step while paused, Sync vs Non-sync multi-camera playback, and download of a clip by interval.
- UniFi Protect 7.2 (Jul 2026) is the most relevant evidence reference: SHA-256 fingerprinting and signing of clips with public verification, plus chain-of-custody logs.

### Cited Findings
**Synology Surveillance Station 9 (web UI inside DSM; NAS-bound)**
- "Multi-Recording Playback allows you to simultaneously watch videos recorded on one day or at the same time by different cameras. All recordings are lined up on the timeline" — [Synology Help: Work with Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player) (read via Playwright)
- Timeline colors mark "No event was detected" vs "Event detected" (motion, audio, tampering, etc.), independent of recording schedule — [Synology: Work with Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player) (read)
- Controls: a calendar picks the date. Buttons go to the previous or next recording, play backward or forward, slow down or speed up, and "While pausing, click … to see the previous or next frame." "Sync Mode": Sync plays "multiple videos recorded at the same time", Non-sync plays "gaplessly (not necessarily at the same time)". A drop-down toggles "24, 12, 8, 4, 2 or 1 hour mode". "Show Events Only" filters the timeline. Seek works by typing a time and clicking "Go To" — [Synology: Work with Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player) (read)
- Per-tile tools: Snapshot; "Drag and zoom" for digital zoom with a "Reset digital zoom" control; show camera name and time; camera info (codec, FPS, bit rate, resolution); fixed aspect ratio. Download offers "Download complete file" or "Download a video clip: Specify the time interval", saved as .mp4 — [Synology: Work with Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player) (read)
- Web-player limits: "Only H.264 and MJPEG video codecs are supported. At most 36 channels are supported in the Timeline layout" — [Synology: Work with Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player) (read)
- User Guide 9 (Feb 2026): Monitor Center has Alerts and Bookmarks panels. Playback controls "play, pause, rewind, or fast forward 10 seconds, jump to the previous or next event, or jump to the previous or next second". "The currently selected camera feed is highlighted with a yellow frame. Double-clicking any camera feed enlarges the image … Double-clicking again returns to the normal layout." Recordings can be locked "to ensure they are not accidentally deleted" — [Surveillance Station 9 User Guide (PDF)](https://global.download.synology.com/download/Document/Software/UserGuide/Package/SurveillanceStation/9.0/enu/Surveillance_Station_User_Guide_9_enu.pdf) (read)

**UniFi Protect (web app + desktop/mobile; tied to UniFi hardware)**
- 6.0 (12 Jun 2025), as stated in Ubiquiti's post:
  - "The new timeline shows quick, camera-specific object summaries, allowing instant playback from any detected event."
  - "Object-counting charts", "Spatial filters", and "Multi-camera scrubbing lets you review events across multiple feeds in parallel".
  - "Full audit trail of footage views, downloads, and deletions".

  Source: [Ubiquiti blog: Introducing Protect 6.0](https://blog.ui.com/article/introducing-protect-6-0) (read; confirms earlier snippet)
- 7.0 (17 Mar 2026): "The timeline has been redesigned with a smoother multi-playback workflow … Multi-camera synchronized playback". "Consolidated motion events for cleaner timelines", "Motion paths embedded directly in thumbnails" — [Ubiquiti blog: Introducing Protect 7.0](https://blog.ui.com/article/introducing-protect-7-0) (read)
- 7.2 (30 Jul 2026): "Each clip can be cryptographically fingerprinted with SHA-256 and digitally signed, allowing downloaded evidence to be verified at evidence.ui.com. Authentic videos are confirmed, while altered or tampered-with clips ar[e flagged]." Case management records "who viewed a case, which assets were accessed, and what evidence was downloaded". Mobile gets "frame by frame scrubbing directly from the timeline" — [Ubiquiti blog: Welcome to UniFi Protect 7.2](https://blog.ui.com/article/welcome-to-protect-7-2) (read)
- Third-party notes, not official: playback is scrubbed by dragging, a scissors tool downloads a clip, and motion-only recordings are shaded purple — [SJB help article](https://help.sjb.school/support/solutions/articles/55000013048) (snippet). Firefox seeking is slow compared with Chromium — [Mozilla Connect thread](https://connect.mozilla.org/t5/discussions/poor-performance-with-ubquiti-s-unifi-protect-video-viewer/m-p/42860) (snippet)

### Inferences
- Timeline zoom: Synology's preset scale buttons (24/12/8/4/2/1 h) are a discoverable alternative to gesture-only zoom. For drive-length data, presets such as "Whole drive / 10 min / 1 min / 10 s" fit DashLens (inference).
- Transport: Synology's previous/next event plus frame step when paused, together with Frame.io's J/K/L, covers everything a crash reviewer needs.
- Evidence: UniFi 7.2 is the strongest current precedent for DashLens's SHA-256 bundle. DashLens cannot sign without keys or a server, but it can say plainly what the hash proves ("these bytes are unchanged since export") and what it does not prove (authenticity at capture). That difference is exactly what UniFi's signed capture-time fingerprint adds (inference).
- Sync vs Non-sync: Synology's split matches DashLens's "cameras in sync at time T" vs "play through clips gaplessly". DashLens only needs Sync. Non-sync is a possible "continuous drive" playthrough.

### Gaps
- The help.ui.com UniFi Protect pages returned 403 to curl and were not opened in Playwright. No official UniFi web-timeline manual was read, only release blogs. Web vs desktop-app differences remain unverified.
- No screenshots of either UI were viewed.

## Q4. Telemetry and activity tools: Strava, Garmin Connect, RaceRender, RaceChrono, Telemetry Overlay

### Takeaway
- Strava's web analysis view is the best documented model for DashLens's speed and G lanes. It has stacked charts with instantaneous values that update on hover, average and maximum stats for a dragged selection, drag-to-zoom, and the selection highlighted on the map.
- Telemetry Overlay is the leading paid desktop overlay tool. It is offline, has an export queue, and includes click-on-chart-or-map seeking in its sibling Telemetry Extractor.
- RaceChrono is mobile-only, so it is out of scope as a desktop reference.

### Cited Findings
**Strava activity pages (web)**
- Analysis view:
  - "To the right of the elevation profile and the stacked performance chart (speed, power, and other values), you'll see instantaneous values … Moving your cursor over the elevation profile or any performance chart updates those values."
  - "To the left of the charts, you'll see average and maximum values for the selected range."
  - "Click and drag a selection … to zoom in … The statistics … update to reflect your selection, which is highlighted in blue on the map. You can then expand, shrink, or slide that selection. Click anywhere on the elevation profile or stacked charts to zoom back out."
  - A mile-marker or clock icon switches between distance-based and time-based views.

  Source: [Strava Support: Ride Activity Pages (18 Sep 2026)](https://support.strava.com/en-us/articles/15401886-ride-activity-pages) (read)
- Segment bars below the elevation profile show where segments fall. Hovering a segment highlights it "in blue on the map, with the portion of your ride's elevation profile … shown in dark gray". The summary panel "is persistent across all views" and has Show More / Show Less, and "Your browser will remember this preference" — [Strava: Ride Activity Pages](https://support.strava.com/en-us/articles/15401886-ride-activity-pages) (read)
- Runs: "Hover over a lap to see it highlighted in both the map and elevation profile; click to zoom in, and click again to 'unfocus.'" "Mouse over the elevation profile to view instantaneous stats" — [Strava Support: Run Activity Pages (9 Sep 2026)](https://support.strava.com/en-us/articles/15401883-run-activity-pages) (read)

**Garmin Connect (web + mobile)**
- "GPS-tracked activities include a map with a themed polyline that details the metric of your choice along your route" — [Garmin blog: Unlocking the Potential of Garmin Connect](https://www.garmin.com/en-US/blog/fitness/unlocking-the-potential-of-garmin-connect/) (read)
- Device manual: "an overhead map view, pace and speed charts, and customizable reports" — [Garmin Descent Mk2i manual: Garmin Connect](https://www8.garmin.com/manuals/webhelp/GUID-4A2D3019-BA14-49BD-B371-4214D187D493/EN-US/GUID-5C0E79E4-C381-4B87-A6A0-B8FE049AB597.html) (read)
- Forum reports: the web map is "very very small", and charts or maps are sometimes missing — [Garmin Forums: full screen map very small](https://forums.garmin.com/apps-software/mobile-apps-web/f/garmin-connect-web/143235/full-screen-map-currently-very-small) (snippet)

**Telemetry Overlay / Telemetry Extractor (native Windows, macOS, Linux; paid)**
- Telemetry Overlay costs $199 ("Pay once, Use forever, 1 Year Updates & Support"). Key features include "GPS routes with map & satellite — Hundreds of gauge types … Activity presets … Export Queue — Batch Loader — Join multiple files — Transparent/chroma exports — Mix multiple data sources — Works offline" — [goprotelemetryextractor.com: Telemetry Overlay](https://goprotelemetryextractor.com/telemetry-overlay-gps-video-sensors) (read; official host, confirming the earlier mirror-based claims)
- Telemetry Extractor: "The data is presented in a visual and interactive way. You can click on customizable maps and charts to move the video to that position." Tesla: "Original Tesla dashcam video files contain telemetry data since late 2025 … a great way to review an incident or a significant event" — [goprotelemetryextractor.com: Tools for Tesla](https://goprotelemetryextractor.com/tools-for-tesla) (read)
- The site lists "Crash reconstruction" as a use case — [goprotelemetryextractor.com](https://goprotelemetryextractor.com/) (read)

**RaceRender 3 (native Windows, macOS; HP Tuners; Free / Deluxe / Advanced / Ultimate)**
- "Supports multiple cameras with picture-in-picture, split-screen, and camera-switching capabilities". Data formats include "CSV, VBO, NMEA, GPX, TCX, FIT". Features include "Customizable Layouts & Sizes" and "Trimming and Synchronization Tools". The Free edition's "Maximum Output Video Length [is] 3 Minutes" with a logo. Deluxe costs $39.95, Advanced $49.95 and Ultimate $59.95 — [RaceRender Features](https://racerender.com/RR3/Features.html) (read)

**RaceChrono (iOS and Android only)**
- Feature table includes "Data analysis with synchronised graph, map and video" and "Hardware accelerated video export with configurable data overlay". Changelog v10.3.5 for Android (23 Nov 2026): "Fixed: Laggy analysis map cursor". iOS v10.3.3: "Analysis layout changed from side-by-side …" (truncated on page) — [racechrono.com](https://racechrono.com/) (read)

### Inferences
- Telemetry lanes: copy Strava's three-part pattern.
  - Instantaneous values next to the lanes at the cursor or playhead.
  - Drag a range on any lane to zoom, with that range's average and maximum (for example max G, max speed, speed drop) shown at the side and the range highlighted on the route.
  - Click to zoom back out.

  For an incident, "speed before/after" and "peak G" over a selected range are exactly what a stressed owner needs for an insurer.
- The range selection (Strava) and the export range (Frigate's handles) should be the same object. Select a range on the lanes, and "Save evidence" prefills with it (inference).
- Map: Garmin's "polyline that details the metric of your choice" and DCV's speed-colored route agree. Use a single-hue speed ramp, so it stays within the one-accent rule.
- Avoid the overlay-editor depth of Telemetry Overlay and RaceRender (hundreds of gauges, layout editors). DashLens's overlay needs a fixed, legible preset plus a few toggles.
- RaceChrono's "laggy analysis map cursor" fix shows that map cursor performance is a known pain point. Throttle map-marker updates to animation frames, not every telemetry sample (inference).

### Gaps
- Garmin Connect's web hover sync between charts and the map was not confirmed from an official source (unverified).
- No public Strava activity page was opened in a browser, because it needs a login. Behavior comes from Strava's own support articles.
- RaceRender's User Guide is a frameset and its pages were not read in detail. Telemetry Overlay's manual was not read.

## Q5. Vendor dashcam desktop viewers: VIOFO, Thinkware, Garmin

### Takeaway
Vendor viewers are thin: a playlist, a front/rear toggle, a small map, and G and speed readouts. They are useful mainly as a baseline that DashLens must exceed. VIOFO Player is actively maintained (v1.1.20, Jun 2026). Garmin's desktop Dash Cam Player has not been updated since 2018.

### Cited Findings
**VIOFO Player (native Windows + macOS; free)**
- "Desktop player for recorded video with GPS track & G-sensor … view the GPS route and speed, read G-sensor data, and capture screenshots." Windows V1.1.20 dated 2026-06-08. Updates:
  - "Added video editing mode, supporting … video trimming, adding title cards, and customizing export resolution".
  - "Added a multi-stream playback-based video stitching method".
  - "Added support for panning the video frame in zoom mode".
  - "after a single video segment finishes playing, the next video will automatically play in sequence".

  Source: [VIOFO Help Center: Software](https://www.viofo.com/pages/viofo-app) (read via Playwright)
- Forum: GPS and map data were missing for some users on early builds — [DashCamTalk: Official VIOFO Player thread](https://dashcamtalk.com/forum/threads/official-viofo-player-now-available-for-windows-pc-mac.52227/post-635410) (snippet)

**Thinkware PC Viewer (native Windows + macOS; free)**
- U3000 PRO manual (Sep 2025), section 6.2.2 screen layout. The front camera video is large on the left, and the rear camera video is smaller at top-right. Below those are a map, a playlist (bottom-right), a G-sensor value readout, the driving speed, current and total time, a progress bar, and playback controls. There are buttons to switch front and rear, open settings and go fullscreen. The Mac version is on the App Store as "Thinkware Dashcam Viewer". Listed requirements (Windows 7+, Mac OS X 10.10+, DirectX 9) look outdated — [Thinkware U3000 PRO manual, Sep 2025 (PDF)](https://download2.inavi.com/dashcam/U3000PRO/manual/u3000pro_manual_english_20250924.pdf) (read, and page 31 screenshot viewed)

**Garmin**
- The desktop "Garmin Dash Cam Player for Mac" was last updated to version 2.6 "as of January 25, 2018". Earlier changes included "Show unconnected note in map view when internet is unconnected" and "Added trimming ability for .mp4 files" — [Garmin: Dash Cam Player for Mac Updates & Downloads](https://www8.garmin.com/support/download_details.jsp?id=7164) (read)
- The Garmin Drive app is mobile (iOS/Android) — [App Store: Garmin Drive](https://apps.apple.com/us/app/1276198893) (snippet)
- Garmin manuals say Dash Cam Player can "view and overlay time, date, location, and speed information" — [Garmin Dash Cam 46/56/66W manual: Videos and Photos on Your Computer](https://www8.garmin.com/manuals/webhelp/dashcam46-56-66w/EN-GB/GUID-E75CB7BE-ACAB-4427-A608-A4D9F919A911.html) (fetched; body text not extracted, so snippet only)

### Inferences
- The common vendor layout (Thinkware, and DCV's p.1 screenshot) puts the front camera large, the rear camera small, a map at the side and readouts below. DashLens's equal-tile 2x2 grid with a focus mode is more flexible, but a "front large + others small" preset should exist because users expect it (inference).
- VIOFO adding auto-play of the next segment in 2026 confirms that seamless playback across segment boundaries is a basic expectation. DashLens must not stutter there (see the Frigate complaint in the earlier notes).
- Garmin's 2018 "unconnected note in map view" is a small precedent for an explicit offline map state. DashLens should say "Map tiles need internet; route still shown" or similar rather than show a blank map (inference).

### Gaps
- BlackVue Viewer and Nextbase current versions were not re-checked this pass. See the earlier notes, which are snippet-only.
- No VIOFO Player screenshots or manual were viewed.

## Q6. Final ranked references for DashLens (whole app and per element)

### Takeaway
- Best whole-app references:
  1. Frigate History/Review (web) for the overall layout of a single-page review tool.
  2. Dashcam Viewer 4.0.9 (native) for domain features.
  3. Sentry Studio (Electron) for a modern multicam dashcam viewer (earlier notes).
- Per element, the strongest verified references are listed below with a one-line reason. The ranking is my judgment from the findings above.

### Cited Findings
**Whole app**
1. Frigate History + Review (web, dark, free): main player, synced secondary previews you can click to promote, a Timeline/Events/Detail side panel, an Actions menu with Export, and explicit empty states. It is the closest single-page analogue — [Frigate History](https://docs.frigate.video/usage/history)
2. Dashcam Viewer 4.0.9 (native Win/Mac): the most complete dashcam feature set (speed-colored route, click-to-seek graphs, geotags, trips, audio events, GPS integrity flags). Borrow the features, not the 5-window layout — [DCV Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
3. Sentry Studio (Electron): modern multicam dashcam UI with overlay export, from the earlier notes — [GitHub ChadR23/Sentry-Six](https://github.com/ChadR23/Sentry-Six)

**Per element (best first)**
- Player transport:
  - Frame.io V4. It has a complete, documented key set: Space/K, multi-speed J/L, 1 or 10-frame arrows, I/O, Shift+I/O, R range, Ctrl+L loop — [Frame.io V4 shortcuts](https://help.frame.io/en/articles/9105337-keyboard-shortcuts)
  - Runner-up: Synology. It adds previous/next event and frame-step-while-paused — [Synology Timeline](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player)
- Timeline:
  - Resolve Cut page dual timeline. A whole-drive overview strip sits above the zoomed lane — [DR18 Cut Page](https://ltbits.github.io/davinci-resolve-manuals/DR18/DR18-RM04-TheCutPage.pdf)
  - Plus Frame.io hover frame preview — [Frame.io blog](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/)
  - Plus Synology preset zoom levels and "Show Events Only" — [Synology](https://kb.synology.com/en-us/SurveillanceStation/help/SurveillanceStation/multievent_player)
  - Plus Frigate shaded review regions with visible no-recording gaps — [Frigate History](https://docs.frigate.video/usage/history)
- Multicam grid:
  - FCP angle viewer. Number keys switch angles, the active angle is highlighted, and names come from metadata — [Apple FCP angles](https://support.apple.com/guide/final-cut-pro/cut-and-switch-camera-angles-ver23c76c9c/mac)
  - Plus Frigate click-a-secondary-preview-to-promote at the same timestamp — [Frigate History](https://docs.frigate.video/usage/history)
  - Plus Synology double-click to enlarge and again to restore, with a highlighted selected tile — [Synology SS9 User Guide](https://global.download.synology.com/download/Document/Software/UserGuide/Package/SurveillanceStation/9.0/enu/Surveillance_Station_User_Guide_9_enu.pdf)
- Telemetry lanes:
  - Strava analysis. Stacked charts, live values at the cursor, a drag-select range with average and maximum, and the range highlighted on the map — [Strava Ride Activity Pages](https://support.strava.com/en-us/articles/15401886-ride-activity-pages)
- Map with route:
  - Dashcam Viewer. Speed-colored route with a configurable scale, Follow, Click To Go, N Up, and controls that hide when narrow — [DCV Manual v4.0.9](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
  - Plus Strava's selection highlight on the map — [Strava](https://support.strava.com/en-us/articles/15401886-ride-activity-pages)
- Event list:
  - Frigate Events/Detail. Click seeks, and "the active card is highlighted as the video plays" — [Frigate History](https://docs.frigate.video/usage/history)
  - Plus DCV audio events on the time axis with previous/next buttons and graded severity — [DCV Manual](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
- Markers/pins:
  - FCP markers. M adds one while playing, Option-M adds one and edits its note, Control-M deletes — [Apple FCP markers](https://support.apple.com/guide/final-cut-pro/add-and-remove-markers-verf3fd3b5c/mac)
  - Plus DCV geotags. The "g" key, an auto address title, numbered map markers, and text export/import — [DCV Manual](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
- Export dialog:
  - Frigate Export. The range is preselected and adjustable by typing or by dragging timeline handles — [Frigate History](https://docs.frigate.video/usage/history)
  - Plus UniFi 7.2's SHA-256 fingerprint with verification, which frames DashLens's checksums — [Ubiquiti 7.2](https://blog.ui.com/article/welcome-to-protect-7-2)
  - Plus DCV's Data Browser preview of CSV/GPX before export — [DCV Manual](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
- Settings:
  - IINA 1.5. Settings are visible at a glance with no hidden drop-downs, a live Layout sidebar works without opening Settings, and docked vs floating controls plus a Compact option are offered — [IINA 1.5.0 blog](https://iina.io/blog/150-release/)
  - Plus Frame.io remappable shortcuts — [Frame.io V4 shortcuts](https://help.frame.io/en/articles/9105337-keyboard-shortcuts)
- Empty, loading and error states:
  - Frigate "No recordings found for this time" with its likely causes listed — [Frigate History](https://docs.frigate.video/usage/history)
  - Plus DCV's cancellable load progress that keeps the files already loaded, "No GPS Data for this segment", and a hover-to-explain integrity icon — [DCV history](https://www.dropbox.com/s/8yh4b525vrzgv15/history.pdf?dl=0), [DCV Manual](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)
  - Plus Tesla SEI Explorer's local-only drop prompt, from the earlier notes — [GitHub teslamotors/dashcam](https://github.com/teslamotors/dashcam)
- Keyboard help:
  - Frame.io V4 "?" panel, also reachable from a keyboard icon, with remapping — [Frame.io V4 shortcuts](https://help.frame.io/en/articles/9105337-keyboard-shortcuts)
  - Borrow only the color-coded command groups and search from FCP's Command Editor — [Apple FCP view shortcuts](https://support.apple.com/guide/final-cut-pro/view-keyboard-shortcuts-ver4df74f72/mac)

**Avoid list (verified)**
- Multi-window layouts that need a "Reset Window Positions" command ([DCV](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0)).
- Maps that silently need internet ([DCV](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0); [Garmin DCP changelog](https://www8.garmin.com/support/download_details.jsp?id=7164)).
- Free-tier export caps such as a 5 s clip or 3 min output ([DCV](https://www.dropbox.com/s/w2ppuuyxbkyho73/Dashcam%20Viewer%20Users%20Manual.pdf?dl=0), [RaceRender](https://racerender.com/RR3/Features.html)).
- Gauge editors with hundreds of options ([Telemetry Overlay](https://goprotelemetryextractor.com/telemetry-overlay-gps-video-sensors)).
- Two-hue severity coding (red/orange) that clashes with DashLens's single orange accent ([Frigate](https://docs.frigate.video/usage/history)).
- Abandoned vendor viewers ([Garmin DCP 2018](https://www8.garmin.com/support/download_details.jsp?id=7164)).

### Inferences
- The concrete gaps DashLens can fill against every tool here:
  - local-only in the browser,
  - 4 synced cameras,
  - one fixed dark layout,
  - range selection shared by lanes, map and export,
  - an evidence bundle with plain-language hash wording.

  No reviewed app combines all of these.
- Highest-value additions suggested by this pass (inference, not yet validated with users):
  1. A whole-drive overview strip above the zoomed timeline (Resolve).
  2. Strava-style live values plus range statistics on the lanes.
  3. Frigate-style "active event highlighted as video plays" in the events list.
  4. Explicit empty and error states for no GPS, no G-sensor and failed files (Frigate, DCV).

### Gaps
- No official Sentry Studio re-check this pass; its entries rely on the earlier notes (GitHub README read then).
- No usability or user-preference data exists for any of these patterns. The rankings are expert judgment from documentation.
