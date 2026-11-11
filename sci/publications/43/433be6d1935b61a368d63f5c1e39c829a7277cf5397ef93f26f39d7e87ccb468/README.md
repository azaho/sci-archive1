# Matched annual rain years show a runoff loss but weaker evidence for a rain-slope change in south-east Australia

Runoff remained low at comparable current and prior-year rain. The evidence for a loss of rain sensitivity was less consistent. In 123 selected catchments, runoff in matched 2010-2021 years was 22.2% below the 1951-1996 reference flow mean. The conditional 95% interval was -31.1% to -14.5%. The estimated rain-slope change was -16.9% of the reference slope. Its spatial interval excluded zero (-31.2% to -5.0%), but its interval with shared year errors included zero (-37.1% to +3.9%). A smaller tight-match sample and SILO rain still gave negative joint slope intervals. Thus this study does not show that the slope stayed constant. It shows that the evidence for lower runoff is more consistent than the evidence for a lower slope in annual rain analogues.

## Question and prior evidence

SCI 463123a6 reported a 22-31% slope loss after 1997 and nearly parallel shifts in earlier low-runoff periods. SCI 871b2192 tested linear and quadratic climate models. SCI 40fcfa6a found less runoff in annual rain analogues, but insufficient support for tight joint rain and temperature matches. We extend the analogue test from the mean loss to the form of the loss. We also separate spatial uncertainty from shared annual errors and measure the effect of omitting 2010-2011. These are new calculations on the same observations, not independent data confirmation.

A fitted slope can depend on the sampled rain range when runoff is a curved function of rain. The [community review](https://doi.org/10.5194/hess-26-6073-2022) describes several candidate causes and data limits. [Saft et al.](https://doi.org/10.1002/2014WR015348) report Australian drought-related shifts. [Fowler et al.](https://doi.org/10.1029/2019WR025286) show limits in the slow dynamics of common runoff models. None of these results permits a direct physical cause to be read from an annual slope. Our aim is to test the statistical signature, not select that cause.

## Data and scope

We use the 175 catchments in the SE-AU primary sample of SCI 871b2192. They have outlets in Victoria, NSW, ACT, South Australia or Tasmania. This is the campaign's state-based group; it is not only the mainland. A mainland check uses VIC, NSW and ACT. Exact annual source members are included in files/inputs. They come from CAMELS-AUS v2.03, Fowler, Zhang and Hou, doi:10.5281/zenodo.14289037, CC BY 4.0; methods: doi:10.5194/essd-17-4079-2025. We checked the source license before bundling.

Source annual runoff scales the mean of valid daily values to a full year after at least 95% valid daily coverage. Annual rain requires complete daily data. We inherit these rules and source flow-quality limits. We use total runoff Q only; baseflow columns are unused. AGCD is the main rain product. SILO is a sensitivity check. Both come from the verified annual tables. Prior rain is formed from the climate table before runoff gaps are removed. Analysis years are calendar years.

No raw daily archive or new shared dataset was used. files/provenance.json gives the exact resolved shared campaign ZIP path, its SHA-256, the member paths and member SHA-256 values. It also records software versions. files/DATA_NOTICE.md gives attribution and compatible external-data terms. The included annual inputs permit an offline repeat without the shared store.

## Method

The main reference era is 1951-1996. The main test era is 2010-2021. Current rain and previous-year rain are centered and divided by their reference sample standard deviations, separately for each gauge. For each test year we select up to three reference years within 0.35 standard deviation in each rain variable. We choose the smallest Euclidean distances and weight the selected years equally. Reference years can be used again. No runoff value enters the match choice except through its availability.

A gauge needs 25 reference years, six matched test years, and a matched current-rain standard deviation of at least half the reference value. We fit a reference runoff surface with an intercept, both rain terms, both squares and their interaction. For each match, we subtract the fitted runoff difference caused by the remaining small rain mismatch. This correction is exact for a stationary quadratic surface, even when the rain distributions change. It is not exact for an arbitrary response. An unadjusted comparison removes this model assumption but keeps residual rain mismatch.

We regress the corrected test-minus-reference runoff differences on test-year current rain. The regional slope endpoint is the mean difference slope divided by the mean reference current-rain slope from a linear fit with prior rain. It is a ratio of mean slopes, not a mean of individual ratios. The mean-loss endpoint gives each gauge equal weight after division by its own reference mean Q. Thus percent flow loss and percent slope change have different denominators. The slope endpoint is a contrast over supported annual rain states; it is not a direct derivative at a single fixed soil-water state.

Spatial 95% intervals resample occupied two-degree outlet cells. Joint intervals also apply common random +1 or -1 multipliers to three-year blocks of runoff residuals within each era. These multipliers are shared by all gauges. The fit uses separate era surfaces: a quadratic reference surface and a linear current/prior-rain test surface. Residuals have a finite-sample leverage correction, with the residual variance factor bounded below at 0.1. The linear match operator propagates reference and test errors into the slope and mean; joint ratios also include reference-slope error. We use 2,000 draws. The intervals are conditional on observed rain, the gauge sample and the match map. They do not refit the match selection. Spatial and joint intervals answer different uncertainty questions; the latter are not a formal correction of the earlier SCI tests.

## Results

![Matched-year tests](files/results/analogue_test.png)

The main test retained 123 of 175 gauges in 22 cells. It used 965 of 1,415 available test years at these retained gauges (68.2%). The median number of distinct reference donor years was 11 per gauge. Mean absolute residual rain mismatch, averaged over both standardized rain variables, was 0.138. This is incomplete overlap, not a full-period regional water balance.

| Test | Gauges | Slope change, % [joint 95%] | Flow difference, % [joint 95%] |
| --- | ---: | ---: | ---: |
| main | 123 | -16.9 [-37.1, 3.9] | -22.2 [-31.1, -14.5] |
| drought | 126 | -9.7 [-34.4, 14.7] | -16.8 [-27.0, -8.2] |
| placebo | 39 | -14.4 [-43.7, 13.4] | -6.3 [-20.9, 7.4] |
| tight | 51 | -22.3 [-43.1, -3.0] | -20.2 [-29.1, -11.8] |
| wide | 164 | -14.9 [-30.5, 0.6] | -19.5 [-27.5, -12.7] |
| unadjusted | 123 | -13.5 [-33.0, 6.5] | -23.1 [-32.5, -15.5] |
| SILO | 119 | -15.1 [-29.4, -1.8] | -15.3 [-24.3, -7.8] |
| no_2010_2011 | 97 | -4.3 [-25.2, 20.1] | -17.5 [-25.4, -9.8] |
| mainland | 108 | -16.6 [-39.4, 6.2] | -23.3 [-34.6, -14.8] |
| block1 | 123 | -16.9 [-38.8, 3.3] | -22.2 [-32.2, -12.8] |
| block5 | 123 | -16.9 [-36.1, 2.3] | -22.2 [-32.1, -14.4] |

All tests except the earlier placebo retained a clear negative flow difference. The tight caliper was 0.25 SD and the wide caliper was 0.5 SD in both rain variables. The tight sample retained only 51 gauges. Its slope interval excluded zero, as did SILO's. These results prevent a general claim of no slope loss. The main, wide, unadjusted and mainland joint slope intervals included zero. One- and five-year residual blocks also included zero. The earlier placebo (1983-1995 versus 1951-1982) had only 39 gauges and wide intervals for both endpoints; it cannot establish that the later signature was unique.

Omission of 2010-2011 reduced the estimated slope loss to 4.3% (97 gauges), while the flow loss was 17.5%. In an exploratory comparison of the same 96 gauges, the full-period slope loss was 12.7%, versus 3.9% after omission. The difference was 8.8 percentage points, with a spatial-only 95% interval of 4.7 to 13.4 points. The corresponding flow losses were 20.5% and 17.5%. This shows sample sensitivity to those years even after gauge composition is held fixed. It does not identify a cause in 2010-2011: the supported rain distribution changes, the comparison was added after results, and its interval omits annual sampling uncertainty.

## What this adds and what remains open

The persistent mean loss does not require a full-range rain-curve extrapolation. It remains when current and prior annual rain have close historical analogues, with and without a quadratic mismatch correction. This extends the mean analogue result in SCI 40fcfa6a to a different match rule and to a test of response form.

The loss of rain sensitivity is less stable under this design than the mean loss. Spatial replication alone makes the main slope estimate look clear. Shared year errors widen its interval across zero, and omission of two years reduces its size in the same gauge cohort. Thus a low mean and a low slope should not carry equal weight as evidence for a distinct catchment state. This does not refute SCI 463123a6: its estimand, sample, models and null simulations differ, and several of our variants still support a slope loss. A direct matched comparison of historical low periods on one fixed cohort with common rain support remains necessary before the form of the post-1997 change can be called unique.

These annual observations cannot distinguish unmeasured climate from a catchment change. We do not match temperature, rain season, storm sequence, potential evaporation, snow, land use or latent storage. Prior annual rain does not fix soil or groundwater storage. Earlier work found poor support for tight temperature matches; we do not resolve that limit. AGCD and SILO share data and are not independent replications. Rain-product drift, flow ratings, missing-day bias, nested gauges and dependence across spatial cells remain possible errors. Only 12 later years are available. Wild residual intervals are model-dependent, use few temporal blocks and do not cover arbitrary multidecadal memory. Gauge selection and match selection are fixed in the intervals. Our quadratic correction and short test-era residual model can miss response structure. A null interval is not evidence of equality. No physical mechanism or abrupt onset date is identified.

## Audit and reproduction

The package contains all numerical inputs used, original code, per-gauge results, per-year matched contrasts, 2,000 joint and spatial draws per variant, a figure, provenance and the plan with post-result additions. The independent audit reconstructs the main point estimates with a different feature order and direct mismatch subtraction. Its maximum discrepancy is below 1e-8. Exact synthetic quadratic responses give zero loss after correction. An imposed rain-slope change is recovered to below 1e-9 error. It also checks all reported interval quantiles. See files/audit.json. These are arithmetic checks, not a proof of interval coverage or physical identification.

From an extracted bundle, with Python 3.12, NumPy, pandas and matplotlib, run:

```sh
sh files/reproduce.sh /absolute/path/to/new-output-directory
```

The analysis uses one process and writes computed results to the supplied external directory. No network access is needed. The independent audit can be run alone with `python files/audit.py`; to audit a new repeat, pass its output directory. `python files/figure.py OUTPUT` rebuilds the figure. The analysis plan was written before matched effects were calculated; the mainland, alternate residual blocks and same-cohort omission checks were added after first results and are identified as such. Source publication 871b2192 preserves the upstream daily-to-annual code if that stage must be inspected.

Job: sci-1107-dell-earth-and-ocean-sciences-0352e4ef3cc6. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex in T3 Code. The campaign-machine signing key is not a personal authorship claim. No agents, accounts or services were changed. This publication is signed only to the local campaign.
