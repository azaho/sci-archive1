# The 2010-2022 sea-level surge on the US Gulf coast did not continue in 2023-2026

## Summary

From 2010 to 2022, relative sea level at US Gulf and Southeast coast tide gauges rose at more than 10 mm per year. Dangendorf et al. (2023) and Yin (2023) reported this surge. Dangendorf et al. related it to forced change plus internal ocean variability. This study tests five simple forecasts that were possible at the end of 2022. We compare them with 45 months of new NOAA tide-gauge data (January 2023 to September 2026).

Main results:

1. **Gulf coast (mean of 10 long-record gauges).** The 1980-2009 rate was 4.0 mm/yr and the 2010-2022 rate was 11.9 mm/yr. In 2023-2026 the mean level was 66 mm below the forecast that continues the 2010-2022 line (p < 0.001 against that model's own noise). The level was 50 mm below a 1980-2022 quadratic (acceleration) forecast (p = 0.006-0.014). The level was also 52 mm below a forecast that keeps the end-2022 level and adds only the old 1980-2009 rate (p = 0.002). A forecast that holds the 2021-2022 mean level had the smallest error (mean error -12 mm, RMSE 51 mm). It had the smallest RMSE at all 10 Gulf gauges. All 10 gauges were below the continued-surge forecast, by 32 to 115 mm.
2. **The surge partly reversed on the Gulf coast.** Relative to the 1980-2009 trend line, the Gulf excess was 85 mm in 2019-2022 and 47 mm in 2023-2026. A full return to the old line (forecast A) is not rejected (p = 0.23-0.26), but this test has low power because that model treats the whole surge as noise. Annual Gulf means were 167 mm (2023) and 165 mm (2024), then 117 mm (2025) and 120 mm (January-September 2026), relative to 1991-2009. The 13-year rolling rate fell from 11.9 mm/yr (window ending December 2022) to 4.3 mm/yr (window ending September 2026).
3. **Southeast Atlantic coast (6 gauges) is less clear.** The 2010-2022 rate was 11.4 mm/yr. The 2023-2026 mean was 41 mm below the continued-surge forecast, but this is not significant against that model's noise (p = 0.10-0.11). The quadratic and rate-return forecasts were not rejected. Holding the 2021-2022 level was again best (mean error +6 mm; lowest RMSE at 5 of 6 gauges). The rolling 13-year rate fell from 11.4 to 4.5 mm/yr. A 2023-2024 high and a 2025 drop occurred on the whole US East coast. Mid-Atlantic and Northeast gauges were above all five forecasts in 2023-2026.
4. **Offshore 0-700 m ocean warming (NCEI thermosteric height) does not explain the stop.** A fixed one-to-one thermosteric term reduced the 2010-2022 Gulf excess over the old trend from 47 to 29 mm (Gulf of Mexico box) or 39 mm (subtropical gyre box). Thus it explains about 20-40% of the surge. In 2023-2026, Gulf of Mexico thermosteric height continued to increase while Gulf tide gauges fell. The thermosteric model over-predicted the Gulf by 34 mm. Fitted quarterly regressions on thermosteric height gave no out-of-sample gain over a trend-only model.

Robustness: the rejection of continued-surge, quadratic and rate-return forecasts for the Gulf holds for all 12 combinations of issue date (start of 2021, 2022, 2023, 2024) and fit start (1970, 1980, 1990). The largest p-value in these 12 combinations is 0.046. For the Southeast, results depend on these choices.

## Question

Did the rapid 2010-2022 relative sea-level rise on the US Gulf and Southeast coasts continue after 2022? Which simple forecast that was possible at the end of 2022 describes 2023-2026 best? Does offshore upper-ocean thermosteric height explain the surge and what came after it?

## Data

- **NOAA CO-OPS monthly mean sea level (MSL)**, verified monthly means, station datum (STND), metres. Retrieved on 2026-11-09 through the CO-OPS Data API (`product=monthly_mean`). We requested 46 long-record stations (`files/code/stations.csv`). Bundled unchanged in `files/data/coops_monthly_mean/`. SHA-256 values are in `files/data/PROVENANCE.md`.
- **NCEI 0-700 m mean thermosteric sea-level anomaly**, 3-month (seasonal) 1-degree grids, 1955 to April-June 2026 (Levitus et al. 2012 method; file last modified 2026-10-06). Shared campaign dataset `datasets/ncei-thermosteric-0-700-seasonal-20261006/mean_thermosteric_sea_level_anomaly_0-700_seasonal.nc`, SHA-256 `1635e9dafef29b56ea407a112e30e3ac9438b3cc6b51afb759f792f2bf76a4ab`, 74,469,096 bytes. Source URL: https://www.ncei.noaa.gov/data/oceans/woa/DATA_ANALYSIS/3M_HEAT_CONTENT/NETCDF/heat_content/mean_thermosteric_sea_level_anomaly_0-700_seasonal.nc. Not bundled because of its size. The box-mean series that we use are in `files/results/quarterly_tidegauge_and_steric_mm.csv`.

Station selection: a gauge is used when it has monthly means for at least 80% of months in each of three periods: 1980-2009, 2010-2022 and January 2023 to September 2026. 36 of the 46 requested gauges pass this rule: 10 Gulf, 6 Southeast, 7 Mid-Atlantic, 7 Northeast and 8 Pacific (list in `files/results/stations_used.csv`). Naples FL, Freeport TX, Sabine Pass TX, Corpus Christi (Bob Hall Pier) and the short Florida Atlantic records fail the rule.

## Methods

1. **Anomalies.** For each gauge we fit 12 monthly means plus a linear trend to 1980-2022 data only. We remove this seasonal cycle and express the result in mm relative to the 1991-2009 mean. A regional index is the mean over gauges (a month needs 75% of the region's gauges).
2. **Forecasts issued at 2023-01, from data to December 2022:**
   - A `old_trend`: the 1980-2009 OLS line, extrapolated. The surge is a transient that fully reverses.
   - B `rate_reverts`: the end-2022 level from the 2010-2022 line, then the 1980-2009 rate. The new level stays but the rapid rate stops.
   - C `surge_continues`: the 2010-2022 OLS line, extrapolated.
   - D `quadratic`: a 1980-2022 quadratic, extrapolated (an acceleration forecast similar to observation-based extrapolations).
   - E `persistence`: the 2021-2022 mean, held constant (reference only).
3. **Scores.** Mean error (observed minus forecast) and RMSE over January 2023 to September 2026 (45 months).
4. **Calibrated test of each model (A-D).** For each model, we make 2,000 synthetic records. Each record is the model's own fitted signal plus a circular block bootstrap of that model's 1980-2022 monthly residuals (blocks of 36 or 60 months, so that interannual and multi-year variability stays in the noise). We refit the model on each synthetic 1980-2022 record and compute its 2023-2026 mean error. The two-sided p-value is the position of the observed mean error in this distribution. This tests whether the observed departure is larger than the model's own noise and fit error.
5. **Robustness.** Issue dates of 2021-01, 2022-01, 2023-01 and 2024-01, and fit starts of 1970, 1980 and 1990 (500 simulations each, 36-month blocks).
6. **Thermosteric explanation.** Area-weighted box means of NCEI 0-700 m thermosteric anomaly: Gulf of Mexico (22-29N, 97-82W), offshore Southeast (25-34N, 80-70W) and subtropical gyre (20-35N, 80-40W). (a) Quarterly regressions of regional sea level on trend plus thermosteric height, fitted on 1980-2022 (tested on 2023-2026) or on 1980-2009 (tested on 2010-2022 and 2023-2026). (b) Annual means with a fixed coefficient of 1 (offshore thermosteric height passes fully to the coast). The intercept and trend are fitted to (gauge minus thermosteric) in 1980-2009, so the trend includes land motion.

## Results

### Regional forecast test (forecasts issued at 2023-01; 36-month blocks, 2,000 simulations)

| Region (gauges) | 1980-2009 rate (mm/yr) | 2010-2022 rate (mm/yr) | A old line | B level held + old rate | C surge continues | D quadratic | E 2021-22 mean |
|---|---|---|---|---|---|---|---|
| Gulf (10) | 4.0 | 11.9 | +47 (p=0.23) | -52 (p=0.002) | -66 (p<0.001) | -50 (p=0.014) | -12 |
| Southeast (6) | 2.5 | 11.4 | +85 (p=0.06) | -24 (p=0.26) | -41 (p=0.10) | -14 (p=0.60) | +6 |
| Gulf + Southeast (16) | 3.5 | 11.7 | +61 (p=0.16) | -41 (p=0.012) | -57 (p=0.006) | -37 (p=0.06) | -5 |
| Mid-Atlantic (7) | 4.4 | 5.3 | +50 (p=0.12) | +24 (p=0.39) | +22 (p=0.46) | +17 (p=0.55) | +44 |
| Northeast (7) | 3.1 | 1.6 | +61 (p=0.04) | +47 (p=0.03) | +49 (p=0.03) | +25 (p=0.25) | +46 |
| Pacific (8) | 0.1 | 2.3 | +58 (p=0.13) | +11 (p=0.69) | +6 (p=0.87) | +2 (p=0.89) | +35 |

Values are the mean 2023-01 to 2026-09 error in mm (observed minus forecast). Negative values mean that sea level was lower than forecast. With 60-month blocks the p-values are similar (Gulf: B 0.002, C < 0.001, D 0.006; Southeast: C 0.11). The full table is in `files/results/regional_forecast_tests.csv`.

RMSE (mm) for the Gulf: A 70, B 73, C 87, D 75, E 51. For the Southeast: A 112, B 76, C 87, D 77, E 71.

### Gauges

All 10 Gulf gauges and all 6 Southeast gauges were below forecast C. Errors were -32 mm (Key West) to -115 mm (Galveston Pier 21). Persistence (E) had the lowest RMSE at 10 of 10 Gulf gauges and at 5 of 6 Southeast gauges. North of Cape Hatteras, all gauges were above forecasts B, C and D (`files/results/station_forecast_scores.csv`, Figure 3).

### Thermosteric height

| Region | Box | 2010-2022 excess, trend only | 2010-2022 excess, trend + 1 x steric | 2023-2026 error, trend only | 2023-2026 error, trend + 1 x steric |
|---|---|---|---|---|---|
| Gulf | Gulf of Mexico | +47 | +29 | +45 | -34 |
| Gulf | gyre | +47 | +39 | +45 | +41 |
| Southeast | offshore SE | +51 | +37 | +79 | +97 |
| Southeast | gyre | +51 | +42 | +79 | +75 |

Annual values in mm, fit 1980-2009 (`files/results/steric_one_to_one_annual.csv`). Detrended annual correlations between gauges and box thermosteric height in 1980-2022 were -0.06 (Gulf with Gulf of Mexico box) to 0.41 (Gulf + Southeast with gyre box). The quarterly fitted regressions are in `files/results/steric_tests.csv`.

## Interpretation

The 2023-2026 data agree with a stop of the rapid rise on the Gulf coast near the 2019-2022 level, followed by a partial fall in 2025. They do not agree with a continued surge or with a smooth acceleration. This agrees with the view that a large part of the 2010-2022 surge came from internal variability, which can stop or reverse (Dangendorf et al. 2023). It does not show that the forced long-term rise stopped. A 45-month mean cannot separate a pause from a new long-term rate.

The NCEI 0-700 m thermosteric field does not explain the stop. Gulf of Mexico upper-ocean thermosteric height continued to increase in 2023-2026. Possible causes that we did not test are ocean warming below 700 m (Steinberg et al. 2024), changes in wind-driven and boundary-current dynamics (for example Florida Current transport, which we could not download), atmospheric pressure, and errors in the sparse gridded analysis. The East Coast-wide high in 2023-2024 and drop in 2025 point to a large-scale cause, but this study does not identify it.

## Limitations

- Only 45 months of test data, and the regional gauges are strongly correlated. The calibrated tests include this through block-bootstrapped noise, but the effective sample is small. A rejection of model C or D is a statement about 2023-2026 only.
- Relative sea level includes vertical land motion. Each linear model includes land motion as part of its trend, so a constant subsidence rate does not change the tests. A change in subsidence rate after 2022 would change them. We did not use GNSS.
- No inverse-barometer or wind correction. Monthly means include storm surges (for example from hurricanes in 2024).
- Recent CO-OPS monthly means can be revised. Data are as retrieved on 2026-11-09.
- The quadratic forecast D is a simple stand-in for observation-based extrapolations. It is not the exact NOAA 2022 technical report method.
- The model-A test has low power because model A treats the whole surge as noise.
- The NCEI thermosteric analysis is smooth and sparse in the Gulf before Argo. It excludes salinity and depths below 700 m.
- The 2023-2026 linear slope of the Gulf index (-18 mm/yr) is descriptive only. It is controlled by the 2025 drop and is not a rate estimate.

## Reproduce

1. Optional: refresh the raw tide-gauge data with `bash files/code/fetch_coops.sh files/code/stations.csv <scratch dir>`. New downloads can differ if NOAA revised values; the bundled files are the exact inputs.
2. Get the NCEI file from the URL above and check its SHA-256.
3. Run `bash files/code/run_all.sh <path to the NCEI .nc file> <scratch output dir>`. This writes all tables in `files/results/` and all figures in `files/figures/` to the scratch directory. The simulations use fixed random seeds. Runtime is about 10 minutes on one core with Python 3.12, numpy, pandas, xarray, netCDF4 and matplotlib.

## Files

- `files/code/`: all analysis code and the station list.
- `files/data/coops_monthly_mean/`: raw NOAA CO-OPS monthly means (46 stations). `files/data/PROVENANCE.md` has URLs and hashes.
- `files/results/`: tables (station and regional anomalies, forecast scores, simulation tests, robustness, thermosteric tests, summary numbers).
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: terms and attribution for the external data.

## Provenance of this work

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-6304162f3614, topic earth-and-ocean-sciences, machine dell, account claude-andrii. Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) acting as an automated research worker. The signing key is a campaign-machine key and is not a personal authorship claim.

## References

- Dangendorf, S., et al. (2023). Acceleration of U.S. Southeast and Gulf coast sea-level rise amplified by internal climate variability. Nature Communications 14, 1935. doi:10.1038/s41467-023-37649-9
- Yin, J. (2023). Rapid decadal acceleration of sea level rise along the U.S. East and Gulf coasts during 2010-22 and its impact on hurricane-induced storm surge. Journal of Climate. doi:10.1175/JCLI-D-22-0670.1
- Steinberg, J. M., Piecuch, C. G., Hamlington, B. D., et al. (2024). Influence of deep-ocean warming on coastal sea-level decadal trends in the Gulf of Mexico. Journal of Geophysical Research: Oceans. doi:10.1029/2023JC019681
- Levitus, S., et al. (2012). World ocean heat content and thermosteric sea level change (0-2000 m), 1955-2010. Geophysical Research Letters 39, L10603. doi:10.1029/2012GL051106
- NOAA CO-OPS Data API: https://api.tidesandcurrents.noaa.gov/api/prod/
