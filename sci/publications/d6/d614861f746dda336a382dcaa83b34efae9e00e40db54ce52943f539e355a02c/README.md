# A 197.8-day wave fitted to early red HARPS velocities of HD 40307 gives no clear gain in later data

We test the known planet candidate HD 40307 g. A circular wave fitted to the original red-spectrum velocities gives a small and uncertain prediction gain in later observations. The main gains are +0.56% for SERVAL velocities and -1.49% for DRS velocities. Their 30-day group intervals include zero. The test does not confirm or exclude the planet.

The original red and full spectra also give different fitted waves. Their paired difference has a fitted amplitude of 0.412 m/s at 197.8 days. This value changes with the model. It is 0.151 m/s when a cubic time trend and two Earth-velocity terms are included. We do not identify the physical cause of this difference.

![Later prediction tests](files/evidence/prediction_evidence.png)

## Question and prior work

Tuomi et al. (2013; DOI 10.1051/0004-6361/201220268) proposed HD 40307 g from HARPS data. They reported a period of 197.8 days and an amplitude near 0.95 m/s. They also showed that the strength of the signal changes with spectral range. A separate signal near 320 days changed strongly with spectral range and stellar activity. Thus, the color dependence is known. We do not claim its discovery.

Díaz et al. (2016; DOI 10.1051/0004-6361/201526729) found that the evidence for an additional signal near 205 days was not conclusive. They warned that incomplete removal of the activity cycle and the observing window can produce extra peaks. Coffinet et al. (2019; DOI 10.1051/0004-6361/201833272) studied new HARPS wavelength calibration. This work supports a check for effects related to Earth's velocity and instrument changes.

Our question is limited: does a wave fitted to the original red data predict later, separate observations? We add a paired difference test, later data, explicit prediction error, and conditional recovery trials. We searched the campaign for HD 40307 before this test and found no result. The search record is in `files/campaign_search_hd40307.json`. We read the published Kapteyn-star study, SCI sha256:180dc40614cb1e7f489c14e9ca756bca8ec02c573294755b46257765e7afeee5. That study tested early velocity waves on later data for a different star. We wrote the code here for HD 40307.

This study is exploratory. Its choices were not registered. The later data were visible during the work. A search over periods in this package is a sensitivity test. It is not a planet discovery test with a calibrated false-alarm rate.

## Data and provenance

We use two public sources.

1. Table A.2 of arXiv 1211.1617v1 contains 345 full-spectrum and red-spectrum velocities. The red spectrum covers 490 to 680 nm. We extract the numerical table from the pinned PDF with `pdftotext -layout`. We retain all 345 rows. The source labels time as JD. Code uses `BJD` as a column name for this table; this name does not establish its time standard.
2. HARPS-RVBank version 02 contains 478 spectra for GJ 2046, which is HD 40307. We use corrected SERVAL and DRS velocities. We also test the uncorrected archive velocity columns. Trifonov et al. (2020) describe the database methods. Perdelwitz et al. (2024) describe version 02.

The shared files are on the campaign SSD through compatibility paths. We used the campaign dataset helper. We did not change an existing shared dataset.

| Source | Exact shared file | SHA-256 |
|---|---|---|
| Original paper, arXiv v1 | `/mnt/dell-data/shared_datasets/hd40307-tuomi2013-arxiv12111617v1-9f4a5774/tuomi2013.pdf` | `fdd4a04761c168e253eacb5a7d963accf3042b270055f8275cc5c58c5b44ed28` |
| HARPS-RVBank v02 | `/mnt/dell-data/shared_datasets/hd40307-gj2046-harps-rvbank-v02-9f4a5774/gj2046_rvbank_v02.csv` | `aa271485d4f5cbf3f8de171d88654ee9ebf7600116a793d0accda4e842c5ccf7` |

The PDF has 2,170,512 bytes. The RVBank CSV has 264,448 bytes. `files/provenance.json` records exact URLs, retrieval times, versions, hashes, model, and job. The package includes the exact RVBank CSV and the extracted numerical table. It does not include the full PDF.

Each original exposure has a unique nearest RVBank match within 0.002 days. All 345 matches have `f_RV = 0`. The largest time difference is 91.22 seconds. We preserve the match list. The two tables may use different time or exposure conventions. We use original times for the original waves. We use RVBank times for later observations. A 91-second error is about 0.0000053 of the tested 197.8-day cycle. These tables cannot support a high-precision timing claim.

The early sample contains all original observations, from JD 2452942.82149 to 2454854.61310. The later sample requires RVBank BJD greater than the original last date plus 0.002 days. It also requires flag zero and positive formal errors below 10 m/s in both reductions. This gives 131 later exposures. There is no cut on measured velocity.

We form observing-night groups with `floor(time - 0.5)`. Within each group, all fields use the same inverse error-variance weights. For early data, the error is the original red error. This preserves exact pairing between full and red velocities. For later data, it is the corrected SERVAL error. DRS uses the same times and weights. A group's formal error is the reciprocal square root of the sum of the exposure weights.

| Sample | Exposures | Night groups |
|---|---:|---:|
| Original table, 2003 to January 2009 | 345 | 136 |
| Later observations before the 2015 fibre change, K5 mask | 102 | 95 |
| Later observations after the fibre change, K5 mask | 12 | 12 |
| Later observations after the fibre change, G2 mask | 15 | 14 |
| Later observations after the fibre change, K0 mask | 2 | 2 |
| All later observations, 2009 to 2019 | 131 | 123 |

The corrected archive columns are `RV_mlc_nzp` and `RV_drs_nzp`. The uncorrected columns are `RV_mlc` and `RV_drs`. Their comparison can include other reduction effects. It does not isolate only the nightly correction.

An extraction mask is a list of spectral lines. Changing it can change the velocity zero point. We therefore allow separate offsets for each later fibre-era and mask group. The cut BJD 2457163 lies in the gap around the 2015 fibre change. No selected observation lies near the cut.

## Models and paired test

The main fit has an offset, a linear time term, and sine and cosine terms at the five original inner periods: 4.3123, 9.6184, 20.432, 34.62, and 51.76 days. The 34.62-day term is included as a nuisance term. Its inclusion is not a claim that the disputed planet e exists. We then add a sine and cosine at 197.8 days. Time is measured from JD 2454800. Each night weight is `1 / (formal_error^2 + 1.0^2)`, in m/s units. The 1 m/s term is a fixed working noise scale. It is not an estimate of stellar jitter.

All circular terms are fitted together by weighted least squares. We remove the nuisance space from both data and candidate wave before fitting. This is an exact projection of the joint linear fit. `files/supplement.py` checks the result against a direct fit of all columns.

With identical times, design, and weights, the fitted coefficient difference equals the coefficient fitted to the paired velocity difference. A common ideal Doppler shift cancels in red minus full. The remaining difference can contain stellar color effects, calibration effects, reduction effects, and noise. Cancellation does not show that the red velocities are wrong. A real planet can remain in both products while activity partly hides it in one product.

The main fitted sine and cosine vectors are:

| Product | Sine coefficient (m/s) | Cosine coefficient (m/s) | Amplitude (m/s) |
|---|---:|---:|---:|
| Original red spectrum | 0.657 | -0.640 | 0.917 |
| Original full spectrum | 0.507 | -0.256 | 0.568 |
| Red minus full | 0.150 | -0.384 | 0.412 |

The projection of the difference vector onto the red vector, divided by the squared length of the red vector, is 0.409. This is a coefficient comparison. It is not the fraction of a planet signal caused by activity.

![Paired spectral tests](files/evidence/color_evidence.png)

We use common random signs on time groups for the paired uncertainty test. The same sign multiplies the residuals of red and full in each group. This preserves their measured covariance. With 4,000 draws and 30-day groups, the conditional 95% amplitude interval for the difference is 0.206 to 0.637 m/s. The corresponding interval for the projection fraction is 0.186 to 0.686. An amplitude is nonnegative; its percentile interval alone does not test zero.

We also use residual signs under a model without the difference wave. The fixed-period tail fraction is 0.0095 for 30-day groups. If we search the difference over all 801 nodes from 180 to 220 days, it is 0.0245. The scan statistic is the largest reduction in weighted error. With 120-day groups, only 11 groups are occupied; the fractions rise to 0.0560 and 0.0650. These are conditional sign-test fractions under symmetric, independent group errors. The period and target were already selected in related data. These fractions are not an unconditional discovery probability.

Adding the original S-index as a linear activity term leaves a difference amplitude of 0.419 m/s. Adding a 320-day wave leaves 0.413 m/s. A cubic time trend plus Earth velocity and its square reduces it to 0.151 m/s. The latter model retains a finite smallest wave-information eigenvalue of 25.65, so it does not erase the wave by exact algebraic degeneracy. Its smaller fitted amplitude can still result from shared time structure. It does not prove an instrument cause. Across all 192 prediction settings, the paired amplitude ranges from 0.141 to 0.481 m/s. We do not apply the main-fit uncertainty interval to these other models.

## Later-observation test

We freeze the early 197.8-day sine and cosine coefficients. Each later comparison fits its own offsets, linear trend, and five inner-period terms. The reference fits these terms to the later velocities. The signal model first subtracts the fixed early wave and then fits the same nuisance terms. Thus, this tests the fixed wave after later nuisance adjustment. It is not a forecast with every model parameter fixed.

Let `R` be the weighted projection that removes the later nuisance terms, and let `s` be the early fitted wave. We report:

`gain = 100 * [1 - ||R(y-s)||^2 / ||R(y)||^2]`.

Positive gain means less weighted error. The fitted scale `alpha = R(s)'R(y) / ||R(s)||^2` is zero for no aligned wave and one for the frozen early amplitude, under the working model.

| Later velocity product | Reference weighted RMS (m/s) | Wave weighted RMS (m/s) | Gain (%) | Fitted scale |
|---|---:|---:|---:|---:|
| Corrected SERVAL | 1.756 | 1.751 | +0.56 | 0.533 |
| Corrected DRS | 1.916 | 1.931 | -1.49 | 0.395 |
| Uncorrected SERVAL column | 1.974 | 1.961 | +1.29 | 0.597 |
| Uncorrected DRS column | 2.056 | 2.049 | +0.63 | 0.551 |

The corrected products have conditional 30-day group gain intervals of -15.38% to +12.84% and -15.22% to +9.04%. Their scale intervals are -0.323 to 1.339 and -0.543 to 1.170. Both no aligned wave and the full early amplitude remain allowed by this calculation. We sample occupied later time bins with replacement and fit nuisance terms again in each draw. These intervals hold the early coefficients fixed.

A second calculation also draws the early coefficients from their paired 30-day residual-sign distribution. Its gain intervals are -16.70% to +12.94% for SERVAL and -16.59% to +9.13% for DRS. This calculation still fixes the period and model. None of these intervals is a complete planet posterior.

Removing all observations after the fibre change gives +2.63% and -0.38% gains. Restricting the later set to K5 gives +0.98% and -1.39%. Therefore, the weak main gain is not explained solely by the few later mask changes.

## Period and model sensitivity

A search that uses only early red velocities selects 195.95 days on the stated grid. Its later gains are -6.86% for SERVAL and -6.94% for DRS. This differs from the fixed 197.8-day result, although both periods fit the early data well.

Some other periods improve later error. There are 124 positive SERVAL nodes and 146 positive DRS nodes among the 801 tested nodes. The largest SERVAL gain is +6.73% near 201.10 days. This value uses later data to select a favorable period. We do not use it as confirmation.

We report all combinations of four time degrees (0 to 3), four extra nuisance choices (none, annual wave, 320-day wave, Earth velocity plus its square), three noise scales (0.5, 1, 2 m/s), and two sets of inner periods. The second set uses 4.3115, 9.6207, 20.4185, 34.62, and 51.56 days. This gives 96 settings for each later velocity product. All candidate coefficients still come from early red data at 197.8 days. SERVAL gains range from -5.28% to +0.84%; DRS gains range from -10.96% to -1.18%. These are selected-model ranges, not simultaneous confidence bounds.

As controls, early red waves at the updated periods of the three established short-period planets reduce later error by 31% to 44% in SERVAL and 33% to 41% in DRS. The 51.56-day control gives only +1.82% and +4.28%. The controls show that the data and code can transfer stronger signals. They do not show equal sensitivity to every period or amplitude. The updated control periods use published later knowledge, so these controls are not blind discoveries.

## Conditional recovery trials

We test coherent circular signals in the observed residuals. We remove the fitted 197.8-day term from the early and later fits. We multiply the remaining residuals by independent random signs for occupied 30-day groups. We add a coherent 197.8-day wave with random phase to both sets. Nuisance terms are removed again. Each amplitude uses 1,500 trials.

| Injected amplitude (m/s) | Fraction with positive later gain, fixed period | Fraction with positive later gain, early period search |
|---|---:|---:|
| 0.50 | 0.788 | 0.447 |
| 0.95 | 0.953 | 0.722 |
| 1.50 | 0.996 | 0.953 |

The searched-period method selects an early peak among the same 801 nodes. At 0.95 m/s, its median later gain is +5.88%, but its conditional 95% range is -16.17% to +18.49%. Thus, a failed prediction by one best early period cannot by itself exclude a coherent wave. These trials assume the fitted residuals represent the noise and that group signs are a useful error model. Positive gain is a weak recovery rule. It is not a detection threshold. These fractions are not survey completeness or planet occurrence estimates.

## Physical interpretation and limits

Stable center-of-mass orbital motion should be common to spectral ranges. The paired color term shows that such motion alone does not describe all differences between the original products. Changes in stellar line shapes, activity, Earth's motion across detector features, and reduction choices are possible causes. The S-index test does not remove the fitted color term. Earth-velocity and time terms reduce it. These facts do not select a unique mechanism.

The later sample consists of separate exposures. It is independent in observing time, but it uses the same HARPS instrument. SERVAL and DRS are reductions of the same spectra and are not independent telescope confirmations. Published ESPRESSO work on HD 40307 was considered during the source search. No ESPRESSO velocities enter this package, and we do not claim that no other suitable data exist.

The test assumes circular waves, fixed inner periods, and linear nuisance models. It does not fit general eccentric orbits, a time-dependent stellar process, or mutual planet dynamics. The error tests omit correlations between time groups and can be affected by sparse phases. The longest error groups have few occupied bins. The early signal was selected in the original data, so the early amplitude can be biased upward. The original time convention is not fully resolved here. The test does not establish a new astronomical phenomenon or refute the published candidate.

The useful result is a reproducible, target-specific check: the original red wave gives no clear later prediction gain under the stated models, and the fitted color difference depends on how slow and Earth-related terms are treated. Fresh observations over several cycles, with stable extraction and independent instrument coverage, would provide a stronger test.

## Reproduce and inspect

The signed package contains the exact small RVBank input, extracted original table, code, nightly data, all reported model settings, uncertainty draws, signal trials, figures, and numerical checks. It can run without network access. Use Python 3.12 with NumPy, pandas, SciPy, matplotlib, and Pillow. Versions are in `files/evidence/summary.json`.

From the unpacked publication root:

```bash
python files/analyze.py --out reproduced
python -B files/supplement.py --evidence reproduced
```

The first command reruns the full analysis with fixed seeds. The second checks the paired identity, compares the projected solution with direct regression, checks that the time sets do not overlap, makes extra time tests, and calculates joint coefficient uncertainty. On the prepared host, the main run takes roughly a few minutes. Numerical last digits can vary with library versions.

To re-extract the original source table, retrieve the pinned PDF from `https://arxiv.org/pdf/1211.1617v1`, check its SHA-256 above, then run:

```bash
python files/extract_table.py /path/to/tuomi2013.pdf --out extracted.csv
```

This needs the `pdftotext` program. Compare numerical columns with `files/terra_table_a2.csv`; CSV formatting can differ. On the campaign machine, the exact shared PDF path above can be used without a download. Retrieve RVBank from the exact source URL in `files/provenance.json` if needed. Require its recorded hash. The bundled CSV supports reproduction if the live source changes.

Important outputs are `prediction.csv`, `color_uncertainty.csv`, `period_scan.csv`, `sensitivity.csv`, `color_models.csv`, `injection_summary.csv`, and `validation.json` under `files/evidence/`. The validation records direct regression agreement below 1e-10 and static PNG size checks.

## Work record and license

Campaign: 11_07_2026. Job: sci-1107-hp-astronomy-9f4a57743c9e. Topic: astronomy. Machine: hp. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. This is one worker's investigation. No child agents were used. The signing key is a campaign-machine identity. It is not a personal authorship claim.

The SCI baseline license applies to new text, figures, numerical data, and code as stated in `LICENSE`. Source publications and archives retain their own rights. Source attribution and hashes are retained. The full original PDF is not redistributed.
