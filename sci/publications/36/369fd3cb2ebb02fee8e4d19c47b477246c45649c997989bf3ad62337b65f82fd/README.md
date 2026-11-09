# Cascadia tremor in 2013-2026 followed the M2 tide about twice as strongly 48 h or more after local onset as in the first 24 h

**Job:** sci-1107-dell-earth-and-ocean-sciences-c48481b79827 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-andrii · **Campaign:** 11_07_2026 · **Date:** 2026-11-08.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Houston (2015, doi:10.1038/ngeo2419) used about 31,000 tremor events from six large Cascadia slow-slip events (2007-2012). She found that the tidal sensitivity of tremor increases during several days after tremor starts at a location. She explained this as fault weakening as slip accumulates.

We ask three questions:

1. Does the same increase occur in tremor that started after 2012, outside the time of the original events, and in all Cascadia regions of the PNSN catalog?
2. Is the increase larger than the change that the same procedure gives at non-tidal periods?
3. Can simple alternatives explain the increase? We test the local tremor rate, the position in the episode, the end of the episode, catalog saturation, and the mix of cells.

We do not compute tidal stress on the fault. We measure modulation at the M2 period (12.42 h) with a phase that we fit in one period and then keep fixed. Thus our amplitude is a relative rate response, not a sensitivity per kPa.

## 2. Data

* **Tremor:** PNSN tremor API v3.0, all events from 2009-08-01 to 2026-11-08 (791,720 detections; latitude 39.1-50.9 N).
  Shared campaign dataset `datasets/pnsn-tremor-v3-20090801-20261108/pnsn_tremor_v3_20090801_20261108.csv`
  (real path `/mnt/dell-data/shared_datasets/.campaign-dataset-objects/pnsn-tremor-v3-20090801-20261108-k7r7oi9c/`),
  source URL `https://tremorapi.pnsn.org/api/v3.0/events?starttime=2009-08-01T00:00:00&endtime=2026-11-08T00:00:00&format=csv`,
  SHA-256 `08ee9054c43249d8441f0700fe7241c2b103ba51854d13bf4d9f212c97aad826`, 67,459,361 bytes.
  We did not copy the raw catalog into this bundle. The derived hourly panel is in `files/data/panel.parquet`.
* **Tides:** NOAA CO-OPS harmonic constants for six gauges (`files/data/harcon_*.json`) and hourly Neah Bay predictions for 2020-01 to 2020-03 (`files/data/pred_9443090_2020q1.csv`). We use them only to check the phase convention and to give the tremor peak time relative to local high water.

Catalog facts that affect the method:

* All detection times are on a 150-s grid. One cell can have at most 24 detections in one hour.
* Before 2017 the catalog has no duration field. From 2017 the windows are 150 s or 300 s. We test the two parts of the test period separately.

## 3. Method

**Cells and local episodes.** We put detections in cells of 0.2 deg latitude by 0.3 deg longitude. We count detections per cell per UTC hour. In each cell, a gap of more than 72 h with no detection starts a new local episode. We keep local episodes with 30 or more detections and 24 h or more from the first to the last detection. This gives 4,484 local episodes (604,700 detections). The onset is the first detection hour. The time since onset is tau.

**Regions.** N California (< 43 N), Oregon (43-45.5 N), S Washington (45.5-47 N), N Washington and Vancouver Island (> 47 N).

**Model.** We use conditional (fixed-effect) Poisson regression of hourly counts. The fixed effects are cell x local episode x 24-h block after onset. They remove the slow rise and fall of each episode. We add 24 UTC hour-of-day effects. These remove daily detection cycles (for example cultural noise), which also remove the solar S2 and S1 periods. The tidal term is a * cos(V_M2(t) - theta_r). V_M2 is the M2 equilibrium argument. We checked the convention: a fit to NOAA Neah Bay predictions gives an M2 phase of 248.7 deg, and NOAA gives 246.3 deg (the difference agrees with the nodal correction that we omit). exp(a) is the tremor-rate ratio at the peak tidal phase relative to the mean.

**Split (fixed before the test fits).**
* Phase-fit period: local episodes with onset from 2009-08 to 2012-12 (712 episodes, 101,237 detections). For each region, we fit the M2 phase theta_r of the peak rate.
* Test period: onset from 2013-01 to 2026-11 (3,772 episodes, 503,463 detections). We keep theta_r fixed and fit a in bins of tau. We also fit a quadrature term sin(V - theta_r) in each bin.

**Primary statistic.** D = a(tau >= 48 h) - a(tau < 24 h) in the test period, pooled over regions. The Houston (2015) result predicts D > 0.

**Uncertainty.** (1) A cluster bootstrap: we draw exponential weights for clusters of region x 60-day onset window (260 test clusters, 400 draws). (2) Cluster-robust sandwich errors. (3) A placebo null: we apply the full pipeline (phase fit in 2009-2012, test in 2013-2026) to 34 non-tidal periods from 1.45-1.80 and 2.10-2.55 cycles per day.

**Alternative explanations that we test.**
* *Rate:* modulation can depend on the background stress rate. A high local tremor rate can mark a fast slip front. We repeat the tau test inside tertiles of the cell daily count.
* *Accumulated tremor:* we use the share of the local episode detections that have already occurred (F) as a proxy for local slip, and we fit F and tau together.
* *Episode edges:* we fit modulation as a function of the time before the last local detection.
* *Saturation:* we remove all 24-h blocks in which any cell-hour has 12 or more detections.
* *Mix of cells:* we keep only local episodes that last 96 h or more, so that the same episodes give early and late hours.
* *Settings:* we use cells of 0.1 x 0.15 deg and 0.4 x 0.6 deg, gaps of 48 h and 120 h, and an onset at the 5% quantile of the episode detections.

## 4. Results

### 4.1 Main test (Figure 2)

| Test period 2013-2026 | 0-24 h | 24-48 h | >= 48 h | D (late - early) |
|---|---|---|---|---|
| a (cluster-robust SE) | 0.077 (0.013) | 0.089 (0.016) | 0.164 (0.014) | **0.086 (0.017)** |
| rate ratio at peak, exp(a) | 1.08 | 1.09 | 1.18 | |

* Bootstrap 95% interval for D: 0.054 to 0.116. No bootstrap draw gave D <= 0.
* Finer bins rise steadily: a = 0.058 (0-12 h), 0.099 (12-24 h), 0.089 (24-48 h), 0.131 (48-72 h), 0.147 (72-120 h), 0.187 (>= 120 h).
* The phase-fit period (in-sample, 2009-2012) gives a similar pattern: 0.062, 0.117, 0.167 (D = 0.106, SE 0.038).

### 4.2 Placebo periods (Figure 3)

* At the 34 non-tidal periods, D has mean 0.002, SD 0.015 and maximum 0.030. The M2 value (0.086) is larger than all 34 and is about 5.5 placebo SDs from their mean.
* The pooled out-of-sample M2 amplitude is a = 0.136 (SE 0.011). The placebo amplitudes have SD 0.005. Thus the 2009-2012 phase predicts the 2013-2026 M2 response well.
* The test-period quadrature term is 0.047. Thus the peak phase in 2013-2026 is about 19 deg (about 40 min) different from the 2009-2012 phase.
* O1 gives a small out-of-sample response (a = 0.039, SE 0.008; D = 0.021, SE 0.020). N2 gives no clear response (a = 0.014, SE 0.009; D = 0.011, SE 0.017). The N2 ocean tide is about 0.2 times the M2 tide, so we expect a value near 0.03 and the test has low power.

### 4.3 Regions (Figure 2, right)

| Region | 0-24 h | 24-48 h | >= 48 h | D (SE) |
|---|---|---|---|---|
| N California | 0.034 | 0.010 | 0.045 | 0.011 (0.021) |
| Oregon | 0.076 | 0.012 | 0.207 | 0.131 (0.057) |
| S Washington | 0.169 | 0.160 | 0.253 | 0.084 (0.066) |
| N Washington / Vancouver I. | 0.146 | 0.197 | 0.276 | 0.129 (0.026) |

* The increase is clear in N Washington and in Oregon. It is uncertain in S Washington (few detections).
* **N California tremor shows almost no M2 response at any tau** (a <= 0.045), although this region has 47% of the test detections. In the 2009-2012 fit its amplitude was also small (0.030). The other regions have amplitudes of 0.15-0.22 in the same fit.
* In the 2009-2012 fit, the peak tremor rate occurs 3.7-4.7 h after local M2 high water at the NOAA reference gauges (Toke Point, South Beach, Neah Bay). This is about 1.5-2.5 h before low water.

### 4.4 Alternative explanations (Figure 4)

* **Rate does not explain the increase.** Inside each daily-count tertile, a increases from early to late: low 0.10 -> 0.25, middle 0.07 -> 0.21, high 0.08 -> 0.15. Over all tau, modulation is larger at low rates (0.21, 0.17 and 0.12 from low to high tertile). Thus a rate effect exists in addition to the time effect.
* **Accumulated tremor and time both contribute.** a increases with the share F of the episode that has passed: 0.074, 0.107, 0.183, 0.188 for the four quarters. With F and tau together, tau >= 48 h adds 0.049 (SE 0.018) beyond F, and the last half of F adds about 0.09 beyond tau. The two variables are strongly related, and the data cannot separate "time" from "accumulated slip".
* **The episode end does not give the increase.** In the last 24 h before the last local detection, a is lower (0.092) than 24-48 h before the end (0.163). With time-to-end in the model, the tau increase stays (0.035 -> 0.126).
* **Saturation and mix of cells do not explain it.** Without near-saturated blocks: D = 0.101 (0.020). Only episodes of 96 h or more: D = 0.092 (0.021).
* **The catalog change does not explain it.** 2013-2016: D = 0.105 (0.031). 2017-2026: D = 0.081 (0.021).
* **Settings:** D = 0.120 (0.1 deg cells), 0.073 (0.4 deg cells), 0.097 (48-h gap), 0.083 (120-h gap), 0.113 (onset at the 5% quantile). All SEs are 0.016-0.020.

## 5. Conclusion

With a phase that we fit in 2009-2012 and then keep fixed, Cascadia tremor in 2013-2026 shows a clear M2 response. The response at 48 h or more after local onset is about twice the response in the first 24 h. This result agrees with Houston (2015) in tremor that the original study did not use, and it is stable across the tests above. A local-rate effect also exists, but it does not explain the time effect. The data cannot separate elapsed time from accumulated local tremor (a slip proxy). Both agree with weakening of the fault as slip accumulates, but our test does not prove that mechanism. Northern California tremor shows almost no M2 response.

## 6. Limitations

* We do not compute tidal stresses (solid earth and ocean load) on the plate interface. Thus we cannot give a sensitivity per kPa or a friction value, and we cannot compare the shear and normal stress parts as Houston (2015) did.
* One phase per region is a simplification. The ocean-load phase changes along the coast and inland. The 19 deg phase difference between periods shows a small error of this type. Projection on a slightly wrong phase decreases a; it does not make a larger with tau unless the phase changes with tau. The quadrature terms by tau are in `files/results/results.json`.
* The catalog is a detection catalog with a 150-s grid. Detection can change with ocean or tidal-current noise at M2. A constant detection effect cannot make the tau pattern, but it can add to a.
* Clusters of 60 days by region do not remove all dependence. Regions share the same tidal phase at a given time. The placebo null does not depend on this choice and gives the same conclusion.
* The weak N California response can have a physical cause (stress phase, depth, or a different fault state) or a catalog cause. We did not test these causes.
* The definition of a local episode (cell size, gap, minimum count) is arbitrary. The tested variants give the same sign and similar size.

## 7. Reproduce

From a campaign worktree that has the `datasets/` link:

```
bash files/code/run_all.sh
```

* `prep.py` makes the hourly panel and local episodes (seconds).
* `cpois.py` has the conditional Poisson fit and the tidal arguments.
* `analysis.py` makes the main test, the regions, the placebo periods, N2/O1, saturation, era and rate tests (about 35 min on 24 cores, seed 20261108). Output: `files/results/results.json`.
* `robustness.py` makes the setting variants, F, and time-to-end fits. Output: `files/results/robustness.json`.
* `phase_check.py` checks the phase convention against NOAA. Output: `files/results/phase_check.json`.
* `figures.py` makes the four figures in `files/figures/`.

Python 3.12 with numpy, pandas, pyarrow and matplotlib. No other dependencies.

## 8. Files

* `files/data/panel.parquet`: hourly counts y per cell per local episode (ep, cy, cx, hr = hours since 2000-01-01 UTC, tau, block).
* `files/data/local_episodes.csv`: one row per local episode (cell centre, onset, end, number of detections).
* `files/results/*.json`: all fitted values.
* `files/figures/fig1_data.png` to `fig4_explanations.png`.

## References

* Houston, H. (2015). Low friction and fault weakening revealed by rising sensitivity of tremor to tidal stress. Nature Geoscience 8, 409-415. doi:10.1038/ngeo2419
* Rubinstein, J. L., La Rocca, M., Vidale, J. E., Creager, K. C., Wech, A. G. (2008). Tidal modulation of nonvolcanic tremor. Science 319, 186-189. doi:10.1126/science.1150558
* Wech, A. G., Creager, K. C. (2008). Automated detection and location of Cascadia tremor. Geophysical Research Letters 35, L20302. doi:10.1029/2008GL035458
* Hawthorne, J. C., Rubin, A. M. (2010). Tidal modulation of slow slip in Cascadia. Journal of Geophysical Research 115, B09406. doi:10.1029/2010JB007502
* PNSN tremor catalog: https://pnsn.org/tremor
