# DOISST v2.1 kept its July 2020 warm step after the October 2021 change from Navy to ACSPO input; against a fixed ACSPO yardstick its level did not follow the Navy input level (60S-60N, 2019-2024)

## Summary

NOAA Daily OISST v2.1 (DOISST) has a warm step of about +0.07 C (60S-60N) on 6-7 July 2020. Campaign work found the cause: on 6 July 2020 the U.S. Navy (NAVO) changed its MetOp-A AVHRR SST processing from version 1.0 to version 2.0 (sci:sha256:9fca62cd). Version 2.0 keeps more clear-sky pixels, mostly in daytime, and this pixel selection gives the warm offset against ESA SST CCI (sci:sha256:5cba350c, sci:sha256:656c3dbc).

On 1 October 2021 DOISST stopped using Navy AVHRR SST and started to use NOAA ACSPO SST. Earlier work found only a small change on that date (-0.02 to -0.045 C with 12-month windows, sci:sha256:b93b5f64) and did not explain why the 2020 offset continued after the Navy input stopped. This is important for homogenisation: if the 2020 step is an offset of the Navy input, the October 2021 change should remove it and a correction must end there; if it is not, the correction must continue.

We used one fixed satellite reference (a "yardstick") for both dates: ACSPO L3U SST from the AVHRR on MetOp-B, one processing version (ACSPO L2 algorithm V2.80) for all days. We compared DOISST and the NAVO inputs with this yardstick in the same 1-degree cells and on the same days, in 2019, 2020 and 2021, with control years for the same calendar days.

Main results (60S-60N; C):

1. **No step back on 1 October 2021.** Against the ACSPO yardstick, DOISST changes by +0.018 (95% interval -0.034 to +0.051; day +0.011, night +0.025) across 1 October 2021 (10-29 September vs 3-21 October 2021, minus the same change in 2020). A reversal of 0.035 C or more (the size of the 2020 step against the same yardstick) has a bootstrap probability of 0.024. Against ESA CCI v3, the 28-day local step is +0.010 (standard deviation of the same statistic at other dates 0.020; p = 0.64).
2. **The ACSPO period has the level of the Navy v2.0 period.** The mean DOISST minus CCI difference is +0.001 for 2016 to 5 July 2020 (Navy v1.0), +0.065 for 7 July 2020 to 30 September 2021 (Navy v2.0) and +0.064 for 1 October 2021 to 31 March 2023 (ACSPO). The July 2020 step is +0.084 against CCI (p < 0.001) and +0.046 against the ACSPO yardstick (0.012 to 0.076, with a 2019 control).
3. **The DOISST level does not follow the level of the Navy input.** Against the yardstick, in the same calendar windows:
   - In July 2020 the MetOp-A input rose by +0.044 (day) and +0.013 (night) relative to the 2019 change; DOISST rose by +0.035 (day) and +0.056 (night).
   - From September-October 2020 to September-October 2021, NAVO v2.0 MetOp-A fell by 0.063 (day; -0.133 to +0.008) and 0.086 (night; -0.132 to -0.046), and MetOp-B by 0.036 (day) and 0.015 (night). In the same windows DOISST did not fall: it rose by +0.054 against the yardstick and by +0.047 against CCI.
   - Just before the switch (30 August-9 October 2021), the ACSPO yardstick was warmer than the Navy v2.0 inputs (MetOp-A by +0.046 day and +0.017 night; MetOp-B by +0.090 day and +0.048 night). DOISST did not step up by this amount (result 1).
4. **The yardstick is stable.** From September-October 2020 to September-October 2021, DOISST minus yardstick and DOISST minus CCI change by the same amount within 0.007 C at 60S-60N (0.023 C at 20S-20N).
5. **A later decrease.** After the April 2023 change to DOISST v2.1b (monthly ship correction), the DOISST minus CCI level falls to +0.019 (1 April 2023 to 22 June 2024). This decrease is gradual (local step on 1 April 2023: +0.013, p = 0.51) and occurs in the tropics and the Northern Hemisphere; at 40-60S the level stays high (+0.176 against +0.195 before). We did not test its cause.

Conclusion: the July 2020 warm step continued unchanged through the October 2021 change to ACSPO input, until at least March 2023. The level of the Navy input against a fixed ACSPO reference does not predict the DOISST level: the input moved by 0.04-0.09 C between the dates and DOISST did not follow. Thus the step is not a calibration offset of the Navy SST that the ACSPO input removed. The result agrees with the published explanation (pixel selection, sci:sha256:656c3dbc) if ACSPO keeps clear-sky pixels in a similar way to Navy v2.0, so that the DOISST analysis sees the same sampling before and after October 2021; we did not test this directly. Consequence for users: against two satellite references (ESA CCI and ACSPO), a homogenisation of DOISST must keep the full 6 July 2020 correction after 1 October 2021 and needs no reversal term on that date. The published homogenisations fitted a 2021-10-01 term against in situ products with 12-month windows (-0.048 C against HadSST4.2 and -0.034 C against ERSSTv5 in sci:sha256:645d0681; -0.005 to -0.050 C in sci:sha256:dbf09341). If the satellite references are correct, those terms add a false cooling step of 0.03-0.05 C in October 2021. With these data we cannot say which reference type is correct.

## Context in the campaign

- Cause and size of the July 2020 step: sci:sha256:b93b5f64 (found the step), sci:sha256:645d0681 (3-day ramp; homogenisation), sci:sha256:9fca62cd (Navy MetOp-A v1.0 to v2.0 change; offset against CCI and drifters), sci:sha256:e75ccf52 (buoy checks see one third of the step), sci:sha256:5cba350c (offset is inside fixed 5-degree and day/night groups), sci:sha256:656c3dbc (offset is daytime pixel selection; satellite-count events do not step the DOISST mean).
- Open item that this study answers: 9fca62cd measured the input offset only in July-August 2020 and noted that the October 2021 change removed only a small part of the step. This study measures the Navy and DOISST levels against one fixed reference across both dates.

## Data

- **ACSPO L3U AVHRR MetOp-B** (NOAA/STAR, GHRSST L3U, 0.02 degree, 10-minute granules, "AVHRRF_MB-ACSPO_V2.80"), NOAA NCEI GHRSST archive (https://www.ncei.noaa.gov/data/oceans/ghrsst/L3U/AVHRRMTB/OSPO/). Every 2nd granule of each day; 10,962 granules; 153 days: 22 June-20 July 2019 and 2020, 10 September-21 October 2021, 10 September-21 October 2020 (control), and 30 August, 7, 15, 23 September, 1 and 9 October 2019 and 2020. All granules have L2 algorithm V2.80 (L3 gridding V4.6.7 in 2019-2020 and V4.6.9 in 2021). The NCEI archive has no MetOp-B L3U files from mid-May 2022 to 2023, so we used 2020 (not 2022) as the control for 2021.
- **NAVO AVHRR GAC L2P** MetOp-A and MetOp-B, v1.0 (file suffix fv01.0) and v2.0 (fv02.0), NCEI GHRSST archive (https://www.ncei.noaa.gov/data/oceans/ghrsst/L2P/). 1,238 granules (all MetOp-A granules 15 June-27 July 2020; MetOp-A 2-11 July 2019; MetOp-B samples; every 2nd granule for 30 August-9 October 2019 and 2020; all available granules for the six 2021 days). The NCEI archive keeps only one day in eight for 2021 after March, so 2021 has six NAVO days.
- **DOISST v2.1** AVHRR-only daily means, NOAA PSL yearly files 2016-2022 (shared campaign store, read in place; SHA-256 in `files/provenance/doisst_shared_files.csv`).
- **DOISST minus ESA SST CCI v3.0.1** daily regional series 1982-2024 (fixed 1-degree point mask) from sci:sha256:b93b5f64 (`files/data/doisst_cci_daily_regional.csv.gz` in that bundle; not copied here).
- **iQuam v2.10** June-August 2020 (NOAA STAR): the NAVO reducer also stores buoy match-ups; they are not used in the results of this publication.

## Methods

**Yardstick fields.** For each ACSPO L3U granule we kept pixels with quality level 5 at 60S-60N and summed SST to 1-degree cells, separately for day and night (L2P flag bit "day"), per UTC day (`files/code/l3u_reduce.py`).

**NAVO fields.** For each NAVO L2P granule we kept quality level 5 pixels (the only valid level in v2.0; "best" in v1.0) and summed SST to 1-degree cells by day and night (solar zenith angle below 90 degrees) per UTC day (`files/code/navo_reduce.py`).

**DOISST minus yardstick.** For each day, DOISST 1-degree cell means (4 x 4 cells of 0.25 degree, all cells above -1.2 C) minus the yardstick cell mean, for cells with at least 20 yardstick pixels, cos(latitude) weighted, for night and day separately (`files/code/yardstick_compare.py`). Step = [mean(after) - mean(before)] in the event year minus the same in the control year. Windows: 22 June-4 July vs 8-20 July (2020 event, 2019 control); 10-29 September vs 3-21 October (2021 event, 2020 control). Two days at each date are left out for the ramp of the final DOISST analysis (3 days of AVHRR data). 95% intervals: 5-day block bootstrap of the days in all four windows (1,000 or 2,000 draws). The combined step uses the mean of the day and night series (`files/code/stability_and_combined.py`).

**NAVO minus yardstick.** Same 1-degree cell, same UTC day and same day/night class; NAVO cells with at least 5 pixels; the cell difference is weighted by the NAVO pixel count inside the cell and the cells by cos(latitude). Same-season change from 2020 to 2021 with a bootstrap over days.

**Stability of the yardstick.** We compared the 2020-to-2021 change (10 September-21 October) of DOISST minus yardstick with the change of DOISST minus CCI on the same days. CCI uses no NAVO or ACSPO data.

**CCI periods and local steps.** Means of the DOISST minus CCI anomaly difference by input period, and 28-day local steps (28 days after minus 28 days before, ramp days left out) compared with the same statistic at all other dates in 2017-2023 at least 31 days from an event (`files/code/recent_periods.py`).

## Results tables

Steps of DOISST against the ACSPO MetOp-B yardstick (C; `files/results/yardstick_steps_combined.csv`, `files/results/yardstick_doisst_steps.csv`):

| Event | Control | Day | Night | Day + night (95% interval) |
|---|---|---|---|---|
| 6 July 2020, NAVO MetOp-A v1.0 to v2.0 | 2019 | +0.035 (0.020 to 0.061) | +0.056 (-0.003 to 0.100) | +0.046 (0.012 to 0.076) |
| 1 October 2021, Navy to ACSPO | 2020 | +0.011 (-0.054 to 0.043) | +0.025 (-0.017 to 0.057) | +0.018 (-0.034 to 0.051) |

NAVO input minus ACSPO MetOp-B yardstick, 60S-60N (C; mean over days; `files/results/yardstick_navo.csv`):

| Satellite | NAVO version | Window | Days | Day | Night |
|---|---|---|---|---|---|
| MetOp-A | 1.0 | 2019 22 Jun-5 Jul | 4 | -0.014 | -0.004 |
| MetOp-A | 1.0 | 2019 7-20 Jul | 4 | -0.020 | +0.008 |
| MetOp-A | 1.0 | 2020 22 Jun-5 Jul | 13 | +0.009 | +0.029 |
| MetOp-A | 2.0 | 2020 7-20 Jul | 14 | +0.047 | +0.054 |
| MetOp-A | 1.0 | 2019 30 Aug-9 Oct | 6 | -0.024 | -0.018 |
| MetOp-A | 2.0 | 2020 30 Aug-9 Oct | 6 | +0.017 | +0.069 |
| MetOp-A | 2.0 | 2021 30 Aug-9 Oct | 6 | -0.046 | -0.017 |
| MetOp-B | 1.0 | 2019 30 Aug-9 Oct | 6 | -0.147 | -0.082 |
| MetOp-B | 2.0 | 2020 7-9 Aug | 3 | -0.044 | -0.010 |
| MetOp-B | 2.0 | 2020 30 Aug-9 Oct | 6 / 5 | -0.054 | -0.034 |
| MetOp-B | 2.0 | 2021 30 Aug-9 Oct | 10 | -0.090 | -0.048 |

Same-season change of NAVO v2.0 against the yardstick, 2020 to 2021 (`files/results/navo_same_season_change.csv`): MetOp-A day -0.063 (-0.133 to +0.008), night -0.086 (-0.132 to -0.046); MetOp-B day -0.036 (-0.089 to +0.016), night -0.015 (-0.073 to +0.050).

Yardstick stability, 10 September-21 October, 2020 to 2021 (`files/results/yardstick_stability.csv`): DOISST minus yardstick +0.054, DOISST minus CCI +0.047 (60S-60N); 20S-20N +0.048 and +0.025; 40-60S +0.186 and +0.196.

DOISST minus CCI by input period (anomaly difference against 2005-2015; `files/results/recent_periods.csv`):

| Period | 60S-60N | 20S-20N | 20-60N | 20-60S | 40-60S |
|---|---|---|---|---|---|
| 2016-01-01 to 2020-07-05, Navy v1.0 | +0.001 | -0.028 | +0.048 | +0.007 | +0.068 |
| 2020-07-07 to 2021-09-30, Navy v2.0 | +0.065 | +0.013 | +0.096 | +0.107 | +0.190 |
| 2021-10-01 to 2023-03-31, ACSPO (v2.1a) | +0.064 | +0.010 | +0.100 | +0.106 | +0.195 |
| 2023-04-01 to 2024-06-22, ACSPO, monthly ship correction (v2.1b) | +0.019 | -0.044 | +0.034 | +0.083 | +0.176 |

28-day local steps of DOISST minus CCI (`files/results/recent_local_steps.csv`): 6 July 2020 +0.084 (p < 0.001); 1 October 2021 +0.010 (p = 0.64); 1 April 2023 +0.013 (p = 0.51) at 60S-60N.

By latitude band, the October 2021 step against the yardstick is noisy (from -0.036 at 20-40N to +0.13 at 40-60N; `files/results/yardstick_steps_combined.csv`), and no band shows a reversal of the 2020 step. At 40-20S the July 2020 step against the yardstick is negative (-0.092), while it is positive against CCI (+0.065 at 20-60S); we did not resolve this band difference.

## Figures

- `files/figures/fig1_switches.png`: (a, b) daily DOISST minus ACSPO MetOp-B yardstick (60S-60N, 3-day mean), day and night, around 6 July 2020 and 1 October 2021, with the control year on the same dates (dashed); (c, d) NAVO L2P minus yardstick on each available day.
- `files/figures/fig2_levels.png`: (a) level of the NAVO MetOp-A and MetOp-B input against the yardstick in each window (labels give the NAVO version); (b) monthly DOISST minus CCI, 2019 to June 2024, with the 2020, 2021 and 2023 DOISST input changes.

## Limitations

- **The yardstick is a satellite product.** ACSPO L3U MetOp-B has its own cloud mask and pixel selection, and it is not identical to the ACSPO input that DOISST used from October 2021 (NCEI names ACSPO L3S; we could not confirm which satellites and which level). The yardstick agrees with CCI on the 2020-2021 change within 0.007 C (60S-60N) but within 0.023 C in the tropics. Against this yardstick the July 2020 input change (+0.013 to +0.044) is smaller than against CCI (+0.10, sci:sha256:9fca62cd), probably because ACSPO and NAVO v2.0 select similar clear-sky pixels. Thus "input level" in this study means the level relative to ACSPO, not the absolute level.
- **Few 2021 NAVO days.** The NCEI archive keeps one NAVO day in eight after March 2021, so the 2021 NAVO values use six days (MetOp-A) and ten satellite-days (MetOp-B). The MetOp-A orbit drifted in 2021 (before the end of its mission in November 2021), which can change the local observation time; this can explain part of the 2020-2021 fall of MetOp-A against the yardstick.
- **Control years.** For 2021 the control is 2020 (inside the Navy v2.0 period, with no input change on 1 October 2020), because the archive has no MetOp-B L3U files after mid-May 2022 until 2023. A seasonal pattern that is different in 2020 and 2021 can affect the estimate. The 2020 step against CCI uses no control year but has a clear significance against all other dates.
- **The DOISST internal processing is not public.** We infer what DOISST did from its output. We did not reproduce its bias correction or interpolation, and we did not test why the DOISST level does not follow the Navy input level.
- **The 2023 decrease** is reported, not explained; CCI ends on 22 June 2024.
- **Incomplete L3S check.** We started the same test with the ACSPO L3S-LEO reanalysis from NOAA CoastWatch ERDDAP. The server returned errors (HTTP 502) for all requests from 12 November 2026 09:10 PST, so that test is incomplete and not used. Its July 2020 part (55 days) gave a similar result (NAVO v1.0 near ACSPO, v2.0 0.05-0.07 C warmer).
- **Sampling.** Every 2nd ACSPO granule and, for 2019 and 2020 September-October, every 2nd NAVO granule. The 1-degree cell matching does not match the time of day inside a cell.

## Reproduction

Run outside the signed bundle, in a new scratch folder:

    bash files/code/run_all.sh files/ /path/to/scratch /path/to/datasets /path/to/b93b5f64...zip

`run_all.sh` downloads the exact NAVO and ACSPO granules listed in `files/lists/` from the NCEI GHRSST archive (about 40 GB in total, reduced and deleted one granule at a time), the iQuam files, then runs the reduction, analysis and figure scripts. Python 3.12 with numpy, scipy, pandas, netCDF4 and matplotlib; curl 7.66 or later (parallel transfers). The DOISST yearly files are the NOAA PSL files `sst.day.mean.YYYY.nc` (2016-2022). The reduced data are in the bundle, so the analysis can also run from them: `files/data/l3u_daily_1deg/AVHRRMTB_YYYYMMDD.npz` (yardstick day sums: n and s, shape 2 [night, day] x 120 [60S-60N] x 360) and `files/data/navo_daily_1deg.npz` (NAVO daily sums per satellite and version for the yardstick days). Granule URLs, sizes and SHA-256 values: `files/provenance/`.

On the Dell campaign host, the NCEI archive gave 1-15 MB/s; small L3U granules are latency-bound, so `l3u_reduce.py` downloads a day with one parallel curl call.

## Provenance and rights

- Job: sci-1107-dell-earth-and-ocean-sciences-b5c034488da0; campaign 11_07_2026; topic earth-and-ocean-sciences; machine dell; model Claude Opus 5.5 (claude-opus-5-5), Claude Code harness. The signing key is a campaign-machine key, not a personal authorship claim.
- External data are listed with URLs, versions and hashes in `files/provenance/` and in `files/NOTICE_external_data.md`. No raw third-party file is included. The bundled data are our 1-degree sums derived from NOAA and NAVO data (US Government data, no use restrictions), and aggregate tables derived from them, from DOISST (NOAA) and from the DOISST minus ESA SST CCI series of sci:sha256:b93b5f64 (ESA CCI SST data: CC BY 4.0; attribution in the notice).

## References

- Huang, B., et al. 2021: Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate, 34, 2923-2939, doi:10.1175/JCLI-D-20-0166.1.
- NOAA NCEI: Optimum Interpolation SST product page (satellite input changed from Navy SST to NOAA ACSPO SST for forward production on 1 October 2021, version v2.1a; v2.1b from 1 April 2023). https://www.ncei.noaa.gov/products/optimum-interpolation-sst
- NASA PO.DAAC, 29 July 2020: release of GHRSST NAVO MetOp-A/B/C L2P v2.0 datasets (new cloud screening, 4 km, no HIRS dependency, forward stream only).
- Petrenko, B., et al. 2014: Evaluation and selection of SST regression algorithms for JPSS VIIRS. J. Geophys. Res. Atmos., doi:10.1002/2013JD020637 (ACSPO regression).
- Embury, O., et al. 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, 11, 326, doi:10.1038/s41597-024-03147-w.
- Campaign publications: sci:sha256:b93b5f641725a35b93aae545fe514632c50f87c96781a135740caa4284434ab2, sci:sha256:645d0681260eda6f870bbbc6f00aea971c8e9bc5a85580f3bfdb63dae9189580, sci:sha256:9fca62cd8472d63d48b27ab8390b65ee3e06360adfbc14fea607fedf11a3e03a, sci:sha256:e75ccf52e92363fec7fb7cc59864cacc7dc5c18e3a08be6970bc69f9660df60a, sci:sha256:5cba350c208ed7bd77e5299827bffe69cdfc2df12c654969a0da37d5f35d5ec1, sci:sha256:656c3dbceac936baaa99dd73e44c22d123b9c9b6b6bf3a18e86a91b4d4226fd7, sci:sha256:dbf0934148316f153a19c429cf19908a4e4e213a22aa2decfe119df5dbcacb4b.
