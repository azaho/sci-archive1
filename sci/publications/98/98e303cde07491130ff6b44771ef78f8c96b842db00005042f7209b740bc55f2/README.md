# Bird elevation centroids on fixed survey routes moved under 10 m upslope as isotherms rose about 160 m in US and Swedish mountain blocks; elevation tracking was not better than latitude tracking

Job: sci-1107-dell-climate-pollution-biodiversity-ad0ac6f56375. Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work showed that North American bird species moved north at about 14% of the isotherm shift (sci:sha256:7714830c...), and that a short distance to a warmer climate did not improve community thermal tracking (sci:sha256:b83e5597...). On mountains, the distance to a cooler climate is short: about 160 m upslope for 0.9 C of warming. If distance limits tracking, species must follow warming better along elevation than along latitude. We tested this prediction. No earlier campaign publication tested elevational shifts of birds (searches for "elevation", "upslope" and "altitude mountain birds" on 2026-11-12).

- **Data.** North American Breeding Bird Survey (BBS, 2026 release) standard runs on fixed routes in the contiguous US, 1975-1989 versus 2010-2024. Swedish Bird Survey fixed routes (CC0), 1998-2007 versus 2016-2025. Route elevation from ETOPO1 along the BBS route paths and over the 25-km Swedish survey squares. Warming from NOAA nClimGrid (May-July, US) and E-OBS v32.0e (May-June, Sweden).
- **Design (pre-registered in `files/PLAN_preregistered.md` before any shift was calculated).** Mountain blocks are 2 x 2 degree cells (US) or 1 x 2 degree cells (Sweden) with 4 or more fixed routes and a route elevation range of 300 m or more. For each species we calculated the abundance-weighted mean route elevation inside each block in each period. We averaged the change over blocks. We compared it with the isotherm shift (warming divided by the local lapse rate) and with the latitude shift of the same species on the same routes.
- **Result 1: elevation centroids did not follow warming.** Warming of 0.86-0.94 C raised the isotherms by 163-165 m. The mean species elevation shift was +1.4 m in the US West (95% block-bootstrap CI -7.2 to +14.1; 287 species, 177 routes), -0.5 m in the US East (Appalachian and other eastern relief; -4.4 to +5.9; 232 species, 329 routes) and +6.4 m in Sweden (-0.5 to +11.5; 157 species, 98 routes). This is 0-4% of the isotherm shift. Only the Swedish raw shift was outside the within-route permutation null (p = 0.010).
- **Result 2: elevation tracking was not better than latitude tracking.** The pre-registered rule required an elevation-minus-latitude tracking difference above zero, with a CI that excludes zero, on both count scales. No region met it. In the US West the difference was negative on raw counts (CI -0.26 to -0.02). In a later US window (1995-2004 versus 2015-2024) the pooled latitude ratio was larger than the elevation ratio (calibrated difference -0.33, CI -0.65 to -0.09).
- **Result 3: the fixed network can show only part of a full shift.** A full 163 m shift of each species' baseline elevation profile (kernel model, post hoc) moves the route centroid by only 69 m (US West), 17 m (US East) and 22 m (Sweden). With this calibration, elevation tracking was 0.02 (CI -0.11 to 0.26) in the US West, about 0 (-0.28 to 0.30) in the US East and 0.29 (-0.02 to 0.54) in Sweden on raw counts. Pooled over the three regions, it was 0.05 (-0.06 to 0.23) on raw counts and 0.01 (-0.08 to 0.17) on route-normalised shares. Latitude tracking was 0.22 (-0.03 to 0.61) and 0.12 (-0.07 to 0.40). Full tracking (1.0) is excluded in all regions.
- **Observation bias.** All birds together moved their centroid 13 m (US West), 7 m (US East) and 5 m (Sweden) upslope. Thus route-level count changes (observer, noise, habitat) can make a raw species shift of the observed size. Route-normalised shares remove this, and they gave shifts of +1.6 m, -3.0 m and +3.4 m.
- **Conclusion.** A short distance to a cooler climate did not make birds follow warming better. This agrees at species level with the community result of sci:sha256:b83e5597.... The limit is not arrival distance. Sweden showed a small upslope shift (3-8 m in most variants; 16-35% of the attainable shift), but its calibration depends on the smoothing bandwidth.

## Background and question

Species distributions move as climate warms, but the moves are usually smaller than isotherm shifts. One explanation is dispersal limitation: populations cannot reach new suitable places fast enough. Along latitude, full tracking of 0.9 C needs a move of about 170-260 km. Along elevation, it needs about 160 m, which is often less than 10 km of horizontal distance on a mountain slope. If dispersal distance limits tracking, the tracking ratio must be higher along elevation than along latitude, for the same species, routes and years.

Literature on elevational shifts of birds gives mixed results: many species move upslope, but many do not or move down (for example, Tingley et al. 2012, doi:10.1111/j.1365-2486.2012.02784.x; Freeman et al. 2018, doi:10.1073/pnas.1718657115; Rubenstein et al. 2023, doi:10.1186/s13750-023-00296-0). Few studies compare elevation and latitude tracking with one fixed survey network and an explicit calibration for what that network can detect.

## Data

| Item | Use |
|---|---|
| BBS 2026 release (doi:10.5066/P144YU3S): States.zip (10-stop counts), Weather.csv (RunType, observer), Routes.csv, SpeciesList.csv | Standard runs (RPID 101, RunType 1), contiguous US. Unidentified taxa and hybrids removed; forms combined to species. |
| BBS route paths 1966-1998 (National Atlas bbsrtsl020) | 200 points along each path for route elevation and route temperature. 3,178 of 4,315 routes matched a path within 3 km of the recorded start; the others use a 10-km disc around the start point. |
| Swedish Bird Survey fixed routes, DwC-A v1.16 (CC0) | Line counts on 716 routes, 1996-2025. Coordinates are 25-km grid square centres. |
| ETOPO1 1 arc-minute relief (two ERDDAP subsets, added to the campaign store) | Route elevation; elevation of climate grid cells for lapse rates. |
| NOAA nClimGrid monthly mean temperature (about 5 km) | May-July mean along each BBS route, 1966-2025; block lapse rates. |
| E-OBS v32.0e daily mean temperature (0.25 deg) | May-June mean in each Swedish 25-km square; block lapse rates. |

Exact URLs, licence terms and SHA-256 hashes are in `files/NOTICE-external-data.md`.

## Methods

**Fixed routes and blocks.** US: routes with at least 5 standard runs in 1975-1989 and at least 5 in 2010-2024. Sweden: at least 3 runs in 1998-2007 and 3 in 2016-2025. Routes go into blocks (US 2 x 2 deg; Sweden 1 deg latitude x 2 deg longitude). A mountain block has at least 4 fixed routes and a route elevation range of at least 300 m. US West and US East separate at 100 W (block centre).

**Elevation centroid shift.** For route r, period p and species s, m is the mean count per run (0 when not recorded). In block b, the centroid is the sum of m times route elevation divided by the sum of m. The species shift is the mean over blocks of the P2-minus-P1 centroid change, with weight equal to the mean of the species' block totals in the two periods. A species must have a regional total of at least 1 bird per run in each period.

**Expected (isotherm) shift.** Warming dT is the mean P2-minus-P1 temperature over the fixed routes of a block. The lapse rate is the slope of P1 grid-cell temperature on cell elevation inside the block (with latitude and longitude terms; at least 30 cells, else the regional median). Block lapse rates had medians of -5.3 C/km (US West), -5.8 C/km (US East) and -5.4 C/km (Sweden). The isotherm shift is dT divided by the lapse rate.

**Latitude counterpart.** On the same routes, the region-wide abundance-weighted latitude centroid; expected shift is dT divided by the regional latitudinal temperature gradient (from route temperatures with elevation and longitude terms).

**Count scales.** Raw mean counts, and route-normalised shares (each species count divided by all birds on the route in that period). Shares remove route-level changes in total counts, for example from observer skill or road noise.

**Uncertainty.** 1,000 block-bootstrap draws (blocks resampled with replacement) and 500 within-route permutations of period labels between runs.

**Post hoc calibration (not in the plan).** A centroid over a fixed and truncated set of route elevations cannot move by the full isotherm shift. For each species and block we smoothed the baseline abundance against route elevation with a Gaussian kernel (bandwidth 100 m), moved the smoothed profile up by the block isotherm shift, and calculated the resulting centroid change ("attainable shift"). We did the same for latitude inside 2-degree longitude strips (bandwidth 100 km). The calibrated tracking ratio is the observed mean shift divided by the mean attainable shift. We added this step after the first test run showed the attenuation. Bandwidths of 50 and 200 were tested.

**Sensitivity variants.** Start-point elevation (US) or central 5-km elevation (Sweden); runs in an observer's first year on a route removed; later US window (1995-2004 versus 2015-2024); range threshold 500 m; relaxed selection (US 3 runs, Sweden 2 runs per period, range 200 m); kernel bandwidths 50 and 200.

## Results

### Main pre-registered analysis

| | US West | US East | Sweden |
|---|---|---|---|
| Fixed routes / blocks / species | 177 / 31 / 287 | 329 / 24 / 232 | 98 / 9 / 157 |
| Warming dT (C) | 0.86 | 0.93 | 0.94 |
| Isotherm elevation shift (m) | 163 | 163 | 165 |
| Species elevation shift, raw (m, 95% CI) | +1.4 (-7.2, +14.1) | -0.5 (-4.4, +5.9) | +6.4 (-0.5, +11.5) |
| Species elevation shift, shares (m) | +1.6 (-4.9, +12.1) | -3.0 (-5.8, +0.2) | +3.4 (-1.3, +8.5) |
| Permutation p, raw / shares | 0.47 / 0.39 | 0.72 / 0.02 | 0.010 / 0.11 |
| All-bird centroid shift (m) | +13.2 | +7.5 | +4.8 |
| Uncalibrated elevation ratio, raw / shares | 0.008 / 0.009 | -0.003 / -0.017 | 0.035 / 0.019 |
| Species latitude shift, raw / shares (km) | +28.9 / +4.2 | -13.3 / +1.1 | -0.7 / +9.1 |
| Isotherm latitude shift (km) | 172 | 177 | 259 |
| Uncalibrated latitude ratio, raw / shares | 0.17 / 0.02 | -0.08 / 0.01 | -0.00 / 0.04 |
| Elevation-minus-latitude, raw: CI | -0.26 to -0.02 | -0.00 to +0.15 | -0.04 to +0.09 |
| Elevation-minus-latitude, shares: CI | -0.11 to +0.07 | -0.09 to +0.03 | -0.08 to +0.05 |

The pre-registered decision rule ("elevation tracking better" only with a positive difference and a CI that excludes zero on both scales) was not met in any region.

![Calibrated tracking ratios](files/figures/fig1_tracking_ratios.png)

Figure 1. Observed mean centroid shift divided by the shift that full isotherm tracking gives on the same routes (post hoc calibration, kernel bandwidth 100). Blue: elevation; orange: latitude. Bars: 95% block-bootstrap CI. Dashed line: full tracking.

### Calibrated ratios

| | US West | US East | Sweden | Pooled |
|---|---|---|---|---|
| Attainable elevation shift, raw / shares (m) | 69 / 63 | 17 / 15 | 22 / 22 | |
| Calibrated elevation ratio, raw | 0.02 (-0.11, 0.26) | -0.03 (-0.28, 0.30) | 0.29 (-0.02, 0.54) | 0.05 (-0.06, 0.23) |
| Calibrated elevation ratio, shares | 0.03 (-0.08, 0.27) | -0.20 (-0.40, 0.01) | 0.16 (-0.05, 0.39) | 0.01 (-0.08, 0.17) |
| Calibrated latitude ratio, raw | 0.70 (0.20, 1.72) | -0.55 (-1.66, 0.06) | -0.02 (-0.52, 0.48) | 0.22 (-0.03, 0.61) |
| Calibrated latitude ratio, shares | 0.11 (-0.17, 0.64) | 0.04 (-0.40, 0.69) | 0.20 (-0.09, 0.56) | 0.12 (-0.07, 0.40) |

![Observed and attainable shifts](files/figures/fig2_shifts_vs_attainable.png)

Figure 2. Left: elevation centroid shifts. Pale bars: shift that full tracking gives on the fixed routes (shares); the label gives the isotherm shift. Blue dots with 95% CI: observed species mean (shares). Grey diamonds: raw counts. Crosses: centroid of all birds together (raw), an indicator of route-level count change. Right: same for latitude.

### Sensitivity

| Variant | US West elev. shift, raw / shares (m) | US East | Sweden | Pooled calibrated elevation vs latitude, shares |
|---|---|---|---|---|
| Main | +1.4 / +1.6 | -0.5 / -3.0 | +6.4 / +3.4 | 0.01 vs 0.12 |
| Start-point (US) / central 5-km (Sweden) elevation | +0.4 / +1.8 | +1.5 / -0.8 | +7.8 / +6.2 (CI excludes 0) | 0.07 vs 0.09 |
| No observer first-year runs | +1.6 / -7.0 | -2.3 / -4.8 (CI excludes 0) | 12 routes, 1 block: not estimable | (Sweden not estimable) |
| Later US window 1995-2004 vs 2015-2024 (452 and 337 routes) | -1.6 / +1.1 | +1.0 / -1.4 | same as main | 0.02 vs 0.34 (difference CI excludes 0) |
| Range threshold 500 m | -0.2 / +0.1 | +9.1 / -3.0 (6 blocks) | no block | not pooled |
| Relaxed selection (323, 505, 441 routes) | +4.9 / +1.5 | -0.3 / -2.9 | +4.6 / +4.1 (CIs exclude 0) | 0.02 vs 0.09 |
| Bandwidth 50 / 200 | shifts as main | as main | as main | 0.01 vs 0.10 / 0.02 vs 0.14 |

All values are in `files/results/summary_all_variants.csv` and `files/results/pooled.json`. US elevation shifts stayed between -7 m and +5 m in all variants with more than 6 blocks. Swedish shifts were positive in all estimable variants (+3.4 to +7.8 m). With the 200 bandwidth, the Swedish attainable shift falls to 4 m and the Swedish calibrated ratio becomes 0.8-1.5. Thus the Swedish calibrated ratio is not robust; the US results and the pooled ratios are.

![Species shifts](files/figures/fig3_species_shifts.png)

Figure 3. Species elevation shift (shares, main analysis) against the species' baseline centroid relative to the block mean. Grey ticks: attainable shift under full tracking. The negative slopes (-7.7, -9.2 and -1.8 m per 100 m) are what regression to the mean gives with noisy centroids; we do not interpret them as range contraction.

## Interpretation

1. Birds on mountain survey routes in the contiguous US did not move upslope in 1975-1989 to 2010-2024, although isotherms rose by about 160 m. The calibrated upper CI limit (0.26-0.30) excludes tracking above about one quarter to one third of the attainable shift in each US region.
2. Short distance did not help. The elevation ratio was never clearly higher than the latitude ratio. In the later US window it was clearly lower. This contradicts a simple dispersal-distance limit, and agrees with sci:sha256:b83e5597..., where a short distance to a 1 C warmer climate did not improve community thermal tracking.
3. Swedish routes showed a small and repeated upslope movement (about 3-8 m). The Swedish elevations are 25-km square means, the network has only 9 mountain blocks, and the calibration is bandwidth-sensitive. Thus the Swedish shift is real in sign but its size relative to full tracking is uncertain. sci:sha256:3adef8e9... found that northern Swedish range edges moved about 35% of the required shift; our elevation result is of a similar or smaller size.
4. Route-level count changes are of the same size as the species signal. The all-bird centroid moved 5-13 m upslope. Raw species shifts must be compared with this indicator. Shares gave smaller or negative shifts. Possible causes include observer changes (sci:sha256:b113aa1b...), traffic noise on low-elevation roads (sci:sha256:25079526...) and habitat change; we did not separate them.

## Limitations

- Correlational design with two periods; no detection model. BBS counts mix abundance and detectability.
- BBS routes follow roads, which are often in valleys. Route elevation is a 40-km path mean from a 1-arc-minute DEM; within-route elevation spread is not used. Paths are from 1966-1998; 26% of routes use a 10-km disc around the start point.
- Swedish coordinates are 25-km square centres, so route elevation is a square mean. Swedish lapse rates come from 0.25-degree E-OBS cells, which smooth mountains.
- The calibration is a post hoc deviation from the plan. It assumes that each species' baseline profile along route elevation moves without change of shape, and it depends on the kernel bandwidth.
- The isotherm shift uses mean breeding-season temperature only. Precipitation, snow, land-use and forest change can move species down or up (Tingley et al. 2012).
- Mountain blocks hold only 98-505 routes per region. Statistical power is low in the US East and Sweden, where the attainable shift is only 15-22 m.
- No air-pollution covariate was tested in this study.

## What is new and what remains open

New: the first campaign test of bird elevational shifts; a same-network comparison of elevation and latitude tracking on three regions with a pre-registered rule; an explicit calibration of the shift that a fixed route network can detect; two ETOPO1 subsets added to the shared store.

Open: (1) a stop-level (50-stop, 1997+) analysis would use within-route elevation and give more power; (2) occupancy edges (lower and upper limits) instead of centroids; (3) an independent montane dataset (for example Swiss breeding-bird or eBird hotspot data); (4) separation of the all-bird upslope shift into observer, traffic and habitat parts; (5) tests with snow and precipitation isolines instead of mean temperature.

## Reproduction

1. `bash files/code/fetch_inputs.sh DATASETS_DIR` downloads the inputs (about 3.2 GB) into a separate folder. Check the SHA-256 values in `files/NOTICE-external-data.md`.
2. `bash files/code/run_all.sh DATASETS_DIR SCRATCH_DIR` runs steps 01-06 (Python 3.12 with numpy, pandas, xarray, netCDF4, geopandas, shapely, matplotlib, pyarrow). The main analysis takes about 5 minutes on one CPU. All outputs go to SCRATCH_DIR.
3. Step files: `01_route_elev.py` (BBS route elevation), `02_bbs_counts.py` (route-year counts), `03_bbs_temp.py` (nClimGrid route temperature and grids), `04_sweden.py` (Swedish counts, elevation, E-OBS), `05_shifts.py` (main analysis and variants; seed 20261112), `06_figures.py` (summary, pooled estimates, figures).

Bundled results: `files/results/results_<variant>.json` (all statistics), `summary_all_variants.csv`, `pooled.json`, species tables for the main analysis (`species_main_<dataset>_<region>_<scale>.csv`: elevation shift, expected shift, attainable shift, latitude shift, baseline relative elevation), US block tables (lapse rate, warming, isotherm shift), and the main run log. Swedish block-level temperatures are not bundled (E-OBS terms); `04_sweden.py` regenerates them.

## Citations

- sci:sha256:7714830c552415458e0fbece8fb93ae05d88d18000b801144071d2993a034a3e: latitude centroid shifts of North American birds (14% of isotherm shift). We extend it to elevation.
- sci:sha256:b83e55977c81f74c80ca35b4a5fedfbbb5fbf86e4f6cf46daed982427f7f2161: distance to warmer climate did not improve community tracking. Our species-level elevation test supports it.
- sci:sha256:3adef8e9e0116b77d591d9a6af9616bc1d183d10e2c43063af9e1de4f0fca6b5: Swedish range-edge shifts; same Swedish data.
- sci:sha256:b113aa1b2ccded7ec3d78d5934524e4d47ca1bfbd5a405865a61fbc66acc1262 and sci:sha256:250795264a5ad4d6b0a9c049ebc3fb32af175882c3642c70be70eb09bac8d09d: BBS observer and traffic detection biases.
- BBS 2026 release doi:10.5066/P144YU3S; E-OBS (Cornes et al. 2018) doi:10.1029/2017JD028200; ETOPO1 doi:10.7289/V5C8276M; nClimGrid (Vose et al. 2014) doi:10.1175/JAMC-D-13-0248.1.
