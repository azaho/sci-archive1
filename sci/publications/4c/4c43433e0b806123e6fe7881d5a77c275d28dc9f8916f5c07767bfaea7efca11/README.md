# Region-level links from cell types, input wiring and Kv3 expression to spiking almost disappear inside 226 mouse brain regions

Job `sci-1107-hp-neural-structure-and-computation-8636e99187fd`, topic neural-structure-and-computation,
campaign 11_07_2026, machine hp, account claude-olen, model Claude Opus 5.5 (`claude-opus-5-5`).
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

Earlier SCI studies used region means. They found that the cell-type mix of a mouse brain region predicts
its intrinsic spiking, that input wiring predicts task coding, and that Kv3 and Pvalb expression predict
short spikes across regions (48d934f4, 49479722, 8811fcd1, 5d9610e9, eca21679). We asked if these links
also hold **inside** regions, at the 100-300 um scale. Inside a region, layers and sub-nuclei change the
local cell types and the local axon density along one probe.

We placed 61,101 good IBL Brain-Wide Map units (689 probes, 139 mice) in the Allen CCF. For each unit we
calculated the local MERFISH neuron subclass mix (315 subclasses, Gaussian kernel sigma 150 um), the local
ipsilateral input density from 291 source regions in the Knox 2019 voxel model, and local gene expression.
A group is one probe inside one Knox region (2,505 groups in 226 regions). We removed the group means, so
only the variation inside a probe and region remained. A plan was frozen before we calculated any
unit-level outcome statistic (`files/plan/`).

Main results (95% intervals from 1,000 mouse-cluster bootstrap draws):

1. **Most variation is inside groups, but almost none of it repeats across mice.** 61-81% of the unit
   variance of the 7 spike features is inside groups. Units from different mice that are less than 100 um
   apart have a correlation of only 0.0062 (-0.0012 to 0.0150) between their group-demeaned features
   (0.0034, 0.0004 to 0.0064, at 100-200 um). Thus at most about 0.6% of the within-group variance is a
   reproducible spatial map at the IBL localization accuracy (Figure 1c).
2. **Region-level mappings transfer only weakly.** Ridge mappings that we fitted on region means predict
   region means well (10-fold cross-validated r: position 0.56, cell types 0.49, input 0.70; 173 regions).
   Applied to the local predictors of single units, the same mappings gave within-group correlations of
   0.029 (0.012 to 0.035) for cell types, 0.023 (0.012 to 0.031) for input and 0.016 (0.007 to 0.025) for
   position. Cell types and input did not differ (difference 0.006, -0.012 to 0.016). The cell-type value
   is about 14% of the reproducible within-group variance in finding 1 (0.029^2 / 0.0062) (Figure 1a, b).
3. **The cell-type transfer is specific to the true unit position.** When we moved every unit of a probe
   400-600 um along its track, the cell-type transfer fell by 0.0097 (0.0037 to 0.0156). This passed the
   planned peak test. The input transfer fell by 0.0074 (-0.0014 to 0.0167), which did not pass. Position
   splines showed no peak. The cell-type curve was highest at +200 um (deeper), and the input curve was
   highest at -200 um (Figure 3a).
4. **Mappings learned inside groups explained almost nothing.** With whole held-out regions, every model
   had within-group R2 below 0.0004 and every interval included 0. With held-out mice (the same regions
   are in training), R2 was 0.0008 (0.0003 to 0.0014) for cell types, 0.0010 (0.0004 to 0.0017) for
   input and 0.0013 (0.0005 to 0.0019) for both. Their shared part was 0.0006 (0.0003 to 0.0010). The
   unique parts of cell types (0.0002) and input (0.0003) had intervals that included 0 (Figure 3b).
   Thus inside regions we cannot split control between wiring and cell types: the two maps carry the same
   small signal.
5. **Kv3 and Pvalb expression did not predict spike duration inside regions.** Across 191 regions, the
   local Kv3 score (mean of Kcnc1-3) and Pvalb had Spearman rho -0.46 and -0.64 with spike duration.
   Inside groups, the correlations were 0.003 (-0.010 to 0.018) for Kv3, 0.002 (-0.021 to 0.023) for
   Pvalb and -0.000 (-0.011 to 0.011) for the Pvalb-type fraction. The between-region slopes predict
   -0.062 and -0.103. The within-group slope was -0.05 (-0.30 to 0.17) times the between-region slope for
   Kv3 and -0.02 (-0.23 to 0.22) times for Pvalb. The local Kv3 map is reliable at this scale: it had a
   within-group correlation of 0.80 with the second MERFISH brain and 0.85 with itself 100 um along the
   probe. Kv3 and Pvalb were not different from random genes (Figure 2).

Interpretation. The region-level links are real between regions, but they do not describe how spike
features change inside a region. Inside regions, almost all spike-feature variance is cell-to-cell
variance that has no reproducible position at 100-300 um. The between-region association of Kv3 and Pvalb
with short spikes is therefore not a dose-response relation that holds at every scale. It is more likely a
correlate of region identity (for example, which cell classes the probes record in each region). A
quantitative wiring-versus-cell-type split is possible between regions but not inside them with the
present localization accuracy.

## Data

| Input | Version and use |
| --- | --- |
| IBL Brain-Wide Map aggregates `clusters.pqt`, `clusters.acgs_log.npy`, `acgs_log.times.npy` | 2026_Q2 (`aggregates/2026_Q2_IBL_et_al_BWM`); good units (`label == 1`), unit x, y, z, features |
| Session to subject table | `files/data/from_48d934f4/ibl_session_lab_subject.csv` (from sci:sha256:48d934f4..., IBL openalyx) |
| Knox et al. 2019 voxel model `weights.csv.gz` (226,346 x 428), `nodes.csv.gz` (428 x 448,962) | Allen download site; right-hemisphere grey source voxels, grey target voxels, 100 um |
| Knox 2019 `normalized_connection_density.csv.gz` | the list of 291 summary source regions |
| Allen MERFISH C57BL6J-638850 cell metadata with CCF coordinates | 20231215; 2,126,273 neurons (classes 01-29) |
| Zhuang-ABCA-1 cell annotation and CCF coordinates | 20241115 / 20230830; 1,097,888 neurons, replication brain |
| ABC WMB-10X cluster means `precomputed_stats_ABC_revision_230821.h5`, `gene.csv` | 20240831 / 20231215; gene expression per cluster |
| Allen CCF 2017 `annotation_100.nrrd`, structure graph 1 | grey mask, regions, distance to the brain surface |

The exact URLs and SHA-256 values are in `files/provenance/input_sha256.txt` and `files/code/00_get_data.sh`.
In this campaign the files were read from the shared store `./datasets/<name>/` with the names that the
script uses. We hashed each file again before use, and all values agreed with the store provenance.

## Methods

* **Unit features** (definitions of 48d934f4): log10 firing rate, ACG 2-10 ms and 10-100 ms indices
  (relative to 300-1900 ms), ISI burstiness and memory, peak-to-trough duration (ms) and log peak/trough
  ratio. Winsorized at 0.5/99.5% and z-scored.
* **Position.** IBL xyz to CCF with bregma (ML 5739, AP 5400, DV 332 um). The atlas region at the
  transformed position agreed with the IBL region label for 82.5% of units on the 100 um grid. All points
  were mirrored onto the right hemisphere.
* **Local maps.** Counts of MERFISH neurons per subclass and voxel-model input densities on the 100 um
  grid, smoothed with the same Gaussian kernel (sigma 150 um; 100 and 250 um for sensitivity), sampled
  by trilinear interpolation. Composition = smoothed subclass counts / smoothed total, used as
  sqrt(fraction). Input = log10(density), floor 1e-9. Gene scores = mean over local neurons of the 10x
  cluster-mean log2(CPM+1).
* **P1 scale transfer.** Ridge (GCV) of region-mean features on region-mean predictors (173 regions with
  >= 20 units and >= 3 sessions), applied to unit predictors, then the pooled within-group correlation.
* **P2 within-group learning.** Ridge on group-demeaned features and predictors; 10 outer folds of whole
  regions (or mice); alpha per feature by inner 5-fold block cross-validation (amendment 1).
* **P3 misregistration curve.** All units of a probe moved by s = -1000..1000 um along the probe axis
  (first principal axis of all its clusters); maps resampled; P1 and P2 repeated. Peak statistic on the
  53,466 units valid at 0, +-400 and +-600 um.
* **P4.** Within-group correlation and partial correlation of spike duration with local Kv3, Pvalb and the
  Pvalb-type fraction; nulls from 1,000 random gene triplets and 3,000 random single genes.
* **Ceiling (exploratory).** Correlation of group-demeaned features for pairs of units from different mice,
  binned by distance, with a mouse-pair bootstrap (300 draws).

## Deviations from the plan

* Amendment 1 (`files/plan/AMENDMENTS.md`): in the first test run the GCV alpha over-fitted the clustered
  unit data (all out-of-fold R2 < 0). We changed P2, P3, S1 and S3 to inner block cross-validation before
  the full run. The planned design is otherwise unchanged.
* Exploratory additions after the plan: the cross-mouse ceiling (`07_ceiling.py`), the between-region
  cross-validation (`08_between.py`), slope transfer and map reliability for Kv3 (`06_kv3_pvalb.py`,
  section P4b), and the removal of generic expression components (`10_exploratory_checks.py`).
* S3 sensitivity runs used 200 bootstrap draws and no P3.

## Secondary and sensitivity results

* **Replication brain (S1).** With Zhuang-ABCA-1 composition, the cell-type transfer was 0.021 and the
  within-group learned R2 was 0.0001. The two brains gave a median within-group correlation of 0.71 for
  the local subclass fractions at the unit positions.
* **Divisions (S2).** The cell-type transfer was 0.016 to 0.036 in isocortex, hippocampal formation,
  thalamus, striatum, midbrain and the remaining divisions. Within-group learned R2 was at most 0.0017
  (isocortex, all predictors).
* **Technical control (S3).** Adding the axial position, its square and the lateral position on the probe
  did not change the learned R2 (all predictors 0.00036; technical terms alone -0.0002).
* **Kernel width (S3).** Cell-type transfer was 0.022 (-0.005 to 0.028) at sigma 100 um and 0.032
  (0.022 to 0.038) at 250 um. Kv3 and Pvalb within-group correlations stayed inside -0.007 to 0.007 for
  both widths, with intervals that included 0.
* **Kcnc1 alone (exploratory).** Kcnc1 had a within-group correlation of -0.021 (-0.035 to -0.006) with
  spike duration, but 24% of random genes had a larger absolute value. After we removed the first 5
  principal components of 3,000 random-gene scores (57% of their within-group variance), Kcnc1 had
  r = -0.022 (-0.037 to -0.006), with random-gene p = 0.046. This is one of three exploratory tests and
  is weak evidence at most.

## Limitations

* Unit positions come from IBL histology and electrophysiology alignment, and MERFISH positions come from
  registration of one brain (and a second brain) to the CCF. Errors of about 100 um reduce all
  within-group correlations. The cross-mouse ceiling contains the same errors, so it is the ceiling for
  predictors at these positions, not for the true biology.
* The Knox voxel model interpolates sources across injections. Its target-side detail comes from the
  tracer data, but the voxel input maps are smooth.
* The ceiling uses pairs of nearby units from different mice. Its interval is wide (it includes 0 at
  0-100 um), so the 14% share in finding 2 is approximate.
* Extracellular units are a biased sample of neurons (large cells, active cells). The composition maps
  count all neurons.
* Spike duration is quantized in steps of 1/30 ms. Units in one group share a probe and a session.
* The results are associations. They do not show how wiring or cell types cause spiking.
* Unit-level task coding was not available in the shared aggregates, so we did not test the task-coding
  side of the earlier split.

## Reproduction

1. `bash files/code/00_get_data.sh DATA_DIR` (or use the campaign store `./datasets`).
2. `pip install --no-deps --target SCRATCH/pylib pynrrd==1.1.3`.
3. `SCI_DATASETS=DATA_DIR SCRATCH=SCRATCH bash files/code/run_all.sh`. All derived tables go to
   `SCRATCH`, never into the publication. Run time was about 2.5 h on the hp host.

Bundled outputs: `files/results/*.json` (all statistics), `files/results/logs/` (run logs, also the
50-draw test run after amendment 1), `files/figures/` (three figures), `files/plan/` (frozen plan, its
hash and the amendment). Software versions are in `files/provenance/environment.txt`. External terms and
attribution are in `files/NOTICE.md`.

## Figures

* `files/figures/fig1_scale_gap.png`: (a) the same mapping between regions and inside groups; (b) per
  feature transfer and the cross-mouse ceiling; (c) cross-mouse pair correlation against distance.
* `files/figures/fig2_kv3_pvalb_scales.png`: Kv3 and Pvalb against spike duration between regions and
  inside groups; slope ratios; random-gene null.
* `files/figures/fig3_shift_curves.png`: misregistration curves for the transfer (a) and the learned
  models (b).
