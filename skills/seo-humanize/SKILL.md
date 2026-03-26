---
name: seo-humanize
description: >
  Use when the user asks to humanize, de-AI, or make a blog post sound less like
  AI-generated content. Also use when the user says "humanize the post",
  "make it sound human", "remove AI tone", or "clean up the draft" for a post
  that already exists on a blog/<topic-slug> branch.
---

# Humanize Blog Post

Remove AI writing fingerprints from a blog draft while preserving content, meaning, and the author's established voice. Runs as a two-pass process: analyze then rewrite.

## Prerequisites

- A draft post exists on a `blog/<topic-slug>` branch
- `.seo-blog/config.md` is present
- `.seo-blog/style-guide.md` is present

If any file is missing, stop and tell the user exactly which prerequisite is needed.

## Context Loading

Read ALL of the following before starting:

1. `.seo-blog/style-guide.md` — this is your voice constraint. Every rewrite must stay within this voice.
2. `.seo-blog/config.md` — extract blog directory path to locate the draft
3. The draft post on the current `blog/<topic-slug>` branch
4. 1-2 existing published posts from the blog directory — use these as a baseline for what "human" sounds like in this blog's voice

## Pass 1: Analysis

Scan the entire draft and internally catalog every AI tell found. Group findings by category. If the user has asked you to report back before rewriting, present the report and wait for approval. Otherwise proceed directly to Pass 2.

### Word-Level Flags

**Flagged words** — these are NOT banned. Track frequency. If a flagged word appears more than once in the post, mark all but one occurrence for replacement. If it appears once and fits naturally, leave it. The goal is "don't default to these words" not "never use them."

Flagged word list (non-exhaustive — flag similar words when spotted):

| Category | Words |
|---|---|
| Verbs | delve, leverage, utilize, foster, harness, navigate, embark, elevate, unleash, spearhead, underscore, streamline, revolutionize, optimize, facilitate, empower, catalyze, bolster, illuminate, cultivate |
| Adjectives | robust, comprehensive, cutting-edge, seamless, pivotal, meticulous, groundbreaking, innovative, transformative, state-of-the-art, vibrant, bustling, intricate, holistic, multifaceted |
| Nouns | tapestry, landscape, realm, journey, testament, labyrinth, paradigm, synergy, ecosystem, cornerstone, bedrock, nexus, catalyst, linchpin |
| Adverbs | seamlessly, profoundly, meticulously, strategically, fundamentally, remarkably, inherently |

**Filler transitions** — flag if used more than twice total in the post: Furthermore, Moreover, Additionally, Notably, Consequently, Subsequently, Indeed, Accordingly, Nonetheless.

**"Magic" adverbs** — flag adverbs injecting false gravitas into ordinary claims: quietly, deeply, fundamentally, remarkably, profoundly. Keep only if the sentence genuinely warrants emphasis.

### Phrase-Level Flags

Flag every occurrence of these patterns:

- "In today's [digital age / world / landscape]..."
- "In the ever-evolving [world / landscape / realm] of..."
- "Let's [dive in / delve into / explore]..."
- "It's worth noting that..." / "It's important to note..."
- "Unlock the [potential / secrets / power] of..."
- "Harness the power of..." / "Foster a culture of..."
- "[noun] is a game-changer" / "...is a testament to..."
- "In conclusion..." / "In summary..." / "To summarize..."
- "Think of it as..." / "Here's the thing:" / "Here's the kicker:"
- "...serves as a [reminder / testament / example]..." (the "serves as" dodge)

### Sentence-Level Flags

- **Negative parallelism**: "It's not X — it's Y" or "It's not about X, it's about Y" constructions
- **Stacked negation**: "Not X. Not Y. Just Z." dramatic countdown patterns
- **Rhetorical Q&A**: self-posed question immediately answered ("The result? A more robust framework.")
- **Anaphora abuse**: 3+ consecutive sentences starting with the same word or phrase
- **Tricolon overuse**: compulsive grouping in threes ("faster, smarter, and more efficient") — flag when it appears more than once in the post
- **Em dash overuse**: count all em dashes (—). Target: max 1-2 per 500 words. Flag the rest for replacement.
- **Colon as dramatic device**: "Here's the thing:" / "There's a catch:" / "The answer is simple:"
- **"From X to Y" false ranges**: "From healthcare to education, from finance to entertainment..."
- **-ing phrase injection**: tacked-on participial phrases that add no substance ("...creating a more inclusive environment")

### Structure-Level Flags

- **Uniform paragraph length**: 3+ consecutive paragraphs within ~10 words of each other
- **Low burstiness**: sentence lengths too consistent throughout a section (measure standard deviation of sentence word counts — low variance = flag)
- **Fractal summaries**: section endings that restate the section + article conclusion that restates the whole post
- **Bold-first bullets**: every item in a list opens with **bold text**: followed by explanation
- **Democratic attention**: every topic/section gets nearly identical word count rather than spending more on what matters most
- **Perpetual balance**: "While some argue X, others contend Y" hedging where a clear position would be more natural
- **Signposted conclusion**: explicitly saying "In conclusion" or "To wrap up" rather than letting the ending emerge naturally

## Pass 2: Rewrite

Apply fixes for every flagged item. Follow these rewrite rules strictly.

### Hard Constraints

- Do NOT change the meaning or factual content of any sentence
- Do NOT remove or add citations/sources
- Do NOT alter keyword placement from the outline's keyword plan
- Do NOT touch frontmatter, image placeholders, or CTAs
- Do NOT add new sections, headings, or restructure the post's outline
- Preserve the voice and tone from `.seo-blog/style-guide.md` at all times
- Read the style guide AGAIN if you're unsure whether a rewrite matches the voice

### Rewrite Rules

**Words:**
- Replace excess flagged words with plain English (leverage -> use, utilize -> use, robust -> strong, facilitate -> help, etc.). Keep at most one occurrence if it fits naturally.
- Replace filler transitions with shorter connectors: But, So, And, Still, Yet, Meanwhile — or remove entirely if the connection is obvious without one.
- Remove magic adverbs unless the sentence genuinely needs the emphasis.

**Phrases:**
- Replace cliche openers with direct statements. "In today's digital age, businesses need..." -> "Businesses need..."
- Remove "it's worth noting" / "it's important to note" — just state the thing.
- Replace "serves as" with "is" or rephrase directly.
- Remove signposted conclusions — cut "In conclusion" and let the final paragraph stand on its own.

**Sentences:**
- "Not X — it's Y" -> rephrase as a direct positive statement. "It's not about speed — it's about consistency" -> "Consistency matters more than speed"
- Rhetorical Q&A -> merge into a single direct statement. "The result? Faster deployments." -> "This cut deployment time significantly."
- Anaphora -> vary sentence openings. If three sentences start with "This", rewrite two of them with different subjects.
- Em dashes -> replace excess with commas, parentheses, periods, or semicolons depending on context. Keep 1-2 em dashes per 500 words maximum.
- Colon as drama -> rephrase as a normal sentence or remove the setup entirely.
- Tricolon -> vary list lengths. Sometimes two items, sometimes four. Don't always group in threes.
- "-ing" phrase injection -> cut the phrase if it adds nothing, or rewrite as its own sentence if the idea matters.

**Structure:**
- Uniform paragraphs -> vary length. Some paragraphs should be 1 sentence. Others 3-4 sentences. Break the rhythm.
- Low burstiness -> mix short punchy sentences (3-7 words) among longer ones (15-25 words) within the same paragraph.
- Fractal summaries -> remove redundant section-end restating. Keep only the final conclusion, and trim it to say something new or forward-looking rather than repeating.
- Bold-first bullets -> vary list formatting. Some items can lead with bold, others don't need it.
- Democratic attention -> this is informational only. Do not add or remove content, but note it in the report if present.
- Perpetual balance -> where the blog's position is clear, let it be clear. Remove unnecessary "on the other hand" hedging.

### Citation Formatting

- **Mid-sentence citations**: leave as inline markdown links (no change)
- **End-of-sentence/paragraph citations**: wrap in parentheses. Example: `...showed a 40% improvement ([Stanford Research](https://example.com)).`
- Do not change anchor text or URLs — only adjust the wrapping punctuation.

## Save and Commit

- Save the humanized post, overwriting the draft
- Stage the file: `git add <filepath>`
- Commit on the blog branch: `git commit -m "humanize: <topic-slug>"`

## Common Mistakes

| Mistake | Why It's Wrong | What To Do Instead |
|---|---|---|
| Banning flagged words entirely | Sometimes "utilize" really is the best word | Allow up to one natural occurrence per post |
| Changing content meaning while rewriting | The skill humanizes tone, not substance | Re-read original sentence after rewriting to confirm meaning is preserved |
| Over-casualizing the tone | The post should match the blog's voice, not sound like a text message | Check every rewrite against the style guide |
| Removing all em dashes | Em dashes are legitimate punctuation — humans use them too | Keep 1-2 per 500 words, replace only the excess |
| Restructuring the post | Humanizing is not editing or reorganizing | Preserve all headings, sections, and outline structure |
| Making every paragraph short | Uniformly short paragraphs are just as robotic as uniformly long ones | Vary — some short, some medium |
| Ignoring the style guide | Rewrites that don't match the blog's voice create inconsistency | Read the style guide before starting and reference it throughout |
