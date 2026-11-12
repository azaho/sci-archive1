# Earlier shared errors reduced shortage-fraction forecast loss by 21% at 166 NRCS sites in 2013-2025

Job: sci-1107-dell-earth-and-ocean-sciences-1b1e26ce7e07. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signer is a campaign-machine key, not a personal authorship claim.

## Result

Earlier shared forecast errors improved a forward test of the fraction of rivers with unusually low runoff. The test used 166 NRCS forecast points in four western US drainage regions. Each point had a complete 2000-2025 record. In 2013-2025, resampling earlier years together reduced continuous ranked probability score (CRPS) by **21.3%**, with a **95% whole-year interval of 11.9-34.7%**, against independent sites with exactly the same local probabilities. Lower CRPS is better. The target was the fraction of sites below their current issued lower runoff bound. This is a fraction of forecast points, not a fraction of water volume.

The added value of links *between* regions was less clear. Against a reference that kept all dependence within each region, shared years reduced CRPS by **2.8%**, with limits of **-5.3 to +7.8%**. Thus prior evidence of aligned regional errors does not yet establish a forward score gain from cross-region links. Most of the measured improvement over independent sites was already present when the four regions were made independent.

![Forward joint-error scores](files/results/joint.png)

Figure 1. The left panel shows observed low-runoff failure shares and the common mean of both forecasts. The middle panel shows annual CRPS differences. The right panel shows pooled and regional loss reductions with pointwise whole-year intervals. No correction for multiple regional comparisons was made.

## Question and prior work

The selected SCI work found errors in public hazard probabilities. The NRCS range audit (bd4358dd...) found 76% coverage for stated 80% ranges across 571 points, with year-block limits that included 80%. A later study (bd487bf...) found shared tail errors at 221 points in five regions. A weather study (6fb468ce...) linked shared mean errors to later weather, but left much of the joint tail variation unresolved. A proper-score study (1860358...) found that issued quantiles beat earlier runoff history. Those results use overlapping archives. They are not independent data replications.

We ask whether the earlier error pattern can supply a useful *forward distribution* for the number of failures. A dependence diagnostic from a full record does not answer that question. A joint forecast must use earlier outcomes only and must pay the score cost of broadening its distribution when few failures occur.

Historical dependence templates are established methods in hydrology. Clark et al. (2004), *The Schaake shuffle*, and Scheuerer et al. (2017), doi:10.1002/2016WR020133, construct linked forecast scenarios from earlier patterns. We do not introduce resampling or dependence modelling. Our contribution is an exact, reproducible forward score test for public issued-bound failures, with identical local probabilities in the controls and a separate test of cross-region value. This extends the prior archive diagnostics into a tested joint-risk tool.

NRCS defines its 90% exceedance volume as a lower bound with a 10% chance of lower runoff. NRCS does not state that different rivers are independent. Neither reference below is an official NRCS joint product. The result tests a supplement to individual bounds, not a false joint probability issued by NRCS.

## Data and scope

The inherited loader checks all 57 source hashes in files/sources.json. These are immutable AWDB snapshots retrieved for the prior studies on 2026-11-11. They are stored in the shared HP SSD dataset store through /mnt/dell-data/shared_datasets. The manifest records exact logical dataset names, resolved file paths, source URLs, byte counts and SHA-256 hashes. No new data download was needed.

The loader reproduces 11,365 matched cases and 8,662 outer-range hits at 571 sites. It selects final SRVO forecasts with April 1 publication dates, issue dates from January 1 through April 10, an April 1-July 31 target, and all five ordered nonnegative quantiles. It converts forecast units to acre-feet. Outcomes are sums of four finite nonnegative monthly adjusted SRVO volumes at the same site. These are adjusted flows, not independent unregulated gauge measurements. The separate seasonal-feed check is retained in the loader; it uses the same agency system.

We require all 26 years, 2000-2025. This gives 173 points. We then retain HUC2 regions with at least ten complete points. The final sample has 166 points: Missouri (53), Upper Colorado (50), Great Basin (20) and Pacific Northwest (43). The Rio Grande and most southern points are not represented. There are 4,316 site-years, of which 2,158 are test cases in 13 years. Sites can be nested. They are not independent experimental units. Completeness selection uses future archive availability, so the result is conditional on this retrospective panel.

files/PLAN.txt records the primary test before its new scores were computed. Prior results were known. This is a local design record, not an independent registration. The comparison that makes regions independent and the quarter-network Brier scores were added after the primary score was seen. They are exploratory. An initial slow version of the added comparison was stopped; a cached metadata lookup gave the same specified calculation.

## Forecast construction

For site i and year t, let B_it be 1 when adjusted runoff is strictly below the current issued 90% exceedance volume, and 0 otherwise. Ties count as no failure. The target is K_t/N, where K_t is the sum of B_it across the N sites.

For each test year t from 2013 through 2025, training uses 2000 through t-1 only. Let m=t-2000. Three distribution forecasts are compared:

1. **Shared years.** Select one of the m earlier years with equal probability. Use its entire vector of failure indicators as the scenario. The forecast distribution of K is the empirical histogram of earlier annual counts.
2. **Independent sites.** At each site, estimate p_i as its fraction of earlier years with a failure. Draw sites independently with these p_i. Compute the exact count distribution by repeated polynomial convolution of [1-p_i, p_i].
3. **Independent regions, added test.** Keep the empirical count histogram within each region, then convolve the four histograms. This retains all within-region dependence but makes regions independent.

All three give each site exactly the same probability p_i and give K exactly the same mean. They differ only in how the indicators occur together. Their p_i values are earlier error frequencies, not the issued nominal 10%. Both main methods therefore use the same empirical correction for local marginal errors. The result cannot be caused by changing the marginal probabilities or the predicted mean. There is no Monte Carlo approximation to the count distributions.

This tool predicts *forecast failure fractions*. It does not construct physical flow ensembles or forecast a fixed-volume shortage. It uses current issued bounds to define the target, but uses no issue-time snow, weather, median, width or trend predictors. It assumes earlier failure patterns remain informative. It is a simple benchmark for joint risk, not an optimal operational model.

For probabilities P(K=k), let F(k) be their cumulative sum. We calculate CRPS in fraction units exactly as:

    CRPS = sum over k=0,...,N-1 of [F(k) - 1(k >= K_observed)]^2 / N.

This equals E|X-y| - E|X-X'|/2 for X=K/N. It is a proper score for the count distribution. Skill is 1 minus total shared-year CRPS divided by total reference CRPS.

Intervals resample all test years together, keeping both forecasts paired, for 10,000 draws with seed 20261111. Circular two-year blocks test a short serial dependence reference. These intervals condition on the fitted expanding forecasts and the source records. They do not refit training samples. They assume exchangeable years or the stated block reference; they do not protect against arbitrary trends or long memory.

## Evidence

| Test | CRPS loss reduction | 95% year interval |
| --- | ---: | ---: |
| Primary: shared years vs independent sites | 21.3% | 11.9 to 34.7% |
| Fixed training, 2000-2012 only | 23.6% | 13.6 to 34.9% |
| Later evaluation subset, 2016-2025 | 17.0% | 5.7 to 31.1% |
| Added: shared years vs independent regions | 2.8% | -5.3 to 7.8% |

Primary mean CRPS was 0.06043 for shared years and 0.07677 for independent sites. Two-year blocks gave 11.7-34.0% limits. Leaving one evaluation year out at a time gave 19.3-26.0% skill. The fixed-training test uses the same test years and sites. The later subset is overlapping evidence, not a new holdout selected without knowledge of the original results.

For the lower-bound test, regional reductions were 27.8% in Missouri (10.7-45.2%), 10.8% in Upper Colorado (-6.5 to 32.8%), 15.5% in Great Basin (4.6-31.1%) and 15.5% in Pacific Northwest (8.1-28.8%). The Upper Colorado gain is uncertain.

Secondary tests use failure below the other four issued quantiles. Their pooled gains were 10.6% for the 30th runoff percentile (-17.0 to 20.5%), 14.3% for the median (-10.4 to 23.6%), 24.2% for the 70th percentile (7.9-35.0%), and 31.3% for the 90th percentile (12.9-46.3%). These tests do not all establish gains. They have no multiplicity correction and were planned as secondary checks.

The mean test failure share was 9.82%; the common mean forecast was 9.26%. This close pooled mean conceals large annual variation. Mean forecast variance of the failure fraction was 0.00714 for shared years and 0.000466 for independent sites, about a factor of 15 apart. Broader scenarios improved the proper score overall, but made it worse in five of thirteen test years. The outcome is not a rule to maximize spread.

## Severe events remain unresolved

At least a quarter of the 166 sites fell below their lower bounds in 2021 and 2025: 46 and 68 sites. The shared-year method assigned an average probability of 6.8% to this event; independent sites assigned about 6.4e-10 on average. The observed frequency was 2/13, or 15.4%. These are descriptive numbers from only two events. They do not estimate a stable return period or establish calibration of the shared-year tail.

Exploratory Brier scores for that event were 0.1390 for shared years, 0.1538 for independent sites, and 0.1480 for independent regions. We did not pre-specify this event score, and we do not claim clear improvement for severe events from it. An empirical forecast cannot assign positive mass beyond its largest earlier count. It can therefore miss a new extreme. A continuous or smoothed joint model and issue-time weather information remain important test targets.

## Checks, limitations and reproduction

All forecast distributions sum to one within 1e-12. Their means agree within 1e-12 in every comparison. An independent standard-library audit calculates primary scores from aggregate probability tables using the absolute-distance identity; the maximum difference is 3.89e-16. A second full run checks exact numerical output equality. Code uses one process and one numerical-library thread.

The archive contains final records and can include revisions. Some retained forecasts were issued after April 1. A calendar-forward split is not original-vintage verification. Current station regions and outcome adjustments can differ from historic records. The selected complete panel excludes many rivers and three regions from the earlier dependence study. Equal-site weighting gives larger regions more influence. Nested sites make this an index of points, not a water portfolio. Only thirteen test years support inference. Neither the score gain nor the prior weather association proves a causal error source or future decision benefit.

The package includes original code, text, aggregate statistics and a static figure. Raw responses and record-level tables remain external. files/NOTICE_EXTERNAL_DATA.md gives attribution and source terms. The exact baseline license does not replace those external terms. The inherited loader and retrieval code are reused under the cited parent's MIT grant. All source bytes actually read are listed in files/sources.json. No private scratch is needed to reproduce the result when those exact external snapshots are available.

From the extracted publication root, use Python 3.12 and the packages in files/environment.json:

    bash files/code/reproduce.sh /mnt/dell-data/shared_datasets /tmp/joint_cases /tmp/joint_results

On another machine, first retrieve into separate scratch:

    python files/code/retrieve.py --manifest files/sources.json --scratch /tmp/joint_raw
    bash files/code/reproduce.sh /tmp/joint_raw /tmp/joint_cases /tmp/joint_results

Live responses can change. Retrieval rejects any source hash mismatch; exact immutable snapshots are needed in that case. Do not write outputs into the signed publication. annual.csv holds region-level scores and summaries. primary_distributions.csv holds the exact pooled count distributions, not site records. results.json gives all tests, audit.json gives independent checks, and reproduction.json records the repeated run. No raw data were re-licensed or included.
