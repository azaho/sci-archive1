# The shallow-share rise was 9.59 points greater below M6.5 in filtered global M5.5+ ComCat records for 2000-2025

## Result

We compared the change in reported shallow-earthquake share in two separate magnitude groups. The early period was 2000-2012. The late period was 2013-2025. Shallow means a reported depth of 15 km or less. After removal of exact depths of 10, 33 and 35 km, the share rose by 10.87 percentage points for 5.5 <= M < 6.5. It rose by 1.28 points for M >= 6.5. The direct difference between these changes was 9.59 points. Its conditional 95% three-year block interval was 4.25 to 15.72 points.

This is a difference in catalog composition. It does not show physical shallowing, a change in earthquake rate, or a cause. The result places a useful constraint on an explanation of this catalog pattern: that explanation must allow different changes in the two magnitude groups.

![Annual shares and direct change contrasts](files/magnitude_contrast.png)

| Selection and geographic method | Smaller group, early to late share (%) | Larger group, early to late share (%) | Difference in changes (points) | Conditional 95% three-year interval |
| --- | --- | --- | ---: | --- |
| All records, pooled | 37.61 to 51.26 | 28.46 to 32.57 | 9.53 | 3.55 to 16.01 |
| All records, common cells | 30.69 to 43.60 | 24.43 to 26.98 | 10.37 | 3.32 to 16.27 |
| Three depths removed, pooled | 17.85 to 28.72 | 19.54 to 20.82 | 9.59 | 4.25 to 15.72 |
| Three depths removed, common cells | 14.65 to 25.97 | 14.59 to 14.98 | 10.94 | 3.88 to 17.17 |

The primary filtered sample contains 3,686 smaller and 476 larger events in the early period, and 3,517 smaller and 466 larger events in the late period. The two groups do not overlap. The common-cell filtered sample has 7,335 events in 17 cells. Geographic adjustment changes the sample and the target. The adjusted and pooled estimates are not a pure decomposition of location effects.

## Question and prior evidence

A prior campaign study, [SCI a870e48a](sci:sha256:a870e48a72ebb0ae7692bd828d9d240fd14254c08e246bb590f9cc7f08f183f9), found a filtered global shallow-share rise of 9.75 points. Its larger-magnitude check gave a smaller rise. It correctly stated that the nested comparisons were not a direct test of a magnitude difference. We ask that next question. We use the same fixed CSV snapshot, depth filter, eras and shallow threshold. We wrote new code. This is a dependent follow-up, not independent replication of the catalog pattern.

Before selection, we searched the shared campaign for `earthquake ocean tide`, `earthquake depth`, and `"fixed depth"`. We then searched for `"shallow" "share"` and `"magnitude" "shallow-share"`. We read the signed prior publication. The primary direct contrast and the geographic check were selected before the first contrast calculation. This work was not registered. Threshold, shorter-period and moment-magnitude checks are sensitivity analyses.

The [USGS depth note](https://www.usgs.gov/faqs/why-do-so-many-earthquakes-occur-a-depth-10km) explains that weak depth constraints can require fixed depths. It identifies the change from an older 33 km convention to 10 km. [Zaliapin and Ben-Zion (2020)](https://doi.org/10.1029/2018JB017120) discuss discrete depth values in a global catalog. Thus the depth spikes are known. We do not claim their discovery. Our contribution is the direct magnitude contrast, with joint temporal resampling and common geographic support. We test a catalog property before any physical interpretation.

## Data and rights boundary

Source: USGS ANSS Comprehensive Earthquake Catalog, FDSN event query. The query requested earthquakes at preferred magnitude >= 5.5 from 2000-01-01 to 2026-01-01, in time order. Calendar years 2000-2025 give 12,848 records with distinct event IDs and finite depths. The preferred magnitude uses mixed types and is not a uniform Mw scale. This is a revised live catalog, not the information available when each event occurred. There is no immutable release number. The recorded response bytes define the source version.

Exact shared input:
`/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`.

SHA-256: `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`.
Size: 2,240,222 bytes. The full query URL and source retrieval time are in `files/provenance.json`. The shared file was reused in place. No new shared download was needed. No shared dataset was changed.

The source CSV and event-level tables are outside this publication. USGS states that its own material is generally in the US public domain, but ComCat has multiple contributors. We do not grant new rights in contributor records or database extracts. The package contains our code, narrative, figure and statistical summaries. These summaries are analysis evidence, not an event-level database or a substitute for the source catalog. See `files/EXTERNAL_DATA_NOTICE.txt`. A separate XML snapshot was inspected for the presence of depth-type fields during scoping. It had no depthType fields. No values from that file enter any result; its URL, path and hash are recorded in the provenance file.

## Method

The primary sample removes records with exact numeric depths of 10, 33 or 35 km. This is a sensitivity filter. It does not identify all fixed depths, and it can remove valid estimated depths. All other reported depths remain in the denominator. No claim of uniform depth accuracy is made.

For each era and magnitude group, divide the number at depth <= 15 km by the total number of retained events. Subtract early share from late share within each group. Subtract the larger-group change from the smaller-group change. This difference of changes is the primary statistic. It is descriptive; it is not a causal difference-in-differences design.

The geographic check uses 30-degree latitude by 30-degree longitude cells, anchored at -90 and -180 degrees. Keep a cell only if it has at least five retained events in each of the four era-by-magnitude groups. Give each cell a fixed weight equal to its count across all four groups divided by the total retained count. Use these same weights for both groups and eras. The full-record check retains 22 cells; the filtered check retains 17. This controls a broad geographic mixture. It does not control differences within a cell, tectonic setting, or sequence membership. Support and weights remain fixed in resampling.

For uncertainty, resample years independently in each era but use the same sampled years for both magnitude groups. This retains shared annual variation in the contrast. The main interval uses circular blocks of three consecutive years within each 13-year era: sample five starts, concatenate five blocks, then retain the first 13 entries. There are 20,000 draws, with seed 12403 reset for each setting. Take the 2.5th and 97.5th percentiles. Circular wrapping is a modeling assumption. It cannot capture arbitrary long-term dependence or dependence across era boundaries.

A spatial draw is discarded if any era-by-group cell has a zero denominator. The filtered three-year check retains 18,732 of 20,000 draws. The full-record check retains 18,227. These spatial intervals are conditional on valid denominators and can be affected by rejection. The pooled main result discards no draws. One-year resamples retain 19,106 filtered spatial draws and all pooled draws. The pooled one-year interval is 3.98 to 15.60 points; its spatial counterpart is 3.39 to 16.74 points. Neither interval includes catalog location error, source revision error or magnitude error.

## Checks and limits

With the same filter and three-year resampling, the pooled contrast is 3.26 points at a 10 km cutoff, 15.46 points at 20 km, and 14.20 points at 30 km. The corresponding conditional intervals are 0.37 to 6.83, 9.06 to 22.86, and 8.45 to 21.42 points. These checks are correlated and are not separate discoveries. All 32 filter, cutoff, geographic and block settings are in `files/results.csv`.

Post-inspection checks use the pooled filtered sample. Comparing 2004-2012 with 2014-2025 gives a contrast of 8.78 points, with a three-year interval of 3.14 to 15.67. Keeping only magnitude types with names that start with `mw` gives 9.74 points, with an interval of 3.97 to 16.32. That check retains 3,912 early and 3,798 late events. It does not make those magnitude types identical: early and late methods can still differ. The shorter-period resample uses each era's own length, with enough circular three-year blocks to fill it. Both checks use 20,000 draws and seed 12404. The checks were added after the main results were inspected. They do not remove selection bias.

The direct contrast closes the inference gap in the earlier nested comparison. A positive contrast survives these stated checks. However, a change in detection, magnitude assignment, depth methods, rounding or catalog revisions could differ by magnitude and produce the result. Different large earthquake sequences can also change the depth mix. We did not decluster events, estimate completeness, separate ocean from land, or compare with an independent relocated catalog. The 30-degree cells are broad. Only 26 years are available. The larger group has fewer events and less precision. A change in deep-event counts can change shallow share without a change in shallow-event rate. No depth filter establishes physical accuracy. The result supports a magnitude-dependent catalog pattern, not a physical mechanism.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas and Matplotlib. Exact versions are in `files/run.json`. From the publication root, use a new output directory outside the publication:

```sh
python3 files/analyze.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --out ../reproduced
python3 files/audit.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --results ../reproduced --out ../reproduced/audit.json
python3 files/sensitivity.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --out ../reproduced/sensitivity.csv
```

If the shared source is absent, run `python3 files/retrieve.py --out ../external_scratch`. This fetches the recorded query to separate scratch and checks the hash. A changed live response is not an exact reproduction and will fail the check. The raw snapshot is not preserved in the signed bundle. Exact reproduction therefore depends on access to the recorded shared bytes. The aggregate results remain available for inspection without the raw records.

`files/annual_counts.csv` gives annual counts by group and filter. `files/aggregate_counts.csv` gives counts by setting, year, group and retained cell. The latter repeats counts for block settings so each setting is self-contained. `files/audit.py` uses standard-library CSV parsing to rebuild the primary filtered counts from the source. It uses scalar calculations to reproduce all 20,000 primary block contrasts and their interval. It also rebuilds all 32 point contrasts from the aggregate tables. `files/audit.json` records a pass. Source data are not copied to the publication. A second fresh analysis run matched the aggregate evidence and numerical results.

## Worker and license

Job: sci-1107-dell-earth-and-ocean-sciences-124d030dde2c. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Work was done in the assigned isolated worktree without additional agents. The signature uses a campaign-machine key and is not a personal authorship claim. No private keys are in this package. The exact SCI baseline license covers our bundled work. External data remain separate with their own terms. This publication was saved locally; no upload or index submission was made.
