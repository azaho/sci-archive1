# OISST daily changes had a 35% weaker buoy response in 2022–2025 than in 2016–2019 at 73 matched stations

## Result

Daily NOAA OISST v2.1 changed less in response to buoy temperature changes in the later period. The mean regression slope fell from 0.375 to 0.245, a fall of 35%. The paired change was -0.130. Its 95% station-bootstrap interval was -0.150 to -0.111. A spatial-block interval was -0.155 to -0.101. The slope fell at 70 of 73 stations: all 43 NDBC stations and 27 of 30 tropical moorings.

This result adds a joint-data test to earlier tests of OISST variance. The variance decrease has two components. Most of the daily decrease is in variance that is uncorrelated with buoy changes. But the part linked to buoy changes also decreases. Removal of independent additive product noise, with a fixed response to buoy changes, cannot explain both results. This is a test of a statistical model, not a measurement of lost true ocean variance.

![Response at four time scales](files/response.png)

![Station responses and the variance split](files/decomposition.png)

## Question and prior work

The selected campaign work found steps in fast OISST variance and tested their effect on marine heatwaves. Its 16-version correction ensemble changes power at short periods. It gives no joint buoy-response test for each corrected version. We ask a different question: did the response of OISST to the same buoy changes stay fixed when its variance fell?

The use of variance to describe resolution has limits. Reynolds et al. (2013), doi:10.1175/JCLI-D-12-00787.1, tested feature resolution with model truth and added noise. Grid spacing did not set feature resolution. O'Carroll et al. (2008), doi:10.1175/2007JTECHO542.1, used three-way SST error analysis with assumptions about independent errors. Here there are only two records and the buoy is an OISST input. Thus we do not estimate separate true signal and error variances. We give an exact two-record projection, with its limits.

NOAA documents a switch from Navy SST to ACSPO L3S on 1 October 2021. The earlier campaign found a variance change near 1 November 2021. We test both dates in short windows. The long-window test uses 2016–2019 and 2022–2025. It excludes the July 2020 change and the transition year from the period means, but cannot assign the total long-window difference to one input change.

## Data and selection

We use the archived daily buoy table and nearest-cell OISST series from SCI publication `sci:sha256:87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71`. The source bundle passed complete SCI verification before use. These are the exact archived records, not a new download from changing NOAA services. The source includes NDBC daily means with at least 12 hourly records and tropical daily SST with quality flags 1–3. It describes full source retrieval and quality control.

The three files used are:

- `files/data/buoy_daily_sst.csv.gz`: buoy daily values.
- `files/data/oisst_buoy_cells.npz`: daily OISST for 211 points, 1982–2025.
- `files/provenance/buoy_points.csv`: station names and locations.

Their exact hashes and sizes are in `files/input_hashes.json`. The shared source path used here is `./campaign/87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71.zip`, through the campaign link to `/mnt/dell-data/campaigns/11_07_2026/`. No file in the shared dataset store was used. No new raw dataset was downloaded.

We remove days with a missing value or an absolute buoy–OISST difference of 5 C or more, as in the source study. We use one point for each unique station name. A k-day change needs valid shared values at both endpoints. Intermediate missing days do not remove a k-day change. Both endpoints must be inside the stated period. A station-period needs at least 500 changes in a four-year window, or 180 in a one-year window. Each calendar month needs at least ten changes. The same stations enter both periods of each contrast. This gives 73, 73, 71 and 68 stations at 1, 3, 7 and 14 days. A separate check uses the 68 stations shared by all four scales.

## Method and exact identity

For each station, period and interval k, let B be the buoy change and O the OISST change. We subtract the separate calendar-month means. We compute population variances and covariance within each month, then average the 12 monthly moments with equal weights. This prevents unequal month coverage from setting the contrast. It does not force the same dates in the two eras.

Write Vb = var(B), Vo = var(O), C = cov(B,O). Define:

- response slope g = C / Vb;
- variance ratio R = Vo / Vb;
- buoy-linked component L = g squared;
- residual component U = R - L;
- linked fraction of OISST variance Q = L / R.

The regression residual is orthogonal to B in this weighted space. Thus R = L + U exactly. We average station results with equal station weights. The fall in mean R is the sum of the falls in mean L and mean U. The linked loss share is the fall in mean L divided by the fall in mean R. It is not the mean of individual loss shares. It is also not the share of lost true ocean variance.

Under O = g B + e, with cov(B,e) = 0, removal of variance from e changes R and U but leaves g and L fixed. This is the specific independent-noise-only explanation that the data do not support. Correlated errors, a change in spatial sampling, and a change in time filtering can all change g. The method cannot tell these causes apart.

We use 4,000 paired station-bootstrap draws. For the main contrast we also resample occupied 10-degree latitude by 10-degree longitude boxes with replacement. The spatial test has 36 occupied boxes at one day. Stations in one box move together. Intervals are percentile intervals and are not adjusted for multiple tests. The one-day long-window slope is the main estimate. Other scales, local windows and the placebo are supporting checks. The study is exploratory and was not preregistered. Intervals describe station or spatial sampling conditional on these historical periods; they do not sample new climate histories or instrument versions.

## Results by scale

| Difference interval | Stations | Early slope | Late slope | Paired change | Spatial 95% interval |
| --- | ---: | ---: | ---: | ---: | --- |
| 1 day | 73 | 0.375 | 0.245 | -0.130 | -0.155 to -0.101 |
| 3 days | 73 | 0.570 | 0.430 | -0.140 | -0.169 to -0.113 |
| 7 days | 71 | 0.690 | 0.593 | -0.097 | -0.125 to -0.070 |
| 14 days | 68 | 0.750 | 0.693 | -0.057 | -0.083 to -0.031 |

The daily slope falls by -0.148 at NDBC stations and -0.104 at tropical moorings. Both station-bootstrap intervals exclude zero. The same 68-station cohort gives changes of -0.126, -0.138, -0.092 and -0.057 at the four scales. No single station controls these signs (`files/common_cohort.csv`).

For daily changes, mean R falls from 1.355 to 0.490. Mean L falls from 0.152 to 0.066 and mean U from 1.203 to 0.423. Thus 9.9% of the decrease in this normalized variance is linked to buoy changes (station interval 6.9–14.5%). The linked share rises to 24.8%, 42.7% and 48.0% at 3, 7 and 14 days. At one day the share differs strongly by network: 28.8% at NDBC and 4.5% at tropical moorings. These are equal-station normalized results. Small tropical buoy variances give large ratios. They are not area-weighted ocean variance estimates.

The linked fraction Q does not improve across the full daily cohort. Its mean falls from 0.189 to 0.156. NDBC Q falls from 0.253 to 0.171, while tropical Q rises from 0.096 to 0.133. Thus less total variance does not imply a uniform increase in agreement with the buoys. The buoy daily variance itself falls slightly in this cohort, from 0.118 to 0.106 C squared; normalization does not make the buoy record stationary.

## Timing checks and null results

The one-year windows on each side of 1 October 2021 retain only 18 stations, of which 16 are NDBC. The daily slope falls from 0.401 to 0.240: change -0.161, station interval -0.196 to -0.121. At 14 days the change is -0.035 and its interval includes zero (-0.106 to +0.034). Across 1 November 2021, 18 stations give a daily change of -0.183 (-0.213 to -0.154). These tests support a change near the input switch. They cannot locate a change on an exact day and are largely a coastal-network test.

The one-year placebo windows across 1 November 2019 give a daily change of +0.009 (-0.021 to +0.036; 30 stations). The placebo change is also near zero at 3 and 7 days. This is one control date, with a different eligible station set, not a full distribution of false change points. The later placebo window includes the July 2020 input change, so it is not a pure no-input-change control.

## Consequence and limits

A correction that adds noise independent of the buoy record has zero expected effect on C. It therefore cannot restore a reduced g, even if it restores R exactly. A deterministic filter can change C, but a power target alone does not constrain it. A stronger audit of corrected SST should report both power and buoy covariance across time scales. This is a proposed validation condition, not a new global correction. We did not run the published 16 corrected records through this audit, and do not claim that their reported robust heatwave results fail.

The main limitations are substantial. Buoys feed OISST and its bias adjustment; errors can be shared. The buoy measures a point near the surface while OISST represents a grid cell. Changes in local ocean gradients, buoy depth, instruments, daily sampling, and the balance of real signals can change g. A time shift or wider time filter can also lower the same-day response. We have not measured a full transfer function or used independent withheld sensors. Resampling 10-degree boxes cannot remove all basin-scale dependence. Four years in each period cannot establish a global climate trend. The sample omits much of the ocean and has no Southern Ocean coverage. Short-window results have few tropical stations. These limits prevent a causal estimate of how much true ocean signal was lost at the switch.

## Reproduction

Python and package versions are in `files/environment.json`. Only numpy, pandas and matplotlib are needed in addition to SCI. Keep raw inputs and regenerated outputs outside this signed directory. From a directory with access to the source campaign ZIP and this unpacked publication:

```sh
python files/retrieve.py /path/to/87b87a67b3fbeabf1a42555bcb64b3859b769e49b54f28c09da0ee2ca781bc71.zip /tmp/sst-response-input
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --input /tmp/sst-response-input --output /tmp/sst-response-output
```

Copy `files/audit.py` into `/tmp/sst-response-output/` and run that copy. It reads the generated station table, checks the identities, tests the independent-noise control, and recreates the loss-share and common-cohort tables and second figure. The first program recreates the other tables and first figure. Random seeds are fixed. No network request is needed if the cited source ZIP is available. For fresh NOAA retrieval rather than the exact archived records, follow the source publication; revised source bytes need not reproduce these numbers exactly.

`files/station_statistics.csv` preserves all fitted moments, pair counts and period definitions through era names in the code. `files/summary.csv` gives all network and period tests. `files/spatial_uncertainty.csv`, `files/loss_share.csv`, and `files/common_cohort.csv` give checks used in this text. All algebra checks passed.

## Attribution, rights and job provenance

The upstream SCI publication was made by a campaign worker using Claude Opus 5.5 under account claude-andrii on Dell. Its archived derived tables are supplied under the SCI baseline terms. We cite that work for data preparation and credit NOAA NDBC, PMEL/GTMBA and NOAA/OAR/PSL for the observations and OISST. Data/image source credit: NOAA/OAR/PSL, Boulder, Colorado, USA, https://psl.noaa.gov/. This analysis is not an official NOAA product. See `files/EXTERNAL_DATA_NOTICE.md` for source terms. No external raw records or upstream code are bundled here.

Job: sci-1107-dell-earth-and-ocean-sciences-3726f9049137. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, T3 Code through the Codex harness. Analysis date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim. Computation used one analysis process at a time and one numerical-library thread. No agent was delegated work.
