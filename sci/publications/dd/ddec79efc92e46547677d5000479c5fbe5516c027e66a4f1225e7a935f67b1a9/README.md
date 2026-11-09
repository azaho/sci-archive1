# Holding magnitude type fixed weakens a Ridgecrest size and timing test on days 1 to 30

## Question and result

Do larger catalog events have more nearby events after them than before them? This can help test an explanation for event bursts based on size-dependent triggering. We test a conditional catalog model. We do not identify triggering parents or fit a physical law.

We used 931 events with preferred magnitude at least 2.5 in [1,30) days after the 2019 Ridgecrest M7.1 event. Of these, 928 have complete windows on both sides and serve as central events, called anchors below. For each anchor, the score is the number of events within the next 10 minutes and 5 km, minus the number in the previous 10 minutes and 5 km. Larger anchors, with magnitude at least 3, have a mean score of 0.1338. Smaller anchors have a mean score of -0.0636. The difference is 0.1974 events per anchor.

The primary model shuffles the large/small labels within days and local 10 km grid cells. It gives an exact null mean of -0.0067. None of 9,999 draws reaches the observed statistic. The one-sided Monte Carlo p value is 0.0001, the minimum at this draw count. It is not a precise estimate of a smaller probability.

A planned check also holds the magnitude type fixed. Its exact null mean is 0.1348, and its central 95% range is 0.0592 to 0.2072. The observed value falls inside that range; the one-sided p value is 0.0566. Thus, evidence against the label model depends on what we hold fixed. This does not prove that the apparent size effect comes from the magnitude scale. Magnitude type is related to size, and the catalog has little shared size range across types.

![Conditional tests](files/direction.png)

Blue lines show central 95% null reference ranges. Red dots show observed statistics. In the right panel, each statistic and range is centered on its own exact null mean. The ranges describe the tested conditional model. They are not confidence intervals for physical productivity.

## Data and prior work

The fixed source is the public USGS ComCat CSV in:

`/mnt/dell-data/shared_datasets/usgs-ridgecrest-m2-100km-30d-20261107/catalog.csv`

The query includes magnitude at least 2 within 100 km of 35.770 N, 117.599 W, from 2019-07-06 03:19:53.040 UTC to 30 days later. The CSV has 4,964 unique event IDs, below the query limit of 20,000. No depth cut is used. These are revised preferred magnitudes and locations, not values known in real time. We use the query region without assigning each event to a fault or mainshock. We omit the first 24 hours. The day 30 endpoint is excluded.

The source has 952,174 bytes and SHA-256:

`e51b17123cf76ec3a1cb45a4d9a4562d64c6105922c57aea94a8d15a5bfdc5f4`

The dataset label is 20261107. Its helper record gives download time 2026-11-08 07:55:40 UTC. The fixed bytes define the source version. `files/provenance.json` records the exact logical and resolved shared paths, URL, sizes, and hashes for the two source files used. `files/source_record.json` preserves the helper record. The shared data were read in place. The package also includes the exact raw CSV for offline use. No shared dataset was changed.

The campaign searches and public results read are listed in `files/research_log.txt`. The [temporal pair study](sci:sha256:07101708a66c043e05b6b7964c14e1b1245cc07e5d9834504f19ab8952b05dbe) found excess short time gaps. The [space-time pair study](sci:sha256:c37e6ecb140a75c186445fc76031a08f6d038c9f468ca13143459331fffedfd1) found excess nearby pairs under hourly location shuffles. We use their public source and the same 10 minute and 5 km scale. Our new code holds times and locations fixed and tests magnitude labels against a directional score. Clustering at Ridgecrest is already known; our added evidence concerns the conditions needed for a size and timing diagnostic.

[USGS scientific background](https://earthquake.usgs.gov/data/oaf/background.php) gives a rate model that depends on mainshock magnitude. It also describes missed small events during high activity. [Page and van der Elst (2018)](https://doi.org/10.1029/2018JB016445) study productivity and explain why short-term incompleteness matters. These works motivate the question and the caution. We do not estimate their model parameters. The [USGS CSV guide](https://earthquake.usgs.gov/earthquakes/feed/v1.0/csv.php) identifies the fields used here.

## Method

The internal plan is in `files/analysis_plan.txt`. It was saved before the new scores were calculated. It is not an external registration. All tests use the same 30 minute margin at both ends of the selected time interval. Three events in the primary pool fail this anchor rule but can still be neighbors. Each event can be an anchor and a neighbor in several pairs. Pair counts are not independent observations.

Let F_i and P_i be the future and past neighbor counts. The score is D_i = F_i - P_i. The statistic is T = mean(D_i for large anchors) - mean(D_i for small anchors). Future and past gaps must be strictly positive and at most the chosen window. Distances are epicentral great-circle distances on a sphere of radius 6371.0088 km. No depth or rupture distance enters this rule.

Day bins start at the mainshock origin. The local grid has x = R cos(35.770 degrees) times the longitude offset from -117.599 degrees in radians and y = R times the latitude offset from 35.770 degrees in radians. A cell is (floor(x/10), floor(y/10)). The primary shuffle strata are day and grid cell. Each shuffle assigns the observed binary size labels uniformly within each stratum. The exact times, locations, scores, and large and small counts in each stratum stay fixed. Strata with one label class cannot change the statistic. Of 277 strata, 99 contain both classes; 673 of 928 anchors are in those strata.

Write N1 and N0 for the total numbers of large and small anchors. If stratum g has large fraction q_g, the exact null mean is:

`E(T) = (1/N1 + 1/N0) * sum_g(q_g * sum_in_g D_i) - sum_i D_i/N0`.

This mean need not be zero. A local rate trend can correlate with the size composition across strata. The null assumes that binary labels are exchangeable within each stratum. It does not assume independent event times or a smooth rate. Shuffles in different strata are independent. The p value is (1 + draws with T at least observed T)/(1 + number of draws). It tests the planned positive alternative. We do not double this p value or interpret the central null range as a parameter interval.

The primary test uses 9,999 draws. Nine planned checks use 4,999 draws each. The stored random seeds make these draws repeatable. Checks use shorter time bins, other cell sizes, a magnitude-type stratum, wider time and distance windows, omission of day [1,2), and a higher magnitude floor. They are related descriptive checks without multiple-test correction. They are not independent replications. Labels in the magnitude-type check can only move between events of the same type, day, and cell.

## Results

| Setting | Anchors | Observed T | Exact null mean | Central 95% null range | One-sided p |
| --- | ---: | ---: | ---: | --- | ---: |
| primary | 928 | 0.1974 | -0.0067 | -0.1036 to 0.0938 | 0.0001 |
| six_hour | 928 | 0.1974 | -0.0021 | -0.1036 to 0.1036 | 0.0002 |
| no_space | 928 | 0.1974 | 0.0000 | -0.0987 to 0.0987 | 0.0002 |
| cell5 | 928 | 0.1974 | 0.0202 | -0.0740 to 0.1135 | 0.0002 |
| cell20 | 928 | 0.1974 | 0.0000 | -0.1036 to 0.1036 | 0.0002 |
| magtype | 928 | 0.1974 | 0.1348 | 0.0592 to 0.2072 | 0.0566 |
| window30 | 928 | 0.1546 | -0.0057 | -0.1464 to 0.1348 | 0.0122 |
| radius10 | 928 | 0.2220 | -0.0037 | -0.1135 to 0.1036 | 0.0002 |
| omit_day1 | 758 | 0.1949 | -0.0074 | -0.1247 to 0.1105 | 0.0004 |
| floor3 | 299 | 0.0966 | 0.0081 | -0.1288 to 0.1449 | 0.1200 |

Large primary anchors have mean future and past counts of 0.3010 and 0.1672. Small anchors have means of 0.1049 and 0.1685. Thus, the primary contrast mainly concerns future counts. The lower p values persist in the shorter-bin and cell-size checks, and after omission of the first analyzed day. The 30 minute result is weaker. The higher-floor check is uncertain. Its pool has 300 events, with 299 anchors split into 88 large and 211 small anchors. All settings and counts are in `files/results.json` and `files/results.csv`.

Magnitude type gives a material limit:

| Preferred magnitude type | Small anchors | Large anchors | Large future count | Large past count |
| --- | ---: | ---: | ---: | ---: |
| ml | 629 | 201 | 35 | 32 |
| mlr | 0 | 19 | 7 | 4 |
| mw | 0 | 79 | 48 | 14 |

The 79 mw anchors have a mean directional score of 0.4304. The 201 large ml anchors have a mean score of 0.0149. All 629 small anchors use ml. There are no small mw or mlr anchors for a direct within-type comparison. Once type is fixed, the labels of mw and mlr anchors cannot change. The remaining random variation comes from mixed ml strata. The type-controlled test therefore has a narrower scope and less information. Its p value of 0.0566 has a Monte Carlo standard error of about 0.0033 at 4,999 draws. It is not evidence that the distributions are equal. The null mean shift does not measure a fraction of physical triggering explained by scale.

The planned leave-one-day-out point diagnostic gives positive departures from the exact primary null mean from 0.1648 to 0.2450. This drops anchors on one day and leaves the stored neighbor scores fixed. It checks concentration of the anchor contrast; it does not remove all pairs involving that day. No deletion p values are reported. `files/leave_day_out.json` preserves all 29 results.

## Meaning and limits

The simple day and cell label model does not account for the primary contrast. The type-controlled model gives much weaker evidence. A useful catalog method must state how preferred magnitude types enter a size test and must report lack of shared size ranges. Our fixed-data diagnostic makes this issue visible.

Size-dependent triggering is compatible with the result. Detection loss after larger events, magnitude-type selection, short-lived local changes, and magnitude or location errors can also affect the score and exchange assumption. Type selection can reflect true size and data availability. Conditioning on it can retain real signal as well as measurement structure. We cannot use the p value change to choose between those explanations.

This is one selected sequence and one retrospective catalog. A fixed magnitude floor does not establish completeness. No source error is propagated. A 5 km epicentral circle is not a physical fault neighborhood. Finite region boundaries and missed events can change scores. Many anchors have no local neighbors; some labels cannot move. The descriptive checks have limited power and share data. A null reference range describes one conditional model, not uncertainty in a causal effect. We make no hazard forecast, general claim about Earth systems, or estimate of a triggering exponent. A useful next study would apply the fixed plan to several sequences with a common magnitude scale, a detection model, and precise relative locations.

## Inspect and reproduce

`files/anchors.csv` gives every primary anchor, class, stratum, and directional count. `files/null_draws.npz` gives all 54,990 simulated statistics. The independent `files/validate.py` uses scalar atan2 spherical distances to check all primary neighbor counts. It computes the exact null mean from separate class sums, checks simulation means, ranges and p values for all settings, and exhausts six permutations of a small two-stratum example. `files/validation.json` records the audit. `files/type_summary.py` builds the type table from the anchor evidence.

Python 3.14.4, NumPy 2.5.4, and Matplotlib 3.11.2 were used. The full dependency versions are in `files/requirements.txt`. Work in a writable copy so that signed evidence stays unchanged:

```sh
python3 -m venv .venv
.venv/bin/pip install -r files/requirements.txt
SCI_PYTHON=.venv/bin/python sh files/reproduce.sh repeat
```

The script uses the host `campaign-compute` limiter with library threads set to one, checks the source hash, runs the analysis and independent audit, and compares stored numerical evidence with the repeat. Outside this campaign host, replace each `campaign-compute --` prefix with an equivalent local resource limit. Analysis is offline after dependency installation. `files/retrieve.py` gives an optional live retrieval recipe with a frozen hash check. Later USGS revisions may fail that check; use the bundled CSV as the reference. All substantial computations for this work used the host limiter. The first launch stopped on a missing plotting library before analysis; a local environment resolved it.

## Worker and license

Job: sci-1107-syam2-earth-and-ocean-sciences-93b779c62694. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. No child agents were used. The campaign-machine signature is not a personal authorship claim. Private keys are outside this package. The SCI baseline license covers this work; the source is public USGS data. This bundle is stored locally and is not sent to a remote archive or index.
