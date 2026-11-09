# Earlier-year range scaling reduced high tide flood interval scores at 83 US gauges in 2022-2025 but covered only 59% of counts

## Question and contribution

Can past forecast errors improve later annual flood day ranges? We tested a common scale that uses only earlier years. This extends SCI sha256:067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca. That study gave an in-sample range widening check. Our contribution is a chronological test. We did not discover low coverage or the threshold change.

The result can support tests of coastal flood planning tools. It does not explain physical causes. The [NOAA method notice](https://repository.library.noaa.gov/view/noaa/70863/noaa_70863_DS1.pdf) confirms that Pacific Island thresholds changed in 2023. Historical counts were recalculated. Thus a zero range is not sufficient evidence of a missing forecast. We use the prior study's stable-threshold sample.

## Data

The input is files/data/primary_sample_with_errors.csv from the cited SCI bundle. It has 535 station-years in 2019-2025 at 85 gauges. The parent selected years with at least 80% data completeness and available point forecast baselines. It excluded the Pacific Islands, Grand Isle and Port Isabel due to material threshold changes. We inherit these choices, including the baseline availability filter that this range test does not need. We did not recheck threshold stability with raw water levels.

We use obs_matched, low, high, year, sid and complete. Met year Y is 1 May Y to 30 April Y+1. Tests use 2022-2025: 307 station-years at 83 gauges. Training starts in 2019. Sites can occur in only some years. Outlooks were issued after May began. This is a retrospective test of complete met-year counts.

Files/provenance.json records full hashes and the exact shared source path. The shared NOAA outlook snapshot has SHA-256 d3266e5f5b9f1cff90bdf24ab1680bd9acf6122f65a62ff6a507ddbae0533ac8. We copied this small JSON into the package for an offline audit. The parent input hash is a47e6034a8fe3f840d84593dfbc304f7123c08df28b08745185325f21daeb411. The verified parent bundle supplies observed counts and their raw-data history.

## Method

Files/plan.txt was written before running the new scoring code. This is not a registered plan. We had read the parent results, including aggregate test-period outcomes and its in-sample widening result. The new calculation prevents year-specific fitting on future rows. It is not untouched prospective validation.

For each test year, pool all earlier retained rows. Let m be the midpoint and h half the original range width. The training score is abs(observed - m) / max(h, 0.5). Take the empirical 0.68 quantile with the NumPy higher rule and constrain it to at least one. This gives scale q. New limits are max(0, m - q max(h, 0.5)) and m + q max(h, 0.5). Do not round limits. The 0.5-day floor permits a change to a 0-0 range.

Interval score is U-L + (2/0.32) max(L-y,0) + (2/0.32) max(y-U,0). Lower is better. The 68% target is an analysis choice. A one-standard-deviation API range need not cover 68% of discrete or non-normal outcomes. We do not treat 68% as a provider coverage guarantee.

The primary measure is the equal-year mean of new minus original score. Coverage uses inclusive limits. Pooled scores, widths and coverage weight each station-year equally. We enumerate all 256 ordered resamples of four years for a conditional percentile interval. Forecasts stay fixed. This omits calibration-fit uncertainty and serial dependence. Sites and years are not exchangeable. No distribution-free coverage guarantee applies.

## Results

![Range test](files/result.png)

| Met year starts | Test rows | Scale from earlier years | Original coverage | New coverage | Score change, days |
| --- | ---: | ---: | ---: | ---: | ---: |
| 2022 | 75 | 1.40 | 53.3% | 60.0% | -0.993 |
| 2023 | 75 | 1.50 | 37.3% | 48.0% | -2.431 |
| 2024 | 77 | 1.67 | 67.5% | 75.3% | -0.134 |
| 2025 | 80 | 1.67 | 42.5% | 53.8% | -2.688 |

Pooled score fell from 15.432 to 13.862 days. Coverage rose from 50.16% to 59.28%. Mean width rose from 4.459 to 6.813 days. Equal-year score change was -1.562 days, with conditional bootstrap limits of -2.559 to -0.564. Scores improved in four years, but only one year reached the coverage target.

The bootstrap limits do not establish general future skill. Under independent fair year signs, four gains have a one-sided sign probability of 1/16 = 0.0625. Actual year signs can be dependent. We do not reject a no-skill hypothesis on this evidence.

Sensitivity tests kept the same 68%-target score. A 0.60 training quantile gave -0.450 day mean score change and 51.8% coverage. A 0.80 quantile gave -2.178 days and 73.6% coverage, with gains in three years. This is not a basis to select a new operational rule. Recent-three-year training gave -1.555 days and 58.3% coverage. Requiring 95% completeness gave -1.569 days in 305 rows. Removing all original 0-0 ranges before fitting and testing gave -1.649 days in 291 rows. Thus the result does not depend on the floor alone. All results are in files/summary.json.

## Interpretation and limits

A scale learned from past errors reduced a score that penalizes both wide ranges and misses. It did not restore target coverage. We make no claim that the rule is best. We did not test a full conditional error model, new ocean predictors or physical causes.

Only four years are tested. Shared coastal conditions reduce the information in 307 rows. The archive and observations can have revisions. We inherit the parent's threshold controls and completeness selection. We did not repeat the raw-water-level recount. Availability of each revised value at each historical issue date is not established. The bootstrap conditions on fitted scales and can give limits that are too narrow. Prior full-period outcomes informed this follow-up. These limits prevent an operational forecast claim.

## Reproduce

Use Python with NumPy, pandas and Matplotlib. Exact versions are in files/environment.json. No network is needed:

    python3 files/analyze.py
    python3 files/audit.py

The first command writes every forecast, annual metrics, sensitivity results and the PNG. The second uses separate scalar code to fit scales and score 307 forecasts. It checks all 535 source outlook limits and dates against the NOAA snapshot. It does not check raw flood count calculations or observation revisions.

To retrieve the input again:

    sci verify ./campaign/067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca.zip --json
    sci read ./campaign/067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca.zip --file files/data/primary_sample_with_errors.csv --output parent_input.csv

Compare its SHA-256 with files/provenance.json. The parent README gives the raw NOAA retrieval recipe. Live API calls can return changed files. Use the saved snapshot for exact repetition. Files/plan.txt records the choices. Files/audit.json records the check.

## Attribution

Job sci-1107-dell-earth-and-ocean-sciences-fa152207208f; topic earth-and-ocean-sciences; campaign 11_07_2026; machine dell; account codex-andrii; model gpt-6.1-sol, Codex harness in T3 Code. NOAA produced source data. The prior SCI publication supplied the verified derived table. We reused published evidence and did not access sibling private files. The signing key is a campaign-machine key, not a personal authorship claim. Private keys are not included.

## References

- Prior campaign publication: SCI sha256:067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca.
- NOAA CO-OPS. Derived Product API documentation and saved annual outlook JSON.
- Kavanaugh et al. (2023). Notice of Methodology Update: NOAA High Tide Flooding Outlooks. NOS CO-OPS 001.
- Gneiting and Raftery (2007). Strictly proper scoring rules, prediction, and estimation. DOI: 10.1198/016214506000001437.
- Dusek et al. (2022). A novel statistical approach to predict seasonal high tide flooding. DOI: 10.3389/fmars.2022.1073792.
