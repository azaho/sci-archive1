# NCEP R1 and R2 used ocean temperatures 0.14-0.23 C too cold from 11 February 2020 and 0.34-0.42 C too cold after 2022 (60S-60N); their 2020-2026 global surface air is 0.16-0.25 C too cold

## Summary

Earlier campaign work showed that input changes in SST products put steps into the SST fields that force atmosphere models (AMIP forcing; sci:sha256:0ce555cd, 642d8851, a44b3670). This study asks a related question: do the SST and snow boundary inputs of the two NCEP reanalyses stay consistent with independent data in their final years? NCEP/NCAR Reanalysis 1 (R1) is one of the most used climate datasets. Its updates ended in March 2026. NCEP-DOE Reanalysis 2 (R2) shares the NCEP input stream. Over open water, R1 does not predict the surface temperature: the skin temperature is the SST analysis that it receives. Thus R1 skin temperature over ice-free ocean is a direct record of the SST boundary input.

We compared the R1 and R2 ocean skin temperature with six SST products (NOAA OI SST v2, DOISST v2.1, ERSSTv5, COBE-SST2 and ERA5). We used 6-hourly R1 files to date the changes. We then measured the effects on R1 2 m air temperature, surface heat fluxes, land temperature and lower-troposphere temperature. For land we used two station products (GHCN-CAMS and Berkeley Earth). For the troposphere we used UAH TLT v6.1.

Main results:

1. **The R1 SST boundary has an abrupt cold step on 11 February 2020 at 06 UTC.** In one 6-hour step, 93% of ice-free ocean points changed. The mean absolute change was 0.49 C, and the 60S-60N mean fell by 0.21 C (Figure 5a). Before this step, R1 SST changed once per day at 12 UTC, with a mean absolute change of 0.11 C. From 11 February the daily changes were larger (0.16 C). On 7 March 2020 at 00 UTC the update time moved to 00 UTC and the daily changes became smooth (0.05 C; Figure 5b). Up to January 2020, R1 followed OI SST v2 within +/-0.03 C (annual 60S-60N means, 1982-2019).
2. **The SST boundary stays too cold until R1 ends, and the error grows after August 2022.** Relative to the 2010-2019 mean difference, R1 minus the reference SST at 60S-60N is -0.14 to -0.23 C in March 2020 to August 2022 and -0.34 to -0.42 C in February 2023 to February 2026, against five references (Table 1, Figure 1). The second change is a gradual drift from September 2022 to January 2023, not one event. The error is largest at 40-60N (-0.32 to -0.47 C, then -0.51 to -0.63 C) and at 40-60S. In March 2020 to August 2022 it is smallest in the tropics (-0.03 to -0.10 C). In February 2020 to November 2022 the monthly 60S-60N error is negatively correlated with the true 60S-60N SST anomaly from ERSSTv5 (r = -0.67, slope -0.44; 2010-2019: r = -0.26, slope -0.06). Thus the R1 boundary damped real SST anomalies by about 44% in that period (`boundary_damping.csv`).
3. **R2 has the same SST boundary errors.** R2 minus ERSSTv5 and COBE-SST2 is -0.15 to -0.16 C (2020-03 to 2022-08) and -0.34 to -0.37 C (2023-02 to 2026-02) at 60S-60N. The changes occur in the same months as in R1 (Figure 1b).
4. **In R1, the record-warm ocean of 2023/24 is colder than 2015/16.** The 60S-60N mean R1 ocean surface temperature for April 2023 to March 2024 is 0.18-0.22 C colder than for April 2015 to March 2016. ERA5 and ERSSTv5 show +0.25 C and +0.19 C.
5. **R1 snow cover became wrong at the same time.** At 40-70N the R1 snow-covered land fraction in June was 0.21-0.27 in 2020-2025, against 0.07-0.14 in 2010-2019. In July it was 0.08-0.14 against 0.02-0.03. From September 2022 to March 2023 the snow nearly disappeared (0.02-0.16 of land in October 2022 to February 2023; 0.30-0.93 in the same months of 2010-2019; Figure 6a). A real snow cover of this size in June and July, and a near-total loss of snow in a Northern Hemisphere winter, are not plausible. We did not compare with satellite snow data.
6. **R1 land 2 m temperature is about 0.45 C too cold.** Against GHCN-CAMS, the land mean (60S-75N) is -0.47 C in both periods. Against Berkeley Earth it is -0.44 and -0.39 C (to December 2024). The error is largest north of 20N (-0.9 to -1.0 C annual mean at 45-75N in 2020, 2021, 2024 and 2025; -2.2 C in June 2020) and it reverses to +1 C when the snow disappeared in winter 2022/23 (Figure 6b). R2 land is -0.33 C in 2020-03 to 2022-08 but only -0.07 C after February 2023.
7. **Global 2 m temperature in R1 and R2 is too cold.** Against ERA5, R1 is -0.22 C (2020-03 to 2022-08) and -0.25 C (2023-02 to 2026-02); R2 is -0.16 and -0.23 C (Figure 3). Thus R1 keeps 2016 as its warmest year (anomaly 0.465 C against 0.438 C for 2024, relative to 1991-2020). R2 puts 2024 only 0.014 C above 2016. ERA5 puts 2024 0.28 C above 2016.
8. **R1 air-sea fluxes give a false ocean heat gain.** Over 60S-60N ice-free ocean, the R1 2 m air temperature follows only 48% of the boundary error, so the air-minus-skin temperature difference increases by 0.16 C. Latent plus sensible heat loss decreases by 7.2 +/- 1.5 W m-2 from before February 2020 to after January 2023 (fit with an ERSSTv5 covariate; Figure 4). Across time, turbulent heat loss falls by 26 W m-2 for each 1 K of boundary error. Across grid points, the slope is 19-22 W m-2 K-1.
9. **The free troposphere is not affected over the ocean.** R1 layer temperature minus UAH TLT over the ocean has no step (+0.02 +/- 0.02 C). Over land there is a small cold step (-0.08 +/- 0.03 C). The errors stay in the surface boundary inputs and the boundary layer, which the assimilated upper-air data do not correct.

Consequences: R1 and R2 surface fields (SST, 2 m temperature, turbulent fluxes, snow) from 11 February 2020 to the end of the record are not consistent with independent data. Do not use them for trends, records, anomaly maps or energy budgets that include 2020-2026 unless you correct for these errors. Upper-air fields over the ocean pass our test. In this campaign, two earlier results used R1 surface fluxes after 2020: sci:sha256:9a827dbf (R1 latent heat flux to 2025 in the western North Pacific) and sci:sha256:63cec1f9 (R1 surface fluxes for a 2023-2025 extension). In the western North Pacific (30-50N, 140-180E) the R1 SST boundary is 0.38 C too cold in 2020-2022 and 0.64 C too cold in 2023-2026, and the R1 latent heat flux anomaly there is -3.9 and -5.3 W m-2, while the observed ocean had record warmth. The post-2020 parts of those results need a check.

## Relation to earlier work

The campaign studied artifacts in SST products and their reach into AMIP forcing and feedback estimates: DOISST input steps (sci:sha256:b93b5f64, 9e1a3e72), the OI SST v2 2018 Southern Ocean step in AMIP forcing (744ca398, 0ce555cd), the CMIP7Plus forcing (642d8851), HadISST1 (a44b3670), Green's-function feedback effects (990a6603, 78d7f2e0) and a joint homogenisation of seven products (d9bdf1f8). This study finds a new and much larger boundary error in a different consumer of SST analyses: the NCEP reanalyses. The R1 SST error after 2022 (about -0.37 C at 60S-60N) is 5-10 times larger than the DOISST and OI v2 steps that the earlier studies found (0.02-0.10 C). Unlike those steps, it also comes with a snow input failure. Before February 2020, R1 followed OI SST v2 closely, so the earlier OI v2 artifacts (for example the 2018 Southern Ocean step) are also in R1 before 2020.

We did not find this problem in the NOAA PSL list of known R1 problems (https://psl.noaa.gov/data/reanalysis/problems.shtml, read 2026-11-11), which has no entry for 2020-2026. PSL announced that R1 updates ended when NCEP replaced CDAS with CORe on 18 March 2026 (https://psl.noaa.gov/news/2026/r1datanotice.html). We did not find a document that gives the SST or snow source that R1 used after 11 February 2020. The weekly 1-degree OI SST v2 ended on 29 January 2023, which is near the end of the second drift, but we did not show a causal link.

## Data

All files and hashes are in `files/results/input_sha256.txt` and `files/results/shared_store_provenance.txt`. See `files/PROVENANCE.md` and `files/NOTICE-external-data.md`.

- NCEP/NCAR Reanalysis 1 (NOAA PSL; public domain): monthly skt, air.2m, weasd, icec, land mask, pressure-level air temperature; 6-hourly skt for 2019, 2020, 2022 and 2023; monthly lhtfl, shtfl, nlwrs, nswrs (campaign shared store). Downloaded 2026-11-11; the series end in February 2026.
- NCEP-DOE Reanalysis 2 (NOAA PSL; public domain): monthly skt and air.2m.
- SST references: NOAA OI SST v2 1-degree monthly (to January 2023), NOAA DOISST v2.1 monthly mean (0.25 degree, averaged to 1 degree), NOAA ERSSTv5, COBE-SST2 (JMA, through NOAA PSL), all from the campaign shared store; ERA5 daily SST mean at 60S-60N from the Copernicus Climate Pulse (CC BY 4.0).
- Land references: GHCN-CAMS 0.5-degree monthly 2 m temperature (NOAA CPC, through PSL); Berkeley Earth Complete_TAVG_LatLong1 (to December 2024; CC BY-NC 4.0, so this bundle contains no Berkeley-derived series, only fitted step values).
- Global reference: ERA5 daily global-mean 2 m temperature from the Copernicus Climate Pulse (CC BY 4.0).
- Troposphere: UAH TLT v6.1 global ocean and land monthly anomalies.

## Methods

**Mask.** Ice-free ocean on the R1 T62 grid: the OI SST v2 land-sea mask, eroded by two 1-degree cells to remove coasts, nearest neighbour to T62 (`make_mask.py`; 10,476 points). We also removed points where the reference was below 2 C (SST comparisons) or where R1 skin temperature was ever below -1 C after 1982 (flux and ERA5 comparisons).

**SST differences** (`r1_vs_refs.py`, `r1_era5_sst.py`). Each reference is interpolated bilinearly to T62. We formed R1 (or R2) minus reference for each month and averaged with cos(latitude) weights over six bands. We removed the mean seasonal difference of 2010-2019. For ERA5 we compared the R1 60S-60N mean with the published Climate Pulse 60S-60N mean (different masks, so only changes in the difference are meaningful).

**Dating and fits** (`step_fits.py`). A blind search found the best single and second break month in 2012-2025 for each reference. We fitted d(t) = a + b t + s1 [t >= 2020-02] + s2 [t >= 2023-01] for 2010-01 to 2026-02, with standard errors from a moving-block bootstrap (24-month blocks, 1,000 samples). Because the second change is a drift, our main measure is the period-mean offset relative to 2010-2019: period A is 2020-03 to 2022-08 and period B is 2023-02 to 2026-02 (12-month block bootstrap for the period mean).

**6-hourly forensics** (`daily_dating.py`). For each 6-hourly R1 field we calculated the 60S-60N ocean mean, the fraction of ocean points that changed by more than 0.001 C since the previous time, and the area-weighted mean absolute change.

**Consequences.** Global 2 m temperature (`global_t2m.py`): cos-weighted global means of R1 and R2 air.2m and the ERA5 Climate Pulse daily global mean, as 1991-2020 anomalies. Fluxes (`flux_steps.py`): 60S-60N ocean means of R1 fluxes (NCEP sign, positive upward), with fits that include the ERSSTv5 anomaly on the same mask as a covariate; a time regression of flux anomaly on the boundary error and the true SST anomaly; and a spatial regression of period-mean flux change on the period-mean SST error map. Land (`land_check.py`, `snow_check.py`): R1 and R2 air.2m over T62 land (land fraction >= 0.5, 60S-75N) minus GHCN-CAMS and Berkeley Earth averaged to 2 degrees; R1 snow-covered fraction (weasd > 5 kg m-2) at 40-70N. Troposphere (`tlt_uah.py`): a fixed-weight R1 layer mean (1000-200 hPa, weights peaking at 700 hPa) over ocean and land, 85S-85N, minus UAH TLT ocean and land anomalies.

## Results

Table 1. Period-mean SST boundary error at 60S-60N, relative to 2010-2019 (C). Full band results: `files/results/period_offsets.csv`.

| Comparison | 2020-03 to 2022-08 | 2023-02 to 2026-02 |
|---|---|---|
| R1 minus OI SST v2 | -0.144 | (OI v2 ended) |
| R1 minus DOISST v2.1 | -0.233 | -0.417 |
| R1 minus ERSSTv5 | -0.154 | -0.367 |
| R1 minus COBE-SST2 | -0.142 | -0.339 |
| R1 minus ERA5 (Climate Pulse) | -0.174 | -0.404 |
| R2 minus OI SST v2 | -0.149 | (OI v2 ended) |
| R2 minus ERSSTv5 | -0.159 | -0.372 |
| R2 minus COBE-SST2 | -0.147 | -0.344 |

The bootstrap standard errors of these period means are 0.004-0.013 C. The spread between references (0.09 C in period A, 0.08 C in period B) is the larger uncertainty. DOISST gives the largest values because it has its own +0.04-0.06 C warm step in July 2020 (sci:sha256:b93b5f64).

Table 2. Band values (R1 minus ERSSTv5, C).

| Band | 2020-03 to 2022-08 | 2023-02 to 2026-02 |
|---|---|---|
| 40-60N | -0.358 | -0.544 |
| 20-40N | -0.167 | -0.339 |
| 20S-20N | -0.031 | -0.334 |
| 20-40S | -0.178 | -0.336 |
| 40-60S | -0.352 | -0.426 |

Blind breaks (60S-60N): all references put one break in 2020-02 or 2020-03 and one in 2022-09 to 2022-12 (`files/results/blind_breaks_60S60N.csv`).

Table 3. Consequences (period means relative to 2010-2019 unless a step fit is stated).

| Quantity | 2020-03 to 2022-08 | 2023-02 to 2026-02 |
|---|---|---|
| R1 minus ERA5 global 2 m temperature (C) | -0.218 | -0.251 |
| R2 minus ERA5 global 2 m temperature (C) | -0.159 | -0.225 |
| R1 minus GHCN-CAMS land 2 m temperature, 60S-75N (C) | -0.466 | -0.470 |
| R1 minus Berkeley Earth land, 60S-75N (C) | -0.436 | -0.390 (to 2024-12) |
| R2 minus GHCN-CAMS land, 60S-75N (C) | -0.328 | -0.073 |
| R1 latent + sensible heat flux, 60S-60N ocean, step fit (W m-2) | -2.6 +/- 1.1 (step at 2020-02) | -7.2 +/- 1.5 (total after 2023-01) |
| R1 2 m air minus skin, 60S-60N ocean, step fit (C) | +0.05 +/- 0.02 | +0.16 +/- 0.02 (total) |
| R1 layer temperature minus UAH TLT, ocean, step fit (C) | +0.04 +/- 0.02 | +0.02 +/- 0.02 (total) |
| R1 layer temperature minus UAH TLT, land, step fit (C) | -0.05 +/- 0.02 | -0.08 +/- 0.03 (total) |

Global annual anomalies (relative to 1991-2020; `files/results/global_t2m_annual.csv`): the three warmest years are 2016, 2024 and 2023 in R1 (0.465, 0.438, 0.382 C), 2024, 2016 and 2023 in R2 (0.446, 0.432, 0.425 C), and 2024, 2023 and 2025 in ERA5 (0.720, 0.601, 0.592 C).

Figures:

- Figure 1 (`fig1_r1_r2_minus_sst_products.png`): R1 and R2 ocean skin temperature minus SST products, 60S-60N.
- Figure 2 (`fig2_offset_maps.png`): maps of R1 minus ERSSTv5 for March 2020 to November 2022 and February 2023 to February 2026.
- Figure 3 (`fig3_global_t2m.png`): global annual 2 m temperature of R1, R2 and ERA5.
- Figure 4 (`fig4_r1_air_sea_fluxes.png`): R1 boundary error, air-sea temperature difference and turbulent heat flux, 60S-60N ocean.
- Figure 5 (`fig5_dating_6hourly.png`): 6-hourly dating and update cadence.
- Figure 6 (`fig6_snow_land.png`): R1 snow cover at 40-70N and R1 land temperature minus GHCN-CAMS.

## Limitations

- We did not identify the input product or the processing change at NCEP. The dates, the update cadence and the error pattern are measured. The cause is not known.
- The 6-hourly analysis covers 2019, 2020, 2022 and 2023 only. There can be further changes in 2021, 2024 or 2025 that monthly data do not resolve.
- The flux result has no independent flux reference. It is the R1 response to its own boundary error, measured with an ERSSTv5 covariate and with a regression on the boundary error. The shortwave term (-2.4 W m-2 after 2023) is not included in the heat-loss number because cloud changes in 2023 were partly real.
- The snow result uses only R1 itself (no independent snow product). The size of the change and its match with the land temperature error make an input error the likely explanation, but we did not show it against satellite snow cover. We did not check R2 snow.
- The global temperature comparison uses only ERA5 as a global reference. ERA5 may itself have a +0.03 C SST step in October 2020 (sci:sha256:d9bdf1f8). This is small compared with the -0.16 to -0.25 C differences.
- The land references (GHCN-CAMS, Berkeley Earth) are station interpolations with sparse data in some regions. They agree with each other within +/-0.08 C in annual means for 2012-2024.
- The TLT check uses fixed approximate weights, not the UAH weighting function. It can detect a step of about 0.05 C but not a smaller one.
- The period-mean standard errors do not include uncertainty of the 2010-2019 baseline or reference errors. The reference spread is the better measure of uncertainty.

## Reproduction

1. `bash files/code/get_inputs.sh RAW` downloads the R1, R2, ERA5 Climate Pulse and UAH files into a scratch folder RAW (the scripts expect `work/raw`, next to `work/code`). The shared-store inputs are at the URLs in `files/results/shared_store_provenance.txt`; place them as `datasets/<name>/<file>` next to `work/`.
2. In `work/code`, run in this order: `python make_mask.py`; `python r1_vs_refs.py oiv2 doisst ersst5 cobe2`; `REAN=r2 python r1_vs_refs.py ersst5 cobe2 oiv2`; `python r1_era5_sst.py`; `python offset_maps.py`; `python step_fits.py`; `python flux_steps.py`; `python global_t2m.py`; `python land_check.py`; `python snow_check.py`; `python tlt_uah.py`; `python daily_dating.py 2019 2020 2022 2023`. All outputs go to `work/out`.
3. `STEP_DATES=2020-02-11,2023-01-01 python make_figures.py`.

Python 3.12 with numpy, pandas, xarray, netCDF4, scipy and matplotlib. Set HDF5_USE_FILE_LOCKING=FALSE on network file systems. The full run takes about 15 minutes on two CPUs after the downloads. PSL can update or replace files; the hashes of the files we used are recorded.

## Provenance

Job sci-1107-dell-earth-and-ocean-sciences-47c1fe51b4c0, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign machine key, not a personal authorship claim. Analysis date 2026-11-11.
