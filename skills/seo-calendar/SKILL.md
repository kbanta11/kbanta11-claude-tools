---
name: seo-calendar
description: Use when the user wants to create a blog content calendar, plan blog topics based on keyword research, find SEO content gaps, or schedule upcoming posts. Also use when the user says "content calendar", "blog plan", "keyword research for blog", or "what should I write about".
---

# SEO Content Calendar

## Prerequisites

Check that `.seo-blog/config.md` exists in the project root. If it does not exist, stop and tell the user:

> "Run the `seo-setup` skill first to initialize your SEO blog configuration."

Do not proceed without a valid config file.

## Workflow

```
Seed Ideas --> Project Analysis --> Keyword Research --> Gap Analysis --> Calendar Output
     |                                  |                     |
     |                            (Google + Bing)             |
     v                                  v                     v
  User input              Search variations,          Compare against
  topics/themes           long-tail, PAA,             existing content
                          comparisons, trends         and competitors
```

### Step 1: Seed Idea Gathering

Ask the user what topics, themes, or niches they want to explore. Accept free-form input -- a list of words, sentences, URLs, or rough ideas all work. Collect at least 2-3 seed ideas before proceeding.

### Step 2: Project Analysis

Read these files to understand the project:
- `README.md` and any landing page files (HTML, MDX, or markdown in `src/`, `pages/`, `public/`)
- Product descriptions, feature lists, pricing pages
- Existing blog posts in `.seo-blog/posts/`, `blog/`, `content/`, or similar directories

Extract:
- What the project does (core value proposition)
- Target audience segments
- Features and benefits already documented
- Topics already covered by existing blog posts (build a topic map)

### Step 3: Keyword Research

Use **WebSearch** on **both Google and Bing** for each seed idea. Run these search types:

| Search Type | Example Query |
|---|---|
| Seed + variations | `"[topic] tutorial"`, `"[topic] guide"`, `"how to [topic]"` |
| Long-tail keywords | `"best way to [topic] for [audience]"`, `"[topic] for beginners"` |
| People Also Ask | `"[topic]"` and note PAA/related questions in results |
| Comparison keywords | `"[project] vs [competitor]"`, `"[topic] vs [alternative]"` |
| Trending/timely angles | `"[topic] 2026"`, `"[topic] trends"`, `"new [topic]"` |
| Competitive landscape | `"[topic] blog"` -- note who ranks and content quality |

Record for each keyword cluster: estimated competitiveness (low/medium/high based on what is ranking), relevance to the project, and search intent (informational, navigational, transactional).

### Step 4: Gap Analysis

- Compare existing blog content against discovered keyword opportunities
- Identify topics where competitors have content but this project does not
- Find internal linking opportunities between planned posts and existing content
- Flag keywords where the project has a natural authority advantage

### Step 5: Write the Calendar

Write results to **`.seo-blog/calendar.md`** using this format for each entry:

```markdown
## [Topic Title]
- **Primary keyword:** [keyword]
- **Secondary keywords:** [3-5 keywords, comma-separated]
- **Target audience:** [segment]
- **CTA target:** [specific feature/page, or "default"]
- **Internal link targets:** [existing posts to link to/from]
- **Priority:** [1-5] -- [one-line rationale]
- **Status:** planned
- **Suggested publish date:** [optional, YYYY-MM-DD]
```

Sort entries by priority (5 = highest) descending.

### Step 6: Update Logic

When `.seo-blog/calendar.md` already exists:
- Read the existing calendar first
- Merge new findings without duplicating existing entries
- Update priority scores if the competitive landscape has changed
- Preserve status fields (do not reset `in-progress`, `draft`, or `complete` back to `planned`)
- Append new entries below existing ones, maintaining priority sort

## Common Mistakes

| Mistake | Why it matters | Do this instead |
|---|---|---|
| Skipping Bing search | Bing surfaces different results and question formats | Always search both Google and Bing |
| Targeting only high-competition keywords | New blogs cannot rank for head terms | Prioritize long-tail and low-competition keywords |
| Ignoring existing content | Leads to cannibalization and duplicate topics | Always scan existing posts first |
| No internal link plan | Missed SEO authority signals between posts | Map link targets for every new entry |
| Resetting status on update | Overwrites real progress on in-flight posts | Only update priority and keywords, preserve status |
| Generic CTAs | Wastes conversion opportunity | Tie each post to a specific feature or page |
| Skipping project analysis | Content drifts off-brand or off-audience | Read project files before keyword research |
