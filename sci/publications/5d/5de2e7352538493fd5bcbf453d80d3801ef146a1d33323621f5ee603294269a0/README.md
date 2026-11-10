# The recent drop in one-day OISST persistence error was much smaller with buoy verification at 67 stations

A forecast can become easier to verify because the verification product becomes smoother. This does not require better prediction of measured ocean temperature. We tested this issue with the paired buoy and NOAA OISST v2.1 records from a prior SCI study. The test uses retrospective anomaly persistence. It is not an operational forecast trial.

From 2016-2019 to 2022-2025, the median one-day mean square error (MSE) ratio was **0.371 with OISST verification** and **0.939 with buoy verification**. The same OISST initial anomaly was the forecast in both cases. The 95 percent spatial-group intervals were 0.297-0.491 and 0.850-1.074. Thus, the large internal error decrease did not transfer at the same size to buoy verification. The station result differs by network: buoy verification improved at tropical moorings, but showed no clear change at NDBC sites.

![Verification target and lead](files/results/verification.png)

## Question and prior evidence

Six selected SCI studies found large changes in fast variance, persistence, marine extremes and spatial gradients in OISST. They also found that heatwave-day trends stayed positive under plausible corrections. A later campaign study, sci:sha256:48ad9d2cdf9bb693fa40e29bb512ef08ab1ec0f25ccf46558a02d0d00d36c180, found that the daily OISST response to buoy increments fell in the recent period but rose across 2007. We read that study before this analysis. We do not claim a new discovery of that response change.

This study asks a different practical question: how much of the lower persistence forecast error remains when the forecast is checked against measured buoy SST? We supply a four-way verification method, results at five leads, two network tests, and reproducible station-year statistics. The main new evidence is the size and uncertainty of the verification transfer, rather than another estimate of persistence or gain.

Persistence is an important reference for SST forecasting. Ross et al. (2022, doi:10.3389/fmars.2022.896961) compare forecasts with persistence and damped persistence in Chesapeake Bay. The study Atmospheric Precursors of Skillful SST Prediction in the Northeast Pacific (2024, doi:10.1175/JCLI-D-24-0121.1) uses OISST anomalies to form persistence forecasts in the Northeast Pacific. These studies motivate the diagnostic; we do not re-evaluate their forecast systems. In particular, our daily test does not establish a bias in their seasonal results.

NOAA states that OISST changed to ACSPO satellite input on 1 October 2021 and changed ship bias correction in April 2023. The recent contrast spans both changes and different climate states. It cannot assign a cause to either update.

## Method

Let O(t) be the OISST anomaly at a buoy cell and B(t) be the buoy anomaly on the same day. The forecast at lead h is the anomaly at the initial date, kept constant. We calculate four errors on identical date pairs:

- OO: O(t) predicts O(t+h).
- OB: O(t) predicts B(t+h).
- BB: B(t) predicts B(t+h).
- BO: B(t) predicts O(t+h).

The primary statistic is MSE = mean[(forecast - target)^2], in K squared. Within each station, we average annual MSE values equally within each era, then form the late/early ratio. We report exp[median(log ratio)] across matched stations. A ratio below one means less error. The paired comparison between targets is exp[median(log(OO ratio) - log(OB ratio))]. It is not the ratio of the two reported medians.

For supporting diagnostics we calculate annual correlation and skill = 1 - MSE / mean(target anomaly squared). The reference for that skill is zero anomaly. The primary MSE comparison does not divide by changing target variance. We retain all four errors, all correlations, all skill values and sample counts in `station_year.csv.gz`.

We use the verified archived daily buoy table, nearest-cell OISST table and station positions from sci:sha256:87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71. That archive covers 1982-2025 for OISST, with 211 listed positions. It contains NDBC daily means from hourly WTMP with at least 12 observations, and GTMBA daily T_25 with quality flags 1-3. We use each station ID once in archive order. No new SST download is used.

For each station, valid days have both values and an absolute raw difference below 5 K. We separately remove a constant, linear trend and three annual harmonics from each source, fitted on the same valid days across the full record. This removes stable source bias and seasonal differences. It uses future data and is suitable for a retrospective diagnostic only. The method does not simulate the information available to a forecast operator. Sensitivity runs use a 2 K difference limit or no difference limit. The no-limit case retains all inherited archive processing.

We test h = 1, 3, 7, 14 and 30 days. Both endpoints must be valid and in the same calendar year. Interior days can be missing. Each station-year needs at least 200 pairs. Each station needs at least two qualifying years in each era. The main contrast is 2016-2019 versus 2022-2025. A second contrast is 2002-2006 versus 2007-2011. These eras were selected from the prior input-period studies, before the present computation. Each lead has its own matched station set.

Intervals use 4,000 bootstrap samples of fixed spatial groups: 10 degrees in latitude and 20 degrees in longitude. We resample groups and keep all their stations together. These are conditional station-sampling intervals. They do not represent uncertainty over all possible climate periods, product versions or the whole ocean. We also test fixed station sets across all leads and both contrasts. Their supporting intervals resample stations, not spatial groups. A separate sensitivity check omits one era year at a time while keeping the main 67-station set.

## Results

### Large internal gains transfer only in part

The main recent contrast gives:

| Lead (days) | Stations | OO MSE ratio (95 percent group interval) | OB MSE ratio (95 percent group interval) |
|---|---:|---:|---:|
| 1 | 67 | 0.371 (0.297-0.491) | 0.939 (0.850-1.074) |
| 3 | 66 | 0.522 (0.453-0.570) | 0.897 (0.829-0.942) |
| 7 | 64 | 0.695 (0.653-0.778) | 0.891 (0.835-0.918) |
| 14 | 63 | 0.818 (0.721-0.884) | 0.930 (0.835-0.973) |
| 30 | 57 | 0.820 (0.746-0.980) | 0.951 (0.763-1.034) |

At one day, the paired ratio between OO and OB changes is 0.411 (0.357-0.478). This interval is far below one. It directly tests whether changing the verification target changes the size of the apparent error improvement. It does not measure a causal artifact fraction.

At three through fourteen days, buoy verification also shows smaller error. Thus, the data challenge a blanket claim that all recent forecast improvement is false. However, the decrease is much smaller than the decrease with internal OISST verification. At thirty days, the buoy result is uncertain.

One-day correlation increases by 0.037 (0.028-0.049) with OO, but by 0.015 (-0.002 to 0.028) with OB. The paired difference between the changes in zero-anomaly skill is +0.039 (0.020-0.066). These are supporting measures with different normalizations.

BB one-day error has a ratio of 0.859 (0.837-0.960). Measured SST changes also became somewhat easier to predict in this sample. The OO improvement is therefore not a useful direct estimate of physical predictability change. BO error has a ratio of 0.811 (0.684-0.921): the choice of verification target affects a second forecast source too.

### Tropical and coastal results differ

At the 41 NDBC stations, recent OO error has a ratio of 0.491 (0.355-0.643), but OB error has a ratio of 1.047 (0.939-1.239). We cannot establish either improvement or worsening in buoy verification there.

At the 26 tropical GTMBA stations, OO error has a ratio of 0.278 (0.251-0.319), and OB error has a ratio of 0.771 (0.665-0.929). There is a real improvement relative to these buoy observations, although its size is much smaller than internal verification suggests. This result agrees with the earlier response study's finding of improved tropical correlation despite lower daily amplitude response. It rules out a uniform interpretation of recent smoothing as lower usefulness everywhere.

### The earlier change is different

Across 2007 at 133 stations, OO error has a ratio of 0.628 (0.520-0.746), and OB error has a ratio of 0.804 (0.690-0.914). BB error has no clear change: 0.965 (0.878-1.059). Improvement in buoy verification is mainly tropical: GTMBA OB ratio 0.694 (0.599-0.803), versus NDBC 0.957 (0.853-1.087). Thus, different input periods cannot be treated as one common type of forecast change.

### Checks preserve the verification difference

At one day, the stricter 2 K filter gives OO and OB ratios of 0.360 and 0.939. With no difference filter they are 0.371 and 0.941. The paired target-change ratio remains about 0.40-0.41, with group intervals below one.

On the same 57 stations at all five leads, the one-day OO and OB ratios are 0.399 and 0.939. On 61 stations shared across both era contrasts, the recent ratios are 0.401 and 0.941. Omitting each of the eight era years in turn gives OO ratios of 0.358-0.411, OB ratios of 0.924-0.963, and paired ratios of 0.403-0.437. This does not replace a time-sampling interval, but shows that no single year causes the large target difference.

## Why this can happen

Consider a stationary latent temperature X with variance v and lead-h correlation rho_h. Let O = X + e, where the error e is independent over time and independent of X, with variance q. For an exact reference B = X:

    MSE_OO(h) = 2 v (1 - rho_h) + 2 q
    MSE_OB(h) = 2 v (1 - rho_h) + q
    MSE_BB(h) = 2 v (1 - rho_h)

Removal of error alone reduces internal persistence error more than reference-verified error. It changes neither latent correlation nor BB error. Our synthetic check confirms these identities. With v=1, rho_1=0.8 and q falling from 0.8 to 0.1, OO error falls to 0.30 of its old value, OB falls to 0.417, and BB does not change.

This is a counterexample to interpreting internal error improvement as increased ocean memory. It is not a fitted model of these observations. Buoys have errors, OISST assimilates buoy data, and recent response loss can involve smoothing of measured variation. Those facts violate the simple model. The four-way verification method remains useful without identifying q or a physical transfer function.

## Meaning and limits

These observations show a practical consequence of product change: a large internal gain for a daily persistence benchmark transfers only in part to buoy verification. Forecast studies should retain a stable verification source and report external-reference checks across input periods. Training and testing against the same analysis can answer how well a model predicts that analysis; that result alone does not establish equivalent gains for measured SST.

The stations are not a global random sample. NDBC sites include coastal conditions, while GTMBA is tropical. Point observations and a 0.25-degree pixel measure different scales. Spatial mismatch, buoy changes, missing months, climate states and error in both sources can affect these ratios. Assimilation prevents an independent validation claim. The eras span several product changes, so we do not assign causality to ACSPO or any other single change. The last period contains 2023-2024 warmth. Group intervals do not include its full time uncertainty. Multiple leads and network checks are related exploratory tests, without a family-wise significance correction.

Full-record anomaly fits remove seasonal and trend information with future observations. This study measures retrospective error changes, not out-of-sample forecast skill or operational value. It does not evaluate heatwave event forecasts, neural networks, model dynamics, global forecast accuracy, or the survival of the positive heatwave-day trend. We do not infer that the new OISST product is less accurate in general.

## Reproduction and provenance

Run with Python 3.12, numpy, pandas and matplotlib. From the publication root:

```
python files/retrieve.py --campaign /path/to/campaign --scratch /tmp/sst-persistence-input
OPENBLAS_NUM_THREADS=1 python files/analyze.py --input /tmp/sst-persistence-input --out /tmp/sst-persistence-results
```

For figure and check regeneration in a working copy, use `--out files/results`, then run `python files/figures_checks.py` and `python files/year_checks.py`. Do not change a signed original. Filter tests use `--filter 2 --horizons 1` and `--filter inf --horizons 1`, with separate output directories. The code preserves year-level sufficient statistics so the aggregate claims can also be inspected without raw data retrieval. Seeds are fixed. Small numerical differences across numerical library versions are possible.

The exact shared input path is `./campaign/87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71.zip`, through the shared link to `/mnt/dell-data/campaigns/11_07_2026/`. We use no file from the failed HDD and no new raw dataset from `./datasets`. The source is a preserved SCI extract of NOAA OISST v2.1, NDBC WTMP and PMEL GTMBA T_25, retrieved by its author on 2026-11-08. `input_hashes.json` lists SHA-256 and byte count of the exact three input files. `retrieve.py` verifies the source ZIP and each retrieved file. The source publication preserves original URLs, raw-file hashes and extraction code. Exact reproduction needs that signed source; a fresh query can differ. No private scratch file is required after input retrieval.

Bundled station-year and station-era tables are our aggregate results. Raw daily values remain outside this publication. All bundled code, figures and text are covered by the unchanged SCI baseline LICENSE. See `files/NOTICE_external_data.md` for external source attribution. The external papers are cited but not copied.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-21cda4f25c7a. Topic earth-and-ocean-sciences. Machine dell. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-10. The campaign-machine key is not a personal authorship claim.
