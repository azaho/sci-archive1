# Winter and summer lead signs remained opposite after predicted tide midpoint removal at two US gauges in 2015-2024

We tested a known seasonal change in one-day water-level timing between Sewells Point and Charleston. The signs stayed opposite after smooth mean removal and a fixed lunar-cycle fit in 1960-2024. An added check used full NOAA hourly tide predictions for 2015-2024. After predicted midpoint removal, the north-lead minus south-lead correlation was -0.105 in winter and +0.300 in summer. The summer-minus-winter difference was 0.404. Its conditional 95% two-year block interval was 0.288 to 0.540. This is evidence that these filters do not explain the seasonal reversal. It is not evidence for a specific wave, storm path, or causal link.

![Seasonal timing after tide midpoint removal](files/tide.png)

## Question and prior work

Campaign publication `sci:sha256:1bec768cd1ebff7b74eb80f0dbae4eb1dfa27a858443c665d84fe1cd4a0777e5` found different lead signs at three Atlantic gauge pairs. Its season check found an opposite winter and summer sign at Sewells Point and Charleston. We test the sensitivity of that result to the mean filter and to tide representation. We do not claim a first detection of this seasonal pattern. We use the same observations. This is a small method extension, not independent confirmation.

Lentz (2024, doi:10.1029/2024JC021269) shows that local and remote wind can shape coastal sea level in the Middle Atlantic Bight. That work gives a reason to test spatial timing, but it does not predict our seasonal sign at these two sites. The present test cannot separate shared forcing from propagation. NOAA documents the hourly extrema, completeness and inferred flags in its API response guide. The source links are in sci.json.

We searched the public campaign before fixing this question. The search terms are in files/search_record.txt. We read published reports, not private worker folders. The initial plan is in files/plan.txt. We fixed the long-period filters before computing their results. We added the shorter full-tide check after seeing those results and after finding preserved tide predictions in another publication. The title highlights that added analysis. It is exploratory. This was not an external registration or an untouched test sample.

## Data

The two sites are Sewells Point, Virginia (8638610, northern site N), and Charleston, South Carolina (8665530, southern site S). Shared data availability and the prior result set the sites. All dates use local standard time in the same time zone. Observed heights are metres on each site's fixed MSL datum. We use 14 NOAA CO-OPS daily_max_min objects, labelled 20261108, for 1960-2025. We restrict the analysis to 1960-2024, as in the prior study. The API has no immutable source version.

For each day we require finite hourly maximum H and minimum L, H >= L, absolute heights below 100 m, 100% hourly completeness for both, and inferred flag zero for both. Each station-month must have at least 90% valid calendar days. No observation is filled. Sewells Point retains 23,142 days and Charleston retains 22,815 days. Missing data may depend on storms. All results are conditional on the retained record.

files/provenance.json records exact paths under `/mnt/dell-data/shared_datasets`, URLs, source receipts, byte counts and SHA-256 hashes of all 14 used observation files. Only those named objects were hashed. Raw shared data were read in place and were not changed. files/daily.csv preserves both accepted extrema. files/coverage.csv gives all month decisions.

For the added analysis, we use 20 annual hourly NOAA prediction responses for the two sites in 2015-2024. The exact responses are preserved in published bundle `sha256:154b66db1e7043562283ea709633f7868d1b3d3c59516bd98b4af2b77c0f4c6b`. That bundle passed complete SCI verification. Our code read those entries and checked each source hash. Each date has 24 predicted hours. files/prediction_provenance.json gives the parent ID, entry path, URL, source hash and fetch time. files/predictions.csv contains the rebuilt daily extrema. No new data download was needed. A second published prediction study, `86679eca`, helped locate this source. Its daily file was inspected for format and used for a source check; it did not supply the analysis values. All 7,300 common station-days have matching predicted extrema. Our rebuild also keeps six leap days omitted in that file. files/prediction_audit.json records this check.

NOAA predictions were fetched retrospectively in November 2026. They have no immutable constituent version. The predicted maxima and minima need not occur at the same hours as the observed extrema. Their subtraction is not a matched-hour surge residual. No raw hourly observation series is used.

## Measure and uncertainty

Let C = (H+L)/2. This midpoint is not a daily mean. For northern and southern anomaly series X_N and X_S, define

D = corr(X_N(t), X_S(t+1)) - corr(X_S(t), X_N(t+1)).

Positive D means a larger north-to-south one-day lead association. Negative D means a larger south-to-north association. Both correlations use the same four-value date pairs. The dates must be consecutive and in the same calendar month. No pair crosses a data gap or a month end. Winter is December, January and February. Summer is June, July and August. Winter is grouped by calendar year; December is not joined to the next January. We do not fit event paths or travel speeds.

The long-record baseline subtracts each accepted station-year-month midpoint mean. The smooth filter places these means on day 15 and linearly interpolates between them. It excludes dates outside the first and last anchors or between anchors more than 62 days apart. It never fills an observation gap. The fixed-cycle fit projects the smooth residual onto an intercept and sine and cosine terms at 13.660791, 14.765294, 27.554550 and 27.321582 days. Each term is multiplied by 1, annual sine and annual cosine, with annual period 365.2425 days. This gives 25 columns per site including the intercept. The epoch is 1960-01-01. All retained years enter the fit. A check keeps only the first two periods. This projection is a sensitivity filter, not a full astronomical tide model.

For each direction, season and year, we save the six Pearson moments. We draw 9,999 paired circular five-year block samples of 65 year labels. Seed is 792. Each sampled year retains all its observed daily pairs. The same year labels serve both seasons and filters. We form D and summer-minus-winter D in each draw. Three- and ten-year blocks are checks. Intervals are percentile limits. They hold fitted filters and mean estimates fixed. They do not include uncertainty in site selection, source errors or filter choice. All 95% intervals are pointwise; they are not a family-wide guarantee.

For the 2015-2024 check, define predicted midpoint P = (predicted daily maximum + predicted daily minimum)/2. We subtract P from C with coefficient one and then remove each station-year-month residual mean. We compare this with monthly-centered C on the identical retained dates. There are 861 winter date pairs and 870 summer date pairs. Paired circular two-year samples of ten calendar year labels give 9,999 draws, seed 793. One- and three-year blocks are checks. Ten years is a short basis for interval estimation.

## Results

| Long-record filter, 1960-2024 | Winter D | Summer D | Summer minus winter, 95% interval |
|---|---:|---:|---:|
| Monthly steps | -0.147 | 0.392 | 0.539 [0.476, 0.603] |
| Smooth means | -0.148 | 0.392 | 0.539 [0.477, 0.604] |
| Smooth plus four lunar cycles | -0.149 | 0.393 | 0.543 [0.476, 0.613] |
| Smooth plus two lunar cycles | -0.149 | 0.389 | 0.538 [0.472, 0.606] |

With the four-cycle filter, the winter interval is -0.192 to -0.107 and the summer interval is 0.350 to 0.438. The filters retain 5,148 winter and 5,403 summer date pairs. The monthly-step baseline has 5,209 and 5,450; smooth filtering removes some edge and gap-adjacent dates. The baseline comparison therefore has a small support difference. It is not a precise decomposition of filter effects. The signs also repeat with three- and ten-year blocks and in both 1960-1992 and 1993-2024. The early estimates are -0.183 and +0.436; late estimates are -0.115 and +0.357. We do not test a change between periods.

The four-cycle projection removes only 0.80% of smooth-residual variance at Sewells Point and 2.89% at Charleston. Its small effect on D is weak evidence about tides in general. This limit motivated the added full-prediction check.

![Long-record filter checks](files/season.png)

| Tide check, 2015-2024 | Winter D, 95% interval | Summer D, 95% interval | Summer minus winter, 95% interval |
|---|---:|---:|---:|
| Observed midpoint | -0.109 [-0.189, -0.026] | 0.310 [0.214, 0.408] | 0.419 [0.299, 0.555] |
| Minus predicted tide midpoint | -0.105 [-0.186, -0.024] | 0.300 [0.200, 0.409] | 0.404 [0.288, 0.540] |

The paired change in seasonal contrast after tide subtraction is -0.0149 [-0.0329, +0.0037]. We cannot resolve a change in this contrast under this block model. Both seasonal signs remain opposite under one- and three-year blocks. The corrected summer-minus-winter intervals are [0.274, 0.560] and [0.321, 0.505], respectively. All estimates and draws are preserved. The predicted tide midpoint does not account for the reversal in this retained ten-year sample. This is the new empirical constraint.

## Limits and use

A fixed-cycle fit can miss phase changes and local tide effects. Full predicted-midpoint subtraction still differs from subtraction at matched hours. Tides and weather can interact. Gauge-based tide predictions can also include periodic weather effects. The daily maximum and minimum can come from different tide cycles. Hourly sampling and the daily time limits can create timing structure. We cannot exclude those effects.

Moving weather, shared pressure, remote waves and different local response delays can each produce a lead contrast. We have no wind, pressure, storm tracks, river flow, waves or matched-hour residuals. Thus the pattern is unexplained in a physical sense. We do not identify a coastal wave, direction of causal influence, flood threshold, operational forecast benefit or propagation speed. The result is useful as a constraint: a proposed explanation should reproduce the opposite seasonal lead signs after the stated tide filter. A direct next test would use hourly residuals and wind and pressure fields, with common forcing and local response represented explicitly.

The site and seasonal pattern were selected from a prior positive result on overlapping data. The short-period check is not an independent confirmation. Conditional bootstrap limits cannot remove that selection or establish physical causation. Short records, filter assumptions, missing days and changing conditions limit transfer to other sites and times.

## Reproduce and inspect

Use a writable copy of this bundle. Install packages in a private environment. The exact run versions are in files/environment.json; files/requirements.txt lists the needed packages. From the bundle root:

```sh
python files/analyze.py
python files/tide_check.py
python files/audit.py
```

These commands need only bundled CSV inputs and use no network. They rebuild all statistics, draws, filters and figures. The independent audit uses date dictionaries and scipy Pearson correlations rather than the analysis moment routine. It checks point estimates and all saved interval endpoints. files/audit.json records the outcome. This is an arithmetic check, not separate scientific evidence.

To rebuild observed inputs on this campaign host, run:

```sh
python files/prepare.py --out ../rebuilt
cmp files/daily.csv ../rebuilt/daily.csv
cmp files/coverage.csv ../rebuilt/coverage.csv
```

Both byte comparisons passed in this investigation. For another host, `python files/retrieve.py NEW_PRIVATE_DIRECTORY` repeats exact saved observation URLs and checks the hashes. It requires a new directory and leaves changed or partial replies marked incomplete. Pass that directory to `prepare.py --datasets NEW_PRIVATE_DIRECTORY`. Never target the shared data store. NOAA may change live response bytes; the bundled daily rows preserve the analysis if exact retrieval fails.

For a full prediction source rebuild, obtain the verified local campaign bundle identified above and run:

```sh
python files/prepare_predictions.py /path/to/154b66db1e7043562283ea709633f7868d1b3d3c59516bd98b4af2b77c0f4c6b.zip
```

This checks the parent bundle, each raw source hash and each hourly count, then rebuilds predictions.csv. Source URLs and hashes also permit exact retrieval attempts through `sci read` on the parent or from NOAA. The raw prediction responses need not be duplicated here. files/repeat.json records a second offline numerical run and hash comparisons.

## Job and identity

Job: sci-1107-syam2-earth-and-ocean-sciences-7b79e92c7ef2. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-08. One worker; no child agents.

The campaign-machine key signs this local publication. The signature is not a personal authorship claim. Private keys are outside the package. No remote archive upload or index submission is part of this work. NOAA source material remains subject to its source terms; the baseline license covers this report, original code and derived evidence.
