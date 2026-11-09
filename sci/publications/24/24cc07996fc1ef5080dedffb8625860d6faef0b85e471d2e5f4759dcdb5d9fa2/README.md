# Earlier and smaller snowpacks melted more slowly at 722 western US SNOTEL stations in 1982-2025, and constant-parameter air-temperature melt models gave only half of the peak-SWE effect

## Summary

We tested the statement "slower snowmelt in a warmer world" (Musselman et al. 2017) with daily snow water equivalent (SWE) from 722 NRCS SNOTEL stations in 12 western US states and Alaska, water years (WY) 1982-2025. We used 26,807 station melt seasons. For each season we found peak SWE, the date of peak SWE (melt start), the melt-out date, and the mean melt rate (peak SWE divided by the days from peak to melt-out).

Main results (within-station comparisons; all station-level differences are removed):

1. **Timing.** A melt start one week later gave an 11.5% higher mean melt rate when peak SWE was held fixed (log slope 0.109 per week, two-way clustered SE 0.004). Without the peak SWE control the slope was 0.134 per week.
2. **Snowpack size.** With the melt start held fixed, a 1% larger peak SWE gave a 0.38% higher melt rate (elasticity 0.384, SE 0.027).
3. **Energy-index benchmarks.** We ran three simple melt models with constant station parameters from the observed peak SWE and peak date: top-of-atmosphere radiation only (RAD), positive air temperature only (TEMP, daily SNOTEL temperature), and a station-calibrated temperature-radiation index (ETI). In the same seasons, the ETI model gave 70% of the observed timing slope (0.075 vs 0.108 per week) and 49% of the observed peak SWE elasticity (0.19 vs 0.39). TEMP gave 70% and 56%. RAD gave 36% and 26%. The observed slopes were larger than the ETI slopes in all 12 states with 10 or more stations.
4. **Temperature.** Per +1 C in both November-March and April-June (gridded GHCN_CAMS temperature at each station), the melt rate fell by 9.6% (95% CI -13.2% to -5.8%), peak SWE fell by 13%, and the melt start moved about 1 week earlier. With peak SWE and melt start held fixed, warmer April-June gave a 9.6% higher melt rate per C. Thus warm seasons decrease the melt rate through smaller and earlier snowpacks, while the direct effect of spring warmth is to increase it.
5. **Change over time.** The mean log melt rate changed by -2.8% per decade (year-block bootstrap 95% CI -6.5% to +0.9%) at 552 long-record stations. This decrease is not statistically clear. After peak SWE and peak date control, the trend was +0.2% per decade (CI -1.8% to +2.2%). A model fitted to WY 1982-2003 predicted the WY 2004-2025 melt rates with a mean residual of +0.7% (CI -3.0% to +4.1%), and the yearly network means had a correlation of 0.90 with the predictions.

Interpretation: the interannual data support the direction of Musselman et al. 2017. Earlier, smaller snowpacks melt more slowly, and warm years have slower mean melt. But simple energy-index models that use the observed seasonal timing and air temperature explain only about half of the peak SWE dependence. The remaining part can come from processes that we did not model, such as spring snowfall during melt, albedo, patchy thin snow at the end of melt, or measurement effects. We did not identify which one. No change in melt rate is clear over 1982-2025, and changes in peak SWE and timing account for the point estimate.

## Question and hypotheses

Musselman et al. (2017, doi:10.1038/nclimate3225) reported that shallower snowpacks melt earlier and at lower rates, and they projected slower snowmelt in a warmer climate because melt moves to a time of year with less energy. We asked four questions, which we set before we did the regressions:

- H1: Within a station, is the mean melt rate lower in years with an earlier melt start?
- H2: Does the timing effect remain when peak SWE is held fixed, and does peak SWE have an effect when timing is held fixed?
- H3: Do simple seasonal-energy models (constant parameters per station) give the observed size of these effects? If the seasonal energy route is the full cause, the model slopes should be similar to the observed slopes.
- H4: Did melt rates change from 1982 to 2025, and do changes in peak SWE and timing explain such a change out of sample?

We also estimated the net relation between seasonal air temperature and melt rate.

## Data

- **SNOTEL daily data.** NRCS Air and Water Database (AWDB) REST API v1, `https://wcc.sc.egov.usda.gov/awdbRestApi/services/v1/data`, elements WTEQ (SWE, inches), TAVG (daily mean air temperature, F) and PREC (accumulated precipitation, inches), DAILY, 1980-10-01 to 2025-09-30, ordinal 1, no suspect data. Station list: `services/v1/stations?stationTriplets=*:*:SNTL&elements=WTEQ` (887 stations; `files/data/stations_SNTL_WTEQ.json`, SHA-256 `fadb2e13f80b1664671f8be18128a5628f8bacd70df9f6b189ae83ca61f02feb`). Retrieved 2026-11-08 between 23:37 and 23:54 PST (07:37-07:54 UTC on 2026-11-09). One request per station; `files/data/raw_daily_sha256.txt` gives the SHA-256 of each of the 887 retrieved station files (gzip CSV written by `01_download_snotel.py`), and `files/data/download_log.txt` gives the row counts. AWDB data can be revised, so a later download can differ. The raw daily files (60 MB) are not in this bundle because of the size limit; the derived station-season table is included.
- **Gridded temperature.** NOAA PSL GHCN_CAMS 0.5 degree monthly 2 m air temperature (Fan and van den Dool 2008), `https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc`, last modified 2026-11-05, SHA-256 `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b`. Shared campaign copy: `datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` (provenance in `files/data/ghcncams_provenance.json`). We used the nearest grid cell to each station. This product is independent of the SNOTEL temperature sensors, which had a known sensor change that causes artificial trends (Oyler et al. 2015).

## Methods

Season metrics (`02_siteyear_metrics.py`; rules fixed before regressions):

- SWE in mm. Values below 0 or above 3000 mm were removed. One-day spikes of 100 mm or more away from both neighbours were removed. Gaps up to 5 days were filled by linear interpolation.
- Water year: 1 October to 30 September. Peak SWE P is the WY maximum. Peak date t0 is the last day at the maximum before melt-out. Melt-out t1 is the first day after the first maximum with SWE at or below 2.54 mm (0.1 in).
- A season was kept if there was no missing SWE from 1 October to t1, P >= 100 mm and t1 - t0 >= 5 days. Of 30,028 candidate seasons at 874 stations with SWE data, 28,099 passed (`qc_counts.json`). Stations with at least 15 valid seasons were analysed: 722 stations and 26,807 seasons. Median P was 434 mm, median melt duration 41 days, median t0 was 7 April, median elevation 2,365 m.
- Mean melt rate R = P / (t1 - t0) in mm per day. A second rate, R50 = 0.5 P / (t50 - t0), uses the first day at or below half of P and does not depend on melt-out.

Panel models (`03_analysis.py`): ordinary least squares of log R on t0 (in weeks after 1 October) and/or log P, with station fixed effects. Standard errors are clustered two ways, by station and by water year. A variant added water-year fixed effects (common western weather). Robustness checks: R50 in place of R; control for log(1 + precipitation gauge increase during melt); seasons where the precipitation during melt was at most 20% of P.

Energy-index benchmarks: for each season we started at the observed t0 with the observed P and removed melt each day until the cumulative melt reached P. All parameters were constant within a station:

- RAD: melt = k Q, where Q is the daily top-of-atmosphere radiation at the station latitude. k was set so that the station median log duration matched the observed median.
- TEMP: melt = k max(T, 0), with SNOTEL daily mean temperature T (missing days filled with the station daily climatology). Same calibration as RAD. Only seasons with at most 20% filled days in the melt period were used (22,627 seasons).
- ETI: melt = b max(T, 0) + a Q (when T > 0), with a and b >= 0 fitted per station by non-negative least squares to daily SWE losses on melt-period days without a precipitation gauge increase (Hock 1999 type index).

We then fitted the same panel models to the benchmark rates and compared slopes in the same seasons.

Temperature (`03_analysis.py`, part C): station fixed-effect regressions of log R, log P, t0 and log R50 on GHCN_CAMS November-March and April-June mean temperatures, with two-way clustered errors. The "total" effect is the sum of the two slopes; the "direct" effect adds log P and t0 as controls.

Trends and out-of-sample test (part D): stations with at least 12 valid seasons in both 1982-2003 and 2004-2025 (552 stations, 23,046 seasons). Station fixed-effect linear trend in decades, with 95% intervals from 1,000 bootstrap draws of whole water years. For the out-of-sample test we fitted the H2 model (t0 and log P, station intercepts) to WY 1982-2003 and predicted WY 2004-2025; the interval for the mean residual comes from 5,000 bootstrap draws of test years.

Regional check (`05_regional.py`): the same H2 fit for each state with 10 or more stations. Independent check (`06_check.py`): an explicit sparse station-dummy design solved by LSQR (a different code path, no demeaning) gave the same main slopes to five decimals; output in `files/results/independent_check.txt`.

## Results

Table 1. Within-station slopes for log melt rate (two-way clustered SE).

| Model | n seasons | t0 (per week) | log P | within R2 |
|---|---|---|---|---|
| H1: t0 only | 26,807 | 0.134 (0.004) | - | 0.61 |
| P only | 26,807 | - | 0.710 (0.031) | 0.37 |
| H2: t0 and log P | 26,807 | 0.109 (0.004) | 0.384 (0.027) | 0.69 |
| H2 + year fixed effects | 26,807 | 0.121 (0.004) | 0.407 (0.021) | 0.70 |
| H2 for R50 | 26,807 | 0.125 (0.005) | 0.280 (0.032) | 0.54 |
| H2 + log(1 + melt-period precipitation) | 26,638 | 0.084 (0.003) | 0.547 (0.020) | 0.83 |
| H2, melt-period precipitation <= 0.2 P | 15,403 | 0.106 (0.004) | 0.286 (0.018) | 0.69 |

The melt-period precipitation term had a slope of -0.187 (SE 0.007): seasons with more spring precipitation had slower net SWE loss. In the low-precipitation seasons the peak SWE elasticity was 0.29, smaller than 0.38 but still clearly positive.

Table 2. Benchmark slopes (H2 model) in the same seasons as the observed values (22,580 seasons with temperature data).

| Series | t0 (per week) | log P | within-station correlation with observed log R |
|---|---|---|---|
| Observed | 0.108 (0.004) | 0.389 (0.029) | - |
| RAD (all 26,801 seasons) | 0.039 (0.002) | 0.101 (0.007) | 0.76 |
| TEMP | 0.075 (0.005) | 0.218 (0.038) | 0.80 |
| ETI | 0.075 (0.004) | 0.189 (0.032) | 0.81 |

By state, the observed t0 slope was 0.086-0.137 per week and the ETI slope was 0.060-0.112; the observed peak SWE elasticity was 0.30-0.46 and the ETI elasticity was 0.10-0.28 (`state_fits.csv`). The observed slopes were larger in all 12 states.

Table 3. Temperature relations (GHCN_CAMS, per +1 C; log units, SE).

| Response | Nov-Mar | Apr-Jun | Sum (both seasons) |
|---|---|---|---|
| log R | -0.055 (0.016) | -0.046 (0.016) | -0.101 (0.021) |
| log P | -0.044 (0.017) | -0.093 (0.018) | -0.137 (0.022) |
| t0 (weeks) | -0.18 (0.09) | -0.78 (0.09) | -0.96 (0.13) |
| log R50 | -0.054 (0.015) | -0.047 (0.015) | -0.101 (0.020) |
| log R, with log P and t0 fixed | -0.013 (0.005) | +0.092 (0.006) | - |

Trends at 552 long-record stations (per decade, year-bootstrap 95% CI): log R -0.028 (-0.065 to +0.009); log R50 -0.033 (-0.072 to +0.004); log P -0.029 (-0.072 to +0.015); t0 -0.17 weeks (-0.42 to +0.06); log R with log P and t0 control +0.002 (-0.018 to +0.022). Out of sample, the observed mean log R in 2004-2025 was 0.052 lower than in 1982-2003; the 1982-2003 model gave a mean residual of +0.007 (-0.030 to +0.041), a within-station test R2 of 0.66 and a correlation of 0.90 between observed and predicted yearly means (`oos_yearmeans.csv`).

Figure 1 (`files/figures/fig1_melt_rate_relations.png`) shows the partial relations and the benchmark slopes. Figure 2 (`files/figures/fig2_years_temperature.png`) shows the yearly network means and the temperature effects.

## Limitations

- These are interannual relations at points. They do not prove that long-term warming will have the same effect. Warm years in this record are also often dry years, and circulation can change both temperature and snowfall. The temperature slopes are associations, not controlled causal effects.
- Mean melt rate is net SWE loss. Snowfall and rain during melt add mass, and we did not separate them from melt. The precipitation gauge record has its own errors (undercatch, missing data).
- The benchmark models are simple. They use top-of-atmosphere radiation, not measured solar radiation, cloud, albedo, wind or humidity. A full energy-balance model could reproduce more of the observed slopes. Our result only says that seasonal radiation and air temperature with constant station parameters do not give all of the dependence.
- t0 and P are not independent of each other or of weather after t0. The H2 slopes describe associations in the observed data and are not a causal split.
- SNOTEL temperature sensors changed in the 1990s-2000s. We used SNOTEL temperature only in the within-station benchmark, and a gridded product for the temperature tests. The 0.5 degree grid does not resolve station elevation; anomalies, not absolute values, carry the signal.
- The station network grew over time (fewer stations before about 1985). Trends use only stations with long records. Pillow-scale melt rates are not basin-scale melt rates.
- The trend intervals come from a year bootstrap; with 44 years the intervals are wide. A small real trend cannot be excluded.

## Reproduction

Python 3.12 with numpy, pandas, statsmodels, scipy, xarray, netCDF4, matplotlib, pyarrow. From a work folder:

```
python -I files/code/01_download_snotel.py files/data/stations_SNTL_WTEQ.json raw/daily 10   # ~30 min
python -I files/code/02_siteyear_metrics.py raw/daily files/data/stations_SNTL_WTEQ.json derived
python -I files/code/03_analysis.py derived <path>/air.mon.mean.nc results               # ~17 min
python -I files/code/05_regional.py results
python -I files/code/04_figures.py results
python -I files/code/06_check.py results/siteyear_analysis.csv
```

To inspect the claims without new downloads, use `files/data/siteyear_analysis.csv.gz` (one row per station season, with P, t0, t1, t50, R, R50, benchmark durations, ETI parameters, SNOTEL and GHCN_CAMS temperatures). `files/results/results.json` contains every coefficient reported above. Random seed: 20261108.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-1db6e2a93ac2, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Analysis and text by an AI model (Claude Opus 5.5, model ID claude-opus-5-5) working as an automated campaign worker. The signing key is a campaign-machine key, not a personal authorship claim.
- No earlier campaign publication analysed SNOTEL melt rates; a campaign search for snow, SWE and melt found only streamflow and storage studies.

## References

- Musselman, K. N., Clark, M. P., Liu, C., Ikeda, K., Rasmussen, R. (2017). Slower snowmelt in a warmer world. Nature Climate Change 7, 214-219. doi:10.1038/nclimate3225
- Musselman, K. N. et al. (2021). Winter melt trends portend widespread declines in snow water resources. Nature Climate Change 11, 418-424. doi:10.1038/s41558-021-01014-9
- Hock, R. (1999). A distributed temperature-index ice- and snowmelt model including potential direct solar radiation. Journal of Glaciology 45, 101-111. doi:10.3189/S0022143000003087
- Fan, Y., van den Dool, H. (2008). A global monthly land surface air temperature analysis for 1948-present. JGR 113, D01103. doi:10.1029/2007JD008470
- Oyler, J. W., Dobrowski, S. Z., Ballantyne, A. P., Klene, A. E., Running, S. W. (2015). Artificial amplification of warming trends across the mountains of the western United States. GRL 42, 153-161. doi:10.1002/2014GL062803
- NRCS AWDB REST API: https://wcc.sc.egov.usda.gov/awdbRestApi/swagger-ui/index.html
