# Analyse stock charts on Telegram with RSI, MACD and moving averages explained by Gemini

## Description (n8n listing)

A Telegram bot that answers `/ta AAPL` (or `$TSLA`, `BTC`, `VOD.L`, `^GSPC`) with a clean price chart and a plain-English read of the technicals. RSI(14), MACD(12/26/9) and the 20/50/200-day moving averages are **calculated in a Code node from real daily prices**, so Gemini explains numbers instead of guessing from a picture. Prices come from Yahoo Finance's public chart endpoint and the chart from QuickChart, so there is no paid chart or data API. Bad tickers get a helpful reply instead of an error, and every message carries a not-financial-advice note.

## Who it's for
- Retail investors who want a quick, honest read of a chart
- Finance educators and trading communities on Telegram
- Developers who want a clean starting point for a market bot

## How it works
1. **Receive Telegram message** reads `/ta TICKER`, `$TICKER` or a bare ticker; `/start` shows help.
2. **Get daily prices from Yahoo** fetches two years of daily candles (retries on failure).
3. **Compute indicators** works out RSI, MACD, SMA/EMA, trend and a technical-bias score, and builds the chart config.
4. **Draw chart with QuickChart** renders a PNG; **Explain the chart in plain English** (Gemini + structured output) writes the summary.
5. The chart and the full analysis are sent back to the chat.

## Setup
1. Create a bot with @BotFather and add a **Telegram** credential.
2. Add a free **Google Gemini (PaLM) API** credential.
3. Optionally change `default_range` in **Set bot settings**.
4. Activate the workflow and send `/start` to your bot.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key: the free tier at https://aistudio.google.com/app/apikey is enough for normal use. Any other chat model node (OpenAI, Anthropic, Groq, Ollama) can replace the Gemini node.

## Customisation ideas
- Add your own indicator to the Code node; it is plain JavaScript with helper functions for SMA, EMA and RSI.
- Change the ticker shortcuts (BTC, SPX, GOLD...) at the top of **Read the ticker**.
- Swap Gemini for any chat model node.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/fhSzZ
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
