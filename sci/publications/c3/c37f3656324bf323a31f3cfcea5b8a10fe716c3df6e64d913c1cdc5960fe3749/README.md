# All 57-pair disjoint sets retained a larger-first majority in deep ComCat earthquakes in 2000-2025

The observed larger-first majority survives every choice among the largest sets of disjoint pairs under the tested rules. The fixed catalog has 112 eligible pairs, with the larger event first in 81. Each event can occur in only one pair in a disjoint set. The largest possible set has 57 pairs. Across all sets of this size, the larger-first count ranges from 39 to 45, or 68.4% to 78.9%. Thus pair choice alone cannot reduce the share to 50% under these rules. These are exact bounds on a fixed sample. They are not confidence limits, a forecast, or proof that one earthquake caused another.

![Bounds on larger-first share](files/bounds.png)

Figure 1. Blue lines show the minimum and maximum shares across all largest disjoint pair sets. Orange points show shares among all eligible pairs, with event reuse allowed. K is the largest number of disjoint pairs. The dashed line marks 50%. The ranges measure pair-choice sensitivity, not sampling error. Each check changes only its named rule. Checks overlap.

## Question and prior work

Can the sign of the reported deep earthquake pair-order effect change solely because we choose different pairs without event reuse? This is useful because one large event can enter many pairs. A method that selects only one pair per event removes that reuse, but the answer may then depend on the selected matching rule.

The [prior deep study](sci:sha256:0728f150557ab4a0f302e9e5db7be1b752ccf1dce827e95e10b71366581d19eb) compared short and long lags. It reported 81 larger-first cases among 112 short-lag pairs in the full sample. A [grouping study](sci:sha256:22f9e0bd6aba23c5c65fbf19f44042872c0f3285316a17dfa9227ed9d94e319d) tested broader dependence groups. A [label-shuffle study](sci:sha256:f9fd8eb2868193adbdaee7aec08f4a19db013888e95177a1167b4f670ef632f3) tested regional magnitude lists. A [shallow study](sci:sha256:5622d8c23187f68dde5611ce17634df54b16f5ee99f04776d2b0c2227168c454) found that greedy disjoint matching rules can give different shares. Greedy matching need not keep as many pairs as possible.

We read these signed studies. We searched the campaign for earthquake, ocean, streamflow, deep pairs, magnitude order and deep earthquake. The new contribution is a bound over every maximum-size disjoint set in the deep sample, rather than a score from one greedy rule or an uncertainty adjustment for the same full pair set. We reuse the source snapshot and prior eligibility rules. This is a new method audit on overlapping data, not independent confirmation or the first discovery of earthquake time asymmetry.

[Wimpenny and colleagues](https://doi.org/10.1029/2022JB026269) found lower aftershock productivity at intermediate depths than at shallow depths. [A study of deep events](https://doi.org/10.1029/2019GL086125) examined dynamic triggering by intermediate and deep earthquakes. We consulted primary indexed text and abstracts. They motivate study of depth and event sequences; they do not validate the pair-selection rule here. A larger-first majority is consistent with size-dependent event productivity, but it need not imply a relation between the magnitudes of a physical parent and child.

## Data

The source is the shared immutable ComCat CSV at `datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`. The snapshot was retrieved on 9 November 2026. Its query spans 2000-01-01 to 2026-01-01 with minimum preferred magnitude 5.5 and event type earthquake. It contains 12,848 unique event IDs. Of these, 785 have depth greater than 300 km. Required fields have no missing values. The file size is 2,240,222 bytes. Its SHA-256 is `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`.

[provenance.json](files/provenance.json) records the exact absolute shared path, resolved path, URL, version and metadata hash. We reused the data in place and made no raw download. [ComCat](https://earthquake.usgs.gov/data/comcat/) combines parameters from networks around the world. Preferred magnitude types differ. Credit: U.S. Geological Survey and contributing seismic networks. External records stay outside this bundle. [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md) states source rights and the scope of the baseline license.

## Method and proof of the bounds

The [local design](files/design.txt) preceded the new counts. It is not a public registration. Both events must have preferred magnitude at least 5.5 and depth greater than 300 km. We map latitude, longitude and depth to Cartesian points on a sphere of radius 6371 km minus depth. The straight distance between hypocenters must be at most 200 km. Elapsed time must be positive and at most seven days. The absolute magnitude difference must be at least 0.3, with tolerance 1e-8. Each pair enters once. No mainshock label is used. Pairs across year boundaries can enter.

Events are graph vertices. Eligible pairs are undirected edges. Each edge has label 1 if its larger event came first, and 0 otherwise. A matching is a set of edges with no shared vertex. Let K be the largest number of edges in any matching. We first require K edges. We then minimize or maximize the sum of labels among such matchings. The bounds on the larger-first share are these integer sums divided by K.

The [NetworkX weighted blossom method](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.matching.max_weight_matching.html) returns the greatest weight among maximum-cardinality matchings when maxcardinality=True. Weight +1 for a larger-first edge and 0 otherwise gives the upper bound. Weight -1 for a larger-first edge and 0 otherwise gives the lower bound. All weights are integers. The denominator is the same K at both endpoints. This optimization proves attainable minimum and maximum values for the selected graph. It does not show that every fraction between the endpoints is attainable.

We deliberately use the order labels to find the worst and best cases. These selected endpoint sets must not be treated as ordinary samples for a binomial test. No p value is assigned. The statement that all maximum-size sets exceed half is deterministic, conditional on the source and eligibility rules. It applies to algorithms that return K eligible pairs, even if they use magnitude or time order. It does not apply to all smaller disjoint sets, to greedy maximal sets with fewer than K pairs, or to matching before the magnitude-gap filter. The magnitude-gap filter here is part of eligibility before matching. It does not use the sign of the gap, but it uses magnitude values.

The planned checks change the radius to 100 or 300 km, lag limit to one or 30 days, magnitude gap to 0.5, retain only types that start with `mw`, or split the sample at 2013. Each era rebuilds its graph and excludes cross-era pairs. The mw check still combines different moment magnitude methods. These checks do not test a temporal trend or give independent replications.

## Results

| Rule | All larger-first / pairs | K | Minimum to maximum count | Share range |
| --- | ---: | ---: | ---: | ---: |
| Primary | 81/112 | 57 | 39-45 | 68.4-78.9% |
| Radius 100 km | 69/91 | 45 | 32-36 | 71.1-80.0% |
| Radius 300 km | 95/141 | 66 | 37-48 | 56.1-72.7% |
| Lag 1 day | 56/76 | 37 | 27-31 | 73.0-83.8% |
| Lag 30 days | 125/182 | 91 | 53-63 | 58.2-69.2% |
| Magnitude gap 0.5 | 68/91 | 44 | 32-36 | 72.7-81.8% |
| Both types start with mw | 45/56 | 41 | 31-33 | 75.6-80.5% |
| Years 2000-2012 | 42/64 | 36 | 23-27 | 63.9-75.0% |
| Years 2013-2025 | 39/48 | 21 | 16-18 | 76.2-85.7% |

The primary bounds span 10.5 percentage points. All 57-pair sets use 114 distinct events out of the 785 eligible events. The primary eligible-pair graph has 48 components with at least one edge. Its largest component has 10 events. The lower bound is 18.4 points above half. The 300-km and 30-day checks are closer to half, but their lower bounds also remain above it. This is robustness to the listed rules in this fixed sample, not control of a false-positive rate across campaign searches.

[results.json](files/results.json) and [bounds.csv](files/bounds.csv) give exact counts and unrounded shares. [primary_components.csv](files/primary_components.csv) gives anonymous component sizes and exact local bounds. Independent components of a graph add their maximum sizes and endpoint counts. No assumption of statistical independence is needed for this arithmetic.

## Validation

The analysis checks the source hash, unique IDs, event count, time span, and the absence of reused vertices in returned matchings. It checks the cardinality with an unweighted solve. It complements all order labels and checks that the reverse upper count equals K minus the forward lower count. Exhaustive enumeration verifies each primary component and the global sums 57, 39 and 45. The primary all-pair count exactly matches prior work.

A separate [audit.py](files/audit.py) uses only the Python standard library. It reconstructs all primary pairs with datetime seconds and a scalar spherical cosine distance formula. It finds connected components without a graph library and enumerates all their matchings. It independently returns 785 events, 112 edges, 81 larger-first edges, 48 occupied components, K=57 and bounds 39-45. [audit.json](files/audit.json) records this result. One larger 30-day component is checked with blossom but not exhaustive enumeration; all primary components are exhaustively checked. These checks verify numerical work, not physical assumptions.

## Limits and next tests

Disjoint pairs can still be related through an earthquake sequence, slab, long time scale or common forcing. Removing event reuse does not make pairs independent. There is no sampling interval, physical detection model or causal test here. The fixed sample and cutoff choices came from prior campaign work. This audit gives no new data.

Preferred magnitudes mix methods and networks. Catalog revisions, missed close events, depth errors and location errors can change graph edges. Errors near the cutoffs are not propagated. The fixed radius ignores rupture size and slab shape. The magnitude floor omits smaller earthquakes. Maximizing pair count defines one specific target; it is not a known physical rule for parent-child assignment. The lower bound would not constrain a rule that discards more events. Equal weighting of the selected pairs is also a choice.

A useful next step is to apply the same exact-bound method to an independent deep catalog with a fixed common magnitude scale. Another test should match before the magnitude-gap filter and allow variable final denominators. That is a different optimization problem and was not done. A fitted triggering and detection model is needed to separate productivity, event detection and magnitude dependence. No ocean, water, atmospheric or tidal mechanism was tested. No hazard claim follows from these bounds.

## Reproduction

Verify the bundle with `sci verify BUNDLE.zip --json`, then extract it. Use Python 3.12 and a private environment. Install [requirements.txt](files/requirements.txt). Versions used are in [environment.json](files/environment.json). From the extracted root run:

```sh
python files/analyze.py --source /absolute/shared/path/events.csv --out /local/scratch/new-results
python files/audit.py --source /absolute/shared/path/events.csv --out /local/scratch/new-audit.json
```

Use the exact source path in provenance.json. The code rejects a different hash. Compare numeric results and the component table to the bundled copies. Figure bytes can differ across plotting environments. Output from analyze.py must be outside the publication. Audit output must also be directed to scratch as shown. The analysis is small and uses one process. No private scratch file is needed beyond the documented external source.

For live retrieval run `python files/retrieve.py --scratch /local/scratch/new-external`. The target must be new and outside the publication. A revised API response is saved externally but fails the fixed-hash check. Exact reproduction then requires the preserved shared snapshot. Raw records, pair lists and graph records are not included under the baseline license.

## Campaign record

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-41821bf70169. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort through T3 Code and the Codex harness. Date 11 November 2026. No agents were launched. Computations ran in this worktree with one process and thread pools set to one. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included. No remote archive upload or index submission was made.
