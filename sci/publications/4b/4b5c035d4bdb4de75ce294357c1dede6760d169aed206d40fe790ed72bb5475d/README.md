# Transcriptomic-like EM cell types do not remove the 4- to 7-fold excess of EM inhibition between interneurons over slice recordings in mouse V1

## Summary

An earlier SCI publication ([sci:sha256:999aa3ea…](sci:sha256:999aa3ea9cc47df6164773d528fc777358c9bb155162acf842a0c16c716b365e), "the EM–slice comparison" below) compared connection rates in the MICrONS electron microscopy (EM) volume with the rates in Allen Synaptic Physiology paired recordings from mouse primary visual cortex (V1) slices. At matched soma distance, slices found only 9 to 74 percent of the inhibitory connections onto interneurons that EM predicts. A second publication ([sci:sha256:62a5b936…](sci:sha256:62a5b93648b2487d8e85dd1679a03f5ebe229ccdd6000f154e4e69049bd899d2)) showed that missed small responses do not explain this. Both publications listed a mismatch between EM groups and Cre classes as an open cause. The EM–slice comparison put EM inhibitory axons into target-based groups (perisomatic, distal, interneuron-targeting) and used as interneuron targets only the 98 proofread inhibitory cells.

We tested the class-mismatch cause directly. We used MICrONS materialization v1507, which has 322 proofread inhibitory axons (3.3 times more), and the Allen metamodel cell types (BC, MC, BPC; Pvalb-, Sst- and Vip-like) for sources **and for all 7,856 typed single-soma interneurons as targets**. We wrote the test criteria before we compared any v1507 rate with physiology (`files/provenance/PROGRESS_log_and_preregistration.md`).

Main results:

1. **The class definitions disagree in part.** Of 207 proofread metamodel basket cells (BC), 54 (26 percent) are in the "Sst-like" distal-targeting group under the earlier rules. MC and BPC cells mostly fall in the expected groups (50 of 61 and 30 of 37).
2. **Metamodel types raise R but do not close the gap (primary test T1 failed for mismatch).** R is slice connections divided by EM-expected connections. For the four class pairs with the largest deficit, R changed from 0.14, 0.09, 0.12 and 0.09 (earlier work) to 0.24 (95% CI 0.14–0.35) for Pvalb→Sst, 0.18 (0.13–0.23) for Sst→Sst, 0.16 (0.06–0.31) for Vip→Pvalb and 0.14 (0.07–0.22) for Vip→Vip. All four upper limits are below the pre-set value of 0.5. Thus class mismatch is not the main cause. EM still predicts 4 to 7 times more of these connections than slices find.
3. **Layer matching (T2) did not change this.** R was 0.25, 0.18, 0.18 and 0.17.
4. **No relabelling of EM types can give the slice rates for Vip→Vip, and probably not for Sst→Sst or Vip→Pvalb (T4b).** We let every slice layer pair use the EM type pair (of BC, MC, BPC and NGC) with the lowest EM rate. This choice is more generous than any consistent relabelling. R was still 0.25 for Vip→Vip, 0.48 for Sst→Sst, 0.49 for Vip→Pvalb and 0.76 for Pvalb→Sst.
5. **No EM subpopulation matches the slice rates (T5, T6).** Only 1 of 56 MC axons (2 percent) had a distance-matched Sst→Sst rate at or below the slice rate, and 0 of 25 BPC axons for Vip→Vip. On the target side, a zero-inflated model permits at most 12.5 percent (Sst), 12.5 percent (Pvalb from Vip) and 40 percent (Vip) of target cells with no input. The slice data would need 82, 84 and 86 percent.
6. **The excess is specific to inhibition between interneurons.** Excitatory inputs onto the same EM target classes had R from 1.1 to 1.5. The double ratio R(I→T)/R(E→T) cancels target-side EM effects (for example, incomplete target dendrites). It was 0.16 (Sst→Sst), 0.10 (Vip→Vip), 0.11 (Vip→Pvalb) and 0.22 (Pvalb→Sst).
7. **Slices show a sharper version of the EM pattern (exploratory).** Across the nine inhibitory-to-interneuron class pairs, the slice and EM rates had the same rank order (Spearman ρ = 0.83, p = 0.005). But slice rates vary 18-fold (0.014 to 0.25), and EM rates vary only 3.2-fold (0.10 to 0.32). The log-log slope was 2.1.
8. **Synapse number per connection does not explain the pattern (post hoc).** When we count only EM connections with 2 or more synapses, several pairs move to R ≈ 1. But Sst→Sst (0.39), Vip→Pvalb (0.33) and Vip→Vip (0.44) stay low, and excitatory controls go to R = 2.8 to 9.8. A model with one per-synapse detection probability q for all nine inhibitory-to-interneuron pairs failed (likelihood ratio 302, 8 df, p < 1e-50). The fitted q went from 0.07 (Vip→Pvalb) and 0.09 (Sst→Sst, Vip→Vip) to 0.80 (Sst→Vip).

Conclusion: the low slice rates of Pvalb→Sst, Sst→Sst, Vip→Pvalb and Vip→Vip connections are not an artefact of EM class labels, layer composition, a subpopulation of sources or targets, or synapse multiplicity, under the stated assumptions. EM shows anatomical synapses for these class pairs at 10 to 18 percent of nearby pairs. Slices find a response in only 1.4 to 4.3 percent of pairs. The remaining candidate causes are on the functional side (synapses that give no detectable somatic response in these specific class pairs, for example silent or very weak synapses, or electrical-only coupling), EM false-positive synapses that are specific to these pairs, and differences between animals and ages. Models that take interneuron-to-interneuron wiring from EM should not assume that each EM connection is functional with the same probability across class pairs.

## Relation to earlier work

- [sci:sha256:999aa3ea…](sci:sha256:999aa3ea9cc47df6164773d528fc777358c9bb155162acf842a0c16c716b365e): source of the question, the physiology extraction and the ratio method. We replicate its inhibitory results on v1507 with its own rules (Figure 1, orange squares; all 15 R values within 0.14 of the earlier values and all intervals overlap; Sst→Sst 0.13 against 0.09).
- [sci:sha256:62a5b936…](sci:sha256:62a5b93648b2487d8e85dd1679a03f5ebe229ccdd6000f154e4e69049bd899d2): excluded missed small responses. Its first open item was "re-run the EM side with EM cells typed by transcriptomic-like labels (MICrONS metamodel cell types) to test the class-mismatch cause". This work does that.
- [sci:sha256:7c2a1974…](sci:sha256:7c2a19742967a85569db376f7e1868b54c6bb72a0c9e3ec5e9e4ee913d03bb38): used the same v1507 tables and metamodel classes for synapses per connection and PSP strength, but not for connection rates.
- Literature: Pfeffer et al. 2013 (doi:10.1038/nn.3446) found in slices that Sst cells inhibit other Sst cells rarely and that Vip cells inhibit mostly Sst cells. Campagnola et al. 2022 (doi:10.1126/science.abj5861) is the physiology source. Schneider-Mizell et al. 2025 (doi:10.1038/s41586-025-08840-3) describes the target-based inhibitory groups. Our result says that the EM wiring of the MICrONS mouse has the same rank order as this slice "rule set", but with much less contrast.

New here: (1) the first EM–slice rate comparison for interneuron pairs with transcriptomic-like types for all interneuron targets and with 3.3 times more proofread inhibitory axons; (2) a relabelling bound that is independent of any one class mapping; (3) source- and target-subpopulation tests; (4) a synapse-multiplicity detection model.

## Data

- **EM.** MICrONS minnie65 materialization v1507 (one mouse; CC BY 4.0): `synapses_with_axon_proofreading` (2,089,627 synapses from 2,141 proofread axons), `aibs_metamodel_celltypes_v661` (94,014 nuclei; 64,195 excitatory and 7,963 inhibitory neurons), `proofreading_status_and_strategy`. Shared store paths, URLs and SHA-256 hashes are in `files/provenance/data_sources.json`.
- **Physiology.** Allen Synaptic Physiology release 2.1, `synphys_r2.1_small.sqlite` (Allen Institute terms of use). Mouse V1 pairs with more than 10 presynaptic test spikes, a connection call and a soma distance below 250 µm. Same selection as the EM–slice comparison (Sst→Sst 90/3,180 pairs, identical to that work).

No record-level data from either source is in this publication.

## Methods

**EM cells.** Neurons with exactly one nucleus per segment and a metamodel type. Mapping: BC→Pvalb, MC→Sst, BPC→Vip; NGC has no Cre class in the physiology data and is excluded from the main comparison. Layer of each neuron: the majority layer of the excitatory types of its 25 nearest excitatory neighbours (as in sci:7c2a1974); inhibitory cells above the most superficial excitatory cells are L1.

**EM pairs.** Sources: all proofread axons (status `t`) of typed single-soma neurons that have synapses in the table (322 inhibitory: 207 BC, 61 MC, 37 BPC, 15 NGC; 1,740 excitatory). Candidate targets: every typed single-soma neuron with its nucleus within 250 µm (3D). Excitatory sources: inhibitory targets only. A pair is connected if the table has 1 or more synapses from the axon onto the target. 5,796,044 candidate pairs, 456,699 connected.

**Ratio.** For each physiology pair, the EM-expected connection probability is the EM rate of the same class pair in the same stratum. Strata: 25 µm bins of 3D soma distance (T1), or presynaptic layer × postsynaptic layer × 50 µm bin (T2). R = observed slice connections / sum of EM-expected probabilities. 95 percent intervals: two-level bootstrap over EM presynaptic cells and physiology slices (2,000 draws). For E→interneuron controls, sources are in L2/3 to L5 on both sides.

**Pre-registered tests** (written before the comparison):
- T1 class mismatch: metamodel types for sources and all targets. Mismatch explains the deficit if R ≥ 0.5 for each of the four lowest pairs; it is rejected as the main cause if the upper CI limit is below 0.5 for 3 or more of 4.
- T2 layer composition: T1 with layer strata.
- T3 replication: the rules of the EM–slice comparison on v1507 axons (interneuron-targeting if ≥ 35 percent of synapses go to inhibitory cells; else perisomatic if ≥ 25 percent of synapses on excitatory targets are within 15 µm of the nucleus; else sparse if < 800 output synapses; else distal), with targets restricted to typed proofread inhibitory cells.
- T4 relabelling bound. As written, T4 used all type × layer group pairs. Cross-layer group pairs have low rates for geometric reasons, so the T4 minimum (0.031 for all Cre pairs) is not informative (`T4_bound_summary.csv`). We therefore added T4b before we looked at its output: a layer-preserving version. For each slice layer pair, it uses the lowest distance-matched EM rate over all inhibitory source and target types in those layers (≥ 5 source axons, ≥ 100 candidate pairs).
- T5: per-axon distance-matched rate onto each target class, compared with the slice rate.
- Sensitivity: targets with proofread dendrites only (S1), ≥ 2 synapses (S2), fully extended axons only (S3), distance < 150 µm (S4), sources in L2/3 to L5 (S5), targets in L2/3 to L5 with layer strata (S6).

**Added after the pre-registration** (exploratory): decomposition with the same proofread target set (D1), double ratios, the target-side zero-inflated model (T6), the rate-compression slope, and the synapse-multiplicity model.

- T6: for each target cell, the number of candidate proofread sources of one class and its number of connections. Model: a fraction π of targets has no input from the class; the others connect with probability c·p(d), where p(d) is the class-pair rate per distance bin. Maximum likelihood with a profile-likelihood 95 percent interval for π (grid step 0.025). If the slice targets were a random sample of the class, the slice data would need π ≥ 1 − R.
- Multiplicity model: a connection with n EM synapses is detected in slices with probability 1 − (1 − q)^n. EM gives the distribution of n per distance bin (n = 0 included). q is fitted per class pair by maximum likelihood on the slice counts per bin. The interval comes from 500 bootstrap draws of EM presynaptic cells. A likelihood-ratio test compares one common q with separate values.

## Results

### Rates and ratios (Figure 1, `files/results/ratios_all_variants.csv`, `decomposition.csv`)

| Class pair | Slice connected/probed | EM rate at slice distances (T1) | EM sources / targets | R, earlier work | R, earlier rules on v1507 (T3) | R, metamodel, same targets (D1) | R, metamodel, all targets (T1) | R, + layers (T2) |
|---|---|---|---|---|---|---|---|---|
| Pvalb→Pvalb | 467/1841 | 0.319 | 207 / 3,280 | 0.57 (0.49–0.68) | 0.58 (0.51–0.65) | 0.71 (0.63–0.80) | 0.80 (0.71–0.89) | 0.75 (0.66–0.85) |
| Pvalb→Sst | 26/605 | 0.181 | 207 / 2,417 | 0.14 (0.08–0.21) | 0.18 (0.11–0.26) | 0.22 (0.13–0.33) | **0.24 (0.14–0.35)** | 0.25 (0.15–0.37) |
| Pvalb→Vip | 19/488 | 0.105 | 207 / 1,444 | 0.25 (0.14–0.40) | 0.27 (0.15–0.40) | 0.33 (0.18–0.50) | 0.37 (0.21–0.56) | 0.39 (0.23–0.59) |
| Sst→Pvalb | 77/583 | 0.232 | 61 / 3,032 | 0.38 (0.26–0.54) | 0.45 (0.32–0.60) | 0.51 (0.34–0.71) | 0.57 (0.39–0.79) | 0.61 (0.42–0.86) |
| Sst→Sst | 90/3180 | 0.159 | 61 / 2,231 | 0.09 (0.07–0.13) | 0.13 (0.10–0.17) | 0.22 (0.15–0.30) | **0.18 (0.13–0.23)** | 0.18 (0.14–0.24) |
| Sst→Vip | 78/517 | 0.164 | 61 / 1,228 | 0.74 (0.52–1.04) | 0.80 (0.59–1.05) | 0.65 (0.47–0.88) | 0.92 (0.68–1.21) | 0.90 (0.64–1.22) |
| Vip→Pvalb | 12/471 | 0.160 | 37 / 1,735 | 0.12 (0.05–0.25) | 0.13 (0.05–0.24) | 0.13 (0.05–0.25) | **0.16 (0.06–0.31)** | 0.18 (0.07–0.36) |
| Vip→Sst | 43/524 | 0.183 | 37 / 1,246 | 0.33 (0.21–0.49) | 0.36 (0.24–0.51) | 0.32 (0.20–0.48) | 0.45 (0.28–0.66) | 0.49 (0.32–0.73) |
| Vip→Vip | 15/1070 | 0.099 | 37 / 652 | 0.09 (0.05–0.15) | 0.11 (0.06–0.19) | 0.09 (0.05–0.15) | **0.14 (0.07–0.22)** | 0.17 (0.08–0.27) |
| Pvalb→E | 276/964 | 0.314 | 207 / 62,574 | 0.80 (0.69–0.95) | 0.84 (0.73–0.96) | – | 0.91 (0.80–1.05) | 0.89 (0.79–1.01) |
| Sst→E | 135/872 | 0.275 | 61 / 56,833 | 0.46 (0.34–0.63) | 0.52 (0.41–0.64) | – | 0.56 (0.43–0.74) | 0.59 (0.45–0.74) |
| Vip→E | 5/614 | 0.018 | 37 / 33,170 | 0.76 (0.12–1.79) | 0.62 (0.11–1.45) | – | 0.45 (0.08–1.10) | 0.36 (0.06–0.94) |
| E→Pvalb | 263/900 | 0.202 | 1,345 / 3,238 | 1.06 (0.83–1.38) | 1.19 (1.05–1.35) | 1.29 (1.13–1.46) | 1.45 (1.27–1.64) | 1.55 (1.37–1.74) |
| E→Sst | 165/824 | 0.181 | 1,345 / 2,383 | 0.80 (0.63–1.16) | 0.92 (0.77–1.09) | 0.84 (0.71–1.00) | 1.11 (0.93–1.31) | 1.32 (1.13–1.56) |
| E→Vip | 33/589 | 0.040 | 1,345 / 1,378 | 1.05 (0.63–1.84) | 1.16 (0.74–1.64) | 1.04 (0.67–1.42) | 1.40 (0.92–1.95) | 1.37 (0.89–1.93) |

In the physiology rows, Pvalb, Sst and Vip are Cre classes. In the EM columns, they are target-based groups (first two R columns) or metamodel types (last three).

- The step from the earlier rules to metamodel labels with the same proofread targets (T3 → D1) raised Sst→Sst from 0.13 to 0.22 and Pvalb→Pvalb from 0.58 to 0.71. It did not change the Vip-source pairs. Thus mismatch explains part of the Sst→Sst deficit (a factor of about 1.7), not the rest.
- The step to all typed targets (D1 → T1) raised most ratios by 10 to 40 percent, and also the excitatory controls (E→Pvalb 1.29 → 1.45). Most of this is probably target-side EM incompleteness (non-proofread dendrites lose synapses), which affects all sources.
- Double ratios R(I→T)/R(E→T) in T1 (`double_ratios.csv`; intervals combine the two bootstraps independently): Pvalb→Sst 0.22 (0.12–0.33), Sst→Sst 0.16 (0.12–0.22), Vip→Pvalb 0.11 (0.04–0.22), Vip→Vip 0.10 (0.05–0.19), Pvalb→Pvalb 0.55 (0.46–0.65), Sst→Vip 0.66 (0.41–1.09).
- Sensitivity (`ratios_all_variants.csv`): for the four key pairs, R stayed between 0.09 and 0.28 in S1, S3, S4, S5 and S6. S3 has no Vip sources (no BPC axon is fully extended) and only 16 MC sources.

### Relabelling bound (Figure 1, black bars; `T4b_layer_preserving_bound.csv`)

| Class pair | R with the most favourable EM types per layer pair, NGC allowed | NGC not allowed |
|---|---|---|
| Pvalb→Sst | 0.76 | 0.61 |
| Sst→Sst | 0.48 | 0.44 |
| Vip→Pvalb | 0.49 | 0.35 |
| Vip→Vip | 0.25 | 0.17 |

The lowest EM rates came from pairs such as Pvalb→NGC, NGC→Vip and Pvalb→Vip, which are not plausible matches for these Cre pairs. Even with this choice, Vip→Vip stays at a quarter of the EM expectation, and Sst→Sst and Vip→Pvalb at half.

### Subpopulations (Figure 2; `T5_subpop_summary.csv`, `T5_per_axon_rates.csv`, `T6_target_subpop.csv`)

- Sources: the fraction of axons whose own distance-matched rate was at or below the slice rate was 6 percent (Pvalb→Sst, 11 of 172), 2 percent (Sst→Sst, 1 of 56), 8 percent (Vip→Pvalb, 3 of 36) and 0 percent (Vip→Vip, 0 of 25). The median axon rates were 3 to 7 times the slice rates.
- Targets: the fitted fraction of targets with no input (π, 95 percent interval) against the fraction that the slice data need: Pvalb→Sst 0.11 (0.10–0.125) against 0.76; Sst→Sst 0.10 (0.075–0.125) against 0.82; Vip→Pvalb 0.09 (0.05–0.125) against 0.84; Vip→Vip 0.32 (0.225–0.40) against 0.86. The need is outside the interval for 8 of 9 inhibitory-to-interneuron pairs (Sst→Vip needs only 0.08).

### Rate compression and synapse multiplicity (Figure 3; `summary_rate_compression.json`, `multiplicity_*.csv`)

- Across the nine pairs, log slice rate = a + 2.1 × log EM rate (OLS on 9 points; descriptive). Spearman ρ = 0.83 (p = 0.005).
- Per-synapse detection q (95 percent bootstrap interval over EM sources): Pvalb→Pvalb 0.60 (0.52–0.67), Sst→Vip 0.80 (0.58–1.0), Sst→Pvalb 0.35 (0.24–0.53), Pvalb→Vip 0.25 (0.22–0.29), Vip→Sst 0.24 (0.18–0.35), Pvalb→Sst 0.12 (0.11–0.14), Vip→Vip 0.09 (0.08–0.12), Sst→Sst 0.09 (0.07–0.12), Vip→Pvalb 0.07 (0.05–0.15). One common q (0.28) was rejected (LR 302, 8 df). For inhibitory→excitatory pairs a common q was also rejected (LR 28.6, 2 df). For excitatory→interneuron pairs q was at its upper limit 1 (EM finds fewer connections than slices).
- In EM, 52 to 68 percent of connections in the four low pairs have one synapse, against 40 to 54 percent for Pvalb→Pvalb and Sst→Vip. This difference is too small to give the 7-fold difference in q.

## Figures

- `files/figures/fig1_ratios_by_class_definition.png`: (A) R by class pair for five EM class definitions and the relabelling bound; (B) cross-tabulation of metamodel types and target-based groups of the 322 proofread inhibitory axons.
- `files/figures/fig2_subpopulation_tests.png`: (A) per-axon EM rates and slice rates; (B) zero-inflated target model.
- `files/figures/fig3_rate_compression_and_multiplicity.png`: (A) slice against EM rate; (B) per-synapse detection probability.

## Limitations

- One EM mouse; physiology from many mice of a different age (median 46 days in the EM–slice comparison) and preparation. Animal and age differences are not tested here.
- Metamodel types are predictions from soma and nucleus features. They are not Cre lines. We cannot test how each Cre line maps to EM cells. The relabelling bound (T4b) covers mappings at the level of metamodel type × layer. It does not cover a Cre class that selects cells across types by some other feature.
- EM inhibitory axons are proofread, but most target dendrites are not. Missing target synapses lower EM rates. This makes the EM excess a lower limit. False merges of targets could add false connections. S1 (proofread dendrites only, 61 to 208 targets per class) gave the same result.
- Synapse detection errors in EM are not modelled. False-positive synapses that are specific to some interneuron class pairs remain a possible cause. A uniform false-positive rate would also affect excitatory and Pvalb→E pairs, where R is near 1.
- The layer of EM cells comes from neighbouring excitatory types. It is approximate at layer borders. The physiology layer comes from the Allen cortical location or the target layer.
- T6 assumes one rate scale c for all non-immune targets and uses a coarse grid for the profile interval. The double-ratio intervals combine two bootstraps as independent.
- The rate-compression slope and the multiplicity model are post hoc and descriptive (9 class pairs).
- Vip sources are few (37 axons; 25 to 36 with enough targets for per-axon tests).

## What remains open

- Same-cell tests: paired recordings followed by EM (as in Holler et al. 2021) for Sst→Sst, Vip→Vip, Vip→Pvalb and Pvalb→Sst connections. This is the direct test of silent or very weak anatomical synapses.
- A second EM volume (for example the MICrONS V1DD volume or a human volume) with typed interneurons, to test whether the EM rates for these pairs repeat across animals.
- EM synapse-detection error rates per class pair (for example manual review of a random sample of Sst→Sst and Vip→Vip synapses).
- Gap junctions: Sst–Sst and Pvalb–Pvalb pairs are often electrically coupled. EM synapse tables do not include gap junctions; the slice electrical-coupling calls could be compared with chemical EM rates.
- Patch-seq or Cre-line-labelled EM cells to map Cre classes onto EM cells directly.

## Reproduce

1. Get the four input files. Use the shared campaign store (`datasets/`), or run `bash files/provenance/retrieve_data.sh /path/to/scratch_datasets` (about 260 MB; writes outside the publication and checks SHA-256).
2. Run `bash files/provenance/run_all.sh /path/to/datasets /path/to/this/publication /path/to/empty_workdir`. It copies `files/code` into the work folder and writes `scratch/`, `results/` and `figures/` there (about 20 minutes on one CPU; the bootstrap seeds are fixed).
3. Compare `results/` with `files/results/`.

Software: Python 3.12.15, pandas 3.1.1, numpy 2.5.4, scipy 1.18.1, matplotlib 3.11.2, pyarrow 26.0.1. We re-ran `run_all.sh` from the package in a clean work folder before signing (see Provenance).

## Files

- `files/code/`: `01_em_pairs.py` (EM cells, layers, axon groups, candidate pairs), `02_synphys_pairs.py` (physiology pairs; adapted from sci:999aa3ea), `ratio_lib.py` (stratified ratio and bootstrap; generalised from sci:999aa3ea), `03_ratios.py` (T1–T3, S1–S6), `04_bound_subpop.py` (T4, T4b, T5), `05_decomp.py` (D0–D2, double ratios), `06_target_subpop.py` (T6), `07_multiplicity.py`, `08_figures.py`, `09_export.py` (per-axon tables with MICrONS IDs).
- `files/results/`: aggregate tables listed above. `em_inhibitory_axons_types.csv` gives, for each of the 322 proofread inhibitory axons, the MICrONS nucleus ID, v1507 root ID, metamodel type, layer, target-based features and group. `T5_per_axon_rates.csv` gives per-axon EM rates. `T4_group_rates.csv` gives EM rates per type × layer group pair.
- `files/provenance/`: `data_sources.json` (URLs, hashes, shared paths), `retrieve_data.sh`, `run_all.sh`, `PROGRESS_log_and_preregistration.md`, `ref_999aa3ea_inhib_ratios.csv` (the aggregate ratio table of sci:999aa3ea, used in Figure 1), `NOTICE-external-data.md`.

## Provenance

SCI campaign 11_07_2026. Job sci-1107-hp-neural-structure-and-computation-987ea48eb659. Topic neural-structure-and-computation. Machine hp. Account claude-olen. Model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. Analysis date 2026-11-12. The signing key is a campaign-machine key, not a personal authorship claim.

Reproduction check: before signing, `run_all.sh` was run from the packaged code in a clean work folder with the shared input files. It gave all files in `files/results/` and `files/figures/` again byte for byte.

## External data and attribution

See `files/provenance/NOTICE-external-data.md`. MICrONS data: MICrONS Consortium, CC BY 4.0. Allen Synaptic Physiology data: Allen Institute for Brain Science, used under the Allen Institute terms of use. This publication contains no copy of either source data set.
