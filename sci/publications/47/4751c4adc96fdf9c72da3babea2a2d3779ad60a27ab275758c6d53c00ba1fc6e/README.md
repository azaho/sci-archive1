# The 1 January 2005 DOISST v2.1 warm step (+0.07 C, 60S-60N) is not from its sea-ice input or a sudden Pathfinder input change; it forms in the analysis as ICOADS input became real-time data

## Summary

**Question.** NOAA Daily OISST v2.1 (DOISST) has a warm step of about +0.07 C at 60S-60N on 1 January 2005. Earlier campaign work found this step against ESA CCI, HadSST4, ERSSTv5, Argo and moored buoys (sci:sha256:b93b5f64), and it is one of the three main steps that make DOISST warm 0.03-0.05 C per decade too fast. NOAA documents one input change on that date: the sea-ice input changed from NASA GSFC to NCEP. But the step also occurs in the tropics, so earlier work wrote that "a change in the large-scale satellite bias correction is likely, and another unlisted change on that date is possible". We tested three candidate causes: (A) the Pathfinder AVHRR satellite input, (B) the sea-ice input, and (C) the in situ input.

**New documentary fact.** DOISST used ICOADS Release 2.4 as its in situ input for 1981-2006 (Banzon et al. 2016, Table 1). ICOADS Release 2.4 took its data for 1784-2004 from the delayed-mode archive (ICOADS.DM) and its data for 2005-May 2007 from the real-time GTS archive (ICOADS.RT, converted from NCEP BUFR) (Woodruff et al. 2011). Thus the DOISST in situ input also changed type on 1 January 2005. The DOISST input tables do not show this change.

**Approach.** We binned the archived Pathfinder v5.0 4 km files (NCEI; monthly 2003-2006, daily 1 December to 31 January around 1 January 2004, 2005 and 2006) to the DOISST grid. We matched 5.5 million ICOADS R3.0.0 ship, drifter and moored-buoy cell-days (5.3 million at 60S-60N) to DOISST. We then measured: (1) the 1 January step of DOISST minus CCI for every year 1983-2024; (2) monthly steps of DOISST, Pathfinder and DOISST minus Pathfinder against ERSSTv5 and HadSST4 with placebo dates; (3) the change within one week of 1 January against moored and drifting buoys at the same cell-days; (4) a year-on-year test inside one Pathfinder processing run; (5) the step as a function of distance from DOISST ice.

**Results.**

1. **The 2005 step is unique among New Years.** DOISST minus CCI changes by +0.095 C at 60S-60N across 1 January 2005. This is rank 1 of 42 New Years from 1983 to 2024 (z = 3.7 against the other years; standard deviation 0.031 C). The mean profile of the other 40 years shows no New-Year transient. In the monthly model, the step at 2005-01 is +0.073 C against ERSSTv5 (95% interval 0.060 to 0.086) and +0.072 C against HadSST4 (0.060 to 0.085). The placebo New-Year steps of 2004 and 2006 are between -0.040 and -0.016 C.
2. **The sea-ice input is not the cause (B rejected for 60S-60N).** The NCEP ice from 2005 has no cells with 0-15% concentration (0.48% of cell-days in 2004, 0.0016% in 2005). But the DOISST minus ERSSTv5 step is zero within 500 km of DOISST ice (-0.004 C, -0.025 to +0.017). It is +0.046 C at 500-1000 km and largest more than 4000 km from ice (+0.078 C, 0.070 to 0.086). An ice cause would give the opposite pattern.
3. **The step does not start in the Pathfinder input (A rejected as the cause of the sudden step).** In the week after 1 January 2005, DOISST rises against ICOADS moored buoys at the same cell-days by +0.093 C (0.064 to 0.122) at day-matched cells and by +0.083 C (0.062 to 0.104) at night-matched cells. In the same week, Pathfinder does not change against the same buoys: -0.006 C (-0.032 to +0.020) by day and +0.013 C (-0.025 to +0.056) by night. DOISST minus Pathfinder rises by +0.114 C (day 0.092 to 0.135) more than 1000 km from ice. In monthly series, Pathfinder minus ERSSTv5 even falls from December 2004 to January 2005 (Figure 3).
4. **The step is made in the analysis, at all in situ platform types.** At monthly scale, DOISST rises on 1 January 2005 against ICOADS R3 ships (+0.063 C, 0.045 to 0.082), drifting buoys (+0.066 C, 0.033 to 0.099) and moored buoys (+0.017 C, 0.009 to 0.025) at their own cells. The 2004 placebo steps are -0.039, -0.004 and -0.003 C. Far from ice, DOISST minus Pathfinder carries the step (+0.064 to +0.072 C at night in box steps more than 1000 km from ice).
5. **A slower Pathfinder contribution is possible but not resolved.** Within one Pathfinder processing run (files made in November 2007, NOAA-17), Pathfinder minus ERSSTv5 is +0.044 C (0.014 to 0.073) warmer in January-May 2005 than in January-May 2004; DOISST minus ERSSTv5 is +0.062 C (0.037 to 0.086). This rise starts in February-March, not on 1 January. Pathfinder changes by similar amounts between other years (2003 against 2004). The monthly step model therefore gives Pathfinder +0.036 to +0.043 C and DOISST minus Pathfinder +0.030 to +0.035 C at 60S-60N, but the box-level estimator gives Pathfinder night about zero far from ice. We cannot separate a real input contribution from Pathfinder year-to-year drift with one year of the same processing.
6. **The archived Pathfinder "Version5.0" record is three processing runs.** The daily file histories show that the 2003 files were made in January 2005 (cloud-test reference from an interim "pfrt" path), the January 2004 to May 2005 files in November 2007, and the June 2005 to 2006 files in February-March 2009 ("pfv51", NOAA-18). The last run is after the DOISST v2 release (November 2008), so DOISST cannot have used those archived files. The NLSST coefficients change at each New Year (1 January 2004, 2005 and 2006); the 2005 change is not special.

**Conclusion.** The 1 January 2005 step is an artifact of the DOISST analysis, not a change in the ocean. It is not caused by the documented sea-ice input change: it is absent near ice and largest far from ice. It does not start in the Pathfinder satellite input: the input does not change in the week when DOISST rises. The step starts within one or two days of 1 January at all distances from ice and at the cells of ships, drifters and moorings. The only input change that we found on that date and that is not limited to ice regions is the change of the ICOADS in situ input from delayed-mode to real-time GTS data. The in situ data enter the DOISST analysis directly and through the large-scale satellite bias correction, which spreads in situ differences to regions with few observations; this agrees with the step being largest far from observations (sci:sha256:e75ccf52). We did not test the real-time data directly, because ICOADS Release 2.4 is no longer distributed. Thus cause C is the best remaining explanation, not a demonstrated one. The step correction of earlier campaign work (sci:sha256:645d0681, dbf09341, e2e438dd) is justified, but a homogenisation that is based on satellite inputs only will miss this step. Other products that used ICOADS Release 2.3 or 2.4 across 2005 can have a similar step.

## Context in the campaign

The campaign series on DOISST artifacts found noise steps (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 819eea65, 5d8902f2, 5003de8e, 4e3a13fa, ef9c2a57, 5d9b238d, 0d84af9c) and mean steps at input changes (sci:sha256:b93b5f64). The 7 July 2020 step was traced to the NAVO MetOp-A L2P v1.0-to-v2.0 change (sci:sha256:9fca62cd, 5cba350c). The 2005 step was the largest unexplained one; it is largest in the Southern Ocean and it affects the east-Pacific and 50-60S trend results (sci:sha256:9e1a3e72, 167ff86c). At drifter cells DOISST shows 58% of the open-ocean 2005 step, against 34% for the 2020 satellite step (sci:sha256:e75ccf52). The homogenised ensembles (sci:sha256:645d0681, dbf09341, e2e438dd) remove the 2005 step without a known cause. This study gives the cause most likely to be correct and rules out the documented one.

## Data

- **DOISST v2.1** daily SST (NOAA PSL yearly files 2003-2006, campaign shared store), the PSL monthly mean file, and the DOISST ice concentration files (PSL `icec.day.mean.YYYY.nc`, 2003-2006).
- **AVHRR Pathfinder v5.0** 4 km HDF4 files from NCEI: monthly SST and quality for 2003-2006 (day and night, NOAA-17 codes 2/4 to May 2005, NOAA-18 codes 1/3 after), and daily files for 1 December to 31 January around each New Year 2004, 2005 and 2006 (468 file pairs in total). Quality level 4 or more, at least 8 (monthly) or 3 (daily) 4 km pixels per 0.25-degree cell. The processing history of each daily file gives the processing date, cloud-test reference and NLSST coefficients.
- **ICOADS R3.0.0** individual reports (NCEI monthly netCDF, 2003-2006): SST with trimming flag SF = 1, platform types 0-5 (ships), 6 (drifting buoys), 7 (moored buoys). Super-observations per cell, day, platform group and ID; reports more than 3 C from DOISST were removed.
- **ERSSTv5** (2-degree monthly) and **HadSST.4.2.0.0** median (5-degree monthly anomalies) from the campaign shared store.
- **DOISST minus ESA CCI v3** daily regional series 1982-2024 from sci:sha256:b93b5f64 (`files/data/doisst_cci_daily_regional.csv.gz`).
- Documentation: Banzon et al. (2016) Table 1 (inputs), Reynolds et al. (2007), Reynolds (2009) "What's new in version 2", Woodruff et al. (2011) (ICOADS Release 2.4 composition).

## Methods

**Grids.** DOISST cells with ice > 0 on the day (daily) or in the month (monthly) were removed. Monthly fields were averaged to 2-degree boxes (DOISST minus Pathfinder), to the ERSSTv5 cells and to the HadSST4 5-degree boxes. DOISST was also sampled at the Pathfinder clear-sky cells ("DOISST at PF cells").

**Monthly step model.** For each region we took the cos-latitude weighted mean of box values after removal of the box mean for each calendar month (2003-2006). We fitted calendar-month effects plus step terms at 2005-01 and 2005-06 (Pathfinder NOAA-17 to NOAA-18) and, in the main model, placebo steps at 2004-01 and 2006-01. Intervals come from a moving-block bootstrap of residuals (3-month blocks, 2,000 draws). Box steps use the same model per box with at least 36 valid months.

**New-Year test.** For each year 1983-2024 we took the mean DOISST minus CCI of days 5 to 35 minus days -35 to -5 around 1 January.

**One-week test.** For each daily window we took the mean of days 0 to 6 minus days -7 to -1 of: DOISST minus Pathfinder (cell means, region-weighted), and DOISST or Pathfinder minus ICOADS drifting and moored buoys at the same cell-days. Intervals resample days (4,000 draws). The 2004 and 2006 windows are controls. Both are imperfect: on 1 January 2004 the archived Pathfinder files change processing run, and the 2006 window uses NOAA-18 and the later pfv51 run.

**Same-processing test.** We compared January-May 2005 with January-May 2004 (both NOAA-17, files made in November 2007) per box, with 20-degree spatial block bootstrap intervals.

**Ice-distance test.** We calculated the great-circle distance from each cell to the nearest cell with DOISST ice on any day of 2004 or 2005 and averaged the 2005-01 box steps in distance bins.

**In situ test.** Monthly means of DOISST minus ICOADS R3 values at the matched cell-days, by platform type (moored buoys after removal of each cell mean) and by source deck, with the monthly step model.

## Results tables

Monthly step model, 60S-60N (C; `results/monthly_steps.csv`):

| Series | 2004-01 (placebo) | 2005-01 | 95% interval (2005-01) | 2006-01 (placebo) |
|---|---|---|---|---|
| DOISST - ERSSTv5 | -0.032 | +0.073 | +0.060 to +0.086 | -0.040 |
| DOISST - HadSST4 | -0.016 | +0.072 | +0.060 to +0.085 | -0.016 |
| Pathfinder night - ERSSTv5 | -0.047 | +0.038 | +0.011 to +0.064 | -0.013 |
| Pathfinder day - ERSSTv5 | +0.003 | +0.043 | +0.022 to +0.066 | -0.024 |
| DOISST - Pathfinder night | +0.018 | +0.035 | +0.009 to +0.065 | -0.028 |
| DOISST - Pathfinder day | -0.034 | +0.030 | +0.005 to +0.053 | -0.019 |

Step against distance from DOISST ice (box steps at 2005-01, C; `results/test4_step_vs_ice_distance.csv`):

| Distance (km) | DOISST - ERSSTv5 | DOISST - Pathfinder night | Pathfinder night - ERSSTv5 |
|---|---|---|---|
| 0-500 | -0.004 | -0.098 | +0.089 |
| 500-1000 | +0.046 | -0.016 | +0.069 |
| 1000-2000 | +0.067 | +0.064 | +0.004 |
| 2000-4000 | +0.057 | +0.064 | -0.005 |
| > 4000 | +0.078 | +0.072 | +0.007 |

One-week change at 1 January (days 0-6 minus days -7 to -1, C; `results/test2_abrupt_change_daily.csv`):

| Series (matched cells) | 2004 (control) | 2005 | 2006 (control) |
|---|---|---|---|
| DOISST - moored buoys, day cells | +0.040 | **+0.093** (0.064 to 0.122) | -0.037 |
| DOISST - moored buoys, night cells | +0.005 | **+0.083** (0.062 to 0.104) | -0.027 |
| Pathfinder - moored buoys, day | -0.013 | -0.006 (-0.032 to 0.020) | -0.073 |
| Pathfinder - moored buoys, night | -0.050 | +0.013 (-0.025 to 0.056) | -0.086 |
| DOISST - Pathfinder, > 1000 km from ice, day | +0.046 | **+0.114** (0.092 to 0.135) | +0.003 |
| DOISST - Pathfinder, > 1000 km from ice, night | +0.093 | **+0.114** (0.103 to 0.125) | +0.029 |

Drifter comparisons are noisier (Pathfinder minus drifters +0.11 and +0.09 C in 2005, -0.07 and -0.11 C in 2004) because few drifter cell-days are clear-sky matches; we use the moored buoys as the main daily reference.

Same-processing year-on-year test, January-May 2005 minus January-May 2004 (C; `results/test3_same_processing_yoy.csv`): Pathfinder night - ERSSTv5 +0.044 (0.014 to 0.073); Pathfinder day - ERSSTv5 +0.044 (0.014 to 0.073); Pathfinder - HadSST4 +0.053 / +0.052; DOISST - ERSSTv5 +0.062 (0.037 to 0.086); DOISST - HadSST4 +0.073 (0.047 to 0.102); DOISST - Pathfinder +0.018 / +0.019 (intervals include zero). More than 1000 km from ice: Pathfinder +0.034 to +0.049, DOISST +0.062 to +0.072, DOISST - Pathfinder +0.027 to +0.028.

In situ cells, monthly model (C; `results/insitu_steps.csv`): DOISST - ships +0.063 (0.045 to 0.082), DOISST - drifting buoys +0.066 (0.033 to 0.099), DOISST - moored buoys +0.017 (0.009 to 0.025). Ships from the delayed-mode logbook deck 926 and from the GTS deck 992 give the same step (+0.054 and +0.057 C). Drifter decks differ (+0.019 to +0.183 C); deck composition changes in time, so we do not interpret single decks.

Pathfinder processing metadata (`results/pf_daily_coefficients.csv`): processing dates January 2005 (2003 files), November 2007 (January 2004 - May 2005), February-March 2009 (June 2005 - 2006, "pfv51"); first NLSST coefficient set on 31 December 2004 (1.219, 0.930, 0.132, 1.190) and on 1 January 2005 (1.245, 0.932, 0.127, 1.317); the sets also change on 1 January 2004 and near 1 January 2006.

## Figures

- `figures/fig1_timing.png`: (a) DOISST minus CCI around 1 January 2005 and the mean of 40 other New Years; (b) DOISST and Pathfinder minus moored buoys at the same cell-days, 2005 with 2004 and 2006 controls; (c) DOISST minus Pathfinder more than 1000 km from ice, day and night.
- `figures/fig2_ice_distance.png`: 2005-01 box steps against distance from DOISST ice.
- `figures/fig3_monthly_processing.png`: monthly differences 2003-2006 more than 1000 km from ice, with the three Pathfinder processing runs.

## Limitations

- **The in situ cause is inferred, not measured.** ICOADS Release 2.4 and its real-time archive for 2005 are no longer distributed, so we could not compare the real-time data that DOISST used with the delayed-mode data. The causal claim rests on the date match, the rejection of the two other candidates and the spatial pattern. Another undocumented change in the DOISST processing on 1 January 2005 remains possible.
- **We do not know exactly which Pathfinder files DOISST used.** The archived files for June 2005-2006 were made after the DOISST v2 release, and the 2003 files come from an earlier run. Our test of the input is valid for January 2004 - May 2005 only, which covers the step date.
- **Controls are imperfect.** The 2004 daily control contains a Pathfinder processing change, and the 2006 control uses another satellite. DOISST minus Pathfinder also rises on 1 January 2004 (+0.05 to +0.09 C), while DOISST minus ERSSTv5 does not; this agrees with a drop of the archived Pathfinder at that processing boundary.
- **The Pathfinder share of the January-May mean is uncertain.** Depending on the estimator, Pathfinder contributes between about zero and about half of the 2005 step on a time scale of months. One year of the same processing cannot separate this from Pathfinder drift.
- **The references are not independent of all inputs.** ERSSTv5 and HadSST4 use ICOADS R3, which contains many of the same observations as DOISST (in delayed-mode form). The daily buoy and CCI references are noisy at the 0.02-0.05 C level.
- **Scope.** We tested 60S-60N and 2003-2006 only. We did not test the effect on polar regions or a correction of DOISST.

## Reproduction

`files/code/run_all.sh` lists all steps in order and the folder layout. Raw downloads (about 7 GB streamed; Pathfinder files are deleted after binning) go to a local `scratch/` folder, never into the bundle. Runtime on the campaign host with 2 CPUs: about 1.5 h, mostly downloads. To check the main results without downloads, run `final_tests.py` and `figures.py` with the bundled `results/` files (and `data/monthly_difference_fields_2003_2006.npz` for the monthly tests). `files/provenance/data_provenance.json` gives the URL and SHA-256 hash of all 936 Pathfinder files, 48 ICOADS files, 4 ice files, the shared DOISST, ERSSTv5 and HadSST4 files, and the prior-bundle file.

## Provenance

- Job: sci-1107-hp-earth-and-ocean-sciences-d700a04e2eb3; campaign 11_07_2026; topic earth-and-ocean-sciences; machine hp; account claude-myxtap.
- Model: Claude Opus 5.5 (claude-opus-5-5) through Claude Code. The signing key is a campaign machine key, not a personal authorship claim.
- Shared datasets used in place: `datasets/noaa-psl-oisst-v21-highres-sst-day-mean-{2003..2006}-20261109`, `datasets/noaa-psl-oisst-v21-monthly-complete-20261109-dba314`, `datasets/ersst-v5-psl-sst-mnmean-20261108-olen`, `datasets/hadsst-4.2.0.0-median-metoffice-20261110` (hashes in `files/provenance/data_provenance.json`). The shared file `noaa-psl-oisst-v2.1-highres-sst-mon-mean-20261109/sst.mon.mean.nc` could not be opened (HDF error; its hash matches its own record, so the original download was probably incomplete); we used the "monthly-complete" copy.
- External terms and attribution: `files/NOTICE_external_data.md`.

## References

- Banzon, V., Smith, T. M., Chin, T. M., Liu, C., Hankins, W. (2016) A long-term record of blended satellite and in situ sea-surface temperature for climate monitoring, modeling and environmental studies. Earth Syst. Sci. Data 8, 165-176. doi:10.5194/essd-8-165-2016
- Reynolds, R. W., Smith, T. M., Liu, C., Chelton, D. B., Casey, K. S., Schlax, M. G. (2007) Daily high-resolution-blended analyses for sea surface temperature. J. Climate 20, 5473-5496. doi:10.1175/2007JCLI1824.1
- Huang, B., et al. (2021) Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. J. Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Woodruff, S. D., et al. (2011) ICOADS Release 2.5: extensions and enhancements to the surface marine meteorological archive. Int. J. Climatol. 31, 951-967. doi:10.1002/joc.2103
- Freeman, E., et al. (2017) ICOADS Release 3.0: a major update to the historical marine climate record. Int. J. Climatol. 37, 2211-2232. doi:10.1002/joc.4775
- Casey, K. S., Brandon, T. B., Cornillon, P., Evans, R. (2010) The past, present, and future of the AVHRR Pathfinder SST program. In: Oceanography from Space, Springer. doi:10.1007/978-90-481-8681-5_16
- Huang, B., et al. (2017) Extended Reconstructed Sea Surface Temperature, Version 5 (ERSSTv5). J. Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
- Kennedy, J. J., Rayner, N. A., Atkinson, C. P., Killick, R. E. (2019) An ensemble data set of sea surface temperature change from 1850. J. Geophys. Res. Atmos. 124, 7719-7763. doi:10.1029/2018JD029867
- Embury, O., et al. (2024) Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data 11, 326. doi:10.1038/s41597-024-03147-w
