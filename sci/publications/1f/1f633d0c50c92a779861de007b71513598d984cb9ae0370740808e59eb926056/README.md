# Issued USGS aftershock forecasts for 248 mainshocks (2019-2026) were calibrated after Bayesian updates at depths to 70 km but too high for deeper mainshocks and Guam-Marianas 10 km circles

Job `sci-1107-dell-earth-and-ocean-sciences-b809982ab421`, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** The USGS Operational Aftershock Forecast (OAF) system issues automatic forecasts after earthquakes in the United States and its territories (and, by analysts, after some large foreign earthquakes). It updates each forecast many times during one year. An earlier campaign study (sci:sha256:1bc9d0d0...) tested only a re-computed generic forecast for global M 6+ mainshocks. It did not test the forecasts that USGS issued. We asked: (1) Are the issued forecasts calibrated against the ComCat catalog? (2) Which of the archived model variants (generic, sequence-specific, Bayesian) scores best for the same issue times? (3) Where does the miscalibration come from?

**Data.** ComCat keeps every issued OAF version. We downloaded all 14,454 versions for the 252 mainshocks that have an OAF product (M 3.8-8.8, July 2019 to November 2026; 17 versions were deleted by USGS). Each version gives, for windows of 1 day, 1 week, 1 month and 1 year, the probability of 1 or more events with M >= 3, 4, 5, 6, 7 in a stated search circle. It also gives a 95% count range, count fractiles, and the probability of an event larger than the mainshock. The `forecast_data.json` file of each version also archives the generic, sequence-specific and Bayesian RJ forecasts and flags the issued one. We counted ComCat earthquakes in each circle and window (window end on or before 2026-11-01). We scored only magnitude bins at or above the catalog completeness magnitude (Mcat) that OAF itself used. We wrote the analysis plan (`files/ANALYSIS_PLAN.md`) before we compared a forecast with a count.

**Main results** (O = number of windows with 1 or more events, E = sum of the forecast probabilities; 95% intervals from 2,000 bootstrap samples of mainshocks).

1. **First forecasts were too high.** The first issued version (median 10 minutes after the origin; 85% generic RJ) gave O/E = 0.61 (0.47-0.75) for 247 mainshocks: 190 against 310.
2. **Updated forecasts were calibrated for mainshocks at depths to 70 km.** Over all versions, O/E = 0.97 (0.84-1.10) for 217 such mainshocks (4,458 against 4,573), with 0.91, 0.90, 0.94 and 1.09 for the day, week, month and year windows. The reliability diagram follows the diagonal from probability 0.003 to 0.99 (Figure 1). Alaska (O/E 0.99) and California (1.15) agree.
3. **The Bayesian update gives the calibration.** For the same 153,538 units, the archived generic forecasts gave O/E = 0.63 (0.45-0.83), the sequence-specific forecasts 1.02 (0.79-1.27) and the Bayesian (issued) forecasts 0.97 (0.76-1.19). The Bayesian forecasts had the best Brier score (generic minus Bayesian +0.0024, 95% CI +0.0010 to +0.0040; sequence-specific minus Bayesian +0.0004, -0.0000 to +0.0008) and the best log score.
4. **Forecasts for mainshocks deeper than 70 km were much too high.** There were 31 such mainshocks (12%; 19 Guam-Marianas, 11 Alaska-Aleutians, 1 Colombia). The first forecasts gave 1 window with an event against 35.5 expected (O/E 0.03, 0.00-0.09). All versions gave 45 against 294 (0.15, 0.00-0.36); in 1-day windows 0 against 35.0. The Bayesian update reduced the error but did not remove it (generic 0.09, Bayesian 0.27). All 30 of these mainshocks with archived parameters got the shallow subduction-zone generic parameters (SZ generic or SZ on-shore).
5. **Guam-Marianas counts in 10 km circles failed.** For 31 Guam-Marianas mainshocks at depths to 70 km, all versions gave 12 against 161 (O/E 0.07). OAF used the minimum search radius of 10 km for all of them.
6. **Post-hoc radius check.** When we counted in circles 2 to 3 times wider (with the same issued probabilities), the shallow Guam-Marianas 1-day and 1-week ratios rose to about 1 (1.03 and 0.96 at 3 times). Thus most of that deficit agrees with location scatter of teleseismic epicentres outside a 10 km circle. For deep mainshocks, the 1-day ratio stayed near zero (0.09 at 3 times, 3 against 33.4) and the 1-week ratio stayed below 1 (0.65, 0.33-1.10). Thus deep mainshocks had few early aftershocks, independently of the circle. For other shallow mainshocks, wider circles made the observed counts higher than the forecasts (1-week O/E 1.19 at 2 times).
7. **Time since the mainshock.** Versions issued in the first hour were too high (O/E 0.74 at depths to 70 km), and versions issued more than 90 days after the mainshock were too low (1.41, 1.07-1.88; Figure 4). The RJ model has no background rate, which agrees with the late deficit.
8. **Large events.** For depths to 70 km, the M >= 6 and M >= 7 bins gave O/E 0.61 (0.11-0.87) and 0.59 (0.00-0.78). The probability of an event larger than the mainshock gave 112 against 366 (0.31, 0.09-0.60) over all versions and 9 against 37 for the first versions. Only 8 mainshocks had a larger event inside the circle, and this ratio depended strongly on the radius (1.21 at 2 times for shallow mainshocks outside Guam-Marianas). We do not consider this result robust.

**Conclusion.** For shallow mainshocks, the issued USGS aftershock forecasts became calibrated after the first hours, and the Bayesian combination of the generic and sequence-specific models was the best archived variant. The errors that remain are specific and repairable: (a) the generic parameters are too high for intermediate-depth mainshocks, and USGS issued these forecasts with shallow subduction-zone parameters; (b) a fixed 10 km minimum circle is too small for teleseismically located sequences in the Guam-Marianas region; (c) the first forecasts (generic) are about 1.6 times too high; (d) late forecasts omit background events.

## Figures

![Reliability](files/figures/fig1_reliability.png)

**Figure 1.** Reliability of the issued probability of 1 or more events with M >= m (bins at or above Mcat). Left: first issued version of each mainshock. Right: all issued versions. Blue: mainshock depth 70 km or less. Orange: depth more than 70 km. Bars are 95% bootstrap intervals by mainshock. A calibrated forecast lies on the dashed line. Points on the bottom edge had no event.

![Observed over expected](files/figures/fig2_observed_expected.png)

**Figure 2.** Observed over expected number of windows with 1 or more events, for the main groups. The numbers at the right are O / E.

![Model variants](files/figures/fig3_variants.png)

**Figure 3.** Archived model variants for the same 153,538 units (12,307 versions that archive all three RJ variants). Left: observed over expected. Right: mean Brier score per mainshock minus the Bayesian (issued) variant, times 1,000.

![Lag](files/figures/fig4_lag.png)

**Figure 4.** Observed over expected for all issued versions by the time between the mainshock and the issue of the version.

![Radius check](files/figures/fig5_radius.png)

**Figure 5.** Post-hoc check. Observed over expected when we count events in circles 1, 1.5, 2 and 3 times the issued radius (same center and same issued probabilities), for 231 mainshocks with circles of 60 km or less. In 1-day windows, background events are few; in 1-year windows, a wider circle adds many background events.

## Data

| Input | Source and version | License | In bundle |
| --- | --- | --- | --- |
| OAF products, all versions | ComCat `includesuperseded=true` detail files and product files `forecast.json`, `forecast_data.json`; retrieved 2026-11-10 07:27-07:55 UTC; code versions 1.00.1135 (2019) to 1.06.1876 (2026-07-27) | U.S. public domain (USGS) | No (570 MB raw). SHA-256 of every file: `files/provenance/manifest_sha256.txt.gz`, `forecast_data_sha256.txt.gz`. Derived unit tables: yes |
| ComCat events, M >= 2.5, in a circle that covers all search circles of each mainshock, from 1 day before the mainshock to 2026-11-10 | ComCat FDSN `query?format=csv`, retrieved 2026-11-10 07:42-07:48 UTC; wide circles 08:18-08:38 UTC | U.S. public domain (USGS) | No. SHA-256: `files/provenance/catalog_sha256.txt.gz`, `catalog_wide_sha256.txt.gz`; query bounds `catalog_bounds.json.gz` |

We did not use shared campaign datasets. The shared store had no OAF products and no ComCat files below M 4.5 for these regions. See `files/DATA_NOTICE.md` for attribution.

## Methods

**Scoring unit.** One unit is (issued version, window, magnitude bin). The observed count N is the number of ComCat events of type `earthquake` with preferred magnitude >= m - 0.05 (OAF itself searches from M 2.95 for the M 3 bin), origin time in [timeStart, timeEnd), epicentre inside the circle (center and radius from the version), excluding the mainshock. OAF search depths are -5 to 700 km, so we did not use a depth limit. We used only windows that end on or before 2026-11-01 00:00 UTC.

**Verifiable bins.** We used a bin only if m >= Mcat of that version (`Mcat` in `forecast.json` or `magCat` in `forecast_data.json`). Over all versions, Mcat was 3.5 in 7,671 versions (contiguous USA and most Alaska versions), 4.6 in 3,165 (mostly Guam-Marianas), and mostly 3.0 (1.5-3.5) in California. Results for bins below Mcat are in the tables as secondary results (`*_belowMcat`).

**Sets.** S1: the first issued version of each mainshock (one per mainshock). S2: all issued versions. The units in S2 overlap strongly in time. All intervals come from bootstrap samples of mainshocks, which keeps all versions of one mainshock together.

**Statistics.** O/E of windows with 1 or more events; reliability by probability class; the 95% range coverage; the shares of counts below the 0.025 fractile and above the 0.975 fractile; a randomized PIT from the 197 count fractiles. For the variants, we used the Brier score and the Bernoulli log score of P(N >= 1) (probabilities clipped to 1e-4 and 1 - 1e-4). We took the mean over the units of each mainshock and then the mean over mainshocks.

**Post-hoc analyses (not in the plan).** The region groups (California, Alaska, Guam-Marianas, other), and the radius check (circles 1.5, 2 and 3 times the issued radius for the 231 mainshocks with circles of 60 km or less).

## Further results

* **Count ranges and PIT.** The issued 95% ranges contained 99.4% of the counts. The share above the 0.975 fractile was 0.6% (S2). Most units have a forecast count near zero, and discrete counts make a range include more than 95%; thus this coverage is not a clear sign of too wide ranges. The randomized PIT histograms for shallow mainshocks in S2 were flat (decile densities 0.92-1.18; `files/results/pit_hist.csv`).
* **Bins below Mcat** (secondary). First versions: O/E 0.53 (0.44-0.61); all versions: 0.69 (0.60-0.77), with 0.34 in Guam-Marianas and 0.99 for the contiguous USA. These bins forecast events that the catalog does not record completely, so low ratios are expected.
* **Counting rules.** With M >= m (no 0.05 tolerance), S2 O/E was 0.89 (0.94 shallow). With all event types, the results did not change. Without the versions issued before October 2024, S2 O/E was 0.92 (0.98 shallow).
* **ETAS forecasts.** Ten mainshocks (all versions ETAS, issued for large earthquakes such as Kamchatka 2025 M 8.8 and Myanmar 2025 M 7.7, and for Puerto Rico 2020) gave O/E 0.89 (0.66-1.01) at depths to 70 km. These versions have no archived RJ variants, so we could not compare ETAS with RJ for the same units.
* **Regimes and networks.** `files/results/calibration_table.csv` has all groups. Examples (S2): ACR oceanic boundary 3.06 (1.16-6.30; 41 mainshocks, mostly on and off the coast of Oregon), SZ outer-trench 0.02 (8), SCR generic 0.21 (15), Texas network 3 against 106 (8 mainshocks). These groups are small and post hoc.

## Limitations

* **Circle and catalog.** Calibration is a property of the forecast and the counting rule together. Our rule copies the stated OAF circle, but the OAF circle center can move between versions, and location errors move events across the circle edge. The radius check is post hoc. Wider circles also include background events.
* **Real-time and final catalogs differ.** We used the ComCat catalog of 2026-11-10. OAF fitted its models to the real-time catalog. Late additions, relocations and magnitude revisions can change both N and the issued forecast inputs.
* **Dependence.** The versions of one mainshock overlap, and nearby mainshocks (for example, the Guam-Marianas and Aleutian sequences) are not independent. The bootstrap by mainshock includes the first effect but not the second. Intervals for small groups (deep mainshocks, M >= 7 bins, larger-than-mainshock) are wide.
* **Scope.** Most mainshocks are M 4-6 in US regions; only 12 mainshocks are larger than M 7. The 2019-2024 forecasts are mostly absent from ComCat (only Ridgecrest 2019 and Puerto Rico 2020 remain from before October 2024), so the test covers mainly the automated system from late 2024.
* **Mcat.** We used the Mcat that OAF states. If the true completeness is worse (for example, soon after large mainshocks), observed counts are too low and the forecasts look too high, mainly in the first-hour versions.
* **Two products had invalid JSON** (Kamchatka 2025, trailing commas). We removed the trailing commas before parsing.
* **The probability of an event larger than the mainshock** depends on the circle, and few mainshocks had one; we do not claim a robust result.

## Reproduction

Python 3.12 with numpy, pandas, pyarrow and matplotlib.

```
cd files/code
bash run_all.sh --tables-only     # recompute all tables and figures from files/data (about 5 min)
bash run_all.sh /path/to/scratch  # download everything again (about 1.5 h) and rerun
```

`fetch_oaf.py` and `fetch_oaf_data.py` download all OAF versions; `fetch_catalog.py` and `fetch_catalog_wide.py` download ComCat events; `score_units.py` makes `units.parquet` and `versions.csv`; `event_meta.py` makes `events.csv`; `analyze.py` makes the tables in `files/results`; `radius_check.py` and `radius_tables.py` make the post-hoc radius tables; `figures.py` makes the figures. Bootstrap seed 20261110. A new download can differ because ComCat changes; compare it with the hash lists in `files/provenance`.

## Files

* `files/ANALYSIS_PLAN.md`: plan written before scoring.
* `files/data/units.parquet`: 1,029,922 units (issued and archived variants): event, version, window, bin, Mcat, probability, 95% range, median, 0.025/0.975 fractiles, approximate CDF at N, and counts N (tolerance rule), N_exact, N_all (all event types).
* `files/data/versions.csv.gz` (14,437 issued versions: issue time, model, circle, Mcat, variants, code version), `events.csv` (252 mainshocks: ComCat origin, regimes, generic parameters), `variant_units.parquet` (153,538 paired units), `radius_units.parquet` (post-hoc recounts).
* `files/results/calibration_table.csv`, `reliability.csv`, `pit_hist.csv`, `variant_comparison.csv`, `per_event.csv`, `radius_check.csv`, `radius_check_by_window.csv`, `summary.json`. (`etas_vs_rj.csv` is empty because no ETAS version archives an RJ variant.)
* `files/provenance/`: ComCat OAF event list and SHA-256 lists of all raw files.
* `files/DATA_NOTICE.md`: external data sources and attribution.

## References

* Reasenberg, P. A., and Jones, L. M. (1989). Earthquake hazard after a mainshock in California. Science 243, 1173-1176. doi:10.1126/science.243.4895.1173
* Page, M. T., van der Elst, N., Hardebeck, J., Felzer, K., and Michael, A. J. (2016). Three ingredients for improved global aftershock forecasts. BSSA 106(5), 2290-2301. doi:10.1785/0120160073
* Hardebeck, J. L., Llenos, A. L., Michael, A. J., Page, M. T., and van der Elst, N. (2019). Updated California aftershock parameters. SRL 90(1), 262-270. doi:10.1785/0220180240
* van der Elst, N. J., Hardebeck, J. L., Michael, A. J., McBride, S. K., and Vanacore, E. (2022). Prospective and retrospective evaluation of the U.S. Geological Survey public aftershock forecast for the 2019-2021 Southwest Puerto Rico earthquake and aftershocks. SRL 93(2A), 620-640. doi:10.1785/0220210222
* Schneider, M., Barall, M., Hardebeck, J., Michael, A., Page, M., and van der Elst, N. (2025). Evaluating the forecasting performance of U.S. Geological Survey aftershock forecasts. SSA Annual Meeting abstract (evaluation of a prototype ETAS system with simulated forecasts; no results were in the abstract).
* USGS ComCat, doi:10.5066/F7MS3QZH; USGS OAF overview, https://earthquake.usgs.gov/data/oaf/overview.php
* Campaign work: generic USGS aftershock forecasts for global M 6+ mainshocks (sci:sha256:1bc9d0d0bdeda0f0adac9de2ea154364b1e8d97947499798a2bced60277e210e), which found deep generic forecasts about 4 times too high; PAGER fatality probabilities (sci:sha256:156946e5385f0a25a45be2eb1d8d541e7298c796c636d418b02d0d9d9047d7aa).
