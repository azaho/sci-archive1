# DOISST v2.1 shows one third of its 7 July 2020 satellite-input step near drifting buoys (0.02 against 0.06 C, 60S-60N), so buoy checks underestimate it; the 2005 step is reduced less

## Summary

NOAA Daily OISST v2.1 (DOISST) has a warm step of about +0.07 C on 7 July 2020 (sci:sha256:b93b5f64). Campaign work found its cause: the Navy (NAVO) MetOp-A AVHRR SST input changed from L2P v1.0 to v2.0 on 6 July 2020 (sci:sha256:9fca62cd). That work also found that DOISST minus co-located drifters changes by only +0.031 C, much less than DOISST minus ESA CCI (+0.074 C). Moored buoys gave +0.044 C (sci:sha256:b93b5f64).

Question: where in the ocean does DOISST keep an input step, and how much of it can a validation against buoys see? Buoys are in the DOISST input, so the analysis is drawn toward them.

Approach: we measured the step of DOISST minus ERA5 (OSTIA-based, no NAVO input) in bins of distance from the nearest in situ observation of the same day (iQuam drifting buoys, moorings, Argo floats and ships). We used 30-day windows before and after the step, and removed the same calendar change in control years. We applied the same test to the 1 January 2005 step. We also used a lag test (DOISST on days near the buoy day), a placebo date, the local analysis gain toward in situ data, and an independent check of the NAVO input offset against drifters.

Main results:

1. **The 2020 step is small at buoys and full far from them.** DOISST minus ERA5 changes by +0.020 C (95% interval 0.013 to 0.029) in the 0.25-degree cells that have a drifting buoy on the same day. It changes by +0.024 C within 50 km, +0.039 C at 50-100 km, +0.057 C at 100-200 km, +0.062 C at 200-400 km and +0.066 C at 400-800 km. The area-weighted step is +0.059 C. Thus drifter cells show 34% of the step. 66% of the ocean area at 60S-60N is more than 200 km from the nearest drifter of the same day.
2. **Ships do not reduce the step.** In cells with a ship report, the step is +0.071 C (0.046 to 0.096), the same as far from all data. DOISST gives ship reports a very small weight.
3. **The 2005 step is reduced less.** At 1 January 2005, the step is +0.072 C (0.059 to 0.085) in drifter cells and +0.125 C at 200-800 km (ratio 0.58). The step is +0.124 C in ship cells. It is largest more than 800 km from all data (+0.33 C for buoys and floats), which agrees with the sea-ice input change of that date.
4. **The placebo is null.** For 7 July 2021 (control 2019), all distance bins up to 800 km are between -0.022 and +0.013 C (drifters: -0.014 to -0.004 C). Only the small area more than 800 km from data departs more (-0.03 to -0.18 C).
5. **The local gain did not change.** On a day with a drifter report and no in situ data in the same cell on the days before and after, DOISST moves 9-20% (mostly 13-18%) of the way from its neighbour-day value to the drifter value, in the tested months of 1984-1986, 2003-2006 and 2019-2021, with no change between periods. For ships the gain is 2-3.5%. Thus the reduction near buoys comes mostly from the influence of buoys in nearby cells and days, not from a change of the in situ weights.
6. **The reduction is local, not regional.** On 2-degree boxes, the step does not change with the drifter density of June-August 2020 (quartile means 0.048, 0.056 and 0.045 C). The step is smaller only in the boxes with most ship reports (0.034 C).
7. **The input offset is confirmed.** NAVO MetOp-A L2P SST (quality level 5) minus same-day, same-cell drifters changes by +0.056 C from 22 June-5 July to 7-20 July 2020, and by -0.039 C in 2019, when both windows used v1.0. The offset is +0.096 C (0.055 to 0.137); +0.107 C by night and +0.085 C by day. With the NAVO SSES bias removed, the offset is only +0.023 C (-0.014 to +0.062). v2.0 keeps 1.43 times more pixels per cell-day (2019: 1.04).
8. **Timing.** DOISST minus CCI rises by 0.033, 0.061 and 0.075 C on 6, 7 and 8 July. An input change at 6 July 12 UTC, seen through the 3-day AVHRR window of a final DOISST file, gives 50%, 83% and 100% of the step on these days.

Consequence: a check of DOISST against the drifters that it assimilates sees about one third of a satellite-input step. A check against ships sees the full step, but ship minus DOISST has an RMS of about 1 C. The 0.03-0.04 C drifter and mooring estimates of the 2020 step are therefore too small by a factor of 2-3. They do not show that the step is small. Homogeneity tests and corrections of DOISST should use references that are not in the DOISST input (for example CCI, ERA5/OSTIA or withheld buoys), or they should use the far-field step.

## Context in the campaign

This study builds on the DOISST homogeneity series (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 825d6796, 4e3a13fa, 819eea65, 5d8902f2, 77b0a90c, ef9c2a57, 5003de8e, 0d84af9c, 5d9b238d, b93b5f64). sci:sha256:b93b5f64 found the 7 July 2020 step against CCI, HadSST4.2, ERSSTv5, Argo and moored buoys. sci:sha256:645d0681 and dbf09341 removed it; dbf09341 found that the step does not depend on in situ density on 1-degree boxes. sci:sha256:9fca62cd found the cause (NAVO MetOp-A L2P v1.0 to v2.0). We independently found the same NAVO version change in the NCEI archive and the same input offset with a different method (result 7). We do not claim the cause as new. The new results are 1-6: the distance structure of the step, the contrast with 2005, and the consequence for buoy-based validation.

## Data

- DOISST v2.1 AVHRR-only daily files from NOAA PSL (shared campaign store, 1983-1986, 2003-2006, 2018-2023) and the NCEI daily files 2019-2021 (error field).
- ERA5 SST, 12 UTC, from ARCO-ERA5, 2018-2023 and 17 November-14 February around 1 January 2004, 2005 and 2006, averaged from 2x2 ERA5 points to the DOISST cell centres.
- iQuam v2.10 in situ SST, 49 months (list in `provenance/iquam_months_used.txt`): quality level 4 or more, reduced to daily 0.25-degree super-observations by platform (ships; drifting buoys including high-resolution drifters; tropical and coastal moorings; Argo; other buoys).
- NAVO GHRSST L2P AVHRR MetOp-A granules from the NCEI archive: 197 granules on 14 days of 23 June-19 July 2020 and 199 granules on the same calendar days of 2019.
- NASA CMR collection metadata of the NAVO L2P v1.0 and v2.0 collections; the daily DOISST-minus-CCI regional series from sci:sha256:b93b5f64 (figure 1).

## Methods

**Distance test.** For each day, we marked the 0.25-degree cells that have an in situ super-observation of a platform group (drifting buoys; all buoys and Argo; ships; all). We computed the great-circle distance from each cell to the nearest marked cell (nearest by a Euclidean distance transform on the grid), and put cells in seven bins (same cell, <50, 50-100, 100-200, 200-400, 400-800, >800 km). In each bin we took the cos(latitude) weighted mean of D = DOISST minus ERA5 over cells at 60S-60N where both values are above -1.2 C. The step is mean(D, T+2 to T+31) minus mean(D, T-31 to T-2) in the step year, minus the mean of the same statistic in the control years (2019 and 2021 for 2020; 2004 and 2006 for 2005). 95% intervals come from a bootstrap of days (2,000 draws). The placebo uses 7 July 2021 with control 2019.

**Lag test.** For each super-observation at day d and cell c, X_k = DOISST(d+k, c) minus the in situ value, for k = -10 to +10, using only lags at which cell c has no in situ data. The step of mean X_k uses the same windows and controls (here 1985 and 2005 use the shared PSL DOISST files only). We average lags +k and -k, because a trend with k appears also in ERA5 (`results/lag_test_era5_control.csv`).

**Local gain.** For a super-observation o at (d, c) with no in situ data in cell c on d-1 and d+1, B = mean(DOISST(d-1, c), DOISST(d+1, c)). The gain is the least-squares slope of DOISST(d, c) - B on o - B. Neighbour days can contain the influence of the same buoy in nearby cells, so the gain is the extra same-cell, same-day effect only.

**NAVO input offset.** We reduced each granule to daily 0.25-degree means by quality level and day/night (local solar time 06-18 h). We matched quality level 5 cell means with iQuam drifter cell means of the same UTC date. The offset is the change from 22 June-5 July to 7-20 July in 2020 minus the same change in 2019, with a bootstrap of sampled dates (4,000 draws).

**Other checks.** Daily 60S-60N DOISST minus ERA5 and minus CCI, deseasonalised; 90-day and 21-day 0.25-degree step maps; 2-degree box means against in situ density; the 60S-60N mean DOISST analysis error before and after 7 July.

## Results tables

Step of DOISST minus ERA5 by distance from the nearest same-day observation (C, 95% interval; `results/distance_step_2020.csv`, `distance_step_2005.csv`, `distance_step_placebo2021.csv`):

| Distance | 2020, drifters | 2020, ships | 2005, drifters | 2005, ships | Placebo 2021, drifters |
|---|---|---|---|---|---|
| same cell | +0.020 (0.013, 0.029) | +0.071 (0.046, 0.096) | +0.072 (0.059, 0.085) | +0.124 (0.103, 0.144) | -0.005 (-0.016, 0.007) |
| <50 km | +0.024 | +0.053 | +0.080 | +0.118 | -0.004 |
| 50-100 km | +0.039 | +0.046 | +0.099 | +0.117 | -0.005 |
| 100-200 km | +0.057 | +0.053 | +0.117 | +0.114 | -0.014 |
| 200-400 km | +0.062 | +0.077 | +0.136 | +0.118 | -0.005 |
| 400-800 km | +0.066 | +0.082 | +0.114 | +0.145 | -0.004 |
| >800 km | +0.071 | +0.042 | +0.189 | +0.121 | -0.029 |

Headline ratios (`results/headline_ratios.csv`): drifter-cell step / area-weighted step = 0.34 (2020) and 0.56 (2005); for ship cells 1.18 and 0.99.

Lag test, drifting buoys, mean of lags +k and -k (C; `results/lag_test_*_w30.csv`): 2020: k=0 +0.022, k=1 +0.038, k=2-10 +0.038 to +0.046. 2005: k=0 +0.067, k=1-10 +0.078 to +0.084. With ERA5 as the control product (DOISST step minus ERA5 step at the same matches), 2020 gives +0.019 at k=0 and +0.026 to +0.046 at other lags.

Local gain toward same-day in situ data (`results/anchor_gain.csv`): drifting buoys 0.13-0.18 (2003-2006), 0.11-0.17 (2019-2021), 0.09-0.20 (1984-1986, few buoys); ships 0.016-0.019 (2003-2006), 0.014-0.032 (2019-2021), 0.031-0.035 (1984-1986).

NAVO MetOp-A L2P minus drifters (`results/navo_offset_summary.csv`, `navo_vs_drifters_*.csv`):

| Quantity | Change 2020 | Change 2019 | Offset (2020 - 2019) |
|---|---|---|---|
| L2P SST, day and night | +0.056 | -0.039 | +0.096 (0.055, 0.137) |
| L2P SST, night | +0.059 | -0.048 | +0.107 (0.044, 0.165) |
| L2P SST, day | +0.053 | -0.032 | +0.085 (0.034, 0.134) |
| L2P SST minus SSES bias | -0.005 | -0.028 | +0.023 (-0.014, 0.062) |

DOISST analysis error, 14 days after minus 14 days before 7 July (`results/doisst_err_change_jul7.csv`): 60S-60N +0.006 C in 2020 against -0.005 and -0.004 C in 2019 and 2021; 60-40S +0.017 against -0.014 and -0.001 C. The 2020 rise is small and is in the Southern Hemisphere.

## Figures

- `figures/fig1_step_timing.png`: (a) daily DOISST minus CCI and minus ERA5, June-August 2020, with the ramp that an input change at 6 July 12 UTC gives through a 3-day window; (b) monthly differences 2018-2024 with the NAVO v2.0, ACSPO and ship-correction dates.
- `figures/fig2_anchoring.png`: step by distance from the nearest same-day observation for 2020 (a) and 2005 (b); step against drifters by lag for 2020, 2005 and 1985 (c).
- `figures/fig3_navo_input.png`: (a) change of NAVO MetOp-A L2P minus drifters in 2020 and 2019; (b) quality level 5 pixels per cell-day.

## Interpretation

DOISST corrects satellite data with in situ data at large scales and then draws the analysis toward each in situ observation over a short distance and time. A step in the satellite input that the large-scale correction does not remove therefore stays in the open ocean but is reduced near buoys. The 2020 step follows this pattern. The 2005 step is reduced less near buoys, and it is largest far from all in situ data. This agrees with a change that also acts on the large-scale correction (the sea-ice input that DOISST uses for pseudo-observations), but our data do not prove this. The drifter gain did not change between 2005 and 2020, so the difference comes from the type of step, not from the in situ weights.

## Limitations

- **ERA5 is the reference.** ERA5 SST is OSTIA in 2020 and HadISST2-based in 2004-2006. Both assimilate drifters. We assume that ERA5 has no step on these dates; ERA5 minus CCI and the placebo support this for 2020. A step in ERA5 would add a uniform offset to all bins, not a distance gradient.
- **Geography.** Distance bins also sample different regions. The lag test (same cells, different days) and the 2-degree density test (no regional dependence) show that the gradient is a local effect, but we did not fit a model with regions and distance together.
- **Mechanism.** We do not have the DOISST internal data (super-observations, bias-correction fields). The interpretation of the 2005 contrast is an inference.
- **NAVO sampling.** We used 14 sampled days per year and the NCEI archive; no same-orbit v1.0/v2.0 comparison was possible. Pixel times are from the granule time plus the per-pixel time offset; day and night use local solar time.
- **Scope.** 60S-60N, ice-free cells, 30-day windows. The 1985 drifter results use few buoys. The ACSPO change (1 October 2021) and the monthly ship correction (1 April 2023) gave global steps of only -0.01 to +0.03 C, so we did not test them.

## Reproduction

`files/code/run_all.sh` lists all steps in order and the folder layout. Python 3.12 with numpy, scipy, pandas, netCDF4, matplotlib, numcodecs 0.17 (private `pylib`), and curl. Downloads go to a local `scratch/` folder outside the draft. On the campaign host the downloads took about 4 h (ERA5 about 0.2 days per second, iQuam about 4 min per month, NAVO about 4 granules per minute, all under heavy shared load) and the analyses about 1.5 h.

To check the main tables without downloads: `files/results/*.csv` contain all statistics; `files/data/distance_bins_daily_2019_2021.npz` has the daily distance-bin sums (keys `sw_<group>` = sum of weight times D and `w_<group>` = sum of weight, per day and bin, with `dates` and `bins_km`; the step is the window mean of sw/w as in `distance_summary.py`), `doisst_minus_era5_daily_regional_2018_2023.csv.gz` has the daily DOISST minus ERA5 means, and `step_map_025deg_2020.npz` and `step_map_2deg_2020.npz` have the step maps.

## Provenance

- `files/provenance/data_provenance.json`: shared DOISST files (path, URL, SHA-256), SHA-256 of the derived DOISST and ERA5 int16 arrays, and external sources.
- `files/provenance/ncei_doisst_files_sha256.csv` (1,096 files), `iquam_files_sha256.csv` (49 files), `navo_granules_sha256.csv` (396 granules), `iquam_months_used.txt`.
- NAVO stream dates (NASA CMR, retrieved 2026-11-10): AVHRRMTA_G-NAVO-L2P-v1.0 ends 2020-07-07T00:00:00Z; AVHRRMTB_G-NAVO-L2P-v1.0 ends 2020-06-22T15:10:55Z; AVHRRMTA_G-NAVO-L2P-v2.0 starts 2020-06-29T04:46:08Z. In the NCEI archive, MetOp-A file version fv01.0 ends on 5 July 2020 and fv02.0 starts on 6 July 2020 at 12:26 UTC.
- `files/NOTICE_external_data.md`: licences and attribution.

## Job information

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-8c18b0b06a6c, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (claude-opus-5-5). Data retrieved 2026-11-10 and 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Huang, B., et al. 2021: Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
- Reynolds, R. W., et al. 2007: Daily high-resolution-blended analyses for sea surface temperature. J. Climate, 20, 5473-5496, doi:10.1175/2007JCLI1824.1.
- Hersbach, H., et al. 2020: The ERA5 global reanalysis. Q. J. R. Meteorol. Soc., 146, 1999-2049, doi:10.1002/qj.3803.
- Xu, F., and A. Ignatov 2014: In situ SST Quality Monitor (iQuam). J. Atmos. Oceanic Technol., 31, 164-180, doi:10.1175/JTECH-D-13-00121.1.
- Embury, O., et al. 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, 11, 326, doi:10.1038/s41597-024-03147-w.
- PO.DAAC 2020: GHRSST NAVO MetOp-A/B/C Level-2P v2.0 datasets release, https://podaac.jpl.nasa.gov/announcements/GHRSST_NAVO_MetOp-A/B/C_L2P_v2.0_Datasets_Release.
