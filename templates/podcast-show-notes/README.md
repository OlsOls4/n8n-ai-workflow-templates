# Write podcast show notes, chapters and social posts from new RSS episodes with Gemini and Gmail

## Description (n8n listing)

Show notes take longer than they should. This template watches your podcast RSS feed and, for each new episode, sends the audio straight to Gemini for a timestamped transcript (no separate transcription service). Gemini then writes a summary, 120-180 word show notes, key takeaways, chapters, title ideas, verbatim quotes, an X post, a LinkedIn post, an Instagram caption and a newsletter blurb, using only facts from the episode. Chapters are validated against YouTube's rules (first at 00:00, at least three, 10 seconds apart, inside the episode) and turned into a paste-ready YouTube description. Everything arrives as one email and is logged in Google Sheets. If the audio can't be transcribed, the notes fall back to the episode description and the email says so.

## Who it's for
- Independent podcasters
- Podcast editors and producers
- Video podcasters publishing to YouTube

## How it works
1. **Read podcast RSS feed** and **Pick newest episodes** find new audio episodes; **Skip episodes already done** prevents repeats.
2. **Transcribe episode with Gemini** (Google Gemini node, audio from URL) returns a transcript with timestamps and speakers.
3. **Write show notes pack** (Basic LLM Chain + Structured Output Parser) builds the pack.
4. **Check chapters and build email** validates chapters and builds the HTML email and YouTube description.
5. **Email me the show notes** and **Log episode to Google Sheets** deliver it.

## Setup
1. Add **Google Gemini (PaLM) API**, **Gmail OAuth2** and **Google Sheets OAuth2** credentials.
2. Fill in **Set podcast settings** (feed URL, show name, hosts, tone, your email).
3. Create an `Episodes` tab: `episode_id, title, published, audio_url, transcript_source, chapters, chapters_ok, summary, show_notes, title_ideas, x_post, linkedin_post, instagram_caption, newsletter_blurb, youtube_description, quotes, processed_at`, and put the Sheet ID in **Set podcast settings**.
4. Activate. The first run handles your latest episode.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (the free tier at https://aistudio.google.com/app/apikey is enough for personal use)

## Customisation ideas
- Raise `max_episodes_per_run` to backfill.
- Change the tone or the length rules in the prompt.
- Long episodes use more Gemini tokens; the free tier handles typical 30-60 minute shows.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($24, extra features listed on the page): https://payhip.com/b/YeBfF
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
