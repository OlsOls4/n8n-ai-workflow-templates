# Cluster Google Autocomplete keywords by search intent with Gemini into a Google Sheets content calendar

## Description (n8n listing)

Most keyword-clustering templates need DataForSEO, SerpAPI or Bright Data credits. This one starts from free Google Autocomplete suggestions. Enter up to 10 seed keywords, a country and a language. The workflow expands each seed with question prefixes (how, what, why, best, is, can...) and the alphabet, calling the public suggest endpoint once every 1.2 seconds. It cleans and dedupes the suggestions, removes ones that drift off-topic, and counts how often each keyword appeared as a rough popularity signal. Gemini groups the keywords into topic clusters by search intent, referring to them by id so nothing is invented. Each cluster gets a pillar keyword, intent, funnel stage, content type, priority and working title. A Code step validates the clusters and ranks them. Keywords and a 4-week content calendar are saved to Google Sheets.

Google Autocomplete is an unofficial endpoint and has no search volumes. Use this for topic coverage and intent, not traffic estimates.

## Who it's for
- Bloggers and niche-site owners
- SEO freelancers and small agencies
- Content marketers planning topical authority

## How it works
1. **Keyword seeds form**: seeds (one per line), country and language.
2. **Plan autocomplete queries** builds question and a-z variations, capped by `max_queries`.
3. **Get Google Autocomplete suggestions** calls the suggest endpoint, throttled to one request every 1.2 s.
4. **Clean and count keywords** normalises, dedupes, removes drift, adds an intent hint and counts hits.
5. **Cluster keywords by intent** (Gemini + Structured Output Parser) returns clusters by keyword id; **Validate clusters** drops invented ids and ranks clusters.
6. **Save keywords** and **Save content calendar** upsert to Sheets; **Show the plan** displays the result.

## Setup
1. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials.
2. Create `Keywords` and `Calendar` tabs with the columns below.
3. Fill in **Set planner settings** (Sheet ID, site topic, audience, language, posts per week).
4. Activate and open the form's Production URL.

### Google Sheet tabs
- `Keywords`: `keyword_key, project, keyword, seed, hits, words, is_question, intent, cluster, last_seen`
- `Calendar`: `slot_key, project, publish_date, title, primary_keyword, secondary_keywords, questions, cluster, intent, funnel, content_type, priority, status`

### Settings
| Node | Setting | Default | What it does |
|---|---|---|---|
| **Set planner settings** | `default_project` | `My site` | Project name used when the form leaves it blank. |
| **Set planner settings** | `site_topic` | `Practical guides for home cooks` | What your site is about (guides clustering and briefs). |
| **Set planner settings** | `audience` | `Busy beginners who want simple, reliable advice` | Who you write for. |
| **Set planner settings** | `language` | `British English` | Language and spelling for everything the AI writes. |
| **Set planner settings** | `default_hl` | `en` | Default Autocomplete language (hl), e.g. en, de, fr. |
| **Set planner settings** | `default_gl` | `gb` | Default Autocomplete country (gl), e.g. gb, us, de. |
| **Set planner settings** | `max_queries` | `80` | Maximum Autocomplete calls per run (one every 1.2 s). Keep it modest; the endpoint is unofficial. |
| **Set planner settings** | `max_keywords` | `150` | Maximum keywords sent to the AI for clustering. |
| **Set planner settings** | `posts_per_week` | `2` | Articles per week in the calendar (1-5). |
| **Set planner settings** | `weeks` | `4` | How many weeks the calendar covers. |
| **Set planner settings** | `start_date` | (blank) | First calendar date (YYYY-MM-DD). Blank = next Monday. |
| **Set planner settings** | `sheet_id` | YOUR_SHEET_ID (replace) | The ID from your Google Sheet URL: docs.google.com/spreadsheets/d/<ID>/edit |

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key. The free tier at https://aistudio.google.com/app/apikey is enough for normal volumes.

## Customisation ideas
- Add your own modifiers (e.g. `for kids`, `uk`) to the query list in **Plan autocomplete queries**.
- Raise `max_queries` for more keywords (slower; be polite).
- Change the cluster rules in the prompt (e.g. stricter one-intent-per-page).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/miKNu
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
