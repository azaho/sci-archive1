# Inside mouse brain regions, the between-region input-wiring rule predicts unit spike physiology more robustly than the cell-type rule (IBL, 162 regions)

**Job** sci-1107-dell-neural-structure-and-computation-0477008f4415 · **campaign** 11_07_2026 ·
**topic** neural-structure-and-computation · **machine** dell · **account** claude-olen ·
**model** Claude Opus 5.5 (`claude-opus-5-5`) · **date** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work split wiring control and cell-type control of mouse brain physiology only
*between* regions. It used region medians (sci:sha256:49479722, sci:sha256:f4e4c521,
sci:sha256:a4fae2b2, sci:sha256:36eebd98, sci:sha256:8811fcd1). In that work, cell-type mix was the
stronger predictor of intrinsic spiking, with a wiring share of 0.25. Region-level tests have one
general weakness. Region identity, brain division and geometry go together with every structural
map. Thus a region-level link can come from region identity and not from a local mechanism.

We asked the same question **inside** regions, at 100 um scale:

1. Does the spike physiology of a unit follow the local neuron-type mix at its position (MERFISH),
   or the local afferent input profile at its position (Knox 2019 voxel model)?
2. Do the structure-to-physiology rules that hold *between* regions also hold *inside* regions?
3. Is the wiring versus cell-type split the same at the two scales?

## 2. Data

| Item | Content |
|---|---|
| Units | IBL Brain-Wide Map 2026_Q2, label-1 units, rate > 0.1 Hz. Primary sample: 52,753 units in 162 Knox regions (>= 40 units, >= 3 sessions), 456 sessions, 139 mice, 12 labs. The 100 um voxel label of each unit agrees with its IBL region. |
| Features | 9 amplitude-free features of sci:sha256:36eebd98: log rate, burstiness, memory, 3 ACG windows, peak-trough duration, half-peak duration, peak-trough ratio. Each is z-scored over units. |
| Position | IBL x, y, z converted to Allen CCF (bregma ML 5739, AP 5400, DV 332 um), folded to the right hemisphere. |
| Input map I | Knox et al. 2019 voxel model, W = weights x nodes (226,346 source voxels x 448,962 target voxels). For each target voxel: input from each of 291 source regions (ipsilateral, and contralateral through the mirror voxel). Sources in the unit's own region are removed. Shares, then square root. We checked the voxel order: regional sums of W reproduce the published regional matrix (r = 1.000). |
| Cell-type map T | Allen MERFISH brain C57BL6J-638850, 2.13 million neurons (classes 01-29), 315 subclasses, counted on the 100 um grid and smoothed (Gaussian sigma 150 um). Shares, then square root. Replication: Zhuang-ABCA-1 (1.10 million neurons, same taxonomy). |

Exact source URLs, shared-store paths and SHA-256 values are in `files/provenance/`.

## 3. Methods

A plan was written and hashed before any structure-physiology statistic (`files/plan/PLAN.md`).
Three dated addenda record every later, exploratory analysis and what we saw before each
(`files/plan/ADDENDUM_1..3.md`, hashes in `PLAN_hash.txt`).

* **Planned test (H1-H3).** We removed the region mean of each feature, and we reduced T and I
  inside regions to 10 principal components each. We fitted OLS models of position (G), G+T, G+I
  and G+T+I with 10-fold cross-validation by region (the rule must transfer to unseen regions) and
  by mouse. The null rotated the unit positions about each region centroid and then took the map
  value of the nearest voxel of the same region (200 draws planned, 110 completed). Uncertainty came from a region
  bootstrap.
* **E1. Variance components and spatial ceiling.** We split the variance into region,
  insertion-in-region and unit-in-insertion parts. We tested if units or insertions in *other* mice
  at nearby positions predict the deviations (calibrated with a centroid-shuffle null).
* **E2. Scale transfer (main exploratory test).** We fitted the *between-region* map from
  region-mean T (or I) to region-mean physiology (10 PCs, OLS; cross-validated R2 reported). Then
  we applied the same coefficients to each unit's within-region structure deviation. If the rule
  acts locally, the slope of observed on predicted within-region deviations is near 1 times the
  attenuation from localisation error. If the rule only reflects region identity, the slope is
  near 0. Controls: 200 rotation draws, interior units, a border-bleed term (expected physiology
  shift from nearby voxels of other regions), per-region linear position removal, insertion
  centring, a second MERFISH brain as an instrument, and leave-one-division-out.
* **Split at two scales.** Between regions: unique cross-validated R2 of T and I (20 x 10-fold).
  Inside regions: unique R2 of the T- and I-predicted deviations in a joint regression with the
  border-bleed term. Wiring share sI = uI / (uI + uT). We used a paired region bootstrap for the
  difference.

## 4. Results

### 4.1 Unit physiology inside a region is mostly not spatial (Figure 1)

* Between-region differences hold 11.6% of unit variance. Offsets between insertions in the same
  region hold 15.5%. Units inside one insertion hold 72.9%.
* Insertion offsets are reliable inside an insertion (odd/even split, Spearman-Brown 0.65-0.86).
  But the nearest insertion in another mouse (median 202 um away) shares them only weakly:
  r = 0.02 against a shuffle-null mean of -0.06 (p = 0.001). The excess correlation was 0.041 at
  0-250 um and 0.028 at 250-500 um (p <= 0.002), and 0 at 0.5-1 mm. Thus only a few percent of
  the insertion offset is spatial. Most of it is specific to the session or insertion.
* Neighbours from other mice inside 150-800 um did not predict a unit's within-region deviation
  (out-of-mouse R2 -0.005 to -0.038 with shrinkage; part of this negative value is a centring
  artefact; `results/ceiling.json`, `results/ceiling_insertion.json`).

### 4.2 The planned test failed: no within-region rule could be learned (Figure 2)

All planned models had out-of-fold R2 between -0.004 and +0.001 (leave regions out: G -0.0030,
G+T+I -0.0037; uT -0.0006, 95% CI -0.0023 to 0.0008; uI -0.0001, CI -0.0017 to 0.0015).
Leave mice out gave uT 0.0002 (CI -0.0008 to 0.0011) and uI 0.0008 (CI -0.0010 to 0.0027).
All 8 planned robustness variants gave |uT|, |uI| < 0.006 (Figure 2b).

But the rotation-null draws were *more* negative than the observed values. With real maps the
models lost less accuracy than with misaligned maps: leave regions out, uT p = 0.018 and uI
p = 0.009 (null means -0.0028 and -0.0022; 110 draws); leave mice out, uT p = 0.054 and uI
p = 0.027. Region-specific ridge models with leave-mouse-out inside each region (159 regions)
gave the same pattern: uI 0.0031 (p = 0.0099, 100 draws) and uT 0.0002 (p = 0.54).

**Decision on the hypotheses.** H1 and H2 asked for uT > 0 and uI > 0 beyond the rotation null.
Both gains beat the null, but neither was above zero. Thus we do not count H1 or H2 as supported.
H3 (sI < 0.5) could not be tested because the planned sI interval was undefined (-2.9 to 5.4).
The within-region signal is too small, relative to unit noise, for a rule to be *learned* from
within-region data. But the real maps carry aligned information, and the input map carries more
of it. Section 4.3 tests this directly.

### 4.3 The between-region rules do transfer into regions (Figure 3)

| Map | Between-region CV R2 (10-fold; leave-division) | Within-region slope [95% CI] | Rotation null 95% | p | Expected slope at 100 / 200 um error |
|---|---|---|---|---|---|
| Cell types T (MERFISH 638850) | 0.54; 0.37 | 0.54 [0.35, 0.70] | -0.22 to 0.22 | 0.005 | 0.79 / 0.55 |
| Cell types T (Zhuang-ABCA-1) | 0.50; 0.24 | 0.32 [0.12, 0.48] | -0.18 to 0.20 | 0.005 | 0.80 / 0.57 |
| Input I (Knox voxel model) | 0.48; 0.28 | 0.45 [0.25, 0.64] | -0.11 to 0.15 | 0.005 | 0.68 / 0.47 |
| T and I together | 0.56; 0.37 | 0.66 [0.44, 0.85] | -0.19 to 0.19 | 0.005 | 0.77 / 0.55 |

(p is two-sided; 0.005 is the smallest value possible with 200 draws.)

The maps vary much less inside regions than between them. The SD of predicted within-region
deviations is 0.06 (T) and 0.08 (I) z units, against 0.30 and 0.29 between regions. Thus the
explained within-region variance is very small even though the slopes are clearly positive: the
unscaled predictions give R2 -0.0007 (I) to 0.0015 (T and I), and the fitted joint model of
section 4.4 explains 0.37%. Slopes stayed positive for interior units more than 200 um from the region
edge (T 0.47 [0.01, 0.88]; I 0.40 [0.04, 0.64]) and with the border-bleed term removed (T 0.35
[0.15, 0.51]; I 0.37 [0.20, 0.56]). Units near an edge took on most of the physiology of the
adjacent region (bleed slope 0.97), but this term explained only 0.24% of within-region variance.

### 4.4 The split changes with scale (Figure 4)

* **Between regions** (same 162 regions and units): T R2 0.55, I 0.48, T+I 0.57; unique T 0.085
  [0.046, 0.126], unique I 0.020 [-0.007, 0.048]; **wiring share 0.19 [-0.10, 0.39]**. This
  agrees with the earlier 0.25.
* **Inside regions** (joint regression with border bleed): slope of the T-predicted deviation 0.26
  [0.07, 0.41], slope of the I-predicted deviation 0.35 [0.16, 0.53]; **wiring share 0.78
  [0.29, 0.99]**. Within minus between: **+0.59 [0.09, 0.94]** (bootstrap P(difference <= 0) = 0.01).
* The I slope was robust. It was 0.36 [0.13, 0.58] after removal of each region's own linear
  position gradient, 0.28 [0.10, 0.47] with insertion centring, 0.36 [0.17, 0.55] with the second
  MERFISH brain as instrument for T, and 0.27-0.39 when any one division was left out.
  The unique T slope was not robust: 0.11 [-0.13, 0.33], 0.19 [-0.06, 0.44] and 0.11
  [-0.13, 0.34] under the same three controls. The two MERFISH brains gave similar predictions
  (r = 0.74), so noise in the cell-type map does not explain the weak unique T slope.
* By feature (point estimates), the I map carried the ACG and burst features (acg_mid 0.75,
  burstiness 0.48). The T map carried rate and spike width relatively more (lfr 0.38, ptd 0.31).

## 5. Interpretation

1. Below the region scale, IBL unit physiology is dominated by unit-to-unit and insertion-to-insertion
   variation. Reproducible spatial structure inside a region is small and decays by about 0.5 mm.
   Thus region-level medians in brain-wide studies carry large insertion noise, and a within-region
   structure-physiology rule cannot be *learned* from these data.
2. But the rules learned *between* regions predict within-region variation with slopes of 0.3-0.66.
   With 100-200 um localisation error (expected slopes 0.47-0.80 for a fully local rule), these
   slopes agree with roughly 40-100% of the between-region effect acting locally. Thus the region-level structure links are not only a label effect of
   region identity.
3. The split depends on scale. Between regions, cell-type mix carries most of the unique signal
   (wiring share 0.19). Inside regions, the input-profile map carries most of it (share 0.78). One
   interpretation: cell-type composition sets the region-level baseline, and graded input
   topography inside a region shapes local firing patterns. This is a hypothesis, not a causal
   result.

## 6. Limitations

* All tests are correlational. The input map is a model of tracer data from other mice (target side
  measured at 100 um, source side interpolated). The cell-type map comes from one brain per atlas,
  with sections about 200 um apart. Neither map has single-cell registration to the recorded units.
* IBL unit positions have registration and localisation error. We modelled its effect on the slope
  by jitter but we did not measure it.
* The planned primary hypotheses failed. Every positive result in sections 4.3-4.4 is exploratory
  and post hoc (addenda 1-3). The rotation p-values are limited to 0.005 by 200 draws.
* The within-region wiring-share interval is wide (0.29-0.99). The unique T slope depends on
  controls. The I map may carry layer or compartment identity that the MERFISH subclass mix does
  not resolve, so "input map" must not be read as "synaptic input causes".
* The 9 features are intrinsic spike measures. Task coding at unit level was not tested (spike times
  were not used).
* The planned rotation nulls used 110 of the 200 planned draws (2 h task limit on a shared host
  with load average about 100 on 24 CPUs). With 110 draws the smallest possible p is 0.009.

## 7. Files

| Path | Content |
|---|---|
| `files/code/` | All scripts. `run_all.sh` gives the order; `get_data.sh` downloads every input into a separate scratch folder. |
| `files/plan/` | Frozen plan, 3 addenda, hash log. |
| `files/results/*.json` | All test statistics (R2, slopes, CIs, null summaries, p-values). |
| `files/results/insertion_offsets.csv` | Per region-insertion mean feature deviations (IBL-derived, CC BY 4.0). |
| `files/results/*.png` | Figures 1-4. |
| `files/data/session_subjects.csv` | IBL session, lab and subject (OpenAlyx, CC BY 4.0). |
| `files/provenance/` | Input hashes and URLs, software versions, hashes of derived files not bundled. |
| `files/EXTERNAL_DATA_NOTICE.md` | Third-party data, licences and attribution. |

**Reproduce.** `bash files/code/get_data.sh /scratch/ds` (or use the campaign store), then
`WS_DATA=/scratch/ds WS_DER=/scratch/der WS_RES=/scratch/res bash files/code/run_all.sh`.
Python 3.12 with numpy, scipy, pandas, pyarrow, scikit-learn, matplotlib (versions in
`files/provenance/software_versions.txt`). The full run took about 6 h on a loaded 24-CPU host.
The Allen-derived voxel maps (about 2 GB) are written only to `WS_DER`.

**Run notes.** The planned rotation nulls (06_main.py primary and mouse_cv) were stopped by the 2 h
tool task limit after 110 of 200 planned draws each. `06b_finalize.py` summarises the 110
checkpointed draws. No other step was shortened. Logs of every run are in `files/logs/`.

## 8. Citations

Builds on sci:sha256:49479722, sci:sha256:f4e4c521, sci:sha256:a4fae2b2, sci:sha256:7fc46a6a,
sci:sha256:36eebd98, sci:sha256:8811fcd1, sci:sha256:48d934f4, sci:sha256:18f77139,
sci:sha256:745e2c94 (campaign); IBL Brain-Wide Map (doi:10.1038/s41586-025-09235-0); IBL
reproducibility study (doi:10.7554/eLife.100840); Knox et al. 2019 (doi:10.1162/netn_a_00066);
Yao et al. 2023 (doi:10.1038/s41586-023-06812-z); Zhang et al. 2023 (doi:10.1038/s41586-023-06808-9);
Wang et al. 2020 (doi:10.1016/j.cell.2020.04.007).
