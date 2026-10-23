# Track calories from Telegram meal photos and text with Gemini, daily targets and Google Sheets


## Description (n8n listing)

This is a Telegram food diary that does the maths for you. Send your bot a photo of a meal, or type what you ate ("2 eggs on toast and a flat white"), and Google Gemini estimates the dish, portion, calories, protein, carbs and fat. Every meal goes into Google Sheets.

After each meal the bot replies with what is left of your daily targets. Set your targets once with `/goal 2000 150 200 70`.

Commands:
- `/fix half portion` re-estimates your last meal and updates its row in place.
- `/undo` removes your last meal.
- `/today` shows today's totals against your targets.
- `/week` shows a 7-day table with your average, the number of days logged, your protein average and the trend against the week before.

Every evening at 9pm, everyone who has set targets gets a summary of the day plus one practical tip from Gemini.

Photos that are not food are rejected instead of being logged. Several people can share one bot, because every row and target is keyed to the sender's Telegram user ID. It runs on Gemini's free API tier. The estimates are approximate and meant for everyday tracking, not medical use.

## Who it's for
- People tracking calories or macros who find logging apps tedious
- Couples, families or small groups who want one shared bot
- Coaches who want clients to log meals in a familiar chat app

## How it works
1. **Parse message** turns every Telegram message into one of: photo, text meal, or a command (`/goal`, `/today`, `/week`, `/fix`, `/undo`, `/help`). Dates and times use the workflow's timezone.
2. **Route by message type** (Switch) sends each kind down its own branch.
3. Photos are downloaded and handled by **Estimate meal from photo** (Gemini Vision). Text meals and `/fix` corrections are handled by **Estimate meal from text**. Both use the same structured JSON schema.
4. **Is it food?** drops anything that is not food.
5. **Prepare log row** builds the row. A correction keeps the original `meal_id`, date and time.
6. New meals are appended. Corrections update the existing row matched on `meal_id`.
7. `/undo` and `/fix` first run **Find my last meal**. If you have nothing logged yet, the bot says so.
8. `/goal` upserts your targets in the `Targets` tab, matched on `user_id`.
9. After every action, **Read my meals** and **Read my targets** feed **Build progress reply**. That node shows what was logged or changed, then today against your targets (left or over), or the 7-day view for `/week`.
10. **Every evening at 9pm** reads all targets and meals and builds one summary per user. Users with `evening_summary` set to `no` are skipped. **Write coaching tip** adds a 30-word tip, then the summary goes to each user.

## Setup
1. Create a bot with **@BotFather** and add a **Telegram API** credential.
2. Get a free Gemini key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential to the three Gemini model nodes.
3. Create a Google Sheet with two tabs:
   - `Meals`: `meal_id | date | time | user_id | user_name | dish | portion | calories_kcal | protein_g | carbs_g | fat_g | confidence | source | status | notes`
   - `Targets`: `user_id | chat_id | user_name | kcal | protein_g | carbs_g | fat_g | evening_summary`
4. Put the Sheet ID in **Config** and **Config (Every evening at 9pm)** and add a **Google Sheets OAuth2** credential.
5. In **Workflow settings**, set the timezone to yours so that "today" resets at your midnight.
6. Activate the workflow and send `/goal 2000 150 200 70` to your bot (kcal, then protein, carbs and fat in grams; the macros are optional). Then send a meal photo.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted. The Telegram Trigger needs a public HTTPS URL when self-hosting.
- A Telegram bot (free)
- A Google Gemini API key (the free tier is enough for personal use)
- A Google account with Google Sheets

## Customisation ideas
- Change the evening summary time in **Every evening at 9pm**.
- Track fibre or sugar by adding them to the two JSON examples, **Prepare log row** and the sheet header.
- Restrict the bot to known users with the trigger's *Restrict to Chat IDs* option.
- Edit the tone of the evening tip in **Write coaching tip**.

## Tested
- Tested on n8n 2.43.7 with 10 fixture variants: photo, non-food photo, text meal, `/fix`, `/undo`, `/week`, `/goal`, invalid `/goal`, `/start`, and the evening summary.
- A Groq model stood in for Gemini. Telegram and Sheets were replaced by fixtures.
- All 10 variants passed.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
