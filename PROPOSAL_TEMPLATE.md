# Proposal: <change-name>

Use this structure for every proposal. Replace `<change-name>` and the placeholders below with your content. The **Capabilities** section drives the specs phase: each new capability becomes `specs/<name>/spec.md`.

---

## Why

<!-- Explain the motivation for this change. What problem does this solve? Why now? -->

## What Changes

<!-- Describe what will change. Be specific about new capabilities, modifications, or removals. Mark breaking changes with **BREAKING**. -->

## Capabilities

### New Capabilities
<!-- Capabilities being introduced. Each creates specs/<name>/spec.md. Use kebab-case (e.g., user-auth, data-export). -->
- `<name>`: <brief description of what this capability covers>

### Modified Capabilities
<!-- Existing capabilities whose REQUIREMENTS are changing (not just implementation). Each needs a delta spec file. Use existing spec names from openspec/specs/. If none, write "None" or leave a single bullet with "None". -->
- `<existing-name>`: <what requirement is changing>
<!-- Example: "None" if no existing specs are being changed -->

## Impact

<!-- Affected code, APIs, dependencies, systems -->
