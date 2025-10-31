# Chatbot — LangGraph + Google Gemini (Streamlit UI)

Small demo project that wires a LangGraph-based chat backend to Google Gemini (via the
`langchain_google_genai` adapter) and provides a few Streamlit frontends (in-memory and
SQLite-persisted).

## Repository layout

- `langgraph_backend.py` — in-memory LangGraph backend
- `langgraph_backend_database.py` — SQLite-persistent LangGraph backend (uses `chatbot.db`)
- `streamlit_frontend_database.py` — Streamlit UI using the DB-backed backend
- `streamlit_frontend_streaming.py` — simple streaming demo
- `streamlit_frontend_treading.py` — in-memory threaded demo
- `.env` — local env file (DO NOT COMMIT)

## Prerequisites

- Python 3.10+ (virtualenv recommended)
- A Google API key with access to the Generative Models API

## Quick setup (macOS / zsh)

1. Create & activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install required packages (example)

```bash
pip install streamlit python-dotenv langgraph langchain-core langchain-google-genai
```

3. Add your Google API key to a local `.env` file (this repo's `.gitignore` already ignores it)

```
GOOGLE_API_KEY=your_api_key_here
```

## Run the app

- Database-backed UI:

```bash
export GOOGLE_API_KEY="your_api_key_here"  # or rely on .env
streamlit run streamlit_frontend_database.py
```

- Streaming/in-memory demos:

```bash
streamlit run streamlit_frontend_streaming.py
streamlit run streamlit_frontend_treading.py
```

## Notes

- `chatbot.db` is used by the SQLite backend to persist checkpoints. It is ignored by git by
  default in `.gitignore`.
- Do NOT commit `.env` or API keys to GitHub. Rotate keys if they were accidentally exposed.
- If you want reproducible dependencies, create a `requirements.txt` with pinned versions.

## Troubleshooting

- If Streamlit shows stale UI after edits, restart the Streamlit process.
- If LLM calls fail, verify `GOOGLE_API_KEY` and network connectivity.

License: MIT (add a LICENSE file if you want to publish under a specific license)
