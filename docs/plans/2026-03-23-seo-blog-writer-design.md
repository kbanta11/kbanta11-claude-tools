# SEO Blog Writer Plugin — Design Document

## Overview

A Claude Code plugin with 7 skills for researching and writing SEO-optimized blog posts. Project-agnostic — outputs markdown files that work with any blog framework. Skills chain together through a shared `.seo-blog/` directory for state and configuration.

## Goals

- Automate the full SEO blog workflow from topic ideation to finalized post
- Beat competitor content by systematically analyzing what ranks and finding gaps
- Maintain writing consistency across posts via auto-generated style guides
- Generate a content calendar driven by keyword research and project analysis
- Include organic, topic-aware CTAs in every post
- Keep API keys secure (`.env` + `.gitignore` enforcement)
- Create each blog on its own git branch for review before publishing

## Configuration (`.seo-blog/config.md`)

On first use, `seo-setup` detects and asks:
- Blog post directory (e.g., `content/blog/`, `posts/`)
- Image directory (e.g., `public/images/blog/`)
- Blog post format (frontmatter fields, file naming convention)
- Calendar file location
- Primary CTA (action text, target URL, whether posts can override)
- OpenRouter API key location (must be in `.env`, `.gitignore` verified)

## Skills

### 1. `seo-setup`
**Trigger:** First use in a project, or explicit reconfiguration.

- Detects project structure (framework, existing posts, image dirs)
- Asks configuration questions, writes `.seo-blog/config.md`
- Analyzes existing blog posts to generate `.seo-blog/style-guide.md`
- Asks for primary CTA (action, URL, override policy)
- Verifies `.env` is in `.gitignore`, refuses to proceed if not

### 2. `seo-calendar`
**Trigger:** User wants to plan blog content or find topic opportunities.

- Takes seed ideas from user
- Analyzes project (README, landing pages, features) for context
- Scans existing blog posts to map covered topics
- Keyword research via WebSearch (Google + Bing) for volume signals and ranking opportunities
- Identifies content gaps and low-competition opportunities
- Generates/updates `.seo-blog/calendar.md`
- Each entry: topic, primary keyword, secondary keywords, target audience, CTA target (specific feature/page), internal link targets, priority score, status

### 3. `seo-research`
**Trigger:** User picks a topic to write about.

- Input: topic (from calendar or ad-hoc)
- Searches Google + Bing for top-ranking content
- Deep-reads top 5-10 competitor articles
- Analyzes strengths, weaknesses, missing angles
- Researches authoritative sources — saves URLs, key claims, exact quotes
- Verifies source accuracy (URLs live, quotes real)
- Outputs `.seo-blog/research/<topic-slug>.md`

### 4. `seo-outline`
**Trigger:** Research complete, ready to plan the post.

- Reads research file + style guide + existing posts (for internal linking)
- Re-validates style guide against current posts, updates if drifted
- Proposes heading structure, keyword placement strategy, internal links
- Plans CTA placement (mid-article natural nudge + end-of-post CTA)
- Plans image placement (header + 1-2 body images) with descriptions
- Presents outline for user approval before proceeding

### 5. `seo-draft`
**Trigger:** Outline approved, ready to write.

- Creates git branch: `blog/<topic-slug>`
- Writes full markdown draft following approved outline
- Matches writing style from style guide
- Natural keyword usage (no stuffing)
- Inserts image placeholders with:
  - Detailed AI generation prompt
  - Target filename (e.g., `images/blog/<topic-slug>/header.png`)
- Proper source citations with links
- Organic CTAs tailored to topic
- Frontmatter matching project's existing format

### 6. `seo-images` (optional)
**Trigger:** User wants to generate images for a draft.

- Reads image placeholders from draft
- Reads OpenRouter API key from `.env`
- Calls OpenRouter to generate images using embedded prompts
- Saves to correct location (`images/blog/<topic-slug>/`)
- Replaces placeholders with actual image references
- Commits images to blog branch

### 7. `seo-finalize`
**Trigger:** Draft complete, ready for final review.

- Re-verifies all cited sources (links live, claims accurate)
- Checks SEO metadata (title length, meta description, heading hierarchy)
- Checks keyword density
- Validates markdown syntax
- Checks mobile-friendliness (line lengths, image sizing)
- Updates style guide if post introduces new patterns
- Updates calendar status to "complete"
- Final commit on blog branch

## Skill Chaining

Full workflow: `seo-calendar` -> pick topic -> `seo-research` -> `seo-outline` -> `seo-draft` -> `seo-images` -> `seo-finalize`

Each skill reads/writes to `.seo-blog/` directory. Users can jump in at any point.

## File Structure

```
.seo-blog/
  config.md              # Project-specific settings
  style-guide.md         # Auto-generated writing style reference
  calendar.md            # Content calendar
  research/
    <topic-slug>.md      # Research notes per topic
```

## Security

- API keys in `.env` only
- Skill verifies `.env` is in `.gitignore` before reading keys
- Never echo/log key values
- Keys never appear in markdown output or commits
