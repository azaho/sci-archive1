# A fixed trait model raised mean prediction error across six bird drought abundance samples from a 2024 release

Job: sci-1107-dell-climate-pollution-biodiversity-ec9cdda1fa2d. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign machine key, not a personal authorship claim.

## Result

A fixed model of bird traits did not improve mean prediction error for relative drought responses in six abundance samples. Mean squared error (MSE), with each study given equal weight, rose from 0.43915 to 0.47776 when each study was held out. This is an 8.79% increase. When each country was held out, MSE rose to 0.51680, a 17.68% increase. Both tests lowered MSE in only one of six study samples. These are finite-sample scores, not estimates with known confidence coverage.

The analysis used 179 source records, 151 study-species units and 143 distinct species names. It tests a specified model on old public data. It adds no field observations.

![Error ratios by study and holdout rule](files/transfer.png)

Each point is the model MSE divided by the equal-response reference MSE. A ratio below one shows lower error. The horizontal axis has a log scale. These points have no sampling error bars. The two panels reuse the same test records with different training exclusions.

| Study and setting | Species | Reference MSE | Study-held-out MSE | Country-held-out MSE |
| --- | ---: | ---: | ---: | ---: |
| 1073, Australia | 47 | 0.92848 | 0.96276 | 0.97690 |
| 1112, Australia | 26 | 0.40470 | 0.42239 | 0.49965 |
| 1126, Hawaii, USA | 15 | 0.78901 | 0.73009 | 0.77305 |
| 1131, Spain | 8 | 0.04083 | 0.10200 | 0.10200 |
| 4001, Australia | 47 | 0.01814 | 0.16405 | 0.21068 |
| 4004, North Dakota, USA | 8 | 0.45377 | 0.48528 | 0.53854 |

The large error ratios for study 4001 partly reflect its small reference error. The primary summary is the ratio of mean study errors, not the mean of the six ratios. Study-specific scores and both summaries are in files/scores.csv and files/summary.csv.

## Question and prior work

Can measured species traits predict which birds have a lower recorded abundance response to drought in another study? This question matters if trait-based risk assessment is used outside its training region.

Zhang, Ma and Liu (2024) studied trait and biome explanations in a synthesis of bird demographic responses. Their paper reported population-level links for diet and life-history traits, and noted publication bias. Our test is narrower. It uses abundance measures and asks about transfer of a joint model. It does not reconstruct or refute their full meta-analysis. Source: [Zhang et al.](https://doi.org/10.1111/1365-2656.14195).

We searched the campaign before choosing this question. We read the prior precision-weight audit, body-mass audit and species-rank audit cited in sci.json. They found different slope signs and little overlap of species between studies. We use the same six study-metric definitions but new code. This is a follow-up on overlapping biological records, not independent validation of the prior campaign results. Unlike a rank test on common species, this model can predict from traits for species absent from training.

Study and country exclusions follow the purpose of structured validation: the test records must represent the intended transfer task. See [Roberts et al.](https://doi.org/10.1111/ecog.02881). We do not make random row splits. Drought addresses the weather-extreme part of the objective. No air pollution, ecological timing or causal climate-change effect is tested.

## Data

Source: [Zhang, Ma and Liu, Dryad](https://doi.org/10.5061/dryad.2bvq83c0w), 17 October 2024 release, API version 322550. The exact shared input is:

/mnt/dell-data/shared_datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip

This is the shared compatibility path to the HP store. The resolved path, URL and hashes are in files/provenance.json. ZIP SHA-256: 38b8a1746e1a693f9943c9c12a37f889837a0bc41d3065e8b3a3d66c7d24f0c1. Used member: Appendix1_Zhang_et_al._2024.xls. Member SHA-256: c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b.

We remove outer spaces from metric labels. We keep study 1073, total counts; 1112, the change of reporting rate; 1126, number of birds per station; 1131 and 4001, abundance; and 4004, density June. These are the six samples in the prior weight audit with at least eight species. We exclude survival and reproductive metrics.

We average supplied yi within each study and species. The source defines yi as a standardized drought-minus-reference response (Hedges' d). A negative value means a lower recorded metric under drought. Species matching removes outer spaces and folds case; it does not resolve taxonomic synonyms. Only Hawaii has repeat rows per species in this selection. We use species-study medians for numeric traits and check that available trait values within a unit agree. Every unit has a finite response. We do not use vi for fitting or score weights.

Trait inputs are adult body mass, maximum longevity, mean clutch size and diet. Numeric inputs are log-transformed. Missing numeric traits affect 2, 0, 7, 0, 12 and 1 species in study order 1073, 1112, 1126, 1131, 4001 and 4004. Missing diet affects three species in 1112 and one in 4001. Training medians fill numeric gaps. Test records never set these medians. Missing diet has its own indicator. The five other diet indicators are the source categories: fruits/nectar, invertebrates, omnivore, plants/seeds and vertebrates/fish/scavenging. The model has nine features before removal of zero variation through scaling. Source traits can themselves include taxonomic imputations.

## Method

The exploratory plan in files/PLAN.md was written after we inspected the schema, missing counts and study dates, before any prediction score. We selected the features, penalty and sensitivity rules at that point. We did not tune them with the test scores.

For training study s, subtract its mean response and each feature mean. Give each study total weight 1/S and each of its species equal weight. Scale each centered feature by its training weighted standard deviation; a scale below 1e-12 is set to one. Fit ridge coefficients b to minimize:

mean over training studies of mean over species of (centered yi - centered scaled traits times b)^2 + 0.1 times sum(b^2).

The coefficient formula is (X'WX + 0.1 I)^(-1)X'Wy. Log transforms use natural logs. The missing-value median uses the training species-study units. Fit a new model for each holdout.

For the study test, exclude all rows of the held-out study. For the country test, exclude 1073, 1112 and 4001 together for Australia, 1126 and 4004 together for the USA, and 1131 for Spain. Thus the country test has three training exclusions and six study scores. The USA group includes very different Hawaiian and mainland systems. It is a coarse geographic exclusion.

Center test features within each study and predict their relative responses. For scoring only, subtract the observed test study mean from its responses. The reference predicts zero for every centered response. Therefore this is a test of species contrasts conditional on a study, not an absolute forecast of abundance loss. It does not estimate a new study's unknown average response. Using a test outcome mean in scoring cannot change fitted coefficients or predictions.

This score also has a pairwise interpretation. For centered residuals e in a study with n species, the mean of (e_i - e_j)^2 over unordered pairs is 2n/(n-1) times mean(e_i^2). Thus the same error ratio tests species-response differences without requiring a forecast of the study mean. The pairs are not independent replicates.

MSE is the squared error averaged within each study, then averaged equally across the six studies. Mean absolute error is a secondary score. Equal species weights prevent repeated source rows from directly dominating a study. Study centering removes its common response offset. Neither step corrects species-dependent observation error.

## Sensitivity and uncertainty

With penalties 0.01 and 1, study-held-out mean MSE still rose by 10.92% and 2.18%. Country-held-out mean MSE rose by 27.88% and 3.09%. These checks do not show that any penalty or model must fail.

Excluding from training all species names present in the test study raised primary mean MSE by 9.40%. This guards against direct shared-species transfer. Country exclusion already separates all repeated species in this selection, so that check is unchanged there.

Complete numeric and diet cases gave increases of 5.67% for study exclusion and 22.31% for country exclusion. This uses a selected subset and cannot resolve nonrandom missing traits. Primary absolute error improved in two of six study tests and one of six country tests. Within-study fitted MSE fell in all six samples, by 8.35-96.85%; these fitted scores have no validation value.

Deleting each test study from the summary, without refitting the stored predictions, leaves MSE increases of 3.28-15.74% for study exclusion and 10.45-26.10% for country exclusion. These are sensitivity ranges, not confidence intervals. They are generated by files/score_deletions.py.

The data have only six selected study samples and three country groups. Folds share training records and related species. We give no population confidence interval or p-value based on treating species or folds as independent droughts. Error includes noise in the supplied response and any original standardization error. The analysis does not separate ecological prediction error from measurement error.

## Observation bias, dates and limits

Recorded counts, reporting rates and density estimates depend on detection, observer effort, movement and true abundance. Drought and traits can affect all four. The source extract lacks linked observer and visit histories. Centering removes common study offsets, but cannot remove trait-dependent detection changes. Equal weighting changes the target population of species; it does not estimate detection-corrected abundance. The source synthesis also reports publication bias.

Differences in response metrics, event severity, shared ancestry and habitat can explain failed transfer. We do not identify which explanation is correct. A nonlinear model, a different trait set, better observations or a model with local drought covariates might perform better. This result does not show that traits have no ecological role.

Study periods are 1988-1992; 1998/2009/2013; 1998-2011; 2005-2007; 2000-2016; and June 1987-June 1989. Study 4001 lists drought dates that include years outside its stated study period. We do not repair that inconsistency. The extract cannot provide a balanced early-to-late validation panel. Country exclusions reduce geographic overlap; they do not verify independent drought events within countries. Temporal replication remains untested.

The practical result is limited but useful: this fixed joint trait model has higher error than equal relative response in these selected transfer tests. Trait-based conservation ranking needs external validation with comparable metrics, clear event dates and explicit observation effort.

## Reproduction and rights

The package contains our code, text, static figure and aggregate model results. The source workbook and species-level tables stay outside the signed package. Dryad states that submitted datasets are published under CC0. Attribution and external terms are in files/EXTERNAL_DATA_NOTICE.md. The exact SCI baseline LICENSE applies to our bundled material. It does not replace external terms.

After verifying and extracting the ZIP into publication, run from its parent:

```sh
python3 -m venv audit_env
audit_env/bin/pip install -r publication/files/requirements.txt
audit_env/bin/python publication/files/retrieve.py --scratch external_raw
audit_env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
audit_env/bin/python publication/files/validate.py --source external_raw/drought_v20241017.zip --out reproduced/validation.json
audit_env/bin/python publication/files/score_deletions.py --scores reproduced/scores.csv --out reproduced/score_deletions.csv
```

The exact shared ZIP can replace retrieval. The retrieval script refuses publication-internal output and existing targets. Analysis validates the workbook hash. A newly packaged ZIP may differ while the workbook remains identical. Outputs must be outside the signed package.

Checks confirm source selection, trait consistency, study exclusion and the pairwise score identity. An independent augmented least-squares solver matched ridge predictions to within 1.4e-15. Replacing held-out responses with arbitrary values did not change predictions. Repeat runs gave identical numerical tables and figure bytes before the final figure layout change. The final layout uses the same scores. Runtime versions and checks are included. No private scratch is needed after retrieval. All computations stopped before signing.
