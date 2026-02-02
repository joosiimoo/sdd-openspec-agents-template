# Change Template — SDD + OpenSpec

This template defines the **mandatory structure and flow** for any new change in this repository.

Every feature, fix, or behavior change **MUST** follow this template.
Deviations are **not allowed**.

This document is part of the system’s operating model, not optional documentation.

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

### Naming rules

* Use kebab-case
* Describe **behavior**, not implementation

**Examples:**

* `order-processing`
* `cash-drawer-validation`
* `reconcile-rendition`

This creates:

```text
openspec/changes/<change-name>/
```

---

## 2. Proposal (WHY + WHAT)

**File:**

```text
openspec/changes/<change-name>/proposal.md
```

### Purpose

The proposal defines:

* **Why** this change exists
* **What** it enables at a high level
* **What is explicitly out of scope**

It intentionally avoids rules, edge cases, and technical decisions.

---

### Mandatory Proposal Template

When `/opsx:new` is executed, the proposal **MUST** be initialized using the following template.
Do **not** start from an empty document.

```markdown
# Proposal: <change-name>

> This document defines **why** this change exists and **what** it enables.
> It intentionally avoids rules, edge cases, or technical decisions.

---

## Intent

Describe the core problem this change addresses.

Guidelines:
- Why does this change matter?
- Who is affected?
- What pain or limitation exists today?

Avoid:
- Solution descriptions
- Technical language
- Feature lists

---

## Context (optional)

Provide background information needed to understand the problem.

Examples:
- Business constraints
- Regulatory context
- Organizational realities

Do NOT include:
- Systems
- Architecture
- Data models
- APIs

---

## Scope

Describe **what this change enables**, at a high level.

Use short bullet points.  
Each bullet describes a capability, not a rule.

Example:
- Allow orders to be created and tracked through their lifecycle
- Make order state observable at any point in time

---

## Non-goals

This section is **mandatory**.

Explicitly list what this change does NOT attempt to solve.

Example:
- No persistence
- No authentication
- No integrations with external systems

---

## Success criteria

Describe how we know this change is successful.

Guidelines:
- Observable outcomes only
- No technical metrics
- No implementation assumptions

Example:
- Users can determine the current state of an order
- Invalid state transitions are prevented
```

---

### Proposal Rules

* MUST follow the Mandatory Proposal Template
* MUST use plain language
* MUST be understandable by non-engineers
* MUST NOT include:

  * Technical decisions
  * Rules or validations
  * State machines
  * APIs or data models
  * Edge cases

If intent or scope is unclear → **stop and clarify**.

---

## 3. Specs (Behavior Definition)

**Agent:** Spec Refiner
**Command:** `/opsx:continue`

**Location:**

```text
openspec/changes/<change-name>/specs/<capability>/spec.md
```

### Rules

* Use OpenSpec **delta format only**:

  * `ADDED`
  * `MODIFIED`
  * `REMOVED`
* Each requirement MUST:

  * Describe observable system behavior
  * Include GIVEN / WHEN / THEN scenarios
  * Produce deterministic outcomes
* MUST include an explicit:

```text
The system does NOT:
```

section.

### Forbidden in specs

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

```text
openspec/changes/<change-name>/TEST_CONTRACT.md
```

### Purpose

Translate specs into **verifiable behavior**.

The test contract defines:

> “How we know the system behaves correctly”

Not:

> “How the system is implemented”

### Rules

* One or more tests per scenario
* No new behavior
* No implementation hints
* Deterministic inputs and outputs

If a scenario cannot be tested → **stop and report the gap**.

---

## 5. Design (Optional but Explicit)

**File:**

```text
openspec/changes/<change-name>/design.md
```

### When design is required

Design is required if:

* Multiple approaches are possible
* Trade-offs exist
* Clarification is needed before tasks

### Rules

* Explains **approach**, not code
* No functions, classes, or APIs
* Must not contradict specs or test contract

If no design decisions exist, explicitly state:

```text
This change requires no design decisions beyond the defined specs.
```

---

## 6. Tasks (Execution Plan)

**Agent:** Task Planner

**File:**

```text
openspec/changes/<change-name>/tasks.md
```

### Rules

* Tasks derive **ONLY** from the Test Contract
* One task = one verifiable capability
* Tasks reference **test scenarios**, not specs
* MUST NOT mention:

  * Files
  * Functions
  * Classes
  * Frameworks
  * Libraries

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

```text
All tests pass
```

Failures mean:

* Implementation is incomplete
* Specs or tests must NOT be changed silently

---

## 9. Archive the Change

Archive only when ALL are true:

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
* Fix specs or tests ad hoc

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
