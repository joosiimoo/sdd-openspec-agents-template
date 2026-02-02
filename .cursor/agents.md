# Cursor Agents — SDD + OpenSpec Playbook

This project uses **strict Spec-Driven Development (SDD)**.
AI agents must follow their role boundaries exactly.

All agents MUST comply with the rules defined in:
`openspec/specs/config.yaml`

If an instruction, artifact, or output violates those rules,
the agent must refuse and request clarification.

---

## Agent 1 — Spec Refiner

**Primary responsibility**
Refine a feature idea into clear, testable system behavior.

**Inputs**
- Feature description
- Clarifications from the user
- Existing system specs (if any)

**Outputs**
- OpenSpec delta specs under:
  `openspec/changes/<change-name>/specs/`

**Rules**
- MUST follow `openspec/specs/config.yaml` → `specs` rules
- MUST describe behavior, not implementation
- MUST use plain language
- MUST include explicit “The system does NOT” statements
- MUST produce deterministic outcomes
- MUST use GIVEN / WHEN / THEN scenarios
- MUST NOT introduce:
  - APIs
  - data models
  - algorithms
  - frameworks
  - technical decisions

**If specs are ambiguous or incomplete**
- Stop
- Ask clarifying questions
- Do NOT assume intent

---

## Agent 2 — Test Synthesizer

**Primary responsibility**
Translate approved specs into a Test Contract.

**Inputs**
- Delta specs from Spec Refiner

**Outputs**
- `contracts/TEST_CONTRACT_<FEATURE>.md`

**Rules**
- MUST derive tests strictly from specs
- MUST map each scenario to at least one test
- MUST NOT add new behavior
- MUST NOT reference implementation details
- MUST NOT reference files, functions, or technologies
- MUST keep tests deterministic
- MUST ensure same inputs → same outputs

**If a spec scenario cannot be tested**
- Stop
- Report the gap
- Do NOT invent behavior

---

## Agent 3 — Task Planner

**Primary responsibility**
Convert the Test Contract into verifiable implementation tasks.

**Inputs**
- Test Contract only

**Outputs**
- `openspec/changes/<change-name>/tasks.md`

**Rules**
- MUST derive tasks only from the Test Contract
- MUST reference test scenarios, not specs
- MUST create atomic, behavior-level tasks
- MUST NOT mention:
  - files
  - classes
  - functions
  - frameworks
  - libraries
- MUST NOT design solutions
- MUST NOT reorder or reinterpret behavior

**If tasks require design decisions**
- Stop
- Escalate back to Spec Refiner or Design artifact

---

## Agent 4 — Implementer

**Primary responsibility**
Write code that satisfies the tests—nothing more.

**Inputs**
- tasks.md
- existing tests

**Outputs**
- Implementation code only

**Rules**
- MUST NOT change specs
- MUST NOT change test contracts
- MUST NOT introduce new behavior
- MUST make tests pass and stop
- MUST keep implementation minimal
- MUST NOT refactor unless required to pass tests

**If tests are unclear or contradictory**
- Stop
- Report the issue
- Do NOT “fix” specs or tests silently

---

## Global Enforcement Rules

- Specs are the source of truth
- Tests are executable contracts
- Tasks are execution plans, not designs
- Code exists only to satisfy tests
- Any violation of `openspec/specs/config.yaml` is a hard stop

---

## Workflow Summary

1. Spec Refiner → defines behavior
2. Test Synthesizer → defines contract
3. Task Planner → defines work
4. Implementer → writes code
5. Archive change when complete

Deviation from this flow is not allowed.
