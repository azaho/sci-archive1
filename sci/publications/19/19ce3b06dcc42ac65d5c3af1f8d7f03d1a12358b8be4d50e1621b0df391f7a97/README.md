# Trained fly visual-system connectome models keep their motion tuning with the column-offset synapse profiles of two other flies, but lose it when type-pair synapse totals change (10 flyvis models)

**Job** sci-1107-dell-neural-structure-and-computation-7357ec7c68af · **topic** neural-structure-and-computation ·
**machine** dell (campaign 11_07_2026) · **model** Claude Opus 5.5 (claude-opus-5-5) · **date** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Connectome-constrained models of the fly visual system (flyvis; Lappalainen et al. 2024) take their wiring from one
7-column FIB-25/FIB-19 reconstruction. Then they train only one strength per cell-type pair and the neuron
parameters. The models predict the tuning of many cell types, for example the direction selectivity (DS) of T4 and T5.
Each fly has a different connectome. Thus we ask: **do the predictions stay the same when we put the synapse counts of
other optic lobes into the trained models?** If the predictions change, which part of the count difference causes
the change? We also tested a pre-specified "sloppiness" hypothesis (H2): real between-animal count differences
change the model responses less than random differences of the same size.

The campaign record had no publication that used flyvis when we chose the question. One later publication
(sci:sha256:6c1fffed) compares the original flyvis models with calcium data. This work is the first
cross-connectome test of these models. It is the functional consequence of the fly synapse-count variability results
of sci:sha256:04069535, sci:sha256:f072f243 and sci:sha256:82b12617, and the convolutional-model counterpart of the
whole-brain spiking-model comparisons sci:sha256:7d2472fd and sci:sha256:34240293.

## Data and approach (short; full detail in "Methods")

- **Models:** the 10 best of the 50 pretrained flyvis models (ensemble `flow/0000`, 65 cell types, 721 columns).
- **New count tables:** FlyWire v783 right and left optic lobes (female, TEM; 31 column-assigned types) and male CNS
  v1.0 right and left (male, FIB-SEM; 28 types). For each optic lobe we computed the flyvis count estimator: the mean
  synapse count per (source type, target type, column offset). We aligned the hex lattice to the FIB25 frame and
  replaced the 710 model keys whose two types are column-assigned. These keys hold 46% of the model synapse mass.
  Each table was scaled to the FIB25 total. A consensus table is the geometric mean of the four large optic lobes.
- **Decomposition:** *shape* = the new offset profile inside each type pair with FIB25 type-pair totals; *gain* = the
  FIB25 offset profile with the new type-pair totals. **Positive control:** FIB25 counts permuted across offsets
  inside each type pair. **Nulls (H2):** per-key ratios permuted across keys (*shuffle*), or type-pair ratios and
  per-key residuals permuted separately (*pairs*), 2 draws each.
- **Read-outs:** flyvis flash response index (FRI, ON/OFF polarity), DSI and preferred direction (PD) for ON and OFF
  edges in 12 directions at 13 deg/s, and agreement with the flyvis ground-truth lists from experiments.
  10 models x 27 conditions = 270 simulations.

## Results

### 1. The FIB25 table differs from all four large optic lobes; they agree with each other (Figure 1)

| Comparison (701 shared keys) | SD of log count difference |
|---|---|
| FIB25 vs each large optic lobe | 0.53-0.56 |
| FlyWire vs male CNS (different flies, sexes and methods) | 0.25-0.34 |
| Left vs right of the same fly (FlyWire; male CNS) | 0.30; 0.22 |
| FlyWire right: own columns vs partner-assigned columns | 0.20 |
| FlyWire 7-column patch vs its full optic lobe (20 patches) | 0.68-0.97 (mean 0.75) |

The deviations of the four large optic lobes from FIB25 correlate with each other (r = 0.81-0.92). Thus most of the
FIB25 difference is specific to FIB25. A FlyWire table built from only 7 columns of postsynaptic cells differs from its
own full optic lobe even more (mean 0.75). Thus the FIB25 difference is in the range of 7-column sampling noise.
The large optic lobes agree on some large type-pair changes relative to FIB25. Examples are Tm9->T5 (log2 -0.6 to -1.0),
C3->T4 (-0.3 to -0.45) and Tm3->T4 (+0.35 to +0.75) (Figure 1C).

### 2. Real count tables degrade motion tuning but not flash polarity (Figure 2A-C, Figure 3)

Medians over 10 models; Wilcoxon signed-rank test against the FIB25 model of the same network.

| Condition | DSI vs known motion tuning (r) | T4/T5 subtypes with correct PD (of 8) | FRI vs known polarity (r) |
|---|---|---|---|
| FIB25 (original) | 0.68 | 5.5 | 0.80 |
| FlyWire R | 0.47 (8/10 lower, p = 0.027) | 3.0 (p = 0.055) | 0.62 (paired p = 0.63) |
| FlyWire L | 0.44 (9/10 lower, p = 0.004) | 4.5 | 0.78 |
| FlyWire R, partner-assigned columns | 0.47 (p = 0.020) | 3.0 | 0.61 |
| male CNS R | 0.19 (9/10 lower, p = 0.010) | 2.5 | 0.71 |
| male CNS L | 0.36 (p = 0.020) | 3.0 (p = 0.027) | 0.67 |
| consensus of 4 optic lobes | 0.50 (p = 0.049) | 3.0 | 0.68 |

With every real table, one or more T4/T5 subtypes stopped responding to edges in some models (median 0.5-1.5 of 8
subtypes). Their polar tuning became flat or reversed (Figure 3). Flash polarity agreement did not change consistently
(paired p = 0.32-1.0 for all six real tables). The FlyWire partner-assigned-column control was almost identical to
FlyWire with its own columns (prediction distance 0.002). Thus the column-assignment method that we had to use for the
male CNS does not explain its larger effect.

### 3. The type-pair totals cause all of the change; the new offset profiles cause none (Figure 2D-E)

| Condition | DSI r | PD correct | median response change D_edge |
|---|---|---|---|
| FlyWire R shape / gain | 0.69 / 0.44 | 5.5 / 3.0 | 0.001 / 0.18 |
| male CNS R shape / gain | 0.69 / 0.25 | 5.5 / 3.0 | 0.001 / 0.42 |
| consensus shape / gain | 0.69 / 0.47 | 5.5 / 3.0 | 0.001 / 0.20 |
| FIB25 offsets permuted inside type pairs (2 draws) | 0.59-0.64 (10/10 lower, p = 0.002) | 4.5-5.0 | 0.003-0.005 |

The real shape changes are large (log-SD 0.44 per key; 22% of the synapse mass moves between offsets). But they left
DS and PD unchanged (median DSI r change +0.001 to +0.014; PD unchanged). The smaller random offset permutation inside type pairs did lower
DS in all 10 models. Thus the models are sensitive to offset structure, and the offset structure of three other
optic lobes is compatible with the trained models. The gain-only tables reproduced the full damage of the real tables.

### 4. Post hoc localisation (Figure 2G-H)

Restoring the FIB25 values of all keys that target T4a-d and T5a-d gave partial recovery (DSI r 0.52 for FlyWire R,
0.46 for male CNS R; PD 5.0 and 4.0 of 8). Restoring only Tm9->T5 did not help (0.47; 0.19). Thus part of the damage
comes from the T4/T5 input totals and part comes from upstream type pairs. The cell types with the largest
response change were not only T4/T5. Examples are TmY9, Mi2, T3 and TmY types for FlyWire, and T4d, TmY18 and Mi3 for
male CNS (files/results/per_type_change.csv).

### 5. H2 (real differences less disruptive than random ones): not supported

Pre-specified criterion: D_edge(real) < D_edge(null) in >= 70% of models with p < 0.05, for both nulls and both bases.

| Base | shuffle null: real smaller, p | pairs null: real smaller, p |
|---|---|---|
| FlyWire R | 8/10, p = 0.064 (median ratio 0.44) | 6/10, p = 0.56 |
| male CNS R | 5/10, p = 0.92 | 9/10, p = 0.027 |

Only 1 of 4 tests passed, so H2 is not supported. The random nulls did lower flash-polarity agreement more than the
real tables (for example FlyWire R shuffle draw 0: FRI r 0.26, p = 0.006). Two null runs of model 007 became unstable
(flash responses diverged to NaN). No real-table run became unstable.

### 6. Between-animal vs within-animal prediction differences (H3)

Median distance between the predictions of two conditions in the same model (1 - r of the peak edge-tuning vectors):
left vs right 0.009 (FlyWire) and 0.010 (male CNS); FlyWire vs male CNS 0.057-0.16; FIB25 vs a real table 0.05-0.06;
two different flyvis models with FIB25 counts 0.105. Mean |change of FRI|: left vs right 0.04-0.06, FlyWire vs male
CNS 0.12, FIB25 vs a real table 0.15-0.17, between models 0.20. Thus in these models the two eyes of one fly give
almost the same predictions, and different flies give clearly different predictions. These between-fly differences
are smaller than the differences between independently trained models.

## Interpretation

In flyvis, the weight of an edge is a trained type-pair strength times a fixed count. A change of the type-pair total
is therefore the same as a change of the trained strength. The result says that the models' motion tuning sits in a
narrow region of strength space. The type-pair totals of other optic lobes (or of their consensus) move the models out
of that region. The part of the connectome that the models take from the data and do not retrain is the offset
profile inside each type pair. This part transferred to the optic lobes of two other flies, both eyes and both
sexes, without loss. The result supports the use of the spatial (offset) structure of one connectome to constrain
these models. It also shows that the absolute type-pair synapse totals of a single small reconstruction are not
a fixed property that a trained model can be moved between animals with. We did not retrain models on the new tables,
so we cannot say whether models trained on FlyWire or male CNS counts would reach the same tuning.

## Limitations

- **No retraining.** The test is a transplant into trained models. Retraining on GPU was not possible on this machine
  (2 CPUs). The gain result is expected to disappear if strengths are retrained; this was not tested.
- **One speed (13 deg/s) and dt = 0.01 s.** Lappalainen et al. averaged several speeds and used finer time steps for
  evaluation. With our settings, the original models gave the correct PD for a median of 5.5 of 8 subtypes (range 0-8;
  models 004 and 005 had 1 and 0). All comparisons are paired inside the same model and settings.
- **10 of 50 models, 2 draws per null.** The H2 tests have low power.
- **Partial replacement.** Only the 710 keys between the 31 (male CNS: 28) column-assigned types were replaced; other
  keys kept FIB25 values. 14-18% of the new optic lobes' synapse mass between replaced type pairs fell on offsets that
  the model has no edge for and was dropped. Male CNS has no R7, R8 and Tm21 labels.
- **Columns.** Male CNS columns of 16 types came from our partner rule (55-99% agreement with FlyWire's own columns on
  FlyWire). The FlyWire partner-assigned control shows that this has little effect on the predictions. The lattice
  orientation was one fit per optic lobe (12 candidates).
- **Estimator.** We copied the conditional-mean estimator of the flyvis table. The original FIB25 table also merged
  FIB-19 data and scaling steps that we did not reproduce for the other optic lobes. The global normalisation removes
  only overall detection differences between EM methods.
- **Ground truth.** We used the flyvis ground-truth lists (polarity of 29 types, motion tuning of 18 types, PD of 8
  subtypes), not new measurements.
- Post hoc analyses (section 4, the per-type ranking) were added after the main results. They are labelled post hoc.

## What remains open

1. Retrain flyvis models with FlyWire, male CNS and consensus counts (GPU), and compare the predictions with the FIB25
   ensemble and with calcium data (sci:sha256:6c1fffed used Currier and Clandinin 2025 flicker data).
2. A full single-type-pair "rescue" screen to find which type-pair totals move the models out of the tuned region.
3. All 50 models, several speeds and finer dt; more null draws for H2.
4. Male CNS columns for all types from the Janelia optic-lobe hex tables, if they become available.

## Methods

### Models
We used the 50 pretrained connectome-constrained models of the fly visual system from flyvis 1.2.0
(Lappalainen et al. 2024, Nature 634:1132; ensemble `flow/0000`, trained on optic flow from Sintel). Each model has
65 cell types on a hexagonal lattice of 721 columns. The weight of an edge is
`sign(src,tar) x syn_strength(src,tar) x syn_count(src,tar,du,dv)`. `syn_count` is a fixed (not trained) mean
synapse count per source type, target type and column offset, taken from the FIB-25/FIB-19 7-column reconstructions
(`fib25-fib19_v2.2.json`, 2,355 keys). `syn_strength` (one value per type pair), resting potentials and time
constants were trained. The models are sorted by validation loss; we used the 12 best (000-011).

### Count tables from other optic lobes
- FlyWire v783 (female, TEM): column assignment of 31 columnar types (codex `column_assignment.csv.gz`) and the
  proofread connection table (Zenodo 10676866). Hex coordinates `u = p, v = -q`.
- Male CNS v1.0 (male, FIB-SEM, Janelia FlyEM): `assignedOlHex1/2` (`u = hex1, v = -hex2`) exist for only 12-15
  types. We used these 12 types on both sides as anchors and gave every other neuron of the 28 shared columnar types
  the anchor column with the most synapses to it (inputs and outputs). On FlyWire, where all 31 types have columns,
  this rule recovered the FlyWire column exactly for 55-99% of neurons by type (T4/T5 76-89%). We also ran FlyWire
  right with partner-assigned columns (FlyWire R*) as a control for the assignment method.
- For each optic lobe we computed, per (source type, target type, du, dv), the mean synapse count over connected
  pairs (the estimator of the flyvis table). We chose the lattice orientation (one of 12 symmetries, one choice per
  optic lobe) with the best correlation to the FIB25 table on off-centre offsets (FlyWire: rot60 for both eyes,
  r = 0.60; male CNS: Rrot240 for both eyes, r = 0.57-0.59; the next best orientation was at least 0.06 lower).
- We replaced only keys whose source and target types are both column-assigned (710 keys, 701 for male CNS, which has
  no R7, R8 and Tm21 labels). These keys hold 46% of the model synapse mass. All other keys kept their FIB25 values.
  Each replacement table was scaled so that its total over replaced keys equals the FIB25 total (global
  normalisation). Keys absent in a new optic lobe were set to zero; 14-18% of the new lobe's synapse mass between
  replaced type pairs falls on offsets that the model has no edge for and was dropped.
- Consensus: geometric mean of log(n + 0.5) of FlyWire R, FlyWire L, male CNS R and male CNS L.

### Conditions (per model)
`orig` (FIB25), five real tables, `cons`; decomposition `X^shape` (offset profile of X, FIB25 type-pair totals) and
`X^gain` (FIB25 offset profile, type-pair totals of X) for X = FlyWire R, male CNS R, consensus; positive control
`fib~offsetperm` (FIB25 counts permuted across offsets inside each type pair, 2 draws); matched nulls for
FlyWire R and male CNS R (2 draws each): `shuffle` (per-key ratio new/FIB25 permuted across all keys) and `pairs`
(type-pair geometric-mean ratio permuted across type pairs and per-key residual ratio permuted across keys).

### Stimuli and read-outs
flyvis stimuli and indices: full-field flashes (1 s, radius 6, ON and OFF) -> flash response index (FRI); moving ON
and OFF edges in 12 directions at 13 deg/s -> peak rectified central-cell responses, direction selectivity index
(DSI) and preferred direction. Euler step dt = 0.01 s (the flash FRI at 0.01 s agreed with 0.005 s, r = 0.992, no
sign changes; dt = 0.02 s gave two sign changes). Agreement with experiment uses the flyvis ground-truth lists:
known polarity of 29 types (FRI correlation and sign count), motion-tuned (T4a-d, T5a-d) vs not motion-tuned types
(DSI correlation), and known preferred directions of T4/T5 subtypes (error <= 45 deg counts as correct). A type is
"silent" to edges when its peak rectified central-cell response is below 1e-3 for all 24 edges. Response change
`D_edge` = median over 65 types of 1 - Pearson r between the central-cell edge responses (all frames, 24 edges)
under a condition and under `orig` in the same model.

### Statistics
Per-model paired comparisons with the FIB25 model of the same network use the Wilcoxon signed-rank test (n = 10
models, two-sided; `files/results/paired_vs_orig.csv`). The H1-H3 summaries are in `files/results/tests.json`.
H1 as pre-specified: (a) median drop of FRI correlation < 0.1 was met for all real tables (paired median change -0.02
to +0.02); (b) PD within 45 deg for >= 75% of model x subtype was not met even by the original models at our settings
(64%); real tables gave 35-49%.

## Files

- `files/figures/fig1_tables.png`, `fig2_predictions.png`, `fig3_t4t5_tuning.png`: figures.
- `files/data/variants/*.csv`: per-key count tables (columns `n_fib` = FIB25 table, `n_cond` = conditional mean
  in the new optic lobe, `n_all` = mean per postsynaptic cell, `n_pairs`, `n_post`) for fw_R, fw_L, fwA_R, mc_R, mc_L,
  cons; `summary.csv` = orientation and fit; `struct_pairwise.csv`, `patch_noise.csv`, `input_gains.csv`,
  `assign_calibration.csv`.
- `files/results/metrics_model_condition.csv`: all read-outs per model and condition; `summary_by_condition.csv`;
  `paired_vs_orig.csv`; `tests.json`; `H3_pair_distances.csv`; `per_type_change.csv`;
  `per_run_type_readouts.csv.gz`: FRI, DSI, PD, response correlations and peak tuning per model x condition x cell
  type (17,550 rows).
- `files/code/`: all code (see below); `requirements-venv.txt` (exact package versions).
- `files/NOTICE-EXTERNAL-DATA.md`: sources, licences, hashes and attribution of external data.

## Reproduce

1. `bash files/code/retrieve.sh DEST` downloads the external inputs into `DEST/datasets/...` and
   `DEST/work/ext/...` and checks the SHA-256 values. Copy `files/code` to `DEST/work/code`; run all steps in `DEST/work`.
2. Environment: `uv venv --python 3.12 .venv`; install `torch==2.15.0+cpu` and `torchvision==0.29.2+cpu` from
   `https://download.pytorch.org/whl/cpu`, then the rest of `requirements-venv.txt` (flyvis 1.2.0 with its deps).
   The code reads the FIB25 table from `.venv/lib/python3.12/site-packages/flyvis/connectome/fib25-fib19_v2.2.json`.
   Set `OMP_NUM_THREADS=1`.
3. Tables: `python code/extract_flywire.py ../datasets`, `python code/extract_mcns.py ../datasets`,
   `python code/calib_assign.py`, `python code/build_variants.py`, `python code/build_consensus.py`,
   `python code/struct_compare.py`, `python code/patch_noise.py`, `python code/input_gains.py` (writes `scratch/`).
4. Stimuli: `.venv/bin/python code/render_edges.py` (about 55 min once; cached in `ext/flyvis_root/renderings`.
   If a renderer is killed, delete `renderings/RenderedOffsets_0000`, because flyvis then waits for ever).
5. Simulations: `.venv/bin/python code/run.py scratch/runs 13 0.01 000,001,...,009` (resumable; about 1-3 min per
   model x condition on one CPU; 270 runs in about 8 CPU-hours). `code/handoff.sh` was only used to schedule the runs.
6. Analysis: `code/analyze.py scratch/runs scratch/analysis`, `code/paired_tests.py scratch/analysis`,
   `code/export_runs.py scratch/runs scratch/analysis/per_run_type_readouts.csv.gz`, `code/fig_struct.py`,
   `code/fig_results.py scratch/analysis scratch/runs`.

Notes: runs 000-006 (and part of 007) were made before `torch.set_flush_denormal(True)` was added to `sim.py`
(added to fix a 25-minute stall of one 007 run). This changes only values below 1e-38.

## References

- Lappalainen J. K. et al. (2024) Connectome-constrained networks predict neural activity across the fly visual
  system. Nature 634:1132-1140. doi:10.1038/s41586-024-07939-3. Code and models: https://github.com/TuragaLab/flyvis
- Takemura S. et al. (2017) eLife 6:e24394; Shinomiya K. et al. (2019) eLife 8:e40025 (FIB-19/FIB-25 medulla).
- Dorkenwald S. et al. (2024) Nature 634:124 (FlyWire); Schlegel P. et al. (2024) Nature 634:139; Matsliah A. et al.
  (2024) Nature 634:166 (optic lobe columns); Buhmann J. et al. (2021) Nat Methods 18:771 (synapses).
- Nern A. et al. (2025) Nature (male optic lobe); Janelia FlyEM male CNS v1.0, https://male-cns.janelia.org/
