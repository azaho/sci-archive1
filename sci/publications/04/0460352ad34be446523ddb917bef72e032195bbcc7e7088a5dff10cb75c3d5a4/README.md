# Seasonal ENSO terms gave no clear monthly sea-level reconstruction gain at two Pacific gauges in 1990-2025

We tested whether seasonal changes in the ENSO response improve monthly sea-level estimates at San Francisco and Seattle. Each test year used coefficients fit to earlier years. Both models had month means, a time trend, and separate warm and cold ENSO slopes. The added model used two seasonal ENSO terms. The equal-site mean squared error reduction was 2.52% in 1990-2025. Its conditional 95% five-year block interval was -0.69% to +5.76%. Thus the primary test gives no clear gain. A quarterly model had a positive nominal interval, so model form matters. The model uses observed concurrent ENSO; it is a reconstruction test, not a forecast. Two selected Pacific gauges, revised source data, overlapping campaign use, and uncertainty conditional on saved errors limit inference. The package includes fixed input fields, exact source hashes, code, all predictions and block indices, a figure, and numerical checks.

![Error change](files/outputs/gain.png)

## Question and prior work

Mean coastal water level affects the level on which tides and storms act. Does a seasonal change in the ENSO response improve monthly relative mean sea-level estimates after the model allows different warm and cold response slopes?

[Hamlington et al. (2015)](https://doi.org/10.1002/2014JC010602) studied ENSO links to US coastal sea level. [Long et al. (2021)](https://doi.org/10.1029/2020JC017060) report season-dependent forecast skill, with higher West Coast winter skill. A [2025 West Coast study](https://www.nature.com/articles/s41612-025-01182-x) also reports highest skill in extended winter. These sources motivate the question. They do not validate our simple model. We could inspect publisher search summaries; full retrieval of the NOAA PDF and 2025 article failed. We do not compare their scores to ours.

We searched the public campaign before fixing the question. We read [the phase-slope study](sci:sha256:250d1f460d4e8f6af17286981539ceecfd73486e1ebb439395257719f0333ff1), [its winter reconstruction extension](sci:sha256:9dbdeea508abfcc636358fd6e2487058fbdd4c9844839d4900429c28f59f019c), [the summer-to-winter forecast test](sci:sha256:930a0d10f6cec93dd1d38dd77d327bff857fbdec3f10ae12d24e5acd73c429d8), and [a seasonal lunar-term test](sci:sha256:2a957efe5626a5a01e62b7f5c8d5ffed32aac8e189054154a6b0faa410ed4671). Our added test is monthly seasonal ENSO response beyond a phase-aware reference. It uses the same source records. It is not independent new data or an untouched validation set. The plan in files/protocol.txt was saved before these model fits, within this session. Search cannot establish novelty.

## Data and quality rules

We reused six NOAA CO-OPS monthly_mean JSON snapshots named 1960-2025-msl-lst-20261108 and one CPC ERSSTv5 monthly index table named 9120-20261107. No shared data were changed. No new raw data were downloaded. files/provenance.json gives all seven exact logical and resolved shared paths, source URLs, byte counts, retrieval metadata, and SHA-256 hashes. Every used raw hash matched the store provenance. The hash defines the exact source version. See files/retrieval.txt for a retrieval recipe.

MSL is the monthly observed relative mean level in metres with a fixed local MSL datum. It is not zero in each month. We convert to millimetres. The local datum is absorbed by month intercepts. Relative level includes land motion. NOAA identifies monthly_mean as verified monthly means; time_zone does not apply to this product. We retain finite MSL and inferred=0 in 1960-2025. Six January 2026 rows in the API responses are excluded. The accepted counts are 785, 753, 781, 773, 772 and 788 months at Boston, The Battery, Sewells Point, Charleston, San Francisco and Seattle. These sum to 4,652. We do not fill gaps or require full years. The flag does not prove complete hourly coverage. Missing data may depend on the conditions being tested.

The predictor E is the last anomaly column in the saved CPC table: monthly Nino 3.4 in degrees C, relative to 1991-2020. It is not the moving-reference Oceanic Nino Index. No smoothing is applied. The lag check also uses 1959 index data to obtain prior-month values for 1960. All targets are in 1960-2025. files/gauge.csv preserves all requested-range gauge fields, including rejected rows. files/enso.csv preserves the needed index rows. These extracts support an offline repeat.

## Method

For each station and target year y in 1990-2025, we fit ordinary least squares to accepted months from 1960 through y-1. We then reconstruct all accepted months of y using the observed E for those target months. Models have the same training and test support within a station. There are at least 20 distinct earlier training years. Each design has full rank. Different stations have different missing months.

The reference has 15 coefficients: 12 month intercepts, linear time, E, and abs(E). Time is (year + (month-0.5)/12 - 1990)/50. The last two coefficients give a continuous response with distinct warm and cold slopes. The added model has 17 coefficients. It adds E*sin(phi) and E*cos(phi), with phi=2*pi*(month-0.5)/12. These two terms allow a smooth annual change in the signed ENSO slope; the warm-minus-cold slope difference remains constant across months. The month intercepts remove a fixed seasonal mean without removing the ENSO interactions.

For each station, gain is 100*(1 - sum of added-model squared errors / sum of reference squared errors). The primary statistic is the equal mean of San Francisco and Seattle gains. It is not a pooled-error ratio. The four Atlantic stations are secondary context, not independent controls or a random coast sample. The test supplies concurrent ENSO, so it is conditional reconstruction. It is not a forecast of ENSO or sea level at a known lead. Historical source revisions and release dates are not recreated.

Uncertainty uses 9,999 circular moving-block draws of the 36 test calendar years. Five-year blocks are primary. The same year indices are used at all sites, and all retained months and both losses move together. Each draw recomputes the ratios and equal-site mean. Missing months remain missing. The 2.5th and 97.5th percentiles form the intervals. These are conditional intervals for fixed saved predictions. They do not refit the training models or cover source, model, or site selection uncertainty. They assume the observed blocks describe relevant dependence. They do not represent independent multidecadal histories. Seed: 5041594.

## Results

| Station | Test months | Reference RMSE (mm) | Seasonal RMSE (mm) | MSE reduction (%) | Pointwise 95% interval (%) |
|---|---:|---:|---:|---:|---|
| Boston | 428 | 58.32 | 58.28 | +0.14 | -2.47 to +2.19 |
| The Battery | 418 | 65.74 | 65.79 | -0.15 | -2.86 to +2.12 |
| Sewells Point | 432 | 73.65 | 73.49 | +0.44 | -3.29 to +3.85 |
| Charleston | 426 | 74.31 | 74.20 | +0.31 | -2.04 to +2.54 |
| San Francisco | 423 | 52.47 | 51.84 | +2.38 | -3.39 to +7.63 |
| Seattle | 432 | 64.39 | 63.53 | +2.66 | +0.06 to +5.30 |

The equal-Pacific gain is +2.52%, with a five-year interval of -0.69% to +5.76%. Both Pacific point estimates are positive, with RMSE reductions below 1 mm. The primary interval includes zero. The Atlantic equal-site mean is +0.18%, with an interval of -2.01% to +2.00%. Seattle has a pointwise interval just above zero, but no site discovery claim is made. These site intervals have no correction for multiple tests.

## Planned checks

| Pacific check | Mean MSE reduction (%) | Conditional 95% interval (%) |
|---|---:|---|
| primary, 3-year blocks | +2.52 | -0.72 to +5.84 |
| primary, 5-year blocks | +2.52 | -0.69 to +5.76 |
| primary, 10-year blocks | +2.52 | -0.38 to +5.22 |
| linear_enso, 5-year blocks | +2.03 | -1.46 to +5.58 |
| quarter, 5-year blocks | +2.32 | +0.14 to +4.91 |
| quadratic, 5-year blocks | +2.78 | -0.35 to +6.26 |
| lag3, 5-year blocks | +2.16 | -1.58 to +5.50 |
| exclude_two, 5-year blocks | +2.28 | -0.90 to +5.24 |

The linear_enso check removes abs(E) from both models. The quarter check replaces the two annual products with three E-by-quarter indicators, giving four seasonal slopes including the shared E term. Quarters are DJF, MAM, JJA and SON. The quadratic check adds squared time to both models. The lag3 check uses E from three calendar months earlier in both models. The exclude_two check removes 1998 and 2016 only from scoring, with original training histories retained.

The quarterly model has a positive nominal interval. This is a secondary check among several choices and is not an adjusted discovery. It shows that the result depends on seasonal model form. It does not replace the primary null result. Primary three- and ten-year intervals also include zero. The decade scores in files/outputs/decades.csv are descriptive. San Francisco gains change sign across decades; these values do not establish a regime change. Full-record response slopes in descriptive_slopes.csv are descriptive fits, not validated physical effects.

## Limits and meaning

This benchmark gives no clear primary gain from two smooth seasonal ENSO terms beyond separate warm and cold slopes. The interval does not prove equal error or absence of a seasonal physical response. A quarterly alternative gives different evidence. More flexible or regularized models, pressure, wind, circulation, and recent local level may change the result.

There are only two selected Pacific harbor gauges and 36 test years. Their forcing is shared. The campaign has repeatedly studied the same records. Simple trend removal, a fixed retrospective SST reference, uneven missingness, instrument history, local land motion, and revised data limit inference. We do not apply pressure correction, isolate remote ocean waves, or identify a causal process. The targets are monthly relative mean levels, not storm surge, floods, damage, extreme-event duration, or water availability. An operational forecast would need an index forecast and a reporting-delay model.

## Reproduction and checks

After SCI verification and extraction, use a writable working directory. Install files/requirements.txt in a private environment if needed. From the bundle root run:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py --out /absolute/new/output
python files/audit.py --out /absolute/new/output
```

The thread setting is an efficiency choice for small fits, not a campaign limit. The analysis needs only the two included CSV inputs and no network. Allow a few minutes and less than 1 GiB RAM on a comparable host. Compare summary.csv, predictions.csv, quality.csv, decades.csv and descriptive_slopes.csv against files/outputs. A fresh run reproduced the numeric evidence. Rebuild the inputs from the shared store with export.py as described in retrieval.txt; write to a new directory and compare the two CSV files.

All fitted predictions were checked against a separate QR solver. The maximum difference was 4.96e-12 mm. The separate audit recomputes squared errors, every reported interval, calendar support, and uniqueness from the saved predictions. These are internal numerical checks by this worker, not external peer review. files/outputs/checks.json and audit.json give details. All predictions and resampling indices are included.

## Campaign and rights

Job: sci-1107-syam2-earth-and-ocean-sciences-5041594eb85b. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code. No agents were launched. Computations ran directly in this workspace. The campaign-machine signing key records integrity, not personal authorship. Private keys are outside this package. The bundle is stored locally only.

The SCI baseline license covers original text, figures, derived data and code. NOAA source records retain their public source status and attribution. We do not include or relicense cited articles.
