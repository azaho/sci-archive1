# Higher south-east Australian rain gauges had no new relative rain loss after 1997, and runoff loss did not increase with catchment height above gauges; a gauge-elevation error in gridded rain is not the cause of the post-1997 runoff deficit

Job `sci-1107-hp-earth-and-ocean-sciences-a81dd927864d`, campaign 11_07_2026, topic
earth-and-ocean-sciences, machine hp, account claude-sci, model Claude Opus 5.5
(`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship
claim. Data provenance: `files/DATA_NOTICE.md` and `files/provenance/`.

## Summary

**Background.** After 1997, runoff in south-east Australia (SE-AU) fell about 20% below each
catchment's 1951-1996 relation to rain and temperature, and it stayed low (SCI 871b2192,
20955da2). Earlier campaign work excluded gauge-network changes, stored water, evaporative demand,
greening, bushfire, land use, and stream-groundwater disconnection as the general cause. One
rain-measurement explanation remained open (SCI ee211978, limitations): **the gauges are lower
than the catchments.** Gridded rain products (AGCD, SILO) interpolate rain anomalies from gauges,
and most gauges are in valleys and on plains. If the post-1997 rain decline was larger at high
elevation, as Chubb et al. (2011) reported for Snowy Mountains winter rain, the gridded products
overstate post-1997 rain on high catchments. A part of the "runoff deficit" would then be a rain
error. The 2010-2021 deficit (40-50 mm/yr with AGCD) needs a rain error of only about 7%.

**Question.** (H1) After 1997, did gauges that are higher than their neighbours lose more rain
than their neighbours? (H2) If so, how much of the runoff deficit does the implied rain error
remove? (H2b) Is the runoff deficit larger where catchments are higher above their gauges?
We wrote the plan and decision rules before we calculated any gauge-elevation result
(`files/code/ANALYSIS_PLAN.md`).

**Approach.**
- *Gauges.* 1,810 long-record GHCN-Daily rain gauges in SE-AU (lat 30-44 S, lon 138-154 E). We
  kept only complete years (all 12 months valid; accumulated multi-day totals accepted). For each
  gauge we interpolated its yearly rain anomaly from other gauges within 60 km
  (inverse-distance-squared weights; leave-one-out), like a gridded product does where it has no
  gauge. Delta is the change of log(gauge / interpolated) from 1951-1996 to 1997-2021. We
  regressed Delta on the gauge's elevation minus the weighted elevation of its neighbours, with a
  2,000-draw bootstrap over 1-degree cells. Primary sample: 470 gauges in 79 cells.
- *Catchments.* CAMELS-AUS v2.03, 125 SE-AU catchments with at least 30 calibration years and at
  least 5 years in 2010-2021. Model: Q = a + bP + cP(t-1) + dT, fitted on 1951-1996, separately
  with AGCD and SILO rain; deficit = mean 2010-2021 residual. Elevation gap = catchment mean
  elevation minus the weighted elevation of gauges active after 1997 within 60 km of the centroid.
- *Correction (H2).* We multiplied post-1996 catchment rain by exp(slope x gap/100 m) and
  recomputed the deficit with the unchanged 1951-1996 relation.

**Results.**

1. **The planned gauge slope was small.** From 1951-1996 to 1997-2021, gauges lost
   **-0.65% of rain per 100 m** of height above their neighbours (95% interval -1.42 to -0.03;
   470 gauges). By the planned rule, H1 is formally supported, but the effect is about
   one seventh of the -4.3% per 100 m that the median AGCD deficit needs (Figure 1b, c). Gauges
   more than 150 m above their neighbours changed by -0.5% on average (n = 33).
2. **The slope is not new after 1997.** The planned pre-1997 placebo (1975-1996 against
   1951-1974) gave the same slope: **-0.58% per 100 m (-1.05 to -0.22)**. Post hoc, the change
   from 1975-1996 to 1997-2021 was **-0.19% per 100 m (-0.53 to +0.20)**. Thus the higher
   gauges drifted slowly down relative to lower gauges through the whole record. There was no
   step at 1997, when the runoff deficit started.
3. **Other variants agree.** 30 km neighbours -1.03 (-1.71 to -0.44; 139 gauges); 100 km -0.51
   (-1.27 to +0.13); 1997-2009 -0.21 (-0.82 to +0.29); 2010-2021 -0.30 (-1.15 to +0.41); May-Oct
   rain -0.23 (-1.03 to +0.34); Nov-Apr rain -0.49 (-1.28 to +0.13); 5,160 gauge pairs with
   latitude and longitude controls -0.28 (-0.57 to +0.01). No variant comes near -4% per 100 m
   (`files/results/h1_variants.csv`).
4. **Runoff loss does not increase with catchment height above the gauges (H2b).** The
   2010-2021 AGCD deficit changed by -0.7 percentage points per 100 m of gap (95% interval -4.3 to
   +3.2; aridity, latitude and longitude controls; Spearman rho -0.05). Catchments more than
   200 m above their gauges lost 17.4% (median, n = 36). Catchments less than 50 m above them lost
   16.4% (n = 38). An elevation error cannot make a deficit in catchments that are level with
   their gauges. The result was the same with SILO rain, for 1997-2009, and with 30 km or
   100 km gauge radii (`files/results/h2b_sensitivity.csv`; Figure 2a).
5. **The correction removes a small share (H2).** With the planned slope, the rain correction
   removed **13% of the mean AGCD deficit** (interval 0.5% to 28%; -51 to -45 mm/yr), and 28%
   (1% to 62%) of the smaller SILO deficit (-20 to -14 mm/yr). With the 1997 step slope it removed
   4% (-4% to 10%) and 8% (-9% to 23%) (Figure 2b). Because the planned slope also existed before
   1997, the planned-slope shares are upper estimates.

**Conclusion.** Under the tested assumptions, a larger rain decline at elevation that the gauges
do not see is not the cause of the persistent post-1997 SE-AU runoff deficit. Higher gauges had
a slow relative rain decline over the whole record, but no new decline at 1997. The runoff deficit
is as large in catchments that are level with their gauges as in catchments far above them. At
most, this error explains about one quarter of the AGCD deficit, and probably less than one tenth.
Together with the fixed-gauge test (SCI 20955da2), this removes rain measurement as a general
explanation at the scale of the long-record gauge network. The cause of the deficit stays open;
the evidence continues to point to a change in the catchments, not in the rain data.

**What this does not show.** The highest GHCN-Daily gauge in the sample is 1,082 m. The alpine
zone above about 1,100 m, where Chubb et al. (2011) found the largest decline, is not sampled.
Few CAMELS-AUS catchments are in that zone, but a few high catchments could still have a rain
error. Relative elevation is a simple proxy for orographic exposure: we did not test slope
aspect or windward position. The gauges that AGCD used in each year are approximated by the
GHCN-Daily inventory. Our interpolation is inverse-distance weighting, not the AGCD or SILO method.
The catchment test uses mean elevation, not a rain-weighted hypsometry. The catchment sample is
125 basins in 32 one-degree cells, and the annual model is linear.

## Figures

![Gauge test](files/figures/fig1_gauge_elevation_test.png)

**Figure 1.** Gauge test. (a) Change of each gauge's rain relative to its interpolated neighbours,
1997-2021 against 1951-1996 (marker size: elevation). (b) The same change against the gauge's
height above its neighbours, with bin means, the fitted slope and the slope that the median AGCD
runoff deficit needs (dashed). (c) Slope and 95% cell-bootstrap interval for all variants; grey:
pre-1997 placebo and the change relative to 1975-1996.

![Catchment test](files/figures/fig2_catchment_test.png)

**Figure 2.** Catchment test. (a) 2010-2021 runoff residual (% of 1951-1996 mean flow) against
the catchment's mean height above nearby gauges, with bin medians, for AGCD and SILO rain.
(b) Share of the mean 2010-2021 deficit that the rain correction removes, with the planned slope
and with the slope relative to 1975-1996; bars show the point value, lines the values at the
slope interval ends.

## Table 1. Gauge-test slopes (% rain change per 100 m of relative elevation)

| Variant | Gauges (or pairs) | Slope | 95% interval |
| --- | --- | --- | --- |
| Primary: 60 km, 1997-2021 vs 1951-1996 | 470 | -0.65 | -1.42 to -0.03 |
| 30 km neighbours | 139 | -1.03 | -1.71 to -0.44 |
| 100 km neighbours | 567 | -0.51 | -1.27 to +0.13 |
| 1997-2009 only | 711 | -0.21 | -0.82 to +0.29 |
| 2010-2021 only | 246 | -0.30 | -1.15 to +0.41 |
| May-Oct rain | 704 | -0.23 | -1.03 to +0.34 |
| Nov-Apr rain | 758 | -0.49 | -1.28 to +0.13 |
| Gauge pairs, lat/lon controls | 5,160 pairs | -0.28 | -0.57 to +0.01 |
| Placebo: 1975-1996 vs 1951-1974 | 656 | -0.58 | -1.05 to -0.22 |
| Post hoc: 1997-2021 vs 1975-1996 | 535 | -0.19 | -0.53 to +0.20 |
| Needed to explain the median AGCD deficit | - | about -4.3 | - |

## Table 2. Catchment deficits (CAMELS-AUS, model fitted on 1951-1996)

| Rain | Era | Catchments | Median deficit (% of flow) | Mean deficit (mm/yr) | Share negative |
| --- | --- | --- | --- | --- | --- |
| AGCD | 1997-2009 | 124 | -11.8 | -31.5 | 0.80 |
| AGCD | 2010-2021 | 125 | -19.6 | -51.2 | 0.83 |
| SILO | 1997-2009 | 124 | -7.9 | -19.0 | 0.72 |
| SILO | 2010-2021 | 125 | -9.3 | -19.8 | 0.66 |

The rain error needed to remove each catchment's 2010-2021 deficit has a median of 6.9% of
post-1997 rain with AGCD (interquartile range 1.6-11.0%) and 3.5% with SILO
(`files/results/required_error.json`).

## Methods details

- **Gauge years.** A month is valid if no value has a quality flag and missing days are followed
  by a reported (accumulated) value in the same month, with at most 10 missing days. A year is
  valid if all 12 months are valid. 1,804 of 1,810 gauges had valid years (95,495 gauge-years).
- **Gauge test.** Anomaly ratio A = P / mean P(1951-1996) for each gauge. For a target gauge,
  the interpolated anomaly is the inverse-distance-squared mean of A over neighbours from 1 to
  60 km with a valid year (at least 3). Requirements: at least 60% valid years in each window
  (and the planned 30 calibration and 15 post-1997 years). Slope: OLS of Delta on relative
  elevation with an intercept, converted to percent per 100 m. Interval: 2,000 bootstrap draws of
  1-degree cells (seed 20261111). Placebo and step variants use the stated windows as baseline.
- **Pair test.** All gauge pairs 1-60 km apart with at least 20 common valid years in 1951-1996
  and 12 in 1997-2021; Delta of log(rain ratio) oriented from the lower to the higher gauge;
  OLS through the origin on elevation, latitude and longitude differences.
- **Catchments.** SE-AU = CAMELS-AUS catchments with centroid south of 31 S and east of 138 E
  (321). Annual flow uses years with at least 95% of daily values. Deficits in % use the
  1951-1996 mean flow. The catchment test uses 2010-2021 catchments with at least 5 years (many
  series end in 2014, 2020 or early 2022).
- **H2 correction.** Post-1996 rain (and the lagged rain term) multiplied by
  exp(log(1 + slope/100) x gap/100 m). The 1951-1996 coefficients are unchanged.

## Reproduction

1. `SCRATCH=/your/scratch DATASETS=/path/to/datasets bash files/code/retrieve_data.sh`
   (CAMELS-AUS from the shared store or Zenodo; GHCN-Daily from NCEI; about 1.3 GB).
2. `SCRATCH=... DATASETS=... RESULTS=/your/results bash files/code/run_all.sh`
   (about 10 minutes on 8 cores). Outputs: the JSON/CSV files in `files/results/` and the
   figures in `files/figures/`.
3. Software: Python 3.12.15, pandas 3.1.1, numpy 2.5.4, matplotlib 3.11.2, pyarrow 26.0.1.

GHCN-Daily files change over time; use `files/provenance/ghcnd_dly_sha256.txt` to check whether
a new download is identical to ours.

## Files

- `files/code/`: analysis scripts `01`-`09`, `ANALYSIS_PLAN.md`, `retrieve_data.sh`, `run_all.sh`.
- `files/results/`: `h1_summary.json`, `h1_variants.csv`, `h1_dz_bins.csv` (gauge test,
  aggregates); `h2b_summary.json`, `h2b_sensitivity.csv` (catchment gap test); `h2_summary.json`
  (correction shares); `required_error.json`, `required_error_bins.csv`;
  `catchment_deficit_summary.csv`.
- `files/figures/`: Figures 1 and 2.
- `files/provenance/`: hashes of external inputs.
- `files/DATA_NOTICE.md`: external data sources, licenses and attribution.

## Relation to earlier campaign work

This work tests the rain-measurement alternative left open by SCI ee211978 ("unmeasured climate
(orographic rain pattern)") and extends the fixed-gauge test of SCI 20955da2, which removed
network changes but not gauge representativeness. It agrees with SCI 1ace58a8 and 978a2bab,
which found that the loss acts on all parts of the catchments and mostly on event water, and
with SCI d8cf8c14, 646c1422 and 905bbb47, which weakened the groundwater-disconnection
explanation. The cause of the persistent deficit remains unexplained.
