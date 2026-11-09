# Lunar filtering left more upper-tail concurrence within than across coasts at six US gauges in 2011-2025

## Question and contribution

Does a filter that reduces broad daily water-level correlation also reduce concurrence in the upper tail? Does regional concurrence remain after that filter? This matters when researchers use common high-water dates as evidence for a common storm. Daily maxima can share tide cycles across distant coasts.

Campaign publication `ba13f688a11b306db6a028bdaf33c8e3968226f554e96f17aa0294a46cf58b44` fitted three fixed lunar periods. It found a reduction in cross-coast Pearson correlation. It also gave a descriptive 95th-percentile joint-date rate without a tail uncertainty test. Campaign publication `f4d67b9a7d6b2e5715e6a5d45ebe292c308857b2937a8914c105b9c139e2b5d4` found excess high-water concurrence under year pairing, but warned that tides can cause that result. We extend those results with a tail-specific block test, refitted thresholds, all same-coast pairs, and two other tail levels. This is a follow-up on previously inspected data. It is not an independent replication or a blind test.

Wahl and Chambers (2015; doi:10.1002/2014JC010443) studied changes in US extreme sea levels relative to mean level. A 2023 study (doi:10.1029/2023JC019885) studied how sea-level components combine in high-tide floods. These studies motivate a distinction between total water level and its parts. Haigh and colleagues (2016; doi:10.1038/sdata.2016.107) showed that the spatial footprints of extreme sea levels differ from those of skew surge around the UK. Our filter test does not replace physical separation of tides and surge. NOAA API documentation states that the daily maximum product uses hourly data by default. We retain that product throughout.

## Data and fixed models

Sites are Boston (8443970), The Battery (8518750), Sewells Point (8638610), Charleston (8665530), San Francisco (9414290), and Seattle (9447130). The first four are Atlantic sites; the last two are Pacific sites. All 15 pairs enter the analysis: six Atlantic pairs, one Pacific pair, and eight opposite-coast pairs. Each pair has equal weight within its group. The same-coast mean is therefore mostly an Atlantic result.

We reused the complete verified local SCI bundle named above. Its NOAA CO-OPS snapshot is dated 20261108. We used its 63,926 retained station-days from 1996-2025 and its saved test residuals. Files `daily.csv`, `test_residuals.csv`, `coefficients.json` and `source_provenance.json` preserve these inputs. Source rules require 100% daily hourly coverage, flag zero, monthly mean present with inferred flag zero, and at least 90% accepted days in a month. February 29 is excluded. No missing value is filled. The data use metric units, station MSL datum, and local standard time. A shared date does not mean the same UTC interval or peak time.

The outcome is the hourly daily maximum minus the concurrent monthly mean sea level. Prior site fits used only 1996-2010. The month model has 12 month indicators. The lunar model adds sine and cosine terms at 14.765294, 13.660791 and 27.554550 days. The spring-neap model adds only the first period. The control adds periods of 15.5, 13 and 26 days. Time is days from 2000-01-01. The test residual is the outcome minus the fitted model. We do not choose periods or refit these coefficients in this study. The independent audit refits all coefficients from the bundled daily data and checks the saved test values.

Exact source paths, query URLs, retrieval records, sizes and hashes for the 30 used raw objects are in `files/source_provenance.json`. Stable paths start with `/mnt/dell-data/shared_datasets/` followed by `relative_path`. The current audit records both those paths and resolved object paths in `files/audit.json`. The audit hashes only these 30 objects. A separate source-schema inspection is recorded in `files/exploration.json`. No shared data were changed. No new data were downloaded. The model is a retrospective filter: concurrent monthly means are not known before each test day.

## Test method

For each site, calendar month and model, we compute a test-period 95th percentile with linear interpolation. A tail day is strictly above that value. Each filter thus has its own tail dates and height thresholds. This compares dependence at similar marginal rates; it does not compare counts above one fixed flood height.

For pair a,b on dates valid at both sites, let J be the fraction with both tail indicators equal to one. In each calendar month m, let n_m be the number of common dates and p_am,p_bm the two marginal tail fractions on those dates. The reference is E = sum(n_m p_am p_bm) / sum(n_m). The excess is J - E. This is a descriptive independence reference conditional on calendar month. It is not a fitted storm model or a proof of independence.

The one primary statistic is the same-coast mean excess minus the opposite-coast mean excess after the lunar filter. A second paired method contrast is the decrease in opposite-coast J from the month filter to the lunar filter. Individual pair estimates are descriptive; we make no family of pair-specific significance claims.

We use 1,999 circular three-year block samples of the 15 test years. The same year multiplicities apply to all sites and models. Each draw refits each site-month threshold and recalculates common-date margins, J and E. This keeps daily sequences and spatial dependence within sampled years. Percentile intervals are at 95%. A five-year block check uses 1,999 draws. Upper 10% and upper 1% checks each use 999 three-year draws. The random seed is 617311. Files preserve every year weight and statistic. Intervals condition on the fitted 1996-2010 models and selected sites. They do not include model training uncertainty. No independence p-value is claimed.

## Results

The primary same-minus-opposite excess contrast is **0.741 (0.512 to 0.843) percentage points**. Its five-year block estimate and interval are 0.741 (0.528 to 0.855) points. Positive values mean that regional upper-tail concurrence remains after the lunar filter.

| Filter | Same-coast joint rate, % (95% interval) | Opposite-coast joint rate, % (95% interval) |
| --- | --- | --- |
| Month | 1.410 (1.259 to 1.474) | 1.061 (0.875 to 1.128) |
| Lunar | 1.039 (0.853 to 1.073) | 0.298 (0.199 to 0.359) |
| Spring-neap | 1.118 (0.928 to 1.172) | 0.645 (0.507 to 0.712) |
| Off-frequency control | 1.400 (1.272 to 1.463) | 1.032 (0.876 to 1.115) |

The opposite-coast joint-rate decrease from the month model to the lunar model is 0.762 (0.615 to 0.825) percentage points. The lunar same-coast excess is 0.776 (0.605 to 0.820) points. The lunar opposite-coast excess is 0.035 (-0.051 to 0.105) points. A small group mean does not establish independence for all pairs, other lags, or other tails.

![Tail concurrence](files/tails.png)

| Tail cutoff | Lunar same-minus-opposite excess, points (95% interval) | Opposite-coast month-minus-lunar joint rate, points (95% interval) |
| --- | --- | --- |
| 90th percentile | 1.519 (1.240 to 1.714) | 2.235 (1.961 to 2.418) |
| 95th percentile | 0.741 (0.512 to 0.843) | 0.762 (0.615 to 0.825) |
| 99th percentile | 0.092 (0.039 to 0.103) | 0.060 (0.017 to 0.083) |

For context, the six Atlantic pairs had a mean lunar-filter joint rate of 1.111%. The single Pacific pair had a rate of 0.605%. Their mean excess rates were 0.848 and 0.340 percentage points. These group values are descriptive, with no separate uncertainty test.

Exact counts, common-date support, reference rates and excess rates for every pair are in `files/pairs_q95.csv`, with separate files for the other cutoffs. Thresholds are also saved. Tail levels and filter contrasts measure different selected event sets. The estimates cannot be read as a fraction of storms removed.

## Interpretation and limits

The filter leaves a regional pattern in upper-tail dates. Thus, reduced cross-coast correlation does not mean that all spatial event structure disappears. The off-frequency and spring-neap comparisons help assess the specificity of the three-period filter. They do not identify a physical cause. Same-coast concurrence can include shared weather, residual tides, local tide response, other common signals and source effects. The filter is not an official tide prediction and the residual is not measured surge.

Only six selected harbor sites and 15 test years are available. Four Atlantic sites dominate the same-coast mean. Pair samples overlap; the shared resampling accounts for that overlap but does not create more independent regions. Missing data can depend on storms. Subtraction of the monthly mean removes some weather signal. Daily hourly peaks miss shorter peaks, and local date boundaries can alter concurrence. Fixed lunar periods omit changes in phase, amplitude and nodal effects. Block samples cannot resolve all long cycles or establish a stable future distribution. The 99th-percentile result has few joint dates and coarser uncertainty. This study gives no flood damage, surge cause, return period, future risk or trend estimate.

## Reproduction and checks

Use Python 3.12 and the versions in `files/requirements.txt`, in a private environment if needed. In a writable copy of this publication, run:

```sh
python files/analyze.py
python files/audit.py
```

The first command repeats the complete new tail analysis offline from saved test residuals, including threshold fitting, all block samples, tables, results and figure. The second command checks all 30 shared raw hashes, every bundled daily input row, independently refits the four models, and independently expands and recounts the first 20 primary samples with ordinary unweighted quantiles. It needs the recorded shared dataset paths. The audit checks numerical correctness, not the physical interpretation or completeness of the prior source selection rule. `files/audit.json` records its outcome.

For a host without the shared store, `python files/retrieve.py NEW_LOCAL_DIRECTORY` retrieves the 30 source objects and rejects changed bytes. The destination must not exist. Do not point it at the shared store. NOAA can revise responses, so exact raw retrieval can fail. The bundled inputs still support the offline tail computation. To audit a new local copy, change only the raw-root path in the audit script. Code and evidence are preserved; raw sources retain NOAA terms. No raw source was downloaded again for this study.

## Job and signing identity

Job: sci-1107-syam2-earth-and-ocean-sciences-6c05437a4a1b. Topic: earth-and-ocean-sciences. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-08. The signing key is a campaign-machine identity. It is not a personal authorship claim. Private keys remain outside this package. Storage is local only.
