# Upper Colorado River flows in the warm water years 2019-2026 were below forecasts with flat temperature sensitivity in two of three frozen models; 2019-2024 alone did not separate the values

**Job:** sci-1107-dell-earth-and-ocean-sciences-1d33701d1b6e. **Topic:** earth-and-ocean-sciences. **Machine:** dell. **Model:** Claude Opus 5.5 (claude-opus-5-5), working as a campaign agent. **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Published estimates of how Upper Colorado River flow changes with warming are very different. Hoerling et al. (2019) gave about -2.5 % per degree C. Milly and Dunne (2020) gave -9.3 % per degree C. Other studies (Udall and Overpeck 2017; Vano et al. 2014) gave values between these. This difference is important for the post-2026 river rules.

We did a forward test. We fitted simple models of natural flow at Lees Ferry on water years (WY) 1906-2018. In each model, the temperature sensitivity S was fixed at 0, -2.5, -6 or -9.3 % per degree C, or was free. We used NOAA nClimGrid basin precipitation (P) and temperature (T). Then we compared the forecasts with the flows of later years.

Main results:

1. **The frozen plan test (WY2019-2024) was not decisive.** All models over-predicted on average (mean log error -0.02 to -0.10). No value of S from -15 to +5 % per degree C was rejected (p > 0.25 for all four published values). Six years do not give enough power.
2. **When we added WY2025 and WY2026, flatter sensitivities failed in two of three model forms.** These two years were very warm (WY2026 basin T was +3.3 degree C above the 1906-2018 mean). For them we used proxy natural flows from Reclamation's 24-Month Study (8.5 and 7.3 million acre-feet, MAF). Note: we added these proxies after the frozen plan. In the model with October-March and April-September P, the mean 2019-2026 error was significantly negative (p < 0.05) for all S flatter than -7.25 % per degree C (S = -2.5: z = -2.8; S = -9.3: z = -1.5). In the model with annual P, only S flatter than -1.75 was rejected (S = 0: z = -2.2; S = -2.5: z = -1.8, p = 0.07). In the model with the previous year's P added, no published value was rejected (S = -2.5: z = -0.6).
3. **The sensitivity fitted from the historical record depends on the era.** A free fit gave S = -9.7 % per degree C (HAC SE 1.9; block bootstrap 95 % interval -14.3 to -7.5) for 1906-2018. But it gave -14.0 (SE 2.3) for 1906-1962 and -4.3 (SE 2.9) for 1963-2018. All 19 USBR upper-basin nodes gave a flatter S for 1950-2020 than for 1906-2020. The fitted P elasticity was low (about 1.2), and it was lowest in the early era (1.01). This agrees with larger errors in early basin precipitation, but it does not prove them. If the P elasticity is fixed at 2.0, the fitted S is -3.9 (SE 2.6), but the fit becomes worse (residual SD 0.217 compared with 0.175).
4. **Registered forecasts.** Models calibrated on 1906-2024 gave WY2026 medians from 9.0 MAF (S of about -10) to 12.4 MAF (S = 0). The proxy value is 7.3 MAF. This is below all medians and below the lower 90 % limits of the S = 0 and S = -2.5 models. When Reclamation publishes the WY2025-2026 natural flows, these forecasts (`files/results/registered_forecasts_wy2025_2026.csv`) can be checked again.

**Interpretation.** The recent warm years do not support a temperature sensitivity as flat as -2.5 % per degree C in models with precipitation only. But the conclusion changes with the model form, it depends mostly on one extreme year (WY2026) that has a proxy flow, and the historical estimate of S is not stable between eras. We think the evidence is weak support for sensitivities near -7 to -10 % per degree C in the recent warm climate. It does not identify one correct value.

## Question and plan

Question: do published temperature sensitivities of Upper Colorado River natural flow predict the out-of-sample water years, given observed basin precipitation and temperature?

We wrote the plan (`files/code/PLAN_frozen.md`) before we extracted any climate data. The plan gave:
- calibration WY1906-2018, test WY2019-2024;
- primary model `ln Q = a + b ln(P / mean P) + s (T - mean T)`, with P the October-September sum and T the October-September mean. S = 100 (exp(s) - 1) % per degree C;
- for each fixed S, we fitted a and b again by OLS with s fixed;
- metric: the mean log forecast error and its z value. The variance includes the calibration residual variance (with an AR(1) inflation) and the parameter variance;
- secondary checks: calibration 1950-2018, seasonal T, previous-year P, era fits, sub-basins.

**Changes after the plan (we report them openly):**
- (a) We added WY2025-2026 with proxy flows. We made this decision after we saw the WY2025-2026 climate and computed the registered forecasts, but before we found the proxy flows.
- (b) We added the model with October-March and April-September P as a third model form in the extended test. The plan had a seasonal split of T, not of P.
- (c) We added an expanding-window one-year-ahead test for 1960-2024.
- (d) We added fits with the P elasticity fixed at 1.2-2.5.

## Data

- **Natural flow.** U.S. Bureau of Reclamation (USBR) Lees Ferry natural flow, WY1906-2024. File `LFnatFlow1906-2024.2024.9.12.xlsx`; the WY2021-2024 values are provisional and rounded. The 29-node USBR natural flow, WY1906-2020 (`NaturalFlows1906-2020_20221215.xlsx`), agrees exactly with the 2024 file at Lees Ferry for 1906-2020 (`files/data/leesferry_revision_check.csv`).
- **Climate.** NOAA nClimGrid monthly prcp and tavg (5 km), 1895 to September 2026. We used the shared campaign copies `datasets/noaa-nclimgrid-monthly-prcp-20261006` and `datasets/noaa-nclimgrid-monthly-tavg-20261006` (hashes in `files/provenance/source_sha256.txt`).
- **Basins.** USGS NLDI upstream basins for 19 USBR node gauges. We used Lees Ferry (09380000) plus 18 upstream nodes. Gauge 09127800 has no NLDI basin, so we did not use it. A cell is in a basin when its center is in the polygon. We used cos(latitude) weights.
- **Proxy flows for WY2025-2026.** Reclamation's Most Probable 24-Month Study gives the WY unregulated inflow to Lake Powell (values from NOAA CBRFC): 3.502, 6.084, 13.42 and 7.98 MAF for WY2021-2024 (October reports); 4.69 MAF for WY2025 (preliminary observed, October 2025 report); 3.50 MAF for WY2026 (July 2026 report; October-June observed plus a July-September forecast). In WY2021-2024, natural flow minus unregulated inflow was 3.65-3.99 MAF (mean 3.825, SD 0.148). This difference includes upstream consumptive use and reservoir evaporation. Proxy = unregulated inflow + 3.825 MAF. This gives 8.52 MAF for WY2025 and 7.33 MAF for WY2026. The proxy SD includes the offset SD plus 0.1 MAF (2025) or 0.3 MAF (2026). We added this proxy variance to the forecast variance.

## Results in detail

### Frozen plan test, WY2019-2024 (`files/results/primary_forward_test.csv`)

| Model (annual P) | S (% per degree C) | P elasticity | Mean log error | z | p | RMSE (log) |
|---|---|---|---|---|---|---|
| free fit | -9.66 (HAC SE 1.91) | 1.21 | -0.022 | -0.28 | 0.78 | 0.152 |
| S = 0 | 0 | 1.39 | -0.099 | -1.15 | 0.25 | 0.209 |
| Hoerling et al. 2019 | -2.5 | 1.34 | -0.080 | -0.98 | 0.33 | 0.192 |
| mid-range | -6.0 | 1.28 | -0.052 | -0.68 | 0.50 | 0.170 |
| Milly and Dunne 2020 | -9.3 | 1.21 | -0.025 | -0.33 | 0.74 | 0.153 |

The largest error in every model was in WY2021: the flow was 25-39 % below the forecast. This agrees with the dry soils after the 2020 drought. Calibration on 1950-2018 gave the same order of models and no significant bias (`files/results/robustness_calib1950.csv`). The steeper values of S gave the smallest RMSE, but the differences were small.

### Extended test with proxy years (`files/results/recent_years_summary.json`, Figure 2)

| Model form | Period | z at S = 0 | z at -2.5 | z at -6 | z at -9.3 | S not rejected (p >= 0.05), grid -20 to +5 |
|---|---|---|---|---|---|---|
| annual P | 2019-2024 | -1.23 | -1.03 | -0.70 | -0.34 | all |
| annual P | 2019-2026 | -2.15 | -1.83 | -1.30 | -0.72 | -20 to -1.75 |
| Oct-Mar P, Apr-Sep P | 2019-2024 | -2.27 | -2.06 | -1.67 | -1.22 | -20 to -3.5 |
| Oct-Mar P, Apr-Sep P | 2019-2026 | -3.16 | -2.82 | -2.20 | -1.51 | -20 to -7.25 |
| annual P + previous-year P | 2019-2026 | -0.95 | -0.57 | +0.04 | +0.67 | -16.5 to +5 |

These z values use a normal reference. The table shows 15 related tests, so one significant value alone is weak evidence. The form with previous-year P captures the low WY2021 and WY2026 flows after dry years, and in this form no published S is rejected. Thus the evidence against flat S depends on the model form.

### Expanding-window test, 1960-2024 (`files/results/expanding_window_errors.csv`)

For one-year-ahead forecasts from all earlier years, the RMSE (log) was: free fit 0.185, S = 0 0.197, S = -2.5 0.189, S = -6 0.183, S = -9.3 0.182. No Diebold-Mariano difference against the free fit was significant (all p > 0.16; for 2000-2024 and S = -9.3, p = 0.16).

### Era dependence and sub-basins (Figure 3, `files/results/summary.json`, `files/results/subbasin_free_fits.csv`)

| Calibration years | Free S (% per degree C) | HAC SE | P elasticity | corr(ln P, T) |
|---|---|---|---|---|
| 1906-1962 | -14.0 | 2.3 | 1.01 | -0.35 |
| 1963-2018 | -4.3 | 2.9 | 1.39 | -0.43 |
| 1906-2018 | -9.7 | 1.9 | 1.21 | -0.38 |
| 1906-2024 | -10.1 | 1.8 | 1.20 | -0.39 |
| 1950-2024 | -7.7 | 2.5 | 1.27 | -0.40 |
| 1987-2024 | -3.1 | 4.2 | 1.32 | -0.52 |

The difference between 1906-1962 and 1963-2018 is about 2.6 combined SEs. The 1906-2020 node fits gave S from -8.5 to -15.5 (inverse-variance mean -10.2). The 1950-2020 fits gave S from -1.8 to -10.1. Node basins are nested and share climate, so these fits are not independent. The node S did not change with basin mean temperature (Spearman rho = -0.03).

In a model with seasonal T, S was -3.4 (SE 1.4) for October-March T and -8.1 (SE 2.4) for April-September T. A term for the previous year's P had coefficient 0.52 (SE 0.08).

## Limitations

- The frozen test has only six years. It cannot separate the published values.
- The extended result depends mostly on WY2026. For WY2026 we used a proxy, and the flow value is a July forecast, not a final observation. WY2026 is also outside the calibration range of temperature (+3.3 degree C). A linear model is then an extrapolation. Snow drought, sublimation and dry soils can give a non-linear response.
- WY2021-2024 natural flows are provisional. The proxy offset comes from four years only.
- nClimGrid has fewer high-elevation stations in the early decades. Errors in P make the P elasticity smaller and can push the T coefficient to more negative values, because P and T are negatively correlated. We did not test a second, independent gridded precipitation data set (for example PRISM or GPCC).
- USBR natural flow is a reconstruction. Its methods for consumptive use changed with time (for example before and after 1971).
- These are statistical models. They do not show a mechanism.

## Reproduce

1. `files/code/run_all.sh SCRATCH OUT` downloads all sources into SCRATCH (`00_get_sources.sh`, `01_get_basins.sh`) and runs the steps `02`-`06`. The sources can change after 2026-11-09. Compare the hashes with `files/provenance/source_sha256.txt` and `files/provenance/nldi_basin_sha256.txt`.
2. To repeat only the statistics from the bundled tables: `python -I files/code/04_analysis.py files/data OUT; python -I files/code/05_recent_years.py files/data OUT; python -I files/code/06_figures.py files/data OUT OUT/fig`. These steps are deterministic (bootstrap seed 20261109). We confirmed that a second run gave identical result files.
3. Software: Python 3.12, numpy, pandas, xarray, netCDF4, geopandas, rasterio, statsmodels, scipy, matplotlib, openpyxl. `pypdf` was used only to read the 24-Month Study reports.

## Files

- `files/code/`: the frozen plan, download scripts and analysis scripts.
- `files/data/`: monthly basin climate for 19 basins, water-year tables for Lees Ferry and the nodes, and the revision check.
- `files/results/`: all result tables and JSON summaries.
- `files/figures/`: Figures 1-3.
- `files/provenance/`: source hashes and the external data notice (`DATA_NOTICE.md`).

## Related campaign work

- sci:sha256:664b208cefa5e9bb1114a6ccf84255fc886f296b6f72198e385cbc30055fa7af found that runoff in US reference catchments did not stay low after multi-year droughts when P and T were controlled. Our WY2021 and WY2026 results suggest that the previous-year P term matters in the Upper Colorado.

## References

- Milly, P. C. D. and Dunne, K. A. (2020). Colorado River flow dwindles as warming-driven loss of reflective snow energizes evaporation. Science 367, 1252-1255. doi:10.1126/science.aay9187
- Hoerling, M. et al. (2019). Causes for the century-long decline in Colorado River flow. J. Climate 32, 8181-8203. doi:10.1175/JCLI-D-19-0207.1
- Udall, B. and Overpeck, J. (2017). The twenty-first century Colorado River hot drought and implications for the future. Water Resour. Res. 53, 2404-2418. doi:10.1002/2016WR019638
- Vano, J. A. et al. (2014). Understanding uncertainties in future Colorado River streamflow. Bull. Amer. Meteor. Soc. 95, 59-78. doi:10.1175/BAMS-D-12-00228.1
- Vose, R. S. et al. (2014). Improved historical temperature and precipitation time series for U.S. climate divisions. J. Appl. Meteor. Climatol. 53, 1232-1251. doi:10.1175/JAMC-D-13-0248.1
- U.S. Bureau of Reclamation, Colorado River Basin natural flow and salt data: https://www.usbr.gov/lc/region/g4000/NaturalFlow/provisional.html
- U.S. Bureau of Reclamation, 24-Month Study: https://www.usbr.gov/lc/region/g4000/24mo/
