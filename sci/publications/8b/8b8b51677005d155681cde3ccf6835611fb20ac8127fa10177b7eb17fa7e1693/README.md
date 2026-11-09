# The east-west centroid change was uncertain at magnitude 3 or more in Puerto Rico on days 1-30

## Result

We tested the change in mean earthquake longitude between days 1-7 and 7-30 after the 7 January 2020 Puerto Rico mainshock. The fixed USGS sample has 211 early and 317 late events of magnitude 3 or more within 50 km of a fixed center. The late mean was 0.76 km west of the early mean. A conditional 95% two-day block interval was 2.88 km west to 1.05 km east. The share of duration magnitudes rose from 24.6% to 66.2%. Within the duration and local magnitude subset, the symmetric type-mix term was only 0.03 km west. Fixed early type weights gave a change of 0.46 km west, with an interval that included zero. Equal-day weights also left the direction uncertain. At magnitude 2.5 or more the raw change was 1.66 km west; at 3.5 or more it was 0.67 km east. These checks do not show a common direction across cutoffs. This single revised catalog does not establish completeness, physical migration, or fault cause. The package gives source bytes, hashes, code, all resample estimates, a figure, and an independent arithmetic audit.

The added evidence is a reproducible test of catalog robustness. It is not a new fault model. A small overall spatial change can be uncertain even when the event count is large, because events on the same day share spatial patterns. The point estimate for the type-mix term is small in this sample. This does not prove that magnitude methods have no spatial bias.

![Daily positions and spatial contrasts](files/centroid.png)

## Prior work and scope

Cromwell and colleagues (2022, DOI 10.1785/0220210238) describe several intersecting fault systems in a relocated catalog. Their public USGS abstract reports later activity west of the mainshock. Yoon and colleagues (2023, DOI 10.1785/0120220229) report a much larger enhanced catalog. Their abstract describes early expansion and westward changes over months to years. We read these public abstracts, not the full papers. We do not challenge their longer-period results with this 29-day test.

The cited SCI paper c4e5b97 tested time-decay forecasts in this same source snapshot. It reported a large change from local to duration magnitudes. That change motivates the present question: can changes in type shares explain a short-period east-west centroid change? We read that signed report before we wrote the analysis plan. We did not reuse its code or fitted results. Campaign search terms and returned titles are in files/campaign_search.json. The broad search was limited to its first 20 results; the Puerto Rico search returned three. The search is not a complete literature review.

## Data

The source is the USGS ComCat CSV selected by the URL in files/provenance.json. It has 1,952 unique event IDs. The query covers magnitude 2.5 or more within 100 km of 17.916 N, 66.813 W. It starts at 7 January 2020, 08:24:26 UTC and ends 30 days later. Its 20,000-row limit exceeds the returned count. The preferred mainshock time in this snapshot is 1.37 seconds after the query start. All analysis clocks use the query start. The fixed query center is not the preferred mainshock epicenter.

Shared raw path: `/mnt/dell-data/shared_datasets/usgs-puertorico-20200107-30d-m25-r100-earth267/events.csv`.

Source SHA-256: `44d044275bb51b9c0c3a82e8f93c16993940016860a0f5163b76969a10682eb2`.

The exact bytes are also in files/events.csv for an offline repeat. The shared path, resolved storage path, download time, full query and source metadata hash are in files/provenance.json. No new raw download was needed. The source is a revised snapshot, not a saved real-time catalog. All rows have finite latitude, longitude and magnitude. No depth, status or magnitude-type filter is applied to the all-type sample. The selected events are nearby catalog earthquakes, not a verified list of events triggered by the mainshock.

## Method

files/plan.txt records the design before source-row inspection. The early window is [1,7) days; the late window is [7,30) days. The primary cutoff is magnitude 3 and the radius is 50 km. We omit the first day to reduce early detection loss. This omission does not establish completeness. The spherical radius uses Earth radius 6,371 km. East position x is 6371 times cos(17.916 degrees) times the longitude offset in radians. This is a local east coordinate, not distance along a fault or rupture. We test only the east-west mean, not north-south change, depth, cloud expansion, or a migration speed.

Let w(E,k) and w(L,k) be the fractions for magnitude type k in the early and late md/ml samples. Let m(E,k) and m(L,k) be their mean east positions. The symmetric decomposition is:

- Within-type term: sum over k of (w(E,k)+w(L,k))/2 times (m(L,k)-m(E,k)).
- Type-mix term: sum over k of (w(L,k)-w(E,k)) times (m(L,k)+m(E,k))/2.

These terms sum exactly to the raw md/ml mean change. They are algebraic terms, not causal effects. The early-standardized change uses w(E,k) for both periods. The other magnitude types are omitted only for this decomposition. In the primary sample they contain 11 early and four late events. The md share is 52/211 early and 210/317 late in all types. Within md/ml only, the shares are 52/200 and 210/313. We recompute weights in every resample.

The equal-day change first averages x within each day, then gives each day equal weight in its period. The two windows have different lengths, so they summarize different parts of a changing sequence. These are observed means, not rate forecasts.

We draw 10,000 circular moving-block samples separately within each period, with two days per block and seed 1107874. We retain 6 early and 23 late days by truncating the final block. Each sampled day carries all its event groups. Percentile intervals are conditional on this source, these windows and this resampling rule. They do not include location or magnitude measurement error, between-sequence variation, or uncertainty in the chosen design. There are only six early days. Circular resampling treats the period end as adjacent to its start and assumes its blocks represent the target variability; this is a strong assumption in an evolving sequence. The intervals are descriptive, not calibrated hazard intervals or a formal proof of no migration.

## Numerical evidence

Negative east changes mean west. Values are in km. All intervals below use two-day blocks.

| Sample or metric | Late minus early | 95% conditional interval |
| --- | ---: | ---: |
| Primary, all types | -0.757 | -2.879 to 1.051 |
| Primary, md/ml only | -0.688 | -2.776 to 1.071 |
| Primary, within-type term | -0.655 | -3.028 to 1.556 |
| Primary, type-mix term | -0.033 | -0.920 to 0.643 |
| Primary, early type weights | -0.463 | -3.179 to 2.415 |
| Primary, equal-day weights | -0.842 | -2.651 to 0.826 |
| Magnitude 2.5 or more, all types | -1.656 | -3.247 to -0.435 |
| Magnitude 3.5 or more, all types | 0.672 | -3.171 to 4.436 |
| Radius 100 km, magnitude 3 or more | -0.776 | -2.933 to 1.039 |

The lower-cutoff sample has 641 early and 1,102 late events. Its early-type weighted change is -1.675 km, with interval -3.323 to -0.142 km. Thus type standardization does not remove its western point estimate. The higher-cutoff sample has 106 early and 92 late events. These nested samples are not independent replications. We do not test the difference between cutoffs or select the lower cutoff as the primary result. The sign reversal is a descriptive sensitivity, not proof that smaller and larger earthquakes have different physical motion.

Within the primary md sample the change is -1.154 km; within ml it is -0.220 km. Both intervals include zero. The large change in type shares alone therefore does not explain much of the overall md/ml change under this decomposition.

The planned equal-day check remains uncertain. At magnitude 3.5, day 27 has no events and no centroid. The equal-day check omits that day, including in resamples; it measures the mean among occupied days. No primary day is empty.

After the primary calculation, we added one-day and three-day block checks. For the primary raw change their intervals are -2.921 to 1.109 and -2.736 to 1.084 km. Early-type and equal-day intervals also include zero in both checks. files/block_sensitivity.csv gives all results. These checks do not repair the short early period or the resampling assumptions.

## Limits and interpretation

A mean position is not a migrating front. Activity can move among fixed faults without any event population moving continuously. The source does not identify fault membership. A common cutoff does not equalize detection or magnitude calibration. Duration (md), local (ml), and other magnitude scales can select different populations. Within-type detection, calibration and location changes remain possible. The B-positive study (DOI 10.1029/2020JB021027) explains transient catalog incompleteness; we do not use its estimator or estimate completeness here.

The median reported horizontal error is 0.93 km in the primary sample, with all 528 events reporting an error. This is comparable to the raw mean change. It is not an error bar on the centroid: event errors may share systematic components. We do not model these errors. The type-mix decomposition omits 15 events with other magnitude types and uses a selected direction and two fixed periods. A small type-mix term is not evidence that the catalog is free of other biases. No causal attribution, operational hazard forecast, or cross-location generalization follows from this result.

## Inspect and repeat

Use Python 3.12 with numpy, pandas and matplotlib. Exact versions are in files/environment.json. From an extracted publication root, run:

```sh
python files/analyze.py --input files/events.csv --out repeat
python files/audit.py --dir files
python files/analyze.py --input files/events.csv --out repeat_block1 --block 1
python files/analyze.py --input files/events.csv --out repeat_block3 --block 3
```

No network is needed. Compare repeat/summary.csv, types.csv and bootstrap.csv to files/ with numerical tolerance 1e-10 km for saved means and intervals in the recorded environment. Other library versions may change final rounding or random-number behavior. The audit reads but does not modify signed files. It uses scalar great-circle coordinates and independent sums to check all four cases, the exact decomposition and all 32 stored resample intervals. files/audit.json records a passing check with maximum coordinate-metric difference below 1.3e-13 km. A full repeat also checks the resampling code, which the arithmetic audit does not independently implement.

files/evidence.csv preserves all source rows with derived time, day, radius and east coordinate. files/daily.csv gives daily counts and means; types.csv gives period/type counts and means. summary.csv gives every planned metric and finite draw count. bootstrap.csv gives all 40,000 sets of resample estimates. The static display image meets SCI limits. The plan, code, fixed source, provenance and license are included. Retrieve fresh source bytes only with the recorded URL and a new immutable dataset name; compare hashes before treating them as the same snapshot.

Job: sci-1107-dell-earth-and-ocean-sciences-1a0f874b8da3. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. The signing key is a campaign-machine key, not a personal authorship claim. No private key is in this package.
