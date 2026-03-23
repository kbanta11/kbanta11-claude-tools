---
name: seo-draft
description: "Use when the user asks to write, draft, or generate a full SEO blog post from an approved outline. Also use when the user says 'write the post', 'draft the article', or 'create the blog draft' for a topic that has a completed outline."
---

# SEO Blog Post Draft

## 1. Prerequisites

Before writing, confirm ALL of these exist:

- `.seo-blog/config.md` — abort with instructions if missing
- `.seo-blog/style-guide.md` — abort with instructions if missing
- `.seo-blog/research/<topic-slug>.md` — abort and tell user to run research skill first
- An approved outline for this topic — abort and tell user to run outline skill first

If any file is missing, stop and tell the user exactly which prerequisite is needed.

## 2. Branch Creation

Create and checkout a git branch named `blog/<topic-slug>`.

- Run `git branch --list blog/<topic-slug>` to check if it already exists
- If it exists, ask the user: "Branch `blog/<topic-slug>` already exists. Continue on it, or delete and start fresh?"
- If continuing, `git checkout blog/<topic-slug>`
- If starting fresh, `git branch -D blog/<topic-slug>` then `git checkout -b blog/<topic-slug>`
- If it does not exist, `git checkout -b blog/<topic-slug>`

## 3. Context Loading

Read ALL of the following before writing anything:

1. `.seo-blog/config.md` — extract blog directory path, CTA defaults, site URL, author info
2. `.seo-blog/style-guide.md` — extract tone, structure rules, formatting preferences
3. `.seo-blog/research/<topic-slug>.md` — extract verified sources, competitor analysis, key data points
4. The approved outline — extract section structure, keyword placement plan, target keywords
5. 2-3 existing blog posts from the blog directory in config — study for voice matching, frontmatter format, and structural patterns

## 4. Frontmatter

Match the project's existing frontmatter format exactly by copying the structure from existing posts. Include all fields found in existing posts (typically title, description/excerpt, date, tags/categories, author). Use today's date. Do not add fields that existing posts do not use. Do not omit fields that existing posts do use.

## 5. Writing Rules

Follow these rules strictly:

- Match the tone and style from the style guide exactly — do not deviate
- Keep paragraphs short: 2-4 sentences maximum
- Write smooth transitions between every section
- Use keywords naturally as specified in the outline's keyword plan — never force them
- Vary sentence length for readability (mix short punchy sentences with longer explanatory ones)
- Prefer active voice over passive voice
- If the style guide uses second person, address the reader directly ("you")
- Do not use filler phrases like "In today's world" or "It's important to note"

## 6. Source Citations

- ONLY cite sources marked as **VERIFIED** in the research file
- Use inline markdown links: `[descriptive anchor text](URL)`
- Never fabricate, guess, or approximate a URL
- If a source is marked UNVERIFIED, do not link to it — omit the citation entirely or rephrase without attribution
- Prefer descriptive anchor text over raw URLs or generic "click here" text

## 7. CTA Integration

Insert exactly two CTAs:

- **Mid-article CTA**: Weave naturally into a relevant section. It should feel like a helpful suggestion, not a sales pitch. Use the CTA text and link from config unless the outline specifies an override.
- **End-of-post CTA**: Place after the final section, before any closing. Make it clear and direct. Use the calendar/booking link from config, or a specific override if the outline provides one.

## 8. Image Placeholders

For each image location (header, and any body images indicated in the outline), insert this exact format:

```markdown
<!-- IMAGE_PLACEHOLDER
filename: images/blog/<topic-slug>/header.png
alt: Descriptive alt text for SEO
prompt: Detailed AI generation prompt — subject, style (photorealistic/illustration/flat design), color palette, mood, composition, aspect ratio (16:9 for header, 4:3 for body), what to avoid
-->
![Alt text](images/blog/<topic-slug>/header.png)
```

Use unique, descriptive filenames for each image. Write alt text that is specific and SEO-relevant. Write prompts that are detailed enough for high-quality AI image generation.

## 9. Save and Commit

- Save the completed post to the blog directory specified in config, using the standard filename pattern from existing posts
- Stage the file: `git add <filepath>`
- Commit on the blog branch: `git commit -m "draft: <post-title>"`

## 10. Common Mistakes

| Mistake | Why It's Wrong | What To Do Instead |
|---|---|---|
| Fabricating sources or URLs | Destroys credibility; readers get 404s | Only cite VERIFIED sources from research file |
| Keyword stuffing | Hurts readability and SEO ranking | Use keywords naturally per the outline's placement plan |
| Ignoring the style guide | Creates inconsistent brand voice | Re-read style guide before writing; check tone after each section |
| Long paragraphs | Readers skim; walls of text get skipped | Break into 2-4 sentence paragraphs |
| Generic CTAs | Low conversion; feels like spam | Tie CTA to the section's specific value proposition |
| Missing frontmatter fields | Breaks site build or SEO metadata | Copy exact format from existing posts |
| Passive voice overuse | Weakens writing; feels distant | Rewrite with subject-verb-object structure |
| Skipping transitions | Sections feel disconnected | Add a bridging sentence between every section |
