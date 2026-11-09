# Colder winters were followed by lower next-summer counts of resident birds relative to migratory birds on North American survey routes, 1967-2024

## Summary

We tested one question: does the temperature of the winter before a breeding season change the next-summer count of bird species that stay at the route in winter, relative to species that leave it?

We used the North American Breeding Bird Survey (BBS, 2025 release) and the GHCN-CAMS monthly gridded land temperature. Each data point is the change in count of one species on one route from year t-1 to year t. The same observer surveyed both years. We compared three migration classes from AVONET: resident (sedentary), partially migratory and migratory.

The design uses the migratory species as a negative control. A migratory species is not at the route in winter, so the local winter temperature cannot affect it directly. A fixed effect for each route and year pair absorbs all conditions that are the same for all species in that survey pair: observer, survey date, survey weather, effort and shared detectability shocks. This fixed effect removes the main sources of observation bias. Only the difference in winter slope between classes is identified.

Main results (4,097 routes, 361 species, 4,927,559 species-route year pairs):

1. After a winter 1 °C warmer than the route's 1981-2010 mean, the next-summer count change of resident species was 0.94% larger than that of migratory species (95% CI 0.72 to 1.17; z = 8.2). For partially migratory species, the difference was 0.83% (95% CI 0.61 to 1.05).
2. In a separate model with year fixed effects, the class slopes were 1.05% per °C for residents (0.74 to 1.36), 0.97% for partial migrants (0.66 to 1.27) and 0.17% for migrants (-0.05 to 0.39). The migratory slope was close to zero, as the negative-control logic predicts.
3. The effect was stronger for cold winters than for warm winters. After winters 3 °C or more colder than normal, resident counts fell by 5.0% (95% CI 3.8 to 6.2) relative to migrants, against the reference of winters within 1 °C of normal. After winters more than 2 °C warmer than normal, resident counts rose by 1.8% (0.5 to 3.1).
4. The contrast was positive and its 95% CI excluded zero in all six independent region-by-period samples (West, Central, East; 1967-1995 and 1996-2024) and in all three terciles of route winter climate.
5. A placebo test with the winter after the survey gave no contrast (0.12% per °C, 95% CI -0.19 to 0.43).
6. At the species level, 74% of 66 resident species had positive slopes (26% significantly positive, none significantly negative). Only 9% of 128 migratory species had significantly positive slopes. The resident-minus-migratory difference in mean species slope was 1.0 percentage point per °C (label-permutation p = 0.001). Carolina Wren had the largest slope of the widespread species (9.6% per °C on 1,337 routes). This species is a known example of winter-limited populations.

7. The contrast did not clearly change between periods. In one pooled model, the resident-minus-migratory slope was 1.14% per °C in 1967-1995 (0.87 to 1.40). The change for 1996-2024 was -0.33 (95% CI -0.76 to 0.10). The point estimates were smaller in 1996-2024 in all three regions, but each period CI overlapped.
8. Most of a one-winter loss was transient. When we added the winter before the previous survey (lag 1), the current-winter contrast was 1.07% per °C (0.84 to 1.30) and the lagged contrast was -0.66% per °C (-0.93 to -0.40). Thus, in the next year, residents recovered about 60% of the relative change. The point estimate of the net two-year effect is 0.41% per °C. We did not compute a CI for this sum.

## Data

All raw data are public. The campaign used shared copies of the raw files, which we did not change. The file `files/results/shared_dataset_provenance.txt` records the shared paths, source URLs, download times and SHA-256 hashes.

| Data | Source and version | File and SHA-256 |
|---|---|---|
| BBS counts | USGS North American Breeding Bird Survey, 2025 release, ScienceBase item 691cfb53d4be021d1d89b482 | States.zip, cd0d638a70c30cb0506ff6504b1c17974a1cdb3d2e27165ae7ecff27180542e5 |
| BBS run data | same release | Weather.csv, bd8ceccc2045089762aacf32c4e160cdf75feb9bb387621949fb349b97b8d8b7 |
| BBS routes | same release | Routes.csv, baeee8510dc811d68891bc3fa14c47f8ea21565fe6f6c48e7029e4f4bff24556 |
| BBS species list | same release | SpeciesList.csv, e1ddbdfc0fd7b8688d5b02fc3f8484585f2163de390114459f6a11951ee5d144 |
| Temperature | NOAA PSL GHCN-CAMS monthly mean land air temperature, 0.5°, version 3.01, https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc (retrieved 2026-11-05, 1948-01 to 2026-10) | air.mon.mean.nc, 8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b |
| Migration class | AVONET Supplementary dataset 1 (Tobias et al. 2022, Ecology Letters, doi:10.1111/ele.13898), figshare 10.6084/m9.figshare.16586228.v7, file https://ndownloader.figshare.com/files/34480856 | AVONET Supplementary dataset 1.xlsx, sha256 eb645e83dddb40f1654a3e8d721998dbca76eff540231b7b809267c1e96f8d3e (md5 1445afdcfb6df784010c2ca034544bc8, as figshare reports) |

Shared paths (campaign host): `/mnt/dell-data/shared_datasets/usgs-bbs-2025-release-states-zip/States.zip`, `.../usgs-bbs-2025-weather/Weather.csv`, `.../usgs-bbs-2025-routes/Routes.csv`, `.../usgs-bbs-2025-specieslist/SpeciesList.csv`, `.../noaa-psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc`.

AVONET was not in the shared store. We downloaded it with curl into the private workspace and checked the figshare MD5. The campaign dataset helper could not publish it: its Python download stalled at 0 bytes on the figshare redirect, so we stopped the helper and it removed its lock and stage directory. To get the file, use: `curl -L -o AVONET1.xlsx https://ndownloader.figshare.com/files/34480856` and check the SHA-256 above. `files/results/species_traits.csv` contains the AVONET values that we used for each BBS species.

## Methods

**Survey selection.** We used standard BBS runs (RPID 101) that met all BBS quality criteria (QualityCurrentID = 1, RunType = 1), one run per route and year, 1966-2024, on routes with 10 or more such runs. BBS did not run in 2020, so year pairs that include 2020 are missing.

**Species.** We combined subspecies forms into their parent species. We removed unidentified and hybrid records. We removed orders that the BBS samples poorly: waterbirds and shorebirds, nocturnal birds (owls, nightjars) and diurnal raptors. A species entered a route if it was recorded on at least one third of the route's quality runs. On the runs where the species was not recorded, its count was set to zero.

**Migration class.** AVONET "Migration" (Tobias & Pigot 2019): 1 = sedentary (resident), 2 = partially migratory, 3 = migratory (most of the population migrates long distances). We matched BBS scientific names to the AVONET eBird-taxonomy sheet (666 of 676 names), then to the BirdLife sheet. A short synonym list covers recent genus changes. Seven names had no match and we excluded them. We set this classification before we fit models and did not change it.

**Response.** dy = log(count_t + 1) - log(count_{t-1} + 1), only for consecutive years with the same observer (ObsN). This removes observer turnover, a main source of BBS observation bias.

**Exposure.** W = mean temperature for December (t-1), January (t) and February (t) at the GHCN-CAMS cell nearest to the route start, as an anomaly from the 1981-2010 mean of the route. Secondary exposures: the coldest of the three winter months; spring (March-May, year t); the previous breeding season (June-August, year t-1).

**Model A (main contrast).** dy[s,r,t] = a[s] + FE[r,t] + b_res·W[r,t]·RES[s] + b_par·W[r,t]·PAR[s] + e. Migratory species are the reference. The route-year fixed effect absorbs every survey condition that is shared across species in the year pair. We fit the two-way fixed effects by alternating projections. The standard errors are cluster-robust. We report the larger of the year-clustered (56 clusters) and route-clustered (4,097 clusters) values.

**Model B (class slopes).** dy = a[s] + d[t] + Σ_class b_class·W·class + c1·Δdate + c2·Δdate² + e. This gives an absolute slope for each class. Spatial differences in winter anomaly within a year identify the slopes.

**Period and recovery tests.** Model A with an added W·class·(year ≥ 1996) term tests a change between periods. Model A with an added W[r,t-1]·class term tests recovery in the next year.

**Replication and checks.** We refit model A in six independent samples: three longitude regions (West < 105° W, Central 105-90° W, East > 90° W) × two periods (1967-1995, 1996-2024). We also refit it in terciles of route winter climate and with these changes: coldest-month exposure, control for spring and previous-summer temperature, observer changes included, passerines only, pairs with two zero counts removed, survey date change of 7 days or less. The placebo replaces W with the winter after the survey (December t to February t+1). A nonlinearity test uses anomaly bins with (-1, 1] °C as the reference. Species-level slopes use year and route fixed effects for each species with 2,000 or more rows on 30 or more routes (229 species). A label-permutation test (10,000 permutations) compares resident and migratory species means.

## Figures

- `files/figures/fig1_dose_response.png`: (A) Resident and partial-migrant count change relative to migrants, by winter-anomaly bin. (B) The annual mean resident-minus-migratory change (route-year centred) against the mean winter anomaly over all routes, 1967-2024.
- `files/figures/fig2_replication.png`: The resident-minus-migratory slope in the main model, six region-by-period samples, three winter-climate terciles, robustness checks and the placebo.
- `files/figures/fig3_species.png`: Slopes for each species by migration class.

## Interpretation

The results agree with this explanation: cold winters increase over-winter mortality, or decrease condition, of birds that stay near the breeding route, and the next breeding population is smaller. For species that leave the route, the local winter has a small or no effect. The effect is asymmetric: cold extremes cause larger losses than the gains after warm winters. Route winter temperature at BBS routes increased by about 0.40 °C per decade in 1967-2024 (the mean anomaly over routes). The partial recovery in the next year (result 8) agrees with density-dependent compensation or with a lower detectability that continues for one year. Thus, these data do not show a long-term population consequence of winter warming, and we did not calculate one.

## Limitations

- **Observation, not abundance.** BBS counts are indices of abundance. The route-year fixed effect removes detectability changes that all species share, but not changes in detectability that differ by class. For example, after a warm winter, residents can start to breed earlier and sing at a different rate on the survey date. The placebo test, the date-change check and the spring control do not support this explanation as the main cause, but they cannot exclude it fully.
- **Classification errors.** AVONET migration classes are coarse and contain some errors for North American populations. For example, Purple Martin is coded as sedentary, and Pacific Wren and Golden-crowned Kinglet are coded as migratory although many individuals winter within the breeding range. Such errors make the contrast smaller, not larger. AVONET cannot separate short-distance from long-distance migrants, because its range latitudes include only breeding and resident ranges.
- **Exposure scale.** A 0.5° monthly grid cell is a coarse measure of winter conditions. It does not include snow cover, ice storms or the duration of cold spells. Data for daily extremes would give a better test of the cold-extreme effect.
- **Spatial dependence.** Winter anomalies are correlated over large areas. Year-clustered standard errors allow for this correlation within a year, but the number of independent winters is limited (56 survey years).
- **Species set.** We excluded waterbirds, raptors and nocturnal species. Sparse species and species with few routes do not contribute much information.
- **Scope.** The results apply to BBS routes in the United States and Canada, 1967-2024. They do not show a causal mechanism for single species.

## Relation to other campaign work

Other publications in this campaign tested ozone, survey weather and summer warmth on BBS counts and richness and most results were null. One publication (sci:sha256:3250b81c789d8cd041cf359eb978868b41ae06364686201fde41eeb105a326c8) reported that warm breeding seasons were followed by lower counts in the warm part of species ranges. This study uses a different exposure (the preceding winter) and a different identification strategy (a within-survey contrast between migration classes with migratory species as a negative control). It does not reuse their code.

## Reproduce

```
uv venv --python 3.12 venv && uv pip install --python venv/bin/python -r files/code/requirements.txt
source venv/bin/activate
bash files/code/run_all.sh /mnt/dell-data/shared_datasets /path/to/AVONET1.xlsx /path/to/scratch
```

Run time: about 70 minutes on one core with 8 GB of memory. The code reads the raw files directly. The panel has about 5.3 million rows. `files/results/` contains all the numbers in this README (`results.json`, `extra_results.json` and the CSV tables) and the model logs.

## Provenance

- Job: sci-1107-syam1-climate-pollution-biodiversity-7a0c419c537c
- Topic: climate-pollution-biodiversity; campaign 11_07_2026
- Machine: syam1; account: claude-olen
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent
- Date: 2026-11-08
- The signing key is a campaign-machine key, not a personal authorship claim.
