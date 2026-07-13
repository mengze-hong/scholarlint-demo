# ScholarLint — LaTeX Pre-Submission Integrity Checker

Upload a LaTeX project ZIP and get strict, rule-based **plus** LLM-assisted checks before you submit to a conference or journal. ScholarLint catches the mistakes that lead to desk rejects: broken citations, fabricated/mismatched references, numbers in the text that don't match the tables, missing figure labels, and structural gaps.

## 🌐 Live Demo

### **http://120.92.88.223:8088**

No installation needed — open the link, drag in a LaTeX `.zip`, and review the integrity report. Core checks run instantly and require **no API key**.

> **AI features (optional):** Simulate Review, AI Fix, Polish, Abstract optimization, and LLM-assisted data-claim grounding use a **Bring-Your-Own-Key** model. Click **⚙️ AI Key** in the top bar and paste your own OpenAI-compatible **API key + Base URL + Model**. It is stored **only in your browser** (localStorage) and sent directly with each request — never saved on the server. Reviewers who just want the core integrity report can skip this entirely.

## What It Checks (6 gates)

| Gate | What it catches |
|------|-----------------|
| **Structure** | Missing sections, document skeleton problems |
| **Citations** | `\cite{key}` with no matching `.bib` entry (→ `[?]` in the PDF), orphaned/duplicate keys |
| **References** | Fabricated or mismatched references, unresolvable DOIs, retractions — verified against Crossref / Semantic Scholar / OpenAlex / DBLP / ACL Anthology. **AI never invents references, DOIs, authors, titles, or years.** |
| **Figures/Tables** | Floats never referenced in text, missing `\label` |
| **Data integrity (NCG)** | Numbers claimed in prose that don't match the corresponding table cells (LLM extracts structured claims → rules verify against cells) |
| **Writing** | Long sentences, structural and clarity signals |

Commented-out LaTeX is never flagged. Strict by design: false positives are acceptable, missed integrity issues are not.

## How Reviewers Use It

1. Open **http://120.92.88.223:8088**
2. Drag in a LaTeX project `.zip` (main `.tex` + `.bib` + figures)
3. Read the **Integrity Report**: overall score, per-gate pass/fail, and a multi-dimensional (Novelty / Soundness / Clarity / Significance) heuristic
4. Enter the **Workspace** to click any issue and jump to the exact line, apply fixes, re-check, and download the fixed ZIP
5. *(Optional)* Set your own AI key via **⚙️ AI Key** to unlock Simulate Review, AI Fix, Polish, and Abstract optimization

## Run It Yourself

### Local (Python 3.11+)

```bash
python -m venv .venv
source .venv/bin/activate            # Windows: .venv/Scripts/activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Open `http://localhost:8000`. No API key required for core checks; set your own key in-app for AI features.

### Docker

```bash
docker compose up -d --build         # http://localhost:8000
```

For a public deployment (self-contained overlay, maps host port 8088):

```bash
docker compose -f docker-compose.deploy.yml up -d --build
```

Create a `.env` (see `.env.example`) — for a BYOK demo you can leave all `LLM_*` blank; the server needs no key.

## Tech Stack

FastAPI · SQLite · single-page HTML/JS frontend (CodeMirror editor) · OpenAI-compatible LLM client · Docker.

## Privacy & Security

- Your LLM API key lives only in your browser and is sent per-request — the server never stores it.
- Uploaded papers, reports, and secrets are never committed to this repository.
- AI outputs are **suggestions that require human verification**; reference-authenticity checks never call an LLM, so citations can't be fabricated.

---

*Results and AI suggestions are for reference only and may contain false positives/negatives. Not academic or legal advice — final requirements follow your target venue.*
