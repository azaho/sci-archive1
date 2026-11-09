# Opposite-season thermal sea-level anomaly trends had no clear hemispheric contrast in NOAA 1955-2025 estimates

We tested changes in a fixed-season contrast of upper-ocean thermal sea-level anomalies. We used NOAA hemisphere means for the upper 700 m in 1955-2025. The northern contrast was July-September minus January-March. The southern contrast used the reverse order. The trend difference was -0.469 mm per decade. Its conditional 95% five-year block limits were -1.182 to 0.250. Thus, the test did not resolve a difference between the hemisphere trends. The point difference changed sign when we used 1980 as the start year or used the other pair of seasons. These data do not establish a hemisphere-wide change in seasonal amplitude.

![Seasonal anomaly contrasts and trends](files/seasonal.png)

## Question and context

Does a fixed warm-season minus cold-season thermal anomaly contrast have a different trend in the two ocean hemispheres? The distinction matters: an annual mean can rise while its seasonal contrast falls. Thermal sea level measures the effect of temperature on water volume. It is not sea surface temperature, ocean mass, coastal water level, or flood risk.

Published work reports stronger sea surface temperature seasonality [doi:10.1038/s41467-024-48381-3](https://doi.org/10.1038/s41467-024-48381-3). Liu et al. report weaker temperature seasonality below the mixed layer in extratropical oceans since the 1980s [doi:10.1038/s43247-024-01986-4](https://doi.org/10.1038/s43247-024-01986-4). Shi et al. study changes with depth and their relation to human influence [doi:10.1175/JCLI-D-24-0418.1](https://doi.org/10.1175/JCLI-D-24-0418.1). These results motivate a depth-integrated test. They do not imply a sign for the present fixed-season density response. We do not repeat their attribution tests.

We searched the shared SCI campaign before we chose the precise question. Terms included “ENSO earthquake ocean recovery”, “steric”, “thermosteric seasonal amplitude”, and “thermosteric opposite season”. We read the published spatial variance study [sci:sha256:83bb4a863ca08443a070d2d8a307cdcf0240a412bb6658f15108556091390ba4](sci:sha256:83bb4a863ca08443a070d2d8a307cdcf0240a412bb6658f15108556091390ba4). That study used the same NOAA thermal file, but tested total-to-thermal variance in 2005-2025. Our contribution is a reproducible seasonal trend test with a null main result and explicit time and season checks. Search does not prove novelty. This is not an independent test of the source product.

## Data

We used NOAA NCEI Ocean Heat Content, Salt Content, and Sea Level Anomalies. Credit is due to NCEI, the Ocean Climate Laboratory, and NOAA Global Ocean Monitoring and Observing. The source methods cite Levitus et al. [doi:10.1029/2012GL051106](https://doi.org/10.1029/2012GL051106). The [product page](https://www.ncei.noaa.gov/products/ocean-heat-salt-sea-level) describes the in situ source and coverage limits. The [thermal field page](https://www.ncei.noaa.gov/access/global-ocean-heat-content/tsl_global.html) provides three-month products.

We reused this shared file in place:
`/mnt/dell-data/shared_datasets/ncei-thermosteric-0-700-seasonal-20261006/mean_thermosteric_sea_level_anomaly_0-700_seasonal.nc`.

Its SHA-256 is `1635e9dafef29b56ea407a112e30e3ac9438b3cc6b51afb759f792f2bf76a4ab`. Its size is 74,469,096 bytes. The internal creation date is 2026-09-30; the folder label is not the version authority. The hash defines the snapshot. The exact resolved path and source URL are in files/provenance.json.

We used supplied mean variables `seas_a_mm_NH`, `SH`, `NA`, `SA`, `NP`, `SP`, `NI`, and `SI`, with the common prefix on each name. N and S mean northern and southern. A, P, and I mean Atlantic, Pacific, and Indian. The Atlantic includes the Arctic. Values have units of mm. We selected the first 284 quarterly values, at time 1.5 through 850.5 months since 1955-01-01. This gives 71 complete calendar years, 1955-2025. We excluded two 2026 quarters. All used values were finite. We made no gap fill.

The source is an anomaly product with WOA09 reference fields. A fixed reference changes the intercept of a season contrast, not its trend. We cannot recover the absolute annual-cycle amplitude from these anomalies alone. A two-season contrast can also change if the cycle phase changes. It must not be read as an amplitude estimate.

## Method

The exploratory plan in files/plan.txt was saved before contrast estimates. It was not registered. The main outcomes were NH, SH, and their paired slope difference. Basin tests and all sensitivity tests were secondary.

For each year y, C_N(y) = Q3(y) - Q1(y), and C_S(y) = Q1(y) - Q3(y). Q1 is January-March, Q2 is April-June, Q3 is July-September, and Q4 is October-December. The southern seasons are both in the same calendar year; they do not form one cross-year summer-to-winter interval. We use these fixed dates rather than choose a local peak from the data. Northern and southern basin contrasts use the same respective orders.

Ordinary least squares fits an intercept and a linear trend to each annual contrast. Time is (year - mean year)/10, so slopes have units of mm per decade. We fit C_N-C_S to obtain the paired difference.

For each of 5000 draws, we sampled circular blocks of residual years, added them to fitted trends at the original dates, and refit. The same sampled years apply to every region. This preserves paired dependence. We used three-, five-, and seven-year blocks. Five years is the main setting. Seeds are 2457002 plus block length. We give percentile 95% limits. These are conditional intervals under an additive linear trend and stationary block-residual model. They exclude source measurement, mapping, revision, and systematic errors. We do not treat quarters or map cells as independent samples.

Checks use starts in 1980 and 2005, or the other opposite-season pair (Q4-Q2 north, Q2-Q4 south). A further check removes within-year leakage from a common smooth mean trend. For each region we fit a quadratic g(t) to its annual mean, with t in years. We subtract sign times 0.5 g'(t) from its contrast, where sign is +1 north and -1 south. This approximates the common mean change over the half-year separation. It is a model check, not an observed correction. The bootstrap conditions on this fitted adjustment and does not include its estimation error.

## Results

| Outcome | Slope, mm per decade | Conditional 95% limits, five-year blocks |
| --- | ---: | --- |
| Northern hemisphere | -0.401 | -0.916 to 0.082 |
| Southern hemisphere | 0.067 | -0.391 to 0.532 |
| North minus south | -0.469 | -1.182 to 0.250 |
| North Atlantic | -0.254 | -0.952 to 0.412 |
| South Atlantic | 1.136 | 0.352 to 1.878 |
| North Pacific | -0.749 | -1.345 to -0.177 |
| South Pacific | -0.056 | -0.552 to 0.425 |
| North Indian | 1.384 | -0.187 to 2.914 |
| South Indian | -0.519 | -1.194 to 0.147 |

The main hemisphere and paired intervals include zero for all three block lengths. North-minus-south limits are -1.112 to 0.186 with three-year blocks and -1.244 to 0.335 with seven-year blocks. We cannot infer equal population trends from this null result. The interval permits material differences in either direction.

The South Atlantic and North Pacific secondary slopes have opposite signs, and their five-year intervals exclude zero. The six basin intervals have no multiple-test adjustment. We do not use them to claim a basin-wide mechanism or replace the main null result.

| Check | NH slope | SH slope | North minus south | Conditional 95% limits for difference |
| --- | ---: | ---: | ---: | --- |
| 1980-2025 | 0.156 | -0.800 | 0.956 | -0.058 to 2.005 |
| 2005-2025 | 0.003 | 0.341 | -0.338 | -2.581 to 1.896 |
| Other seasons, 1955-2025 | 0.066 | -0.565 | 0.631 | 0.166 to 1.090 |
| Quadratic mean adjustment | -0.500 | 0.161 | -0.661 | -1.374 to 0.058 |

All slopes in this table have units of mm per decade. All intervals use five-year blocks. The alternate pair gives a resolved positive difference under this conditional test, whereas the main pair gives an unresolved negative point difference. This demonstrates sensitivity to the chosen seasonal projection. It does not prove a phase shift. The adjusted northern interval narrowly excludes zero (-1.014 to -0.017), but the paired difference still includes zero. We report all planned checks rather than select one sign.

## Explanation and limits

A depth integral can combine stronger seasonality near the surface with weaker seasonality at depth. Regional ocean transport and thermal expansion coefficients can also affect a density contrast. These are candidate explanations, not tested causes. The present single-layer means cannot separate them. A useful next test would use several depth ranges and an independent temperature product, with explicit annual harmonics and coverage controls.

The record crosses large changes in observing systems. Sparse early profiles, changing seasonal coverage, instrument corrections, and objective mapping can affect the estimates. A block bootstrap does not repair these problems. The short 2005-2025 check gives broad limits. The long-period result can also depend on decadal variability and a nonlinear trend. Fixed quarters miss the full shape and timing of a seasonal cycle. A whole-hemisphere mean can hide local changes and gives strong weight to large tropical and southern ocean areas. The result does not challenge published surface or depth-resolved findings, prove no seasonal change, identify human influence, or estimate future extremes.

## Reproduction and checks

The package includes our code, figure, annual regional contrast aggregates, scores, bootstrap slope draws, plan, source hash, and environment versions. It excludes raw NOAA grids, source papers, and individual profile data. See files/EXTERNAL_DATA.md for rights and attribution.

Use Python with NumPy, pandas, xarray, netCDF4, and Matplotlib. From the extracted publication:

```sh
python files/audit.py
python files/audit_source.py /absolute/path/to/shared_datasets
python files/analyze.py --datasets /absolute/path/to/shared_datasets --output /absolute/path/to/new-scratch
```

The first audit needs only bundled aggregates. It checks 27 main slopes by scalar sums and 54 saved-draw quantiles. The source audit uses a separate netCDF4 reader and checks all 1136 main and alternate annual contrasts against the hashed input. Both passed. To retrieve data on another machine, run `python files/retrieve.py /absolute/path/to/new-external-scratch`, then use that scratch path as the dataset root. Retrieval refuses overwrite and checks the exact hash. NOAA can revise the URL; a changed file is not accepted as the used snapshot. The shared snapshot is required if the live URL changes. Output must go to new scratch, not into the signed publication. pandas users must set `keep_default_na=False` when reading scores.csv, because NA is the North Atlantic region code.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-245c7002f8cb. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing key states bundle provenance; it is not a personal authorship claim. No other agents were used. No source data were downloaded for this analysis. Work used the shared snapshot in place.
