# Score remote job listings against your CV with AI and alert on Telegram

## Description (n8n listing)

Let AI read the job boards for you. Twice a day this workflow collects new remote jobs from three free sources (the Remotive API, the Remote OK API and the We Work Remotely RSS feed), keeps the ones whose title or tags mention your keywords, and asks Google Gemini to score each against your CV from 0 to 100.

Only jobs at or above your threshold reach you on Telegram, each with the score, a one-line verdict, the skills you match, the gaps to address and a link to the original listing. Location and time-zone limits count against the score, so "US only" roles don't waste your time. Every job is scored once: listings seen in earlier runs are skipped, which also keeps AI usage low.

The sources need no API keys, and Gemini's free tier covers typical use. An optional Google Sheets node (disabled by default) can log every match for tracking applications. Alerts credit the source and link to its listing, as the Remotive and Remote OK API terms require.

## Who it's for
- Job seekers looking for remote roles who are tired of checking several boards
- Freelancers and contractors watching for specific skills
- Career coaches running searches for clients

## How it works
1. **Twice a day (9am and 5pm)** (Schedule Trigger). Remotive asks API users to call at most 4 times a day.
2. **Set your CV and preferences** holds `cv_text`, `keywords`, `min_score`, `max_age_days`, `max_jobs_per_run` and `telegram_chat_id`.
3. **Fetch Remotive jobs**, **Fetch Remote OK jobs** (HTTP Request) and **Fetch We Work Remotely jobs** (RSS Read) run in parallel. Each continues on error, so one outage doesn't stop the run.
4. **Wait for all sources** (Merge) lets all three finish.
5. **Normalize and filter jobs** (Code) maps the three formats to one shape (title, company, URL, location, salary, tags, date, plain-text description), keeps jobs newer than `max_age_days` whose title or tags match a keyword, sorts newest first and caps at `max_jobs_per_run`.
6. **Skip jobs already scored** (Remove Duplicates across executions, keyed on the job URL).
7. **Score job against CV** (Basic LLM Chain + Gemini 3.5 Flash-Lite + Structured Output Parser) returns `score`, `verdict`, `matching_skills`, `missing_skills` and `location_ok`. Batching keeps you inside free-tier rate limits.
8. **Attach score to job** merges the score with the job details; **Keep good matches** applies `min_score`.
9. **Send job alert to Telegram**, and optionally **Log match to Google Sheets**.

## Setup
1. Open **Set your CV and preferences**. Replace the sample `cv_text` with your CV and what you want (role, seniority, time zones, salary). Edit `keywords` (comma-separated) and `min_score`.
2. Get a free Gemini API key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential on **Gemini 3.5 Flash-Lite**.
3. Create a Telegram bot with **@BotFather**, add a **Telegram API** credential on **Send job alert to Telegram**, message your bot once and put your chat ID in `telegram_chat_id`.
4. Optional: create a Google Sheet with a `Matches` tab and the header row `score | verdict | matching_skills | missing_skills | location_ok | title | company | location | salary | source | url | found_at`, put the Sheet ID in **Set your CV and preferences**, add a Google Sheets credential and enable the node.
5. Activate the workflow.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted.
- A Google Gemini API key (free tier)
- A Telegram bot (free)
- Optional: Google Sheets

## Customisation ideas
- Add more feeds (for example a We Work Remotely category feed or another job board's RSS) as extra Merge inputs and map them in the Code node.
- Make the prompt stricter about salary floor, visa sponsorship or contract type.
- Ask the model for a two-sentence cover letter opener and include it in the alert.
- Lower `min_score` at first to calibrate, then raise it once you trust the scores.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- Free version on n8n.io: https://n8n.io/workflows/21457
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
