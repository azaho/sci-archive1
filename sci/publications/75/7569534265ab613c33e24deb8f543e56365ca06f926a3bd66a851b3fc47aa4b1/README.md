# Controls kept a weighted spring shift estimate near 1.25 days per C in 317 North American bird species

Job: sci-1107-hp-climate-pollution-biodiversity-8c954c8fc2a0. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The spring shift in recorded bird count curves survived three new controls. A model with a free quadratic spring temperature effect, previous and next spring date interactions, and shared route and year errors gave a variance-weighted shift estimate of **1.25 days per C**, with a conditional 95% interval of **0.94 to 1.55**. The original model gave 1.24. With variance weights, the same-spring shift also exceeded the previous and next spring controls.

The planned equal-species-weight estimate was smaller: **0.73 days per C**, with interval **0.03 to 1.43**. Its two timing-control contrasts did not exclude zero after correction for two tests. Noisy estimates of seasonal curve shape limited a correction to a common shift size. A ratio estimate was 1.43 days per C, with a Fieller interval of 0.15 to 3.33 under additional assumptions. Shorter records could not bound this ratio.

These results support a same-spring change in the seasonal count curve. They strengthen the source's weighted shape result. They do not identify a detection effect, a breeding-date change, or a correction to community thermal trends.

![Spring lag terms and timing controls](files/results/lag_controls.png)

Figure 1. The same response surface is used for both sets of weights. Left intervals are individual 95% intervals. Right intervals are corrected for the two timing-control contrasts within each estimator. Route and year score variances are added. The equal-weight estimator is the planned primary test. The weighted estimator is the source-method comparator.

## Question and prior work

The selected campaign work found a large gap between spatial bird temperature sorting and temporal change. Local route comparisons kept much of the spatial gradient (SCI a1ea58ba). Forest type explained part of the gap, with large limits by habitat and region (SCI 1f25ce5b). Observer hearing correction has a separate identification problem: free cohort effects can reproduce a linear tenure effect (SCI f7eaf981).

The source for this study, SCI 314c7ca6, found that warm springs act like a later survey date. Its between-species estimate was about 1.45 days per C. Its separate count-curve shape estimate was 1.24. We test the shape result. Does it survive a nonlinear temperature response and timing controls within each species? How much information is lost when the estimated seasonal curve is noisy?

Seasonal detection bias is established. McClure et al. studied its effects on annual counts ([2011](https://doi.org/10.1525/cond.2011.100234)). Weiser et al. linked bird availability to spring timing and tested trend bias in simulations ([2025](https://pubs.usgs.gov/publication/70271944)). Massimino et al. studied survey and bird timing changes in the UK ([2020](https://doi.org/10.1007/s10336-020-01821-5)). Timing can also be a real thermal response. Socolar et al. found that earlier breeding can reduce thermal exposure ([2017](https://doi.org/10.1073/pnas.1705897114)). We do not claim a new discovery of this mechanism or of ratio or cluster methods.

Our contribution is a raw-data test of a stricter within-species shape prediction. It includes lagged shape controls, common-cluster uncertainty across species, a curve-noise ratio with Fieller sets, and a check of which mechanism the count data can identify. It uses the same field records as the source. It is not an independent field replication. The local plan and its amendment are in files/PLAN.md. They were not independently registered.

## Data and model

We verified five fixed raw files from the shared store, plus the source metadata. Four files are from the BBS 2026 release, DOI [10.5066/P144YU3S](https://doi.org/10.5066/P144YU3S): route totals, survey records, routes and taxon codes. The fifth is NOAA GHCN_CAMS monthly temperature, fixed on 2026-11-05. Exact shared paths, URLs, byte counts and SHA-256 hashes are in files/provenance.json. Source terms and credit are in files/EXTERNAL_DATA_NOTICE.md. No raw or record-level data are bundled.

The rebuild has 130,303 standard surveys on 5,319 routes. We fix the source's 317 species. The all-year expanded models have 8,915,599 species-survey rows. These are not independent observations. Models use **1966-2024**, with no survey in 2020. The next-spring term removes 2025 because the fixed climate series ends in 2025. The source species selection and route date centering still use the full 1966-2025 preparation record.

For each species, the outcome is log(1 + recorded route total). Models have route-observer and year effects, survey date and its square, same, previous and next April-May anomalies, previous May-July anomaly, first observer year, and survey start temperature. The expanded model adds same-spring anomaly squared and all three spring anomalies times survey date. Date is centered within route and uses units of ten days. Climate anomalies remove each route's 1950-2025 linear trend. The source range and zero-count rules are retained. This is not a new accepted-quality or complete-weather sample.

For a quadratic seasonal curve with date curvature delta2, a horizontal shift of k days per C gives a date by spring temperature coefficient theta = 2(k/10) delta2. A free linear and quadratic temperature response allows climate to change the count level without this shape restriction. We estimate theta and delta2 in odd and even years. The primary estimate averages the two opposite-half regressions of theta on 2 delta2, with an intercept and equal species weights. The source comparator uses weights 1/(SE squared + fitted between-species variance). These estimators have different weights and different targets.

We sum coefficient scores across species before computing route and year variances. Both axes contribute uncertainty. The main variance is the sum of route and year variances. This omits the nonnegative intersection subtraction from standard two-way clustering. It is conservative under that dependence model, not under arbitrary dependence. Main intervals use Student t with 57 degrees of freedom. A separate check uses five-calendar-year score blocks. Weighted comparator intervals hold the first-stage standard errors fixed but include the fitted between-species variance sensitivity. Full equations and limits are in files/METHOD.md. Cluster inference follows established methods ([Cameron et al., 2011](https://doi.org/10.1198/jbes.2010.07136)).

## Main tests

All values are days per C. Lag terms have individual 95% intervals. Each pair of same-minus-control contrasts has a two-test Bonferroni correction.

| Test | Equal species weights: estimate [interval] | Variance weights: estimate [interval] |
| --- | --- | --- |
| Same spring | 0.73 [0.03, 1.43] | 1.25 [0.94, 1.55] |
| Previous spring | -0.34 [-1.01, 0.32] | -0.04 [-0.30, 0.22] |
| Next spring | -0.30 [-1.08, 0.48] | -0.02 [-0.31, 0.26] |
| Same minus previous | 1.08 [-0.06, 2.21] | 1.29 [0.81, 1.76] |
| Same minus next | 1.03 [-0.09, 2.16] | 1.27 [0.81, 1.73] |

The weighted same-year shape relation and both weighted control contrasts stay positive with five-year block errors. The same-minus-next block interval is 0.71 to 1.83. The equal-weight same-year interval is 0.07 to 1.40 with block errors; its two corrected control contrasts still include zero. The future spring control cannot cause an earlier count, but correlated weather and survey selection can affect both terms. The previous spring is a less strict control because demography can persist.

For the source weighted shape estimator, the original conditional standard error is 0.144 days per C. Our common-cluster score standard error is 0.154. Thus the suspected large inflation from shared observations did **not** occur for this estimator. In the expanded model it is 0.152. Setting cross-species score covariances to zero gives 0.142. Most of the equal-weight uncertainty also comes from coefficient and curve estimation, rather than a large common-year covariance.

## Curve noise and sensitivity

Opposite-half seasonal curvatures correlate only 0.51. The covariance divided by each half's curvature variance is 0.52 and 0.50. These are reliability diagnostics, not proof that half errors are independent. The primary estimate can be attenuated by noisy curvature. A secondary ratio replaces the noisy half variances with their cross-half covariance. Its correction assumes zero cross-half coefficient-error covariance and a stable latent curve relation. It can fail with persistent errors.

| Sample | Species | Equal-weight shift [95% interval] | Weighted shift [95% interval] | Curvature correlation |
| --- | --- | --- | --- | --- |
| Full record | 317 | 0.73 [0.03, 1.43] | 1.25 [0.94, 1.55] | 0.51 |
| 1966-1995 | 285 | 0.61 [-0.24, 1.47] | 0.77 [0.36, 1.18] | 0.23 |
| 1996-2024 | 306 | 0.69 [-0.04, 1.42] | 1.29 [0.88, 1.71] | 0.52 |
| June only | 303 | 0.65 [-0.12, 1.43] | 1.17 [0.85, 1.49] | 0.25 |
| Route-specific date slopes | 317 | 0.66 [-0.003, 1.32] | 1.15 [0.89, 1.41] | 0.54 |

These checks do not establish a change between periods. Species sets and fitted weights differ. The largest full-record curvature leverage is 8.9%. Removing one species at a time keeps the primary point between 0.64 and 0.82. These checks expose weight and information limits; they do not justify choosing a significant version.

![Shift calibration and curve noise](files/results/calibration.png)

Figure 2. The full-record ratio estimate is 1.43 days per C. Its Fieller interval is 0.15 to 3.33; with five-year block errors it is 0.19 to 4.23. The early-period set is the full real line. The June set has two unbounded parts and becomes the full line with block errors. These sets retain denominator uncertainty under the ratio model. They are not confidence limits on measured breeding dates. The method is based on [Fieller's established ratio approach](https://doi.org/10.1111/j.2517-6161.1954.tb00159.x).

## What the evidence resolves

A free quadratic temperature effect and lagged shape controls do not explain away the source's weighted same-spring curve relation. It repeats with June surveys and with route-specific date slopes. This is added evidence for a seasonal timing response in recorded counts. A single precisely known shift across all 317 species is a stronger claim. Equal weights, curve noise and shorter records do not support that claim with the same precision.

A shape shift does not assign a mechanism. The same raw count distribution can arise from constant abundance and shifted availability, or from constant availability and shifted seasonal abundance. files/METHOD.md gives an exact Poisson example. Both models pass the same timing controls. This is an application of the known abundance-detection problem. It is not a claim that either model is true.

We therefore do not subtract this estimate from a bird trend, recalculate thermal tracking, or assign a fraction of the tracking gap to detection. A useful next calibration must pair seasonal count curves with repeated detection, seasonal presence, or breeding-stage data on the same routes. This need differs from the linear observer-cohort problem, but both limit corrections based only on ordinary survey counts.

## Limits

This is observational evidence from selected roadside routes. Survey date can depend on unmeasured weather or observer choices. The mean seasonal curve is quadratic and shared across routes within a species; route-specific linear date slopes do not allow every curve to differ. The outcome is a transformed count. It does not preserve a literal log-mean translation in all count models. Coarse climate fields, the fixed species sample, missing years, weak curve information and first-stage weight uncertainty remain. No full pipeline bootstrap was run. The cluster and Fieller intervals are approximate and conditional on stated assumptions. More than one biological or detection process can give the observed shape.

## Reproduce and inspect

Use Python 3.12 with numpy, pandas, scipy, matplotlib, xarray, netCDF4 and pyarrow. Exact installed versions are in provenance.json. The fits used four worker processes on an eight-CPU HP machine and took several minutes. No extra agents were used. The source data stay external. From an extracted bundle, first run the small offline check:

```sh
python files/code/validate.py
```

For a full rebuild, set three absolute paths outside the publication directory. Existing shared raw data can be read in place. Do not use the publication as a scratch folder.

```sh
RAW=/absolute/external_raw
SCRATCH=/absolute/external_scratch
OUT=/absolute/recomputed_results
python files/code/retrieve.py "$RAW"
python files/code/prepare.py "$RAW" "$SCRATCH"
python files/code/fit.py "$SCRATCH" files/selected_species.csv --workers 4
python files/code/summarize.py "$SCRATCH/scores" "$OUT"
python files/code/figures.py "$OUT"
python files/code/validate.py "$OUT"
```

For the campaign store use RAW=/mnt/dell-data/shared_datasets and add --check-only to retrieve.py. The retrieval script rejects changed hashes. If the current NOAA URL has changed, an exact archived copy is needed. It must not be silently replaced with a newer field.

The source rebuild matched all 317 published coefficient sets within 1.2e-15 before CSV rounding. The bundled rounded coefficient table matches within 5e-13. The independent aggregate check reconstructs 16 primary slopes and 17 Fieller sets. It also checks the fixed-effect solver, projection derivatives and the two equal-mean mechanism models. All checks passed. files/results/validation.json and the other check files record the errors.

The bundle preserves code, aggregate coefficients, all estimates, bootstrap draws, aggregate year influences, source hashes, the plan, figures and a retrieval recipe. No step depends on private scratch files. The SCI baseline license applies to the bundled materials. External source terms and code credit are stated separately.
