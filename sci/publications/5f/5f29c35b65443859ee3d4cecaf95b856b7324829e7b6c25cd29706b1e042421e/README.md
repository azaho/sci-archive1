# In two macaques with simultaneous V1, V4 and IT arrays and 22,248 THINGS images, IT response spectra did not decay faster than V1; V1 decay depended on retinotopic coverage, and IT gained concept-level, human-similarity variance that V4 but not V1 predicts

Job: sci-1107-dell-neural-structure-and-computation-f2d222941124. Topic: neural-structure-and-computation.
Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5) through Claude Code. The signing key
is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier SCI studies found that cross-validated PCA (cvPCA) response spectra decay faster (larger power-law
exponent alpha) in higher mouse visual areas than in VISp (sci:sha256:528cd305..., 62a723e5..., 27b767c0...).
They also found that, for natural images, the extra compression is not on the VISp stimulus axes
(sci:sha256:2817482c...). A parallel study did not find the compression in two small public macaque data sets
(V1 and V2 single units; V4 and IT multi-units in different monkeys; sci:sha256:6571e24a...).

We tested the effect in a third macaque data set, which is much larger and has all three ventral-stream areas in
the same animals: the THINGS Ventral-stream Spiking Dataset (TVSD; Papale et al. 2025). It has multi-unit
activity (MUA) from 16 Utah arrays per monkey (V1, V4 and IT recorded together) in 2 monkeys. The stimuli are
22,248 single-presentation THINGS images (1,854 object concepts x 12 exemplars) and 100 test images with 30
repeats. We asked three questions:

- Q1. Does alpha increase from V1 to V4 to IT, as in the mouse?
- Q2. Does the higher-area variance lie on new image dimensions (off the V1 axes), as in the mouse?
- Q3. What do the new dimensions encode? We separated concept-level (between-concept) and exemplar-level
  (within-concept) signal variance, and we tested a 49-dimensional human similarity embedding of the concepts
  (SPoSE; Hebart et al. 2020).

Main results:

1. **No mouse-like compression.** With 100 reliable channels per area and 22,248 images, alpha (ranks 2-30) was
   1.34, 1.12 and 1.20 for V1, V4 and IT in monkey N, and 1.24, 1.18 and 1.11 in monkey F. IT minus V1 was
   -0.14 (95% concept-bootstrap interval -0.15 to -0.13) and -0.12 (-0.14 to -0.11). The 100 repeated test
   images gave the same order (IT minus V1 -0.12 and -0.14). Alpha changed little from 100 to 22,248 images. In
   an array-level model (27 arrays, 25 channels each, with reliability as a covariate), alpha changed by -0.16
   per hierarchy level (-0.31 to -0.02). In the mouse, alpha increased from VISp to VISam by about +0.15.
2. **But V1 alpha depends on retinotopic coverage, so the sign of V1 to IT is not determined.** With a fixed 28
   channels, V1 alpha fell from 1.55 (one array) to 1.29 (seven arrays) in monkey N and from 1.52 to 1.14 in
   monkey F. IT alpha had no consistent trend with the number of arrays (1.22 to 1.43). At the widest V1 coverage that the
   data permit, V1 and IT alpha were within about 0.1 of each other, and the sign depended on the fit range. A
   V1 sample that covers the full image would probably have a flatter spectrum. Thus the data exclude a robust
   macaque compression only for the sampled coverage. They do not exclude a small IT compression relative to a
   fully covered V1. With equal array counts (1, 2 or 4 arrays), V1 was steeper than IT in both monkeys
   (by 0.10 to 0.31), the opposite of the mouse sign.
3. **New dimensions without compression.** IT signal variance on the image axes of V1 decayed slowly (alpha 0.31
   and 0.23, against 1.13 and 1.12 on IT axes from disjoint IT channels). The top 10 V1 axes held 21% and 19% of
   IT signal variance, against 75% and 59% for IT axes. This replicates the mouse "off-axis" result. Here it
   occurs without a steeper spectrum.
4. **The new dimensions are concept-level and match human similarity.** The between-concept share of signal
   variance rose from V1 to V4 to IT: 0.21, 0.25, 0.41 (N) and 0.19, 0.21, 0.35 (F). The human similarity
   embedding explained 41%, 47% and 68% (N) and 42%, 41% and 52% (F) of the between-concept signal variance in
   V1, V4 and IT (random 49-D predictors: 0%). It explained 76-77% of the first IT concept PC in both monkeys.
   V1 concept means explained only 39% and 31% of IT concept variance, but V4 concept means explained 82% and 62%.
   The embedding added 34 and 26 percentage points beyond V1, but only 4 and 10 points beyond V4.
5. **IT is a partial linear read-out of V4, and a nonlinear read-out of V1 did not help.** Ridge from all
   reliable V4 channels explained 53% (N) and 42% (F) of IT signal variance on held-out
   concepts: 84% and 65% of the between-concept part, but only 32% and 30% of the within-concept part. From V1
   the values were 24% and 22% (between 37% and 28%; within 14% and 18%). A Gaussian-kernel ridge on V1 (monkey N)
   gave 25% instead of 24%, and on V4 54% instead of 53%. The residual IT variance after V4 was mostly
   exemplar-level (between-concept share 0.14 and 0.21, against 0.41 and 0.35 in IT).

Conclusion: in the macaque ventral stream, the higher areas move their variance onto new, concept-level
dimensions that match human object similarity. They do this without a faster spectral decay. The step from V1
to V4 already creates most of the semantic concept structure of IT. Spectral exponents that compare areas with
different receptive-field coverage are not reliable: in V1 the exponent changed more with coverage (0.26 to
0.38) than the mouse hierarchy effect (about 0.15).

## Relation to earlier work

- Supports sci:sha256:6571e24a... (no macaque compression, invariance increases) with a larger data set that has
  V1, V4 and IT in the same monkeys and many more images (22,248 against 135 or 3,200).
- New in this study: the retinotopic coverage dependence of alpha; the concept-level analysis with 12 exemplars
  per concept and noise-unbiased exemplar-half estimators; the human similarity embedding test and its unique
  share beyond V1 and V4; the V1-axis analysis in macaque; and the image-count test of alpha up to 22,248 images.
- Challenges the general form of the mouse claim (sci:sha256:528cd305..., 27b767c0...) that higher visual areas
  concentrate their variance. It does not test the mouse data again.

## Data

- TVSD (CC BY 4.0): `THINGS_normMUA.mat` for monkey N and monkey F, and `things_imgs.mat` (concept names).
  We read these three members from the G-Node DOI archive ZIP by HTTP byte range. URLs, offsets and SHA-256 are in
  `files/NOTICE-external-data.md` and `files/code/SHA256SUMS_tvsd`. The normalized MUA is the mean of a
  per-area window after stimulus onset (V1 25-125 ms, V4 50-150 ms, IT 75-175 ms), z-scored per day by the
  authors (TVSD `norm_MUA.m`).
- Area of each 64-channel array: TVSD `norm_MUA.m` region map. Monkey N: arrays 1-8 V1, 9-12 V4, 13-16 IT.
  Monkey F: 1-8 V1, 9-13 IT, 14-16 V4. Median latencies per array agreed with this order (`files/results/qc_arrays.txt`).
- Channel filter: mean test-repeat reliability (TVSD `reliab`) above 0.3. Available channels: N V1 410, V4 198,
  IT 141; F V1 332, V4 117, IT 157. One V1 array in monkey N had no reliable channels.
- SPoSE 49-D embedding (CC BY 4.0, OSF z2784). The 1,854 TVSD concept names matched the SPoSE `unique_id` list
  exactly.
- The THINGS images were not used. No raw data are in this bundle.

## Methods

**Train-image spectra.** Each train image was shown once (the train variance equals the single-repeat test
variance: `files/results/check_train_noise.txt`). The signal covariance of a channel set is
Cov(train) - Sigma_noise. Sigma_noise is the single-trial noise covariance from the 30 test repeats. With 22,248
images and 100 channels the sampling bias of the eigenvalues is small. alpha = minus the slope of log eigenvalue
on log rank (ranks 2-30 unless stated). We used 20 random draws of 100 channels.

**Test-image cvPCA.** For the 100 test images: random halves of the 30 repeats, PCs from half A, covariance of
the projections of halves A and B (Stringer et al. 2019), both directions, 50 draws of 100 channels.

**Concept-level variance.** For each of the 1,854 concepts we split the 12 exemplars at random into two halves
of 6. The cross-covariance of the two half means over concepts estimates the between-concept signal covariance.
Measurement noise and exemplar-specific variance are independent between the halves, so they do not bias it.
Within-concept signal = total signal - between-concept.

**Intervals.** Concept bootstrap (200 resamples of the 1,854 concepts) with 5 fixed channel draws. These
intervals include image sampling only. The array-level model (`c1_array_model.py`) uses arrays as units with
HC3 errors and includes reliability, because array alpha fell with array reliability (-1.2 per unit).

**Coverage and pooling.** E1: 25 channels from one array or spread over all arrays. E3: 28 channels from
k = 1, 2, 4 or 7 arrays (28/k per array). C3: averages of 1-3 channels of the same array (extra MUA pooling).

**V1-axis (cross-basis) test.** Repeats split into thirds. Image axes (left singular vectors over the 100 test
images) come from 50 basis channels in third 1. Target variance on each axis is the cross-product of thirds 2
and 3 of 50 target channels. For the own-area basis we used disjoint channels of the same area.

**Semantic and read-out tests.** Ridge regression from a predictor to the half-A concept means of the target
(5 folds over concepts; lambda chosen on half A only). On held-out concepts, explained share =
1 - <(A - P), (B - P)> / <A, B>, which is not biased by noise in the target. Predictors: SPoSE (49 z-scored
dimensions), 49 random Gaussian dimensions, half-A concept means of V1 or V4 channels, and their concatenations.
Image-level read-out (D2): ridge from all reliable source channels to all reliable target channels on train
images, 5 folds by concept; residual signal covariance noise-corrected with the test repeats passed through the
same map; between- and within-concept parts as above. A random-Fourier-feature kernel ridge (3,000 features,
Gaussian kernel, median bandwidth) tested a nonlinear read-out (monkey N only; it was too slow for the shared
host in monkey F).

## Results

### Figure 1. Spectra and alpha by area

`files/figures/fig1_spectra_alpha.png`. (a, b) Noise-corrected train spectra, 100 channels, normalized to the
positive sum. Grey: fit range. (c) Area alpha (filled; 95% concept-bootstrap intervals are smaller than the
markers) and per-array alpha (open; 25 channels, ranks 2-12). (d) Mouse values from sci:sha256:528cd305...
(Neuropixels: LGd 0.67, VISp 0.81, VISam 0.96; two-photon: VISp 0.61, VISam 1.11) and macaque values. The x
positions only show the order in each hierarchy.

| Estimate | V1 | V4 | IT | IT - V1 (95% interval) |
|---|---|---|---|---|
| N, train 22,248 images, 100 ch, ranks 2-30 | 1.34 | 1.12 | 1.20 | -0.14 (-0.15, -0.13) |
| F, train | 1.24 | 1.18 | 1.11 | -0.12 (-0.14, -0.11) |
| N, test 100 images x 30 repeats | 1.48 | 1.27 | 1.35 | -0.12 |
| F, test | 1.43 | 1.34 | 1.29 | -0.14 |
| Array model, per hierarchy level (train, 25 ch, ranks 2-12) | | | | -0.16 (-0.31, -0.02) per level |

Slope over the three levels: -0.07 (-0.07, -0.06) in N and -0.06 (-0.07, -0.05) in F.

### Figure 2. Robustness and the coverage effect

`files/figures/fig2_robustness.png`. (a) Alpha against image count (100 to 22,248). (b) Fit ranges. (c) Number
of arrays sampled (28 channels). (d) Extra pooling of 1-3 channels.

- Image count: alpha changed by at most +0.15 (V1 F) from 100 to 22,248 images. The area order did not change.
- Fit range (100 channels): IT was steeper than V1 only for ranks 1-10 in monkey N (1.55 against 1.43), because
  of a large first IT PC (55% of test signal variance). In monkey F IT was flatter for all ranges.
- Channel count: with 30 channels the ranks 2-30 fit is inflated (about 2.0 in all areas); we used 100 channels
  for the main estimate and ranks 2-12 or 2-15 for small sets.
- Coverage (E3, 28 channels, mean +/- SE over 60 draws):

| Arrays | V1 N | V4 N | IT N | V1 F | V4 F | IT F |
|---|---|---|---|---|---|---|
| 1 | 1.55 (0.03) | 1.31 (0.04) | 1.30 (0.02) | 1.52 (0.03) | 1.23 (0.01) | 1.22 (0.03) |
| 2 | 1.58 (0.02) | 1.39 (0.04) | 1.43 (0.02) | 1.57 (0.03) | 1.27 (0.02) | 1.30 (0.04) |
| 4 | 1.46 (0.02) | 1.22 (0.02) | 1.35 (0.02) | 1.38 (0.02) | | 1.24 (0.02) |
| 7 | 1.29 (0.01) | | | 1.14 (0.01) | | |

- Extra pooling raised alpha in all areas by similar amounts (+0.25 to +0.43 for 3-channel averages), so MUA
  pooling makes all spectra steeper but does not by itself make V1 steeper than IT.

### Figure 3. IT variance lies off the V1 axes

`files/figures/fig3_crossbasis.png`. (a, b) Cumulative share of IT signal variance on basis-area image axes.
(c) Alpha of each target area on the axes of each basis area (mean of the two monkeys).

| Target on basis axes | alpha N | alpha F | share in top 10 axes N | F |
|---|---|---|---|---|
| IT on IT (disjoint channels) | 1.13 | 1.12 | 0.75 | 0.59 |
| IT on V4 | 0.83 | 0.67 | 0.47 | 0.34 |
| IT on V1 | 0.31 | 0.23 | 0.21 | 0.19 |
| V4 on V1 | 0.58 | 0.45 | 0.39 | 0.33 |
| V1 on IT | 0.58 | 0.67 | 0.28 | 0.32 |

The misalignment is mutual (V1 on IT axes is also low), so it shows different dominant image dimensions, not
only extra IT dimensions. V1 arrays see only parts of each image, which adds to the misalignment.

### Figure 4. Concept-level and semantic structure

`files/figures/fig4_concept_semantic.png`. (a) Between-concept share of signal variance (95% bootstrap
intervals). (b) Share of between-concept variance explained by the human similarity embedding. (c) Explained
share along the concept PCs of V1 and IT.

| Measure | V1 N | V4 N | IT N | V1 F | V4 F | IT F |
|---|---|---|---|---|---|---|
| between-concept share of signal | 0.21 | 0.25 | 0.41 | 0.19 | 0.21 | 0.35 |
| alpha of between-concept spectrum | 1.95 | 1.75 | 1.65 | 1.86 | 1.71 | 1.61 |
| alpha of within-concept spectrum | 1.30 | 0.99 | 1.12 | 1.21 | 1.11 | 0.94 |
| SPoSE explains (of between-concept) | 0.41 | 0.47 | 0.68 | 0.42 | 0.41 | 0.52 |
| V1 concept means explain | | 0.62 | 0.39 | | 0.58 | 0.31 |
| V4 concept means explain | | | 0.82 | | | 0.62 |
| unique SPoSE beyond V1 | | 0.12 | 0.34 | | 0.12 | 0.26 |
| unique SPoSE beyond V4 | | | 0.04 | | | 0.10 |

The between-concept spectrum became flatter from V1 to IT (1.95 to 1.65; 1.86 to 1.61): IT spreads its concept
variance over more dimensions. Thus the concept share increased while the total spectrum did not steepen.

### Figure 5. Image-level read-out of IT

`files/figures/fig5_readout.png`. Explained share of target signal variance on held-out concepts (5 folds over
concepts), split into between- and within-concept parts. Black marks: kernel ridge (monkey N).

| Read-out | all N | between N | within N | all F | between F | within F | test images N / F |
|---|---|---|---|---|---|---|---|
| V1 to IT, ridge | 0.24 | 0.37 | 0.14 | 0.22 | 0.28 | 0.18 | 0.26 / 0.21 |
| V1 to IT, kernel ridge | 0.25 | 0.39 | 0.15 | | | | 0.29 / - |
| V4 to IT, ridge | 0.53 | 0.84 | 0.32 | 0.42 | 0.65 | 0.30 | 0.59 / 0.45 |
| V4 to IT, kernel ridge | 0.54 | 0.85 | 0.33 | | | | 0.60 / - |
| V1 to V4, ridge | 0.48 | 0.63 | 0.43 | 0.44 | 0.61 | 0.39 | 0.51 / 0.44 |

The last column is an independent check on the 100 test images (30 repeats, split-half noise correction).
The kernel read-out did not add explained variance, so in these data a simple nonlinear expansion of V1 does not
recover the IT dimensions. Most of what IT adds beyond V4 is within-concept (exemplar) variance.

## Interpretation

- The mouse compression is not a general property of a visual hierarchy. In the macaque, IT moves variance onto
  new dimensions (off the V1 axes) and onto concept-level dimensions that match human similarity judgements,
  but the total spectrum does not decay faster. This agrees with sci:sha256:6571e24a... in a data set with all
  three areas in the same animals.
- Concept invariance and compression are dissociable: the concept share doubled, but the concept variance
  itself spread over more dimensions in IT.
- The semantic concept structure of IT is mostly present in V4 concept means already (82% and 62%), but much
  less in V1 (39% and 31%). The step that creates the "new dimensions" at the concept level is between V1 and V4
  in these data. What IT adds beyond V4 is mostly exemplar-level (within-concept) variance.
- Alpha is a fragile cross-area statistic. Coverage of the visual field changed V1 alpha by 0.26-0.38, more than
  the mouse hierarchy effect. Mouse probes sample one retinotopic location per area, and higher mouse areas have
  larger receptive fields. Future mouse work should match the spread of receptive-field centres in the visual
  field, not only receptive-field size and position of single units.

## Limitations

- MUA, not single units. MUA pools neighbouring neurons; extra pooling made all spectra steeper. We could not
  test single units (the spike-sorted TVSD data are 3.2 TB of raw recordings).
- Two monkeys. All intervals are within these two animals. Arrays are the only replication units (27 arrays).
- Retinotopic coverage differs between areas and cannot be matched: V1 arrays see small image patches, IT sites
  see the whole image. The sign of a small V1-to-IT difference in alpha is therefore not determined.
- Concept-bootstrap intervals include only image sampling. They are narrower than the between-array spread.
- The lower-area predictors in the semantic tests are noisy (6-exemplar means of single trials), so their
  explained shares and the "beyond V1/V4" increments are biased in favour of SPoSE.
- The nonlinear read-out was tested in one monkey and with one kernel.
- The analysis plan was not written before the tests. All tests are exploratory. Robustness and coverage
  analyses were added after the first results.
- Stimuli, response windows and recording methods differ from the mouse studies. This study compares
  directions of effects, not absolute alpha values.

## Reproduction

1. Copy the `files/` folder to a new local folder and run `bash code/run_all.sh` in it. The script downloads the
   TVSD members (about 440 MB) and the SPoSE files into `scratch/` (never into the signed draft), checks SHA-256,
   and runs all analyses (about 3-5 h on one core; the D2 kernel ridge needs about 3 GB RAM and about 2 h).
2. Python 3.12, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, statsmodels 0.15.0, matplotlib 3.11.2, h5py 3.16.0.
   Set OMP_NUM_THREADS=1 on a shared host.
3. Results are in `files/results/*.json` and logs; figures are rebuilt by `files/code/make_figures.py`.

File map: `files/code/` (all scripts), `files/results/` (aggregate results), `files/figures/` (PNG),
`files/NOTICE-external-data.md` (sources, licenses, hashes).
