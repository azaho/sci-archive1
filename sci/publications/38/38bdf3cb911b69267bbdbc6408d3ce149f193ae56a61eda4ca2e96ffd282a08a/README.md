# Larger Cascadia tremor episodes were followed by longer quiet times but were not preceded by longer quiet times in 50 km bins of the 2009-2026 PNSN catalog

Job `sci-1107-hp-earth-and-ocean-sciences-fd683feec267`. Campaign 11_07_2026. Topic: earth and ocean sciences. Machine: hp. Model: Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Tectonic tremor in Cascadia occurs in episodes. Large episodes come with slow slip on the plate boundary (episodic tremor and slip, ETS). Between them, smaller episodes occur.

Two classic recurrence models make different predictions (Shimazaki and Nakata, 1980):

- **Time-predictable model.** Failure occurs at a fixed stress level. A larger event releases more stress. Thus a larger event is followed by a **longer** quiet time.
- **Slip-predictable model.** Each event lowers stress to a fixed base level. A longer loading time gives more stress to release. Thus a larger event is preceded by a **longer** quiet time.

Gao, Schmidt and Weldon (2012) used about ten geodetic slow slip events in northern Cascadia. They found "weakly time predictable" and "moderately anti-slip predictable" recurrence. We ask: does the same pattern occur in tremor episodes along the full Cascadia margin over 17 years? We also ask how strong and how stable the pattern is.

## 2. Data

We used one input dataset: the PNSN tremor catalog (API v3.0) from 2009-08-06 to 2026-11-07. It has 791,720 tremor windows of 2.5 minutes, with location and energy. The file is in the shared campaign store:

- Path: `datasets/pnsn-tremor-v3-20090801-20261108/pnsn_tremor_v3_20090801_20261108.csv`
- SHA-256: `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826` (67,459,361 bytes)
- Source URL and retrieval recipe: `files/data_provenance.json`

We do not include the raw catalog in this package. The package includes the derived episode catalog (`files/results/episodes_W50_a5_g3.csv`), which is sufficient to repeat the main statistics.

## 3. Method

1. **Along-strike coordinate.** We fitted a line through the median tremor locations. We gave each tremor window a distance along this line (0 km at 39.9°N, 1,338 km at 50°N on Vancouver Island). Figure 1 (`files/fig1_overview.png`) shows the catalog.
2. **Episodes.** We divided the margin into 26 bins of 50 km. In each bin, a day is "active" if it has 5 or more windows. Active days with gaps of 3 days or less form one episode. Episode size is its number of windows. This gave 5,055 episodes.
3. **Size cutoff.** We used only episodes with size at or above a cutoff *m* (50, 100 or 300 windows; 100 is primary). Smaller events can be undetected or merged, so a cutoff makes the catalog more consistent.
4. **Quiet times.** For each episode, the quiet time BEFORE is from the end of the previous episode to its start. The quiet time AFTER is from its end to the start of the next episode. We used the same bin and the same cutoff.
5. **Statistic.** In each bin, we calculated the Spearman correlation of log size with log quiet time after (r_after) and before (r_before). The primary version is a partial correlation. It removes linear and quadratic time trends and a step at 2017-07-01, because detection improved in the south after 2017 (Figure 1). We pooled bins with Fisher z weights (K - 3).
6. **Asymmetry test.** For any stationary process that is the same forward and backward in time, r_after and r_before have the same expected value. Example: periodic large episodes plus random small episodes. Such a mixture can make r_after positive, but it makes r_before equally positive. Thus **r_after minus r_before** is the main diagnostic. It shows a time direction in the dependence of quiet time on size.
7. **Uncertainty.** Bins share the same large ETS, so they are not independent. We used a moving-block bootstrap in calendar time. Blocks are 2 years long and contain all bins together. We used 500 replicates for the margin-wide values and 300 for the segments.
8. **Checks.**
   - Time reversal of the raw catalog: the method must exchange r_after and r_before exactly.
   - Synthetic catalogs: 200 sets of 26 bins with quasi-periodic large episodes plus Poisson small episodes. One version is time-reversible. One version adds a 60-day period without small episodes after each large episode.
   - Sensitivity: 27 detection settings (bin 25, 50, 100 km; day count 2, 5, 10; gap 1, 3, 7 days), 3 size cutoffs, with and without time control (162 runs).
   - Segment scale: one catalog of regional ETS for each of three separated segments: S (0-250 km, about 40-42°N), C (500-750 km, about 44.3-46.9°N), N (850-1100 km, about 47.6-49.3°N). The rules are: daily count of 20 or more, gap of 7 days or less, and size of 1,000 windows or more.
   - Out-of-sample forecast: a model with one slope shared by all bins predicts log quiet time after from size. Size is measured against the bin's median of the previous 3 years. We trained on 2009-2017 and tested on 2018-2026, and then the reverse. The baseline is the training median of each bin.
   - Kaplan-Meier curves of quiet time after, by size third within each bin.

## 4. Results

### 4.1 Margin-wide, 50 km bins (Figure 2a)

| Size cutoff | Bins | Episode pairs | r_after [95% CI] | r_before [95% CI] | r_after - r_before [95% CI] |
| --- | --- | --- | --- | --- | --- |
| 50 | 26 | 2,054 | 0.205 [0.135, 0.273] | 0.023 [-0.023, 0.066] | 0.182 [0.081, 0.279] |
| **100** | **26** | **1,336** | **0.275 [0.201, 0.363]** | **-0.006 [-0.071, 0.060]** | **0.282 [0.160, 0.428]** |
| 300 | 25 | 599 | 0.368 [0.309, 0.496] | 0.019 [-0.174, 0.107] | 0.349 [0.242, 0.607] |

These values are time-controlled partial correlations. Values without time control are almost the same: for cutoff 100, r_after = 0.269 and r_before = 0.017 (`files/results/main_results.json`). At cutoff 100, r_after is positive in 21 of 26 bins. r_before is positive in 15 of 26 bins.

The within-bin log-log slope of quiet time after on size is 0.25 [0.18, 0.33]. When the size doubles, the following quiet time is about 19% longer. The slope for quiet time before is 0.04 [-0.04, 0.08]. The slope is much less than 1. Thus tremor size gives only a partial measure of the stress that the episode releases.

### 4.2 Recovery curves (Figure 3a)

For episodes in the largest third of sizes, the median quiet time after was 1.36 times the bin median. For the smallest third, it was 0.85 times. At day 90, 49% of bins were still quiet after a large episode. After a small episode, 30% were still quiet. At day 180, the values were 25% and 12%.

### 4.3 Asymmetry against synthetic catalogs (Figure 3b)

- Time-reversible synthetic catalogs gave r_after - r_before = 0.001 ± 0.037 (mean ± SD, cutoff 100). In these catalogs, r_after was positive (0.07 at cutoff 100, 0.25 at cutoff 300), but r_before had the same value. Thus a positive r_after alone does not show time-predictable behaviour.
- The catalog with a 60-day recovery period gave 0.26 ± 0.04. This is near the observed value of 0.25 (no time control).
- The time-reversed real catalog gave r_after = 0.017 and r_before = 0.269. These are the forward values exchanged, so the method has no built-in time direction.

### 4.4 Sensitivity (Figure 2b)

In all 162 runs, r_after was positive (range 0.086 to 0.389). In all 162 runs, r_after was larger than r_before (r_before range -0.095 to 0.106). File: `files/results/sensitivity_grid.csv`.

### 4.5 Segments

At the 50 km bin scale (cutoff 100, time-controlled, `files/results/segments_binlevel.json`):

| Segment | Episodes | r_after [95% CI] | r_before [95% CI] |
| --- | --- | --- | --- |
| S (0-250 km) | 466 | 0.32 [0.24, 0.44] | 0.01 [-0.09, 0.13] |
| C (500-750 km) | 93 | 0.05 [-0.50, 0.41] | 0.25 [-0.15, 0.67] |
| N (850-1100 km) | 272 | 0.35 [0.22, 0.47] | -0.16 [-0.29, -0.06] |

At the segment scale, with regional ETS catalogs (Figure 4, `files/results/regional_results.csv`):

- **N:** 43 events. Size against quiet time after gave rho = 0.44 (p = 0.004). Size against quiet time before gave rho = -0.27 (p = 0.09). A permutation test of the difference gave p < 0.001. With a size cutoff of 2,000 windows (23 events), rho after = 0.74 (p < 0.001) and rho before = -0.16. This agrees with Gao et al. (2012): time-predictable and weakly anti-slip-predictable.
- **C:** 15 events. rho after = 0.63 (p = 0.016) and rho before = 0.37 (p = 0.19). With the 2,000-window cutoff (11 events), rho after = 0.32 (p = 0.37). The result for C is uncertain.
- **S:** The results changed sign with the event rules (rho after from -0.19 to 0.14). At this scale, the high and changing background tremor in the south makes regional ETS unclear. We did not find a segment-scale pattern in S. The 50 km bins in S show the time-predictable pattern.

### 4.6 Forecast value

The size term made the out-of-sample error of log quiet time smaller by only a small quantity (`files/results/forecast_results.json`):

- Cutoff 100, training on 2009-2017 and testing on 2018-2026: 4.2% [0.3, 8.0] smaller mean absolute error. Error became smaller in 10 of 14 bins.
- Reverse direction: 1.2% [-1.4, 3.6].
- Cutoff 50: 4.0% [2.7, 5.7], and -0.1% in reverse.
- Cutoff 300: no gain (-0.2% and -3.8%).

The dependence is statistically clear, but it gives little practical forecast skill for the next episode.

## 5. Interpretation

Across Cascadia, tremor episodes show a time direction. A large episode is followed by a longer quiet time in the same place. The quiet time before an episode does not set its size. This agrees with the time-predictable model and a recovery or reloading period after large episodes. It does not agree with the slip-predictable model. In northern Cascadia, the weak negative r_before agrees with the anti-slip-predictable result of Gao et al. (2012). One possible cause is small precursory episodes just before large ETS. Hulbert et al. (2020) describe a months-long increase in seismic energy before ETS. Our data do not separate these causes.

## 6. Limitations

- Episode size is a count of detected 2.5-minute windows. It is not slip or moment. Detection changed with station coverage. South of 40.5°N there are few windows before 2012. Background detection between 41 and 44°N increased after 2017. We used a time-trend control and an era step, but other detection effects can remain.
- The episode rules are arbitrary. The sensitivity grid shows a stable sign, but the effect size changes from 0.09 to 0.39.
- Bins share large ETS events. The block bootstrap takes this into account only on time scales up to 2 years. Bootstrap intervals for cutoff 300 are not centred on the point estimate. Thus treat them as approximate.
- The central segment has few episodes. Its result is uncertain.
- We tested only size against quiet time. We did not test tidal, seasonal or hydrological forcing, or along-strike migration direction.
- The live PNSN API can revise the catalog. A new download can have a different hash.

## 7. Reproduce

Requirements: Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, pyarrow 26.0.1 and matplotlib 3.11.2.

1. Get the catalog. Use the shared path above or the URL in `files/data_provenance.json`. Check its SHA-256.
2. Copy `files/code/` to a scratch folder.
3. Run `TREMOR_CSV=/path/to/pnsn_tremor_v3_20090801_20261108.csv bash run_all.sh`. The script checks the hash, builds the along-strike coordinate and the episodes, and runs all analyses. It writes the figures to `../result/files/`.
4. The bootstrap steps take about 15 minutes on a loaded 8-core machine.

You can also repeat the main statistics without the raw catalog. Run `core.make_pairs`, `core.per_bin` and `core.pooled` on `files/results/episodes_W50_a5_g3.csv`.

File list:

- `files/code/*.py`: all analysis code.
- `files/results/`: all numeric results, the primary episode catalog, the regional ETS catalogs and the along-strike line.
- `files/fig1_overview.png` to `files/fig4_regional.png`: figures.

## 8. References

- Shimazaki, K. and Nakata, T. (1980). Time-predictable recurrence model for large earthquakes. GRL. doi:10.1029/GL007i004p00279
- Gao, H., Schmidt, D. A. and Weldon, R. J. (2012). Scaling relationships of source parameters for slow slip events. BSSA. doi:10.1785/0120110096
- Wech, A. G. and Creager, K. C. (2008). Automated detection and location of Cascadia tremor. GRL. doi:10.1029/2008GL035458
- Wech, A. G. and Creager, K. C. (2011). A continuum of stress, strength and slip in the Cascadia subduction zone. Nature Geoscience. doi:10.1038/ngeo1215
- Brudzinski, M. R. and Allen, R. M. (2007). Segmentation in episodic tremor and slip all along Cascadia. Geology. doi:10.1130/G23740A.1
- Hulbert, C. et al. (2020). An exponential build-up in seismic energy suggests a months-long nucleation of slow slip in Cascadia. Nature Communications. doi:10.1038/s41467-020-17754-9
- Pollitz, F. F. et al. (2013). Annual modulation of non-volcanic tremor in northern Cascadia. JGR. doi:10.1002/jgrb.50181
- Meng, Q. et al. (2026). Cascadia slow earthquake behaviors modulated by tectonic and environmental forcings. GRL. doi:10.1029/2025GL120690
