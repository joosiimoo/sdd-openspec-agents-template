# SDD + OpenSpec + Agents Template

This repository is a **project template** for building software using
**Spec-Driven Development (SDD)** with **OpenSpec** and **AI agents**.

It is intentionally minimal.
The product here is the **process**, not the code.

---

## What This Template Is

- A repeatable setup to build software from **specs first**
- A clean integration of:
  - OpenSpec (system behavior as source of truth)
  - Test Contracts (behavior as executable agreement)
  - AI agents with strict roles
- A structure that scales to many features without chaos

---

## What This Template Is NOT

- ❌ A sample application
- ❌ A code generator
- ❌ A framework
- ❌ An AI playground

---

## Core Principles

- No code without a spec
- No tests without a spec
- No implicit decisions
- Specs define behavior, not implementation
- Tests enforce contracts, not structure

---

## Repository Structure

| Path | Purpose |
| --- | --- |
| `.cursor/agents.md` | Official agent role definitions |
| `openspec/` | System of record for behavior |
| `contracts/` | Test contracts derived from specs |
| `tests/` | Executable tests derived from contracts |
| `src/` | Implementation code |

---

## Standard Workflow

1. **Start a change**
   ```text
   /opsx:new <feature-name>
   ```
2. Refine specs
    - Agent: Spec Refiner
    - Output: OpenSpec delta specs

3. Generate test contract
   - Agent: Test Synthesizer
   - Output: `contracts/TEST_CONTRACT_<FEATURE>.md`

4. Plan tasks
   - Agent: Task Planner
   - Output: `openspec/changes/<feature>/tasks.md`

5. Implement
   - Agent: Implementer
   - Goal: Make tests pass, nothing more

6. Archive
   ```bash
   openspec archive <feature-name>
   ```

---

## How to Use This Template
1. Clone the repository
2. Open it in Cursor
3. Install OpenSpec
4. Define your feature
5. Follow the workflow

---

## Why This Exists
Most AI-assisted development fails not because of AI, but because of weak specs and implicit decisions.

This template enforces clarity, traceability, and reproducibility.

---

## License
MIT
