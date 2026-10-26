# Critical Reading Checklist (for active questioning)

Use together with `evidence-ladder.md`: that file supplies the criteria, this one supplies **the questions to ask**. Work through A to D in order; do not skip.

## A · Samples, representativeness, controls

1. How many **independent** particles / samples / devices / batches were actually measured? How many figures are really different processing of the same specimen?
2. How were samples selected? Are size, morphology, orientation (zone axis, grain orientation, device orientation) or "trackability" selection criteria? **Were only the good-looking ones reported?**
3. Do the single-object structure and the ensemble performance come from **the same statistical population**? Explaining batch B's activity with particle A's structure is a mismatch.
4. Are controls complete: blank, positive and negative controls, before/after treatment, before/after cycling, **unirradiated or untreated specimens**?
5. Were any negative results dropped?

## B · Metric definition, numbers, statistics

1. How is the metric defined? What is the denominator?
2. Is it reporting percentage points or percent? Was the conversion done correctly?
3. Is n particle-level, batch-level or atom-level? **Atoms inside one particle are not independent experiments.**
4. Are error bars SD, SEM or CI? Computed from how many repeats?
5. Which test was used? One-sided or two-sided? Is there an effect size beyond the p-value?
6. When "reversible" or "stable" is claimed, which meaning is intended (see `evidence-ladder.md` section 5)?

## C · Measurement artefacts and model sensitivity

1. Walk through the artefact list in `evidence-ladder.md` section 3, item by item, asking "did this paper handle it".
2. Does the model survive a change of prior? Is it parameter-sensitive? Did the authors provide a sensitivity analysis?
3. Could several processes produce the same final result? Did the authors discuss this?

## D · Excluding alternative explanations (**construct actively, not just check passively**)

For **every core claim**, invent at least **two** competing explanations yourself, then state what experiment would make them predict differently.

Usual sources of competing explanations: structural difference / chemical state / coverage / sintering and agglomeration / strain / interfacial effects / mass-transport limitation / irradiation and heating / differences in measurement conditions / statistical artefact.

Criterion: **look for an intervention that discriminates between mechanisms, not for more good-looking figures of the same kind.** If the authors only added more data from the same technique, nothing was excluded.

## E · Attribution of novelty (no vagueness allowed)

Separate the three kinds of "first", which authors routinely blur:

| Claim | What it actually means |
|---|---|
| First demonstration | The first time this phenomenon or system was produced at all |
| First quantification | The phenomenon was seen before; this is the first reliable number for it |
| First direct proof | Predecessors had only indirect inference; this is the first direct evidence |

Also mandatory: **a new combination of mature tools is not a new instrument or algorithm**; "first application of technique X to system Y" is usually combinatorial novelty only.

## F · Independence between figures

- Do this set of figures share **the same dataset**, the same **assumption**, the same **sample**?
- Does a later figure use an earlier figure's conclusion as a premise? If so they are **not** cross-validation, only a chain.
- Where "multiple techniques corroborate" is claimed, are they measuring the same physical quantity? Only the same quantity measured by two instruments counts as corroboration.

## G · Panel classification (to stop schematics posing as evidence)

Classify every panel first, then judge whether it can carry the authors' sentence:

| Type | Can it be evidence? |
|---|---|
| Raw observation (micrograph, spectrum, curve) | Yes, but check conditions and artefacts |
| Processed data (filtered, fitted, reconstructed) | Yes, but check whether processing introduced structure |
| Statistical summary (bar chart, distribution, error) | Can support a "trend", never a "mechanism" |
| Simulation output (DFT, MD, FEM) | Can support "possible", cannot replace observation |
| Schematic / mechanism drawing | **Not evidence** — only the authors' narration |

If a key claim rests only on schematics and simulation with **no raw observation at all**, that link is the weakest by definition.

## H · Hunting contradictions in the SI

1. **Failed or unsuccessful experiments** — the part that breaks when conditions change, or that could not be reproduced
2. **Spectra with no signal** — a peak that should be there and is not, waved away with "possibly …"
3. **Limitations the authors admit** — "this work does not consider …", "limited by …"

These three are often worth more than any figure in the main text. **Where the main text and the SI disagree, priority is highest.**
