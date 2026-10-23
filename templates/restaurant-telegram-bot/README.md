# Answer restaurant FAQs and menu questions with an AI Telegram bot and Google Sheets

## Description (n8n listing)

Give your restaurant or café a Telegram assistant that answers the questions staff hear all day: opening hours, parking, vegan options, what's in a dish, which allergens it contains. The bot answers only from a Google Sheet you control, so updating the menu or your hours is as easy as editing a cell.

Allergen guardrails are built into the prompt: the bot repeats only the allergens you list, never calls a dish "safe", always asks customers to tell staff about allergies, and gives your phone number when it doesn't know. Booking requests get your booking details. Messages trying to make the bot go off-topic are ignored.

Telegram and Gemini's free tier cost nothing to run for a typical venue.

## Who it's for
- Independent restaurants, cafés, bars and food trucks
- Agencies and freelancers building chatbots for hospitality clients
- Anyone who wants a no-code FAQ bot backed by a spreadsheet

## How it works
1. **Receive Telegram message** (Telegram Trigger). **Is it a text message?** routes photos and stickers to **Ask for a text question**.
2. **Set restaurant details** holds the name, phone number and booking info.
3. **Read menu and FAQ sheet** reads the `Knowledge` tab on every message, so edits are live immediately.
4. **Build knowledge base** (Code) turns rows into a compact menu (price, allergens, dietary tags) plus an information list.
5. **Answer question with AI** (Basic LLM Chain + Gemini 3.5 Flash-Lite) answers in the customer's language, under 100 words.
6. **Send answer on Telegram**.

## Setup
1. Create a bot with **@BotFather** (`/newbot`), copy the token and add a **Telegram API** credential on the trigger and both Telegram nodes.
2. Create a Google Sheet with a tab named `Knowledge` and the header row `type | name | details | price | allergens | dietary`.
   - Dishes: `menu | Lasagne al forno | Beef ragu, bechamel | £15.50 | gluten, milk, egg, celery |`
   - Everything else: `info | Opening hours | Tue-Sun 12:00-22:30, closed Mondays | | |`
3. Put the Sheet ID in **Set restaurant details** (the long ID in the sheet URL) and add a **Google Sheets** credential.
4. Add a **Google Gemini (PaLM) API** credential (free key at https://aistudio.google.com/app/apikey).
5. Fill in **Set restaurant details** (replace the YOUR_... placeholders) and activate.

## Requirements
- n8n 2.x (built and import-tested on 2.43.7). Telegram triggers need a public HTTPS URL (n8n cloud, or self-hosted with a tunnel or domain).
- Google Sheets and a Google Gemini API key (free tier)

## Customisation ideas
- Change tone or length in **Answer question with AI** (e.g. "playful, use one emoji").
- Add rows of type `info` for private hire, gift cards, dress code or delivery areas.
- Swap the Telegram nodes for WhatsApp Business Cloud nodes once you have Meta access.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/XmRis
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
