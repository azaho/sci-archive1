# NOAA Coral Reef Watch four-month outlooks (2019-2026) gave coral bleaching Alert probabilities about 3 times too high at 9-20 weeks ahead, but week-1 probabilities were correct

Campaign 11_07_2026. Job `sci-1107-dell-earth-and-ocean-sciences-f4b853404a2f`. Topic: earth and ocean sciences.
Machine: dell. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The NOAA Coral Reef Watch (CRW) Four-Month Coral Bleaching Heat Stress Outlook (version 5, CFSv2 ensemble, 0.5 deg grid) is a public operational hazard product.
Reef managers use it to prepare for coral bleaching. Each week, CRW issues 10 files. The file for percentile p gives the heat-stress level that at least p% of the
ensemble members reach, for each of the next 20 weeks. The levels are: 0 No Stress, 1 Watch, 2 Warning, 3 Alert Level 1, 4 Alert Level 2.
CRW states that Alert Level 1 means "bleaching likely" and Alert Level 2 means "mortality likely".

We did a pre-registered verification (`files/PREREGISTRATION.md`) of all as-issued outlooks from 28 April 2019 to 1 November 2026 (392 weekly issues).
We compared them with the CRW satellite product of the same levels (5km daily Bleaching Alert Area, 7-day maximum) at the 5km reef pixels of the CRW reef mask.
The test unit is a 0.5 deg outlook cell with reef pixels (3,623 cells) and one forecast week. There are 5.4 to 5.6 million cell-weeks for each group of 4 lead weeks.

Main results:

1. **Week 1 is correct.** At week 1, the observed number of Alert 1+ cell-weeks was 1.03 times (95% interval 0.995-1.07) the lowest
   expectation that the stated probability bins permit. The week-1 forecast starts from the satellite observations.
2. **Alert probabilities are too high at longer leads.** The observed count of Alert 1+ cell-weeks fell to 0.45 (0.37-0.54) of the lowest
   permitted expectation at weeks 5-8, and to 0.32-0.35 (0.25-0.42) at weeks 9-20. Thus the outlook gave Alert 1+ at least 2.9 times too often for any reading
   of its 10% probability bins. Warning+ was at least 1.7-1.8 times too frequent at weeks 9-20 (0.55-0.58 of the lowest expectation). Alert 2 was similar to Alert 1+.
   When all members gave Alert 1+ at weeks 5-12, Alert 1+ occurred in only 56% of cases. At weeks 13-20 the value was 42%.
3. **Watch probabilities are too low.** Watch or higher occurred more often than the highest permitted expectation at weeks 5-20 (1.05-1.13 times).
   The outlook moves heat stress from the Watch level into the Warning and Alert levels.
4. **No skill for Alerts beyond one month.** At weeks 5-20, the Brier score of the Alert 1+ probabilities was worse than a cell calendar climatology
   (Brier skill score -0.58 to -1.39) and worse than a climatology that uses the observed state at the issue week (-0.85 to -1.39).
   It was not better than persistence of the issue-week level (-0.03 to -0.20; all four 95% intervals include 0). At weeks 1-4 the outlook was better than
   persistence (+0.22, 0.15-0.28) and calendar climatology (+0.32), but not better than the state-conditioned climatology (-0.14, -0.28 to -0.03).
5. **The error is an approximately additive floor, and it has a spatial pattern.** The observed Alert 1+ frequency at weeks 5-12 changed by a factor of 6 between issue years
   (1.8% in 2021 to 11.4% in 2024). The lowest permitted forecast frequency in the same two years was 10.4% and 18.6% (range over all years 7.9-18.6%). Thus the relative error was largest in the cool
   La Nina years 2020-2022 (0.17-0.25 of the lowest expectation) and smallest in the 2023-2024 global bleaching event (0.54-0.61).
   The error was largest in the Western Pacific and Coral Triangle (0.25, 0.20-0.31), the Indian Ocean (0.30) and the central-eastern Pacific (0.36). It was smallest
   in the Caribbean and Atlantic (0.87, 0.70-1.05). In 71% of reef cells at weeks 5-12, the forecast Alert 1+ frequency was more than 2 times the observed frequency.
   The cell errors in 2019-2022 and in 2023-2026 had a rank correlation of 0.63. Thus a large part of the error is fixed in space.
6. **The four-month composite.** The composite map at percentile p is exactly the maximum of the weekly maps (verified in all issues).
   We predicted that the composite understates the chance that any week reaches a level. This was true for Watch+ (observed/highest expectation 1.07, 1.05-1.09).
   It was false for Alert levels, because the weekly over-forecast is larger: Alert 1+ occurred in 0.55 (0.48-0.63) of the lowest permitted expectation.
7. **A simple correction removes the excess but adds no skill.** A table that maps (lead week, probability bin) to the observed frequency was fitted on 2019-2022
   and tested on 2023-2026. It decreased the Alert 1+ Brier score at weeks 5-12 from 0.0856 to 0.0563. A per-cell factor gave 0.0561. These values only equal the state-conditioned climatology (0.0562).
   The corrected forecasts were too low in the hotter 2023-2026 period (observed/expected 2.2), because the outlook excess changes from year to year.

The result is robust to the truth definition. With "any reef pixel in the cell" as truth (the most favourable choice for the outlook), Alert 1+ at weeks 13-16 was 0.40 (0.32-0.46)
of the lowest expectation. With all ocean pixels of the cell, it was 0.33. A back-filled archive (219 issues from 2011-2019, written by CRW in 2019) shows the same pattern and a larger excess
(Alert 1+ 0.13-0.16 of the lowest expectation at weeks 9-20, when observed Alert frequency was only 1.2%).

## Why this matters

The outlook is used to plan reef monitoring, to warn the public and to prepare responses. At lead times of 2-5 months, it shows Alert-level stress in most reef cells every
Southern Hemisphere summer, also in years with almost no observed Alerts (Figure 3). The stated probabilities therefore must not be read at face value beyond about 4 weeks.
The error is largest in the Coral Triangle, which has the largest reef area. The product page gives only qualitative skill information (Liu et al. 2018 compared 2011-2015
outlooks with satellite data qualitatively). We did not find a published reliability verification of the probabilistic as-issued outlook.

## Data and method

- **Forecasts.** CRW Outlook v5 netCDF archive, 10 percentile files per issue, layers `CRW_BAA_Week_01`..`_20` and `CRW_BAA_FourMonth`.
  An issue is "as issued" if the server file time is less than 10 days after the initial-condition week. This is true for all issues from 2019-04-28,
  except one file (icwk 2019-08-11) that CRW rewrote in 2020. Files before 2019-04-28 were written in bulk in August 2019. We call them "back-filled".
- **Stated probability.** For level k, p_hat = the largest percentile whose file shows level >= k. The stated probability is in [p_hat, p_hat + 10%).
  p_hat = 0 means less than 10% of members. p_hat = 100% means all members. The exact boundary depends on how CRW rounds the member count; we cannot see the members.
- **Truth.** CRW 5km `baa-max-7d` on the Sunday that ends each forecast week (week L of an issue ends L x 7 days after the initial-condition Sunday). We used the 57,504
  5km reef pixels of the CRW Thermal History v3.7 reef mask, grouped into 4,213 0.5 deg cells. Of these, 3,623 cells have valid outlook data (the outlook land mask removes 14%).
  Primary truth: the median reef-pixel level is >= k. Cells with less than half of their reef pixels valid are not used.
- **Strict bounds.** Most cell-weeks are in the [0, 10%) bin. This makes the expectation range wide. So we report O/E_low = observed count / sum of lower bin bounds.
  If O/E_low < 1, the forecasts are too high for any probability inside the stated bins. O/E_high (with upper bounds) > 1 means too low for any reading.
- **Uncertainty.** Block bootstrap over issues in blocks of 13 consecutive weekly issues (1,000 draws in the primary run). All cells of an issue stay together.
- **Reference forecasts** (only observed data, no look-ahead): persistence of the issue-week level; a state-conditioned climatology P(level at lead L | issue-week level,
  target month, region) fitted on 2011-2019 observations or refitted each January on all earlier observations ("expanding"); a calendar climatology for each cell (2011-2019, +-1 month).

## Figures

- `files/figures/fig1_ratio_by_lead.png`: O/E_low and O/E_high for each lead week, with 95% bootstrap intervals.
- `files/figures/fig2_reliability.png`: reliability diagrams (the [0,10%) bin is shown at 0.05).
- `files/figures/fig3_counts_timeseries.png`: weekly number of reef cells at Warning+ and Alert 1+: observed, and expected by the outlook at leads 1, 4 and 12 weeks.
- `files/figures/fig4_brier_skill.png`: Brier skill score of the outlook against the three reference forecasts.
- `files/figures/fig5_strata.png`: O/E_low by issue year and by region (weeks 5-12).
- `files/figures/fig6_season.png`: observed frequency and stated range by target month and hemisphere (weeks 5-12).
- `files/figures/fig7_cell_map.png`: per-cell log2(observed / forecast frequency) for Alert 1+, weeks 5-12.

## Tables (in `files/results/`)

`primary/` is the pre-registered analysis. `sens_any_pixel/` and `sens_all_ocean/` change the truth definition. `sens_zero_bin_2.5pct/` puts 2.5% (not 0) in the Brier score for the [0,10%) bin
(the change is less than 0.001 in Brier score). `secondary_backfilled_2011_2019/` uses the back-filled archive (219 of 408 issues; baselines there are in-sample).
Main files: `reliability_by_lead.csv`, `reliability_bins.csv`, `reliability_strata.csv` (issue year, region, issue-week state, ensemble-size block, target month by hemisphere),
`brier_by_lead.csv`, `brier_by_region.csv`, `composite_4month.csv`, `composite_bins.csv`, `cellbias_summary.csv`, `cellbias_cells.csv`, `recalibration_test.csv`,
`issue_series.csv`, `observed_weekly_counts.csv`, `transitions.csv`, `saturation_lead.csv`.

## Possible sources of the error (what the data show and do not show)

- The error starts at week 2, immediately after the satellite-observed start, and it grows until weeks 9-10. Then it stays constant (`saturation_lead.csv`).
  The 12-week Degree Heating Week sum controls the Alert levels. A constant warm offset of the model sea surface temperature relative to the satellite climatology
  (the maximum monthly mean, MMM) would accumulate in this way. The spatial pattern (Figure 7), the fixed part of the cell errors, and the additive floor in cool years agree with
  such an offset. But we did not have the CFSv2 sea surface temperature forecasts. Thus this explanation is not tested. Other explanations are possible, for example too large
  daily variability in the model, or the method that CRW uses to join the model to the satellite climatology.
- In 57% of reef cells (weeks 5-12), Watch+ is too rare and Alert 1+ is more than 2 times too frequent in the same cell. Across cells, the two log ratios have a
  positive rank correlation (0.30): cells with a larger Alert excess have a smaller Watch deficit. This agrees with a warm offset that changes in size from cell to cell,
  together with forecast HotSpots that are too seldom between 0 and 1 deg C above the MMM. (Exploratory; computed from `cellbias_cells.csv`.)
- An "Alert stays on after the heat ends" error (Degree Heating Weeks without the HotSpot condition) is not supported: forecast percentile maps do drop from Alert to No Stress
  from one week to the next (`transitions.csv`). But percentile maps are not member paths, so this test is weak.
- The ensemble-size changes (112, 49 and 28 members at weeks 1-5, 6-12 and 13-20) do not cause a step in the error.

## Limitations

- The truth is the CRW satellite heat-stress level, not observed bleaching. In-situ bleaching data that we could use stop in 2019-2020.
- The truth and the forecast use the same level rules, but not the same spatial support. We tested three cell definitions. The result does not change.
- The 10% bins do not give the exact probability. We report bounds that are valid for any probability inside a bin.
- The bootstrap keeps whole issues and 13-week blocks together, but year-to-year climate (ENSO) gives only 7.5 independent years. Year and region intervals are approximate.
- Reef cells that the outlook masks as land (14%) are not verified.
- The as-issued screen uses server file times. CRW could have replaced files without a change in the file time; we did not see evidence of this after April 2019.
- Only 219 of 408 back-filled issues were downloaded (all of 2011-2012 and every fourth week after that), because the CRW server was slow (20-160 kB/s).

## Deviations from the pre-registration

- Added the strict-bound ratios O/E_low and O/E_high, because the [0,10%) bin makes the pre-registered range test almost always pass at week 1.
- Added the expanding state-conditioned climatology, the target-month strata, the per-cell bias and recalibration analysis, the lead saturation analysis and the transition test.
  These were chosen after we saw the first partial results (2019-2020 issues). They are exploratory.
- Fixed the stratum bootstrap so that it resamples only blocks that contain the stratum.
- The back-filled sample is a subset (see Limitations).

## Reproduction

Requirements: Python 3.12 with numpy, pandas, netCDF4, scipy, matplotlib; curl. About 3 GB of scratch space.

```
mkdir -p scratch/raw scratch/derived scratch/results
python3 files/code/01_index.py scratch/derived/file_index.csv          # lists CRW files and server times
NPAR=6 files/code/02_fetch.sh scratch/derived/file_index.csv scratch/raw   # resumable download; rerun to retry FAIL lines
curl -4 -o scratch/raw/reef/noaa_crw_thermal_history_sst_trend_v3.7.0.nc \
  https://www.star.nesdis.noaa.gov/pub/sod/mecb/crw/data/thermal_history/v3.7/noaa_crw_thermal_history_sst_trend_v3.7.0.nc
python3 files/code/03_reefgrid.py scratch/raw/reef/noaa_crw_thermal_history_sst_trend_v3.7.0.nc scratch/derived/reefgrid.npz
files/code/run_all.sh scratch/raw scratch/derived scratch/results       # all tables and figures
python3 files/code/12_watch_alert_cells.py scratch/results/primary   # exploratory cell check
python3 files/code/10_manifest.py scratch/raw scratch/derived/file_index.csv scratch/derived/raw_file_manifest.csv scratch/derived/issues_used.txt
```

`issues_used.txt` is written from `scratch/derived/outlook_reefcells.npz` (field `icwk`); see `run_all.sh` and `05_extract_outlook.py`.

Compare the hashes with `files/provenance/raw_file_manifest.csv`. CRW can add files and can revise the 5km record. The index in
`files/provenance/file_index.csv` is the list as of 2026-11-10. `run_all.sh` uses every complete outlook issue in the raw folder; the as-issued
selection and the back-filled selection are made inside `06_verify.py`. The issue list we used is `files/provenance/issues_used.txt`.
Download all files from `file_index.csv` to also include the remaining back-filled issues. Run times on the Dell host: extraction about 10 minutes,
each verification run about 4 minutes.

## External data and license

See `files/NOTICE-external-data.md`. The CRW products are credited to NOAA Coral Reef Watch. They are not in this bundle.
The `LICENSE` applies to our code, text, figures and aggregate tables.

## References

- Liu G. et al. (2018) Predicting heat stress to inform reef management: NOAA Coral Reef Watch's 4-month Coral Bleaching Outlook. Front. Mar. Sci. 5:57. doi:10.3389/fmars.2018.00057
- Skirving W. et al. (2020) CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sens. 12:3856. doi:10.3390/rs12233856
- Saha S. et al. (2014) The NCEP Climate Forecast System Version 2. J. Climate 27:2185-2208. doi:10.1175/JCLI-D-12-00823.1
- CRW outlook product page: https://coralreefwatch.noaa.gov/satellite/bleachingoutlook_cfs/outlook_cfs.php
- Earlier campaign verifications of public hazard products are cited in `sci.json`.
