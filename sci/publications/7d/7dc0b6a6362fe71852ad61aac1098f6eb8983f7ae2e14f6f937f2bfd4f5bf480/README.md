# A May air-temperature model of Gulf of Mexico hypoxic area per nitrate load failed its 2024 test and the 1985-1999 back-cast

## Summary

Each July, a bottom-water hypoxic zone (dissolved oxygen below 2 mg/L) forms on the Louisiana-Texas shelf. Since about 2006, forecasts of its size have used the May nitrate plus nitrite (NO3+NO2) load of the Mississippi and Atchafalaya rivers. In 2024, Turner, Rabalais and Glaspie (Limnology and Oceanography, doi:10.1002/lno.12722) added a new term. Their model makes the hypoxic area per unit of May load a curved (optimum-type) function of the mean May air temperature at New Orleans airport. They fit it to 2000-2023 data and gave the hypothesis that ocean warming shrinks the zone. The LSU group used the model for the 2024 and 2025 forecasts.

We tested this model with independent public data: USGS daily WRTDS-K loads (data release ver. 3.0, May 2026), the LUMCON area series for 1985-2026, GHCN-Daily temperatures, NDBC winds and HURDAT2 storm tracks.

Main results:

1. **First operational year.** The 2024 temperature-model forecast was 5,107 km2 (stated 95% interval 4,687-5,569 km2). The measured area was 17,360 km2, which is 3.4 times the forecast. Our reproduction of the model gave 6,604 km2. A load-only model fitted to the same years gave 14,113 km2. LSU later classified 2024 as a storm year (Hurricane Beryl, landfall in Texas, about 500 km away, 13 days before the cruise). But storm mixing decreases the hypoxic area, so a storm cannot explain an area much larger than the forecast. In 2025, the forecast (12,470 km2) was near the measured area (11,401 km2), and the load-only model was nearer (12,564 km2).
2. **Back-cast to 1985-1999.** These 12 storm-free years were not in the fit window. With the frozen 2000-2023 fit, the temperature model increased the mean absolute error (MAE) from 4,493 km2 (load only) to 6,606 km2. The difference is +2,113 km2 (bootstrap 95% CI +826 to +3,432). The curve decreases quickly below 24 °C, and it predicted 6,891 km2 for the cool May of 1993. The measured area in 1993 was 17,520 km2.
3. **The fit is not specific to May.** In the 17 LSU fit years, the curved May fit explains 35% of the area-per-load variance (permutation p = 0.048). The same fit with February temperature explains 48%, and with November temperature 34%.
4. **There is a weak link to warmth, but it is not specific to May.** In a log-linear model for all 30 storm-free years from 1985 to 2025, a 1 °C warmer May gave 11% less area per load (p = 0.046). A 1 °C warmer June gave 23% less (p < 0.001). June and July river discharge did not remove these links.
5. **Forecast value.** We made one-year-ahead forecasts for the storm-free years from 2000 to 2025 (18 years), with refits that use only earlier years. The curved May model decreased the MAE by 451 km2 (95% CI 50 to 851) relative to a constant area-per-load ratio. May was the only one of 13 temperature predictors that gave this result. Also, LSU selected May after they saw these years. A monotonic May term gave a smaller gain with an interval that includes zero (-248 km2, CI -557 to +81). A linear year trend (the earlier "increasing sensitivity" term) made the forecasts worse (+836 km2, CI -438 to +2,176).
6. **Published forecasts.** We compared 18 LSU June forecasts from 2007 to 2026 with the measured areas. In 15 years, the forecast was larger than the measured area. The median ratio of measured area to forecast was 0.83 (0.80 in the 12 years that LSU did not mark as storm years).

**Conclusion.** The data do not support the curved May temperature "tipping point" as a forecast tool. It failed its first operational year and the earlier years, and other months fit the same data equally well or better. There is a weaker monotonic association: warmer late spring and early summer go with less hypoxic area per unit of nitrate. This association is a possible real effect, and new data must test it. It does not support the statement that warming alone made the zone smaller in a given year. The May nitrate load stays the main and most reliable predictor.

## Data

All data are public. File hashes and URLs are in `files/data/sources.csv`.

| Data | Source | Use |
| --- | --- | --- |
| Daily WRTDS-K NO3+NO2, TN and TP fluxes and discharge, Mississippi R. near St. Francisville (07373420) + Atchafalaya R. at Melville (07381495), WY1980-2025 | USGS data release doi:10.5066/P1MFARP2 ver. 3.0 (Klager 2026), file `eLists.zip`. Campaign copy: `/mnt/dell-data/shared_datasets/usgs-gulf-loads-v3-202605-elists-zip` (sha256 909138f3...a55a) | May load (sum of daily `GenFlux` for both rivers), June/July discharge |
| Mid-summer hypoxic area, 1985-2026 | LUMCON/LSU tables at gulfhypoxia.net (images transcribed into `files/code/hypoxia_inputs.py`). 2026 from the LSU press release of 2026-08-05 | Response |
| LSU June forecasts 2007-2026, cruise dates, excluded years | LSU/LUMCON forecast PDFs and yearly cruise pages (`files/data/lsu_forecast_sources.csv`) | Forecast check, storm classification |
| Daily TMAX/TMIN, New Orleans Intl Airport (USW00012916) | NOAA GHCN-Daily | Monthly mean air temperature, (TMAX+TMIN)/2, at least 25 days |
| HURDAT2 1851-2025 | Shared campaign dataset `nhc-hurdat2-atl-1851-2025-092326` | Tropical storms within 300 or 500 km of 28.9N 91.5W, from 14 or 30 days before the cruise to the cruise end |
| NDBC stdmet BURL1, GISL1, 42035 | NOAA NDBC historical files | Mean wind speed from 14 days before the cruise to the cruise end |
| ERSSTv5 monthly SST | Shared campaign dataset `ersst-v5-psl-sst-mnmean-20261108-olen` | May SST, 27.5-30.5N, 88-95W (placebo predictor) |

Check of the load calculation: the sum of our daily fluxes for each water year agrees with the USGS annual GULF NO3+NO2 loads (in short tons) to within 0.5% after unit conversion (factor 1.10 at 2000, 2010, 2020, 2024 and 2025). Our May 2024 discharge (32,945 m3/s) agrees with the 33,000 m3/s that the LSU 2025 report gives.

## Methods

* **Ratio.** R = area (km2) / May NO3+NO2 load (1000 metric tons N).
* **Reproduction of the temperature model.** We do not have the exact published equation. We used a quadratic R = a + bT + cT^2 in May temperature T. We fit it to the 17 LSU fit years (2000-2023 without the years that the LSU 2025 report excludes: 1988, 1989, 1997, 2003, 2005, 2008, 2010, 2016, 2019, 2020, 2024). The fitted optimum is 24.7 °C. For 2024 and 2025, our reproduction gives 6,604 and 13,000 km2. The published forecasts are 5,107 and 12,470 km2.
* **Load-only reference.** Constant ratio, sum(area)/sum(load), over the same years (119 km2 per 1000 t).
* **Hold-out tests.** We froze both fits and applied them to 1985-1999 (12 storm-free years with data) and to 2024-2025. We used a paired bootstrap (20,000 draws) for the MAE difference.
* **Month placebo.** We repeated the same quadratic fit and the forecast test with the temperature of each calendar month and with May SST.
* **Log-linear models.** log(area) = a + b log(load) [+ c year] [+ d T_month] [+ log discharge]. We used OLS with HC3 standard errors on the 30 storm-free years from 1985 to 2025. The analysis also includes versions with all years, with objective tropical-storm flags, and with 1988 removed (area 40 km2).
* **Rolling-origin forecasts.** For each target year from 2000 to 2025, we fit each model only on earlier storm-free years (expanding window, and a 24-year window), and then predicted the target year. The models are climatology, constant ratio, linear load, load + year, the curved May ratio model and a linear temperature ratio model. We also used log-linear models with monotonic May or June terms. We report the scores separately for storm-free years (n = 18) and for years that LSU excludes (n = 7).

## Results tables

`files/data/results.json`, `results_extra.json` and `results_rolling_loglinear.json` hold all estimates. Key numbers:

| Test | Temperature model | Load only | Note |
| --- | --- | --- | --- |
| 2024 (measured 17,360 km2) | 5,107 published; 6,604 reproduced | 14,113 | storm in 2024 can only reduce area |
| 2025 (measured 11,401 km2) | 12,470 published; 13,000 reproduced | 12,564 | |
| 1985-1999 back-cast MAE, n = 12 | 6,606 km2 | 4,493 km2 | difference +2,113 (CI +826 to +3,432) |
| Leave-one-out MAE in fit years, n = 17 | 3,985 km2 | 4,058 km2 | |
| Rolling MAE 2000-2025, storm-free, n = 18 | 3,556 km2 | 4,007 km2 | difference -451 (CI -851 to -50); only May of 13 predictors |
| Rolling MAE 2000-2025, excluded years, n = 7 | 4,648 km2 | 3,673 km2 | |

Log-linear temperature coefficients (1985-2025, storm-free years, n = 30; % change of area per load per 1 °C; 95% CI): May -11% (-21 to 0), June -23% (-33 to -11), February -8% (-13 to -3). Other months have intervals that include zero (`files/data/loglinear_month_placebo.csv`). Adding log June discharge gives a May coefficient of -0.123 (p = 0.027). Mean May temperature at New Orleans rose by 0.47 °C per decade from 1985 to 2025.

Wind and storms: in all years with data, neither the mean wind speed at BURL1/GISL1 in the 14 days before and during the cruise (p = 0.41) nor the tropical-storm flag (p = 0.48) explained the residuals of the load-only model (`results.json`, `residual_wind_tc_T`). The study has low power for this test, and only six years have flagged storms.

## Figures

* `files/figures/fig1_ratio_vs_may_temperature.png`: Area per load against May temperature, with the quadratic fit, the 1985-1999 years outside the fit window, and 2024-2025.
* `files/figures/fig2_area_timeseries_predictions.png`: Measured areas and predictions from the frozen 2000-2023 fits, with the published LSU forecasts.
* `files/figures/fig3_month_placebo.png`: Month placebo for the log-linear coefficient (A) and for the rolling forecast gain (B).
* `files/figures/fig4_lsu_forecast_verification.png`: The published LSU forecasts compared with the measured areas, 2007-2026.

## Limitations

* We reproduced the temperature model from its description ("hyperbolic", with an optimum, May air temperature at New Orleans airport, 2000-2023). The published forecasts for 2024 and 2025 are within 30% of our reproduction, but the exact form can be different. The 2024 forecast test uses the published number, so it does not depend on our reproduction.
* Our loads are the final WRTDS-K estimates. The forecasts used provisional USGS May loads that were available in June, and these can be different.
* Each year gives one measured area (n = 30-38). All tests have low power. Three out-of-sample years exist after the fit (2024-2026), and storms affected two of them (2024: Beryl, according to LSU; 2026: Tropical Storm Bertha).
* No 2026 May load is in the USGS release. Thus 2026 is only in the check of the published forecasts (forecast 19,508 km2, measured 3,449 km2 after Tropical Storm Bertha).
* LSU cruise dates for 1985-2005 are not on the source pages. We used 20-30 July for those years in the storm and wind windows.
* The measured area depends on the cruise coverage and timing. LUMCON states that the area is sometimes an underestimate when ship time is short.
* We found no LSU forecast document for 2023. The 2009-2011 forecasts are the stated model or the midpoint of the range.
* The month-placebo result (June stronger than May) is exploratory. We did not choose it before we did the analysis.

## Reproduction

1. `files/code/retrieve.sh` downloads the raw inputs into `raw/`. Compare the hashes with `files/data/sources.csv`. The two shared campaign datasets are read in place from `../datasets/`.
2. `PY=<python> bash files/code/run_all.sh` runs from the parent folder of `result/`, with `raw/` beside it. This builds `files/data/year_table.csv`, runs all tests and makes the figures. The pipeline is deterministic (fixed random seeds), and a second run gave a byte-identical `results.json`.
3. Environment: Python 3.12, numpy 2.5.4, pandas 3.1.1, statsmodels 0.15.0, matplotlib 3.11.2, xarray 2026.9.0, netCDF4 1.7.5.1, rdata 1.1.0 (to read the USGS EGRET `.rds` files), pypdf 7.0.0 (PDF text only).

## Provenance

* Campaign 11_07_2026, job `sci-1107-dell-earth-and-ocean-sciences-044f70be6fe6`, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
* Analysis and text by the AI model Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code, 2026-11-09. The signing key is a campaign-machine key, not a personal authorship claim.
* No earlier campaign publication covers Gulf of Mexico hypoxia. The campaign search found none on hypoxia, nitrate or the Mississippi River.
