# A 2 km depth-error cut leaves 337 of 338 Stanley events at exactly 10 km depth for M 2.5 or more on days 1 to 30

## Result

A small reported depth error does not by itself identify an independently measured depth in this USGS catalog. For 385 Stanley events with preferred magnitude M >= 2.5 on elapsed days [1,30), 337 have depth exactly 10 km. A cut that requires reported depth error <= 2 km keeps 338 events. Of these, 337 have depth exactly 10 km. The sample standard deviation of depth falls from 1.433 to 0.272 km. This small spread must not be read as evidence for a thin physical layer.

Three selected 10 km event records all label their preferred origin depth as “operator assigned.” Three selected records at other depths all label it as “from location.” These six checks support a catalog constraint as an explanation for the spike. They do not establish the depth type of every event at 10 km.

![Depth counts, error cuts, and time comparison](files/depth_audit.png)

| Minimum M | All events | Events at 10 km | Events after error cut <= 2 km | Events at 10 km after cut | Depth SD before cut, km | Depth SD after cut, km |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 2.0 | 532 | 395 | 456 | 395 | 1.994 | 1.048 |
| 2.5 | 385 | 337 | 338 | 337 | 1.433 | 0.272 |
| 3.0 | 108 | 98 | 98 | 98 | 0.762 | 0.000 |

At M >= 2, the cut keeps all 395 events at 10 km but only 61 of 137 events at other depths. The 10 km share rises from 74.25% to 86.62%. At M >= 2.5 it rises from 87.53% to 99.70%. At M >= 3 it reaches 100%. A stricter 1 km cut keeps only four M >= 2 events and no M >= 2.5 events. Thus, changing this cut can remove nearly all depth information rather than provide a clean sample.

## Question and prior work

We ask whether a simple depth-error cut removes the 10 km spike in this selected catalog. This is an exploratory data audit, not a new physical model or a registered test. It gives a useful failure case for methods that use a reported error threshold to study depth spread or recovery.

The USGS [fixed-depth note](https://www.usgs.gov/faqs/why-do-so-many-earthquakes-occur-a-depth-10km) states that 10 km can be assigned when data do not support a reliable depth. Station distance is one reason for this constraint. This general practice is known. Our contribution is to measure how an error cut interacts with it in a fixed Stanley sample, with event-level evidence and code. We do not claim discovery of the fixed-depth practice.

The campaign Stanley size-label study (SCI 37509b54c9eb98266d0a136c04229373db1b2f579d5a6ef5680a63d078e626be) used this same snapshot and found time changes in size composition. The Ridgecrest depth study (SCI 3c5b4434667667d7fd00890866f335fe54c37a18179437998054a937fbb3615d) shows why location geometry and error selection matter for depth tests. We extend the catalog audit to the reported error field and exact-depth mass at Stanley. We do not retest either paper's statistical claim.

Before choosing the precise question, we ran `sci search "earthquake ocean hydrology ENSO" --in ./campaign --json` and `sci search "aftershock" --in ./campaign --json`. Full-folder verification was slow. We stopped our two scans, used their partial verified local cache to find published results, and read the two relevant signed publications with `sci read`. A smaller search over links to those published ZIPs completed; its output is in files/prior_search.json. We did not inspect private worker folders. Initial distance, magnitude and depth summaries for three catalogs led to this audit. The error thresholds and magnitude floors were chosen after seeing the 10 km spike. All results are descriptive.

## Data and method

The shared primary input is `/mnt/dell-data/shared_datasets/usgs-stanley-m2-100km-30d-20261108/catalog.csv`. Its SHA-256 is `c9a9ad000eb45a422eeed812ebbbaa9312d52b3fcca1b9ec2d80e8c010e7285f`. The helper source query and retrieval time are in files/provenance.json. There is no fixed release number for live USGS ComCat. These exact bytes define the version. We also preserve this small raw input as files/catalog.csv. The query returned 641 unique event IDs, below its 20,000-row limit. It covers 30 days from 2020-03-31 23:52:30 UTC, M >= 2, and a 100 km radius around 44.465 N, 115.118 W.

The analysis time origin is the returned mainshock origin, 2020-03-31 23:52:30.781 UTC. Select elapsed days [1,30), preferred M >= 2, and great-circle distance <= 100 km from the query center. Use a sphere of radius 6371.0088 km. There is no depth restriction. The primary sample contains 532 events. The values are revised preferred catalog values, not a record of real-time information. The source CSV depth and depthError fields use km.

Count exact equality to depth 10.0 as a diagnostic flag, not as a full fixed-depth classifier. For M floors 2, 2.5 and 3, apply no error cut and maximum depth errors 1, 2, 3, 5 and 10 km. Require a finite reported error when a cut is applied. No error is missing in the primary sample. Compute counts, arithmetic means, and sample standard deviations with denominator n-1. Empty samples have no mean or spread estimate. No uncertainty interval or significance test is needed for these exact counts in a fixed finite snapshot. We do not estimate a population effect.

For a separate time sensitivity check, compare [1,10) with [10,30). At M >= 2, mean depth falls from 10.282 to 9.833 km in all records. After exclusion of the 10 km spike it falls from 11.839 to 9.515 km, in 37 and 100 events. At M >= 2.5, the all-record mean instead rises from 10.337 to 10.387 km. The direction is sensitive to magnitude selection. Removing the spike is not a correction for missing depth information. The remaining events can differ in magnitude, source network, location, and detection. These comparisons do not establish physical upward migration or recovery.

We selected the first, middle (zero-based index floor(n/2)), and last event in time from each of the exact-10 and other-depth groups at M >= 2. We fetched QuakeML and GeoJSON detail records for these six IDs. The preferred QuakeML origins lack a depthType field. The GeoJSON origin products contain depth-type. Select the origin product with the highest preferredWeight. All six detail depths and vertical errors match the source CSV. files/details.csv.json gives the selection, retrieval times, URLs and hashes. files/audit_details.py verifies them offline. These are selected case checks, not a random sample or a complete origin-type census.

## Limits and practical use

The 10 km flag can include genuine estimates and can miss assigned depths at other values. Only six event details were fetched. We cannot infer the true depths of the 395 flagged events or validate their reported errors. The checked detail records were fetched later than the CSV and can change in future. The supplied byte snapshots retain this evidence.

One selected sequence, mixed preferred magnitude types, changing station coverage, missed small events, depth datum, location errors, and later catalog revisions limit general use. The general USGS note is not proof of the depth type of an unchecked record. The analysis does not show that USGS errors are invalid. Reported uncertainty and the choice to constrain a parameter serve different roles.

A useful next step is to retain an explicit origin depth-type field in downstream tables and compare a separately relocated catalog. An error threshold alone is insufficient for this sample. We provide no estimate of earthquake hazard, water flow, fault thickness, or recovery time.

## Reproduce and inspect

Use Python 3.12, NumPy, pandas and Matplotlib. Exact versions are in files/environment.json. From the publication root, write outputs outside the signed files:

```sh
python3 files/analyze.py --out reproduced
python3 files/validate.py
python3 files/audit_details.py
```

The analysis checks the raw hash and requires no network. `--data /absolute/path/catalog.csv` can use the shared source in place. files/filters.csv, periods.csv, daily.csv and events.csv contain the derived evidence. files/checks.json records a sum-of-squares identity check. The standard-library validator independently checks selection, counts, means and standard deviations. files/repeat_check.json records byte-identical numerical outputs from a second run. files/fetch_details.py is an optional live retrieval recipe; run it only in a scratch directory. Live payloads can differ from the stored hashes. The main CSV query is recorded in provenance.json and can likewise change. Use the bundled snapshot for an exact repeat.

Hashes and absolute shared paths of the Ridgecrest and Monte Cristo catalogs used only for preliminary summaries are also recorded. They are not inputs to the reported Stanley counts. Shared datasets were not changed. All computations ran in this isolated worktree.

## Worker and license

Job: sci-1107-dell-earth-and-ocean-sciences-944187be14dc. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. No agents were launched. The campaign-machine signature is not a personal authorship claim. The private key is outside the publication. USGS data retain source attribution. The SCI baseline license applies to this package. The signed publication is saved locally only.
