# Most of the 1982-2025 rise in daily SST memory in DOISST v2.1 is a loss of fast variance that steps at satellite input changes and is absent in 34 NDBC buoys

## Summary

Lee et al. (2025, Nature Climate Change) used NOAA daily Optimum Interpolation SST (DOISST) to report that the memory of sea surface temperature (SST) anomalies increased across the global ocean after 1982. They estimated memory as tau10 = -10 / ln(phi10), where phi10 is the lag-10-day autocorrelation in each year. They related the increase to a deeper mixed layer and to weaker damping of SST anomalies.

We tested a different explanation: the analysed SST field possibly became smoother from day to day because the satellite input changed. A smoother field increases phi10 and tau10, but the decay rate of real anomalies does not change.

We did these steps:

1. We repeated the tau10 calculation on DOISST v2.1, 1982-2025, on 1-degree block means, for 29,423 ice-free cells between 60S and 60N.
2. We divided each yearly autocorrelation function (ACF) into two parts. We fitted phi_k = A exp(-k / tau_s) for lags k = 5 to 20 days. A is the share of variance in the slowly decaying part. tau_s is the decay time of that part. A synthetic test showed that this fit separates a loss of fast variance (A increases, tau_s does not change) from a real slowing (tau_s increases).
3. We examined breaks in the global series and compared them with the dates of documented DOISST input changes.
4. We compared DOISST with hourly in situ water temperature from 34 moored NDBC buoys, on the same days and in the same 1-degree cells.
5. We compared DOISST with three other SST products at weekly and monthly resolution.

## Main results

**R1. The reported increase repeats.** The 60S-60N mean tau10 increased from 11.5 days (1982-1986) to 22.6 days (2021-2025). The area-median cell trend was +1.71 days per decade. The Mann-Kendall test gave a significant positive trend (|z| > 1.96) in 63% of the ocean area and a significant negative trend in 0%. This agrees with Lee et al. (2025).

**R2. Most of the increase comes from the intercept A, not from the decay time tau_s.** We divided the trend of ln(phi10) into a part from ln A and a part from -10/tau_s. In the 60S-60N area, 66% came from A and 24% from tau_s. The fit residual gave the remaining 10%. In the tropics (20S-20N) the share from A was 73%. In the North Atlantic (20N-60N) it was 106%, and the tau_s part was negative. The area-median A trend was +0.056 per decade, with significant positive trends in 52% of the area. tau_s had significant positive trends in only 10% of the area and significant negative trends in 1%. The 60S-60N mean of the yearly tau_s fits decreased from 34.4 days (1982-1986) to 25.6 days (2021-2025). Fits to decade-mean ACFs gave a smaller increase of tau_s, from 16.1 to 19.6 days (Figure 2). The same fits gave an increase of A from 0.71 to 0.92. Thus, a moderate increase in slow decay time is possible in some regions, but it cannot explain most of the tau10 increase.

**R3. The fast variance fell in steps at the dates of satellite input changes.** The variance of the 1-day change of the anomaly (dvar) decreased by a factor of about 6 between 1982-1986 and 2021-2025. It decreased in 97% of the area (significant). The decrease was not smooth. A break search with no prior dates selected breaks at 2007 and 2021. These are the dates of two input changes that NCEI documents: on 2007-01-01, DOISST changed from Pathfinder AVHRR (one satellite) to operational Navy AVHRR (two satellites). On 2021-10-01, it changed from Navy AVHRR to NOAA ACSPO L3S (about five satellites, AVHRR and VIIRS). For tau10, a model with steps at the input-change dates (2007, 2016, 2022) gave BIC = 58.0. A linear trend gave BIC = 80.5. In segments with one input stream, the tau10 trend was small and not significant: +0.34 days per decade in 1982-2006 (z = 1.66) and +0.10 days per decade in 2007-2015 (z = 0.0).

**R4. Independent buoys do not show the change.** At 34 NDBC buoys (17N-57N, Pacific, Atlantic, Gulf of Mexico, Hawaii; median 29 station-years), with the same days used for both sources:

| Quantity (median over 34 stations) | NDBC buoy | DOISST at buoy cell |
|---|---|---|
| Trend of ln(dvar) per decade | -0.014 (21 of 34 negative) | -0.160 (30 of 34 negative) |
| dvar ratio, 2010-2025 to 1985-2000 | 0.99 | 0.79 |
| Trend of tau10 (days per decade) | -0.24 (22 of 34 negative) | +0.32 (19 of 34 positive) |

The paired Wilcoxon test for the difference in ln(dvar) trend (DOISST minus buoy) gave p = 1.1e-7. For the difference in tau10 trend it gave p = 5.4e-4 (median difference +0.65 days per decade). In 2023-2025, the station-median tau10 was 19-24 days in DOISST and 10-14 days in the buoys (Figure 5).

**R5. Other SST products do not show the same increase.** For 4-year blocks in 1982-2021, the lag-1-week ACF of DOISST weekly means increased by 0.027 per decade (Mann-Kendall z = 2.86). The older NOAA OI.v2 weekly product had a trend of 0.006 per decade (z = 0.36). At lag 1 month, DOISST had +0.010 per decade (z = 1.25), ERSST v5 (in situ only) had +0.010 per decade (z = 1.07), and HadISST had -0.041 per decade (z = -2.33). The 2022-2025 block had higher monthly persistence in all three monthly products. This block contains the 2023-2024 global ocean warm event and the 2021 input change, so we cannot separate the two causes.

## Interpretation

Our data agree with this explanation: most of the post-1982 increase in daily SST memory in DOISST is a change in the analysis, not a change in the ocean. The fast (day-to-day) part of the analysed SST variance became smaller in steps at satellite input changes. Moored buoys at the same places did not show a decrease in fast variance or an increase in tau10. A one-lag memory metric such as tau10 is sensitive to the share of fast variance. Thus, this metric is not a good measure of anomaly damping in a product that has changing inputs.

Our results do not show that the damping of SST anomalies did not change. Some regions (eastern equatorial Pacific, parts of the Southern Ocean) show positive tau_s trends (Figure 3). The decade-mean fits give a moderate global increase of tau_s. The buoys sample only part of the Northern Hemisphere ocean. A test of physical change in SST memory needs a metric that does not depend on the fast variance share (for example tau_s or ratios of long-lag correlations) and a homogeneous input record. Reprocessed satellite SST climate data records are possible candidates.

## Figures

- `files/figures/fig1_global_series.png`: 60S-60N annual means of tau10, A, tau_s and dvar. Dashed lines show the input changes in 2007, 2016 and October 2021.
- `files/figures/fig2_pooled_acf.png`: decade-mean ACF curves for 1982-1991 and 2016-2025. The late curves are higher mostly because the early fast drop at lags 1-5 days is missing.
- `files/figures/fig3_trend_maps.png`: maps of 1982-2025 Theil-Sen trends of tau10, A and tau_s.
- `files/figures/fig4_crossproducts.png`: weekly and monthly ACF in 4-year blocks for DOISST, OI.v2, HadISST and ERSST v5.
- `files/figures/fig5_buoy_check.png`: station-median dvar and tau10 for NDBC buoys and DOISST on matched days.

## Methods

**DOISST.** We used DOISST v2.1 AVHRR-only daily 0.25-degree files from NOAA PSL (`sst.day.mean.YYYY.nc`, 1982-2025). We made 1-degree block means (mean of valid 0.25-degree pixels; a cell needs 8 or more of 16 pixels). Lee et al. interpolated to 1 degree; our block means are similar but not the same. We kept cells between 60S and 60N with a complete record and a minimum SST above -1.0 C (ice-free). For each cell, we removed a least-squares fit of a constant, a linear trend and three annual harmonics over 1982-2025. This is the same anomaly definition as in Lee et al. (seasonal cycle and linear trend removed).

**Yearly ACF.** For each calendar year and cell, we calculated the sample ACF for lags of 1 to 40 days. We removed the year mean, and lag pairs did not cross the year end. tau10 = -10 / ln(phi10).

**Decomposition.** We fitted phi_k = A exp(-k / tau_s) for k = 5 to 20 days by least squares. We used an exact profile over A and a log-spaced grid of tau_s from 1 to 365 days (241 values). This fit does not remove cells with small ACF values. 1.3% of cell-years had tau_s at a grid edge. The trend of ln(phi10) is approximately the trend of ln A plus the trend of -10/tau_s, plus a fit residual.

**Synthetic test (`code/05_simulation.py`).** We used 1,000 synthetic cells and 44 years of 365 days. Each series was a slow AR(1) part (tau 15 days, variance 1), a fast AR(1) part (tau 2 days, variance 0.25) and white noise (variance 0.10). In scenario S1, the fast and noise variances decreased by 50%. tau10 increased by 0.31 days per decade, A increased, and tau_s did not change (median trend 0.0). In scenario S2, tau_s increased from 15 to 22 days. tau10 increased by 0.41 days per decade, and tau_s increased by 0.88 days per decade. With no change (S0), the false positive rates were near 2.5% for each sign. The 365-day ACF gives a downward bias in tau_s (10.9 days estimated for 15 days true). The bias does not change the sign of the trends.

**Trends and breaks.** We used Theil-Sen slopes and the Mann-Kendall test (normal approximation, no correction for autocorrelation) for each cell and for regional mean series. We used area weights cos(latitude). We calculated BIC for piecewise-constant models with 0 to 4 breaks (minimum segment 3 years, best breaks from an exhaustive search), for a linear model, and for a model with steps at the documented input-change years.

**Buoys.** We used NDBC historical standard meteorological files (hourly WTMP). We used daily means with 12 or more hourly values. We removed values more than 4 C from a 15-day running median. We removed a station fit of a constant, a trend and three harmonics. We used DOISST anomalies only on days with a valid buoy value. A station-year needs 250 or more valid days. A station needs 20 or more years, a first year before 1996 and a last year after 2014.

**Other products.** We used NOAA OI.v2 weekly (1982-2022), HadISST1 monthly, ERSST v5 monthly, and DOISST averaged to 7-day and calendar-month means. For each product, we removed the same anomaly fit. We calculated the ACF in 4-year blocks (block mean removed, lag pairs inside the block).

## Limitations

- DOISST assimilates ship and buoy data, so the NDBC buoys are not fully independent of DOISST. The buoys measure temperature at about 0.6-1.5 m depth, at one point. DOISST gives a 1-degree block mean. Buoy hulls and sensors also changed over the record. We used current station positions for all years.
- The buoys cover only US-operated sites from 17N to 57N. The buoy test does not cover the tropical Pacific, the Southern Ocean or the Indian Ocean.
- The Mann-Kendall significance does not correct for serial correlation (for example ENSO). The BIC comparisons use annual values that have serial correlation. Thus, the p-values and BIC differences are approximate.
- The 2022-2025 period contains both the ACSPO input change and a large global warm event in 2023-2024. Our data cannot separate their effects on persistence.
- We did not use the DOISST analysis error field. Our download of that field failed after 1991 (`code/07_error_link.py` is not included and was not run).
- tau_s from 365-day ACFs has a downward bias and much noise. Our decomposition uses only lags of 5 to 20 days.
- We did not repeat the stochastic-model attribution of Lee et al. (mixed layer depth, ERA5 fluxes).

## Reproduction

The commands below run from a work directory that has a `datasets` link to the shared campaign datasets. Python 3.12 with numpy, scipy, pandas, xarray, netCDF4 and matplotlib is necessary.

```
python code/01b_download_psl_coarsen.py 1982 2025   # about 21 GB download, 1-degree block means
python code/03_anomalies_acf.py                      # anomalies and yearly ACF (8 processes)
python code/04_analysis.py                           # tau10, A, tau_s, trends, attribution
python code/05_simulation.py                         # synthetic validity test
python code/06_crossproducts.py                      # weekly and monthly block ACF, all products
python code/12_crossproduct_trends.py
bash   code/09_download_ndbc.sh                      # NDBC buoy files
python code/10_buoy_check.py
python code/11_segments.py                           # breaks and segment trends
python code/08_figures.py
```

`code/01_download_doisst.sh` and `code/02_download_doisst_err_ice.sh` are earlier ERDDAP download scripts. The results do not use their output.

## Files

- `files/code/`: all analysis code. `common.py` has the ACF, fit and trend estimators.
- `files/results/main_results.json`: series, trends, attribution, pooled ACF and BIC for DOISST.
- `files/results/segments.json`: break search and segment trends.
- `files/results/buoy_check.json`, `buoy_station_trends.csv`, `buoy_station_years.csv`, `buoy_annual_medians.csv`: buoy comparison.
- `files/results/crossproduct_block_acf.json`, `crossproduct_trends.json`: other products.
- `files/results/simulation.json`: synthetic test.
- `files/data/doisst_global_annual_series.csv`: 60S-60N annual means.
- `files/data/doisst_cell_fields_1982_2025.npz`: per-cell yearly tau10, A, tau_s and per-cell trends (slope per year and Mann-Kendall z). `cell_index_180x360` gives the flat index on the 180 x 360 grid (latitude from -89.5, longitude from 0.5 east).
- `files/provenance/data_provenance.json`: source URLs, SHA-256 hashes and shared dataset paths. `ndbc_files_sha256.csv`: the 1,427 NDBC files with hashes.

## Provenance

- Campaign 11_07_2026. Job sci-1107-hp-earth-and-ocean-sciences-a9cafbf80d84. Topic earth-and-ocean-sciences. Machine hp. Account claude-myxtap. Model Claude Opus 5.5 (claude-opus-5-5). Date 2026-11-08.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- DOISST v2.1 daily files: https://downloads.psl.noaa.gov/Datasets/noaa.oisst.v2.highres/ (downloaded 2026-11-08; hashes per year in `data_provenance.json`).
- Shared datasets used in place: `noaa-psl-oisst-v2-sst-wkmean-1981-1989-20261108`, `noaa-psl-oisst-v2-sst-wkmean-1990-present-20261108`, `noaa-psl-oisst-v2-lsmask-20261108`, `noaa-psl-ersst-v5-sst-mnmean-20261108`, `metoffice-hadisst1-sst-20261108` (paths and hashes in `data_provenance.json`). HadISST is for academic research use; we do not redistribute the raw data.
- NDBC: https://www.ndbc.noaa.gov/data/historical/stdmet/ (downloaded 2026-11-08).
- DOISST input history: NCEI OISST product page (https://www.ncei.noaa.gov/products/optimum-interpolation-sst) and the NCEI OISST Climate Algorithm Theoretical Basis Document (CDR 01B-09).
