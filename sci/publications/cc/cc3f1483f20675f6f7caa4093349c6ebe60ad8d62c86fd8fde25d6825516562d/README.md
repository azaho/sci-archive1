# The 1951-2000 heavy-rain trend for central India matched the 2001-2025 IMD mean at 1-degree scale only with the 2005-2007 seasons; 0.25-degree counts stayed near the 1976-2000 level

## Summary

Goswami et al. (2006, Science) reported that heavy monsoon rain events over central India became more frequent from 1951 to 2000. Moderate events became less frequent. Lin and Huybers (2019, GRL) said that part of this rise can come from changes in the rain-gauge network, with a jump after 1975. We did an out-of-sample test with 25 new monsoon seasons (2001-2025).

We used the India Meteorological Department (IMD) 0.25-degree daily gridded rainfall (Pai et al. 2014) for 1951-2025. We kept the Goswami definitions: June-September (JJAS), central India 74.5-86.5E and 16.5-26.5N, heavy is 100 mm/day or more, very heavy is 150 mm/day or more, moderate is 5 to below 100 mm/day. We counted grid-day events at two scales: 1-degree box means (the scale that Goswami used) and the native 0.25-degree cells. We fitted three models to 1951-2000 only and forecast 2001-2025:

- a stationary mean,
- a log-linear trend (the Goswami form),
- a step at 1976 (the form that a network jump after 1975 gives; its forecast is the 1976-2000 mean).

Main results:

1. **1-degree heavy events.** The 2001-2025 mean was 35.1 events per season. The trend forecast was 36.2 (observed/forecast 0.97, 95% season-bootstrap interval 0.80-1.17). The step forecast was 25.3 (ratio 1.39, 1.15-1.67). The stationary forecast was 21.7. The trend cut the mean squared error by 32% against the stationary forecast (interval -54% to +1%).
2. **The 1-degree agreement depends on 2005-2007.** These three seasons had 59, 96 and 63 heavy events. Without them, the 2001-2025 mean was 0.82 of the trend forecast (0.72-0.92) and 1.18 of the step forecast (1.04-1.33). So the counts are between the two models.
3. **0.25-degree cells did not follow the trend.** Heavy cell events were 0.91 of the trend forecast (0.80-1.03) and 1.10 of the step forecast (0.98-1.25). Very heavy cell events were 0.80 of the trend forecast (0.65-0.97) and 1.17 of the step forecast (0.96-1.43). Without 2005-2007, both 0.25-degree series were at the step forecast (ratios 1.01 and 1.00) and clearly below the trend (0.83 and 0.67).
4. **No rise inside 2001-2025.** The trend inside 2001-2025 was -8% per decade for 1-degree heavy events (95% interval -32% to +23%) and -3% per decade for 0.25-degree heavy events (-18% to +16%). The interval is wide, so a continued rise is not excluded. In the 1951-2000 fit, most of the rise came before 1976 (+37% per decade in 1951-1975; +5% per decade, not significant, in 1976-2000).
5. **Moderate events stopped their decline.** Moderate counts rose 5-6% per decade in 2001-2025 (p = 0.003 at both scales). The 1951-2000 trend forecast was too low (observed/forecast 1.03 at 1 degree and 1.05 at 0.25 degree). The JJAS mean rain did not change: 894, 874 and 886 mm in 1951-1975, 1976-2000 and 2001-2025.
6. **Box-mean extremes rose faster than cell extremes.** The ratio of 1-degree to 0.25-degree heavy counts was 0.025, 0.029 and 0.037 in the three 25-year periods. Larger rain systems or a thinner station network can cause this.
7. **Station-network proxy.** The IMD files do not give station counts, so we made a proxy: the number of strict local extrema per 100 cells on wet days. IMD interpolation keeps station values at station cells, so more reporting stations give more extrema. The proxy has a minimum in 1971-1972, when Lin and Huybers report a large station loss. It is high in 1990-1999, low in 2005-2015, and high again in 2023-2025. An October-May version, which does not use monsoon rain, correlates with the JJAS version (r = 0.42) and also falls after 2000. Fewer extrema went with more 1-degree heavy events. This relation explains about +12% (-0.4% to +25%) of the +39% change in 1-degree heavy events from 1976-2000 to 2001-2025 with the JJAS proxy, and about +3% with the October-May proxy. The trend stayed significant after we added the proxy and the seasonal total to the model.
8. **PERSIANN-CDR cannot check the extremes.** The satellite product agreed with the IMD seasonal totals (r = 0.92, 1983-2025). But its counts of high daily values over central India fell after 1997 (by 51% at 40 mm, 76% at 60 mm and 86% at 80 mm, 1998-2025 against 1983-1997), while its totals did not change. This is a product change, not a rain change, so we did not use PERSIANN-CDR to test the trend.

Our conclusion: the IMD record does not support a simple continuation of the 1951-2000 log-linear rise into 2001-2025. At the 0.25-degree scale, 2001-2025 counts were near the 1976-2000 level. At the 1-degree scale, the counts matched the trend only because of three very wet seasons (2005-2007). A part of the 1-degree rise can come from changes in the station network, but our proxy explains only a small part.

## Question and prior claims

- Goswami et al. 2006 (doi:10.1126/science.1132027): significant rising trends in the frequency of heavy (100 mm or more) and very heavy (150 mm or more) events, and a falling trend of moderate events, over central India in JJAS 1951-2000. They used the IMD 1-degree grid (1,803 stations).
- Rajeevan et al. 2008 (doi:10.1029/2008GL035143): a smaller trend in 1901-2004 data, with large decadal changes.
- Roxy et al. 2017 (doi:10.1038/s41467-017-00744-9): a threefold rise in widespread extreme events in 1950-2015.
- Lin and Huybers 2019 (doi:10.1029/2018GL079709): station-network change makes a jump toward more extreme rain after 1975 in IMD data. Trends after the jump are not significant.

Our test: if the Goswami trend is a real and continuing change, the 2001-2025 counts should follow the 1951-2000 log-linear extrapolation. If the rise is only a network step near 1975, the 2001-2025 counts should stay at the 1976-2000 level.

## Data

| Data | Version and access | Use | Terms |
| --- | --- | --- | --- |
| IMD 0.25-degree daily gridded rainfall (Pai et al. 2014, MAUSAM 65:1-18, doi:10.54302/mausam.v65i1.851) | Yearly binary files `ind<YYYY>_rfp25.grd`, 1951-2025, from the POST form `https://www.imdpune.gov.in/cmpg/Griddata/rainfall.php` (page `Rainfall_25_Bin.html`), downloaded 2026-11-09 | All counts | No license text on the download page; the page asks users to cite Pai et al. (2014). We do not redistribute IMD grids. |
| PERSIANN-CDR v01r01 daily (Ashouri et al. 2015, doi:10.1175/BAMS-D-13-00068.1) | `https://www.ncei.noaa.gov/data/precipitation-persiann/access/<YYYY>/`, JJAS 1983-2025, 5,246 files, downloaded 2026-11-09 | Independent check | NOAA Climate Data Record, US government data. |

SHA-256 of every input file is in `files/provenance/imd_input_files_sha256.tsv` (75 files) and `files/provenance/persiann_input_files_sha256.tsv` (5,246 files). We downloaded the IMD 2020 NetCDF (`RF25.php`) once. It holds the same values as the binary file (maximum difference 0), and it has no station-count variable. IMD can revise recent years, so later downloads can give different hashes.

## Methods

- **Counting** (`code/process_imd.py`). For each JJAS season, we count central-India land values at or above 25, 50, 75, 100, 125, 150, 200 and 250 mm, and values from 5 to below 100 mm. The 0.25-degree domain has 1,845 land cells. The 1-degree boxes are centred on X.5 degrees. Each box mean uses the 0.25-degree points in [X, X+1) and needs at least half of its 16 points on land (129 boxes).
- **Forecast test** (`code/analyze.py`). We fit Poisson GLMs with a quasi-Poisson scale to 1951-2000: constant, log-linear year trend, and a step at 1976. We forecast 2001-2025 and score the mean squared error, the Poisson deviance, and the observed/forecast ratio of the 25-season mean. Intervals come from 10,000 paired bootstrap resamples of the 2001-2025 seasons (seed 20261109). Trend intervals use HAC standard errors (2 lags).
- **Sensitivity.** We exclude 2005-2007, compute leave-one-season-out ranges, and vary the threshold from 50 to 250 mm. We also scan single break years from 1961 to 2015 and compare quasi-AIC values for 1951-2025.
- **Seasonal total.** We add the log of the JJAS central-India mean rain as a covariate.
- **Network proxy** (`code/network_proxy.py`). For each season, we count strict local maxima and minima (against all 8 neighbours) per 100 interior land cells, on days with a central-India mean of 5 mm or more (JJAS) or 2 mm or more (October-May). We also compute a neighbour-difference roughness value. We add the proxy to the 1951-2025 Poisson model with trend and log seasonal total.
- **PERSIANN-CDR** (`code/fetch_persiann.py`, `code/process_persiann.py`). We cut out the India area and make 1-degree box means over the IMD land boxes. We choose the threshold that matches the IMD 1983-2000 mean count.

`files/provenance/analysis_plan.md` is the plan that we wrote before we computed any count. These analyses are additions that we made after we saw the first results: the network proxy, the exclusion of 2005-2007, the leave-one-out ranges and the observed/forecast ratio intervals. The 1976 step date comes from Lin and Huybers (break after 1975). It was fixed before the test.

## Results tables

Mean events per JJAS season (central India):

| Series | 1951-1975 | 1976-2000 | 2001-2025 | Stationary forecast | Trend forecast | Step forecast |
| --- | --- | --- | --- | --- | --- | --- |
| Heavy, 1-degree | 18.0 | 25.3 | 35.1 | 21.7 | 36.2 | 25.3 |
| Very heavy, 1-degree | 2.2 | 3.4 | 5.8 | 2.8 | 5.5 | 3.4 |
| Moderate, 1-degree | 6,208 | 5,924 | 5,828 | 6,066 | 5,637 | 5,924 |
| Heavy, 0.25-degree | 713 | 866 | 955 | 790 | 1,053 | 866 |
| Very heavy, 0.25-degree | 149 | 216 | 254 | 183 | 319 | 216 |
| Moderate, 0.25-degree | 75,640 | 71,862 | 71,548 | 73,751 | 68,023 | 71,862 |

Observed/forecast ratio of the 2001-2025 mean (95% season-bootstrap interval):

| Series | Trend, all seasons | Step, all seasons | Trend, without 2005-2007 | Step, without 2005-2007 |
| --- | --- | --- | --- | --- |
| Heavy, 1-degree | 0.97 (0.80-1.17) | 1.39 (1.15-1.67) | 0.82 (0.72-0.92) | 1.18 (1.04-1.33) |
| Very heavy, 1-degree | 1.07 (0.70-1.54) | 1.70 (1.12-2.44) | 0.74 (0.54-0.94) | 1.19 (0.87-1.52) |
| Moderate, 1-degree | 1.03 (0.99-1.08) | 0.98 (0.94-1.03) | 1.04 (0.99-1.09) | 0.99 (0.94-1.04) |
| Heavy, 0.25-degree | 0.91 (0.80-1.03) | 1.10 (0.98-1.25) | 0.83 (0.75-0.90) | 1.01 (0.92-1.10) |
| Very heavy, 0.25-degree | 0.80 (0.65-0.97) | 1.17 (0.96-1.43) | 0.67 (0.58-0.75) | 1.00 (0.87-1.12) |
| Moderate, 0.25-degree | 1.05 (1.01-1.10) | 1.00 (0.95-1.04) | 1.06 (1.01-1.11) | 1.00 (0.95-1.05) |

Trends (% per decade, HAC 95% interval):

| Series | 1951-2000 | 1951-1975 | 1976-2000 | 2001-2025 | 1951-2025 |
| --- | --- | --- | --- | --- | --- |
| Heavy, 1-degree | +15.2 (4.0, 27.5) | +36.7 (1.9, 83.3) | +4.7 (-12.4, 25.0) | -8.4 (-31.9, 23.3) | +13.1 (7.0, 19.6) |
| Very heavy, 1-degree | +19.9 (4.5, 37.5) | +73.1 (12.8, 165.8) | -0.2 (-31.1, 44.5) | -31.1 (-59.7, 17.7) | +17.5 (6.8, 29.3) |
| Heavy, 0.25-degree | +8.1 (2.9, 13.6) | +10.2 (-1.8, 23.7) | +6.4 (-5.5, 19.9) | -2.8 (-18.4, 15.7) | +5.7 (2.7, 8.8) |
| Very heavy, 0.25-degree | +16.6 (9.2, 24.5) | +30.0 (8.0, 56.5) | +11.0 (-4.8, 29.4) | -12.9 (-34.9, 16.5) | +10.1 (4.9, 15.5) |
| Moderate, 1-degree | -1.9 (-4.0, 0.1) | -4.2 (-11.1, 3.3) | 0.0 (-2.9, 3.0) | +5.6 (1.8, 9.5) | -1.1 (-2.4, 0.3) |

Our 1-degree heavy trend for 1951-2000 (+15% per decade) is near the value of about 10% per decade that Rajeevan et al. (2008) give for the Goswami analysis. Our 1-degree boxes are means of the newer 0.25-degree product, not the original 1-degree IMD grid. Thus the absolute counts are different from Goswami's counts.

For 1951-2025, the quasi-AIC values for 1-degree heavy events were: stationary 86.3, trend 69.2, trend plus step at 1976 70.9, and step alone 74.1. In the trend-plus-step model, the step was not significant (+12%, p = 0.52) and the trend was significant (+11% per decade, p < 0.001). The best single break year was 1970 (1-degree heavy) and 1984 (0.25-degree heavy).

All numbers are in `files/results/results.json`. The season table is `files/results/central_india_jjas_counts.csv`.

## Figures

- `figures/fig1_timeseries_forecasts.png`: 1-degree counts with the 1951-2000 fits and the 2001-2025 forecasts.
- `figures/fig2_forecast_skill.png`: change in 2001-2025 MSE against the stationary forecast, for all six series.
- `figures/fig3_threshold_sensitivity.png`: period means against the threshold at both scales. The 1-degree values at 200 and 250 mm use very few events.
- `figures/fig4_change_maps.png`: change in mean heavy days per 1-degree box between periods.
- `figures/fig5_network_proxy.png`: the network proxy and the 1-degree/0.25-degree count ratio.
- `figures/fig6_persiann_check.png`: PERSIANN-CDR against IMD for 1983-2025.

## Limitations

- This study uses one gridded product. The IMD station data and the daily station counts are not public in the current files, so we could not repeat the Lin and Huybers interpolation test for 2001-2025.
- The network proxy is indirect. Real changes in the size of rain systems also change the number of local extrema. Thus the proxy can show too little or too much of the network effect.
- The 2001-2025 result depends on a few seasons. Seasons are not fully independent, and the season bootstrap does not include year-to-year correlation.
- We did not test the cause of 2005-2007 or the role of sea-surface temperature or moisture transport.
- The IMD record for recent years (especially 2025) can change in later releases. Our hashes identify the files that we used.
- PERSIANN-CDR has a step in daily extremes near 1998. Thus we have no independent extreme-rain record for the full period.

## Reproduce

```
bash files/code/run_all.sh /path/to/scratch
```

This downloads about 1.9 GB of IMD data and about 6.6 GB of PERSIANN-CDR data (the script keeps only India cut-outs) into the scratch folder, then runs all steps. It needs Python 3.12 with numpy, pandas, statsmodels (0.15), netCDF4 and matplotlib, and curl. The IMD downloads take about 1 minute per year. The publication folder receives no raw data.

## Provenance

- Campaign job: sci-1107-dell-earth-and-ocean-sciences-984c01b64f41; topic earth-and-ocean-sciences; machine dell; account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated researcher. The signing key is a campaign-machine key. It does not claim personal authorship.
- Date of the analysis: 2026-11-09.
- External data terms and attribution: see `files/EXTERNAL_DATA_NOTICE.md`.
