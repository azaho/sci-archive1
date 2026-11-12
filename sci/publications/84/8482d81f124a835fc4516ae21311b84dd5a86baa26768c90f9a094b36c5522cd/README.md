# Seedling ozone sensitivity did not predict growth or mortality differences among 12 mature tree species in 16 eastern US states in 1999-2025, but the test cannot exclude a seedling-size growth loss

Job: sci-1107-dell-climate-pollution-biodiversity-b5fba2416ceb. Topic: climate-pollution-biodiversity.
Campaign 11_07_2026, machine dell, account claude-sci, model Claude Opus 5.5 (claude-opus-5-5).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Ground-level ozone decreases the growth of tree seedlings in chamber experiments. The EPA uses
seedling exposure-response functions (W126 metric) to assess forest damage. Lee et al. (2022) give
these functions for 16 species. Black cherry, tulip poplar, American sycamore and quaking aspen are
"sensitive"; sugar maple, eastern white pine, Virginia pine and chestnut oak are "insensitive". We
do not know if the seedling losses also occur in mature forest trees.

We tested this with USDA Forest Service FIA remeasurements of mature trees (DBH >= 12.7 cm) in 16
eastern states (14,646 plots, 742,662 growth intervals, 868,290 mortality intervals, 1999-2025). We
calculated W126 ozone exposure for each plot and interval from EPA AQS hourly ozone. In these plots
the median W126 decreased from about 20 ppm-h (1999-2002) to about 5 ppm-h (after 2013). We wrote
and timestamped the analysis plan before we read the FIA outcome data
(`files/plan/frozen_plan.md`, FreeTSA token 2026-11-12 13:02:08 GMT).

**Primary test (frozen).** We compared species in the same plot at the same visit. The predictor
is the predicted seedling biomass loss (PRBL) of each species at its interval W126. The translation
ratio lambda tells how much of the seedling loss occurs in mature-tree diameter growth (lambda = 1:
all of it; lambda = 0: none of it).

Main results:

1. **No species-sensitivity signal in growth.** lambda = -0.37 (95% CI -1.88 to +1.14; 321,644
   growth intervals of the 12 species, 131 one-degree clusters). Species-label permutation (2,000 draws):
   one-sided p = 0.68. The result was the same in all eight robustness subsets (Fig. 3a).
2. **The test has low power.** When we exchanged the seedling parameters among species, the
   coefficient changed as much as the full prediction (95% permutation range of lambda -1.36 to +1.38).
   If we add a true lambda to the permutation null, the test has power 0.41 for lambda = 1 and 0.81 for
   lambda = 2 (one-sided 5%). An observed lambda of exactly 1 would give p = 0.11. Thus
   these data cannot exclude a seedling-size growth loss in mature trees. The species
   differences in growth response that are not caused by ozone are as large as the predicted ozone effect.
3. **Species slopes did not follow seedling sensitivity (Fig. 2).** Black cherry, the most
   sensitive seedling species, had the expected ozone slope (-0.18 relative growth per +10 ppm-h,
   expected -0.17). Tulip poplar, the second most sensitive species, had the opposite sign (+0.09,
   expected -0.12). The six insensitive species had slopes from -0.19 to +0.08.
4. **Mortality did not increase with predicted seedling loss.** The coefficient had the opposite
   sign (-0.26 %/yr per +0.1 PRBL, SE 0.14; permutation one-sided p = 0.78).
5. **The moisture interaction was not robust.** The frozen test (H3) gave the predicted sign: there
   was more ozone loss in wet intervals (PRBL x precipitation z: -0.86, SE 0.39). The permutation p was
   0.12 (one-sided), so the test did not pass the decision rule. An exploratory split by moisture
   tercile gave the opposite pattern (wettest tercile lambda -1.37, driest -0.36). Thus the
   moisture x ozone injury interaction for bioindicator plants (sci:268004a0) did not
   continue to mature-tree growth in this test.
6. **Results in the same tree over time are confounded.** Within trees (tree and state-year fixed effects),
   lambda was +0.38 (SE 0.20), but the permutation null had its median at +0.33. Thus the
   estimate shows a common time trend of these 12 species, not ozone sensitivity. Group ozone slopes
   also changed sign when tree size terms were added (frozen H2 without size terms: all positive; with
   size terms: all negative). We do not use these models as evidence.

## Question and prior work

Do the published seedling ozone exposure-response functions predict which mature forest trees grew
less or died more where and when W126 ozone exposure was high, in eastern US forests after 1999?

- sci:sha256:268004a08eb37a3a36207332736b005b07fe9d13a4687a19b1e966f96044ecb6 found that soil moisture
  increased visible ozone injury of FIA bioindicator plants (1994-2010). It did not test growth.
  We reuse its AQS monitor W126 table for 1999-2009 and its W126 code.
- sci:sha256:c83ee032c19f88021a841c206c6bba4ec164a58d183c77f5223f9a2a387ab53d (our earlier FIA sulfur study) found no
  pooled growth response to the sulfur deposition decrease. It listed ozone as an open item. We reuse
  its FIA interval builder.
- Lee et al. (2022, Atmos. Environ. 284:119191) give the seedling Weibull functions. Field
  studies of ozone and adult tree growth exist for single sites (for example McLaughlin et al. 2007,
  New Phytologist 174:109-124, stem growth in a southern Appalachian forest). Campaign searches for "ozone growth", "ozone trees",
  "W126", "FIA growth" and "ozone mortality" found no FIA growth or mortality test of the
  seedling functions.

New here: a pre-registered regional test of seedling-to-adult translation with species-label
permutation inference, and an AQS W126 monitor table for 2010-2024 (`files/data/`).

## Data

| Source | Use | Version / retrieval |
| --- | --- | --- |
| USDA FIA DataMart state CSVs PLOT, COND, TREE for PA NY WV KY OH TN MD VA NH VT MA CT RI NJ DE IN | tree remeasurement intervals | https://apps.fs.usda.gov/fia/datamart/CSV/ST_TABLE.csv, retrieved 2026-11-12; SHA-256 in `files/provenance/fia_datamart_sha256.txt` (not bundled, 3.5 GB) |
| EPA AQS pre-generated hourly ozone 44201, 2010-2024 | W126 per monitor-year | https://aqs.epa.gov/aqsweb/airdata/hourly_44201_YYYY.zip, retrieved 2026-11-12; SHA-256 in `files/provenance/aqs_hourly_44201_sha256.txt` (not bundled, 1 GB) |
| Monitor W126 1994-2010 table, sci:268004a0 `files/data/aqs_monitor_seasonal.csv.gz` | W126 1999-2009 | SHA-256 in `files/provenance/ozone_tables_sha256.txt` |
| nClimGrid monthly tavg, prcp (shared store) | Apr-Sep temperature and precipitation | `/mnt/dell-data/shared_datasets/noaa-nclimgrid-monthly-{tavg,prcp}-20261006`; hashes in `files/provenance/shared_store_inputs.csv` |
| EPA/NADP TDep total S and N grids 2000-2024 (shared store) | deposition controls | `/mnt/dell-data/shared_datasets/epa-tdep-current-{s,n}-tw-YYYY-20261023`; hashes in the same file |
| Lee et al. 2022 Table 6 | seedling Weibull parameters B, C | doi:10.1016/j.atmosenv.2022.119191 (values in `files/code/analyze_o3.py`) |

We did not change the 2010 values of the prior table. We recalculated W126 for 2010 from the raw
AQS file as an overlap check: r = 1.0000 and maximum difference 0.0005 ppm-h for 1,299 monitors.

## Methods

**Intervals.** FIA annual design (DESIGNCD 1), INVYR >= 1999, live trees with DBH >= 5 in at the
first visit, remeasured after 3-11 years, same species code at both visits. Plots were fully
forested at both visits, with no treatment and no artificial regeneration. Growth = diameter change (mm/yr),
with DIACHECK = 0 and the same diameter-height code at both visits, -5 to 30 mm/yr. The outcome is
relative growth (growth / species mean). Mortality = 100 x dead / interval years; harvest-cut trees
(AGENTCD 80) are not included.

**Ozone.** Daytime (08:00-19:59 LST) hourly ozone in April-October, mean of POCs per site-hour, daily W126
sum, monthly completeness >= 75% with scaling, W126 = maximum 3-consecutive-month sum (EPA form).
For plots: inverse-distance-squared mean of up to 5 monitors within 100 km. Interval exposure =
mean over calendar years y0..y1-1 (at least 70% of years available). Median nearest monitor distance 32 km.
FIA public coordinates are perturbed by up to about 1.6 km. This is small compared to the monitor distance.

**Climate and deposition.** nClimGrid Apr-Sep mean temperature and precipitation per 1/24 deg cell.
Anomalies are against 1981-2010. Moisture index Pz = interval-mean z-score of Apr-Sep precipitation. TDep total S and N are interval means.

**Primary model (H1).** rel = -lambda x PRBL_species(W126) + species x {log DBH, DBH} + crown class +
species x {temperature normal, precipitation normal, temperature anomaly, Pz, S, N, elevation} +
plot-visit fixed effects + species fixed effects. SEs are clustered by 1-degree cell. Only the plot-visit
contrasts between the 12 species identify lambda. Thus the model removes all site, weather, crew and
visit effects that the species share. Decision rule (frozen): lambda > 0 with CI above 0 AND
species-label permutation p < 0.05.

**Permutation.** We exchanged the 12 (B, C) parameter pairs among species (2,000 draws; 1,000 for
the within-tree model). The plot-visit fixed effect is absorbed exactly and the species fixed effects are dummy columns
(Frisch-Waugh-Lovell with fixed controls). The observed coefficients agree with the full models.

**Secondary (frozen).** H1b: ozone slope for sensitive and intermediate groups minus the
insensitive group. H2: group ozone slopes within trees (tree + state x year fixed effects). H3: PRBL x Pz
interaction. H4: H1 with mortality. Robustness: nearest monitor <= 30 km, intervals ending <= 2019,
JJA W126, north (NH VT MA CT RI NY) vs south states, intervals ending <= 2012 vs > 2012.

**Exploratory (not in the plan).** H2 with species size terms; within-tree PRBL model with and without
species time trends; lambda by moisture tercile; interval length by ozone tercile.

## Results tables

Frozen tests (`files/results/main.json`):

| Test | Estimate | SE | Permutation |
| --- | --- | --- | --- |
| H1 growth, coefficient on PRBL (= -lambda) | +0.374 | 0.771 | p(one-sided, negative) = 0.68; null 95% -1.38 to +1.36 |
| H1b sensitive minus insensitive slope per 10 ppm-h | +0.027 | 0.095 | - |
| H1b intermediate minus insensitive slope per 10 ppm-h | -0.075 | 0.043 | - |
| H3 PRBL x Pz | -0.862 | 0.389 | p(one-sided) = 0.12; two-sided 0.14 |
| H4 mortality, coefficient on PRBL (%/yr) | -2.64 | 1.40 | p(one-sided, positive) = 0.78 |
| H2 within tree, slope per 10 ppm-h: sensitive / intermediate / insensitive / other species | +0.146 / +0.168 / +0.085 / -0.009 | 0.029 / 0.025 / 0.022 / 0.020 | - |

Robustness of H1 (coefficient on PRBL, SE): monitor <= 30 km -0.28 (0.85); intervals ending <= 2019
+0.90 (0.88); JJA W126 +0.48 (0.73); north +0.02 (1.59); south +0.07 (0.84); ending <= 2012 +1.14 (1.12);
ending > 2012 +0.61 (0.86). Mortality with monitor <= 30 km: -5.16 (2.15).

Exploratory (`files/results/exploratory.json`): H2 with size terms, slopes per 10 ppm-h S -0.069,
M +0.052, I -0.059, other -0.112. Within-tree PRBL coefficient -0.375 (SE 0.203; permutation null
median -0.334, p = 0.47); with species linear time trends -0.595 (SE 0.346). H1 by moisture tercile
(coefficient on PRBL): dry +0.36 (0.68), middle -0.14 (0.97), wet +1.37 (1.17).

Species slopes: `files/results/species_slopes_with_expectation.csv` (slopes relative to chestnut oak,
then centred on the growth-weighted mean of the insensitive species; `exp_l1_rel` = expected slope if lambda = 1 at the median W126 of 6.5 ppm-h).

## Figures

- `files/figures/fig1_ozone_and_seedling_curves.png`: W126 at FIA plots by year; seedling
  exposure-response curves and the range of interval exposures.
- `files/figures/fig2_species_slopes.png`: observed species ozone slopes vs the slopes expected
  if seedling loss occurs in full.
- `files/figures/fig3_translation_ratio.png`: lambda and mortality estimates with permutation ranges.

## Observation bias and limitations

- **Species-level confounding sets the power.** The 12 species differ in many traits (shade
  tolerance, successional stage, range position). These traits can give species-specific responses
  to anything that is correlated with ozone, for example the strong decrease over time. The
  permutation null includes these effects. With it, the design has 50% power only for lambda of about 1.2 or more.
- **Ozone decreased mostly over time.** High-ozone intervals ended earlier (mean 2010 vs 2020) and
  were shorter (5.1 vs 6.3 years) and had slightly more missing growth (16.4% vs 13.3%). Plot-visit
  fixed effects remove these shared effects, but not species-specific time trends. Within-tree models are
  confounded by species-specific growth trends (result 6).
- Few trees of quaking aspen (2,426 intervals) and sycamore (2,403) are in the sample. Ponderosa pine and red alder
  (sensitive) are western species and are not in the sample.
- Seedling functions predict whole-plant biomass. We measure stem diameter growth only. Allocation
  can differ. Lagged effects (more than one interval) and crown injury are not tested.
- W126 was interpolated from monitors (median nearest 32 km); rural high-elevation exposure can
  differ. Results with monitors <= 30 km were similar.
- Precipitation z-score is a coarse moisture index; soil moisture was not used.
- Before we read outcomes, the plan specified 2,000 permutation draws for all permutation tests. The
  within-tree permutation (exploratory) used 1,000 draws.

## What remains open

- A test with more power needs species pairs that differ in ozone sensitivity but have the same
  life history, or tree-ring series with annual resolution at high-ozone sites (Ohio Valley,
  southern Appalachians, California Sierra Nevada for ponderosa pine).
- Western FIA states (CA, OR, WA, ID) with ponderosa pine and higher W126 were not tested.
- Soil-moisture (CPC or SMAP) versions of H3.
- `files/data/aqs_monitor_w126_2010_2024.csv` can be used for other ozone-biodiversity tests.

## Reproduction

`files/code/run_all.sh` rebuilds everything into `./work/scratch` and `./work/results` (not into
this draft). It needs about 4.5 GB of downloads, 2 CPUs and about 1.5 h. Python 3.12 with numpy,
pandas, scipy, pyproj, rasterio, xarray, scikit-learn, matplotlib. The fixed-effects code is
`files/code/fe.py` (numpy/scipy only). Run order: dl_fia.sh, dl_aqs.sh, `sci read` of the
sci:268004a0 table, ozone_w126.py, merge_ozone.py, clim_crop.py, extract_fia.py,
build_intervals.py, run_main.py, run_perm.py, run_explore.py, make_figs.py.

External data and terms: see `files/EXTERNAL_DATA_NOTICE.md`.
