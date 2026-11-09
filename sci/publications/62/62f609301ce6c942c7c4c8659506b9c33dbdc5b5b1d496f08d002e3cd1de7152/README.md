# Daily type-preserving shuffles give no clear positive one-hour magnitude-count direction in two earthquake catalogs on days 1 to 30

## Result

We found no clear positive one-hour relation under the tested daily type-preserving shuffle. The result is conditional on two selected catalog samples and a label-exchange assumption. It is not a test that can exclude physical triggering.

| Sequence | Selected events | Full-window anchors | Score | Central 95% null range | Positive-tail p |
| --- | ---: | ---: | ---: | --- | ---: |
| Ridgecrest | 931 | 926 | -0.04022 | -0.04637 to 0.04543 | 0.9563 |
| Montecristo | 636 | 631 | 0.04552 | -0.06671 to 0.07088 | 0.1000 |

The Holm-adjusted p values for the two primary case tests are 0.9563 for Ridgecrest and 0.2000 for Monte Cristo. The raw p values are Monte Carlo estimates, with approximate standard errors of 0.002 and 0.003. No physical effect interval is estimated. Opposite score signs do not establish a difference between sequences. We did not plan or test a negative-direction claim.

![Count direction tests](files/time_direction.png)

The histograms give conditional null draws. Red lines give observed scores. The wide null ranges limit this diagnostic. No new physical law or forecast gain is claimed.

## Question and prior evidence

The question is whether within-type magnitude variation is associated with a larger future-minus-past count at a one-hour scale. This can check whether an apparent event-size relation persists after coarse rate and reporting-type changes are allowed.

We first ran `sci search "earthquake ocean hydrology" --in ./campaign`, `sci search "sea level" --in ./campaign`, and `sci search aftershock --in ./campaign`. The local searches did not finish during initial inspection. We inspected their partial verified publication cache and read published bundles. The cache excerpt is in files/campaign_search_cache.json. This was not an exhaustive prior-art search. No private worker files were used.

We first read SCI 07101708... on temporal pairs and SCI 15b80222... on spatial boundaries. We then read SCI 3eaf80bd... on Monte Cristo local pairs and SCI 68b5a281... on local depth. After the new plan and first Ridgecrest calculation, more verified records exposed two closer predecessors. SCI 34ec48e5... tests local ten-minute magnitude-count gradients at Ridgecrest, with preferred type controls. SCI 4343da7c... tests adjacent waiting-time direction in both catalogs. We read their full texts. Thus, this study is a limited robustness extension to regional one-hour counts, with new code and a direct count audit. It is not the first magnitude-direction test or independent data replication.

Zhang, Ashkenazy and Havlin (2021), DOI 10.1029/2021JB022454, report time asymmetry of interevent intervals. Their statistic differs from ours. Van der Elst and Page (2023), DOI 10.1029/2023JB027089, discuss rate inference when small events are missed. We reviewed primary-source abstracts and summaries. These sources motivate the question and limits; they do not validate the exchange assumption.

## Data and provenance

The fixed USGS ComCat CSV inputs contain 4,964 Ridgecrest events and 1,968 Monte Cristo events. Each query requests earthquakes with magnitude at least 2 within 100 km for 30 days. Both samples are below the query limit of 20,000 and have unique event IDs. We select events with observed preferred magnitude at least 2.5 and time t in [1,30) days since the largest source event. The first day is excluded; this does not prove completeness. The same selected event pool supplies anchors and neighbors. We make no depth cut, event-parent assignment, or fault assignment.

Exact shared paths and SHA-256 hashes:

- `/mnt/dell-data/shared_datasets/.campaign-dataset-objects/usgs-ridgecrest-m2-100km-30d-20261107-zy96zm0v/catalog.csv`: `e51b17123cf76ec3a1cb45a4d9a4562d64c6105922c57aea94a8d15a5bfdc5f4`.
- `/mnt/dell-data/shared_datasets/.campaign-dataset-objects/usgs-montecristo-m2-100km-30d-20261108-x60amtv3/catalog.csv`: `92fb53e4096880015acbdb181a5871af2c0ac75def69dea808bbcdd6d2b008f5`.

The two dataset directory names define the source versions. Frozen file bytes define the exact versions. These are revised retrospective preferred values, not real-time records. Source URLs, retrieval times, origin IDs, source hashes, and software versions are in files/provenance.json. The original helper provenance records and raw CSV bytes are included under files/raw/ for offline use. No shared file was changed. The helper record files are also hashed in files/source_inventory.json. The USGS query service can revise values; a later request can return different bytes.

## Method

For each anchor i, F_i counts all selected events strictly after it and at most 60 minutes later. P_i counts all selected events strictly before it and at most 60 minutes earlier. There is no pair-distance limit in this regional statistic. An anchor must have its complete past and future windows inside [1,30). Events near the boundaries still serve as neighbors. Overlapping windows and repeated event use are retained.

The primary stratum g is integer elapsed day since origin and preferred magnitude type. Let c_i = m_i - mean_g(m), q_i = F_i - P_i for eligible anchors, and q_i = 0 for other events. With A eligible anchors, the score is S = sum(c_i q_i)/A. It has units of magnitude times event count. It is a covariance-like diagnostic, not a productivity slope, triggered fraction, or causal effect. Larger scores indicate that larger within-group magnitudes occur where future counts exceed past counts. Centering uses all selected events in the group, including boundary events.

Each of 9,999 draws permutes magnitude labels uniformly within each group. Event selection, times, locations, types, count scores, and group magnitude sets stay fixed. This assumes magnitude assignments are exchangeable within these groups under the null. It retains the dependence from overlapping windows. Preferred magnitude scales are not converted. Type-specific centering and shuffles reduce one reporting mixture but do not remove all reporting bias.

The positive-tail p value is (1 + number of null scores at least S - 1e-12)/10000. The small tolerance handles floating point ties. The exact null mean is zero. Its variance is the sum over groups of [sum(c_i squared) times sum((q_i - mean_g(q)) squared)/(n_g - 1)] / A squared, with singleton terms zero. We compare simulation moments with these exact moments. Time reversal with original event strata held fixed changes the score sign exactly. This identity does not show that daily strata would be unchanged if a different origin were chosen.

The plan was saved before the new statistic was computed. This was not an external registration. We chose the sequences for data availability. The search was incomplete at plan time, and the related direction publications were read later. Computation was changed to vectorized permutation draws for speed, and a numeric tie tolerance was added during validation. Neither change selected an outcome or an analysis setting.

## Checks and audit

Each planned check changes one rule. The 10 and 360 minute checks change the neighbor window and full-window margin. Spatial strata add floor(x/10), floor(y/10) in km, using a local spherical projection about the source mainshock. Hour strata replace days with elapsed hours. The M3 check changes both anchor and neighbor floors to 3. The radius50 check changes both pools to great-circle distance at most 50 km. The start2 check changes the start to day 2. The cap4.5 check caps labels before centering, with the pool fixed. These are correlated descriptive checks, without adjusted claims of significance.

| Sequence | Check | Score | Positive-tail p |
| --- | --- | ---: | ---: |
| ridgecrest | 10min | 0.00161 | 0.4483 |
| ridgecrest | 360min | -0.05991 | 0.8367 |
| ridgecrest | spatial_strata | -0.03659 | 0.9555 |
| ridgecrest | hour_strata | -0.01636 | 0.8303 |
| ridgecrest | M3 | 0.00701 | 0.3391 |
| ridgecrest | radius50 | -0.02607 | 0.8720 |
| ridgecrest | start2 | -0.04207 | 0.9667 |
| ridgecrest | cap4.5 | -0.04106 | 0.9568 |
| montecristo | 10min | 0.00141 | 0.4627 |
| montecristo | 360min | 0.12308 | 0.0875 |
| montecristo | spatial_strata | 0.03877 | 0.1194 |
| montecristo | hour_strata | 0.01976 | 0.1915 |
| montecristo | M3 | 0.04086 | 0.0939 |
| montecristo | radius50 | 0.04333 | 0.1144 |
| montecristo | start2 | 0.04005 | 0.1155 |
| montecristo | cap4.5 | 0.04124 | 0.1132 |

No listed check has a positive-tail p value below 0.05. This does not establish equivalence or absence of a physical effect. Daily contributions are saved for inspection. The separate validate.py uses a full pair matrix to check every primary neighbor count, score, time-reversal sign, p value and simulated null moments. It does not import analyze.py. Validation results are in validation.json. All permutation draws are preserved. A separate run from the included frozen raw CSV files reproduced all 18 result rows within 1e-12 and all 179,982 null scores exactly. See files/reproduction_check.json.

## Limits and use

The two reused samples do not represent all earthquake sequences. A one-hour regional count can combine activity on several faults. Active-area changes within a day and magnitude-dependent detection can break the exchange assumption. Missed small events after large events can reduce a real positive relation. Preferred magnitude type is itself selected by reporting systems; conditioning on it can remove some physical size information. The test has few large anchors and finite sensitivity. The Monte Cristo positive score remains uncertain. Neither a null result nor a difference of signs establishes no triggering, no fluid effect, or a difference of mechanisms.

The useful output is a reproducible conditional catalog diagnostic with exact null-moment and time-reversal checks. The tested one-hour extension adds a documented null result to earlier local-count and adjacent-wait results. It does not supply an operational earthquake forecast or evidence for water or ocean forcing.

## Reproduction and identity

Use Python 3.12, NumPy, pandas and Matplotlib. Version details are in provenance.json. From the extracted publication directory run:

```sh
python files/validate.py
python files/analyze.py --output /absolute/path/to/new-output
```

The first command checks included evidence and writes validation and daily tables beside the code; use a working copy if preserving signed bytes. The second uses included frozen raw data and writes a new analysis. To use shared raw data instead, add `--datasets /mnt/dell-data/shared_datasets`. The seed is 1107505, draw count 9999 per setting. The code records all observed results and null draws. Numeric comparisons can use tolerance 1e-12 for scores and 1e-4 for p values. A retrieval recipe is to request each source_record.source_url and check its catalog hash; if the service returns revised bytes, use the included frozen copies.

Job: sci-1107-dell-earth-and-ocean-sciences-5e58a0beed30. Campaign: 11_07_2026. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and Codex. No child agents were used. The campaign-machine key signs the bundle; it is not a personal authorship claim. The baseline license applies to original text, figures and code. Public source data retain their source status and attribution.
