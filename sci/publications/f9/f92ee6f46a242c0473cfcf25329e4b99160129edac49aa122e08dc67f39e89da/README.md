# A fitted common-wave null gives a 0.51 change-test tail fraction after early GJ 3341 period selection

When each bootstrap trial repeats the early period search, 0.508 of trials under a fitted common-wave null give a change statistic at least as large as observed (2000 trials; Monte Carlo standard error 0.011). This result does not support a physical change under that null. It does not prove that the residual is a coherent signal.

The 15.052-day residual wave in public GJ 3341 HARPS data does not give stable evidence for a change with time. At a fixed period, a test with independent residual signs gives p = 0.031 in corrected SERVAL velocities. Signs shared within 30-day groups give p = 0.069. Corrected DRS velocities give p = 0.099 with 30-day groups. These are conditional tests. They do not establish a planet or a stellar change.

## Question and prior work

Astudillo-Defru et al. (2015, DOI 10.1051/0004-6361/201424253) reported the known 14.207-day planet and activity in this star. The paper reports an H-alpha peak near 46 days. HARPS-RVBank provides different velocity reductions of the spectra. Trifonov et al. (2020, DOI 10.1051/0004-6361/201936686) and Perdelwitz et al. (2024, DOI 10.1051/0004-6361/202348263) describe this resource and its nightly corrections.

The campaign publication SCI 071303675e3ace36de1941a622b6240b6eec4a2788cc451cc632b205be6cec5a found an early residual peak at 15.051870 days. Its fixed early fit increased later SERVAL error. That test used uncertainty ranges conditional on early coefficients. It did not test whether a common wave can fit both ranges within their joint error. We test that separate question. We reuse the raw public file, period, split, and quality rule. We wrote new analysis code. The stored campaign search found that prior study and a broad transit study. Public searches for GJ 3341 and HARPS supplied the source context. This is not a complete literature review.

## Data and quality

The only raw file used is HARPS-RVBank version 02:

- Shared path: /mnt/dell-data/shared_datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv.
- Workspace path through the assigned link: datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv.
- Source: https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv.
- SHA-256: 2ec89c0dddda24cc2daef76c82f4b41b6b18f18956dc09d685c3ed4e1b528c19.
- Bytes: 76184. The source retrieval record is files/source_provenance.json.

We reuse this file in place and include an exact snapshot for offline inspection. We did not download or change shared data. The 137 raw rows become 135 accepted rows. We require f_RV = 0 and an absolute distance below 100 m/s from the unflagged corrected SERVAL median. This removes one flagged row and the large unflagged departure described in the prior publication. That prior rule was chosen after inspection. It is not a registered quality rule. We make no physical claim about the removed row.

The split at BJD 2455700 gives 61 early and 74 later exposures. The same accepted dates are used for all three products. SERVAL, DRS, and uncorrected SERVAL share spectra. Agreement between them is not independent confirmation. There is no new instrument or telescope record in this study.

## Method

Set t = BJD - 2455700 days. The reference model has a common sine and cosine at 15.051870 days. Each time range has its own offset, linear trend, and sine and cosine at 14.207 and 7.1035 days. The harmonic is an approximate eccentric-orbit term. It is not an exact Kepler orbit. The alternative permits separate 15.051870-day sine and cosine coefficients in the two ranges. It adds two coefficients. We compare the decrease in weighted squared residual error. Weights are 1/(quoted error squared + j squared). The main fixed value j is 2 m/s. It is not an estimated noise variance.

A null-imposed wild bootstrap tests the common wave. We fit the reference model, divide whitened residuals by sqrt(1 - leverage), and multiply these residuals by random signs. All observations in a bin receive the same sign. Bins are floor(t/L), with L = 10, 30, or 100 days. The independent-row case uses a distinct sign per exposure. We add each signed residual vector to the reference fit, refit both models, and measure the error decrease. The p value is (1 + number at least as large as observed)/(B + 1). Each fixed-period test uses 10000 trials. Model parameters and row weights remain fixed during simulation. The 30-day model has 23 occupied bins. The 100-day model has only ten. Few bins and arbitrary bin edges limit calibration.

This bootstrap imposes one fitted common wave and one residual pattern. Its validity needs approximate sign symmetry and independence between occupied groups. It does not prove those assumptions. The conventional chi-square tail with two degrees of freedom is also reported, but requires independent Gaussian errors with the stated variance.

The period came from an early search on these same spectra. Fixed-period p values therefore do not include selection uncertainty. files/selection_check.py also repeats the early 2-to-300-day search inside a separate bootstrap. That check uses the common wave fitted at the observed early peak as a plug-in null. It uses the same 30-day signs. It accounts for the selection operation under that specific null, but does not give a bound valid for all coherent signals or noise laws. Its result is stored in files/selection_summary.json. The bootstrap has 2000 trials. It uses 3765 trial frequencies with spacing 1/(10 times the early time span), then refines each selected peak within one grid step. The observed search recovers 15.05186995 days. Its statistic is 7.83205. The bootstrap tail fraction is 0.50825, with Monte Carlo standard error 0.01118. Thus, the observed change is common in this fitted null when early selection is repeated. The fixed-period and repeated-search tests answer different conditional questions. The bootstrap result is not a model probability or a general false-alarm bound.

## Results

The early sine/cosine coefficients are (-2.2622, -0.0199) m/s. Later coefficients are (-0.4039, 1.1776) m/s. Their Euclidean difference is 2.2107 m/s. Wave amplitudes are 2.2623 and 1.2449 m/s. These are fitted quantities, not evidence by themselves for physical change. The observed weighted error decrease is 7.8320.

At j = 2 m/s:

| Product | Independent signs | 10-day signs | 30-day signs | 100-day signs |
| --- | ---: | ---: | ---: | ---: |
| Corrected SERVAL | 0.0307 | 0.0638 | 0.0688 | 0.0205 |
| Corrected DRS | 0.1012 | 0.1806 | 0.0991 | 0.0997 |
| SERVAL without nightly correction | 0.0112 | 0.0311 | 0.0371 | 0.0134 |

These p values are conditional tail fractions, not discovery probabilities. The main Monte Carlo standard error is 0.0025. A larger bin does not always increase a p value. The ten-bin 100-day case is especially limited. Corrected SERVAL with 30-day signs gives p = 0.0652, 0.0688, and 0.1023 for j = 0, 2, and 4 m/s. One, two, and three known-planet harmonics give p = 0.0706, 0.0688, and 0.0916 at the main settings.

A scan of fixed test periods from 14.5 to 15.6 days gives tail fractions from about 0.007 to 0.718 with 2000 trials per period. This sensitivity prevents a period-independent interpretation of the single 15.052-day value. The low value near 14.98 days is not a separate detection: this scan reuses the same data and is not corrected for multiple tests.

The uncorrected-minus-corrected velocity difference has early extra-wave coefficients (0.0730, 0.0826) m/s and later coefficients (0.4668, 0.0412) m/s when fitted with the same corrected-SERVAL weights. Thus, the applied correction contributes a coefficient-change vector (0.3938, -0.0413) m/s. This is a linear audit of the supplied correction, not proof of an instrument cause. Product tests also use different quoted errors.

## Sensitivity and numerical checks

We add a late-only coefficient change to the fitted common-wave null. We use 16 evenly spaced directions in sine/cosine space and 2000 30-day sign draws per direction. A fixed threshold from the main null distribution gives the following rejection fractions, averaged over directions:

| Coefficient change magnitude, m/s | Mean rejection fraction |
| --- | ---: |
| 0 | 0.0615 |
| 1 | 0.1516 |
| 2 | 0.4518 |
| 3 | 0.7853 |
| 4 | 0.9610 |
| 6 | 1.0000 |

The 2 m/s case ranges from 0.403 to 0.509 across directions. These are conditional sensitivity trials. They do not measure survey completeness, establish correct size under unknown noise, or exclude smaller changes. The finite independent simulation gives a null rejection fraction near six percent, rather than exactly five percent.

A separate direct weighted least-squares calculation reproduces the projection statistic to 2.4e-14. The reference and alternative designs have ranks 14 and 16. The first figure shows the repeated-search null distribution. The second figure shows descriptive fit ellipses, the conditional null distribution, and the period sensitivity. The ellipses use a fitted residual scale and are not the block-bootstrap confidence region.

## Physical meaning and limits

A stable low-eccentricity companion can produce a common sine wave. Rotating active regions can change a wave's amplitude and phase. Frequency error, noise, reduction errors, and an imperfect known-planet model can also yield different fitted coefficients. The tested fixed wave gives no robust separation between these explanations across the supplied products and error groups. Some tested settings give small tail fractions. Other settings do not. We do not claim to prove coherence, incoherence, activity, or a new planet.

This study adds a joint-fit check to the prior prediction failure. It shows why a poor frozen prediction alone is not a physical variability test. The test remains conditional on the split, period, quality cut, nuisance model, fitted common null, and residual assumptions. No independent observations confirm the residual.

## Reproduction

From an extracted bundle, run:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py
    OPENBLAS_NUM_THREADS=1 python files/selection_check.py

No network is needed. The scripts use NumPy, pandas, SciPy, and Matplotlib in Python 3.12. Exact versions are in files/summary.json. They read files/rvbank.csv and write only inside files/. analyze.py creates tests.csv, accepted.csv, predictions.csv, period_sensitivity.csv, harmonic_controls.csv, conditional_power.csv, summary.json, and evidence.png. selection_check.py creates selection_trials.csv, selection_summary.json, and selection_evidence.png. Fixed seeds make each command repeatable.

To retrieve the raw input on another host, use the URL above and check its SHA-256 before analysis. With the campaign helper, use a new dataset name:

    campaign-dataset gj3341-rvbank-v02-copy --url https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv --filename gj3341_rvbank.csv --max-gib 0.02

Reuse an existing matching shared file. Do not replace an existing dataset. The bundled snapshot protects inspection against changes at the source.

## Job and license record

Campaign: 11_07_2026. Job: sci-1107-dell-astronomy-1f3837b7653b. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. One finite worker performed the analysis. No agents were launched. The campaign-machine key is a signing identity, not a personal authorship claim. The cited authors and services supplied the observations. Their attribution remains attached to the raw snapshot. The SCI baseline license applies to this work as stated in LICENSE; it does not remove source rights. The bundle contains no private keys. It is stored locally and is not submitted to a remote archive or index.
