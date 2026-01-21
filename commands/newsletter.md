---
name: newsletter
description: Research trending content and generate a newsletter draft in under 60 seconds
---

## /newsletter

Creates a newsletter draft by researching trending content from newsletters and LinkedIn creators, then writing in your voice.

### Quick Start

Just run:
```
/newsletter
```

First time? You'll answer 2-3 quick questions. After that, you get a draft every time.

### Execution Flow

**Step 1: Check for first-run setup**

Check if `./newsletter/config.json` exists.

If it doesn't exist, run onboarding:

1. Ask the user (use AskUserQuestion tool):
   - "What's your niche?" (e.g., design to founder, solopreneur, SaaS, marketing)
   - "Who's your target audience?" (e.g., designers starting businesses, agency owners)

2. Ask optional follow-up:
   - "Paste 1-2 newsletter URLs you admire (or press enter to skip)"

3. Create the newsletter folder structure:
   ```
   ./newsletter/
   ├── config.json      # Their settings
   ├── voice.md         # Their voice profile (copied from defaults)
   ├── drafts/          # Where drafts go
   └── metrics/         # Where research goes
   ```

4. Copy the voice template from plugin defaults to `./newsletter/voice.md`

5. Create `./newsletter/config.json` with their answers:
   ```json
   {
     "niche": "[their answer]",
     "audience": "[their answer]",
     "customNewsletters": [],
     "customLinkedIn": [],
     "createdAt": "ISO timestamp"
   }
   ```

6. Tell the user:
   ```
   Setup complete!

   Your config: ./newsletter/config.json
   Your voice profile: ./newsletter/voice.md (edit this to sound more like you)

   Now researching and writing your first draft...
   ```

**Step 2: Load configuration**

1. Read `./newsletter/config.json` for niche, audience, custom sources
2. Read `./newsletter/voice.md` for their voice profile
3. Load starter creators from plugin's `defaults/starter-creators.json`
4. Merge user's custom sources with starter pack

**Step 3: Launch content-researcher agent**

Use the Task tool to launch the `content-researcher` agent with:

```json
{
  "sources": {
    "newsletters": [starter newsletters + user custom],
    "linkedinCreators": [starter LinkedIn + user custom]
  },
  "niche": "[from config]",
  "audience": "[from config]",
  "timeframeDays": 14
}
```

The agent will return research insights. Save the full research to:
`./newsletter/metrics/research-YYYY-MM-DD.json`

**Step 4: Launch newsletter-writer agent**

Use the Task tool to launch the `newsletter-writer` agent with:

```json
{
  "research": [research insights from Step 3],
  "voiceProfile": "./newsletter/voice.md",
  "writingRules": "[plugin path]/rules/writing-rules.md",
  "niche": "[from config]",
  "audience": "[from config]"
}
```

The agent will return:
- 3 subject line options
- Complete 500-800 word draft
- Key takeaways

**Step 5: Save and report**

1. Generate topic slug from the selected topic (lowercase, hyphens, no special chars)

2. Append the footer to the draft:
   ```markdown

   ---
   *Made with [Newsletter OS](https://github.com/jimifiliposvki/newsletter-os) by Jimi Filipovski*
   ```

3. Save draft to: `./newsletter/drafts/YYYY-MM-DD-{topic-slug}.md`

4. Report to user:
   ```
   Done!

   Draft saved to: ./newsletter/drafts/2026-01-20-your-topic.md
   Research saved to: ./newsletter/metrics/research-2026-01-20.json

   Subject line options:
   1. [First option]
   2. [Second option]
   3. [Third option]

   Open the draft to review and edit before sending.
   ```

### Optional Flags

**Research only:**
```
/newsletter --research-only
```
Runs research phase and saves report, but skips writing. Useful when you want to review trends before committing to a topic.

**Skip research:**
```
/newsletter --skip-research
```
Skips research and writes from the most recent research file. Only works if research exists and is less than 7 days old. Useful for writing multiple drafts from the same research.

**Specific topic:**
```
/newsletter --topic "your specific topic"
```
Focuses the research and writing on a specific topic you have in mind.

### File Locations Summary

| File | Purpose |
|------|---------|
| `./newsletter/config.json` | User's niche, audience, custom sources |
| `./newsletter/voice.md` | User's voice profile |
| `./newsletter/drafts/` | Generated newsletter drafts |
| `./newsletter/metrics/` | Research reports |

### Error Handling

- If WebFetch fails for a source, log it and continue with other sources
- If all sources fail, inform user and suggest checking URLs or trying again
- If research is empty, inform user no trending content was found
- If voice.md is missing, copy from defaults automatically

### Tips for Users

After running a few times:
1. Edit `./newsletter/voice.md` to better match your style
2. Add your own newsletters and LinkedIn creators to `./newsletter/config.json`
3. Review past research in `./newsletter/metrics/` to spot patterns
4. Keep drafts you like as reference for future voice matching
