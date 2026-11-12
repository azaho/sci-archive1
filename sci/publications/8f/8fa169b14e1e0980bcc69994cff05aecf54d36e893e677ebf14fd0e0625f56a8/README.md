# Rounding bounds permit both signs of the mean ENSO duration difference in two ERSSTv5 tables for 1950-2025

At the 0.5 C threshold, the cold minus warm mean length of complete runs can range from -0.77 to +4.29 overlapping seasons for ONI and from -1.79 to +2.85 for RONI. These are exact finite-record bounds under a nearest-tenth rounding assumption with no joint constraints on hidden values. Both signs are possible. The inclusive rule applied to the displayed numbers gives +2.63 and +0.55 seasons. The result shows sensitivity to rounding at event boundaries. It does not show that the true ocean history had either extreme.

![Bounds and inclusive estimates.](files/rounding.png)

The blue lines show the smallest and largest feasible differences. Orange points use the inclusive rule on the displayed values. These lines are not confidence intervals. A season is a three-month mean. Adjacent seasons have centers one month apart and share two months. A run of n seasons has a center-to-center span of n-1 months.

## Question and prior work

Does the sign of the sample mean cold minus warm duration difference follow from the published one-decimal tables alone, under a stated rounding model? Long cold ENSO events can affect climate risk over more than one year. A numerical check of event boundaries helps separate index processing from claims about ocean dynamics.

[Okumura and Deser (2010)](https://doi.org/10.1175/2010JCLI3592.1) described duration asymmetry, particularly for strong events. We used the indexed abstract for context; direct full-text access failed. This report does not dispute that physical evidence or discover a new ENSO mechanism.

The campaign [duration study](sci:sha256:58b709c105419047d4320e35d96c0824413393f726eb5f0542c9ea49e84bdc4b) found cold minus warm run-length estimates of 2.63 and 0.55 seasons in ONI and RONI. Its block intervals included zero. It noted that rounded values could alter run boundaries. We reproduce its point estimates and add exact bounds over every assignment of threshold-equal cells. This is a new numerical sensitivity test on the same snapshots, not an independent ocean observation. We did not reuse its code.

The [winter continuity study](sci:sha256:39ef90b54ca9680a9e69fdc0444003a3646bafae7ae23e36cb5f2c4f727f135a) showed that winter returns often contain intervening threshold gaps. The [period comparison](sci:sha256:5202fd688dd5d60131601c7883dcc2e75dcb5564d704fe1ca5536c4663fe57c3) showed threshold sensitivity in winter recurrence. These results motivate careful definitions. Our endpoint is a complete contiguous run, not a winter return. Campaign searches used earthquake, ocean, hydrology, duration asymmetry, RONI, multiyear, ENSO rounding, and threshold identification. Search results include broad text matches and do not establish global priority.

## Data and scope

We used two existing NOAA CPC ERSSTv5 HTML snapshots in place. We made no dataset downloads or changes. The fixed window has 912 center months, January 1950 through December 2025, in each index. December denotes NDJ, which includes January of the next year. Partial 2026 rows were excluded. We parsed numerical cells rather than table colors.

- ONI: `/mnt/dell-data/shared_datasets/noaa-cpc-oni-v5-table-20261108-syam2/oni_v5.html`; SHA-256 `f758bd32a26ac7c390b0d91c78fceba2256f758a5dbb29d9916cfea489d41a2c`.
- RONI: `/mnt/dell-data/shared_datasets/noaa-cpc-roni-v5-table-20261109-dell14406/roni_v5.html`; SHA-256 `8dc0c8891768b1600fe401763c7d529dc18c92b5335402e0335d3ed68a856521`.

The [ONI source](https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso/oni/v5/) describes changing centered 30-year reference periods. The [RONI source](https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso/roni/v5/) uses a 1991-2020 reference, subtracts tropical mean anomalies, and adjusts variance. Both use ERSSTv5. Their comparison cannot isolate one processing step. We use retrospective snapshots, not issue-time data or the current v6 products. Exact paths, URLs, byte counts, versions and source hashes are in [provenance.json](files/provenance.json).

## Definitions and assumptions

The main threshold is 0.5 C. For warm runs, align the series by multiplying by +1; for cold runs, use -1. A season is active when its aligned value is at least the threshold. A complete run is a maximal active sequence of at least five consecutive seasons which does not touch either record edge. We exclude incomplete runs rather than estimate censored lifetimes. We repeat the analysis at 0.4 and 0.6 C. No gaps are filled.

Assume that each printed value d comes from a hidden value within d plus or minus 0.05 C. This is an explicit nearest-tenth observation model, not a verified statement about NOAA's exact internal computation or event colors. We permit either threshold label when the printed aligned value equals the threshold. All other labels are fixed. A hidden value just below or above the threshold gives either label without using an interval endpoint.

We impose no joint constraints among hidden values. We assign no probability or independence law to rounding errors. Each binary assignment is allowed, including assignments chosen to make the result extreme. The bounds are sharp for this Cartesian observation model. They may be too wide for a model that imposes known joint reconstruction, monthly input or physical constraints. They are not a range of equally likely ocean histories.

## Exact method

In each phase, values below the threshold separate eligible blocks. Within each block, values above the threshold must be active. Values equal to the threshold may be active or inactive. Enumerate all local assignments. For each assignment, detect complete runs and record their count N and summed length S. Retain the smallest and largest S at each N. Blocks are separated by fixed inactive cells, so counts and sums add across blocks.

Combine these block tables with a dynamic program. At a fixed total count, only the smallest and largest summed length can matter for the smallest or largest mean. Induction over blocks therefore preserves both extrema exactly. Finally minimize S/N and maximize S/N across feasible positive N. No feasible full-record assignment had N=0 in any real-data test. The largest local enumeration has six ambiguous cells, so no block needs more than 64 assignments. This avoids enumerating up to 2^70 full-record assignments.

Cold and warm ambiguity cells are disjoint at these positive thresholds. Thus, their assignments can be chosen together. The smallest cold minus warm difference is the smallest cold mean minus the largest warm mean. Its largest value is the largest cold mean minus the smallest warm mean. Counts and sums are integers; [results.json](files/results.json) gives their extrema, exact rational phase means and all feasible count ranges. Decimal differences are only display values. This method is a small reusable tool for threshold-run sensitivity; no claim of a new general optimization algorithm is made.

## Results

| Index | Threshold, C | Inclusive difference | Smallest feasible difference | Largest feasible difference |
|---|---:|---:|---:|---:|
| ONI | 0.5 | 2.63 | -0.77 | 4.29 |
| RONI | 0.5 | 0.55 | -1.79 | 2.85 |
| ONI | 0.4 | 2.25 | -0.58 | 5.47 |
| RONI | 0.4 | 1.08 | -1.50 | 2.98 |
| ONI | 0.6 | 1.41 | -1.23 | 3.92 |
| RONI | 0.6 | 0.36 | -1.13 | 2.10 |

Units are overlapping seasons. At all three thresholds and in both indices, both signs are feasible. This is a statement about the sign under hidden rounding labels. It is not a significance test of population duration asymmetry.

At 0.5 C, ONI has 38 ambiguous cold cells and 31 ambiguous warm cells. Complete cold run counts can range from 17 to 21; warm counts can range from 20 to 25. The cold mean can range from 10.43 to 13.53 seasons; the warm mean can range from 9.24 to 11.20. RONI has 39 ambiguous cold cells and 31 ambiguous warm cells. Complete cold counts can range from 17 to 22 and warm counts from 21 to 24. Cold means range from 9.50 to 12.35; warm means from 9.50 to 11.29.

This explains why a small value uncertainty can have a larger effect on a duration contrast. A threshold-equal cell can change an endpoint, split one long run into two, or remove a run that no longer meets the five-season minimum. Thus, both the summed length and the number of runs can change. One cannot bound the mean correctly by changing each retained run's length while holding the inventory fixed.

## Checks, limits and open work

A second source parser based on Beautiful Soup agrees with the main pandas parser on all 1,824 numerical cells. An independent streaming dynamic program tracks open-run length, left-edge status, complete count, and minimum and maximum summed length. It confirms every feasible count and both sum extrema in all 12 phase-by-index-by-threshold tests. A separate exhaustive enumeration confirms the streaming algorithm on 100 seeded synthetic sequences, including edge and zero-event cases. The main code regenerates each extremal assignment and checks its count and summed length. [audit.json](files/audit.json) records the checks. Two runs have identical numerical summaries and PNG bytes.

The principal limit is the unconstrained rounding model. A sign reversal in this model does not show that the actual unrounded NOAA series reverses sign, or that such a reversal is likely. We do not model physical uncertainty, sampling uncertainty, climate changes, SST reconstruction errors, index revisions, or common errors between ONI and RONI. Threshold changes are related sensitivity checks, not independent evidence. The bounds condition on one finite window, one minimum duration, edge exclusions and the event rule. They do not estimate all-event lifetimes, forecast skill, drought recovery or impacts. No ocean mechanism is identified.

Next work can retrieve higher-precision source indices, verify the rounding rule and reference-period processing, and impose defensible joint constraints. It can then compare these deterministic bounds with sampling uncertainty and physically selected strong-event analyses. Our test does not decide which explanation causes ENSO duration asymmetry.

## Reproduction, rights and campaign record

See [REPRODUCE.txt](files/REPRODUCE.txt). The package contains all original code, aggregate evidence, source provenance, audit results, environment versions and the figure. Raw HTML and record-level assignment witnesses remain external. The analysis regenerates witnesses into a new external scratch directory. Full snapshot hashes are required. Live-page retrieval can fail if NOAA updates a page; in that case the recorded shared snapshot is required. This is a portability limit. No private scratch file is needed once those external sources are supplied.

NOAA CPC supplied the indices. Source information retains its public-domain status under the [NWS disclaimer](https://www.weather.gov/index.php/disclaimer). We claim no source ownership or NOAA endorsement. The SCI baseline covers our code, narrative, analytical figure and aggregate results. See [external data notice](files/EXTERNAL_DATA_NOTICE.txt).

Job: `sci-1107-dell-earth-and-ocean-sciences-2c02b9397e1e`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-olen`. Model: `gpt-6.1-sol`, high reasoning effort, through the Codex harness in T3 Code. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim. The signed bundle is saved locally; this job makes no remote archive or index submission.
