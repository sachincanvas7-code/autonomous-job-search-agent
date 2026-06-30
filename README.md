# Autonomous Job Search AI Agent

> A build-it-yourself project. An agent that takes a resume, searches the web for
> matching jobs, reads and judges each one for fit, and emails a shortlist —
> deciding its own steps along the way.

**Stack:** Python · Streamlit · OpenAI (function calling)
**Source:** Curious PM — Stay Curious: AI Agents & SDKs

---

## What I'll learn
- What actually makes an "agent": a loop where the model picks tools and decides when to stop
- Defining custom tools (web search, scrape, analyze, parse resume, send email)
- The hard parts: graceful tool-failure handling, infinite-loop prevention, context across steps
- Balancing autonomy vs. user control

## Architecture (files I'll build)
| File | Role |
|------|------|
| `config.py` | Load API keys from environment (never hardcode) |
| `tools.py` | The tool functions the agent can call |
| `prompts.py` | System prompt + tool definitions |
| `agent.py` | The agentic loop: call model → run tool → repeat → stop |
| `app.py` | Streamlit UI that streams the agent's reasoning live |

## Build progression (each step = one commit)
- [ ] **Step 1 — config + keys** from env (`.env.example` provided)
- [ ] **Step 2 — one tool** (web search) and a single model call that uses it
- [ ] **Step 3 — the loop:** let the model chain tool calls until done
- [ ] **Step 4 — more tools:** scrape, analyze fit, parse resume, send email
- [ ] **Step 5 — guardrails:** max iterations, error handling, stop conditions
- [ ] **Step 6 — Streamlit UI** with live reasoning log

## Setup
```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env   # add MY OWN keys — see .env.example
streamlit run app.py
```

> ⚠️ Keys live in environment variables only. Never commit real keys.

## Ship it
Deploy on **Streamlit Community Cloud** (set secrets in the dashboard) or Fly.io.
Public URL + demo video go in the portfolio.

## CI/CD — how deployment works
Platform-native Git integration on **Streamlit Community Cloud** — no pipeline file:

```
git push → GitHub → Streamlit Cloud detects the push → app redeploys automatically
```

One-time setup: create the app on share.streamlit.io pointing at this repo / branch /
`app.py`, then add keys under **Settings → Secrets** (never commit keys — they load from
env via `config.py`). Every push to `main` redeploys on its own.

---
*Starter scaffold. The implementation is mine, committed step by step.*
