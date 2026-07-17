# Guardian — EHS Assistant

A single-file, client-side EHS assistant: incident triage, near miss, first aid,
risk assessment, compliance, and a digital **Permit to Work** (fill → AI review →
print). It works **offline out of the box** and can optionally connect to Claude,
any free/OpenAI-compatible LLM, or a local Ollama model.

Everything runs in the browser. No backend, no build step, no server. Any API key
you enter is stored only in your browser (`localStorage`) and is never committed to
the repo.

---

## Deploy to GitHub Pages (about 2 minutes)

### Option A — its own repo
1. Create a new repository (e.g. `guardian`).
2. Add **`index.html`** to the repository root and commit.
3. Repo **Settings → Pages** → *Build and deployment* → **Deploy from a branch** →
   Branch: `main`, Folder: `/ (root)` → **Save**.
4. Wait ~1 minute. Your site is live at
   `https://<your-username>.github.io/guardian/`.

### Option B — inside your existing `username.github.io` site
1. In your `username.github.io` repo, create a folder, e.g. `guardian/`.
2. Put **`index.html`** inside it and commit.
3. It's live at `https://<your-username>.github.io/guardian/`
   (Pages is already enabled for this repo).

The page uses only relative paths and a Google Fonts CDN, so it works at any
sub-path without changes.

---

## Connecting a model (optional)

Open **Settings** (gear, bottom-left) and pick a provider. Use **Test connection**
to confirm it works before relying on it.

| Provider  | Cost        | Setup |
|-----------|-------------|-------|
| **Offline** (default) | Free | Nothing — built-in EHS reference library |
| **Claude** | Paid | Anthropic API key from console.anthropic.com |
| **Free LLM** | Free tiers | Any OpenAI-compatible API — **OpenRouter** (has `:free` models) or **Groq** (`https://api.groq.com/openai/v1`) |
| **Ollama** | Free, private, offline | Run a model locally (see below) |

### Running the local Ollama option
1. Install from https://ollama.com, then `ollama pull llama3.1`.
2. Start it so the browser is allowed to reach it:
   - macOS/Linux: `OLLAMA_ORIGINS='*' ollama serve`
   - Windows: set env var `OLLAMA_ORIGINS` = `*`, then relaunch Ollama.
   - To lock it down, use your site's origin instead of `*`, e.g.
     `OLLAMA_ORIGINS=https://<your-username>.github.io`.
3. In Settings → Ollama, Base URL `http://localhost:11434/v1` (or
   `http://127.0.0.1:11434/v1`), model `llama3.1`, then **Test connection**.

> A browser can reach `http://localhost` from an HTTPS Pages site in Chrome. If a
> request fails with *"Failed to fetch"*, it's almost always the `OLLAMA_ORIGINS`
> setting above. Note that any in-app/preview sandbox cannot reach your localhost —
> test on the deployed page.

---

## Privacy
- No analytics, no tracking, no backend.
- API keys and your conversation stay in your browser only.
- Offline mode and the risk-matrix / permit tools need no connection at all.

## Note
Guardian is decision-support, not a substitute for a qualified professional,
site-specific procedures, or legal advice. Offline answers are concise
best-practice summaries — verify against the current regulation for your
jurisdiction.
