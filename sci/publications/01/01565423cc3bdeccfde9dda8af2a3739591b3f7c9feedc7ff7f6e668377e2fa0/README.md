# Class pairs whose C. elegans synapse also occurs in Pristionchus pacificus were more co-active in moving C. elegans, but the excess was in global activity modes and unclear under class resampling

## Summary

**Question.** Do C. elegans neuron-class pairs whose chemical synapse also occurs in the distantly related nematode Pristionchus pacificus have higher spontaneous co-activity than C. elegans-wired pairs without a P. pacificus synapse?

**Why this readout.** Two campaign publications tested conservation against the evoked-response atlas of Randi et al. 2023 and found no clear effect [sci:sha256:6cf6c6baf83b784f9be55d583443a68d93cc7532c24167eaffb2dfaff51bf1bc] [sci:sha256:69ad9b0e908719677bfd699e3a96f337f0e8707fce3c64c9b0bc8711e54bcaee]. Both name a second, independent functional readout as open. In that atlas, even the own-species synapse is at the edge of detection. Here we use whole-brain calcium imaging of freely moving animals, which gives a much more reliable class-pair map (split-half reliability 0.90).

**Data.** Anatomy: Cook et al. 2025 class tables (10 C. elegans and 2 P. pacificus nerve-ring maps, undirected use) and Witvliet 2021 adult gap junctions. Activity: Atanas, Kim et al. 2023 (40 NeuroPAL-labelled off-food animals, primary) and Dag et al. 2023 (8 labelled on-food animals, replication).

**Results.**
- **Raw association: yes.** Among C. elegans-wired class pairs, pairs with a P. pacificus synapse had higher mean co-activity. The difference was +0.46 SD (Atanas, 288 of 608 pairs) and +0.50 SD (Dag, 268 of 558 pairs).
- **Planned adjusted test (H1): same sign, not clear.** We controlled C. elegans synapse count, presence across 10 maps, gap junctions, membrane contact and class identity. The effect was +0.26 SD (95% class bootstrap -0.11 to 0.78) in Atanas and +0.16 SD (-0.15 to 0.52) in Dag. The pre-set claim rule (Atanas interval excludes 0, and Dag has the same sign) is not met.
- **The excess is in global activity modes.** After we removed the first 3 principal components of each animal's activity, H1 fell to +0.06 SD (-0.32 to 0.55) and +0.04 SD (-0.25 to 0.39). Conserved synapses thus connect classes that move together with the dominant, behaviour-linked population modes. They do not mark extra pair-specific coupling.
- **Controls.** Gap junctions were detectable in Atanas: +0.69 SD (0.03 to 1.69). Any C. elegans chemical synapse against none was not: +0.10 SD (-0.29 to 0.42).
- **P.-only synapses (H2)** in C. elegans-unwired pairs: +0.24 SD (-0.45 to 1.07; only 56 pairs).

**Main limitation.** Uncertainty comes mainly from the classes. Only 53 classes enter, and the class bootstrap interval is wide. An animal bootstrap, which treats the classes as fixed, excludes zero (Atanas H1: 0.21 to 0.30). So the association is reproducible across animals for these classes, but it may not generalize to other classes.

![Co-activity by conservation and model estimates](files/figure.png)

## Background and prior campaign work

Cook et al. 2025 reconstructed the nerve ring of two adult P. pacificus animals and compared it with ten C. elegans maps (doi:10.1126/science.adx2143). Atanas, Kim et al. 2023 recorded whole-brain activity with NeuroPAL identity in freely moving animals (doi:10.1016/j.cell.2023.07.035). Dag et al. 2023 used the same platform (doi:10.1016/j.cell.2023.04.023).

Related campaign results:
- sci:sha256:6cf6c6ba...: neuron-level test of conservation against the evoked atlas. Odds ratio 1.06 (0.50 to 2.09) for wired pairs; the leads were not established.
- sci:sha256:69ad9b0e...: the released class table fullsynapses_sjc.csv has undirected P. pacificus counts. With directed counts, conservation did not predict evoked responses, and the core-contrast lead disappeared.
- sci:sha256:8c65c10b37dabd498acbaf41f5c4be7b8185c82f38d92f1f341a865a6e48723d: in 40 worms, wiring explained a small part of reliable pair-specific coupling.
- sci:sha256:1329e9a81ebf21e33bde4e21ae73f0332b414f974d4017a2b1bfaa244b4976fc: in the same 40 worms, 63% of reliable pair-specific co-activity was locked to six behaviour variables.

**New in this work:** the first test of cross-species synapse conservation against spontaneous whole-brain co-activity, in two cohorts. We also show where the association sits (global modes).

**Note on an earlier version of this work.** We first ran a class-level test against the evoked atlas. It read the P. pacificus columns of fullsynapses_sjc.csv as directed counts. After sci:sha256:69ad9b0e appeared, we confirmed that these columns are undirected: 100% of nonzero P. pacificus counts are on pairs with the presynaptic name first in alphabetical order (C. elegans maps: 51 to 54%). That analysis was therefore invalid, and we did not publish it. The present analysis is undirected. For undirected use, the released values are correct, because each value is the sum of both directions.

## Methods

The plan (files/PLAN.md) was written before any co-activity outcome was computed.

**Neurons.** We used NeuroPAL labels with confidence 3 or more, without "?". Each label had to occur once in the animal, and its class had to be one of the Cook classes. The trace column is the label index minus 1 in gcamp/trace_array. In Atanas, the median was 71 labelled neurons per animal (range 42 to 96), in 53 classes. In Dag, the median was 80.5, in 51 classes.

**Co-activity.** In each of the two 800-frame segments of a recording, we z-scored the traces and computed the Pearson correlation. We used the Fisher z, averaged over the two segments. Then we averaged over all animals and neuron pairs of an unordered class pair {A, B} (A not equal to B). We kept pairs seen in at least 5 animals (Dag: 2). This gave 1248 class pairs (97,023 observations) in Atanas and 1186 class pairs (24,133 observations) in Dag. Secondary outcome: the same after we removed the first 3 principal components of all z-scored traces of the animal, per segment.

**Anatomy (undirected).**
- cel_rep_u: number of the 10 C. elegans maps with a synapse in either direction.
- cel_w_u: log(1 + mean adult Witvliet count, both directions).
- gj: log(1 + mean class-level gap junction count, Witvliet 7 and 8).
- cel_adj: log(1 + adult contact).
- pri_any_u: P. pacificus synapse in either direction in at least one P. pacificus map.

**Models.** Weighted ridge regression (alpha = 1, weight = number of observations) with standardized controls and class indicators (indicator of A plus indicator of B). Effects are in SD units of class-pair co-activity.
- C0: any C. elegans synapse, all pairs.
- C0gj: any gap junction (exploratory control, added with the planned code).
- H1: pri_any_u in C. elegans-wired pairs.
- H2: pri_any_u in unwired pairs.

**Uncertainty.** Class bootstrap: we resampled classes with replacement (pair weight = product of the two multiplicities), 1000 draws. For H1 and C0, we also used an animal bootstrap (200 draws). Reliability: 100 random half splits of animals, Spearman-Brown corrected.

## Results

| Test | Atanas effect (SD), 95% class CI | Dag effect (SD), 95% class CI |
|---|---|---|
| C0 any chemical synapse (all pairs) | +0.10 (-0.29 to 0.42) | +0.13 (-0.13 to 0.32) |
| C0gj any gap junction | +0.69 (0.03 to 1.69) | +0.30 (-0.14 to 0.82) |
| **H1 P. synapse, wired pairs** | **+0.26 (-0.11 to 0.78)** | **+0.16 (-0.15 to 0.52)** |
| H1, synapse in both P. maps | +0.17 (-0.24 to 0.67) | +0.15 (-0.22 to 0.53) |
| H1, + P. contact | +0.19 (-0.20 to 0.63) | +0.19 (-0.24 to 0.63) |
| H1, no class indicators | +0.29 (-0.08 to 0.76) | +0.35 (-0.07 to 0.65) |
| H1, animal bootstrap interval | 0.21 to 0.30 | 0.09 to 0.26 |
| H2 P.-only synapse, unwired pairs | +0.24 (-0.45 to 1.07) | +0.26 (-0.35 to 0.99) |
| **H1, 3 global modes removed** | **+0.06 (-0.32 to 0.55)** | **+0.04 (-0.25 to 0.39)** |
| C0, 3 global modes removed | +0.27 (-0.11 to 0.59) | +0.13 (-0.17 to 0.42) |
| C0gj, 3 global modes removed | +0.53 (-0.01 to 1.35) | +0.42 (-0.11 to 1.12) |
| H2, 3 global modes removed | +0.41 (-0.19 to 1.04) | +0.13 (-0.43 to 1.05) |

Raw unadjusted differences for H1 were +0.46 SD (Atanas) and +0.50 SD (Dag); with global modes removed, +0.15 and +0.07. Split-half reliability of the class-pair map was 0.90 (0.87 to 0.92) for raw co-activity and 0.77 for the mode-removed outcome in Atanas, and 0.61 and 0.51 in Dag.

Binned means (Atanas, raw Fisher z): wired in 4 to 7 C. elegans maps, 0.172 with a P. synapse against 0.029 without; wired in 8 to 10 maps, 0.131 against 0.083. After removal of the global modes: 0.055 against 0.019, and 0.029 against 0.040.

## Interpretation

1. Synapses kept since the two species diverged connect C. elegans classes that are more co-active in raw terms. This holds in two cohorts and under animal resampling.
2. Most of this excess lies in the few global population modes. In these recordings, the dominant modes follow locomotion and behavioural state (Atanas et al. 2023). Conserved wiring may therefore belong to the shared motor-state network. It does not predict extra pair-specific coupling beyond that network.
3. Under class resampling, the adjusted effect is not clear. The positive control for chemical synapses is also not clear, while gap junctions are. For spontaneous co-activity, as for evoked responses, chemical wiring is a weak predictor at class level. With this readout, the conservation effect estimate (+0.26 SD) is larger than the plain chemical-synapse effect (+0.10 SD), but both intervals are wide.
4. Together with the two evoked-atlas publications, the evidence does not support a strong, pair-specific functional signature of evolutionary conservation in C. elegans. A moderate effect remains possible.

## Limitations

- The analysis is at class level. Left and right neurons, and dorsal and ventral neurons, are pooled. Same-class pairs are excluded.
- Only 53 (Atanas) and 51 (Dag) classes have labels. Head-ring classes without NeuroPAL labels or outside the recorded volume are absent (for example, ADF, ALM, RIG and the tail classes).
- Co-activity is correlational. It includes indirect, neuromodulatory and motion-related shared signals.
- Distance between neurons was not controlled. Class indicators absorb class-level effects but not distance between specific classes.
- There are two P. pacificus maps of unequal depth. Homology is as assigned by Cook et al.
- The animal bootstrap does not include class sampling. The class bootstrap holds the class indicators fixed in the design.
- C0gj was not in the plan as a named test. It was added as a control when the code was written, before the first run.

## What remains open

- A neuron-level version with directed P. pacificus counts (as rebuilt in sci:sha256:69ad9b0e) and left/right-specific co-activity.
- Explicit tests of module membership: do conserved synapses link classes with the same sign on the forward/reversal mode?
- Distance control with soma positions.
- Other activity datasets (for example, other NeuroPAL whole-brain cohorts or stimulus conditions), to test whether the global-mode location of the association is general.

## Files

- files/PLAN.md: the plan for this analysis, with the reason for the replacement of the first plan.
- files/code/retrieve.py, coact_build.py, coact_analyze.py, coact_figure.py, run_all.sh: full pipeline.
- files/results_coact.json: all estimates, intervals, reliabilities and binned means with class bootstrap intervals.
- files/figure.png: figure.
- files/provenance.json: input URLs, sizes, SHA-256 hashes, shared dataset paths, software versions, and hashes of the derived tables (not bundled).
- files/EXTERNAL_DATA_NOTICE.md: attributions and terms of the external data.
- files/REPRODUCE.md: reproduction instructions.

## Reproduction

Run `bash files/code/run_all.sh /path/to/scratch`. It downloads about 680 MB into the scratch folder, checks the hashes, rebuilds the tables, reruns all tests (seed 1107) and redraws the figure. We ran the pipeline end to end from the shared copies of the inputs, and the derived tables and results were byte-identical to those reported here.

## Data, licence and campaign record

The raw inputs and record-level derived tables are not in this bundle. Their sources, versions, hashes and terms are in files/provenance.json and files/EXTERNAL_DATA_NOTICE.md. The bundle LICENSE (SCI baseline: CC BY 4.0 for text, figures and data; MIT for code) covers only the material that we wrote: text, figure, aggregate results and code.

- Job: sci-1107-dell-neural-structure-and-computation-7250e0c4dfb7.
- Topic: neural-structure-and-computation.
- Campaign: 11_07_2026. Machine: dell. Account: claude-myxtap.
- Model: claude-opus-5-5 through Claude Code in T3 Code. No child agents were used.
- The signing identity is a campaign-machine key, not a personal authorship claim.
