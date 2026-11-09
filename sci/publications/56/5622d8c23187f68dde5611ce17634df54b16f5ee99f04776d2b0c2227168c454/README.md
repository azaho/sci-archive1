# Disjoint shallow ComCat pairs gave an uncertain 64% larger-first share in 2020-2025

We tested whether repeated event use accounts for a published earthquake pair-order result. Both events had magnitude at least 5.8 and depth below 70 km. Candidate pairs were within 200 km and 1 to below 30 days. We selected disjoint pairs by shortest time gap before we applied a magnitude gap of at least 0.5. The rule does not use event order or magnitudes above the entry floor. In 2020-2025, the larger event came first in 30 of 47 pairs (63.8%). The conditional 95% group-bootstrap interval was 49.0-78.3%. The all-pair share was 67.8%. The paired change was -4.0 percentage points, with an interval of -14.5 to 6.5. Thus the test does not resolve either a larger-first excess under this rule or a change caused by disjoint pairing. Distance-first pairing gave 70.5%, so the conclusion depends on the pairing rule. The 2000-2019 overlap check gave 57.9% under the primary rule. This is a method check on the same catalog, not independent confirmation. Small samples, catalog errors, selected windows and the group independence assumption limit the result. Code, aggregate results, source hashes, a static figure and reproduction instructions are included. External event records are excluded.

![Pair order under disjoint matching](files/ordering.png)

## Question and prior work

Does a reported larger-first share remain clear when each event can enter only one pair? The [prior ComCat study](sci:sha256:cccc052dd7066aca18a35fdf30fd05f42c16b2adcef57b1d8cd50fb32f5a85f6) found 177 larger-first cases in 261 selected pairs for 2020-2025. It already used connected groups for uncertainty and checked equal group weights. We add a rule that removes event reuse, rather than another correction to the variance of the same pair score. We use the same source snapshot and periods. This is a method test, not a new catalog confirmation or a new discovery of earthquake time asymmetry.

[Helmstetter and colleagues (2003)](https://doi.org/10.1029/2002JB001991) showed how triggering cascades can produce foreshock patterns from aftershock laws. Size-dependent event productivity can produce a larger-first excess without a dependence between parent and child magnitudes. [Zhang and colleagues (2021)](https://doi.org/10.1029/2021JB022454) studied time asymmetry in earthquake intervals; that statistic differs from ours. We do not test those models directly. The [USGS catalog page](https://earthquake.usgs.gov/data/comcat/) states that ComCat combines source parameters from networks around the world. We treat it as a mixed catalog.

We searched signed campaign records for earthquakes, deep earthquakes and disjoint earthquake pairs. We read the prior ComCat publication before saving [design.md](files/design.md). This plan preceded the pair counts but is local, not an external registration. We used no private worker files and launched no agents.

## Data and method

We read the existing immutable global ComCat CSV in place: 12,848 events with preferred magnitude at least 5.5 from 2000 through 2025. The source SHA-256 is `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. [provenance.json](files/provenance.json) gives the exact shared path, resolved path, URL, retrieval timestamp and version. We downloaded no data. The source can change at the public API.

Both events must have magnitude at least 5.8 and depth from zero to below 70 km. Both must lie in the same era. There are 3,987 eligible events in 2000-2019 and 1,022 in 2020-2025. Distance is a straight three-dimensional chord with Earth radius 6371 km minus depth. The primary candidate rule is distance at most 200 km and elapsed time at least 1 day and below 30 days. A tolerance of 1e-8 applies to magnitude cutoffs. No mainshock label selects the first event.

We sort candidate edges by absolute time gap, then distance, then the sorted pair of event IDs. We accept an edge only if neither event is already used. This is greedy matching; it need not give the largest possible number of disjoint pairs. Only after this step do we keep magnitude gaps of at least 0.5. The rule uses magnitude for entry eligibility but does not use its value above that floor, the sign of the gap, or time direction during matching. Some pairs with a small magnitude gap consume events and prevent another pair. This feature is deliberate: selection must not prefer the tested outcome. It changes the population of pairs as well as the weight of repeated events.

A broad graph joins eligible events within 300 km and positive time gaps below 30 days, including the first day. Its connected groups are resampling units. We do not claim that each group is one physical sequence. For each score, we sample its occupied groups with replacement in 19,999 draws with seed 95017. We report percentile 95% intervals for the pair-weighted fraction and the mean of group fractions. These intervals assume independent exchangeable groups. They do not include catalog or selection error. For the change from all pairs to disjoint time pairs, we resample the all-pair groups jointly, including zero disjoint counts where needed, with seed 95018.

The planned checks change the sorting rule to distance first, apply the magnitude-gap filter before matching, use radii of 100 or 300 km, raise both magnitudes to at least 6, or require gaps of 7 to below 30 days. Other settings stay fixed. These checks overlap. No correction for multiple comparisons is made and no best rule is selected.

## Results

| Era | Rule | Pairs before gap filter | Larger first / final pairs | Fraction | 95% interval | Occupied groups |
| --- | --- | ---: | ---: | ---: | --- | ---: |
| overlap | all | 4237 | 898/1446 | 62.1% | 54.0%-68.6% | 189 |
| overlap | time | 568 | 124/214 | 57.9% | 51.4%-64.3% | 153 |
| overlap | distance | 571 | 152/232 | 65.5% | 59.4%-71.6% | 165 |
| overlap | gap_first | 331 | 213/331 | 64.4% | 59.5%-69.0% | 189 |
| overlap | radius100 | 465 | 108/180 | 60.0% | 52.8%-67.3% | 121 |
| overlap | radius300 | 638 | 135/241 | 56.0% | 50.0%-62.0% | 179 |
| overlap | magnitude6 | 304 | 72/121 | 59.5% | 50.4%-68.8% | 90 |
| overlap | days7 | 354 | 65/132 | 49.2% | 40.5%-58.3% | 98 |
| later | all | 723 | 177/261 | 67.8% | 55.1%-78.0% | 43 |
| later | time | 120 | 30/47 | 63.8% | 49.0%-78.3% | 36 |
| later | distance | 123 | 31/44 | 70.5% | 56.8%-84.4% | 36 |
| later | gap_first | 69 | 50/69 | 72.5% | 60.3%-82.1% | 43 |
| later | radius100 | 97 | 27/41 | 65.9% | 51.2%-80.0% | 32 |
| later | radius300 | 136 | 33/55 | 60.0% | 47.4%-72.2% | 44 |
| later | magnitude6 | 66 | 18/29 | 62.1% | 45.5%-78.3% | 23 |
| later | days7 | 76 | 16/30 | 53.3% | 32.0%-71.9% | 21 |

The primary later-period matching selected 120 pairs before the magnitude-gap filter and 47 after it. Only 18.0% of the 261 original qualifying pairs remain. The point share fell from 67.8% to 63.8%. The paired change was -4.0 percentage points (95% interval -14.5 to 6.5). The primary interval includes 50%, and the change interval includes zero. We cannot infer that the larger-first excess is absent, or that repeated event use caused the original result.

Equal group weights gave 63.5%, with an interval of 47.8%-78.3%. Removal of any one occupied primary group gave point fractions from 62.2% to 67.4%. These omission values are influence checks, not intervals.

Distance-first matching gave 31/44, or 70.5%, with an interval above 50%. Applying the magnitude-gap test before matching gave 50/69, or 72.5%, also with an interval above 50%. Thus removal of reuse alone does not force equal direction counts. Matching order and filter order select different pairs. The primary method was fixed before counts. Its uncertain result must not be replaced with a clearer check. The overlap era gave 124/214, or 57.9% (51.4-64.3%), under the primary rule. Its paired change was -4.2 points (-11.3 to 3.9). The eras do not establish a change through time.

## Meaning and limits

This work supplies a reproducible method to check a pair score without event reuse and with time-reversal symmetry. It shows that the later data give low precision under one simple magnitude-blind rule. The result does not distinguish physical size-dependent triggering from selection effects, indirect cascades, or catalog errors. We fit no causal model and make no forecast.

The primary estimate uses only 47 pairs in six years. Dropping reuse loses data and changes the target population. Greedy shortest-gap matching is one rule, not a unique definition of an event pair. First-day exclusion can remove useful pairs and does not prove completeness at later times. Fixed radii can miss large ruptures. Magnitudes mix sources and types; errors near all cutoffs can alter membership. The bootstrap can miss dependence across connected groups, regions and years. Time links outside 30 days can join groups that are treated as independent. Multiple checks give marginal rather than simultaneous coverage. No method here estimates the behavior of all earthquakes.

## Audit and reproduction

[analyze.py](files/analyze.py) checks the input hash and unique source IDs, converts timestamps to explicit elapsed seconds, and asserts that disjoint pairs do not reuse events. It exactly reproduces the earlier all-pair counts (898/1446 and 177/261). A second distance calculation uses the scalar spherical cosine formula. It agrees with Cartesian distances to less than 7e-9 km. A separate reverse-time construction gives exactly the same primary matching set. No candidate time gaps tie in either era, so distance roundoff cannot change a tie decision. [audit.json](files/audit.json) stores these checks and the paired-change intervals. These checks validate the implementation, not the physical explanation.

[REPRODUCE.md](files/REPRODUCE.md) gives commands. [summary.json](files/summary.json) preserves all estimates, intervals, anonymous group counts and omission ranges. It contains no event IDs, coordinates, times or pair lists. [retrieve.py](files/retrieve.py) provides a hash-checked retrieval recipe into external scratch. Exact replication requires the immutable snapshot if the API changes. [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md) credits USGS and contributing networks and explains why external records stay outside this package. The unchanged SCI baseline LICENSE covers our bundled code, text, figure and aggregate statistical results; it does not relicense the source catalog.

Campaign: `11_07_2026`. Job: `sci-1107-dell-earth-and-ocean-sciences-95b179f3a428`. Topic: `earth-and-ocean-sciences`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort, in T3 Code through the Codex harness. The campaign-machine signature is not a personal authorship claim. All computations ran in this worktree. No remote upload or submission was made. No private keys are included.
