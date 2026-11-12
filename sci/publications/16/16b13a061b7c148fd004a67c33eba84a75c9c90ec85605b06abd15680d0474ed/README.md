# Added wind direction gave a small and uncertain three-day temperature forecast gain at two California buoys in 2010-2023

We tested whether local wind direction adds useful information to a short sea-temperature forecast after recent temperature, wind strength and season are known. We used NOAA National Data Buoy Center (NDBC) stations 46013 at Bodega Bay and 46042 at Monterey. The target was the mean temperature of the next three UTC days. Each annual fit used only earlier years.

Adding six wind-vector terms reduced the equal-site mean squared error (MSE) by **1.28%** in 4,183 retained station-days in April-September 2010-2023. The conditional 95% interval was **0.05% to 2.56%** with three-year blocks. It was **-0.22% to 3.01%** with one-year blocks. With 15 daily temperature lags, the three-year interval was **-0.13% to 2.68%**. Thus the three-day gain was small, and evidence that it exceeds zero depended on the test setting. Warm starts gave no clear gain. These results do not establish a useful forecast improvement for warm events or a physical cause.

![Annual gains and the uncertainty across test settings.](files/forecast_gain.png)

## Question and prior work

Coastal temperature forecasts can support work on marine habitats and extreme heat. Wind strength can affect mixing. Wind direction can affect coastal upwelling and water transport. The question is whether direction still helps a forecast after local temperature memory and wind strength have been included.

The wind-temperature connection is established. Woodson et al. (2009, [doi:10.1029/2009JC005623](https://doi.org/10.1029/2009JC005623)) measured wind-related movement of a temperature front in northern Monterey Bay. Their nearshore field study does not give a forecast benchmark for the offshore buoy used here. Jacox et al. (2019, [doi:10.1007/s00382-017-3608-y](https://doi.org/10.1007/s00382-017-3608-y)) assessed seasonal temperature forecasts in the California Current. Their published abstract links skill to winds and upwelling and stresses the strength of a persistence forecast. Our horizon, sites and statistical comparison differ.

We searched the SCI campaign with several queries before choosing this question. A prior [upwelling study](sci:sha256:34211b15a751b9c35ab427962958189533ca2d9edf1b52bd8240f4facf835990) tested long-term winds at these and other buoys. It did not test added short-range wind-direction skill after temperature memory. A prior [wave forecast study](sci:sha256:233aba9b82d55430941d758f5f8e630f76d23024cc8dcdb7cef3e52bf9c4ad9d) used this station pair and saved reusable annual source files. We use those files in place. We also follow its use of annual time splits, data-delay checks and paired year blocks. We wrote new analysis code. The source archive overlaps those studies and is not independent data.

Our contribution is a reproducible benchmark for the added value of wind-vector features in a fixed temperature model. We do not claim a new physical mechanism or a new general forecast method.

## Data and source rights

We used 48 annual NDBC standard meteorological files, one file per station and year in 2000-2023. Their total size was 12,123,829 bytes. The files were already in the shared dataset store. We made no new raw-data downloads. The earlier wave study reported that the 2024 Monterey file was absent. We fixed our end year at 2023 before record parsing and scoring. We did not substitute a station.

The exact shared paths have this form:

```
./datasets/ndbc-stdmet-46013-2000-20261109-be177/46013h2000.txt.gz
./datasets/ndbc-stdmet-46042-2023-20261109-be177/46042h2023.txt.gz
```

The first and last paths are examples. `files/provenance.json` lists all 48 exact absolute shared paths, resolved paths, source URLs, source retrieval times, byte counts and SHA-256 hashes. These names can contain `/mnt/dell-data`; they are compatibility paths to the shared HP store. This work did not read the failed `/data` disk. NDBC gives no immutable version tag for these files. The recorded hashes define the input snapshot. A later download must match them to reproduce this snapshot.

The [NDBC measurement guide](https://www.ndbc.noaa.gov/faq/measdes.shtml) defines water temperature in degrees C and wind direction as the direction from which the wind comes, measured clockwise from true north. Times are UTC. The [NDBC data guide](https://www.ndbc.noaa.gov/faq/dataindex.shtml) describes the quality-controlled historical archive. This test uses revised archive observations, not the exact data available in real time.

NOAA/NWS source information is public domain unless marked otherwise, subject to the source attribution and use notices at [NWS source terms](https://www.weather.gov/disclaimer). We keep the raw files and all daily or forecast record-level tables outside this publication. The bundle contains our code, report, figures, fitted coefficients, source identifiers and aggregate error statistics. `files/EXTERNAL_DATA_NOTICE.txt` separates external source terms from the exact SCI baseline LICENSE. We claim no ownership of NDBC observations. This study is not an official NOAA/NWS product and has no NOAA/NWS endorsement.

## Fixed analysis

The plan is in `files/analysis_plan.txt`. It was saved before source parsing and forecast calculations. It was not independently registered or timestamped. A note records one availability correction: a first run stopped when it found no eligible Bodega cases in 2021. The final code retains that empty calendar year with zero count and zero error sums. No dates, sites, models or cutoffs changed. A later code correction fixed JSON serialization. Neither correction selected a model from forecast scores.

### Observation processing

For each source record, we kept water temperature from -2 to 35 degrees C, wind speed from 0 to 60 m/s, and wind direction from 0 to 360 degrees. Other values, including source missing codes, became missing. We checked timestamps and removed duplicates by retaining the first source record. No duplicate timestamp was found.

Let speed be `w` and direction in radians be `d`. The east and north wind components are `-w sin(d)` and `-w cos(d)`. We formed three strength or stress proxies at record level:

- strength `s2 = w*w`;
- east proxy `east = -w*w*sin(d)`;
- north proxy `north = -w*w*cos(d)`.

The proxies have units of square metres per square second. They omit air density and a drag coefficient and are not estimates of physical stress. We averaged each variable within clock hours first, then gave each hour equal weight in a UTC daily mean. Each daily variable needed at least 18 valid clock hours. This avoids giving later, more frequent sampling more weight. We used no interpolation or gap filling. Wind heights, hull changes and temperature-sensor depths were not adjusted.

There were 7,647 valid daily temperature means at Bodega Bay and 8,443 at Monterey in 2000-2023. Predictor and target completeness impose further cuts. Test origins are daily bins labelled April 1 through September 30. The issue is at the end of that UTC bin, so the first possible issue is April 2 at 00:00 UTC. At the end of day `t`, the main target is the mean of daily temperatures on `t+1`, `t+2` and `t+3`. All three days must be valid. All predictors end at or before the issue. This is a forecast of a future interval mean, not an instantaneous value at a three-day lead.

### Models and time split

The baseline has an intercept, daily temperatures at lags 0 through 7, and three wind-strength terms: current day, mean of lags 1-3, and mean of lags 4-7. Every member of a lag window must be valid. It also has annual and semiannual sine/cosine terms and a linear time term. The annual phase uses elapsed days divided by 365.2425.

The direction model adds east and north proxies for the same three windows, for six added terms. Thus it tests a particular vector feature set after a particular scalar strength model. A gain could also reflect model form or omitted weather; it does not isolate a causal effect of direction. The persistence forecast is current daily temperature.

For each site and test year, we standardized predictors with training means and population standard deviations. We fit ridge regression with penalty 1 on the sum of squared errors and no intercept penalty. The first fit used eligible April-September origins in 2000-2009. Each later test year used all eligible earlier years. Every training target ended before the test year. No test data selected a penalty. There were 1,616 Bodega training cases and 1,750 Monterey training cases for the first fit.

Within each setting, the baseline and direction model use identical training and test cases. The two sites can have different cases. The main test retained 2,103 of 2,562 possible origins at Bodega Bay (82.1%) and 2,080 of 2,562 at Monterey (81.2%). Bodega had no retained cases in 2021. Monterey had only 38 in 2017. Gaps and selection can affect the result. We do not claim skill on missing days.

### Effect and uncertainty

For each site, gain is `100 * (1 - direction SSE / baseline SSE)`, where SSE is the sum of squared errors over retained test cases. The primary effect is the arithmetic mean of the two site gains. It is not the pooled raw MSE ratio, and it is not the mean of annual gains.

We used 20,000 paired circular calendar-year bootstrap draws with seed 110711. The main block length was three years. Each draw samples blocks until it has 14 calendar years, then truncates. It resamples the same year indices at both sites and recomputes the ratios from annual error sums. Empty years remain in the axis with zero sums. One-year blocks are a planned check. Whole years preserve dependence from overlapping targets within years and much shared weather between sites. Fourteen years still give few long blocks. Circular blocks also join 2023 to 2010. The intervals condition on the fitted forecasts and observed case selection; they omit uncertainty from new training fits and do not guarantee future performance.

Planned checks used 15 temperature lags, penalties 0 and 10, direction terms delayed three days, and next-day and next-seven-day targets. For the delay test, baseline, current-direction and delayed-direction fits use the same reduced sample. The delayed model replaces all vector terms with their values three days earlier and retains current scalar strength and temperature. Its score is relative to the scalar baseline. A delay therefore changes timing and is not a pure test of information loss.

A planned warm-start test used current temperature departure from a seasonal and linear-time mean fitted only on training data. A start was warm if this departure reached the training 90th percentile. This definition uses no future outcome. It is not a standard marine heatwave definition or a direct measure of recovery time.

## Results

All gains below compare direction with the baseline containing temperature history and scalar wind strength. Brackets are conditional 95% intervals from three-year blocks, unless stated otherwise.

| Site | Main cases | Baseline RMSE (degrees C) | Direction RMSE | Persistence RMSE | MSE reduction (%) |
| --- | ---: | ---: | ---: | ---: | ---: |
| Bodega Bay, 46013 | 2,103 | 0.6689 | 0.6641 | 0.7378 | 1.43 [0.08, 3.26] |
| Monterey, 46042 | 2,080 | 0.5488 | 0.5457 | 0.6199 | 1.13 [-0.26, 2.29] |
| Equal-site mean gain | 4,183 total | — | — | — | 1.28 [0.05, 2.56] |

RMSE fell by only 0.0048 degrees C at Bodega Bay and 0.0031 at Monterey. Mean absolute error fell from 0.5214 to 0.5166 degrees C at Bodega Bay and from 0.4282 to 0.4263 at Monterey. These are small changes. A positive mean point estimate is not enough to show practical value or reliable skill in a new period.

| Planned setting | Total cases | Equal-site mean MSE reduction (%) | Conditional 95% interval (%) |
| --- | ---: | ---: | ---: |
| Main, three-year blocks | 4,183 | 1.28 | 0.05 to 2.56 |
| Main, one-year blocks | 4,183 | 1.28 | -0.22 to 3.01 |
| 15 temperature lags | 4,066 | 1.23 | -0.13 to 2.68 |
| Ordinary least squares | 4,183 | 1.26 | 0.04 to 2.55 |
| Ridge penalty 10 | 4,183 | 1.35 | 0.13 to 2.64 |
| Direction delayed three days | 4,147 | -0.75 | -1.47 to 0.05 |
| Next-day target | 4,219 | 1.26 | 0.54 to 2.10 |
| Next-seven-day target | 4,119 | -0.55 | -2.17 to 1.44 |
| Main target, warm starts only | 416 | -0.93 | -2.94 to 2.37 |

The main point estimate stayed positive with longer temperature history and both other penalties. But the longer-history interval reached below zero. The one-year interval also reached below zero. The short interval mean for the next day had a positive gain at both sites. The seven-day target did not. These are planned comparisons, not independent replications. Changing horizons and history also changes case eligibility.

Warm starts had 226 cases at Bodega Bay and 190 at Monterey. Their gains were -0.16% [-2.61, 7.34] and -1.70% [-4.98, -0.29], respectively. The mean gain was -0.93% [-2.94, 2.37]. Thus this feature set gave no clear added benefit for the warm subset. Warm-start baseline RMSE was 0.9787 degrees C at Bodega Bay and 0.6540 at Monterey. Adding direction changed them to 0.9795 and 0.6596, respectively. We make no positive heat-recovery forecast claim.

![Forecast error at all retained starts and at warm starts.](files/forecast_error.png)

`files/year_scores.csv` gives case counts, squared-error sums, absolute-error sums and signed-error sums for every year, site, setting and subset. `files/summary.csv` includes both block lengths for all settings and subsets. `files/bootstrap.csv.gz` preserves all three-year-block gain draws. We do not hide negative settings or low-coverage years.

## Interpretation and limits

The result is compatible with a short delayed temperature response to wind direction. It does not establish that explanation. Water transport, upwelling, surface heat exchange and shared weather can produce statistical associations. We did not measure currents, mixed-layer depth, heat flux or subsurface temperature. We did not fit a physical model. We did not test nonlinear wind-strength controls, interactions with season or climate mode, partner-buoy predictors, or forecast future winds. These omissions limit any attribution to wind direction.

The benchmark gives a useful limit on a simple method: adding recent local vector information after eight days of local temperature gave a small three-day gain and no clear warm-start gain in the retained sample. The main inference changes with reasonable uncertainty settings. A claim that local direction reliably improves three-day forecasts would be stronger than this evidence permits.

The two sites and their shared weather do not represent the whole California Current. Archive revision and sensor changes limit operational use. Variable coverage can remove difficult weather. The 2010-2023 test contains only 14 calendar years and an empty Bodega year. Models were refitted annually, so this is a sequence of past-only forecasts, not a single frozen model. The bootstrap does not refit those models. Multiple planned settings and subsets add context but do not form one adjusted family of significance tests. The small RMSE differences may not matter in practice.

The next useful test is a fixed model applied to other coastal buoys and a later, untouched period, with real-time data delays and independent sensor checks. A test with future wind forecasts could distinguish the value of recent wind memory from the value of future forcing. Those tests remain open. No further campaign work is queued by this job.

## Numerical checks and reproduction

The analysis program independently solved eight selected ridge fits with augmented least squares and an explicit intercept. Its predictions agreed with the main normal-equation solution to less than 4.1e-14 degrees C. `files/numerical_audit.json` gives those checks and training target dates.

The separate `files/audit.py` checked all 56 main site-year-subset score groups against external saved forecasts. The largest squared-error-sum difference was 1.42e-9 after decimal serialization. It checked all 42 saved three-year intervals and all aggregate point effects. It also used a separate raw-line parser on six source days to check hourly and daily temperature processing. `files/audit.json` records the checks and hashes of the external daily and forecast tables. Those tables can be regenerated and need not survive this worktree.

Use Python 3.12 and the packages in `files/requirements.txt`. From the extracted publication root, use a separate sibling directory for every generated file:

```
# Reuse the shared store. Replace this path if the store is mounted elsewhere.
python files/analyze.py --data-root /mnt/dell-data/shared_datasets \
  --scratch ../sst_reproduction/scratch --out ../sst_reproduction/results
python files/audit.py --evidence ../sst_reproduction/results \
  --scratch ../sst_reproduction/scratch \
  --data-root /mnt/dell-data/shared_datasets \
  --output ../sst_reproduction/audit.json
```

If the shared inputs are unavailable, retrieve the exact source snapshot into separate local scratch first:

```
python files/retrieve.py --dest ../sst_reproduction/raw
python files/analyze.py --data-root ../sst_reproduction/raw \
  --scratch ../sst_reproduction/scratch --out ../sst_reproduction/results
python files/audit.py --evidence ../sst_reproduction/results \
  --scratch ../sst_reproduction/scratch --data-root ../sst_reproduction/raw \
  --output ../sst_reproduction/audit.json
```

Retrieval is sequential and checks every source hash. It stops if a current file differs from the recorded snapshot. It does not claim that mutable URLs will always return the original bytes. The saved aggregate error tables, fitted parameters and bootstrap draws permit inspection of the claims without downloading raw data. A full rerun needs the source snapshot. The programs reject outputs inside the publication folder. Do not add regenerated raw or record-level data to the signed draft. No private key is needed for analysis.

## Job identity

Campaign: `11_07_2026`. Job: `sci-1107-hp-earth-and-ocean-sciences-f5656e707f05`. Topic: `earth-and-ocean-sciences`. Machine: `hp`. Account: `codex-olen`. Model: `gpt-6.1-sol`, high reasoning effort, through the Codex harness in T3 Code. Analysis date: 2026-11-11 UTC. This was one finite worker with no subagents. Numerical libraries used one thread. The signing identity is a campaign-machine key and is not a personal authorship claim. `files/job.json` records this identity and the data provenance location. No private key is bundled.
