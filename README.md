# Newsletter OS

Research trending content. Write newsletters that sound like you. Ship in under 60 seconds.

Built for designers and agency owners becoming founders — people who want to build an audience but don't know where to start with content.

## Installation

In Claude Code, run these two commands:

```
/plugin marketplace add jimiabreak/newsletter-os
/plugin install newsletter-os@jimiabreak-newsletter-os
```

That's it. You're ready to go.

## Quick Start

1. Run `/newsletter`
2. Answer 2-3 quick questions (first time only)
3. Get a ready-to-edit draft

That's it.

## What It Does

- **Researches** top newsletters and LinkedIn creators in your space
- **Identifies** trending topics and content gaps
- **Writes** a 500-800 word draft with 3 subject line options
- **Applies** proven writing rules that prevent AI-sounding content
- **Saves** everything locally to your project

## The Command

```
/newsletter
```

On first run, you'll answer a few quick questions:
- What's your niche?
- Who's your target audience?
- Any newsletters you admire? (optional)

After that, just run `/newsletter` and get a draft.

### Optional Flags

```
/newsletter --research-only       # Just run research, skip writing
/newsletter --skip-research       # Write from most recent research
/newsletter --topic "your topic"  # Focus on a specific topic
```

## What You Get

**Newsletter draft** saved to `./newsletter/drafts/YYYY-MM-DD-topic.md`:
- 3 subject line options (curiosity, benefit, contrarian)
- 500-800 word draft
- Actionable takeaways
- Your voice, not AI slop

**Research report** saved to `./newsletter/metrics/research-YYYY-MM-DD.json`:
- Top performing posts from your sources
- Trending topics across creators
- Content gaps and opportunities
- Why high-performers worked

## Customization

After first run, you'll have these files to customize:

| File | What to edit |
|------|--------------|
| `./newsletter/config.json` | Your niche, audience, custom sources |
| `./newsletter/voice.md` | Your voice profile and style |

The defaults work out of the box. Customize when you're ready.

## Writing Rules

This plugin ships with battle-tested writing rules that prevent AI-sounding content:

- No corporate jargon or marketing fluff
- No LLM patterns ("Let's dive in", "In conclusion")
- Banned words list (leverage, utilize, innovative, etc.)
- Active voice, specific examples, direct language

See `rules/writing-rules.md` for the full list.

## Starter Sources

The plugin ships with a curated list of popular newsletters and LinkedIn creators relevant to designers and founders. You can add your own sources anytime.

## Made By

[Jimi Filipovski](https://jimifiliposvki.co) — Designer turned founder, writing about the journey at [Designer to Founder]([https://www.jimisnewsletter.com/]).

I built this because I needed it. Researching content manually took hours. Now it takes a minute.

## Attribution

Every draft includes a small signature at the bottom. Feel free to keep it or remove it — your call.

---

*Made with [Newsletter OS](https://github.com/jimiabreak/newsletter-os) by Jimi Filipovski*
