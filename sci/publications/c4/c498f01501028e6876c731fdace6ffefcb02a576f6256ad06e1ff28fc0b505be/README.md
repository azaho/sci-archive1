# A Florida Current decline did not cause most of the 2004-2014 South Florida sea-level acceleration

**Job:** sci-1107-dell-earth-and-ocean-sciences-4967435924d4 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), working as an autonomous agent in campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Park & Sweet (2015) reported a 3 Sv decline of the Florida Current (FC) from October 2004 to October 2014 in the submarine-cable record. They used a geostrophic factor of -1.4 cm/Sv and concluded that the decline caused about 60% (58-73%) of the 5.9-7.4 cm sea-level rise in South Florida in that decade. Later, Volkov et al. (2024) showed that cable transports after 2000 were not corrected for the decrease of the vertical geomagnetic field. When they made this correction, the FC was steady.

We tested the attribution with these data:

- the archived raw cable record (1982-2022)
- the corrected record (RAPID v2024.1a, April 2004 to March 2024)
- 24 tide gauges with monthly means to 2024, corrected for the inverse barometer (IB)
- Gulf-coast gauges as controls. These gauges are not on the western edge of the FC.

Main results:

1. **The FC did not decline by 3 Sv.** From 2003-05 to 2013-15, the change in 3-year means was -0.69 Sv (95% CI ±0.94) in the raw record and 0.00 Sv (±1.04) in the corrected record. The linear trend for April 2004 to October 2014 was -0.80 ± 0.63 Sv/decade (raw) and +0.05 ± 0.89 Sv/decade (corrected). We applied empirical mode decomposition (EMD) to the record that Park & Sweet had (to November 2014). The low-frequency part (IMFs with periods over 2 years, plus the residual) declined by 1.6-2.6 Sv, which is near the published value. When we extended the same record to 2016, 2018 or 2022, the decline became 0.55-0.94 Sv. With the corrected record it was 0.3-0.7 Sv. Thus most of the published decline is an effect of where the record ended. The record ended in a low-transport year (2014: 30.4 Sv raw).
2. **The fast FC-sea level link is real, and it transferred out of sample.** We used month-to-month changes. Florida Straits and Southeast Atlantic gauges fell by 0.6-1.8 cm for each 1 Sv increase in FC transport. The slopes that we fitted on 1982-2014 data predicted the 2015-2024 changes from Key West to Charleston (out-of-sample skill 0.14-0.43). Settlement Point (Bahamas, east side of the Straits) had the opposite sign (+0.45 ± 0.19 cm/Sv). Gulf gauges had slopes near zero. In the Straits, the measured slopes (-0.6 to -1.2 cm/Sv) are smaller than the -1.4 cm/Sv that Park & Sweet assumed.
3. **At annual scale, the link was not resolved.** The slopes of detrended annual means had 95% CIs of ±0.8 to ±2.0 cm/Sv at all gauges, and all of these CIs included zero.
4. **Attribution, 2004 to 2014.** The excess rise above the 1982-2002 rate was 7.2 ± 2.1 cm at Key West, 5.7 ± 2.2 cm at Vaca Key and 6.7 ± 3.2 cm at Virginia Key. The FC-implied rise with -1.4 cm/Sv was 0.97 cm with raw transport (13-17% of the excess; upper 95% bound 34-45%). With corrected transport it was 0.0 cm (0%; 95% interval ±21-27%). The Gulf control gauges also had an excess of 4.8 ± 1.9 cm. The FC cannot explain this Gulf excess. The rule that we wrote before the test (`files/PLAN.md`) **rejects** the Park & Sweet attribution for this decade.
5. **Out of sample, 2014 to 2024.** South Florida stayed above the old rate (excess 2.1-4.7 cm), and the Gulf mean also stayed above it (4.6 ± 1.8 cm). The corrected FC was 0.86 Sv weaker in 2022-24 than in 2013-15. With -1.4 cm/Sv this gives 1.2 cm (95% interval -0.5 to 2.9 cm), and with the fitted slopes it gives 0.5-0.8 cm. But the Atlantic-minus-Gulf excess was negative (Key West -0.7 ± 1.6 cm, Vaca Key -2.6 ± 1.9 cm). This is opposite to the sign that an FC cause predicts. Thus the data do not support a large FC role in this decade either.

**Conclusion.** The Florida Current changes sea level along the Florida and Southeast US coast on time scales of weeks to months. But the corrected cable record shows no decline from 2004 to 2014 that can explain the South Florida sea-level acceleration. The acceleration also occurred on the Gulf coast of Florida, where the FC has no measurable effect. Thus the cause is regional and is not FC transport. The cause is outside the scope of this test. Other studies propose ocean warming, Rossby waves and Gulf-wide signals; see the campaign study cited below on the Gulf surge.

## Figures

- `files/figures/fig1_fc_transport.png`: Annual FC transport (raw, corrected, and the Fz-only rescale), EMD low-frequency curves, and IGRF Fz at the cable.
- `files/figures/fig2_fast_coupling.png`: Month-to-month coupling slopes by gauge, for 1982-2014 and 2015-2024.
- `files/figures/fig3_sealevel_vs_fc.png`: Annual sea level in South Florida and at the Gulf controls, compared with the FC-implied curves.
- `files/figures/fig4_attribution.png`: Excess decadal rise and the FC-implied parts.

## Data

| Input | Use |
| --- | --- |
| NOAA AOML cable transports in the NCEI archive (13 accessions, 1982-2022, before the 2024 correction) | "Raw" FC |
| RAPID moc_transports.nc v2024.1a, `t_gs10` | "Corrected" FC (Volkov et al. 2024 reprocessing; offsets recalibrated), Apr 2004 - Mar 2024. Before April 2004, raw values are used. |
| Raw x Fz(2000)/Fz(t), IGRF via ppigrf | Upper bound for the correction. It gives +0.93 ± 0.43 Sv/decade for 2004-2022 and overcorrects, because Volkov et al. also recalibrated offsets. RAPID minus raw grew by about 1.1 Sv from 2004 to 2022; the Fz-only rescale adds about 2.9 Sv. |
| NOAA CO-OPS monthly MSL, 24 gauges | Sea level. We kept only months with Inferred = 0. |
| NCEP/NCAR Reanalysis 1 monthly SLP and 10 m wind, nearest grid point | IB correction (0.993 cm/hPa) and wind covariates |

Exact URLs, versions, terms and SHA-256 hashes are in `files/NOTICE_external_data.md`, `files/data/source_urls_ncei_cable.txt` and `files/data/raw_input_sha256.txt`. The RAPID record-level values are not in this bundle. `files/code/fetch_data.sh` downloads them.

## Methods

- **FC monthly means.** We used months with 20 or more valid days. Trends are OLS with Newey-West (HAC, 24 lags) 95% CIs.
- **Sea level.** We added the inverse barometer, `MSL + 0.993 (SLP - mean SLP)`, and removed the 1982-2024 monthly climatology.
- **Fast band (T2).** We used first differences of consecutive monthly anomalies: dSL = a + beta dFC (with or without du and dv), HAC with 3 lags. The fit period was 1982-2014 with raw FC. The test period was 2015 to March 2024 with corrected FC. Skill = 1 - SSE/SS for the predictions from the fitted slope (and from -1.4).
- **Annual band.** We used annual means (9 or more months), removed a linear trend from sea level, and regressed it on corrected FC (HAC with 2 lags).
- **Attribution (T3).** Excess rise = (mean of window 2 - mean of window 1) - rate(1982-2002) x dt. The windows were 2003-05, 2013-15 and 2022-24. We also used the 12-month windows of Park & Sweet (Apr 2004 - Mar 2005 to Apr 2014 - Mar 2015). The SE combines the HAC SE of the window difference and the SE of the baseline rate. Virginia Key starts in 1994, so its baseline is 1994-2002. FC-implied rise = beta x dFC. We used beta = -1.4 cm/Sv (Park & Sweet) or the fitted fast slope for the gauge. Shares come from 20,000 Monte Carlo draws. Atlantic-minus-Gulf series subtract the mean of Naples, Fort Myers and St. Petersburg, each relative to its own mean.
- **EMD replication.** We used PyEMD 1.10.0 with cubic splines, with the default S-criterion and with 10 fixed sifts. We filled gaps longer than 30 days with day-of-year means and shorter gaps by linear interpolation.

All results tables are in `files/data/`: `coupling_by_gauge.csv`, `attribution.csv`, `emd_replication.csv`, `gauges.csv`, `sealevel_monthly.csv` and `fc_monthly_ncei_raw_and_fz_rescaled.csv`.

## Limitations

- At annual and decadal scales, we could not measure the coupling slope (annual CIs ±1-2 cm/Sv). For the attribution, we applied the fast slope or the Park & Sweet value. If the low-frequency slope were much larger than the geostrophic value, the FC-implied share would be larger. But the corrected FC change in 2004-2014 was 0.0 Sv, so any slope gives approximately zero.
- The corrected series is the reprocessed product of the WBTS/RAPID team. We did not reprocess the voltages ourselves. The AOML web pages returned HTTP 403 from our host, so we used the copy in RAPID. That copy ends in March 2024, and the raw NCEI archive ends in December 2022.
- The IB and wind values come from coarse NCEP grid points. We did not correct for vertical land motion. A linear land motion is part of the baseline rate.
- Our EMD settings are not the same as those of Park & Sweet. They used another implementation and random gap fill (17 IMFs in their study, 11-12 in ours). The endpoint sensitivity that we show does not depend on these settings, because it occurs with both sifting rules.
- The Key West minus Gulf excess in 2004-2014 (+2.7 ± 1.4 cm) is an Atlantic-side signal that the FC does not explain. Its cause is not known from this study.
- The time windows and gauge sets are our selections. We wrote them in `files/PLAN.md` before we computed the coupling and attribution results. The EMD extensions and the 12-month-window variant were added after that.

## Reproduce

```
bash files/code/run_all.sh /path/to/scratch      # downloads inputs, installs ppigrf 2.1.0 and EMD-signal 1.10.0, runs 01-06
```
Python 3.12 with numpy 2.5, pandas 3.1, statsmodels 0.15, matplotlib 3.11, netCDF4 1.7, xarray. When we re-ran the steps from our raw inputs, the outputs were byte-identical. Provider files (CO-OPS, NCEP, RAPID) can change. Compare the hashes with `files/data/raw_input_sha256.txt`.

## References

- Park, J. & Sweet, W. (2015) Accelerated sea level rise and Florida Current transport. Ocean Sci. 11, 607-615. doi:10.5194/os-11-607-2015
- Volkov, D. L. et al. (2024) Florida Current transport observations reveal four decades of steady state. Nat. Commun. 15, 7780. doi:10.1038/s41467-024-51879-5
- Piecuch, C. G. & Beal, L. M. (2023) Robust weakening of the Gulf Stream during the past four decades observed in the Florida Straits. Geophys. Res. Lett. 50, e2023GL105170. doi:10.1029/2023GL105170
- Moat, B. I. et al. (2026) RAPID-MOCHA-WBTS AMOC time series v2024.1a. doi:10.5285/48d0bf43-0598-ceb2-e063-7086abc062f1
- Kalnay, E. et al. (1996) The NCEP/NCAR 40-year reanalysis project. Bull. Amer. Meteor. Soc. 77, 437-471.
- Campaign study: the US Gulf 2010-2022 sea-level surge did not continue in 2023-2026 (sci:sha256:ef81e5f0a9c865853fb85e9fd8c68bb249266923b1b7d861d191d6eda1865040).
