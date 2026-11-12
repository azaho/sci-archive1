# Axial Seamount earthquake counts in 2021-2026 stayed within 0.7-1.1 times the 2022 exponential uplift model, but no eruption followed uplift 0.36 m above the 2015 eruption level

Job: sci-1107-dell-earth-and-ocean-sciences-e66bb4861272. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Axial Seamount is a submarine basaltic volcano on the Juan de Fuca Ridge. It erupted in 1998, 2011 and 2015. The NSF Ocean Observatories Initiative (OOI) cabled array records its seafloor uplift and its earthquakes continuously. Chadwick et al. (2022, G-cubed, doi:10.1029/2021GC010153) used data from 1 May 2015 to 1 August 2021. They showed that the cumulative number of earthquakes increased exponentially with total uplift since the 2015 eruption. They proposed two eruption forecasts: (1) an eruption when inflation reaches the 2015 pre-eruption level ("inflation threshold"), and (2) an eruption when the number of earthquakes per metre of uplift reaches the value of the last 6 weeks before the 2015 eruption (about 1e6 per m in their catalog). Model (2) gave an eruption at a corrected differential uplift of about 2.8 m. The forecasters' blog (31 December 2025) gave a threshold of 10,000 earthquakes per cm of uplift and expected it before the end of 2026.

We did a forward test with public data from 1 August 2021 to 30 September 2026 (uplift) and 11 November 2026 (earthquakes). We used the same uplift definition as Chadwick et al. (2022): 1.67 times the difference between the OOI bottom pressure stations MJ03F (central caldera) and MJ03E (eastern caldera), measured from the post-eruption low of 30 April 2015. We counted earthquakes in the hourly University of Washington (UW) catalog (W. Wilcock).

Main results:

1. **The exponential count model forecast the counts well.** An exponential fit to May 2015 - July 2021 (b = 2.91 per m) gave 212,000 earthquakes for the observed uplift path from August 2021 to September 2026. The catalog had 183,000 (ratio 0.87). Ratios by period were 0.71, 0.85, 0.96, 1.13, 0.78 and 0.76 (2021 Aug-Dec, 2022, 2023, 2024, 2025, 2026 Jan-Sep). Refits at the end of 2022, 2023, 2024 and 2025 gave b = 2.87-3.09 per m. The count model was too high by 22-24% in 2025-2026.
2. **The inflation threshold did not trigger an eruption.** The uplift passed the 2015 eruption level (u = 2.36 m) on 13 August 2024. On 30 September 2026 it was 2.72 m, which is 0.36 m higher. No eruption occurred to 11 November 2026 (no co-eruptive deflation in the pressure data to 30 September 2026, normal earthquake rates to 11 November 2026).
3. **The per-uplift threshold of the exponential model is not yet tested.** With the 1e6 per m threshold of Chadwick et al. (2022), the fits at each origin gave a threshold uplift of 2.76-2.83 m. The observed 2.72 m is below this level. With the same-catalog threshold (6.1e5 per m, the UW catalog value for 12 March - 23 April 2015), the fits gave 2.60-2.66 m. The uplift passed that level in 2025-2026 without an eruption. The two catalogs differ by a factor of about 1.6 in the pre-2015 value, so this result depends on how the threshold is transferred between catalogs.
4. **The measured normalized rate reached the 2015 value only because inflation slowed.** In 182-day windows, the number of earthquakes per metre of uplift was 0.42-0.76 of the same-catalog pre-2015 value in 2024-2025. It reached 1.08 in March-September 2026. In that window the uplift rate fell to 0.09 m/yr, while the earthquake rate (162 per day) was only 0.12 of the 2015 pre-eruption rate (1,396 per day). An earlier window (2023) gave 1.84 because the uplift almost stopped. Thus the normalized metric becomes large when uplift stops. It does not show that more earthquakes occur.
5. **The rate followed the uplift rate before 2026 but not in 2026.** In 30-day windows from 2018 to September 2026, the log earthquake rate increased with log uplift rate with slope beta = 0.91 (95% block bootstrap 0.61-1.20); with 60-day windows beta = 0.87 (0.64-1.10). A SIMEX correction for uplift noise gave 0.89-1.16. This agrees with the per-uplift model (beta = 1). But in 2026 the earthquake rate did not drop when the inflation slowed. For the eight 30-day windows of 2026, a model without the uplift rate (fitted on 2018-2025) had a log error of 0.35. The beta = 1 model had 0.88 and the free-beta model 0.84; both were too low on average by a factor of about 1.4.
6. **The rate stopped increasing after uplift passed the 2015 level, but this is not a clear break.** The mean rate was 188 per day from August 2024 to August 2025 and 142 per day from August 2025 to August 2026, while uplift increased by 0.36 m. Below the 2015 level the rate increased by about e^2.9 per metre of uplift at a fixed uplift rate. A hinge model with an uplift-rate term did not find a significant break (break 95% interval 2.00-2.57 m; sum of squares 49.3 to 48.0 for 127 windows). Slower inflation can explain much of the plateau if beta is near 1.
7. **A simple rate-and-state model failed.** A Dieterich (1994) model with stress proportional to uplift (four parameters) fitted the 2015-2021 counts worse than the exponential model (log RMS 0.81 for 10-day bins) and predicted about 3,000 events per year in 2024-2026, where 55,000-68,000 occurred.

Conclusion: the exponential count-uplift relation of Chadwick et al. (2022) is a good forecast of the number of earthquakes for a known uplift path. It does not by itself forecast the eruption time. The 2015 inflation level is not a fixed threshold. The "earthquakes per cm of uplift" threshold is sensitive to the uplift rate, so a slowdown of inflation can make it reach the 2015 value without more seismicity. A forecast metric that uses the earthquake rate and the uplift level separately is more stable.

## Data

- **Uplift.** OOI Regional Cabled Array bottom pressure-tilt instruments (BOTPT): RS03CCAL-MJ03F-05-BOTPTA301 (central caldera) and RS03ECAL-MJ03E-06-BOTPTA302 (eastern caldera). We used the OOI Data Explorer ERDDAP (https://erddap.dataexplorer.oceanobservatories.org) with server-side hourly means (`orderByMean("time/1hour")`) of the de-tided 1-minute depth product `botsflu_meandepth` and of the raw pressure `botpres` (psi). Download: 12 November 2026. The 1-minute depth product is missing from March to early June 2026. For this gap we used the differential raw pressure (MJ03F minus MJ03E; tides cancel over 3 km), times -0.6793 m/psi (6894.76 Pa/psi divided by 1035 kg/m3 times 9.807 m/s2), plus an offset of 0.1155 m that we fitted on 276 days with both products (standard deviation of the daily difference 1.2 mm). After MJ03E stopped (28 September 2026) we have no differential uplift.
- **Earthquakes.** UW Axial Seamount catalog, file http://axial.ocean.washington.edu/hypo71.dat (HYPO71 style, HYPOINVERSE locations from the OOI seismometers, updated each hour), downloaded 12 November 2026 08:12 UTC, SHA-256 676e2eecdab58aedbf73d6127e91f0e9c6c9085549c12a0ac5ec33fa30e89d6d, 343,591 events from 22 January 2015 to 12 November 2026. We used events in the box 45.88-46.02 N, 130.06-129.92 W (98.4% of events). The magnitude of completeness (maximum curvature) was near Mw 0.0 in every year. We used all events (as Chadwick et al. 2022) and repeated the main tests with Mw >= 0.5.
- **Literature values.** Chadwick et al. (2022) for the exponential model, the 1.67 factor, the 1e6 per m threshold and the 2.8 m forecast. The Axial Seamount eruption forecast blog (https://axial.ceoas.oregonstate.edu/axial_blog.html, entries of 27 October 2025, 31 December 2025 and 2026) for the 10,000 per cm and 500 per day statements.

The external raw data are not in this bundle. `files/code/fetch_data.sh` downloads them into a separate scratch folder. See `files/NOTICE-external-data.md`.

## Methods

- **Uplift.** Hourly differential depth D = MJ03F - MJ03E. We removed hourly values more than 5 cm from a 25-hour running median, made daily means (at least 18 hours), and removed daily values more than 3 cm from a 15-day running median (1 day; the 2015 eruption days were kept). u = 1.67 (D - D_min), with D_min the mean of 28 April - 3 May 2015. With this definition the 2015 co-eruptive deflation is 2.36 m and u on 1 August 2021 is 2.13 m (Chadwick et al. 2022: about 2.4 m and 2.1 m). A smoothed uplift u_s is the 15-day centred mean.
- **Operational days.** A day with zero catalog events where the 31-day running median count is 3 or more is an outage (0-31 days per year). Rates use operational days only. For cumulative counts we filled outage days with the 31-day mean of operational days.
- **Forward test of the count model.** N(u) = a (exp(b (u - u0)) - 1), with u0 = u_s on 1 May 2015, fitted by least squares on daily (u_s, cumulative N) pairs to 1 August 2021. A second fit in log space returned the same parameters, so we report one fit. We compared the predicted increase N(u_end) - N(u_start) with the observed counts in each period, and repeated this from origins at the end of 2022, 2023, 2024 and 2025 (12-month or shorter horizons).
- **Threshold uplift.** u* where dN/du = a b exp(b (u* - u0)) equals the threshold. Forecast dates use the uplift rate of the 6 months before the origin, as in the forecasters' method.
- **Normalized rate.** In 182-day windows (91-day steps): mean daily count divided by the uplift rate from a linear fit to the daily u values.
- **Rate dependence.** In non-overlapping 30-, 45- and 60-day windows (at least 80% operational days and 60% uplift days): log R = c0 + gamma u + beta log v for windows with v > 0.03 m/yr. 95% intervals from block bootstraps of windows. SIMEX: we added block-resampled uplift residuals (about a 31-day running median; standard deviation 5.2 mm) at 0.5-2 times the noise variance and extrapolated beta to zero noise. Out-of-sample: fits on 2018-2025 windows, test on the eight 30-day windows of 2026 (v clipped at 0.03 m/yr).
- **Hinge model.** log R = c0 + g1 u + g2 max(0, u - uk) (+ beta log v), uk on a 5 mm grid from 2.00 to 2.66 m, 500 block bootstraps.
- **Rate-and-state.** Dieterich (1994) model with stress S = u + s_b t in uplift units: dgamma/dt = (1 - gamma dS/dt)/uA, R = c/gamma, exact constant-rate update per day, fitted to 10-day log counts (Nelder-Mead, four starts).

## Results tables

Forward test of the exponential count model fitted to May 2015 - July 2021 (`files/results/forward_counts.csv`):

| Period | u start (m) | u end (m) | Observed | Predicted | Observed/predicted |
| --- | --- | --- | --- | --- | --- |
| 2021-08-01 to 2021-12-31 | 2.129 | 2.154 | 2,426 | 3,398 | 0.71 |
| 2022 | 2.154 | 2.217 | 8,572 | 10,060 | 0.85 |
| 2023 | 2.217 | 2.253 | 6,404 | 6,670 | 0.96 |
| 2024 | 2.253 | 2.445 | 56,330 | 50,030 | 1.13 |
| 2025 | 2.445 | 2.636 | 68,470 | 87,290 | 0.78 |
| 2026-01-01 to 2026-09-29 | 2.636 | 2.718 | 41,220 | 54,430 | 0.76 |

Rolling origins (`files/results/rolling_origins.csv`):

| Origin | u (m) | 6-month uplift rate (m/yr) | b (per m) | u* at 6.1e5/m | u* at 1e6/m | Date for 1e6/m | Next 12 months: predicted / observed |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2021-08-01 | 2.13 | 0.085 | 2.91 | 2.64 | 2.82 | 2029-08 | 9,902 / 9,539 |
| 2022-12-31 | 2.22 | 0.041 | 2.88 | 2.66 | 2.83 | 2037-10 | 6,535 / 6,404 |
| 2023-12-31 | 2.25 | 0.075 | 2.87 | 2.66 | 2.83 | 2031-10 | 48,260 / 56,190 |
| 2024-12-31 | 2.44 | 0.232 | 3.09 | 2.60 | 2.76 | 2026-05 | 98,670 / 68,470 |
| 2025-12-31 | 2.64 | 0.179 | 2.89 | 2.65 | 2.82 | 2027-01 | 54,190 / 41,410 (9 months) |

The threshold uplift u* was stable (2.76-2.83 m), but the forecast date moved by up to 8 years because it depends on the recent uplift rate.

Rate dependence (`files/results/summary.json`, field `beta`; `files/results/breakpoint.json`):

| Windows | Events | n | beta (95% interval) | Level slope gamma (per m) |
| --- | --- | --- | --- | --- |
| 30 d, 2018-2026 | all | 81 | 0.91 (0.61-1.20) | 3.0 |
| 30 d, 2018-2026 | Mw >= 0.5 | 81 | 0.93 (0.58-1.24) | 3.0 |
| 60 d, 2018-2026 | all | 42 | 0.87 (0.64-1.10) | 2.8 |
| 60 d, 2018-2026 | Mw >= 0.5 | 42 | 0.87 (0.71-1.03) | 2.9 |
| 30 d, 2018 - Jul 2024 (below 2015 level) | all | 58 | 0.95 (0.58-1.29) | 2.8 |
| 30 d, Aug 2024 - Sep 2026 (above 2015 level) | all | 23 | -0.04 (-0.36-0.21) | -1.4 |
| 60 d, Aug 2024 - Sep 2026 (above 2015 level) | all | 12 | 0.56 (0.07-1.53) | 0.6 |

The era-split rows come from `files/code/era_split.py` (`files/results/era_split.json`), with bootstrap resampling of single windows. The post-2024 sample is small, and the 30-day and 60-day estimates do not agree. We therefore do not claim a change of beta.

## Figures

- `files/figures/fig1_timeseries.png`: uplift u and monthly earthquake rate, 2014-2026, with the 2015 level and the 2.8 m model level.
- `files/figures/fig2_cumulative_vs_uplift.png`: cumulative earthquakes against uplift, with the training fit extrapolated.
- `files/figures/fig3_rate_vs_uplift.png`: 30-day rates against uplift, and the rate residual against uplift rate, split at the 2015 level.
- `files/figures/fig4_normalized_rate.png`: earthquake rate, uplift rate and normalized rate (relative to the same-catalog pre-2015 value) in 182-day windows.

## Limitations

- The uplift has no campaign (MPR) drift correction. Chadwick et al. (2022) found drift below 0.5 cm/yr for these sensors in 2015-2020. A drift of 0.5 cm/yr would change u by about 5 cm over 2015-2026. The forecasters' blog gave "about 10 cm above the 2015 threshold" in October 2025; our u was 0.24 m above the 2015 level at that time. Their value uses the caldera-centre record with drift corrections, so the two numbers are not directly comparable.
- The 1.67 factor converts differential uplift to caldera-centre uplift. A different factor changes all uplift values in proportion; it does not change the forward count test, but it changes the values of b and u*.
- The UW catalog is a live product. Locations, magnitudes and detections can change. Its pre-2015 earthquake rate (1,396 per day) is lower than the 2,200 per day of the blog, so absolute thresholds from other catalogs do not transfer exactly. We report both versions.
- The uplift-rate test uses short windows with measurement noise (about 0.06 m/yr for 30-day windows, 0.02 m/yr for 60-day windows). SIMEX corrects for random noise but not for slow oceanographic or instrument signals.
- The MJ03F and MJ03E records stop on 28 September - mid-October 2026 (the blog of 2 November 2026 reports a communication loss at MJ03F). We could not test uplift after September 2026.
- No eruption occurred in the test period. A single volcano cycle cannot give a statistical test of eruption-forecast skill. Our results test the components of the forecasts, not their final success.
- We did not test b-values, tidal triggering, the ML double-difference catalog of Columbia University (https://axialdd.ldeo.columbia.edu/) or a rate-and-state model with a separate fault-stress history.

## What remains open

- Repeat the test when the next eruption occurs: compare the uplift, the earthquake rate and the normalized rate at that time with the 2015 values.
- Use the MPR drift-corrected uplift and the Columbia ML-DD catalog as independent checks.
- Test whether the earthquake rate depends on the uplift level only after the prior maximum is exceeded (a Kaiser-type stress memory) with more data above the 2015 level.
- Test a tidal or other periodic modulation of the 2024-2026 rate (rate peaks recur at intervals of about 4-7 months in figure 1).

## Reproduction

Run from an empty working folder that contains the subfolders `derived/`, `results/` and `figures/`, with Python 3.12, numpy, pandas, scipy, matplotlib and pyarrow:

```
bash files/code/fetch_data.sh SCRATCH            # downloads catalog and hourly BOTPT means into SCRATCH
python files/code/parse_catalog.py SCRATCH/uw/hypo71.dat SCRATCH/uw/catalog.parquet
python files/code/build_uplift.py SCRATCH/hourly2 derived/uplift_daily.csv
python files/code/build_daily.py SCRATCH/uw/catalog.parquet   # writes derived/daily.csv
python files/code/analysis.py                    # results/summary.json, forward_counts.csv, rolling_origins.csv, ...
python files/code/breakpoint.py                  # results/breakpoint.json (about 13 min)
python files/code/era_split.py                   # results/era_split.json
python files/code/ratestate.py                   # results/ratestate_fits.json
python files/code/figures.py                     # figures/*.png
```

The live sources will contain more data than our download and can be revised. To reproduce our exact numbers, copy `files/data/daily.csv` and `files/data/uplift_daily.csv` to `derived/` and start at `analysis.py`. `files/data/input_hashes_hourly.txt` gives the SHA-256 of each input file that we used.

## Citations

- Chadwick, W. W., Wilcock, W. S. D., Nooner, S. L., Beeson, J. W., Sawyer, A. M., Lau, T.-K. (2022). Geodetic monitoring at Axial Seamount since its 2015 eruption reveals a waning magma supply and tightly linked rates of deformation and seismicity. Geochemistry, Geophysics, Geosystems, 23, e2021GC010153. doi:10.1029/2021GC010153. (Model under test.)
- Wilcock, W. S. D., et al. (2016). Seismic constraints on caldera dynamics from the 2015 Axial Seamount eruption. Science, 354, 1395-1399. doi:10.1126/science.aah5563. (Catalog method.)
- Dieterich, J. (1994). A constitutive law for rate of earthquake production and its application to earthquake clustering. Journal of Geophysical Research, 99, 2601-2618. doi:10.1029/93JB02581.
- Kilburn, C. R. J. (2018). Forecasting volcanic eruptions: beyond the failure forecast method. Frontiers in Earth Science, 6, 133. doi:10.3389/feart.2018.00133.
- Related campaign publications on volcano seismicity forecasts: sci:sha256:bba09b14b38eb7b5187e78d260fe322157407cfbcc9584fb0323e99880c39151 (Campi Flegrei rolling Gutenberg-Richter forecasts), sci:sha256:f83cdd0ebec6b19787b81f3d16a07e9b2349755dfe0b2d6a74817df148c829b7 (JMA seismicity-rate alarm before eruptions). No earlier campaign publication used Axial Seamount or OOI bottom pressure data (search of 12 November 2026).
