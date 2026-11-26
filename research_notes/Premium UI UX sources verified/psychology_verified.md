# Psychology and Emotional Design for a UI Used Under Stress: Verification Against Primary Sources

Scope: this checks the claims and Gaps in `research_notes/Premium UI UX for DashLens/psychology_emotion.md`, which was built partly from search summaries. DashLens context: a dashcam video viewer used by a stressed owner just after an incident.

Labels used on each finding:
- **CONFIRMED**: the primary source says it. A short exact quote and the URL are given.
- **CORRECTED**: the primary source says something different. What it really says is given.
- **NOT FOUND**: I could not find it in the primary source, or could not reach the source. The reason is given.

Method: pages were fetched directly (curl) and searched as text. Abstracts for paywalled papers came from PubMed (NCBI E-utilities), Crossref and OpenAlex, which carry the publisher's abstract. Hosts that were still unreachable in this session: `www.viget.com` (HTTP 429, bot-check page), `www.vm.ibm.com`, `academic.oup.com`, `dl.acm.org` and `tandfonline.com` (403), `blog.chayn.co` and `medium.com` (blocked), `web.archive.org` (blocked). Anything that depends only on those hosts is marked NOT FOUND.

---

## 1. Nielsen's response-time limits; NN/g on progress indicators and skeleton screens; the skeleton-screen studies (Viget, Mejtoft)

### Takeaway
Nielsen's 0.1 s / 1 s / 10 s limits are confirmed word for word. NN/g's own rules are: give some feedback at once, show a progress indicator for anything over about 1 s, use a spinner only for 2–10 s, and use a percent-done bar at 10 s and over. Two corrections matter: NN/g says skeleton screens are **only** for full-page loads and should **not** be used for processes such as download, convert or export. The one peer-reviewed skeleton study NN/g cites (Mejtoft et al. 2018) found **no significant differences**.

### Cited Findings
**Nielsen, "Response Times: The 3 Important Limits" (Jakob Nielsen, dated 1 January 1993; excerpt from ch. 5 of *Usability Engineering*, with a 2014 update)** — [NN/g](https://www.nngroup.com/articles/response-times-3-important-limits/)
- CONFIRMED (0.1 s): "0.1 second is about the limit for having the user feel that the system is reacting instantaneously, meaning that no special feedback is necessary except to display the result."
- CONFIRMED (1 s): "1.0 second is about the limit for the user's flow of thought to stay uninterrupted, even though the user will notice the delay."
- CONFIRMED (10 s): "10 seconds is about the limit for keeping the user's attention focused on the dialogue."
- CONFIRMED (beyond 10 s), from the 2014 update: "Anything slower than 10 seconds needs a percent-done indicator as well as a clearly signposted way for the user to interrupt the operation." Also: "Assume that users will need to reorient themselves when they return to the UI after a delay of more than 10 seconds."
- NEW, from the same page: the 1993 text says a percent-done bar may be "overkill" for 2–10 s operations because it can violate "the principle of display inertia (flashing changes on the screen so rapidly that the user cannot keep pace or feels stressed)". For work of unknown size: "it is still possible to provide running progress feedback in terms of the absolute amount of work done."
- NEW: Nielsen traces the limits to earlier work: "The basic advice regarding response times has been about the same for thirty years [Miller 1968; Card et al. 1991]". The page summary says the limits "are determined by human perceptual abilities".

**NN/g, "Progress Indicators Make a Slow System Less Insufferable" (dated 26 Oct 2014)** — [NN/g](https://www.nngroup.com/articles/progress-indicators/)
- NEW: "Always give some type of immediate feedback." / "Use a progress indicator for any action that takes longer than about 1.0 second."
- NEW: Looped animation (spinner) "should be reserved for actions that take between 2-10 seconds". Under 1 s it is "distracting… users cannot keep up with what happened and might feel anxious about whatever flashed on the screen."
- NEW: "Percent-done animation: Use for actions that take 10 seconds or more." Below 10 s a percent-done bar is still fine "if the action involves processing a series of documents or registries… include a text explanation of the process, for example 'Updating address 3 of 50.'"
- NEW: "if the progress moves quickly only to hang on the last percentage remaining, the user will become frustrated and the benefits of showing progress will be negated." It also advises: "Start the progressive animation slower and allow it to move faster as it approaches the end."
- NEW: "Static progress indicators: Don't use them." and "Don't-click-again warnings: Don't use them."
- NEW: "For actions that take a little while, give users the option to stop the process… Otherwise, your design may be hijacking control of the system, leaving the user powerless."
- NEW (secondary study cited by NN/g, not checked): in a University of Nebraska–Lincoln study, people who saw a moving progress bar "were willing to wait on average 3 times longer". NN/g's reference is Nah, F. (2004), *Behaviour and Information Technology* 23(3).

**NN/g, "Skeleton Screens 101" (page dated 2 Sep 2026)** — [NN/g](https://www.nngroup.com/articles/skeleton-screens/)
- CONFIRMED with qualification (shorter perceived wait): the summary says skeleton screens are "used for full-page loads and reduces the perceived loading time". NN/g's only reference for this is Mejtoft et al. 2018, which found no significant difference (see below).
- CONFIRMED (spinners for 2–10 s): "they are best used when the page takes 2–10 seconds to load. Similarly, skeleton screens should be used with a wait time that's under 10 seconds."
- CONFIRMED (no indicator under 1 s): "If a page takes less than 1 second to load, skeleton screens or spinners aren't necessary".
- CORRECTED / NEW (missing from the earlier notes, and it matters): "Skeleton screens are used to indicate progress only when the process that the system is performing is a full-page load. Whenever some other process (e.g., download, upload, convert a file) is involved, it does not make sense (and could even be confusing) to show a skeleton screen. Instead, show a progress bar or a wizard that walks the user through the steps of the process."
- NEW: "Spinners are typically best used on a single module, like a video or a card which is on a dashboard." NN/g advises against frame-only skeletons. It notes that shimmer animations "can potentially be distracting, annoying, or even create accessibility problems for some users."

**Mejtoft, Långström & Söderström (2018), "The effect of skeleton screens: Users' perception of speed and ease of navigation", ECCE 2018, DOI 10.1145/3232078.3232086** — [abstract via OpenAlex](https://api.openalex.org/works?filter=doi:10.1145/3232078.3232086); [DOI](https://doi.org/10.1145/3232078.3232086)
- CORRECTED: the earlier notes said this study "reportedly found skeletons rated faster". The abstract says the skeleton page "scored higher on average on both perceived speed and ease of navigation. However, people using the page with spinners were faster at finding the article… The results of this paper cannot show any significant differences in any of the comparisons between the web pages." The sample size is not in the abstract.

**Viget, "A Bone to Pick with Skeleton Screens" (2017)** — [Viget](https://www.viget.com/articles/a-bone-to-pick-with-skeleton-screens/)
- NOT FOUND: the page returned HTTP 429 (a Vercel bot-check page) on every try. The figures n = 136 and perceived waits of 2.82 s (skeleton), 2.41 s (spinner) and 2.29 s (blank) are still unconfirmed. Treat them as secondary until someone checks the page.

### Inferences
- **DashLens timing rules, now on solid ground.** Acknowledge a drop or click within 0.1 s. For indexing a folder, use a counted, determinate indicator ("Reading GPS: 9 of 14 clips"), which NN/g allows even under 10 s for "a series of documents". For an export that may take 10 s or more, show a percent-done bar **and** a visible Cancel; Nielsen calls both necessary.
- **No skeleton screens for export, parsing or conversion.** NN/g limits skeletons to full-page loads. Spinners suit a single module, such as the video tile while it decodes, or the map tile.
- **Avoid a bar that races and then stalls at 99%.** NN/g says it "negates" the benefit. Start conservatively.
- **Do not claim that skeleton screens make DashLens feel faster.** The cited evidence found no significant effect.

### Gaps
- Viget's numbers (n = 136; 2.82 / 2.41 / 2.29 s) remain unconfirmed because the site was unreachable.
- Mejtoft et al.'s sample size was not in the abstract; the ACM full text was unreachable (403).
- Nah (2004), the "3 times longer" waiting study, was not checked at source.

---

## 2. Stanford Web Credibility guidelines; Fogg et al. 2002 study figures

### Takeaway
The full list of ten guidelines is now confirmed from the Stanford page. The 46.1% "design look" figure is confirmed. It is 46.1% **of comments**, not of people: the executive summary itself says "nearly half of all consumers (or 46.1%)", which mixes the two. The report dates are settled: released 29 Oct 2002, data collected 15 June to 15 Aug 2002. The often-quoted line "To look good is to be good" is not in the report. A finding missing from the earlier notes is highly relevant to DashLens: **privacy policies were mentioned in under 1% of comments**.

### Cited Findings
**Stanford Guidelines for Web Credibility (Fogg, B.J., May 2002; page "Updated June, 2002")** — [credibility.stanford.edu/guidelines](https://credibility.stanford.edu/guidelines/)
- CONFIRMED (basis): "We have compiled 10 guidelines for building the credibility of a web site. These guidelines are based on three years of research that included over 4,500 people."
- CONFIRMED, the full list (exact wording):
  1. "Make it easy to verify the accuracy of the information on your site." The comment adds: "Even if people don't follow these links, you've shown confidence in your material."
  2. "Show that there's a real organization behind your site."
  3. "Highlight the expertise in your organization and in the content and services you provide."
  4. "Show that honest and trustworthy people stand behind your site."
  5. "Make it easy to contact you."
  6. "Design your site so it looks professional (or is appropriate for your purpose)." The comment adds: "We find that people quickly evaluate a site by visual design alone… The visual design should match the site's purpose."
  7. "Make your site easy to use -- and useful."
  8. "Update your site's content often (at least show it's been reviewed recently)."
  9. "Use restraint with any promotional content (e.g., ads, offers)." The comment adds: "Avoid pop-up ads… try to be clear, direct, and sincere."
  10. "Avoid errors of all types, no matter how small they seem." The comment adds: "Typographical errors and broken links hurt a site's credibility more than most people imagine. It's also important to keep your site up and running."
- NEW: the supporting study "ptl02" (Stanford-Makovsky 2002) is labelled on the page as a "Report from the Persuasive Technology Lab (not peer reviewed)".

**Fogg, Soohoo, Danielson, Marable, Stanford & Tauber, "How Do People Evaluate a Web Site's Credibility? Results from a Large Study" (Stanford PTL / Consumer WebWatch / Sliced Bread Design)** — [report PDF, Consumer Reports advocacy site](https://advocacy.consumerreports.org/wp-content/uploads/2013/05/stanfordPTL.pdf)
- CONFIRMED (sample and figure): "In this study, 2,684 people evaluated the credibility of two live Web sites on a similar topic… We found that the 'design look' of the site was mentioned most frequently, being present in 46.1 percent of the comments. Next most common were comments about information structure and information focus."
- CORRECTED (dates): the cover says "Report Released: October 29, 2002 / Report Updated on November 11, 2002 / Study term: June 15, 2002, to August 15, 2002." Recruiting began in May 2002. The earlier "May vs. October" conflict is therefore recruitment start vs. release.
- CORRECTED (unit): 46.1% is a share of **comments**. The executive summary words it loosely: "nearly half of all consumers (or 46.1%) in the study assessed the credibility of sites based in part on the appeal of the overall visual design of a site, including layout, typography, font size and color schemes."
- NEW (category split): visual-design comments were more frequent for "finance (54.6%), search engines (52.6%), travel (50.5%), and e-commerce sites (46.2%)" and less frequent for "health (41.8%), news (39.6%), and nonprofit (39.4%) sites."
- NEW (highly relevant to a privacy-first tool): "people rarely used these rigorous criteria when evaluating credibility (e.g., they almost never referred to a site's privacy policy.) We found a mismatch… between what people say is important and what they actually do." Also: "We found that people mentioned privacy policies in less than 1 percent of" the comments, and only 8.8% referred to the identity of the site or its operator.
- NEW (design of the study): "two live Web sites randomly assigned from one of 10 content categories (e-commerce, entertainment, finance, health, news, nonprofit, opinion or review, search engines, sports, and travel.) A total of 100 sites were assessed. We gathered the comments people wrote (2,440 in all)". The percentages are therefore shares of 2,440 comments, not of the 2,684 participants.
- NOT FOUND: the quote "To look good is to be good — that's the primary test…" does not appear in the report text. It comes from press coverage (InternetNews), so attribute it to press coverage, not to the report.

**Stanford, Tauber, Fogg & Marable (2002), "Experts vs. Online Consumers: A Comparative Credibility Study of Health and Finance Web Sites" (Consumer WebWatch)** — [PDF](https://advocacy.consumerreports.org/wp-content/uploads/2013/05/expert-vs-online-consumers.pdf)
- CONFIRMED with figures: "15 experts from the health and finance fields… A total of 8 health and 7 finance experts". "More than half (54.6%) of the comments by the consumers regarding finance sites referred to design look… compared to only 16.4 percent of finance expert comments… 41.8 percent of consumer comments regarding health sites made note of a site's design look, compared to 7.6 percent of surveyed health experts' comments."
- CONFIRMED: "our experts were far less concerned about visual appeal as a marker of credibility than the Stanford PTL consumers, and they were more concerned about the quality of a site's information."

**NN/g, "Prominence-Interpretation Theory" (Therese Fessenden, 19 Aug 2018)** — [NN/g](https://www.nngroup.com/articles/prominence-interpretation-theory/)
- CONFIRMED: "Prominence-interpretation theory suggests that people determine a site's credibility by judging prominent attributes of the site that grab their attention… Prominence refers to those salient elements of the site that stand out and that the users are likely to notice. Interpretation refers to how people judge those elements."

### Inferences
- **A privacy policy page alone will not build trust.** Users almost never looked at privacy policies (under 1% of comments). The "nothing is uploaded" promise must be a *prominent* element in the interface (prominence-interpretation), such as a line by the open-file control and a visible local-processing status, not a linked policy.
- **For insurers and other expert readers, content quality counts more than looks.** Experts weighted information quality far above design. The exported summary should stress verifiable facts (source file, timestamps, what was not altered) over styling. This matches guideline 1, "Make it easy to verify".
- **Errors and downtime damage credibility (guideline 10).** For a local tool, this includes a broken map tile, a typo in the export, or a wrong unit label.

### Gaps
- The 2003 peer-reviewed version (Fogg et al., DUX 2003, ACM) was unreachable (dl.acm.org 403). The figures above are from the 2002 report, which is the primary data source.
- No study was found on which privacy-reassurance wordings raise trust in local-only web apps (unchanged from before).

---

## 3. Aesthetics and usability: Kurosu & Kashimura 1995; Tractinsky 1997/2000; Lindgaard 2006; the study where poor usability outweighs aesthetics; aesthetics and performance

### Takeaway
The early studies are confirmed: aesthetics drives *apparent* usability before use, and in Tractinsky 2000 also after use. Later controlled studies qualify this. **Tuch et al. (2012, *Computers in Human Behavior*, N = 80)** is the study the question asks for: aesthetics did **not** affect perceived usability, while poor usability **lowered** post-use beauty ratings, through frustration. Grishin & Gillan (JUS) found that usability, not aesthetics, drove usability judgments. Lindgaard 2006 needs one correction: the 50 ms ratings were compared with **500 ms** ratings, not with "longer viewing" in general. One correction from the earlier notes matters for DashLens: aesthetics *can* improve performance, mainly when the task is hard (Reppa & McDougall 2015; Moshagen et al. 2009), and a meta-analysis found a small positive effect (g = 0.12).

### Cited Findings
**Kurosu & Kashimura (1995)**
- CONFIRMED (citation and finding): "Apparent usability vs. inherent usability: experimental analysis on the determinants of the apparent usability", *CHI '95 Conference Companion*, pp. 292–293, DOI 10.1145/223355.223680. The abstract (OCR-garbled in the index) says the "apparent usability is strongly affected by the aesthetic aspects rather than the inherent usability." — [OpenAlex record](https://api.openalex.org/works?filter=doi:10.1145/223355.223680); [DOI](https://doi.org/10.1145/223355.223680)
- NEW (companion paper): Kurosu & Kashimura, "Determinants of the apparent usability", IEEE SMC 1995, vol. 2, pp. 1509–1514. "In both experiments, two kinds of usability concepts showed low correlations with each other… the apparent usability… is rather related to the visual impression of the interface… interface designers have to make efforts to make the interface 'look' usable as well as to make it 'actually' usable." — [DOI](https://doi.org/10.1109/icsmc.1995.537986)
- NOT FOUND: the claims of an ATM-layout task, Japanese participants and the sample size. The ACM full text was unreachable, and the abstract does not say.

**Tractinsky (1997)**
- CONFIRMED (citation): "Aesthetics and apparent usability: empirically assessing cultural and methodological issues", *Proc. CHI '97*, pp. 115–122, DOI 10.1145/258549.258626. — [DOI](https://doi.org/10.1145/258549.258626)
- CORRECTED (the description of the replication): the Ben-Gurion University page cited earlier is titled "Replicating and extending research on relations between visual aesthetics and usability". It says: "This paper describes a replication and extension of a study that found strong positive correlation between evaluation of a product's beauty and pre-use perceptions of its usability. The original study was conducted in Japan; its replication and extension took place in Israel. The extension involved mainly methodological improvements to the original study, which demonstrated the robustness of the original study's findings." The page does **not** mention differences in correlation size between the samples, or a cross-cultural direction. That detail in the earlier notes is unconfirmed. — [BGU page](https://www.bgu.ac.il/en/researcher/noam-tractinsky/publications/351759634/)

**Tractinsky, Katz & Ikar (2000), "What is beautiful is usable", *Interacting with Computers* 13(2):127–145, DOI 10.1016/S0953-5438(00)00031-X**
- CONFIRMED (abstract via OpenAlex): "The experiment used a computerized application as a surrogate for an Automated Teller Machine (ATM)… Post-experimental measures indicated that the strong correlation remained intact. A multivariate analysis of covariance revealed that the degree of system's aesthetics affected the post-use perceptions of both aesthetics and usability, whereas the degree of actual usability had no such effect." — [OpenAlex record](https://api.openalex.org/works?filter=doi:10.1016/S0953-5438(00)00031-X); [DOI](https://doi.org/10.1016/S0953-5438(00)00031-X)
- NOT FOUND: the sample size (not in the abstract; OUP and the Aalto PDF were unreachable or behind a login).

**Lindgaard, Fernandes, Dudek & Brown (2006), "Attention web designers: You have 50 milliseconds to make a good first impression!", *Behaviour & Information Technology* 25(2):115–126, DOI 10.1080/01449290500330448**
- CONFIRMED (citation and headline): "visual appeal can be assessed within 50 ms, suggesting that web designers have about 50 ms to make a good first impression." — [abstract via OpenAlex](https://api.openalex.org/works?filter=doi:10.1080/01449290500330448); [Crossref](https://api.crossref.org/works/10.1080/01449290500330448)
- CORRECTED (design): there were three studies. Studies 1 and 2 used **500 ms** exposures. Study 3 "replicated the 500 ms condition as well as adding a 50 ms condition… visual appeal ratings were highly correlated from one phase to the next as were the correlations between the 50 ms and 500 ms conditions." So 50 ms ratings matched 500 ms ratings, not ratings after long viewing. Study 2 also found "Visual appeal was found to be closely related to most of" seven design dimensions.
- CONFIRMED (the 500 ms quote): Nature news, 13 Jan 2006: "'My colleagues believed it would be impossible to really see anything in less than 500 milliseconds,' says Gitte Lindgaard of Carleton University". — [Nature news](https://www.nature.com/news/2006/060109/full/news060109-13.html)
- NOT FOUND: the "1–100 scale" detail (not in the abstract; the full text was unreachable). Note that the "halo effect" framing in the Nature piece is the journalist's paraphrase of Lindgaard's comments, not a finding of the paper.

**What drives first impressions: Tuch, Presslaber, Stöcklin, Opwis & Bargas-Avila (2012), "The role of visual complexity and prototypicality regarding first impression of websites"**
- CONFIRMED and authors now verified: "119 screenshots of real websites varying in VC (low vs. medium vs. high) and PT (low vs. high) were rated on perceived aesthetics… Results reveal that VC and PT affect participants' aesthetics ratings within the first 50 ms of exposure… Results suggest that VC and PT affect aesthetic perception even within 17ms, though the effect of PT is less pronounced than the one of VC." — [Google Research PDF](https://research.google.com/pubs/archive/38315.pdf)

**The study where poor usability outweighs aesthetics: Tuch, Roth, Hornbæk, Opwis & Bargas-Avila (2012), "Is beautiful really usable? Toward understanding the relation between usability, aesthetics, and affect in HCI", *Computers in Human Behavior* 28(5):1596–1607, DOI 10.1016/j.chb.2012.03.024**
- IDENTIFIED and CONFIRMED (citation): [University of Copenhagen research profile](https://researchprofiles.ku.dk/da/publications/is-beautiful-really-usable-toward-understanding-the-relation-betw/)
- CONFIRMED (design and findings), from the authors' Google Research blog post: "we conducted an experimental lab study with 80 participants. We created four versions of an online clothing shop varying in beauty (high vs. low) and usability (high vs. low)… The results showed that the beauty of the interface did not affect how users perceived the usability of the shops… However, the experiment showed that the usability of the shops influenced how users rated the products' beauty… poor usability lead to frustration, which put the users in a bad mood and made them rate the product as less beautiful than before interacting with the shop." — [Google Research blog](https://www.research.google/blog/is-beautiful-usable-what-is-the-influence-of-beauty-and-usability-on-reactions-to-a-product/)

**Grishin & Gillan, "Exploring the Boundary Conditions of the Effect of Aesthetics on Perceived Usability", *Journal of Usability Studies* (Feb 2019)**
- CORRECTED (authors, date): the authors are John Grishin and Douglas J. Gillan. The work began as Grishin's NC State thesis (2018). — [NCSU repository record via OpenAlex](https://api.openalex.org/works?search=Exploring%20the%20Boundary%20Conditions%20of%20the%20Effect%20of%20Aesthetics%20on%20Perceived%20Usability)
- NOT FOUND at primary: the JUS article page now redirects to the new *Journal of User Experience* site, and the PDF (`JUS_Grishin_Feb2019.pdf`) returns 404. A secondary summary by TC Camp describes two experiments with a 2×2 design (aesthetics × usability) and reports that "aesthetics didn't factor much into users' perceptions of usability at all." — [TC Camp summary](https://tccamp.org/viewpoints/beautys-in-the-eye-of-the-user). Sample size unknown.

**Aesthetics and performance (corrects the earlier "Effect on performance is mixed" item)**
- CORRECTED (what PMC4577531 is): it is not a review. It is an empirical Brief Report: Reppa & McDougall (2015), "When the going gets tough the beautiful get going: aesthetic appeal facilitates task performance", *Psychonomic Bulletin & Review*, DOI 10.3758/s13423-014-0794-z. In icon-search tasks, "icons that were appealing were found more quickly than their unappealing counterparts… appeal can influence performance, especially under duress", and gave "no benefits when the task was made easier". Its introduction says: "The handful of studies examining whether visual aesthetic appeal might influence performance has yielded mixed support". — [PMC4577531](https://pmc.ncbi.nlm.nih.gov/articles/PMC4577531/)
- CONFIRMED (the "only on low-usability websites" study is Moshagen et al. 2009, as described by Reppa & McDougall): "When the website was highly usable, appeal made no difference in the two performance measures. However, for websites of low usability… aesthetic appeal led to better task performance." — [PMC4577531](https://pmc.ncbi.nlm.nih.gov/articles/PMC4577531/)
- NEW (fills an old gap): Sonderegger & Sauer (2010), *Applied Ergonomics* 41(3):403–410. With 60 adolescents (14–17 years) using two functionally identical simulated phones, "participants using the highly appealing phone rated their appliance as being more usable… Furthermore, the visual appearance of the phone had a positive effect on performance, leading to reduced task completion times for the attractive model." — [PubMed 19892317](https://pubmed.ncbi.nlm.nih.gov/19892317/)
- NEW: Perrig, Ueffing, Opwis & Brühlmann (2023), *Frontiers in Psychology*. In an online experiment (N = 281), "results point toward a positive impact of interface aesthetics on performance (i.e., the number of questions answered correctly)." They report that a meta-analysis by Thielsch et al. (2019) found "a small, positive effect of interface aesthetics on user performance (g = 0.12)". — [PMC10306164](https://pmc.ncbi.nlm.nih.gov/articles/PMC10306164/)
- NEW (counter-evidence on the halo): Hamborg, Hülsmann & Kaspar (2014), *Advances in Human-Computer Interaction*, N = 88, mobile phone prototype: "the mobile phone's aesthetics does not affect its perceived usability, either directly or indirectly. Instead, results revealed an effect of usability on perceived beauty". — [DOI 10.1155/2014/946239](https://doi.org/10.1155/2014/946239)

### Inferences
- **The halo effect is real before use but fragile during use.** Tuch 2012, Hamborg 2014 and Grishin & Gillan all find that when people actually use a product and usability is poor, perceived usability follows the real usability, and poor usability then makes the product look *less* beautiful. For DashLens: polish wins the first 50 ms, but a broken export or a hard-to-find event will make the whole app feel worse, frustration included.
- **Visual quality may matter most at the hardest moment.** Reppa & McDougall and Moshagen et al. found that appeal helped performance mainly when the task was hard ("under duress"). This gives tentative support, not proof, for investing in clear, attractive visuals in the incident flow, such as legible event markers and timeline icons, where the stressed user's task is hardest.
- **Keep the first screen simple and familiar.** Tuch et al.'s first-impression work shows that low visual complexity and high prototypicality (looking like what users expect) drive appeal within 17–50 ms. A simple, familiar file-open screen makes the best first impression.

### Gaps
- Sample sizes for Kurosu & Kashimura 1995 and Tractinsky 1997/2000 are not confirmed; the full texts were unreachable.
- The Grishin & Gillan full text (sample, effect sizes) was unreachable; only a secondary summary was read.
- The Thielsch et al. (2019) meta-analysis was not read directly; g = 0.12 is as reported by Perrig et al. 2023.
- Still no study of the aesthetics-usability effect under acute stress, or for video or telemetry tools.

---

## 4. Other studies: Shields 2016; Ghibellini & Meier 2025; Mathur 2019; Kivetz 2006; the 2024/2025 colour-emotion review; peak-end; red-effect replications

### Takeaway
All of these citations are confirmed, with some corrections. Ghibellini & Meier's figures (0.99 ratio over 37/38 publications; 67% resumption over 21 publications) are now confirmed from the paper. Two corrections: the colour review covers **132 articles, 42,266 participants and 64 countries**, and appeared in journal issue **32(4), 2025**, online 13 Jan 2025. The colonoscopy return-visit effect is real but **"slightly higher" (OR 1.41)**, not dramatic.

### Cited Findings
**Shields, Sazma & Yonelinas (2016), "The effects of acute stress on core executive functions: A meta-analysis and comparison with cortisol", *Neurosci Biobehav Rev* 68:651–668**
- CONFIRMED: "We found that stress impaired working memory and cognitive flexibility, whereas it had nuanced effects on inhibition. Many of these effects were moderated by other variables, such as sex." — [PubMed 27371161](https://pubmed.ncbi.nlm.nih.gov/27371161/)
- NEW: stress produces "a state characterized by more reactive processing of salient stimuli but greater control over actions." — same source.

**Ghibellini & Meier (2025), "Interruption, recall and resumption: a meta-analysis of the Zeigarnik and Ovsiankina effects", *Humanities and Social Sciences Communications*, published 1 July 2025, DOI 10.1057/s41599-025-05000-w**
- CONFIRMED: "We found no memory advantage for unfinished tasks but found a general tendency to resume tasks… Conclusively, the Ovsiankina effect represents a general tendency, whereas the Zeigarnik effect lacks universal validity." — [Nature (publisher)](https://www.nature.com/articles/s41599-025-05000-w)
- CONFIRMED (0.99 ratio; the earlier notes had this from a blog): "a weighted ratio mean(IR)/mean(CR) = 0.99 resulted (N = 38 publications)… If Zeigarnik (1927) is excluded… 0.99 persists (N = 37 publications)". — same source
- CONFIRMED (67% resumption): "a weighted resumption rate (%) = 67.00% results (N = 21 publications)… interrupted tasks are resumed roughly 67% of the time… well above the chance rate of 50%." — same source
- NEW (nuance): Zeigarnik's own measure, mean ratio IR/CR, gave 1.13 (N = 7 publications), or 1.09 without Zeigarnik herself. The authors say "the values from Zeigarnik's (1927) original computations are inflated." The method is a sample-size-weighted mean of measures across publications, not a standard effect-size meta-analysis; the authors say most studies "did not report any effect size". — same source

**Mathur, Acar, Friedman, Lucherini, Mayer, Chetty & Narayanan (2019), "Dark Patterns at Scale: Findings from a Crawl of 11K Shopping Websites", *Proc. ACM HCI* 3(CSCW), Article 81, DOI 10.1145/3359183**
- CONFIRMED: "Analyzing ~53K product pages from ~11K shopping websites, we discover 1,818 dark pattern instances, together representing 15 types and 7 broader categories… find 183 websites that engage in such practices. We also uncover 22 third-party entities that offer dark patterns as a turnkey solution." — [arXiv 1907.07032](https://arxiv.org/abs/1907.07032)
- CONFIRMED (1,254 sites; low estimate): "These 1,818 dark patterns were found on 1,254 of the ∼11K shopping websites (∼11.1%)… These numbers represent a lower bound". — [arXiv PDF](https://arxiv.org/pdf/1907.07032)
- CONFIRMED with detail: "We uncovered 234 instances of dark patterns—across 183 websites—that exhibit deceptive behavior." Countdown timers and testimonials were among the practices examined, for example offers that remain valid "even after the countdown timer of 60 minutes expires." — same PDF
- NEW: "Shopping websites that were more popular, according to Alexa rankings, were more likely to feature dark patterns." — same PDF

**Kivetz, Urminsky & Zheng (2006), "The Goal-Gradient Hypothesis Resurrected: Purchase Acceleration, Illusionary Goal Progress, and Customer Retention", *Journal of Marketing Research* Vol. XLIII (Feb 2006), 39–58**
- CONFIRMED: "(1) participants in a real café reward program purchase coffee more frequently the closer they are to earning a free coffee; (2) Internet users who rate songs in return for reward certificates visit the rating Web site more often, rate more songs per visit, and persist longer… (3) the illusion of progress toward the goal induces purchase acceleration (e.g., customers who receive a 12-stamp coffee card with 2 preexisting 'bonus' stamps complete the 10 required purchases faster than customers who receive a 'regular' 10-stamp card); and (4) a stronger tendency to accelerate toward the goal predicts greater retention". — [Columbia PDF](https://business.columbia.edu/sites/default/files-efs/pubfiles/1200/goalgradient.pdf)
- CORRECTED (minor): the paper says the hypothesis was "originally proposed by the behaviorist Clark Hull in 1932". Hull (1934) is the classic rat experiment it cites. — same source

**Colour–emotion systematic review: Jonauskaite & Mohr, "Do we feel colours? A systematic review of 128 years of psychological research linking colours and emotions", *Psychonomic Bulletin & Review* 32(4):1457–1486; online 13 Jan 2025 (print Aug 2025), DOI 10.3758/s13423-024-02615-z**
- CORRECTED (date and scope): it is listed as "2024" in the earlier notes because of the DOI, but it was published online in January 2025. "we identified 132 relevant peer-reviewed articles published in English between 1895 and 2022. These articles covered a total of 42,266 participants from 64 different countries." — [abstract via Crossref](https://api.crossref.org/works/10.3758/s13423-024-02615-z); [Springer](https://link.springer.com/article/10.3758/s13423-024-02615-z)
- CORRECTED (the arousal mapping is more nuanced): "(i) LIGHT and DARK colours were associated with positive and negative emotions, respectively; (ii) RED with empowering, high arousal positive and negative emotions; (iii) YELLOW and ORANGE with positive, high arousal emotions; (iv) BLUE, GREEN, GREEN–BLUE, and WHITE with positive, low arousal emotions; … (vii) GREY with negative, low arousal emotions; and (viii) BLACK with negative, high arousal emotions." The effects are "driven by lightness, saturation, and hue". So grey is **negative**, low arousal, not neutral.
- CONFIRMED (associations, not felt effects): "As most colour–emotion correspondences were tested on an abstract level (i.e., associations), it remains to be seen whether such correspondences translate to the impact of colour on experienced emotions and specific contexts."

**Red-effect replications**
- CONFIRMED: Gnambs et al., "Processing the Word Red and Intellectual Performance: Four Replication Attempts", *Collabra: Psychology* (2020), DOI 10.1525/collabra.277. Ns = 69, 104, 103 and 1,149. "these results do not corroborate the assumption that processing the word red impairs intellectual performance." — [DOI](https://doi.org/10.1525/collabra.277)
- CONFIRMED with figures: "Limited evidence for the effect of red color on cognitive performance: A meta-analysis" (*Psychon Bull Rev*, 2020). It covers "67 effect sizes (38 samples)… After correcting for publication bias no evidential value for an effect of red color on intellectual performance was available." — [DOI 10.3758/s13423-020-01772-1](https://doi.org/10.3758/s13423-020-01772-1)
- CONFIRMED (field still young): Elliot & Maier, *Annual Review of Psychology* (vol. 65, 2014; online 2013): "The literature remains at a nascent stage of development… considerable work on boundary conditions, moderators, and real-world generalizability is needed before strong conceptual statements and recommendations for application are warranted." — [DOI 10.1146/annurev-psych-010213-115035](https://doi.org/10.1146/annurev-psych-010213-115035)
- CONFIRMED (Palmer & Schloss is about preference, which the earlier notes flagged as unchecked): Schloss & Palmer (2017) summarise Ecological Valence Theory as stating "that preference for a given color is determined by the combined valence (liking/disliking) of all objects and events associated with that color." — [PubMed 28456532](https://pubmed.ncbi.nlm.nih.gov/28456532/)

**Peak-end**
- CONFIRMED: Kahneman, Fredrickson, Schreiber & Redelmeier (1993), *Psychological Science*: a 60 s cold-water trial at 14 °C vs. the same plus 30 s more as the water rose to 15 °C. "A significant majority chose to repeat the long trial… such evaluations are often dominated by the discomfort at the worst and at the final moments of episodes." — [DOI 10.1111/j.1467-9280.1993.tb00589.x](https://doi.org/10.1111/j.1467-9280.1993.tb00589.x)
- CONFIRMED: Redelmeier & Kahneman (1996), *Pain* 66:3–8. Colonoscopy n = 154, lithotripsy n = 133. "Patients' judgments of total pain were strongly correlated with the peak intensity of pain (P < 0.005) and with the intensity of pain recorded during the last 3 min… lengthy procedures were not remembered as particularly aversive." — [PubMed 8857625](https://pubmed.ncbi.nlm.nih.gov/8857625/)
- CORRECTED (size of the return-visit effect): Redelmeier, Katz & Kahneman (2003), *Pain* 104:187–194, a randomised trial with n = 682. Return rates "averaged 50.4% and were slightly higher (odds ratio=1.41, P=0.038) for those who underwent the longer procedure". The extended group rated the final moments 1.7 vs. 2.5 and the whole experience 4.4 vs. 4.9. — [PubMed 12855328](https://pubmed.ncbi.nlm.nih.gov/12855328/)
- NOT FOUND: the "rated every 60 s" and "4–69 min" duration details. They are not in the abstracts.

### Inferences
- **Resume, don't nag.** The Ovsiankina finding (about 67% resumption) supports a local-only "Resume where you left off" offer. The Zeigarnik "unfinished tasks stick in memory" claim should not be used to justify persistent incomplete-task badges.
- **Use a calm palette without claiming it calms people.** The colour review shows associations, not felt effects. Large areas of mid-grey are associated with *negative* low-arousal emotion. A neutral base is fine for letting the video stand out, but lighter neutrals, or a restrained blue or green accent, fit the "positive, low arousal" associations better than flat grey. Keep red for real problems; it is associated with high arousal of both positive and negative kinds.
- **Design the end of the flow, but expect modest gains.** Peak-end is robust, but the clinical effect on behaviour (returning for a repeat colonoscopy) was modest (OR 1.41). A good completion screen is worth building, but it will not save a bad flow.

### Gaps
- The 2024 *Brain, Behavior, & Immunity – Health* stress-decision review (PMC11407068) was not re-checked; the PMC site showed a reCAPTCHA to the fetcher, and I had no confirmed DOI.
- The authors and full text of the "Men in red" reexamination (DOI 10.3758/s13423-015-0866-8) were not retrieved; the abstract was not in the index.
- The anxiety–attention reviews (PMC2933078, PubMed 12916567), Hick's law and Shneiderman's golden rules from the earlier notes were not re-verified in this pass.

---

## 5. Maister, "The Psychology of Waiting Lines"; the origin of the Doherty threshold

### Takeaway
Maister's propositions are confirmed from the full text on his site. There are **eight** waiting propositions, plus "S = P – E", the "First Law of Service". The "told 30 minutes, took 25 / 35" example is **not** in Maister's text. For Doherty, Laws of UX's claim that the paper appeared in the *IBM Systems Journal* is **not supported** by Crossref. The 1982 paper appears to be an IBM publication (form GE20-0752-0) hosted on an IBM site this session could not reach. The peer-reviewed IBM Systems Journal paper on this topic is Thadhani (1981).

### Cited Findings
**Maister, D. (1985), "The Psychology of Waiting Lines", in Czepiel, Solomon & Surprenant (eds.), *The Service Encounter*, Lexington Books** — [davidmaister.com full text](https://davidmaister.com/articles/the-psychology-of-waiting-lines/)
- CONFIRMED (source): "This article is from THE SERVICE ENCOUNTER edited by John a Czepiel, Michael R. Solomon and Carol Suprenant, © 1985 by D.C. Heath and Company, Lexington Books."
- CONFIRMED, the propositions (headings, exact wording): "Occupied Time Feels Shorter Than Unoccupied Time." / "People Want to Get Started." / "Anxiety Makes Waits Seem Longer." / "Uncertain Waits Are Longer than Known, Finite Waits" / "Unexplained Waits Are Longer than Explained Waits" / "Unfair Waits Are Longer than Equitable Waits" / "The More Valuable the Service, the Longer the Customer Will Wait" / "Solo Waits Feel Longer than Group Waits".
- NEW: the "First Law of Service" is "S = P – E", where "'S' stands for satisfaction, 'P' for perception and 'E' for expectation." The "Second Law of Service" is "It's hard to plan catch-up ball."
- CONFIRMED (fear of being forgotten): "one's 'anxiety' level is much higher while waiting to be served than it is while being served, even though the latter wait may be longer. There is a fear of 'being forgotten'."
- CONFIRMED (uncertainty): "The most profound source of anxiety in waiting is how long the wait will be." And: "Waiting in ignorance creates a feeling of powerlessness".
- NEW (managing expectations): Maister reports Sasser et al.'s example: "some restaurants follow the practice of promising guests a waiting time in excess of the 'expected time'. If people are willing to agree to wait this length of time, they are quite pleased to be seated earlier".
- NOT FOUND in Maister: the "told 30 minutes and it takes 25 → lucky; 35 → cheated" example. It probably comes from the UEN textbook chapter cited earlier, not from Maister. Cite it to UEN, or drop it.
- NEW: Maister presents these as "testable propositions offering the opportunity for future research". They are conceptual, not experimental findings, which confirms the earlier grading.

**Doherty threshold**
- CONFIRMED (Laws of UX wording): "Productivity soars when a computer and its users interact at a pace (<400ms) that ensures that neither has to wait on the other." Origins: "In 1982 Walter J. Doherty and Ahrvind J. Thadani published, in the IBM Systems Journal, a research paper that set the requirement for computer response time to be 400 milliseconds, not 2,000 (2 seconds) which had been the previous standard." Takeaway: "Provide system feedback within 400 ms in order to keep users' attention and increase productivity." — [Laws of UX](https://lawsofux.com/doherty-threshold/)
- CORRECTED / unconfirmed venue: Crossref holds no "Economic Value of Rapid Response Time" article in the *IBM Systems Journal*. Search results describe an IBM-hosted copy carrying "© Copyright IBM Corporation 1982, 1997" and form number GE20-0752-0, i.e. an IBM publication, not a journal article. That host (www.vm.ibm.com) could not be reached here, so the 400 ms figure and the exact claims are **not confirmed at the primary source**. — [IBM copy (unreachable here)](https://www.vm.ibm.com/devpages/jelliott/evrrt1.html)
- NEW (related peer-reviewed work): Thadhani, A.J. (1981), "Interactive user productivity", *IBM Systems Journal* 20(4):407–423, DOI 10.1147/sj.204.0407. "the cost of the aggregate user time being the dominant component… computer systems should be managed for maximum user effectiveness rather than for maximum machine usage." The correct spelling of the co-author is likely "Thadhani". — [DOI](https://doi.org/10.1147/sj.204.0407)
- NEW: Laws of UX also says "Purposefully adding a delay to a process can actually increase its perceived value and instill a sense of trust". That is a practitioner claim with no source on the page; do not use it for DashLens (see Inferences).

### Inferences
- **Every Maister rule has a DashLens counterpart.** Explained waits ("Reading GPS from 14 clips"), finite waits (counts, not spinners), occupied waits (let the user scrub while indexing), and "being forgotten" (export progress that persists until a clear completion state).
- **Promise conservatively.** S = P – E and the restaurant example agree with NN/g's advice to start progress slowly and allow extra time. An honest, slightly cautious estimate that is beaten feels better than an optimistic one that is missed.
- **Do not add fake delays** to look thorough. For a forensic-adjacent tool that promises honesty, an artificial "analysing…" pause would be a dark pattern in spirit.

### Gaps
- The Doherty & Thadhani (1982) text could not be read. The 400 ms figure rests on Laws of UX and secondary sources.
- The Kent Beck "Precious Eyeblink" critique and the UX Collective "two clocks" piece were not re-checked.

---

## 6. Style guidance: Atlassian voice and tone; Mailchimp; GOV.UK error messages; Chayn trauma-informed design; NN/g on delight and progressive disclosure

### Takeaway
All four guides were read at source. The guidance that fits DashLens best is GOV.UK's: "Avoid things like humorous error messages. People often use government services for serious things or when under stress." Atlassian is the other: when a person feels "overwhelmed, unsure, hesitant, stressed" (for example "being blocked by errors"), be *more practical*, and "Delight means little flourishes, not humor or being cheeky." Mailchimp has two descriptions of its voice (TL;DR vs. full page). Chayn has two versions of its principles: 9 in Hussain's 2021 article, and 8 in the later set.

### Cited Findings
**Atlassian Design System, "Voice and tone"** — [atlassian.design](https://atlassian.design/foundations/content/voice-tone)
- FILLS GAP (traits): the personality traits are "Bold", "Optimistic" and "Practical, with a wink".
- NEW: "Tone is how we express Atlassian's voice, and it should change depending on the situation the user is in (for example, receiving an error versus successfully completing a project)." Writers should ask: "What is the emotional state of the user when they encounter your content…?" and "How might our personality traits diffuse a moment of frustration or pain?"
- NEW (when to be less bold): "Person is feeling: apprehension, confusion, annoyance, fear, anger. Examples: new users, trial users…"
- NEW (when to be more practical): "Person is feeling: overwhelmed, unsure, hesitant, stressed. Examples: people with deadlines or being blocked by errors, supporting new or occasional users". The "wink" "isn't always appropriate to use. Be mindful of where someone is at and what they might be experiencing before going beyond the practical." Add the wink only when the person is feeling "successful, joy, proud, relief."
- NEW (principles): "Inform to build trust", used "In confusing, warning, or error states": "Tell people only what they need to know in the moment and nothing more." Also "Satisfy by meeting expectations": "Simply tell people what they need to know and get out of the way."
- NEW (delight): "You can deliver appropriate delight (a 'wink') by celebrating success or progress, but only once you've built trust. Don't overdo it. Delight means little flourishes, not humor or being cheeky… Think about the timing and how frequently a user will see this. Once may amuse, but a dozen times…" (the sentence is cut off in the fetched text).

**Mailchimp Content Style Guide** — [Voice and Tone](https://styleguide.mailchimp.com/voice-and-tone/); [TL;DR](https://styleguide.mailchimp.com/tldr/)
- CONFIRMED (TL;DR): "Mailchimp's voice is: Human / Familiar / Friendly / Straightforward". Also: "We have a sense of humor, but we value clarity over entertainment." And: "Lead with the main point or the most important content."
- CORRECTED (the full Voice and Tone page lists different traits): "We are plainspoken… We are genuine… We are translators… Our humor is dry." The two pages differ; cite the one you mean.
- CONFIRMED (voice steady, tone changes): "You have the same voice all the time, but your tone changes… You wouldn't want to use the same tone of voice with someone who's scared or upset as you would with someone who's laughing."
- CONFIRMED (straight face): "it's always more important to be clear than entertaining… don't go out of your way to make a joke—forced humor can be worse than none at all. If you're unsure, keep a straight face."
- NEW: "we avoid distractions like fluffy metaphors and cheap plays to emotion."

**GOV.UK Design System, "Error message"** — [design-system.service.gov.uk](https://design-system.service.gov.uk/components/error-message/)
- CONFIRMED (now from source; the earlier notes relied on other departments' summaries): "In the error message explain what went wrong and how to fix it." / "Describe what has happened and tell them how to fix it. The message must be in plain English, use positive language and get to the point."
- CONFIRMED with exact list: "Do not use: technical jargon like 'form post error', 'unspecified error' and 'error 0x0000000643'; words like 'forbidden', 'illegal', 'you forgot' and 'prohibited'; 'please' because it implies a choice; 'sorry' because it does not help fix the problem; 'valid' and 'invalid' because they do not add anything to the message; humourous, informal language like 'oops'".
- CONFIRMED (hint text): "Do not give an example in the error message if there is an example on the screen."
- CONFIRMED (match the label): "Error messages should directly include language from the question or fieldset label."
- NEW (be specific): avoid "'An error occurred'… 'This field is required'". "Different errors need different messages."
- NEW (problems the user cannot fix): "Do not use error messages to tell a user… about a lack of capacity or other problem the user cannot fix - because the problem is with the service… Instead, take the user to a page that explains the problem… and provides useful information about what to do next."
- NEW: "Do not clear any form fields when showing the Error message component."

**GOV.UK Service Manual, "Writing for user interfaces"** — [gov.uk](https://www.gov.uk/service-manual/design/writing-for-user-interfaces)
- NEW (highly relevant): "Avoid things like humorous error messages. People often use government services for serious things or when under stress." Also: "If people do not notice your copy, you're probably doing it right. Aim to be boring."
- NEW (when sorry is acceptable): "Say 'sorry' if something serious has gone wrong - for example, the service has stopped working completely." "There's no need to say 'sorry' in validation error messages."
- NEW (terse errors): "do not say 'You have entered the wrong password'. Say 'Wrong password'."
- NEW (contractions): avoid "negative contractions like 'can't' and 'don't' - some users find them harder to read, or misread them as the opposite of what they say". This bears on DashLens copy such as "can't read this file".
- NEW: "Do not rely on shape, size, colour or location alone to communicate information".

**Chayn trauma-informed design**
- CONFIRMED (trust and safety first), from Hera Hussain, "Trauma-informed design: understanding trauma and healing", UX Magazine, 30 Jun 2021: "Chayn is a survivor-led community, which means we practise trauma-informed design and prioritise trust and safety over aesthetic or simplicity." — [UX Magazine](https://uxmag.com/articles/trauma-informed-design-understanding-trauma-and-healing). CORRECTED attribution: this sentence is not on the Promo Cymru page the earlier notes cited for it.
- CONFIRMED (provisional): "These principles may continue to evolve over time" and "I expect these to change in the future too". — UX Magazine, same article
- CORRECTED (two versions): the 2021 article lists **nine**: "Safety", "Trustworthy", "Plurality", "Agency", "Open and accountable", "Solidarity", "Empathy", "Friction and privacy", "Hope". The later set on Promo Cymru (written "with help from Hera Hussain") has **eight**: safety, agency, equity, privacy, accountability, plurality, sharing power, hope. — [UX Magazine](https://uxmag.com/articles/trauma-informed-design-understanding-trauma-and-healing); [Promo Cymru](https://promo.cymru/resource/trauma-informed-design-an-introduction-for-non-profits)
- NEW (consistency builds trust): "Trustworthy: Build trust with transparent, clear and consistent communication and design. People who experience trauma have often lived through internal and external unpredictability… One way to build trust is to be consistent and predictable." — UX Magazine
- NEW (friction): "We should remove unnecessary obstacles from users getting to the information and help they require, although some friction is necessary to protect user data and personal rights." — UX Magazine
- NEW (privacy, applies to video): "A survivor's personal information including their trauma story – such as data, images, videos, or statements – must be kept secure and not disclosed, unless the survivor decides to do so." — [Promo Cymru](https://promo.cymru/resource/trauma-informed-design-an-introduction-for-non-profits)
- NEW (accountability): "being open and transparent about what is being done, how, and why… To build trust, this communication should be clear and consistent." — Promo Cymru
- NEW (hope): "Users do not need harsh words and sad pictures that remind them of their struggles… Interventions should be designed to be an oasis for users. This means being empathetic, warm and soothing." — Promo Cymru
- NEW (expect triggers): "It's impossible that your services won't trigger someone at some point. Taking a trauma-informed approach means: Having a plan to mitigate the impact when these triggers happen". — Promo Cymru
- NOT FOUND: Chayn's own principles page (chayn.co links to blog.chayn.co, which was unreachable) and the "Bloom" consistency post on blog.chayn.co.

**NN/g, delight and progressive disclosure**
- CONFIRMED: Therese Fessenden, "A Theory of User Delight" (5 Mar 2017): "UI embellishments can only produce surface delight; deep delight can only be achieved in functional, reliable, and usable interfaces." On Walter: "superior needs (such as pleasure and delight…) can only be achieved after more foundational ones (such as functionality and usability) are fulfilled… a product can be delightful only if it is usable." — [NN/g](https://www.nngroup.com/articles/theory-user-delight/)
- CONFIRMED: Fessenden, "Pillars of User Delight" (27 Nov 2022): delight is "experienced viscerally, behaviorally, and reflectively" (Norman's levels used as pillars). — [NN/g](https://www.nngroup.com/articles/pillars-user-delight/)
- CONFIRMED: Jakob Nielsen, "Progressive Disclosure" (3 Dec 2006): "Initially, show users only a few of the most important options." "By hiding the advanced settings, progressive disclosure helps novice users avoid mistakes". "designs that go beyond 2 disclosure levels typically have low usability because users often get lost when moving between the levels. If you have so many features that you need 3 or more levels, consider simplifying your design." — [NN/g](https://www.nngroup.com/articles/progressive-disclosure/)

### Inferences
- **The incident flow should be boring.** GOV.UK ("Aim to be boring"; no humour because people are "under stress") and Atlassian (be more practical when "stressed… blocked by errors") give an explicit, sourced basis for a plain, joke-free incident flow. Keep any wink for success states such as "Clip saved", and keep it to small flourishes, not humour.
- **An error-copy checklist for DashLens, from GOV.UK.** Say what happened and how to fix it. No "please", "sorry", "invalid" or "oops". Be specific to the cause. Avoid negative contractions ("cannot read" rather than "can't read"). For problems the user cannot fix (an unsupported codec), give an explanation and a next step, not a red inline error. Keep everything the user has already done (marked ranges, settings) when an error occurs.
- **Treat incident footage as sensitive personal media.** Chayn names "videos" in its privacy principle and accepts "some friction… to protect user data". For DashLens this supports local-only storage, explicit export, and not autoplaying footage of the crash.
- **Consistency is a trust feature.** Chayn's "consistent and predictable" fits with GOV.UK's rule that the inline message and the summary should "look, sound and mean the same".

### Gaps
- Chayn's own principles page on chayn.co/blog.chayn.co could not be reached. The 8-principle list is confirmed only through Promo Cymru's co-written resource.
- The Contentful "delight scale" and UserTesting items from the earlier notes were not re-checked; they are low-weight practitioner sources.
- Norman's "attractive things work better" (jnd.org) was not re-checked in this pass.
