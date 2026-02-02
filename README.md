# SDD + OpenSpec + Agents — Project Template

This repository is a **public template** for building software using **Strict Spec-Driven Development (SDD)** with **OpenSpec** and **AI Agents**.

Behavior-first development: **repeatable**, **auditable**, **operational** — no magic, no assumptions.

---

## 👉 Entry point: the Change Template

**Before writing code or running agents, read this:**

**[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)**

That document is the **mandatory structure and flow** for every change in this repo. It is part of the system’s operating model, not optional documentation.

It defines:

* **When** to use it (new feature, behavior change, clarification)
* **Steps 0–11**: from “start change” → proposal (human-only) → specs → test contract → tasks → implementation → verify → archive
* **Rules per step**: what is allowed, forbidden, and when to stop
* **No assumptions**: the flow does not rely on implicit decisions; each step has explicit criteria

The proposal is **human-first by design** — you write it manually; OpenSpec does not generate it. The rest of the flow is **teachable, repeatable, and defendible**: agents have clear roles and boundaries, and the template tells you exactly what to do when the flow breaks.

Use **CHANGE_TEMPLATE.md** as your single source of truth for *how* to work. This README gives you *what* this repo is and *why* it exists.

---

## What This Repo Is

A **non-negotiable development flow** (full detail in [CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)):

```
PROPOSAL (human-written, intent only)
   ↓
SPECS (behavior, delta format)
   ↓
TEST CONTRACT (executable agreement)
   ↓
TASKS (from contract only)
   ↓
IMPLEMENTATION (code to satisfy tests)
   ↓
VERIFY → ARCHIVE (source of truth)
```

* Specs define **what the system does**, never how
* Tests are **contracts**, not examples
* Code exists **only** to satisfy tests
* No implicit decisions, no speculative design, no shortcuts

---

## What This Repo Is NOT

❌ Not a framework
❌ Not a coding style guide
❌ Not an architecture reference
❌ Not tied to any language or stack

It intentionally avoids prescribing APIs, databases, frameworks, or “best practices” without specs.

---

## Core Principles

* **No code without a spec**
* **No tests without a spec**
* **No tasks without a test contract**
* **No assumptions** — if unclear, stop and clarify
* **Specs are the source of truth**
* **Tests are executable contracts**
* **AI agents respect role boundaries** (defined in the Change Template)

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

### 0. Read the Change Template

**[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)** is the entry point. It defines when to use the template, the full step-by-step flow, and what to do when the flow breaks. Do not skip this.

### 1. Initialize OpenSpec

```bash
openspec init
```

This creates the `openspec/` directory and loads project rules.

### 2. Start a Change (then follow the template)

```bash
/opsx:new <change-name>
```

Example: `/opsx:new order-processing` → creates `openspec/changes/order-processing/`.

**Next (mandatory):** Write `proposal.md` manually (use [PROPOSAL_TEMPLATE.md](./PROPOSAL_TEMPLATE.md)). Do not run `/opsx:continue` or ask the AI to infer intent until the proposal is complete. Then follow [CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md) from step 3 onward.

---

## The Agent-Based Workflow

This repo uses **four explicit AI agents** with strict responsibilities. **When and how to use each agent** is defined in **[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)** (steps 3–7). Summary:

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

Full flow and rules → **[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)** (steps 6–8).

Once proposal, specs, test contract, and tasks are complete:

```bash
/opsx:apply
```

The AI works through `tasks.md` and produces code.

Run tests locally:

```bash
pytest
# or equivalent for your stack
```

---

## Archiving a Change

Criteria and command → **[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)** (step 9).

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

**Start with [CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md).** It is the operating model for every change. If the process feels slower at the beginning — that’s intentional.

The payoff is: faster iteration after the first features, fewer rewrites, less tech debt, and AI that helps instead of guessing.
