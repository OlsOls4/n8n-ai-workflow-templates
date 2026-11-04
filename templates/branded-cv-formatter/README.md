# Turn PDF CVs into branded candidate profiles with Gemini, Google Docs templates and Google Sheets

## Description (n8n listing)

Recruiters lose hours every week retyping CVs into the agency format, and CV-formatting SaaS charges per CV forever. Upload a PDF CV to this form and get it back in **your** branded Google Docs template: a clean candidate profile with summary, key skills, experience and education, plus a PDF ready to send. Gemini extracts the profile in a neutral third-person voice, never invents facts and leaves out protected details such as age or marital status. Every candidate is logged to Google Sheets and you get the links by e-mail.

## Who it's for
- Recruitment and staffing agencies
- In-house talent teams presenting shortlists to hiring managers
- Freelance recruiters who send candidate profiles to clients

## How it works
1. **CV upload form** takes the PDF, the role and optional recruiter notes.
2. **Extract PDF text** reads the text layer; scanned PDFs are flagged by e-mail instead of producing a bad profile.
3. **Extract candidate profile** (Basic LLM Chain + Gemini + Structured Output Parser) returns the profile.
4. **Plan documents** writes the text for every placeholder (experience with dates and bullet highlights, education, skills...).
5. **Copy branded template** + **Fill the template** create the Google Doc; **Export as PDF** saves the PDF in your output folder.
6. The candidate is logged to `Candidates` and **Email the recruiter** sends the Doc and PDF links.

## Setup
1. Connect **Google Drive**, **Google Docs**, **Google Sheets**, **Gmail** and **Google Gemini (PaLM) API**.
2. Create a branded Google Doc (your logo, colours, fonts) containing these placeholders, each on its own line: `{{CANDIDATE_NAME}}`, `{{HEADLINE}}`, `{{LOCATION}}`, `{{CONTACT}}`, `{{REFERENCE}}`, `{{SUMMARY}}`, `{{KEY_SKILLS}}`, `{{EXPERIENCE}}`, `{{EDUCATION}}`, `{{CERTIFICATIONS}}`, `{{LANGUAGES}}`, `{{AVAILABILITY}}`, `{{SALARY}}`, `{{RIGHT_TO_WORK}}`, `{{RECRUITER_NOTES}}`, `{{RECRUITER_NAME}}`, `{{RECRUITER_CONTACT}}`, `{{AGENCY_NAME}}`, `{{DATE}}`. Copy the Doc ID from its URL.
3. Create a Google Sheet with this tab:
   - `Candidates`: `logged_at | reference | version | candidate | email | phone | headline | location | years_experience | seniority | sector | key_skills | notice_period | salary_expectation | right_to_work | client | role | source | original_file | doc_url | pdf_url | duplicate_of | recruiter_notes`
4. Fill in **Set formatter settings** (sheet ID, template doc ID, output folder ID, agency name, recruiter name, e-mail and phone).
5. Put your e-mail in **Email the error**, pick this workflow under **Workflow settings > Error workflow**, activate and open the form URL.

## Requirements
- n8n 2.x, cloud or self-hosted (built and import-tested on n8n 2.43.7). Built-in nodes only, no community nodes.
- A Google account (Gmail / Google Workspace). Google credentials in n8n: https://docs.n8n.io/integrations/builtin/credentials/google/
- A Google Gemini API key (the free tier from https://aistudio.google.com/app/apikey is enough for normal volumes).

## Customisation
- Leave out any placeholder you don't want: it is simply not in your template.
- Change the tone or language in `language` and in the prompt of **Extract candidate profile**.
- Put the output in client-specific folders by editing `output_folder_id` per run (or use the Pro version's `Templates` tab).

## Troubleshooting
- **'No text layer' e-mail**: the PDF is a scan or an image. Ask for the original file (the Pro version reads scans and Word files).
- **Placeholders left in the Doc**: the placeholder text must match exactly, including the double braces and capitals; retype it in one go so Google Docs doesn't split the formatting.
- **Copy fails**: the connected Google account needs access to the template and the output folder.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/KuTCy
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
