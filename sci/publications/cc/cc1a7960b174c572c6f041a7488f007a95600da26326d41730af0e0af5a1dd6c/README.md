# Cascadia tremor days did not raise nearby earthquake rates beyond the rise 40-100 km away (PNSN tremor and ComCat, 2009-2026)

## Summary

We tested whether episodic tremor and slip (ETS) in the Cascadia subduction zone increases the rate of regular earthquakes near the tremor zone. We used the full PNSN tremor catalog (791,720 tremor windows, 2009-08-06 to 2026-11-07) and the USGS ComCat catalog for the same period (101,648 earthquakes between 39.5 and 50.5 N). We divided the margin into 0.25-degree latitude bands. We compared daily earthquake counts on tremor-active band-days with counts on quiet band-days in the same band and calendar month. We got the uncertainty from 1,000 common circular time shifts of the tremor record.

Results:

1. On days with 10 or more tremor windows in a band, M1.5+ earthquakes within 20 km of the tremor zone were 1.30 times more frequent (95% interval 1.12-1.53, p = 0.002). But M1.5+ earthquakes 40-100 km from the tremor zone in the same bands were also 1.34 times more frequent (1.05-1.61). The near/far ratio was 0.97 (0.76-1.30, p = 0.82). Thus we found no tremor-local excess.
2. The same-day excess did not occur on strong tremor days (50 or more windows: rate ratio 1.04, 0.82-1.36). It did not occur when the tremor was on the day before and the day after (1.11, 0.87-1.47). It did not occur around 1,118 major tremor arrivals in an event study (days 0-13: observed/expected 0.91, placebo range 0.86-1.16). Most of the excess came from weak-tremor band-days with 1-9 windows (1.18, 1.01-1.39). When we removed 3.8% of tremor windows on earthquake days, the excess decreased to 1.10-1.13 and was no longer significant. This occurred both near the earthquake times and 2-8 hours away. When we removed the same quantity of windows 3-30 days away, the excess stayed (1.24). Thus the same-day link depends on a small number of marginal tremor windows on earthquake days. It is not a property of ETS episodes.
3. ETS did not change the magnitude distribution near the tremor zone. For M1.5+ events during tremor days or the next 14 days, b = 0.86. For other days, b = 0.89 (difference -0.03, null 95% range -0.07 to 0.05, p = 0.65). The fraction of M2.5+ events was 12.5% and 12.2% (p = 0.73).
4. In 88 specifications (segment, magnitude, depth, tremor definition), the near/far ratio had p < 0.05 three times. All three were below 1. The only interesting positive hint is in Washington and southern British Columbia: M1.5+ events at 20 km depth or more on strong tremor days had a rate ratio of 1.51 (1.01-2.43, p = 0.04). The near/far ratio of all M1.5+ events on strong tremor days was 1.63 (0.97-2.70, p = 0.07). These results do not survive correction for multiple tests. A new data period must test them.

Main limitation: at the M1.5 completeness level, the data can exclude only a large tremor-local increase. The upper 95% bound of the near/far ratio is about 1.3 for same-day tremor and 1.18 for tremor days plus 14 days. Tremor and earthquake detections both depend on seismic noise. Thus same-day rate comparisons that do not use a spatial control can show false links.

## Research question and motivation

Slow slip changes the stress on the plate interface and the material around it. In some subduction zones, slow slip events increase regular earthquake rates. In Cascadia, studies of single ETS episodes found small surpluses of tiny intraslab events (Vidale et al. 2011). Bombardier, Cassidy and Dosso (2026, Seismica) studied northern Cascadia on the Canadian side (2006-2024). They found no significant link between daily seismicity rates and ETS. But they found a significant change in the magnitude distribution of M > 2.5 events during and shortly after ETS. We asked: in the US part of the margin (northern California to southern British Columbia), with the PNSN tremor catalog, do earthquake rates or magnitude distributions near the tremor zone change during ETS? Does a spatial control (earthquakes 40-100 km from the tremor zone) explain any change?

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| PNSN tremor catalog | Shared campaign dataset `datasets/pnsn-tremor-v3-20090801-20261108/pnsn_tremor_v3_20090801_20261108.csv`, from `https://tremorapi.pnsn.org/api/v3.0/events?starttime=2009-08-06T00:00:00&endtime=2026-11-08T00:00:00&format=csv`, downloaded 2026-11-08, 67,459,361 bytes, sha256 `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826` | Tremor window epicentres and times (791,720 windows) |
| USGS ComCat | FDSN event service `https://earthquake.usgs.gov/fdsnws/event/1/query?format=csv&starttime=Y-01-01&endtime=Y+1-01-01&minlatitude=39.5&maxlatitude=50.5&minlongitude=-128&maxlongitude=-119&minmagnitude=-1&orderby=time-asc&limit=20000`, one query per year 2009-2026, downloaded 2026-11-08 | Earthquakes (type `earthquake`; explosions and blasts removed). The exact CSV snapshot is in `files/raw_comcat/` (gzip); `SHA256SUMS_uncompressed.txt` gives the hashes of the uncompressed files |

The raw tremor file is not copied into this bundle, because it is in the shared campaign dataset store. The recipe above downloads it again. The derived band-day tremor count matrix is in `files/results/tremor_band_day_counts.npz`.

## Methods

**Tremor zone.** We counted tremor windows in 0.1-degree cells. The 704 cells with 300 or more windows hold 90% of all windows. These cells define the tremor zone (`files/results/footprint_cells.csv`). For each earthquake we calculated the epicentral distance to the nearest tremor-zone cell centre. "Near" earthquakes are within 20 km. "Far" earthquakes are 40-100 km away. We removed earthquakes within 15 km of 13 Cascade volcanoes (Baker to Lassen).

**Band-day activity.** We assigned tremor windows and earthquakes to 0.25-degree latitude bands (about 28 km) and UTC days. A band-day is tremor-active if it has 10 or more tremor windows (4.9% of band-days). Variants: 50 or more windows (strong, 1.7%); 10 or more on both the day before and the day after (excludes same-day detections); active day plus the next 14 days; 1-9 windows only.

**Rate ratio.** Indirectly standardised rate ratio (active versus quiet band-days). The strata are band x calendar month, so seasonal and long-term changes in network detection cancel. Only strata with active and quiet days and at least one earthquake contribute. The near/far ratio (difference in differences) divides the near rate ratio by the far rate ratio for the same activity definition. Any day-level factor that affects the whole band thus cancels.

**Null distribution and intervals.** We shifted the complete tremor activity matrix (all bands together) by 1,000 random circular offsets between 180 days and (record length - 180 days). This keeps the along-strike and temporal structure of tremor and the clustering of earthquakes. The p-values are two-sided permutation p-values. The 95% intervals are the observed ratio divided by the 97.5% and 2.5% quantiles of the null ratios.

**Diagnostic tests.**
- Time offsets between each near/far earthquake (M1.0+) and tremor windows within 60 km (`diag_offsets.py`).
- Along-strike displacement: we moved tremor activity by 4 to 24 bands (111-667 km) relative to the earthquakes (`placebo_space.py`).
- Tremor cleaning: we removed tremor windows that start from 5 min before to 30 min after any M1.0+ catalog earthquake within 150 km. As controls, we removed the same windows around the earthquake times shifted by a random 3-30 days, and by a random 2-8 hours (`clean_tremor.py`).
- Event study: major arrivals are the first day with 50 or more windows in a band after 60 or more days without such a day. There are 1,118 arrivals. Expected counts use the band x calendar-year mean daily rate. The placebo moves all arrivals by a common random offset (`eventstudy.py`).
- Magnitudes: Aki-Utsu b-value with magnitudes rounded to 0.1 (Mc = 1.5 and 2.0), and the fraction of M2.5+ events, during and outside ETS, with the same time-shift null (`magnitude_eventstudy.py`).

## Results

### Detection depends on noise
Tremor detections on Saturday and Sunday are 14-21% above the weekly mean (22-30% above the weekday mean). They are 40% less frequent between 08 and 17 local time than at night. They are low from November to February. M1.5+ earthquake counts also have a low winter rate. Thus same-day comparisons need a spatial control. The band x calendar-month strata control the seasonal part.

### Rate ratios (all segments, M1.5+, band x calendar-month strata)

| Tremor definition | Near RR (95%) | p | Far RR | Near/far (95%) | p |
| --- | --- | --- | --- | --- | --- |
| >= 10 windows, same day | 1.30 (1.12-1.53) | 0.002 | 1.34 | 0.97 (0.76-1.30) | 0.82 |
| >= 50 windows, same day | 1.04 (0.82-1.36) | 0.79 | 1.37 | 0.76 (0.52-1.23) | 0.20 |
| >= 10 on day before and day after | 1.11 (0.87-1.47) | 0.37 | 1.33 | 0.84 (0.58-1.35) | 0.33 |
| >= 10, same day + 14 days | 1.08 (0.98-1.19) | 0.11 | 1.06 | 1.01 (0.87-1.18) | 0.91 |
| 1-9 windows only | 1.18 (1.01-1.39) | 0.04 | 1.04 | 1.14 (0.91-1.49) | 0.32 |
| >= 10, M2.5+ | 1.35 (0.93-2.06) | 0.12 | 1.51 | 0.89 (0.49-1.69) | 0.69 |
| >= 50, M2.5+ | 0.48 (0.28-1.02) | 0.06 | 1.45 | 0.33 (0.14-0.97) | 0.05 |

All 88 specifications are in `files/results/results_v2.csv`. The first-pass results with band x year strata are in `results_rate_ratio.csv`. They are similar (near 1.27, far 1.32).

### Tremor cleaning (near, M1.5+, >= 10 windows)

| Tremor record | Near RR (95%) | p |
| --- | --- | --- |
| Original | 1.30 (1.12-1.53) | 0.002 |
| Windows within 30 min / 150 km of earthquakes removed (3.8% of windows) | 1.10 (0.95-1.31) | 0.19 |
| Control: same removal, earthquake times shifted 3-30 days (4.1%) | 1.24 (1.06-1.47) | 0.008 |
| Control: same removal, earthquake times shifted 2-8 hours (4.2%) | 1.13 (0.97-1.33) | 0.11 |

The excess decreased by a similar quantity when we removed windows at the earthquake time and 2-8 hours away. Thus the excess is not specific to tremor that occurs at the time of an earthquake. Earthquake signals in the tremor detector cannot be the full explanation. Within 5 minutes of an earthquake, tremor windows within 60 km were only 7% more frequent than a uniform rate (695 found, 652 expected). Within 1 hour, they were 8% more frequent (8,468 found, 7,825 expected). The excess depends on band-days whose tremor count is near the threshold and on earthquake days.

### Along-strike displacement
When tremor and earthquakes are in the same band, the rate ratios are 1.30 (near) and 1.34 (far). When we moved tremor by 111-667 km, the near ratios had a mean of 1.02 (range 0.79-1.30) and the far ratios a mean of 1.03 (0.83-1.17). When any band on the margin was active, the ratio was 0.99 (near) and 1.06 (far). Thus the same-day link is local in latitude. But it is equally strong 40-100 km across strike from the tremor zone, so it is not specific to the tremor zone.

### Event study around 1,118 major tremor arrivals (M1.5+)

| Window (days) | Near obs/exp | Placebo 95% | Far obs/exp | Placebo 95% |
| --- | --- | --- | --- | --- |
| -30 to -1 | 0.96 | 0.91-1.11 | 1.10 | 0.87-1.20 |
| 0 to 13 | 0.91 | 0.86-1.16 | 0.87 | 0.83-1.33 |
| 14 to 44 | 0.97 | 0.90-1.09 | 1.06 | 0.87-1.20 |
| 45 to 90 | 1.07 | 0.92-1.08 | 1.09 | 0.89-1.14 |

For M2.5+, the near ratio in days 45-90 was 1.19 (placebo 0.83-1.18, p = 0.04). This is one of 16 window tests, and the other near M2.5+ windows were 0.88-0.96.

### Magnitude distribution (near, ETS = tremor day or next 14 days)

| Mc | b during ETS | b outside | Difference (null 95%) | p | M2.5+ fraction ETS / outside | p |
| --- | --- | --- | --- | --- | --- | --- |
| 1.5 | 0.86 (n = 1,419) | 0.89 (n = 2,464) | -0.03 (-0.07 to 0.05) | 0.65 | 12.5% / 12.2% | 0.73 |
| 2.0 | 1.01 (n = 553) | 0.99 (n = 911) | 0.02 (-0.06 to 0.14) | 0.83 | 32.2% / 33.0% | 0.82 |

## Figures

- `files/figures/fig1_map.png`: tremor density, near and far earthquakes.
- `files/figures/fig2_rate_ratios.png`: rate ratios for the main tremor definitions and cleaning controls.
- `files/figures/fig3_alongstrike_placebo.png`: rate ratio when tremor is moved along strike.
- `files/figures/fig4_event_study.png`: earthquake rate around major tremor arrivals with the shifted-arrival placebo range.
- `files/figures/fig5_magnitudes.png`: magnitude distributions during and outside ETS.

## Interpretation

The PNSN tremor catalog and ComCat show a same-day link between tremor and earthquakes along the US Cascadia margin. But the link is equally strong 40-100 km from the tremor zone. It does not occur on strong tremor days or around major ETS arrivals. It becomes small and not significant when we remove a small number of tremor windows on earthquake days. These properties agree with a shared detection or catalog effect at the scale of a day and a latitude band. They do not agree with stress triggering by slow slip. We cannot identify the exact mechanism. Possible causes are station noise or outages that affect both catalogs in one part of the network, and uncatalogued or distant earthquake energy that adds marginal tremor detections.

Our rate result agrees with the null daily-rate result of Bombardier et al. (2026) for northern Cascadia. Our magnitude result does not reproduce their magnitude-distribution change in the US data. But the regions, catalogs and magnitude ranges are different, and the M2.5+ samples are small. Thus our result does not refute their result for Vancouver Island.

## Limitations

- ComCat completeness is about M1.0-1.5 in western Washington and less uniform in Oregon and northern California. Oregon has almost no earthquakes near the tremor zone. Thus most of the information comes from Washington (47-49 N) and the Mendocino area (40-42 N).
- The tremor zone is defined from the tremor catalog. The "near" class includes crustal, interface and intraslab earthquakes. The depth split (20 km) is approximate and we did not use a slab model.
- We did not decluster the earthquake catalog. The time-shift null keeps the clustering. But single sequences can still dominate small samples (see the spikes in the far event-study curve).
- The tremor catalog uses fixed-depth locations and has variable detection over time. We used band x month strata, but daily noise changes are not modelled.
- The analysis used 88 specifications and several diagnostics. We report all of them. We chose the band x calendar-month strata and the near/far control after the first pass showed the far-zone excess. We report this order of work openly. The first-pass results (band x year strata) are also in the bundle.
- The intervals come from the time-shift null. They are approximate, because they assume that the null distribution has the same spread at the observed ratio.

## Reproduction

1. Put the shared tremor CSV at `datasets/pnsn-tremor-v3-20090801-20261108/` (or download it with the URL above and check the sha256).
2. Gunzip `files/raw_comcat/*.csv.gz` into `work/raw/comcat/` (or download it again with the URL above; ComCat changes with time, so a new download can differ a little).
3. Copy `files/code/` to `work/code/` and run `sh work/code/run_all.sh` from the parent directory. Python 3.12.16, numpy 2.5.4, pandas 3.1.1, matplotlib 3.11.2 and pyarrow were used. The full run takes about 1-2 hours on one core. The random seeds are fixed in the scripts.

Output files: `results_v2.csv` (main grid), `results_placebo_space.csv`, `results_clean_W30_R150_days.csv` and `_hours.csv`, `results_eventstudy.json`, `results_magnitude.json`, `null_v2.npz` (null draws for each main-grid specification), and logs in `files/logs/`.

## Provenance

- Campaign job: sci-1107-dell-earth-and-ocean-sciences-69ffe9519a72, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis date: 2026-11-08.

## References

- Bombardier, M., Cassidy, J. F., Dosso, S. E. (2026). Does episodic tremor and slip influence seismicity in northern Cascadia? Seismica 5(1). doi:10.26443/seismica.v5i1.1953
- Vidale, J. E., et al. (2011). Tiny intraplate earthquakes triggered by nearby episodic tremor and slip in Cascadia. Geophysical Research Letters. https://pubs.usgs.gov/publication/70036383
- Wech, A. G., Creager, K. C. (2008). Automated detection and location of Cascadia tremor. Geophysical Research Letters 35, L20302. doi:10.1029/2008GL035458
- Wech, A. G. (2010). Interactive tremor monitoring. Seismological Research Letters 81(4), 664-669. doi:10.1785/gssrl.81.4.664
- PNSN tremor API: https://tremorapi.pnsn.org ; USGS ComCat: https://earthquake.usgs.gov/fdsnws/event/1/
