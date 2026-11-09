# The April-March temperature difference reduced later errors for birch and beech leaf date gaps in two Swiss regions, 2011-2025

Job: sci-1107-hp-climate-pollution-biodiversity-dbcb8f0c6aa1. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs the package. It is not a personal authorship claim. This worker used no other agents.

## Question and main result

Does the temperature difference between April and March help estimate the time between birch and beech leaf unfolding, beyond the two-month temperature mean? The test uses paired dates at the same stations. This matters when a seasonal temperature mean is used to represent the timing of several species.

Adding the monthly difference reduced later-year root mean square error (RMSE) by 13.6% in both Swiss regions. The fits used 1996-2010 and were frozen before estimates for 2011-2025. Each model used observed weather from the target year. These are estimates with known weather, not forecasts issued before spring. Removing the time trend from both models reduced the gains to 7.3% in the East and 5.7% in the West. The term added information in this fixed test, but the size of the gain depended on the time model.

The fitted slopes were negative in all four region-period samples. The standard cluster intervals were below zero. A check with three-year blocks was less clear. Seven-day reporting delays can remove all four point-slope signs. These limits are part of the result.

![Gap slopes and later-year errors](files/result.png)

## Data and fixed sample

Source: MeteoSwiss. Data provided by NOAA PSL, Boulder, Colorado, USA, from https://psl.noaa.gov. The providers did not take part in this analysis and do not endorse it.

We reused four shared files. Exact paths, URLs, versions, sizes, download times and SHA-256 hashes are in `files/provenance.json`. No shared file was changed. The phenology file is the legacy checked previous-year snapshot retrieved on 2026-11-09. It contains records through 2025. Phase 606 is European beech (Fagus sylvatica) leaf unfolding at 50%. Phase 642 is silver birch (Betula pendula) leaf unfolding at 50%. The phase metadata confirm these definitions. The record has one date per species, station and year, not an individual-tree time series.

There were no duplicate station-year-phase keys. The date fields agreed with the reference year and day of year. We required each date to be day 1-182 and matched station coordinates. There were 3,042 pairs in 1996-2025 before the common-station screen. Each retained station needed at least five paired years in each period. The main sample has 2,615 pairs at 104 stations. The East has 59 stations and the West has 45. The eight-year screen retained 2,315 pairs at 87 stations. No outcome residual or gap sign was used for selection.

West means longitude below 8.2 E. East means longitude at least 8.2 E. Periods are 1996-2010 and 2011-2025. The regions have separate stations and the periods have separate years. They are not independent climate experiments. The correlation between the annual regional April-minus-March means was 0.980. The same national observation system serves both regions. The later test cohort was selected with record counts from both periods. Thus transfer is conditional on stations that remained usable, not a test of future station retention.

The nearest 0.5-degree GHCN-CAMS grid centre supplies monthly temperature. The file has version attribute 3.01. Its snapshot covers January 1948 to October 2026; only January-April 1996-2025 is used. Temperatures were converted from Kelvin to C. The main eastern and western samples each use 15 grid cells, with three cells shared at the region boundary. Fixed station intercepts absorb constant local offsets, but cannot correct errors in annual mountain weather.

## Variables and methods

The signed outcome is `gap = beech day - birch day`. A smaller signed gap need not mean a smaller absolute separation. Beech was recorded first in 11-27% of pairs across the four samples. Ties made up 4.3-9.5%. The row means of the gap were 7.61 and 9.38 days in the East and 3.88 and 4.81 days in the West. These are descriptive means with some missing years, not trend estimates.

Define `M = (March C + April C) / 2`, `D = April C - March C`, and `W = (January C + February C) / 2`. Each separate primary fit is:

`gap(site, year) = station intercept + bM*M + bD*D + bW*W + bT*(year-2010) + error`.

Each row has weight one divided by that station's record count in its sample. Stations have equal total weight. A one-C increase in D at fixed M means April is 0.5 C warmer and March is 0.5 C cooler. It does not mean a one-C rise in April alone. Using M and D is an invertible change from separate March and April terms. No new physical variable or biological mechanism is introduced by this change of coordinates.

Calendar windows are fixed. They do not depend on the recorded event date. However, 2.7-7.1% of birch dates and 0-0.8% of beech dates were before April 1. Between 65% and 94% of birch dates and 57% and 80% of beech dates were before May 1. Much of April weather therefore followed the event. These fits do not estimate pre-event causal effects.

The primary covariance has station and year clusters, with the standard finite-sample correction. The t reference has 14 degrees of freedom. Four-test Bonferroni intervals use the 0.99375 quantile. This controls the four planned D-slope tests under the covariance assumptions. Other model terms and sensitivity models are secondary, not additional confirmed discoveries.

| Region | Period | Pairs | Stations | Slope, days/C | Four-test family 95% interval |
| --- | --- | --- | --- | --- | --- |
| East | 1996-2010 | 751 | 59 | -0.91 | [-1.76, -0.07] |
| East | 2011-2025 | 794 | 59 | -1.86 | [-3.03, -0.68] |
| West | 1996-2010 | 516 | 45 | -0.86 | [-1.48, -0.23] |
| West | 2011-2025 | 554 | 45 | -1.50 | [-2.39, -0.61] |


The planned sign rule is met with this covariance: all four family upper limits are below zero. This conclusion is sensitive to dependence assumptions. We also resampled whole three-year circular blocks across all stations, and station IDs independently, for 4,999 draws per sample. The original row weights were multiplied by the resampling counts. All draws had full rank. These percentile intervals were:

| Region | Period | Block 95% interval | Block four-test family 95% interval |
| --- | --- | --- | --- |
| East | 1996-2010 | [-1.94, 0.14] | [-2.50, 0.61] |
| East | 2011-2025 | [-2.79, -1.18] | [-3.27, -0.88] |
| West | 1996-2010 | [-1.61, 0.05] | [-1.96, 0.32] |
| West | 2011-2025 | [-2.27, -0.47] | [-2.71, 0.26] |


Only the later eastern family interval was below zero with this method. The early samples have marginal block intervals that also include zero. Fifteen years provide limited information about serial dependence and tail intervals. We do not claim a common negative slope that is clear under both uncertainty methods.

## Transfer to later years

The baseline has station intercepts, M, W and a linear year term. The expanded model adds D. Both models were trained on 1996-2010. All coefficients, including station intercepts, were then frozen. Estimates use the same selected stations in 2011-2025. Errors give each station equal total weight in the test period.

| Region | Fit | Baseline RMSE, days | Added-term RMSE, days | RMSE gain, % | Two-region family 95% interval for gain, % |
| --- | --- | --- | --- | --- | --- |
| East | planned_trend | 9.92 | 8.57 | 13.56 | [4.18, 19.56] |
| East | added_no_trend | 9.37 | 8.69 | 7.30 | [1.91, 11.99] |
| West | planned_trend | 10.29 | 8.89 | 13.55 | [3.27, 21.51] |
| West | added_no_trend | 9.41 | 8.87 | 5.75 | [0.73, 12.01] |


`planned_trend` is the planned test. `added_no_trend` omits the year term from both models. We added this check after the first fits because the planned model extrapolates a linear trend. It supports a smaller transfer gain, rather than the full 13.6% being caused only by trend extrapolation. All four conditional intervals for gain are above zero. The two-region correction applies separately to each specification; it is not a new four-test discovery claim.

For each comparison we used 9,999 crossed station and three-year test-year block resamples. The intervals condition on the frozen training fits. They do not include uncertainty from another training period or a different model-selection process. Regional weather remains strongly shared. The test is forward in time at retained stations, not validation in another national network.

RMSE and mean absolute error are in `files/transfer.csv`. In the planned model, mean absolute error fell from 7.44 to 6.58 days in the East and from 7.61 to 6.65 days in the West. Some target weather was outside the pooled training range: 4.9% of eastern and 3.8% of western test D values were outside it. Every test year was beyond the fitted time range. `files/transfer_ranges.csv` gives all range checks. Pooled ranges do not test each station's full multivariate support.

## Explanation and observation bias

[Prior work in Germany and Slovenia](https://doi.org/10.1007/s00484-007-0113-8) reports differences between the spring months most closely linked to birch and beech leaf unfolding. That work motivates our monthly contrast. It does not validate the current Swiss errors. [Work on leaf-out synchrony](https://doi.org/10.7554/eLife.40214) also describes differences in day-length responses among species. Our signed species gap is different from within-species synchrony. We measured no tree competition or food supply.

A [prior campaign study](sci:sha256:9e4d9a374151cd91d41042e03cfe7a4aed4fadafe10deff3384df2b770de454a) tested seasonal means for the hazel flowering-to-beech unfolding gap. Its Swiss beech and weather sources overlap ours. It did not test birch leaf unfolding, the March-April difference, or the later-year error gain here. A [two-forest campaign study](sci:sha256:0e4379eaf2dffe6ccb275e2b8751ffdbf3f61db50d62def2c833110e28d5d176) used actual visit brackets for different tree species. It helps show why our assumed delay caps are not measured visit bounds. We do not claim a new statistical bound formula or a new physiological mechanism.

On the same records and design, the beech D slopes were -0.41 to -1.15 days/C and the birch D slopes were +0.30 to +0.71. The difference of these slopes equals the gap slope. This is an algebraic check, not independent evidence of a mechanism. At fixed spring mean, the result is consistent with birch responding more to March and beech more to April. Chilling, day length, rain, local weather and reporting changes remain competing explanations.

The common-station screen reduces changes caused by full station entry or exit. Within these stations, complete-pair shares among years with at least one valid date rose from 91.4% to 95.2% in the East and from 83.8% to 92.8% in the West. The diagnostic D slopes of pair availability ranged from -0.00965 to +0.00153 probability units/C. All ordinary 95% intervals included zero. This does not show random missingness. Years with neither date are absent from this diagnostic. No inverse-probability correction was applied.

No trend, equal record weights and the eight-year screen kept all four D point slopes negative. Allowing all stations with at least five pairs per period kept negative slopes, but the early eastern family interval included zero. With year effects instead of a linear trend, the D slopes were -0.48, -0.04, +1.00 and -0.99 days/C in table order. All four family intervals included zero. That fit uses only differences in weather across stations within a year; it does not test the same broad annual forcing as the primary model. It provides no clear local within-year confirmation.

Omitting each year in turn kept the four point slopes negative. Their ranges were [-1.13, -0.72], [-2.17, -1.46], [-1.06, -0.71] and [-1.70, -1.18] days/C in table order. This rules out a point-slope sign determined by one year, but does not resolve block uncertainty. Weekday counts had maximum shares of 15.4-17.4% across species and samples. These counts do not recover actual visits or prove accurate dates. Full model outputs and diagnostics are included.

## Sharp bounds for assumed reporting delays

Let the reported date for each species be its true date plus a delay in [0,L] days. Delays can vary independently across species and records, and may be linked to weather. Then each true gap can differ from its reported gap by any value in [-L,L]. For fixed records, weather and weights, let `a_i` be the linear influence of gap i on bD. The sharp allowed slope limits are:

`bD - L*sum(abs(a_i))` and `bD + L*sum(abs(a_i))`.

To attain the lower limit, move the beech true date earlier by L when a_i is positive and move the birch date earlier by L when a_i is negative. Reverse these assignments for the upper limit. This constructs permissible one-sided event delays at both endpoints. A shared additive delay on both species in one record cancels from the gap. Species-specific delays do not. No order constraint is imposed between these different species.

All four point-slope bounds remain negative for L=1 day. The smallest L that permits zero is 1.86 days in the early East, 4.62 in the later East, 1.80 in the early West and 3.77 in the later West. Three-day bounds permit both signs in the two early samples. Seven-day bounds permit both signs in all four samples.

![Seven-day delay bounds](files/delay_bounds.png)

These are fixed-record possibility bounds, not confidence intervals. They do not combine sampling uncertainty with date error. There are no visit logs in these inputs to justify a particular L. Wrong phase judgements, missing records, tree replacement and errors outside the assumed delay range are not covered. This sensitivity limits a biological sign claim even when the recorded-date slope is negative.

## Limits and scientific use

This is a test of monthly temperature information in two selected Swiss station sets. The error gain does not establish that warming caused the leaf gap to shrink, that the gap changed over time, or that ecosystem synchrony improved. All four primary residual time-trend intervals include zero. Regional mean gaps can change with missing records even in a fixed station set.

One coarse weather field cannot represent Alpine valleys, plant microclimate or daily extremes. One national observation system cannot establish global transfer. We have no observer identities, individual-tree histories, actual visit intervals, air pollution, frost injury, species losses or ecological interaction measurements. The year-block check weakens slope replication, and the hypothetical delay bounds allow sign reversals. The result supports retaining monthly information when estimating these selected records with known weather. It supplies no pollution effect or forecast of biodiversity loss.

## Inspect and reproduce

The exact internal plan is `files/PLAN.md`. It was written before temperature-outcome fits and was not externally registered. The added no-trend transfer check is labeled in that file. `files/sufficient_statistics.json` stores within-station weighted Gram matrices and right-hand sides for all four main samples. These aggregate values allow reconstruction of all main point slopes without external data. `files/validate.py` also enumerates all endpoint choices in a small bound example. With the external panel it independently checks the slopes, two-way cluster standard errors and family intervals, and directly refits the attainable delay endpoints. All 58 checks passed. The panel audit restores the source float32 weather precision from CSV decimals before float64 algebra.

Use Python 3.12 and the versions in `files/requirements.txt` and `files/versions.json`. From an extracted publication:

```sh
python files/validate.py
```

With the retained shared data snapshots:

```sh
python files/analyze.py --data-root /path/to/shared_datasets --out /path/to/scratch/results
python files/validate.py --panel /path/to/scratch/results/external_panel.csv
python files/audit_context.py --panel /path/to/scratch/results/external_panel.csv --out /path/to/scratch/context
```

To retrieve sources on another machine:

```sh
python files/retrieve.py /path/to/scratch/raw
python files/analyze.py --data-root /path/to/scratch/raw --out /path/to/scratch/results
```

All four source hashes are checked before analysis. Live upstream files can change; a hash mismatch stops exact reproduction. Use the retained shared snapshots or an exact external copy in that case. Retrieval and analysis refuse output paths inside the signed publication. Raw data and the record-level panel and prediction table stay in external scratch. The publication includes our code, aggregate results and figures. `files/EXTERNAL_DATA.md` identifies source terms and transformations. The exact baseline LICENSE is unchanged. No private key or third-party article text is bundled.

The full retained-input rebuild and validation record is in `files/reproduction.json`. An exact rebuild must use the full default resampling counts and seed 11072026. Default output includes 136 model-term rows, 12 delay-bound rows, four primary block summaries and four transfer comparisons. Lower draw counts are only for code checks and do not reproduce the published interval endpoints. Optional single-thread BLAS settings can reduce overhead for these small matrix fits; they do not define the method.
