# ⚠️ PCB Red Flag Scanner

> Find manufacturability issues before they cost you time and money.

**PCB Red Flag Scanner** is a free DFM/DFA tool for hardware engineers and PMs. Describe your PCB design and get an instant analysis of the most common production, assembly and reliability issues — categorized by severity.

🌐 **Live:** [kathegrima.github.io/pcb-redflag-scanner](https://kathegrima.github.io/pcb-redflag-scanner)  
🌍 **Available in:** Italian 🇮🇹 · English 🇬🇧

---

## What it does

Paste a description of your PCB (layers, dimensions, connectors, components, manufacturer) and get a structured analysis:

- 🔴 **Critical** — blocks production or causes field failure
- 🟡 **Serious** — increases cost or defect rate
- 🟢 **Improvable** — best practice recommendations

For each issue: what's wrong · why it's a problem · how to fix it.

---

## How it works

1. User describes the PCB and optional context (units, budget, manufacturer)
2. Frontend sends data to a **Cloudflare Worker**
3. Worker calls **Google Gemini 2.5 Flash-Lite** with a DFM-specific prompt
4. Analysis is returned in the selected language

---

## Stack

| Layer | Technology |
|---|---|
| Hosting | GitHub Pages |
| Frontend | Vanilla HTML + CSS + JS (zero dependencies) |
| Backend / Proxy | Cloudflare Workers (free tier) |
| AI | Google Gemini 2.5 Flash-Lite |
| Font | Space Mono (Google Fonts) |

---

## Repository structure
/
└── index.html # Full frontend — single file, no build step

---

## Deploy

### 1. Fork and enable GitHub Pages
1. Fork this repository
2. Go to **Settings → Pages** → Source: `main` / `root`
3. Live at `https://yourusername.github.io/pcb-redflag-scanner`

### 2. Create the Cloudflare Worker
1. Sign up at [cloudflare.com](https://cloudflare.com)
2. **Workers & Pages → Create → Start with Hello World**
3. Name it `pcb-redflag`
4. Replace the default code with the Worker below
5. Click **Save and deploy**

### 3. Add the Gemini API key
1. Get a free key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. In your Worker: **Settings → Variables and Secrets → Add**
   - Name: `GEMINI_API_KEY`
   - Type: **Secret**
   - Value: your `AIza...` key

### 4. Connect Worker to frontend
In `index.html`, update:
```javascript
const WORKER_URL = 'https://pcb-redflag.your-account.workers.dev/';


