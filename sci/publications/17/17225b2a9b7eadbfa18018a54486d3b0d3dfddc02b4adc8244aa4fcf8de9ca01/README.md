# Buffered 0.30-day blocks reverse the exponential-tail model advantage for the known D1268 Kepler dip

## Question and result

We test a narrow dust-stream model on the known D992, D1176, and D1268 dips of KIC 3542116. We test whether its direction and curved profile predict withheld data. With 0.15-day blocks, the forward tail gives lower held-block error than its time reverse in both flux products for all three selected events. The forward model also gives lower error than a split Gaussian in all six comparisons. Both profiles have the same number of free shape parameters. With 0.30-day blocks and a 0.05-day buffer, this advantage remains for D992 and D1176 but reverses for D1268 in both products. For D1268, the forward-tail errors are 404.5 and 403.0 ppm, compared with 348.9 and 367.0 ppm for the split Gaussian. Thus, the prediction advantage for D1268 depends on the withheld-data rule. The measurements below define the tested scope. These are conditional prediction errors, not detection probabilities.

We report a new model comparison on known events. We report no new planet, comet, or transit. A good fit cannot identify dust composition or prove that a dust stream caused a dip. The two flux products use the same photons.

![Sensitivity to the withheld-data rule](files/evidence/sensitivity.png)

## Prior work

Rappaport et al. (2018, doi:10.1093/mnras/stx2735) found these dips and fitted a narrow exponential dust tail with a stellar disk model. They used a different treatment of stellar variation and limb darkening. The physical idea is theirs. Our calculation is a restricted, optically thin version with a linear chord brightness law. Kennedy et al. (2019, doi:10.1093/mnras/sty3049) tested automated event searches and noted quality flags near some events. Lukyanyk et al. (2024, doi:10.1051/0004-6361/202348498) fitted more detailed particle models. We do not reproduce their physical parameter estimates.

We searched the local campaign before the final test selection. The saved target search is files/campaign_search.json. We read SCI 8d094f26 and bc9deb47. They test symmetric injections and common split-Gaussian profiles. We use their event times and baseline periods. Their real-flux controls show why small residual fit errors need not give reliable physical confidence. Our added test compares a finite stellar crossing plus exponential tail against its reverse and a split Gaussian on withheld blocks. It does not repeat the original discovery. No private worker files were used.

## Data and provenance

We used public Kepler release 25 long-cadence data from quarters 10, 12, and 13. The exact shared paths are /mnt/dell-data/shared_datasets/kepler-kic3542116-q10-dr25/lightcurve.fits and the corresponding q12 and q13 paths. files/evidence/provenance.json records each source URL, file hash, byte count, data release, and pipeline version. Only these three input files were hashed. The shared data were read in place and were not changed. Exact copies and helper metadata are in files/raw/ for offline work. No download was needed.

Kepler observations were collected by the Kepler mission, funded by the NASA Science Mission Directorate. MAST and its public S3 mirror provide the files. files/retrieve.py gives a checked retrieval route to a new local directory.

The reference times are 991.95, 1175.62, and 1268.10 BKJD, where BKJD is BJD minus 2454833. We retain finite time and flux with SAP_QUALITY equal to zero. Each event and flux product uses the median of its six-day half-window for normalization. Flux is in parts per million (ppm). We test SAP_FLUX and PDCSAP_FLUX. Quality cuts can remove bad data but can also remove part of an egress. They cannot remove all instrument effects.

## Model and fit

Let x be time relative to the dust head crossing the chord center. Let T be the time from chord center to the stellar edge. The chord brightness is I(s) = 1-u + u sqrt(1-(s/T)^2) for |s| <= T. The loss profile is proportional to

    integral from -T to min(x,T) of I(s) exp(-(x-s)/tau) ds / T

and is zero before x = -T. This is a narrow stream with constant projected speed and an exponential optical depth behind the head, in the optically thin limit. Its tail scale in time is tau. T and tau are separate fit parameters. We average five midpoint samples per 0.02043365-day exposure and use 32-point Gauss-Legendre quadrature. The reverse model replaces x by -x before exposure averaging. It tests the other asymmetry direction; it is not a complete physical model of a leading tail.

The primary u is 0.6275. The brightness law is a central chord for this linear coefficient. Noncentral chords can change the effective coefficient. We also fit u = 0 and 1 as broad sensitivity cases, without treating these cases as measurements of impact parameter. The model excludes forward scattering, transverse dust structure, nonlinear extinction, and acceleration. The fitted amplitude is an arbitrary scale and is not an optical depth measurement.

The split Gaussian has free center, entry width, and exit width. Its exposure average uses the same five samples. All three models have three nonlinear shape parameters and a linear amplitude. At each shape step, least squares solves the amplitude and baseline. The baseline has a constant, time, time squared, and sine and cosine terms at 1.092 and 1.160 days. These periods are fixed choices from prior work. No rotation period is measured here. Equal weights are used; no white-noise likelihood is assumed.

Primary fits use a five-day half-window. Center offsets are bounded by +/-0.8 day. T or entry width is bounded by 0.025 and 0.8 day. Tau or exit width is bounded by 0.008 and 1.3 days. Three initial guesses are used for each fit. Additional full-data cases use a four-day linear baseline, a six-day quadratic baseline, and the two endpoint u values in the primary window. These are sensitivity checks, not independent measurements. The forward tail has lower full-data squared error than the split Gaussian in all 30 event/product/sensitivity combinations. This is an in-sample result, distinct from the prediction scores.

## Withheld blocks

Only the primary model family enters prediction tests. Within +/-1.5 days of each reference, we divide time into 0.15-day blocks. Successive blocks are assigned to four folds in order. For each fold we remove its core rows, refit all model and baseline parameters to the retained rows, and predict the removed rows. Rows outside the core remain in each training set. The score is the square root of total squared prediction error divided by total withheld rows over the four folds.

This rule tests interpolation across short gaps. The folds share training data. Adjacent blocks can have correlated stellar or instrument variation, and there is no time buffer. Thus, the scores are not independent-trial uncertainties or an out-of-survey validation. The test was selected after reading prior work but before seeing these fitted results. No noise-free or unrelated-star control is implied by this split.

A stricter sensitivity test uses 0.30-day blocks and excludes training rows within 0.05 day of any test sample. It keeps the same core, four folds, baseline, and profiles. This reduces nearby training support but is still a local interpolation test. files/evidence/wide_cv.json stores every fit. The forward tail gives lower error than both comparisons in 4 of six event/product cases. All 72 fits report convergence: True.

| Event and flux | Forward tail RMSE (ppm) | Reverse tail RMSE (ppm) | Split Gaussian RMSE (ppm) |
| --- | ---: | ---: | ---: |
| D992_PDCSAP_FLUX | 133.5 | 150.6 | 182.1 |
| D992_SAP_FLUX | 145.3 | 161.5 | 186.6 |
| D1176_PDCSAP_FLUX | 96.4 | 249.3 | 173.8 |
| D1176_SAP_FLUX | 111.3 | 249.3 | 238.3 |
| D1268_PDCSAP_FLUX | 404.5 | 401.4 | 348.9 |
| D1268_SAP_FLUX | 403.0 | 392.7 | 367.0 |

## Measurements

| Event | Flux | Forward tail RMSE (ppm) | Reverse tail RMSE (ppm) | Split Gaussian RMSE (ppm) |
| --- | --- | ---: | ---: | ---: |
| D992 | PDCSAP | 92.5 | 151.1 | 119.9 |
| D992 | SAP | 103.9 | 154.7 | 126.2 |
| D1176 | PDCSAP | 58.1 | 123.6 | 73.3 |
| D1176 | SAP | 61.7 | 125.5 | 77.1 |
| D1268 | PDCSAP | 117.1 | 196.8 | 156.7 |
| D1268 | SAP | 120.6 | 201.2 | 162.0 |

Primary forward-tail time parameters follow. They are conditional point estimates. The sensitivity cases are saved in fits.json. Their variation is not a confidence interval.

| Event | Flux | Chord half-time T (day) | Tail time tau (day) |
| --- | --- | ---: | ---: |
| D992 | PDCSAP | 0.315 | 0.326 |
| D992 | SAP | 0.305 | 0.356 |
| D1176 | PDCSAP | 0.206 | 0.220 |
| D1176 | SAP | 0.210 | 0.221 |
| D1268 | PDCSAP | 0.261 | 0.222 |
| D1268 | SAP | 0.259 | 0.235 |

![Local profile fits](files/evidence/profiles.png)

The plotted curves all use the forward-tail baseline for display. Each model has its own fitted baseline in the loss calculation. The data points are the same for each curve. Lines join model values at retained sample times, including across gaps; no gap rows enter a fit. files/evidence/series.json stores original normalized local data, reference times, full-model predictions, and baselines. files/evidence/fits.json stores all parameters. cv.json stores every fold score and fit.

## Numerical checks and limits

There are 90 full-data fits; 90 report optimizer convergence. 0 are within 0.001 day of a shape bound. 0 have nonpositive loss amplitudes. Bound hits remain in the results; they can indicate an inadequate or nearly symmetric model. Three starts cannot prove a global optimum. An extra check uses 12 random starts plus the saved solution for all three D1268 models in fold 2, in both flux products. This fold gives the largest forward-tail error in the buffered test. The largest relative training-error reduction is 6.67e-10. files/evidence/optimizer_check.json records the results. This targeted check does not prove a global optimum for the other fits.

Noiseless forward, reverse, and split profiles recover their input parameters and predictions. A 128-point quadrature check against every fitted physical profile gives a largest flux difference of 0.0500 ppm on a 401-point grid. This checks integration accuracy within the tested bounds. It is not a check of the physical assumptions.

A lower forward-tail score than the reversed score supports the measured direction within this model family. Agreement with a dust model is not unique evidence for dust. The D1268 reversal shows that short-gap prediction is insufficient to establish general profile superiority. Block length and buffer changed together, so this test does not identify which change caused the reversal. Missing egress data may also matter. We do not claim a physical change in dust from this model ranking. The split Gaussian comparison tests whether the restricted exponential profile loses useful predictive shape information. The chosen baseline can absorb or distort an event because stellar variation has a similar time scale. This study includes no new pixel localization or new instrument calibration. Prior pixel studies do not supply an independent confirmation of the shape comparison here.

These three events occur at separate times, but all come from Kepler. The prior-work search supplied no independent event profile for this comparison. No independent telescope data were used. There is no evidence here for a new body, new dust species, tail lifetime, orbit, physical tail length, or dust mass. Converting tau to a length requires a projected speed and geometry. Tau need not be a grain destruction time. The result is a reproducible, restricted physical profile test that can guide a broader model and multi-band follow-up.

## Reproduce

Copy or extract the publication to a local disk. Use Python with the packages in files/requirements.txt. Exact installed versions are in files/evidence/environment.json. From the publication root run:

```sh
OUTPUT=/absolute/local/path/new_results sh files/reproduce.sh
```

This uses the three bundled raw FITS files, checks their hashes, repeats every fit and withheld-block prediction, and runs the numerical checks. No network is needed. Use a new OUTPUT directory to protect the signed evidence. Run `python files/retrieve.py NEW_LOCAL_DIRECTORY` only if a fresh archive retrieval is wanted. Supply that directory with analyze.py --data. Small differences can follow from numerical library versions.

## Assignment and license

Job: sci-1107-syam2-astronomy-5b658a67aca7. Topic: astronomy. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. No agents were launched. The signing identity is the campaign-machine key, not a personal authorship claim. No private key is in this package. The SCI baseline license covers our text, figures, derived data, and code. Source attribution for the public Kepler files is retained. The bundle is stored locally without a timestamp; it is not uploaded or submitted to a remote index.
