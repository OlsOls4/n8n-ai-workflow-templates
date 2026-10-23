# n8n AI workflow templates (free)

25 ready-to-import [n8n](https://n8n.io) workflows that use **Google Gemini's free tier** (or any chat model) with Gmail, Google Sheets, Telegram, Google Analytics, Search Console and more. Every workflow uses built-in n8n nodes only (no community nodes), has sticky-note documentation on the canvas, and ships with placeholders instead of credentials.

Built and import-tested on n8n 2.43.7 (Cloud or self-hosted).

## Quick start

1. Open the template's folder below and download `workflow.json` (click **Raw**, then save).
2. In n8n go to **Workflows > Import from File** (or paste the JSON straight onto a canvas).
3. Add the credentials the template's README lists. For Gemini, a free key from [Google AI Studio](https://aistudio.google.com/app/apikey) is enough for normal use; add it as a **Google Gemini (PaLM) API** credential.
4. Replace every `YOUR_...` placeholder (sheet IDs, chat IDs, emails). The canvas sticky notes say where.
5. Run once manually, check the output, then activate.

Prefer OpenAI, Anthropic, Groq or Ollama? Swap the Gemini chat model node for another chat model node; the prompts and Structured Output Parsers stay the same.

## Templates

### Business & operations

| Template | What it does | Free n8n.io page | Pro version |
|---|---|---|---|
| [Categorise bank statement CSV transactions into bookkeeping categories with Gemini and Google Sheets](templates/bank-transaction-categoriser/) | Upload any business bank CSV and get every transaction sorted into bookkeeping categories by Gemini, saved to Google Sheets with review flags and a spending summary. | — | [Pro $29](https://payhip.com/b/yewoS) |
| [Manage employee leave requests with working-day counts, Google Sheets balances and Gmail approvals](templates/leave-request-approval/) | A hosted time-off form that counts real working days (weekends and public holidays removed), checks the leave balance in Google Sheets and asks the manager to approve in one click by Gmail. | — | [Pro $29](https://payhip.com/b/YH1RU) |
| [Answer website chat questions from a Google Sheets FAQ with Gemini and capture leads](templates/website-faq-chatbot/) | An embeddable website chat widget that answers only from your Google Sheets FAQ with Gemini, logs every conversation and saves visitors' contact details as leads. | — | [Pro $39](https://payhip.com/b/YQBt7) |
| [Answer restaurant FAQs and menu questions with an AI Telegram bot and Google Sheets](templates/restaurant-telegram-bot/) | Telegram bot that answers opening hours, menu and allergen questions only from a Google Sheet you control. | — | [Pro $39](https://payhip.com/b/XmRis) |
| [Screen CVs from an n8n form against your job description with Gemini and Google Sheets](templates/ai-cv-screening/) | Hosted application form; Gemini reads each PDF CV, scores it 0-100 against your job description and must-haves, and logs it to Google Sheets. | — | [Pro $39](https://payhip.com/b/fzcWA) |
| [Triage new Gmail emails with AI labels and priority using Gemini](templates/gmail-ai-triage/) | Gemini reads new unread Gmail and applies category labels (Needs reply, Action, FYI, Newsletter, Receipt, Promotion) plus a High priority label. | — | [Pro $24](https://payhip.com/b/dGXcm) |

### Marketing, SEO & sales

| Template | What it does | Free n8n.io page | Pro version |
|---|---|---|---|
| [Send a weekly Google Analytics 4 report with AI insights via Gmail](templates/ga4-weekly-ai-report/) | Every Monday: GA4 this week vs last week (users, sessions, key events, top pages, sources) with a Gemini-written summary, emailed as HTML. | — | [Pro $29](https://payhip.com/b/y02Vz) |
| [Send a weekly Meta Ads report with week-over-week KPIs and Gemini insights via Gmail](templates/meta-ads-weekly-report/) | Every Monday, pull last week's Meta Ads results per campaign, compare them with the week before, flag wasted spend and fatigue, and email an HTML report with Gemini insights. | — | [Pro $24](https://payhip.com/b/613vR) |
| [Find striking-distance keywords in Google Search Console and write content briefs with Gemini](templates/gsc-striking-distance-briefs/) | Every week, find the Search Console queries where your pages rank 4-20, estimate the clicks a top-3 move would bring, and get a Gemini brief to improve each page in Google Sheets. | — | [Pro $24](https://payhip.com/b/jaKdp) |
| [Audit any web page for on-page SEO issues from an n8n form with Gemini recommendations](templates/seo-page-audit/) | A hosted form that audits any page for 17 on-page SEO checks, scores it 0-100 and asks Gemini for a prioritised fix list with a new title and meta description. | — | [Pro $29](https://payhip.com/b/AMjyN) |
| [Write personalised cold email opening lines for Google Sheets leads with AI](templates/lead-research-cold-email/) | Writes one specific, non-cheesy cold email opening line per lead in your Google Sheet with Gemini. | — | [Pro $24](https://payhip.com/b/ievgI) |
| [Find buyer-intent Reddit posts with AI and send a daily Telegram digest](templates/reddit-intent-leads/) | Finds Reddit posts asking for a tool like yours, ranks them by buying intent with AI and sends one Telegram digest each morning. | — | [Pro $19](https://payhip.com/b/PslpA) |
| [Write product titles, descriptions and tags from photos with Gemini Vision and Google Sheets](templates/product-listing-from-photo/) | Upload a product photo; Gemini Vision writes the title, description and tags for Etsy or Shopify, checks length limits and saves to Sheets. | — | [Pro $19](https://payhip.com/b/semO6) |

### Creators

| Template | What it does | Free n8n.io page | Pro version |
|---|---|---|---|
| [Summarize new YouTube videos from channel RSS feeds with AI and send to Telegram](templates/youtube-ai-digest/) | Checks chosen YouTube channels every morning and sends one Telegram digest with a short AI summary per new video. | [n8n.io](https://n8n.io/workflows/21170) | — |
| [Draft replies to new YouTube comments with Gemini and review them in Google Sheets](templates/youtube-comment-reply-drafts/) | Pulls new comments on your latest uploads and drafts on-brand replies with Gemini for review in Google Sheets. | — | [Pro $19](https://payhip.com/b/HnjXd) |
| [Find trending video ideas for your niche from Google Trends and YouTube with Gemini and Telegram](templates/creator-trend-radar/) | Reads Google Trends and channels you choose each morning; Gemini picks the trends that fit your niche and sends video ideas to Telegram. | — | [Pro $19](https://payhip.com/b/DPNyW) |
| [Write YouTube Shorts, TikTok and Reels scripts from a form with Gemini and Google Sheets](templates/shorts-script-writer/) | Form to ready-to-film Shorts/TikTok/Reels script with Gemini: timed beats, hooks and an automatic length check, saved to Sheets. | — | [Pro $19](https://payhip.com/b/mipKh) |
| [Write podcast show notes, chapters and social posts from new RSS episodes with Gemini and Gmail](templates/podcast-show-notes/) | New RSS episode: Gemini transcribes the audio, writes show notes, chapters and social posts, and emails them to you. | — | [Pro $24](https://payhip.com/b/YeBfF) |

### Careers & job search

| Template | What it does | Free n8n.io page | Pro version |
|---|---|---|---|
| [Track job application emails from Gmail in Google Sheets with AI status detection](templates/job-application-tracker/) | Watches Gmail hourly; Gemini spots emails about your applications and updates one row per company + role in Google Sheets with the latest status. | — | [Pro $15](https://payhip.com/b/d0Ihr) |
| [Score remote job listings against your CV with AI and alert on Telegram](templates/remote-job-matcher/) | Collects remote jobs from Remotive, Remote OK and We Work Remotely, scores each against your CV with AI and alerts the best on Telegram. | [n8n.io](https://n8n.io/workflows/21457) | — |
| [Generate interview questions and STAR answer outlines from a job description and your CV with Gemini](templates/interview-prep-pack/) | Form with a job description and your CV; Gemini predicts likely interview questions and STAR answer outlines. | — | [Pro $15](https://payhip.com/b/S5nj8) |

### Personal productivity

| Template | What it does | Free n8n.io page | Pro version |
|---|---|---|---|
| [Manage Google Calendar and Google Tasks from Telegram text or voice notes with a Gemini agent](templates/telegram-calendar-assistant/) | Talk to your Google Calendar and Google Tasks from Telegram by text or voice note; a Gemini agent reads and creates events and tasks. | — | [Pro $24](https://payhip.com/b/NT1kj) |
| [Track daily habits and mood with Telegram buttons, Google Sheets and a weekly Gemini review](templates/habit-mood-tracker/) | Evening Telegram check-in with Done / Not today buttons per habit and a mood score, saved to Google Sheets with a weekly Gemini review. | — | [Pro $15](https://payhip.com/b/HCBcW) |
| [Send birthday reminders with Gemini gift ideas and message drafts from Google Sheets to Telegram](templates/birthday-gift-reminders/) | Daily check of a birthday sheet; Telegram reminder with Gemini gift ideas within budget and a message draft. | — | [Pro $12](https://payhip.com/b/XnpvB) |
| [Track calories from Telegram meal photos and text with Gemini, daily targets and Google Sheets](templates/meal-photo-calorie-log/) | Telegram food diary: send a meal photo or text, Gemini estimates calories and macros, logs to Google Sheets and tracks daily targets. | — | — |

## Free vs Pro

Everything in this repo is free to use, modify and share (MIT). Most templates also have a **Pro version** sold on [Payhip](https://payhip.com/OllysAutomationTemplates) for people who want the extended build: multi-client or multi-account loops, approval steps, Telegram alerts, weekly reports, error branches and a longer setup guide. The free versions here are complete, working workflows, not crippled demos.

Two of the free templates are also published on the official n8n template library: [YouTube AI digest](https://n8n.io/workflows/21170) and [remote job matcher](https://n8n.io/workflows/21457). Creator profile: https://n8n.io/creators/ollymcbride

## Conventions

- Credentials are never included. Every ID is a `YOUR_...` placeholder.
- AI steps return structured JSON through a Structured Output Parser, so downstream nodes don't break when the model gets chatty.
- Anything that contacts another person (emails to clients, candidates, customers) is a draft or behind an approval step by default.
- Set your timezone in **Workflow settings** so schedules and dates match your day.

## Contributing

Issues and pull requests are welcome: bug reports with your n8n version, fixes for changed node parameters, or new templates that follow the conventions above.

## License

MIT
