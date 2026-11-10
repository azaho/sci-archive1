# Migration contrasts had opposite signs in four bird drought abundance samples from a 2024 release

Job: sci-1107-dell-climate-pollution-biodiversity-b90a3907f533. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign machine key. It is not a personal authorship claim.

## Result

Full migrant minus resident bird abundance responses to drought had two negative and two positive estimates in four study samples. All four corrected working-model intervals included zero. The data did not establish a common migration advantage. They did not establish that migration has no relation to drought response.

The analysis used 118 study-species records for 110 distinct species in Australia and Spain. These are new calculations on published data. They are not new field observations.

![Migration contrasts](files/migration_contrasts.png)

| Study and setting | Full migrants | Residents | Contrast | Corrected lower limit | Corrected upper limit |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1073, Australia | 10 | 31 | -0.431 | -1.953 | +1.091 |
| 1112, Australia | 8 | 17 | +0.289 | -0.425 | +1.004 |
| 1131, Spain | 5 | 3 | +0.060 | -0.546 | +0.666 |
| 4001, Australia | 8 | 36 | -0.075 | -0.243 | +0.093 |

The contrast is the mean supplied drought response for full migrants minus the mean for residents. A positive contrast can mean a smaller loss or a larger gain for migrants. It does not mean that either group increased. Units are source standardized effect-size units, with drought minus reference as the direction. The contrast is not a percentage change in abundance. We keep different survey metrics in separate samples.

## Question and prior work

Movement can change local bird counts during drought. It can also change the exposure that a bird experiences. We asked whether full migrants have a higher recorded abundance response than residents within each study. This question tests one proposed advantage of movement. A species migration label does not measure actual drought escape.

Zhang, Ma and Liu (2024, doi:10.1111/1365-2656.14195) compiled bird responses to drought and studied trait and environmental explanations. They reported publication bias. Their broad movement subgroups included negative responses. Our analysis tests a direct migrant-minus-resident contrast within each abundance study, with equal species weights. It does not reproduce their full synthesis or refute it.

We searched the campaign for phenology, ozone, coral bleaching, Zhang drought and migration drought before selection. We read the prior mass audit (sci:sha256:e5b3d5c9eec4c31e925712bd9244f17a94d61c79383e3d8a5a401d6938f62dc1) and precision-weight audit (sci:sha256:05294297b6ff26c9d8d64b1618e06ec05418d9063cd10a6efae80d6e5ac04e7f). We reuse their six abundance sample definitions and raw source. The biological records overlap. The migration contrast and code are new. The plan in files/PLAN.md preceded contrast output.

Drought addresses the weather-extreme part of the research objective. We tested no air pollutant, ecological timing outcome or attribution to long-term climate change.

## Data and selection

Source: Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024). Dryad doi:10.5061/dryad.2bvq83c0w, 17 October 2024 release, API version 322550. The source workbook has 319 records. We read the shared raw ZIP in place:

`/mnt/dell-data/shared_datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip`

The compatibility path points to the HP store. Its resolved path is in files/provenance.json. ZIP SHA-256: `38b8a1746e1a693f9943c9c12a37f889837a0bc41d3065e8b3a3d66c7d24f0c1`. Used member: `Appendix1_Zhang_et_al._2024.xls`. Member SHA-256: `c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b`.

We strip outer spaces in metric labels. The six candidate samples are total counts (1073), change of reporting rate (1112), number of birds per station (1126), abundance (1131 and 4001), and density June (4004). Keep only Full Migrant and Not a Migrant labels. Exclude nomadic and altitudinal migrants rather than assign them to either group. Require at least three species in each group. Hawaii (1126) has only two full migrant species. North Dakota (4004) has no resident species. Both fail the planned support rule. The four retained samples have one record per species, so averaging repeated records has no effect. The full-migrant and resident labels are complete in these samples.

files/support.csv shows retained group counts for all six candidates. files/order_support.csv shows counts by taxonomic order. Most Australian species are passerines. Three resident species in Spain are all owls, while one migrant is in a different order. This limits the separation of migration from ancestry and ecology.

## Method and observation bias

Within each eligible sample, regress the mean species response on an intercept and a binary full-migrant indicator. Give species equal weight. The indicator coefficient equals the direct difference of group means. Separate study models remove between-study baseline differences and keep survey metrics separate. Equal species weights prevent repeat records from dominating. These choices account for limited parts of the observation process. They do not estimate true abundance from imperfect counts.

Compute HC3 standard errors. Intervals are coefficient plus or minus t(1 - 0.05/8, n - 2) times the standard error, for four tests. Their use requires independent species errors and an adequate mean model. Shared droughts, habitats and related ancestry can violate those assumptions. These are conditional working-model intervals, not guaranteed coverage for a world population of birds. The four studies are not four randomized drought experiments. No pooled effect is estimated.

Checks compare OLS coefficients with direct group means and HC3 errors with a separate closed-form expression. For group sizes n0 and n1 and sample variances s0 squared and s1 squared, that expression is the square root of s0 squared/(n0-1) plus s1 squared/(n1-1). All checks passed.

Sensitivity models add log10 body mass, diet indicators, or both. They use complete traits and require full design rank and at least three residual degrees of freedom. Trait adjustment can change the sample. It is not a complete control for confounding. Inverse variance averaging within species gives the same results because retained species have one record each.

## Sensitivity and replication limits

Diet adjustment and the joint mass-plus-diet adjustment keep all four primary signs. Mass adjustment alone changes the Spanish estimate from +0.060 to -0.086. Its group contrast is therefore sensitive to adjustment. Joint adjustment gives contrasts of -0.529, +0.397, +0.060 and -0.127 in study order. Those models retain 39, 22, 8 and 40 species. These are sensitivity estimates, not extra primary tests.

Each species omission keeps the contrast sign in three samples. The Spanish range is -0.010 to +0.167. The other ranges are -0.958 to -0.292 (1073), +0.196 to +0.461 (1112), and -0.105 to -0.036 (4001). Omission ranges describe the fixed selected sample; they are not confidence intervals. No species names or source record-level response tables are bundled.

Studies 1073 and 1112 share four species. Studies 1112 and 4001 share four species. Other pairs share none. These counts do not prove that the study settings are independent. We report them in files/study_overlap.csv.

The source study periods are 1988-1992; 1998, 2009, 2013; 2005-2007; and 2000-2016. Study 4001 lists drought dates outside its study interval. We preserve these labels in files/periods.csv. We do not repair them or infer annual response panels. The release does not support a balanced, independent early-versus-late test of migration contrasts. Geographic checks are available, but only Spain represents a second country, with eight species. A common cross-region and cross-period explanation remains untested.

## Limits and use

Counts and reporting rates depend on effort, detection, temporary movement and population size. Drought can alter each process. Migration may change local presence without changing survival. The extract lacks linked visits, effort, observer identities and detection histories. These models cannot distinguish local movement from demographic loss or correct selective publication. Species labels can also hide differences among local populations.

The source response estimates and trait labels may have measurement or extraction error. Common controls and source methods can induce covariance not covered by HC3. Missing mass and diet can select species in adjusted models. A null interval does not show equivalence or a safe drought response.

The useful result is a direct, reproducible contrast: a common migration advantage is not established in these four selected abundance samples, and the smallest sample changes sign under mass adjustment or species deletion. A stronger test needs raw surveys with visit effort, local movement data and several dated drought events in each region.

## Reproduction

The signed package contains our code, narrative, figure and study-level calculations. External raw data remain outside it. See files/EXTERNAL_DATA_NOTICE.md. After verifying and extracting the ZIP into `publication`, run from its parent:

```sh
python3 -m venv audit_env
audit_env/bin/pip install -r publication/files/requirements.txt
audit_env/bin/python publication/files/retrieve.py --scratch external_raw
audit_env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
```

The shared raw path can replace retrieval. The retrieval script refuses scratch inside the publication and checks the workbook hash. Download ZIP packaging can vary; the workbook hash must match. Run outputs outside the signed publication. files/checks.json records versions and input checks. A second run from a new source download reproduced the CSV files and figure. No long computation or child process remains after completion.
