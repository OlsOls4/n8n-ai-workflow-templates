# Onboard new clients with Google Drive folders, a Sheets CRM row, a welcome email and an AI intake summary

## Description (n8n listing)

Every new client gets the same professional start without the copy-paste. Fill in one form when a client signs: the workflow checks for missing details and existing clients, creates a Google Drive folder with your standard subfolders, adds the client to a Google Sheets client list and sends a welcome e-mail with their shared folder and an intake form. When the client submits the intake form, Gemini summarises their goals, gaps and kickoff questions, the CRM row is updated and you get the summary by e-mail.

## Who it's for
- Marketing, design and web agencies
- Consultants, coaches and freelancers
- Bookkeepers and accountants taking on new clients

## How it works
1. **New client form** collects contact, company, e-mail, package, start date, value and notes.
2. **Check details and duplicates** stops on a missing e-mail/name or an e-mail that is already a client, and tells you why.
3. **Create client folder** makes `Company (yyyy-MM)` in your clients folder, then one subfolder per entry in `subfolders`.
4. The client is appended to `Clients` and **Send welcome e-mail** sends the intake form link and shared folder.
5. **Client intake form** (pre-filled with the client ID from the e-mail link) is summarised by **Summarise intake with AI**; the CRM row is updated and the team gets the summary.

## Setup
1. Connect **Google Drive**, **Google Sheets**, **Gmail** and **Google Gemini (PaLM) API**.
2. Create a Google Sheet with this tab:
   - `Clients`: `client_id | created | company | contact_name | email | phone | package | value | start_date | account_manager | folder_id | folder_url | assets_url | intake_url | token | stage | intake_status | intake_received | intake_summary | reminders | last_reminder | kickoff | notes`
3. Create a parent folder for clients in Drive and copy its ID.
4. Fill in **Set onboarding settings** (sheet ID, parent folder ID, subfolders, `n8n_base_url` such as `https://n8n.yourcompany.com`, agency and your name, your e-mail) and **Set intake settings**.
5. Put your e-mail in **Email the error** and pick this workflow under **Workflow settings > Error workflow**.
6. Activate, then open the production URL of **New client form**.

## Requirements
- n8n 2.x, cloud or self-hosted (built and import-tested on n8n 2.43.7). Built-in nodes only, no community nodes.
- A Google account (Gmail / Google Workspace). Google credentials in n8n: https://docs.n8n.io/integrations/builtin/credentials/google/
- A Google Gemini API key (the free tier from https://aistudio.google.com/app/apikey is enough for normal volumes).

## Customisation
- Change the subfolder list in `subfolders` (comma-separated). The one containing `assets_folder_keyword` is linked in the welcome e-mail.
- Rewrite the welcome e-mail in **Write welcome e-mail**: it is plain HTML.
- Add or remove intake questions in **Client intake form** and the labels list in **Prepare intake answers**.

## Troubleshooting
- **Intake form says the client wasn't matched**: the form was opened without `?client_id=` (not from the e-mail link). The summary still reaches you, flagged.
- **Folder errors**: the parent folder ID must be a folder the connected Google account can edit.
- **Intake link broken**: `n8n_base_url` must be your public n8n address without a trailing `/webhook`; the workflow must be active.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/NPqj7
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
