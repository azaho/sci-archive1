# High water above the annual mean had no network trend at 173 UHSLC tide gauges in 1980-2021, but local trends exceeded chance and did not extrapolate

## Summary

Coastal flood risk depends on two parts of the water level: the mean sea level (MSL) and the height of high water above that mean. We tested whether the second part changed at long-record tide gauges. We used the UHSLC/JASL Research Quality hourly data set. The sample was 173 stations and 6,528 station-years in 1980-2021.

For each station-year, we fitted the astronomical tide by least squares. Our primary metric was the 99th percentile of hourly sea level above the annual mean (P99). We divided P99 change into an astronomical tide part and a non-tidal part. We then divided the non-tidal part into a slow part (30-day running mean) and a fast part (the remainder).

Main results:

1. **No network trend.** The median station trend of P99 was +0.17 mm per decade (95% bootstrap interval -0.62 to +1.16). This is well inside the joint-year permutation null for the median (-1.69 to +1.54). On average, high water followed the annual mean.
2. **More local trends than chance.** 35 of 173 stations had |t| > 1.96 (22 positive, 13 negative). The joint-year block-permutation null gave a mean of 11.7 and a 95th percentile of 22 (p = 0.004).
3. **Small relative to MSL.** At 165 stations with one continuous datum, the median absolute P99 trend was 0.11 times the median absolute relative MSL trend. The median relative MSL trend was +27.8 mm per decade. At 45 stations, |P99 trend| was more than 25% of |MSL trend|; 20 of these 45 also had |t| > 1.96.
4. **Trends did not extrapolate.** We fitted models on 1980-2009 and tested them on 2010-2021. A linear trend added to the mean and nodal model increased the median station mean absolute error (MAE) by a factor of 1.062 (95% interval 1.033-1.089). The trend model was better at only 29% of stations. This was also true for P99.9, annual maxima, tide P99, non-tidal P99, skew surge, and the slow and fast parts (all median ratios > 1).
5. **Tide versus non-tidal part (H2): not robust.** Across stations, tide P99 trends explained more of the P99 trend variance (R² = 0.59) than non-tidal P99 trends (R² = 0.32). But five stations with very large tide trends (Churchill, Balboa, Wyndham, Geting, Cuxhaven) caused this difference. Without them, R² was 0.32 (tide) and 0.36 (non-tidal). Rank correlations were also equal (0.57 and 0.57).
6. **Exploratory: US Atlantic and Gulf coasts.** At 28 stations, the median P99 trend was +5.9 mm per decade (joint-year permutation p = 0.007; 11 stations significant and all positive, null 95th percentile 6). The slow non-tidal part had the largest change (+10.7 mm per decade, p = 0.004). The tide part did not cause it (-1.0 mm per decade). Extrapolation of the 1980-2009 trend also failed here (MAE ratio 1.10, interval 1.02-1.27). Thus the change came late and was not a steady trend.
7. **Exploratory: the fast non-tidal part decreased outside that region.** At the other 145 stations, the fast-part P99 trend was -2.3 mm per decade (p = 0.003) and skew-surge P95 was -2.2 mm per decade (p = 0.016). The fast-part standard deviation decreased at 35 stations and increased at 4 (median -0.8% per decade). The decrease was larger in the tropics and at large-tide stations. Instrument and timing changes can also cause this pattern, so the cause is not known.

Figures: `files/figures/fig1_map_obs_p99_trend.png` (map), `fig2_decomposition.png`, `fig3_forecast_mae_ratio.png`, `fig4_msl_vs_extreme.png`, `fig5_examples.png`, `fig6_regions.png`.

## Question and hypotheses

Do extreme high water levels change only with the mean sea level, or does the height of high water above the mean also change? If it changes, is the cause the astronomical tide or the non-tidal (weather and ocean) part? Can a past trend predict later years?

Prior studies found that changes in extreme sea levels mostly follow MSL (Menéndez and Woodworth 2010; Marcos and Woodworth 2017). Tides changed at some sites (Haigh et al. 2020). In Europe, storm-surge extremes changed at rates near the rate of sea-level rise (Calafat et al. 2022). We tested these ideas with a global hourly data set, a joint-year permutation null, and an out-of-sample test.

We wrote the plan (`files/notes/analysis_plan.md`) before we calculated trend or forecast results:

- H1 (primary): The network median P99 trend is within ±2 mm per decade of zero, and the number of stations with |t| > 1.96 does not exceed the 95th percentile of the permutation null.
- H2: Across stations, tide P99 trends explain more of the P99 trend variance than non-tidal P99 trends.
- H3: For 2010-2021, a model with a 1980-2009 linear trend does not have a lower median MAE than the same model without the trend.

Outcome: H1 part 1 was supported and H1 part 2 was rejected. H2 was supported only when five high-leverage stations were included. H3 was supported.

We added the slow and fast split, the regions and the fast-part analysis after we saw the first results. The plan amendment records this. These results are exploratory.

## Data

- **UHSLC / JASL Research Quality Data Set, hourly**, all 719 station records (netCDF), downloaded 2026-11-09 from `https://uhslc.soest.hawaii.edu/data/netcdf/rqds/global/hourly/`. Dataset citation: Caldwell, P. C., Merrifield, M. A., Thompson, P. R., Sea level measured by tide gauges from global oceans — the Joint Archive for Sea Level holdings (NCEI Accession 0019568), NOAA NCEI, doi:10.7289/V5V40S7W. NCEI lists the data under CC BY 4.0 (some parts CC0 1.0). The SHA-256 of each file is in `files/provenance/uhslc_sha256_20261109.txt`. We did not include the raw hourly files.
- **Natural Earth 110 m land** (public domain), only for the map outline. SHA-256 in `files/provenance/natural_earth_sha256.txt`.

The Research Quality data have a delay. The number of stations with complete years drops after 2021 (273 stations in 2017, 107 in 2022, at least 80% valid hours). Thus we stopped at 2021.

## Method

**Station-years.** For each UHSLC station number and calendar year, we used the record version with the most valid hours. A version is a segment that has no common datum with other segments. All metrics are relative to the annual mean, so datum differences between versions have no effect. We accepted a year if it had at least 80% valid hours and at least 10 months with at least 70% valid hours.

**Tide fit.** For each accepted year, we fitted by ordinary least squares: a constant; 31 astronomical constituents (2Q1, SIG1, Q1, RHO1, O1, M1, P1, K1, J1, OO1, 2N2, MU2, N2, NU2, M2, LDA2, L2, T2, S2, K2, MO3, M3, MK3, MN4, M4, MS4, S4, 2MN6, M6, 2MS6, M8); and 5 long-period terms (Sa, Ssa, Mm, Msf, Mf). The long-period terms are not part of the tide. A fit for each year includes the nodal modulation of that year. It also includes any real change in tidal constants.

**Metrics (mm, relative to the annual mean of valid hours).**
- `obs_p99` (primary): 99th percentile of observed hourly values. `obs_p999` and `obs_max` are secondary.
- `tide_p99`: 99th percentile of the fitted tide at all hours of the year.
- `ntr_p99`: 99th percentile of the non-tidal residual (observed minus mean minus tide).
- `skew_p95`: 95th percentile of skew surges. A skew surge is the observed maximum within ±3 h of a predicted high water, minus the predicted high water.
- `slow_p99` and `fast_p99`: 99th percentiles of the 30-day centred running mean of the residual, and of the residual minus that mean.

**Station selection.** At least 30 accepted years in 1980-2021, at least 18 in 1980-2009, and at least 8 in 2010-2021. Result: 173 stations (median 39 years).

**Trends.** For each station and metric, we used OLS of the annual values on a constant, the year, and cosine and sine terms for 18.61 years (nodal cycle) and 4.43 years (half the lunar perigee cycle). We increased the standard error by sqrt((1+r)/(1-r)), where r ≥ 0 is the lag-1 autocorrelation of the residuals.

**Permutation null.** For each station, we kept the fitted mean, nodal and perigee part. We then permuted the residuals in 3-year blocks of calendar years. We used the same permutation for all stations, which keeps the spatial correlation between stations. Each station keeps its missing years. We used 500 permutations for the network tests and 1,000 for the regional tests.

**Out-of-sample test.** For training years 1980-2009 and test years 2010-2021, we compared three models: (a) mean + nodal + perigee; (b) (a) + linear trend; (c) (a) + the 2000-2009 mean residual. We report the median of the station MAE ratios with a bootstrap interval over stations.

**MSL comparison.** Relative MSL trend from the annual means of the most common version at each station (at least 25 years). The same regression as above.

## Results

### Network trends, 1980-2021 (173 stations, mm per decade)

| Metric | Median trend | 95% interval | Positive / negative with \|t\|>1.96 | Null 95th pct. of count | p (count) | p (median) |
|---|---|---|---|---|---|---|
| obs_p99 (primary) | +0.17 | -0.62, +1.16 | 22 / 13 | 22 | 0.004 | 0.85 |
| tide_p99 | +0.09 | -0.54, +0.65 | 34 / 31 | 37 | 0.002 | 0.78 |
| ntr_p99 | -1.57 | -3.21, +0.09 | 10 / 17 | 19 | 0.002 | 0.12 |
| skew_p95 | -1.16 | -2.23, -0.37 | 10 / 19 | 17 | 0.004 | 0.14 |
| slow_p99 (exploratory) | +0.29 | -1.24, +1.94 | 14 / 9 | 18 | 0.012 | 0.72 |
| fast_p99 (exploratory) | -1.90 | -2.47, -0.97 | 5 / 18 | 21 | 0.034 | 0.002 |
| obs_p999 | -0.51 | -3.16, +1.34 | 12 / 10 | - | - | - |
| obs_max | +0.77 | -4.42, +3.12 | 8 / 11 | - | - | - |

For skew surge, the bootstrap interval of the median does not include zero. But the joint-year permutation test does not reject zero (p = 0.14), because of correlated years. We use the permutation result.

### Out-of-sample test, 2010-2021 (173 stations)

| Metric | Median MAE ratio, trend / no trend | 95% interval | Stations where trend was better |
|---|---|---|---|
| obs_p99 | 1.062 | 1.033-1.089 | 29% |
| obs_p999 | 1.051 | 1.023-1.079 | 31% |
| obs_max | 1.035 | 1.006-1.070 | 38% |
| tide_p99 | 1.053 | 1.000-1.114 | 43% |
| ntr_p99 | 1.042 | 1.014-1.090 | 39% |
| skew_p95 | 1.026 | 1.002-1.044 | 40% |
| slow_p99 | 1.036 | 1.013-1.074 | 36% |
| fast_p99 | 1.025 | 1.014-1.062 | 38% |

Model (c), with the recent residual mean, gave a ratio of 1.000 (0.999-1.012) for obs_p99. The median MAE of the model without a trend was 22 mm for obs_p99.

### Regions (exploratory; regions were chosen after the first results)

| Region | n | obs_p99 | tide_p99 | slow_p99 | fast_p99 | skew_p95 | MSL |
|---|---|---|---|---|---|---|---|
| US Atlantic and Gulf coasts | 28 | +5.87 | -1.00 | +10.65 | +5.58 | +4.54 | +45.7 |
| Australia | 16 | -2.58 | -0.69 | +2.51 | +2.26 | +0.49 | +36.7 |
| Tropical Pacific islands | 21 | +0.18 | +1.37 | -4.75 | -2.01 | -3.17 | +32.0 |
| East and Southeast Asia | 33 | -0.95 | +0.37 | +0.72 | -0.93 | -0.99 | +32.9 |
| Other US and Canada (Pacific coast, Alaska, Hawaii, Canada) | 41 | -0.47 | -0.27 | -0.60 | -4.61 | -2.66 | +5.6 |
| Other | 34 | -0.27 | +0.30 | -3.77 | -1.66 | -1.43 | +20.7 |

Values are median station trends in mm per decade. For the US Atlantic and Gulf group, the joint-year permutation p-values of the median were 0.007 (obs_p99), 0.008 (tide_p99), 0.004 (slow_p99), 0.078 (fast_p99) and 0.048 (skew_p95). In the test years, the model without a trend underpredicted obs_p99 there by a median 9.9 mm. Previous studies reported that MSL rose quickly on the US Southeast coast after about 2010 ("hot spots", Valle-Levinson et al. 2017), and a campaign publication reported a 2010-2022 sea-level surge at US Gulf coast gauges (sci:sha256:ef81e5f0a9c865853fb85e9fd8c68bb249266923b1b7d861d191d6eda1865040). Our slow part is relative to the annual mean, so it shows more variability within the year, not that rise itself. Wilmington (on the Cape Fear River) also has its largest slow-part values in hurricane years (2018, 1999, 1998, 1996) (Fig. 5).

## Interpretation

On average, at these gauges, high water rose with the mean sea level. Changes in the height of high water above the mean were about one tenth as large as MSL changes. At some stations the changes were real and larger than chance. Their causes were different: tide changes at large-tide sites, slow variability on the US Atlantic and Gulf coasts, and decreases of the fast part at some other sites. These changes did not continue as linear trends. A flood-frequency estimate that adds a fitted trend in high water above the mean to the MSL projection made 2010-2021 errors larger at most stations in this test.

## Limitations

- The station network is not uniform. It has many US, Japanese, Australian and Pacific island stations and few stations in Europe, Africa and South America. It does not show European surge trends (Calafat et al. 2022) well.
- The data end in 2021 because of the Research Quality delay.
- Our tide fit uses one year of data and 31 constituents. It does not include shallow-water constituents beyond these, or seasonal changes of tidal constants. At large-tide and river sites, some tide-surge interaction and timing errors go into the non-tidal part.
- The 30-day split between the slow and fast parts is a choice. The fast part includes residual tide energy (for example internal tides at Honolulu) and also instrument noise.
- The decrease of the fast part may come from changes of instruments or sampling (for example, filtered versus instantaneous hourly values). We did not have instrument histories, so we cannot separate this from a real decrease in storm activity.
- Percentile metrics relative to the annual mean do not show changes in the number of flood days, which depend mainly on MSL.
- The regional analysis and the slow and fast split are post hoc. Other region boundaries can give different numbers.
- Some stations have short gaps or a gap at one end. For example, Cuxhaven has no accepted years from 1987 to 1997, and its negative trend depends on the early 1980s.

## Reproduction

1. `bash files/code/00_fetch.sh /path/to/scratch` downloads the 719 UHSLC files and the Natural Earth outline into a scratch folder and compares the hashes with `files/provenance/`. The archive is updated about twice a year, so new downloads can differ.
2. `export UHSLC_RAW=/path/to/scratch/nc NE_LAND=/path/to/scratch/ne_110m_land.zip`
3. `bash files/code/run_all.sh` (Python 3.12; numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, xarray 2026.9.0, netCDF4 1.7.5, matplotlib 3.11.2, geopandas 1.2.0). Run time is about 1 hour on 8 cores. The random seed is fixed (20261109).

Files:
- `files/code/01_inventory.py`: valid hours for each record and year.
- `files/code/02_station_years.py`: tide fit and metrics for each station-year.
- `files/code/03_analysis.py`: trends, permutation null, H2, MSL comparison, out-of-sample test (`derived/results.json`).
- `files/code/05_exploratory_fast.py`, `06_regions.py`, `07_region_tests.py`, `08_h2_robust.py`: exploratory analyses.
- `files/code/04_figures.py`: figures.
- `files/derived/station_year_metrics.csv`: all station-years (219 screened stations); `station_year_metrics_selected.csv`: the 173 selected stations; `station_trends.csv`: trends for each station; `forecast_station.csv`: out-of-sample errors.
- `files/notes/analysis_plan.md`: the plan written before the results, with the later amendment.

## Provenance

- Campaign 11_07_2026, job sci-1107-hp-earth-and-ocean-sciences-f8d598ddb2b6, topic earth-and-ocean-sciences, machine hp, account claude-andrii.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal claim of authorship.
- External data terms and attribution: see `files/NOTICE-external-data.md`.

## References

- Caldwell, Merrifield and Thompson. UHSLC/JASL holdings, NOAA NCEI. doi:10.7289/V5V40S7W
- Menéndez and Woodworth (2010). Changes in extreme high water levels based on a quasi-global tide-gauge data set. JGR. doi:10.1029/2009JC005997
- Marcos and Woodworth (2017). Spatiotemporal changes in extreme sea levels along the coasts of the North Atlantic and the Gulf of Mexico. JGR Oceans. doi:10.1002/2017JC013065
- Haigh et al. (2020). The tides they are a-changin'. Reviews of Geophysics. doi:10.1029/2018RG000636
- Calafat et al. (2022). Trends in Europe storm surge extremes match the rate of sea-level rise. Nature. doi:10.1038/s41586-022-04426-5
- Valle-Levinson et al. (2017). Spatial and temporal variability of sea level rise hot spots over the eastern United States. GRL. doi:10.1002/2017GL073926
