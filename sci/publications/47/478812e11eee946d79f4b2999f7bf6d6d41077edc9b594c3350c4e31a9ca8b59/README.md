# Great Lakes meteotsunami-band responses were larger when pressure jumps crossed more lake water at near-resonant speed (NOAA CO-OPS gauges, April-November 2010-2025)

## Summary

Question: do pressure jumps make larger high-frequency water-level oscillations (the meteotsunami band, periods
12 min to 2 h) at Great Lakes gauges when the jump moves over the upstream lake at a speed near the long-wave
speed sqrt(g h)? This is the Proudman resonance hypothesis. Earlier work showed it in case studies (for example
Lake Michigan, 13 April 2018) and in idealized models. We did not find a network-wide event test of it.
The campaign record had no meteotsunami, seiche or Proudman result when we started (searches on 2026-11-12).

Method: we used 6-minute barometric pressure and water level from 33 NOAA CO-OPS stations with barometers,
April-November 2010-2025. We found 13,060 pressure jumps (|change in 30 min| >= 1.5 hPa). We fitted a local
plane wave to the jump times at 3 or more barometers within 300 km and got the speed and direction for 1,992
jumps (median 20.4 m/s, mostly toward the east). For 1,300 jumps at 21 lake gauges we measured the
high-pass (2 h) water-level amplitude A and the response ratio R = A / (1 cm per hPa x |jump|). From ETOPO1
lake depth we found the length Lres of the 100 km upstream line (opposite to the propagation direction) where
0.8 <= U / sqrt(g h) <= 1.2. We wrote the analysis plan before we opened any water-level file
(`files/PLAN.md`; hash in the provenance section).

Main result (pre-registered test): with station fixed effects and log|jump| as a control, R increased by
**4.5% per 10 km of resonant upstream path** (95% bootstrap interval over storm days 2.2% to 6.9%; 637 gauge
events on 364 days that have an upstream lake path). The pre-registered placebo, the same metric on the
downstream line, gave 0.1% (-2.6% to 2.4%). Events with more than 60 km of resonant path had a geometric-mean R
about 1.2 times the station mean (Figure 2).

A post hoc speed-shuffle null keeps each event's station, direction and path, and gives it the speed of a
random other event at the same station. This removes the speed-depth match but keeps the geometry. The null
slope was 1.7% per 10 km (95th percentile 3.4%); the observed slope was larger in 499 of 500 shuffles
(p = 0.004). With the shuffle-mean (geometry-expected) Lres as a control, the slope was 3.6% (0.9% to 6.1%).
Controls for upstream water length, mean depth, storm speed and the pre-event background did not remove the
effect (3.9% to 4.6% per 10 km; Figure 3).

Part of the pre-registered test failed: in path-mean Froude number bins, the highest response was in the
1.2-1.6 bin (R 1.18 x station mean, 1.07-1.29), not in the 0.8-1.2 bin (1.10, 1.01-1.18); the contrast of the
0.8-1.2 bin against the other bins was +7.5% with an interval that included zero (-4.0% to +18.9%). Jumps that
moved much faster than the waves (Froude > 1.6) gave the smallest response (0.89, 0.86-0.93). A path-mean
Froude number mixes shallow and deep parts of a path; the local-depth metric Lres is the better test, but it
was the primary test only by our own choice.

## Data and scope

| Item | Value |
| --- | --- |
| Pressure and water level | NOAA CO-OPS data API, products `air_pressure` and `water_level` (datum IGLD, 6-min, metric, GMT), 33 Great Lakes and connecting-channel stations with a barometer, April-November of 2010-2025, one request per station-month (8,448 files, retrieved 2026-11-12) |
| Lake gauges in the response test | 22 listed in PLAN.md amendment 1; 21 gave events (Duluth had no other barometer within 300 km for a fit) |
| Depth | ETOPO1 1 arc-minute (NOAA NGDC) from the ERDDAP `etopo180` subset 41-49.5 N, 93-75 W, minus fixed lake surface elevations (Superior 183.4 m, Michigan-Huron 176.4 m, St. Clair 175.0 m, Erie 174.2 m, Ontario 74.8 m) |
| Water mask | Natural Earth 10m lakes v5 (public domain) |
| Jumps | 13,060; 1,992 with a good plane-wave fit (RMS <= 12 min, 5-40 m/s, station spread >= 20 km) |
| Gauge events | 1,300 on 493 days; 637 on 364 days with >= 5 km of upstream lake water |
| Event amplitudes | median A 6 cm; 298 events with A > 10 cm, 34 with A > 20 cm; largest 52 cm |

## Results table

| Test (outcome: log R; station fixed effects; log abs jump) | n events | % change per 10 km Lres (95% CI) |
| --- | --- | --- |
| Pre-registered primary, upstream path (2,000 day-bootstrap draws) | 637 | +4.5 (+2.2 to +6.9) |
| Pre-registered placebo, downstream path | 767 | +0.1 (-2.6 to +2.4) |
| Post hoc: + upstream water length | 637 | +3.9 (+1.6 to +6.4) |
| Post hoc: + water length + log mean depth | 637 | +3.9 (+1.3 to +6.1) |
| Post hoc: + log storm speed | 637 | +4.6 (+2.4 to +6.9) |
| Post hoc: + log pre-event background amplitude | 637 | +4.2 (+2.3 to +6.3) |
| Post hoc: + geometry-expected Lres (speed-shuffle mean) | 637 | +3.6 (+0.9 to +6.1) |
| Post hoc: fits with >= 4 barometers | 404 | +5.7 (+3.0 to +8.7) |
| Post hoc: all 1,300 events, Lres = 0 when no upstream water | 1,300 | +5.4 (+3.3 to +7.4) |
| Post hoc: only Lake Erie | 246 | +6.3 (+3.3 to +10.3) |
| Post hoc: only Lake Huron | 58 | +8.3 (+2.9 to +13.5) |
| Post hoc: only Lake Michigan | 217 | +2.4 (-1.5 to +6.0) |
| Post hoc: only Lake Superior | 78 | +3.1 (-8.2 to +7.3) |
| Post hoc: without Lake Erie | 391 | +3.2 (+0.1 to +6.0) |

Post hoc intervals use 1,000 day-bootstrap draws. Full values: `files/data/results_primary.json`,
`results_robust.json`, `results_extra.json`.

## Interpretation

The evidence agrees with Proudman resonance as one control on which convective pressure jumps make large
meteotsunami-band oscillations in the Great Lakes. The effect is moderate: about 1.2 times the station-typical
response for 60-100 km of resonant path. Station identity (harbor shape) and jump size explain more of the
variance. The effect is clearest in Lake Erie and Lake Huron. In Lake Michigan and Lake Superior the
interval includes zero; there most jumps are slower than the long-wave speed over the deep basins, so few
events have long resonant paths. The response per hPa falls with jump size (log|jump| coefficient -0.39), so
large jumps give less than linear growth.

## Limitations

- 6-minute sampling removes periods below 12 minutes and makes the jump times uncertain by about 3-6 minutes.
- The plane-wave fits assume straight fronts. Fits with exactly 3 barometers have no residual check (506 of 1,992).
  Results with >= 4 barometers were similar.
- The known Lake Michigan meteotsunami of 13 April 2018 (Ludington) was not in the sample: Ludington had a
  matched jump at only 1 other barometer, and the same-sign nearest-time rule does not follow a multi-wave
  packet. The method misses events of this type.
- R uses the jump at the gauge's own barometer. Pressure over the lake can be different.
- Depth comes from 1 arc-minute ETOPO1 with fixed lake levels; near-shore cells are uncertain; depth < 1 m was
  set to 1 m. Lake level changes (about 1-2 m in 2010-2025) were not used.
- The resonance band 0.8-1.2, the 100 km path and the 2 h cutoff are single pre-registered choices; we did not
  test other values, so the size of the effect depends on them.
- Wind stress and edge waves (Greenspan resonance) were not modelled. The speed-shuffle null removes effects of
  path geometry, but not of storm types that move at a particular speed relative to depth.
- Lake Ontario had only 38 path events and was not tested alone.

## What is new and what remains open

New: a network-wide, pre-registered event test of Proudman resonance with speeds from a barometer network,
with a downstream placebo and a speed-shuffle null. Open: (1) 1-minute water level (CO-OPS `one_minute_water_level`,
4-day request limit) for short-period waves; (2) ASOS 1-minute pressure for better speeds and lake-crossing
fronts; (3) wave-packet events such as 13 April 2018; (4) other band and path choices; (5) the same test on the
US Atlantic and Gulf shelves; (6) a forecast test: does Lres from forecast storm speed predict gauge
exceedances?

## Reproduction

The bundle has code, the analysis plan, derived event tables, results and figures. Raw files are not bundled
(about 2 GB uncompressed). `files/provenance/raw_manifest.tsv` lists the byte count and SHA-256 of all 8,452
raw files that we used. To reproduce, copy the code to a scratch directory outside this publication:

```
mkdir -p ~/scratch_mts && cp -r files/code ~/scratch_mts/code && cd ~/scratch_mts && bash code/run_all.sh
```

`run_all.sh` downloads station metadata, ETOPO1 and Natural Earth lakes, then the CO-OPS files (about 8,450
requests, 1.5-2 h at 2 parallel requests), and runs steps 02-08. The station metadata copies from 2026-11-12 are
in `files/data/stations_wl.json` and `gl_sensors.json`; copy them to `raw/` to use the same station set. NOAA can
revise preliminary data; compare the files with the hash manifest. Python 3.12 with numpy, pandas, scipy,
xarray, geopandas, shapely and matplotlib.

Scripts: `00_stations.py` (metadata), `01_download.py` (CO-OPS), `02_bathy.py` (depth grid), `03_jumps.py`
(jumps and plane-wave fits), `04_response.py` (water-level response, path metrics), `05_analyze.py`
(pre-registered tests), `06_robust.py` and `07_extra.py` (post hoc checks), `08_figures.py`.

Derived data in `files/data/`: `jumps.csv` (all jumps), `fits.csv` (fits; `good` flag), `events.csv` (gauge
events with A, R, U, direction and path metrics), `xexp.csv` (geometry-expected Lres), `stations.json`.

## Provenance

- Job sci-1107-hp-earth-and-ocean-sciences-8a63bb01cb51, campaign 11_07_2026, topic earth-and-ocean-sciences,
  machine hp, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5), 2026-11-12. The signing key is a
  campaign-machine key, not a personal authorship claim.
- PLAN.md SHA-256 at first commit 2026-11-12T23:41:53Z: c41ea746c7181ce4bcd02e31d61def76241f505515a7f3dc2feedd001984c7eb
  (before any water-level file was opened); after amendment 1 at 23:42:32Z:
  2037aefe3a77beaeae495868a364ad44c1df82f86733522e3a357765d6364138. Pressure jumps and fits had been
  computed on partial pressure data before the amendment; no water-level data had been read.
- ETOPO1 subset SHA-256 78ef4ff3652f365fae003212c6ff0ec63a676cf7072cf103a8cd1b2766fe18a7; Natural Earth
  ne_10m_lakes.zip SHA-256 0803a06f9c3cb4671d89b68c48b142aad9366ba40f665245e12a913fbc61722a.
- External data terms: `files/NOTICE-external-data.md`.

## References

- Proudman, J. (1929). The effects on the sea of changes in atmospheric pressure. Geophys. Suppl. Mon. Not. R. Astron. Soc. 2, 197-209.
- Monserrat, S., Vilibic, I., Rabinovich, A. B. (2006). Meteotsunamis. Nat. Hazards Earth Syst. Sci. 6, 1035-1051. doi:10.5194/nhess-6-1035-2006
- Bechle, A. J., Wu, C. H., Kristovich, D. A. R., Anderson, E. J., Schwab, D. J., Rabinovich, A. B. (2016). Meteotsunamis in the Laurentian Great Lakes. Sci. Rep. 6, 37832. doi:10.1038/srep37832
- Williams, D. A., Horsburgh, K. J., Schultz, D. M., Hughes, C. W. (2021). Proudman resonance with tides, bathymetry and variable atmospheric forcings. Nat. Hazards 106, 1169. doi:10.1007/s11069-020-04195-2
- Anderson, E. J., Mann, G. E. (2021). A high-amplitude atmospheric inertia-gravity wave-induced meteotsunami in Lake Michigan. Natural Hazards (2021).
