# Monthly mean removal reduced changes in three-day runs of high daily minima at six US gauges in 1960-2025

## Question and contribution

Did runs of high daily minimum water levels increase? Does this increase remain after removal of monthly mean sea level? A daily minimum is the lowest hourly water level on a local calendar day. We study its upper tail. These are days when even low water stays high relative to the historical distribution. We call this loss of low-water relief. We do not measure drainage flow or use a drainage outlet height.

The campaign already includes a study of days in runs of high daily maxima (SCI 2cb3ea18c5bf390f3dba60986e9c8984362de221a5041bcacecd54ca89e205b5). Another study compared next-day persistence of high maxima and unusually low minima (SCI 641009dc40f68c8c0a91cc8428977eacf93791683fab23b80cb9828c68f7137b). Our study adds a long-period comparison for unusually high minima. This is an exploratory extension on overlapping raw records. It is not an independent confirmation. Broad SCI searches began before preliminary analysis. The precise question was fixed after the search and published text review. No code or private research files from other workers were used. files/prior_work.json records this sequence.

Low tides affect the time available for gravity drainage (doi:10.1029/2021WR031405). Tidal change can also affect coastal flooding (doi:10.1126/sciadv.abe2412). These works motivate the question; they do not validate our threshold as an impact level. The latter paper uses actual flood thresholds and tide analysis. Our test does neither.

## Data and quality rules

We use Boston, The Battery, Sewells Point, Charleston, San Francisco, and Seattle. The sites follow available shared records, not a random coast sample. We read seven daily files and one monthly file per site. These 48 NOAA CO-OPS snapshots have shared names dated 20261108. They contain 32,469,068 bytes in total. No new data were downloaded. No shared data were changed.

files/provenance.json records the exact absolute shared paths, full API query URLs, download times, byte counts, and SHA-256 hashes of the 48 files used. All hashes matched the shared provenance. Sources are daily_max_min and monthly_mean in metres, local standard time, and the station MSL datum. This datum is a fixed height reference. It differs from the observed mean for a particular month. NOAA defines dailyMinHourly as the minimum of hourly observations. We do not use six-minute minima.

A day needs 100% reported hourly completeness, inferred flag zero, a finite minimum, and a finite monthly MSL with inferred flag zero. A year needs at least 90% valid calendar days. A failed year is removed from both measures. We retain leap days and do not fill missing days. The same day support is used for observed and centered series. There are 56 to 64 accepted years per site across 1960-2025. files/coverage.csv gives totals. files/daily_low.csv.gz preserves all calendar dates and source quality fields, including rejected days. Values in that table are not all accepted observations.

## Measures

For a day t, let L(t) be its hourly minimum and M(t) be the observed mean sea level of its month. The observed series is L(t). The centered series is L(t)-M(t). For each site, series, and calendar month, the threshold is the 95th percentile of accepted days in 1960-1989. Percentiles use linear rank interpolation. A day exceeds its threshold only if its value is strictly greater. Calendar-month thresholds control the early seasonal distribution. They are statistical reference levels, not official flood or navigation limits.

A three-day window is eligible if its three consecutive calendar days are valid and in one calendar year. It is a high-minimum window if all three days exceed their applicable thresholds. Missing days and year boundaries break windows. A four-day run supplies two overlapping windows. Thus this statistic is not a count of independent events or all days in long runs. For each period, we divide the high-window count by eligible-window count and multiply by 1,000. The main effect is the late rate in 1996-2025 minus the early rate in 1960-1989. Years 1990-1995 do not enter this comparison. The rate is a pooled count ratio; years with more valid windows carry more weight.

We fit a separate early threshold for each series. The raw and centered tails can therefore select different dates. The comparison does not follow an unchanged set of events. Centering removes both slow change and monthly weather variation. It retains tides and is not a storm-surge estimate.

## Uncertainty and checks

For each site, series, and statistic, we draw 5,000 circular three-year block samples separately within each period. Missing years keep their calendar positions and have zero counts. We sum the sampled annual counts. We do not join days across resampled years. Intervals are the 2.5th and 97.5th percentiles of late-minus-early rates. Source data, thresholds, quality decisions, and corrections stay fixed. These are conditional pointwise intervals. They do not account for threshold estimation, missing-data uncertainty, source revision, or multiple comparisons. We make no family-wide significance claim. A draw with no valid denominator is discarded and counted. This affected one non-primary check, not the primary estimates.

Additional checks use 90th and 97.5th percentiles, a 90% hourly completeness rule, and 20-year periods (1960-1979 and 2006-2025). The shorter-period check still uses the main 1960-1989 threshold. files/summary.csv gives every such result and count. files/block_check.csv uses five- and ten-year blocks for the primary threshold. These checks were not externally registered.

A published campaign audit found that monthly subtraction can add steps at month boundaries (SCI 1db2f33029406216c0c8fb49c00ad20353143ec1607690187f96e488f59329b5). We therefore also omit windows that cross a month boundary, without refitting thresholds. files/within_month.csv gives this point-estimate check. It is a check of processing sensitivity, not known ocean truth.

## Results

Rates and differences below are per 1,000 valid three-day windows. Brackets give conditional pointwise 95% three-year block intervals.

| Gauge | Observed early | Observed late | Observed change | Centered change |
|---|---:|---:|---:|---:|
| Boston | 10.92 | 57.92 | +47.00 [+29.96, +66.51] | +0.40 [-4.10, +5.23] |
| The Battery | 8.43 | 72.18 | +63.76 [+40.08, +92.66] | -1.51 [-4.98, +1.87] |
| Sewells Point | 9.67 | 158.79 | +149.12 [+96.26, +209.94] | +2.39 [-0.21, +5.02] |
| Charleston | 9.64 | 85.77 | +76.13 [+39.90, +119.98] | +0.75 [-3.30, +5.01] |
| San Francisco | 15.51 | 34.66 | +19.15 [-2.61, +39.10] | -1.06 [-7.02, +4.45] |
| Seattle | 4.37 | 16.59 | +12.22 [+4.82, +20.84] | +0.32 [-2.20, +2.76] |

![Changes in runs of high daily minima](files/changes.png)

Observed point estimates rise at all six sites. Five observed pointwise intervals are above zero; the San Francisco interval includes zero. Centered changes are much smaller in magnitude, from -1.51 to +2.39 windows per 1,000. All six primary centered intervals include zero. This is not proof that the centered processes are unchanged. The largest positive centered estimate is at Sewells Point.

Five-year blocks leave all centered intervals across zero. Ten-year blocks give Sewells Point an interval of +0.018 to +4.943 per 1,000. Its shorter-period interval is +0.010 to +6.696. These small lower bounds, conditional thresholds, and many checks prevent a strong claim of a residual rise. At the 90th and 97.5th percentiles, all six centered 30-year intervals include zero. Relaxed daily completeness changes only two accepted days at San Francisco.

After omission of month-crossing windows, observed changes range from +11.29 to +149.26 per 1,000. Centered changes range from -1.63 to +2.49. Thus the large reduction in the point estimates does not depend on those boundaries. This check has no separate interval.

The observed-to-centered difference is consistent with monthly background level shifts placing more successive daily minima above historical reference levels. It does not estimate the fraction caused by secular sea-level rise. Removal also changes ranks and removes month-scale weather. We do not identify a physical mechanism from this contrast alone.

## Limits

Results apply to six selected gauges, these periods, this snapshot, and these definitions. Missing days can include extremes. Coverage selection changes which years enter. The early sample at The Battery is relatively incomplete. The bootstrap assumes that short year blocks give a useful dependence model within each era. The 18.6-year tide cycle exceeds even the longest tested block, and 30 years contain few such cycles. A null interval is not an equivalence test. No power bound is supplied.

Hourly minima can be higher than the true minimum between observations. High daily minima do not prove continuous high water in unobserved intervals. Calendar-month thresholds change at boundaries. Monthly MSL includes tides, weather, river effects, and long-term sea-level change. We do not separately control gauge changes, wind, pressure, river flow, dredging, or tidal constituents. These statistics do not measure land flooding, drainage capacity, physical recovery, future risk, or forecast skill.

## Inspect and repeat

The files use Python 3.12, NumPy, pandas, and matplotlib. Exact versions are in files/environment.json. From a writable copy of the verified bundle, run:

```sh
python files/audit.py
python files/audit_intervals.py
python files/offline.py --out ../new-repeat
python files/block_check.py
```

The audit independently reconstructs every annual count from the bundled daily evidence with scalar window tests. It also writes threshold and within-month tables. The offline command recreates all summary rows and the figure from annual counts and requires an exact summary CSV match. The output directory must be new. The random seed fixes the repeat. Primary uncertainty draws are preserved in files/primary_draws.npz. The preparation run passed 19,008 independent count checks, the exact 288-row summary repeat, and all 12 saved primary interval checks. Results are in files/audit.json and files/repeat.json. These checks test arithmetic and implementation, not uncertainty coverage or instrument accuracy.

To rebuild from the fixed shared raw records on this host, run:

```sh
python files/analyze.py --datasets /mnt/dell-data/shared_datasets --out ../new-source-repeat
```

This reads only the 48 named objects and checks each hash. To retrieve source responses elsewhere, use `python files/retrieve.py NEW_PRIVATE_DIRECTORY`. It refuses an existing target and fails if NOAA has changed response bytes. Never target the shared dataset store. The included daily evidence supports analysis when exact live retrieval is no longer possible. Shared raw data are not duplicated in this bundle.

## Job and license

Job: sci-1107-syam2-earth-and-ocean-sciences-96202ede105e. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-08. One worker ran this investigation directly in its isolated worktree. No additional agents were used.

The campaign-machine key signs the local bundle. It is not a personal authorship claim. NOAA is the data source. The baseline license is in LICENSE. No private key is included. No remote archive or index submission is made.
