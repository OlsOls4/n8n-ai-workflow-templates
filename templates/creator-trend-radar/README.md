# Find trending video ideas for your niche from Google Trends and YouTube with Gemini and Telegram

## Description (n8n listing)

Trends are only useful if they fit your channel. Each morning this workflow reads Google Trends' daily trending searches for your country and the newest uploads from channels you choose, both via free public RSS feeds, and asks Gemini to pick only the ideas that genuinely fit your niche and audience. Each idea comes with a specific title, a hook, a format (short or long), your angle, why it is timely, its source signal and a relevance score. Ideas below your bar are dropped, ideas suggested on earlier days are skipped, and the rest are logged to Google Sheets and sent as one Telegram digest.

## Who it's for
- YouTubers and TikTokers who want timely topics
- Newsletter writers and podcasters looking for hooks
- Social media managers planning content

## How it works
1. **Set radar settings** holds niche, audience, country, watched channel IDs, lookback window, relevance bar and Telegram chat.
2. **Read Google Trends daily feed** and **Read competitor uploads** run in parallel; failures are skipped.
3. **Collect signals** builds prompt text; **Pick video ideas** returns structured ideas; **Rank ideas** keeps and sorts the best.
4. **Skip ideas already suggested** removes repeats across days, then ideas are logged and sent.

## Setup
1. Add **Google Gemini (PaLM) API**, **Google Sheets** and **Telegram** credentials.
2. Create an `Ideas` tab: `idea_id, found_on, topic, hook, format, angle, why_now, source, relevance, urgency, audience, status`.
3. Put the Sheet ID in **Set radar settings** and fill in **Set radar settings** (channel IDs start with `UC`).
4. Activate.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Change `geo` (GB, US, DE...) or run it twice a day.
- Raise `min_relevance` for fewer, sharper ideas.
- Add more RSS feeds (blogs, news) into **Wait for both sources**.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/DPNyW
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
