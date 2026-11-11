# In 32 Allen Neuropixels mice, higher visual areas are a linear VISp read-out for gratings but not for natural scenes and movies; movie spectral compression is outside the VISp-predictable part

## Summary

Higher mouse visual areas (HVAs) have response spectra that decay faster (larger exponent alpha) than VISp.
Earlier campaign work showed that, for natural scenes and movies, this compression is not on the dominant VISp
stimulus axes but on axes that HVAs share (sci:sha256:2817482c...). Two theory bundles then showed that this
result alone cannot tell whether HVAs use signal outside the VISp linear span or only re-weight VISp signal
(sci:sha256:0aac19e1..., sci:sha256:41688665...). We tested this directly with trial-level spikes of 11,559
units in all 32 Allen Visual Coding Neuropixels mice. We predicted each area's trial-averaged responses with
cross-validated kernel ridge regression from (1) VISp populations of other mice or of the same mice on
disjoint trials, (2) size-matched populations of the other HVAs, and (3) image-computable features. All scores
are noise-corrected. Intervals are mean +/- 1.96 SD over random 16/16 splits of the mice.

Main results:

1. **Gratings (positive control): HVAs are a linear read-out of VISp.** VISp of other mice explained as much
   reliable grating variance in each HVA as in VISp itself (ratio rho 0.99 to 1.13). The grating compression
   was in the VISp-predictable part (hierarchy slope of its alpha 0.50, 0.27 to 0.73, against 0.62 for the
   total; residual 0.06, -0.23 to 0.34).
2. **Natural scenes and movies: HVAs are only partly a linear read-out of VISp.** For natural scenes, VISp
   explained only 0.36 (VISrl) to 0.81 (VISpm) of the variance that it explained in VISp itself; for movie
   three 0.63 to 0.88; for movie one 0.79 to 1.00. VISp of the *same* mice, on disjoint trials, did no better.
   Thus the shortfall is not a mismatch of receptive-field positions between mice. A size-matched population
   of the *other* HVAs predicted each HVA better than VISp did (FEV +0.11, +0.07 and +0.09 for scenes, movie
   one and movie three; all intervals above 0). On the top-5 own-area axes of an HVA, VISp predicted 27% of
   the natural-scene variance, the other HVAs 44%; on VISp's own top-5 axes, VISp predicted 65%.
3. **Movies: the compression is in the part that VISp cannot predict.** The hierarchy slope of alpha was
   0.37 (0.20 to 0.55) for the VISp residual of movie one and 0.32 (0.24 to 0.40) for movie three, at least
   as large as for the total (0.30, 0.20). For the VISp-predicted part it was 0.16 (-0.01 to 0.32) and 0.03
   (-0.06 to 0.12). The same-mouse variant gave the same result. For natural scenes the residual part also
   had the full slope (0.17, 0.01 to 0.33), but the predicted part was too uncertain to place the
   compression (0.26, -0.00 to 0.53).
4. **What the new natural-scene dimensions contain: local phase-invariant energy, not global image
   statistics or ImageNet features.** A V1-like Gabor-energy model added HVA-specific signal beyond VISp
   (hierarchy slope of the gain 0.075, 0.038 to 0.112; gain 0.07 to 0.14 in HVAs, 0.00 in VISp). Global image
   statistics (luminance, contrast, global energy) added little, and ImageNet-trained AlexNet layers added
   0.03 at most. In an exploratory test, the energy gain was largest for 6 x 8 to 12 x 16 pooling grids and
   fell to near 0 for global pooling. For movies, no image model added HVA-specific signal beyond VISp, but the dominant
   shared HVA axis was motion energy (r = -0.83 with frame-difference energy in movie one; it carried 22% of
   pooled HVA signal variance against 14% in VISp).
5. **Why lower-dimensional: not resolved.** Energy features pooled over larger regions have steeper spectra
   (alpha 0.75 for 12 x 16 cells to 1.92 for global pooling), but the HVAs preferred local or medium pooling,
   and no feature-predicted part reproduced the hierarchy slope of alpha. ImageNet-trained AlexNet kernels
   had flat spectra (alpha 0.31 to 0.61) and random-weight kernels steeper ones (0.85 to 1.38).

Conclusion: for gratings, HVA responses are linear functions of VISp population responses. For natural
scenes and movies, a large part of the reliable HVA signal is not a linear function of the recorded VISp
population, in the same or in other mice, but is shared among HVAs. The movie compression lies in this part.
For natural scenes this part contains local energy (complex-cell-like) features that VISp responses do not
give linearly. These are correlational results in one data set.

## Question and motivation

The prior bundle sci:sha256:2817482c... measured target variance on fixed stimulus axes of basis populations.
It found that for natural scenes and movies HVAs are compressed on axes that HVAs share, not on VISp axes.
Two theory bundles proved that axis variances cannot separate two cases (sci:sha256:0aac19e1...,
sci:sha256:41688665...):

- **In-span re-weighting.** The HVA response is a linear map of the VISp response. The map makes weak VISp
  directions strong. Then a linear read-out of VISp predicts the HVA response as well as it predicts VISp.
- **New span.** The HVA response holds signal that no linear map of VISp gives (for example nonlinear
  features or signals from other pathways). Then a linear read-out of VISp predicts HVAs less well than VISp.

We asked: (Q1) Is HVA signal inside the VISp linear span, and is the compression in the VISp-predictable part?
(Q2) Which image-computable features predict the part that VISp does not predict? (Q3) Do these features
explain why the HVA spectra are steeper? (Q4) Which image properties order the images along the top HVA axes?
We wrote the plan before we computed any new response statistic (`files/code/PLAN.md`, with five dated
amendments; see "Changes to the plan").

## Data

- Allen Visual Coding Neuropixels, all 32 `brain_observatory_1.1` sessions (one mouse per session), streamed
  with HTTP range reads. S3 ETags are in `files/provenance/source_nwb_etags.tsv`. They are identical to those
  of sci:sha256:2817482c....
- Units: Allen quality filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9) in LGd
  (961 units), LP (1,540), VISp (2,230), VISl (1,016), VISrl (1,563), VISal (1,675), VISpm (950) and VISam
  (1,624); total 11,559, the same as the prior work. Each unit is scaled by its single-trial SD.
- Stimuli: natural scenes (ns; 118 images, 50 repeats, spikes 0-250 ms), natural movie one (nm1; 120 bins of
  250 ms, 20 repeats), natural movie three (nm3; 480 bins, 10 repeats), static gratings (sg; 120 conditions,
  45 repeats; comparison only).
- Stimulus templates: natural-scene images and movie frames from the Allen Visual Coding 2p NWB files 500964514
  and 501271265 (the Neuropixels NWB files hold no templates). AlexNet ImageNet weights from torchvision.
- Hierarchy scores (Harris et al. 2019): LGd -0.515, VISp -0.357, VISl -0.093, VISrl -0.059, LP 0.105, VISal
  0.152, VISpm 0.327, VISam 0.441.

The Allen files, the images, the weights and all record-level or per-image derivatives are not in this bundle
(`files/NOTICE_EXTERNAL_DATA.md`).

## Methods

**Splits.** For each split we divided the 32 mice at random into a target group G1 (16) and a predictor group
G2 (16). Target: 150 random units of an area in G1. Its repeats are split into halves A and B (one split for
all conditions). Neural predictors: 400 VISp units (VISp400), 150 units of each structure, all G2 VISp units
(VISpall), or 400 units of the HVAs other than the target (hvaoth). In the main variant the predictors come from
G2 (other mice). In the same-mouse variant they come from G1 and use repeat third T1, while the target uses
thirds T2 and T3, so predictor and target share no trials.

**Encoding.** Kernel ridge regression across conditions with a linear kernel of the centred predictor matrix
(trial means). Outer CV: 10 folds of conditions (random for ns and sg; contiguous blocks for movies). Ridge
lambda per outer fold by inner 5-fold CV (13 values). We fitted predictions P_A and P_B to Y_A and Y_B.

**Noise-corrected explained variance.** FEV = (2 <P, Ybar> - <P_A, P_B>) / <Y_A, Y_B>, summed over units and
conditions (centred). It uses only products across independent halves, so it has no noise bias. Simulations
gave 0.988 for a true value of 0.995 and about 0 for a random predictor. rho_A = FEV(A | VISp400) /
FEV(VISp | VISp400) in the same split.

**Spectra of parts.** Total: cvPCA of (Y_A, Y_B). VISp-predicted part: cvPCA of (P_A, P_B). Residual part:
cvPCA of (Y_A - P_B, Y_B - P_A); the cross-fitting gives zero-mean noise cross-terms. alpha = minus the slope of
log variance on log rank, ranks 2-20 for ns and 2-30 for the other sets. The ridge shrinkage makes predicted
parts steeper for all targets of one predictor, so we compare areas on one predictor.

**Axis shares.** Image-space axes of each area come from a basis of 100 G2 units of that area (repeat half R2,
disjoint from the predictor units and repeats). We report the share of the target's variance on the top 5 axes
that the predictor reproduces.

**Image features.** low: mean luminance and RMS contrast of the image and of a 3 x 3 grid; lum: luminance on a
24 x 30 grid; gabor: energy of quadrature Gabor pairs (8 orientations, 5 SFs 0.02-0.32 cyc/deg) averaged on a
6 x 8 grid; gaborg: the same energies averaged over the image; motion (movies): mean absolute frame difference
on a 6 x 8 grid; alexnet_conv1 ... fc7: ReLU outputs of ImageNet-trained AlexNet; randnet_*: AlexNet with
random weights. Movie features are averaged over the frames of each 250 ms bin. A combination kernel adds the
VISp400 kernel and a feature kernel, each scaled to unit trace. The gain is FEV(VISp + F) - FEV(VISp).

**Statistics.** Hierarchy slope: OLS slope over the 6 cortical areas. Interval: mean over splits +/- 1.96 SD
over splits (60 splits for ns, nm1, sg and the running control; 12 for nm3 in the main variant; 30 in the
same-mouse variant and the pooling test). This is the approximate half-sample interval used by the prior work.

**Pre-set decision rules (PLAN.md).** T1: "inside the VISp linear span" if rho >= 0.9 for all 5 HVAs; "partly
outside" if the FEV hierarchy-slope interval is below 0. T2: "compression in the VISp-predictable part" if the
s_pred interval excludes 0 and s_pred >= 0.5 s_tot; "not in the VISp-predictable part" if the s_pred interval
includes 0 and the s_tot interval excludes 0. T3: feature F adds HVA-specific signal if the hierarchy slope of
its gain has an interval above 0. T4: Spearman correlation of the best AlexNet layer with hierarchy.

## Results

### Figure 1. Linear span

`files/figures/fig1_linear_span.png`. (a) FEV of each cortical area from 400 VISp units (blue) or 400 units of
the other HVAs (orange), from other mice (filled, solid) or the same mice on disjoint trials (open, dashed).
(b) Share of the target's variance on its top-5 own-area axes that the predictor reproduces.

Ratio rho = FEV(HVA | VISp) / FEV(VISp | VISp), other mice (`results/main/rho_main.csv`):

| Set | VISl | VISrl | VISal | VISpm | VISam | Pre-set T1 verdict (other mice / same mice) |
| --- | --- | --- | --- | --- | --- | --- |
| Natural scenes | 0.63 | 0.36 | 0.55 | 0.81 | 0.66 | inconclusive / partly outside |
| Natural movie one | 0.89 | 0.79 | 0.89 | 0.92 | 1.00 | inconclusive / inconclusive |
| Natural movie three | 0.67 | 0.65 | 0.63 | 0.80 | 0.88 | inconclusive / inconclusive |
| Static gratings | 1.06 | 0.99 | 1.09 | 1.13 | 1.13 | inside the VISp linear span / not run |

- Absolute FEV from VISp400 (other mice), natural scenes: VISp 0.37, VISl 0.23, VISrl 0.13, VISal 0.20, VISpm
  0.30, VISam 0.24; gratings 0.74 to 0.84. Even for VISp targets, VISp of other mice explained only 37% of the
  reliable natural-scene variance (39% in the same mice). Most of each population's reliable natural-image
  signal is therefore not a linear function of another VISp population of 400 units.
- The FEV hierarchy slope was below 0 only for natural scenes in the same-mouse variant (-0.088, -0.168 to
  -0.008). In the other cases rho was below 0.9 for at least one HVA, but the slope interval included 0, so T1
  is "inconclusive" by the pre-set rule.
- Other HVAs minus VISp, mean over the 5 HVAs (`results/derived/paired_hva_vs_visp.csv`): natural scenes +0.106
  (0.077 to 0.135; same mice +0.091), movie one +0.065 (0.039 to 0.091; +0.062), movie three +0.086 (0.059 to
  0.113; +0.081), gratings +0.006 (-0.005 to 0.017).
- Axis shares (`results/derived/axis_hva_summary.csv`), top-5 own-area axes, mean of 5 HVAs: VISp predicted 0.27
  (scenes), 0.31 (movie one), 0.32 (movie three), 0.84 (gratings); other HVAs 0.44, 0.42, 0.44, 0.87. On the
  top-5 VISp axes the two predictors did equally well (0.50 vs 0.44, 0.41 vs 0.44, 0.48 vs 0.48). Thus VISp
  fails specifically on the dominant HVA axes.
- Running control: with single-trial running speed regressed out of each unit, the natural-scene values did not
  change (rho 0.37 to 0.81; HVA-minus-VISp +0.107).

### Figure 2. Where the spectral compression is

`files/figures/fig2_compression_parts.png`. (a) Hierarchy slopes of alpha for the total response, the
VISp-predicted part and the VISp residual part (circles: other mice; squares: same mice). (b, c) alpha of each
area for the total and the VISp residual.

| Set, variant | Total s_tot | VISp-predicted s_pred | VISp residual s_res | Pre-set T2 verdict |
| --- | --- | --- | --- | --- |
| Natural scenes, other mice | 0.17 (0.03, 0.31) | 0.26 (-0.00, 0.53) | 0.17 (0.01, 0.33) | not in the VISp-predictable part (marginal) |
| Natural scenes, same mice | 0.18 (0.02, 0.33) | 0.26 (-0.00, 0.52) | 0.17 (0.07, 0.28) | not in the VISp-predictable part (marginal) |
| Natural scenes, running removed | 0.18 (0.01, 0.35) | 0.28 (0.05, 0.52) | 0.17 (-0.00, 0.35) | in the VISp-predictable part |
| Movie one, other mice | 0.30 (0.17, 0.43) | 0.16 (-0.01, 0.32) | 0.37 (0.20, 0.55) | not in the VISp-predictable part |
| Movie one, same mice | 0.30 (0.14, 0.47) | 0.17 (-0.03, 0.37) | 0.39 (0.19, 0.60) | not in the VISp-predictable part |
| Movie three, other mice | 0.20 (0.08, 0.32) | 0.03 (-0.06, 0.12) | 0.32 (0.24, 0.40) | not in the VISp-predictable part |
| Movie three, same mice | 0.21 (0.08, 0.33) | 0.02 (-0.15, 0.19) | 0.29 (0.09, 0.49) | not in the VISp-predictable part |
| Static gratings, other mice | 0.62 (0.43, 0.82) | 0.50 (0.27, 0.73) | 0.06 (-0.23, 0.34) | in the VISp-predictable part |

- For both movies and both variants the compression is in the residual part. The residual slope is as large as
  or larger than the total slope, and the predicted-part slope interval includes 0.
- For natural scenes the verdict depends on the third decimal of the s_pred lower bound (-0.005, -0.004, and
  +0.046 after running removal). We treat it as undetermined: the residual part has the full slope, but the
  predicted part may also carry a slope. The predicted part is a small share of the variance (FEV 0.13 to 0.30
  in HVAs), and its alpha is steepened by ridge shrinkage, so its slope is imprecise.
- Gratings: the compression is in the VISp-predictable part, as the prior work found on VISp axes.

### Figure 3. Image-computable features

`files/figures/fig3_features.png`. (a, b) FEV gain over VISp400 alone (other mice) when a feature kernel is
added, for natural scenes and movie one. (c) Exploratory: gain of Gabor energy pooled on grids from 12 x 16 to
1 x 1 cells, for VISp and VISam. (d) alpha of the feature kernels themselves on the 118 natural scenes.

T3, hierarchy slope of the gain over VISp (`results/main/tests_main.json`):

| Feature added to VISp | Natural scenes | Movie one | Movie three |
| --- | --- | --- | --- |
| Gabor energy (6 x 8) | 0.075 (0.038, 0.112) | 0.012 (-0.035, 0.059) | 0.003 (-0.036, 0.042) |
| Global Gabor energy | 0.026 (0.002, 0.050) | -0.055 (-0.130, 0.019) | -0.002 (-0.035, 0.031) |
| Low-level statistics | 0.022 (-0.010, 0.054) | -0.005 (-0.059, 0.049) | -0.001 (-0.027, 0.025) |
| AlexNet conv2 | 0.029 (0.009, 0.049) | 0.004 (-0.020, 0.029) | 0.009 (-0.007, 0.024) |
| AlexNet conv5 | 0.032 (0.016, 0.048) | 0.007 (-0.017, 0.032) | 0.016 (0.003, 0.029) |
| Motion energy | n/a | 0.007 (-0.046, 0.060) | 0.020 (-0.005, 0.045) |
| Other HVAs (400 units) | 0.035 (-0.035, 0.106) | 0.050 (-0.013, 0.112) | 0.048 (0.004, 0.092) |

- Natural scenes: the Gabor-energy gain was 0.00 in VISp and 0.07 (VISl), 0.14 (VISrl), 0.09 (VISal), 0.08
  (VISpm), 0.09 (VISam). Gabor energy alone predicted VISrl better (FEV 0.25) than VISp400 did (0.13). All
  AlexNet layers met the T3 rule for natural scenes, but with HVA gains of 0.02 to 0.05 only. The other-HVA
  population added 0.11 to 0.14 in every HVA (its slope over the 5 HVAs was not above 0).
- Movies: AlexNet conv layers added 0.01 to 0.06 in all areas, also in VISp (0.04 for movie one), so these gains
  were not HVA-specific. Gabor, low-level and motion-energy kernels added at most 0.03. The other-HVA gain was
  larger (0.08 to 0.13 in the HVAs).
- T4 (descriptive): the best AlexNet layer was conv2 for VISp and conv5 (movie one; conv5 or fc6 for movie
  three) for most HVAs; Spearman with hierarchy 0.65 (p = 0.16) and 0.72 (p = 0.11). For natural scenes conv2 was
  best in VISp and in 4 of 5 HVAs (Spearman 0.13). Absolute AlexNet FEV was low (0.03 to 0.18).
- Exploratory pooling test (`results/derived/pooling_*.csv`, 30 splits): for natural scenes the gain over VISp
  was largest for 6 x 8 and 12 x 16 grids (HVAs 0.07 to 0.14) and near 0 for the global 1 x 1 pool (-0.00 to
  0.03). The best grid alone was 6 x 8 (median) in VISal, VISpm and VISam and 12 x 16 in VISp, LGd, VISl and
  VISrl. For movie one all gains were small (at most 0.04).
- Spectra of the features (`results/main/feature_alpha.csv`, `results/pooling_scale/feature_alpha.csv`): the
  natural-scene Gabor-energy kernel had alpha 0.75 (12 x 16), 0.81 (6 x 8), 0.90 (3 x 4), 1.07 (2 x 2) and 1.92
  (1 x 1). ImageNet AlexNet layers had alpha 0.31 to 0.61, random-weight AlexNet layers 0.85 to 1.38. The neural
  totals were 0.76 to 0.91 for cortical areas.

### Descriptive axis identity (Q4)

`results/axes/` holds full-sample (all 32 mice) analyses of the top axes of the pooled HVA population and of
VISp, LP and LGd.

- Natural scenes: VISp axis 1 tracked central contrast (r = 0.72 with RMS contrast of the central grid cell).
  The pooled-HVA axis 1 tracked low-SF energy (r = -0.48 at 0.04 cyc/deg) and axis 2 mean luminance (r = -0.42).
  Gabor energy predicted HVA axes 4 to 10 better (mean FEV 0.52) than VISp axes 4 to 10 (0.30).
- Movies: axis 1 was motion energy in VISp and in HVAs (r = -0.84 and -0.83 for movie one; 0.58 and -0.78 for
  movie three; the sign is arbitrary). It carried 22% of the pooled HVA signal variance against 14% in VISp
  (movie one) and 16% against 12% (movie three).
- Subspace overlap (mean squared cosine of the top-3 axes): pooled HVAs vs VISp 0.33 (scenes), 0.49 (movie one),
  0.52 (movie three); pooled HVAs vs VISam 0.89, 0.85, 0.92.

## Interpretation

1. The grating result agrees with the prior work: higher areas keep the phase-invariant part of the VISp
   representation, and a linear read-out of VISp gives the HVA grating responses. Complex-cell-like units are
   already present in VISp, so a linear read-out of the population can give phase invariance for gratings.
2. For natural scenes and movies, the HVA signal that carries most variance is shared among HVAs but is not a
   linear function of 400 recorded VISp units, even in the same mice. This favors the "new span" case over pure
   in-span re-weighting, within the limits below. The movie compression is in this non-linear part.
3. For natural scenes, local energy features at a medium scale explain part of the non-VISp signal. A plausible
   reading is that HVAs pool rectified (energy-like) VISp outputs over space, which no linear map of the VISp
   responses gives when the predictor population samples only part of the visual field. For movies, the
   dominant shared HVA axis is motion energy. HVAs give it more variance than VISp.
4. Steeper spectra are a property of pooled energy features, but the HVAs did not prefer global pooling, and
   the feature-predicted parts did not reproduce the hierarchy slope. The cause of the lower dimension remains
   open.

## Limitations

- Linear span is limited by what we can measure. 400 units per predictor, trial noise and 118 to 480 conditions
  limit FEV (VISp predicted only 37% of VISp natural-scene variance). A larger or less noisy VISp sample could
  explain more of the HVA signal. The comparison with size-matched other-HVA predictors controls for size and
  noise, but not for the different visual-field coverage of VISp and HVA samples.
- The pre-set T1 rule gave "inconclusive" in 5 of 7 natural-stimulus cases: rho was below 0.9, but the FEV
  slope interval included 0. The natural-scene T2 verdict is marginal and changed with the running control.
- Movie three used 12 splits in the main variant (run time), and the pooling test, the same-mouse
  extension with other-HVA predictors and the Q4 axis analyses were added after the first results
  (amendments 4 and 5). They need independent confirmation.
- Combination kernels use one fixed weight; a better weight could give larger gains.
- The image models are simple. We used one CNN (AlexNet) and assumed 16 px/deg for scenes and 5.07 px/deg for
  movies. Movie features were averaged over 250 ms bins.
- Correlational tests in one data set, with 6 cortical areas for each hierarchy slope. We did not repeat the
  tests in the two-photon data.

## Changes to the plan

`files/code/PLAN.md` holds the plan (written about 12:00 PST on 2026-11-10, before any new response statistic)
and five amendments: (1) population sizes changed because some areas have fewer units in a 16-mouse half;
(2) one fixed combination weight and a reduced running control, for run time; (3) movie three as a separate
run with 24 planned splits (12 finished) and no random-weight network or pixel kernels; (4) after one split, the
same-mouse variant became a main test and got the other-HVA predictor; (5) the exploratory pooling-scale test.
Debug runs on 11 sessions were used only to test code. Host processes stopped twice; finished splits were saved
and the runs were resumed with the same seeds (restructured code reproduced a saved split to 6e-8).

## Reproduction

Run `bash files/code/reproduce.sh SCRATCH_DIR OUT_DIR` (requirements: `files/code/requirements.txt`; versions:
`files/provenance/python_versions_used.txt`). It reads the Allen metadata and about 15 GB of NWB data from the
public Allen S3 bucket, the stimulus templates from two 2p NWB files, and the AlexNet weights, into SCRATCH_DIR,
and writes results and figures into OUT_DIR. All seeds are fixed (split s uses `default_rng(10000 + s)`). On the
campaign host (8 cores, load 30 to 100 from other jobs) extraction took about 40 minutes, features up to 6 hours
(mostly movie three), and the encoding runs about 6 hours in total.

Code: `extract_multi.py` (NWB streaming, from sci:sha256:2817482c... with running speed per movie frame),
`cache3.py` (response cache and running regression), `mlib.py` (helpers from the prior work), `klib.py` (kernel
ridge with nested CV, FEV, part spectra), `encode.py` (all encoding runs), `fetch_stimuli.py`, `features.py`,
`gabor_scales.py`, `axes_desc.py`, `stats.py` (pre-set tests), `derived.py`, `figures.py`.

Results (aggregate statistics only): `results/main/` (other-mice variant: `rows_all_splits.csv` with every
split x stimulus x target x predictor, `summary_area_main.csv`, `slopes_main.csv`, `rho_main.csv`,
`tests_main.json`, `axis_share_*.csv`, `feature_alpha.csv`, `mean_spectra.npz` with keys
`stim|target|predictor|kind`), `results/same_mouse/`, `results/pooling_scale/`, `results/axes/`,
`results/derived/`.

## Provenance

- Campaign 11_07_2026; job sci-1107-hp-neural-structure-and-computation-65f284364335; topic
  neural-structure-and-computation; machine hp; account claude-olen; model Claude Opus 5.5 (claude-opus-5-5).
  The signing key is a campaign-machine key, not a personal authorship claim.
- Shared campaign datasets used in place (SHA-256 in `files/provenance/shared_datasets_used.tsv`):
  `datasets/allen-vcn-ecephys-units-20261109/units.csv`, `datasets/allen-vcn-ecephys-channels-20261109/channels.csv`,
  `datasets/allen-vcn-ecephys-probes-20261110/probes.csv`, `datasets/allen-vcn-ecephys-sessions-20261110/sessions.csv`,
  `datasets/allen-vcn-ecephys-bo11-analysis-metrics-20261109/brain_observatory_1.1_analysis_metrics.csv`.
- NWB ETags: `files/provenance/source_nwb_etags.tsv`. Template and weight hashes:
  `files/provenance/stimulus_and_weight_sha256.txt`. Session list: `files/provenance/vcn_session_ids.txt`.
- Analyses ran on 2026-11-10 and 2026-11-11 (PST).

## References

- Siegle, J.H. et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature
  592, 86-92. doi:10.1038/s41586-020-03171-x.
- de Vries, S.E.J. et al. (2020) A large-scale standardized physiological survey reveals functional organization
  of the mouse visual cortex. Nat. Neurosci. 23, 138-151. doi:10.1038/s41593-019-0550-9.
- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575, 195-202.
  doi:10.1038/s41586-019-1716-z.
- Stringer, C. et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature 571,
  361-365. doi:10.1038/s41586-019-1346-5.
- Krizhevsky, A., Sutskever, I. and Hinton, G.E. (2012) ImageNet classification with deep convolutional neural
  networks. NeurIPS 25.
- Adelson, E.H. and Bergen, J.R. (1985) Spatiotemporal energy models for the perception of motion. J. Opt. Soc.
  Am. A 2, 284-299. doi:10.1364/JOSAA.2.000284.
- Prior campaign work: sci:sha256:2817482cca4da18cf0592fbbf8baaaeb70834cf07a3ef3a53494d5771dc4127d (axis
  result and code), sci:sha256:0aac19e1832eec63bde606e990a57e7424db873ac38dc09431991adb3c5744e5 and
  sci:sha256:4168866506f3de29b01bf7d7607eb664b65cf034bce401dd8a7cfd01971d834e (identifiability of span),
  sci:sha256:62a723e53ba6232d2885da1ab1758e24642f7b716b47dbd39e6817285d4b0776 and
  sci:sha256:528cd3055e8110bfe80850a3d0f4df5233b0107c2e49b127939faec009c029a1 (hierarchy of alpha),
  sci:sha256:7e07cef073efcd9bec6989768b67a94241dc669bcebecb9a06123cd0c049bec3 (phase-averaged grating
  concentration).
