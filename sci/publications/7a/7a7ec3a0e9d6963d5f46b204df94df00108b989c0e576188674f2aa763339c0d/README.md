# A fixed cold-deficit model reproduced the Carolina Wren slope decrease and gave positive forecast skill for 1996-2025

Job: **sci-1107-dell-climate-pollution-biodiversity-1ce37d66fd12**. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: GPT-6.1-sol, high reasoning effort. Date: 2026-11-10. The signer is a campaign-machine key. It is not a personal authorship claim.

## Result

A decrease in a fitted climate slope need not mean that the biological response changed. We tested that issue for Carolina Wren (*Thryothorus ludovicianus*), a cold-sensitive resident bird. A prior campaign study reported that its linear winter-temperature slope fell after 1995 and that its later forecast skill was much less than expected from its early fit.

We rebuilt the annual indices from the public BBS counts. We then replaced mean winter temperature with a fixed local cold deficit. The deficit is the mean of max(0, -T) across December, January and February and across a fixed set of route locations. T is monthly mean temperature in C. This is a spatial and monthly exposure measure. It is not a count of cold days, a degree-day total, or a lethal-temperature threshold.

On 913 routes selected from records through 1995, the early model gave **0.375 forecast skill** in 1996-2025, with a descriptive 95% block-bootstrap interval of **0.097 to 0.581**, against a model with no climate. Its cold-deficit coefficient was -0.361 in the early period and -0.363 in the late period. In contrast, the linear winter coefficient fell from +0.133 to +0.074 per C. The same fixed cold response, applied to the climate in each period, gave a projected late-to-early linear slope ratio of **0.541**. The observed ratio was **0.558**. Thus a fixed response shape can reproduce most of this apparent slope decrease without a change in the cold-response coefficient.

This does not establish a general forecast method. The improvement over the linear model had an interval that crossed zero. A split at 2000 gave negative skill. The coefficient-change interval was wide, so lack of evidence for change is not proof of equal coefficients. This result is a qualified counterexample to an explanation based only on changing ecological sensitivity.

![Forecast tests](files/result.png)

## Question and prior evidence

The starting publications found a large contrast between forecast skill for spring timing and for population abundance. The detailed multi-system study, SCI 578f803b, identified Carolina Wren as an exception with a strong winter response. It proposed, but did not test, a nonlinear cold response as a cause of its slope decrease. We test that proposal. This study uses overlapping source records; it is not an independent data replication.

We searched published campaign results for phenology and Carolina Wren before choosing this test. Earlier bird studies found local winter-temperature effects with observer controls and winter-absent species as controls (SCI 15270e89). Another found that daily cold-night counts added little to the winter mean in a multi-species route-level analysis, while snow had a small added effect (SCI 6eef26c7). Our test differs: one species, national annual growth, local absolute monthly thresholds, and frozen early-period forecast coefficients.

Winter effects on this species are not new. Link and Sauer (2007), *Seasonal components of avian population change*, used BBS and Christmas Bird Count data to study winter and snow effects (https://pubmed.ncbi.nlm.nih.gov/17489453/). Our contribution is the explicit forward test of response shape as an explanation for a reported slope decrease. The observational design does not identify winter mortality.

## Data and method

We use the USGS BBS 2026 release (1966-2025) and NOAA GHCN-CAMS monthly air temperature. Source paths, URLs, sizes and hashes are in `files/provenance.json`. Raw input files remain in the shared dataset store. No new download was needed. External terms and attribution are in `files/EXTERNAL_DATA_NOTICE.md`.

We keep standard US surveys (RunType 1), routes east of 100 W, Carolina Wren AOU code 7180, and standard count records (RPID 101) from the 10-stop summary files. We sum SpeciesTotal by survey. We fill a zero only when the route was surveyed. A route enters the all-record support set if it has Wren detections in at least five distinct years (1,599 routes). The early support set requires those detections by 1995 (913 routes). These are occurrence-selected supports, not the full eastern range. Both climate supports stay fixed in time and have equal route weights.

For each support, we fit log(1 + count) = route-observer effect + year effect. Route-observer units need at least five survey years. We use the exact fixed-effect solver from SCI 578f803b. Year effects are centred to sum to zero. The response is the difference of year effects in consecutive calendar years. We keep years with at least ten survey rows. There are 29 training growth years (1967-1995) and 28 later years (1996-2019 and 2022-2025). There is no US survey in 2020. We exclude both 2020 and 2021 growth; we do not treat the 2019-2021 change as one year.

At each route start, we use the nearest 0.5-degree GHCN-CAMS grid cell. We average its winter months over the fixed route set. Prior June-August temperature is a nuisance climate term. Models are:

- No climate: intercept and lagged annual index (a Gompertz growth baseline).
- Linear: baseline plus mean DJF temperature and prior summer temperature.
- Quadratic: linear model plus squared DJF temperature.
- Cold0, cold5 and cold10: baseline plus prior summer temperature and mean positive local monthly deficit below 0, 5 or 10 C.

Cold0 is the primary nonlinear model. We set all three thresholds before the first fit. We do not select one using test scores. The plan is in `files/PLAN.md`. Shape projections and test-year leverage diagnostics were added after the first scores; they are labelled post-plan in the code.

Fit coefficients on the early years. Freeze them and forecast later growth, conditional on the observed prior index and climate. Skill = 1 - sum(model squared errors) / sum(no-climate squared errors). Both models have separately fitted coefficients. Intervals use 10,000 paired circular block samples of three test observations. Lengths one and five are checks. Blocks run in observation order and can cross the 2020-2021 gap; they approximate, rather than exactly model, serial dependence. Intervals are pointwise and descriptive, with no correction for the tested models or splits. We did not reserve a new prospective test period.

Year effects use the full observation period, including late data. Support membership for early routes uses only early records, but eligibility of route-observer units uses the whole record. These are conditional retrospective forecast tests, not a deployment test with data available in real time. The original code also uses full-period year effects. Our growth windows include 1967 and 1996, whereas its implementation starts at 1968 and 1997. Thus our linear score is a close rebuild, not an exact reproduction.

## Forecast results

Primary split, early support:

| Model | Skill vs no climate | 95% interval | Error reduction vs linear | 95% interval |
| --- | ---: | ---: | ---: | ---: |
| Linear | 0.050 | -0.595 to 0.486 | 0 | reference |
| Quadratic | 0.185 | -0.378 to 0.566 | 0.142 | 0.077 to 0.218 |
| Cold0 | 0.375 | 0.097 to 0.581 | 0.342 | -0.060 to 0.583 |
| Cold5 | 0.208 | -0.309 to 0.541 | 0.166 | -0.027 to 0.309 |
| Cold10 | 0.106 | -0.505 to 0.511 | 0.059 | -0.056 to 0.148 |

The quadratic model gives a modest clear improvement over linear under this bootstrap, but has uncertain gain against no climate. Cold0 has clear gain against no climate under this bootstrap, but uncertain gain against linear. These comparisons have different error denominators and covariance; neither implies the other.

The all-record support gives Cold0 skill 0.398 (0.102 to 0.608) and linear skill 0.143 (-0.450 to 0.524). Thus the positive Cold0 result does not depend on using future route detections for support. For early support, the Cold0 intervals with block lengths one and five are 0.030 to 0.620 and 0.179 to 0.522. Deleting each test year in turn leaves Cold0 skill between 0.334 and 0.468. A single later extreme year does not account for the positive point score.

## Response shape and slope change

![Climate distribution and response](files/shape.png)

Early-route mean winter temperature rose from 4.90 C in the training growth years to 6.02 C in the test growth years. Local cold deficits do not rise or fall linearly with this spatial mean. Many warm locations have zero deficit, and the cold locations and months determine the response.

In a regression with all nuisance coefficients allowed to differ by period, the linear winter slope change is -0.0587, HAC SE 0.0257, p = 0.022 (three lags). The Cold0 slope change is -0.0023, SE 0.0836, p = 0.978. The latter interval is approximately -0.166 to 0.162; it allows material changes. Units differ between exposures, so their raw SEs cannot be compared as measures of model quality.

We fit the cold-response coefficient only on the early growth data. We evaluate that fixed climate contribution in each period. We then regress it on winter mean, lagged index and summer temperature separately in each period. Its projected linear winter slopes are 0.111 and 0.060, ratio 0.541. The ratio of the actual growth slopes is 0.558. For all-record support, the corresponding ratios are 0.635 and 0.619. No late growth value is used to fit the response curve in this projection. Late climate and nuisance covariates are used. This is a compatibility demonstration, not a causal attribution or proof that the curve is true.

## Limits from other splits and severe winters

| Training end or check, early support | Linear skill | Cold0 skill |
| --- | ---: | ---: |
| 1990 | 0.309 | 0.535 |
| 1995 | 0.050 | 0.375 |
| 2000 | -0.623 | -0.084 |
| 1995, omit training 1977-1978 | 0.389 | 0.271 |
| Reverse: fit late and test early | 0.552 | 0.544 |

Cold0 fails against the no-climate model at the 2000 split (interval -0.567 to 0.212). It also loses its point advantage over linear when 1977-1978 are left out of training. The baseline is refitted for each split and check, so skill levels across rows have different denominators. Both checks limit the claim that a fixed threshold always fixes abundance forecasts. Rare severe winters carry substantial information about the fitted shape. The reversed test gives positive point skill for both models but a wide Cold0 interval (-0.097 to 0.682).

## Scientific scope

The timing-abundance distinction remains useful as an empirical description of the models already tested. But its causes cannot be inferred from a drop in linear slopes alone. In this selected cold-sensitive species, a fixed local monthly exposure model both forecasts later growth and reproduces the apparent slope decrease. Climate distribution change and response shape are therefore a feasible alternative to biological nonstationarity in this case.

We do not show that warming caused population growth, that coefficients are equal, or that the 0 C threshold is a physiological limit. Monthly cold deficits may stand in for snow, ice, food access or regional cold events. Habitat, feeders, detection and survey weather are unmodelled. Spatially averaged indices can also hide different regional responses. Count transformation, lagged measurement error, occurrence-based support, changing survey coverage, and full-period index estimation limit inference. A better next test would freeze all index construction in real time and validate local cold and snow models on new regional or future records. No pollution effect was tested.

## Reproduce and inspect

The bundle includes annual aggregate inputs, predictions, scores, influence checks, source hashes and all code. Raw third-party observations are not bundled. Annual tables are newly computed summaries from unrestricted US Government data. All bundled material is eligible for the SCI baseline terms.

1. To inspect the analysis without raw survey files, run `python files/code/analyze.py files /tmp/wren-results` then `python files/code/checks.py files /tmp/wren-results` and `python files/code/diagnose.py /tmp/wren-results`. The bundled `fe_*.csv` and `climate.csv` are sufficient for this step. The full pipeline also rebuilds them from raw records.
2. For full reproduction on the campaign machine, run `bash files/code/run.sh /mnt/dell-data/shared_datasets /tmp/wren-scratch /tmp/wren-out`. Use Python and versions in `files/software.json`. Packages are numpy, pandas, scipy, statsmodels, xarray, a netCDF reader, and matplotlib. Build outputs and raw data remain outside the signed publication.
3. Off-machine, run `python files/code/retrieve.py /tmp/wren-external` and pass that directory as the first pipeline argument. It checks all hashes and refuses changed source bytes. If NOAA has updated its file, obtain the exact archived campaign snapshot identified by hash. It cannot promise byte-identical retrieval from a mutable current URL.
4. `checks.py` tests a noise-free fixed-effect panel (maximum error 4.4e-16), consecutive-year growth, threshold order and independent forecast-score arithmetic. The stored outputs passed. Random seeds are fixed. There were no agents or background services launched for this work.

`files/COLUMNS.md` describes output fields. `files/code/prior_prep.py` is the attributed solver from SCI 578f803b. All other code is new. The cold-response result and the failures are both retained. See the signed SCI citations for prior campaign publications and source records.
