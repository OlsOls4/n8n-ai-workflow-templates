# Triage new Gmail emails with AI labels and priority using Gemini

## Description (n8n listing)

Stop sorting your inbox by hand. Every minute this workflow picks up new unread emails, has Google Gemini read each one, and adds a category label (Needs reply, Action, FYI, Newsletter, Receipt, Promotion) plus a High priority label when it matters.

Quoted reply history is cut before the AI reads the email, so it judges only the new message, and a short description of your work (`my_context`) tells it what counts as important to you. Nothing is moved, archived or deleted: the workflow only adds labels, so it is safe to run on a real inbox from day one.

Gemini's free tier covers typical personal inbox volumes.

## Who it's for
- Freelancers, consultants and founders who live in Gmail
- Anyone who wants a filtered "Needs reply" view without writing Gmail filters
- Teams testing AI triage before rolling it out

## How it works
1. **Check Gmail for new emails** (Gmail Trigger, every minute, unread inbox, Simplify off for the full body).
2. **Set your labels and context** holds `label_prefix`, `my_context` and `max_body_chars`.
3. **Clean email text** (Code) keeps sender, subject and the new part of the body, and flags emails with an unsubscribe header (a strong newsletter signal).
4. **Classify email with AI** (Basic LLM Chain + Gemini 3.5 Flash-Lite + Structured Output Parser) returns `category`, `priority`, `summary` and `reason`. The prompt treats the email as data, so instructions hidden in emails are ignored.
5. **List Gmail labels** runs once per batch; **Match AI category to label IDs** turns label names into IDs and notes any missing labels.
6. **Keep emails with a matching label** then **Add labels in Gmail**.

## Setup
1. In Gmail create the labels `AI/Needs reply`, `AI/Action`, `AI/FYI`, `AI/Newsletter`, `AI/Receipt`, `AI/Promotion` and `AI/High priority` (Settings > Labels > Create new label; "AI/..." nests them under an AI folder).
2. Add a **Gmail OAuth2** credential to **Check Gmail for new emails**, **List Gmail labels** and **Add labels in Gmail**.
3. Get a free Gemini API key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential to **Gemini 3.5 Flash-Lite**.
4. Edit `my_context` in **Set your labels and context** (one or two sentences about your work and what matters).
5. Activate the workflow.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted
- A Gmail account and a Google Gemini API key (free tier)

## Customisation ideas
- Change the Gmail Trigger search (`in:inbox -category:social`) to include or skip folders and senders.
- Add categories: edit the prompt list and the `NAMES` map in **Match AI category to label IDs**, and create the matching labels.
- Add a Gmail "Mark as read" node after labelling for newsletters and promotions.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/dGXcm
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
