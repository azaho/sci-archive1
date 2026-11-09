# Within-stratum depth trend intervals included zero in two US trawl surveys in 1982-2019

We tested whether deeper catches also showed a change in catch depth relative to survey hauls within fixed strata. We used public OceanAdapt data from the eastern Bering Sea and Northeast US fall surveys. We kept a fixed taxon list and fixed strata in each region. We tested 1982-2000 and 2001-2019 separately.

All four adjusted intervals for the within-stratum depth trend included zero. The point estimates were +0.52, -0.49, +0.24 and -0.46 m per decade. The Northeast late-period total depth trend was +4.85 m per decade, but its within-stratum component was -0.46. Thus the total trend did not require a positive within-stratum trend in this sample. This does not prove that animals did not move deeper. It does not establish a climate cause.

![Depth trend decomposition](files/outputs/depth.png)

## Question and prior work

Marine depth indicators can help assess changes linked to warming. Pinsky et al. (2013; doi:10.1126/science.1239352) related shifts in marine distributions to local climate velocity. OceanAdapt computes annual catch-weighted positions on a consistent survey footprint and uses taxa caught in every year. A fixed footprint does not fix the depth of every sampled haul. Also, catch can change across strata that have different mean depths. Can those two parts be separated from the catch-depth difference within strata?

Our contribution is an exact three-part decomposition of a catch-depth indicator, with an observation-process check. It is a small method audit. It does not reproduce the official OceanAdapt indicator, which uses its own stratum positions and weights. We use actual haul depth within strata.

We searched the campaign for climate, biodiversity, phenology, bleaching, OceanAdapt and depth trawls before the complete estimates. We read SCI publications 574c7309f1f213014bcb4d616918aee2098602eb89e7a4b233d5f5dea755e269 and f07015b2c467a3942a4bbf2f81bd3db886e2db9b97768c7e878aa51c5e9bf3a8. They tested effects of survey weights on latitude estimates. We used their public source scope and duplicate-record warnings to design a depth test. We did not reuse their derived estimates. Our raw observations overlap those studies, so this is not an independent confirmation of them. The two regions give separate regional checks. The two periods share taxa, strata and survey methods. Independence across regions and periods is not exact.

## Data and sample

We reused this shared file in place:

`/mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz`

The same file is available through `datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz` in the assigned worktree. The compatibility path points to the campaign SSD store. We did not read the failed disk or change shared data.

Source version: pinskylab/OceanAdapt Git commit `0d4bcaffe649e970674fe165fe892ab4d787e76a`. Source URL:

https://raw.githubusercontent.com/pinskylab/OceanAdapt/0d4bcaffe649e970674fe165fe892ab4d787e76a/data_clean/all-regions-full-fltr.csv.gz

File size: 30,884,574 bytes. SHA-256: `cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41`. The code checks this hash before analysis. `files/outputs/provenance.json` records the exact resolved shared path, source, hash, package versions and sample audit. The package also preserves the source metadata for NOAA AFSC and NEFSC. Those files state that depth is in meters and describe survey processing. Their URLs and hashes are in `files/source/provenance.json`.

We selected years 1982-2019. The Northeast source has no 2017 observations; we did not fill the gap. Each region-year-haul has one depth, stratum and area. We counted all unique hauls from the source catch table, including rows without a named taxon. We removed two Northeast hauls with missing depth. No Bering haul had missing depth. We kept strata with at least one valid-depth haul in every available survey year. This left all 10 Bering strata and 13,427 hauls, and 61 Northeast strata and 9,326 hauls. Areas were constant within strata.

We required scientific names with two alphabetic words in genus-species form. We excluded a whole taxon if any haul had conflicting catch values for it. This removed Platichthys stellatus in the Bering Sea and Placopecten magellanicus in the Northeast. We removed 5,538 identical Northeast haul-taxon catch repeats. We retained taxa with positive catch in every available year after these rules: 59 Bering taxa and 62 Northeast taxa. Lists are in the audit file. These are persistent selected taxa, not total biodiversity. Name format is not a full taxonomic validation. Missing focal catches are treated as zero, conditional on the catch table representing all survey hauls. Completely absent hauls cannot be found from this table.

## Exact decomposition

For a taxon in a year, let Q_s be the sum of weight catch per unit effort in stratum s; QD_s is the sum of catch times depth. Let n_s be all recorded valid-depth hauls in that stratum and year, A_s its area, and dbar_s the unweighted mean depth of those hauls. Let d0_s be the equal-year mean of dbar_s over 1982-2019. It is fixed through time. Define b_s = A_s Q_s/n_s and Z = sum(b_s). Then:

- Total depth T = sum(A_s QD_s/n_s)/Z.
- Between-stratum part B = sum(b_s d0_s)/Z.
- Haul-depth part H = sum[b_s (dbar_s - d0_s)]/Z.
- Within-stratum part W = sum[(A_s/n_s)(QD_s - Q_s dbar_s)]/Z.

The identity T = B + H + W holds for every taxon-year. We then take the unweighted mean across the fixed regional taxon set. The identity still holds. The annual means are the analysis units. We do not treat taxa as independent statistical replicates. Positive trends mean deeper water.

B changes when the relative catch contribution of fixed strata changes. H measures the catch-weighted change in sampled stratum depth relative to its fixed reference. W measures catch depth relative to the same year's haul-depth mean within each stratum. A taxon with constant catch at every haul has W = 0. Thus W removes the simple sampled-depth mean under that benchmark. It does not remove all observation bias. Changing haul positions, catchability and within-stratum habitats can change W. Even fixed taxon-specific depth differences within strata can give changing W when biomass shifts between strata. W is not a pure measure of individual movement or depth choice. B is not bias: it can include real ecological redistribution. H is not proof of bias either. The decomposition separates arithmetic contributions, not causal processes.

## Trend tests and uncertainty

For each region and period, we fit an intercept and a linear year term to each annual mean. Slopes use meters per decade and actual calendar years. The eight primary estimates are total and within-stratum slopes in four samples. We use a heteroskedasticity and autocorrelation consistent covariance estimate with three observed-year lags and the finite-sample correction in statsmodels. Intervals use a t quantile with n-2 degrees of freedom and a Bonferroni factor of eight. Each marginal interval has nominal coverage 99.375%, with an intended family coverage of 95%. This is an approximate procedure, not a guarantee with 18-19 observations. The missing Northeast year makes observation lags differ from calendar lags. The source table cannot give design-based uncertainty from all original survey sampling units.

The decomposition and all slopes were specified before the first complete fit. The period split is a convenient check, not a detected climate break. We also computed lags one and five, a Northeast late-period model with a post-2008 step, and omission of each taxon in turn. These are sensitivity checks. The step addresses the documented survey vessel and calibration change; it can also absorb ecological change. It does not identify a vessel effect. Intervals for B and H in the full CSV are working intervals only, outside the eight-test family; we make no separate significance claim for them.

## Results

All values below are meters per decade. Brackets give the eight-test adjusted working intervals. B + H + W equals T before rounding.

| Region and period | T: total | B: between strata | H: haul depth | W: within strata |
| --- | ---: | ---: | ---: | ---: |
| Bering, 1982-2000 | 0.03 [-2.06, 2.11] | 0.30 | -0.79 | 0.52 [-0.64, 1.68] |
| Bering, 2001-2019 | -1.78 [-3.19, -0.36] | -1.27 | -0.02 | -0.49 [-1.15, 0.17] |
| Northeast, 1982-2000 | 3.51 [-2.14, 9.15] | 3.82 | -0.55 | 0.24 [-1.29, 1.76] |
| Northeast, 2001-2019 | 4.85 [2.01, 7.69] | 3.46 | 1.85 | -0.46 [-1.52, 0.61] |

The late Northeast total trend was positive, but the within-stratum point estimate was negative. Most of the positive depth trend arose from B and H in this decomposition. A positive total slope alone therefore does not establish a positive W slope. The Bering late-period total trend was negative. This selected sample does not show general deepening across both regions and periods.

All four W intervals included zero with lags one and five as well. The late total Bering interval stayed below zero and the late total Northeast interval stayed above zero with those lag choices. With the post-2008 step, the late Northeast total slope fell to +1.47 [-1.98, 4.92], and W was -0.74 [-3.01, 1.54]. Thus the late total Northeast inference depends on representation of the survey change. There are few years on each side of the step.

Removing one taxon at a time kept each W point estimate's sign. The slope ranges were +0.29 to +0.61, -0.57 to -0.40, +0.10 to +0.33, and -0.54 to -0.32 in table order. These are sensitivity ranges, not confidence intervals. They do not resolve the uncertainty shown in the main table.

## Meaning and limits

This method can help inspect depth indicators before a climate explanation is fitted. It distinguishes catch changes across depth strata from catch-depth differences relative to sampled depth within strata. The result does not show that animals avoid deeper water, do not respond to warming, or have no thermal refuge. Null intervals do not prove equivalence. Temperature, marine heat extremes, air pollution and ecological timing were not measured in this test. The study addresses the species-distribution and observation-bias part of the campaign objective.

Selected persistent taxa, survey boundaries, missing hauls, depth measurement, taxon names, changing gear, fishing pressure and spatially varying catchability limit interpretation. Area weights address allocation among strata under representative within-stratum sampling; they do not ensure that assumption. The total indicator can hide range-edge loss or gain. Linear trends can hide abrupt changes. The two regions have different habitats and survey designs. Neither supplies a global estimate. A next study could test bottom temperature responses of all three parts using fixed stations and explicit survey-change terms. The present package supports no causal climate or pollution claim.

## Reproduction and checks

From the extracted bundle root, run:

```sh
python files/verify_results.py
python files/analyze.py --raw /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz --out reproduced
python files/verify_results.py reproduced
```

The offline verifier rebuilds every taxon-year component from the saved stratum catch sums, checks annual means, checks non-step slopes with a separate centered-sum formula, and checks exact slope additivity. It includes a synthetic two-stratum example with unequal areas and catches and a constant-catch benchmark. It also writes the taxon omission ranges. It does not independently validate the HAC standard errors. A complete raw-data rerun matched every bundled CSV table. The raw-data script reproduces all interval and step fits. Use Python 3 with numpy, pandas, scipy, statsmodels and matplotlib; recorded versions are in provenance.json.

If the shared raw file is unavailable, retrieve the exact versioned URL above to private scratch and verify its stated SHA-256. In this campaign, use the workspace campaign-dataset helper for new reusable raw data; do not replace shared data. Gzip timestamps can differ on rerun; compare decoded tables. No network access is needed for analysis after data retrieval.

`stratum_evidence.csv.gz` gives Q, QD, n, area, dbar and d0 for every positive-catch retained taxon-year-stratum. Zero-catch strata add no numerator or denominator. `haul_design.csv` gives all retained stratum-year haul denominators, including strata without focal catches. `taxon_depth.csv.gz` and `annual.csv` give the decomposed positions. `trends.csv` gives every model estimate and interval. The PNG is static and within SCI display limits. Source metadata have their own provenance file and retain their upstream terms. The baseline license applies to our original text, figure, code and derived outputs; it does not replace source terms.

Job: sci-1107-dell-climate-pollution-biodiversity-5d686b1ea418. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. One finite automated worker performed the investigation. No agents were launched. The campaign-machine key is not a personal authorship claim. No private key is included.
