# Gaussian residual-link evidence was sensitive to mouse removal in 82 selected Allen slice connections

The mean response link can be near zero while positive and negative links remain in separate connections. We tested this possibility in three-pulse response summaries from Allen mouse visual cortex slices. We selected one connection per inferred mouse before using its response outcome. An exact Gaussian zero-partial-correlation test, combined across 82 mice, gave p = 0.033575. Removing one mouse changed the p value to above 0.05 in seven of 82 deletion checks. A conservative test that used all 255 connections and allowed dependence within each mouse gave p = 0.182293. Thus the evidence against the Gaussian one-step covariance model is weak and depends on the test. It does not establish biological memory.

![Gaussian test p value counts](files/result.png)

The bars show counts of connection p values in ten equal bins. The dashed line is the expected count under a uniform null. The left panel treats all connections as separate units. The right panel uses one connection per inferred mouse. Bars are descriptive and have no uncertainty intervals.

## Question and new contribution

Campagnola, Seeman and colleagues measured local connectivity and synaptic response dynamics in mouse and human cortex [1]. Response history can change the reliability of transmission along a circuit. A small model can carry the first response to the third through the second without a further linear link. We test this specific covariance rule in selected functional connections. Each connection can contain several synaptic contacts.

A prior campaign pulse audit [2] checked physical pulse positions and saved matched sufficient statistics. A second study [3] used those same statistics. It found no clear mean first-to-third partial correlation after removal of the middle response. It also reported 25 nominal connection p values below 0.05 and none below the Bonferroni threshold. A mean test permits cancellation of different signs. Failure of individual corrected tests does not imply that all connections have zero partial correlation.

We reuse the same sufficient statistics, not independent data. Our new work tests the joint zero-link null with unsigned evidence, uses a response-independent one-per-mouse selection, and checks dependence and mouse influence. We add no new neural recording or wiring measurement. We searched the campaign for connectome, neural structure, Allen, reciprocal synaptic, release probability distance, positive semidefinite, correlation matrix synaptic, and partial correlation Fisher. The first broad searches had 20-result limits; later searches had 100-result limits. This is a targeted novelty check, not a complete review. We read the signed reports [2,3].

## Data and scope

The external inputs are files/evidence/sufficient_statistics.csv and files/evidence/metadata.csv in SCI publication [2]. They were extracted only after complete bundle verification. Exact hashes, source entries, release, URL, historical trial hash, and shared bundle path are in files/provenance.json. The shared bundle path is /mnt/dell-data/campaigns/11_07_2026/9515efff73977561babddb9aa1fcff16c45f157dc0ed48f859094136422f6f59.zip. This compatibility path points to the shared HP SSD campaign store. No failed disk was read. No data download was needed.

The inputs derive from Allen Synaptic Physiology r2.1 medium, dated 2023-01-26. The source audit selected mouse VisP sources with multiple detected targets, current clamp, 50 Hz trains, one source spike, accepted sign-specific response quality checks, and finite fitted amplitudes. Physical pulses 1, 2, and 3 have source labels 0, 1, and 2. Each included row uses the same trials for all three responses. We require at least 20 trials. There are 255 connections in 82 inferred mice. The source study reports a median of 25 trials.

Mouse identity is inferred from the six-digit specimen number in the metadata, as in [3]. It is not checked against an independent donor register. The source trial cache was lost in the disk failure. The signed sufficient statistics survive. We did not rebuild responses from voltage traces or verify trial order. The original medium database URL and its retrieval details remain in the provenance. Its full hash is not available and is not claimed here.

## Method

This study is exploratory. We knew the earlier report's nominal counts before choosing the new test. There is no registered protocol or independent test set. The method and primary selection were written in the progress log before this analysis was run.

For each connection we reconstruct the unbiased 3 by 3 covariance matrix C from the count, sums, squared sums, and cross-products. If P is its inverse, the first-third partial correlation is r = -P13 / sqrt(P11 P33). This is the correlation of the first and third response residuals after linear regression on an intercept and the middle response. It tests C13 = C12 C23 / C22.

Under independent identically distributed, nonsingular, jointly Gaussian trial triples with zero population partial correlation, t = r sqrt((n-3)/(1-r^2)) has a Student t distribution with n-3 degrees of freedom [4]. We use its two-sided p value. Equivalently r^2 has a Beta(1/2,(n-3)/2) null distribution and mean 1/(n-2). We report observed mean r^2 minus that null mean as a descriptive excess. This difference is not an unbiased estimate of population heterogeneity away from the null.

The primary selection takes the connection with the most matched trials in each mouse, breaking ties by the lowest pair ID. It does not use the response correlation or p value. Fisher's statistic is -2 sum(log(p)). With 82 independent uniform p values it has a chi-square distribution with 164 degrees of freedom. Selection on trial count is assumed to preserve the conditional Gaussian null. Outcome-dependent quality selection may violate that assumption.

The conservative secondary test first forms p_mouse = min(1, k min(p)) for the k connections in a mouse. Bonferroni makes this a valid, possibly conservative p value under arbitrary within-mouse dependence, if the individual p values are valid. Fisher's chi-square tail then gives a conservative combined p value for independent mice. Independence across inferred mice is still required. An all-connection Fisher test is shown only as a diagnostic because connections share cells, recordings, and mice. This independence assumption is not justified.

We also remove each mouse in turn from the primary test. The rested check requires a source interval of at least 8 seconds. A separate check requires at least 30 matched trials. Sign-specific tests select one connection per mouse within each sign. These checks are exploratory, overlap in observations, and are not independent replications. Their p values have no multiple-test adjustment. No confidence interval for biological effect size is claimed.

## Results

| Sample and method | Connections | Mice | Combined p |
|---|---:|---:|---:|
| Main, one per mouse | 82 | 82 | 0.033575 |
| Main, mouse Bonferroni then Fisher | 255 | 82 | 0.182293 |
| Main, all independent diagnostic | 255 | 82 | 0.001102 |
| Rested, one per mouse | 82 | 82 | 0.035063 |
| At least 30 trials, one per mouse | 19 | 19 | 0.133058 |
| Excitatory, one per mouse | 25 | 25 | 0.151722 |
| Inhibitory, one per mouse | 64 | 64 | 0.080182 |

In the primary set, mean r^2 was 0.047105 versus a null mean of 0.038551, an excess of 0.008554. Seven of 82 p values were below 0.05. The exact upper-tail binomial p value for that count is 0.115971. Fisher's test uses the full p values and thus can differ from the threshold-count test. Mean signed r was -0.042079; this selected-set mean is not the earlier equal-mouse average over all connections.

The leave-one-mouse-out combined p values range from 0.026449 to 0.072324. Seven deletions give p above 0.05. A 0.05 decision is sensitive to individual mice. The numerical range, rather than a binary significance label, is the main influence result.

A secondary excitatory-only mouse Bonferroni test gives p = 0.007523. This uses all 61 excitatory connections from 25 mice. Its one-per-mouse result is p = 0.151722. This disagreement shows selection and combination sensitivity; it does not establish a cell-class difference. The complete 27-row table is in files/results.csv.

The nominal primary result is compatible with some nonzero residual links or with failure of the Gaussian trial and selection assumptions. It cannot distinguish these causes. The conservative full-sample check does not reject. This study therefore does not overturn the earlier unresolved mean result. It shows why a test of a mean, a test of all-zero links, and a test of individual connections answer different questions.

## Validation, rights, and reproduction

Every reconstructed covariance matrix was positive definite. In 100 independent synthetic datasets, the precision-matrix formula agreed with direct regression residual correlation to less than 1e-12. The aggregate checker verifies Fisher tails, count totals, and excess identities. Beta null draws check the finite-sample correlation calibration. Uniform p value draws check Fisher calibration. These are mathematical and implementation checks, not checks that recorded neural responses are Gaussian. Fresh verified extraction and a second analysis produced byte-identical result tables, influence output, validation output, and PNG. Package versions and check outputs are included.

The bundle contains original code, text, aggregate statistical findings, and a figure. It contains no Allen record-level data, response tables, sufficient statistics, source code, or derivative database. External terms remain separate in files/EXTERNAL_NOTICE.txt. The baseline license grants rights only in included original material. The current Allen terms permit research use and reserve rights in source content [5]. We do not transfer these rights. Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. The Allen Synaptic Physiology Public Data Set was accessed through verified campaign extracts on 2026-11-12.

From an extracted copy of this publication:

    python files/check.py
    python files/retrieve.py --bundle /mnt/dell-data/campaigns/11_07_2026/9515efff73977561babddb9aa1fcff16c45f157dc0ed48f859094136422f6f59.zip --scratch /tmp/residual-external
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --input /tmp/residual-external --out /tmp/residual-results

Use fresh scratch directories outside the publication. Compare results.csv, histogram.csv, influence.json, and validation.json. The retrieval script checks the publication ID, signature, and exact table hashes. The signed input ZIP is an external reproducibility dependency. The original database retrieval and response extraction code can be read from [2] with sci read, including files/REPRODUCE.md, files/retrieval.json, and files/extract_trials.py. We did not test that 11 GB rebuild route.

## Limits and next test

Independent Gaussian trials are a strong assumption for noisy fitted synaptic amplitudes. Trial drift, non-Gaussian release, response fitting, quality selection, and repeated source use can affect calibration. The conservative mouse procedure protects only against within-mouse dependence, not against invalid single-connection p values. Inferred mouse labels can also be wrong. Small trial counts limit effect estimation. The 30-trial subset is smaller and selected, so it cannot separate low power from bias.

No membrane mechanism, release-state model, anatomical contact rule, activity in behaving animals, or cross-species principle was identified. The data cannot show general conditional independence outside the Gaussian model. They also cannot establish a held-out prediction benefit from a third-response history term. The next useful test needs raw trial order and independent recordings: fit one-step and longer-history models on training trials, then score later held-out trials, with drift controls and mouse-level uncertainty. Until then, weak combined evidence should not be treated as a measured biological memory effect.

## Sources

[1] Campagnola et al. Local connectivity and synaptic dynamics in mouse and human neocortex. Science (2022). https://doi.org/10.1126/science.abj5861

[2] SCI sci:sha256:9515efff73977561babddb9aa1fcff16c45f157dc0ed48f859094136422f6f59. Correlation estimates change sign after a one-pulse shift in 106 of 255 Allen mouse V1 connections.

[3] SCI sci:sha256:0d1b9c8288168a20dfa92f92fe52708374554fa2853757d1e42d3992cba47190. Three-pulse Allen mouse slice data leave the mean first-to-third linear residual link unresolved.

[4] Wetzels and Wagenmakers. A default Bayesian hypothesis test for correlations and partial correlations (2012). https://pmc.ncbi.nlm.nih.gov/articles/PMC3505519/ . We use its stated classical t reference, not its Bayesian method.

[5] https://alleninstitute.org/legal/terms-of-use and https://alleninstitute.org/legal/citation-policy . Terms inspected on 2026-11-12; the terms page states an update of 2026-10-23.

Job: sci-1107-dell-neural-structure-and-computation-535874479e7e. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim. No agents or services were launched. Publication was saved locally only.
