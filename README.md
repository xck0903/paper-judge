# Paper Judge · Critical Reading & Verdict

> `paper-judge` — an agent skill for **close reading of scientific papers that ends in a verdict**. It reads with a referee's attitude: acknowledge what the work contributes, but do not take its conclusions on trust.

**English** · [中文](README.zh-CN.md)

Reading is the means. **The verdict is the product.** That is why it is called *judge* and not *review* — review describes reading it once; judge means you have to say where it stands.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Discipline agnostic](https://img.shields.io/badge/scope-discipline--agnostic-blue)
![Pure markdown](https://img.shields.io/badge/dependencies-none-lightgrey)

---

## The problem it solves

Ask an AI to read a paper and three failures recur:

| Failure | What it looks like |
|---|---|
| **Paraphrasing** | The abstract restated in different words. You finish reading and still do not know whether the work holds up |
| **Politeness** | "This study is of great significance" and "the method design is reasonable" throughout, with not one checkable statement |
| **Fabrication** | Reporting "about 3.2 nm" for a figure the model never actually looked at; completing experimental conditions the paper never stated |

Every hard rule in this skill exists to block one of these. The rules are not stylistic preferences — they are countermeasures with a specific failure attached.

---

## Core design: three scales, each on its own layer

The same word — "good" or "weak" — cannot be used across three different layers. This skill keeps three scales apart:

| Object | Scale | Question it answers |
|---|---|---|
| **A single claim** | Well supported / supported with caveats / plausible hypothesis / insufficient | Can I use this sentence? |
| **A single figure or piece of evidence** | Strong / moderate / weak, plus its rung on the evidence ladder | What does this figure actually prove? |
| **The whole paper** | Tier 1 well substantiated / Tier 2 sound with gaps / Tier 3 half-believable (~50%) / Tier 4 does not hold | Can I cite this, and how? |

**The paper's tier is set by its most critical weak claim, not by the average.** Five solid conclusions and one soft one: the tier follows the soft one.

---

## The evidence ladder (the foundation)

Before grading evidence, know which rung it stands on and where it was substituted:

| Level | What happens | Usual substitution |
|---|---|---|
| 1 Direct signal | What the instrument actually recorded | A processed pretty image passed off as the raw signal |
| 2 Preprocessing | Denoising, background subtraction, peak fitting, registration, AI restoration | Processing introduced periodicity or contrast, then read as "structure" |
| 3 Quantification and reconstruction | Counting, coordinates, phase fractions, strain | Algorithm settings undisclosed; built-in assumptions presented as observation |
| 4 Statistical association | Which groups, what n, how large the error | Thousands of atoms in one particle treated as thousands of independent experiments |
| 5 Physical / chemical interpretation | Why a structural metric maps onto performance or mechanism | The intermediate step never measured, filled in from "well known" |
| 6 Causation and generality | Intervention, controls, repeats, independent characterization | "Two quantities move together" upgraded to "one causes the other" |

Two hard floors:

> Never derive causation from two quantities co-varying.
> Never describe reconstructed or fitted coordinates as a filmed trajectory.

---

## How to use it

**Input**: a paper PDF (with supporting information if available) plus one line about what you want out of it.

**Workflow** (the skill stops and waits at each checkpoint):

```
Pick an emphasis
  ↓
Part 1  Venue, group, and what the paper did (~30%)
  ↓   ← STOP: ask whether to go figure by figure, and which figures
Part 2  Figure by figure, panels classified, rungs located (~50%)
  ↓
Part 3  Survey of techniques (horizontal table: routine/novel, familiar to you, strength)
  ↓
Part 4  Holes and suspect logic (each with anchor + severity + fix)
  ↓
Emphasis add-on (only if one was chosen)
  ↓   ← STOP: invite questions, discuss over one or two rounds
Multi-dimensional score (6 dimensions × 5 points)
  ↓
Save as markdown
```

**Emphasis is a weight, not a menu.** Whatever you pick, all four parts are produced, the logic chain is drawn and the hole list is complete. Emphasis only decides where the prose gets thicker and which single section is appended.

| Emphasis | Where it digs |
|---|---|
| Default (none given) | Full close read, balanced output |
| ① Experimental method | Protocol, synthesis logic, condition window; appends "Transferable methods" |
| ② Data analysis and reasoning | How data became claims, how evidence was chained; appends "Its reasoning moves" |
| ③ Writing and figure design | Figure order, text–figure interlock, how weaknesses are routed around; appends "Borrowable writing" |
| ④ Citing it | Position in the field, citable sentences, their qualifiers (the tier is still mandatory — citing transfers responsibility) |
| ⑤ Challenging it | Part 4 becomes the main event; appends "The control experiments most worth adding" |

---

## A few of the criteria

- **A schematic is not evidence.** If a key claim rests only on schematics and simulation, with no raw observation, that link is the weakest by definition.
- **Figures are not automatically independent.** Six attractive figures can share one dataset and one sample. That is not cross-validation, it is repetition.
- **Thousands of atoms inside one particle ≠ thousands of independent experiments.**
- **"Not significant" is not "equivalent";** "reversible" must be split into trajectory recovery, distribution recovery, or a non-significant difference.
- **Percentage points are not percent.** From 92.3% to 91.0% is 1.3 percentage points, not 13%.
- **Construct two competing explanations yourself.** Not "did the authors exclude it" — build them, then state what experiment would make them predict differently.
- **Hunt the SI for contradictions**: the experiment that fails when conditions change, the spectrum with no signal, the limitation the authors admit.
- **Venue reputation is background only.** Never infer paper quality from the journal name. High-impact venues publish filler; low-impact venues publish solid work.
- **Every judgment carries an anchor** (Fig. 3c / p.5 / SI Fig. S12). No anchor, no claim.

---

## Discipline-agnostic by design

The skill binds to no field. The mechanism: **pitfall checklists are organised by measurement paradigm, not by discipline.**

| Paradigm | Typical questions |
|---|---|
| Imaging | Radiation damage, drift, projection effects, sampling bias |
| Spectroscopy and diffraction | Charging and baselines, fitting constraints, peak overlap, quantification factors |
| Electrochemistry and performance | iR compensation, normalization denominator, transport and bubbles, stability duration |
| Mechanics, thermal, devices | Contact resistance or thermal resistance, calibration and hysteresis, size effects |
| Computation and simulation | Convergence, sampling, model priors, relation to experiment |

If your paradigm is not listed, write your own group in the same form: **"what else could fake this instrument's reading?"** That is how a checklist is used, not memorised.

---

## Repository layout

```
.
├── SKILL.md                      Workflow skeleton, three scales, hard rules
├── references/
│   ├── evidence-ladder.md        Six-level ladder, three evidence types, paradigm pitfalls, statistical traps
│   ├── critique-checklist.md     Groups A–H, the three kinds of "first", inter-figure independence, panel classification
│   └── reading-template.md       12-question summary + the four claim-level verdicts
├── examples/
│   └── output-structure.md       Output skeleton
├── docs/
│   └── DESIGN.zh-CN.md           Design rationale (Chinese)
├── README.zh-CN.md               Chinese README
├── CONTRIBUTING.md
├── CHANGELOG.md
└── LICENSE
```

`references/` is loaded on demand: the main file does not consume every detail at once, it opens the relevant appendix when grading evidence, walking the checklist, or saving a note.

---

## Install

```bash
git clone https://github.com/xck0903/paper-judge.git
cp -r paper-judge ~/.your-agent/skills/
```

Or download the repository zip and unpack it into your skills directory.

Directory layouts differ between agents (WorkBuddy / Claude Code / Codex / anything that reads markdown instructions). The skill is pure markdown with no proprietary API dependency — **if the agent can read files and follow instructions, it works.**

Fill in the three lines under "Configuration" in `SKILL.md` once (field background, notes directory, default emphasis). You can also leave the file untouched and keep the preferences in the agent's memory.

---

## What the output looks like

See [`examples/output-structure.md`](examples/output-structure.md). In one sentence:

> A full four-part dissection (each figure located on the evidence ladder), then a discussion with you, then six scores and a saved markdown note where every judgment carries an anchor.

Every judgment carries an anchor like `Fig. Xc / p.N / SI Fig. SN` so you can check it against the source. **That is the floor of this skill: never write a sentence the user cannot verify.**

---

## Who it is for

- Graduate students and postdocs deciding whether a paper is worth following up
- Writers who need to cite something without misquoting its boundary
- Authors studying how high-level papers build a story
- Anyone presenting a paper at a group meeting or a defence
- Anyone who needs to balance respect for technical innovation against not being impressed by difficulty alone

## Who it is not for

- Anyone who wants a fluent summary — that is not the goal here
- Anyone who wants the AI to do the reading so they never open the paper — **the value of this skill rests on you checking the anchors**

---

## Design origin and acknowledgements

- The core criteria come from the author's own research practice in electron microscopy and electrocatalysis.
- The six-level evidence ladder, the three evidence types, per-panel classification and competing-explanation construction draw on critical-reading logic chains and peer-review practice circulating in the research community. No specific source text was copied.
- Contributions of additional measurement paradigms and failure cases are welcome.

## Disclaimer

This skill is a **reading aid**. It does not replace peer review, and it does not replace your own judgment. AI models make mistakes, including wrong anchors, wrong venue details and wrong author details. **Any decision affecting your experiments or your submission must be checked against the source.**

## License

[MIT](LICENSE)
