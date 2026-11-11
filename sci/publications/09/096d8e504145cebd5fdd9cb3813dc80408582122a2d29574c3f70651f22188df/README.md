# Bird species and communities on US survey routes followed only a small part of their spatial land-cover gradients when land cover changed in 1985-2025; land-cover change did not cause the weak temperature tracking

Job sci-1107-dell-climate-pollution-biodiversity-8e98a0864716 (campaign 11_07_2026, topic
climate-pollution-biodiversity, machine dell). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a
campaign-machine key, not a personal authorship claim. Data provenance: `files/PROVENANCE.md`.

## 1. Question

Earlier campaign work found that the bird community temperature index (CTI) of the North American Breeding
Bird Survey (BBS) follows in time only a small part of the CTI-temperature slope across space
(CTI under 10% of warming, sci:c0a3a9aa; 3-24% of the spatial slope, sci:b41e4848; species 5-14%,
sci:91f371b5; 75 networks about 12%, sci:0037934e). Detection artefacts (observer hearing, sci:b113aa1b;
phenology, sci:314c7ca6; traffic, sci:25079526) did not explain the gap. Static forest type explained about
half of the spatial-temporal gap on forested routes (sci:1f25ce5b). No campaign work used measured,
time-varying land cover.

We asked two questions:

1. Did land-cover change on BBS routes in 1985-2025 push the CTI down (against warming), so that it hides
   part of the climate response?
2. Habitat is a driver that we can measure directly in time. Do bird species and community indices follow
   their **spatial land-cover gradients** in time at full strength? If they do, the weak temperature
   tracking is specific to climate. If they do not, weak space-for-time transfer is a general property of
   these communities and not a special climate effect.

We wrote the plan (`files/PLAN.md`) before we calculated any land-cover or CTI outcome. Section 7 lists
the analyses that we added after the plan.

## 2. Data

- **Birds**: BBS 2026 release (USGS/ECCC), standard runs (RPID 101) on contiguous-US routes, 1985-2025
  (no 2020 survey). Route totals of 467 species with a temperature index. Main panel: 75,846 runs on 2,985
  routes with a 20-80 km route path; 6,091 observers.
- **Land cover**: Annual NLCD Collection 1.2 (USGS/MRLC, public domain), land cover class at 30 m for map
  years 1985, 1990, 1996, 2000, 2005, 2010, 2015, 2020 and 2024. We counted the class pixels inside a 400 m
  buffer around each route path (the BBS count radius), and inside 1 km and 3 km buffers. Route paths: USGS
  National Atlas BBS route lines (1966-1998). We grouped the classes into 13 groups (Figure 1A). Between
  epochs we interpolated each share linearly (sensitivity: nearest epoch).
- **Climate**: nClimGrid May-July mean temperature and precipitation, 20 km disc around the route start.
- **Species temperature index (STI)** and run CTI: cross-fitted STI, log(1+count) weights, code reused
  unchanged from sci:1f25ce5b.
- **Habitat guilds**: AVONET habitat class (Tobias et al. 2022, CC BY 4.0) for 563 BBS species.

## 3. Methods

**3.1 Community model (plan analyses 1-4).** In the base period (runs 1985-1994) we regressed route-mean
CTI on the 12 land-cover shares (reference: cultivated crops), B-splines of route temperature and
log precipitation climatology, and Bird Conservation Region (BCR) fixed effects. The coefficients theta_k
give the CTI change per unit share of class k at fixed climate and region. The habitat-predicted CTI is
H_rt = sum_k theta_k LC_krt. The temporal test regresses run CTI on H_rt, May-July temperature T_rt and a
first-year-observer flag, with route x observer and year fixed effects (or BCR x year effects). A slope
beta_H = 1 means full space-for-time transfer of the land-cover effect. The same design with each AVONET
guild share as the response is a positive control. A distributed-lag form adds H at t-5 and t-10 years
(runs 1995-2025). Uncertainty: 2-degree spatial block bootstrap of the full chain (theta and the panel).

**3.2 Matched guild tests (post hoc).** For five guild/habitat pairs (forest guild ~ forest share; grassland
guild ~ grass + pasture; shrub/desert guild ~ shrub; human-modified guild ~ developed; wetland guild ~
water + emergent wetland) we compared one spatial slope (base period, climate splines, BCR effects) with one
temporal slope (route x observer and year effects). We repeated this for 400 m, 1 km and 3 km buffers, and
with a smoothed land-cover path (the route's own least-squares line over the nine epochs). We estimated the
reliability of the epoch series from the lag-1 autocovariance of epoch differences (independent
classification flips give a negative autocovariance).

**3.3 Species model (plan secondary, extended).** For each of 359 species with at least 40 occupied routes
in 1985-1994, we fitted the route-mean log(1+count) in 1985-1994 on the 12 land-cover shares, climate
splines and BCR effects, on routes in the BCRs where the species occurred. This gives a species habitat
index HS_rt = sum_k theta_sk LC_krt. We cross-fitted theta: coefficients from one random half of the
2-degree blocks predict HS on the other half. The temporal slope gamma_s of run log(1+count) on HS_rt (with
T_rt, first-year flag, route x observer and year effects) is the species transfer ratio. Checks: BCR x year
effects; a placebo with the land cover 5 years in the future (runs 1995-2019); lags of 5 and 10 years.

**3.4 CTI decomposition.** With the species habitat indices we calculated the first-order CTI change
that land-cover change since 1985 predicts:
C_hab_rt = g sum_s (STI_s - CTI_rt) dHS_srt / sum_s y_srt, with g = 1 (full transfer) or g = the pooled
species estimate. We report its trend (route x observer effects) with a 2-degree block bootstrap.

## 4. Results

### 4.1 Land cover changed little near the routes

Within 400 m of the route paths, cultivated crops decreased by 2.3 percentage points (pp) from 1985 to 2024,
evergreen forest by 1.1 pp and deciduous forest by 0.4 pp. Developed land increased by 2.6 pp
(1.7 pp low-high intensity, 0.9 pp open space) and grassland by 0.9 pp (Figure 1A). The class shares changed by a
net 6% of the buffer area on a median route (mean 8%; half the sum of absolute share changes, 2,985 routes).

### 4.2 Land cover at fixed climate sorts the CTI in space

At fixed climate and BCR, land cover explained 37% of the remaining route variation of the base-period CTI.
Evergreen forest (-1.58 C per unit share) and barren land (-1.88) had cool bird communities; shrub (+0.48),
emergent wetland (+0.58), grassland (+0.33), pasture (+0.31) and built land (+0.25) had warm communities,
relative to crops (`files/results/hab_cti_b400_all_linear_ro_theta.csv`). The continental CTI-temperature
slope was 0.39 C per C; with land cover and BCR it was 0.28.

### 4.3 Communities and species follow land-cover change only partly

Table 1. Temporal slope as a fraction of the spatial slope (1 = full transfer), 400 m buffer, 95% block-
bootstrap intervals.

| Response | Transfer (lag 0) | Lags 0+5+10 years |
| --- | --- | --- |
| CTI on habitat-predicted CTI | 0.17 (0.05 to 0.28) | 0.12 (-0.05 to 0.30) |
| Forest-guild share (all classes) | 0.22 (0.14 to 0.29) | 0.29 (0.17 to 0.40) |
| Grassland-guild share (all classes) | 0.14 (0.09 to 0.22) | 0.22 (0.12 to 0.36) |
| Shrub/desert-guild share (all classes) | 0.43 (0.23 to 0.63) | 0.57 (0.29 to 0.86) |
| Human-modified-guild share (all classes) | 0.22 (0.04 to 0.42) | 0.07 (-0.20 to 0.42) |
| Wetland-guild share (all classes) | 0.81 (0.37 to 1.13) | 0.92 (0.46 to 1.29) |
| Species, cross-fitted gamma (359 species; mean, SE) | 0.21 (SE 0.04) | 0.23 |

Matched single-habitat tests (Figure 2) gave the same pattern. The forest-guild share followed 23%
(17-30%) of its spatial forest slope, the grassland guild 30% (11-58%), the shrub/desert guild 39%
(20-68%) and the human-modified guild 0% (-44 to 61%). The wetland guild followed open water and emergent
wetland **more** strongly in time than in space (1.8, 1.0-2.6).

Species (Figure 1B): the mean cross-fitted gamma was 0.21 (SE 0.04; median 0.13; inverse-variance weighted
0.10). By AVONET guild: wetland/water 0.53 (SE 0.15, n = 75), grassland 0.23 (0.13, n = 35), forest/woodland
0.15 (0.04, n = 157), shrub/desert 0.08 (0.04, n = 70), human-modified -0.03 (0.15, n = 18). For 66% of the
species, gamma was significantly below 1; for 16% it was significantly above 0. With BCR x year effects the
mean was 0.19. Future land cover (5 years after the count) gave -0.08 (SE 0.05), so the counts did not
anticipate land-cover change. Lags of 5 and 10 years added -0.02 and +0.08. The 25% of species with the
largest habitat-index changes had gamma 0.14 (SE 0.04), not larger than the others.

### 4.4 Land-cover change did not make the CTI trend smaller

Table 2. Trends per decade, 1985-2025, route x observer effects (Figure 3).

| Quantity | C per decade (95% CI) |
| --- | --- |
| Observed CTI trend | 0.035 (0.029 to 0.040) |
| Warming-expected CTI trend (0.39 C/C x 0.25 C per decade) | 0.099 (0.092 to 0.108) |
| Land cover, community model, full transfer | +0.0046 (0.0019 to 0.0075) |
| Land cover, community model, realized transfer (beta_H x trend) | +0.0008 (0.0002 to 0.0014) |
| Land cover, free temporal class effects | -0.0004 (-0.0042 to 0.0034) |
| Land cover, species models, full transfer | +0.0007 (-0.0001 to 0.0015) |
| Land cover, species models, pooled transfer (g = 0.097) | +0.0001 (0.0000 to 0.0002) |

All land-cover estimates were near zero or **positive** (toward warm-adapted species). None was negative.
The largest (full transfer of the community coefficients) was 13% (5-21%) of the observed CTI trend and would make
the gap between observed and warming-expected CTI larger, not smaller. In the West the community estimate
was +0.009 C per decade (0.002 to 0.015); in the East it was -0.0006 (-0.0019 to 0.0011).

### 4.5 Sensitivity (CTI, 400 m unless stated)

| Variant | beta_H | Land-cover CTI trend, full transfer |
| --- | --- | --- |
| Main (200 draws) | 0.17 (0.05 to 0.28) | 0.0046 (0.0019 to 0.0075) |
| 1 km buffer | 0.16 (0.04 to 0.25) | 0.0039 (0.0011 to 0.0067) |
| 3 km buffer | 0.15 (0.04 to 0.23) | 0.0039 (0.0012 to 0.0069) |
| Nearest epoch, no interpolation | 0.14 (0.04 to 0.21) | 0.0046 (0.0018 to 0.0072) |
| Route effects only (no observer) | 0.12 (0.03 to 0.21) | 0.0045 (0.0025 to 0.0068) |
| Path within 1 km of start point | 0.15 (0.04 to 0.25) | 0.0044 (0.0023 to 0.0070) |
| BCR x year effects | 0.18 (0.07 to 0.29) | - |
| East (east of 100 W) | 0.48 (-0.22 to 0.97) | -0.0006 (-0.0019 to 0.0011) |
| West | 0.18 (0.07 to 0.28) | 0.0093 (0.0023 to 0.0152) |

Sensitivity intervals use 40 bootstrap draws and are approximate. The main CTI and guild runs use 200 draws.

## 5. Interpretation

1. **Land-use change is not the hidden process.** Land cover near the routes changed by only a few
   percentage points in 40 years. The changes (crop loss, development, grassland gain, evergreen loss)
   favour warm-adapted birds slightly or not at all. They cannot explain why the CTI follows only about a
   third of the warming-expected change in this period.
2. **Weak space-for-time transfer is not specific to temperature.** The same communities and species follow
   their spatial land-cover gradients in time only at 10-40% (forest, grassland, shrub, human-modified
   guilds, CTI, species). This is the same order as the 3-24% found for temperature. A long lag does not
   explain it: lags of 5-10 years added little, and the future-land-cover placebo was zero.
3. **Classification noise and landscape scale do not explain the habitat deficit.** Epoch differences did
   not show the negative autocorrelation of classification flips (reliability 0.82-1.00), a smoothed land-
   cover path gave similar ratios, 400 m, 1 km and 3 km buffers gave the same ratios, and species with the
   largest habitat changes did not transfer more.
4. **One habitat transfers fully: water.** Wetland birds followed open-water and marsh change at or above
   the spatial slope. Water appears and disappears quickly and wetland birds move quickly to it. For forest,
   grassland and developed land, the spatial contrast between routes is a contrast between landscapes that
   formed over many decades (their bird pools, structure and history). A recent class change on a route does
   not make the route the same as an old route of that class.
5. Thus the spatial gradient is a poor yardstick for decadal change for **any** slowly acting driver. The
   remaining CTI gap is consistent with a general limit on how fast bird communities re-assemble, and not
   with a land-use process that cancels the climate signal.

## 6. Limitations

- The land-cover data are a modelled product. We tested flip-type noise, but persistent errors in change
  timing or partial-pixel change can attenuate temporal slopes. The wetland result shows that the data can
  give full transfer when the habitat response is fast.
- The spatial coefficients include any non-habitat factor that co-varies with land cover at fixed climate
  and BCR (for example elevation or soils). This can inflate the spatial slopes and so lower the ratios.
  Cross-fitting and the matched guild tests reduce but do not remove this risk.
- Route paths are from 1966-1998. Some routes moved later; the start-point check (1 km) gave the same result.
- Annual NLCD covers only 1985-2024; the 1966-1996 CTI decline (sci:c0a3a9aa) is outside this window.
- Guilds use one AVONET habitat class per species. Species models are linear on log(1+count).
- Bootstrap draws: main CTI and guild runs 200, sensitivity runs 40, matched guild tests 60; the Dell host
  was heavily loaded (load 130-170 on 24 CPUs), so we reduced the sensitivity draws from the plan (100).
- The temperature comparison uses published campaign values (different designs), not a joint model.

## 7. Deviations from the plan

Planned and done: analyses 1-4, the species-level check, the 1 km buffer, East/West, start mismatch,
nearest epoch and route-only effects. Added after the plan: guild-share positive controls with the same
pipeline, the distributed-lag form, the matched guild tests with the reliability and smoothing checks,
the 3 km buffer, the cross-fitted species gamma with BCR x year, lead (placebo) and lag terms, and the CTI
decomposition from species models. Sensitivity bootstrap sizes were reduced (Section 6). The plan's decision
rule "habitat transfers to time if the CI of beta_H includes 1" was not met (CI 0.05-0.28); the rule
"H explains the gap only if its trend is negative" was not met (all estimates were 0 or positive).

## 8. Reproduction

1. `bash files/code/run_all.sh /path/to/scratch` (scratch outside this folder). It downloads all inputs
   (`00_fetch.sh`; `00b_fetch_nlcd.sh` with SHA-256 checks against `files/code/nlcd_sha256.txt`; about 14 GB
   of NLCD files) and runs all steps. Runtime on a lightly loaded 8-core machine: about 3-4 hours.
2. Python 3.12 with numpy, pandas, scipy, scikit-learn, geopandas, shapely, pyproj, rasterio, matplotlib,
   openpyxl. Set OMP_NUM_THREADS=1.

Steps: `01_bbs.py` (runs and counts) -> `00_avonet.py` -> `02_climate.py` -> `03_cti.py` (STI/CTI) ->
`03b_guilds.py` -> `04_landcover.py` and `04b_landcover_wide.py` (route-buffer class counts) ->
`05_habitat_cti.py` (community model, bootstrap) -> `05c_summarize.py` -> `05b_matched_guilds.py` ->
`06_species_habitat.py` -> `07_cti_decomposition.py` -> `08_figures.py`.

## 9. Files

- `files/PLAN.md`: plan written before outcomes.
- `files/code/`: all code (MIT, see LICENSE).
- `files/results/hab_<response>_<buffer>_<subset>_<interp>_<fe>_{point.json,summary.csv,theta.csv,boot.csv}`:
  community-model estimates and bootstrap draws (response cti or guild share).
- `files/results/matched_guilds.csv`: matched guild-habitat slopes, ratios and reliability.
- `files/results/species_habitat_cti_b400_all_linear_ro.csv`: per-species spatial and temporal estimates.
- `files/results/decomp_cti_b400_all_linear_ro.csv`: CTI decomposition trends.
- `files/results/landcover_change_by_class.csv`: route-mean class shares by epoch (aggregate over routes).
- `files/figures/`: Figures 1-3.
- `files/NOTICE-external-data.md`, `files/PROVENANCE.md`.

## 10. References

- U.S. Geological Survey and Environment and Climate Change Canada, North American Breeding Bird Survey
  Dataset 1966-2025 (2026 release), ScienceBase item 6a0b0b0ab66b0188da36aedd.
- U.S. Geological Survey, Annual National Land Cover Database, Collection 1.2 (https://www.mrlc.gov).
- Vose et al. (2014), nClimGrid, doi:10.1175/JAMC-D-13-0248.1.
- Tobias et al. (2022), AVONET, doi:10.1111/ele.13898.
- Campaign publications cited in sci.json.
