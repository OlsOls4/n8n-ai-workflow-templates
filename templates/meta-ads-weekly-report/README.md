# Send a weekly Meta Ads report with week-over-week KPIs and Gemini insights via Gmail

Every Monday, pull last week's Meta Ads results per campaign, compare them with the week before, flag wasted spend and fatigue, and email an HTML report with Gemini insights.

## Who it's for
Business owners running their own Facebook and Instagram ads, freelance media buyers and small agencies who build weekly reports by hand.

## Description (n8n listing)
Every Monday morning, pull last week's Meta (Facebook and Instagram) Ads results per campaign, compare them with the week before, flag wasted spend and fatigue with clear rules, and email a clean HTML report with a short Gemini-written summary of wins, problems and next steps. For business owners, freelance media buyers and small agencies who are tired of screenshotting Ads Manager.

### How it works
1. **Set report settings** holds the ad account, the conversion you track (purchase, lead, complete_registration or messaging), targets and recipient.
2. **Get last week by campaign** and **Get the week before** call the Marketing API insights edge for the last two full 7-day periods.
3. **Compare weeks and flag campaigns** calculates spend, conversions, CPA, ROAS, link CTR, CPM and frequency, week-over-week changes and rule flags (spend with no conversions, CPA 30% over target, low CTR, frequency above 3).
4. **Write performance insights** turns only those numbers into a headline, wins, problems and actions.
5. **Email the report** sends KPI tiles, notes and a campaign table via Gmail.

### Setup
1. Create a **Facebook Graph API** credential with a system-user or long-lived token that has `ads_read` (README.md walks through it).
2. Add **Google Gemini (PaLM) API** and **Gmail** credentials.
3. Fill in **Set report settings** (`act_` + your ad account number).

### Customization
- Change thresholds in the settings node; switch Gmail to a draft to review first.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. **Meta access token**: in Meta Business Settings create a System User, assign it your ad account, and generate a token with the `ads_read` permission (or use a long-lived user token). In n8n create a **Facebook Graph API** credential with that token.
2. Add **Google Gemini (PaLM) API** and **Gmail** credentials.
3. In **Set report settings** set `ad_account_id` (`act_` + the number in Ads Manager), name, recipient, currency symbol, the conversion you track (`purchase`, `lead`, `complete_registration` or `messaging`), and your CPA/ROAS targets.
4. Activate. The first report arrives next Monday at 8am (or click Test workflow).

## Customization
- Rule thresholds (`min_ctr`, `max_frequency`, targets) are in **Set report settings**.
- Swap **Email the report** for a Gmail draft if you want to review before it goes to a client.
- Custom conversions: put the exact `action_type` (e.g. `offsite_conversion.custom.123`) in `conversion_action`.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Meta ad account and a token with `ads_read`

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/613vR
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
