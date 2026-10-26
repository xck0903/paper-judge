# Evidence Ladder and Pitfall Checklists

Before grading evidence strong / moderate / weak, locate the rung it stands on and where it was substituted. **When judging a figure, locate the level first, then check the usual substitution at that level.**

## 1. The six-level evidence ladder

| Level | What happens here | What to ask | Usual substitution |
|---|---|---|---|
| **1 Direct signal** | What the instrument actually recorded: scattering intensity, mass spectrum, current, spectral peak, image projection | What is the raw record? Was it calibrated? Can it be reproduced? | A processed, good-looking image presented as the raw signal |
| **2 Preprocessing** | Denoising, background subtraction, peak fitting, registration, AI restoration / super-resolution | How does each step alter the signal? Could it manufacture structure out of nothing (especially CNN denoising and AI inpainting)? | Periodicity or artificial contrast introduced by processing, then read as "structure" |
| **3 Quantification and reconstruction** | Atom counting, coordination number, 3D coordinates, phase fractions, strain maps | What geometric prior, physical model or algorithm parameter does it depend on? Does the conclusion survive a change of parameter? | Algorithm parameters undisclosed; the reconstruction's built-in assumptions presented as observed fact |
| **4 Statistical association** | Which groups were compared? What is n? How many independent repeats? How large is the error? | Is the independent unit a particle, a batch, or an atom? Are the error bars SD or SEM? | Thousands of atoms inside one particle treated as thousands of independent experiments |
| **5 Physical / chemical interpretation** | Why a structural metric maps onto adsorption, electronic state, barrier height, deactivation | Was the intermediate link actually measured, or is it "well known"? | The intermediate step never measured, filled in from literature common sense |
| **6 Causation and generality** | Controlled intervention, controls, repeats, independent characterization | Can other mechanisms be excluded? Does it hold in another system? | "Two quantities move together" upgraded to "one causes the other" |

**Two hard floors**

- Never derive causation directly from two quantities co-varying.
- Never describe reconstructed or fitted atomic coordinates as a filmed, atom-by-atom trajectory.

## 2. Three evidence types, kept distinct

| Type | Definition | Capability |
|---|---|---|
| **Direct observation** | Signal the instrument delivers and that reproduces after reasonable calibration | Strongest, but covers only what the instrument measures |
| **Indirect inference** | A non-observable variable derived from image intensity, fitting, statistics or a structural model | Only as strong as the model; the dependency must be stated |
| **Mechanistic interpretation** | A causal narrative supported by correlation, prior theory or computation | Weakest; must be tested for uniqueness |

**How this differs from the three-layer labelling**: the three-layer label (as claimed / my inference / to be verified) asks **who is speaking**; the three evidence types ask **what kind of evidence this is**. Label both; neither substitutes for the other.

## 3. Measurement pitfall checklists (matched by paradigm)

Do not look these up by field. Look them up by **the measurement paradigm this paper uses**. Every category answers the same question: **is the instrument seeing the sample, or seeing itself?**

**Imaging** (microscopy, tomography, optical, high-speed photography)
- Irradiation or illumination damage: what dose? Is there an unirradiated control?
- Drift and rotation: how was it corrected? Could the correction itself erase real change?
- Aberration, defocus, focus drift: is the contrast structure, or an imaging condition?
- Projection: a 2D projection integrates 3D; intensities in thin and thick regions are not directly comparable
- Surface contamination build-up: a growing contamination layer can fake an "evolution" trend
- Authenticity of in situ conditions: is the local pressure, temperature or field really what was set? Is the measurement point affected by the holder, the window, the heater?
- Beam-induced sintering and mass transport: is the observed change thermodynamic or beam-driven?
- Sampling bias: how were objects selected? Were only the best-looking ones reported? Were the tracked ones only "the survivors"?

**Spectroscopy and diffraction** (XPS / XAS / Raman / IR / NMR / MS / XRD)
- Charging and baseline: how was charge correction done? How was the baseline chosen? How much does peak area change with a different baseline?
- Fitting constraints: are peak number, shape and width measured or imposed? Does the conclusion survive a change of constraint?
- Peak overlap: can the assignments of two components be swapped?
- Quantification factors: do the sensitivity factors, cross-sections and probe depth apply to this sample?
- Sampling position and time: only the most representative spot measured? Did the beam or laser itself alter the sample?

**Electrochemistry and performance testing**
- iR compensation and reference calibration: how much was compensated? How was reference drift controlled?
- The denominator in normalization: geometric area, ECSA, or loading? Does the conclusion change with the denominator?
- Mass transport and bubbles: is this intrinsic activity, or a transport ceiling?
- Stability duration and duty: how many hours? How far from real operating conditions?
- Benchmark: compared against whom? Was that "best literature value" measured under the same conditions?

**Mechanics, thermal, devices**
- Fixture and contact: are contact resistance or thermal resistance included? Is the interface the dominant term?
- Calibration and hysteresis: how often is the sensor calibrated? How much lag do ramp rates introduce?
- Size effects: the smaller the specimen, the larger the boundary contribution

**Computation and simulation**
- Functional, force field, cutoff, cell size: was a convergence test done?
- Sampling and configurations: how long, how many independent trajectories, or only the prettiest one reported?
- Model priors: are the initial structure, symmetry and charge state set or solved for?
- Relation to experiment: an independent prediction, or a necessary modeling step to get a structure out of the data?

**If the paper's paradigm is not in these five** → write your own group in the same sentence form: "what else could fake this instrument's reading?" **That is how a checklist is used, not memorised.**

## 4. Model sensitivity (mandatory for any reconstruction)

If the model depends on symmetry, atom-count conservation, a potential function, an initial structure or a regularization strength, ask for each: **change this prior, does the main conclusion survive?**

Related check: can several different processes produce the same final statistical distribution? **A distribution shift is not a per-object transition** — "fewer low-coordination sites, more high-coordination sites" is not "low-coordination sites turned into high-coordination sites one by one".

## 5. Statistical and numerical traps

- **Percentage points ≠ percent**: going from 92.3% to 91.0% is a drop of 1.3 percentage points, not 13%.
- **Stratify n**: particle-level, batch-level and atom-level are different. Atoms within one particle are not independent.
- **Error bar meaning**: SD, SEM and 95% CI are three different things; never blur them.
- **Effect size beats p-value**: a small p does not mean a large difference; pile on samples and a trivial shift turns significant.
- **"Reversible" has three meanings**: (1) atom trajectories return to the original; (2) the overall distribution returns to the initial; (3) the before/after difference is not significant. **Not significant is not equivalent** — especially with a small sample.
- **"Stable" needs a duration**: for how long was it measured? Was it extrapolated to operating conditions?

## 6. The role of computation

- Structural relaxation, electronic structure, adsorption energy and reaction barrier are **four different things** — do not merge them.
- Classical MD ≠ DFT ≠ proof of a reaction pathway.
- Distinguish computation as **independent verification of an experiment** from computation as **a required modeling step to extract structure from the data** — the latter is not independent evidence.
