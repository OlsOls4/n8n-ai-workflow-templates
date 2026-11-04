# Extract invoice data from Gmail with Gemini, check the maths and duplicates, and log to Google Sheets

## Description (n8n listing)

Supplier invoices and receipts arrive in Gmail as PDFs, scans or phone photos. This workflow reads each one with Gemini and then *checks* it before it reaches your spreadsheet: missing fields, net + tax = total, line items against the net, unusual tax rates, impossible dates and duplicates (same supplier and invoice number, or same supplier and total within 7 days). Every document is logged to Google Sheets as `ok`, `needs review`, `duplicate` or `ignored` (statements, quotes and payment reminders), and you get one summary e-mail per run.

## Who it's for
- Bookkeepers and small accounting firms processing invoices for clients
- Ops and office managers who approve supplier bills
- Trades, agencies and small businesses that still type invoices into spreadsheets

## How it works
1. **New invoice email** polls Gmail every 5 minutes for messages with invoice-like attachments (edit the search to use a label).
2. **Split attachments** turns every PDF or image into its own item and skips logos and signature images.
3. **Extract PDF text** reads PDFs with a text layer; scans and photos go to **Read scan or photo with Gemini**.
4. **Extract invoice fields** (Basic LLM Chain + Gemini + Structured Output Parser) returns supplier, number, dates, net, tax, total, currency, bank digits and line items.
5. **Check maths and duplicates** compares with your existing rows and labels each document.
6. Rows are appended to `Invoices` and **Email the summary** sends one e-mail per run.

## Setup
1. Connect **Gmail**, **Google Sheets** and a **Google Gemini (PaLM) API** credential.
2. Create a Google Sheet with this tab (header row exactly as shown):
   - `Invoices`: `invoice_id | received | sender_email | file_name | document_type | vendor | vendor_key | invoice_number | invoice_date | due_date | currency | net | tax | total | status | issues | line_items`
3. Fill in **Set invoice settings**: `sheet_id`, `notify_email`, `allowed_tax_rates` (your VAT/GST rates, e.g. `0,5,20`), `tolerance` (rounding allowance, default 0.05) and `min_confidence`.
4. Put your e-mail in **Email the error** and pick this workflow under **Workflow settings > Error workflow**.
5. Activate.

## Requirements
- n8n 2.x, cloud or self-hosted (built and import-tested on n8n 2.43.7). Built-in nodes only, no community nodes.
- A Google account (Gmail / Google Workspace). Google credentials in n8n: https://docs.n8n.io/integrations/builtin/credentials/google/
- A Google Gemini API key (the free tier from https://aistudio.google.com/app/apikey is enough for normal volumes).

## Customisation
- Use a Gmail label instead of the search: set **Label Names or IDs** in the trigger's filters and empty the search.
- Add your own checks to **Check maths and duplicates** (e.g. require a PO number above a certain amount).
- Change `allowed_tax_rates` for your country: `0,7,19` for Germany, `0,10` for Australia, `0` to switch the check off.

## Troubleshooting
- **Nothing happens**: the trigger only sees e-mails that arrive after activation and match the search. Send yourself a test invoice.
- **`needs review` on good invoices**: check `allowed_tax_rates`; mixed-rate invoices will show a rate warning (expected).
- **Wrong dates**: numeric dates are read as day/month/year unless the document is clearly American. Edit the rule in the prompt if you work in US format.
- **Scans are empty**: Gemini needs a readable image; very low-resolution phone photos lower the confidence and are flagged.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/9RnZf
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
