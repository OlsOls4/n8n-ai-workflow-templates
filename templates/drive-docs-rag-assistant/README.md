# Chat with your Google Drive documents using Gemini and a free in-memory vector store

## Description (n8n listing)

Chat with the PDFs, Google Docs, Slides and text files in one Google Drive folder. The workflow downloads the files (Google Docs are exported as text), splits and embeds them with Gemini's free embedding model and keeps them in n8n's built-in in-memory vector store, so there is no Pinecone, Supabase or Qdrant to pay for. An AI Agent answers questions in n8n's hosted chat using only what it retrieves, and names the files each answer came from. A daily schedule rebuilds the index so new documents are picked up and a restart never leaves you with an empty store for long.

## Who it's for
- Small teams with an HR handbook, SOPs or policies in Drive
- Consultants and agencies answering the same client questions
- Anyone who wants a first RAG workflow without a vector database bill

## How it works
1. **Index my documents** (button) or **Every day at 6am** lists the folder and keeps supported files.
2. **Download the file** fetches each file; Google Docs/Slides are exported as text, Sheets as CSV.
3. **Store in the in-memory vector store** loads, chunks (1,200 characters, 200 overlap) and embeds the text with Gemini, keeping file name and link as metadata.
4. **When a chat message is received** opens the hosted chat; **Answer from the documents** (AI Agent + memory) searches the store and answers with file names.

## Setup
1. Add **Google Drive OAuth2** and **Google Gemini (PaLM) API** credentials.
2. Put the folder ID (last part of the folder URL) in **Set index settings**.
3. Click **Index my documents** once, then activate the workflow and open the chat trigger's URL.

## Requirements
- n8n 2.x (built and import-tested on n8n 2.43.7). Cloud or self-hosted; built-in nodes only, no community nodes.
- A Google Gemini API key: the free tier at https://aistudio.google.com/app/apikey is enough for normal use. Any other chat model node (OpenAI, Anthropic, Groq, Ollama) can replace the Gemini node.

## Customisation ideas
- Change chunk size and overlap in **Split into chunks**.
- Edit the agent's system message to set tone or language.
- Switch the chat trigger to embedded mode to put the chat on your intranet.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/DpShK
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
