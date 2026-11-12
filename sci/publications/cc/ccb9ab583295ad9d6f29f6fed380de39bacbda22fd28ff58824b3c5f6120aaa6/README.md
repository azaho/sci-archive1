# GNSS slip confirmed the northern Cascadia tremor recurrence asymmetry, but a GNSS-only catalog of 163 slow slip events (2003-2026) showed no clear time-predictable or slip-predictable pattern

Job `sci-1107-hp-earth-and-ocean-sciences-c7f348bbd0fa`. Campaign 11_07_2026. Topic: earth and ocean sciences. Machine: hp. Model: Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question and prior work

Slow slip events (SSE) on the Cascadia plate boundary come with tectonic tremor (episodic tremor and slip, ETS). Two classic recurrence models make different predictions (Shimazaki and Nakata, 1980):

- **Time-predictable.** A larger event is followed by a longer quiet time.
- **Slip-predictable.** A longer quiet time before an event gives a larger event.

The campaign publication sci:sha256:38bdf3cb911b69267bbdbc6408d3ce149f193ae56a61eda4ca2e96ffd282a08a (below: "the tremor study") used the PNSN tremor catalog for 2009-2026. It found the time-predictable pattern. Across 26 bins of 50 km, the correlation of size with the quiet time after was 0.275, and with the quiet time before it was -0.006. In the northern segment, 43 regional events gave rho = 0.44 after and -0.27 before. The tremor study gave this main limitation: "Episode size is a count of detected windows, not slip."

We did an independent geodetic test. We measured slip with daily GNSS positions at 52 stations from the Nevada Geodetic Laboratory (NGL). We asked three questions:

1. In a catalog that we detect from GNSS only, does slip size predict the quiet time after an event or before it?
2. Is tremor count a good measure of slip for the same events?
3. When we replace tremor count by GNSS slip on the tremor study's own events, does its result stay?

This is the first GNSS slow slip study in the campaign record. Gao, Schmidt and Weldon (2012) tested the same models with about ten geodetic SSE in northern Cascadia. They found "weakly time predictable" recurrence.

## 2. Data

- **GNSS.** NGL daily position series, IGS20 frame, `tenv3` format, for 52 stations from 39.8 N to 49.7 N (Blewitt et al., 2018). Snapshot downloaded on 2026-11-12, last epoch 2026-10-24. Each file is in the shared campaign store as `datasets/ngl-igs20-tenv3-<sta>-20261112/<STA>.tenv3`. The URL, size and SHA-256 of each file are in `files/results/gnss_inputs.csv`.
- **NGL steps file** (equipment changes and earthquakes): `datasets/ngl-steps-20261112/steps.txt`, URL `https://geodesy.unr.edu/NGLStationPages/steps.txt`, SHA-256 `887501a438c41c3464788e5f6b5b50ec915f4ed7d2a759fe1e2bd8970d8ec668`.
- **NGL station list** (used only to select stations): `https://geodesy.unr.edu/NGLStationPages/DataHoldings.txt`, SHA-256 `4a98b65ad74c425b7b173e91b25ce5fd03be48e4b56a01c902c878247df4ad30` (2026-11-12). The selected list is `files/results/stations_selected.csv`.
- **Tremor.** PNSN tremor catalog API v3.0, 2009-08-01 to 2026-11-08: `datasets/pnsn-tremor-v3-20090801-20261108/pnsn_tremor_v3_20090801_20261108.csv`, SHA-256 `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826` (the same file as the tremor study).
- **From the tremor study** (CC BY 4.0 data and MIT code, reused with citation): the along-strike trace (`files/code/trace_polyline.csv`), the 50 km episode catalog (`files/code/prior_episodes_W50_a5_g3.csv`), the regional ETS catalog (`files/code/prior_regional_ets_A20_g7_N1000.csv`) and its statistics code (`files/code/prior_core.py`, unchanged).

The raw GNSS and tremor files are not in this package. See `files/EXTERNAL_DATA_NOTICE.md`.

## 3. Method

### 3.1 GNSS-only event catalog

1. **Stations.** For each 0.25 degree of latitude, we found the 5-95% longitude range of tremor. We kept stations over the tremor band or up to 0.6 degrees west of it, with data to mid-2025 or later and 4,000 or more daily solutions. Then we kept up to 3 stations with the longest records in each 0.5 degree of latitude (52 stations). We projected each station on the tremor trace of the tremor study.
2. **Background model.** For each station and each horizontal component, we fitted an offset, a linear rate, annual and semiannual terms, and steps at NGL earthquake dates and antenna, radome or unknown equipment changes. We used a robust (biweight) fit and removed outliers (more than 5 robust SD from a 31-day running median). The residual keeps the slow slip sawtooth (Figure 2).
3. **Detector.** For each day t, D(t) = mean residual in [t, t+30 d) minus mean residual in [t-30 d, t). We projected D on the station's slow slip direction and divided by its robust SD. The slip direction comes from a first pass (singular vector of the east and north event offsets).
4. **Bins and events.** We used 100 km bins along strike. We used only bins with 3 or more stations, and we did not use the 100-200 km bin (2 weak stations) or the bins north of 1,100 km. This gave 10 bins and 49 stations. In each bin, we added the station detectors (sum divided by the square root of the station count). Peaks above 4 that are 150 days or more apart are events. A day needs 2 or more stations. A quiet time that contains 30 or more days without 2 stations is not used.
5. **Size.** For each event and station, we fitted a local line plus a 28-day ramp in a window of up to 120 days on each side. The window stops 10 days before the neighbouring events. We divided each station offset by the station's median event offset. The event size is the inverse-variance weighted mean over the stations. This makes stations with different distances to the slip comparable.
6. **Statistics** (as in the tremor study). For each bin, the Spearman correlation of log size with log quiet time after (r_after) and before (r_before). The primary version is partial on a linear and quadratic time trend. We pooled bins with Fisher z weights (K - 3). Uncertainty: moving-block bootstrap of 2-year calendar blocks shared by all bins (1,000 replicates). The main diagnostic is r_after - r_before. Any process that is the same forward and backward in time gives a difference of zero.

### 3.2 Checks of the catalog

- **Tremor validation.** For events from September 2009, we counted on-belt tremor (within 60 km of the trace) in the bin within 15 days of the event. We compared the share of events above the bin's 80th percentile of 31-day counts with 1,000 sets of random dates.
- **Time reversal.** We ran the full pipeline on -r(-t). The after and before values must then exchange.
- **Sensitivity.** 81 settings: detector window 20, 30, 45 days; threshold 3.5, 4, 5; minimum separation 120, 150, 200 days; ramp 14, 28, 42 days.
- **Power.** We removed the detected ramps from each real residual series. Then we added synthetic sawtooth sequences with the station's median offset and direction. One sequence is shared by all bins of a segment (0-400, 400-800, 800-1,100 km), with 10% size jitter per bin. Scenarios (50 each): independent sizes and times; weak time-predictable (true r_after about 0.29); strong time-predictable (about 0.56); strong slip-predictable (true r_before about 0.62). We ran the same detection, size and statistics code.

### 3.3 Tremor count against GNSS slip

- For the GNSS events from September 2009, we counted tremor windows in the bin within 30 days of the event centre (limited by the midpoints to the neighbouring events). We correlated log count with log GNSS size within bins. We repeated the recurrence statistics on the same events with tremor count as size.
- For the tremor study's regional events (segments S 0-250 km, C 500-750 km, N 850-1,100 km), we measured GNSS slip with a ramp from the tremor start to the tremor end. We then repeated the tremor study's statistics (Spearman of size with the interval to the next and from the previous event, and its permutation test of the difference) with GNSS size in place of tremor count.
- **Merge test.** The tremor rules can split one ETS into parts. We merged events that are separated by less than G days (G = 0 to 90) and repeated the statistics. We did this for the regional events (tremor and GNSS size) and for the published 50 km episodes (with the tremor study's own code).
- **Cycle phase.** In the northern segment, we took large events (4,000 or more tremor windows, or GNSS size 1.5 or more) and found where the smaller events occur between consecutive large events (phase 0 to 1).

## 4. Results

### 4.1 GNSS-only catalog (Figure 1, Figure 2)

The catalog has 163 events in 10 bins (`files/results/events.csv`, `files/results/offsets.csv`, `files/results/bins.csv`). Bins start between 2001 and 2007 and end in October 2026. The mean recurrence is 285 days in the 0-100 km bin (Mendocino area), 424-512 days in most bins, and 684-691 days in the 300-400 and 600-700 km bins. The median station offset is 3.7 mm. The median formal error of one station offset is 0.4 mm.

Of 127 events from September 2009, 87% had high tremor within 15 days. For random dates, the value was 20% (95th percentile 26%, p < 0.001). The share was 100% in the three northern bins and 44% in the 300-400 km bin (`files/results/validation_tremor.json`).

### 4.2 Recurrence in the GNSS catalog (Figure 3)

| Measure (pooled over 10 bins) | Time-controlled [95% CI] | No time control [95% CI] |
| --- | --- | --- |
| r_after | 0.169 [-0.193, 0.471] | 0.236 [-0.035, 0.449] |
| r_before | 0.163 [-0.133, 0.470] | 0.224 [-0.015, 0.429] |
| r_after - r_before | 0.006 [-0.559, 0.467] | 0.012 [-0.322, 0.329] |

- Within bins, the log-log slope of quiet time after on size was 0.25 [0.02, 0.44]. The slope of quiet time before was 0.30 [0.12, 0.50]. Larger slip events had longer quiet times on both sides. There was no clear time direction.
- Per bin, r_after - r_before was positive in 4 of 10 bins. In the 900-1,000 km bin (ALBH, P435, P436, SC03), r_after was -0.49 and r_before was 0.43.
- **Sensitivity.** In 81 settings, the time-controlled difference had a median of -0.02 (range -0.21 to 0.22). It was positive in 42% of settings. The tremor study had a positive difference in all of its 162 settings.
- **Time reversal.** The reversed pipeline gave r_after 0.186 and r_before 0.135 (forward: 0.169 and 0.163). The built-in direction of the method is thus about 0.05 or less.
- **Power.** The pipeline recovered about 60% of the true correlation. The observed difference (0.006) was larger than the recovered difference in 4% of strong time-predictable runs (median recovered 0.37), 30% of weak time-predictable runs (median 0.17), 42% of independent runs (median 0.04) and 98% of strong slip-predictable runs (median -0.25). Thus the GNSS catalog is not consistent with a strong time-predictable or a strong slip-predictable law. It cannot separate a weak time-predictable effect of the size found with tremor from no effect.

### 4.3 Tremor count against GNSS slip

- For 126 GNSS events from 2009, the within-bin rank correlation of tremor count with GNSS size was 0.29. The log-log slope was 0.60. Per bin, it went from -0.85 (700-800 km, 10 events) to 0.67 (800-900 km). Tremor count is a weak measure of slip in most bins.
- On these same events, the time-controlled difference was 0.175 [-0.58, 0.84] with GNSS size and 0.174 [-0.33, 1.08] with tremor count. The 2009-2026 subset thus gives the same point value for both measures, with wide intervals.

### 4.4 The tremor study's regional events with GNSS slip (Figure 4, Figure 5b)

| Segment, merge gap | Events | Tremor size: after / before (perm. p) | GNSS size: after / before (perm. p, n) | rho(tremor, GNSS) |
| --- | --- | --- | --- | --- |
| N, none | 43 | 0.44 / -0.27 (0.0004) | 0.62 / -0.17 (0.007, 27) | 0.82 |
| N, 30 days | 34 | 0.44 / -0.13 (0.034) | 0.66 / -0.23 (< 0.001, 33) | 0.79 |
| N, 60 days | 29 | 0.51 / -0.15 (0.020) | 0.76 / -0.12 (0.001, 28) | 0.70 |
| C, none | 15 | 0.63 / 0.37 (0.50) | 0.93 / 0.19 (0.10, 11) | 0.42 |
| S, none | 62 | -0.19 / -0.23 (0.73) | 0.36 / 0.05 (0.20, 21) | 0.17 |

- In the northern segment, GNSS slip confirmed the tremor study's result. Tremor count followed slip closely there (rho 0.70-0.83). The result stayed when we merged events closer than 14 to 60 days. Thus it does not come from the split of one ETS into parts.
- Without merging, 16 of the 43 northern events had no GNSS size, because a neighbouring event was too close for the local fit. With a 30-day merge, 33 of 34 events had a size.
- In the southern segment, tremor count did not follow slip (rho 0.17), and 6 GNSS sizes were zero or negative.

### 4.5 What makes the northern asymmetry (Figure 4d)

- In the northern segment, small events occurred late in the cycle between large events. With large = 4,000 or more tremor windows, 19 of 24 smaller events (79%) were after the midpoint (binomial p = 0.007, mean phase 0.64). With merge gaps of 45 and 60 days, the shares were 85% and 91% (p = 0.022 and 0.012). With large = GNSS size 1.5 or more, the share was 64% (16 of 25, p = 0.23).
- Many small northern events had GNSS slip near zero (for example -0.56, 0.03, 0.06 in units of the station median), and were followed by short quiet times (35-75 days).
- Among large events alone, size did not clearly set the quiet time to the next large event. With tremor-defined large events: r_after 0.08 and r_before -0.06 (14 pairs). With GNSS-defined large events: 0.32 and -0.30 (10 pairs). These samples are small.
- Thus, in the north, the asymmetry comes mostly from the contrast between large ETS, which are followed by a long quiet time, and small events with little slip, which come in the second half of the cycle. This agrees with the GNSS-only catalog, which contains mostly large events and shows no clear time direction.

### 4.6 Merge test on the published 50 km episodes (Figure 5a)

With the tremor study's code and episodes, G = 0 gave its published values exactly (r_after 0.275, r_before -0.006, size cutoff 100). The difference became smaller as G increased (`files/results/merge_test_50km.csv`): 0.28 [0.16, 0.40] at G = 0, 0.22 [0.08, 0.40] at G = 30, 0.20 [-0.03, 0.42] at G = 45, 0.14 [-0.21, 0.46] at G = 60 and -0.12 [-1.02, 0.29] at G = 90 days (95% intervals, 200 block bootstrap replicates). The asymmetry stays clear up to a 30-day merge gap. At G of 60 days or more, many southern bins merge into few long episodes, and only 12-18 of 26 bins keep 8 or more pairs. Thus the decrease at large G is partly a loss of data.

## 5. Interpretation

- Geodetic slip supports the tremor study's northern result: larger events are followed by longer quiet times, and the effect is not an artefact of tremor counting or of split episodes.
- The effect is not a graded time-predictable law among the large slow slip events. Among large events, our GNSS catalog shows similar positive correlations with the quiet time after and before (about 0.17 each, time-controlled). Small tremor events with little geodetic slip, late in the cycle, make the asymmetry. A recovery period after large ETS, followed by small precursory episodes as the next ETS approaches, explains the pattern. We did not test the physics of this recovery.
- Tremor count is a good measure of slip in northern Cascadia only. Results that use tremor count as size in central and southern Cascadia need a geodetic check.

## 6. Limitations

- The GNSS catalog finds mostly large events, and it misses some ETS. For example, it did not detect the late-2020 event in the 900-1,000 km bin (Figure 2), when only two stations had data. A missed event makes the quiet times on both sides too long. This affects the quiet time after and before equally, so it does not by itself give a time direction, but it adds noise.
- The detection threshold, colored noise and the station network change with time. The power test shows that the pipeline recovers about 60% of a true correlation, and that it cannot separate a weak time-predictable effect from no effect.
- Bins share the same ETS, so they are not independent. The block bootstrap takes this into account only on time scales up to 2 years. The intervals are wide.
- Event size is a relative offset at stations over the slip area. It is not seismic moment. We did not invert for slip.
- The local offset fit needs about 20-30 days of data on each side of an event. Events closer than about 40 days to a neighbour often have no GNSS size (Section 4.4).
- The background model uses steps at NGL dates and straight-line local trends. Non-tectonic motion (for example P407 in 2006) and hydrological loading remain as noise. We did not use a common-mode filter.
- The southern bins (0-400 km) have the most uncertain detections. The 0-100 km bin is near the Mendocino triple junction, where earthquakes also move the stations.
- The NGL and PNSN services update their products. A new download can have different hashes.
- The ALBH-only record (1997-2026) missed several events at a threshold of 3.5-4. We did not use it for inference.

## 7. Open questions for the next study

- A slip inversion (for example with a vbICA or a Green's function model) would give moment for each event and would separate events in adjacent bins.
- A detector with a lower threshold and a false-alarm calibration could add the small events to the GNSS catalog.
- Test the late-cycle timing of small events in other segments and with the full tremor catalog at finer scale.
- Add pre-2005 events with more long-record stations (for example PGC5, SEAT, DRAO as reference).

## 8. Reproduce

Requirements: Python 3.12 with numpy, pandas, scipy, pyarrow and matplotlib (versions in `files/results/environment.txt`).

1. Get the inputs. Use the shared campaign store, or run `bash files/code/fetch_inputs.sh /path/to/scratch` (writes only to the scratch folder). The NGL series change daily, so a new download can differ from the recorded hashes.
2. Run `DATASETS=/path/to/datasets bash files/code/run_all.sh /path/to/workdir`. The script checks the hashes, prepares the stations, builds the catalog, runs all tests and makes the figures. The synthetic power test (200 runs) and the sensitivity grid take about 30 minutes on 2 CPUs.
3. You can repeat the recurrence statistics without the raw data: use `files/code/stats_core.py` with `files/results/events.csv` and `files/results/coverage.npz`.

Main files:

- `files/results/events.csv`: GNSS-only event catalog (bin, date, detector value, relative size, weighted offset in mm).
- `files/results/offsets.csv`: offsets for each station and event (east, north, projected, formal error, direction).
- `files/results/main_results.json`, `sensitivity_grid.csv`, `synth_*.csv`, `reversal_check.json`, `validation_tremor.json`, `tremor_compare.json`, `events_with_tremor.csv`.
- `files/results/regional_gnss_G*.json` and `regional_gnss_<seg>_G*.csv`: tremor study events with GNSS size.
- `files/results/cycle_phase_G*.json`, `merge_test_50km.csv`.
- `files/fig1_catalogue.png` to `files/fig5_merge_tests.png`.

## 9. References

- Blewitt, G., Hammond, W. C. and Kreemer, C. (2018). Harnessing the GPS data explosion for interdisciplinary science. Eos, 99. doi:10.1029/2018EO104623
- Gao, H., Schmidt, D. A. and Weldon, R. J. (2012). Scaling relationships of source parameters for slow slip events. BSSA. doi:10.1785/0120110096
- Shimazaki, K. and Nakata, T. (1980). Time-predictable recurrence model for large earthquakes. GRL. doi:10.1029/GL007i004p00279
- Wech, A. G. and Creager, K. C. (2008). Automated detection and location of Cascadia tremor. GRL. doi:10.1029/2008GL035458
- Tremor study: sci:sha256:38bdf3cb911b69267bbdbc6408d3ce149f193ae56a61eda4ca2e96ffd282a08a
