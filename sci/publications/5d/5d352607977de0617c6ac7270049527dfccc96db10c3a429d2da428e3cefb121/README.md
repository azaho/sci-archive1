# Runoff loss after 1997 did not jump at the Victoria - New South Wales border; the 1997 step followed the winter-rain share, not the state line (CAMELS-AUS, 1951-2021)

Job: sci-1107-dell-earth-and-ocean-sciences-5c628e4008a2. Topic: earth and ocean sciences. Machine: dell (campaign 11_07_2026).
Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.

## 1. Question

After 1997, runoff in south-east Australia fell 12-25% below each catchment's 1951-1996 rainfall-runoff relation and
stayed low. Campaign work found that the timing is different in the two states: Victorian runoff efficiency fell in a
1997-1998 step, but New South Wales (NSW) runoff efficiency fell gradually from the 1950s (sci:sha256:e3ac7e44).
A later test could not resolve this difference with fixed rain models (sci:sha256:2f6a785d).

A state difference has two possible causes:

1. **Institutions.** Victoria and NSW use different gauging agencies, rating practice, water licensing (for example
   farm dams), and land and forest management. Victorian stream gauging was privatised in 1994. A cause of this type
   changes at the state line.
2. **Geography.** Climate, rain season, terrain and drought depth change gradually across the border. A cause of
   this type does not change at the state line.

We used the state border as a natural experiment. Rain and drought are continuous across the border, but
institutions are not. **Is the post-1997 runoff deficit, or its timing, discontinuous at the border?**

## 2. Data and method

- **Data.** CAMELS-AUS v2.03 (Zenodo 14289037): daily streamflow (mm/d) and catchment-mean daily rain from AGCD and
  SILO, catchment centroids, and the state boundary shapefile in the CAMELS-AUS bonus data. Calendar years. A year is
  complete when 95% or more of its days have flow (small gaps are scaled to a full year).
- **Catchments.** We used Victorian and NSW/ACT catchments with 25 or more complete years in 1951-1996: 166 for the
  departure windows and 161 for the timing statistics. For the east-wide check we added Queensland and South
  Australia (221 catchments). Distance is the distance from the catchment centroid to the Victoria - NSW/ACT land
  border (EPSG:3577). Within 150 km of the border there are 51-54 Victorian and 21-22 NSW catchments.
- **Rain-runoff model.** For each catchment, Q = a + bP + cP(t-1), fitted by ordinary least squares on 1951-1996.
  The departure for a window is the mean of (observed - predicted) as a percentage of the mean calibration flow.
  Pre-1997 windows (placebos) use a fit on the other pre-1997 years. Variants: sqrt(Q), a P^2 term, and SILO rain.
- **Timing statistics** (per catchment):
  - *trend*: coefficient d in Q = a + bP + cP(t-1) + d(year-1974)/10, fitted on 1951-1996 (% of mean flow per decade);
  - *step*: mean departure in 1997-2019 minus mean departure in 1985-1996 (percentage points).
- **Border estimators.**
  - Planned primary estimator: local-linear regression of the departure on signed distance, with a separate slope on
    each side, a triangular kernel (bandwidth 150 km) and a longitude control. The output is the jump J = Victoria
    minus NSW at the border.
  - More stable estimator: band means (Victoria minus NSW) within 75 km and within 150 km.
  - Uncertainty: 2,000 bootstrap draws that resample 1-degree cells within each side.
- **Plan.** The plan (`files/PLAN.md`) was written before any departure was calculated. It defines the primary test
  (AGCD, 2010-2019, bandwidth 150 km) and its decision rule. The near/far timing contrast, the rain-season analysis,
  the east-wide regressions and the NSW-Queensland border check are post hoc (exploratory).

## 3. Results

### 3.1 The planned primary test is unresolved, and its point estimate is opposite to a Victorian border effect

| Window (AGCD, linear) | Border jump J, VIC - NSW (95% interval) | VIC / NSW band mean | n VIC / NSW |
| --- | --- | --- | --- |
| 2010-2019 (primary) | +11.1 (-24.1 to +29.2) | -21.4 / -25.9 | 51 / 22 |
| 1997-2009 | +30.2 (+12.1 to +44.6) | -6.9 / -15.3 | 54 / 21 |
| 1983-1996 (placebo) | +35.5 (-10.3 to +43.3) | -5.3 / -17.6 | 27 / 9 |
| Rain anomaly 1997-2009 | -1.7 (-8.6 to +11.2) | -18.3 / -18.8 | 54 / 22 |

Units are % of the mean calibration flow; for the rain anomaly they are % of 1951-1996 rain.

- The decision rule needed a 95% interval that excludes -10.7 (half the Victorian deficit) for the result "smooth".
  The interval includes it, so by the plan the primary result is **unresolved**.
- The point estimate is positive. Thus near the border, Victorian catchments lost slightly *less* runoff than NSW
  catchments, not more.
- The local-linear jump is imprecise because only one NSW catchment with a long record lies within 50 km of the border.
  The NSW intercept is therefore an extrapolation. Same-slope fits give J = -2.8 (-20.6 to +15.1) for 2010-2019.
- **Band means are more stable** (Figure 2, `results/band_means.json`):

| Within 150 km, VIC - NSW (95% interval) | AGCD | SILO |
| --- | --- | --- |
| Departure 2010-2019 | +4.5 (-7.9 to +16.9) | -1.9 (-14.3 to +11.6) |
| Departure 1997-2009 | +8.4 (+0.9 to +18.1) | +2.7 (-4.9 to +13.9) |
| Departure 1983-1996 | +12.3 (+3.1 to +36.0) | +13.4 (+2.1 to +27.6) |
| Rain anomaly 1997-2009 | +0.5 (-1.5 to +2.3) | +1.7 (-1.3 to +4.6) |

Units are percentage points.

- Within 75 km (AGCD; n = 23-26 VIC and 8 NSW), the 2010-2019 departures were -23.0% (VIC) and -30.4% (NSW).
- **No result shows a larger Victorian loss at the border.** Drought depth was the same on both sides: the AGCD rain
  anomaly in 1997-2009 was -18% on both sides.

### 3.2 The Victoria-step / NSW-gradual contrast disappears at the border

| Step, VIC - NSW (95% interval) | AGCD linear | AGCD with P^2 | SILO linear |
| --- | --- | --- | --- |
| Within 150 km | +0.6 (-7.7 to +10.5) | -2.2 (-8.2 to +5.8) | -5.4 (-13.7 to +13.3) |
| More than 150 km | -11.9 (-18.9 to -5.7) | -10.5 (-16.9 to -4.6) | -12.2 (-18.7 to -6.2) |

- Far from the border, the earlier finding repeats: Victorian catchments stepped down after 1997 and NSW catchments
  did not.
- Within 150 km of the border, NSW catchments stepped down as much as Victorian catchments (AGCD: -9.3 against -8.7
  points).
- The near-minus-far difference-in-differences of the step contrast was +12.5 (+1.7 to +24.0) with AGCD and +6.8
  (-3.6 to +24.7) with SILO.
- Near the border, the NSW catchments also had the lower pre-1997 trend (-7.5 against -1.7% per decade; difference
  +5.8, -0.2 to +11.3). They were already low in 1983-1996 (Section 3.1). Figure 4 shows the annual paths: near the
  border, NSW was below Victoria in about 1990-2009, and the two states were equal after 2010.

### 3.3 The 1997 step follows the winter-rain share in both states (exploratory)

Figures 1 and 3 and `results/east_*.json`, `results/within_*.json`.

**Step against the May-October share of 1951-1996 rain.** Across 221 eastern catchments (VIC, NSW/ACT, QLD, SA), the
step changed steadily with the rain season:

| May-October rain share | Below 0.3 | 0.3-0.4 | 0.6-0.65 | Above 0.65 |
| --- | --- | --- | --- | --- |
| Mean step, AGCD (points) | +6.5 | +5.3 | -11.7 | -16.6 |

- The slope was -4.7 points per 0.1 share (-6.8 to -2.5). SILO and the P^2 model gave the same pattern.
- With the season share in the model, the state indicators were no longer different from zero (VIC -2.6, -19.6 to
  +11.4).
- Within Victoria alone, the step fell by -10.3 points per 0.1 share (-19.4 to +0.3; SILO -12.8, -20.5 to -3.8).
  Within NSW, the slope was -2.2 (-8.3 to +1.8).
- East-wide, the season share and latitude are strongly correlated, so they cannot be separated (Section 4).

**Drought depth did not set the step.**

- Within Victoria, the 1997-2009 rain anomaly had no relation to the step: -0.8 points per 10 points of rain anomaly
  (-9.4 to +9.4).
- East-wide, the rain anomaly alone gave +4.6 (+0.1 to +9.8), but -2.0 (-6.4 to +2.2) with the season share, latitude,
  mean rain and runoff ratio in the model.
- The cool-season rain anomaly also did not predict the step.

**The pre-1997 decline is in mixed-regime catchments.**

- The trend was most negative at a May-October share of 0.4-0.5 (-14% per decade; mostly central and northern NSW).
- It was near zero in summer-rain Queensland catchments (+4.4) and in winter-rain Victorian catchments (about 0).
- At equal season share, NSW catchments declined more than Queensland catchments (state term -16.9% per decade,
  -24.1 to -9.7).
- A NSW-Queensland border check had only 8 NSW and 17 Queensland catchments within 200 km. The jump in the trend was
  -2.4 (-13.4 to +22.3), so this check gives no information.

### 3.4 Rain products

- The SILO/AGCD rain ratio fell by about 2-4% after 1997 everywhere. Within 75 km, the fall was 4.5 points (2.2 to
  6.2) larger on the NSW side than on the Victorian side.
- With separate slopes, SILO rain showed a border jump in its rain anomaly (+9.5, +2.5 to +17.6), but AGCD did not.
  The band means differed by only 1.5-1.7 points.
- We conclude that the separate-slope estimator is fragile with so few NSW catchments near the line. We do not claim
  a SILO border artefact.

## 4. Interpretation

- **Institutions.** Victoria and NSW have different gauging agencies, gauging history (Victorian gauging was
  privatised in 1994) and water and land policy. These differences did not produce a larger Victorian loss at the
  border. NSW catchments next to the border stepped down after 1997 by the same amount.
- **Geography.** The state contrast in the 1997 step is a geographic gradient. Its size follows the winter-rain share
  across eastern Australia and inside Victoria. It does not follow the local depth of the 1997-2009 drought. Thus the
  step is a property of winter-rain catchments, where runoff comes after the soil and groundwater stores wet up
  each winter. This agrees with mechanisms that act through seasonal storage and stream connection. It does not
  agree with a simple dose response to the rain deficit.
- **The pre-1997 decline.** This is a different signal. It is centred on mixed-regime NSW catchments and is
  absent in Queensland at equal rain season. Next to the Victorian border, it is already visible on the NSW side in
  1983-1996. This part of the state contrast is not explained by rain season. The data cannot separate a
  NSW-specific (institutional) cause from a local geographic one, because the NSW sample near both borders is small.
- **Consequence for the open question.** The two timings are not one process seen through two state data systems.
  The 1997 step is regional and is tied to the winter-rain regime. The slow decline is older, centred on NSW, and its
  cause remains open.

## 5. Limitations

- The planned primary test is unresolved. Only 21-22 NSW catchments with long records lie within 150 km of the
  border, and only one lies within 50 km. Local-linear intercepts are extrapolations.
- The near/far, rain-season, east-wide and NSW-Queensland analyses are post hoc. Treat them as exploratory.
- Season share, latitude and state are correlated. The within-Victoria slope is the cleanest evidence for the season
  gradient, and its AGCD interval just touches zero.
- We used one linear annual model family (with sqrt and P^2 checks), calendar years, and 2-degree-scale spatial
  dependence through 1-degree cell bootstraps. The bootstrap does not include shared year-to-year errors.
- Victorian records from the Saft data set end in February 2020, so the common late window ends in 2019.
- We did not test gauging records, rating curves, farm-dam data or land use directly. "Institutional" covers all
  state-level factors together.

## 6. Files and reproduction

- `files/PLAN.md`: pre-analysis plan.
- `files/code/`:
  - `get_data.sh` downloads and checks the inputs into scratch;
  - `run_all.sh` runs the full pipeline;
  - `00_geometry.py` and `00b_geometry_qld.py`: border distances;
  - `01_annual_tables.py`: annual totals;
  - `02_departures.py`: window departures;
  - `03_border_rd.py`: local-linear border jumps;
  - `04_timing.py`: trend and step;
  - `05_season.py`: rain-season shares;
  - `06_gradient.py`, `07_within_state.py`, `08_east_regression.py`: covariates;
  - `09_figures.py`: figures;
  - `10_band_means.py`: band means.
- `files/results/`: per-catchment departures, trends, steps, season shares and border distances, and all bootstrap
  summaries (JSON). These are our derived statistics; no raw series are included.
- `files/figures/`: Figures 1-4 (PNG).
- `files/NOTICE-external-data.md`: sources, licences, attribution and input SHA-256.

To reproduce, run these two commands from `files/code` (the second takes about 40 minutes on 1 CPU):

```
bash get_data.sh /path/to/scratch
bash run_all.sh /path/to/scratch
```

Software: Python 3.12, numpy, pandas, geopandas, shapely and matplotlib. Random seeds are fixed in the scripts.
