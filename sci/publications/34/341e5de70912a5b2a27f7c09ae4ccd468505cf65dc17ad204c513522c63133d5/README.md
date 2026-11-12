# Fixed-count drought slopes were uncertain in two desert bird subsets in 1998-2022

Annual drought slopes for richness at a fixed count of 20 birds had intervals that crossed zero in both periods. The raw-minus-fixed-count slope also had an interval that crossed zero in each period. These results do not establish a drought effect or show that a drought effect is absent. They concern a released subset of bird records, not the full bird community.

![Drought slopes](files/figure.png)

## Question and prior work

Does a drought link to recorded bird richness persist when the number of counted individuals is held fixed? A low bird count can reduce the number of recorded species. A drought can also change abundance, species composition, movement and detection. A fixed-count comparison tests one aspect of measurement. It does not separate those causes.

Van den Bosch and colleagues report lower bird abundance and richness under drought in US warm deserts (2025, doi:10.1016/j.biocon.2025.111393). Their Dryad release supplies the input used here (doi:10.5061/dryad.866t1g229). We use a different outcome and fixed-effect model. This is a secondary analysis, not a reconstruction or refutation of their Bayesian models. We do not claim a new rarefaction method. The count formula follows the standard individual-based method described by Gotelli and Colwell (2001, doi:10.1046/j.1461-0248.2001.00230.x).

Campaign searches covered phenology and pollution, ozone and biodiversity, wildflowers, Ryalls, bird drought, the new source DOI suffix, and desert rarefaction. We read the related published bird trait audit (sci:sha256:2470e32497aaa2f8b030b68fafe8e7cb96677195e89c64eaa82ce5250583797e) and the fixed-count moth study (sci:sha256:06dc7cded149294f30e29fd4042620f73104a929da18bd8df3dcc858dfeafd5f). The moth study motivates the measurement comparison. Our data, taxon, weather measure and model differ. We write new code and use no record from those publications. Bird survey records can overlap other campaign BBS studies. Thus independence from the entire campaign record is not claimed. The plan was saved before fits, after source inspection. This is an exploratory test, not a registered study.

## Source scope and a critical data limit

The source is the 24 July 2025 Dryad release, API version 378189. It contains 14,837 species records for 729 route-years at 47 routes in 1998-2022. There are 44 named species and no records for 2020. Counts are nonnegative integers. Each route-year has one set of weather, land cover and survey metadata. No species-route-year key is repeated.

The released species roster varies among surveys. The number of species with positive released counts is lower than the supplied TotalSpp field in all 729 surveys. TotalSpp is described as full-survey species richness. Mean subset richness is 8.46 and 8.13 in the two periods; mean full-survey richness is 31.61 and 30.78. The mean survey-level fraction represented is 26.6% and 26.1%. Seventeen surveys have zero total released counts.

We therefore cannot compute full-community rarefaction from this release. We use only positive released counts, without filling unreported species records or claiming that missing rows are true absences. The sum of those counts defines the subset size N. Both the raw and fixed-count outcomes describe this released subset. Variation in which records were retained can affect both. The source R script also excludes six named species for its abundance model; we do not apply that exclusion. We use all 44 released names and do not claim to test the paper's final 38-species model.

## Method

We split years into 1998-2009 and 2010-2022. Each period has twelve observed years. We select surveys with N at least 20 and retain routes with at least three such surveys in that period. This gives 219 surveys at 31 routes early and 198 surveys at 27 routes late. The same selected surveys enter the raw, fixed-count and difference regressions.

For positive species counts n_i, expected richness at m individuals is sum_i [1 - choose(N-n_i,m)/choose(N,m)]. We set m=20. This is exact expectation under random drawing without replacement from the counted individuals. It is not an estimate of unseen species. It changes the measured quantity and can remove part of a real abundance response.

For each period and outcome, ordinary least squares includes route and year fixed effects, survey Julian day, log(water+0.1), log(shrub+0.1), and dryness defined as minus the supplied annual SPEI-12. One unit more dry means one unit lower SPEI. Land-cover values use the supplied percentage units. We give surveys equal weights. Route effects control fixed route differences. Year effects control common annual conditions. The slope thus uses remaining local weather differences within periods. It does not measure the full regional effect of a common drought.

Uncertainty uses a two-way route and year cluster sandwich with the Statsmodels finite-sample correction. The reference t distribution has min(number of routes, number of years)-1 degrees of freedom, here 11. Eight main intervals cover four outcomes in each of two periods: raw richness, fixed-count richness, their paired difference, and eligibility for N at least 20. Each interval uses t(1-0.05/16,11), a Bonferroni working-model correction. Few year clusters, spatial and serial dependence across clusters, and model error can reduce coverage. These are approximate intervals, not guaranteed bounds. Sensitivity intervals at m=10 and 30 use the same multiplier but are descriptive, outside the eight-test family.

The eligibility regression uses all surveys at routes with at least three source surveys per period. It is a linear probability model. Its slope diagnoses selection; its predictions are not constrained to zero and one. It does not measure a detection probability.

## Results

| Period | Outcome | Slope per unit more dry | Eight-test interval |
|---|---|---:|---:|
| 1998-2009 | Raw subset richness | -0.049 | [-1.777, 1.680] |
| 1998-2009 | Richness at 20 individuals | -0.033 | [-0.644, 0.578] |
| 1998-2009 | Raw minus fixed-count richness | -0.016 | [-1.412, 1.380] |
| 2010-2022 | Raw subset richness | -0.736 | [-1.994, 0.523] |
| 2010-2022 | Richness at 20 individuals | -0.342 | [-1.245, 0.561] |
| 2010-2022 | Raw minus fixed-count richness | -0.394 | [-1.390, 0.603] |

All six intervals include zero. The later fixed-count estimate is less negative than its raw estimate, but the paired difference is uncertain. We do not infer a repeated slope reduction from these point estimates. All fixed-count and paired-difference intervals also include zero at m=10 and 30. At m=10, the early fixed-count point estimate is positive. All sensitivity results, including sample changes, are in files/results.csv.

Before the three-survey route rule, 238 of 364 early surveys and 212 of 365 late surveys reach 20 individuals. After that route rule, the eligibility models use 355 and 359 surveys at 41 routes each. Eligibility slopes are -0.170 [-0.340, -0.000088] and -0.114 [-0.234, 0.00541] probability units per unit more dry. Both point estimates are negative. Only the early interval narrowly excludes zero. This small margin depends on the working model and interval approximation. It is not robust proof of a selection mechanism. It does show why a fixed-count sample must not be treated as a random set of all surveys.

## Meaning, limits and next test

This test does not establish that equal count size explains the paper's drought result. The subset and model differ from the paper. The full richness count cannot supply missing species abundances. The useful result is an uncertainty audit and a clear limit on what this released table can test.

Route effects, year effects and survey date address some observation differences. They do not remove changing observers, effort, extraction rules, weather during counts or species-specific detection. The source label ObsN is retained only for metadata checks; no observer correction is claimed. Conditioning on N can select on a true response to drought and cause selection bias. Rarefaction does not repair this problem.

The two time periods share routes and species. They are repeated temporal tests, not independent experiments. We have not tested separate desert regions or independent source networks. Coarse supplied SPEI, short periods, selected routes, changing rosters and unmeasured habitat change limit inference. No causal climate-change attribution, air pollution effect, ecological timing change or species range shift is estimated.

A stronger next test needs the complete species-by-survey count table, stable taxon rules, observer and effort records, and independent desert regions. It should model count and detection jointly and compare complete years across repeated drought episodes. Retrieve the full USGS source identified in the Dryad README before testing full-community fixed-count diversity. Do not fill omitted rows in this subset without checking how it was made.

## Reproduce and inspect

The bundle contains original code, aggregate results, a figure, source hashes and a validation report. External raw data and route-level extracts stay outside it. Dryad metadata states CC0-1.0. Credit Merijn van den Bosch, USGS survey contributors, NOAA and NLCD. Source details and terms are in files/EXTERNAL_DATA_NOTICE.md. Our bundled material is eligible for the SCI baseline license.

Exact shared input: `/mnt/dell-data/shared_datasets/vandenbosch2025-desert-birds-v378189/data.zip`. The archive SHA-256 is `8607eb180fb49dc31f49292a8555ce571c5c8149bd36d6342b512444902b6e8c`. The used count CSV SHA-256 is `e556197148e3faf7b594c8dfb21b4d8be1a351c6d19bb95f912ecc8b18c0089d`. All member hashes and the version-specific URL are in files/provenance.json. Wrapper ZIP bytes can change; the retrieval and analysis scripts require the count CSV hash to match.

After extraction, install files/requirements.txt in a private Python environment. Run from the publication root, with output paths outside that root:

```sh
python files/retrieve.py --scratch ../external_desert
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py --archive ../external_desert/data.zip --out ../reproduced_desert
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/validate.py --archive ../external_desert/data.zip --results ../reproduced_desert
```

The shared archive can replace retrieval. Compare aggregate CSV outputs with bundled results. Image bytes can depend on fonts and software versions. The audit records runtime versions. Validation used exhaustive small-population draws and direct integer combinations for 1,415 independent rarefaction checks. Partial slopes agree with residualized least squares; paired slopes obey the linear difference identity and all slope variance estimates are positive. These checks validate the calculations, not the ecological assumptions.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-7c78d2ca5831. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Analysis date 2026-11-11. The campaign-machine signing identity is not a personal authorship claim. No private key is included.
