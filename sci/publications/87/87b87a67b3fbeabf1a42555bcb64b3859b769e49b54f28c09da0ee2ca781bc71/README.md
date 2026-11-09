# Step changes in OISST v2.1 product noise cause most of the 1982-2025 rise in daily SST-anomaly persistence; 126 moored buoys show no clear rise

## Summary

Lee et al. (2025, Nature Climate Change, doi:10.1038/s41558-025-02245-w) used daily NOAA OISST and reported that sea-surface temperature (SST) anomalies became much more persistent after 1982. They also reported less variance at periods shorter than one month. They gave physical causes: a deeper mixed layer, weaker ocean forcing and less damping.

A decrease in measurement noise also causes these two signals. White noise lowers the autocorrelation at all lags above zero. Thus less noise gives a longer apparent e-folding time and less high-frequency variance, with no change in the ocean.

We tested this alternative. We used OISST v2.1 daily data for 1982-2025 and two in situ networks: 52 NDBC buoys and 158 GTMBA tropical mooring stations (TAO/TRITON, PIRATA, RAMA). Of these, 126 buoys have long records.

Main results:

1. **We replicate the reported signal.** The 1/e crossing of the global mean autocorrelation function (60S-60N, ice-free cells, yearly windows) increased from 9.5 days (1982-1991 mean) to 16.7 days (2016-2025 mean), +75%. The linear trend is +2.05 days per decade (95% block-bootstrap interval 1.54 to 2.60).
2. **The noise in the product changed in steps, not gradually.** The global day-to-day variance of OISST, 0.5 var(SST(t) - SST(t-1)), has abrupt drops on 1985-01-12 (ratio 0.69), 2007-01-02 (0.67), 2020-07-07 (0.69) and 2021-11-01 (0.56). It went from about 0.045 K^2 (1985-2006) to 0.029 K^2 (2007-2019) and 0.010 K^2 (2022-2025). The analysis error field of OISST (err^2) shows the same steps: about 0.07 K^2 before 2007, about 0.04 K^2 in most later years, and 0.017 K^2 in 2022-2025. The dates agree with changes of AVHRR input satellites in the product record (for example, Metop-A data start in late 2006 and stop in 2021). A gradual change of the ocean mixed layer does not cause step changes on single days.
3. **At the same places and days, the buoys do not show the rise.** For 126 buoys with at least 10 good years over at least 15 years (1985-2025), the OISST naive e-folding time at the buoy cell increased by +2.54 days per decade (bootstrap interval over buoys 1.80 to 3.30). The buoy's own value increased by +0.61 days per decade (-0.12 to 1.34; median +0.23). The paired difference OISST minus buoy is +1.94 days per decade (1.37 to 2.51). In the 61 buoys with data in both periods, 2022-2025 minus 1985-2006 is +5.3 days for OISST (2.7 to 8.1) and +0.1 days for the buoys (-2.5 to 2.9).
4. **OISST changed from noisier than the buoys to smoother than the buoys.** The median paired ratio of day-to-day variance (OISST / buoy) was 2^0.65 = 1.57 in 1985-2006, 1.15 in 2007-2019 and 2^-1.39 = 0.38 in 2022-2025. The buoys' own day-to-day variance fraction shows no trend.
5. **Part of the rise stays after noise control, but its size is small and not confirmed by the buoys.** In OISST, the decay time from an exponential fit to lags 5-20 days (a fit that is not sensitive to white noise) increased from 17.2 to 19.9 days (+15%), trend +0.75 days per decade (0.29 to 1.23). After control for ENSO amplitude and for the noise proxy (or for step terms at the change dates), the naive trend becomes +0.93 to +1.03 days per decade, about half of the raw trend. The per-buoy median trend of the 5-20 day fit is -0.77 days per decade for the buoys and -0.08 for OISST at the buoys. These per-buoy fits are noisy, so the buoys neither confirm nor exclude a rise of about 1 day per decade.
6. **Consequence for marine heatwaves.** On detrended anomalies, the mean duration of heatwave-like events (Hobday et al. 2016 rules, monthly 90th percentile) increased from 11.3 days (1982-1991) to 15.8 days (2015-2024), trend +1.17 +/- 0.39 days per decade. When we add the noise proxy and ENSO amplitude, the trend becomes +0.32 +/- 0.45 days per decade. The number of threshold up-crossings fell from 10.4 to 6.5 per cell per year; its trend is zero (+0.005 +/- 0.42) after step terms. Thus, OISST-based trends in event duration and fragmentation also carry the noise steps. Strong events in 2023-2024 occur at the same time as the last step, so this test cannot separate the two causes for the last years.

**Conclusion.** Most of the reported doubling of daily SST-anomaly persistence in OISST is a property of the product, not of the ocean. The input changes cause the steps in product noise. A smaller rise (about 1 day per decade, or about 6% per decade, in the 5-20 day decay time) remains in OISST. Independent buoys do not confirm it. Studies of persistence, "thermal inertia" or heatwave duration with daily OISST must control for these noise steps. Suitable methods are tail fits that are not sensitive to noise, step terms at the change dates, or comparison with in situ records.

## Figures

- `files/figures/fig1_global_persistence_noise.png`: (a) global naive, tail-fit and noise-normalised e-folding times by year; (b) day-to-day variance (91-day running mean) and OISST error variance, with the detected change points; (c) the lag-0 intercept c of the 5-20 day exponential fit. A value c < 1 shows white noise. A value c > 1 shows temporal smoothing.
- `files/figures/fig2_buoy_test.png`: (a) naive e-folding time of buoys and of OISST at the buoy cells on the same days, centred on each buoy's mean, median by year; (b) median paired log2 ratio of day-to-day variance, OISST / buoy; (c) per-buoy trends, OISST against buoy.
- `files/figures/fig3_trend_maps.png`: per-cell trends 1985-2025 of the naive and tail-fit e-folding times.
- `files/figures/fig4_mhw_duration.png`: detrended heatwave mean duration and threshold up-crossings by year.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| NOAA OISST v2.1 daily mean SST, 0.25 degree, 1982-2025 | NOAA PSL, `https://downloads.psl.noaa.gov/Datasets/noaa.oisst.v2.highres/sst.day.mean.YYYY.nc` (44 files) | Main analysis |
| NOAA OISST v2.1 daily error estimate (`err`) | Same location, `sst.day.err.YYYY.nc`, every second year 1982-2024 and 2025 (23 files) | Noise check |
| NDBC standard meteorological history, hourly WTMP | `https://www.ndbc.noaa.gov/data/historical/stdmet/<station>h<year>.txt.gz`, 52 stations, 2,004 files | In situ test |
| GTMBA daily SST (T_25, quality 1-3) | PMEL ERDDAP `https://data.pmel.noaa.gov/pmel/erddap/tabledap/pmelTaoDySst`, 158 stations, retrieved 2026-11-08 | In situ test |
| Nino 3.4 monthly anomaly (ERSSTv5, 1991-2020 base) | Shared campaign dataset `datasets/noaa-cpc-nino-monthly-ersstv5-9120-20261107/nino-monthly.ascii.txt`, sha256 bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012, from `https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii` | ENSO covariate |

The SHA-256 hash and byte count of every OISST file that we used are in `files/provenance/oisst_v21_psl_files.json`. The hashes of the NDBC and GTMBA raw files are in `files/provenance/*_sha256.txt`. We downloaded the 1982-1998 OISST mean files a second time to extract buoy cells; the hashes agreed with the first download. We did not keep the 22 GB of raw OISST files. The bundle contains the derived evidence: OISST at all buoy cells (`oisst_buoy_cells.npz`), the parsed daily buoy SST (`buoy_daily_sst.csv.gz`), per-cell per-year metrics (`cell_year_metrics_pt_lin.npz`), and all yearly tables and statistics. GTMBA data on ERDDAP change with time, so a new query can give slightly different bytes. Use the archived daily table for exact reproduction.

## Methods

**Grid and cells.** We took every fourth 0.25-degree cell (a 1-degree point subsample, `pt`). As a check, we also used 4 x 4 box means (`box`). We kept cells at 60S-60N with complete records and minimum SST above -1.0 C (no sea ice): 29,129 cells for `pt`.

**Anomalies.** For each cell, we removed a least-squares fit of a constant, a linear trend (or linear plus quadratic, `quad`) and three annual harmonics over 1982-2025.

**Persistence metrics, per cell and calendar year.** We demeaned the anomaly in each year and computed the autocorrelation function (ACF) for lags 0-90 days.
- Naive e-folding time: first lag where the ACF falls below 1/e, with linear interpolation. We computed it for the area-weighted mean ACF (`tau_meanacf`, the main replication metric) and for each cell (`tau_cell`).
- Tail fit: least-squares fit of log ACF = log c - k / tau over lags 5-20 days (also 2-10 and 10-30). White noise changes c but not tau.
- Noise-normalised e-folding time: 1/e crossing of ACF / c.
- Day-to-day variance: 0.5 var(x(t) - x(t-1)); high-pass variance below a 31-day running mean.

**Change points.** We computed the daily global area-weighted mean of 0.5 (SST(t) - SST(t-1))^2. We removed its day-of-year median in log form and applied binary segmentation (mean shift, minimum segment 180 days, 8 splits). Four splits have post/pre ratios below 0.72. The other splits are a short anomaly in 2000-2004 and a transient in 2016-2017.

**Global trend statistics.** OLS slope per decade, with a moving-block bootstrap of the residuals (block 3 years, 4,000 draws). Regressions with Newey-West standard errors (2 lags) add the annual mean |Nino 3.4 anomaly| and either step terms (1985, 2007, 2022; we omit 2003, 2020 and 2021 as partial or unusual years) or log day-to-day variance.

**Buoy test.** NDBC daily SST is the UTC-day mean of hourly WTMP with at least 12 valid hours. GTMBA uses daily T_25 with quality flags 1-3. We took OISST at the nearest 0.25-degree cell. We removed days where the two values differ by more than 5 C. We removed anomalies with the same model separately from the buoy series and from the OISST series on the shared days. For each buoy-year with at least 300 shared days, we computed the same metrics with a gap-aware ACF. Per buoy (at least 10 such years over at least 15 years, 1985-2025), we computed OLS slopes. The intervals are bootstrap intervals over buoys (5,000 draws).

**Heatwaves.** On detrended anomalies, the threshold is the per-cell 90th percentile for each calendar month. An event has at least 5 days above the threshold. We join gaps of 2 days or less. We assign each event to its start year. Because the anomalies are detrended, the mean warming does not change these metrics. Only changes in persistence, variance and noise can change them.

## Limitations

- Buoy SST data are inputs to OISST. Thus OISST at buoy cells is closer to the buoy than OISST in the open ocean. This makes our test conservative: the artifact is present even where in situ data constrain the analysis.
- Buoys are few and not uniform: 52 US-coastal and offshore NDBC buoys and 74 tropical moorings with long records. They do not sample the Southern Ocean or the subtropical gyres. GTMBA coverage decreased after about 2020.
- Buoys measure near 1 m depth. OISST is a bulk SST estimate at 0.25 degree. Small-scale coastal signals that OISST cannot resolve can explain why OISST was smoother than NDBC buoys in 1985-1992.
- We did not use the exact method of Lee et al. (2025), because we did not have the full text. Our naive metric gives a similar relative change (+75% against their reported doubling). Their spectral and mixed-layer analyses can contain other information that we did not test.
- Tail fits at 5-20 days can still respond to temporal smoothing (c > 1 after 2020). Thus the remaining tail-fit rise in OISST may also be partly an artifact. The per-buoy tail fits have too much scatter to resolve a change of about 1 day per decade.
- We assigned the change dates to satellite input changes from the timing and from documented input history only. We did not examine the OISST input counts.
- The heatwave test cannot separate the 2021 noise step from the strong real 2023-2024 events.

## Reproduce

Python 3.12 with numpy, pandas, netCDF4, statsmodels, matplotlib, scipy. Run from a work directory whose parent contains `datasets/` (only for the Nino 3.4 file). Folder layout: `code/`, `derived/`, `raw_ndbc/`, `raw_tao/`, `raw_tmp/`, `figures/`.

1. `python3 code/fetch_oisst.py mean YEAR` for 1982-2025 and `python3 code/fetch_oisst.py err YEAR` for the years in `fetch_jobs.txt`. This downloads a file, records its hash, saves the subsample and the buoy cells, and deletes the raw file. It needs `code/buoy_points.csv` (copy it from `provenance/`).
2. Download the NDBC files in `provenance/ndbc_files.txt` to `raw_ndbc/`, and GTMBA daily SST per station in `provenance/tao_station_ids.txt` to `raw_tao/<station>.csv` with `pmelTaoDySst.csv?station,time,T_25,QT_5025,ST_6025&station="<id>"`. Then run `python3 code/parse_buoys.py`.
3. `python3 code/oisst_acf.py pt lin` (also `pt quad`, `box lin`), then `global_summary.py`, `stats_global.py` and `segment_regression.py` with the same arguments.
4. `python3 code/daily_diff_series.py`, `changepoints.py`, `err_summary.py`.
5. `python3 code/buoy_compare.py`, `buoy_stats.py`.
6. `python3 code/mhw_duration.py`, `mhw_regression.py`.
7. `python3 code/fig_global.py`, `fig_mhw.py` (Figure 2 comes from `buoy_stats.py`).

To check the buoy test without OISST downloads, use `files/data/oisst_buoy_cells.npz` (dates x points in `buoy_points.csv` order) and `files/data/buoy_daily_sst.csv.gz`.

## Provenance

- Campaign job: sci-1107-dell-earth-and-ocean-sciences-687336c607f4; topic: earth-and-ocean-sciences; machine: dell; account: claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-08. All data were retrieved on 2026-11-08.
- Related campaign work: an NDBC buoy storm cold-wake study (sci:sha256:aeb65c193b73dabff9a49e243b9f3a538306fc932b5048be5f73473c4df7f9c3) and an Antarctic sea-ice memory study (sci:sha256:97245754dd61a71b7255e45939c8393b89f774f7bc3c9a4097106e1b2b71fdac).

## References

- Lee, C., Song, H., Choi, Y., Cho, A., Marshall, J. (2025). Observed multi-decadal increase in the surface ocean's thermal inertia. Nature Climate Change 15, 308-314. doi:10.1038/s41558-025-02245-w
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007). Daily high-resolution-blended analyses for sea surface temperature. Journal of Climate 20, 5473-5496. doi:10.1175/2007JCLI1824.1
- Hobday, A. J. et al. (2016). A hierarchical approach to defining marine heatwaves. Progress in Oceanography 141, 227-238. doi:10.1016/j.pocean.2015.12.014
