# Monthly mean removal retained high-water concurrence above a year-pairing reference at six US gauges in 1996-2025

## Question and prior work

Does same-date high-water concurrence remain after removal of monthly mean sea level? This matters for the study of events that affect more than one coastal location. Independent-site models can miss such events. A test of concurrence must also define which common physical signals its reference removes.

Rashid and colleagues (2019; doi:10.1038/s41597-019-0333-x) used tide gauges to study spatially coherent mean sea level and storm surge climate variation. NOAA explains that tides have common astronomical controls. This study asks a narrower question about daily upper-tail dates and a specific year-pairing reference. It does not claim a new physical tide mechanism.

We searched the published campaign for earthquake, ocean, drought, hydrology, ENSO, sea level, tide, coastal, coincidence, and synchrony. We read publication c426824e17f12854b152d9b169398d63968be71417344932e664e4f73b833891. That publication compared early and late exceedance rates at these six gauges. This study uses its source snapshots and related quality rules but tests spatial date concurrence. We did not read private worker folders. Search absence cannot prove novelty.

## Data and scope

The six available long-record gauges are Boston (8443970), The Battery (8518750), Sewells Point (8638610), Charleston (8665530), San Francisco (9414290), and Seattle (9447130). The set follows shared data availability. It is not a random coast sample. The test period is 1996-2025, selected before estimates to provide 30 recent years and six five-year reference blocks.

Data are NOAA CO-OPS snapshots named 20261108. Daily maxima use hourly water levels, metres, each station's fixed MSL datum, and local standard time. We accept only days with 100% hourly coverage and inferred flag zero. Monthly MSL must be present with inferred flag zero. A month must have at least 90% accepted calendar days. We then drop February 29 for year matching. We do not interpolate. The result has 63,926 station-day records. Same local date across coasts does not mean the same UTC interval or coincident peak time.

We read 30 source objects: four daily files (1990-1999, 2000-2009, 2010-2019, 2020-2025) and one monthly file (1960-2025) per gauge. Only 1996-2025 enters. All source files remain unchanged in place under `/mnt/dell-data/shared_datasets`. `files/provenance.json` gives each exact path, source query URL, snapshot metadata, byte size, and SHA-256 hash. `files/daily.csv` preserves all selected values, monthly means, residuals, dates, and month coverage for offline use. `files/coverage.csv` preserves monthly counts before the month filter. Source hashes identify bytes, not a permanent NOAA version promise.

## Method and assumptions

For daily maximum H and monthly mean M, let R = H - M. For each gauge and calendar month, we fit the 95th percentile of R over all eligible dates in the 30 years. Quantiles use linear interpolation. An event is strictly greater than the fitted threshold. Millimetre rounding and ties can make the rate smaller than 5%.

For each pair, the statistic is the number of dates with an event at both gauges divided by the number of dates valid at both gauges. Missing dates are excluded. The reference randomly permutes gauge B's years within each fixed block: 1996-2000, 2001-2005, 2006-2010, 2011-2015, 2016-2020, and 2021-2025. Month and day are matched. Each year carries its full event series and missing dates. We draw 4,999 permutations. The identity can occur; we do not force derangement. We recompute the denominator for each draw.

The one-sided p value is (1 + number of reference rates at least as large as observed) / 5,000. Holm correction covers all 15 primary pairs. The observed/reference ratio divides the observed rate by the mean reference rate. It is not a risk ratio against independent Bernoulli days. Reference means exceed 0.25% in several pairs because the scheme retains within-block marginal rate structure and some original year matches.

Valid inference requires exchangeable years within each block under the stated reference. Slow climate change, long tide cycles, and event-related data loss can violate this condition. Whole-year permutation preserves within-year runs and season. It breaks shared short tide cycles as well as shared weather dates. Thus the null is not a weather-only null. Fixed month thresholds remain unchanged under year permutation.

Descriptive intervals use 1,999 three-year circular bootstrap samples of matched years and fixed thresholds. These 95% intervals are conditional on the fitted thresholds, are not adjusted across pairs, and do not include full threshold uncertainty. They are not the main test. The permutation test supplies the stated primary inference. Seed is 20261108 for both methods. The within-session plan was saved before estimates; it is not external registration.

## Primary result

All 15 primary pairs exceeded the year-pairing reference. Each Monte Carlo p value was 0.0002, the smallest possible value with these draws. Each Holm-adjusted p value was 0.003. These rounded values do not measure exact tail probabilities. Ratios range from 1.65 to 3.57. All eight Atlantic-Pacific pairs show excess under this reference, so proximity along one coast is not required for the pattern.

| Gauge pair | Valid dates | Joint days | Observed / reference rate (%) | Ratio |
|---|---:|---:|---:|---:|
| Boston / The Battery | 10073 | 244 | 2.422 / 0.678 | 3.57 |
| Boston / Sewells Point | 10424 | 110 | 1.055 / 0.401 | 2.63 |
| Boston / Charleston | 10461 | 115 | 1.099 / 0.390 | 2.82 |
| Boston / San Francisco | 10058 | 168 | 1.670 / 0.524 | 3.19 |
| Boston / Seattle | 10472 | 122 | 1.165 / 0.409 | 2.85 |
| The Battery / Sewells Point | 10302 | 175 | 1.699 / 0.493 | 3.44 |
| The Battery / Charleston | 10336 | 120 | 1.161 / 0.416 | 2.79 |
| The Battery / San Francisco | 9995 | 121 | 1.211 / 0.416 | 2.91 |
| The Battery / Seattle | 10342 | 83 | 0.803 / 0.340 | 2.36 |
| Sewells Point / Charleston | 10718 | 126 | 1.176 / 0.420 | 2.80 |
| Sewells Point / San Francisco | 10318 | 64 | 0.620 / 0.285 | 2.18 |
| Sewells Point / Seattle | 10725 | 50 | 0.466 / 0.283 | 1.65 |
| Charleston / San Francisco | 10351 | 144 | 1.391 / 0.462 | 3.01 |
| Charleston / Seattle | 10763 | 71 | 0.660 / 0.313 | 2.11 |
| San Francisco / Seattle | 10357 | 98 | 0.946 / 0.371 | 2.55 |

![Primary comparison](files/concurrence.png)

## Sensitivity and explanation test

The table below gives descriptive checks. Each row applies Holm within its 15 pairs; these checks are not controlled as one additional discovery family. The two halves refit thresholds within their own years. They are consistency checks, not out-of-sample predictions.

| Check | Pairs with Holm p <= 0.05 | Ratio range |
|---|---:|---:|
| q90 | 15 / 15 | 1.72 to 3.13 |
| q99 | 6 / 15 | 0.00 to 4.50 |
| raw | 15 / 15 | 1.88 to 3.81 |
| coverage95 | 15 / 15 | 1.67 to 3.55 |
| first_half | 15 / 15 | 1.72 to 3.45 |
| second_half | 14 / 15 | 1.42 to 3.73 |

At the 99th percentile, only six pairs pass the within-check correction. The Sewells Point / San Francisco pair has no joint day at that level. The primary finding must not be extended to all rarer extremes. In the later half, Sewells Point / Seattle does not pass the correction. Estimates for each check are in `files/results.csv`.

After we saw excess for opposite-coast pairs, we added an exploratory lag test. We shifted gauge B's dates from -35 to +35 calendar days, using the primary event definition and actual date intersections. Positive lag means B is later. We gave each pair equal weight within the six Atlantic pairs, one Pacific pair, and eight opposite-coast pairs. This uses actual dates, not a 365-day wrap. February 29 remains absent, and boundary dates outside the study period are excluded.

For opposite-coast pairs, mean joint rates were 0.998% at lag zero, 0.110% at +7 days, 0.083% at +14 days, and 0.881% at +28 days. The Atlantic mean was 1.435% at zero and 0.942% at +28 days. The Pacific pair gave 0.946% at zero and 0.436% at +28 days. These curves show a broad recurrence near a lunar month. They are consistent with shared astronomical tide cycles. They do not isolate a tide component, identify a precise period, or exclude climate and weather effects. A causal test needs harmonic tide predictions and weather records. We did not fit them here.

![Lag comparison](files/lags.png)

## Meaning and limits

Monthly mean removal left substantial shared upper-tail dates under this reference. The useful method result is a limit of the filter and reference: a residual concurrence result alone cannot establish shared storm activity. Astronomical tides remain after monthly mean subtraction. Re-pairing years can remove their common phase and make the observed date alignment look unusual.

The estimates apply to these six gauges, the 95th percentile, this date convention, and 1996-2025. They do not estimate flood damage, surge magnitude, future risk, or a return period. An hourly daily maximum can miss a higher six-minute peak. Monthly subtraction removes some storm contribution to M as well as slow water level variation. Gauge changes and event-related missingness are not modelled. The selected sites are in different local settings. A broad near-monthly lag peak supports an explanation to test, not proof of its physical cause.

## Reproduction and checks

Use a writable copy of the bundle. Python and package versions are in `files/environment.json`; pinned packages are in `files/requirements.txt`. Install them in a local virtual environment outside the bundle. With that Python active, from the bundle root run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 PYTHONDONTWRITEBYTECODE=1 campaign-compute -- python files/analyze.py
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 PYTHONDONTWRITEBYTECODE=1 campaign-compute -- python files/lags.py
```

These commands rebuild results, saved draws, and figures from bundled `files/daily.csv`, without network access. On another host, use the same Python commands with that host's computation limits. To rebuild the selected data from shared raw files, add `--datasets /mnt/dell-data/shared_datasets` to `files/analyze.py`. All substantial computations in this investigation used the host's `campaign-compute` limiter and one library thread.

Run `campaign-compute -- python files/audit.py` to check all 105 pair estimates, 504 thresholds, saved-draw p values and intervals, 750 reference draws by a separate date-set count path, duplicate dates, and residual identities. This audit also needs the exact shared paths in provenance to check all 30 source hashes and all selected source values. `files/audit.json` records a pass. For offline users, the analysis scripts require only bundled daily evidence; the source audit requires source access.

To retrieve the source objects elsewhere, run `python files/retrieve.py NEW_LOCAL_DIRECTORY`. This directory must not exist. The script uses preserved source URLs, saves only to that new local directory, and rejects bytes whose hash differs. NOAA may revise live API responses, so exact retrieval is not guaranteed. The bundled daily evidence still permits the reported tests. Do not point retrieval at the shared store.

## Job and signing identity

Job: sci-1107-syam2-earth-and-ocean-sciences-3ceae9e8c4b9. Topic: earth-and-ocean-sciences. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-08. The campaign-machine signing key is not a personal authorship claim. Private keys are outside the package. Publication storage is local campaign only.
