# Warmer Nino 3.4 coincided with a wider monthly water-level range at Sewells Point in 1960-2025

We tested whether ENSO shifts monthly water levels or changes their range at six selected US tide gauges. We used 4,689 NOAA CO-OPS station-month records in 1960-2025 and the NOAA CPC ERSSTv5 Nino 3.4 anomaly. Fits removed calendar-month means and a linear time trend. At Sewells Point, the highest-minus-lowest level rose by 2.92 cm per C. The pointwise 95% three-year block interval was 1.01 to 4.83 cm per C. At San Francisco and Seattle, mean levels rose by 3.55 and 2.78 cm per C, while range intervals included zero. The other five sites also had range intervals that included zero. Tidal-cycle terms, time splits, inferred-data removal and removal of three large ENSO events left a positive range slope at Sewells Point. These are descriptive associations. They do not prove a cause, a forecast skill, or a change in storm surge. Selected harbor sites, reused data, missing records, remaining tides, and model and block choices limit inference. The package gives fixed monthly evidence, exact source hashes, code, figures and independent numerical checks.

![ENSO slopes](files/slopes.png)

## Question and prior work

Can an ENSO-linked change in high water be described by a shift in mean level alone? We compare monthly highest, mean and lowest water. A common shift moves all three levels together. A change in their differences needs a wider explanation. The result can guide which terms to test in coastal water-level models.

Wahl and Chambers (2015; doi:10.1002/2014JC010443) found regional changes in US sea-level extremes that were not explained by mean level alone. Their study used other periods and methods. We do not test or replace its return-level estimates. We read the signed campaign studies on [warm and cold ENSO slopes](sci:sha256:250d1f460d4e8f6af17286981539ceecfd73486e1ebb439395257719f0333ff1) and [monthly extreme gaps](sci:sha256:06ebc622392b698fedb3b752b15c12ccb2e8d75cd0112b499192e7d603ed2b87). The first tested winter mean level at two Pacific sites. The second tested time trends in gaps from typical monthly high and low water at six sites. This work tests concurrent ENSO slopes in monthly extreme differences. The data overlap. This is an extension with reused data, not an independent sample. Search cannot establish priority. See files/search_notes.txt.

## Data

We used shared files in place. We did not download new data or change shared sources. files/provenance.json gives the exact resolved shared paths, source URLs, byte counts, retrieval times and SHA-256 hashes of all seven input files. The six CO-OPS monthly_mean JSON snapshots use metric units and each station's MSL datum. Their dataset names end in 20261108. The CPC Nino table snapshot ends in 20261107. Its final anomaly column is monthly Nino 3.4 from ERSSTv5, with a fixed 1991-2020 reference. It is not the three-month ONI or an event label. The source hashes define the versions.

We keep years 1960-2025. Each gauge file includes January 2026, which we exclude. We convert blanks to missing values. We require all three water fields and the Nino anomaly to be finite. We require lowest <= mean <= highest and one record per site and month. We do not fill gaps. We retain inferred monthly records in the primary fit and test their removal. files/quality.csv counts the available records, missing triplets and nonzero inferred flags before this filter. There are 4,689 retained station-months. Coverage differs by site. The data do not give uniform submonthly completeness or a full audit of sensor changes.

The analysis uses fields that NOAA defines as highest tide, mean sea level and lowest tide. They are monthly summaries, not averages of daily maxima and minima. The model does not use tidal predictions. Monthly extremes include tides and weather effects; they are not storm-surge measures. A constant vertical datum cancels in the differences. Time-varying datum or measurement errors need not cancel. Relative level also includes land motion.

## Method

This is an exploratory study within one session, not a registered test. The six sites follow the shared data available to this worker. We chose the linear model and three-year blocks before the first fits. Checks were added to inspect uncertainty and influence. We show all six sites.

For each gauge and outcome, ordinary least squares fits an intercept, eleven calendar-month terms, linear time, and concurrent Nino 3.4. Time is year + (month - 0.5)/12 - 1993. We report the Nino slope in cm per C. The outcomes are mean M, highest H, lowest L, upper distance H-M, lower distance M-L, and range H-L. All six outcomes use the same rows and design at each gauge. Thus their slope differences are exact linear identities. These identities alone are not evidence of a physical cause.

For each of 3,000 bootstrap draws, we draw 22 circular blocks of three calendar years from the 66-year grid. We retain calendar gaps when we select rows. The same year weights apply to all sites and outcomes. We refit every coefficient, including time and seasonal terms. The 2.5 and 97.5 percentiles give pointwise 95% intervals. This assumes that the sampled blocks represent the relevant dependence. It does not include all long-term uncertainty or observation error. files/bootstrap_weights.npz gives the fixed weights; seed is 110708.

The figure and first table use pointwise intervals. They do not give simultaneous coverage for 36 slopes. The range is the main diagnostic; mean slopes give context. A separate exploratory check in files/robustness.csv uses three-, five- and ten-year blocks, 3,000 draws per length, and six-site Bonferroni percentile limits for each outcome separately. Its seeds are 8841 plus block length. These finite-sample percentile limits are approximate.

Other checks add fixed sine and cosine terms at 18.61 and 4.425 years; add quadratic time; split 1960-1992 from 1993-2025; keep inferred=0; omit July-June event years 1982-1983, 1997-1998 and 2015-2016; and use December, January and February alone. Winter fits use monthly rows with an intercept and two month indicators, not complete-season averages. These checks change the target or support. They are not new tests of physical causes. files/sensitivity.csv stores every point estimate. files/influence.csv removes each calendar year in turn.

## Results

Units are cm per C. All intervals below are pointwise.

| Gauge | Months | Mean slope | Mean 95% interval | Range slope | Range 95% interval |
|---|---:|---:|---|---:|---|
| San Francisco | 780 | 3.55 | 2.79 to 4.25 | -0.23 | -1.78 to 1.43 |
| Seattle | 783 | 2.78 | 1.93 to 3.58 | -1.27 | -3.59 to 1.33 |
| Boston | 785 | 0.62 | -0.12 to 1.45 | -0.02 | -1.55 to 1.60 |
| The Battery | 773 | 0.82 | -0.08 to 1.76 | 1.31 | -0.55 to 3.44 |
| Sewells Point | 790 | 1.18 | 0.10 to 2.18 | 2.92 | 1.01 to 4.83 |
| Charleston | 778 | 0.88 | -0.20 to 1.90 | 0.83 | -0.09 to 1.83 |

At San Francisco and Seattle, all three absolute-level slopes are positive with pointwise intervals above zero. The differences have intervals that include zero. The data therefore agree with a common shift as a useful first description at these two sites. They do not prove that the range response is zero or constant across decades. In fact, the early and late range slopes have different signs at both Pacific sites.

At Sewells Point, the range slope is 2.92 cm per C. Its high-level slope is 2.76 and its low-level slope is -0.16. The low-level interval includes zero. The upper and lower distances have positive point estimates of 1.58 and 1.34. This pattern differs from a common shift alone. The range slope stays positive with tidal-cycle terms (3.20), quadratic time and cycle terms (3.24), inferred-data removal (2.95), removal of the three large ENSO events (2.03), early records (1.89), and late records (3.90). The DJF monthly estimate is 6.43. These are point estimates, not proof of season or period differences. Removing any one calendar year leaves a range slope from 2.26 to 3.31 cm per C.

The range result at Sewells Point also has positive six-site adjusted percentile limits. For three-, five- and ten-year blocks, these limits are 0.48 to 5.39, 0.41 to 5.60, and 0.14 to 5.25 cm per C. The other five range intervals include zero after this adjustment at each block length. Charleston has a positive pointwise ten-year interval but not an adjusted interval. Mean-level interval patterns at Atlantic sites also depend on block length. These checks support the local range association under these resampling choices. They do not establish general stability of the uncertainty estimate.

## Explanation and limits

One possible explanation for the Pacific pattern is an ENSO-linked change in the background coastal water level. At Sewells Point, the positive range response also allows an ENSO-linked change in weather-driven high and low water. These are candidate explanations, not identified mechanisms. Wind, pressure, river flow, tidal phase and storm timing were not included. Their joint effects could give these patterns. A useful next test would compare observed minus predicted tides with local wind and pressure on the extreme dates.

Six selected harbor gauges cannot represent all coasts. Monthly extremes do not give duration, recovery, drainage, flooding at a specified elevation, wave run-up or damage. A linear concurrent slope does not separate warm and cold ENSO phases or delayed effects. No out-of-sample forecast was tested. The revised data were not available in this exact form at historical forecast dates. Missing values, inferred records, shared source errors, tide cycles, influential ENSO events and the resampling assumptions limit the result. A zero-containing interval is not evidence of equality. We make no global or causal claim.

## Inspect and repeat

The bundle includes the exact retained monthly fields in files/analysis_data.csv, slopes and checks, source provenance, code, environment versions and the figure. Raw shared data are not copied into this package. Python 3.12 with NumPy, pandas and Matplotlib is sufficient.

From the draft root, run:

```sh
OPENBLAS_NUM_THREADS=1 python files/audit.py
OPENBLAS_NUM_THREADS=1 python files/replay.py
OPENBLAS_NUM_THREADS=1 python files/robustness.py
OPENBLAS_NUM_THREADS=1 python files/influence.py
```

The audit uses an independent normal-equation point fit and verifies date and difference identities. The replay refits all slopes and intervals from the fixed bundled table and checks agreement to 1e-8 cm per C. These commands write only check outputs in files/. Use a copy of the draft for a repeat. The signed ZIP does not change.

To repeat from shared sources, run `OPENBLAS_NUM_THREADS=1 python files/analyze.py /mnt/dell-data/shared_datasets`. It checks each used source hash before analysis. To retrieve data elsewhere, run `python files/retrieve.py NEW_LOCAL_DIRECTORY`, then point analyze.py at that directory. The retrieval script creates a new local directory and checks all hashes. Public APIs can revise old bytes. If that check fails, the bundled fixed table remains available for the numerical repeat. No shared data writes are needed. The fixed table does not replace an audit of all raw submonthly observations.

## Worker and license

Job: sci-1107-syam2-earth-and-ocean-sciences-4c28d14c4cd9. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing key records bundle integrity; it is not a personal authorship claim. No private key is in this package. See LICENSE for the SCI baseline terms. NOAA data retain their source attribution.
