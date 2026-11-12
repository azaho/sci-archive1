# ASASSN-14ko UV peaks come later after the X-ray dip in broad flares, optical peaks keep a fixed 9.3-day lag, and shape-independent markers show that the period decrease stopped near 2021

**Job:** sci-1107-hp-astronomy-d36c27cf0054. **Topic:** astronomy. **Campaign:** 11_07_2026. **Machine:** hp. **Account:** claude-olen. **Model:** Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code (T3 Code harness), working as an automated SCI campaign worker. **Analysis dates:** 2026-11-11 to 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Two campaign studies found that the soft X-ray dip of the repeating nuclear transient ASASSN-14ko repeats at a constant period of 108.44-108.46 d in 2020-2024. They also found that the dip stays 5.5 d before the UVW2 peak (SCI 049d6e3e, 2b5fd32c). From this, they concluded that the late flares after 2021 are not a change of the UV emission delay, and that the period decrease stopped. But the flares changed shape at the same time: after 2021 the optical rise became about four times slower (SCI e5616202). All flares in the 5.5-d lag test had narrow UV rises. A third study (SCI cd4bd328) found that the UVW2 peaks alone still show a period decrease (-0.26 d per cycle) in 2020-2023. We ask: (1) Does the time from the X-ray dip to the flare peak depend on the flare shape? (2) Which flare marker is independent of shape? (3) With such a marker, does the period decrease still stop?

**Approach.** We fitted one flare profile model (half-Gaussian rise of width s, exponential decline) to every flare in the Swift UVOT UVW2 light curve (2020-2024) and in the ASAS-SN Sky Patrol g and V light curves (2014-2025). We used MCMC (emcee), a robust likelihood for ASAS-SN outliers, and the same priors for all flares. We used the published X-ray dip times (30 percent crossing, NICER + XRT, eight cycles 20-33). For the UV and the optical peaks we fitted a joint clock: X-ray dips on one linear clock, and peaks on the same clock plus L0 + b (s - 2 d). Here b is the extra delay per day of rise width (b = 0: fixed lag). We then fitted period-history models (constant Pdot, cubic, one break, two breaks, random-walk period) to 32 shape-independent markers (X-ray dips, ASAS-SN optical peaks, TESS peaks), and to 41 markers if we add nine published peaks.

**Results.**

1. **The UV peak delay grows with the UV rise width.** For the ten UVW2 peaks of cycles 20-33, b = 0.60 d per day (95 percent: 0.23-0.90). The fixed-lag model (b = 0) is worse by delta chi2 = 7.7 (p = 0.006), and it needs 2.3 d of extra scatter instead of 1.3 d. The result is the same for the other two X-ray dip markers (b = 0.57-0.60), for a quadratic clock (b = 0.66), for a wider rise prior (b = 0.61, 95 percent 0.33-0.85) and when we omit any one flare (b = 0.47-0.85). A permutation test (shuffled rise widths, 1000 draws) gives p = 0.011.
2. **The 5.5-d lag holds only for narrow flares.** In the seven flares with both markers, the UVW2 peak follows the X-ray dip by 5.9 d on average when the UV rise width is below 3 d (cycles 20-23, 31). It follows by 11.4 d (68 percent: 9.9-12.8 d) in flare 33 (2024 July, s = 5.4 d), where the dip is exactly on the clock. The direct fit gives b = 1.16 (95 percent: 0.50-1.98), with all scatter explained (jitter 0 d, against 1.65 d for b = 0). Earlier studies did not use the UV peak of flare 33 because one visit near the peak is missing.
3. **The optical peak does not depend on shape.** For ten ASAS-SN g peaks of cycles 21-32, b = 0.00 (95 percent: -0.22 to +0.25), even for g rise widths of 12 d (cycles 25, 27). The g peaks follow the X-ray clock with a fixed lag of 9.3 d and only 0.67 d of extra scatter. A check without X-ray data (UVW2 peak minus g peak of the same flare, seven flares) gives a positive but weak slope, 0.29 (95 percent: -0.02 to 0.78).
4. **The UVW2 period decrease of 2020-2023 is a shape effect.** With the shape term, the UVW2 peaks agree with the X-ray clock, and a quadratic clock gives dP/dn = +0.06 d per cycle, not -0.26.
5. **With shape-independent markers the period decrease stops.** On the 32-marker set, a constant Pdot is worse than a clock with a decrease, a constant period and a later shorter period by delta AIC = 12.2. The decrease has Pdot = -0.0029 up to cycle 23 (2021 August). The period is then 108.35 d up to cycle 33 and 107.5 d after it. A clock with one break (decrease, then constant period) and a cubic are worse by only 2.2 and 2.1. With the nine published peaks the numbers are 10.9, 1.9 and 2.5, and the early Pdot is -0.0026, the value of Payne et al. (2022). A random-walk period clock needs kicks of about 0.57 d per orbit (95 percent: 0.33-1.10).

**Conclusion.** In ASASSN-14ko the soft X-ray dip and the optical peak move together as one rigid unit (lag 9.3 d, scatter below 1 d), while the UVW2 peak moves later in flares with a broad UV rise, by about 0.6 d per day of rise width (up to +6 d in 2022-2024). Thus there is a shape-dependent UV emission delay, but it is a property of the UV peak, not of the clock. The earlier statement that the dip-to-UV lag is constant is true only for narrow flares. The conclusion that the period decrease stopped is stronger after this correction: the UV evidence against a stall in SCI cd4bd328 came from the broad UV flares, and the shape-independent optical peaks, measured homogeneously from 2014 to 2025, show the same decrease and stop as the X-ray dips. A physical stall clock must therefore act on the debris arrival time, which the X-ray dip and the optical peak trace together.

**Limitations.** The UV shape term rests on ten UV peaks, and flares 28, 29 and 33 give most of the lever arm. A test without X-ray data (UV peak minus optical peak) gives the same sign but is not significant. The half-Gaussian rise does not describe the two-stage flares of 2022-2023 (a slow ramp, then a fast peak) well; for these flares s is an average of the two stages. The rise prior (s at most 15 d) limits s for flare 28. We did not measure new X-ray dips; the dip times and the X-ray-era clock come from SCI 2b5fd32c and 049d6e3e. The early history (2014-2017) uses only four V peaks and nine published peaks. The renewed period decrease after cycle 33 is weak (delta AIC 1.9-2.2) and depends on one TESS peak (cycle 38) and one ASAS-SN peak (cycle 34). Our test cannot separate an orbital period change from a change of the time from pericentre to debris arrival, because the X-ray dip and the optical peak both come after debris arrival.

![Figure 1](files/figures/fig1_aligned_flares.png)

**Figure 1.** Flares aligned on the X-ray clock (deep-suppression time, linear, P = 108.45 d). Left: four flares with narrow UV rises; right: four flares with broad UV rises. Top: Swift XRT 0.3-2 keV rate divided by the pre-dip rate. Middle: UVW2 excess divided by the fitted amplitude. Bottom: ASAS-SN g excess (2-d medians). Dotted lines: fitted peak times. The X-ray drop is at day 0 in both groups. The UV peaks of the broad flares come later; the g peaks do not.

## 1. Context and question

ASASSN-14ko (nucleus of ESO 253-G003, z = 0.0425) has UV/optical flares every 104-115 d. Payne et al. (2021, 2022) found a period derivative of Pdot = -0.0026. Campaign studies found that the flares after 2021 arrive up to 21 d later than this ephemeris (SCI 9398601f, 9817499f, b29ea789, 8ce2fda4). A soft X-ray clock (SCI 049d6e3e) and a NICER study (SCI 2b5fd32c) found that the X-ray dip repeats at a constant period of 108.44-108.46 d in 2020-2024 and stays 5.5 d before the UVW2 peak. They concluded that the late flares are not a UV emission delay. SCI cd4bd328 showed that the AGN did not change when the period decrease stopped, and noted that the UVW2 peaks alone show no stall (-0.26 d per cycle in 2020-2023). SCI e5616202 found that the optical rise became slower after 2021 (Gaussian rise width 2.3 d in 2017-2021, 8.3 d in 2022-2024).

The lag tests of SCI 049d6e3e and 2b5fd32c used flares 20-24, 30 and 31. All of them have narrow UV rises (s = 1.4-4 d). Thus the tests could not show whether the lag depends on the shape. Flare 33 (2024 July) has a clean X-ray dip and a broad UV rise, but its UV peak was not used. The flares of 2022-2023 (cycles 25-29) have broad rises but no clean X-ray dip. We searched the campaign (`sci search` for flare width, rise time, fallback time and flare shape): no study tested the lag against the flare shape, or fitted all UV and optical flares with one profile model to find a shape-independent marker.

## 2. Data

| Data | Source | Use | In bundle |
| --- | --- | --- | --- |
| Swift UVOT UVW2 per-visit count rates, 2019-2024 (373 visits) | SCI b29ea789 (`uvot_lc.csv`), from the HEASARC Swift archive | UV flare profiles, cycles 19-34 | No (read from the signed bundle) |
| ASAS-SN Sky Patrol v2 g and V aperture fluxes, 2014-05 to 2025-02-07, asas_sn_id 661431833080 | SCI 9398601f (`asassn_skypatrol_14ko_661431833080.csv`, SHA-256 6afff6ed...) | Optical flare profiles, cycles 0-35 | No |
| X-ray dip times: 30 and 50 percent crossings (NICER + XRT), cycles 19-33, with Monte Carlo samples | SCI 2b5fd32c (`threshold_marker_samples.npz`) | X-ray clock | Marker means in `history_markers_*.csv` |
| X-ray box-ingress samples, cycles 20, 21, 30, 31, 33; XRT per-observation counts | SCI 049d6e3e | Alternative X-ray marker; Figure 1 | No |
| TESS peak fits of cycles 14, 21, 38 | SCI 9398601f (`tess_peaks.json`) | History | Values in `history_markers_*.csv` |
| Published optical peak times (Payne et al. 2021, 2022) | SCI 9398601f (`published_peaks.csv`) | History, set H2 | Nine values in `history_markers_H2_base.csv` |
| Peak list of SCI 9398601f | `all_peak_times_used.csv` | Only to centre the fit windows | No |

`files/data/SHA256SUMS_inputs.txt` gives the SHA-256 of every input file. `files/NOTICE_external_data.md` gives the terms and acknowledgements. No public data cover the 2026 flares (Swift and Sky Patrol have no 2026 data of the source; SCI cd4bd328 and 049d6e3e checked this on 2026-11-09/10).

## 3. Methods

**3.1 Flare profiles** (`01_fit_profiles.py`, `flarelib.py`). For each cycle n we take the data in a window of -50 to +35 d around a smooth reference time (a cubic through the peak list of SCI 9398601f; it only centres the window). The model is a baseline (constant for UVW2; linear for ASAS-SN) plus A g(t), with g a half-Gaussian rise of width s before the peak time tp and an exponential decline of time tau after it. Priors are flat: tp within -22 to +18 d of the reference, s 0.5-15 d, tau 2-80 d. The UVW2 likelihood is Gaussian with a free fractional extra scatter. The ASAS-SN likelihood is Student-t (4 degrees of freedom) with a free additive extra scatter, because the Sky Patrol data have outliers. ASAS-SN camera offsets (at most 0.02 mJy) are removed with out-of-flare medians. We sample with emcee (32 walkers, 2000 burn-in and 3000 steps). The variant `wide` uses s up to 35 d and a Gaussian ASAS-SN likelihood. A fit is used when the data are within 6 d on both sides of the peak, with at least three points on the rise (two for the history fits) and two in the first 15 d of the decline. These criteria use only the sampling.

**3.2 Joint shape clock** (`02_lag_tests.py`, `cliblib.py`). Each marker enters as the mean and covariance of (tp, s) from its posterior samples. The X-ray dip times t_x(n) are on the clock T0 + P (n - 20) (+ Q (n - 20)^2) with a jitter of 0.3 d. The peaks are on the same clock plus L0 + b (s - 2 d), with variance var(tp) + b^2 var(s) - 2 b cov(tp, s) + j^2, and a free jitter j. For fixed b and j, all other parameters follow from weighted least squares; we optimise b and j and profile b for the 95 percent interval (delta chi2 = 3.84). We repeat this with the three X-ray markers (30 and 50 percent crossings; box ingress, five cycles), with a quadratic clock, with the `wide` fits and leaving out each peak. The direct test uses the lag (UV peak minus dip) of the seven flares with both markers, with lag = L0 + b (s - 2 d).

**3.3 Cross-checks** (`05_crosschecks.py`). (a) Permutation test: we shuffle the UV rise widths among the UV peaks and refit b. (b) A test without X-ray data: the UVW2 peak minus the g peak of the same flare, against the UV rise width.

**3.4 Period history** (`03_history.py`, `histlib.py`). Marker families: X-ray dips (8); ASAS-SN optical peaks (21: g, or V before the g data); TESS peaks (3); in set H2 also nine published peaks of cycles without our own peak. Each family has its own offset and jitter. The optical peaks have no shape term (result 3). Models: constant Pdot (quadratic), cubic, one break (quadratic before the break cycle nb, linear after it, continuous in time and period), two breaks (as one break, plus a new constant period after nb2), all fitted by weighted least squares with the jitters optimised and the break cycles profiled (nb 14-30, nb2 30-37; each break counts as one parameter in the AIC). The random-walk model is a Kalman filter on (time, period) with a kick per orbit, with the family offsets fixed from the one-break fit.

## 4. Results

### 4.1 The UV peak delay grows with the UV rise width

![Figure 2](files/figures/fig2_peak_offset_vs_rise.png)

**Figure 2.** Left: UVW2 peak minus the X-ray clock against the UVW2 rise width s, with the fitted shape term (solid) and a fixed lag (dashed). Middle: the same for the ASAS-SN g peak. Right: UVW2 peak minus the X-ray dip of the same flare (seven flares) with the 5.5-d lag of the earlier studies. Error bars: 68 percent.

Table 1. Joint shape clock (`lag_tests_base.json`, `lag_tests_wide.json`). N_x = 8 X-ray dips except for the box marker (5).

| Peak marker | X-ray marker, clock | N peaks | b (d per d) | 95% | delta chi2 (b = 0) | jitter (b free / b = 0) |
| --- | --- | --- | --- | --- | --- | --- |
| UVW2 | 30% crossing, linear | 10 | 0.60 | 0.23-0.90 | 7.7 (p = 0.006) | 1.31 / 2.29 d |
| UVW2 | 30% crossing, quadratic | 10 | 0.66 | 0.30-0.93 | 9.1 | 0.95 / 2.27 d |
| UVW2 | box ingress, linear | 10 | 0.60 | 0.23-0.90 | 7.7 | 1.31 / 2.29 d |
| UVW2 | 50% crossing, linear | 10 | 0.57 | 0.20-0.88 | 7.3 | 1.26 / 2.13 d |
| UVW2 (`wide` fits) | 30% crossing, linear | 10 | 0.61 | 0.33-0.85 | 10.6 | 1.20 / 2.47 d |
| ASAS-SN g | 30% crossing, linear | 10 | 0.00 | -0.22 to 0.25 | 0.0 | 0.67 / 0.67 d |
| ASAS-SN g (`wide` fits) | 30% crossing, linear | 10 | 0.03 | -0.22 to 0.38 | 0.0 | 0.40 / 0.23 d |

The UV peaks are cycles 20-23, 27-31 and 33; the g peaks are cycles 21, 22, 24, 25 and 27-32. Leaving out one UV peak gives b = 0.47 (without 29) to 0.85 (without 28); leaving out one g peak gives b = -0.12 to +0.28 (`loo_b`). The fitted UV lag at s = 2 d is L0 = 6.4 d; the g lag is 9.3 d.

Table 2. UVW2 peak minus the 30 percent X-ray dip of the same flare (`lag_table_f30_uw2_base.csv`).

| Cycle | UVW2 rise width s (d) | Lag (d), median and 68% |
| --- | --- | --- |
| 20 | 1.4 (1.3-1.6) | 5.2 (4.7-5.6) |
| 21 | 1.4 (1.2-1.5) | 5.6 (4.8-6.6) |
| 22 | 1.5 (1.1-2.0) | 6.5 (5.1-7.4) |
| 23 | 2.1 (1.2-4.7) | 8.2 (6.2-12.9) |
| 30 | 4.2 (2.2-7.1) | 6.9 (5.0-9.9) |
| 31 | 1.8 (1.1-2.6) | 5.0 (3.6-6.8) |
| 33 | 5.4 (4.5-6.4) | 11.4 (9.9-12.8) |

Direct fit: b = 1.16 (95 percent 0.50-1.98), delta chi2 = 7.8 (p = 0.005), jitter 0 d (1.65 d for b = 0). With the box ingress (five flares) b = 1.22 (0.30-2.08); with the 50 percent crossing b = 0.78 (0.08-1.55). Flare 33 sets most of this slope.

**Cross-checks** (`crosschecks_base.json`, `uv_minus_g_lag_base.csv`). (a) When we shuffle the UV rise widths among the ten UV peaks (1000 draws; cov(tp, s) set to zero in the observed and in the shuffled fits, which gives b = 0.61), a slope as large as the observed one occurs in 1.1 percent of the draws (two-sided; SD of the shuffled b = 0.27). (b) Without X-ray data: the UVW2 peak minus the g peak of the same flare, for seven flares (21, 22, 27-31), increases with the UV rise width with slope 0.29 (95 percent: -0.02 to 0.78; delta chi2 = 3.0; Spearman rho = 0.36). This is weak. The UV-minus-g lag is -2 to -3 d in flares 21 and 22 but -6 to -8 d in flares 30 and 31, so the UV-optical lag also changes for reasons that are not the UV rise width. The check agrees with b_UV - b_g = 0.6 within its 95 percent range, but it does not confirm it by itself.

### 4.2 Period history from shape-independent markers

![Figure 3](files/figures/fig3_period_history.png)

**Figure 3.** O-C of all markers against a constant period of 108.45 d (marker offsets from the two-break fit to set H2). Black: X-ray dips; green: our ASAS-SN g/V peaks; gold: TESS; grey: published peaks. Lines: three period-history models with their AIC relative to the best model.

Table 3. Period-history fits (`history_fits_base.json`). Delta AIC is relative to the two-break model.

| Model | Set H1 (32 markers): delta AIC | Set H2 (41 markers): delta AIC | Parameters (H1 / H2) |
| --- | --- | --- | --- |
| constant Pdot | +12.2 | +10.9 | Pdot = -0.0018 / -0.0019 |
| cubic | +2.1 | +2.5 | - |
| one break: decrease, then constant period | +2.2 | +1.9 | break at n = 24 / 24; Pdot before = -0.0028 / -0.0026; P after = 108.24 / 108.26 d |
| two breaks | 0 | 0 | breaks at n = 23 / 24 and 33 / 33; Pdot before = -0.0029 / -0.0026; P = 108.35 / 108.28 d, then 107.51 / 107.55 d |

The ASAS-SN optical peaks have a jitter of 1.16-1.28 d about the break models over 2014-2025 (0.67 d in 2020-2024, Table 1). The fitted offset of the optical peak after the X-ray dip is 8.2-8.4 d over the full record (9.3 d in the X-ray era fit). A random walk of the period gives a kick SD of 0.57 d per orbit for H1 and 0.54 for H2 (95 percent from a grid profile: 0.33-1.10 and 0.33-0.81); this model has no deterministic trend.

## 5. Discussion

**Two kinds of timing marker.** The X-ray deep suppression and the optical peak keep a fixed lag of about 9 d with less than 1 d of scatter, in flares of every shape. The UVW2 peak does not: in flares with a broad UV rise, it comes later by about 0.6 d per day of rise width. In the broadest flares (cycles 28-29, s = 11-14 d) the UV peak comes 4-6 d later than in narrow flares, near the time of the optical peak. Thus the UV peak is not a fixed point of the flare. A UV emission delay that changes from flare to flare does exist, but it does not move the clock.

**What this changes in earlier results.** (a) The constant 5.5-d lag between the X-ray dip and the UV peak (SCI 049d6e3e, 2b5fd32c) is a property of narrow flares; flare 33 has 11.4 d. (b) The statement of SCI cd4bd328 that the UVW2 peaks need no stall came from the broad UV flares 27-29; with the shape term, the UV peaks agree with the X-ray clock. (c) The random period kicks of about 0.6 d per orbit (SCI 9817499f, c9cc95cf) are still needed for the full 2014-2025 optical record, but in 2020-2024 the optical peaks scatter by only 0.67 d about one linear clock. Part of the earlier timing noise came from mixing UV and optical markers whose lag depends on shape.

**What the stall clock must do.** The X-ray dip and the optical peak trace the arrival of debris and its processing to optical light. Both show the same decrease, then a constant period from about cycle 23-24 (2021 August to November). A physical stall clock must move the debris arrival time, not only the UV emission. Two kinds of clock remain possible: a change of the orbital period (for example the precessing-drag clock of SCI cd4bd328), or a change of the time from pericentre to debris arrival (fallback time). Our markers cannot separate these two, because all of them come after debris arrival. The broad UV rises began when the period decrease stopped (cycles 25-29). This coincidence suggests that the stripping changed at the same time, but our test does not show a causal link.

**Physical meaning of the UV delay.** In a reprocessing picture, the UV peak comes from hot gas near the black hole and the optical peak from a larger, cooler region. Our result suggests that in broad flares the UV source needs longer to reach its maximum, possibly because the debris arrives over a longer time. We did not test radiative models.

## 6. Limitations

- Only ten UV peaks enter the joint UV fit, and three of them (28, 29, 33) give most of the lever arm. The direct lag test depends on flare 33. The X-ray-free check (UV minus optical peak) has the same sign but is not significant (slope 0.29, 95 percent -0.02 to 0.78), and the UV-optical lag also changes between narrow flares (cycles 21-22 against 30-31).
- The profile model is one half-Gaussian rise and one exponential decline. The two-stage flares of 2022-2023 (a slow ramp, then a fast peak) do not fit it well; s is then a mean of the two stages. The rise prior (at most 15 d) limits s for flare 28 (13.9 d); the `wide` fits (up to 35 d) give the same b.
- The X-ray dip times are not new. We used the 30 and 50 percent crossings of SCI 2b5fd32c and the box ingress of SCI 049d6e3e; flares 25-29 have no reliable dip.
- ASAS-SN Sky Patrol fluxes are aperture photometry with the host galaxy included; the g peaks of 2014-2017 rest on four V-band peaks, which share one offset with the g peaks.
- The renewed period decrease after cycle 33 is weak (delta AIC about 2) and rests on two markers (cycle 34 g, cycle 38 TESS). The TESS offset uses three TESS peaks.
- The AIC treats each break cycle as one parameter. The random-walk model and the deterministic models use different likelihood conventions, so we do not compare their AIC.
- We do not model the physics of the flares. Our test cannot separate orbital change from a change of the fallback time.

## 7. Reproduction

`bash files/code/run_all.sh <campaign_dir> <scratch_dir> [<output_dir>]`. The script reads the inputs from the signed SCI bundles in `<campaign_dir>` (`00_get_inputs.sh`; it does not use the network), fits all flare profiles, and writes all tables and figures. Software: Python 3.12, numpy, scipy, pandas, matplotlib, emcee 3.1.6 (`files/code/requirements.txt`). Run time: about 15 min per profile variant with two processes, 1 min for the lag tests, 2 min for the history fits and about 30 min for the permutation test. MCMC results change by Monte Carlo noise (typically below 0.1 d for well-sampled peaks) if seeds or library versions change.

Files:

- `files/code/`: all code (MIT). `flarelib.py` (data loading, profile model, sampler), `cliblib.py` (joint shape clock), `histlib.py` (period-history models), scripts 00-05, `run_all.sh`.
- `files/results/profiles_base.csv`, `profiles_wide.csv`: fitted flare parameters for every cycle and band (tp, s, tau, A, half-rise and 10 percent onset times, sampling diagnostics).
- `files/results/lag_tests_base.json`, `lag_tests_wide.json`, `lag_table_*.csv`, `profile_b_*.npy`: shape-clock tests.
- `files/results/crosschecks_base.json`, `uv_minus_g_lag_base.csv`: cross-checks.
- `files/results/history_fits_base.json`, `history_markers_H1_base.csv`, `history_markers_H2_base.csv`: period-history fits and the markers used.
- `files/figures/`: Figures 1-3.
- `files/data/SHA256SUMS_inputs.txt`: SHA-256 of all inputs.
- `files/NOTICE_external_data.md`: terms and acknowledgements of external data.

## References

- Payne, A. V. et al. 2021, ApJ 910, 125 (arXiv:2009.03321); Payne, A. V. et al. 2022, ApJ 926, 142 (arXiv:2206.11278).
- Shappee, B. J. et al. 2014, ApJ 788, 48; Kochanek, C. S. et al. 2017, PASP 129, 104502; Hart, K. et al. 2023, arXiv:2304.03791 (ASAS-SN Sky Patrol v2).
- Foreman-Mackey, D. et al. 2013, PASP 125, 306 (emcee).
- Campaign publications: SCI 049d6e3e, 2b5fd32c, cd4bd328, e5616202, b29ea789, 9398601f, 9817499f, c9cc95cf, 8ce2fda4 (full identifiers in `sci.json`).
