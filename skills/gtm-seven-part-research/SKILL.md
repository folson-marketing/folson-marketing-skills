---
name: gtm-seven-part-research
description: "Run a data-backed GTM analysis using Frank's seven-part framework (User insight, Product design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization) with Apify MCP research, a full competitor sweep, and a styled HTML report plus a Markdown report. Use for any new product, idea, or client GTM."
---

# GTM Seven-Part Research

You are a senior GTM strategist. This skill runs one product or idea through the seven parts of go-to-market below, backs every part with real data pulled through the Apify MCP, runs a full competitor sweep inside the Brand positioning part, and ends with a styled, self-contained HTML report backed by a supplemental Markdown file.

The seven parts are one chain, and the order is the point. What you learn about users shapes the product, the product shapes the positioning, the positioning becomes content, content goes out through channels, channels bring people to a conversion, and the conversion data shows where the path leaks, which sends you back to users. Do the parts in order. Never write a later part from guesswork when an earlier part has not been researched.

| # | Part | Question it answers |
|---|---|---|
| 1 | User insight | Who are these people, what do they struggle with, in their own words, and which five of them do we go after first? |
| 2 | Product design | What is the smallest product that solves that exact moment, and what do we cut? |
| 3 | Brand positioning | What do they use today instead, who else serves them, and what is the one sentence that says why we are the better answer? |
| 4 | Content strategy | How does that sentence become things people read, watch, and share, in the right format for each place? |
| 5 | Marketing channels | Which single channel do we master first, and with what cadence? |
| 6 | Conversion strategy | What do we ask for, when, and how do we make it small and visible? |
| 7 | Path optimization | Where does the funnel leak, which one number proves real value, and which part do we revisit when it is flat? |

## Standing rules

- Write with no dashes (no em dashes, en dashes, or "--"). Use commas, colons, or separate sentences. This applies to the HTML report's copy as much as the Markdown.
- Save raw data before analysing it. Never overwrite a file; append or create a new version.
- If a research call returns nothing, create the file anyway and write "No data found" with the reason.
- If an actor fails, a site blocks you, or the Apify MCP is unavailable, note it in the file and continue with WebSearch and WebFetch as the fallback.
- Save a checkpoint file after each part so the run can resume.
- All intake, raw-data, and checkpoint files are clean Markdown. The final deliverable is two files: `report.html`, a styled, self-contained HTML report that is the primary thing the user reads, and `report.md`, a supplemental plain-Markdown version carrying the same content in fuller narrative form. Never ship one without the other.
- If a Folson client brief exists for this product (`client-brief.md` in a connected client folder), read it first and reuse its competitor list, keywords, and positioning notes.

## Folder layout

Create `gtm-research/<project-slug>/` in the working directory (or inside the connected client folder if one exists):

```
intake.md                          answers from Phase 0
raw-data/01-user-insight.md        raw pulls, one file per part
raw-data/02-product-design.md
raw-data/03-positioning.md         competitor map and status quo
raw-data/03-competitor-<slug>.md   one file per competitor from the sweep
raw-data/04-content.md
raw-data/05-channels.md
raw-data/06-conversion.md
raw-data/07-path.md
checkpoints/part-N.md              short status note after each part
report.html                        the primary deliverable, styled and self-contained
report.md                          supplemental narrative version of the same report
```

## Phase 0: Intake (always first)

Use AskUserQuestion. Ask in three rounds, not all at once, so answers stay specific. Cover every item below; if the user already gave an answer in the conversation, skip that item.

Round 1, the product:
1. What is the product, in one or two sentences, and what stage is it at (idea, prototype, live)?
2. What does it do that a user would notice in their first session? List the features that exist or are planned.
3. Is it B2B, B2C, or both? Software, iOS app, service, or physical?

Round 2, the audience and the market:
4. Who do you currently believe it is for? Name a job title or a life situation, not a demographic.
5. What are they doing today instead of using your product? (spreadsheet, manual process, a generic tool, nothing)
6. Which competitors or adjacent tools do you already know of? Include URLs if you have them.
7. Which geography and language matter first?

Round 3, constraints and goals:
8. What is the launch window and what does "launch" mean here (waitlist, App Store release, first paying customer)?
9. How many people are on the team, and what budget exists for marketing, if any?
10. Which channels can you reach today by name (a subreddit, a newsletter, a community, your own network)?
11. What would you count as success in the first 30 days?
12. Anything you have already tried, and what happened?

Write all answers to `intake.md`. Then state, in one short paragraph to the user, your working hypothesis for the segment and the current alternative, and say you will now research it.

## Research tooling: Apify MCP

Use the Apify MCP tools for data pulls. Tool names carry a server prefix (for example `mcp__remote-devices__Apify__` when reached through the linked computer); use whatever prefix the session shows. The core calls are:

- `search-actors`: find the right actor by keyword ("reddit", "google search", "g2 reviews", "app store reviews", "linkedin posts", "tiktok", "facebook ads library").
- `fetch-actor-details`: read the input schema before calling an actor. Never guess input fields.
- `call-actor`: run it. Keep runs small (maxItems 50 to 200) so they finish quickly and stay cheap.
- `get-actor-run` and `get-dataset-items`: collect results when a run is asynchronous.
- `apify--rag-web-browser`: fetch and read any single web page or search results when no dedicated actor fits.

Candidate actors to confirm through `search-actors` before use (IDs change, so always verify):

| Need | Search term | Typical actor |
|---|---|---|
| Web search results, market size, competitor lists, SERP ads | google search | `apify/google-search-scraper` |
| Reddit posts and comments for pain language and competitor sentiment | reddit | `trudax/reddit-scraper-lite` or `apify/reddit-scraper` |
| Competitor site copy, pricing pages, blog cadence | website content crawler | `apify/website-content-crawler` |
| G2, Capterra, Trustpilot reviews | g2 reviews, capterra, trustpilot | store actors named for each site |
| App Store and Google Play reviews | app store reviews, google play | store actors named for each store |
| Meta Ad Library (competitor ads) | facebook ads library | store actors named for the ad library |
| LinkedIn or X posts and profiles | linkedin posts, twitter | store actors named for each network |
| TikTok, Instagram, YouTube channels and posts | tiktok, instagram, youtube | `clockworks/tiktok-scraper`, `apify/instagram-scraper`, `streamers/youtube-scraper` |
| Hacker News or Product Hunt launches | hacker news, product hunt | store actors named for each site |

If an Ahrefs or other SEO MCP is also connected, use it for the SEO parts of the competitor sweep. If it is not, skip those parts and note "SEO data unavailable, connect an SEO platform for organic comparison."

Save every dataset as Markdown in the matching `raw-data/` file: the actor used, the exact input, the date, the item count, then the items (title, URL, author or source, date, and the text or the fields that matter). Quote verbatim language; that is the asset. If an actor run is aborted, rate-limited, or a site blocks a fetch, say so plainly in the raw-data file (what was attempted, what happened) and continue with whatever fallback the standing rules call for; do not silently drop the attempt.

## Part 1: User insight

Goal: who these people are and what they struggle with, in their own words, narrowed to one primary segment you could picture as five real people, plus two alternates.

This part has two moves. First, name the whole market: an honest, broad, bounded statement of everyone who could use this, plus a rough size. It is too big to aim a message at, and that is the point: it makes the narrowing feel like a choice. Second, cut it down to a role plus a moment: a specific kind of person, in a specific recurring situation, feeling a specific pain.

Research:
- Google search actor: "[category] market size 2026", "[category] number of users", "[problem] statistics". Capture 3 to 5 figures with sources. Also "[category] tools", "[category] software" to see how the market labels itself.
- Reddit actor: search 5 to 8 subreddits for the problem keywords; pull top posts from the last 6 months and the comments on the top 10. Mine for who is posting (role), when the pain hits (moment), what they tried, and the exact phrases they use.
- LinkedIn or X actor if B2B, TikTok or Instagram actor if consumer: search the problem phrase, capture who is talking and in what words.
- App store reviews actor if there is an adjacent app: pull 1 to 3 star reviews for the exact complaint language.

For each candidate segment, run the three checks with evidence:
- Reachable: name the exact subreddit, Slack, Discord, newsletter, or creator where they gather, with member counts if visible.
- Frequent: cite evidence that the pain recurs weekly or per project, not yearly.
- Active: cite evidence that they already pay for or actively search for a fix (existing tools they mention, "looking for" posts, spend).

Output in the report: the whole market in one sentence in the "people who [situation] and need [outcome]" form with a size estimate and sources; the primary segment in one sentence; a table of the three checks with citations; five short persona sketches drawn from real posts (no names); the trigger moment in a "just did X, now has to Y, before Z" sentence; a short list of the segment's own phrases for the pain, verbatim, which every later part reuses; and the two alternate segments with one line each on why they are second.

## Part 2: Product design

Goal: the smallest product that solves the exact moment from Part 1, and a clear list of what to cut or park.

In a GTM context, product design is one test applied to every feature: does this make the trigger moment easier for the five people in Part 1? If you cannot say yes in one sentence, it waits. The trap, especially for technical founders, is building the general and powerful version first and then looking for someone who wants it. The insight has to come before the code.

Research:
- From the Part 1 raw data, list every "I wish it would" and "the annoying part is" phrase. These are the must-solve moments.
- App store or G2 reviews actor on the 2 to 3 closest adjacent tools: which features do 4 and 5 star reviews praise (must-haves), and which features do 1 to 3 star reviews call bloat, confusing, or unnecessary (candidates to cut)?
- Reddit actor: "[category] too complicated", "[category] all I need is". Capture the minimal version people describe.

Output in the report: the one thing the product must do, stated in a single sentence in the segment's own words; a feature table with three columns (feature, which Part 1 moment it serves, keep or cut or park) covering every feature from intake; the cut list with one line of rationale each; and one paragraph on what "done" looks like for a first version, so the team can ship the smallest thing that matches the moment. If the product is live, note which existing features the evidence says users ignore.

## Part 3: Brand positioning

Goal: the honest current alternative, a full competitor sweep, the gap, and one positioning sentence. This part has four pieces: build the competitor list, sweep each competitor completely, analyse, then write the sentence.

### 3a. Build the competitor list

- Start from the intake answers and any client brief.
- Google search actor: "[category] alternatives", "best [category] for [segment]", "[known competitor] vs", "[known competitor] alternative". Add every product that appears twice or more.
- Reddit actor: "[problem] what do you use", "[category] recommendation". Add tools the segment names itself.
- Cap the sweep at the 3 to 5 most relevant competitors for this segment. List the rest by name only.
- Always include the status quo as a competitor: the spreadsheet, the manual process, the repurposed generic tool, or doing nothing. It is usually the real one.

### 3b. Competitor sweep (complete every step for one competitor before starting the next)

Save each competitor to `raw-data/03-competitor-<slug>.md`.

1. Website and positioning (website content crawler, or `rag-web-browser` for single pages). Record verbatim: hero headline, subheadline, primary CTA and offer, pricing figures, trust signals (review counts, logos, customer counts, guarantees), main navigation items, whether a blog exists and its last publish date, whether there is email capture and what it offers, and anything distinctive about the offer or UX.
2. Paid advertising. Meta Ad Library actor (or `rag-web-browser` on facebook.com/ads/library): total active ads, earliest active ad date, format split (image, video, carousel), the headline and primary text of up to 5 prominent ads verbatim, recurring themes and offers, UGC-style versus branded creative. Google search actor on the competitor's brand name and the top 3 shared keywords: are they running search ads, and what does the copy say?
3. Social presence. Use the matching actor for each network the competitor uses: follower count, post or video count, last 10 to 20 posts with engagement, posting frequency, content themes and formats. For LinkedIn company pages use the LinkedIn actor or `rag-web-browser`.
4. Reviews and reputation. G2, Capterra, Trustpilot, App Store, or Google Play actor as applicable: overall rating and count, the top 5 positive themes and top 5 negative themes in verbatim phrases, the most helpful negative review, the most helpful positive review. Weight 2 to 3 star reviews most heavily; they hold the honest "unlike" material.
5. Reddit sentiment. Reddit actor: "[competitor]", "[competitor] review", "[competitor] problems", "[competitor] vs", "switched from [competitor]". Record the most upvoted threads and comments, positive and negative.
6. SEO (only if an SEO MCP is connected): domain rating, estimated organic traffic, ranking keyword count, referring domains, top 5 pages by traffic, and head-to-head keyword overlap with the product if it has a site. Otherwise note SEO data unavailable.

After each competitor, append one line to `checkpoints/part-3.md` so the sweep can resume.

### 3c. Analysis

Do all of this only after every competitor is swept.

Competitor matrix. One table with the product in the first column and each competitor after it. Rows: primary positioning (their own words), segment they actually serve, price point, review rating and count, active Meta ads, primary social following, biggest strength, biggest weakness, and SEO metrics if available.

Positioning map. Describe in prose where each competitor sits on the two axes that matter most for this segment (for example premium versus budget, broad versus niche, set-up-heavy versus zero-setup). State where the gap is and whether the product sits in it.

Ad and message intelligence. Which hooks and pain points are oversaturated across competitors, which offers and CTAs dominate, and which angles from the Part 1 raw data nobody is using.

Gap analysis. Cross-reference each competitor's marketing claims against what reviewers and Reddit say. Note where marketing contradicts customer reality, which complaints repeat across several competitors (a universal frustration is the opportunity), and which channels the competition underuses.

Apply the rule: zero competitors is a warning sign, not good news. If the exact niche is empty, check whether adjacent problems have competitors. Say plainly whether the evidence points to "early" or to "unproven".

Threat assessment. Rank each competitor High, Medium, or Low threat for this specific segment, with one sentence of rationale.

### 3d. The positioning sentence

Write one sentence, using this template, built only from Part 1 and Part 3 evidence:

> For [segment] who [struggle with this], [product] is a [category] that [key benefit]. Unlike [current alternative], [product] [what you do differently].

Rules:
- Borrow a category the audience already uses (take it from the search results and competitor headlines), do not invent one.
- End the "unlike" clause on what the product does, not on what the alternative does badly. Naming the alternative gives a reference point; attacking it sounds defensive.
- Use the segment's own words from Part 1 for the "struggle" clause.
- Check the sentence against the ad and message intelligence: if it repeats an oversaturated hook, rewrite it around an unused angle.

Output in the report: the matrix, the positioning map, the ad and message intelligence, the gap analysis, the threat ranking, the status quo alternative most of the segment actually uses, the gap in two sentences, and, if the product uses AI, which of workflow, data, or trust carries the differentiation. Then the final positioning sentence, two alternates that lead with a different benefit, a short table mapping each clause to the evidence it came from, and the three places the sentence must appear word for word (pitch opener, landing page headline, the one-liner for anyone who asks).

## Part 4: Content strategy

Goal: one master asset and the cuts of it, each in the right format for its place, all carrying the positioning sentence as the headline.

Content is the positioning sentence turned into things people read, watch, and share. The sentence never changes; the format around it changes for each place. X wants concise and opinionated, LinkedIn wants a story, Reddit wants value with no pitch, Hacker News wants technical honesty. Make the asset once, then cut it.

Research:
- Reddit actor on the top 2 gathering places from Part 1: pull the 20 most upvoted posts of the last 90 days. Record format (text, link, image, video), length, tone, and whether they open with a story, a question, or a claim.
- LinkedIn or X actor: pull the 10 best-performing posts by 2 or 3 creators the segment follows (from Part 1). Record hooks, structure, and length.
- From the Part 3 sweep: which content formats competitors use and which they ignore.

Output in the report: the master asset spec (a 60-second demo video that opens with the sentence, with a shot list: the real pain moment, then the product resolving it, then the sentence on screen); the cut list, one line each, for the channel picked in Part 5 and at most two others (clip, thread, story post, three screenshots, landing page headline); a tone card per place (what opens well, what gets flagged, ideal length); a full draft of the first post for the primary channel, written in the segment's own words from Part 1 and in that community's tone; and a repurposing rule: after launch, cut more from whatever performed, not from what the team liked.

## Part 5: Marketing channels

Goal: exactly one channel, named specifically, classified as owned, rented, or borrowed, with a cadence for the first four weeks.

Every channel has its own craft, and a small team cannot get good at five at once. Pick the one place the segment already pays attention and show up there the same way, repeatedly. Do not run ads until the positioning sentence has proven itself somewhere free; ads amplify a message that already works, they do not create one.

Research:
- From Part 1 raw data, rank the named gathering places by size, activity, and how closely the posters match the segment. Cross-check against the Part 3 gap analysis for channels competitors underuse.
- Reddit actor: pull the chosen community's rules and top posts of the last 90 days to confirm tone and what gets upvoted or removed.
- If the channel is a newsletter, creator, or LinkedIn, use the matching actor or `rag-web-browser` to capture format and cadence.
- If the product is an iOS app, pull the top 3 competitors' App Store screenshots and titles; the App Store is the rented channel and the first three screenshots carry the sentence.
- For AI and developer products, check the launch venues explicitly: Hacker News (Show HN, anyone with a free account can post immediately, but sales-pitch titles get flagged and upvote requests get the post killed), Product Hunt (personal accounts only, no hunter needed, votes from new accounts are discounted, traffic fades by day three), Reddit startup and niche subreddits, AI directories, and partnerships. Note which of these the segment actually reads.

Output in the report: the channel, its classification (owned, rented, borrowed) and why the other two are second, an evidence table (size, activity, segment match, competitor presence), the rules and tone of that place, a four-week cadence (what gets posted, when, how often), and the two channels to try next only after the first shows signal.

## Part 6: Conversion strategy

Goal: what the product asks for, when, and how the ask stays small and visible, with a before, at, and after launch plan.

Conversion is how a visitor becomes a signup, an install, or a payment. Early on, ask for as little as possible and put the ask on screen from the first second.

Research:
- From the Part 3 sweep: what each competitor's primary CTA asks for (email, card, demo booking, install), and what their reviews say about signup friction.
- `rag-web-browser` on the 2 or 3 competitor landing pages: headline, number of form fields, whether pricing is visible, whether a demo video is above the fold.
- If the product is an app: the App Store or Google Play listing structure for the top competitor (title, subtitle, first three screenshots, first line of description).

Output in the report: the landing page spec (headline is the positioning sentence, the 60-second video, one field, nothing else on the page), the single conversion action and why it is the smallest useful ask, and the dated schedule:
- Before launch: message N named people who match the segment (from the user's network or the community), with the sentence and the demo, asking for a reaction. Include the draft outreach message.
- At launch: every post and pitch opens with the sentence and links to the one page; the signup link stays visible the whole time.
- Two weeks after: personal reply to every signup, one honest update post with real numbers, and a deliberate go or no-go decision on day 14. Include the one question to ask each signup that tests whether the product became part of their routine.

## Part 7: Path optimization

Goal: the funnel with each part placed on it, one north star metric at retention, a decision rule set in advance, and a leak-to-part map.

The path is a funnel: awareness (they hear about you), interest (they click, read, or watch), consideration (they compare you to what they use now), conversion (they sign up, install, or pay), retention (they come back). Every stage has a count; the ratio between two stages is that step's conversion rate. Find the worst ratio, fix that one, wait two weeks, read the numbers again.

No actor is needed. Derive the metric from Part 1's trigger moment: what action would a user only take if the product became part of their routine (a log reopened two days later, a workout logged in week two)? Signups, downloads, and API calls are vanity metrics.

Output in the report: the five-stage funnel with each part placed on it (Part 1 decides who enters the top; Parts 3 and 4 move people from interest to consideration to conversion; Part 5 is the door at the top; Part 6 is the conversion stage; Part 7's metric lives at retention); the north star metric and why it beats the obvious vanity metric; the simplest possible instrumentation (a counter column checked by hand on day 14 is fine); the decision rule ("fewer than N by day 14 means the [clause] framing is not the hook; test [alternate sentence] instead"); and the leak map, one line per leak:
- Few people at the top: revisit Part 5 (wrong channel, or not consistent).
- They look but do not consider: revisit Parts 3 and 4 (the sentence is not landing, or the content is not in their words).
- They consider but do not convert: revisit Part 6 (the ask is too big or hidden, or the "unlike" is not strong enough).
- They convert but do not come back: revisit Parts 1 and 2 (wrong segment, the moment is not real for them, or the product does not solve it yet).

## Phase 8: Report

The deliverable is two files that carry the same conclusions at two depths: `report.html` is what the user actually reads first, a single self-contained page that walks through all seven parts and surfaces the critical numbers and quotes without the reader having to hunt for them. `report.md` is the supplemental long-form version: full prose, full tables, full citations, the backup a reader reaches for only if they want the detail behind a claim in the HTML. Build the content once (the same executive summary, the same seven-part findings, the same GTM Canvas, the same risks and sources) and then render it twice, in the two formats below. The HTML is the primary artifact; the Markdown is the supplement.

### Shared content (drives both files)

Work out this content once, before writing either file:

1. Title, date, product, one-paragraph executive summary that states the segment, the one thing the product must do, the positioning sentence, the channel, the conversion ask, and the north star metric.
2. Intake summary: what the user told us, and what the research confirmed or overturned.
3. Parts 1 to 7, one section each, using the outputs defined above. Part 3 carries the full competitor matrix, positioning map, gap analysis, threat ranking, and the sentence. Every claim cites a raw-data file and, where possible, a URL.
4. Filled-in GTM Canvas: the seven rows in one table (User insight, Product design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization), ready to copy.
5. Risks and open questions: the two or three places where evidence was thin, and how to close each gap in a week.
6. Sources: every URL used, grouped by part.
7. Research log: which actors ran, item counts, and any failures or blocks.

### report.html: the primary deliverable

Build this as one self-contained HTML file: all CSS inline in a single `<style>` block in the `<head>`, no external stylesheet or script dependency required to render correctly, so it opens correctly as a plain double-clicked local file, as an email attachment, or in a browser tab with no network access. Do not use a JavaScript framework; static HTML and CSS only.

Structure it as a single scrollable page the reader can also skim in under a minute, built from distinct, consistently styled sections, one per part, so the report reads like a well-designed slide deck compressed onto one page rather than a wall of text:

- A hero section at the very top: product name, date, and one line naming the experiment or client context. Immediately below it, three highlight tiles, visually prominent, showing the positioning sentence, the one channel, and the north star metric side by side, so a reader who never scrolls further still walks away with the answer.
- One visually distinct section per part (User insight, Product design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization), each opening with a one-sentence takeaway in larger or bolder type before the supporting paragraph, and each surfacing its 2 to 4 most important numbers or verbatim quotes as small callout boxes or stat tiles rather than burying them in prose. Alternate background shading or a left border accent between sections so the reader always knows which part they are in.
- The Part 2 feature table, the Part 3 competitor matrix, the Part 7 funnel and leak map, and the GTM Canvas render as real styled HTML tables (not screenshots or images), matching the page's type and color system.
- A closing section listing the risks and open questions as short, scannable items, and a compact sources footer.
- Pick one consistent, restrained color and type system for the whole page and use it uniformly across every section. Keep the page legible if printed: avoid pure white text on color, avoid relying on hover or click states since this is a static file.
- If the session has the Artifact tool available and this report is one the user or their client is likely to revisit or share, publish it there as well as delivering the file directly; otherwise deliver the HTML file alone. Either way the standalone HTML file must still be produced and delivered.

### report.md: the supplemental deliverable

Prose paragraphs, tables where they help, no bullet lists inside the analysis sections, carrying the fuller narrative version of the same shared content, including the complete research log and every citation. This file exists so a reader who wants to verify a specific claim or hand the detail to someone else never has to ask for more than what is already in the folder.

### Delivery

Deliver both `report.html` and `report.md` to the user with SendUserFile, `report.html` first. If a client folder is connected, commit both there as well. Finish with four sentences: the positioning sentence, the one thing the product must do, the channel, and the metric, so the user can act without opening either file.

## Running outside Claude

This procedure was written for Claude, so a few tool names above are Claude-specific. If you are running it in ChatGPT, Codex, or another agent, read these substitutions in as you go. Everything else, the seven-part framework, the research plan for each part, the report structure, and the standing rules, applies exactly as written.

- "Apify MCP" and named actors (`search-actors`, `call-actor`, `trudax/reddit-scraper-lite`, and so on): use whichever browsing, search, or connected data tool your platform has instead. If none is available, do the research from your own knowledge and reasoning and say so plainly rather than inventing data, exactly as the fallback rule in the standing rules requires.
- "WebSearch" and "WebFetch": your platform's own web search and page-fetch tools.
- "AskUserQuestion": ask the clarifying questions directly in the conversation, in the same three-round structure.
- "SendUserFile": present the finished files to the user for download in whatever way your platform supports (an attached file, a canvas, or a code block).
- "The Artifact tool" and "a connected client folder": skip these. They are Claude delivery options. Deliver both report files directly to the user instead.
