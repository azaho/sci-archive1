# Equal sea-surface heat anomalies decreased Landsat kelp canopy only in the California Current (Baja to northern California), and a 1985-2013 heat model explained 9-41% of the 2014-2026 loss there

Job: sci-1107-dell-climate-pollution-biodiversity-708061cd9455. Topic: climate-pollution-biodiversity. Machine: dell.
Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
Date of analysis: 2026-11-12.

## Summary

Question. Marine heatwaves decreased kelp forests in some regions. Does the same heat dose give the same canopy loss in
different kelp regions? Is the loss controlled by the local anomaly (relative heat) or by the absolute temperature
(a warm limit near the same value everywhere)? Does a heat response that we fit before 2014 forecast the canopy after 2014?

Data. Quarterly Landsat kelp canopy area (1984-2026) from Kelpwatch.org for 163 coastal segments (H3 resolution-4
cells, about 45 km across) in 14 regions: SE Alaska, Washington, northern, central and southern California, Baja
California, Kamchatka-Kuril, Falklands, Tierra del Fuego, Santa Cruz and Chubut (Argentina), Namibia, Northern Cape and
Western Cape (South Africa). Monthly NOAA OISST v2.1 SST at the nearest ocean pixel of each kelp cell.

Method (plan written before results, see "Pre-registered design"). For each segment and year, K is the largest
cloud-corrected canopy area in the three quarters around the segment's usual peak quarter. The response is
R = log((K + 0.1B)/(1.1B)), where B is the 1984-2013 median of K. Heat is the peak monthly SST anomaly (H_anom) or the
peak absolute monthly SST (H_abs) in the 12 months that end at the end of the peak quarter. We compared a no-heat model
(M0), an anomaly model (M1), an absolute-temperature hinge model (M2, threshold fitted), both (M3), and an anomaly
hinge (M4), by leave-one-region-out and by forward tests (fit 1985-2013, test 2014-2026).

Main results.

1. A clear negative canopy response to heat occurred only in the four California Current regions. Within-segment slopes
   per +1 C peak anomaly were: northern California -0.59 (95% year-bootstrap interval -0.85 to -0.36), Baja California
   -0.31 (-0.47 to -0.14), southern California -0.29 (-0.45 to -0.16), central California -0.17 (-0.33 to -0.03).
   In the other 10 regions all intervals included zero (slopes -0.17 to +0.33). Western Cape (-0.01, -0.09 to 0.07),
   SE Alaska (-0.02, -0.12 to 0.08) and Washington (-0.04, -0.15 to 0.07) had narrow intervals near zero (Figure 1).
2. The heat slope did not follow the regional warmth. The Spearman correlation between the regional slope and the
   climatological warmest-month SST was -0.01 (p = 0.97, n = 14). Northern California (warmest month 13.0 C) had the
   most negative slope. Western Cape (18.6 C) had no response. Thus a common absolute warm limit does not explain
   the regional differences.
3. Across regions, no heat model transferred well. Mean regional RMSE of R in leave-one-region-out tests was 0.763 (M0),
   0.751 (M1, anomaly), 0.755 (M2, absolute hinge at 20.0 C), 0.748 (M3) and 0.749 (M4). The anomaly model improved
   on M0 by 0.013 (region-bootstrap interval -0.031 to +0.003). The absolute hinge was not better than the anomaly
   model (difference +0.004, -0.010 to +0.022). Forward tests for 2014-2026 gave the same order (M0 0.765, M1 0.742,
   M2 0.750; M1 gain 0.023, -0.052 to +0.002).
4. The 1985-2013 anomaly model under-predicted the 2014-2026 loss in the California Current. It explained 26% of the
   mean loss in Baja California, 41% in southern, 37% in central and 9% in northern California
   (files/results/forward_bias_share.csv). Within 2014-2026, the year-to-year heat slope in these regions was
   -0.15 to +0.17. The canopy stayed low in cooler years. This is a level shift that a heat slope does not forecast.
5. Observation bias. (a) Segment-years with fewer than three cloud-free quarters in the peak window had canopy values
   0.19 log units lower (SE 0.04, 208 region-years) than full-coverage segments in the same region and year. (b) Before
   1999 (Landsat 5 only) most non-US regions had almost no data: valid segment-year fraction 0.02 in Kamchatka-Kuril,
   0.05 in Tierra del Fuego, 0.10 in the Falklands. (c) With only 1999-2026 full-coverage segment-years, the
   California Current slopes stayed negative (-0.12 to -0.75), and SE Alaska (-0.13, -0.24 to -0.05) and the Falklands
   (-0.23, -0.37 to -0.07) also became negative. The slope-warmth correlation stayed near zero (+0.11).

Main limitations. Kelpwatch layers for non-US regions end in 2021-2025 and have unpublished methods and terms. SST at
0.25 degrees is not the temperature at the kelp. We did not measure nitrate, waves, urchins or sea otters; in the
California Current a warm anomaly also means low nitrate, and the northern California loss is known to follow urchin
increase after sea-star wasting. Sensor steps (2012, 2013, 2022) could not be separated from real changes in the
Northern Hemisphere.

## Background and what is new

Landsat studies of giant kelp in California and Baja California showed large losses during the 2014-2016 marine
heatwave and different resistance among sites (Cavanaugh et al. 2019, doi:10.3389/fmars.2019.00413; Bell et al. 2020, doi:10.1016/j.rse.2018.06.039).
Northern California bull kelp decreased by more than 90% with heat, sea-star wasting and urchin barrens
(Rogers-Bennett and Catton 2019, doi:10.1038/s41598-019-51114-y; McPherson et al. 2021, doi:10.1038/s42003-021-01827-6).
Reviews of marine heatwave effects report that responses are often larger near the warm range edge.

In this campaign, no earlier publication studied kelp. A BioTIME study found that marine heatwaves did not increase
assemblage change in 93 studies (sci:sha256:c2cfbd47...). A synthesis of 38 forward tests found that frozen climate
relations rarely capture later level shifts (sci:sha256:17f2e323...).

New here: (1) one standard satellite canopy index and one SST product across 14 regions in both hemispheres;
(2) a direct test of relative versus absolute heat across regions; (3) forward tests with a frozen 1985-2013 model;
(4) measured observation biases from cloud coverage and the Landsat 5 era.

## Pre-registered design

We wrote this design into the progress log before we fit any heat model (except a debug run on SE Alaska only):

- Units: H3 resolution-4 segments that hold H3 resolution-5 cells with kelp in the Kelpwatch tiles (mean value > 0.01
  and more than 20% of quarters > 0). 266 segments were queried; 163 passed the baseline filter (B >= 0.05 km2 and at
  least 15 valid years in 1984-2013). Oregon and Peru segments failed this filter (small canopy before 2014).
- Quarterly area A = kelp_area / clear_fraction when clear_fraction >= 0.5, else missing.
- Peak quarter p = the quarter with the largest median A in 1984-2013. K = max(A) over quarters p-1, p, p+1.
- R = log((K + 0.1B)/(1.1B)). Heat window: 12 months that end at the end of quarter p.
- T1: pooled models, leave-one-region-out. T2: fit 1985-2013, test 2014-2026, all regions. T3: sensor-era checks and
  clear-fraction threshold 0.8.
- Added after the main run (exploratory): within-region slopes by period and with the 12-month mean anomaly; the
  1999-2026 full-coverage variant; the coverage-bias contrast.

Regions: the California tileset was split at 32.53 N (Baja), 34.6 N, 37.9 N, 42.0 N and 46.25 N; Argentina at 46 S and
52.4 S; South Africa at 28.6 S and 31.5 S. One Namibia segment passed the filter.

## Results in detail

### Regional heat slopes (Figure 1)

Slope of R on H_anom after segment demeaning, with 1,000 year-block bootstrap draws
(files/results/region_slopes_main.csv; variants region_slopes_clear08.csv and region_slopes_r1999.csv).

| Region | Segments | Segment-years | Slope (95% interval) | Warmest-month SST (C) |
|---|---|---|---|---|
| N California | 4 | 168 | -0.59 (-0.85, -0.36) | 13.0 |
| Baja California | 13 | 501 | -0.31 (-0.47, -0.14) | 20.3 |
| S California | 13 | 545 | -0.29 (-0.45, -0.16) | 18.4 |
| C California | 9 | 377 | -0.17 (-0.33, -0.03) | 15.2 |
| Tierra del Fuego | 17 | 456 | -0.17 (-0.42, 0.06) | 9.3 |
| Kamchatka-Kuril | 15 | 410 | -0.09 (-0.28, 0.09) | 10.1 |
| Falklands | 27 | 672 | -0.09 (-0.23, 0.07) | 10.2 |
| Washington | 6 | 249 | -0.04 (-0.15, 0.07) | 12.1 |
| Namibia | 1 | 38 | -0.03 (-0.26, 0.16) | 16.2 |
| SE Alaska | 31 | 1014 | -0.02 (-0.12, 0.08) | 12.6 |
| W Cape | 9 | 346 | -0.01 (-0.09, 0.07) | 18.6 |
| N Cape | 4 | 150 | 0.03 (-0.29, 0.32) | 16.6 |
| Chubut | 5 | 145 | 0.06 (-0.31, 0.55) | 15.7 |
| Santa Cruz | 9 | 271 | 0.33 (-0.22, 0.88) | 12.5 |

With clear fraction >= 0.8 (133 segments), the four California Current slopes were -0.18 to -0.59 and all other
intervals included zero. Spearman rho with warmest-month SST: -0.12. With 1999-2026 full-coverage years (3,138
segment-years): rho +0.11.

### Absolute and relative heat (Figure 2)

In the pooled Northern Hemisphere data, R decreased when the peak monthly SST was above about 20 C, and when the
peak anomaly was above about 1 C. Southern Hemisphere segments rarely had peak SST above 21 C or anomalies above
2.5 C, and their binned means stayed near zero. Thus the Southern Hemisphere data cannot test the response above
21 C. The cross-region evidence against a single absolute limit comes from northern California (loss at 13-16 C)
and from the Western Cape (no loss at 18-21 C).

### Model transfer (files/results/model_summary_*.json, model_errors_*.csv)

| Test | M0 | M1 anomaly | M2 abs. hinge | M3 both | M4 anomaly hinge |
|---|---|---|---|---|---|
| Leave one region out | 0.763 | 0.751 | 0.755 | 0.748 | 0.749 |
| Forward 2014-2026 | 0.765 | 0.742 | 0.750 | 0.738 | 0.736 |
| Forward, region left out | 0.766 | 0.746 | 0.748 | 0.738 | 0.740 |

Values are equal-region-weight mean RMSE of R. M2 beat M1 in 9 of 14 regions in the leave-one-region-out test but with
a higher mean error. The fitted hinge was 20.0 C in all main fits. In the 1999-2026 variant, the forward hinge was 16 C
and the forward region-left-out M2 error was large (1.37), so the absolute hinge was not stable.

### Forward test in the California Current (Figure 3)

Mean forward error of M0 (= observed mean R in 2014-2026 minus the 1985-2013 mean level) and of M1:

| Region | M0 error | M1 error | Share explained by M1 |
|---|---|---|---|
| Baja California | -0.86 | -0.64 | 26% |
| S California | -0.47 | -0.28 | 41% |
| C California | -0.39 | -0.25 | 37% |
| N California | -1.84 | -1.68 | 9% |

Baja California and central California had additional large losses in 2023-2026 (median R -1.73 and -0.95) with
mean peak anomalies of about 1.8 and 1.6 C, lower than in 2014-2016 (3.6 and 2.9 C).

### Observation bias (Figure 4, files/results/coverage_bias.json, valid_fraction_by_era.csv, obsbias_summary.json)

- Coverage: mean within-segment R by number of valid quarters in the peak window: 1 quarter -0.44 (463
  segment-years), 2 quarters -0.02 (1,169), 3 quarters +0.06 (3,711). Within the same region-year, segments with fewer
  than three valid quarters were 0.19 lower (SE 0.04). The maximum of fewer images is lower.
- Landsat 5 era: before 1999, the valid fraction was 0.02-0.30 in Kamchatka-Kuril, Tierra del Fuego, Falklands,
  Chubut and Santa Cruz, and 0.71-1.00 in US regions. Early values in Kamchatka-Kuril and Tierra del Fuego were very
  low (median R -2.4 and -2.3 in 1985-1996) and are probably not real.
- Sensor transitions: after removal of heat terms and segment effects, the Southern Hemisphere year effect was 0.18
  higher in 2013-2017 than in 2008-2012 (Landsat 8 start), and 2012 (Landsat 7 SLC-off only) was 0.21 below
  2010-2011 and 2014-2015. These are possible sensor artefacts of about 20%, but real changes can give the same
  pattern. The Northern Hemisphere step after 2022 (-0.48) comes from the California and Baja losses; Washington changed
  by less than 0.1.

## Interpretation

The data do not support one heat-response rule for kelp canopy. The response is regional. In the California Current,
warm anomalies come with low nitrate and with the ecological changes after 2013 (sea-star wasting, urchin increase).
Our heat slope there mixes direct heat stress, nutrient supply and these changes. Outside the California Current,
including the warm Benguela coast (Western Cape) and the cold Southern Hemisphere coasts, canopy did not respond
clearly to SST anomalies of the observed size. An absolute warm limit near 20 C fitted the pooled Northern Hemisphere
data, but it did not transfer and it does not explain the northern California loss.

## Open questions and next steps

- Add nitrate proxies (upwelling indices, CUTI/BEUTI) and wave height to separate heat from nutrient and storm effects.
- Use the US SBC LTER NetCDF (pixel level, CC BY 4.0) when EDI access is restored. EDI required a login on 2026-11-12.
- Repeat with daily SST (degree heating) and with in-situ temperature where available.
- Test Peru (El Nino 1997-98, 2015-16, 2017, 2023) with a baseline after 1999; Peru failed the 1984-2013 baseline filter.
- Check the 2012 and 2013 sensor steps with pixel-level scene counts.
- Tasmania and other Australian kelp are hidden on Kelpwatch and were not tested.

## Reproduction

1. Get NOAA OISST v2.1 monthly SST (URL and hash in files/EXTERNAL_DATA_NOTICE.md).
2. Install Python 3.12 packages: numpy, pandas, scipy, matplotlib, netCDF4, mapbox-vector-tile, h3 (4.5.0).
3. Run `bash files/code/run_all.sh SCRATCH_DIR PATH/sst.mon.mean.nc`. It downloads Kelpwatch tiles and segment
   aggregates into SCRATCH_DIR (about 45 minutes at 2 parallel requests), builds the panels, models and figures.
4. Compare the downloaded files with files/provenance/kelpwatch_download_sha256.csv. Kelpwatch updates quarterly, so
   new downloads can differ.

Files: files/code (scripts 01-07), files/results (aggregate tables and JSON summaries; region_year_medians.csv holds the regional series of Figure 3), files/figures (PNG),
files/provenance (download hashes), files/EXTERNAL_DATA_NOTICE.md (third-party data, attribution and terms).
Record-level kelp series are not included (see the notice).
Intermediate hashes: cells_res5.json sha256 50534d69deb008062ee9dfbc246c10b48b33a6f68417de15faf55857a59370c0;
seg_sst_monthly.csv sha256 1218d6a84db6bf6bc4f318dca827f18fa59324ed593e9a93cac4c1589c111cc1.

## License

The LICENSE file (SCI baseline: CC BY 4.0 for text, figures and data; MIT for code) covers the authors' own material
only. Third-party data are described in files/EXTERNAL_DATA_NOTICE.md and are not part of this publication.
