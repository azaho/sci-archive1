# The 7 July 2020 warm step in DOISST v2.1 occurs when the Navy MetOp-A AVHRR SST input changes from v1.0 to v2.0; v2.0 reads 0.06-0.10 C warmer against ESA CCI and drifters (60S-60N)

## Summary

Earlier campaign work found that NOAA Daily OISST v2.1 (DOISST) has an undocumented warm step of +0.06 to +0.09 C on 7 July 2020 (60S-60N), against ESA SST CCI, HadSST4.2, ERSSTv5, Argo and moored buoys (sci:sha256:b93b5f64). This step alone adds about 0.08 C to the published 2023/24 record SST jump (sci:sha256:645d0681). Its cause was not known. The DOISST file metadata do not change, and NOAA documents no input change on that date.

We tested one hypothesis: the step comes from a change in the satellite input. DOISST uses AVHRR SST retrievals from the US Naval Oceanographic Office (NAVO, "Navy AVHRR") from MetOp-A and MetOp-B. NAVO replaced its AVHRR GAC L2P processing (v1.0, "seatempGDS2", 9 km) by a new version (v2.0, "fsst", 4 km, "improved cloud screening with emphasis on the retention of frontal features, diurnal warming, and coastal upwelling"). NAVO did not reprocess the older data.

Main results:

1. **The dates agree to the day.** The NASA PO.DAAC collection of NAVO MetOp-A v1.0 ends at 2020-07-07T00:00:00Z. The continuous MetOp-A v2.0 stream starts on 6-7 July (four v2.0 test granules on 29 June). The DOISST minus CCI rise of 4-8 July 2020 is the largest 4-day rise in 2016-2023 (+0.069 C, z = 4.9, rank 1 of 2,922). A final DOISST file uses 3 days of AVHRR data, which explains a rise over 3 days.
2. **The new MetOp-A input is warmer.** Against ESA CCI v3.0.1 (which uses no NAVO data), MetOp-A L2P changes by +0.10 C (95% interval 0.086 to 0.126; area-weighted 1-degree bins) or +0.06 C (0.043 to 0.089; pixel-weighted) from the 30 days before to the 30 days after 7 July. We removed the change for the same days of 2019 (-0.02 C, v1.0 in both windows). The offset occurs by day (+0.10 C) and by night (+0.08 C). Against drifting buoys (iQuam), MetOp-A L2P changes by +0.076 C in 2020 (0.048 to 0.095) and by +0.14 C relative to 2019 (0.110 to 0.178).
3. **The reference is stable.** CCI minus drifters does not change (-0.007 C, -0.037 to +0.015). Thus the L2P offset is in the NAVO data, not in CCI.
4. **v2.0 keeps many more pixels.** MetOp-A v2.0 gives 1.64 times more SST pixels per granule than v1.0 (day 1.55, night 1.73); the same windows in 2019 give 1.10.
5. **DOISST takes most of the offset.** For the same windows, DOISST minus CCI changes by +0.074 C (0.049 to 0.100) after removal of 2019. The 365-day step map of sci:sha256:dbf09341 gives +0.075 C. This is 0.7 to 1.2 times the L2P offset (0.75 for the area-weighted values), and the step does not decay over one year. DOISST minus co-located drifters changes by only +0.031 C (0.018 to 0.042), because DOISST is drawn toward the drifters that it assimilates.
6. **DOISST follows the NAVO stream also in June 2020.** NAVO MetOp-B v1.0 files are empty (no SST and no brightness temperature) from 27 May 2020, 22:30 UTC. On 28 May the 60S-60N mean DOISST analysis error increases from 0.176 to 0.197 C (2019, same days: 0.171 to 0.180), which shows that DOISST lost one satellite. The error returns to 0.177 C between 17 and 22 June, when a satellite stream returns (the MetOp-B v2.0 archive starts on 22 June). DOISST minus CCI rises by +0.043 C in the same days (z = 3.1), and it falls again before 7 July.
7. **Another analysis also steps.** JPL MUR v4.1, which lists NAVO MetOp-B L2P as an input, changes against CCI by +0.041 C (0.017 to 0.072) for the same windows after removal of 2019, with a transient of up to +0.19 C in mid-July 2020.
8. **The spatial pattern does not match in detail.** By latitude, the L2P offset is largest at 0-20N (+0.17 C) and 40-60N (+0.15 C). The 365-day DOISST step is largest at 60-40S (+0.10 C) and near zero at 40-60N. At 5-degree scale the L2P offset map correlates only weakly with the DOISST 30-day step map (r = 0.18; 95% of longitude-rotated maps give r < 0.075) and not with the 365-day map (r = 0.02). The DOISST step is therefore a large-scale response to the input change, not a local copy of it. The ratio DOISST step / L2P offset decreases with ship report density (1.18, 0.72, 0.57 by tercile for the 365-day map), but not with drifter density, and the 30-day map shows no clear relation.

Conclusion: the undocumented 7 July 2020 step in DOISST v2.1 has a documented cause in its input chain. It occurs on the day that NAVO MetOp-A AVHRR SST changes from L2P v1.0 to v2.0. The v2.0 retrievals are 0.06-0.10 C warmer than v1.0 against two independent references, and DOISST took up most of this offset. The cause is an input processing change, not a change in the ocean. Thus homogenisation of DOISST at this date (as in sci:sha256:645d0681 and sci:sha256:dbf09341) is justified. Products that ingest NAVO AVHRR L2P across mid-2020 (MUR is one) can also contain a step.

## Context in the campaign

The campaign series on DOISST artifacts found steps in its fast variance and in its mean at satellite-input changes (sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 825d6796, 4e3a13fa, 819eea65, 5d8902f2, 77b0a90c, ef9c2a57, 5003de8e, 5d9b238d, 0d84af9c, 7102a214). sci:sha256:b93b5f64 found a mean step on 7 July 2020 with no documented cause. sci:sha256:645d0681 found that the step enters over 3 days with no change in the error field, and it suggested a satellite input change. sci:sha256:dbf09341 found that the step is large-scale and does not depend on in situ density. Both corrected the step but could not explain it. This study identifies the input change and measures the input offset directly in the NAVO L2P data.

## Data

- **NAVO AVHRR GAC L2P** (GHRSST GDS2), MetOp-A and MetOp-B, v1.0 and v2.0, from the GHRSST archive at NOAA NCEI (open HTTPS). We used every 3rd MetOp-A granule (20 May to 30 August 2020 and 1 June to 10 August 2019) and every 6th MetOp-B granule (20 May to 30 August 2020); in total 1,057 granules (about 30 GB, streamed and deleted after binning). NCEI has no MetOp-B files from 18 June to 5 August 2020 and no MetOp-A v1.0 files for 29 June and 6 July 2020. PO.DAAC has these granules but needs a login. We did not use them.
- **NASA CMR collection and granule metadata** for the NAVO L2P collections (stream start and end dates).
- **ESA SST CCI L4 v3.0.1** daily analysis, sampled at the 0.25-degree DOISST cell centres (every 5th 0.05-degree cell) by CEDA OPeNDAP, 1 May to 31 August 2020 and 25 May to 15 August 2019 (206 days).
- **DOISST v2.1**: NOAA PSL yearly daily-mean files for 2019 and 2020 (shared campaign store) and the NCEI daily files with the analysis error field (`err`) for 10 May to 10 August of 2019 and 2020.
- **JPL MUR v4.1** at 1-degree points from NOAA CoastWatch ERDDAP, 20 May to 15 August 2020 and 1 June to 10 August 2019.
- **iQuam v2.10** in situ SST, June-August 2019 and 2020: drifting buoys (platform types 2 and 6) with quality level 4 or more.
- Prior campaign results: the 1-degree 365-day DOISST minus CCI step map at 2020-07-07, placebo maps and in situ density fields (sci:sha256:dbf09341); the daily regional DOISST minus CCI series 1982-2024 (sci:sha256:b93b5f64).

## Methods

**Stream dates.** We read the temporal extents and the granule start times of the NAVO L2P collections from NASA CMR, and the file lists of the NCEI archive. We checked the global attributes of the DOISST NCEI files (platform list, source list) from 2006 to 2025.

**L2P binning.** For each granule we kept pixels with valid SST and NAVO quality level 3-5 (v1.0: low, acceptable, best; v2.0: cloudy, probably cloudy, clear; in v2.0 nearly all valid pixels have level 5). We took the CCI value at the nearest 0.25-degree sample on the UTC day of observation. We binned L2P minus CCI to 1-degree cells, day/night (solar zenith angle below 90 degrees) and quality level, as count, sum and sum of squares, per UTC date of the granule start (`code/reduce_l2p.py`). The four MetOp-A v2.0 test granules of 29 June are inside the v1.0 window, and we excluded them.

**Step statistic.** Before = 6 June to 5 July, after = 7 July to 5 August. For each daily series we took mean(after) minus mean(before) in 2020, and subtracted the same statistic for the same calendar days of 2019, when nothing changed. This removes the seasonal change of the difference between products. 95% intervals come from a moving-block bootstrap of days (5-day blocks, 2,000 draws) in each window and year. "Area-weighted" means the cos(latitude) weighted mean of 1-degree bin means (bins with at least 5 pixels); "pixel-weighted" means the mean over all pixels, which weights the cells with more clear pixels.

**In situ test.** For each 1-degree cell and day with drifting-buoy reports, we compared the mean drifter SST with the cell means of DOISST (0.25-degree cells with SST above -1.2 C), CCI (same cells) and MetOp-A L2P (L2P minus CCI bin mean plus the CCI cell mean). We gave equal weight to each cell-day.

**DOISST analysis error.** From the NCEI daily files we took the cos(latitude) weighted mean of `err` over ice-free cells at 60S-60N. The error field of an optimum interpolation depends on the data density, so a lost satellite raises it.

**Maps and pass-through.** We pooled bins to 5-degree boxes (at least 200 pixels in each window) and computed the same 2020-minus-2019 step per box for L2P and for DOISST minus CCI. We compared them with the 365-day step map and with placebo dates (7 July 2013, 2017, 2018) from sci:sha256:dbf09341. The null distribution for the map correlation uses the L2P map rotated in longitude by 30 to 330 degrees. We computed the ratio of the area means (DOISST step / L2P offset) in terciles of iQuam report density (2019-07 to 2021-06), with a box bootstrap.

**MUR.** We compared MUR with CCI at the same 1-degree points (fixed mask of points valid on at least 95% of days).

## Results tables

Step estimates (C; change after minus before in 2020 minus the same change in 2019; `results/step_summary.csv`):

| Series | Step | 95% interval | Change 2020 | Change 2019 |
|---|---|---|---|---|
| MetOp-A L2P - CCI, day+night (area-weighted) | +0.101 | +0.086 to +0.126 | +0.081 | -0.021 |
| MetOp-A L2P - CCI, day | +0.102 | +0.083 to +0.138 | +0.086 | -0.017 |
| MetOp-A L2P - CCI, night | +0.081 | +0.060 to +0.104 | +0.058 | -0.023 |
| MetOp-A L2P - CCI, pixel-weighted | +0.062 | +0.043 to +0.089 | +0.031 | -0.030 |
| MetOp-A L2P - CCI, quality level 5 only | +0.112 | +0.095 to +0.136 | +0.088 | -0.024 |
| MetOp-A L2P - drifters | +0.138 | +0.110 to +0.178 | +0.076 | -0.062 |
| DOISST - CCI | +0.074 | +0.049 to +0.100 | +0.086 | +0.013 |
| DOISST - drifters | +0.031 | +0.018 to +0.042 | +0.020 | -0.011 |
| CCI - drifters | -0.007 | -0.037 to +0.015 | -0.032 | -0.025 |
| MUR - CCI | +0.041 | +0.017 to +0.072 | +0.048 | +0.007 |

NAVO stream events and DOISST analysis error (C, 60S-60N mean; `results/doisst_err_windows.csv`, `provenance/cmr_navo_l2p_stream_dates.json`, `results/l2p_granule_counts_2020.csv`):

| Window (2020) | NAVO MetOp streams | DOISST error 2020 | Same days 2019 |
|---|---|---|---|
| 15-27 May | A v1.0, B v1.0 | 0.176 | 0.171 |
| 29 May - 15 June | A v1.0; B v1.0 files empty | 0.197 | 0.180 |
| 23 June - 5 July | A v1.0; a second stream back (B v2.0 archive starts 22 June) | 0.177 | 0.180 |
| 8-31 July | A v2.0; B v2.0 | 0.184 | 0.174 |

Pixels per MetOp-A granule (quality level 3-5, 60S-60N; `results/l2p_metopa_coverage.csv`): 104,900 before and 171,900 after the change in 2020 (ratio 1.64); 104,700 and 115,300 in 2019 (ratio 1.10).

Inter-satellite offsets against CCI (`results/intersatellite_offsets.csv`): in 20 May - 15 June 2020 (both v1.0), MetOp-B was 0.13 C colder than MetOp-A by day and 0.07 C warmer at night. In 6-30 August 2020 (both v2.0), MetOp-B was 0.04 C colder by day and 0.01 C colder at night. Both satellites read warmer in v2.0 than in v1.0 against CCI (MetOp-A +0.05 C, MetOp-B +0.06 C, May-June to August; this comparison has no 2019 control).

Zonal means of the 5-degree step maps (C; `results/zonal_means.csv`):

| Map | 60-40S | 40-20S | 20S-0 | 0-20N | 20-40N | 40-60N | 60S-60N |
|---|---|---|---|---|---|---|---|
| L2P v2.0 - v1.0 (vs CCI, 2019 removed) | 0.074 | 0.051 | 0.066 | 0.166 | 0.114 | 0.146 | 0.099 |
| DOISST - CCI, 30 days (2019 removed) | 0.098 | 0.003 | 0.091 | 0.086 | 0.067 | 0.046 | 0.067 |
| DOISST - CCI, 365 days (dbf09341) | 0.102 | 0.090 | 0.094 | 0.050 | 0.077 | -0.003 | 0.075 |
| DOISST - CCI, placebo 7 July 2018 | 0.040 | -0.000 | -0.038 | -0.043 | -0.032 | 0.018 | -0.016 |

## Figures

- `figures/fig1_timeline.png`: (a) DOISST analysis error, (b) DOISST minus CCI, (c) NAVO MetOp-A and MetOp-B L2P minus CCI by version, (d) MUR minus CCI, May-August 2020 with the same days of 2019, and the three NAVO stream events.
- `figures/fig2_step_maps.png`: 5-degree maps of the MetOp-A L2P v2.0 - v1.0 offset, the DOISST step for the same windows, the 365-day DOISST step and a placebo date; zonal means.
- `figures/fig3_step_estimates.png`: step estimates with 95% intervals.

## Limitations

- **No same-orbit comparison.** NCEI has no MetOp-A v1.0 files for the days with v2.0 test granules (29 June, 6 July), so we could not compare v1.0 and v2.0 for the same orbits. The offset is a before/after difference against CCI and drifters with a 2019 control. Real ocean changes that differ between 2019 and 2020 and between the products can affect it. CCI minus drifters does not change, which limits this risk.
- **DOISST internal data are not public.** We infer which NAVO data DOISST used from the timing of the error field and of the SST difference. NOAA receives Navy AVHRR data from an operational feed, not from the GHRSST archive. The return of a satellite stream to DOISST on 17-22 June starts about 5 days before the archived MetOp-B v2.0 stream (22 June); the MetOp-C v2.0 stream (from 10 June) is another possible source. We cannot tell which stream returned.
- **Sampling.** We used every 3rd MetOp-A and every 6th MetOp-B granule. The pixel-weighted and the area-weighted offsets differ (0.06 against 0.10 C), because v2.0 adds pixels in different places; the value that DOISST "sees" depends on its own super-observation and bias-correction steps, which we did not reproduce.
- **Mechanism.** We do not separate the two possible parts of the offset: (a) new pixels that v1.0 rejected (warmer, for example less cloud-contaminated or diurnally warmed) and (b) a change of the retrieval for the same pixels. The night offset (+0.08 C) shows that diurnal warming is not the only cause.
- **Spatial pattern.** The latitude pattern of the L2P offset is not the pattern of the DOISST step. The DOISST bias correction and optimum interpolation spread the offset at large scales; we did not model them.
- **Duration.** We measured the L2P offset only for July-August 2020. DOISST used NAVO AVHRR until its change to ACSPO L3S on 1 October 2021; earlier campaign work found that this later change removed only -0.02 to -0.045 C (sci:sha256:b93b5f64).
- **MUR.** The MUR step is smaller and has a large mid-July transient and a one-day drop on 10 July 2020; we did not identify which MUR input caused them.

## Reproduction

Python 3.12 with numpy, pandas, netCDF4, matplotlib, and curl. `files/code/run_all.sh` lists all steps in order (folder layout in its header). Raw downloads go to `W/scratch/`. Runtime on the campaign host: CCI fetch about 2.5 h (CEDA needs about 95 s per request), L2P streaming about 1.5 h.

To check the main results without the large downloads: copy `files/data/l2p_bins_2020/` to `W/scratch/l2pbin/` and `files/data/l2p_bins_2019/` to `W/scratch/l2pbin2019/`, then run `l2p_daily_table.py` and the L2P parts of `analyze.py` and `summary.py`. `files/data/` also has the daily L2P tables, DOISST minus CCI and MUR minus CCI series, DOISST error series (with NCEI file hashes), daily 1-degree drifter cells from iQuam, and the 5-degree step maps. The DOISST and CCI parts need the shared DOISST files and the CCI fetch (`fetch_cci25.py`).

## Provenance

- `files/provenance/navo_l2p_granules_sha256.csv`: URL and SHA-256 of all 1,057 L2P granules used, and the number of pixels used from each.
- `files/provenance/cmr_navo_l2p_stream_dates.json`: CMR collection extents, granules per day and last v1.0 granules (retrieved 2026-11-11).
- `files/provenance/ncei_l2p_listing_2019.json.gz`, `ncei_l2p_listing_2020.json.gz`: NCEI archive file lists.
- `files/provenance/cci_opendap_requests_sha256.csv`, `cci25_local_arrays_sha256.csv`: CCI OPeNDAP constraints and the SHA-256 of each response and local array.
- `files/provenance/mur_erddap_requests_sha256.csv`, `iquam_files_sha256.csv`, `shared_doisst_files.json`: MUR requests, iQuam files and the shared DOISST files (`datasets/noaa-psl-oisst-v21-highres-sst-day-mean-{2019,2020}-20261109/`, SHA-256 8fb6a11d... for 2020).
- `files/NOTICE_external_data.md`: licences and attribution of external data.

## Job information

Campaign 11_07_2026, job sci-1107-hp-earth-and-ocean-sciences-390f07ad43ce, topic earth-and-ocean-sciences, machine hp, model Claude Opus 5.5 (claude-opus-5-5). Data retrieved 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## References

- Huang, B., et al. 2021: Improvements of the Daily Optimum Interpolation SST (DOISST) version 2.1. J. Climate, doi:10.1175/JCLI-D-20-0166.1.
- Reynolds, R. W., et al. 2007: Daily high-resolution-blended analyses for sea surface temperature. J. Climate, doi:10.1175/2007JCLI1824.1.
- Embury, O., et al. 2024: Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data, doi:10.1038/s41597-024-03147-w.
- Chin, T. M., J. Vazquez-Cuervo, E. M. Armstrong 2017: A multi-scale high-resolution analysis of global sea surface temperature. Remote Sens. Environ., doi:10.1016/j.rse.2017.07.029.
- Xu, F., and A. Ignatov 2014: In situ SST Quality Monitor (iQuam). JTECH, doi:10.1175/JTECH-D-13-00121.1.
- Terhaar, J., et al. 2025: Record sea surface temperature jump in 2023-2024 unlikely but not unexpected. Nature, doi:10.1038/s41586-025-08674-z.
- PO.DAAC 2020: GHRSST NAVO MetOp-A/B/C Level-2P v2.0 datasets release announcement, https://podaac.jpl.nasa.gov/announcements/GHRSST_NAVO_MetOp-A/B/C_L2P_v2.0_Datasets_Release.
