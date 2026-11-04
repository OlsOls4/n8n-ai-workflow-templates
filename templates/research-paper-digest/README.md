# Send a weekly arXiv research digest with AI TL;DRs and relevance scores using Gemini and Gmail

## Description (n8n listing)

Keep up with new research without skimming arXiv by hand. Every Monday the workflow searches arXiv for each of your topics (optionally limited to categories such as cs.CL), keeps papers from the last week, skips any it has already sent you, and asks Gemini for a one-sentence TL;DR plus a 1-10 relevance score based on a short description of *your* interests. Papers that clear your bar arrive in one e-mail, best first, with links. arXiv's API needs no key and Gemini's free tier covers normal use.

## Who it's for
- PhD students and researchers tracking a field
- R&D and applied-AI teams
- Analysts, consultants and science writers

## How it works
1. **Every Monday at 7am** starts the run; **Set digest settings** holds topics, interests, categories, look-back and e-mail.
2. **Search arXiv** runs one query per topic, newest first, 3.5 seconds apart as arXiv requests.
3. **Read the papers** parses the feed, keeps the look-back window and removes cross-topic duplicates.
4. **Skip papers already sent** remembers paper IDs between runs; **Keep the newest papers** caps the volume.
5. **TL;DR and relevance** (Gemini + structured output) summarises each abstract; **Build the digest** and **Send the digest** e-mail the relevant ones.

## Setup
1. Add **Google Gemini (PaLM) API** and **Gmail** credentials.
2. Edit **Set digest settings**: topics (one per line), `research_profile`, categories and your e-mail.
3. Run it once to test, then activate.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key: the free tier at https://aistudio.google.com/app/apikey is enough for normal use. Any other chat model node (OpenAI, Anthropic, Groq, Ollama) can replace the Gemini node.

## Customisation ideas
- Use exact arXiv syntax in a topic line, e.g. `au:hinton` or `ti:diffusion`.
- Raise `min_relevance` for a shorter e-mail.
- Change the schedule to daily for fast-moving fields.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/DJare
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
