# Hurricane-force winds gave at most a small decrease in next-summer resident bird counts on eastern US survey routes in 1970-2024, and the decrease did not repeat across regions and periods

## Summary

**Question.** Do Atlantic hurricanes decrease the number of birds that the North American Breeding Bird Survey (BBS) counts on a route in the next breeding season? Resident species stay on the route when an August-November storm passes. Most long-distance migrants are in the tropics at that time. Thus migrants are a negative control for the same route, observer and survey day.

**Data.** BBS 2025 release, 2,025 US routes east of 100 W and south of 46 N, 65,117 acceptable surveys (RunType 1) in 1970-2024, 192 species (43 resident, 40 partial migrant, 109 migrant in AVONET), 4,179,743 route-species-year counts. Atlantic HURDAT2 best tracks for the 1966-2024 seasons. We modelled the peak 1-minute wind at each route in each season with a symmetric modified Rankine vortex. 497 surveys on 298 routes came after a season with modelled hurricane-force wind (64 kt or more, 75 storms in 38 seasons). 6,100 surveys came after tropical-storm-force wind (34-63 kt).

**Method.** log(1 + count) event models with fixed effects for route x species and observer, and for species x year (a) or species x Bird Conservation Region (BCR) x year (b). Wind bins for the season after the survey (placebo, t), the season one year after that (placebo, t+1), and the seasons 1, 2 and 3 years before the survey. A within route-year contrast (resident minus migrant, route x year fixed effects) removes observer, survey weather, survey date and road access. Two-way clustered intervals (route and year). A season-permutation test moves the complete wind field of a season to a random other season. Checks of the survey process, a dose response, four subsets (east and west of 84 W, 1970-1997 and 1998-2024), and species estimates.

**Main results** (change in log(1 + count) x 100, which is approximately %; 95% CI):

| Model, season t-1 hurricane-force wind | Estimate | Placebo season t |
| --- | --- | --- |
| Residents, species x year FE | -3.0 (-5.3 to -0.7) | -0.1 (-2.8 to +2.6) |
| Residents, species x BCR x year FE | -2.1 (-4.4 to +0.2) | +0.8 (-2.2 to +3.8) |
| Partial migrants, species x BCR x year FE | +0.4 (-2.5 to +3.2) | +0.6 (-3.3 to +4.6) |
| Migrants, species x BCR x year FE | -0.3 (-2.2 to +1.6) | +1.7 (-0.7 to +4.1) |
| Resident minus migrant, route x year + species x year FE | -3.0 (-5.4 to -0.5) | -1.2 (-4.4 to +2.1) |
| Resident minus migrant, route x year + species x BCR x year FE | -1.2 (-4.0 to +1.6) | +0.5 (-2.9 to +3.8) |

- The resident decrease is present only in the first breeding season. In the second and third seasons the estimates are near zero (species x BCR x year FE: +0.3 and +1.7).
- Season-permutation test (1,300 draws, route-year class means, route + BCR x year FE): resident coefficient -3.3, one-sided p = 0.055; resident-minus-migrant coefficient -1.5, one-sided p = 0.23.
- The decrease did not repeat across subsets. Residents: west of 84 W -4.0 (-7.1 to -0.9), east of 84 W -0.9 (-4.1 to +2.2); 1998-2024 -3.3 (-5.6 to -1.0), 1970-1997 -0.2 (-3.1 to +2.7). The resident-minus-migrant contrast had an interval that included zero in all four subsets, and its sign was different in the east (-2.7) and the west (+1.4).
- There was no monotonic dose response. For residents: 64-79 kt -3.1 (-5.5 to -0.6), 80 kt or more -1.7 (-5.9 to +2.4). For migrants, 80 kt or more gave -3.2 (-6.4 to -0.1).
- Exposure did not change the survey process in the next season: the probability of an acceptable run -0.6 percentage points (-4.8 to +3.6), observer change +1.2 (-2.0 to +4.5), survey day +0.0 days (-1.2 to +1.2). The sky code was lower (-0.17, -0.26 to -0.07). The within route-year contrast removes this.
- Species estimates (route-clustered, exploratory): the inverse-variance mean of the 43 resident species was -2.4 (SE 0.7); for the 109 migrants it was -0.3 (SE 0.6). Seven resident woodpecker species (Picidae) had a mean of -7.0 (SE 1.6), with a placebo mean of -0.3. We did not plan this woodpecker contrast before the analysis.

**Conclusion.** After hurricane-force wind, resident bird counts on eastern US BBS routes in the next June were at most a few percent lower. The data exclude a mean resident decrease larger than about 4-5%. The decrease was not robust: it became smaller with regional year effects, did not repeat in two of four subsets, did not increase with wind speed, and the season-permutation test gave only weak evidence. This agrees with Rittenhouse et al. (2010), who found changes in community similarity but no significant loss of total abundance after hurricanes in BBS data.

## 1. Background

Hurricanes break trees, remove fruit and seeds, and kill birds. Field studies after single storms (for example Hurricane Hugo, Maria and Irma in the Caribbean, Laura and Delta in Louisiana) found decreases in resident birds. Rittenhouse et al. (2010, Global Change Biology 16:905) used BBS routes, hurricane tracks and Landsat. They found a decrease in community similarity in the first breeding season after a hurricane, but no significant loss of total abundance or richness. Their study used a small set of storms. This study uses all Atlantic storms that reached the eastern US from 1969 to 2023, a modelled wind field, placebo seasons, and migrants on the same routes as an internal control. It extends prior campaign BBS work on weather and migration class (winter cold: sci:sha256:979b781f...; warm seasons: sci:sha256:3250b81c...).

## 2. Data and provenance

All raw inputs were read in place. Hashes of the exact files are in `files/data/input_sha256.txt` and `files/provenance.json`.

| Input | Shared path or source | SHA-256 |
| --- | --- | --- |
| BBS States.zip (2025 release, doi:10.5066/P14SNUV4) | `/mnt/dell-data/shared_datasets/usgs-bbs-2025-release-states-zip/States.zip` | cd0d638a...42e5 |
| BBS Weather.csv | `/mnt/dell-data/shared_datasets/usgs-bbs-2025-weather/Weather.csv` | bd8ceccc...b7d8 |
| BBS Routes.csv | `/mnt/dell-data/shared_datasets/usgs-bbs-2025-routes/Routes.csv` | baeee851...4556 |
| BBS SpeciesList.csv | `/mnt/dell-data/shared_datasets/usgs-bbs-2025-specieslist/SpeciesList.csv` | e1ddbdfc...44e5 |
| AVONET supplementary dataset 1 (Tobias et al. 2022) | `/mnt/dell-data/shared_datasets/avonet-tobias2022-supplementary-dataset1/AVONET_Supplementary_dataset_1.xlsx` | eb645e83...8d3e |
| Atlantic HURDAT2 1851-2025 (release 092326) | exact bytes from campaign bundle sci:sha256:9bc0e5f0... (`files/hurdat2.txt`); source https://www.nhc.noaa.gov/data/hurdat/hurdat2-1851-2025-092326.txt | 75202780...b6125b4 |

## 3. Methods

**Surveys and counts.** We used BBS primary runs (RPID 101) with RunType 1 in May-July, one run per route and year, and routes with 10 or more such surveys. A species is in the panel of a route if it was detected in at least one third of that route's surveys, and in at least 40 routes in total. Zero counts are kept. The panel code follows sci:sha256:979b781f...

**Migration class.** AVONET (eBird taxonomy) migration 1 = resident, 2 = partial migrant, 3 = migrant. Five BBS names were mapped to AVONET names (`files/code/prep_bbs.py`). All 192 species matched.

**Wind exposure** (`files/code/storms.py`). HURDAT2 fixes (all storm types, Vmax 25 kt or more, inside 18-50 N, 105-60 W) were linearly interpolated to 30-minute steps. Wind at distance r from the centre: V = Vmax r/Rmax inside Rmax, V = Vmax (Rmax/r)^0.5 outside. Rmax = 46.4 exp(-0.0155 Vmax[m/s] + 0.0169 lat) km (Willoughby and Rahn 2004). Best-track Vmax already includes the decrease over land. The model has no asymmetry from storm motion and no surface roughness. For each route and season we kept the maximum over all storms. The bins are H = 64 kt or more and T = 34-63 kt.

**Timing.** The BBS survey is in June of year t. Storms of season t occur after that survey, and storms of season t+1 occur one year later. Thus H(t) and H(t+1) are placebo terms. H(t-1) is the main exposure; H(t-2) and H(t-3) test persistence.

**Event models** (`files/code/model.py`, pyfixest 0.60, LSMR demeaner). y = log(1 + count) ~ sum over k in {t+1, t, t-1, t-2, t-3} of (H_k + T_k) | route x species + species x year (or species x BCR x year) + observer. Each migration class was fitted separately. Within route-year model: all classes together with route x species, species x (BCR x) year and route x year fixed effects; H_k and T_k interacted with resident and with partial-migrant indicators (migrants are the reference). Standard errors are clustered by route and by year (CRV1, two-way).

**Dose response.** Wind bins 20-33, 34-49, 50-63, 64-79 and 80 kt or more for seasons t+1, t and t-1, with H and T for t-2 and t-3 as controls.

**Season-permutation test** (`files/code/perm_fast.py`). Route-year means of y over the species of each class (`files/data/routeyear_class_means.csv.gz`). The statistics are the H(t-1) coefficients for (1) the resident mean and (2) the resident-minus-migrant mean, each with route + BCR x year fixed effects and all lead and lag terms. In each draw, a permutation of the 59 seasons (1966-2024) moves the complete wind field of a season to another season. The draw keeps which routes are often exposed and the spatial shape of each storm; it breaks only the timing. Fixed effects were removed by alternating projections (tolerance 1e-10). The observed values agree with pyfixest to 5 decimals. Note: the resident statistic here has no observer fixed effect, so its value (-3.3) is different from the species-level models.

**Survey-process checks** (`files/code/checks.py`). Route-year outcomes from all BBS run records in the study region after the first acceptable run of the route: acceptable run (0/1), any run (0/1), observer change from the last year, first year of the observer, survey day, wind code and sky code. Models: same H/T terms | route + BCR x year.

**Species and traits** (`files/code/traits.py`). One model per species (route + BCR x year + observer fixed effects, route-clustered SE), for species with 5 or more exposed routes. Inverse-variance group means by migration class and AVONET trophic niche, habitat, primary lifestyle and body-mass tertile. These SE do not include spatial correlation between species, thus they are too small. We treat these results as exploratory.

## 4. Results

Figure 1 shows the routes and the event-time estimates. Figure 2 shows the dose response, the subsets and the permutation null. Figure 3 shows the species estimates and the survey-process checks. All coefficients are in `files/results/model_coefficients.csv`.

1. **Leads.** The placebo terms H(t+1) and H(t) were near zero in the six main class models (largest absolute value 1.7) and in the two within route-year models (largest 1.5). Thus storms did not hit routes that already had different counts in the same year. The tropical-storm bin T showed a resident pre-trend with species x year FE (T(t+1) = -1.0, T(t) = -0.9). With species x BCR x year FE this pre-trend disappeared (-0.5, -0.3). Thus regional year effects are necessary.
2. **First season.** Residents decreased by 2-3% after hurricane-force wind. The interval included zero with species x BCR x year FE. Partial migrants and migrants did not change.
3. **Recovery.** H(t-2) and H(t-3) for residents were near zero or positive with species x BCR x year FE.
4. **Contrast with migrants.** With route x year FE the resident decrease relative to migrants was -3.0 (-5.4 to -0.5) with national species-year effects and -1.2 (-4.0 to +1.6) with regional species-year effects.
5. **Permutation.** In 1,300 season permutations the resident coefficient (-3.3) was at the 5.5% lower tail of the null (null SD 2.1). The difference between the first season and the placebo season (-3.7) was at the 1.7% lower tail. The resident-minus-migrant coefficient (-1.5) was at the 23% lower tail (null SD 2.0). Thus the timing of storms explains the resident decrease only weakly, and does not explain a resident decrease relative to migrants on the same survey.
6. **Subsets.** The resident-only decrease came from the west (Gulf of Mexico storms) and the 1998-2024 period. The resident-minus-migrant contrast did not replicate in any subset.
7. **Dose.** No monotonic increase of the decrease with wind. The migrant decrease at 80 kt or more agrees with habitat damage on the breeding grounds of migrants, but it can also be chance.
8. **Survey process.** No effect on run completion, observer change, first-year observers, survey date or wind code.
9. **Species.** 28 of 43 resident species (65%) had negative point estimates. The largest negative estimates with many exposed routes were for woodpeckers: Red-bellied -9.2 (SE 3.0, 255 exposed routes), Red-headed -7.0 (4.3), Downy -5.6 (3.2), Pileated -5.0 (3.4). Blue Jay -5.1 (2.5) and Mourning Dove -5.3 (2.8) also decreased. Carolina Wren (+2.8, 2.7) and Northern Cardinal (-2.4, 1.9) changed little. Trait groups (trophic niche, habitat, body mass) did not separate clearly, because their intervals overlap.

## 5. Limitations

- The wind model is simple. It has no motion asymmetry, no land roughness and a climatological Rmax. Fast storms in the Northeast (Gloria 1985, Bob 1991) have many exposed routes, and the model can overestimate their winds. Wind is also not tree damage, flood or storm surge.
- BBS counts are an index. There is no detection model. A storm can change detectability (for example open canopy) and abundance in the same direction or in opposite directions.
- Exposed surveys are few (497) and are clustered in 38 seasons. The power to detect a 2% effect is low, and the intervals are wide.
- Migrants are not a perfect control. Some migrants were still on the routes in August-September, and storms damage their breeding habitat too.
- Species with fewer than 40 routes or rare detections are not in the panel. Thus rare coastal residents that can be most vulnerable are not tested.
- The woodpecker result was found after the analysis started. It needs an independent test.
- The 2024 season (Helene, Milton) is used only as a placebo lead because BBS data end in 2024.
- The design is observational. Fixed effects and placebos control for many but not all confounders.

## 6. Reproduction

Python 3.12, pandas 3.1.1, numpy 2.5.4, scipy 1.18.1, pyfixest 0.60.0, matplotlib 3.11.2, openpyxl (`uv venv --python 3.12 .venv; uv pip install pyfixest pandas numpy scipy matplotlib openpyxl statsmodels`).

```
DS=/mnt/dell-data/shared_datasets          # or a folder with the same five inputs
H=hurdat2.txt                              # extract files/hurdat2.txt from sci:sha256:9bc0e5f0... or download (see table)
python code/storms.py $H $DS/usgs-bbs-2025-routes/Routes.csv scratch/storms
python code/prep_bbs.py $DS scratch/storms result/files/data scratch
python code/model.py scratch result/files/results
python code/checks.py scratch result/files/data result/files/results scratch/storms
NPERM=... python code/perm_fast.py scratch result/files/results scratch/storms
python code/traits.py scratch result/files/results
python code/exposure_summary.py result/files/data scratch/storms result/files/results
python code/figures.py result/files/data result/files/results result/files/figures scratch/storms
```

Run times on the campaign host (load average 300-900): storms 4 min, panel 2 min, all event models about 1.5 h, permutation about 5 s per draw. `checks.py` writes `scratch/agg.pkl`, which `perm_fast.py` reads. Permutations ran in several workers with different seeds (20261108 for 550 draws; 20261102, 20261103 and 20261104 for 250 draws each); the files are concatenated in `files/results/permutation_null.csv`.

## 7. Files

- `files/code/` analysis code (MIT).
- `files/storms/` modelled route x season peak wind (`route_season_peak_wind.csv.gz`), all route x storm winds of 20 kt or more, and storm route counts.
- `files/data/` input hashes, panel information, AVONET traits used, survey table with wind terms (`surveys.csv.gz`), all BBS run records in the region (`all_runs.csv.gz`), route-year class means.
- `files/results/` model coefficients and logs, survey-process checks (`attrition.csv`), route-year models, permutation null and test, species and trait-group estimates, exposed storms.
- `files/figures/` three figures.

## 8. Provenance

Campaign 11_07_2026, job sci-1107-dell-climate-pollution-biodiversity-3ed5f1f5df8a, topic climate-pollution-biodiversity, machine dell, account claude-andrii, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim. See `files/provenance.json`.

## References

- Rittenhouse C.D. et al. 2010. Avifauna response to hurricanes: regional changes in community similarity. Global Change Biology 16:905-917.
- Willoughby H.E., Rahn M.E. 2004. Parametric representation of the primary hurricane vortex. Part I. Monthly Weather Review 132:3033-3048.
- Landsea C.W., Franklin J.L. 2013. Atlantic hurricane database uncertainty and presentation of a new database format (HURDAT2). Monthly Weather Review 141:3576-3592.
- Tobias J.A. et al. 2022. AVONET: morphological, ecological and geographical data for all birds. Ecology Letters 25:581-597.
- U.S. Geological Survey. North American Breeding Bird Survey dataset 1966-2024 (2025 release). doi:10.5066/P14SNUV4.
- Cameron A.C., Gelbach J.B., Miller D.L. 2011. Robust inference with multiway clustering. Journal of Business and Economic Statistics 29:238-249.
