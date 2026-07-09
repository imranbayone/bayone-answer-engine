# SKILL: reddit-monitor-broad

## Purpose
Fetch recent posts from BayOne's pilot subreddits using the Apify actor `trudax/reddit-scraper-lite`. This skill is READ-ONLY reconnaissance: it collects posts so they can later be scored and drafted. It never logs into Reddit, never posts, never comments, never votes.

## Hard Rules
1. NEVER attempt to post, reply, vote, or log in to Reddit in any way. This skill only reads public data via Apify.
2. NEVER print, echo, or write the Apify token anywhere in output, logs, memory, or files. It is referenced only as an environment variable.
3. If the Apify call fails, report the HTTP status and error body summary, then stop. Do not retry more than twice.
4. Stay within budget: never request more than 30 items per subreddit in a single run.

## Requirements
- Environment variable `APIFY_TOKEN` must be set in `~/.hermes/.env`. If it is missing, stop and tell the user to add it. Do not ask the user to paste the token into chat.
- The subreddit list lives in `~/bayone-answer-engine/skills/reddit-monitor-broad/subreddits.json`. Always read it fresh from that file; do not use a memorized copy.

## How to Fetch Posts
Call the Apify "run actor synchronously and get dataset items" endpoint using curl through the terminal tool.

Endpoint:
```
POST https://api.apify.com/v2/acts/trudax~reddit-scraper-lite/run-sync-get-dataset-items?token=$APIFY_TOKEN
Content-Type: application/json
```

Input JSON template (batch of subreddits from ONE portfolio at a time, max 10 startUrls per run):
```json
{
  "startUrls": [
    { "url": "https://www.reddit.com/r/dataengineering/new/" },
    { "url": "https://www.reddit.com/r/MLOps/new/" }
  ],
  "maxItems": 100,
  "skipComments": true
}
```

Example invocation pattern (token comes from the environment, never inline):
```bash
source ~/.hermes/.env 2>/dev/null || true
curl -s -X POST \
  "https://api.apify.com/v2/acts/trudax~reddit-scraper-lite/run-sync-get-dataset-items?token=${APIFY_TOKEN}" \
  -H "Content-Type: application/json" \
  -d @input.json > results.json
```

Note: the actor's input schema may evolve. If the run returns a schema/validation error, fetch the actor's current input schema from the Apify Console output shown in the error, adjust field names minimally, and note the change in your summary so the skill file can be updated in git.

## Output Handling
From each returned item, extract and normalize these fields (field names in the raw output may vary slightly; map the closest match):
- `subreddit` (e.g., "dataengineering")
- `title`
- `body` (the post's selftext; may be empty for link posts)
- `url` (permalink to the thread)
- `created_at` (post timestamp)
- `upvotes` (score)
- `num_comments`
- `source` = always the literal string `"broad"`
- `portfolio` = A, B, or C (look it up from subreddits.json)
- `service_line` (look it up from subreddits.json)

Discard items that are: stickied/mod announcements, image/video-only posts with no text and no question in the title, or older than 48 hours.

## Test Mode
When asked to "test the reddit monitor", run ONE subreddit only (r/dataengineering), with maxItems 10, print a compact table of title / url / upvotes / num_comments for the returned posts, and report the total item count and approximate cost (items ÷ 1000 × $3.40).

## Full Scan Mode
When asked to "run the broad scan", process all subreddits from subreddits.json in three batches (one per portfolio: A, then B, then C), maxItems 100 per batch, then report per-portfolio counts. Store normalized results in a session file at ~/scan-output/broad-YYYY-MM-DD.json (create the directory if needed). Downstream skills (score-and-draft, sheets-writer) will consume that file.
