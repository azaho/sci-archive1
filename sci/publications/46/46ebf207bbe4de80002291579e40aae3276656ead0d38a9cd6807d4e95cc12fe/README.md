# Cold winters decreased next-summer counts of resident birds but not of long-distance migrants on the same North American survey routes, 1968-2019

**Job:** sci-1107-syam1-climate-pollution-biodiversity-da448f0e0178 · **Topic:** climate-pollution-biodiversity · **Campaign:** 11_07_2026 · **Machine:** syam1 · **Account:** claude-olen · **Model:** Claude Opus 5.5 (claude-opus-5-5), operating as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

We tested one question: does a cold winter decrease the bird counts of the next breeding season, and is the effect specific to the birds that were present during that winter?

We used the USGS North American Breeding Bird Survey (BBS, 2025 release) and the NOAA GHCN_CAMS monthly gridded temperature. We put the landbird species into two guilds:

- **Resident species (R):** species that stay on or near their breeding range in winter (130 species).
- **Long-distance migrant species (M):** species whose US and Canadian breeding populations winter almost fully south of the US (114 species).

The long-distance migrants were not on the route during the winter. But they are counted by the same observer, on the same day, in the same weather, and with the same route effects as the residents. Thus the migrant change is a control for detection and observer effects within the survey. The main outcome is C = dR − dM. Here dR and dM are the changes, from one year to the next, in the mean log(1 + count) over the route's resident and migrant species.

Main results (86,809 same-observer pairs of consecutive-year surveys on 4,508 routes, winters 1968-2019, route and year fixed effects, standard errors clustered by year):

1. **Each +1 °C of December-February temperature anomaly increased C by 0.0133 log units (95% CI 0.0097 to 0.0169).** The effect is in the residents (dR slope 0.0128, CI 0.0093 to 0.0164). The migrants show no effect (dM slope −0.0004, CI −0.0027 to 0.0019).
2. **The response is asymmetric. Cold winters have the largest effect.** Relative to winters within ±1 °C of normal, winters more than 3 °C colder than normal (4,579 pairs) were followed by a resident index that was 0.068 log units lower (about 7%, CI −0.090 to −0.045). The migrant index did not change (+0.006, CI −0.005 to 0.016). In a piecewise model, the cold-side slope (0.020 per °C) was approximately four times the warm-side slope (0.005 per °C).
3. **The result replicated in independent subsets:** eastern and western routes, northern and southern routes, the winters of 1968-1993 and 1994-2019, four alternative guild definitions, and all observers. Canadian routes alone gave a smaller and uncertain slope (0.0045, CI −0.0036 to 0.0125). **A placebo exposure, the winter after the survey, had no effect** (−0.0026, CI −0.0064 to 0.0012).
4. **The effect is wide across species.** For the 83 resident species with sufficient data, 77% of the slopes were positive (12 clearly positive and 0 clearly negative). For the 103 migrant species, 50% of the slopes were positive (2 clearly positive and 5 clearly negative). Carolina Wren, a species with known sensitivity to winter, had one of the largest well-sampled slopes (+0.091 per °C). Body mass did not predict the resident slope.
5. **Winter Storm Uri (February 2021) gave an inconclusive out-of-sample test.** On routes south of 37° N with a February 2021 anomaly of −4 °C or colder (110 routes, mostly in Texas, Oklahoma and Arkansas), C changed from 2019 to 2021 by −0.110 (CI −0.173 to −0.048) relative to 328 milder southern routes. The 1968-2019 model predicted −0.033. But most of this contrast came from a higher migrant count (+0.073), not from a lower resident count (−0.037, CI −0.096 to 0.023). The same two route sets gave contrasts of similar size in 2 of 20 placebo year pairs (2000-2019). Thus we cannot attribute the 2021 contrast to the storm.

![Dose response and species slopes](files/figures/fig1_dose_response_species.png)

## Background and gap

Cold winters can kill resident birds. Earlier single-species and regional studies report declines after severe winters, for example in Carolina Wren and Northern Bobwhite. Studies of Breeding Bird Survey trends usually use breeding-season climate or long-term trends. Other studies in this campaign examined breeding-season warmth and next-year counts (sci:sha256:3250b81c…) and range-centroid shifts (sci:sha256:7714830c…). We did not find a continental BBS test that (a) separates winter exposure by migratory guild on the same survey, (b) has a placebo exposure and a negative-control guild, and (c) replicates across regions and periods. Winter Storm Uri killed many early-arriving Purple Martins (a migrant) in Texas and Louisiana (PubMed 41792447). We found no BBS analysis of its effect on resident species.

## Data

| Data | Shared path (campaign store) | Source | SHA-256 |
| --- | --- | --- | --- |
| BBS counts, States.zip | `usgs-bbs-2025-release-states-zip/States.zip` | USGS ScienceBase item 691cfb53d4be021d1d89b482 (2025 release) | `cd0d638a70c30cb0506ff6504b1c17974a1cdb3d2e27165ae7ecff27180542e5` |
| BBS routes | `usgs-bbs-2025-routes/Routes.csv` | same item | `baeee8510dc811d68891bc3fa14c47f8ea21565fe6f6c48e7029e4f4bff24556` |
| BBS survey conditions | `usgs-bbs-2025-weather/Weather.csv` | same item | `bd8ceccc2045089762aacf32c4e160cdf75feb9bb387621949fb349b97b8d8b7` |
| BBS species list | `usgs-bbs-2025-specieslist/SpeciesList.csv` | same item | `e1ddbdfc0fd7b8688d5b02fc3f8484585f2163de390114459f6a11951ee5d144` |
| Monthly temperature, 0.5° | `noaa-psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` | https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc (GHCN_CAMS v3.01) | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |
| AVONET species traits | not in the shared store (see below) | figshare 10.6084/m9.figshare.16586228 v7, file 34480856 "AVONET Supplementary dataset 1.xlsx" | `eb645e83dddb40f1654a3e8d721998dbca76eff540231b7b809267c1e96f8d3e` (figshare MD5 `1445afdcfb6df784010c2ca034544bc8` matched) |

The shared-store path prefix is `/mnt/dell-data/shared_datasets/`. We computed the hashes on the files that we used (`files/data/input_sha256.txt`). They agree with the `provenance.json` records of the store. The campaign dataset helper could not import AVONET because figshare returned HTTP 403 to the helper. The helper left no lock. We downloaded the file with `curl` to a local scratch folder and checked the figshare MD5. The bundle does not include the AVONET workbook. It includes the extract that we used (`files/data/species_guilds.csv`: AOU code, name, AVONET Migration and Mass, and the guild flags).

## Methods

**Surveys.** We used BBS roadside routes with 50 stops (RouteTypeID 1, RouteTypeDetailID 1), the standard protocol (RPID 101), and surveys with RunType 1 (accepted). This gave 127,482 surveys on 5,291 routes. We used landbird orders only (no waterbirds, shorebirds, owls or nightjars). We removed hybrids, forms, and unidentified taxa. Of 428 species, 425 matched AVONET by scientific name (eBird taxonomy sheet first, then BirdLife).

**Guilds.** The AVONET Migration codes (1 sedentary, 2 partial, 3 migratory) are global species codes. Many codes are wrong for North American breeding populations. For example, Purple Martin, Yellow-breasted Chat and Northern House Wren have code 1, and Northern Mockingbird, Red-tailed Hawk and Cooper's Hawk, which winter widely in the US, have code 3. Thus we made the guild table explicit (`files/code/guilds.py`):
- R = AVONET code 1, minus 36 species that migrate, migrate partly or irrupt in the US and Canada (list in the code).
- M = a list of 114 species whose breeding populations in the US and Canada winter almost fully in Mexico, the Caribbean, or Central and South America.
- The other species are not in the main contrast.
We wrote these lists before we ran any model. As sensitivity tests we used (a) residents of core resident families only (tits, nuthatches, woodpeckers without sapsuckers, quail, grouse, corvids, wrens, cardinals, bushtit), (b) the raw AVONET codes 1 versus 3, (c) residents without introduced species, and (d) migrants without swallows.

**Guild index.** For each route, the species pool is each species that was recorded in 25% or more of the accepted surveys of the route (the route must have 5 or more surveys). For each survey, the guild index is the mean of log(1 + count) over the pool species of the guild, with zero for pool species that were not recorded. A route must have 3 or more pool species in each guild.

**Exposure.** For each route, we used the nearest 0.5° GHCN_CAMS cell. Winter t is December of year t−1 plus January and February of year t. The anomaly is relative to the cell's mean for winters 1981-2010. Secondary exposures: the anomaly of the coldest single winter month, and the February anomaly. Covariate: the March-May anomaly of year t, because a cold winter can come before a cold, late spring that can change detection.

**Models.** Unit: consecutive-year surveys of one route (t−1, t) by the same observer, survey years 1968-2019. Outcome: C, dR or dM. Linear model with the DJF anomaly, the March-May anomaly, route fixed effects and year fixed effects. Because the outcome is a first difference, the route effects absorb route-specific linear trends. The year effects remove continental changes common to the year (for example, changes in protocol or in common detection). Thus the winter slope comes only from spatial differences in anomaly within a year. Standard errors are clustered by survey year (52 clusters), because temperature anomalies have strong spatial correlation within a year. Other tests: models without year effects, a model with the change in survey date, all observers, a piecewise linear model (cold part and warm part), anomaly bins, an interaction with the 1981-2010 winter climatology, the placebo exposure (the winter after survey t), separate slopes for each year, and slopes for each species (year fixed effects, at least 300 pairs and 20 years).

**Uri test.** The 2020 survey was mostly cancelled (COVID-19). Thus we compared same-observer surveys in 2019 and 2021 (two-year change). We did not use the 2021 data to fit any model. We compared routes south of 37° N with a February 2021 anomaly of −4 °C or colder ("severe", mean −5.3 °C; 44 Texas, 27 Oklahoma, 22 Arkansas, 10 Missouri, 7 other routes) with routes south of 37° N with an anomaly above −2 °C ("mild", mean −0.3 °C). Confidence intervals are route bootstraps (4,000 draws). As a placebo distribution we calculated the same severe-minus-mild contrast for the same route sets in each two-year pair (t−2, t) for t = 2000 to 2019. We also followed both zones (all latitudes) to 2024.

## Results

### Main model and controls

| Model (outcome, n = 86,809 pairs unless stated) | Slope per +1 °C DJF anomaly | 95% CI |
| --- | --- | --- |
| C, route + year FE (main) | 0.0133 | 0.0097 to 0.0169 |
| C, route FE only | 0.0120 | 0.0091 to 0.0149 |
| C, + change in survey date | 0.0132 | 0.0095 to 0.0169 |
| C, all observers (n = 93,730) | 0.0128 | 0.0092 to 0.0164 |
| C, coldest-month anomaly instead of DJF | 0.0073 | 0.0040 to 0.0106 |
| dR (residents alone) | 0.0128 | 0.0093 to 0.0164 |
| dM (migrants alone, negative control) | −0.0004 | −0.0027 to 0.0019 |
| C, placebo: winter after the survey | −0.0026 | −0.0064 to 0.0012 |
| C, piecewise: cold part (anomaly < 0) | 0.0200 | 0.0143 to 0.0257 |
| C, piecewise: warm part (anomaly > 0) | 0.0052 | 0.0008 to 0.0097 |
| C, anomaly × winter climatology (per °C of climatology) | 0.00013 | −0.00021 to 0.00047 |

Without year effects, dM had a small negative slope (−0.0025, CI −0.0042 to −0.0008). With year effects, it had none. This agrees with continental year-to-year signals in migrants that are not related to local winter weather. Within single years, 42 of 52 (81%) cross-sectional slopes of C on the DJF anomaly were positive (`files/figures/figS2_within_year_slopes.png`). The slope did not change clearly with the winter climatology of the route. Thus we found no evidence that the same anomaly has a larger effect in warm-winter regions.

### Replication

| Subset | n pairs | Slope of C | 95% CI |
| --- | --- | --- | --- |
| East (longitude > −100) | 60,049 | 0.0140 | 0.0087 to 0.0194 |
| West (longitude ≤ −100) | 26,760 | 0.0093 | 0.0050 to 0.0137 |
| South (latitude < 37) | 23,330 | 0.0089 | 0.0006 to 0.0171 |
| North (latitude ≥ 37) | 63,479 | 0.0141 | 0.0102 to 0.0180 |
| Canada only | 12,542 | 0.0045 | −0.0036 to 0.0125 |
| Winters 1968-1993 | 31,777 | 0.0165 | 0.0113 to 0.0216 |
| Winters 1994-2019 | 55,032 | 0.0117 | 0.0069 to 0.0165 |
| Core resident families vs M | 83,231 | 0.0132 | 0.0091 to 0.0172 |
| Native residents only vs M | 80,250 | 0.0137 | 0.0094 to 0.0180 |
| R vs M without swallows | 86,300 | 0.0128 | 0.0092 to 0.0165 |
| Raw AVONET 1 vs 3 | 88,489 | 0.0084 | 0.0054 to 0.0114 |

The raw AVONET guilds gave a smaller slope. This agrees with the misclassification above: the raw code-3 group contains species that winter in the US, and the raw code-1 group contains true migrants.

![Replication forest plot](files/figures/fig2_replication_forest.png)

### Species

Resident species with clearly positive slopes (lower 95% limit > 0) include Carolina Wren (0.091 ± 0.018 SE per °C), Northern Bobwhite (0.046 ± 0.012), Bushtit, Sharp-tailed Grouse, Ring-necked Pheasant, Red-bellied Woodpecker, California Quail, House Sparrow, Black-capped Chickadee and White-breasted Nuthatch (`files/data/species_slopes.csv`). The weighted regression of the resident slope on log10 body mass gave −0.0007 ± 0.0020 (p = 0.73). Thus small residents were not clearly more sensitive. Among migrants, Purple Martin had a negative slope (−0.012 ± 0.006). A negative slope is the opposite of a winter-mortality effect. A possible explanation is that warm winters cause early arrival and exposure to late cold spells, but we did not test this.

### Winter Storm Uri

| Southern routes (lat < 37° N), 2021 minus 2019 | Severe minus mild | 95% CI | Placebo years (2000-2019): mean ± SD |
| --- | --- | --- | --- |
| C | −0.110 | −0.173 to −0.048 | −0.009 ± 0.069 (2 of 20 lower) |
| dR (residents) | −0.037 | −0.096 to 0.023 | −0.002 ± 0.091 |
| dM (migrants) | +0.073 | 0.028 to 0.119 | +0.007 ± 0.050 |
| C predicted from the 1968-2019 coldest-month model | −0.033 | −0.018 to −0.048 | |

When we included the northern plains (677 routes with February 2021 anomaly ≤ −4 °C at all latitudes), the residents increased from 2019 to 2021 (+0.034, CI 0.009 to 0.060). Thus the 2021 data do not show a clear resident decline after the storm. The change in the contrast has the predicted sign, but it comes mainly from the migrant side. Also, it is within the range of the same-route placebo contrasts. The two-year change includes winter 2020 and changes in survey effort during COVID-19.

![Uri hold-out test](files/figures/fig3_uri_holdout.png)

## Interpretation

On average across North America, the bird counts of a breeding season record the preceding winter, but only in the species that were present during the winter. This is what we expect if winter survival (or winter movement) of residents is the cause. It is not what we expect from a survey artifact, because the migrants on the same survey did not respond, and because the next winter did not "predict" the counts. The effect is small for a typical anomaly (approximately 1.3% per °C), but it is concentrated in cold winters (approximately 7% after winters more than 3 °C below normal). Warming winters will thus probably help many resident populations, while migrants do not get this benefit. This is one possible mechanism for the different trends of resident and migrant birds in North America. A single extreme, short cold event (Uri) did not give a clear additional signal in the BBS. Monthly means do not resolve such a short event well, and 110 routes give low statistical power against the year-to-year noise.

## Limitations

- **Observation bias.** The migrant control removes effects that are common to the guilds (observer, date, weather, route). It cannot remove a detection effect that is specific to residents and related to the winter (for example, a different song rate after a cold winter). We controlled for the spring anomaly and the change in survey date. We cannot exclude such effects fully.
- **Exposure.** Monthly 0.5° gridded means do not measure snow, ice storms, wind chill, or extremes that last a few days. The Uri test is limited by this.
- **Guilds.** Our guild lists use expert knowledge of winter ranges, not a winter-abundance data set. Some short-distance movement of "residents" is possible. The results with raw AVONET codes and with core resident families agree in sign.
- **Outcome.** The index is a mean of log(1 + count) over pool species. It is not an estimate of absolute abundance or of survival. Pool species were chosen with all years of data.
- **Causality.** The design is observational. Winter anomalies can correlate with other factors (for example, food supply or disease). The placebo and negative-control tests decrease, but do not remove, this risk.
- **Coverage.** Canadian routes gave an uncertain slope, and the northern boreal region and Alaska have few routes. Mexico is not included.
- **Inference.** Clustering by year allows any correlation in a year, but with 52 clusters the CIs are approximate. We did not correct for multiple tests across the robustness table. The main result does not depend on one test.

## Reproduction

1. Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, netCDF4 1.7.5.1, openpyxl 3.1.5, matplotlib 3.11.2, pyarrow 26.0.1.
2. Get the AVONET workbook: `curl -L -o AVONET_Supplementary_dataset_1.xlsx https://ndownloader.figshare.com/files/34480856` and check the SHA-256 above. Get the BBS and GHCN_CAMS files from the sources above, or use the campaign store.
3. Run `DATASETS=/mnt/dell-data/shared_datasets AVONET=AVONET_Supplementary_dataset_1.xlsx PYTHON=python3 bash files/code/run_all.sh WORKDIR`. Set all thread variables to 1. On the campaign host (one thread), the full run took approximately 20 minutes.
4. The outputs in `WORKDIR/out` must agree with `files/data/` (`results.json`, `uri_south.json`, CSV tables). The bootstrap seeds are fixed.

Files:
- `files/code/prep.py`: reads BBS, AVONET and temperature data and makes route-level tables.
- `files/code/guilds.py`: the guild rules and lists.
- `files/code/analyze.py`: all models, bins, species slopes and the Uri test.
- `files/code/uri_regional.py`: the southern Uri test and placebo years.
- `files/code/figures.py`: figures.
- `files/data/route_guild_index.csv.gz`: guild index for each survey (route, year, observer, R_idx, M_idx).
- `files/data/route_pairs.csv.gz`: all analysis pairs with exposures.
- `files/data/results.json`, `uri_south.json`: all model estimates.
- `files/data/dose_response_bins.csv`, `species_slopes.csv`, `within_year_slopes_*.csv`, `uri_*.csv`, `pairs_2021_vs_2019.csv`: tables for the figures.
- `files/figures/`: main figures 1-3 and supplementary S1 (recovery of the Uri zones to 2024) and S2 (slopes for each year).
