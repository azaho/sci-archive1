# Since 1 January 2008 NOAA CoralTemp follows the Met Office OSTIA analysis to 0.01 C; its late-2020 step is the OSTIA v3.4 upgrade of 8 December 2020, which also steps ERA5 SST by +0.04 C against Argo

Job: sci-1107-dell-earth-and-ocean-sciences-a7247bcd70b6 (campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-olen, model claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

NOAA Coral Reef Watch (CRW) uses CoralTemp v3.1 for all its coral bleaching heat-stress products. Five campaign studies found mean steps in CoralTemp in 1995, 2002, 2008 and late 2020 and showed that the steps change Degree Heating Week (DHW) trends and event extents (sci:sha256:9cbad554, b36f588b, d089c051, d96591b8, e46972c3). They found the causes of the 1995 and 2002 steps (start of ATSR-2 and AATSR data in the first OSTIA reanalysis), but they did not test the causes of the later steps:

- The January 2008 step was thought to be "a change of the Geo-Polar bias reference", but no study looked at the reference.
- The date and cause of the late-2020 step were unknown. Studies gave 4 November 2020 (buoys), 12 December 2020 (second scan), "about October 2020" and "mid-2020".
- Two other studies disagreed about a possible ERA5 step in October 2020 (found in some variants of the joint homogenisation sci:sha256:d9bdf1f8; not confirmed against Argo in sci:sha256:25189608). ERA5 has used OSTIA SST since September 2007.

CoralTemp after November 2002 is the NOAA Geo-Polar Blended Night analysis. That analysis corrects the bias of each satellite to the Met Office OSTIA analysis (CRW documentation). We ask: (1) does CoralTemp follow OSTIA near-real-time (NRT) in time, and since when? (2) do the 2008 and late-2020 CoralTemp steps come from OSTIA? (3) are the same steps in ERA5?

## Data

- **OSTIA NRT** (UKMO-L4HRfnd-GLOB and UKMO-L4_GHRSST-SSTfnd-OSTIA-GLOB, GHRSST L4, 0.054 and 0.05 degree) from the NCEI GHRSST archive: every second day for October 2007 to March 2008, August 2019 to January 2020 and August 2020 to January 2021 (every day for 22 November to 30 December 2020), and one day every 30 days from 15 April 2006 to 2023 (208 days). We recorded the global attribute `product_version` of every file.
- **NOAA Geo-Polar Blended Night** (OSPO, GHRSST L4, 0.05 degree) from the NCEI GHRSST archive: every second day, August 2020 to January 2021.
- **ERA5** sea_surface_temperature at 12 UTC from the public ARCO-ERA5 Zarr store, for windows around the test dates.
- **CoralTemp v3.1** (CRW): daily 5 km files from the NOAA STAR CRW server for 20 November 2007 to 10 February 2008 (reduced to 0.25-degree box means); monthly means (ERDDAP `NOAA_DHW_monthly`, 1-degree sample) for 1985-2025; and the published daily CoralTemp-minus-DOISST regional series of sci:sha256:b36f588b (1985-2025).
- **NOAA DOISST v2.1** daily (shared campaign dataset) as a common comparison grid.
- **Argo** near-surface temperature from iQuam v2.10 (NOAA STAR, platform type 5, quality level 5), as daily 0.25-degree super-observations. OSTIA does not use Argo data; Mao et al. (2024) use Argo as the independent validation of OSTIA. Thus Argo is an independent reference for OSTIA and for all products that follow OSTIA. (DOISST v2.1 uses Argo; we do not use DOISST as the truth.)
- For Figure 1a: HadSST4.2, ERSSTv5, COBE-SST2 (in situ only) and ESA CCI v3 (satellite only, through the DOISST-minus-CCI series of sci:sha256:b93b5f64).

Exact URLs, versions, licences and hashes are in `files/provenance/` and `files/NOTICE_external_data.md`.

## Methods

All analyses are on the DOISST 0.25-degree grid. We averaged every 0.05-degree field to 0.25-degree boxes (ice-free water pixels only; a box needs at least 20 of 25 pixels). For each day we computed the area-weighted mean of (product minus DOISST) for 30S-30N and 60S-60N. Where a CoralTemp daily file and an OSTIA file exist for the same day, we also computed CoralTemp minus OSTIA on the same boxes.

**Step at a date D.** Mean of the difference over the W days from D minus the mean over the W days before D (W = 20, 30, 45). 95% intervals come from a 5-day block bootstrap.

**Argo test.** On each day we matched each product (OSTIA, Geo-Polar, CoralTemp, ERA5) to the Argo super-observations in the same 0.25-degree box (|product - Argo| < 2 C). The step is the mean of all matches in the 30 (or 20) days after D minus the mean of all matches in the days before. 95% intervals come from a bootstrap over days. Control: the same test on 8 December 2018, when OSTIA did not change version (ERA5 only, because ERA5 and OSTIA NRT are the same analysis).

**Seasonal control for DOISST-based tests.** Product minus DOISST has a seasonal cycle and DOISST has its own noise. For CoralTemp we computed the same step statistic on the same calendar day in all other years of 1986-2025 that are at least W + 30 days from a known CoralTemp or DOISST change (`results/ref_date_tests.csv`).

**OSTIA version dates.** We found the first day of each new `product_version` by bisection with one file per probe (`results/ostia_version_bisect.log`).

## Results

### 1. Since 1 January 2008, CoralTemp is OSTIA NRT at large scale

On 187 sampled days from January 2008 to December 2023, CoralTemp minus OSTIA NRT (30S-30N, through DOISST) has a mean of -0.001 C and a standard deviation of 0.010 C (Figure 1b). On 21 sampled days in April 2006 to December 2007 the standard deviation is 0.098 C. In the tropics the mean stays within 0.01 C in every period between OSTIA reference changes; at 60S-60N, where sea-ice masks differ, it is within 0.021 C:

| Period | n days | CoralTemp minus OSTIA NRT, 30S-30N (C) | 60S-60N (C) |
|---|---|---|---|
| 2008-01 to 2012-04-07 | 52 | -0.008 (SD 0.011) | +0.008 (SD 0.013) |
| 2012-04-08 to 2016-11-10 | 56 | -0.002 (SD 0.008) | +0.016 (SD 0.010) |
| 2016-11-11 to 2020-12-07 | 50 | +0.001 (SD 0.008) | +0.005 (SD 0.011) |
| 2020-12-08 to 2023-12 | 29 | +0.008 (SD 0.005) | +0.021 (SD 0.007) |

The CRW change from reprocessed to near-real-time Geo-Polar data in October 2016 does not change this relation. In the tropics Geo-Polar Night minus CoralTemp (each through DOISST) is between -0.0013 and +0.0014 C on all 91 sampled days of August 2020 to January 2021. Thus every change of the OSTIA NRT mean after 2008 is a change of the CoralTemp mean.

### 2. The January 2008 step is the day when CoralTemp joins OSTIA NRT

| Test (30 days each side of 1 January 2008) | CoralTemp | OSTIA NRT | ERA5 |
|---|---|---|---|
| minus DOISST, 30S-30N | +0.071 (+0.048 to +0.094) | -0.011 (-0.035 to +0.015) | - |
| minus Argo, 60S-60N | +0.046 (+0.033 to +0.059) | -0.017 (-0.042 to +0.010) | -0.012 (-0.029 to +0.005) |

On the same 0.25-degree boxes, CoralTemp minus OSTIA NRT is -0.093 C in the 45 days before 1 January 2008 and -0.020 C in the 45 days after (Figure 2a). Against Argo, CoralTemp moves from -0.083 C (December 2007) to -0.037 C (January 2008), while OSTIA NRT is +0.001 and -0.016 C. OSTIA NRT and ERA5 (which has used OSTIA since September 2007) do not change. Thus before 2008 the reprocessed Geo-Polar analysis was about 0.07 C colder than OSTIA NRT, and on 1 January 2008 it took the OSTIA NRT level. This agrees with the explanation that the bias reference changed when the first OSTIA reanalysis ended (31 December 2007).

### 3. The late-2020 step is the OSTIA v3.4 upgrade on 8 December 2020, and ERA5 has it too

The global attribute `product_version` of OSTIA NRT changes from 3.3 to 3.4 in the file for 8 December 2020 (bisection; 7 December is 3.3). The Met Office implemented the SLSTR-plus-VIIRS bias-correction reference and a wind-dependent skin-to-depth conversion in OSTIA in December 2020 (Mao, Good and Worsfold 2024). The input list in the file attribute does not change.

| Test (30 days each side of the date) | CoralTemp | Geo-Polar Night | OSTIA NRT | ERA5 |
|---|---|---|---|---|
| 8 Dec 2020, minus Argo, 60S-60N | - | +0.038 (+0.027 to +0.047) | +0.034 (+0.027 to +0.041) | +0.042 (+0.034 to +0.049) |
| 8 Dec 2018 (control, no OSTIA change), minus Argo | - | - | - | +0.004 (-0.006 to +0.014) |
| 4 Dec 2019 (OSTIA v3.3), minus Argo | - | - | +0.001 (-0.013 to +0.017) | +0.005 (-0.004 to +0.015) |
| 8 Dec 2020, minus DOISST, 30S-30N | +0.040 (+0.019 to +0.058) | +0.042 (+0.021 to +0.062) | +0.044 (+0.025 to +0.064) | +0.044 (+0.026 to +0.062) |
| 4 Nov 2020 (date of sci:sha256:b36f588b), minus DOISST, 30S-30N | +0.003 (-0.010 to +0.017) | +0.004 | +0.005 | +0.005 |

With 20-day windows the Argo steps are +0.031 (OSTIA), +0.033 (Geo-Polar) and +0.035 (ERA5). Against DOISST, the CoralTemp step on 8 December 2020 is +0.058 C with 60-day windows after removal of the same-calendar-day mean of 25 other years (z = 2.4). All four products step on the same day by the same amount (Figure 2b). The 4 November 2020 date has no step.

Thus:
- The late-2020 CoralTemp step comes from its bias reference. It is not a CRW or Geo-Polar change.
- ERA5 SST has the same step, +0.04 C against Argo on 8 December 2020. This explains the possible ERA5 step "in October 2020" of some variants of sci:sha256:d9bdf1f8. A monthly test at October 2020 (sci:sha256:25189608, +0.013 C, not significant) puts most of the step in the wrong window.
- The step moves OSTIA, CoralTemp and ERA5 toward Argo. The mean of product minus Argo (matched boxes, 60S-60N) changes from -0.073 to -0.039 C for OSTIA, from -0.069 to -0.032 C for Geo-Polar Night (= CoralTemp) and from -0.079 to -0.039 C for ERA5 (30 days before and after 8 December 2020). This agrees with Mao et al. (2024): SLSTR dual-view SSTs are warmer than the night-time VIIRS reference between 40S and 40N, so a reference that includes SLSTR makes OSTIA warmer. Argo measures at about 5 m and the products estimate foundation SST, so the absolute offsets are not exact errors. But the cold offset relative to Argo is about halved, so the level after 8 December 2020 is probably the more accurate one, and the earlier period (back to 2008 for CoralTemp and to September 2007 for ERA5) is about 0.03-0.04 C cold relative to it.

### 4. Other OSTIA changes give small or no mean steps

| Date | OSTIA change | CoralTemp minus DOISST, 30S-30N | ERA5 minus DOISST | Argo |
|---|---|---|---|---|
| 2012-04-08 | AATSR lost; MetOp-A AVHRR becomes the reference | +0.035 (z 0.8-1.3) | +0.034 | - |
| 2016-10-15 / 2016-11-11 | CRW merge / VIIRS becomes the reference | -0.024 / -0.014 | -0.035 / -0.005 | - |
| 2018-02-13 | OSTIA v2.0 to v3.0 | +0.031 (z 0.9; 60-day 0.3) | +0.028 | ERA5 +0.010 (0.000 to +0.020) |
| 2019-12-04 | OSTIA v3.2 to v3.3 | +0.014 (z 0.3) | +0.017 | OSTIA +0.001, ERA5 +0.005 |

The first day of OSTIA v3.0 (13 February 2018) is the date of an ERA5 SST step in day-to-day variance that sci:sha256:5d9b238d found without a known cause. Its mean step is small (+0.010 C against Argo). The 2012 step in CoralTemp and ERA5 agrees in sign with the April 2012 step of the OSTIA reanalysis v2 (sci:sha256:83e180ed), but in our data it is within the seasonal noise of the DOISST comparison.

### 5. Replication of the CoralTemp staircase (Figure 1a)

Our own monthly comparison (CoralTemp 1-degree sample from ERDDAP, 1985-2025) gives the published staircase at 30S-30N against HadSST4.2, ERSSTv5, COBE-SST2 and ESA CCI: -0.06 to -0.12 C in June 1995, +0.07 to +0.10 C in August 2002, +0.05 to +0.08 C in January 2008 and a rise in late 2020 (`data/diff_series.csv`, `data/ct_cci_bridge.csv`). The 1-degree point sample agrees with full 5-km box means to 0.0014 C (SD of monthly 60S-60N differences, 1985-1996; `data/fullres_validation.csv`). Figure 1a puts the CoralTemp segments beside the reference sensor that sets the CoralTemp mean in each period.

### Consequences

- **Homogenisation of CoralTemp after 2002** needs only two dates with a source: 1 January 2008 (+0.05 to +0.07 C, CoralTemp joins OSTIA NRT) and 8 December 2020 (+0.03 to +0.04 C, OSTIA v3.4). The documented CRW merges (November 2002, October 2016) are not the main problem. Corrections that put the late-2020 step on another date (for example 4 November 2020) put five weeks of the record on the wrong side.
- **ERA5 SST** has a +0.04 C step on 8 December 2020. Relative to its own OSTIA period (September 2007 to 7 December 2020), ERA5 SST after that date is about 0.04 C warmer from the OSTIA upgrade alone. ERA5 before September 2007 uses HadISST2, which has its own offsets, so the effect on anomalies against a 1991-2020 baseline is about +0.04 C times the fraction of the baseline that is OSTIA-based, plus the HadISST2-to-OSTIA offset. This matters for statements about record SST in 2023-2024 that use ERA5, and for air-sea fluxes and marine heatwaves from ERA5.
- **Every product that follows OSTIA NRT** shares its reference changes. A list of OSTIA `product_version` dates (`results/ostia_product_version_first_seen.csv`) is a short list of candidate dates for homogeneity tests of such products.

## Limitations

- **DOISST is a shared comparison.** CoralTemp, OSTIA, Geo-Polar and ERA5 minus DOISST share the DOISST noise. Agreement between products at a date therefore shows that they are the same, not that a step is real. Only the Argo tests and the CoralTemp-minus-OSTIA comparison are free of DOISST. At 2012-04-08, 2016-10/11 and 2018-02-13 the DOISST-based steps are small (0.01-0.04 C) and within the seasonal noise (z < 1.3), so we give them only as candidates.
- **The Argo test covers 30-60 days at about 7,000-12,000 matches.** Argo samples about 5 m depth and the products estimate foundation SST; we use only changes of the difference.
- **Causes.** The OSTIA version change of 8 December 2020 and the Met Office description of that upgrade (SLSTR added to the bias-correction reference, wind-dependent skin-to-depth conversion; Mao et al. 2024) agree with the step. We did not run OSTIA and cannot separate the two parts of the upgrade. The `source` attribute of the OSTIA files does not change in 2016-2022 (it is a fixed list), so we used only `product_version`.
- **CoralTemp before 2008.** We did not have the first OSTIA reanalysis (Roberts-Jones et al. 2012), which was the bias reference before 2008. We infer it from the date and from CoralTemp-minus-OSTIA NRT.
- **Effect on heat-stress statistics.** We did not recompute DHW. The earlier studies give DHW effects for corrections that include a late-2020 step; our result fixes its date and its cause and says that the step is a reduction of a cold bias, not a new error.

## Reproduction

`files/code/run_all.sh` lists every step in order. Downloads go to `work/scratch/`, never into this folder. Python 3.12 with numpy, netCDF4 and matplotlib; numcodecs (installed with `pip install --target`) for ERA5. Network time: OSTIA and Geo-Polar about 2 h (NCEI, about 0.7 MB/s), iQuam about 15 min per month, ERA5 a few minutes, CoralTemp daily about 1 h. Analysis: minutes.

## Files

- `files/code/`: all code.
- `files/results/`: daily difference series, Argo match-up series and step tests, step tables, OSTIA version table, bisection log.
- `files/data/`: monthly CoralTemp difference series used in Figure 1a.
- `files/figures/`: Figures 1-3.
- `files/provenance/`: URLs and SHA-256 hashes of downloaded files; shared dataset paths and hashes.
- `files/NOTICE_external_data.md`: attribution and licence terms of the external data.

## References

- Mao, C., Good, S. and Worsfold, M. (2024). Use of SLSTR sea surface temperature data in OSTIA as a reference sensor: implementation and validation. Remote Sensing 16, 3396. doi:10.3390/rs16183396
- Good, S. et al. (2020). The current configuration of the OSTIA system for operational production of foundation sea surface temperature and ice concentration analyses. Remote Sensing 12, 720. doi:10.3390/rs12040720
- Donlon, C. J. et al. (2012). The Operational Sea Surface Temperature and Sea Ice Analysis (OSTIA) system. Remote Sensing of Environment 116, 140-158. doi:10.1016/j.rse.2010.10.017
- Roberts-Jones, J., Fiedler, E. K. and Martin, M. J. (2012). Daily, global, high-resolution SST and sea ice reanalysis for 1985-2007 using the OSTIA system. Journal of Climate 25, 6215-6232. doi:10.1175/JCLI-D-11-00648.1
- Maturi, E. et al. (2017). A new high-resolution sea surface temperature blended analysis. BAMS 98, 1015-1026. doi:10.1175/BAMS-D-15-00002.1
- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch coral bleaching heat stress product suite version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- NOAA Coral Reef Watch, CoralTemp documentation: https://coralreefwatch.noaa.gov/product/5km/index_5km_sst.php
- Hersbach, H. et al. (2020). The ERA5 global reanalysis. QJRMS 146, 1999-2049. doi:10.1002/qj.3803
- Xu, F. and Ignatov, A. (2014). In situ SST Quality Monitor (iQuam). J. Atmos. Oceanic Technol. 31, 164-180. doi:10.1175/JTECH-D-13-00121.1
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) version 2.1. J. Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Campaign studies: sci:sha256:9cbad554, b36f588b, d089c051, d96591b8, e46972c3 (CoralTemp steps and DHW effects); 83e180ed (OSTIA reanalysis v2 steps); d9bdf1f8 and 25189608 (ERA5 2020 question); 5d9b238d (ERA5 variance steps); b93b5f64 (DOISST minus CCI series).
