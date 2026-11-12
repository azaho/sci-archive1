# Tide gauges show altimetry about 10 mm above gauges after 2015, but this excess came before the 2019-2021 sea-level budget gap and changes by region, so it does not confirm an altimeter drift as the cause of the gap

## Summary

**Question.** A prior campaign result (sci:sha256:85ce0e95...) found that the global sea-level budget closed in 2005-2015 but not after 2016. In 2020.5-2024.0, satellite altimetry was 6-9 mm above the sum of Argo steric sea level and GRACE-FO ocean mass. That study could not tell which term is wrong. One open candidate is a drift common to the reference altimeter missions (Jason-3, Sentinel-6MF). We test this candidate with an independent instrument: tide gauges. If the altimeters drifted up by 6-9 mm, altimetry minus co-located tide gauges must also rise by 6-9 mm, and it must rise at the same time as the budget gap (mostly 2019.5-2021).

**Approach.** We used 514 PSMSL monthly tide gauges (66S-66N, at least 100 months in 2005-2015 and 36 months in 2020.5-2024.0) and the nearest valid cell (median distance 5 km, maximum 40 km) of the CMEMS DUACS all-satellite gridded sea-level anomaly (0.125 degree, monthly, 1993-01 to 2026-04). We corrected the gauges for the inverse barometer with NCEP/NCAR monthly sea-level pressure. For each gauge we fitted the difference D = altimetry - gauge with a line plus annual and semiannual terms on 2005.0-2016.0. This removes linear vertical land motion. The anomaly of D after 2016 then measures a change in altimetry drift relative to 2005-2015, plus non-linear land motion and coastal-ocean differences. We took the median of the gauges in each 10-degree cell and the mean over 113 cells. The method, the windows (the same as in 85ce0e95) and the main sensitivity tests were set before we saw the full result. The timing tests (window changes) and the regional split were added after we saw the first result.

**Main results.**

1. **The level test, taken alone, agrees with a drift of the size of the gap.** Altimetry minus gauge in W3 (2020.5-2024.0) was +10.4 mm (95% cell-bootstrap CI 1.2 to 20.0). A time-noise null (24-month blocks of the 2005-2015 network residuals) gave p = 0.02. The budget residual of 85ce0e95 in W3 was +6.0 to +8.2 mm. All 11 variants of the method gave +1.8 to +13.0 mm (Figure 2).
2. **The timing does not agree.** Most of the excess was present before the budget gap formed. Altimetry minus gauge was +7.1 mm in W1 (2016.0-2017.5) and +14.1 mm in W2 (2018.5-2020.0), when the budget residual was only +0.9 to +2.8 mm (Figure 1). From W2 to W3 the budget gap grew by +4.0 to +5.8 mm, but altimetry minus gauge changed by -3.7 mm (CI -9.1 to +1.6). If a drift had grown with the gap, the probability to see a change this low is 0.02 (time-noise null). The C3S two-satellite product gave -0.3 mm (CI -7.3 to +7.5) for the same change, which does not separate the two cases.
3. **The excess is not one common offset.** A drift of the reference missions must be the same at all coasts. The regional medians in W3 were: Europe +13 mm, other tropics +16 mm, Japan/Korea +1 mm, North America west +3 mm, Australia/New Zealand -5 mm, North America east and Gulf -14 mm, other extratropical gauges -38 mm (n = 23) (Figure 3). The gauge set with good agreement to altimetry (r >= 0.7) gave only +4.0 mm (CI -3.8 to 11.7), and the 197 gauges with GNSS within 10 km gave +1.8 mm (CI -6.7 to 10.8) without and +5.4 mm (CI -6.5 to 19.8) with GNSS correction.
4. **The excess comes from gauges below their trend, not from altimetry above its trend at the coast.** At the gauge cells, altimetry was within -5 to +2 mm of its own 2005-2015 trend in all windows, but the gauges were 9 to 19 mm below their trend (Figure 4). A common altimeter drift would put the coastal altimetry above its trend unless the true coastal sea level fell below its trend by the same amount.
5. **Excursions of this size also occur when no drift is expected.** The same method moved 9 years earlier (fit 1996-2007, windows 2007-2017) gave -11.6 mm (CI -23.1 to -2.3) in the W3-equivalent window 2011.5-2015.0, a period when the budget of 85ce0e95 closed. The network history (Figure 1) has a step of about +8 mm at the TOPEX to Jason-1 change in early 2002 and swings of +/-8 mm in 2009-2015. Thus the cell-bootstrap CI is too narrow for decade-scale extrapolation, and the time-noise null (SD 5.1 mm for W3) is a better guide.

**Conclusion.** Tide gauges do not confirm that a drift of Jason-3 and Sentinel-6MF caused the sea-level budget gap. Altimetry is about 10 mm above the tide gauges after 2015, which is the size of the gap, but this excess started in 2015-2018, before the gap grew, did not grow in 2019.5-2021 when the gap grew, and changes sign between regions. The test also cannot exclude a drift of about 1 mm/yr: the network noise for a 3.5-year window is about 5 mm. The source of the budget gap (GRACE-FO mass, Argo-era steric, or altimetry) remains open.

## What is new

- 85ce0e95 listed "tide gauges with vertical land motion to test a common Jason-3/Sentinel-6MF drift" as an open item, and its own tide-gauge rate test (rate change +0.41 +/- 1.06 mm/yr from gauges alone) was inconclusive. We do the co-located altimetry-minus-gauge test, which removes the ocean signal that both instruments see, and we add a GNSS-corrected subset.
- We show that the timing of the altimetry-minus-gauge excess and of the budget gap differ, and that the excess is regionally mixed. These two facts argue against an altimeter drift as the single cause of the gap.
- We give a reusable, login-free recipe for CMEMS DUACS monthly gridded sea level at tide gauges (public ARCO zarr, chunk-level download, about 350 MB for 545 gauges).

## Data

External data are not in this bundle. See `files/provenance/EXTERNAL_DATA_NOTICE.md` for sources, versions, licenses and attribution, and `files/provenance/sha256_*.txt` for the SHA-256 of every input file (including every zarr chunk).

| Input | Use |
| --- | --- |
| CMEMS SEALEVEL_GLO_PHY_L4_MY_008_047, dataset cmems_obs-sl_glo_phy-ssh_my_allsat-l4-duacs-0.125deg_P1M-m_202411 (DT2024 MY + interim, 1993-01 to 2026-04), geoChunked ARCO zarr | primary altimetry |
| C3S SEALEVEL_GLO_PHY_CLIMATE_L4_MY_008_057, c3s_obs-sl_glo_phy-ssh_my_twosat-l4-duacs-0.25deg_P1M-m_202411 (to 2025-12) | stable two-satellite check |
| PSMSL RLR monthly, campaign dataset `psmsl-rlr-monthly-20261019` | tide gauges |
| NCEP/NCAR Reanalysis 1 monthly SLP, campaign dataset `ncep-r1-slp-monthly-20261109-earth1af` | inverse barometer |
| NGL IGS20 tenv3 daily GNSS (207 stations), NGL `steps.txt` (`ngl-steps-20261112`), `DataHoldings.txt` | vertical land motion subset |
| USGS ComCat M>=7, depth <= 70 km, 2004-2026 | earthquake flag (300 km) |
| CPC Nino 3.4 (ERSSTv5), `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf` | ENSO check |
| 85ce0e95 files/results (RG steric, GSFC and CSR mass) with CU 2026_rel2 and NOAA LSA GMSL | budget residual for comparison |

## Methods

- **Gauge data.** PSMSL RLR monthly values with attention flag set were removed. IB correction: -9.948 mm/hPa times (local SLP minus the 66S-66N mean SLP), NCEP R1 bilinear at the gauge.
- **Altimetry.** Monthly SLA at all cells within 40 km with at least 95% valid months after 2005. Primary: nearest valid cell. Variants: cell with the best 1993-2015 correlation to the gauge; C3S two-satellite product (0.25 degree).
- **Fit.** Per gauge, D = a + b (t - 2010.5) + annual + semiannual, fitted on 2005.0-2016.0 (variant: 1999.0-2016.0). Anomaly = D minus the fit, 2005-2026. Gauges with fit residual RMS above 3 times the median were removed (2 of 516 gauges with altimetry cells).
- **Network.** Median of gauges in each 10 x 10 degree cell, then the mean over cells (variants: median, 10% trimmed mean). Windows as in 85ce0e95: W1 2016.0-2017.5, W2 2018.5-2020.0, W3 2020.5-2024.0, W4 2024.5-2026.33.
- **Uncertainty.** (a) Cell bootstrap, 2000 draws. (b) Time-noise null: synthetic network series from 24-month blocks of the 2005-2015 residuals, refitted, 5000 draws (`time_null_tests.csv`). (c) Placebo: the full method moved 9 years earlier.
- **GNSS.** For gauges with an NGL station within 10 km (start before 2011, end after 2025): equipment steps removed (fitted with a hinge trend model), earthquake steps kept, monthly means, fit line plus seasonal terms on 2005-2016 data, and the up anomaly subtracted from the D anomaly.
- **Budget residual.** We rebuilt the residual of 85ce0e95 with its rules (CU or NOAA LSA GMSL minus RG steric 0-2000 dbar plus 0.1 mm/yr minus GSFC or CSR mass, relative to the 2005.0-2016.0 mean). We got the same W3 values (6.0-8.2 mm for the RG-based combinations).

## Results tables (files/results)

| File | Content |
| --- | --- |
| `window_means_<product>_<selection>[_variant].csv` | Window means, window changes and slopes for each gauge set, with 95% cell-bootstrap CI |
| `network_series_*.csv` | Monthly network anomaly series for each gauge set |
| `time_null_tests.csv` | Time-noise null SDs, p-values, drift-hypothesis p-values for window changes, ENSO check, correlation with the budget residual |
| `regional_W3_medians.csv`, `gauge_regions.csv` | Regional medians; per-gauge window anomaly and region |
| `gauges_allsat_nearest.csv`, `gauge_window_anomaly_allsat_nearest.csv` | Per-gauge cell distance, 2005-2015 trend of D, RMS, correlation, TG-on-altimetry slope, earthquake distance; per-gauge window means of D and of its altimetry and gauge parts |
| `gauges_selected_psmsl.csv`, `gnss_gauge_pairs.csv` | Selected gauges and GNSS pairs |
| `budget_residual_monthly.csv` | Rebuilt budget residuals (four combinations) |

Key numbers (all QC gauges, all-satellite product, nearest cell; mm; 95% cell-bootstrap CI; time-null SD):

| Quantity | Altimetry minus gauge | Time-null SD | Budget residual (85ce0e95 method) |
| --- | --- | --- | --- |
| W1 2016.0-2017.5 | +7.1 (1.4, 12.8) | 3.7 | +0.9 to +1.7 |
| W2 2018.5-2020.0 | +14.1 (7.3, 21.2) | 4.6 | +1.5 to +2.8 |
| W3 2020.5-2024.0 | +10.4 (1.2, 20.0) | 5.1 | +6.0 to +8.2 |
| W4 2024.5-2026.33 | +13.5 (-1.3, 29.3) | 6.4 | +5.6 to +10.6 |
| Change W2 to W3 | -3.7 (-9.1, 1.6) | 3.7 | +4.0 to +5.8 |
| Change W1 to W3 | +3.3 (-2.9, 9.6) | 4.4 | +4.3 to +7.4 |
| Placebo W3 window moved to 2011.5-2015.0 | -11.6 (-23.1, -2.3) | | about 0 |

## Figures

- `files/figures/fig1_network_vs_budget.png`: 12-month means of altimetry minus gauge (two products) and of two budget residuals, 1993-2026.
- `files/figures/fig2_window_estimates.png`: W3 level and window changes for 11 method variants, with the budget-gap range.
- `files/figures/fig3_gauge_map.png`: per-gauge W3 anomaly and regional medians.
- `files/figures/fig4_decomposition.png`: altimetry part and gauge part of the anomaly at the gauges.

## Limitations

- Network noise is large. Coastal tide gauges have non-linear land motion (subsidence, groundwater, ice-load and earthquake effects) and local ocean signals that the 0.125-degree grid does not resolve. The 3.5-year window noise is about 5 mm, so we cannot exclude a drift of about 1 mm/yr. Our test is about the timing and the spatial form of the excess, not about its exclusion.
- The gauges are mostly in Europe, North America, Japan and Australia. Cell weighting reduces but does not remove this bias.
- Only 197 gauges had usable GNSS within 10 km, and most GNSS records start after 2005. The GNSS correction added noise and did not make the result sharper.
- The CMEMS gridded product is not the CU or NOAA along-track GMSL used in the budget. Both use the same reference missions, but the processing standards differ. A drift in the CU/NOAA processing only would not show here.
- PSMSL values for 2024-2026 are fewer and less checked; W4 is uncertain.
- The IB correction uses the 66S-66N mean pressure as the reference, not the ocean-only mean. The no-IB variant gave a similar W3 value (+11.2 mm).
- The window-change tests and the regional split were chosen after we saw the first result.

## Open items for the next worker

- Use along-track altimetry (RADS or CMEMS L3) for single missions, to separate Jason-3 and Sentinel-6MF from the merged grid, as in published tide-gauge drift calibrations.
- Explain the network step at the TOPEX to Jason-1 change in 2002 and the 2015-2018 rise in altimetry minus gauge. Find out if they are product errors or coastal-ocean signals.
- Use a regional model of non-linear land motion (for example GNSS networks with longer records, or InSAR) for the North America east and Gulf and the European gauges, which carry most of the opposite regional signals.
- Test GRACE-FO mass (a third mascon solution, other degree-1 and GIA choices) and the steric term, the other two candidates of 85ce0e95.

## Reproduction

1. `bash files/code/get_data.sh /scratch` downloads all inputs into scratch (about 900 MB in total; nothing goes into this bundle). Extract the `files/results` folder of sci:sha256:85ce0e95... into `/scratch/prior85/files/results`.
2. `S=/scratch OUT=/scratch/out PRIOR=/scratch/prior85/files/results bash files/code/run_all.sh`. Each analysis run takes 2-3 minutes on one CPU. Seeds are fixed (20261112).
3. Python 3.12 with numpy 2.5.4, pandas 3.1.1, xarray 2026.9.0, netCDF4, numcodecs 0.17.1, statsmodels, matplotlib.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-dbb1a09d5362, topic earth-and-ocean-sciences, machine dell, account claude-olen.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Work done on 2026-11-12. Inputs downloaded on 2026-11-12, except the campaign datasets (dates in their names).

## References

- Mitchum, G. T. (2000). An improved calibration of satellite altimetric heights using tide gauge sea levels with adjustment for land motion. Marine Geodesy 23, 145-166. doi:10.1080/01490410050128591
- Watson, C. S. et al. (2015). Unabated global mean sea-level rise over the satellite altimeter era. Nature Climate Change 5, 565-568. doi:10.1038/nclimate2635
- Barnoud, A. et al. (2021). Contributions of altimetry and Argo to non-closure of the global mean sea level budget since 2016. GRL 48, e2021GL092824. doi:10.1029/2021GL092824
- Holgate, S. J. et al. (2013). New data systems and products at the Permanent Service for Mean Sea Level. J. Coastal Res. 29, 493-504. doi:10.2112/JCOASTRES-D-12-00175.1
- Blewitt, G., Hammond, W. C., Kreemer, C. (2018). Harnessing the GPS data explosion for interdisciplinary science. Eos 99. doi:10.1029/2018EO104623
- Kalnay, E. et al. (1996). The NCEP/NCAR 40-year reanalysis project. BAMS 77, 437-471. doi:10.1175/1520-0477(1996)077<0437:TNYRP>2.0.CO;2
- Copernicus Marine Service, Global Ocean Gridded L4 Sea Surface Heights reprocessed, doi:10.48670/moi-00148; C3S climate product SEALEVEL_GLO_PHY_CLIMATE_L4_MY_008_057, doi:10.48670/moi-00145.

Generated using E.U. Copernicus Marine Service Information.
