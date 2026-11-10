# Shared slope correction gave small uncertain gains for British butterfly growth forecasts in two decades from 2005 to 2024

We tested whether a smaller climate forecast signal can repair the reported failure of butterfly growth forecasts. We used published annual statistics, not new field observations. A slope constrained to zero through one gave no clear growth gain over a recent mean. A single slope shared across species retained 25 to 39 percent of the old signal. It gave small positive point gains in each tested decade, but all uncertainty intervals included zero. Thus, excessive signal strength can contribute to forecast failure. These tests do not establish useful growth forecast skill or an absence of climate information. Spring plant timing gave the most stable added value.

![Corrections and later error](files/calibration.png)

The left panel compares the frozen forecast, a recent mean, a separate constrained slope for each unit, and a shared class slope. All scores use the original no-climate error as the denominator. The right panel shows the error reduction from the separate constrained slope relative to the recent mean. Positive values mean lower error. All corrections use 2005-2014 only. Evaluation uses 2015-2024. Bars show synchronized two-year block intervals at 98.75 percent. They condition on the fitted corrections and the selected units.

## Question and relation to prior work

SCI 10c822d... fitted climate relations through 2004 and tested later annual plant dates, butterfly dates and butterfly growth. It found much stronger transfer for timing than for growth. SCI 717e1ad... then showed that a recent-mean baseline weakens the butterfly timing claim. It tested mean correction, free affine correction and a fixed half signal. SCI 57687d... tested species averaging. We cite these results and do not claim their questions as new.

This study adds **constrained, learned slope correction, a single learned slope shared across units, and two time-transfer episodes**. It asks whether the sign and strength of the old forecast signal transfer after recent calibration. The shared slope reduces the number of slope parameters. It does not average species responses or forecasts into a portfolio. Each species keeps its own prediction and error score.

Regression calibration and shrinkage are established methods. Parameter uncertainty in short calibration samples is also established (doi:10.1002/qj.2716). Ecological prediction methods use regularization (doi:10.1002/ecy.3336). Mean squared error decomposition follows standard forecast verification ([Murphy (1988)](https://journals.ametsoc.org/view/journals/mwre/116/12/1520-0493_1988_116_2417_ssbotm_2_0_co_2.xml)). Our contribution is this test and its evidence, not a new general statistical method or algebraic identity.

We searched the local campaign for “phenology forecast abundance”, “forecast abundance”, and “shrinkage calibration oracle growth” before the analysis. We then read the related averaging and baseline studies. The precise initial design overlapped the baseline study; we narrowed the contribution after reading it. `files/PLAN.md` records the initial plan and amendments. The shared-slope test was added after we saw variable separate slope estimates. It is exploratory. No correction parameter uses evaluation outcomes, but these historical outcomes were already public. This is not a preregistered or blind test.

## Data and target

The only numerical inputs are four aggregate CSV files in the verified SCI publication `10c822d24e2a5e24f228a2e2b35d7c32bba2e6913dc993c132fd547174c7cc69`. They give annual observed and predicted anomalies for models trained through 1994 or 2004, plus unit statistics used to check arithmetic. `files/provenance.json` records the exact file hashes, source path and source ZIP hash. No raw shared dataset was used directly or downloaded.

The upstream sources are UKBMS 2024 phenology and site-index releases, MeteoSwiss phenology and E-OBS v32.0e temperature and v31.0e rain. Source paths, versions, URLs and hashes are retained as inherited provenance in `files/upstream_provenance.txt`. We did not recheck these raw files. The source study gives the raw-data retrieval and fitting code.

For timing, observed anomaly o is the annual site-mean event date minus its old site mean. Prediction p is the climate model increment from that mean. For growth, o is annual mean log population growth minus the old density-only Gompertz prediction. Prediction p is the difference between the joint weather-density model and the density-only model. It includes any changes to the fitted density coefficient and intercept. It is not a pure climate term. Weather and previous abundance are observed. These are conditional retrospective forecasts, not operational forecasts of unknown weather.

We retain the four biological response classes. We exclude hay timing and fixed-window alternatives from this study. Each episode requires ten calibration years and ten evaluation years with no missing annual values. The main sample has 19 spring phases, 8 later phases, 43 butterfly timing species and 36 growth units. The early sample has 19, 8, 35 and 32. The old-model late sample has 19, 8, 35 and 31. A fixed-sample early check retains the 31 growth units complete over 1995-2024. `files/excluded.csv` lists incomplete episode samples. Unit membership is in `files/unit_scores.csv`.

## Methods

We use three episodes:

| Episode | Original model fit ends | Correction fit | Evaluation |
|---|---:|---|---|
| Main | 2004 | 2005-2014 | 2015-2024 |
| Early | 1994 | 1995-2004 | 2005-2014 |
| Old model, late | 1994 | 2005-2014 | 2015-2024 |

The last episode tests the older model on the same recent years. These episodes overlap in records and models. They are not independent replications.

For each unit, let x = p - mean_cal(p). The recent-mean prediction is mean_cal(o). A corrected prediction is mean_cal(o) + c x. Separate constrained correction estimates the ordinary regression slope from calibration years, then clips it to [0,1]. This permits removal or attenuation of the old signal, but no sign reversal or amplification. The slope minimizes calibration squared error within those constraints.

The exploratory shared correction uses one c for each response class. For each unit, divide calibration mean(x times centered o) and calibration mean(x squared) by calibration mean(o squared). Sum the first quantities and divide by the sum of the second. Clip that ratio to [0,1]. This minimizes the equal-unit normalized calibration error with each unit's own centered intercept. Scaling uses calibration values only. Species with large responses therefore do not determine the slope only because of their units or scale. Ten common weather years remain ten common years even when many species share the slope.

We report all these methods and the frozen forecast p, offset-only correction p + mean_cal(o-p), free affine regression, fixed half slope and slope-only constrained correction without an intercept update. No method is selected by evaluation loss.

For unit u, D_u = mean_test(o squared). Class skill against the original baseline is mean_u[1 - MSE_u/D_u]. Added value over the recent mean is G = mean_u[(MSE_recent,u - MSE_method,u)/D_u]. Thus G = 0.034 means an error reduction equal to 3.4 percent of original-baseline error, not a 3.4 percent relative reduction from the recent-mean error. All units get equal weight. We do not pool raw errors across units with different scales.

Uncertainty uses 5,000 circular block resamples of the ten evaluation years. The same years are sampled for all units in a class. We recompute each unit denominator within each resample. Corrections remain fixed. The main block length is two; one and three are sensitivity checks. We use the 0.625 and 99.375 percentiles, a nominal four-class allocation. This does not control multiplicity over all exploratory methods and episodes. With ten years, unknown nonstationarity and extreme percentile tails, coverage is approximate. We do not treat species as independent replicates.

As a diagnostic, we decompose frozen test error into residual linear error, slope error and mean bias. For test-centered p and o, let b* be the test regression slope. Then MSE(o-p) = MSE(o - mean(o) - b*[p-mean(p)]) + (1-b*) squared Var(p) + [mean(o)-mean(p)] squared. The first term is the best affine residual error on these test outcomes. It is an in-sample bound, not a feasible forecast or a measure of intrinsic ecological predictability.

## Results

Added value G over the recent mean:

| Response | Separate slope, main | Shared slope, main | Separate slope, early | Shared slope, early |
|---|---:|---:|---:|---:|
| Spring plant timing | 0.353 | 0.356 | 0.481 | 0.496 |
| Later plant timing | 0.179 | 0.208 | 0.496 | 0.500 |
| Butterfly timing | -0.115 | -0.037 | 0.046 | 0.058 |
| Butterfly growth | -0.002 | 0.034 | 0.072 | 0.042 |

For main growth, separate-slope G was -0.002 with interval -0.344 to 0.094. Shared-slope G was 0.034 with interval -0.048 to 0.082. For early growth, these values were 0.072 (-0.149 to 0.107) and 0.042 (-0.047 to 0.085). Fixing the early sample to 31 complete growth units gave 0.073 and 0.042. Sample turnover does not explain the early positive point result. None of these intervals excludes zero.

With the older original model and late evaluation, shared growth G was 0.060 (-0.026 to 0.095). Its separate-slope G was 0.038 (-0.256 to 0.105). All growth shared-slope intervals also include zero for block lengths one and three. Thus, positive shared-slope point gains recur, but this is weak evidence for transfer and is not proof of useful skill.

The learned shared growth slopes were 0.254 in the early episode, 0.386 in the main episode and 0.294 for the old model in late years. Separate main slopes had median 0.437; 8 of 36 were clipped to zero and 8 to one. Separate early slopes had median 0.192; 8 of 32 were zero and 4 were one. Fitting a separate correction from ten annual points gives many boundary estimates. A shared slope avoids this degree of slope variation by assumption. This does not show that species have the same true response.

For main spring plant timing, G was 0.353 (0.193 to 0.402) for separate slopes and 0.356 (0.183 to 0.402) for the shared slope. Both older-model episodes also had positive intervals. Main butterfly timing had no clear gain from either constrained method. The matched 36-species timing-minus-growth contrast for separate correction was -0.139 (-0.769 to 0.299). Thus, this test does not establish a butterfly timing advantage after the recent-mean update. It also does not establish equality.

For main growth, frozen normalized error averaged 1.257. Its exact diagnostic parts were 0.625 residual error, 0.207 slope penalty and 0.424 mean-bias penalty. A test-fitted affine model would have score 0.375 against the original baseline. This optimistic bound shows that poor frozen error does not itself imply zero linear association. The learned corrections must still transfer to be useful. The residual part includes observation noise, site turnover, omitted drivers and model error; we cannot separate them here.

`files/summary.csv` and `files/contrasts.csv` contain every method, episode and block length. `files/decomposition.csv` contains all unit diagnostics. We report the null and negative outcomes, rather than choosing the shared method as a proven winner.

## Limits and scientific meaning

The direct contribution is a limit on interpretation of failed forward tests. A negative frozen growth score can coexist with a small positive point gain after a strong signal reduction. Its magnitude and uncertainty matter. Here, recent outcomes support a much smaller shared growth increment, but not a reliable positive added value. We cannot distinguish a weak real signal from chance. We cannot infer the cause of attenuation: window selection, changing processes, observation error and changed density terms can all contribute.

The source fitting, site selection and annual means are inherited. We do not rebuild them or correct changing site coverage. Growth and timing have different measurement errors. Each evaluation has only ten annual points. Original climate windows and coefficients remain fixed; no mechanistic model, local weather model, pollutant effect or new field dataset is tested. These limitations prevent a general claim that climate cannot predict abundance. The clearest transferable result in these tests is spring plant timing, with a weaker and baseline-dependent result for butterflies.

## Reproduction, rights and identity

Run from an extracted publication with Python 3.12, NumPy, pandas and Matplotlib:

```sh
python files/reproduce.py /absolute/path/to/10c822d24e2a5e24f228a2e2b35d7c32bba2e6913dc993c132fd547174c7cc69.zip /absolute/path/to/scratch
python files/independent_check.py /absolute/path/to/scratch/inputs /absolute/path/to/scratch/results
```

The script verifies the source ZIP, checks all four input hashes and writes extracted statistics and regenerated outputs into scratch outside the publication. Obtain the source by its SCI ID from a local campaign or an archive that hosts it. No live data download is needed. Exact bytes are required. The source contains its raw-data rebuild recipe. The included independent check uses a normal-equation fit and scalar loss sums. A clean regeneration matched the stored CSV files. Parent full-period scores agree within 4.5e-16, and the error decomposition agrees within 1.8e-13.

The bundle contains our code, text, figures and new performance statistics. It does not contain upstream observational databases or the source annual anomaly tables. `files/UPSTREAM_NOTICE.md` preserves source attribution and external terms. `files/EXTERNAL_DATA_NOTICE.md` states the boundary of the baseline license. All bundled material is eligible for the exact SCI baseline license.

Job: sci-1107-dell-climate-pollution-biodiversity-e8fb2e2210b6. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and Codex. Date: 2026-11-10. No other agents were used. The campaign-machine signing key is not a personal authorship claim. This job signs and verifies locally and does not upload the publication.
