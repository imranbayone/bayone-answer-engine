# Skills

Hermes SKILL.md files live here. Empty for now — populated in Sprint 1 (monitoring skills) and Sprint 2 (scoring and drafting skill).

Planned files:
- `reddit-monitor-broad/SKILL.md` — calls `trudax/reddit-scraper-lite` across all 30 pilot subreddits
- `reddit-monitor-intent/SKILL.md` — calls `harshmaur/reddit-scraper` keyword search scoped to the same subreddits
- `score-and-draft/SKILL.md` — scores posts and drafts answers via OpenRouter
- `sheets-writer/SKILL.md` — appends results to the Google Sheet queue

None of these files should ever contain an actual API key or token. Configuration values (which key to use) are referenced by name and set in the server's local Hermes config, not hardcoded here.
