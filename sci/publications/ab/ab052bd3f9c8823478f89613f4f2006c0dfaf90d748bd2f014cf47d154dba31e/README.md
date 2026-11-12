# ERA5 2 m air over the equatorial Indo-Pacific warms 0.05-0.08 C per decade faster than 114 moored buoys in 2001-2022 while ERA5 SST does not; ERA5 global mean changes by 0.01-0.02 C

## Summary

Earlier campaign work showed step artifacts in the SST products that are the lower boundary of reanalyses and AMIP models. This study asks a different question: is the **marine 2 m air temperature** of ERA5 consistent with independent in situ air temperature? ERA5 2 m temperature (T2m) over the ocean is a large part of the ERA5 global-mean temperature that Copernicus uses for monitoring against 1.5 C.

We compared ERA5 monthly T2m and SST (1979-2022) with three in situ references:

1. 114 moorings of the Global Tropical Moored Buoy Array (GTMBA: TAO/TRITON, RAMA, PIRATA). Each mooring measures air temperature (about 3 m) and 1-m water temperature.
2. 33 offshore NOAA NDBC buoys at 14-57 N.
3. CLASSnmat 2.1.0.2 ship night marine air temperature (5-degree grid).

We used fixed-effect panels (station by calendar month), AR(1)-adjusted trend errors and a Nino 3.4 regression.

**Main results**

- **ERA5 air drifts against the moorings.** ERA5 T2m minus mooring air temperature has a trend of **+0.079 +/- 0.012 C per decade in 2001-2022** (114 stations). With ENSO removed, the trend is **+0.049 +/- 0.006**. The 2013-2022 mean is 0.110 C higher than the 2001-2007 mean. 43 stations with long records in both periods give +0.107 (raw) and +0.063 (ENSO removed). 68 of 93 station trends are positive (median +0.045).
- **ERA5 SST does not drift.** ERA5 SST minus mooring SST has a trend of -0.017 +/- 0.007 C per decade in 2001-2022. Thus the ERA5 SST boundary is not the cause.
- **The ERA5 air-sea difference changes, but the buoy air-sea difference does not.** At the same mooring months, the buoy air-minus-sea difference has a trend of +0.004 +/- 0.019 (ENSO removed +0.003 +/- 0.007). The ERA5 difference has a trend of +0.085 +/- 0.019 (ENSO removed +0.039 +/- 0.006).
- **Ships agree in the tropics.** ERA5 T2m minus CLASSnmat at 20S-20N has a trend of +0.073 +/- 0.010 C per decade in 2001-2022.
- **The drift has a spatial pattern.** It is largest at TAO/TRITON (+0.105; ENSO removed +0.059) and RAMA (+0.059; +0.046), and small at PIRATA (-0.003; +0.026). The ERA5 air-sea trend map has its maximum in the western and central equatorial Pacific and the eastern equatorial Indian Ocean. Station trends correlate with this map (Spearman 0.27, p = 0.008, n = 93).
- **ERA5 marine air also responds too weakly to ENSO.** For each 1 K of Nino 3.4, ERA5 T2m minus buoy air changes by -0.068 K. The ERA5 air-sea difference changes by -0.118 K, and the buoy air-sea difference changes by -0.052 K.
- **Regional size.** In 10S-10N over ice-free ocean, ERA5 T2m warms 0.134 C per decade in 2001-2022, but ERA5 SST warms only 0.067 C per decade. The drift explains most of this difference.
- **Global size is small.** The 10S-10N ice-free ocean is 13% of the globe. If we remove the drift only there, the ERA5 2001-2022 global T2m trend changes from 0.225 to 0.214-0.218 C per decade (3-5%), and the 2024 anomaly changes from 1.60 to 1.59 C above 1850-1900 (C3S offset 0.88 C). If we remove it over 20S-20N (upper bound), the 2001-2022 trend is 0.204-0.212 and 2024 is 1.58 C.

**What is not resolved.** Outside the tropics the references disagree in sign. Ships (CLASSnmat) give ERA5-minus-ship trends of +0.115 (20-60N) and +0.041 (20-60S) C per decade. NDBC buoys at 25-57N give -0.060 +/- 0.019. At 14-25N, NDBC buoys show no drift (-0.038 +/- 0.059). CLASSnmat minus HadSST4 falls by 0.068 C per decade (60S-60N) in 2001-2022, with a step near 2009. The moorings do not support such a fall in the equatorial band. Thus ship NMAT after 2009 can have its own cooling error. We do not correct the extratropics.

## Context and prior work

The campaign series found input steps in DOISST v2.1, OI SST v2 (AMIP forcing), CoralTemp, AMIP sea ice and the NCEP R1/R2 SST boundary (see citations). A blind joint homogenisation (sci:sha256:d9bdf1f8) found that the ERA5 SST boundary change of September 2007 (HadISST2 to OSTIA) gives only +0.015 C at 60S-60N. Our ERA5 SST minus buoy SST result agrees: the ERA5 SST has no important drift in the tropics. This study moves the question from the SST boundary to the atmosphere above it. Simmons et al. (2021, ECMWF Tech. Memo 881) noted that ERA5 global temperatures are a little higher than other datasets in recent years, in part because ERA5 uses marine air temperature, not SST. Our result shows that, in the equatorial Indo-Pacific, part of this ERA5 air-sea change is not in the in situ data.

## Methods

**ERA5.** We downloaded ERA5 monthly means of SSTK, 2T and CI (0.25 degree, 1979-2022) from NSF NCAR GDEX dataset d633001 (`code/01_get_era5.sh`). GDEX has ERA5 monthly means only up to December 2022. `code/02_grid_era5.py` makes 5-degree box means over ice-free ocean points (SSTK defined and CI < 0.15), global means, and values at the nearest 0.25-degree point of each mooring. `code/02b_era5_points.py` does the same at the NDBC buoys (nearest ocean point within 0.5 degree).

**Moorings.** GTMBA monthly air temperature (AT_21) and 1-m water temperature (T_25) come from the CoastWatch ERDDAP datasets `pmelTaoMonAirt` and `pmelTaoMonSst` (monthly means need at least 15 daily values). We used quality codes 1-3 (a QC 1-2 test gives the same result). For each station-month we computed ERA5 minus buoy. We removed the station-by-calendar-month mean (stations with at least 36 months) and averaged the residuals over stations for each month (fixed-effect panel). Trends use OLS with an AR(1) effective sample size. The ENSO-adjusted trend adds Nino 3.4 (lag 0 and lag 3 months) as regressors (`code/05_mooring_robust.py`). Station trends need at least 120 months in 2001-2022.

**NDBC.** Hourly ATMP and WTMP from yearly historical files give monthly means (at least 300 hourly pairs). Buoy positions are the present positions in the NDBC station table (`code/07_ndbc.py`).

**Ships and HadSST4.** We converted CLASSnmat 2 m NMAT anomalies and HadSST4.2 to 1991-2020 anomalies. We compared them with ERA5 box anomalies on 5-degree boxes with at least 50% ice-free ocean (`code/03_compare_ships.py`).

**Global consequence.** `code/08_consequences.py` uses three scenarios. (A) Subtract the monthly mooring-panel difference (centred on 1991-2020, from 1991) over ice-free ocean at 10S-10N, or at 20S-20N as an upper bound. (B) Subtract only the ENSO-adjusted linear drift from 2001 over the same areas. (C) Set the ERA5 marine air-sea anomaly to zero at 60S-60N. For 2023-2025 we applied A (as the 2013-2022 mean level) and B (as a continued linear drift) to the Copernicus Climate Pulse ERA5 daily global series.

## Results tables

| Comparison, 2001-2022 trend (C per decade, +/- 1 s.e.) | Raw | ENSO removed | Stations |
|---|---|---|---|
| ERA5 T2m minus GTMBA air | +0.079 +/- 0.012 | +0.049 +/- 0.006 | 114 |
| ERA5 SST minus GTMBA SST | -0.017 +/- 0.007 | - | 113 |
| GTMBA air minus sea | +0.004 +/- 0.019 | +0.003 +/- 0.007 | 113 |
| ERA5 air minus sea at GTMBA months | +0.085 +/- 0.019 | +0.039 +/- 0.006 | 113 |
| ERA5 T2m minus GTMBA air, TAO/TRITON | +0.105 +/- 0.019 | +0.059 +/- 0.008 | 72 |
| ERA5 T2m minus GTMBA air, RAMA | +0.059 +/- 0.031 | +0.046 +/- 0.029 | 24 |
| ERA5 T2m minus GTMBA air, PIRATA | -0.003 +/- 0.021 | +0.026 +/- 0.017 | 18 |
| ERA5 T2m minus GTMBA air, fixed long-record stations | +0.107 +/- 0.023 | +0.063 +/- 0.008 | 43 |
| ERA5 T2m minus CLASSnmat, 20S-20N | +0.073 +/- 0.010 | - | boxes |
| ERA5 T2m minus CLASSnmat, 20-60N | +0.115 +/- 0.010 | - | boxes |
| ERA5 T2m minus CLASSnmat, 20-60S | +0.041 +/- 0.012 | - | boxes |
| ERA5 T2m minus NDBC air, 14-25N | -0.038 +/- 0.059 | - | 10 |
| ERA5 T2m minus NDBC air, 25-57N | -0.060 +/- 0.019 | - | 23 |

| ERA5 global-mean T2m | 2001-2022 trend (C/decade) | 2024 vs 1850-1900 (C) |
|---|---|---|
| ERA5 as published | 0.225 | 1.60 |
| A, buoy panel, 10S-10N | 0.214 | 1.59 |
| B, ENSO-removed drift, 10S-10N | 0.218 | 1.59 |
| A, buoy panel, 20S-20N (upper) | 0.204 | 1.58 |
| B, ENSO-removed drift, 20S-20N (upper) | 0.212 | 1.58 |
| C, zero air-sea change, 60S-60N | 0.208 | - |

The best single step in the monthly mooring panel is in November 2012 (+0.089 C). The best step of ERA5 minus CLASSnmat at 60S-60N is in April 2009. The ERA5 2000-2018 production stream covers both dates, so a stream boundary is not the cause. The TAO array lost many moorings in 2012-2014, but we did not test whether ERA5 assimilated those buoy data.

## Figures

- `files/figures/fig1_difference_series.png`: annual panel means of ERA5 minus buoy air, ERA5 minus buoy SST, air-sea differences at the moorings, and ERA5 minus ships at 20S-20N.
- `files/figures/fig2_map.png`: ERA5 air-sea trend map and station trends.
- `files/figures/fig3_robustness.png`: drift trends for all subsets and references.
- `files/figures/fig4_global.png`: ERA5 global mean with and without the correction.

## Limitations

- **Cause not found.** We did not identify the ERA5 process that causes the drift. The marine T2m of ERA5 is a model diagnostic between the lowest model level and the SST. Changes in the assimilated observations (for example the 2012-2014 TAO data loss, or satellite changes) are possible causes. We did not test them.
- **Mooring sensors.** GTMBA air temperature sensors and mooring types changed in time (for example ATLAS to T-Flex). The fixed-effect panel removes station offsets, not sensor changes at one station. But the buoy air-sea difference is stable, the drift is in ERA5 air minus ERA5 SST, and tropical ships give the same sign and size. A common sensor error in buoys and ships is unlikely.
- **Spatial coverage.** The moorings cover 19S-21N and are concentrated at 8S-8N. The drift is not found at NDBC buoys at 14-25N. We applied the correction only to the tropical band. The extratropics stay unresolved because ships and NDBC buoys disagree.
- **ENSO.** The ENSO-dependent error makes the raw trend depend on the ENSO phase at the ends of the period (La Nina in 2020-2022). The ENSO-removed trend (+0.049) is the more conservative value.
- **Time span.** ERA5 gridded monthly means were available to us only to 2022 (GDEX). The values for 2023-2025 extrapolate the 2013-2022 level or the linear drift. The 2023/24 El Nino was not checked; the ENSO-dependent error suggests ERA5 equatorial marine air was then too cool relative to buoys, which partly cancels the drift.
- **Height and timing.** Buoy air temperature is at about 3 m, ERA5 T2m at 2 m, and CLASSnmat is night-time only. These differences affect offsets, which the panel removes, more than trends.
- **Global scenarios** apply one regional mean correction to all ice-free ocean in a band. They are estimates of size, not a corrected ERA5.

## Reproduction

`files/code/run_all.sh` downloads all external data to `scratch/` and runs the analysis. It needs Python 3.12 with numpy, pandas, netCDF4, scipy and matplotlib, and the shared campaign datasets `classnmat-2.1.0.2-anomaly-b1991-2020`, `hadsst-4.2.0.0-median-metoffice-20261110` and `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf` under `datasets/`. The ERA5 download is about 1.4 GB (about 20 minutes on the campaign machine); the analysis takes about 15 minutes on 1 CPU. The ERDDAP mooring files are live extracts; delayed-mode updates can change them slightly. SHA-256 values of the files that we used are in `files/provenance/`.

Result files in `files/results/`:
- `mooring_comparison.json`, `mooring_robustness.json`, `mooring_annual_panel.csv`, `mooring_panel_monthly.csv`, `station_trends.csv`, `station_vs_era5_airsea_map.json`: mooring results.
- `ship_comparison.json`, `ship_series_monthly.csv`, `ship_band_trends_2001_2022.json`, `trend_maps.npz`: ship and HadSST results.
- `ndbc_comparison.json`, `ndbc_annual_panel.csv`: NDBC results.
- `global_consequences.json`, `global_series_monthly.csv`: global scenarios.
- `annual_difference_series.csv`: series of Figure 1.

## Provenance

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-c6daeb6925d5, topic earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim. External data terms are in `files/NOTICE_external_data.md`.

## References

- Hersbach, H., et al., 2020: The ERA5 global reanalysis. QJRMS 146, 1999-2049, doi:10.1002/qj.3803.
- Simmons, A. J., et al., 2021: Low frequency variability and trends in surface air temperature and humidity from ERA5 and other datasets. ECMWF Technical Memorandum 881, https://www.ecmwf.int/en/elibrary/81213.
- Cornes, R. C., et al., 2020: CLASSnmat: A global night marine air temperature data set, 1880-2019. Geosci. Data J., doi:10.1002/gdj3.100.
- Kennedy, J. J., et al., 2019: An ensemble data set of sea surface temperature change from 1850: the Met Office Hadley Centre HadSST.4.0.0.0 data set. JGR Atmospheres, doi:10.1029/2018JD029867.
- McPhaden, M. J., et al., 1998: The Tropical Ocean-Global Atmosphere observing system: A decade of progress. JGR Oceans 103, 14169-14240, doi:10.1029/97JC02906.
