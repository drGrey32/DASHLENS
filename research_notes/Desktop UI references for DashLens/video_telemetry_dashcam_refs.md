# Desktop UI references for DashLens: video review, multicam, telemetry, dashcam viewers

Research date: 2026-11-26. Scope: desktop/laptop UIs only (web vs native noted).

Research limits to keep in mind:
- Several official hosts could not be fetched from this session because the network blocks them: dashcamviewer.com, docs.frigate.video, blog.frame.io and cdn.jjkeller.com (which hosts the Dashcam Viewer manual PDF). For those apps, the claims below come from search-result snippets of the official pages, which carry less weight than a full read. Each one is marked "(snippet)".
- GitHub pages were fetched in full: Tesla dashcam, Sentry-Six/Sentry Studio, LosslessCut and the Frigate 0.14 UI discussion.
- Points marked "(unverified)" come from my own background knowledge and have no source fetched this session. They are hints for follow-up, not citable facts.

## Q1. Pro video review and editing apps: what to borrow for transport, timeline, multicam, keyboard help

### Takeaway
Frame.io V4 (web) is the best model for a review-first player. It has frame previews when you hover the timeline, comments pinned to timecodes, and a "?" keyboard help panel. DaVinci Resolve and Premiere Pro supply the multicam conventions: number keys 1-9 pick an angle, and angle numbers are drawn over each tile. LosslessCut is the best model for a simple segment-and-export workflow. Full NLEs are too dense to copy whole.

### Cited Findings
**Frame.io V4 (web app; Adobe)**
- The V4 player added frame-accurate seeking: hovering over the timeline shows a preview of each frame as you move — [Frame.io blog, V4 Player and Commenting, May 2024](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/) (snippet)
- After a comment is submitted, focus goes back to the player so you can keep driving playback from the keyboard. Typing in the comment box pauses the player — [Frame.io blog, V4 Player and Commenting](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/) (snippet)
- Pressing "?" opens Keyboard Shortcuts Help, and a keyboard icon in the app shows the full list. Cmd+F and Cmd+K open search — [Frame.io Help: Keyboard shortcuts (V4)](https://help.frame.io/en/articles/9105337-keyboard-shortcuts) (snippet)
- Legacy player shortcuts: Space plays or pauses, C jumps into the comment box and pauses, I/O set in and out points for range comments, Tab leaves the comment box, and J/K/L follow standard NLE behaviour — [Frame.io Help: Keyboard shortcuts (legacy)](https://help.frame.io/en/articles/7785-keyboard-shortcuts-legacy) (snippet; legacy, so V4 may differ)
- A redesigned player put file metadata above the comments list — [Frame.io blog, Redesigned Player](https://blog.frame.io/?p=4451) (snippet)
- In the V4 Premiere Pro panel, comments are tied to sequence markers rather than the original timestamp — [Adobe Community: new Frame.io panel beta](https://community.adobe.com/announcements-732/now-in-beta-all-new-frame-io-panel-311901) (snippet)
- More references: [Frame.io Help: Player page features](https://help.frame.io/en/articles/7786-player-page-features), [Frame.io Help: Commenting](https://support.frame.io/en/articles/3331455-commenting), [Frame.io V4 Feb 2025 releases](https://blog.frame.io/2025/03/11/whats-new-in-frame-io-version-4-february-2025-releases/) (not fetched)

**DaVinci Resolve (native; Win/Mac/Linux; free version exists)**
- The Edit page has the classic multicam viewer: a grid of angles with precise trimming. The Cut page uses the Sync Bin, which is built for speed and works with the Speed Editor keyboard — [Digital Production, "Switching to Resolve: multicam", Apr 2026](https://digitalproduction.com/2026/04/24/switching-to-resolve-selects-and-assembly-in-multicam-editing/) (snippet)
- To change angles, click an angle in the Multicam Viewer or press number keys 1-9 — [Motion Array: Resolve multicam](https://motionarray.com/learn/davinci-resolve/davinci-resolve-multicam-editing/); [Larry Jordan: multicam in Resolve](https://larryjordan.com/articles/get-started-multicam-editing-in-davinci-resolve/) (snippets)
- One blog claims multicam mode became a property of the timeline viewer in Resolve 21. That is a single source and unconfirmed against Blackmagic's release notes — [Digital Production](https://digitalproduction.com/2026/04/24/switching-to-resolve-selects-and-assembly-in-multicam-editing/) (snippet)
- An experienced editor rates Resolve's multicam as the weakest of FCP, Premiere and Resolve — [ProVideo Coalition: Speed Editor review part 2 (multicam)](https://www.provideocoalition.com/review-davinci-resolve-speed-editor-part-2-multicam/amp/) (snippet)
- Cut page multi-angle tutorial: [RedShark News](https://www.redsharknews.com/tutorials/item/6840-how-to-use-resolve-s-cut-page-for-multi-angle-editing?hs_amp=true) (not fetched)

**Adobe Premiere Pro (native; Win/Mac)**
- In the Program Monitor you can add a "Toggle Multi-Camera View" button that shows all cameras at once. Wrench menu > Overlays numbers each angle — [Pixflow blog (Premiere multicam)](https://pixflow.net/blog/?p=94680) (snippet; third-party guide, check against Adobe Help)
- Source and Program monitor multicam view discussion: [Adobe Community thread](https://community.adobe.com/t5/premiere-pro/edit-multicam-view-in-timeline-for-both-source-and-program-monitors/m-p/12187401) (not fetched)

**LosslessCut (native Electron; Win/Mac/Linux; free, open source)**
- Features: merge cut segments; "Segments, markers and tags, with import/export of chapters, CSV, EDL and more"; snapshots and frame export; keyboard shortcuts; detect scenes, black frames and silence and split by them; "Change the format (remux) ... without re-encoding" — [GitHub mifi/lossless-cut README](https://github.com/mifi/lossless-cut)
- Platforms: macOS (Intel and Apple Silicon), Windows and Linux (x64/arm64), plus the Mac App Store, Microsoft Store and Snap. Windows 7/8/8.1 support ended after v3.50.0 — [GitHub README](https://github.com/mifi/lossless-cut)

### Inferences
- Transport: copy the Frame.io and NLE conventions. Space for play/pause, J/K/L for reverse, pause and forward speed, and I/O for in and out marks. Return focus to the player after any text entry, such as a pin note, so the enthusiast never loses keyboard control. This matches the legacy Frame.io behaviour above.
- Timeline hover: a frame-preview thumbnail on hover (the Frame.io V4 pattern) suits DashLens's canvas timeline. It lets the stressed owner find the moment of impact without playing through.
- Multicam: use the number keys 1-4 to focus a camera and show camera numbers or labels on each tile (Resolve and Premiere). DashLens has at most 4 cameras, so the 1-4 mapping fits cleanly.
- Keyboard help: "?" opening a shortcuts overlay is an established convention (Frame.io V4). DashLens should match it.
- Export: LosslessCut shows that a segment list plus a lossless or "copy original" option can live alongside a re-encode option. That maps onto DashLens's split between "original file copies" and "clip with telemetry overlay".
- Avoid copying full NLE density (Resolve's Edit page, Premiere's panels). DashLens users are reviewing, not editing.

### Gaps
- Final Cut Pro (multicam Angle Viewer, skimming), Avid Media Composer, Descript, Kdenlive, Shotcut, mpv, VLC and IINA were not researched this session for lack of budget. As background only (unverified): FCP's skimming (the playhead follows the pointer across the timeline) and IINA's minimal on-screen controller with a thumbnail-preview seekbar are worth looking at. Official sources to check: [Apple FCP User Guide](https://support.apple.com/guide/final-cut-pro/welcome/mac) and [IINA site](https://iina.io/) (not fetched).
- The current Frame.io V4 shortcut list could not be read in full because blog.frame.io is blocked here and help.frame.io was only seen as snippets.
- The LosslessCut README does not describe its export dialog or keyboard help dialog in detail. Its docs or screenshots would need a separate check.

## Q2. Multicam, security (VMS/NVR) and evidence platforms: timeline, event review, evidence export

### Takeaway
Security video tools are the closest match to DashLens's "event review + evidence" side. Frigate 0.14's redesign (web, free) has an alerts/detections/motion split, segments you can mark as reviewed, and export handles on the timeline. Milestone XProtect has evidence locks, bookmarks and digitally signed exports. Axon Evidence never modifies the original, logs extractions and offers a PDF audit trail. UniFi Protect 6.0 added multi-camera scrubbing.

### Cited Findings
**Frigate NVR 0.14+ (web UI; self-hosted; free, open source)**
- Rationale for the redesign: "Frigate's UI was never designed around specific user goals." It was rebuilt with a design firm (Jim Designs), funded partly by Frigate+ — [GitHub discussion #11136, Rebuilding the Frigate UI for 0.14](https://github.com/blakeblackshear/frigate/discussions/11136)
- The review page is timeline-oriented. Activity is grouped into segments that are "mutually exclusive," so each can be marked reviewed once watched. The default view covers the last 24 hours, and a calendar day can be picked — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- A scrollable thumbnail grid sits next to the timeline. Hovering previews a segment, and the progress bar allows scrubbing — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- Alerts are the higher-priority tab ("By default, all person and car objects are considered alerts"). The Motion tab scrubs all cameras at once against a motion-activity timeline — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- Export: "exporting using handles on the timeline is already implemented" — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- User complaints: a half-second stutter at every segment boundary; requests for a shared playhead with "Play All" synced across cameras; mobile controls too small — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- Home page: recent alerts appear as animated thumbnails in a filmstrip above the live feeds, and camera groups are available — [GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)
- History docs: [docs.frigate.video/usage/history](https://docs.frigate.video/usage/history) (host blocked here; not fetched)

**Ubiquiti UniFi Protect 6.0 (web + desktop app; tied to UniFi hardware)**
- Protect 6.0 (June 2025) added multi-camera scrubbing to review events across several feeds in parallel. It also added "Find Anything" search with object-count charts and zone filters, and frame-level object selection that finds a subject across cameras — [Ubiquiti blog: Introducing Protect 6.0](https://blog.ui.com/article/introducing-protect-6-0) (snippet)
- Older workflow: select each camera in Playback and view its timeline, with detections listed beside it — [Notion user guide to UniFi Protect](https://space-cadets.notion.site/Unifi-Protect-b6da3b51ad8a4ec8a9c2191f316a0626) (snippet; probably older than 6.0)
- Version overview with screenshots: [LazyAdmin: UniFi Protect 5.2.42 overview](https://lazyadmin.nl/home-network/unifi-protect-5-2-42-overview/) (not fetched)

**Milestone XProtect Smart Client (native Windows)**
- Evidence locks stop footage from being deleted. Locked evidence can be added to the Export list from the evidence lock list while staying in playback mode — [Milestone docs: Exporting video evidence (2024 R1)](https://doc.milestonesys.com/2024R1/en-US/standard_features/sf_sc/sf_operation/sc_exportingevidence.htm) (snippet)
- XProtect-format export can include a digital signature that the XProtect Smart Client – Player verifies (Export settings > XProtect format > Include digital signature) — [Milestone docs: Exporting video evidence](https://doc.milestonesys.com/2024R1/en-US/standard_features/sf_sc/sf_operation/sc_exportingevidence.htm) (snippet)
- Bookmarks and evidence locks can be searched, which the docs call more precise than the timeline controls, and several bookmarks can be edited at once from search results — [Milestone docs 2025 R1: actions from search results](https://doc.milestonesys.com/2025R1/en-US/standard_features/sf_sc/sf_investigate/current/sc_searchadditioninfoactionsfromsearchr.htm) (snippet)
- Full manual PDF: [XProtect Smart Client User Manual 2023 R3](https://doc.milestonesys.com/sc/pdf/2023r3/en-US/MilestoneXProtectSmartClient_UserManual_en-US.pdf); simplified manual: [2024 R1 Simplified](https://doc.milestonesys.com/sc/pdf/2024r1/en-US/MilestoneXProtectSmartClient_UserManualSimplified_en-US.pdf) (not fetched)

**Axon Evidence / evidence.com (web; body-camera evidence)**
- Extractions create a new evidence file from a parent file. "The original file is never modified," and each extraction becomes a separate, linked evidence item with its own audit trail. Clip and marker extractions follow the same pattern — [Axon Help: Understanding evidence extractions](https://www.axon.com/help/axon-evidence/software/axon-evidence/evidence/manage-evidence/evidence-extractions.htm) (snippet)
- The audit trail records views, updates and share/unshare. It is exported as a PDF via More actions > Audit trail, after choosing a period — [Axon Help: Audit trail](https://www.axon.com/help/axon-evidence/software/axon-evidence/audit-trail/audit-trail.htm) (snippet)
- Recommended order: clip first, extract, then redact the extracted clip — [Axon Help: evidence extractions](https://www.axon.com/help/axon-evidence/software/axon-evidence/evidence/manage-evidence/evidence-extractions.htm) (snippet)

### Inferences
- Event review: Frigate's "mark segment as reviewed" and its alerts vs detections tiers fit DashLens's events list. A "reviewed" check per event helps the enthusiast work through a long drive. Severity tiers (impact events above parking motion) help the stressed owner find the crash first.
- Multicam sync: Frigate's main complaint is stutter at segment boundaries and the lack of a shared "Play All" playhead. DashLens already syncs 4 cameras. It must avoid visible hitches at clip boundaries, since dashcams split drives into 1-3 minute files.
- Evidence export: present "Save evidence" in the Axon and Milestone framing. The original is never modified, the export is a new derived file, and integrity is shown. DashLens's SHA-256 checksums play the role of Milestone's signature. Adding a small action log (what was exported and when) to the incident summary page would mirror Axon's audit trail, without needing a server.
- Export range: timeline handles for in/out (Frigate) plus manual time entry (requested by Frigate users) is the right pair for the export dialog.

### Gaps
- Genetec Security Center, Blue Iris and Synology Surveillance Station were not researched (budget). Starting points, not fetched: [Genetec TechDoc](https://techdocs.genetec.com/), [Blue Iris help PDF](https://blueirissoftware.com/), [Synology Surveillance Station KB](https://kb.synology.com/).
- I could not confirm how UniFi Protect 6.0's multi-camera scrubbing works in its web vs desktop clients.
- Axon player marker UI details were not found in free sources.

## Q3. Telemetry and data-overlay tools: lanes, charts, map sync, overlay export

### Takeaway
Grafana sets the pattern for stacked charts that share a time axis: a shared crosshair and tooltip across panels, drag-to-zoom, and (in 12.4) drag on the axis to pan. Sentry Studio and Garmin VIRB Edit show what overlay export needs: gauge templates, a choice of overlay elements, and fixes for "gauges missing in export" bugs. MoTeC i2 and Telemetry Overlay show that syncing video and data is the hard, error-prone part.

### Cited Findings
**Grafana (web)**
- "Shared crosshair" shows the crosshair on every graph panel when you hover one, and "shared tooltip" also shows the tooltips. It is set in dashboard settings and is off by default — [Grafana docs: Modify dashboard settings](https://grafana.com/docs/grafana/latest/visualizations/dashboards/build-dashboards/modify-dashboard-settings/) (snippet)
- Grafana 12.4 (Jan 2026): drag the x-axis timestamps to pan, drag across a visualization to zoom into a range, and double-click to widen the range by half on each side. This works on time series, heatmap, state timeline and status history panels — [Grafana What's New: time range pan and zoom, 2026-01-15](https://grafana.com/whats-new/2026-01-15-time-range-pan-and-zoom/) (snippet)
- Community report: on the timeseries panel, shared crosshair and shared tooltip behave the same — [Grafana community](https://community.grafana.com/t/will-the-timeseries-panel-support-shared-crosshairs-tooltips-in-the-future/44153) (snippet; anecdotal)

**Telemetry Overlay (goprotelemetryextractor.com; native Win/Mac; paid)**
- Adds GPS, sensor and fitness data to video from GoPro, DJI and Insta360. Inputs include GPX. Exports are a finished MP4, transparent overlays or transparent frames — [manuals.plus mirror of the Telemetry Overlay manual](https://manuals.plus/GoPro/telemetry-overlay-manual); [Product Hunt listing](https://www.producthunt.com/posts/telemetry-overlay) (snippets; a mirror rather than the official host)
- After Effects templates exist, and transparent exports work with Resolve, FCP and Premiere — [RedShark News: GoPro Telemetry Extractor](https://redsharknews.com/post/item/6769-gopro-telemetry-extractor-lets-you-do-cool-stuff) (snippet)

**Sentry Studio / Sentry-Six (native Electron; macOS 13+, Win 10/11, Linux; free, open source; Tesla)**
- Overlay dashboards show speed, gear, Autopilot/Self-Driving state, pedals, steering, blinkers and G-force. They come in full and compact versions, floating or fixed to the front camera. Needs Tesla firmware 2025.44.25+ on HW3/AI3+ — [GitHub ChadR23/Sentry-Six](https://github.com/ChadR23/Sentry-Six)
- Export takes any cameras plus dashboard, map and timestamp, in H.264, HEVC or AV1. A full-window editor lets you drag and resize overlay elements, blur plates and faces, and preview the result — [GitHub Sentry-Six](https://github.com/ChadR23/Sentry-Six)
- The map marks FSD disengagements and accelerator presses along the route — [GitHub Sentry-Six](https://github.com/ChadR23/Sentry-Six)

**Garmin VIRB Edit (native Win/Mac; free; legacy product)**
- G-Metrix templates, gauges and graphs (speed, elevation, heart rate, G-force, lap data) and a track map next to the video. OBD-II gauges were added later — [Garmin VIRB manual (webhelp)](https://www8.garmin.com/manuals/webhelp/virbultra30/EN-US/GUID-F2CB040B-10E5-4BC1-B651-53F02E659850.html); [Garmin VIRB Edit downloads/changelog](https://www8.garmin.com/support/download_details.jsp?id=6592) (snippets)
- The changelog fixes "graphs not showing data in exported videos" and "frozen or flashing gauges" in export, and 5.3 added time-precise gauges — [Garmin VIRB Edit release notes](https://www8.garmin.com/support/download_details.jsp?id=6592) (snippet)
- The G-Metrix Sync tool for aligning GPS data with video froze for some users (2015-era) — [Garmin forums: VIRB Edit 3.0.1](https://forums.garmin.com/apps-software/apps-software-archive/f/virb-edit-windows/94000/virb-edit-3-0-1-is-available/518597) (snippet; historical)

**MoTeC i2 (native Windows; Standard free, Pro paid)**
- Synchronised video analysis is a listed feature. Sync is automatic with a MoTeC camera; other cameras need a Video Sync Module or manual sync in i2 Pro — [MoTeC i2 product page](https://www.motec.com.au/i2/); [MoTeC forum](https://forum.motec.com.au/viewtopic.php?p=25477) (snippets)

**Tesla SEI Explorer (web; official Tesla, open source)**
- "Web-based video player that displays SEI metadata alongside video playback": speed, steering wheel angle and self-driving state. Clips are loaded by drag-and-drop and "Works entirely in your browser - your files never leave your computer." Needs firmware 2025.44.25+ and HW3+ — [GitHub teslamotors/dashcam](https://github.com/teslamotors/dashcam); hosted at [teslamotors.github.io/dashcam/sei_explorer.html](https://teslamotors.github.io/dashcam/sei_explorer.html)

### Inferences
- Telemetry lanes: DashLens's speed and G lanes and the G-sensor chart should share one crosshair with the video playhead and the map marker. This is Grafana's shared crosshair, extended to video. Hovering any lane should show the value at that time in every lane, and clicking should seek.
- Zoom: Grafana 12.4's gestures (drag to zoom a range, double-click to zoom out) are a good, documented model for zooming DashLens's canvas timeline. A visible "reset zoom" control is still needed for discoverability (unverified recommendation).
- Overlay export: give a short choice of overlay elements (speed, G, map, timestamp) and a preview (Sentry Studio's editor, in simpler form). Test that the overlay really appears in the exported file, since VIRB Edit shipped several "gauges missing in export" fixes.
- Privacy: Tesla SEI Explorer's line "your files never leave your computer" is a short, official example of local-only wording that DashLens can match.
- Avoid manual sync tools for the user (VIRB G-Metrix Sync, MoTeC manual sync). Dashcam data is embedded, so DashLens should sync automatically and only flag drift.

### Gaps
- RaceRender, DashWare (discontinued), RaceChrono, AiM Race Studio, Track Attack and Harry's LapTimer: no usable free sources found in this session's searches.
- Strava and Garmin Connect activity pages (stacked charts synced with a map on hover) were not researched. Background only (unverified): both link a hover point on the elevation, pace and heart-rate charts to a dot on the route map.
- The official Telemetry Overlay manual on goprotelemetryextractor.com was not reached. Only a third-party mirror was seen.

## Q4. Dashcam viewers and their user complaints

### Takeaway
Dashcam Viewer (Win/Mac, third-party) is the closest feature match. It has a speed-colored route map, plots of speed, distance, bearing, G-force and altitude, and click-to-seek on both the map and the graphs. Sentry Studio is the strongest modern open-source multicam viewer (Tesla). Vendor viewers (BlackVue, Nextbase) draw consistent complaints: G-sensor or map data goes missing after updates, and the map marker falls out of sync with the video.

### Cited Findings
**Dashcam Viewer (dashcamviewer.com; native Win/Mac; free version plus Pro)**
- The route is drawn on a 2D map, color-coded by speed. Plots track speed, distance and compass direction over time. Clicking the map route or a graph trace jumps the video to that point — [BlackboxMyCar: Dashcam Viewer page](https://www.blackboxmycar.com/pages/dashcam-viewer); [Softpedia listing](https://www.softpedia.com/get/Multimedia/Video/Other-VIDEO-Tools/Dashcam-Viewer.shtml) (snippets)
- Graphs for speed, distance, bearing, G-force and altitude are available. Pro adds an Elevation Grade graph. The free version is "fully-functional" but loads up to 2 videos at a time — [search snippets of dashcamviewer.com / reviewer pages](https://kelaenderkoe.pages.dev/Function-https-dashcamviewer.com/features/) (snippet via a mirror; official page blocked here, so treat as unverified until checked)
- G-force support depends on the camera: no G-force for GoPro, and one BlackVue owner reported G-sensor data was not read — [DashCamTalk: Dashcam Viewer for Mac and Windows thread](https://dashcamtalk.com/forum/threads/dashcam-viewer-for-mac-and-windows.4357/post-453981) (snippet)
- The v3.9.7 changelog mentions a user-supplied GPS/G-force format (DTS) and fixes for Google Maps not loading — [Softpedia changelog](https://www.softpedia.com/progChangelog/Dashcam-Viewer-Changelog-246592.html) (snippet)
- User manual (JJ Keller edition PDF): [cdn.jjkeller.com manual](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/60428/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf) (host blocked here; not read)

**Sentry Studio / Sentry-Six (Tesla; Electron; free)**
- "All six cameras, perfectly in sync." You can focus one camera, zoom into it, and rearrange or mirror cameras. Speeds run 0.5x-4x with frame-accurate seeking — [GitHub Sentry-Six](https://github.com/ChadR23/Sentry-Six)
- The clip browser lists event triggers ("Manual Save", "Sentry", "Honk", "Object Detected"). Shortcuts can be edited in Settings. Export can blur plates and faces, and shared links expire — [GitHub Sentry-Six](https://github.com/ChadR23/Sentry-Six)

**BlackVue Viewer (native Win/Mac; free with cameras)**
- Four sections: recording list, playback, satellite/map position, and 3-axis accelerometer — [NikkTech DR900S review](https://www.nikktech.com/main/articles/gadgets/car-motorcycle/dash-cams/9604-pittasoft-blackvue-dr900s-2ch-4k-uhd-car-dashcam-review?start=4) (snippet)
- Complaint: on Viewer 1.09 the GPS map marker did not stay in sync with the video and only moved when the file changed — [DashCamTalk: which viewer software](https://dashcamtalk.com/forum/threads/which-viewer-software.36870/) (snippet)
- Playback failures on specific Windows and Android setups — [DashCamTalk: BlackVue player errors](https://dashcamtalk.com/forum/threads/blackvue-player-errors.50683) (snippet)

**Nextbase Replay 3 / MyNextbase Player (native Win/Mac)**
- G-sensor dials disappeared during playback in MyNextbase Player 4.14.1 on a 320XR — [DashCamTalk: 320XR G-sensor speed display](https://dashcamtalk.com/forum/threads/320xr-g-sensor-speed-display.53428/) (snippet)
- On the 412GW, a Nextbase representative said the software was misreading G-sensor data after an update and that a fix was in beta. Versions 3.4.1 and 3.6.3 later lost sensor and map data — [DashCamTalk: G-force display in Replay 3 incorrect](https://dashcamtalk.com/forum/threads/g-force-display-in-replay-3-incorrect.32467); [DashCamTalk: 412GW GPS speed data missing](https://dashcamtalk.com/forum/threads/nextbase-replay-3-playback-software-412gw-cam-gps-speed-data-missing.32967/page-2) (snippets; older, anecdotal)
- A positive counterpoint: the player gives a detailed display of map and G-sensor metadata — [Best Buy review, Nextbase 322GW](https://www.bestbuy.com/site/reviews/nextbase-full-hd-322gw-dash-cam-with-gps-wifi-bluetooth-parking-mode-2-5-touchscreen-black/6347000?page=22) (snippet)

### Inferences
- Map: copy Dashcam Viewer's speed-colored route and click-to-seek on both the map and the charts. DashLens's single orange accent rules out a full rainbow speed scale, so a lightness ramp or a single-hue scale with a legend fits the design rules (unverified recommendation).
- Avoid the top vendor failures: telemetry that silently vanishes and a map marker that drifts from the video. DashLens should say clearly when a file has no G-sensor or GPS data (for example, "No GPS in this clip") instead of showing empty dials, and keep the marker updated every frame.
- Multicam focus: Sentry Studio's "focus one camera, rearrange, mirror" is the right set for a 4-camera grid. Mirror matters for rear cameras.
- Event types: Sentry Studio's clip browser labels triggers in plain words ("Honk", "Sentry"). DashLens's event list should use plain labels too (Driving, Parking, Impact, Manual) rather than codes.

### Gaps
- Thinkware Dashcam Viewer, Viofo and Vantrue players, Garmin Drive, Rexing player, TeslaCam Browser and other teslacam-viewer projects: not researched this session.
- Reddit complaints were not searched. The DashCamTalk threads found are mostly several years old.
- The current Dashcam Viewer version and Pro pricing were not confirmed, because the official site was unreachable.

## Q5. Ranked recommendations: whole-app and per-element references

### Takeaway
Best whole-app references: (1) Dashcam Viewer, for domain fit: map, graphs and click-to-seek. (2) Sentry Studio, for a modern multicam dashcam viewer with overlay export. (3) Frigate 0.14+, for event review and timeline UX in a dark web UI. Per element, the strongest documented references are listed below. The ranking is my judgment based on the cited findings above.

### Cited Findings
Ranking is a synthesis. Each line points to the evidence in Q1-Q4.
- Whole app, domain fit: Dashcam Viewer — speed-colored route map, multi-metric graphs, click map or graph to seek ([BlackboxMyCar](https://www.blackboxmycar.com/pages/dashcam-viewer)) (snippet)
- Whole app, modern multicam dashcam: Sentry Studio — synced cameras, focus/rearrange/mirror, overlay editor, editable shortcuts ([GitHub](https://github.com/ChadR23/Sentry-Six))
- Whole app, event review in a web UI: Frigate 0.14+ — segments marked reviewed, alert tiers, thumbnail grid plus timeline, export handles ([GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136))
- Player transport: Frame.io V4 — Space, J/K/L, I/O, focus returns to the player ([Frame.io legacy shortcuts](https://help.frame.io/en/articles/7785-keyboard-shortcuts-legacy)); Sentry Studio 0.5x-4x and frame-accurate seeking ([GitHub](https://github.com/ChadR23/Sentry-Six))
- Timeline: Frame.io V4 hover frame preview ([Frame.io blog](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/)); Frigate segments and export handles ([GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)); Grafana 12.4 drag-to-zoom and pan ([Grafana](https://grafana.com/whats-new/2026-01-15-time-range-pan-and-zoom/))
- Multicam grid: Sentry Studio focus/rearrange/mirror ([GitHub](https://github.com/ChadR23/Sentry-Six)); Resolve/Premiere number-key angles and angle overlays ([Motion Array](https://motionarray.com/learn/davinci-resolve/davinci-resolve-multicam-editing/), [Pixflow](https://pixflow.net/blog/?p=94680)); UniFi Protect 6.0 multi-camera scrubbing ([Ubiquiti](https://blog.ui.com/article/introducing-protect-6-0))
- Telemetry lanes/charts: Grafana shared crosshair/tooltip ([Grafana docs](https://grafana.com/docs/grafana/latest/visualizations/dashboards/build-dashboards/modify-dashboard-settings/)); Dashcam Viewer click-graph-to-seek ([BlackboxMyCar](https://www.blackboxmycar.com/pages/dashcam-viewer))
- Map with route: Dashcam Viewer speed-colored route and click-to-seek; Sentry Studio event marks on the route (disengagements, pedal presses) ([GitHub](https://github.com/ChadR23/Sentry-Six))
- Event list: Frigate alerts/detections tiers and "reviewed" state ([GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136)); Sentry Studio plain-word trigger labels ([GitHub](https://github.com/ChadR23/Sentry-Six))
- Markers/pins: Frame.io timecoded comments and range comments with I/O ([Frame.io legacy shortcuts](https://help.frame.io/en/articles/7785-keyboard-shortcuts-legacy)); Milestone searchable bookmarks with bulk edit ([Milestone 2025 R1](https://doc.milestonesys.com/2025R1/en-US/standard_features/sf_sc/sf_investigate/current/sc_searchadditioninfoactionsfromsearchr.htm)); LosslessCut segments/markers with CSV export ([GitHub](https://github.com/mifi/lossless-cut))
- Export dialog: Axon "original never modified" plus linked extraction and audit trail ([Axon](https://www.axon.com/help/axon-evidence/software/axon-evidence/evidence/manage-evidence/evidence-extractions.htm)); Milestone signed export ([Milestone](https://doc.milestonesys.com/2024R1/en-US/standard_features/sf_sc/sf_operation/sc_exportingevidence.htm)); Sentry Studio overlay element choice and preview ([GitHub](https://github.com/ChadR23/Sentry-Six)); LosslessCut lossless vs re-encode ([GitHub](https://github.com/mifi/lossless-cut))
- Settings: Sentry Studio editable shortcuts in Settings ([GitHub](https://github.com/ChadR23/Sentry-Six)); Frigate's new Settings page was praised by testers ([GitHub #11136](https://github.com/blakeblackshear/frigate/discussions/11136))
- Empty/loading states: Tesla SEI Explorer's drag-and-drop prompt with a local-only privacy line ([GitHub teslamotors/dashcam](https://github.com/teslamotors/dashcam))
- Keyboard help: Frame.io V4 "?" Keyboard Shortcuts Help plus an in-app keyboard icon ([Frame.io Help](https://help.frame.io/en/articles/9105337-keyboard-shortcuts))

### Inferences
- No single app covers DashLens's mix of local-only multicam review, telemetry and an evidence bundle. The best plan is to combine Dashcam Viewer's domain features, Frigate's review flow and Axon/Milestone's evidence framing, with Frame.io-level transport and keyboard polish.
- For empty and loading states, the evidence is thin. Only the Tesla SEI Explorer drop prompt was confirmed. Loading states for "reading N files / extracting GPS" still need their own references.

### Gaps
- No source was found for empty, loading or error-state design in any of the apps beyond the Tesla drop prompt.
- No screenshots were viewed in this session, so all layout judgments rest on text descriptions.
- Hosts to allow for a follow-up pass: dashcamviewer.com, docs.frigate.video, blog.frame.io, cdn.jjkeller.com. Other likely ones: goprotelemetryextractor.com, iina.io, support.apple.com.
