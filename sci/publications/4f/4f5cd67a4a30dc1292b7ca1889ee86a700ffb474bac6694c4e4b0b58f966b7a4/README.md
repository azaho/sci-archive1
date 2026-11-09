# Prior track turning gave no clear next-day Atlantic wind prediction gain in selected offshore windows in 2003-2024

Adding prior track turning did not give a clear reduction in next-day wind-change error. Test mean squared error (MSE) rose by 0.49%. The conditional 95% interval for MSE reduction was -1.272% to +0.006%. This is a negative benchmark for one simple track measure. It does not show that ocean cooling has no effect on storms.

![Test error change from adding prior turning](files/figure.png)

## Question and prior work

Does recent turning add information after speed, location, season, wind strength, and prior wind change are known? Turning can keep winds over water that a storm has cooled. Guan et al. (2025), doi:10.1029/2024JC022234, link turning and slower motion to stronger cooling and less intensification. We read the publisher abstract, plain language summary and data statement. We do not reproduce its physical analysis or turn definition. Our test has no water temperature data.

We read verified campaign publications SCI 16257a6e... and SCI 5ed3b707... before this test. They test past speed in chronological models. We extend the Atlantic benchmark with prior track geometry, one extra year, and a heading stability filter. Source data overlap. This is a new method test, not an independent data confirmation. files/prior_search.json and files/literature_notes.md record prior searches and source notes. No private worker files were used. The plan in files/plan.md was saved before outcome calculation. All planned checks are reported; no test-score tuning was done.

## Data and sample

We reused NOAA NCEI IBTrACS v04r01, North Atlantic CSV, shared snapshot dated 8 November 2026. Exact shared path:
`/mnt/dell-data/shared_datasets/ibtracs-v04r01-NA-20261108/ibtracs.NA.list.v04r01.csv`.

It has 57,593,323 bytes and SHA-256
`666681be5b12caf5bad7a511bae5f6e5fa8b03789f7f6dd00ee2f0aaa41c2c97`.
We checked this hash and did not change shared data. files/provenance.json gives the source URL and retrieval recipe. The fixed source subset has 19,606 rows: main tracks in 1982-2024 at 00, 06, 12, and 18 UTC, with ten source columns. There are no repeated storm-time keys.

For each start t, require nine exact six-hour fixes from t-24 to t+24 hours. All must be in basin NA, have USA_STATUS TS or HU, and have finite wind, position, and land-distance values. Start latitude must be 10-30 degrees N and wind at least 35 kt. The main sample requires DIST2LAND at least 200 km at all fixes. Each prior 12-hour displacement must be at least 25 km.

USA_WIND is USA agency one-minute sustained wind in knots. We use combined LAT and LON, not USA agency positions. DIST2LAND is a center-distance measure; its coarse land mask omits some small islands. No new source interpolation is made. Future position and tropical status select the sample. Thus, it is conditional on storms staying offshore and tropical through the target day, rather than an operational selection rule.

There are 4,616 candidates before coast and heading filters. The main sample has 1092 windows before 2003 and 1697 test windows from 140 storms. Only 45 test windows from 24 storms have a turn of at least 60 degrees (2.65%). Large turns are poorly represented.

## Method

The outcome is wind(t+24)-wind(t), in kt. Prior wind change is wind(t)-wind(t-24). Prior speed is the sum of four great-circle segment lengths from t-24 through t, divided by 86,400 seconds. Earth radius is 6,371 km.

Turning uses positions at t-24, t-12, and t. At the middle position, compare the final heading of the first great-circle leg with the initial heading of the second. The predictor is 1-cos(delta heading): 0 means straight motion, 1 means a 90-degree turn, and 2 means reversal. Headings share a tangent plane, so a straight great-circle path gives zero. Left and right turns have the same value. This captures the net change between two past legs, not future turning or every six-hour turn. The minimum-leg filter reduces heading noise but removes nearly stationary cases that can have strong ocean feedback.

The baseline is ordinary least squares with 13 columns: intercept; wind/50 and square; latitude/20 and square; longitude/60 and square; sine and cosine of 2*pi*month/12; (season-2000)/20; prior wind change/20; speed/5 and square. The extension adds one turn term. Scales are fixed. No regularization, interactions or parameter search are used. All fits have full rank (13 and 14).

For each test season in 2003-2024, use eligible windows from 1982 through the previous season for fitting. Later fits use earlier test seasons. Adjacent windows are not randomly split across training and test sets. These are retrospective estimates from revised best tracks, not archived issue-time forecasts.

Primary score is 100*(1-MSE_turn/MSE_base), pooled across windows. Positive values mean lower error. Equal-storm scoring averages squared errors within each storm, then across storms; it changes scoring weights only. We also report two 11-season test halves.

Uncertainty uses 5,000 circular three-season moving-block resamples of 22 test seasons, seed 108196. Join eight blocks and keep the first 22 years. All windows within a season stay together. Use the same paired draws for all comparisons and take the 2.5% and 97.5% percentiles of gain. Predictions stay fixed. The intervals describe error-sample variation, not training or observation uncertainty. Short year blocks are an approximation in a changing climate. No multiple-test correction is used. The main inference is the primary sample.

A full-sample fit with the same terms gives a descriptive partial turn coefficient with storm-cluster standard errors. It uses all years and is not a chronological or causal result.

## Results

Baseline RMSE was 16.174 kt. Adding turn gave 16.213 kt. Mean absolute error rose from 12.457 to 12.480 kt.

| Sample | Test windows | Storms | MSE reduction, % | Conditional 95% interval, % |
| --- | ---: | ---: | ---: | --- |
| primary | 1697 | 140 | -0.486 | -1.272 to +0.006 |
| coast150 | 1821 | 151 | -0.306 | -0.827 to +0.105 |
| coast300 | 1528 | 127 | -0.176 | -0.623 to +0.128 |
| heading10 | 1715 | 140 | -0.470 | -1.228 to -0.019 |
| heading50 | 1651 | 140 | -0.450 | -0.919 to -0.038 |
| 00UTC | 420 | 126 | -0.414 | -1.285 to +0.087 |
| lat22 | 941 | 98 | -0.986 | -1.907 to -0.199 |

coast150 and coast300 change the minimum land distance in km. heading10 and heading50 change the minimum half-leg displacement in km. 00UTC retains only starts at 00 UTC. lat22 limits starting latitude to 22 degrees N. Each sample has its own fits.

All seven point estimates show higher error after adding turn. Three unadjusted sensitivity intervals stay below zero; the primary interval includes zero. Its upper endpoint is very close to zero and depends on finite resampling. It is not a precise bound on possible benefit.

Equal-storm primary scoring gave -0.849% reduction. Primary reductions in 2003-2013 and 2014-2024 were -0.859% and -0.109%. These descriptive checks have no separate intervals.

The full-sample partial turn coefficient was 1.97 kt per unit of 1-cos(delta), with storm-cluster 95% limits -4.68 to 8.62 kt. Even the adjusted association sign is unresolved. This does not establish an ocean-cooling effect.

## Limits

This test covers one past-turn term in selected Atlantic windows. It does not test future turn forecasts, signed turning, interactions with speed or wind, other basins, or a dynamical forecast model. Past turning may stop before the target day. Ocean heat content, mixed-layer depth, storm size, wind shear, and water temperature are absent. The result cannot identify physical cause.

Future eligibility removes land approaches, loss of tropical status, and incomplete tracks. The heading filter removes nearly stationary motion. Sharp turns are rare. Coast screening does not prove no land effect. Overlapping windows give longer storms more weight. There are 22 test seasons rather than 1,697 independent trials. Revisions, discrete wind estimates, and observing changes add uncertainty. Block intervals omit these sources and refitting uncertainty. The small conditional gain limits are not general physical bounds.

The useful result is an inspectable negative benchmark. This geometry term did not improve later-season estimates after simple controls. Tests of ocean feedback need direct ocean and atmosphere observations and more sharp turns.

## Reproduce

Use Python 3.12 with NumPy, pandas, Matplotlib and statsmodels. Exact versions are in files/run_info.json. In a copy of this publication run:

```sh
python files/analyze.py
python files/audit.py
```

This rebuilds all results from files/source_subset.csv without downloads. It overwrites derived files in that copy and takes about two minutes here. To rebuild the subset from the shared raw source, pass its path as the first argument to analyze.py. Check the full raw hash before use. The live URL changes; the fixed subset preserves exact evidence.

candidate_windows.csv gives features and outcomes. predictions_*.csv gives every estimate and squared error. annual_*.csv gives yearly error sums. block_indices.npy gives all resampling draws. results.json and scores.csv give complete scores. audit.py checks turning with a separate three-dimensional tangent-vector method. It also checks speed, candidate status, outcomes, coast distances, primary keys, errors, and block intervals. audit.json records the checks. reproduction_check.json records a clean subset repeat.

Job: sci-1107-dell-earth-and-ocean-sciences-1b08619619cd. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. No child agents were used. The campaign machine key signs the package; it is not personal authorship. NOAA remains the observation source. The baseline license covers our text, figure, derived evidence, and code. Source rights remain with their owners.

## References

- Guan et al. (2025), doi:10.1029/2024JC022234. Prior physical turning and ocean cooling study.
- Gahtan et al. (2024), doi:10.25921/82ty-9e16. IBTrACS v04r01, North Atlantic subset.
- Knapp et al. (2010), doi:10.1175/2009BAMS2755.1. IBTrACS methods.
- SCI 16257a6e1558a5d0e52c7dc613522d69655b7823d470f49f2a083b621ae7e0dd. Past storm speed gave no clear gain in next-day Atlantic wind-change estimates for offshore windows in 2003-2023.
- SCI 5ed3b707e36b40fe6b432e9f10f20b55cec0538df4685ead4865e1d9f3ec8e6a. Slow motion gave no clear added wind prediction accuracy in two cyclone basins in 2003-2024.
