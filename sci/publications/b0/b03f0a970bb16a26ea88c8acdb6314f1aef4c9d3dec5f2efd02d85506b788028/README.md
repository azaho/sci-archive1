# ASASSN-14ko optical half-rises tied to the X-ray dip show a shorter period again after 2023 and slow flare rises only while the period was constant; flare 41 forecast for 2026 November 10-15

**Job:** sci-1107-dell-astronomy-7fdef037b7d7. **Topic:** astronomy. **Campaign:** 11_07_2026. **Machine:** dell. **Account:** claude-myxtap. **Model:** Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code (T3 Code harness), working as an automated SCI campaign worker. **Analysis date:** 2026-11-11 (UTC). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** The soft X-ray dips of the repeating nuclear transient ASASSN-14ko repeat at a constant period of 108.44 d in 2020-2024 (SCI 049d6e3e, 2b5fd32c). Thus the fast period decrease of Payne et al. (2022) stopped. Earlier studies then found that the 2024-2026 optical, TESS and SPHEREx flares arrive 3-8 d early relative to that X-ray clock (SCI 049d6e3e). This would mean that the period decrease started again. A precessing star-disc drag clock predicts such a return (SCI cd4bd328); a two-break clock predicts that the period stays constant. But the optical flare shapes changed after 2021 (SCI e5616202): the rise became slower, and the optical peaks of 2022 came up to 24 d early while the X-ray clock stayed constant. Thus an early optical marker can come from a shape change, not from the orbit. We ask: (1) Which optical marker keeps a constant lag on the X-ray dip of the same flare? (2) With that marker, is the early arrival of the 2024-2026 flares real? (3) What form has the period history, and which frozen clocks survive? (4) Is the flare shape related to the period change?

**Approach.** We fitted all ASAS-SN g-band flares of 2017-2025 (cycles 11-34) and the TESS rises of flares 14 and 38 with a half-Gaussian-rise, exponential-decline model (MCMC), and with a second model that adds a slow linear precursor. For the seven cycles with a measured X-ray deep-suppression dip (NICER and Swift XRT, SCI 2b5fd32c) we measured the lag of each optical and UV marker on the dip of the same cycle. We then converted the best marker into dip-equivalent times for cycles without a dip. We used only flares that passed fixed sampling and shape rules (rise sampled within 5 d on both sides, half-rise error below 1.5 d, rise width at most 6 d, the range of the calibration flares). We fitted 18 timing points (cycles 12-38) with constant-period, constant-Pdot, step, ramp and piecewise ("on-off-on", "on-off-step") clocks, and we scored the frozen clock curves of SCI cd4bd328.

**Results.**

1. **The optical half-rise is a dip-locked marker.** The half-rise time of the one-component fit follows the X-ray dip by 4.75 +/- 0.52 d in six cycles (21-24, 30, 31), with chi2 = 1.6 for 5 degrees of freedom and no excess scatter. This is as stable as the UVW2 peak (5.51 +/- 0.37 d, chi2 = 2.5/6). The optical peak (chi2 = 14.8/5, excess scatter 2.1 d) and the two-component markers (chi2 = 27-38/5) are not stable.
2. **Broad flares give early markers.** In 2022-2023 (cycles 25, 27-29, 32) the optical rise was slow (half-Gaussian sigma 7-13 d) and an optical precursor began 6-20 d before the dip (precursor index 0.10-0.23 in cycles 24, 25, 27, 28; at most 0.01 in the other well-referenced cycles). For these flares the half-rise comes 2.6-12 d before the dip-equivalent time of the X-ray clock, while the UVW2 peaks come late. Our shape rule removes them.
3. **The 2024-2026 flares are early also with shape control.** Flares 34 (ASAS-SN, rise sigma 4.1 d) and 38 (TESS, 2.9 d) have normal, narrow rises. Their dip-equivalent times are -3.06 +/- 0.62 d and -7.51 +/- 0.68 d relative to the constant X-ray clock; the SPHEREx peak of flare 37 gives -6.4 +/- 3.1 d. For cycles 19-38 a constant period is worse than the best model by Delta AIC = 17-32 (jitter free, 0.5 d or 1 d). Without flare 38 it is worse by 5-8, without flare 34 by 20-37. Thus the period did become shorter again after 2023. This is not an effect of the flare shape.
4. **The period history is decrease, constant, decrease.** On cycles 12-38 the best clocks are "on-off-step" (dP/dn = -0.53 +/- 0.04 d per cycle before cycle 21, constant period 108.43 +/- 0.06 d, then a sudden change of -1.23 +/- 0.20 d after cycle 32) and "on-off-on" (the same start, then dP/dn = -0.17 +/- 0.03 d per cycle after cycle 29); Delta AIC = 0.7 between them. A constant Pdot is worse by Delta AIC = 18-30. A renewed decrease at the early rate (k3 = k1) is worse by 3.3-7.0 for jitter of 0.5 d or less, but not for 1 d. With 2019-2026 data alone, a slow constant decrease (-0.106 +/- 0.019 d per cycle) is also allowed (Delta AIC = 1.7-4.2).
5. **Frozen clocks.** The two-break clock M2 of SCI cd4bd328 (constant period after 2021) is rejected (Delta AIC = 10-26 in all variants with flare 38). The precessing star-disc drag clock M3 (s = -1.5) fits within Delta AIC = 0-2.5 for jitter 0.5-1 d (7.6 with free jitter) and is the best frozen model in all variants.
6. **The flares rose slowly only while the X-ray clock was constant.** With era boundaries taken from the X-ray dips alone (constant clock in cycles 20-33), the median rise sigma is 7.1 d in the constant era (10 flares) and 2.9 d in the decrease eras (7 flares; before 2020 and after 2024). A one-sided Mann-Whitney test gives p = 0.012 (permutation p = 0.011; p = 0.036 with a stricter error cut). The optical precursor occurred only in cycles 24-29 (and possibly in the poorly sampled cycle 11).
7. **Flare 41 forecasts (frozen before the flare).** All clocks that fit the data put the X-ray dip of flare 41 on 2026 November 6-10 (on-off-step MJD 61354.0 +/- 1.4; on-off-on 61352.0 +/- 1.6; M3 61350.1 +/- 0.6), the optical half-rise on November 10-15, the UVW2 peak on November 11-15 and the optical peak on November 16-20. The constant X-ray clock and M2 put the half-rise on November 21-26. These differ by 7-16 d. On 2026-11-11 no public data cover this flare (Swift: last archived visit 2026-02-05; no Rubin alert stream object within 5 arcsec).

**Interpretation.** The X-ray dip, the UVW2 peak and the optical half-rise of narrow flares move together. Thus the period history from these markers is the history of the debris clock, not of the emission. The period decreased fast before 2020 (about -0.53 d per cycle), was constant for about 11-13 cycles, and became shorter again after 2023, by a sudden change of about 1.2 d or by a slower ramp (-0.17 d per cycle). A clock that switches off and on, such as precessing star-disc drag, fits; a clock that stays constant after 2021 does not. The flare shape changed in the same era as the period change: slow rises and optical precursors occurred only while the period was constant. This is a new constraint for any physical clock. In a precessing orbit, one angle (the orientation of the orbit relative to the disc) sets both the drag and the geometry of the returning debris, so a joint change is possible. A sudden step of 1.2 d needs an energy change of 0.76 percent of the orbital energy in one orbit, 4.4 times the energy loss per orbit at the published Pdot; for an evolved star (as M3 needs) this is 60-110 times the energy scale of a mass-loss kick.

**Limitations.** Only six cycles calibrate the half-rise lag, and two of them have large errors. We assume that the lag of narrow flares is the same before 2020 and after 2024. The post-2024 result rests on two narrow flares (34, 38) and one SPHEREx peak. Step and ramp are not separable with the present data. We chose the shape rule (rise sigma at most 6 d) after we saw that the 2022-2023 flares are broad; the limit is the edge of the calibration range. The width-era test uses few flares (p = 0.01-0.04). Frozen-curve errors do not include the uncertainty of the curve shapes. The ASAS-SN light curve that we used ends on 2025-02-07.

![Figure 1](files/figures/fig2_marker_lags.png)

**Figure 1.** (a) Lag of four flare markers on the X-ray deep-suppression dip of the same cycle. Dashed lines: weighted means. (b) Reduced chi-square for a constant lag. The optical half-rise of the one-component fit and the UVW2 peak keep a constant lag; peaks and two-component markers do not.

## 1. Context

ASASSN-14ko (nucleus of ESO 253-G003, z = 0.0425) has UV/optical flares every 104-115 d. Payne et al. (2021, 2022) found a period derivative of -0.0026. Campaign studies found that the 2022-2026 flares arrive up to 21 d later than that ephemeris (SCI 9398601f, 9817499f, b29ea789, 8ce2fda4). The soft X-ray dip gave an independent clock: the deep suppression repeats at a constant 108.44-108.46 d in 2020-2024 and stays 5.5 d before the UVW2 peak (SCI 049d6e3e, 2b5fd32c). The AGN did not change when the period decrease stopped, and only a precessing star-disc drag clock fits as a drag model (SCI cd4bd328). Clocks that couple the period change to the flare energy fail (SCI e5616202, edf8ce3b, c2b0b0ea). SCI 049d6e3e found that the 2024-2026 markers arrive early again, but it used optical marker offsets calibrated on two flares, without a test of the flare shape. SCI e5616202 found that the rise became slower after 2021.

A campaign search (`sci search` for ASASSN-14ko, flare shape, precursor and AT2022dbl/AT2020vdq, 2026-11-11) found no study that tied optical markers to the X-ray dip of each cycle or that tested the flare shape against the clock eras. Third flares of AT2022dbl and AT2020vdq are already reported absent (Hinkle et al. 2026, arXiv:2606.06578), so we did not study them.

## 2. Data

| Data | Source | Use | In bundle |
| --- | --- | --- | --- |
| ASAS-SN Sky Patrol v2 g-band photometry (source 661431833080), 2017-2025 | SCI b29ea789 `asassn_skypatrol_14ko.csv` | Optical flare fits | No (fitted parameters only) |
| TESS sectors 4 and 98 light curves | SCI b29ea789 `tess_lc_local_s0004.csv`, `s0098.csv` | Rises of flares 14 and 38 | No |
| X-ray deep-suppression (f30) dip times, cycles 19-25, 30, 31, 33 | SCI 2b5fd32c `marker_table.csv` | Reference clock | No (values repeated in `marker_table_cycles.csv`) |
| NICER and XRT visit rates | SCI 2b5fd32c `xray_visits_combined.csv` | Pre-dip X-ray level, Figure S1 | No |
| UVW2 peak times | SCI 049d6e3e `xclock_oc.csv` | UV lag | No |
| Swift UVOT UVW2 photometry | SCI b29ea789 `uvot_lc.csv` | Figure S1 | No |
| Frozen clock curves M0-M3 | SCI cd4bd328 `clock_fit_curves.csv` | Model scores and forecasts | No |
| SPHEREx peak of flare 37 (MJD 60936, 2-sigma 60931-60939) | SCI 8ce2fda4 | One timing point (60935.5 +/- 2.0) | One value |

SHA-256 of all inputs: `files/data/input_sha256.txt`. Terms: `files/NOTICE_external_data.md`.

We checked for new data on 2026-11-11: the HEASARC Swift master table has no visit of the source after 2026-02-05; the Fink (Rubin) and ALeRCE (Rubin) cone searches return no object within 5 arcsec; the Swift planning API timed out. The ASAS-SN light curve ends on 2025-02-07 (as found by SCI 049d6e3e).

## 3. Methods

**3.1 Flare fits** (`01_fit_asassn.py`, `02_fit_tess.py`, `flarelib.py`). ASAS-SN g data with quality G and flux error below 0.3 mJy are averaged per night (inverse-variance weights). For each flare we fit a window of -45 to +40 d around the published peak. Model S (one component): baseline + A x [exp(-(t - tp)^2 / 2 sigma^2) before tp, exp(-(t - tp)/tau) after tp]. Model P (two components): model S plus a linear ramp from 0 at ts to C at tp, which then declines with tau; the ramp must start before the 10 percent point of the main rise. A free white jitter is added to the errors. Priors: sigma 0.3-20 d, tau 2-80 d, tp within 15 d of the start value, ramp length 3-45 d, 0 <= C < 5A. We sample with emcee 3.1.6 (40 walkers, 1500 burn-in and 2500 steps, differential-evolution moves) from the best of 27 Nelder-Mead starts. Markers: half-rise th = tp - 1.177 sigma, peak tp, 10 percent onset tp - 2.146 sigma. TESS data are binned to 0.25 d, normalised by the median, and fitted in the same way.

**3.2 Lag calibration** (`03_lags_and_markers.py`). For cycles with an f30 dip and an optical fit (21, 22, 23, 24, 30, 31; cycles 19 and 25 have broad or bimodal dip posteriors and are not used), the lag is the optical marker posterior minus the dip posterior (split-normal from the 68 percent range). We fit a constant lag with a free intrinsic scatter (maximum likelihood). The UVW2 lag uses the UVW2 peaks of SCI 049d6e3e on cycles 20-24, 30, 31.

**3.3 Timing set** (`04_clock_models.py`). Cycles 12-38: the f30 dip where it exists; otherwise the half-rise minus 4.75 d with error sqrt(e_th^2 + 0.52^2) (the fitted lag scatter is 0). Rules for an optical point: at least one night within 5 d before and one within 5 d after th, half-rise error below 1.5 d, rise sigma at most 6 d. The calibration flares with precise lags have sigma 2.3-5.4 d. Flare 38 uses the TESS half-rise (TESS minus ASAS-SN offset of flare 14: -0.01 d; extra error 0.42 d). Flare 37 uses the SPHEREx peak minus the peak lag (10.35 +/- 1.18 d, scatter 2.08 d).

**3.4 Clock models.** Constant period; constant Pdot; step (sudden period change after cycle n_b); ramp (constant dP/dn after n_b); on-off-on (dP/dn = k1 before b1, 0 between b1 and b2, k3 after b2); on-off-on with k3 = k1; on-off-step (k1 before b1, 0, then a step after b2). Break cycles are profiled on integer grids and counted as parameters in the AIC. The timing jitter is free or fixed at 0.5 or 1 d. The frozen curves of SCI cd4bd328 (fitted there to a different marker set) get only a free offset. Robustness (`04b_robustness.sh`): with the broad flares included, without flare 34, 37 or 38, and with a lag scatter floor of 1 d.

**3.5 Shape tests** (`07_precursor_index.py`, `08_width_era_test.py`). The model-free precursor index is (median g flux 6-20 d before the dip) minus (median 30-50 d before), divided by the flare amplitude (bootstrap errors). The reference is the f30 dip where measured, else the dip time of the on-off-step clock, which does not use the broad flares. The rise-width test compares the one-component sigma in cycles 20-33 (constant X-ray clock of SCI 049d6e3e and 2b5fd32c) with the other cycles. We use two selections: (A) sigma and half-rise errors below 3 d; (B) the sampling rule of 3.3 only.

**3.6 Energy scale** (`06_energy_scales.py`). Delta E / E = (2/3) Delta P / P. The mass-loss kick scale is Delta M x G M R* / r_t^2 for Delta M = 0.003 Msun per flare (the scale of SCI edf8ce3b), with r_t = R* (M / M*)^(1/3).

## 4. Results

### 4.1 Which marker is locked to the dip

Table 1. Lag on the f30 dip of the same cycle (`files/results/lag_calibration.json`).

| Marker | Cycles | Mean lag (d) | chi2 / dof (no scatter) | ML excess scatter (d) |
| --- | --- | --- | --- | --- |
| Optical half-rise, one-component fit | 21, 22, 23, 24, 30, 31 | 4.75 +/- 0.52 | 1.6 / 5 | 0.0 |
| UVW2 peak (SCI 049d6e3e) | 20-24, 30, 31 | 5.51 +/- 0.37 | 2.5 / 6 | - |
| Optical peak, one-component fit | as above | 10.35 +/- 1.18 | 14.8 / 5 | 2.1 |
| Optical main half-rise, two-component fit | as above | 6.51 +/- 1.26 | 38.0 / 5 | 2.5 |
| Optical 10 percent onset, two-component fit | as above | 3.96 +/- 1.66 | 27.0 / 5 | 3.2 |

The two-component model is not preferred by BIC in most flares (`files/results/fits/asassn_fits.json`), and its split between precursor and main rise is not unique. The simple half-rise integrates over the rise and gives the stable lag.

### 4.2 The dip-referenced timing set

Table 2. Timing points relative to the constant X-ray clock t = 59738.74 + 108.437 (n - 26) MJD (`files/results/models/clock_points_full.csv`).

| n | Source | O-C (d) | Error (d) |
| --- | --- | --- | --- |
| 12 | ASAS-SN half-rise | -19.19 | 1.06 |
| 14 | ASAS-SN half-rise | -11.20 | 0.67 |
| 15 | ASAS-SN half-rise | -7.75 | 0.61 |
| 17 | ASAS-SN half-rise | -3.34 | 0.59 |
| 18 | ASAS-SN half-rise | -1.49 | 0.92 |
| 19-25 | X-ray f30 dip | -3.48, +0.01, +0.08, -0.26, -0.68, +1.16, -5.31 | 4.99, 0.43, 0.87, 0.76, 2.90, 2.24, 3.78 |
| 30, 31, 33 | X-ray f30 dip | -0.08, -0.33, +0.17 | 0.48, 0.67, 1.20 |
| 34 | ASAS-SN half-rise | -3.06 | 0.62 |
| 37 | SPHEREx peak | -6.39 | 3.12 |
| 38 | TESS half-rise | -7.51 | 0.68 |

Rejected by the rules (`clock_points_rejected_full.csv`): 26 (one night on each side, error 3.0 d), 27, 28, 29 and 32 (rise sigma 10.4, 12.6, 7.5 and 6.7 d). Their O-C values (-24.0, -8.2, -9.6, -4.7, -2.6 d) are early, while the UVW2 peaks of 27-29 are 3.8-5.1 d late (SCI 049d6e3e). The broad flares thus spread to both sides of the clock.

### 4.3 Clock models

![Figure 2](files/figures/fig3_oc_models.png)

**Figure 2.** (a) O-C of the dip-referenced timing set against the constant X-ray clock, with the two best piecewise clocks, a constant period, and the frozen M3 (precessing drag) and M2 (two-break) curves of SCI cd4bd328 (jitter 0.5 d). Open squares: broad-rise flares that the shape rule removes. (b) Zoom on 2024-2027; the grey band shows future cycles.

Table 3. Model comparison, cycles 12-38, 18 points (`files/results/models/clock_models_full.csv`). Delta AIC against the best model of each jitter column.

| Model | Breaks | Free jitter | 0.5 d | 1 d | Parameters (0.5 d jitter) |
| --- | --- | --- | --- | --- | --- |
| on-off-step | 21, 32 | 0.0 | 0.0 | 4.0 | P = 108.43 +/- 0.06 d, k1 = -0.53 +/- 0.04 d/cycle, step -1.23 +/- 0.20 d |
| on-off-on | 21, 29 | 1.0 | 0.7 | 4.4 | k1 = -0.52 +/- 0.04, k3 = -0.17 +/- 0.03 d/cycle |
| on-off-on, k3 = k1 | 22, 33 | 7.0 | 3.3 | 4.5 | k = -0.44 +/- 0.02 d/cycle |
| frozen M3 s = -1.5 (precessing drag) | - | 7.6 | 2.5 | 0.0 | offset only |
| frozen M2 (two breaks) | - | 19.2 | 22.1 | 9.9 | offset only |
| constant Pdot | - | 27.0 | 30.5 | 18.1 | k = -0.17 d/cycle |
| constant period | - | 58.9 | 354.7 | 190.5 | P = 108.66 d |

Table 4. Robustness of the post-2019 result (cycles 19-38; Delta AIC of a constant period and of frozen M2 against the best model; `files/results/models/log_*.txt`).

| Variant | Constant period (free / 0.5 / 1 d) | Frozen M2 (free / 0.5 / 1 d) |
| --- | --- | --- |
| Main | 18.9 / 32.1 / 17.3 | 15.5 / 26.2 / 13.1 |
| Broad flares included | 17.1 / 30.2 / 15.7 | 13.9 / 25.2 / 12.0 |
| Without flare 34 | 23.0 / 36.9 / 19.7 | 19.3 / 28.9 / 14.7 |
| Without flare 37 | 18.1 / 31.5 / 16.8 | 14.4 / 25.1 / 12.3 |
| Without flare 38 | 7.6 / 6.5 / 5.1 | 3.0 / 1.8 / 1.5 |
| Lag scatter floor 1 d | 19.1 / 22.1 / 14.5 | 14.4 / 13.0 / 9.1 |

Flare 38 (TESS) carries most of the weight against M2. Flare 34 alone still rejects a constant period by Delta AIC 5-8.

### 4.4 Flare shape and the clock eras

![Figure 3](files/figures/fig4_width_eras.png)

**Figure 3.** (a) Dip-referenced O-C with the on-off-step clock. (b) One-component rise sigma of each flare. (c) Model-free precursor index. Blue band: cycles 20-33, where the X-ray clock is constant (era taken from the X-ray dips only).

Table 5. Rise width by era (`files/results/rise_width_eras_*.json`).

| Selection | Constant era: N, median sigma | Decrease eras: N, median sigma | Mann-Whitney p (one-sided) | Permutation p | p without TESS |
| --- | --- | --- | --- | --- | --- |
| B: sampling rule | 10, 7.1 d | 7, 2.9 d | 0.012 | 0.011 | 0.016 |
| A: errors below 3 d | 8, 5.2 d | 7, 2.9 d | 0.036 | 0.028 | 0.041 |

The precursor index is 0.10-0.23 in cycles 24, 25, 27 and 28 (0.06 in 29), and between -0.12 and +0.01 in cycles 12, 14, 15, 17, 18, 21, 22, 31, 32 and 34 (`precursor_index.csv`). Cycle 11 (2017 December) gives 0.40, but its rise is poorly sampled (half-rise error 5.3 d) and its reference time is extrapolated from the model. The soft X-ray level 8-30 d before the dip was low in cycles 28-29 (0.14-0.16 NICER-equivalent count/s, against 0.5-1.1 in other cycles), in the same era.

### 4.5 Forecasts

Table 6. Frozen forecasts for jitter 0.5 d (`files/results/forecasts_41_44.csv`; dates UTC). Half-rise = dip + 4.75 d; UVW2 peak = dip + 5.51 d; optical peak = dip + 10.35 d.

| Model | n = 41 dip (MJD) | n = 41 half-rise | n = 41 UVW2 peak | n = 42 dip | n = 44 dip |
| --- | --- | --- | --- | --- | --- |
| on-off-step | 61354.0 +/- 1.4 (Nov 10) | Nov 14 | Nov 15 | 61461.2 +/- 1.5 (2027 Feb 25) | 61675.6 +/- 1.8 (2027 Sep 27) |
| on-off-on | 61352.0 +/- 1.6 (Nov 8) | Nov 12 | Nov 13 | 61458.2 +/- 2.0 (Feb 22) | 61670.1 +/- 2.7 (Sep 22) |
| frozen M3 s = -1.5 | 61350.1 +/- 0.6 (Nov 6) | Nov 10 | Nov 11 | 61455.4 +/- 0.6 (Feb 19) | 61665.1 +/- 0.6 (Sep 17) |
| frozen M2 | 61360.3 +/- 0.6 (Nov 16) | Nov 21 | Nov 21 | 61468.2 +/- 0.6 (Mar 4) | 61683.7 +/- 0.6 (Oct 5) |
| constant X-ray clock (049d6e3e) | 61365.3 (Nov 21) | Nov 26 | Nov 27 | 61473.7 (Mar 10) | 61690.6 (Oct 13) |

Step and ramp differ by 3 d at flare 42 and by 5.5 d at flare 44; M3 differs from the step by 6 d and from the ramp by 2.8 d at flare 42 and 5-10 d at flare 44. A narrow flare 41 with a half-rise before November 16 supports a shorter period; a half-rise after November 20 supports a constant period. We predict that the next flares have narrow rises (sigma below about 5 d) while the period decreases.

### 4.6 Energy scale of a sudden change

For M_BH = 10^7-10^7.86 Msun and M* = 1 Msun, a step of -1.23 d is Delta E / E = 0.0076, that is 7e48-3e49 erg, or 4.4 times the energy loss per orbit at the published Pdot (`energy_scales.json`). The energy scale of a mass-loss kick (0.003 Msun per flare) is 2.5e48-4.8e48 erg for R* = 1 Rsun and 1.2e47-2.4e47 erg for R* = 20 Rsun. A step therefore needs a kick efficiency of 3-6 times this scale for a Sun-like star and 60-110 times for a giant. The flares 32-34 did not have unusual amplitudes. Thus, if the change was a step, a single mass-loss kick is an unlikely cause for an evolved star; a ramp or the smooth M3 clock does not need a single large event.

## 5. Discussion

**The renewed decrease is real.** SCI 049d6e3e found early 2024-2026 markers with offsets calibrated on two flares. We tie the optical half-rise to the X-ray dip in six cycles and find a constant lag without excess scatter, and we remove broad flares with a fixed rule. The two narrow 2024-2026 flares then remain 3.1 and 7.5 d early. A flare-shape effect would need a lag change of 3-8 d in narrow flares, but narrow flares in 2020-2023 have constant lags within about 1 d.

**What the broad flares show.** The 2022-2023 flares had slow rises and optical precursors. Their half-rises are early and their UVW2 peaks are late, so a single shape change moves markers to both sides of the X-ray clock. This explains the 2022 optical peaks below the clock (SCI 049d6e3e) and the UVW2-only period decrease of SCI cd4bd328 (k = -0.26 d per cycle from late UVW2 peaks in 27-29). The X-ray dip of cycle 25 (f30 at -5.3 d, bimodal; SCI 2b5fd32c) agrees with an early, extended debris arrival in this era.

**Constraints for the physical clock.** (1) The clock switched off near cycle 21 and on again after cycle 29-32. A clock without a return to a decrease (M2) fails. (2) The precessing drag clock M3, fitted before our analysis to other markers, fits our independent timing set and predicts the earliest flare 41. (3) The flare shape changed in the same era: slow rises and precursors only while the period was constant. In a precessing orbit, the orientation of the orbit relative to the disc sets both the drag and the path of the returning debris, so both can change together. A mass-loss coupling would also link the shape and the period change, but SCI e5616202 and edf8ce3b showed that a coupling to flare energy fails. Our width-era association is a new test for both pictures: it must hold again in the next stall.

## 6. Limitations

- The lag calibration uses six cycles; cycles 23 and 30 have errors above 3 d. The lag of narrow flares before 2020 and after 2024 is assumed equal to the 2020-2023 lag. If narrow-flare lags differ by 3-8 d in those eras, the result changes.
- The shape rule (sigma at most 6 d) was chosen after we saw the broad 2022-2023 flares. It is the upper edge of the calibration range. Including the broad flares does not change the rejection of a constant period (Table 4).
- The renewed decrease rests on flares 34 and 38 and on one SPHEREx peak with a 3-d error. Without flare 38, M2 is not rejected.
- Step and ramp are not separable (Delta AIC 0.7). The early-rate return (k3 = k1) is disfavoured only for small jitter.
- The width-era test has 15-17 flares and p = 0.01-0.04; it uses era boundaries from earlier studies (X-ray clock), and the TESS width is in a different band.
- The frozen-curve forecasts include only the offset and jitter errors, not the uncertainty of the curve shapes. Our model forecasts include parameter covariance and jitter.
- The ASAS-SN photometry is aperture photometry with host light; camera offsets are not modelled (a free jitter absorbs scatter).
- No public data cover flares 35-36 in the optical or any flare after 2026 February in X-rays.

## 7. Reproduction

`files/code/run_all.sh <campaign_dir> <scratch_dir>` verifies the four input SCI bundles with `sci verify`, extracts the inputs into `<scratch_dir>/inputs`, checks their SHA-256 against `files/data/input_sha256.txt`, and runs all steps. Python 3.12 with numpy, scipy, pandas, matplotlib, astropy and emcee 3.1.6 (`pip install --no-deps --target <dir> emcee==3.1.6`, then add `<dir>` to PYTHONPATH). The ASAS-SN fits take about 40-70 min on one CPU; all other steps take less than 2 min. MCMC medians can change by Monte Carlo noise (below about 0.1 d for well-sampled flares) with other library versions.

Files:
- `files/code/`: all code (MIT). `modelbasis.py` is a copy of the model basis in `04_clock_models.py`, used by the figures.
- `files/data/input_sha256.txt`: hashes of the input files.
- `files/results/fits/`: flare-fit summaries (`asassn_fits.json`, `tess_fits.json`) and thinned posterior chains (columns: baseline, A, tp, ln sigma, ln tau, ln jitter[, C, ramp length]).
- `files/results/`: per-cycle marker table, lag calibration, precursor index, width-era tests, energy scales, forecasts.
- `files/results/models/`: timing points, model tables and logs for all variants.
- `files/figures/`: Figures 1-3 and Figure S1 (`fig1_flares_components.png`: ASAS-SN g flares 17-34 aligned on the X-ray clock with the one-component fit (dotted grey), the two-component fit (green) and its main part (dashed), X-ray rates (blue squares, right axis) and the f30 dip interval (blue band)).

## References

- Payne, A. V. et al. 2021, ApJ 910, 125 (arXiv:2009.03321).
- Payne, A. V. et al. 2022, ApJ 926, 142 (arXiv:2206.11278).
- Shappee, B. J. et al. 2014, ApJ 788, 48; Kochanek, C. S. et al. 2017, PASP 129, 104502; Hart, K. et al. 2023, arXiv:2304.03791 (ASAS-SN Sky Patrol v2).
- Foreman-Mackey, D. et al. 2013, PASP 125, 306 (emcee).
- Hinkle, J. T. et al. 2026, arXiv:2606.06578 (third flares of AT2020vdq and AT2022dbl).
- Campaign publications: SCI 049d6e3e, 2b5fd32c, b29ea789, cd4bd328, 8ce2fda4, e5616202, edf8ce3b, c2b0b0ea, 9398601f, 9817499f, 77860d3a, 252d5770 (full identifiers in `sci.json`).
