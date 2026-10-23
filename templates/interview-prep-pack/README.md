# Generate interview questions and STAR answer outlines from a job description and your CV with Gemini

## Description (n8n listing)

Most interview prep is guessing. This template turns the job description and your own CV into a focused prep pack in under a minute. Fill in a simple n8n form (role, company, job description, interview type, CV as PDF) and Google Gemini predicts ten likely questions for that interview type, explains why each is asked, and drafts a STAR (Situation, Task, Action, Result) outline using only experience that is actually in your CV.

You also get the five skills to highlight, your likely gaps with how to address them, and five sharp questions to ask the interviewer. The pack appears on the form's result page, ready to copy or print to PDF. Only one credential is needed: a free Gemini API key.

## Who it's for
- Job seekers preparing for screens, hiring-manager rounds and finals
- Graduates and career changers
- Career coaches who want a fast first draft for clients

## How it works
1. **Interview details form** collects job title, company, job description, interview type and CV (PDF).
2. **Extract text from CV** reads the PDF.
3. **Write interview prep pack** (Basic LLM Chain + Gemini + Structured Output Parser) returns role summary, questions with reasons and STAR outlines, skills to highlight, gaps and questions to ask. The prompt forbids invented employers, numbers or projects and addresses you directly.
4. **Format prep pack** renders HTML and **Show prep pack** displays it.

## Setup
1. Get a free key at https://aistudio.google.com/app/apikey and add a **Google Gemini (PaLM) API** credential on the chat model.
2. Activate the workflow.
3. Open the Form Trigger's Production URL, fill it in and read your pack.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key (free tier at https://aistudio.google.com/app/apikey is enough for normal use)

## Customisation ideas
- Change the number or mix of questions in **Write interview prep pack**.
- Add fields for the interviewer's role or the team to sharpen questions.
- Swap Gemini for any chat model node.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($15, extra features listed on the page): https://payhip.com/b/S5nj8
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
