# No-flow days at US drying stream gauges stopped their rise after 2017, except in western deserts and mountains

**Job:** sci-1107-dell-earth-and-ocean-sciences-04acc3104dec · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Zipper et al. (2021, *Environ. Res. Lett.* 16 084033) found changes in annual no-flow days at 540 non-perennial
US stream gauges in climate years 1980-2017. Gauges in the south and west became drier. Gauges in the northern Great Plains became wetter.
We asked two questions:

1. Did these changes continue in the eight new climate years 2018-2025 (April 2018 to March 2026)?
2. Does basin climate (precipitation P and potential evapotranspiration PET of the current and the prior year) explain the 1980-2017 trends and the 2018-2025 values?

We wrote the analysis plan (`files/ANALYSIS_PLAN.md`) before we looked at any 2018-2025 no-flow values.
The placebo split, the reference-gauge and approved-data subsets, the precipitation-only model and forecast F4 are additional checks that we added after the first results. F4 is exploratory.

## Data and methods

- **Gauges.** All 9,067 CONUS gauges in GAGES-II (Falcone 2011). We downloaded USGS NWIS daily mean discharge (parameter 00060) for April 1980 to March 2026 on 2026-11-09.
- **No-flow day.** Discharge rounded to 0.1 ft3/s equals zero (as in Zipper et al.). A climate year (CY, April-March) is valid if it has 90% or more of its days. Annual no-flow days = no-flow fraction x 365.
- **Sample.** 30 or more valid CYs in 1980-2017 and a 1980-2017 mean of 5 to 360 no-flow days per year. This gives 572 gauges. 541 gauges also have 5 or more valid CYs in 2018-2025. These 541 gauges are the test sample.
- **Regions.** EPA/CEC Level I ecoregion at the basin centroid, with the Great Plains split at 41.3 N. This rule gives the Zipper et al. region for 536 of their 540 gauges.
- **Trend class.** Mann-Kendall test on 1980-2017 annual no-flow days, p < 0.05: "drying" (more no-flow days), "wetting" (fewer) or "none".
- **Direction test (H1).** For each trend class, the share of gauges whose 2018-2025 mean moved in the trend direction. We compare with the 1980-2017 mean and with the 1999-2017 mean. The second comparison asks if the change continued past the level that it had already reached. Two-sided binomial test against 50%.
- **Forecasts (H2).** We forecast the 2018-2025 mean of each gauge with: F0 = 1980-2017 mean; F1 = 1999-2017 mean; F2 = Sen-slope line at CY 2021.5 (clipped to 0-365); F3 = per-gauge regression of no-flow days on standardized log(P/PET) of the current and the prior CY, fitted on 1980-2017, with observed 2018-2025 climate. Score = mean absolute error (MAE) over gauges. 95% intervals come from a gauge bootstrap and from a cluster bootstrap over HUC-2 regions.
- **Climate (H3).** Basin-mean monthly nClimGrid precipitation and mean temperature over the GAGES-II basin polygon. PET is from the Thornthwaite method. We repeated the climate models with precipitation only.
- **Placebo.** We applied the same method inside the published period: trend class from CY1980-2009, "recent" mean CY1991-2009, test CY2010-2017.

## Results

**Replication.** Our 1980-2017 Mann-Kendall class agrees with Zipper et al. for 96.8% of 539 matched gauges. The Kendall tau values correlate at r = 0.994. Our eligible sample has 144 drying, 91 wetting and 337 no-trend gauges. Zipper et al. had 139, 80 and 321 of 540.

**Direction in 2018-2025 (541 gauges).**

| 1980-2017 class | n | Above (drying) / below (wetting) 1980-2017 mean | Continued past 1999-2017 mean | p (vs 50%) | Median change vs 1999-2017 (days/yr) |
|---|---|---|---|---|---|
| Drying | 137 | 74% | 52% | 0.73 | +1.5 |
| Wetting | 86 | 94% | 67% | 0.002 | -2.0 |
| None | 318 | - | 32% higher, 68% lower | - | -7.7 |

Drying gauges stayed drier than in 1980-2017. But the typical drying gauge did not become drier than its 1999-2017 level. The mean change was +11.3 days/yr (95% CI 1.2 to 21.7), and a minority of gauges caused it. Wetting gauges continued to become wetter by a small amount. Gauges without a trend had fewer no-flow days in 2018-2025 (mean -7.8 days/yr, CI -12.1 to -3.7).

**The stall is new.** In the placebo split (504 gauges), 68% of 81 drying gauges continued past their 1991-2009 level in 2010-2017 (p = 0.002, median +17.3 days/yr). Selection on a significant trend thus does not by itself cause the 2018-2025 result.

**Regions (drying gauges, change vs 1999-2017).** Western Deserts: 13 of 16 higher (81%), median +17.6 days. Western Mountains: 61%, +8.0. South Great Plains: 55%, +4.5. Mediterranean California: 47%, -3.2. Eastern Forests: 20%, -13.9. The north Great Plains had no drying gauges. See Figure 2 (`files/figures/fig2_change_by_region.png`) and Figure 4 (`files/figures/fig4_map.png`).

**Forecasts.** MAE (days/yr) over 541 gauges:

| Forecast | MAE | Difference from F1 (gauge CI; HUC-2 cluster CI) |
|---|---|---|
| F0 1980-2017 mean | 34.9 | +5.8 (3.9 to 7.8; 2.4 to 9.7) |
| F1 1999-2017 mean | 29.0 | - |
| F2 Sen trend extended | 32.5 | +3.5 (1.1 to 5.9; -3.2 to 9.8) |
| F3 P/PET model, observed climate | 33.1 | +4.1 (2.2 to 6.0; -0.1 to 8.4) |
| F3P precipitation-only model | 31.4 | +2.4 |
| F4 (exploratory) F1 + climate slope x climate change | 28.5 | -0.5 (-1.5 to 0.5) |

The recent level (F1) was the best of the planned forecasts. Linear trend extension was worse. The trend was better than F1 only in the Eastern Forests and the north Great Plains. Median absolute errors give the same order (F1 17.3, F2 18.0, F0 20.2, F3 21.2).

**Climate.** The per-gauge P/PET model explains a median 33% of the year-to-year variance in 1980-2017. After the P/PET adjustment, 46% of drying trends and 70% of wetting trends stay significant. With precipitation only, 67% and 64% stay significant. Thus the temperature-based PET term absorbs part of the drying trends. In 2018-2025, drying gauges had 18.7 more no-flow days per year than the calibration climate models predicted (CI 9.1 to 28.3). Wetting gauges had 33.9 fewer (CI -42.4 to -25.7). Gauges without a trend had 17.4 fewer (CI -21.6 to -13.3). The 1980-2017 level shifts thus continued without a climate cause in these models. Basin P/PET in 2018-2025 was lower than in 1999-2017 in five of six regions (largest in the Western Deserts, Western Mountains and South Great Plains). In the Eastern Forests, precipitation increased (1,226 vs 1,189 mm) and the gauges became wetter, but Thornthwaite PET also increased. See Figure 1 (`files/figures/fig1_trend_class_timeseries.png`) and Figure 3 (`files/figures/fig3_forecast_mae.png`).

**Robustness.** Reference (GAGES-II "Ref") gauges only (n = 155): 56% of 41 drying gauges continued past the 1999-2017 level (p = 0.53), and F1 had the lowest MAE. When we use only test years without provisional data, the results do not change (drying 52%, wetting 67%). Provisional values are 1.6% of test-period days (11% in CY2025).

## Interpretation

The 1980-2017 drying at many US non-perennial gauges acted more like a shift to a new level than a continuing linear trend. In 2018-2025, the 1999-2017 level was the best simple forecast. Further drying continued in the Western Deserts and, less strongly, in the Western Mountains, where basin P/PET was lowest. Current- and prior-year P/PET did not explain the persistent shifts: gauges kept their 1980-2017 trend direction relative to the climate-model forecast. Possible causes that this study did not test include multi-year groundwater storage loss, water use, channel or gauge-control changes, and nonlinear climate response.

## Limitations

- Eight test years is a short period. The test period includes the wet California winters of CY2018 and CY2022 and droughts in 2020-2022 in the west and south. Climate variability can hide or mimic a trend.
- Discharge near zero is sensitive to gauge rating and reporting practice. NWIS values are revised over time. CY2025 data are 11% provisional.
- Most gauges (386 of 541) are not GAGES-II reference gauges. Human water use can affect them.
- Thornthwaite PET uses temperature only. A different PET method can change the climate attribution. The climate model is linear, with two predictors per gauge.
- Gauges cluster in space (for example, many gauges in southern California and Texas). HUC-2 cluster intervals are wider than gauge-bootstrap intervals, and some include zero.
- 31 eligible gauges had fewer than 5 test years (7 drying, 5 wetting, 19 no-trend). We excluded them.
- Region labels follow our centroid rule, not the Zipper et al. table.

## Files

- `files/code/` - all code. `run_all.sh quick` re-runs the analysis, checks and figures from the bundled tables (exact match verified). `run_all.sh full SCRATCH DATASETS` downloads all sources into a scratch folder and rebuilds every table. Python 3.12 with numpy, pandas, scipy, xarray, netCDF4, shapely, pyproj, pyshp, pymannkendall, matplotlib (py7zr for the optional Zipper comparison).
- `files/data/cy_noflow_eligible_sites.csv` - per gauge and CY: valid days, no-flow days, provisional days (from USGS NWIS, public domain).
- `files/data/cy_basin_climate.csv` - per gauge and CY: basin P, PET, mean temperature, log(P/PET) (from NOAA nClimGrid, public domain).
- `files/data/eligible_sites_regions.csv` - gauge attributes from GAGES-II and the region labels.
- `files/results/` - `summary.json` (H1-H3), `robustness.json`, `zipper_comparison.json` (aggregate agreement only), per-gauge summaries, region table, climate-model residuals.
- `files/provenance.json` - source URLs, versions, licenses and SHA-256 hashes (including NWIS files of the 572 eligible gauges).
- `files/EXTERNAL_DATA_NOTICE.md` - terms of external data.
- `files/ANALYSIS_PLAN.md` - the plan written before the test data were inspected.

## References

- Zipper, S. C., et al. (2021). Pervasive changes in stream intermittency across the United States. Environ. Res. Lett. 16, 084033. doi:10.1088/1748-9326/ac14ec. Data and code: doi:10.4211/hs.fe9d240438914634abbfdcfa03bed863.
- Falcone, J. A. (2011). GAGES-II: Geospatial Attributes of Gages for Evaluating Streamflow. USGS. doi:10.3133/70046617.
- Vose, R. S., et al. (2014). NOAA Monthly U.S. Climate Gridded Dataset (nClimGrid), version 1. doi:10.7289/V5SX6B56.
- Thornthwaite, C. W. (1948). An approach toward a rational classification of climate. Geogr. Rev. 38, 55-94. doi:10.2307/210739.
