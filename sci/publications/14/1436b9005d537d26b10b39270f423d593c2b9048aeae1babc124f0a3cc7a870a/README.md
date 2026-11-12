# NHC wind speed probabilities in 2010-2025 were about 1.3 times too low for best-track and buoy 34-kt winds; the model's own wind geometry hides offsetting Pacific, hurricane and post-tropical errors

**Job:** sci-1107-dell-earth-and-ocean-sciences-f47d7c487e7b, campaign 11_07_2026, topic earth-and-ocean-sciences,
machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key and does not claim personal authorship.

## Summary

We tested the operational NHC/CPHC tropical cyclone **wind speed probabilities** (WSP, Monte Carlo model of DeMaria et al.
2009, 2013). We used all 8,683 archived 0.5-degree GIS grids for 2010-2025: the 120-h cumulative probability of 34-, 50- and 64-kt
winds. We compared them with HURDAT2 best-track positions and wind radii (603 storms, Atlantic and eastern/central Pacific,
18.8 million point-cycles). A plan was written and timestamped (FreeTSA) before any comparison (`files/prereg/`). Intervals are
95 % bootstrap intervals over storms. **B** is the frequency bias: observed events divided by the sum of probabilities.
B > 1 means the probabilities are too low.

1. **Pre-registered result (truth = full best-track quadrant sectors, all storm stages):** the probabilities were too low:
   B = 1.31 [1.22, 1.40] (34 kt), 1.44 [1.31, 1.57] (50 kt), 1.28 [1.15, 1.43] (64 kt). By the pre-registered rule
   this is miscalibration. **But H4 failed:** with best-track radii multiplied by 0.8, B = 1.02, 1.12 and 0.99. The result
   therefore depends on the truth geometry, and the geometry effect is as large as the error.
2. **The WSP model does not use the full sectors.** It takes 0.85 x the quadrant radius as the value at the quadrant
   centre and interpolates in azimuth (DeMaria et al. 2009). We found this after we wrote the plan, so the following truths are post hoc.
   With this model-consistent geometry, the totals are calibrated: B = 1.02 [0.95, 1.09], 1.13 [1.03, 1.23],
   1.00 [0.91, 1.11]. The reliability curves are near the diagonal (Fig. 1).
3. **The calibrated totals come from offsetting errors** (model-consistent truth, 34 kt; Fig. 2):
   - eastern/central Pacific B = 0.75 [0.67, 0.86] (too high) against Atlantic 1.15 [1.07, 1.23] (too low);
   - storms below 64 kt at issue time B = 0.89 [0.83, 0.96] against hurricanes 1.15 [1.05, 1.24]. The pre-registered H2
     predicted the opposite order from the NHC error-circle result. **H2 failed, with the reverse direction supported**:
     B(weak)/B(hurricane) = 0.81 [0.75, 0.88] (pre-registered truth) and 0.78-0.89 under all truths;
   - 300-1000 km from the storm B = 0.80 [0.77, 0.84], but beyond 1000 km B = 1.21 [1.09, 1.33]. The far-field excess goes
     away when only tropical/subtropical stages count as truth (0.68 [0.63, 0.74]). It comes from post-tropical wind fields.
4. **Sources (exploratory; Fig. 4).** The sum of WSP probabilities over the grid equals the expected wind-swath size of one
   Monte Carlo realization. B therefore measures swath **size**: track spread moves the swath but does not change its expected
   size. Per storm-cycle, the observed/expected swath ratio followed the official intensity error (Spearman rho = -0.21,
   -0.33, -0.40 for 34/50/64 kt) and not the official track error (rho = 0.09, 0.02, -0.05).
   - Atlantic cycles where the storm stayed tropical for all 120 h were near calibrated (B = 0.95 [0.88, 1.02]). Cycles where
     it became post-tropical or ended were too low (1.23 [1.12, 1.32]; 1.26 when the official intensity error was within 5 kt).
   - Eastern Pacific cycles were too high in every cell: B = 0.68 [0.64, 0.72] when the official intensity error was
     within 5 kt, and 0.70 when the storm stayed tropical. Intensity error and post-tropical stages do not explain this
     excess, so it is an excess of **wind-radius size** for eastern Pacific storms. Eastern Pacific best-track 34-kt radii
     decreased by 7.2 n mi per decade at fixed intensity class (2004-2025); Atlantic radii decreased by 1.3 n mi per decade.
5. **Independent buoy winds (exploratory):** At 83 NDBC moored buoys (98,901 buoy-cycles, 538 storms), measured winds gave a 34-kt bias of B = 1.33 [1.17, 1.49] with the central wind conversion. With the low and high conversion factors, B = 1.11 [0.97, 1.25] and 1.55 [1.37, 1.73]. At the same buoys, the pre-registered full-sector best-track truth counted 1.04 [0.97, 1.13] times the buoy events. The model geometry (0.85 x interpolated radii) counted only 0.76 [0.70, 0.82] times the buoy events. The measured 34-kt winds thus agree with the pre-registered truth, and the model's 0.85 rule under-counts measured 34-kt exposure by about one quarter. At buoy sites, 34-kt WSP were too low for measured winds by about one third (1.1-1.55 with the conversion). Buoy reliability (34 kt): 17.5 % observed in the 5-20 % bin (mean p 10.7 %) and 39.7 % in the 20-40 % bin (mean 28.5 %), but 86 % in the 80-100 % bin (mean 94 %). By basin, 97 % of buoy 34-kt events were at Atlantic-assigned buoy-cycles (7,959 events against 5,804 expected, B = 1.37). Eastern Pacific buoy-cycles had 273 events against 383 expected (B = 0.71, no interval), the same direction as the gridded eastern Pacific result. At 50 and 64 kt, the buoys recorded fewer events than best track (buoy B = 0.85 and 0.49). Buoys are known to under-measure and fail in high winds, so the 50/64-kt buoy test does not decide.

**Conclusion.** For 34-kt winds as measured at buoys, and as drawn by the published best-track radii, the WSP were too low
by about 1.3 times. Most of this gap comes from the model's 0.85 interpolated wind geometry, which covers about one quarter
less area than the measured 34-kt winds. With its own geometry the model is calibrated in total, but only through offsetting
errors. Eastern Pacific wind fields are too large. Atlantic post-tropical wind fields are too small. Hurricanes get too
little and weak storms too much 34-kt area.

Main limitations: (a) truth is a best-track analysis, not a measured wind field. The calibration verdict changes by about
+-30 % with the assumed geometry. The buoy check covers only buoy sites (near US coasts, the Gulf of Mexico, the Caribbean and Hawaii). It depends on a
wind conversion factor (range 1.10-1.19), counts any 34-kt wind within 1000 km of a storm (some may be non-tropical gales),
and is not decisive at 50/64 kt. (b) Truth geometries 2 and 3 were chosen after
the plan. (c) Systems not in HURDAT2 at issue time (potential tropical cyclones, systems that HURDAT2 lists as
post-tropical) were removed with their probability fields: 121 cycles were dropped and 26.9 % of kept cycles lost at
least one component. (d) Grid points are strongly dependent within a cycle and across overlapping cycles. The storm
bootstrap allows for this but treats storms as independent.

## Data and code

| Item | Location |
|---|---|
| Pre-registration and FreeTSA proof | `files/prereg/PREREGISTRATION.md`, `.sha256`, `prereg.tsq`, `prereg.tsr` (timestamp 2026-11-11 14:28:24 UTC) |
| External data, licences and hashes | `files/EXTERNAL_DATA_NOTICE.md`, `files/results/wsp_cycle_files.txt`, `files/results/ndbc_files.txt` |
| Code | `files/code/` (see Reproduction) |
| Aggregate results | `files/results/*.csv`, `files/results/summary.json`, `files/results/storm_cycles_*.parquet` |
| Figures | `files/figures/` |

The WSP grids, HURDAT2, NHC error files and NDBC buoy files are NOAA public-domain data. Raw files are not bundled (about
1.1 GB). The fetch scripts download them again into local scratch. The bundled tables contain our own aggregates
(sums by stratum, bin or storm-cycle) and per storm-cycle swath sums.

## Methods

**Forecasts.** The file `YYYYMMDDHH_wsp_120hrhalfDeg.zip` holds point shapefiles `wsp{34,50,64}knt120hr_halfDeg` with
`PWIND120` (percent). One file covers all active systems (NHC, CPHC, JTWC). Points that are not listed are p = 0 (below
the file floor of about 0.1 %). A cycle with no 50/64-kt layer has p = 0 for that threshold. The domain is longitude
[-180, 0) and latitude [0, 60] on the 0.5-degree grid. Seven files could not be read.

**Truth.** HURDAT2 fixes (including non-synoptic records) were interpolated linearly to 1-h steps. A point is an event for
cycle t0 if it is inside the threshold wind area of an *advised storm* at any hour in [t0, t0+120 h]. An advised storm has
status TD, TS, HU, SD or SS at t0; storms that form later are not truth (WSP does not forecast genesis).
Geometries:
- `sector1.0` (pre-registered primary): full quadrant sectors with the published (maximum-extent) radii, all later stages;
- `sector0.8` and `sector1.2` (pre-registered H4): radii x 0.8 and x 1.2;
- `i85all` (post hoc): 0.85 x radii as quadrant-centre values (45, 135, 225, 315 degrees), interpolated linearly in
  azimuth, all later stages. This is the WSP model geometry (DeMaria et al. 2009);
- `i85trop` (post hoc): as `i85all`, but only hours with TD/TS/HU/SD/SS status. This is close to the DeMaria et al.
  verification, which cut the best tracks to times with official forecasts.

If the maximum wind is at or above the threshold but all radii are 0, the event is the nearest grid point only.

**Matching.** The 34-kt probability field was split into 8-connected components. A component is kept if it has a point
within 150 km of an advised storm position at t0; points of other components are removed. A cycle is dropped if an
advised storm with at least 34 kt has no component (121 cycles). Each point goes to the nearest advised storm (the
bootstrap unit). The strata use the best-track maximum wind at t0 (H2) and the distance from the t0 position (H3).

**Statistics.** B_all = sum of events (including events at p = 0) / sum of p. Reliability uses fixed bins. The Brier
skill score uses the zero forecast as reference: BSS = 1 - sum (p - o)^2 / sum o. It was 0.50, 0.40 and 0.31 for
34/50/64 kt (pre-registered truth). Events at p = 0 were 3.7 %, 3.2 % and 3.2 % of all events. The bootstrap resamples
storms with replacement, 2,000 times.

**Mechanism (exploratory).** `mechanism.py` sums p and events per storm-cycle. It joins the NHC OFCL error files
(mean 12-120 h intensity and track error, forecast minus best track) and counts hours with tropical status in the
window. `mechanism_basin.py` splits by basin, lifetime and intensity-error class. `size_check.py` gives best-track
34-kt radii by year and the near-field bias by basin and year.

**Buoys (exploratory).** NDBC-owned moored buoys at 5-50 N and 180-40 W (no Great Lakes) with 2010-2025 historical standard meteorological files (83 of 85 had usable data). Buoy WSPD (8-min or 10-min mean at about 4 m) was changed to a 10-m 1-min sustained wind: x 1.09 (neutral log profile, z0 = 2e-4 m) x 1.05 (at-sea 10-min to 1-min factor, Harper et al. 2010), so 1.145 in total. Factors 1.10 and 1.19 were kept as bounds. A buoy-cycle was used if wind data covered at least 80 % of the 121 window hours and if no surrounding grid point lay in a removed component. A buoy event is a converted wind at or above the threshold in an hour when the buoy is within 1000 km of an advised storm. WSP at the buoy is the bilinear value of the four nearest grid points. Best-track truth was evaluated at the exact buoy position with each geometry. The bootstrap resamples storms (the storm nearest to the buoy at t0).

## Results tables

**Table 1. Frequency bias B (95 % storm bootstrap) by truth geometry and stratum.** File: `files/results/frequency_bias_strata.csv` (also year by year).

| Stratum | k | sector1.0 (pre-reg.) | i85all (post hoc) | i85trop (post hoc) |
|---|---|---|---|---|
| all | 34 | 1.31 [1.22, 1.40] | 1.02 [0.95, 1.09] | 0.75 [0.71, 0.79] |
| all | 50 | 1.44 [1.31, 1.57] | 1.13 [1.03, 1.23] | 0.88 [0.82, 0.93] |
| all | 64 | 1.28 [1.15, 1.43] | 1.00 [0.91, 1.11] | 0.87 [0.81, 0.94] |
| Atlantic | 34 | 1.48 [1.38, 1.58] | 1.15 [1.07, 1.23] | 0.79 [0.74, 0.83] |
| Atlantic | 50 | 1.62 [1.46, 1.77] | 1.27 [1.14, 1.39] | 0.91 [0.84, 0.98] |
| Atlantic | 64 | 1.44 [1.26, 1.62] | 1.11 [0.98, 1.26] | 0.93 [0.84, 1.02] |
| E/C Pacific | 34 | 0.96 [0.85, 1.11] | 0.75 [0.67, 0.86] | 0.67 [0.64, 0.71] |
| E/C Pacific | 50 | 1.03 [0.94, 1.13] | 0.81 [0.74, 0.89] | 0.79 [0.73, 0.84] |
| E/C Pacific | 64 | 0.94 [0.86, 1.03] | 0.76 [0.69, 0.82] | 0.75 [0.69, 0.81] |
| t0 wind < 64 kt | 34 | 1.17 [1.09, 1.26] | 0.89 [0.83, 0.96] | 0.70 [0.67, 0.74] |
| t0 wind < 64 kt | 50 | 1.21 [1.09, 1.34] | 0.93 [0.84, 1.03] | 0.78 [0.72, 0.84] |
| t0 wind < 64 kt | 64 | 1.07 [0.95, 1.22] | 0.83 [0.74, 0.94] | 0.74 [0.67, 0.82] |
| t0 wind >= 64 kt | 34 | 1.45 [1.33, 1.56] | 1.15 [1.05, 1.24] | 0.79 [0.75, 0.84] |
| t0 wind >= 64 kt | 50 | 1.60 [1.44, 1.76] | 1.27 [1.14, 1.40] | 0.94 [0.88, 1.00] |
| t0 wind >= 64 kt | 64 | 1.39 [1.23, 1.57] | 1.09 [0.97, 1.23] | 0.94 [0.87, 1.02] |
| < 300 km from t0 position | 34 | 1.16 [1.15, 1.18] | 0.93 [0.92, 0.95] | 0.93 [0.91, 0.95] |
| < 300 km from t0 position | 50 | 1.21 [1.18, 1.24] | 0.95 [0.93, 0.97] | 0.95 [0.92, 0.97] |
| < 300 km from t0 position | 64 | 1.17 [1.11, 1.23] | 0.92 [0.88, 0.97] | 0.92 [0.88, 0.96] |
| 300-1000 km | 34 | 1.04 [1.00, 1.09] | 0.80 [0.77, 0.84] | 0.76 [0.73, 0.80] |
| 300-1000 km | 50 | 1.13 [1.07, 1.20] | 0.90 [0.85, 0.95] | 0.86 [0.82, 0.90] |
| 300-1000 km | 64 | 1.06 [0.99, 1.13] | 0.84 [0.78, 0.90] | 0.82 [0.77, 0.88] |
| >= 1000 km | 34 | 1.56 [1.41, 1.72] | 1.21 [1.09, 1.33] | 0.68 [0.63, 0.74] |
| >= 1000 km | 50 | 1.75 [1.53, 1.97] | 1.38 [1.20, 1.55] | 0.86 [0.78, 0.94] |
| >= 1000 km | 64 | 1.52 [1.28, 1.77] | 1.17 [1.00, 1.37] | 0.90 [0.80, 1.00] |
| 2010-2017 | 34 | 1.27 [1.15, 1.41] | 0.99 [0.89, 1.09] | 0.74 [0.69, 0.80] |
| 2010-2017 | 50 | 1.44 [1.27, 1.62] | 1.13 [0.99, 1.27] | 0.91 [0.83, 0.98] |
| 2010-2017 | 64 | 1.30 [1.11, 1.51] | 1.02 [0.88, 1.18] | 0.94 [0.82, 1.07] |
| 2018-2025 | 34 | 1.35 [1.22, 1.47] | 1.06 [0.95, 1.15] | 0.76 [0.71, 0.80] |
| 2018-2025 | 50 | 1.44 [1.25, 1.61] | 1.13 [0.98, 1.27] | 0.85 [0.77, 0.91] |
| 2018-2025 | 64 | 1.27 [1.09, 1.46] | 1.00 [0.86, 1.14] | 0.82 [0.75, 0.89] |
| land points | 34 | 1.58 [1.30, 1.90] | 1.10 [0.91, 1.31] | 0.73 [0.61, 0.85] |
| land points | 50 | 1.55 [1.28, 1.89] | 1.12 [0.94, 1.33] | 0.79 [0.64, 0.93] |
| land points | 64 | 1.20 [0.97, 1.45] | 0.83 [0.68, 0.98] | 0.71 [0.56, 0.85] |
| water points | 34 | 1.30 [1.21, 1.38] | 1.02 [0.95, 1.09] | 0.75 [0.72, 0.79] |
| water points | 50 | 1.44 [1.31, 1.56] | 1.13 [1.03, 1.23] | 0.88 [0.82, 0.93] |
| water points | 64 | 1.29 [1.15, 1.43] | 1.01 [0.91, 1.12] | 0.88 [0.81, 0.95] |

**Table 2. Pre-registered radius sensitivity (H4), all strata.**

| k | radii x 0.8 | x 1.0 | x 1.2 |
|---|---|---|---|
| 34 | 1.02 [0.95, 1.08] | 1.31 [1.22, 1.40] | 1.62 [1.51, 1.73] |
| 50 | 1.12 [1.02, 1.22] | 1.44 [1.31, 1.57] | 1.76 [1.61, 1.92] |
| 64 | 0.99 [0.89, 1.10] | 1.28 [1.15, 1.43] | 1.56 [1.40, 1.73] |

**Table 3. Reliability at 34 kt (observed frequency by forecast bin).** File: `files/results/reliability.csv`.

| bin (%) | n point-cycles | mean p | obs. sector1.0 | obs. i85all | obs. i85trop |
|---|---|---|---|---|---|
| 0-5 | 11,286,071 | 0.012 | 0.025 | 0.013 | 0.005 |
| 5-10 | 1,975,894 | 0.071 | 0.098 | 0.058 | 0.027 |
| 10-20 | 1,789,328 | 0.143 | 0.193 | 0.129 | 0.068 |
| 20-30 | 947,786 | 0.245 | 0.336 | 0.245 | 0.149 |
| 30-40 | 625,451 | 0.347 | 0.465 | 0.358 | 0.241 |
| 40-50 | 457,432 | 0.447 | 0.580 | 0.470 | 0.345 |
| 50-60 | 354,711 | 0.548 | 0.681 | 0.573 | 0.456 |
| 60-70 | 285,277 | 0.648 | 0.771 | 0.671 | 0.567 |
| 70-80 | 236,744 | 0.748 | 0.851 | 0.770 | 0.680 |
| 80-90 | 203,615 | 0.848 | 0.915 | 0.859 | 0.787 |
| 90-100 | 469,808 | 0.978 | 0.965 | 0.941 | 0.919 |

**Table 4. Buoy check (exploratory).** B at buoy positions; `ratio` rows give best-track events / buoy events (central conversion). File: `files/results/buoy_summary.csv`, `buoy_reliability.csv`.

| k | truth | events | B or ratio [95 %] |
|---|---|---|---|
| 34 | buoy_c1.10 | 6,885 | 1.11 [0.97, 1.25] |
| 34 | buoy_c1.145 | 8,232 | 1.33 [1.17, 1.49] |
| 34 | buoy_c1.19 | 9,559 | 1.55 [1.37, 1.73] |
| 34 | besttrack_sector1.0 | 8,544 | 1.38 [1.24, 1.55] |
| 34 | besttrack_i85all | 6,214 | 1.00 [0.88, 1.15] |
| 34 | besttrack_i85trop | 5,591 | 0.90 [0.79, 1.03] |
| 34 | ratio sector1.0/buoy_c1.145 | 8,544 | 1.04 [0.97, 1.13] |
| 34 | ratio i85all/buoy_c1.145 | 6,214 | 0.75 [0.70, 0.82] |
| 34 | ratio i85trop/buoy_c1.145 | 5,591 | 0.68 [0.62, 0.74] |
| 50 | buoy_c1.10 | 1,230 | 0.64 [0.49, 0.79] |
| 50 | buoy_c1.145 | 1,629 | 0.84 [0.65, 1.04] |
| 50 | buoy_c1.19 | 1,963 | 1.02 [0.79, 1.27] |
| 50 | besttrack_sector1.0 | 2,602 | 1.35 [1.14, 1.57] |
| 50 | besttrack_i85all | 2,115 | 1.10 [0.91, 1.29] |
| 50 | besttrack_i85trop | 2,048 | 1.06 [0.88, 1.25] |
| 50 | ratio sector1.0/buoy_c1.145 | 2,602 | 1.60 [1.32, 2.04] |
| 50 | ratio i85all/buoy_c1.145 | 2,115 | 1.30 [1.10, 1.61] |
| 50 | ratio i85trop/buoy_c1.145 | 2,048 | 1.26 [1.08, 1.54] |
| 64 | buoy_c1.10 | 305 | 0.39 [0.23, 0.57] |
| 64 | buoy_c1.145 | 381 | 0.49 [0.29, 0.68] |
| 64 | buoy_c1.19 | 472 | 0.61 [0.37, 0.84] |
| 64 | besttrack_sector1.0 | 951 | 1.22 [0.92, 1.63] |
| 64 | besttrack_i85all | 778 | 1.00 [0.75, 1.27] |
| 64 | besttrack_i85trop | 759 | 0.98 [0.72, 1.25] |
| 64 | ratio sector1.0/buoy_c1.145 | 951 | 2.50 [1.70, 4.40] |
| 64 | ratio i85all/buoy_c1.145 | 778 | 2.04 [1.45, 3.39] |
| 64 | ratio i85trop/buoy_c1.145 | 759 | 1.99 [1.40, 3.30] |

**Table 5. Swath-size bias by official intensity error and tropical lifetime (i85all truth, exploratory).** Files: `mechanism_groups_*.csv`, `mechanism_basin_i85all.csv`, `mechanism_correlations_*.csv`.

| group | k | B [95 %] | storms | storm-cycles |
|---|---|---|---|---|
| all | 34 | 1.02 [0.95, 1.09] | 603 | 11519 |
| all | 50 | 1.13 [1.03, 1.23] | 603 | 11519 |
| all | 64 | 1.00 [0.91, 1.10] | 603 | 11519 |
| OFCL Imean < -5 kt | 34 | 1.02 [0.93, 1.11] | 325 | 2175 |
| OFCL Imean < -5 kt | 50 | 1.19 [1.07, 1.32] | 325 | 2175 |
| OFCL Imean < -5 kt | 64 | 1.14 [1.02, 1.30] | 325 | 2175 |
| OFCL |Imean| <= 5 kt | 34 | 1.07 [0.99, 1.15] | 553 | 4689 |
| OFCL |Imean| <= 5 kt | 50 | 1.20 [1.07, 1.33] | 553 | 4689 |
| OFCL |Imean| <= 5 kt | 64 | 1.07 [0.93, 1.23] | 553 | 4689 |
| OFCL Imean > +5 kt | 34 | 0.92 [0.83, 1.01] | 384 | 2351 |
| OFCL Imean > +5 kt | 50 | 0.99 [0.87, 1.11] | 384 | 2351 |
| OFCL Imean > +5 kt | 64 | 0.83 [0.70, 0.94] | 384 | 2351 |
| no OFCL verification | 34 | 1.08 [0.92, 1.33] | 587 | 2304 |
| no OFCL verification | 50 | 1.14 [0.99, 1.30] | 587 | 2304 |
| no OFCL verification | 64 | 0.97 [0.84, 1.12] | 587 | 2304 |
| TC all 121 h | 34 | 0.85 [0.80, 0.91] | 228 | 2928 |
| TC all 121 h | 50 | 0.95 [0.88, 1.02] | 228 | 2928 |
| TC all 121 h | 64 | 0.89 [0.81, 0.97] | 228 | 2928 |
| TC 49-120 h | 34 | 1.09 [1.00, 1.17] | 470 | 4302 |
| TC 49-120 h | 50 | 1.23 [1.09, 1.35] | 470 | 4302 |
| TC 49-120 h | 64 | 1.08 [0.94, 1.25] | 470 | 4302 |
| TC <= 48 h | 34 | 1.11 [1.02, 1.22] | 599 | 4289 |
| TC <= 48 h | 50 | 1.23 [1.08, 1.39] | 599 | 4289 |
| TC <= 48 h | 64 | 1.07 [0.90, 1.25] | 599 | 4289 |
| record ends < 120 h | 34 | 1.00 [0.91, 1.08] | 580 | 6247 |
| record ends < 120 h | 50 | 1.11 [0.99, 1.23] | 580 | 6247 |
| record ends < 120 h | 64 | 0.96 [0.83, 1.12] | 580 | 6247 |

## Pre-registered hypotheses: outcomes

| Hypothesis | Rule | Outcome |
|---|---|---|
| H1 calibration | 95 % interval of B excludes 1 and abs(B-1) > 0.10 | Met for 34, 50 and 64 kt with the pre-registered truth (B 1.31, 1.44, 1.28): probabilities too low |
| H2 weak > hurricane | ratio B(weak)/B(hurricane) > 1, interval excludes 1 (34 kt) | Not supported; the reverse is supported: 0.81 [0.75, 0.88] |
| H3 lead trend | intervals of < 300 km and >= 1000 km bands do not overlap | Met: 1.16 [1.15, 1.18] vs 1.56 [1.41, 1.72] (34 kt); post hoc, the far-field excess is from post-tropical stages |
| H4 radius robustness | H1 direction holds for radii x 0.8 and x 1.2 | Not met for 34 kt (B 1.02 [0.95, 1.08] at x 0.8) or 64 kt (0.99); met for 50 kt (1.12 [1.02, 1.22]) |

## Reproduction

Python 3.12 with numpy, pandas, scipy, geopandas, pyogrio, shapely and matplotlib. With 2 CPUs, the full run takes
about 2-3 hours, plus downloads (about 30 min).

```
mkdir -p work/raw/lists work/derived work/results work/figs && cd work
# 1. archive lists and WSP grids (NHC GIS archive)
for y in $(seq 2010 2025); do curl -4 -s -A "Mozilla/5.0" "https://www.nhc.noaa.gov/gis/archive_wsp.php?year=$y" \
  | grep -oi 'forecast/archive/[0-9]*_wsp_120hrhalfDeg.zip' | sort -u > raw/lists/$y.txt; done
bash code/fetch_wsp.sh                     # -> raw/wsp/YYYY/*.zip; compare with results/wsp_cycle_files.txt
# 2. best track (HURDAT2 files named in EXTERNAL_DATA_NOTICE.md)
python -I code/parse_hurdat.py hurdat2-1851-2025-092326.txt hurdat2-nepac-1949-2025-092926.txt derived/hurdat_fixes.parquet
python -I code/build_footprints.py derived/hurdat_fixes.parquet derived/footprints.pkl
curl -4 -sL -o raw/ne_50m_land.zip https://naciscdn.org/naturalearth/50m/physical/ne_50m_land.zip
python -I code/land_mask.py raw/ne_50m_land.zip derived/landmask.npy
# 3. per-cycle verification and analysis
bash code/run_verify_all.sh                # derived/rows_YYYY.parquet, cycles_YYYY.parquet
python -I code/analyze.py derived results
for t in i85all sector1.0 i85trop; do python -I code/mechanism.py derived ATL_errors.txt EPAC_errors.txt results $t; done
python -I code/mechanism_basin.py results/storm_cycles_i85all.parquet derived/footprints.pkl results/mechanism_basin_i85all.csv
python -I code/size_check.py derived results
# 4. buoys
curl -4 -s -o raw/ndbc/station_table.txt https://www.ndbc.noaa.gov/data/stations/station_table.txt
curl -4 -s -o raw/ndbc/stdmet_index.html https://www.ndbc.noaa.gov/data/historical/stdmet/
python -I code/select_buoys.py raw/ndbc/station_table.txt raw/ndbc/stdmet_index.html derived/buoys.csv derived/buoy_files.txt
bash code/fetch_ndbc.sh
python -I code/buoy_verify.py derived/hurdat_fixes.parquet derived/buoys.csv raw/ndbc/stdmet raw/wsp derived/buoy_ck/a 2010-2017
python -I code/buoy_verify.py derived/hurdat_fixes.parquet derived/buoys.csv raw/ndbc/stdmet raw/wsp derived/buoy_ck/b 2018-2025
python -I code/buoy_merge.py derived/buoy_ck derived/buoy_cycles.parquet
python -I code/buoy_analyze.py derived/buoy_cycles.parquet results
# 5. figures
python -I code/figures.py results figs && python -I code/figure_mechanism.py results figs
```

## Relation to earlier campaign work

This study extends the campaign's verification of public hazard products, for example the NHC error-circle studies
(sci:sha256:d0ccb2101584659f74f0e3f8f0d1b2cadf30cfd26e863e6196b75bd823c7c3c3, sci:sha256:6f21c3dcabb3fbed3337b50cbdf17804a2ef5fef3517a8674d93d2c5319e8bde) and the NHC genesis-probability test (sci:sha256:dfcaee13573a2a1761068c668acd60702339bff10b9132ac4d40f4adb3c8e40e).
It reports a new product (WSP) and identifies the sources of its errors. As in the ShakeAlert result in this series,
near-correct totals came from offsetting errors.

## References

- DeMaria, M., et al. (2009): A new method for estimating tropical cyclone wind speed probabilities. Wea. Forecasting 24, 1573-1591, doi:10.1175/2009WAF2222286.1 (https://www.nhc.noaa.gov/pdf/2009waf_wsp.pdf).
- DeMaria, M., et al. (2013): Improvements to the operational tropical cyclone wind speed probability model. Wea. Forecasting 28, 586-602, doi:10.1175/WAF-D-12-00116.1.
- Knaff, J. A., et al. (2007): Statistical tropical cyclone wind radii prediction using climatology and persistence. Wea. Forecasting 22, 781-791, doi:10.1175/WAF1026.1.
- Landsea, C. W., and J. L. Franklin (2013): Atlantic hurricane database uncertainty and presentation of a new database format. Mon. Wea. Rev. 141, 3576-3592, doi:10.1175/MWR-D-12-00254.1.
- Harper, B. A., et al. (2010): Guidelines for converting between various wind averaging periods in tropical cyclone conditions. WMO/TD-No. 1555.
