# Check if a website is trustworthy with domain age, page checks and a Gemini risk verdict

## Description (n8n listing)

Check whether a website looks trustworthy before you buy from it, pay a new supplier or click a link someone sent you. Paste the URL into an n8n form and the workflow collects facts from free public sources: domain age and registrar from RDAP, whether the site loads over HTTPS, security headers, contact details, privacy/returns policies, company details, extreme discounts and risky payment or phishing wording. A Code node turns those facts into a 0-100 risk score with red flags and good signs; Gemini only explains the result and suggests next steps. No SerpAPI or paid lookups.

## Who it's for
- Online shoppers and small businesses vetting suppliers
- E-commerce and marketplace operations teams
- IT helpdesks checking links users forward

## How it works
1. **Check a website** form takes the URL and what you are about to do.
2. **Normalise the URL** extracts the registrable domain (handles co.uk and similar).
3. **Fetch the page** and **Look up domain age (RDAP)** gather facts; a failed check counts as unknown.
4. **Score the risk signals** returns a 0-100 score, red flags and good signs.
5. **Write the verdict** (Gemini) explains it; **Show the report** displays it.

## Setup
1. Add a free **Google Gemini (PaLM) API** credential.
2. Activate the workflow and open the form's production URL.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key: the free tier at https://aistudio.google.com/app/apikey is enough for normal use. Any other chat model node (OpenAI, Anthropic, Groq, Ollama) can replace the Gemini node.

## Customisation ideas
- Tune the weights and word lists in **Score the risk signals**.
- Add your own allow-list of known-good domains at the top of the same node.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/nRgyH
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
