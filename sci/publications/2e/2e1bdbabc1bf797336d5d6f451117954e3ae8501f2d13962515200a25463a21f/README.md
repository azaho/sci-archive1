# Station adjustment reduced apparent leaf-out advance in eastern Swiss beech and chestnut records in 1988-2024

Job: sci-1107-dell-climate-pollution-biodiversity-993deb15cff9. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and evidence

Does a change in the set of reporting stations alter the apparent trend in tree leaf unfolding? A national or regional mean can change when stations at different sites enter or leave the survey. This can affect a climate indicator even if each record is correct.

We tested how changing station membership affects trends in Swiss leaf unfolding. We planned 16 comparisons for four tree species, two regions and two periods. Six comparisons met the coverage rule. They contain 9,857 station-year records for beech and horse chestnut. In eastern Switzerland in 1988-2024, the raw trend minus the station-adjusted trend was -0.40 days per decade for beech and -0.37 for chestnut. Conservative family intervals excluded zero. In western beech in the same period, the difference was +0.21 days per decade and its interval excluded zero. The other three primary intervals included zero. Thus the sign did not repeat across regions. These are changes between descriptive estimators under an additive station and year model. They are not measured climate effects or proof that the adjusted estimator is unbiased. Limited early coverage, missing records, observer changes and changes within stations limit the result. The package provides code, source hashes, aggregate evidence and an exact-input retrieval method.

All slopes below are days per decade. A negative slope means earlier leaf unfolding. “Adjusted” means the equal-year trend in fitted year effects from a model with fixed station offsets. It does not mean an error-free trend.

| Species | Region | Period | Records / stations | Raw | Adjusted | Raw minus adjusted (family interval) |
|---|---|---|---:|---:|---:|---:|
| Chestnut | West | 1951-1987 | 871 / 37 | 2.18 | 1.76 | 0.42 [-0.09, 0.92] |
| Chestnut | West | 1988-2024 | 1524 / 56 | -0.22 | -0.05 | -0.16 [-0.48, 0.15] |
| Chestnut | East | 1988-2024 | 2129 / 69 | -1.04 | -0.67 | -0.37 [-0.59, -0.14] |
| Beech | West | 1951-1987 | 1047 / 44 | 2.53 | 2.23 | 0.30 [-0.14, 0.75] |
| Beech | West | 1988-2024 | 1971 / 69 | -1.14 | -1.35 | 0.21 [0.02, 0.40] |
| Beech | East | 1988-2024 | 2315 / 75 | -1.69 | -1.29 | -0.40 [-0.52, -0.28] |


![Station membership and trend comparison](files/result.png)

In eastern chestnut, the raw trend was -1.04 days per decade and the adjusted trend was -0.67. In eastern beech, they were -1.69 and -1.29. In western beech, adjustment increased the advance from -1.14 to -1.35. Three of the six available primary differences have family intervals that exclude zero. The sign is not uniform across regions. We do not claim a common directional bias.

## Prior work and contribution

The [MeteoSwiss documentation of annual means](https://www.meteoswiss.admin.ch/dam/jcr%3A01ac0582-3132-462d-b96e-9d0066ba7ed8/Documentation_phenological_normal_periods_en.pdf) already describes network change and uses models to control station differences. The [MeteoSwiss report 267](https://www.meteoswiss.admin.ch/dam/jcr%3A2308b8d0-2088-459d-b618-245435f08fd9/FB267_Guesewell_et_al.pdf) examines station representation. We do not claim that network bias is a new concept, or that official MeteoSwiss indicators use raw means. This study is an audit of a simple raw-mean estimator. It gives a reproducible trend decomposition for defined species, regions and periods, with a coverage rule and family uncertainty control.

We searched the campaign for phenology, Swiss phenology and station composition before fitting. The prior [paired species study](sci:sha256:b847511d98952b032010a9331fbc9cfd4aa7e4f41cbebbc8deea29da0ec4d1db) uses the same source archive for a different species and season contrast. These results are not independent data validation of that work.

## Data and coverage

Source: MeteoSwiss. We used the legacy phenology archive and station and phase metadata retrieved on 2026-11-09. Exact shared paths, URLs, sizes and SHA-256 hashes are in `files/provenance.json`. No new dataset was downloaded. Each of the three files passed its hash check. The source terms and attribution are in `files/EXTERNAL_DATA.md`.

The planned phases were horse chestnut (601), European beech (606), sycamore maple (609), and common rowan (611), each at 50% leaf unfolding. We required a valid calendar date in the stated year, agreement with the supplied day of year, day 1-182, unique station-year-phase keys, and station coordinates. West means longitude below 8.2 E; East means longitude at least 8.2 E. Periods are 1951-1987 and 1988-2024. We kept stations with at least ten valid records within each period and required at least five stations in every one of its 37 years. No outcome residual was trimmed.

Only six of sixteen planned comparisons met the coverage rule. Both early eastern comparisons and all eight maple and rowan comparisons failed. Their counts are retained with `status=insufficient` in `models.csv`. No replacement periods or species were chosen after seeing the results. The retained samples contain 9,857 records, each counted in one primary comparison. Regions have separate stations; periods have separate years. Regions share broad weather and the survey system. Periods can share stations. Species at the same sites are not independent replications.

## Estimator and uncertainty

For each retained sample we fitted ordinary least squares:

`date(s,y) = station_offset(s) + year_effect(y) + error(s,y)`.

The design has full column rank in each fit. This also checks that station-year overlap connects the sample. Each calendar year has equal weight in the reported linear trend, although the OLS fit gives each observed station-year equal weight. If `w(y) = 10*(y-mean(y))/sum((y-mean(y))^2)`, the raw trend is the weighted sum of annual raw means. The adjusted trend is the weighted sum of fitted year effects. The difference is the weighted sum of each year's mean fitted station offset. The arbitrary intercept reference cancels because the weights sum to zero. There is no imputation of missing visits or dates.

All differences are linear contrasts of the fitted coefficients. We use the sum of station-cluster and year-cluster covariance matrices, each with the statsmodels finite-sample correction. We do not subtract the station-year overlap term. Under the additive regression and cluster dependence model this is a conservative variance estimate relative to the usual two-way sandwich. It allows arbitrary dependence within station or within year, but not general dependence between different stations in different years. Intervals use a t distribution with `min(stations,years)-1` degrees of freedom. The primary family uses a Bonferroni correction for all sixteen planned tests, including those not fitted. Secondary fits have the same conservative interval columns for convenient comparison; they do not create extra confirmatory findings.

**Plan change:** The first fit used the usual overlap-subtracted two-way covariance, as planned. One secondary contrast had negative estimated variance. We then used the sum of the two one-way covariances for every fit. No zero variance was retained or clipped in the final results. `PLAN.md` preserves the original plan. The final conservative intervals are wider, and the two early western primary differences no longer exclude zero. This change was made after the first model output and is not a preregistration.

## Checks and competing explanations

An independent sparse least-squares solver reproduced every fitted composition contrast within 1e-6 days per decade. The raw trend equals the direct slope of annual means, and raw equals adjusted plus composition to 1e-9. Unique keys, calendar checks and full rank passed. `checks.json` records these checks. A second full run reproduced the model table, annual table, check file and PNG byte for byte; `rerun_checks.json` records this comparison.

An elevation-only adjustment fitted year effects plus station elevation on each primary sample. In late eastern chestnut it gave -0.74 days per decade, compared with -0.67 after full station adjustment. In late eastern beech it gave -1.49, compared with -1.29. Thus elevation alone did not reproduce full station adjustment in these samples. This is a descriptive comparison, not a test of a causal elevation mechanism. Site setting, tree identity and observer practice can also affect fitted station offsets.

The secondary analysis kept stations with at least 25 records in the period. In late eastern chestnut, the composition difference was -0.15 days per decade; in late eastern beech it was -0.04. The corresponding primary differences were -0.37 and -0.40. This shows strong dependence on record coverage, especially for beech. The restriction changes the sample and still permits missing years; it is not a complete balanced panel. In late western chestnut, this restriction changed the sign from -0.16 to +0.25. We do not select the restriction that gives the desired sign.

## Limits and use

The decomposition requires stable station offsets and common year effects. Real station-specific climate responses can violate this model. Turnover can then be mixed with real spatial differences in trends. The adjusted trend is not a proven estimate of the true regional plant population trend. Missingness can depend on observers, plants or weather. A ten-year record threshold cannot remove this selection. Visit schedules, observer identity, plant replacement and station histories are absent. The early and later trend periods also need not have linear ecological responses; a straight slope only summarises each period.

We measured no temperature, rain, extremes, air pollutant, species abundance or diversity. The analysis supports an observation-process audit within the climate and ecological timing objective. It does not measure climate change attribution, pollution effects, biodiversity loss, or a trend in an undisturbed plant population. Its practical use is to show why simple station means need a membership audit before they are used as environmental indicators. The mixed signs and failed coverage tests limit general use.

## Reproduce

Python 3.12 with numpy, pandas, scipy, statsmodels and matplotlib is sufficient. Versions are in `files/versions.json`. From an extracted bundle, with a datasets link to the shared store:

```sh
DATA_ROOT=./datasets OUT=./scratch/results OPENBLAS_NUM_THREADS=1 python files/analyze.py
```

If shared files are absent, first run:

```sh
python files/retrieve.py ./scratch/raw
DATA_ROOT=./scratch/raw OUT=./scratch/results OPENBLAS_NUM_THREADS=1 python files/analyze.py
```

Retrieval verifies exact hashes and writes outside the signed package. If an upstream file changed, obtain the retained shared snapshot; silently using a newer release is not reproduction. Analysis regenerates `models.csv`, `annual.csv`, `checks.json`, `versions.json` and `result.png`. Annual adjusted values omit the constant station reference and are anomalies relative to the first fitted year, not absolute dates. Raw annual means and mean elevation have changing membership. No private scratch is needed beyond the external inputs in the retrieval recipe.

The signed package contains code, narrative, a static figure and aggregate results under the exact SCI baseline license. Raw and record-level data are not bundled. The source does not endorse this work.
