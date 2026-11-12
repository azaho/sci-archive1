# Tree seedlings in eastern US forests followed about 58% of their spatial temperature slope in 1999-2025, saplings and adults under 25%; the seedling shift did not follow local or regional warming

Job: sci-1107-dell-climate-pollution-biodiversity-f71f335d5a0d. Topic: climate-pollution-biodiversity. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work found that community thermal composition follows only a small part of its spatial temperature gradient in time: about 12% in 75 monitoring networks (sci:sha256:0037934e), less than 10% in North American birds, and about 14% in British butterflies with European niche indices (sci:sha256:814f6d39). The gap is in species membership (sci:sha256:3f5200e4). Bird colonisation is limited by colonist supply beyond about 100 km (sci:sha256:79a502af). The processes that set the gap are not known in general.

Trees give a direct test of one candidate process, demographic inertia. A tree community has layers with very different turnover times. Seedlings turn over in a few years. Saplings turn over in decades. Adults turn over in a century or more. If longevity sets the gap, the seedling layer must follow its spatial slope at near full strength, and the adult layer must not. If establishment or seed supply sets the gap, the seedling layer must also follow little.

We asked:

1. Which fraction of its own spatial temperature slope does each layer (seedlings, saplings, adults) follow in time?
2. Does the shift in each layer follow local or regional differences in warming?
3. Which species and which demographic flows (ingrowth, natural mortality, harvest) make the change?

## 2. Data

- USDA Forest Service Forest Inventory and Analysis (FIA) DataMart, state CSV files PLOT, COND, TREE and SEEDLING for 31 eastern states (ME NH VT MA CT RI NY NJ PA DE MD WV VA NC SC GA FL AL MS TN KY OH IN IL MI WI MN IA MO AR LA), and REF_SPECIES. Downloaded 2026-11-11 from https://apps.fs.usda.gov/fia/datamart/CSV/. The file `files/data_provenance.csv` gives the URL, byte count and SHA-256 of each of the 125 files that we used.
- NOAA NCEI nClimGrid monthly mean temperature (`nclimgrid_tavg.nc`, file dated 2026-10-06, SHA-256 b781f5ee586c1b9de5334a65453bb6e6888da43c959ba8d306f2d1e7f59d83c7). We used the shared campaign copy `datasets/noaa-nclimgrid-monthly-tavg-20261006/nclimgrid_tavg.nc`.

Sample: annual-inventory visits (INVYR 1999 or later, KINDCD 1-3, QA_STATUS 1, sampled forest plot) with at least 90% of the plot area and microplot area in natural forest (COND_STATUS_CD 1, STDORGCD not 1) and no planted condition. This gives 209,534 visits on 64,508 plots, measured 1999-2025 (median 4 visits per plot). Plot baseline temperature (1981-2010 annual mean at the nearest nClimGrid cell) is -1.7 to 25.5 C (median 11.4 C).

Layers:

- Seedling: SEEDLING table (stems under 1 inch diameter; conifers at least 6 inches tall, hardwoods at least 12 inches tall), four microplots of 1/300 acre.
- Sapling: live trees with diameter 1.0-4.9 inches (microplots).
- Adult: live trees with diameter of 5 inches or more (subplots).
- Flows between visits: ingrowth (live adults with RECONCILECD 1 or 2), natural mortality (STATUSCD 2, live at the previous visit, AGENTCD not 80), harvest (STATUSCD 2, live at the previous visit, AGENTCD 80).

## 3. Methods

The analysis plan (`files/analysis_plan.md`) was written before we calculated a community index. Section 6 lists the tests that we added later.

- Species temperature index (STI): the mean baseline temperature of the first-visit plots where the species occurs as an adult. We calculated STI in two random halves of the plots (by plot identifier) and applied each STI to the other half (cross-fitting). Species need at least 30 plots in the STI half. 141 taxa have an STI.
- Community temperature index (CTI): the mean STI of the taxa present in a layer at a visit (main index). Secondary indices: abundance weights (stems per acre for seedlings and saplings, basal area for adults), genus-level STI, and 81 "core" species (species-level codes, adult on at least 1% of plots).
- Spatial slope b: the slope of first-visit CTI on baseline temperature, inside 2-degree latitude-longitude blocks (main) and pooled over all plots.
- Temporal trend: the within-plot slope of CTI on measurement year (plot fixed effects), in C per decade. The temperature trend is the within-plot slope of the 10-year trailing mean temperature before the measurement year, on the same visits.
- Tracking ratio R = CTI trend / (b x temperature trend). R = 1 is a full space-for-time response. R = 0 is no response.
- Local-warming test: change of CTI between consecutive visits on change of trailing temperature, with 4-degree block x measurement-year effects; slope divided by b.
- Regional-warming test: across 2-degree blocks with at least 30 plots, the block CTI trend on the block temperature trend, with block baseline temperature as a control, weighted by plot number; slope divided by b.
- Long-term warming offset: the plot mean of (seedling CTI - adult CTI) on 1951-1980 to 1996-2025 warming, inside 4-degree blocks, with baseline temperature and stand age as controls.
- Stand ageing adjustment: the within-block cross-sectional slope of first-visit CTI on recorded stand age (with baseline temperature), multiplied by the within-plot trend of stand age, is removed from the CTI trend.
- Seed source: seedling CTI on same-visit adult CTI and baseline temperature, inside 2-degree blocks.
- Species contributions: an exact split of the within-plot presence CTI trend into species terms q_s = I_s (STI_s - plot mean CTI) / S. A positive term for a cool species means that the species became less frequent.
- Year path: plot + year two-way fixed effects for CTI and trailing temperature.
- Uncertainty: 95% intervals from 200 bootstrap draws of 2-degree blocks (101-118 blocks).

## 4. Results

### 4.1 Spatial gradients are strong in all layers

All three layers sort by temperature in space at almost the same slope (Figure 1a). Inside 2-degree blocks, b = 0.65 (0.59-0.71) for seedlings, 0.65 (0.59-0.71) for saplings and 0.63 (0.58-0.68) for adults. Pooled slopes are 0.63, 0.66 and 0.69.

### 4.2 Seedlings followed most of their slope; saplings and adults did not

The 10-year trailing temperature increased by 0.22 C per decade (0.19-0.25) on the measured plots.

| Layer | CTI trend, C/decade | R (main) | R, stand-age adjusted | R, 81 core species | R, undisturbed plots |
| --- | --- | --- | --- | --- | --- |
| Seedling | +0.083 (0.059 to 0.109) | 0.58 (0.38 to 0.84) | 0.71 (0.51 to 0.95) | 0.47 (0.30 to 0.65) | 0.57 (0.29 to 0.89) |
| Sapling | +0.011 (-0.013 to 0.032) | 0.08 (-0.09 to 0.26) | 0.24 (0.11 to 0.38) | 0.04 (-0.12 to 0.22) | -0.01 (-0.22 to 0.25) |
| Adult | +0.024 (0.011 to 0.035) | 0.17 (0.07 to 0.28) | 0.25 (0.17 to 0.34) | 0.15 (0.05 to 0.26) | 0.13 (0.05 to 0.25) |

Other variants gave the same order. Seedlings: abundance weights 0.57 (0.37-0.78), genus level 0.65 (0.45-0.98), 5-year trailing temperature 0.74 (0.47-1.23), species-number control 0.60, north of 40 N 0.76 (0.31-1.48), south of 40 N 0.46 (0.32-0.65). Adults: abundance weights 0.22 (0.15-0.31), genus level 0.18 (0.07-0.29). Saplings followed their slope only north of 40 N (0.57, 0.35-0.93); south of 40 N their CTI went down (R -0.23, -0.39 to -0.11). Adults also followed more in the north (0.48, 0.28-0.74) than in the south (-0.01, -0.07 to 0.05).

The seedling year path increased steadily from about 2004 to 2025 by about 0.2 C (Figure 3a). It does not show a single step that a protocol change would make. Seedling species number per plot first increased and then decreased in the south, but the CTI trend stayed when we controlled for species number.

### 4.3 The seedling shift did not follow differences in warming

The seedling shift is near the spatial expectation on average, but it is not larger where warming was larger:

- Local warming, consecutive visits: R_local = 0.03 (-0.07 to 0.14) for seedlings, 0.00 (-0.07 to 0.08) for saplings and 0.02 (-0.03 to 0.07) for adults. The interval for seedlings excludes the trend ratio of 0.58.
- Regional warming, 101 blocks: R_regional = -0.60 (-0.84 to -0.30) for seedlings. Blocks that warmed more in 1999-2025 had smaller seedling shifts. Saplings and adults gave -0.05 (intervals include 0). The block temperature trends have a standard deviation of only 0.11 C per decade.
- Long-term warming: plots that warmed more from 1951-1980 to 1996-2025 had warmer seedlings relative to their adults, 0.26 C per C (0.08 to 0.44), which is 0.41 of b. The same test for saplings gave 0.10 (-0.09 to 0.26). Warming varies only 0.13 C (SD) inside 4-degree blocks.

Thus the timing (a steady trend while the region warmed) and the 70-year spatial offset agree with a climate response, but the 25-year local and regional contrasts do not. We cannot attribute the seedling shift to local warming.

### 4.4 Which species and flows changed the CTI

The species tables also give the within-plot trend of each species' presence (share of visits, per decade). The sign of a species term depends on whether the species is warmer or cooler than the plots where it changes. For example, a decrease of a species on plots where it is cooler than the plot mean makes a positive term.

Seedling-layer trend (+0.083 C/decade, Figure 2a): many common species became less frequent as seedlings: red maple (-4.1 percentage points per decade), black cherry (-3.8), flowering dogwood (-2.9), sugar maple (-2.3), quaking aspen (-1.1), paper birch (-1.0) and balsam fir (-0.5). The decreases of the cool species (sugar maple +0.008, aspen +0.011, paper birch +0.004, balsam fir +0.003) and of red maple where it is a cool element (+0.019) made the largest positive terms. The decrease of warm flowering dogwood (dogwood anthracnose) made the largest negative term (-0.008). Ash seedlings became more frequent (white ash +1.0, black ash +1.1 points per decade; this agrees with ash regeneration after emerald ash borer kills the adults) and made negative terms (-0.005 each). Serviceberry seedlings increased (+3.8 points per decade, term +0.011); the 81-core-species index, which excludes "spp." taxa such as serviceberry, still gave R = 0.47. No single species makes most of the trend. Thus the seedling CTI increased mostly because cool or locally cool species became less frequent, not because warm species arrived.

Adult-layer trend (+0.024 C/decade, Figure 2b): red maple adults became more frequent (+2.0 points per decade, term +0.006), and white ash (-1.4, emerald ash borer), paper birch (-0.5) and quaking aspen (-0.3) became less frequent (positive terms +0.004 to +0.005). More frequent black cherry, sugar maple and American beech adults made negative terms (-0.003 each).

Adult flows (Figure 1c): relative to the standing adult CTI, ingrowth was cooler by 0.10 C (presence; 0.06 to 0.14) and natural mortality was cooler by 0.17 C (0.12 to 0.22). With basal-area weights the values were -0.20 and -0.27. Harvest removed slightly warmer species (+0.09, 0.04 to 0.14; basal-area weighted +0.03, -0.00 to +0.06). Thus adults warmed because cool species died faster than cool species grew in, not because warm species grew in. This agrees with the mortality-led adult result of sci:sha256:adb306e0.

### 4.5 Seed source and climate filter in space

In space, seedling CTI follows the adult CTI on the same plot at 0.50 (0.47 to 0.53) per C, and baseline temperature adds 0.33 (0.28 to 0.37) per C inside 2-degree blocks. Thus about half of the seedling spatial slope is a climate filter that acts beyond the local seed source. 60% of seedling presences were species that also occurred as adults or saplings on the same plot.

## 5. Interpretation

1. Demographic inertia alone does not explain the gap. The fastest layer, seedlings, moved toward warm-affinity species at about 0.5-0.7 of its spatial slope. This is near the near-full tracking of Northeast Shelf plankton (sci:sha256:dd5e171c) and Finnish moths (sci:sha256:6d955436), and much more than birds or the network median.
2. The shift stops at the seedling-to-sapling step. Saplings, which are recruited from seedlings over 5-20 years, did not follow (R about 0.0-0.2), except in the north. This agrees with the species-centroid result that seedling offsets do not pass to new saplings (sci:sha256:b96c60e0). The bottleneck is survival or growth from seedling to sapling, not seed arrival.
3. Adults warmed slowly through the death of cool species (aspen, paper birch, balsam fir), not through the gain of warm species.
4. A temporal shift that is near the spatial expectation is not evidence of climate tracking by itself. The seedling shift did not follow local or regional warming differences. The same pattern occurred in winter bird communities (sci:sha256:26c7bb1f) and in bird colonisation (sci:sha256:b83e5597). Widespread species-specific drivers (fewer seedlings of red maple, black cherry, sugar maple and aspen, possibly from browsing, canopy closure or pathogens; dogwood anthracnose; ash regeneration after emerald ash borer) may produce a large part of it. In trees, the seedling and adult shifts came from losses of cool or locally cool species. This is different from the 52-network result, where community warming came from gains of warm-affinity taxa and not from losses of cold-affinity taxa (sci:sha256:b640c9c8).

## 6. Limitations and deviations from the plan

- Added after the 12-state pilot (not in the written plan): the stand ageing adjustment and the seed-source regression. Added after the full results: the 81-core-species index, the species-number control, the regional-warming test and the year path. We wrote and then removed a sapling "pass-through" regression, because sapling measurement noise enters both sides of that regression and biases it upward.
- The pilot on 12 northeastern states (46,794 visits) gave a seedling R near 0. The full 31-state sample gave 0.58, and the north-of-40-N subset of the full sample gave 0.76. Because the pilot states are a subset with a different species mix (more balsam fir and spruce, spruce-budworm cycles), this shows that the seedling result depends on the region. Readers must not extend it to single states.
- The time span is short (median 2003-2022 per plot) and warming was 0.22 C per decade, so the expected CTI change is only about 0.14 C per decade. The local and regional tests have little warming contrast (SD 0.11-0.13 C).
- STI uses only US plots east of about 98 W. Ranges are cut at the Canadian border and at the Great Plains. This compresses the STI scale, but b and the trend use the same STI.
- FIA public coordinates are perturbed by up to about 1.6 km. Climate is at the nearest 5 km nClimGrid cell.
- Seedling counts come from a small area (four microplots, 1/75 acre in total) and FIA seedling and species-coding rules changed between regions and years. The genus-level, core-species and species-number variants do not remove the result, but they cannot exclude every protocol effect.
- Stand-age, disturbance and harvest codes are coarse. The stand-ageing adjustment uses a cross-sectional age slope.
- Deer browsing, pathogens, fire suppression and nitrogen deposition are not measured here.

## 7. Files

- `files/figures/fig1_layers.png`, `fig2_species.png`, `fig3_yearpath.png`: figures.
- `files/results/main_results.json`: spatial slopes, trends and R for all layers and index versions, with intervals.
- `files/results/secondary_results.json`: local, regional and long-term warming tests, flows, seed source, ageing, sensitivities.
- `files/results/species_contrib_{seedling,sapling,adult}.csv`: exact species terms of the presence CTI trend, presence share and within-plot presence trend per decade.
- `files/results/sti.csv`: species and genus temperature indices (both halves and full sample).
- `files/results/yearpath.csv`: two-way fixed-effect year paths.
- `files/results/visit_cti.csv.gz`: one row per visit with plot identifier, FIA CN, year, perturbed public coordinates, climate and the CTI of each layer and index version.
- `files/code/`: all code. `files/data_provenance.csv`: source URLs and SHA-256 of all inputs. `files/analysis_plan.md`: the plan. `files/NOTICE.md`: source attribution.

## 8. Reproduction

Needs Python 3.12 with numpy, pandas, pyarrow, netCDF4 and matplotlib, plus curl and unzip. About 2.4 GB of downloads and 15 minutes of computation on 2 CPUs.

```
bash files/code/run_all.sh /path/to/scratch /path/to/nclimgrid_tavg.nc
```

The script downloads the FIA files into the scratch folder (never into the publication), reduces nClimGrid, builds the visit tables, and writes all results and figures. The FIA DataMart is updated over time; compare the downloaded files with `files/data_provenance.csv`. With newer files, numbers can change a little.
