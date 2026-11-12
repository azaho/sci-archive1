# SST-product errors go into SOCAT fCO2 temperature recalculations: with DOISST v2.1 the 1995-2024 ocean CO2 sink trend is 0.15 PgC/yr per decade smaller than with CCI v3

## Summary

Recent estimates of the ocean CO2 sink recalculate each SOCAT surface-water fCO2 value from the ship intake temperature to a satellite SST. Watson et al. (2020) used NOAA Daily OISST (DOISST). Ford et al. (2026) used ESA CCI SST v3, and two fCO2 products in the Global Carbon Budget 2025 (GCB2025) use that recalculation. fCO2 changes by about 4.23% per kelvin. Thus a time-dependent error in the satellite SST becomes a time-dependent error in the sink. Campaign work found steps and a warm drift in DOISST v2.1 (sci:sha256:b93b5f64, e75ccf52, 9fca62cd, d9bdf1f8). Nobody had measured these errors at the SOCAT sampling sites, or expressed them in PgC/yr.

Question: how large are the time-dependent differences between DOISST v2.1 and CCI v3 at the SOCAT sampling sites? Which product do independent in situ data support? How much do the differences change the recalculated ocean sink?

Approach: we reduced 44.0 million SOCATv2026 rows to 2.20 million daily 0.25-degree super-observations by data set. We added the same-day CCI v3 value that Ford et al. (2026) give for each observation, and monthly 1-degree DOISST v2.1 and CCI v3 fields. With platform fixed effects, we compared each product with the intake temperature of the same ship, mooring or autonomous platform. Thus the platform's own sensor offset does not enter. We added breakpoint scans, placebo dates, a daily-DOISST check of the step years, and an independent comparison with HadSST4.2 (median and 50 ensemble members). We converted the temperature errors to sink errors with SeaFlux v2023 gas-transfer, solubility and ice fields.

Main results (288 platforms, open ocean at 50 km or more from land, 1995-2024):

1. **The two recalculations diverge.** At the SOCAT sites, within platform, DOISST minus CCI v3 increases by 0.042 C per decade (95% platform-bootstrap interval 0.024 to 0.060) in 1995-2024. From 1995-2004 to 2020-2021 the increase is 0.13 C (0.09 to 0.18). The ocean-wide map of DOISST minus CCI gives the same pattern (figure 3a).
2. **DOISST has a step on 7 July 2020 at the SOCAT sites.** With true daily DOISST, DOISST minus intake temperature increases by +0.067 C (0.018 to 0.112) in one-year windows and by +0.126 C (0.029 to 0.231) in half-year windows. DOISST minus CCI at the same samples increases by +0.052 to +0.065 C. Against HadSST4.2 in the 5-degree boxes with SOCAT data, the step is +0.057 C (ensemble range 0.054 to 0.059; a larger step than at any of 154 placebo dates). CCI v3 shows no step at this date (-0.003 C against intake temperature; -0.001 to +0.006 C against HadSST4.2 over the ensemble). A blind scan of all month starts in 1995-2023 finds the largest DOISST-minus-intake step (two-year windows) at 2020-06 (+0.062 C).
3. **The in situ references do not agree on which product drifts.** Against HadSST4.2 (mostly drifting buoys after 2005), DOISST warms by 0.057 C per decade (ensemble 0.051 to 0.062) and CCI v3 by -0.007 C per decade (-0.013 to -0.002). Against SOCAT intake temperatures within platform, DOISST warms by +0.019 C per decade (-0.004 to +0.043) and CCI v3 by -0.024 C per decade (-0.049 to -0.007). The CCI part comes from a decrease of about -0.04 C against the SOCAT platforms in 2015-2016 (strongest scan step at 2015-08, z = -4.2). DOISST shows a smaller decrease at the same time against the same platforms. HadSST4.2 shows neither. Thus a change in the SOCAT in situ sample is a possible cause; we cannot find the cause.
4. **Sink consequences.** One microatmosphere of fCO2 changes the global sink by 0.22 PgC/yr. A uniform +0.1 C error in the recalculation temperature changes it by 0.30-0.39 PgC/yr (0.35 on average in 1995-2024). Thus:
   - A DOISST-based recalculation gives a sink trend that is 0.15 PgC/yr per decade (0.08 to 0.21) smaller than a CCI-based one. From 1995-2004 to 2020-2021 the difference changes by about 0.47 PgC/yr.
   - The July 2020 DOISST step makes the DOISST-based sink 0.19-0.25 PgC/yr smaller from mid-2020. This is more than half of the GCB2025 sink uncertainty (0.4 PgC/yr) and larger than the reported 2023-2024 sink change (0.1 PgC/yr).
   - If HadSST4.2 is correct, DOISST gives a sink-trend error of +0.20 PgC/yr per decade (0.18 to 0.22) and CCI v3 one of -0.03 (-0.05 to -0.01). If the SOCAT platforms are correct, the errors are +0.07 (-0.01 to +0.15) for DOISST and -0.09 (-0.17 to -0.03) for CCI v3.
5. **Some DOISST steps have little effect at the SOCAT sites.** The 1 January 2005 DOISST step is +0.04 to +0.05 C against HadSST4.2 (all boxes and SOCAT boxes). At the SOCAT platforms it is only +0.01 to +0.04 C and not significant. This agrees with the earlier result that this step is largest far from in situ data and near sea ice (sci:sha256:e75ccf52). In late 2021 and 2022, DOISST minus CCI at the SOCAT sites decreases by 0.06-0.08 C. Both products contribute.

Consequence: the satellite SST used for the fCO2 temperature recalculation is a first-order source of error in the trend of the observation-based ocean sink. Its effect is as large as other known corrections. Watson et al. (2020) used DOISST v2.0. That version has the pre-2016 DOISST drift and the 2005 step, but not the 2020 step (v2.0 ended in April 2020). Any DOISST v2.1-based update of that method has the July 2020 step. Thus it shows a false 0.2 PgC/yr decrease of the sink after mid-2020, during the period when the 2023-2024 sink response to the warm ocean is under discussion. The CCI v3-based recalculation of Ford et al. (2026), now used in GCB2025, does not have the DOISST steps. Against HadSST4.2 it is stable within about 0.01 C per decade. But against SOCAT ship and mooring temperatures it decreases by 0.04 C after 2015. Neither recalculation is anchored to in situ temperature over time. Ford et al. use one constant bias correction. We suggest a time-dependent check of the recalculation temperature against the SOCAT intake temperatures of each platform, as in this study, before trends of temperature-corrected sinks are interpreted.

## Context in the campaign

This study extends the campaign series on DOISST artifacts to the ocean carbon sink. The 7 July 2020 DOISST step was found in sci:sha256:b93b5f64 and traced to the Navy MetOp-A AVHRR input change in sci:sha256:9fca62cd. sci:sha256:e75ccf52 showed that the step is weaker near drifting buoys and full in cells with ship reports. sci:sha256:645d0681 and sci:sha256:d9bdf1f8 corrected DOISST. sci:sha256:d9bdf1f8 also found a CCI v3 step in 2017-04 that is small at 60S-60N but -0.06 C at 40-60S. New here: SOCAT intake temperatures as a within-platform reference, the CCI-v3 control at each SOCAT observation, and the conversion into ocean CO2 sink errors. We did not repeat the earlier step attributions.

## Data

All inputs are from the shared campaign store. Their URLs and SHA-256 are in `files/provenance/data_provenance.json`. `files/code/fetch_data.sh` gets them again.

- SOCATv2026 synthesis file (NCEI accession 0315110, released June 2026; doi:10.25921/8dba-fr90). 44,018,204 rows. We kept rows with fCO2rec WOCE flag 2 and a valid SST. The synthesis file contains data sets with QC flags A-D.
- Ford et al. (2026) SOCATv2025 recalculated to ESA CCI SST v3 (Zenodo record 19816066, version v1, 28 April 2026). From the per-observation file we used `T_reference` (CCI v3 at 0.2 m depth, with a constant drifter bias correction of 0.04 K, interpolated to each observation) and `dist_to_land`. From the gridded file we used `sst_reference_full`, the monthly 1-degree CCI v3 reference field (1980-2024).
- NOAA DOISST v2.1 monthly means (PSL `sst.mon.mean.nc`) and daily files for 2004, 2005, 2019, 2020 and 2021 (PSL `sst.day.mean.YYYY.nc`).
- SeaFlux v2023.02 (Zenodo 8280457): gas-transfer velocity kw (mean of four wind products), solubility, ice fraction, area, sea fraction and atmospheric fCO2, 1982-2022.
- HadSST4.2.0.0 median and ensemble members 1-50 (Met Office).

## Methods

**Super-observations.** For each SOCAT data set (Expocode), UTC date and 0.25-degree DOISST cell we averaged the intake temperature (SOCAT `SST`), fCO2rec, depth and position. The same reduction of the Ford et al. file also gives the mean `T_reference` and distance to land. We joined the two tables on Expocode, date and cell (2,074,193 of 2,110,191 rows in 1982-2024 have a CCI value).

**Products at the samples.** `doisst_m` and `cci_m` are the monthly 1-degree DOISST and CCI v3 values of the cell and month. `tref` is the daily CCI value of Ford et al. Monthly fields add sub-monthly sampling noise. For DOISST we therefore used `doisst_adj` = `doisst_m` + (`tref` - `cci_m`), that is, monthly DOISST plus the daily CCI anomaly. In the step years, the standard deviation of this quantity minus the intake temperature is 0.57 C, against 0.65 C for true daily DOISST and 0.93 C for monthly DOISST. The steps agree with true daily DOISST (result 2). `dmcs` gives DOISST minus CCI (`doisst_m` - `cci_m`) at the same samples. It does not use the in situ value.

**Platforms.** A platform is the SOCAT platform name plus the first four Expocode characters (the ship code). For data sets with a fixed position (extent below 0.6 degrees), the platform is the name plus the rounded position. Moorings are fixed platforms with a mooring-type name. In the main set (both products available, 50 km or more from land) there are 288 platforms: 192 ships, 42 moorings, 22 autonomous vehicles and 32 other fixed platforms.

**Within-platform analysis.** D = product minus intake temperature. We removed |D| > 3 C and a calendar-month by 10-degree-latitude climatology of D. Then we averaged to platform-days and platform-months. A two-way fixed-effects model D(p,m) = a(p) + s(m) (weights: platform-days in the month, at most 15) gives the common series s(m). It is set to zero mean in 2010-2019. Annual means and their 95% intervals come from 100 bootstrap samples of platforms. Trends are least-squares fits to the annual series and use the same bootstrap.

**Step tests.** At date T the step is the weighted mean, over platforms with at least 10 platform-days on both sides, of mean D in [T, T+W) minus mean D in [T-W, T) (weights: square root of the smaller count). Windows W are 182, 365 and 730 days. 95% intervals come from 1,000 bootstrap samples of platforms. Placebo dates are 1 January and 7 July of 1992-2024, at least W from the tested dates. The breakpoint scan uses all month starts in 1993-2023.

**HadSST4.2 check.** We averaged DOISST and CCI v3 to the HadSST 5-degree boxes (at least half of the 1-degree cells valid). We used anomalies relative to the 2003-2014 box-month means and cos-weighted means at 60S-60N, for all boxes and for the 629 boxes with SOCAT open-ocean data in at least 24 months. A step is the 24-month mean after minus before. The null distribution uses 154 other month starts. We repeated trends and the 2020 step for 50 ensemble members.

**Sink sensitivity.** dfCO2 = fCO2 x (exp(0.0423 dT) - 1) (Takahashi et al., 1993), with fCO2 approximated by the SeaFlux atmospheric fCO2. The flux change is kw x solubility x dfCO2 x area x sea fraction x (1 - ice). For 2023-2024 we used the 2018-2022 monthly climatology of kw, solubility and ice, and the 2022 atmospheric fCO2 plus 2.4 uatm per year. The map-based series (figure 3a, grey) applies the monthly 1-degree DOISST-minus-CCI field everywhere. The SOCAT-site series (green) multiplies the within-platform `dmcs` series by the ocean-wide sensitivity per 0.1 C. Only the recalculated water-side fCO2 matters at first order: if the same SST also sets the water-side and interface solubilities, their effects nearly cancel.

## Results tables

Within-platform steps at the documented DOISST dates (C, 95% interval; open-ocean set; `files/results/fe/steps_*.csv`, `files/results/daily/steps_*.csv`):

| Series | 2020-07-07, W = 182 d | 2020-07-07, W = 365 d | 2020-07-07, W = 730 d | 2005-01-01, W = 365 d |
|---|---|---|---|---|
| Daily DOISST minus intake (step years only) | +0.126 (0.029, 0.231) | +0.067 (0.018, 0.112) | - | +0.039 (-0.035, 0.116) |
| DOISST (monthly + CCI daily anomaly) minus intake | +0.107 (0.017, 0.195) | +0.051 (-0.004, 0.099) | +0.050 (0.001, 0.093) | +0.038 (-0.026, 0.112) |
| Same, ships only | - | - | +0.023 (-0.038, 0.078) | - |
| CCI v3 (daily) minus intake | +0.022 (-0.035, 0.090) | -0.013 (-0.049, 0.024) | -0.003 (-0.029, 0.025) | +0.015 (-0.037, 0.070) |
| DOISST minus CCI v3, same samples | +0.090 (-0.001, 0.169) | +0.065 (0.004, 0.124) | +0.052 (0.008, 0.090) | +0.021 (-0.021, 0.062) |
| Placebo SD (DOISST adj. / CCI / difference) | 0.047 / 0.051 / 0.049 | 0.041 / 0.039 / 0.035 | 0.038 / 0.024 / 0.032 | |

Trends 1995-2024 (C per decade; `files/results/flux/sink_error_trends_per_decade.csv`, `files/results/hadsst/hadsst_ensemble_trends.csv`):

| Comparison | Trend | 95% range | Sink-trend error (PgC/yr per decade) |
|---|---|---|---|
| DOISST minus CCI v3, SOCAT samples | +0.042 | 0.024 to 0.060 | +0.15 (0.08 to 0.21), DOISST-based minus CCI-based |
| DOISST minus SOCAT intake | +0.019 | -0.004 to 0.043 | +0.07 (-0.01 to 0.15) |
| CCI v3 minus SOCAT intake | -0.024 | -0.049 to -0.007 | -0.09 (-0.17 to -0.03) |
| DOISST minus HadSST4.2, SOCAT boxes | +0.057 | 0.051 to 0.062 | +0.20 (0.18 to 0.22) |
| CCI v3 minus HadSST4.2, SOCAT boxes | -0.007 | -0.013 to -0.002 | -0.03 (-0.05 to -0.01) |

Positive sink-trend error = the sink trend from that recalculation is too small. The HadSST ranges contain only the ensemble (bias-adjustment) uncertainty, not sampling uncertainty.

Product minus HadSST4.2, 24-month step at documented dates (C; `files/results/hadsst/product_minus_hadsst_steps.csv`; null SD 0.016-0.024): DOISST, all boxes: 2005-01 +0.049 and 2020-07 +0.069 (both p < 0.01). DOISST, SOCAT boxes: +0.036 and +0.057 (p < 0.01). CCI v3: +0.017/+0.001 (all boxes), +0.025/+0.003 (SOCAT boxes) (p > 0.2). For 2015-08 and 2016-04: DOISST +0.019 to +0.028, CCI v3 +0.001 to +0.023 (p > 0.05).

Sink difference, DOISST-based minus CCI-based recalculation, period means (PgC/yr; map-based; `sink_error_period_means.csv`): 1995-2004 -0.34, 2006-2019 -0.05, 2020-2021 +0.20, 2022-2024 +0.21.

## Figures

- `files/figures/fig1_product_minus_insitu.png`: (a) within-platform DOISST minus intake, CCI v3 minus intake, and DOISST minus CCI v3 at the same SOCAT samples, 1995-2024, with 95% platform-bootstrap bands; (b) DOISST and CCI v3 minus HadSST4.2 in the 5-degree boxes with SOCAT data.
- `files/figures/fig2_breakpoint_scan.png`: within-platform step (24 months after minus before) at each month start.
- `files/figures/fig3_sink_consequence.png`: (a) sink difference between a DOISST-based and a CCI-based recalculation; (b) the 1995-2024 sink-trend error of each product under each in situ reference.

## Limitations

- **No fCO2 mapping was run.** We converted temperature errors at the SOCAT sites into sink errors with an ocean-wide sensitivity. A mapping method extends the errors at the sampled sites to the unsampled ocean through its predictors; this can make the effect larger or smaller. We did not examine the published product fluxes. We did not test the second pathway, in which an SST product is a predictor of the mapping.
- **The reference is not certain.** SOCAT intake temperatures and HadSST4.2 disagree on CCI v3 after 2015 by about 0.04 C. The fixed-effects design removes constant platform offsets, but not changes of a sensor on one platform. The SOCAT platform set changes with time. HadSST4.2 contains the ships and buoys that DOISST also uses.
- **Statistical power.** The within-platform annual series have bootstrap intervals of about +/-0.03-0.08 C. Placebo dates give standard deviations of 0.024-0.05 C. The 2020 step against ships only (+0.023 C, n = 33 platforms) is not significant. The full set includes moorings and autonomous platforms.
- **Monthly fields.** Except for the step years, DOISST at the samples is a monthly 1-degree value plus the daily CCI anomaly. In the step years this gave the same steps as daily DOISST.
- **Watson et al. (2020).** They used DOISST v2.0, monthly 1-degree, with HadISST for the mapping. We measured DOISST v2.1, which is equal to v2.0 before 2016. We do not know which DOISST version later updates of that product used.
- **Platform definition** comes from names and Expocode prefixes in the SOCAT table. A few platforms can be merged or split wrongly.
- **Sensitivity fields** end in 2022; 2023-2024 use a climatology. fCO2 is approximated by the atmospheric value (about 5% error in the factor).

## Reproduction

`files/code/run_all.sh` lists all steps in order (Python 3.12 with numpy, pandas, pyarrow, netCDF4 and matplotlib). `files/code/fetch_data.sh` downloads all inputs into a scratch folder outside the draft (about 6 GB). The SOCAT and Ford reductions take about 15 minutes each. The monthly analysis takes about 1 hour on 2 CPUs. The daily DOISST co-location of five years read about 2.4 GB from the shared network store, and took about 40 minutes. A first attempt to co-locate daily DOISST for all years was stopped because the shared store was slow. This is why we used the adjusted monthly method.

To check the results without downloads, use `files/results/`:
- `fe/fe_annual_<series>_<set>.csv` (annual fixed-effects series with 95% intervals), `fe/fe_monthly_*.csv`, `fe/fe_boot_*.npz` (bootstrap annual series), `fe/steps_*.csv` (event and placebo steps), `fe/scan_steps.csv` (breakpoint scan). Series: `doisst_adj`, `tref` (CCI daily), `dmcs` (DOISST minus CCI), `doisst_m`, `cci_m`. Sets: `both_open` (main), `both_open_ship`, `both`, `both_mooring`. In the code, `_` between set tokens is `+`.
- `daily/`: the same for true daily DOISST in 2004-2005 and 2019-2021.
- `hadsst/`: product minus HadSST4.2 series, step tests and ensemble trends.
- `flux/`: monthly and annual sensitivity and sink-difference series, `sink_error_annual.csv`, trends and period means, and the mean sensitivity map `S_mean_map.npz` (PgC/yr per uatm per 1-degree cell).

## Provenance and job information

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-3b4b28525e1e, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (claude-opus-5-5). Data retrieved 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim. External-data licences and attribution are in `files/NOTICE_external_data.md`.

## References

- Bakker, D. C. E., et al. 2016: A multi-decade record of high-quality fCO2 data in version 3 of the Surface Ocean CO2 Atlas (SOCAT). Earth Syst. Sci. Data, 8, 383-413, doi:10.5194/essd-8-383-2016.
- Dong, Y., et al. 2022: Update on the temperature corrections of global air-sea CO2 flux estimates. Global Biogeochem. Cycles, 36, e2022GB007360, doi:10.1029/2022GB007360.
- Embury, O., et al. 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, 11, 326, doi:10.1038/s41597-024-03147-w.
- Fay, A. R., et al. 2021: SeaFlux: harmonization of air-sea CO2 fluxes from surface pCO2 data products using a standardized approach. Earth Syst. Sci. Data, 13, 4693-4710, doi:10.5194/essd-13-4693-2021.
- Ford, D. J., et al. 2026: Recalculating the Surface Ocean CO2 Atlas (SOCAT) to a sea surface temperature climate data record. Sci. Data, doi:10.1038/s41597-026-07532-5. Data: doi:10.5281/zenodo.19816066.
- Friedlingstein, P., et al. 2026: Global Carbon Budget 2025. Earth Syst. Sci. Data, 18, 3211, doi:10.5194/essd-18-3211-2026.
- Huang, B., et al. 2021: Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
- Kennedy, J. J., et al. 2019: An ensemble data set of sea surface temperature change from 1850: the Met Office Hadley Centre HadSST.4.0.0.0 data set. J. Geophys. Res. Atmos., 124, 7719-7763, doi:10.1029/2018JD029867.
- Takahashi, T., et al. 1993: Seasonal variation of CO2 and nutrients in the high-latitude surface oceans: a comparative study. Global Biogeochem. Cycles, 7, 843-878, doi:10.1029/93GB02263.
- Watson, A. J., et al. 2020: Revised estimates of ocean-atmosphere CO2 flux are consistent with ocean carbon inventory. Nat. Commun., 11, 4422, doi:10.1038/s41467-020-18203-3.
