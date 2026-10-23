# Draft replies to new YouTube comments with Gemini and review them in Google Sheets

## Description (n8n listing)

Replying to comments grows a channel, but it takes hours. This template checks your five newest uploads every six hours (via the channel's free RSS feed, so no API quota is spent finding videos), pulls comment threads with the official YouTube Data API, and keeps only recent top-level comments with no reply that weren't written by you.

Google Gemini sorts each one (question, praise, feedback, criticism, collaboration, spam), sets a priority and drafts a short reply in the voice you describe. Spam and emoji-only comments are dropped. Drafts land in Google Sheets, highest priority first, with a direct link to the comment. The prompt is told not to invent facts such as version numbers or prices. Nothing is posted automatically.

## Who it's for
- YouTube creators who want to answer more comments in less time
- Channel managers and social media assistants
- Course creators and B2B channels where comments are leads

## How it works
1. **Every 6 hours** triggers; **Set channel and settings** holds your channel ID, voice, lookback window and per-run cap.
2. **Read latest videos from RSS** and **Keep recent videos** get your five newest uploads.
3. **Get comment threads** (HTTP Request with your YouTube OAuth2 credential) fetches up to 50 threads per video.
4. **Pick new unanswered comments** filters out answered, old and own comments; **Skip comments already drafted** removes anything seen before.
5. **Draft reply with AI** (Basic LLM Chain + Gemini + Structured Output Parser) returns category, priority, needs-reply, reply and a summary.
6. **Prepare review rows** sorts by priority and **Save drafts to Google Sheets** appends them.

## Setup
1. In Google Cloud enable **YouTube Data API v3**, then add a **YouTube OAuth2** credential in n8n and select it on **Get comment threads**.
2. Add a free **Google Gemini (PaLM) API** credential.
3. In **Set channel and settings** replace `YOUR_CHANNEL_ID` (starts with `UC`, from YouTube Studio > Settings > Channel > Advanced) and describe your voice.
4. Create a Google Sheet with a `Comments` tab and header row:
   `drafted_at | priority | category | video_title | author | comment | reply_draft | summary | link | comment_id | status`
   then put the Sheet ID in **Set channel and settings** and connect **Google Sheets OAuth2**.
5. Activate.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)
- A YouTube channel, a Google Cloud project with YouTube Data API v3 (free quota), and Google Sheets

## Customisation ideas
- Change `lookback_hours`, the schedule or the number of videos checked.
- Edit categories and reply rules in **Draft reply with AI**.
- Send high-priority drafts to Telegram or Slack.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($19, extra features listed on the page): https://payhip.com/b/HnjXd
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
