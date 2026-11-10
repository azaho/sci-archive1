# Bird abundance gradients between nearby US survey routes kept 69% of the regional temperature gradient per degree with 5 km route-path climate; year-to-year tracking stayed at about 3% (1966-2025)

Job `sci-1107-hp-climate-pollution-biodiversity-84f3f73657bc` · topic climate-pollution-biodiversity ·
machine hp · model claude-opus-5-5 (Anthropic) · campaign 11_07_2026. The signing key is a campaign-machine
key. It is not a personal authorship claim.

## 1. Question

Prior campaign work found that bird communities and species follow only a small part of warming
(community temperature index (CTI) tracking ratio 0.06, sci:sha256:c0a3a9aa; species year-to-year
responses 5-14% of their spatial gradients, sci:sha256:91f371b5; 12% of the spatial CTI gradient in 75
networks, sci:sha256:0037934e). All these ratios divide by a spatial gradient that was measured across
the continent with 0.5-degree GHCN_CAMS temperature at the route start point. A related bundle
(sci:sha256:0bc2a582) found lower CTI slopes inside ecological regions (0.20-0.31) than across them.

Thus one candidate explanation of the deficit is the denominator: a continental gradient can contain
non-thermal biogeography (species pools, history, photoperiod), and only the thermal part can respond to
warming in place. We tested this directly:

1. Is the spatial abundance-temperature gradient the same per degree at the regional scale and at the
   local scale, between nearby routes that differ in temperature mainly because of elevation and coast?
2. How much do coarse climate data change the gradient and the year-to-year ratio?
3. Which tracking ratio remains when the denominator is the local gradient?

We wrote the plan (`files/PLAN.md`) before we calculated outcomes. Analyses that were not in the plan
are marked "exploratory".

## 2. Data

* North American Breeding Bird Survey (BBS), 2026 release, 1966-2025: standard runs (RPID 101,
  RunType 1) on contiguous-US routes. 107,900 runs on 3,949 routes with valid climate. Species filters
  are the same as in sci:sha256:91f371b5 (no unidentified forms or hybrids; no waterbirds (AOU code
  below 2850), owls or nightjars). 314 species had at least 30 routes with 3 or more detection runs.
* nClimGrid monthly mean temperature and precipitation (NOAA NCEI, 1/24 degree, about 4.6 km), file
  versions of 2026-10-06.
* BBS route paths: National Atlas route lines (1966-1998), Stanford Digital Repository vy474dv5024.
  2,946 of 3,949 routes (75%) had a path that started within 3 km of the official start point and had a
  length of 25-60 km. For the other routes we used the start point.
* GHCN_CAMS 0.5-degree monthly temperature (NOAA PSL), for comparison with the prior denominator.

Exact files, sizes, URLs and SHA-256 hashes: `files/input_hashes.txt`. Terms: `files/EXTERNAL_DATA_NOTICE.md`.

## 3. Methods

**Route climate.** May-July mean temperature, climatology 1971-2000 (the prior work used the same
period). The route value is the mean of nClimGrid cells sampled every 1 km along the route path. The
regional part T_reg is the same mean of a Gaussian-smoothed nClimGrid field (sigma 75 km; 40 and 150 km
as variants; NaN-aware smoothing). The local part is T_loc = T - T_reg. We did the same for the
logarithm of May-July precipitation (P_reg, P_loc). At sigma 75 km, T_loc has 8.9% of the spatial
variance of T (4.9% at 40 km, 14.8% at 150 km). Its SD is 0.46 C in the East and 1.98 C in the West.

**Species scale test (main).** For each species, inside its range envelope (Bird Conservation Regions
with detections on at least 5% of routes), y_r is the route mean of log(1 + count) over all runs. A
cubic regression spline (df 4) s(T) gives the niche curve f. We fit

  y = s(T) + gamma * T_loc.

Between nearby routes the slope is f'(T) + gamma; across regions it is f'(T). If abundance responds to
temperature in the same way at both scales, gamma = 0. The ratio kappa = 1 + gamma / f'_w compares the
local slope with the regional slope per degree, where f'_w is f'(T) averaged with the route weights that
the gamma estimate uses. This Mundlak-type form is robust to niche curvature. A simpler "s(T_reg) +
linear T_loc" form, which the plan named first, failed a positive control in a 12-species pilot because of
niche curvature. The plan's second form (s(T_reg) + kappa * s'(T_reg) * T_loc) has the same reference problem. We changed the
main model to the form above after that pilot and before any full-sample outcome; the plan form is kept as a description (`split_loc_on_reg` in the pooled table: 0.39, 0.24-0.50). Variants: precipitation control (+ s(P_reg) + P_loc); 1-degree cell fixed effects (y on T
within cells, compared with f' weighted by the within-cell variation of T); sigma 40 and 150 km; routes
with paths only; start-point climate; spline df 6.

**Controls.** Positive control: the cell estimator applied to the fitted smooth niche (kappa = 1 is
expected). Placebo: T_loc permuted among routes of the same 2-degree block (kappa near 0 is expected).

**Pooling and uncertainty.** We pooled species with a regression of the local slope on the regional
slope through the origin, with weights 1/var(gamma) (floored at the 5th percentile of the variances),
and we removed the noise bias of the denominator with the bootstrap (co)variances. Uncertainty comes
from a joint 2-degree spatial block bootstrap: each draw resamples the same blocks for all species
(200 draws for the main fit, 100 for variants). Intervals are percentile 95% intervals.

**CTI scale test.** Species temperature index (STI) = count-weighted mean route climate, cross-fitted
on a 2-degree checkerboard (routes in one half use STIs from the other half). Route CTI = count-weighted
mean STI. We regressed CTI on T, on T_reg and T_loc, on s(T) + gamma T_loc, and on T within 1-degree
cells, with nClimGrid and with GHCN_CAMS climate (500 block-bootstrap draws).

**Temporal ratio (secondary).** For each species, log(1 + count) per run with route x observer and
year fixed effects, a first-year-observer term, and May-July temperature anomalies of the same and the
previous summer (11-year centred running mean removed). Each anomaly term interacts with the route
gradient g_r from the species spline. The interaction coefficient theta is the within-species
space-for-time ratio lambda (1 = full equivalence). A 2 x 2 design used the gradient from GHCN_CAMS or
nClimGrid and the anomaly from GHCN_CAMS or nClimGrid. Species values were pooled with inverse-variance
weights (route-clustered SEs).

**CTI trend.** Run-level CTI on year with route x observer fixed effects (and route fixed effects only),
and nClimGrid route-path May-July temperature on year with route fixed effects, on the same 107,273
run-years (3,706 routes with 5 or more runs; 300 block-bootstrap draws).

## 4. Results

### 4.1 Coarse climate mismeasures route climate and attenuates local gradients

GHCN_CAMS start-point climatology correlated 0.94 with the nClimGrid route-path climatology, but the
two differed by an SD of 1.69 C between routes. Year-to-year anomalies agreed well (r = 0.967).
With nClimGrid, species gradients were 1.19 times steeper per degree than with GHCN_CAMS (pooled ratio,
95% CI 1.13-1.24; West 1.38, East 1.14). Within 1-degree cells, the CTI slope was 0.40 C per C (95% CI
0.36-0.43) with nClimGrid and 0.23 (0.19-0.27) with GHCN_CAMS. The GHCN_CAMS within-cell value is in the range that earlier work found inside ecological regions
(0.20-0.31), so those lower within-region slopes can be largely a measurement-error effect of the
0.5-degree climate. We did not refit the ecoregion model itself.

### 4.2 The CTI gradient is almost the same between nearby routes (Figure 1)

| CTI slope (C per C), all routes | estimate | 95% CI |
| --- | --- | --- |
| continental, GHCN_CAMS (prior-type denominator) | 0.41 | 0.39-0.43 |
| continental, nClimGrid route path | 0.43 | 0.41-0.45 |
| regional part T_reg (75 km) | 0.44 | 0.42-0.46 |
| local part T_loc (75 km) | 0.37 | 0.30-0.43 |
| within 1-degree cells | 0.40 | 0.36-0.43 |
| kappa (s(T) + gamma T_loc) | 0.78 | 0.64-0.92 |
| kappa East / West | 0.47 / 0.89 | 0.33-0.59 / 0.75-1.02 |

The binned local relation is flat for |T_loc| below about 0.5 C and steeper in the tails (Figure 1C),
so the local slope comes mainly from routes with large local contrasts (mostly in the West).
Results at sigma 40 and 150 km were nearly the same (kappa 0.77 and 0.77; `files/results/cti_spatial_slopes.csv`).

### 4.3 Species gradients: about 70% of the regional slope remains locally (Figure 2)

| Pooled species test (314 species) | kappa | 95% CI |
| --- | --- | --- |
| main, all routes | 0.69 | 0.58-0.76 |
| East / West | 0.63 / 0.70 | 0.49-0.69 / 0.54-0.80 |
| with precipitation control | 0.50 | 0.39-0.58 |
| 1-degree cell fixed effects | 0.73 | 0.58-0.80 |
| smoothing sigma 40 km | 0.70 | 0.53-0.78 |
| smoothing sigma 150 km | 0.69 | 0.60-0.75 |
| routes with paths only (307 species) | 0.70 | 0.59-0.77 |
| start-point climate instead of route path (312 species) | 0.53 | 0.42-0.60 |
| spline df 6 | 0.70 | 0.58-0.76 |
| positive control (smooth niche, cell estimator) | 1.02 | 0.98-1.06 |
| placebo (T_loc shuffled within 2-degree blocks) | 0.14 | 0.06-0.23 |

With start-point climate in place of the route-path mean, kappa fell to 0.53, and the precipitation-controlled
kappa to 0.27. A single point mismeasures the local temperature of a 40 km route, so this is the expected
attenuation (section 4.1); the route-path values are the main result.

The placebo is not exactly 0 because the shuffle keeps the block means of T_loc, which hold 26% of the
T_loc variance; the expected leakage is about 0.26 x 0.69 = 0.18. The estimator thus separates
"local response present" from "no local response". Among the 109 species with both slopes more than 2 SE
from 0, 78% had the same sign locally and regionally.

**Exploratory (not in the plan): the scale test fails mainly for warm-adapted species.** Species with
an STI below the median kept most of the regional slope locally (kappa 0.85, 95% CI 0.74-0.91; cell
estimator 0.98, 0.82-1.10), but species with an STI above the median did not (kappa 0.43, 0.25-0.54;
cell 0.54, 0.40-0.62). A split by the sign of the regional slope gave the same pattern (species that
decrease with temperature 0.94, 0.82-1.01; species that increase 0.32, 0.18-0.43). Positive controls
were 1.01-1.03 in all groups. Examples: Northern Cardinal regional slope 0.28 log count per C, local
0.04; Tufted Titmouse 0.25 and -0.01; Chestnut-sided Warbler -0.33 and -0.37; Winter Wren -0.28 and -0.21.
Thus the cold side of species ranges follows temperature at every scale, but much of the warm-species
continental gradient is not a local temperature response.

### 4.4 Year-to-year tracking is about 3% with either climate product (Figure 3)

| gradient / anomaly | lambda, same summer (SE) | lambda, same + previous summer (SE) |
| --- | --- | --- |
| GHCN_CAMS / GHCN_CAMS | 0.018 (0.002) | 0.030 (0.003) |
| GHCN_CAMS / nClimGrid | 0.017 (0.002) | 0.029 (0.003) |
| nClimGrid / GHCN_CAMS | 0.020 (0.002) | 0.033 (0.003) |
| nClimGrid / nClimGrid | 0.019 (0.002) | 0.032 (0.003) |

Random-effects pooling gave 0.030-0.033 for the same summer. Exploratory groups: low-STI species 0.040
(SE 0.005), high-STI species 0.031 (0.003). The species with scale-consistent gradients thus do not
track much better. Between species, mean year-to-year responses did not scale with mean gradients
(level ratios -0.02 to 0.003), as in sci:sha256:91f371b5. With the local gradient as denominator (lambda / kappa) the two-summer ratio is
0.032 / 0.69 = 0.047 (0.064 with the precipitation-controlled kappa); for low-STI species it is
0.040 / 0.85 = 0.047.

### 4.5 CTI trend against each denominator

On the same route-years, May-July temperature increased by 0.237 C per decade (95% CI 0.228-0.248).
The CTI increased by 0.025 C per decade (0.017-0.032) with route x observer effects and by 0.005
(-0.002 to 0.012) with route effects only. The CTI / temperature ratio was 0.10 (0.07-0.14) or 0.02
(-0.01 to 0.05). Divided by the spatial CTI slopes, the "slow fraction" is 0.24 (continental,
nClimGrid), 0.28 (local T_loc) and 0.26 (within cells, nClimGrid) for the within-observer trend. A
within-cell denominator from GHCN_CAMS would give 0.45, an artefact of section 4.1. Prior work
(sci:sha256:b113aa1b) found that observer hearing-type drift makes 31-77% of the within-observer CTI
trend; with that correction the slow fraction is about 0.06-0.19 for every denominator. We did not
recompute that correction here.

## 5. Interpretation

* The denominator of the bird tracking deficit is mostly a real thermal gradient. Between nearby routes,
  bird communities differ by 0.37-0.40 C of CTI per C of local temperature, close to the continental
  0.43. Species abundance gradients keep about 70% of their regional slope locally (50% with a
  precipitation control).
* Therefore a biogeographic denominator explains at most a factor of about 1.4-2 of the deficit. The
  deficit itself is a factor of about 4-30 (year-to-year lambda 0.03; slow CTI fraction 0.04-0.28). Most of
  the deficit is in the temporal response, not in the spatial reference.
* Better climate data do not remove the deficit. nClimGrid anomalies changed lambda by less than 0.003.
  Coarse 0.5-degree climate makes gradients about 16% flatter (1/1.19) and halves within-region CTI
  slopes, so ratios with a coarse within-region denominator overstate tracking.
* Exploratory: warm-adapted species have continental gradients that only partly repeat at the local
  scale (kappa about 0.3-0.4). Their continental gradient thus overstates the warming response that
  a local temperature mechanism can produce. Cold-adapted species pass the scale test, but they still
  track year-to-year warming at only about 4%.

## 6. Limitations

* Correlational design. Local temperature contrasts come mostly from elevation and coast, which also
  change habitat (forest type, land use) and precipitation. The precipitation control reduced kappa
  to 0.50, so part of the local "thermal" slope can be a moisture or habitat effect. We had no land
  cover data.
* nClimGrid is an interpolated product. Its local contrasts depend on its elevation model; we did not
  compare it with station data. Route paths are from 1966-1998 and 25% of routes used the start point.
* Route means of log(1 + count) mix observers and years and do not model detection. Detection can
  differ with elevation or habitat. The temporal model uses route x observer effects, but the
  hearing-type drift found in prior work is not removed from the CTI trend in section 4.5.
* The sigma of the Gaussian smooth defines "local". Results for 40-150 km were similar, but
  smaller scales (single valleys) are not resolved by 40 km routes.
* The pooled kappa uses precision weights; a few well-measured species have a large weight. The placebo
  shows some leakage of block-scale structure (0.14).
* The STI and sign splits were not in the plan; treat them as hypotheses. The bootstrap includes
  spatial correlation between species, but not uncertainty of the climate fields.
* Contiguous US only (nClimGrid). No winter or migration-route climate.

## 7. Files

* `files/PLAN.md` - analysis plan written before outcomes.
* `files/code/` - `00_fetch.sh` (download and hash check), `01_prep.py` (runs, counts, route climate),
  `02_spatial.py` (species scale tests and joint bootstrap), `03_temporal.py` (lambda), `04_cti.py`
  (CTI slopes), `05_summarize.py` (pooling), `06_figures.py`, `07_cti_trend.py`, `08_make_scijson.py`, `run_all.sh`.
* `files/results/pooled_scale_tests.csv` - all pooled kappa estimates (variants, units, exploratory groups).
* `files/results/species_scale_estimates.csv` - per species and unit: regional and local slopes, gamma,
  cell slopes, GHCN_CAMS and nClimGrid gradients with bootstrap SEs.
* `files/results/species_temporal_estimates.csv` - per-species temporal coefficients (2 x 2 design).
* `files/results/temporal_lambda.csv`, `cti_spatial_slopes.csv`, `cti_trend_tracking.json`, `summary.json`.
* `files/results/route_climate_cti.csv` - per-route climate parts (nClimGrid, GHCN_CAMS) and
  cross-fitted CTI (no coordinates; join with BBS Routes.csv by rid = 84000000 + state x 1000 + route).
* `files/figures/` - three figures.

## 8. Reproduction

1. `bash files/code/00_fetch.sh /local/datasets` (about 3.6 GB; checks SHA-256 hashes). In the campaign
   the same files are in `datasets/` (paths in `files/input_hashes.txt`).
2. `bash files/code/run_all.sh /local/datasets /local/scratch files/results files/figures`
   (about 1.5-2 h at host load 35-45 with 6 workers; Python 3.12, numpy, pandas, scipy, patsy,
   geopandas, netCDF4, xarray, matplotlib). Bootstrap seeds are fixed in the scripts.
