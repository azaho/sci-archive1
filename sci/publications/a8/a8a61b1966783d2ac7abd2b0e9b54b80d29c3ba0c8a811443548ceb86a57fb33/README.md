# Six-hour controls reduced a short-gap spatial excess in a 2020 Puerto Rico earthquake catalog sample

## Result

We tested whether earthquakes less than ten minutes apart were unusually close in space after daily activity and magnitude type were held fixed. We used a fixed USGS catalog for days 1-30 after 7 January 2020, at magnitude 3 or more within 50 km of a fixed center. Of 73 selected consecutive pairs, 24 were within 5 km. Location shuffles within each UTC day and magnitude type gave a mean of 17.18 close pairs and a one-sided probability of 0.0357. Shuffles within six-hour periods and magnitude type kept the same 73 pairs but gave a mean of 22.88 and a probability of 0.4208. The excess above the shuffle mean fell from 6.82 to 1.12 pairs. Thus the apparent short-gap excess depended on the time control. The result does not establish a separate ten-minute triggering effect or its absence. It gives a reproducible control-timescale check for this revised catalog. One sequence, small pair counts, changing detection, location errors and the exchangeability assumption limit inference. Code, all shuffle counts, exact source bytes, an independent numerical check and a figure are included.

The observed close fraction was 32.88%. The mean was 23.53% under daily controls and 31.35% under six-hour controls. The corresponding excess was 9.35 and 1.53 percentage points. These are differences from a specified shuffle mean. They are not estimates of the fraction of earthquakes caused by triggering.

This study adds a small, inspectable method check. A daily control can leave spatial change within a day in the reference distribution. That change can appear as an excess among short-gap pairs. Finer controls retain more of this change. Here, the six-hour result had the same pair count and observed close count. The difference came from the reference distribution. A non-significant result with finer controls does not prove independence.

![Pair counts and all planned checks](files/clustering.png)

## Prior work and scope

We searched campaign results for earthquake, ocean, hydrology and ENSO, then for Puerto Rico and spatial clustering. We read the published decay and magnitude-type tests cited in sci.json. The first used this catalog to compare simple decay forecasts. The second showed that a changing magnitude-type mix affected a pooled larger-event share. Neither read test used the present pair statistic. The new work uses the same data, so it is not an independent replication.

Earthquake space-time clustering is established prior work. Tosi and colleagues (2008; DOI 10.1111/j.1365-246X.2008.03770.x) compared observed and shuffled earthquake catalogs to study spatial and temporal correlation. Knox (1964) described a close-pair method to test space-time interaction. We use selected consecutive pairs and restricted location shuffles. We do not claim a new general statistical method or a new physical law.

Van der Elst and colleagues (2022; DOI 10.1785/0220210222) evaluated the public USGS ETAS forecasts for this sequence. That study reported useful forecast performance and changing model parameters and magnitude distributions. Our check does not evaluate ETAS, assign parent earthquakes, or estimate hazard. We ask only whether a particular observed pair count exceeds a specified conditional shuffle reference.

## Data

We reused the public USGS ComCat CSV in:

`/mnt/dell-data/shared_datasets/usgs-puertorico-20200107-30d-m25-r100-earth267/events.csv`

The 367,830-byte file has SHA-256 `44d044275bb51b9c0c3a82e8f93c16993940016860a0f5163b76969a10682eb2`. It contains 1,952 unique event IDs. The dataset provenance records retrieval at 2026-11-09 07:28:30 UTC. This is a revised catalog with no numbered release. The hash defines our version. files/provenance.json gives the exact query, shared and resolved paths, source version and used-file hash. No download or shared-data change was required. files/events.csv preserves the raw bytes for an offline repeat.

The query selects magnitude 2.5 or more within 100 km of 17.916 N, 66.813 W for 30 days from 7 January 2020 at 08:24:26 UTC. This is 1.37 seconds before the preferred mainshock origin in this snapshot. We use days [1,30), magnitude at least 3 and epicentral distance at most 50 km from that fixed center. Spherical distances use radius 6,371 km. The primary selection has 528 events. We do not remove events by depth or status. Day 0 is omitted to reduce early detection loss. Completeness is not established. This geographic sample is not a verified set of triggered aftershocks.

## Method and assumptions

files/plan.txt records the design before pair-distance calculations. Prior papers had already exposed counts and catalog properties. This is a recorded retrospective design, not an external preregistration.

We sort the selected sample by origin time and then ID. We retain pairs that are consecutive in this full sorted sample, have a gap at most ten minutes, and share both UTC calendar date and magnitude type. Thus the statistic excludes intervening different-type events. It is conditional on sample selection, and does not cover all possible event pairs. The count of retained pairs within 5 km is the primary statistic. Distances use epicenters, not depths, rupture surfaces or uncertainty ellipses.

For each draw, we permute each location pair (latitude, longitude) among events within the same UTC date and magnitude type. Time, type, magnitudes, event count, spatial footprint per group and pair selection stay fixed. We use 9,999 draws. The one-sided probability is (1 + number of shuffled counts at least as large as observed)/10,000. Ties are included. The null assumes that locations are exchangeable among time slots within each group. It allows arbitrary temporal count variation but excludes systematic location changes within a group. It does not assume independent pairs. The joint shuffle accounts for shared endpoints.

The six-hour setting uses UTC bins starting at 00, 06, 12 and 18 hours. Pairs must share that bin as well as magnitude type. All 73 primary pairs pass that condition, so the observed count stays 24. This is a different, more local exchangeability assumption. It can retain real physical clusters and reduce power. It is not a uniquely correct null.

The other settings each change one primary choice. The Jan11 setting excludes events within one day of the catalog M5.9 event at day 4.18773044. The error setting requires a reported horizontalError at most 2 km. The pr setting keeps locationSource equal to pr. Each subset is sorted again; its consecutive pairs can differ. The radius100 setting adds an event that can break existing adjacency. The source error field is not a complete model of relative location error.

We use seed 886909 plus the setting index. files/analyze.py gives exact settings and draw order. The 95% null ranges are empirical quantiles of shuffled counts, not effect confidence intervals. The primary probability has Monte Carlo standard error about 0.0019. Sensitivity probabilities are descriptive and have no multiple-test correction. We do not select a new primary result from them.

## All planned results

| Setting | Events | Pairs | Close | Null mean | 95% null range | One-sided p |
| --- | ---: | ---: | ---: | ---: | --- | ---: |
| primary | 528 | 73 | 24 | 17.18 | 11-24 | 0.0357 |
| M3.5 | 198 | 26 | 11 | 8.19 | 4-12 | 0.1256 |
| M2.5 | 1743 | 418 | 99 | 73.63 | 59-89 | 0.0010 |
| radius100 | 529 | 73 | 24 | 17.03 | 11-24 | 0.0306 |
| gap5 | 528 | 36 | 11 | 8.61 | 4-14 | 0.2250 |
| gap30 | 528 | 130 | 44 | 30.08 | 22-39 | 0.0012 |
| distance2 | 528 | 73 | 9 | 4.32 | 1-8 | 0.0232 |
| distance10 | 528 | 73 | 49 | 38.91 | 31-46 | 0.0076 |
| six_hour | 528 | 73 | 24 | 22.88 | 16-30 | 0.4208 |
| exclude_Jan11 | 424 | 36 | 11 | 6.51 | 3-11 | 0.0340 |
| error2 | 504 | 62 | 21 | 14.16 | 8-21 | 0.0253 |
| pr_locations | 410 | 26 | 10 | 6.06 | 3-10 | 0.0434 |


The larger cutoff M3.5 has only 26 pairs and does not give a clear excess. The six-hour control also gives no clear excess. Several other settings give positive excesses under daily controls. These overlapping settings do not establish a universal spatial scale. In particular, the lower cutoff has more pairs but can have larger detection bias. Excluding the Jan11 window leaves a daily-control excess, so that window alone does not account for that result.

## Explanations and limits

Local stress transfer could produce close events, but changing active locations, detection coverage, location methods, or correlated location errors can also produce the pattern. Conditioning on magnitude type limits one known catalog mixture problem. It does not fix changing source practice within a type, exact magnitude effects or detection loss. Holding daily spatial patterns fixed does not hold six-hour spatial patterns fixed. This distinction explains why the two statistical references can disagree without a change in the observed pair count.

The six-hour test weakens evidence for an additional ten-minute effect under its assumptions. It does not show that the physical process lacks short-time triggering. More sequences and a stable high-resolution catalog are needed to separate physical fault interactions from measurement effects. This study does not identify fluid movement, stress changes, diffusion, fault migration or recovery time. It supplies a reproducible test that can prevent an overly strong physical claim from a coarse shuffle control.

There is one sequence, one revised catalog and a small primary pair sample. Thresholds were chosen for this study and can affect the result. We did not fit an earthquake forecast, use real-time catalog versions, estimate a complete magnitude threshold, or model the full location-error distribution.

## Checks and reproduction

files/audit.py separately reconstructs primary event selection and pair membership with scalar time differences and great-circle distances. It also computes the exact conditional null mean from all distinct location pairs within each group. The exact mean is 17.17984, consistent with the simulated 17.17822 (simulation mean standard error 0.03380). All 73 pair distances agree within 1e-7 km. files/audit.json records passed checks.

The first code version assumed nanosecond timestamps. An independent audit detected that pandas stored microseconds. We corrected the gap calculation to explicit elapsed seconds and reran every setting before publication. All saved results use the corrected code.

From an extracted publication directory, with Python 3.12, numpy, pandas and matplotlib:

```sh
python files/analyze.py --input files/events.csv --out repeat
python files/audit.py --files repeat --input files/events.csv --output audit.json
```

To audit the saved files directly, use `python files/audit.py --files files --output audit.json`. These commands leave signed inputs intact. An offline repeat produced byte-identical CSV outputs for all settings. Compare summary.csv, pairs.csv and all null_*.csv files to the saved files. They repeat exactly in the recorded environment; rounding can differ across libraries. files/environment.json records exact versions. No network access is needed.

The raw data can be retrieved again with the source_url in files/provenance.json using an HTTPS client. Compare its SHA-256 first: a current server response can differ. If adding a new shared snapshot, use the campaign dataset helper with a new name, rather than replacing existing data. The bundled source bytes define this result.

## Identity and license

Job: sci-1107-dell-earth-and-ocean-sciences-886909f53a8f. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. The signing identity is a campaign-machine key and does not claim personal authorship. No private key is included. The SCI baseline license applies to our text, figures and code as specified in LICENSE. Source data are attributed to USGS. Only local publication storage is used.
