# Find local business leads from OpenStreetMap with website checks and AI openers in Google Sheets

## Description (n8n listing)

Finding local businesses to pitch usually means a paid Google Maps scraper. This template uses free sources only: OpenStreetMap's Nominatim search and each business's own homepage. Enter a category (dentist, cafe, hairdresser, plumber...) and a town in an n8n form. The workflow finds the businesses in that area (throttled to Nominatim's one request per second), drops roads and bus stops, and dedupes the list. It reads phone, e-mail, website and social links from OpenStreetMap tags and from the homepage, then checks each site for HTTPS, a mobile viewport tag, the copyright year, a meta description and online booking. Gemini scores how well each business fits what you sell and writes a short, specific cold-email opener. Leads are upserted into Google Sheets by OpenStreetMap ID, and the best ones appear on the form's result page.

OpenStreetMap lists fewer businesses than Google Maps, especially in small towns. Treat it as a free, legal starting point rather than a complete directory.

## Who it's for
- Web designers and developers selling to local businesses
- Local SEO and marketing freelancers
- Agencies building prospect lists for SMB outreach

## How it works
1. **Lead search form** collects category, town and how many leads (up to 40).
2. **Find the town on OpenStreetMap** gets the town's bounding box; **Search businesses in the area** queries Nominatim inside it.
3. **Clean and dedupe businesses** keeps named businesses and reads contact tags; towns or categories with no results get a friendly message.
4. **Fetch the homepage** + **Read contact details from the site** add e-mails, phones, socials and website checks.
5. **Score fit and write opener** (Gemini + Structured Output Parser) returns fit score, reasons, pitch angle, opener and subject line.
6. **Save leads to Google Sheets** upserts by `lead_id`; **Show the leads** lists the top results.

## Setup
1. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials.
2. Create a Google Sheet with a `Leads` tab using the columns below.
3. Open **Set lead finder settings**: Sheet ID, what you sell, your ideal customer, and a real contact e-mail in `user_agent` (Nominatim policy).
4. Activate the workflow and open the form's Production URL.

### Google Sheet tabs
- `Leads`: `lead_id, found_at, search, name, category, address, postcode, city, phone, email, other_emails, website, facebook, instagram, linkedin, other_socials, opening_hours, has_website, site_status, site_issues, site_score, fit_score, priority, reasons, pitch_angle, opener, subject_line, osm_url, maps_url, status`

### Settings
| Node | Setting | Default | What it does |
|---|---|---|---|
| **Set lead finder settings** | `your_service` | `Website design, online booking and local SEO for small busin` | What you sell, in one line. The AI scores fit against this. |
| **Set lead finder settings** | `ideal_customer` | `Independent local businesses with 1-20 staff that rely on lo` | Who you want to work with (size, type, situation). |
| **Set lead finder settings** | `user_agent` | `LocalLeadFinder/1.0 (n8n workflow; YOUR_CONTACT_EMAIL)` | Sent to OpenStreetMap Nominatim. Its usage policy requires an app name plus a real contact e-mail. |
| **Set lead finder settings** | `language` | `British English` | Language and spelling for everything the AI writes. |
| **Set lead finder settings** | `min_score_hot` | `70` | Fit score (0-100) from which a lead counts as high priority / hot. |
| **Set lead finder settings** | `only_inside_town` | `True` | Drop results whose OpenStreetMap address doesn't mention the town (a town's bounding box can reach into neighbouring towns). Set false to keep the whole area. |
| **Set lead finder settings** | `sheet_id` | YOUR_SHEET_ID (replace) | The ID from your Google Sheet URL: docs.google.com/spreadsheets/d/<ID>/edit |

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key. The free tier at https://aistudio.google.com/app/apikey is enough for normal volumes.

## Customisation ideas
- Use OSM words for the category (dentist, cafe, restaurant, hairdresser, estate agent, florist). Very niche phrases return little.
- Change the scoring rules in the prompt, for example to favour businesses without a website.
- Add a Gmail draft step after scoring to turn the opener into a full e-mail.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/5jZJr
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
