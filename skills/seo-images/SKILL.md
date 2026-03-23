---
name: seo-images
description: "Use when the user asks to generate images for a blog draft, replace image placeholders, or create blog post illustrations. Also use when the user references IMAGE_PLACEHOLDER blocks or asks to finalize a draft's images."
---

# SEO Blog Image Generation

## Prerequisites

Before starting, verify ALL of the following:

1. `.seo-blog/config.md` exists in the project root. Read it for blog settings (image dimensions, style preferences, output paths).
2. A draft file exists containing one or more `<!-- IMAGE_PLACEHOLDER ... -->` blocks.
3. A `.env` file exists at the project root with `OPENROUTER_API_KEY` set (or the key name specified in `config.md`).
4. **CRITICAL:** Confirm `.env` is listed in `.gitignore` BEFORE reading the key. Run `grep -q '\.env' .gitignore` and check the exit code. If `.env` is NOT gitignored, REFUSE to proceed and instruct the user to add it.

## Security Rules

- NEVER display, log, echo, or include the API key value in any output.
- Read the key in Bash using `source .env` or `grep`, and reference it only via shell variable expansion (e.g., `$OPENROUTER_API_KEY`).
- The key must never appear in markdown content, commit messages, tool output, or error reports.

## Workflow

### 1. Parse Placeholders

Search the draft for all `<!-- IMAGE_PLACEHOLDER ... -->` comment blocks. Each block contains three fields to extract:

- `filename`: the target save path for the generated image (e.g., `images/blog/my-topic/hero.png`)
- `alt`: the alt text for the image
- `prompt`: the text prompt for image generation

### 2. Generate Images

For each placeholder:

1. Create the target directory if it does not exist (e.g., `mkdir -p images/blog/<topic-slug>/`).
2. Call the OpenRouter API via `curl` in Bash. Use model `openai/dall-e-3` (or another image-capable model on OpenRouter). Pass the extracted `prompt` as the generation input.
3. Save the returned image data to the path specified in `filename`.
4. **Error handling:**
   - **Rate limits (HTTP 429):** Retry up to 3 times with exponential backoff (2s, 4s, 8s).
   - **Model errors / failures:** Log which image failed, skip it, and continue with remaining images. Report all failures to the user at the end.

### 3. Replace Placeholders

For each successfully generated image:

- Remove the `<!-- IMAGE_PLACEHOLDER ... -->` comment block from the draft.
- Keep the `![Alt text](path)` markdown image reference that accompanies the placeholder — it already contains the correct path and alt text.

### 4. Review With User

After all images are processed:

- List which images were successfully created and their file paths.
- List any that failed and why.
- Ask the user if any images need regeneration. If yes, accept an adjusted prompt for each and regenerate only those specific images.

### 5. Commit

Once the user approves all images:

- Stage the generated image files and the updated draft file.
- Commit to the current blog branch with a descriptive message (never include API keys in the message).

## Common Mistakes

| Mistake | Prevention |
|---|---|
| Exposing the API key in output or logs | Always use shell variables; never print or echo the key value |
| Reading `.env` without checking `.gitignore` | Always verify `.env` is gitignored before reading; refuse if not |
| Wrong image save path | Use the exact `filename` from the placeholder block; create directories with `mkdir -p` |
| Leaving placeholder comments in the draft | Confirm each `<!-- IMAGE_PLACEHOLDER -->` block is removed after successful generation |
| Committing `.env` to the repository | Never stage `.env`; only stage image files and the updated draft |
| Ignoring generation failures | Track and report all failures; prompt user for retry decisions |
