# ERA5 SST day-to-day variance rose 4.9-fold at the 2007 HadISST2-to-OSTIA switch and biases its heatwave trends; with one common noise spectrum ERA5 and OISST agree on detrended trends (60S-60N)

## Summary

Earlier campaign studies showed that NOAA OISST v2.1 lost fast (sub-monthly) variance in steps at its satellite-input changes, and that these steps bias marine heatwave (MHW) and marine cold-spell (MCS) statistics (sci:sha256:f50dc28f, sci:sha256:87b87a67, sci:sha256:69a00227, sci:sha256:cfeb640f, sci:sha256:819eea65). Those studies corrected one product and used buoys as the check. Two questions remained:

1. Does the other product that many MHW studies use, the ECMWF ERA5 reanalysis, have the same problem?
2. If two products with different input histories receive the same correction, do they then give the same MHW trends? This is a stronger test of the correction than a buoy test, because it covers the full ice-free ocean.

We read the ERA5 SST at 12 UTC for every day of 1979-2025 from the public ARCO-ERA5 store, at the same 28,805 ice-free one-degree sample cells (60S-60N) as the OISST studies. We measured the fast variance of both products, found the ERA5 change points, compared both products with 127-173 moored buoys, and calculated the Hobday et al. (2016) statistics for the published products and for homogenised versions.

Main results:

- **R1. ERA5 has a large step at the documented input change.** The day-to-day SST variance of ERA5 increased by a factor of 4.9 on exactly 2007-09-01, when the ERA5 SST lower boundary changed from HadISST2 to OSTIA (Figure 1a). Before this date, ERA5 has almost no variance at periods of 2-8 days: on matched buoy windows, ERA5 has 0.00-0.05 times the buoy power at these periods. After the change it has 1.0-1.9 times the buoy power at 2-5 days (2007-2013) (Figure 1b). We found five smaller ERA5 steps (1985-01-09 x0.73, 1995-05-28 x1.24, 2013-01-17 x0.55, 2016-11-11 x0.73, 2018-02-13 x1.97). OISST has steps in the opposite direction (Figure 1c). Thus ERA5 became noisier with time, and OISST became smoother.
- **R2. The ERA5 step biases ERA5 MHW statistics in the direction opposite to OISST.** At 127 buoys (per-buoy 1982-2025 trends on matched days), published ERA5 has an MHW frequency trend that is too low (ERA5 minus buoy, median -0.135 events per year per decade, 95% CI -0.235 to -0.075, p = 2e-6), an MHW peak-intensity trend that is too high (+0.085 C per decade, +0.053 to +0.118, p = 8e-12), and a false decrease of SST memory (lag-1 autocorrelation -0.019 per decade, p = 1e-21). Published OISST has the opposite peak-intensity and memory biases (-0.055 C per decade and +0.017 per decade). After homogenisation of each product to one common target spectrum, all these differences from the buoys become small and not significant for ERA5 (frequency +0.006, p = 0.9; peak intensity -0.011, p = 0.9; lag-1 autocorrelation +0.001) (Figure 5).
- **R3. Over the full ocean, published ERA5 and OISST disagree on MHW trends; the common correction removes most of the disagreement for the noise-sensitive statistics.** Area-mean 1982-2025 trends per decade, 60S-60N:

| Statistic (per decade) | OISST published | ERA5 published | OISST homogenised | ERA5 homogenised | ERA5 minus OISST, published | ERA5 minus OISST, homogenised |
|---|---|---|---|---|---|---|
| MHW frequency (events/yr) | +0.654 | +0.394 | +0.851 | +0.734 | -0.260 (-0.370 to -0.149) | -0.117 (-0.170 to -0.065) |
| MHW max intensity (C) | +0.005 | +0.095 | +0.053 | +0.037 | +0.090 (+0.071 to +0.109) | -0.016 (-0.024 to -0.008) |
| MHW mean intensity (C) | -0.007 | +0.034 | +0.015 | +0.010 | +0.041 (+0.033 to +0.049) | -0.005 (-0.009 to -0.001) |
| Annual max anomaly (C) | +0.106 | +0.201 | +0.206 | +0.182 | +0.095 (+0.075 to +0.115) | -0.023 (-0.036 to -0.010) |
| Annual min anomaly (C) | +0.292 | +0.108 | +0.184 | +0.125 | -0.184 (-0.218 to -0.149) | -0.059 (-0.076 to -0.042) |
| MCS max intensity (C) | +0.005 | -0.077 | -0.045 | -0.024 | -0.082 (-0.103 to -0.062) | +0.021 (+0.002 to +0.039) |
| MCS duration (days) | +0.754 | +1.036 | -0.283 | +0.092 | +0.282 (-0.151 to +0.705) | +0.375 (+0.131 to +0.632) |
| MHW duration (days) | +4.468 | +4.246 | +3.125 | +2.100 | -0.223 (-0.892 to +0.440) | -1.025 (-1.394 to -0.675) |
| MHW days (days/yr) | +21.0 | +16.5 | +21.8 | +16.3 | -4.5 (-6.3 to -2.6) | -5.5 (-7.0 to -4.0) |
| MHW cumulative intensity (C days/yr) | +29.9 | +22.2 | +31.0 | +22.7 | -7.7 (-10.1 to -5.4) | -8.3 (-10.5 to -6.2) |

The intervals are 95% moving-block bootstrap intervals (3-year blocks) of the trend of the annual ERA5-minus-OISST difference. The homogenisation removes 82% of the peak-intensity disagreement, 68-76% of the annual-extreme disagreements, 55% of the frequency disagreement and 74% of the MCS peak-intensity disagreement (Figure 2, Figure 3). The ERA5 excess of the peak-intensity trend is present over almost the full ocean, and it is gone after homogenisation (Figure 4c, d). The same signs occur in the tropics (20S-20N), the north (20N-60N) and the south (20S-60S) (`cross_table.csv`).

- **R4. The remaining disagreement comes from a different mean warming rate.** ERA5 warms 0.043 C per decade slower than OISST on these cells (0.148 against 0.190 C per decade, 1982-2025). The annual ERA5-minus-OISST mean difference falls from +0.13 C (1982-2001) to -0.03 C (2020-2025) (Figure 4a, b). At 127 buoys, the mean offset of OISST from the buoys drifts by +0.034 C per decade (95% CI +0.024 to +0.045; GTMBA moorings +0.050, NDBC -0.026) and the offset of ERA5 drifts by -0.009 C per decade (-0.015 to -0.004). Across cells, the trend difference of MHW days increases by 105 days per year per decade for each 1 C per decade of mean-warming difference (r = 0.72). At equal mean warming, the expected homogenised difference is small for peak intensity (-0.010 C per decade), MCS frequency (-0.008) and MHW frequency (+0.072), but not zero for MHW duration (-0.40 days per decade) (`cell_regression.csv`).
- **R5. With each product's own mean trend removed, the homogenised products agree on all event statistics.** When we remove each product's fitted linear trend before event detection (Figure 6), the homogenised ERA5 and OISST trends per decade are: MHW duration +0.67 and +0.62 days (difference +0.05, -0.26 to +0.35), MHW frequency -0.002 and -0.061 events/yr, MHW peak intensity +0.029 and +0.035 C, MCS duration +0.67 and +0.61 days, MCS frequency +0.005 and -0.052. Before homogenisation, the detrended products disagree in peak intensity by +0.096 C per decade (+0.078 to +0.114), in annual maximum anomaly by +0.138 C per decade and in annual minimum anomaly by -0.141 C per decade.
- **R6. Effect inside ERA5 alone.** When ERA5 is homogenised to its own 2013-2016 segment (the ERA5 segment closest to the buoys), the published ERA5 MHW frequency trend (+0.394) changes to +0.642 events per year per decade (+63%), the peak-intensity trend falls from +0.095 to +0.043 C per decade (the published value is 2.2 times too large), the MCS-duration trend falls from +1.04 to +0.27 days per decade, and the MHW-duration trend falls from +4.25 to +3.00 days per decade. MHW days change by less than 8%.
- **R7. Day-level agreement is low, and the correction does not improve it.** The Jaccard index of MHW days (days in an MHW in both products divided by days in either) is only 0.28 in 1982-2006 (annual range 0.20-0.45) and 0.61 in 2015-2025, when the warming trend dominates. Homogenisation adds independent noise, so it does not increase this agreement (0.28 and 0.54). A 32-day low-pass raises it to 0.37 and 0.67.
- **R8. Sensitivity.** On every fourth chunk of cells, cutoff periods of 16 and 64 days and a second noise realisation change the homogenised trends by at most 0.25 days per decade (MHW duration), 0.06 events per year per decade (frequency) and 0.004 C per decade (peak intensity) (`sensitivity.csv`). The 32-day low-pass (no fast variance) gives the same signs for peak intensity and annual extremes, but it changes the event definition (duration trends +8.9 to +12.3 days per decade), so we do not recommend it as an MHW metric.

## Interpretation

ERA5 is a second widely used daily SST product with a large fast-variance inhomogeneity. Its inhomogeneity is a step at a documented input change (HadISST2 to OSTIA, 2007-09-01), and its sign is opposite to OISST: ERA5 gets noisier with time, while OISST gets smoother. Thus the two products give opposite artifacts in the statistics that depend on the tails of daily anomalies and on the event structure. Published ERA5 doubles the 1982-2025 trend of MHW peak intensity, underestimates the rise in MHW frequency by about 40%, and shows a false loss of SST memory. Published OISST hides the peak-intensity rise and overestimates the duration rise.

When both products receive the same sub-monthly spectrum, their trends of MHW peak and mean intensity, annual maximum anomaly and cold-spell peak intensity agree within 0.005-0.023 C per decade (annual minimum anomaly: 0.059, from 0.184), and their detrended event statistics agree within about 0.06 per decade. This is an independent test of the spectral homogenisation of sci:sha256:819eea65 over the full ice-free ocean: two products with different inputs and opposite artifacts converge after one common correction. The consistent homogenised estimates are: MHW peak intensity rises by 0.04-0.05 C per decade, MHW frequency rises by 0.73-0.85 events per year per decade, the annual maximum anomaly warms by 0.18-0.21 C per decade, and the annual minimum anomaly warms by 0.12-0.18 C per decade (common-target versions of both products).

The statistics that mostly count exceedance days (MHW days, area, cumulative intensity) are robust to the noise steps in both products, as the earlier studies found for OISST. But they depend on the mean warming rate, and the two products differ by 0.043 C per decade. This mean-warming difference, not noise, explains most of the remaining MHW-day and duration difference (about 4.5-5.5 MHW days per year per decade, 21-25%). The buoys suggest a warm drift of OISST at the tropical moorings, but the buoys sample only the tropics and US waters, so this study does not decide which global mean trend is correct.

For users: an MHW trend from published daily ERA5 or OISST that depends on event count, duration, peak intensity, or annual extremes is product-dependent and partly artifact. A common-spectrum homogenisation, or comparison of detrended statistics, removes most of the product dependence. MHW-day trends need a check of the mean warming rate.

## Limitations

- The homogenisation corrects only second-order (spectral) properties at periods shorter than about 32 days (taper to 64 days). Noise that it adds is independent of the ocean, so it cannot recover the timing of real fast variations (R7). Before 2007-09-01 ERA5 has almost no 2-8 day variance, so in this period almost all fast variance of homogenised ERA5 is synthetic.
- The common target is the 2016-01-01 to 2020-07-06 OISST spectrum of each cell. This segment is near the buoys (sci:sha256:819eea65) but it is short and includes the end of the 2015-2016 El Nino. The trend levels depend a little on the target (R6, R8); the cross-product agreement is the main test.
- ERA5 has less variance than OISST at 16-64 days in all segments (about 0.6-0.8 times). Periods longer than 64 days are not changed, and this offset can affect the levels of intensity statistics and part of the remaining duration difference.
- ERA5 change points other than 2007-09-01 come from a change-point search on the same data (`dvar_changepoints.json`). We did not find documentation for them; they can be changes of the operational OSTIA system. The search uses an area mean and can miss regional steps.
- We read ERA5 at 12 UTC only. ERA5 SST changes once per day, with small changes within the day; a daily mean can differ slightly. ERA5 points are 0.125 degree north and east of the OISST pixel centres, and they are interpolated by ARCO-ERA5 to 0.25 degree.
- Buoys are inputs to OISST, HadISST2 and OSTIA, so the buoy test is not independent. The buoys cover only the tropical moorings and US waters. Per-buoy duration trends have a large scatter.
- The cell sample uses one point per one-degree box between 60S and 60N; we did not test higher latitudes, box means or the native ERA5 grid.
- Bootstrap intervals use annual area means with 3-year blocks; they do not include the uncertainty of the method (R8 gives an estimate).

## Figures

- `files/figures/fig1_fast_variance.png`: (a) monthly day-to-day anomaly variance of ERA5 and OISST, with ERA5 (dotted) and OISST (dashed) segment boundaries; (b, c) median product/buoy power ratio by period in each ERA5 and OISST segment.
- `files/figures/fig2_trends.png`: 1982-2025 area-mean trends of nine statistics for published, homogenised and low-pass versions of both products, with 95% intervals.
- `files/figures/fig3_series.png`: annual area means of MHW duration, frequency, peak intensity and MCS duration for published and homogenised ERA5 and OISST.
- `files/figures/fig4_maps.png`: (a) ERA5 minus OISST mean SST trend; (b) annual area-mean ERA5 minus OISST difference; (c, d) ERA5 minus OISST MHW peak-intensity trend, published and homogenised.
- `files/figures/fig5_buoys.png`: per-buoy trend differences (product minus buoy) for published and homogenised versions.
- `files/figures/fig6_detrended.png`: trends of event statistics with each product's own linear trend removed.

## Methods

**Data.** OISST v2.1 AVHRR-only daily files (NOAA PSL, 1982-2025; shared campaign datasets `noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109`; all 44 SHA-256 values agree with the dataset records). We used the native 0.25-degree pixel at index (1::4, 1::4) (the sample of sci:sha256:87b87a67 and sci:sha256:819eea65): 29,129 ice-free pixels, 60S-60N. ERA5: variable `sea_surface_temperature` from the ARCO-ERA5 Zarr store, one chunk (hour 12 UTC) per day, 1979-01-01 to 2025-12-31 (17,167 chunks, read 2026-11-10). We kept the 0.25-degree ERA5 point at row and column index (2::4, 2::4), which is 0.125 degree north and east of each OISST pixel, and the nearest ERA5 point to each buoy. Common cells: ERA5 valid on all 16,071 days of 1982-2025 and minimum SST above -1.0 C: 28,805 cells. Buoys: daily NDBC and GTMBA SST and OISST at the buoy cell from the signed bundle sci:sha256:87b87a67; we removed days where either product differs from the buoy by 5 C or more, and kept 173 buoys with at least 900 matched days.

**Fast variance and change points (`03_dvar_changepoints.py`).** Anomaly = SST minus a least-squares fit of a constant, a linear trend and three annual harmonics (1982-2025). Daily series: area-weighted mean of half the squared day-to-day anomaly difference. ERA5 change points: binary segmentation for mean shifts on the deseasonalised monthly log10 series (BIC-type penalty, at most six breaks, segments of at least 12 months), then a refinement of each break day on the daily series (+/- 3 months). We used all six detected ERA5 breaks as segment boundaries. OISST segments are those of sci:sha256:819eea65.

**Buoy spectra (`07_buoy_spectra.py`).** Same gap-free 128-day windows for buoy, OISST and ERA5, Hann window, linear detrend, per-buoy mean periodograms, median over buoys of the log2 product/buoy ratio, grouped by ERA5 segments and by OISST segments.

**Homogenisation (`common2.py`).** Welch spectra (128-day Hann windows, 50% overlap, 5-bin smoothing) per cell and segment. `match_to`: in each product segment, where the segment has more power than the target, the anomaly is filtered with gain sqrt(target/segment); where it has less, Gaussian noise with spectrum (target - segment) is added. The change is tapered from full at periods of 32 days and less to zero at 64 days (cosine in log frequency). This is the "match" method of sci:sha256:819eea65 with an external target and product-specific segments. Common target (versions `O_match`, `E_match`): the OISST 2016-01-01 to 2020-07-06 spectrum of the same cell. ERA5 own target (`E_own`): the ERA5 2013-01-17 to 2016-11-10 spectrum of the cell. Low-pass (`O_lp`, `E_lp`): gain zero at periods of 32 days and less, one at 64 days and more. The median segment ratio to the target after matching is 0.86-1.09 at 4-16 days (`spectra_summary.json`).

**MHW and MCS statistics.** `mhwlib.py` of sci:sha256:819eea65 (unchanged; it agrees with the reference code ecjoliver/marineHeatWaves to better than 2e-11): 1983-2012 baseline, 90th/10th percentile thresholds from +/- 5-day windows, 31-day smoothing, events of 5 days or more, gaps of 2 days or less joined, events counted in their start year. Detrended versions remove each product's fitted linear trend before detection. Event-day agreement: per cell and year, the number of days in an MHW in both products divided by the number in either. Buoy statistics (`08_buoy_mhw.py`): the rules of sci:sha256:819eea65 (climatology from all matched days, events end at gaps, station-years with at least 300 valid days, per-buoy OLS trends with at least 10 station-years over at least 15 years); the homogenisation is applied to the gap-free product series at the buoy, with the OISST 2016-2020 spectrum of the buoy cell as the common target.

**Statistics.** Area weights cos(latitude). Duration and intensity means use only cell-years with events. OLS trends per decade of annual area means; 95% moving-block bootstrap of residuals (3-year blocks, 4,000 draws). Cross-product effects: trend of the annual ERA5-minus-OISST difference with the same bootstrap. Buoy tests: Wilcoxon signed-rank test and bootstrap interval of the median (4,000 draws). Cell regression (`14_cell_regression.py`): weighted least squares of the per-cell trend difference on the per-cell mean-warming difference, bootstrap over 10 x 10 degree boxes (2,000 draws).

## Reproduction

Python 3.12 with numpy 2, scipy, pandas, matplotlib, netCDF4 and numcodecs. In a work directory WORK, copy `files/code/` to `WORK/code` and run `bash code/run_all.sh <path to the 87b87a67...zip>`. The script lists all steps in order. The ERA5 fetch (`01_fetch_era5.py`) transfers about 22 GB over anonymous HTTPS, keeps only the sampled points (4.4 GB local scratch), is resumable, and records the SHA-256 of each chunk; compare it with `files/provenance/era5_arco_chunk_sha256.txt.gz`. ARCO-ERA5 can be updated by its maintainers; the chunk hashes show if the values changed. On the loaded campaign machine the fetch took 65 minutes, the main grid run 35 minutes on 10 processes, and the detrended and sensitivity runs 40 minutes.

## Files

- `files/code/`: all code. `mhwlib.py`, `degrade.py`, `common.py`, `01_extract.py`, `04_build_matrix.py` and `06_buoy_mhw.py` come unchanged from sci:sha256:819eea65; the other files are new.
- `files/results/trend_table.csv`, `trend_table_dt.csv`: trends and intervals per version, statistic and region (published, homogenised, own-target, low-pass; detrended).
- `files/results/cross_table.csv`, `cross_table_dt.csv`: ERA5-minus-OISST trend differences for each version pair.
- `files/results/series.csv`, `series_dt.csv`: annual regional means of all statistics and the event-day agreement.
- `files/results/cell_trends.npz`, `cell_trends_dt.npz`, `mean_trend.npz`: per-cell 1982-2025 trends (cell index into the OISST sample; see `02_build_era5.py`).
- `files/results/cell_regression.csv`, `mean_diff_year.csv`, `sensitivity.csv`, `spectra_summary*.json`, `era5_segments.json`, `dvar_changepoints.json`, `dvar_daily.csv.gz`.
- `files/results/buoy_spectra3.json`, `buoy3_station_years.csv`, `buoy3_trends.csv`, `buoy3_mean_offset.csv`: buoy tests.
- `files/provenance/data_provenance.json`: OISST file paths, URLs, sizes and SHA-256; ERA5 store and access details; prior bundle hashes. `era5_arco_chunk_sha256.txt.gz`: per-chunk ERA5 hashes. `era5_fetch_meta.json`: sampling and buoy-point indices.
- `files/NOTICE.md`: external data terms and required attribution.

## Data sources and terms

See `files/NOTICE.md`. Raw ERA5, OISST and buoy files are not in this bundle. ERA5 is CC BY 4.0 (Copernicus Climate Change Service); the derived ERA5 values in this bundle contain modified Copernicus Climate Change Service information. OISST and buoy data are NOAA products (US Government works).

## Provenance

- Campaign 11_07_2026; job sci-1107-dell-earth-and-ocean-sciences-617e0fe148ed; topic earth-and-ocean-sciences; machine dell; account claude-olen.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-10. ERA5 read 2026-11-10 from ARCO-ERA5 (store attribute last_updated 2026-11-09).

## References

- Hersbach, H. et al. (2020). The ERA5 global reanalysis. Quarterly Journal of the Royal Meteorological Society 146, 1999-2049. doi:10.1002/qj.3803
- Hirahara, S., Balmaseda, M. A., de Boisseson, E., Hersbach, H. (2016). Sea surface temperature and sea ice concentration for ERA5. ERA Report Series 26, ECMWF.
- Carver, R. W., Merose, A. (2023). ARCO-ERA5: An analysis-ready cloud-optimized reanalysis dataset. 22nd Conference on AI for Environmental Science, AMS.
- Good, S. et al. (2020). The current configuration of the OSTIA system for operational production of foundation sea surface temperature and ice concentration analyses. Remote Sensing 12, 720. doi:10.3390/rs12040720
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Hobday, A. J. et al. (2016). A hierarchical approach to defining marine heatwaves. Progress in Oceanography 141, 227-238. doi:10.1016/j.pocean.2015.12.014
- Oliver, E. C. J. et al. (2018). Longer and more frequent marine heatwaves over the past century. Nature Communications 9, 1324. doi:10.1038/s41467-018-03732-9
- Campaign studies: sci:sha256:819eea65, sci:sha256:cfeb640f, sci:sha256:87b87a67, sci:sha256:f50dc28f, sci:sha256:69a00227, sci:sha256:48ad9d2c, sci:sha256:825d6796, sci:sha256:b4e19931, sci:sha256:77b0a90c, sci:sha256:4e3a13fa, sci:sha256:5d8902f2.
