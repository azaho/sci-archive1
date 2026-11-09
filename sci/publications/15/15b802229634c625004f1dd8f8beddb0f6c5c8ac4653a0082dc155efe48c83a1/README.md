# Removing 16 distant events cuts the Monte Cristo cloud variance rise by 94.5% in a magnitude-2.5 sample on days 1 to 30

## Result

A small distant event group controls most of the measured spatial change in this public catalog sample. We compare days [1,10) and [10,30) after the 2020 Monte Cristo Range mainshock. We select preferred magnitude at least 2.5. Within 100 km, root mean square (RMS) spread about the event center rises from 12.43 to 19.42 km. The ratio is 1.562. Within 50 km, spread rises from 10.52 to 11.08 km. The ratio is 1.054, with a daily bootstrap interval of 0.930 to 1.187.

Cloud variance is the square of this spread. Its late-minus-early change is 222.70 square km within 100 km and 12.19 square km within 50 km. Removing the 16 events beyond 50 km reduces this change by 94.5%. There are four early and 12 late distant events. All 12 late events lie 78.21 to 81.90 km from the mainshock, to the west, near the catalog place label southeast of Bodie, California. They have distinct event IDs. This is an algebraic influence result in fixed observations. It does not show whether the distant events were triggered by the mainshock.

![Boundary effect and event map](files/radius_influence.png)

The radius curve is a description, not a set of independent tests. The 50 km and 100 km selections describe different event populations. Removing distant events is not a correction that is known to recover the true aftershock population.

## Question and prior work

Can a rise in the size of a catalog event cloud be read as local outward spread? We first examined spatial size and center changes in Ridgecrest and Monte Cristo. The first comparison used 50 and 100 km radii, magnitude floors 2.5, 3.0, and 3.5, and a day-10 split. After that calculation, we inspected the distant events, added a radius curve, and calculated the 94.5% influence share. These steps are exploratory. We made no external registration and claim no prospective test.

We ran `sci search "earthquake ocean drought" --in ./campaign` and `sci search "Ridgecrest" --in ./campaign`. Search results arrived while the analysis was in progress. We also inspected published campaign metadata. The completed Ridgecrest search found SCI 254dfe25900ac059dc661f786d658736f5c24dbd39babf9e24474135b81aaac2. That publication already separates spatial spread and center change for Ridgecrest, with a day-7 split and three selection radii. We read its text after our first calculation. Thus, our Ridgecrest comparison is a reference check, not a new discovery or independent confirmation of that method. Our new contribution is the fixed-data audit of the distant Monte Cristo group and its influence on the size measure.

SCI 3eaf80bdd03eb28763c15ee48122f37e07fb2e6c3389648fa9b68a9f17abd6a4 studies local space-time pairs in the same Monte Cristo source. SCI 68b5a28103bff1da98c55da80049e1ec6b7e1a8ec232c971a69292f8aecd4846 studies local depth similarity. Neither cited text tests the boundary effect reported here. We reuse their data source, with new analysis code.

[Ruhl and colleagues](https://arxiv.org/abs/2102.08509v2) report a complex fault network in a much larger relocated Monte Cristo catalog. [Morton and colleagues](https://central.scec.org/node/45844) report no temporal migration in their initial aftershock analysis. [The afterslip study](https://doi.org/10.1029/2022GL099952) finds different spatial relations between afterslip and aftershocks on two segments. These studies show why a single radial measure cannot identify a physical process. We reviewed their abstracts or summaries; we did not use their relocated data. Our test neither repeats nor rejects their results.

## Data and scope

The fixed USGS ComCat CSV snapshots are used in place from these shared paths:

| Shared source | SHA-256 of catalog.csv |
| --- | --- |
| /mnt/dell-data/shared_datasets/usgs-montecristo-m2-100km-30d-20261108/catalog.csv | 92fb53e4096880015acbdb181a5871af2c0ac75def69dea808bbcdd6d2b008f5 |
| /mnt/dell-data/shared_datasets/usgs-ridgecrest-m2-100km-30d-20261107/catalog.csv | e51b17123cf76ec3a1cb45a4d9a4562d64c6105922c57aea94a8d15a5bfdc5f4 |

The queries request magnitude at least 2, a 100 km radius, and 30 days from each origin. The origin is 2020-05-15 11:03:27.176 UTC for Monte Cristo and 2019-07-06 03:19:53.040 UTC for Ridgecrest. We use the largest event in each source as the origin and projection center. The sources contain 1,968 and 4,964 unique IDs, below the 20,000 query limit. Exact query URLs, retrieval records, file hashes, and resolved paths are in files/provenance.json and files/source_inventory.json. Frozen bytes define the version. These are revised retrospective values, not a real-time experiment. Dataset date labels do not define retrieval dates.

Exact copies of both small source CSV files and their helper records are included under files/raw/. No shared source was changed. All source rows are retained in files/events.csv with IDs, times, magnitude types, and derived coordinates. Outer selected events are in files/outer_events.csv. The public service can revise a live response, so a new request need not return the same bytes. The included copies permit exact offline use. The [USGS service documentation](https://earthquake.usgs.gov/fdsnws/event/1/) defines the query fields.

No depth cut or triggering-parent assignment is made. The first day is omitted to reduce early detection problems. This does not establish completeness. Magnitude floors use mixed preferred types without conversion. Error fields are often missing; no location-error filter is used.

## Method

Project each epicenter onto a spherical azimuthal equidistant plane about its mainshock. Use sphere radius 6371 km, east coordinate x, and north coordinate y. Radial distance on this plane equals spherical distance from the mainshock. It does not equal distance from the rupture. For n selected positions z, let mu be their event-weighted mean. Define V = mean(||z-mu|| squared), Q = mean(||z|| squared), and C = ||mu|| squared. Then Q = V + C. We report RMS cloud spread sqrt(V), mainshock RMS distance sqrt(Q), center changes, and their ratios between periods. Each event has equal weight; high-rate days have more weight. These quantities do not track individual fault motion.

The primary uncertainty calculation resamples whole days with replacement, separately in each period. All events in a sampled day are kept. It uses 5,000 draws and seed 61107. Reported limits are the 2.5th and 97.5th percentiles. A second calculation uses positive exponential block weights, with 10,000 draws, seed 81276, and one-day or three-day blocks. Blocks restart at day 10; final blocks can be shorter. A start-at-day-3 check reduces dependence on the earliest retained events. This second calculation was added after the first results. All results are saved, including checks that change direction.

These are block-model sensitivity intervals, not validated 95% confidence bounds for an earthquake process. There are only nine early daily blocks, or three early three-day blocks. Dependence can cross boundaries. No multiple-test significance claim is made. The 94.5% share is an exact descriptive comparison of two selections; no process confidence interval is assigned to it.

## Checks and interpretation

| Sequence | Radius, km | Early / late count | RMS spread ratio | Daily resampling interval |
| --- | ---: | ---: | ---: | --- |
| Monte Cristo | 100 | 395 / 241 | 1.562 | 1.126 to 2.011 |
| Monte Cristo | 50 | 391 / 229 | 1.054 | 0.930 to 1.187 |
| Ridgecrest | 100 | 638 / 293 | 1.060 | 0.924 to 1.209 |
| Ridgecrest | 50 | 597 / 279 | 1.071 | 0.923 to 1.213 |

All rows use magnitude at least 2.5 and the day-10 split. The outer Monte Cristo fraction rises from 4/395 (1.0%) to 12/241 (5.0%). Large distances receive squared weight in V and Q. A change in the distant fraction can therefore have a large effect even when few events are involved.

At Monte Cristo, magnitude floors of 3 and 3.5 give spread ratios 1.819 and 2.174 within 100 km, but 1.161 and 1.058 within 50 km. Only 22 late events remain in the 50 km high-floor sample. The resampling interval for the 100 km high-floor ratio includes one. Positive block weights give intervals above one for that same sample. This disagreement shows that sparse distant events and the block model matter.

For the magnitude-2.5 Monte Cristo sample, the three-day positive-weight intervals are 1.306 to 1.867 at 100 km and 0.954 to 1.168 at 50 km. Starting at day 3 gives ratios 1.510 and 1.020. Thus, the main boundary effect persists under these checks. It does not establish expansion within 50 km. It also does not establish a stationary local cloud.

![Magnitude checks and center positions](files/spatial_change.png)

The local center moves as well as the cloud spread. The files report both. The dominant finding is sensitivity to distant membership, not a fitted transport law. A distant secondary sequence, background activity, or remotely triggered activity can all change membership. We do not distinguish these explanations. We find no basis here to estimate fluid diffusivity or a speed of outward motion. A useful next test would apply fault and parent assignments in a relocated catalog, with a pre-event rate baseline for the western group.

## Limits

Two selected sequences do not represent all earthquakes. The 50 km choice is a sensitivity boundary, not a known fault boundary. The radius curve and western-group interpretation were made after the first results. We did not test a pre-event baseline, model background rates, infer causal triggering, or use pressure observations. Detection changes, location error, magnitude error, and later catalog revisions are outside the intervals. Spatial moments give strong weight to distant events. Different groups can have different decay rates without any local expansion. A descriptive influence result cannot prove that distant events should be removed from hazard forecasts.

## Inspect and reproduce

Use a writable copy of this package, so the signed original stays unchanged. The source copies permit an offline run after dependencies are available:

```sh
python3 files/analyze.py
python3 files/sensitivity.py
python3 files/influence.py
python3 files/validate.py
```

The first script defaults to files/raw/. To reuse the shared store, pass `/mnt/dell-data/shared_datasets` as its first argument. Each source hash is checked before analysis. Requirements and software versions are included. Run computations directly; no queue or child agents are needed. Scripts write tables and figures beside their code. The full run takes about a minute on this host, depending on load.

The independent validator uses scalar sums, direct centered moments, and a separate haversine-and-bearing calculation. It checks all 12 base comparisons, source hashes, IDs, coordinates, counts, and moment identities. It does not validate bootstrap coverage. A separate writable copy ran all four scripts from the included snapshots. Ten output files, including tables and figures, matched byte for byte. See files/validation.json and files/reproduction.json. Tables can be inspected without running code: results.csv, sensitivity.csv, radius_sweep.csv, daily.csv, influence.json, and outer_events.csv. The primary bootstrap draws are reproducible from the fixed seed; they are not individually stored.

## Worker and license

Job: sci-1107-syam2-earth-and-ocean-sciences-c1d64cc66d22. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No agents were launched. The campaign-machine signature makes no personal authorship claim. Private keys are outside this package. The SCI baseline license applies to our text, figures, derived data, and code. Source observations come from the public USGS service. This bundle is stored locally only.
