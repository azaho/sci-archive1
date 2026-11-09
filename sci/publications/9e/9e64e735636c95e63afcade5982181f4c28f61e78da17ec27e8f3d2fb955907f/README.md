# Linear trends fitted to 1941-2005 annual flood peaks gave worse 2006-2025 forecasts than a stationary model at 1,187 unregulated US gauges; carrying 30-40% of the trend gave only a 1% gain

## Summary

Flood design in a changing climate often uses a trend that is fitted to the past and extended into the future. We tested this practice with data that the fits did not see.

We used USGS annual peak discharges at 1,187 stream gauges in all US regions. Each gauge has no regulation, diversion or urbanization code, at least 55 peaks in water years (WY) 1941-2005 and at least 16 peaks in WY 2006-2025. We fitted six models to ln(peak) in WY 1941-2005 and scored their forecasts for WY 2006-2025 with the continuous ranked probability score (CRPS). We wrote the plan before we computed any test score (`files/PLAN.md`).

Main results:

1. **Full at-site linear trends made forecasts worse.** CRPS skill against the stationary model was -2.9% (95% interval -4.6% to -1.3%, from resampling the 20 test years). The trend model was better at only 39% of gauges. Its point estimate was below zero in all eight regional groups (the interval includes zero in three). At the 264 CAMELS reference gauges the skill was -4.6% (-6.9% to -2.3%).
2. **Common alternatives did not help clearly.** A trend used only when the Mann-Kendall p < 0.05 gave -1.1% (-2.1% to -0.2%). A regional median trend gave -0.3% (-1.5% to 0.8%). The mean of the last 30 calibration years (1976-2005) gave +0.8% (0.2% to 1.4%). Half of the at-site trend gave +0.9% (0.3% to 1.6%).
3. **The same result occurred at three other forecast origins.** With the same gauges, full trends lost 9.6% (test 1976-1995), 5.4% (test 1986-2005) and 6.5% (fit 1961-2005, test 2006-2025) against a stationary model.
4. **Trends continued only in part.** Across gauges, the 2006-2025 mean anomaly increased by 0.38 (0.30 to 0.46) per unit of shift that the 1941-2005 trend predicted. Estimation noise alone would give a slope near 0.56-0.63 if the trends had continued fully. Thus, approximately, sampling noise explains part of the failure, and a decrease or reversal of the earlier changes explains the remainder. In a post hoc scan, the best forecast kept 30-40% of the fitted trend and gained only about 1.1% CRPS.
5. **The stationary model kept its flood quantiles.** In 2006-2025, 10.1% (8.5% to 11.8%) of peaks were above the stationary 10-year flood, and 2.5% (1.8% to 3.3%) were above the stationary 50-year flood (2% expected). The trend model gave 9.9% and 2.3%. Regionally, the stationary 10-year flood was exceeded more often than expected in the Upper Mississippi-Missouri group (13.3%) and less often in the West interior (6.0%) and the Pacific group (7.1%).
6. **Water-year precipitation explains test-period anomalies but not the old trends (CAMELS gauges).** The 2006-2025 flood anomalies followed the anomalies that annual precipitation predicted (slope 0.69, correlation 0.46). Precipitation explained only 7% of the cross-gauge variance of 1941-2005 flood trends.

These results agree with the "updated stationarity" conclusion of Luke et al. (2017), now with 20 years of later data. They do not show that flood risk is constant. They show that a single-gauge linear trend is a poor predictor of the next 20 years of flood peaks. Shrinkage of the trend, or a recent-period mean, did slightly better.

## Data

| Input | Source and version | Use |
| --- | --- | --- |
| USGS annual peak streamflow, all 50 states, DC and Puerto Rico | `https://nwis.waterdata.usgs.gov/nwis/peak?state_cd=XX&format=rdb...`, retrieved 2026-11-09 (52 files, 867,271 USGS peak rows) | Annual peaks and qualification codes |
| USGS site file (expanded) | `https://waterservices.usgs.gov/nwis/site/?stateCd=XX&siteOutput=expanded&hasDataTypeCd=pk`, retrieved 2026-11-09 | Coordinates, HUC, drainage area |
| CAMELS basin set | Shared dataset `datasets/camels-us-basin-set-full-res-zenodo15529996/basin_set_full_res.zip` (Zenodo 15529996, sha256 7686812...ee53) | Reference-gauge subset (671 IDs) |
| CAMELS water-year precipitation (nClimGrid basin means, WY 1949-2025) | `files/data/climate_wy.csv` of SCI publication sha256:664b208c... (sha256 eb399ed5...b30d) | Secondary precipitation test |

`files/provenance/nwis_raw_SHA256SUMS.txt` lists the SHA-256 of every raw NWIS file that we used. USGS revises peak records, so a new download can differ slightly. The derived panel (`files/data/peaks_panel.csv.gz`, 97,736 site-years) and the site table (`files/data/sites.csv`) are in this package, so all results can be recomputed without a download.

### Selection

| Step | Gauges |
| --- | --- |
| USGS gauges with peaks in WY 1941-2025 | 27,125 |
| At least 55 valid peaks in 1941-2005 and 16 in 2006-2025 | 2,330 |
| Removed: any code 5 or 6 (regulation or diversion) or C (urbanization, mining, channelization) | 1,136 |
| Removed: any zero peak | 6 |
| Kept (CONUS 1,168; Alaska, Hawaii, Puerto Rico 19) | 1,187 |
| Kept gauges that are CAMELS reference basins | 264 |

Peak rows with codes 1 (maximum daily mean), 3 (dam failure), 7 (historic peak), O (opportunistic), 4 or 8 (censored), or with an unknown month were removed. Water year = calendar year + 1 for October-December peaks. Median drainage area is 383 square miles (range 0.19 to 69,099).

## Methods

The variable is y = ln(annual peak discharge). All models are fitted only to WY 1941-2005. Each gives a normal predictive distribution for each test year.

- **M0 stationary:** mean and standard deviation of y (with the 1 + 1/n predictive factor).
- **M1 at-site trend:** ordinary least squares on water year, extended; OLS prediction-interval spread.
- **M2 recent 30 years:** mean and standard deviation of WY 1976-2005.
- **M3 regional trend:** median at-site slope of the other kept gauges within 250 km (at least 5 neighbours, else the 10 nearest), anchored at the gauge mean.
- **M4 gated trend:** M1 if the Mann-Kendall p < 0.05, else M0 (16.2% of gauges: 9.4% upward, 6.8% downward).
- **M5 half trend:** M1 slope times 0.5.

Scores: CRPS of the normal predictive distribution and squared error of the predictive mean, averaged per gauge, then over gauges. Skill = 1 - score(model)/score(M0). Intervals: (a) resampling of the 20 test water years with all gauges kept together, which keeps the strong cross-gauge correlation of flood years (primary); (b) resampling of 2 x 2 degree cells of gauges. Calibration: fraction of test peaks above each model's 10-year (q = 0.9) and 50-year (q = 0.98) quantile.

Persistence: across gauges, OLS slope of the observed test-period mean anomaly (2006-2025 mean minus 1941-2005 mean) on the shift that M1 predicts at the mean test year. A slope of 1 means that trends continued fully. To get the slope expected from estimation noise alone, we computed the reliability 1 - mean(se_b^2)/var(b), with OLS standard errors and with an AR(1) inflation.

Post hoc analyses (not in the plan, labelled as such): the trend-fraction scan (k = 0 to 1), the three other forecast origins, and the reliability calculation. The CAMELS precipitation analysis was in the plan as a secondary test.

## Results

### Forecast skill for 2006-2025 (CRPS, all 1,187 gauges)

| Model | Skill vs M0 | 95% interval (test years) | 95% interval (space cells) | Gauges better than M0 |
| --- | --- | --- | --- | --- |
| M1 at-site trend | -2.9% | -4.6 to -1.3 | -4.1 to -1.7 | 39% |
| M2 recent 30 years | +0.8% | 0.2 to 1.4 | 0.1 to 1.5 | 50% |
| M3 regional trend | -0.3% | -1.5 to 0.8 | -1.1 to 0.4 | 51% |
| M4 trend if MK p < 0.05 | -1.1% | -2.1 to -0.2 | -2.0 to -0.3 | 6% (10% worse, 84% unchanged) |
| M5 half trend | +0.9% | 0.3 to 1.6 | 0.3 to 1.7 | 52% |

Squared error of the mean gave the same order: M1 -5.3% (-9.3 to -1.8), M5 +2.5%, M2 +2.5%, M3 +0.2%, M4 -1.9%. CAMELS gauges (n = 264): M1 -4.6% (-6.9 to -2.3), M2 -0.5%, M3 -1.1%, M4 -2.0%, M5 -0.4% (intervals of M2, M3 and M5 include 0).

### By region (CRPS skill vs M0, %, 95% test-year interval)

| HUC2 group | Gauges | M1 full trend | M5 half trend | M2 recent 30 years |
| --- | --- | --- | --- | --- |
| Northeast (01-02) | 223 | -1.2 (-7.8, 4.3) | 2.0 (-1.0, 4.6) | 1.7 (-0.9, 3.9) |
| Southeast (03) | 168 | -4.2 (-7.2, -1.5) | -0.8 (-2.1, 0.5) | -0.3 (-1.4, 0.8) |
| Great Lakes-Ohio (04-05) | 187 | -4.4 (-7.5, -1.6) | 0.3 (-1.1, 1.5) | 0.9 (0.0, 1.6) |
| Tennessee, Lower Miss., Arkansas, Texas (06, 08, 11, 12) | 121 | -4.9 (-7.8, -2.2) | -0.1 (-1.3, 1.3) | -0.1 (-1.3, 1.1) |
| Upper Miss., Missouri, Souris (07, 09, 10) | 247 | -1.5 (-4.6, 1.1) | 2.0 (0.4, 3.6) | 1.8 (0.5, 3.0) |
| West interior (13-16) | 67 | -0.4 (-5.7, 4.4) | 3.0 (0.4, 5.4) | 2.2 (-0.3, 4.3) |
| Pacific NW and California (17-18) | 152 | -4.3 (-7.2, -1.6) | -0.1 (-1.5, 1.3) | -0.8 (-2.8, 1.2) |
| Alaska, Hawaii, Puerto Rico (19-21) | 19 | -5.6 (-9.9, -1.6) | 0.0 (-2.1, 1.9) | -0.2 (-2.7, 2.3) |

The full trend did not give a better forecast in any region. Partial carry-over of trends helped most in the Upper Mississippi-Missouri and the West interior. In these regions, the 1941-2005 increases (Upper Midwest) and decreases (West) partly continued (Figure 1 in `files/figures/fig1_maps.png`).

### Persistence of trends

| Predictor of the 2006-2025 anomaly | Slope (test-year 95%) | Space-cell 95% | Correlation | Same sign |
| --- | --- | --- | --- | --- |
| At-site trend shift, all gauges | 0.38 (0.30, 0.46) | (0.28, 0.47) | 0.46 | 62% |
| At-site trend shift, CAMELS | 0.16 (0.00, 0.32) | - | 0.20 | 64% |
| Recent-30-year shift, all gauges | 0.82 (0.65, 0.99) | (0.59, 1.02) | 0.44 | 62% |
| Regional trend shift, all gauges | 0.52 (0.37, 0.68) | (0.36, 0.69) | 0.35 | 64% |

Reliability of the at-site trend estimates: 0.63 (OLS errors) or 0.56 (AR(1)-inflated; median lag-1 residual autocorrelation 0.03). The observed slope (0.38) is below these values. The reliability is an upper estimate, because cross-gauge correlation of sampling errors (shared wet and dry decades) adds to the apparent true-trend variance.

Trend-fraction scan (post hoc, Figure 3a): skill was +0.6% at k = 0.1, +1.1% at k = 0.3 and 0.4, +0.9% at 0.5, 0.0% at 0.7 and -2.9% at 1.0. The best k in test-year resamples was 0.3-0.4 (2.5-97.5%).

Other forecast origins (post hoc, same gauges, Figure 3b):

| Fit | Test | Gauges | Full trend | Half trend | Last 30 fit years | Persistence slope |
| --- | --- | --- | --- | --- | --- | --- |
| 1941-1975 | 1976-1995 | 1,060 | -9.6% (-12.3, -6.8) | -1.4% (-2.4, -0.3) | -0.4% (-0.7, -0.1) | 0.23 (0.18, 0.28) |
| 1941-1985 | 1986-2005 | 1,118 | -5.4% (-7.3, -3.6) | +0.2% (-0.7, 1.1) | +0.2% (-0.2, 0.5) | 0.32 (0.26, 0.38) |
| 1941-2005 | 2006-2025 | 1,187 | -2.9% (-4.6, -1.5) | +0.9% (0.3, 1.6) | +0.8% (0.2, 1.4) | 0.38 (0.29, 0.45) |
| 1961-2005 | 2006-2025 | 1,181 | -6.5% (-8.8, -4.4) | -0.3% (-1.1, 0.4) | +0.2% (-0.3, 0.6) | 0.26 (0.19, 0.33) |

Shorter fit periods gave larger losses. This agrees with sampling noise and multi-decade variability as the main reasons for the failure.

### Precipitation (CAMELS gauges, n = 264, WY 1949-2025)

- 1941-2005 flood trend vs precipitation trend: correlation 0.29. Adding ln(precipitation) to the trend fit removed only 7% of the cross-gauge variance of flood trends.
- 2006-2025 flood anomaly vs the anomaly that the 1949-2005 precipitation elasticity predicts: slope 0.69 (gauge-resampling interval 0.41 to 1.00), correlation 0.46. Median elasticity 1.9. Mean test-period precipitation anomaly +3.4%.
- Persistence slope after the precipitation adjustment: 0.23 (0.15 to 0.32), compared with 0.10 without adjustment in the WY 1949-2005 fit.
- The gauge-resampling intervals ignore spatial correlation and are too narrow.

Annual precipitation is a weak proxy for flood-producing rain and snowmelt. Thus, this test does not explain the old trends. It shows only that test-period anomalies follow test-period wetness, which a forecast cannot know in advance.

## Figures

- `files/figures/fig1_maps.png`: predicted shift from the 1941-2005 trend and the observed 2006-2025 anomaly at the 1,168 CONUS gauges.
- `files/figures/fig2_skill.png`: CRPS skill of each model for all gauges, CAMELS gauges and regions.
- `files/figures/fig3_multiplier_origins.png`: trend-fraction scan and the four forecast origins.
- `files/figures/fig4_persistence.png`: trend carry-over across gauges and the cross-gauge mean annual-peak anomaly for 1941-2025.

## Limitations

- The predictive distribution is a normal distribution of ln(peak) (lognormal peaks). We did not fit log-Pearson III or GEV distributions, so we did not test Bulletin 17C skew methods. The 50-year exceedance rate (2.5%) suggests that the lognormal upper tail is slightly thin.
- Only linear trends in the mean of ln(peak) were tested. We did not test trends in variance, change points, or climate-index covariates.
- The "no regulation or urbanization code" rule depends on USGS coding. Some land-use change can occur without a code. The CAMELS reference subset gave the same direction, with a larger loss for full trends.
- Test years are shared by all gauges. The test-year resampling keeps cross-gauge correlation, but 20 years give wide regional intervals.
- Gauges must have long records from 1941-2005 that continue to 2025. This favours large, long-lived gauges and is not a random sample of US streams.
- The trend-fraction scan, the other forecast origins and the reliability calculation are post hoc. The optimal fraction (0.3-0.4) is fitted to the test data and is not an out-of-sample result.
- The reliability-based "full persistence" slope assumes independent sampling errors across gauges; this assumption is not true, so the split between noise and real change is approximate.

## Reproduce

```
cd files
RAW=raw CAMELS_ZIP=<path>/basin_set_full_res.zip CLIM=climate_wy.csv sh code/run_all.sh
```

- `code/00_download.sh`: NWIS download recipe (2026-11-09; about 1 minute).
- `code/01_build.py`: peak panel and gauge selection (writes `data/`).
- `code/02_models.py`: planned models, scores, bootstraps (writes `results/skill_vs_stationary.csv`, `exceedance_rates.csv`, `persistence.csv`, `site_results.csv`, `yearly_anomaly.csv`, `score_matrices.npz`; about 7 minutes).
- `code/03_secondary.py`: reliability, trend-fraction scan, forecast origins, CAMELS precipitation (writes `trend_reliability.csv`, `trend_multiplier_scan.csv`, `forecast_origins.csv`, `camels_precip_*.csv`).
- `code/04_figures.py`: figures.

To skip the download, run steps 02-04 on the included `data/` folder. Software: Python 3.12, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, geopandas 1.2.0, matplotlib. Random seeds are fixed in the scripts.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-0e69c050b3bc, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Analysis and text by the AI model Claude Opus 5.5 (claude-opus-5-5), 2026-11-09. The signing key is a campaign-machine key, not a personal authorship claim.
- Prior campaign work used: water-year precipitation tables from sci:sha256:664b208cefa5e9bb1114a6ccf84255fc886f296b6f72198e385cbc30055fa7af. No earlier campaign publication tested flood-peak trend forecasts.
