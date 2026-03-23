---
name: seo-research
description: >
  Use when the user wants to research a blog topic, analyze competitors,
  gather sources, or prepare for writing an SEO post. Also use when
  the user picks a topic from the content calendar or asks for
  competitor analysis on a keyword.
---

# SEO Research

## Prerequisites

1. Verify `.seo-blog/config.md` exists. If not, tell the user to run `seo-setup` first.
2. Accept topic from `.seo-blog/calendar.md` or ad-hoc from user.
3. Identify primary keyword and 2-4 secondary variations.

## Step 1: Competitor Analysis

WebSearch the target keyword + variations on **both Google and Bing**. Collect top 5-10 ranking articles (skip forums, Q&A, product pages).

WebFetch each competitor article. For each, document:

- URL, title, estimated word count
- Strengths: structure, depth, unique data, visuals
- Weaknesses: missing, outdated, or shallow content
- Keyword usage patterns
- Full H2/H3 heading structure

## Step 2: Angle Identification

After analyzing all competitors, determine:

- What's **not covered** across any top result
- What's **outdated** and can be refreshed
- Winning angle to beat current results (more depth, better data, unique perspective, more actionable, better visuals)

## Step 3: Source Research

Search for authoritative sources: studies, reports, expert opinions, official docs, case studies. For each source record:

- **Exact URL** (specific page, not domain)
- **Key claim/data point** (exact quote when possible)
- **Author/organization** and **publication date**

**CRITICAL: Verify every source.** WebFetch the URL, confirm the claim exists on that page. Mark anything unverifiable as **UNVERIFIED**. Never skip this.

## Step 4: Save Output

Save to `.seo-blog/research/<topic-slug>.md`:

```markdown
# Research: [Topic Title]

## Target Keywords
- Primary: [keyword]
- Secondary: [keyword 2], [keyword 3]

## Competitor Analysis
| # | Title | URL | Words | Strengths | Weaknesses |
|---|---|---|---|---|---|

### Detailed Competitor Notes
[Per-competitor heading structure, keyword patterns, full analysis]

## Content Gaps & Angles
[Missing/outdated/beatable areas and recommended angle]

## Verified Sources
| # | Claim | Source | Author/Org | Date | URL |
|---|---|---|---|---|---|

## Unverified Sources
| # | Claim | Source | Why Unverified | URL |
|---|---|---|---|---|

## Recommended Approach
[2-3 sentences: winning angle, target word count, key differentiators]
```

## Common Mistakes

| Mistake | What to do instead |
|---|---|
| Fabricating sources or URLs | NEVER invent a source. Only include what you fetched and verified with WebFetch. |
| Inventing statistics or quotes | Only use exact quotes confirmed on the source page. If you cannot find a stat, say so. |
| Searching only Google | Always search both Google AND Bing. |
| Skipping WebFetch on competitors | Deep-read every competitor, not just the search snippet. |
| Skipping source verification | WebFetch every source URL. Mark failures as UNVERIFIED. |
| Too few competitors | Aim for 5-10 minimum. |
| Ignoring heading structure | Document every competitor's H2/H3 outline. |
