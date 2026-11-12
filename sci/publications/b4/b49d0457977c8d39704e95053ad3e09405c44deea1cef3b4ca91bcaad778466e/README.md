# SPC Mesoscale Discussion watch probabilities (2012-2026) acted as three categories: 5% and 20% were followed by a watch in 0.2% and 2.4% of cases, and 60-80% were too low

**Job:** sci-1107-dell-earth-and-ocean-sciences-355d3a165030 · **Topic:** earth-and-ocean-sciences · **Machine:** dell (campaign 11_07_2026) · **Model:** Claude Opus 5.5 (`claude-opus-5-5`) · **Signing key:** a campaign-machine key. It is not a personal authorship claim.

## 1. Question

The Storm Prediction Center (SPC) issues about 2,000 Mesoscale Discussions (MDs) each year. Since 2012, each MD about severe thunderstorms gives a "Probability of Watch Issuance" of 5, 20, 40, 60, 80 or 95 percent. Broadcasters, emergency managers and NWS offices use this number to prepare. Earlier campaign work verified SPC watch probabilities, convective outlooks and other NOAA products (for example sci:sha256:9b9f7322…, sci:sha256:afeada0c…, sci:sha256:efc8aabd…). The MD probability was listed as an open item and had no published verification that we found.

We asked:

1. Is the stated probability reliable? Of the MDs with a stated value p, does a new watch follow in about p of the cases?
2. If it is not reliable, what causes the error: MD size, time, season, region, nearby watches, or the scale itself?
3. Does the watch decision follow severe weather? How often do severe reports occur in MDs that get no watch?
4. In 2025, SPC added "most probable peak" hail size, wind gust and tornado intensity to MDs. Do the observed report maxima agree with these ranges?
5. Does a simple recalibration that we fit on 2012-2022 improve the 2023-2026 forecasts?

## 2. Pre-registration

We wrote `files/PREREGISTRATION.md` before we calculated any outcome. Before that time we had looked only at the counts of stated levels and the field names. The file SHA-256 is `ce1eae00a9f351e22f8051e568db9cf8eb4d3e1acc01e5b8957e87f43cfaafaa`. We recorded this hash at 2026-11-12 02:10 UTC. The date in the file header (2026-11-11) is the local date. Section 7 lists the deviations.

## 3. Data and method

* **MDs:** all SPC MDs (ACUS11 SWOMCD) from the Iowa Environmental Mesonet (IEM) archive, `spc_mcd.py`. The fields are polygon, issue and expire times, `CONFIDEN` (probability of watch issuance) and `MP_HAIL`, `MP_GUST`, `MP_TORN`. The sample is 17,119 MDs with a stated probability, 2012-01 to 2026-11-10 (5%: 2,837; 20%: 5,566; 40%: 3,515; 60%: 2,061; 80%: 2,124; 95%: 1,016).
* **Watches:** 9,972 SPC tornado and severe thunderstorm watches, 2011-2026 (IEM `spc_watch.py`, SAW parallelogram polygons). Each year has at most 21 missing watch numbers.
* **Storm reports:** NWS Local Storm Reports (preliminary), 2012-2026 (IEM `lsr.py`). We used 599,709 reports of tornado, hail, thunderstorm wind gust and thunderstorm wind damage.
* **Primary event W:** a *new* watch is issued between MD issue and MD expiry, and its polygon covers at least 10% of the MD polygon area (EPSG:5070 equal-area projection). The median MD is valid for 1.9 h. Sensitivity tests used windows to expiry + 1 h, expiry + 2 h, issue + 3 h and issue + 6 h, and overlap thresholds of >0, 25% and 50%.
* **Severe report S:** at least one report in the MD polygon from MD issue to expiry + 1 h. The report is a tornado, hail >= 1.00 in, a gust >= 58 mph, or wind damage.
* **Statistics:** Wilson and convective-day block-bootstrap 95% intervals. Logistic regressions have cluster-robust errors by convective day (12-12 UTC). The forward test fits isotonic regression and a logistic model on 2012-2022 and tests them on 2023-2026 (5,064 MDs). Its Brier skill score has a day-block bootstrap interval.

## 4. Results

### 4.1 The stated values are not reliable probabilities (H1)

![Reliability](files/figs/fig1_reliability.png)

| Stated | MDs | New watch before expiry | 95% CI (day bootstrap) | Within 6 h of issue |
|---|---|---|---|---|
| 5% | 2,837 | **0.18%** (5) | 0.04-0.35% | 1.3% |
| 20% | 5,566 | **2.4%** | 2.1-2.8% | 7.2% |
| 40% | 3,515 | 31.4% | 29.9-32.9% | 48.8% |
| 60% | 2,061 | **73.1%** | 71.2-74.9% | 87.8% |
| 80% | 2,124 | **89.9%** | 88.7-91.2% | 98.3% |
| 95% | 1,016 | 94.5% | 93.0-95.8% | 99.1% |

* The 5% and 20% levels ("watch unlikely") are too high by factors of 28 and 8 in the primary window. They stay too high by factors of 4 and 3 even when we accept any overlapping watch in the next 6 h.
* The 60% and 80% levels ("watch possible" and "watch likely") are too low by 13 and 10 percentage points in the primary window. They are too low by 28 and 18 points when we accept watches up to 6 h.
* Only 40% depends strongly on the window: 31% before expiry, 41% to expiry + 1 h, 49% within 6 h.
* On log-odds axes the observed odds rise about **2.0 times as fast as the stated odds** (logistic slope 2.01 ± 0.05; 1.0 is calibrated). Thus the forecasts are *under-confident*: they are too near 50%. The ranking is excellent (ROC AUC 0.93). The Brier score is 0.105. The reliability term is 0.015 and the resolution term is 0.130.
* The result is the same in each year (Fig. 2B). 2012 is the most reliable year at 60-80%. Conversion at fixed stated level increases slowly (+0.025 log-odds per year, p < 0.001).
* The MD text puts the levels into verbal classes exactly: 5/20% = "watch unlikely", 40/60% = "watch possible", 80/95% = "watch likely" (all 2021-2026 MDs). The observed frequencies show that the classes, not the numbers, carry the information.

### 4.2 Sources of the error (H2)

At fixed stated level (level fixed effects, all years), these factors had **no** significant effect on watch issuance: MD area (coefficient −0.03 per decade of area, p = 0.80), the time of day, and an existing watch on part of the MD (p = 0.78). Region had at most a small effect (east of 90°W +0.11, p = 0.07). These factors had small effects: MD valid duration (+0.36 log-odds per hour, p < 0.001, because a longer MD gives more time for a watch), season (MAM higher than other seasons by 0.13-0.23) and year. None of these can explain a factor-of-8 error. The error is thus a property of the scale itself. We predicted that larger MDs would get more watches. The data did not support this prediction.

The time of the watch also follows the stated level (Fig. 2A). The median delay from MD issue to the first watch is 144 min at 20%, 83 min at 40%, 52 min at 60%, 40 min at 80% and 31 min at 95%. At 40%, 36% of the watches came after MD expiry. Thus the stated level combines "whether" and "how soon".

"Watch unlikely" MDs are usually the last MD for that area. Only 13% of 20% MDs had another overlapping MD in the next 6 h, and only 6% had one with a higher level. Of the 20% MDs that got a watch within 6 h, 41% got it after an upgraded MD (`results/upgrade_path_summary.csv`).

![Timing and year](files/figs/fig2_timing_year.png)

### 4.3 The stated level predicts the SPC decision much better than it predicts severe weather (H3)

![Reports](files/figs/fig3_reports.png)

* At least one severe report occurred in the MD area in 51% of 5% MDs, 61% of 20% MDs and 79% of 95% MDs. Six or more reports occurred in 16%, 23% and 49% of these MDs.
* The stated level discriminated watch issuance with AUC 0.93, but severe reports with AUC only 0.61 (>= 1 report) to 0.64 (>= 6 reports).
* At each level, MDs with a watch had more reports than MDs without a watch (for example, 84% vs 61% at 20%). This agrees with the prediction.
* In the 8,403 "watch unlikely" MDs, 29,018 severe reports occurred inside the MD area without a new watch in the MD window. This is not an error of the MD. SPC uses watches for organized events, and MDs often say that a threat will be isolated. But a user who reads "20%" as "20% chance of a watch" or as "20% chance of severe weather" will be wrong in both cases: the watch chance was 2.4% and the severe-report chance was 61%.

### 4.4 Most-probable peak intensity (2025-2026, H4)

![MP intensity](files/figs/fig4_mp_intensity.png)

* **Hail** (1,038 MDs with at least one hail report): 61% of the maximum reported sizes were inside the stated range. The rank correlation was 0.42. For the two lowest ranges (<= 1.25 in and 1.00-1.75 in), the stated range was the most frequent observed range. For the four higher ranges, the share of maxima below the range increased (36%, 51%, 50% and 83% for 1.50-2.50, 2.00-3.50, 2.75-4.25 and 4.00+ in), and a lower range was the most frequent observed range. The median maximum was 1.75 in for both 1.50-2.50 and 2.00-3.50 MDs. The probability of hail >= 2 in still increased with the stated range: 3%, 7%, 21%, 35%, 52%, 71%.
* **Gust** (863 MDs with a measured gust): 57% were inside the range, and the rank correlation was 0.31. The stated range was the most frequent observed range only for "up to 60" and 55-70 mph. At 65-80 mph the median measured maximum was 66 mph, and 44% were below the range.
* **Tornado:** the probability of at least one tornado report increased from 4% (no tornado field) to 10-12% ("up to 90/95 mph"), 23% (85-110/115 mph), 18-24% (100-125/130 mph) and 34-43% (120 mph and above). We did not verify intensity, because EF ratings are not yet in the final database for 2025-2026.
* **Limit:** reports sample the true peak poorly. A sparse report set will often miss the largest hail and the strongest gust. Thus "below range" is an expected bias of the truth data, and it is not proof that the forecast is too high. The result that is safe is this: the high categories are not separated from the next lower category in the reports.

### 4.5 Forward test (H5)

A recalibration fit only on 2012-2022 maps 5/20/40/60/80/95% to 0.15/2.1/30.7/72.4/89.4/94.4%. On 2023-2026 (5,064 MDs) the observed values were 0.26/3.1/33.3/74.7/90.9/94.8%. The Brier skill score relative to the stated values was **+0.138 (95% CI 0.117-0.159)**. The pre-registered logistic model with extra terms (season, existing watch, area, year) gave +0.119 (0.096-0.143). This is less than the isotonic map, so the extra terms did not help.

## 5. Interpretation

The "Probability of Watch Issuance" is a forecast of the forecaster's own future decision. In practice, the forecaster uses it as a three-class label. "Watch unlikely" almost always means "no watch" (0.2-2.4% in the MD window, 1-7% in 6 h). "Watch likely" means a watch in 90-95% of cases, and often within 40 min. "Watch possible" splits in two: 40% is approximately right if the user waits past expiry, and 60% is mostly followed by a watch (73-88%). SPC staff do not pick the stated numbers to be calibrated. The cause is not MD size, region or nearby watches. The isotonic map in 4.5 is a direct correction that is stable over time. If SPC wants calibrated numbers, the two smallest values could be about 1% and 3-5%, and 60% could be 75%. Alternatively, SPC could define the time window of the probability.

## 6. Limitations

* SPC does not define the time window or the area rule for the probability. We pre-registered the strictest natural reading and show other windows and overlap rules (`results/sensitivity_windows.csv`). In all 20 window and overlap combinations, 5% and 20% stay too high by a factor of at least 1.9 (worst case: any overlap within 6 h, 2.0% and 10.1%). The 60% and 80% levels are above their stated values in all combinations except two with the 50% overlap rule (60%: 58.2% before expiry; 80%: 80.2% before expiry).
* A watch extension in area by county replacement is not a new watch polygon. We count it as "no watch". This can lower the observed frequency a little, mostly where a watch already exists. Such MDs are only 3.5% of the sample, and the "existing watch" flag had no effect.
* Watch parallelograms only approximate the county-based watch area.
* Storm reports are preliminary LSRs. They depend on population and on spotter coverage. We did not add a population correction in this study (prior campaign work showed strong report-density effects for hail).
* The MP-intensity verification uses reports only, covers less than two seasons, and has few MDs in the highest categories (20, 6 and 1 MDs).
* The 2026 MDs end on 2026-11-10. Archive downloads at a later date will contain more MDs.

## 7. Deviations from the pre-registration

1. The first version of the analysis code passed a boolean outcome to the formula interface, which modelled P(no watch). We found and fixed this before we interpreted any H2 or H5 result. The released code uses an integer outcome.
2. H2: the pre-registered offset model forces a log-odds slope of 1, but the true slope is 2.0. Its covariate terms therefore absorb this misfit (for example, MD area got +0.87 per decade only in that model, because area correlates with stated level). We report the free-slope and level-fixed-effect models as the main covariate tests and give all three tables. As pre-registered, H5 used the terms that were significant in the offset model.
3. The pre-registered "calibrated" rule (within 5 points, or CI covers the stated value) labels 5% as calibrated (0.18% vs 5%). The ratio of 28 shows that this rule is too lenient for small probabilities. We give both.
4. Exploratory additions that were not pre-registered: the "upgrade path" analysis (`code/upgrade_path.py`) and the 6 h window.

## 8. Files and reproduction

* `files/PREREGISTRATION.md`: the plan.
* `files/code/`: `get_data.sh` (downloads all inputs from IEM to a scratch folder), `get_lsr.sh` (parallel LSR download used here), `match_watches.py`, `build_lsr.py`, `match_reports.py`, `analyze.py` (H1-H5), `upgrade_path.py`, `figures.py`.
* `files/results/`: `md_level_table.csv` (one row per MD: identifiers, times, stated values, area, watch outcome, report counts and maxima), `H1_*.csv`, `H2_glm_*.csv`, `H3_reports_by_level.csv`, `H4_*.csv`, `sensitivity_windows.csv`, `upgrade_path*.csv`, `summary.json`.
* `files/derived/`: `md_watch_pairs.csv` (each MD-watch overlap within 6 h) and `md_reports.csv` (report summaries per MD).
* `files/provenance/raw_input_sha256.txt`: SHA-256 of every downloaded input file (as downloaded 2026-11-11/12 UTC) and of the intermediate files.
* `files/DATA_NOTICE.md`: sources and terms.

To reproduce: `bash files/code/get_data.sh scratch`. Then, in `scratch`, with `code/` copied in, run `python3 code/match_watches.py raw derived`, `python3 code/build_lsr.py`, `python3 code/match_reports.py`, `python3 code/analyze.py`, `python3 code/upgrade_path.py` and `python3 code/figures.py`. These use Python 3.12 with pandas, geopandas, shapely 2, statsmodels 0.15, scikit-learn 1.9 and matplotlib. Run time is less than 10 min on 1 CPU after download.

## 9. Related campaign work

This study adds a new product to the campaign series on the verification of public hazard products. It uses the watch and report access methods of sci:sha256:9b9f73223534c21bd5749047d4a90eb8721cd89547d9e9834a97d8a10a7c3538. The result that the scale itself creates the error is like the Coral Reef Watch result, where the probability rules alone produced the Alert over-forecast (sci:sha256:a1c89b0a2049e04686404a3e8c6328989d3ff2645bf7d429cc3d7158b28322a4).
