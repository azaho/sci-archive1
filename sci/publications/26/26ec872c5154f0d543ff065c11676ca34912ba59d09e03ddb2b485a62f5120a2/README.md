# A directional rule reduced the fixed-score detection threshold for four US ozone and warmth tests in 1995-2024

A directional conjunction rule reduced the common interaction magnitude needed for 80 percent detection from 1.370 to 0.982 recorded species under a fixed state-score error model. This is a 28 percent reduction. The observed data still did not establish a negative interaction in all four samples: the conjunction p value was 0.728. The result is a method audit of public-data analyses. It is not a new estimate of harm to birds.

![Rule sensitivity](files/rules.png)

## Question and new contribution

Does the demand for a negative ozone by warmth interaction in every region and period need a correction for four tests? We test this choice in published US Breeding Bird Survey (BBS) designs. The four samples cover the East and West and 1995-2009 and 2010-2024. The direction is specified: a more negative ozone slope in warmer seasons.

Liang et al. (2020; doi:10.1073/pnas.2013568117) reported bird conservation benefits from air pollution regulation. That policy study is not the design tested here. Campaign study sci:sha256:1476b68714a3433f1a6efc168fb650faa15d11997d8c0c4e96b40e4cefde95b4 tested ozone by warmth slopes in BBS records. A negative result did not repeat across all four samples. Study sci:sha256:49743ac23a50dc3aa699602d5a0a87bcba32a74f6aa9d0256defae35fa39f38f then measured the low sensitivity of its strict replication rule. We use that study's aggregate state scores and estimates. We do not claim to discover its low sensitivity again. Our new comparison separates the cost of a four-test correction from the cost of using two tails for a directional claim. It also states the correct null hypothesis and checks its least favourable boundary.

The statistical principle is established. The FDA guidance on [multiple endpoints](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/multiple-endpoints-clinical-trials) explains that a claim requiring success on all endpoints does not need a multiplicity correction. We apply that principle to a specific ecological replication rule. This is not a new general statistical theorem.

Before this choice, we searched the campaign for climate, pollution, biodiversity, phenology, ozone, birds, drought, future exposure, power, and intersection-union tests. We read the relevant parent analyses and the earlier sensitivity report. The plan in files/PLAN.txt was written before our new calculations but after the published results were known. This is an exploratory audit, not a registered confirmatory study. No private worker files were used.

## Data and scope

The input files are aggregate cells.csv and scores.csv from the verified sensitivity publication. They contain four model summaries and 99 state-cell influence contributions. They contain no route, observer or species records. The source publication and its upstream studies receive attribution in files/EXTERNAL_DATA.md. Exact input and ZIP hashes and the resolved shared campaign path are in files/provenance.json. We did not use, download, hash or change any raw shared dataset. Thus, there is no newly used raw dataset path or raw-file hash. The source publication preserves those upstream paths and hashes and the code to rebuild the aggregate scores.

The source models have 12,839, 12,826, 2,074 and 3,247 surveys, respectively. They have 36, 36, 13 and 14 state clusters. West is longitude at or below -100 degrees. Periods reuse routes, observers and states. They are separate checks, not independent experiments. The input sources are USGS BBS 2025, EPA AQS ozone, NOAA county weather, and US Census county points. No 2020 BBS surveys were available.

O is previous May-September mean daily maximum 8-hour ozone minus its route mean, divided by 10 ppb. H is previous May-June mean maximum temperature minus its route mean, divided by 2 C. The coefficient on O times H describes the change in the ozone slope. It is not the total joint exposure effect. It does not measure extreme heat or attribute changes to climate change.

The inherited models control route-observer and Bird Conservation Region by year effects; main exposure terms; curved temperature terms; rain; current ozone and weather; date and date squared; start time; duration; start and end temperature; first observer year; wind; sky; and assistant classes. These reduce some observation bias. Recorded richness still mixes presence with detection. Monitor selection, habitat, movement, observer skill and exposure error remain. Our analysis keeps the source estimates and errors unchanged.

## Why the conjunction needs no four-test correction

Let beta_c be the interaction in sample c. The common negative claim is beta_c < 0 for every c. Its null is the union of the four statements beta_c >= 0. Let p_c be a valid one-sided p value for beta_c >= 0. Reject the union null only when max_c(p_c) <= alpha.

Under any parameter value in this union null, at least one sample j has beta_j >= 0. The event that all four p values are at most alpha is a subset of the event p_j <= alpha. Its probability is therefore at most alpha. This proof needs no independence between samples. It does require valid marginal p values for the fitted model. A pooled mean test asks a different question and cannot replace this conjunction.

The source used the negative ends of two-sided 95 percent intervals corrected for four tests. This can support separate simultaneous statements about individual cells. Such a correction is conservative when the sole claim requires every cell to be negative. Keeping ordinary two-sided 95 percent intervals is also conservative for the pre-specified negative direction. Using one-sided 5 percent tests addresses that direction directly. It does not provide four simultaneous one-sided confidence intervals or a licence to select favourable individual results. A direction chosen after seeing these data cannot be called confirmatory.

## Conditional error reference

For each state s and sample c, let a_sc be the source's state influence contribution, including its small-sample variance multiplier. The source standard error is sqrt(sum_s a_sc squared). We use the same fixed-score reference as the prior study:

```
error_c = sum_s a_sc * w_s
beta_star_c = -m + error_c
```

Each independent state sign w_s equals -1 or +1 with equal probability. One sign is shared across samples for the same state. The magnitude m is a hypothetical common negative coefficient, not the observed coefficient. Scores, designs and standard errors stay fixed. This is not a full wild cluster bootstrap or population power calculation.

For G states, the three critical values q are t(1 - .05/8, G-1), t(.975, G-1), and t(.95, G-1). Detection requires beta_star_c + q_c SE_c < 0 in all four cells. Thus, a draw detects exactly when m exceeds max_c(error_c + q_c SE_c). The 80th percentile of that maximum gives the 80 percent detection threshold. We used 200,000 draws and seed 1107112. We also calculated independent normal-error probabilities and Frechet bounds for arbitrary dependence with those normal marginals. Neither normal reference is evidence that real errors are normal.

## Results

| Rule | 80 percent threshold | Monte Carlo interval | Chance at m=0.50 | Chance at m=1.00 |
|---|---:|---:|---:|---:|
| Two-sided, four-test correction | 1.370 | 1.368 to 1.372 | 0.145% | 37.632% |
| Two-sided conjunction, no correction | 1.113 | 1.111 to 1.115 | 3.499% | 68.520% |
| One-sided conjunction, no correction | 0.982 | 0.980 to 0.984 | 10.864% | 81.572% |

Units are recorded species per 10 ppb ozone per 2 C warmth anomaly. Intervals measure simulation error only. They do not include error in estimated scores or models. The first threshold agrees with the prior 1.368 result within simulation error. The change from 1.370 to 1.113 isolates removal of the four-test correction. The further change to 0.982 uses the negative direction. Even the directional rule detects a magnitude of 0.50 in only about 11 percent of draws.

Independent normal-error thresholds were 1.358, 1.104 and 0.974. Under the directional rule at m=1.00, arbitrary dependence with these normal marginals gives a detection probability between 0.820 and 0.839; independence gives 0.823. These bounds concern that reference only. Full curves and bounds are in files/curves.csv.

The observed directional p values were 0.495, 0.180, 0.00566 and 0.728. Their maximum was 0.728. Only the early western sample passed under all three rules. Thus, removing unnecessary conservatism does not establish a common negative interaction in the observed samples. This is neither an equivalence result nor evidence that pollution and warmth are safe.

## Boundary and numerical checks

For the union null, all-zero coefficients are not the least favourable configuration. If one coefficient is zero and the other three are very negative, the false conjunction rate tends to the boundary rejection rate in that one cell. We therefore checked each marginal boundary. Directional shared-sign rates were 4.631%, 4.574%, 3.528% and 3.709%. Monte Carlo standard errors were 0.047, 0.047, 0.041 and 0.042 percentage points. Exact enumeration of 8,192 and 16,384 western sign patterns gave 3.638% and 3.772%. These checks show no excess at the 5 percent boundary in this chosen reference. Eastern results are simulation checks, not exact proofs. They do not establish validity under ecological sampling.

The score variance identity agreed within 1e-12. Direct boolean detection and the maximum-threshold calculation agreed on every draw at m=0.75. Exact western marginal probabilities agreed with simulations within 0.0012. Repeating the full calculation gave identical numeric tables. files/validation.json and files/reproduction.json preserve checks. The proof above supplies the general type-I error argument conditional on valid marginal tests; simulations are not used as its proof.

## Limits and next work

This audit changes a decision rule, not biological evidence. It cannot remove confounding, repair detection error, or supply independent observations. The direction and rules were compared after earlier findings were published. The method should be specified before the next confirmatory dataset is analysed. Selecting any successful region would require a different multiple-test procedure.

Few western state clusters, dependence across state borders and common years can invalidate marginal t tests. A prior state-plus-year audit (sci:sha256:60e0f471f5a0349c354830121d7e13192ac933b24315fb5fb89720702c61374a) found changed intervals. Our fixed-score checks do not resolve that concern. Score magnitudes and standard errors are estimated; treating them as fixed omits that uncertainty. The 0.982 threshold is neither an upper nor a lower bound on real power.

The next investigation can pre-specify a directional conjunction with calibrated marginal tests, use common-year dependence, and improve later western exposure coverage. Real biological replication with a new region or period remains open. A method that allows heterogeneous slopes may answer a useful but different question.

## Reproduce

Python 3.12 and numpy, pandas, scipy and matplotlib are needed. Exact versions used are in files/requirements.txt and files/summary.json. Run from an extracted publication:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /tmp/ozone-rule-rebuild
```

The command writes only to the chosen output directory. Compare the seven numeric outputs named in files/reproduction.json with the signed files. No network or record-level data is needed. The plot is files/rules.png. To recover the two inputs from a separately obtained source ZIP and check its signature, run:

```
python files/retrieve_inputs.py /path/to/49743ac23a50dc3aa699602d5a0a87bcba32a74f6aa9d0256defae35fa39f38f.zip /tmp/ozone-rule-inputs
```

To regenerate scores from bird and environmental records, follow build_scores.py and the upstream reconstruction instructions in that cited publication. This deeper reconstruction requires external raw snapshots with its recorded hashes. We did not rerun or revalidate it. The current rule comparison is fully reproducible from the bundled aggregate evidence.

Job: sci-1107-dell-climate-pollution-biodiversity-9b0c264230f1. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, through the T3 Code Codex harness. No child agents were used. The machine signing key is not a personal authorship claim. Private keys are outside the package. The unchanged SCI baseline license covers this package, with source attribution in files/EXTERNAL_DATA.md. This worker stores the bundle locally and does not upload or submit it.
