# Audit any web page for on-page SEO issues from an n8n form with Gemini recommendations

A hosted form that audits any page for 17 on-page SEO checks, scores it 0-100 and asks Gemini for a prioritised fix list with a new title and meta description.

## Who it's for
SEO freelancers and agencies auditing prospects, web designers handing over sites, and business owners checking their own pages.

## Description (n8n listing)
Paste a URL (and optionally a target keyword) into a hosted n8n form and get a scored on-page SEO audit in about 20 seconds: 17 technical and content checks run in code, then Gemini turns the failures into a prioritised fix list with a rewritten title and meta description. Useful for freelancers and agencies auditing prospects, and for business owners checking their own pages. Needs only a free Gemini key.

### How it works
1. **SEO audit form** collects the page URL and keyword. **Check the URL** adds https:// and validates it.
2. **Fetch page HTML** and **Fetch robots.txt** download the page (redirects followed) and the site's robots rules.
3. **Extract on-page signals** parses title, meta description, canonical, robots meta, headings, word count, image alt text, links, lang, viewport, Open Graph, JSON-LD and keyword placement, then scores weighted checks to 0-100.
4. **Write SEO recommendations** asks Gemini for 3-6 concrete fixes, a 30-60 character title and a 120-155 character meta description, using only facts from the page.
5. **Show audit report** displays the result. Pages that fail to load get a clear error page.

### Setup
1. Add a **Google Gemini (PaLM) API** credential (free key from aistudio.google.com).
2. Activate the workflow and open the form's production URL.

### Customization
- Change check weights inside **Extract on-page signals**.
- Add a Gmail or Google Sheets node after **Build audit report** to email reports or log leads.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. Add a **Google Gemini (PaLM) API** credential.
2. Activate the workflow and open the form's production URL.
3. Enter a URL and (optionally) a target keyword.

## Customization
- Change check weights in **Extract on-page signals** (each `add(...)` call has a weight).
- To use it as a lead magnet, add an Email field to the form and a Gmail node after **Build audit report**.
- Checks: HTTP status, HTTPS, noindex, robots.txt blocking, title length, meta description length, single H1, H2s, word count, image alt text, canonical, viewport, html lang, Open Graph, JSON-LD, internal links, sitemap in robots.txt, plus five keyword-placement checks when a keyword is given.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/AMjyN
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
