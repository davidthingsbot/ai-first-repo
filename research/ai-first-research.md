# AI-First Research Repositories

A pattern for structuring research repositories where humans and AI coding agents collaborate on data analysis, experimentation, and knowledge accumulation.

---

## The Core Architecture

```
repo/
├── AGENTS.md           # Instructions for AI assistants
├── README.md           # Human-oriented overview
├── HISTORY.md          # Development log (decisions, milestones)
├── FUTURE.md           # Ideas for future work
├── RUNS.md             # Index of all runs with key outcomes
│
├── input/              # Raw data (immutable)
│   ├── dataset-A/
│   │   ├── README.md   # What this data is, how it was collected
│   │   └── *.csv
│   └── dataset-B/
│
├── library/            # Accumulated knowledge
│   ├── research/
│   │   ├── problem_statement.md
│   │   ├── findings/   # Discoveries from runs
│   │   └── datasets/   # Dataset documentation
│   └── scripts/        # Reusable analysis templates
│
└── runs/               # Individual experiments
    ├── 2026-03-06_initial/
    ├── 2026-03-11_followup/
    └── ...
```

---

## The Three Zones

### 1. Input (Raw Data)

The `input/` directory holds **immutable source data**. Each dataset is a subdirectory with:

- **README.md** — Provenance, collection protocol, known issues
- **Raw files** — CSVs, logs, whatever was collected

**Rules:**
- Never modify raw data — it's the ground truth
- Every dataset must be documented (if undocumented, flag it and create a README)
- Date-label datasets for clarity

### 2. Library (Accumulated Knowledge)

The `library/` directory is the **knowledge base** that grows over time:

- **research/** — Problem statements, findings, theoretical background
- **scripts/** — Reusable analysis templates that runs can adapt
- **[domain-specific]/** — Device docs, reference material, etc.

**Rules:**
- Library content is **promoted from runs** (not written directly)
- Findings are extracted and generalized after runs complete
- Templates improve incrementally as runs reveal better patterns

### 3. Runs (Experiments)

The `runs/` directory contains **individual research experiments**. Each run is a **forward-flowing data pipeline**:

```
00_research_plan/       # What we're investigating and why
01_ingress/             # Load and clean raw data
02_data_review/         # Quality checks, visualizations
03_analysis/            # Core analysis (varies by run)
...
N_summary/              # Final synthesis
N+1_contribute_back/    # Promote findings to library (MANDATORY)
```

---

## The Run Architecture

### Numbered Stages

Each stage is **self-contained** with:

| Output | Purpose |
|--------|---------|
| `script.py` | Analysis code |
| `test_script.py` | Tests (written first!) |
| `summary.md` | Stage report with inline plots |
| `summary.pdf` | Generated PDF for sharing |
| `*.png` | Visualizations |
| `*.csv` | Data outputs |

**Data flows forward only** — Stage 3 can read from Stage 2, but never writes back.

### Stage 0: Research Plan (Mandatory)

Before any analysis, document:

1. **Background & Motivation** — Why this run matters
2. **Dataset Description** — What data, how collected, known issues
3. **Research Questions** — Specific, numbered, answerable
4. **Hypotheses** — Expected outcomes
5. **Analysis Plan** — Stage sequence and methods
6. **Success Criteria** — How we'll know if it worked

### Stage N+1: Contribute Back (Mandatory)

Every run must end with a **contribute back** stage:

- Identify novel findings → promote to `library/research/findings/`
- Improve templates → update `library/scripts/`
- Document datasets → add to `library/research/datasets/`
- Capture future ideas → append to `FUTURE.md`

**This is how the library grows.** Without it, knowledge stays trapped in individual runs.

---

## Interactive Checkpoints

The AI assistant works **interactively**, not autonomously. After every stage:

```
✅ STAGE X COMPLETE: [Stage Name]
==================================

Key Findings:
  • [Finding 1]
  • [Finding 2]

⚠️  Surprises / Concerns:
  • [Issue] — [recommendation]

📋 Next: Stage Y: [purpose]

❓ Ready to proceed?

[WAIT FOR USER RESPONSE]
```

**Never batch multiple stages.** Always wait for human approval before proceeding.

---

## Test-Driven Development

For scientific code, **write tests before implementation**:

1. **Write the test** — Define expected inputs and outputs
2. **Run the test** — Confirm it fails
3. **Write the implementation** — Make it pass
4. **Run all tests** — Confirm nothing broke

This catches data assumptions early and prevents silent numerical errors from propagating.

---

## Documentation as First-Class Output

Every stage produces documentation, not just code:

- **summary.md** — What was done, what was found, what it means
- **Inline plots** — Charts embedded where discussed (not dumped at the end)
- **PDF generation** — Shareable reports for stakeholders

The run should be **readable as a narrative** — someone reviewing later can understand the full story without re-running code.

---

## The Knowledge Flywheel

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│    INPUT ──────► RUNS ──────► LIBRARY                       │
│      │            │              │                          │
│      │            │              │                          │
│      │            └──────────────┘                          │
│      │                   ▲                                  │
│      │                   │ (templates, findings             │
│      │                   │  inform future runs)             │
│      │                   │                                  │
│      └───────────────────┘                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

- **Runs consume** input data and library knowledge
- **Runs produce** findings that flow back to the library
- **Future runs** benefit from accumulated knowledge
- **The library compounds** over time

---

## Key Files

| File | Purpose |
|------|---------|
| `AGENTS.md` | Detailed instructions for AI assistants — the "how to work here" guide |
| `README.md` | Human-oriented overview |
| `HISTORY.md` | Chronological log of decisions and milestones |
| `FUTURE.md` | Ideas sparked by runs, not yet pursued |
| `RUNS.md` | Index of all runs with purpose and key outcomes |

---

## Why This Works

1. **Separation of concerns** — Raw data, accumulated knowledge, and experiments live in distinct zones
2. **Forward-flowing pipelines** — Each stage builds on the last, no circular dependencies
3. **Interactive checkpoints** — Human stays in control, AI handles execution
4. **Mandatory contribute-back** — Knowledge accumulates instead of staying siloed
5. **Test-driven development** — Scientific code gets the rigor it deserves
6. **Documentation throughout** — The repo tells its own story

---

## Getting Started

1. Create the directory structure above
2. Write your `AGENTS.md` with domain-specific instructions
3. Add your first dataset to `input/` with a README
4. Bootstrap a run with `00_research_plan/`
5. Work through stages interactively with your AI assistant
6. Contribute findings back to `library/`
7. Index the run in `RUNS.md`

Repeat. The library grows. Future runs get easier.

---

*This pattern emerged from real research collaboration between humans and AI coding agents. It's designed to make that collaboration productive, traceable, and accumulating.*
