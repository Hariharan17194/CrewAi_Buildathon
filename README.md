# CrewAI Amazon Customer Support Agent

A multi-agent customer support assistant built with [CrewAI](https://github.com/crewAIInc/crewAI) that answers Amazon-style customer queries using Retrieval-Augmented Generation (RAG) over an uploaded knowledge base, with a live web search fallback.

## How it works

1. **RAG knowledge base** — Upload a `.txt` file of customer support content (FAQs, policies, refund/return rules, etc.). It's chunked, embedded with OpenAI embeddings, and indexed in a local FAISS vector store (`support_core.py`).
2. **Web search** — A DuckDuckGo-powered search tool answers questions the knowledge base doesn't cover.
3. **Agents**:
   - **CLI** (`Customer_support.py`) — a single agent that checks the knowledge base first and only falls back to the web if needed, returning one combined answer.
   - **Web UI** (`app.py`) — two agents running in parallel: one strictly on the knowledge base, one strictly on web search, so both answers are shown side by side.

## Setup

```bash
python -m venv venv
venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

Copy `.env.example` to `.env` and add your OpenAI API key:

```
OPENAI_API_KEY=your-openai-api-key
```

## Usage

**Command line:**

```bash
python Customer_support.py
```

Press Enter to use the bundled sample data (`data/amazon_customer_support.txt`), or pass your own `.txt` file path.

**Web UI (Streamlit):**

```bash
streamlit run app.py
```

Upload your own `.txt` knowledge base file from the sidebar, or use the default Amazon support sample. Ask a question and see the knowledge-base-only answer and the web-search-only answer side by side.

## Project structure

```
support_core.py   # shared RAG index, tools, and agent definitions
Customer_support.py  # CLI entry point
app.py                # Streamlit web UI
data/                  # sample knowledge base (.txt)
requirements.txt
.env.example
```
