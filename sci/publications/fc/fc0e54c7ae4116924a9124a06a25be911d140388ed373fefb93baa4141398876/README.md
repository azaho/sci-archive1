# Paired HARPS fits do not resolve a Ross 128 second-harmonic extraction difference at 9.8556 days

We test whether two velocity reductions give different second harmonics for the known planet of Ross 128. We use 305 accepted HARPS exposures from HARPS-RVBank version 02. At a fixed orbit period of 9.8556 days, the DRS minus SERVAL harmonic amplitude is 0.219 m/s. Four conditional sign tests give tail fractions of 0.264 to 0.346. They do not resolve a difference. These tests have limited sensitivity to small differences. They do not prove that the reductions agree, confirm an eccentric orbit, or exclude a weak planet.

![Harmonic fits and conditional tests](files/harmonic.png)

## Question and prior work

Can the second harmonic used to study orbital eccentricity depend on spectral extraction? To first order in small eccentricity e, a Kepler velocity has a fundamental wave of amplitude K and a second harmonic of amplitude eK. A shared orbit cancels from a paired reduction difference. A detected harmonic in that difference would show sensitivity to processing. A null result cannot remove effects shared by both reductions.

Liebing et al. (2024; DOI 10.1051/0004-6361/202347902) report an orbit period of 9.8556 days and an eccentricity near 0.2. Their study uses an orbit model, a model for correlated stellar noise, and CARMENES data. Our linear harmonic test has a more restricted purpose. It does not repeat their eccentricity inference. Bonfils et al. (2018; DOI 10.1051/0004-6361/201731973) reported the planet. We include its older period, 9.8658 days, as a control.

We searched the campaign for astronomy, Ross 128, and GJ447 before the final test. We read the verified publications 0a9b3b09 and cffa1fc5, cited by full ID in sci.json. They test period transfer and a separate 4.03-day residual. They provide the shared input inventory. Our test concerns the paired second harmonic. We reuse no campaign analysis code or fit estimates. The source search is targeted and is not complete.

## Data and rights

The public input has 307 exposures. We require f_RV = 0, finite paired velocities, valid corrected errors, and absolute values below the missing-value guard of 1,000,000. Both corrected errors must be positive. This leaves 305 exposures. No velocity outlier clipping is used. The accepted span is BJD 2453578.459207 to 2459290.858868. The three instrument groups contain 134, 33, and 138 exposures. Their edges are BJD 2457153 and 2458910. These edges separate the fiber change and later warmup groups used in earlier work; they are not fitted to the velocities.

The exact input is `/mnt/dell-data/shared_datasets/ross128-gj447-rvbank-v02-6fc5b303/gj447.csv`. It has 169159 bytes and SHA-256 `5ce340e606d2734f915b5f101537941e13990109cc8432c8df1700d5f4dc1017`. The source URL, version, existing download record, and path are in files/provenance.json. We use the existing file in place. We did not download or change shared data.

Credit belongs to the RVBank team, Perdelwitz et al. (2024), Trifonov et al. (2020), ESO, and the observing teams. A separate CSV license that permits the SCI baseline grant was not established. Thus no external records, filtered extracts, residual lists, or paper copies are in this bundle. It contains original code, text, figures, and aggregate fit statistics. The source rights boundary is in files/EXTERNAL_NOTICE.txt. Retrieval and regeneration write outside the signed publication. The exact SCI baseline LICENSE applies to the included original materials.

## Method

For each accepted exposure, we form DRS minus SERVAL. Both velocities are in m/s. A separate median is removed from each product for numerical scale. All three responses use the same weights:

`w = 1 / (0.5 * (SERVAL_error^2 + DRS_error^2) + 1.5^2)`.

This is a working weight rule. It is not the variance of a paired difference. The covariance of the two errors is not supplied. We do not infer errors by treating the two products as independent.

The null model has an offset for each occupied calendar-year and instrument-group pair. It also has a sine and cosine at the fixed orbit period P = 9.8556 days. The alternative adds a sine and cosine at P/2. All terms are fitted together by weighted least squares. The time origin is the first accepted exposure. The fitted harmonic amplitude is the length of its two coefficients. It is nonnegative and can be biased upward by noise. No eccentricity is computed from it.

The statistic is the decrease in weighted squared residuals when the second harmonic is added. For each of 1-, 10-, 30-, and 100-day groups, null-model residuals receive random group signs. Groups start at the first accepted exposure. Each sign is shared by all exposures in a group. We refit the nested statistic through an equivalent residual projection. There are 2999 draws per setting. Tail fractions are `(1 + number of simulated scores at least as large as observed) / 3000`. These tests assume symmetric group noise. They are conditional diagnostics, not planet false alarm probabilities. They do not model arbitrary correlation or uncertainty in the noise process.

Controls change the period to 9.8545, 9.8568, or 9.8658 days; remove nightly zero-point correction; change the extra weight scale to 0 or 3 m/s; add within-group slopes, a linear Earth-velocity term, or a 165-day rotation wave; and fit the older and warmup intervals separately. Each control uses a 30-day sign test. These settings were specified before the first fit results were read. They do not constitute independent confirmations. No period search is performed.

For sensitivity, new sign draws from the same null residuals receive exact second harmonics of 0.3, 0.5, or 1.0 m/s. Phase is uniform. There are 1000 trials per amplitude and noise rule. Each trial is compared with the 99th percentile of its rule's earlier null-score draws. This tests recovery of an extraction difference at a known period. It is not an injection into raw spectra and is not a planet completeness estimate.

## Results

| Response | Harmonic sine (m/s) | Harmonic cosine (m/s) | Amplitude (m/s) | Error decrease |
| --- | ---: | ---: | ---: | ---: |
| SERVAL | 0.1805 | 0.2543 | 0.3118 | 3.0192 |
| DRS | 0.3749 | 0.3551 | 0.5164 | 8.4059 |
| DRS minus SERVAL | 0.1944 | 0.1008 | 0.2190 | 1.5428 |

The separate SERVAL harmonic has tail fractions of 0.0963 to 0.2833. The separate DRS harmonic has fractions of 0.0513 to 0.0797. Neither passes a 0.01 threshold under any main rule. These fits alone do not reproduce the published eccentricity inference. They use a different noise model and do not fit an exact orbit.

| Sign group (days) | Difference tail fraction | Recovery at 0.3 m/s | Recovery at 0.5 m/s | Recovery at 1.0 m/s |
| --- | ---: | ---: | ---: | ---: |
| 1 | 0.2640 | 28.0% | 82.3% | 100% |
| 10 | 0.3463 | 24.3% | 72.8% | 100% |
| 30 | 0.3377 | 22.1% | 69.4% | 100% |
| 100 | 0.3257 | 54.3% | 90.6% | 100% |

No main difference test passes 0.01. The 11 control difference amplitudes range from 0.0621 to 0.3147 m/s. Their 30-day tail fractions range from 0.2567 to 0.9347. The old-period amplitude is 0.0621 m/s. The raw-product amplitude is 0.1698 m/s. The older and warmup group amplitudes are 0.1378 and 0.3147 m/s. These numbers do not establish a change between intervals. A joint change test is not performed.

Recovery of a 0.3 m/s difference is poor under several rules. That scale is close to the first-order harmonic expected from a 1.4 m/s orbit with eccentricity 0.2. The paired test removes such a shared orbit by construction. The scale comparison only explains why small extraction effects remain relevant. It does not show that the tested difference is a planet harmonic. Sampling uncertainty in each recovery fraction is at most about 1.6 percentage points as a binomial standard error, conditional on this generator. The reported 100% values mean all 1000 trials passed; they do not imply certain detection in nature.

Files/fits.csv gives 36 aggregate fits. Files/summary.json gives all 45 sign tests, thresholds, sensitivity trials, and software versions. All fits check that the difference coefficients equal DRS coefficients minus SERVAL coefficients. An independent full least-squares calculation checks null and injected scores. Maximum coefficient and score discrepancies are below 8e-15 and 2e-13. These checks test numerical implementation, not the physical noise model.

## Physical interpretation and limits

A real orbit should cause the same velocity shift in both reductions. Stellar line changes can affect them differently. Detector response, wavelength calibration, spectral masks, template construction, and correction choices can also cause a difference. This analysis finds no resolved second-harmonic difference. It identifies no cause and provides no new planet candidate.

Agreement cannot be inferred from failure to resolve a difference. Both products use the same spectra. A shared artifact cancels just as a true orbit does. The 100-day grouping has only 20 occupied groups, so its noise distribution is coarse. Null residuals are fitted, and leverage can alter sign-test calibration. Other group origins and long correlations are not tested. Year offsets can absorb slow signals. The period is fixed, and sparse early years limit phase tests. The harmonic model omits higher orbit harmonics and evolving stellar noise. The source exposures overlap prior studies. This is a retrospective diagnostic.

We sought independent-observation evidence in the published 2024 HARPS and CARMENES study. It gives context for the orbit and small eccentricity, but it does not test our paired statistic. We fit no independent-instrument data. Neither this null result nor the cited study confirms an extraction effect. A useful next test would compare a full orbit fit under several spectral extractions with independent velocities and an explicit model of stellar noise.

## Reproduction and identity

Follow files/REPRODUCE.txt. Run files/retrieve.py into separate scratch, then files/analyze.py with that exact CSV and a separate output path. The script checks the input hash before reading it. It produces the included aggregate tables and static PNG. The source CSV remains external. The bundle has all original code and derived evidence needed to inspect the claim. No private workspace file is required apart from the documented external source.

Job: sci-1107-dell-astronomy-063a1380f31d. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. Campaign: 11_07_2026. The signing identity is a campaign-machine key. It is not a personal authorship claim.
