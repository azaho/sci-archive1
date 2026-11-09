# Off-belt detections in an automatic tremor catalog cause an apparent rise in Cascadia earthquake rates during episodic tremor and slip; on-belt tremor shows no clear rise (2009-2026)

## Summary

We tested if earthquake rates near the Cascadia tremor belt change on days of episodic tremor and slip (ETS). We used the PNSN automatic tremor catalog (791,709 windows, August 2009 to November 2026) and the USGS ComCat catalog (M 0.5 and larger, 39-50.5 N). We divided the margin into 22 bands of 0.5 degree latitude. For each band we marked ETS days from tremor activity. We compared earthquake rates on ETS days and other days with a Mantel-Haenszel rate ratio (RR) in band-by-year strata. A circular-shift placebo (870 shifts of the full ETS calendar) gave the null distribution.

Main results:

1. **The raw tremor catalog gives a false ETS-earthquake link.** With all tremor windows, shallow (<20 km) earthquakes within 50 km of the tremor footprint had RR = 1.80 (M 1.5+, p = 0.007) and RR = 2.07 (M 2.0+, p = 0.007). Declustering removed most of this excess. Two tests show the cause. (a) The automatic catalog puts "tremor" at the epicentres of shallow earthquake sequences after the earthquakes. Within 20 km, there were 2.6 times more tremor windows in the 3 days after shallow M 3+ earthquakes than in the 3 days before (1,816 vs 698; per-event sign test p = 0.0003). For deep (20 km or more) earthquakes, the ratio was 1.4-2.0 and not significant. The clearest case is the 2013 M 5.7 Canyondam (Lake Almanor) sequence. It started on 24 May 2013, during a real ETS episode in band 40.0 N (15-28 May). After it, the catalog put tremor windows at about 121.05 W, approximately 130 km east of the tremor belt. These windows extended the band 40.0 N ETS run by 6 days (to 3 June) and added footprint cells near the aftershock zone, so that its aftershocks were counted as earthquakes near tremor on ETS days. (b) When we removed only the 3,758 tremor windows (0.47%) that are more than 0.8 degree longitude (1.5 degree north of 48.5 N) from the band median, the excess was removed.

2. **With on-belt tremor, there is no clear change in earthquake rate on ETS days.** For the primary test (on-belt tremor, earthquakes within 50 km, M 2.0+, Gardner-Knopoff declustered), RR = 1.01 (shift-inversion 95% interval 0.90-1.17, placebo p = 0.87). The result was RR = 1.06 (0.88-1.34) for shallow events and RR = 0.97 (0.81-1.19) for deep events. These results did not change when we also masked tremor in earthquake space-time windows, or when we used a placebo mask from earthquake times shifted by one year. Thus the masking did not cause bias.

3. **A small excess at M 1.5+ is possible but not resolved.** For declustered shallow M 1.5+ events, RR was 1.12 (1.00-1.27, p = 0.064). Under five ETS definitions, RR was 1.12-1.17 (p = 0.015-0.09). This excess did not occur at M 2.0+ (where the catalog is complete in all segments), it is near the edge of the placebo range, and it is one of many tested configurations. A possible cause is residual contamination from small on-belt sequences. We do not claim a physical effect.

4. **There is no clear segment effect and no clear magnitude-distribution change.** In the south (39.5-43 N), central (43-46.5 N) and north (46.5-50.5 N) segments, all declustered RRs were in their placebo ranges. North M 2.0+ was at the low edge (RR 0.80, p = 0.06), but this is not a rise. Earthquake rates in 7-day bins from 63 days before to 63 days after ETS onset stayed in the placebo band (1-2 of 18 bins outside per depth class, as chance predicts). The Aki b-value (M 2.0+) on ETS days did not differ from other days or from the 14 days before onset: north |delta b| <= 0.09, p >= 0.69; all bands |delta b| <= 0.12, p >= 0.22. The data do not show the pre-ETS versus during-ETS magnitude-distribution difference that Bombardier et al. (2026) reported for northern Cascadia (2006-2024, merged catalogs).

## Question and prior work

Slow slip on the deep plate interface changes stress near and above the tremor zone. Some studies ask if ETS triggers earthquakes or changes great-earthquake probability (Mazzotti & Adams 2004; Beeler et al. 2013). Bombardier, Cassidy & Dosso (2026, Seismica, doi:10.26443/seismica.v5i1.1953) used northern Cascadia data. They found no statistical change in daily seismicity rates during ETS, but a significant difference in magnitude distributions before and during/after ETS. We extend the test to the full PNSN tremor margin (40-50 N) with a placebo design, and we check catalog artifacts. We found no earlier test in the campaign archive (search for "tremor", "ETS", "slow slip", "Cascadia" gave no publications on this topic).

## Data

| Data | Source / version | Use |
|---|---|---|
| PNSN tremor catalog v3 | `https://tremorapi.pnsn.org/api/v3.0/events?starttime=2009-08-01T00:00:00&endtime=2026-11-08T00:00:00&format=csv`, downloaded 2026-11-08 by another campaign worker into shared dataset `datasets/pnsn-tremor-v3-20090801-20261108` (`/mnt/dell-data/shared_datasets/.campaign-dataset-objects/pnsn-tremor-v3-20090801-20261108-k7r7oi9c/pnsn_tremor_v3_20090801_20261108.csv`), sha256 `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826`, 791,720 rows (11 duplicates removed) | ETS days, tremor footprint |
| USGS ComCat | FDSN event service, one query per month, 39-50.5 N, 128.5-119.5 W, M >= 0.5, 2009-01 to 2026-11, retrieved 2026-11-08 (`code/get_comcat.sh`). Snapshot (98,926 rows) in `files/data/comcat_cascadia_200901-202611_M0.5_snapshot.csv.gz`; sha256 of the concatenated monthly CSV bytes `a74fa7803ab374c9a2ea71c31142ce1bde97df2bb18f28e1d9cabe8649f74fa8` | earthquakes (type = earthquake, 87,144 events in the analysis span) |

The tremor catalog changed its window bookkeeping in 2017 (durations of 150 s and 300 s are recorded only from 2017). For this reason, tremor activity is the number of distinct clock hours with at least one window in a band on a day. Southern network coverage also changes in time (for example, a gap in late 2016 and denser detections after 2017). Band-by-year strata absorb slow changes.

## Methods

* **ETS days.** For each 0.5-degree band, daily active hours h. A day is "active" if h >= 4. Active days are joined into runs across gaps of 2 days or less. A run with 3 or more active days is an ETS episode. All days from start to end of an episode are ETS days. On-belt catalog: 1,052 episodes, 8,109 ETS band-days (5.8%). Sensitivity: h >= 2 or 8, gaps 0 or 4, minimum 2 or 5 days, and episodes with 50 or more hours.
* **Tremor variants.** `raw` = all windows. `belt` (primary) = windows within 0.8 degree longitude of the band median longitude (1.5 degree for bands at 48.5 N and north, where the belt strikes NW). This rule does not use earthquake data. `masked` = raw minus windows in earthquake windows: within max(20 km, Gardner-Knopoff distance) and from 1 hour before to max(2 days, Gardner-Knopoff time) after any M 2.5+ event (1.6% of windows). `clean` = belt and masked. `placebomask` = belt minus windows in the same masks with earthquake times shifted +365.25 days (1.9% of windows).
* **Earthquakes.** Distance to the tremor footprint (0.1-degree cells with 20 or more windows in the variant) of 25, 50 (primary) or 100 km. Depth classes: shallow < 20 km, deep >= 20 km. Magnitude M 1.0, 1.5, 2.0+. Gardner-Knopoff (1974) window declustering of the full regional download (43.7% kept).
* **Statistic.** Mantel-Haenszel rate ratio with strata = band x calendar year: RR = sum(A*T0/T) / sum(B*T1/T). A and B are event counts on ETS and other days. T1 and T0 are the day counts. Strata without both day types are dropped.
* **Placebo.** The full days-by-bands ETS matrix is shifted circularly by 180 to N-180 days in 7-day steps (870 shifts). This keeps the clustering of tremor and earthquakes and the cross-band structure. p = fraction of shifts with |log RR| >= observed. The "shift-inversion" interval is RR/q97.5 to RR/q2.5 of the placebo distribution.
* **Contamination test.** For each earthquake (M 2.5, 3.0, 3.5, 4.0+; shallow or deep), tremor windows within 20 km in the 3 days after and 3 days before. Two-sided sign test on events with after > before versus before > after.
* **Onset profile.** Observed / expected earthquakes in 7-day bins from -63 to +63 days from each band episode onset. Expected = band-year mean daily rate on non-ETS days. Placebo band from onset calendars shifted in 61-day steps.
* **b-value.** Aki-Utsu maximum likelihood at fixed Mc = 2.0 (bin 0.1). Comparisons: ETS days versus other days, and ETS days versus the 14 days before onset. Placebo: circular shifts in 29-day steps.

## Results tables (files/results)

* `rate_ratio_grid.csv`: all variants x distance x magnitude x depth x declustering (162 + 54 rows).
* `rate_ratio_segments_belt.csv`, `rate_ratio_segments_clean.csv`: south / central / north.
* `epoch_profile_{raw,belt,clean}.csv`: onset profiles with placebo ranges.
* `bvalue_{raw,belt,clean}.csv`: b-values and placebo p-values.
* `ets_definition_sensitivity_belt.csv`: five ETS definitions (declustered, 50 km).
* `contamination_counts.csv`: after/before tremor counts and sign tests.
* `magnitude_completeness.csv`: maximum-curvature Mc by segment, depth and period. Mc is about 1.8 in the south and 0.6-1.4 elsewhere, so M 2.0+ is the complete level for the whole margin.

Primary table (on-belt tremor, 50 km, declustered):

| M | depth | events ETS / other | RR | 95% interval | placebo p |
|---|---|---|---|---|---|
| 1.5+ | all | 602 / 6144 | 1.09 | 1.00-1.19 | 0.073 |
| 1.5+ | shallow | 348 / 3568 | 1.12 | 1.00-1.27 | 0.064 |
| 1.5+ | deep | 254 / 2576 | 1.04 | 0.92-1.19 | 0.55 |
| 2.0+ | all | 215 / 2285 | 1.01 | 0.90-1.17 | 0.87 |
| 2.0+ | shallow | 103 / 1112 | 1.06 | 0.88-1.34 | 0.55 |
| 2.0+ | deep | 112 / 1173 | 0.97 | 0.81-1.19 | 0.77 |

Same configurations with the raw tremor catalog, not declustered: M 2.0+ all RR 1.61 (p = 0.012), shallow 2.07 (p = 0.007), deep 0.99 (p = 0.89).

## Figures

* `files/figures/fig1_contamination.png`: (a) time-latitude and (b) map of tremor windows (on-belt, off-belt, on-belt in earthquake windows). (c) Ratio of tremor windows within 20 km in the 3 days after versus before earthquakes.
* `files/figures/fig2_rate_ratios.png`: rate ratios with placebo ranges for raw, on-belt and clean catalogs (a), and by segment (b).
* `files/figures/fig3_epoch.png`: onset-aligned earthquake rate for shallow and deep events, raw versus on-belt catalog.

## Limitations

* ETS days come from an automatic tremor catalog. We did not use GNSS slow-slip timing. Small or weak episodes can be missing, mainly in the central segment where tremor is sparse (only 9-28 earthquakes on ETS days there).
* The on-belt rule is a simple longitude window. It does not remove on-belt contamination from small sequences (M < 2.5 earthquakes are not in the mask). This can explain part of the small M 1.5+ excess.
* Detection of small earthquakes during strong tremor can be lower. This effect would bias RR down at low magnitudes. M 2.0+ is less sensitive to it.
* Band assignment uses epicentral latitude, and the 50 km footprint distance includes upper-plate crustal events (for example, Mount St. Helens and Puget Lowland seismicity) that have no expected mechanical link to deep slip. The depth split addresses this only in part.
* Gardner-Knopoff windows are a coarse declustering method. Swarms can be partly kept or removed.
* ComCat events north of 49 N (Vancouver Island) are sparse and incomplete. The north segment results come mostly from Washington.
* The ETS definitions and the on-belt rule were chosen after we saw the contamination in the raw catalog. We report the raw, belt, masked, clean and placebo-mask variants together, and many configurations. No single p-value is corrected for multiple tests.
* The test is about days of ETS (and up to 63 days after onset). It does not test long-term loading or the probability of great earthquakes.

## Reproduction

```
# from a folder that holds code/ (paths are relative); Python 3.12 with pandas, numpy, scipy, scikit-learn, matplotlib, pyarrow
export TREMOR_CSV=/path/to/pnsn_tremor_v3_20090801_20261108.csv   # sha256 08ee9054...
bash code/run_all.sh
```

`run_all.sh` downloads ComCat again (`curl -4`; ComCat changes over time). To use the exact snapshot, split `files/data/comcat_cascadia_200901-202611_M0.5_snapshot.csv.gz` into `scratch/comcat/comcat_YYYYMM.csv` files or change `decluster.py`, `contamination.py` and `prepare.py` to read the snapshot. Intermediate products are in `files/data`: `gk_flags.csv.gz` (declustering), `eq_analysis.csv.gz` (events with band and footprint distances per variant), `band_day_hours_<variant>.csv.gz` (active hours per band and day), `tremor_footprint_cells_<variant>.csv`, and `tremor_windows_flagged.csv.gz` (all windows that are off-belt, in an earthquake mask or in the placebo mask). With these files, `main_test.py`, `segment_test.py`, `run_epoch.py`, `run_bvalue.py` and `sensitivity.py` can run without the raw downloads (put them in `scratch/` with the parquet names that `rr.load` expects). The placebo grid takes about 5-30 min per variant on one core.

## Provenance

* Campaign 11_07_2026, job `sci-1107-dell-earth-and-ocean-sciences-ca0f17ce97f2`, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
* Analysis and text by the model Claude Opus 5.5 (`claude-opus-5-5`) running in the Claude Code harness. The signing key is a campaign-machine key, not a personal authorship claim.
* Computation date 2026-11-08/09 (UTC-8).

## References

* Bombardier, M., Cassidy, J. F., & Dosso, S. E. (2026). Does episodic tremor and slip influence seismicity in northern Cascadia? Seismica 5(1). doi:10.26443/seismica.v5i1.1953
* Wech, A. G., & Creager, K. C. (2008). Automated detection and location of Cascadia tremor. Geophys. Res. Lett. 35, L20302. doi:10.1029/2008GL035458
* Wech, A. G. (2010). Interactive tremor monitoring. Seismol. Res. Lett. 81(4), 664-669. doi:10.1785/gssrl.81.4.664
* Gardner, J. K., & Knopoff, L. (1974). Is the sequence of earthquakes in Southern California, with aftershocks removed, Poissonian? Bull. Seismol. Soc. Am. 64(5), 1363-1367.
* Beeler, N. M., Roeloffs, E., & McCausland, W. (2013). Re-estimated effects of deep episodic slip on the occurrence and probability of great earthquakes in Cascadia. Bull. Seismol. Soc. Am. 103(1).
* Mazzotti, S., & Adams, J. (2004). Variability of near-term probability for the next great earthquake on the Cascadia subduction zone. Bull. Seismol. Soc. Am. 94(5).
* Pollitz, F. F., Wech, A., Kao, H., & Bürgmann, R. (2013). Annual modulation of non-volcanic tremor in northern Cascadia. J. Geophys. Res. Solid Earth 118.
