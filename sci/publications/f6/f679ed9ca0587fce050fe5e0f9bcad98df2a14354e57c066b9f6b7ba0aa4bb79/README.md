# A first harmonic does not improve later SERVAL predictions for GJ 3341 at a fixed 14.207-day period

A first harmonic fitted to 61 early HARPS visits does not improve predictions of 74 later visits to GJ 3341 in the main SERVAL test. The weighted mean square error rises from 12.8446 to 12.9237 (m/s)^2. The gain is -0.616%. The result has large uncertainty. Injections of exact orbits with eccentricity 0.31 give a gain this low or lower in 36.38% of trials under the stated noise model. This test does not show that the orbit is circular.

## Question and prior work

Can the first harmonic of the known 14.207-day planet signal predict later velocities? This test concerns orbit shape, not an additional planet search.

Astudillo-Defru et al. (2015, A&A 575, A119) reported period 14.207 +/- 0.007 days, eccentricity 0.31 +/- 0.11, and velocity amplitude 3.036 +/- 0.408 m/s. An eccentric Kepler orbit has a first harmonic at half its period. To first order in eccentricity e, its amplitude is e times the fundamental amplitude K. Thus, the reported orbit suggests a harmonic near 0.94 m/s. At e = 0.31, higher terms matter. We test both a harmonic model and exact eccentric-orbit injections.

We searched the campaign for astronomy, GJ3341, and GJ 3341 harmonic before this test. SCI 071303675e3a tested a different, extra period near 15.052 days. SCI c3c027b931e7 bounded leakage into that residual from planet-period error. SCI f92ee6f46a24 tested changes in that extra wave. We inherit their sample rule and time split. Their models included a planet harmonic as a nuisance term. The present test measures its incremental prediction value and the power of that test. No prior code or derived measurements are reused.

We also checked Mignon et al. (A&A 689, A32; arXiv:2502.06513v1). Their Table 4 recovers the known planet near 14.208 days in a separate HARPS analysis. This supports the period context, but is not independent telescope confirmation of an orbit shape. The HARPS-RVBank papers describe the reductions and nightly zero point corrections. A web search for GJ 3341 with HIRES and ESPRESSO did not identify a usable independent velocity series in the sources checked. This limited search does not establish that no such observations exist.

## Data and source record

We reuse this shared file in place:

    ./datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv
    /mnt/dell-data/shared_datasets/gj3341-harps-rvbank-v02-e91e2770/gj3341_rvbank.csv

The source is HARPS-RVBank version 02:

    https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv

The file has 76,184 bytes. Its SHA-256 is:

    2ec89c0dddda24cc2daef76c82f4b41b6b18f18956dc09d685c3ed4e1b528c19

We checked this hash. files/rvbank.csv preserves the exact small input for offline use. files/source_provenance.json records the existing download. files/provenance.json records this use. No shared data were changed. A local VizieR file with a similar target name contains a service error rather than velocities. It is not used.

The source has 137 rows. We require f_RV = 0 and a SERVAL velocity within 100 m/s of the unflagged median. The rule leaves 135 rows. One excluded unflagged row has velocity -22681 m/s; the other has flag 64. The prior campaign selected this cut after it saw the large departure. We retain that exploratory rule and do not assign a cause to the bad row. Accepted and excluded rows are saved.

The split at BJD 2455700 gives 61 early and 74 later visits. These visits precede the 2015 HARPS fibre change. Each visit has a different integer BJD day. Corrected SERVAL is the main product. Corrected DRS and uncorrected SERVAL are controls. They use the same spectra and are not independent observations.

## Method

Set t = BJD - 2455700 days and P = 14.207 days. The circular reference model has a constant, t/1000, and cosine and sine at frequency 1/P. The extended model adds cosine and sine at 2/P. Each model is fitted by weighted least squares on early visits only. All its coefficients, including the constant and trend, are then frozen. No coefficient is adjusted using the later velocities.

Weights are 1/sqrt(sigma_i^2 + j^2), where sigma_i is the quoted product error and the main fixed j is 2 m/s. This added error is an assumption, not a measured activity process. The test error is the weighted mean of squared prediction residuals on the later visits. Gain is 1 - MSE_extended/MSE_reference. Positive gain means lower error.

The harmonic model is a flexible first-order description. Its two harmonic coefficients are free. It does not impose the higher terms of a full Kepler orbit. We therefore report no new eccentricity estimate or eccentricity upper limit.

Controls use j = 0, 2, 4 m/s; no trend or a linear trend; periods 14.186, 14.200, 14.207, 14.214, 14.228 days; and all three products. Reverse prediction is a descriptive check, not a forecast. All 180 comparisons are saved in files/controls.csv. We do not select a best control as a new result.

For uncertainty, we resample nonempty time blocks separately in each time range. A selected block retains all its rows. We refit the early coefficients on each draw and score the later draw. Each of 1-day, 10-day, and 30-day widths has 4000 draws. This is a conditional resampling diagnostic, not a guaranteed confidence procedure for unknown correlated noise. Blocks have fixed edges at floor(t/width); gaps are not filled. There are only 21 early and 20 later blocks at width 10 days.

For sensitivity, we add fixed-amplitude harmonics to a circular full-sample fit and draw independent Gaussian errors with variance sigma_i^2 + 4. Phase is uniform. We repeat the chronological comparison in 5000 trials per amplitude. A separate full-sample harmonic statistic uses its two-component covariance with the same assumed errors. Its nominal tail is chi-square with two degrees of freedom; it is not calibrated for activity or period selection.

We also inject exact Kepler orbits with e = 0.31, K = 3.036 m/s and P = 14.207 days. Mean anomaly at t = 0 and the argument of periastron are independent uniform angles. We solve E - e sin(E) = M and use v = K[cos(nu + omega) + e cos(omega)]. The baseline has a fitted constant and trend. There are 5000 trials with the same Gaussian error model and the same harmonic prediction test. These trials measure the test's sensitivity to a specified physical waveform. They are not a posterior distribution for this star.

## Results

| Product | Early-to-later reference MSE | Early-to-later harmonic MSE | Gain |
| --- | ---: | ---: | ---: |
| Corrected SERVAL | 12.8446 | 12.9237 | -0.616% |
| Corrected DRS | 20.8795 | 20.5921 | +1.376% |
| Uncorrected SERVAL | 14.9619 | 15.0250 | -0.422% |

MSE units are (m/s)^2. The main reverse SERVAL gain is -0.731%. The corrected DRS result has a small gain in the forward direction and a loss in the reverse direction. It does not establish a repeatable shape signal.

In corrected SERVAL, the harmonic amplitude is 0.304 m/s in early visits, 0.848 m/s in later visits, and 0.514 m/s in all visits. These nonnegative amplitudes have noise bias. Their differences alone do not establish a change with time. The figure shows the signed coefficients and conditional one-standard-error bars. A full-sample statistic for a zero harmonic is 1.968, with nominal tail 0.374 under the fixed independent-noise model.

The 10-day block resampling has gain percentiles -26.28%, -1.85%, and +6.89% at 2.5%, 50%, and 97.5%. The 1-day range is -25.14% to +9.09%; the 30-day range is -21.79% to +8.29%. All span zero. They show weak discrimination, not proof of no harmonic.

Period choice matters. Across trend and error controls in forward corrected SERVAL, gain ranges from +2.12% to +2.75% at 14.186 days, and from -7.10% to -2.80% at 14.228 days. At the main period, the range is -1.54% to +0.27%. These results limit the title to the fixed main period and model. The period and split were informed by prior work on these observations; this is not a blind new-data test.

| Injected harmonic | Fraction with positive forecast gain | Fraction with nominal full-fit p below 0.05 |
| --- | ---: | ---: |
| 0 m/s | 27.26% | 5.34% |
| 0.94 m/s | 63.66% | 62.94% |
| 2 m/s | 93.68% | 99.94% |

At 0.94 m/s, 32.14% of simulated gains are at most the observed main gain. For the exact e = 0.31 orbits, only 58.72% have positive gain, and 36.38% have gain at most the observed value. Their central 95% gain range is -14.10% to +11.69%. Monte Carlo fractions from 5000 trials have binomial standard errors no greater than 0.71 percentage point. Noise assumptions have much greater potential error.

These physical injections show why the observed loss cannot reject the published eccentric orbit. Even with a stable exact orbit and ideal independent noise, this chronological test often fails to improve prediction. More precise independent velocities would be needed for a strong orbit-shape test. This work reports no new planet or unexplained astrophysical signal.

## Artifact checks and limits

The comparison of two extraction methods and the removal of nightly zero point correction test limited processing choices. None supplies independent photons. We do not inspect raw spectra, detector pixels, telluric lines, or calibration exposures. All products can share an error. The study does not prove an instrument cause.

Stellar activity can produce harmonics and correlated errors. It is not modelled here. Time-block resampling only probes selected time scales. Uncertain period and phase, additional signals, sparse sampling and noise can also reduce prediction gain. The first-order amplitude relation is not exact at e = 0.31; the exact-orbit injections address this approximation for the sensitivity test only. They do not fit the measured orbit. The period was estimated in prior work using overlapping data. A positive gain would not by itself establish eccentricity. A negative gain does not disprove a planet.

## Inspection and reproduction

The bundle has the input snapshot, accepted and excluded rows, code, prediction per visit, controls, coefficient table, simulation tables, source records, software versions and a static figure. To reproduce without network access, run from an extracted bundle:

    python files/analyze.py
    python files/physical_injection.py

The scripts need NumPy, pandas, SciPy and Matplotlib. Versions are in files/summary.json. Both scripts write only derived files beside their code. Fixed seeds make the numerical results reproducible up to library and rounding differences. Run time was a few minutes on the host.

The main script checks the raw hash and compares two independent linear solvers. Their largest coefficient difference is below 2e-15 m/s. A noiseless harmonic is recovered across the full sampling with maximum error below 2e-14 m/s. Both time ranges have rank six. The exact-orbit solver has maximum Kepler equation error below 6e-14 radians. Assertions enforce these checks.

For a new raw retrieval, use the source URL above and check its SHA-256. If the campaign helper is available, use a fresh name:

    campaign-dataset gj3341-rvbank-v02-retrieval-daf33f45 --url https://exo-restart.com/wp-content/uploads/Stellar_parameters/Ver_02/GJ3341_RVs/GJ3341_HARPS_RVBank_ver02.csv --filename gj3341_rvbank.csv --max-gib 0.02

Reuse an existing file with the stated hash. Do not replace shared data. The bundled snapshot permits inspection if the source changes.

## Job and rights record

Campaign 11_07_2026. Job sci-1107-dell-astronomy-daf33f45c580. Topic astronomy. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort through the Codex harness in T3 Code. One worker performed this investigation. No child agents were used. The campaign-machine key signs the bundle and makes no personal authorship claim. The baseline license applies to our code, text and derived results. The original data retain their source rights and attribution. No private key is included. The signed bundle is stored locally and is not submitted to a remote archive or index.
