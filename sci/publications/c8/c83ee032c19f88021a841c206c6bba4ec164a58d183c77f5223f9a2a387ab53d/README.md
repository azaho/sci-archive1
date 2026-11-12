# Eastern US tree growth and survival did not change on average with the 2000-2025 sulfur deposition decrease; red spruce and other conifers grew faster where sulfur decreased most

Job: sci-1107-dell-climate-pollution-biodiversity-d050b5ced972. Topic: climate-pollution-biodiversity.
Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a
campaign-machine key. It is not a personal authorship claim.

## 1. Question

Total sulfur (S) deposition in the eastern US decreased by about 85% from 2000 to 2025. Nitrogen (N)
deposition decreased by about 35%. Large inventory studies (Horn et al. 2018, PLoS ONE
13:e0205296; Dalton et al. 2024, Front. For. Glob. Change) fit tree growth and survival to the
**spatial** gradient of S and N deposition. Many species had negative S responses in those fits.

We asked: **when S deposition decreased at a plot, did the same trees grow faster and die less, by
the amount that the spatial relation predicts?** This is a space-for-time test of a pollution
effect on a biological response. The campaign record has many space-for-time tests for climate
(for example sci:sha256:0037934e, sci:sha256:8fb85925), but no test of tree growth against
deposition change. Related campaign results on deposition: Wood Thrush counts did not follow acid
deposition decrease (sci:sha256:9e80c094); bark lichens followed SOx decrease
(sci:sha256:d2550804); East German leaf colouring after the SO2 fall (sci:sha256:b6f27029). Forest
community change from FIA: sci:sha256:adb306e0, sci:sha256:8fb85925.

## 2. Data

* **Trees.** USDA Forest Inventory and Analysis (FIA) DataMart, annual inventory (DESIGNCD 1), 15
  states with a large deposition gradient: NH VT MA CT RI NY NJ PA DE MD WV KY OH IN TN.
  We used live trees with diameter at breast height (DBH) >= 5.0 in (12.7 cm) at the first visit,
  which FIA measured again on a later visit (1999-2026). Plots had 100% forest at both visits, no
  harvest or other treatment, and no artificial regeneration. Growth: change of DBH per year
  (mm/yr), same diameter-height code at both visits, no estimated diameters. Mortality: tree
  dead at the second visit and not cut (AGENTCD not 80), in percent per year (dead / interval
  length).
* **Deposition.** NADP/EPA TDep total S and total N deposition, annual 4-km grids 2000-2024.
  For each interval we used the mean of the calendar years from the first measurement year to
  the year before the second measurement.
* **Climate.** NOAA nClimGrid monthly. Growing-season (April-September) mean temperature and
  precipitation over the same years, and 1981-2010 normals.

Sample after filters: 12,739 plots, 327,707 trees, 617,033 growth intervals, 718,389 mortality
intervals. Mean growth 2.74 mm/yr. Mean mortality 1.35%/yr. For plots with two or more visits,
interval-mean S decreased from 9.25 to 3.02 kg S/ha/yr (mean change -6.2, interquartile
range -9.0 to -3.0). N decreased from 10.2 to 8.5 kg N/ha/yr (Figure 1).

## 3. Method

Response for growth: relative growth = growth / mean growth of the species (1 = species mean).
So a coefficient of 0.01 per kg S/ha/yr means 1% of species-mean growth per kg.
All models include species-specific log(DBH) and DBH terms, crown class, and plot basal area.
Standard errors are clustered by 1-degree cells (117-120 clusters). We also give 2-degree and
state clusters for the main models.

1. **Spatial model (Horn-type).** First interval of each tree that started in 1999-2006. Relative
   growth (or mortality) on S, N, temperature and precipitation normals, elevation, and species
   fixed effects. Variant: add state fixed effects.
2. **Within-tree temporal model.** Trees with two or more intervals (487,208 intervals). Tree fixed
   effects remove all fixed site and tree properties. State-by-measurement-year fixed effects
   remove common time changes in each state (for example CO2, regional weather, inventory
   changes). The S coefficient then comes from plots in the same state and year with different
   S decreases. Interval growing-season temperature and precipitation are controls.
   For mortality we used plot fixed effects (a tree dies only once).
3. **Initial-load test (no lag form).** S of 2000-2002 x decades from 2010. This tests whether
   growth changed more over time at plots that started with more S, for any lag.
4. **Species.** The same spatial and temporal models for each of the 25 most common species.
5. **Exploratory heterogeneity.** Conifers vs hardwoods, plots with red spruce or balsam fir,
   elevation, latitude, and initial S tercile.

Positive controls: the within-tree models must detect known weather effects. They did:
precipitation +2.9% growth per 100 mm (SE 0.66%), and growing-season temperature +0.31%/yr
mortality per 1 C (SE 0.11).

## 4. Results

### 4.1 Pooled growth: no response to the S decrease

| Model | S coefficient (relative growth per kg S/ha/yr) | 95% CI |
| --- | --- | --- |
| Spatial, species FE | +0.0096 | -0.0017 to +0.0209 |
| Spatial, species + state FE | +0.0154 | +0.0044 to +0.0264 |
| Spatial, only trees used in the temporal model | +0.0016 | -0.0060 to +0.0092 |
| **Within tree, state-year FE** | **-0.0003** | **-0.0072 to +0.0067** |
| Within tree, year FE only | -0.0037 | -0.0082 to +0.0008 |
| Within tree, plots with no recorded disturbance | +0.0012 | -0.0060 to +0.0085 |

With 2-degree clusters the main within-tree SE is 0.0042. With state clusters (15) it is 0.0080.
The mean plot S decrease (6.2 kg) multiplied by the main coefficient gives a growth change of
+0.2% of the species mean. The 95% CI is -4.2% to +4.5% (1-degree clusters) and -9.6% to +9.9%
(state clusters). The spatial slopes were near zero or **positive**, not negative. Thus in this
region the pooled spatial relation did not predict a growth gain, and no growth gain occurred.
The partial-residual plots (Figure 2) show no trend.

The initial-load test gave a small sign that depends on the N term. With S and N load together:
S load x decade -0.0060 (SE 0.0017), N load x decade +0.0226 (SE 0.0025). With S load alone:
+0.0030 (SE 0.0019). S and N loads of 2000-2002 have a correlation of 0.75, so this test cannot
separate them.

### 4.2 Pooled mortality: no clear response

S coefficients in %/yr per kg S/ha/yr: spatial -0.004 (SE 0.011); within plot, state-year FE
-0.012 (SE 0.019); within plot, year FE -0.025 (SE 0.014). The sign agrees with lower mortality at
higher S (opposite to harm), but no estimate is clear. The within-plot CI is wide: a 6.2-kg S
decrease is consistent with mortality changes from -11% to +22% of the mean rate.

### 4.3 Species: red spruce and some conifers grew faster where S decreased most

Within-tree S slopes for 25 species (Figure 3, right): 5 were negative with |z| > 1.96 (growth
increased as S decreased): red spruce -0.156 (SE 0.036), eastern white pine -0.041 (0.017),
sourwood -0.055 (0.021), American beech -0.027 (0.006), mockernut hickory -0.021 (0.010). Two were
positive: red maple +0.012 (0.005) and sweet birch +0.023 (0.010). Spatial S slopes: none
negative with |z| > 1.96, four positive (sugar maple, chestnut oak, northern red oak, scarlet oak).

Across species the spatial slope predicted the temporal slope only through red spruce: Pearson
r = 0.67, Spearman 0.23; without red spruce r = 0.20, Spearman 0.13. For red spruce the spatial
slope (-0.139, SE 0.089) and the temporal slope (-0.156, SE 0.036) agree.

Red spruce checks: with annual mean temperature added (a proxy for winter warmth) -0.156
(0.036); year FE only -0.087 (0.028); S without N -0.100 (0.018). Raw red spruce relative growth
was 0.68-0.81 in intervals that ended in 2008-2009 and about 1.0-1.15 after 2016 (Figure 4).

All conifers together: -0.027 (SE 0.011). All hardwoods: +0.001 (SE 0.004). **But** hardwoods
that grow on the same plots as red spruce also had a negative slope: -0.060 (SE 0.016). Thus the
response belongs to the site type (spruce-fir forests of the northern Appalachians, Adirondacks
and New England) more than to the species. In the pooled model with one set of state-year
effects, the extra S slope on spruce-fir plots was smaller: -0.0095 (SE 0.0049). Plots north of
42 N: extra slope -0.015 (SE 0.006). Plots in the top initial-S tercile: extra slope +0.011
(SE 0.003), so the response was not larger where S was highest. These heterogeneity tests are
exploratory (we made 4 tests plus the species set) and we did not correct for multiple tests.

## 5. Interpretation

1. For the forest as a whole, the large S decrease of 2000-2025 did not give a measurable change
   in diameter growth or mortality of trees >= 12.7 cm DBH within about 5-20 years. The 95% bound
   for growth is about +/-4% (1-degree clusters) to +/-10% (state clusters) per 6.2 kg decrease.
2. The pooled spatial relation in this region did not predict harm from S, so this null does not
   contradict a working space-for-time transfer. It shows that a spatial S effect on pooled
   growth was not present to transfer.
3. Red spruce is the one clear case where spatial and temporal S slopes agree. This fits the
   known acid-deposition damage to red spruce (calcium loss, winter injury) and its reported
   growth recovery after 2000 (Kosiba et al. 2018, Sci. Total Environ. 637-638:1480-1491).
   The same negative slope for hardwoods on the same plots shows that a site-level change in
   the spruce-fir zone can also explain it. That change can be soil recovery from acid
   deposition, or a local trend that the controls do not remove.

## 6. Limitations

* Ozone is not in the models. Ozone also decreased after 2004 and correlates with oxidized N.
* TDep grids start in 2000. We cannot use deposition of the 1980s-1990s, when acid loads were
  highest, and soil recovery can lag by decades.
* S and N decreased together. In the interval data their correlation is 0.78. Separate S
  and N coefficients have wide CIs.
* The 2003 winter injury of red spruce in New England falls inside the early intervals. Part of
  the red spruce growth increase can be recovery from that event. Its link to acid deposition is
  known but we did not model it.
* FIA public plot coordinates are perturbed by up to about 1.6 km. This adds error to deposition
  and climate at plots and can bias slopes toward zero.
* Diameter growth has measurement error. Trees with "shrank" reconcile codes were kept; trees
  with estimated diameters were removed.
* Mortality is in a linear form (dead / years) without tree size-specific hazard models.
* Species models for 25 species are many tests; 1 to 2 nominal results per sign can occur by
  chance.
* The region does not include the southeastern and Great Lakes states. Results may differ there.

## 7. What remains open

* Add ozone (W126) and base-cation/critical-load exceedance maps to separate soil sensitivity.
* Test the spruce-fir site effect with tree-ring data or with remeasured sites outside FIA.
* Extend to the Great Lakes states (MI, WI, MN) and the Southeast (VA, NC, GA) for an independent
  region. The code takes any FIA state list.
* Use survival hazard models with tree size.

## 8. Files

* `files/figures/fig1_deposition.png`: S deposition maps 2000-2002 and 2020-2022 with plot
  locations; interval-mean S and N by remeasurement year.
* `files/figures/fig2_partial_residuals.png`: binned partial residuals for the spatial and
  temporal growth and mortality models.
* `files/figures/fig3_coefficients.png`: S coefficients over model forms; species spatial vs
  temporal slopes.
* `files/figures/fig4_trajectory.png`: raw interval S and raw relative growth by initial S
  tercile; raw red spruce growth.
* `files/results/main_models.json`: pooled models. `robust_se.json`: 1-degree, 2-degree and
  state clusters. `extra_models.json`: conifer, hardwood and red spruce checks.
  `heterogeneity_models.json`: exploratory interactions. `species_slopes.csv`: 25 species.
  `bins_*.csv`, `trajectory_*.csv`, `deposition_by_interval_end_year.csv`: figure data.
  `sample.json`: sample counts. `input_sha256.txt`: hashes of all raw input files.
* `files/code/`: all code. `run_all.sh` gives the order. `retrieve_data.sh` gets the raw data
  into a scratch folder outside the publication. `fe.py` is a small fixed-effects OLS with
  cluster-robust SEs (alternating projections).
* `files/EXTERNAL_DATA_NOTICE.md`: sources, versions and terms of the external data.

## 9. Reproduction

1. `mkdir -p work && cp -r files/code work/code`
2. Make nClimGrid monthly `nclimgrid_tavg.nc` and `nclimgrid_prcp.nc` available at
   `datasets/noaa-nclimgrid-monthly-{tavg,prcp}-20261006/` (or edit `clim_crop.py`).
3. `bash work/code/run_all.sh`. It downloads about 2.3 GB, then runs all steps. With 2 CPU
   cores the models take about 1 hour. Python 3.12 with numpy, pandas, scipy, pyarrow, xarray,
   netCDF4, rasterio, pyproj and matplotlib.

Species codes: 12 balsam fir, 68 eastern redcedar, 97 red spruce, 126 pitch pine, 129 eastern
white pine, 261 eastern hemlock, 316 red maple, 318 sugar maple, 371 yellow birch, 372 sweet
birch, 375 paper birch, 403 pignut hickory, 407 shagbark hickory, 409 mockernut hickory, 531
American beech, 541 white ash, 621 yellow-poplar, 693 blackgum, 711 sourwood, 762 black cherry,
802 white oak, 806 scarlet oak, 832 chestnut oak, 833 northern red oak, 837 black oak.
