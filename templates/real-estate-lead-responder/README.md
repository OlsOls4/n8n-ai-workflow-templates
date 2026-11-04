# Qualify real estate leads from portal emails and web forms with Gemini, Gmail drafts and Google Sheets

## Description (n8n listing)

Property leads go cold fast, and portal e-mails are a pain to copy into a CRM. This template watches Gmail for enquiry e-mails from Rightmove, Zoopla, OnTheMarket, Zillow, Realtor.com, Homes.com, Trulia, Redfin and OpenRent (or anything with a `leads` label). It also gives you a webhook for your own website form. Code parsers pull out the name, e-mail, phone, message, property reference and enquiry type. Gemini then reads the enquiry like an experienced negotiator: intent (buy, rent, valuation), budget, timeline, mortgage approval in principle or pre-approval, and buying position. It writes a warm, specific first reply that only uses facts from the enquiry. Simple rules turn the AI read-out into a 0-100 score. The lead goes into a Google Sheets CRM, the reply waits as a Gmail draft, and hot leads are e-mailed to you straight away.

## Who it's for
- Estate and letting agents (UK)
- Realtors and real estate teams (US)
- Property VAs and lead managers

## How it works
1. **New portal or enquiry e-mail** (Gmail, every minute) and **Website enquiry form** (webhook) receive leads.
2. **Read the portal e-mail** / **Read the web form** extract the lead fields.
3. **Qualify and draft the reply** (Gemini + Structured Output Parser) returns intent, budget, timeline, pre-approval, position, an AI score and the reply.
4. **Score the lead** applies rules (pre-approved, moving within 3 months, phone given, valuation request) for a final score and temperature.
5. **Add lead to Google Sheets**, **Create reply draft in Gmail** and, for hot leads, **Email me the hot lead**.

## Setup
1. Add **Gmail OAuth2**, **Google Sheets OAuth2** and **Google Gemini (PaLM) API** credentials.
2. Create a `Leads` tab with the columns below.
3. Fill in **Set responder settings** (agency, agent, signature, booking link, Sheet ID, your e-mail).
4. Edit the Gmail search in **New portal or enquiry e-mail** to match your portals, send your website form to the webhook's Production URL, and activate.

### Google Sheet tabs
- `Leads`: `lead_id, created_at, updated_at, source, name, email, phone, enquiry_type, intent, property, budget, timeline, pre_approved, position, score, temperature, score_reasons, summary, missing_info, stage, status, reply_status, followups_sent, next_followup, last_contact, enquiries, message, reply_subject, reply_body, last_followup, replied_at`

### Settings
| Node | Setting | Default | What it does |
|---|---|---|---|
| **Set responder settings** | `agency_name` | `Your Agency` | Your agency or brokerage name. |
| **Set responder settings** | `agent_name` | `Alex` | The person replies come from. |
| **Set responder settings** | `agent_phone` | `01234 567890` | Phone number the AI may give to leads. |
| **Set responder settings** | `signature` | `Best wishes, / Alex / Your Agency \| 01234 567890` | Exact sign-off appended to every reply. |
| **Set responder settings** | `booking_link` | `https://calendly.com/your-agency/viewing` | Viewing / valuation booking link (Calendly, Cal.com, your CRM). Leave blank to ask for times instead. |
| **Set responder settings** | `office_hours` | `Mon-Fri 9:00-17:30, Sat 9:00-13:00` | Shown to the AI so it doesn't promise out-of-hours calls. |
| **Set responder settings** | `market` | `UK` | UK or US (affects terms such as approval in principle vs pre-approval). |
| **Set responder settings** | `language` | `British English` | Language and spelling for everything the AI writes. |
| **Set responder settings** | `hot_score` | `70` | Final score (0-100) from which a lead is hot and triggers an alert. |
| **Set responder settings** | `notify_email` | YOUR_EMAIL (replace) | Where summary and notification e-mails go. |
| **Set responder settings** | `sheet_id` | YOUR_SHEET_ID (replace) | The ID from your Google Sheet URL: docs.google.com/spreadsheets/d/<ID>/edit |

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key. The free tier at https://aistudio.google.com/app/apikey is enough for normal volumes.

## Customisation ideas
- Add your own portal's sender domain to the Gmail search.
- Change the scoring rules in **Score the lead**.
- Translate the prompt for another market or language.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/Qmd4U
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
