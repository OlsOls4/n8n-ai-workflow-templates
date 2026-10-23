# Categorise bank statement CSV transactions into bookkeeping categories with Gemini and Google Sheets

Upload any business bank CSV and get every transaction sorted into bookkeeping categories by Gemini, saved to Google Sheets with review flags and a spending summary.

## Who it's for
Small business owners, freelancers, sole traders and bookkeepers who sort bank statements into categories by hand before doing their books or VAT.

## Description (n8n listing)
Upload a CSV export from any business bank account and get every transaction sorted into a bookkeeping category, saved to Google Sheets, with a summary of income, spending and top suppliers. Built for small business owners, freelancers and bookkeepers who still sort statements by hand.

### How it works
1. **Bank statement upload form** takes the CSV, currency and date format.
2. **Normalise transactions** finds the date, description and amount columns (single amount or paid in / paid out), parses dates and amounts, cleans merchant names and gives each row a stable ID.
3. Unique merchants are sent to Gemini in batches of 40, so 500 rows cost only a few AI calls.
4. Categories are mapped back to every row. Low-confidence results and sign mismatches (money in labelled as an expense) are flagged `needs_review`.
5. Rows are upserted into Google Sheets by ID, so uploading the same statement twice never duplicates anything. The form shows a summary.

### Setup
1. Add a **Google Gemini (PaLM) API** credential (free key from aistudio.google.com).
2. Create a Google Sheet with a `Transactions` tab and the header row listed in **Save to Transactions sheet**'s note.
3. Put the Sheet ID in **Config** and connect **Google Sheets**.
4. Activate and open the form's production URL.

### Customization
- Edit the category list in **Categorise merchants with AI**.
- Change the review threshold (0.7) in **Apply categories to transactions**.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. Add a **Google Gemini (PaLM) API** credential.
2. Create a Google Sheet with a `Transactions` tab and this header row:
   `txn_id | date | description | merchant | amount | currency | category | confidence | needs_review | review_note | ai_reason | corrected_category`
3. Put the Sheet ID in **Config** and connect **Google Sheets**.
4. Activate and open the form's production URL. Upload a CSV, pick the currency and date format.

## Customization
- Edit the category list in **Categorise merchants with AI** (keep "Uncategorised").
- Change the 0.7 review threshold in **Apply categories to transactions**.
- Works with single `amount` columns and with separate paid in / paid out (debit / credit) columns. Amounts like `(12.50)`, `12.50 DR` and `1.234,56` are handled.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Google account with Google Sheets

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/yewoS
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
