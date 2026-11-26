# UI/UX Patterns from Pro Video Tools and Dashcam/Telemetry Viewers, for DashLens

Method note: research ran on 2026-11-26. Page fetching was blocked in this session (blog.frame.io and heise.de did not resolve), so the findings below come from search-result summaries of the cited pages, not full reads. Treat exact wording as close paraphrase. Where a source is a vendor blog, forum post or low-authority guide, it is flagged. No Reddit or DashCamTalk threads came back in any search, so the complaints below come from App Store reviews, GitHub READMEs and Tesla Motors Club / racing forums.

## 1. Pro video tools: transport, JKL, timecode, timeline, in/out, markers, scrub preview, multicam, shortcut discoverability

### Takeaway
Pro tools have settled on one shared keyboard grammar: J/K/L shuttle (repeat presses speed up), arrow keys for single frames and Shift+arrow for 10 frames, I/O for in and out with Shift+I/O to jump to them, and number keys to pick a camera angle. Frame.io V4 adds frame-accurate hover previews and comments tied to a point or a range. DashLens should copy this grammar exactly rather than invent its own, because the enthusiast users already know it from YouTube, QuickTime and NLEs.

### Cited Findings
**Frame.io (V4, 2024–2025)**
- V4 (beta May 2024) shipped a fully redesigned player and commenting. Seeking is frame-accurate, and hovering over the timeline previews each frame — [Frame.io blog, V4 Player and Commenting, 2024-05-28](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/)
- V4 comments can be anchored to a point on video, images or design frames. Frame.io says this makes them easier for new or unfamiliar reviewers to find — [Frame.io blog, 2024-05-28](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/); [Frame.io blog, V4 beta announcement, 2024-04-09](https://blog.frame.io/2024/04/09/frame-io-version-4-beta-is-here/)
- A later redesigned player (date unclear, probably 2025) plays at the highest resolution by default, adds 1:1 frame guides, a dedicated audio player and a new URL structure. File metadata now sits above the comments, and long comment lists scroll smoothly — [Frame.io blog, "Introducing a Redesigned Player Experience"](https://blog.frame.io/?p=4451). The search results also show a 2018 post with the same title ([2018 post](https://blog.frame.io/2018/02/02/a-redesigned-player-experience/)), so the date of these details is uncertain.
- Current Frame.io shortcuts: I sets the in point and O the out point. Shift+I and Shift+O jump to them. R marks a range, C adds a comment and Shift+R replies. Arrow keys step 1 frame and Shift+arrow steps 10 frames — [Frame.io Help, Keyboard shortcuts (current)](https://help.frame.io/en/articles/9105337-keyboard-shortcuts)
- In the legacy Frame.io player, I/O set the in and out of a range-based comment, C moves the cursor into the comment box and pauses the clip, and Tab moves the cursor back out — [Frame.io Help, Keyboard shortcuts (legacy)](https://help.frame.io/en/articles/7785-keyboard-shortcuts-legacy)
- The Frame.io player help page says J/K/L follows standard NLE behaviour — [Frame.io Help, Player page features](https://support.frame.io/en/articles/7786-player-page-features)
- In the new Frame.io panel for Premiere (beta), comments attach to sequence markers rather than the original source timestamp, so they stay with the right part of the edit — [Adobe Community announcement](https://community.adobe.com/announcements-732/now-in-beta-all-new-frame-io-panel-311901)

**JKL shuttle and transport (Premiere, Resolve, FCP, QuickTime)**
- In recent Premiere versions J/K/L are mapped to shuttle (reverse, stop, forward), and some users ask how to get back the older fixed-speed behaviour — [Adobe Community thread](https://community.adobe.com/t5/premiere-pro-discussions/j-k-l-keys-are-assigned-to-shuttle-but-used-to-be-playback-speed-how-do-i-change-it-back/m-p/9938004)
- In Premiere, tapping Shift+L repeatedly ratchets playback speed up in small steps ("Shuttle Slow Right/Left") — [ProVideo Coalition, Tool Tip Tuesday](https://www.provideocoalition.com/tool-tip-tuesday-for-adobe-premiere-pro-add-the-shift-key-to-step-playback/)
- In DaVinci Resolve, J/K/L (reverse/stop/forward) is a global shortcut — [Pixflow guide](https://pixflow.net/blog/davinci-resolve-keyboard-shortcuts/) (third-party guide)
- Resolve ships importable keyboard presets for Premiere Pro, Final Cut Pro 7 and Avid Media Composer. This shows that matching shortcut conventions across apps is treated as essential — [Storyblocks guide](https://www.storyblocks.com/resources/blog/davinci-resolve-keyboard-shortcuts)
- In Final Cut Pro, pressing J or L repeatedly speeds up rewind and fast-forward — [Tella definition page](https://www.tella.com/definition/jkl-editing) (low-authority, and not checked against Apple docs). A 2013 Duke page says JKL also works in QuickTime — [Duke DDMC](https://sites.duke.edu/ddmc/2013/10/31/quicktime-j-k-l-keyboard-shortcuts/)
- Avid MediaCentral documents the same J-K-L playback convention for web-based media review — [Avid MediaCentral UX guide](https://resources.avid.com/SupportFiles/attach/Interplay_Central/IPC_Help/InterplayCentral_Help/UG_Media.16.09.html)

**YouTube player conventions (the baseline most users know)**
- J and L seek 10 s back and forward. Left and Right arrows seek 5 s when the seek bar has focus. Keys 1–9 jump to 10–90% of the video and 0 jumps to the start — [YouTube Help, Keyboard shortcuts](https://support.google.com/youtube/answer/7631406?hl=en)
- While paused, comma steps back one frame and period steps forward one frame — [YouTube Help](https://support.google.com/youtube/answer/7631406?hl=en)
- In YouTube's new desktop layout the player must be clicked before shortcuts work. This focus trap is a known friction point — [YouTube Help](https://support.google.com/youtube/answer/7631406?hl=en)
- Note the conflict: on YouTube J/L means ±10 s jumps, while in NLEs and Frame.io it means shuttle.

**Scrub preview (thumbnails on hover)**
- Mux serves timeline hover previews as one storyboard sprite image plus a WebVTT (or JSON) file. Each cue maps a time range to a tile with an `#xywh=` fragment, for example `#xywh=0,0,256,160` — [Mux Docs, Create timeline hover previews](https://www.mux.com/docs/guides/create-timeline-hover-previews)
- Video.js has a `<media-thumbnail>` component that reads cues from `<track kind="metadata" label="thumbnails">` — [Video.js docs](https://videojs.org/docs/framework/html/how-to/show-timeline-thumbnail-previews). Media Chrome's `<media-preview-thumbnail>` appears on hover when that track is present — [Media Chrome docs](https://media-chrome-docs-4k9srq27o-mux.vercel.app/docs/en/components/media-preview-thumbnail)
- A Mux post (Nov 2026) says storyboard previews can show chapter titles and timestamps on timeline hover — [Mux blog](https://www.mux.com/blog/mux-robots-generated-thumbnails-and-chapters-straight-to-your-player)
- A step-by-step build of scrub-bar sprites using FFmpeg and WebVTT — [DEV Community](https://dev.to/masonwritescode/build-scrub-bar-thumbnail-previews-with-ffmpeg-and-a-webvtt-sprite-3ei2)

**Multicam angle viewer**
- In Premiere multicam, number keys 1–9 pick a camera, and Ctrl+number cuts to that camera during playback. Each choice made while playing is recorded as an edit — [Adobe Community thread](https://community.adobe.com/t5/premiere-pro-discussions/multi-camera-editing-switching-cameras/td-p/8493110)
- In Resolve, the source viewer in Multicam mode shows a thumbnail per camera, and you click one to switch. A 2018 thread found that the angle 1–9 shortcuts failed in 1x1 view and Next/Previous Angle shortcuts were the workaround — [Blackmagic Forum](https://forum.blackmagicdesign.com/viewtopic.php?p=420091); [Blackmagic Forum](https://forum.blackmagicdesign.com/viewtopic.php?p=547295)
- Premiere users report that angles sometimes "disappear" from the multicam source monitor, a recurring complaint thread — [Adobe Community](https://community.adobe.com/t5/premiere-pro/multicam-angle-disappears-from-source-monitor/m-p/10901423)

### Inferences
- **Adopt:** K or Space for play/pause. J/L as shuttle where repeat presses speed up (1x, 2x, 4x, 8x), with K+J / K+L for slow motion if feasible. Left/Right for ±1 frame and Shift+Left/Right for ±10 frames or ±1 s. Comma/period for frame steps (the YouTube habit). I/O to set the export range and Shift+I/O to jump to it. 1–4 to make a camera tile primary or full-size. 0 or Home to go to the start of the drive. This covers both the YouTube and NLE groups. If J/L becomes shuttle, show the current rate (for example "2× ▶") so YouTube users are not confused when it doesn't jump 10 s.
- **Adopt:** a hover scrub preview on the timeline that shows the front-camera frame plus the wall-clock time. DashLens works on local files, so it can create thumbnails on demand from a hidden `<video>` element and canvas. It doesn't need a server-built sprite sheet, though caching thumbnails the first time a clip loads follows the same idea as Mux storyboards.
- **Adopt:** Frame.io's link between a time-anchored note and the timeline. An "event" or user flag should show as a marker on the timeline and as a row in the list, and clicking either should seek. Range flags (I/O) are the natural basis for export.
- **Adopt:** the multicam pattern. Small thumbnails for every camera, one large "primary" view, number keys to switch. Avoid Resolve's quirk where shortcuts stop working in one view mode. Keys must work in every layout.
- **Avoid:** YouTube's "click the player first" focus trap. Make shortcuts global to the page, except inside text inputs.
- **Keyboard shortcut discoverability:** the cited tools all document shortcuts on separate help pages. Inferred: a "?" overlay and keyboard hints inside tooltips (for example "Play (K)") would make shortcuts easy to find without a help page. This is standard in web apps, but no source here confirms that the pro tools above do it in-app.

### Gaps
- Could not fetch the Frame.io V4 blog posts directly, so details of comment-marker styling, avatar "comment heads" on the timeline and the player chrome layout are unconfirmed.
- No official Apple (Final Cut Pro) or Blackmagic documentation came back for exact JKL speed steps or timeline zoom shortcuts. Conventions I know but did not verify, such as Cmd/Ctrl +/− to zoom the timeline, Shift+Z to zoom to fit, and pinch/Alt+scroll to zoom, are therefore not cited.
- Found nothing on NN/g, Vidstack or Plyr video-player UX guidance. No Netflix player specifics came back.
- No source found on timecode display formats (HH:MM:SS:FF and similar) in these tools.

## 2. Dashcam and car telemetry viewers: what exists, what users praise and complain about

### Takeaway
Leading dashcam viewers (BlackVue Viewer, Dashcam Viewer, Tesla's in-car and app viewer) share one layout: video, a map with a live position marker, speed and coordinates, a G-sensor line graph, and a filter by event type. The common complaints are about the basics: cameras out of sync, buggy scrubbing, no way to enlarge one camera, telemetry missing from exports, parking clips with no GPS, and unreliable Wi-Fi pairing.

### Cited Findings
**Tesla (firmware 2025.x)**
- The 2025 Holiday Update (2025.44.25) added telemetry to dashcam playback: speed, steering-wheel angle and Autopilot status are shown in the in-car and app viewers. Parked Sentry clips don't have this data because the sensors are shut off to save energy. Full app features need Premium Connectivity and app version 4.51.5 or later — [heise online](https://heise.de/-11112252) (summary only, page fetch failed)
- Tesla's Sentry viewer can filter clips by trigger type: All, Handle Pull, Panic, Manual Save, Honk, Emergency Brake, and in some builds "Aware". Tesla did not include this in the official 2025.44.25.1 notes — [heise online](https://heise.de/-11112252); [Drive Tesla Canada](https://driveteslacanada.ca/news/teslas-holiday-update-includes-undocumented-dashcam-storage-feature/)
- A Dashcam Storage Viewer (Safety menu) splits storage into Saved, Sentry and Recent — [Drive Tesla Canada](https://driveteslacanada.ca/news/teslas-holiday-update-includes-undocumented-dashcam-storage-feature/)
- 2025.20.x added pinch-to-zoom and pan in the Dashcam Viewer, plus multi-select delete. The newer viewer arrived in 2025.14 for Ryzen-based cars — [Yeslak blog](https://www.yeslak.com/blogs/tesla-news-insights/tesla-dashcam-viewer-update-zoom-feature) (community/vendor blog); [Not a Tesla App, 2025.20.x notes](https://www.notateslaapp.com/software-updates/version/2025.20.200/release-notes)

**Community TeslaCam viewers**
- TeslaCam Viewer II (Windows) plays all three cameras in sync based on recording time, with adjustable speed and keyboard shortcuts — [GitHub NateMccomb/TeslaCamViewer](https://github.com/NateMccomb/TeslaCamViewer)
- SentryDeck (Windows) uses one timeline with clips grouped by day, each showing a thumbnail, event reason and location — [SentryDeck via awesome.ecosyste.ms](https://awesome.ecosyste.ms/projects/github.com%2Fdanielchalmers%2Fsentrydeck)
- A browser-based TeslaCam Viewer offers a synced quad view when you drag the TeslaCam folder onto it, running in the browser like DashLens — [teslacam.pages.dev](https://teslacam.pages.dev/)
- An iOS "Dashcam Viewer" app decrypts and plays Tesla Dashcam/Sentry clips from USB with up to six camera angles in sync — [App Store](https://apps.apple.com/app/id1465175541). One reviewer said a clip looked wrong there but was fine in another viewer — [summary of App Store reviews](https://apps.apple.com/app/id1465175541)
- SentryCam was criticised as "only good as a viewer", with buggy scrubbing and no way to enlarge one camera's feed — [App Store, SentryCam](https://apps.apple.com/us/app/sentrycam/id1468682448)
- The tesla-dashcam project notes that clips for the same minute from the four cameras are not always the same length, which is a root cause of drift between cameras — [PyPI tesla-dashcam](https://pypi.python.org/pypi/tesla-dashcam)
- A Tesla Motors Club user reports the TeslaCam date stamp is correct but the time is off by hours (likely a timezone issue, cause not stated) — [TMC thread](https://teslamotorsclub.com/tmc/threads/teslacam-time-stamp-always-wrong.163874/)

**BlackVue Viewer (official manual)**
- The layout has the playback screen, a map panel with speed and coordinates shown above the map, and a G-sensor line graph over the timeline — [BlackVue manual DR750X](https://manual.blackvue.com/docs/dr750x-2ch/playing-and-managing-videos/using-your-computer-windows-macos-dr750x-2ch/); [BlackVue manual DR590X](https://manual.blackvue.com/docs/dr590x-2ch/playing-and-managing-videos/new-using-your-computer-windows-macos-dr590x-plus-series/)
- Parking-mode recordings show no map data because GPS isn't recorded in parking mode — [BlackVue manual](https://manual.blackvue.com/docs/dr750x-2ch/playing-and-managing-videos/using-your-computer-windows-macos-dr750x-2ch/)
- A file filter separates E (event) and I (impact while parked) files. Event types include impact, overspeed, hard braking and geofence. Event recordings start 5 seconds before the trigger — [BlackVue manual](https://manual.blackvue.com/docs/dr590x-2ch/playing-and-managing-videos/new-using-your-computer-windows-macos-dr590x-plus-series/)
- Controls include play/pause, next frame, playback speed and full screen. The viewer can also format the microSD card — [BlackVue manual](https://manual.blackvue.com/docs/dr750x-2ch/playing-and-managing-videos/using-your-computer-windows-macos-dr750x-2ch/)

**Dashcam Viewer (dashcamviewer.com, third-party, 140+ camera models)**
- It shows a live map of location, speed and route. The map auto-pans to keep the vehicle centred, with an option to keep the map fixed — [Dashcam Viewer user manual (J.J. Keller edition, PDF)](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/50106/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf)
- Speed appears in a heads-up display and in graphs. The route line and speed traces are colour-coded by speed. It can graph speed, distance, bearing, G-force and altitude — [Dashcam Viewer manual](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/50106/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf); [Softpedia listing](https://www.softpedia.com/get/Multimedia/Video/Other-VIDEO-Tools/Dashcam-Viewer.shtml)
- The free tier loads only 2 videos at a time — [Softpedia listing](https://www.softpedia.com/get/Multimedia/Video/Other-VIDEO-Tools/Dashcam-Viewer.shtml)
- Complaints: exported video can't include the sensor data as an overlay, and G-sensor data wasn't read on one BlackVue model — [user reviews summarised via Softpedia / SourceForge](https://sourceforge.net/app/dashcam-viewer/mac/)

**Brand phone/Wi-Fi viewers (Thinkware, Nextbase, Momento)**
- Thinkware's iOS Dashcam Viewer works only with certain models (X350/F750/F770/FA700). Reviews call it buggy and say Wi-Fi connection is hard. iOS 13 broke SSID detection when location permission is off — [App Store, Thinkware Dashcam Viewer](https://apps.apple.com/us/app/dashcam-viewer/id962249167)
- Nextbase Cam Viewer reviews describe an endless cycle of failed Wi-Fi connections and an app not updated in years — [App Store, Cam Viewer](https://apps.apple.com/us/app/cam-viewer/id1088562776)

**Telemetry overlay / racing tools**
- Telemetry Overlay imports GoPro, Insta360, DJI, RaceChrono CSV, GPX, CSV and KML. It has a "Sync Telemetry" control with a start or end anchor, and it can export a transparent gauge-only video — [Telemetry Overlay manual (manuals.plus)](https://manuals.plus/GoPro/telemetry-overlay-manual); [Product Hunt](https://www.producthunt.com/posts/telemetry-overlay)
- GoPro Quik's desktop gauge feature is treated as legacy and reportedly doesn't work for Hero 8. RaceChrono users complain about duplicate video files and gauges that aren't as well synced when routed through other tools — [surfski.wiki GoPro gauges](https://mail.surfski.wiki/gopro_gauges); [RaceChrono forum](https://racechrono.com/forum/discussion/comment/13672/)
- Garmin Catalyst 2 overlays track map, speed, delta time and a G-G traction-circle diagram on 1440p video — [Competition Motorsport](https://competitionmotorsport.com/blogs/tech-product-info/garmin-catalyst-2-smaller-and-better); [AutoGuide](https://cdn-fastly.autoguide.com/auto/garmin-launches-catalyst-2-track-driving-coach-with-built-in-camera-44630233)
- Catalyst can play short clips of the same corner over successive laps, either full-screen or next to a speed graph — [Hagerty review](https://www.hagerty.com/media/motorsports/review-garmin-catalyst/). 2021 forum users wanted side-by-side video and speed-trace comparison and found deep metric review hard — [Grassroots Motorsports forum](https://grassrootsmotorsports.com/forum/grm/garmin-catalyst/182436/page1)

### Inferences
- **Adopt (table stakes):** synced cameras with one primary tile that can be enlarged, a map with a live marker and an auto-follow toggle, speed and coordinates next to the map, a G-sensor lane aligned with the timeline, and an event-type filter. Each of these is either a core feature of the market leaders or a named complaint when it's missing.
- **Adopt:** a filter by trigger/event type and a Saved/Event/Parking split, matching Tesla and BlackVue. Show the plain trigger name ("Hard braking", "Impact while parked") rather than file-letter codes (E/I).
- **Adopt:** an explicit empty state for parking clips without GPS, such as "No GPS while parked – the camera does not record location in parking mode". Both BlackVue and Tesla behave this way, and a blank map reads as a bug.
- **Adopt:** sync by wall-clock timestamps, not by file start, and handle clips of unequal length. Show a small per-camera sync offset control (similar to Telemetry Overlay's Sync Telemetry) for when the camera clocks disagree.
- **Adopt:** timezone handling for timestamps, showing the source timezone and letting the user correct it, given the TMC "off by hours" complaint.
- **Differentiate:** burn the telemetry (time, speed, GPS) into exported clips as an option. Dashcam Viewer users specifically miss this.
- **Avoid:** limiting the number of loaded clips (Dashcam Viewer free tier: 2), and anything that needs pairing with the device.
- **Enthusiast extra (low priority):** a G-G (friction-circle) plot next to the G-sensor line chart, following Catalyst.

### Gaps
- No usable results for Rivian's Gear Guard/dashcam viewer, Viofo's desktop player, Nextbase's desktop player (Nextbase Player / MyNextbase), Garmin Drive/Vault desktop playback, or Track Attack.
- Reddit (r/Dashcam, r/TeslaMotors) and DashCamTalk threads did not appear in any search, so the complaint list is limited to App Store and forum excerpts.
- Could not confirm the official dashcamviewer.com feature page directly. The details come from a licensed manual edition and listings.

## 3. Map + video sync, speed/G-force visualisation, event flagging, and evidence export for insurance or police

### Takeaway
The proven sync pattern is two-way: the map marker follows the playhead, the map auto-pans unless the user pins it, and the route or speed trace is colour-coded by speed. For evidence, the consistent advice is to keep the original untouched file, give a hash for the original and any copy, export GPS separately (GPX), and send a playable working copy next to the native master.

### Cited Findings
- Dashcam Viewer's map auto-pans to keep the vehicle centred, with a "keep map fixed" option. The route line and speed graph are colour-coded by speed — [Dashcam Viewer manual](https://cdn.jjkeller.com/wcsstore/CVCatalogAssetStore/samples/50106/Dashcam-Viewer-Users-Manual-JJ-Keller.pdf)
- BlackVue displays speed and coordinates above the map during playback, plus a G-sensor line graph over time — [BlackVue manual](https://manual.blackvue.com/docs/dr750x-2ch/playing-and-managing-videos/using-your-computer-windows-macos-dr750x-2ch/)
- Tesla overlays speed, steering angle and Autopilot state during playback, and filters clips by trigger type — [heise online](https://heise.de/-11112252)
- BlackVue event recordings include 5 s before the trigger. This pre-roll convention matters when DashLens auto-sets export ranges around events — [BlackVue manual](https://manual.blackvue.com/docs/dr590x-2ch/playing-and-managing-videos/new-using-your-computer-windows-macos-dr590x-plus-series/)
- **Evidence:** courts prefer the original file from the SD card over an exported clip. Avoid compressing, trimming or converting the master, and check cloud transfer didn't re-encode it — [Nexar, why dash cam footage is rejected](https://www.getnexar.com/blog/why-dash-cam-footage-rejected-as-evidence); [Nexar, small-claims court](https://www.getnexar.com/blog/dash-cam-footage-small-claims-court) (vendor blogs)
- Note the MD5 hash of the original before sharing. NIST-style verification compares the hash of the original and the copy — [DEV Community, chain of custody](https://dev.to/craig_solomon/chain-of-custody-for-digital-evidence-how-to-prove-your-video-wasnt-faked-56dg) (individual author, not authoritative)
- Recommended package: the native file (with its player) as the master, plus a playable working copy, with a hash recorded for each — [Spot AI, video evidence packages](https://www.spot.ai/blog/video-evidence-packages-police-insurers-attorneys) (vendor blog)
- Compare the footage timestamp with the police or claim timeline. A different "Modified" date is not necessarily a problem but should be noted. Exporting GPS as GPX supports independent analysis — [Nexar, reading timestamps and GPS](https://www.getnexar.com/EN-US/blog/how-to-read-dash-cam-timestamps-gps-data)
- Police may take the SD card. Ask for a receipt and a return estimate, and give a copy rather than the original where possible — [Nexar, police investigation process](https://www.getnexar.com/EN-US/blog/dash-cam-footage-police-investigation-process)
- Timing and authentication are the core dispute issue for video in claims — [DEV Community, video evidence timing](https://dev.to/craig_solomon/video-evidence-in-disputed-claims-why-footage-timing-is-the-authentication-problem-4lbl)
- Blackboxmycar advises against "AI enhancement" of original dashcam footage meant for evidence — [BlackboxMyCar blog](https://www.blackboxmycar.com/blogs/news/ai-dash-cam-enhancement-original-footage) (vendor blog, title only seen)
- Academic dashcam forensics work (DFRWS) exists on recovering and analysing dashcam data — [DFRWS paper (Lallie)](https://dfrws.org/wp-content/uploads/2023/07/lallie-dashcamforensics.pdf) (not read in detail)

### Inferences
- **Adopt:** the map marker follows the playhead, clicking the route seeks the video, and a follow/pin toggle. Colour the route by speed using one sequential ramp (not a rainbow), with a legend, so it stays readable without relying on colour alone.
- **Adopt:** data lanes under the timeline (speed, G-force), drawn on the same time axis as the clip rows so the playhead crosses all of them. This is the "waveform lane" idea from NLEs applied to telemetry. Mark G-sensor spikes above a threshold as event markers.
- **Adopt for evidence export:** (1) "Export original files" that copies the source files byte for byte, never re-encoded. (2) A separate "working copy" clip, which may be trimmed or overlaid and is clearly labelled as derived. (3) A SHA-256 (optionally MD5 too, since guides mention it) for every original and derived file, computed in the browser with Web Crypto. (4) A manifest or incident summary listing filenames, sizes, hashes, camera, recorded start/end times, timezone, GPS points and the export time and tool version. (5) GPX/CSV export of the track. (6) Wording that says DashLens never modifies the originals.
- **Avoid:** calling a trimmed or re-encoded clip "the evidence". Avoid enhancement filters on evidence exports. Avoid claiming legal admissibility, since all sources are vendor guidance, not law.
- **Event pre-roll:** when the user exports "around this event", default to a few seconds before (BlackVue uses 5 s) and some after, and show the range on the timeline before export.

### Gaps
- No authoritative (police, insurer or standards body) guidance was retrieved. The evidence advice comes from vendors and individual authors. The SWGDE or NIST primary documents were not fetched.
- Found no dashcam viewer that already produces a hashed evidence manifest. This appears to be an open opportunity, but the absence isn't proven.

## 4. What makes these tools feel "pro": density, precision, keyboard-first, neutral grey UI

### Takeaway
"Pro" comes from precision (frame-accurate seek, frame and 10-frame steps, exact in/out), a keyboard grammar shared across apps, and a neutral, untinted dark-to-mid grey interface so colour in the UI doesn't bias how the footage looks. Colour is kept for meaning such as markers and states. The 18% grey convention is practitioner lore, not hard science, and some users find dark-on-charcoal tiring, so contrast still matters.

### Cited Findings
- Surrounding colour changes how footage colour is perceived. Grading workspaces avoid unusual colours and extreme brightness. A dark UI makes colours look punchier, so neutral grey is preferred for judging colour — [Envato Tuts+, neutral grey themes in Photoshop/Lightroom](https://photography.tutsplus.com/tutorials/want-better-color-use-neutral-gray-themes-in-adobe-photoshop-and-lightroom--cms-23342)
- 18% / middle grey is the conventional neutral for colour-correction suites, for both the interface and the walls — [Frame.io Workflow Guide, colour correction suites](https://workflow.frame.io/guide/color-correction-suites); [Envato Tuts+](https://photography.tutsplus.com/tutorials/want-better-color-use-neutral-gray-themes-in-adobe-photoshop-and-lightroom--cms-23342)
- A KDE forum post objects that a default dark theme has a "distinct blue tint" that is a problem for grading. Neutrality matters, not just darkness — [KDE Discuss, built-in gray theme](https://discuss.kde.org/t/built-in-gray-theme/45385)
- Premiere users ask for a light UI for bright rooms, and some say dark grey on charcoal causes eye strain — [Adobe Community, light mode UI interest gauge](https://community.adobe.com/questions-729/premiere-pro-interface-color-light-mode-ui-interest-gauge-1349360); [Adobe feature request, white UI for grading](https://community.adobe.com/feature-requests-730/similar-to-lightroom-add-a-white-ui-option-to-help-color-grading-1329257)
- Frame.io V4's selling points are frame-accurate seeking with per-frame hover preview and 1:1 frame guides. These are precision features, not decoration — [Frame.io blog 2024-05-28](https://blog.frame.io/2024/05/28/frame-io-v4-features-player-and-commenting/); [Frame.io blog, redesigned player](https://blog.frame.io/?p=4451)
- Keys give more precise scrubbing than a pointer, including frame-by-frame — [freeCodeCamp / summary of YouTube shortcut guides](https://www.freecodecamp.org/news/youtube-keyboard-shortcut-hotkey-list-repeat-speed-subtitles/)
- Pro tools invest in keyboard portability, for example Resolve shipping Premiere, FCP and Avid key presets — [Storyblocks](https://www.storyblocks.com/resources/blog/davinci-resolve-keyboard-shortcuts)

### Inferences
- **Adopt:** a neutral (zero-chroma, or very low chroma) dark grey around the video tiles, with no blue tint. Keep saturated colour for event markers, the playhead and the single accent. The footage should be the most colourful thing on screen. That helps users judge things like traffic-light colour and vehicle colour, which matters in incidents.
- **Adopt:** dense but legible telemetry. Use tabular (monospaced) figures for time, speed and coordinates so digits don't shift as they change. Show units, and give wall-clock time with seconds (and frame or ms when paused).
- **Adopt:** a light theme or high-contrast option, given the eye-strain complaints. Meet WCAG contrast rather than going for an ultra-dark look.
- **For the stressed owner:** pro density should not get in the way of a plain path (load the card, see events, export evidence). A progressive-disclosure layout, with simple defaults and pro controls revealed on demand, reconciles the two user groups. This is an inference, not sourced.

### Gaps
- No controlled study found showing that a neutral grey UI changes judgement of footage colour. Evidence is practitioner convention.
- No design case study found (Frame.io design blog or similar) that states the grey values or design-token rationale behind V4.
