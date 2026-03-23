---
name: seo-outline
description: Use when the user asks to create a blog post outline, plan a blog post structure, or generate an SEO-optimized outline for a topic.
---

## Prerequisites

Before starting, verify these files exist:

- `.seo-blog/config.md` — site config, CTA defaults, target audience
- `.seo-blog/style-guide.md` — tone, formatting rules, heading conventions
- `.seo-blog/research/<topic-slug>.md` — keyword research and topic data

If any are missing, stop and tell the user which files are needed.

## Step 1: Style Guide Re-validation

1. Read existing published blog posts in the project.
2. Read `.seo-blog/style-guide.md`.
3. Compare actual post patterns (tone, structure, formatting) against the style guide.
4. If the style has drifted (new patterns, different tone, changed conventions), update `.seo-blog/style-guide.md` to reflect current practice.
5. Note what changed and inform the user of any updates.

## Step 2: Heading Structure

Build the outline following heading hierarchy from the style guide:

- **H1**: Include the primary keyword. Keep under 60 characters.
- **H2s**: Include secondary keywords naturally. Must be scannable and descriptive.
- **H3s**: Use for sub-topics within H2 sections.

Every heading must serve both readers and search engines. Never force a keyword into a heading where it reads awkwardly.

## Step 3: Keyword Placement Plan

For each section in the outline, note where keywords appear:

- Target 1-2% keyword density overall.
- Primary keyword must appear in: H1, first paragraph, at least 2 H2s, conclusion.
- Secondary keywords distributed across remaining sections.
- NO keyword stuffing. Every keyword usage must read naturally in context.

## Step 4: CTA Planning

Plan two CTAs:

- **Mid-article CTA**: A natural, contextual nudge related to the surrounding section content. Not salesy. Feels like a helpful suggestion.
- **End-of-post CTA**: More direct with a clear action. Use CTA text and URL from `.seo-blog/config.md`, unless the calendar entry provides an override.

Both CTAs should feel like a natural part of the content, not bolted on.

## Step 5: Image Planning

Plan images with specific placement:

- **Header image**: Describe subject, mood, and style.
- **1-2 body images**: Tied to specific sections. Describe what each should show (infographic, illustration, screenshot, diagram). Note placement (after which heading/section).

## Step 6: Internal Linking Plan

Create a two-part linking plan:

- **Outbound links**: Which existing posts to link TO from this new post, and in which section each link belongs.
- **Inbound links**: Which existing posts should be updated to add a link TO this new post.

## Step 7: Approval Gate

Present the complete outline to the user including all sections above. Do NOT proceed to drafting. Wait for explicit approval. If the user requests changes, revise the outline and re-present it. Only move forward when the user confirms.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Keyword density over 2% | Remove forced keyword instances, use synonyms |
| H1 over 60 characters | Tighten wording, move detail to the first paragraph |
| CTA feels salesy or disconnected | Rewrite to tie directly to the section topic |
| Skipping H3s under dense H2 sections | Break long sections into scannable sub-topics |
| Missing internal links | Review all existing posts for linking opportunities |
| Proceeding without user approval | Always stop at the approval gate and wait |
| Style guide not re-validated | Always compare live posts against the guide first |
| Images described vaguely | Give specific subject, mood, style, and placement |
