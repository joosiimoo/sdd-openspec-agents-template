# How to Start a Change

Short checklist for starting a new change in this repository (SDD + OpenSpec + Agents).

---

## Checklist

1. **Run** `/opsx:new <change-name>`  
   Creates `openspec/changes/<change-name>/`. OpenSpec does **not** generate content; it only initializes the container.

2. **Create** `proposal.md` from **[PROPOSAL_TEMPLATE.md](./PROPOSAL_TEMPLATE.md)** (manual step).  
   OpenSpec does **not** auto-generate the proposal. You **MUST** create `openspec/changes/<change-name>/proposal.md` yourself.

3. **Do not run** `/opsx:continue` until the proposal is complete.

4. **Then** run `/opsx:continue` for design, specs, and tasks (as defined in [CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)).

5. **Then** `/opsx:apply` and `/opsx:archive` when implementation is done and tests pass.

---

## References

- **[CHANGE_TEMPLATE.md](./CHANGE_TEMPLATE.md)** — Full flow, steps 0–11, and rules per step.
- **[PROPOSAL_TEMPLATE.md](./PROPOSAL_TEMPLATE.md)** — Structure for the proposal.
- **README.md** — Section [Important: Proposal Generation](./README.md#important-proposal-generation): why the proposal is manual and where to create it.
