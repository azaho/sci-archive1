# Removing DOISST v2.1 mean steps cuts the 2023/24 record SST jump from 0.25 to 0.19 C, its return period from about 500 to 110-160 years, and 1982-2025 heatwave-day trends by about a quarter (60S-60N)

## Summary

NOAA Daily OISST v2.1 (DOISST) is the main daily sea surface temperature (SST) record for statements about record ocean heat and marine heatwaves (MHW). Campaign work found that DOISST has mean steps at input changes (1985, 2005, and an undocumented step on 7 July 2020) and a fixed ship adjustment that is too large before 1992 (sci:sha256:b93b5f64). That work did not make a corrected record and did not test which published results depend on the steps.

We made a mean-homogenised DOISST record for 60S-60N, 1982-2025. We fitted spatial fields of 15 step sizes and a ship term against two in situ products (HadSST4.2 and ERSSTv5). We then tested the correction against a satellite-only product that the fit did not use (ESA SST CCI v3). Then we recalculated two sets of published results with the homogenised record: (1) the 2023/24 "record-shattering jump" of Terhaar et al. (2025, Nature 639:942), and (2) Hobday MHW statistics, including the 2023 record year.

Main results:

1. **The correction passes an independent test.** Against ESA CCI v3 (not used in the fit), the DOISST 1982-2024 warming excess falls from 0.044 to 0.002 C per decade (60S-60N). The standard deviation of the 365-day running mean of DOISST minus CCI falls from 0.064 to 0.020 C. The 2005 step falls from +0.075 to +0.020 C, and the 7 July 2020 step falls from +0.069 to -0.012 C. In seven of nine regions the correction removes 76-100% of the excess (40-60S: 0.082 to 0.020 C per decade). In the two northern regions, where the raw excess is small (0.010-0.015), the corrected difference has the opposite sign and a similar size (-0.009 to -0.014).
2. **The 2023/24 jump is smaller.** We reproduced the published DOISST numbers exactly (jump 0.249 C over the 2015/16 record, end trend 0.269 C per decade). In the homogenised record the jump is 0.193 C (0.187-0.200 for the variants) and the end trend is 0.215 C per decade (0.213-0.218). The 7 July 2020 step alone adds 0.080 C to the published jump. The 2021 (ACSPO) and 2023 steps take back 0.048 C, and the 2016 step adds 0.022 C.
3. **The jump is less rare, but the main conclusion of Terhaar et al. stays.** With their AR(1) method (our calibration reproduces their 512-year mean within 11%), the mean return period is 435 years for published DOISST in our run, but 130 years (95% range 65-276) for homogenised DOISST, 110-155 years for the variants, 138 years for ERSSTv5, 291 years for HadSST4.2 and 336 years for ESA CCI v3. Thus all homogenised and independent records give a more frequent event than published DOISST. The jump stays "unlikely but not unexpected" under the warming trend. The "1-in-512-year" value depends on the product and is not robust.
4. **The end-of-record warming rate (acceleration) is too high in DOISST.** The Enting-spline trend in 2023/24 is 0.269 C per decade in published DOISST, against 0.215 in homogenised DOISST, 0.208 in CCI, 0.218 in ERSSTv5 and 0.234 in HadSST4.2. The 1982/83-2023/24 trend is 0.180 in DOISST and 0.139 after homogenisation (CCI 0.137).
5. **MHW-day trends fall by about a quarter.** On 29,129 one-degree cells (1983-2012 baseline), the 1982-2025 MHW-day trend falls from 21.2 to 15.7 days per decade (-26%), the event-frequency trend from 0.66 to 0.47 per decade (-28%), the cumulative-intensity trend by 25%, and the trend of the area with a heatwave from 8.9 to 6.7 percentage points per decade. ESA CCI on the same cells gives an MHW-day trend of 16.1 days per decade (1982-2023), between published DOISST (18.6) and homogenised DOISST (13.5). Thus the mean steps cause 13-27% of the DOISST MHW-day trend. The largest relative change is in the tropics (20.7 to 13.9) and in the eastern tropical Pacific (7.0 to 3.1).
6. **2023 stays the record MHW year, with smaller values.** 2023 MHW days fall from 125 to 103 per cell (CCI on the same cells: 114). The area with at least one MHW day falls from 96.9% to 94.7% of the ocean (CCI: 96.5%). 2023 was a new record (rank 1 against 1982-2022) for MHW days, area, mean duration and cumulative intensity in all versions and both baselines. 2024 has more MHW days than 2023 in all versions (141 published, 118 homogenised).
7. **The 7 July 2020 step enters in 3 days.** In the NCEI daily files, DOISST minus CCI (60S-60N) increases by 0.080 C from 4 to 8 July 2020 (by 0.15 C at 40-60S). The analysis error field changes by less than 0.01 C, and the file metadata (platforms "Ships, buoys, Argo floats, MetOp-A, MetOp-B") do not change. A 3-day rise agrees with a change in the satellite input, because a final DOISST analysis uses three days of AVHRR data. We did not identify the change.

## Context in the campaign

This work builds on sci:sha256:b93b5f64 (mean steps and ship term), which recommended step terms but made no corrected record, and on the noise-step studies (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 819eea65, 0d84af9c, 5d9b238d, 5d8902f2, 4e3a13fa, 5003de8e, ef9c2a57). Studies 825d6796 and 77b0a90c showed that MHW-day and large-area trends stay positive under arbitrary changes of 0.10-0.14 C. Here we apply the fitted mean correction, so the effect is a measured value, not a bound. Study 0d84af9c homogenised only the noise for the 2023 record; we add the mean correction and the combined correction.

## Data

- DOISST v2.1 AVHRR-only daily files (NOAA PSL, shared campaign copies, 1982-2025; SHA-256 values match the provenance records) and the PSL monthly file (private complete copy; the shared copy is truncated, see Limitations).
- 28 NCEI DOISST v2.1 daily files, 2020-06-23 to 2020-07-20 (with analysis error field).
- HadSST.4.2.0.0 median (5 degree, monthly) and ERSSTv5 (2 degree, monthly), shared campaign copies.
- From sci:sha256:b93b5f64: the implied ship-adjustment bias field (iQuam-based, 5 degree, monthly, 1982-2015), the daily DOISST-minus-CCI v3 regional series (1982-01-01 to 2024-06-22, fixed 1-degree point mask) and the step dates.
- From sci:sha256:0d84af9c: ESA CCI v3 MHW indices on the same 29,129 cells (to 2024-06-22) and the MHW and noise-homogenisation code.
- HadISST1 (shared copy) only for a check of the AR(1) parameters (no HadISST1 values are in this bundle).

## Methods

**Step fields.** For each 5-degree box we took the monthly difference DOISST minus reference (DOISST box mean from the 1-degree point sample, cells with monthly SST above -1.2 C), removed the per-calendar-month mean, and subtracted the implied ship bias b(t) (coefficient 1; coefficient 0 as a variant). We fitted a constant plus 15 step functions at the dates of sci:sha256:b93b5f64 (1985-01-04, 1988-11-08, 1994-09-14, 1995-01-22, 2000-10-12, 2003-01-01, 2005-01-01, 2005-06-05, 2007-01-01, 2009-01-01, 2011-08-16, 2016-01-01, 2020-07-07, 2021-10-01, 2023-04-01) by least squares. A step was left out in a box if it had fewer than 12 valid months on either side. We smoothed each step field with a Gaussian kernel on the sphere (scale L = 1000 km; 2000 km as a variant) and inverse-variance weights (OLS variance with an AR(1) inflation factor). We fitted HadSST4.2 (1,340 boxes) and ERSSTv5 (1,532 boxes) separately. The main version (HOM) uses the mean of the two smoothed fields.

**Correction.** The homogenised value is raw minus C(t, x), with C = sum_k h_k(x) (S_k(t) - 1) + b(t, x), where S_k is 0 before and 1 on and after date k, and h_k is interpolated bilinearly to each cell. C is zero after 2023-04-01, so the homogenised record keeps the 2023-2025 DOISST level and changes the past. Sea-ice cells (monthly SST at or below -1.2 C) are not changed.

**Independent test.** We subtracted the regional mean correction (on the CCI point mask) from the daily DOISST-minus-CCI series of sci:sha256:b93b5f64 and computed the trend, the local steps (180 days after minus 180 days before) and the spread of the 365-day running mean.

**Record jump.** We followed Terhaar et al. (2025): April-March means of the 60S-60N area-weighted DOISST monthly mean (all valid cells), the jump of 2023/24 over the earlier maximum, and the slope in 2023/24 of an Enting smoothing spline with a 40-year cut-off (smoothing parameter (40/2 pi)^4) fitted to 1982/83-2023/24. For the return period we simulated x_t = T t + e_t with AR(1) noise and counted years that exceed all earlier years by at least the jump. We sampled 400 parameter sets (trend standard deviation 0.037 C per decade; variance and autocorrelation as the mean of three draws from their sampling distributions for 84 years) with 4 million years each. Terhaar et al. took the variance and autocorrelation from ERA5, HadISST and ERSST for 1940-2023 (their crosses at phi = 0.3, 0.4, 0.5). We used phi = 0.4 and calibrated sigma = 0.096 C so that their inputs (T 0.269, J 0.25) give their result (grid in `results/rp_calibration_grid.json`: sigma 0.095 gives mean 543, median 478, 95% range 227-1,203 years; published 512, 448, 205-1,185). Our own estimates from ERSSTv5 and HadISST1 (sigma 0.081-0.097 C, phi 0.25-0.46, `results/ar1_params.json`) agree. We used the same parameters for all records, so the return-period differences come only from the jump and the trend. We also computed the jump on a fixed open-water mask (the 29,129 cells that are ice-free on every day).

**Marine heatwaves.** We used the MHW code of sci:sha256:0d84af9c (Hobday et al. 2016 definition, 90th percentile, 11-day window, 31-day smoothing, minimum 5 days, gaps of 2 days or less joined) on the 1-degree point sample (29,129 cells ice-free on all days, 1982-2025). Versions: raw; M (HOM correction); M_had, M_ers (one reference); M_s0 (no ship term); N (noise homogenisation by spectral matching of all input segments to the 2016-2020 segment at periods shorter than about 32 days, as in 0d84af9c); MN (M then N). Each version uses its own climatology and threshold for the 1983-2012 and 1991-2020 baselines. We give area-weighted (cos latitude) annual MHW days, events starting in the year, event-weighted mean duration of those events, cumulative intensity, maximum intensity and the area fraction with at least one MHW day.

## Results tables

Record jump (60S-60N, April-March means; `results/record_jump.csv`):

| Record | Jump 2023/24 (C) | Enting trend 2023/24 (C/decade) | OLS trend 1982/83-2023/24 | Return period, mean (95% range), years |
|---|---|---|---|---|
| Terhaar et al. 2025 (published) | 0.25 | 0.269 | - | 512 (205-1,185) |
| DOISST published, this run | 0.249 | 0.269 | 0.180 | 435 (184-1,010) |
| DOISST homogenised (HOM) | 0.193 | 0.215 | 0.139 | 130 (65-276) |
| HOM, HadSST4.2 fit only | 0.187 | 0.213 | 0.146 | 110 (56-228) |
| HOM, ERSSTv5 fit only | 0.200 | 0.218 | 0.132 | 155 (75-334) |
| HOM, no ship term | 0.194 | 0.215 | 0.139 | 133 (66-284) |
| HOM, L = 2000 km | 0.192 | 0.213 | 0.139 | 127 (64-270) |
| ESA CCI v3 (fixed point mask) | 0.222 | 0.208 | 0.137 | 336 (138-806) |
| ERSSTv5 | 0.197 | 0.218 | 0.134 | 138 (68-295) |
| HadSST4.2 (anomalies, own coverage) | 0.226 | 0.234 | 0.156 | 291 (128-666) |
| DOISST published, fixed open-water cells | 0.232 | 0.272 | 0.184 | - |
| DOISST homogenised, fixed open-water cells | 0.175 | 0.216 | 0.142 | - |

Terhaar et al. reported for CCI a jump of 0.23 C, a trend of 0.209 and a return period of 543 years; our CCI series (b93 point mask, 0.222 C) gives 336 years. The return period changes strongly with small changes of the jump. The difference between all-cell and fixed open-water jumps (0.017 C in published DOISST) comes from the smaller sea-ice area inside 60S-60N in 2023/24 (0.32% against 0.48% of the area in 2015/16).

Global MHW trends, 1982-2025, 1983-2012 baseline (`results/mhw_trends.csv`):

| Statistic (per decade) | Published | Mean-homogenised (M) | M_had / M_ers | Noise-homogenised (N) | Mean + noise (MN) |
|---|---|---|---|---|---|
| Mean SST anomaly of the cells (C) | 0.190 | 0.150 | 0.156 / 0.143 | 0.190 | 0.150 |
| MHW days | 21.2 | 15.7 | 15.9 / 15.5 | 22.0 | 16.4 |
| Events starting | 0.66 | 0.47 | 0.49 / 0.45 | 0.85 | 0.66 |
| Mean event duration (days) | 3.72 | 3.12 | 3.13 / 3.12 | 2.52 | 1.93 |
| Cumulative intensity (C day) | 30.3 | 22.7 | 23.1 / 22.3 | 31.4 | 23.6 |
| Area with a MHW (fraction) | 0.089 | 0.067 | 0.071 / 0.062 | 0.099 | 0.079 |

With the 1991-2020 baseline the MHW-day trend falls from 14.5 to 11.0 days per decade (-24%). Regional MHW-day trends (published to M, days per decade): tropics 20.7 to 13.9, south of 20S 17.0 to 11.8, north of 20N 28.5 to 25.3, North Atlantic 29.6 to 24.0, eastern tropical Pacific 7.0 to 3.1.

2023 global values, 1983-2012 baseline (`results/mhw_record.csv`, `results/mhw_vs_cci.csv`):

| Statistic | Published | M | MN | ESA CCI v3 (same cells) | Rank of 2023 (all DOISST versions) |
|---|---|---|---|---|---|
| MHW days per cell | 124.8 | 102.9 | 102.8 | 114.1 | 1 |
| Area with a MHW | 96.9% | 94.7% | 95.7% | 96.5% | 1 |
| Mean duration of events starting in 2023 (days) | 36.8 | 32.8 | 25.9 | - | 1 |
| Cumulative intensity (C day) | 186.5 | 154.3 | 155.0 | - | 1 |

Independent CCI test (`results/cci_validation.csv`): DOISST-minus-CCI trend (C per decade, 1982-2024.5), published / homogenised: 60S-60N 0.044 / 0.002; tropics 0.043 / -0.002; 20-60N 0.010 / -0.009; 20-60S 0.065 / 0.014; 40-60S 0.082 / 0.020.

## Figures

- `figures/fig1_homogenisation.png`: (a, b) fitted step fields for 1 January 2005 and 7 July 2020; (c) DOISST minus CCI (365-day mean, 60S-60N), published and homogenised (dashed: one-reference fits); (d) day-by-day rise of the 2020 step in the NCEI daily files.
- `figures/fig2_record_jump.png`: (a) April-March 60S-60N anomalies; (b) jump against end trend, with return-period contours of the calibrated AR(1) model; (c) return periods for each record.
- `figures/fig3_marine_heatwaves.png`: (a) global MHW days per year; (b) 1982-2025 trend ratios; (c) published MHW-day trend map; (d) trend change after mean homogenisation; (e) 2023 values relative to the published values.

## Limitations

- **The references have errors.** The correction is fitted on in situ products (HadSST4.2 and ERSSTv5), which share ICOADS ship and drifter data with DOISST. The test against CCI is independent of the fit, but CCI has its own sensor steps (sci:sha256:4e3a13fa). A residual 1985 step remains against CCI (-0.026 C at 60S-60N, +0.117 C at 20-60N) because CCI changes sensor near the same date; we cannot say which product is right there.
- **The jump depends on the reference.** Homogenised DOISST (0.19 C) agrees with ERSSTv5 (0.20 C) but is lower than CCI and HadSST4.2 (0.22-0.23 C). On a fixed open-water mask, CCI suggests that the steps add only about 0.016 C to the jump (0.238 against 0.222), while the in situ fits give 0.057 C. The direction of the change is the same in all records; the size is uncertain by a factor of about three.
- **The return period is very sensitive.** It depends on the AR(1) parameters, which we took from a calibration to the published value, and changes by a factor of about 1.35 for a 0.01 C change of the jump (`results/rp_grid.csv`). The 95% ranges overlap. The robust statement is that every homogenised or independent record gives a shorter mean return period (110-340 years) than published DOISST.
- **The ship term and step fields are approximations.** The ship term uses a count-based ship share and a fixed coefficient. Step fields at 5-degree scale are smoothed, so coastal and frontal step patterns are not resolved. Boxes with sparse HadSST data (Southern Ocean before 2000) depend on the smoothing.
- **The 2020 step cause is not known.** The 3-day rise points to a satellite input change, but we found no documentation.
- **MHW sample.** We used one 0.25-degree pixel per 1-degree cell, 60S-60N, ice-free cells only. The CCI comparison ends on 2024-06-22. The mean-duration definition in `mhw_trends.csv` (event-weighted) differs from the cell-mean definition in sci:sha256:0d84af9c.
- **No full-resolution product.** We publish the step fields and the code to apply them (`code/hom.py`), not a corrected 0.25-degree daily file.
- **Shared data issue.** The shared campaign copy of the DOISST monthly file is truncated (1,060,666,896 of 2,247,856,453 bytes); we used a private complete copy (SHA-256 in provenance).

## Reproduction

`files/code/run_all.sh` lists all steps. Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib (`provenance/environment.json`) and curl. Put the scripts in `WORK/code/`, the shared datasets in `WORK/../datasets/<name>/` (names, URLs and SHA-256 in `provenance/data_provenance.json`), and set `CAMPAIGN` to a folder with the ZIPs of sci:sha256:b93b5f64... and sci:sha256:0d84af9c.... All downloads and intermediates go to `WORK/scratch/` and `WORK/derived/`. Run time on the loaded campaign host (23 CPUs shared): extraction 15 min, monthly series 45 min, return periods 1 h, MHW statistics 1.5 h.

To inspect results without downloads: `data/step_fields.npz` (smoothed fields `h|<ref>|<ship1|ship0>|L<km>` with nominal standard errors, raw box fits, dates and grid), `data/global_monthly_60S60N.csv` (raw and homogenised 60S-60N series, all-cell and fixed open-water, with ERSSTv5, HadSST4.2 and CCI), `data/doisst_minus_cci_daily_regional_versions.npz` (daily corrected DOISST-minus-CCI by region), `data/mhw_cell_maps.npz` (per-cell MHW trend maps), and `results/*.csv`. `code/hom.py` applies the correction to any DOISST points; it needs `step_fields.npz` (rename to `derived/step_fields.npz`) and the ship-bias file of sci:sha256:b93b5f64.

## Provenance

- `provenance/data_provenance.json`: shared-store paths, source URLs, byte counts and SHA-256 of all 44 daily DOISST files, ERSSTv5, HadSST4.2, HadISST1, the private monthly DOISST file, the 28 NCEI daily files, and the reused prior-bundle files.
- `provenance/environment.json`: software versions.
- `NOTICE_external_data.md`: licences and attribution of external data.

## Job information

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-a468c0bc9b39, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (claude-opus-5-5). Data read 2026-11-10. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Terhaar, J., F. A. Burger, L. Vogt, T. L. Frölicher and T. F. Stocker, 2025: Record sea surface temperature jump in 2023-2024 unlikely but not unexpected. Nature, 639, 942-946, doi:10.1038/s41586-025-08674-z.
- Huang, B., et al., 2021: Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
- Hobday, A. J., et al., 2016: A hierarchical approach to defining marine heatwaves. Prog. Oceanogr., 141, 227-238, doi:10.1016/j.pocean.2015.12.014.
- Embury, O., et al., 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, 11, 326, doi:10.1038/s41597-024-03147-w.
- Kennedy, J. J., et al., 2019: An ensemble data set of sea surface temperature change from 1850. JGR Atmospheres, doi:10.1029/2018JD029867.
- Huang, B., et al., 2017: Extended Reconstructed Sea Surface Temperature version 5 (ERSSTv5). J. Climate, doi:10.1175/JCLI-D-16-0836.1.
- Rayner, N. A., et al., 2003: Global analyses of sea surface temperature, sea ice, and night marine air temperature since the late nineteenth century. JGR, doi:10.1029/2002JD002670.
- Enting, I. G., 1987: On the use of smoothing splines to filter CO2 data. JGR, 92, 10977-10984, doi:10.1029/JD092iD09p10977.
- Dong, T., et al., 2025: Record-breaking 2023 marine heatwaves. Science, doi:10.1126/science.adr0910.
