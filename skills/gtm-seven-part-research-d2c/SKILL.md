---
name: gtm-seven-part-research-d2c
description: "Run a data-backed e-commerce D2C GTM analysis using Frank's seven-part framework (User insight, Product and offer design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization), with unit economics, an Amazon, Shopify, and Meta Ad Library competitor sweep, Apify MCP research, and a styled HTML report plus a Markdown report. Use for any physical consumer product, D2C brand, Shopify store, Amazon or TikTok Shop launch, or client e-commerce GTM."
---

# GTM Seven-Part Research: E-commerce D2C

You are a senior D2C growth strategist. This skill runs one physical consumer product or brand through the seven parts of go-to-market below, backs every part with real data pulled through the Apify MCP, runs a full competitor sweep across brand sites, Amazon, and the Meta Ad Library inside the Brand positioning part, checks the unit economics before any channel is chosen, and ends with a styled, self-contained HTML report backed by a supplemental Markdown file.

This is the D2C sibling of `gtm-seven-part-research`, which is tuned for software. Use this one when the thing being sold ships in a box: apparel, beauty, skincare, supplements, food and beverage, home goods, pet, baby, fitness gear, accessories, and similar. The framework is the same; what changes is where the evidence lives (Amazon reviews, TikTok, the Meta Ad Library, Shopify storefronts), what the product is (a hero SKU and an offer, not a feature set), how the first channel is usually bought (paid social and creators rather than a forum post), and what proves value (the second order, not the signup).

The seven parts are one chain, and the order is the point. What you learn about shoppers shapes the product and the offer, the offer shapes the positioning, the positioning becomes creative, creative goes out through channels, channels bring people to a product page, and the order and reorder data shows where the path leaks, which sends you back to shoppers. Do the parts in order. Never write a later part from guesswork when an earlier part has not been researched.

| # | Part | Question it answers |
|---|---|---|
| 1 | User insight | Who buys this, what moment makes them buy, what do they complain about in their own words, and which five of them do we go after first? |
| 2 | Product and offer design | Which single hero SKU do we lead with, at what price and bundle, and do the unit economics survive paid acquisition? |
| 3 | Brand positioning | What do they buy today instead, who else sells to them (brands, Amazon sellers, retail), and what is the one sentence that says why we are the better answer? |
| 4 | Content strategy | How does that sentence become thumb-stopping creative, UGC, and product page content, in the right format for each place? |
| 5 | Marketing channels | Which single acquisition channel do we master first, at what test budget and break-even target? |
| 6 | Conversion strategy | What does the product page, the offer, and the capture flow look like, so a first visit becomes a first order? |
| 7 | Path optimization | Where does the funnel leak, which one number proves real value (repeat purchase, not ROAS), and which part do we revisit when it is flat? |

## Standing rules

- Write with no dashes (no em dashes, en dashes, or "--"). Use commas, colons, or separate sentences. This applies to the HTML report's copy as much as the Markdown.
- Save raw data before analysing it. Never overwrite a file; append or create a new version.
- If a research call returns nothing, create the file anyway and write "No data found" with the reason.
- If an actor fails, a site blocks you, or the Apify MCP is unavailable, note it in the file and continue with WebSearch and WebFetch as the fallback.
- Save a checkpoint file after each part so the run can resume.
- All intake, raw-data, and checkpoint files are clean Markdown. The final deliverable is two files: `report.html`, a styled, self-contained HTML report that is the primary thing the user reads, and `report.md`, a supplemental plain-Markdown version carrying the same content in fuller narrative form. Never ship one without the other.
- If a Folson client brief exists for this product (`client-brief.md` in a connected client folder), read it first and reuse its competitor list, keywords, and positioning notes.
- Every money figure states its currency and whether it is an estimate, a user-supplied number, or an observed price with a source. Unit economics built on guesses are labelled as guesses, with the range that would change the recommendation.
- Flag claim risk. Supplements, skincare, food, baby, and pet products carry regulated claim language (health, "clinically proven", "cures", "organic", "non-toxic", and similar). When a competitor or a draft line in this report uses such a claim, note that it needs substantiation and a compliance check before it runs in an ad. You are not giving legal advice; you are keeping a list of lines to check.

## Folder layout

Create `gtm-research/<project-slug>/` in the working directory (or inside the connected client folder if one exists):

```
intake.md                          answers from Phase 0
raw-data/01-user-insight.md        raw pulls, one file per part
raw-data/02-product-offer.md       price ladder, bundles, unit economics
raw-data/03-positioning.md         competitor map and status quo
raw-data/03-competitor-<slug>.md   one file per competitor from the sweep
raw-data/04-content.md
raw-data/05-channels.md
raw-data/06-conversion.md
raw-data/07-path.md
raw-data/store-data.md             only if a live store is connected
checkpoints/part-N.md              short status note after each part
report.html                        the primary deliverable, styled and self-contained
report.md                          supplemental narrative version of the same report
```

## Phase 0: Intake (always first)

Use AskUserQuestion. Ask in three rounds, not all at once, so answers stay specific. Cover every item below; if the user already gave an answer in the conversation, skip that item.

Round 1, the product and the numbers:
1. What is the product, in one or two sentences, and what stage is it at (idea, samples in hand, inventory ordered, live and selling)?
2. How many SKUs, sizes, scents, or colours exist or are planned, and which one do you think is the hero?
3. What is the planned retail price, and what does one unit cost you landed (manufacturing, packaging, freight, duties)? Rough ranges are fine.
4. Is it a one-time purchase, a consumable that runs out (and roughly how fast), or something bought as a gift?

Round 2, the shopper and the market:
5. Who do you currently believe buys it? Name a life situation or a moment, not a demographic ("new runners training for a first half marathon", not "women 25 to 34").
6. What do they buy today instead? (a known brand, an Amazon generic, a drugstore or supermarket product, a homemade fix, nothing)
7. Which competitor brands, Amazon listings, or retailers do you already know of? Include URLs if you have them.
8. Where will it be sold first: your own Shopify or other store, Amazon, TikTok Shop, wholesale or retail, a marketplace such as Etsy? And which countries do you ship to first?

Round 3, constraints and goals:
9. What is the launch window and what does "launch" mean here (waitlist, preorders, crowdfunding, store live, first 100 orders, a retail placement)?
10. How much inventory do you have or have committed to (the MOQ), and how is fulfilment handled (yourself, a 3PL, Amazon FBA)?
11. What monthly budget exists for ads, creators, and samples, and how many people are on the team?
12. Which audiences can you reach today by name (an email list, an Instagram or TikTok following, a creator you know, a community, your own network)?
13. What would you count as success in the first 30 and the first 90 days?
14. Anything you have already tried (ads, creators, a pop-up, a marketplace), and what happened?

Write all answers to `intake.md`. Then state, in one short paragraph to the user, your working hypothesis for the segment, the purchase moment, and the current alternative, and say you will now research it.

### Live store data (optional)

If the brand is already selling and a Shopify MCP (or another store or analytics connector) is connected to the brand's own store, ask the user to confirm it is the right store, then pull and save to `raw-data/store-data.md`: the last 90 days of orders, average order value, top SKUs by revenue and units, the share of customers with two or more orders, median days between first and second order, discount code usage, and refunds or returns by SKU. Use the connector's analytics query tool where one exists. Treat this as the strongest evidence in the run: where it disagrees with public research, the store data wins, and the report says so. Never pull customer names, emails, or addresses into the raw-data files; aggregate only.

## Research tooling: Apify MCP

Use the Apify MCP tools for data pulls. Tool names carry a server prefix (for example `mcp__remote-devices__Apify__` when reached through the linked computer); use whatever prefix the session shows. The core calls are:

- `search-actors`: find the right actor by keyword ("amazon reviews", "amazon product", "shopify", "tiktok", "facebook ads library", "google shopping", "reddit", "trustpilot").
- `fetch-actor-details`: read the input schema before calling an actor. Never guess input fields.
- `call-actor`: run it. Keep runs small (maxItems 50 to 200) so they finish quickly and stay cheap.
- `get-actor-run` and `get-dataset-items`: collect results when a run is asynchronous.
- `apify--rag-web-browser`: fetch and read any single web page or search results when no dedicated actor fits.

Candidate actors to confirm through `search-actors` before use (IDs change, so always verify):

| Need | Search term | Typical actor |
|---|---|---|
| Amazon listings: price, rating, review count, Best Sellers Rank, bullets | amazon product | store actors named for Amazon product data, such as `junglee/amazon-crawler` |
| Amazon reviews for complaint and praise language | amazon reviews | store actors named for Amazon reviews |
| Competitor Shopify catalogues, prices, variants, launch cadence | shopify | store actors named for Shopify stores, or `rag-web-browser` on `<store>/products.json` |
| Competitor site copy, product pages, offers, popups, shipping and returns pages | website content crawler | `apify/website-content-crawler` |
| Meta Ad Library (competitor ads, the most important D2C source) | facebook ads library | store actors named for the ad library |
| TikTok videos, hashtags, TikTok Shop listings and creators | tiktok, tiktok shop | `clockworks/tiktok-scraper` and store actors named for TikTok Shop |
| Instagram and YouTube posts, reels, comments | instagram, youtube | `apify/instagram-scraper`, `streamers/youtube-scraper` |
| Google search, Google Shopping prices, SERP ads | google search, google shopping | `apify/google-search-scraper` and store actors named for Google Shopping |
| Trustpilot and retailer reviews (Target, Walmart, Sephora, Ulta, and similar) | trustpilot, the retailer name | store actors named for each site |
| Reddit posts and comments for pain language and brand sentiment | reddit | `trudax/reddit-scraper-lite` or `apify/reddit-scraper` |
| Search demand and seasonality | google trends | store actors named for Google Trends |

If an Ahrefs or other SEO MCP is also connected, use it for the SEO parts of the competitor sweep. If it is not, skip those parts and note "SEO data unavailable, connect an SEO platform for organic comparison." If a marketplace analytics tool (Jungle Scout, Helium 10, or similar) is connected, use it for Amazon sales estimates; otherwise estimate from Best Sellers Rank and review velocity and label the figure as a rough estimate.

Save every dataset as Markdown in the matching `raw-data/` file: the actor used, the exact input, the date, the item count, then the items (title, URL, author or source, date, price where relevant, and the text or the fields that matter). Quote verbatim language; that is the asset. If an actor run is aborted, rate-limited, or a site blocks a fetch, say so plainly in the raw-data file (what was attempted, what happened) and continue with whatever fallback the standing rules call for; do not silently drop the attempt.

## Part 1: User insight

Goal: who buys this and what makes them buy, in their own words, narrowed to one primary segment you could picture as five real shoppers, a purchase trigger, plus two alternate segments.

This part has two moves. First, name the whole market: an honest, broad, bounded statement of everyone who could buy this, plus a rough size in shoppers and in annual spend. It is too big to aim a creative at, and that is the point: it makes the narrowing feel like a choice. Second, cut it down to a person plus a moment: a specific kind of shopper, in a specific recurring or life-event situation, feeling a specific frustration with what they buy now. In consumer products the moment is often the whole story: a new baby, a first apartment, a training block, a skin flare-up, a move to a colder city, a gift deadline.

Research:
- Google search actor: "[category] market size 2026", "[category] consumer spending", "[problem] statistics". Capture 3 to 5 figures with sources. Google Trends for the main category terms over five years: is demand growing, flat, or seasonal, and which months peak?
- Amazon reviews actor on the 3 to 5 best-selling listings in the category: pull 1 to 3 star reviews for complaint language and 5 star reviews for the reason people bought. Mine for who is buying (they often say: "as a nurse", "for my toddler"), the moment, what they used before, and the exact phrases.
- TikTok and Instagram actors: search the problem phrase and the category hashtags. Capture who is posting, the comments under the top videos (comments are where shoppers ask "does this work for...", "where is it from"), and the words they use.
- Reddit actor: search 5 to 8 subreddits for the problem and the category ("[category] recommendations", "[problem] what actually worked"). Pull top posts from the last 6 months and the comments on the top 10.

For each candidate segment, run the four checks with evidence:
- Reachable: name the exact creators, hashtags, subreddits, communities, or interest targets where they gather, with follower or member counts if visible.
- Frequent: evidence that they buy repeatedly (a consumable that runs out, a seasonal need, a collection habit) or that the life moment recurs across many people each year.
- Active: evidence that they already spend on a fix (named products, "just ordered", haul videos, price mentions, subscriptions).
- Willing to pay the price: evidence that this segment pays at or above the planned price point for adjacent products, not only the cheapest option.

Output in the report: the whole market in one sentence in the "people who [situation] and want [outcome]" form with a size estimate and sources; the demand trend and seasonality in one line; the primary segment in one sentence; a table of the four checks with citations; five short shopper sketches drawn from real reviews and posts (no names); the purchase trigger in a "just did X, now needs Y, before Z" sentence; the top three purchase objections in their words (price, "will it work for me", size or fit, shipping time, trust in a new brand); a short list of the segment's own phrases for the frustration and the desired result, verbatim, which every later part reuses; and the two alternate segments with one line each on why they are second.

## Part 2: Product and offer design

Goal: one hero SKU, a price and bundle ladder, a clear list of what to cut or park, and unit economics that prove the business can afford to acquire a customer.

In D2C, the product a shopper meets is not the whole catalogue; it is one hero product plus an offer. The test for every SKU, variant, and add-on is the same as for features in software: does it make the purchase moment from Part 1 easier for the five shoppers? The traps are launching twelve variants and splitting a small ad budget across all of them, and pricing from cost plus markup instead of from what the segment already pays. A product that cannot survive paid acquisition at its price needs a different price, a bundle, a higher order value, or a repeat purchase before any channel is chosen.

Research:
- From the Part 1 raw data, list every "I wish it", "the problem with every one I tried", and "finally found one that" phrase. These are the must-solve product attributes (size, fit, taste, texture, durability, ingredients, packaging, refill).
- Amazon reviews actor on the 2 to 3 closest competing products: which attributes 4 and 5 star reviews praise (must-haves) and which 1 to 3 star reviews blame (quality, sizing, smell, breaks after, arrived damaged). Damaged-on-arrival and packaging complaints are a product decision, not a logistics footnote.
- Price ladder: Amazon product actor, Google Shopping actor, and competitor Shopify catalogues. Record the price of the budget option, the mainstream leader, and the premium brand for the same use, plus price per unit or per use where it applies. Record which competitors sell bundles, multipacks, subscriptions, and at what discount.
- Shipping and returns norms: `rag-web-browser` on 3 competitor shipping and returns pages. Record free-shipping thresholds, delivery promises, and return windows.

Unit economics (build this table, labelling each input's source):

| Line | Figure |
|---|---|
| Retail price, hero SKU and main bundle | |
| Landed unit cost (COGS) | |
| Pick, pack, packaging, and outbound shipping per order | |
| Payment processing (about 3 percent) | |
| Expected return or refund rate and its cost | |
| Contribution margin per first order, before marketing | |
| Break-even customer acquisition cost on the first order | |
| Break-even ROAS on the first order (price divided by contribution margin) | |
| Expected orders per customer in 12 months and the resulting 12-month contribution | |
| Target CAC that pays back within 90 days | |

Say plainly whether the numbers work. Rules of thumb to state and test, not to hide behind: a first-order contribution margin under roughly 50 percent of price makes cold paid social very hard; a break-even ROAS above roughly 2.5 on the first order means the brand needs a repeat purchase, a bundle, or a higher price to scale on paid; average order value below the category's free-shipping threshold leaves margin on the table. If the numbers do not work, recommend the change (bundle, price, pack size, subscription, cheaper packaging, a different channel mix) before continuing, and carry it into every later part.

Output in the report: the one job the hero product must do, stated in a single sentence in the segment's own words; the hero SKU and why it leads (evidence from reviews, search, and competitor bestsellers); a SKU and variant table with three columns (SKU or variant, which Part 1 moment or objection it serves, launch or park or cut) covering everything from intake; the price and bundle ladder (single, bundle or multipack, subscription if it is a consumable) with competitor reference prices; the unit economics table and a one-paragraph verdict; the packaging and unboxing requirements the reviews point to; and one paragraph on what "ready to launch" means for the first version. If the brand is live, note which SKUs the store data says carry the business and which ones dilute it.

## Part 3: Brand positioning

Goal: the honest current alternative, a full competitor sweep, the gap, and one positioning sentence. This part has four pieces: build the competitor list, sweep each competitor completely, analyse, then write the sentence.

### 3a. Build the competitor list

- Start from the intake answers and any client brief.
- Google search actor: "best [category] for [segment]", "[category] brand", "[known competitor] alternative", "[known competitor] vs", "[known competitor] review". Add every brand that appears twice or more.
- Amazon product actor: the top 10 results for the main category search term. Note the leading brands, the Amazon Basics or private-label option, and generic sellers.
- TikTok and Instagram actors: the brands that show up repeatedly in the top videos for the category hashtags and in "Amazon finds" or "TikTok made me buy it" content.
- Reddit actor: "[category] what do you use", "[category] worth it". Add brands the segment names itself.
- Cap the sweep at the 3 to 5 most relevant competitors for this segment, and make sure the set covers at least one D2C brand, one Amazon-first seller, and one retail or legacy brand if they exist. List the rest by name only.
- Always include the status quo as a competitor: the drugstore or supermarket option, the cheapest Amazon generic, the homemade fix, or doing without. It is usually the real one.

### 3b. Competitor sweep (complete every step for one competitor before starting the next)

Save each competitor to `raw-data/03-competitor-<slug>.md`.

1. Storefront and offer (website content crawler, or `rag-web-browser` for single pages). Record verbatim: hero headline and subheadline, primary CTA, the hero product and its price, bundle and subscription offers with discounts, the first-visit popup (discount, quiz, free gift) and what it asks for (email, SMS, both), free-shipping threshold, guarantee and return window, trust signals (review count on the product page, "as seen in", certifications, founder story), product page structure (image count, whether there are UGC photos or video, comparison charts, FAQ, ingredient or materials section), checkout options (Shop Pay, buy now pay later, PayPal), and whether there is a quiz or bundle builder. If the store runs on Shopify, `<store>/products.json` gives the catalogue: SKU count, price range, and recent launch dates.
2. Paid advertising, the most important step for D2C. Meta Ad Library actor (or `rag-web-browser` on facebook.com/ads/library): total active ads, the earliest active ad date (an ad running for months is a proven winner), format split (static image, video, carousel, collection), share of UGC or creator-style creative versus polished brand creative, the hook (first line or first three seconds) and primary text of up to 5 of the longest-running ads verbatim, the offer each ad carries, and the landing page each ad sends to (home page, product page, a listicle or advertorial, a quiz). Google search and Google Shopping actors on the brand name and the top 3 category terms: are they running search and Shopping ads, at what price, and what does the copy say? Note any TikTok ads visible in the TikTok Creative Center or ad library if reachable.
3. Social and creators. TikTok, Instagram, and YouTube actors: follower count, post count, last 10 to 20 posts with engagement, posting frequency, content themes and formats. Record whether the brand relies on its own account or on creators: count distinct creators tagging or mentioning the brand in the last 90 days, and note affiliate or discount codes in captions. If the brand sells on TikTok Shop, record the listing, price, units sold if shown, and the creators driving it.
4. Reviews and reputation. Amazon reviews actor (and Trustpilot, the brand's own product page reviews, and any retailer reviews as applicable): overall rating and count, the top 5 positive themes and top 5 negative themes in verbatim phrases, the most helpful negative review, the most helpful positive review. Weight 2 to 3 star reviews most heavily; they hold the honest "unlike" material. Note shipping, subscription-cancellation, and customer-service complaints separately: they are operational weaknesses a new brand can beat.
5. Marketplace position (if the competitor sells on Amazon). Amazon product actor: price, Best Sellers Rank in its main category, rating and review count, number of variants, whether it wins the buy box, and a rough monthly unit estimate labelled as an estimate. Note the listing's title and the first three bullets verbatim.
6. Reddit sentiment. Reddit actor: "[competitor]", "[competitor] review", "[competitor] worth it", "[competitor] vs", "switched from [competitor]", "[competitor] dupe". Record the most upvoted threads and comments, positive and negative. "Dupe" threads show what shoppers think the brand is really selling and what they would pay for it.
7. SEO (only if an SEO MCP is connected): domain rating, estimated organic traffic, ranking keyword count, referring domains, top 5 pages by traffic, and keyword overlap with the product's site if it has one. Otherwise note SEO data unavailable.

After each competitor, append one line to `checkpoints/part-3.md` so the sweep can resume.

### 3c. Analysis

Do all of this only after every competitor is swept.

Competitor matrix. One table with the product in the first column and each competitor after it. Rows: primary positioning (their own words), segment they actually serve, hero product and price, price per unit or use, bundle and subscription offer, first-visit offer, free-shipping threshold and returns, review rating and count (by site), Amazon Best Sellers Rank if applicable, active Meta ads and longest-running ad age, UGC versus brand creative share, primary social following and creator count, biggest strength, biggest weakness, and SEO metrics if available.

Positioning map. Describe in prose where each competitor sits on the two axes that matter most for this segment (for example premium versus budget, clinical versus natural, performance versus aesthetic, single hero versus wide catalogue). State where the gap is and whether the product sits in it.

Creative and offer intelligence. Which hooks, claims, and pain points are oversaturated across competitor ads, which offers dominate (percentage off, free gift, bundle, subscribe and save), which creative formats the longest-running ads use, and which angles from the Part 1 raw data nobody is using. Flag any competitor claims that carry claim risk under the standing rules.

Gap analysis. Cross-reference each competitor's marketing claims against what reviewers, commenters, and Reddit say. Note where marketing contradicts customer reality, which complaints repeat across several competitors (a universal frustration is the opportunity), which price points are empty, and which channels or creator niches the competition underuses.

Apply the rule: zero competitors is a warning sign, not good news. If the exact niche is empty, check whether adjacent products have competitors and whether the search demand from Part 1 exists. Say plainly whether the evidence points to "early" or to "unproven". Apply the opposite rule too: a category where the top Amazon listings have tens of thousands of reviews and generic sellers undercut on price is a commodity; the product needs a reason to exist beyond "better quality", or it needs a channel where Amazon is not the default.

Threat assessment. Rank each competitor High, Medium, or Low threat for this specific segment, with one sentence of rationale.

### 3d. The positioning sentence

Write one sentence, using this template, built only from Part 1 and Part 3 evidence:

> For [segment] who [struggle with this], [product] is the [category] that [key benefit]. Unlike [current alternative], [product] [what it does differently].

Rules:
- Borrow a category the shopper already uses (take it from Amazon search terms, TikTok hashtags, and competitor headlines), do not invent one.
- End the "unlike" clause on what the product does, not on what the alternative does badly. Naming the alternative gives a reference point; attacking it sounds defensive.
- Use the segment's own words from Part 1 for the "struggle" clause.
- The benefit is felt, not specified: "stays cold through a double shift" beats "double-wall vacuum insulation". Specs belong in the reasons to believe.
- Check the sentence against the creative and offer intelligence: if it repeats an oversaturated hook, rewrite it around an unused angle. Check it against the claim-risk rule.

Output in the report: the matrix, the positioning map, the creative and offer intelligence, the gap analysis, the threat ranking, the status quo alternative most of the segment actually buys, the gap in two sentences, and three reasons to believe (a material, a process, a proof point such as a test result, a guarantee, or a founder credential), each tied to evidence. Then the final positioning sentence, two alternates that lead with a different benefit, a short table mapping each clause to the evidence it came from, a brand voice note in three adjectives with one "sounds like" and one "never sounds like" line, and the places the sentence must appear word for word or near it (the product page headline, the first line of the best ad, the Amazon title or first bullet if selling there, the one-liner for anyone who asks).

## Part 4: Content strategy

Goal: a creative system, not a single asset: a handful of angles, each produced in a few formats, with UGC and creators carrying most of it, and a product page that closes the argument the ad started.

In D2C, content is mostly ad creative and product page content, and creative is the biggest lever on acquisition cost. The positioning sentence stays fixed; the angle and the format around it change. Plan to make many small, cheap variations and let the data pick, rather than one polished brand film. Creator and customer faces beat brand polish on TikTok and Reels; clean, benefit-led statics still win in many categories on Facebook and Instagram feeds.

Research:
- From the Part 3 sweep: the longest-running competitor ads, their hooks, formats, and lengths. These are the market's proven templates.
- TikTok and Instagram actors: the 20 best-performing videos in the last 90 days for the category hashtags and "TikTok made me buy it" or "Amazon finds" style searches. Record the hook (first three seconds, on-screen text), format (talking head, demo, before and after, unboxing, routine, comparison, skit), length, and whether it was a creator, a customer, or the brand.
- TikTok and Instagram actors on 5 to 10 creators the segment follows (from Part 1): follower counts, typical engagement, whether they do paid partnerships, and the format of their sponsored posts.
- Amazon and product page reviews: the photos and phrases customers use to describe the result; they become UGC briefs and product page copy.

Output in the report:
- Three to five creative angles, each one line, each tied to Part 1 evidence (for example: the frustration with the status quo, the transformation or result, the trigger moment, social proof, the founder's reason, the price-per-use comparison). Mark the lead angle.
- A creative testing matrix: angles down the side, formats across the top (UGC talking head, demo or before and after, static with benefit headline, carousel, founder video), with the first 8 to 12 concepts to produce marked. Each concept gets a hook line written in the segment's own words.
- Two full UGC briefs for the lead angle: the hook, the story beats (pain moment, discovery, product in use, result, call to action), the must-say lines, the claims not to make, length, and deliverables.
- A creator seeding plan: the tier of creators (nano, micro, mid), how many to seed in the first month, product-only versus paid, the ask, and how to track them (unique codes or links). Include the draft outreach DM.
- The product page content spec: the image stack in order (hero shot, in use, result or before and after, scale or size, what is in the box, UGC photo, comparison), the benefit bullets written from the positioning sentence and reasons to believe, the objection-handling FAQ from Part 1's top objections, and where reviews and guarantee sit.
- The email and SMS flows to write before launch: welcome series (3 emails), abandoned cart (2 to 3 messages), post-purchase (how to use, review ask, replenishment reminder timed to when the product runs out). One line each on what they say.
- A repurposing rule: after launch, iterate on whatever creative wins (new hooks on the winning body, new creators on the winning script), not on what the team liked.

## Part 5: Marketing channels

Goal: exactly one primary acquisition channel, named specifically, with a first-month test budget, a break-even target from Part 2, a cadence, and the two channels to add next.

Every channel has its own craft, and a small team cannot master five at once. In D2C the realistic first choices are usually one of: Meta paid social (Facebook and Instagram), TikTok (organic plus Spark Ads, or TikTok Shop with affiliate creators), creator seeding and affiliate, Amazon (if the category is searched there first), or an owned audience the founder already has. Pick the one where the segment already pays attention and where the Part 2 economics can survive. Ads amplify creative that already works; they do not rescue an offer that does not.

Research:
- From Part 1 and Part 3, rank the candidate channels by where the segment gathers, where the category is searched (Amazon versus Google versus TikTok), where competitors are winning, and where they are absent.
- If Meta: from the Part 3 ad sweep, the creative volume competitors sustain (a brand running 50 plus active ads is testing hard), and interest or lookalike seeds implied by Part 1 (creators, publications, communities the segment follows).
- If TikTok or TikTok Shop: the category's top TikTok Shop listings, price points, and the affiliate commission rates visible, plus how many creators are selling competing products.
- If Amazon: search volume signals (autocomplete, number of results, sponsored slots on page one), the review count needed to compete on page one, and the price the buy box sits at. Note the fee drag from referral and FBA fees against the Part 2 margin.
- If creators or affiliate: the creator list from Part 4 with counts and rates.
- Seasonality from Part 1: when to launch and when not to (for example, avoid launching into the fourth-quarter ad cost spike unless the product is a gift).

Output in the report: the channel, its classification (owned, rented, borrowed, or paid) and why the others are second; an evidence table (segment presence, category search behaviour, competitor presence, cost signals, fit with the unit economics); the first-month plan with a test budget, the number of creatives in rotation, the campaign structure in two or three lines (for Meta, for example, one broad campaign with the concepts from Part 4 as separate ads, rather than many narrow ad sets), the break-even CPA and ROAS from Part 2, and the kill or scale rule for a creative (for example, cut any ad above 1.5 times target CPA after spend equal to two times target CPA); a four-week cadence (what launches, what gets refreshed, what gets reviewed, when); and the two channels to add next only after the first shows signal, typically email and SMS retention (always on from day one, but not an acquisition channel) plus one of the others.

## Part 6: Conversion strategy

Goal: the page a shopper lands on, the offer they see, how their email or phone number is captured if they do not buy, and a before, at, and after launch plan.

Conversion is how a visitor becomes an order. For D2C that happens on the product page and in checkout, with email and SMS as the safety net that turns a lost visitor into an order a few days later. Early on, send paid traffic to the hero product page (or one purpose-built landing page), not the home page, and make the offer obvious above the fold.

Research:
- From the Part 3 sweep: each competitor's product page structure, first-visit offer, free-shipping threshold, guarantee, and checkout options, plus review complaints about checkout, shipping, or subscriptions.
- `rag-web-browser` on the 2 or 3 competitor pages that their longest-running ads send traffic to: headline, price and offer visibility above the fold, number of images, review count shown, whether there is a bundle selector, and the page type (product page, advertorial, listicle, quiz).
- Category benchmarks via Google search actor ("[category] ecommerce conversion rate", "ecommerce add to cart rate benchmark 2026"). Capture 2 or 3 figures with sources, and label them as industry averages.

Output in the report:
- The product page spec: headline is the positioning sentence or its shortest form, the Part 4 image stack, price with the bundle ladder as a selector (default to the bundle when the economics favour it), star rating and review count near the price, the guarantee and shipping promise beside the add-to-cart button, the objection FAQ, and fast checkout (Shop Pay or the platform equivalent, plus a buy now pay later option if the price is high for the category).
- The offer: what the first-order offer is (a bundle, a gift with purchase, free shipping, a small discount, or none) and why, checked against the Part 2 margin. Prefer offers that raise order value over straight discounts.
- The capture flow: the popup offer and what it asks for (email first, then SMS on the second step), when it appears, and the expected capture rate as a stated assumption.
- Social proof plan for a brand with zero reviews: seed product to the first 20 to 50 customers or creators for honest reviews and photos, use a review app with photo reviews, and show review count honestly. Never invent or buy reviews.
- The dated schedule:
  - Before launch: build a waitlist (a landing page with the sentence and a preorder or early-access offer), seed product to N named creators or community members who match the segment, and message N people from the founder's network. Include the draft waitlist page headline and the draft outreach message. If preorders or crowdfunding are part of the plan, say what they need to prove (demand at the planned price) and the number that counts as proof.
  - At launch: waitlist email and SMS first (they convert best), then the Part 5 channel goes live with the Part 4 concepts; every ad, post, and pitch uses the sentence and points to the one page.
  - Two weeks after: a personal note to the first customers, a review request timed to after delivery and first use, one honest look at the numbers, and a deliberate go or no-go decision on day 14 on the creative and offer, with the final judgement on repeat purchase coming at the Part 7 checkpoint. Include the one question to ask first customers that tests whether they will reorder or recommend it.

## Part 7: Path optimization

Goal: the funnel with each part placed on it, one north star metric that captures real value, a decision rule set in advance, and a leak-to-part map.

The D2C path is a funnel: awareness (ad impression or creator view), interest (click through to the site), consideration (product page view, then add to cart), conversion (checkout started, then order placed), retention (a second order, a subscription that survives the second charge, or a referral). Every stage has a count; the ratio between two stages is that step's conversion rate. Find the worst ratio against benchmark, fix that one, wait two weeks, read the numbers again.

No actor is needed beyond the benchmarks already saved. Derive the metric from Part 1's frequency check and Part 2's unit economics. Platform-reported ROAS, follower counts, and first-order revenue are the vanity metrics of D2C: they can look healthy while every customer loses money. The north star is usually one of: the share of first-time customers who place a second order within the product's natural replenishment window (for consumables), 90-day contribution margin per customer divided by blended acquisition cost (for most brands), or the share of buyers who refer or gift within 60 days (for one-time or gift products). Pick one and say why.

Output in the report:
- The five-stage funnel with each part placed on it (Part 1 decides who enters the top; Part 4 creative drives awareness to interest; Parts 3 and 4 product page content drives consideration; Part 6 is the conversion stage; Part 2's product and the post-purchase flows decide retention; Part 5 is the door at the top). Give a benchmark or target ratio for each step (for example, click-through rate, product page to add to cart, add to cart to order, first to second order), labelled as a benchmark or an assumption.
- The operating metrics to watch weekly: blended CAC (total marketing spend divided by new customers, not platform-attributed), first-order contribution after marketing, average order value, and the north star.
- The north star metric and why it beats platform ROAS.
- The simplest possible instrumentation: the store's own analytics plus a weekly sheet with spend, new customers, orders, AOV, and returning customers is enough at the start; post-purchase "how did you hear about us" survey for attribution.
- The decision rule, set now: for example, "if blended CAC is above the Part 2 break-even after the first N orders, the [angle] is not the hook; test [alternate angle or alternate sentence] next", and "if fewer than N percent of first customers reorder by day [replenishment window plus 14], revisit Part 2 before spending more on acquisition".
- The leak map, one line per leak:
  - Low click-through or high cost per click: revisit Part 4 (the hook is not stopping the scroll) or Part 5 (wrong audience or channel).
  - Clicks but few add to carts: revisit Parts 3 and 6 (the page does not match the ad's promise, the sentence is not landing, the price is not justified above the fold).
  - Add to carts but few orders: revisit Part 6 (shipping cost surprise, checkout friction, missing trust signals) and Part 2 (price or offer).
  - Orders but no second order: revisit Parts 1 and 2 (wrong segment, the product does not deliver the result, the replenishment timing is off), and check the post-purchase flow from Part 4.
  - Healthy funnel but no profit: revisit Part 2 (price, bundle, COGS, shipping) before scaling spend.

## Phase 8: Report

The deliverable is two files that carry the same conclusions at two depths: `report.html` is what the user actually reads first, a single self-contained page that walks through all seven parts and surfaces the critical numbers and quotes without the reader having to hunt for them. `report.md` is the supplemental long-form version: full prose, full tables, full citations, the backup a reader reaches for only if they want the detail behind a claim in the HTML. Build the content once (the same executive summary, the same seven-part findings, the same GTM Canvas, the same risks and sources) and then render it twice, in the two formats below. The HTML is the primary artifact; the Markdown is the supplement.

### Shared content (drives both files)

Work out this content once, before writing either file:

1. Title, date, product, one-paragraph executive summary that states the segment and purchase trigger, the hero SKU and its offer, whether the unit economics work and the break-even CAC, the positioning sentence, the lead creative angle, the channel and its test budget, and the north star metric.
2. Intake summary: what the user told us, and what the research (and store data, if pulled) confirmed or overturned.
3. Parts 1 to 7, one section each, using the outputs defined above. Part 2 carries the unit economics table and verdict. Part 3 carries the full competitor matrix, positioning map, creative and offer intelligence, gap analysis, threat ranking, and the sentence. Every claim cites a raw-data file and, where possible, a URL.
4. Filled-in GTM Canvas: the seven rows in one table (User insight, Product and offer design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization), ready to copy.
5. Risks and open questions: the two or three places where evidence was thin (unit cost guesses, untested price, unverified demand), the claim-risk list, and how to close each gap in a week (a sample order, a price test on the waitlist page, a small creative test).
6. Sources: every URL used, grouped by part.
7. Research log: which actors ran, item counts, and any failures or blocks.

### report.html: the primary deliverable

Build this as one self-contained HTML file: all CSS inline in a single `<style>` block in the `<head>`, no external stylesheet or script dependency required to render correctly, so it opens correctly as a plain double-clicked local file, as an email attachment, or in a browser tab with no network access. Do not use a JavaScript framework; static HTML and CSS only.

Structure it as a single scrollable page the reader can also skim in under a minute, built from distinct, consistently styled sections, one per part, so the report reads like a well-designed slide deck compressed onto one page rather than a wall of text:

- A hero section at the very top: product name, date, and one line naming the experiment or client context. Immediately below it, four highlight tiles, visually prominent, showing the positioning sentence, the hero offer with its break-even CAC, the one channel, and the north star metric, so a reader who never scrolls further still walks away with the answer.
- One visually distinct section per part (User insight, Product and offer design, Brand positioning, Content strategy, Marketing channels, Conversion strategy, Path optimization), each opening with a one-sentence takeaway in larger or bolder type before the supporting paragraph, and each surfacing its 2 to 4 most important numbers or verbatim quotes as small callout boxes or stat tiles rather than burying them in prose. Alternate background shading or a left border accent between sections so the reader always knows which part they are in.
- The Part 2 SKU table, price ladder, and unit economics table, the Part 3 competitor matrix, the Part 4 creative testing matrix, the Part 7 funnel and leak map, and the GTM Canvas render as real styled HTML tables (not screenshots or images), matching the page's type and color system.
- A closing section listing the risks, the claim-risk list, and open questions as short, scannable items, and a compact sources footer.
- Pick one consistent, restrained color and type system for the whole page and use it uniformly across every section. Keep the page legible if printed: avoid pure white text on color, avoid relying on hover or click states since this is a static file.
- If the session has the Artifact tool available and this report is one the user or their client is likely to revisit or share, publish it there as well as delivering the file directly; otherwise deliver the HTML file alone. Either way the standalone HTML file must still be produced and delivered.

### report.md: the supplemental deliverable

Prose paragraphs, tables where they help, no bullet lists inside the analysis sections, carrying the fuller narrative version of the same shared content, including the complete research log and every citation. This file exists so a reader who wants to verify a specific claim or hand the detail to someone else never has to ask for more than what is already in the folder.

### Delivery

Deliver both `report.html` and `report.md` to the user with SendUserFile, `report.html` first. If a client folder is connected, commit both there as well. Finish with five sentences: the positioning sentence, the hero offer and whether its economics work, the lead creative angle, the channel with its test budget, and the metric, so the user can act without opening either file.

## Running outside Claude

This procedure was written for Claude, so a few tool names above are Claude-specific. If you are running it in ChatGPT, Codex, or another agent, read these substitutions in as you go. Everything else, the seven-part framework, the research plan for each part, the unit economics, the report structure, and the standing rules, applies exactly as written.

- "Apify MCP" and named actors (`search-actors`, `call-actor`, `clockworks/tiktok-scraper`, and so on): use whichever browsing, search, or connected data tool your platform has instead. If none is available, do the research from your own knowledge and reasoning and say so plainly rather than inventing data, exactly as the fallback rule in the standing rules requires.
- "Shopify MCP" or a store connector: use whatever store or analytics integration your platform has, or ask the user to paste an export of aggregate order data. Never ask for customer personal data.
- "WebSearch" and "WebFetch": your platform's own web search and page-fetch tools.
- "AskUserQuestion": ask the clarifying questions directly in the conversation, in the same three-round structure.
- "SendUserFile": present the finished files to the user for download in whatever way your platform supports (an attached file, a canvas, or a code block).
- "The Artifact tool" and "a connected client folder": skip these. They are Claude delivery options. Deliver both report files directly to the user instead.
