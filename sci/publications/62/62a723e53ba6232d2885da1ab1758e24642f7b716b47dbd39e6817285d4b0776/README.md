# Steeper response spectra in higher mouse visual areas occur for four stimulus sets and are not explained by classical receptive-field properties

## Summary

A source study (sci:sha256:528cd305...) found that the cross-validated PCA (cvPCA) spectrum of natural-image
responses decays faster in higher areas of the anatomical mouse visual hierarchy. It named two open
problems: the result was shown for one stimulus set only, and receptive-field (RF) size and position were not
controlled. We tested both problems in the same 32 Allen Visual Coding Neuropixels mice (11,559 quality units
in LGd, LP and six cortical areas). We also built an image-computable "model twin" for each unit that has a
significant RF.

Main results:

1. **The trend generalizes across stimulus sets.** The hierarchy slope of the decay exponent alpha (ranks
   2-30, 300-unit pooled populations) was positive for natural scenes (0.27; 95% half-sample interval 0.19 to
   0.34), static gratings (0.91; 0.78 to 1.04), natural movie one (0.45; 0.36 to 0.54) and natural movie three
   (0.35; 0.23 to 0.47). It was also positive inside the six cortical areas for all four sets (0.19 to 0.69).
   In every valid half-sample of the mice (199 or 200 of 200), every slope was positive. The area order of alpha agreed between
   stimulus sets (Spearman 0.83 to 0.90).
2. **RF matching did not reduce the slope.** We matched RF area, RF azimuth and RF elevation across the six
   cortical areas (99 units per area). The natural-scene slope was 0.21 with matching and 0.23 without
   matching (difference -0.02; interval -0.32 to 0.29). The other three stimulus sets gave the same result
   (differences -0.03 to -0.005). The matching test has low power: its intervals are wide.
3. **RF model twins explain only a part of the trend.** Each twin had the RF centre, RF size, preferred
   spatial frequency, preferred orientation and simple/complex class of its real unit. On the same 118
   images and unit sets, the twins gave a slope of 0.09 to 0.11 with equal unit weights, against 0.27 in the
   data (8 structures). In cortex the twins gave 0.03 to 0.07 against 0.25. The data slope was larger than the
   twin slope (difference 0.18, interval 0.03 to 0.34, for envelope scale c = 0.5). When we also gave each
   twin the measured reliability of its real unit, the twins reached 49% to 69% of the data slope, and the
   remaining difference was not significant. Unit weights alone (with RF properties permuted between areas)
   gave almost no slope (0.04).
4. **Exploratory: phase invariance carries the grating trend.** The share of reliable grating variance that
   does not depend on spatial phase increased along the hierarchy (LGd 0.48, VISp 0.79, VISam 0.92;
   cortical slope 0.15, interval 0.10 to 0.19). The phase-averaged responses had a steeper decay in higher
   cortical areas (slope 0.57, 0.39 to 0.76). The phase-dependent part had no cortical trend (-0.01,
   -0.23 to 0.21). Across areas, the phase-invariant share went with the natural-scene alpha (Spearman 0.86;
   0.83 in cortex).

Conclusion: the faster spectral decay in higher areas is a general property of these areas across natural
images, gratings and natural movies. Classical RF size, RF position, spatial-frequency preference and
simple/complex type do not explain most of it. The grating data point to increased invariance (pooling over
spatial phase) as one candidate mechanism. All tests are correlational and use 6 to 8 areas.

## Question and motivation

Stringer et al. (2019) found that mouse V1 responses to natural images have a power-law spectrum with alpha
near 1. The source study found that alpha increases from LGd to VISp to higher areas, and that this survives
reliability matching, layer strata and Cre-line strata. Two simple explanations remained:

- **Stimulus specificity.** The trend could be a property of the 118 natural images (for example, of their
  spatial power spectrum) and not of the areas.
- **RF size and position.** Higher areas have larger RFs. A larger RF pools more of the image, which makes
  responses smoother across images. RF positions also differ between areas, and part of the screen is outside
  the image.

We asked: (1) Does the trend occur for other stimulus sets? (2) Does it survive RF matching? (3) Can a model
with the measured classical RF properties of each unit reproduce it? We wrote the analysis plan with fixed
decision rules before we computed any new spectrum (`files/provenance/analysis_plan_2026-11-09.md`).

## Data

- Allen Visual Coding Neuropixels, all 32 `brain_observatory_1.1` sessions (one mouse per session). We
  streamed the spike times from the 32 NWB files with HTTP range reads. The ETags and sizes are the same as in
  the source study (`files/provenance/vcn_nwb_etags.tsv`).
- Units: Allen quality filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9) in LGd,
  LP, VISp, VISl, VISrl, VISal, VISpm and VISam. 11,559 units (950 to 2,230 per structure), as in the source.
- Stimulus sets (all from the same sessions):
  - natural scenes (ns): 118 images, 50 repeats, spike count 0-250 ms after onset;
  - static gratings (sg): 120 conditions (6 orientations x 5 spatial frequencies x 4 phases), 45 repeats,
    0-250 ms;
  - natural movie one (nm1): 30 s cut into 120 bins of 250 ms, 20 repeats;
  - natural movie three (nm3): 120 s cut into 480 bins of 250 ms, 10 repeats.
- RF metrics: `brain_observatory_1.1_analysis_metrics.csv` (shared campaign dataset). RF-defined units have an
  RF permutation p < 0.01 and the RF centre on the screen: 145 (LGd), 166 (LP), 1,386 (VISp), 347 (VISl),
  295 (VISrl), 405 (VISal), 286 (VISpm) and 537 (VISam) units.
  **Note:** in this CSV the column `p_value_rf` contains booleans and the column `on_screen_rf` contains
  numbers from 0 to 1 with three decimals. The two labels are swapped. We used `on_screen_rf` as the
  p-value and `p_value_rf` as the on-screen flag (`files/provenance/template_and_metrics_checks.txt`).
- The 118 natural-scene images: `natural_scenes_image_stack` from one Visual Coding two-photon NWB file
  (experiment 500964514). Both Brain Observatory datasets use the same images.
- Hierarchy scores (Harris et al. 2019, as used by Siegle et al. 2021): LGd -0.515, VISp -0.357,
  VISl -0.093, VISrl -0.059, LP 0.105, VISal 0.152, VISpm 0.327, VISam 0.441.

The Allen files and all record-level derivatives (spike counts, per-unit tables, images) are not in this
bundle. See `files/NOTICE_EXTERNAL_DATA.md`.

## Methods

**Estimator (same as the source).** We scaled each unit by its single-trial SD. For each condition we split the
repeats at random into two halves. We found the PCs of half A and projected both halves on them. The
cross-covariance of the projections gives the reliable variance per dimension. We used both split directions
and 4 splits. alpha is minus the OLS slope of log variance on log rank over ranks 2 to 30. The hierarchy slope
is the OLS slope of alpha on the hierarchy score over areas.

**P2, stimulus generality.** For each stimulus set and structure: 50 random draws of 300 units from all mice
pooled.

**P1, RF matching.** Cortex only, RF-defined units. We made 27 cells: RF area (<= 500, 600-900, >= 1000 deg2)
x azimuth terciles x elevation terciles. In each cell we took the minimum count over the six areas, and drew
that many units per area. This gave 99 units per area. The comparison used unmatched draws of the same size
from the same RF-defined units. Balance after matching: mean RF area 955 to 1,078 deg2 in all areas (unmatched:
560 in VISp to 1,003); mean azimuth and elevation within 3.5 degrees between areas (`files/results/rf_balance.csv`).

**Within-area RF split (secondary).** In each cortical area we split RF-defined units at the median RF area
and compared 120-unit populations of the two halves. We also fitted alpha ~ hierarchy + log(RF area) over
area x RF-area-tercile cells (60 units per cell).

**Model twins.** Each RF-defined unit got one model unit with its own RF centre, RF area, preferred static
grating spatial frequency and orientation, and class (simple if F1/F0 of drifting gratings > 1, else
complex). A simple twin is a half-rectified Gabor filter. A complex twin is a Gabor energy unit. The Gaussian
envelope SD is c x sqrt(RF area / pi). The Allen RF area comes from 20-degree Gabor patches on a 10-degree
grid, so it over-states the true RF size. A value of c near 0.3 to 0.4 gives RF diameters close to published
mouse V1 values. We used c = 0.5 and 0.7 as generous values and c = 0.3 in a sweep. Geometry: the image is
centred on the screen at azimuth 50 and elevation 10 in RF-metric coordinates, and spans 73.4 x 57.4 degrees
(0.0625 degree per pixel). Outside the image the screen is grey. Sweeps used a 1.3 x larger image and a
left-right flip. We computed noise-free PCA spectra of the twin populations for the same unit draws as the data
(140 units per structure; 145 and 166 RF units are available in LGd and LP). Variants: equal weights;
reliability weights (each twin has the cross-validated signal SD of its real unit, as in the data
normalization); weights only (RF parameters permuted between all RF-defined units).

**Phase analysis (exploratory).** We split the static-grating responses into the phase-averaged part (30
orientation x spatial-frequency conditions) and the phase-dependent part (each response minus its phase
average). One repeat split is shared by all conditions, so the two halves stay independent. The
phase-invariant share is the cross-validated variance of the phase-averaged part divided by the total.

**Uncertainty.** The plan specified a session (mouse) bootstrap. We found that the bootstrap inflates alpha:
a mouse that is drawn twice puts identical units twice into one population, and identical units add no
dimensions. The mean inflation was 0.01 to 0.07 for 300-unit populations, but 0.04 to 0.29 for the 99-unit
RF-matched populations, and it differed between areas. We therefore report intervals from **half-sampling**:
200 draws of 16 of the 32 mice without replacement (the same draw for all areas). For a smooth statistic the
variance over half-samples approximates the variance of the full-sample statistic (delete-d jackknife with
d = n/2). The interval is the point estimate +/- 1.96 SD over half-samples. In half-samples, the RF-matched
populations had only 30 to 57 units per area (median 38), so those intervals are conservative. Only 137 of
200 half-samples had at least 30 matched units per area. The pre-planned bootstrap results are also in
`files/results/` (`boot.csv`, `rf_match.csv`, `summary_*.csv`) and agree in sign.

## Results

### Figure 1. The trend occurs for four stimulus sets

`files/figures/fig1_stimulus_generality.png`: (a) natural-scene spectra; (b) alpha against hierarchy for the four
stimulus sets (bars: +/- 1.96 half-sample SD); (c) hierarchy slopes with 95% half-sample intervals.

| Stimulus set | LGd | VISp | VISl | VISrl | LP | VISal | VISpm | VISam | Slope, 8 str. | Slope, cortex |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Natural scenes | 0.67 | 0.82 | 0.79 | 0.90 | 0.90 | 0.90 | 0.94 | 0.96 | 0.27 (0.19, 0.34) | 0.19 (0.10, 0.29) |
| Static gratings | 0.93 | 1.40 | 1.64 | 1.64 | 1.40 | 1.74 | 1.87 | 1.99 | 0.91 (0.78, 1.04) | 0.69 (0.53, 0.86) |
| Natural movie one | 0.71 | 1.04 | 1.05 | 1.11 | 0.92 | 1.10 | 1.27 | 1.27 | 0.45 (0.36, 0.54) | 0.32 (0.21, 0.42) |
| Natural movie three | 0.49 | 0.76 | 0.74 | 0.85 | 0.69 | 0.88 | 0.87 | 0.93 | 0.35 (0.23, 0.47) | 0.21 (0.12, 0.30) |

- The natural-scene values agree with the source (alpha 0.67 LGd, 0.81 VISp, 0.96 VISam; slope 0.27).
- Spearman rho of alpha with hierarchy: 0.95, 0.83, 0.79 and 0.81 (8 structures); 0.89 to 0.94 in cortex.
- LP was below the cortical line for gratings and movies (for example sg: LP 1.40, VISal 1.74). Thus for these
  sets the 8-structure trend combines a thalamus-to-cortex step and the cortical trend.
- The top-5 fraction of reliable variance also increased with hierarchy for every set (8-structure slopes 0.10
  to 0.31; planned-bootstrap intervals exclude 0; `summary_stimuli.csv`).
- Fit range: ranks 2-20 and 5-50 gave positive slopes for all sets. For ranks 1-10 in cortex, natural scenes
  gave no trend (slope -0.01, as in the source), but gratings (0.46), movie one (0.22) and movie three (0.14)
  did. Thus the source's "no trend in the first 10 ranks" applies to natural scenes only.

### Figure 2. RF matching does not remove the trend

`files/figures/fig2_rf_controls.png`: (a) RF-area balance; (b) natural-scene alpha in RF-defined units, matched and
unmatched (bars: +/- 1.96 half-sample SD, from smaller half-sample populations); (c) cortical slopes with 95%
half-sample intervals; (d) within-area difference of alpha between the larger-RF and smaller-RF halves.

| Stimulus set | Unmatched slope | RF-matched slope | Matched minus unmatched |
| --- | --- | --- | --- |
| Natural scenes | 0.23 (-0.01, 0.47) | 0.21 (-0.04, 0.46) | -0.02 (-0.32, 0.29) |
| Static gratings | 0.58 (0.25, 0.91) | 0.56 (0.24, 0.88) | -0.02 (-0.44, 0.40) |
| Natural movie one | 0.36 (0.12, 0.60) | 0.33 (0.09, 0.58) | -0.03 (-0.35, 0.30) |
| Natural movie three | 0.26 (0.05, 0.48) | 0.26 (0.05, 0.47) | -0.01 (-0.28, 0.27) |

- Pre-registered decision rule: RF properties "explain" the trend if the matched interval includes 0 **and**
  the point estimate falls by more than half; the trend "survives" if the matched interval excludes 0. The
  point estimate fell by 2% to 8% only, so RF properties do not "explain" the trend in any set. The trend
  "survives" for gratings and both movies. For natural scenes the half-sample interval includes 0 (it was
  0.03 to 0.41 with the planned bootstrap, which has an upward bias here), so the natural-scene result is
  inconclusive by the strict rule.
- Inside each cortical area, units with larger RFs (about 3 times the RF area) had steeper spectra: +0.09 for
  natural scenes (all 6 areas positive), +0.17 gratings, +0.13 movie one, +0.06 movie three. Thus RF size
  does change alpha. But the median RF-area ratio between VISp and higher cortical areas is only 1.4 to 1.6, which predicts a
  change of about +0.04 by this within-area relation, against an observed VISp-to-VISam change of +0.14. In
  the cell regression, the hierarchy coefficient stayed at 0.20 (natural scenes) with log RF area in the model
  (RF coefficient 0.04 per log unit). This regression has no interval.

### Figure 3. RF model twins reproduce a minority of the trend

`files/figures/fig3_model_twins.png`: (a, b) alpha of data and twins against hierarchy for c = 0.5 and 0.7;
(c) slopes with 95% half-sample intervals.

| Population (140 RF units per structure) | Slope, 8 structures | Fraction of data slope | Slope, cortex |
| --- | --- | --- | --- |
| Data (cvPCA) | 0.27 (0.12, 0.42) | 1 | 0.25 (0.11, 0.40) |
| Twins, equal weights, c = 0.5 | 0.09 (-0.01, 0.18) | 0.32 | 0.03 (-0.10, 0.16) |
| Twins, equal weights, c = 0.7 | 0.11 (0.01, 0.22) | 0.41 | 0.07 (-0.07, 0.21) |
| Twins, reliability-weighted, c = 0.5 | 0.13 (-0.04, 0.30) | 0.49 | 0.10 (-0.05, 0.26) |
| Twins, reliability-weighted, c = 0.7 | 0.19 (0.01, 0.37) | 0.69 | 0.16 (-0.01, 0.33) |
| Weights only, c = 0.5 | 0.04 (-0.12, 0.20) | 0.16 | 0.00 (-0.14, 0.14) |

- Data minus equal-weight twins: 0.18 (0.03, 0.34) at c = 0.5 and 0.16 (0.00, 0.32) at c = 0.7 (8 structures);
  0.22 (0.05, 0.40) and 0.18 (-0.00, 0.36) in cortex.
- Data minus reliability-weighted twins: 0.14 (0.02, 0.26) at c = 0.5 and 0.08 (-0.05, 0.22) at c = 0.7.
- The twin slope increased with c (c = 0.3: 0.05 equal, 0.08 weighted; `summary_model_twins.csv`). A 1.3 x
  larger image or a left-right flip lowered the twin slopes (0.04 to 0.11).
- Interpretation: classical RF properties alone give at most about one third of the trend with equal weights.
  The combination of RF properties and unit reliability gives more. But realistic envelope sizes (c <= 0.5)
  leave at least half of the data slope unexplained.

### Figure 4 (not a display item). Phase invariance in gratings

`files/figures/fig4_phase_invariance.png`: (a) phase-invariant share of reliable grating variance; (b) alpha
(ranks 2-15) of the full, phase-averaged and phase-dependent responses; (c) phase-invariant share against
natural-scene alpha.

| Quantity | LGd | VISp | VISl | VISrl | LP | VISal | VISpm | VISam | Cortical slope |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Phase-invariant share | 0.48 | 0.79 | 0.88 | 0.85 | 0.80 | 0.90 | 0.91 | 0.92 | 0.15 (0.10, 0.19) |
| alpha, phase-averaged (2-15) | 1.91 | 1.71 | 1.82 | 1.92 | 1.81 | 1.98 | 2.12 | 2.16 | 0.57 (0.39, 0.76) |
| alpha, phase-dependent (2-30) | 0.91 | 1.21 | 1.30 | 1.31 | 0.82 | 1.30 | 1.24 | 1.23 | -0.01 (-0.23, 0.21) |

Higher cortical areas put more of their grating variance into the phase-invariant (orientation x spatial
frequency) subspace, and that subspace has a steeper spectrum in higher areas. The phase-dependent part
shows no cortical trend. This test was exploratory.

## Interpretation

The source result is not specific to natural images. The same area order appears for gratings and for natural
movies, which have very different statistics. Thus the faster decay is a property of how each area responds,
not of one image set. Matching RF size and position did not change the cortical slope, and twins that copy the
classical RF properties of each unit reproduce at most a minority of the slope at realistic RF sizes. The
grating analysis gives one candidate mechanism: higher areas are more invariant to spatial phase, so their
reliable variance falls into a smaller, more structured subspace. This agrees with a gradual increase of
invariance (pooling over local features) along the hierarchy, beyond what RF size alone gives. The tests do
not show a cause.

## Limitations

- Correlational, area-level tests with 8 structures (6 cortical areas). The hierarchy score is one summary of
  connectivity.
- The RF-matching test has low power. 99 units per area in the full data and 30 to 57 in half-samples. The
  natural-scene matched interval includes 0. We cannot exclude a moderate RF contribution.
- RF metrics come from a coarse Gabor mapping (10-degree grid, 20-degree patches). Only 11% (LP) to 62% (VISp)
  of units have a significant on-screen RF, so the RF analyses use a selected subset. The RF significance
  columns of the Allen CSV appear swapped; we documented our reading.
- The twin model is simple: one linear or energy filter per unit, no normalization, no surround, no noise. Its
  envelope scale is not calibrated; results depend on c. The screen geometry is an approximation (sweeps
  included). A stronger nonlinear model (for example a deep network) could explain more.
- Half-sample intervals are an approximation to the sampling spread of the full-sample statistic and use smaller
  populations. The planned bootstrap was replaced after we found its bias; both are reported.
- 118 to 480 conditions. alpha values depend on the number of conditions and repeats, so we compare only the
  slopes and area orders inside each stimulus set, not alpha values between sets. Movie bins are temporally
  correlated; slower integration in higher areas could add temporal smoothness to the movie spectra.
- No two-photon replication of the new tests in this work.

## Reproduction

Run `bash files/code/reproduce.sh SCRATCH_DIR OUT_DIR` with Python 3.12, numpy, scipy, pandas, h5py,
matplotlib and remfile 0.1.15. The script downloads metadata, streams about 15 GB from the public Allen S3
bucket into SCRATCH_DIR, and writes all results and figures into OUT_DIR. Random seeds are fixed. On the
campaign host (8 cores, load 40 to 60 from other jobs) the extraction took about 30 minutes with 6 streams and
the analyses about 3 hours. Main result files: `files/results/stats_half.json` (all primary intervals),
`summary_stimuli.csv`, `summary_rf_match.csv`, `summary_rf_split.csv`, `summary_model_twins.csv`,
`stats_extra.json`. Per-draw values are in `pooled.csv`, `half_stim.csv`, `rf_match.csv`, `half_rf.csv`,
`half_model.csv`, `model_twins.csv`, `phase_parts.csv`. The bundled results are aggregate statistics (alpha
values of unit draws); they contain no Allen record-level data.

Code files: `extract_multi.py` (NWB streaming), `get_templates.py` (images), `build_cache.py`, `mlib.py` (estimator),
`analysis_main.py` (P2, P1, RF split, phase share, planned bootstrap), `halfsample.py` (half-sample intervals and
model twins against data), `model_twins.py` (twin model and sweep), `phase_parts.py`, `stats.py`, `stats_half.py`,
`figures.py`.

## Provenance

- Campaign 11_07_2026; job sci-1107-hp-neural-structure-and-computation-014377fb3a8e; topic
  neural-structure-and-computation; machine hp; account claude-olen; model Claude Opus 5.5 (claude-opus-5-5).
  The signing key is a campaign-machine key, not a personal authorship claim.
- Shared campaign datasets used in place: `datasets/allen-vcn-ecephys-units-20261109/units.csv`
  (SHA-256 1dffbe8d...f078), `datasets/allen-vcn-ecephys-channels-20261109/channels.csv` (d2932f1e...ed98),
  `datasets/allen-vcn-ecephys-bo11-analysis-metrics-20261109/brain_observatory_1.1_analysis_metrics.csv`
  (a5335a7a...5209). Full hashes, URLs and the NWB ETags are in `files/provenance/`.
- The analysis plan was written at 2026-11-09 23:50 PST, before any new spectrum was computed. Changes after
  the plan: half-sample intervals in place of the bootstrap (reason above); the twin weighting variants and the
  phase split analysis were added as exploratory tests.

## References

- Stringer, C. et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature 571,
  361-365. doi:10.1038/s41586-019-1346-5.
- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575,
  195-202. doi:10.1038/s41586-019-1716-z.
- Siegle, J.H. et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature
  592, 86-92. doi:10.1038/s41586-020-03171-x.
- de Vries, S.E.J. et al. (2020) A large-scale standardized physiological survey reveals functional
  organization of the mouse visual cortex. Nat. Neurosci. 23, 138-151. doi:10.1038/s41593-019-0550-9.
- Pospisil, D.A., Pillow, J.W. (2024) Revisiting the high-dimensional geometry of population responses in
  visual cortex. bioRxiv. doi:10.1101/2024.02.16.580726.
- Source publication: sci:sha256:528cd3055e8110bfe80850a3d0f4df5233b0107c2e49b127939faec009c029a1.
- Related: sci:sha256:19f7eb8e97c3c505c7176cf992bc2c93b3ce4d8f97552f8f4484e6f79a14ea73 (reliability falls with
  distance from the retina), sci:sha256:39fdce5888169dfdc22376ddb8c02fc68aa3f6f22472bd136e6f6b445608b6f4
  (VISl-VISp spectrum crossover).
