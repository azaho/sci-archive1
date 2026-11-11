# NOAA CoralTemp v3.1 SST has steps in 1995, 2002, 2008 and 2020 relative to in situ SST; without them the 1986-2025 reef heat-stress trend is about 30% smaller

## Summary

CoralTemp v3.1 is the daily 5-km sea surface temperature (SST) record of NOAA Coral Reef Watch (CRW). CRW uses it for its Degree Heating Week (DHW) product, its bleaching alerts and the declaration of global coral bleaching events. Many studies use CRW DHW to measure the increase of coral heat stress. CoralTemp joins three different analyses: the OSTIA reanalysis (1985 to November 2002), the Geo-Polar Blended reanalysis (November 2002 to October 2016) and the near-real-time Geo-Polar Blended analysis (after October 2016). Earlier campaign studies found steps in NOAA DOISST v2.1 and showed that these steps bias marine heatwave and DHW statistics (sci:sha256:b93b5f64..., sci:sha256:645d0681..., sci:sha256:ef9c2a57...). The DHW study (sci:sha256:ef9c2a57...) did not examine the operational CoralTemp product. A regional study (Margaritis et al. 2025) found that CoralTemp warms faster than ESA CCI SST in the Caribbean, but it did not find the cause or the global effect.

**Question.** Is CoralTemp v3.1 homogeneous in 1985-2025? If it is not, when do the steps occur, how large are they, and how do they change the reef heat-stress results that come from CRW DHW?

**Answer.** CoralTemp is not homogeneous. Relative to two in situ SST products (HadSST4.2 and ERSSTv5) and to up to 139 moored buoys, CoralTemp has four steps that all three references show:

| Date | CoralTemp minus HadSST4.2, 30S-30N | minus ERSSTv5, 30S-30N | minus buoys (median, 95% interval) | Daily date from buoys | Probable cause (not proven) |
|---|---|---|---|---|---|
| 1995-06-03 | -0.076 C | -0.033 C | -0.057 (-0.072 to -0.045) | 1995-06-03 | ATSR-2 data start in the OSTIA reanalysis |
| 2002-07-24 | +0.103 C | +0.098 C | +0.075 (+0.065 to +0.092) | 2002-07-24 | AATSR data start in the OSTIA reanalysis |
| 2008-01-01 | +0.072 C | +0.071 C | +0.056 (+0.046 to +0.067) | 2008-01-02 | Geo-Polar reanalysis changes its bias reference from OSTIA reanalysis to near-real-time OSTIA |
| 2020-11-04 | +0.053 C (sum of July and November 2020 terms; see R3) | +0.048 C (same sum) | +0.044 (+0.024 to +0.052) | 2020-11-04 to 2020-12-12 | Unknown; it is not the DOISST step of 7 July 2020 |

The 95% range of the same buoy statistic at placebo dates is -0.043 to +0.034 C. The documented product splice in November 2002 has no step relative to in situ SST (+0.002 C and -0.007 C). The large step is on 24 July 2002, three months earlier, inside the OSTIA segment. Because of the steps, CoralTemp is about 0.1 C too cold from mid-1995 to mid-2002, relative to the years before and after. This cold period is inside the 1985-2012 baseline of the CRW climatology and includes the 1997-98 bleaching event.

**Consequences.** CoralTemp warms 0.033-0.040 C per decade faster than the in situ products in the tropics and in the 5-degree boxes with reefs (1985-2025). After we remove the four steps, the excess is -0.002 to +0.005 C per decade, also in cross-validation (fit to one in situ product, test against the other). At 1,763 reef cells, the step correction makes the CRW maximum of monthly mean climatology (MMM) 0.14 C warmer relative to the current level (5-95% of cells: 0.02 to 0.24 C). This decreases the 1986-2025 trend of the reef-mean annual maximum DHW from +1.12 to +0.78 C-weeks per decade (-30%; all variants -27% to -32%). It decreases the trend of the reef fraction with DHW of 4 C-weeks or more from +10.8 to +7.5% per decade, and in 2024 this fraction from 82.5% to 62.3% (variants 61.7% to 67.2%). The increase of reef heat stress stays positive and large in all versions. 2024 stays the year with the highest heat stress.

## Main results

**R1. CoralTemp warms faster than in situ SST, in steps (Figure 1).** The 1985-2025 trend of CoralTemp minus HadSST4.2 is +0.033 C per decade (95% interval +0.016 to +0.050) at 30S-30N and +0.039 (+0.022 to +0.057) in reef boxes. Against ERSSTv5 it is +0.036 (+0.028 to +0.044) and +0.036 (+0.024 to +0.048). For comparison, DOISST v2.1 minus the same references is +0.050 to +0.059 C per decade. The difference series is not a linear drift. It has a cold period from mid-1995 to mid-2002 and steps up in 2002, 2008 and late 2020. A blind change-point search (binary segmentation with an AR(1) surrogate test) on monthly CoralTemp minus HadSST4.2, ERSSTv5 and DOISST found breaks within two months of 1995-06 in 10 of 12 CoralTemp difference series (3 references x 4 regions), of 2002-08 in 11 of 12 and of 2008-01 in 10 of 12. Late 2020 (4 of 12) and 2013-11 (4 of 12) were less consistent.

**R2. The steps are sharp and dated to the day (Figure 2).** In the daily CoralTemp minus DOISST difference (30S-30N), the largest break of the full record is on 2002-07-25 (+0.148 C; z = 4.3). Other breaks are on 1995-06-03 (-0.103 C) and on 2008-01-01 (+0.072 C). The median difference against the mooring network gives the same days: 1995-06-03 (-0.084 C, z = 8.7), 2002-07-24 (+0.077 C, z = 9.2) and 2008-01-02 (+0.048 C, z = 7.9). DOISST minus buoys has no step on these days.

**R3. The 2020 CoralTemp step is a different event from the DOISST step of 7 July 2020.** Daily CoralTemp minus DOISST (60S-60N) falls by 0.06 C on 2020-07-08, when DOISST steps up. The difference rises again by about 0.05 C in November-December 2020, when CoralTemp steps up. Against the buoys, the best date of the CoralTemp step is 2020-11-04 (+0.049 C, z = 8.0); a second scan gives 2020-12-12. Thus two independent satellite analyses warmed relative to the moorings within five months in 2020. Monthly in situ products cannot separate the two dates.

**R4. Other candidate dates are not supported by all references.** We tested 1988-11 (NOAA-11), 2001-02, the documented November 2002 splice, 2013-11 and the documented October 2016 change to near-real-time data. The in situ products give a 2013-11 step of -0.02 to -0.08 C (largest in the reef boxes), but the buoys give +0.004 C (-0.009 to +0.016). For 2016-10 the reef boxes give +0.05 to +0.07 C, but the buoys give -0.037 C. For 1988-11 HadSST4.2 and ERSSTv5 disagree. We use these dates only in the sensitivity variants ("six dates" and "all ten dates").

**R5. A correction with four dates removes the excess warming (Figure 3).** We fitted the four step sizes in every 5-degree box against HadSST4.2 and against ERSSTv5, smoothed them with a 1,000-km Gaussian kernel and took the mean of the two fields. The reef-mean steps are -0.070, +0.098, +0.032 and +0.056 C. After correction, the 1985-2025 trend of CoralTemp minus the references is -0.000 to +0.005 C per decade (30S-30N and reef boxes). The cross-validated values (fit to one reference, test against the other) are -0.002 to +0.004 C per decade. At the buoys, the corrected CoralTemp has no step at 2002-07-24 (-0.006 C), 2002-11-15 (-0.003 C), 2008-01-01 (-0.001 C) or 2020-07-07 (+0.015 C, not significant). At 1995-06-03 the correction is slightly too large (+0.027 C, 0.005 to 0.044), and at 2020-11-04 it is slightly too small (+0.027 C, 0.009 to 0.045).

**R6. CoralTemp has smaller fast-variance changes than DOISST (Figure 5).** Relative to the buoys, the median ln ratio of the variance of 1-day changes was -0.07 (1985-1994), -0.01 (1995-2001), +0.03 (2003-2007), +0.22 (2008-2016), +0.01 (2017-2019) and -0.20 (2021-2025). DOISST gave +0.11, +0.58, +0.41, +0.18, +0.04 and -0.80. Relative to DOISST, CoralTemp fast variance also changes on the same step dates. The mean steps are the main CoralTemp problem for DHW. We did not homogenise fast variance.

**R7. The steps change the reef heat-stress record (Figure 4).** At the 1,763 reef cells (0.25-degree cells at the sites of a global bleaching database), we calculated CRW statistics with the CRW method. Our MMM from raw CoralTemp agrees with the official CRW v3.1 MMM to 0.003 C (RMS over cells). The table gives reef-mean values. "Official" uses raw CoralTemp and the official CRW MMM. "Corrected" uses CoralTemp with the four steps removed and its own MMM. The intervals are 3-year moving-block bootstrap intervals.

| Statistic | Official | Corrected (4 dates) | Range of 5 variants |
|---|---|---|---|
| Reef SST trend, 1986-2025 (C per decade) | +0.217 | +0.179 | +0.178 to +0.182 |
| Annual maximum DHW trend (C-weeks per decade) | +1.12 (0.44 to 1.73) | +0.78 (0.25 to 1.26) | +0.76 to +0.82 |
| Annual accumulated DHW trend (C-weeks per decade) | +1.22 | +0.82 | +0.80 to +0.87 |
| Trend of reef fraction with DHW >= 4 (% per decade) | +10.8 (5.3 to 15.5) | +7.5 (3.1 to 11.4) | +7.4 to +7.7 |
| Trend of reef fraction with DHW >= 8 (% per decade) | +5.7 | +4.2 | +4.0 to +4.3 |
| 1998: reef fraction with DHW >= 4 | 24.8% | 28.7% | 27.5% to 30.3% |
| 2016: reef fraction with DHW >= 4 | 47.4% | 34.8% | 32.4% to 42.2% |
| 2024: reef-mean annual maximum DHW (C-weeks) | 9.66 | 7.56 | 7.49 to 8.08 |
| 2024: reef fraction with DHW >= 4 | 82.5% | 62.3% | 61.7% to 67.2% |
| 2024: reef fraction with DHW >= 8 | 51.0% | 37.0% | 36.6% to 39.6% |
| 2017-2025 mean reef fraction with DHW >= 4 | 37.6% | 27.6% | 27.4% to 28.4% |

The variants are: steps fitted only to HadSST4.2 or only to ERSSTv5, three dates (without 2020), six dates (with 2013-11 and 2016-10) and ten dates (all candidates). The corrected record has more heat stress in 1996-2002 and less heat stress after 2002. The difference increases to -1.5 to -2.1 C-weeks of annual maximum DHW in 2023-2025 (Figure 4c). The cause is the baseline: the 1985-2012 MMM period includes the seven too-cold years, and the record after 2002 is up to 0.19 C too warm relative to these years. Thus the official product gives too high HotSpots after 2002.

**R8. The bleaching surveys do not confirm the correction.** We compared the maximum DHW in the 90 days before each of 34,492 surveys of the global bleaching database (1,568 reef cells, 1985-2020) with the observed bleaching. The area under the ROC curve (AUC) for bleaching of 10% or more was 0.724 with the official product and 0.715 with the corrected product (difference -0.009; cluster-bootstrap 95% interval -0.018 to -0.001). For any bleaching it was -0.010 (-0.018 to -0.002). DOISST gave 0.738. The median DHW of bleached surveys decreases from 1985-2002 to 2017-2020 in all products (official 2.3 to 1.8, corrected 2.3 to 0.3, DOISST 4.8 to 1.0 C-weeks). Thus this database cannot calibrate absolute DHW levels across eras. Survey effort and selection changed strongly (most 1985-2002 records come from reports of bleaching events). The small AUC decrease is a real result of this test. It does not show which SST level is correct at the reefs.

## Interpretation

The CRW heat-stress products are not homogeneous in time. The four steps put a cold period of about 0.1 C into 1995-2002, inside the climatology baseline, and make the record after 2008 warmer. The probable causes are changes of the reference satellite in the OSTIA reanalysis (ATSR-2 in June 1995 and AATSR in July 2002, which OSTIA uses for bias correction) and the change of the bias reference in the Geo-Polar reanalysis on 1 January 2008. The documented product splices (November 2002 and October 2016) are not the main problem. The cause of the November 2020 step is unknown.

DHW is very sensitive to a small offset between the baseline and the current SST, because it counts only HotSpots of 1 C or more. An offset of 0.1-0.2 C changes the area with DHW of 4 C-weeks or more by up to 20 percentage points in a strong year. The official CoralTemp product thus overstates the increase of bleaching-level heat stress at reefs by about 30%, and the extent of the 2024 heat stress by about one quarter. Bleaching-level heat stress still increased strongly: the corrected trends are positive with intervals above zero, and 2024 stays the year of maximum heat stress.

These results agree in sign with the Caribbean result of Margaritis et al. (2025) and they explain it: the excess warming is a staircase of satellite-reference steps. The effect is opposite in sign to the DOISST fast-variance bias of DHW trends (sci:sha256:ef9c2a57...), which made DOISST DHW trends 11-16% too low. Both CoralTemp and DOISST warm faster than the in situ products (by 0.03-0.04 and 0.05-0.06 C per decade at reefs).

## Figures

- `files/figures/fig1_coraltemp_minus_insitu.png`: monthly CoralTemp minus HadSST4.2 and ERSSTv5 (DOISST minus HadSST4.2 for context), 30S-30N and reef boxes, with the four step dates.
- `files/figures/fig2_daily_dating_buoys.png`: (a) daily CoralTemp minus DOISST around the four dates; (b) median steps relative to moored buoys for raw CoralTemp, corrected CoralTemp and DOISST at ten test dates, with the placebo range.
- `files/figures/fig3_step_fields.png`: smoothed 5-degree fields of the four steps, with reef cells.
- `files/figures/fig4_reef_heat_stress.png`: reef-mean annual maximum DHW and reef fraction with DHW >= 4, official and corrected; their difference by year; trends of all variants relative to the official trend.
- `files/figures/fig5_fast_variance.png`: day-to-day variance of CoralTemp relative to DOISST and to the buoys.

## Methods

**CoralTemp.** We downloaded all 14,975 daily files `coraltemp_v3.1_YYYYMMDD.nc` for 1985-01-01 to 2025-12-31 from three NOAA servers that have identical files (STAR, CoastWatch, NCEI). For each day we kept compact extracts and deleted the file: the mean of the valid 0.05-degree pixels in each 0.25-degree reef cell (5 x 5 pixels), 5 x 5 windows at the moorings, 1-degree block means at 60S-60N with pixel counts, one 0.25-degree sample cell per 1-degree cell, and the ice-pixel count. The SHA-256 of every file is in `files/provenance/coraltemp_files_sha256.csv.gz`.

**References.** DOISST v2.1 (NOAA PSL daily files, shared campaign store). HadSST4.2.0.0 median (anomalies, 5 degrees). ERSSTv5 (2 degrees, averaged into 5-degree boxes). Moored buoys: the archived daily SST of 211 GTMBA and NDBC moorings from sci:sha256:87b87a67... (198 with matched data; 1,371,404 matched buoy-days, 1985-2025). Reef cells: the 1,763 DOISST reef pixels of sci:sha256:ef9c2a57... (BCO-DMO dataset 773466 sites).

**Monthly comparison.** We used 1-degree cells that have at least 50% valid CoralTemp pixels and no CoralTemp ice pixel on any day, and DOISST in the same cells (27,973 cells). We averaged them into 5-degree boxes (area weights), took CoralTemp minus each reference, removed the calendar-month mean, and averaged boxes with valid values in at least 80% of months. Regions: 60S-60N, 30S-30N, 30-60 degrees, and boxes that contain reef cells.

**Change points.** Blind search: binary segmentation; a break is kept if its reduction of the residual sum of squares is larger than the 95% quantile in 400 AR(1) surrogate series with the residual AR(1) parameters. Fixed dates: one OLS model with steps at all ten candidate dates (DOISST input-change dates from sci:sha256:645d0681... as nuisance steps for CoralTemp minus DOISST), Newey-West standard errors (24 lags), and a placebo test that moves each date to every month that is at least 18 months from all candidate dates. Daily dating: a two-window scan (90 days each side) on daily CoralTemp minus DOISST, and a 120-day scan on the daily median of the deseasonalised product-minus-buoy differences.

**Buoy step test.** For each buoy and date: mean difference (product minus buoy, deseasonalised per buoy) in the 2 years after minus the 2 years before; at least 180 matched days on each side. Median over buoys, bootstrap interval over buoys, and the same statistic at 84 placebo dates (1st of January, April, July and October, more than one year from all test dates). A 1-year window gives the same results (`files/results/buoy_steps_W365.json`).

**Correction.** In each 5-degree box with at least 80% valid months, we fitted CoralTemp minus reference = a + sum of h_k S_k(t), with S_k a step at date k. We smoothed the box estimates with a Gaussian kernel (L = 1,000 km) and weights area / se^2, and interpolated them bilinearly to the reef cells. The corrected series is CoralTemp - sum of h_k (S_k(t) - 1): the correction is zero after the last step. DHW does not change if a constant is added to a record, so the choice of the reference level has no effect on DHW.

**Heat stress.** CRW v3.1 method (Skirving et al. 2020), with code from sci:sha256:ef9c2a57...: monthly means of 1985-2012 regressed on year and evaluated at 1988.2857; MMM = maximum of the 12 values; HotSpot = SST - MMM; DHW = sum over 84 days of HotSpots of 1 C or more, divided by 7. We used the 0.25-degree cell mean of CoralTemp. Statistics per cell and calendar year; trends for 1986-2025 (1985 has no complete 84-day window in January-March).

## Limitations

- The references are not the truth. HadSST4.2 and ERSSTv5 share ship and drifter data, and the buoys are inputs of all products. Moorings are in the open tropical ocean and on United States coasts, not at reefs. The two in situ products give different step sizes (for example -0.076 and -0.033 C at 1995-06 in the tropics). The variants show the effect of this choice.
- The causes in the table are probable, not proven. We did not use the source data of OSTIA or Geo-Polar Blended. The cause of the November 2020 step is unknown.
- In situ products and buoys disagree about 2013-11 and 2016-10. If these steps are real at reefs, the "six dates" variant applies; its DHW results are almost the same as the main variant.
- The correction is smooth at 1,000 km. Local steps near coasts and reefs can be different. We did not test against reef temperature loggers.
- We did not homogenise fast (day-to-day) variance. CoralTemp variance changes are smaller than those of DOISST, but they can change DHW by some percent.
- The bleaching database does not support the correction (R8). We think that the database cannot test absolute SST levels across eras, but this is an interpretation.
- Reef cells are unweighted 0.25-degree cells at survey sites, not the full CRW 5-km reef mask. We did not reproduce the official CRW DHW files, only the method and the official MMM.
- Intervals are approximate (HAC and block bootstrap on 40 annual values with strong ENSO variability).

## Reproduction

`files/code/run_all.sh` runs all steps from a work directory. It needs Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib, the shared campaign dataset store, and the unzipped prior bundles sci:sha256:ef9c2a57... and sci:sha256:87b87a67... . The CoralTemp download transfers about 120 GB and takes 3-8 hours; the downloader skips days that it has already reduced and writes only to `scratch/`. The DOISST extraction takes about 30 minutes and the analysis about 1 hour. `files/code/oi_reef_fix.py` repaired a longitude error in an early version of `oi_extract.py`; the current `oi_extract.py` is correct and the repair is not necessary in a new run. The configurations are in `files/config/`.

To inspect the results without downloads, use `files/results/`:
- `monthly_diff_series.csv`: monthly CoralTemp minus HadSST4.2, ERSSTv5 and DOISST (and DOISST minus in situ), by region.
- `daily_ct_minus_doisst.csv.gz`: daily CoralTemp minus DOISST, by region.
- `blind_breaks.json`, `stepfit.json`, `daily_breaks.json`, `buoy_steps.json`, `buoy_steps_W365.json`, `buoy_daily_dating.json`: change-point results.
- `step_fields_<variant>.npz`, `step_fields_summary_<variant>.json`: 5-degree step fields (raw box fits with standard errors and smoothed fields) for the variants main, core3, six and all.
- `validation.json`: trends of corrected CoralTemp minus the references, with cross-validation.
- `reef_dhw.json`, `reef_dhw_annual.csv`: reef heat-stress statistics for all versions.
- `daily_fastvar.csv.gz`, `buoy_fastvar_years.csv`: fast-variance diagnostics.
- `bleach_auc.json`: bleaching-survey test (aggregate values only).

## Data and terms

The bundle contains no CoralTemp, DOISST, HadSST or ERSST values. It contains only our differences, aggregates, statistics and figures. See `files/NOTICE_external_data.md` for sources, versions, licences and attribution. Exact paths, URLs and SHA-256 hashes are in `files/provenance/data_provenance.json`.

## Provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-1f9bcbb3ee8f. Topic earth-and-ocean-sciences. Machine dell. Account claude-sci. Model Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. Dates 2026-11-10 to 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## References

- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch Coral Bleaching Heat Stress Product Suite Version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- Margaritis, G., Kent, E. C. and Foster, G. L. (2025). Intercomparison of satellite-derived SST with logger data in the Caribbean: implications for coral reef monitoring. PLOS Climate. doi:10.1371/journal.pclm.0000480
- Donlon, C. J. et al. (2012). The Operational Sea Surface Temperature and Sea Ice Analysis (OSTIA) system. Remote Sensing of Environment 116, 140-158. doi:10.1016/j.rse.2010.10.017
- Roberts-Jones, J., Fiedler, E. K. and Martin, M. J. (2012). Daily, global, high-resolution SST and sea ice reanalysis for 1985-2007 using the OSTIA system. Journal of Climate 25, 6215-6232. doi:10.1175/JCLI-D-11-00648.1
- Kennedy, J. J. et al. (2019). An ensemble data set of sea surface temperature change from 1850: the Met Office Hadley Centre HadSST.4.0.0.0 data set. JGR Atmospheres 124, 7719-7763. doi:10.1029/2018JD029867
- Huang, B. et al. (2017). Extended Reconstructed Sea Surface Temperature, version 5 (ERSSTv5). Journal of Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- van Woesik, R. and Kratochwill, C. (2022). A global coral-bleaching database, 1980-2020. Scientific Data 9, 20. doi:10.1038/s41597-022-01121-y
