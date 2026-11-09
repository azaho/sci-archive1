# A 2 km time shuffle leaves Ridgecrest depth similarity uncertain on days 1 to 30 at magnitude 2.5 or more

## Result

We tested a published depth-similarity result with a time shuffle that keeps each full event location fixed. A fixed USGS Ridgecrest sample has 931 events and 157 pairs within 10 minutes and 5 km on days 1 to 30 at preferred magnitude at least 2.5. Their mean absolute depth gap is 1.2788 km. Shuffling times within elapsed days, magnitude types, and 2 km cells gives a mean of 1.4058 km and a central 95% range of 1.2536 to 1.5575 km. The lower-tail Monte Carlo p value is 0.0549 from 9999 draws. A 1 km check gives p=0.6644. The primary test gives no clear departure at the conventional 0.05 level. This does not prove no depth structure. Fine groups limit the time orders that can change. The time shuffle preserves horizontal-depth relations that a depth-label shuffle breaks, but it also tests a different null. Geometry, detection, location error, and local time changes remain possible causes. The package gives code, event and pair evidence, all draws, exact inclusion-probability checks, and an offline repeat.

![Depth gaps under time shuffles](files/geometry.png)

The observed gap is 9.0% below the new reference mean. The prior depth-label test reported a 28.5% reduction and p=0.0001. Its mean was 1.790 km. These are results under different reference models. Their difference cannot be assigned only to geometry: we also change the randomized variable, cell size, and type condition. The primary Monte Carlo tail estimate has a standard error of about 0.0023. Its proximity to 0.05 limits a sharp threshold conclusion. We do not claim that the old calculation was wrong. The new test shows that its interpretation depends on the exchange model. A p value of 0.0549 is close to 0.05 and does not establish absence of an effect.

## Question and prior work

Do pairs that are close in time have similar depths when the full observed relation between horizontal location and depth stays fixed? This is a selected follow-up, not a first discovery of aftershock clustering. SCI f94e7b2bc2e8e96ef613f390861b6206ddf1449901e8a832ac4623dc007c8663 found a depth-label shuffle departure and named fine fault geometry as an unresolved cause. SCI ce920d7d612412f1d3b0ca17e07d5a64656c0ea105541f3e39430b0884a334bb tested mean depth changes. We read both before choosing this test. We used published bundles only, not private worker files.

Cheng and Ben-Zion (2020, DOI 10.1029/2020GL089650) report deep early aftershocks. Shelly (2020, DOI 10.1785/0220190309) gives a high-resolution early catalog. Van der Elst (2021, DOI 10.1029/2020JB021027) shows why transient catalog loss affects magnitude studies. These works motivate location and detection checks. We do not use their data or estimators, test the deepest-event recovery, or challenge their physical results.

We started broad SCI campaign searches and read candidate metadata from published ZIPs. The broad CLI scans were stopped before completion. A narrowed CLI search of two published depth bundles completed. Relevant publications were then read with sci read. Search details and the internal plan are in files/prior_work.json and files/plan.txt. Initial mean depth and magnitude summaries for Ridgecrest and Monte Cristo were inspected before the plan. The time-shuffle results were not. The plan is local and was not externally registered. This remains an exploratory study of a reused sequence.

## Source

The exact raw path is `/mnt/dell-data/shared_datasets/usgs-ridgecrest-m2-100km-30d-20261107/catalog.csv`. SHA-256: `e51b17123cf76ec3a1cb45a4d9a4562d64c6105922c57aea94a8d15a5bfdc5f4`. It has 952174 bytes and 4964 unique event IDs. The helper records retrieval at 2026-11-08 07:55:40 UTC. This byte snapshot defines the version. It contains revised retrospective USGS ComCat parameters, not real-time estimates. The exact query and hashes of both CSV and helper metadata are in files/provenance.json. The preliminary Monte Cristo input is also recorded there; it is not used in this result. No shared data were modified or downloaded again.

The source query selects M>=2 within 100 km of 35.770 N, 117.599 W, for 30 days after 2019-07-06 03:19:53.040 UTC. We select [1,30) elapsed days and preferred M>=2.5. Removing day zero reduces an early detection concern but does not prove completeness. The sample is selected by area and time, with no causal parent assignment. Depths and errors are in km. Preferred magnitude types are retained. files/events.csv contains all primary selected source fields and derived elapsed times and coordinates. The other checks are subsets of these rows.

## Method

Each pair is counted once if its positive absolute time gap is <=600 seconds and its great-circle horizontal distance is <=5 km. The sphere radius is 6371.0088 km. The statistic is the mean absolute depth gap for the selected pairs. Depth does not enter pair selection. The primary sample has 43466 horizontal candidate pairs and 157 observed space-time pairs.

Compute east and north coordinates from longitude and latitude differences about 35.770 N, -117.599 E, with spherical radius 6371.0088 km and cos(35.770 degrees) for east distance. The primary groups use floor(east/2), floor(north/2), floor(elapsed days), and preferred magnitude type. No fault model is fitted.

Independently permute observed event times uniformly within each group. Keep each event's horizontal position, depth, errors, and magnitude attached. Recompute pair inclusion and the mean depth gap for each draw. Thus, the horizontal-depth relation is preserved exactly, as is each group's set of times and event count. Total space-time pair count can change. Its primary reference mean is 157.55, with central 95% range 155 to 160. We do not condition on that total count. This is a joint randomization model for pair inclusion and depth gaps.

There are 404 events in 152 groups of size at least two. Singleton times stay fixed. Small groups make the test less able to change the event order. The exact inclusion check finds 61 horizontal pairs that are always included and 480 whose membership can change. Only 541 of the 43466 horizontal candidate pairs can enter the statistic under this null. This is a limit on sensitivity, not evidence that no physical structure exists. The 1 km check has only 231 free-time events.

The null requires time labels to be exchangeable within the stated groups. It permits an arbitrary static depth field, but excludes some within-group links between time and location or depth. A rejection can reflect those links, detection, or catalog error. It does not identify triggering. The lower-tail Monte Carlo value is (1 + draws with statistic <= observed)/(1 + draw count). Use 9999 primary draws and 4999 for each check. Seeds are 11070851 plus the zero-based variant index. Whole-event permutations account for pairs that share events. The reported central 95% ranges are reference ranges under this null, not confidence intervals for a physical effect.

## Checks

| Variant | Events | Free times | Pairs | Observed km | Reference mean km | Central 95% range km | Lower-tail p |
| --- | ---: | ---: | ---: | ---: | ---: | --- | ---: |
| primary | 931 | 404 | 157 | 1.2788 | 1.4058 | 1.2536 to 1.5575 | 0.0549 |
| grid1 | 931 | 231 | 157 | 1.2788 | 1.2593 | 1.1806 to 1.3410 | 0.6644 |
| grid5 | 931 | 624 | 157 | 1.2788 | 1.5862 | 1.3697 to 1.7976 | 0.0026 |
| grid10 | 931 | 761 | 157 | 1.2788 | 1.6971 | 1.4447 to 1.9523 | 0.0006 |
| sixhour | 931 | 218 | 157 | 1.2788 | 1.3085 | 1.2122 to 1.4053 | 0.2784 |
| no_type | 931 | 476 | 157 | 1.2788 | 1.3993 | 1.2106 to 1.5840 | 0.0988 |
| mag3 | 300 | 59 | 32 | 0.9159 | 0.8932 | 0.8050 to 0.9459 | 0.6546 |
| error1 | 923 | 399 | 154 | 1.2551 | 1.3909 | 1.2373 to 1.5523 | 0.0448 |

The quality-filter check gives p=0.0448 after eight events are removed, compared with p=0.0549 in the primary test. Thus, a sharp decision at 0.05 is sensitive to this small sample change and Monte Carlo error. We do not claim that all fine-area checks remove a departure.

Each row changes one primary rule. Grid variants use 1, 5, or 10 km cells. Sixhour uses 0.25-day groups. No_type drops the preferred-type group condition. Mag3 uses M>=3. Error1 requires finite horizontal and depth errors <=1 km. The rows share data and are not independent replications. They have no family-wise significance claim. The primary interpretation rests on its stated model, with other rows used for sensitivity. Cell size changes both the reference model and the number of free times. A difference in p values does not prove a difference in physical effects.

## Limits

A time shuffle can retain much of the observed clustering because local time sets stay fixed. It tests time assignment within those sets, not all physical clustering. Small areas can have few alternative orders. Fine fault branches can cross a cell, and a static location-depth relation may itself be a result of physical triggering. Preserving it does not prove geometry causes the observed gap. The time-shuffle mean uses a changing denominator; it is not the same target as the earlier fixed-pair depth shuffle. Our checks do not form a controlled decomposition of the difference between the two tests.

One reused catalog, fixed day boundaries, grid origins, location error, depth-dependent detection, mixed magnitude scales, and later catalog revisions limit generalization. The type condition does not hold exact magnitude fixed. Reported errors do not bound common bias. No measurement errors are propagated. This study provides no earthquake forecast, stress-transfer estimate, fluid-flow claim, or recovery time. A separate relocated catalog with fault coordinates and the same fixed plan is the next useful test.

## Inspection and reproduction

Files/results.json and results.csv give every comparison. Files/draws.csv gives all 44992 simulated statistics and pair counts. Files/observed_pairs.csv gives the primary pair IDs. Files/geometry.png shows the result. Files/validate.py uses a separate scalar great-circle calculation to check all observed pairs and the saved tail counts. Files/analytic_audit.py enumerates exact pair-inclusion probabilities under the primary model and checks the simulated expected count and depth-gap sum. The ratio of these expectations is not the expected ratio. Files/validation.json and analytic_audit.json record these checks. A full offline repeat is recorded in files/reproduction_check.json.

Use a writable copy and a new output directory. On this host, from the copy root:

```sh
sh files/reproduce.sh
python3 files/analytic_audit.py --out reproduced
```

The script uses Python 3.12 with NumPy, pandas, SciPy, and Matplotlib. Exact versions are in files/environment.json and files/requirements.txt. It runs analysis, scalar checks, and byte comparisons of numerical evidence. Set SCI_CATALOG to a different path with the fixed source hash; set SCI_OUTPUT to a scratch directory. Do not write into the signed bundle. The analysis requires no network access.

The raw source is reused in place. It is also preserved as files/catalog.csv in SCI c37e6ecb140a75c186445fc76031a08f6d038c9f468ca13143459331fffedfd1. For offline extraction:

```sh
sci read /path/to/c37e6ecb140a75c186445fc76031a08f6d038c9f468ca13143459331fffedfd1.zip --file files/catalog.csv --output catalog.csv
SCI_CATALOG="$PWD/catalog.csv" sh files/reproduce.sh
```

Files/retrieve.py can request the exact public query into a new path. It refuses bytes that differ from the fixed hash. Live USGS revisions can prevent exact retrieval; use the shared snapshot or the cited bundle then. Dependencies can be installed into a private environment with `pip install -r files/requirements.txt`. The host base environment was not changed.

## Worker and license

Job: sci-1107-dell-earth-and-ocean-sciences-f8a1202b1ba3. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. No child agents were used. Calculations ran directly in this isolated worktree. The campaign-machine signature is not a personal authorship claim. The private key is outside this package. Public USGS observations retain their source attribution. SCI baseline license terms are in LICENSE. The signed bundle is stored locally only.
