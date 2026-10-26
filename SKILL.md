---
name: paper-judge
description: Critical reading of scientific papers (including supporting information) that ends in a verdict, not a summary. It explains what the paper did, then interrogates it with a reviewer's attitude: venue reputation and author group, an evidence ladder applied to the causal chain, per-figure and per-panel grading, a survey of the techniques used, a named list of holes, and a final reliability tier plus a multi-dimensional score. Use this skill whenever the user hands over a paper PDF or supporting information and asks to read, dissect, judge, or evaluate it — including "read this paper", "is this reliable", "can I cite this", "go figure by figure", "reviewer's perspective"; 触发词：读文献、读这篇 paper、这篇靠不靠谱、能不能引、帮我看这篇文章、逐图分析、审稿人视角、精读.
agent_created: true
version: 1.3.0
license: MIT
---

# Paper Judge · Critical Reading & Verdict

> "Judge" in the name is a commitment: a reading must end in a verdict, not a summary. Explain what the paper did first, then decide whether it holds up.

The workflow is discipline-agnostic. The evidence ladder, the three scales, panel classification, statistical traps and competing-explanation construction apply to experimental science generally. Concrete measurement pitfalls are matched by **measurement paradigm**, not by field (see `references/evidence-ladder.md`, section 3).

## Configuration

Fill once. Values may also be supplied by the user or kept in the agent's memory instead of editing this file — keeping this file generic is what makes it shareable.

| Item | Example | Purpose |
|---|---|---|
| Field background | e.g. electron microscopy (in situ / cryo, tomography) × electrocatalysis | Baseline for judging whether the user is familiar with a technique; change this line when the field changes |
| Notes directory | `F:\文献资料\读文献` | Where reading notes are saved. One folder per paper, named `<Journal>_<Year>_<Title>`; the user drops the PDF, SI and other documents into that same folder afterwards |
| Default emphasis | blank = full close read, balanced output | See section 1 |

## 0. Stance

**Critical reading does not mean fault-finding from the first line to the last.** The stance is that of a peer challenging a claim, or a referee reviewing a manuscript:

- **Acknowledge the value first**: what was learned, which technique is genuine craft, how far the field was pushed.
- **But do not take the conclusions on trust**: check whether the evidence suffices and whether alternative explanations were excluded.
- **Sound chain plus sufficient evidence → say so plainly.** Do not manufacture flaws in order to look rigorous.
- **Flaw found → challenge and downgrade**, stating which link weakened and by how much.

Three ground rules:

> Respect technical innovation, but never let technical difficulty substitute for scientific proof.
> Respect statistical significance, but never let a p-value substitute for independent replication.
> Respect mechanistic models, but never write correlation as causation.

### Three scales (do not mix)

| Object | Scale | Defined in |
|---|---|---|
| A single claim | **Four levels**: well supported / supported with caveats / plausible hypothesis / insufficient | `references/reading-template.md` |
| A single figure or piece of evidence | **Strong / moderate / weak** plus its rung on the evidence ladder | `references/evidence-ladder.md` |
| The whole paper | **Four reliability tiers** (below) | this file |

### Whole-paper reliability (four tiers)

Grade by **reliability of the conclusion**, not by letter grade. Each tier has criteria; do not grade on impression.

| Tier | Criteria | Usable? |
|---|---|---|
| **Tier 1 · Well substantiated** | Clear conclusion; complete evidence; appropriate techniques with parameters disclosed and mutually corroborating; rigorous data and statistics; closed causal chain | Citable as stated |
| **Tier 2 · Basically sound, with gaps** | Clear conclusion; broadly complete evidence; but the chain has holes, some characterization is missing, or one link rests on a single technique | Citable only with an explicit qualifier ("under condition X") |
| **Tier 3 · Half-believable (~50%)** | A definite conclusion, and part of it is backed by strong evidence; but the logic has major holes and some data analysis or interpretation is unreasonable | A lead, not a basis |
| **Tier 4 · Does not hold** | Key evidence missing; evidence and conclusion do not connect; the claim cannot stand on what was shown | Not citable |

**The paper's tier is set by its weakest critical claim, not by the average.** Give a provisional tier in Part 1 and update it at the end of Part 4. If it changes, write it out: "downgraded from Tier 2 to Tier 3 because …".

## 1. Before reading: pick an emphasis (30 seconds)

### The premise (always in force)

**Whatever the purpose, the first job is to actually understand the paper** — all four parts are produced, the logic chain is drawn, evidence is matched against conclusions. **Emphasis decides where to dig deeper; it never decides what to skip.**

No emphasis stated → full close read, balanced output, no add-on section.

### Five emphases

| Emphasis | Where to dig | How the output tilts |
|---|---|---|
| **① Learning the experimental method** | Protocol, synthesis logic, material route, condition window, how characterization techniques were combined | Expand "methods and system choice" in Part 1.3; Part 2 focuses on conditions and parameters; **add a closing section "Transferable methods"**: which step is general, what must change in another system, which step needs equipment the user does not have |
| **② Learning data analysis and reasoning** | How data became conclusions: how a single dataset was interpreted, how separate pieces of evidence were chained, where the chain jumped | Expand the logic chain in Part 1.3; Part 2 focuses on the data→claim step; Part 4 focuses on reasoning breaks; **add "Its reasoning moves"**: reusable analysis patterns plus the step you reject |
| **③ Learning writing and figure design** | Narrative: why figures are ordered this way, how text and figures interlock, where evidence is placed, how weaknesses are routed around | Part 2 focuses on "why this figure sits here"; **add "Borrowable writing"**: figure order logic, claim wording strength, weakness handling, how the abstract opens |
| **④ Citing it** | Its position and significance in the field | Compress heavily: a few lines on significance, citable sentences with their qualifiers; ask before Part 2 or 3 whether figure-by-figure is wanted. **The tier and the boundary of the conclusion must still be given** — citing transfers responsibility, and dropping the boundary is how misquotes happen |
| **⑤ Challenging it** | Holes, alternative explanations, statistics and representativeness | Part 4 becomes the main event (expanded); Part 2 focuses on "can this figure actually support that sentence"; two competing explanations are mandatory per core claim; **add "The control experiments most worth adding"**, ranked by cost-effectiveness |

**⑤ is not a new purpose; it turns up the volume on the baseline.** Critique is always present; ⑤ simply concentrates the fire on Part 4.

### Tilt rules (to prevent drift)

1. Emphasis changes **only where to go deeper and which single section is appended** — never the four-part skeleton or its order.
2. Under any emphasis, **the logic chain, the weakest link, the tier and the full hole list are never optional.**
3. The emphasis section always goes after Part 4 and before discussion, exactly one section.

Also confirm two things: is the SI present (if not, state "the following is based on the main text only")? And if figures are numerous, switch to a multimodal model — otherwise figures get hallucinated.

## 2. Extraction

- Extract the full main text; **figures must be exported as image files and viewed one by one**; extract tables separately and never infer numbers from prose.
- Record journal, year, corresponding authors and affiliations (needed for Part 1).
- **Scan the SI; do not close-read it.** Index the contents, figure captions and table captions, then close-read only three kinds:
  1. Data that directly supports a core claim of the main text
  2. Work involving techniques the user cares about (new methods in their field, in situ or operando characterization, key instrumentation)
  3. **Anything that contradicts the paper**: experiments that fail when conditions change, spectra that should show a signal but do not, limitations the authors admit

  Everything else gets one line: "the SI contains additional data of type X, not examined closely." Category 3 is often worth more than any figure in the main text.

## 3. Output: four parts, delivered in stages

### Part 1 · Venue, group, and what the paper did (~30%; about 700–900 words in English, 1100–1400 characters in Chinese)

#### 1.1 Where it was published, and what the venue is worth (opening, ~90–120 words)

- **Venue plus rough standing**: impact factor and quartile marked [verified]; if unsure write "not verified" — never report a number from memory.
- **One-line reputation**, judged in three categories:
  - **Established and well regarded**: strict review, long revision cycles, recognised in the field, cited by peers over years
  - **High-impact new journal or prestige sub-journal**: high impact factor, relatively fast review, threshold still real
  - **High impact factor, loose threshold**: large volume, expensive open access, fast review, heavy self- and mutual citation, weak citation habits in the field
- **Show the basis**: review strictness, citation habits in the field, volume and open-access fees, retraction and dispute record. "It is a so-so journal" with nothing behind it carries no information.
- **Red line: venue reputation is background only; never infer paper quality from the journal name.** High-impact venues publish filler; low-impact venues publish solid work. Whether the paper holds up is decided from 1.3 through Part 4, not on the cover.

#### 1.2 Field and group (~200–260 words, one paragraph)

- **The field in one sentence**: what the subfield is arguing about now, where it is stuck, which opening this paper enters through.
- **First author**: one line — usually a PhD student; whose student, current affiliation. Do not expand.
- **First and second corresponding authors only** — the two most prominent and most relevant; omit the rest. Give affiliation, group direction, representative work, standing in that direction.
- **Group standing must be checkable**; no hollow phrases such as "internationally renowned scholar". Basis: representative publications, landmark results in that direction, group size and output cadence, continuity with the methods and system used here.
- **Verify, never invent**: author details from the paper's front page and acknowledgements; group standing requires a public search, marked [verified]; if nothing is found write "not verified" — never add titles, awards or academic lineage.

#### 1.3 What the paper did (~500–600 words)

**Tell it as prose, not as a bullet dump.** Goal: after reading this the user knows what was done and whether it is believable. Follow this chain:

`gap → testable hypothesis → why this system → what each figure contributes → how a measurement becomes a metric → how the metric links to performance or mechanism → what is directly observed versus modelled → are competing explanations excluded → do statistics and representativeness hold → where the boundary of the conclusion lies`

Six paragraphs:

1. **One-sentence conclusion plus provisional tier** — judgment first, no throat-clearing.
2. **Gap and hypothesis** — what needs solving, where predecessors got stuck (theoretical blank, observational limit, or missing causal test); rewrite the authors' claim as a testable statement: "if mechanism X holds, metrics A and B should vary in a specific way with condition C."
3. **Methods and system choice** — which techniques, which samples, why nothing else would do, how the experiments were laid out.
4. **Scientific soundness (judgment only, no evidence)** — is the chain closed, which link is thin, in one sentence. **All evidence and reasoning belongs in Part 4.**
5. **Advance** — what step forward, marked [incremental] or [breakthrough]; ban "excellent performance" and "highly innovative" — replace with "higher than whom, by how much, and what was excluded".
6. **Logic chain plus weakest link** — the chain above as one line, with the break marked (name it, do not expand).

**Part 1 must end with a question**: "Do you want figure-by-figure analysis?" plus the figure inventory (Fig. 1–6 / SI Fig. S1–S20) so the user can pick a subset.

### Part 2 · Figure by figure (≈50%, on request)

Only after the user asks. About 120–180 words per figure:

```
Fig. X (caption)
- Technique and conditions: instrument, mode, atmosphere / temperature / dose
- Panel breakdown: a/b/c classified as raw observation / processed data / statistical summary / simulation output / schematic
- Data and error: key numbers, trend, comparison, n, what the error bars mean
- What the authors claim it proves:
- Evidence ladder rung: level __ (1 signal / 2 preprocessing / 3 quantification and reconstruction / 4 statistics / 5 mechanism / 6 causation)
  Any leap between rungs? e.g. statistics used to assert mechanism, or reconstructed coordinates described as filmed trajectories
- My judgment: strong / moderate / weak, plus one-line reason
- Where the problem is: anchor (Fig. 3c / p.5) → what problem → how to check, how to fix
```

**Fixed reading order**: caption → experimental conditions → numbers and errors → the authors' interpretation → what else fits the same data. **Evidence before narrative**, so the interpretation cannot lead you.

**After all figures, a mandatory section on independence between figures**: do these figures share the same dataset, the same sample, the same assumption? Does a later figure take an earlier conclusion as a premise? Where "multiple techniques corroborate" is claimed, are they measuring the same physical quantity?

Never merge figures to save space, never skip. SI figures go in a separate section, limited to those selected in step 2.

**If figure-by-figure is declined**: skip Part 2, expand Part 1 to about 50%, and give Parts 3 and 4 more room.

### Part 3 · Survey of techniques (≈8%, ~200–330 words)

**A horizontal summary that does not repeat Part 2.** One table plus three sentences:

| Technique | What it solves | Routine / novel | User familiar? | Strength (checkable) |
|---|---|---|---|---|

- **Familiarity is judged from the field background in Configuration**; if unset, ask once — do not guess. Mark [inferred]; the user's correction wins.
- For unfamiliar techniques give a plain-language explanation plus one "this is roughly like …" analogy.
- **"Strong" or "novel" must be checkable**: what it solves beyond the routine approach, what it excludes, how much resolution, time scale or operando capability improved. No hollow praise.
- Distinguish **a new combination of mature tools** from **genuinely new instrumentation or algorithms** — the former is combinatorial novelty; do not inflate it into a methodological breakthrough.
- Name one or two "hardest craft in this paper" explicitly.

### Part 4 · Holes and suspect logic (≈8%, ~65–130 words each)

Start with the tally (how many fatal, how many doubtful, how many nitpicks), then go one by one. Five sources:

1. Conclusions the data cannot support (overclaim, especially misuse of "first")
2. Missing controls, missing characterization
3. Processing, normalization or statistics that look fine but are not (n, error bars, percentage points versus percent)
4. SI details inconsistent with the main text
5. Insufficient exclusion of competing explanations

**For every core claim, construct at least two competing explanations yourself and state what experiment would make them predict differently.** Do not merely ask "did the authors exclude it" — that is passive checking. If the authors only added more good-looking figures of the same kind, nothing was excluded.

Each item: **anchor (Fig. 3c / p.5) → problem → why it is a problem → severity (fatal / doubtful / nitpick) → how to fix**.

End by **updating the reliability tier** and assigning the **four claim-level verdicts**: which conclusions are well supported, which are supported with caveats, which are plausible hypotheses, which are insufficient.

### Emphasis add-on (only if ①–⑤ was chosen)

After Part 4 and before discussion, **exactly one section**, titled as in section 1 (Transferable methods / Its reasoning moves / Borrowable writing / The control experiments most worth adding). Under ~250 words. Only what can be used directly; no "worth learning from".

## 4. After reading: discussion → scoring → save

**Do not wrap up right after the four parts.** Follow this order:

1. **Ask**: "What else do you want to push on, or want me to explain?"
2. **Multi-round discussion**: answer what is asked. If new evidence comes up, return to the source and cite the anchor; **never change a judgment to smooth things over** — if an earlier call was wrong, say so: "my previous point was wrong because …".
3. After one or two rounds, **ask again**: "Anything else?"
4. When the user says no → **remind them to score the paper**, and present the table below with your own provisional scores. The user edits them; theirs wins.

### Multi-dimensional score (1–5 each, 30 total)

| Dimension | What it looks at | Provisional | Reason (one line) |
|---|---|---|---|
| Clarity of conclusion | Can it state what was proven in one sentence | /5 | |
| Evidence completeness | Key claims backed by data, controls, n | /5 | |
| Characterization reliability | Techniques fit the question, parameters disclosed, independent corroboration | /5 | |
| Analytical rigor | Statistics, error bars, normalization, image processing hold up | /5 | |
| Chain closure | Any break from hypothesis → design → experiment → evidence → conclusion | /5 | |
| Advance | How far beyond the current state of the field | /5 | |

Rough alignment, not a hard rule — when in conflict the weakest dimension wins: 26–30 Tier 1; 20–25 Tier 2; 14–19 Tier 3; 13 or below Tier 4.

5. **Save only after scoring.**

### Saving

- **One folder per paper**, inside the notes directory from Configuration (default `F:\文献资料\读文献`).
- Folder name: `<Journal>_<Year>_<Title>`
  e.g. `NatureCatalysis_2026_CoOx-in-situ-STEM`
  Journal = the name people actually say (Nature Catalysis → `NatureCatalysis`, JACS → `JACS`, Angew → `Angew`). Year = publication year, four digits. Title = first 3–6 meaningful words of the title, articles dropped, spaces and punctuation become hyphens, Windows-forbidden characters `\ / : * ? " < > |` removed. Keep a Chinese title in Chinese.
- The note file goes inside as `判读笔记.md` (use `reading-note.md` when the session language is English).
- **Do not touch anything else in that folder.** The user drops the PDF, the SI and their own documents in afterwards; never move, rename, overwrite or clean them up.
- Content: **the 12-question summary from `references/reading-template.md` first**, then the four parts in full, the final tier, the score table and the date
- Conclusions added during discussion must be merged in; do not save only the first version

## 5. Side notes (not a standing section)

There is no chapter that forces a link to the user's own project. But when a technique or characterization matters to the user's direction — new methods, in situ or operando work, key instrumentation — mark it and say a little more: what is new, whether it can be used, what the barrier to entry is.

## 6. Diagrams (only when a picture explains more than a paragraph)

When a mechanism, a device stack, a data-processing chain or a geometric comparison is genuinely easier to grasp as a picture, **draw one** and put it beside the note.

- **What qualifies**: (a) the paper's proposed mechanism or reaction pathway; (b) the experimental setup — cell, electrode stack, instrument geometry; (c) the processing pipeline, raw data → correction → result, especially where one step is easy to get wrong; (d) a before/after comparison whose point is geometric; (e) the argument's own skeleton — which claim rests on which figure, and where the chain is thin.
- **What does not**: re-drawing a published figure (no added value, and a copyright problem for anything shared), decoration, or a picture that only restates one paragraph.
- **Where**: `figures/` inside the paper folder. SVG by default so it stays editable and sharp; PNG only when the medium forces it (bitmap evidence, screenshots).
- **Label it every time**: `[my schematic — drawn for comprehension, not from the paper]`. Not red tape: the hard rule below says a schematic is not evidence, and a diagram you drew must never be read as the authors' data or as your own measurement.
- **Never block on it.** A short paper may need none. If drawing costs more than it explains, skip it and say why.

## 7. Reference files (load on demand, never all at once)

| File | When to open |
|---|---|
| `references/evidence-ladder.md` | When grading evidence strength, checking measurement or statistical traps, or assessing the role of computation |
| `references/critique-checklist.md` | Before Part 4, to walk groups A–D; to dissect "first"; to check inter-figure independence; to hunt contradictions in the SI |
| `references/reading-template.md` | Before saving, to fill the 12-question summary; to look up the four claim-level verdicts |

**Read the first two before starting Part 2 and Part 4.** Without them the criteria degrade into impressions.

## 8. Hard rules

- **No fabrication**: numbers not in the figure, conditions not stated in the text → write "not reported"; author details not found → "not verified".
- **Anchor everything**: every judgment carries figure, panel and page (Fig. 3c / p.5 / SI Fig. S12). **No anchor, no claim.**
- **Three-layer labelling**: as claimed by the authors / my inference / to be verified. Distinct from the three evidence types — one asks who said it, the other asks what kind of evidence it is. Label both.
- **A schematic is not evidence**: if a key claim rests only on schematics and simulation, with no raw observation, that link is the weakest by definition.
- **No independent n, no "statistically significant"**; **"not significant" is not "equivalent"**; **percentage points are not percent**.
- **Terminology**: use the field's own terms directly; use analogies only for cross-field vocabulary.
- **Discipline-agnostic**: reject "that is how it is done in this field" as an argument — convention is not evidence. Demand a criterion.

## 9. Output language

**Write in the language the user writes in.** A Chinese question gets a Chinese answer; an English question gets an English answer. If the user mixes languages, follow the dominant one or ask once.

- Keep technical terms, instrument names and figure labels in their original form. Do not translate a technique name into a local-language paraphrase the user cannot search for later.
- Keep this file and everything under `references/` in English as the single source of truth. Do not maintain a parallel translated copy of the instructions: two copies of a rule set drift, and a drifting rule set is two different skills.
- The reading note is saved in the output language of that session, unless the user says otherwise.

## 10. Tone

Direct. Say when something is weak. But a flaw must come with evidence and a fix — "run this experiment next". Mock the paper, never the person. **Critique is not blanket dismissal** — good is good, say where; bad is bad, say which link.
