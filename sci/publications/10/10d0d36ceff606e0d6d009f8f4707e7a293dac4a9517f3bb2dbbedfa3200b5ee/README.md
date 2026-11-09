# The Bugeon 2022 transcriptomic axis predicted running modulation of mouse V1 interneuron types during grey screen in an independent dataset, but not during visual stimuli in that dataset

## Summary

Bugeon et al. (2022) found that one transcriptomic axis (tPC1, the first principal component of
in situ gene expression of inhibitory neurons) predicts how mouse V1 interneurons change their
activity with brain state. Interneuron types with high tPC1 (Vip, Sncg) fire more when the mouse
runs. Types with low tPC1 (Pvalb) fire less. The relation was also found between types inside
one subclass. Bugeon et al. measured it during a grey screen in 4 mice.

We tested this claim in an independent dataset: Allen Institute DANDI:002015 (9 mice, jGCaMP8s,
mesoscope two-photon imaging, Xenium gene counts of the same neurons, Allen Brain Cell Atlas
taxonomy). We transferred the Bugeon tPC1 gene loadings to the 32 genes that the two gene panels
share. We first ran the same pipeline on the Bugeon processed data as a positive control.

Main results:

1. **Positive control passed.** In the Bugeon data, our pipeline found the published relation. The
   slope of the running correlation on type-mean tPC1 inside subclasses was +0.26 per SD (mouse
   bootstrap 95% interval 0.14 to 0.46, 4 mice, 789 cells). With only the 32 shared genes, the
   transferred axis correlated r = 0.94 with the full 72-gene tPC1.
2. **The planned primary test failed.** In DANDI:002015, with whole sessions (mostly drifting
   gratings and natural movies), the type-mean slope was -0.016 (-0.085 to 0.059; 7 mice, 1,005
   cells). The cell-level slope inside subclasses was +0.005 (-0.004 to 0.014).
3. **During grey screen, the relation replicated at the type level (exploratory).** Within the same
   DANDI cells and sessions, the grey-screen type-mean slope was +0.18 (0.05 to 0.28; 5 mice, 692
   cells; leave-one-mouse-out range 0.15 to 0.24). During stimulus periods it was +0.05 (-0.03 to
   0.16). The grey-minus-stimulus difference was +0.13 (0.004 to 0.22). Across subclasses, the
   cell slope was +0.10 (0.07 to 0.13) during grey screen and +0.02 (0.00 to 0.03) during stimuli.
4. **The reason is that Pvalb and Sst cells become more running-correlated when a stimulus is
   shown.** This occurred in both datasets. In the Bugeon gratings recordings the decrease of the
   tPC1 relation was smaller: the type-mean slope stayed +0.21 (0.05 to 0.41).
5. **A tPC1 that we computed again from the DANDI genes did not replicate the type-level relation.**
   This de novo axis (library-size normalised) correlated r = 0.93 with the transferred axis. Its
   grey-screen type-mean slope was +0.05 (-0.19 to 0.23).

Thus, the transferred Bugeon axis generalised to a second set of mice, to a different calcium
indicator and to a different cell-type taxonomy, but only for spontaneous activity during grey
screen. During visual stimulation, the transcriptomic axis did not predict running modulation
well in the Allen data. The grey-screen finding is exploratory: we added it after the planned
whole-session test failed.

## Question

Does the Bugeon et al. (2022) transcriptomic axis predict running (arousal) modulation of V1
interneurons in an independent dataset: (a) across transcriptomic types inside a subclass, (b)
across single cells inside a subclass, and (c) across all interneurons? Does the result depend on
the behavioural and sensory condition?

## Data

| Dataset | Mice | Interneurons used | Indicator, frame rate | Genes | Taxonomy |
| --- | --- | --- | --- | --- | --- |
| Bugeon et al. 2022 (figshare 19448531 v2) | 4 | 1,031 with gene counts; 812 in both conditions | GCaMP6m, about 4.3 Hz | 72 (coppaFISH) | Tasic 2018 subtypes |
| DANDI:002015 draft (Allen Institute) | 9 | 1,457 co-registered GABAergic neurons | jGCaMP8s, about 10.7 Hz per plane | 299 or 480 (Xenium; 265 common) | ABC atlas supertypes |

DANDI:002015 has two Xenium panels: 299 genes (6 mice) and 480 genes (3 mice). We used the 265
common genes and centred each gene inside each panel. 32 of the 72 Bugeon genes are in the common
set. Each DANDI mouse has 3 drifting-grating sessions (each with about 6 min of grey screen) and 1
natural-movie session.

## Methods

**Activity measure.** For each neuron and recording we smoothed the activity (detected events in
DANDI, deconvolved activity in Bugeon) and the running speed with a 5-s boxcar. The main measure is
r_run, the Pearson correlation of the two. We used a recording only if 5% to 95% of its frames had
running above 2 cm/s. Per cell, we averaged r_run over the recordings with Fisher z, weighted by
frame count. Secondary measures: a modulation index (running versus stationary), the Bugeon
running versus stationary-synchronised index (Bugeon data only), and the correlation with pupil
area in stationary frames.

**Periods.** Grey screen: DANDI grey-screen blocks of 60 s or longer; Bugeon "Blank" recordings.
Stimulus: DANDI frames outside grey-screen blocks (gratings and movies); Bugeon drifting-grating
recordings. Whole session: all DANDI frames (planned primary measure).

**tPC1.** Bugeon tPC1: PCA of log(1 + count) of the 72 genes of the 1,031 Bugeon interneurons with
gene counts (variance explained 26%). Axis A1 (primary transfer): the 72-gene loadings restricted
to the 32 shared genes, applied to log(1 + count) of the DANDI cells. A1b: PCA of the Bugeon cells
with only the 32 shared genes. A2: de novo PCA of DANDI GABAergic cells (184 genes detected in at
least 5% of cells, transgene probes removed). A2n: the same after library-size normalisation. Sign
convention: Vip positive, Pvalb negative. Each axis is z-scored over the cells of its dataset.

**Models.** Least squares with fixed effects:

- T1: r_run ~ type-mean tPC1 + subclass + mouse (types with 5 or more cells; this is the Bugeon Fig. 5c claim);
- T2: r_run ~ cell tPC1 + subclass + mouse;
- T3: r_run ~ cell tPC1 + type + mouse;
- T0: r_run ~ cell tPC1 + mouse.

Intervals are 2.5 and 97.5 percentiles of a bootstrap that resamples mice (1,000 resamples). We
also give HC1 standard errors and leave-one-mouse-out ranges. The condition test uses the same
cells and only sessions where both periods are valid. It models r_grey, r_stim and their difference.

## Results

Slopes are changes of r_run per SD of tPC1, with the 95% mouse-bootstrap interval
(`files/results/fig2_values.csv`, `files/results/condition_regressions.csv`, `files/results/regressions.csv`).

| Data and period | Mice / cells | T1 type mean, inside subclass | T2 cell, inside subclass | T0 cell, all interneurons |
| --- | --- | --- | --- | --- |
| Bugeon, grey screen | 4 / 812 | +0.26 (0.14, 0.46) | +0.17 (0.05, 0.32) | +0.19 (0.15, 0.27) |
| Bugeon, gratings | 4 / 812 | +0.21 (0.05, 0.41) | +0.16 (0.04, 0.31) | +0.13 (0.09, 0.21) |
| DANDI, grey screen | 5 / 723 | +0.18 (0.05, 0.28) | +0.06 (-0.02, 0.11) | +0.10 (0.07, 0.13) |
| DANDI, stimulus periods | 5 / 723 | +0.05 (-0.03, 0.16) | +0.01 (-0.01, 0.02) | +0.02 (0.00, 0.03) |
| DANDI, whole session (planned primary) | 7 / 1,035 | -0.02 (-0.09, 0.06) | +0.01 (-0.00, 0.01) | +0.02 (0.01, 0.03) |

Paired differences (grey minus stimulus), same cells: DANDI T1 +0.13 (0.004, 0.22), T0 +0.08
(0.07, 0.09); Bugeon T1 +0.05 (-0.01, 0.18), T0 +0.06 (0.02, 0.09).

Mean r_run by subclass, same cells (`files/results/subclass_by_condition.csv`):

| Subclass | Bugeon grey | Bugeon gratings | DANDI grey | DANDI stimulus |
| --- | --- | --- | --- | --- |
| Pvalb | -0.16 | +0.01 | -0.03 | +0.11 |
| Sst | +0.13 | +0.25 | +0.04 | +0.19 |
| Lamp5 | +0.18 | +0.18 | +0.01 | +0.14 |
| Vip | +0.32 | +0.35 | +0.18 | +0.17 |
| Sncg | +0.35 | +0.30 | +0.13 | +0.08 |

Other checks:

- The planned primary null did not change with dF/F instead of events (T1 -0.011), with
  high-confidence supertype labels (bootstrap probability 0.8 or more; T1 -0.009), with log
  library size as a covariate (T2 +0.005), with axis A1b (T1 -0.009), or with grating sessions
  only or movie sessions only (T1 -0.011 and +0.044; all intervals include zero).
- With the de novo axes, DANDI whole-session slopes inside subclasses were zero or negative
  (A2n: T2 -0.036, -0.056 to -0.014). Raw A2 is mostly a library-size axis: all of its large
  loadings have the same sign (Gad1, Gad2, Rab3b, Pvalb).
- Grey-screen pupil correlation in DANDI (6 mice): T1 +0.09 (-0.05, 0.20), T0 +0.04 (0.004, 0.06).
  Grey-screen modulation index: T1 +0.22 (-0.10, 0.45), T0 +0.12 (0.08, 0.14).
- Per mouse, the grey-screen type-mean slope was positive in 4 of 4 Bugeon mice and 4 of 5 DANDI
  mice (`files/results/per_mouse_typemean_slopes.csv`).
- Labels explain more than tPC1. In DANDI (whole session) subclass + mouse explained R2 = 0.11 and
  supertype + mouse 0.16; adding tPC1 added less than 0.001. In the Bugeon data the values were 0.24
  and 0.35 (`files/results/variance_explained.csv`).

## Figures

- `files/figures/fig1_type_means_by_condition.png`: type-mean r_run against type-mean tPC1, grey
  screen and stimulus, in both datasets (same cells within a dataset).
- `files/figures/fig2_slopes.png`: slopes and mouse-bootstrap intervals for T1, T2 and T0.
- `files/figures/fig3_subclass_by_condition.png`: subclass means of r_run, grey screen against stimulus.

## Limitations

- The grey-screen and condition results are exploratory (PLAN amendment 3, added after the planned
  whole-session test). Treat them as a hypothesis for a new test.
- DANDI has only about 6 min of grey screen per grating session. Only 5 of 9 mice had sessions with
  both running and stationary frames in grey screen and in stimulus periods. The intervals are wide.
- The transfer uses 32 of 72 genes. In the Bugeon data this keeps r = 0.94 with the full tPC1, but
  Xenium and coppaFISH have different detection efficiency. The de novo DANDI axis did not give the
  type-level result, so the replication depends on the axis definition.
- Types are not the same: Tasic 2018 subtypes in Bugeon, ABC-atlas supertypes in DANDI. We did not
  map one taxonomy to the other.
- Indicators (GCaMP6m against jGCaMP8s), activity measures (deconvolution against event detection),
  imaging rate and the stimulus sets differ between the datasets. The stimulus contrast in DANDI
  mixes gratings and natural movies; in the Bugeon data it is drifting gratings only.
- The Bugeon "stationary synchronised" state is not available in DANDI. We used running correlation
  as the common measure.
- With 4 to 7 mice, a mouse bootstrap has a coarse distribution. We also give leave-one-mouse-out ranges.
- We used 1,031 Bugeon interneurons with gene counts (the paper reports 1,065).

## Plan and deviations

`files/PLAN.md` holds the plan and three amendments. Amendments 1 and 2 were written before any
tPC1-activity analysis: (1) whole session as the primary period because grey-screen blocks are
short, (2) common genes and centring per panel. Amendment 3 (the condition test) was written after
the main results.

## Reproduction

Run `bash files/code/run_all.sh <scratch_dir> [<local Bugeon ZIP>]` with Python 3.12 (numpy,
pandas, requests, matplotlib) and curl. The script writes only into the scratch folder. It reads
about 18 GB of the 128 GB DANDI assets with single Zarr chunk requests (5.2 GB stays on disk) and
about 0.4 GB from figshare (or from the campaign copy datasets/bugeon2022-figshare19448531-v2).
The scripts run in this order: 00, 01 (data), 02 (state measures), 04 (Bugeon cells and tPC1),
03 (DANDI cell table), 05 (DANDI axes), 06 (main tests), 08 (condition test), 09 (grey pupil),
07 (figures). Bootstrap seeds are fixed. The whole run took about 1.5 h on the campaign host.

## Provenance

- Job sci-1107-dell-neural-structure-and-computation-9571ba147340, campaign 11_07_2026, topic
  neural-structure-and-computation, machine dell, model claude-opus-5-5 (Claude Code). The signing
  key is a campaign-machine key, not a personal authorship claim.
- DANDI:002015 draft, read 2026-11-09. Asset IDs, Zarr URLs, DANDI Zarr checksums and bytes read
  are in `files/provenance/dandi002015_assets.csv`.
- Bugeon et al. 2022 data: doi:10.6084/m9.figshare.19448531 v2, ZIP SHA-256
  bd6a6d5eec512bea05196d6b7a54542e745ff3c36a5beb194a6e9cbc043eaa9c. Member hashes are in
  `files/provenance/bugeon_members_sha256.txt`.
- External data terms and attribution: `files/NOTICE-EXTERNAL-DATA.md`. No record-level source data
  is in this publication.
- Prior campaign work on DANDI:002015: sci:sha256:7340d496... (we reused its Zarr HTTP reader).
