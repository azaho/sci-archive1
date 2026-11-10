# A division-local covariance cut simulated false wiring signals and kept five task links in 176 IBL regions

Job: sci-1107-dell-neural-structure-and-computation-9365b8cb1464. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Does the Gaussian-process (GP) null from SCI f4e4c5 control false positive wiring claims for regional maps with different forms of spatial covariance?

The selected work linked task coding to input wiring and intrinsic spike measures to cell-type composition. SCI f4e4c5 showed that distance-stratified graph shuffles gave false positive results for smooth maps. It proposed a fitted GP null and obtained a pooled false positive rate of 5 percent on five generators. SCI a4fae2 then found useful held-region prediction from input fingerprints and cell-type composition. Prediction gain and wiring-specific association are different claims. This study tests the calibration claim. It does not estimate causal control of physiology.

Spatial surrogate models are established tools, including Burt et al. (2020), doi:10.1016/j.neuroimage.2020.117038. The contribution here is a controlled covariance stress test of the exact input-neighbour coefficient in this campaign, with a known-covariance reference. It is not a new general theory of spatial null models.

## Data

We rebuild structure on the same 176 complete regions used by SCI a4fae2. These regions have five task scores and nine spike measures. Regional medians come from SCI f4e4c5. Task values come from IBL region_info.csv at commit de37454426bc4107047b5a18b854fc1ef7a5959c. The sample is fixed before simulation. It differs from the 191-region intrinsic sample in f4e4c5.

The Knox 2019 ipsilateral connection density gives W[source,target]. Allen CCF 2017 gives regional centroids. Allen MERFISH mouse 638850, release 20231215, gives neuron-supertype proportions. Their square-root Gram matrix T is the Bhattacharyya similarity. V indicates a shared major brain division. C counts probes with good IBL units in both regions, from the 2026_Q2 clusters table. D is Euclidean centroid distance in mm. We reuse the published mapping and source code. Exact file paths, URLs and hashes are in files/inputs.json, files/extra_provenance.json and the retrieval script. No external matrix or region-level source table is in this publication.

## Methods

For a matrix M, the predictor at target r is the weighted mean of y in all other source regions: sum_s M[s,r] y[s] / sum_s M[s,r], with s unequal to r. We regress standardized y on standardized predictors from W, exp(-D), C, V and T, with an intercept. The test statistic is the W coefficient. Values of y are first converted to standardized ranks. This is the statistic and the four controls used by the source GP analysis.

The fitted null uses covariance a0 exp(-D/0.5) + a1 exp(-D) + a2 exp(-D/2) + a3 T + a4 V + a5 I + 1e-6 I. It fits the six positive weights by maximum likelihood after centering y. Log weights have bounds -12 to 3. The two starts match the source code. We use analytic gradients to reduce run time. We draw 499 Gaussian maps from the fitted covariance, rank them, and calculate their coefficients. The one-sided p value is (1 + number of surrogate coefficients at least as large as the observed coefficient)/500. We do not refit the covariance for each surrogate, as in the source method.

Each generator produces 200 independent Gaussian maps. Every covariance uses geometry, types or division only. None uses W. Each has unit diagonal, with 90 percent structured covariance and 10 percent independent noise. The eight structured covariances are:

1. Exponential distance, exp(-D), which lies in the fitted covariance family.
2. Exponential smoothing: form row-normalized M=exp(-D), then convert M M transpose to a correlation matrix. This resembles an original calibration generator.
3. Squared exponential distance, exp(-D squared / 2).
4. Three anisotropic squared exponential kernels. One anatomical axis has length 0.3 mm; the other two have length 3 mm. We test AP, DV and ML as the short axis in separate conditions.
5. Division-local covariance, exp(-D) times V. Different divisions have independent spatial fields.
6. Space-type covariance, exp(-D) times T to the eighth power.

All kernels are positive definite after adding noise. The oracle and fitted tests use separate random surrogate draws. Products are elementwise. Different generator seeds are 936500 plus their fixed index in code. The oracle test uses independent surrogate maps from the known generating covariance, with the same rank transform, regression statistic and p-value rule. Thus it has the correct null distribution without covariance fitting. It is a simulation reference, not an available test for real physiology.

We report rejection rates at p < 0.05 and 95 percent Wilson intervals over independent maps. With 499 surrogates, exact exchangeability gives rejection probability 24/500=0.048. A one-sided binomial test against 0.048 and Holm correction across the eight generators are added in the report code to quantify excess rejection. Intervals are pointwise, not simultaneous. Reused anatomy makes conditions dependent, but maps within each condition are independent.

Four exploratory conditions were added after partial results from the first four conditions showed no clear excess rejection. Three apply amplitudes exp(0.7 z) to an exponential field, where z is standardized AP, DV or ML position. Their covariance is 0.9 A exp(-D) A + 0.1 I, so marginal variance varies in space. The fourth mixes independent exponential fields of lengths 0.3 and 3 mm with weights w and 1-w, where w is the logistic function of twice standardized AP position. This covariance is normalized to unit diagonal, then mixed with 10 percent independent noise. These four tests use new seeds and a separate Holm family. See files/code/EXTENSION.md. They do not use real physiology to choose covariance parameters.

The primary plan was saved before test statistics were inspected. Its hash is in files/plan_sha256.txt. It has no independent preregistration timestamp. The code ran four local compute processes. An early serial run was stopped for speed; incomplete conditions restarted with the same seeds. No condition was selected or removed based on its rejection rate.

## Results

The primary division-local condition gave **25 rejections in 200 maps (12.5 percent; 95 percent Wilson interval 8.6 to 17.8 percent)** with the fitted GP. The known-covariance null gave **9 in 200 (4.5 percent; interval 2.4 to 8.3 percent)**. The binomial test against the exact nominal rate of 4.8 percent gave p=0.0000133, or 0.000106 after Holm correction across eight primary conditions. All primary GP fits converged.

| Primary covariance | Fitted GP rejection rate | Known-covariance rejection rate |
| --- | ---: | ---: |
| Exponential distance | 5.0% | 4.5% |
| Exponential smoothing | 6.0% | 6.0% |
| Squared exponential distance | 6.5% | 3.0% |
| Short AP length | 1.0% | 4.5% |
| Short DV length | 4.5% | 3.5% |
| Short ML length | 5.5% | 7.0% |
| Division-local distance | 12.5% | 4.5% |
| Space-type product | 6.0% | 3.5% |

Only the division-local fitted test had a clear excess after the eight-condition correction. The known-covariance test had no clear excess in any primary condition. Anisotropy did not cause a general increase in rejection. The AP condition was conservative. A single average calibration rate would hide this dependence on covariance structure.

The exploratory variance-gradient conditions gave fitted rejection rates of 8.0 percent (AP), 5.5 percent (DV) and 7.0 percent (ML). The varying-smoothness condition gave 4.0 percent. Their known-covariance rates were 2.5, 5.0, 3.5 and 6.0 percent. None of the four fitted rates had clear excess after the separate four-condition correction. These results do not support a general failure for nonstationarity. All fits converged.

On fresh division-local maps, the original model rejected **26/200 (13.0 percent; interval 9.0 to 18.4 percent)**. The extended model rejected **12/200 (6.0 percent; interval 3.5 to 10.2 percent)**. Fourteen maps were rejected only by the original model; none was rejected only by the extended model. A post-result paired exact test gave p=0.000061, or 0.000122 if adjusted for the two repair conditions. This supports a reduction under this generator. It does not prove exact nominal calibration.

On fresh exponential-distance maps, rejection was 10/200 (5.0 percent) for the original model and 9/200 (4.5 percent) for the extended model. All 800 covariance fits in this two-condition comparison converged.

For measured physiology, **all five task measures passed Holm correction with the extended covariance**: adjusted p=0.0234 for stimulus, 0.0010 for choice, 0.0010 for feedback, 0.0030 for wheel speed and 0.0032 for block prior. None of the nine intrinsic measures passed correction. The smallest intrinsic adjusted p was 0.0972 for the 3–10 ms autocorrelogram index. Thus this specific covariance repair preserved the task-versus-intrinsic association contrast. It does not remove every possible anatomical confound.

![Independent repair check](files/repair.png)

![Calibration](files/calibration.png)

## Exploratory repair

After the primary division-local failure, we added the covariance component exp(-D) times V to the fitted GP. It has its own positive weight. All other fit bounds, starts, controls and test rules stay the same. We tested the original and extended models on 200 new maps for division-local covariance and 200 new exponential-distance maps. Seeds were 1946500 plus the generator index. The models share each observed synthetic map but use independent surrogate draws. These checks were specified in files/code/REPAIR_PLAN.md after the primary result. They supply a targeted validation, not a new primary test. The table in files/repair_summary.csv includes Wilson intervals and convergence counts.

We also test each of the 14 measured features with the extended GP, using 4999 surrogates. Holm correction is separate for the five task measures and nine intrinsic measures. These are sensitivity tests on the existing sample, not independent biological replications. We do not pool features because the new procedure does not model cross-feature dependence.

## Interpretation and limits

The primary failure has a simple structural explanation. Suppose each division has its own independent spatial field f_d with covariance k(distance). Then the covariance between two regions is k(distance) if their divisions match, and zero otherwise. In matrix form, it is K times V, element by element. A shared spatial field plus division offsets has covariance K + aV. Those models describe different dependence. Division offsets alone do not supply division-local spatial covariance. The repair adds the missing interaction without using wiring.

The experiment therefore narrows the claim that the fitted GP is calibrated for non-wiring regional structure. It worked within uncertainty for most tested covariances, but division-local fields were a counterexample. A broad wiring-specific interpretation needs calibration against interactions between anatomy and spatial fields, not only additive geometry and division terms. The real task links survived this targeted repair. Together, the calibration and sensitivity results strengthen those task associations against one identified source of error. They do not establish causal wiring control. Useful prediction can also remain when a spatial association null is misspecified.

The formal fitted GP null is a restricted covariance model. A rejection under a covariance outside that family is not a contradiction of that formal null. It is a false positive only for the broader claim that the test isolates wiring dependence from non-wiring structure. This distinction is central to the interpretation.

These simulations do not show that measured physiology has any of the tested covariances. They test conditional calibration, not the truth of an observed biological association. The oracle controls use known latent Gaussian covariances, which are unknown for real data. Twelve choices do not cover all spatial structure. The 499-surrogate calibration tests cannot resolve p values near 0.001. The null rejection probability at p < 0.01 is 4/500=0.008; that rate is also supplied in the table. The lengths and noise fraction are fixed, not fitted to physiology. The repair is validated only on the two stated covariance conditions; it is not re-tested on all twelve generators. We use one brain atlas, one connectome and one MERFISH animal. We do not repeat the thalamus-only test, the pair-similarity analysis, or the cross-animal replication. Those require separate calibration. The 176-region subset and co-recording reconstruction can change observed coefficients relative to the original report.

## Validation, rights and reproduction

The batched regression agrees with a separate direct least-squares calculation to within 2.5e-16. The analytic optimizer agrees with the prior finite-difference objective on a fixed synthetic check. All generating covariances have positive eigenvalues. See files/checks.json.

Run files/code/retrieve.py into a separate scratch root, then prepare.py, build_extra.py, check.py, run_parallel.py and report.py as described in files/REPRODUCE.md. The package contains all analysis code, fitted synthetic parameters, coefficients, p values, aggregate rates, exact source hashes, environment versions and the figure. Raw source data and derived region databases stay outside the signed package. See files/NOTICE.md for attribution and external terms. The exact SCI baseline license applies to the original code, text, figures and aggregate analysis results in this package.
