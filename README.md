# reddit-data-collector

A personal background script I threw together to continuously collect and store public Reddit post data across a large list of subreddits. Nothing fancy — just something I needed that I couldn't find a simple version of online.

## Background

I wanted to track how topics trend across different communities over time. Most existing tools were either too heavy, required accounts I didn't want to make, or were paywalled. So I just wrote my own. It's been running on my Linux box for a while now and does exactly what I need.

## What it does

- Continuously polls a rotating list of subreddits on a 5-minute cadence
- Grabs post titles, scores, upvote ratios, comment counts, and timestamps
- Tags each post with subreddit and collection timestamp
- Writes everything to a local SQLite database
- Completely read-only — no posting, no voting, no account interaction of any kind

## What it doesn't do

- Doesn't collect usernames or any personal data
- Doesn't store comments
- Doesn't upload or share data anywhere
- Doesn't touch private subreddits

## Requirements

- Python 3.10+
- `praw`
- `schedule`
- `sqlite3` (stdlib, no install needed)
- technology
programming
datascience
MachineLearning
artificial
worldnews
science
finance
stocks
cryptocurrency

Install dependencies:

```bash

                                                                                                                                                                                                                                                                                                                                                            The scraper shuffles through the list randomly each cycle to avoid hammering the same subreddits repeatedly. Runs at roughly 500 requests/min to keep up with 200+ subreddits and maintain data freshness.

## Database

Data is stored in `data.db` — a plain SQLite file. Schema is simple:

```sql
CREATE TABLE posts (
    id TEXT PRIMARY KEY,
    subreddit TEXT,
    title TEXT,
    score INTEGER,
    upvote_ratio REAL,
    num_comments INTEGER,
    created_utc INTEGER,
    collected_at INTEGER
);
```

You can query it with any SQLite tool. I use DB Browser for SQLite locally.

## Known issues / TODO

- No deduplication yet beyond the PRIMARY KEY constraint — if a post gets scraped twice it just fails silently which is fine for now
- Rate limiting is handled by praw but I want to add better logging around it
- Might add a simple Flask dashboard at some point to visualize trends, haven't gotten around to it

## License

MIT — do whatever you want with it                                                                      
