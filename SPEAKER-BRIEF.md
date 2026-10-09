# Speaker Brief — Vidushi's Live Build

Private reference. Not shown to the audience.
The exact sequence and prompts to feed Claude, in order.

---

## PART A — Build the Brain Dump page (About Me, Voice, Strategy)

Everything below goes on **one Notion page: "Brain Dump".**

### 1. About Me — scrape LinkedIn, then enrich

Show the Apify actor, then paste:

> this is the brain dump, i want to create about me page on this notion page. Use this actor and scrape my linkedin profile `crawlerbros/linkedin-profile-scraper` and help me build my about me page
> https://www.linkedin.com/in/vidushimalhan/

Then ask Claude to interview you:

> Now I want to build my about me page. So ask me more questions to make my about me page — it would be a .md file used to create content. Ask more questions to enrich my file.

*(Claude asks ~10 organic questions → you answer → it writes the About Me section.)*

### 2. Voice — analyse last 20 posts, then enrich

> Now using this scraper `supreme_coder/linkedin-post` check my last 20 posts, and on the same page where we added About Me add a section for Voice — the kind of voice details including hooks etc. that I'm using in my posts. After this ask me any questions you think are relevant to enrich it.

Then add post structure:

> In the brain dump, also add a post structure: my hook style from my last 20 posts, my writing style, the phrases I use and don't use, the line breaks I give, if I use all caps or not, the kind of CTAs, the approximate word limit — put it all there.

### 3. Strategy — content pillars from the posts

> Based on the posts I've published, also create a Strategy section of the different content pillars I currently have.

**End state:** Brain Dump page has 3 sections — **About Me · Voice · Strategy.**

---

## PART B — Build the Content System database

One database with **3 sections: Content · Calendar · Resources.**

### The exact prompt to paste into Claude

> Create a Notion database called "Content System" on this page: [PASTE NOTION PAGE URL]
>
> One unified schema with these properties:
>
> **Core (all entries):**
> - Name — Title
> - Type — Select: Resource, Idea, Draft, Published, Report, Competitor
> - Pillar — Select: [my content pillars]
> - ICP — Select: ICP 1, ICP 2, ICP 3
> - Platform — Select: LinkedIn, Instagram, Both
> - Publish Date — Date
> - URL — URL
> - Notes — Text
>
> **For competitors / resources:**
> - Website — URL
> - Geography — Select: Berlin, DACH, Pan-Europe / Global
> - Audience & Problem (ICP) — Text
> - Content Pillars — Text
> - Relevant Ideas For Us — Text
> - Criteria Met — Multi-select with these 5 options:
>     1. Same niche / content overlap
>     2. Outlier posts detected
>     3. Audience fit
>     4. Borrowable format
>     5. Europe-relevant
> - Score (#) — Number (how many of the 5 criteria are met)
> - Pass / Fail — Select: **Pass (green)** if 3 or more criteria met, **Fail (red)** if fewer than 3
>
> **Views (3):**
> 1. **Content** — Table, Type = Idea or Draft. Show: Name, Type, Pillar, ICP, Platform, Publish Date, Notes
> 2. **Calendar** — Calendar view by Publish Date. Show: Name, Pillar, Platform, Status
> 3. **Resources** — a separate page with 3 stacked tables: Articles & Resources (Type = Resource), Competitors (Type = Competitor), Post Inspiration (Type = Inspiration)
>
> Automation: when a post draft is marked Done, set its Publish Date to today so it shows on the Calendar automatically.

**On the scoring criteria — say this out loud:**
Criteria Met is not colour-coded tags — it's a scoring filter. Each resource is checked against the 5 criteria; the Score counts how many are met; **3 of 5 or more = Pass (green), fewer = Fail (red).**

The 5 criteria:
1. **Same niche / content overlap** — LinkedIn growth, personal branding, content strategy, or AI for founders
2. **Outlier posts detected** — at least one post >10% above their average engagement
3. **Audience fit** — overlaps SocialFlo ICP (founders, operators, builders)
4. **Borrowable format** — carousel, list, step-by-step, story
5. **Europe-relevant** — content or audience relevant for DACH / Europe

---

## PART C — Resource analysis (score competitors)

### Analyse the existing competitors already in the table

> Analyse the resources in the Resources table. For each one, read the source, fill all the empty columns, score it against the 5 criteria, and set Pass or Fail.

*(Uses `crawlerbros/linkedin-profile-scraper` + `supreme_coder/linkedin-post` for LinkedIn, `apify/rag-web-browser` for newsletters/websites. Pass = 3+ criteria.)*

### Assess new competitors and populate

> Now assess these new competitors, fill all their columns the same way, and populate the table: [paste names / links]

---

## PART D — Content generation (populate the Content table)

> Now create 10 LinkedIn posts for me and put them under Content.
> Use my voice, structure, and content pillars — everything in the Brain Dump.

*(Posts save to the Content view as Type = Idea, 150–350 words each, in your voice.)*

---

## Quick reference

**Apify actors:**
- `crawlerbros/linkedin-profile-scraper` — profile, bio, followers
- `supreme_coder/linkedin-post` — last 20 posts (voice + outlier detection)
- `apify/rag-web-browser` — newsletters, blogs, websites

**Scoring:** Score = number of the 5 criteria met · Pass = 3+ (green) · Fail = <3 (red)

**Content System DB:** https://app.notion.com/p/vidushimalhan/0ed5f9020eb74805b2a56594eb20d8d1
