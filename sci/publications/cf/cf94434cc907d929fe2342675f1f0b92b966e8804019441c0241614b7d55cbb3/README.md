# The GOES flux-scale change of December 2019 explains the Cycle 25 M-flare excess per F10.7 unit and made SWPC M-flare forecasts too low in 2020-2024

## Summary

In December 2019, GOES-16 became the primary NOAA X-ray satellite. At that time, NOAA stopped applying the 0.7 factor to the long-channel (1-8 Å) flux. Flare peak fluxes in the operational NOAA/SWPC event list are therefore about 1.43 times larger after this date than before it. This change occurred at the minimum between Solar Cycle 24 and Solar Cycle 25. Thus, the operational list compares Cycle 25 on one flux scale with Cycles 23 and 24 on a different flux scale.

We used the SWPC event lists (1998-2026), the NCEI science-quality GOES flare summaries (GOES-8 to GOES-19), the SWPC daily solar data and 9,515 SWPC daily forecasts. We did these steps:

1. We matched 34,845 operational events (C1 and larger) to science-quality peaks from the same satellite. The median ratio of science peak to operational peak is 1.451 for all events before December 2019 and 1.016 after it (Figure 1a). The change is a step, and it occurs when the event list changes from GOES-15 to GOES-16.
2. We made one homogeneous flare list on the true (science) flux scale, and we compared the flare rates of the three cycles at matched solar activity.
3. We compared the SWPC M-class and X-class probabilities with the outcomes on the operational scale and on the legacy (x0.7) scale.

Main results:

- **Rescaling increases the Cycle 24 M-flare count by a factor of 1.53** (797 to 1,219 flares of M1 or more; X1 or more: 1.55). An independent count from NCEI science-quality detections agrees with the homogeneous list (5,787 against 5,698 flares in 1998-2026; Figure 1b).
- **Per unit of F10.7, Cycle 25 does not have more M flares than Cycle 24.** With the operational list, the Cycle 25/Cycle 24 rate ratio at matched F10.7 is 1.38 (95% CI 1.10-1.77). With the homogeneous list, it is 0.92 (0.74-1.15). With NCEI science detections, it is 0.87 (0.69-1.14). The scale change explains all of the apparent excess per F10.7 unit.
- **Per sunspot, Cycle 25 has about 1.4 times more M flares than Cycle 24, also after the correction.** With SWPC sunspot number, the ratio falls from 2.21 (1.72-2.83, operational) to 1.45 (1.14-1.84, homogeneous). With SWPC sunspot area, it falls from 2.19 (1.79-2.68) to 1.44 (1.19-1.79). Thus, the scale change explains about half of the logarithmic excess per sunspot. The remaining excess agrees with a higher F10.7 per sunspot in Cycle 25: at a SILSO sunspot number of 100, the F10.7 regression gives 140 sfu in Cycle 25 and 131 sfu in Cycles 23 and 24.
- **The SWPC M-class probabilities did not follow the new flux scale in 2020-2024.** In Cycles 23 and 24, the observed frequency of M-flare days was 0.79 and 0.78 times the mean day-1 forecast (forecasts too high). In Cycle 25, the ratio is 1.12 (1.05-1.19) with the operational list (forecasts too low). The change from Cycle 24 to Cycle 25 is a factor of 1.43 (1.28-1.59). This is the size of the removed factor. With outcomes on the legacy scale, the change is only 1.12 (0.99-1.26). For 2020-2024, the outcome frequency at the same issued probability was 1.64 (1.46-1.86) times the Cycle 24 frequency on the operational scale, and 1.31 (1.13-1.49) times on the legacy scale.
- **In 2025-2026 the SWPC forecasts became higher.** At matched F10.7 and prior-day flare state, the mean day-1 M probability increased from 2020-2024 to 2025-2026 (Section 4.4). The operational-scale ratio of observed to forecast frequency became 0.93 (0.85-1.01) in 2025-2026. This agrees with an adjustment of the forecasts, but the data cannot separate an adjustment from an effect of the cycle phase.
- **X-class forecasts:** the observed/forecast ratio changed by 1.50 (1.01-2.40) on the operational scale and by 0.92 (0.59-1.53) on the legacy scale. SWPC X-class forecasts stay too high in all cycles (operational ratio 0.34-0.52).

Limitations: the analysis uses one data set per index and three solar cycles. The rate ratios assume one constant cycle factor at all activity levels. Flare rates per F10.7 unit also differ between Cycles 23 and 24 (0.72, CI 0.57-0.93) on one flux scale. Thus, a cycle-to-cycle difference of about 30% occurs also without a scale change. We cannot say which activity index is the correct normalization. Cycle 25 is not complete (data to 8 November 2026).

## 1. Question and background

The NOAA GOES X-ray Sensor (XRS) gives the standard flare classes (C, M, X). For GOES-8 to GOES-15, NOAA multiplied the 1-8 Å flux by 0.7, so that the data agreed with GOES-7. The GOES-R satellites (GOES-16 and later) give the true flux. NOAA did not use the factor for GOES-16. NCEI reprocessed GOES-1 to GOES-15 without the factor. Janssens et al. (2025, Space Weather and Space Climate 15, 14) showed that the correction increases the M and X counts for 1976-2019 by about 50%. A recent verification of the SWPC flare forecasts for 1998-2024 (arXiv:2508.01114) did not examine the scale change.

Many people state that Cycle 25 has more large flares than expected from its sunspot number. We asked two questions:

1. How much of the Cycle 25 flare excess per unit of activity comes from the flux-scale change, and how much remains on one homogeneous scale?
2. Did the SWPC probability forecasts change with the flux scale? If not, the forecasts must become too low for operational outcomes after December 2019.

## 2. Data

All flare and forecast data are from NOAA (United States Government work, public domain).

| Data | Source | Use |
| --- | --- | --- |
| SWPC edited event lists, 1998-05 to 2026-11-09 | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_events.tar.gz`, `2026/2026_events/` | Operational flare list (54,543 XRA 1-8 Å events with class and satellite) |
| SWPC Report of Solar-Geophysical Activity (RSGA), 2000-10 to 2026-11-09 | `.../warehouse/YYYY/YYYY_RSGA.tar.gz`, `2026/RSGA/` | Day-1, day-2, day-3 probabilities for M-class and X-class flares (issued 2200 UT) |
| SWPC Daily Solar Data (DSD), 1997-2026 | `.../warehouse/YYYY/YYYY_DSD.txt`, `pub/indices/old_indices/2026Q*_DSD.txt` | F10.7, SESC sunspot number, sunspot area, daily flare counts (check) |
| NCEI GOES XRS L2 flare summaries (science quality), GOES-08 to GOES-19 | `https://www.ncei.noaa.gov/data/goes-space-environment-monitor/access/science/xrs/goesNN/xrsf-l2-flsum_science/` (v1-0-0, v2-3-0) and `https://data.ngdc.noaa.gov/platforms/solar-space-observing-satellites/goes/goesNN/l2/data/xrsf-l2-flsum_science/` (v2-2-2) | True-scale peak fluxes; independent flare detections |
| SILSO daily total sunspot number V2.0 | `https://www.sidc.be/SILSO/INFO/sndtotcsv.php` (CC BY-NC 4.0) | Aggregate cross-check of F10.7 per sunspot only; not in this bundle |

The SHA-256 of each input file is in `files/data/input_sha256.txt` (790 files). NCEI issues the GOES-R mission files again with new end dates. We used the files that end on 2026-11-08.

The F10.7 values come from the Penticton observatory (National Research Council Canada) through the SWPC DSD. We do not include the F10.7 column in the bundled daily table. The script `00_fetch_data.sh` downloads it again.

## 3. Methods

**Event parsing (`01_parse.py`).** We read all XRA 1-8 Å lines of the SWPC event lists (class, begin, maximum and end time, satellite). We read the M and X probabilities from section III of each RSGA. We read the DSD table. We read the `EVENT_PEAK` records of the NCEI flare summaries (yearly files for GOES-08 to GOES-15, mission files for GOES-16 to GOES-19).

**Scale check (`02_crossmatch.py`).** For each operational event of class C1 or larger, we found the science peak of the same satellite within 4 minutes of the operational maximum. 34,845 of 37,550 events have a match.

**Homogeneous list (`03_daily.py`).** For each operational event, the true-scale peak is the matched science peak. If there is no match, it is the operational peak times the median ratio of its era (1.451 before 2019-12-01, 1.016 after). The legacy-scale peak is 0.7 times the true-scale peak. We counted the events per UT day (day of the peak) at three thresholds (M1, M5, X1) for each scale. As an independent check, we counted the NCEI science detections of one primary satellite per period (GOES-08, 12, 11, 10, 14, 15, 16, 18) at the same thresholds. The event-list daily counts agree with the DSD daily M+X counts (correlation 0.996; 4,412 against 4,413 flares).

**Cycles.** C23: 1998-06-01 to 2008-11-30. C24: 2008-12-01 to 2019-11-30. C25: 2019-12-01 to 2026-11-08. The C24/C25 boundary is also the date of the scale change.

**Rate ratios (`04_rates.py`).** We fitted a Poisson regression of the daily flare count on a cubic regression spline (4 degrees of freedom) of the logarithm of one activity index, plus one indicator for C23 and one for C25 (C24 is the reference). The indicator coefficients give the rate ratios at matched activity. We used three indices: F10.7, SWPC SESC sunspot number and SWPC sunspot area. We used three variants: all days ("main"); only the activity range that both C24 and C25 cover between their 5th and 95th percentiles ("common"); and C24 limited to its first 83 months, which is the same cycle age as the C25 data ("phase"). The 95% intervals come from a bootstrap of 27-day blocks within each cycle (300 replicates for the main M1 fits, 100 for the others).

**Forecast verification (`05_forecast.py`, `05b_ratio_of_ratios.py`, `05c_c25_split.py`).** The RSGA issued at 2200 UT on day d gives the probabilities for UT days d+1, d+2 and d+3. The outcome for day d+k is one or more events at or above the threshold on that day, with the operational, legacy or true peak. For each cycle and scale, we calculated the ratio of the observed frequency to the mean forecast, the Brier skill score against the sample climatology of the cycle, reliability tables, and a logistic recalibration (intercept and slope on logit p). The change of calibration from C24 to C25 is the ratio of the two observed/forecast ratios. A stratified version compares the C25 outcomes with the C24 frequency at the same issued probability. The intervals come from a 27-day block bootstrap (1,000 replicates).

## 4. Results

### 4.1 The scale step

Figure 1a shows the quarterly median ratio of science peak to operational peak. Before December 2019, the ratio is 1.40-1.49 in almost all quarters for GOES-08, 09, 10, 11, 12, 14 and 15 (median 1.451). Two GOES-13 quarters with few events give 1.58 and 1.64. It is slightly larger than 1/0.7 = 1.429 because the NCEI reprocessing also changed other calibration terms. After the change to GOES-16, the ratio is 1.01-1.03 (median 1.016). GOES-18 and GOES-19 also give 1.01-1.06. The first G16 events in the operational list occur in December 2019.

### 4.2 Flare rates at matched activity

Table 1. Cycle 25/Cycle 24 rate ratio of flares of M1 or more at matched activity (main variant, 95% block-bootstrap interval). Full results for M1, M5 and X1, three variants and C23/C24 are in `files/results/rate_ratios.csv`.

| Activity index | Operational list | Homogeneous list | NCEI science detections |
| --- | --- | --- | --- |
| F10.7 | 1.38 (1.10-1.77) | 0.92 (0.74-1.15) | 0.87 (0.69-1.14) |
| SWPC sunspot number | 2.21 (1.72-2.83) | 1.45 (1.14-1.84) | 1.39 (1.05-1.82) |
| SWPC sunspot area | 2.19 (1.79-2.68) | 1.44 (1.19-1.79) | 1.38 (1.12-1.70) |

The "common" and "phase" variants give the same pattern (Figure 3). In the common F10.7 range (76-162 sfu), the homogeneous ratio is 0.77 (0.61-1.00). For M5 and X1 flares, the homogeneous ratios at matched F10.7 are 0.80 (0.53-1.16) and 0.75 (0.47-1.33). At matched sunspot number, they are 1.31 (0.90-1.91) and 1.25 (0.70-1.99).

On one scale, C23/C24 rate ratios are 0.72 (0.57-0.93) per F10.7 unit and 0.87 (0.69-1.12) per sunspot number. Thus, differences of 15-30% between cycles also occur without a scale change.

The F10.7 per sunspot increased in Cycle 25. A linear fit of monthly F10.7 on the monthly SILSO sunspot number (months with SN > 20) gives F10.7 = 63.5 + 0.670 SN for C23, 63.6 + 0.672 SN for C24 and 60.4 + 0.794 SN for C25. With the SWPC SESC sunspot number, the result is the same (142 sfu at 100 in C25, against 128-129 sfu). The ratio of SESC to SILSO sunspot number is 0.97-1.03 in all cycles. Thus, the change is not a change of the SWPC sunspot count. Because the flare rate per F10.7 unit did not change, the higher F10.7 per sunspot agrees with the remaining excess of flares per sunspot.

### 4.3 SWPC forecasts across the scale change

Table 2. Day-1 M-class forecasts: observed frequency divided by mean forecast probability (95% interval).

| Cycle | Days | Mean forecast | Operational outcome | Legacy-scale outcome | True-scale outcome |
| --- | --- | --- | --- | --- | --- |
| C23 (2000-10 to 2008-11) | 2,981 | 0.232 | 0.79 (0.74-0.84) | 0.79 (0.73-0.85) | 1.02 (0.96-1.08) |
| C24 | 4,008 | 0.139 | 0.78 (0.71-0.86) | 0.78 (0.71-0.86) | 1.05 (0.98-1.12) |
| C25 | 2,526 | 0.273 | 1.12 (1.05-1.19) | 0.88 (0.81-0.95) | 1.12 (1.06-1.19) |

Figure 4a shows that in C25 the operational outcome frequency is above the diagonal at most probabilities. In C23 and C24 it is below the diagonal. With legacy-scale outcomes (Figure 4b), the three cycles agree more closely. The calibration change from C24 to C25 is 1.43 (1.28-1.59) with operational outcomes at day 1, 1.43 at day 2 and 1.42 at day 3. With legacy-scale outcomes, it is 1.12 (0.99-1.26), 1.11 and 1.10. The Brier skill score of the M-class forecasts is 0.23-0.32 in all cycles (`files/results/forecast_summary.csv`).

For X-class day-1 forecasts, the observed/forecast ratio is 0.52, 0.34 and 0.52 for C23, C24 and C25 with operational outcomes. The change from C24 to C25 is 1.50 (1.01-2.40) on the operational scale and 0.92 (0.59-1.53) on the legacy scale. The X-class result has large uncertainty (107 operational X flares in C25).

### 4.4 Change during Cycle 25

Figure 4c shows the observed/forecast ratio for each year. It is 0.76-0.95 in all active years from 2001 to 2015. It is 1.07-1.34 in 2021-2024 and 0.98 and 0.86 in 2025 and 2026.

Table 3. Day-1 M-class calibration in two parts of Cycle 25 (`files/results/c25_split_calibration.csv`).

| Period | Days | Mean forecast | Observed / forecast, operational | Against C24 calibration, operational | Observed / forecast, legacy |
| --- | --- | --- | --- | --- | --- |
| 2019-12 to 2024-12 | 1,851 | 0.235 | 1.23 (1.16-1.30) | 1.64 (1.46-1.86) | 0.98 (0.90-1.06) |
| 2025-01 to 2026-11 | 675 | 0.376 | 0.93 (0.85-1.01) | 1.24 (1.10-1.42) | 0.69 (0.62-0.75) |

At matched F10.7 and matched prior-day M-flare state, the mean SWPC day-1 M probability in 2020-2024 was lower than or equal to the C24 value (for example, F10.7 120-150 sfu and no M flare on the prior day: 0.21 against 0.27). In 2025-2026, it was higher (0.33). See `files/results/forecast_level_by_activity.csv`. This agrees with an upward adjustment of the forecasts in 2025. We did not find a public SWPC notice about such a change. Also, the declining phase of a cycle can have different flare conditions. Thus, this result is not a proof of an adjustment.

## 5. Interpretation

The operational NOAA flare record has a step of about 1.43 in peak flux at the start of Cycle 25. For flare counts above a fixed class, this step gives about 1.5 times more M and X flares. Comparisons of Cycle 25 with earlier cycles that use the operational classes include this artefact. On one homogeneous scale, Cycle 25 produces the number of M flares that its F10.7 predicts from Cycle 24. It produces about 1.4 times more M flares per sunspot than Cycle 24, together with about 7-10% more F10.7 per sunspot. A possible physical explanation is that Cycle 25 active regions have more magnetic flux or more plage per counted sunspot. We did not test this explanation.

The SWPC M-class probabilities stayed close to their earlier relation to activity in 2020-2024. Because the outcomes are now measured on the larger true scale, the earlier small over-forecast changed to an under-forecast. A user who verifies SWPC probabilities over periods that include December 2019 must use one flux scale for the outcomes. Forecast systems that are trained on GOES-1 to GOES-15 operational classes and verified on GOES-R classes (or the opposite) have the same problem.

## 6. Limitations

- Only three cycles, and Cycle 25 is not complete. The cycle factor is one number for all activity levels.
- The choice of activity index changes the answer for the flare excess (F10.7: no excess; sunspot number and area: about 1.4). We report all three. We do not know which index is the best normalization.
- The homogeneous list keeps the SWPC event detections. Only the peak flux changes. Events that SWPC did not list (for example, during data gaps or overlapping flares) are not in the list. The NCEI science detections use a different algorithm and give the same result.
- 7% of the operational events have no science match. For these events we used the median era ratio.
- The forecast analysis uses the 2200 UT RSGA only. We did not analyse the region-level probabilities or the 3-day forecast product.
- The bootstrap uses 27-day blocks. Longer dependence (for example, from long-lived active regions) can make the true intervals wider.
- We do not know the SWPC internal procedure. The 2025 forecast increase can have other causes.

## 7. Reproduction

```
bash files/code/00_fetch_data.sh <work>          # NOAA/NCEI/SILSO files into <work>/raw (scratch, not the bundle)
python -I files/code/01_parse.py <work>          # -> <work>/derived/*.csv
python -I files/code/02_crossmatch.py <work>
python -I files/code/03_daily.py <work>
for x in f107 area ssn; do for v in main common phase; do
  python -I files/code/04_rates.py <work> 300 $x:$v & done; done; wait
python -I files/code/04b_merge.py <work>
python -I files/code/05_forecast.py <work> 1000
python -I files/code/05b_ratio_of_ratios.py <work> 1000
python -I files/code/05c_c25_split.py <work> 1000
python -I files/code/07_silso_check.py <work>
python -I files/code/06_figures.py <work> <work>/figs
```

Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, statsmodels 0.15.0, patsy 1.0.3, xarray 2026.9.0, matplotlib 3.11.2. Random seeds are fixed. Compare the input file names and hashes with `files/data/input_sha256.txt`. Later NCEI and SWPC files can add days after 2026-11-08.

## 8. Files

- `files/code/`: all scripts.
- `files/data/events_homog.csv.gz`: the 54,543 SWPC XRA events with operational, matched science, true-scale and legacy-scale peak flux.
- `files/data/xmatch_ops_sci.csv.gz`: the event-to-science match table (C1 and larger).
- `files/data/daily_counts_forecasts_noaa.csv.gz`: daily counts on each scale, NCEI detection counts, SWPC sunspot number and area, DSD counts and RSGA probabilities (F10.7 removed; see Section 2).
- `files/data/input_sha256.txt`: hashes of all input files.
- `files/results/`: rate ratios, forecast summaries, reliability tables, recalibration fits, calibration change, Cycle 25 split, forecast level by activity, annual ratios.
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: sources and terms of external data.

## 9. Provenance

This work was done by an automated research agent (model claude-opus-5-5) in SCI campaign 11_07_2026, job sci-1107-dell-astronomy-c625c271b19e, topic astronomy, machine dell, on 2026-11-09. The signing key is a campaign-machine key. It is not a personal claim of authorship. Related campaign work: a test of a 629-day flare clock that also corrected the GOES 0.7 factor (sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf), and a Cycle 25 amplitude forecast test (sci:sha256:ec45cb745d5f008953765f6b90cb021dc7c6fea3ef875f5f48ad9a95223b5f2d).
