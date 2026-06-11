# 🧠 HumanizeAI — AI Text Humanizer & Writing Improver

Transform AI-generated text into natural, human-sounding writing that bypasses AI detection tools and plagiarism checkers.

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![React](https://img.shields.io/badge/React-18-61DAFB) ![Flask](https://img.shields.io/badge/Flask-3.0-green) ![License](https://img.shields.io/badge/License-MIT-yellow)

---

## What It Does

HumanizeAI takes robotic, AI-generated text and rewrites it through a **3-pass humanization pipeline**:

| Pass | Purpose |
|------|---------|
| **1. Deep Rewrite** | Completely restructures sentences, changes word choices, varies paragraph lengths |
| **2. Flow & Variation** | Polishes transitions, fixes repetitive patterns, improves natural rhythm |
| **3. Anti-Detection Sweep** | Final check for AI-telltale patterns, adds subtle human imperfections |

## Features

- **Dual AI Backend** — OpenAI GPT-4o-mini (cloud) or Ollama (local, private)
- **5 Tone Modes** — Natural, Simpler, Academic, Casual, Professional
- **Temperature Control** — Fine-tune creativity vs precision
- **Multi-Pass Processing** — 1 to 3 passes for varying levels of humanization
- **Pass Transparency** — View output from each processing stage
- **Copy to Clipboard** — One-click copy of final result
- **Dark Theme UI** — Modern, responsive React frontend

---

## Quick Start

### Prerequisites

- Python 3.10+
- Node.js 18+
- OpenAI API key (for cloud mode) OR Ollama installed (for local mode)

### 1. Clone & Setup Backend

```bash
cd humanize-ai/backend

# Create virtual environment
python -m venv venv
venv\Scripts\activate    # Windows
# source venv/bin/activate  # macOS/Linux

# Install dependencies
pip install -r requirements.txt

# Configure API key
copy .env.example .env
# Edit .env and add your OPENAI_API_KEY
```

### 2. Setup Frontend

```bash
cd humanize-ai/frontend

npm install
```

### 3. Run

**Terminal 1 — Backend:**
```bash
cd backend
python app.py
# Server starts on http://localhost:5000
```

**Terminal 2 — Frontend:**
```bash
cd frontend
npm start
# Opens browser at http://localhost:3000
```

---

## API Reference

### POST `/api/humanize`

**Request Body:**
```json
{
  "text": "Your AI-generated text here...",
  "provider": "openai",
  "model": "gpt-4o-mini",
  "tone": "natural",
  "temperature": 0.72,
  "passes": 3
}
```

**Response:**
```json
{
  "original": "...",
  "final": "The humanized output text...",
  "passes": [
    { "name": "Deep Rewrite", "output": "..." },
    { "name": "Flow & Variation", "output": "..." },
    { "name": "Anti-Detection Sweep", "output": "..." }
  ]
}
```

| Parameter | Type | Default | Options |
|-----------|------|---------|---------|
| `text` | string | required | — |
| `provider` | string | `"openai"` | `"openai"`, `"ollama"` |
| `model` | string | auto | `"gpt-4o-mini"`, `"mistral"`, `"llama3"` |
| `tone` | string | `"natural"` | `"natural"`, `"simpler"`, `"academic"`, `"casual"`, `"professional"` |
| `temperature` | float | `0.72` | `0.4` – `1.0` |
| `passes` | int | `3` | `1`, `2`, `3` |

### GET `/api/health`

Returns `{ "status": "ok", "version": "1.0.0" }`

---

## Using Ollama (Local Mode)

1. Install Ollama: https://ollama.com
2. Pull a model:
   ```bash
   ollama pull mistral
   # or
   ollama pull llama3
   ```
3. Ollama runs on `http://localhost:11434` by default
4. Select "Ollama" in the UI provider selector

---

## Example Input / Output

**Input (AI-generated):**
> Artificial intelligence has significantly transformed various industries in recent years. Furthermore, it has enabled organizations to automate complex processes and improve efficiency. Moreover, the integration of machine learning algorithms has led to remarkable advancements in data analysis. In addition, natural language processing has revolutionized how humans interact with technology.

**Output (Humanized):**
> AI has honestly changed the game for a lot of industries over the past few years. Companies are automating stuff that used to take entire teams, and it's making things run way smoother. Machine learning, in particular, has gotten really good at crunching data — we can see that in everything from recommendation engines to medical diagnostics. And the way NLP lets us just talk to our devices now? That's something most of us take for granted, but it's a pretty big deal when you think about it.

---

## Project Structure

```
humanize-ai/
├── backend/
│   ├── app.py              # Flask API server
│   ├── humanizer.py         # Multi-pass humanization pipeline
│   ├── model_handler.py     # OpenAI + Ollama unified interface
│   ├── requirements.txt     # Python dependencies
│   ├── .env.example         # Environment variable template
│   └── .env                 # Your local config (gitignored)
├── frontend/
│   ├── package.json
│   ├── public/index.html
│   └── src/
│       ├── App.js           # Main app component
│       ├── App.css           # Full dark theme styles
│       ├── index.js
│       ├── api/humanize.js   # API client
│       └── components/
│           ├── TextInput.js
│           ├── TextOutput.js
│           ├── ModelSelector.js
│           ├── ToneSelector.js
│           └── Controls.js
├── README.md
├── INSTRUCTIONS.md
└── SKILLS.md
```

---

## License

MIT
