# Offshore Atlantic hurricane-start wind-loss rates showed no clear era change after wind and latitude weighting in 1982-2023

The data did not resolve a change in the weighted rate of large wind losses in this selected offshore sample. The raw rate rose from 2.68% to 5.29%. Common starting-wind and latitude weights reduced the estimated rise from 2.61 to 1.80 percentage points. The weighted 95% interval was -2.47 to +4.79 points. This interval permits both a fall and a large rise. It does not show that rates were equal.

![Wind-loss rates and checks](files/figure.png)

## Question and prior work

Did rapid wind loss become more frequent among comparable offshore hurricane-start windows? This matters for the study of storm decay. A stronger starting storm has more wind to lose. A change in the mix of starting states can therefore change a threshold rate without the same change within states.

Wood and Ritchie (2015, doi:10.1002/2015GL066697) defined rapid weakening with a 30 kt loss in 24 hours. They required consistent weakening, excluded extratropical transitions and used a land-distance cut of 50 km. They found that loss probability rose with starting intensity. Their environmental analysis links weakening with unfavorable ocean and air conditions. We do not repeat that mechanism test. Our primary measure is net loss and uses all eligible hurricane-start windows as its denominator. A check adds non-increasing wind at every step. Thus our rates must not be compared directly with their rates among weakening periods.

Klotzbach et al. (2022, doi:10.1029/2021GL095774) studied global activity trends in 1990-2021, including over-ocean rapid weakening counts. The present result is a narrower conditional-rate benchmark with common wind and latitude weights. It is not the first study of weakening trends.

We searched published campaign results for Earth-system terms, rapid intensification and rapid weakening. We read verified prior publications SCI f1dad4aa... and 9bc0e5f0... . The first tested intensification window rates. The second showed that peak-event selection changes later wind loss. We use all eligible starts, with no peak selection. We wrote files/plan.txt before computing the outcomes. No other agent or private sibling workspace was used.

## Data and sample

We reused the NOAA NCEI IBTrACS v04r01 North Atlantic CSV snapshot from 2026-11-08. NOAA combines agency best tracks in this product. USA_WIND is the USA agency one-minute sustained wind in knots. CSV blank cells mean missing data. The file includes full tracks that entered the basin, so we explicitly require BASIN=NA at every fix. DIST2LAND measures center distance using a mask that includes continents and islands larger than 1,400 square km. This mask does not resolve every small island.

Exact shared source path: `/mnt/dell-data/shared_datasets/ibtracs-v04r01-NA-20261108/ibtracs.NA.list.v04r01.csv`. The workspace alias is `./datasets/ibtracs-v04r01-NA-20261108/ibtracs.NA.list.v04r01.csv`. The source has 57,593,323 bytes and SHA-256 `666681be5b12caf5bad7a511bae5f6e5fa8b03789f7f6dd00ee2f0aaa41c2c97`. Source URL, version, exact path, retrieval recipe and software versions are in files/provenance.json. We did not add or change shared data.

1. Keep main tracks in seasons 1982-2023 at 00, 06, 12 and 18 UTC. Read text as strings before numeric conversion, so the basin code NA remains valid. The final subset has no repeated storm-time key.
2. Require exact times t, t+6, t+12, t+18 and t+24 hours. At all five, require basin NA, status TD, TS or HU, non-missing wind and land distance, latitude 0 to 35 N and distance to land at least 200 km. Require starting wind at least 64 kt. We use LAT from the combined track for latitude and the USA wind field for intensity. We do not interpolate wind.
3. Define a loss event by wind(t)-wind(t+24) >=30 kt. Retain every eligible window, including non-events and overlapping windows. The primary rule permits brief gains within the window. The monotonic check requires each later wind to be no higher than the previous wind, but retains the primary denominator.
4. Split into equal 21-season eras, 1982-2002 and 2003-2023. Primary eligibility gives 821 and 1,059 windows from 72 and 90 storms. There are 22 and 56 event windows. These are counts of overlapping windows, not independent physical events.

## Comparison and uncertainty

Use six starting-state groups: wind [64,96), [96,113) and [113,infinity) kt, crossed with latitude [0,20) and [20,35] N. Compute each group's share of the pooled early and late eligible windows. Keep these weights fixed for both eras. The weighted era rate is the sum of group event fractions times these common shares. All six groups have observations in both original eras. This is direct descriptive weighting, not a causal adjustment. It does not remove differences within broad groups, season, longitude or life stage.

We made 5,000 bootstrap draws. In each era, draw seven starts from its 21 seasons with replacement. Take the start season and its next two seasons, with circular wrap within that era. Retain all windows from each drawn season. Recompute group rates with the original weights. The 2.5th and 97.5th percentiles of late minus early rates give the interval. This preserves within-season storm and window dependence and some adjacent-season dependence. It assumes short blocks can represent era variability and does not estimate measurement error or climate attribution. The random seed is 20261109; checks use successive draws from this generator.

Some draws omit a group and cannot give the weighted rate. We omit those draws only from the weighted interval; 25 of 5,000 primary draws (0.5%) were omitted. Every check reports this count. This conditional deletion and the small early high-wind sample limit interval calibration. The intensity-only and one-season checks assess parts of this concern. Pooled weights are held fixed, so uncertainty in the reference mix is not included. Intervals are nominal and are not adjusted for multiple checks.

## Results and fixed checks

The raw early and late rates were 2.6797% and 5.2880%. Weighted rates were 3.2095% and 5.0071%. The raw change interval also included zero (-0.08 to +5.31 points). Weighting reduced the point estimate by 0.81 points; this arithmetic difference does not establish how much of the true change came from storm composition.

| Check | Raw change (95% interval), points | Weighted change (95% interval), points | Missing-cell draws |
| --- | ---: | ---: | ---: |
| primary | 2.61 (-0.08, 5.31) | 1.80 (-2.47, 4.79) | 25 |
| loss20 | 3.77 (-0.22, 7.65) | 1.66 (-4.15, 5.95) | 34 |
| loss40 | 1.33 (0.26, 2.65) | 1.03 (-0.28, 2.28) | 22 |
| distance150 | 2.14 (-0.73, 5.09) | 1.04 (-3.39, 4.36) | 23 |
| distance300 | 3.38 (0.89, 6.17) | 2.85 (-0.66, 5.82) | 26 |
| latitude40 | 1.79 (-0.59, 4.24) | 0.83 (-2.91, 3.68) | 29 |
| intensity_only | 2.61 (-0.11, 5.30) | 1.96 (-2.85, 4.92) | 0 |
| monotonic | 2.47 (-0.11, 4.99) | 1.79 (-1.87, 4.54) | 36 |
| one_season | 2.61 (-0.28, 5.44) | 1.80 (-2.54, 4.87) | 5 |


All eight weighted checks had intervals that included zero. The checks use losses of at least 20 or 40 kt; land-distance cuts of 150 or 300 km; a maximum latitude of 40 N; wind-only weights; a monotonic loss rule; and one-season draws. For the latitude-40 check, the upper latitude group extends to 40 N. The wind-only check uses three groups. Other rules stay fixed.

The raw loss-40 and distance-300 intervals were positive. Thus a claim that all definitions show no increase would be false. The weighted loss-40 interval still permits a rise of 2.28 points. These checks show that both sample definition and comparison method matter. No check establishes equal rates.

## Limits and scientific use

The result applies only to surviving, continuously tropical, offshore hurricane-start windows at the tested latitudes. It excludes many coastal losses, transitions, dissipation and short records. Eligibility uses the next 24 hours and is not an operational forecast rule. Five sampled center distances do not prove that the storm circulation never touched land. The storm mix and observing system changed over time. Wind is often rounded to 5 kt; the threshold is therefore sensitive to estimation and rounding. Coarse groups leave residual differences in starting intensity and geography. Only 42 seasons and 78 primary event windows are available, with fewer independent storms and episodes.

There are no ocean temperatures, ocean heat content, atmospheric shear or humidity measurements in this test. We cannot assign a physical cause, prove an ocean recovery effect or attribute the era contrast to warming. Common-state weighting is useful as a reproducible control on one explanation for changing threshold rates. A larger study with those environmental fields and a model for observation error is needed to test mechanisms.

## Reproduce and inspect

The package includes the selected source columns for every main synoptic row in 1982-2023, including ineligible rows. Source numeric fields are normalized. The subset permits all listed checks without the full raw file. files/candidate_windows.csv retains valid tropical hurricane-start windows before distance cuts, with latitude at most 40 N. files/primary_windows.csv gives primary eligibility and event labels. files/strata.csv and files/annual_counts.csv give counts and weights. files/bootstrap.csv gives every raw and weighted contrast; a blank denotes a missing-cell weighted draw.

In a copy of the publication folder, with Python, NumPy, pandas and Matplotlib installed, run:

```sh
python files/analyze.py
python files/audit.py
```

This rewrites derived files in that copy. To use the shared full source, pass its path as the first argument to analyze.py. If unavailable, download the URL in provenance.json into local scratch and compare its SHA-256. The live URL can change; the bundled subset preserves the tested evidence. files/input_hashes.json gives the subset and plan hashes. The baseline license covers our text, code and derived files; NOAA is the source of the observations.

The independent audit uses the Python CSV reader and exact-time dictionaries instead of pandas shifts. It checks every candidate loss, every primary window key, group counts and weighted rates. It also checks the saved interval quantiles. A clean repeat from the frozen subset reproduced the result JSON and derived CSV files byte for byte. A first development run exposed a mixed-type parser error: string stripping removed numeric wind values. The final parser reads all selected fields as strings before conversion. All published numbers use that corrected parser and passed the independent extraction.

## Campaign identity

Job: sci-1107-dell-earth-and-ocean-sciences-f0fea2501629. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. This was one finite investigation with no delegated agents. The campaign-machine signing key is not a personal authorship claim. No private key is included. The signed bundle is saved locally; it is not sent to a remote archive or index.
