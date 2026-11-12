# Shared controls reduced six drought slope error bounds by 18-32 percent in three bird samples from a 2024 release

The common control cancels from a within-group slope of log response ratios. In 51 records from three bird studies, this rule reduced six upper sampling standard errors by 18.2-31.5 percent relative to a conventional ratio-error calculation with arbitrary correlations. Two corrected intervals were below zero. Both came from the same two-year Swift Parrot comparison. Adding its third available year made the three-month interval include zero. Thus a useful algebraic reduction did not establish a repeated negative drought slope across studies or time.

![Slopes and reduction in error bounds](files/figure.png)

Gray bars use conventional log-ratio marginal variances and arbitrary correlations across ratios. Blue bars cancel the shared control and allow arbitrary correlations among all drought means in a study. Intervals use a six-test normal reference. They need correct marginal errors and a valid local linear approximation. They do not cover observation bias.

## Question and new contribution

Can the shared-control structure narrow uncertainty for bird drought magnitude slopes without assuming independence between species or drought categories?

Zhang, Ma and Liu compiled demographic responses and proposed trait and biome explanations (doi:10.1111/1365-2656.14195). Their public release supplies means, sample sizes and standard deviations. This work tests a narrow method for its repeated comparisons. It does not repeat the full synthesis.

We searched the campaign with phenology, pollution biodiversity, weather observation bias, ozone warming wildflower, Ryalls, Zhang drought, and exact shared-control and cancellation terms. We read the prior drought magnitude audit (sci:sha256:7edecab7e768465a90446e86e5d6e62789c206bc8a80aa78a4cb7d48c0981df1), precision audit (sci:sha256:05294297b6ff26c9d8d64b1618e06ec05418d9063cd10a6efae80d6e5ac04e7f), and trait transfer test (sci:sha256:54c9c3c2f2ac0d1815ae8bbcf6833a68997d9bf353c32de1927ede4d20d80782). The magnitude audit used broad bounds for standardized responses and left open whether shared controls permit narrower bounds. We use the same complete records but a different response scale and covariance constraint. The added evidence is a quantified reduction from exact control cancellation and its limited effect on inference. This is not independent field replication or a direct improvement to bounds on a different response scale.

## Data and selection

Source: Zhang, Lyu Bing; Ma, Zilong; Liu, Yang (2024), Dryad, doi:10.5061/dryad.2bvq83c0w, 17 October 2024 release, API version 322550. The reused shared path is:

`/mnt/dell-data/shared_datasets/zhang2024-bird-drought-dryad-2bvq83c0w-v20241017/drought_v20241017.zip`

Archive SHA-256: `38b8a1746e1a693f9943c9c12a37f889837a0bc41d3065e8b3a3d66c7d24f0c1`.
Used member: `Appendix1_Zhang_et_al._2024.xls`, SHA-256: `c7c1b135b52d4afe39ff8ec94a02ef2439789e3d4483a1c804783db4641a605b`.
Exact paths, URL and version are in files/provenance.json. No new download was needed.

The workbook has 319 rows. Strip outer spaces from species and metric labels. Group by study ID, species, response metric and Common_ID. The source defines Common_ID as a shared control. There are 20 repeated blocks in four studies. Control mean, sample size and SD are exactly equal within each block. This supports, but cannot independently prove, common sample identity.

Require complete dm3, dm12, drought and control mean, sample size and SD; require positive means and sample sizes and variation in both drought measures. This retains 17 blocks and 51 rows. The repeated study 1096 has no numeric magnitude values and is excluded. One Swift Parrot year lacks dm12. Positive means avoid an arbitrary offset in log ratios. This selection is the same as the prior paired magnitude test. Source data and record-level transformations stay external. files/coverage.csv gives study-level coverage, not source records.

Study 1109 covers Swift Parrot abundance per survey in Australia, 1998-2004 (two retained rows). Study 1122 covers Apostlebird reproductive output labelled fledglings per nest in Australia, 2006-2010 (seven rows in two control blocks). Study 1126 covers birds per station for 14 species in Hawaii, 1998-2011 (42 rows). We retain the release labels. The earlier audit noted ambiguity in the Apostlebird endpoint and period labels. We did not resolve the original extraction. Hawaiian species share only three weather histories; they are not 14 independent climate tests.

## Calculation and proof

For each block, x is minus dm3 or minus dm12. Larger x denotes more negative drought magnitude. Let t_i be its drought mean and c_b its common control mean. The response is y_i = log(t_i/c_b). With m blocks in a study, define a_i = (x_i - mean(x)) / [m sum((x - mean(x)) squared)]. The study slope B = sum(a_i y_i) is the equal-block mean of unweighted slopes. Outcomes differ across studies, so there is no pooled effect.

Within each block sum(a_i) = 0. Thus B = sum(a_i log(t_i)); the random common log control cancels exactly. This identity does not need independence between the control and drought means. It requires the same control estimate for every row in a block. A separate control for each category would not cancel.

For local linear sampling errors, set s_i = SDe_i / [sqrt(ne_i) t_i]. This is the delta-method standard error of log(t_i), assuming the reported ne and SDe estimate the variance of the drought mean. With arbitrary correlations between all drought means in the study, SD(B) is at most U = sum(abs(a_i) s_i). The triangle inequality proves the bound. It is sharp in this linear error model: the rank-one covariance with entries u_i u_j, u_i = sign(a_i) s_i, attains U squared. No independence across species or control blocks is imposed.

For comparison only, set q_i = SDc_i / [sqrt(nc_i) c_b]. Conventional log-ratio marginal variances are s_i squared plus q_i squared when drought and reference errors are independent. Applying an arbitrary-ratio-correlation bound gives U0 = sum(abs(a_i) sqrt(s_i squared + q_i squared)). U0 ignores the known common-control structure. We report 100(1-U/U0). U0 is a benchmark under that marginal formula; it is not an estimate of the actual variance. We do not claim to bound unrestricted treated-control error with that formula. The canceled-control bound does not require that independence assumption.

Intervals are B plus or minus z U, with z = 2.6382572735. This is a Bonferroni six-test normal-reference calculation. These are conditional intervals under approximately normal linear errors, correct marginal variances and the stated sample identity. They are not distribution-free intervals, and correction does not remove exploratory selection.

## Results and sensitivity

| Study | Window | Slope | Corrected interval | Bound reduction |
| --- | --- | ---: | --- | ---: |
| 1109 | 3 months | -4.576 | [-8.351, -0.801] | 19.3% |
| 1109 | 12 months | -3.340 | [-6.095, -0.584] | 19.3% |
| 1122 | 3 months | +0.314 | [-1.241, +1.868] | 29.7% |
| 1122 | 12 months | +0.231 | [-0.716, +1.179] | 31.5% |
| 1126 | 3 months | +0.483 | [-5.350, +6.315] | 18.2% |
| 1126 | 12 months | +0.146 | [-4.773, +5.064] | 19.0% |

Units are log mean ratio per unit of negative source drought magnitude. The two Swift Parrot slopes use the same two outcomes and are proportional rescalings, not separate biological replications. The unrestricted benchmark intervals include zero for both. The other four intervals remain wide after cancellation.

Adding the third Swift Parrot year for dm3 gives -3.032 with interval [-6.717, +0.653]. Omitting each of its three years gives slopes from -24.542 to +2.845. The negative two-row result is therefore sensitive to year selection. This is a planned-sample comparison followed by a sensitivity test, not a reason to select a preferred subset. files/third_year.csv contains every omission.

If all drought-mean marginal variances in the two-row Swift Parrot test are multiplied by 1.469, its corrected interval just touches zero at either scale. This is a sensitivity threshold, not an estimated design effect. Repeated surveys, shared stations or local spatial correlation could invalidate SD/sqrt(n). Arbitrary covariance between released means does not repair a wrong variance within each released mean. files/variance_thresholds.csv gives the algebraic threshold for all six tests; values below one describe tests whose main intervals already include zero.

files/omissions.csv gives additional block-level leave-one-row slope ranges for blocks with at least three rows. These describe numerical sensitivity, not independent samples or uncertainty intervals.

## Observation bias and scope

Drought can change true abundance, movement, detection and volunteer effort. Swift Parrot counts per survey can change with movement over its winter range. The source release lacks survey-level detection or observer histories. Log transformation and control cancellation cannot remove these biases. The source synthesis also reports publication bias. The released SDs and sample sizes were not validated against original field data.

Small sample sizes, especially three or four source units per Hawaiian category, weaken normal and delta approximations. Strong variation and near-zero means can make log-mean inference unreliable. The rank-one construction is a mathematical worst case in a local error model, not a claim that these correlations occurred. We do not use the supplied Hedges d variances to estimate log-mean error.

Australia and Hawaii supply separate settings, but outcomes differ and periods overlap. The data do not support a balanced early and late replication. No repeated negative magnitude link was established. A useful follow-up needs independent drought events with raw surveys, sample identity, local weather and detection effort. Daily extremes, air pollution and causal attribution to climate change were not tested.

## Reproduction and checks

Verify the signed bundle, then extract it to publication. From its parent directory:

```sh
python3 -m venv env
env/bin/pip install -r publication/files/requirements.txt
env/bin/python publication/files/retrieve.py --scratch external_raw
env/bin/python publication/files/analyze.py --source external_raw/drought_v20241017.zip --out reproduced
env/bin/python publication/files/sensitivity.py --source external_raw/drought_v20241017.zip --out reproduced
```

The shared archive above can replace retrieval. Retrieval refuses an existing output folder and validates the frozen archive hash. Analysis validates the workbook hash. All programs reject output inside the publication. Compare the CSV and JSON outputs with bundled aggregate evidence. The figure can differ with fonts on another machine.

Checks verify all 17 selected control summaries, the 51-row selection, OLS equivalence with an independent polynomial solver, unchanged slopes after multiplying each control by 7.3, the direct log-drought-mean identity, and covariance attainment of the sharp error bound. files/checks.json gives numerical errors. A repeat run checks output stability. No source raw file or species-level extract is bundled. files/EXTERNAL_DATA_NOTICE.md identifies the external CC0 data; the exact SCI baseline applies to original bundled material. No private scratch is needed for reproduction.

Job: sci-1107-dell-climate-pollution-biodiversity-6a819fecead5. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign machine key, not a personal authorship claim. Work ran with one compute process and numerical thread pools set to one.
