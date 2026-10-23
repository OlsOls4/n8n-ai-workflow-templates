# Answer website chat questions from a Google Sheets FAQ with Gemini and capture leads

An embeddable website chat widget that answers only from your Google Sheets FAQ with Gemini, logs every conversation and saves visitors' contact details as leads.

## Who it's for
Local service businesses, clinics, shops and the web agencies that build their sites: anyone answering the same customer questions every day.

## Description (n8n listing)
Put an AI chat widget on any website that answers only from your own FAQ in Google Sheets, admits when it doesn't know, and turns interested visitors into leads. Built for local service businesses, clinics, agencies and shops that get the same questions every day. No vector database: edit answers in the sheet and the bot uses them on the next message.

### How it works
1. **When a visitor sends a chat message** receives messages from the embedded n8n chat widget.
2. **Load FAQ from Google Sheets** reads your `FAQ` tab (question, answer, category, active) and **Build knowledge base** turns it into context and spots emails or phone numbers in the message.
3. **Answer the visitor** (AI Agent + Gemini + 10-message memory) replies from the FAQ only and returns structured data: the reply, whether the FAQ covered it, whether they want a human, and any lead details.
4. Every exchange is logged to `Chat log`, so unanswered questions show you what to add to the FAQ.
5. Visitors who leave an email or phone are saved to `Leads` (one row per conversation).

### Setup
1. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials.
2. Create a sheet with `FAQ`, `Chat log` and `Leads` tabs (headers below) and put the Sheet ID in **Set business details**.
3. Fill in **Set business details**.
4. Activate, then paste the embed snippet below into your site, using the chat trigger's production URL.

Failure alerts: fill in the alert node in **Alert on errors** and choose this workflow under **Settings > Error workflow**.

## Setup
1. Add **Google Gemini (PaLM) API** and **Google Sheets** credentials.
2. Create a Google Sheet with three tabs:
   - `FAQ`: `question | answer | category | active` (set active to `no` to hide a row)
   - `Chat log`: `time | session_id | question | reply | answered_from_faq | wants_human`
   - `Leads`: `session_id | updated | name | email | phone | need | wants_human`
3. Put the Sheet ID in **Set business details** and fill in **Set business details**.
4. Activate the workflow, copy the production URL from **When a visitor sends a chat message**, and add this before `</body>` on your site:

```html
<link href="https://cdn.jsdelivr.net/npm/@n8n/chat/dist/style.css" rel="stylesheet" />
<script type="module">
  import { createChat } from 'https://cdn.jsdelivr.net/npm/@n8n/chat/dist/chat.bundle.es.js';
  createChat({ webhookUrl: 'YOUR_PRODUCTION_CHAT_URL', initialMessages: ['Hi! Ask me anything about our services.'] });
</script>
```

## Customization
- Set **Allowed Origins** on the chat trigger to your domain instead of `*`.
- Edit tone and rules in the system message of **Answer the visitor**.
- Filter `Chat log` by `answered_from_faq = no` to see what to add to the FAQ.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), Cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Google account with Google Sheets
- Any website where you can add a script tag

## Notes
- All IDs in the JSON are placeholders (`YOUR_...`). No credentials are included.
- Gemini model names can be swapped for any chat model node (OpenAI, Anthropic, Groq, Ollama); prompts and Structured Output Parsers stay the same.
- Tested on n8n 2.43.7 with fixture data and an OpenAI-compatible stand-in model (live Gemini calls were not possible in the test environment).

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($39, extra features listed on the page): https://payhip.com/b/YQBt7
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
