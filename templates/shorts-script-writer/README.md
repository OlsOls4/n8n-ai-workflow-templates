# Write YouTube Shorts, TikTok and Reels scripts from a form with Gemini and Google Sheets

## Description (n8n listing)

Short-form scripts fail in the first three seconds or run 20 seconds too long. This template writes a ready-to-film script from a simple n8n form and then *checks* it. Gemini returns a beat-by-beat script (timing, voiceover, on-screen text, what to film), three alternative hooks, a caption, hashtags and a call to action. A Code step counts the spoken words, estimates the length at your speaking pace, enforces platform rules (adds `#shorts` for YouTube, keeps 3-5 hashtags, caption limits), flags banned words and, if the script is more than 15% over your target, has Gemini tighten it once and checks it again. The result is saved to Google Sheets and shown on the form's result page.

## Who it's for
- YouTube Shorts, TikTok and Instagram Reels creators
- Social media managers writing for several accounts
- Coaches and small brands starting short-form video

## How it works
1. **Short video brief form** collects topic, audience, platform, length, tone and CTA.
2. **Set channel voice** adds your niche, voice notes, banned words and words per second.
3. **Write short-form script** (Basic LLM Chain + Gemini + Structured Output Parser) returns title, 3 hooks, timed beats, caption, hashtags and CTA.
4. **Check length and platform rules** measures spoken length and applies the platform rules; too-long scripts go through **Tighten the script** once.
5. **Save script to Google Sheets** appends the row and **Show the script** displays it.

## Setup
1. Add a free **Google Gemini (PaLM) API** credential (key from https://aistudio.google.com/app/apikey).
2. Create a Google Sheet with a `Scripts` tab: `created_at, topic, platform, length_seconds, title, hook_1, hook_2, hook_3, script, caption, hashtags, cta, est_seconds, status, issues`.
3. Put the Sheet ID in **Set channel voice** and connect **Google Sheets**.
4. Edit **Set channel voice**, activate the workflow and open the form's Production URL.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Change `words_per_second` (2.5 is natural; 3 for fast talkers).
- Edit the `RULES` object at the top of the check node for new platform limits.
- Add a field for a reference video or brand pillars.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/mipKh
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
