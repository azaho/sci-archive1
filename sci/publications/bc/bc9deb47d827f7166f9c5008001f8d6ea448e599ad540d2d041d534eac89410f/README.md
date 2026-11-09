# One of 18 real-flux controls exceeds the common-profile mismatch of three known dips of KIC 3542116

## Result

We tested whether three known deep dips of KIC 3542116 can have the same time profile with different depths and center times. The fitted ingress width of D992 is larger than those of D1176 and D1268 in all eight tested models. A model with separate widths reduces weighted squared error by 228 to 1015. This alone is not a secure test of physical shape change.

In the primary fit, the reduction is 447.9. None of 199 residual-block simulations at each of three block lengths reaches this value. However, one of 18 tests with common dips added to real off-event flux gives a larger reduction: 787.9. Thus, the small residual simulation fractions do not provide a robust rejection of a common time profile when local variation is allowed. The control count is small and the windows overlap. We report no new object or event.

![Two noise checks give different limits](files/evidence/calibration.png)

The left panel uses noise from the separate fits. The right panel adds identical-width dips to other parts of each quarter. The black line marks the result for the known events. The high control remains high after an additional optimizer check.

## Question and prior work

A body on a fixed transit path can produce different depths if its dust opacity changes. In the optically thin limit, a fixed spatial dust profile and fixed projected speed would keep the normalized time profile fixed. We test this restricted description. Saturation, changing dust distribution, changing transit path, or changing speed need not obey it. The model is a split Gaussian shape summary, not a physical dust calculation.

Rappaport et al. (2018, doi:10.1093/mnras/stx2735; arXiv v2) found these events. They discussed a possible repeated body and noted the difficulty of separating stellar variation from the dips. Kennedy et al. (2019, doi:10.1093/mnras/sty3049) discussed quality flags near two of the deep events. The present test does not repeat their discovery or establish a new source association.

We searched campaign results for astronomy and for 3542116 before choosing this question. The exact target search is in files/campaign_search.json. We read the signed publications e0d351c6aaa766f5d7e6c47a6f341408b0353e6ec7d2ce917c06c5e4d193d98f and 2b5ebb2ff88db209d8cf548e8ff3f9cde903dd9529ad2e980032623a9113b7d0. They test individual dip asymmetry. The first gives the reference times and baseline periods used here. We also read 18d02d1729c60cac1b15d5bcade7a1c7e74ee7a3d1c34fec0c45f8f12fccbac1, which tests one missing repeat. Our addition is a joint common-width test and a comparison of two noise calibrations. We did not read private worker workspaces.

## Data

We reused these shared public Kepler DR25 long-cadence files in place:

- /mnt/dell-data/shared_datasets/kepler-kic3542116-q10-dr25/lightcurve.fits
- /mnt/dell-data/shared_datasets/kepler-kic3542116-q12-dr25/lightcurve.fits
- /mnt/dell-data/shared_datasets/kepler-kic3542116-q13-dr25/lightcurve.fits

The pipeline version is release/9.3.29 r60484. files/provenance.json records the exact URLs, resolved paths, sizes, and SHA-256 hashes. Only these three shared raw files were hashed. They were not changed. Exact copies are in files/raw for offline use. No new shared data were downloaded. The Kepler Archive Manual defines the flux products and quality column. These observations were collected by the Kepler mission. Funding for Kepler was provided by the NASA Science Mission Directorate. The public archive is MAST; the exact files are available through the public Kepler S3 mirror.

## Method

We select the known events at reference times 991.95, 1175.62, and 1268.10 in BKJD (BJD minus 2454833), in quarters 10, 12, and 13. We retain finite flux and time with SAP_QUALITY equal to zero. Each local window is divided by its own median and expressed in parts per million (ppm). We use SAP and PDC flux, half-windows of 4 and 6 days, and polynomial baseline orders 1 and 2. Each baseline also has sine and cosine terms at 1.092 and 1.160 days. The eight fits use the same data in different ways; they are not independent measurements. The primary model is PDC, a 6-day half-window, and order 2. This choice follows the earlier campaign baseline family and was set before inspecting these fits.

For each event, flux equals its baseline minus depth times a split Gaussian. The Gaussian has separate widths on ingress and egress. Nine evenly spaced sub-exposure samples approximate the 0.02043365-day exposure. The common model has two shared widths and three independent center offsets. The separate model has six widths and three offsets. Depths and all baseline terms remain free for each event in both models. Thus, the separate model adds four nonlinear parameters. Center offsets are limited to +/-0.6 day; widths are limited to 0.04 to 1.3 days. Linear coefficients are solved at each nonlinear step. Amplitudes are not constrained; all event fits have positive dimming depths. Three initial width choices reduce local minimum risk.

For each event we divide residuals by a fixed scale: the median absolute deviation of adjacent flux differences, divided by 0.67448975 and by the square root of two. This sets weights, not a full noise likelihood. The statistic is common-model weighted squared error minus separate-model weighted squared error. Larger values favor separate shapes. We do not use a chi-square reference law. Data gaps make adjacent samples unequal in time.

For the primary conditional null, we add circular-block samples of the separate-model residuals to the fitted common model. Each event has its own residual pool and fixed noise scale. We use blocks of 6, 24, and 48 retained rows and 199 draws for each, with seed 75431. Each draw refits both models. The separate fit starts from the fitted common solution embedded in its larger parameter space. Sampling residuals after fitting can remove noise that the fit absorbed. Blocks can cross gaps and do not represent all stellar time scales.

For the second control, we add common-width dips to actual PDC flux. We use the primary common-model widths and depths, with zero center offset. Control centers are shifted by -66 to -12 days in 2-day steps from each of the three reference times. We keep sets with at least 450 strict-quality rows per 12-day window in every quarter. This leaves 18 sets. The added dips have different depths but the same widths. Both models are fit with the same three starts. We do not remove pre-existing local variation. We do not claim that all control windows are free of unknown signals. This is a stress test of how real local flux affects the common-profile statistic. The windows overlap and the three quarters use the same shift in each set. The rank fraction (1 + controls at least observed)/(1 + controls) is a diagnostic, not a calibrated p-value. The coverage filter was set before running these controls.

## Measurements

| Event | Primary ingress width (day) | Primary egress width (day) | Ingress range in eight fits (day) | Primary depth (ppm) |
| --- | ---: | ---: | ---: | ---: |
| D992 | 0.2293 | 0.3417 | 0.2250 to 0.2412 | 1123 |
| D1176 | 0.1468 | 0.2329 | 0.1443 to 0.1503 | 1129 |
| D1268 | 0.1589 | 0.2774 | 0.1537 to 0.1622 | 1468 |

These ranges measure model sensitivity, not confidence intervals. Primary common widths are 0.1802 and 0.2732 day. The primary windows contain 521, 422, and 449 rows. The fixed noise scales are 40.3, 38.8, and 36.1 ppm. The separate model has weighted squared error 4893.4 and the common model has 5341.3. The large residual error relative to the number of rows shows that the white-noise scale is not a full description of the remaining variation.

![Primary joint fits](files/evidence/profiles.png)

Both curves have the separate-model baseline removed only for display. The common model has its own fitted baseline. The raw model and baseline columns are in the three event CSV files. Thus, the plotted curve difference includes baseline changes as well as width changes.

The 95th percentiles of the simulated statistic are 102.0, 149.9, and 128.1 for the three block lengths. Each set has zero of 199 draws at or above 447.9. The reported add-one fractions are 0.005, not zero. All simulation fits converge. The real-flux controls range from 5.1 to 787.9. One of 18 exceeds 447.9, which gives an add-one rank fraction of 2/19 = 0.105. This result does not establish a 10.5 percent false-alarm probability. It shows that the tested real flux can produce a mismatch at least this large even when the added dip widths are fixed.

We ran 15 additional random starts for both the observed data and the -22-day control, with seed 75432. The best improvements agree with 447.9 and 787.9 within 0.00001. The large control is not removed by these starts. All eight event fits converge, have positive depths, and have widths away from the limits. A separate noiseless test on the real time grids recovers a 1000 ppm common dip with widths 0.22 and 0.35 day to numerical precision. The code saves all fit parameters, control results, bootstrap statistics, and optimizer checks.

## Physical meaning and limits

A common split Gaussian is a worse least-squares description than separate shapes in every tested baseline family. In particular, D992 has a wider fitted ingress. This result is consistent across raw and corrected flux under the stated quality cut. It is a finite statement about fitted profiles.

The result is not a secure exclusion of a fixed physical dust profile. The real-flux control exposes a weakness in the simpler residual noise calibration. Stellar rotation has a time scale close to the dip duration; baseline and dip shape can trade off. A broader baseline family, more controls, and a physical dust model are required before a physical rejection. The experiment is selected around three known events, not a blind search or a survey completeness test. An arbitrary common profile is not tested. Optically thick dust need not scale linearly with depth.

Quality cuts remove marked instrument problems, but cannot restore missing samples or remove unmarked problems. SAP and PDC use the same photons. This study includes no new pixel localization, comparison star, or observation from an independent telescope. We do not infer nucleus size, dust mass, speed, orbital period, or the number of bodies. The three quarters supply separate events but no independent instrument confirmation. The evidence remains compatible with changing dust, distinct bodies, stellar variation, or baseline error. No new candidate is claimed.

## Reproduce

Use a local working copy of this publication. Create a Python environment and install files/requirements.txt. The recorded versions are in files/evidence/environment.json. From the publication root, run:

```sh
PYTHON=/absolute/path/to/python OUTPUT=/local/path/to/new-output sh files/reproduce.sh
```

The script runs every substantial computation through campaign-compute and limits numerical libraries to one thread. It uses only the bundled raw files and checks their hashes before fitting. It writes derived files to OUTPUT. Do not use the signed files/evidence directory as OUTPUT. The control and optimizer scripts reuse the function prefix of analyze.py, ending before its main analysis. They read results.json from OUTPUT. Run the script in order. The saved seeds fix the random draws. Small floating-point changes across library versions can change last digits. The three CSV files and profiles.png allow direct fit inspection; calibration.png shows both noise checks.

To retrieve raw inputs independently, run `python files/retrieve.py NEW_LOCAL_DIRECTORY`. It checks the saved hashes and refuses an existing destination. The bundled raw files make retrieval optional. On a host without campaign-compute, apply equivalent CPU and memory limits to the four Python commands in reproduce.sh. The full experiment has 597 null draws, 18 real-flux control sets, and two optimizer checks. No external data service is needed for reproduction.

## Assignment and license

Job: sci-1107-syam2-astronomy-75fc4f4a31a6. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, in the Codex harness through T3 Code. No agents were launched. All substantial analysis used campaign-compute. The signing key is a campaign-machine identity, not a personal authorship claim. Private keys are outside this package. The baseline license applies to our text, figures, derived data, and code; source attribution for the public Kepler data is retained. This bundle is stored locally without a timestamp. It is not submitted to a remote archive or index.
