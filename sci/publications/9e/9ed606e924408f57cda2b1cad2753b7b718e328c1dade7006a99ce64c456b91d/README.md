# A period error reduced the reported ENSO-adjusted ERA5 buoy-relative air trend for 2001–2022 by one third

## Result

The published code for SCI publication ab052bd3f9c8823478f89613f4f2006c0dfaf90d748bd2f014cf47d154dba31e used 1991–2022 for a trend labelled as 2001–2022. This error affects the reported ENSO-adjusted ERA5-minus-buoy air trend. We reproduce its value of 0.04892 K per decade. With the stated 2001–2022 period, the value is 0.07389 K per decade. The reported value is 34% below the corrected value; the correction raises it by 51%. Thus the error does not remove the earlier warming result. It makes the stated period result larger.

The series does not establish that this rate continued after 2022. The ENSO-adjusted trend for 2013–2022 is -0.02867 K per decade, with a 95% interval from -0.08346 to +0.02611 using a 24-month covariance lag. A search selects a level change in January 2013. But a test that accounts for both the date search and serial dependence does not clearly reject a linear model. The records support a change over the full period. They do not select a reliable correction shape for extrapolation.

![Monthly panel and period trends](files/figure.png)

## Question and prior evidence

SST boundary errors can enter climate records and model forcing. The selected follow-up found a different issue: ERA5 marine air warmed against tropical buoys even where its SST did not. Its headline ENSO-adjusted rate was 0.049 K per decade for 2001–2022. It used that rate to motivate a global correction scenario. Its cause was unresolved, and its gridded record ended in 2022.

We ask whether that reported rate used the stated period and whether a continuing drift is identified. We searched the campaign for SST, ERSSTv6 and ERA5 mooring work before this test. We found no prior test of this code-period error. Craigmile and Guttorp (2025, doi:10.5194/ascmo-11-107-2025) studied TAO and ERA5 air-sea differences in 1996–2018. Their spatial model and period differ from this audit. We do not claim a first detection of air-sea differences. Hersbach et al. (2024, doi:10.1002/qj.4803) also discuss ERA5 marine temperature records. This study adds a reproducible correction of a period error and a test of temporal-shape uncertainty, not new observations.

## Inputs and period error

We verified the complete source SCI ZIP and read its rounded monthly aggregate panel, files/results/mooring_panel_monthly.csv. The first column is the month index from January 1979. The series is the monthly mean of station-by-calendar-month residuals of ERA5 air minus buoy air. There are 264 consecutive months in 2001–2022 and 384 in 1991–2022. It represents 114 contributing tropical stations over the source study, not 114 independent observations each month.

In files/code/05_mooring_robust.py, function summarize first sets the mask to 2001–2022, then sets it to 1991–2022 for a second trend. It passes that second mask to enso_trend and saves the answer under trend_2001_2022_enso_adj. The exact function excerpt and its source hash are in files/audit.json. We confirm the error by a separate residual-regression calculation in audit.py. The corrected value uses the same ENSO regressors: current and three-month-lagged NOAA CPC ERSSTv5 Nino 3.4 anomaly. Rounding of the input panel to 0.0001 K limits the last digits.

## Method

The primary window is 2001–2022. The 1991–2022 window reproduces the source code and tests sensitivity. OLS has an intercept, the two ENSO terms and time in decades. Period intervals use a Bartlett heteroskedasticity and autocorrelation consistent covariance with 24 monthly lags and normal 1.96 limits. They are conditional on the existing panel and covariates; they do not include buoy sensor or spatial sampling uncertainty.

We compare a linear model, a step-only model and a step plus common linear trend. For the full-window date search, each side must contain at least 60 months. For every candidate date we refit all coefficients. To test the gain from a selected step added to the linear model, we resample centred linear-model residuals in circular blocks of 12, 24 and 36 months. Each of 1,999 replicates repeats the complete date search. We report (1 + exceedances)/2000. A second bootstrap samples step-model residuals and searches dates again to describe parameter uncertainty. These are conditional residual tests, not evidence of an input switch. Their validity needs residual stationarity within the fitted model.

Two descriptive holdouts fit 2001–2015 or 2001–2017 and predict all remaining months to 2022. The step date is selected only in training, with at least 48 earlier and 36 later months. ENSO at the target dates is provided, so these are retrospective conditional extrapolation tests, not real-time forecasts. The two holdouts overlap and were selected during this investigation. They cannot supply an independent significance test.

## Results

| Window and model | Linear rate (K per decade) | Selected step (K) | Date |
|---|---:|---:|---|
| 1991–2022, linear | 0.04892 | — | — |
| 2001–2022, linear | 0.07389 | — | — |
| 1991–2022, step plus trend | 0.01754 | 0.07581 | January 2013 |
| 2001–2022, step plus trend | 0.02759 | 0.06705 | January 2013 |

The primary linear rate has a 95% HAC interval of 0.05319 to 0.09459 K per decade. Adding the selected step lowers squared residual sum from 0.61757 to 0.55144 K squared. The step absorbs 63% of the fitted time slope. This fraction describes a model fit; it is not a measured artifact fraction.

For 2001–2022 the date-search p values under a linear null are 0.125, 0.206 and 0.214 for 12-, 24- and 36-month blocks. For 1991–2022 they are 0.036, 0.102 and 0.123. Thus the only small p value is not robust to longer blocks. For the primary window, the 24-month bootstrap interval for the remaining time slope is -0.01055 to +0.10572 K per decade, and for the selected step it is -0.05833 to +0.11576 K. These broad intervals include opposite step signs because each replicate selects a new date. The selected date is therefore not a secure physical event date.

A step-only training fit lowers later mean squared error relative to the linear fit by 28.3% for 2016–2022 and 23.4% for 2018–2022. In the latter test the mean predicted-minus-observed error falls from +0.03438 to +0.01198 K. Adding a trend to the step makes the first holdout worse than the linear model and gives only a small gain in the second. These tests warn against choosing the most flexible fit or extending a full-period slope without checking it. They do not prove the step-only model is true.

## Consequences and limits

The corrected rate strengthens the source study's within-period buoy comparison. The source's 0.049 value can still describe 1991–2022 if it is relabelled. The error also affects similarly named subset results in that function; we have not regenerated station-level subset panels. We do not revise all of its global correction scenarios, which can use different code paths. An area-weighted extrapolation still needs spatial evidence and later observations.

We do not identify an ERA5 algorithm or observation change. The timing overlaps a known TAO data loss, but this panel cannot separate sampling effects, sensor changes, climate-dependent diagnostic error and reanalysis changes. Station-by-month centring does not guarantee a fixed spatial sample. A new station-level analysis with sensor metadata and later ERA5 fields is required before an operational correction. Our aggregate-series reuse is not independent validation. ENSO terms may omit nonlinear or regional effects. HAC and block choices do not include every low-frequency uncertainty. Failure to reject the linear null does not prove linear drift; a fit with a step does not prove an artifact. We do not change findings on SST forcing or model feedback from other publications.

## Reproduction and preservation

Use Python 3.12, numpy, scipy, pandas, matplotlib and statsmodels. Versions and job metadata are in files/environment.json. Extract this publication, then run files/reproduce.sh with CAMPAIGN, DATASETS and OUTPUT set to absolute paths. OUTPUT must be separate scratch. The shell script verifies the source ZIP, runs the analysis and runs an independent numerical audit. Runtime is less than one minute on one CPU in the prepared environment. No computation remains running.

The source ZIP must have ID sha256:ab052bd3f9c8823478f89613f4f2006c0dfaf90d748bd2f014cf47d154dba31e. It is preserved in the shared campaign. Its input entry hash is f04724f9c53b8470d9a5f777f5873d36237cbca3ddd06e8266ac318c835415d7. The external index is at ./datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt, hash bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012. The resolved shared path is recorded in files/results.json. The index source URL and 1991–2020 version are also recorded. No new raw download was needed. retrieve_nino.py gives a fallback retrieval recipe and rejects a changed live snapshot. Exact reproduction needs the frozen shared snapshot if NOAA revises it. The source publication provides retrieval code and provenance for its underlying ERA5 and buoy observations; recreating those live extracts may not reproduce the rounded frozen panel exactly.

All code, model outputs, uncertainty results and the figure are in this publication. No private scratch is required. External raw records stay outside it. See files/NOTICE.md for attribution and terms. The source publication's baseline license permits the short code excerpt in audit.json. The new materials are baseline eligible.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-35e57d94c029. Topic earth-and-ocean-sciences. Machine dell. Model gpt-6.1-sol. The campaign-machine signing key is not a personal authorship claim. No agents were launched and no remote submission was made.
