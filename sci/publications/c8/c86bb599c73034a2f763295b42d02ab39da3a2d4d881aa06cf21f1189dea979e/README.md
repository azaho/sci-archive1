# Climate suitability change predicted little of US bird abundance change in 2010-2025

## Summary

Stephens et al. (2016, Science 352:84) reported that climate suitability trends from species distribution models predict bird population trends in Europe and the United States. This work tests that idea forward in time with the North American Breeding Bird Survey (BBS) and gridded US climate data (nClimGrid).

We fitted one climate model for each species to its 1981-2000 distribution on US BBS routes. We then kept each model unchanged (frozen). We used it to calculate the climate suitability of each route in each year from 1981 to 2025. We compared the suitability change with the change in bird counts at two levels:

1. **Within species, between routes.** Did a species become more abundant on the routes where its climate became more suitable?
2. **Between species.** Did species whose climate suitability increased (the Stephens "climate-favoured" species) have more positive population trends?

We used two periods: 1981-2009 (this overlaps the Stephens period) and 2010-2025 (a forward period). We also used two independent regions: East (longitude -100 and east) and West.

**Main results**

- Within species, route abundance change followed suitability change in 2010-2025, but the response was small. One log unit of suitability change gave 0.053 log units of abundance change (95% CI 0.035 to 0.070; 346 species, 1,623 routes). The sign was the same in the East (0.061, CI 0.040 to 0.083) and in the West (0.036, CI 0.010 to 0.062). The result stayed positive with species x Bird Conservation Region fixed effects, with routes that kept the same observers, with spatial-block clusters, with a boosted-tree climate model and when we removed species that have 20% or more of their BBS birds in Canada (Figure 1). With 1-year climate instead of 5-year means it was smaller (0.016, CI 0.005 to 0.027).
- The response was timing-specific. On routes that had data in both periods, 2010-2025 abundance change followed 2010-2025 suitability change (0.063, SE 0.013) and not 1981-2009 suitability change (0.004, SE 0.014).
- In 1981-2009 the within-species result was weaker and not robust: 0.037 (CI 0.003 to 0.071) in the main model, but near zero with species x region fixed effects, with the boosted-tree model and in the West. It was clear (about 0.06 to 0.07) only for US-centred species (all US and East) and for eastern routes that kept the same observers.
- Between species, suitability trends did not predict population trends in 1981-2009 (Spearman rho -0.01, permutation p = 0.89; 287 species). In 2010-2025 the link was weak (rho 0.085, p = 0.11; OLS slope 0.085, CI 0.017 to 0.153) and not clear in either region alone (Figure 3). A model calibrated on 1981-2009 had no forecast skill for 2010-2025 species trends (mean squared error 0.5% lower than a constant forecast for all US species, and slightly higher than the constant in East and West).
- Species suitability trends were not stable between the periods (Spearman rho 0.03 between the 1981-2009 and 2010-2025 trends). Thus the group of "climate-favoured" species changed between periods.
- Observer control changed the species trends. The median 2010-2025 trend was -0.134 log per decade with observer fixed effects and -0.050 with route fixed effects only.

**Interpretation.** In the forward period, bird abundance on US routes moved in the direction that frozen climate models predicted. But the response was only about 5% of full tracking (Figure 2), and it explained a very small part of the variation in abundance change. Between-species climate indicators of the Stephens type gave almost no information about which US species increased or decreased. The small within-species response agrees with a published campaign result: the BBS community temperature index followed less than 10% of warming (sci:sha256:c0a3a9aa...).

## Data

| Source | Version and files used | License |
| --- | --- | --- |
| North American Breeding Bird Survey, USGS (Ziolkowski et al. 2026), doi:10.5066/P144YU3S | 2026 release (1966-2025): States.zip (10-stop counts), Weather.csv, Routes.csv, SpeciesList.csv | US Government public domain |
| NOAA NCEI nClimGrid monthly, doi:10.7289/V5SX6B56 | nclimgrid_tavg.nc and nclimgrid_prcp.nc, files of 2026-10-06 (1895-01 to 2026-09) | US Government public domain |

The exact URLs and SHA-256 hashes are in `files/NOTICE.md` and `files/code/00_get_data.sh`. The analysis used the shared campaign copies at `datasets/bbs-2026-release-*-6a0b0b0a/` and `datasets/noaa-nclimgrid-monthly-{tavg,prcp}-20261006/`. We checked the hashes of all files against the recorded provenance.

Note: the BBS 50-stop files contain almost no data before 1997. Our first run used them by mistake and gave wrong 1981-2009 results. We found the error (implausible mean count changes), changed the pipeline to the 10-stop State files, which cover 1966-2025, and ran all steps again. All results in this publication come from the corrected run.

## Methods

**Survey data.** We used US routes (country 840), standard protocol (RPID 101) and surveys that meet BBS quality standards (RunType 1). The count for a route, year and species is the 50-stop total from the 10-stop State files. We used 2020 data where present; there were no 2020 surveys.

**Climate.** For each route start point we took the mean of valid nClimGrid cells in a 5 x 5 cell window (about 20 x 20 km). The climate year Y is July of Y-1 to June of Y (the 12 months before the June survey). Four variables: winter temperature (Dec-Feb mean), summer temperature (mean of Jul and Aug of Y-1 and Jun of Y), log annual precipitation and log April-June precipitation. Suitability for year Y uses the 5-year mean of climate years Y-4 to Y (a 1-year version is a robustness check).

**Climate models.** Training data: 2,690 routes with at least 5 good surveys in 1981-2000. Response: mean count per survey in 1981-2000. Predictors: the four 1981-2000 mean climate variables, with squares and pairwise products (14 terms), in a Poisson GLM with a small ridge penalty (scikit-learn PoissonRegressor, alpha 0.001). We fitted 367 species present on 50 or more training routes (we removed hybrids, unidentified forms and subspecies forms). Five-fold spatial-block cross-validation (5-degree blocks) gave a median AUC of 0.914; we kept the 346 species with AUC 0.7 or more. A Poisson boosted-tree model (HistGradientBoostingRegressor) on the same data is a second model type.

**Within-species route test.** For each window we compared a start block and an end block of years: 1981-85 to 2005-09, and 2010-14 to 2021-25. A route was used when it had at least 3 good surveys in each block. A species-route pair was used when the species was counted on the route at least once in the window. The abundance change is log(mean count end + 0.5) - log(mean count start + 0.5). The suitability change is the log ratio of the mean suitability in the two blocks, winsorised at the 1st and 99th percentiles in each window. Model: abundance change ~ suitability change + observer turnover | species fixed effects, with standard errors clustered by route and by species (pyfixest feols). Observer turnover is the fraction of end-block surveys by observers who did not survey the route in the start block. Variants: species x BCR fixed effects; a baseline-suitability control; spatial-block clusters (2-degree cells); routes with no observer change; boosted-tree suitability; 1-year climate; US-centred species only.

**Species-level test.** For each species, window and region we used all routes on which the species was counted at least once in the window, with zeros for surveys that did not record it. Population trend: Poisson regression of count on year with route and observer fixed effects and a first-year-observer term (pyfixest fepois, LSMR demeaner, route-clustered SE). Climate suitability trend (CST): the slope of log(mean suitability over the same routes) on year. We report Spearman correlations with 2,000 permutations, OLS slopes with HC3 intervals, and the difference in mean trend between species with positive and negative CST (bootstrap intervals).

## Results tables

All numbers above come from these files:

- `files/results/route_tests.csv`: all within-species route models (coefficient, SE, 95% CI, p, n).
- `files/results/route_timing.csv`: timing test and persistence on routes with data in both windows.
- `files/results/robust_us_species.csv`: US-centred species check.
- `files/results/species_trends.csv`: trend and CST for each species, window and region.
- `files/results/species_tests.csv`, `species_crosswindow.json`, `species_forward.csv`: species-level tests.
- `files/results/sdm_fit.csv`: cross-validated fit for each climate model.
- `files/results/route_climate_change.csv`: climate change for each route and window (Figure 4).
- `files/data/route_longdiff.parquet`: the species-route long-difference table used in the route tests.

Climate change in the two windows (mean over routes, between block means): East winter +1.27 C and summer +0.27 C in 1981-2009, +1.51 C and +0.14 C in 2010-2025; West winter +0.46 C and summer +0.66 C, then +0.64 C and +0.96 C (Figure 4).

## Limitations

- The climate models use US routes only. They cut the range of species that also live in Canada or Mexico. The check with US-centred species gave similar or larger route coefficients, but range truncation can still bias suitability for northern and southern species.
- The models use four climate variables and no land cover. They are simpler than the atlas-based models of Stephens et al. Thus this is a conceptual forward test of the Stephens idea, not an exact replication.
- Errors in suitability make the route coefficient smaller (attenuation). Thus 0.05 is a lower limit of the true response to climate suitability, if the models describe the true niche. With boosted trees the coefficient was 0.034, and with routes that kept the same observers it was 0.066.
- BBS counts are an index. We did not model detection. Observer fixed effects and observer turnover terms reduce, but do not remove, observer effects.
- The 2010-2025 end block has no 2020 data and fewer routes in 2021-2025 (2,091 to 2,215 surveys per year).
- We did not pre-register the analysis. We report all model variants that we ran. The baseline-suitability, species x BCR and US-centred checks were added after we saw the first results.
- Long differences of 5-year blocks reduce noise but can miss non-linear changes within a window.

## Reproduce

1. Run `files/code/00_get_data.sh` in an empty scratch folder. It downloads the source files into `./datasets/<name>/` and checks the SHA-256 hashes. (nClimGrid files change monthly; a newer copy will have a different hash.)
2. Copy `files/code/` to `./work/code/`. Make a Python 3.12 environment with pandas 3.1.1, numpy 2.5.4, scipy 1.18.1, scikit-learn 1.9.1, xarray 2026.9.0, netCDF4 and pyarrow, and a second venv (`work/.venv`) with pyfixest 0.60.0, statsmodels 0.15.0 and matplotlib 3.11.2.
3. Run `bash work/code/run_all.sh` from the scratch folder. The full run takes about 45 minutes on 16 cores. The outputs go to `work/out/` and `work/fig/`.

The climate-model step uses fixed random seeds. Small numerical differences can come from different BLAS libraries.

## Provenance

- Job: sci-1107-dell-climate-pollution-biodiversity-121a5e2faf9f; campaign 11_07_2026; topic climate-pollution-biodiversity; machine dell; account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Date of analysis: 2026-11-09.
