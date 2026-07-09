# Subreddit Targeting — Pilot List (30)

Narrowed from a 156-subreddit master map (Primary/Secondary/Tertiary tiers across 9 BayOne service lines) down to a focused pilot list. Full expansion back to Secondary/Tertiary tiers happens in Sprint 4 once precision is proven at this scale.

## Selection Logic

Every subreddit on this list passed three filters:
1. Maps to a named capability on a live BayOne service page
2. Verified active (confirmed member count and posting velocity)
3. Primary tier only — buyer presence and intent, not just topical adjacency

Subreddits appearing under multiple service lines (e.g., r/devops) are housed once, under the portfolio where they carry the most weight, to avoid duplicate monitoring.

## Portfolio A — AI & Data (Owner: You)

| Subreddit | Service Line | Note |
|---|---|---|
| r/ArtificialInteligence | Artificial Intelligence | ~1.74M members, biggest AI sub (misspelled handle) |
| r/AI_Agents | Artificial Intelligence | ~374K, fast-growing +5.5%/mo |
| r/MachineLearning | Artificial Intelligence | ~3M, research hub |
| r/datascience | AI / Data Engineering | |
| r/automation | AI (RPA, process optimization) | |
| r/dataengineering | Data Engineering | ~440-460K, ~32 posts/day, highest intent density |
| r/MLOps | Data Engineering / AI | |
| r/analytics | Data Engineering | |
| r/BusinessIntelligence | Data Engineering / AI | |
| r/ExperiencedDevs | Application Modernization | Senior-dev buyer presence |
| r/softwarearchitecture | Application Modernization | |

## Portfolio B — Infrastructure & Reliability (Owner: Rachel)

| Subreddit | Service Line | Note |
|---|---|---|
| r/sre | Site Reliability Engineering | |
| r/devops | SRE / App Mod / Quality Eng | Appears under 3 service lines; housed once here |
| r/sysadmin | SRE / Tech Ops | |
| r/kubernetes | SRE / App Mod | |
| r/QualityAssurance | Quality Engineering | |
| r/softwaretesting | Quality Engineering | |
| r/ITManagers | Tech & Business Ops | Manager-level buyer intent |
| r/msp | Tech & Business Ops | |
| r/servicedesk | Tech & Business Ops | |

## Portfolio C — Experience & Talent (Owner: Social Media Manager)

| Subreddit | Service Line | Note |
|---|---|---|
| r/UXDesign | Experience Design | |
| r/userexperience | Experience Design | |
| r/UXResearch | Experience Design | |
| r/ProductManagement | UX / PMO | |
| r/projectmanagement | PMO Services | |
| r/agile | PMO Services | |
| r/recruiting | Talent Solutions | |
| r/humanresources | Talent Solutions | |
| r/talentacquisition | Talent Solutions | |
| r/startups | Talent Solutions | Founder audience, staffing intent |

## Changing This List

If a portfolio owner wants to swap a subreddit, update this file and the corresponding Apify actor input in `skills/reddit-monitor-broad/SKILL.md`, then commit both changes together with a note explaining the swap.
