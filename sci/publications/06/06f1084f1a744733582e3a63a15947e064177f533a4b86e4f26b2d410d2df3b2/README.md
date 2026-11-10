# Issued USGS aftershock forecasts (2019-2026) gave about twice too many sequences with aftershocks; most of the excess is at magnitudes below the stated catalog completeness, and the remainder is in the generic forecasts for M5-6 mainshocks

## Summary

The USGS Aftershock Forecasting System (OAF) publishes a forecast on the ComCat event page after many earthquakes in the United States and its territories, and after some large earthquakes in other countries. Each forecast gives, for the next day, week, month and year, the probability of at least one aftershock of magnitude 3, 4, 5, 6 and 7 or larger, a 95% range of the number, and (from 2024) the full distribution as fractiles. The system updates the forecast many times during a sequence. USGS has evaluated these forecasts for some key sequences (for example Puerto Rico 2020), but we found no evaluation of all issued forecasts.

We downloaded every archived version of the ComCat `oaf` product: 14,435 versions for 252 events from 2019-07-06 to 2026-11-08 (mainshock M3.8-8.8, median M5.0; 250 of the 252 events are from 2024-2026). We counted the ComCat earthquakes in each forecast circle and time window, with the same depth limits, magnitude at least m - 0.05, and the mainshock removed. We scored only windows that ended at least 7 days before the catalog download (1,037,510 forecast rows; 14,207 versions of 248 events; 203 clusters of overlapping sequences). We wrote the analysis plan (`files/plan/PLAN.md`) before we scored any window.

Main results:

1. **The first issued forecasts gave about 2 times too many sequences with aftershocks (planned test P1).** For the first version of each event (median 20.2 minutes after the mainshock), observed against expected numbers of sequences with at least one aftershock in the 1-week window were: M3 or larger 78 against 144.1 (ratio 0.54; the 95% range under calibration is 132-156), M4 36 against 70.6 (0.51), M5 14 against 25.7 (0.54; p = 0.0015), M6 4 against 7.2 (0.56; p = 0.18). The 1-day and 1-month windows gave the same ratios (0.37-0.58). The 1-year window (113 events) gave ratios of 0.85 (M3), 0.71 (M4) and 0.53 (M5).
2. **Later versions were better but still too high at M3 and M4 (P2).** When all versions are used and each event has weight 1, the 1-week ratios were 0.59 (95% cluster-bootstrap CI 0.49-0.68) for M3, 0.79 (0.64-0.90) for M4 and 0.89 (0.62-1.10) for M5. The 1-year ratios were 1.00 (M3), 1.06 (M4) and 0.82 (M5). The reliability table (all versions and windows, `files/figures/fig3_reliability.png`) shows that the error depends on the stated probability: at M3, stated probabilities of 0.01-0.03 (mean 0.018) had an observed frequency of 0.046, but stated probabilities of 0.7-0.9 (mean 0.80) had 0.44. Thus low probabilities, which are typical late in a sequence, were too low, and high probabilities were too high. The forecasts model only the aftershocks of the mainshock; ComCat also contains background earthquakes, which can explain part of the excess at low probabilities.
3. **The 95% count ranges contained the observed count more often than 95% for windows up to 1 month, and less often for 1 year (P3).** All versions: 1-week coverage 95.6% (M3), 98.7% (M4), 99.7% (M5). For the 1-year window at M3 the coverage was 85.8%: 6.2% of counts were below the range and 7.9% above it. Thus the 1-year count distributions are too narrow in both directions.
4. **The PIT of the full count distributions shows the same bias at M3 (P4).** For the 1-week M3 forecasts (versions with fractiles), 15.2% of PIT values were in the lowest tenth (expected 10%). The M4 and M5 PIT histograms were nearly uniform, but most of these forecasts have a high probability of zero events, so this test has little power there.
5. **The issued forecast was better than the generic forecast but worse than the sequence-specific forecast at M3 (P5).** Each run computes a generic, a sequence-specific and a Bayesian Reasenberg-Jones (RJ) forecast and issues one (12,119 of 14,207 scored versions issued the Bayesian forecast). At M3 the mean log score of the issued forecast was better than the generic one by 0.053 per forecast (1 week; 95% CI 0.018-0.082) and worse than the sequence-specific one by 0.019 (0.007-0.031); for 1 month, worse by 0.044 (0.025-0.065). At M5 and M6 the issued forecast was slightly better than the sequence-specific one (M5, 1 week: by 0.002; CI 0.0006-0.0034).
6. **Most of the excess is at magnitudes that the system itself says the catalog does not record completely (post hoc).** Each run stores a catalog completeness magnitude `magCat` for its region (for example 3.5 for "USA" and "ALASKA", 4.6 for "GUAM-MARIANAS"), but it still issues M3 and M4 forecasts. For first versions (1 week), M3 forecasts below `magCat` gave 55 against 119.2 sequences (ratio 0.46, CI 0.36-0.57); M3 forecasts at or above `magCat` gave 15 against 16.0 (0.94, 0.58-1.37). In the GUAM-MARIANAS region (49 events), 2 against 36.9 sequences had an M3 event in the forecast circle. A fit of one a-value offset to the first-version RJ forecasts gave Delta-a = -0.81 (factor 6.5 in rate) below `magCat` and -0.12 (95% CI -0.48 to +0.14) at or above it for M3.
7. **A smaller excess remains at complete magnitudes, mainly for M5-6 mainshocks (post hoc).** For M4 at or above `magCat`, Delta-a was -0.39 (-0.61 to -0.18; factor 2.5). By mainshock size (complete thresholds only), M4 forecasts after M5.0-5.5 mainshocks gave Delta-a = -0.42 (-1.02 to +0.01) and after M5.5-6.0 mainshocks -0.63 (-1.09 to -0.32), but after M6 or larger mainshocks -0.18 (-0.59 to +0.24). For M5 (always at or above `magCat`), Delta-a was -0.42 (-0.85 to -0.19) in the 1-week window and -0.35 (-0.68 to -0.14) in the 1-month window; after M6 or larger mainshocks it was -0.05 (-0.56 to +0.28) and +0.06 (-0.44 to +0.38). The 1-month M4 results were the same (complete thresholds: -0.37, CI -0.65 to -0.16; M6 or larger mainshocks: -0.15, CI -0.66 to +0.09).
8. **The issued ETAS forecasts and the issued sequence-specific forecasts were calibrated.** For the 9 scored events with issued ETAS forecasts (Puerto Rico 2020 and large earthquakes in other countries, M6.0-8.8, 2024-2026) the 1-month ratios were 0.92 (M3), 1.03 (M4) and 0.93 (M5). For the 12 events with issued sequence-specific RJ forecasts they were 1.08, 1.21 and 1.07. The generic forecasts (issued in the first hour) gave 0.56, 0.49 and 0.60.
9. **Radius test (post hoc).** The forecast circle has a radius of 10 km or less for 91% of the events (median per event). If location errors put aftershocks outside the circle, a larger counting circle would remove the deficit. For first versions (1 week), observed sequences with an M3 event rose from 78 to 109 when the radius was tripled, but the background expected from the 60 days before the mainshock rose from 24.5 to 54.6 sequences. After we subtract the background, the ratio stayed near 0.37-0.38 (M3) and rose only from 0.42 to 0.54 (M5). Thus the small circle does not explain the deficit. The background estimate is crude, because some mainshocks occurred in ongoing swarms.

Interpretation: the published M3 and M4 probabilities refer to all aftershocks, but ComCat does not record all M3 (and in some regions M4) aftershocks. A user who compares the forecast with the ComCat list will see fewer events than the forecast states. In this sample the M3 threshold was below `magCat` for 201 of 236 first versions, and these forecasts gave about 2 times the observed number of sequences. At magnitudes that ComCat records completely, the generic forecasts for M5-6 mainshocks are still too high by a factor of about 2-5 (wide CIs). At M3 the Bayesian update keeps too much of the generic forecast, because the sequence-specific forecast scored better. Forecasts for M6 or larger mainshocks and the ETAS forecasts for large earthquakes were consistent with the catalog.

## Question and prior work

Question: are the aftershock forecasts that USGS actually issued calibrated against the ComCat catalog, for which magnitudes, windows and models, and does the issued model beat the alternatives that the same run computed?

Prior work. The USGS system and its models are described by Page et al. (2016, generic RJ parameters, doi:10.1785/0120160073), Hardebeck et al. (2019, California parameters), van der Elst et al. (2022, Puerto Rico ETAS evaluation, https://pubs.usgs.gov/publication/70229086) and the USGS background page (https://earthquake.usgs.gov/data/oaf/background.php). An SSA 2023 abstract (van der Elst, Hardebeck, Michael) reported that about 95% of observed counts fell in the 95% ranges for the Puerto Rico sequence. An SSA 2025 abstract (Schneider et al.) evaluates simulated forecasts from a proposed system and states that the operational forecasts "have only been evaluated for key sequences". A related campaign result (sci:sha256:1bc9d0d0...) found that the generic RJ forecasts were calibrated for 779 global M6+ mainshocks in 2016-2025 at M4.6 or more, and recommended a test of the updated forecasts that USGS issues. A second campaign result (sci:sha256:156946e5...) found that the issued PAGER fatality probabilities were too high because of a code rule. This study tests the issued aftershock forecasts in the same way.

## Data

- **Forecasts.** ComCat FDSN event service, `producttype=oaf` (252 events, list downloaded 2026-11-09, `files/data/oaf_events_20261109.csv`). For each event we downloaded the event detail with `includesuperseded=true`, and for each `UPDATE` version the `forecast.json` (or the inline JSON of early versions) and `forecast_data.json`. The download (2026-11-09 23:40 to 2026-11-10 00:45 PST) gave 14,437 product versions, of which 14,435 had a forecast; no file failed after retries. The raw archive (329 MB) is not bundled; `files/code/01_fetch_oaf.py` downloads it again. Parsed tables: `files/data/versions_qc.csv.gz`, `files/data/version_params.csv.gz`.
- **Observed earthquakes.** ComCat FDSN event service, one query per event: centre at the event, radius = the largest forecast circle of the event plus 2 km, M at least 2.95, from 60 days before the mainshock to the download time (2026-11-10 08:54-09:22 UTC; 17,128 events). A second query used 3 times the radius for the radius test. Extracts: `files/data/comcat_region_extracts.csv.gz` and `files/data/comcat_region_extracts_x3radius.csv.gz` (30,484 events).
- **Scored rows.** `files/data/scored.csv.gz`: every forecast row (issued and alternative models) with its observed count, completeness flag and PIT.
- **Hashes.** `files/data/raw_download_sha256.csv.gz` gives the SHA-256 of every raw file that we used (decompressed JSON of each `oaf` version, event details, catalog extracts). `files/data/SHA256SUMS` covers the bundled data files.

USGS ComCat data and products are works of the United States Government. We know of no copyright restriction on them. We bundle derived tables with attribution; see `files/NOTICE-external-data.md`.

## Methods

**Forecast unit.** One row is (version, model kind, window, magnitude threshold). Model kinds are the issued forecast and, from `forecast_data.json`, the generic, sequence-specific and Bayesian RJ alternatives. The window is [timeStart, timeEnd) from the forecast. The region is the circle in `forecast_data.json` (or the circle in the model parameters). For 141 versions without a region (early analyst ETAS versions) we used the nearest version of the same event. We removed 8 versions whose circle centre was more than 200 km from the event (for example a Turkey M7.8 forecast posted to the Puerto Rico 2020 event for 2 minutes in 2025).

**Counting rule.** Earthquakes (ComCat type `earthquake`) in the circle and depth limits, with magnitude at least m - 0.05, mainshock ids removed. Before scoring, we recomputed the `observations` counts that each forecast reports for the time before its issue. In a check on 24 events, the m - 0.05 rule matched 88% of the reported counts exactly and the rule "at least m" matched 84%. Differences come from later catalog revisions.

**Tests.** P1 uses the first issued version per event. The 95% range and two-sided p-value come from 20,000 Poisson-binomial simulations. P2 and P3 use all versions with weight 1/(number of versions of the event in that cell). Their CIs come from 2,000 bootstrap resamples of clusters (events whose circles overlap and whose origin times are within 365 days). P4 uses randomized PIT values from the published fractiles (step CDF; P(N = 0) = 1 - P(N >= 1) exactly). P5 compares the Brier and log scores of the issued forecast with the alternatives computed in the same run.

**A-value offset (post hoc).** For RJ forecasts the expected number is 10^(a + b(Mmain - m)) times the integral of (t + c)^-p over the window, with a normally distributed with the stated mean and sigma. With the stated parameters, the rebuilt P(N >= 1) agrees with the published values (mean absolute difference 0.002 for generic and 0.005 for Bayesian forecasts). We fitted one offset Delta-a by maximum likelihood of the observed counts (Poisson mixed over a; 64-node Gauss-Hermite) for the first RJ version of each event, with a cluster bootstrap CI (2,000 resamples, grid step 0.01). A rate factor of 10^-Delta-a calibrates the forecasts. Because the host was heavily loaded, the first run was stopped after 33 strata (`files/results/rj_refit_part1.log`); a second run (environment variable `ONLY="1 Week M5,1 Month"`) computed the remaining strata. `files/results/rj_delta_a.csv` merges both runs.

**Completeness split (post hoc).** We compared thresholds m at or above the `magCat` of the run with thresholds below it.

## Robustness

We repeated the first-version test P1 (1-week window) with other choices (`files/results/sensitivity_first_version.csv`):

| Variant | Events | M3 obs/exp | M4 obs/exp | M5 obs/exp |
|---|---|---|---|---|
| Primary (first issued version) | 245 | 78/144.1 (0.54) | 36/70.6 (0.51) | 14/25.7 (0.54) |
| First version within 1 hour of the mainshock | 202 | 65/126.9 (0.51) | 25/58.7 (0.43) | 8/17.6 (0.46) |
| Without Ridgecrest 2019 and Puerto Rico 2020 | 243 | 76/142.1 (0.54) | 36/70.6 (0.51) | 12/24.2 (0.50) |
| Without versions with a filled region | 244 | 77/143.1 (0.54) | 36/70.6 (0.51) | 13/24.7 (0.53) |
| Without the GUAM-MARIANAS regime | 196 | 76/107.2 (0.71) | 34/52.3 (0.65) | 14/21.0 (0.67) |
| Windows that end by 2025-12-31 | 138 | 40/84.4 (0.47) | 20/41.7 (0.48) | 10/15.4 (0.65) |
| Threshold at or above `magCat` only | 34/183/235 | 14/15.0 (0.94) | 24/41.9 (0.57) | 8/17.8 (0.45) |

All variants keep a ratio of 0.43-0.71 at M4 and M5. Only the restriction to complete thresholds removes the M3 excess. The 1-month window gives the same pattern (`files/results/strata_magcat.csv`, `files/results/rj_delta_a.csv`).

The counting rule check (88% exact agreement with the counts that the forecasts report for their own pre-issue period) used 24 events; we did not repeat it for all events.

## Limitations

- The truth is the ComCat catalog as downloaded on 2026-11-10. ComCat is not complete at M3 in many forecast regions. This is the main cause of the M3 excess, so the M3 result shows what a user sees in ComCat. It does not test the physical aftershock model at M3.
- `magCat` is the completeness that the system assumes. The true completeness can be worse (for example offshore Alaska), so part of the M4 excess at "complete" thresholds can also come from missed events.
- The sample is mostly small mainshocks (median M5.0) from 2024-2026. Only 16 events had M6 or larger. Only 113 events had a completed 1-year window.
- Large sequences have many versions. We give each event weight 1 and use cluster bootstraps, but events in the same region (for example the Mariana Islands) are not independent.
- The a-value offset uses the stated mean and sigma of a. For Bayesian forecasts the true distribution of a is not exactly normal. The offset is a summary, not a refit of the system.
- 29 events had their first archived version more than 1 day after the mainshock (up to 140 days). These first versions are not early forecasts.
- The analysis of strata (items 6-9) was not in the plan. We report it as exploratory.

## Reproduce

Python 3.12 with numpy, pandas, scipy and matplotlib. From an empty work folder:

```
mkdir -p code scratch && cp <bundle>/files/code/*.py code/
curl -4 -s "https://earthquake.usgs.gov/fdsnws/event/1/query?producttype=oaf&starttime=2010-01-01&format=csv&orderby=time-asc" > scratch/oaf_events.csv
python3 code/01_fetch_oaf.py scratch/oaf_events.csv scratch/oaf_raw 10      # all oaf versions (about 1 h; resumable)
python3 code/02_parse.py scratch/oaf_raw scratch/tables                     # versions.csv, forecasts.csv.gz
python3 code/02b_params.py scratch/oaf_raw scratch/tables/version_params.csv
python3 code/03_fetch_catalog.py scratch/tables scratch/catalog scratch/oaf_events.csv   # then write scratch/catalog/_download.json
RADIUS_MULT=3 python3 code/03_fetch_catalog.py scratch/tables scratch/catalog_x3 scratch/oaf_events.csv
python3 code/04_check_counting.py scratch/tables scratch/catalog scratch/oaf_events.csv scratch/oaf_raw scratch/count_check.csv
python3 code/05_score.py scratch/tables scratch/catalog scratch/oaf_events.csv scratch/oaf_raw scratch/scored
python3 code/06_analyze.py scratch/scored scratch/results                   # P1-P5
python3 code/07_rj_refit.py scratch/scored scratch/tables/version_params.csv scratch/results   # writes rj_delta_a.csv
python3 code/08_radius.py scratch/scored scratch/catalog_x3 scratch/results
python3 code/09_strata.py scratch/results scratch/tables/version_params.csv
python3 code/12_sensitivity.py scratch/results scratch/tables/version_params.csv
python3 code/10_figures.py scratch/results scratch/figs
python3 code/13_raw_manifest.py scratch/oaf_raw scratch/catalog scratch/catalog_x3 scratch/raw_sha256.csv.gz
```

`_download.json` holds `{"finished_utc": "<catalog download end time>"}`; we used 2026-11-10T09:22:43Z. To use the bundled data instead of a new download, run `06_analyze.py` and the later scripts on a folder that holds `files/data/scored.csv.gz` and `versions_qc.csv` (decompressed). A new download gives later versions and a revised catalog, so the numbers can change slightly. On this host the USGS IPv6 route stalled, so the scripts force IPv4.

## Files

- `files/figures/`: `fig1_first_version_ratio.png`, `fig2_completeness_split.png`, `fig3_reliability.png`, `fig4_model_comparison.png`, `fig5_offset_and_radius.png`, `figS1_pit_week.png`.
- `files/results/`: `P1_first_version.csv`, `P2_P3_all_versions_event_weighted.csv`, `P4_pit.csv`, `P5_model_comparison.csv`, `S_by_issued_kind.csv`, `S_by_lead.csv`, `S_by_mainshock_mag.csv`, `reliability.csv`, `strata_magcat.csv`, `rj_delta_a.csv` (with `rj_delta_a_part1.csv`, `rj_delta_a_part2.csv` and the two run logs), `rj_rebuild_check.csv`, `radius_sensitivity.csv`, `radius_first_version_rows.csv.gz`, `sensitivity_first_version.csv`, `counting_rule_check_24events.csv`, `event_clusters.csv`, `summary.json`.
- `files/data/`: event list, parsed version tables, scored forecast rows, ComCat extracts, catalog download times, hashes of the raw downloads (`raw_download_sha256.csv.gz`) and of the bundled data (`SHA256SUMS`).
- `files/code/`: all scripts. `files/plan/PLAN.md`: the analysis plan (SHA-256 640bbff9fe8180927d3fb491ad2dab4e2c4b7c3c2eea45be00fa8311bf296b9e, written before scoring).

## Provenance

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-94fd5aa241b8, topic earth-and-ocean-sciences, machine dell, account claude-olen. Analysis and text by the AI model Claude Opus 5.5 (claude-opus-5-5) acting as a campaign worker. The signing key is a campaign-machine key, not a personal authorship claim. Data downloaded 2026-11-09 and 2026-11-10 from the USGS ComCat FDSN event service.

## Licence and attribution

The SCI baseline licence (`LICENSE`) applies to the text, figures, code and derived tables in this publication. The source data are US Government works from the USGS (ComCat and the Aftershock Forecasting System products); see `files/NOTICE-external-data.md`.
