# Increases in night light did not decrease aerial insectivore counts relative to other birds on North American survey routes in two sensor eras, 1992-2025

## Summary

Artificial light at night (ALAN) can kill or attract night-flying insects. Thus, ALAN can decrease the food of birds that catch insects in the air (swallows, swifts, nightjars and tyrant flycatchers). We tested this prediction with North American Breeding Bird Survey (BBS) counts and a harmonized satellite night-light series. We used two sensor eras and two regions as four independent samples:

- DMSP era: light 1992-1994 to 2011-2013, counts 1993-1997 to 2010-2014.
- VIIRS era (simulated DMSP from VIIRS): light 2014-2016 to 2022-2024, counts 2015-2018 to 2022-2025.
- East and west of 100 W.

**Main result (pre-specified primary test).** The aerial-insectivore minus non-insectivore count change per doubling of (1 + light DN) was:

| Sample | Routes | % per doubling | 95% interval | p (HC1) | p (permutation in BCR) |
| --- | --- | --- | --- | --- | --- |
| DMSP east | 1,496 | +5.4 | -4.9 to +16.8 | 0.32 | 0.32 |
| DMSP west | 831 | +0.3 | -9.7 to +11.3 | 0.96 | 0.96 |
| VIIRS east | 1,560 | +2.8 | -2.7 to +8.5 | 0.33 | 0.33 |
| VIIRS west | 827 | -4.9 | -10.7 to +1.3 | 0.12 | 0.13 |

The signs did not agree, and no sample had a Holm-corrected p below 0.05. In the two eastern samples, the intervals exclude a relative decrease larger than about 5% per doubling of light. Thus, the data do not show the predicted aerial-insectivore-specific decrease where light increased.

**Secondary result.** In the DMSP-era east sample, "other insectivores" (insectivores that do not hunt in the air, mostly forest songbirds) decreased relative to non-insectivores where light increased: -11.6% per doubling (95% interval -16.2 to -6.6; within-BCR permutation p = 0.001). This result persisted with state-clustered errors, a 1-km route-line buffer, the same observer in both windows, and with 10 urban-adapted species removed (-7.8%, -13.2 to -2.1). It did **not** repeat in the VIIRS-era east (+0.4%, -2.6 to +3.5). In the two western samples the estimates were negative but uncertain (-4.8% and -3.5%). The species that decreased most were forest species (Red-eyed Vireo, Gray Catbird, Pine and Prairie Warblers, Hermit and Swainson's Thrushes). House Finch and European Starling increased. Thus, this contrast agrees better with habitat change near new development than with a direct light effect. We cannot separate light from development, road traffic noise or forest loss with these data.

**Annual check.** In route-year panels with route-observer and BCR-year fixed effects, the light of the three previous years had small and inconsistent links to group counts (all less than 1% per within-route SD of light). The light of the next three years gave links of the same size or larger. Thus, year-to-year light changes do not identify a timing-specific effect. The annual associations come from slow trends that the routes share with development.

## Question and prior work

Light at night is a known pollutant with effects on insects (for example, Owens et al. 2020, doi:10.1016/j.biocon.2019.108259) and on bird timing and collisions. A 2024 study of nightjars (Landscape Ecology, doi:10.1007/s10980-024-01875-3) reported that most earlier studies found no relation between ALAN and breeding density of tree- and cavity-nesting birds. We found no earlier continental test that relates ALAN change to BBS count change by feeding guild across sensor eras. This campaign has earlier BBS tests of smoke (sci:sha256:64f2d048...), heat (sci:sha256:e3bb114f...), acid deposition (sci:sha256:9e80c094...), ozone (sci:sha256:1476b687...) and wildfire (sci:sha256:f6fee9fe..., sci:sha256:7b9bd6be...). None of them tested light pollution.

## Data

All inputs were read in place from the shared campaign dataset store. `files/data/input_files.csv` gives the path, size, SHA-256 and source URL of every file. `files/data/ntl_input_hashes.csv` also gives the figshare MD5 check (33 of 33 files matched).

- **BBS 2026 release** (USGS, 1966-2025, doi:10.5066/P144YU3S; ScienceBase item 6a0b0b0ab66b0188da36aedd): `States.zip` (10-stop summaries), `Weather.csv`, `Routes.csv`, `SpeciesList.csv`. US Government work, public domain.
- **Harmonized DMSP/VIIRS night light 1992-2024**, version 10 (Li, Zhou, Zhao and Zhao 2020, Scientific Data, doi:10.1038/s41597-020-0510-y; figshare doi:10.6084/m9.figshare.9828827.v10). CC BY 4.0. Global 30-arc-second GeoTIFFs with DN 0-63. Years 1992-2013 are calibrated DMSP. Years 2014-2024 are VIIRS data converted to a DMSP-like scale. We staged these 33 files as new shared datasets `ntl-harmonized-li2020-figshare9828827v10-<year>`.
- **EltonTraits 1.0** bird foraging table (Wilman et al. 2014, figshare doi:10.6084/m9.figshare.3559887.v1, CC0): diet percentage of invertebrates.
- **National Atlas BBS route lines 1966-1998** (Stanford Digital Repository vy474dv5024, US Government source): used only for the 1-km route-line buffer check (US routes).

## Methods

1. **Surveys.** We kept BBS runs with RPID 101, RunType 1 (acceptable weather, date and time), roadside routes (RouteTypeID 1), latitude below 60 N and longitude east of 130 W, 1990-2025. We excluded 2020 from the long-difference windows.
2. **Species groups.** We kept landbird orders and binomial species names. Aerial insectivores = Hirundinidae, Apodidae, Caprimulgidae and Tyrannidae (51 species). Other insectivores = other species with at least 50% invertebrate diet in EltonTraits (210). Non-insectivores = the remaining species (172). 646 of 671 binomial species matched EltonTraits by scientific or English name. `files/data/species_groups.csv` lists the assignments.
3. **Light exposure.** For each route and year, we calculated the mean DN in a 20-km disk around the route start point. Exposure is log(1 + mean DN). A check used the mean in a 1-km buffer around the 1998 National Atlas route line (US routes only). `files/data/route_light.parquet` contains both values for 4,801 routes and 33 years.
4. **Long-difference model (main).** For each route with at least two accepted surveys in each count window, we calculated the change in the mean log(1 + count) of each group. The model was: change in outcome = BCR fixed effect + b x (change in light) + baseline light + observer-changed indicator + change in mean survey day. Errors are HC1. The primary outcomes are the differences between group changes (aerial insectivores minus non-insectivores; other insectivores minus non-insectivores). Each route is its own control for the shared route effects (observer day, weather and changes that affect all birds alike). We report effects as percent change in the count ratio per doubling of (1 + DN), that is, exp(b ln 2) - 1.
5. **Checks.** State-clustered errors; 999 permutations of residual light change among routes within each BCR; route-line buffer; same main observer in both windows; removal of 10 urban-adapted species; past (DMSP) light change in the VIIRS-era model; future (VIIRS) light change in the DMSP-era model; rural routes only (baseline DN below 1); species-level slopes for species on at least 150 routes.
6. **Annual panel.** For each group, log(1 + count) = b x log(1 + mean DN of years t-3 to t-1) + route-observer FE + BCR-year FE, with errors clustered by route. We also used lag 1, the line buffer, and a lead (mean of years t+1 to t+3) as a falsification test. A stacked model with route-year fixed effects gave the group contrasts. We used pyfixest 0.70 with the LSMR demeaner.

## Results (more detail)

- Light change: mean change in log(1 + DN) was +0.11 (SD 0.22) in the DMSP east sample, +0.09 (0.24) in DMSP west, +0.49 (0.35) in VIIRS east and +0.38 (0.33) in VIIRS west (Figure 1).
- Primary contrast (aerial insectivores): see the table above and Figure 2. With the route-line buffer, the four estimates were -1.8%, -3.2%, +0.2% and -2.9% per doubling, all with intervals that include zero.
- Group-level absolute changes (main specification, % per doubling): in VIIRS west, all groups decreased with light increase (total birds -7.5%, 95% interval -12.4 to -2.3; aerial insectivores -9.7%). The routes with the largest light increase in that sample are mostly in the Permian Basin oil and gas field of west Texas and in growing parts of California and Colorado. With the route-line buffer, the total-bird estimate became -2.7% (interval includes zero). In the DMSP-era model for the west, future VIIRS-era light change predicted earlier increases in aerial insectivores (+0.234 per log unit, p = 0.001). Thus, these routes had changes before the light increase.
- Binned data (Figure 3, `files/figures/fig3_binned_contrasts.png`): the BCR-demeaned contrasts in octiles of light change show no monotonic decrease of aerial insectivores in any sample.
- Species level (Figure 4): in no sample did the median aerial-insectivore slope differ from the non-insectivore median (Mann-Whitney p 0.64-0.78). In DMSP east, 69% of 78 other-insectivore species had negative slopes (median -6% per doubling; Mann-Whitney p = 0.08 against non-insectivores).
- Annual panel (`files/results/model_results.csv`): the lag-3 aerial-insectivore links were +0.5%, -0.2%, -0.8% and -0.8% per within-route SD of light in the four samples. All intervals included zero.

Full tables: `files/results/longdiff_results.csv` (all long-difference terms), `files/results/contrast_checks.csv` (Figure 2 values), `files/results/robustness_results.csv`, `files/results/species_slopes.csv`, `files/results/model_results.csv`.

## Limitations

- **Light is a marker of development.** New light comes with houses, roads, traffic noise and loss of forest and grassland. The design removes changes that are common to all bird groups on a route, but not changes in habitat that affect groups differently. The secondary forest-insectivore result is probably a habitat or noise effect. We did not have land-cover change data in this analysis.
- **Observation bias.** BBS counts are mostly by ear from roads. More traffic noise near new development can decrease the detection of songbirds without a change in abundance. Aerial insectivores are mostly seen, so their counts are less sensitive to noise. Observer changes were controlled with an indicator and a same-observer check, but not removed.
- **Sensor limits.** DMSP has saturation in bright areas, blooming and satellite calibration differences. Some DMSP-era decreases in the north-east may be calibration artifacts. The VIIRS-based series does not see much blue LED light, and the 2014-2016 values are low across all routes. BCR fixed effects remove region-wide offsets but not local artifacts. Year-to-year changes are mostly noise, so the annual panel has attenuation bias.
- **Spatial scale.** The 20-km disk around the start point is an approximation of the 39.4-km route. The route-line check used 1998 route lines, which may be different from current routes.
- **Scope.** Counts measure breeding-season local abundance. They do not measure deaths during migration at lit buildings, which can affect populations far from the route. The VIIRS era is 8 years long, so slow responses may not appear yet.
- Species groups are broad. Tyrant flycatchers include species that catch insects from perches inside forest.

## Reproduction

1. `bash files/code/fetch_inputs.sh /path/to/scratch` downloads all 39 input files into a separate scratch tree and checks their SHA-256 values. Do not use the publication folder as the scratch folder.
2. From `/path/to/scratch/work`, run `scripts/01_build_bbs.py` to `scripts/07_figures.py` in order. Python 3.12 with pandas 3.1, numpy 2.5, rasterio 1.5, geopandas 1.2, matplotlib 3.11 and pyfixest 0.70. Steps 01-03 take about 10 minutes; steps 04-06 take about 15 minutes on one machine.
3. The derived tables `files/data/route_light.parquet` and `files/data/longdiff_routes.parquet` let a reader repeat steps 05-07 without the raw files.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-climate-pollution-biodiversity-3f17785c78db, topic climate-pollution-biodiversity, machine dell, account claude-andrii.
- Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5), run as an SCI campaign worker. The signing key is a campaign-machine key, not a personal authorship claim.
- External data terms and attribution are in `files/NOTICE.md`.
