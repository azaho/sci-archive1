# Oxygen on the 26.5 isopycnal in the core CalCOFI grid stopped its 1984-2006 decline and stayed low through 2025

## Summary

From 1984 to 2006, oxygen fell in the subsurface southern California Current (Bograd et al., 2008). Three published views give three different expectations for later years:

1. The linear 1984-2006 decline continues.
2. Oxygen follows the salinity ("spice") of the source water on the isopycnal. Pozo Buil and Di Lorenzo (2017) used isopycnal salinity as a proxy for oxygen. They predicted "a new period of strong decline in oxygen by 2020".
3. Oxygen has multidecadal fluctuations, so it can recover.

We tested these expectations with independent data that are later than the papers. We used the CalCOFI bottle database (1949-03 to 2021-05) and the bottle rows in the CalCOFI CTD product files (2021-07 to 2025-04). We used only Winkler bottle oxygen. The analysis uses 57 core stations that CalCOFI sampled in at least 115 cruises after 1984. It contains 9,705 casts and 169 cruise means from 1984 to 2025. The training period is 1984-2006. The test period is 2007-2025.

Main results (annual means of anomalies from the 1984-2006 station x season climatology, all 57 stations):

- **The decline stopped, but oxygen did not recover.** On sigma0 = 26.5 kg/m3, oxygen fell at -1.04 umol/kg per year in 1984-2006 (95% HAC interval -1.39 to -0.69). In 2007-2025 the slope was +0.10 umol/kg per year (-0.08 to +0.28). The mean anomaly in 2007-2025 was -16.2 umol/kg. The extended 1984-2006 trend gave a 2025 value of -31.2 umol/kg, and its forecast RMSE was 8.7 umol/kg. A forecast that holds the 2002-2006 level gave an RMSE of 3.9 umol/kg. This difference in loss is marginal: the 95% block-bootstrap interval of the loss difference is 0.9 to 122. It includes zero if we remove 2023 or stop in 2020.
- **There was no new strong decline by 2020.** The 2018-2025 mean oxygen on sigma0 = 26.5 was 1.8 umol/kg higher than the 2008-2017 mean (0.1 to 3.5; without 2023: -0.4 to 3.0). The depth of the 60 umol/kg hypoxic boundary was 11 m deeper in 2018-2025 than in 2008-2017 (2 to 21 m). The hypoxic boundary was shallowest in 2011-2013, about 50-65 m shallower than the 1984-2006 mean.
- **The isopycnal-salinity proxy failed after 2006.** In 1984-2006, annual oxygen and salinity on sigma0 = 26.5 had r = -0.92 (slope -360 umol/kg per psu). In 2007-2025, r = -0.15. Salinity went back toward its 1984-2006 mean after 2010, but oxygen stayed low. The observed oxygen was 11.5 umol/kg below the proxy prediction (95% interval -14.4 to -9.6). The proxy forecast (RMSE 12.2) was worse than the held 2002-2006 level (RMSE 3.9). The same result occurs on sigma0 = 26.7, nearshore and offshore, without 2023, and in the bottle database alone (to 2020).
- **The oxygen loss is an AOU gain with a phosphate gain at the remineralization ratio.** From 1984-1995 to 2008-2025, oxygen on sigma0 = 26.5 changed by -21.9 umol/kg. The solubility change from the warmer, saltier isopycnal water was only -0.9 umol/kg (4%). Apparent oxygen utilization (AOU) increased by 21.1 umol/kg. The ratio -dO2/dPO4 was 186 (158-230), near the remineralization ratio of 170 (Anderson and Sarmiento, 1994). The ratio -dO2/dNO3 was 18.0 (15.9-20.6), and N* (NO3 - 16 PO4) changed by -0.67 uM (-1.06 to -0.28). Thus the water lost nitrate in relation to phosphate.
- **The change is grid-wide.** All 57 stations had lower 2008-2025 oxygen than in 1984-1995 on sigma0 = 26.5. All 56 stations with data had a shallower hypoxic boundary.

Interpretation (not a tested causal claim): the oxygen deficit after 2007 is not explained by isopycnal salinity or by solubility. It agrees with water that has more respiration (higher AOU at the Redfield phosphate ratio) and a lower N*. Sources that can give these signals include older or less ventilated source water, a larger part of denitrified tropical water that is not visible as extra salinity on the isopycnal, and more local remineralization. Our data do not separate these sources.

## Figures

- `files/figures/fig1_timeseries.png`: annual and cruise-mean anomalies for oxygen on sigma0 = 26.5, the three forecasts, isopycnal salinity, and the hypoxic-boundary depth.
- `files/figures/fig2_salinity_proxy.png`: annual oxygen against isopycnal salinity, training and test years.
- `files/figures/fig3_station_change_map.png`: station changes (2008-2025 minus 1984-1995) of oxygen on sigma0 = 26.5 and hypoxic-boundary depth.
- `files/figures/fig4_tracer_budget.png`: oxygen, solubility, and AOU changes on sigma0 = 26.5; observed change ratios divided by remineralization ratios.

## Questions and pre-set tests

We defined these tests after a first look at the 1984-2021 bottle-database series. During the quality checks of the post-2021 files we also saw some post-2021 cruise means before we ran the tests. Thus the tests are not fully blind. The cast QC rule and the 2023 sensitivity came after we saw the data (see Limitations).

- T1, trend continuation (Bograd et al., 2008 period): fit OLS to the 1984-2006 annual means and extend it to 2007-2025. Compare the RMSE with (a) the held 2002-2006 mean level and (b) the 1984-2006 mean (zero anomaly). The interval of the mean squared-error difference comes from a moving-block bootstrap (block 3 years, 10,000 draws). We also report the 2007-2025 OLS slope with Newey-West (HAC, 3 lags) intervals. Variables: oxygen on sigma0 = 26.5 (primary), oxygen on 26.7 and at 200 m, and hypoxic-boundary depth.
- T2, new low-oxygen period by about 2020 (Pozo Buil and Di Lorenzo, 2017): compare the 2018-2025 mean with the 2008-2017 mean (HAC regression on a period indicator). If the prediction is correct, 2018-2025 must be lower.
- T3, salinity proxy: fit annual oxygen on annual salinity (both on sigma0 = 26.5) for 1984-2006. Predict 2007-2025 from the observed salinity. Report the mean residual (block bootstrap), RMSE, and the test correlation.
- T4, tracer budget (descriptive): change from 1984-1995 to 2008-2025 in oxygen, oxygen solubility (gsw O2sol_SP_pt), AOU, nitrate and phosphate on sigma0 = 26.5. Intervals come from a bootstrap of years within each period.

## Data

- **CalCOFI bottle database**, CSV release of 16 October 2023 (cruises 1949-03 to 2021-05). Source: https://calcofi.org/downloads/database/CalCOFI_Database_194903-202105_csv_16October2023.zip. ZIP SHA-256: 1d074d0581beb662fe141842eb4a4f46ebc4f02340ea9051eb1d894bafe807b7 (37,779,228 bytes). It is staged in the campaign shared store as `/mnt/dell-data/shared_datasets/calcofi-bottle-db-194903-202105-csv-16oct2023/`. The SHA-256 values of the extracted `194903-202105_Bottle.csv` and `194903-202105_Cast.csv` are in `files/provenance/bottle_db_extracted_csv_sha256.txt`.
- **CalCOFI CTD product files**, from https://calcofi.org/data/oceanographic-data/ctd-cast-files/. These are 9 "FinalQC" products (2019-02 to 2021-05) and 21 "Prelim" products (2021-07 to 2026-07), retrieved on 2026-11-09. We fetched only the CSV members with HTTP range requests. `files/provenance/calcofi_ctd_csv_members_manifest.csv` gives the URL, member name, ZIP CRC-32, size and SHA-256 of each of the 3,897 CSV members. We used the bottle rows (`OxBuM`, `SaltB`, `BTL_Temp`, `NO3`, `PO4`, with CTD `TempAve`/`SaltAve_Corr` where a bottle value is missing). They are frozen in `files/data/ctd_files_bottle_rows_2019_2025.csv.gz`. The Prelim products of 2025-07 and later had no bottle oxygen when we retrieved them, so the test period ends at cruise 2504.
- **Natural Earth 10 m land** (map background only): `/mnt/dell-data/shared_datasets/naturalearth-10m-land-v5/ne_10m_land.zip`, SHA-256 e547d749445eaa0964aba76738090ec88f5e63c4585122170f98c67a7ea922dc.

## Methods

1. **Bottle selection.** Bottle database: observed bottles only (RecInd = 3, no interpolated standard levels). We used oxygen only when the quality code was blank. We also removed flagged temperature, salinity, nitrate and phosphate values. CTD files: bottle oxygen `OxBuM` from 0 to 500 umol/kg. The files use negative values as missing-data flags.
2. **Profiles.** We calculated TEOS-10 sigma0 from in-situ T and practical salinity (gsw 3.6.23) for both data sources. Thus density has the same definition before and after 2021. For each cast, we interpolated linearly to these values:
   - oxygen, T and S at fixed depths (maximum gap 80 m between bottles);
   - oxygen, S, T, nitrate and phosphate on sigma0 = 26.0, 26.3, 26.5 and 26.7 (maximum gap 0.35 kg/m3, on the monotonic part of the profile);
   - the shallowest depth below 20 m where oxygen crosses 60 umol/kg.
3. **Validation of the two sources.** For 3 cruises that are in both sources (2019-04, 2020-01, 2020-07), the bottle profiles from the CTD files agree with the database. The median differences are 0.0 umol/kg for oxygen on sigma0 = 26.5 and 0.000 psu for salinity on the isopycnal. The SD of the difference is 3.1 umol/kg. The CTD sensor oxygen in the Prelim files is not usable: in the casts we examined, the "StaCorr" columns were often about half of the bottle values. We did not use sensor oxygen.
4. **Stations and anomalies.** Core grid: the 57 stations on lines 76.7-93.3 with oxygen at 200 m in at least 115 database cruises after 1984. Climatology: the mean for each station and season (Dec-Feb, Mar-May, Jun-Aug, Sep-Nov) in 1984-2006. Cast QC: we removed a cast when T or S at 100 m or 200 m was more than 5 training SDs from its station-season mean. The QC used T and S only, never oxygen. It removed 3 database casts and 16 CTD-file casts (14 from cruise 2024-01, where line 93.3 had 200 m temperatures near 4.7 degC, a sensor failure).
5. **Series.** A cruise mean is the mean anomaly over core stations, if 15 or more stations have a value. An annual mean is the mean of the cruise means in that calendar year. Nearshore = station number 60 or less; offshore = station number 70 or more.

## Robustness

| Check | Post-2006 O2 slope (umol/kg/yr) | 2018-25 minus 2008-17 | Proxy mean residual 2007-25 |
|---|---|---|---|
| All stations | +0.10 (-0.08, +0.28) | +1.8 (0.1, 3.5) | -11.5 (-14.4, -9.6) |
| Nearshore | +0.19 (+0.03, +0.36) | +2.8 (1.2, 4.4) | -10.2 (-12.7, -8.4) |
| Offshore | -0.02 (-0.22, +0.19) | +0.5 (-1.7, 2.7) | -14.2 (-17.0, -12.2) |
| Without 2023 | +0.05 (-0.12, +0.22) | +1.3 (-0.4, 3.0) | -12.0 |
| Bottle database only, to 2020 | +0.12 (-0.15, +0.39) | n/a | -12.4 (-15.5, -10.6) |
| sigma0 = 26.7 (all) | +0.11 (-0.16, +0.37) | n/a | -11.9 (-14.8, -10.1) |

On sigma0 = 26.7 the decline continued to about 2011, after the end of the training period. Thus the extended 1984-2006 trend gave a lower error there than the held 2002-2006 level (skill 0.44). At 200 m the post-2006 slope was +0.34 (-0.03, +0.72) umol/kg per year. All numbers are in `files/data/results.json`.

## Limitations

- **Proxy scope.** Pozo Buil and Di Lorenzo (2017) used a large-scale salinity index from ocean reanalysis (ORA-S3 EOF1 on sigma 26.5, 136-118 W, 31-46.5 N) and a 9-12 year lead from the gyre. We did not rebuild their index. We tested (a) their stated outcome, a new strong oxygen decline by 2020, with CalCOFI oxygen, and (b) the local form of the salinity-oxygen relation with CalCOFI isopycnal salinity. A large-scale index can behave differently from local CalCOFI salinity.
- **Post-2021 data are preliminary.** The CTD-file bottle values can change when CalCOFI releases final data. The QC rule and the 2023 sensitivity came after we saw the data. Cruise 2023-01 had high oxygen at many stations; the main conclusions do not depend on it.
- **Short test record.** The test period has 19 annual values with strong autocorrelation. The trend-versus-level loss difference is marginal. The post-2006 slope estimates are the more robust evidence.
- **Spatial and seasonal sampling.** Cruises sample different numbers of core stations (typically 20-30 have oxygen on sigma0 = 26.5). Anomalies remove the station-season means, but composition changes can add noise. Some cruises in 2024-2025 were partial.
- **Process attribution.** T4 is descriptive. A fixed remineralization ratio cannot separate ventilation age, source-water mix, and local respiration. N* also changes with denitrification history outside the region.
- **Multiple tests.** We report 4 test families on related variables and did not correct for multiple tests.

## Reproduction

`files/code/run_all.sh <path to files/>` repeats every step from public sources: download and checksum, range fetch of the CTD CSVs, per-cast metrics, series, tests and figures. Software: Python 3.12.16, pandas 3.1.1, numpy 2.5.4, gsw 3.6.23, statsmodels 0.15.0, matplotlib 3.11.2, remotezip 0.12.6, and geopandas 1.2.0 (map land layer only). Bootstrap seed: 20261109. Scripts:

- `profiles.py`: cast interpolation, TEOS-10 density.
- `process_bottle.py`, `process_ctd.py`: per-cast metrics.
- `build_series.py`: core grid, QC, anomalies, cruise and annual means.
- `analyze.py`: T1-T4 and sensitivities.
- `figures.py`: figures.
- `fetch_ctd.py`: range download of the CSV members.

Derived data: `files/data/bottle_db_casts.csv.gz` and `ctd_casts.csv.gz` (per-cast metrics), `core_cast_anomalies.csv.gz` (core-grid casts after QC, with anomalies), `cruise_means_*.csv`, `annual_*.csv`, `core_stations.json`, `results.json`.

## Provenance

- Campaign 11_07_2026.
- Job sci-1107-dell-earth-and-ocean-sciences-22050c1ec9e2.
- Topic earth-and-ocean-sciences.
- Machine dell.
- Model claude-opus-5-5 (Claude Code agent).
- Analysis date 2026-11-09.

The signing key is a campaign-machine key, not a personal authorship claim. We found no earlier campaign publication on CalCOFI oxygen.

## References

- Bograd, S. J., et al. (2008). Oxygen declines and the shoaling of the hypoxic boundary in the California Current. Geophysical Research Letters. doi:10.1029/2008GL034185
- Pozo Buil, M., and Di Lorenzo, E. (2017). Decadal dynamics and predictability of oxygen and subsurface tracers in the California Current System. Geophysical Research Letters 44, 4204-4213. doi:10.1002/2017GL072931
- Bograd, S. J., et al. (2015). Changes in source waters to the Southern California Bight. Deep-Sea Research Part II. doi:10.1016/j.dsr2.2014.04.009
- Ren, A. S., et al. (2018). A sixteen-year decline in dissolved oxygen in the central California Current. Scientific Reports. doi:10.1038/s41598-018-25341-8
- Anderson, L. A., and Sarmiento, J. L. (1994). Redfield ratios of remineralization determined by nutrient data analysis. Global Biogeochemical Cycles. doi:10.1029/93GB03318
