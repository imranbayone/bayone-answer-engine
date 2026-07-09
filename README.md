# BayOne Reddit Answer Engine

An agent-assisted pipeline that monitors targeted subreddits, scores and drafts answers to relevant buyer questions, and routes them through a human review queue for BayOne's named executives to post manually.

**Why this exists:** AI chatbots (ChatGPT, Perplexity, Gemini, Claude, AI Overviews) are now a primary research channel for B2B buyers, and Reddit is the single largest source those engines cite from. BayOne currently has zero AI citations. This system exists to close that gap by getting genuine, expert, disclosed BayOne answers into the threads AI engines are already reading — without ever automating the actual posting.

This repo is the single source of truth for the project: agent skills, prompts, scoring rubric, subreddit targeting, rules of engagement, and setup docs. It does **not** contain any secrets (API keys, tokens, service-account credentials) — see [Secrets Policy](#secrets-policy) below.

---

## What This System Does

1. **Monitors** ~30 pilot subreddits daily using two Apify actors — a broad subreddit scan and a keyword/intent search — with no Reddit API key and no login required.
2. **Scores** every post found (0–100) against a rubric: is it a genuine question, does it map to a BayOne capability, is there buyer intent, is it answerable with a clear position.
3. **Drafts** an answer for posts that clear the threshold, in the voice of the relevant subject-matter expert, following BayOne's rules of engagement and style rules.
4. **Queues** every scored post and draft into a Google Sheet, split by portfolio.
5. **Never posts automatically.** A human portfolio owner reviews the queue, edits if needed, and a named BayOne executive posts manually from their own real, disclosed Reddit account.

```
Apify (scrape) → Hermes agent (score + draft) → Google Sheet (human queue) → Executive posts manually
```

The agent never logs into Reddit, never posts, and never touches Reddit directly. This is a deliberate design choice — see [docs/BAN_RISK_POSTURE.md](docs/BAN_RISK_POSTURE.md).

---

## Repo Structure

```
bayone-answer-engine/
├── README.md                      ← you are here
├── CHANGELOG.md                   ← dated log of what changed and why
├── .gitignore                     ← blocks all secrets from ever being committed
├── docs/
│   ├── ARCHITECTURE.md            ← full system design and component reasoning
│   ├── SERVER_SETUP.md            ← Lightsail + Hermes install, step by step
│   ├── GITHUB_WORKFLOW.md         ← how changes move from laptop → server
│   ├── SUBREDDIT_TARGETING.md     ← the 30 pilot subreddits, portfolios, why these
│   ├── RULES_OF_ENGAGEMENT.md     ← posting rules, style rules, disclosure requirements
│   ├── BAN_RISK_POSTURE.md        ← why this architecture carries near-zero ban risk
│   └── SPRINT_PLAN_SUMMARY.md     ← condensed version of the full Excel sprint plan
├── skills/                        ← Hermes SKILL.md files (added in Sprint 1-2)
│   └── (empty for now — reddit-monitor-broad, reddit-monitor-intent,
│         score-and-draft, sheets-writer land here)
└── prompts/                       ← scoring rubric + drafting prompt text (added in Sprint 2)
    └── (empty for now)
```

---

## Project Status

Currently in **Sprint 1** — infrastructure setup. See [docs/SPRINT_PLAN_SUMMARY.md](docs/SPRINT_PLAN_SUMMARY.md) for the full phase breakdown, or the master Excel sprint plan (kept outside this repo, shared separately) for the task-level detail.

| Phase | Status |
|---|---|
| Sprint 0 — Accounts & decisions | ✅ Complete (portfolio sign-off + executive commitments in progress separately) |
| Sprint 1 — Infrastructure & monitoring | 🔄 In progress — server launched, Hermes install next |
| Sprint 2 — Scoring & drafting brain | Not started |
| Sprint 3 — Pilot | Not started |
| Sprint 4 — Scale | Not started |

---

## Secrets Policy

**Nothing sensitive is ever committed to this repository.** No API keys, no `.env` files, no service-account JSON, no tokens. The `.gitignore` blocks these patterns by default. All secrets live only in the server's local configuration, entered directly on the server via SSH — never pasted into a file that gets committed, never shared over chat or email.

If you ever see a key, token, or credentials file staged in `git status`, stop and do not commit. Rotate the credential immediately if it was ever pushed.

---

## Who Owns What

| Portfolio | Owner | Service Lines |
|---|---|---|
| A — AI & Data | You | Artificial Intelligence, Data Engineering, Application Modernization |
| B — Infrastructure & Reliability | Rachel | SRE, Quality Engineering, Tech & Business Ops Support |
| C — Experience & Talent | Social Media Manager | UX, PMO Services, Talent Solutions |

Posting is done by named BayOne executives from their own real Reddit accounts — never by the agent, never anonymously.
