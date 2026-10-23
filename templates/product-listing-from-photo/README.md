# Write product titles, descriptions and tags from photos with Gemini Vision and Google Sheets

## Description (n8n listing)

Writing listings is the slowest part of adding stock. Upload one product photo through a simple n8n form, add the facts the photo can't show (size, material, price), choose Etsy, Shopify or another shop and a tone, and Google Gemini Vision writes a complete listing: title, three-paragraph description, five bullet points, tags, SEO title, meta description and alt text.

A Code node then enforces marketplace limits (140-character Etsy titles, exactly 13 tags of 20 characters or fewer) and marks each draft `REVIEW` or `FIX`. The prompt forbids inventing sizes, materials or certifications. Drafts are saved to Google Sheets and shown on the result page; nothing is published to your shop.

## Who it's for
- Etsy and Shopify sellers adding new products
- Makers and small brands without a copywriter
- E-commerce VAs and agencies writing listings for clients

## How it works
1. **Product photo form** takes the photo (JPG, PNG or WebP), notes, platform and tone.
2. **Write listing from photo** (Basic LLM Chain with the image + Gemini 3.8 Flash + Structured Output Parser) returns the listing as JSON.
3. **Check listing limits** trims the title, deduplicates and limits tags, and flags problems.
4. **Save listing to Google Sheets** appends the draft and **Show the listing** displays it.

## Setup
1. Add a free **Google Gemini (PaLM) API** credential on **Gemini 3.8 Flash (vision)**.
2. Create a Google Sheet with a `Listings` tab and this header row:
   `created_at | platform | product_notes | photo_filename | title | description | bullet_points | tags | seo_title | meta_description | alt_text | colors | materials | status | issues`
3. Put the Sheet ID in **Config** and connect **Google Sheets OAuth2**.
4. Activate and open the form's Production URL (bookmark it on your phone for quick uploads).

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A Google account with Google Sheets

## Customisation ideas
- Add your brand voice and words to avoid to the prompt.
- Add Amazon or eBay to the platform dropdown and its limits in **Check listing limits**.
- Swap the vision model for another multimodal chat model.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/semO6
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
