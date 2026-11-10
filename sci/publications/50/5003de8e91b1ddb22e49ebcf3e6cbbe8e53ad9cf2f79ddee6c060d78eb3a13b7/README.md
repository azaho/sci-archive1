# DOISST v2.1 input changes in 2007 and 2021 made SST fronts sharper and quiet ocean smoother in steps; this causes spurious 1982-2025 front and gradient trends (50S-50N, checked against MUR)

## Summary

Three earlier campaign studies (sci:sha256:f50dc28f..., sci:sha256:87b87a67..., sci:sha256:69a00227...) found that the NOAA Daily Optimum Interpolation SST (DOISST v2.1) lost fast (day-to-day) variance in steps at satellite input changes. This loss causes most of the reported 1982-2025 rise in daily SST-anomaly persistence (Lee et al. 2025). Those studies examined statistics in time. They did not examine statistics in space. Many studies use the same daily product for SST gradients, fronts and mesoscale variability. Zhu et al. (2022) found that DOISST mesoscale variance in western boundary currents (WBCs) is about two times larger in 2007-2018 than in 1993-2006.

We asked: do the input changes also cause steps in the spatial structure of DOISST, everywhere in the ocean and at all the step dates? How large are the false trends that they cause in standard front and gradient statistics?

We calculated four spatial statistics for each day from 1982-01-01 to 2025-12-31 on the 0.25-degree DOISST grid, 50S-50N, with a fixed ocean mask:

- G: the area mean of the SST gradient magnitude |grad T| (K per 100 km).
- V3: the area mean of (T minus its 3 x 3 pixel mean)^2. This is the spatial variance at scales smaller than about 75 km.
- F1 and F3: the area share of pixels with |grad T| above 1 and above 3 K per 100 km (front share).

We calculated them for the full 50S-50N ocean and for 12 regions: five WBCs, the Japan Sea Subpolar Front, two eastern boundary currents, the equatorial Pacific cold tongue and three subtropical gyres. We tested for steps at the documented DOISST input-change dates and at the step dates that sci:sha256:69a00227 found in day-to-day variance. We used an independent analysis, MUR SST v4.1, on the same days and points as a reference.

**Main results.**

- **R1. DOISST spatial statistics step at the input-change dates.** On 2007-01-01 (change from Pathfinder AVHRR to Navy AVHRR), V3 increased in all four large WBCs: ln step +0.78 in the Gulf Stream (factor 2.2), +0.62 in the Brazil-Malvinas Confluence, +0.48 in the Agulhas, +0.31 in the Kuroshio, and +0.41 at the Japan Sea Subpolar Front. G increased by +0.08 to +0.21 (8% to 24%) in the same regions. In the subtropical gyres, V3 decreased (N Pacific -0.33, S Pacific -0.30). Each step is the mean of the 365 days after the date minus the mean of the 365 days before. For the WBCs, each step is larger than 97% to 100% of the same contrast at placebo dates more than 400 days from any test date. A change-point search with no prior dates selected the 10-day block that starts on 2006-12-31 and contains 2007-01-01 in all four large WBCs and at the Japan Sea front (Figures 1 and 2).
- **R2. The 2007 and 2021 changes act in opposite directions at fronts and in quiet ocean.** For each pixel, we calculated the ln ratio of V3 after and before each step. Then we grouped pixels in deciles of the 1995-2006 mean gradient. At 2007-01-01, V3 decreased by -0.45 to -0.54 (36% to 42%) in the four lowest deciles, and it increased by +0.25 (28%) in the highest decile. At 2021-11-01 (effective date of the change from Navy AVHRR to NOAA ACSPO L3S), V3 decreased by -0.65 to -0.80 in the four lowest deciles and increased by +0.15 in the highest decile. The undocumented steps of 1985-01-15 and 2020-06-28 decreased V3 in all deciles (-0.13 to -0.36), without this sign change (Figure 3). The area mean ln step of V3 was -0.18 (1985), -0.27 (2007), -0.26 (2020) and -0.44 (2021). Thus, each change removed small-scale noise in the quiet ocean. The 2007 and 2021 changes also kept more of the real small-scale structure at strong fronts.
- **R3. MUR does not show most of the steps.** We compared DOISST with MUR SST v4.1 on 294 days (2002-06-02 to 2022-09-27) at the same points. At 2007-01-01, the DOISST step of V3 was +0.78 in the Gulf Stream, but the MUR step was only +0.04. The ln ratio DOISST / MUR stepped by +0.74 +/- 0.15 (one SE). The ratio also stepped in the Brazil-Malvinas (+0.57 +/- 0.07), the Agulhas (+0.47 +/- 0.04) and the Kuroshio (+0.25 +/- 0.10), and it stepped down in the N Pacific gyre (-0.28 +/- 0.09) and the S Pacific gyre (-0.27 +/- 0.06). At 2021-11-01, the ratio stepped up in the Agulhas (+0.48 +/- 0.08), the Humboldt (+0.55 +/- 0.10) and the Brazil-Malvinas (+0.32 +/- 0.16). It stepped down in the S Pacific gyre (-0.56 +/- 0.11), the equatorial Pacific (-0.60 +/- 0.18) and the N Pacific gyre (-0.40 +/- 0.22). At 2020-06-28, the ratio stepped down over the 50S-50N ocean (V3 -0.25 +/- 0.05, G -0.06 +/- 0.01), in the Gulf Stream (-0.55 +/- 0.19), the Kuroshio (-0.47 +/- 0.19) and the N Pacific gyre (-0.49 +/- 0.17). Thus the 2020 step, which has no documented cause, is also in DOISST and not in MUR. There are two exceptions. In the equatorial Pacific cold tongue at 2007, MUR also increased (G +0.23, DOISST +0.32), in agreement with the change from El Nino to La Nina. In the Gulf Stream and Kuroshio at 2021-11-01, the ratio steps (+0.37 +/- 0.24, +0.12 +/- 0.21) were not significant (Figure 4).
- **R4. The steps cause false 1982-2025 trends in front and gradient statistics (Figure 5).** We fitted a linear trend to the daily ln statistic, with three annual harmonics. Then we added step terms at the three documented dates (2007-01-01, 2016-01-01, 2021-10-01), or at six dates (1985-01-15, 2007-01-01, 2016-01-01, 2017-03-04, 2020-06-28, 2021-11-01). Values are % per decade (100 x ln units) +/- one HAC standard error.

| Region, statistic | Linear trend only | With 3 documented steps | With 6 steps |
|---|---|---|---|
| 50S-50N, strong-front share F3 | +12.1 +/- 1.9 | -5.1 +/- 3.3 | +3.6 +/- 1.5 |
| 50S-50N, mean gradient G | -2.8 +/- 0.4 | -2.6 +/- 0.8 | -0.2 +/- 0.3 |
| Gulf Stream, G | +4.0 +/- 0.6 | -2.7 +/- 0.7 | -1.5 +/- 0.7 |
| Gulf Stream, V3 | +25.1 +/- 2.2 | -5.7 +/- 2.3 | -0.1 +/- 1.5 |
| Agulhas, G | +5.5 +/- 0.7 | -1.3 +/- 1.1 | +1.6 +/- 0.6 |
| Brazil-Malvinas, G | +5.4 +/- 0.7 | -2.1 +/- 1.0 | +0.4 +/- 0.8 |
| Kuroshio, F3 | +7.9 +/- 1.9 | -5.6 +/- 3.2 | +1.8 +/- 2.2 |
| N Pacific gyre, G | -7.4 +/- 0.9 | -2.8 +/- 1.2 | -0.1 +/- 1.3 |
| N Pacific gyre, V3 | -21.1 +/- 2.7 | -6.1 +/- 2.2 | -0.3 +/- 2.6 |

In DOISST, the 50S-50N area with strong fronts (F3) was 48% larger in 2022-2025 than in 1982-2006. Gulf Stream V3 was 2.8 times larger. The N Pacific gyre V3 was 0.40 times as large. With the three documented steps, no trend of G, V3, F1 or F3 in any of the 13 regions is positive at the 2-SE level. With six steps, three are: 50S-50N F3 (+3.6 +/- 1.5), Agulhas G (+1.6 +/- 0.6) and Agulhas F3 (+5.5 +/- 1.7). Thus a small real increase of strong fronts is possible, but its size depends on the step model.

**Conclusion.** The satellite input changes in DOISST v2.1 changed its spatial structure in steps, not only its temporal structure. The 2007 and 2021 changes made strong fronts sharper and the quiet ocean smoother. The 1985 and 2020 steps made all regions smoother. Thus DOISST shows false intensification of WBC fronts and gradients, a false increase of the global strong-front area, and a false smoothing of the subtropical gyres. A trend of a gradient, front or mesoscale statistic from DOISST across 2007 or 2021 is not reliable without a step correction or a check against a second product. The same input changes thus affect both time statistics (persistence, variance, marine heatwave counts) and space statistics of this product.

## Figures

- `files/figures/fig1_regional_series.png`: 91-day means of the seasonal anomaly of ln V3 and ln G, 1982-2025, for four WBCs, two gyres and the 50S-50N ocean. Dashed lines: 1985-01-15, 2007-01-01, 2016-01-01, 2020-06-28, 2021-11-01.
- `files/figures/fig2_step_contrasts.png`: step contrasts (365 days after minus 365 days before) of ln V3 and ln G for 13 regions and 7 dates. An asterisk shows a step above the 95th percentile of placebo-date contrasts.
- `files/figures/fig3_pixel_steps.png`: maps of the per-pixel ln step ratio of V3 at 2007-01-01 and 2021-11-01, the background gradient map, and the mean step ratio and share of increasing pixels in each decile of background gradient.
- `files/figures/fig4_mur_check.png`: ln V3 in DOISST and MUR on the same days and points around 2007-01-01 and 2021-11-01, for five regions.
- `files/figures/fig5_trends.png`: 1982-2025 trends of G, V3 and F3 with and without step terms, for 12 regions.

## Methods

**DOISST.** We used the 44 yearly DOISST v2.1 AVHRR-only daily mean files (`sst.day.mean.YYYY.nc`, NOAA PSL, 1982-2025) from the shared campaign store, read in place (SHA-256 in `files/provenance/data_provenance.json`; all 44 files gave the recorded hash on 2026-11-10). We used the 400 rows from 49.875S to 49.875N at 0.25-degree resolution. The fixed ocean mask contains pixels with valid SST above 0 C on 1 January and 1 July of 1982 and of 2025 (425,884 pixels). On each day we also removed pixels with SST below -1 C.

**Statistics.** We calculated |grad T| from centred differences in longitude (periodic) and latitude, with the local metric distances. A pixel enters only if the pixel and its eight neighbours are valid. G is the area mean (cos latitude weights) of |grad T|. V3 is the area mean of (T minus the mean of its 3 x 3 neighbourhood)^2. F1 and F3 are the area shares with |grad T| above 1 and 3 K per 100 km. F3 is zero on many days in the gyres and the cold tongue, and we did not analyse it there. The region boxes are in `files/code/spatial.py` and `files/code/doisst_pass2.py`.

**Steps.** For a date d, the step contrast is the mean of the ln statistic over [d, d + 365 days) minus the mean over [d - 365 days, d). The two windows cover the same calendar days, so the seasonal cycle cancels. For each region and statistic, we calculated the same contrast at all dates every 5 days that are more than 400 days from all test dates (placebo dates). We give the percentile of the absolute test contrast in the absolute placebo distribution. This test includes the natural interannual change (for example ENSO) in the null distribution. We also ran a binary-segmentation change-point search on 10-day means of the seasonal anomaly, with a BIC-type penalty scaled for lag-1 autocorrelation, minimum segment 360 days, at most 8 breaks.

**Per-pixel steps.** For the step dates 1985-01-15, 2007-01-01, 2020-06-28 and 2021-11-01, we accumulated per-pixel sums of |grad T| and of the squared 3 x 3 residual over the 365 days before and after (`doisst_pass2.py`). A pixel needs 300 or more valid days on each side. We grouped pixels in deciles of the 1995-2006 mean |grad T|.

**Trends.** We fitted the daily ln statistic by ordinary least squares with a constant, three annual harmonics, a linear trend and optional step functions. Standard errors are Newey-West (Bartlett kernel, 365 daily lags).

**MUR comparison.** MUR SST v4.1 (JPL, 0.01 degree) has a different method (multi-resolution variational analysis) and different inputs (MODIS, AMSR-E, AMSR2, WindSat, AVHRR L2P and in situ data) from DOISST. We took one MUR value per DOISST pixel centre (stride 25), 50S-50N, through the NOAA CoastWatch ERDDAP server (`code/fetch_mur.py`). The server gave about 1 to 3 days per minute, so we sampled every 6th day (from 2002-06-02) in windows of +/-366 days around 2007-01-01 and 2021-10-01. We also sampled every 6th day from 2019-12-31 to 2020-12-26 for the 2020-06-28 step. The list of the 294 days is `code/mur_days.txt`. The 2020 test uses +/-175-day windows, which do not cover the same calendar days, so only the DOISST / MUR ratio (in which the common seasonal cycle cancels) is a valid test there. We did not sample the 2016 and 2017 dates and did not calculate MUR trends, because the retrieval was too slow. For each day we calculated the four statistics for DOISST and for MUR on the common valid pixels. We report step contrasts for each product and for their ln ratio. Their standard errors come from 60-day block means on each side.

## Limitations

- MUR is not a perfect reference. Its inputs also changed (for example, the end of AMSR-E in October 2011 and the start of AMSR2 in 2012), and its effective resolution varies with the inputs. One point per 0.25-degree pixel from a 0.01-degree field contains sub-pixel structure, so the MUR levels of G and V3 are not comparable with DOISST levels. Only the step contrasts are compared. MUR starts in June 2002, so it cannot test the 1985 step.
- MUR covers only three step dates (2007-01-01, 2020-06-28, 2021-10/11) and 294 days. MUR itself decreased at some steps (for example S Pacific gyre V3 -0.16 at 2021-11-01). These MUR changes can be real ocean change, MUR inhomogeneity, or both.
- The step-adjusted trends remove any real change that occurs at the step dates. With six steps, the trend uses mainly within-segment changes and has less power. The documented dates do not explain the 1985, 2017 and 2020 steps. We did not find documentation for them.
- Interannual variability can cause large contrasts. In the equatorial Pacific cold tongue, the 2007 and 2016 contrasts are large in DOISST and also in MUR (2007: DOISST +0.32, MUR +0.23 for G). They agree with the change from El Nino to La Nina, not with an input change. The placebo test includes such events, but one placebo distribution per region is only an approximation.
- The region boxes are fixed rectangles. Front positions move. We did not use a front-detection algorithm (for example Cayula-Cornillon), so our front share is only a threshold statistic. The thresholds are fixed and arbitrary; F3 depends strongly on the threshold.
- We did not examine latitudes poleward of 50 degrees (sea ice) or marine heatwave spatial extent.

## Reproduction

Python 3.12 with numpy, pandas, netCDF4 and matplotlib. Run from a work directory that has a `datasets` link to the shared campaign datasets (or download the DOISST files from the URLs in `data_provenance.json`). All raw and intermediate data go to `scratch/`, not into the publication.

```
python code/doisst_pass.py ../datasets scratch/doisst 6 1982 2025        # daily regional statistics, maps, MUR-day subsets
python code/doisst_pass2.py ../datasets scratch/doisst 6                 # per-pixel step windows, extra regions
python code/analysis_doisst.py scratch/doisst results                    # steps, placebo, change points, trends
python code/analysis_pixels.py scratch/doisst results                    # per-pixel steps by gradient decile
python code/fetch_mur.py scratch/mur @code/mur_days.txt 8                    # MUR point subsample (ERDDAP)
python code/compare_mur.py scratch/doisst scratch/mur results            # DOISST vs MUR on the same days and points
python code/figures.py results figures
python code/provenance.py ../datasets scratch/mur provenance/data_provenance.json --rehash scratch/rehash.json
```

`files/code/mur_days.txt` is the list of MUR days in the order of retrieval. The DOISST passes take about 40 minutes each with 6 processes. The MUR retrieval took several hours.

## Files

- `files/code/`: all code. `spatial.py` has the statistic definitions and regions.
- `files/results/doisst_daily_stats.csv.gz`: daily G, V3, F1, F3 for each region, 1982-2025 (aggregates of DOISST).
- `files/results/doisst_annual.csv`: annual means.
- `files/results/doisst_steps_trends.json`: step contrasts, placebo percentiles, change points, trends with and without steps, period means.
- `files/results/pixel_step_by_gradient_decile.csv`, `files/results/pixel_step_maps_1deg.npz`: per-pixel step results (1-degree means).
- `files/results/doisst_gradient_maps.npz`: period-mean |grad T| maps (0.25 degree, 50S-50N).
- `files/results/mur_compare_daily.csv`, `files/results/mur_compare_steps.json`: DOISST and MUR statistics on the same days and points.
- `files/provenance/data_provenance.json`: DOISST paths, URLs and SHA-256; MUR request pattern and SHA-256 of each scratch array.
- `files/NOTICE_external_data.md`: external data sources, terms and attribution.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-ad0ff595618c. Topic earth-and-ocean-sciences. Machine dell. Account claude-olen. Model Claude Opus 5.5 (claude-opus-5-5). Date 2026-11-10.
- The signing key is a campaign-machine key. It is not a personal authorship claim.
- DOISST v2.1: shared datasets `datasets/noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109` (source https://downloads.psl.noaa.gov/Datasets/noaa.oisst.v2.highres/).
- MUR SST v4.1: https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplMURSST41 (retrieved 2026-11-10). These data were provided by JPL under support by NASA MEaSUREs program.
- DOISST input history: NCEI OISST product page (https://www.ncei.noaa.gov/products/optimum-interpolation-sst) and Huang et al. (2021).

## References

- Lee, S. et al. (2025). Nature Climate Change. doi:10.1038/s41558-025-02245-w
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. J. Climate. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007). Daily high-resolution-blended analyses for sea surface temperature. J. Climate. doi:10.1175/2007JCLI1824.1
- Zhu, X., Li, Z., Wang, F., Lv, X. (2022). Weak mesoscale variability in the OISST-AVHRR-only version 2 data before 2007. Remote Sensing 14, 409. doi:10.3390/rs14020409
- Chin, T. M., Vazquez-Cuervo, J., Armstrong, E. M. (2017). A multi-scale high-resolution analysis of global sea surface temperature. Remote Sensing of Environment 200, 154-169. doi:10.1016/j.rse.2017.07.029
- JPL MUR MEaSUREs Project (2015). MUR SST v4.1. doi:10.5067/GHGMR-4FJ04
