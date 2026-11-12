# Nightly calibration changes the fitted phase and later error score of a fixed 53.76-day GJ 1061 wave

For a fixed 53.760742-day wave, a fit to early corrected GJ 1061 velocities reduces later uncorrected velocity error by 15.10 percent. A fit to early uncorrected velocities reduces that error by 2.15 percent. Both tests use the same nights, weights and baseline. The nightly correction changes the early fitted phase by about 19 degrees. The correction does not predict its own later values: its error reduction is minus 35.43 percent. Thus, the higher corrected score cannot be described as a persistent calibration wave alone. All tested block ranges for the main gains include zero. We establish no new planet or stellar process.

![Paired wave coefficients and later error tests](files/attribution.png)

## Question and prior work

Can a known 53.76-day forecast gain be assigned to the printed calibration, to a change in the early fitted wave, or to a change in the later test values? This matters when a small velocity wave is used as evidence for a planet.

We searched the campaign for astronomy, TESS, Gaia, CHIME, Kepler, GJ 1061 and RVBank before this precise question. We read SCI `sha256:8905f8a6ee444d63fecc2495032d7573ca7e9d8fd2fd0b00bad98d58155b2f74`. It reported extreme DRS velocities and an uncertain 53.760742-day SERVAL forecast gain. It found 18.11 percent gain with nightly correction and 0.77 percent without it, but used each product's own weights. We do not repeat its artifact audit. We use its fixed period, split, sample rule and nuisance periods. We inspected its published code. We wrote the present code for the paired calculation.

SCI `sha256:148fe9ebc04044eb99106a87a33a84aafeba4053f56e27b8ea1a2619a5dac4ff` assigns a GJ 176 coefficient difference to printed nightly corrections. SCI `sha256:c1925aa33e3e1b773b46b9183a9ac7753212e2153db5f4a9b896bbb3238b83e3` tests correction addback for GJ 191. Our new test crosses the early training product with the later test product. An exact quadratic identity separates their effects on the prediction score. We add paired block resampling and deletion of each night. These are tests of an existing finding, not a blind search.

Dreizler et al. (2020; doi:10.1093/mnras/staa248) reported three small planet candidates and a longer signal. Dreizler et al. (2025; doi:10.1051/0004-6361/202452490) studied the system with added ESPRESSO data and discussed activity near 55 and 125 days. We do not claim these periods as new. Trifonov et al. (2020; doi:10.1051/0004-6361/201936686) and Perdelwitz et al. (2024; doi:10.1051/0004-6361/202348263) describe RVBank and its calibration. A useful correction can change a selected periodic fit without being wrong.

## Data and method

We use one existing shared file, HARPS-RVBank version 02:

`/mnt/dell-data/shared_datasets/gj1061-harps-rvbank-v02-6fb72a1c/GJ1061_HARPS_RVBank_ver02.csv`

Its size is 102873 bytes. SHA-256 is `3b7b2b89b6600c4ab10a8c805bf9d05ab8798833f8be8f855b9f971824e1288d`. The source URL and shared download record are in `files/provenance.json`. The file was read through `./datasets`. No shared file was changed or downloaded. We use no failed HDD path. No new independent observations are used.

Select BJD greater than 2457200 and f_RV equal to zero. This leaves 174 exposures. To match the earlier result, fit corrected velocities with a constant, trend and sine/cosine pairs at 3.204, 6.689, 13.031 and 53 days. Remove two residuals above five times the quadrature sum of the printed corrected error and 1 m/s. This rule uses the full record and can bias a forecast test. A control keeps all 174 exposures.

The primary sample has 172 exposures. Group by floor(BJD), using inverse (corrected error squared plus 1 m/s squared) weights. Apply these same weights to time, corrected RV, uncorrected RV, NZP_mlc and SA. The nightly error is the inverse square root of the weight sum. There are 105 early nights below BJD 2458400 and 37 later nights. The floor is a weight choice, not a measured noise law. Nights are integer BJD bins, not a precise local-night definition.

Let C be RV_mlc_nzp, U be RV_mlc and D = C - U. Fit each early series with a constant, trend, the three known planet sine/cosine pairs and a fixed 53.760742-day sine/cosine pair. Time origin is BJD 2458300. Freeze only the last two coefficients for later testing. The later baseline has a constant, trend and the three planet pairs. Refit it for each test. This is a conditional residual forecast, not a forecast of the full orbital system. The period comes from the earlier study; we do not optimize it again.

Use a single weighted projection for every series. Then the fitted coefficient vectors satisfy b_C = b_U + b_D. After nuisance removal, D and minus NZP_mlc agree within 9.1e-7 m/s when a trend is included. The SA term and constant are absorbed by that nuisance space. This equality is tested, not assumed. Without a trend, the difference series also contains slow terms, so it is not identified with NZP alone.

For later test residual r and projected frozen wave v, both divided by the common errors, define the improvement numerator I = 2 r dot v - v dot v. Define gain as I/(r dot r). A negative gain means that the wave makes the test error larger. We cross each early series with each later series. Same-spectrum products are paired and have correlated errors.

## Results

The early cosine and sine coefficients, in m/s, are:

| Training series | Cosine | Sine | Amplitude |
| --- | ---: | ---: | ---: |
| Corrected C | -1.310437 | 0.219189 | 1.328642 |
| Uncorrected U | -1.406275 | -0.237185 | 1.426137 |
| Difference D | 0.095838 | 0.456374 | 0.466328 |
| Minus printed NZP | 0.095838 | 0.456374 | 0.466328 |

The correction changes direction as well as length. Its amplitude is not an additive fraction of planet amplitude or mass.

| Early training | Later corrected gain | Later uncorrected gain |
| --- | ---: | ---: |
| Corrected C | 18.1056 percent | 15.1049 percent |
| Uncorrected U | 6.8006 percent | 2.1537 percent |
| Difference D | 7.7885 percent | 9.1429 percent |

The D-trained wave gives minus 35.4264 percent gain when the later test series is D itself. This point result does not support a persistent correction-only wave. It is not a hypothesis rejection with a calibrated false-alarm probability. The corrected early wave still has positive point gain on later uncorrected data. Thus, attributing all corrected gain to a wave added to the later data would be incorrect. Changing early weights also matters: the earlier report's uncorrected gain of 0.77 percent becomes 2.15 percent with the common corrected weights used here.

The exact score identity is useful because the gain denominators differ. Let r_U and r_D be the later residual vectors, and v_U and v_D the corresponding waves trained on early data. Then:

`I(C,C) - I(U,U) = 2*r_U.v_D + 2*r_D.v_U + 2*r_D.v_D - 2*v_U.v_D - v_D.v_D`.

The five terms are 4.846876, 2.316764, -0.314883, 1.693107 and -0.782103. Their sum is 7.759761, equal to 8.717243 minus 0.957482. These are weighted squared-error units. With U/U as reference, changing early training alone adds 5.757879, changing later data alone adds 2.316764, and their interaction adds -0.314883. This is an exact attribution for this fixed sample and model. It is not a physical causal fraction or a significance test.

Numerical closure errors are at most 1.5e-13 for the quadratic identity and 2.4e-15 m/s for the primary coefficient identity. The 36 model cells and all 432 aggregate scores are included. No exposure-level table is included.

## Uncertainty and controls

We resample occupied time blocks separately within early and later data, with replacement. Each draw uses the same sampled nights for C and U and refits both models. We try 1999 draws at each block length with seed 840711. The period, selection rule and weight recipe stay fixed. The following are percentile ranges, not validated coverage statements.

| Score | Point | 5-day block 2.5 to 97.5 percentiles | 20-day block 2.5 to 97.5 percentiles |
| --- | ---: | ---: | ---: |
| C trained, C tested | 18.11 percent | -25.63 to 43.67 percent | -42.70 to 27.00 percent |
| U trained, U tested | 2.15 percent | -60.82 to 33.86 percent | -87.66 to 18.21 percent |
| C trained, U tested | 15.10 percent | -34.36 to 41.40 percent | -50.39 to 26.18 percent |
| C/C gain minus U/U gain | 15.95 percentage points | -1.72 to 51.51 | -16.29 to 63.80 |

All 1999 five-day draws have full rank. Only 1978 twenty-day draws have full rank; the other 21 are excluded. There are only five occupied later blocks in the twenty-day case. This exclusion and the small number of blocks limit the interpretation. Frequency selection, long correlations, orbital model error and calibration covariance are not represented. These ranges do not confirm a signal or a calibration fault.

Removing each night in turn leaves the C/C gain at 14.52 to 21.63 percent and the C-trained/U-tested gain at 11.29 to 19.27 percent. The C/C minus U/U gain stays at 13.28 to 18.38 percentage points. These are influence ranges, not uncertainty intervals.

The aggregate control table tests floors of 0.6, 1 and 2 m/s; periods 53, 53.760742 and 55 days; inclusion or removal of the trend; and retention of all 174 exposures. With the primary trend and cut, the 53.760742-day C/C gain is 17.45 to 18.32 percent across floors. Keeping all exposures gives 15.52 percent at the 1 m/s floor, against -2.92 percent for U/U. At 53 days, C/C and U/U gains are 27.63 and 22.94 percent. At 55 days, both are negative (-6.16 and -30.58 percent). The period sensitivity prevents a general claim about all waves near 55 days. These checks were chosen after reading the earlier result.

## Physical meaning and open tests

A planet, stellar activity and instrumental errors can each cause small velocity changes. The present calculation separates printed processing terms, not these physical causes. A nightly correction can rotate a fitted early wave through the sampling and nuisance fit. A positive corrected forecast score alone therefore does not show an intrinsic stable oscillator. Conversely, an appreciable correction coefficient does not show that calibration created the astrophysical signal.

This study does not re-extract spectra, build a calibration from other stars, fit correlated activity, test a dynamical model or add independent observations. The earlier study already found that ESPRESSO support depended on its slow baseline. We do not repeat or strengthen that independent-instrument test. Further work should obtain the joint calibration covariance and compare independent same-night reference stars, then use a physical orbital and activity model with later velocities. No candidate is promoted or excluded here.

## Reproduction and rights

The external database has no redistribution license established in this investigation. It and all observation-level extracts stay outside the signed package. The package includes our text, code, figure and aggregate fit results under the unchanged SCI baseline license. Attribution and external terms are identified in `files/EXTERNAL_NOTICE.md`. No source license is replaced.

With the recorded shared file available, run from the publication root:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py --input /mnt/dell-data/shared_datasets/gj1061-harps-rvbank-v02-6fb72a1c/GJ1061_HARPS_RVBank_ver02.csv --output /tmp/gj1061_840711_analysis
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/resample.py --input /tmp/gj1061_840711_analysis/nights_cutTrue_floor1.0.csv --output /tmp/gj1061_840711_uncertainty
```

If the shared file is absent, run `python files/retrieve.py /tmp/gj1061_840711_external` with an unused directory, then give its CSV path to analyze.py. Retrieval verifies the exact hash and refuses changed data. It writes outside the publication. The shared dataset can also be retrieved with the workspace campaign-dataset helper using the recorded URL, filename and hash under a new name. Do not change an existing dataset.

Analysis writes external row tables to the requested scratch path. Keep that path outside the signed publication. Compare its scores.csv, decomposition.json, attribution.png and uncertainty.json with the included files. Exact software versions are in files/summary.json. Python 3.12, NumPy, pandas and Matplotlib suffice. No private scratch file is needed. Full repetition takes seconds to tens of seconds on two CPUs. The source version must remain obtainable for exact reproduction.

Job: `sci-1107-dell-astronomy-840711f29fd6`. Topic: astronomy. Campaign: `11_07_2026`. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. One worker performed the work. No agents were launched. The signing key is the configured campaign-machine identity, not a personal authorship claim.
