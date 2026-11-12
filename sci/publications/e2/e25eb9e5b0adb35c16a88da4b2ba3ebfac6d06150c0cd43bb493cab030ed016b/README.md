# Flash-onset US droughts ended sooner than gradual-onset droughts after first D2, and precipitation did not explain the difference

**Job:** sci-1107-dell-earth-and-ocean-sciences-33acaf49c7c0 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), campaign 11_07_2026 · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

A "flash drought" starts fast. In the U.S. Drought Monitor (USDM), a common definition is a two-category increase (for example D0 to D2) in four weeks or less (Chen et al. 2019; Otkin et al. 2018). We asked three questions:

1. After a county first reaches severe drought (D2), does a fast onset predict a shorter remaining drought than a slow onset?
2. If yes, does precipitation explain the difference? We tested precipitation after onset (weather) and precipitation before onset (deficit memory).
3. Does onset speed improve a forecast of drought duration on later years that the model did not see?

Earlier work described USDM drought events and the share of flash droughts (Leeper et al. 2022). We did not find a test of onset speed as a predictor of the remaining duration, with precipitation controls and an out-of-sample check. The campaign record had no flash-drought study. Related campaign results show that runoff, groundwater, GRACE storage and deep soil moisture do not stay low after droughts end (sci:sha256:664b208cefa5e9bb1114a6ccf84255fc886f296b6f72198e385cbc30055fa7af, sci:sha256:d124c3f7b86233dad035f06abfad3634a6d52b5bdd842bd4eefc7f3e0f3ee4e1, sci:sha256:363ebf385701685fa5382e81bf36dccb0271e5bab3f2d5bea44af45c003cd59e, sci:sha256:92d50c68d83a6c447afe82feeeb5fcf409a85e3d0cfcb4a8dfb5696265452ba7). A campaign study of CPC drought outlooks (sci:sha256:10e2d26b1dd31a8e40a1efa2e9878c080f04c14bd316e1c72829139af48bf1c0) used USDM as its verification target. This study looks at the time inside the drought instead.

## Data

- **USDM county statistics** (NDMC, USDA, NOAA, NASA). We used weekly cumulative percent area in D0-D4 for every CONUS county (3,109 counties, 1,402 weekly maps, 2000-01-04 to 2026-11-10). Source: `https://usdmdataservices.unl.edu/api/CountyStatistics/GetDroughtSeverityStatisticsByAreaPercent?aoi=<STATE>&startdate=1/1/<Y>&enddate=12/31/<Y>&statisticsType=1`. We retrieved the files on 2026-11-12. `files/provenance/usdm_fetch_log.json` lists each of the 1,323 URLs with the SHA-256 of the returned bytes. We do not include the raw USDM tables or the county event table (see NOTICE section).
- **CPC Unified Gauge-Based Analysis of Daily Precipitation over CONUS** (NOAA PSL; 0.25 degree; V1.0 for 1991-2006 and RT for 2007-2026). We used the shared campaign copies at `/mnt/dell-data/shared_datasets/noaa-psl-cpc-us-precip-v1-<YYYY>-20261111/`. `files/provenance/precip_and_gazetteer_sources.json` has the source URL and SHA-256 of each file.
- **Census 2020 Gazetteer county file** (internal point of each county), with its URL and SHA-256 in the same provenance file.

## Method

All definitions were fixed before we looked at duration results. The only exception is the later diagnostic checks, which we mark as such.

- **County category.** C = the highest category k (D0 to D4) whose cumulative area is 50% or more, else "none".
- **Event.** A run of weeks at D1 or worse. The event ends at the first week of four consecutive weeks at D0 or better. We kept events that reached D2.
- **Onset weeks (dON).** The number of weeks from the last week at D0 or better to the first D2 week (t2). Classes: flash dON ≤ 4; middle 5-8; gradual ≥ 9. We dropped events with no observed onset (those in drought at the start of the record).
- **Outcome.** R = weeks from t2 to the event end. Every event uses t2 as time zero, so the slow onset of gradual events does not count in R. Events still in drought on 2026-11-10 are right-censored.
- **Precipitation indices.** For each county we averaged the 3x3 CPC cells around the county internal point. A nonparametric SPI-like z compares a window sum with sums for the same county and window that end within ±7 days of the same day of year in 1993-2022. Antecedent windows (28, 91, 182, 365, 730 d) end on the day before t2. Post-onset windows (28, 56, 91 d) start at t2. A weekly SPI series (91, 182, 365 d) gives the first week after t2 at which precipitation returns to normal (z ≥ 0). This is a recovery measure that does not use the USDM.
- **Statistics.** We used Kaplan-Meier medians, Cox proportional-hazards models of drought end (statsmodels PHReg, Efron ties) stratified by NOAA climate region x season of t2 (or finer strata), and logistic models of R ≥ 26 weeks. Intervals are 2.5-97.5 percentiles of a bootstrap that resamples whole calendar years of t2 (27 blocks; 200 draws, or 50 for the finer strata). This keeps the strong spatial dependence of counties in the same drought inside each block. The out-of-sample test fits on t2 in 2000-2012 and scores on t2 in 2013-2026.
- **Sensitivity.** We repeated the analysis with category thresholds of 25% and 75% area, and with end rules of 1 and 8 weeks at D0 or better.

## Results

24,784 county events reached D2 with an observed onset: 13,910 flash, 6,783 middle and 4,091 gradual. 3.7-5.3% were censored.

| Quantity | Flash | Middle | Gradual |
| --- | --- | --- | --- |
| KM median weeks from first D2 to end | 15 (12-18) | 19 (16-24) | 23 (18-28) |
| Share of events with peak D3 or worse | 42% | 47% | 44% |
| Weeks until 91-d precipitation returns to normal | 14 (12-15) | 14 (13-17) | 14 (13-16) |
| Weeks until 365-d precipitation returns to normal | 37 (22-46) | 45 (30-51) | 49 (42-54) |
| KM median weeks from 91-d recovery to USDM end | 7 (5-9) | 9 (6-11) | 12 (9-16) |
| USDM end before 91-d recovery | 38% | 30% | 21% |

1. **Flash-onset droughts ended sooner (Fig. 1).** The gradual-minus-flash difference in median R was 8 weeks (4-12). The Cox hazard ratio (HR) of drought end for flash vs gradual was 1.22 (1.12-1.33). The relation was graded (Fig. 3A). Median R rose from 12 weeks for a one-week onset to 21 weeks for 9-12 onset weeks and 32 weeks for 21-52 onset weeks. Each e-fold increase in dON gave an HR of 0.89 (0.84-0.93). Peak severity was similar in the three classes, so flash droughts were not milder at their peak.
2. **Precipitation after onset did not explain the difference.** Post-onset precipitation was the same in the classes (flash minus gradual 91-d z = +0.06, -0.12 to +0.23). Post-onset rain was the strongest predictor of drought end (HR 1.90 per unit z of 91-d rain). But adding it increased the flash HR to 1.34 (1.24-1.48). In each tercile of post-onset rain, gradual events lasted about 1.5 times longer (dry tercile 42 vs 31 weeks; middle 21 vs 14; wet 11 vs 7).
3. **Precipitation before onset did not explain it either.** Flash events had drier last months (28-d z flash minus gradual -0.52, -0.60 to -0.44). Gradual events had larger 6-12 month deficits (182-d +0.40, 0.27 to 0.53; 365-d +0.24, 0.12 to 0.35). Antecedent 91-, 365- and 730-d z at t2 had HRs near 1, and adding them did not change the flash HR (1.21, 1.10-1.32; with both sets 1.33, 1.23-1.48).
4. **The USDM removed flash droughts sooner after the same rain recovery (Fig. 2).** 91-d precipitation returned to normal after a median of 14 weeks in all classes (difference 0, -1 to +2). After that point, flash events left drought sooner (HR 1.21, 1.11-1.34). The 365-d deficit of gradual events recovered 12 weeks later (2-25). After 182-d recovery, the class difference was not clear (HR 1.05, 0.93-1.18). After 365-d recovery, it was 1.16 (0.90-1.39). So the extra persistence of gradual droughts follows the slow recovery of 6-12 month precipitation deficits that build during the slow onset. It does not follow the deficit size at t2.
5. **The effect was present inside drought episodes, but it was weaker after 2012 (Fig. 3B).** With strata of region x year x season, the flash HR was 1.22 (1.14-1.35). With state x year x quarter it was 1.22 (1.07-1.42), and with region x calendar month 1.33 (1.19-1.50). By period (region x year x season strata), the HR was 1.33 (1.19-1.50) in 2000-2012 and 1.13 (0.99-1.27) in 2013-2026. One-week D0-to-D2 jumps became rare (370 events in 2000-2012, 75 in 2013-2026).
6. **Onset speed gave no out-of-sample forecast gain.** For R ≥ 26 weeks, adding flash to region x season terms changed the 2013-2026 Brier score by +0.00008 (-0.0014 to +0.0016; 12,013 test events). log dON added -0.0005 (-0.0029 to +0.0016). Within year x stratum, Harrell's C of a Cox model with log dON fitted on 2000-2012 was 0.493 (0.472-0.513) on 2013-2026. Unadjusted test-period rates of R ≥ 26 weeks were 26% (flash) and 44% (gradual). The stratum-weighted difference was only -5 percentage points. Most of the crude contrast comes from where and when flash droughts occur.
7. **The effect was regional.** Median R (flash vs gradual) was 13 vs 19 weeks in the South and 13 vs 18 in the Southeast. These two regions supply most events. The Ohio Valley, Northeast, Northern Rockies-Plains and Northwest had differences of 0-4 weeks. In the West the difference was 43 vs 64 weeks, but only 64 flash events. The difference was reversed in the Upper Midwest (24 vs 15) and the Southwest (61 vs 43). Episode level: in 278 region-quarter episodes with 20 or more county events, episodes with more flash onsets were shorter (Spearman -0.29). Within regions the value was -0.12 (-0.29 to -0.01).
8. **Sensitivity.** With the 25% and 75% thresholds and the 1-week and 8-week end rules, the flash HR was 1.19-1.24, the median difference was 7-8 weeks, and the out-of-sample Brier gain stayed at zero.

## Interpretation

Over 2000-2026, fast-onset county droughts in the USDM ended sooner than slow-onset droughts of similar peak severity. Rain after onset did not cause this: it was the same for both classes, and the class difference stayed at equal rain. The deficit size at onset did not cause it either. The data agree best with a memory that the slow onset builds. Gradual droughts collect 6-12 month precipitation deficits, and these deficits need longer to recover. The USDM keeps such droughts after short-term rain has returned. We cannot separate two causes of this memory: slow physical stores (soil water, groundwater, streamflow) and USDM authors' use of long-term indicators. Both are plausible. The effect is real in the pooled record, but it is small in practice. It was weaker after 2012, it differed between regions, and it gave no forecast skill on later years.

## Limitations

- The USDM is an expert blend, not a physical measurement. Its practice changed over time (for example, fewer one-week jumps after 2012). The onset classes partly describe how authors change the map.
- County category uses an area threshold. Large counties in the West mix conditions. We tested 25% and 75% thresholds but not area-weighted grids.
- Precipitation comes from a 3x3 CPC cell mean at one point per county. It is not a county area mean. CPC V1.0 (to 2006) and RT (from 2007) differ in gauge processing. Connecticut planning regions (USDM FIPS 09110-09190) have no gazetteer match, so they have no precipitation indices.
- We did not use temperature, evaporative demand, soil moisture or streamflow. Thus we cannot test heat or storage as the cause of the memory.
- County events in one drought are dependent. Year-block bootstrap intervals cover this but are wide, and the finer-strata runs used only 50 draws.
- Results 4-7 include checks that we added after the first results (meteorological recovery lag, within-episode strata, period split, dose-response bins). Treat them as diagnostic.
- We did not correct for multiple tests.

## Open questions for later work

- Use soil moisture (for example USCRN or SMAP) and USGS streamflow percentiles to test whether physical storage or USDM depiction causes the post-recovery lag of gradual droughts.
- Find out why the effect weakened after 2012. Candidates are new objective blends, author practice, and a different mix of drought types.
- Explain the reversed sign in the Upper Midwest and the Southwest.
- Repeat with a gridded physical flash-drought index (for example a soil-moisture percentile drop) instead of USDM categories.

## Reproduction

`files/code/run_all.sh` runs the full pipeline in an empty scratch folder. It downloads the USDM tables (about 390 MB of CSV), reads the CPC files, and writes `results/` and the figures. Steps: `fetch_usdm.py` → `extract_precip.py` → `spi_weekly.py` → `build_events.py 50 4 main` → `precip_indices.py main` → `analyze.py`, `analyze_met.py`, `oos_check.py`, `within_episode.py`, `dose_response.py` → `run_sensitivity.sh` → `figures.py`. Run time is about 2 h on 2 CPUs; most of it is the bootstrap. The USDM service can revise data, so compare your downloads with the SHA-256 values in `files/provenance/usdm_fetch_log.json`.

### Files

- `files/fig1_persistence.png`, `files/fig2_precip_recovery.png`, `files/fig3_dose_robustness.png`: the figures.
- `files/results/main/`: `results.json` (counts, KM medians, Cox HRs, SPI contrasts, out-of-sample scores), `met_recovery.json`, `oos_concordance.json`, `within_episode.json`, `dose_response.csv`, `km_curves_R.csv`, `median_R_by_region.csv`, `median_R_by_spi_tercile.csv`, `spi_by_class.csv`, `episode_table.csv` (aggregates by region and quarter).
- `files/results/{thr25,thr75,end1,end8}/`: sensitivity results.
- `files/code/`: all code. `files/provenance/`: source URLs and hashes.
- `files/NOTICE-external-data.md`: attribution and terms for external data.

## References

- Chen, L. G., et al. (2019). Flash drought characteristics based on U.S. Drought Monitor. Atmosphere 10, 498. doi:10.3390/atmos10090498
- Otkin, J. A., et al. (2018). Flash droughts: a review and assessment of the challenges imposed by rapid-onset droughts in the United States. BAMS 99, 911-919. doi:10.1175/BAMS-D-17-0149.1
- Leeper, R. D., et al. (2022). Characterizing U.S. drought over the past 20 years using the U.S. Drought Monitor. Int. J. Climatol. 42, 6616-6630. doi:10.1002/joc.7653
- Svoboda, M., et al. (2002). The Drought Monitor. BAMS 83, 1181-1190. doi:10.1175/1520-0477-83.8.1181
- Pendergrass, A. G., et al. (2020). Flash droughts present a new challenge for subseasonal-to-seasonal prediction. Nat. Clim. Change 10, 191-199. doi:10.1038/s41558-020-0709-0
- Chen, M., et al. (2008). Assessing objective techniques for gauge-based analyses of global daily precipitation. JGR 113, D04110. doi:10.1029/2007JD009132
