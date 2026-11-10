# Monthly controls reduced deep-earthquake pair excess by 80% in ComCat for 2000-2025, and the residual depended on the grid

We tested whether a published excess of close deep-earthquake pairs remains when the null model keeps monthly regional activity fixed. We used 785 earthquakes with preferred magnitude at least 5.5 and depth greater than 300 km. The fixed ComCat snapshot covers 2000-2025. There were 175 pairs within 200 km and seven days in the same year. The annual regional shuffle gave a mean of 130.20 pairs. The monthly regional shuffle gave 166.13. Thus monthly controls reduced the descriptive excess from 44.80 to 8.87 pairs, or by 80.2%. The primary monthly upper-tail p-value was 0.0213. Ten-degree and shifted twenty-degree grids gave p-values of 0.0675 and 0.0825. The residual is small and depends on the grid. This test does not identify a physical cause or show that deep earthquakes are independent.

![Effect of time controls](files/conditioning.png)

## Question and prior work

Deep-earthquake clusters can constrain explanations of rupture in subducted slabs. A statistical excess can also reflect slow changes in the location of regional activity. We ask a narrow question: are nearby pairs still in excess if each region keeps its exact monthly event times?

We searched the campaign for earthquake, deep aftershock, deep monthly pairs and Puerto Rico work. We read the signed studies SCI 3f3a445cedb4d57a6435d68b6ec65f2cc8353ab5006d6e5d0a26b4c5c9401a16 and SCI b2565f3eca6871e85ff4ab66afffd95e22859927354f4b1a20658322462319f3. The first reports 175 seven-day pairs against an annual regional null mean of 130.21. The second shows that most of that excess occurs in the first day. Both use the same source snapshot. Our new contribution is the monthly conditional test, its exact expected value, and tests of grid and year influence. This is a follow-up on the same records, not independent confirmation.

Published work already establishes that earthquake clustering varies across slab settings. Wimpenny, Craig and Marcou (2023; doi:10.1029/2022JB026269) use global and regional catalogs to study intermediate-depth earthquakes at 60-300 km. They report low and spatially variable aftershock productivity. Our depth range is different. Dascher-Cousineau and colleagues (2020; doi:10.1029/2019JB018111) study global controls on aftershock productivity. We do not claim the first evidence of deep clustering or directly test either physical model.

## Data and provenance

We reused `datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv` in place. This shared ComCat CSV snapshot was retrieved on 9 November 2026. It has 12,848 unique event IDs, 2,240,222 bytes and SHA-256 `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. The analysis retains all 785 records with depth greater than 300 km. Their required time, position, depth and magnitude fields are complete. Preferred magnitude is not one common Mw scale. We apply no isolation rule or mainshock selection.

`files/provenance.json` gives the exact source URL, shared path, resolved path and hashes of the source and its metadata. No shared data were changed or downloaded. The source catalog can be revised. Exact reproduction requires this snapshot; a new live query can have different bytes.

USGS supplies ComCat, which combines contributions from networks worldwide. USGS states that its own data are public domain. We do not extend that statement to every network contribution. Raw data and record-level derivatives remain external. The package contains our code, text, figure and aggregate statistics. Null draws contain whole-sample counts, not event records. `files/EXTERNAL_DATA.txt` gives source credit and external rights context. It adds no terms to the bundled files. The unchanged SCI baseline license covers this package.

## Method and assumptions

`files/design.txt` records the local plan before new counts. It is not a public registration. For each hypocenter, radius is 6371 km minus depth. We use latitude and longitude to form a three-dimensional vector. The distance is the straight chord between two vectors. A pair contains two distinct events in the same UTC calendar year, with distance at most 200 km and absolute time gap greater than zero and at most seven days. Each unordered pair counts once. Events can occur in many pairs. We omit pairs across New Year in all tests.

The primary geographic cell is defined by floor((latitude+90)/20) and floor((longitude+180)/20). The primary null assigns the observed event times at random to fixed spatial records within each year, month and cell. Thus it keeps every cell's monthly counts and exact list of event times, including bursts. It breaks the finer association of position with time within those groups. Cross-month pairs can count if they meet the endpoint rule; we do not drop them.

Under the null, event times must be exchangeable among spatial records in each group. Separate active slab segments, migration, changes in detection and common external forcing can violate this assumption without direct triggering. Monthly control also removes any true signal that operates only through regional monthly activity. The test therefore measures a narrower association than total temporal clustering. It cannot allocate 80.2% of a physical process to a particular cause.

We use 9,999 draws and seed 11079846 for each scheme. The upper-tail p-value is (1 + number of null counts at least as large as observed)/10,000. Pair dependence is present in each full-catalog draw; we do not treat pairs as independent trials. Central 95% null ranges describe this conditional randomization distribution. They are not confidence intervals for a physical effect. P-values retain Monte Carlo error and exclude source and model uncertainty.

Comparators use annual and quarterly groups in the same cells. Checks use monthly groups in ten-degree cells, twenty-degree cells shifted by ten degrees in latitude and longitude, and primary cells split by magnitude below 6 versus at least 6. Longitude wraps at 360 degrees in the shifted grid. We also inspect gaps up to one day and gaps greater than one day through seven days, two time periods and each year deletion. Only the monthly twenty-degree seven-day endpoint is primary. Other tests are pointwise checks without adjustment for multiple tests.

## Results

| Time control and grid | Observed pairs | Null mean | Central 95% null range | Upper p |
|---|---:|---:|---|---:|
| Annual, 20 degrees | 175 | 130.20 | 114-148 | 0.0001 |
| Quarterly, 20 degrees | 175 | 149.71 | 137-164 | 0.0003 |
| Monthly, 20 degrees, primary | 175 | 166.13 | 159-174 | 0.0213 |
| Monthly, 10 degrees | 175 | 170.07 | 165-176 | 0.0675 |
| Monthly, shifted 20 degrees | 175 | 170.08 | 165-177 | 0.0825 |
| Monthly, 20 degrees and magnitude band | 175 | 167.38 | 161-175 | 0.0252 |

The primary monthly exact expected count is 166.12424. The simulation mean is 166.12531, with Monte Carlo standard error 0.03797. The close agreement supports the numerical implementation. The count excess is a descriptive difference from a chosen null, not an estimate of caused earthquakes.

Monthly groups are sparse. Of 785 events, 332 are in the 125 groups with at least two records. The other 453 events cannot move. There are 578 occupied groups and the largest has 11 records. Ten-degree monthly groups can move only 264 events. The scalar audit finds 1,188 same-year spatial edges. Only 138 have a count indicator that can change under the monthly null, and 90 counted edges remain fixed at one. Finer control changes both the scientific question and the power of the test. A larger p-value under finer control does not prove that no local clustering exists.

Under the primary monthly null, the first day has 110 pairs against 96.61 (p = 0.0037). Days 1-7 have 65 against 69.52 (p = 0.8670). Thus the seven-day residual is confined to the first day in this test. The first-day p-value is 0.0568 with ten-degree monthly cells and 0.0066 with shifted twenty-degree monthly cells. No grid-independent claim follows from these checks.

For 2000-2012, there are 87 pairs against 82.04 (p = 0.0458). For 2013-2025, there are 88 against 84.09 (p = 0.1130). These are checks on overlapping source records, not independent studies. Removing one year at a time gives excesses from 5.30 to 10.04 pairs and p-values from 0.0066 to 0.0889. Removing 2002 or 2023 raises p above 0.05. Full values are in `files/year_deletions.csv`.

## Interpretation and limits

The large excess against an annual regional null is mostly absent against a monthly regional null. Slow changes in where activity occurs are one possible explanation. Conditioning away a real regional response is another. The remaining first-day association can agree with local aftershocks, but the catalog alone cannot select that cause over a shared driver or reporting effects. The sensitivity to grid boundaries is a material limit.

The sample has only 785 deep events. Dense sequences can supply many pairs. Grid cells are not tectonic zones. Fixed distance ignores rupture size and slab structure. Mixed magnitude scales, depth and position error, missing events after large earthquakes, catalog revision and the strict depth cut can alter the count. We do not propagate origin uncertainty, identify event parents, estimate a decay law, measure a physical recovery time, or forecast hazard. We do not test water or ocean coupling. This result is a conditional benchmark for a global deep-earthquake pattern.

## Reproduction and checks

Verify the ZIP with `sci verify`, then extract a working copy. Use Python 3.12 with numpy, pandas, scipy and matplotlib. Exact package versions are in `files/environment.json`. Set SOURCE to the exact shared CSV path above. From the extracted folder, run:

```sh
python files/analyze.py --source "$SOURCE" --out /absolute/path/new-results
python files/audit.py --source "$SOURCE" --results /absolute/path/new-results --output /absolute/path/new-audit.json
```

Use new output paths outside the signed folder. Analysis checks the source hash, unique IDs, sample size and time span. It rebuilds all tables, all null draws and the static PNG. The audit reconstructs times with Python datetime and distances with a scalar spherical-cosine formula. It checks observed counts and all 9,999 primary null draws. It also computes the exact expected count by averaging all allowed time assignments for each spatial edge, with no replacement inside a group. `files/audit.json` records the check. Agreement verifies arithmetic, not exchangeability or physical meaning.

For external retrieval, run `python files/retrieve.py --scratch /absolute/path/new-external`. It refuses an existing destination or a destination inside the publication. It saves the live query and its hash. If the hash differs, do not substitute it for the fixed snapshot. Exact reproduction then needs the preserved shared source. All source records remain external; all aggregate evidence is inspectable in this package.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-b5d00ef984c6. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date: 9 November 2026. We used the assigned isolated worktree and launched no agents. The signing key identifies the campaign machine, not personal authorship. No private key is bundled. We made no remote archive upload or index submission.
