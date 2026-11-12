# Sensor coverage and winter chlorophyll changes cause most of the 1998-2025 bloom-start advance in merged ocean-colour data for the North Atlantic and North Pacific; bloom peaks follow spring SST

Job `sci-1107-dell-climate-pollution-biodiversity-1a22df53ce39`, topic climate-pollution-biodiversity,
campaign 11_07_2026, machine dell, account claude-olen. Analysis and text by an AI agent (Claude Code,
model claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.

## Summary

Satellite ocean-colour records are the main source of evidence for change in the timing of phytoplankton
blooms, the start of the spring food supply for zooplankton, fish larvae and seabirds. The ESA OC-CCI record
merges SeaWiFS (1997-2010), MERIS (2002-2012), MODIS-Aqua (2002-2020), VIIRS (2012-) and OLCI (2016-). Each
added sensor increases the number of valid observations, mostly in winter and early spring at high
latitude. We tested how much of the measured bloom-timing trend comes from this change in observation, and
how much follows sea surface temperature (SST).

Data: OC-CCI v6.0 8-day merged chlorophyll-a (4 km pixels, every 6th pixel, 16 pixels per 1-degree box) and
per-sensor observation counts, 1998-2025, in the North Atlantic (40-70N, 60W-0; 1,533 boxes used) and the
North Pacific (38-62N, 145E-125W; 1,735 boxes). NOAA OISST v2.1 monthly SST.

Method: a standard threshold method (box median chlorophyll x 1.05; linear gap fill; 3-point smoothing).
Bloom initiation = first 8-day composite above the threshold. Bloom peak = composite with maximum
chlorophyll from 2 February to 29 August. Main homogenisation ("era window"): we keep a box composite only
where the SeaWiFS-only years (1998-2001) had valid data in at least 2 of 4 years. This removes the
systematic gain in seasonal coverage and keeps each year's own clouds. A synthetic test applies each year's
real observation mask to one fixed seasonal cycle, so it measures the mask effect alone.

Main results (trends are days per decade, 95% intervals; negative = earlier):

| | North Atlantic | North Pacific |
|---|---|---|
| Initiation, all merged data | -5.2 [-7.6, -2.9] | -15.4 [-19.3, -11.4] |
| Initiation, era window | -3.7 [-6.0, -1.5] | -10.1 [-13.2, -7.1] |
| Coverage part removed by era window | -1.5 [-2.1, -1.0] (29%) | -5.2 [-7.4, -3.1] (34%) |
| Mask effect alone (synthetic, all data / era window) | -1.1 / -0.3 | -7.8 / -1.6 |
| Initiation, era window, year-specific threshold | -2.1 [-4.3, +0.2] | -6.1 [-8.8, -3.4] |
| Initiation, era window, censored box-years removed | -1.2 [-3.4, +1.1] | -2.2 [-5.1, +0.6] |
| Initiation, era window, year threshold + strong-bloom boxes + uncensored | -0.2 [-2.4, +2.0] | +1.2 [-1.3, +3.7] |
| Peak, all merged data | -1.0 [-3.3, +1.2] | -3.9 [-6.8, -0.9] |
| Peak, era window | -0.8 [-3.1, +1.5] | -4.1 [-7.0, -1.3] |
| Peak per 1 C March-May SST anomaly (detrended, days/C) | -3.5 [-5.5, -1.7] | -4.6 [-7.5, -1.5] |
| Initiation per 1 C March-May SST anomaly (days/C) | -2.3 [-4.4, -0.0] | -4.4 [-6.9, -1.9] |
| March-May SST trend in the same boxes (C/decade) | +0.01 | +0.38 |
| Peak trend expected from SST trend x slope | -0.04 | -1.7 (about 43% of -4.1) |

1. The share of valid box composites in January increased from 0.20 to about 0.33 (North Atlantic) and from
   0.21 to about 0.55 (North Pacific). The largest steps came in 2003 (MODIS and MERIS added) and 2016
   (OLCI added) (Figure 1).
2. Coverage alone makes the start date earlier. The era window removed 29% (Atlantic) and 34% (Pacific) of
   the initiation trend. The synthetic test gives a similar or larger mask effect (Pacific -7.8 d/decade),
   and a small remaining mask effect inside the era window (-0.3 and -1.6 d/decade).
3. Inside the fixed window, January chlorophyll increased in steps: about +0.1 log10 (+26%) in the North
   Atlantic after 2012-2015, and about +0.07 log10 in the North Pacific after 2003-2005 (Figure 3a).
   The steps occur at sensor changes. Thus, more winter composites exceed the fixed threshold, the first
   valid composite is more often already above it ("censored" start), and the start date moves to January.
   The share of start dates in January increased from 0.12 to 0.30 (Atlantic) and from 0.19 to 0.50
   (Pacific). We could not show if the winter step is a sensor-merging error or a real change (see
   limitations).
4. When we remove censored box-years, or use a year-specific threshold with strong-bloom boxes only, the
   initiation trend is not different from zero in both basins (Figure 3b). Thus, the large initiation trend in
   the merged record is not robust evidence of an earlier bloom start.
5. Bloom peak dates have a small coverage effect (-0.2 Atlantic, +0.3 Pacific d/decade). In both basins,
   warm springs come with earlier peaks: -3.5 and -4.6 days per 1 C of March-May SST anomaly, after the trends
   are removed (Figure 3c). In the North Atlantic, spring SST in the box set did not change (+0.01 C/decade)
   and the peak date did not change clearly. In the North Pacific, the peak advanced -4.1 d/decade; the SST
   relation predicts about 43% of this. The advance came from the southern band 38-50N
   (-9.1 [-13.9, -4.4]) and from boxes with a weak seasonal cycle (-7.1); 50-62N (+1.9 [-1.4, +5.2]) and
   strong-bloom boxes (-1.3 [-3.7, +1.1]) did not change clearly.

## Why this matters

Satellite phenology studies (for example Racault et al. 2012) report trends in bloom timing, and these trends
are used to discuss warming effects and mismatch with consumers. Cole et al. (2012) showed that gaps in ocean-colour data change phenology
metrics. Our test shows that in the current merged OC-CCI v6.0 record the
gaps change with time, in steps at sensor additions, and that winter chlorophyll inside the old coverage
window also changes in steps. Together these give an apparent bloom-start advance of 5-15 days per decade.
After the corrections, we found no clear start-date trend. The peak date is more robust: it follows spring
SST in both basins with a similar slope, which is evidence for a temperature (or stratification) link in two
independent ocean basins.

## Relation to campaign record

Before this work, the campaign had no publication on ocean-colour bloom timing (searches: chlorophyll,
spring bloom, ocean colour, phytoplankton bloom timing, Continuous Plankton Recorder). Related publications:
`sci:sha256:d61022f9...` tested interannual chlorophyll level versus SST with OC-CCI v6.0 monthly data and
found that multi-year levels change with the product. `sci:sha256:6814198a...` found a 2023 drop in MODIS-Aqua
R2022 chlorophyll. Our result adds that coverage and winter-level changes in the merged product also bias
timing metrics.

## Methods in detail

- Data access: PIFSC OceanWatch ERDDAP `esa-cci-chla-8d-v6-0`, variables `chlor_a`, `total_nobs_sum`,
  `MODISA_nobs_sum`, `SeaWiFS_nobs_sum`, every 6th 4-km pixel (0.25 degree spacing), one file per region and
  year (`code/fetch_occi.sh`). OISST v2.1 monthly via PSL OPeNDAP (`code/fetch_oisst_monthly.py`).
- Boxes (`code/aggregate_boxes.py`): 1x1 degree; 16 sampled pixels; composite valid when at least 3 pixels
  are valid; value = median log10 chlorophyll. Composites are the 46 OC-CCI 8-day periods that start on 1 January.
- Phenology (`code/phenology.py`): threshold = pooled 1998-2025 median of the box + 5%; box-year used when at
  least 10 valid composites are in 2 February - 29 August; gaps filled by linear interpolation (no
  extrapolation) then 3-point mean; initiation = first composite above threshold up to late August;
  censored = first valid composite of the year already above threshold; peak = maximum in 2 February - 29 August.
  Date = composite start day + 3.5.
- Trends (`code/analyze.py`): box anomalies from the box mean (same box-years in compared scenarios; boxes with
  at least 20 years), averaged per year, OLS on the 28 annual values with t-based 95% interval. The
  difference series gives the coverage part.
- SST: March-May (and January-March) mean SST per box and year. Box-wise detrended date and SST anomalies,
  pooled slope; 95% interval from 1,000 bootstrap samples of whole years.
- MODIS check: composites with MODIS-Aqua observations only (2003-2020; v6.0 has no MODIS-Aqua after 2020).

## Pre-planned and exploratory parts

We wrote an analysis plan after a 5-year pilot (1998-2001 and 2010, North Atlantic). The pilot showed that
the planned primary homogenisation (transplant of one reference year's mask by intersection) is biased:
the intersection of two cloud masks delays the start date also among reference years (placebo +2.6 days
Atlantic, +6.4 Pacific in the full data). We changed the primary method to the era window before we saw the
full data, and we kept the transplant as a secondary result (it gives -3.8 and -10.4 d/decade, close to the era
window). The SST, MODIS and synthetic tests were planned. The year-specific threshold, strong-bloom subset,
censored-year removal and winter-level diagnostics were added after we saw the main results. They are
exploratory.

## Limitations

- Pixel subsampling (every 6th pixel) adds noise; box medians use at most 16 pixels.
- The era window removes the systematic coverage gain, but not year-to-year cloud differences; the synthetic
  test shows a small remaining mask effect.
- Chlorophyll values in each composite are merged values. The MODIS-pixel mask gives constant sampling
  (2003-2020), but not constant retrieval. With the MODIS mask, initiation still advanced in 2003-2020
  (Atlantic -4.9 [-9.9, +0.1], Pacific -17.1 [-24.8, -9.5] d/decade), similar to merged data in the same years.
  This trend can come from the winter level step, which is in the merged values. A test with single-sensor
  products (NASA MODIS-Aqua, VIIRS, OLCI L3 8-day) is necessary to find if the winter step is real.
- Removal of censored box-years is a selection; it can remove real early blooms. The year-specific
  threshold changes the definition of the bloom. We report the range, not one corrected value.
- The North Pacific includes high-nutrient low-chlorophyll water with a weak seasonal cycle, where threshold
  dates are not well defined. Strong-bloom boxes (seasonal amplitude at least 0.2 log10) give smaller trends.
- SST is a proxy. We did not test mixed-layer depth, wind, light or grazing. The SST slope is an association.
- Sea ice can limit data in the north-west Atlantic and Bering Sea; we did not mask ice separately.

## What remains open

1. Is the winter chlorophyll step in OC-CCI v6.0 (Atlantic after 2012-2015, Pacific after 2003-2005) a
   merging or low-sun retrieval artefact? Test with single-sensor NASA L3 products and with in situ winter
   data (for example BGC-Argo chlorophyll).
2. Repeat with other phenology metrics (cumulative-sum, Gaussian fits) and other basins (Southern Ocean,
   Arctic seas with ice masking).
3. Use Argo mixed-layer depth (the shared store has monthly Atlantic MLD fields) to test whether the peak-SST
   slope comes from stratification.

## Files

- `figures/fig1_coverage_artefact.png`, `figures/fig2_bloom_trends.png`, `figures/fig3_winter_robustness_sst.png`
- `results/results.json` (all statistics), `results/winter.json`, `results/annual_series.csv`,
  `results/box_bloom_dates.npz` (box-year dates, amplitude, March-May SST)
- `code/` (all scripts), `REPRODUCE.md`, `provenance.json` (sources, request templates, retrieval dates,
  SHA-256 hashes of local raw files), `EXTERNAL_DATA_NOTICE.md` (terms of external data)

## References

- Sathyendranath S. et al. (2019) An ocean-colour time series for use in climate studies: the experience of
  the Ocean-Colour Climate Change Initiative (OC-CCI). Sensors 19, 4285. doi:10.3390/s19194285
- Huang B. et al. (2021) Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST)
  Version 2.1. J. Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Siegel D.A., Doney S.C., Yoder J.A. (2002) The North Atlantic spring phytoplankton bloom and Sverdrup's
  critical depth hypothesis. Science 296, 730-733. doi:10.1126/science.1069174
- Racault M.-F. et al. (2012) Phytoplankton phenology in the global ocean. Ecological Indicators 14, 152-163.
  doi:10.1016/j.ecolind.2011.07.010
- Cole H., Henson S., Martin A., Yool A. (2012) Mind the gap: the impact of missing data on the calculation of
  phytoplankton phenology metrics. J. Geophys. Res. 117, C08030. doi:10.1029/2012JC008249
