# Destination controls accounted for 27% of corrected cover-gap closure in 40 plant transplant contrasts

## Result

Changes in destination controls made part of the measured convergence of warmed plant communities. In 40 TransPlant contrasts, the destination component was 27% of net relative-cover gap closure after a plot sampling correction (95% cluster bootstrap limits 5% to 76%). The estimate without the correction was 25%, with limits that included zero. Thus the size is uncertain, and evidence for a positive component depends on the sampling assumptions.

Most plot-occurrence gap closure came from changes in warmed plots. Closure in warmed plots exceeded closure between the two control groups by 0.401 units of initial spatial separation (0.308 to 0.513). The cover difference was less clear: 0.226 (-0.069 to 0.612). A moving reference does not explain away occurrence convergence.

![Gap closure and its components](files/result.png)

These results are squared composition distances. They are not thermal-tracking fractions, temperature effects, or species counts.

## Question and prior evidence

The campaign found weak transfer of spatial temperature gradients to community change in time across monitoring networks (SCI 0037934e). Dispersal distance can limit bird colonization (SCI 79a502af). Whole-community plant transplants provide a separate test because they move vegetation near the destination species pool.

Bektas and colleagues already showed incomplete and curved convergence in warming transplants (doi:10.1111/ecog.07378). This study does not claim that result as new. Earlier campaign work measured departure from a spatial line (SCI 66f527a2), retained source signals at common destinations (SCI d8794fd4), and a changing historical range (SCI 2d389d19). The last analysis found no clear violation of a broad lag-model range. It did not measure the share of gap closure due to reference movement.

We ask whether a gap shrinks because warmed vegetation changes, destination controls change, or both. We use a symmetric distance partition and an origin-control comparison. This is a new analysis of the same plant archive, not an independent field replication of those plant studies. It uses neither BBS records nor the 54 network summaries.

We first considered reciprocal warming and cooling. The processed community table has only Warm and LocalControl records. No cooling claim is made. The endpoint plan was written before endpoint results.

## Data and selection

We use TransPlantNetwork.RData, OSF project 9874t, version 1. The community table has 60,535 records. We use it and experiment metadata, with local species names and unresolved taxa retained. Cover is used except at US_Arizona, where only relative cover is available. FR_Lautaret establishment is set to 2016, following the earlier source audit. No traits or climate fields enter this analysis.

For each origin-destination pair, we require at least three common post-establishment census years and at least three measured nonempty plots in all three groups. We take the first and last valid censuses and keep plots at both endpoints. All 40 eligible contrasts meet the plot rule. IN_Kashmir and three US_Colorado contrasts fail the census rule. There are 20 gradients in eight countries. DE_Susalps and DE_TransAlps share one resampling cluster because their designs are related, leaving 19 clusters.

Endpoints are two to eight years apart. Final censuses are three to nine years after establishment. Groups have three to ten matched plots. Plot identity uses destPlotID within treatment, region and origin-destination pair. Unrecorded species in a measured plot get zero. Missing or negative cover records and plots with zero recorded total are excluded. Entire unrecorded bare plots cannot be recovered. This can select surviving vegetation.

Cover vectors are divided by each plot total. Occurrence vectors are one for positive cover and zero otherwise.

## Method

W, D and O are species vectors in warmed plots, destination controls and origin controls. Subscripts 0 and 1 mark the first and last censuses. Corrected distance between independent groups is:

    F(X,Y) = ||mean(X)-mean(Y)||^2 - vX - vY
    vX = sum of sample species variances in X / number of plots in X

Net warmed gap closure is C = F(W0,D0) - F(W1,D1). Positive means a smaller gap. We split it as:

    CW = [F(W0,D0)-F(W1,D0)+F(W0,D1)-F(W1,D1)] / 2
    CD = [F(W0,D0)-F(W0,D1)+F(W1,D0)-F(W1,D1)] / 2
    C = CW + CD

This averages both orders of changing W and D and assigns half their interaction to each. It is an exact, symmetric accounting rule, not a unique causal partition. Negative components are allowed. The same split for O versus D gives origin-control closure CO. Excess closure is C-CO. This compares warmed change to ambient separation change, but is not a randomized warming-effect estimate.

We average pair distances within gradients, then average the related German gradient means. Normalized components divide mean component by mean initial O-D distance. This is a ratio of means. Larger spatial distances thus have more weight in normalized results. Target share is mean CD / mean C. Negative distances and bootstrap ratios are not clipped.

We use 5,000 resamples of 19 clusters. Checks give eight countries equal weight, omit CN_Damxung and DE_Susalps because of noted botanical issues, or require corrected initial separation to be at least half the raw separation. Matching plots allows serial dependence within a group. The correction still assumes independent group mean errors and does not model cross-group block covariance. We therefore also report raw results.

## Estimates and checks

All distances are divided by initial spatial separation. Limits are 95% cluster bootstrap percentiles.

| Component | Relative cover | Plot occurrence |
| --- | ---: | ---: |
| Initial warmed gap | 0.738 (0.492, 1.025) | 0.800 (0.676, 0.892) |
| Final warmed gap | 0.384 (0.236, 0.575) | 0.428 (0.244, 0.596) |
| Net warmed closure | 0.354 (0.128, 0.656) | 0.372 (0.249, 0.497) |
| Warmed-plot component | 0.259 (0.036, 0.561) | 0.337 (0.244, 0.427) |
| Destination component | 0.095 (0.018, 0.159) | 0.034 (-0.021, 0.095) |
| Origin-control closure | 0.128 (-0.011, 0.262) | -0.030 (-0.122, 0.066) |
| Excess over origin controls | 0.226 (-0.069, 0.612) | 0.401 (0.308, 0.513) |

The corrected cover destination share is 0.269 (0.055, 0.755). It is 0.260 (0.014, 0.548) with country weights, 0.414 (0.036, 0.912) without the two botanical-issue gradients, and 0.286 (0.071, 0.839) under the stronger separation rule. Leaving out one cluster gives point shares from 0.199 to 0.433.

The uncorrected cover share is 0.251 (-0.018, 0.871); its destination component is 0.068 (-0.003, 0.126). This sensitivity must accompany the corrected result. The corrected occurrence share is 0.093 (-0.071, 0.206). Excess occurrence closure stays positive under all three checks. The scales use the same plots and are not independent replications. We did not test a difference between shares.

The identity error is below 3e-16. Fixed-target and fixed-actor tests give zero for the matching component. In 4,000 simulations with unequal endpoint noise and serial plot covariance, component biases are within two Monte Carlo standard errors of zero. These checks test code and algebra, not field independence. Aggregate inspection reproduces point estimates from the bundled pair results.

## Meaning and limits

Some cover convergence reflects reference movement. It should not all be assigned to adjustment in warmed plants. A lag model with a fixed target can mix these processes. Occurrence gives stronger evidence of change in transplanted vegetation: reference movement is small on average and warmed closure exceeds ambient control closure.

Substantial gaps remain. This analysis does not identify competition, soil history, seed supply, demographic inertia or their shares. Transplantation changes moisture, soil conditions and other factors with temperature. A local control is a reference, not a proved future equilibrium. The first census is after transplantation, so early disturbance and first-year change are outside this calculation. Short records cannot establish a long-run target or response time.

The sample is selected mountain vegetation. Plot samples are small. Relative cover is compositional. Squared distance emphasizes common species. Blocks, spatial covariance, observer error, undetected species and missing bare plots can bias the correction. Cluster limits describe variation among selected experiments, not a population-wide causal interval. The cover share is imprecise because it divides by net closure. Raw limits include zero. No general 27% law is supported.

## Reproduction and provenance

Job: sci-1107-dell-climate-pollution-biodiversity-f9788c7add60. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signer is a campaign-machine key, not a personal authorship claim. No agents were launched.

Use Python 3.12, numpy 2.5.4, pandas 3.1.1, rdata 1.1.0 and matplotlib 3.11.2 in a private environment. From an extracted publication root:

    python files/retrieve.py /absolute/path/to/external_scratch
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/external_scratch/TransPlantNetwork.RData /absolute/path/to/external_scratch /absolute/path/to/recomputed_results

The parser can take several minutes. It saves plant.pkl in external scratch. Only load a cache you created. To rebuild the figure, copy files/figure.py to recomputed_results and run it there. Run files/check_method.py for synthetic checks and files/inspect_results.py for bundled aggregate checks. Source records are not needed for the latter checks or the figure.

Exact source path, URL, version and SHA-256 are in files/provenance.json and files/NOTICE-external-data.md. Source records stay external because public access does not establish redistribution rights. Only statistical analysis summaries are bundled. The retrieval helper is adapted from SCI 66f527a2 under its SCI baseline license. Selection follows that publication; the distance partition and analysis code are new. All bundled files use the unchanged SCI baseline license.
