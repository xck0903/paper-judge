# Contributing

The value of this skill comes from its **criteria**, not from the number of entries. So the bar for a contribution is not "write more" — it is "every criterion must be testable".

## Welcome contributions

### 1. Add a measurement paradigm

Section 3 of `references/evidence-ladder.md` organises pitfalls by measurement paradigm. If your area (rheology, single-cell sequencing, wind-tunnel testing, field observation) is not among the five:

1. Add a category in the existing format, headed `**Your category** (typical techniques listed)`
2. Write each pitfall in the form "what else could fake this instrument's reading"
3. Each item must map to a concrete action ("was there an unirradiated control", "how much iR was compensated"), not to a reminder like "pay attention to data quality"

### 2. Report a criterion that fails

The most valuable issue is this: **a criterion that produced a wrong verdict on a particular kind of paper**.

Please include:
- Which criterion (quote the line from `SKILL.md` or `references/`)
- What kind of paper broke it
- How it broke (false positive — a flaw that wasn't there? or false negative — a real flaw missed?)
- What you would change

**Do not paste unpublished manuscript text in an issue.** A de-identified description is enough.

### 3. Add a real case

`examples/` currently holds only a structural sketch. De-identified real output is welcome (strip the material system, data and author details; keep the reasoning), together with an explanation of how a particular judgment was reached.

### 4. Translation

The instructions are maintained in English as the single source of truth. Translations of the **README** are welcome, named `README.<lang>.md`.

We deliberately do not maintain translated copies of `SKILL.md` — two copies of a rule set drift, and a drifting rule set is two different skills.

## Changes that will be declined

These are rejected on direction, not attitude:

| Not accepted | Why |
|---|---|
| Hard-wiring criteria to one discipline | Discipline-agnosticism is the core design. Field-specific content belongs in the paradigm list as a new category |
| "That is how it is done in this field" as an argument | Convention is not evidence. Every criterion needs a testable reason |
| Adding evaluative words such as "excellent performance" or "highly innovative" | Replace with checkable statements: higher than whom by how much, what was excluded |
| Relaxing the anchor requirement | Anchors (Fig. 3c / p.5) are the only thing that makes a judgment checkable |
| Recommending specific vendors, journals or institutions | This skill does not rate journals; it teaches how to judge |

## Self-check before submitting

- [ ] For every criterion I add, I can say **when it does not apply**
- [ ] Every entry maps to a concrete action, not a reminder
- [ ] No personal data, unpublished data or third-party copyrighted material included
- [ ] I ran the modified skill on at least one real paper

## Development conventions

- `SKILL.md` holds only the workflow and the hard rules. Detail lives in `references/`, registered in section 6 with "when to open which file".
- Keep `SKILL.md` under 24 KB (the English instruction file runs longer than a Chinese one for the same rule set). Going over means something should move into an appendix, not that more entries should be added.
- Record version changes in `CHANGELOG.md`.

## License

Contributions are accepted under the [MIT](LICENSE) license.
