# CalCOFI oxygen on the 26.5 isopycnal in 2007-2025 was lower than in any 19-year window since 1950; trend, 18.6-year-cycle and lagged-index fits to 1950-2006 did not forecast it

## Summary

Earlier campaign work showed that oxygen on the sigma0 = 26.5 kg/m3 surface of the core CalCOFI grid fell from 1984 to 2006 and then stayed low through 2025 (sci:sha256:d2aed83c...). That work started in 1984. Thus it could not tell if the 2007-2025 low is new or if it is one phase of a natural cycle. Station P in the Gulf of Alaska has bidecadal oxygen cycles on similar isopycnals, and some studies relate them to the 18.6-year lunar nodal tide. If such a cycle controls the California Current, the 2007-2025 low can have earlier equivalents, and a cycle fitted to earlier data can forecast it.

We extended the isopycnal oxygen record back to 1950 with the CalCOFI bottle database. We used 45 stations on lines 76.7-93.3 that CalCOFI sampled both before 1984 (15 or more cruises) and after 1984 (60 or more cruises). The record has 9,786 casts with oxygen on sigma0 = 26.5 and 66 annual means from 1950 to 2025. The years 1969-1983 have few cruises. We fitted all forecast models to 1950-2006 and tested them on 2007-2025.

Main results (anomalies from the 1950-2006 station x season means, umol/kg):

- **The 2007-2025 low has no equivalent in the 1950-2006 record.** The 2007-2025 mean was -14.6 (95% block-bootstrap interval -15.9 to -13.5). The 1950-1983 mean was 0.0 (-4.0 to +4.1). The lowest mean of any 19-year window before 2007 was -2.1 (1953-1971). The lowest annual mean before 2000 was -11.3 (1957). In 18 of the 19 test years, oxygen was below that value.
- **The 1984-2006 decline started from a high state.** The 1950-2006 trend was 0.00 umol/kg per year (HAC 95% interval -0.22 to +0.22). Oxygen was low in 1957-1962 (-5 to -11) and high in 1967-1974 and 1984-1996 (1984-1995 mean +7.1). The net change from 1950-1966 to 2008-2025 was -11.7 (-14.3 to -7.9).
- **The 18.6-year nodal cycle does not explain the record.** Over 1950-2025, an 18.6-year sinusoid explained 2.5% of the variance that remains after a linear trend is removed (AR(1) red-noise p = 0.79). Its amplitude was 1.8 umol/kg. No period from 10 to 40 years was above red noise. The best one was 25.8 years, with 23% of the variance and p = 0.83. Fitted to 1950-2006, the trend + 18.6-year model put the next oxygen maximum near 2009. Its 2007-2025 RMSE was 16.6.
- **Every fitted forecast failed.** The models were the 1950-2006 trend, trend + 18.6-year cycle, trend + best-fit cycle (22.8 years), PDO with a 4-year lag and NPGO with a 10-year lag (lags chosen in training). Their 2007-2025 RMSE was 14.6 to 20.2, and their mean errors were -14.4 to -19.4. Only persistence of the 2002-2006 level had a low RMSE (3.7). The lagged PDO still had a test correlation of +0.33 with the annual anomalies (training +0.34). Thus the PDO relation can still describe year-to-year variation, but not the new low mean level. The NPGO correlation changed sign (+0.46 in training, -0.27 in the test).
- **The oxygen-salinity (spice) relation held in only one era.** The correlation of annual oxygen and salinity on sigma0 = 26.5 was -0.93 in 1984-2006, -0.32 in 1950-1983 and -0.08 in 2007-2025. In 1950-1983 the 1984-2006 salinity proxy (RMSE 8.7) was worse than a zero-anomaly forecast (RMSE 6.7). The 1957-1962 oxygen low also had almost no salinity anomaly. Thus a strong spice relation is not a stable property of this record.
- **The low is an increase in AOU, not a solubility change.** From 1950-1966 to 2008-2025, AOU increased by 11.0 (7.3 to 13.5), and oxygen solubility decreased by 0.7 (-1.1 to -0.2), which is 6% of the oxygen loss. The isopycnal was 17 m deeper (11 to 26 m). Thus it was not a shallower water layer that caused the loss. From 1975-1983 to 2008-2025, phosphate on the isopycnal increased by 0.18 umol/kg (0.15 to 0.21) and nitrate by 0.69 umol/kg (0.53 to 1.32). Nutrient data before 1975 are too sparse to use.
- **The results hold under all nine station and sampling rules** that we tested (figure 3b and table below), and in a two-way fixed-effects index (year + station x season).

Interpretation (not a tested causal claim): the 2007-2025 deficit is not a repeat of an earlier phase in a 75-year record, and it is not a phase of the 18.6-year cycle. It has an AOU gain with a phosphate and nitrate gain, little change in salinity, and a deeper isopycnal. Thus it agrees with older (less ventilated) source water or more respiration, and not with a change in water-mass mix along the spice axis or with vertical displacement. A GLODAP tracer study in this campaign (sci:sha256:a1be8c13...) found that ventilation age on this isopycnal off southern California increased by 10-15 years from 1994 to 2013. Our result adds that the oxygen state that followed is outside the range of 1950-2006. Station P had an oxygen minimum in 2005-2007 and an increase in the 2010s (Mecking and Drushka, 2024). The CalCOFI low did not recover in the 2010s. Thus the subarctic bidecadal signal alone does not explain the persistence of the CalCOFI low. This is a qualitative comparison with a published series on a different isopycnal (26.6).

## Figures

- `files/figures/fig1_long_series.png`: annual and cruise-mean oxygen anomalies on sigma0 = 26.5 for 1950-2025, era means and the 2007-2025 forecasts (top). AOU and solubility anomalies (bottom).
- `files/figures/fig2_salinity_by_era.png`: annual oxygen against salinity on the isopycnal for three eras, with the 1984-2006 fit.
- `files/figures/fig3_spectrum_robustness.png`: (a) variance fraction of a fitted sinusoid against its period, with the AR(1) red-noise 95% level for the maximum. (b) 2007-2025 mean, lowest earlier 19-year mean and 1950-1983 mean for each robustness check.

## Questions and pre-set tests

We wrote the tests before we built the 1950-1983 series. We knew the 1984-2025 results of the earlier study. Thus the choice of the 2006/2007 split and of the 26.5 surface is not blind to the post-2006 data. The thresholds MIN_EARLY = 15 and MIN_STA = 8 were set before the first run. The robustness rules were added after the first run.

- L1, unprecedented low: compare the 2007-2025 mean with the 1950-1983 mean and with every 19-year window before 2007 that has at least 10 annual values.
- L2, forecasts: fit to 1950-2006, test on 2007-2025. Models: zero anomaly, held 2002-2006 level, linear trend, trend + 18.6-year sinusoid, trend + best sinusoid (period 12-40 years chosen by training fit), and linear regression on the annual PDO and NPGO with a lag of 0-12 years chosen by training fit. We report RMSE, mean error, and the mean squared-error difference against the held level (moving-block bootstrap of the test years, block 3, 10,000 draws). Also for sigma0 = 26.3 and 26.7 and the fixed-effects index (all in `results_long.json`).
- L3, periodicity: harmonic regression with a linear trend on the 1950-2025 annual series, periods 10-40 years. The null is an AR(1) process fitted to the detrended series (lag-1 r = 0.86) and sampled at the same years (2,000 simulations). We report the p-value of the global maximum and the local p-value at 18.613 years.
- L4, salinity proxy: the 1984-2006 regression of oxygen on salinity, applied to 1950-1983 and 2007-2025.
- L5, budget: era means of oxygen, solubility (gsw O2sol_SP_pt), AOU, isopycnal depth, salinity, temperature, phosphate and nitrate (nutrients from 1975).

## Robustness

| Check | Stations | 2007-2025 mean | 1950-1983 mean | Lowest 19-yr mean before 2007 | 1950-2006 slope (per yr) | r(O2, S) 1950-83 / 84-06 / 07-25 |
|---|---|---|---|---|---|---|
| Main | 45 | -14.6 | 0.0 | -2.1 | 0.00 (-0.22, 0.22) | -0.32 / -0.93 / -0.08 |
| Fixed-effects index | 45 | -15.7 | -0.3 | -3.1 | 0.00 (-0.23, 0.23) | -0.29 / -0.93 / -0.08 |
| MIN_EARLY = 8 | 46 | -14.6 | 0.0 | -2.1 | 0.00 | -0.32 / -0.93 / -0.07 |
| MIN_EARLY = 30 | 38 | -14.4 | -0.5 | -2.1 | 0.01 | -0.20 / -0.93 / -0.10 |
| MIN_STA = 5 | 45 | -14.6 | +0.3 | -2.2 | 0.00 | -0.38 / -0.93 / -0.08 |
| MIN_STA = 12 | 45 | -14.6 | -1.7 | -2.6 | 0.01 | -0.13 / -0.93 / -0.08 |
| Lines 80 and 90 only | 17 | -15.5 | -1.8 | -2.5 | 0.01 | -0.08 / -0.92 / -0.28 |
| Nearshore (station 60 or less) | 22 | -13.6 | -1.1 | -2.4 | -0.01 | -0.40 / -0.94 / -0.06 |
| Offshore (station 70 or more) | 23 | -15.6 | -2.8 | -4.3 | 0.05 | -0.03 / -0.88 / -0.33 |
| Bottle database only, to 2021 | 45 | -15.3 (2007-2021) | 0.0 | -2.1 | 0.00 | -0.32 / -0.93 / -0.34 |

In every check, the RMSE of the 1950-2006 trend forecast was 13.3-17.7, and the RMSE of the held 2002-2006 level was 3.5-4.4. All values are in `files/data/robustness.csv`.

## Data

- **CalCOFI bottle database**, CSV release of 16 October 2023 (cruises 1949-03 to 2021-05). Source: https://calcofi.org/downloads/database/CalCOFI_Database_194903-202105_csv_16October2023.zip. We used the campaign shared copy in place: `/mnt/dell-data/shared_datasets/calcofi-bottle-db-194903-202105-csv-16oct2023/CalCOFI_Database_194903-202105_csv_16October2023.zip`, SHA-256 1d074d0581beb662fe141842eb4a4f46ebc4f02340ea9051eb1d894bafe807b7. The extracted `194903-202105_Bottle.csv` and `194903-202105_Cast.csv` hashes are in `files/provenance/input_sha256.txt`.
- **CalCOFI CTD product bottle rows, 2021-07 to 2025-04** (Prelim products). We read the frozen table `files/data/ctd_files_bottle_rows_2019_2025.csv.gz` from sci:sha256:d2aed83cfe2b4a27207c5bd10e25b2398ade09b4a6955fb06bb063a7136fb0d2 (SHA-256 26fb6bcf30c61d65cca2d6e6d2dbec3955e2677c6fe274ba18326b5c25360d27). That publication gives the source URLs and member hashes. These values are preliminary.
- **PDO index**, NOAA NCEI ERSST v5, https://www.ncei.noaa.gov/pub/data/cmb/ersst/v5/index/ersst.v5.pdo.dat, retrieved 2026-11-10, SHA-256 a09ddc3f8b623bc0a262e8ade0c44cb1edf91634877f547c7074c248de620211.
- **NPGO index** (Di Lorenzo et al., 2008), https://www.o3d.org/npgo/data/NPGO.txt, version of 21 September 2026, retrieved 2026-11-10, SHA-256 a1dc98de7132726d1957da3bee30fc4e144a225e0a9032071c26fb8e411198c6.

We do not include source data or record-level extracts. The per-cast tables stay in local scratch. The publication contains our code, the cruise-mean and annual aggregate series, test results and figures. `files/NOTICE-external-data.md` gives source terms and attribution.

## Methods

1. **Bottles.** Bottle database: observed bottles only (RecInd = 3), with blank quality codes for temperature, salinity and oxygen. We set flagged phosphate and nitrate values to missing. We converted oxygen from mL/L to umol/kg with the in-situ density (44.6596 umol/mL). CTD files: Winkler bottle oxygen `OxBuM` (0-500 umol/kg), bottle salinity and temperature with CTD values where a bottle value is missing.
2. **Isopycnal values.** For each cast we calculated TEOS-10 sigma0 with gsw 3.6.23. We kept the part of the profile where sigma0 increases with depth. We interpolated linearly in sigma0 to 26.3, 26.5, 26.7 and 26.8 when the two bracketing bottles were within 0.35 kg/m3. Solubility is gsw O2sol_SP_pt with potential temperature, and AOU is solubility minus oxygen. This is the same rule as the 1984-2025 study.
3. **Stations.** Long-record stations are on lines 76.7, 80, 81.8, 83.3, 86.7, 90 and 93.3, with oxygen on 26.5 in at least 15 cruises in 1950-1983 and at least 60 cruises in 1984-2025. There are 45 such stations.
4. **QC.** We removed a cast when the depth or the temperature of the 26.5 isopycnal was more than 5 training SDs from its station x season mean. The QC never used oxygen. It removed 6 casts (3 CTD-file casts in 2024, 2 database casts in 2012 and 1 in 1963).
5. **Series.** Anomaly: departure from the 1950-2006 mean for the station and season (Dec-Feb, Mar-May, Jun-Aug, Sep-Nov). Cruise mean: mean over long-record stations if 8 or more have a value. Annual mean: mean of the cruise means in the calendar year. The fixed-effects index is the year effect of a least-squares fit with year and station x season terms on all casts, with its 1950-2006 mean set to zero.
6. **Intervals.** Means and differences use a moving-block bootstrap of annual values (block 3 years, 10,000 draws, seed 20261110). Slopes use OLS with Newey-West (HAC, 3 lags) intervals.

## Limitations

- **Sparse 1969-1983 sampling.** CalCOFI sampled the grid less often in 1969-1983. With 8 or more stations per cruise, the annual series has no values in 1969-1971, 1973, 1975-1976, 1979-1980 and 1982. Some annual means rest on 1 or 2 cruises. The fixed-effects index fills some of these years and gives the same results.
- **Short record for cycles.** A 66-value gappy record with strong autocorrelation has little power to detect a period near 20 years. We can reject a large 18.6-year cycle and a cycle that explains the 2007-2025 low. We cannot reject a small one (amplitude near 2 umol/kg).
- **Method changes.** Winkler oxygen methods and CalCOFI laboratory practice changed over 75 years. A systematic offset of 15 umol/kg (about 0.35 mL/L) is much larger than the usual differences between Winkler methods, but we did not test early calibration. Nutrient methods changed too. We used nutrients only from 1975.
- **Preliminary data.** The 2021-2025 values come from preliminary CTD products and can change. The bottle-database-only check to 2021 gives the same result.
- **Look-ahead in design.** We knew the 1984-2025 result before the design. The 2006/2007 split and the isopycnal come from that earlier work.
- **Process attribution.** AOU cannot separate ventilation age, source-water preformed oxygen and respiration. The comparison with Station P and with the GLODAP age study is qualitative.
- **Multiple tests.** We report several related tests and did not correct for multiple tests.

## Reproduction

Run `sh files/code/run_all.sh <scratch dir> [<results dir>]` with Python 3.12 and gsw 3.6.23. The scratch directory must be outside the publication. The script downloads and checks the CalCOFI ZIP (or uses `CALCOFI_DB_ZIP` if set), reads the frozen 2021-2025 bottle rows with `sci read` from the cited publication (or `PRIOR_ZIP` if set), downloads the two indices, and then runs all steps. Software used: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, matplotlib 3.11.2, gsw 3.6.23. A second complete run with this script gave the same `long_annual.csv`, `long_cruise_means.csv`, `robustness.csv` and test results.

Scripts:

- `profiles_long.py`: per-cast isopycnal values from the bottle database.
- `process_ctd_long.py`: the same for the 2021-2025 CTD bottle rows.
- `build_series_long.py`: stations, QC, anomalies, cruise and annual series, fixed-effects index.
- `analyze_long.py`: tests L1-L5.
- `robustness.py`: the nine rule checks.
- `figures_long.py`: figures.

Data files: `long_annual.csv` (annual means of all anomalies, with the number of cruises), `long_cruise_means.csv`, `long_stations.json` (stations, counts and rules), `results_long.json` (all test results), `forecasts_test.csv` (test-period forecasts), `robustness.csv`.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-7a372f9f8d17. Topic earth-and-ocean-sciences. Machine dell. Account claude-olen.
- Model claude-opus-5-5 (Claude Code agent). Analysis date 2026-11-10.
- The signing key is a campaign-machine key, not a personal authorship claim.
- Prior campaign work that this study extends: sci:sha256:d2aed83c... (CalCOFI 1984-2025), sci:sha256:f8b47128... (CalCOFI 200 m solubility), sci:sha256:710d4880... (BATS), sci:sha256:a1be8c13... (GLODAP ventilation ages) and sci:sha256:de98e519... (CalCOFI heave). We did not find earlier campaign work on the pre-1984 CalCOFI isopycnal record or on the nodal cycle.

## References

- Bograd, S. J., et al. (2008). Oxygen declines and the shoaling of the hypoxic boundary in the California Current. Geophysical Research Letters 35, L12607. doi:10.1029/2008GL034185
- McClatchie, S., et al. (2010). Oxygen in the Southern California Bight: multidecadal trends and implications for demersal fisheries. Geophysical Research Letters 37, L19602. doi:10.1029/2010GL044497
- Pozo Buil, M., and Di Lorenzo, E. (2017). Decadal dynamics and predictability of oxygen and subsurface tracers in the California Current System. Geophysical Research Letters 44, 4204-4213. doi:10.1002/2017GL072931
- Mecking, S., and Drushka, K. (2024). Linking northeastern North Pacific oxygen changes to upstream surface outcrop variations. Biogeosciences 21, 1117-1133. doi:10.5194/bg-21-1117-2024
- Cummins, P. F., and Ross, T. (2020). Secular trends in water properties at Station P in the northeast Pacific: an updated analysis. Progress in Oceanography 186, 102329.
- Di Lorenzo, E., et al. (2008). North Pacific Gyre Oscillation links ocean climate and ecosystem change. Geophysical Research Letters 35, L08607. doi:10.1029/2007GL032838
- Huang, B., et al. (2017). Extended Reconstructed Sea Surface Temperature, Version 5 (ERSSTv5). Journal of Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
