# The CRW four-month outlook rules alone give its 3.7-times Alert over-forecast: a perfect-SST emulation at 3,595 reef cells (2019-2025) matches the measured error

Campaign 11_07_2026. Job `sci-1107-hp-earth-and-ocean-sciences-57bebfaec126`. Topic: earth and ocean sciences.
Machine: hp. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The earlier SCI study sha256:a1c89b0a found that the NOAA Coral Reef Watch (CRW) Four-Month Coral Bleaching Outlook (v5, CFSv2) gave Alert Level 1+
probabilities about 3 to 4 times too high at lead weeks 9-20 (2019-2026), but correct values at week 1. That study suggested a warm model SST offset as the cause,
but it did not test a cause.

The outlook algorithm (Liu et al. 2018, Table 1 and Figure 1) has two rules that the satellite product does not have:

1. **HotSpot threshold ramp.** The satellite DHW adds only daily HotSpots of at least 1 deg C. The outlook adds every predicted HotSpot at or above a
   threshold that falls linearly from 1 deg C at lead day 0 to 0 deg C at day 70 and later. Thus, after day 70, every day with SST above the maximum monthly mean (MMM) adds heat to the DHW.
2. **DHW threshold ramp** for the Warning level, from 0 to 2 deg C-weeks at day 70.

CRW added the ramp because model SST in the top 10 m has smaller daily excursions than satellite SST (top 1 m).

We applied the published outlook rules to the observed SST (NOAA OISST v2.1) as if the SST forecast were perfect. We compared the result with the satellite
rules applied to the same SST. We also measured the sub-monthly SST variability of 36 CFSv2 operational forecasts at the reef cells. The plan and the six
predictions were written before we computed any emulation output (`files/PREREGISTRATION.md`). All six predictions passed.

Main results (329 weekly issues from 2019-04-28 to 2025-08-10; 3,595 reef cells; 95% block-bootstrap intervals):

1. **The rule alone gives the measured excess.** With a perfect SST forecast, the published rules give Alert 1+ observed/expected (O/E) = 1.23 at week 1,
   0.39 (0.36-0.43) at weeks 5-12 and **0.27 (0.23-0.31) at weeks 9-20**. The measured outlook O/E (bin mid, a1c89b0a) at weeks 9-20 is **0.25**.
   The rule-only error is 0.94 (0.85-1.05) of the measured log error (H6). On the same issues, at lead weeks 12 and 16, the measured outlook O/E was 0.30 and 0.29;
   the perfect-SST emulation gave 0.29 and 0.25 (Figure 1, `comparison_matched_issues.csv`). Warning+ also agrees: emulated 0.45, measured 0.45 at weeks 9-20.
2. **Damping does not save the rule.** CFSv2 sub-monthly SST variability at the reef cells is 0.76-0.80 of OISST (36 runs; standard deviation of daily SST minus its
   31-day running mean). This damping does not change with lead time between days 16 and 125 (Figure 6), but the threshold falls from 1 to 0 deg C in the same period.
   If the forecast SST had no sub-monthly variability at all (alpha = 0), the published rules still give Alert 1+ O/E = 0.27 (0.23-0.31) at weeks 13-20 (H2).
   With a fixed 1 deg C threshold, removing all sub-monthly variability lowers the Alert frequency by only a factor of 1.2 (O/E 1.44 to 1.73). The ramp raises it by a factor of 5.3 to 6.4.
   Thus the ramp corrects for damping about 5 times too strongly.
3. **The rule explains the year, region and cell pattern.** By issue year (weeks 5-12), the emulated O/E and the measured O/E have a Spearman correlation of 0.89
   (p = 0.007, 7 years). The emulated excess is largest in the cool years 2020-2022 (O/E 0.33) and smallest in 2023-2024 (0.46) (H3). By region, the correlation is 0.94 (6 regions);
   the largest excess is in the Western Pacific-Coral Triangle in both (emulated 0.30, measured 0.25 low bound). Across 3,595 reef cells, the two cell log ratios have
   Spearman 0.69 (H4). Because both ratios contain a truth term, we also removed each data set's own observed frequency: the emulated forecast frequency still predicts the
   real outlook's forecast frequency per cell (partial rank correlation 0.65 at weeks 5-12).
4. **Why the measured Watch level is too rare.** The outlook classifies each week from the weekly MEDIAN of daily HotSpot and DHW. The verification truth is the 7-day MAXIMUM of the daily level.
   With a perfect SST forecast, this mismatch alone makes Watch+ 1.17 times too rare at all leads (H5; measured 1.05-1.27) and Alert 1+ 1.44 times too rare if the
   1 deg C threshold is kept. The ramp more than cancels this deficit for the Warning and Alert levels.
5. **What threshold would be neutral.** With a perfect SST forecast, a long-lead HotSpot threshold of about 0.86 deg C (weeks 13-20; 0.80 at weeks 5-12) gives O/E = 1.
   With alpha = 0 (no sub-monthly variability) the value is still 0.82 deg C (`threshold_hstar.csv`, Figure 2). The published value is 0.
6. **The rule error grew with ocean warming.** In a 1985-2025 emulation (every second Sunday), the rule-only Alert 1+ excess (expected minus observed cell-weeks, weeks 9-20)
   rose from 1.6% of reef cell-weeks in 1985-1994 to 14.6% in 2015-2025 (+3.9 percentage points per decade; Spearman with year 0.92). The O/E stayed between 0.08 and 0.37 in all 41 years.
   The cause is the heat that only the outlook counts: the annual sum of HotSpots between 0 and 1 deg C per reef pixel rose from about 2-3 to about 8 deg C-weeks (Figure 5).

Conclusion: the CRW outlook would over-forecast Alert levels by the measured amount even if the CFSv2 SST forecast were perfect, or if it had no sub-monthly variability.
A warm model SST offset is not necessary to explain the error. The result supports the outlook rule as the main source of the error found by a1c89b0a
and challenges the warm-offset explanation that a1c89b0a suggested. Short-lead errors (weeks 1-4) are not explained: there the real outlook gave more Alerts than the emulation
(measured O/E 0.56 at week 4 against emulated 0.76; 1.00 at week 1 against 1.23).

## Why this matters

The ramp was tuned on a few bleaching events (2005 Caribbean, 2010 global) and then kept. With a perfect forecast, it already over-forecast Alert levels by 4-5 times
in 2005 and 2010 (emulated O/E 0.25 and 0.20). As reefs warm, more days sit just above the MMM, and the rule turns this heat into false Alerts. A change of one
number (the long-lead HotSpot threshold, from 0 to about 0.8-0.9 deg C), or the satellite 1 deg C threshold together with the 7-day maximum classification,
would remove most of the error. This must be checked with the real CFSv2 ensemble before use, because member spread and model bias also affect the result.

## Data and method

- **SST.** NOAA OISST v2.1 daily 0.25 deg, 1985-2025 (41 campaign shared files; paths, URLs and SHA-256 in `files/provenance/oisst_files.csv`).
  For each 0.5 deg CRW reef cell of a1c89b0a (`reef_cells.csv`, 4,213 cells), we used the valid OISST pixels inside the cell (14,433 pixels, 4,013 cells; 3,595 of these cells also have outlook data).
- **Climatology.** CRW method per pixel: monthly means 1985-2012 without 1991-1992, linear trend per month, re-centred to 1988.2857; MMM = maximum of the 12 values. HotSpot = max(SST - MMM, 0).
- **Truth (satellite rules).** Daily DHW = sum of HotSpots >= 1 deg C over 84 days / 7. Daily level from Table 1 of Liu et al. (2018), satellite column.
  Weekly truth = maximum daily level in the Monday-Sunday week (as the CRW `baa-max-7d` truth of a1c89b0a). Cell event = level >= k in at least half of the cell's pixels.
  Validation: the OISST truth frequencies are near the CRW 5km truth frequencies (Alert 1+ 5.9% against 5.0%; Watch+ 48% against 46%), and the per-cell truth frequencies have Spearman 0.75 (`validation_truth_frequency.csv`, `comparison_cells_strict.csv`).
- **Perfect-SST outlook emulation** (`code/02_emulate.py`). For each issue (initial-condition Sunday S), the 7 initial-condition days D = S-6..S are 7 equal members.
  HotSpots up to D use the satellite filter. HotSpots after D come from the forecast SST and use the threshold 1 - (1 - h) min(lead, 70)/70 (published: h = 0).
  Weekly HotSpot and DHW = medians of 7 daily values; the level uses the outlook column of Table 1, with both thresholds at the lead of the middle day of the week.
  Expected count E = sum of member-mean probabilities over cells; O = truth count. The forecast SST is R31 + alpha (SST - R31), with R31 the centred 31-day running mean (alpha = 1: perfect; alpha = 0: no sub-monthly variability).
  A check: with h = 1 and weekly-median truth, O/E = 1.000 at all leads for Alert levels (`Omedian_over_E` in `emulated_ratio_by_lead.csv`), so the code reproduces the satellite rules exactly.
- **CFSv2 damping** (`code/03_fetch_cfs.py`, `code/05_cfs_damping.py`). Ocean top-layer temperature (`ocnsst`, POT at 5 m, 0.5 deg grid that matches the CRW cells), member 01 of the 00Z 9-month run,
  on the first day of every second month from 2019-05 to 2025-03 (36 runs), daily mean of the 12 and 24 h steps, days 1-140 (only these GRIB messages were read, through the `.idx` byte offsets).
  Damping factor = pooled SD ratio of (daily SST - 31-day running mean), CFSv2 against OISST, on the same dates; 1,000 run-bootstrap draws.
- **Measured outlook error** from a1c89b0a: `reliability_by_lead.csv`, `reliability_strata.csv`, `issue_series.csv` and `cellbias_cells.csv`, read from the verified bundle.
- **Uncertainty.** Block bootstrap over issues (blocks of 13 weeks; 500 draws for main ratios, 200 for strata). With 6.3 years of issues, year-to-year climate gives few independent samples.

## Figures

- `files/figures/fig1_ratio_by_lead.png`: O/E by lead week for Alert 1+, Warning+ and Watch+: measured outlook (a1c89b0a) and perfect-SST emulations.
- `files/figures/fig2_threshold_grid.png`: O/E at weeks 13-20 against the long-lead HotSpot threshold h, for three sub-monthly SST amplitudes.
- `files/figures/fig3_year_region.png`: emulated against measured O/E by issue year and by region.
- `files/figures/fig4_cells.png`: per-cell emulated and measured log ratios, and a map of the emulated rule excess.
- `files/figures/fig5_long_record.png`: rule-only Alert frequency 1985-2025, and the annual HotSpot sums below and above 1 deg C.
- `files/figures/fig6_cfs_damping.png`: CFSv2/OISST sub-monthly SD ratio by lead, with the published HotSpot threshold.

## Tables (in `files/results/`)

`predictions.json` (H1-H6), `emulated_ratio_by_lead.csv` (all variants, events and leads; also member-S-only and weekly-median-truth ratios), `comparison_by_lead.csv`,
`comparison_matched_issues.csv`, `comparison_year_region.csv`, `comparison_year_region_correlations.csv`, `comparison_cells.csv`, `comparison_cells_strict.csv`,
`cells_emulated_vs_measured.csv`, `threshold_grid.csv`, `threshold_hstar.csv`, `sensitivity_threshold_day.csv`, `validation_truth_frequency.csv`, `cfs_damping_summary.csv`,
`longrecord_by_issue_year.csv`, `hotspot_classes_by_year.csv`. `files/derived/emu_*.npz` hold the aggregate emulation sums (per issue, lead week, region-hemisphere group and level), so that
`04_analyze.py` and the first part of `07_longrecord.py` run without the SST data.

## Sensitivity

- Thresholds at the last day of the target week (not the middle day): Alert 1+ O/E 0.27 at weeks 9-20 (unchanged), 1.16 at week 1.
- One member only (initial-condition day S): Alert 1+ O/E 0.28 at weeks 9-20.
- alpha = 0.5: 0.29; alpha = 0: 0.29 at weeks 9-20.

## Limitations

- The emulation is not the outlook. It has no model bias, no ensemble spread and no CFSv2 climatology. We show that the rules are sufficient to produce the measured excess. We do not show that
  CFSv2 has no warm offset; a warm offset and the rule could both act, and the short-lead (weeks 1-4) difference shows that some other factor exists.
- If the real CFSv2 SST had a warm offset in addition to the rule, the real excess would be larger than the emulated one. The measured excess is not larger at weeks 9-20 (0.25 against 0.27). This argues against a large warm offset, but member spread can act in both directions.
- The truth here is OISST (0.25 deg). The outlook verification used the CRW 5km product. The two truths agree in frequency and pattern, but not exactly. The ratio O/E of the emulation uses only OISST.
- CFSv2 damping uses one member per run, 36 runs, and instantaneous 00Z/12Z values; it measures only sub-monthly variability, not month-scale anomalies.
- The measured outlook O/E depends on how the 10% bins are read; we compare with the bin mid and the bin bounds of a1c89b0a.
- The issue period ends in August 2025, because the shared OISST record ends in December 2025. The a1c89b0a measurements cover issues to November 2026.
- The 1985-2018 part is a rule-only emulation; no outlook existed then in this form.

## Deviations from the pre-registration

- Added after the first results: the partial cell correlations (`comparison_cells_strict.csv`), because the pre-registered cell ratio test shares a truth term in both ratios;
  the OISST-CRW truth validation table; the decomposition with h = 1; the CFSv2 damping measurement (planned in spirit as "damping brackets", but the real-model measurement was added).
- The long record uses every second Sunday (not every Sunday) to save CPU time. The threshold-day sensitivity also uses every second Sunday.
- The pre-registration did not fix whether the ratios in H6 use E with the [0,10%) bin at 0.05 (bin mid) or at 0; we used the bin mid of a1c89b0a as written there.

## Reproduction

Requirements: Python 3.12 with numpy, pandas, scipy, netCDF4, matplotlib; for CFSv2 a private environment with `pygrib`. About 3 GB of scratch space and about 4 CPU-hours.

```
sci pull sha256:a1c89b0a2049e04686404a3e8c6328989d3ff2645bf7d429cc3d7158b28322a4   # measured outlook tables and reef cells
sh files/code/run_all.sh DATASETS_DIR a1c89b0a2049e04686404a3e8c6328989d3ff2645bf7d429cc3d7158b28322a4.zip SCRATCH_DIR
```

`DATASETS_DIR` must contain `noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109/sst.day.mean.YYYY.nc` for 1985-2025 (download from the PSL URLs in `files/provenance/oisst_files.csv`
and compare the SHA-256). `03_fetch_cfs.py` reads the CFSv2 files listed in `files/provenance/cfs_runs.csv` from the NOAA open-data bucket (the idx hash in that table identifies the file version).
The analysis alone (no SST data) runs from the bundled aggregates:

```
python files/code/04_analyze.py files/derived/emu_main.npz files/derived/emu_hgrid.npz files/derived/emu_end.npz PRIOR/files/results/primary OUT
```

Run times on the hp host at load 15-40 with 2 processes: OISST extraction about 15 minutes, main emulation about 90 minutes, threshold grid about 2 hours, long record about 70 minutes, CFSv2 download about 1.8 hours.

## External data and license

See `files/NOTICE-external-data.md`. No raw external data are bundled. OISST and CFSv2 are NOAA works. The `LICENSE` applies to our code, text, figures and aggregate tables.

## References

- Liu G. et al. (2018) Predicting heat stress to inform reef management: NOAA Coral Reef Watch's 4-month Coral Bleaching Outlook. Front. Mar. Sci. 5:57. doi:10.3389/fmars.2018.00057
- Huang B. et al. (2021) Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. J. Climate 34:2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Saha S. et al. (2014) The NCEP Climate Forecast System Version 2. J. Climate 27:2185-2208. doi:10.1175/JCLI-D-12-00823.1
- Skirving W. et al. (2020) CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sens. 12:3856. doi:10.3390/rs12233856
- SCI publication sha256:a1c89b0a (measured outlook error) and earlier campaign verifications of public hazard products (cited in `sci.json`).
