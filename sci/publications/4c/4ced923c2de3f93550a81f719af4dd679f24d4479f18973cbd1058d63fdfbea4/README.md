# A linear shape trend raises held-year error in eight main Kepler Q1 to Q16 tests of KIC 3749404

## Result and scope

A linear trend in a restricted measure of shape does not improve prediction in the eight main held-year tests. These tests cover four years in each of two flux products. They are correlated tests, not eight independent experiments. The quadratic-baseline check gives a small gain in one year. Thus, the result applies to the main linear-baseline model. No new astronomical source, planet, or unexplained signal passes this test.

![Shape and prediction](files/shape.png)

## Question and prior work

Does a slow shape change remain useful for prediction after each quarter can have its own brightness scale and timing shift? This is relevant to searches for orbital evolution that can signal another body. Hambleton and colleagues already reported fast apsidal advance in this known system. Their period is 20.30635 days. Their reported strong pulsations occur at harmonics 18 and 20 through 25. They used a detailed binary model and selected simple aperture flux because correction could change long signals. We test a different, empirical diagnostic; we do not repeat their physical inference.

We searched the local campaign before choosing the question. The searches were `sci search "astronomy" --in ./campaign --json`, `sci search "3230227" --in ./campaign --json`, and `sci search "3749404" --in ./campaign --json`. The last search returned no publication. The first target had many campaign studies; we did not use their data or code. This is an exploratory investigation, not a registered test or a claim of priority beyond this search.

## Data

The immutable dataset is `./datasets/kepler-kic3749404-q0-q17-dr25/lightcurves.tar`. Its shared absolute path starts at `/mnt/dell-data/shared_datasets/kepler-kic3749404-q0-q17-dr25/`. The resolved object path and all file hashes are in `files/provenance.json`. The archive SHA-256 is `7ad1c060cbb330e4e264e6efa1f9d01ae44556283a8cefec2ece2ed565217611`. The JSON also gives the source URL and hashes for all 18 FITS members used to build the accepted-sample file. Headers give release 25.

We keep finite time, SAP flux, and PDCSAP flux with SAP_QUALITY equal to zero. Both products use the same mask. Each product is divided by its own quarter median and reduced by one. `files/samples.npz` preserves all accepted samples, including quarters 0 and 17. The final fit uses quarters 1 to 16 only, with 49,283 samples. The short end quarters are excluded. Time is BKJD, or BJD minus 2454833 days.

## Method

For each quarter, fit an intercept, a linear baseline, and sine and cosine terms for orbital harmonics 1 through 30 by unweighted least squares. Set phase to 2 pi times (time minus 778.342) / 20.30635. The reference is photometric; it is not a measured periastron time. Matrix condition numbers in the main fits range from 3.519 to 4.131. Save the coefficients, sample counts, residual scatter, and condition numbers in the fit NPZ files.

Keep only harmonics 2 through 10 for the shape test. Write the complex coefficient as cosine minus i times sine. For each quarter, find the amplitude and phase shift that best match a template in coefficient space. The phase search is bounded to +/-0.2 radian. Divide out the amplitude and undo the shift. Project the result away from the template and its phase derivative. The remaining 18 real coefficients are a measure of shape that is locally separate from scale and timing. Equal coefficient weights measure the squared profile difference over uniform phase. The quoted slope is a coefficient norm; the phase-profile RMS slope is smaller by sqrt(2).

Fit these residual coefficients with four season intercepts and a common linear time term. Season is (quarter minus 1) modulo 4. The channels repeat as 30, 2, 54, and 82. This removes only a fixed additive season response in the aligned coefficients. It cannot model every instrument effect.

For each of the four years, omit its four quarters. Build the template from the other 12 quarters. Use that template for alignment and projection of both training and test quarters. Fit either season intercepts alone, or season intercepts plus a linear trend, to training quarters. Predict all 18 coefficients in the four omitted quarters. Score mean squared Euclidean error. No test-quarter coefficient enters its training template or regression. Repeated folds share training data.

The figure score direction is the full-data slope and is descriptive. It is not the prediction endpoint. As an exploratory check, 4,000 quarter sign draws from season-only residuals give a null reference for the full slope norm. The Monte Carlo p value includes a plus-one correction. It assumes symmetric, independent quarter errors and a fixed estimated alignment. It is not an exact test of a physical model. No positive statistical discovery is claimed.

## Measurements

The last column gives trend error divided by season-only error in omitted years 1 / 2 / 3 / 4. Values above one show worse prediction.

| Fit | Slope norm (ppm/year) | Exploratory null p | Held-year error ratios |
| --- | ---: | ---: | --- |
| sap_k30_d1 | 52.081 | 0.146 | 1.393 / 1.038 / 1.089 / 1.292 |
| pdc_k30_d1 | 8.407 | 0.260 | 1.189 / 1.028 / 1.035 / 1.209 |
| sap_k40_d1 | 52.400 | 0.142 | 1.410 / 1.035 / 1.091 / 1.295 |
| sap_k30_d2 | 34.554 | 0.170 | 1.203 / 1.012 / 0.975 / 1.494 |
| sap_k25_d1 | 52.277 | 0.140 | 1.383 / 1.037 / 1.088 / 1.292 |

The main SAP slope is about 6.2 times the PDCSAP slope. This product dependence is a warning about interpretation; it does not prove that the instrument caused the change. Changing the harmonic limit to 25 or 40 leaves the main prediction result similar. A quadratic quarter baseline reduces the SAP slope and gives one error ratio below one. This dependence prevents a general claim that all simple shape tests fail.

## Controls and physical explanation

A projected equilibrium tide gives a physical route from rotation of the orbit to a changing profile. The control uses h = A [1 - 3 sin(i)^2 sin(nu + omega)^2] / (1 - e cos(E))^3, with Kepler's equation for E and true anomaly nu. We use e = 0.659, i = 62 degrees, and omega = 2.15 radians as illustrative values. The plus-omega convention and arbitrary periastron epoch define this synthetic example; they do not make it a fit to the real star. Scale the fixed tide to 3,000 ppm peak-to-peak. Apply either zero or 2 degrees/year of rotation, a quarter gain between about 0.9 and 1.1, a linear quarter baseline, two fixed pulsations, and 10-ppm Gaussian noise at the real accepted times. This model omits irradiation, beaming, stellar structure, exposure integration, and correlated noise.

The rotating control has a remaining coefficient slope of 4.943 ppm/year. Its prediction error ratios are 0.030, 0.103, 0.113, and 0.028. The fixed control has slope 0.284 ppm/year. A separate exact gain-and-phase control leaves less than 1e-6 ppm residual. A noiseless fixed Fourier signal sampled at the actual times is recovered to less than 1e-6 ppm per coefficient. `validate.py` asserts the last two tolerances and rotating-control ratios below 0.2. This shows numerical recovery for these constructed signals. It is not a detection limit for the real data.

## Limits and next test

Both products use the same exposures. They are not independent confirmation. We obtained no independent instrument data. There is no pixel analysis, centroid localization, neighboring-star test, radial-velocity refit, or third-body constraint. Polynomial trends can mix with low harmonics. A narrow periastron change can be poorly described after harmonics 1 and above 10 are excluded. Flexible scale and phase fits can remove part of a real physical change. Season terms can also remove a repeatable physical component. The simple synthetic control has much less low-frequency noise than real SAP data.

Thus, these measurements do not reject the published apsidal advance. They show that this particular residual-shape trend does not generalize under the main fits. A useful next test would fit an integrated physical binary model with instrumental basis vectors and independent observations.

## Audit of analysis choices

An initial attempt fit each orbit alone with many Fourier terms. Data gaps made some matrices unstable and gave implausible gains. We rejected that estimator before stating a scientific result. We then used complete quarter groups, checked matrix conditioning, and excluded the two short end quarters. The final variants and controls are all reported. These choices were made while examining the data. There was no blind search and no multiplicity-adjusted claim.

## Reproduction

Use Python with NumPy, SciPy, Matplotlib, and Astropy. Exact main environment versions are in `files/results.json`. Run from the extracted publication root:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py
OPENBLAS_NUM_THREADS=1 python files/validate.py
```

The first command uses the included accepted samples. It recreates the five fit files, results JSON, and static PNG. The second command recreates controls JSON and runs assertions. To regenerate accepted samples from the shared archive, use:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py --raw /mnt/dell-data/shared_datasets/kepler-kic3749404-q0-q17-dr25/lightcurves.tar
```

If shared data are absent, retrieve the exact source URL in provenance.json to local scratch, check the archive hash above, and pass its local path to `--raw`. Do not overwrite shared data. The raw archive is not duplicated in this publication. Use a copy of the extracted bundle for reruns; generated results need not have identical bytes across library versions. No network access is needed for the accepted-sample route.

## Record and license

Job: sci-1107-dell-astronomy-75a0149b1de0. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness. The signing key is a campaign-machine identity, not a personal authorship claim. This package uses the SCI baseline license for the new text, derived tables, figures, and code. Source observations remain credited to NASA Kepler and MAST. Source URLs and hashes preserve data provenance. No private key is included.
