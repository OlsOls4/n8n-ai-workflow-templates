# Write personalised cold email opening lines for Google Sheets leads with AI

## Description (n8n listing)

The first line decides whether a cold email gets read. This workflow takes the leads in your Google Sheet and writes one specific, non-cheesy opening line per lead with Google Gemini, using only the facts you already have: company, role, website and your research notes.

Each line comes with what it was based on and a confidence rating, so you can spot the generic ones at a glance. The prompt bans the usual clichés ("I came across your profile", "I hope this email finds you well") and never invents facts. Results are written back to the same row, and each lead is processed once.

## Who it's for
- Freelancers, agencies and SDRs doing personalised outbound
- Founders writing their own cold emails who want a strong first line fast
- Anyone with a lead list and a few notes per lead

## How it works
1. **Start manually** (click Execute workflow after adding leads).
2. **Set your offer** holds `what_you_sell` (so the line leads naturally into your pitch) and `max_leads_per_run`.
3. **Read leads from Google Sheets** → **Keep new leads** (has an email, empty `status`) → **Limit leads per run**.
4. **Write opening line with AI** (Basic LLM Chain + Gemini 3.5 Flash-Lite + Structured Output Parser) returns `first_line`, `based_on` and `confidence`.
5. **Save opening line to Google Sheets** updates the row (matched on `email`) with the line, its basis and `status = first line written`.

## Setup
1. Create a Google Sheet with a tab `Leads` and the columns `first_name | last_name | email | company | role | website | notes | first_line | first_line_basis | status`.
2. Put what you know in `notes`: a recent post, a funding round, a new location, a hire, something from their website. More specific notes give better lines.
3. Put the Sheet ID in **Set your offer** and add a **Google Sheets** credential.
4. Add a **Google Gemini (PaLM) API** credential (free key at https://aistudio.google.com/app/apikey).
5. Describe your offer in **Set your offer** and click **Execute workflow**.

## Requirements
- n8n 2.x (built and import-tested on 2.43.7)
- Google Sheets and a Google Gemini API key (free tier)

## Customisation ideas
- Swap **Start manually** for a Schedule Trigger to process new leads every morning.
- Clear a lead's `status` to regenerate its line.
- Change the rules in the prompt for a different length, language or tone.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/ievgI
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
