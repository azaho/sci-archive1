# Voxel-scale tracer projection density does not predict short-latency spike links between mouse visual areas better than distance in two Allen Neuropixels datasets

## Summary

**Question.** Mouse visual areas are connected topographically. An axon from one point in area A goes mostly to some points in area B and not to others. We asked a structure–function question: does the density of axons that one point sends to another point, as predicted from Allen anterograde tracer data, tell which unit pairs in two visual areas have a short-latency directed spike link? We asked whether it does this better than area identity, the distance between the units, firing rate, layer and spike width.

**Approach.**
1. We made a voxel-scale (100 µm) projection model on the Allen cortical flatmap. It uses 289 anterograde tracer injections in visual cortex (wild-type, Emx1, intratelencephalic and Rbp4 lines). The model is kernel regression over injection centroids, as in Knox et al. 2019. A Gaussian kernel of 200 µm gave the best leave-one-experiment-out prediction of held-out tracer maps (mean r of log density = 0.88; 0.63 without position information).
2. For each recorded unit we found its position on the flatmap. For each directed test (source unit i in area A, target unit j in area B), the model gave the predicted density D(i→j) of axons from the position of i at the position of j.
3. We used a shared campaign cache of directed cross-correlogram (CCG) tests between units on different probes in six visual areas (VISp, VISl, VISrl, VISal, VISpm, VISam). A "link" is a sharp CCG peak at +0.5 to +12.5 ms (Poisson p < 1e-5, larger than the mirrored peak). There are two independent datasets:
   - Allen Visual Coding Neuropixels (VC; passive viewing): 3,368,326 tests, 5,921 links, 50 mice.
   - Allen Visual Behavior Neuropixels (VBN; change-detection task): 4,837,658 tests, 33,831 links, 62 sessions, 34 mice.
4. We fitted Poisson log-link models with absorbed fixed effects and mouse-clustered sandwich standard errors. The main ("between") model has area-pair and session fixed effects, a cubic B-spline of 3-D inter-unit distance, and firing-rate, layer and spike-width terms for both units. A stricter ("within") model has session × area-pair and source-unit fixed effects. The effect is the link rate ratio (RR) per 10-fold increase of D.

**Main result.**
- Without a distance control, D predicted links in VC. The raw link rate increased from 1.25 to 3.40 per 1000 tests between the lowest and the highest decile of within-area-pair D. With area-pair fixed effects only, RR = 2.18 per 10-fold D (z = 4.97).
- The 3-D distance between the units removed most of this association. In the main model, RR = 1.22 (95% CI 0.92–1.62) in VC and 0.94 (0.77–1.16) in VBN. The adjusted rate ratios by decile were flat in both datasets (Figure 2).
- Distance alone was a strong predictor in both datasets. Relative to 0.5 mm, the adjusted link rate was 0.43 (VC) and 0.59 (VBN) at 1 mm, and 0.19 (VC) and 0.13 (VBN) at 3 mm (Figure 4).
- In VBN, D had no association at any adjustment level, also without the distance control (area-pair fixed effects only: RR 1.14, z = 0.73).
- The within-session model gave RR = 2.17 (1.11–4.26) in VC, but 0.85 (0.54–1.34) in VBN. This VC result did not replicate.
- Across five variants (strict links, wild-type tracers only, kernels of 100 and 400 µm) the VC estimates were always above 1 (3 of 10 with a CI that excludes 1). The VBN estimates were always below 1 (none with a CI that excludes 1). No pooled VC + VBN estimate differed from 1 (main between model: RR 1.03, 0.87–1.22).
- The tracer direction did not matter. The reverse-direction density D(j→i) did not predict links better than chance in VC. In the VBN within-session model it had the opposite sign (RR 0.60, z = −2.05).

**Conclusion.** At the resolution of the Allen tracer data (injections of about 0.5–1 mm), predicted point-to-point axon density gives no consistent information about which cross-area unit pairs have short-latency spike links, after we control for distance. The positive VC signal is mostly a distance effect. A small remaining VC tendency is present in all variants, but it is absent in VBN, and the two datasets disagree. We cannot tell if this difference comes from behavioral state (passive viewing against a task), from probe placement, or from chance. The VBN data exclude an effect larger than RR 1.16 per 10-fold D in the main model (about 1.04 per standard deviation of within-area-pair log D).

## Figures

- `files/figures/fig1_tracer_model.png`: predicted axon density maps from a VISp and a VISam position, with recorded unit positions and the leave-one-out selection of the kernel width.
- `files/figures/fig2_deciles.png`: adjusted rate ratio (left) and raw link rate (right) by decile of within-area-pair predicted density, for VC and VBN.
- `files/figures/fig3_forest.png`: rate ratio per 10-fold D (95% CI) for all models, sensitivity analyses and the adjustment ladder.
- `files/figures/fig4_distance.png`: adjusted link rate against 3-D inter-unit distance (no tracer term).

## Results tables

All rate ratios are per 10-fold increase of predicted density D(i→j). CI: 95%, clustered by mouse. "Tests" is the number of rows in the case-control sample (see Methods). Full table: `files/results/forest_table.csv` and `files/results/all_models.csv`.

### Main models (kernel 200 µm, 289 tracer experiments, all links)

| Data | Model | RR | 95% CI | z |
|---|---|---|---|---|
| VC | between (area pair + session FE, distance, unit covariates) | 1.22 | 0.92–1.62 | 1.39 |
| VC | within (session × area pair FE, source-unit FE, distance, target covariates) | 2.17 | 1.11–4.26 | 2.26 |
| VBN | between | 0.94 | 0.77–1.16 | −0.57 |
| VBN | within | 0.85 | 0.54–1.34 | −0.69 |

### Adjustment ladder (between-session design)

| Step | VC RR (z) | VBN RR (z) |
|---|---|---|
| area-pair FE only | 2.18 (4.97) | 1.14 (0.73) |
| + session FE | 1.74 (3.78) | 1.10 (0.85) |
| + firing rate, layer, spike width of both units | 1.62 (4.00) | 1.16 (1.38) |
| + distance spline (main model) | 1.22 (1.39) | 0.94 (−0.57) |

### Direction test (forward and reverse density in one model)

| Data | Model | D(i→j) RR (z) | D(j→i) RR (z) |
|---|---|---|---|
| VC | between | 1.21 (1.48) | 1.05 (0.37) |
| VC | within | 2.01 (2.11) | 1.39 (0.69) |
| VBN | between | 0.93 (−0.73) | 1.13 (1.10) |
| VBN | within | 0.93 (−0.29) | 0.60 (−2.05) |

### Sensitivity analyses

RR per 10-fold D, 95% CI, z. Full table: `files/results/forest_table.csv`.

| Variant | VC between | VC within | VBN between | VBN within |
|---|---|---|---|---|
| main (kernel 200 µm, 289 tracers, all links) | 1.22 (0.92–1.62), 1.39 | 2.17 (1.11–4.26), 2.26 | 0.94 (0.77–1.16), −0.57 | 0.85 (0.54–1.34), −0.69 |
| strict links only | 1.24 (0.85–1.80), 1.13 | 2.24 (0.67–7.47), 1.31 | 0.92 (0.70–1.20), −0.63 | 0.72 (0.36–1.47), −0.89 |
| WT/Emx1 tracers only (92) | 1.47 (1.10–1.98), 2.56 | 1.85 (0.92–3.73), 1.74 | 0.96 (0.76–1.22), −0.34 | 0.99 (0.62–1.57), −0.05 |
| kernel 100 µm | 1.19 (0.91–1.54), 1.27 | 1.73 (0.97–3.08), 1.85 | 0.95 (0.81–1.12), −0.59 | 0.78 (0.60–1.03), −1.78 |
| kernel 400 µm | 1.35 (0.97–1.87), 1.77 | 2.63 (1.15–6.01), 2.29 | 0.91 (0.71–1.17), −0.75 | 0.71 (0.43–1.17), −1.34 |

In VC, all 10 estimates are above 1 and 3 of 10 have a CI that excludes 1. In VBN, all 10 estimates are below 1 and none has a CI that excludes 1.

### VC and VBN pooled (inverse-variance, fixed effect)

| Variant | between: pooled RR (95% CI); heterogeneity p | within: pooled RR (95% CI); heterogeneity p |
|---|---|---|
| main | 1.03 (0.87–1.22); 0.15 | 1.14 (0.78–1.67); 0.024 |
| strict links | 1.02 (0.82–1.26); 0.20 | 0.97 (0.53–1.79); 0.11 |
| WT/Emx1 tracers | 1.14 (0.94–1.37); 0.027 | 1.20 (0.82–1.76); 0.14 |
| kernel 100 µm | 1.01 (0.88–1.16); 0.16 | 0.90 (0.71–1.15); 0.015 |
| kernel 400 µm | 1.05 (0.86–1.28); 0.063 | 1.01 (0.66–1.56); 0.008 |

No pooled estimate differs from 1. The two datasets disagree significantly (p < 0.05) in 4 of 10 comparisons. File: `files/results/pooled_vc_vbn.csv`.

### Feedforward and feedback pairs (main model, by Harris et al. 2019 hierarchy)

RR per 10-fold D (95% CI), z. Feedforward: the target area is higher in the hierarchy than the source area.

| Data | Subset | between | within |
|---|---|---|---|
| VC | feedforward (3,901 links) | 1.30 (0.99–1.72), 1.85 | 2.55 (1.06–6.11), 2.09 * |
| VC | feedback (2,020 links) | 0.94 (0.63–1.42), −0.28 | 1.31 (0.58–2.97), 0.64 |
| VBN | feedforward (20,733 links) | 0.88 (0.71–1.09), −1.17 | 0.91 (0.52–1.58), −0.34 |
| VBN | feedback (13,098 links) | 1.37 (1.00–1.87), 1.93 | not computed † |

\* IRLS stopped at the cap of 30 iterations (deviance criterion not met). The estimate is the same as in a first run without the cap (2.546).
† The fit did not finish within the 2-hour job limit (slow convergence of the fixed-effect projections in this subset). We did not run it again.

The feedforward/feedback split does not give a consistent pattern: in VC the feedforward estimates are larger, and in VBN the feedback estimate is larger.

## Interpretation

1. **Distance is the robust structural predictor.** In both datasets, the link rate decreased by a factor of 5–8 between 0.5 mm and 3 mm. This agrees with the general decrease of connection probability with distance. It is the effect that generalized across animals and behavioral conditions.
2. **Tracer topography adds no consistent information.** Predicted density and distance are correlated (r = −0.35 to −0.37 between log D and log distance). When both are in the model, D has no consistent effect. A real but small topographic effect is possible. The data exclude a large one in VBN.
3. **Possible reasons for the null result.** (a) Resolution. Tracer injections cover about 0.5–1 mm of cortex, and the kernel model smooths at about 200 µm. Fine retinotopic matching between single units can be below this resolution. (b) Range. Allen probes were placed at retinotopically matched positions. This decreases the range of D within an area pair (within-area-pair SD of log10 D: 0.31 in VC, 0.24 in VBN; within session × area pair: 0.11 and 0.08). (c) Link definition. A CCG link is not proof of a monosynaptic connection. Shared input with a delay can also make an asymmetric peak. (d) Area labels. VC area labels come from sign maps, so some "VISl" or "VISal" units are outside the CCF area border. The tracer model uses only CCF positions, so this has no effect on D, but the area-pair fixed effects mix positions.

## Limitations

- D is a model prediction from other animals, not a measurement in the recorded animals. The prediction error at single-unit scale is not known. Leave-one-out accuracy describes whole tracer maps, not point-to-point values.
- The tracer data report axon density, not synapse number or synaptic weight. Layer-specific targeting is averaged over cortical depth in the flatmap.
- Eight of 58 VC sessions have no CCF coordinates (value −1000) and are excluded. VBN tests include periods that the Allen data mark as invalid (the shared cache did not remove them).
- We used a case-control sample: all tests with a link and a random 10% of tests without a link, with weight 10. This is a consistent estimator for log-link slopes with rare events, and it loses little precision (links are 0.2–0.7% of tests). One random seed (0) was used.
- Many models were fitted (two datasets, two designs, a direction test, strict links, three tracer/kernel variants, feedforward/feedback subsets). The isolated positive results (VC within; VC WT-tracer between) must be read with this multiplicity in mind. None replicated in VBN.
- CCG tests were computed over whole sessions (stimulus and gray-screen periods together). We did not test state dependence.

## Methods (details)

**Data.** All inputs are from the shared campaign dataset store (read-only). SHA-256 of all 1,068 input files: `files/provenance/input_files_sha256.csv` (all match the SHA256SUMS of the datasets).
- `allen_neuropixels_crossarea_directed_tests_layers/v1_2026-11-02`: directed CCG tests (`tests_vc/*.npz`, `tests_vbn/*.npz`) and unit tables (`units_vc.parquet`, `units_vbn.parquet`). Derived from Allen Visual Coding Neuropixels (Siegle et al. 2021, doi:10.1038/s41586-020-03171-x) and Allen Visual Behavior Neuropixels. The link rule is from that cache (`code/02_tests.py` there): partially hollow Gaussian baseline (σ = 10 ms, hollow fraction 0.6), largest excess in (+0.5, +12.5) ms, Poisson p < 1e-5, and larger than the largest mirrored excess. "Strict" links add p < 1e-6, width ≤ 1.5 ms, onset ≥ 1 ms and zero-lag excess < half of the peak.
- `allen_connectivity_grid100/v2026-10-28` and `v2026-10-30_visual`: Allen Mouse Brain Connectivity Atlas 100 µm projection_density and injection_density grids (Oh et al. 2014, doi:10.1038/nature13186; Harris et al. 2019, doi:10.1038/s41586-019-1716-z).
- `allen_projection_unionize_visual_layers/v1_2026-10-30/all_experiments_service.json`: experiment list (injection structure, transgenic line, product).
- `allen_ccf_streamlines/v1_2026-10-30`: ccf_streamlines closest-surface lookup and dorsal flatmap lookup (Wang et al. 2020, doi:10.1016/j.cell.2020.04.007).

**Flatmap.** Each point (µm, CCF 2017) goes to its 10 µm voxel, then to the closest isocortex surface voxel (streamline lookup), then to its dorsal flatmap pixel (1360 × 1360). The lookup covers the left hemisphere, so right-hemisphere points are mirrored first. Points outside isocortex use the nearest isocortex voxel within 60 µm. Mapped: 14,454/16,778 VC units and 18,770/19,568 VBN units.

**Tracer model.** We used experiments with the primary injection structure in VISp, VISl, VISal, VISrl, VISa, VISam, VISpm, VISli, VISpor or VISpl, products 5/35/36, and lines in the set "main" (wild type, Emx1-IRES-Cre, Rbp4-Cre_KL100 and the intratelencephalic lines of Harris et al. 2019; 289 experiments) or "wt" (wild type and Emx1 only; 92 experiments). List: `files/results/experiments.csv`. Grids were folded to the right hemisphere. Voxels with injection signal were masked by column. Projection density was averaged over cortical depth in 100 µm flatmap bins, normalized to unit sum, and smoothed (Gaussian, 1 bin). Prediction for a source position s: D(s, t) = Σ_e w_e(s) F_e(t) / Σ_e w_e(s), with w_e = exp(−|s − c_e|² / 2σ²), c_e = the injection-density-weighted centroid on the flatmap. Experiments with a masked bin at t were left out of that sum. σ was chosen by leave-one-experiment-out correlation of log maps in the region of the recorded units (`files/results/model_cv.csv`).

**Statistics.** Poisson log-link model y ~ exp(a_k + b_u + X β), fitted by IRLS with both fixed effects absorbed by weighted alternating projections (the ppmlhdfe method). Standard errors are cluster-robust by mouse. Our fitter gave the same estimate as statsmodels GLM with explicit dummy variables (RR 1.22047 in both, z 1.3876 vs 1.3874; `files/results/check_fe_vs_statsmodels.txt`). Distance: cubic B-spline of log 3-D CCF distance with interior knots at quintiles. Unit covariates: centered log spike count and its square, fast-spiking flag (waveform < 0.4 ms), layer (2/3, 4, 5, 6). Fixed-effect levels without any link carry no information and were dropped (so VC uses 50 mice and VBN 34 mice).

## Reproduction

Code: `files/code` (MIT). Run `files/code/run_all.sh` from `files/code` with Python 3.12 and the packages in `files/provenance/python_environment.txt`. Set `DATASETS` to the shared dataset root (default `/mnt/dell-data/shared_datasets`) and `SCRATCH` to a local folder for large intermediates (about 2 GB). The full run takes about 4–5 h on one CPU core with less than 3 GB memory. Most of the time is in `04_stats.py` on the VBN data.

| Script | Purpose |
|---|---|
| `common.py` | paths and constants |
| `01_flatmap.py` | flatmap coordinates of units and 100 µm grid voxels |
| `02_model.py` | tracer flat maps, injection centroids, leave-one-out kernel width selection |
| `03_pairs.py <set> <sigma>` | D(i→j), D(j→i) and distances for every directed test |
| `fe.py` | Poisson model with two absorbed fixed effects and clustered sandwich SEs |
| `04_stats.py <set> <sigma> [outcome] [core]` | main models and decile analysis |
| `04b_extra.py` | adjustment ladder, distance curve, feedforward/feedback subsets |
| `05_figures.py`, `07_tables.py` | figures and tables |
| `06_provenance.py` | SHA-256 of all input files |
| `check_fe_vs_statsmodels.py` | validation of `fe.py` |

Run notes. The host job limit is 2 hours. Our first run of `run_stats.sh` stopped after the main and strict configurations. We ran the three other sensitivity configurations again with the two primary models only (`core` argument). We ran `04b_extra.py` again per dataset with an IRLS cap of 30 iterations and a result file that is written after each model. The VBN feedback within-session model did not finish in that time. All numbers in this README come from the result files in `files/results`.

The CCG arrays and tracer grids are not in this bundle (Allen Institute Terms of Use; size). They can be made again from the Allen sources with the scripts in the shared caches named above.

## Provenance

- Campaign 11_07_2026; job sci-1107-syam1-neural-structure-and-computation-7d574831f897; topic neural-structure-and-computation; machine syam1; model claude-opus-5-5 (Claude Code); account claude-olen. The signing key is a campaign-machine key, not a claim of personal authorship.
- Data: Allen Institute for Brain Science. Allen Brain Map data are used under the Allen Institute Terms of Use (https://alleninstitute.org/terms-of-use/). This publication does not include Allen raw data.
- Related shared-cache studies (cited in the dataset READMEs; not in this campaign folder): a study of inter-areal spike-coupling lag against axon path length, and a study of feedforward/feedback spike links against tracer layer rules. No publication in this campaign folder existed when this work started.
