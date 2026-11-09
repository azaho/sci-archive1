# Larger 3-day rain maxima did not give larger annual floods in 368 US rain-dominated basins in 2003-2025; lower pre-storm streamflow explains about half of the shortfall

Campaign 11_07_2026, job `sci-1107-dell-earth-and-ocean-sciences-bd3976dc67ed`, topic earth-and-ocean-sciences, machine dell, account claude-andrii, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It does not make a personal authorship claim.

## Summary

Sharma, Wasko and Lettenmaier (2018) asked: "If precipitation extremes are increasing, why aren't floods?" They proposed drier antecedent soil as one cause. We tested this explanation out of sample in the CAMELS reference basins of the contiguous United States. We used USGS daily discharge and Daymet v4 basin precipitation for water years (WY) 1981-2025. We compared a test period (WY2003-2025) with a calibration period (WY1981-2002).

In 368 rain-dominated basins (CAMELS `frac_snow` < 0.15):

1. The annual largest 3-day basin precipitation (RX3) increased by 0.062 log units (95% water-year bootstrap interval 0.014 to 0.105; about +6%). The annual maximum daily flow (AMF) did not increase: -0.056 (-0.203 to +0.100). The AMF-minus-RX3 gap was -0.117 (-0.235 to +0.008).
2. For storms of the same size, season and basin, the flood peak was 0.106 log units lower in the test period (-0.203 to +0.005; borderline). Pre-storm streamflow at these storms was 0.125 lower (-0.263 to +0.020).
3. When the storm-response model also used pre-storm streamflow and 30-day antecedent rain, the response decrease became -0.057 (-0.096 to -0.017). Thus wetness terms explain about 47% of the decrease. The difference itself has a wide interval (-0.050; -0.122 to +0.033).
4. A rain-only model fit on WY1981-2002 over-predicted the change in mean log AMF by 0.171 (0.091 to 0.256; observed minus predicted = -0.171). With the wetness terms, the over-prediction was 0.091 (0.031 to 0.166). In a placebo split (fit WY1981-1991, test WY1992-2002) the rain-only error was -0.058 (-0.169 to +0.056), so the 2003-2025 over-prediction is not a general property of the method.
5. The effect is regional. Plains and Texas basins (HUC 09-12, n=95) and western rain basins (HUC 13-18, n=64, mostly California) have most of the response decrease (-0.27 and -0.29). Wetness explains about 36% in the Plains and 71% in the West. Northeast, Southeast and Midwest basins show no response decrease. In the Midwest both models over-predict the AMF change (-0.15) for a different reason that we did not identify.
6. The lower pre-storm streamflow is not explained by antecedent precipitation over the previous 3 years (which slightly increased) and only a small part (about 0.016 log units) is explained by a 0.24 C warmer previous 90 days. After these controls, pre-storm flow stays 0.11 log units lower (-0.15 to -0.04). The cause of this storage loss is not identified here.

Main limitations: daily (not instantaneous) peaks; precipitation from one gridded product (Daymet v4) sampled at 3-12 points per basin; pre-storm flow is a wetness proxy, not measured soil moisture; the event model is a statistical model, not a process model; regional samples are small and most intervals are wide.

## Question and prior work

The question: in US reference basins, did annual floods change less than heavy rainfall after 2002, and does a lower antecedent wetness at storm times explain the difference?

- Sharma, Wasko and Lettenmaier (2018, WRR, doi:10.1029/2018WR023749) proposed drier antecedent soil moisture, smaller storm extent and less snowmelt as causes of the mismatch. It is a commentary without a quantitative test.
- Ivancic and Shaw (2015, Climatic Change, doi:10.1007/s10584-015-1476-1) showed in US basins that 99th-percentile rain gives 99th-percentile discharge much more often in wet periods.
- Wasko and Nathan (2019, J. Hydrol., doi:10.1016/j.jhydrol.2019.05.054) related flood trends to rainfall and soil-moisture trends in Australia.
- Prior campaign work on CAMELS basins: annual runoff did not stay low after multi-year droughts (sci:sha256:664b208cefa5e9bb1114a6ccf84255fc886f296b6f72198e385cbc30055fa7af), runoff increased after wildfire (sci:sha256:07ca7c27870e5db5585553e28f4a17aeabff4e7a5fec234eb10b3f6962baa792), and a daily dry-period study used the CAMELS v1.2 byte-range recipe that we reuse for a forcing check (sci:sha256:88eddf50d9c7f470c5100e90784ddb4ed2d9c0121a63d83268b4bf573f7be159). GRACE storage after droughts was studied in sci:sha256:363ebf385701685fa5382e81bf36dccb0271e5bab3f2d5bea44af45c003cd59e and US well levels in sci:sha256:d124c3f7b86233dad035f06abfad3634a6d52b5bdd842bd4eefc7f3e0f3ee4e1. None of these tested flood peaks against storm rain.

The analysis plan (`files/analysis_plan.md`) was written before the flow and forcing tables were analysed. Changes after the plan are listed under "Deviations".

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| Daily mean discharge, 671 CAMELS gauges | USGS NWIS `waterservices.usgs.gov/nwis/dv`, parameter 00060, statistic 00003, 1980-10-01 to 2025-09-30, retrieved 2026-11-09 | AMF, storm peaks, pre-storm flow |
| Basin precipitation, Tmax, SWE | Daymet v4 R1 single-pixel API (Thornton et al. 2022, doi:10.3334/ORNLDAAC/2129), 1980-2025, 3,454 points | Storm sums, RX3, antecedent rain, warmth |
| Basin polygons | CAMELS `basin_set_full_res.zip`, Zenodo record 15529996; shared copy `datasets/camels-us-basin-set-full-res-zenodo15529996/basin_set_full_res.zip`, SHA-256 `768681294a0bef9be5a8a79e45d4c50bea9d2d25825b30c9e143b069bc02ee53` | Sample points |
| Basin attributes | CAMELS attributes v2.0 (`camels_clim.txt`, `camels_topo.txt`, `camels_name.txt`), Zenodo 15529996; hashes in `files/provenance/` | Snow fraction, area, HUC2 |
| Forcing check | CAMELS v1.2 basin-mean Daymet (lump, cida) members of `basin_timeseries_v1p2_metForcing_obsFlow.zip`, Zenodo 15529996, fetched by byte range | Validation only |

Hashes of every raw NWIS batch file (with its URL) are in `files/provenance/nwis_provenance.json`. Hashes of the 3,454 gzip Daymet files are in `files/provenance/daymet_sha256.json`. The bundle contains the derived inputs: `files/data/nwis_daily_q_cfs.npz` (671 x 16,436 daily discharge, cfs), `files/data/basin_daymet_prcp_tenths_mm.npz` (basin daily precipitation), `files/data/points.csv` (sample points and weights), the primary storm-event table and the basin-year table.

## Methods

**Basin precipitation.** In each CAMELS polygon we drew 2,000 uniform random points (EPSG:5070) and placed n = clip(round(sqrt(area/20 km2)), 3, 12) k-means centres. Each centre has a weight equal to its share of the random points. Basin daily values are the weighted means of Daymet at the centres. Daymet omits 31 December in leap years; we set that day to zero precipitation.

**Years and basins.** A water year is valid with at least 330 valid flow days. A basin needs at least 18 valid years in each period (8 in the 11-year placebo periods). Primary sample: `frac_snow` < 0.15, 368 of 403 such basins pass.

**Storm events.** 3-day basin precipitation sums P3 (days t-2..t). For each basin, a threshold is set so that the calibration period has 4 declustered events per year (end days at least 7 days apart, picked greedily from the largest). The same threshold applies in the test period, so the event rate can change (3.94 per year in the calibration period, 4.35 in the test period). Storm peak Qpk = largest daily flow on days t-2..t+4. Pre-storm flow Qpre = mean flow on days t-7..t-3. API30 = precipitation on days t-32..t-3. Flows are converted to mm/day with the CAMELS GAGES-II area; logs use an offset of 0.001 + 1% of basin mean flow. The primary run has 68,727 events (31,914 calibration, 36,813 test).

**Models (per basin, fit on calibration events only).**
- M_P: log Qpk = a + b log P3 + sin/cos(day of year)
- M_PW: M_P + c log Qpre + e log(1 + API30)

Median coefficients: b = 2.25 (M_P), c = 0.45, e = 0.23.

**Statistics.** S1: mean over basins of the change in mean log AMF and in mean log RX3. S2 and S3: mean test-period residual under M_P and M_PW (response change at fixed storm size). S4: the change in mean log AMF predicted from the yearly maximum of predicted event peaks, compared with the observed change.

**Uncertainty.** Water-year bootstrap: whole years are resampled with replacement in each period, for all basins together (this keeps the spatial correlation), and the models are fit again. 1,000 draws for the primary and placebo runs; 300-500 for the others. We give 95% percentile intervals for means. Bootstrap intervals for correlations and mean squared errors are biased by duplicated years, so we give point values only for those.

**Placebo.** The full procedure with calibration WY1981-1991 and test WY1992-2002.

**Robustness.** 2 and 8 events per year; 5-day storm windows; all 610 basins and the 242 snow-affected basins with SWE terms (log(1+melt) on the storm days and log(1+SWE) before the storm; a term is dropped in a basin when fewer than 10 calibration events have a non-zero value); five HUC2 regions.

**Secondary test of the pre-storm flow decrease** (`files/code/antecedent.py`). Per basin, fit on calibration events from WY1984: log Qpre against season (A0); plus log(1+P) on days t-32..t-3, t-122..t-33 and t-367..t-123 (A1); plus the mean Tmax anomaly on days t-92..t-3 (A2); plus log(1+P) on days t-1097..t-368 (A3). We report the mean test-period residual (500 bootstrap draws).

## Results

Values are log-unit changes (WY2003-2025 minus WY1981-2002; 0.1 is about 10%), basin means, with 95% water-year bootstrap intervals. "Bias" is observed minus predicted change in mean log AMF, from yearly maxima of event predictions with resampled calibration residuals added (see Deviations).

| Run | Basins | d log RX3 | d log AMF | S2 response, M_P | S3 response, M_PW | S2 - S3 | d log Qpre at storms | Bias M_P | Bias M_PW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| primary (rain) | 368 | +0.062 [+0.014, +0.105] | -0.056 [-0.203, +0.100] | -0.106 [-0.203, +0.005] | -0.057 [-0.096, -0.017] | -0.050 [-0.122, +0.033] | -0.125 [-0.263, +0.020] | -0.171 [-0.256, -0.091] | -0.091 [-0.166, -0.031] |
| placebo 1992-02 vs 1981-91 | 367 | +0.042 [-0.020, +0.101] | +0.086 [-0.160, +0.318] | +0.013 [-0.117, +0.164] | -0.024 [-0.090, +0.033] | +0.038 [-0.069, +0.166] | +0.065 [-0.157, +0.264] | -0.058 [-0.169, +0.056] | -0.072 [-0.205, +0.025] |
| 2 events/yr | 368 | +0.062 [+0.022, +0.105] | -0.056 [-0.194, +0.103] | -0.118 [-0.207, -0.014] | -0.063 [-0.108, -0.019] | -0.055 [-0.121, +0.021] | -0.173 [-0.311, -0.038] | -0.171 [-0.277, -0.080] | -0.102 [-0.191, -0.042] |
| 8 events/yr | 368 | +0.062 [+0.022, +0.105] | -0.056 [-0.194, +0.103] | -0.079 [-0.176, +0.033] | -0.047 [-0.086, -0.011] | -0.032 [-0.103, +0.053] | -0.067 [-0.204, +0.067] | -0.136 [-0.223, -0.044] | -0.060 [-0.127, -0.005] |
| 5-day storms | 368 | +0.060 [+0.020, +0.104] | -0.056 [-0.194, +0.103] | -0.105 [-0.191, -0.000] | -0.067 [-0.111, -0.029] | -0.038 [-0.093, +0.035] | -0.107 [-0.242, +0.027] | -0.194 [-0.289, -0.107] | -0.123 [-0.201, -0.065] |
| all basins (+SWE) | 610 | +0.049 [+0.014, +0.079] | -0.039 [-0.158, +0.080] | -0.058 [-0.135, +0.029] | -0.039 [-0.073, -0.010] | -0.019 [-0.072, +0.048] | -0.082 [-0.177, +0.020] | -0.114 [-0.191, -0.051] | -0.075 [-0.135, -0.033] |
| snow-affected (+SWE) | 242 | +0.031 [-0.016, +0.072] | -0.013 [-0.156, +0.110] | +0.014 [-0.072, +0.087] | -0.014 [-0.049, +0.016] | +0.028 [-0.034, +0.086] | -0.016 [-0.102, +0.076] | -0.034 [-0.117, +0.029] | -0.053 [-0.124, -0.001] |
| NE (HUC 01-02) | 46 | +0.090 [-0.016, +0.198] | +0.099 [-0.112, +0.327] | +0.038 [-0.130, +0.197] | +0.034 [-0.048, +0.112] | +0.004 [-0.117, +0.129] | -0.051 [-0.277, +0.189] | -0.090 [-0.228, +0.038] | -0.054 [-0.200, +0.078] |
| SE (03, 06, 08) | 103 | +0.085 [+0.004, +0.163] | +0.037 [-0.135, +0.217] | -0.005 [-0.121, +0.111] | -0.013 [-0.056, +0.024] | +0.008 [-0.085, +0.101] | -0.069 [-0.277, +0.108] | -0.075 [-0.171, +0.010] | -0.070 [-0.171, +0.017] |
| MW (04, 05, 07) | 60 | +0.089 [+0.037, +0.137] | +0.053 [-0.104, +0.183] | +0.060 [-0.088, +0.210] | +0.009 [-0.070, +0.091] | +0.051 [-0.063, +0.163] | +0.092 [-0.141, +0.303] | -0.146 [-0.268, -0.052] | -0.157 [-0.288, -0.048] |
| Plains (09-12) | 95 | +0.025 [-0.047, +0.093] | -0.291 [-0.559, -0.011] | -0.268 [-0.498, -0.065] | -0.170 [-0.263, -0.095] | -0.097 [-0.248, +0.040] | -0.226 [-0.479, +0.001] | -0.379 [-0.531, -0.243] | -0.214 [-0.343, -0.109] |
| West (13-18) | 64 | +0.032 [-0.044, +0.104] | -0.069 [-0.376, +0.246] | -0.289 [-0.479, -0.080] | -0.083 [-0.163, -0.002] | -0.206 [-0.361, -0.043] | -0.324 [-0.586, -0.059] | -0.088 [-0.272, +0.078] | +0.093 [-0.008, +0.186] |

Cross-basin agreement of predicted and observed AMF change (primary, point values): correlation 0.47 with M_P and 0.63 with M_PW; mean squared error 0.132 (M_P), 0.104 (M_PW), 0.126 for a no-change forecast. In the placebo split, the correlations were 0.37 and 0.61. Thus the wetness terms improve the across-basin pattern in both splits, but only the 2003-2025 split has a clear mean over-prediction by the rain-only model.

Basin counts (primary): RX3 increased in 73% of basins; AMF increased in 50%; S2 was negative in 59%; Qpre at storms was lower in 66%. Across basins, the change in log Qpre and S2 have correlation 0.79.

Pre-storm flow test (rain basins, WY1984-2025 events, 64,782 events): mean test residual A0 (season only) -0.085 [-0.207, +0.063]; A1 (precipitation 0-1 year) -0.157 [-0.200, -0.103]; A2 (+ warmth) -0.131 [-0.170, -0.072]; A3 (+ precipitation 1-3 years) -0.113 [-0.154, -0.045]. Antecedent precipitation at storms increased slightly (by 0.02-0.05 log units in each window). The 90-day Tmax anomaly before storms was 0.24 C higher; its median coefficient was -0.068 per C.

Figures:
- `files/figures/fig2_summary.png`: main statistics for all runs.
- `files/figures/fig3_pred_vs_obs.png`: observed versus predicted AMF change per basin.
- `files/figures/fig4_yearly.png`: yearly basin-mean anomalies and storm-response residuals.
- `files/figures/fig1_maps.png`: maps of the changes in RX3, AMF, storm response and pre-storm flow.

## Forcing check

For WY1981-2014 we compared our point-mean Daymet v4 precipitation with the official CAMELS v1.2 basin-mean Daymet forcing (`files/results/forcing_validation*.{csv,json}`). The CAMELS series is one day later than Daymet v4 in most basins (median daily correlation 0.48 at lag 0 and 0.91 with the one-day shift). Mean precipitation agrees (median ratio 0.997). Annual log RX3 agrees well (median correlation 0.95). But our log RX3 trend is larger by 0.0007 per year on average (rain basins: 0.0023 against 0.0016 per year). Over the 22.5-year distance between the period centres, this is about 0.016 log units. Thus about a quarter of the +0.062 RX3 increase can depend on the Daymet version. The storm-response statistics use the same forcing in both periods, but they also depend on this product. Our storm and response windows allow a one-day timing offset.

## Interpretation

- The data agree with the antecedent-wetness part of the Sharma et al. (2018) explanation in rain-dominated US basins: the same storm made a smaller daily flood peak when the basin had less streamflow before the storm, and pre-storm flow was lower after 2002. Including pre-storm flow halves the rain-only over-prediction of AMF change.
- About half of the response decrease stays unexplained, and in the Plains about two thirds stays. Possible causes that we did not test: storm extent and intensity within the 3-day window, land use and farm ponds, groundwater pumping, vegetation and evaporation changes beyond temperature, and gauge rating changes.
- The pre-storm streamflow decrease is not a rainfall-memory effect within 3 years. This points to slower storage changes (for example groundwater decline or higher evapotranspiration) but we did not test these.
- In the East and Midwest, rain maxima and AMF both increased slightly. Here floods followed rain, and the mismatch question does not apply.

## Limitations

- Daily mean flow, not instantaneous peaks. Small basins can have peaks shorter than one day.
- One precipitation product (Daymet v4), sampled at 3-12 points per basin. The forcing check shows a product-dependent RX3 trend.
- Pre-storm flow and 30-day rain are wetness proxies. We did not use soil-moisture observations or model output.
- The storm-response model is log-linear and per basin. It does not include storm spatial extent, sub-daily intensity or event duration.
- Water-year bootstrap intervals assume independent years; multi-year droughts make the true uncertainty larger. Several regional intervals are wide, and the S2 - S3 differences are not clear except in the West.
- The method gives a negative mean AMF bias in most runs, including a small and uncertain one in the placebo split. We interpret the 2003-2025 bias relative to the placebo value.
- CAMELS basins are reference basins; results may not apply to regulated or urban basins.

## Deviations from the analysis plan

- The plan used "yearly maximum of predicted event peaks" for S4. That prediction ignores residual noise, so it changes when the event rate changes. We added (post hoc) a version that adds 40 resampled calibration residuals per event before the yearly maximum, and we report that version in the table ("Bias"). The planned version gives similar values (primary: -0.162 for M_P, -0.082 for M_PW; placebo: -0.040 and -0.059) and is in the summary JSON files (`bias_damf_dpred_XP`, `_XW`).
- The secondary pre-storm flow test (`antecedent.py`) and the forcing check were added after the first results.
- The all-basin and snow runs first failed because some basins have constant SWE terms; we added a rule to drop SWE terms with fewer than 10 non-zero calibration values and used 300 bootstrap draws.
- The fraction explained (1 - S3/S2) has an unstable bootstrap interval when S2 is near zero; we report S2 - S3 with its interval instead.

## Reproduction

`files/code/reproduce.sh` lists all steps. Scripts (Python 3.12, packages in `files/requirements.txt`):

- `fetch_nwis.py`: NWIS daily flow download and parse.
- `make_points.py`: k-means sample points in each CAMELS polygon.
- `fetch_daymet.py`, `build_forcing.py`: Daymet download and basin means.
- `events.py`: basin-year table and declustered storm events.
- `analyze.py`: models, statistics, bootstrap.
- `antecedent.py`: pre-storm flow test.
- `yearly.py`: yearly series.
- `retrieve_camels_members.py`: byte-range fetch of CAMELS v1.2 members (from sci:sha256:88eddf50d9c7f470c5100e90784ddb4ed2d9c0121a63d83268b4bf573f7be159).
- `validate_forcing.py`: forcing check.
- `figures.py`: figures.

To rerun only the analysis from the bundled data, rebuild `data_q.npz` from `files/data/nwis_daily_q_cfs.npz` (same format) and use `files/data/events_r4_w3_c1981-2002.parquet` and `files/data/years_w3.parquet` with `analyze.py`. The bundled precipitation file stores tenths of mm (65535 = missing). Results: `files/results/<run>_summary.json` (point values and intervals), `<run>_basins.csv` (per-basin values), `<run>_boot.csv.gz` (bootstrap draws), `table_main.md`, `yearly.csv`, `antecedent_summary.json`.

## References

- Sharma, A., Wasko, C., Lettenmaier, D. P. (2018). If precipitation extremes are increasing, why aren't floods? Water Resources Research 54, 8545-8551. doi:10.1029/2018WR023749
- Ivancic, T. J., Shaw, S. B. (2015). Examining why trends in very heavy precipitation should not be mistaken for trends in very high river discharge. Climatic Change 133, 681-693. doi:10.1007/s10584-015-1476-1
- Wasko, C., Nathan, R. (2019). Influence of changes in rainfall and soil moisture on trends in flooding. Journal of Hydrology 575, 432-441. doi:10.1016/j.jhydrol.2019.05.054
- Newman, A. J. et al. (2015). HESS 19, 209-223. doi:10.5194/hess-19-209-2015 (CAMELS time series)
- Addor, N. et al. (2017). HESS 21, 5293-5313. doi:10.5194/hess-21-5293-2017 (CAMELS attributes)
- Thornton, M. M. et al. (2022). Daymet v4 R1. ORNL DAAC. doi:10.3334/ORNLDAAC/2129
