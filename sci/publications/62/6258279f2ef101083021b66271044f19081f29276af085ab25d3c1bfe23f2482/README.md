# NCEP R1 and R2 lost 0.32-0.37 C of ocean surface temperature in steps after 11 February 2020; R1 global 2 m temperature is 0.2-0.27 C too cold in 2020-2026

Job: sci-1107-dell-earth-and-ocean-sciences-35bf82a92743. Topic: earth-and-ocean-sciences. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work showed that SST input changes put steps into DOISST v2.1 and OI SST v2, and that these steps reach AMIP model forcing. This study asks a different question: do the same SST inputs also put steps into atmospheric reanalyses? We tested the NCEP/NCAR Reanalysis 1 (R1), the NCEP-DOE Reanalysis 2 (R2) and CFSR/CFSv2. We compared their ocean skin temperature (the SST lower boundary) with three SST products (COBE-SST2, ERSSTv5, DOISST v2.1) on the same T62 grid. We then measured the effect on 2 m air temperature (T2m).

Main results:

1. **R1 and R2 have three cold SST steps after 2019.** Until 2019, R1 and R2 ocean skin temperature followed OI SST v2 (R2 monthly anomaly correlation 0.996, difference SD 0.017 C). Then, at 60S-60N, the R1 skin temperature fell against all references:
   - on 11-12 February 2020: -0.11 to -0.23 C (a one-day step in 6-hourly R1 data, Figure 1c);
   - in late November / early December 2022: -0.13 to -0.17 C. NOAA discontinued the 1-degree weekly OISST at NCEP on 5 December 2022;
   - in July 2023: -0.03 to -0.06 C.
   The total is -0.32 to -0.37 C against the in situ-based products (COBE-SST2, ERSSTv5) and -0.42 C against DOISST, which has its own +0.06 C step in July 2020. The steps occur in all latitude bands (Table 1). R2 has the same steps (-0.15, -0.15, -0.05 C against COBE-SST2). R1 and R2 also keep the July 2018 OI v2 Southern Ocean cold step (R1: -0.13 to -0.17 C at 40-60S). After 2022 the R1 ocean still follows ENSO (Nino-3.4 anomaly correlation 0.97), but it is 0.4 C too cold there. Thus the steps are offsets, not a frozen climatology. We found no public notice that documents these changes.

2. **R1 snow cover also broke in 2020.** From 2020, the R1 summer (June-August) snow-covered fraction of land north of 30N is 0.20-0.23, against 0.08-0.13 in 1990-2019. In January-February 2023 it falls to 0.16 (other years 0.74-0.89). Thus R1 land T2m is 2-3 C too cold in summer over northern Asia and the Arctic coasts, and too warm in winter 2022/23 (Figure 2). Against GHCN-CAMS station analysis, R1 land T2m is -0.43 C too cold in March 2020-August 2022 and -0.58 C too cold in July 2023-February 2026 (2011-2019: -0.05 C).

3. **The SST steps reach the air above the ocean.** Over ice-free ocean (60S-60N), R1 T2m fell 0.16 C relative to COBE-SST2 when the skin temperature fell 0.34-0.36 C. Thus about 45% of the SST step passes into ocean T2m in this analysis-constrained system.

4. **R1 global T2m is too cold and loses the recent records.** Relative to ERA5, the R1 global-mean T2m anomaly is -0.22 C (March 2020-August 2022) and -0.27 C (July 2023-February 2026); in 2011-2019 it is 0.00 C. Against NOAAGlobalTemp v6 the values are -0.19 and -0.22 C. In R1, 2016 stays the warmest year in 1979-2025; 2024 is second, 2023 third and 2020 is tenth (ERA5: 2024 first, 2023 second, 2020 fifth). With the fitted steps removed, R1 ranks 2024 first. R2 global T2m is also 0.09-0.27 C too cold (annual means) after 2019; in R2, 2024 is only 0.01 C above 2016.

5. **CFSR/CFSv2 follows DOISST and keeps its steps, but its T2m changes less.** CFSR skin temperature follows DOISST v2.1 (1982-2010 anomaly correlation 0.991, difference SD 0.024 C) and keeps the January 2005 DOISST warm step (+0.05 to +0.06 C against in situ products; DOISST +0.06 to +0.07 C). CFSv2 has a cold step in December 2022 (-0.08 to -0.16 C) and July 2023 (-0.02 to -0.06 C), so its 60S-60N skin temperature is 0.11-0.20 C too cold after 2023. Only about one third passes into CFSv2 ocean T2m (-0.05 C), and CFSv2 global T2m shows no net step against ERA5 (+0.05 and -0.08 C at the two dates). Thus these two steps do not change the CFS daily global T2m series much (Climate Reanalyzer used CFS until 2023-2024). The large CFSR-to-CFSv2 splice in 2011 is a different, known problem.

Why this matters: R1 is one of the most used climate datasets. Many indices, web plotting tools and studies use its surface fields after 2020. Its 2020-2026 surface temperatures, and quantities that depend on air-sea temperature contrast, must not be used for trends or records without correction. The result also extends the campaign finding that SST input artifacts reach model boundary conditions: here the same NCEP SST supply chain reaches reanalyses, and the post-2019 breaks are larger than the DOISST and OI v2 steps found before.

## Figures

- `files/figures/fig1_sst_breaks.png`: R1 (and R2) and CFS ocean skin temperature minus three SST products, 60S-60N, 2008-2026; daily detail of the 11 February 2020 R1 break.
- `files/figures/fig2_maps_snow.png`: maps of the R1 SST changes at the 2020 and 2022-23 breaks; R1 summer land T2m error; R1 snow-covered fraction north of 30N.
- `files/figures/fig3_global_t2m.png`: annual global T2m anomalies in R1, R2, CFS, ERA5 and NOAAGlobalTemp; decomposition of the R1 deficit into land and ocean parts.

## Table 1. Total SST step (sum of the fitted steps) in reanalysis skin temperature minus reference SST (C)

Fit: monthly difference = constant + annual and semi-annual harmonics + step terms (R1: February 2020 with weight 18/29 in the step month, December 2022, July 2023; CFSv2: December 2022, July 2023). Windows: R1 2011-01 to 2026-02; CFSv2 2011-04 to 2025-02. Newey-West (12-month) standard errors for single steps are 0.005-0.03 C (`files/data/sst_step_fits.csv`). Values with a linear trend term are in `files/data/sst_step_totals.csv`.

| Region (ice-free ocean) | R1 - COBE2 | R1 - ERSSTv5 | R1 - DOISST | CFS - COBE2 | CFS - ERSSTv5 | CFS - DOISST |
|---|---|---|---|---|---|---|
| 60S-60N | -0.34 | -0.37 | -0.42 | -0.15 | -0.18 | -0.20 |
| 20N-60N | -0.37 | -0.43 | -0.48 | -0.15 | -0.21 | -0.23 |
| 20S-20N | -0.31 | -0.35 | -0.37 | -0.10 | -0.14 | -0.14 |
| 20S-40S | -0.32 | -0.34 | -0.39 | -0.15 | -0.17 | -0.20 |
| 40S-60S | -0.43 | -0.43 | -0.53 | -0.28 | -0.25 | -0.34 |

With a trend term, the R1 totals are -0.27 to -0.44 C and the CFS totals are -0.08 to -0.19 C in all regions.

## Table 2. Mean anomaly differences (C, anomalies relative to 1991-2020)

| Quantity | 2011-04..2019-12 | 2020-03..2022-08 | 2023-07..2026-02 |
|---|---|---|---|
| R1 global T2m - ERA5 | -0.00 | -0.22 | -0.27 |
| R1 global T2m - NOAAGlobalTemp | +0.01 | -0.19 | -0.22 |
| R1 land T2m - GHCN-CAMS (60S-60N land) | -0.05 | -0.43 | -0.58 |
| R1 ocean T2m - COBE-SST2 | +0.00 | -0.10 | -0.16 |
| R1 ocean skin - COBE-SST2 | -0.02 | -0.16 | -0.36 |
| CFS global T2m - ERA5 | -0.13 | -0.10 | -0.14 |
| CFS ocean skin - COBE-SST2 | +0.00 | +0.01 | -0.14 |

Annual values and ranks: `files/data/annual_global_t2m_ranks.csv`.

## Methods

- **Reanalysis fields.** CFSR (1979-01 to 2011-03) and CFSv2 (2011-04 to 2026-10, with gaps in 2025-2026 where NCEI has no file) monthly-mean low-resolution flux files `flxl06` (T62 Gaussian grid, 192 x 94) from NCEI THREDDS: surface temperature, 2 m temperature, land mask, ice cover, fluxes. R1 and R2 monthly means (skt, air.2m, icec, weasd) and R1 6-hourly skt for 2019, 2020, 2022 and 2023 from NOAA PSL. All are on the same T62 grid.
- **SST references.** COBE-SST2 (JMA), ERSSTv5 and DOISST v2.1 monthly means, and OI SST v2 1-degree monthly (to January 2023). We binned each product onto the T62 grid (cosine-latitude weighted mean of source cells; cell valid if more than 50% of its area is valid).
- **Mask.** Ice-free ocean: T62 ocean cell, ice cover below 0.01 in every month of CFS and R1 (R2 below 0.11 because its ice field has a 0.1 floor), and all three SST products valid in 1990-2022. Area-weighted means for 60S-60N and five bands.
- **Step fits.** OLS on step dummies, harmonics and (as a test) a linear trend, with Newey-West standard errors (lag 12). The step dates come from the daily R1 data (11 February 2020), from the NOAA notice (weekly OISST end, December 2022) and from visual inspection (July 2023). The July 2023 step may partly be a weaker response to the 2023 El Nino warming (regression slope 0.78-0.91 after 2022) and not a step.
- **2 m temperature.** Global means of reanalysis T2m against the ERA5 daily global series (Copernicus Climate Pulse, monthly averages) and NOAAGlobalTemp v6.0.0 gridded anomalies (5-degree, area-weighted). Land T2m against GHCN-CAMS (binned to T62). Ocean T2m against COBE-SST2 over the ice-free ocean mask.
- **Snow.** R1 snow water equivalent above 1 kg m-2 counts as snow-covered.
- **Corrected ranks.** We removed the three fitted steps of (R1 - ERA5) global T2m from R1 and ranked annual means again.

## Limitations

- We do not know what NCEP changed on 11 February 2020 or what supplied the SST after December 2022. The cause attribution is by date and pattern only. The snow problem may share a cause with the 2020 SST change (both start in February-March 2020), but we did not test the snow input directly.
- The references are not perfect. DOISST has its own +0.06 C step in July 2020 (so R1 - DOISST overstates the R1 step). COBE-SST2 and ERSSTv5 agree within 0.05 C.
- ERA5 and NOAAGlobalTemp are references, not truth. ERA5 SST may have a small step near October 2020 (earlier campaign work). This changes the R1 numbers by less than 0.03 C.
- The T2m step fits for land are disturbed by the 2022/23 snow-loss episode. The period means in Table 2 are more robust than the single-step land coefficients in `t2m_step_fits.csv`.
- The effect on surface turbulent heat fluxes was not resolved: R1 minus CFS latent plus sensible flux at 60S-60N shows no clear step in February 2020 (+0.2 +/- 0.9 W m-2) and a -2.0 +/- 0.5 W m-2 change in July 2023, but CFS has its own changes.
- We used monthly means for CFS and R2. We did not test R2 snow or land T2m.
- CFSv2 monthly files for March and May-December 2025 and some 2026 months are missing at NCEI; the CFS fits stop in February 2025.
- R1 production stopped on 17 March 2026 (PSL notice), so the R1 record ends in early 2026.

## Reproduction

1. `files/code/get_data.sh WORKDIR DATASETS_DIR` downloads all external data into a scratch tree outside this publication (CFS from NCEI, R1/R2 from PSL, ERA5 series from Copernicus Climate Pulse, NOAAGlobalTemp from NCEI, one Climate Reanalyzer series). The shared SST and GHCN-CAMS files must be placed in `DATASETS_DIR` from the source URLs in `files/provenance/shared_datasets_provenance.json` (with sha256).
2. Make a Python 3.12 environment with numpy, pandas, xarray, netCDF4, matplotlib, eccodes and eccodeslib (pip). Run `files/code/run_all.sh` from `WORKDIR/code`. Runtime is about 10 minutes on 1 CPU after download (CFS GRIB extraction about 3 minutes).
3. Hashes of the files we used: `files/provenance/cfs_flxl06_sha256.txt` (560 CFS files), `files/provenance/downloads_sha256.txt` (R1, R2, ERA5 series, NOAAGlobalTemp, R1 6-hourly skt, Climate Reanalyzer OISST series), `files/provenance/shared_datasets_provenance.json` (shared campaign datasets, with the exact paths under /mnt/dell-data/shared_datasets). Products that are still updated (ERA5 series, R1/R2 monthly files) can change after 11 November 2026.

Derived data in `files/data/`:
- `regional_monthly_ocean_skin_sst.csv`: monthly ice-free-ocean means (5 regions) of CFS, R1 skin temperature and the three SST products.
- `monthly_anomalies_1991_2020.csv`: monthly anomaly series used for Table 2 and Figure 3.
- `sst_step_fits.csv`, `sst_step_totals.csv`, `t2m_step_fits.csv`, `regime_table.csv`, `summary.json`: fit results and headline numbers.
- `r1_daily_sst_60S60N.csv`: daily R1 skin temperature and ERA5 SST means, 60S-60N (2019, 2020, 2022, 2023).
- `r2_series.csv`, `annual_global_t2m_ranks.csv`, `r1_minus_cfs_turbulent_flux_60S60N.csv`.

External data terms and attribution: see `files/NOTICE.md`. No raw third-party data files are in this bundle.
