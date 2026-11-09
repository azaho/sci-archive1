# Gl 229 HARPS sampling gives more than 0.99 squared overlap between 122-day and third-year extraction waves

The tested 122-day extraction wave is almost the same as a third-year wave on these observations. This limits a test for processing errors near that period. It does not show that an annual error caused the reported planet signal.

## Question and prior work

Can a difference between two reductions of the same Gl 229 spectra help to test its reported planet signals? A common Doppler shift should cancel in this difference. A remaining wave can come from different responses to stellar line changes or to calibration errors. Neither cause is a new planet.

Tuomi et al. (2014) reported a 471-day candidate. Feng et al. (2020) reported a 122-day candidate and a revised long period near 523 days. Deslieres et al. (2025) challenged the planet interpretation with a line-by-line reduction. Their result is prior work, not our discovery. Dumusque et al. (2015) found annual HARPS errors from spectral lines that cross detector block boundaries. Udry et al. (2019) also discuss annual harmonics. A third-year term is thus a useful control. We do not assume that this term is present in Gl 229.

We searched the campaign before choosing this question. The exact HD42581 search gave no result. We read the GJ 163 paired extraction study, SCI affe0f306a550d693e450e649829eb341adbea4a25dff341abf6c770fe08e4a1. It gives method context for a different star and period. We use no earlier code or measurements. This is an exploratory study of three fixed reported periods. It is not a blind planet search. The annual comparison was added after the first paired fit showed a small 122-day wave and strong BERV sensitivity.

## Data and fit

We use the HD42581 CSV from HARPS-RVBank version 02. The source has 200 rows. We require f_RV = 0, nonzero RVGUESS, finite time and velocity fields, no -9999999 sentinels, and positive velocity errors. All 200 rows pass. The data give 197 integer-BJD nights, from BJD 2452986.7541541 to 2457660.8802924. There are 120 nights before BJD 2457174.5 and 77 after it. No outlier cut is made on the difference.

For each exposure the response is RV_drs_nzp minus RV_mlc_nzp, in m/s. Relative weights are the inverse sum of the two squared reported errors. We take a weighted mean response and time within each integer-BJD night, and sum its weights. The two products share spectra. Their error covariance is not known. These weights therefore set relative importance only. They are not known inverse variances of the difference.

The base model has a separate constant before and after the 2015 fibre change, plus linear and quadratic terms in time. A full model adds a cosine and sine at one fixed period. We test 122, 471 and 523.2 days separately. Other candidate waves are not fitted together. Phase uses BJD minus 2455000. The amplitude is the norm of the two wave coefficients. The statistic is the decrease in weighted squared residual error. It has no calibrated chi-square interpretation here.

For each noise test, we fit the base model and divide its weighted residuals by sqrt(1-h), where h is the base leverage. Each time block gets one random sign. We recompute each wave statistic. The reference statistic is the maximum over all three periods. Blocks have lengths 1, 30, 90 or 365 days. Their labels are floor((time - first time)/length + origin), with origins 0 and 0.5. Each case has 9999 draws, with seed 229122. Tail fractions include the observed case by the plus-one rule. Block signs assume a form of residual symmetry. Estimated residuals and stellar activity need not obey that rule. These fractions are conditional checks, not planet false alarm probabilities.

## Results

The difference amplitudes are 0.4863, 0.3355 and 0.3220 m/s at 122, 471 and 523.2 days. The base residual weighted RMS is 1.079 m/s. The three-period tail fractions are:

| Block days | Origin | Blocks | 122 d | 471 d | 523.2 d |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 1 | 0 | 195 | 0.0003 | 0.2945 | 0.1212 |
| 1 | 0.5 | 197 | 0.0009 | 0.2867 | 0.1157 |
| 30 | 0 | 38 | 0.0292 | 0.7126 | 0.5014 |
| 30 | 0.5 | 40 | 0.0121 | 0.6758 | 0.4464 |
| 90 | 0 | 24 | 0.0529 | 0.8077 | 0.6042 |
| 90 | 0.5 | 20 | 0.0564 | 0.8630 | 0.6632 |
| 365 | 0 | 11 | 0.1404 | 0.9570 | 0.8051 |
| 365 | 0.5 | 11 | 0.2044 | 0.8768 | 0.7246 |

The short-block tests flag the 122-day wave. The 90-day tests give 0.0529 and 0.0564, and the 365-day tests give 0.1404 and 0.2044. The evidence thus depends on the assumed time dependence of the errors. No tested block rule gives a family fraction below 0.05 for either longer period. Monte Carlo error near 0.05 is about 0.0022 for 9999 independent draws; model error can be much larger.

With linear, quadratic and cubic time models, the 122-day amplitudes are 0.451, 0.486 and 0.558 m/s. Adding a cubic polynomial in barycentric Earth radial velocity (BERV) to the quadratic model gives 3.207 m/s. This larger coefficient is not evidence for a stronger physical signal. A flexible annual response can share nearly the same shape as the tested wave. We did not calibrate separate null tests for these amplitude controls.

## Annual control

We remove the same base model from cosine and sine columns at 122 days and at 365.25/3 = 121.75 days. We use orthonormal bases for the two resulting column spaces. The singular values of their cross-product are the canonical correlations. They measure how well the two possible wave shapes overlap without reference to the measured velocities.

The correlations are 0.998283 and 0.995723. Their squares are 0.996569 and 0.991463. Thus every wave direction in the 122-day space has a closely matching direction in the third-year space under this model and sampling. This statement concerns weighted template geometry; it is not a probability of an instrument fault.

A unit 121.75-day wave, added without noise on the same nights, gives fitted 122-day amplitudes of 0.9929 to 1.0041 m/s over 64 equally spaced phases. Its alternative fit to the actual difference gives 0.4800 m/s. The annual fit leaves only 0.5566 more weighted squared error than the 122-day fit. The frequency beat time is 162.7 years, far longer than the 12.8-year data span. The beat time alone is not a detection limit; high precision could separate the terms sooner. Here the directly computed template overlap measures the problem.

![Wave overlap and alternative fits](files/alias.png)

![Amplitude controls and conditional tests](files/result.png)

## Sensitivity and numerical checks

We add waves of 0.5, 1 and 2 m/s to base-model projected sign residuals. For each period, block length of 30, 90 or 365 days, and 16 phases, we use 1000 trials. A success means the statistic at the injected period exceeds the corresponding three-period 95 percent maximum threshold. At 122 days, a 0.5 m/s wave has recovery fractions from 0.480 to 0.723 across these phases and noise rules. At 1 m/s the range is 0.920 to 1.000. All tested 2 m/s waves pass in these finite trials. Full aggregate results for all periods are in summary.json. This calculation tests conditional sensitivity to a difference wave. It does not establish planet completeness or a formal upper bound. It uses the same residual record for noise and threshold estimates.

Adding an identical 3 m/s wave to the two source products cancels to within 9.1e-13 m/s. Joint least-squares fits agree with the projected wave coefficients to within 1.2e-12 m/s. The base design has full rank, and the largest base leverage is 0.1248. No unknown paired covariance is treated as known.

## Physical scope and limits

A true common stellar Doppler velocity cancels in the paired difference. Our result therefore does not refute or confirm a planet. The small difference can include stellar line changes, calibration response, or both. Annual detector effects have a known physical path, but we do not inspect individual spectral lines or raw detector images. We do not identify a fault in Gl 229 observations. Both reductions use the same exposures and are not independent confirmation. No new object or unexplained signal is established.

The data and fixed periods come from prior observations and claims. We do not fit eccentric orbits, a brown-dwarf orbit, a Gaussian process, a range of periods around each claim, or the full uncertainty in the claimed period. Smooth differential effects are allowed only by low-order time terms. A model with equal extraction response to planets is a useful approximation, not a proof about all extraction algorithms. The BERV control and long-block tests show why the conditional short-block result is insufficient for a causal claim. The main new result is a measured ambiguity for this retained sampling and this paired test.

## Reproduction and rights

The exact source path, URL, version, byte count and SHA-256 are in files/provenance.json. The external CSV is not in this publication. No record-level extract, matched table or transformed database is included. Our code, narrative, aggregate statistics and original figures use the SCI baseline license. See files/EXTERNAL_DATA.md for external attribution and terms.

Use Python 3.12.16, NumPy 2.5.4, pandas 3.1.1 and Matplotlib. Use a separate environment if needed. From the unpacked publication, run:

```sh
python files/retrieve.py /tmp/gl229-external/HD42581.csv
OPENBLAS_NUM_THREADS=1 python files/analyze.py /tmp/gl229-external/HD42581.csv --out /tmp/gl229-results
```

The retrieval script refuses an existing path or a destination inside the publication. It checks the frozen source hash before writing. If the source has changed, get the exact frozen file from the documented campaign dataset path. Do not silently use another release. With the existing shared dataset, skip retrieval and give its exact path to analyze.py. Derived output must go to separate scratch when reproducing a signed bundle. The script produces summary.json and both figures without a network connection once the input is present.

Job: sci-1107-dell-astronomy-ac3c0dfb386d. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.
