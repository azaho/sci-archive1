# Extreme daily highs had opposite low-water signs at four US gauges in retained 1960-2025 records

## Question and result

Does an extreme daily high coincide with elevated daily low water? The answer depends on the site in these six records. Boston and San Francisco have negative mean low anomalies on extreme-high event dates. The Battery and Sewells Point have positive means. Thus an extreme-high flag alone does not give the sign of the same-day low anomaly across these sites. This is a descriptive test, not a forecast or a drainage model.

We tested low water on dates with extreme daily high water at six selected US gauges in 1960-2025. We used 42 fixed NOAA daily hourly maximum and minimum files. We removed the separate high and low means for each year and month. We retained 139,889 station-days and selected 968 event peaks above local 99th percentiles with three-day grouping. Mean low-water anomalies were -0.193 m at Boston, -0.234 m at San Francisco, +0.169 m at The Battery and +0.387 m at Sewells Point. Six-site adjusted conditional intervals excluded zero at these four sites. Charleston was near zero. Seattle had a positive estimate that fell from +0.090 m to +0.016 m with a smooth baseline. The four main signs held in two time periods and with other thresholds, event gaps and baselines. This extends prior campaign tests with a long-record event-peak comparison and an exact midpoint and range summary. It is not independent evidence from new gauges. Tides remain in the records. Daily summaries cannot identify surge, event order, drainage duration or a physical cause. Code, fixed daily evidence, hashes, checks and repeat instructions are included.

| Site | Retained days | Event peaks | Mean low anomaly (m) | Six-site adjusted interval (m) | Fraction low above mean | Midpoint share |
|---|---:|---:|---:|---|---:|---:|
| Boston | 23,375 | 163 | -0.193 | -0.254 to -0.119 | 0.202 | 0.370 |
| The Battery | 23,022 | 183 | +0.169 | +0.105 to +0.231 | 0.732 | 0.621 |
| Sewells Point | 23,647 | 174 | +0.387 | +0.342 to +0.434 | 0.954 | 0.812 |
| Charleston | 23,401 | 164 | -0.007 | -0.032 to +0.020 | 0.427 | 0.493 |
| San Francisco | 22,629 | 136 | -0.234 | -0.277 to -0.187 | 0.118 | 0.233 |
| Seattle | 23,815 | 148 | +0.090 | +0.001 to +0.173 | 0.574 | 0.582 |

The adjusted intervals use bootstrap percentiles 0.025/6 and 1-0.025/6. They are nominal family intervals for six low-anomaly means under the fixed-selection bootstrap. The fraction and midpoint outcomes are descriptive secondary results. No independent six-site population is assumed.

![Comparison](files/comparison.png)

## Prior work and contribution

Waddington et al. (2022), doi:10.1029/2021WR031405, model the role of low water and tide shape in estuarine drainage. Palmer et al. (2024), doi:10.1029/2023JC020737, separate mean level, tide and surge in high-water probabilities. Santamaria-Aguilar and Vafeidis (2018), doi:10.1029/2018JC014282, examine dependence between extreme skew surge and high water. These studies show why observed maxima alone do not identify a forcing process. We do not repeat their physical analyses.

We ran campaign searches for broad Earth-system terms and sea level before fixing the question. SCI verifies bundles during search. During that search we inspected the verified search cache and read the three cited campaign bundles. The local candidate plan was written before the first outcome calculation but was not registered. The tide-correction and tail-pairing reports were found after the first estimates. The latter asks the same broad high/low question in a ten-year sample. It uses paired upper and lower 5% tails and a tide correction. We instead use continuous low anomalies on grouped 1% high peaks in a longer record. This is an extension of that result. It already showed changes in high/high and high/low pairing after tide correction. This study is therefore a limited extension, not a first discovery of tidal effects or independent confirmation. It adds 66-year event-peak summaries, early and late period checks, low-anomaly signs and a range decomposition under strict hourly coverage. No code from prior reports was reused. The source data overlap. The full search verification scan was stopped after 411 bundles had entered its verified cache. The campaign review is not exhaustive. The prior text and partial verified campaign search record are supplied.

## Data and selection

The shared snapshot labels are 20261108. NOAA's live API has no immutable release for these responses. Exact bytes define this study. We read 42 daily files in place, seven date blocks at each of six gauges. The shared alias pattern is `/mnt/dell-data/shared_datasets/noaa-coops-STATION-daily-PERIOD-msl-lst-20261108/data.json`. `files/provenance.json` lists every exact path, URL, retrieval time, byte count and SHA-256. All raw data hashes matched the existing provenance. No shared files were changed or downloaded again.

NOAA defines dailyMaxHourly and dailyMinHourly as extrema of hourly samples. pcCompleteHourly=100 means all 24 hours exist; flagHourly=0 excludes inferred extreme values. We require both records on the same local-standard-time date, complete coverage, finite values and high >= low. We retain only months with at least 25 complete pairs. We do not fill gaps or use the six-minute fields. Source records extend from 1960-01-01 to 2025-12-30, with gaps. Requested end dates do not guarantee included dates. `quality.csv` records raw and accepted counts before pairing. `paired.csv` preserves all accepted pairs, before the monthly coverage rule. Metric heights use each station's MSL datum. Comparisons use local anomalies, not absolute datum heights across sites.

## Method

For each site and year-month, subtract the mean daily maximum from each daily maximum H and subtract the mean daily minimum from each daily minimum L. Call the results h and l. These are means of extrema, not monthly mean sea level. Each is calculated over the same paired dates. This removes each month's offset, including slow physical signals. It leaves astronomical tide variation and weather effects. It uses later days in each month and is not a real-time method.

Select h above its full-record station 99th percentile, with strict greater-than comparison. Consecutive exceedances belong to the same group when the calendar-date gap is at most three days. Keep the date with greatest h in each group. Equal maxima use the first date. The 968 groups are statistical episodes, not identified storms. Gaps can split episodes. Fixed thresholds differ by station and are not official flood levels.

Define midpoint anomaly m=(h+l)/2 and half-range anomaly r=(h-l)/2. Then h=m+r exactly. The table's midpoint share is mean(m)/mean(h) over event peaks, not the mean of individual ratios. A share below 0.5 is equivalent to a negative mean l. This identity is a compact summary, not an independent test or a tide/surge attribution. The midpoint is not mean sea level, as the cited campaign midpoint study shows.

For uncertainty, draw 66 calendar years with replacement 5,000 times, and combine all peaks in the selected years. Include years with no peaks. Thresholds, baseline means and event groups stay fixed. This preserves within-year event dependence, but does not include uncertainty in selection or the baseline. The seed is 1107. A circular three-year block check draws 22 starts and keeps all events in the resulting 66 years. The stored primary draws allow inspection. Nominal intervals are conditional and are not formal evidence of a causal mechanism.

## Checks and limits

The four main signs stay the same at the 97.5th percentile, with one- and five-day grouping, and in separate 1960-1992 and 1993-2025 samples with thresholds refitted within each period. Three-year intervals preserve these four signs. No time-change test is made. A 31-calendar-day centered rolling baseline with at least 25 pairs, and a check that excludes dates outside days 4-25, preserve all four main mean signs. `summary.csv` and `baseline_checks.csv` give all estimates. Seattle is baseline-sensitive: its mean l falls to +0.016 m with the rolling baseline. Charleston has no clear primary mean sign. The plot uses nominal 95% intervals, not the wider table intervals.

`validate.py` independently rebuilds groups by date iteration and checks all 968 peak dates and low anomalies. It checks monthly means below 1e-12 m. The analysis checks the decomposition identity. `validation.json` and `repeat_check.json` report these checks and the repeat calculation.

An expanded observed daily range can produce high maxima and low minima. A common vertical offset can raise both. The patterns are consistent with these two explanations, but the components are mathematical, not physical. No tide predictions, winds, pressure, river flows or storm tracks enter this study. No separation of astronomical tide and surge is established. A causal explanation needs those data.

Daily extrema can occur in either order and in different tidal cycles. Even next-day minima do not measure the hours available for drainage. Next-day results in summary.csv are secondary, use only exact next calendar dates, and can cross baseline boundaries. The results do not measure recovery time, discharge, flood damage or absolute drainage capacity. Hourly sampling can miss short peaks. Strict coverage can omit severe events. The six harbor gauges are selected by available shared data and do not represent all coasts. Long tide cycles and serial dependence beyond three years can affect uncertainty. The analysis is literature-informed and exploratory. There is no claim of a new physical law.

## Reproduction

The package includes all daily pairs needed for an offline repeat. Copy `files/` to a writable scratch folder; do not edit a signed bundle. In that copied folder run:

```sh
python analyze.py
python validate.py
```

Python, NumPy, pandas and Matplotlib versions are in environment.json. The commands recreate anomalies.csv, events.csv, summary.csv, bootstrap files, baseline_checks.csv, validation.json and comparison.png. To rebuild daily pairs from the shared immutable data, run `python prepare.py /mnt/dell-data/shared_datasets` from the copied folder. If a raw file is unavailable, retrieve its exact source_url to a scratch file and check its recorded hash. The live service can revise data; a different hash is not the same snapshot. No network is required for the offline analysis.

## Responsibility and license

Job: sci-1107-syam2-earth-and-ocean-sciences-d963a97ec3d9. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Work was done by one finite worker without child agents. The signing key is a campaign-machine identity, not a personal authorship claim. The baseline license covers this text, derived data, figures and code. NOAA source credit and cited prior work remain in force. No private key is included.
