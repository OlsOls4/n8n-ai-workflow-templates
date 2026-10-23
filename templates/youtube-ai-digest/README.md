# Summarize new YouTube videos from channel RSS feeds with AI and send to Telegram

## Description (n8n listing)

Follow more YouTube channels without drowning in notifications. Every morning this workflow checks the channels you choose, finds the videos published since the last run and sends you one Telegram digest with a short AI summary and a link for each.

It uses YouTube's free public RSS feeds, so there is no YouTube API key, quota or Google Cloud project to set up. Google Gemini writes a one-sentence summary and a "worth watching if" line from each video's title and description, ignoring sponsor plugs and link lists. Videos already sent are remembered, so you never see the same one twice, and a mistyped channel ID is skipped rather than breaking the run.

Long digests are split automatically to stay under Telegram's message limit. Everything runs on free tiers: Gemini's free API and a Telegram bot.

## Who it's for
- Developers, researchers and creators who follow many channels and want a quick daily scan
- Teams who want a shared channel digest in a Telegram group
- Anyone learning how to combine RSS, deduplication and AI summaries in n8n

## How it works
1. **Every morning at 8am** (Schedule Trigger) starts the run.
2. **Set channels and settings** holds `channel_ids` (a list), `lookback_hours` and `telegram_chat_id`.
3. **One item per channel** (Split Out) turns the list into one item per channel.
4. **Read channel RSS feed** (RSS Read) loads `https://www.youtube.com/feeds/videos.xml?channel_id=...` for each channel, with the `media:group` field so the video description is included. Errors continue instead of stopping the workflow.
5. **Keep videos from lookback window** (Filter) keeps videos published in the last `lookback_hours`.
6. **Skip videos already sent** (Remove Duplicates, "items seen in previous executions") drops anything already summarised.
7. **Summarize video with AI** (Basic LLM Chain + Gemini 3.5 Flash-Lite) writes the two-line summary. Batching keeps you inside Gemini's free-tier rate limits.
8. **Build digest message** (Code) assembles an HTML-formatted digest and splits it under 4,096 characters.
9. **Send digest to Telegram** posts it.

## Setup
1. Get a free Gemini API key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential on **Gemini 3.5 Flash-Lite**.
2. Create a bot with **@BotFather** in Telegram, add a **Telegram API** credential on **Send digest to Telegram**, then send your bot any message.
3. Find your chat ID (for example, open `https://api.telegram.org/bot<token>/getUpdates` after messaging the bot) and put it in `telegram_chat_id`.
4. Replace the two example channel IDs in `channel_ids` with your own. On a channel page choose *About > Share channel > Copy channel ID*; IDs start with `UC`.
5. Activate the workflow. The first run sends videos from the last 24 hours.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted.
- A Google Gemini API key (free tier)
- A Telegram bot (free)

## Customisation ideas
- Weekly digest: run the trigger weekly and set `lookback_hours` to 168.
- Send to a Telegram group or channel by using its chat ID (add the bot to it first).
- Swap the model for Groq, OpenAI, Anthropic or a local Ollama model by replacing the chat model sub-node.
- Change the prompt to summarise in another language or to output bullet points.
- Skip YouTube Shorts by adding a condition to the Filter on the title or link.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- Free version on n8n.io: https://n8n.io/workflows/21170
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
