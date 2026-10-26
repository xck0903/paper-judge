# Changelog

This project follows [Semantic Versioning](https://semver.org/).

## [1.2.0] - 2026-10-26

### Changed

- **Language architecture split in two.** Instruction files (`SKILL.md`, `references/`) are now English and are the single source of truth. Introduction files are bilingual: `README.md` (English) and `README.zh-CN.md` (Chinese). A Chinese design note, `docs/DESIGN.zh-CN.md`, explains why each criterion exists.
- **Output language is now adaptive** (section 8). The skill writes in whatever language the user writes in, keeping technical terms in their original form. Previously the output was hard-coded to Chinese, which made the skill unusable by non-Chinese readers.
- `references/` rewritten in English with the same criteria, no rule removed. Length budgets are given in both words and characters so the proportions hold in either language.
- `examples/output-structure.md` translated to English; placeholders unchanged.

### Why not two translated copies of `SKILL.md`

Because they drift. Two copies of a rule set that are edited independently become two skills with different behaviour, and whichever copy an agent loads determines what it does. One source, one behaviour; translation belongs at the README level, where a stale translation costs a reader some confusion instead of corrupting a judgment.

## [1.1.0] - 2026-10-26

### Changed

- **Renamed `paper-review` → `paper-judge`.** The old name described the action (read it once); the new name names the product (a reading must end in a verdict). Reading is the means, the verdict is the output.
- **Description rewritten** to fix the output order — explain what the paper did, then judge — so the skill is not mistaken for a fault-finding tool. Added real intents such as "is this reliable" and "can I cite this" as triggers.
- **No alias kept for the old name.** Replace the skill directory with `paper-judge/` and delete the old one; there is no data to migrate.

## [1.0.0] - 2026-10-26

First public release.

### Core mechanics

- **Four parts, delivered in stages**: Part 1 venue and content (~30%) → stop and ask about figure-by-figure → Part 2 figure-by-figure (~50%) → Part 3 survey of techniques → Part 4 holes and suspect logic.
- **Three scales**: four levels per claim, strong/moderate/weak plus ladder rung per figure, four tiers per paper. The paper tier is set by its weakest critical claim.
- **Six-level evidence ladder**: direct signal → preprocessing → quantification and reconstruction → statistical association → mechanism → causation.
- **Three evidence types**: direct observation / indirect inference / mechanistic interpretation, used alongside the three-layer source label (as claimed / my inference / to be verified).
- **Pitfall checklists organised by measurement paradigm**: imaging / spectroscopy and diffraction / electrochemistry and performance / mechanics, thermal and devices / computation. Not bound to any discipline.
- **Mandatory competing-explanation construction**: two alternatives per core claim, plus the experiment that would discriminate them — not merely checking whether the authors excluded them.
- **Three kinds of SI close-reading**: what supports a core claim, what matches the user's direction, and what contradicts the paper (failed experiments, missing signals, admitted limitations).
- **Anchors are mandatory**: every judgment carries figure, panel and page. No anchor, no claim.

### Workflow

- Pick an emphasis before reading (default close read / experimental method / data analysis and reasoning / writing and figures / citing / challenging); emphasis weights the output, it never skips a part.
- After the four parts: multi-round discussion, then a 6-dimension × 5-point score, then save.
- The saved note opens with the 12-question summary, followed by the full four parts, the final tier and the score table.

### Engineering

- Split into `SKILL.md` plus three `references/` appendices, loaded on demand so the main file does not grow with every iteration.
- Configuration (field background / notes directory / default emphasis) is decoupled from the criteria, keeping the file generic and shareable.
