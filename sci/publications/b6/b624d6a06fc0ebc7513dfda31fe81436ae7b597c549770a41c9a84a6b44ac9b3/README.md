# Bird species followed land-cover change at only 11-25% of their spatial land-cover associations, about twice their temperature transfer; land-cover change did not slow community warming (US BBS, 1985-2021)

## Summary

Earlier campaign work showed that North American bird communities and species follow only a small part
of their spatial temperature associations in time. The open question was which ecological process sets
the remaining gap. We used annual land cover from outside the Breeding Bird Survey (BBS), USGS LCMAP
v1.3 (1985-2021), in 400 m buffers of 3,229 BBS route paths. We asked two questions:

1. **Positive control.** Do the same species follow route land-cover change at the rate that their
   spatial land-cover associations predict? Land cover is a direct habitat driver with a well-measured
   change. If species follow it fully, the survey and the method can detect fast composition change,
   and the weak climate response is specific to climate.
2. **Attribution.** Did land-cover change along the routes hold the community temperature index (CTI)
   back, and does it explain the gap between the observed CTI trend and the spatial climate expectation?

Main results:

- **Species followed land cover weakly, too.** For 384 species, the temporal response to land-cover
  change was 0.106 (95% CI 0.064-0.148) of the spatial prediction. The temporal response to May-July
  temperature in the same models was 0.050 (0.040-0.060). Both were far below full transfer (1).
- **Correction for errors in the spatial coefficients** (split-fold reliability, about 0.56 for both
  predictors) gave 0.19 (0.11-0.27) for land cover and 0.090 (0.067-0.115) for temperature. With route
  effects only (comparisons across observer changes), the corrected values were 0.25 (0.17-0.33) and
  0.12 (0.09-0.15). Temperature transfer was 0.47 (0.29-0.83) of land-cover transfer.
- **The land-cover response is real and partly slow.** Land cover 5 years before the survey gave 0.099
  (0.060-0.139). Land cover 5 years after the survey (placebo) gave 0.033 (-0.004 to 0.071), and 0.009
  (-0.029 to 0.047) when lag, same-year and lead terms were fitted together.
- **Land-cover change did not hold the CTI back.** Land-cover change along the routes was small (median
  route change 2.1 percentage points; 22% of routes changed by 5 points or more). It implied a CTI change
  of +0.0020 C per decade (0.0007-0.0036). The gap between the spatial climate expectation (0.096 C per
  decade) and the observed within-observer CTI trend (0.034) was 0.063 C per decade. Land-cover change
  thus increased the gap by 3% (95% CI 1-6%); it did not explain it. Two other methods gave +0.0006 and
  +0.0010 C per decade.
- **Landscape context did not change the CTI trend.** Natural-cover share, land-cover diversity and the
  amount of land-cover change did not change the CTI trend relative to the Bird Conservation Region
  (all |effects| < 0.002 C per decade per SD, SE about 0.003). We did not find the French result of
  Gauzere et al. (2017) in US routes.

Interpretation: a large part of the weak climate tracking relative to spatial benchmarks is a general
property of space-for-time transfer in BBS abundance, because it also occurs for a direct habitat
driver. The climate-specific part is about a factor of two (0.47). Land-cover change is not the missing
ecological process for the CTI gap.

## Data

| Source | Version and use | License |
| --- | --- | --- |
| North American Breeding Bird Survey | 2026 release (1966-2025), ScienceBase item 6a0b0b0ab66b0188da36aedd; States.zip counts, Weather.csv runs, Routes.csv, SpeciesList.csv | USGS, public domain |
| BBS route paths | National Atlas `bbsrtsl020` route lines (routes to 1998), Stanford EarthWorks vy474dv5024 | USGS National Atlas, public domain |
| USGS LCMAP CONUS Collection 1.3 | Primary land cover (LCPRI), 1985-2021, Microsoft Planetary Computer collection `usgs-lcmap-conus-v13` | USGS, public domain |
| NOAA nClimGrid monthly | tavg and prcp, 1/24 degree, NCEI access files of 2026-10-06 | NOAA, public domain |

Exact shared-dataset paths, source URLs and verified SHA-256 hashes are in
`files/provenance/inputs.json`. The 5,291 LCMAP file URLs that we read are in
`files/provenance/lcmap_v13_lcpri_urls.csv.gz`. See `files/NOTICE-external-data.md`.

## Methods

**Runs and species.** Standard BBS runs (RunType 1) on contiguous-US routes with a National Atlas path,
1985-2021: 69,243 runs on 2,986 routes. 429 species on 30 or more routes (named forms merged;
unidentified taxa and hybrids removed; 88 in aquatic orders).

**Climate.** nClimGrid May-July mean temperature and total precipitation at 9 points along each path,
averaged. For the panels we used 5-year running means (years t-4 to t).

**Land cover.** For each route, the path was buffered by 400 m in the LCMAP Albers projection and
rasterized onto the LCMAP 150 km ARD tiles. Because the host network was slow (about 100 KB/s per
stream), we read the COG overviews with nearest sampling: factor 4 (120 m) for the first 172 tiles and
factor 8 (240 m) for the other 235. A check on one 61 km x 61 km window showed factor-4 class counts within 1% (the four largest classes within 0.4%) of the
30 m counts divided by 16. For all routes we used the 13 years 1985, 1988, ..., 2021 and interpolated
fractions linearly between them. Counts from tiles at different factors were put on one area scale.
Classes: developed, cropland, grass/shrub, tree cover, water, wetland, and other (barren, snow/ice).
3,229 routes; median 2,240 valid 120 m pixel-equivalents per route.

**Species temperature index (STI) and CTI.** We assigned 4-degree blocks at random to two folds. The
STI of each species for routes in one fold is the abundance-weighted mean 1985-2021 May-July
temperature of the routes in the other fold. Run CTI = sum(log(1+n) STI) / sum(log(1+n)).

**Primary analysis: space-for-time transfer per species.** For each species with 50 or more occupied
routes we used the routes within 250 km of an occupied route (median 1,283 routes). A spatial Poisson
model (L2 penalty 1e-4 on standardized terms) related route totals (offset: number of runs) to cubic
splines of the temperature normal and the log precipitation normal and to six land-cover fractions
(tree cover as reference). Coefficients fitted in one fold gave predictions for routes in the other
fold (cross-fitting). For each run we calculated three predicted log-abundance terms:
x_LC from that year's land cover, x_T and x_P from the 5-year climate means. A conditional Poisson
model of the run counts on x_LC, x_T and x_P with route x observer and year fixed effects and
route-clustered errors gave theta_LC, theta_T and theta_P. Theta = 1 means that the temporal response
equals the spatial prediction. We pooled species with DerSimonian-Laird random effects (384 species
with converged fits). The estimator (`files/code/pfe.py`) agreed with a statsmodels Poisson model with
dummy variables to 1e-8 on a simulated test.

**Reliability correction (added after the main estimate).** Errors in the spatial coefficients
attenuate theta. The coefficients from the two folds have independent errors. For each species, the
covariance between the within-group changes predicted by the two folds, divided by the variance of the
cross-fitted change, estimates the attenuation factor. Corrected theta = sum(w theta) / sum(w
reliability), with random-effects weights w; 95% intervals come from 4,000 species bootstrap draws.
This assumes classical errors and a near-linear response.

**Other added checks (after the main estimate).** Route effects only; land cover 5 years before and 5
years after the survey (survey years 1990-2016); land-cover class components of x_LC; 5-year smoothed
land cover; routes with 5 or more percentage points of total change.

**CTI attribution.** (a) Spatial OLS of route-mean CTI on the temperature normal, log precipitation
normal and land-cover fractions; the land-cover-implied CTI trend is sum(c_k x trend of fraction k).
The climate expectation is the spatial CTI-temperature slope (0.428 C per C; 0.416 with land-cover
controls) times the within-route warming trend (0.225 C per decade). Observed CTI trend: linear trend
with route x observer effects. 200 draws of a 4-degree block bootstrap. (b) Within-route CTI model on
land-cover fractions and 5-year climate with route x observer and year effects. (c) CTI of
species-model predictions with only land cover or only climate changing. (d) CTI trend x standardized
route natural-cover share, land-cover diversity and land-cover change, with route x observer and Bird
Conservation Region x year effects.

## Results

### Land-cover change along the routes (Figure 4)

Mean net change 1985 to 2021: developed +0.21, cropland -0.25, grass/shrub +0.67, tree cover -0.69
percentage points; wetland and water near 0. Median absolute route change was 0.4 to 1.1 points per class.
Median within-group SD of x_LC was 0.055 log units (0.093 on routes with 5 or more points of change),
against 0.43 for x_T. The spatial SDs were 1.23 (land cover) and 2.64 (temperature).

### Space-for-time transfer (Figures 1 and 2; `files/results/tables/theta_pooled.csv`)

| Variant | theta land cover (95% CI) | theta temperature (95% CI) |
| --- | --- | --- |
| Main model (384 species) | 0.106 (0.064-0.148) | 0.050 (0.040-0.060) |
| Each predictor alone | 0.106 (0.064-0.148) | 0.050 (0.040-0.060) |
| Landbirds (313) | 0.096 (0.049-0.143) | 0.048 (0.037-0.059) |
| Aquatic orders (71) | 0.151 (0.057-0.245) | 0.068 (0.040-0.097) |
| Route effects only | 0.139 (0.097-0.181) | 0.063 (0.050-0.076) |
| 5-year smoothed land cover | 0.117 (0.070-0.164) | |
| Routes with >= 5 points change | 0.077 (0.027-0.126) | |
| Routes with < 5 points change | 0.126 (0.071-0.181) | |
| Survey years 1990-2016, same year | 0.105 (0.059-0.151) | |
| Land cover 5 years before survey | 0.099 (0.060-0.139) | |
| Land cover 5 years after survey (placebo) | 0.033 (-0.004 to 0.071) | |
| Reliability-corrected, route x observer | 0.19 (0.11-0.27) | 0.090 (0.067-0.115) |
| Reliability-corrected, route only | 0.25 (0.17-0.33) | 0.12 (0.09-0.15) |

The within-species difference theta_LC - theta_T was 0.060 (0.012-0.107). The corrected ratio
theta_T / theta_LC was 0.47 (0.29-0.83), and 0.47 (0.31-0.75) with route effects only. Median
reliability was 0.63 for both predictors. Precipitation transfer was 0.011 (0.006-0.016). The temperature
value repeats the campaign result of 0.053 in sci:sha256:c86bb599 with a different design.

In a joint model, land cover 5 years before (0.091, 0.051-0.132) and in the survey year (0.093,
0.048-0.137) both contributed, and land cover 5 years after did not (0.009). Thus part of the response
comes with a delay; the sum of the lag and same-year terms (about 0.18 raw, about 0.33 after the
reliability factor) is still far below 1.

Class components of x_LC (raw, not corrected): wetland 1.37 (0.78-1.95), cropland 0.19 (0.06-0.33),
water 0.18 (0.05-0.30), developed 0.17 (-0.03 to 0.37), grass/shrub 0.10 (0.03-0.18), other -0.03.
Only wetland change was followed at the spatial rate; it is rare and changes little on routes.

Routes with large land-cover change gave a lower theta, not a higher one. Random year-to-year
classification noise is therefore not the main cause of the low land-cover transfer.

### CTI attribution (Figure 3; `files/results/cti_attribution.json`)

| Quantity (C per decade, 1985-2021) | All routes | East (lon > -100) | West |
| --- | --- | --- | --- |
| Observed within-observer CTI trend | 0.034 (0.024-0.042) | 0.025 (0.017-0.033) | 0.054 (0.040-0.070) |
| Spatial climate expectation | 0.096 (0.083-0.110) | 0.078 (0.065-0.091) | 0.130 (0.108-0.152) |
| Land-cover-implied, spatial model | +0.0020 (0.0007-0.0036) | -0.0009 (-0.0020 to 0.0004) | +0.0067 (0.0034-0.0119) |
| Land-cover share of the gap | -3.1% (-5.8 to -1.1%) | +1.7% (-0.8 to 3.6%) | -8.9% (-16 to -4%) |

Within-route model: +0.0006 C per decade (SE 0.0003). Species-model predictions: land cover only
+0.0010 (SE 0.0003); climate only +0.076 (SE 0.0013). Negative shares mean that land-cover change
increased the CTI and so increased the gap. In the West, the gain of grass/shrub and the loss of tree
cover and cropland favoured warm open-country species.

The observed CTI trend here is the within-observer trend without year effects. Campaign results
sci:sha256:b113aa1b and sci:sha256:b9959b67 show that observer hearing drift inflates this trend;
we use it only as the common reference for the attribution, not as a new tracking estimate.

Landscape modifiers (C per decade per SD, with BCR x year effects): natural cover -0.00002 (SE 0.0030),
diversity -0.0003 (0.0031), land-cover change +0.0019 (0.0025).

## Limitations

- LCMAP has 8 broad classes. It does not show forest age, crop type, grazing, agricultural intensity
  or fine structure. Changes inside a class, which may drive farmland and grassland bird declines, are
  not in x_LC. Our land-cover result applies to class changes only.
- The route paths are from the National Atlas (to 1998). Later route changes and the 400 m buffer
  (birds are detected beyond 400 m) add error to route land cover. This error is in both x_LC and the
  spatial model; the reliability correction does not remove it.
- We read 120 m and 240 m overviews and 13 of 37 years, with linear interpolation. This removes
  short-lived changes.
- The reliability correction assumes classical, independent errors in the two folds and a near-linear
  Poisson response. Species-level reliabilities are noisy (some are negative); we pooled them as ratios
  of weighted sums.
- Spatial land-cover associations can include non-causal parts (soil, region, management). A low
  theta can mean that these parts do not transfer in time, which is part of what we measure, not only
  slow responses.
- Responses that take more than about 5-10 years are only partly in the estimates. The lag test shows
  that delays exist.
- The supplementary checks (reliability correction, route-only effects, lags, class components) were
  added after the main estimate was known. The main model and the CTI attribution followed the plan in
  `files/plan/analysis_plan.md`. The planned long-difference check was replaced by the route-effects and
  lag checks. The change of LCMAP sampling (overview factor, 13 years) was made for download speed
  before any outcome was calculated.
- Contiguous US only; Canadian and Alaskan routes have no LCMAP data.

## Files

- `files/code/`: all code (`run_all.sh` runs the pipeline; `pfe.py` has the estimators).
- `files/plan/analysis_plan.md`: plan written before the land-cover outcomes.
- `files/results/tables/species_theta.csv`: per-species estimates, SEs, reliabilities and variants.
- `files/results/tables/theta_pooled.csv`, `species_pooled_extra.json`: pooled estimates.
- `files/results/cti_attribution.json`, `boot_*.csv`: CTI attribution and bootstrap draws.
- `files/data/route_landcover_lcmap_1985_2021.csv.gz`: route x year LCMAP fractions (derived; lets users
  skip the 1.5 h download). `run_cti_1985_2021.csv.gz`: run CTI and climate. `species_sti.csv`:
  species list and STI. `predicted_cti_route_year.csv.gz`: CTI of species-model predictions.
- `files/figures/`: four PNG figures.
- `files/provenance/`: input hashes, LCMAP URLs, software versions.

## Reproduction

```
bash files/code/run_all.sh /path/to/shared_datasets /path/to/scratch /path/to/output
```

Python 3.12 with numpy, pandas, scipy, scikit-learn, geopandas, rasterio (GDAL 3.12), shapely,
netCDF4 and matplotlib (versions in `files/provenance/software_versions.txt`). Set OMP_NUM_THREADS=1.
LCMAP files are read from the Microsoft Planetary Computer with an anonymous SAS token
(`https://planetarycomputer.microsoft.com/api/sas/v1/token/usgs-lcmap-conus-v13`); the script forces
IPv4. Bootstrap and fold seeds are fixed in the code. Runtime on the campaign host: about 1.5 h for
LCMAP, 10 min for species models, 30 min for the CTI bootstrap.

## Provenance

Job sci-1107-dell-climate-pollution-biodiversity-fceca40172ae, campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell, model Claude Opus 5.5 (claude-opus-5-5). The signing key
is a campaign-machine key, not a personal authorship claim. Work date 2026-11-10.
