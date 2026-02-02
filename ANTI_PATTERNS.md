# Anti-Patterns — SDD + OpenSpec + AI

This document lists **common failure modes** when using Spec-Driven Development with AI agents.

If you recognize one of these patterns in your workflow, **stop immediately** and correct course.

---

## 1. Writing Code Before Specs Exist

**Smell**

* “It’s a small feature, I’ll just code it.”
* “We’ll refine the spec later.”

**Why it breaks**

* Behavior becomes implicit
* Specs become retroactive justifications
* AI starts guessing intent

**Correction**

* No spec → no code
* Always start with `/opsx:new`

---

## 2. Specs That Describe Implementation

**Smell**

* Specs mention APIs, endpoints, classes, schemas, or algorithms
* GIVEN/WHEN/THEN references technical artifacts

**Why it breaks**

* Specs become fragile
* Tests lock you into early design decisions
* AI can’t reason at the behavior level

**Correction**

* Rewrite specs in plain language
* Describe *observable behavior only*

---

## 3. Ambiguous Specs “Fixed” in Tests

**Smell**

* Tests add behavior not clearly stated in the spec
* Test names explain rules the spec never defined

**Why it breaks**

* Specs stop being the source of truth
* Tests silently redefine the system

**Correction**

* Stop test generation
* Go back to Spec Refiner
* Make the behavior explicit in the spec

---

## 4. Tests That Are Examples, Not Contracts

**Smell**

* Tests look like happy-path demos
* Edge cases are missing
* Determinism is not enforced

**Why it breaks**

* Passing tests don’t guarantee correctness
* AI fills gaps with assumptions

**Correction**

* Every GIVEN/WHEN/THEN must map to a test
* Same inputs must always produce same outputs

---

## 5. Task Lists That Contain Design Decisions

**Smell**

* Tasks mention files, functions, classes, frameworks
* Tasks explain *how* instead of *what*

**Why it breaks**

* Implementation is decided too early
* Agents collapse into “code generator mode”

**Correction**

* Tasks must reference scenarios, not solutions
* If design is required, add `design.md`

---

## 6. Skipping the Design Artifact “Because It’s Obvious”

**Smell**

* “There’s only one way to do this.”
* “We don’t need design for something this small.”

**Why it breaks**

* Hidden assumptions go undocumented
* Later changes become inconsistent

**Correction**

* Either write a short design
* Or explicitly state: “No design decisions required”

---

## 7. Letting the Implementer Change Specs or Tests

**Smell**

* “I adjusted the spec to match the code.”
* “The test was wrong, so I fixed it.”

**Why it breaks**

* Source of truth shifts silently
* Behavior changes without review

**Correction**

* Implementer must stop and escalate
* Only Spec Refiner can change specs

---

## 8. “Refactoring” During Initial Implementation

**Smell**

* Code cleanup before all tests pass
* Renaming, abstraction, optimization mid-flow

**Why it breaks**

* Introduces untested behavior
* Makes failures harder to reason about

**Correction**

* First goal: make tests pass
* Refactor only as a separate change

---

## 9. Adding Behavior Not Covered by Tests

**Smell**

* “This might be useful later”
* Extra logic not exercised by any test

**Why it breaks**

* Creates undocumented behavior
* Specs and reality diverge

**Correction**

* Delete the code
* Or add a spec → test → task → implementation

---

## 10. Mixing Multiple Features in One Change

**Smell**

* One change folder touches multiple domains
* Specs feel overloaded or unrelated

**Why it breaks**

* Specs become unreadable
* Archive becomes meaningless

**Correction**

* One change = one behavioral concern
* Split changes aggressively

---

## 11. Archiving Without Full Validation

**Smell**

* Specs archived but tests don’t exist
* Tests pass but specs were never approved

**Why it breaks**

* Source of truth is polluted
* Future changes build on unstable ground

**Correction**

* Archive only when:

  * Specs approved
  * Test contract exists
  * Tests pass

---

## 12. Treating AI Prompts as “Magic”

**Smell**

* Workflow depends on remembering special prompts
* Only one person knows “how to talk to the AI”

**Why it breaks**

* Knowledge is not transferable
* Process is not repeatable

**Correction**

* Encode rules in:

  * `.cursor/agents.md`
  * `openspec/specs/config.yaml`
  * Templates and walkthroughs

---

## 13. Optimizing for Speed Instead of Clarity

**Smell**

* “This feels slow”
* Pressure to skip steps

**Why it breaks**

* Ambiguity compounds
* Rework increases exponentially

**Correction**

* Slowness at the start = speed later
* Clarity is the acceleration mechanism

---

## 14. Confusing “Agent-Native” With “Hands-Off”

**Smell**

* Expecting AI to decide intent
* Letting agents proceed without clarification

**Why it breaks**

* AI invents behavior
* Specs drift from reality

**Correction**

* Humans own intent
* Agents execute roles, not judgment

---

## Final Rule

If at any point you feel:

* Confused
* Forced to assume
* Tempted to “just fix it”

👉 **You are one step too far ahead.**

Go back to the previous artifact.

---

## Why This Document Exists

These anti-patterns were not theoretical.
They are distilled from **real failures** in AI-assisted development.

Avoid them, and SDD + AI becomes:

* Predictable
* Auditable
* Scalable

Ignore them, and you’re just generating code faster — not software better.
