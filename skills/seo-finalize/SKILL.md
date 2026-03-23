---
name: seo-finalize
description: >
  Use when the user asks to finalize, review, or verify an SEO blog post draft
  that already exists on a blog/<topic-slug> branch. Also use when the user says
  "finalize post", "final review", "verify sources", or "check SEO" for a draft.
---

## Prerequisites

- A draft post exists on a `blog/<topic-slug>` branch.
- `.seo-blog/config.yaml` is present with site and keyword configuration.
- A research file with cited sources exists alongside the draft.

## Source Re-verification

WebFetch every cited URL in the post. For each source:

- Confirm the page loads and contains the referenced claim.
- **Broken link**: find an alternative source via WebSearch, or remove the citation.
- **Unverifiable claim**: flag to the user and suggest removal or rewording.

After all checks, report: "X sources verified, Y broken (fixed/removed), Z unverifiable."

## SEO Metadata Checklist

Check each item and fix any issues found:

| Item | Requirement |
|---|---|
| Title tag | 50-60 characters, includes primary keyword |
| Meta description | 150-160 characters, includes keyword, has CTA |
| H1 | Matches title or close variant; exactly one H1 |
| H2s | Include secondary keywords, are descriptive |
| URL slug | Short, keyword-rich, no stop words |
| First paragraph | Primary keyword within first 100 words |
| Image alt text | Descriptive, includes keywords where natural |
| Internal links | At least 2-3 links to existing site content |
| Keyword density | 1-2% for primary keyword, no stuffing |

## Content Quality Review

- **Readability**: short paragraphs, varied sentence length, active voice.
- **Scanability**: subheadings every 200-300 words; use lists where appropriate.
- **Transitions**: smooth flow between sections.
- **CTA integration**: must feel natural, not forced.
- **Accuracy**: verify any claims, statistics, or dates mentioned in the post.

## Markdown Validation

- No broken syntax (unclosed tags, malformed links, broken image refs).
- Heading hierarchy is correct (no skipped levels, e.g., H2 to H4).
- Frontmatter is valid YAML.
- Image paths exist, or placeholders remain if images are not yet generated.
- Code blocks are properly fenced (if any).

## Mobile-Friendliness

- No rendered text lines over 80 characters (tables are exempt).
- Images include responsive sizing attributes if the framework supports it.
- Paragraphs are under 4 sentences to avoid walls of text on small screens.
- Tables use minimal columns.

## Post-Finalization Updates

1. Update `.seo-blog/style-guide.md` if this post introduces new patterns or conventions.
2. Update `.seo-blog/calendar.md` — set this post's status to "complete."
3. Create a final git commit on the blog branch: `finalize: <topic-slug>`.

## Finalization Report

Present the following to the user:

- **SEO checklist**: pass/fail for each item in the metadata checklist.
- **Source verification**: counts of verified, broken (fixed/removed), and unverifiable.
- **Issues found and fixed**: list each correction made.
- **Remaining warnings**: anything that needs manual attention.
- **Status**: "Branch `blog/<topic-slug>` is ready for review."

## Common Mistakes

| Mistake | Why it matters | Fix |
|---|---|---|
| Title over 60 characters | Truncated in search results | Shorten while keeping primary keyword |
| Missing meta description | Search engine generates a random snippet | Write a 150-160 char description with CTA |
| Skipped heading levels | Hurts accessibility and SEO crawlers | Restructure to maintain H1 > H2 > H3 order |
| Keyword stuffing (>2%) | Triggers search engine penalties | Reduce repetition, use synonyms |
| Broken citation links | Erodes reader trust and SEO authority | Replace with working source or remove |
| Paragraphs over 4 sentences | Poor mobile readability | Break into shorter paragraphs |
| No internal links | Missed opportunity for link equity | Add 2-3 links to related existing content |
| Unverified statistics | Damages credibility if wrong | WebFetch the source or remove the claim |
