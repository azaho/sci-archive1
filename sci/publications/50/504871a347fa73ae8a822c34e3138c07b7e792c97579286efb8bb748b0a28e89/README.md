# The 1949-2016 global tropical-cyclone slowdown trend did not hold for raw 2017-2024 IBTrACS data; a 4% slowdown within region-latitude-month cells continued

## Summary

Kossin (2018, Nature 558:104) reported a 10% decrease in the annual-mean translation speed of tropical cyclones (TCs) from 1949 to 2016. The data were 6-hourly NHC and JTWC best-track positions. We repeated this method on IBTrACS v04r01 and then tested the frozen 1949-2016 trend on eight new seasons (2017-2024) with final best tracks.

- **Reproduction.** With the same method, the 1949-2016 global decrease was -8.6% (slope -0.024 km/h per year, 95% CI -0.035 to -0.014 after AR(1) correction). Kossin reported -10%. Our regional values were also near the published values: western North Pacific -15% (published -16%), western North Pacific over land -21% (published -21%), North Atlantic over land -18% (published -16%), Australian region -10% (published -14%) and Australian region over land -18% (published -22%).
- **Raw out-of-sample test.** The 2017-2024 global mean speed was 18.13 km/h. The extended trend predicted 17.37 km/h. All 8 test seasons were above the trend line. The difference was +0.77 km/h, outside the 95% range expected if the trend continued with AR(1) noise (-0.70 to +0.69 km/h; p = 0.03). The extended trend had about twice the squared error of the 1949-2016 mean (1.10 vs 0.57 km²/h²) and of the 2007-2016 mean (0.60). The excess came mainly from 2018, 2020 and 2021. The 2022-2024 seasons were near the trend line. Variants that remove extratropical or weak points gave the same sign with p = 0.06-0.11.
- **Latitude mix.** Translation speed increases strongly toward the poles: about 16 km/h at 5-20 degrees and 32-46 km/h at 35-50 degrees. The share of segments at 30 degrees or more fell from 13.0% (1949-1969) to 9.4% (2007-2016), then rose to 12.5% in 2017-2024. We compared seasons within region x 5-degree latitude band x month cells (560 cells, fixed effects). With this adjustment the 1949-2016 decrease became -3.9% (p = 0.007), and 2017-2024 was on the frozen trend line (+0.04 km/h, 95% range -0.69 to +0.69, p = 0.91). The latitude band alone gave the same result (-3.7%; test residual -0.04 km/h). The basin mix or the month alone did not.
- **Interpretation.** Approximately half of the reported raw global slowdown, and all of the 2017-2024 departure from it, follow the latitude distribution of the recorded track segments. A smaller decrease within cells (about 4% over 68 years) remains and continued in 2017-2024. But in the test period the frozen trend line was not clearly better than the 2007-2016 mean (squared error 0.31 vs 0.33). When we also put 6-hourly wind category into the cells, the within-cell decrease became -2.0% (p = 0.17).
- **Over-land regions.** The two largest published over-land slowdowns did not clearly change in 2017-2024: western North Pacific +1.2 km/h above the frozen line (p = 0.54) and Australian region -1.1 km/h below it (p = 0.55). Both ranges are wide. The North Atlantic over-land mean was far above the line (+5.5 km/h, p = 0.02). This came from fast extratropical and weak over-land points: for points of tropical-storm strength the residual was +0.2 km/h (p = 0.94).

## Question and plan

Did the TC translation-speed slowdown that Kossin (2018) reported for 1949-2016 continue in seasons that the original study did not use? We wrote the plan (`files/PLAN.md`) before we calculated any 2017-2024 statistic. The primary test is the global raw annual mean in 2017-2024, compared with forecasts fitted on 1949-2016 only:

- F1: the 1949-2016 OLS trend line, extended (the claim under test);
- F0: the 1949-2016 mean;
- FP: the 2007-2016 mean (recent persistence);
- FS: the 1980-2016 OLS trend line, extended (the geostationary-satellite era).

The composition adjustment, the basin and over-land subsets, and the intensity variants were secondary analyses in the plan. We added the latitude-only, region-only and other cell definitions (`composition_specs.csv`) after we saw the adjusted result. Treat them as diagnostics.

## Data

- IBTrACS v04r01, file `IBTrACS.ALL.v04r01.nc` from NOAA NCEI (global attribute `date_created` 2026-11-07 00:30:36; 23,498,405 bytes; sha256 `c20cc4e291f91e166b92b560bec64cfda3bc23c00d39b1282ae7c3b34ba12d17`). URL: https://www.ncei.noaa.gov/data/international-best-track-archive-for-climate-stewardship-ibtracs/v04r01/access/netcdf/IBTrACS.ALL.v04r01.nc. Campaign shared copy: `datasets/ibtracs-v04r01-ALL-netcdf-20261109/IBTrACS.ALL.v04r01.nc`.
- We used only the USA-agency positions (`usa_lat`, `usa_lon`: NHC/CPHC HURDAT2 for the Atlantic and eastern/central Pacific, and JTWC for the other basins), as Kossin (2018) did.
- Final JTWC best tracks are in the file through the 2024 season. For 2025, the file has only operational `tcvitals` positions for JTWC basins. Thus we report 2025 separately and do not use it in any score.

## Methods

1. Points (`code/01_extract_points.py`): USA positions at 00, 06, 12 and 18 UTC (the 3-hourly IBTrACS points are interpolated; we did not use them). 99.7% of the selected points have the original-data flag.
2. Segments (`code/02_segments.py`): consecutive points 6 h apart in the same main or provisional track (we removed spur tracks). Speed is great-circle distance divided by 6 h. Season is the IBTrACS season (the calendar-year variant gives the same result). Region is from the basin at segment start, with the Southern Hemisphere divided at 100 E as in Kossin (2018). A segment is over land if IBTrACS `dist2land` = 0 at either end (Kossin used ETOPO2). The result is 223,676 segments; 172,084 are in 1949-2016 and 22,028 are in 2017-2024.
3. Trends and forecasts (`code/03_forecast_test.py`): OLS on annual means. The CI uses effective degrees of freedom for lag-1 autocorrelation of residuals. Percent change uses the end points of the fitted line, as in Kossin (2018). A storm-block bootstrap (2,000 draws; storms resampled within each season) gives the sampling uncertainty of the 2017-2024 mean: 17.70-18.59 km/h globally.
4. Prediction test (`code/04_prediction_and_adjusted.py`): we simulated 20,000 complete 1949-2024 series from the fitted trend with AR(1) noise. For each, we fitted the trend to 1949-2016 again and calculated the mean 2017-2024 residual. This gives the 95% range and the two-sided p-value of the observed residual. Thus the test includes the uncertainty of the extended line.
5. Composition adjustment: segment speed = season effect + cell effect, solved with sparse least squares. The primary cell is region x 5-degree latitude band x calendar month. The season effects are shifted so that their 1949-2016 mean equals the raw 1949-2016 mean. `code/05_composition.py` gives other cell definitions, a direct standardization with fixed 1949-2016 region x band weights, and indicators such as the poleward share and the region shares.

## Results

### Global (Figure 1)

| Series | 1949-2016 change | 2017-2024 mean | Extended trend | Residual (95% range if trend continued) | p |
|---|---|---|---|---|---|
| Raw, all points (primary) | -8.6% | 18.13 | 17.37 | +0.77 (-0.70, +0.69) | 0.03 |
| Raw, calendar year | -8.8% | 18.13 | 17.35 | +0.78 (-0.72, +0.71) | 0.03 |
| Raw, no ET/DS points | -7.4% | 17.68 | 17.04 | +0.64 (-0.77, +0.77) | 0.11 |
| Raw, TS points at 34 kt or more | -15.4% | 17.91 | 16.94 | +0.97 (-1.00, +1.00) | 0.06 |
| Adjusted, region x lat x month | -3.9% | 17.92 | 17.88 | +0.04 (-0.69, +0.69) | 0.91 |
| Adjusted, 34 kt or more | -3.6% | 18.66 | 18.32 | +0.34 (-0.81, +0.81) | 0.42 |

Units are km/h. Squared errors of the forecasts for the raw primary series in 2017-2024: F1 1.10, F0 0.57, FP 0.60, FS 0.73 (km²/h²). For the adjusted series: F1 0.31, F0 0.46, FP 0.33. The 1980-2016 raw trend was -0.009 km/h per year (p = 0.42). This agrees with earlier reports that the slowdown is small in the satellite era (Chan 2019; Lanzante 2019). The 1949-2024 raw trend that includes the test seasons is still negative (-7.4%, p < 0.001), because the test period is short relative to the 68-year fit period.

Annual raw global means for 2017-2024 were 17.91, 19.12, 17.59, 19.17, 18.90, 17.55, 17.49 and 17.31 km/h. For 2025 (operational JTWC data) the value was 18.96 km/h.

### Composition (Figure 2)

| Cell definition | 1949-2016 change | p | 2017-2024 residual vs extended trend |
|---|---|---|---|
| none (raw) | -8.6% | <0.001 | +0.77 |
| region | -9.5% | <0.001 | +0.67 |
| month | -9.7% | <0.001 | +0.83 |
| region x month | -9.8% | <0.001 | +0.70 |
| 5-degree latitude band | -3.7% | 0.02 | -0.04 |
| region x latitude band | -4.9% | 0.001 | +0.04 |
| region x latitude band x month (primary) | -3.9% | 0.007 | +0.04 |
| region x 2.5-degree band x month | -3.8% | 0.012 | +0.02 |
| ... x nature (TS / ET / other) | -3.4% | 0.019 | +0.17 |
| ... x 6-hourly wind category | -2.0% | 0.17 | -0.04 |

(p values here are naive OLS p values of the 1949-2016 trend.) Mean absolute latitude of segments decreased by 0.39 degrees per decade in 1949-2016 (p < 0.001). The poleward share was 13.0% (1949-1969), 9.5% (1970-1989), 9.7% (1990-2006), 9.4% (2007-2016) and 12.5% (2017-2024). Most of the poleward segments are in the North Atlantic and western North Pacific. In these two regions the poleward share was 33% and 9% in 2007-2016, and 41% and 12% in 2017-2024.

### Basins and land (Figure 3)

No single basin or hemisphere rejected its frozen trend at p < 0.05, but all eight basin and hemisphere residuals are positive (range +0.02 to +1.31 km/h). The over-land results are given in the summary. All values are in `files/data/forecast_test_table.csv` and `files/data/prediction_tests.json`.

## Limitations

- The test period is 8 seasons. The raw rejection (p = 0.03) depends mainly on 2018, 2020 and 2021, and the intensity variants are borderline (p = 0.06-0.11). The evidence is that the raw trend did not continue as a line. It does not show a reversal.
- The latitude adjustment does not tell why the latitude mix changed. Possible causes are a real poleward shift of TC activity (an earlier campaign study, cf44cb4a, found that the latitude of peak intensity continued to move poleward in 2013-2025), changes in how far agencies follow storms into the extratropics, and early under-detection of low-latitude stages. If the latitude shift is physical, the raw mean speed is the correct measure of local exposure. In that case the adjusted series answers a different question: do storms move slower at a given place and season?
- Wind categories before satellite data are not consistent. Thus the -2.0% wind-adjusted value is only a sensitivity check.
- We used the IBTrACS land mask, not ETOPO2, and IBTrACS v04r01, not v03r10. HURDAT2 reanalysis has changed some Atlantic tracks before 1966 since 2018. These differences can explain why our reproduction is about 1.5 percentage points weaker than the published -10%.
- We did not analyze rainfall, stalls of individual storms, or attribution to circulation change.

## Reproduce

1. `bash files/code/00_get_ibtracs.sh /some/scratch` downloads the netCDF to local scratch and checks its hash. NCEI regenerates the file; a later version can differ slightly.
2. In a folder that contains `code/` (a copy of `files/code/`): `bash code/run_all.sh /some/scratch/IBTrACS.ALL.v04r01.nc`. This needs Python 3.12 with numpy 2.5, pandas 3.1, scipy 1.18, netCDF4 1.7, pyarrow 26 and matplotlib 3.11. It writes `derived/` and `figures/` in about 5 minutes. All random seeds are fixed. We ran it again from a clean folder and got the same tables.
3. `files/data/segments.parquet` has all 223,676 segments (derived from US-government public-domain best tracks), so you can do steps 3-6 without the netCDF.

## Files

- `files/PLAN.md`: analysis plan, written before the test-period calculations.
- `files/code/`: retrieval script, pipeline (`01`-`06`) and `run_all.sh`.
- `files/data/annual_mean_speed.csv`: raw annual means for every subset and variant (`variant:subset` columns).
- `files/data/annual_adjusted_speed.csv`, `composition_spec_series.csv`: adjusted annual series.
- `files/data/forecast_test_table.csv` (note: the North Atlantic subset is the string `NA`; read with `keep_default_na=False`), `prediction_tests.json`, `composition_specs.csv`, `composition_indicators.csv`.
- `files/data/segments.parquet`: segment table.
- `files/figures/`: Figures 1-3.
- `files/NOTICE-external-data.md`: source and terms of the external data.

## Provenance

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-bbea7dba9426, topic earth-and-ocean-sciences, machine dell. Analysis by the AI model Claude Opus 5.5 (claude-opus-5-5), run 2026-11-09. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Kossin, J. P. (2018). A global slowdown of tropical-cyclone translation speed. Nature 558, 104-107. doi:10.1038/s41586-018-0158-3
- Moon, I.-J., Kim, S.-H. & Chan, J. C. L. (2019). Climate change and tropical cyclone trend. Nature 570, E3-E5. doi:10.1038/s41586-019-1222-3
- Lanzante, J. R. (2019). Uncertainties in tropical-cyclone translation speed. Nature 570, E6-E15. doi:10.1038/s41586-019-1223-2
- Kossin, J. P. (2019). Reply to: Moon, I.-J. et al.; Lanzante, J. R. Nature 570, E16-E22. doi:10.1038/s41586-019-1224-1
- Chan, K. T. F. (2019). Are global tropical cyclones moving slower in a warming climate? Environ. Res. Lett. 14, 104015. doi:10.1088/1748-9326/ab4031
- Knapp, K. R. et al. (2010). The International Best Track Archive for Climate Stewardship (IBTrACS). BAMS 91, 363-376. doi:10.1175/2009BAMS2755.1
- Gahtan, J. et al. (2024). IBTrACS Project, Version 4r01. NOAA NCEI. doi:10.25921/82ty-9e16
