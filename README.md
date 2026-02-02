# SDD + OpenSpec + Agents — Project Template

This repository is a **public template** for building software using **Strict Spec-Driven Development (SDD)** powered by **OpenSpec** and **AI Agents**.

It is designed to make **behavior-first development** repeatable, auditable, and compatible with AI-assisted workflows (Cursor, ChatGPT, etc.).

---

## What This Template Is

This project enforces a **non-negotiable development flow**:

```
PROPOSAL
   ↓
SPECS (behavior)
   ↓
TEST CONTRACT (executable contract)
   ↓
TASKS (execution plan)
   ↓
IMPLEMENTATION (code)
   ↓
ARCHIVE (source of truth)
```

Key properties:

* Specs define **what the system does**, never how
* Tests are **contracts**, not examples
* Code exists **only** to satisfy tests
* No implicit decisions
* No speculative design
* No shortcuts

---

## What This Template Is NOT

❌ Not a framework
❌ Not a coding style guide
❌ Not an architecture reference
❌ Not tied to any language or stack

This repo intentionally avoids:

* APIs
* Databases
* Frameworks
* Infrastructure
* Performance tuning
* “Best practices” without specs

---

## Core Principles

* **No code without a spec**
* **No tests without a spec**
* **No tasks without tests**
* **Specs are the source of truth**
* **Tests are executable contracts**
* **Tasks describe behavior, not solutions**
* **AI agents must respect role boundaries**

---

## Repository Structure

```text
.
├── openspec/
│   ├── specs/                 # Source of truth (current system behavior)
│   │   └── <domain>/spec.md
│   ├── changes/               # Active changes (one folder per change)
│   │   ├── <change-name>/
│   │   │   ├── proposal.md
│   │   │   ├── design.md      # Optional
│   │   │   ├── tasks.md
│   │   │   ├── specs/
│   │   │   └── TEST_CONTRACT.md
│   │   └── archive/           # Completed & merged changes
│   └── specs/config.yaml      # Project rules (enforced by agents)
│
├── contracts/                 # Test contracts (if separated)
├── src/                        # Implementation (language-agnostic)
├── tests/                      # Automated tests
└── .cursor/
    └── agents.md               # AI agent role definitions
```

---

## Required Tooling

* **Node.js 20+**
* **OpenSpec CLI**

Install OpenSpec globally:

```bash
npm install -g @fission-ai/openspec@latest
```

---

## Quick Start (New Project)

### 1. Initialize OpenSpec

```bash
openspec init
```

This creates the `openspec/` directory and loads project rules.

---

### 2. Start a New Change

```bash
/opsx:new <change-name>
```

Example:

```bash
/opsx:new order-processing
```

This creates:

```text
openspec/changes/order-processing/
```

---

## The Agent-Based Workflow

This template assumes **four explicit AI agents**, each with strict responsibilities.

Their rules are defined in:

```
.cursor/agents.md
openspec/specs/config.yaml
```

### Agent 1 — Spec Refiner

**Purpose:** Define behavior

Produces:

```
openspec/changes/<change>/specs/<domain>/spec.md
```

Rules:

* Plain language only
* GIVEN / WHEN / THEN
* Deterministic outcomes
* Explicit “The system does NOT” section
* No implementation details

If behavior is unclear → **STOP**

---

### Agent 2 — Test Synthesizer

**Purpose:** Convert specs into a contract

Produces:

```
openspec/changes/<change>/TEST_CONTRACT.md
```

Rules:

* One test per scenario (minimum)
* No new behavior
* No technical references
* Deterministic results

If a scenario cannot be tested → **STOP**

---

### Agent 3 — Task Planner

**Purpose:** Define execution steps

Produces:

```
openspec/changes/<change>/tasks.md
```

Rules:

* Derived strictly from Test Contract
* One task = one verifiable capability
* No files, functions, or frameworks
* No design decisions

If a task implies design → **STOP**

---

### Agent 4 — Implementer

**Purpose:** Write code

Rules:

* Do not modify specs, tests, or tasks
* Implement the minimum to pass tests
* Stop once tests pass
* No refactors unless required by tests

---

## Implementing a Change

Once all artifacts are complete:

```bash
/opsx:apply
```

The AI will work through `tasks.md` and produce code.

Run tests locally:

```bash
pytest
# or equivalent for your stack
```

---

## Archiving a Change

When:

* Specs are approved
* Test contract exists
* Tasks are complete
* Tests pass

Archive the change:

```bash
openspec archive <change-name>
```

This will:

* Merge delta specs into `openspec/specs/`
* Move the change to `openspec/changes/archive/`
* Update the system’s source of truth

---

## Why This Template Exists

Most teams struggle not because of code — but because of:

* Weak specs
* Implicit decisions
* Non-reproducible reasoning
* AI generating solutions without constraints

This template exists to:

* Make reasoning explicit
* Make behavior testable
* Make AI safe to use in production workflows
* Scale engineering judgment, not just output

---

## When to Use This Template

✔ New greenfield projects
✔ Critical systems
✔ Financial, operational, or regulatory domains
✔ Teams adopting AI-assisted development
✔ Teaching engineering rigor

---

## License

MIT — use it, fork it, adapt it.

If you improve the playbook, **share it back**.

---

## Final Note

If you feel the process is “slower” at the beginning — that’s expected.

The payoff is:

* Faster iteration after first features
* Fewer rewrites
* Less tech debt
* AI that actually helps instead of guessing
