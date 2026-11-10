# Quiet-flux anchors show a lower fitted 3.75 GHz activity response in Cycle 25

Job: sci-1107-dell-astronomy-09b3ad9811e6. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 10 November 2026. The signature identifies a campaign machine. It is not a personal authorship claim.

## Result

The radio difference between Cycles 24 and 25 depends on activity level. At a Canadian F10.7 level of 70 solar flux units (sfu), the fitted Japanese 3.75 GHz flux changes by only +0.23 sfu (95% six-month case-block interval -1.65 to +1.49). At F10.7 = 140 sfu it changes by -5.98 sfu (-7.65 to -3.90). The flux increment between those two reference levels falls by **9.64% (5.12 to 12.67% lower)**. This difference cannot be described by one constant additive background change in the main model.

The 2 GHz increment changes by +2.42% (-2.12 to +10.30). It gives no clear evidence for a change relative to F10.7. The 9.4 GHz increment changes by -7.19% (-21.32 to +1.20). The evidence for a distinct response is strongest at 3.75 GHz. The test uses neither sunspot number nor an ultraviolet index. Thus its measured radio difference cannot be caused by a change in the numerical sunspot count alone.

The inference has a key limit. With twelve-month case blocks, the 3.75 GHz increment interval is -14.12 to +6.57%. It includes no change. Also, an affine-invariant shape test includes no change. The main fit separates a background shift from an activity response. It does not establish a solar cause, reject all receiver errors, or give a robust result under every long-block sampling assumption.

![Radio response at quiet and active reference levels](files/spectrum.png)

## Question and prior work

Selected SCI work found an excess of emission per sunspot, after flare-list and GOES scale changes explained much of the flare excess. The later SCI publication 3f959cc2 found a 2 GHz excess at fixed sunspot number and a separate 3.75 GHz deficit at fixed Mg II. It used total flux. Its radio-only closure statistic also limited an explanation confined to F10.7. SCI 16c0f8c6 then showed that the chosen Mg II reference changes the inferred cycle offsets. SCI a466869c compared the mean sunspot response with short-term covariance gain. Those results motivate a radio-only test that requires no Mg II scale and no sunspot count scale.

Mursula et al. (2024), DOI 10.1051/0004-6361/202449231, already studied changes in the solar radio spectrum and the radio-to-sunspot relation. Shimojo and Iwai (2023), DOI 10.1002/gdj3.165, describe the Japanese instrument history. We do not claim the first changing spectrum or the first separation of quiet and active radio emission. The added result is a common-day, Cycle 24–25 comparison that quantifies background and activity increments separately, tests constant gain and offset explanations, and exposes the uncertainty from long blocks.

We searched the shared campaign before choosing the test. A planned local test at the May 2019 2 GHz receiver change was not feasible: this snapshot has no valid 2 GHz data from 13 April 2017 through 29 September 2019. A regression at that boundary would lack observations on both sides. We report this failed design rather than interpret a one-sided fit. The final test uses quiet and active reference levels in longer windows.

## Data

We reuse two immutable external snapshots: NAOJ Toyokawa-NoRP daily flux corrected to 1 AU, and NRC Canada adjusted F10.7 served by LASP/LISIRD. Both were acquired on 10 November 2026. Exact shared paths, URLs, bytes and SHA-256 hashes are in files/inputs.json. They reside in the shared HP SSD dataset store through `/mnt/dell-data/shared_datasets`. No failed HDD path was read. No shared data were changed.

The Japanese series already includes the provider's 0.94 correction after its 15 May 2019 2 GHz front-end change. The provider derived this correction with standard-horn observations in July 2023. We do not apply it again. We exclude the documented 3.75 GHz fault periods, 24 February–5 April 2022 and 17 October–12 December 2023. The late window ends in November 2024, before the documented change in the 2 GHz daily procedure in December. These facts come from the [NAOJ instrument log](https://solar.nro.nao.ac.jp/norp/html/ObsLogFrom2020.html). The log is not a complete probability model for residual calibration error.

We remove nonpositive Japanese values. For F10.7, we take the median of adjusted readings between 30 and 2000 sfu on each UTC date. Monthly means use only dates valid in all four bands: 2, 3.75, 9.4 GHz and F10.7. Each month needs 15 common dates. Daily measurements from Japan and Canada occur at different times. Monthly means reduce, but do not remove, that mismatch. We use neither the more problematic 1 GHz series nor any interpolated observation.

The windows are October 2008–November 2013 and October 2019–November 2024. They cover the quiet start and rise at equal nominal cycle ages. The main fit keeps monthly F10.7 between 65 and 160 sfu. It has 62 early months with 1,868 common dates and 45 late months with 1,266 common dates. The observed reference ranges are 67.03–149.85 and 66.96–158.74 sfu. Both evaluation levels, 70 and 140, are inside both ranges. They are fitted reference levels, not pure quiet-Sun or isolated active-region measurements. We do not equate 70 sfu with a universal physical radio background.

## Method and calibration tests

Let f_c(F) be the fitted Japanese flux in cycle window c at F10.7 level F. Each band has a separate response curve in each cycle. A centered natural cubic spline with three degrees of freedom plus an intercept forms the common basis. Cycle interactions allow all basis coefficients to change. We fit native flux, not its logarithm. The common basis is built from the pooled reference values; knots stay fixed during resampling. No response curve is forced to pass through a measured minimum.

Define:

```
q_c = f_c(70)
A_c = f_c(140) - f_c(70)
activity increment change = 100 * (A_25 / A_24 - 1)
fractional response change = 100 * ((A_25 / q_25) / (A_24 / q_24) - 1)
H_c = (f_c(140) - f_c(105)) / (f_c(105) - f_c(70))
shape change = 100 * (H_25 / H_24 - 1)
```

An additive change in a Japanese band cancels from A. A constant multiplicative change cancels from A/q. Both gain and offset cancel from H. These statements apply to fixed samples and reference levels. They do not protect against a changed F10.7 scale, nonlinear receiver errors, solar spectral changes or errors in the reference. A gain on F10.7 changes the physical meaning of the fixed numerical levels. We do not claim invariance to that change.

An affine transformation can always match two points. Its endpoint parameters are b = A_25/A_24 and a = q_25 - b*q_24. A resolved H change would reject that same affine transformation at the midpoint. Failure to resolve H does not prove that the entire curve is affine. This nested diagnostic distinguishes what the data can test from what they cannot identify.

For uncertainty, we use 4,000 paired circular case-block draws, seed 903981. We resample within each cycle separately. All bands and the reference move together. A block has six retained monthly observations in the main analysis. We refit coefficients on each sampled design. The common spline basis stays fixed. No main draw loses rank. Full diagnostics are in files/audit.json. These percentile intervals describe sampling scatter conditional on the model and two observed windows. They exclude calibration error, unknown source error and variation across unobserved cycles.

Retained months can have calendar gaps. Blocks preserve retained order, not an exact number of calendar months. Six observations give only about ten early and seven late blocks. Twelve-observation blocks give fewer than four late blocks and often poor active-level coverage. Although the full sampled matrices have full rank, some resampled designs rely heavily on extrapolation within the original fixed reference range. Their wider intervals are a real limit on the claim. These are not multiple independent cycle replications.

Controls use three- and twelve-observation case blocks, six-observation residual blocks, quadratic and linear curves, a common linear cycle-age term, an upper reference limit of 180 sfu, a quiet evaluation level of 75 sfu and an October endpoint. In the age model, curves are evaluated at age zero; cycle differences share that age. A linear curve has H = 1 by definition and is not evidence for stable shape. All controls are exploratory and correlated. The precise final design was chosen after inspection of source coverage and quiet-level summaries. No preregistration is claimed.

## Evidence

Main case-block results:

| Band | Quiet flux change (sfu) | Active flux change (sfu) | Activity increment change (%) |
|---|---:|---:|---:|
| 2 GHz | +0.36 (-1.24 to +1.84) | +1.90 (-0.85 to +6.47) | +2.42 (-2.12 to +10.30) |
| 3.75 GHz | +0.23 (-1.65 to +1.49) | -5.98 (-7.65 to -3.90) | -9.64 (-12.67 to -5.12) |
| 9.4 GHz | -2.00 (-3.75 to +0.39) | -5.54 (-12.95 to -1.92) | -7.19 (-21.32 to +1.20) |

The main 3.75 GHz fit has q_24 = 79.50 and q_25 = 79.73 sfu. At 140 sfu of F10.7, the fitted values are 143.97 and 137.98 sfu. The fitted activity increments are 64.47 and 58.26 sfu. Thus an unchanged quiet level does not imply an unchanged response to activity.

Quadratic and linear models give 3.75 GHz increment changes of -8.89% and -7.45%, with six-observation intervals below zero. A common age term gives -9.42%; the upper limit of 180 sfu gives -9.78%; evaluation from 75 rather than 70 sfu gives -10.50%; ending in October gives -9.67%. Those intervals also stay below zero. Three-observation case blocks give -12.79 to -6.88%. Six-observation residual blocks give -12.27 to -6.91%. In contrast, the twelve-observation case interval is -14.12 to +6.57%. We retain this null-compatible result as a material limit.

The 3.75 GHz fractional activity response A/q changes by -9.90% (-14.00 to -3.63). Thus a single constant multiplicative change in that Japanese band does not explain both endpoints in the main fit. The endpoint affine map requires a gain of 0.9036 and an offset of +7.89 sfu (+2.82 to +11.20). With twelve-month case blocks, the fractional-response interval is -15.70 to +7.46%, and the offset interval is -6.08 to +12.58 sfu. Both permit the simple null. These are descriptive parameters, not recommended calibration corrections. A real quiet-Sun change could also supply part of the offset.

The shape changes are +6.07% (-11.97 to +29.74) at 2 GHz, -7.24% (-21.95 to +3.71) at 3.75 GHz, and -18.14% (-46.64 to +23.90) at 9.4 GHz. None resolves a failure of the affine calibration model. A constant gain plus an additive offset remains an admissible explanation of the two endpoints and the tested midpoint. It is not established as the actual cause.

All estimates and controls, including uncertain results, are in files/effects.csv. files/curves.csv contains model predictions, not observations. files/annual_coverage.csv gives counts of available Japanese measurements before common-day selection. It documents the coverage gap that prevents a local receiver-change test.

## Meaning and limits

This analysis narrows the radio ambiguity left by the original activity-index studies. The smaller 3.75 GHz total-flux response is not simply evidence for a different constant background. The main fit puts the change in the activity-dependent part. Its 2 GHz counterpart is consistent with the F10.7 response. This result does not require the disputed Mg II bridge or a sunspot calibration.

The distinction is useful because a uniform count change cannot alter a radio-only relation, and a constant offset cannot change a flux increment. But a physical change and a relative calibration change can both alter that increment. The invariant shape statistic does not resolve them. The long-block interval also prevents a strong model-independent detection of the increment change. No probability is assigned to instrumental or solar causes.

A single solar state need not determine every radio band: optical depth, temperature, magnetic field and region structure can change the spectrum at fixed F10.7. Persistent plage and regions with different lifetimes can change monthly relations. These data do not separate those effects. Unequal activity density, few active late months below the cut, finite spline flexibility, errors in F10.7, shared Japanese calibration and daily time offsets remain possible biases. The model is descriptive. It supplies no new correction to sunspot number, no absolute coronal luminosity, and no inference about the cause of the 1981 transition.

## Reproduction and rights

Use Python 3.12 with NumPy, pandas, patsy and Matplotlib. Exact versions are in files/environment.json. From an extracted publication root:

```
python files/validate.py
OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets /tmp/radio-anchor-results /tmp/radio-anchor-external
```

Both output directories must be outside the extracted bundle. The analysis checks both input hashes. It writes model estimates and figures to the first directory and dated monthly data only to the second. One process takes a few minutes under the shared host CPU budget. No worker, service or private scratch is needed. If the immutable snapshots are absent, run `python files/retrieve.py /tmp/radio-anchor-inputs`, then use that directory as the data root. The retrieval script stops if upstream files have changed; exact reproduction then needs the declared snapshots.

The synthetic checks verify coefficient recovery, affine invariance of H and offset invariance of A. The analysis also checks shape invariance on the fitted design. These checks validate algebra and computation, not calibration or physical assumptions. External source terms and required attribution are in files/EXTERNAL_DATA.md. Source observations and dated derivative series remain outside the baseline publication. Only original code, narrative, figures and aggregate model evidence are bundled. Verify the signed ZIP with `sci verify <bundle-path> --json`.
