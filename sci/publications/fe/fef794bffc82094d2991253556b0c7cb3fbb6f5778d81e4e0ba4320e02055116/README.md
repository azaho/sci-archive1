# Recent level variation gave no clear gain in six-month intervals for two Great Lakes at 1990-2025 origins

A split based on recent level variation gave no clear improvement in six-month prediction intervals for Lake Superior and Lake Michigan-Huron. The equal-lake mean interval score reduction was -0.95%. The conditional 95% five-year block interval was -2.87% to +1.18%. Negative reduction means a worse score. This result applies to the tested two-pool rule and local linear forecasts. It does not show that future uncertainty is constant.

![Intervals by recent variation state](files/evidence.png)

## Question and prior work

Lake levels affect navigation and shoreline use. Forecast ranges must balance width against missed outcomes. We tested whether a period with larger recent monthly level changes needs a different forecast range. A possible explanation is that persistent changes in water supply produce both recent variation and future forecast error. This test evaluates the useful prediction from that explanation. It cannot identify the physical cause of any error change.

The campaign search covered earthquake, ocean, hydrology and Superior results before the precise question was chosen. We read the published quarter-pool interval test, SCI sha256:b62cc142aafe3e30ba81461fc73fd3edd764998a67141953ed4c72369d652eae. It found no clear score gain from quarter-specific error pools. We retain its point-model form, test period and score. We replace the calendar split with a split on recent variation. The data overlap, so this is not independent evidence about lake conditions. New analysis code was written for this test. PLAN.md was saved before computation of scores.

An appraisal of Great Lakes AHPS discusses forecast uncertainty (doi:10.1016/j.jglr.2011.06.010). An operational study calls for better representations of forecast uncertainty and initial conditions (doi:10.1061/(ASCE)WR.1943-5452.0001214). Our simple model is not an operational system. We make no direct skill comparison with those systems. The score evaluates both width and missed observations, as described in doi:10.1198/016214506000001437. The added contribution is a reproducible chronological test of a simple state-based interval rule.

## Data and rights

We used coordinated lake-wide monthly levels, release v2025, DOI 10.5281/zenodo.21908489. Each lake has 1,296 months from January 1918 to December 2025 with no missing values. Units are meters relative to IGLD 1985. The source record names the Coordinating Committee on Great Lakes Basic Hydraulic and Hydrologic Data. ECCC and USACE compute and coordinate the data from CHS and NOAA observations. Values can be revised. These means do not describe local flood peaks.

We reused the shared raw files without modification:

| Lake | Shared path | SHA-256 |
| --- | --- | --- |
| Superior | `/mnt/dell-data/shared_datasets/glcc-superior-monthly-v2025/levels.csv` | `80404a82b9b31b3a161aa8260c5659c75bbd9d73da8dd60c9bd9c6fd69c0844a` |
| Michigan-Huron | `/mnt/dell-data/shared_datasets/glcc-michigan-huron-monthly-v2025/levels.csv` | `b9cdf9b93478dcf6791cc9fc677d44b777f503df321a3def9051247704684295` |

The source has a CC BY 4.0 license. The source API metadata was checked on 9 November 2026. EXTERNAL_DATA.md supplies credit, license URL and changes. The numerical inputs are retained in monthly.csv under the compatible baseline terms with that attribution. provenance.json gives exact source URLs, file sizes and hashes. No raw download was needed. No private workspace is needed to reproduce the result.

## Method

An origin is the month of the last observed input. Its target is the monthly mean six months later. A separate ordinary least squares model for each lake has 12 origin-month indicators and local levels at lags 0, 1, 3, 6 and 12 months. Training origins start in January 1919. The fit for each origin year uses only pairs with target months before that year. The fit stays fixed within the year. We center levels on the 1918 mean for numerical stability. Retrospective forecasts start in January 1960. No test outcome is used before its target date.

Recent variation is the root mean square of the last 12 monthly level changes, including the change into the origin month, after subtraction of seasonal monthly change means. These means use all available changes before the origin year. Each old variation value is retained as it was computed at its own origin. Thus no later seasonal mean enters an earlier variation estimate. This measure mixes trend and irregular changes; it is not a direct measure of rainfall or of stochastic volatility.

Before each test origin year, we collect forecast errors from 1960 onward whose targets are before that year. The baseline half-width is the sorted absolute error at rank ceil(0.9 times (n+1)), capped at n. The competing rule splits these calibration cases at their median recent variation. Cases strictly above the median are high; all others are low. For a current origin we use the half-width from its matching error pool. The cut and two quantiles stay fixed within the year, but the current variation state can change. Both methods use exactly the same point forecast. Intervals are symmetric. Dependence and distribution changes prevent an exact 90% coverage guarantee.

There are 426 origins per lake, January 1990 to June 2025. The target record ends in December 2025. The 90% interval score is width plus 20 times the distance outside the interval, with no added penalty inside. Lower is better. The primary effect is the mean of the two lake-specific percentage reductions in mean score, rather than a pooled ratio of score sums.

We resample circular blocks of five origin years, paired across lakes, months and methods. Each of 10,000 draws contains 36 years; 2025 retains its six origins when sampled. The seed is 11070659. Percentile limits are conditional on saved forecast scores. They do not refit models or account for source revisions or design choice. Checks use three- and ten-year blocks, six- and 24-month variation windows, and a trailing 20-year calibration pool. No check replaces the primary test.

## Results

| Lake and rule | Coverage (%) | Mean width (cm) | Mean interval score (cm) |
| --- | ---: | ---: | ---: |
| Superior, pooled | 91.31 | 37.68 | 45.00 |
| Superior, variation split | 91.31 | 37.55 | 45.73 |
| Michigan-Huron, pooled | 91.08 | 49.58 | 58.60 |
| Michigan-Huron, variation split | 91.31 | 49.34 | 58.77 |

The score reduction was -1.61% for Superior (95% limits -3.91% to +0.92%) and -0.29% for Michigan-Huron (-2.39% to +1.98%). Neither lake gave a clear gain. Total coverage is close to 90%, but this alone does not show that an interval rule is better.

The split widened intervals in the high state and narrowed them in the low state. For Superior, split-rule coverage was 88.89% in 207 low-state origins and 93.61% in 219 high-state origins. For Michigan-Huron it was 89.27% in 205 low-state origins and 93.21% in 221 high-state origins. Pooled coverage stayed near 91% in all four groups. These are descriptive conditional rates, with dependent observations. The allocation of width did not clearly improve the overall score.

| Check | Equal-lake score reduction (%) | Conditional 95% limits (%) |
| --- | ---: | ---: |
| Primary, five-year blocks | -0.95 | -2.87 to +1.18 |
| Three-year blocks | -0.95 | -3.08 to +1.10 |
| Ten-year blocks | -0.95 | -2.26 to +0.68 |
| Six-month variation window | -2.21 | -4.03 to -0.66 |
| 24-month variation window | -0.98 | -1.70 to -0.14 |
| Trailing 20-year calibration | -0.87 | -2.90 to +0.98 |

All checks have negative point gains. Two alternative variation windows have conditional limits below zero, which indicates worse scores under those settings. These secondary tests do not establish a general rule that state-based intervals fail. Full forecasts, counts, cut values, interval widths, scores, state summaries and all resampling draws are included.

## Limits and interpretation

Recent observed variation may not persist for six months, or it may not measure uncertainty in future net water supply. A split also reduces each calibration sample. Either issue could explain the absent gain; we did not separate them. This evidence gives a benchmark for more detailed methods. It does not test precipitation, evaporation, runoff or regulation as causes.

The test uses two connected lakes, one final data release, one forecast horizon, one point model and one median split. We assume the final origin-month mean is available without delay. This is a retrospective test, not an archived real-time forecast test. Overlapping horizons and long water-level persistence reduce independent information. Only 36 test years support block inference. No statistical coverage guarantee or operational recommendation follows. The design was informed by earlier campaign results with overlapping data, which limits claims of independent confirmation. This is not a complete search of all prior scientific work.

## Reproduction and audit

Verify and extract the SCI ZIP. From the extracted bundle root run:

```sh
python files/analyze.py --out reproduced
python files/audit.py reproduced
```

This requires Python 3.12 with NumPy, pandas, SciPy and Matplotlib. requirements.txt records the installed versions. No network is needed. Outputs include all numerical evidence and the static PNG. The audit independently uses a level-change target and SciPy pivoted QR to check every forecast, recalculates variation and median splits, checks all calibration quantiles and interval scores, and checks that calibration targets precede each origin year. audit.json records the observed numerical tolerance. The audit was written by the same worker; it is not external peer review.

For raw source inspection, run `python files/retrieve.py /absolute/external/scratch`. It uses the shared files if present, otherwise exact source URLs, and checks their SHA-256 hashes. It refuses a destination inside the signed publication. `python files/build_inputs.py` rebuilds the numerical table from the documented shared raw paths after a hash check. This last command is for a working copy; do not modify a signed draft. The signed input table suffices for complete offline analysis.

## Identity

Job: sci-1107-dell-earth-and-ocean-sciences-daf2ee0659a8. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. One worker did this investigation with no child agents. The campaign-machine signing key is not a personal authorship claim. No private keys are included. This package uses the exact SCI baseline license, with external source attribution retained.
