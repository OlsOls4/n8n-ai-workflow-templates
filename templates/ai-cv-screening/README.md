# Screen CVs from an n8n form against your job description with Gemini and Google Sheets

## Description (n8n listing)

Hiring for a small team means reading dozens of CVs that don't fit. This template gives you a hosted application form; every PDF CV is read and scored by Google Gemini against your job description and must-haves, and the result lands in Google Sheets with a 0-100 score, a shortlist / maybe / reject recommendation, the must-haves met and missed, strengths, gaps and red flags.

The scoring prompt only judges job-relevant evidence and is told to ignore protected characteristics (name, age, gender, nationality and so on). Scanned or image-only PDFs are caught and the candidate is asked to upload a text-based PDF instead of being scored zero. It runs on Gemini's free tier, and the AI only advises: you still make every decision.

## Who it's for
- Founders and small businesses hiring without an ATS
- Recruitment agencies doing first-pass screening
- Hiring managers who want a ranked sheet instead of an inbox of attachments

## How it works
1. **Job application form** (n8n Form Trigger) collects name, email, PDF CV and an optional note.
2. **Extract text from CV** reads the PDF; **Is the CV readable?** routes unreadable files to **Ask for a text-based PDF**.
3. **Set job description** holds the role title, description, must-haves and nice-to-haves.
4. **Score CV against job description** (Basic LLM Chain + Gemini 3.5 Flash-Lite + Structured Output Parser) returns score, recommendation, summary, must-haves met/missing, strengths, gaps, years of experience, red flags and location.
5. **Prepare candidate row** flattens the result, **Log candidate to Google Sheets** appends it and **Show thank-you page** confirms to the candidate.

## Setup
1. Get a free Gemini API key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential on **Gemini 3.5 Flash-Lite**.
2. Create a Google Sheet with a `Candidates` tab and this header row:
   `submitted_at | name | email | score | recommendation | summary | must_haves_met | must_haves_missing | strengths | gaps | years_experience | red_flags | location | note | cv_filename`
3. Paste the sheet ID (from `docs.google.com/spreadsheets/d/<ID>/edit`) into the `sheet_id` field of **Set job description** and connect a **Google Sheets OAuth2** credential.
4. Write your role into **Set job description** (be specific about must-haves).
5. Activate the workflow, open the Form Trigger's **Production URL** and put it in your job ad.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Google account with Google Sheets

## Customisation ideas
- Change the 80 / 50 score bands or the recommendation rules in the prompt.
- Add form fields (salary expectation, notice period, right to work) and map them in **Prepare candidate row**.
- Use a conditional-format rule on `score` to colour the sheet.
- Swap Gemini for any chat model node (OpenAI, Groq, Ollama).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/fzcWA
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
