# Find buyer-intent Reddit posts with AI and send a daily Telegram digest

## Description (n8n listing)

People ask Reddit for tool recommendations every day. This workflow finds the posts where someone describes the problem your product solves, or asks for a tool like it, and sends you one Telegram digest each morning, ranked by buying intent.

It uses Reddit's public search RSS feeds (no API key, no Reddit app) with one search per keyword across all your subreddits at once. Google Gemini scores every new post from 1 to 10, labels the type of intent and names the pain point. Vendors promoting their own products are scored down. Posts already scored in earlier runs are skipped, and quiet days send nothing.

## Who it's for
- SaaS founders and indie hackers looking for early customers
- Marketers and community managers watching for buying signals
- Freelancers and agencies looking for people asking for help

## How it works
1. **Every day at 8am** (Schedule Trigger).
2. **Set keywords and subreddits**: product description, keywords, subreddits, `min_intent_score`, `lookback_hours`, `max_posts_to_score`, `telegram_chat_id`.
3. **Build Reddit search feeds** (Code) makes one feed per keyword: `reddit.com/r/a+b+c/search.rss?q="keyword"&restrict_sr=on&sort=new&t=day`.
4. **Read Reddit search feed** (RSS Read, continues on error).
5. **Clean and dedupe posts** (Code) keeps posts inside the lookback window, one per link, as plain text with the subreddit name. **Skip posts already seen** removes posts handled in earlier runs.
6. **Score buying intent with AI** (Gemini 3.5 Flash-Lite + Structured Output Parser): `intent_score`, `intent_type`, `pain_point`, `reason`.
7. **Attach score to post** → **Keep high-intent posts** → **Build daily digest** (highest first, split under Telegram's limit) → **Send digest to Telegram**.

## Setup
1. Fill in **Set keywords and subreddits**. Use phrases people actually write ("any tool for", "sick of chasing invoices") rather than your product category.
2. Add a **Google Gemini (PaLM) API** credential (free key at https://aistudio.google.com/app/apikey).
3. Create a bot with @BotFather, add a **Telegram API** credential, message the bot once and put your chat ID in `telegram_chat_id`.
4. Activate the workflow.

## Requirements
- n8n 2.x (built and import-tested on 2.43.7)
- A Google Gemini API key (free tier) and a Telegram bot

## Customisation ideas
- Lower `min_intent_score` to 5 to see more borderline posts while you tune keywords.
- Change the schedule to twice a day and `lookback_hours` to 12.
- Reddit rate-limits anonymous feeds: keep to roughly 10 keywords per run.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/PslpA
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
