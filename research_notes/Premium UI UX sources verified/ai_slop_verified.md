# AI-slop UI tells: the earlier notes checked against primary sources

Checked on 2026-11-26 against `research_notes/Premium UI UX for DashLens/ai_slop_tells.md`. Labels used below:
- **CONFIRMED**: the primary source says this. A short exact quote follows.
- **CORRECTED**: the source says something different. The correct version follows.
- **NOT FOUND**: the page loaded but the claim is not in it.
- **NOT VERIFIED**: the page could not be loaded from this session (HTTP 403, or the host is not allowed).

These hosts were still unreachable:
- searchengineland.com, uxdesign.cc and designsystemscollective.com: DNS blocked by session network rules
- northeasttimes.com, microsoft.com/research and gettyimages.com: HTTP 403
- x.com: not tried

## 1. Adrian Krebs's original post: method, number of sites, percentages, list of tells

### Takeaway
The post exists and was revised after it was published. The first version (19–20 Apr 2026) scored **500** Show HN pages against **15** patterns and reported heavy 21% (5+ patterns), mild 46% (2–4) and clean 33% (0–1). The current version scores **1,590** pages against **16** patterns, with new tier thresholds: high 22% (4+), medium 32% (2–3) and low 46% (0–1). Both sets of numbers in the earlier notes were real. They come from different versions of the same post, not from conflicting sources.

### Cited Findings
**The post itself**
- Title and date: "Scoring Show HN submissions for AI design patterns", Apr 20, 2026. — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)
- GIGAZINE links to the post under an earlier title, "Show HN submissions tripled and now mostly share the same vibe-coded look". — [GIGAZINE](https://gigazine.net/gsc_news/en/20260423-design-slop/)
- Where the tells came from: designers, not data. "A designer recently told me that 'colored left borders are almost as reliable a sign of AI-generated design as em-dashes for text'… Then I asked some more designer friends what they think are common AI patterns." — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)
- Method, CONFIRMED: "A headless browser loads each site (Playwright)… A small in-page script analyzes the DOM and reads computed styles… Every pattern is a deterministic CSS or DOM check. I intentionally do not take screenshots and let the LLM judge them." He estimates false positives from a manual QA run at "maybe 5-10%". — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)

**The current list of tells, CONFIRMED** — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)

| Group | Tells |
|---|---|
| Fonts | "Inter used for everything, but especially the centered hero headlines"; Space Grotesk, Instrument Serif and Geist combos; "Serif italic for one accent word in an otherwise-Inter hero" |
| Colors | "VibeCode Purple"; "Perma dark mode with medium-grey body text and all-caps section labels"; "Barely passing body-text contrast in dark themes"; "Gradient everything"; "Large colored glows and colored box-shadows" |
| Layout | centered generic-sans hero; "Badge right above the hero H1"; colored top or left card borders; identical icon-topped feature cards; numbered "1, 2, 3" steps; stat banner rows; sidebar or nav with emoji icons; all-caps headings and labels |
| CSS | shadcn/ui; glassmorphism |

**Current numbers, CONFIRMED**
- "I scored 1,590 Show HN submissions… High (4+ patterns): 22% (347 sites) · Medium (2-3 patterns): 32% (508 sites) · Low (0-1 patterns): 46% (735 sites)". The tiers are "based on how many of the 16 patterns they trigger". — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)
- The same post also says "~1400 Show HN pages" in its method section, so the text is internally inconsistent. — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)
- Two secondary sources repeat the current numbers:
  - "Adrian Krebs scored 1,590 Show HN pages: 22% heavy, 32% mild, 46% clean." — [Developers Digest](https://www.developersdigest.tech/series/ai-tools-deep-dive)
  - "about 1,600 … 22% in the heavy band (four or more patterns)". — [maxiality](https://maxiality.com/how-to-spot-an-ai-generated-website/)

**First-version numbers, CONFIRMED in two places**
- The HN submission on Apr 19 was titled "Scoring 500 Show HN pages for AI design slop". — [HN 47825004](https://news.ycombinator.com/item?id=47825004)
- dang quoted the original figures in the main thread: "Heavy slop (5+ patterns) · 105 sites · 21% / Mild (2–4) · 230 sites · 46% / Clean (0–1) · 165 sites · 33%". — [HN 47864393](https://news.ycombinator.com/item?id=47864393)
- GIGAZINE (Apr 23) reports "15 such 'AI-like elements'… in 500 posts" and gives a rate for each pattern. — [GIGAZINE](https://gigazine.net/gsc_news/en/20260423-design-slop/)

**Rate of each pattern in the first version** (from GIGAZINE; none of these rates appears in the current post's text):

| Pattern | Share of 500 sites |
|---|---|
| Gradients | 28% |
| shadcn/ui left at its defaults | 23.5% |
| Centered title | 23.5% |
| Perma-dark (dark background, grey text, uppercase labels) | 20.3% |
| Templated icon-card grid | 20.1% |
| Glass panels | 17.1% |
| "AI fonts" (Space Grotesk, Instrument Serif, Geist, Syne, Fraunces) | 15.8% |
| Colored card stripe | 13% |
| Stat banner | 12.2% |
| Purple CTA | 10.7% |
| All-caps labels | 10.5% |
| Numbered steps | 9.4% |
| Pill badge above the title | 4.7% |
| Colored box shadow | 4.3% |
| Emoji in nav | 3.8% |

**Author's verdict and later tools**
- "Is this bad? Not really, just uninspired… before the AI era, everything looked like Bootstrap." — [Krebs](https://www.adriankrebs.ch/blog/design-slop/)
- He later released a scanner, "Design Slop Cop". — [HN 48821493](https://news.ycombinator.com/item?id=48821493) → slopcop.adriankrebs.ch
- slop-detect now credits Krebs with "original AI-design-slop study #1–14". Its README no longer contains the "~1,400 submissions, 67%" claim: NOT FOUND. — [slop-detect](https://github.com/ravidsrk/slop-detect)

### Inferences
- The "67%" in the earlier notes probably equals 21% heavy plus 46% mild from the first version. It is not a separate finding.
- The pill badge was the most memorable example, yet it was one of the rarest patterns (4.7%). The most common patterns were gradients, default shadcn, a centered hero, perma-dark with grey text, and the icon-card grid.
- Perma-dark (20.3%) is the pattern closest to DashLens. Krebs's version of it is specifically dark, plus medium-grey body text, plus all-caps section labels. A dark background on its own is not the pattern.

### Gaps
- No pre-2023 baseline exists, so these rates cannot show that AI caused the patterns. An HN commenter (raincole) points this out.
- The current post's rate for each of the 16 patterns may be in its charts. Only the text was readable, and the 16th pattern is not named in the text.

## 2. Hacker News discussions: tells most commenters agree on, and the counter-opinions

### Takeaway
Agreement is broad on three things: defaults used without any change, decoration that carries no meaning ("busy-ness"), and low contrast. The objections are just as consistent:
- many of the tells predate AI and come from Tailwind UI and shadcn
- the list is based on designers' impressions plus a frequency illusion
- every model has its own style, and the style changes over time

By mid-2026 commenters were saying the default had moved from purple to beige/cream with an orange or terracotta accent.

### Cited Findings
**Krebs thread** (333 points, 235 comments) — [HN 47864393](https://news.ycombinator.com/item?id=47864393)

Agreement:
- joegibbs: "AI definitely does seem to want to add coloured left borders, tags and superfluous numbers all over the place".
- computerphage, on barely passing contrast: "these vibe coded UIs are basically unreadable to my eyes".
- dematz: "a big unmentioned one is a grid of rounded rects".

Counter-opinions:
- michaelcampbell: "so, n=1 plus Baader-Meinhof?"
- nomdep: "design patterns that were already very common before AI… You can blame most of them on TailwindUI and shadcn."
- raincole: the author "didn't use the same 'slop score' to measure Show HN posts from <2023".
- deaux: "half the stuff in there is already outdated. Models have their own archetypes… almost every vibecoded website is Opus".
- ChrisArchitect: "it's not the Tailwind purple anymore… more of the same beige scheme this very blog post is using".
- flexagoon, on the fonts: "They may be somewhat overused but they are popular for a reason".
- kykat and richard_chase: they used colored borders before AI.
- tptacek: "AI-generated look-feel and web design is basically fine".

**Jim Nielsen "The AI Aesthetic" thread** (378 points, 176 comments) — [HN 49117099](https://news.ycombinator.com/item?id=49117099)

Agreement:
- jjcm, who worked on AI tooling at Figma: "LLMs write code to represent designs as well, which means you get consistent designs. You end up aligning on a generic mean".
- TheOtherHobbes: "Busy-ness is a key tell… most of it is decoration for the sake of distraction."
- smoe: "the AI aesthetic is the opposite of utilitarian. It adds so much unnecessary bits and bobs".
- yieldcrv: "loooooooooooong landing pages is a sure tell".
- monk_grilla: the "cream serif with orange highlight look" was on "every other vibe-coded website".

Counter-opinions:
- paxys: "This is mostly just the 2010-2024 SaaS aesthetic."
- ValentineC: beige/cream with orange accents is "literally the HN design".
- cyanregiment: "I have not noticed 'orange' as a particular AI trend."
- aetherspawn and strictnein prefer the small icons.

**"Ask HN: How can you tell a site/app is vibe coded?"** (9 points, 9 comments) — [HN 49290499](https://news.ycombinator.com/item?id=49290499)
- The asker: "Black background, green and orange gradients, same font".
- roundabout-host: "Inter font. Corners are usually quite rounded… lots of gradients… weird descriptions of what a particular UI element does, even though it's obvious".
- One commenter (Wpnx330) lists: "the dark background offset glow, thick boarders, flat display style, over use of techy color schemes like navy blue… and emojis in headers".
- wbnns: "em dashes all throughout the content".

**"Color palette gives away AI slop"** (May 2026, 3 points) — [HN 48269907](https://news.ycombinator.com/item?id=48269907)
- The poster lists "Editorial layout · Cream canvas · Cobalt or Terracotta ink · Persimmon or Coral signal · Mono font".

### Inferences
- Strongest agreement: unchanged defaults, decoration without meaning, low-contrast grey text, sameness. Disputed: individual fonts, colored borders, and shadcn as a tell.
- HN sentiment on design itself is mixed. Many commenters care more about whether the substance was vibe-coded than about how it looks.

### Gaps
- None of these threads is a representative survey. Vote counts only measure interest.

## 3. Jim Nielsen; Impeccable (Paul Bakaus); Anthropic's frontend-design skill and its Nov 2025 article

### Takeaway
All three are CONFIRMED and current. Anthropic's SKILL.md currently lists five clusters of AI-generated design. Cluster 2 is "a near-black background with a single bright acid-green or vermilion accent". Cluster 5 includes "tinted near-black (#0B0B0B, #111)", "a monospace face for small data labels" and "a tracked-out ALL-CAPS eyebrow label above every heading". The skill also says: "All traits are legitimate for some briefs, but they are defaults rather than choices." Impeccable now has 62 detector rules. One of its rules says to keep a dark theme when it suits the product, but to cut the glow.

### Cited Findings
**Jim Nielsen, "The AI Aesthetic" (Jul 29, 2026). CONFIRMED.** — [Nielsen](https://blog.jim-nielsen.com/2026/ai-aesthetic/)
- "There are other aesthetics my brain associates with AI, like beige/cream colors, orange accents, and serif typefaces as well as whack-a-mole UI controls".
- Other idioms he names: the sparkle emoji ("now it means AI"), "shimmering text" for async work, and tiny icons.
- CORRECTION: the earlier notes said an HN thread tied the cream/orange look to the Claude, Codex and Cursor apps. In fact Nielsen himself names those apps, and he names them for *tiny, thin icons*, not for cream/orange: "desktop AI apps on the left (Claude, Codex, Cursor)… have much smaller, thinner icons than their native counterparts."
- NOT VERIFIED (403): the Kyle Chayka/New Yorker quote reported through Northeast Times.

**Anthropic SKILL.md, current text. CONFIRMED.** — [anthropics/skills frontend-design](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)

The five clusters, quoted exactly:
1. "a warm cream background (near #F4F1EA) with a high-contrast serif display and a terracotta or warm-clay accent (often near #D97757 — Anthropic's own Claude-interaction accent, so on a user's brief it reads as a tell)"
2. "a near-black background with a single bright acid-green or vermilion accent"
3. "broadsheet-style layout with hairline rules, zero border-radius, and dense newspaper-like columns"
4. "the SaaS-card kit… one border-radius on everything… the same soft grey shadow (rgba(0,0,0,.1))… gradient washes"
5. "template chrome… a tracked-out ALL-CAPS eyebrow label above every heading; meta strings joined with middle dots ('A · B · C'); labels built as 'WORD — fragment' with a spaced em dash; tinted near-black (#0B0B0B, #111) standing in for black; a monospace face for small data labels; a '→' appended to link and button text."

Also confirmed in the same file:
- The typographic tells: "Accenting just a single word…", "Using all caps for labels", "Adding unnecessary typographic labels above content".
- On the hero: "a big number with a small label, supporting stats, and a gradient accent is the default treatment".
- On motion: "fade-and-slide-up entrances on each section and hover transitions on every card are the generic default and read as AI-generated".
- On restraint: "Spend your boldness in one place."

Version note: the GitHub commit history could not be read (API access was denied), so the date these clusters were added is unknown.

**Anthropic article, "Improving frontend design through Skills" (November 12, 2025). CONFIRMED.** — [claude.com](https://claude.com/resources/articles/improving-frontend-design-through-skills)
- "it will almost always conform to Inter fonts, purple gradients on white backgrounds, and minimal animations."
- "Distributional convergence… Without direction, Claude samples from this high-probability center."
- Its prompt says: "Never use: Inter, Roboto, Open Sans, Lato, default system fonts".
- It lists "Code aesthetic: JetBrains Mono, Fira Code, Space Grotesk" as *recommended* fonts.
- It also says the model converges on "Space Grotesk, for example".

**Impeccable** — [impeccable.style/slop](https://impeccable.style/slop); [README](https://raw.githubusercontent.com/pbakaus/impeccable/main/README.md)
- Rule count, CORRECTED: the earlier notes gave 25, 37 or 58 rules. The README now says "62 deterministic rules", and the slop page says "62 detector rules and 6 patterns for design review". Of the 68 catalog entries, 37 are labelled "AI slop". An HN commenter cited 59.
- "Cyan-on-dark", CONFIRMED as the rule "AI color palette": "Purple gradients and bright cyan on dark backgrounds are familiar AI defaults."
- "Dark mode with glowing accents": "Keep the dark theme if it suits the product, and reduce the glow so useful information stands out."
- Also CONFIRMED:
  - "Bounce or elastic easing"
  - "Monotonous spacing": "Equal gaps everywhere make it hard to tell what belongs together."
  - the "Modal Abuse" example
  - "Overused font": "Inter and Geist"
  - "Cream / beige palette"
  - "Icon tile stacked above heading"
  - "Badge above the main headline"
  - "Hero metric layout"
  - "Tiny numbered section labels"
  - "Em-dash overuse"
  - "Hairline border with wide shadow"
  - "Side-tab accent border"
- NOT FOUND: "every button styled as primary". It is not in the current catalog.
- NOT FOUND: "fingerprints of generic 2024–25 AI work". The Mintlify docs page the earlier notes cited now returns HTTP 410 "Page gone".
- The slop page groups tells by era tabs: "2022 / 2025 / 2026". The 2022 tab is "Purple gradients, glass panels, neon glow".
- Latent Space, CONFIRMED: "Impeccable began as a relatively simple extension of Anthropic's frontend design skill." Bakaus: "[models] converge in one direction, and if everybody uses the same skill… everything ends up looking the same." — [Latent Space](https://www.latent.space/p/skill-engineering-design)
- NOT FOUND in that article: the earlier claim "prohibitions work better than 'create good design'". In practice, though, every Impeccable rule pairs the problem with a fix.

### Inferences
- **DashLens's palette is close to Anthropic's cluster 2.** Vermilion is a red-orange, so near-black plus one bright orange is a near match. Using #0B0B0B or #111 as the base, mono data labels and all-caps eyebrows would complete cluster 5.
- **The way out is in the skill's own wording.** These traits are "defaults rather than choices". A video viewer has a real reason to be dark.
- **What has to show the choice was made:**
  - true surface steps rather than one tinted near-black
  - orange used only to mean "active" or "now", with no glow
  - mono used only for real tabular telemetry
  - no eyebrows, middle-dot meta strings or "→" on buttons

### Gaps
- I found no source that tests whether *users* (as opposed to designers) read dark-plus-one-accent as AI-made.

## 4. Articles on AI design sameness (uxdesign.cc, dev.to, Smashing, CSS-Tricks, Mintlify, NN/g) and the Tailwind indigo-500 origin

### Takeaway
NN/g's primary article (Oct 24, 2025) CONFIRMS the generic look. It traces it to training data and to defaulting to shadcn and Tailwind. It also describes the default as "neutral, minimalistic visual aesthetics with bright color accents". The indigo-500 story is a real joke tweet by Adam Wathan (Aug 2025), but no source shows the causal chain. Smashing and CSS-Tricks have no dedicated article on this topic. The uxdesign.cc posts could not be reached.

### Cited Findings
**NN/g, "AI Prototyping" (October 24, 2025; last reviewed Aug 19, 2026). CONFIRMED, primary.** — [NN/g](https://www.nngroup.com/articles/ai-prototyping/)
- "AI prototyping tools tend to output designs that share a similar, generic look using sans-serif typeface and minimalistic styling. This homogeneity is largely because AI systems favor common patterns from their training data and often default to component libraries like Shadcn and front-end frameworks like Tailwind CSS".
- "That bias could potentially be good for the user experience".
- "default to neutral, minimalistic visual aesthetics with bright color accents".
- Second-hand quotes from uxcel are partly checked. "don't confuse visual fidelity with design quality" and "established design styles or frameworks instead of using generic visual descriptions like simple, clean, and modern" are attributed to NN/g. — [uxcel](https://uxcel.com/lessons/directing-taste-011)

**Tailwind indigo-500 origin** — [dev.to alanwest](https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p); [AIbase](https://news.aibase.com/news/20365); [Product Hunt](https://www.producthunt.com/p/vibecoding/an-accidental-choice-a-butterfly-effect-and-the-future-of-ai-aesthetics)
- The dev.to post (Mar 2026) says: "In August 2025, Adam Wathan… posted a semi-apologetic tweet that got over a million views… sorry for making every button in Tailwind UI use bg-indigo-500 five years ago".
- AIbase dates the tweet to Aug 7, 2025 and gives about 684k views. The view count is therefore disputed.
- Product Hunt says Wathan "joked" about it.
- The tweet itself was not read. Status: the tweet is CONFIRMED by secondary sources. The causal claim is unproven; Wathan made it as a joke.

**dev.to and other secondary articles**
- dev.to kenimo49, CONFIRMED but weak: "95.4% clustered around 240° (blue-purple)". The sample is only "AI-generated UI samples", with no size or method given. — [dev.to](https://dev.to/kenimo49/why-ai-generated-uis-are-all-the-same-color-and-the-data-to-prove-it-12oe)
- dev.to alanwest, fix post: "The 'AI look' isn't really about AI. It's about defaults." — [dev.to](https://dev.to/alanwest/how-to-fix-the-ai-generated-look-in-your-frontend-1ahh)
- CORRECTED attribution: the line "Lovable, v0, and Claude Code all ship with the same defaults: Inter, shadcn components, Lucide icons, and Tailwind spacing" is from foundey, which cites SaaStr. It is not from the dev.to fix post. — [foundey](https://foundey.com/blog/ai-slop-icons)
- Kosta Canatselis (Jul 23, 2026), CONFIRMED: "Slop is design with no author. It's the statistical average of ten thousand interfaces". His tells are Inter, the purple-to-blue gradient, "Cards with the same corner radius everywhere", "That damn left-edge coloured line", missing empty/loading/error states, and "Everything visible at all times". — [HEY](https://world.hey.com/kostac/spot-the-slop-a-ui-designer-s-guide-to-fixing-ai-defaults-4c448c9c)
- Built In, CONFIRMED: "The baseline for acceptable design has quietly shifted to whatever AI produces." — [Built In](https://builtin.com/articles/ai-design-slop-era)
- arXiv "Design Theater" (Jul 2026, AAAI/AIES), CORRECTED. The paper's main finding is about rationale. It studied 120 interfaces from 5 tools and found that "over 25% of user-facing design rationales are not implemented". Sameness is a secondary finding: "convergence in visual appearance and layout organization, with greater variation in color choices". — [arXiv 2607.22928](https://arxiv.org/abs/2607.22928)

**IOV Labs paper, via maxiality** (newly found)
- CORRECTED: the critique the earlier notes attributed to Krebs's study actually targets this paper. "thresholds were tuned on the same 202 sites" refers to a June 2026 IOV Labs paper with 27 tells.
- Its counterpoint: "brand purple is not a tell, since Stripe uses it heavily and scores 0. Neither is Inter… what gives a page away is defaults with nothing deliberate next to them." — [maxiality](https://maxiality.com/how-to-spot-an-ai-generated-website/)

**21st.dev and MindStudio**
- 21st.dev (Aug 2026), CONFIRMED: "A face nobody else in your space uses, paired with something plain", a claim "that could only be about you", and "Show the product… the fastest single change available". — [21st.dev](https://21st.dev/blog/website-not-look-ai-generated)
- 21st.dev, CORRECTED: the claim that "scroll animations are the fastest way to look AI-generated" is NOT FOUND. "Fastest" on that page refers to the *fix*.
- MindStudio, CONFIRMED: "a page built from your actual customer language, your actual product screenshots, and a specific visual reference will look nothing like…". — [MindStudio](https://www.mindstudio.ai/blog/avoid-vibecoded-landing-pages)
- MindStudio, NOT FOUND: the quote "say the same things, in the same order, with the same vague promises".

**Smashing Magazine and CSS-Tricks**
- I found no Smashing article dedicated to sameness. The closest is a July 28, 2026 piece sponsored by MacPaw, which argues for intentional human craft: "Using the same textbox format across all AI assistants does provide consistency. But we wanted to create a new, more personal and differentiated experience". — [Smashing](https://www.smashingmagazine.com/2026/07/digital-design-ai-era/)
- I found no CSS-Tricks article on this topic (search only).

**Rauno Freiberg, CONFIRMED:** "Small teams with autonomous high-performers usually produce the highest quality output because it is more likely you'll find 5 people aligned on taste and skill than 500." — [Lovers Magazine](https://spaces.is/loversmagazine/interviews/rauno-freiberg)

**Not reachable or gone**
- NOT VERIFIED: both uxdesign.cc essays, Design Systems Collective (the shadcn/Radix/Lucide claims), Microsoft Research and Northeast Times (the Canva "Imperfect by Design" claim).
- NOT FOUND (404): the dev.to yigit-konur shadcn theming guide.
- "Mintlify" in the earlier notes was a mirror of Impeccable's docs. It is now 410 Gone.

### Inferences
- **Independent sources agree on the cause.** NN/g, Anthropic, Kosta, the dev.to posts and HN commenters all say it is defaults from training data and stack choice. That makes the cause the most widely agreed point in this whole note set.
- **The indigo story should be treated as folklore.**

### Gaps
- No confirmation from Tailwind or Wathan beyond the joke tweet, and the tweet itself was not read.
- uxdesign.cc content is unverified.

## 5. The em-dash debate

### Takeaway
Many sources list the em dash as a tell: Krebs's designer quote, Impeccable, slop-detect, HN commenters and dev.to. Writers push back hard. The relevant point for UI is narrow: Anthropic flags "WORD — fragment" labels with a spaced em dash as template chrome.

### Cited Findings
- Optimizely, CONFIRMED. On the list of supposed tells: "none of these are AI tells. They're just language… It learned all of that from us". The author adds: "I use the em dash constantly. I used it before I'd ever typed a prompt into anything." — [Optimizely](https://www.optimizely.com/no/field-notes/articles/in-defense-of-the-em-dash-and-everything-else-on-this-ai-tell-trial)
- Search Engine Land: NOT VERIFIED (host blocked). Its method and findings remain unknown. — [Search Engine Land](https://searchengineland.com/ai-writing-tics-engagement-study-470051)
- dev.to raxxostudios, CONFIRMED: "This is the single most recognizable AI writing pattern." — [dev.to](https://dev.to/raxxostudios/why-your-ai-generated-content-looks-like-ai-and-how-to-fix-it-4ao6)
- Impeccable rule "Em-dash overuse": "A dash in every sentence is a familiar AI writing habit." — [Impeccable](https://impeccable.style/slop)
- skillselion's "at most 1 per 1,000 words": NOT FOUND in the fetched page, which may render with JS. — [skillselion](https://skillselion.com/skills/mblode/agent-skills/copywriting)
- The Admin Bar, CONFIRMED: "if your homepage contains seamless experiences, unique journeys, and something being unlocked, I'd start getting suspicious." — [The Admin Bar](https://theadminbar.com/how-to-edit-ai-website-copy/)

### Inferences
- In DashLens UI strings, avoid "Label — fragment" constructions and dashes in every sentence. In longer prose, the occasional em dash is defensible.

### Gaps
- No quantitative study of em-dash rates could be read.

## 6. Custom vs stock icons, and stock 3D illustrations, as perceived signals

### Takeaway
No rigorous study shows that stock icons make a site look AI-made. Practitioners and Krebs's data agree on narrower signals:
- icons in rounded tiles above every card heading
- emoji in navigation
- sparkles marking AI features
- mismatched icon sets
- default stroke, unchanged

For 3D or stock illustration, the evidence is weak and mixed. NN/g found no trust penalty for AI-generated hero photos. The only signals are practitioner warnings against generic or placeholder art.

### Cited Findings
**Icons**
- Krebs, first version: icon-topped card grid on 20.1% of sites, emoji in nav on 3.8%. — [GIGAZINE](https://gigazine.net/gsc_news/en/20260423-design-slop/)
- foundey (Nov 13, 2026): "Rounded tiles above every feature card, sparkles on AI buttons, emoji in the sidebar, and the same default outline set". — [foundey](https://foundey.com/blog/ai-slop-icons)
  - "Lucide isn't the problem… The problem is that it ships its defaults untouched."
  - "Most common mistake: swapping the line icons for expensive 3D icons in the same tiles."
  - Fix: a size scale (16/20/24 px), "One stroke weight… matched to your type weight", color roles.
  - Two of its claims are second-hand and unverified here: SaaStr's "The same Lucide icons are a dead giveaway", and a 2026 University of Jyväskylä study finding that "better-looking icons don't improve usability".
- Jim Nielsen: AI apps have "much smaller, thinner icons than their native counterparts". — [Nielsen](https://blog.jim-nielsen.com/2026/ai-aesthetic/)
- HN reactions to Nielsen — [HN 49117099](https://news.ycombinator.com/item?id=49117099):
  - piskov: "The issue with the icons is not the diameter but their stroke thickness — it should be the same as the letters."
  - somenameforme: the tell is "random and seemingly inappropriate symbols".
  - ajkjk: the sparkle is "the telltale sign of 'buttons not to click'".
- Impeccable rules: "Icon tile stacked above heading" ("Try placing the icon beside the heading, or remove its container") and a "Massive Icons" example. — [Impeccable](https://impeccable.style/slop)

**Illustrations and imagery**
- Impeccable rules: "Placeholder-style illustrations" ("generic circles and blocks"), "Rough SVG illustrations" ("A hastily drawn mascot") and "Broken or placeholder image". Its README describes the default output as "flat vector illustrations in rounded cards". — [Impeccable](https://impeccable.style/slop); [README](https://raw.githubusercontent.com/pbakaus/impeccable/main/README.md)
- 21st.dev: "Stock everything. Generic illustrations, a smiling team photo that is not the team". — [21st.dev](https://21st.dev/blog/website-not-look-ai-generated)
- NN/g, counter-evidence: 77 participants rated 6 page versions that differed only in the hero image. "When users didn't know whether an image was AI-generated, the images we tested did not create any perception penalty compared to stock photos." — [NN/g](https://www.nngroup.com/articles/ai-generated-images/)
- Getty/iStock: the claim that AI imagery was "least preferred" against real and 3D/CGI imagery is NOT VERIFIED (HTTP 403).

### Inferences
- For DashLens:
  - use one icon set with stroke matched to the text weight
  - put icons beside labels, not in tiles
  - no emoji or sparkles
  - a few custom glyphs only for dashcam concepts (front/rear camera, G-shock, parking)
  - no decorative 3D art at all, since real footage is the product's imagery

### Gaps
- I found no controlled study of custom versus stock icon sets as a perceived craft or AI signal.
- I found no study specifically on stock 3D illustrations.

## 7. Ledger: every "(via search summary)" claim and Gap in the earlier notes

### Takeaway
Of 31 items checked:
- 12 CONFIRMED
- 9 CORRECTED (mostly attribution or version issues, not substance)
- 5 NOT FOUND
- 5 NOT VERIFIED (blocked hosts)

The core list of tells stands. The numbers and attributions needed fixing.

### Cited Findings
| Earlier claim | Status | Correct version / source |
|---|---|---|
| Krebs: 500 posts, 21/46/33 (GIGAZINE) | CONFIRMED for the first version | [dang on HN](https://news.ycombinator.com/item?id=47864393) |
| Krebs: 22/32/46 (Developers Digest) | CONFIRMED for the current version (1,590 sites, 4+ / 2–3 / 0–1) | [Krebs](https://www.adriankrebs.ch/blog/design-slop/) |
| Krebs: ~1,400 sites, 67% (slop-detect) | NOT FOUND in the current slop-detect README. "~1400" appears in Krebs's method section; 67% is probably 21+46 | [Krebs](https://www.adriankrebs.ch/blog/design-slop/) |
| Krebs used "about 15–16 patterns" | CORRECTED: 15 in the first version, 16 in the current one | [GIGAZINE](https://gigazine.net/gsc_news/en/20260423-design-slop/) |
| Critic: thresholds tuned on the same sample | CORRECTED: this targets the IOV Labs paper (202 sites), not Krebs | [maxiality](https://maxiality.com/how-to-spot-an-ai-generated-website/) |
| HN commenters: zero-offset glows, 1px border + 40px blur, Inter/Roboto/Geist, plus JetBrains Mono | CORRECTED: one commenter describing Impeccable's rules. JetBrains Mono NOT FOUND in that thread | [HN 49290499](https://news.ycombinator.com/item?id=49290499) |
| Jim Nielsen: beige/cream, orange, serif | CONFIRMED | [Nielsen](https://blog.jim-nielsen.com/2026/ai-aesthetic/) |
| HN tied the cream look to Claude/Codex/Cursor apps | CORRECTED: Nielsen names those apps for tiny icons | [Nielsen](https://blog.jim-nielsen.com/2026/ai-aesthetic/) |
| Kyle Chayka quote (Northeast Times) | NOT VERIFIED (403) | — |
| Impeccable: cyan-on-dark, purple-blue, uniform spacing, modals, bounce | CONFIRMED | [Impeccable](https://impeccable.style/slop) |
| Impeccable: every button primary | NOT FOUND | — |
| Impeccable: "fingerprints of 2024–25" (Mintlify) | NOT FOUND (page 410) | — |
| Impeccable rule counts 25/37/58 | CORRECTED: 62 rules (+6 review patterns) | [README](https://raw.githubusercontent.com/pbakaus/impeccable/main/README.md) |
| Impeccable: bans paired with alternatives (Latent Space) | CORRECTED: not in the article, but true of the catalog | [Latent Space](https://www.latent.space/p/skill-engineering-design) |
| Lucide as an AI signature (DSC, foundey) | foundey CONFIRMED (citing SaaStr); DSC NOT VERIFIED | [foundey](https://foundey.com/blog/ai-slop-icons) |
| NN/g generic sans-serif look, "potentially good" | CONFIRMED in the primary source | [NN/g](https://www.nngroup.com/articles/ai-prototyping/) |
| arXiv Design Theater | CORRECTED emphasis (rationale gap is the main finding) | [arXiv](https://arxiv.org/abs/2607.22928) |
| Microsoft Research homogenisation | NOT VERIFIED (403) | — |
| MindStudio "same things, same order" | NOT FOUND; "customer language… screenshots" CONFIRMED | [MindStudio](https://www.mindstudio.ai/blog/avoid-vibecoded-landing-pages) |
| 21st.dev: scroll animations are the fastest tell | CORRECTED: "show the product" is the fastest *fix* | [21st.dev](https://21st.dev/blog/website-not-look-ai-generated) |
| 21st.dev typeface / "only about you" | CONFIRMED | [21st.dev](https://21st.dev/blog/website-not-look-ai-generated) |
| Admin Bar "seamless… unlocked" | CONFIRMED | [Admin Bar](https://theadminbar.com/how-to-edit-ai-website-copy/) |
| dev.to raxxo: em dash "single most recognizable" | CONFIRMED | [dev.to](https://dev.to/raxxostudios/why-your-ai-generated-content-looks-like-ai-and-how-to-fix-it-4ao6) |
| skillselion: 1 em dash per 1,000 words | NOT FOUND | — |
| Search Engine Land em-dash study | NOT VERIFIED (blocked) | — |
| Optimizely defense | CONFIRMED | [Optimizely](https://www.optimizely.com/no/field-notes/articles/in-defense-of-the-em-dash-and-everything-else-on-this-ai-tell-trial) |
| Tailwind indigo-500 origin | CORRECTED: a real but joking Wathan tweet (Aug 2025); causation unproven; view count disputed (684k vs >1M) | [AIbase](https://news.aibase.com/news/20365) |
| Lovable/v0/Claude Code ship Inter+shadcn+Lucide (dev.to fix) | CORRECTED source: foundey/SaaStr | [foundey](https://foundey.com/blog/ai-slop-icons) |
| Kosta "design with no author" | CONFIRMED | [HEY](https://world.hey.com/kostac/spot-the-slop-a-ui-designer-s-guide-to-fixing-ai-defaults-4c448c9c) |
| Built In baseline shift | CONFIRMED | [Built In](https://builtin.com/articles/ai-design-slop-era) |
| Rauno small teams / taste | CONFIRMED | [Lovers Magazine](https://spaces.is/loversmagazine/interviews/rauno-freiberg) |

### Inferences
- The earlier DashLens recommendations still hold, and the primary sources make them stronger:
  - Anthropic's cluster 2 and cluster 5 match DashLens closely.
  - Impeccable explicitly allows a dark theme if the glow is cut.
  - NN/g and IOV Labs put the problem down to "defaults with nothing deliberate next to them", not to any single color.

### Gaps
- Still open: uxdesign.cc, Design Systems Collective, Search Engine Land, Northeast Times/Chayka, Microsoft Research, the Getty research, and the Wathan tweet itself. These need the hosts allowed in the session network settings.
