# Joint structure improved spike prediction across held sessions and spatial regions in IBL data

Job: sci-1107-dell-neural-structure-and-computation-001063c6ed9d. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim.

## Question and result

Do input wiring and cell-type composition give useful joint prediction when both regional physiology labels and recording sessions are held out? We tested nine intrinsic spike measures in the IBL Brain-Wide Map. The common source sample has 176 regions, 59,047 good units and 455 sessions. Each of 20 global session splits retained 146 to 162 regions with enough data in both halves.

The joint structure model reduced cross-session prediction error by 17.9 percent against the spatial reference, 6.2 percent against the input model and 7.5 percent against the cell-type model. The joint model won in all 20 splits at each of three spatial lengths. This supports complementary prediction information across recordings. It does not give a fraction of causal control.

![Prediction transfer and repeatability](files/transfer.png)

Figure: A, each point is a session split, averaged across nine features and two transfer directions. Black bars give means. All four models include space and major division; input and types are additions to that reference. B, reduction in cross-session error from the joint model, against each named reference. Bars show split ranges, not confidence intervals. C, session-half map correlations before and after removal of division means. Bars again show split ranges.

## Prior work and scope

SCI 49479722 found different pair-similarity links for task coding and intrinsic spiking. SCI f4e4c5 found that distance-rewired nulls can be liberal. It also used session halves for an input-neighbour association test. SCI a4fae2 found joint intrinsic prediction gains with held spatial regions, but used one pooled physiology map for training and testing. SCI cdc62391 then found that two joint Gaussian covariance models failed residual checks. Thus, a quantitative biological partition remains unsupported.

Our test combines global session separation with nested spatial region validation. It asks whether the joint intrinsic prediction gain transfers to a second group of recordings. It does not repeat the prior rewiring test or estimate a new variance-component model. The use of repeated measurements to reduce noise bias is established in neural representation work (Walther et al. 2016, doi:10.1016/j.neuroimage.2015.12.012). Spatial validation is also established (Roberts et al. 2017, doi:10.1111/ecog.02881). The contribution here is the combined transfer test and measured repeatability of these nine regional maps.

## Inputs

IBL 2026_Q2 supplies unit quality, region labels, recording IDs, spike features and autocorrelograms. We keep quality label 1 and map each unit to its nearest Knox ancestor using Allen ontology graph 1. The nine features match f4e4c5: log firing rate, burstiness, interval memory, peak-to-trough duration, half-peak duration, log peak/trough ratio and three autocorrelogram indices. The last three use 3-10, 20-100 and 200-600 ms windows relative to the mean at lags of at least 1 s. Units and smoothing constants match the source code. Region values are pooled unit medians, not session means.

We reuse the 176-region common sample and structural definitions from a4fae2. Input similarity is the Gram matrix of square-root normalized Knox 2019 afferent densities, using all 291 sources and removing self edges. Type similarity is the Gram matrix of square-root neuronal supertype fractions from Allen MERFISH mouse 638850, release 20231215. Centroids come from CCF 2017, one hemisphere on a 40 um grid. The reference is a squared-exponential distance kernel plus a shared-major-division indicator. Exact paths, source versions, URLs and file hashes are in files/inputs.json and files/code/retrieve.py. External data and region-level derivatives remain outside the package.

## Method

For split indices 0 through 19, seed 106300 plus the index divides the 455 sessions into two global groups of 227 and 228. A session cannot enter both groups. A region needs at least five good units and two sessions in each half, and complete feature medians. This rule is applied before prediction and uses no error result. It gives a mean of 153.05 regions per split. The region sample can change between splits.

For each direction, A to B and B to A, we train only on the source-half map. Five coordinate k-means groups define outer test regions. Three new coordinate groups within each outer training set tune the penalty. K-means uses seed 1063 and ten starts. The four kernels are reference, reference plus input, reference plus types, and reference plus both. Addition weights equal one. Kernel ridge penalties are 0.001, 0.01, 0.1, 1, 10 and 100. Each feature is tuned separately by source-half inner test error. Kernel centering and target scaling use training regions only. The intercept is unpenalized.

The final predictions for each held region are scored against both its source-half median and its target-half median. No target-half phenotype enters training, tuning, centering or scaling for that direction. Errors are divided by the source outer-training feature variance. We average over regions, then features, then directions, then splits. The primary spatial length is 1 mm. The 0.5 and 2 mm conditions are planned sensitivity checks. All anatomical attributes are known at test time. This tests missing physiology, not missing anatomy.

We also measure Pearson correlation between the half maps, with and without separate division mean removal in each half. The normalized cross moment 2 covariance(A,B)/(variance(A)+variance(B)) is supplied as a descriptive repeatability statistic. It is not a causal or noise-corrected variance fraction. The local plan predates results but has no independent registration timestamp.

## Results

At the primary length, mean standardized squared errors were:

| Model | Same-session target | Disjoint-session target |
|---|---:|---:|
| Space and division | 1.2340 | 1.2298 |
| Plus input | 1.0771 | 1.0762 |
| Plus types | 1.0900 | 1.0907 |
| Plus both | 1.0086 | 1.0090 |

Same-session scoring here still holds out the spatial region. Its labels do not enter training. The small same-versus-cross change shows that these model rankings do not require the same recording group for training and target scoring. It does not show that sampling noise is absent.

The cross-session joint gain against space was 0.2207 standardized squared-error units, with split range 0.1472 to 0.4646. Against input the gain was 0.0671, range 0.0286 to 0.1266. Against types it was 0.0816, range 0.0374 to 0.1390. The joint model beat each reference in every split at 0.5, 1 and 2 mm. The relative joint gain against space was 17.0, 17.9 and 13.5 percent at those lengths. These are repeated uses of the same dataset, not 60 independent replications.

The joint model improved the mean cross-session score of all nine features against space at 1 mm. Three features had a negative gain in at least one split: burstiness, memory and the short-lag autocorrelogram index. Mean-only prediction, added as a post-result diagnostic, had cross-session error 1.4120. Errors above one are possible because a held spatial group can differ from the training distribution. The joint model improved on this mean-only reference as well.

Full-map half correlations ranged from a mean of 0.458 for memory to 0.891 for peak-to-trough duration. After division mean removal, the range was 0.237 to 0.506. For burstiness the mean fell from 0.641 to 0.343. For half duration it fell from 0.767 to 0.438. Thus, high brain-wide repeatability can partly reflect broad divisions. The weaker within-division repeatability places a practical limit on attempts to fit precise regional covariance shares from these medians.

## Checks and limits

Global session groups are disjoint and cover all sessions. Changing held-region source labels leaves predictions unchanged. An independent augmented ridge solve agrees with the kernel predictor within 6.1e-15. Input and type kernels have positive minimum eigenvalues. Rebuilt pooled medians match the source table within 7.74e-8. files/checks.json preserves these checks.

This is a new analysis of existing recordings, not an independent animal cohort. Different sessions can share mice or labs. Neither lab nor mouse independence is claimed. Both halves can repeat regional sampling biases, including depth, cell isolation and cell-type selection. Pooled unit medians weight dense sessions more. Spatial groups share divisions, and the reference does not control every anatomical variable. Structural sources are from other animals; the type data come from one MERFISH brain. The sample excludes sparsely recorded regions and changes across splits. The tuning grid, fixed kernel weights and kernel transforms limit generality.

The split ranges are sensitivity ranges. We assign no population confidence intervals or p values to them. We do not compare task reliability, recover a noise ceiling, explain the failed Gaussian residual checks, or prove a causal wiring-versus-types split. The result strengthens the claim of useful complementary intrinsic prediction across sessions. It also shows why whole-brain repeatability alone is too weak a basis for precise within-division biological fractions.

## Reproduction and rights

files/REPRODUCE.md gives commands for a fresh external scratch directory. The package preserves code, seeds, aggregate results for all conditions, checks, environment versions, provenance and the figure. No source matrix, unit table, region table or individual prediction is bundled. files/NOTICE.md identifies external sources and their terms. The exact SCI baseline license covers this package. No remote upload is part of this job.
