# Write researched blog posts with a multi-agent Gemini team and save them to Google Docs

## Description (n8n listing)

One-prompt AI articles read like one-prompt AI articles. This template splits the job between four agents that run on the free Gemini tier, with no SerpAPI, Perplexity or OpenAI key. Give it a topic or target keyword in an n8n form, plus optional source URLs. The **research agent** reads Wikipedia, Google Autocomplete questions and your source pages, then builds a fact sheet with source links and a list of claims to avoid. The **outline agent** plans the title, slug, meta description, H2s and FAQs. The **writer agent** writes the Markdown article using only those facts, linking sources inline. The **editor agent** scores the draft for SEO, readability, accuracy, voice and completeness, and lists specific fixes. If the score is under your bar, a revision agent applies them. The final article, its scores and its sources are saved to a new Google Doc.

## Who it's for
- Bloggers and niche-site owners
- Content marketers and small agencies
- Founders writing their own SEO content

## How it works
1. **Blog post brief form**: topic, audience, length, notes and source URLs; **Prepare the brief** normalises it.
2. **Search Wikipedia**, **Fetch research sources** (Autocomplete questions, your pages) and **Collect research notes** gather material.
3. **Research agent** → fact sheet; **Outline agent** → structure; **Writer agent** → Markdown article.
4. **Editor agent** scores it; **Decide next step** sends it to the **Revision agent** once if it's below `min_quality_score`.
5. **Finalise article** builds the doc text and HTML; **Create the Google Doc** and **Write the article into the Doc** save it.

## Setup
1. Add **Google Gemini (PaLM) API** and **Google Docs** credentials.
2. Fill in **Set blog writer settings**: Drive folder ID, brand voice, language and default length.
3. Activate and open the form's Production URL.


### Settings
| Node | Setting | Default | What it does |
|---|---|---|---|
| **Set blog writer settings** | `brand_voice` | `Friendly, practical and specific. Short sentences, real exam` | How the writer should sound. |
| **Set blog writer settings** | `default_audience` | `Busy beginners who want clear, trustworthy advice` | Audience used when the form/queue row leaves it blank. |
| **Set blog writer settings** | `language` | `British English` | Language and spelling for everything the AI writes. |
| **Set blog writer settings** | `wiki_language` | `en` | Wikipedia language edition for research, and the Autocomplete language. |
| **Set blog writer settings** | `default_word_count` | `1200` | Length used when none is given. |
| **Set blog writer settings** | `min_quality_score` | `80` | Editor score (0-100) an article must reach before it's accepted. |
| **Set blog writer settings** | `max_edit_rounds` | `1` | Maximum revision rounds by the writer after editor feedback. |
| **Set blog writer settings** | `docs_folder_id` | YOUR_DRIVE_FOLDER_ID (replace) | Google Drive folder for the new Docs (the ID from the folder URL). |

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7), cloud or self-hosted. Built-in nodes only, no community nodes.
- A Google Gemini API key. The free tier at https://aistudio.google.com/app/apikey is enough for normal volumes.

## Customisation ideas
- Rewrite the brand voice and the writer rules for your style guide.
- Raise `min_quality_score` for stricter editing.
- Use another Wikipedia language with `wiki_language`.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/jDC4A
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
