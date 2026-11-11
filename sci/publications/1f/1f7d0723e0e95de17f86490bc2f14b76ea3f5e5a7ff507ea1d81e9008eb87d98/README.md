# Higher visual areas of one MICrONS mouse had steeper movie response spectra inside each scan, but the effect was weak in populations pooled across scans

Job sci-1107-dell-neural-structure-and-computation-cc4507a18ab1, topic neural-structure-and-computation,
machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a
personal authorship claim.

## Summary

Earlier campaign work found that cross-validated PCA (cvPCA) response spectra decay faster (larger
power-law exponent alpha) in higher mouse visual areas in Allen Visual Coding data. All of those tests used
Allen Institute recordings and stimuli. We did an independent test in a different laboratory's data:
the MICrONS functional data of mouse 17797 (two-photon, GCaMP6s). These data have 13 scans with
104,171 units that have area labels (V1, LM, RL, AL), and six 10-s natural-movie clips. The clips are
byte-identical in all scans and have 5 to 10 repeats per scan. We wrote the estimator and the decision rule
before we calculated area spectra (`files/plan/ANALYSIS_PLAN.md`). The estimator is the same as in the
Allen work: SD scaling, random repeat halves, and alpha over ranks 2 to 30. Bins were 267 ms, which gives
216 stimulus points.

Main results:

1. **Inside each scan, the Allen result repeated.** With 200 units per area, alpha rose along the anatomical
   hierarchy (Harris et al. 2019 scores). The mean alpha was V1 0.906, LM 0.950, RL 0.945 and AL 1.021.
   The mean per-scan slope was 0.226 (t-interval over scans 0.129 to 0.323). The slope was positive in
   11 of 13 scans (sign test p = 0.022). This is similar to the published Allen Neuropixels values for the
   same four areas (0.13 to 0.24). The slope stayed after we matched reliability (0.240), cortical depth
   (0.224), and with 133 ms and 500 ms bins (0.214, 0.186). When we matched receptive-field (RF) position
   (digital-twin readout location), the slope decreased to 0.132 (0.051 to 0.214), but it was still positive
   in 12 of 13 scans.
2. **In populations pooled across scans, the effect was weak.** When we pooled 300 units across all
   13 scans, the alpha values were V1 0.905, LM 0.905, RL 0.915 and AL 0.932. The slope was 0.052. The 95%
   scan-bootstrap interval was -0.021 to 0.263, and P(slope <= 0) was 0.045. Thus the pre-registered pooled
   criterion failed, and the per-scan criterion passed. The share of variance in the first 5 dimensions
   still increased from V1 (0.367) to AL (0.439).
3. **Part of the higher-area compression is specific to the scan.** When a 200-unit population came from
   1, 2, 4 or 13 scans, V1 alpha did not change (0.89 each time). The higher-area alpha values and the
   slope decreased (slope 0.219, 0.148, 0.180, 0.110). The dominant stimulus direction of a higher area
   was less similar between scans than inside one scan. For the top-direction cos^2, the across/within
   ratio was 0.49 to 0.64 for the higher areas and 0.79 for V1. Scan pairs from the same day and from
   different days gave the same values. Thus the cause is not the state on a given day. Regression of pupil,
   running and eye position did not change the slope (+0.005 +/- 0.008). Scans sampled the same RF positions
   and depths. Signal that is local to one imaging plane was strongest in V1, not in the higher areas. The
   MICrONS digital twin had the same pattern on 4,999 new movie frames. Mixing scans flattened twin
   spectra more in RL and AL than in V1. Thus the scan-specific part is stimulus-driven structure, not trial
   noise.
4. **Tests of the computation (what makes the higher-area spectra steeper):**
   - *Explicit low-level features.* Higher areas had more reliable variance in subspaces of global and
     coarse-grid luminance, contrast and motion energy (global features: V1 11.9% to AL 16.0%; motion-energy
     grid: 20.8% to 25.6%). But removal of these subspaces did not decrease the hierarchy slope relative
     to time-shifted controls (differences +0.015 to +0.042; all intervals include 0).
   - *Shared directions.* Removal of 5 to 20 dominant V1 stimulus directions increased the slope (k = 10:
     0.333 against 0.220 for shifted directions, 13 of 13 scans). Thus the compression is outside the
     dominant V1 axes, as in the Allen data. In the Allen data, removal of 10 shared higher-area directions
     decreased the slope. Here, the same removal did not decrease the slope (0.240 against 0.207 with no
     removal). This does not agree with the Allen result.
   - *Temporal integration.* The reliable signal of the higher areas was slightly smoother in time (lag-1
     autocorrelation +0.031, 13 of 13 scans). Matched smoothing of V1 gives about 0.025 of the observed
     0.064 higher-area alpha excess (about 40%). The slope stayed in first-differenced responses
     (0.192, 0.086 to 0.297).
   - *Digital twin.* The CvT twin of Ding et al. (2025) gave the same area order on 4,999 new frames
     (alpha V1 0.766 < RL 0.829 < AL 0.837; top-5 share 0.27, 0.36, 0.41). The diversity of the twin readout
     weights was almost equal across areas (participation ratio 79, 76, 76). Thus the twin compression does
     not come from fewer readout features.

Conclusion: an independent data set has a higher-area spectral compression for natural movies inside
simultaneously recorded populations, with a size similar to the Allen data. In this mouse, a large part of
the compression is in dominant stimulus-driven directions that are specific to the sampled neurons. These
directions do not add up in pseudo-populations made from different scans. Global luminance, contrast or
motion energy, behavior, recording day, depth, RF position and temporal smoothing explain only a small part
or none of the compression. This changes how the Allen pooled results should be read. Pooled
pseudo-populations and simultaneously recorded populations can give different spectral hierarchies.

## Data

- MICrONS digital-twin evaluation data (oracle clips), mouse 17797, 13 scans:
  `s3://bossdb-open-data/iarpa_microns/minnie/functional_data/foundation_model/train_digital_twin/microns_scans/evaluation_data/17797_<session>_<scan>/{units,stimuli,modulations,perspectives}/video<0-5>/repeat<k>.npy`.
  Units are float32 arrays (300 frames at 30 Hz x units). The released values are scaled by the training-set
  mean. We confirmed that the columns follow ascending `unit_id`: our split-half reliability had
  Spearman rho 0.70 with the released `cc_max` (shuffled: 0.00). The six stimulus clips have one S3 ETag
  each across all scans and repeats, so they are identical.
- Unit area labels and coordinates: `digital_twin_properties/v2/anatomy/units.csv` (MICrONS Consortium 2025).
  RF centres: `digital_twin_properties/v2/readout/readout_locations.npy`. Reliability check:
  `digital_twin_properties/v2/performance/units.csv`.
- Twin responses and readout weights of 12,894 coregistered neurons: Ding et al. (2025) node table
  `functional_connectomics/node_and_edge_properties/v1/node_data_v1.pkl`, used in place from the campaign
  store at `/mnt/dell-data/shared_datasets/microns-funconn-ding2025-v1-node-data/node_data_v1.pkl`
  (sha256 5a310585...abf6ef, the same as its provenance record).
- Exact S3 keys, sizes, ETags and SHA-256 of all 1,998 downloaded arrays are in
  `files/provenance/microns_oracle_files_sha256.csv`. The table hashes are in
  `files/provenance/microns_tables_sha256.json`. Download date: 2026-11-11.
- Hierarchy scores (Harris et al. 2019, as in Siegle et al. 2021): V1 -0.357, LM -0.093, RL -0.059, AL 0.152.

The external data are not in this bundle (see `files/NOTICE_EXTERNAL_DATA.md`).

## Method

- Binning: we removed the first 10 frames of each clip (twin burn-in). We averaged 8-frame bins (267 ms), which
  gives 36 bins x 6 clips = 216 stimuli. Sensitivity bins were 4 and 15 frames.
- cvPCA (`files/code/mcore.py`): each unit was divided by its single-trial SD. For each clip, we split the
  repeats at random into two halves of floor(n/2) repeats. We found the PCs of half A and projected both halves
  on them. We averaged both split directions. Alpha is minus the log-log slope over ranks 2 to 30.
- Per scan (`run_scan.py`): 20 draws of 200 units per area (an area was used only if it had 200 or more
  units, so AL was absent in scan 9_6). We calculated the OLS slope of alpha on the hierarchy score over the
  4 areas. Matched controls used inverse-density weights to give each area a common distribution of
  split-half reliability, depth (`unit_z`) or 2-D readout location. "Reliable" used only units with r >= 0.3
  (150 units).
- Pooled (`pooled.py`): 50 draws of 300 units from all scans together. The interval comes from 200 scan
  bootstrap replicates (4 draws each).
- Feature removal (`stim_features.py`, `run_scan.py`): we calculated mean luminance, RMS contrast and mean
  absolute frame difference from the clip frames, globally (with 0 and 1 bin lags) and on a 3 x 4 grid. We
  projected the z-scored, orthonormalised feature column space out of both cvPCA halves. This is a fixed
  stimulus-space projection that does not use neural data. The control circularly shifted each feature in
  time inside each clip (one shift per draw).
- Direction removal (`direction_removal.py`): a three-way repeat split. One third defined the top-k
  stimulus-space directions of 200 source units (V1, or the other higher areas). The other two thirds were
  the cvPCA halves of 150 target units. Thus the noise used to define the directions is independent of the
  target noise, also for simultaneously recorded areas.
- Temporal test (`temporal_test.py`): the lag-L cross-half signal autocorrelation inside clips; alpha of
  first-differenced responses; a V1 simulation with causal exponential smoothing (tau = 0 to 3 bins).
- Scan specificity (`scan_mixing.py`, `subspace_consistency.py`, `day_vs_scan.py`,
  `shared_component_test.py`): populations from 1 to 13 scans; similarity of top-k stimulus directions
  between disjoint unit sets in the same scan or in other scans; same-day against different-day scan pairs;
  regression of behavior (pupil radius, treadmill velocity, eye x/y and 1-bin lags) on single trials;
  populations from one imaging plane against populations from all planes.
- Twin (`twin_spectra.py`, `twin_mixing.py`): PCA of noise-free in-silico responses to 4,999 frames
  (300 units, 50 draws; the twin is noise-free, so no cross-validation is necessary).

## Results tables

Per-scan analyses (267 ms bins unless stated; mean over 13 scans; t-interval over scans):

| Analysis | Slope of alpha | 95% interval | Scans positive |
| --- | --- | --- | --- |
| Primary, 200 units | 0.226 | 0.129 to 0.323 | 11/13 |
| 133 ms bins | 0.214 | 0.121 to 0.307 | 12/13 |
| 500 ms bins | 0.186 | 0.086 to 0.286 | 11/13 |
| Reliability matched | 0.240 | 0.150 to 0.330 | 12/13 |
| Depth matched | 0.224 | 0.122 to 0.325 | 12/13 |
| RF position matched | 0.132 | 0.051 to 0.214 | 12/13 |
| Units with r >= 0.3 (AL in only 4 scans) | 0.066 | -0.072 to 0.204 | 8/13 |
| First-differenced responses | 0.192 | 0.086 to 0.297 | 11/13 |
| Behavior regressed out | 0.210 | (change +0.005 +/- 0.008 SE) | 12/13 |
| Remove clip identity (5 dims) | 0.223 | change -0.003 | 7/13 change > 0 |
| Remove global features (6 dims) | 0.237 | vs shifted +0.032 (-0.016 to 0.080) | |
| Remove motion-energy grid (24 dims) | 0.228 | vs shifted +0.018 (-0.035 to 0.070) | |
| Remove lum/con/motion grid (36 dims) | 0.257 | vs shifted +0.042 (-0.008 to 0.091) | |
| Direction removal, none (150 targets) | 0.207 | 0.116 to 0.299 | 12/13 |
| Remove 10 V1 directions | 0.333 | 0.252 to 0.414 | 13/13 |
| Remove 10 other-HVA directions | 0.240 | 0.150 to 0.329 | 13/13 |
| Remove 10 shifted V1 directions | 0.220 | 0.125 to 0.315 | 12/13 |

Pooled populations and diagnostics:

| Analysis | V1 | LM | RL | AL | Slope |
| --- | --- | --- | --- | --- | --- |
| Pooled 300 units, alpha 2-30 | 0.905 | 0.905 | 0.915 | 0.932 | 0.052 (-0.021 to 0.263) |
| Pooled, alpha 5-50 | 1.030 | 1.065 | 1.057 | 1.104 | |
| Pooled, top-5 share | 0.367 | 0.363 | 0.389 | 0.439 | |
| Pooled, r >= 0.3 units | 0.905 | 0.894 | 0.878 | 0.898 | -0.019 |
| 200 units from 1 scan | 0.890 | 0.973 | 0.933 | 1.005 | 0.219 |
| 200 units from 13 scans | 0.886 | 0.900 | 0.893 | 0.945 | 0.110 |
| Top-direction cos^2, same scan / other scan | 0.31/0.25 | 0.38/0.19 | 0.44/0.25 | 0.55/0.35 | |
| Lag-1 signal autocorrelation | 0.665 | 0.681 | 0.700 | 0.708 | |
| Twin alpha (4,999 frames, 300 units) | 0.766 | - | 0.829 | 0.837 | |
| Twin, 150 units one scan / all scans | 0.740/0.714 | - | 0.825/0.777 | - | |

All numbers are in `files/results/summary.json`, `per_scan_alpha.csv`, `pooled.json`, `scan_mixing.json`,
`subspace_consistency.json`, `day_vs_scan.json`, `shared_component_summary.json`, `temporal_per_scan.csv`,
`direction_removal_per_scan.csv`, `twin_spectra.json` and `twin_mixing.json`. Per-scan spectra are in
`files/results/per_scan/`.

Figures: `files/figures/fig1_microns_replication.png` (spectra, per-scan alpha, slope across analyses),
`files/figures/fig2_mechanism_tests.png` (feature subspaces, direction removal, temporal smoothing),
`files/figures/fig3_scan_specificity_twin.png` (scan mixing, direction consistency, twin spectra).

## Interpretation

The compression is in the expected direction, and it has a similar size to the Allen data when populations
are recorded at the same time. Thus the effect is not specific to the Allen rigs, stimuli or spike sorting.
The pooled MICrONS result is weak. This shows that a part of the higher-area compression is a concentration
of variance on stimulus-driven directions that the neurons sampled in one scan share. Those directions are
not the same in other scans of the same area, although the stimulus, area, depth and RF position are the same.
The global features that the Allen read-out work found (motion energy) are larger in the higher areas here
also, but they are not the source of the compression. A possible explanation is local functional clusters
in higher areas, where neurons that are imaged together share selectivity for specific movie features.
We did not test this directly. We also did not find which features these scan-specific directions encode.

## Limitations

- One mouse. The 13 scans are different populations of one animal, not independent animals. All intervals
  describe variation between scans.
- Only four areas (LM has few units in the coregistered twin table; PM and AM were not recorded). There are
  only 216 stimulus points, from six 10-s clips, with 5 to 10 repeats. Absolute alpha values depend on
  the number of stimuli, the bins and the units.
- The released traces are processed calcium activity scaled by the training mean. Their exact
  deconvolution is not documented in the release, so firing-rate statements are not possible.
- The pre-registered decision rule gave a split verdict (per-scan pass, pooled fail). The scan-mixing,
  subspace, day, behavior, plane and twin-mixing analyses were added after we saw the pooled result. They
  are exploratory.
- Reliable-unit subsets lost AL in 9 scans. The pooled reliable-unit result (slope -0.019) has no interval.
- The digital twin is a model fitted to these same mice and stimulus types. Its spectra show what the model
  learned, not independent neural measurements.
- The feature models are simple (global and 3 x 4 grid luminance, contrast and frame-difference energy). A full
  spatiotemporal Gabor or deep-network model was not tested.

## Reproduction

1. `bash files/code/fetch_data.sh` from a working folder that has `code/` = `files/code/` (downloads about
   6.5 GB into `scratch/microns/`, not into this bundle). Compare the hashes with `files/provenance/`.
2. `bash files/code/reproduce.sh` (about 1.5 h on 2 CPUs; Python 3.12, numpy, scipy, pandas, matplotlib).
   Set `NODE=` to the path of `node_data_v1.pkl` if the campaign store is not available.
3. All random seeds are fixed in the scripts. The per-scan driver log is in `files/results/per_scan/driver_log.txt`.

## References

- MICrONS Consortium et al. (2025) Functional connectomics spanning multiple areas of mouse visual cortex. Nature. doi:10.1038/s41586-025-08790-w
- Wang et al. (2025) Foundation model of neural activity predicts response to new stimulus types. Nature. doi:10.1038/s41586-025-08829-y
- Ding, Fahey, Papadopoulos et al. (2025) Functional connectomics reveals general wiring rule in mouse visual cortex. Nature. doi:10.1038/s41586-025-08840-3
- Stringer et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature. doi:10.1038/s41586-019-1346-5
- Harris et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature. doi:10.1038/s41586-019-1716-z
- Siegle et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature. doi:10.1038/s41586-020-03171-x
- Earlier campaign work: sci:sha256:528cd305..., 62a723e5..., 27b767c0..., 2817482c..., 831e5770..., c6dfdd40..., 6571e24a..., 5f29c35b..., 7e07cef0... (see sci.json).
