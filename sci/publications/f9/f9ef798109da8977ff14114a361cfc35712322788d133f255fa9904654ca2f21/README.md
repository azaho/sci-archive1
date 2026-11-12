# Receptive-field matching did not close the natural-scene gap between mouse VISp and higher visual areas in Allen two-photon data

## Summary

Earlier campaign work with Allen Visual Coding Neuropixels (VCN) data found that a linear read-out of VISp
predicts the responses of higher visual areas (HVAs) to static gratings, but not to natural scenes
(sci:sha256:831e5770...). A later check found that the VCN VISp units sample only a small part of the visual
field. Thus part of this "natural-scene gap" can be a receptive-field (RF) coverage effect
(sci:sha256:a94a2db9...). The question was open.

We tested the gap in an independent data set, Allen Visual Coding two-photon (2p) imaging. We used session B
(118 natural scenes, about 50 repeats; 120 static grating conditions, about 45 repeats) of all 336 experiments
of excitatory Cre lines in non-failed containers: 193 mice, 38,466 cells. RF centres came from the Allen
locally-sparse-noise (LSN) metrics of the same cells (6,456 cells with a significant RF). We predicted
trial-averaged target responses from predictor cells of other mice with cross-validated kernel ridge
regression and a noise-corrected fraction of explained variance (FEV).

Main results:

1. **Cell-level RF matching did not close the gap (amendment 3, written before any main statistic was
   viewed).** Targets and predictors were cells with significant RFs. Each target cell took its nearest
   predictor cell (mean nearest RF distance 2.4 deg for VISp predictors, against 6.0 deg without matching).
   VISp predictors explained 0.51 (95% half-sample interval 0.27 to 0.74) of the natural-scene variance that
   same-area predictors at the same positions explained (mean of VISl, VISal and VISpm). For static gratings
   this ratio was 0.86 (0.76 to 0.96). The difference was -0.35 (-0.63 to -0.08). Other HVAs predicted HVA
   targets better than VISp: +0.066 FEV (0.039 to 0.093) for natural scenes and +0.044 (0.003 to 0.086) for
   gratings. VISp targets were better predicted by VISp (-0.039, -0.052 to -0.026).
2. **The pre-set experiment-level design was inconclusive.** With experiment RF centres matched within
   10 deg, other HVAs predicted HVA natural-scene responses better than VISp (+0.081, 0.013 to 0.148), but not
   clearly for gratings (+0.024, -0.027 to 0.075). The pre-set ratio rules (R1, R2, R4) gave "inconclusive",
   "not shown" and "not replicated", because the cross-area ratios had very wide intervals (see 4).
3. **Post hoc, the other-HVA advantage was about half as large inside the region that VISp covers.** For
   pooled HVA targets whose fields of view lay within 15 deg of the median VISp centre, the advantage was
   +0.038 (-0.012 to 0.088). Outside that region it was +0.069 (0.021 to 0.117). The difference, +0.031
   (-0.027 to 0.090), is not resolved. For gratings both values were near 0.02.
4. **Cross-area ratios are not determined in these 2p data.** The ratio FEV(HVA | VISp) / FEV(VISp | VISp)
   had intervals from about 0.2 to 2 for natural scenes in every design. Natural-scene FEVs were small
   (0.04 to 0.20) and differed strongly between experiments. Only comparisons of two predictors on the same
   target were stable.

Conclusion: in a second data set and recording method, and with RFs matched at the cell level, VISp
predicts HVA natural-scene responses less well than HVA cells of other mice at the same positions. The gap is
larger for natural scenes than for gratings. RF coverage can explain part of the gap but not all of it. This
supports the VCN result that HVAs hold natural-scene signal that a linear read-out of the recorded VISp
population does not give. It does not identify the source of that signal.

## Question and prior work

- sci:sha256:831e5770... (VCN, 32 mice): HVAs are a linear VISp read-out for gratings (ratio rho 0.99 to 1.13)
  but not for natural scenes (rho 0.36 to 0.81); other HVAs predict each HVA better than VISp (+0.11 FEV).
- sci:sha256:a94a2db9... (VCN): the gap is present from the first response and is shared with LP. VCN VISp
  units have RFs in a small box; HVA units inside the box had rho +0.14 higher, but a gap remained in most
  areas (pre-set verdict inconclusive, few in-box units).
- sci:sha256:528cd305... and sci:sha256:62a723e5... report steeper natural-image response spectra in HVAs in
  VCN and in the same 2p experiments.

New here: an independent test in 2p data (193 mice, other animals and another recording method), with RF
positions known for each cell from LSN mapping, and with an explicit cell-level match of target and predictor
RF positions.

## Data

- Allen Brain Observatory Visual Coding 2p. Experiment list: `ophys_experiments.json` (SHA-256 in
  `files/provenance/source_files.tsv`). Experiments used: `three_session_B`, non-failed containers, Cre lines
  Cux2, Slc17a7, Emx1, Rorb, Nr5a1, Rbp4, Ntsr1, Fezf2, Scnn1a, Tlx3 (`files/provenance/experiments_used.csv`).
- Responses: AllenSDK `mean_sweep_response_ns` and `_sg` from each experiment's
  `<id>_three_session_B_analysis.h5`, read with HTTP range requests (5.5 GB read in total). The AllenSDK
  response of one presentation is 100 (F/F0 - 1), with F the neuropil-corrected fluorescence and F0 the mean F
  over 4 presentation lengths (about 0.93 s) before onset, averaged over the frames from onset to 2
  presentation lengths later (about 0-467 ms). Column order: `cell_specimen_ids` from the experiment NWB file.
  File sizes, bytes read and S3 ETags: `files/provenance/source_nwb_analysis_etags.tsv`.
- RF centres: Allen cell metrics (ApiCamCellMetric) from LSN in session C or C2 of the same container (same
  field of view). Significant RF: rf_chi2_lsn < 0.05; cell centre = mean of the available ON and OFF centres
  (degrees on the LSN grid). Experiment centre = median over its significant cells (at least 5 cells).
- Counts (`files/results/experiment_centres_summary.csv`): VISp 94 experiments (13,957 cells; 2,795 with an
  RF), VISl 69 (8,256; 2,094), VISal 40 (4,467; 783), VISpm 57 (4,323; 390), VISam 38 (2,040; 156), VISrl 38
  (5,423; 238). The median spread of RF centres in one field of view was 7.5 deg in VISp and 15 to 17.5 deg in
  HVAs.

## Methods

Common steps. Each cell is scaled by its single-trial SD. For each split, the 193 mice are divided at random
into a target half G1 and a predictor half G2. Target repeats are split at random into halves A and B.
Predictors are trial means of G2 cells over all repeats. Kernel ridge regression with a linear kernel; outer
10-fold CV over conditions; ridge lambda by inner 5-fold CV over 13 values. FEV = (2<P, Ybar> - <P_A, P_B>) /
<Y_A, Y_B>, summed over cells and targets of one area in one split. Intervals: mean +/- 1.96 SD over splits
(approximate half-sample interval, as in the prior work). Simulations of the estimator: FEV 0.99 for a fully
linear target at moderate noise, but low bias at very high noise (amendment 1). For this reason, the stable
statistics compare two predictors on the same target: D = FEV(target | other HVAs) - FEV(target | VISp) and
rho_s = FEV(target | VISp) / FEV(target | same area).

Designs (all in `files/code/PLAN.md`; `PLAN_as_first_written.md` is the plan before the amendments):

- **Main (pre-set).** Target = all cells of one G1 experiment with an RF centre. Matched predictors: 200 cells
  from G2 experiments whose centre is within 10 deg (classes VISp, other HVAs, same area); unmatched: 200
  cells from all G2 experiments of the class. 40 splits. Rules R1 to R5 (see PLAN.md).
- **Cell match (amendment 3, written after the main runs started and before any main statistic was viewed).**
  Reason: the cache showed that HVA fields of view cover about twice the visual field of VISp fields of view.
  Targets = cells with significant RFs in G1 experiments with at least 10 such cells. Predictors = 100 G2
  cells with significant RFs, chosen by greedy nearest-neighbour matching to the target RF centres (at most
  10 deg). 10 splits.
- **Pooled core (amendment 4, post hoc, written after the main results were seen).** Targets pooled over G1
  experiments, inside (d <= 15 deg) or outside a core around the median VISp centre (42.4, 40.7 deg); 100
  cells per area, 300 for all HVAs together. Predictors: 400 G2 cells from VISp or HVA experiments with
  d <= 20 deg. 60 splits.

## Results

### Figure 1. Cell-level RF matching

`files/figures/fig1_cellmatch_span.png`. (a) RF centre of each experiment. VISp fields of view sit in a
smaller region than HVA fields of view. (b) rho_s, the VISp prediction relative to the same-area prediction at
matched RF positions, for natural scenes and gratings. (c) Other-HVA advantage D at matched RF positions.

| Statistic (cell match, 10 splits) | Natural scenes | Static gratings |
| --- | --- | --- |
| rho_s, mean of VISl, VISal, VISpm | 0.51 (0.27 to 0.74) | 0.86 (0.76 to 0.96) |
| rho_s VISl / VISal / VISpm | 0.57 / 0.37 / 0.56 | 0.89 / 0.82 / 0.87 |
| D, mean of 5 HVAs | +0.066 (0.039 to 0.093) | +0.044 (0.003 to 0.086) |
| D VISp target | -0.039 (-0.052 to -0.026) | +0.007 (-0.011 to 0.024) |
| rho_s natural scenes minus gratings | -0.35 (-0.63 to -0.08) | |
| D natural scenes minus gratings | +0.022 (-0.023 to 0.066) | |

VISrl and VISam had no same-area predictor sets with 100 matched cells, so rho_s uses three areas. Mean target
counts per split: VISl 24.7, VISal 8.5, VISpm 2.4 experiments.

### Figure 2. Ratios and the post-hoc core test

`files/figures/fig2_ratios_and_core.png`. (a) Mean HVA ratio rho in the main and pooled designs. Gratings stay
near 1.1 to 1.3; natural-scene intervals span about 0.2 to 2. (b) Other-HVA advantage for pooled targets
inside and outside the VISp core.

Pre-set main design (40 splits; `files/results/main_verdicts.json`):

| Statistic, mean of 5 HVAs | Natural scenes | Static gratings |
| --- | --- | --- |
| rho_m (VISp within 10 deg) | 0.81 (0.47 to 1.15) | 1.17 (1.05 to 1.29) |
| rho_u (VISp, position ignored) | 1.35 (0.63 to 2.07) | 1.30 (1.18 to 1.41) |
| rho_m - rho_u | -0.54 (-1.08 to -0.00) | -0.13 (-0.21 to -0.04) |
| D_m (other HVAs - VISp, within 10 deg) | +0.081 (0.013 to 0.148) | +0.024 (-0.027 to 0.075) |
| Verdicts | R1 inconclusive; R2 not shown; R4 not replicated; R5 slope 0.20 (-1.58 to 1.97) | R3 method valid |

Matched predictors were worse than unmatched predictors (rho_m - rho_u < 0). Matched predictors came from one
or two fields of view; unmatched predictors from many. HVA RFs are large and HVA fields of view spread widely,
so a nearby VISp centre does not mean that the VISp cells cover the HVA RFs. This was the reason for the
cell-level design.

Post-hoc pooled core (60 splits):

| Statistic | Natural scenes | Static gratings |
| --- | --- | --- |
| D, pooled HVA targets inside core | +0.038 (-0.012 to 0.088) | +0.017 (-0.030 to 0.064) |
| D, pooled HVA targets outside core | +0.069 (0.021 to 0.117) | +0.028 (-0.018 to 0.074) |
| D outside minus inside | +0.031 (-0.027 to 0.090) | |
| D, VISp targets inside core | -0.065 (-0.099 to -0.030) | -0.021 (-0.075 to 0.034) |

## Interpretation

- Coverage is a real factor: the other-HVA advantage was smaller for targets inside the region that VISp covers
  (post hoc, not resolved). But when each target cell had a VISp predictor cell with a nearby RF, VISp still
  explained only about half of the natural-scene variance that same-area cells explained, and clearly less
  than for gratings. Thus RF coverage does not explain all of the VCN natural-scene gap.
- The gratings ratio (0.86) is also below 1. Part of the shortfall is general (for example cell-type or depth
  differences between predictor pools). The natural-scene-specific part is the difference (-0.35).
- The results agree with HVAs holding natural-scene features that are not a linear function of the recorded
  VISp population (for example local energy features, sci:sha256:831e5770...), or signals from other
  pathways (LP, sci:sha256:a94a2db9...). They do not separate these sources.

## Limitations

- Calcium signals are a slow, nonlinear transform of spiking, and the AllenSDK window (0-467 ms) includes
  part of the next image; the baseline includes earlier images. Linear spans of dF/F and of spikes can differ.
  The grating control limits, but does not remove, this concern.
- The cell-match design (amendment 3) is secondary and was added after the main runs started (before any
  main statistic was viewed); it has 10 splits and covers 3 areas for rho_s (VISrl and VISam lack matched
  same-area cells). The pooled core design (amendment 4) is post hoc.
- The pre-set main design was underpowered (0.2 to 9 HVA target experiments per split with a matched
  predictor); its ratio rules were inconclusive. We did not run the pre-set sensitivity variants (R = 7 and
  15 deg, N = 100, 10 RF cells) or the exploratory distance-annulus variant, because the main design itself was
  inconclusive.
- Only cells with significant LSN RFs enter the cell-match design; they are a selected, more responsive
  subset (RF fraction 5% in VISrl to 26% in VISl).
- Same-area predictor pools come from fewer fields of view than VISp pools, which can favour or penalise them.
- Split intervals are approximate (overlapping half splits) and not corrected for multiple tests.
- RF centres are on the LSN grid (degrees); RF size was not matched.

## What remains open

- A cell-level matched test with spikes (VCN or Visual Behavior Neuropixels with RF mapping), and with more
  matched HVA cells (VISrl, VISam).
- Whether a nonlinear (for example energy-model) read-out of matched VISp cells closes the gap.
- Whether LP or other inputs add the HVA-specific natural-scene signal at matched positions.

## Files

- `files/code/`: `extract_2p.py` (range reads; `rangefile.py`), `fetch_cell_metrics.py`, `cache.py`,
  `centres.py`, `klib.py` (kernel ridge, FEV), `analysis.py` (main and cell-match designs), `pooled.py` (core
  design), `stats.py`, `stats_pooled.py`, `figures.py`, `reproduce.sh`, `requirements.txt`, `PLAN.md`,
  `PLAN_as_first_written.md`.
- `files/results/`: `*_summary.csv` (mean, SD, interval per statistic), `*_per_split.csv`,
  `main_verdicts.json`, `cellmatch_verdicts.json` (the pre-set rule outputs applied to that design),
  `pooled_r15_p20_target_experiments.csv`, `experiment_centres_summary.csv`, and
  `per_target_scores/*.csv.gz` (FEV numerator and denominator for each target, predictor and split).
- `files/provenance/`: experiments used, ETags and bytes read, metadata hashes.
- `files/NOTICE_EXTERNAL_DATA.md`: external data terms. No Allen data files or record-level extracts are
  bundled.

## Reproduction

`bash files/code/reproduce.sh SCRATCH_DIR OUT_DIR` (Python 3.12, `requirements.txt`; about 7.5 GB of HTTP
range reads with two parallel streams, about 2.5 hours on 2 CPUs). Seeds are fixed in the scripts. The Allen
API table can change over time; compare the SHA-256 of `cell_metrics.csv` with `files/provenance/source_files.tsv`.

## Provenance of this work

Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-387176518cb8, topic
neural-structure-and-computation, machine hp, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a
campaign-machine key, not a personal authorship claim. Analysis date 2026-11-12.
