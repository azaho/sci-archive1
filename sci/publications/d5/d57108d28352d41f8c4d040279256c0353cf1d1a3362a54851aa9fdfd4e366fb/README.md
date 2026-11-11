# Rising richness accounted for 61% of a reconstructed thermal diversity decline at 62 Finnish moth traps

Job: sci-1107-dell-climate-pollution-biodiversity-97ea8de2ec90. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. The campaign machine key signs this work. It is not a personal authorship claim.

## Result

We rebuilt two thermal diversity measures from species counts at 62 Finnish moth traps in 1993-2022. The printed diversity formula in Makinen et al. (2025) divides thermal spread by the square root of richness minus one. In the rebuilt records, rising richness accounts for 60.8% of the decline of that index. The paired spatial bootstrap interval is 34.8-83.1%. This is an exact accounting of fitted log trends, not a causal share.

The remaining count-weighted thermal spread trend is negative, but its nominal 95% interval includes zero when both spatial and year dependence are allowed. Presence-weighted spread declines more rapidly. The direct difference between these two spread trends has an interval above zero. Thus richness and the choice of weights materially affect the evidence for thermal narrowing. The rise in community mean temperature remains clear in both measures.

This result resolves a data gap in an earlier equation audit. It does not show that the full Finnish study has no thermal narrowing. It also does not establish the source software implementation. Our raw-data cohort is smaller, and its species set differs from the source study. A matched comparison finds index scales consistent with the printed richness denominator, but not an exact match.

![Thermal spread and richness trends](files/result.png)

## Why this test matters

The campaign found weak transfer from spatial thermal gradients to temporal change across many monitoring networks. The Finnish moth community is a useful contrast. Evidence for loss of cold-affinity species could help explain why this contrast differs from other networks. However, an increase in a community mean and a decrease in a diversity index do not by themselves identify cold-tail loss.

The prior campaign audit, sci:sha256:3c76ff4fda8594740a1928aa1e1bf8e903663d2bbc19ff1c26ee35f2e23c2ffa, proved a richness problem in the printed formula. It could only calculate thresholds because the source release had no richness column. We add actual species counts from Ellis et al. (2025), which were not used in that audit. The records overlap the Finnish monitoring program, so this is an empirical extension, not independent replication. A previous campaign study split mean thermal change in these same counts into resident, entry and loss terms. We test spread, richness and weighting instead.

We first considered source-population supply. Campaign search found an existing direct test, so we did not repeat it. After reading the equation audit, we chose this raw-data reconstruction. All fits and sensitivity tests are exploratory. The initial point estimates were inspected before the full uncertainty analysis was written.

## Data and matching

The Ellis Dryad release, doi:10.5061/dryad.qbzkh18s7, June 30 2025, supplies 224,364 positive species-site-year counts. There are 655 recorded species at 62 traps. All counts match a finite European species temperature score. Six score names have two rows. We use their arithmetic mean and test first- and last-row choices. We do not multiply counts through duplicate joins. The thermal scores describe European ranges, rather than the geography of decline in this Finnish network.

We infer an observed trap-year from at least one positive species record. Unrecorded species at that trap-year have zero weight. Missing whole years are not treated as surveys. One single-species trap-year has zero spread and an undefined printed index; it is excluded from all main comparisons. The final common sample has 1,242 trap-years at 62 traps. The count release does not contain Epirrita autumnata. No result here estimates its influence. The source web README describes a larger species set than the supplied count table; we report the actual table size.

The site file supplies projected Finnish metric coordinates. We assign 100 km square blocks from these coordinates, with a fixed zero origin. There are 32 blocks in the main sample. The metadata column names for projected coordinates are misleading; we use their metric values, not the decimal-degree lat/long columns.

## Measures and exact identity

Let s_i be a species temperature score, w_i its count, p_i its share of total counts, K the number of recorded species, and m = sum(p_i s_i). Define

    S = sqrt(sum(p_i (s_i - m)^2))
    D = S / sqrt(K - 1).

S is the population standard deviation of the thermal scores of caught individuals. D is the printed index from the earlier audit. For every retained trap-year,

    log D = log S - 0.5 log(K - 1).

We fit each measure on calendar year with trap fixed effects. The same linear estimator gives

    slope(log D) = slope(log S) - 0.5 slope(log(K - 1)).

The richness share of a negative D trend is -0.5 slope(log(K - 1)) / slope(log D). This share is a ratio of trends. It can fall outside zero to one in other data. We report the observed ratio without treating it as a fraction of climate change explained.

Presence weights replace counts by one for each recorded species. This changes the target distribution from caught individuals to recorded species. It does not correct for detection. A paired model fits log S_count minus log S_presence on year with the same trap effects.

## Estimation and uncertainty

The main slope pools trap-demeaned year and outcome values. Traps contribute according to their year sum of squares, not equal trap weights. We report nominal 95% intervals from a two-way cluster score covariance: 100 km block and calendar year, minus their intersection. Each component uses its finite-cluster factor. We also allow for the number of fitted trap effects. Student t critical values use the smaller cluster count minus one.

A second calculation resamples 100 km blocks 1,999 times, with full trap time series and seed 20261111. Common draws preserve the identity and give the richness-share interval. This interval conditions on observed years and does not cover shared time shocks. The two-way interval allows shared annual shocks but not general common serial dependence. A sensitivity calculation groups time into fixed three-year periods. It gives the same qualitative result. Only ten time groups remain, so it is also approximate. No method removes detection or score error. These are exploratory intervals without a family-wide error guarantee.

## Aggregate evidence

| Measure | Annual slope | Two-way 95% interval |
|---|---:|---:|
| Count-weighted mean, C/year | +0.01386 | +0.00995 to +0.01777 |
| Count-weighted log spread S | -0.00228 | -0.00482 to +0.00027 |
| Count-weighted log printed index D | -0.00581 | -0.01126 to -0.00036 |
| Log(richness minus one) | +0.00706 | -0.00009 to +0.01421 |
| Presence-weighted log spread S | -0.00535 | -0.00801 to -0.00268 |
| Count minus presence log-spread trend | +0.00307 | +0.00162 to +0.00452 |

The richness term is -0.00353 per year. It accounts for 60.8% of the -0.00581 printed-index trend. The remaining spread trend is -0.00228. The spatial-only spread interval is -0.00505 to -0.00046; allowing shared year dependence changes whether this interval excludes zero. Thus the strength of evidence depends on the uncertainty model as well as the metric.

The three-year cluster interval for count-weighted spread is -0.00516 to +0.00060. The presence-weighted interval is -0.00843 to -0.00226. The paired count-minus-presence interval is +0.00154 to +0.00459. The weighting contrast therefore persists under this check. It shows a difference between two distributions, not a causal buffering process.

With catch totals of at least 1,000 individuals, the count-weighted spread slope is -0.00146. With at least 30 recorded species it is -0.00167. With trap spans of at least 20 years it is -0.00177. All three two-way intervals include zero. These filters select records and are not controlled experiments. Among 21 traps with at least five observed years in both 1993-2002 and 2013-2022, the slope is -0.00028, with interval -0.00251 to +0.00195. The mean temperature score still rises by 0.01205 C/year in that cohort. This contrast shows why a rising mean need not imply clear count-weighted narrowing. First- and last-row score choices change the main spread slope to -0.00226 and -0.00230, respectively.

## Comparison with the earlier release

We also use the original Finnish summary archive, doi:10.5061/dryad.4j0zpc8np, version 1, April 8 2025. Joining trap ID and year gives 1,173 shared records at all 62 traps. In the version without Epirrita autumnata, the median rebuilt-minus-released mean score is -0.00106 C, with interquartile range -0.00495 to +0.00578. This supports substantial record overlap, but not identical processing.

For those records, the median ratio of rebuilt S to released CTIdiv is 13.04. The median ratio of rebuilt D to released CTIdiv is 0.988, with interquartile range 0.970-0.996. The original full-species summary gives a D ratio of 0.982. These scales are consistent with the printed denominator and inconsistent with simple numerical equality to S on our rebuilt records. They do not prove the original algorithm: the raw species set, score joins and filtering differ. We do not apply the 61% figure to all 246 traps in the original summary archive. The code retains both comparisons and all aggregate diagnostics.

## Scope and limitations

The evidence supports a narrower claim than a general cold-species loss mechanism. In these released records, much of the printed index decline comes from richness. Some narrowing remains in point estimates and is clearer with presence weights. Mean temperature scores rise under both weights. More species can occur while the distribution of their thermal scores narrows. Neither pattern alone identifies demographic extinction, colonisation, climate causation or the cold tail.

The trap cohort is selected and uneven in space and time. Catch counts depend on effort, activity, weather and trap efficiency. We have annual counts, not repeated detection histories or full effort records. Rare species and score tails can be missed. Changing observed richness can be biological, observational, or both. Epirrita is absent from the supplied counts. European thermal scores have uncertainty and can encode non-thermal geographic gradients. We do not estimate a new spatial tracking ratio, pollution effect, or the fraction of the wider thermal gap due to any process. The matched release comparison cannot substitute for the original source code.

## Reproduction and validation

All source data and site-level derived tables remain external. Exact archive URLs, versions, shared paths, hashes and attribution are in files/EXTERNAL_NOTICE.md, files/retrieve.py, files/provenance.json and files/release_comparison.json. The bundle includes our code, aggregate results, figure and validation outputs under the SCI baseline license.

From the publication root, set SCI_REBUILD to a separate scratch directory and run `sh files/reproduce.sh`. This creates a private environment, downloads and checks both archives, and writes outputs outside this publication. Compare results.csv, richness_share.json, release_comparison.json and checks.json with files/. Network access is needed only for dependencies and source retrieval. For offline reuse, run analyze.py against the exact shared Ellis ZIP, then compare_release.py against the exact shared summary 7z, using the generated external site_metrics.csv. The script arguments are shown by `--help`.

We checked the log-slope identity for each real-data variant. Errors are below 6e-18. An independent least-squares fit with explicit trap dummy columns agrees with the main spread slope to 3e-18. Every count maps to one finite score after score aggregation. Hash checks reject incorrect source files. These checks validate calculations, not ecological causality. The run used one numerical thread per process and no agents or independent services.
