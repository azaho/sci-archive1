# Automated b-value traffic lights classified 9 of 65 Japanese M5+ foreshock sequences before the larger event, and over 80% of red alarms were false (JMA, 2000-2024)

## Summary

Gulia and Wiemer (2019) proposed a "foreshock traffic light" (FTLS). After a large earthquake, the method compares the b-value of the next events with the background b-value. A drop of more than 10% gives a red light: a larger earthquake can follow. A rise of more than 10% gives a green light: the sequence is a normal aftershock sequence. The original test used 29 hand-selected sequences and reported 95% success.

We applied the rule automatically and causally to every shallow (depth 50 km or less) first event of magnitude 5.0 or more in the Japan Meteorological Agency (JMA) unified hypocenter catalog, 2000 to 2024. A "first event" is the largest event near its location in the previous 365 days. There are 1,459 first events (240 of M 6.0 or more). The b-value after the first event uses only events that occurred before a decision time T (0.25, 1, 3 or 10 days). The outcome is a larger event (M > M0) within one rupture length R in the next 30 days. We ran 72 settings of the free method choices and three b-value estimators.

Main results:

1. **Most larger events came too early for a decision.** 65 first events had a larger event within 30 days. Half of these larger events came within 8 hours (median delay 0.33 day). 31 of 65 came before the earliest decision time of 6 hours.
2. **Most sequences had too few events for a b-value.** At T = 1 day, only 123 of 1,459 first events (8%) had 50 or more complete post-event events and a stable background. For the 65 larger events, the FTLS (own-Mc Aki-Utsu estimator, primary setting) gave a valid class before the larger event in only 9 cases: 5 red, 2 orange, 2 green.
3. **Red alarms were mostly false.** In the primary setting (T = 1 day), 4 of 35 red alarms were followed by a larger event (11%, 95% CI 3-27%). After a non-red class, 3 of 72 were followed by a larger event (4%, 1-12%). The difference is not significant (one-sided Fisher p = 0.16). Red alarms occurred in 31% of the sequences that had no larger event.
4. **The result depends on the method choices.** Over 72 settings at T = 1 day, the median ratio of red to non-red follow-on rates was 2.4, but only 17% of settings gave p < 0.05. At T = 3 days the ratio was 0.33. The b-positive estimator gave stronger results at T = 1 day (red 4 of 22, non-red 3 of 76, p = 0.043) but no signal at T = 3 or 10 days.
5. **A simple magnitude gap ranked the sequences better.** The gap is M0 minus the largest event so far. Its area under the ROC curve (AUC) was 0.83 at T = 1 day; the FTLS AUC was 0.68 (bootstrap difference -0.28 to -0.002). The gap score had a higher AUC than the FTLS and b-positive scores in every setting at every decision time.
6. **The two famous Japanese cases repeat, but so do false alarms.** Before the 2016 Kumamoto M7.3 and the 2011 Tohoku M9.0, the b-value at T = 1 day was 17% and 37% below background (red), with all estimators. But after the largest event of Noto 2024 (M7.6), the b-positive value also stayed 13-23% below background (red) for 30 days, and after Tohoku 2011 (M9.0) it stayed near -10%.

The b-value drop has some information: at T = 1 day, red alarms were followed by larger events more often than other classes. But in an automatic, real-time application to the Japanese catalog, the FTLS could not warn before most larger events, and most of its red alarms were false.

## Question and prior work

Can the b-value traffic light (FTLS) tell, in real time, whether a large earthquake is a foreshock of a larger one? Gulia and Wiemer (2019, Nature) reported success for 29 sequences, including Kumamoto 2016. Dascher-Cousineau, Lay and Brodsky (2020) showed that expert choices (source volume, completeness correction, blind time, background period) change the result for Ridgecrest 2019 and Puerto Rico 2020. Nanjo et al. (2021, arXiv:2104.01598) found that a strict Kumamoto analysis gave an aftershock-like class before the M7.3. We know of no systematic, automated, pseudo-prospective test over a complete national catalog. This study gives one for Japan, with all free choices varied.

## Data

- JMA unified hypocenter catalog, annual files `hYYYY.zip` from https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/ (October 1997 to December 2024; `h199710.zip` and `h1998.zip` to `h2024.zip`). We read the shared campaign copies in place (`datasets/jma-hypocenter-hYYYY-20261108/hYYYY.zip`). File names, byte counts and SHA-256 hashes are in `files/data/jma_raw_files_sha256.json`.
- We keep JMA-located records (type J) of natural earthquakes (subsidiary code 1). This removes low-frequency events (code 5). We keep all magnitude types (mostly Mj from velocity and displacement amplitudes; Mw for Tohoku). Times are converted from JST to UTC. The parsed catalog has 4,613,138 natural events.

## Method

**Candidates.** All events with M0 of 5.0 or more, depth 50 km or less, between 2000-01-01 and 2024-09-30 UTC. A candidate must be the largest event near it in the previous 365 days: no earlier event of magnitude M0 or more within 2 x max(R, R_prev), where R = 10^(0.59 M - 2.44) km (Wells and Coppersmith 1994 subsurface rupture length), limited to 10-200 km. This gives 1,459 candidates (240 with M0 of 6.0 or more).

**Event volume.** Events within radius r = f x R (f = 0.5, 1 or 2; minimum 5 km) of the candidate epicenter and within 30 km of its depth.

**Background b-value.** Events in [t0 - Y years, t0 - 1 day], Y = 2 or 5. Mc = maximum curvature + c (c = 0.1, 0.2 or 0.3). If fewer than 250 events are above Mc in the volume, we use the nearest 250 complete events within 150 km (as in Gulia and Wiemer 2019).

**Post-event b-value at decision time T.** Events in (t0 + blind, t0 + T], blind = 0.01, 0.05, 0.25 or 0.5 day (blind < T). Three estimators:
- *aki* (FTLS style): Mc = maximum curvature + c on the post-event events; Aki-Utsu maximum likelihood with bin correction on the latest 400 complete events; 50 or more events required.
- *common*: the same, but both b-values use the larger of the two Mc values. This removes the effect of a magnitude-dependent b-value.
- *bpos*: b-positive (van der Elst 2021) from successive magnitude differences of 0.2 or more. This estimator is robust to short-term incompleteness. 50 or more differences required (100 for the background).

**Class.** Relative change db = b_post / b_ref - 1. Red: db < -0.10. Green: db > +0.10. Orange: otherwise.

**Outcome.** A later event with M > M0 (variant: M >= M0) within R (variant: 2R) and depth 80 km or less, in (t0 + T, t0 + T + W], W = 30 days (variants 90 and 365 days). Candidates whose larger event came at or before t0 + T are "resolved early" and are not in the test at that T. Candidates with less than T + W days of catalog are removed unless the event occurred.

**Primary setting.** We set it before we tabulated the M5 outcomes: T = 1 day, blind = 0.05 day, c = 0.2, Y = 5 years, f = 1, W = 30 days, M > M0 within R, all regions, aki estimator. The M>=5 set is the main set; the M>=6 set gives the same analysis at the original FTLS magnitude.

**Metrics.** Fraction of red alarms followed by a larger event (with Clopper-Pearson 95% intervals), the same fraction after non-red classes, one-sided Fisher exact test, fraction of no-larger-event sequences that were red ("false red rate"), and AUC of -db. As a simple comparison score, we use the magnitude gap M0 - (largest event in (t0, t0 + T] within r). We compare the two AUC values by a candidate bootstrap (2,000 resamples). "Operational recall" counts, for each of the 65 larger events, the class at the last decision time before the larger event.

## Results

### 1. Timing and data sufficiency

![Timing and warning status](files/figures/fig1_timing_warnings.png)

Figure 1. (a) Delay from the first event to the first larger event within R, for the M>=5 and M>=6 sets. Dotted lines are the decision times. (b) Class at the last decision time before each of the 65 larger events (M>=5 set, primary setting). Dark gray: the larger event came before 6 hours. Light gray: no valid b-value at any earlier decision time.

- M>=5 set: 65 of 1,459 candidates (4.5%) had a larger event within R in 30 days. Delay quartiles were 0.05, 0.33 and 2.2 days; 62% came within 1 day.
- M>=6 set: 9 of 240 (3.8%). Delays were 0.005 to 6.4 days (median 1.2 days).
- Valid FTLS b-values (aki, primary setting) existed for 4.5%, 8.4%, 11% and 13% of the M>=5 candidates at T = 0.25, 1, 3 and 10 days. Inside the dense-network box (30-46 N, 128-146.5 E) the fraction at T = 1 day was 18% (98 of 542). Valid candidates are larger (median M0 5.8 versus 5.3 for all).
- For the 65 larger events, the FTLS gave a valid class before the event in 9 cases: 5 red, 2 orange, 2 green (aki). The common-Mc and b-positive estimators gave 5 red and 4 red.

### 2. Primary test

Table 1. M>=5 set, primary setting (W = 30 days, M > M0 within R). "Red success" = fraction of red alarms followed by a larger event.

| Estimator | T (d) | Valid | Larger events | Red alarms | Red success (95% CI) | After non-red (95% CI) | False red rate | Fisher p | AUC b | AUC gap |
|---|---|---|---|---|---|---|---|---|---|---|
| aki | 0.25 | 63 | 4 | 29 | 3/29 = 0.10 (0.02-0.27) | 1/34 = 0.03 (0.00-0.15) | 0.44 | 0.25 | 0.69 | 0.91 |
| aki | 1 | 107 | 7 | 35 | 4/35 = 0.11 (0.03-0.27) | 3/72 = 0.04 (0.01-0.12) | 0.31 | 0.16 | 0.68 | 0.83 |
| aki | 3 | 133 | 3 | 36 | 0/36 = 0.00 (0.00-0.10) | 3/97 = 0.03 (0.01-0.09) | 0.28 | 1.00 | 0.49 | 0.71 |
| aki | 10 | 155 | 3 | 34 | 2/34 = 0.06 (0.01-0.20) | 1/121 = 0.01 (0.00-0.05) | 0.21 | 0.12 | 0.79 | 0.91 |
| common | 1 | 89 | 7 | 29 | 3/29 = 0.10 (0.02-0.27) | 4/60 = 0.07 (0.02-0.16) | 0.32 | 0.41 | 0.68 | 0.84 |
| bpos | 1 | 98 | 7 | 22 | 4/22 = 0.18 (0.05-0.40) | 3/76 = 0.04 (0.01-0.11) | 0.20 | 0.043 | 0.67 | 0.83 |
| bpos | 3 | 121 | 3 | 28 | 0/28 = 0.00 (0.00-0.12) | 3/93 = 0.03 (0.01-0.09) | 0.24 | 1.00 | 0.35 | 0.69 |

All rows are in `files/results/primary_table_M5.csv` and `files/results/primary_table_M6.csv`. In the M>=6 set at T = 1 day, the FTLS had 56 valid sequences and 3 larger events; 2 of 16 red alarms were followed by a larger event (Fisher p = 0.19).

![Primary scatter](files/figures/fig3_primary_scatter.png)

Figure 2. Relative b change at T = 1 day against the magnitude gap, M>=5 set, primary setting. Colored points had a larger event in (1, 31] days. Dashed lines are the traffic-light thresholds.

At T = 1 day (aki), the seven larger-event sequences were: red for Kumamoto 2016-04-14 (M6.5), off Sanriku 2011-03-09 (M7.3), west of Kyushu 2004-12-12 (M5.1, 31.8 N) and the Izu Islands 2000-06-29 (M5.7, 34.1 N); orange for 2010-05-16 (M5.0, 28.8 N) and 2023-09-08 (M5.1, 29.3 N) in the Ryukyu arc; green (+37%) for 2007-07-31 (M6.1, 27.4 N). All seven had a small magnitude gap (0.1-0.8) except the green 2007 case (1.6).

### 3. Robustness over the method choices

![Grid robustness](files/figures/fig4_grid_robustness.png)

Figure 3. Distribution over all settings (radius factor, blind time, Mc correction, background years) for the M>=5 set (W = 30 days, M > M0 within R). (a) Fraction of red alarms followed by a larger event; black bars: rate after non-red classes (aki, median). (b) Fraction of no-larger-event sequences flagged red. (c) AUC of the b-value score; diamonds: AUC of the magnitude gap.

- At T = 1 day, the median red/non-red ratio was 2.4 (aki), 1.7 (common) and 8.7 (bpos). The fraction of settings with Fisher p < 0.05 was 17%, 1% and 62%.
- At T = 3 days, no estimator gave a signal (median AUC 0.49-0.57; no red alarm in the primary setting was followed by a larger event).
- The false red rate was 19-58% (aki) and 18-36% (bpos) over the settings. It was largest at T = 0.25 day, when short-term incompleteness is largest.
- The magnitude-gap AUC (0.84-0.94 median) was higher than the b-value AUC in all aki and bpos settings and in all but 1-6% of the common-Mc settings (`files/results/grid_robustness_M5.csv`).

**Outcome definitions** (`files/results/outcome_variants_M5_T1.csv`). With W = 365 days, the aki red success was 6/33 (18%) against 6/67 (9%) after non-red (p = 0.16). Inside the dense-network box, all 4 larger events at T = 1 day followed red alarms, but 26 of 86 other sequences were also red (red success 4/30 = 13%; p = 0.011). The box was a planned sensitivity analysis, but with 4 events this result is fragile.

### 4. Case series

![Case series](files/figures/fig2_case_series.png)

Figure 4. Relative b change against decision time for eight well-known sequences (median and 10-90% range over 72 settings). Each b-value uses only events before T. The vertical line marks the larger event; values after it include that event's own aftershocks.

- Kumamoto 2016 M6.5: median red with both estimators from 0.1 day to the M7.3 at 1.2 days (aki median -18% to -35%; bpos -21% to -23%).
- Off Sanriku 2011 M7.3: red from 0.26 day to the M9.0 at 2.1 days (aki -29% to -47%; bpos -26% to -29%).
- Largest events: Chuetsu 2004 M6.8 (aki red for the first 0.3 day), Iwate-Miyagi 2008 M7.2 (mostly orange or green), Kumamoto M7.3 (green or orange, then bpos near or below -10% after 4 days), Tohoku M9.0 (bpos -3% to -18%, near -10% for most of 30 days; aki changes sign), Noto 2024 M7.6 (bpos red, -13% to -23%, for 30 days). Noto 2024 is a clear false red alarm under b-positive; Tohoku M9.0 is at the red threshold.
- Noto 2023 M6.5 (the M7.6 came 241 days later): green or orange in the first days.

## Interpretation

The b-value after a large shallow earthquake in Japan was lower before a larger event in the best-known cases. At T = 1 day, red alarms were followed by larger events about 2-4 times more often than other classes. This agrees with the direction of the Gulia and Wiemer (2019) result. But the operational value is small:

- Half of the larger events came within 8 hours, before a b-value is possible.
- Most sequences do not produce 50 complete events in a day, so the method gives no class.
- With a base rate near 4%, a false red rate of 20-45% means that most red alarms (82-100% in the primary rows) are false.
- The signal is not stable with T: at 3 days it is absent.
- A trivial score (how close the largest early aftershock is to the first event) ranks the sequences at least as well. Part of the b-value signal can come from the same information: a large early aftershock changes the post-event magnitude distribution.

The 95% success of the original study does not transfer to an automated test on a complete catalog. The difference comes mostly from the selection of cases, the treatment of non-decisions ("orange" and "no data" are not failures there), and the many false red alarms in the full population.

## Limitations

- **Few positive cases.** At each decision time there are only 2-7 larger events with a valid class. All confidence intervals are wide. We cannot exclude a moderate real effect.
- **Simplified source volume.** We use a circle of radius f x R around the epicenter, not a fault-plane volume. We vary f from 0.5 to 2 to cover this. Gulia and Wiemer used a fault-oriented volume and expert choices; our automatic version is not identical to theirs.
- **Completeness.** Mc by maximum curvature is not reliable in the first hours. The b-positive estimator is less sensitive, and gives the same main conclusion.
- **Mixed magnitude types.** JMA uses velocity and displacement magnitudes in different ranges; the b-value can depend on the magnitude range. The common-Mc estimator controls this and gives weaker results.
- **One catalog.** Only JMA, 2000-2024. Offshore and distant regions (Ryukyu, Izu-Bonin, Taiwan, Kuril) have high Mc and few valid sequences.
- **Outcome definition.** A "larger event" within R. Larger events farther away (for example in a long subduction rupture) are not counted; the 2R variant gives the same results.
- **Multiple settings.** We report all settings; the primary setting is one of 72, chosen before the M5 outcomes were tabulated. The M6 primary results were seen before the M5 run.

## Reproduction

1. Get the JMA files `h199710.zip`, `h1998.zip` to `h2024.zip` (shared copies or the JMA URL above). Check the SHA-256 values in `files/data/jma_raw_files_sha256.json`.
2. Run `cd files/code && bash run_all.sh <DATASETS_DIR> <WORK_DIR>` (Python 3.12; versions in `files/code/environment.txt`). The M>=5 grid takes about 20 minutes on one core.
3. Without the raw catalog, `03_evaluate.py`, `05_summary.py` and `06_figures.py` run from the saved tables in `files/data` (rename `candidates_M5.csv` to `candidates.csv` and `bvalues_grid_M5.parquet` to `bvalues_grid.parquet` in one folder per set).

## Files

- `files/code/01_parse_jma.py`: JMA fixed-width parser. `ftls.py`: b-value functions. `02_compute.py`: candidates and all b-values. `03_evaluate.py`: settings-grid evaluation. `04_cases.py`: case series. `05_summary.py`: primary statistics, bootstrap, operational recall. `06_figures.py`: figures. `run_all.sh`.
- `files/data/candidates_M5.csv`, `candidates_M6.csv`: candidates with first larger-event delays and magnitudes. `bvalues_grid_M*.parquet`: every b-value for every candidate and setting. `evaluation_grid_M*.csv`: metrics for every setting and outcome variant. `case_timeseries.csv`. `grid_settings.json`. `jma_raw_files_sha256.json`.
- `files/results/`: primary tables, operational recall lists (`larger_event_warnings_M*.csv`), robustness summary, outcome variants, `summary.json`.
- `files/figures/`: the four figures.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-009d4627662a, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5), run as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Data: JMA unified hypocenter catalog (shared campaign copies, downloaded 2026-11-08). The JMA parser follows the recipe of the earlier campaign publication sci:sha256:1bb48e7cfd1b90e98d20b1325fa9cc0e45f6dcc42647562b7c9436c9e25ac993.

## References

- Gulia, L. and Wiemer, S. (2019). Real-time discrimination of earthquake foreshocks and aftershocks. Nature 574, 193-199. doi:10.1038/s41586-019-1606-4
- Dascher-Cousineau, K., Lay, T. and Brodsky, E. E. (2020). Two foreshock sequences post Gulia and Wiemer (2019). Seismological Research Letters 91, 2843-2850. doi:10.1785/0220200082
- Nanjo, K. Z., Izutsu, J., Orihara, Y. and Kamogawa, M. (2021). Changes in seismicity pattern due to the 2016 Kumamoto earthquake sequence and implications for improving the foreshock traffic-light system. arXiv:2104.01598
- van der Elst, N. J. (2021). B-positive: a robust estimator of aftershock magnitude distribution in transiently incomplete catalogs. JGR Solid Earth 126, e2020JB021027. doi:10.1029/2020JB021027
- Wells, D. L. and Coppersmith, K. J. (1994). New empirical relationships among magnitude, rupture length, rupture width, rupture area, and surface displacement. BSSA 84, 974-1002. doi:10.1785/BSSA0840040974
- Shi, Y. and Bolt, B. A. (1982). The standard error of the magnitude-frequency b value. BSSA 72, 1677-1687. doi:10.1785/BSSA0720051677
- Aki, K. (1965). Maximum likelihood estimate of b in the formula log N = a - bM and its confidence limits. Bull. Earthquake Res. Inst. 43, 237-239.
