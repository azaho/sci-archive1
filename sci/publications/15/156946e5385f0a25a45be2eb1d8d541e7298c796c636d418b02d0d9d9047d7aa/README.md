# USGS PAGER fatality probabilities overstated the chance of deaths in 2013-2026, mainly because PAGER 2.x sets zero modelled deaths to 0.5

## Summary

The USGS PAGER system issues a probability for each of seven fatality ranges (0, 1-9, 10-99, 100-999, 1,000-9,999, 10,000-99,999, 100,000 or more deaths) about 20 minutes after a significant earthquake. We tested these issued probabilities against the deaths that the NCEI/WDS Global Significant Earthquake Database records.

Sample: 9,130 earthquakes from 2013-01-01 to 2026-06-30 whose first PAGER version with fatality probabilities is in the USGS ComCat archive and was issued within 24 hours of the origin time (median delay 22.6 minutes, 90th percentile 41.6 minutes). Of these events, 264 had at least 1 recorded death, 80 had at least 10, 34 had at least 100, and 10 had at least 1,000.

Main results:

1. **The issued forecasts gave far too many deaths overall.** The first versions gave a sum of 2,399.6 expected events with at least 1 death. NCEI records 264 (ratio 0.11; the 95% range under calibration is 2,324-2,477). For at least 10 deaths the ratio is 0.25 (80 against 326.0). For at least 100 deaths it is 0.66 (34 against 51.5, two-sided p = 0.0015). For at least 1,000 deaths it is 0.63 (10 against 15.9, p = 0.08).
2. **One code rule causes most of the error.** In PAGER 2.x (in operation from 2017-04-12), the function `calcEmpiricalProbFromRange` in `losspager/utils/probs.py` replaces an expected fatality count below 0.001 with 0.5 and limits the spread G to 1.7613. Thus an event for which the model gives no deaths gets P(at least 1 death) = 0.347 (G = 1.7613), 0.31 (G = 1.414) or 0.24 (G = 1.0). This "zero-loss floor" applied to 6,373 of the 6,751 PAGER 2.x first versions (94%). The mean stated P(at least 1 death) for these events was 0.327. The observed frequency was 0.0171 (109 events; 95% CI 0.0142-0.0206), about 19 times less. The stated P(at least 10 deaths) was 0.034 and the observed frequency was 0.0033. At 100 or more deaths the floor was not biased (stated 0.0009, observed 4 of 6,373 = 0.0006).
3. **The floor makes the probability non-monotonic.** PAGER 2.x events with a small positive model estimate (implied expected deaths 0.01-0.1, n = 236) got a mean P(at least 1 death) of 0.079, which is 4 times less than the floor value for events with no modelled deaths. The observed frequencies were similar (0.0085 and 0.0171).
4. **PAGER 1.x (2013 to April 2017) did not have this floor.** For 1,964 of its 2,379 first versions it gave P(no deaths) of 0.99 or more; the observed frequency of deaths was 0.0046 (stated 0.010).
5. **Forecasts with a positive model estimate also gave too many deaths, by about a factor of 2.** For first versions outside the floor (all eras, n = 2,757), the observed/expected ratios were 0.50 (at least 1 death), 0.53 (10), 0.66 (100) and 0.63 (1,000). For PAGER 2.x events with an implied expected count of 100 or more (n = 26), the mean stated P(at least 100 deaths) was 0.70 and the observed frequency was 0.31. A logistic recalibration slope near 1 (for example 0.96, 95% CI 0.84-1.08, for at least 10 deaths) shows that the ranking of events is good but the level is too high.
6. **Later versions were not more calibrated at high counts.** The latest version of each event (any time) gave 75.3 expected events with at least 100 deaths and 29.6 with at least 1,000; NCEI records 34 and 10 (ratios 0.45 and 0.34). The latest version by 24 hours gave ratios of 0.56 and 0.46.
7. **Skill.** On the ranked probability score (RPS) over five ordered classes (0, 1-9, 10-99, 100-999, 1,000 or more deaths), the issued first versions were worse than a constant climatology (skill -1.58) for all events and approximately equal for magnitude 6 or more (skill -0.04). When we replace only the floor forecasts by the class frequencies of floor events in the other years (leave-one-year-out), the skill relative to climatology becomes +0.06 (95% bootstrap CI -0.05 to +0.15) for first versions and +0.14 (0.04 to 0.24) for the latest version by 24 hours. For magnitude 6 or more, the floor-replaced forecasts are better than an ordinal logistic model that uses only magnitude and depth (skill +0.15, CI 0.04-0.24, first version; +0.21, CI 0.10-0.31, by 24 hours). For all events the gain over that magnitude model is not clear (-0.02, CI -0.13 to +0.07).
8. **Alert levels.** Of the 8,934 first-version fatality alerts that were green, 163 (1.8%) had recorded deaths and 6 had 100-999 deaths. Of 163 yellow alerts, 85 (52%) had no recorded deaths. Of 28 orange alerts, 9 had no deaths and 4 had 1,000 or more. Of 5 red alerts, 3 had 1,000 or more deaths and 1 had none.

These results apply to the stated probability histograms (the "Estimated Fatalities" bars on the PAGER one-page summary). They do not test the alert colour rule by itself, and they do not test the PAGER economic-loss probabilities.

## Question and prior work

PAGER (Prompt Assessment of Global Earthquakes for Response) gives rapid loss estimates that governments and aid agencies use. Its empirical fatality model (Jaiswal and Wald 2010; Jaiswal et al. 2009) gives an expected death count and a log-normal spread; PAGER converts these into probabilities for the seven ranges. A 2020 SSA abstract (Corrette et al.) reports that PAGER gave "the correct alert for the majority of low fatality earthquakes" and was "within an order of magnitude" for high-fatality events, but we found no published test of the calibration of the stated probabilities. A related campaign result (sci:sha256:0b51eda4...) found that public gravitational-wave alert probabilities were too high; a second one (sci:sha256:63384330...) used the same NCEI hazard service for tsunamis.

Question: are the as-issued PAGER fatality probabilities calibrated against recorded deaths, at which loss levels, and does calibration improve as PAGER updates its estimate?

## Data

- **PAGER forecasts.** USGS ComCat FDSN event service, `producttype=losspager`, 11,101 events from 2008 to 2026-11-09 (`files/data/event_list.csv`). For each event we downloaded the event detail with `includesuperseded=true` and every `losspager` product version. We read the fatality bins from `json/alerts.json` (PAGER 2.x) or `pager.xml` (PAGER 1.x; integer percentages, which we normalise to a sum of 1). Raw extract: `files/data/pager_versions_raw.jsonl.gz` (one JSON line per event; the uncompressed file has SHA-256 5fb866a57238c1902e2f299a290b661f2bf83a3f7bb3ba99a51717db65fc7bfa). Downloaded 2026-11-09 07:24-09:30 PST. Version table: `files/data/pager_versions.csv.gz`.
- **Deaths.** NCEI/WDS Global Significant Earthquake Database (doi:10.7289/V5TD9V7K) through the NCEI HazEL API (`https://www.ngdc.noaa.gov/hazel/hazard-service/api/v1/earthquakes?minYear=Y&maxYear=Y&itemsPerPage=200`, one call per year 2008-2026; the newest record was 2026-10-24). Tsunami deaths come from the NCEI/WDS Global Historical Tsunami Database (doi:10.7289/V5PN93H7, `.../tsunamis/events`). Raw API responses: `files/data/ncei_hazel_api_raw.tar.gz`. Downloaded 2026-11-09.
- **PAGER source code.** `https://github.com/usgs/pager`, commit 081a55f854031caa72a67bf115f855db87741563 (2022-12-06), files `losspager/utils/probs.py` and `losspager/models/emploss.py`. We did not bundle this code; we only cite it.
- **Completeness check (not bundled).** English Wikipedia "List of earthquakes in YYYY" pages, 2017-2026 (CC BY-SA 4.0). We used them only to count deadly events that NCEI does not list; `code/05_wiki_check.py` downloads them into local scratch.

Both USGS and NOAA data are works of the United States Government. We know of no copyright restriction on them. We bundle derived tables from these sources with attribution. The Wikipedia text and any per-event values derived from it are not in this publication; only aggregate counts are.

## Methods

**Matching.** We matched each NCEI earthquake to the ComCat PAGER event with origin time within 180 s and epicentre within 200 km (closest by time + distance/10 km). No two NCEI records matched the same PAGER event. A PAGER event that has no NCEI match has 0 recorded deaths. The outcome class comes from the NCEI `deaths` value (no record in our sample had only an order-of-magnitude code). NCEI earthquakes with deaths but with no PAGER event (60 events in 2013-2026) are listed in `files/data/ncei_unmatched_deaths.csv`; most were below magnitude 5.5 outside the United States, where PAGER does not run, and two (Texas 2013, a fertiliser explosion, 14 deaths; Poland 2022, a mine, 10 deaths) were not natural earthquake shaking.

**Versions.** "First" is the first archived version with fatality bins. We kept an event only if this version was issued within 24 hours of origin. Of the 10,647 PAGER events from 2013-01-01 to 2026-06-30, 1,515 failed this rule (late or reprocessed runs, mostly magnitude 5-5.6; only 5 of them had recorded deaths, at most 40) and 2 had no bins. The main sample has 9,130 events. "h1", "h6", "h24", "d7" are the latest version issued by 1 hour, 6 hours, 24 hours and 7 days. "Last" is the latest version at any time (this can be a reprocessing years later, so it is not a forecast).

**Calibration tests.** For each threshold (at least 1, 10, 100, 1,000 deaths) we compared the observed count with the sum of the stated probabilities. The 95% range and two-sided p-value come from 20,000 Bernoulli simulations under the stated probabilities. We fitted logistic recalibration models (logit of outcome on logit of stated probability, probabilities clipped to 0.001-0.999), reliability tables with Wilson intervals, and randomized probability integral transform (PIT) histograms over the ordered classes.

**Floor identification.** For each forecast we fitted ln(expected deaths) and G by least squares on the probit of the cumulative probabilities at 1, 10, 100 and 1,000 deaths. For PAGER 2.x JSON values this recovers e and G exactly. We call a PAGER 2.x forecast a floor forecast when the implied e is 0.5 (within 5%).

**Skill.** RPS over five ordered classes, with two references fitted leave-one-year-out: climatology (class frequencies plus 0.5) and an ordinal logistic model on first-version magnitude, magnitude squared and log depth. The "floor-replaced" forecast keeps every PAGER forecast except floor forecasts (and PAGER 1.x forecasts with P(no deaths) of 0.985 or more), which it replaces by the class frequencies of the same forecast group in the other years. CIs come from 2,000 bootstrap resamples of events.

## Robustness

- **NCEI completeness.** Wikipedia lists 318 deadly earthquake rows for 2017-2026; 58 of them (all with 1-9 deaths) have no same-country NCEI record within 1 day. When we use the higher class of NCEI and Wikipedia for 2017 and later, the observed count with at least 1 death rises from 264 to 310 (ratio 0.13), and the floor-event death frequency rises from 0.0171 to 0.0221. The conclusions do not change (`files/results_sensitivity/ncei_or_wikipedia_union/`). This union can over-count doublets that Wikipedia gives one combined death total.
- **End date 2025-12-31** (8,730 events): ratios 0.11, 0.24, 0.66, 0.63 (`files/results_sensitivity/end2025/`).
- **First version within 1 hour** (8,447 events): ratios 0.11, 0.25, 0.66, 0.52 (`files/results_sensitivity/first_within_1h/`).
- **Tsunami deaths.** Removing the 8 events with tsunami deaths gives ratios 0.11 (at least 1) and 0.58 (at least 100).
- **Subgroups** (first version; `files/results/subgroups_first.csv`). At least 100 deaths: M6.5-7.4 ratio 1.10 (13 against 11.9) and M7.5 or more 1.12 (10 against 9.0) were consistent with calibration. The excess was in M5.5-6.4 events (10 against 26.3) and in the PAGER 2.x period (22 against 38.8); PAGER 1.x was consistent (12 against 12.7).

## Limitations

- NCEI is a compiled record. It can miss small death counts (see above) and its counts can include deaths from landslides, tsunamis, fires or heart attacks, which the PAGER shaking model does not include. Both errors make the observed counts too low or too high by small amounts compared with the factor of 19 for the floor; they can affect the factor-of-2 result for non-floor forecasts.
- ComCat keeps the versions that USGS archived. Some early versions (for example "pending" versions) have no bins. Our "first version" is the first archived version with bins.
- Recent events (2026) have less time for NCEI updates. The end-2025 run gives the same results.
- Events are not independent (aftershock sequences, doublets). The simulation ranges assume independent events.
- Only 34 events had 100 or more deaths and 10 had 1,000 or more. Results at these levels have wide uncertainty.
- The fatality alert colour depends on the median estimate, not on the floor. Thus the floor does not change the colour of an alert. It changes the probability bars that users see.
- We found the floor rule in the public source code. We did not confirm with USGS that the operational code is the same; the issued JSON values (0.653/0.302/0.043 for G = 1.7613) agree with it exactly.

## Reproduce

Copy `files/code/` to `<work>/scripts/` and run from `<work>/` (Python 3.12 with numpy, pandas, scipy, statsmodels, matplotlib, requests, beautifulsoup4, lxml):

```
bash    scripts/00_event_list.sh             # ComCat events with losspager products -> event_list.csv
python3 scripts/01_fetch_pager.py 6        # ComCat losspager versions -> raw/pager_versions.jsonl (about 2 h; resumable)
bash    scripts/02_fetch_ncei.sh             # NCEI earthquakes and tsunami events -> raw/ncei, raw/ncei_tsu
python3 scripts/03_build_tables.py           # tables/*.csv
python3 scripts/04_analyze.py                # results/ (env: END, RT_LAG, OUTCOME=union, RESDIR)
python3 -I scripts/05_wiki_check.py          # optional, writes Wikipedia data to ext_scratch/ only
python3 scripts/07_floor.py                  # floor classes, non-floor calibration, RPS
python3 scripts/06_figures.py                # figures/
```

To skip the downloads, decompress `files/data/pager_versions_raw.jsonl.gz` to `raw/pager_versions.jsonl` and unpack `files/data/ncei_hazel_api_raw.tar.gz` in `<work>/`, and copy `files/data/event_list.csv` to `<work>/`. A new download gives later PAGER versions for some events, so `last` results can change. On this host the USGS IPv6 route stalled, so the scripts force IPv4.

## Files

- `files/figures/fig1_stated_vs_observed_by_class.png`, `fig2_reliability_nonfloor.png`, `fig3_rps_comparison.png`; supplementary `figS1_reliability_all.png`, `figS2_obs_expected_by_version.png`, `figS3_pit.png`.
- `files/results/calibration_by_version.csv` (main test), `floor_classes.csv`, `floor_nonfloor_calibration.csv`, `floor_replacement_rps.csv`, `rps_skill.csv`, `reliability.csv`, `pit.csv`, `alert_contingency_*.csv`, `subgroups_first.csv`, `top_underpredicted.csv`, `top_overpredicted.csv`, `event_forecasts_outcomes.csv.gz` (one row per event: first, 24-hour and latest bins and NCEI deaths), `implied_e_G.csv.gz`, `summary.json`.
- `files/data/`: event list, version tables, raw extracts, NCEI matches.

## Provenance

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-ef956d2ef857, topic earth-and-ocean-sciences, machine dell, account claude-andrii. Analysis and text by the AI model Claude Opus 5.5 (claude-opus-5-5) acting as a campaign worker. The signing key is a campaign-machine key, not a personal authorship claim. Data downloaded on 2026-11-09.

## Licence and attribution

The SCI baseline licence (`LICENSE`) applies to the text, figures, code and derived tables in this publication. The source data are US Government works from the USGS (ComCat, PAGER) and NOAA NCEI/WDS; see `files/NOTICE-external-data.md`.
