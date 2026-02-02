# Change Template — SDD + OpenSpec

This template defines the **mandatory structure and flow** for any new change in this repository.

Every feature, fix, or behavior change MUST follow this template.
Deviations are not allowed.

---

## 0. When to Use This Template

Use this template whenever you want to:

* Add a new feature
* Modify existing behavior
* Remove existing behavior
* Clarify ambiguous system behavior

Do **not** write code, tests, or tasks before following this template.

---

## 1. Start the Change

From the project root:

```bash
/opsx:new <change-name>
```

Naming rules:

* Use kebab-case
* Describe behavior, not implementation

Examples:

* `order-processing`
* `cash-drawer-validation`
* `reconcile-rendition`

This creates:

```
openspec/changes/<change-name>/
```

---

## 2. Proposal (WHY + WHAT)

**File:**

```
openspec/changes/<change-name>/proposal.md
```

### Purpose

Explain:

* Why this change exists
* What behavior is being added/changed/removed
* What is explicitly out of scope

### Required Sections

```markdown
# Proposal: <change-name>

## Intent
Why this change is needed.

## Scope
What behavior is included.

## Non-Goals
What this change will NOT do.

## Assumptions
Any known constraints or invariants.
```

### Rules

* No technical decisions
* No solution design
* Plain language
* Understandable by non-engineers

If intent or scope is unclear → **stop and clarify**.

---

## 3. Specs (Behavior Definition)

**Agent:** Spec Refiner
**Command:** `/opsx:continue`

**Location:**

```
openspec/changes/<change-name>/specs/<capability>/spec.md
```

### Rules

* Use OpenSpec delta format only:

  * `ADDED`
  * `MODIFIED`
  * `REMOVED`
* Each requirement MUST:

  * Describe observable behavior
  * Include GIVEN / WHEN / THEN scenarios
  * Produce deterministic outcomes
* MUST include an explicit:

  ```
  The system does NOT:
  ```

  section

### Forbidden

* APIs
* Data models
* Algorithms
* Technologies
* Frameworks

If behavior is ambiguous → **stop and ask questions**.

---

## 4. Test Contract (Executable Agreement)

**Agent:** Test Synthesizer

**File:**

```
openspec/changes/<change-name>/TEST_CONTRACT.md
```

### Purpose

Translate specs into **verifiable behavior**.

### Rules

* One or more tests per scenario
* No new behavior
* No implementation hints
* Deterministic inputs and outputs

This file defines:

> “How we know the system behaves correctly”

Not:

> “How we build it”

If a scenario cannot be tested → **stop and report the gap**.

---

## 5. Design (Optional but Explicit)

**File:**

```
openspec/changes/<change-name>/design.md
```

### When Required

Design is required if:

* Multiple approaches are possible
* Trade-offs exist
* Clarification is needed before tasks

### Rules

* Explains *approach*, not code
* No functions, classes, or APIs
* Must not contradict specs or test contract

If no design decisions exist, explicitly state:

```
This change requires no design decisions beyond the defined specs.
```

---

## 6. Tasks (Execution Plan)

**Agent:** Task Planner

**File:**

```
openspec/changes/<change-name>/tasks.md
```

### Rules

* Tasks derive ONLY from the Test Contract
* One task = one verifiable capability
* Tasks reference test scenarios
* No files, functions, frameworks, or technologies

If a task requires design → **stop and go back to design**.

---

## 7. Implementation

**Agent:** Implementer
**Command:** `/opsx:apply`

### Rules

* Code exists only to satisfy tasks
* Tests define correctness
* No speculative behavior
* Stop when tests pass

Do NOT:

* Modify specs
* Modify test contracts
* Add new behavior

---

## 8. Verify

Run tests:

```bash
pytest
```

Expected:

```
All tests pass
```

Failures mean:

* Implementation is incomplete
* Specs or tests must NOT be changed silently

---

## 9. Archive the Change

When ALL are true:

* Specs approved
* Test Contract exists
* Tasks completed
* Tests passing

Run:

```bash
openspec archive <change-name>
```

Results:

* Delta specs merged into `openspec/specs/`
* Change moved to `openspec/changes/archive/`
* System source of truth updated

---

## 10. Non-Negotiable Rules

* No code without specs
* No tests without specs
* No tasks without test contracts
* No assumptions
* No silent fixes
* No shortcuts

If the process feels slow:
👉 That is intentional.

---

## 11. If the Flow Breaks

If you feel tempted to:

* Skip a step
* “Just code it”
* Fix tests or specs ad hoc

Stop.

Go back **one step**, not forward.

---

## Final Note

This template exists to make:

* AI reliable
* Behavior explicit
* Systems auditable
* Teams scalable

Follow it strictly.
