# Customer Support RAG Chatbot (Telegram + n8n)

A fully automated RAG (Retrieval-Augmented Generation) chatbot built with n8n that answers customer questions on Telegram using your own business documents.

---

## How It Works

Two separate pipelines in one workflow:

**Pipeline 1 — Document Upload**
```
Web Form (file upload)
      ↓
OpenAI Embeddings (converts text to vectors)
      ↓
Pinecone Vector Store (stores knowledge base)
```

**Pipeline 2 — Customer Chat**
```
Telegram Message
      ↓
AI Agent (GPT-5-nano + memory per user)
      ↓
Vector Store Search (finds relevant answer from docs)
      ↓
Telegram Reply
```

---

## Features

- **RAG-powered answers** — AI only answers from your uploaded documents, not general knowledge
- **Per-user memory** — each customer has their own conversation history (session by Telegram user ID)
- **Simple upload form** — non-technical staff can update the knowledge base via a web form
- **Fully automated** — zero human involvement after setup

---

## Tech Stack

| Tool | Purpose |
|---|---|
| n8n | Workflow automation |
| OpenAI (GPT-5-nano) | Language model + embeddings |
| Pinecone | Vector database (knowledge storage) |
| Telegram Bot API | Customer-facing chat interface |

---

## Setup

### 1. Import Workflow
- Open n8n → **Import from file** → select `workflow.json`

### 2. Add Credentials
You need three credentials in n8n:

| Credential | Where to get |
|---|---|
| OpenAI API Key | platform.openai.com |
| Pinecone API Key | app.pinecone.io |
| Telegram Bot Token | @BotFather on Telegram |

### 3. Configure Pinecone
- Create an index named `rag` in your Pinecone dashboard
- Dimensions: `1536` (OpenAI embeddings)
- Metric: `cosine`

### 4. Upload Your Documents
- Open the form URL (from the `On form submission` node)
- Upload your business PDF/docs
- Data is embedded and stored in Pinecone automatically

### 5. Activate Workflow
- Toggle the workflow **Active** in n8n
- Send a message to your Telegram bot — it will answer from your documents

---



---

## Use Cases

- E-commerce customer support (product info, policies)
- Restaurant menu & reservation bot
- Clinic FAQ bot (services, timings, pricing)
- Any business with repetitive customer queries

---

## License

MIT — free to use and modify.
