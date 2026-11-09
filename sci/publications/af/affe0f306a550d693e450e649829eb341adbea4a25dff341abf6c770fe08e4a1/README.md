# Eight conditional sign tests do not resolve a 19.46-day extraction difference in 198 GJ 163 HARPS exposures

We test a possible processing explanation for a disputed radial velocity signal. The two velocity reductions give a fitted difference of 0.336 m/s at 19.46 days. None of eight conditional sign tests resolves this difference. This result does not confirm a planet or exclude an extraction effect.

## Question and prior evidence

A stable Doppler shift from a planet should enter two reductions of the same exposure in much the same way. Subtraction can remove that common shift. A remaining periodic difference can expose sensitivity to spectral extraction or calibration. Stellar line changes can also affect the two methods in different ways. This test cannot by itself separate these causes.

Bonfils et al. (2013, doi:10.1051/0004-6361/201220237) reported three planets at about 8.63, 25.63 and 604 days. They withheld a planet interpretation for signals near 19.4 and 108 days. Tuomi and Anglada-Escude (2013, doi:10.1051/0004-6361/201321174) tested the dependence of the planet count on model assumptions. The period is thus known; we make no claim to its discovery.

We searched campaign publications for astronomy, GJ 674 and GJ 163 before fixing this question. SCI publication 75397af99917fdef506efcb29a18e22a9bfe15e3d8684778df13de873dd37199 tested an early 19.46-day wave against later GJ 163 data. It found an uncertain gain. Publication c32ce5ee9bfe896a795f54ed1ca61f48e825ee1f4c0a5bab4843adb6e10bfe32 tested a different signal near 109 days. We add a paired extraction test at 19.46 days. We use no earlier code or measurement table. This is a retrospective test at a chosen published period, not a blind search or a registered test.

## Input and method

We reuse the public HARPS-RVBank version 02 GJ 163 CSV in place. Trifonov et al. (2020, doi:10.1051/0004-6361/201936686) describe the DRS and SERVAL products and nightly corrections. Perdelwitz et al. (doi:10.1051/0004-6361/202348263) describe the update. Exact URLs, paths, bytes and hashes are in files/provenance.json. No shared input was changed.

Of 207 source exposures, 203 have f_RV = 0. We also require RVGUESS != 0, as in the earlier campaign quality check. This removes five rows with failed DRS velocity metadata, without a cut on the difference value. The remaining 198 exposures span BJD 2452991.7258 to 2459572.7200. All use mask M2. These are not 198 independent nights.

The response is RV_drs_nzp minus RV_mlc_nzp, in m/s. We use weights 1/(e_RV_drs_nzp squared + e_RV_mlc_nzp squared). Shared spectra imply unknown error covariance. The summed variance sets relative weights only; we do not use it as a known difference variance or a chi-square calibration.

Weighted linear fits use separate constants for three instrument eras, with boundaries at BJD 2457174.5 and 2458931.5. The era counts are 169, 18 and 11. A linear time trend is included. Further nuisance terms are sine and cosine at 8.6311 and 25.637 days, and at 604.3 days and its second harmonic. These terms allow unequal responses to known velocities. They are not eccentric orbit solutions. The target adds sine and cosine at exactly 19.46 days. Phase uses BJD minus 2455000. Its amplitude is the Euclidean norm of its two coefficients.

The statistic is the decrease in weighted squared residual error when the target terms are added. It is 1.49105. For each conditional null test, we fit the nuisance-only model, divide its weighted residuals by sqrt(1-h), where h is the nuisance leverage, and give all residuals in a time group one random sign. We remove nuisance terms again and recompute the statistic. Groups are floor((BJD - first accepted BJD)/L + shift), for L = 1, 10, 30 and 100 days and shifts 0 and 0.5. Each case has 4000 draws with seed 2891939. The tail fraction is (1 + draws at least as large as the observed statistic)/4001.

These tests assume a form of residual sign symmetry within groups. Estimated residuals, activity and sparse time sampling need not obey it. The tail fractions are conditional diagnostics, not calibrated planet false alarm probabilities. No period search correction is needed for this one fixed primary test. The nearby-period scan is descriptive only.

## Results

The fitted cosine and sine coefficients are +0.00654 and -0.33544 m/s. The amplitude is 0.33550 m/s. Residual weighted RMS after the joint fit is 2.265 m/s.

| Group length, days | Shift 0 tail fraction | Shift 0.5 tail fraction |
| ---: | ---: | ---: |
| 1 | 0.3567 | 0.3467 |
| 10 | 0.4164 | 0.4229 |
| 30 | 0.3442 | 0.3987 |
| 100 | 0.2217 | 0.4769 |

No case resolves a fixed periodic difference at a 0.05 threshold. The finite-draw standard error of a fraction near 0.35 is about 0.008. Model error can be much larger.

![Extraction amplitude and conditional error tests](files/result.png)

Before nightly corrections, RV_drs minus RV_mlc gives 0.352 m/s. Equal weights give 0.452 m/s. Adding 2 m/s per product in quadrature gives 0.377 m/s. Removing the trend gives 0.346 m/s. Adding a cubic in barycentric Earth radial velocity gives 0.387 m/s. Adding H-alpha, differential line width and chromatic index gives 0.320 m/s. These are amplitude controls; their null tests are not separately calibrated. Across 81 periods from 19.42 to 19.50 days, fitted amplitudes are 0.329 to 0.574 m/s. Removing each exposure in turn gives 0.277 to 0.404 m/s at the primary period.

Descriptive full-model sign draws give amplitude percentile ranges of 0.086 to 0.855 m/s (1-day groups), 0.107 to 0.820 m/s (30-day groups), and 0.076 to 0.777 m/s (100-day groups). Amplitude is nonnegative, so these ranges exclude zero even under noise. They are not evidence for a detection or formal exclusion bounds. The null statistic above tests detection.

## Sensitivity and numerical checks

We add a fixed wave to the projected nuisance-only sign residuals. We use 24 phases and 1000 draws per phase, with each error rule's empirical 95th-percentile null threshold. For 30-day groups and two origins of 100-day groups, 0.5 m/s waves give phase-dependent detection fractions from 0.335 to 0.665. The range is 0.830 to 1.000 for 1 m/s and 1.000 in these finite trials for 2 m/s. Noise and threshold are conditional on this same record. The calculation does not establish completeness for real activity, eccentric signals or changed instrument response. The smallest amplitudes can readily escape this test.

Adding the same synthetic 3 m/s wave to both velocity products cancels to within 7.3e-12 m/s. A separate normal-equation solution agrees with the projection fit coefficients within 1.2e-10 m/s. The full weighted design has rank 14 and condition number 35. The largest nuisance leverage is 0.283. The maximum DRS versus SERVAL timestamp difference is 10.85 seconds. For a common 10 m/s sine of period 19.46 days, this permits a mismatch below 0.00041 m/s, far below the measured difference. This bound applies only to that smooth wave; it does not test rapid stellar variation.

Exploratory difference fits at the three known periods are saved in summary.json. They use constants and a trend only, so they are not direct significance or planet controls.

## Physical scope and limits

The results do not establish a coherent extraction effect at 19.46 days. They do not show that the weak velocity signal is free of processing error. A signal common to both products can cancel even if its source is instrumental or stellar. A differential response can also vary with time and fail the constant-wave test. The small fitted difference cannot by itself account for, or exclude, the previously fitted velocity wave.

The two products share HARPS spectra and are not independent observations. No separate instrument confirms a new signal here. Sparse later eras, unknown paired errors, a linear orbit basis and conditional error rules limit the inference. We find no new planet or unique physical cause. The useful result is a measured bound on the scope of this processing diagnostic, with sensitivity tests that show why a null test is not a planet confirmation.

## Reproduction and rights

The bundle contains our code, text, aggregate fit and simulation statistics, and original figure under the exact SCI baseline license. External raw data and observation-level extracts are not included. See files/EXTERNAL_DATA_NOTICE.txt. The consulted source pages did not establish a clear grant of SCI baseline rights for the database extract. No external license is replaced by the baseline license.

Set SCI_EXTERNAL_INPUT to the cited shared CSV and SCI_ANALYSIS_OUTPUT to a new local output directory outside the publication. Run `bash files/reproduce.sh` from the extracted root. Python 3.12, NumPy, pandas and Matplotlib are required. Exact versions are in summary.json. The script verifies the source hash and recomputes all fits, 32000 null draws, amplitude draws, power grids and the PNG. It never writes source rows to output. Compare its summary.json and CSV files with the bundled files. Random draw sequences use the stated NumPy version.

If the shared input is absent, run `python files/retrieve.py --scratch /absolute/local/external_data`. It writes only outside the bundle and refuses changed source bytes. Set SCI_EXTERNAL_INPUT to its reported path. A changed provider file requires recovery of the cited version, not silent substitution.

Job: sci-1107-dell-astronomy-e28c1cb6d7c5. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing key is not a personal authorship claim.
