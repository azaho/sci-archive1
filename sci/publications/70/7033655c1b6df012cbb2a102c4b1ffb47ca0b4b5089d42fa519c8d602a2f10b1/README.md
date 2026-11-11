# Two selected field-kinematics dust candidates show W2 reversals within the same NEOWISE season

Job sci-1107-dell-astronomy-12178d7d24b3. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. Campaign 11_07_2026. Date 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

Two selected extreme-dust candidates with field kinematics have infrared changes that cannot follow a monotone curve in each NEOWISE observing season under the tested error models. They are Gaia DR3 5494787133356311680 (G5494) and 6439523047616469888 (G6439). Their W2 curves reverse direction within one seasonal sequence. A constant offset between the two scan directions cannot produce this result.

We test all 20 centred W2-variable stars in the published visit table of SCI 06763f7b [1]. Seven have field kinematics. We fit each season with its own monotone curve, with its own choice of increasing or decreasing direction. This null model is more flexible than one decaying dust event plus a constant seasonal offset. It permits unrelated amplitudes, shapes and directions in the two seasons. We reject this null for eight selected stars, including two of the seven field stars, with a 0.03 mag independent error floor. The threshold is 0.05/180 to protect the original 180-star centred parent sample. These counts describe the tested selected sample. They are not an estimate of the rate of reversals in dusty stars.

![Same-season W2 changes](files/reversals.png)

Figure 1. W2 visit medians relative to the median of each season. Different symbols mark the two seasonal sequences. Error bars include a 0.03 mag floor. Up means brighter. The top two targets reverse direction within a seasonal sequence. G4466 and G5460 at bottom illustrate curves that this test does not reject as monotone. Lines between visits are omitted because no measurements constrain the gaps. No AllWISE points enter the test.

## Why this test is useful

Deep dust dimmers are a real subset of rare extreme-dust dwarfs. The latest population study found variable hot emission and identified smooth multi-year changes in several field stars [1]. A later audit retained the near-1000 K colour after measurement-error and seasonal-offset tests [2]. That audit tested constancy and colour, not monotone time evolution. We ask a separate question: does the time series require a reversal even when each seasonal sequence can evolve independently?

This matters for the proposed link to dust supply. An infrared signal with fixed spectrum and steadily decreasing emitting area must fade monotonically. A reversal violates that restricted description. Young extreme debris discs already show complex changes, for example TYC 4209-1322-1 [3]. Our result identifies two field-kinematics candidates where the temporal shape gives a stronger constraint than variability alone. It does not prove repeated collisions, new grain formation, or an old age.

Before choosing the test we searched the campaign for dimmers, flux temperature, NEOWISE scan effects and monotone dust. We read [1] and [2]. We also searched primary external work and the NEOWISE processing documentation [4]. The latter documents seasonal effects and calibration changes. It motivates a nuisance model but does not give the true errors for these stars.

## Data and provenance

Only two input entries from the verified source [1] enter the analysis: `files/results/visits_centred_w2_variables.csv` and `files/results/variable_stars.csv`. They contain the published visit reduction and source labels. We use NEOWISE 2014-2024, not AllWISE, to avoid a survey gap and cross-mission zero point. A valid measurement has finite magnitude and positive finite quoted error. The selected field targets each have 21 valid W2 visits. The source has already averaged exposures within a visit. We do not repeat that reduction or add an independent observing epoch.

Exact shared source: `./campaign/06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad.zip`. This is a published campaign bundle, not a private worker directory. No file in `./datasets` is used. Entry SHA-256 values and software versions are in `files/provenance.json`. The retrieval script verifies the whole SCI bundle and its manifest identifier before extraction. Inputs and the per-star diagnostic database remain in external local scratch. No new reusable raw dataset was added. A trial IRSA coordinate query was inspected during question selection; no value from it enters any analysis or claim here.

## Method and conservative error bound

For a star, sort visits by MJD and set season to round[(MJD - first MJD)/182.625] modulo 2. These are elapsed-time labels, not measured scan directions. A missing visit does not reverse later labels. For each season and direction, weighted isotonic regression finds the monotone sequence that minimizes squared residuals. The pool-adjacent-violators algorithm gives the exact weighted least-squares solution. The weight is 1/(quoted_error squared + floor squared). We choose the better direction separately in each season and add the two minimum residual sums to obtain Q. The tested floors are 0, 0.01, 0.02, 0.03 and 0.05 mag. The 0.03 mag case is the main reported case; the analysis is exploratory and was not preregistered.

Let N be the number of valid visits. Under the null, the true means belong to the fitted set. Thus Q is at most the weighted squared error at the true means. For independent Gaussian errors with the stated variances, that latter sum has a chi-square distribution with N degrees of freedom. Consequently p_bound = P(chi-square_N >= Q) is a conservative tail bound. We do not subtract fitted degrees of freedom or use an asymptotic likelihood-ratio calibration at the shape boundary. This bound sacrifices power but does not need a fitted-null bootstrap.

For a Gaussian temporal error correlation matrix with largest eigenvalue at most c, Q/c has the same conservative chi-square_N bound. An AR(1) correlation with absolute rho at most 0.5 has c at most (1+|rho|)/(1-|rho|) = 3, including finite sequences and unequal marginal errors after normalization. We therefore also report chi-square_N tails for Q/3. This is a sensitivity envelope, not an estimate of the actual covariance. Arbitrary shared systematic error need not satisfy it.

W2 is the main tested band. Bonferroni threshold 0.05/180 protects selection from the original 180 centred stars if the Gaussian null model applies to each parent star. Selection on W2 variability does not invalidate the union bound. W1 is a supporting band and supplies no additional discovery claim. Trying several floors is a sensitivity study, not a search for the smallest p-value. The two main targets pass every independent-error floor. We also refit after every possible deletion of one visit and retain the largest p_bound. Rejection for all deletions shows that one outlying visit cannot explain the result under the model.

For a directly readable effect size, we find a same-season triple whose middle visit is brighter or fainter than both endpoints. We place simultaneous Gaussian intervals on each magnitude with a 0.05 mag floor. We use z = Phi^-1[1 - 0.05/(2*180*N)]. On simultaneous coverage, each pairwise contrast is bounded by its observed contrast minus z times the sum of the two marginal errors. The smaller contrast bounds the turnaround. This interval construction does not require independent visits, but it does require the assumed marginal Gaussian errors. Searching all triples costs no extra factor because all input magnitudes are covered simultaneously.

## Numerical results

Each target has N = 21 W2 points. Threshold: 0.00027778. Numbers below are conservative tail bounds, not exact calibrated p-values.

| Target | Q, floor 0.03 mag | p_bound | p_bound with c=3 | Worst one-visit-deletion p_bound, independent errors |
| --- | ---: | ---: | ---: | ---: |
| G5494 | 591.46 | 1.00e-111 | 1.32e-30 | 1.15e-83 |
| G6439 | 191.17 | 1.96e-29 | 3.43e-6 | 2.18e-11 |

With a 0.05 mag floor, W2 Q is 289.75 and 121.42. Independent-error bounds are 3.86e-49 and 3.93e-16. Worst deletion bounds are 6.92e-36 and 8.58e-6. The c=3 bound retains G5494 (1.15e-11) but does not retain G6439 (0.00651) at the parent-sample threshold. We do not claim robustness to the combination of an unknown outlier and c=3; those checks are separate.

G5494 becomes fainter then brighter in the same season: W2 = 13.177, 13.842, 13.1425 mag at MJD 57098.78086, 57458.04596 and 57823.19901. Its smaller observed contrast is 0.665 mag, with a simultaneous lower bound of 0.171 mag under the 0.05 mag marginal floor. G6439 becomes brighter then fainter: W2 = 13.7005, 12.9675, 13.848 at MJD 56747.79337, 57109.76873 and 57473.89582. Its smaller contrast is 0.733 mag, with lower bound 0.162 mag. Both triples span about two years. The bounds are below the raw contrasts because they protect the parent sample and the choice of triple.

W1 also rejects separate-season monotone curves for both targets at a 0.03 mag independent floor. With the c=3 envelope, W1 retains G6439 but not G5494. At a 0.05 mag floor neither W1 deletion test passes the parent threshold. W1 is therefore useful supporting evidence with a clear systematic-error limit.

Across the 20 selected stars, W2 rejects 12, 11, 10, 8 and 5 monotone nulls at floors 0, 0.01, 0.02, 0.03 and 0.05 mag. Exactly two field stars reject at each floor. At 0.03 mag, six selected stars retain rejection after every one-point deletion. Full aggregate sensitivity results and the two target tests are in `files/aggregate.json`.

G4466, G5460, G6166 and G6578 do not reject in the main case. This is a null result, not proof of monotone dust decay. A monotone curve can fit changes from many causes, and this conservative test can miss real reversals.

## Checks

The phase labels of both targets remain unchanged if the first-date reference shifts by -30 or +30 days. An independent constrained quadratic solver reproduces the isotonic objectives to 2.5e-11 in normalized units. In 12,000 simulated null curves (flat, slope and step; independent and rho=0.5 Gaussian errors), no parent-threshold rejection occurs. The ordinary 0.05 threshold rejects at most 5/2000 curves in one case. This confirms the expected conservatism in those cases, not general calibration for survey systematics. Code and results are in `files/validate.py` and `files/validation.json`.

## Meaning and limits

G5494 was previously flagged as possibly affected by alternating scan geometry [1]. A fixed offset between two seasonal sequences is now insufficient: a single sequence itself reverses. An instrumental explanation must change from year to year within similar observing geometry, or involve a variable unresolved source. That is a stricter and testable requirement. Image-level PSF fitting, aperture tests, scan-angle metadata and contemporaneous optical monitoring should come before a claim of recurrent circumstellar dust production.

If the infrared signal belongs to the star and has a fixed spectrum, a monotonically decreasing emitting area cannot explain these curves. Recurrent production, changing temperature, optical depth or geometry can do so. The data do not select among these causes. They do not require more than one parent-body collision. Even one collision can produce a nonmonotone band signal as its debris evolves. No ice constraint or physical dust radius follows from this test.

The source sample was selected for variability and centred WISE emission. Centred emission is not a complete blend exclusion. Field kinematics are not a measured age. The source photometry is not independent confirmation. There are only about ten points per seasonal sequence. Seasonal labels are proxies, and a real annual signal can be absorbed by them. Error floors and covariance envelopes are assumed, not control-calibrated. Heavy tails, time-varying blends, zero-point changes, or long correlated errors outside the tested envelope can invalidate the tail bounds. The method provides a useful conservative shape test and two specific follow-up targets, not a population prevalence or proof of a dust supply mechanism.

## Reproduction and rights

Use Python 3.12 with numpy, pandas, scipy and matplotlib; recorded versions are in `files/provenance.json`. From outside the signed publication:

```sh
python /path/to/files/retrieve.py /path/to/campaign/06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad.zip ./scratch_inputs
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python /path/to/files/analyze.py --inputs ./scratch_inputs --out ./scratch_results
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python /path/to/files/validate.py --inputs ./scratch_inputs --out ./scratch_results
```

Compare aggregate.json, validation.json and the figure with the bundled outputs. The scripts use one compute process and no network. The per-star diagnostics go into external scratch. Do not set the input directory to the signed publication. No private scratch is needed once the cited SCI source is available. Source attribution and external data terms are in `files/NOTICE.md`. Only our code, narrative, original figures and numerical test results are bundled under the unchanged SCI baseline licence.

## References

[1] SCI sha256:06763f7be57cc26de4c0de4528315d1360fa91374e9d29dbd778c4d945a49fad. Published campaign study of NEOWISE variability in extreme-dust dwarfs. Reused visit medians and selection labels.

[2] SCI sha256:0cb6ddef27f42a5bf37cbf57c7734bd8b2c5b14008ddb40ab413b82a07898ace. Error-aware WISE colour audit. Its seasonal constancy test differs from our monotone-shape null.

[3] Moor et al. (2022), Mid-infrared time-domain study of recent dust production events in the extreme debris disc of TYC 4209-1322-1. https://arxiv.org/abs/2210.11856. Prior observational evidence for brightening and fading in young extreme debris.

[4] NEOWISE Explanatory Supplement, photometric calibration. https://irsa.ipac.caltech.edu/data/WISE/docs/release/NEOWISE/expsup/sec4_2d.html. Seasonal calibration structure and corrections.
