# Find striking-distance keywords in Google Search Console and write content briefs with Gemini

Every week, find the Search Console queries where your pages rank 4-20, estimate the clicks a top-3 move would bring, and get a Gemini brief to improve each page in Google Sheets.

## Who it's for
SEO freelancers, content marketers and site owners who want a weekly, prioritised list of pages to improve rather than another dashboard.

## Description (n8n listing)
Every Monday, pull the last 28 days of Google Search Console data, find the queries where your pages rank in positions 4-20 (close to page-one top spots), estimate the extra clicks a move to position 3 would bring, read each page, and let Gemini write a brief to improve that page. Briefs land in Google Sheets. For SEO freelancers, content teams and site owners who want a weekly to-do list instead of a dashboard.

### How it works
1. **Query Search Console** calls the Search Analytics API (query + page, last 28 days, 3-day data lag skipped).
2. **Find striking-distance keywords** filters by position band, impressions and brand terms, scores each query by potential clicks (impressions x the CTR gap to position 3) and keeps the top pages.
3. **Fetch the ranking page** and **Read page content** check the title, H1, H2s, word count and whether each query appears on the page.
4. **Write content brief** returns title, meta description, H2 outline, missing subtopics, FAQs and quick wins.
5. Briefs are appended to the `Briefs` tab.

### Setup
1. Create an **OAuth2 API** credential for Google: auth URL `https://accounts.google.com/o/oauth2/v2/auth`, token URL `https://oauth2.googleapis.com/token`, scope `https://www.googleapis.com/auth/webmasters.readonly`, auth query `access_type=offline&prompt=consent` (details in README.md).
2. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials and put the Sheet ID in **Set report settings**.
3. Set your property (`sc-domain:example.com` or `https://www.example.com/`) and brand terms in **Set report settings**.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. **Search Console access** (one-time, about 10 minutes):
   - In Google Cloud Console create a project, enable the **Google Search Console API**, and create an **OAuth client ID** (Web application) with your n8n OAuth callback URL as redirect URI.
   - In n8n create an **OAuth2 API** credential: Grant Type `Authorization Code`, Authorization URL `https://accounts.google.com/o/oauth2/v2/auth`, Access Token URL `https://oauth2.googleapis.com/token`, Scope `https://www.googleapis.com/auth/webmasters.readonly`, Auth URI Query Parameters `access_type=offline&prompt=consent`, Authentication `Body`. Paste the client ID and secret and connect.
2. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials.
3. Create a Google Sheet with a `Briefs` tab: `week | page | primary_keyword | potential_clicks | impressions_28d | best_position | queries | search_intent | recommended_title | recommended_meta | h2_outline | missing_subtopics | faq_questions | quick_wins | status`
4. Put the Sheet ID in **Set report settings**, then set `site_url` (`sc-domain:example.com` for domain properties or `https://www.example.com/` for URL-prefix) and brand terms in **Set report settings**.

## Customization
- Position band, minimum impressions and number of pages are in **Set report settings**.
- Potential clicks = impressions x (expected CTR at position 3 - current CTR), using a standard CTR curve you can edit in **Find striking-distance keywords**.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- Access to the site's Google Search Console property and a Google Cloud OAuth client

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/jaKdp
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
