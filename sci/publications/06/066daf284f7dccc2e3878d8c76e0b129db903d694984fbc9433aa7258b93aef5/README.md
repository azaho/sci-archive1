# Spring-timing climate forecasts lost their gain when issued before the events, river-flow forecasts kept 74% at six months, and a lead-specific gate chose correctly in 36 of 40 tests (10 families, 2005-2024)

Job `sci-1107-dell-climate-pollution-biodiversity-38c847e22e95`, campaign 11_07_2026, topic climate-pollution-biodiversity, machine dell, account claude-myxtap, model Claude Opus 5.5 (`claude-opus-5-5`). Date 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign tests found that some climate-response relations keep forecast skill in later years. Examples are spring plant phases, cherry flowering, lake ice dates and river flow. A training-only false-signal gate (FSR_T) chose correctly between a climate model and a trailing mean in new families (sci:sha256:6081bf76). But all these tests used **observed weather up to the end of the reference month**. An audit of the fitted windows (sci:sha256:d71d00b6) found that few timing models had their inputs early. It asked for the decisive test: refit the models under a fixed issue date.

We did this test in ten families from sci:sha256:8804b69f and sci:sha256:6081bf76 (14,313 series, training years to 2004, test years 2005-2024). For each forecast lead h (0, 1, 2, 3 or 6 months before the end of the reference month), only climate windows that are complete at the issue date were allowed. We refitted the window choice, recomputed the gate with both nulls, and also tested a second operational method (keep the lead-0 model and fill the unknown months with climatology). We froze the hypotheses, the threshold and all analysis scripts in a timestamped plan before we computed any result at a lead of 1 month or more. Lead 0 reproduced the published series results exactly in all ten families.

Main results:

1. **At lead 0, most timing "forecasts" were issued after the event.** In the five day-of-year families, 79-96% of test-year events occurred on or before the end of the reference month (Figure 3). At lead 1, 20-33% still did. Only at lead 2 did the issue date come before at least 98.8% of events.
2. **At that event-safe lead, the timing gain was gone.** The median gain of the refitted climate model over the 5-year trailing mean (O3) fell from 0.34 to -0.08 in German spring phases, from 0.49 to -0.06 in Japanese cherry flowering, and from 0.45 to 0.07 in lake and river ice dates (Figure 1). At lead 1, these families kept 78-89% of their lead-0 gain.
3. **River flow kept most of its gain.** Annual US river flow (reference month December) kept 94% of its lead-0 gain at lead 2, 88% at lead 3 and 74% at lead 6 (median O3 0.49 at six months). 92% of river series still beat the trailing mean at lead 6.
4. **The lead-specific gate mostly knew this in advance (H1, H2, H3 passed).** Recomputed from training years at each lead, FSR_T stayed near 0.12-0.14 for rivers and rose above the frozen threshold 0.32 at lead 2 or 3 in the timing families (Figure 2). The gate chose the better of the climate model and the trailing mean in 12 of 16 prospective units of the four open families (H1a, criterion 12) and in 36 of 40 prospective units (H1b, criterion 32). Its pooled score beat the response-class rule by +0.042 (95% interval 0.036 to 0.048) and the static gate that keeps the lead-0 decision by +0.010 (0.004 to 0.015).
5. **The gate did not predict the exact usable lead (H4 failed, 2 of 4 families).** It closed one step too early for lake ice (lead 2, FSR_T 0.346, just above 0.32) and one step too late for cherry flowering (lead 2, FSR_T 0.25). Two of the four wrong units were near ties (difference in unit score 0.03 and 0.001).
6. **Refitting on complete windows beat climatology fill overall (H5: +0.086, 0.074 to 0.104), but not for rivers.** For river flow, the fill method was a little better at every lead (by 0.02-0.04). For cherry flowering, the fill method failed badly at leads 2-6 (median O3 down to -0.88), because the 1951-2004 climatology is too cold for the warmer test years.
7. **Families without a transferable signal stayed without one.** In German late and crop phases, NDVI, crop yields, dengue and river invertebrates, the gate was closed at all leads, and the trailing mean was better at all leads.

![Skill by lead](files/fig1_skill_by_lead.png)

*Figure 1. Median skill against the training mean (1 - MSE/MSE of the 1951-2004 mean) by lead for the 5-year trailing mean (grey), the climate model refitted on windows complete at issue (blue) and the lead-0 model with climatology fill (orange). Bands: 95% cluster-bootstrap intervals. Squares: gate decision from training years only (filled: open, FSR_T(h) <= 0.32).*

## Question

Do climate-response relations that kept forecast skill with observed weather still help when the forecast must be issued before the response, using only weather that is complete at the issue date? And can a training-only false-signal rate, recomputed for each lead, show in advance how much lead each family can bear?

## Design (frozen before any lead >= 1 result)

- Plan: `files/plan/frozen_plan.md`, SHA-256 `6365bafe2c903051161fffb1a47dcf8a7f09f7f56d4efc01401c816d0fe5fcce`. FreeTSA RFC 3161 timestamp 2026-11-11 18:51:05 UTC (`frozen_plan.tsq`, `frozen_plan.tsr`). Verify: download `https://freetsa.org/files/cacert.pem` and `https://freetsa.org/files/tsa.crt`, then `openssl ts -verify -data files/plan/frozen_plan.md -in files/plan/frozen_plan.tsr -CAfile cacert.pem -untrusted tsa.crt`.
- Before the freeze we rebuilt the ten families and ran lead 0 only (reproduction check). The plan appendix lists the lead-0 FSR, FSR_T and O3 values and names the four open families (FSR_T(0) <= 0.32): US river flow, lake and river ice, Japanese cherry, German spring phases.
- The plan lists the SHA-256 of every analysis script. All are unchanged in this bundle. Scripts written after the freeze: `s23_figures.py`, `s24_exploratory.py`, `run_all.sh`.

**Families.** Unchanged builders and series definitions. USR US river flow (652 CAMELS gauges, annual mean flow, USGS), LIC lake and river ice-off and ice-on (183 series, NSIDC LIAG), JPC Japanese cherry first flowering and full bloom (115, JMA), DWS and DWL German wild-plant phases to June and after June (2,510 and 2,127, DWD), DWC German field-crop phases (3,176, DWD), NDV peak-season NDVI (1,500 pixels, PKU GIMMS), FAO national crop yields (516, FAOSTAT), DEN national dengue cases (72, OpenDengue), EMI English river invertebrate families (3,462, EA via UKCEH). US breeding birds were not used (cost; gate closed at lead 0).

**Lead constraint (`p21_lead.py`).** The forecast for target year t is issued at the end of month r - h (r = reference month of the series). The 120 candidate windows (temperature or precipitation, 1, 2, 3, 6 or 12 months) end in one of the 12 months r-h-11 .. r-h, so every candidate is complete at issue and the number of candidates does not change with lead. The engine (`p04_forecast.analyze`) is unchanged: window selection on training years, leave-one-year-out R2_cv with reselection in each fold, frozen slope, level from the 5 most recent observed years (M2_h). R2 is the 5-year trailing mean, R1 the training mean. P_h keeps the lead-0 window and slope and replaces each window month after the issue month by the 1951-2004 mean of that calendar month at the site.

**Gate at each lead (`n21_null_lead.py`).** Circular-shift and trend-preserving nulls with the lead-h candidate set (max(2, ceil(4000/n)) draws per series). FSR_T(h) = share of null R2_cv >= 0.10 divided by the observed share. Gate_T: M2_h for every series of the unit if FSR_T(h) <= 0.32, else R2. Comparison rules: Gate_C (circular null), Gate_T0 (lead-0 decision at every lead), Class (M2_h for abiotic and timing families), Rule_qT (series rule).

**Scores.** Skill = 1 - MSE(strategy)/MSE(reference). Unit score = median over series of skill against R1. Pooled score = mean of unit scores over the 40 prospective units (10 families x leads 1, 2, 3, 6). Intervals: 1,000 cluster-bootstrap draws (stations, gauges, lakes, sites, countries or NDVI tiles resampled within family, the same draw for all leads).

## Results of the pre-registered tests

Full output: `files/results/prereg_tests.json`, `unit_table.csv` (all 50 family-lead units), `unit_medians_ci.csv`.

| Test | Frozen criterion | Result | Decision |
|---|---|---|---|
| H1a gate accuracy, open families | >= 75% of 16 prospective units | 12 of 16 | **Passed** (at the limit) |
| H1b gate accuracy, all families | >= 32 of 40 | 36 of 40 | **Passed** |
| H1 secondary (open families) | reported | Gate_C 11, Gate_T0 10, Class 10 of 16 | - |
| H2a Gate_T minus Class | lower 95% limit > 0 | +0.042 [0.036, 0.048]; 16 disagreeing units | **Passed** |
| H2b Gate_T minus static Gate_T0 | lower 95% limit > 0 | +0.010 [0.004, 0.015]; 8 disagreeing units | **Passed** |
| H2 Gate_T minus Gate_C | reported | +0.003 [0.002, 0.004]; 2 disagreeing units | - |
| H3a FSR_T tracks decay within open families | rho < 0 in >= 3 of 4 | LIC -1.0, DWS -1.0, JPC -0.67, USR +0.40 | **Passed** |
| H3b FSR_T vs median O3, 50 units | rho <= -0.5 | -0.75 (prospective units -0.66) | **Passed** |
| H4 usable-lead horizon | exact agreement in >= 3 of 4 | USR 6/6, DWS 1/1 agree; LIC predicted 1, realized 3; JPC predicted 2, realized 1 | **Failed** |
| H5 refit minus fill (two-sided) | report direction | +0.086 [0.074, 0.104]: refit better | refit better |

Pooled scores over the 40 prospective units (median skill against the training mean): Rule_qT 0.419, Gate_T 0.418, Gate_C 0.415, Gate_T with fill 0.413, static Gate_T0 0.408, Class 0.375, trailing mean for all 0.329, refitted climate model for all 0.320, fill model for all 0.287. USR in H3a: FSR_T barely changed with lead (0.115-0.138) while O3 fell slowly, so the within-family rank correlation is not informative there.

![FSR by lead](files/fig2_fsr_by_lead.png)

*Figure 2. Trend-preserving false-signal rate by lead, from training years only. Filled points: the refitted climate model beat the trailing mean in 2005-2024 (unit score); open points: it did not. Dotted: frozen threshold 0.32.*

### Retained gain (H6, descriptive) and events before issue (H7, descriptive)

| Family | Median O3 at lead 0 | Lead 1 | Lead 2 | Lead 3 | Lead 6 | % events before issue, lead 0 / 1 / 2 |
|---|---|---|---|---|---|---|
| US river flow | 0.65 | 0.64 | 0.61 | 0.58 | 0.49 | (annual mean; not an event) |
| Lake and river ice | 0.45 | 0.35 | 0.07 | -0.06 | -0.12 | 79 / 21 / 0.5 |
| Japanese cherry | 0.49 | 0.43 | -0.06 | -0.05 | 0.01 | 96 / 24 / 0.0 |
| German spring phases | 0.34 | 0.28 | -0.08 | -0.21 | -0.32 | 95 / 33 / 1.2 |
| German late phases | -0.20 | -0.20 | -0.24 | -0.23 | -0.32 | 88 / 20 / 0.3 |
| German crop phases | -0.13 | -0.15 | -0.23 | -0.29 | -0.38 | 92 / 26 / 0.3 |

O3 = skill of the refitted climate model against the 5-year trailing mean. 95% intervals for O3 at lead 2: ice [0.017, 0.149], cherry [-0.128, 0.027], German spring phases [-0.099, -0.060]. The share of series in which the climate model beat the trailing mean fell from 78% to 42% (German spring phases), from 94% to 43% (cherry) and from 96% to 58% (ice) between lead 0 and lead 2 (`e3_series_shares.csv`). In rivers it stayed at 92-98% up to lead 6.

![Events before issue](files/fig4_events_before_issue.png)

*Figure 3. Share of test-year events that occurred on or before the issue date. The reference month is the month of the training-period median date, so lead 0 issues after most events.*

![FSR against O3](files/fig3_fsr_vs_o3.png)

*Figure 4. Lead-specific FSR_T against the median gain O3 for all 50 family-lead units. Lines join the leads of one family.*

## Exploratory results (after the pre-registered results; not decision rules)

Code `files/code/s24_exploratory.py`; output `files/results/exploratory.json`, `e1_tau_sweep.csv`, `e3_series_shares.csv`.

- **E1 threshold.** Over the 40 prospective units the frozen tau 0.32 gave 36 correct decisions. The maximum, 37, occurred for tau 0.36-0.40. Every tau from 0.16 to 0.42 gave 36 or 37. No single tau was right in all units: cherry at lead 2 (FSR_T 0.25, climate model worse) needs tau < 0.25, but German spring phases at lead 1 (FSR_T 0.26, climate model better) needs tau >= 0.26; lake ice at lead 3 (FSR_T 0.83, climate model slightly better) needs tau >= 0.83, but German spring phases at lead 2 (FSR_T 0.44, climate model worse) needs tau < 0.44.
- **E2 event-safe lead.** In all five day-of-year families, lead 2 was the first lead with fewer than 2% of events before issue. There, the refitted climate model beat the trailing mean only for lake ice (unit score 0.27 vs 0.15).
- **E4 near ties.** Of the four wrong gate decisions, two had unit-score differences of 0.03 (lake ice, lead 3) and 0.001 (cherry, lead 6).

## Interpretation

1. A forward test with observed weather up to the reference month measures whether a response relation transfers. It does not measure whether a forecast can be issued. For spring phenology, cherry flowering and ice dates, the reference-month convention of the earlier campaign tests put the issue date after 79-96% of events. When the issue date came before nearly all events, the climate gain over a trailing mean disappeared or became small. These relations are useful as short-lead nowcasts (lead 1, 78-89% of the gain kept, but 20-33% of events already past) and not as season-ahead forecasts with observed weather alone.
2. Integrated annual responses behave differently. Annual river flow depends on precipitation over many months; at lead 6 half of the year is already observed, and the climate model kept 74% of its gain. Here the fill method (lead-0 model with climatology for the unknown months) was slightly better than a refit.
3. The training-only gate can be recomputed for any issue date at no extra data cost. It tracked the loss of signal with lead and beat both the class rule and a gate that ignores lead. It is a coarse tool: it did not locate the usable lead exactly, and decisions near the threshold were wrong in both directions.
4. Practical recipe for a new family: fix the issue date first; restrict the windows to those complete at that date; compute FSR_T on training years; use the climate anomaly with a trailing level only if FSR_T is at most about 0.3, otherwise use a trailing mean. For integrated annual responses, also consider keeping the full-window model with a recent (not 1951-2004) climatology for the unknown months.

## Limitations

- **Observed weather only.** We did not use archived weather or seasonal forecasts. Real forecasts for the unknown months can recover part of the lost gain; the fill method is a lower-bound proxy for that. The 1951-2004 climatology used for fill is biased in warmer test years; a recent climatology would be fairer. This bias explains most of the fill failure in cherry flowering.
- **Zero release lag.** We assumed that monthly gridded temperature and precipitation are known at month-end. CRU TS is released once a year; GHCN-CAMS and nClimGrid are released within weeks. A one-month release lag shifts every result by one lead step.
- **The reference month is not an event date.** We counted events before issue from the observed day of year (test years). The issue date is fixed per series, not per year.
- **Few open families.** Only four families had a signal at lead 0, so H1a, H3a and H4 rest on 16 units and 4 families. The bootstrap intervals cover sampling of stations, gauges and sites within families, not the choice of families.
- **Same families as earlier tests.** The lead-0 results were known. Only the lead >= 1 results are prospective.
- Single-window linear models with 0.5-degree (global) or 1/24-degree (US) gridded climate; null calibration with 2-56 draws per series; the earlier limitations of each family (observer changes, sampling changes, national aggregation) apply.

## Reproduce

External inputs are not in this bundle (`files/EXTERNAL_DATA_NOTICE.md`). On the campaign host they are in the shared store; all 35 files match the SHA-256 recorded by the source publications (`files/provenance/shared_input_files.csv`). Elsewhere run `sh files/code/fetch_inputs.sh /path/to/inputs`. USGS and JMA files are fetched by `f01_fetch_external.py` into RAW (`files/provenance/fetched_files.csv` lists the 85 files and hashes of our fetch; the lead-0 results with these new downloads were identical to the published ones).

```
DATASETS=/path/to/inputs RAW=/path/to/raw SCRATCH=/path/to/scratch BUNDLE=/path/to/out \
PRIOR8804=/path/to/8804b69f_results PRIOR6081=/path/to/6081bf76_results sh files/code/run_all.sh
```

PRIOR8804 and PRIOR6081 hold `series_diagnostics.csv` and `family_summary.csv` of the two source publications (`sci read <zip> --file files/results/series_diagnostics.csv --output ...`). Python 3.12 with numpy, pandas, scipy, netCDF4, geopandas, shapely, pyproj and matplotlib. On the dell host with at most 2 processes: data build about 75 minutes (most of it the USGS download and NDVI), lead-0 reproduction about 15 minutes, all leads with both nulls about 45 minutes, tests about 10 minutes. Record-level intermediates go to SCRATCH and are not bundled.

## Files

- `files/plan/` frozen plan, FreeTSA query and reply.
- `files/code/` all code. New: `p21_lead.py`, `n21_null_lead.py`, `r20_repro.py`, `s22_tests.py`, `s23_figures.py`, `s24_exploratory.py`, `p00_provenance.py`, run scripts. Unchanged copies (MIT, SCI baseline): `b01_families.py`, `b02_ndvi.py`, `f01_fetch_external.py` from sci:sha256:8804b69f; `b11_families.py`, `c11_climate.py`, `b03_pack.py`, `p04_forecast.py`, `n07_null.py`, `n17_null_trend.py` from sci:sha256:6081bf76.
- `files/results/` aggregate results; `repro_lead0_prefreeze.csv` (pre-freeze check) and `repro_lead0.csv` (final run); `series_lead_diagnostics.csv.gz` (per-series and per-lead model statistics; no observed response values).
- `files/provenance/` input hashes and URLs.
- `files/EXTERNAL_DATA_NOTICE.md` sources, terms and required attributions.
