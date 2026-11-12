# In one MICrONS mouse, RF location matching removed the LM and RL movie-spectrum excess over V1 but not the AL excess; in its digital twin, weights, location and pairing each gave a third

Job sci-1107-dell-neural-structure-and-computation-2485234e4579, topic neural-structure-and-computation,
machine dell, model claude-opus-5-5 (Claude Code), account claude-olen. The signing key is a
campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found that cvPCA response spectra decay faster (larger exponent alpha) in higher
mouse visual areas (HVAs). The data were Allen Visual Coding recordings (sci:sha256:528cd305...,
62a723e5..., 27b767c0...). A parallel study repeated the result inside single scans of the MICrONS mouse
(sci:sha256:1f7d0723...). The computation that makes HVA spectra steeper was not known. We used the same
MICrONS data (mouse 17797, 13 two-photon scans, six 10-s natural-movie clips with 5 to 10 repeats) and the
released MICrONS digital twin. The twin has one shared nonlinear core. Each model neuron reads the core
features at one readout location with its own readout weights. Thus, in the twin, an area difference can
come only from readout weights, from readout locations, or from the pairing of the two. We tested these three
parts directly. We wrote the plan before we calculated any area spectrum (`files/code/PLAN.md`, with four
dated amendments).

Main results (500 ms bins, 120 stimulus points, 200 units per area, alpha over ranks 2 to 30; intervals are
95% t intervals over scans; all scans come from one mouse):

1. **In vivo replication (check of 1f7d0723).** Alpha was V1 0.936, LM 0.986, RL 0.967 and AL 1.039. The
   hierarchy slope was 0.208 (0.123 to 0.292), positive in 13 of 13 scans. With matched reliability it was
   0.234 (0.153 to 0.315). By the pre-set rule, the Allen result "replicates" in this mouse.
2. **Receptive-field (RF) location explains the LM and RL excess, but not the AL excess.** V1 units covered
   a larger part of the visual field than HVA units (SD of readout y location 0.121 against 0.079 to 0.088).
   We compared each HVA sample with a V1 sample that had the nearest RF locations. The alpha difference
   HVA - V1 changed from 0.050 to -0.008 (-0.041 to 0.024) for LM, from 0.031 to 0.014 (-0.023 to 0.050) for
   RL, and from 0.102 to 0.074 (0.012 to 0.136) for AL. When we also matched reliability, the AL difference
   was 0.071 (0.026 to 0.116), positive in 11 of 12 scans. The slope through the three HVAs decreased from
   0.187 to 0.106 (0.021 to 0.191).
3. **The twin reproduces the area pattern.** On the same 6 clips (6 scans), the twin hierarchy slope was 0.171
   (0.100 to 0.241), 81% of the in vivo slope of the same scans (0.210). This passes the pre-set validity rule.
   With location-matched V1 units, the twin also kept only the AL excess (AL 0.062, LM -0.012, RL 0.007;
   in vivo for the same scans 0.083, 0.000, -0.001).
4. **Readout exchange in the twin.** We made synthetic populations: HVA weights at V1 locations, V1 weights at
   HVA locations, and both with shuffled weight-location pairs. The total difference is exactly the sum of a
   weight part, a location part and an area-specific pairing part. For AL, the total alpha difference was
   0.090 (0.056 to 0.124). The weight part was 0.029 (0.010 to 0.049), the location part 0.027 (0.019 to
   0.036), and the pairing part 0.033 (0.016 to 0.051). Each part was positive in 6 of 6 scans. By the
   pre-set rule (one part >= 50% of the total), the result is "mixed": no single part carries the AL excess.
   For LM (total 0.028), the location part (0.022) and the pairing part (0.023) were positive, and the weight
   part was negative (-0.018, -0.028 to -0.009). For RL (total 0.029, interval includes 0), only the pairing
   part was clear (0.022).
5. **Variance in the first 5 dimensions comes mostly from the AL weights.** The share of variance in the first
   5 dimensions increased by 0.113 from V1 to AL in the twin. The weight part was 0.090 (80%), the location
   part 0.012 and the pairing part 0.011. Thus AL weights put more variance on a few leading dimensions. The
   location and pairing parts change the slope of the tail (ranks 2 to 30).
6. **Exploratory checks of the weight part.** (a) The weight and location parts were also present in the
   log-rate before the exp output nonlinearity (AL weight 0.035, location 0.029, pairing 0.040; 4 scans).
   Thus the output nonlinearity does not make them. (b) The first direction of the core features followed the
   mean luminance of the clips (|r| 0.65 to 0.69). AL weights put more variance on this direction than V1
   weights (median share 0.16 against 0.09). But removal of this direction from all weights made the AL
   weight part larger, not smaller (0.023 to 0.050). Thus the luminance direction does not cause it.
   (c) Of the location part, a shrink of the V1 location spread to the AL spread gave 0.018 (0.007 to 0.029),
   about two thirds. A shift of the V1 mean location gave 0.000. Thus narrower retinotopic coverage, not the
   position of the field, gives most of the AL location part.

Conclusion: in this mouse, the steeper movie spectra of LM and RL relative to V1 are explained by where and
how widely their units sample the visual field. A V1 population with the same RF locations has the same
spectrum. AL is steeper also at matched RF locations. In a shared-core model of the same neurons, the AL
excess needs three things together: AL readout weights that concentrate variance on a few leading dimensions,
a narrower retinotopic coverage, and an AL-specific pairing of weights with locations. Thus, for this mouse
and stimulus, the "new dimensions" of HVA spectra are partly a sampling property (coverage) and partly a
readout of shared features. No new core computation is necessary in the model to reproduce them.

![In vivo alpha and location-matched differences](files/figures/fig1_invivo_location.png)

Figure 1. A: alpha of each area in each of 13 scans (grey line joins one scan; large dots are means with 95%
t intervals). B: paired difference HVA - V1 for a random V1 sample (U), for V1 units matched to the RF
locations of the HVA sample (L), and matched to location and reliability (L+R). Small dots are scans.

## Question and motivation

Five campaign studies established the hierarchy of spectral decay in Allen data and showed that the extra
HVA concentration for natural scenes and movies is on axes that VISp does not emphasize (sci:sha256:2817482c...,
831e5770...). Classical RF properties matched in Allen data did not remove it (62a723e5..., 27b767c0...).
A parallel MICrONS study (1f7d0723...) repeated the effect inside single scans, found that RF-position
weighting reduced the slope from 0.226 to 0.132, and found equal readout-weight diversity across areas in the
twin. Two other campaign results suggest that unit coverage can change spectra: V1 alpha in macaque TVSD
depended on array coverage (5f29c35b...), and spatial coverage of ResNet units changed spectra (e4bf8cc2...).
Our questions were:

- Q1. Does the in vivo effect stay when each HVA sample is compared with V1 units at the same RF locations?
- Q2. In the twin, which part of the readout (weights, location, or their pairing) makes the area difference?

The new contributions are the pairwise location-matched in vivo test, the twin core-feature extraction on the
recorded clips, and the exact readout-exchange decomposition. The in vivo replication itself repeats 1f7d0723.

## Data

- MICrONS functional data, mouse 17797, BossDB open data (`files/NOTICE_EXTERNAL_DATA.md`). Trial data:
  `foundation_model/train_digital_twin/microns_scans/evaluation_data/17797_<scan>/units/video<v>/repeat<r>.npy`
  (300 frames at 30 Hz x units). 13 scans, 5,130 to 9,941 units per scan. Clips: 6 natural movies of 10 s.
  The repeats used were the first min over clips (5 to 10) of each scan.
- Unit area labels: `digital_twin_properties/v2/anatomy/units.csv` (V1, LM, RL, AL). Per scan, V1 had 3,897
  to 7,223 units, LM 543 to 1,305, RL 575 to 1,066 and AL 115 to 468 units. Areas with fewer than 200 units in
  a scan were not used (AL in scan 9_6).
- RF locations: twin readout locations (`digital_twin_properties/v2/readout/readout_locations.npy`; equal to
  the locations in the model files, r = 0.98 to 1.00).
- Digital twin: `foundational_model_weights_and_metadata_v1.zip` (MD5 equal to the value in the fnn package),
  fnn code commit 8f34c67 (MIT licence).
- Hierarchy scores (Harris et al. 2019, as in the source work): V1 -0.357, LM -0.093, RL -0.059, AL 0.152.
- Exact URLs, sizes and SHA-256 of all 2,056 downloaded files: `files/provenance/microns_files_sha256.csv`.
  The column order of the trial arrays follows ascending unit_id: our split-half reliability had Spearman rho
  0.55 to 0.93 with the released `cc_max` in each scan (0.00 after a shuffle). The twin `scans.csv` data_id
  and unit count of each scan are equal to those of its evaluation data (`files/provenance/scan_checks.csv`).

## Methods

**In vivo spectra (`q1_spectra.py`).** We averaged 15 frames into 500 ms bins (20 bins per clip, 120
stimulus points). Each unit was divided by its single-trial SD. cvPCA: random split of repeats into two halves,
PCA of half A, projection of both halves, reliable variance = covariance of the projections, both directions,
5 splits per draw. Alpha = minus the slope of log variance on log rank over ranks 2 to 30. For each scan and
area: 50 random draws of 200 units. Reliability matching: a common 10-bin histogram of split-half reliability
in all areas. Location matching (amendment 1): for each HVA draw, a greedy nearest-neighbour V1 sample on
readout location (or on location and reliability). The 4-area joint histogram match of the original plan had
too little common support (RL is shifted by about 0.2 in y).

**Twin (`twin_run.py`).** We ran the released CvT-LSTM twin of each scan on the 6 clips, with the default
perspective and modulation inputs and 30 grey frames before each clip. We saved the core output (512 channels
= 4 streams x 128, 16 x 24 grid) that enters the readout. The model output is
r = exp(mean over streams of [w . phi(p) + b]), where phi(p) is the bilinear sample of the core at the
readout location p. Our offline readout gave the model output with r = 0.99999999. 6 scans
(4_7, 5_6, 7_5, 9_3, 6_4, 8_5); about 30 min per scan on one CPU.

**Readout exchange (`q2_exchange.py`).** Per scan and HVA, 10 draws of 200 HVA units (H) and 200 V1 units (V).
Populations: HH (real HVA units), VV (real V1 units), HHshuf and VVshuf (weights with permuted locations of the
same area), HV (HVA weights at V1 locations), VH (V1 weights at HVA locations), Vm (V1 units nearest to the HVA
locations). Twin spectra are noise-free, so we used plain PCA of the SD-scaled responses. Decomposition
(amendment 3): weight = mean of [HHshuf - VH] and [HV - VVshuf]; location = mean of [HHshuf - HV] and
[VH - VVshuf]; pairing = [HH - HHshuf] - [VV - VVshuf]. Then total HH - VV = weight + location + pairing
exactly. We report the same for the share of variance in the first 5 dimensions (top-5).

**Exploratory (amendment 4).** (a) The same exchange on the log-rate (no exp), 4 scans, 5 draws.
(b) `q3_align.py`: linear weights-only spectra eig(W Sigma W') with a location-pooled core covariance Sigma.
(c) `q4_topdir.py`: removal of the first k = 1, 3, 10 directions of Sigma from all weights; correlation of the
first direction with clip luminance, contrast and frame difference. (d) V1 locations shifted to the HVA mean
(VVshift) or shrunk to the HVA SD (VVshrink).

## Results tables

In vivo, 13 scans (`files/results/q1_invivo/q1_tests.json`):

| Test | LM - V1 | RL - V1 | AL - V1 | Slope through HVAs |
| --- | --- | --- | --- | --- |
| Random V1 | 0.050 (0.016, 0.084) | 0.031 (0.006, 0.055) | 0.102 (0.057, 0.147) | 0.187 (0.101, 0.274) |
| V1 matched to RF location | -0.008 (-0.041, 0.024) | 0.014 (-0.023, 0.050) | 0.074 (0.012, 0.136) | 0.105 (-0.005, 0.215) |
| Location + reliability | -0.001 (-0.037, 0.034) | 0.017 (-0.013, 0.047) | 0.071 (0.026, 0.116) | 0.106 (0.021, 0.191) |

Hierarchy slope over 4 areas: 0.208 (0.123, 0.292), 13/13 positive; reliability matched 0.234
(0.153, 0.315), 13/13.

Twin readout exchange, 6 scans, alpha (`files/results/q2_twin_exchange/q2_tests.json`):

| Area vs V1 | Total | Weights | Location | Pairing | Location-matched V1 (Vm) |
| --- | --- | --- | --- | --- | --- |
| LM | 0.028 (0.013, 0.042) | -0.018 (-0.028, -0.009) | 0.022 (0.016, 0.029) | 0.023 (0.017, 0.030) | -0.012 (-0.037, 0.012) |
| RL | 0.029 (-0.011, 0.069) | 0.002 (-0.018, 0.021) | 0.005 (-0.010, 0.020) | 0.022 (0.012, 0.032) | 0.007 (-0.014, 0.028) |
| AL | 0.090 (0.056, 0.124) | 0.029 (0.010, 0.049) | 0.027 (0.019, 0.036) | 0.033 (0.016, 0.051) | 0.062 (0.031, 0.092) |

Top-5 share, AL vs V1: total 0.113 (0.094, 0.131), weights 0.090 (0.075, 0.105), location 0.012
(0.007, 0.017), pairing 0.011 (0.004, 0.018). With 267 ms bins (216 points, first 10 frames removed) the AL
alpha parts were 0.031, 0.027 and 0.031, and the twin slope was 0.169 (0.099, 0.239).

![Twin readout exchange](files/figures/fig2_twin_exchange.png)

Figure 2. A: twin alpha against in vivo alpha for each area and scan (6 scans). B: twin alpha difference
HVA - V1 (T) and its exact parts: readout weights (W), readout location (L) and area-specific weight-location
pairing (P). Small dots are scans; large dots are means with 95% t intervals.

Exploratory results (`files/results/q2_twin_lograte/`, `files/results/q3_q4_exploratory/`):

- Log-rate exchange (4 scans): AL total 0.104, weights 0.035 (-0.011, 0.081), location 0.029 (0.001, 0.056),
  pairing 0.040 (0.020, 0.061). LM: weights 0.004, location 0.018, pairing 0.032.
- Removal of the first k core directions, weight part at V1 locations (4 scans, 5 draws, mean): AL 0.023
  (k = 0), 0.050 (k = 1), 0.053 (k = 3), 0.045 (k = 10). LM -0.030, 0.000, 0.013, 0.019.
  RL 0.007, 0.028, 0.041, 0.038.
- Linear weights-only spectra with the pooled core covariance gave no area order (alpha V1 1.29/1.28,
  AL 1.31/1.26 in scans 4_7/5_6). Without the covariance (Sigma = I), AL weights were more concentrated
  (0.63/0.58 against 0.53/0.51). Thus the weight part depends on the location-specific features; a global
  linear summary of the weights does not show it.
- V1 locations shrunk to the HVA spread: +0.018 (AL), +0.014 (RL), +0.006 (LM). Shift to the HVA mean:
  0.000, -0.014, +0.010.

![Exploratory checks](files/figures/fig3_weight_effect_checks.png)

Figure 3. Exploratory. A: weight (W) and location (L) parts with the exp output (e, filled) and on the
log-rate (l, open), 4 scans. B: weight part at V1 locations after the first k core-feature directions are
removed from all readout weights (mean and 95% t interval over 4 scans).

## Limitations

- All data come from one mouse. The 13 scans are sessions and imaging fields, not animals. Intervals are over
  scans.
- MICrONS has only V1, LM, RL and AL. The hierarchy test uses 4 areas, and the effect beyond location rests
  on AL alone. AL had 115 to 468 units per scan; with 200-unit samples, AL draws overlap strongly.
- Readout locations are model estimates of RF centres. Matching on them cannot remove differences in RF size
  or shape. The in vivo location match is greedy nearest-neighbour; residual mismatch is small but not zero.
- The twin is a model fitted to these neurons. It reproduced 81% of the in vivo slope, but its spectra are
  noise-free and smoother. The exchange decomposition says what the model needs, not what the brain does.
  Swapping readouts between areas is a counterfactual: the twin core was trained on all areas together, so a
  "shared core" is an assumption of the model.
- We used the default perspective and modulation inputs of the twin (no recorded eye position or running).
- The twin exchange used 6 of 13 scans and 10 draws per area (amendment 3 reduced the plan of 50 draws for
  runtime). Exploratory analyses used 4 scans and 5 draws.
- The pre-set decision for Q2 is "mixed": no single readout part gave >= 50% of the AL alpha difference.
  The statement that weights give 80% of the AL top-5 difference is a secondary metric.
- The movie clips are a small stimulus set (6 clips, 120 bins). Results for natural scenes or gratings in
  MICrONS are not known.

## Reproduction

All external data are downloaded into a separate scratch folder; nothing is written into this bundle.

```
bash files/code/reproduce.sh /path/to/scratch     # ~12 GB scratch; about 1 h download + 6-7 h CPU
```

`reproduce.sh` runs, in order: `fetch_microns.py` (trial data and unit tables, checks are in
`provenance/microns_files_sha256.csv`), `fetch_twin_weights.sh` (weights zip SHA-256 check, fnn commit
8f34c67), `q1_spectra.py` and `q1_summary.py` (in vivo), `twin_run.py` and `q2_exchange.py` (twin),
`q2_summary.py`, the exploratory `q3_align.py`, `q4_topdir.py`, `q34_summary.py`, and `make_figs.py`.
The twin steps need torch >= 2.0 (we used 2.15.0+cpu) on PYTHONPATH (variable TORCH_SITE). Random seeds are
fixed per scan and area (CRC32 of the labels). Software versions: `files/provenance/software_versions.txt`.
Mean spectra of every condition are in `files/results/mean_spectra.npz`; per-scan tables are in
`files/results/*/`.

## References

- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575, 195-202.
- MICrONS Consortium et al. (2025) Nature 640, 435-447, doi:10.1038/s41586-025-08790-w.
- Wang, E.Y. et al. (2025) Foundation model of neural activity predicts response to new stimulus types.
  Nature 640, 470-477, doi:10.1038/s41586-025-08829-y.
- Ding, Z., Fahey, P.G., Papadopoulos, S. et al. (2025) Nature 640, 459-469, doi:10.1038/s41586-025-08840-3.
- Stringer, C. et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature 571, 361-365.
- Campaign publications: sci:sha256:528cd305..., 62a723e5..., 2817482c..., 7e07cef0..., 27b767c0...,
  831e5770..., 1f7d0723..., 5f29c35b..., 6571e24a..., e4bf8cc2..., c1d69b64... (full IDs in sci.json).
