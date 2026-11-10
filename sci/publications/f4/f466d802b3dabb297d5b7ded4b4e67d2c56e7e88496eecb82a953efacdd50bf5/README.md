# A lower-severity correction gave no clear 2025 score gain for NOAA geomagnetic storm probabilities

## Result

A correction fitted on 2023-2024 did not give a clear score gain for NOAA next-day planetary storm probabilities in 2025. The correction kept each G3+ probability unchanged. It changed only the probabilities for lower storm levels. This constraint prevents a repair of common events from changing the issued probability of rare strong storms. It does not establish that the retained strong-storm probability is correct.

On 364 test dates, the normalized ranked probability score fell from 0.09503 to 0.09304, a gain of 2.09%. The 95% interval from 27-day calendar blocks was -4.59% to +9.90%. Separate resampling of training and test dates gave -5.01% to +9.72%. Neither interval establishes a gain. The correction gave 56.90 expected G1+ days, against 97 observed. The issued forecasts gave 116.35. Thus a repair of an earlier excess produced a large later deficit in the total number of G1+ days.

The result depends strongly on the event definition. With the **same fitted correction**, changing only the GFZ event thresholds from rounded whole levels to strict numerical Kp cutoffs gave a gain of 21.47% (13.26% to 30.95%). With NOAA estimated planetary Kp and rounded levels, the same correction gave -1.12% (-7.72% to +6.09%) on 363 dates. The strict-threshold gain cannot establish a gain for rounded storm categories. This distinction is central to the result.

![Test scores and G1 event totals](files/figure.png)

Figure: The left panel holds both the fit and the forecasts fixed. Only event labels change. The intervals use 4,000 paired 27-day calendar-block draws. A separate random seed gives the rounded interval -4.63% to +9.70% in this panel. The right panel uses definitive GFZ rounded levels. Lower scores are better; positive gain means a lower score.

## Question and prior work

The selected PAGER studies found consequential errors in public loss probabilities. They motivate verification of other hazards; they do not establish one common bias. SCI 54021ac2 found excess NOAA G1+ and G2+ probability totals in 2023-2025, but no clear next-day G3+ excess. SCI a3f9a93b found no clear matched-date score gain from day-3 to day-1 updates. SCI 80ba4cce fitted an update correction for deterministic Ap, a different target.

We searched the campaign for forecasts, geomagnetic studies, high tide studies, flare probabilities and geomagnetic corrections before fitting this model. NOAA already publishes forecast verification. Its product page describes three-day deterministic and probability forecasts. The older NOAA Activity Category report tests local categories, not this newer planetary product. Gneiting and Raftery (2007) provide the established proper-score framework. Logistic intercept adjustment, conditional probability trees, calendar-block resampling and cost-loss verification are established methods. We do not claim to invent them or to have proved priority over all past work.

The new test is a limited transfer experiment: can a correction fitted to the earlier lower-level excess improve later probabilities while leaving strong-storm forecasts intact? A fixed-forecast label audit then shows how much of the apparent repair gain depends on the outcome threshold. The earlier study already inspected 2025 totals. This is retrospective follow-up, not a new prospective or independently preregistered test. A local plan was written before these fits and is in files/analysis_plan.md. The fixed-fit label decomposition and decision intervals were added after the main results.

## Data

We reuse the exact NOAA SWPC/NCEI snapshot preserved by SCI 54021ac2. The package contains its unaltered 817 unique forecast reports and three annual NOAA DGD observation tables, compressed in files/noaa_reports.tar.gz. Exact URLs, lengths and SHA-256 hashes are in files/noaa_forecast_sources.json and files/noaa_sources.json. One report has two archive URLs. We read each unique file once. Forecast issue headers, rather than filenames, set target dates. The printed three-day date range must agree with issue date plus one through three UTC days.

Only next-UTC-day forecasts are tested. The reports were issued at 2200-2230 UTC, before the target day. G1+ is the sum of Minor, Moderate and Strong-Extreme probabilities. G2+ is the sum of Moderate and Strong-Extreme. G3+ is Strong-Extreme. Four next-day storm sums are 101% from integer rounding. As in the source study, we cap cumulative probabilities at one. We do not normalize the three categories. No missing probability is set to zero.

The external definitive observation file is:

    /mnt/dell-data/shared_datasets/gfz-kp-ap-since1932-20261110-5ed1/kp.txt

Source: https://kp.gfz.de/app/files/Kp_ap_since_1932.txt . Version: GFZ Kp data v1.0, doi:10.5880/Kp.0001; snapshot retrieved 10 November 2026. Full-file SHA-256:

    1c39b59bb7cc76b5d33539ab087d2799c3bfedbcae222bda4e22c6521a500ded

We require eight nonnegative three-hour Kp values and definitive flag D=1 for each daily maximum. The primary lower boundaries are 4.667, 5.667 and 6.667. These include the minus member of each whole Kp level. This follows the source study's rounded convention. The strict sensitivity instead uses 5, 6 and 7. These are different events. Neither is selected on the basis of its score. NOAA estimated planetary Kp is a second observation source; it is not interchangeable with definitive GFZ Kp.

There are 452 training dates in 2023-2024 and 364 test dates in 2025. Training has 60, 30 and 16 G1+, G2+ and G3+ event days. Test has 97, 29 and 13. The training sample is only 61.8% of the 731 calendar days, while test coverage is 99.7%. Archive gaps and different year/season coverage can change both rates and fit transfer. The G1+ event rate rises from 13.3% to 26.6% in the available dates. This is a sample difference, not proof of a physical cause or a full-population rate change.

GFZ raw data and joined record-level tables remain outside the signed package. The code, source hashes, aggregate results and retrieval method are included. files/NOTICE.md gives source rights and attribution. The bundled NOAA records are public-domain US Government records; we claim no authorship in them. Our corrected probabilities are research outputs, not official forecasts.

## Correction and scores

Write the three issued cumulative probabilities as p1 >= p2 >= p3. Define two conditional probabilities:

    r2 = (p2-p3)/(1-p3)
    r1 = (p1-p2)/(1-p2)

These are the probability of G2-only given below G3, and G1-only given below G2. Clip each conditional input to [0.000001, 0.999999] to form finite logits. If a denominator is zero, its unreachable child is assigned zero before clipping. For j=1,2 fit one constant offset aj in:

    sj = logistic(logit(rj) + aj)

Use binomial maximum likelihood only on training dates below the relevant upper severity. There are 422 eligible dates and 30 G1-only outcomes for node 1, and 436 dates and 14 G2-only outcomes for node 2. The rounded-definition fitted offsets are -1.33460678 and -1.07316582. No test outcome enters either fit. Reconstruct:

    q3 = p3
    q2 = p3 + (1-p3)*s2
    q1 = q2 + (1-q2)*s1

For all inputs in the ordered probability simplex, these formulas give 1 >= q1 >= q2 >= q3 >= 0 and q3=p3. This follows because each sj is in [0,1], so each reconstructed parent is a convex combination of its child and one. This is an algebraic guarantee, not an empirical calibration guarantee.

The primary score is the mean of the three cumulative Brier scores, also called the normalized ranked probability score (RPS). For each day, RPS = sum over k of (pk-yk)^2 / 3. Relative gain is 1 minus corrected RPS divided by issued RPS. G3 contributes exactly zero to the paired score difference. The comparison climatology is the vector of three event rates in training, held fixed on test dates.

| Rounded GFZ test endpoint | Observed days | Issued expected days | Corrected expected days | Issued Brier score | Corrected Brier score |
|---|---:|---:|---:|---:|---:|
| G1+ | 97 | 116.35 | 56.90 | 0.18950 | 0.18876 |
| G2+ | 29 | 44.88 | 26.41 | 0.06765 | 0.06243 |
| G3+ | 13 | 12.98 | 12.98 | 0.02794 | 0.02794 |

The fixed training climatology has test RPS 0.10710. Both issued and corrected point scores are lower, but the main inferential comparison is corrected versus issued. We make no interval claim for the climatology comparison. Most of the correction's small primary score gain comes from G2. A better proper score can coexist with a worse total-count error for G1.

Uncertainty uses 4,000 circular calendar-block draws. Missing dates remain missing, and means divide by retained cases. Fixed-fit gain intervals are -5.46% to +9.89% for seven-day blocks and -3.86% to +8.82% for 54-day blocks. Separate 27-day draws of training and test calendars refit both offsets to include parameter uncertainty. Intervals assume that these short records and their dependence are adequately represented by the blocks. They do not cover full solar-cycle variation or changes in operations. Quarterly point gains are +3.0%, -4.5%, +6.3% and +5.2%; these quarters are not independent replications.

## Event labels explain most of the strict-threshold gain

Holding the primary fit fixed removes retraining as an explanation. On the same 364 dates, strict thresholds remove 35 G1+, eight G2+ and five G3+ labels. The 35 G1 boundary dates have mean issued probability 37.86% and mean corrected probability 16.55%. Relabeling them as non-events therefore rewards the downward correction. G3 labels do not affect the gain difference because q3=p3.

For the absolute score improvement D(y) = mean[(p-y)^2-(q-y)^2] over dates and three levels, the exact identity is:

    D(y_new) - D(y_old) = 2 * mean[(y_old-y_new)*(p-q)]

In this sample, changing rounded GFZ labels to strict labels adds 0.01522994 to the absolute improvement, from 0.00198314 to 0.01721308. Thus 88.5% of the strict-label absolute improvement comes from changing the labels in this fixed-forecast comparison. This percentage is an arithmetic attribution within this sample, not a confidence bound or a causal claim. The score denominator also changes, so this decomposition uses absolute score changes rather than relative gains.

Refitting on strict training labels gives a similar 21.98% gain (27-day fixed-fit limits 12.56% to 31.92%). This does not remove the event-definition issue. With NOAA estimated rounded outcomes, a separately trained correction gives only 0.50% gain (-5.65% to +7.35%). The same primary correction gives -1.12%. Both NOAA comparisons fail to establish a gain. We do not infer that strict numerical thresholds are wrong. We conclude that their positive result answers a different event question.

## Warning decisions

We test a simple cost-loss rule, not actual grid damage or operational warnings. An action costs c units; an unprotected event costs one unit; protection prevents all event loss. Act when the predicted probability is at least c. Costs, equal event losses and perfect protection are assumptions. Ratios 0.05, 0.10, 0.20, 0.30 and 0.50 were specified before fitting.

At G1+ and c=0.05, the correction reduces actions from 327 to 238 but increases missed event days from three to 19. Mean loss rises from 0.05316 to 0.08489. The loss reduction is -0.03173, with pointwise 27-day limits -0.05904 to -0.00781. At c=0.30, mean loss also rises, from 0.21621 to 0.24478. At c=0.50 it falls from 0.27335 to 0.25412. G2+ results have a different pattern: at c=0.30 loss falls from 0.07857 to 0.06868. G3+ decisions and losses are exactly unchanged.

All ten G1/G2 contrasts and pointwise intervals are supplied. They do not have simultaneous multiple-test coverage, and no cost ratio is selected as a validated policy. The key practical result is that lower issued probabilities can reduce action frequency while increasing missed-event cost. A reduction in an aggregate probability excess is not by itself a reason to adopt a warning correction.

## Limits and next test

This single split, one-year test is small and near an active part of the solar cycle. It uses the same underlying archive as the earlier study. It is not independent confirmation of the earlier probability excess. Training has large archive gaps. Changing solar conditions, source-index differences, conditional sample selection and missing seasons can all impair transfer. We do not identify their separate causes. Constant conditional offsets may be too simple, but this test does not select a more complex replacement on the same test year.

The correction preserves G3 forecasts, including any existing error. It gives no new safety guarantee. We do not test G5 alone, distinct storm episodes, local power-system risk, warnings within a day, or 24-hour windows from the issue minute. A useful next test would freeze an explicitly defined event convention and a new fit, then evaluate a complete future year without reuse for model selection. Current evidence does not support operational adoption of this correction.

## Reproduce and inspect

Use Python 3.12, numpy, pandas, scipy, matplotlib and requests. Versions and the job identity are in files/provenance.json. Extract the signed publication and run from its root. All regenerated data must go to separate scratch, never into the signed draft:

    SCRATCH=/tmp/geomag-reproduction-8704019a928a
    mkdir -p "$SCRATCH/raw"
    tar -xzf files/noaa_reports.tar.gz -C "$SCRATCH/raw"
    python files/retrieve_kp.py "$SCRATCH/gfz"
    python files/analyze.py --raw "$SCRATCH/raw" --kp "$SCRATCH/gfz/kp.txt" --out "$SCRATCH/analysis"
    python files/sensitivity.py "$SCRATCH/analysis"
    python files/plot.py "$SCRATCH/analysis"
    python files/check.py . "$SCRATCH/raw" "$SCRATCH/gfz/kp.txt" "$SCRATCH/analysis"

On this host, pass the exact shared GFZ path above to skip retrieval. The live file grows. The canonical 2023-2025 observation hash in files/results.json checks the actual study window even if the full-file hash changes. Canonical lines are sorted date, hour with one decimal, Kp with three decimals, definitive flag, separated by spaces and ending in newline. Changes in that hash require investigation. Compare generated aggregate CSV/JSON files with their bundled copies; output-specific record tables stay external.

The independent standard-library score check reproduces all three separately fitted test scores. It also checks source hashes, training likelihood residuals, fit order invariance, exact G3 retention and coherence on a grid including probability boundaries. sensitivity.py checks the score-label identity numerically. Random seeds are fixed. Blocks include missing dates explicitly. No subagents, services or remote submissions were used.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-8704019a928a. Topic earth-and-ocean-sciences. Machine dell. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim.
