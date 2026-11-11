# CoralTemp v3.1 has undocumented SST steps in June 1995 and July 2002; they make the 1998 bleaching-level heat-stress extent too small and the escalation to 2023-2025 too large

**Job:** sci-1107-hp-earth-and-ocean-sciences-c286284bfd37 · **Topic:** earth-and-ocean-sciences · **Campaign:** 11_07_2026 · **Machine:** hp · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-sci · **Signing key:** campaign-machine key (not a personal authorship claim) · **Date:** 2026-11-11

## Summary

**Question.** Earlier campaign studies found step artifacts in the daily SST products that marine climate statistics use: NOAA DOISST v2.1 and ERA5. One study also found that DOISST noise steps bias coral Degree Heating Week (DHW) trends. None tested the record that the official coral heat-stress products use. NOAA Coral Reef Watch (CRW) v3.1 computes HotSpots, DHW and Bleaching Alerts from CoralTemp. CoralTemp joins three sources: the Met Office OSTIA reanalysis (1985 to 2002), the NOAA Geo-Polar Blended (GPB) reanalysis (2002 to 2016) and the GPB near-real-time analysis (from October 2016). The CRW bleaching threshold (MMM) comes from 1985-2012 monthly means. CRW re-centres these means to 1988.29 with a fitted linear trend. Thus a step anywhere in 1985-2012 goes into every HotSpot through the trend. We asked three questions. Is CoralTemp homogeneous at reefs? Do steps go into the MMM? Which published heat-stress results change?

**Approach.** We used CoralTemp monthly mean SST (ERDDAP) on a 1-degree point grid at 35S-35N. The grid has 18,572 ocean points and 574 one-degree cells with sites from a global coral-bleaching database. We compared it with four references of two types: DOISST v2.1 (satellite plus in situ), ERSSTv5, COBE-SST2 and HadSST4.2 (in situ only). We tested steps with 24-month windows and placebo dates, a blind break search and joint fits with autocorrelation-robust errors. We used daily CoralTemp at 60 reef cells in six windows (about 525 point-years) to find the step days. We re-emulated the CRW climatology. It matches the official MMM to a median of 0.00001 C (90% within +/-0.005 C). We then removed the steps and re-computed the MMM. We computed DHW with daily CoralTemp at the 60 cells, and with a hybrid daily record at 559 reef cells for 1985-2025. The hybrid uses CoralTemp monthly means and DOISST daily detail.

**Results.**

1. CoralTemp has two large steps inside the OSTIA reanalysis segment that CRW does not document. Relative to all four references at reef cells, it cools by 0.086-0.124 C in mid-1995 (mean -0.105 C, placebo z -7.1) and warms by 0.074-0.099 C in mid-2002 (mean +0.088 C, z +5.4). Daily data place the steps on 4 June 1995 (-0.10 C, 95% CI -0.19 to -0.003) and 15 July 2002 (+0.12 C, 95% CI +0.06 to +0.19). These dates agree with the start of ATSR-2 SST (31 May 1995) and with the start of the ATSR-2/AATSR overlap (July 2002). The OSTIA reanalysis uses these sensors as its bias reference. The 1995 step is an Indo-Pacific feature (-0.130 C; Atlantic-Caribbean -0.007 C). DOISST has no step on these dates relative to the in situ products (|z| <= 1.2).
2. The documented merge to near-real-time (October 2016) is not clear. The step is +0.04 to +0.10 C at reef cells, but -0.001 C over 35S-35N and -0.03 C (not significant) in daily data. Smaller steps occur near January 2008 (+0.04 C) and August 2014 (-0.05 C), mainly in the Atlantic-Caribbean.
3. The 1995 and 2002 steps mostly cancel in the Indo-Pacific MMM. With both steps removed (primary variant, basin-uniform steps, mean of four references), operational HotSpots are 0.10 C too low at Indo-Pacific reefs from June 1995 to July 2002 (four references: -0.08 to -0.11 C). They are 0.12 C too high at Atlantic-Caribbean reefs after July 2002 (+0.08 to +0.20 C). Elsewhere and at other times the mean bias is at most 0.03 C.
4. Consequences for published results. The share of reef cells with bleaching-level heat stress (DHW >= 4) in 1998 increases from 33.6% to 42.5% (four references: 40.4-45.3%) in the hybrid record. In exact daily CoralTemp at 58 cells it increases from 22.4% to 27.6-29.3%. The 2010, 2014-2017 and 2023-2025 extents change by -2 to +2 points. Thus the ratio of the 2023-2025 extent to the 1998 extent falls from 2.7 to 2.1 (2.0-2.2 in the sensitivity runs). 2023-2025 stays the largest event in all variants (80-92%). The 1985-2025 trend of annual maximum DHW (+1.10 C-weeks per decade) falls by 1-4% when only the two robust steps are removed. It falls by 19-20% when the uncertain 2016 step (or all five steps) is also removed.

**Conclusion.** The CRW product suite is not homogeneous at its OSTIA-reanalysis segment. The fixed-trend re-centring of the MMM carries the 1995 and 2002 steps into HotSpots of all later years. For the Indo-Pacific the two errors cancel after 2002. But the 1998 global bleaching event is too weak by about 0.1 C of HotSpot. For the Caribbean, the HotSpots of all years after July 2002 are about 0.1 C too high. The escalation from the first to the fourth global bleaching event remains, but it is about one fifth smaller in extent ratio than the operational record shows.

## Figures

- `files/figures/fig1_steps_in_time.png`: CoralTemp minus four references at reef cells, 1985-2025, and daily CoralTemp minus DOISST around the 1995, 2002 and 2016 changes.
- `files/figures/fig2_basin_steps_hotspot_bias.png`: step sizes by basin and reference, and the operational-minus-homogenised HotSpot bias by period.
- `files/figures/fig3_dhw_consequences.png`: yearly share of reef cells at DHW >= 4 and the extents of the four global bleaching events, operational against homogenised.

## Data

| Material | Version and access | Use |
| --- | --- | --- |
| CoralTemp v3.1 monthly mean SST | ERDDAP `NOAA_DHW_monthly`, coastwatch.pfeg.noaa.gov, 1985-01 to 2026-10, accessed 2026-11-11 | 1-degree grid, 35S-35N (504 tile requests) |
| CoralTemp v3.1 daily SST and DHW | ERDDAP `dhw_5km`, PacIOOS, accessed 2026-11-11 | 60 reef cells, windows 1995, 1997-10 to 1998, 2002-05 to 2003-04, 2009-10 to 2010, 2016-04 to 2017-03, 2022-10 to 2025 |
| CRW v3.1 climatology (MMM) | NOAA STAR `ct5km_climatology_v3.1.nc`, SHA-256 c49dd890...e875c4 | validation of the MMM emulation |
| DOISST v2.1 daily | NOAA PSL, shared campaign copies 1982-2025 | reference, hybrid daily detail |
| ERSSTv5, COBE-SST2 | NOAA PSL, shared campaign copies | in situ references |
| HadSST.4.2.0.0 median | Met Office, shared campaign copy | in situ reference |
| Coral bleaching database v2 | BCO-DMO 773466 (van Woesik and Kratochwill 2022), shared copy | site coordinates only |

Exact paths, source URLs and SHA-256 hashes are in `files/provenance/`. `files/NOTICE-external-data.md` gives the terms. The OSTIA part of CoralTemp (1985-2002) has academic-use-only Met Office terms. For this reason the bundle has no CoralTemp values, no per-pixel or per-cell series and no per-cell fields. It has only aggregate statistics over many points, test statistics and figures of these aggregates.

## Methods

**Sample grid.** We used the CoralTemp 0.05-degree pixel centres that are also DOISST 0.25-degree pixel centres, at 1-degree spacing (lat 34.875 to -34.125, lon -179.875 to 179.125). A reef cell is a 1-degree cell that contains at least one of the 12,323 unique site coordinates of the bleaching database. We used the grid point of each reef cell. This point is in open water within about 70 km of the reef, not on the reef pixel.

**References and differences.** For each grid point and each reference, we took CoralTemp minus the reference value of the same month (ERSSTv5 2 degrees, COBE-SST2 1 degree, HadSST4.2 5 degrees, DOISST monthly mean of daily values). We removed the mean seasonal cycle of the difference. We made area-weighted (cos latitude) mean series for 35S-35N, reef cells, Indo-Pacific and Atlantic-Caribbean reef cells, 15S-15N and 15-35 degrees. "refmean" is CoralTemp minus the mean of the four deseasonalised references.

**Step tests.** A window step is the mean of 24 months after a change minus the mean of 24 months before it. The month of the change is excluded. Placebo z-scores and empirical p-values use the same statistic at all other dates, with windows that contain a tested date excluded. We also fitted all five steps together with Newey-West errors (12 lags), and we used binary segmentation for a blind search. As a check, DOISST minus each in situ reference must show the published DOISST steps (January 2005, July 2020) and no step at the CoralTemp dates (`results/positive_control_doisst.txt`).

**Daily step days.** At 60 reef-cell points (farthest-point sample of reef cells), daily CoralTemp minus DOISST on the same pixel centre gave a multi-point mean. One least-squares break per window gave the step day. A point bootstrap gave its range and the step size (mean of days 5-65 after minus days 5-65 before). We also compared day-to-day variance and sub-monthly variance (deviation from a 31-day running mean) of CoralTemp relative to DOISST before and after each change.

**CRW emulation.** For each calendar month we fitted the 1985-2012 monthly means against year and evaluated the fit at 1988.2857. MMM is the maximum of the 12 values. HotSpot = SST - MMM. DHW is the sum over the last 84 days of HotSpots >= 1 C, divided by 7. At 9 points we compared our DHW (official MMM, daily CoralTemp) with the operational CRW DHW for 2023-2025. The mean absolute difference was 0.00-0.04 C-weeks (largest single-day difference 0.85 C-weeks).

**Homogenisation.** For each reference and step date, the step is the window step of the basin reef-cell mean series (Indo-Pacific; Atlantic-Caribbean = 100W-20W without the Pacific coast of Central America). We added the steps to all earlier months, so that every segment has the near-real-time level. The month of a change has half the step. A constant offset of the whole record does not change DHW, so only relative steps are important. We then re-emulated the MMM. The operational-minus-homogenised HotSpot on a day is the MMM change minus the shift of that day. Variants: V1 (2002 only), V2 (1995 and 2002, primary), V3 (V2 and 2016), V4 (all five dates). Sensitivity: 10x30-degree box steps instead of basin steps, and 36-month windows.

**Placebo homogenisation.** We repeated the box-step homogenisation 40 times with two random placebo dates in step-free periods (1987-1993 and 1997-2000). The placebo reef-mean steps were at most 0.025 C (95th percentile of the absolute value). The box-to-box spread was 0.06-0.09 C, the same as the spread of the real box steps (0.075-0.086 C). Thus box-level regional structure is noise. For this reason the primary variant uses basin-uniform steps.

**DHW.** (a) Exact: daily CoralTemp at the 60 points for 1998 (from October 1997), 2010 (from October 2009) and 2023-2025 (from October 2022), with official MMM (operational) and with MMM plus the HotSpot bias of the point (homogenised). (b) Hybrid: for 559 reef cells with complete data, daily DOISST plus the linearly interpolated monthly CoralTemp-minus-DOISST difference. The monthly means of the hybrid equal CoralTemp. Correlation with exact daily CoralTemp is 0.95-0.98 and the RMSE is 0.27-0.42 C. Day-to-day variance follows DOISST, not CoralTemp. Event windows: 1998, 2010 (calendar years), June 2014 to May 2017, and January 2023 to June 2025.

## Results in detail

### Steps (reef cells, 24-month windows, CoralTemp minus reference, C)

| Date | DOISST | ERSSTv5 | HadSST4.2 | COBE-SST2 | refmean (z) | 35S-35N refmean (z) |
| --- | --- | --- | --- | --- | --- | --- |
| June 1995 | -0.108 | -0.086 | -0.092 | -0.124 | -0.105 (-7.1) | -0.087 (-6.0) |
| July 2002 | +0.083 | +0.074 | +0.099 | +0.094 | +0.088 (+5.4) | +0.069 (+4.0) |
| January 2008 | +0.037 | +0.049 | +0.038 | +0.042 | +0.040 (+2.3) | +0.055 (+3.2) |
| August 2014 | -0.061 | -0.059 | -0.061 | -0.031 | -0.055 (-3.9) | -0.046 (-3.4) |
| October 2016 | +0.043 | +0.055 | +0.099 | +0.085 | +0.071 (+4.3) | -0.001 (-0.5) |

By basin (refmean, z): 1995 Indo-Pacific -0.130 (-6.6), Atlantic-Caribbean -0.007 (-0.1); 2002 +0.083 (+3.7) and +0.107 (+3.2); 2008 +0.032 (+1.2) and +0.070 (+2.1); 2014 -0.042 (-2.4) and -0.104 (-3.0); 2016 +0.076 (+3.4) and +0.054 (+1.6). With 36-month windows: 1995 -0.101, 2002 +0.075, 2016 +0.081 (reef cells, refmean). Files: `results/splice_step_tests_W24.csv`, `results/splice_step_tests_W36.csv`, `results/basin_steps_W24.csv`, `results/blind_breaks.json`.

The blind search (five references, 35S-35N band and reef cells: ten series) found a break between March and June 1995 in all ten series and a break in August 2002 in seven of ten. It also found a break in January or February 2008 in seven of ten.

### Daily step days (58 points with complete data)

| Change | Break day (bootstrap 90%) | Step, C (95% CI) | Largest placebo | Sub-monthly variance, CT/DOISST after/before |
| --- | --- | --- | --- | --- |
| 1995 | 1995-06-04 (03-21 to 08-15) | -0.097 (-0.189 to -0.003) | 0.12 | x0.53 (83% of points lower) |
| 2002 | 2002-07-15 (07-04 to 09-25) | +0.124 (+0.065 to +0.187) | 0.08 | x1.05 (no change) |
| 2016 | 2016-08-31 (06-21 to 2017-01-08) | -0.033 (-0.085 to +0.021) | 0.04 | x0.99 (no change) |

The day-to-day variance of CoralTemp increases 1.85-fold relative to DOISST from mid-November 2002, when GPB replaces OSTIA. Weekly-scale variance does not change at that date. File: `results/daily_splice_tests.json`, `results/daily_ct_minus_doisst_s*.csv`.

### HotSpot bias (operational minus homogenised, variant V2, C, reef-cell means)

| Basin | Before June 1995 | June 1995 to July 2002 | After July 2002 |
| --- | --- | --- | --- |
| Indo-Pacific (455 cells) | +0.025 (+0.022 to +0.027) | -0.103 (-0.084 to -0.114) | -0.020 (-0.041 to +0.018) |
| Atlantic-Caribbean (119 cells) | +0.014 (+0.008 to +0.022) | +0.012 (-0.028 to +0.072) | +0.118 (+0.078 to +0.197) |

Ranges are over the four references. With V1 (2002 only) the bias after July 2002 is about +0.10 C everywhere. With V3 and V4 the bias after October 2016 is +0.07 to +0.08 C. File: `results/mmm_homogenisation_basin_W24.json`.

### DHW consequences

Hybrid daily record, 559 reef cells. Event extent = share (cos-latitude weighted) of reef cells with DHW >= 4 at any day of the event window. Values in brackets: range over the four references. "op" is the operational CRW method (re-emulated); the other rows remove the steps of each variant.

| Variant | 1998 | 2010 | 2014-2017 | 2023-2025 | 2023-25 / 1998 | Trend of annual max DHW, C-weeks per decade |
| --- | --- | --- | --- | --- | --- | --- |
| op | 33.6% | 42.4% | 71.8% | 89.8% | 2.67 | +1.10 |
| V1 (2002 only) | 32.7% | 31.8% (29.9-33.6) | 55.2% (53.9-59.9) | 79.8% (77.4-84.2) | 2.44 | +0.80 (0.78-0.84) |
| **V2 (1995, 2002; primary)** | **42.5% (40.4-45.3)** | 41.7% (38.6-42.8) | 70.4% (66.9-72.0) | 91.2% (88.7-92.2) | **2.14** | +1.05 (0.99-1.08) |
| V2, 36-month windows | 42.4% (39.1-45.2) | 42.8% (39.9-44.4) | 71.1% (70.1-74.0) | 91.8% (90.3-93.8) | 2.17 | +1.09 (1.04-1.17) |
| V2, 10x30-degree box steps | 43.8% (41.2-47.2) | 41.0% (39.5-42.6) | 69.9% (66.7-71.3) | 88.8% (86.1-90.3) | 2.03 | +1.10 (1.06-1.14) |
| V3 (V2 and 2016) | 42.5% (40.4-45.3) | 41.7% (38.6-42.8) | 68.5% (64.7-69.8) | 85.1% (76.1-88.6) | 2.00 | +0.88 (0.77-0.98) |
| V4 (all five) | 42.0% (39.7-44.8) | 35.2% (34.2-37.0) | 69.0% (67.1-72.4) | 85.1% (78.0-89.8) | 2.03 | +0.89 (0.80-1.02) |

DHW >= 8 (severe) extents, V2 against op: 1998 9.5% against 6.5%; 2023-2025 63.6% against 62.1%.

Exact daily CoralTemp at 58 points (share with annual or event maximum DHW >= 4):

| Variant | 1998 | 2010 | 2023-2025 |
| --- | --- | --- | --- |
| op | 22.4% | 31.0% | 91.4% |
| V2 (primary) | 27.6% (27.6-29.3) | 29.3% (27.6-32.8) | 91.4% |
| V1 | 19.0% | 20.7% | 82.8% |
| V3 | 27.6% | 29.3% | 87.9% |
| V4 | 27.6% | 24.1% | 87.9% |

With V2, the median 1998 annual maximum DHW at the 58 points increases by 0.39 C-weeks; the median 2023-2025 maximum increases by 0.24 C-weeks. Variant V1 shows what a user would get if the user removed only the 2002 step: all post-2002 heat stress would fall by about one quarter. V1 is not supported, because the 1995 step is as large and as significant as the 2002 step. Files: `results/dhw_consequences_*.json`.

## Limitations

- The references have their own errors. DOISST, ERSSTv5, COBE-SST2 and HadSST4.2 share ships and buoys. The OSTIA reanalysis and the GPB bias correction also use in situ data. Steps that all references share would not be visible. DOISST shows no step at the CoralTemp dates, and the four references agree within 0.04 C.
- The grid points are in open water near reefs, not on reef pixels. The steps are large-scale, so we expect similar steps on reef pixels, but we did not test this.
- The bleaching-database sites are survey sites, not a census of reef area. Our extents (for example 33.6% in 1998 and 89.8% in 2023-2025 in the hybrid; 22.4% and 91.4% at the 58 exact points) differ from the NOAA values (21% and 84%), which use all CRW 5-km reef pixels. We report changes relative to our own operational emulation.
- The hybrid daily record has DOISST day-to-day variability, which has its own steps (2007, 2021). The operational-minus-homogenised difference uses the same hybrid, so these steps affect absolute DHW values more than the differences. The exact daily data at 58 points give the same direction for 1998.
- Box-level (10x30 degrees) step fields are not better than noise. Thus we cannot resolve regional step patterns finer than the two basins.
- The 2016 step is uncertain. The trend result depends on it (decrease of 1-4% without, 19-20% with), and so does the 2023-2025 extent (91% without, 85% with).
- The cause of the 1995 and 2002 steps is not proven. The dates agree with ATSR reference-sensor changes in the OSTIA reanalysis, but we did not have the OSTIA reanalysis inputs.
- We did not test whether homogenised DHW predicts observed bleaching better.

## Reproduction

1. Copy `files/code/` to a work folder `WORK/code`. Set `CT_WORK=WORK` and `CT_DATASETS` to a folder with the shared datasets (files and hashes in `files/provenance/shared_datasets_used.json`; source URLs are given there).
2. Accept the CoralTemp/OSTIA terms (`files/NOTICE-external-data.md`).
3. Run `bash WORK/code/run_all.sh`. It downloads about 0.14 GB of CoralTemp files into `WORK/scratch` (1-4 h, set by the ERDDAP servers) and writes about 3 GB of intermediates there and writes results to `WORK/result/files/`. The code refuses to write scratch data inside a publication folder.
4. `run_analysis.sh` repeats only the analysis when the scratch data exist.

Python 3.12 with numpy, pandas, netCDF4 and matplotlib. The downloaded files can differ if NOAA changes the products; `files/provenance/coraltemp_requests.json` has the SHA-256 of every file that we used.

## Relation to earlier campaign work

This study uses the CRW method emulation and DHW definitions of the DOISST reef study (sci:sha256:ef9c2a57a59e66e0e1ad07242f306973d558cd3485f8afb8ff466fb1fd47c074). That study found that noise steps make DOISST DHW trends too low, and that mean-warming differences between products are a larger uncertainty. Here we show that the record that CRW actually uses has its own mean steps, at other dates. Through the MMM re-centring, these steps change the heat stress of the first global bleaching event more than the recent trend. The DOISST mean-step studies (sci:sha256:b93b5f641725a35b93aae545fe514632c50f87c96781a135740caa4284434ab2, sci:sha256:9fca62cd8472d63d48b27ab8390b65ee3e06360adfbc14fea607fedf11a3e03a, sci:sha256:dbf0934148316f153a19c429cf19908a4e4e213a22aa2decfe119df5dbcacb4b) found steps in 1985, 2005 and 2020 in DOISST. We used these dates as known reference artifacts.

## References

- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch coral bleaching heat stress product suite version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- Liu, G. et al. (2014). Reef-scale thermal stress monitoring of coral ecosystems: new 5-km global products from NOAA Coral Reef Watch. Remote Sensing 6, 11579. doi:10.3390/rs61111579
- Roberts-Jones, J., Fiedler, E. K. and Martin, M. J. (2012). Daily, global, high-resolution SST and sea ice reanalysis for 1985-2007 using the OSTIA system. Journal of Climate 25, 6215. doi:10.1175/JCLI-D-11-00648.1
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation SST (DOISST) version 2.1. Journal of Climate 34, 2923. doi:10.1175/JCLI-D-20-0166.1
- Huang, B. et al. (2017). ERSSTv5. Journal of Climate 30, 8179. doi:10.1175/JCLI-D-16-0836.1
- Hirahara, S., Ishii, M. and Fukuda, Y. (2014). COBE-SST2. Journal of Climate 27, 57. doi:10.1175/JCLI-D-12-00837.1
- Kennedy, J. J. et al. (2019). HadSST.4.0.0.0. JGR Atmospheres 124, 7719. doi:10.1029/2018JD029867
- van Woesik, R. and Kratochwill, C. (2022). A global coral-bleaching database, 1980-2020. Scientific Data 9, 20. doi:10.1038/s41597-022-01121-y
- ATSR-2 L2P SST record (CEDA), data from 1995-05-31: https://csw.ceda.ac.uk/geonetwork/srv/api/records/97e5db7e92ded2f321405041a7d5513f
- CMEMS OSTIA reanalysis QUID (ATSR-2/AATSR overlap July 2002 to June 2003): https://catalogue.marine.copernicus.eu/documents/QUID/CMEMS-SST-QUID-010-011.pdf
- NOAA global bleaching event extents (21%, 37%, 68%, 84%) as reported, for example, in https://www.scientificamerican.com/article/worst-coral-mass-bleaching-on-record-caused-by-warming-oceans/
