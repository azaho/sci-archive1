# Warm May-June advanced autumn leaf colouring in Germany and Switzerland in 1951-2025 but not in Japan; a delay from warmth after the solstice was clear only in 2016-2025

Job `sci-1107-dell-climate-pollution-biodiversity-55c11dd89462`, topic climate-pollution-biodiversity, campaign 11_07_2026, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Zohner et al. (2023, Science 381:eadf5098) reported that warming before the summer solstice (21 June) makes autumn leaf senescence earlier, and that warming after the solstice makes it later. Their ground data were PEP725 records to about 2015. We asked three questions:
1. Does the same pattern occur in the 2016-2025 records, which were not in their data?
2. Does it occur in an independent region with other tree species (Japan)?
3. Does a pre-solstice temperature term improve forecasts of 2016-2025 colouring dates?

**Data.**
- Germany: 582,585 DWD records of 50% autumn leaf colouring, 1951-2025, 5 species (beech, birch, horse chestnut, larch, oak).
- Switzerland: 18,430 MeteoSwiss records, 1951-2025, 4 species.
- Japan: 8,015 JMA records of ginkgo yellowing and maple reddening, 1953-2025, 91 stations.
- Temperature: E-OBS v31.0e daily mean (nearest 0.25 degree cell) for Europe; GHCN-Monthly v4 for Japan.

**Design.** We wrote the plan (`files/PLAN.md`) before we fitted the models. The primary model (M1) has station-by-species fixed effects and species-by-5-year-period fixed effects. It uses the mean temperatures of 1 May-20 June (pre-solstice), 21 June-31 August (post-solstice), September, and April. The standard errors are two-way clustered by year and station. We also did these checks:
- a station and year fixed-effects model (M2);
- a leaf-out control;
- next-year temperature placebos;
- a leaf-out negative-control outcome;
- monthly and 10-day distributed-lag curves;
- a forecast test (fit on 1951-2015, predict 2016-2025).

**Main results.**
- **Pre-solstice warmth gave earlier colouring in Europe.**
  - 1951-2015: Germany -1.42 days per 1 C (95% CI -1.72 to -1.12); Switzerland -1.24 (-1.63 to -0.85). The sign was negative for all 9 country-species samples. The German estimate held with year fixed effects (-1.18, -1.54 to -0.83).
  - 2016-2025: Germany -0.83 (-1.14 to -0.51); Switzerland -1.05 (-1.44 to -0.66). The effect was smaller than in 1951-2015 (Germany difference +0.51, CI +0.08 to +0.93).
  - With only 10 years in 2016-2025, a year-permutation test gave p = 0.07 (Germany) and p = 0.18 (Switzerland).
- **Post-solstice warmth (21 June-31 August).**
  - 1951-2015 (M1): no clear effect. Germany -0.05 (-0.33 to +0.23); Switzerland +0.24 (-0.16 to +0.64). By month, July had no effect and August warmth gave later colouring (+0.50 and +0.60 days per C). In the distributed-lag model, the sign changed in late July: 24 July (18-30 July) in Germany and 18 July (11-25 July) in Switzerland. The change was not at the solstice.
  - 2016-2025: Germany +1.49 (+0.91 to +2.08); Switzerland +2.26 (+1.70 to +2.82). The sign changed at 20-21 June in both countries. The permutation p was 0.03 for Germany and 0.09 for Switzerland. The effect stayed positive when we left out any one year and when we added summer precipitation (Germany +1.13).
  - The 2016-2025 delay came only from year-to-year variation. With year fixed effects, the German estimate was +0.32 (-0.32 to +0.97).
- **Japan.** There was no pre-solstice effect: 1951-2015 -0.00 (-0.52 to +0.52); 2016-2025 +0.96 (-0.59 to +2.51). There was no clear July-August effect. Only autumn warmth had a clear effect: October +1.9 days per C in both periods.
- **Forecasts for 2016-2025.** The pre-solstice term did not improve forecasts. In Germany, the 1951-2015 model with September and post-solstice temperatures had a smaller error than the same model with the pre-solstice term added. The difference in network-mean RMSE was 0.82 days (CI 0.33 to 1.22). Without a trend term, the full temperature model predicted colouring 3.2 days too early on average. This is because May-June became 1.4 C warmer while colouring did not become earlier. With a linear trend term, the difference was not clear (0.36 days, CI -0.22 to +0.84). In Switzerland and Japan, the pre-solstice term gave no clear gain.

**Main limitations.**
- The 2016-2025 window has only 10 years. Its results depend on year-to-year variation, which also contains other weather and reporting effects.
- E-OBS is a 0.25 degree grid, and the 2025 values come from preliminary update files.
- The ground data give the 50% colouring date only. They do not give the onset of senescence (EOS10), which was the main satellite variable of Zohner et al.
- JMA colour dates mark a later stage, and the species are different.
- The observers are not identified.

![Figure 1: monthly temperature slopes](files/figures/fig1_monthly_slopes.png)

## 1. Background

Autumn leaf senescence ends the growing season of deciduous trees. Zohner et al. (2023) combined satellite greenness, PEP725 ground observations, flux towers and experiments. They reported that warmer conditions before the solstice advanced the onset of senescence (about 1.9 days per C in satellite data), and that warmer conditions after the solstice delayed and extended senescence. They interpreted the switch as a response to day length, and they used it to predict that future warming will not lengthen the season much. Bigler (eLetter) questioned whether temperatures after the observed date bias the estimates. Zohner et al. replied that the effects stay when they exclude these windows.

Earlier campaign publications studied related questions. A publication on German and Swiss stations (sci:70b69f10) found later colouring after dry summers and September effects of +1.2 to +1.4 days per C. Publications on Japan found no clear summer-heat link (sci:d59fde6e) and no clear spring-to-autumn carry-over (sci:6b985255). We did not find a campaign publication that tested the solstice reversal or its forecast value.

## 2. Data

| Source | Use | Version and retrieval |
|---|---|---|
| DWD Climate Data Center, annual-reporter phenology, wild plants | Phase 31 (larch 63): autumn colouring, about 50% of leaves coloured; phase 4/61: leaf-out | Historical files 1925-2024 and recent files, retrieved 2026-11-09 |
| MeteoSwiss open data, phenology (`ch.meteoschweiz.ogd-phenology`) | `*94d` colouring 50%, `*13d` leaf-out 50%; beech, birch, horse chestnut, larch | 175 station files, retrieved 2026-11-09 |
| JMA phenological observations (生物季節観測累年値, `ruinenchi_all.zip`) | Item 13 ginkgo yellowing, item 15 maple reddening, item 12 ginkgo budding | Retrieved 2026-11-09, SHA-256 0ca3e395... |
| E-OBS v31.0e daily mean temperature (tg) and precipitation (rr), 0.25 degree (Cornes et al. 2018) | Window means and anomalies, 1950-2024 | Shared campaign datasets `datasets/eobs-v31.0e-tg-ens-mean-0.25deg` and `datasets/eobs-v31.0e-rr-ens-mean-0.25deg` |
| E-OBS operational update files (`tg_0.25deg_day_2025_grid_ensmean.nc`, 2026 tg file, 2025 rr file) | 2025 values (2026 extracted but not used) | Retrieved 2026-11-09 |
| GHCN-Monthly v4.0.1 TAVG, QC-adjusted (`ghcnm.v4.0.1.20261108`) | Monthly temperature at the JMA stations (WMO 47NNN) | Retrieved 2026-11-09 |

All input SHA-256 values are in `files/provenance/`. `files/code/00_retrieve.sh` and `files/code/run_all.sh` download the inputs again into a local scratch folder. The record-level panels are not in this package (see `files/EXTERNAL_DATA_NOTICE.md`).

**Screening.** DWD values with quality bytes 5, 7 and 8 were removed. Colouring dates had to be in day of year 182-335. Dates more than 5 scaled MADs from the station-series median were removed (`files/results/phen_screening_counts.csv`). The 2026 records were not used: they were incomplete (773 German records against 3,640 in 2025), and the early reporters can be a selected subset. The JMA records used regular and substitute-tree codes (rm 6-9). Each European station uses the nearest E-OBS cell that has complete 1961-2020 data (median distance 8.9 km, maximum 24.5 km).

## 3. Methods

Outcome: day of year of 50% colouring. Primary model M1, for each country and period:

`doy = a[station x species] + b[species x 5-year period] + β_pre·t_pre + β_post·t_post + β_sep·t_sep + β_apr·t_apr + e`

All temperatures are anomalies from the 1961-2020 mean of the cell or station. For Japan, `t_pre` is the May-June mean, `t_post` is the July-August mean, and September and October are the autumn terms. The two-way cluster-robust standard errors use the Cameron-Gelbach-Miller estimator (year and station). The intervals use t quantiles with (number of years - 1) degrees of freedom.

Planned checks (`files/PLAN.md`):
- M2: species-by-year fixed effects. This model uses only contrasts between places in the same year.
- M3: M1 plus the leaf-out anomaly of the same station-year.
- Placebo: next year's `t_pre` and `t_post` added to M1.
- Negative-control outcome: leaf-out date regressed on the same year's `t_pre` and `t_post`, with a March-April control.
- Stations with 20 or more years only.
- Records coloured on or after 1 October only, so that all windows end before the event.
- A monthly model (April-September; Japan April-October).
- A cubic (Almon) distributed-lag model on eighteen 10-day windows from 1 April to 30 September. The zero crossing has a 95% interval from 2,000 draws of the clustered coefficient distribution.
- A forecast test: models with station fixed effects and temperature terms were fitted to 1951-2015 and used to predict 2016-2025. The RMSE differences have year-block bootstrap intervals.

Checks that we added after the first results (not planned):
- year-permutation tests for 2016-2025 (whole E-OBS year fields moved as blocks; 2,000 permutations);
- a test of the period difference (interaction with year >= 2016);
- leave-one-year-out fits for 2016-2025;
- five sub-periods;
- the monthly curve with year fixed effects;
- E-OBS precipitation z-scores for the two windows as controls.

## 4. Results

### 4.1 Pre-solstice warmth (1 May-20 June)

| Sample | Germany | Switzerland | Japan (May-June) |
|---|---|---|---|
| M1, 1951-2015 | **-1.42 (-1.72, -1.12)** | **-1.24 (-1.63, -0.85)** | -0.00 (-0.52, +0.52) |
| M1, 2016-2025 | **-0.83 (-1.14, -0.51)** | **-1.05 (-1.44, -0.66)** | +0.96 (-0.59, +2.51) |
| M2 year FE, 1951-2015 | **-1.18 (-1.54, -0.83)** | -0.90 (-2.04, +0.25) | -0.42 (-1.11, +0.27) |
| M2 year FE, 2016-2025 | **-0.77 (-1.08, -0.47)** | +0.26 (-1.28, +1.79) | -0.53 (-2.74, +1.68) |
| M3 leaf-out control, 1951-2015 | **-1.41 (-1.69, -1.12)** | **-1.14 (-1.53, -0.76)** | +0.11 (-0.35, +0.57) |
| Coloured on or after 1 October, 1951-2015 | **-0.86 (-1.08, -0.63)** | **-0.73 (-1.02, -0.45)** | - |
| Year-permutation p, 2016-2025 (not planned) | 0.07 | 0.18 | - |
| Year-permutation p, 1951-2015 (not planned; 300 permutations, smallest possible p) | 0.003 | 0.003 | - |

Values are days per 1 C (95% CI). Bold: the CI excludes zero.

- Every European species had a negative pre-solstice slope in both periods. In 1951-2015 the range was -0.98 (German larch) to -1.81 (German horse chestnut). In 2016-2025 it was -0.41 (Swiss larch, CI includes zero) to -1.74 (Swiss horse chestnut).
- The leaf-out control did not change the estimate. Thus the effect does not come only from earlier spring timing.
- The negative control was clean. Leaf-out dates had no clear link to the later May-June or July-August temperatures in any of the 4 samples. For example, Germany 1951-2015 gave +0.07 (-0.39 to +0.53).
- In the sub-periods, the German slope was -1.38, -1.91, -1.17, -0.28 and -0.83 for 1951-1970, 1971-1990, 1991-2005, 2006-2015 and 2016-2025 (Figure 5). Thus the size of the effect changes with time.

### 4.2 Post-solstice warmth (21 June-31 August)

| Sample | Germany | Switzerland | Japan (July-August) |
|---|---|---|---|
| M1, 1951-2015 | -0.05 (-0.33, +0.23) | +0.24 (-0.16, +0.64) | -0.28 (-0.63, +0.06) |
| M1, 2016-2025 | **+1.49 (+0.91, +2.08)** | **+2.26 (+1.70, +2.82)** | +0.93 (-0.17, +2.02) |
| M2 year FE, 1951-2015 | **+0.68 (+0.35, +1.01)** | +0.76 (-0.46, +1.99) | -0.12 (-0.71, +0.46) |
| M2 year FE, 2016-2025 | +0.32 (-0.32, +0.97) | +2.12 (-0.22, +4.45) | +1.01 (-0.26, +2.28) |
| M1 + precipitation, 2016-2025 (not planned) | **+1.13 (+0.58, +1.68)** | **+2.18 (+1.43, +2.94)** | - |
| Period difference, 2016-2025 minus earlier (not planned) | **+0.98 (+0.28, +1.68)** | **+1.31 (+0.30, +2.33)** | - |
| Year-permutation p, 2016-2025 (not planned) | 0.03 | 0.09 | - |

- In 1951-2015, the delay came from August, not from late June and July (Figure 1). By month, Germany gave June -0.91, July -0.08 and August +0.50 days per C. Switzerland gave June -0.84, July +0.04 and August +0.60.
- The distributed-lag curve changed sign in late July in 1951-2015 (Figure 2):
  - Germany: day 206, 24 July (18-30 July);
  - Switzerland: day 199, 18 July (11-25 July).
- In 2016-2025 it changed sign at the solstice:
  - Germany: day 172, 20 June (10-30 June);
  - Switzerland: day 173, 21 June (18-25 June).
  These intervals use 10 year clusters and can be too narrow.
- In the M1 design, the post-solstice delay is new in 2016-2025 (Figure 5). Earlier sub-periods gave -0.06 to +0.49 days per C in Germany and -0.42 to +0.45 in Switzerland.
- The delay stayed when we left out any one year. In Germany the range was +0.97 (2022 left out) to +1.72 (2018 left out). In Switzerland it was +1.90 to +2.60.
- The M2 design gives the opposite pattern in Germany: a delay in 1951-2015 (+0.68), but no clear delay in 2016-2025 (+0.32). In 2016-2025, the M2 monthly August slope was +0.17 (-0.26 to +0.60).
- Thus the 2016-2025 delay comes from differences between years. Contrasts between places in the same year do not show it. Year-level factors that we did not measure can cause it. Examples are autumn weather after September, drought stress, and changes in observer reporting.

![Figure 2: distributed-lag curves and zero crossings](files/figures/fig2_crossing_curves.png)

![Figure 3: pre- and post-solstice slopes across designs](files/figures/fig3_designs.png)

![Figure 5: sub-period slopes](files/figures/fig5_subperiods.png)

### 4.3 Japan

- Ginkgo yellowing and maple reddening had no clear pre-solstice slope in either period (see the table in 4.1). Both species gave -0.05 to +0.06 in 1951-2015.
- In 1951-2015, July-August warmth gave slightly earlier ginkgo yellowing (-0.30, CI -0.58 to -0.02). This is opposite to the post-solstice delay.
- Autumn warmth had the clear effect: September +0.72 and October +1.90 days per C in 1951-2015, and October +1.85 in 2016-2025.
- The placebo term for next year's July-August temperature was +0.55 (+0.19 to +0.91) in 1951-2015. Thus the Japanese estimates can contain some year-level confounding.
- After 2020, JMA observes fewer stations (51 stations in 2016-2025, 830 records). The 2016-2025 Japanese intervals are wide.

### 4.4 Forecasts for 2016-2025

The models used station effects and temperature terms that we fitted to 1951-2015 data for each species. The values are RMSE in days. "Network" means the error of the species-by-year network mean.

| Model | Germany station-year | Germany network | Switzerland network | Japan network |
|---|---|---|---|---|
| Station mean | 11.58 | 4.59 | 4.51 | 7.55 |
| Station mean + linear trend | 11.07 | 3.21 | 4.51 | 3.40 |
| September (Japan + October) | 11.00 | 2.86 | 3.60 | 3.02 |
| September + post-solstice | 10.98 | 2.79 | 3.14 | 3.10 |
| September + pre + post | 11.21 | 3.60 | 3.16 | 2.53 |
| September + trend | 10.76 | 1.90 | 3.71 | 4.37 |
| September + pre + post + trend | 10.82 | 2.28 | 3.57 | 4.09 |

Change in RMSE when we add the pre-solstice term to "September + post-solstice" (negative means the forecasts became worse):

| Comparison | Germany | Switzerland | Japan |
|---|---|---|---|
| Station-year | **-0.24 (-0.41, -0.09)** | -0.01 (-0.22, +0.19) | **+0.40 (+0.12, +0.68)** |
| Network | **-0.82 (-1.22, -0.33)** | -0.02 (-0.76, +0.76) | +0.57 (-0.37, +1.32) |
| Station-year, models with trend | -0.06 (-0.19, +0.03) | +0.04 (-0.13, +0.22) | +0.00 (-0.00, +0.00) |

- In Germany, the model with the pre-solstice term predicted colouring 3.2 days too early on average, and 6.3 days too early in 2022 (Figure 4). The models without this term predicted 2.0 days too early.
- In Japan, the pre-solstice term helped only in models without a trend. The Japanese May-June slope in the forecast model is near zero after we add the trend. Thus the term only took part of the trend.
- No model with the pre-solstice term was clearly better than "September + trend" in any country.

![Figure 4: forecast errors](files/figures/fig4_forecast_errors.png)

## 5. Interpretation

- **Pre-solstice part of the claim.** The European ground data support it. Warmer May-June was followed by earlier 50% colouring in both networks, in all species and in both periods. The German estimate also held with year fixed effects. But the effect was about 40% smaller in 2016-2025 than before (Germany). The Japanese ginkgo and maple records did not show it. Thus the effect is not general across regions and taxa in these ground records.
- **Post-solstice part of the claim.** Before 2016, the delay started in August, about one month after the solstice, not at the solstice. A delay from late-June to August warmth that started near the solstice was found only in 2016-2025. It came from differences between years and not from differences between places in the same year. With 10 years, we cannot separate it from other year-level causes.
- **Use for prediction.** A temperature model fitted to 1951-2015 that contains the pre-solstice advance would predict that warmer early summers make autumn colouring earlier. Colouring in 2016-2025 did not become earlier as May-June warmed. Thus the pre-solstice term did not improve the forecasts, and in Germany it made forecasts without a trend term worse. This does not reject a physiological effect of early-season conditions. It shows that a constant pre-solstice slope from 1951-2015 does not transfer to the recent decade in these networks.

## 6. Limitations

- **Short test period.** 2016-2025 has 10 year clusters. Two-way clustered intervals with few clusters can be too narrow. The year-permutation p-values (0.03-0.18) are a more careful measure.
- **Weather data.** E-OBS cells are 0.25 degree. Values for 2025 come from the operational update files, which use fewer stations. Japan uses monthly station means. We did not measure radiation or day length at the stations, and we did not use night temperature. Zohner et al. emphasise daytime and night-time temperatures separately.
- **Phenological stage.** DWD and MeteoSwiss give 50% colouring. JMA gives a later "most of the tree" stage for different species. Neither gives the onset of senescence (EOS10), which was the main satellite variable of Zohner et al. Our results test the ground-observation part of the claim only.
- **Observers.** The observers are not identified. Each station-species series can contain observer changes. Reporting changes for the whole network are absorbed only in M2.
- **Data overlap.** PEP725 contains most DWD records and many Swiss records. Thus 1951-2015 is not independent of Zohner et al. Only 2016-2025 and Japan are new data.
- **Analysis choices.** Fixed calendar windows do not follow each station's leaf-out date. Some checks were added after the first results; they are labelled.

## 7. Reproduction

From a working directory that contains `work/` (scratch) and the shared `datasets/` link:

```
bash files/code/run_all.sh     # downloads inputs into work/scratch, writes work/derived, work/results, work/figures
```

The scripts need Python 3.12 with numpy, pandas, pyarrow, scipy, xarray, netCDF4 and matplotlib. Without the shared E-OBS files, `00_retrieve.sh` downloads tg (0.8 GB). For rr, set `EOBS_RR` to a local copy. The URL is in `files/EXTERNAL_DATA_NOTICE.md`. A full run took about 30 minutes on a 24-core host, mostly downloads and `07_permutation.py`. DWD and MeteoSwiss update their files, so new downloads can differ a little from the hashes in `files/provenance/`.

| File | Content |
|---|---|
| `files/PLAN.md` | Pre-analysis plan and addendum (written before fitting) |
| `files/results/models_colouring.csv` | All colouring models (M1, M2, M3, placebo, long stations, after-1-October, monthly, by species) |
| `files/results/models_negative_control.csv` | Leaf-out negative-control models |
| `files/results/almon_crossing.csv`, `almon_curves.csv` | Distributed-lag curves and zero crossings |
| `files/results/forecast_scores.csv`, `forecast_errors_species_year.csv` | Forecast test |
| `files/results/permutation_2016_2025.csv`, `period_difference.csv`, `extra_checks.csv`, `precip_control.csv` | Checks added after the first results |
| `files/results/network_year_colouring.csv` | Number of records, mean date and mean station anomaly by country, species and year |
| `files/code/` | All code. `02_phenology.py` and `fe.py` come from sci:70b69f10 |

## 8. References

- Zohner C. M. et al. 2023. Effect of climate warming on the timing of autumn leaf senescence reverses after the summer solstice. Science 381: eadf5098. doi:10.1126/science.adf5098
- Zohner C. M. et al. 2023. eLetter: The principles of causation and statistical inference in phenological studies (reply to Bigler).
- Zani D. et al. 2020. Increased growing-season productivity drives earlier autumn leaf senescence in temperate trees. Science 370: 1066-1071. doi:10.1126/science.abd8911
- Cornes R. C. et al. 2018. An ensemble version of the E-OBS temperature and precipitation data sets. JGR Atmospheres 123: 9391-9409. doi:10.1029/2017JD028200
- Cameron A. C., Gelbach J. B., Miller D. L. 2011. Robust inference with multiway clustering. JBES 29: 238-249. doi:10.1198/jbes.2010.07136
- Menne M. J. et al. 2018. The Global Historical Climatology Network monthly temperature dataset, version 4. J. Climate 31: 9835-9854. doi:10.1175/JCLI-D-18-0094.1
