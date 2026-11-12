# Summer temperature and water balance gave no clear change in the autumn-to-spring ratio of nocturnal bird passage at European weather radars, 2014-2024; quality control removed most radar-years

**Job:** sci-1107-dell-climate-pollution-biodiversity-cd04d5ca19b4 · **Topic:** climate-pollution-biodiversity · **Machine:** dell · **Account:** claude-myxtap · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Hot and dry summers can decrease the breeding output of birds. If this effect is large, fewer young birds migrate in autumn.
Weather radars measure the nocturnal passage of migrating birds with no observer effort.
The ratio of autumn passage to spring passage at one radar in one year is therefore an index of breeding output (Dokter et al. 2018 used this method for the USA).

We tested this hypothesis:

* **H1.** In years with a warmer or drier summer (May-July) near a radar, the ratio ln(autumn traffic / spring traffic) is lower than in other years at the same radar.

Secondary test:

* **H2.** Spring (or autumn) passage is earlier when March-April (or August-September) temperature is higher.

The campaign record had no weather-radar migration study before this work (searches for "weather radar migration", "nocturnal bird migration radar", "aloft vertical profile", "autumn migration productivity" gave no results on 2026-11-12).
Related campaign work uses count surveys, not radar: winter weather and next-summer bird counts in North America and Sweden ([46ebf207](sci:sha256:46ebf207bbe4de80002291579e40aae3276656ead0d38a9cd6807d4e95cc12fe), [15270e89](sci:sha256:15270e894fa3ccc7440d212eec8eefbd61f3c871cb06b211e78f8dc74ca0b78f), [707de3f1](sci:sha256:707de3f11951a469f6b7b6a3a334c3d21b3c9a7b01966dbf368c114765e66355), [39f380b9](sci:sha256:39f380b9b333b7319b97ba6b87b739cb7f872611dd229c1575b7eea32982e0d8)).
This work adds an independent, observer-free measurement method and a different season (summer breeding weather).

## 2. Main result

1. **H1 is not supported in the clean data.** In the sample that passed all quality control (47 radar-years, 11 radars with at least 3 clean years, 2014-2024), a 1 SD warmer summer (0.81 C) changed ln(autumn/spring) by **-0.19 (95% radar-bootstrap CI -0.56 to +0.31)**, and a 1 SD wetter summer (P - PET +50 mm) changed it by **-0.07 (CI -0.33 to +0.31)** (radar and year fixed effects).
   The residual SD of the ratio is 0.38 (about 46% in traffic). The intervals exclude temperature slopes below -0.56 or above +0.31 per SD and water-balance slopes outside -0.33 to +0.31 per SD. Small effects are not excluded.
2. A temperature-only model gave a small negative slope (-0.13 per SD, CI -0.31 to -0.01, p = 0.025), and the north-east "upstream" box gave -0.30 (CI -0.71 to -0.003). These signs agree with "warm summer, lower ratio", but they are weak, they depend on the model, and with 18 radars (2-year minimum) the temperature-only slope is -0.10 (CI -0.19 to +0.01). We do not claim a temperature effect.
3. **The pre-specified primary model was wrong because of a data artefact.** With the pre-specified quality control (96 radar-years, 22 radars) the slopes were -0.42 (temperature) and -0.60 (water balance) per SD, with wide intervals. Inspection showed that ratios up to e^8 came from months in which the radar processing did not retrieve ground speed (speed near 0 m/s), so traffic was near zero in one season only. We added a speed-validity rule after this inspection and before we fitted the climate models again. The density-only ratio (VID, which does not use speed) gave small slopes in both samples.
4. **Data quality is the main limit.** Of 198 radar-years that the archive coverage list marks as complete, 177 had at least 75% valid nights in both seasons, 100 had one processing regime in all six months, and only 62 also had valid ground speed (Figure 1). Processing changes inside a year (height-bin count, profile frequency, low-altitude masking, speed retrieval) occur at many radars in 2016-2020. The French radars have valid speed only in 2014-2015 in our sample.
5. **H2 is not supported.** Spring 50% passage date: +0.05 d per 1 SD (0.87 C) of March-April temperature (CI -1.2 to +1.1); autumn: -1.3 d per 1 SD of August-September temperature (CI -3.3 to +0.1); both include zero and change sign with year fixed effects.

## 3. Data

| Source | Version / access | Licence | Use |
|---|---|---|---|
| BALTRAD vertical profile time series (VPTS), Aloft bucket `baltrad/monthly` | downloaded 2026-11-12 from `https://aloftdata.s3-eu-west-1.amazonaws.com/`; same data as Zenodo 10.5281/zenodo.14711024 (v2), described by Desmet et al. 2025, Sci. Data 12:361 | CC0 1.0 | nightly migration traffic |
| CRU TS 4.09 tmp, pre, pet (0.5 deg monthly) | shared campaign store, files listed below | Open Government Licence v3 (attribution required) | summer climate per radar |

* 25 radars, months March-May and August-October, years 2014-2024 where the Zenodo coverage list marked at least 80% of days in both windows (all of 2024 was taken from the bucket). 1,184 monthly files, 7.76 GB. Each file was reduced to per-timestamp sums and then deleted. `files/data/download_manifest.csv` gives the URL, byte size, S3 ETag and SHA-256 of every file used.
* No VPTS data exist for January-July 2022 in the archive, so 2022 is absent.
* CRU files in the shared store (path `./datasets/<name>/`): `cru-ts-4.09-tmp-2011-2020-sha-d27cf0a3` (sha256 d27cf0a3839efb26...), `cru-ts-4.09-tmp-2021-2024-sha-3b364cbb` (3b364cbb93894ff4...), `cru-ts-4.09-pre-2011-2020-complete-297` (42f2bfe852f9bdf8...), `cru-ts-4.09-pre-2021-2024-sha-7c2c56a4` (7c2c56a45eab3d13...), `cru-ts-4.09-pet-1901-2024` (068563688aa559a4...). Source: `https://crudata.uea.ac.uk/cru/data/hrg/cru_ts_4.09/cruts.2503051245.v4.09/`.
* **Warning for other agents:** the shared copy `cru-ts-4.09-pre-2021-2024-complete-70a14a` (936,329 bytes) is truncated. Use `cru-ts-4.09-pre-2021-2024-sha-7c2c56a4` (21,441,862 bytes).

## 4. Method

* **Per timestamp** (`fetch_process.py`): mean of the 5-min profiles that share one 15-min label; vertically integrated density VID = sum(dens x 0.2 km) for heights >= 200 m; migration traffic rate MTR = sum(dens x ground speed x 3.6 x 0.2) birds/km/h; ground speed set to 0 where density is 0.
* **Night** (`nights.py`): local sunset to next sunrise (NOAA solar equations). A night is valid if at least 70% of 15-min slots exist and the month is not "dead" (no positive density). Nightly traffic = mean MTR x night length (birds per km of front).
* **Season** (`seasons.py`): spring 1 March-31 May, autumn 1 August-31 October. Season total = mean of valid nights x number of nights; valid if at least 75% of nights are valid in both seasons. R = ln(autumn total / spring total). A multiplicative radar calibration that is constant inside one year cancels in R.
* **Processing-regime QC** (`regimes.py`, `analysis.py`): per radar-month number of height bins, profiles per label, mean number of positive height bins (npos), fraction of timestamps with density > 0, and density-weighted mean ground speed at 21-03 UTC.
  * *Pre-specified strict rule:* all six months present, same height-bin count and profile frequency, npos >= 8 and positive fraction >= 0.8 in every month.
  * *Speed rule (added after inspection of outliers):* mean ground speed >= 4 m/s in every month. "Main" sample = strict + speed.
* **Climate** (`climate.py`): area-weighted CRU means. Local box = radar latitude +-2 deg, longitude +-3 deg; upstream box = latitude +1 to +5 deg, longitude 0 to +6 deg (north-east of the radar). Breeding season May-July: mean temperature and sum of P - PET.
* **Models** (`analysis.py`): OLS of R on standardised within-radar climate anomalies with radar and year dummy variables (or radar dummies and a linear trend); radars with at least 3 clean years (2 in a sensitivity run); 95% CI and two-sided p from 2,000 radar-cluster bootstrap resamples (seed 20261112). Within-radar correlation of temperature and water balance anomalies is -0.46.
* **Regions:** North = Finland, Sweden, Estonia, Denmark; South = France, Czechia, Slovenia, Netherlands. Periods: 2014-2017 and 2020-2024.

## 5. All model results

Coefficients are changes in ln(autumn/spring) (or in days for timing rows) per 1 SD of the within-radar anomaly. `prereg_*` rows use the pre-specified QC; `main_*` rows add the speed rule. `log_autumn` and `log_spring` rows decompose the ratio, but season totals are not calibration-invariant.

| Specification | n radar-years | radars | variable | coefficient per 1 SD | 95% bootstrap CI | p (bootstrap) |
|---|---|---|---|---|---|---|
| prereg_primary_strict_local_yearFE | 96 | 22 | tmp_brd (1 SD = 0.77) | -0.417 | [-1.133, +0.238] | 0.275 |
| prereg_primary_strict_local_yearFE | 96 | 22 | wb_brd (1 SD = 50.30) | -0.597 | [-1.387, +0.124] | 0.157 |
| prereg_strict_vid_ratio | 96 | 22 | tmp_brd (1 SD = 0.77) | -0.106 | [-0.270, +0.086] | 0.257 |
| prereg_strict_vid_ratio | 96 | 22 | wb_brd (1 SD = 50.30) | -0.162 | [-0.348, +0.031] | 0.096 |
| main_local_yearFE | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.194 | [-0.561, +0.309] | 0.410 |
| main_local_yearFE | 47 | 11 | wb_brd (1 SD = 49.53) | -0.067 | [-0.329, +0.313] | 0.705 |
| main_local_trendonly | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.158 | [-0.379, +0.003] | 0.061 |
| main_local_trendonly | 47 | 11 | wb_brd (1 SD = 49.53) | -0.060 | [-0.142, +0.025] | 0.158 |
| main_local_trendonly | 47 | 11 | t (1 SD = 3.40) | +0.126 | [-0.064, +0.337] | 0.276 |
| main_upstream_yearFE | 47 | 11 | tmp_brd_up (1 SD = 0.86) | -0.296 | [-0.713, -0.003] | 0.044 |
| main_upstream_yearFE | 47 | 11 | wb_brd_up (1 SD = 44.94) | -0.171 | [-0.407, +0.028] | 0.195 |
| main_tmp_only | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.130 | [-0.314, -0.012] | 0.025 |
| main_wb_only | 47 | 11 | wb_brd (1 SD = 49.53) | +0.072 | [-0.038, +0.152] | 0.147 |
| main_winsorized | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.166 | [-0.478, +0.246] | 0.340 |
| main_winsorized | 47 | 11 | wb_brd (1 SD = 49.53) | -0.052 | [-0.282, +0.263] | 0.688 |
| main_interpolated | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.120 | [-0.479, +0.277] | 0.652 |
| main_interpolated | 47 | 11 | wb_brd (1 SD = 49.53) | -0.004 | [-0.268, +0.296] | 0.874 |
| main_vid_ratio | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.236 | [-0.560, +0.101] | 0.168 |
| main_vid_ratio | 47 | 11 | wb_brd (1 SD = 49.53) | -0.107 | [-0.339, +0.159] | 0.462 |
| main_SepOct_autumn | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.243 | [-0.603, +0.245] | 0.272 |
| main_SepOct_autumn | 47 | 11 | wb_brd (1 SD = 49.53) | -0.091 | [-0.350, +0.258] | 0.501 |
| main_with_winter | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.194 | [-0.591, +0.604] | 0.440 |
| main_with_winter | 47 | 11 | wb_brd (1 SD = 49.53) | -0.067 | [-0.562, +0.649] | 0.674 |
| main_with_winter | 47 | 11 | tmp_win (1 SD = 1.17) | +0.001 | [-0.311, +0.380] | 0.848 |
| main_min2years_yearFE | 61 | 18 | tmp_brd (1 SD = 0.76) | -0.103 | [-0.319, +0.208] | 0.625 |
| main_min2years_yearFE | 61 | 18 | wb_brd (1 SD = 50.49) | -0.005 | [-0.193, +0.261] | 0.793 |
| main_min2years_tmp_only | 61 | 18 | tmp_brd (1 SD = 0.76) | -0.099 | [-0.192, +0.013] | 0.079 |
| relaxed_speed_local_yearFE | 67 | 17 | tmp_brd (1 SD = 0.73) | -0.235 | [-0.457, +0.032] | 0.136 |
| relaxed_speed_local_yearFE | 67 | 17 | wb_brd (1 SD = 50.52) | -0.159 | [-0.383, +0.112] | 0.444 |
| main_North | 29 | 7 | tmp_brd (1 SD = 0.96) | -0.272 | [-0.608, +0.408] | 0.262 |
| main_North | 29 | 7 | wb_brd (1 SD = 36.96) | -0.082 | [-0.349, +0.221] | 0.421 |
| main_South | 18 | 4 | tmp_brd (1 SD = 0.48) | +0.213 | [-7.240, +2.299] | 0.558 |
| main_South | 18 | 4 | wb_brd (1 SD = 66.24) | +0.687 | [-10.431, +6.814] | 0.704 |
| main_2020_2024 | 28 | 9 | tmp_brd (1 SD = 0.65) | -0.030 | [-0.194, +0.226] | 0.726 |
| main_2020_2024 | 28 | 9 | wb_brd (1 SD = 41.25) | -0.030 | [-0.184, +0.158] | 0.725 |
| main_log_autumn | 47 | 11 | tmp_brd (1 SD = 0.81) | -0.051 | [-0.411, +0.215] | 0.289 |
| main_log_autumn | 47 | 11 | wb_brd (1 SD = 49.53) | -0.148 | [-0.553, +0.225] | 0.521 |
| main_log_spring | 47 | 11 | tmp_brd (1 SD = 0.81) | +0.143 | [-0.492, +0.533] | 0.830 |
| main_log_spring | 47 | 11 | wb_brd (1 SD = 49.53) | -0.081 | [-0.611, +0.344] | 0.714 |
| timing_spring_d50_vs_MarApr_tmp | 67 | 17 | tmp_spr (1 SD = 0.87) | +0.051 | [-1.213, +1.088] | 0.985 |
| timing_spring_d50_vs_MarApr_tmp_yearFE | 67 | 17 | tmp_spr (1 SD = 0.87) | +1.583 | [-0.686, +4.182] | 0.107 |
| timing_autumn_d50_vs_AugSep_tmp | 67 | 17 | tmp_aut (1 SD = 1.04) | -1.320 | [-3.302, +0.144] | 0.081 |
| timing_autumn_d50_vs_AugSep_tmp_yearFE | 67 | 17 | tmp_aut (1 SD = 1.04) | +0.831 | [-2.144, +5.444] | 0.592 |


Leave-one-out stability of `main_local_yearFE` (`files/results/leave_one_out.csv`): temperature slope -0.32 to +0.02, water-balance slope -0.15 to +0.08 when we remove one year or one radar.

## 6. Figures

* `files/figures/fig1_radars_and_qc.png`: radar map and QC funnel.
* `files/figures/fig2_seasonal_traffic.png`: median nightly traffic in clean years for six radars (a nldhl March 2017 clutter peak is visible and remains in the data).
* `files/figures/fig3_ratio_vs_summer.png`: ratio vs. summer anomalies after radar and year demeaning.
* `files/figures/fig4_coefficients.png`: all specifications.
* `files/figures/fig5_timing.png`: passage timing vs. temperature.

## 7. Limitations

* Small clean sample: 47-61 radar-years. The test can find only large effects (about 30-50% per SD).
* The South sample is very small (4 radars with >= 3 clean years; French radars only 2014-2015), so the North/South replication is not informative for the South.
* The speed rule was added after we saw outliers. We report the pre-specified result also.
* The ratio also depends on autumn passage routes, stop-over and juvenile survival before passage; radars detect all flying targets (insects partly removed by the vol2bird velocity-variance filter). The September-October-only ratio (less insect contamination) gave the same result.
* One local climate box per radar does not represent the true breeding area of the birds that pass. The upstream box gave similar results.
* Rain and clutter are not removed beyond the archive processing; nightly winsorising at the 99.5th percentile did not change the result.
* We did not test 2022 (no spring data) or 2025-2026 (no CRU data); the 2018 drought year failed QC at all radars.

## 8. What remains open

* Use radar data with homogeneous processing (for example the UvA/KNMI or national re-processed series, or raw volume re-processing with one vol2bird version) to obtain longer clean series. Then the same test has more power.
* Combine radar ratios with ringing-based productivity (for example constant-effort ringing) for the same regions to calibrate the index.
* Test 2025-2026 with ERA5 or E-OBS climate (the bucket has these years).

## 9. Reproduction

* `files/code/reproduce.sh SCRATCH_DIR` downloads the radar files and CRU files into SCRATCH_DIR and runs all steps (about 7.8 GB radar download; about 1 h on 2 CPUs plus download time). It never writes into the bundle.
* Step outputs bundled here (all derived from CC0 radar data or OGL CRU data): `files/data/nights.csv.gz` (nightly traffic for all 25 radars), `seasons.csv`, `regimes.csv`, `climate.csv`, `radars.csv`; `files/results/radar_years.csv` (analysis table with QC flags and climate), `models.json`, `leave_one_out.csv`.
* To repeat only the statistics: `python -I files/code/analysis.py files/data/seasons.csv files/data/regimes.csv files/data/climate.csv files/data/radars.csv OUTDIR` (seconds per spec; `NBOOT` environment variable sets bootstrap size).
* The per-timestamp parquet summaries (1,184 files) are not bundled; `fetch_process.py` regenerates them.
* External data terms: see `files/NOTICE-external-data.md`.

## References

* Desmet P. et al. 2025. Biological data derived from European weather radars. Scientific Data 12:361. doi:10.1038/s41597-025-04641-5
* Dokter A.M. et al. 2018. Seasonal abundance and survival of North America's migratory avifauna determined by weather radar. Nature Ecology & Evolution 2:1603-1609. doi:10.1038/s41559-018-0666-4
* Harris I., Osborn T.J., Jones P., Lister D. 2020. Version 4 of the CRU TS monthly high-resolution gridded multivariate climate dataset. Scientific Data 7:109. doi:10.1038/s41597-020-0453-3
