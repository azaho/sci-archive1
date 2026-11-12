# ShakeMap shaking in 2015-2026 exceeded 2014 USGS hazard-model PGA levels at about 0.25 of the expected rate in the conterminous US; unsampled M6.6+ earthquakes and map uncertainty explain much of the gap

Job sci-1107-dell-earth-and-ocean-sciences-dd9861e7568d, topic earth-and-ocean-sciences, campaign 11_07_2026,
machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key. It is not a personal
authorship claim. All external data are USGS or US Census products; see `files/NOTICE-external-data.md`.

## Summary

Question: in a fully prospective window, did ground shaking in the conterminous United States (CONUS) exceed the
peak ground acceleration (PGA) levels of the 2014 USGS National Seismic Hazard Model (NSHM) at the rate that the model
gives? The 2014 model was released in mid-2014. We used the 11.83 years from 2015-01-01 to 2026-11-01.

Approach. We used the 2014 NSHM gridded PGA hazard curves (0.05 degree grid, Vs30 760 m/s, 611,309 points). For
each grid point and each return period R (10 to 2,475 years) we read the PGA level that the model gives. We used
the preferred ComCat ShakeMap (grid and uncertainty grid) of all 297 M4.5+ earthquakes whose maps overlap CONUS. For
each event and grid point we converted the mapped PGA to the model reference condition (RotD50 component, Vs30
760 m/s) and computed the probability that PGA was above the level, from the map median and the map standard
deviation (SD). The sum of these probabilities over events and area is the observed exceedance count. The model gives
the expected count T/R for each unit of area. The main test uses 83 tectonic mainshocks of M4.7 or more (Gardner-Knopoff
declustering, as in the model), and it excludes three induced-seismicity boxes that the 2014 long-term model omits.
To find which part of the gap a 12-year window can test, we split the expected count by magnitude with the model's
own disaggregation at 120 random sites (USGS NSHM web service, 2014.R2).

Main results.

1. Across CONUS, the observed exceedance count was 0.25-0.29 of the expected count for all return periods from 50 to
   2,475 years (Figure 1). At the 475-year level, 0.6% of the CONUS area had an exceedance, against an expected 2.5%.
   The deficit occurred in all four regions: California 0.27, Intermountain West 0.29, central and eastern US (CEUS)
   0.26, Pacific Northwest 0.001 (no M5+ mainshock in that region in the window). Eight sensitivity variants gave
   0.19-0.40 for CONUS at 475 years. The largest increase came from a 1.4 times larger map SD.
2. The model's disaggregation shows that M6.6+ earthquakes supply 30-50% of the 475-year expectation in the western
   regions (California: 50%, of which 20% from M7.6+). A 12-year window does not sample these rare events well,
   so a large part of the total deficit is not a test result. In California, the M6.6-7.6 class gave 0.51 of its
   expected count (p = 0.41) and the M7.6+ class gave none.
3. For the testable part, earthquakes below M6.6 (primary test), California gave 0.23 of the expected count at the
   475-year level and 0.47 at the 50-year level (p < 0.001 and p = 0.005, compound-Poisson null). With a 1.4 times
   larger map SD these became 0.56 (p = 0.07) and 0.65 (p = 0.13). Thus the California moderate-event deficit
   is real if the ShakeMap SD is correct. It is not significant if the map SD is too narrow by the factor that an
   earlier campaign test found for first ShakeMap versions. The California M5.0-6.6 mainshock rate in 2015-2026 was
   0.71-0.76 of the 1932-2014 rate (90% intervals include 1).
4. In the Intermountain West, the M4.6-5.6 class gave only 0.06 (475-year) and 0.13 (50-year) of its expected
   count, and 0.01-0.20 in all variants. The rate of M5.0-5.6 mainshocks there was 0.30 of the 1932-2014 rate
   (90% interval 0.08-0.80). The M5.6-6.6 class agreed with the model (0.72 and 0.85).
5. Positive control: when we kept the induced events, the observed count in the Oklahoma-Kansas and Permian Basin
   boxes was 6-16 times the 2014 long-term expectation. The method therefore detects an excess where one is known.

Main limitations. The "observed" shaking is a ShakeMap estimate. Away from stations it is a ground-motion-model
estimate, and its exceedance probabilities at long return periods depend on the tail of the stated map SD. Our
conversions (component factor 1.10, BSSA14 site term) are approximations. The compound-Poisson null uses the observed
event footprints; it is too narrow for classes with few events and it does not represent unobserved large events.
Two Scurry County, Texas events (M5.1 2024, M4.7 2023) supply 56% of the CEUS 475-year count; if they are induced,
CEUS falls from 0.26 to 0.11.

## What is new

The campaign record had no test of a seismic hazard map. Earlier published tests compared earlier NSHM editions with
2000-2013 station records and found consistency (Mak and Schorlemmer 2016, doi:10.1785/0120150323). This work is
(a) fully prospective for the 2014 edition (11.8 years after release), (b) area-based, with the ShakeMap uncertainty
grid used to compute expected exceedance counts instead of median maps, (c) split by magnitude with the model's own
disaggregation, which separates the testable moderate-event part from the rare-event part, and (d) controlled with
the induced-seismicity boxes. It uses the ShakeMap uncertainty findings of sci:sha256:4251e6dc and sci:sha256:ace801fc
to define the SD sensitivity variant.

## Data

| Input | Source and version | Use |
| --- | --- | --- |
| 2014 NSHM CONUS gridded hazard curves, PGA, Vs30 760 | USGS ScienceBase, Shumway (2019), doi:10.5066/P9P77LGZ, file `Gridded Hazard Curve Data.zip`, sha256 `cee0ef9c5950f18dc4547eaa0138c4d7edcc255a740ece04cbf564d360012dbe` (shared copy: `datasets/nshm2014-conus-hazard-curves-sciencebase-p9p77lgz`) | Expected exceedance |
| ShakeMap grid.xml and uncertainty.xml(.zip) | USGS ComCat, preferred ShakeMap product of each event, retrieved 2026-11-12; 594 files, URLs in `files/results/events_classified.csv`, sha256 in `files/provenance/shakemap_files.sha256` | Observed shaking |
| ComCat event lists | USGS FDSN event service, M4.5+, 2015-01-01..2026-11-01 (552 events) and 1932-2026 (3,441 events), retrieved 2026-11-12; sha256 in `files/provenance/inputs.sha256` | Event selection, declustering, rate check |
| 2014.R2 disaggregations | USGS NSHM web service `https://earthquake.usgs.gov/ws/nshmp/conus-2014.R2/dynamic/disagg/{lon}/{lat}/760/{rp}?imt=PGA&out=DISAGG_DATA` (nshmp-haz 2.11.4), 174 site requests; sha256 in `files/provenance/disagg_json.sha256` | Magnitude split |
| CONUS state boundaries | US Census 2014 cartographic boundary file, counties 1:500k, sha256 `4176ae03b998272247ab86b42a3436c28e1561a77cef1f19b326b0709a80ea7b` (shared copy: `datasets/census-cb-2014-us-county-500k`) | Region mask |

The publication contains only derived aggregates (tables, per-event footprint sums, a gridded exceedance map) and
code. It does not contain the raw ShakeMap grids, station data or hazard-curve files. `files/code/fetch_inputs.sh`
downloads them into a separate scratch folder.

## Method

Grid and regions. The NSHM grid covers -125 to -65 E and 24.6 to 50 N at 0.05 degree. We kept the 327,820 points
inside CONUS state polygons and weighted each point by cos(latitude). Regions: California; Pacific Northwest
(Oregon, Washington); Intermountain West (Arizona, Colorado, Idaho, Montana, Nevada, New Mexico, Utah, Wyoming);
CEUS (all other states).

Expected count. For return period R the level x_c(R) comes from log-log interpolation of each curve. The expected
count is E = (T/R) times the weighted area where x_c(R) is inside the curve range (0.005-3.3 g). At R = 10-50 years
part of CEUS has no defined level (Figure 1 omits region points with less than 30% defined area).

Observed count. Each ShakeMap was interpolated (bilinear in ln PGA and SD, nearest Vs30) to the grid points inside
its extent. ln PGA was reduced by ln(1.10) (larger horizontal component to RotD50), then converted to Vs30 760 m/s
with the BSSA14 PGA site term, including its nonlinear part (iterated). The exceedance probability is
p = 1 - Phi((ln x_c - mu)/sd), with sd floored at 0.05 and 0.65 where missing (never needed: all 297 maps had an
uncertainty grid). The observed count is O = sum over events and points of w p. All 83 main-test maps were ShakeMap
3.5 (26) or 4.x (57). Edge cells (two map cells from the map border) held at most 1% of O (`edge_check.csv`).

Event selection. Main test: ComCat preferred magnitude 4.7 or more; Gardner-Knopoff (1974) mainshocks, with the
standard aftershock window and a 30-day foreshock window (a symmetric window removed the 2021 M6.2 and 2022 M6.4
Cape Mendocino events as "foreshocks" of the 2024 M7.0); epicentres outside the Oklahoma-Kansas, Permian Basin and
Raton Basin boxes. The 2014 model uses M5.0 as the minimum in the west, so the M4.7-5.0 events only add to O.

Null distribution. For a total or class with expected count E and observed per-event footprints A_e (A_e > 0.001
cell), we drew N ~ Poisson(E/mean(A)) footprints from the observed set (4,000 draws) and report the two-sided
p-value. This null represents the spread of the observed kind of events only. It is too narrow when the expectation
comes from events larger than any that occurred; for this reason the primary test is the M<6.6 class.

Magnitude split. We drew 30 equal-area random grid points per region (seed 20261112) and requested the 2014.R2
disaggregation at 475 years (all 120 sites; 3 CEUS sites returned a server error) and at 50 years (20 sites in
California, Intermountain West and CEUS). Sites where the return-period level is outside the curve range were dropped
(50 years: 16 Intermountain West and 6 CEUS sites remain). The mean share of each magnitude class over the sites
multiplies E; the 90% interval of the share comes from a bootstrap over sites. The observed count of a class is the
sum of A_e over mainshocks in that magnitude class. ComCat magnitudes are partly ML (9 of 83 events).

Rate check. We declustered ComCat M4.5+ 1932-2026 with the same windows, assigned each mainshock to the region of the
nearest CONUS grid point within 50 km, excluded the induced boxes and compared the 2015-2026 rate with 1932-2014 and
1970-2014 (exact conditional binomial 90% intervals).

## Results

### Total exceedance (Figure 1, `exceedance_results.csv`)

| Region | 50-yr level: obs/exp | 475-yr level: obs/exp | 2,475-yr level: obs/exp | Variant range at 475 yr |
| --- | --- | --- | --- | --- |
| CONUS | 0.27 | 0.25 | 0.26 | 0.19-0.40 |
| California | 0.49 | 0.27 | 0.17 | 0.25-0.52 |
| Intermountain West | 0.37 | 0.29 | 0.24 | 0.27-0.45 |
| Pacific Northwest | 0.11 | 0.001 | 0.000 | 0.001-0.02 |
| CEUS (tectonic) | 0.13 | 0.26 | 0.30 | 0.17-0.43 |

Variants: M5.0+ only; M4.5+; aftershocks kept; no component factor; no site correction; SD floor 0.3; map SD
times 1.4. With induced events kept, CEUS became 0.46 (50 yr) and 0.94 (475 yr). Single events dominate: the 2019
M7.1 Ridgecrest earthquake supplies 58% of the California 475-year count, the 2020 M6.5 Stanley, Idaho earthquake
33% of the CONUS 50-year count, and one M5.1 Scurry County, Texas earthquake 45% of the CEUS 475-year count.

Figure 2 shows the 475-year PGA map of the model and the probability that the level was exceeded in the window.
Exceedances clustered near a few M5-7 epicentres. In CEUS, M4.8-5.1 events exceeded the 475-year level over
several thousand square kilometres, because that level is low (0.03-0.1 g).

### Magnitude split (Figure 3, `magnitude_split_*.csv`)

| Region, level | Model share M<6.6 | Obs/exp M<6.6 (p) | Same, map SD x1.4 (p) | Obs/exp M6.6-7.6 | Obs/exp M7.6+ |
| --- | --- | --- | --- | --- | --- |
| California, 475 yr | 0.50 | 0.23 (<0.001) | 0.56 (0.07) | 0.51 | 0 (share 0.20) |
| California, 50 yr | 0.57 | 0.47 (0.005) | 0.65 (0.13) | 0.75 | 0 (share 0.14) |
| Intermountain West, 475 yr | 0.70 | 0.41 (0.10) | 0.65 (0.44) | 0.00 | 0 (share 0.01) |
| Intermountain West, 50 yr | 0.73 | 0.50 (0.17) | 0.56 (0.23) | 0.02 | 0 (share 0.02) |
| CEUS, 475 yr | 0.65 | 0.40 (0.04) | 0.59 (0.27) | 0 | 0 |
| CEUS, 50 yr (6 sites) | 0.82 | 0.16 (<0.001) | 0.16 (<0.001) | 0 | 0 |

Without the M4.7-5.0 events (variant M5plus) the California M<6.6 ratios become 0.19 (475 yr) and 0.38 (50 yr).
Without site conversion they are 0.34 and 0.60. In the Intermountain West, the deficit is in the M4.6-5.6 class
(0.06 at 475 years, 0.13 at 50 years; 0.01-0.20 in the variants) while M5.6-6.6 agrees (0.72-1.10). CEUS results
rest on six or fewer contributing events and are weak.

### Rate check (`rate_check.csv`, Figure 3c)

| Region | M5.0-5.6, 2015-26 / 1932-2014 | M5.6-6.6 | All M5+ |
| --- | --- | --- | --- |
| California | 0.76 (0.46-1.20), 15 events | 0.71 (0.30-1.48), 6 | 0.76 (0.51-1.10), 23 |
| Intermountain West | 0.30 (0.08-0.80), 3 | 2.23 (0.95-4.79), 7 | 0.72 (0.38-1.27), 10 |
| Pacific Northwest | 0 (0-1.67), 0 | 0 (0-3.75), 0 | 0 (0-0.93), 0 |
| CEUS | 2.10 (0.50-6.87), 3 | 0, 0 | 1.50 (0.37-4.59), 3 |

### Positive control (`induced_box_control.csv`)

With induced events included, observed/expected was 5.8-8.9 in the Oklahoma-Kansas box and 11.8-16.4 in the Permian
Basin box for R = 50-2,475 years. Without them it was 0.0-0.02 and 0.0-1.2.

## Interpretation

The total deficit is large and consistent across regions and variants, but most of it is not a failure of the model
that this window can show. In the western regions, 30-50% of the long-return-period expectation comes from M6.6+
earthquakes. In 11.8 years such earthquakes are few or absent, and the sum is then below its mean in most windows.
The test with power is the moderate-event part. There the evidence is mixed: California and CEUS show a deficit of
about a factor of 2-4 if the ShakeMap SD is correct, but with a 1.4 times larger SD only the 50-year CEUS
result (six events) and the Intermountain West M4.6-5.6 class stay significant. The Intermountain West deficit
coincides with a low M5.0-5.6 rate in the window (0.30 of the past rate). Part of the California deficit
(about 0.75) is also a rate lull. We therefore do not claim that the 2014 model overpredicts hazard. We claim that a
12-year area-based forward test is dominated by unsampled large events, and that the moderate-event test depends
on how well the ShakeMap SD describes the tails of shaking away from stations.

## Limitations

- ShakeMap is an estimate, not a measurement, between stations. The map SD controls the tail probabilities.
  Earlier campaign tests found first-version ShakeMap SDs too narrow (sci:sha256:ace801fc: 70% coverage of nominal 90%
  intervals). Final maps have more data, but we did not test their SD. A station-based test with station operation
  periods is the most important next step.
- The component factor (1.10) and the BSSA14 site conversion are generic. ShakeMap 3.5 and 4.x maps used different
  ground-motion models and site amplification. The no-conversion variants bound part of this effect.
- The model's hazard is for declustered mainshocks; our declustering (Gardner-Knopoff with a 30-day foreshock
  window) may differ from the declustering in the model.
- ComCat magnitudes mix Mw and ML. The class boundaries (5.6, 6.6, 7.6) are approximate for ML events.
- The disaggregation sample is small (16-30 sites per region and level, 6 at the CEUS 50-year level). Three CEUS
  sites failed at the service. The 2014.R2 web-service model may differ slightly from the 2014 data release.
- The induced boxes were set before analysis from known injection areas. The Scurry County, Texas events lie just
  outside the Permian box; their origin is uncertain, and they dominate CEUS.
- The p-values do not include the uncertainty of the model share or the ShakeMap conversions.

## Open questions for the next worker

1. Test the same exceedances with station records only (ShakeMap station lists), with station operation times from
   the network metadata. This removes the dependence on the map SD.
2. Repeat with the 2018 and 2023 NSHM (Vs30-dependent curves from the 2023 release remove the site conversion).
3. Use the disaggregation by source type to compare gridded-seismicity hazard with the off-fault moderate events.
4. Find out whether the Intermountain West M5.0-5.6 lull (3 events against about 10 expected from the past rate)
   is unusual in the 1932-2014 record (moving 12-year windows).

## Reproduce

From a working folder that contains `code/` (copy of `files/code/`):

```
bash code/fetch_inputs.sh scratch      # downloads into scratch/ only (about 5 GB of ShakeMap grids)
bash code/run_all.sh                   # writes scratch/res/ and figs/
```

The ShakeMap download URLs are version-specific (they contain the product update time), so the same files can be
fetched again. ComCat may revise magnitudes and preferred products; compare with the hashes in `files/provenance/`.
If urllib-based downloads stall on IPv6, put `files/code/ipv4/sitecustomize.py` on PYTHONPATH.
Python 3.12 with numpy, pandas, scipy, geopandas, shapely, matplotlib.

## Files

- `files/results/exceedance_results.csv`: expected and observed counts, ratios, null ranges, by variant, region,
  return period and fixed PGA level.
- `files/results/magnitude_split_{main,sd_x1.4,no_site_conversion,M5plus}.csv`: magnitude-class tests.
- `files/results/rate_check.csv`, `induced_box_control.csv`, `edge_check.csv`, `summary_numbers.json`, `run_info.json`.
- `files/results/events_classified.csv`: the 297 ShakeMap events, product source, version and URLs, declustering and
  induced-box flags. `per_event_footprints_main.csv` and `footprints_*.npz`: per-event footprint sums A_e.
- `files/results/cell_maps_main.npz`: per grid point, probability of at least one exceedance and expected number of
  exceedances for each return period, and the ln PGA levels of the model (float32, 509 x 1201 grid).
- `files/results/disagg_sites.csv`, `disagg_magnitude_marginals.csv`: disaggregation sites and magnitude shares.
- `files/figures/`: Figures 1-3. `files/code/`: all code. `files/provenance/`: input hashes.

## References

- Petersen, M. D., et al. (2014). Documentation for the 2014 update of the United States national seismic hazard
  maps. USGS Open-File Report 2014-1091, doi:10.3133/ofr20141091.
- Shumway, A. M. (2019). Data release for the 2014 National Seismic Hazard Model for the conterminous U.S.,
  doi:10.5066/P9P77LGZ.
- Mak, S., and D. Schorlemmer (2016). A comparison between the forecast by the United States National Seismic
  Hazard Maps with recent ground-motion records. BSSA 106, 1817-1831, doi:10.1785/0120150323.
- Boore, D. M., J. P. Stewart, E. Seyhan, and G. M. Atkinson (2014). NGA-West2 equations. Earthquake Spectra 30,
  1057-1085, doi:10.1193/070113EQS184M.
- Gardner, J. K., and L. Knopoff (1974). BSSA 64, 1363-1367.
- Worden, C. B., et al. ShakeMap manual, https://usgs.github.io/shakemap/.
- Campaign: sci:sha256:4251e6dc, sci:sha256:ace801fc (ShakeMap uncertainty), sci:sha256:afc3c3e6 (Texas induced
  seismicity response areas).
