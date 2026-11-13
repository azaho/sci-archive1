# Global Mangrove Watch v3 range limits stayed fixed in 1996-2020 and omit stands up to 4 degrees poleward; freezes below -6 C in Louisiana and Gulf Florida removed 12% of mapped area, which recovered

Job `sci-1107-dell-climate-pollution-biodiversity-062e52e9e98e`, topic climate-pollution-biodiversity, campaign 11_07_2026, machine dell, account claude-myxtap, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Mangroves are tropical trees. At their poleward range limits, field studies show that freezes kill them and that fewer freezes let them expand into salt marsh (Cavanaugh et al. 2014, PNAS; Osland et al. 2020, J. Ecol.). Cavanaugh et al. found that in Florida the frequency of extreme cold, not the mean temperature, controls expansion. Giri and Long (2016) found that the US poleward expansion was "inconclusive". The campaign record had no mangrove or salt-marsh publication before this one.

We asked three questions:

1. Can the global annual mangrove maps of Global Mangrove Watch version 3 (GMW v3, 1996-2020) show range-limit movement?
2. In mapped mangroves at |latitude| >= 18 degrees, does winter freeze severity predict year-to-year mapped area loss? Does it predict loss better than the winter mean temperature?
3. Does a freeze response that we fit in one region or sensor era transfer to another region or era?

## 2. Data

- **GMW v3.0** (Bunting et al. 2022, Remote Sensing 14:3657; Zenodo record 6894273, CC BY 4.0). These are annual 25 m maps for 1996, 2007-2010 and 2015-2020, from L-band radar (JERS-1 for 1996, ALOS PALSAR for 2007-2010, ALOS-2 PALSAR-2 for 2015-2020). We used all 470 1x1-degree tiles with a tile-centre |latitude| >= 18 degrees, for all 11 years (5,170 GeoTIFFs). We read them from the yearly ZIP files on Zenodo with HTTP range requests. We did not download the full ZIPs. SHA-256 and ZIP CRC-32 values for each tile are in `files/provenance/gmw_v3_tiles_sha256.json`.
- **NOAA CPC Global Unified daily minimum temperature**, 0.5 degrees (NOAA PSL, `https://downloads.psl.noaa.gov/Datasets/cpc_global_temp/tmin.YYYY.nc`, US Government work). We read calendar years 2006-2020 by HTTP range requests. We kept 17.25-33.75 N for December, January and February, and 17.25-39.75 S for June, July and August. Source sizes, ETags and the hashes of our extracted subsets are in `files/provenance/cpc_tmin_sources.json`. The PSL OPeNDAP server rejected our requests with HTTP 429, so we did not use OPeNDAP.
- **GBIF occurrence records** of nine true mangrove species (Avicennia germinans, Rhizophora mangle, Laguncularia racemosa, Avicennia marina, Kandelia obovata, Aegiceras corniculatum, Bruguiera gymnorhiza, Rhizophora stylosa, Avicennia schaueriana). We retrieved them on 2026-11-12 with the GBIF search API (query URLs in `files/provenance/gbif_query_urls.json`). Most records are CC BY-NC. Thus the bundle has no record-level GBIF data. The figure and the statistics use only the 256 CC0 or CC BY 4.0 records. Counts across all licences are given only as numbers.

## 3. Methods

1. **Mapped area.** For each tile and year, we summed mangrove pixels (value 1) by 0.25-degree cell, with a pixel area that changes with latitude (`aggregate_gmw.py`). For each tile and year, we also recorded the most poleward mangrove pixel.
2. **Range limits.** For 20 range-limit boxes (19 distinct limits; the two Baja boxes share one limit), we took the most poleward mapped pixel in each year. We then counted GBIF records that are poleward of the 2020 GMW limit. We kept records from 2010 onward, with a coordinate uncertainty of 1 km or less or not given, and not flagged as managed or introduced.
3. **Winter cold.** For each CPC cell and winter, we computed the coldest daily minimum (`tabs`), the mean daily minimum, and days below 0, -2 and -4 C (`winter_metrics.py`). Before this, two quality-control steps removed isolated cold artefacts. Step 1 removed a cell-day that was more than 8 C colder than the median of its valid neighbours (two passes). Step 2 removed a cell-day that was more than 12 C colder than the cell's own 5th percentile. The two steps removed 3,569 and 694 cell-days. They removed, for example, a -25 C day in the Eastern Cape in August 2012, a -13 C day on the South Texas coast in December 2009, and a -16 to -28 C patch over Haiti in winter 2019-20. The real January 2010 Florida freeze (about -9 C over many cells) stayed in the data.
4. **Panel.** Each 0.25-degree cell with 5 ha or more of mangrove in some year got the nearest CPC cell with data (median distance 0.18 degrees, maximum 0.95; 1,640 cells). The response is `dlog = log((A1 + 1 ha)/(A0 + 1 ha))` between consecutive maps, clipped to +-3. The main sample has only one-winter pairs within one sensor era: 2007-08, 08-09, 09-10, 15-16, 16-17, 17-18, 18-19 and 19-20. It has 12,922 cell-pairs with A0 >= 5 ha. The winter between maps t-1 and t is December of t-1 to February of t (Northern Hemisphere) or June-August of t (Southern Hemisphere).
5. **Models** (`analyse.py`). We used weighted least squares with map-pair fixed effects and standard errors clustered by 1-degree tile. Model (a) uses bins of `tabs` (> 0, 0 to -2, -2 to -4, -4 to -6, < -6 C). Model (b) is restricted to frost-exposed cells (any winter below 0 C). It compares hinge terms for degrees below 0, -4 and -6 C with the winter-mean anomaly. Model (c) uses within-cell contrasts. Model (d) tests transfer between regions and between sensor eras. Model (e) checks for a delayed response in the next map pair. We also made event trajectories for the January 2010 and January 2018 freezes.

## 4. Results

### 4.1 GMW v3 range limits do not move, and some known stands are absent (Figure 1)

In all 20 boxes, the most poleward mapped mangrove moved by at most 0.094 degrees across the 11 maps from 1996 to 2020 (`gmw_limit_stability.csv`). In 18 boxes it moved by 0.004 degrees (about 400 m) or less. The GMW v3 limit is 29.14 N on the Florida Atlantic coast. On the Texas coast GMW maps nothing north of 26.2 N, and in Western Australia it maps nothing south of 29.25 S.

Independent GBIF records from 2010 onward put mangroves poleward of these limits:

| Region | GMW v3 limit | CC0/CC BY records beyond (0.05-deg cells) | 90th percentile distance beyond | All-licence records beyond |
| --- | --- | --- | --- | --- |
| Texas | 26.18 N | 119 (42) | 2.84 deg | 603 |
| Florida Atlantic | 29.14 N | 53 (20) | 0.80 deg | 567 |
| Western Australia | 29.25 S | 13 (4) | 4.07 deg | 55 |
| Brazil south | 27.83 S | 12 (8) | 0.66 deg | 18 |
| New Zealand | 38.02 S | 10 (7) | 1.12 deg | 20 |

Records in the Florida Gulf, Louisiana, Victoria, Persian Gulf, Bermuda and Red Sea boxes were few or within 0.1 degrees of the limit. There were no records beyond the limit in the Baja, Pakistan, mainland China, Taiwan, Japan, South Australia or South Africa boxes. The positions agree with published fronts: St Augustine near 30 N in Florida, the central and upper Texas coast, Bunbury near 33.3 S, and Laguna near 28.5 S.

The GMW v3 method explains this. The paper states that, outside the 2010 baseline, gain is possible only in a contextual layer "within 2.5 km of the GADM coastal boundary and within 500 m of the GMW 2010 baseline", with an L-HV backscatter change of more than 8 dB. A stand more than 500 m beyond the 2010 baseline therefore cannot appear in any year. GMW v3 cannot test poleward range expansion, and its limits are a property of the product, not of the trees. Gain and loss classes have user accuracies of only 58% and 61% (Bunting et al. 2022).

### 4.2 Freezes in mapped mangroves: rare, local and weakly detected (Figures 2 and 4)

The CPC coldest night went below -4 C in only 35 of the 12,922 one-winter cell-pairs. All of them were in Louisiana (five winters), Gulf Florida (four winters) and one Zhejiang cell in January 2016. GMW-mapped cells in Atlantic Florida, Texas/Tamaulipas, Baja, East Asia (except that cell), Australia, New Zealand and southern Africa did not go below -4 C in 2007-2020. Partly this is because GMW omits the colder fronts.

Mapped area change by coldest-night bin (all regions, one-winter pairs):

| Coldest night | Cell-pairs | Area change (sum) | Pair-FE coefficient on dlog (95% CI) |
| --- | --- | --- | --- |
| > 0 C | 12,481 | -0.25% | reference |
| 0 to -2 C | 310 | -0.95% | -0.007 (-0.020, 0.007) |
| -2 to -4 C | 96 | -1.0% | -0.020 (-0.049, 0.009) |
| -4 to -6 C | 18 | +3.5% | -0.002 (-0.041, 0.036) |
| < -6 C | 17 (10 cells) | -12.3% | -0.089 (-0.178, -0.0001), p = 0.050; area-weighted -0.142 (-0.249, -0.035) |

A loss appears only below -6 C on the CPC grid. This agrees with the field mortality threshold near -7 C for black mangrove (Osland et al. 2020). The CPC grid includes inland stations, so it is colder than coastal sites, and the two thresholds are not directly comparable.

Event trajectories (Figure 4):

- **Louisiana, January 2018.** The CPC minimum was -8.1 C. The 9 cells below -4 C lost 7.8% of mapped area in 2017-18. They then gained 14.5% in 2018-19 and 5.8% in 2019-20. The 4 other cells changed by +2.6%, -5.6% and -3.4%. The fast rebound agrees with the resprouting and 1-3 year recovery that Osland et al. (2020) saw in the field after this freeze.
- **Gulf Florida, January 2010.** The CPC minimum was -8.9 C. The 8 cells below -4 C lost 4.7%, against 1.3% in the 19 other cells. This gap did not grow in 2010-2015.
- **Louisiana, 2009-10.** The regional total fell 8.7%. However, the 3 cells below -4 C gained 7.2% and the 11 other cells lost 16.3%. This loss is therefore not a freeze effect. It occurred in the year of the Deepwater Horizon oil spill and in an area of coastal land loss.
- **Delayed response.** Freeze degrees below -4 C did not predict the change in the next map pair (slope +0.015 per C; 95% CI -0.006 to 0.036; n = 1,013).

### 4.3 Extremes versus winter means (frost-exposed cells, n = 1,360 cell-pairs, 177 cells)

| Predictor (pair FE) | Slope on dlog (95% CI) | p | AIC |
| --- | --- | --- | --- |
| Degrees below 0 C at the coldest night | -0.0068 per C (-0.0133, -0.0002) | 0.042 | -1709.6 |
| Degrees below -4 C | -0.018 per C (-0.043, 0.006) | 0.13 | -1708.6 |
| Degrees below -6 C | -0.034 per C (-0.088, 0.019) | 0.21 | -1707.4 |
| Winter mean Tmin anomaly | -0.0014 per C (-0.0093, 0.0065) | 0.72 | -1704.5 |

The extreme metrics fit slightly better than the winter mean. The mean anomaly has no detectable slope. This agrees in direction with Cavanaugh et al. (2014). However, the evidence comes almost only from Louisiana and Gulf Florida, and the AIC differences are small.

### 4.4 Transfer between regions and eras failed or could not be done

- **Americas to East Asia.** This test was not possible, because only one East Asian cell went below -4 C.
- **East Asia, exploratory.** In 15 frost-exposed cells in Fujian, Zhejiang, Taiwan and Kyushu (many are small, planted stands of 5-30 ha), winters with a coldest night below 0 C gave -15.8% mapped area. Frost-free winters gave +4.3% in the same cells. The within-cell coefficient is -0.27 (95% CI -0.42 to -0.13). This result is **not robust**: with map-pair fixed effects it becomes -0.16 (-0.46 to 0.14). The same cells also declined in the map pair after a frost (-0.29; -0.71 to 0.14). This agrees better with a general decline of small stands than with a frost effect.
- **East Asia to the Americas.** The East Asian slope predicts a -26% excess loss in the 34 American cell-pairs below -4 C. The observed value is -1.6% (95% CI -4.2% to 1.5%).
- **Between sensor eras in the Americas** (freeze slope fitted on ALOS-1 2008-2010 and applied to ALOS-2 2016-2020, and the reverse). Predictions were -1.2% and -8.1%. Observed values were -5.4% (CI -17% to 3%) and -1.0% (CI -6% to 5%). The intervals include both zero and the predictions, so the test cannot decide.
- **Within-cell American contrasts.** Winters below -4 C gave -0.036 (-0.081 to 0.008). Winters from 0 to -4 C gave -0.015 (-0.031 to 0.001).

## 5. Interpretation

1. GMW v3, the standard global product for mangrove extent and blue carbon, cannot record poleward range expansion. In at least 5 of 19 range limits, it leaves out documented poleward stands, by 0.7 to 4 degrees of latitude. Studies that use GMW to estimate climate-driven mangrove expansion, or freeze effects at range limits, will find "no expansion" because of the method. They will also sample only the warm side of each front.
2. Where GMW maps mangroves that froze, it records a small and short-lived loss. The loss is about 12% of mapped area after nights below -6 C, with recovery within one to two years in Louisiana. The field showed leaf damage at about -4 C and biomass recovery of only 45-90% in the first season (Osland et al. 2020). The L-band radar mainly sees woody structure, so it probably records only part of the freeze damage. The GMW authors make the same point for storms that leave the forest structure in place.
3. We could not do the planned independent test across regions and periods. GMW mapped no freeze-exposed mangroves outside the US Gulf coast in 2007-2020. This is a data limit, not evidence against freeze control.

## 6. Limitations

- CPC is a 0.5-degree station analysis. Coastal mangrove sites are warmer than many grid cells, and the nearest-cell match can reach 0.95 degrees. Thresholds in CPC units are not site thresholds.
- Our QC can remove real local extremes, and it can keep coherent artefacts of less than 12 C.
- GMW map timing within each year is not known exactly. We assumed that the Northern Hemisphere winter lies between maps t-1 and t. For the Southern Hemisphere this assumption is weaker, but no Southern Hemisphere cell had a freeze below -4 C.
- GBIF records include planted trees, single seedlings and possible misidentifications. We did not inspect photographs. The New Zealand distances (about 1 degree beyond the limit) need checking. The bundled statistics use only CC0/CC BY records (256 of 1,516 records from 2010 onward).
- We did not analyse the 1996 to 2007 interval. It crosses a sensor change (JERS-1 to ALOS), and we downloaded temperatures only for 2006-2020.
- Freeze events: in the Americas, only two regions and nine winters (four with large freezes); in East Asia, one cell below -4 C. Statistical power is low.

## 7. What remains open

- Test freeze control at the fronts with a product that maps new stands: a Landsat or Sentinel-2 time series at St Augustine, Port Aransas, Bunbury and Laguna, together with station minima (GHCN-D).
- Use the Winter Storm Elliott (December 2022) and Uri (February 2021) freezes with GMW v4 or later annual maps, if they become available.
- Check whether GMW v4 (10 m, 2020) contains the stands that GBIF shows beyond the v3 limits.

## 8. Reproduction

`files/code/run_all.sh` lists the steps. Copy `files/code` to a working folder. The scripts write all raw downloads and intermediate data to `../scratch` and outputs to `../results`, outside the signed draft. Runtime with 2 CPUs: about 15 minutes for the tile fetch, about 15 minutes for the CPC fetch, 11 minutes for aggregation, and a few minutes for the models.

Bundled derived data (`files/data`):

- `gmw_cells.csv`: GMW v3 mangrove area (ha) per 0.25-degree cell and year (CC BY 4.0 derivative of GMW v3; attribution in `NOTICE.md`).
- `gmw_tile_poles.csv`: the most poleward mangrove pixel per tile and year.
- `winter_metrics.csv`: QC-filtered winter cold metrics per CPC cell, 2007-2020 winters (derived from NOAA CPC, public domain).
- `panel_labelled.csv`: the analysis panel.

Results are in `files/results`: `models.json` (all coefficients), `dose_response_bins.csv`, `region_pair_events.csv`, `region_bin_area_change.csv`, `gmw_limit_stability.csv`, `gbif_beyond_gmw_limits.csv`, `gbif_open_record_datasets.csv` and Figures 1-4.

## 9. References

- Bunting P. et al. 2022. Global Mangrove Extent Change 1996-2020: Global Mangrove Watch Version 3.0. Remote Sensing 14:3657. doi:10.3390/rs14153657. Data: doi:10.5281/zenodo.6894273.
- Cavanaugh K.C. et al. 2014. Poleward expansion of mangroves is a threshold response to decreased frequency of extreme cold events. PNAS 111:723-727. doi:10.1073/pnas.1315800111.
- Osland M.J. et al. 2020. Temperature thresholds for black mangrove (Avicennia germinans) freeze damage, mortality and recovery in North America. Journal of Ecology 108. doi:10.1111/1365-2745.13285.
- Giri C., Long J. 2016. Is the geographic range of mangrove forests in the conterminous United States really expanding? Sensors 16:2010. doi:10.3390/s16122010.
- Hesterberg S.G. et al. 2022. Climate drives coupled regime shifts across subtropical estuarine ecosystems. PNAS 119:e2121654119. doi:10.1073/pnas.2121654119.
- NOAA CPC Global Unified Temperature, https://psl.noaa.gov/data/gridded/data.cpc.globaltemp.html.
- GBIF.org (2026-11-12) occurrence search API; datasets in `files/results/gbif_open_record_datasets.csv`.
- Related campaign work on cold extremes and species: sci:sha256:46ebf207bbe4de80002291579e40aae3276656ead0d38a9cd6807d4e95cc12fe, sci:sha256:6eef26c73eda497aa209f27d6e934419c331ee0c3ede7a1d7b5e508c42c068a7, sci:sha256:11274006675b883a300c308a856feab1aa92468e70c027f836cbdc64ffcbc5a4. Related satellite heat-response test of a coastal canopy: sci:sha256:a555abcdeaa645e57dd0f9075b20269addf083797a792b6c353358103f691ae4.
