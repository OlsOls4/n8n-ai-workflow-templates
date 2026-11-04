# Triage new Gmail emails with AI labels and priority using Gemini

## Description (n8n listing)

Stop sorting your inbox by hand. Every minute this workflow picks up new unread emails (not from you), has Google Gemini read each one, and adds a category label (Needs reply, Action, FYI, Newsletter, Receipt, Promotion) plus a High priority label when it matters.

It goes further than labelling: VIP senders and urgent keywords from your settings always rank high, newsletters and promotions can be archived out of the inbox (never deleted), every email is logged to a Google Sheet, urgent emails trigger an alert email to you, and at 8am you get a digest of the last 24 hours. Quoted reply history is cut before the AI reads each message, and a short description of your work (`my_context`) tells it what counts as important to you.

Gemini's free tier covers typical personal inbox volumes.

## Who it's for
- Freelancers, consultants and founders who live in Gmail
- Anyone who wants a filtered "Needs reply" view without writing Gmail filters
- Teams testing AI triage before rolling it out

## How it works
1. **Check Gmail for new emails** (Gmail Trigger, every minute, unread inbox, `-from:me` so alerts never loop, Simplify off for the full body).
2. **Set your labels and context** holds `label_prefix`, `my_context`, `vip_senders`, `urgent_keywords`, `archive_categories`, `alert_email` and `max_body_chars`.
3. **Clean email text and flag VIPs** (Code) keeps sender, subject and the new part of the body, flags unsubscribe headers, VIP senders (addresses or @domains) and urgent keywords.
4. **Classify email with AI** (Basic LLM Chain + Gemini 3.5 Flash-Lite + Structured Output Parser) returns `category`, `priority`, `needs_reply`, `summary` and `reason`. The email is treated as data, so instructions hidden in emails are ignored.
5. **List Gmail labels** and **Match AI category to label IDs** turn label names into IDs, force VIPs and keyword hits to high priority and decide which emails to archive or alert on.
6. Three branches: labels are added (**Add labels in Gmail**), low-value categories are removed from the inbox (**Archive email**), every email is logged (**Log email to Google Sheets**) and urgent ones send **Email me an urgent alert**.
7. A second lane runs at 8am: **Read the email log**, **Build the digest**, **Email me the digest**.

## Setup
1. In Gmail create the labels `AI/Needs reply`, `AI/Action`, `AI/FYI`, `AI/Newsletter`, `AI/Receipt`, `AI/Promotion` and `AI/High priority` (Settings > Labels > Create new label; "AI/..." nests them under an AI folder).
2. Create a Google Sheet with a tab named `Log` and this header row: logged_at, from, subject, category, priority, summary, archived, why_high, gmail_link. Put the sheet ID in **Log email to Google Sheets** and **Read the email log**.
3. Add credentials: **Gmail OAuth2** (trigger and all Gmail nodes), **Google Sheets OAuth2**, and **Google Gemini (PaLM) API** (free key at https://aistudio.google.com/app/apikey).
4. In **Set your labels and context** fill in `my_context`, `vip_senders`, `urgent_keywords`, `archive_categories` (leave empty to never archive) and `alert_email`. Use the same address in **Set digest settings**.
5. Activate the workflow.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted
- A Gmail account, a Google Sheet and a Google Gemini API key (free tier)

## Customisation ideas
- Change the Gmail Trigger search (`in:inbox -category:social`) to include or skip folders and senders.
- Add categories: edit the prompt list and the `NAMES` map in **Match AI category to label IDs**, and create the matching labels.
- Add a Gmail "Mark as read" node after the archive step.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/dGXcm
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
