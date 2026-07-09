# Ban Risk Posture

Why this architecture carries near-zero risk of any Reddit account being banned, and why that was a first-class design constraint rather than an afterthought.

## The Core Design Choice

**The agent never touches Reddit. A human always does the posting.**

Every other decision in this system flows from that one line. Scraping happens through Apify, which reads Reddit's public web pages rather than logging in or calling Reddit's API. Scoring and drafting happen entirely inside the agent, which never authenticates as any Reddit account. The only step where a Reddit account is involved at all is the final one — a named executive, logged in as themselves, choosing to post an answer they've reviewed and, if needed, edited.

This means there is no automated behavior for Reddit's anti-spam systems to detect, because there is no automated posting. What Reddit sees is a real account, with a real history, posting at a human and irregular pace, using its own judgment about tone and timing.

## Why Not Automate Posting Too

It would technically be possible to have the agent post directly using a Reddit account's credentials. This was deliberately ruled out, for two separable reasons:

1. **Ban risk.** Automated posting patterns, even well-disguised ones, are exactly what Reddit's detection systems are built to catch. Volume, timing regularity, and response latency are all signals. A human posting when they have five minutes free doesn't produce those signals; a script does.
2. **Brand integrity, independent of ban risk.** The plan requires disclosed, named executives with genuine expertise standing behind their words. An automated post, even from a real named account, is not actually that person's answer. If this were ever discovered, the reputational cost would be far worse than a temporary ban — it would undermine the credibility the whole citation strategy depends on.

## Supporting Practices

- **Account warm-up.** New executive accounts build a small amount of organic history before their first substantive answer (see `RULES_OF_ENGAGEMENT.md`).
- **Rare linking.** Most answers carry no BayOne link at all, which avoids the single most common trigger for spam flags and moderator removals.
- **Subreddit-specific rule checks.** Executives check each subreddit's own posting rules before their first answer there.
- **Human pacing.** Because a person decides when to post, the natural irregularity of human schedules is preserved rather than smoothed into a predictable, botlike cadence.
- **No third-party skill packs on the server.** Reduces the chance that an unrelated compromise ever gives an attacker a path to Reddit credentials, which are never stored on the server in the first place — the agent has none to store.

## What This Does Not Protect Against

This posture protects against automated-behavior detection and against the agent itself being a source of risk. It does not replace ordinary judgment: an executive who posts too frequently, too promotionally, or without regard for a subreddit's culture can still attract negative attention or a ban on their own account, the same as any other Reddit user. The rules of engagement exist to guard against that separately.
