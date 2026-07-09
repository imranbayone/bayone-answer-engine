# Sprint Plan Summary

Condensed reference. The full task-level plan with owners, dependencies, and dates lives in the Excel workbook `BayOne_Reddit_Answer_Engine_Sprint_Plan.xlsx`, shared with the team outside this repo.

## Sprint 0 — Accounts & Decisions (Jul 13 – Jul 17)

AWS account with MFA and billing alert, OpenRouter account and key, Apify account and token, Google Cloud service account and master Sheet, GitHub private repo, portfolio sign-off from Rachel and the social media manager, and executive commitments with Reddit accounts created.

**Status:** Complete except portfolio sign-off and executive confirmation, in progress separately.

## Sprint 1 — Infrastructure & Monitoring Skeleton (Jul 20 – Jul 31)

Lightsail server launched and hardened, Hermes installed and connected to OpenRouter, server connected to GitHub via read-only deploy key, Skill 1a (`reddit-monitor-broad`) and Skill 1b (`reddit-monitor-intent`) built, Skill 3 (`sheets-writer`) built, full 30-subreddit daily scan running unattended.

**Status:** In progress. Server running; Hermes install and skills next.

**Milestone:** posts from all 30 pilot subreddits appear automatically in the Google Sheet.

## Sprint 2 — The Brain (Aug 3 – Aug 14)

BayOne content (blog posts, case studies) crawled into a knowledge base. Scoring rubric v1 built and threshold set. Skill 2 (`score-and-draft`) built, combining the cheap-model scoring pass and premium-model drafting pass. Calibration test with all three portfolio owners to measure precision before the pilot begins. One-page owner playbook written.

**Milestone:** Sheet fills with scored, drafted, owner-assigned rows ready for human review. Tag `v1.0-pilot`.

## Sprint 3 — Pilot (Aug 17 – Sep 11)

Four weeks of live queue review by all three owners and posting by executives, targeting 4–6 answers per week. Weekly tuning of prompts and rubric based on rejected drafts. Weekly Friday audits of 50 AI-engine prompts to check for early citations. Ends with a manager go/no-go review.

**Milestone:** ≥16 answers posted over the pilot, draft approval rate ≥60%.

## Sprint 4 — Scale (Sep 14 onward)

Expansion to Secondary-tier subreddits, twice-daily scans, a new citation-checker skill to semi-automate the Friday audit, an optional read-only dashboard (built with Emergent) reading from the Google Sheet for manager visibility, and recurring ops hardening (snapshots, key rotation, cost review).

## Success Metrics

| Metric | Pilot Target (Sep 11) | Oct 2026 Target |
|---|---|---|
| Answers posted / week | 4–6 | 8–12 |
| Draft approval rate | ≥60% | ≥75% |
| Queue precision | ≥60% | ≥80% |
| AI citations / week | First citations detected | 60/week |
| Share of AI Voice | Measurable signal | 18–20% |
| Owner review time / day | ≤15 min | ≤15 min |

## Top Risk

Executive posting cadence collapsing is the highest-scored risk in the register. Mitigated by keeping the per-executive time ask small (roughly 30 minutes a week), a visible tracking mechanism in the Sheet, and a fallback plan to run with fewer executives if needed rather than letting the whole pilot stall.
