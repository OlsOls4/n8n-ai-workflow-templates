# Manage employee leave requests with working-day counts, Google Sheets balances and Gmail approvals

A hosted time-off form that counts real working days (weekends and public holidays removed), checks the leave balance in Google Sheets and asks the manager to approve in one click by Gmail.

## Who it's for
Small businesses, agencies and office managers who handle holiday requests by email and spreadsheet and keep losing track of balances.

## Description (n8n listing)
A complete time-off process for small teams that still handle leave by email and spreadsheets. Employees fill in a hosted form; the workflow counts the real working days (weekends and your country's public holidays removed, half days supported), checks their annual leave balance, and emails their manager one-click Approve / Decline buttons. The decision updates the balance in Google Sheets, logs the request and tells the employee.

### How it works
1. **Leave request form** collects email, leave type, dates, half day and notes.
2. **Get public holidays** pulls holidays for the request's years from the free Nager.Date API (no key).
3. **Look up employee** finds their allowance, days taken and manager in the `Employees` tab.
4. **Count working days and check balance** validates dates, counts working days and blocks requests that exceed the balance.
5. **Ask manager to approve** sends a Gmail approval email and waits up to 3 days.
6. Approved: the balance is updated, the request logged and the employee emailed. Declined or no answer: the employee (or HR) is told.

### Setup
1. Connect **Google Sheets** and **Gmail** credentials.
2. Create a sheet with `Employees` and `Requests` tabs (headers below) and put the Sheet ID in **Set leave policy**.
3. In **Set leave policy** set your country code (GB, US, DE...), optional region (e.g. GB-SCT) and HR email.
4. Activate and share the form URL with your team.

### Customization
- Change working days (`1,2,3,4,5` = Mon-Fri) or the 3-day wait.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. Connect **Google Sheets** and **Gmail** credentials.
2. Create a Google Sheet with two tabs:
   - `Employees`: `email | name | manager_email | annual_allowance | days_taken` (emails in lower case)
   - `Requests`: `request_id | submitted | employee | email | leave_type | start_date | end_date | working_days | status | decided | reason`
3. Put the Sheet ID in **Set leave policy**.
4. In **Set leave policy** set `country_code` (ISO code: GB, US, IE, DE, AU...), optional `holiday_region` (e.g. `GB-SCT`, `US-CA`) and `hr_email`.
5. Activate and share the form URL.

## Customization
- Working days: `1,2,3,4,5` = Monday to Friday (7 = Sunday).
- The approval waits 3 days, then HR is emailed. Change it in **Ask manager to approve**.
- Public holidays come from the free Nager.Date API (https://date.nager.at), no key needed. If it is unreachable the request is still counted, without holidays.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google account with Google Sheets and Gmail

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/YH1RU
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
