# Tropical cyclone passage did not change shallow earthquake rates within 200 km in global and Japan catalogs

**Job:** sci-1107-dell-earth-and-ocean-sciences-56f720aeae79 · **Campaign:** 11_07_2026 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Account:** claude-andrii · **Model:** claude-opus-5-5 (Claude Opus 5.5) through Claude Code · **Analysis date:** 2026-11-08.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Some studies report that typhoons can trigger fault slip. Liu et al. (2009) found slow-slip events in eastern Taiwan during typhoons. They proposed that the low air pressure decreases the normal stress on faults. Other studies propose that heavy rain increases pore pressure or causes erosion that changes fault stress (Wdowinski et al. 2011, AGU abstract; Steer et al. 2020). These studies use a small number of storms in one region. We did a systematic test with many storms in two catalogs:

1. **Global:** 4,100 tropical cyclones (IBTrACS v04r01, 1980-2026, hourly track points with wind of 34 kt or more) and the USGS ComCat catalog (M 4.5 or more, 1973-2026).
2. **Japan:** 383 cyclones near Japan (1998-2024) and the JMA unified hypocenter catalog (M 2.5 or more, natural earthquakes, October 1997 to 2024).

For each storm, we counted shallow earthquakes (depth 30 km or less) within 200 km of the storm track. We used time windows relative to the time of closest approach. We compared each count with the counts for the same track and calendar dates moved by 1 to 6 years forward and back (year-shifted placebos). This comparison keeps the location, the season and the slow changes in catalog completeness. We removed aftershocks with Gardner-Knopoff windows and kept the first event of each cluster. The rate ratio (RR) is the observed count divided by the mean placebo count. We give 95% intervals from a bootstrap of storm seasons, and two-sided p-values from a test that changes the label of the "observed" year for all storms in a season together.

**Main result.** We found no change in the rate of shallow earthquakes during the passage window (-1 to +1 day) or after the passage (+1 to +10 days and +10 to +60 days) in the two catalogs (six pre-specified tests, all Holm-adjusted p > 0.5):

| Catalog (declustered, depth <= 30 km, <= 200 km) | Window (days) | Observed | Expected | RR | 95% CI | p (label test) |
|---|---|---|---|---|---|---|
| Global ComCat M >= 4.5 | passage (-1, +1] | 61 | 60.2 | 1.01 | 0.76-1.30 | 0.91 |
| Global ComCat M >= 4.5 | after (+1, +10] | 275 | 264.9 | 1.04 | 0.88-1.19 | 0.61 |
| Global ComCat M >= 4.5 | late (+10, +60] | 1,481 | 1,493.9 | 0.99 | 0.91-1.07 | 0.83 |
| Japan JMA M >= 2.5 | passage (-1, +1] | 180 | 178.5 | 1.01 | 0.86-1.15 | 0.91 |
| Japan JMA M >= 2.5 | after (+1, +10] | 843 | 791.4 | 1.07 | 1.01-1.13 | 0.10 (Holm 0.58) |
| Japan JMA M >= 2.5 | late (+10, +60] | 4,368 | 4,339.9 | 1.01 | 0.96-1.05 | 0.82 |

Thus, an increase of more than about 30% (global M 4.5+) or about 15% (Japan M 2.5+) in the two days near the storm passage is not consistent with these data. The small Japan excess at +1 to +10 days is not significant with the label test. It decreases to RR 1.04 (0.97-1.11, p 0.29) when only symmetric placebo shifts are used. It does not occur on land, where rain loading is expected. It is not larger for strong storms (RR 1.01 for wind of 64 kt or more) than for weak storms (RR 1.10).

**Physical predictions that did not occur.** The pressure-unloading hypothesis predicts the largest effect for shallow events on land near the track with a large local pressure drop. The ocean removes most of the load change at sea (inverted-barometer response). We did not see this pattern:

* Japan, land, within 100 km, passage window: RR 0.89 (0.52-1.32), 15 events.
* Japan, land, local pressure deficit of 10 hPa or more (Holland-type profile), passage: RR 0.79 (0.40-1.23).
* Global, land, within 200 km, passage: RR 1.29 (0.23-2.94), only 8 events (no power).
* Deep events (> 70 km, a negative control) gave RR near 1 in all windows.

**Storm noise did not cause missing small events.** Storms increase seismic noise. Thus, a catalog can miss small events during a storm. In Japan, the passage RR for M 2.5-2.9 events was 0.99 (0.78-1.18). We did not see a detection loss at M 2.5.

**An unexplained excess before the closest approach is a coincidence of a small number of storms.** The global declustered catalog had more shallow events 1 to 3 days before the closest approach (RR 1.45, 1.11-1.82, p 0.014; 85 events). We did not pre-specify this window. It is not physically plausible: at that time the storm center is typically about 400-1,800 km away (translation speed 15-25 km/h). It did not occur in Japan (RR 1.02), at 200-400 km, or within 100 km (1.25, p 0.23). It is at sea and in weak storms. The largest contributor is the 2021-03-04 Kermadec M 8.1 sequence two days before Cyclone Niran (6 declustered events; 256 events without declustering). Other coincidences are the 2021-08-14 Haiti M 7.2 earthquake before Storm Grace and the 1991 Pinatubo eruption earthquakes during Typhoon Yunya. Among 65 global stratum-window tests, 4 had p < 0.05. All 4 are in this window and they share the same events. We think that this excess is a chance coincidence. The non-declustered sensitivity analyses (RR 2.35 before and 1.52 during passage) are controlled by these same sequences, and their intervals include 1.

## Interpretation

At the scale of 2-day and 10-day windows and the magnitudes in standard catalogs, tropical cyclones do not cause a general increase in shallow earthquakes. This result agrees with the small size of the stress change. A 950 hPa storm gives a pressure drop of about 1.5 kPa at 100 km from the center. This is similar to solid-Earth tidal stress, and tidal stress changes global earthquake rates by only a few percent or less. The result does not exclude: slow slip and tremor (Liu et al. 2009 used strainmeters); effects in a small number of critically stressed faults; long-term (months to years) effects of extreme rain and erosion, such as Typhoon Morakot in Taiwan (Steer et al. 2020); or effects below about 15% in Japan.

## Methods

* **Tracks.** IBTrACS v04r01 since-1980 CSV, main tracks only. Wind = USA_WIND if present, otherwise WMO_WIND / 0.88. Pressure = WMO_PRES, otherwise USA_PRES. Linear interpolation to 1 h. We keep hourly points with wind >= 34 kt (all NATURE types, including extratropical stages). Each event uses the nearest of these points (closest approach); dt = event time - time of that point.
* **Catalogs.** ComCat: one fdsnws CSV per year, type "earthquake", de-duplicated by id. JMA: record type J, subsidiary flag 1 (natural earthquake), times changed from JST to UTC, M >= 2.5, from 1997-10-01. Blanks in fixed-width numeric fields were read as zeros (left-justified truncated precision). JMA region: 24-46 N, 122-148 E; storms within 400 km of this box. The JMA M >= 2.5 rate is approximately constant after 1998 except for major sequences (2011, 2016, 2024).
* **Declustering.** Gardner and Knopoff (1974) space-time windows. Events are processed in order of decreasing magnitude. Each unassigned event takes the unassigned events in its window (before and after). The first event of each cluster in time ("initiator") is kept. ComCat: 294,099 events to 99,507 initiators. JMA: 407,331 events to 75,099 initiators.
* **Placebos.** The storm time series is moved by k x 365.2425 days, k = +-1 ... +-6. A shift is valid only if the full window is inside the catalog period. For each season we use the shifts that are valid for all storms in that season. Median: 12 placebos per storm. Sensitivity: only symmetric (+k and -k) shifts.
* **Statistics.** RR = sum of observed counts / sum over storms of mean placebo count. 95% CI: 1,000 bootstrap samples of storm seasons. Label test: in each sample, one valid shift per season (including 0) is chosen at random as "observed" for all storms of that season, and the other shifts are placebos; two-sided p compares |log RR - median| with the null distribution (1,000 samples). Holm correction over the six pre-specified tests (2 catalogs x 3 post-arrival windows, primary stratum). All other strata and windows are secondary.
* **Strata.** Distance (<= 100, <= 200, 200-400 km), land or sea (CSR GRACE RL06 0.25-degree land mask), wind at closest approach (>= 64 kt or < 64 kt), magnitude, local pressure deficit (1010 hPa - central pressure) x (1 - exp(-(40 km / r)^1.3)), depth > 70 km control.

## Limitations

* The magnitude thresholds are high (M 4.5 global). Small or slow events, which the earlier Taiwan studies used, are not in this test. We did not have a dense Taiwan or Philippines catalog.
* The global land sample is small (8 events in the passage window). The global result is mostly for earthquakes at sea, where the inverted-barometer response decreases the load change.
* Gardner-Knopoff windows do not remove all aftershocks of very large earthquakes (for example, Kermadec 2021, Tohoku 2011). The season bootstrap and the label test include this residual clustering, but large sequences make the intervals wide.
* We did not use rainfall data. Storm intensity and pressure are proxies. Rain-driven pore-pressure effects with delays longer than 60 days are not tested.
* The pressure profile (radius of maximum wind 40 km, B = 1.3) is a simple assumption for all storms.
* IBTrACS has different agency wind definitions; the 34-kt threshold is approximate.
* The pre-closest-approach excess was found after we looked at the data. We report it but do not interpret it as a physical effect.

## Files

* `files/code/` - analysis scripts (run with `run_all.sh`), `common.py` (distance and Gardner-Knopoff), `epoch.py` (estimator and tests).
* `files/results/rate_ratios.csv` - all strata x windows x catalogs (columns: rr, obs, exp, ci_lo, ci_hi, p_perm, null_lo, null_hi, n_storms, symmetric, primary_test, p_holm).
* `files/results/time_profile_3day.csv` - 3-day rate ratio profile with the 95% range of the label null.
* `files/results/top_contributing_storms.csv` - storms with the most events in the approach and passage windows.
* `files/results/descriptives.json` - sample sizes.
* `files/data/` - derived inputs: hourly tracks, declustered initiator tables, storm-event pair tables for the declustered analyses, JMA raw-file SHA-256 values, and `provenance.json`.
* `files/figures/` - Figure 1 (time profile) and Figure 2 (strata).

## Reproduce

1. ComCat: extract `files/data/raw/comcat_global_m4.5_1973_2026.tar.gz` from SCI bundle sci:sha256:2182948ccf9d3297ee3ca28cdd0204ea9bf8162558495eb3b423983ebea9368c (archive SHA-256 19e97634...bfb0), or download one CSV per year from `https://earthquake.usgs.gov/fdsnws/event/1/query?format=csv&starttime=YYYY-01-01&endtime=YYYY+1-01-01&minmagnitude=4.5&orderby=time-asc&limit=20000`.
2. JMA: download `https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip` for 1998-2024 and `h199710.zip` (the file hashes we used are in `files/data/jma_raw_sha256.csv`).
3. IBTrACS: shared dataset `/mnt/dell-data/shared_datasets/ibtracs-v04r01-since1980-csv-20261108/ibtracs.since1980.list.v04r01.csv` (SHA-256 1fefe594...d581; source NCEI). Land mask: `/mnt/dell-data/shared_datasets/csr-grace-rl06-v02-landmask-20261108/` (SHA-256 65ddd8f3...f3b).
4. Run `bash files/code/run_all.sh RAW_COMCAT_DIR RAW_JMA_DIR IBTRACS_CSV LANDMASK_NC WORKDIR` (Python 3.12, numpy, pandas, pyarrow, xarray, netCDF4, matplotlib). The two declustered pair tables in `files/data/` let you run `05_analysis.py` and `06_figures.py` directly. On the busy campaign host, the full run took about 2 h; most of the time is the 1,000-sample tests.

## References

* Liu, C.-C., Linde, A. T., Sacks, I. S. (2009). Slow earthquakes triggered by typhoons. Nature 459, 833-836. doi:10.1038/nature08042
* Steer, P. et al. (2020). Earthquake statistics changed by typhoon-driven erosion. Scientific Reports 10, 10899. doi:10.1038/s41598-020-67865-y
* Wdowinski, S. et al. (2011). Tropical cyclones and large earthquakes in Taiwan and Haiti (AGU Fall Meeting abstract).
* Gardner, J. K., Knopoff, L. (1974). Is the sequence of earthquakes in Southern California, with the aftershocks removed, Poissonian? BSSA 64, 1363-1367.
* Knapp, K. R. et al. (2010). The International Best Track Archive for Climate Stewardship (IBTrACS). BAMS 91, 363-376. doi:10.1175/2009BAMS2755.1
* Holland, G. J. (1980). An analytic model of the wind and pressure profiles in hurricanes. Monthly Weather Review 108, 1212-1218.
