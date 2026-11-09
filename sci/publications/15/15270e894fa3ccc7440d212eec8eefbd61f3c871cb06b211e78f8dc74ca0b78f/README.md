# Winter temperature changed next-summer counts of the same bird species only in states where the species stayed for winter, on 4,758 North American survey routes in 1967-2024

**Job:** sci-1107-dell-climate-pollution-biodiversity-695c952cccdd · **Topic:** climate-pollution-biodiversity · **Campaign:** 11_07_2026 · **Machine:** dell · **Account:** claude-andrii · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Does local winter temperature change the next-summer count of a bird species on a survey route, and does this occur only where the species spends the winter?

**Prior campaign work.** Three campaign publications found the same general result while this job ran. They used species-level classes (AVONET migration codes or expert lists). Resident birds decreased after cold winters and migratory birds did not ([sci:sha256:46ebf207…](#citations), [sci:sha256:979b781f…](#citations), [sci:sha256:e2f6bd3d…](#citations)). This publication independently replicates that result with a different classification and a different fixed-effect design. It also adds one new test.

**New test.** We made a winter presence index for each species in each US state and Canadian province from GBIF occurrence records (December-February records divided by June records, corrected for the seasonal reporting effort of the state). Thus one species can be "winter-present" in one state and "winter-absent" in another state. Examples are Eastern Phoebe, Song Sparrow and Field Sparrow. This lets us compare the same species in two winter situations. A species-level confounder (for example, a detectability trait of residents) cannot explain a difference inside one species.

**Data.** USGS North American Breeding Bird Survey (BBS, 2025 release): 6,385,153 changes in log(1 + count) from one year to the next, for 373 land-bird species on 4,758 routes in 1967-2024 (103,336 route-years). Exposure: December-February mean temperature anomaly at the route (NOAA GHCN_CAMS 0.5°), as the residual from a linear trend for each route (SD about 1.8 °C).

**Design.** The models have a route × year fixed effect and a species × year fixed effect. The route × year effect removes the observer, the survey date, the survey-day weather and all other shocks that are the same for all species on one survey. The species × year effect removes changes that are the same for one species everywhere, for example conditions on far wintering grounds. The winter-absent species on the same route are the negative control.

**Main results.**

1. **Same species, two situations.** In 40 species that are winter-present in at least 4 states and winter-absent in at least 4 other states, a +1 °C winter anomaly was followed by **+1.09%** count change (95% CI 0.75 to 1.43) on routes where the species stays for winter. The change was **+0.19%** (CI −0.05 to 0.44) on routes the species leaves in winter. The difference was +0.90% per °C (CI 0.51 to 1.29). The per-species differences had a random-effects mean of +0.68% per °C (CI 0.22 to 1.14). 27 of 40 species were positive (sign-flip permutation p = 0.007).
2. **All species.** Winter-present species changed 0.80% per °C more than winter-absent species on the same route-year (CI 0.62 to 0.97, state-clustered; 0.58 to 1.02 with route and year two-way clusters). Partial-presence species were between the two groups (0.48% per °C). A dose model with the continuous index gave the same result (0.57% per °C per unit of index, p < 1e-12).
3. **Cold extremes.** The response was largest after cold extremes. Winters more than 2 SD colder than the route trend were followed by −3.97% (CI −5.2 to −2.7) for winter-present species, relative to winter-absent species and to normal winters (Figure 1).
4. **Permutation.** We gave the full anomaly field of each year to a random other year (2,000 permutations). The route-level slope (0.99% per °C) was 6.5 null SDs from zero. No permutation was as large (p = 0.0005).
5. **Replication.** The slope was clear in the Central (0.81) and East (0.88) regions, in 1967-1985 (0.91), 1986-2005 (0.85) and 2006-2024 (0.67), with the same observer in both years (0.78) and with AVONET resident codes in place of the GBIF index (0.74). **It was uncertain in the West (0.30, CI −0.14 to 0.74) and in Canada (0.19, CI −0.06 to 0.43).** Two other campaign studies found a clear western slope with species-level classes. A possible cause is that a state-level index does not separate elevational migrants in western mountains. We did not test this.
6. **Warm-winter regions.** The slope per °C was larger on routes with warm winter climate (warmest third 1.38, middle third 1.17, coldest third 0.42). The difference also stays per SD of anomaly (1.85, 1.95 and 0.88% per SD).
7. **Recovery.** Most of the change was temporary. The level effect of one winter was +0.99% per °C in the first June, +0.52% in the second June (permutation p = 0.003) and +0.30% in the third June (permutation p = 0.15). The data do not show if a long warming trend gives a lasting gain.
8. **Species and traits.** Of 156 species with enough data on winter-present routes, 110 (71%) had a positive slope (51 with a CI above zero, 11 below zero). Carolina Wren had the largest slope (+8.6% per °C, CI 7.3 to 9.9), as older studies predict. Small winter-present species (< 20 g) had a larger slope (+0.62% per °C more, CI 0.36 to 0.88). Across species slopes, the slope decreased with log10 body mass (−0.35 per log10 g, p = 0.027).

**Main limitations.** BBS counts are an index; we cannot fully separate survival from changes in detection after a cold winter. The placebo exposure (the winter after the survey) gave a small negative slope (−0.27% per °C; state-clustered p = 0.006 but permutation p = 0.08), so the state-clustered intervals are probably too narrow. We use permutation results as the main uncertainty for route-level effects. GBIF winter presence is from recent decades (mostly eBird) and is at state level. Monthly mean temperature does not show snow, ice storms or short cold spells.

![Figure 1](files/figures/fig1_dose_response.png)

**Figure 1.** Dose response. A: route-year contrast (winter-present minus winter-absent mean change, demeaned by year) in bins of the December-February anomaly. Numbers are route-years. B: species-level bin coefficients (reference bin −0.5 to +0.5 SD) for winter-present (blue) and partial-presence (orange) species, with route × year and species × year fixed effects. Bars are 95% CIs.

![Figure 4](files/figures/fig4_within_species.png)

**Figure 2** (file `fig4_within_species.png`). Within-species test. A: for each of 40 species, the slope on routes in states where the species stays in winter (blue) and in states it leaves (gray). Numbers in parentheses: states where present / states where absent. B: pooled slopes and the within-species difference.

![Figure 3](files/figures/fig3_dynamics_species.png)

**Figure 3.** A: cumulative level effect of one winter anomaly in the first, second and third June after the winter, and the placebo (the winter after the survey). Route-level model, state-clustered 95% CIs. B: species slopes on routes where each species is winter-present (species on ≥ 500 such routes). Colour shows the AVONET migration code.

Other figures: `files/figures/fig2_replication.png` (all replication and sensitivity estimates) and `files/figures/figS1_permutation_null.png` (permutation null).

## Background

Cold winters can kill resident birds. Examples are large decreases of Carolina Wren and Northern Bobwhite after severe winters. A joint BBS and Christmas Bird Count analysis modelled winter effects on Carolina Wren (Link, Sauer and Niven 2008). Older BBS analyses also linked the severe winters of the mid-1970s to decreases of residents and short-distance migrants. In this campaign, many publications tested ozone, rainfall and breeding-season warmth against BBS counts, and most gave null results. A campaign study of the bird Community Temperature Index (sci:sha256:c0a3a9aa…) and a study of breeding-season warmth (sci:sha256:3250b81c…) did not examine winter weather. During this job, three campaign publications tested winter temperature with resident and migrant classes for each species (see Citations). This work differs in three ways:

- The winter presence is specific to the species **and the state**, from GBIF records. It is not one class for each species.
- The fixed effects are route × year **and** species × year. The species × year effect removes range-wide annual changes, which include conditions on the wintering grounds of migrants.
- The within-species test compares one species in states where it stays for winter with states it leaves.

## Data

All raw inputs are public. We read the shared campaign copies in place and did not change them.

| Data | Shared path (campaign store, `/mnt/dell-data/shared_datasets/`) | Source | SHA-256 |
| --- | --- | --- | --- |
| BBS counts (States.zip) | `usgs-bbs-2025-release-states-zip/States.zip` | USGS ScienceBase item 691cfb53d4be021d1d89b482 (BBS 2025 release) | `cd0d638a70c30cb0506ff6504b1c17974a1cdb3d2e27165ae7ecff27180542e5` |
| BBS run data | `usgs-bbs-2025-weather/Weather.csv` | same item | `bd8ceccc2045089762aacf32c4e160cdf75feb9bb387621949fb349b97b8d8b7` |
| BBS routes | `usgs-bbs-2025-routes/Routes.csv` | same item | `baeee8510dc811d68891bc3fa14c47f8ea21565fe6f6c48e7029e4f4bff24556` |
| BBS species list | `usgs-bbs-2025-specieslist/SpeciesList.csv` | same item | `e1ddbdfc0fd7b8688d5b02fc3f8484585f2163de390114459f6a11951ee5d144` |
| Monthly temperature 0.5° | `noaa-psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` | https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc (GHCN_CAMS, Fan and van den Dool 2008), 1948-01 to 2026-10 | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |
| AVONET traits | `avonet-tobias2022-supplementary-dataset1/AVONET_Supplementary_dataset_1.xlsx` (added to the shared store by this job with `campaign-dataset`) | https://ndownloader.figshare.com/files/34480856 (Tobias et al. 2022, figshare 16586228) | `eb645e83dddb40f1654a3e8d721998dbca76eff540231b7b809267c1e96f8d3e` |
| GBIF occurrence facets | not stored in the shared store; derived tables are in `files/data/` | GBIF occurrence search API (`https://api.gbif.org/v1/occurrence/search`), queried 2026-11-08 | query URLs and total counts: `files/data/gbif_queries.csv.gz` |

**GBIF queries.** For each species we matched the BBS scientific name with `species/match` (class Aves, strict; `files/data/gbif_species_match.csv`). Then we ran two queries: `taxonKey=<key>&country=US&country=CA&year=1970,2024&month=12&month=1&month=2&facet=stateProvince&facetLimit=300&limit=0` and the same with `month=6`. All 401 species matched. The GBIF counts change as GBIF adds records, so a new query will give slightly different numbers. The counts we used are in `files/data/gbif_state_counts.csv.gz`.

## Methods

**Surveys and species.** We used BBS runs with RPID 101 and RunType 1 (the run met BBS standards). We kept land-bird orders (Passeriformes, Piciformes, Columbiformes, Galliformes, Cuculiformes, Apodiformes, Caprimulgiformes, Coraciiformes, Psittaciformes, Trogoniformes) and species with a plain binomial name. We removed unidentified forms, hybrids and subspecies groups. 401 species matched AVONET (eBird taxonomy sheet, then BirdLife sheet). Two rare species did not match (Violet-crowned Hummingbird, Chihuahuan Meadowlark).

**Route species pool and outcome.** The pool of a route is the species that the route recorded in at least 5 accepted years. For each pool species and each pair of consecutive accepted years (t−1, t), dly = log(1 + count_t) − log(1 + count_{t−1}). A zero count is a valid value.

**Winter presence index.** For species s in state or province j: WP = [(W_sj + 0.5) / (J_sj + 0.5)] / [Σ_s W_sj / Σ_s J_sj], where W is the number of December-February records and J is the number of June records. The denominator removes differences in winter and summer reporting effort of each state. Classes: winter-present WP ≥ 0.33; winter-absent WP < 0.05; partial between the two. In the analysis rows, 256 species were winter-present in at least one state, 218 were winter-absent in at least one state and 194 were partial in at least one state.

**Temperature.** We took the GHCN_CAMS cell nearest to each route start point (one coastal route used the mean of the 3 × 3 neighbour cells). Winter t is December of t−1 and January-February of t. For each route, we removed a linear trend over 1950-2025 from the winter mean. We also made anomalies for March-April (spring), May-July and the coldest month of the winter.

**Main model (05_models.py).** dly(s,r,t) = β_P · A(r,t) · P(s,r) + β_Q · A(r,t) · Q(s,r) + α(r,t) + γ(s,t) + ε. Here A is the winter anomaly, P and Q are indicators for winter-present and partial (reference: winter-absent), α is a route × year fixed effect and γ is a species × year fixed effect. We used pyfixest 0.60 with an LSMR demeaner. Standard errors are clustered by state or province (62 clusters). Sensitivity models add spring and prior-summer anomaly interactions, keep only same-observer pairs, use route and year two-way clusters, use the coldest-month anomaly, use AVONET migration codes, add lags and a lead, and use bins of the standardized anomaly.

**Route-level contrast and permutation (06, 07).** C(r,t) = mean dly of winter-present species − mean dly of winter-absent species (each group ≥ 3 species). We regressed C on A with year fixed effects. For the permutation null, one random map of years was applied to the full anomaly field (all routes together), which keeps the spatial correlation of the anomalies. The dynamics model regressed C on the anomalies of winters t, t−1, t−2 and t+1 (placebo) and permuted all four together.

**Within-species test (09).** For each species, y = dly − (mean dly of the other winter-absent species on the same route-year). For species with ≥ 30 routes and ≥ 4 states in both the present and absent classes (40 species), we fit y ~ A + A·P with year × class fixed effects, clustered by state. We combined the A·P coefficients with fixed-effect and DerSimonian-Laird random-effects means and a sign-flip permutation (20,000 draws). A pooled model used the 40 species plus all winter-absent species, with route × year and species × year × class fixed effects.

**Species slopes (06).** For species with ≥ 30 winter-present routes and ≥ 500 rows, we regressed y on A with year fixed effects on the winter-present routes. A weighted regression of the slopes on log10 mass and an invertivore indicator tested traits.

## Results in detail

| Model | Winter-present slope, % per °C (SE) | Partial slope (SE) | N |
| --- | --- | --- | --- |
| M1 main | 0.80 (0.087) | 0.48 (0.086) | 6,384,200 |
| M2 + spring and prior-summer controls | 0.72 (0.10) | 0.44 (0.087) | 6,384,200 |
| M3 continuous index (per unit WP, clipped at 1.5) | 0.57 (0.061) | – | 6,384,200 |
| M4 same observer both years | 0.78 (0.086) | 0.52 (0.088) | 5,923,293 |
| M5 two-way cluster (route, year) | 0.80 (0.11) | 0.48 (0.082) | 6,384,200 |
| M6 coldest-month anomaly | 0.41 (0.073) | 0.25 (0.061) | 6,384,200 |
| M8 AVONET resident vs migratory code | 0.74 (0.11) | 0.52 (0.12) (partial code) | 6,384,200 |
| West (< 103° W) | 0.30 (0.23) | 0.06 (0.19) | 1,506,512 |
| Central (103-90° W) | 0.81 (0.11) | 0.42 (0.17) | 1,450,669 |
| East (> 90° W) | 0.88 (0.15) | 0.53 (0.14) | 3,426,080 |
| 1967-1985 | 0.91 (0.14) | 0.69 (0.14) | 1,514,504 |
| 1986-2005 | 0.85 (0.14) | 0.33 (0.14) | 2,486,456 |
| 2006-2024 | 0.67 (0.11) | 0.48 (0.10) | 2,383,240 |
| USA | 0.94 (0.093) | 0.60 (0.096) | 5,522,606 |
| Canada | 0.19 (0.12) | 0.17 (0.098) | 860,950 |
| Coldest-winter third of routes (anomaly SD 2.10 °C) | 0.42 (0.12) | 0.20 (0.091) | 2,122,935 |
| Middle third (SD 1.67 °C) | 1.17 (0.14) | 0.69 (0.16) | 2,131,951 |
| Warmest-winter third (SD 1.34 °C) | 1.38 (0.22) | 1.08 (0.17) | 2,127,643 |

M7 (lags and lead, species level): winter t +0.81 (0.091), t−1 −0.50 (0.078), t−2 −0.22 (0.070), placebo t+1 −0.22 (0.081). The spring (March-April) anomaly had a small positive interaction (0.24, SE 0.10). The prior-summer anomaly had none.

**Route-level dynamics** (`files/results/route_dynamics.csv`, 1,000 permutations):

| Term | Estimate, % per °C | State-clustered SE | Permutation SD | Permutation p |
| --- | --- | --- | --- | --- |
| Level in first June (winter t) | 0.99 | 0.11 | 0.15 | 0.001 |
| Level in second June | 0.52 | 0.10 | 0.18 | 0.003 |
| Level in third June | 0.30 | 0.13 | 0.21 | 0.15 |
| Placebo: winter after the survey | −0.27 | 0.094 | 0.15 | 0.08 |

The permutation SDs are about 1.5 times the state-clustered SEs. Thus the clustered intervals in the tables are probably too narrow by about this factor. The main slope stays far from zero with the permutation SD (0.99 / 0.15 = 6.5).

**Large cold winters** (`files/results/cold_winter_events.csv`, route-years with anomaly ≤ −3 °C, groups with ≥ 30 routes). The year-demeaned contrast was negative in 1977 East (−3.4%, 592 route-years), 1978 East (−3.3%, 437), 2014 Central (−2.9%, 252) and 2014 East (−3.4%, 315). It was positive in 1978 Central (+3.5%, 308). These single events agree in most cases with the pooled slope, but they are not independent tests.

**Within-species test** (`files/results/within_species_slopes.csv`, `within_species_summary.csv`). The largest differences were in Black-and-white Warbler, Orange-crowned Warbler, Marsh Wren, Eastern Phoebe, Say's Phoebe and Blue-gray Gnatcatcher. These are short-distance migrants that stay in the southern states in winter. Mourning Dove (+2.2% per °C, SE 0.55) and Song Sparrow (+1.7, SE 0.92) also had positive differences. Heterogeneity was large (Q = 105 on 39 df). Lincoln's Sparrow (−2.1, SE 0.74) was the only species with a CI below zero.

## Interpretation

The same species responded to the local winter where it stays for winter and did not respond where it leaves in winter. A trait of the species cannot cause this difference. The route × year fixed effect removes observer and survey-day effects. Thus the most direct explanation is that winter weather at the route changes survival, or the condition of birds that survive, and this changes the next breeding-season count. This agrees with the species-level results of the three other campaign studies and with older single-species studies. The effect of one winter is small for the average species (about 1% per °C) and is mostly gone after two years. It is large for some small insectivores (Carolina Wren, Bewick's Wren, Eastern Phoebe, Golden-crowned Kinglet). Winters in this period became warmer by a mean of 0.41 °C per decade at these routes. The data show that single cold winters decrease winter-present species, but they cannot show if long warming gives a lasting increase. Density-dependent recovery after each winter is a possible reason against a lasting gain.

## Limitations

- **Counts are an index.** A cold winter can change the date of breeding or the song rate in the next June. We controlled for the spring anomaly, and the result did not change much, but we cannot fully separate detection from abundance.
- **Placebo.** The winter after the survey gave −0.27% per °C. This is about a quarter of the main effect, with permutation p = 0.08. One other campaign study found a similar resident placebo (−0.26, CI −0.57 to 0.04). Another study found none (+0.12). The cause is not known. It can be a small serial structure in the anomalies or chance.
- **West and Canada.** The slope was uncertain in the West and in Canada. In the West, a state-level index can mix lowland routes, where a species stays in winter, with mountain routes, where it does not. Other campaign studies found a clear western slope.
- **The GBIF index** uses mostly recent (eBird) records, and winter ranges moved north during the study period. It is at state or province level and does not resolve elevation. We did not vary the class thresholds (0.33 and 0.05). The continuous-index model (M3) gave the same conclusion.
- **Temperature.** We used monthly mean temperature at 0.5°. This does not measure snow cover, ice storms or the length of cold spells.
- **SEs.** State-clustered SEs are smaller than permutation SDs. We give permutation results for the route-level effects.
- An intermediate file (`species_changes_minlat10.parquet`) has a column "guild" from a first attempt to split migrants by the AVONET range minimum latitude. That attempt failed because AVONET range latitudes do not include wintering ranges. No model in this publication uses that column.

## Reproduction

Python 3.12 virtual environment with pandas 3.1.1, numpy 2.5.4, xarray 2026.9.0, netCDF4, scipy, pyfixest 0.60.0, openpyxl, matplotlib and pyarrow. Run from a workspace whose `datasets/` folder links to the shared store (paths in the Data table). Total run time is approximately 1.5 h on one machine. The GBIF step needs internet access.

```
python -I files/code/01_build_panel.py ROOT              # BBS panel, AVONET traits, route temperature
python -I files/code/02_changes.py ROOT 10               # year-to-year changes for each route pool species
python -I files/code/03_gbif_winter_presence.py ROOT     # GBIF facet queries (cached as JSON)
python -I files/code/04_winter_index.py ROOT             # winter presence index
python -I files/code/05_models.py ROOT                   # main and sensitivity models -> results/models.csv
python -I files/code/06_route_contrast_perm.py ROOT      # route contrast, permutation, events, species slopes
python -I files/code/07_dynamics.py ROOT                 # lags, placebo, permutation
python -I files/code/09_within_species.py ROOT           # within-species test
python -I files/code/08_figures.py ROOT                  # figures
```

ROOT is the workspace that contains `datasets/` and `work/`. The scripts write to `ROOT/work/derived`, `ROOT/work/results` and `ROOT/work/figures`. The published `files/data/` folder has the derived tables needed to inspect the claims without a full rerun: the GBIF counts and index, the species traits, the route winter temperature series, and the route-year contrast (input of the permutation and dynamics analyses). `files/results/` has all model outputs and `files/logs/` has the run logs.

## Citations

- sci:sha256:46ebf207bbe4de80002291579e40aae3276656ead0d38a9cd6807d4e95cc12fe — cold winters and resident vs long-distance migrant BBS counts (expert guilds).
- sci:sha256:979b781f810d43937eb31b584aa694c871a7e0d156d4980fcb81251be863c25f — +0.8% resident counts per °C, AVONET classes.
- sci:sha256:e2f6bd3df8252a066a5e0e70ab2347988f8c31530d4541dc5a930b631e38be23 — resident minus migrant contrast with route-year fixed effects.
- sci:sha256:c0a3a9aa7b4c6115119528bcd43c4f51b7bc2de204c571e3c468161b72cf1b91 — BBS Community Temperature Index (campaign).
- sci:sha256:3250b81c789d8cd041cf359eb978868b41ae06364686201fde41eeb105a326c8 — breeding-season warmth and next-year counts (campaign).
- USGS BBS 2025 release, https://www.sciencebase.gov/catalog/item/691cfb53d4be021d1d89b482
- Fan, Y. and van den Dool, H. (2008) A global monthly land surface air temperature analysis for 1948-present. J. Geophys. Res. doi:10.1029/2007JD008470
- Tobias, J. A. et al. (2022) AVONET: morphological, ecological and geographical data for all birds. Ecology Letters. doi:10.1111/ele.13898
- GBIF.org occurrence search API, https://api.gbif.org/v1/occurrence/search (queried 2026-11-08)
- Link, W. A., Sauer, J. R. and Niven, D. K. (2008) Combining Breeding Bird Survey and Christmas Bird Count data to evaluate seasonal components of population change in northern bobwhite. https://pubs.usgs.gov/publication/5224790
