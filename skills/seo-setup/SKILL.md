---
name: seo-setup
description: "Use when a project has no `.seo-blog/config.md` file, when the user says 'set up SEO blog', 'configure blog writer', or 'initialize seo', or when any other seo-* skill detects missing configuration."
---

# SEO Blog Writer — First-Time Setup

Configure project-specific settings, detect blog structure, and generate a writing style guide. Run once per project; other seo-* skills depend on its output.

## When to Use

- Project has no `.seo-blog/config.md`
- User explicitly asks to set up or reconfigure the SEO blog writer
- Another seo-* skill fails with missing config

## Process

### 1. Security Gate

Check that `.env` is listed in `.gitignore`:

```
Grep for "^\.env$" or "^\.env\b" in .gitignore
```

**If `.env` is NOT in `.gitignore`, STOP.** Tell the user:

> I cannot proceed. Your `.env` file is not in `.gitignore`, which risks committing API keys. Add `.env` to `.gitignore` and run this skill again.

Do not continue past this step until verified.

### 2. Project Detection

Use Glob and Read to detect the project structure:

```
Detect framework:
  next.config.* -> Next.js
  gatsby-config.* -> Gatsby
  astro.config.* -> Astro
  config.toml + /content/ -> Hugo
  _config.yml + _posts/ -> Jekyll
  none matched -> Generic

Detect blog directory:
  Glob for common paths: content/blog/, posts/, _posts/, src/content/blog/, blog/

Detect image directory:
  Glob for: public/images/, static/images/, assets/images/, src/assets/images/

Detect frontmatter format:
  Read 2-3 existing posts, extract YAML/TOML frontmatter fields

Detect naming convention:
  Examine filenames: YYYY-MM-DD-slug.md, slug.md, slug/index.md, etc.
```

### 3. Configuration Questions

Ask the user ONE question at a time. Suggest detected values when available.

1. **Blog post directory** — "I detected `content/blog/`. Use this, or specify another path?"
2. **Image directory** — "I detected `public/images/blog/`. Use this, or specify another path?"
3. **Post filename convention** — "Your posts use `YYYY-MM-DD-slug.md`. Keep this format?"
4. **Calendar file location** — "Where should the content calendar live? (default: `.seo-blog/calendar.md`)"
5. **Primary CTA** — Ask three sub-parts:
   - Action text (e.g., "Sign up free", "Start your trial")
   - Target URL
   - Can individual posts override the CTA? (yes/no)
6. **OpenRouter API key variable name** — "What is the variable name in `.env` for your OpenRouter key? (default: `OPENROUTER_API_KEY`)"

### 4. Write Config

Save all answers to `.seo-blog/config.md`:

```markdown
# SEO Blog Writer Configuration

## Project
- Framework: Next.js
- Blog directory: content/blog/
- Image directory: public/images/blog/
- Filename convention: YYYY-MM-DD-slug.md

## Calendar
- Location: .seo-blog/calendar.md

## CTA
- Action text: Sign up free
- Target URL: https://example.com/signup
- Posts can override: yes

## API
- OpenRouter key variable: OPENROUTER_API_KEY
```

### 5. Style Guide Generation

If existing blog posts were found, read up to 5 posts and analyze:

| Dimension | What to extract |
|---|---|
| Tone | Formal, casual, conversational, technical |
| Person | First (we/I), second (you), third (they) |
| Paragraph length | Average sentence count per paragraph |
| Headings | H2/H3 patterns, question-style vs statement |
| Formatting | Lists, callouts, blockquotes, code blocks |
| Opening pattern | Story, question, statistic, direct statement |
| Closing pattern | Summary, CTA, question, next-steps |
| Vocabulary | Domain terms, jargon level, recurring phrases |

Write findings to `.seo-blog/style-guide.md` with concrete examples pulled from the analyzed posts. If no posts exist, tell the user a style guide will be generated after their first post.

### Flow

```
.gitignore check
       |
   [PASS?]--NO--> REFUSE, stop
       |
      YES
       |
  Detect framework, dirs, format
       |
  Ask config questions (one at a time)
       |
  Write .seo-blog/config.md
       |
  [Posts exist?]--NO--> Skip style guide, notify user
       |
      YES
       |
  Analyze posts -> write .seo-blog/style-guide.md
       |
     DONE
```

## Common Mistakes

| Mistake | Why it matters | What to do instead |
|---|---|---|
| Skipping `.gitignore` check | API keys get committed to git | Always verify before any config work |
| Asking all questions at once | Overwhelms the user | Ask one question, wait for answer, then next |
| Guessing directories without detection | Wrong paths break all downstream skills | Always Glob first, suggest what you find |
| Generating style guide with < 2 posts | Too little data for reliable patterns | Need at least 2 posts; otherwise skip and note |
| Hardcoding frontmatter fields | Every framework uses different fields | Read actual posts and mirror their format exactly |
| Displaying API key values | Security violation | Only store the variable name, never the value |
