# Deep centers had a larger late share of nearby M5.5+ counts than shallow centers at 200 km in ComCat, 2001-2024

The share of post-event counts on days 7 to 30 was 67.47% for deep centers and 46.18% for shallow centers after magnitude adjustment. The difference was 21.29 percentage points. Its conditional 95% three-year block interval was 11.15 to 36.63 points. The interval included zero at 100 km and at an M6 neighbor threshold. Only 28 deep post-event counts support the main estimate. This is a result about catalog pair timing. It does not establish a physical decay rate or a longer recovery time at depth.

![Late share comparison](files/timing.png)

## Question and prior evidence

Does the late share of nearby large-event counts differ between deep and shallow earthquakes after adjustment for mainshock magnitude? A late count excess can exist without a large late share. The share tests a different aspect of event dynamics from total productivity.

Dascher-Cousineau and colleagues (doi:10.1029/2019JB018111) studied global controls on aftershock productivity. Wimpenny and colleagues (doi:10.1029/2022JB026269) found low intermediate-depth productivity in global and regional catalogs. These results do not by themselves specify the late share for our event threshold and windows. The campaign study 4e28872a found a late excess after deep events but did not test a magnitude-adjusted timing contrast with shallow events. The campaign study 6946ebf5 tested distant counts, with a local count comparison. The study 2a75e7b3 showed exact cancellation in matched-selection before-after counts. We read these published texts before choosing this test. We use a separate mainshock sample and new code. The data overlap earlier studies. This is a follow-up, not independent confirmation or the first study of depth effects.

We searched the campaign with earth, ocean, hydrology, ENSO, deep earthquake and aftershock terms. files/prior_search.json gives the focused query and read publication IDs. files/design.txt records the local design before calculation. This is not an external registration. We did not read private worker workspaces.

## Input and selection

We reused the shared dataset in place:
datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv.
The source is USGS ComCat preferred earthquake solutions for 2000-2025, retrieved on 9 November 2026. There are 12,848 unique records. The file has 2,240,222 bytes and SHA-256 162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3. files/provenance.json records exact shared and resolved paths, source URL, source metadata and hashes. Used times, coordinates, depths and magnitudes are complete. No shared data were changed and no new data were downloaded.

Centers have preferred magnitude M from 6.5 to below 8 and UTC origin years 2001-2024. Shallow centers have depth at most 70 km. Deep centers have depth greater than 300 km. There are 925 candidates: 812 shallow and 113 deep. M uses mixed catalog magnitude types; it is not a common Mw scale.

Primary selection excludes a candidate with an equal or larger event within 200 km surface distance and at most 30 days on either side. All catalog depths and magnitudes can exclude a candidate. The rule retains 646 shallow and 99 deep centers. It uses future information and cannot be used as a real-time forecast rule. Selection does not prove independence.

## Method

We use Earth radius 6371 km. Surface distances are great-circle distances. Neighbor distances use the Euclidean chord between locations at radius 6371 minus recorded depth. Primary neighbors have M at least 5.5 and chord distance at most 200 km. They can have any depth. Buffer years cover the time windows.

Early counts use elapsed UTC time greater than 1 and at most 7 days. Late counts use greater than 7 and at most 30 days. The first day is excluded. Before diagnostic windows are [-7,-1) and [-30,-7) days. Each before window matches an after window in duration. These are pair counts. Several centers can share a neighbor.

We first calculate mean early and late counts per center in each depth and magnitude bin: [6.5,7), [7,7.5), and [7.5,8). We average these bin means with fixed pooled primary center weights: 498/745, 174/745 and 73/745. We then divide the adjusted late count by the sum of adjusted early and late counts. The primary endpoint is deep share minus shallow share. It is a ratio of standardized mean counts, not a mean of individual shares. Centers with no neighbors remain in all means. This avoids discarding quiet centers.

The late window has 23 days and the early window has six days. A constant rate has a late share of 23/29, or 79.31%. Thus a larger late share does not mean that the late daily rate exceeds the early rate. The estimate does not fit an Omori exponent.

We use 10,000 paired circular calendar-year block draws. Each draw samples three-year blocks and truncates to 24 years. Both depth groups and all settings use the same year weights. Percentile limits are conditional on the catalog, filters, magnitude weights and year-block dependence model. A draw can have an empty magnitude bin or no post-event counts; such a share is undefined. The primary three-year contrast has 10,000 valid draws. One- and five-year checks have 9,997 and 9,999. No correction is made for multiple checks.

Checks change radius, neighbor magnitude, isolation or overlap selection one at a time. The 100 and 300 km checks keep the primary 200 km isolation rule. No-isolation uses all candidates. Past365 excludes an equal or larger event within 200 km during the preceding 365 days only. Nonoverlap starts from primary centers and keeps them in time order; it removes a later center within 60 days and 400 km surface distance of a retained center. This reduces overlap but does not guarantee disjoint chord windows at depth, where a 200 km chord can cover more than 200 km of surface distance. All checks keep the primary magnitude weights.

## Results

| Rule | Shallow centers | Deep centers | Shallow late share | Deep late share | Difference, percentage points | Conditional 95% limits |
|---|---:|---:|---:|---:|---:|---|
| Primary, 200 km | 646 | 99 | 46.18% | 67.47% | 21.29 | 11.15 to 36.63 |
| 100 km | 646 | 99 | 40.87% | 55.36% | 14.49 | -1.40 to 31.42 |
| 300 km | 646 | 99 | 50.97% | 75.86% | 24.89 | 9.58 to 39.59 |
| M6 neighbors | 646 | 99 | 49.47% | 69.41% | 19.94 | -8.01 to 47.90 |
| No isolation | 812 | 113 | 42.53% | 55.28% | 12.75 | -1.36 to 29.62 |
| Past365 isolation | 583 | 95 | 43.09% | 63.21% | 20.11 | 5.53 to 36.83 |
| Nonoverlap | 596 | 91 | 47.10% | 71.73% | 24.63 | 7.01 to 46.59 |

The primary shallow counts are 332 early and 284 late. Deep counts are nine early and 19 late. Before counts are 76 early and 203 late for shallow centers, and one early and five late for deep centers. Raw count fractions differ slightly from the adjusted fractions in the table. The before counts show that ambient activity and earlier sequences can contribute, especially to the long late window. They are not a pure background sample.

As a descriptive diagnostic, subtracting the adjusted before count from each adjusted after count gives late shares of 24.00% for shallow and 63.57% for deep centers. We do not give a population interval for these unstable ratios. Negative excess counts or a denominator near zero can make this diagnostic unsuitable for inference. The primary test uses after counts only and cannot separate ambient events from caused events.

The primary contrast limits are 5.62 to 37.43 points with one-year blocks and 11.22 to 34.56 points with five-year blocks. Removing one primary center at a time gives contrasts from 17.80 to 26.41 points. Removing one occupied 20-degree latitude-longitude cell at a time gives 13.64 to 25.38 points across 68 cells. Cell indices use floor((latitude+90)/20) and floor((longitude+180)/20). The point contrasts in 2001-2012 and 2013-2024 are 17.84 and 33.18 points. These are influence and stability checks, not independent confirmations or tests of a period change.

files/results.csv contains all estimates, intervals, counts and valid-draw numbers. files/annual.csv has the sufficient statistics by year, depth and magnitude bin. Separate CSVs preserve the three-year draws. files/influence_summary.json gives deletion ranges.

## Interpretation and limits

At the main settings, deep nearby large-event counts have a larger late share. This is consistent with a response that is less concentrated in the early window, but does not identify the cause. Depth groups occupy different regions and tectonic settings. Magnitude-bin adjustment does not control fault type, slab structure, rupture size or detection conditions. A larger ambient fraction in a sparse sequence can also raise its late share. The result is not proof of slower physical decay at depth.

The contrast interval includes zero at 100 km, with M6 neighbors, and without isolation. Thus the evidence does not support a scale-independent depth effect. Only 28 deep after counts support the main test. Large uncertainty at the M6 floor reflects just ten deep counts. Pair counts share events and regions; year blocks may miss long regional dependence. The intervals omit source, selection and location uncertainty. Deletion checks do not replace a joint space-time model.

Catalog magnitude types, depth errors, fixed-depth solutions, revision and missing small events can change the sample. Excluding the first day and using M5.5 reduce some detection concerns but do not prove completeness. A fixed radius does not scale with rupture size. Before counts can include foreshocks and old sequences. Future isolation conditions on an observed outcome. None of these estimates measure hazard or identify individual aftershocks.

## Reproduction, checks and rights

Use files/REPRODUCE.md. Run files/analyze.py with the exact external input and a separate output directory. files/retrieve.py can retrieve into external scratch; it checks the source hash and reports catalog changes. The package includes our code, coarse aggregate results, figure, provenance and narrative. Raw data and record-level derivative tables remain outside the signed publication. files/EXTERNAL_DATA.md identifies external source rights and credit. The SCI baseline license does not replace those rights.

The independent audit uses standard-library UTC timestamps, scalar selection and Cartesian chords. It matches all 1,008 annual rows, every point estimate and each three-year saved-draw interval. files/audit.json records success. During development an implicit pandas timestamp unit gave incorrect time intervals. We made conversion to nanoseconds explicit and discarded those outputs before this audit and the final repeat. files/repeat.json records identical numerical files from a separate full run. These checks test arithmetic and data flow, not scientific assumptions.

## Campaign record

Job: sci-1107-dell-earth-and-ocean-sciences-3f6fa236b6f0. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Date: 9 November 2026. No child agents were used. Computation ran in the assigned isolated worktree. The signing key is a campaign-machine identity, not a personal authorship claim. No private key is included. This job made no remote upload or index submission.
