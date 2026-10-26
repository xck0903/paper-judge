# What the output looks like

> **Note**: this is an **output skeleton**. Numbers, figure numbers, journals and authors are placeholders `████`, not real data.
> The point is to show what each section should contain and at what granularity. Real output must trace every sentence to an anchor in the source.

---

## Part 1 · Venue, group, and what the paper did (~30%)

### 1.1 Where it was published, and what the venue is worth (~90–120 words)

████ (journal), impact factor ███ 【verified】 (or "not verified").
Reputation: established and well regarded / high-impact new journal / high impact factor with a loose threshold — basis: ████ (review strictness, citation habits in the field, volume and open-access fees).

> Writing note: pick one category, show the basis, never rate the journal itself; **never infer this paper's quality from the journal name.**

### 1.2 Field and group (~200–260 words)

The subfield is currently arguing about ████, and is stuck at ████; this paper enters through ████.
First author ████ (PhD student, ████ group).
First corresponding author ████ (███ University); representative work ████, ████; the group's standing in this direction shows as ████ 【verified】.
Second corresponding author ████, working on ████.
> If nothing is found, write "not verified" — never add titles, awards or academic lineage.

### 1.3 What the paper did (~500–600 words)

**One-sentence conclusion plus provisional tier**: ████, provisionally **Tier 2 (sound with gaps)**.

**Gap and testable hypothesis**: it was previously known that ████, but it could not be shown that ████. The authors' claim rewrites as: "if ████ holds, then metric ████ should change in ████ way with condition ████."

**Methods and system choice**: technique ████ because ████; sample ████ because ████.

**Scientific soundness (judgment only)**: the chain closes overall, thin at link ████ (**evidence and reasoning: see Part 4**).

**Advance**: 【incremental / breakthrough】 — relative to prior work ████, it moves ████ forward by ████ (checkable statement, not "excellent performance").

**Logic chain**:
`gap → hypothesis → system → per-figure evidence → metric → mechanism → causation → boundary`
Weakest link: **████** (named only, not expanded).

> **Mandatory stop at the end**: figure-by-figure analysis? Fig. 1–█ / SI Fig. S1–S█ — a subset is fine.

---

## Part 2 · Figure by figure (~50%, ~120–180 words each)

```
Fig. 3 (caption ████)
- Technique and conditions: ████, mode ████, atmosphere/temperature/dose ████
- Panel breakdown: a raw observation / b processed data / c statistical summary / d simulation output / e schematic
- Data and error: ███±███ (n=██, error bars SD/SEM/CI); trend ████
- What the authors claim it proves: ████
- Evidence ladder: level ██; leap: from level 4 (statistics) straight to level 5 (mechanism)
- My judgment: moderate — reason: ████
- Where the problem is: Fig. 3c (p.5) is over-interpreted; suggests adding ████
```

**Independence between figures** (mandatory after all figures): Fig. 2–4 share the same samples and the same raw data — a chain, **not cross-validation**; Fig. 5 and Fig. 3 measure the same physical quantity with different techniques, and only that pair is genuine corroboration.

---

## Part 3 · Survey of techniques (~8%)

| Technique | What it solves | Routine / novel | User familiar? | Strength (checkable) |
|---|---|---|---|---|
| ████ | ████ | routine | yes | — |
| ████ | ████ | combinatorial novelty | no 【inferred】 | pushes time resolution from ███ to ███; costs ████ |

Hardest craft: ████ (state what it solves beyond the routine approach and what it excludes).

---

## Part 4 · Holes and suspect logic (~8%)

Tally: █ fatal, █ doubtful, █ nitpicks.

**Hole 1 | Fig. 3c (p.5) | fatal**
Problem: ████ is inferred directly from ████.
Why it is a problem: the ladder jumps from level 4 to level 6; what is missing in between is ████.
How to fix: add the ████ control / run under ████ conditions.

**Competing explanations (must be constructed yourself)**
- Explanation A: ████ (predicts ████)
- Explanation B: ████ (predicts ████)
- Discriminating experiment: ████ — measuring ████ would support A

**Claim-level verdicts**
- Well supported: ████
- Supported with caveats: ████ (caveat: ████)
- Plausible hypothesis: ████
- Insufficient: ████

**Tier update**: because of hole 1, **Tier 2 → Tier 3**.

---

## Emphasis add-on (only with an emphasis, under ~250 words)

Produce exactly one of these:

- **Transferable methods**: which step is general ████; what must change in another system ████; which step needs equipment the user lacks ████
- **Its reasoning moves**: reusable pattern ████; the leap I reject ████
- **Borrowable writing**: figure order logic ████; claim wording strength ████; weakness handling ████; how the abstract opens ████
- **The control experiments most worth adding**: ranked by cost-effectiveness ████

---

## Discussion → scoring → saving

After one or two rounds of discussion, give the six scores (1–5 each, 30 total):

| Dimension | Provisional | Reason |
|---|---|---|
| Clarity of conclusion | █/5 | ████ |
| Evidence completeness | █/5 | ████ |
| Characterization reliability | █/5 | ████ |
| Analytical rigor | █/5 | ████ |
| Chain closure | █/5 | ████ |
| Advance | █/5 | ████ |

Then save to `F:\文献资料\读文献\<Journal>_<Year>_<Title>\判读笔记.md` — one folder per paper, see Saving in `SKILL.md` — with the 12-question summary at the top:

```
01 | Scientific question: ████
02 | Prior knowledge and gap: ████
03 | Testable hypothesis: if ████ then ████
04 | Attribution of novelty: ████ (first demonstration / first quantification / first direct proof)
05 | Per-figure evidence: Fig.__ measured ████; level __
06 | Implicit assumptions: ████
07 | Sample and statistics: independent n=__ (particle/batch/atom level)
08 | Causal gap: between ████ and ████ what is missing is ████
09 | Competing explanations: A ████ / B ████ / discriminating experiment ████
10 | Claim-level verdicts: ████
11 | Worth borrowing: ████
12 | Final judgment: tier __
```
