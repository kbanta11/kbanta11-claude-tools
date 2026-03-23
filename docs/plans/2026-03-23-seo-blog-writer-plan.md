# SEO Blog Writer Plugin — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a Claude Code plugin with 7 skills for SEO blog post research, planning, writing, and optimization.

**Architecture:** Each skill is a `SKILL.md` file in `skills/<skill-name>/`. Skills chain through a shared `.seo-blog/` directory in the target project. The plugin manifest lives in `.claude-plugin/plugin.json`.

**Tech Stack:** Markdown skill files, Claude Code plugin system, WebSearch/WebFetch for research, OpenRouter API for image generation via Bash/curl.

---

### Task 1: Write `seo-setup` skill

**Files:**
- Create: `skills/seo-setup/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-setup`, description about first-use configuration
- Security check (.env in .gitignore verification)
- Project structure detection (framework, existing posts, image dirs, frontmatter format)
- Configuration questions asked one at a time (blog dir, image dir, filename format, CTA, calendar location, OpenRouter key)
- Write config to `.seo-blog/config.md`
- Style guide generation from existing posts (tone, structure, formatting, vocabulary, opening/closing patterns)
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-setup/SKILL.md
git commit -m "feat: add seo-setup skill — project detection, config, style guide generation"
```

---

### Task 2: Write `seo-calendar` skill

**Files:**
- Create: `skills/seo-calendar/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-calendar`, description about content planning and keyword opportunities
- Prerequisites check (config must exist)
- Seed idea gathering from user
- Project analysis (README, landing pages, features, existing posts)
- Keyword research on Google AND Bing (topic variations, long-tail, comparison, freshness)
- Scoring: relevance, opportunity, volume signals, content gap, internal linking, CTA alignment
- Internal linking opportunity identification
- Calendar format in `.seo-blog/calendar.md` with priority tiers, keywords, audience, CTA target, status
- Update logic for existing calendars
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-calendar/SKILL.md
git commit -m "feat: add seo-calendar skill — keyword research, gap analysis, content planning"
```

---

### Task 3: Write `seo-research` skill

**Files:**
- Create: `skills/seo-research/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-research`, description about competitor analysis and source verification
- Prerequisites check
- Target keyword identification (from calendar or ad-hoc)
- Competitor analysis: top 5-10 results on Google AND Bing, deep-read with WebFetch, document strengths/weaknesses/angles
- Angle identification: what's missing, outdated, shallow across all top results
- Source research: academic papers, industry reports, expert quotes, case studies
- **Critical source verification**: WebFetch every URL, confirm claims exist on page, mark unverified
- Save to `.seo-blog/research/<topic-slug>.md`
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-research/SKILL.md
git commit -m "feat: add seo-research skill — competitor analysis, source verification, angle identification"
```

---

### Task 4: Write `seo-outline` skill

**Files:**
- Create: `skills/seo-outline/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-outline`, description about post structure planning
- Prerequisites check (config, research, style guide)
- Style guide re-validation (compare to recent posts, update if drifted)
- Heading structure with SEO best practices (keyword in H1 and H2s, scannable, under 60 chars)
- Keyword placement plan per section (1-2% density, no stuffing)
- CTA placement: mid-article natural nudge + end-of-post direct CTA
- Image placement: header + 1-2 body images with descriptions
- Internal linking plan (TO and FROM existing posts)
- Present complete outline for user approval — **do not proceed without approval**
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-outline/SKILL.md
git commit -m "feat: add seo-outline skill — heading structure, keyword strategy, CTA and image planning"
```

---

### Task 5: Write `seo-draft` skill

**Files:**
- Create: `skills/seo-draft/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-draft`, description about writing the full post
- Prerequisites check (config, style guide, research, approved outline)
- Create git branch `blog/<topic-slug>`
- Read all context (config, style guide, research, outline, existing posts for voice matching)
- Write frontmatter matching project format
- Writing rules: match style guide, natural keyword usage, short paragraphs, transitions
- Source citation rules: only verified sources, inline links, never fabricate
- CTA writing: natural mid-article + direct end-of-post
- Image placeholder format with detailed AI generation prompts (subject, style, palette, mood, composition, aspect ratio, what to avoid)
- Save and commit to branch
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-draft/SKILL.md
git commit -m "feat: add seo-draft skill — full post writing with branch, citations, image placeholders, CTAs"
```

---

### Task 6: Write `seo-images` skill

**Files:**
- Create: `skills/seo-images/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-images`, description about AI image generation from placeholders
- Prerequisites check (config, .env with OPENROUTER_API_KEY, draft with placeholders)
- Security verification (.gitignore check before reading .env, never display key)
- Parse IMAGE_PLACEHOLDER blocks from draft
- Create image directory
- OpenRouter API calls via curl (model selection, error handling, rate limit retry)
- Save images to correct paths
- Replace placeholders in markdown (remove comment block, keep image tag)
- Commit images to blog branch
- Regeneration flow for unsatisfactory images
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-images/SKILL.md
git commit -m "feat: add seo-images skill — OpenRouter image generation, placeholder replacement"
```

---

### Task 7: Write `seo-finalize` skill

**Files:**
- Create: `skills/seo-finalize/SKILL.md`

**Step 1: Write the SKILL.md file** with complete content including:
- Frontmatter: name `seo-finalize`, description about final review and verification
- Prerequisites check (draft on blog branch, config, research)
- Source re-verification: WebFetch every cited URL, confirm claims, find alternatives if broken
- SEO metadata checklist: title, meta description, H1, H2s, slug, first paragraph, alt text, internal links, keyword density
- Content quality review: readability, scanability, transitions, CTA integration, accuracy
- Markdown validation: broken syntax, image paths, heading hierarchy, code blocks, frontmatter
- Mobile-friendliness: line lengths, table widths, image sizing, paragraph length
- Style guide update if new patterns introduced
- Calendar update (status to complete)
- Final commit on blog branch
- Finalization report with SEO score, source verification results, issues fixed
- Common mistakes table

**Step 2: Commit**
```bash
git add skills/seo-finalize/SKILL.md
git commit -m "feat: add seo-finalize skill — source verification, SEO checks, markdown validation, finalization"
```

---

### Task 8: Write plugin README.md and CLAUDE.md

**Files:**
- Create: `README.md`
- Create: `CLAUDE.md`

**Step 1: Write README.md** with:
- Plugin name and description
- Skills table (name + purpose for each)
- Workflow diagram showing skill chain
- Installation instructions (marketplace add + plugin install)
- Configuration notes (.env for OpenRouter)
- License (MIT)

**Step 2: Write CLAUDE.md** with:
- Brief plugin description
- How skills chain through `.seo-blog/` directory
- Key rules: always run setup first, always use blog branches

**Step 3: Commit**
```bash
git add README.md CLAUDE.md
git commit -m "docs: add README and CLAUDE.md for plugin overview and installation"
```

---

### Task 9: Write marketplace.json

**Files:**
- Create: `.claude-plugin/marketplace.json`

**Step 1: Write marketplace.json** with:
- Marketplace name: `kbanta11-claude-tools`
- Plugin entry for `seo-blog-writer` with source `./`

**Step 2: Commit**
```bash
git add .claude-plugin/marketplace.json
git commit -m "feat: add marketplace manifest for plugin distribution"
```

---

### Task 10: Create GitHub repo and push

**Step 1: Create repo**
```bash
gh repo create kbanta11-claude-tools --public --source=. --push
```

**Step 2: Verify**
```bash
gh repo view kbanta11-claude-tools
```

---
