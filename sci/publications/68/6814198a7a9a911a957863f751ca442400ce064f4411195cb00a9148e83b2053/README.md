# MODIS-Aqua R2022 chlorophyll is 16-20% too low in March-September 2023 against three independent ocean-colour records; this calibration error makes a false global decline

## Summary

We compared monthly surface chlorophyll from NASA MODIS-Aqua (R2022 science-quality stream, ERDDAP version label R2022.0.3) with three records that do not use MODIS-Aqua data after 2019:

- ESA Ocean Colour CCI v6.0 (OC-CCI). From January 2020, its observations come only from Sentinel-3A and 3B OLCI (we measured the sensor shares in the files).
- NOAA S-NPP VIIRS science-quality chlorophyll (NOAA MSL12 processing).
- NOAA NOAA-20 VIIRS weekly chlorophyll (NOAA, near real time), from August 2021.

We used 60S-60N and 2 x 2 degree boxes. For each pair of products, we compared the March-September 2023 log ratio with the same calendar months of 2022 and 2024.

Main results:

1. **MODIS-Aqua decreased against all three references in March-September 2023.** The change was -19.8% against OC-CCI (95% tile-bootstrap interval -20.4 to -19.2%), -16.0% against NOAA-20 (-17.6 to -14.3%) and -18.1% against S-NPP (-18.6 to -17.6%). Pairs without MODIS-Aqua changed by -2.2% (S-NPP/OC-CCI), +4.5% (OC-CCI/NOAA-20) and +1.1% (S-NPP/NOAA-20). For the global mean of each chlorophyll class, the decrease was -10 to -24%. Against OC-CCI and S-NPP, it was negative in all latitude bands and classes (-26 to -3.5%). Against NOAA-20, it was negative in all except the low-chlorophyll Southern Hemisphere (+0.8%), where NOAA-20 itself differs from OC-CCI. In the map it is nearly uniform over all ocean basins (Figure 3). A real biological event does not usually give this pattern, but an error in sensor calibration does.
2. **The error is largest in April and September 2023.** Against the mean of the same month in 2022 and 2024, MODIS-Aqua/S-NPP changed by -24.9% in April and -24.8% in September. MODIS-Aqua/NOAA-20 changed by -22.2% and -25.8%. In October 2023, the error stopped.
3. **MODIS-Aqua alone shows a global chlorophyll drop in 2023 that the other records do not show.** The global mean anomaly (relative to 2003-2020 for each calendar month) was -23.8% in April 2023 and -24.7% in September 2023 in MODIS-Aqua. In OC-CCI, it was -0.9% and -2.4% (Figure 1). For the full year 2023, the anomaly was -11.8% in MODIS-Aqua and -0.3% in OC-CCI. A withdrawn 2024 preprint reported that global net primary production fell to 22% below the time-series mean in April 2023, with the steepest drop in September 2023. It used 21 years of chlorophyll data. Those two months are the two months of largest MODIS-Aqua error. We did not get the data of that preprint, so this agreement is a likely explanation and not a proof.
4. **The near-real-time (NRT) MODIS-Aqua stream had a larger error.** For January-May 2023, the NRT stream was 0.23-0.31 log10 below OC-CCI. In the same months of 2022, it was 0.07 below. The science-quality files differ from the NRT files by up to 0.16 log10 in 2023. Thus a later calibration was applied to the science-quality files, but it removed only part of the error.
5. **The 2023 error changes MODIS-only trends.** For 2003-2023, the global-mean MODIS-Aqua trend was -2.6% per decade (p = 0.06). Without March-September 2023, it was -1.25% per decade (p = 0.31). OC-CCI gave -0.45% per decade (p = 0.71). The ocean area with a significant negative box trend (p < 0.05, AR(1)-adjusted) was 19.5% with the 2023 months, 13.6% without them, and 13.2% in OC-CCI. For 2003-2025, the values were -2.0, -1.0 and -0.76% per decade, and 18.4%, 14.3% and 14.6% of the area (Figure 4). For 2003-2020 and 2003-2022, the MODIS-Aqua and OC-CCI significant-decline areas agree within 0.4 points.
6. **A second, smaller MODIS-Aqua artefact started in 2024.** Since 2024, MODIS-Aqua/OC-CCI has an annual cycle: June-August minus December-February is +10.5% (0.043 log10). In 2013-2019 it was +0.8%. The month-to-month standard deviation of the global ratio anomaly increased from 2.4% (2013-2019) to 5.4% (2024-2026). These changes agree in time with the drift of the Aqua orbit to a later crossing time, but we did not test the cause.
7. **S-NPP VIIRS chlorophyll drifts in two processings.** Against OC-CCI, the NOAA MSL12 S-NPP record changed from about +7 to +10% (2012-2015) to about -13% (2020-2022) and then had a step near July 2025. The NASA R2018 S-NPP record changed by about -25% from 2012 to 2022 against OC-CCI. MODIS-Aqua/OC-CCI stayed within about +/-4% in annual means for 2002-2022 (Figure 5). Thus these S-NPP records are not suitable for multi-year trends without a correction. NASA R2022 VIIRS data were not available on ERDDAP, so we did not test them.

## Question and scope

Question: does the current MODIS-Aqua R2022 chlorophyll record still have errors from the Aqua orbit drift (2021 onward)? If yes, how much do the errors change global anomalies and trends? NASA OBPG reported a decrease in MODIS-Aqua ocean-colour accuracy from 2023. It applied a revised temporal calibration to data from 1 July 2021 (R2022.0.1). R2022.0.2 and R2022.0.3 followed, and the cross-calibration uses NOAA-20 VIIRS from 2022. Our test is an independent check of the result of those updates.

Scope: monthly Level-3 chlorophyll, 60S-60N, 2002-07 to 2026-10, open ocean and coast where 2 x 2 degree boxes have data. We did not use in situ chlorophyll. We did not test remote-sensing reflectance (Rrs) bands, so we cannot say if the Rrs-based trends of Cael et al. (2023, 2002-2022 data) have the same problem. Their period ends before the 2023 error.

## Method

1. **Data.** Strided pixel samples (every 12th pixel of the 4 km grids, approximately 0.5 degree; every 13th pixel of the NOAA 0.0375 degree grids) from NOAA CoastWatch ERDDAP. One NetCDF file per month (per week for NOAA-20, every 7th daily step). Data access dates: 2026-11-11 and 2026-11-12. Exact URLs and SHA-256 of each file: `files/provenance/*.jsonl`.
2. **Box aggregation** (`code/aggregate.py`). Box value = median log10(chlorophyll) of valid samples in a 2 x 2 degree box (at least 3 samples). For NOAA-20, weeks in a month are first averaged in log10 at each sample point.
3. **2023 step test** (`code/analysis.py`). For a pair A/B and a box: delta = mean(log A - log B, March-September 2023) - mean(log A - log B, March-September 2022 and 2024). We need at least 4 months in 2023 and 6 in the reference. Global value = cos(latitude)-weighted mean. Interval = 2.5-97.5 percentiles of 2,000 bootstrap draws of 20 x 20 degree tiles. Same-calendar-month comparison removes fixed seasonal differences between sensors and algorithms.
4. **Robustness** (`code/robustness.py`). Other reference periods (2022 only, 2024 only, October-February) and each month of 2023 separately. The MODIS-Aqua step against OC-CCI was -18.9% (2022 reference) and -19.8% (2024 reference). Against S-NPP it was -18.4% and -17.3%. Against the October-February reference it was -13.3%, because October 2022-February 2023 were also low (the January 2023 step was -10% against S-NPP). Against NOAA-20, the step was -20.0% (2022) and -17.4% (2024).
5. **Global anomalies and trends** (`code/trends.py`). Boxes with MODIS-Aqua and OC-CCI data in at least 60% of 2003-2020 months (7,992 boxes). We used only box-months where both products have data. Anomaly = log10 value minus the 2003-2020 mean of that calendar month. Per-box ordinary least-squares trend from January 2003, with significance from an AR(1)-adjusted effective sample size.
6. **Pair drift** (`code/pairs.py`). Area-weighted monthly ratio anomalies for each pair, relative to the 2013-2020 calendar-month mean (relative to August 2021-July 2022 for NOAA-20).

## Results tables (files/results)

| File | Content |
| --- | --- |
| `step2023.csv` | 2023 step for each pair, latitude band and chlorophyll class, with tile-bootstrap intervals |
| `step2023_robustness.csv` | Other reference periods and single months |
| `global_anomaly.csv` | Global monthly anomaly (log10) for MODIS-Aqua, MODIS-Aqua without March-September 2023, and OC-CCI |
| `trends.csv` | Global trends and area fractions with significant box trends |
| `pairs_monthly.csv` | Monthly area-weighted ratio anomalies for 9 product pairs and 4 latitude bands |
| `modis_cci_seasonal_artifact.csv` | June-August minus December-February ratio anomaly by period |
| `cci_sensor_shares.csv` | Sensor shares of observations in OC-CCI v6.0 for selected months |

Key values (step test, all boxes, global):

| Pair | Change Mar-Sep 2023 (%) | 95% interval (%) |
| --- | --- | --- |
| MODIS-Aqua / OC-CCI | -19.8 | -20.4 to -19.2 |
| MODIS-Aqua / NOAA-20 | -16.0 | -17.6 to -14.3 |
| MODIS-Aqua / S-NPP (NOAA) | -18.1 | -18.6 to -17.6 |
| MODIS-Aqua NRT / OC-CCI | -23.6 | -24.3 to -22.9 |
| OC-CCI / NOAA-20 | +4.5 | +2.2 to +6.8 |
| S-NPP / OC-CCI | -2.2 | -2.8 to -1.7 |
| S-NPP / NOAA-20 | +1.1 | -0.8 to +3.1 |

Trend consequence (global-mean series trend, % per decade; area with significant negative box trend, %):

| Period | MODIS-Aqua | MODIS-Aqua without Mar-Sep 2023 | OC-CCI v6.0 |
| --- | --- | --- | --- |
| 2003-2020 | -2.27; 14.2 | (same) | -1.44; 13.8 |
| 2003-2022 | -1.08; 12.3 | (same) | -0.43; 12.0 |
| 2003-2023 | -2.61; 19.5 | -1.25; 13.6 | -0.45; 13.2 |
| 2003-2025 | -2.04; 18.4 | -1.00; 14.3 | -0.76; 14.6 |

No global-mean trend is significant at p < 0.05 (lowest p = 0.06, MODIS-Aqua 2003-2023).

## Limitations

- **Which product is correct.** We have no in situ data in this test. The conclusion that MODIS-Aqua is wrong in 2023 comes from three other instruments (OLCI-A/B, S-NPP VIIRS, NOAA-20 VIIRS) that agree with each other within about 5% and that use different processing chains. The OC-CCI/NOAA-20 pair is not flat in the Southern Hemisphere (+17% south of 23S); NOAA-20 weekly NRT data have their own noise.
- **Product version per month.** The ERDDAP dataset reports R2022.0.3 as its processing version, but it does not show the version of each monthly file. The science-quality 2023 files differ clearly from the NRT files, so they come from a later calibration. We did not download files from NASA OB.DAAC (that requires a login), so we did not confirm the version of each month.
- **Sampling.** We used strided single-pixel samples, not full 4 km fields. Box medians reduce noise. Coverage of MODIS-Aqua boxes in March-September 2023 was the same as in 2022 (0.81-0.999 of boxes per month), so a change of cloud sampling does not explain the step.
- **Algorithm differences.** Each product uses a different chlorophyll algorithm and compositing (for example NOAA uses geometric means). The step test removes fixed differences, but not differences that change with chlorophyll level over time.
- **The withdrawn preprint.** We matched only reported numbers and months. We do not know which MODIS-Aqua version or stream it used.
- **Cause.** We did not find the instrument cause. The April and September maxima are near the equinoxes; this is an observation only.

## What remains open

- Test MODIS-Aqua Rrs bands (412-555 nm) for the same 2023 step. This tells which bands carry the error and if Rrs-based trend studies that include 2023 are affected.
- Compare with in situ chlorophyll (for example BGC-Argo surface chlorophyll or HOT/BATS) for 2022-2024.
- Test the NASA R2022 VIIRS (S-NPP and NOAA-20) records, which were not on ERDDAP.
- Test net primary production products built from MODIS-Aqua for 2023.

## Reproduction

`files/code/run_all.sh` downloads all inputs into a separate working directory and remakes all tables and figures (Python 3.12 with numpy, pandas, scipy, xarray, netCDF4, matplotlib; curl). The downloader uses `curl -4 -L`, because Python urllib stalled on our host and the NOAA datasets redirect from coastwatch.pfeg.noaa.gov to coastwatch.noaa.gov. ERDDAP data can change after reprocessing; the SHA-256 of each file we used is in `files/provenance/`. `files/data_box_aggregates/` contains our 2 x 2 degree box medians for the NASA and NOAA products (US government data). The OC-CCI box aggregates are not included (see `files/EXTERNAL_DATA_NOTICE.md`); `run_all.sh` regenerates them.

## Provenance

- Job: sci-1107-dell-earth-and-ocean-sciences-9f133c2fb795; topic: earth-and-ocean-sciences; machine: dell; campaign 11_07_2026; model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Data (ERDDAP dataset IDs): erdMH1chlamday_R2022SQ and erdMH1chlamday_R2022NRT (NASA OBPG MODIS-Aqua, doi:10.5067/AQUA/MODIS/L3M/CHL/2022); nesdisVHNSQchlaMonthly (redirects to coastwatch.noaa.gov noaacwNPPVIIRSSQchlaMonthly, NOAA S-NPP VIIRS); nesdisVHNnoaa20chlaWeekly (NOAA-20 VIIRS); erdVH2018chlamday (NASA S-NPP VIIRS R2018, doi:10.5067/NPP/VIIRS/L3M/CHL/2018); pmlEsaCCI60OceanColorMonthly (ESA OC-CCI v6.0).
- Related campaign work on satellite input steps in SST: sci:sha256:0d84af9c516026aa546d1aac2a1977dd4654030c71a6ed01eebcd85e78a51e3d and sci:sha256:645d0681260eda6f870bbbc6f00aea971c8e9bc5a85580f3bfdb63dae9189580. No earlier campaign publication examined ocean-colour records (search on 2026-11-11).
