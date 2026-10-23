# Track daily habits and mood with Telegram buttons, Google Sheets and a weekly Gemini review

## Description (n8n listing)

A habit tracker you never have to open. Every evening your Telegram bot asks how your day was (mood 1-5) and sends one message per habit with **Done** and **Not today** buttons. Each tap is saved to Google Sheets with a `date|habit` key, so pressing again just changes the answer, and the message updates to show what you picked. Send `/stats` any time for your last 7 days with completion rates and streaks. Every Sunday the workflow compares mood on days you did each habit with days you didn't, and Gemini writes a short, encouraging review with one small experiment for the week ahead. Add or pause habits by editing the sheet; no workflow changes needed.

## Who it's for
- Anyone building habits (reading, exercise, sleep, screen time)
- People who track mood alongside habits
- Coaches who want a simple client check-in

## How it works
1. **Every evening at 9pm** sends the mood question, reads `Habits` and sends one button message per active habit.
2. **Receive Telegram update** handles button presses and messages; **Parse the update** decodes them.
3. Answers are upserted into `Log`, acknowledged, and the message is edited to show the answer.
4. `/stats` runs **Calculate 7-day stats**; **Every Sunday at 7pm** runs the weekly stats and **Write the review**.

## Setup
1. Create a bot with @BotFather; add **Telegram**, **Google Sheets OAuth2** and **Google Gemini (PaLM) API** credentials.
2. Create `Habits` (`habit_id, habit, emoji, active, target_per_week`) and `Log` (`log_id, date, habit_id, value, logged_at`) tabs.
3. Put the Sheet ID and your chat ID in **Set tracker settings**, **Config** and **Config (Every Sunday at 7pm)** (n8n triggers run separately, so each has its own settings node).
4. Activate (button presses need the workflow active). Use a bot that no other workflow uses.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Change the check-in time or the review day.
- Edit the coach prompt for a different tone or language.
- Set `active` to `no` to pause a habit.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($15, extra features listed on the page): https://payhip.com/b/HCBcW
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
