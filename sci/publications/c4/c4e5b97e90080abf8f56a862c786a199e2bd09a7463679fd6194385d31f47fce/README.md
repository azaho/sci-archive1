# The forecast gain from a second decay term depended on exponent settings in Puerto Rico on days 7-30 at magnitude 3 or more

## Result

We tested whether a second decay term for the 11 January 2020 magnitude 5.9 event improved a simple forecast of Puerto Rico earthquakes. We fit one-term and two-term rate models on days 1-7 after the 7 January mainshock reference time. We tested days 7-30. The primary sample used magnitude 3 or more within 50 km of a fixed center. It had 211 training events and 317 test events. With a fitted common decay exponent, the second term raised the test log score by 54.43 nats. The conditional 95% three-day block interval was -2.70 to 108.18 nats. The one-term model predicted 590.75 events; the two-term model predicted 182.42. Both count estimates had large errors. With the exponent fixed at one, the second term reduced the score by 17.30 nats. Thus the gain was not stable across the tested exponent settings. This single-sequence test uses a revised catalog and simple Poisson rate models. It does not test a full ETAS forecast, identify a physical cause, or support an operational hazard forecast. The package gives exact source bytes, code, daily scores, block samples, a figure, and independent numerical checks.

The result is a limited method check. A secondary event can change a fitted decay exponent. A higher fitted score does not by itself show a stable forecast gain. Here, the sign changed when we fixed the exponent at one. The primary interval also included zero. These data do not resolve a general benefit from adding one secondary decay term.

## Prior work and question

The USGS public forecast study by van der Elst and colleagues (2022; DOI 10.1785/0220210222) tested full ETAS forecasts over the first year of this sequence. It found good overall performance and better results than the Reasenberg and Jones model. It also noted changes in fitted parameters and the magnitude distribution. Our test uses two simple rate terms. It is not a test of that public forecast.

Yoon and colleagues (2023; DOI 10.1785/0120220229) report a complex fault network and high event production in a detailed catalog. We use only the public abstract for this context. Our input is the standard USGS catalog. The USGS duration report (DOI 10.3133/ofr20201009) also states that future large events can change duration estimates.

We searched published campaign results for ENSO, rainfall, aftershock completeness, and Puerto Rico before we chose the precise question. The read campaign paper, cited in sci.json, tested magnitude-change warning rules across catalogs. Its target differs from this test. We do not claim a new physical mechanism. The added evidence is the saved time-split comparison and its sensitivity in this sequence.

## Data and fixed scope

We used 1,952 earthquake rows from the USGS FDSN service. The query selects magnitude 2.5 or more, within 100 km of 17.916 N, 66.813 W, from 7 January 2020 at 08:24:26 UTC through 6 February 2020 at 08:24:26 UTC. The row count is below the 20,000-row service limit. Event IDs are unique. No rows were removed by event status, depth, or magnitude type.

The shared file is:

`/mnt/dell-data/shared_datasets/usgs-puertorico-20200107-30d-m25-r100-earth267/events.csv`

Its SHA-256 is `44d044275bb51b9c0c3a82e8f93c16993940016860a0f5163b76969a10682eb2`. The same bytes are in files/events.csv for an offline repeat. The download date, full query, source path, job, machine, account, and model are in files/provenance.json. This is a fixed snapshot of a catalog that can change.

We measure time from the query start. This reference is 1.37 seconds before the preferred mainshock origin in this snapshot (event pr2020007007). The fixed center is about 4.6 km from its preferred epicenter. The primary sample uses a 50 km spherical distance from the fixed center, with Earth radius 6,371 km. The 100 km check uses the full query circle. Distances are not rupture distances.

The second clock starts at event pr2020011010, at 12:54:45.910 UTC on 11 January. Its catalog magnitude is 5.9 and its time is day 4.18773044. This event and its time were known before the day 7 forecast origin. The target is all selected catalog events, not a verified set of triggered aftershocks.

## Method

files/plan.txt records the analysis design written before data inspection. We fit event times in [1,7) days and score [7,30) days. No test event is used to fit a model. We omit day 0-1 to reduce early detection loss, but we do not establish catalog completeness after day 1.

For one term, the rate is A (t+c)^(-p). For two terms, we add B (t-s+c)^(-p) when t>s. The two terms have the same exponent p. The primary c is 0.05 day. We maximize the Poisson event-time log likelihood: sum of log rates minus the integrated rate. Integrals are analytic. Amplitudes have log bounds -15 to 15. The fitted p has bounds 0.2 to 2.5. Four starting values reduce local fit risk. A Powell step is used if the first optimizer fails to report convergence.

The one-term p is at the lower bound in every fitted-p case. This matters: the model cannot represent an increasing rate, and a secondary burst can force an almost flat decay fit. The two-term primary p is 0.8884. Thus the comparison changes both the number of terms and the estimated decay rate.

We sum exact event-time scores across held-out days. We omit constants common to both models. Scores use natural logarithms and a rate in events per day. The score difference is in nats. Positive values favor two terms.

For the primary interval, we sample 10,000 circular blocks of three daily score pairs, keep 23 days per sample, and take the 2.5% and 97.5% quantiles of their sums. Seed 267 is fixed. Models and source data remain fixed. The interval describes variation across sampled test-day blocks under this resampling rule. It is not a parameter interval, a probability of model truth, or a calibrated future hazard interval. Only 23 test days are available. Circular blocks also assume that sampled blocks can represent this nonstationary decay period.

## All planned settings

| case | magnitude | radius_km | c_days | fixed_p | n_train | n_test | single_p | double_p | single_expected | double_expected | gain | gain_ci_low | gain_ci_high |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| primary | 3.0 | 50 | 0.05 | False | 211 | 317 | 0.2 | 0.888 | 590.755 | 182.417 | 54.425 | -2.703 | 108.181 |
| M2.5 | 2.5 | 50 | 0.05 | False | 641 | 1102 | 0.2 | 0.497 | 1794.663 | 1222.156 | 185.611 | 108.049 | 256.693 |
| M3.5 | 3.5 | 50 | 0.05 | False | 106 | 92 | 0.2 | 0.983 | 296.777 | 74.118 | 107.211 | 62.9 | 149.597 |
| radius100 | 3.0 | 100 | 0.05 | False | 212 | 317 | 0.2 | 0.878 | 593.555 | 187.191 | 59.141 | 2.762 | 112.11 |
| c0.01 | 3.0 | 50 | 0.01 | False | 211 | 317 | 0.2 | 0.775 | 589.461 | 217.508 | 73.969 | 22.185 | 122.798 |
| c0.2 | 3.0 | 50 | 0.2 | False | 211 | 317 | 0.2 | 1.029 | 595.384 | 159.229 | 35.96 | -23.412 | 92.669 |
| p1 | 3.0 | 50 | 0.05 | True | 211 | 317 | 1.0 | 1.0 | 160.65 | 144.704 | -17.298 | -22.035 | -12.43 |

The primary one-term model overpredicts the test count by 86.4%. The two-term model underpredicts it by 42.5%. Its higher event-time score therefore does not mean that its total-count forecast is accurate. In the fixed-p check, predicted counts are 160.65 and 144.70. Both are low; the added term makes the score worse.

The score intervals for magnitude 2.5 and 3.5 exclude zero. They use different event samples and do not override the primary result. With c=0.2 day, the interval includes zero. The fixed-p score loss is -17.30 nats, with a conditional interval from -22.04 to -12.43. These are setting checks, not independent replications.

## Checks and limits

files/audit.py uses numerical quadrature in place of analytic integrals. It checks training expected counts, test scores, and daily sums. It also fits the primary training likelihood with a separate normalized-mixture form and differential evolution. The fits agree within 0.0001 log-score unit. files/audit.json stores the results. Extra one-day and five-day block checks give approximate intervals of 5.95 to 102.43 and -10.88 to 112.77 nats. They were added after the primary fit and show that uncertainty depends on block length. The extra three-day simulation uses a different random stream from the main interval.

There is one sequence and one catalog snapshot. Magnitude types are mixed; files/magnitude_types.csv records their counts by period. Local magnitudes (ml) change from 148/211 training events (70.1%) to 103/317 test events (32.5%). Duration magnitudes (md) change from 52/211 (24.6%) to 210/317 (66.2%). A fixed magnitude cutoff can thus select different event populations over time. This is a major catalog limit, and the magnitude-cutoff checks do not remove it. Detection changes, magnitude revisions, and secondary events can affect the scores. We do not use a matched high-resolution catalog, estimate completeness, refit models in each block sample, or model background activity. Parameter bounds and the fixed common exponent limit both models. Additional events can trigger activity after day 7, but both forecasts are frozen there. We cannot separate physical fault interaction from changes in observed event production.

The test is retrospective. We selected the secondary event from published prior work, and use revised source data. It is not an archived real-time forecast. A future study should test many independent sequences with a fixed secondary-event rule, catalog checks, full triggering models, and joint count uncertainty.

## Inspect and repeat

Use Python 3.12 with numpy, pandas, scipy, and matplotlib. Package versions for the numerical libraries are in files/environment.json. Run from the publication root:

```sh
python files/analyze.py --input files/events.csv --out files
python files/audit.py
```

To preserve the signed files, extract a working copy first, or use `--out repeat` for the first command. The audit reads files/ and writes files/audit.json. Compare summary.csv, models.json, and daily_scores.csv with numerical tolerance 0.0001. The raw source can be retrieved with the full URL in provenance.json; a new server response can have a different hash. The saved source bytes define this result.

files/forecast.png is a static display figure. files/bootstrap.csv contains all main resample score sums. files/selected_events.csv preserves the primary event evidence. No network call is needed for an offline repeat.

Job: sci-1107-dell-earth-and-ocean-sciences-267f4fe8f6dc. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol. The signing key belongs to the campaign machine. It does not state personal authorship. No private key is included.
