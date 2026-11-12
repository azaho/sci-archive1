# A melt-energy threshold on days above 0 C gave most of the missing melt-start and peak-SWE effects on SNOTEL melt rates in 1988-2025; cloud, humidity and wind anomalies added little

## Summary

An earlier campaign publication (sci:sha256:24cc07996fc1ef5080dedffb8625860d6faef0b85e471d2e5f4759dcdb5d9fa2) showed this with 722 SNOTEL stations: snowpacks with an earlier peak date or a smaller peak snow water equivalent (SWE) melt more slowly. A calibrated temperature-radiation index model gave only 70% of the melt-start (timing) slope and 49% of the peak-SWE elasticity. The earlier work did not find the cause of the missing part. We tested candidate causes with daily NASA POWER meteorology (all-sky and clear-sky shortwave, longwave, humidity and wind) at each station. We used the same SNOTEL seasons and the same panel models.

Main results (22,098 melt seasons at 721 stations, water years (WY) 1988-2025; all models have constant parameters for each station):

1. **Replication.** We downloaded the SNOTEL data again and got the same 26,807 seasons as the earlier work. Peak SWE, peak date and melt-out date agreed for all seasons. The earlier temperature + top-of-atmosphere (TOA) radiation model gave 70% of the observed melt-start slope and 49% of the observed peak-SWE elasticity again.
2. **Measured weather alone did not close the gap.** Daily all-sky shortwave in place of TOA radiation gave 69% and 51%. A snow-age albedo term increased this to 70% and 56%. Wind, humidity (vapour pressure) and sensible-heat terms increased it to 73% and 59%.
3. **A constant energy threshold closed most of the gap.** We added one constant (negative) energy term on days with a mean air temperature above 0 C. The TOA model then gave 108% of the melt-start slope (station-bootstrap 95% CI 106-110%) and 86% of the peak-SWE elasticity (84-89%). The model with the station daily climatology of all-sky shortwave and a threshold gave 103% and 84%. Parameters fitted on the other half of the years gave the same shares (108%/85% and 103%/83%). The threshold model gave a higher within-station correlation with the observed log melt rate (0.892, against 0.825 without a threshold).
4. **A temperature threshold did not do this.** A degree-day model with a fitted base temperature gave only 58% and 42%. The threshold must act on an energy supply that increases through spring (radiation), not on air temperature alone.
5. **Daily weather anomalies added little after the threshold.** With the seasonal threshold model, we added the daily shortwave anomaly, snow-age albedo, humidity, wind, sensible heat and the daily longwave anomaly. The shares stayed at 100% and 86%, and the within-station correlation increased only from 0.892 to 0.905.
6. **The result was consistent.** In all 12 states with 10 or more stations, the threshold model gave 74-106% of the observed peak-SWE elasticity and 97-122% of the observed melt-start slope. Without the threshold, the ranges were 27-76% and 50-84%. The result did not change with year fixed effects (105% and 87%), in seasons with little precipitation during melt (109% and 94%), or in Alaska (106% and 90%).
7. **A small part remains.** The peak-SWE elasticity of the residual (observed minus threshold model) log rate was 0.054 (SE 0.019), which is 14% of the observed value. At 70% of stations, the model elasticity was below the observed elasticity. More snowfall days in the melt window gave slower observed melt than the model.

Interpretation: the "slower snowmelt" relation is mainly a seasonal energy effect, as Musselman et al. (2017) proposed. But the melt energy is the radiation supply minus an approximately constant loss. The median fitted threshold is 24-32 mm w.e. per day, which is approximately 90-120 W m-2. This is near the typical net longwave loss of a melting snow surface, with some additional energy for the nightly cold content. With this threshold, the energy that is available for melt increases much faster in relative terms through spring than the radiation supply (Figure 3). Thus an earlier start or a smaller snowpack (which melts out earlier) gets a much smaller part of the seasonal energy. Linear index models without such a loss term give approximately half of this effect. Our data do not show that clouds, humidity, wind or albedo cause the missing half. The coarse POWER grid (0.5-1 degree) limits this negative result (see Limitations).

## Question and hypotheses

The earlier work (sci:24cc0799) listed possible causes of the missing part of the slopes: spring snowfall, albedo, thin patchy snow at the end of melt, and measurement effects. It also noted that its models used no measured radiation. Before we ran the models, we wrote this plan (files/ANALYSIS_PLAN.md):

- H-cloud: daily all-sky shortwave (clouds) in place of TOA radiation reproduces the slopes.
- H-albedo: snow-age albedo decay (fresh snow from SWE or gauge increases) reproduces them.
- H-humidity (Harpold and Brooks 2018): drier air in small-snowpack years (more energy lost to sublimation and evaporation) reproduces them. Wind and sensible-heat terms are part of this test.
- H-longwave: daily incoming longwave reproduces them.

The planned models were ETI_TOA, ETI_SW, ETI_ALB, ETI_HUM and ETI_LW. The ETI_LW model gave 89% and 72%. Its longwave term is (LW - 27.27 MJ m-2 d-1), the emission of a 0 C surface, so it contains a large negative constant. To separate this constant from the longwave variation, we added control models after the first run: a free constant on days above 0 C (threshold models), longwave climatology only, and longwave anomaly only. These controls were not in the written plan. We report them as post hoc tests. Split-year parameters, state-level fits and an independent mean-group estimator test them.

## Data

- **SNOTEL daily data** (USDA NRCS Air and Water Database REST API v1, `https://wcc.sc.egov.usda.gov/awdbRestApi/services/v1/data`). Elements WTEQ, TAVG and PREC, daily, 1980-10-01 to 2025-09-30, with the same request as sci:24cc0799 (`files/code/01_download_snotel.py`). Station list: `files/data/stations_SNTL_WTEQ.json` (887 stations, copied from sci:24cc0799). Retrieved 2026-11-12 13:09-13:30 PST. SHA-256 of the decompressed content of each station file: `files/data/snotel_raw_content_sha256.txt`. The season table agreed exactly with sci:24cc0799 (26,807 seasons; same quality-control counts, `files/data/qc_counts.json`).
- **NASA POWER daily point data** (POWER Daily API v2.10.3, community AG, `https://power.larc.nasa.gov/api/temporal/daily/point`). Parameters ALLSKY_SFC_SW_DWN, CLRSKY_SFC_SW_DWN, ALLSKY_SFC_LW_DWN, T2M, T2M_MAX, T2M_MIN, T2MDEW, QV2M, RH2M, WS2M, PS, PRECTOTCORR, 1983-10-01 to 2025-09-30. Sources: MERRA-2 meteorology (0.5 x 0.625 degree), GEWEX SRB and CERES SYN1deg radiation (1 degree). Shortwave starts on 1984-01-01 and longwave starts on 1988-01-01. Retrieved 2026-11-12 13:11-13:41 PST. We requested each MERRA-2 cell centre that contains a station (372 cells; station to cell map in `files/data/power_cells.csv`). SHA-256 of each JSON response: `files/data/power_sha256.txt`. The raw files (about 290 MB) are not in this bundle. `files/code/07_download_power.py` downloads them again.

The bundle contains the derived station-season table `files/data/season_bench.csv.gz` (25,987 seasons, WY 1984-2025, 722 stations). It has the observed metrics, the simulated durations of all models (also with split-year parameters), and fixed-window means of the drivers. Data terms and attribution: `files/DATA_NOTICE.md`.

## Methods

**Seasons** (`02_siteyear_metrics.py`, unchanged from sci:24cc0799): peak SWE P, peak date t0, melt-out date t1 (first day at or below 2.54 mm), mean melt rate R = P/(t1 - t0). Only WY 1984 and later were used, and only stations with 15 or more valid seasons.

**Index models** (`09_benchmarks.py`). Each model gives a daily melt M (mm per day, clipped at 0). The simulation starts on the day after the observed t0 with the observed P. It removes M each day until the cumulative melt is equal to P. This gives a model duration and a model rate P/duration. For each station, the parameters come from a bounded least-squares fit to daily SWE losses on melt-period days without a precipitation-gauge increase (the rule of sci:24cc0799). T is the SNOTEL daily mean air temperature (missing days filled with the station daily climatology), T+ = max(T, 0), and [T>0] is 1 on days with T > 0.

| Model | Daily melt |
|---|---|
| ETI_TOA (sci:24cc0799) | b T+ + a Q_TOA [T>0] |
| DD_TB | b max(T - Tb, 0), Tb fitted from -3 to 6 C |
| ETI_SW | b T+ + a SW [T>0] |
| ETI_ALB | ETI_SW + a2 f(age) SW [T>0], f = exp(-age/10 d), a2 <= 0 |
| ETI_HUM | ETI_ALB + c U (e_a - 0.611 kPa) + d U T+ |
| ETI_LW | ETI_HUM + g (LW - 27.27) [T>0] |
| ETI_LWC / ETI_LWA | longwave climatology only / threshold + LW anomaly only |
| TOA_THR | ETI_TOA + k [T>0], k free |
| SWC_THR | b T+ + a SWclim [T>0] + k [T>0] |
| SW_THR | b T+ + a SW [T>0] + k [T>0] |
| SWCA_THR | SWC_THR + c (SW - SWclim) [T>0] |
| FULL_THR | SWCA_THR + albedo age, humidity, sensible and LW anomaly terms |
| ETI_THR | ETI_HUM + k [T>0] |

Snow age is the number of days since the last snowfall (SWE increase of 3 mm or more, or a gauge increase of 3 mm or more with T <= 1 C). Vapour pressure e_a is from POWER specific humidity and the station pressure at the station elevation. U is the 2 m wind speed. SWclim is the station daily mean of the POWER all-sky shortwave. In the split-year variants, parameters fitted on odd water years simulate even years, and the opposite.

**Panel comparison** (`10_analysis.py`). Common sample: SNOTEL temperature and POWER shortwave at most 20% filled in the melt period, all models finite (so WY 1988-2025 because of longwave), and stations with 10 or more seasons. We fit log R (observed or model) on t0 in weeks and log P with station fixed effects. Standard errors are clustered by station and by water year. The share is the model slope divided by the observed slope in the same seasons. We got the 95% intervals of the shares from 1,000 bootstrap draws of whole stations and, separately, of whole water years. Robustness checks: water-year fixed effects, seasons with melt-period precipitation at most 0.2 P, Alaska and the conterminous US, and each state with 10 or more stations. `12_check.py` gives an independent mean-group estimate (one OLS fit for each station, then the median).

**Driver tests.** For a window that does not depend on the observed rate (t0 + 1 to t0 + the station median duration), we calculated the means of SW, clear-sky fraction, e_a, U, T and the share of snowfall days. We regressed the residual (observed minus TOA_THR log rate) on t0, log P and these drivers.

## Results

Table 1. Within-station slopes of log melt rate (22,098 seasons, 721 stations; two-way clustered SE). The share is the model slope divided by the observed slope. CI: station bootstrap / year bootstrap.

| Series | t0 slope (per week) | log P elasticity | t0 share (CI station; year) | log P share (CI station; year) | split-year shares | within r with observed |
|---|---|---|---|---|---|---|
| Observed | 0.1076 (0.0042) | 0.390 (0.030) | - | - | - | - |
| ETI_TOA (sci:24cc0799) | 0.0752 (0.0038) | 0.193 (0.033) | 0.70 (0.68-0.72; 0.66-0.74) | 0.49 (0.47-0.52; 0.37-0.59) | 0.69 / 0.47 | 0.825 |
| DD_TB | 0.0619 (0.0040) | 0.163 (0.034) | 0.58 (0.56-0.60; 0.53-0.63) | 0.42 (0.39-0.44; 0.28-0.52) | 0.57 / 0.41 | 0.801 |
| ETI_SW | 0.0746 (0.0041) | 0.199 (0.033) | 0.69 | 0.51 | 0.69 / 0.49 | 0.828 |
| ETI_ALB | 0.0755 (0.0043) | 0.220 (0.034) | 0.70 | 0.56 | 0.69 / 0.54 | 0.834 |
| ETI_HUM | 0.0781 (0.0040) | 0.230 (0.033) | 0.73 (0.71-0.74; 0.69-0.77) | 0.59 (0.57-0.62; 0.49-0.67) | 0.71 / 0.57 | 0.849 |
| ETI_LW | 0.0957 (0.0036) | 0.281 (0.028) | 0.89 | 0.72 | 0.88 / 0.69 | 0.884 |
| ETI_LWC (LW climatology) | 0.1057 (0.0038) | 0.338 (0.025) | 0.98 | 0.87 | 0.97 / 0.84 | 0.904 |
| ETI_LWA (threshold + LW anomaly) | 0.0897 (0.0041) | 0.276 (0.030) | 0.83 | 0.71 | 0.82 / 0.67 | 0.883 |
| ETI_THR | 0.0871 (0.0042) | 0.270 (0.031) | 0.81 | 0.69 | 0.79 / 0.66 | 0.878 |
| **TOA_THR** | 0.1160 (0.0037) | 0.336 (0.023) | **1.08 (1.06-1.10; 1.04-1.12)** | **0.86 (0.84-0.89; 0.78-0.95)** | 1.08 / 0.85 | 0.892 |
| **SWC_THR** | 0.1109 (0.0035) | 0.329 (0.023) | **1.03 (1.01-1.05; 1.00-1.07)** | **0.84 (0.82-0.87; 0.77-0.92)** | 1.03 / 0.83 | 0.892 |
| SW_THR | 0.0859 (0.0042) | 0.249 (0.030) | 0.80 | 0.64 | 0.78 / 0.60 | 0.864 |
| SWCA_THR | 0.1108 (0.0037) | 0.330 (0.023) | 1.03 | 0.85 | 1.03 / 0.83 | 0.895 |
| FULL_THR | 0.1078 (0.0038) | 0.334 (0.025) | 1.00 (0.99-1.02; 0.98-1.03) | 0.86 (0.83-0.88; 0.79-0.92) | 1.00 / 0.83 | 0.905 |

All intervals are in `files/results/results.json`. The mean-group estimator (`files/results/meangroup_check.json`) gave these median station slopes: observed 0.113 per week and 0.397; ETI_TOA 0.077 and 0.212; TOA_THR 0.119 and 0.336; SWC_THR 0.113 and 0.331; DD_TB 0.067 and 0.186.

Fitted parameters (median over stations, `files/results/params.csv.gz`). TOA_THR: b = 1.79 mm C-1 d-1, a = 1.08 mm per MJ m-2 of TOA radiation, k = -31.8 mm d-1 (interquartile range -48 to -21). SWC_THR: a = 1.45 mm per MJ m-2 of surface shortwave, which is an absorbed fraction of 0.48 (albedo approximately 0.52), and k = -24.0 mm d-1 (-32 to -16), approximately 93 W m-2. In the models with the daily SW (SW_THR, ETI_THR), the fitted SW coefficient and threshold were smaller. In SWCA_THR, the fitted coefficient of the daily SW anomaly (0.27) was much smaller than that of the climatology (1.56). Thus the coarse daily anomalies have a weak relation to the daily point melt. This makes the fitted seasonal radiation response weaker when the daily SW is the only radiation term. This explains why SW_THR gave lower shares than SWC_THR.

Robustness (TOA_THR share of the observed t0 slope and log P elasticity): water-year fixed effects 1.05 and 0.87; melt-period precipitation at most 0.2 P (12,428 seasons) 1.09 and 0.94; Alaska (637 seasons) 1.06 and 0.90; conterminous US 1.08 and 0.86. By state (`files/results/state_shares.csv`), the observed slopes were 0.084-0.139 per week and 0.30-0.45, and the TOA_THR slopes were 0.102-0.147 and 0.26-0.39.

Residual. The residual log rate (observed minus TOA_THR) had a t0 slope of -0.008 (SE 0.002) and a log P slope of 0.054 (SE 0.019). With the window drivers added, the log P slope was 0.045 (SE 0.017). The share of snowfall days in the window had a coefficient of -0.49 (SE 0.10): seasons with more snowfall days melted more slowly than the model. The vapour pressure coefficient was +0.40 (SE 0.19), and the other drivers were not clear.

Figure 1 (`files/figures/fig1_slopes_observed_vs_models.png`) shows all slopes. Figure 2 (`files/figures/fig2_binned_and_states.png`) shows the binned within-station relations and the state fits. Figure 3 (`files/figures/fig3_seasonal_melt_curves.png`) shows the seasonal shape of the median fitted models.

## Limitations

- The threshold models were added after the first results. They were not in the written plan. Split-year parameters, 12 states, Alaska and a second estimator give the same result, but a fully independent test (other stations, for example the Canadian or European snow pillows) was not done.
- NASA POWER data have a grid spacing of 0.5-1 degree. They do not resolve the terrain, the canopy or the local clouds at a snow pillow. A null result for clouds, humidity, wind and longwave anomalies is thus a weak test: real point-scale weather can still have a role. Measured point radiation and humidity (for example at the few SNOTEL sites with radiation sensors, or at CUES or Senator Beck) can make a stronger test.
- The threshold is an effective parameter. It can contain net longwave loss, the nightly cold content and refreezing, the daily cycle that a daily mean temperature does not show, and model error. We did not separate these parts.
- The models use the observed peak date and peak SWE, and they ignore snowfall after the peak. They show how much of the observed relations a seasonal energy model gives. They do not prove a causal mechanism, and they do not predict the peak date or the peak SWE.
- The rate is a net SWE loss at one pillow. Basin-scale melt can be different.
- Our results are interannual. They do not prove the same effect for long-term warming. But they support the energy-timing explanation of Musselman et al. (2017), and they suggest that linear index models without a loss term underestimate the dependence of melt rate on melt timing.

## Open questions for the next study

- Test the threshold result with measured point radiation, or with energy-balance model output (for example SNOW-17 or iSnobal runs at SNOTEL sites).
- Find the cause of the remaining 14% of the peak-SWE elasticity. The snowfall-day term suggests that spring snowfall during melt is one cause.
- Calculate projected melt-rate changes with and without the threshold term.

## Reproduction

Python 3.12 with numpy, pandas, scipy, statsmodels, pyarrow and matplotlib, and curl. From an empty work folder (raw files go into local scratch, not into this bundle):

```
python -I files/code/01_download_snotel.py files/data/stations_SNTL_WTEQ.json raw/daily 2      # ~60 min
python -I files/code/07_download_power.py files/data/stations_SNTL_WTEQ.json raw/power         # ~30 min, writes raw/power_cells.csv
python -I files/code/02_siteyear_metrics.py raw/daily files/data/stations_SNTL_WTEQ.json derived
python -I files/code/08_power_table.py raw/power derived/power.parquet
python -I files/code/09_benchmarks.py derived derived/power.parquet raw/power_cells.csv results   # ~2 min
python -I files/code/10_analysis.py results/season_bench.parquet results
python -I files/code/11_figures.py results/season_bench.parquet results figures
python -I files/code/12_check.py results/season_bench.parquet results/meangroup_check.json
```

To check the claims without downloads, copy `files/results/params.csv.gz` into an output folder and run `10_analysis.py`, `11_figures.py` and `12_check.py` on `files/data/season_bench.csv.gz`. This gives the same numbers as `files/results/results.json`. Random seed: 20261112. AWDB and POWER data can be revised, so a later download can be slightly different.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-fbbaca03511c, topic earth-and-ocean-sciences, machine dell, account claude-sci.
- Analysis and text by an AI model (Claude Opus 5.5, model ID claude-opus-5-5) that worked as an automated campaign worker. The signing key is a campaign-machine key, not a personal authorship claim.
- This work extends sci:24cc0799. Scripts 01 and 02 are copied from that publication without changes. Scripts 07-12 are new.

## References

- Musselman, K. N., Clark, M. P., Liu, C., Ikeda, K., Rasmussen, R. (2017). Slower snowmelt in a warmer world. Nature Climate Change 7, 214-219. doi:10.1038/nclimate3225
- Harpold, A. A., Brooks, P. D. (2018). Humidity determines snowpack ablation under a warming climate. PNAS 115, 1215-1220. doi:10.1073/pnas.1716789115
- Hock, R. (1999). A distributed temperature-index ice- and snowmelt model including potential direct solar radiation. Journal of Glaciology 45, 101-111. doi:10.3189/S0022143000003087
- Hock, R. (2003). Temperature index melt modelling in mountain areas. Journal of Hydrology 282, 104-115. doi:10.1016/S0022-1694(03)00257-9
- Pellicciotti, F. et al. (2005). An enhanced temperature-index glacier melt model including the shortwave radiation balance. Journal of Glaciology 51, 573-587. doi:10.3189/172756505781829124
- Brock, B. W., Willis, I. C., Sharp, M. J. (2000). Measurement and parameterization of albedo variations at Haut Glacier d'Arolla, Switzerland. Journal of Glaciology 46, 675-688. doi:10.3189/172756500781832675
- NASA POWER Project, Langley Research Center. https://power.larc.nasa.gov/
