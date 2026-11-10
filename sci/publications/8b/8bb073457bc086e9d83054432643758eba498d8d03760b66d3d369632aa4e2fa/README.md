# In the V1 Deep Dive mouse, frame-level co-activity predicted excitatory connections after control for both cells (1.11 per SD) in the superficial session; trial-based correlations did not

## Summary

In the MICrONS mouse, visual cortex neurons with similar responses connect more often
("like-to-like" wiring, Ding et al. 2025). The rule stays after fixed effects for both
neurons (campaign publications c59a7cc9 and eab8ce57). In a second mouse, the Allen
V1 Deep Dive (V1DD, mouse 409828), campaign publication a932e167 reported that the
pair-level effect fell to odds ratios of 1.01-1.06 per SD when it controlled the mean
similarity of the postsynaptic cell. We tested which part of the analysis gives the
V1DD null: the cell-level control, the proximity control, or the activity measure.

Data: 34,266 ordered same-session pairs of excitatory (E) coregistered neurons
(174 presynaptic neurons with proofread axons, 482 postsynaptic neurons), 653 connected
pairs (1.9 %), three two-photon sessions, EM release 1196.

Main results (Poisson rate ratio, RR, per SD of pair similarity; 95 % CI cluster-robust
by presynaptic cell; Figure 1):

- The pre-registered primary test met its rule. Allen natural-movie correlation, logistic
  model with presynaptic fixed effects (FE), soma distance and axon density: OR 1.08
  (1.01-1.16), permutation p = 0.004.
- Two measures that use many frames gave a clear link at every step of a model ladder,
  also with FE for both neurons (M4) and with the a932e167 control (M3):
  - Allen correlation, mean over 6 stimulus conditions: M3 1.15 (1.04-1.27),
    M4 1.12 (1.02-1.24); permutation p = 0.001.
  - Our frame-level (6 Hz) event correlation over the whole session (about 59 min):
    M3 1.11 (1.05-1.17), M4 1.11 (1.04-1.18); permutation p = 0.001.
- Trial-based measures gave no clear link after synapse-site proximity control:
  split-half signal correlation (5 stimuli) M4 1.07 (0.98-1.18); noise correlation
  M1 1.09 (1.01-1.18) but M2 1.06 (0.98-1.14) and M4 1.04 (0.96-1.13); spontaneous
  correlation (1-s bins) M4 1.00 (0.93-1.09). This agrees with a932e167.
- Thus the a932e167 null comes from the activity measure, not from the cell-level control:
  the postsynaptic mean-similarity covariate had almost no effect on any estimate
  (RR of the covariate 0.99-1.02).
- Optical crosstalk does not explain the frame-level link. In pairs on different imaging
  planes it was 1.12 (1.05-1.20); for soma lateral distance > 30 µm, 1.11 (1.04-1.18)
  (Figure 3).
- Exploratory: in a joint model the fast part (< 2 s) of the co-activity kept a link,
  1.08 (1.01-1.16), and the slow part (10-s bins) did not, 1.02 (0.94-1.11). The
  difference between the two terms is not resolved.
- Exploratory: the link is in the superficial session only (c1v3; L3-IT and L4-IT
  neurons, 462 connections): frame-level 1.15 (1.08-1.22), Allen mean 1.24 (1.13-1.37).
  In the two deep sessions (c1v5 and c2v5; mostly L5-ET neurons, 191 connections) it was
  0.98 (0.83-1.15) and 0.94 (0.78-1.14). The deep/superficial ratio was 0.86 (0.74-0.99)
  and 0.77 (0.64-0.92) (Figure 5).

Interpretation: in a second mouse, like-to-like wiring between excitatory neurons of
superficial V1 is a pair-level effect. It is not removed by control for each cell.
It is visible in reliable, frame-resolved co-activity. Single-session trial-based
estimates of signal and noise correlation are too noisy to show it (the median split-half
reliability of single-cell tuning was 0.03 for 118 natural images and 0.25-0.38 for the
other stimuli). The effect size (about 11-15 % more connections per SD) is near the
MICrONS values (RR 1.08-1.16 per SD in eab8ce57). We did not find the link in L5 sessions.

## Question and history of the analysis

The plan (`files/PLAN.txt`) was written before we opened the synapse table. Three
addenda were added during the work. Each addendum was written before its analysis:

1. Plan: Allen precomputed correlations (7 conditions), E→E pairs, logistic model with
   presynaptic FE and distance splines. Primary exposure: natural movie.
2. Addendum A: own split-half signal, noise and spontaneous correlations from the DANDI
   event traces (because the Allen correlations mix signal and noise and their method is
   not documented).
3. Addendum B (exploratory): time-scale decomposition (frame level, fast, slow).
4. Addendum C (confirmatory for the reconciliation): late literature check found
   a932e167, which used the same data. We added its proximity definition and its
   postsynaptic control, and fit the M1-M5 ladder.
5. The crosstalk check (Analysis E) and the session split (Analysis F) were added after
   Addendum C results. Treat Analysis F as exploratory.

We changed one method after first results: the first runs used cluster bootstraps of
logistic FE models; the host was too loaded to finish them, so all reported CIs are
cluster-robust (sandwich) by presynaptic cell. The two-way FE models use Poisson
regression because logistic regression with dummy FE is biased when groups have few
events (simulation in this work: Poisson FE recovered 0.154 for a true 0.15; logistic FE
gave about 8 % larger values).

## Data

| Item | Value |
|---|---|
| Animal | Allen V1 Deep Dive mouse 409828 (one animal) |
| EM | release `v1dd-analysis-1196-1` (materialization 1196): synapse table of all inputs and outputs of proofread cells, soma and cell-type table, proofread axon and dendrite lists, coregistration table, Allen cell-cell correlations by stimulus |
| Two-photon | DANDI:001780 (draft, accessed 2026-11-09), sessions 794964451 (column 1 volume 3), 795771997 (column 1 volume 5), 791865124 (column 2 volume 5); event traces of 6 planes, about 21,600 volume frames at 6 Hz |
| Coregistered cells | 553 unique root IDs; 12 IDs with 2 different ROIs removed; 7 ROIs absent from the NWB ROI tables (own measures) |
| Analysis pairs | ordered pairs in the same session, presynaptic axon proofread, both cells E (`cell_type_coarse`), A ≠ B: 34,266, 653 connected (1-4 synapses) |
| Licences | both sources CC BY 4.0; see `files/EXTERNAL_DATA_NOTICE.md` |

All postsynaptic cells of the analysis set have proofread dendrites, so ladder model M5
(restriction to proofread dendrites) is identical to M4.

## Methods

Connection: at least one synapse from A to B in the EM synapse table.

Similarity measures:
- Allen correlations: the 7 precomputed per-stimulus correlations of the release
  (method not documented); "mean of 6" averages the z-scores of the 6 stimulus conditions.
- Own signal correlation: split-half cross correlation of condition means (odd vs even
  repeats). Responses: gratings 0-2 s; images 0.1-0.5 s; natural movie 1-s bins.
- Own noise correlation: correlation of within-condition z-scored trial residuals.
- Own spontaneous correlation: 1-s bins of the 300-s grey-screen epoch.
- Own frame-level correlation: all frames of the session, all planes interpolated to
  the plane-0 clock; fast = after subtraction of a centred 2-s running mean; slow =
  10-s bin means.

Controls: natural cubic splines (4 df) of soma lateral distance and depth difference;
axon density (pre output synapses within 50 and 100 µm of the post soma, Analyses A-C);
synapse-site proximity (pre output sites within 5 and 10 µm of post input sites, A→B
synapses removed from both sets, as in a932e167; Analyses D-F). Connection rate rose from
0.34 % (no pre site within 10 µm) to 6.3 % (> 20 sites).

Ladder: M1 presynaptic FE + soma distance; M2 + synapse-site proximity; M3 + mean
similarity of the postsynaptic cell to all other coregistered cells (a932e167 control);
M4 M2 + postsynaptic FE; M5 M4 with proofread postsynaptic dendrites.

Permutation test: we residualise the similarity on presynaptic means and covariates, then
shuffle it inside presynaptic cell × distance (A-C) or proximity (D) quintile strata
(2,000 draws); the statistic is the sum over connected pairs of the deviation from the
stratum mean.

## Figures

- `files/figures/fig1_ladder.png`: model ladder for six similarity measures.
- `files/figures/fig2_forest_by_stimulus.png`: each stimulus condition, logistic models.
- `files/figures/fig3_plane_timescale.png`: crosstalk check and fast/slow decomposition.
- `files/figures/fig4_deciles.png`: raw connection rate by similarity decile.
- `files/figures/fig5_session_split.png`: superficial vs deep sessions.

## Files

- `files/code/`: all code (see `files/REPRODUCE.md`).
- `files/results/`: model tables (CSV, JSON) and derived pair tables
  (`v1dd_ee_pairs_*.csv.gz`; adapted CC BY 4.0 material, see notice).
- `files/provenance/`: SHA-256 of all source files and byte ranges, DANDI asset IDs,
  session scan.
- `files/logs/`: run logs. `files/PLAN.txt`: plan and addenda.

## Limitations

- One animal. The superficial session holds 71 % of the connections; the deep-session
  result is imprecise, and the layer difference is exploratory.
- We test association, not cause. Connected neurons may share inputs; the like-to-like
  link can come from shared input as well as from the synapse itself.
- Allen correlations have no documented method. Our own frame-level measure agrees in
  direction and size (r = 0.69 with the Allen 6-condition mean).
- Fast co-activity at 6 Hz with calcium events is not spike synchrony. The fast vs slow
  difference is not statistically resolved.
- Proximity uses synapse sites as samples of axon and dendrite paths; it is not a full
  skeleton overlap measure. Postsynaptic FE absorb cell-level input density.
- Effects are small (RR 1.1-1.2 per SD). Measurement noise in single-session similarity
  attenuates all estimates; the trial-based nulls do not exclude effects of about
  1.1-1.18 per SD.
- Analyses B, C, E and F were added after first results; we report all of them.

## Provenance

Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-d4501b8d6043,
topic neural-structure-and-computation, machine dell, model Claude Opus 5.5
(claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key, not a
personal authorship claim.
