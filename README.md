# SEO Blog Writer

A Claude Code plugin for researching and writing SEO-optimized blog posts. Project-agnostic — works with any blog framework, outputs markdown.

## Skills

| Skill | Purpose |
|-------|---------|
| `seo-setup` | First-run project configuration, style guide generation |
| `seo-calendar` | Content calendar planning with keyword research and gap analysis |
| `seo-research` | Deep competitor analysis, source gathering, angle identification |
| `seo-outline` | Post structure planning with keyword, CTA, and image placement |
| `seo-draft` | Full post writing on a dedicated git branch |
| `seo-images` | AI image generation via OpenRouter, placeholder replacement |
| `seo-finalize` | Source verification, SEO checks, markdown validation, finalization |

## Workflow

```
seo-setup (once per project)
    |
seo-calendar --> pick a topic --> seo-research --> seo-outline --> seo-draft --> seo-images --> seo-finalize
                                                                    |                            |
                                                                    |--- creates blog branch -----|--- ready for review
```

Skills can be run individually or chained. Each reads/writes to a shared `.seo-blog/` directory.

## Installation

Register the marketplace:

```bash
/plugin marketplace add kbanta11/kbanta11-claude-tools
```

Install the plugin:

```bash
/plugin install seo-blog-writer@kbanta11-claude-tools
```

## Configuration

### OpenRouter (for image generation)

Add your API key to the project's `.env` file:

```
OPENROUTER_API_KEY=your-key-here
```

**Important:** Ensure `.env` is in your `.gitignore`. The plugin verifies this before reading any keys.

### First Run

Run `/seo-setup` in your project. It will detect your project structure and ask configuration questions to set up `.seo-blog/config.md` and `.seo-blog/style-guide.md`.

## File Structure

The plugin creates a `.seo-blog/` directory in your project:

```
.seo-blog/
  config.md          # Project settings (blog dir, image dir, CTA, etc.)
  style-guide.md     # Auto-generated and auto-updated writing style reference
  calendar.md        # Content calendar with topics, keywords, status
  research/
    <topic-slug>.md  # Research notes per topic
```

## License

MIT
