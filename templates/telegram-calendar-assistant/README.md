# Manage Google Calendar and Google Tasks from Telegram text or voice notes with a Gemini agent

## Description (n8n listing)

A personal assistant you can talk to from your phone. Send your Telegram bot a message or a voice note like "What's on tomorrow?", "Lunch with Priya Friday 1pm" or "Remind me to renew my passport by the 30th". Voice notes are transcribed by Gemini (no separate speech-to-text bill), and an AI Agent with Google Calendar and Google Tasks tools reads and updates your calendar and to-do list, then replies in plain language. It knows today's date in your timezone, remembers the last 10 messages so follow-ups work, asks when a request is ambiguous, and only answers the Telegram users you allow.

## Who it's for
- Anyone who lives in Google Calendar and wants a faster way to add things
- Freelancers and parents juggling appointments
- People who prefer voice notes to typing

## How it works
1. **Receive Telegram message** gets each message; **Is this an allowed user?** checks it against `allowed_user_ids`.
2. **Voice or text?** sends voice notes to **Download voice note** and **Transcribe voice note with Gemini**.
3. **Calendar and tasks assistant** (AI Agent + Gemini + Simple Memory) uses the tools Get calendar events, Create calendar event, Get open tasks, Create task and Complete task.
4. **Format reply** strips markdown, shows the transcript for voice notes and splits long replies; **Send reply on Telegram** answers.

## Setup
1. Create a bot with @BotFather and add a **Telegram** credential.
2. Add **Google Gemini (PaLM) API**, **Google Calendar OAuth2** and **Google Tasks OAuth2** credentials.
3. In **Set assistant settings** set `allowed_user_ids` (your numeric Telegram ID, from @userinfobot) and `timezone`.
4. Activate the workflow and message your bot.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Use another calendar by changing `primary` in the calendar tools.
- Change the default event length in **Set assistant settings**.
- Add more tools (Gmail, Google Sheets, Notion) to the agent.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/NT1kj
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
