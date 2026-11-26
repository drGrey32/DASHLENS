# Tells of AI-generated ("AI slop") UI, and how professional designers avoid them

Research date: 2026-11-26. Scope: 2023–2026 output of v0, Lovable, Bolt, Cursor, Claude/ChatGPT-made sites and shadcn/Tailwind defaults.

Source note: many hosts were unreachable from this session (news.ycombinator.com, adriankrebs.ch, dev.to, uxdesign.cc, world.hey.com, gigazine.net, blog.jim-nielsen.com, mintlify.com, dixi.agency, matthewblode.com). I read three primary sources in full: Anthropic's Nov 2025 article, Anthropic's current `frontend-design` SKILL.md on GitHub, and the `slop-detect` repo with its pattern spec. Claims from the unreachable sites come from search-engine summaries and are marked "(via search summary)". Quote them with care.

## Visual tells: which ones are widely agreed and which are opinion

### Takeaway
The tells most sources agree on are these:
- purple/indigo accents and gradients
- gradient-clipped hero text
- blurred "aurora" blobs and colored glows
- glassmorphism
- Inter/Geist/Space Grotesk type
- a centered hero with a "Now in beta" pill above the H1
- identical icon-topped cards in a grid
- a big-number stat row and fake logo or testimonial strips
- one radius and one shadow on every card

The look has also moved. By 2026 the earlier "fixes" have become tells themselves: cream/serif/terracotta, near-black with one acid-green or vermilion accent, all-caps eyebrows and monospace data labels. That matters for DashLens's dark UI with one orange accent.

### Cited Findings
**Anthropic, primary source.** The Nov 12 2025 article says that without direction Claude falls back on the most common web defaults. It names these overused fonts: Inter, Roboto, Open Sans, Lato, Arial and system fonts. It names "purple gradients on white backgrounds" as the cliché colour scheme, plus "predictable layouts and component patterns". It also notes that when told to avoid those, the model drifts to the next default, for example Space Grotesk. — [Anthropic: Improving frontend design through Skills](https://claude.com/resources/articles/improving-frontend-design-through-skills)

**Anthropic's current frontend-design SKILL.md, primary source.** It lists these defaults to avoid:
- a cream background with a serif display face and a terracotta accent
- **a near-black background with a single acid-green or vermilion accent**
- broadsheet layouts with hairline rules, zero radius and dense columns
- the "SaaS card kit": identical rounded cards, a uniform soft shadow and gradient washes
- "template chrome": all-caps eyebrows, middle-dot meta strings, "WORD — fragment" labels, tinted near-black, monospace data labels, and arrows on links and buttons

It also warns against accenting one word in a headline, and against labels nobody needs above content. — [anthropics/skills frontend-design SKILL.md](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)

**slop-detect, an open-source scorer.** It credits Adrian Krebs's Show HN study, Impeccable (Paul Bakaus), Anthropic frontend-design and others, and lists 45 design patterns.

Weighted patterns:

| Pattern | Weight |
|---|---|
| AI-default fonts (Inter/Geist) | 8 |
| Cream default background | 7 |
| Low-contrast body text below WCAG AA | 7 |
| Gradient-clipped hero text | 6 |
| Coloured top/left card accent stripe | 6 |
| Launch/beta pill above H1 | 5 |
| Gradient-letter initial avatars | 5 |
| Aurora/mesh blurred blobs | 5 |
| Crushed display tracking | 5 |
| Filled indigo/violet CTAs | 4 |
| Gradient-heavy backgrounds | 4 |
| Glassmorphism | 4 |
| Coloured box-shadow glows | 4 |
| Centred generic-sans hero | 4 |
| **Perma-dark page with grey body text** | 4 |
| Identical icon-top feature cards | 4 |
| Bento grid | 4 |
| Oversized hero H1 | 4 |
| Nested cards | 4 |
| Numbered "1·2·3" steps | 3 |
| Stat banner | 3 |
| AI sparkle badges | 3 |
| Flat type hierarchy | 3 |
| FAQ accordion | 2 |

Review-only patterns:
- one accent word in the H1
- the same radius and shadow on every card
- the cream/serif kit
- the standard section order
- pulsing status-dot badges
- monospace display headings
- multi-hue pastel chips
- fake macOS traffic-light windows
- placeholder "Trusted by" logo strips
- infinite marquees
- the same fade-up reveal on every section
- a cursor-spotlight gradient
- the same hover lift on every card
- repeated section layouts
- a dark page without `color-scheme`

— [slop-detect patterns.md](https://raw.githubusercontent.com/ravidsrk/slop-detect/main/spec/patterns.md); [slop-detect repo](https://github.com/ravidsrk/slop-detect)

**Adrian Krebs's Show HN study (April 2026).** Krebs scored Show HN landing pages against about 15–16 AI-design patterns. The pill badge above the title stood out as especially recognisable. Reported numbers conflict:
- 500 posts, 21% "heavy" (5+ patterns), 46% "mild", 33% "clean" (via search summary of GIGAZINE / a Korean write-up)
- about 1,400 submissions, 67% with fingerprints — [slop-detect](https://github.com/ravidsrk/slop-detect)
- 22% heavy / 32% mild / 46% clean — [Developers Digest](https://www.developersdigest.tech/series/ai-tools-deep-dive) (via search summary)

A critic notes the thresholds were tuned on the same small sample. — [GIGAZINE](https://gigazine.net/gsc_news/en/20260423-design-slop/); [maxiality](https://maxiality.com/how-to-spot-an-ai-generated-website/) (via search summary)

**Hacker News commenters** named these tells: zero-offset dark glows on text, 1px borders paired with a 40px shadow blur, and Inter/Roboto/Geist as the default "tasteful" font. On anything programming-related, add JetBrains Mono. — [HN thread](https://news.ycombinator.com/item?id=49290499) (via search summary)

**The 2026 "AI aesthetic" of beige/cream colours, orange accents and serif typefaces.** Jim Nielsen describes it, and an HN thread associates it with AI desktop apps such as Claude, Codex and Cursor. Kyle Chayka (The New Yorker) is reported describing "beige and cream backgrounds, rusty orange accents, large serif typefaces". — [Jim Nielsen, The AI Aesthetic](https://blog.jim-nielsen.com/2026/ai-aesthetic/); [HN via hn.svelte.dev](https://hn.svelte.dev/item/49117099); [Northeast Times](https://northeasttimes.com/?p=159671) (all via search summary)

**Impeccable (Paul Bakaus), built on Anthropic's skill.** Its anti-pattern list includes:
- cyan-on-dark palettes
- purple-to-blue gradients
- uniform spacing
- modals by default
- bounce/elastic easing
- every button styled as primary

Its docs call these the fingerprints of generic 2024–25 AI work. Reported counts vary: 25, 37 or 58 rules. — [Latent Space interview](https://www.latent.space/p/skill-engineering-design); [Impeccable docs](https://www.mintlify.com/pbakaus/impeccable/concepts/anti-patterns) (via search summary)

**Icons.** Lucide React icons are recognised as a signature of AI-built sites, and one "vibe-coded" scorer flags Lucide plus the same handful of icons. — [Design Systems Collective](https://www.designsystemscollective.com/is-anyone-else-tired-of-every-tailwind-shadcn-app-looking-the-same-69c545e73114); [foundey: AI slop icons](https://foundey.com/blog/ai-slop-icons) (via search summary)

**NN/g, second-hand.** NN/g reportedly ran a real project through several AI prototyping tools in late 2025. The output defaulted to "a similar, generic look using sans-serif typeface and minimalistic styling", with flat, interchangeable screens. NN/g concedes the mainstream bias "could potentially be good for the user experience". — [uxcel summary of NN/g](https://uxcel.com/lessons/directing-taste-011) (via search summary)

### Inferences
- **This matters directly for DashLens.** Its current direction, a dark UI with one orange accent and possibly mono telemetry labels, matches three listed 2026 tells: Anthropic's "near-black + single vermilion accent", slop-detect's "perma dark mode + grey body text", and the "orange accent" of the AI aesthetic. Taken alone, the palette will not make it look designed. A dark UI is justified for video viewing, because it keeps the frame dominant, so keep it. What has to change is that the identity comes from the domain (footage, timeline, map, telemetry), not from the palette. Body text must stay high-contrast, and `color-scheme: dark` must be set.
- **Agreement versus opinion.** The 2024–25 core (indigo, gradient text, blobs, glass, Inter, pill-above-H1, icon-card grid, stat row) appears in every list, including Anthropic's. The 2026 additions (cream/serif, dark + one neon accent, mono labels, eyebrows, arrows on links) come mainly from Anthropic's skill and a few critics. They are better read as "the current default" than as universally condemned.
- Emoji icons and fake testimonials or stats appear in the copy and structure lists (emoji-prefixed headers, placeholder testimonials, fake logo bars), not as standalone visual studies.

### Gaps
- I could not read Krebs's original post (host blocked), so the exact pattern list and numbers are unverified. Secondary sources disagree.
- No rigorous study measures how often each tell appears. The "95.4% of AI UI colours are blue-purple" figure comes from a single dev.to post and is uncorroborated ([dev.to kenimo49](https://dev.to/kenimo49/why-ai-generated-uis-are-all-the-same-color-and-the-data-to-prove-it-12oe)).
- I found no source on stock 3D illustrations specifically as an AI tell, beyond general "unedited AI imagery" warnings ([21st.dev](https://21st.dev/blog/website-not-look-ai-generated), via search summary).

## Structural tells

### Takeaway
The structural tell is sameness: the canonical section order (hero, logo bar, 3 feature cards, numbered steps, stat row, testimonials, 3-tier pricing, FAQ accordion, CTA), each section with the same rhythm and the same reveal animation. Decoration also stands in for information: numbers, labels and borders that encode nothing.

### Cited Findings
- slop-detect flags:
  - "canonical landing section order"
  - "repeated identical section layouts"
  - FAQ accordion
  - numbered steps
  - stat banner
  - "template chrome" (floating glass nav, avatar stack, 3-tier pricing)
  - nested cards
  - flat type hierarchy
  - uniform fade-up animations
  - uniform card hover lift

  — [slop-detect patterns.md](https://raw.githubusercontent.com/ravidsrk/slop-detect/main/spec/patterns.md)
- Anthropic's skill says to use numbered markers, borders and labels only when they encode real information, such as an actual sequence. It also says to avoid fade-and-slide entrances on every section and hover effects on every card, and to remove any decoration that doesn't serve the brief. — [Anthropic SKILL.md](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)
- Anthropic (2025) recommends one well-orchestrated page-load moment rather than scattered micro-interactions. — [Anthropic article](https://claude.com/resources/articles/improving-frontend-design-through-skills)
- A 2026 arXiv paper ("Design Theater") finds generated interfaces cluster visually or structurally while being presented as tailored design responses. Microsoft Research reports that frictionless vibe coding can make homogenisation worse. — [arXiv 2607.22928](https://arxiv.org/pdf/2607.22928); [Microsoft Research](https://www.microsoft.com/en-us/research/?p=1171164) (via search summary)
- AI pages "say the same things, in the same order, with the same vague promises". — via search summary of [MindStudio](https://www.mindstudio.ai/blog/avoid-vibecoded-landing-pages)
- Scroll animations are called the fastest way to look obviously AI-generated. — via search summary of [21st.dev](https://21st.dev/blog/website-not-look-ai-generated)
- Anthropic's skill says empty states should invite action, and errors should say what went wrong and how to fix it. Generic empty states are the opposite. — [Anthropic SKILL.md](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)

### Inferences
- For an app (as opposed to a landing page), the equivalents are:
  - every panel styled as the same card
  - equal visual weight for primary and secondary controls (Impeccable's "every button primary")
  - modals by default
  - decorative status badges
  - empty states that say "No data yet" with an icon, instead of telling the user what to drop or load

### Gaps
- I found no study of over-explaining (redundant helper text) as a measured tell. It appears only in copy-pattern lists ("announced structure", "restated thesis closer").

## Copy tells

### Takeaway
The copy tells most sources agree on:
- buzzword density (seamless, unlock, leverage, robust, elevate, effortless, powerful, transformative)
- "It's not just X, it's Y" antithesis
- "Whether you're X or Y" framing
- rule-of-three adjective lists
- throat-clearing openers and summary closers
- emoji-prefixed bullets
- placeholder testimonials
- uniform sentence rhythm

The em dash is widely cited, but it is also the most contested tell.

### Cited Findings
- slop-detect's copy patterns are:
  - buzzword density (weight 7)
  - "not just X — it's Y" (weight 6)
  - filler openers (weight 5)
  - em-dash overload (weight 2)
  - rule of three
  - "whether you're"
  - formulaic closers
  - emoji bullet headers
  - structural fake social proof
  - announced structure
  - restated-thesis closer
  - trailing "-ing" clauses
  - sentence-length uniformity
  - leaked chatbot or prompt text
  - unfilled `[Insert…]` placeholders
  - `utm_source=chatgpt.com` links

  — [slop-detect repo](https://github.com/ravidsrk/slop-detect); [patterns.md](https://raw.githubusercontent.com/ravidsrk/slop-detect/main/spec/patterns.md)
- "Seamless experiences, unique journeys, and something being unlocked." One instance proves nothing, but a page full of them is a reason for suspicion. — [The Admin Bar](https://theadminbar.com/how-to-edit-ai-website-copy/) (via search summary)
- **Em dash, contested.** It is called the single most recognisable AI writing pattern ([dev.to raxxostudios](https://dev.to/raxxostudios/why-your-ai-generated-content-looks-like-ai-and-how-to-fix-it-4ao6), via search summary). A copywriting skill suggests at most 1 per 1,000 words ([skillselion](https://skillselion.com/skills/mblode/agent-skills/copywriting)). Search Engine Land and Optimizely counter that many human writers use em dashes heavily ([Search Engine Land](https://searchengineland.com/ai-writing-tics-engagement-study-470051); [Optimizely](https://www.optimizely.com/no/field-notes/articles/in-defense-of-the-em-dash-and-everything-else-on-this-ai-tell-trial)).
- An HN commenter says "everything comes in punchy threes" is a giveaway. — (via search summary of HN)
- Anthropic's skill asks for writing from the user's perspective, in plain language, with active verbs and sentence case. — [Anthropic SKILL.md](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)

### Inferences
- Sentence case everywhere (Anthropic) is the safe choice. A mix of Title Case headings and sentence-case buttons reads as unedited.
- DashLens copy should name concrete things: file types, camera brands, GPS, G-sensor events, "nothing leaves your browser". Avoid adjectives.

### Gaps
- No quantitative source compares tricolon frequency in AI and human copy (thin evidence).
- I found no source on title-case/sentence-case inconsistency as a measured tell. It is inferred from style guidance.

## Why it happens

### Takeaway
Models sample from the most probable patterns in their training data (Anthropic calls this "on distribution" or distributional convergence). The tools also ship the same stack before any design decision is made: Tailwind, shadcn/ui on Radix, Lucide and Inter. Output then feeds back into the training data.

### Cited Findings
- "During sampling, models predict tokens based on statistical patterns in training data". Safe, universally acceptable choices dominate, so Claude gravitates to them. Its prompt says: "You tend to converge toward generic, 'on distribution' outputs." — [Anthropic](https://claude.com/resources/articles/improving-frontend-design-through-skills)
- Banning one default shifts the model to the next one: Space Grotesk after Inter. Reportedly, "don't use cream" likewise shifts the palette elsewhere. — [Anthropic](https://claude.com/resources/articles/improving-frontend-design-through-skills); [Northeast Times](https://northeasttimes.com/?p=159671) (via search summary)
- The Tailwind UI origin of indigo-500 is a single secondhand claim. Its buttons were reportedly set to `bg-indigo-500` about five years ago, and models trained on Tailwind UI sites learned blue-purple as the default. — [dev.to alanwest](https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p) (via search summary; unverified)
- Lovable, v0 and Claude Code ship Inter, shadcn, Lucide and Tailwind spacing before the model makes any design decision. Training code is heavily React + Tailwind + shadcn/Radix + Lucide. Radix's predictable shapes help accessibility but limit originality. — via search summaries of [dev.to alanwest (fix)](https://dev.to/alanwest/how-to-fix-the-ai-generated-look-in-your-frontend-1ahh) and [Design Systems Collective](https://www.designsystemscollective.com/is-anyone-else-tired-of-every-tailwind-shadcn-app-looking-the-same-69c545e73114)
- The feedback loop: AI-built sites re-enter training data, which makes later output more purple or more shadcn. — via search summaries of [dev.to](https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p) and [Design Systems Collective](https://www.designsystemscollective.com/is-anyone-else-tired-of-every-tailwind-shadcn-app-looking-the-same-69c545e73114)
- "Slop isn't bad design in the old sense… Slop is design with no author." (UI designer Kosta Canatselis) — [Spot the slop](https://world.hey.com/kostac/spot-the-slop-a-ui-designer-s-guide-to-fixing-ai-defaults-4c448c9c) (via search summary). A related uxdesign.cc essay argues AI design "isn't ugly, it's fluent". — [uxdesign.cc](https://uxdesign.cc/ai-design-isnt-ugly-it-s-fluent-and-that-s-the-problem-131b2f4eb78c) (title only)
- Built In argues that the baseline for acceptable design has shifted to whatever AI produces. — [Built In](https://builtin.com/articles/ai-design-slop-era) (via search summary)

### Inferences
- Because bans just move the model to the next default, a ban list is not enough. The counter is positive, domain-derived decisions (see below). Impeccable's approach of pairing each ban with an alternative is consistent with this.

### Gaps
- The Tailwind indigo-500 origin story is not confirmed by Adam Wathan or Tailwind in any source I could reach.

## Counter-techniques that signal human craft and intent

### Takeaway
Professionals and the published skills agree on the method:
1. Start from the subject and its vernacular.
2. Make a few opinionated decisions: a compact token set, one or two distinct type families with a real scale, and boldness spent in one place.
3. Use real content and specific copy.
4. Remove every decoration that encodes no information.
5. Finish the craft details templates skip: states, accessibility, reduced motion, errors and empty states.

### Cited Findings
- **Anthropic's skill, primary source.** Its process:
  - Identify the subject, the audience and the primary job.
  - Draw visual choices from the subject's own vernacular.
  - Open with the most characteristic element of the subject.
  - "Spend your boldness in one place", keeping everything else restrained.
  - Plan 4–6 named hex values, type roles and an ASCII wireframe.
  - Check the plan against the brief for generic defaults before building.
  - Use one family, or two clearly distinct ones, with a deliberate type scale.
  - Keep lines under 80 characters.
  - Keep a quality floor: responsive, keyboard-focusable, reduced-motion aware, accessible.
  - Critique while building, and remove decoration that doesn't serve the brief.

  — [Anthropic SKILL.md](https://raw.githubusercontent.com/anthropics/skills/main/skills/frontend-design/SKILL.md)
- **Anthropic's 2025 article.**
  - Commit to a cohesive theme with CSS variables, dominant colours and sharp accents, drawing inspiration from IDE themes and cultural aesthetics.
  - Use extreme weight contrast (100/200 vs 800/900) and size jumps of 3x or more.
  - Suggested families include IBM Plex, Source Sans 3, Bricolage Grotesque, Newsreader, JetBrains Mono and Fira Code.
  - Use one orchestrated load sequence.

  — [Anthropic](https://claude.com/resources/articles/improving-frontend-design-through-skills). Caveat: several of these choices (mono labels, a dark theme with one accent) are now themselves listed as defaults in Anthropic's newer SKILL.md, which shows the target moves.
- **Real material.** Build from actual customer language, actual product screenshots and a specific visual reference. Strip the default tells first, then add a style of your own. — [MindStudio](https://www.mindstudio.ai/blog/avoid-vibecoded-landing-pages) (via search summary)
- **Type and headline.** Choose "a face nobody else in your space uses, paired with something plain", and write a headline "that could only be about you", for example a real number. — [21st.dev](https://21st.dev/blog/website-not-look-ai-generated) (via search summary)
- **shadcn users.** Change the icon set, font and radius at setup and define your own design tokens. — [Design Systems Collective](https://www.designsystemscollective.com/is-anyone-else-tired-of-every-tailwind-shadcn-app-looking-the-same-69c545e73114); [shadcn OKLCH theming guide](https://dev.to/yigit-konur/the-complete-shadcnui-theming-guide-a-practical-approach-with-oklch-to-make-it-looks-10x-more-2l4l) (via search summary)
- **Impeccable.** Prohibitions work better than "create good design", and each ban is paired with a positive alternative. — [Latent Space](https://www.latent.space/p/skill-engineering-design) (via search summary)
- **NN/g, second-hand.** Name established design styles rather than vague descriptors. A polished mockup that matches your design system can still be a poor design. — [uxcel summary](https://uxcel.com/lessons/directing-taste-011) (via search summary)
- **Taste.** Rauno Freiberg (Vercel; formerly Arc at The Browser Company) says small teams of autonomous high performers produce the best output because they share taste and skill. His work is known for finely crafted interactions ("Devouring Details"). — [Lovers Magazine interview](https://spaces.is/loversmagazine/interviews/rauno-freiberg) (via search summary). Production is no longer scarce; taste is the bottleneck. — [uxdesign.cc](https://uxdesign.cc/ai-made-everyone-a-creator-not-a-designer-e28deb6e603b) (via search summary)
- **Counter-trend.** Some brands are reacting against AI polish with intentional imperfection. Canva's 2026 trends report calls it "Imperfect by Design". — (via search summary, [Northeast Times](https://northeasttimes.com/?p=159671))

### Inferences (applied to DashLens)
- **Make the footage the hero.** The page should open on a real dashcam frame with a real timeline, real GPS track and real G-sensor trace. Avoid gradient blobs and icon cards. Use real, consented footage with plates and faces blurred, not stock images.
- **Spend the boldness in one place.** For example, the event timeline/scrubber as the one signature element, drawn with care: tick density, event markers that work without colour, gap labels. Keep everything else quiet.
- **Make orange semantic.** Use it only for "now" and active state (playhead, selected event, primary action), never for decoration. That turns it from a palette cliché into a system. Keep body text high-contrast, set `color-scheme: dark`, and use several surface steps rather than one tinted near-black.
- **Use mono only for real data.** Monospace only for values that are tabular data (timestamps, speed, coordinates) with tabular numerals. Avoid all-caps eyebrows and mono decorative labels, both of which are listed tells.
- **Icons.** Use one consistent set, adjusted (stroke and size matched to the type), or a few custom glyphs for dashcam concepts (front/rear camera, parking event, G-shock). Avoid default Lucide everywhere, and never emoji.
- **Copy.** Make it specific and in sentence case. Examples: "Drop a folder from your SD card", "Files never leave this browser", supported brands and formats. Avoid "seamless", "unlock", "powerful", tricolons and "not just X, it's Y".
- **States and craft.** Do the work templates skip: loading, error and empty states; keyboard shortcuts; focus rings; reduced motion; behaviour with a missing GPS file; and copy that says how to fix each problem.
- **Vary rhythm and radius.** Avoid uniform radius and shadow on everything. Vary radius by component role, rely on borders and surface steps rather than soft shadows, and use asymmetric layout where the content justifies it (video large, details narrow).

### Gaps
- I found no authoritative source specifically on custom versus stock icon sets as a craft signal. The recommendation is inferred.
- I found no reachable primary designer essays from Smashing Magazine or CSS-Tricks on this topic in 2024–2026. The search returned mainly dev blogs, tool vendors and skill docs, so most counter-technique evidence is practitioner opinion, not research.
