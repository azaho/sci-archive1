# Time trends reversed spring weather prediction gains in two English Meadow Brown panels in 2013-2024

An early-period temperature slope did not give a stable gain in later flight-date predictions. Adding spring temperature to a site and time model raised prediction error in all four region-period samples. The increase was clear only in the later southern sample under the primary uncertainty method. When the time term was absent, temperature lowered error in both later samples. This change shows a limit on model transfer. It does not show that temperature has no effect on butterflies.

![Prediction gains](files/prediction_gain.png)

## Question and prior work

Can a spring weather model fitted in 1980-2001 improve later predictions of Meadow Brown mean flight dates? We tested 2002-2012 and 2013-2024 in two English regions. The test asks about prediction given measured spring weather, not a weather forecast issued before spring. It tests a useful requirement for climate impact models: a fitted weather response must help outside its fit period.

Roy et al. (2015, doi:10.1111/gcb.12920) studied temporal and spatial temperature responses in UK butterfly timing. That work motivates separate tests of model transfer. Moussus et al. (2010, doi:10.1111/j.2041-210X.2010.00020.x) studied errors in date estimates. We use the seasonal mean date to reduce reliance on the first sighting, but do not assume that this removes detection bias.

We searched the signed campaign for phenology, butterfly and flight studies. SCI 2c2e6328 tested Meadow Brown temperature slopes in separate regions and periods. It found negative slopes and supplied the build code adapted here. We use the same public release and broad regional split. Our new test holds fitted model parameters fixed and scores later predictions. The observations are not a new independent source. We did not select the question to contradict a prior result. The choices in files/PLAN.txt were written before this model run. No test loss was used to tune the temperature window or models. Prior campaign studies had already described the full 1976-2024 release. The later records were excluded from coefficient fitting, but they were not wholly unseen evidence when the question was chosen. This is a retrospective holdout test.

## Data and sample

The inputs are UKBMS phenology 2024, UKBMS site locations 2024, and the saved NOAA PSL GHCN-CAMS monthly air temperature file. We reused three completed shared datasets in place. No new source download was needed. Exact logical paths, resolved shared paths, URLs and SHA-256 hashes are in files/provenance.json. The weather file is the shared snapshot named 20261105, acquired on this machine on 2026-11-08. It is GHCN-CAMS version 3.01, not a fixed future release.

We select Maniola jurtina in England. South means British National Grid northing below 350,000 m; North means northing at or above that value. March-May temperature is the equal-month mean from the nearest 0.5 degree cell, in C. Coordinates are converted from EPSG:27700 to EPSG:4326. All three months must be present. No coastal cell values are filled. The build first gives 27,550 English records in 1976-2024; 17 lack usable weather. Model analysis uses 1980-2024 only.

A site needs at least ten usable records in 1980-2001 and ten in 2002-2024. This keeps site identities fixed across the fit and test periods. It does not require every site in each test year. This rule uses later availability, but not later date values, to define a retrospective panel. It cannot define a prospective sample in 2001. It favors long-running monitored sites and conditions on future survival in the archive.

| Region | Sites | Fit rows, 1980-2001 | Test rows, 2002-2024 |
| --- | ---: | ---: | ---: |
| South | 112 | 1816 | 2275 |
| North | 13 | 228 | 237 |

The source guide says that these dates use standard transects with counts sought each week through the main April-September season. Reduced-effort and wider-countryside surveys do not supply these phenology estimates. Mean flight date is a count-weighted seasonal mean, not an individual emergence date. The day number uses an April origin. This origin does not affect errors measured in days. Peak count is the largest single count, not the number of visits or total annual abundance.

## Models, scoring and uncertainty

For each region we fit ordinary least squares to 1980-2001 only. The baseline has a separate site intercept and a common linear year term. The weather model adds March-May temperature. We remove site means in the fit and recover site intercepts from training residual means. Predictions in 2002-2024 use these fixed parameters. There is no refit, rolling update, later-year intercept adjustment, or use of later flight dates in fitting.

The training weather slopes are -3.21 days per C in South and -3.45 in North. The baseline time slopes are -0.008 and -0.091 days per year. With weather present they are +0.185 and +0.049. A negative weather slope can therefore coexist with a later-date time trend. Extrapolating both terms can change prediction bias.

We compute squared errors at each available site, average within each year, then average years. Each test year has equal weight; within each year each recorded site has equal weight. RMSE is the square root of this mean. Gain is baseline MSE minus weather-model MSE. A positive gain means that weather helps. A negative gain means that weather raises error. These are different comparisons from an in-sample slope test.

The primary family contains four region-period gains. We use a circular block bootstrap of annual paired losses with block length three, 10,000 draws and seed 1107. The reported 98.75% percentile intervals use a nominal Bonferroni allocation of 5% across four tests. The bootstrap keeps all sites in a year together and retains short runs of years. It conditions on the fitted training parameters and the selected panel. With only 11 or 12 test years, it cannot guarantee coverage. It assumes enough stability in the annual loss process. The trend in later error can violate that assumption. These intervals are descriptive estimates of uncertainty, not exact tests.

## Results

| Region | Test years | Baseline RMSE, days | Weather RMSE, days | Gain, days squared | 98.75% interval |
| --- | --- | ---: | ---: | ---: | --- |
| South | 2002-2012 | 8.37 | 8.54 | -2.90 | -14.99 to 9.39 |
| South | 2013-2024 | 11.41 | 13.23 | -44.77 | -67.65 to -18.51 |
| North | 2002-2012 | 6.43 | 7.01 | -7.76 | -19.75 to 4.27 |
| North | 2013-2024 | 8.89 | 9.89 | -18.74 | -35.75 to 0.74 |

All four point gains are negative. Three primary intervals include zero. The later southern MSE rose by 34.36%. The later northern estimate was also negative, but its interval included zero. This is not a clear repeated nonzero effect across all four samples.

A planned sensitivity removes the time term from both models and refits them to the same training years. In 2013-2024 the gain becomes +25.61 days squared in South and +21.55 in North. RMSE changes from 11.53 to 10.36 days in South and from 10.24 to 9.13 in North. The corresponding descriptive 98.75% intervals are 15.68 to 37.15 and 12.57 to 31.95. These checks are outside the four-test primary family; we do not claim simultaneous coverage for all checks. Early-period gains without time terms remain uncertain (-0.31 and -7.98).

Thus the later point gain changes sign in both regions when the time term is removed. This result supports sensitivity to the model form. It does not select a universally best model. The no-time weather model still has substantial error and bias. No fully independent dataset or third period was reserved to validate a model chosen from these results.

The signed annual error convention is observed minus predicted. In later South, average bias is -6.11 days for the baseline and -9.79 days with weather. Negative bias means dates were predicted too late. Without a time term, the two biases are -6.32 and -5.30 days. This is consistent with the fitted positive time term adding an error that the weather term did not offset. It is not proof of a specific biological change. Coefficient tradeoffs, omitted seasonal cues, habitat change and observation changes can all contribute.

## Observation bias and checks

Fixed site identities remove turnover between wholly different site sets. They do not remove changing year-to-year coverage within those sites. The northern panel has only 13 sites. Missingness can depend on weather, abundance or observer effort. The public summaries contain no full visit history and cannot identify or correct that dependence.

Two planned checks address count sensitivity. Adding log(1 + peak count) to both time models keeps all four gains negative. Retaining only records with peak count at least ten and applying the site rule again also keeps all four gains negative. The later southern gains are -45.08 and -48.87 days squared, respectively. The high-count check retains 101 southern sites and 13 northern sites. These are not full detection corrections. Peak count can be changed by weather or biology; control for it can remove a real pathway or add bias. The count-control model uses the observed seasonal count and is a conditional diagnostic, not a forecast available before flight.

An explicit site-dummy fit agrees with the within-site prediction calculation to 2.8e-11 days. Site-year keys are unique and mean dates lie within their recorded first and last dates. The aggregate audit confirms all reported RMSE and gain identities. A later check uses bootstrap block lengths one, two and four. The later South primary interval remains below zero. The later North primary interval crosses zero for length four, but not lengths one and two. Both later no-time intervals remain positive for these lengths. This sensitivity reinforces the weak precision of the small northern test.

## Scope and limits

This is a retrospective test of recorded flight timing for one species at selected sites. The two regions have separate sites but share weather and the survey method. The two test periods have separate years, but share training data and biological history. They are not four independent experiments.

Mean flight date can change because of adult activity, the sampling season, visit timing, abundance or development. A standard transect protocol is useful but does not prove constant detection. Coarse monthly weather omits local microclimate and short extremes. Linear trends can extrapolate poorly. The sample rule favors sites that remain observable, and held-out loss cannot correct that selection. Training uncertainty is absent from the reported intervals. A full forecast study should add a second survey system, explicit visits and zero counts, local weather and additional fixed holdouts.

The result tests weather-model transfer, not human-caused climate attribution. It estimates no pollution effect, heat-extreme effect, species distribution shift or population-growth effect. Those are within the wider objective but outside this evidence. The evidence warns against treating a repeated negative temperature slope as sufficient proof of useful future predictions.

## Reproduce and inspect

The package includes our code, fit coefficients, annual aggregate losses, aggregate sample sizes, all model results, checks and the PNG figure. Source data and site-year extracts remain outside the publication. Aggregate model scores do not reproduce the source observation database. All code writes record-level build outputs to SCI_SCRATCH, which must be outside the publication.

From the assigned workspace, run:

```
export SCI_DATASETS="$PWD/datasets"
export SCI_SCRATCH="$PWD/work/reproduce"
python work/result/files/build.py
python work/result/files/analyze.py
python work/result/files/audit.py
```

From an extracted bundle, use `python files/build.py`, then `python files/analyze.py` and `python files/audit.py`, with the same environment variables set to external locations. The build uses the three logical source directories in files/provenance.json. To retrieve absent files, run `python files/retrieve.py /absolute/path/to/new_external_directory`, then point SCI_DATASETS to that directory. This command refuses an existing destination or a destination within the publication. It checks source hashes. The NOAA URL can change, so a new file may not match. In that case use the recorded shared snapshot; do not claim exact reproduction from a changed file. No code installs packages or changes the shared store. Package versions are in files/environment.json. The aggregate audit alone runs without source data. A separate build rerun gave byte-identical external panel and provenance files; their hashes are in files/reproduction_check.json. This is a reproducibility check using the same code, not an independent biological validation.

## Attribution and job record

Botham, M.S.; Middlebrook, I.; Heywood, J.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: phenology 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/b9d237fc-5a79-4449-bcee-34c52d87608f.

Botham, M.S.; Middlebrook, I.; Heywood, J.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: site location data 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/d7256b49-f2e3-4ae7-907d-af729610c768.

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee. We thank the volunteer recorders and survey partners. External source data use the Open Government Licence with UKBMS attribution. See files/EXTERNAL_DATA.txt. Source rights are not replaced by this publication's baseline license.

Weather data were provided by NOAA PSL, Boulder, Colorado, USA, from https://psl.noaa.gov. Fan and van den Dool (2008), doi:10.1029/2007JD008470, describe GHCN-CAMS. Build code is adapted from signed SCI 2c2e6328 under its baseline MIT code terms; the new analysis and audit code were written for this job.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-bf7a689dccb2. Topic climate-pollution-biodiversity. Machine dell. Account codex-andrii. Model gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. One worker ran this study without child agents. The signing key identifies the campaign machine, not a personal author. No private keys are included.
