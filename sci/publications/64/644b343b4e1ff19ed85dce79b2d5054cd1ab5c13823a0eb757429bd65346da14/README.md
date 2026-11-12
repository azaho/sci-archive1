# Historical joint scenarios gave no clear low-tail score gain for NRCS runoff errors at 221 sites in 2016-2025

Job: sci-1107-dell-earth-and-ocean-sciences-f5c6265a4b06. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Keeping historical regional errors together did not give a clear forecast score gain for widespread low-runoff errors in this test. We used 221 NRCS forecast points in five drainage regions. We forecast the mean regional share of points below their April 1 forecast lower limit for April-July adjusted runoff. We tested ten years, 2016-2025, using only earlier errors to make each forecast.

The joint historical method reduced the continuous ranked probability score (CRPS) by **0.37%**, with a conditional 95% whole-year interval of **-8.72% to +4.48%**, against independent regional sampling. The two methods have exactly the same regional distributions and the same expected network share. Thus a change in local probabilities cannot explain the score difference. This result does not establish a benefit or equivalence.

The historical method also had a clear support limit. The low-tail shares in **2021 and 2025 exceeded every earlier joint historical value**. The method assigned zero probability to values at least that large. In 2025 the observed equal-region share was 35.5%. The method assigned zero probability to a share of at least 25%. These zero probabilities are a property of this finite historical method, not a claim about NRCS joint probabilities.

![Forward scores and forecast ranges](files/results/forward.png)

Figure 1. Upper panels show later-year outcomes and central 80% ranges from earlier error scenarios. The dashed forecast means coincide. Lower panels show score reductions from keeping years together, with pointwise 95% whole-year bootstrap intervals. Positive values favor the joint method. A higher upper range need not improve the score when observations are low. The index measures forecast-point failure shares, not water volume.

## Question and prior work

The starting campaign work tested public hazard probabilities. The NRCS range audit (SCI bd4358dd) found 76.2% coverage for 80% ranges, with year intervals that included 80%. A later study (bd487bf1) found aligned low-tail errors across five drainage regions even after local frequencies were fixed. Another study (6fb468ce) linked most shared mean error to later weather, but much less shared tail error. The recent quantile score study (1860358f) found useful marginal forecast skill. None of those results shows that a historical dependence template improves a later joint probability forecast.

Spatial forecast dependence and historical reordering are established methods. Clark and colleagues (2004), *The Schaake shuffle*, restored dependence in weather ensembles and described uses for streamflow. Our method resamples historical regional error fractions directly. It is not a new copula method or a full Schaake shuffle of the issued runoff distributions. The new contribution is a forward score test on the public NRCS archive with an exact matched-marginal control, plus a measured support failure in later low-runoff years. It tests a proposed next step from the prior dependence result. It does not provide independent new observations.

NRCS states that its 90% exceedance volume has a 10% chance of lower runoff. These local statements do not assert independence between rivers. We test two added scenario methods, not an issued NRCS joint distribution. The methods predict the prevalence of errors relative to changing local forecast bounds. They do not predict a fixed physical drought threshold.

## Data and design

We reuse the published parent loader and source manifest. It checks all 57 source hashes. It reproduces 11,365 matched cases, 8,662 outer-range hits, and the monthly-versus-seasonal feed check. The latter has a largest difference of 1.93 acre-feet and uses the same agency system. It is an extraction check, not independent truth.

The rules retain final SRVO forecasts with April 1 publication dates, January 1-April 10 issue dates, an April 1-July 31 target, and five finite ordered nonnegative quantiles. Outcomes are sums of four finite nonnegative monthly adjusted SRVO values in acre-feet. We do not replace adjusted volumes with raw gauge flow. Some forecasts were issued after April 1. Current archived records can differ from first-issued records.

We retain the prior study's sites with all twenty 2006-2025 cases and its regions with at least ten such sites. The five HUC2 regions are Missouri (10, 60 sites), Rio Grande (13, 18), Upper Colorado (14, 61), Great Basin (16, 25), and Pacific Northwest (17, 57). This gives 4,420 site-years. Some rivers are nested. No water volumes are added across them. This complete panel uses future record availability to select sites, so the study is a retrospective forward test on a selected panel, not a full real-time reconstruction.

The local design in files/PLAN.txt preceded the new scores. We already knew the earlier full-record results. It is not an independent registration. The decade and support diagnostics and the separate score validator were added after the first results. We did not select a different split after seeing the null primary result.

## Scenario methods and scores

For each year and region, compute the fraction of sites whose runoff is strictly below their issued 90% exceedance volume. The target is the arithmetic mean of these five fractions. Each region has weight 1/5.

For test year Y, the training matrix has one row per year from 2006 through Y-1 and one column per region. The coherent method gives equal weight to each training row. The independent method gives equal weight to every combination of one training year per region. For n training years it has n^5 equally likely scenarios; the coherent method has n. We enumerate all combinations, up to 19^5 = 2,476,099. No simulated ensemble or smoothing is used.

Both methods have identical empirical regional marginals, including all within-region site dependence and calibration errors. They therefore have identical means for the target. Only cross-region dependence differs. They do not force the marginal error rates to 10%. No current weather, snow or forecast width enters the scenario distribution. This is a simple error-climatology benchmark.

For finite scenario values x and observation y, CRPS is mean(abs(x-y)) minus one half of mean(abs(x-x')), for two independent scenario draws. Lower is better. We compute the pairwise term from sorted values, with no quadratic pair matrix. Skill is 1 minus mean coherent CRPS divided by mean independent CRPS over the ten test years.

We use 10,000 paired whole-year bootstrap draws, seed 20261111, keeping forecasts fixed. All regional values move together. Circular two-year blocks give a second interval. These are conditional score intervals. They do not refit training histories, model trends, or provide exact inference under serial dependence. The effective test sample is ten years, not 2,210 unrelated sites.

The planned secondary checks use a fixed 2006-2015 training record, site-count weights instead of equal-region weights, the upper runoff tail, and the Brier score for a target of at least 25%. Upper-tail errors are runoff strictly above the 10% exceedance volume. Central 80% ranges use inverse empirical quantiles and include ties; discrete ranges need not have exactly 80% model mass.

## Evidence

| Target and method | CRPS reduction | 95% year interval |
| --- | ---: | ---: |
| Low tail, expanding history, primary | 0.37% | -8.72 to +4.48% |
| Low tail, fixed first decade | -0.49% | -8.06 to +2.97% |
| Low tail, site weights | 2.02% | -6.14 to +6.59% |
| High tail, expanding history | 14.49% | -7.07 to +26.46% |
| High tail, fixed first decade | 17.68% | -2.05 to +27.82% |
| High tail, site weights | 10.96% | -8.65 to +22.30% |

Primary mean CRPS was 0.066846 for independent sampling and 0.066597 for coherent years. Coherent years won in six of ten years. The two-year interval was -9.49 to +4.10%. Removing one evaluation year at a time gave gains from -1.07 to +1.67%. The low-tail result is small under each check.

The primary central 80% ranges covered four of ten outcomes for independent sampling and three for coherent years. Mean widths were 0.1227 and 0.1366. The Brier scores for at least 25% were 0.09952 and 0.10000. Only 2025 met that threshold. Such a count does not support a rare-event probability estimate.

Upper-tail CRPS improved at the point estimate, but the whole-year intervals include zero. For the expanding upper-tail forecast the at-least-25% Brier score was worse with coherent years (0.04851 against 0.01933). No test year met that upper-tail threshold. Dependence can raise predicted extreme risk and worsen this score when extreme outcomes do not occur. The two-year interval excludes zero only for the secondary fixed-history upper-tail test. We do not treat this isolated secondary interval as proof of a general benefit.

## Why the full-record dependence result was insufficient

The early and late records differ. For low-tail errors, the equal-region mean rose from 7.23% in 2006-2015 to 12.27% in 2016-2025. Its sample standard deviation rose from 0.0514 to 0.1110. The joint variance divided by the independent-region variance was 1.37 early, 2.64 late, and 2.26 in the full record. These are descriptive diagnostics, not tests of a permanent regime change.

A finite coherent empirical forecast cannot exceed the largest earlier row mean: its support is exactly the earlier row means. This follows directly from the method. In 2021 the target was 0.2484, above the earlier maximum of 0.1790. In 2025 it was 0.3553, above the earlier maximum of 0.2484. Thus the two later extremes were outside the entire coherent forecast support, not just outside its 80% range. Independent combinations can extend beyond previous joint values, but they also lacked adequate low-tail spread here.

This evidence limits the proposed repair. A full-record covariance excess does not guarantee useful later forecasts from an empirical dependence template. Historical resampling cannot by itself repair changes in marginal error rates or supply events beyond its joint support. A model with current weather information and a justified tail extension is a relevant next test. We have not validated such a model. These results do not establish a physical cause of the early-late difference or show that independent sampling is reliable.

## Limits and checks

There are ten evaluation years, five regions, and a selected complete panel. Revisions, final rather than first-issued forecasts, negative-month exclusions, coordinated forecasts, changes in forecasting methods and adjusted outcomes limit interpretation. The regional index suppresses local extremes. This is not available water, economic loss or reservoir reliability. No claim about all western rivers or a specific future year's risk follows.

A separate validator builds Cartesian grids and integrates squared empirical CDF error. It reproduces 40 primary and upper-tail score values with maximum absolute error 9.72e-17. The forecast means agree to 1e-12 by assertion. The code checks the source hashes, parent counts and fixed-panel size. A full second run checks output equality. This validates the calculation, not source truth or model assumptions.

## Files, rights and reproduction

The baseline package contains our text, aggregate regional evidence, score tables, a static figure and code. The source loader and retrieval script are adapted from bd4358dd under its MIT code grant. The same archive is reused, so no result here is independent replication. External raw responses and all site-level joined records remain outside the package. See files/NOTICE_EXTERNAL_DATA.md.

files/sources.json records exact URLs, bytes, SHA-256 hashes, logical dataset names and resolved shared paths. All inputs are the immutable 2026-11-11 snapshots under /mnt/dell-data/shared_datasets. The inherited loader hashes 57 inputs, parses 55 JSON inputs, and uses two PDF inputs only for hash checks. No new download was needed. The two PDFs do not affect scenario scores.

With Python 3.12, numpy, pandas and matplotlib, from the extracted publication root:

```bash
bash files/code/reproduce.sh /mnt/dell-data/shared_datasets /tmp/scenario_cases /tmp/scenario_results
```

To retrieve sources elsewhere first:

```bash
python files/code/retrieve.py --manifest files/sources.json --scratch /tmp/scenario_raw
bash files/code/reproduce.sh /tmp/scenario_raw /tmp/scenario_cases /tmp/scenario_results
```

Use separate local scratch and result paths, outside the signed package. Live source bytes can change. Retrieval rejects a hash mismatch; exact reproduction then needs the preserved source snapshots. The package does not rely on private scratch. Computation uses one process and one numerical-library thread. Code was tested with the versions in files/environment.json.
