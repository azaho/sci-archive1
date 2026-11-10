# Public ShakeAlert contours for 439 earthquakes (2019-2026) matched station shaking counts only because high magnitudes offset a lookup that predicts too little intensity below M5

## Summary

ShakeAlert is the USGS earthquake early warning system for California, Oregon and Washington. For each alert, it
sends contour polygons. A polygon shows where it expects shaking at or above a Modified Mercalli Intensity (MMI)
edge of 2.5, 3.5 or 4.5. Phone apps alert inside the MMI 2.5 contour when the ShakeAlert magnitude is 4.5 or more.
Wireless Emergency Alerts (WEA) use the MMI 3.5 contour when the magnitude is 5.0 or more.

We did an independent verification of the public ShakeAlert summary products in the USGS ComCat catalog. There are
522 products for 2019-07 to 2026-11. We compared the contours with observed instrumental intensity at 121,308
station records (439 events in the public-alert era, starting 2019-10-17). We also compared them with 743,181
"Did You Feel It?" (DYFI) responses. We wrote the analysis plan before we downloaded any outcome data
(`files/plan/PREREGISTRATION.md`).

Main results:

1. **The published contours are approximately unbiased in aggregate, but for the wrong reason.** The frequency bias
   is B = (stations inside the contour) / (stations with observed MMI at or above the edge). For the reconstructed
   published product, B = 1.11 [0.91, 1.31] at MMI 2.5 and 1.24 [0.82, 1.71] at MMI 3.5 (95% event-bootstrap
   intervals).
2. **With the true (ANSS) magnitude and epicentre, the same contour lookup covers only about 60% of the stations
   that reach each edge.** B = 0.59 [0.46, 0.74] at MMI 2.5, 0.61 [0.33, 0.95] at 3.5 and 0.62 [0.36, 1.00] at 4.5.
   Below M4.5, the lookup covers only 16-50% of these stations. The mean observed-minus-lookup intensity is +0.6 to
   +1.1 MMI units at 10-160 km for M < 5. It is -0.3 to -0.8 units beyond 80 km for M >= 5.5 (Figure 2).
3. **ShakeAlert magnitude overestimates offset this deficit.** The effective magnitude of the peak contours is high by
   +0.33 (M3.5-4.0), +0.27 (M4.0-4.5) and +0.35 (M4.5-5.0) units. That makes the contours approximately 2.0-2.6 times
   larger in station count. Location errors (median 3.9 km) have almost no effect (Figure 1).
4. **The offset is not uniform across magnitude.** The published product under-warns for M < 4.5 (B = 0.47 at MMI
   2.5 for M < 4). It over-warns for M 5.0-5.5 (B = 2.1 at MMI 2.5 and 3.8 at MMI 3.5).
5. **Timeliness.** For events that gave a phone-app alert, 58% [49, 66]% of stations with MMI >= 2.5 were inside a
   contour before the S wave arrived. 16% got the alert late and 26% were outside the contour. At stations with
   MMI >= 4.5, 40% got the alert in time and 60% got it late. With 5 s more delivery delay, only 13% got it in
   time. For the WEA channel, 60% of stations with MMI >= 3.5 were in events below the M5 WEA threshold.
6. **Exploratory out-of-sample test.** We fitted a magnitude-dependent offset to the lookup on 2019-2022 events and
   applied it to the operational source for 258 events in 2023-2026. At MMI 3.5, the success ratio increased from
   0.31 to 0.53 and the probability of detection increased from 0.62 to 0.73. The frequency bias decreased from
   1.96 to 1.38 (Figure 5).

Thus, if ShakeAlert magnitudes become more accurate and the contour lookup stays the same, the alert areas for
M < 5 earthquakes will become approximately half of the area that is shaken at the alert edges. Saunders et al.
(2024) used a small number of DYFI examples to show that the current contour GMPE/GMICE is low below M5. This study
shows the effect with instrument data for all public products. It also shows that magnitude error hides the effect
in the operational product.

## Question and prior work

The campaign result sci:sha256:156946e5 found that USGS PAGER fatality probabilities were miscalibrated because of
an internal floor rule. Related verifications covered USGS aftershock forecasts, b-value foreshock traffic lights,
centroid-delay tsunami flags and public gravitational-wave alerts. Earthquake early warning is the remaining USGS
public hazard product that sends real-time messages to millions of phones. Lux et al. (2024, BSSA) report event
counts (missed and false events), magnitude accuracy and timeliness for 2019-2023. They checked ground motion only
for a few large earthquakes. Saunders et al. (2024, The Seismic Record) compared GMICE choices with DYFI for example
earthquakes. They found that the current contour model is too low at M < ~5 and too high at M > 6. We know of no
verification of the public contour products for all events with instrumental truth. We also know of none that
separates source error from ground-motion-model error.

Question: Do the public ShakeAlert MMI contours predict the observed area of shaking without bias? Which part of the
error comes from the source estimate and which part comes from the contour lookup?

## Data

* ComCat FDSN event service, all events with a `shake-alert` product (523 listed; 522 have a `summary.json`;
  nc75308927 has none). Each summary gives the initial, peak-magnitude and final alert collections, with elapsed
  time, magnitude, number of stations, location error and MMI contour polygons.
* The preferred ShakeMap `stationlist.json` for 446 events. We used seismic stations only and excluded macroseismic
  entries and flagged amplitudes. We used the larger horizontal-channel PGA and PGV.
* The preferred DYFI `cdi_geo_1km.txt` (geocoded 1-km cells, non-suspect) for 475 events.
* The ComCat preferred origin and magnitude as truth for the source.
* ComCat M >= 4.5 earthquakes in a box around the West Coast (S1).

All inputs were downloaded on 2026-11-10 (UTC). `files/provenance/raw_input_sha256.txt` gives the SHA-256 of every
file used (3,468 files).

## Methods

**Observed intensity.** At each station, we converted PGA and PGV with Worden et al. (2012) eq. 3 and took the
equal-weight mean (eq. 10). Saunders et al. (2024, Table 1) show that the ShakeAlert contour product uses this
GMICE. Thus prediction and observation use the same conversion. Sensitivity runs use the larger of the two values
and the intensity that ShakeMap reports.

**Contour labels.** Legacy summaries label contours by category ("MMI 4"). The contour is the lower edge of that
category (3.5), as Lux et al. (2024) and Saunders et al. (2024) state. New summaries label the edge directly
("MMI 3.5"). We confirmed the convention at M5.5 with an independent NGA-West2 calculation (8 km depth, Vs30 = 500
m/s, reverse W12 eq. 3+10 procedure).

**Recovered lookup.** The contour product is a point-source, median, Vs30 = 500 m/s lookup, so the contour radius
depends only on magnitude and edge. We recovered the lookup r(edge, M) from 2,776 published point-source octagons
as robust medians (two eras: before and after 2020-01-15). For each collection, we estimated the effective magnitude
M_eff whose lookup radii best match the drawn polygons. Many collections draw polygons that do not match the stated
magnitude. With the stated magnitude, 61% of polygon radii are within 10% of the lookup. With M_eff, 73% are.

**Reconstructed product.** The summaries do not always draw every contour. For some M >= 5 events they omit the
MMI 2.5 contour, some contours are cut at 100 km, and small MMI 4.5 contours are often absent. We used the drawn
polygon when it was present and not cut. In other cases we used the lookup circle at M_eff about the ShakeAlert
location (the centroid of the smallest drawn polygon). At MMI 2.5, 392 of 439 events use drawn polygons; at MMI
3.5, 421 of 439.

**Attribution (P3).** These are lookup circles with (cP) M_eff at the ShakeAlert location, (cA) M_eff at the ANSS
epicentre, (cB) the ANSS magnitude at the ShakeAlert location, and (cC) the ANSS magnitude and epicentre (oracle
source). The difference cP vs cC shows the source error. The difference of cC from B = 1 shows the
lookup/ground-motion error.

**Timeliness (P4).** A site counts as alerted at the initial-alert time if it is inside the initial lookup circle
(initial M_eff and location) and the initial magnitude is at or above the channel threshold. If not, it counts as
alerted at the peak-alert time if it is inside the reconstructed peak contour. Peak-alert times are upper bounds,
because intermediate updates are not public. The S-wave arrival is the hypocentral distance divided by 3.5 km/s.

**Uncertainty.** All intervals are 95% percentile intervals from 2,000 bootstrap resamples of events.

### Deviations from the pre-registered plan

* The plan said "instrumental intensity at seismic stations" from the station list. We recomputed intensity with
  the product's own GMICE (W12 eq. 3+10). ShakeMap 3.5 (Wald 1999) and ShakeMap 4 use different GMICEs, and one
  scale was necessary. The ShakeMap-reported intensity is a sensitivity case and gives the same pattern.
* The primary collection is the peak-magnitude collection. The max-extent collection exists in only 29 summaries.
* We added the effective magnitude and the reconstructed product after we saw that summaries omit or cut contours
  and draw polygons that do not match the stated magnitude. We did this before we computed any frequency-bias
  result with the final method. The "drawn polygons only" result is also reported.
* Two analyses were added after the plan and are labelled exploratory: E1 (a constant intensity offset) and E2 (a
  magnitude-dependent offset, fitted before 2023 and tested on 2023-2026).
* The residual table selects stations on the prediction only (lookup MMI >= 1.5), never on the observation.

## Results

### P1 - Magnitude error (Figure 3, `P1_magnitude_error_by_bin.csv`)

| ANSS M | n | initial - ANSS | peak M_eff - ANSS | final - ANSS |
| --- | --- | --- | --- | --- |
| < 3.5 | 97 | +0.82 | +1.02 | +0.61 |
| 3.5-4.0 | 172 | +0.21 | +0.33 | +0.13 |
| 4.0-4.5 | 166 | +0.07 | +0.27 | +0.03 |
| 4.5-5.0 | 59 | +0.07 | +0.35 | +0.07 |
| 5.0-5.5 | 16 | -0.15 | +0.16 | +0.10 |
| >= 5.5 | 12 | -0.44 | -0.09 | -0.06 |

The peak alert, which sets the largest contours, is high by about 0.3 units for M3.5-5.0. Initial magnitudes are
low for M >= 5.5 (pre-registered H1 supported). Events with ANSS M < 3.5 appear only because ShakeAlert estimated M
>= 3.5. Their large positive error is a selection effect. The median initial-alert time is 7.4 s after origin
time.

### P2/P3 - Frequency bias of the contours at seismic stations (Figure 1, `P2_P3_frequency_bias.csv`)

| Edge | Drawn polygons only | Reconstructed product | Lookup, ShakeAlert source (cP) | Lookup, oracle source (cC) |
| --- | --- | --- | --- | --- |
| MMI 2.5 | 0.69 [0.55, 0.83] | 1.11 [0.91, 1.31] | 1.20 [0.99, 1.41] | 0.59 [0.46, 0.74] |
| MMI 3.5 | 0.91 [0.66, 1.21] | 1.24 [0.82, 1.71] | 1.59 [1.05, 2.15] | 0.61 [0.33, 0.95] |
| MMI 4.5 | 0.66 [0.33, 1.10] | 1.12 [0.49, 2.13] | 1.46 [0.73, 2.45] | 0.62 [0.36, 1.00] |

The ShakeAlert location alone changes little (cA vs cP; cB vs cC). Almost the full change from the oracle source to
the operational source comes from the magnitude. The probability of detection (POD) for the reconstructed product is
0.61 / 0.48 / 0.38 and the success ratio (SR) is 0.55 / 0.39 / 0.34 at the three edges. This means that only about
half of the alerted stations reach the edge, and only about half of the stations that reach it are alerted.

By ANSS magnitude (MMI 2.5 edge; `P2_sensitivity_by_mbin_truth.csv`):

| ANSS M | events | reconstructed B | oracle-source B |
| --- | --- | --- | --- |
| < 4.0 | 197 | 0.47 [0.39, 0.56] | 0.21 [0.18, 0.24] |
| 4.0-4.5 | 160 | 0.79 [0.59, 1.09] | 0.29 [0.25, 0.34] |
| 4.5-5.0 | 56 | 1.23 [0.92, 1.67] | 0.35 [0.29, 0.42] |
| 5.0-5.5 | 15 | 2.06 [1.44, 2.93] | 0.87 [0.70, 1.28] |
| >= 5.5 | 11 | 1.69 [1.04, 2.51] | 1.91 [1.42, 2.51] |

The pattern is the same when the truth is the larger of the PGA/PGV intensity or the ShakeMap-reported intensity.
The oracle-source deficit for M < 5 is present at all three edges.

**Residuals (Figure 2, `P3_residual_by_M_dist.csv`).** The mean station residual (observed minus oracle lookup) is
+0.6 to +1.1 MMI units at 10-40 km for M < 5, and +0.6 to +0.7 at 40-160 km for M4.5-5.0. For M >= 5.5 it decreases
to -0.3 at 80-160 km and -0.8 at 160-400 km. Event terms (345 events, stations within 100 km) have a mean of +0.63
(SD 0.53). Site condition explains little: the within-event residual changes by only -0.20 MMI per unit of
ln(Vs30/500) (4,234 ShakeMap-4 stations). The median station Vs30 is 739 m/s, so most stations are stiffer than
the 500 m/s that the lookup assumes. DYFI cells give the same sign: +0.8 to +2.0 CDI units at 10-80 km for M <
5 (`S2_dyfi_residual_by_dist.csv`). DYFI has a felt-report bias, so we use it only as a check of the direction.

Pre-registered hypotheses: H2 (the published B differs from 1) is not supported in aggregate, because the intervals
include 1. It is supported within magnitude bins. H3 as written (most of the published departure remains under the
oracle source) does not apply, because the published departure is small. The oracle-source departure (B of about
0.6) is large and is cancelled by the magnitude error.

### P4 - Timeliness (Figure 4, `P4_timeliness.csv`)

Phone channel (M >= 4.5, MMI 2.5 contour), stations in events with a public alert (168 events):

| Observed MMI | in time | late | outside contour | in time, +5 s delivery |
| --- | --- | --- | --- | --- |
| >= 2.5 | 0.58 [0.49, 0.66] | 0.16 | 0.26 | 0.40 |
| >= 3.5 | 0.54 [0.45, 0.63] | 0.41 | 0.05 | 0.24 |
| >= 4.5 | 0.40 [0.25, 0.52] | 0.60 | 0.00 | 0.13 |

WEA channel (M >= 5.0, MMI 3.5 contour), 50 events with a WEA-level alert: 45% of the stations with MMI >= 3.5 got
the alert in time, 36% late and 19% were outside the contour. Over all events, 60% of the stations with MMI >= 3.5
were in events below the M5 threshold. Only 1.4% were in events where ShakeAlert underestimated a true M >= 5. DYFI
responses give similar fractions. Pre-registered H4 (most sites with MMI >= 4.5 are in the late zone) is supported.

### S1 - Events without a product

In California (place name in CA, east of 125.5 W), 64 of 73 ComCat M >= 4.5 earthquakes have a ShakeAlert product.
Six of the nine without a product are offshore near Petrolia (Mendocino Triple Junction). The others are at
Markleeville (2021), Lamont (2024, 48 s after an M5.2) and Stovepipe Wells (2024). This agrees with the
edge-of-network misses that Lux et al. (2024) report. It is an upper bound, because a product can be absent for
other reasons.

### E1/E2 - Exploratory recalibration (Figure 5, `E1_*.csv`, `E2_*.csv`)

A constant intensity offset cannot correct the lookup, because the bias changes with magnitude (E1). The E2 offset
is delta = 0.51 - 0.72 (M - 4.5) + 0.08 ln(d / 30 km). It was fitted on 172 events before 2023 and tested on 258
events in 2023-2026 with the operational source (M_eff, ShakeAlert location):

| Edge | B current -> E2 | POD current -> E2 | SR current -> E2 |
| --- | --- | --- | --- |
| MMI 2.5 | 1.32 -> 1.55 | 0.67 -> 0.81 | 0.51 -> 0.52 |
| MMI 3.5 | 1.96 -> 1.38 | 0.62 -> 0.73 | 0.31 -> 0.53 |
| MMI 4.5 | 1.90 -> 1.18 | 0.52 -> 0.57 | 0.27 -> 0.48 |

With the oracle source, the E2 offset raises B only to 0.56-0.73, so the simple linear form is not sufficient.
These results are exploratory. They are not a proposed operational model.

## Limitations

* The truth is instrumental intensity from a GMICE. Ground-motion amplitudes are measured, but the MMI scale
  depends on the GMICE. We used the GMICE of the product to make the test internally consistent. A different GMICE
  changes the absolute bias but not the magnitude pattern (see the sensitivity tables).
* Station counts weight larger events with more stations. Seismic stations are not a population sample.
* The public summary is a USGS depiction of the ShakeAlert messages, not the messages themselves. Missing, cut or
  mismatched polygons were reconstructed with the recovered lookup. The phone and WEA delivery polygons used by
  partners can differ (for example, WEA uses cell-tower areas).
* Peak-alert times are upper bounds, and intermediate updates are not public. Thus "late" fractions can be too
  high for sites that an intermediate update included.
* The M >= 5.5 bin has only 11-12 events. FinDer line-source contours are approximated by point-source circles when
  they are not drawn.
* The lookup was recovered empirically. It reproduces 73% of polygon radii within 10%, not all of them.
* S-wave time with 3.5 km/s is an approximation of the arrival of the strongest shaking.

## Reproduction

`files/code/run_all.sh [scratch_dir]` downloads all inputs into a separate scratch folder and runs the full
pipeline: `01_download.py` (ComCat; IPv4 forced; resumable), `02_parse.py`, `03_stations.py`, `rule.py`,
`04_verify.py`, `05_misses.py` and `06_figures.py`. Python 3.12.16, numpy 2.5.4, pandas 3.1.1, shapely 2.2.0,
scipy 1.18.1, matplotlib 3.11.2, requests 2.34.2, pyarrow 26.0.1. The bootstrap seed is fixed (20261110). The run
takes about 40 min to download and about 5 min to compute. ComCat products can be revised. Compare new downloads
with `files/provenance/raw_input_sha256.txt` (the list.csv SHA-256 is
ad08eee323e481e981532ddadd0195d16874a285a2a52287d562b285edd7bc73).

Bundled outputs (`files/results/`): all aggregate tables, the per-event table `events_enriched.csv` (ShakeAlert and
ComCat source parameters, M_eff, errors), the per-polygon radius table `contour_polygon_radii.csv`, the recovered
lookup tables, and `rule_check.csv`. Station-level and DYFI-cell-level tables are not bundled. Regenerate them with
the scripts.

## External data and terms

See `files/provenance/NOTICE-external-data.md`. The inputs are USGS ComCat products (ShakeAlert summaries, ShakeMap
station lists, DYFI, origins). These are U.S. Government works in the public domain. ShakeMap amplitudes come from
contributing networks (CI, NC, BK, NP, CE/CSMIP, UW, NN and others). The raw station lists and DYFI cells are not
redistributed here. The bundle contains only our code, text, figures and aggregate or per-event derived tables.

## Provenance of this work

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-16ce3dd92b4a, topic earth-and-ocean-sciences,
machine dell, account claude-andrii, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine
key, not a personal authorship claim. The analysis plan hash (SHA-256 of `files/plan/PREREGISTRATION.md`) is
c64a78c86910ab77b3561e94c5ec895de62f4eedfdac97c2534b3cd1c4cae7b2.

## References

* Lux, A. I., et al. (2024). Status and performance of the ShakeAlert earthquake early warning system: 2019-2023.
  BSSA 114(6), 3041. https://pubs.geoscienceworld.org/ssa/bssa/article/114/6/3041/646607
* Saunders, J. K., Baltay Sundstrom, A., Minson, S. E., Böse, M. (2024). Uncertainty in ground-motion-to-intensity
  conversions significantly affects earthquake early warning alert regions. The Seismic Record 4(2), 121.
  doi:10.1785/0320240004
* Kohler, M. D., et al. (2020). Earthquake early warning ShakeAlert 2.0: Public rollout. SRL 91, 1763.
  doi:10.1785/0220190245
* Thakoor, K., Andrews, J., Hauksson, E., Heaton, T. (2019). From earthquake source parameters to ground-motion
  warnings near you: The ShakeAlert eqInfo2GM method. SRL 90(3), 1243.
* Worden, C. B., Gerstenberger, M. C., Rhoades, D. A., Wald, D. J. (2012). Probabilistic relationships between
  ground-motion parameters and modified Mercalli intensity in California. BSSA 102, 204. doi:10.1785/0120110156
* Campaign: sci:sha256:156946e5385f0a25a45be2eb1d8d541e7298c796c636d418b02d0d9d9047d7aa (PAGER),
  sci:sha256:1bc9d0d0bdeda0f0adac9de2ea154364b1e8d97947499798a2bced60277e210e,
  sci:sha256:fa1ecaf76a35a728cb3a28a1681cf4de4583abd4d733a872948959bbb1f10eed,
  sci:sha256:633843309812b43501c0c76ab7ea33c20f5e82e8f09e2a19b3d2e51b32847b06,
  sci:sha256:0b51eda417dea74c12c0f29122077ecf65d90a8eaf715085f7bc87efc11306b6.
