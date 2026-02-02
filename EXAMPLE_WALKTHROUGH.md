# Example Walkthrough — Order Processing (SDD + OpenSpec + Agents)

This walkthrough shows **end-to-end** how to implement a feature using this template, **without improvisation**, **without hidden steps**, and **without prior context**.

The goal is not the code — it is to demonstrate the **method**.

---

## Example Feature

**Order Processing**

A simple domain used to demonstrate Spec-Driven Development:

* Create an order
* Get an order
* Confirm an order
* Cancel an order

This feature is intentionally small but **complete**, covering:

* State transitions
* Deterministic outcomes
* Error conditions
* Terminal states

---

## Step 0 — Preconditions

Before starting:

* Repo cloned
* OpenSpec installed
* Cursor (or another AI-enabled editor) configured
* `.cursor/agents.md` and `openspec/specs/config.yaml` are present

No code exists yet.

---

## Step 1 — Start a Change

From the project root:

```bash
/opsx:new order-processing
```

This creates:

```text
openspec/changes/order-processing/
```

At this point:

* No specs exist
* No assumptions are allowed
* No code is written

---

## Step 2 — Proposal (WHY + WHAT)

**Agent involved:** none (human or AI-assisted writing is fine)

Create:

```
openspec/changes/order-processing/proposal.md
```

Purpose:

* Explain **why** this change exists
* Define **scope**
* Explicitly list **non-goals**

Example (simplified):

* Intent: demonstrate an order lifecycle
* Scope: in-memory, single process
* Non-goals: persistence, auth, APIs, integrations

⚠️ No technical design yet.

---

## Step 3 — Specs (Behavior Definition)

**Agent:** Spec Refiner

Run (or instruct Cursor):

```text
/opsx:continue
```

The Spec Refiner creates delta specs under:

```
openspec/changes/order-processing/specs/order-processing/spec.md
```

What goes into the spec:

* Requirements in plain language
* GIVEN / WHEN / THEN scenarios
* Deterministic outcomes
* Explicit “The system does NOT” section

Example behaviors:

* New orders start as PENDING
* CONFIRMED and CANCELLED are terminal
* Invalid transitions are rejected

🚫 No APIs
🚫 No functions
🚫 No data models

If behavior is ambiguous → **stop and clarify**.

---

## Step 4 — Test Contract (Executable Agreement)

**Agent:** Test Synthesizer

Input:

* Only the approved specs

Output:

```
openspec/changes/order-processing/TEST_CONTRACT.md
```

Rules enforced:

* Every scenario → at least one test
* No new behavior
* No implementation hints
* Same inputs → same outputs

This file answers:

> “How do we know the system behaves correctly?”

Not:

> “How do we implement it?”

---

## Step 5 — Tasks (Execution Plan)

**Agent:** Task Planner

Input:

* Test Contract only

Output:

```
openspec/changes/order-processing/tasks.md
```

Each task:

* Maps to one or more test scenarios
* Describes **what capability must exist**
* Avoids *how* it is done

Example task phrasing:

* “The system can transition an order from PENDING to CONFIRMED”
* “The system rejects invalid state transitions deterministically”

🚫 No files
🚫 No functions
🚫 No frameworks

If a task requires design → that design belongs in `design.md`.

---

## Step 6 — Implementation

**Agent:** Implementer

Run:

```text
/opsx:apply
```

Rules:

* Code exists only to satisfy tasks
* Tests define success
* No refactors unless required
* Stop when tests pass

Result:

* Minimal code
* No speculative abstractions
* Behavior matches spec exactly

---

## Step 7 — Verify

Run tests locally:

```bash
pytest
```

Expected result:

```
All tests pass
```

If not:

* Fix code
* Do NOT modify specs or tests silently

---

## Step 8 — Archive

When:

* Specs approved
* Test Contract exists
* Tasks completed
* Tests passing

Run:

```bash
openspec archive order-processing
```

This:

* Merges delta specs into `openspec/specs/`
* Moves the change to `openspec/changes/archive/`
* Updates the system’s source of truth

After archive:

```bash
openspec list
# No active changes
```

---

## What This Walkthrough Proves

* Specs can fully drive development
* AI can be constrained safely
* The flow is repeatable
* No tribal knowledge is required
* No “magic prompts” are needed

---

## How to Start Your Next Feature

Repeat **exactly** the same steps:

```bash
/opsx:new <next-feature>
```

Examples:

* `cash-drawer-validation`
* `reconcile-rendition`
* `payment-reconciliation`

The process does not change.
Only the behavior does.

---

## If the Flow Breaks

If at any step you feel:

* Confused
* Forced to assume
* Tempted to “just code it”

That means:
👉 **A spec is weak or missing**

Go back **one step**, not forward.

---

## Final Note

This template is intentionally strict.

Strictness is what makes:

* AI reliable
* Systems auditable
* Teams scalable
