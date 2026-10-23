# Send birthday reminders with Gemini gift ideas and message drafts from Google Sheets to Telegram

## Description (n8n listing)

Never miss a birthday or panic-buy a gift again. List the people you care about in a Google Sheet with their birthday, interests, budget and what you gave last time. Every morning the workflow works out who has a birthday coming up (it understands `1990-05-17`, `17/05/1990`, `17/05` and `05-17`, and handles 29 February), and at your chosen lead days (14, 3 and 0 by default) it sends Telegram reminders. Before the day, Gemini suggests five gifts within budget, mixing experiences and practical items and never repeating a past gift, each with a shopping search link and a card line. On the day it drafts a 2-4 sentence message and a quick one-liner in your style. Reminders are never sent twice.

## Who it's for
- Anyone who forgets birthdays (no judgement)
- Busy parents and people with big families
- Friends who want gifts that feel personal

## How it works
1. **Every morning at 8am** reads the `People` tab.
2. **Find upcoming birthdays** parses dates, finds the next birthday and age, and keeps people at a lead day.
3. **Skip reminders already sent** prevents duplicates; **Gift reminder or birthday today?** routes each person.
4. **Suggest gift ideas** and **Format gift message** send five ideas with search links; **Draft birthday message** writes the day-of message.

## Setup
1. Add **Google Sheets OAuth2**, **Telegram** and **Google Gemini (PaLM) API** credentials.
2. Create a `People` tab: `name, relationship, birthday, interests, budget, notes, last_gift` (optional `occasion`), and put the Sheet ID in **Set reminder settings**.
3. Fill in **Set reminder settings** (Telegram chat ID, your name, message style, lead days, default budget).
4. Activate.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Use any lead days, e.g. `30,7,1,0`.
- Add an `occasion` column for anniversaries.
- Change the message style or language.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($12, extra features listed on the page): https://payhip.com/b/XnpvB
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
