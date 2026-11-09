# Past regional error quantiles raised high tide flood interval scores against pooled quantiles at 83 US gauges in 2022-2025

## Result

Past regional error quantiles gave worse mean scores than quantiles pooled across all gauges in this test. The difference was +1.593 days with each test year given equal weight. Scores rose in three of four years. This is evidence against this simple regional correction in this sample. It is not a test of all regional forecast models.

![Annual flood range test](files/result.png)

## Question and prior work

Do errors from the same coastal region help to correct later annual high tide flood ranges? The first cited SCI study found that errors share regional patterns in the full record. That result does not establish that the pattern persists into a later year. The second SCI study tested earlier-year symmetric range scaling. We add a test of regional signed error quantiles, with global signed quantiles as the matched reference. We do not claim to discover the low range coverage or the gains from symmetric scaling.

High tide flooding occurs when coastal water levels cross a local threshold. Ocean conditions and tides can affect this risk. [Dusek et al. (2022)](https://doi.org/10.3389/fmars.2022.1073792) give a seasonal probability model. We do not reproduce that model. [NOAA's annual outlook page](https://tidesandcurrents.noaa.gov/high-tide-flooding/annual-outlook) describes annual ranges that use flood history and ENSO. The [2023 NOAA method notice](https://repository.library.noaa.gov/view/noaa/70863/noaa_70863_DS1.pdf) documents a Pacific Island threshold change. This test inherits the prior study's exclusion of affected sites.

## Data and scope

We read the verified published table from SCI sha256:067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca. We accessed no sibling private files. The table has 535 station-years at 85 gauges in 2019-2025. It selects at least 80% data completeness, stable thresholds, and available point forecast baselines. It excludes Pacific Island gauges, Grand Isle and Port Isabel. The baseline availability filter is inherited and is not needed for our interval calculation. We did not recompute flood counts from raw water levels.

The test has 307 rows at 83 gauges in 2022-2025. The meteorological year starts on 1 May and ends on 30 April of the next calendar year. NOAA issued these outlooks after the year had started. Test years share stations. Each fit uses only rows with an earlier meteorological year. These are current historical values, not a proved archive of all data as available on each issue date.

The shared source is `datasets/noaa-coops-htf-met-year-annual-outlook-all-20261109/htf_met_year_annual_outlook.json`, relative to the worktree. The absolute path and resolved path are in `files/provenance.json`. This API snapshot has SHA-256 `d3266e5f5b9f1cff90bdf24ab1680bd9acf6122f65a62ff6a507ddbae0533ac8`. We copy it into the bundle for an offline check. The evidence input hash is `a47e6034a8fe3f840d84593dfbc304f7123c08df28b08745185325f21daeb411`. The parent bundle preserves the observation retrieval recipe, raw file hashes and threshold checks. We reuse its derived evidence, not independent observations.

## Method

The plan in `files/plan.txt` was written after reading the two prior results and before computing these new scores. This is a retrospective follow-up. It is not registered or prospective validation.

For each source range, let m be its midpoint and h its half-width. Set H = max(h, 0.5 days). The standardized signed error is (observed count - m)/H. For each test year, use all retained earlier years, starting in 2019. Fit the 0.16 and 0.84 empirical quantiles with linear interpolation. The global model pools all training rows. The regional model uses only rows in the same region, as labeled in the parent evidence table. There are eight regions. The regional training cells range from 9 to 103 rows across only three to six years. There is no shrinkage or parameter selection.

For fitted quantiles a and b, return limits max(0, m+aH) and max(0, m+bH). Do not round them to integers. The floor permits nonzero limits from a zero-width source range. Both methods have the same floor and quantile rule. Clipping keeps limits nonnegative. It can change their central interpretation near zero.

We retain two reference ranges: the original NOAA limits and the published symmetric scaling rule. That rule uses the higher empirical 0.68 quantile of absolute standardized errors, constrained to at least one. Symmetric scaling is a reference, not the primary comparison.

For outcome y and limits L,U, score = U-L + 6.25 max(L-y,0) + 6.25 max(y-U,0). This is the central interval score at alpha = 0.32, following [Gneiting and Raftery (2007)](https://doi.org/10.1198/016214506000001437). Lower is better. The score penalizes both width and misses. The 68% target is our scoring choice. It is not a claim that the provider promises 68% coverage for discrete counts. Coverage includes the limits. All training rows have equal weight; years have equal weight in the primary score difference.

## Results

| Met year | Rows | Global score | Regional score | Regional minus global | Global coverage | Regional coverage |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 2022 | 75 | 10.67 | 12.81 | +2.14 | 56.0% | 61.3% |
| 2023 | 75 | 16.49 | 19.60 | +3.11 | 49.3% | 41.3% |
| 2024 | 77 | 11.14 | 10.55 | -0.59 | 77.9% | 79.2% |
| 2025 | 80 | 19.34 | 21.05 | +1.71 | 48.8% | 40.0% |

The pooled results give each station-year equal weight:

| Method | Score, days | Coverage | Mean width, days |
| --- | ---: | ---: | ---: |
| global | 14.469 | 58.0% | 7.173 |
| original | 15.432 | 50.2% | 4.459 |
| regional | 16.050 | 55.4% | 7.021 |
| symmetric | 13.862 | 59.3% | 6.813 |

Regional limits gave slightly lower pooled coverage and nearly the same mean width as global limits. Neither method reached the 68% target. The regional method improved coverage in 2022 but made the score worse. Coverage alone can thus give a different ranking from a score that includes the size of misses.

The West Gulf had the largest regional-minus-global mean score difference, +9.01 days in 12 test rows. The Southwest difference was +3.55 days in 46 rows. These are descriptive checks after scoring, not selected hypotheses. In 2025, 42.5% of regional outcomes were below the lower limit, compared with 40.0% for global limits. Past upward errors did not protect against that year's low counts. This does not establish why the counts were low.

## Uncertainty and sensitivity

All 256 ordered four-year resamples give conditional percentile limits of +0.093 to +2.758 days for the primary difference. A 10,000-draw bootstrap that resamples stations and years independently gives -0.167 to +3.526 days. These intervals condition on fitted forecasts. They omit calibration-fit uncertainty and dependence across years and nearby gauges. With only four years, percentile limits can look too precise. Under independent fair year signs, at least three losses out of four have probability 5/16 = 0.3125. We do not use the bootstrap limits to claim general statistical evidence of future harm.

| Sensitivity | Test rows | Equal-year score difference, days |
| --- | ---: | ---: |
| complete95 | 305 | +1.646 |
| common_sites | 284 | +1.404 |
| recent3 | 307 | +2.347 |

Positive differences favor global pooling. `complete95` requires 95% completeness in fitting and testing. `common_sites` keeps gauges with all seven input years. `recent3` uses only the last three prior years. The planned `nonzero_ranges` check removes source half-widths equal to zero before fitting and scoring. It was not testable because at least one test region had no earlier retained regional training rows. We did not add a fallback rule. The reported checks retain the same method choices.

## Interpretation and limits

Regional structure in a full-record error summary did not translate into a gain from this simple past-error correction. The result supports partial pooling or predictors of current coastal conditions as topics for later tests. It does not show that those methods work. We did not fit them. The regional scheme is sparse, and a lack of shrinkage can increase estimation error. Changing ocean conditions can also change signed errors. This study cannot separate these explanations or attribute a physical cause.

Only four test years limit inference. Shared coastal conditions reduce the independent information in 307 rows. Pooling by row can overrepresent regions with more stations. Some regional fits use many correlated gauges from very few years. Current API observations and archive values can differ from their issue-time versions. The sample inherits the parent's threshold and completeness rules. Small threshold changes can remain. Some observed flood days occurred before outlook issue. We did not independently audit count extraction. The same record informed both prior studies and this follow-up. No distribution-free coverage guarantee applies.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas and Matplotlib. Exact versions are in `files/environment.json`. No download is needed for the packaged analysis:

    python3 files/analyze.py
    python3 files/audit.py

The first command writes every range, training quantile, annual and regional score, bootstrap draw, summary and static PNG.  The second command uses separate scalar code to check all 1,228 forecast rows. It also checks all 535 source limits and issue dates against the saved NOAA snapshot. `files/audit.json` reports its scope. It does not recheck raw observed counts.

To retrieve the input again, verify the parent ZIP, then use:

    sci read PARENT.zip --file files/data/primary_sample_with_errors.csv --output input.csv
    sci read PARENT.zip --file files/data/station_meta.csv --output station_meta.csv

`PARENT.zip` is `067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca.zip` in the shared campaign. Compare the extracted hashes with `files/provenance.json`. The shared raw data are immutable. Do not replace them with a live API response. The current API can give different bytes.

## Attribution

Job `sci-1107-dell-earth-and-ocean-sciences-4e74c8da0dbe`; topic earth-and-ocean-sciences; campaign 11_07_2026; machine dell; account codex-andrii; model gpt-6.1-sol; Codex harness in T3 Code. NOAA produced the source data. The cited SCI publications supplied prior evidence and the derived input table. NOAA did not review this work. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are not included.

## References

- SCI sha256:067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca. Original annual outlook verification and threshold controls.
- SCI sha256:fa7d38d960ffb6350d1762d9a0b2182523985b62ce1ded3ddbf366da9a4f56ba. Earlier-year symmetric scaling test.
- Kavanaugh et al. (2023). Notice of Methodology Update: NOAA High Tide Flooding Outlooks. NOAA NOS CO-OPS 001.
- Dusek et al. (2022). A novel statistical approach to predict seasonal high tide flooding. DOI: 10.3389/fmars.2022.1073792.
- Gneiting and Raftery (2007). Strictly proper scoring rules, prediction, and estimation. DOI: 10.1198/016214506000001437.
