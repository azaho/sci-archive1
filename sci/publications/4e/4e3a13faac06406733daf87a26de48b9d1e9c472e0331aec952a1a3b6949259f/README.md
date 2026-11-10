# DOISST v2.1 input changes put steps of up to x3 into 1982-2024 SST front statistics that ESA CCI v3 lacks; CCI steps at its own sensor changes, and with step terms both agree on small trends

## Summary

Three earlier campaign studies found that the 1982-2025 rise in daily SST-anomaly memory in NOAA DOISST v2.1 is mostly a loss of fast temporal variance. This loss steps at satellite input changes (sci:sha256:f50dc28f..., sci:sha256:87b87a67..., sci:sha256:69a00227...). All three studies examined statistics in time. Many climate studies also use DOISST for statistics in space: SST gradients, ocean fronts, front frequency and small-scale SST variance. Some of these studies report trends of front intensity (for example, Chen et al. 2022 used DOISST and three other products for the Japan/East Sea Subpolar Front).

**Question.** Do the DOISST input changes also put steps into spatial SST statistics? If so, how much of the reported 1982-2024 change in fronts and gradients is a product artifact, and what change remains?

**Approach.**

1. We calculated daily spatial statistics of DOISST v2.1 (0.25 degree, 1982-01-01 to 2025-12-31, 16,071 days) on 28,458 ice-free 1-degree cells (60S-60N): the mean gradient magnitude |grad SST|, the area fraction of fronts (|grad SST| > 1, 2 and 4 K per 100 km), the variance inside each 1-degree cell, and zonal and meridional structure functions S(r) = mean (SST(x + r) - SST(x))^2 at r = 1 to 16 pixels (about 28 to 445 km at the equator). We searched for change points in each daily series and compared them with the documented DOISST input changes.
2. We fetched ESA SST CCI Analysis v3.0.1, a satellite-only climate data record, at the same 0.25-degree pixel centres on every 5th day (3,103 days, 1982-01-01 to 2024-06-22). We used one zonal row of pixels per degree of latitude (113,702 common pixels). On these pixels and days we calculated the same zonal statistics for both products.
3. We fitted trends with and without step terms at each product's own input-change dates. We tested this adjustment with 200 sets of random step dates.
4. We repeated a published front metric (Japan/East Sea Subpolar Front intensity) in both products.

## Main results

**R1. DOISST spatial statistics step on the dates of input changes (Figure 1).** The daily change-point search found breaks on 1985-01-11 to 1985-01-15, on 2006-12-22 to 2007-01-05 and on 2020-06-16 to 2020-07-10 in all spatial statistics. These dates agree with the day-to-day-variance steps of sci:sha256:69a00227 (1984-10 to 1985-01, 2007-01-02, 2020-06-28). The 2007 date is the documented change from Pathfinder AVHRR to Navy AVHRR (2007-01-01). The sign of the steps depends on the region:

| DOISST full grid, step ratio (365 days after / before; deseasonalised) | 1984-10-09 | 2007-01-01 | 2020-06-28 | 2021-10-01 |
|---|---|---|---|---|
| Strong-front fraction, |grad SST| > 4 K/100 km, 60S-60N | 0.69 | **1.74** | 0.91 | 1.15 |
| Strong-front fraction, western boundary currents (WBC) | 0.76 | **1.69** | 0.90 | 1.12 |
| Variance inside 1-degree cells, WBC | 0.88 | **1.45** | 0.93 | 1.09 |
| Mean |grad SST|, WBC | 0.95 | **1.14** | 0.96 | 1.00 |
| Mean |grad SST|, 20S-20N | 0.94 | **0.90** | 0.93 | **0.90** |

For each step, we compared the step size with the same statistic at all dates more than one year from the test dates (2,392 placebo dates for daily data, 2,280 for 5-day data). For the 2007 step in the global and WBC strong-front fraction, in the WBC cell variance and in the WBC mean gradient, no placebo date gave a step as large (placebo fraction 0.000). At 2007, the mean gradient increased at the large fronts (Gulf Stream, Brazil-Malvinas, Agulhas return current, equatorial Pacific cold tongue) and decreased in most of the quiet ocean (Figure 4a). In 2022-2023 relative to 2019-2020, it decreased in 78% of the ocean area (Figure 4b). The gradient distribution became wider after 2007: weak and strong gradients became more frequent, and gradients near 1 K/100 km became less frequent (Figure 8). Over 1982-2025, the DOISST strong-front fraction increased by +0.22 ln units per decade (95% interval +0.14 to +0.30), and its 2022-2025 mean was 2.1 times its 1982-2006 mean. Inside 1982-2006 its trend was -0.08 ln units per decade.

**R2. ESA CCI does not show the 2007 step (Figures 2, 3).** On the common pixels and days:

| Step ratio at 2007-01-01 | DOISST | CCI | DOISST / CCI |
|---|---|---|---|
| Fraction of zonal |dSST/dx| > 4 K/100 km, 60S-60N | 2.61 | 0.99 | 2.65 |
| Same, WBC | 3.04 | 0.98 | 3.11 |
| Fraction > 2 K/100 km, WBC | 1.41 | 1.00 | 1.40 |
| Mean zonal |dSST/dx|, WBC | 1.20 | 0.99 | 1.21 |
| S(28 km), WBC | 1.72 | 0.96 | 1.79 |
| S(445 km), WBC | 1.35 | 1.03 | 1.32 |

The placebo fraction was 0.000 for DOISST and the ratio, and 0.42 to 0.86 for CCI. The 2007 step in DOISST is almost the same from 28 to 222 km (x1.12 to x1.15, 60S-60N) and smaller at 445 km (x1.07). The 2020-06-28 DOISST step decreases with scale (x0.89 at 28 km, x0.99 at 445 km), which agrees with more smoothing at small scales. CCI did not change on these dates (x0.98 to x1.03) (Figure 3).

**R3. The raw trends of the two products are different (Figures 2, 5, 6a).** For 1982-2023 (ln units per decade, 95% block-bootstrap interval):

| Statistic | Region | DOISST | CCI |
|---|---|---|---|
| Mean zonal gradient | 60S-60N | -0.031 (-0.044 to -0.019) | +0.024 (+0.001 to +0.047) |
| Mean zonal gradient | 20S-20N | -0.115 (-0.140 to -0.090) | -0.053 (-0.078 to -0.029) |
| Mean zonal gradient | WBC | +0.059 (+0.033 to +0.084) | +0.050 (+0.028 to +0.071) |
| Fraction > 4 K/100 km | 60S-60N | +0.340 (+0.204 to +0.476) | +0.165 (+0.111 to +0.220) |
| Fraction > 4 K/100 km | WBC | +0.387 (+0.243 to +0.528) | +0.105 (+0.066 to +0.144) |
| S(28 km) | 60S-60N | +0.012 (-0.020 to +0.043) | +0.099 (+0.054 to +0.142) |

Per 1-degree cell, the DOISST zonal-gradient trend was significantly negative in 60% of the area and significantly positive in 6%. For CCI, the values were 37% and 30%. The global mean gradient trend has opposite signs in the two products.

**R4. CCI also has steps, at the dates of its own input changes.** The change-point search on the CCI series found breaks on 1985-02-19 to 1985-03-01, 1991-11-05, 2012-04-08 to 2012-06-02, 2016-05-22 and 2018-06-21. In the step model for S(28 km), 60S-60N, the CCI step ratios were x1.23, x1.27, x0.85, x1.27 and x1.14. These dates agree in time with the start of NOAA-9 AVHRR (1985), the start of ATSR-1 on ERS-1 (launched July 1991), the loss of Envisat AATSR (April 2012) and the launches of Sentinel-3A (February 2016) and Sentinel-3B (April 2018) SLSTR. We did not verify these dates in the CCI processing record. Between steps, the CCI small-scale statistics often decreased slowly (for example 2003-2015, Figure 2). Thus CCI is also not homogeneous for spatial statistics, and its raw trends are not a reference for real change. At 1985, the two products changed in opposite directions (DOISST x0.82 to x0.85 at all scales, CCI x1.00 to x1.06).

**R5. With step terms at each product's input-change dates, the products agree on small trends (Figure 6).** We fitted ln(statistic) = a + b t + steps, with steps for DOISST at 1985-01-15, 2007-01-01, 2020-06-28 and 2021-10-01, and steps for CCI at the five dates in R4. Over 41 combinations of 7 statistics and 6 regions, the median absolute DOISST-CCI difference of the trend decreased from 0.068 (raw) to 0.022 ln units per decade. The fraction of combinations with a difference below 0.03 increased from 7% to 63%. With 200 sets of random step dates (4 for DOISST, 5 for CCI), the median difference was 0.136 (2.5-97.5%: 0.037 to 0.321), and no set gave a value as small as 0.022. Thus the input-change steps explain most of the disagreement between the products. After adjustment:

- Global strong-front fraction (> 4 K/100 km): DOISST +0.061 (+0.016 to +0.103), CCI +0.038 (+0.010 to +0.066). This is a 4-6% increase per decade, not the raw +0.34 (+40% per decade) of DOISST.
- WBC mean zonal gradient: DOISST +0.011 (-0.002 to +0.023), CCI -0.006 (-0.020 to +0.008). We found no detectable trend.
- S(445 km), 60S-20S: DOISST +0.033 (+0.016 to +0.053), CCI +0.048 (+0.029 to +0.066). Both products show an increase of the large-scale SST contrast in the southern extratropics.
- 20S-20N small-scale statistics: the products still disagree (mean gradient: DOISST -0.020, CCI -0.118). The CCI step adjustment does not remove its drift between steps.

**R6. A published front trend contains the DOISST step (Figure 7).** For the Japan/East Sea Subpolar Front (maximum meridional gradient at 38-41N, mean over 128-138E, from monthly-mean SST; after Chen et al. 2022), the 1985-2020 DOISST trend was +0.23 K/100 km per decade (+0.12 to +0.34). Inside 1985-2006 and 2007-2020, the trends were -0.06 and -0.01. The 4-year step at 2007 was +0.77 K/100 km, larger than all 27 placebo 4-year contrasts. CCI on the same pixels and days had a trend of +0.12 (+0.04 to +0.20) and a step of +0.57 at 2007. Both steps occur in winter 2007 (January-March means: DOISST 3.4 to 4.4, CCI 5.4 to 5.9 K/100 km). The DOISST-CCI difference had a step of +0.35 K/100 km in mid-2006 and a trend of +0.11 (+0.03 to +0.19). Thus about half of the DOISST trend is specific to DOISST. Our data cannot tell whether the part common to both products is real, because both products added Metop-A AVHRR data near this time.

## Interpretation

The DOISST input-change artifact that earlier studies found in time statistics is also present in space statistics. The 2007 change to Navy AVHRR made strong fronts sharper and the quiet ocean smoother. The 1985 and 2020 steps made the field smoother at all scales or at small scales. Front-frequency and front-intensity trends from DOISST are therefore dominated by one step on 2007-01-01. Tropical gradient trends from DOISST have about double the negative trend of CCI.

A satellite-only climate data record does not solve this problem automatically. CCI v3 has steps of similar size at its own sensor changes, mostly upward at the start of a new dual-view radiometer. When each product receives step terms at its own input dates, most of the disagreement between them goes away, and the remaining trends are small: about +4 to +6% per decade for the strong-front fraction, no detectable trend for the mean WBC gradient, and about +3 to +5% per decade for the 445-km structure function in the southern extratropics. These adjusted trends are the best estimate that these two products give of real change. They depend on the step dates, and the tropical estimates still disagree.

Studies of SST fronts, gradients or small-scale variance that use DOISST (or any analysis that merges changing satellite inputs) must test for steps at the input-change dates, and they should compare at least two products with different input histories.

## Figures

- `files/figures/fig1_doisst_daily_spatial.png`: DOISST daily mean |grad SST|, strong-front fraction, sub-1-degree variance and 28-km zonal structure function, 60S-60N, WBC and 20S-20N.
- `files/figures/fig2_doisst_vs_cci_annual.png`: DOISST and CCI annual series on the same pixels and days.
- `files/figures/fig3_step_scale_dependence.png`: step ratio against spatial lag for DOISST, CCI and their ratio.
- `files/figures/fig4_doisst_step_maps.png`: DOISST 2-year contrasts of ln |grad SST| at 2007 and 2022.
- `files/figures/fig5_gradient_trend_maps.png`: per-cell trends of ln zonal gradient, DOISST, CCI and difference.
- `files/figures/fig6_trend_agreement.png`: DOISST against CCI trends for 41 statistic-region combinations, raw and with step terms.
- `files/figures/fig7_case_spf.png`: Japan/East Sea Subpolar Front intensity in both products.
- `files/figures/fig8_doisst_gradient_distribution.png`: DOISST gradient distribution in three input periods.

## Methods

**Data.** DOISST v2.1 AVHRR-only daily mean SST, 0.25 degree, NOAA PSL files `sst.day.mean.YYYY.nc` for 1982-2025, used in place from the shared campaign store (SHA-256 hashes in `files/provenance/data_provenance.json`). ESA SST CCI Analysis L4 v3.0.1 (CDR to 2021, ICDR from 2022), OPeNDAP subsets at CEDA: `analysed_sst[0][602:20:2997][2:5:7199]` (row grid) and `analysed_sst[0][2552:5:2627][6162:5:6357]` (Subpolar Front box), on 1982-01-01 + 5n days up to 2024-06-22. These CCI 0.05-degree pixel centres are also DOISST pixel centres. All 3,103 days were fetched for both subsets; no day was missing. The analysis mask is the 28,458 ice-free 1-degree cells of sci:sha256:69a00227 (both products valid on all days and minimum SST above -1 C).

**DOISST full-grid statistics.** Gradient: centred differences in both directions, distance on the sphere (R = 6,371 km), in K per 100 km, valid where the pixel and its four neighbours are in the mask. Front fractions: area fraction of valid pixels above 1, 2 and 4 K per 100 km. Sub-1-degree variance: variance of the 16 pixels of each 1-degree cell where all 16 are valid. Structure functions: zonal and meridional mean squared differences at lags of 1, 2, 4, 8 and 16 pixels. All means use cos(latitude) weights. Regions: 60S-60N; 20S-20N; 20N-60N; 60S-20S; WBC (Gulf Stream 30-45N 80-45W, Kuroshio-Oyashio 30-45N 140-170E, Agulhas return current 35-50S 10-60E, Brazil-Malvinas 35-50S 60-40W, East Australian Current 25-40S 145-160E); 60S-45S.

**Row-grid statistics (both products).** On rows at latitude -59.875 + k degrees (k = 0..119), all 1,440 longitudes: zonal lag-1 gradient |dSST/dx|, fractions above 1, 2 and 4 K per 100 km, and zonal structure functions at lags 1 to 16 pixels. The common mask has pixels that are valid in both products on all fetched days.

**Change points and steps.** We deseasonalised ln(statistic) with a constant and four annual harmonics. Binary segmentation for mean shifts (8 splits; minimum segment 180 days for daily data, 36 samples for 5-day data) gave the break dates and local ratios. The step at a test date is the mean over the 365 days after the date minus the mean over the 365 days before it. The placebo distribution uses the same statistic at all candidate dates (every 5 days) more than 365 days from all test dates.

**Trends.** Annual means; OLS slope with a 3-year moving-block bootstrap (2,000 draws). Per-cell trends are Theil-Sen slopes with Mann-Kendall z (no correction for serial correlation). The step-adjusted model uses the 5-day samples with a constant, a linear term and step terms; intervals come from a moving-block bootstrap of residuals (block 73 samples = 1 year, 1,000 draws). The random-date placebo draws 4 (DOISST) and 5 (CCI) dates uniformly in 1984-01-01 to 2023-06-30, at least 0.5 years apart.

**Subpolar Front.** We took monthly means of SST (all days for `case_spf.py`; every 5th day for the comparison), the meridional centred gradient, its maximum in 38-41N at each 0.25-degree longitude in 128-138E, the mean over longitudes and the annual mean of the months. Chen et al. (2022) also removed water shallower than 200 m; we did not.

## Limitations

- CCI v3 is not homogeneous for these statistics (R4). We have no in situ reference for spatial gradients, so we cannot tell which product is right at any date. The adjusted trends depend on the choice of step dates. Four of the nine dates come from the change-point search and are not documented input changes in the sources that we checked.
- The CCI comparison uses one zonal row per degree of latitude and every 5th day, so it has zonal statistics only. The DOISST full-grid statistics include meridional terms.
- CCI is a point subsample of a 0.05-degree analysis at 0.25-degree spacing. DOISST is a 0.25-degree analysis. The level of each statistic depends on the product resolution. We compare changes in time, not levels.
- The step model removes any real abrupt change on the same dates. A real global change in fronts on a single day is improbable, but a regional change (for example the winter 2007 Subpolar Front jump in both products) can occur near a step date.
- Bootstrap and Mann-Kendall significance are approximate for serially correlated data. Per-cell tests do not correct for multiple testing.
- The 1982-1984 DOISST and CCI fields can also contain aerosol effects of the 1982 El Chichon eruption. We did not test this.
- DOISST values have a resolution of 0.01 K, which gives a discrete shape at weak gradients (Figure 8a).

## Reproduction

Run `files/code/run_all.sh` from a work directory that contains `code/` and has `../datasets` (the shared campaign datasets), or set `DATASETS`. It needs Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib, and the file `files/data/cell_fields.npz` of sci:sha256:69a00227 (not copied here) at `prior/p3/files/data/cell_fields.npz` (`sci read <bundle> --file files/data/cell_fields.npz --output ...`). The CCI fetch takes about 3 to 4 hours (16 parallel OPeNDAP requests; resumable). The DOISST extraction takes about 25 minutes with 6 processes. The statistics and figures take about 30 minutes. Raw data and the CCI subsets go to `scratch/`, outside the bundle. To check the statistics without downloads, use the derived files below.

## Files

- `files/code/`: all code. `fetch_cci_rows.py`, `fetch_cci_spf.py` (CCI subsets); `extract_doisst_spatial.py` (DOISST daily statistics); `spatial_common.py` (grid, mask, regions, row statistics); `stats_tools.py` (change points, steps, placebo, trends); `analysis_doisst.py`, `row_compare.py`, `analysis_rows.py`, `analysis_adjusted.py`, `adjusted_placebo.py`, `case_spf.py`, `case_spf_compare.py`, `figures.py`, `provenance.py`; `run_all.sh`.
- `files/results/doisst_daily_series.csv.gz`: DOISST daily full-grid statistics by region, 1982-2025.
- `files/results/doisst_spatial.json`: DOISST change points, steps, placebo statistics, trends and BIC; per-cell summary.
- `files/results/doisst_cell_fields.npz`: DOISST per-cell annual mean gradient and sub-1-degree variance, trends and step maps.
- `files/results/row_stats.npz`: daily row-grid statistics for both products (every 5th day), common mask, per-cell annual zonal gradient.
- `files/results/rows_compare.json`, `rows_annual.csv`, `rows_cell_trends.npz`: DOISST-CCI comparison.
- `files/results/adjusted_trends.json`, `adjusted_placebo.json`: step-adjusted trends and the random-date placebo.
- `files/results/case_spf*.{json,csv}`: Subpolar Front case.
- `files/provenance/data_provenance.json`: DOISST file paths, URLs and SHA-256 hashes; CCI constraints and hashes of the local subset arrays; prior-bundle file hash.
- `files/NOTICE_external_data.md`: external data sources, terms and attribution.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-775bee9b9fe1. Topic earth-and-ocean-sciences. Machine dell. Account claude-olen. Model Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. Date 2026-11-10.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- External data and their terms: see `files/NOTICE_external_data.md`. CCI-derived values carry the attribution "Contains ESA SST CCI Analysis v3.0 data (Embury et al. 2024), CC BY 4.0."

## References

- Lee, C., Song, H., Choi, Y., Cho, A., Marshall, J. (2025). Observed multi-decadal increase in the surface ocean's thermal inertia. Nature Climate Change 15, 308-314. doi:10.1038/s41558-025-02245-w
- Chen, S., Wang, H., Chen, W., Zhang, Y., Zhang, Y. (2022). Decadal intensified and slantwise Subpolar Front in the Japan/East Sea. Frontiers in Marine Science 9. doi:10.3389/fmars.2022.1038024
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007). Daily high-resolution-blended analyses for sea surface temperature. Journal of Climate 20, 5473-5496. doi:10.1175/2007JCLI1824.1
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Scientific Data. doi:10.1038/s41597-024-03147-w
- ESA SST CCI Analysis L4 v3.0 dataset. doi:10.5285/4a9654136a7148e39b7feb56f8bb02d2
