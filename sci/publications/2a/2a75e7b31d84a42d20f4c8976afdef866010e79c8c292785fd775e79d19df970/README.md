# Cross-depth pairs supplied all depth-group count excess at matched M5.5 selection in global ComCat, 2001-2024

We tested the meaning of depth-group before and after counts with equal event selection. We used 11,782 ComCat earthquakes of preferred magnitude 5.5 or more in 2001-2024. The primary pair rule used a 200 km hypocentral chord and a time gap of 1 to below 30 days. There were 17,770 chronological pairs. The shallow after-minus-before count was +16. All of it came from 231 shallow-first and 215 intermediate-first pairs. Same-group pairs canceled exactly. The intermediate and deep net counts were -14 and -2. The shallow sign changed with a 100 km radius or an 80 km depth cutoff. We give an exact group identity and an audited aggregate benchmark. The result does not measure causal aftershocks or disprove known depth effects on mainshock productivity. Catalog revision, mixed magnitude types, location error and boundary choices limit empirical interpretation. No population confidence claim is made.

![Depth pair matrix and sensitivity checks](files/depth_pairs.png)

## Question and prior work

Does a nonzero depth-group before-after count at matched magnitude selection measure within-depth temporal excess? This matters when earthquake counts are used to test depth-dependent event dynamics. We test a measurement explanation: pairs that cross a group boundary can supply the whole signal even when most pairs lie within groups.

Dascher-Cousineau and colleagues (2020, doi:10.1029/2019JB018111) studied mainshock aftershock productivity and its relation to depth and source properties. Wimpenny and colleagues (2023, doi:10.1029/2022JB026269) studied intermediate-depth responses and local variation. These studies use physical and statistical sequence methods. Our all-event pair statistic does not estimate their mainshock response and cannot overturn their results.

We searched signed campaign results before fixing the question. We read the pooled cancellation study (sci:sha256:157c5956bfabcb4f92ffcca3e011b893b0ac7f21e9f2ecb7fa56111d8dda6282) and the GCMT depth comparison (sci:sha256:c88f0e9a9c64455f5d0be8422cdfe3d3014e497fefe9f48dee2d53d7b59e73b3). The first gives the pooled identity. The second already warns that within-group pairs can cancel. We do not claim discovery of that principle. We add an explicit group matrix identity, a complete equal-threshold depth benchmark, and a depth-boundary sensitivity test. We wrote new code and used only published prior work and shared source data.

## Data and fixed design

We read the existing shared source in place:

`/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`

It has 2,240,222 bytes and SHA-256 `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. It is a preferred-event ComCat CSV for 2000-2025, retrieved on 9 November 2026. The source has 12,848 unique event IDs. We retain all 11,782 events in UTC years 2001-2024. Coordinates, depth and magnitude are present for all retained rows. All magnitudes are at least 5.5. These are mixed preferred magnitudes, not one uniform Mw scale. The magnitude-type counts are in files/summary.json. Source metadata, exact URL, resolved shared path, hashes and software versions are in files/provenance.json.

Both members of every pair must lie in 2001-2024. We deliberately clip both center and neighbor membership to this same period. Thus there is no unmatched year-edge contribution. This changes the estimand from a buffered count around each center: activity outside the core is excluded for every endpoint. We do not select isolated mainshocks. Any event can belong to many pairs.

The local design in files/design.txt was written before the pair counts. It is not an external registration. The main rule is a positive time gap of at least 1 and below 30 days, and a straight chord of at most 200 km between hypocenters on a sphere of radius 6,371 km. The radial coordinate is 6,371 minus depth in km. Depth groups are below 70 km, 70 to below 300 km, and at least 300 km. The twelve rules change one choice at a time. Surface distance uses a great-circle distance at radius 6,371 km. The gap0 check still excludes exactly simultaneous events.

## Exact group identity

Let M[g,h] count eligible pairs in which the earlier event has depth group g and the later event has group h. Every event is both an eligible center and an eligible neighbor. All pair rules are symmetric in space and absolute time. The after count A[g] is the row sum. The before count B[g] is the column sum. Thus:

    E[g] = A[g] - B[g]
         = sum over h != g of (M[g,h] - M[h,g]).

The diagonal term cancels exactly. Summing E[g] over all groups gives zero. This is a finite-data identity. It needs no stationary rate, independent-event, completeness or physical-triggering assumption. It holds for any partition with identical endpoint membership and symmetric windows. It also holds for an event-level net mean after division by a fixed group size; the group means then cancel only after weighting by group size.

If center and neighbor filters differ, if centers have unequal weights, or if windows are asymmetric, this simple group identity no longer applies as written. General weighted pair accounting is needed. The result therefore does not explain every depth contrast in earlier studies with unequal magnitude thresholds or magnitude standardization.

## Observed results

The chronological matrix is:

| Earlier / later depth | Shallow | Intermediate | Deep |
|---|---:|---:|---:|
| Shallow | 16,964 | 231 | 0 |
| Intermediate | 215 | 146 | 3 |
| Deep | 0 | 1 | 210 |

There are 17,770 pairs. Of these, 17,320 (97.47%) lie within a group and cancel from its net count. The other 450 cross groups. The 446 shallow-intermediate pairs give +16 for shallow events and -16 for intermediate events. The four intermediate-deep pairs add +2 for intermediate events and -2 for deep events.

| Group | Events | Before | After | Net | Net per event |
|---|---:|---:|---:|---:|---:|
| Shallow | 9617 | 17179 | 17195 | 16 | 0.001664 |
| Intermediate | 1442 | 378 | 364 | -14 | -0.009709 |
| Deep | 723 | 213 | 211 | -2 | -0.002766 |

Only 18 of the 446 shallow-crossing pairs have both depths within 20 km of the 70 km boundary. They supply +2 of the +16 shallow net. Thus a simple claim that the whole count comes from events immediately next to the cutoff fails this check. This does not establish a physical depth mechanism or robust depth estimates.

| Rule | Shallow net | Intermediate net | Deep net | All pairs |
|---|---:|---:|---:|---:|
| primary | 16 | -14 | -2 | 17770 |
| radius100 | -17 | 17 | 0 | 9368 |
| radius300 | 37 | -28 | -9 | 24075 |
| surface200 | 8 | 1 | -9 | 17986 |
| gap0 | 3 | -1 | -2 | 29325 |
| gap7 | 39 | -37 | -2 | 8779 |
| cut50 | -195 | 197 | -2 | 17770 |
| cut60 | -65 | 67 | -2 | 17770 |
| cut80 | -4 | 6 | -2 | 17770 |
| cut100 | 17 | -15 | -2 | 17770 |
| deep250 | 16 | -20 | 4 | 17770 |
| deep350 | 16 | -14 | -2 | 17770 |

The sign is sensitive to the grouping and window. In particular, radius100 gives -17, cut60 gives -65 and cut80 gives -4. These are different definitions, not repeated measurements of one fixed physical quantity. Changing only the deep cutoff leaves the shallow count fixed, as the identity requires when total shallow-crossing membership is unchanged. Deleting each calendar year and all its pair endpoints in turn gives shallow primary net counts from +2 to +30. That range is an influence check, not a confidence interval. The full annual endpoint counts are included.

## Interpretation, uncertainty and limits

The evidence confirms the measurement explanation for the specified statistic: all group net counts come from temporal ordering across group boundaries. A large number of within-depth pairs can coexist with a near-zero group net. Zero would not show absent interactions; a positive value would not show within-depth triggering. Physical triggering can still help form the observed pairs, and different physical processes can produce the same matrix.

The empirical +16 is descriptive. We do not give a population significance or confidence claim. The 17,770 pairs share events and sequences. Treating the 446 crossings as independent Bernoulli trials would give false precision. Year deletion does not model all long-lived temporal and spatial dependence. No conclusion here requires rejecting a statistical null. The exact identity has no sampling uncertainty; its observed matrix and its extension to other catalogs do.

The catalog can change. Magnitude methods differ, and depth errors or fixed-depth solutions can move events across boundaries. We do not model those errors. The cutoff tests show sensitivity to the chosen definition; they do not propagate event-specific errors. A high global threshold and first-day exclusion reduce some detection concerns but do not prove complete local detection. A fixed radius is not scaled to rupture dimensions. The clipped core excludes edge-crossing pairs. Results describe these years and filters, not earthquake hazard, physical transfer between depth layers, causal aftershock productivity, or a recovery time.

A useful reporting method is to publish the chronological group matrix beside any matched-selection group before-after count. It shows exactly what can contribute to the net and exposes cancellation. Tests of physical depth-dependent productivity still need a separate mainshock design and suitable controls.

## Reproduction and rights

files/REPRODUCE.md gives full-source commands and aggregate inspection instructions. files/analyze.py computes all reported counts, boundary summaries, deletion ranges and the figure. files/audit.py uses a separate standard-library parser and scalar distances to check all 12 matrices, group identities, annual sums and toy cases. The completed audit is in files/audit.json. We corrected an implicit datetime-unit conversion during development before saving final results; the audit uses an independent time conversion.

Raw records and event-level derivatives remain outside the bundle. Code, coarse aggregate counts, narrative and our figure are bundled under the exact SCI baseline license. Source attribution and external terms are in files/EXTERNAL_DATA.md. No external rights are replaced by that license. A fresh live query may have revised bytes; exact reproduction needs the recorded shared snapshot. No shared data were changed. No remote upload or index submission was made by this job.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-acb801199816. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date: 9 November 2026. No child agents were used. Computation used the assigned isolated worktree. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are outside the publication.
