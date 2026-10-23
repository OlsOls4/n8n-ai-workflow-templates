# Send a weekly Google Analytics 4 report with AI insights via Gmail

## Description (n8n listing)

Opening Google Analytics every week to work out whether things got better is a chore. This template pulls last week's and the previous week's GA4 data with the built-in Google Analytics node (users, new users, sessions, page views, engaged sessions, key events, top pages and traffic sources), calculates week-over-week changes in a Code node, and asks Google Gemini for a short plain-English commentary: a headline, three wins, up to three concerns and three next actions.

The numbers in the table come straight from GA4; the AI only writes the words around them and is told not to invent causes. The report arrives in your inbox every Monday at 8am as a clean HTML email with green and red arrows.

## Who it's for
- Small-business owners who want one weekly email instead of dashboards
- Freelance marketers and web designers reporting to a client
- Founders tracking a marketing site

## How it works
1. **Every Monday at 8am** starts the run; **Set report settings** holds the GA4 property ID, site name, recipient and brand colour.
2. **Get this week's traffic** and **Get last week's traffic** fetch daily metrics for the two 7-day windows; **Get top pages** and **Get top traffic sources** fetch the top 10 of each.
3. **Calculate week-over-week changes** totals each metric and computes percentage changes and engagement rate.
4. **Write insights with AI** (Basic LLM Chain + Gemini + Structured Output Parser) returns headline, wins, concerns and actions.
5. **Build report email** renders the HTML and **Send report via Gmail** sends it.

## Setup
1. In Google Cloud, enable the **Google Analytics Data API**, then add a **Google Analytics OAuth2** credential in n8n and select it on the four GA4 nodes.
2. Add a free **Google Gemini (PaLM) API** credential and a **Gmail OAuth2** credential.
3. In **Set report settings** replace `YOUR_GA4_PROPERTY_ID` (GA4 Admin > Property details, numbers only), the site name and `YOUR_EMAIL_ADDRESS`.
4. Run once manually to check the email, then activate.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A GA4 property you can read, Google Cloud project with the Analytics Data API enabled, and Gmail
- Set your timezone in **Workflow settings** so dates and schedules match your day.

## Customisation ideas
- Replace `keyEvents` with a specific conversion event, or add metrics to the GA4 nodes and the Code node.
- Change the schedule to monthly and the date windows to 30 days.
- Send to Slack or Telegram instead of Gmail.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/y02Vz
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
