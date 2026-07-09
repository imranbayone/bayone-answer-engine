# Changelog

All notable changes to this project are logged here, most recent first. This complements git commit history with a human-readable summary at each milestone.

## [Unreleased] — Sprint 1 in progress

### Added
- Repo scaffolding: README, architecture doc, server setup checklist, GitHub workflow guide, subreddit targeting doc, rules of engagement, ban risk posture doc, sprint plan summary
- Lightsail instance `bayone-answer-engine` launched (Mumbai, Ubuntu 24.04, 2GB plan)

### Decided
- Dual Apify actor approach confirmed: `trudax/reddit-scraper-lite` for broad daily subreddit scanning, `harshmaur/reddit-scraper` for keyword/intent-phrase search, both scoped to the same 30 pilot subreddits and tagged by source for later comparison
- Pilot subreddit list narrowed from 156 (full targeting map) to 30 (Primary tier only), split across 3 owner portfolios
- Architecture shifted from OpenClaw to Hermes agent framework after OpenClaw's disclosed security vulnerabilities (CVE-2026-32922 and others) made it unsuitable for a server holding API keys and executive-adjacent data
- Human-only posting confirmed as a permanent architectural constraint, not a pilot-phase limitation

## [Sprint 0] — 2026-07-13 to 2026-07-17

### Added
- AWS account, OpenRouter account, Apify account, Google Cloud service account and master Sheet, GitHub private repository — all created
- Initial 6-sheet sprint plan workbook built covering overview, task-level sprint plan, phased Gantt view, pilot subreddit list, Google Sheet queue template, and KPIs/risk register
