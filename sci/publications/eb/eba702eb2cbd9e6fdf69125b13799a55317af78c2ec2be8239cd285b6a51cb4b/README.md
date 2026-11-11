# NHC earliest reasonable arrival times of tropical-storm-force winds (2018-2025, 294 storms) came after the observed onset in 14-29% of cases, not 10%; the excess was in large Atlantic storms

## Summary

The National Hurricane Center (NHC) issues two arrival times of sustained tropical-storm-force (34-kt) winds for each grid point with a 5-day wind probability of 5% or more. The "earliest reasonable" time (TOA10) is the time before which the chance of onset is at most 10%. The "most likely" time (TOA50) is the median. The base data also give a most likely (TOD50) and a latest reasonable (TOD90) departure time. We did not find an earlier independent verification of these products.

We wrote a plan before we matched any forecast to an outcome. Then we compared all 6,086 archived Atlantic, eastern and central Pacific 34-kt base-data files of 2018-2025 (313 storms) with the onset and departure of 34-kt winds in the final HURDAT2 best tracks. The test set has 1.14 million (advisory, grid point) cases with an observed onset in the 120-h window (294 storms). A best-track wind radius gives the maximum extent of the wind in a quadrant. Thus, the observed onset time depends on how a radius is changed into an area. We used two area rules: rule P (0.86 times the radius, the rule of the NHC probability model, measured in sci:sha256:9f7a7c98) and rule Q (the full quadrant radius, the NHC definition). We also compared the times in two ways. The issued times are on whole hours. Thus, the second way rounds the observed times to whole hours in the direction that helps the product.

Main results (95% storm-cluster bootstrap intervals):

1. **Onsets came before TOA10 too often.** The share was 0.208 (0.167-0.251) for rule P and 0.287 (0.240-0.331) for rule Q with 10-min observed times. With whole-hour times, it was 0.144 (0.106-0.185) and 0.224 (0.178-0.266). The stated value is 0.10. All four versions exclude 0.10. With equal weight for each storm, rule P with whole-hour times gave 0.105 (0.090-0.122). Thus, the pooled excess comes mostly from storms with many grid points, that is, large storms.
2. **The excess is in large and Atlantic storms.** For a mean 34-kt radius above 70 n mi at the advisory time, the share was 0.17-0.35 in the four versions. For 30 n mi or less, it was 0.06-0.13. Atlantic storms gave 0.17-0.32, eastern Pacific storms 0.04-0.14. In the eastern Pacific, rule P gave a share below 0.10 (TOA10 too early, which is the safe side). This size and basin pattern agrees with the wind speed probability errors in sci:sha256:9f7a7c98 and sci:sha256:79d010f6.
3. **Leads of 12 h or less fail most.** For TOA50 at 12 h or less, the share was 0.35 (rule P) and 0.54 (rule Q) with 10-min times, and 0.14 and 0.35 with whole-hour times. Until 2025, the model had almost no hour-0 spread: less than 0.2% of points with TOA10 at the advisory time had TOA50 more than 1 h later (8.3% in 2026). When the final best-track radius at t0 was more than 5% larger than the operational analysis, the 0-12 h share was 0.49 (rule P, 10-min); when it was more than 5% smaller, 0.26.
4. **The radius part is larger than the track part.** We replaced the official forecast track and 34-kt radii, one at a time, by the best track (onsets to 72 h, 506,040 rule-P cases). Observed onsets came 1.24 h (0.97-1.49 h) before the official deterministic onset on average. Of this, 0.73 h came from the 34-kt radii and 0.51 h from the track. In the Atlantic the parts were 0.93 h (radius) and 0.59 h (track). In the eastern Pacific both were near zero. TOA50 was centred on the official deterministic onset for rule P (mean difference +0.23 h, -0.18 to +0.58 h).
5. **Departures depend on weighting.** Pooled, departures after TOD90 occurred in 0.150 (0.109-0.195) of cases for rule P and 0.184 for rule Q with 10-min times. With equal storm weights it was 0.067 (0.055-0.080). Large storms left late, small storms early. Observed wind duration was longer than the issued median duration by 0.68 h (rule P, -0.00 to 1.49 h) and 1.67 h (rule Q).
6. **2026 check (exploratory).** In 2026 the base data gained hour-0 spread, the same unannounced change found in the 2026 wind speed probabilities (sci:sha256:9f7a7c98). We compared 2026 with 2018-2025 against one truth for all years: the sequence of operational analyses. At 0-12 h the rule-P share fell from 0.34 to 0.22 (10-min times), but the rule-Q share did not fall (0.54 and 0.58), and at 12-24 h the 2026 shares were higher. Thus, the 2026 change did not remove the short-lead excess.
7. **Simple repair (exploratory).** A shift of TOA10 earlier by 0.8-3.3 h, fitted per lead bin on 2018-2023, gave test shares of 0.09-0.17 in 2024-2025 (rule P, 10-min), against 0.16-0.34 for the issued values.

Main limitations: the truth is a best-track wind area, not station data. The verdict size depends on the area rule and on the time rounding; we report all versions. Cases at neighbouring points and advisories are strongly dependent; we resample whole storms. Advisories for potential cyclones that did not form have no best track and are not in the test.

## Figures

- `files/figures/fig1_primary.png`: the four pre-registered shares, all versions.
- `files/figures/fig2_strata.png`: TOA10 share by lead time, size, basin and intensity.
- `files/figures/fig3_sources.png`: timing error decomposition, spread check, and the effect of hour-0 radius analysis error.
- `files/figures/fig4_2026.png`: hour-0 spread by year and the 2026 short-lead check.

## Question and plan

Question: are the NHC arrival and departure times of 34-kt winds calibrated, and if not, which physical or algorithmic parts of the forecast cause the errors?

The plan is `files/plan/PLAN.md`. Git commits record its times (`files/plan/plan_commits.txt`). The plan was committed at 2026-11-11T03:59:36-08:00, before the case builder ran. Before that time we used one advisory (AL092024 advisory 10) only to find the product definition. Three amendments followed:

- A1 (04:08, after a pipeline test on 11 Florence 2018 advisories): tests of hour-0 spread, with the t0 radius difference as a stratifier, and a 2026 check.
- A2 (06:02, after the 2018-2025 primary results, before any 2026 statistic): one truth for the 2026 comparison, because the archive b-decks for 2018-2025 are equal to the final best tracks.
- A3 (06:26, after the primary results): the whole-hour comparison. We added it because the issued values are on whole hours. It decreases all shares. We report it next to the plan version and did not replace the plan version.

## Product definition

The base data `BBSSYYYY_TOA_TOD_34kt_advNNN.grib2` contain four fields on a global 0.5-degree grid (NCEP table 4.2-0-2): 227 TOA10, 228 TOA50, 229 TOD50, 230 TOD90, in UTC epoch seconds. The GRIB2 reference time is the synoptic time t0; NHC releases the advisory about 3 h later. The values are on whole hours after t0. We compared one advisory with the cumulative wind speed probabilities of the same time. Points with a 5-day probability of 5-9% have TOA10 values. Thus, the quantiles are conditional on onset in the 120-h window. Under calibration, for each point, P(onset before TOA10 | onset) = 0.10, P(onset before TOA50 | onset) = 0.50, P(departure after TOD50 | onset) = 0.50, and P(departure after TOD90 | onset) = 0.10.

## Methods

- **Truth.** Best-track centres and 34-kt quadrant radii, linearly interpolated to 10-min steps. Rule Q fills each quadrant to its radius. Rule S interpolates the radius in azimuth between quadrant mid-angles. Rule P is 0.86 times rule S.
- **Cases.** A case is an (advisory, grid point) pair with TOA10, outside the 34-kt area at t0 in both the forecast and the best track, with an observed onset in (t0, t0+120 h]. Departure is the end of the first episode (sensitivity: the last time in the window). A TOD value at the 120-h cap is not tested.
- **Statistics.** Pooled shares, 2,000 storm-cluster bootstrap resamples. Sensitivity runs: equal storm weight, 00 UTC advisories only, land points only (global-land-mask), onsets or TOA10 at least 6 h after the release time.
- **Decomposition.** We used the official forecast (OFCL in the ATCF a-decks) at taus 0-72 h. T(position, radii) is the onset time with the position from B (best track) or O (official), and the radii from B or O. The track and radius parts are the symmetric averages of the two one-at-a-time changes. Their sum is T(B,B) - T(O,O).
- **Operational-analysis truth (2026 check).** The sequence of OFCL tau-0 centres and radii, with a 36-h window. For 2026 we also used the operational b-decks.

## Results tables

| Version | TOA10 share | TOA50 share | TOD50 share | TOD90 share |
| --- | --- | --- | --- | --- |
| Stated | 0.10 | 0.50 | 0.50 | 0.10 |
| Rule P, 10-min | 0.208 (0.167-0.251) | 0.584 (0.537-0.625) | 0.553 (0.506-0.592) | 0.150 (0.109-0.195) |
| Rule P, whole-hour | 0.144 (0.106-0.185) | 0.494 (0.443-0.540) | 0.478 (0.429-0.521) | 0.114 (0.079-0.157) |
| Rule P, 10-min, equal storm weight | 0.174 (0.156-0.193) | 0.518 (0.490-0.546) | 0.407 (0.378-0.435) | 0.067 (0.055-0.080) |
| Rule Q, 10-min | 0.287 (0.240-0.331) | 0.651 (0.608-0.689) | 0.566 (0.527-0.605) | 0.184 (0.140-0.232) |
| Rule Q, whole-hour | 0.224 (0.178-0.266) | 0.582 (0.534-0.623) | 0.505 (0.463-0.546) | 0.151 (0.109-0.196) |

Cases: 1,136,778 (rule P) and 1,370,814 (rule Q) arrivals from 294 storms.

TOA10 share by subset (all four versions):

| Subset | P 10-min | Q 10-min | P whole-hour | Q whole-hour |
| --- | --- | --- | --- | --- |
| All | 0.208 (0.167-0.251) | 0.287 (0.240-0.331) | 0.144 (0.106-0.185) | 0.224 (0.178-0.266) |
| Atlantic | 0.235 (0.185-0.285) | 0.321 (0.267-0.371) | 0.166 (0.120-0.215) | 0.254 (0.203-0.303) |
| Eastern Pacific | 0.085 (0.064-0.111) | 0.135 (0.107-0.170) | 0.040 (0.026-0.059) | 0.086 (0.064-0.114) |
| Radius <= 30 n mi | 0.095 (0.071-0.123) | 0.132 (0.104-0.162) | 0.061 (0.042-0.084) | 0.094 (0.070-0.120) |
| Radius > 70 n mi | 0.247 (0.193-0.307) | 0.346 (0.287-0.405) | 0.173 (0.123-0.231) | 0.274 (0.219-0.330) |
| TOA50 lead 0-12 h | 0.353 (0.329-0.379) | 0.539 (0.515-0.561) | 0.138 (0.118-0.163) | 0.348 (0.322-0.373) |
| TOA50 lead 12-24 h | 0.161 (0.129-0.192) | 0.278 (0.241-0.314) | 0.095 (0.070-0.125) | 0.191 (0.159-0.223) |
| TOA50 lead 72-120 h | 0.229 (0.163-0.288) | 0.280 (0.214-0.334) | 0.193 (0.130-0.251) | 0.244 (0.181-0.297) |
| Land points | 0.201 (0.161-0.239) | 0.311 (0.253-0.370) | 0.131 (0.096-0.163) | 0.250 (0.192-0.307) |

Decomposition (rule P, onset to 72 h; hours, negative means earlier than the official deterministic onset):

| Official onset lead | Cases | Total | Track part | Radius part |
| --- | --- | --- | --- | --- |
| 0-12 h | 95,911 | -0.06 (-0.14 to 0.01) | +0.12 | -0.18 |
| 12-24 h | 96,678 | -0.60 (-0.78 to -0.42) | -0.07 | -0.53 |
| 24-48 h | 176,231 | -1.23 (-1.50 to -0.91) | -0.44 | -0.79 |
| 48-72 h | 137,220 | -2.53 (-3.04 to -2.03) | -1.35 | -1.18 |

The observed onset error spread (median minus 10th percentile, about the official onset) was 1.8, 3.3, 4.5 and 5.5 h in these bins. The issued TOA50 - TOA10 width was 1.0, 3.0, 5.0 and 7.0 h. Thus, the issued spread is too narrow at 0-12 h and wide enough after 24 h; after 24 h the main problem is the early shift (bias), not the spread.

Hour-0 analysis: the final best-track 34-kt radius at t0 was larger than the operational analysis by a factor of 1.018 (1.010-1.026, geometric mean, 4,853 advisories); it was larger in 26% and smaller in 16% of advisories. The median centre difference was 5.8 n mi. With operational-analysis truth instead of final best tracks, the 2018-2025 share at 0-12 h was 0.34 (rule P, 10-min) against 0.35. Thus, post-season best-track changes are not the main cause of the short-lead excess.

Coverage: 10.5% (7.6-13.6%) of all observed rule-P onsets in the window occurred at points that had no timing information (5-day probability below 5%). Under rule Q it was 14.8%. We did not test this share against the 5% threshold, because the 5-day probability of each point is not in the base data.

All values are in `files/results/` (see the file list below).

## Interpretation

The NHC timing model uses the same Monte Carlo realizations as the wind speed probabilities. Thus, it inherits their size error: in large storms the real 34-kt area is larger than the forecast area, so the onset comes earlier and the departure later than the issued times. In small storms and in the eastern Pacific the opposite occurs, and TOA10 is conservative. Until 2025 the realizations had no hour-0 spread, so the 0-12 h interval was too narrow. For a user who reads the NHC radii as maximum extents (rule Q), TOA10 at 0-12 h was after the onset in about half the cases. For users with a low risk tolerance, the earliest reasonable arrival time in large Atlantic storms is not as safe as its definition states.

## Limitations

- Best-track wind radii are analyses, not measurements at each point. Rule P and rule Q are bounds for the real area; the true onset is probably between them.
- The time rounding changes the size of the result (for example 0.208 or 0.144 for rule P). We do not know how the NHC model rounds realization times. The size, basin and short-lead patterns are present in all versions.
- The decomposition uses only cases where all four scenarios reach the point within 72 h. This is a selected subset.
- The 2026 check uses operational analyses as truth and only 35 storms. It is exploratory.
- The repair test uses 2024-2025 only (65 storms) and it was not in the plan.
- Three 2022 files (AL15 advisories 6-8) could not be downloaded. 112 advisories (potential cyclones that did not form, and exercise numbers) have no best track. Western Pacific (JTWC-based) files were not tested.
- The 50-kt files (2020-2025) were downloaded but not verified.

## Reproduction

`files/code/run_all.sh WORKDIR` runs the full analysis in a scratch folder. It downloads the NOAA data (about 10 min), builds cases (about 1.5 h on 2 CPUs) and makes all tables and figures. The Python environment is in `files/code/requirements_venv.txt` (Python 3.12, pygrib 2.1.8, eccodes 2.50, global-land-mask 1.0.0, pandas 3.1.1). `files/results/per_advisory_counts_10min.csv.gz` and `..._hourly.csv.gz` contain, for each storm, advisory, rule, lead bin and land flag, the counts that give every pooled share in this README without new downloads.

Code files: `build_cases.py` (cases), `verify.py` (primary and strata), `ofcl_decomp.py` and `decomp_by_group.py` (decomposition), `explain.py` (hour-0 analysis, spread, duration, repair), `compare_2026.py`, `hour0_spread.py`, `robustness_table.py`, `export_tables.py`, `figures.py`, fetch scripts. `besttrack.py` and `fetch_adeck.py` come from sci:sha256:9f7a7c98 (MIT code); `build_cases.py` adds the TOA matching.

Result files: `results/main34*/` (primary.csv, sensitivity.csv, strata.csv, coverage.csv, per_storm.csv), `results/explain34*/` (t0_radius.csv, f10_by_t0radius.csv, decomp_summary.csv, decomp_by_group.csv, spread_check.csv, duration.csv, recal_test.csv), `results/check2026*/`, `results/robustness.csv`, `results/sample_counts.txt`, `results/hour0_spread_sample.csv`. The suffix `_hourly` marks the whole-hour version.

## Provenance

- Job sci-1107-hp-earth-and-ocean-sciences-3819a1faef18, topic earth-and-ocean-sciences, machine hp, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5), 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.
- NHC TOA/TOD base data: https://ftp.nhc.ncep.noaa.gov/toa/ (2018-2025 year folders and 2026 root), downloaded 2026-11-11. SHA-256 of all 11,815 files: `files/provenance/toa_grib2_sha256.txt.gz`; directory listings: `files/provenance/toa_listings/`.
- HURDAT2: shared datasets `nhc-hurdat2-atl-1851-2025-092326` (https://www.nhc.noaa.gov/data/hurdat/hurdat2-1851-2025-092326.txt, sha256 75202780...) and `nhc-hurdat2-nepac-1949-2025-092926` (sha256 caece626...); full hashes in `files/provenance/hurdat2_sha256.txt`.
- ATCF a-decks and b-decks 2018-2025: https://ftp.nhc.noaa.gov/atcf/archive/YYYY/ (manifest with hashes: `files/provenance/atcf_archive_manifest.csv`). 2026: https://ftp.nhc.noaa.gov/atcf/btk/ and https://ftp.nhc.noaa.gov/atcf/aid_public/ (hashes: `files/provenance/atcf_2026_btk_aid_public_sha256.txt`; these files change during the season).
- External data terms: `files/DATA_NOTICE.md`.
