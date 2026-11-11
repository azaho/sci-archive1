# Two polar splices in NOAA DOISST v2.1 (2005 ice input, 2016 ice-to-SST method) hide the 2005–2025 Arctic summer SST warming, make false post-2016 cold-spell rises at both poles and corrupt the OISST ice trends

Job `sci-1107-dell-earth-and-ocean-sciences-ba773b25cbac` (campaign 11_07_2026), topic earth-and-ocean-sciences, machine dell, account claude-olen, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work showed that NOAA DOISST (OISST) v2.1 has noise steps at satellite input changes between 60°S and 60°N. That work did not examine the polar oceans. Many Arctic and Antarctic marine heatwave (MHW), cold-spell and SST-trend studies use DOISST poleward of 60°. Here we test the two documented polar input changes in DOISST v2.1:

1. **1 January 2005: ice input changes from NASA GSFC to the NCEP ice analysis.** On this day the DOISST ice field gains +1.11 million km² of extent (≥15%) in the north and +1.48 million km² in the south, relative to the NSIDC Sea Ice Index v4. ERA5 ice has no step on this date (+0.01 and −0.00 million km²). After 2005 the DOISST excess grows. In summer it reaches +2 million km² in the Arctic and up to +5 million km² in the Antarctic. As a result, the DOISST ice field gives a 1982–2025 annual-mean extent trend of −0.10 million km² per decade in the Arctic (NSIDC: −0.52; ERA5: −0.55). In the Antarctic it gives +0.75 million km² per decade (NSIDC: −0.11; ERA5: −0.16), which is the wrong sign.
2. **1 January 2016: v2.1 starts.** NOAA kept v2.1 identical to v2.0 before 2016. We confirm this for all cells in December 2015. From 2016, v2.1 uses a freezing-point ice-to-SST conversion, Argo data and a new ship correction. NCEI continued to produce v2.0 until April 2020. This gives a direct counterfactual for 1,578 days. Poleward of 60°N, v2.1 minus v2.0 is −0.43 °C in July (area mean) and −1.34 °C in cells with 35–50% ice. Most of the offset is in cells with partial ice (Figure 2). In July–September, 37% of the Arctic offset is in cells where DOISST shows ice but ERA5 shows open water (−1.30 °C in these cells). Thus the 2016 method change converts the 2005 excess ice into an SST error. On the same day, DOISST minus ERA5 in these cells falls from +0.82 °C (30 days before) to −0.36 °C (30 days after).

**Consequences (DOISST v2.1 as published compared with DOISST with the 2016 splice removed, and with ERA5):**

| Statistic, 1982–2025 record | DOISST v2.1 | 2016 splice removed | ERA5 |
|---|---|---|---|
| Arctic (≥60°N) July–September SST trend 2005–2025, °C/decade | +0.06 ± 0.08 | +0.27 ± 0.08 | +0.27 ± 0.07 |
| Arctic July–September SST, 2016–2025 minus 2005–2015, °C | +0.03 | +0.31 | +0.32 |
| Arctic annual SST trend 2005–2025, °C/decade | +0.03 ± 0.03 | +0.10 ± 0.03 | +0.13 ± 0.04 |
| Antarctic (≤60°S) January–March SST, 2016–2025 minus 2005–2015, °C | +0.09 | +0.20 | +0.25 |
| Arctic marine cold-spell total duration, mean days per year, 2005–2015 → 2016–2025 | 28.8 → 61.7 | 28.8 → 30.7 | 83.1 → 82.8 |
| Arctic marine cold-spell peak intensity, °C, 2005–2015 → 2016–2025 | 0.85 → 1.80 | 0.84 → 0.83 | 0.64 → 0.47 |
| Antarctic marine cold-spell total duration, mean days per year, 2005–2015 → 2016–2025 | 40.3 → 101.3 | 40.3 → 24.9 | 94.1 → 82.4 |
| Arctic MHW area cover (Huang et al. 2021 rules), 2005–2015 → 2016–2025 | 0.47 → 0.48 | 0.47 → 0.53 | 0.46 → 0.60 |

The DOISST v2.1 record therefore shows almost no Arctic summer warming after 2005. The corrected record and ERA5 agree on +0.27 °C per decade. The doubling of DOISST Arctic marine cold-spell days after 2016, and the 2.5-fold rise in the Antarctic, are artifacts of the splice. In the corrected record and in ERA5 the cold-spell days do not rise (Arctic) or they decrease (Antarctic). The absolute cold-spell levels differ between DOISST and ERA5 because the two products treat SST under and near ice differently. Only the changes are comparable. The published Arctic MHW intensity and duration statistics (Huang et al. 2021) change little: the 2007 jump in MHW intensity is also present in ERA5 in July–August 2007, before ERA5 changed its own SST input. The splice does reduce the recent Arctic MHW area cover.

**A global check (60°S–60°N, not polar):** v2.1 is +0.09 °C warmer than v2.0 after 2016. At 102 moored buoys the v2.1 minus buoy difference has no step across 2016-01-01 (median −0.007 °C, 95% interval −0.015 to +0.006 °C). The v2.0 minus buoy difference steps by −0.10 °C (−0.12 to −0.07). Thus outside the polar caps, v2.1 corrected a cold drift in v2.0, and the 2016 change does not put a step into v2.1 there. The splice problem is polar.

## 1. Question and background

DOISST v2.1 (Reynolds et al. 2007; Huang et al. 2021, J. Climate 34:2923) is the standard daily SST record for MHW work. Earlier campaign publications found noise steps at satellite input changes (sci:sha256:f50dc28f…, 87b87a67…, 69a00227…, cfeb640f…, 819eea65…), spatial steps (4e3a13fa…, 5003de8e…, 5d8902f2…) and effects on reef heat stress (ef9c2a57…). All of these studies used 60°S–60°N or 50°S–50°N. Poleward of 60°, DOISST SST comes mostly from a proxy that converts sea-ice concentration to SST. NOAA documents two changes to this part of the product:

- Ice concentrations come from NASA GSFC (Cavalieri et al.) up to 2004 and from the NCEP analysis (Grumbine) from 2005 (NCEI product page; Huang et al. 2021 GRL).
- From 1 January 2016, v2.1 "revised the sea-ice-concentration to SST conversion to remove warm biases in the Arctic" (a freezing point replaces the regressed ice-SST proxy). Data before 2016 are the same as v2.0.

Arctic MHW studies use DOISST v2.1 over this period. Examples are Huang et al. (2021, GRL 48:e2021GL095590, "Prolonged marine heatwaves in the Arctic: 1982–2020") and Barkhordarian et al. (2024, Commun. Earth Environ., a 2007 regime shift in Arctic MHWs). We ask: do the two documented changes put steps into DOISST polar ice and SST, and how much do the steps change polar SST trends, MHW statistics and marine cold-spell (MCS) statistics?

## 2. Data

All raw data stay outside this bundle. `files/provenance/data_provenance.json` gives the URLs, versions and SHA-256 hashes.

- **DOISST v2.1 SST**, daily, 0.25°, 1982–2025: NOAA PSL files `sst.day.mean.YYYY.nc` from the shared campaign store (`datasets/noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109`).
- **DOISST v2.1 ice concentration**, daily: NOAA PSL `icec.day.mean.YYYY.nc` (44 files, downloaded 2026-11-10).
- **OISST v2.0 (AVHRR-only)**, daily, 2015-12-01 to 2020-04-26 (1,609 files) from NCEI `.../sea-surface-temperature-optimum-interpolation/v2/access/avhrr-only/`.
- **ERA5** `sea_surface_temperature` and `sea_ice_cover` at 12:00 UTC each day, 1982–2025, from the public ARCO-ERA5 Zarr store (Google Cloud). ERA5 uses HadISST2 SST and OSI SAF ice before September 2007 and OSTIA after. ERA5 has its own SST variance step at 2007-09-01 (campaign publication 5d9b238d…). ERA5 has no input change on 2005-01-01 or 2016-01-01.
- **NSIDC Sea Ice Index v4 (G02135)** daily hemispheric extent. Its source is the NASA Team algorithm, which is the same family as the pre-2005 DOISST ice input.
- **Moored buoys**: 102 GTMBA and NDBC buoys with daily SST from the campaign publication sci:sha256:87b87a67… (`files/data/buoy_daily_sst.csv.gz`).

All products go onto one grid: every second DOISST 0.25° cell (cell centres 0.125° + 0.5° k), poleward of 50°. ERA5 values are the mean of the four 0.25° ERA5 points around each cell centre.

## 3. Methods

- **Ice extent.** Area of cells with concentration ≥15% in each product. We compare it with the NSIDC extent day by day. The 2005 step is the mean (product − NSIDC) difference in 2005–2007 minus 2002–2004, averaged over the 12 calendar months. We remove the SSM/I gap (December 1987–January 1988) from the plots and trends.
- **2016 counterfactual.** v2.1 − v2.0 for each cell and day, 2016-01-01 to 2020-04-26. We give area means by region, month and v2.1 ice-concentration class. We split the area-integrated summer offset by ice agreement between DOISST and ERA5.
- **Splice correction.** For each cell, calendar month and v2.1 ice state (≥15% or not), we average v2.1 − v2.0 over May 2016–April 2020. We subtract this offset from DOISST v2.1 for all days from 2016-01-01. This puts 2016–2025 on the v2.0 ice-to-SST method that 1982–2015 use. Held-out test: an offset fitted on May 2016–April 2019 reduces the RMS daily v2.1 − v2.0 difference in May 2019–April 2020 from 0.72 to 0.60 °C poleward of 60°N, with a mean residual of +0.05 °C. The correction does not change the 2005 ice-input step.
- **Area-mean SST anomalies.** Monthly means per cell, area-weighted means over cells that are valid in DOISST and ERA5 on all days, anomalies relative to 1982–2011. Trends are OLS. The ± values are 1 standard error with a lag-1 effective sample size.
- **MHW and MCS.** We use the rules of Huang et al. (2021): 95th percentile threshold of an 11-day window in 1982–2011, climatology and threshold smoothed with 6 annual harmonics, at least 5 days, gaps of 2 days or less merged, SST above the long-term mean summer temperature (LMST). Cold spells use the 5th percentile and no LMST rule. Annual metrics per cell (maximum anomaly, total days, number of events, cover = fraction of cells with at least one event) are averaged over cells with an anomaly SD > 0.2 °C, weighted by cos(latitude). We do this for DOISST v2.1, the splice-corrected DOISST and ERA5, separately in each product.
- **Daily step tests.** DOISST − ERA5 daily area means, mean of 365 days after minus 365 days before a date. Placebo distribution: the same statistic on 1 January of other years.
- **Buoy test.** At each buoy we take the nearest 0.5°-grid cell. Step = mean (product − buoy) in 2016–2018 minus 2013–2015, for v2.1 and for v2.0 (both are identical before 2016). We require ≥300 matched days in each period. The interval is a bootstrap of the median over buoys.

## 4. Results

### 4.1 The DOISST ice field has a step on 2005-01-01 and drifts after it (Figure 1)

| Hemisphere | DOISST − NSIDC step at 2005-01-01 (million km²) | ERA5 − NSIDC step | Mean DOISST − NSIDC 1982–2004 | 2005–2025 |
|---|---|---|---|---|
| North | +1.11 | +0.01 | −0.60 | +0.69 |
| South | +1.48 | −0.00 | −0.14 | +2.22 |

Before 2005 DOISST tracks NSIDC with an almost constant offset. Probable causes are the different land masks and grids, and the ice south of 50°N that our domain does not include. After 2005 the difference grows and changes with season and year. Other jumps occur around 2009 (Antarctic summer), 2017 and 2025. Only 0.63 million km² of the northern step is in cells that both products treat as ocean. The remainder is in coastal cells that ERA5 treats as land.

Ice-extent trends (million km² per decade):

| | DOISST | ERA5 | NSIDC |
|---|---|---|---|
| Arctic September 1982–2025 | −0.48 | −0.88 | −0.79 |
| Arctic annual 1982–2025 | −0.10 | −0.55 | −0.52 |
| Antarctic February 1982–2025 | +0.69 | −0.17 | −0.10 |
| Antarctic annual 1982–2025 | +0.75 | −0.16 | −0.11 |

Studies that relate MHWs to sea-ice loss with the OISST ice field (for example Huang et al. 2021 GRL, section 3.2) use an ice record that is not homogeneous.

Under the v2.0 method (1982–2015), the excess ice had little effect on SST. In the daily DOISST − ERA5 area mean poleward of 60°N, the 2005-01-01 step is +0.07 °C; the placebo SD is 0.04 °C.

### 4.2 The 2016 method change cools the ice margins (Figures 2 and 3)

- All 31 days in December 2015 are identical in v2.1 and v2.0 (all cells). The ice fields are identical in 99.9% of the cells after 2016.
- v2.1 − v2.0, 2016-01-01 to 2020-04-26, area mean: −0.11 °C poleward of 60°N (July −0.43 °C, August −0.32 °C), −0.06 °C poleward of 60°S (December −0.20 °C, January −0.15 °C), +0.09 °C at 60°S–60°N.
- By v2.1 ice concentration (60°N): 0%: −0.02; 0–15%: −0.47; 15–35%: −0.82; 35–50%: −1.34; 50–80%: −0.80; 80–100%: +0.07 °C. South: −0.01, −0.07, −0.20, −0.25, −0.16, −0.05 °C.
- In July–September poleward of 60°N, the area-mean offset is −0.31 °C. 60% of it is in cells where both DOISST and ERA5 have ice (−0.60 °C), 37% in cells where only DOISST has ice (9% of the area, −1.30 °C) and 2% in open water. In December–February poleward of 60°S, the area mean is −0.15 °C. 33% of it is in DOISST-only ice cells (−0.39 °C) and 41% in open water (−0.10 °C).
- The DOISST − ERA5 difference in DOISST-only ice cells drops on the day of the change: north +0.82 → −0.36 °C, south +0.15 → −0.27 °C (30-day means). The 365-day step in the area mean poleward of 60°N is −0.11 °C, which is 2.8 placebo SDs.

### 4.3 Consequences for polar SST trends (Figure 4)

See the table in the summary. Poleward of 60°N, the published record gives a 2005–2025 July–September trend of +0.06 ± 0.08 °C per decade. The splice-corrected record gives +0.27 ± 0.08 and ERA5 gives +0.27 ± 0.07. For 1982–2025 the summer trends are +0.27 (published), +0.34 (corrected) and +0.42 °C per decade (ERA5). The remaining 1982–2025 difference to ERA5 has other causes (ERA5's 2007 input change, the 2005 ice step and product differences). This study does not resolve them. In always-open water, the splice has a small effect (2005–2025 summer trend +0.35 published, +0.30 corrected). Poleward of 60°S the splice makes 2016–2025 summers 0.10 °C too cold relative to 2005–2015. The 1982–2025 Antarctic trends stay near zero in all three records.

### 4.4 Consequences for marine heatwaves and cold spells (Figure 6)

Arctic (≥60°N; DOISST 20,656 cells, ERA5 13,043 cells with SD > 0.2 °C):

| Metric | DOISST v2.1 | splice removed | ERA5 |
|---|---|---|---|
| MHW maximum intensity, °C, 2005–2015 → 2016–2025 | 3.16 → 4.14 | 3.16 → 4.15 | 3.68 → 4.26 |
| MHW total days per year, 2005–2015 → 2016–2025 | 27.5 → 40.3 | 27.6 → 41.8 | 28.6 → 48.1 |
| MHW cover trend 2005–2025, per decade | +0.03 | +0.06 | +0.12 |
| MCS total days per year, 2005–2015 → 2016–2025 | 28.8 → 61.7 | 28.8 → 30.7 | 83.1 → 82.8 |
| MCS peak intensity, °C, 2005–2015 → 2016–2025 | 0.85 → 1.80 | 0.84 → 0.83 | 0.64 → 0.47 |
| MCS total-days trend 2005–2025, days per decade | +25.9 | +2.0 | −0.5 |

Antarctic (≤60°S; DOISST 14,568 cells, ERA5 16,058 cells):

| Metric | DOISST v2.1 | splice removed | ERA5 |
|---|---|---|---|
| MHW total days per year, 2005–2015 → 2016–2025 | 15.9 → 23.7 | 15.9 → 24.4 | 16.8 → 29.2 |
| MHW cover trend 2005–2025, per decade | +0.02 | +0.05 | +0.06 |
| MCS total days per year, 2005–2015 → 2016–2025 | 40.3 → 101.3 | 40.3 → 24.9 | 94.1 → 82.4 |
| MCS cover, 2005–2015 → 2016–2025 | 0.71 → 0.82 | 0.71 → 0.42 | 0.84 → 0.77 |
| MCS total-days trend 2005–2025, days per decade | +47.1 | −9.2 | −5.7 |

The corrected DOISST record also has a cold-spell peak in 2009–2011 (Figure 6d). It starts when the DOISST Antarctic ice excess grows in 2009 (Figure 1). We did not correct this part.

Figure 6 shows the annual series. The MHW intensity and duration statistics of Huang et al. (2021) are robust to the splice. Their 1982–2006 versus 2007–2020 rise is present in all three records. ERA5 shows a July–August 2007 SST anomaly poleward of 60°N of +0.76 °C (DOISST +0.98 °C), before the ERA5 input change in September 2007. Thus the 2007 Arctic MHW shift (Huang et al. 2021; Barkhordarian et al. 2024) is not an artifact of the DOISST 2007 AVHRR change. The splice does affect the MHW area cover and, much more, the cold spells. Arctic cold-spell statistics from DOISST v2.1 after 2015 are not usable without a correction.

### 4.5 Outside the polar caps the 2016 change does not make a step (Figure 5)

See the summary. 89 GTMBA and 13 NDBC buoys: GTMBA median step v2.1 −0.003 °C, v2.0 −0.103 °C; NDBC v2.1 −0.030 °C, v2.0 −0.057 °C. The +0.09 °C v2.1 − v2.0 difference at 60°S–60°N is a correction of a v2.0 cold drift after 2015. It does not explain the earlier campaign finding of a +0.03 °C per decade DOISST − buoy warming drift.

## 5. Limitations

- ERA5 is not truth. Its SST and ice come from HadISST2/OSI SAF (to August 2007) and OSTIA (after), and it has its own steps. We use ERA5 only where it has no change (2005-01-01, 2016-01-01, July–August 2007) and as a second estimate of trends.
- We do not know which ice-to-SST method is more accurate. NOAA states that the v2.1 freezing-point method removes a warm bias. Our correction puts 2016–2025 onto the older v2.0 method so that the record is homogeneous. It does not make the record more accurate in absolute terms. A homogeneous v2.1-method record would need a reprocessing of 1982–2015 by NOAA.
- The correction removes the mean offset by cell, month and ice state. It removes 17% of the daily RMS difference in a held-out year. It does not correct day-to-day differences or the 2005 ice-input step.
- The 0.5° subsample uses one in four DOISST cells. ERA5 is a 12:00 UTC value, not a daily mean.
- We tried ESA SST CCI v3 as a third record. The CEDA OPeNDAP server gave less than 0.1 requests per second on 2026-11-10, so we stopped. This study uses no CCI data.
- Few in situ SST data exist in the ice zones. This study does not use polar in situ data (for example UpTempO buoys).
- The buoy test uses moorings that are also inputs to OISST.

## 6. Reproduction

Code is in `files/code/`. Raw data go into a private scratch folder `work/scratch/`, never into the bundle. The steps:

1. `fetch_icec.sh work/scratch/icec`; NSIDC files with `curl` (URLs in the provenance file).
2. `python extract_polar.py sst 1982 … 2025` and `python extract_polar.py icec 1982 … 2025`, then `python assemble.py`.
3. `python fetch_era5_polar.py 16` (needs numpy, numcodecs, requests).
4. `python fetch_v20.py 12`, then `python extract_v21_global.py`.
5. `python ice_compare.py`, `python daily_diag.py`, `python iceclass.py`, `python diffseries.py`, `python ice_trends.py`.
6. `python analysis_v20v21.py`, `python splice_attrib.py`, `python make_corrected.py`, `python trends.py`.
7. `run_mhw.py` for each product and hemisphere (see `run_all.sh`), then `python mhw_tables.py`.
8. `python buoy_splice.py` (needs the buoy file from sci:sha256:87b87a67…).
9. `python check_2007.py`, `python figures.py`, `python provenance.py`, `python pack_results.py`.

`run_all.sh` lists the full order. On the shared Dell host with load near 120, the full run takes about 4 h. The MHW step takes most of the time.

Results in `files/results/`:

- `ice_extent_monthly.csv`: monthly DOISST and ERA5 extent and their difference to NSIDC.
- `ice_steps.json`, `ice_trends.json`: ice steps and trends.
- `v21_minus_v20_summary.json`, `v21_minus_v20_daily.csv`: the 2016 counterfactual.
- `v21_minus_v20_offset_polar.npz`: the correction field (cell × calendar month × ice state, |latitude| ≥ 50°, 0.5° grid). You can use it to correct other DOISST v2.1 polar analyses.
- `splice_attribution.json`, `daily_diag_N.csv.gz`, `daily_diag_S.csv.gz`, `diff_series_daily.csv.gz`, `diff_steps.json`.
- `polar_sst_anomaly_series.csv`, `polar_sst_trends.json`.
- `mhw_area_metrics.csv`, `mhw_trends.json`.
- `buoy_splice_steps.csv`, `buoy_splice_summary.json`.
- `julaug_anomaly_N60.json`: July–August SST anomaly poleward of 60°N per year, DOISST and ERA5 (2007 check).

## 7. Data licenses and attribution

See `files/NOTICE_external_data.md`. In summary: NOAA OISST (v2.0, v2.1) and NOAA@NSIDC Sea Ice Index are U.S. Government data. ERA5 is from the Copernicus Climate Change Service, CC BY 4.0 (Hersbach et al. 2020); the results contain aggregated values derived from ERA5. GTMBA (NOAA PMEL) and NDBC buoy data come through the cited campaign publication. Our code is MIT and our text, figures and derived results are CC BY 4.0 under the SCI baseline license.

## References

- Barkhordarian A., Nielsen D. M., Olonscheck D., Baehr J. (2024) Arctic marine heatwaves forced by greenhouse gases and triggered by abrupt sea-ice melt. Commun. Earth Environ. (2024). doi:10.1038/s43247-024-01215-y
- Hersbach H. et al. (2020) The ERA5 global reanalysis. Q. J. R. Meteorol. Soc. 146:1999–2049. doi:10.1002/qj.3803
- Huang B. et al. (2021) Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. J. Climate 34:2923–2939. doi:10.1175/JCLI-D-20-0166.1
- Huang B., Wang Z., Yin X., Arguez A., Graham G., Liu C., Smith T., Zhang H.-M. (2021) Prolonged marine heatwaves in the Arctic: 1982–2020. Geophys. Res. Lett. 48:e2021GL095590. doi:10.1029/2021GL095590
- Reynolds R. W. et al. (2007) Daily high-resolution-blended analyses for sea surface temperature. J. Climate 20:5473–5496. doi:10.1175/2007JCLI1824.1
- Fetterer F. et al. Sea Ice Index, Version 4 (G02135). NSIDC. https://nsidc.org/data/g02135
- Banzon V. et al. (2019) A comparison of two proxy SST estimation methods in the Arctic. GHRSST poster. https://zenodo.org/records/5042190
