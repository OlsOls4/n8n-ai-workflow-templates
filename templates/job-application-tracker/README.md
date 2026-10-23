# Track job application emails from Gmail in Google Sheets with AI status detection

## Description (n8n listing)

After twenty applications nobody remembers who replied. This template watches your Gmail every hour, lets Google Gemini decide whether each email is about one of your own job applications, and extracts the company, role, status (applied, assessment, interview, offer, rejected, recruiter outreach), next step and any deadline.

Each application is upserted by company + role, so the confirmation, the interview invite and the eventual offer all update the same row instead of piling up. Job alerts, newsletters and marketing mail are ignored. It uses only Gmail, Google Sheets and Gemini's free tier.

## Who it's for
- Job seekers sending lots of applications
- Career changers and graduates who want a simple pipeline view
- Career coaches setting this up for clients

## How it works
1. **Check Gmail for application emails** (Gmail Trigger, hourly) uses a search that skips promotions and social tabs and looks for application words.
2. **Prepare email for AI** keeps the sender, subject, date and first 3,000 characters.
3. **Detect company, role and status** (Basic LLM Chain + Gemini + Structured Output Parser) returns `is_job_application`, company, role, status, next step, deadline and confidence.
4. **Keep job application emails** drops everything else.
5. **Prepare application row** builds a stable key from company + role and a Gmail link; **Update application in Google Sheets** appends or updates the row.

## Setup
1. Add a **Gmail OAuth2** credential to the trigger and a free **Google Gemini (PaLM) API** credential to the chat model.
2. Create a Google Sheet with an `Applications` tab and this header row:
   `application_key | company | role | status | next_step | deadline | last_update | last_subject | from | gmail_link`
3. Put the Sheet ID in **Config** and connect **Google Sheets OAuth2**.
4. Activate. The trigger only picks up emails that arrive after activation.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Gmail account and Google Sheets
- Set your timezone in **Workflow settings** so dates and schedules match your day.

## Customisation ideas
- Edit the trigger's search to add your own keywords or a Gmail label.
- Add statuses such as `withdrawn` or `ghosted` to the prompt.
- Add conditional formatting on `status` for a colour-coded board.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($15, extra features listed on the page): https://payhip.com/b/d0Ihr
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
