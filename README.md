# Homepage Pet Evolution System

A personal-brand AI companion system that lives on [yuanzehua.me](https://yuanzehua.me), evolving through real visitor feedback, AI-generated candidates, and structured evaluation loops.

## What Is This

This is not a pet avatar project. It is a **product experiment**: I applied the same methodology I use for AI products — hypothesis, measurement, iteration — to a tiny companion character on my personal homepage.

The companion is called **Loopi**. Its origin comes from my Chinese zodiac sign (horse), but it is designed as a virtual AI companion avatar, not a literal pony. It symbolizes momentum, curiosity, growth, and continuous iteration.

The key idea: Loopi does not evolve because a new image looks prettier. It evolves because feedback, evaluation, or a clear product diagnosis shows that a change improves its homepage role while preserving brand identity.

## Live

- Homepage: [yuanzehua.me](https://yuanzehua.me) — Loopi display with compact feedback status
- Pet Lab: [yuanzehua.me/pet-lab/](https://yuanzehua.me/pet-lab/) — evolution dashboard, evaluation model, and candidate queue

## Architecture

```
homepage-pet-loop/
├── pet-loop/                    # Evolution system core
│   ├── pet-dna.md               # Stable identity, visual DNA, red lines
│   ├── versions/                # Version records (v0.1, v0.2, ...)
│   ├── candidates/              # Candidate records with generation prompts
│   ├── reports/                 # Iteration reports with feedback analysis
│   ├── feedback/                # Public-safe feedback snapshots
│   ├── evaluations/             # Rule-based iteration decisions
│   ├── generations/             # Candidate batch metadata
│   ├── selections/              # Staging recommendations
│   ├── rules/                   # Evolution thresholds and guardrails
│   ├── prompts/                 # Agent prompts (generation, selection, reporting)
│   └── db/
│       └── schema.sql           # Cloudflare D1 schema
│
├── pet-lab/
│   └── index.html               # Pet Lab dashboard page
│
├── assets/
│   ├── images/pets/loopi/       # Version images (source PNG + optimized WebP)
│   └── pet-feedback.js          # Frontend feedback submit & summary loading
│
├── functions/api/               # Cloudflare Pages Functions
│   ├── pet-feedback.js          # Public feedback submit API
│   ├── pet-feedback-summary.js  # Public aggregate summary API
│   └── pet-feedback-export.js   # Admin-only raw export API
│
├── scripts/
│   ├── run-pet-evolution-loop.js        # Full four-agent loop
│   ├── run-pet-feedback-collector.js    # Feedback Collector Agent
│   ├── run-pet-evaluation.js            # Evaluation Agent
│   ├── run-pet-generation.js            # Generation Agent
│   ├── run-pet-selection.js             # Selection Agent
│   └── generate-pet-report.js           # Legacy report helper
│
├── docs/
│   ├── pet-database-setup.md    # D1 setup guide
│   └── pet-evolution-loop.md    # Loop workflow guide
│
├── .github/workflows/
│   └── pet-evolution-loop.yml   # Weekly / manual scheduled loop
│
└── agent.md                     # Full system agent guide
```

Deliberately simple MVP:

- Static HTML pages (no framework)
- Cloudflare Pages Functions for feedback API
- Cloudflare D1 for feedback storage (one table)
- All version control, candidate prompts, and Pet DNA in git

## How the Loop Works

**Step 1 — Collect Feedback.** Visitors rate Loopi on an 8-question survey covering four dimensions: visual first impression, homepage fit, personal temperament match, and the pony + puppy concept hybrid. Each question is 1-5 scale.

**Step 2 — Evaluate.** The Evaluation Agent reads scores, computes question and dimension averages, checks red lines, and decides whether to keep, watch, or generate candidates.

**Step 3 — Generate Candidates.** When a dimension underperforms, the Generation Agent creates exactly three candidates, each changing only 1-2 visual variables and naming which survey question it targets.

**Step 4 — Select & Review.** The Selection Agent checks candidates against red lines, Pet DNA consistency, homepage fit, and animation feasibility. Human approval is required before homepage production.

**Step 5 — Deploy.** New versions go to Pet Lab first (staging). Only after explicit approval do they replace the homepage image.

## Evaluation Model

The 8-question survey measures four dimensions:

| Dimension | Questions | What It Tests |
|---|---|---|
| A. Visual First Impression | Q1, Q2 | Is Loopi good-looking and professionally polished? |
| B. Homepage Fit | Q3, Q4 | Does Loopi belong on yuanzehua.me without stealing attention? |
| C. Personal Temperament | Q5, Q6 | Does Loopi convey curiosity, warmth, and approachability? |
| D. Pony + Puppy Concept | Q7, Q8 | Can visitors read the hybrid zodiac-horse + ENFP-dog identity? |

Red lines: homepage fit and visual first impression must stay above 3.5, the hybrid pony/dog concept must stay readable, and Pet DNA must not drift.

## Current Status

- **Active version:** `loopi_v0_2` (Companion)
- **v0.1** was a four-legged pony — feedback said "too animal-like"
- **v0.2** shifted to a standing virtual companion with pony-origin energy in the hair and tail, plus subtle ENFP puppy warmth
- **Latest feedback snapshot:** 36 public feedback rows, average score 4.03
- **Latest loop decision:** generate v0.3 candidates and stage the conservative repair candidate
- **Recommended staging candidate:** `loopi_v0_3_auto_20260616_c01`
- **Recommended v0.3 variables:** forward stance + material finish

## Running The Loop

Run the full four-agent workflow:

```bash
node scripts/run-pet-evolution-loop.js loopi_v0_2
```

Run with protected raw export access:

```bash
PET_ADMIN_TOKEN=your-token node scripts/run-pet-evolution-loop.js loopi_v0_2
```

Run individual agents:

```bash
node scripts/run-pet-feedback-collector.js loopi_v0_2
node scripts/run-pet-evaluation.js loopi_v0_2
node scripts/run-pet-generation.js loopi_v0_2
node scripts/run-pet-selection.js loopi_v0_2
```

The scheduled GitHub workflow can run weekly or manually from GitHub Actions. Add `PET_ADMIN_TOKEN` as a GitHub secret if protected export access is needed. Without it, the loop still works from public aggregate feedback.

## Dynamic Loopi Direction

The recommended animation path is a lightweight 3D-style spritesheet, not a full realtime 3D model:

```text
static Loopi image
→ multi-state spritesheet
→ CSS/JS frame animation
→ homepage state machine
→ visitor feedback
→ evolution loop
```

The first animated MVP should prioritize `idle`, `wave`, `thinking`, `happy`, and a static fallback. Animation should remain calm enough for a professional personal homepage.

## Vibe Coding Workflow

This entire system was built using a Vibe Coding workflow:

- Product ideas went from concept to running demo through Figma, Codex, and MCP tools
- The Pet Lab page, feedback API, database schema, and agent prompts were all iterated through natural-language-driven development
- Version control and candidate management stay in git, keeping the loop transparent and auditable

The point is not just that a pet exists on a homepage — it is that the **process of building and iterating it** is itself a demonstration of how I approach AI-native product work.

## Tech Stack

- HTML / CSS / Vanilla JS
- Cloudflare Pages + Pages Functions
- Cloudflare D1 (SQLite)
- Git-based version & candidate management

## License

MIT
