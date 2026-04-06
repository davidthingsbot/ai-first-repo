# AI-First Pattern: Simple Web Product

A lightweight repository pattern for building a small web product with an AI coding agent and a human operator.

This pattern is for cases like:
- a single-page app + small backend
- a marketing site + lightweight API
- a prototype that should be deployable and maintainable

The goal is to make the repo *self-driving* for an agent:
- clear boundaries
- obvious commands
- durable context in files
- safe secrets handling

---

## 1) Repository layout

A simple, durable layout:

```
.
├── README.md
├── AGENTS.md
├── docs/
│   ├── product.md
│   ├── architecture.md
│   └── decisions.md
├── frontend/
├── backend/
├── infra/
│   ├── docker-compose.yml
│   └── deploy.md
├── scripts/
└── .gitignore
```

Variations:
- If there is no backend, omit `backend/`.
- If you’re serverless-only, `infra/` becomes the main deploy surface.

---

## 2) Files that make it AI-first

### README.md (human entrypoint)
Should answer:
- what is this?
- how to run it locally?
- how to deploy?
- where are the docs?

### AGENTS.md (agent entrypoint)
Should include:
- the exact dev commands to run
- code style rules
- how to run tests/linters
- what not to touch (secrets, prod data)
- how to add features safely (branching/PR expectations)

### docs/product.md
- target user
- jobs-to-be-done
- core flows
- what “done” means

### docs/architecture.md
- what talks to what
- data storage
- auth model
- key tradeoffs

### docs/decisions.md
- short decision log (what changed and why)

---

## 3) Dev environment and reproducibility

Pick one of these and commit it:

- **Docker Compose** (recommended for multi-service)
- **devcontainer** (VS Code / Cursor)
- **Makefile** (simple command aliases)

The agent should be able to do:

```bash
# one-time
./scripts/bootstrap.sh

# run
./scripts/dev.sh

# test
./scripts/test.sh
```

Even if those scripts are small wrappers, they reduce ambiguity.

---

## 4) Secrets and configuration (hard rule)

- Put secrets in `.env` / `config.local.*`
- Commit a `.env.example`
- Add real secret files to `.gitignore`

The agent should never invent or hardcode secrets.

---

## 5) Quality gates

Minimum viable gates:
- formatter (prettier/ruff/gofmt/etc.)
- linter
- tests (even a small smoke test)

If you use CI, include a single pipeline that runs:
- install
- lint
- test
- build

---

## 6) Deployment

Keep it boring.

- Document one blessed deployment path in `infra/deploy.md`.
- Prefer immutable builds (build once, run many).
- Record environment variables and required external resources.

---

## 7) Whiteboard relevance (optional)

This pattern maps well to “rooms as repos”:
- the room contains `docs/` (intent)
- the repo contains `code/` (implementation)
- the commit history contains “why” (decisions)

An agent can operate safely because the repo tells it:
- what commands are allowed
- where state lives
- how to verify changes
