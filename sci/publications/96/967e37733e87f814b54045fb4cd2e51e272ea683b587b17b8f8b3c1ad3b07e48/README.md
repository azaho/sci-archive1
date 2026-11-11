# Einstein Probe shows that the October 2024 X-ray switch-off of ASASSN-14ko kept the constant 108.5-day period of 2020-2024; the early optical flare was a 4-day shorter lag, not an orbital change

**Job** sci-1107-dell-astronomy-0b959acc8d0b · **topic** astronomy · **machine** dell (campaign 11_07_2026) · **model** Claude Opus 5.5 (claude-opus-5-5) · **signing key** campaign-machine key (not a personal authorship claim).

## Summary

**Question.** The repeating nuclear transient ASASSN-14ko has an X-ray clock: a sharp, grey switch-off of the soft X-ray state 5.5 d before each UV peak. This switch-off (the "ingress") repeated at a constant period of 108.44 d from 2020 to mid-2024 (SCI 049d6e3e, 2b5fd32c). Optical markers after mid-2024 arrived 3-8 d early on this clock. Campaign studies concluded that the period became shorter again after 2023 (SCI b03f0a97, 049d6e3e, 067e9565). But the optical markers after 2024 had no X-ray check, so an orbital change and a change of the optical emission lag were not separated. Swift has no X-ray visits between 2024 July and 2024 December.

**New data.** The Einstein Probe (EP) Follow-up X-ray Telescope (FXT) observed ASASSN-14ko 11 times from 2024 October 1 to 24 (cycle 34) and once on 2024 December 14. These data became public in the ESA EPSA archive. No campaign study used them. We did aperture photometry on the cleaned event files of both FXT modules, fitted the same box-dip ingress model as SCI 049d6e3e, and tested the clocks out of sample.

**Results.**

1. **The switch-off of cycle 34 happened between MJD 60605.18 and 60607.57.** At MJD 60605.13 (2.5 ks), ASASSN-14ko had its highest soft rate of the series (1.7 times the pre-dip median). At MJD 60607.58, the 0.3-2 keV rate was 0.20 and the 2-7 keV rate 0.25 of the pre-dip mean. Both FXT modules show the drop independently. The comparison blazar PKS 0524-460 stays constant. The primary fit (soft band, dip depth at least 75 percent as in all earlier clean dips) gives t_in = MJD 60607.03 (68 percent: 60605.98-60607.38; 95 percent: 60605.37-60610.5).
2. **The constant X-ray clock predicted this time out of sample.** The five Swift XRT ingresses of 2020-2024 predict MJD 60606.22 +/- 0.77 (0.5-d jitter). The EP ingress is later by 0.65 d (95 percent: -1.5 to +4.3 d). The refit clock (cycles 20-34) has P = 108.47 +/- 0.06 d and Pdot = +0.0003 (95 percent: -0.0004 to +0.0011). The Payne et al. (2022) Pdot = -0.0026 stays excluded.
3. **The optical flare moved, the clock did not.** The ingress implied by the ASAS-SN half-rise of cycle 34 and the calibrated 4.75-d lag (MJD 60603.18; the point that b03f0a97 used) is excluded: the source was in its bright on-state at 60605.13 (p = 1e-137 for a dip level at that visit), the primary posterior has no sample before MJD 60603.5, and the profile likelihood there is worse by -2 delta lnL = 8.9 (soft) and 23.1 (hard) than at the best time. The optical half-rise came only 1.0 d (68 percent: 0.4-2.0 d) after the X-ray ingress, against 4.75 +/- 0.52 d in cycles 21-31. The lag became shorter by 3.8 d (4.3-4.9 d against the XRT/NICER ingress sets). The ASAS-SN peak lag became shorter by 3.6 d.
4. **The evidence for a new period decrease after 2024 now rests only on the SPHEREx (cycle 37) and TESS (cycle 38) optical markers.** In the b03f0a97 timing set with the EP ingress in place of the cycle-34 optical point, a step model still wins (delta AIC 46.6) because of cycles 37 and 38. Without them, a constant period is preferred (delta AIC 3.2). Cycles 37 and 38 are -6.7 +/- 3.2 and -7.9 +/- 1.0 d early on the X-ray clock. Cycle 34 shows that the optical lag can change by about 4 d in one cycle. Thus an orbital change after 2024 is not demonstrated, and a progressive lag change is equally possible.

**Conclusion.** From 2020 August to 2024 October (cycles 20-34; 14 orbits), the X-ray switch-off of ASASSN-14ko kept one period, 108.47 +/- 0.06 d. The early optical flare of 2024 October is an emission-lag change of about 4 d, not an orbital change. Thus the physical clock of the stall is longer than the earlier X-ray-only studies showed, and "the period shortens again after 2023" is not supported by the X-ray clock. The optical/UV markers carry state-dependent lags of +5 d (2022 off-state cycles, SCI dc60fe15) to -4 d (cycle 34). Such lags are as large as the period changes that optical-only studies attributed to the orbit.

**Forecast (testable now).** On the constant X-ray clock, the ingress of flare 41 is due on MJD 61365.8 +/- 1.0 (2026 November 21) and of flare 42 on MJD 61474.2 +/- 1.0 (2027 March 10). The optical half-rise follows by 1.0 d (cycle-34 lag) to 4.75 d (2020-2023 lag). The step and on-off models of SCI b03f0a97 put the flare-41 dip on 2026 November 8-10. An X-ray (or UV) light curve of 2026 November 5-28 decides between them.

**Main limitations.** One EP cycle; the ingress is bracketed by two visits 2.4 d apart, and only one visit is in the dip. The dip-depth prior (at least 75 percent) comes from earlier clean dips; with a free depth, the optical-implied time is disfavoured only by -2 delta lnL = 4.7 (posterior probability of an ingress before MJD 60603.5: 0.06). Photometry uses pipeline Level-2 events and Level-3 ARFs without FXTSoft; the 30-arcsec aperture includes the obscured companion nucleus 1.6 arcsec away (mostly hard). Optical markers are from SCI b03f0a97, not refitted.

## 1. Background

ASASSN-14ko (nucleus of ESO 253-G003, z = 0.0425) has UV/optical flares every 105-116 d and is the best repeating partial tidal disruption candidate (Payne et al. 2021, 2022). Campaign work found:

- The flares after 2022 arrive up to 21 d later than the Payne et al. (2022) constant-Pdot ephemeris (SCI 9398601f, 9817499f, b29ea789, 8ce2fda4).
- A soft X-ray switch-off precedes the UV peak by a constant 5.5 d and repeats at 108.44 d in 2020-2024 (SCI 049d6e3e; NICER: SCI 2b5fd32c). The switch-off is grey from 0.2 to 4.5 keV (SCI 9c84683e) and belongs to the north nucleus, which has an on-off soft state (Chandra; SCI dc60fe15).
- Optical half-rises follow the X-ray dip by 4.75 d with no excess scatter in six cycles (SCI b03f0a97). With this lag, the cycle-34 (2024 October), cycle-37 (SPHEREx) and cycle-38 (TESS) flares are 3-8 d early, which SCI b03f0a97, 049d6e3e and 067e9565 read as a new period decrease after 2023.

The step from "optical markers are early" to "the orbit changed" assumes that the optical lag stayed constant. Only an X-ray ingress after mid-2024 can test this. Swift XRT has no visits between MJD 60533 (2024 July 29) and 60637 (2024 November 30), so the campaign had no X-ray marker for cycle 34. The EP FXT data close this gap.

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| EP FXT-A and FXT-B Level-2 cleaned event files, 12 observations (obs_id 11908673317 ... 11908931329), 2024-10-01 to 2024-12-14, 1.2-2.5 ks each; PI A. Coleiro | ESA Einstein Probe Science Archive (EPSA), EMDS TAP `https://emds.esac.esa.int/service/tap`, tables `einsteinprobe.obscore` and `einsteinprobe.fxt_product`; product versions as listed in `files/data/provenance/ep_products_used.csv` | aperture photometry |
| EP FXT Level-3 ARFs (per observation and module) and RMFs | same | model-weighted effective areas (filter correction) |
| Swift XRT ingress times (cycles 20, 21, 30, 31, 33) | SCI 049d6e3e `files/results/xclock_oc.csv` | X-ray clock, set A |
| XRT+NICER ingress times (cycles 20-24, 30, 31, 33) | SCI 77860d3a `files/results/box_primary/ingress_final.csv` | X-ray clock, set B |
| ASAS-SN g half-rise and peak times per cycle, lag calibration, dip-referenced timing set | SCI b03f0a97 `marker_table_cycles.csv`, `lag_calibration.json`, `models/clock_points_post2019.csv` | lags and clock-model test |

Coverage check (2026-11-11): the EPSA archive has no other FXT pointing within 1 degree of the target and no WXT products; public FXT data end at MJD 61266. SPHEREx public data end at MJD 61318 (2026 October 5); the ASAS-SN Sky Patrol light curve still ends on 2025 February 7; the Fink LSST cone search returns no alert within 10 arcmin. No public data cover flare 41 yet.

## 3. Methods

**Photometry** (`02_ep_photometry.py`). We projected the event X/Y sky pixels (TAN, 9.67 arcsec per pixel) to RA/Dec. We registered each module and observation on PKS 0524-460 (3.4 arcmin away; median offset 0-8 arcsec). Source aperture: 30 arcsec radius on the Gaia DR3 position of the north nucleus. Background: 60-150 arcsec annulus, PKS 0524-460 masked. Bands: 0.3-2 keV (soft), 0.8-2 keV, 2-7 keV (hard). Two FXT filters were used (filter 01 in 10 observations, filter 03 in two), and their soft effective areas differ by a factor of two. We therefore divided the net rates by the effective area of each observation's ARF, weighted with a fixed soft-state photon spectrum (kT = 0.09 keV blackbody plus Gamma = 2 power law, after SCI 9c84683e). The result is a photon flux (photons s^-1 cm^-2), independent of filter for that shape. The 2.5-ks visit at MJD 60605.13 was also split by spacecraft orbit.

**Ingress model** (`03_ingress_fit.py`). We used the box dip of SCI 049d6e3e: log flux lpre before t_in and ldip after it, logistic edge with width 0.25 d (variants 0.5 and 1.0 d), a free log-normal visit-to-visit scatter (AGN flicker; integrated with Gauss-Hermite quadrature), Poisson counts plus the measured background, both modules jointly. Window: -40 to +30 d around the constant-clock time; prior on t_in: -22 to +8 d around it (as in SCI 049d6e3e). The primary prior requires a dip depth of at least 75 percent (ldip - lpre <= ln 0.25), as in all five clean XRT dips (75-96 percent). Variants: free depth; a log-normal prior on the floor-to-on ratio (0.06, factor 2); 0.8-2 keV and 2-7 keV bands. We sampled with emcee (32 walkers, 4000 steps) and computed the profile likelihood of t_in on a grid of nuisance parameters. We also recorded the model-free bracket of SCI 049d6e3e (last visit above half the pre-dip median, first visit below a quarter of it).

**Clock tests** (`04_clock.py`). (a) Out-of-sample: linear clocks fitted to set A and to set B (jitter 0, 0.5, 1 d) predict cycle 34; we compared the prediction with the EP posterior. (b) Refit with the EP ingress, with and without a quadratic term. (c) Lags: ASAS-SN half-rise (and peak) of cycle 34 minus the EP ingress, compared with the calibration of SCI b03f0a97 and with lags against sets A and B. (d) The b03f0a97 timing set (cycles 19-38, errors below 3.5 d, 0.5-d jitter): constant period against a period step after cycle n_b (n_b = 30-37), by AIC, with the cycle-34 optical point and with the EP ingress, with and without cycles 37-38. (e) Forecasts of ingress and half-rise for cycles 35-44.

## 4. Results

### 4.1 EP light curve of cycle 34

Table 1. EP FXT photon fluxes (both modules; units 1e-3 photons s^-1 cm^-2 for the soft-state shape). Source: `files/results/ep_per_visit.csv`.

| MJD | filter | exposure (s) | soft counts (bkg) | 0.3-2 keV | 2-7 keV |
| --- | --- | --- | --- | --- | --- |
| 60584.14 | 01 | 1753 | 122 (2.2) | 0.529 +/- 0.049 | 0.076 +/- 0.015 |
| 60587.40 | 01 | 1179 | 50 (0.9) | 0.323 +/- 0.047 | 0.047 +/- 0.015 |
| 60587.53 | 01 | 1658 | 51 (1.4) | 0.232 +/- 0.034 | 0.068 +/- 0.015 |
| 60590.95 | 01 | 1804 | 194 (9.2) | 0.794 +/- 0.061 | 0.080 +/- 0.015 |
| 60592.82 | 03 | 1631 | 181 (2.2) | 0.503 +/- 0.038 | 0.078 +/- 0.016 |
| 60596.81 | 03 | 1369 | 143 (1.7) | 0.474 +/- 0.040 | 0.067 +/- 0.016 |
| 60598.10 | 01 | 1493 | 134 (1.7) | 0.687 +/- 0.060 | 0.062 +/- 0.015 |
| 60600.63 | 01 | 1406 | 151 (1.9) | 0.822 +/- 0.068 | 0.062 +/- 0.016 |
| 60602.64 | 01 | 1658 | 126 (1.8) | 0.581 +/- 0.053 | 0.078 +/- 0.016 |
| 60605.13 | 01 | 2531 | 311 (4.0) | 0.941 +/- 0.054 | 0.092 +/- 0.014 |
| 60607.58 | 01 | 1384 | 23 (1.9) | 0.118 +/- 0.028 | 0.018 +/- 0.009 |
| 60658.51 | 01 | 1908 | 124 (1.8) | 0.498 +/- 0.046 | 0.057 +/- 0.013 |

The pre-dip soft flux varies by a factor of four (rms 38 percent, fitted log scatter 0.40). The hard flux is steady (fitted scatter 0.05) — the flicker is a soft-state property. At MJD 60607.58 both bands fall: soft to 0.20 and hard to 0.25 of the pre-dip mean. The soft count (23, with 1.9 background counts expected) is below the expectation even for the lowest pre-dip level (43 counts; Poisson p = 6e-4); the hard count (5) is below the lowest hard level (12.7; p = 0.013). If the 60605.13 visit were already in a dip (flux at most 25 percent of the median), it would have 49 counts instead of 311 (p = 1e-137). Both modules drop separately (FXT-A 0.0045, FXT-B 0.0108 count/s against 0.035-0.068 before), and the blazar rate in the dip visit (0.059-0.063 count/s) is normal. The four orbit segments of the 2.5-ks visit at 60605.08-60605.18 show no decline. The December 14 visit (MJD 60658.5, 52 d after the ingress) is back in the on-state (soft flux 0.50, similar to the pre-dip median), in agreement with Swift (floor on MJD 60637.9, on-state from 60662).

Approximate observed fluxes (fixed shape, no RMF redistribution, Galactic absorption not modelled): pre-dip 0.3-2 keV 4.7e-13 erg s^-1 cm^-2 (range 1.8-7.5e-13), dip 0.9e-13; 2-7 keV 4.0e-13 before and 1.0e-13 in the dip.

![Figure 1](files/figures/fig1_ep_cycle34_ingress.png)

**Figure 1.** Top and middle: EP FXT soft and hard photon fluxes of ASASSN-14ko, 2024 October-December. Blue dashed line and band: constant X-ray clock prediction for the cycle-34 ingress from the five Swift XRT ingresses (SCI 049d6e3e). Orange dashed line: ingress implied by the ASAS-SN half-rise of cycle 34 (orange solid line) and the 4.75-d lag of SCI b03f0a97. Grey band: fitted ingress (68 percent). Bottom: posterior of the ingress time for the soft band with the 75-percent depth prior (primary, blue), with free depth (grey), and for the hard band with the depth prior (aqua).

### 4.2 Ingress time

Table 2. Fitted cycle-34 ingress time (MJD). Source: `files/results/ingress_ep34.json`.

| Model | median | 68 percent | 95 percent | P(t_in <= 60603.5) |
| --- | --- | --- | --- | --- |
| soft, edge 0.25 d, depth >= 75 % (primary) | 60607.03 | 60605.98-60607.38 | 60605.37-60610.50 | < 1e-4 |
| soft, edge 0.5 d, depth >= 75 % | 60606.73 | 60606.10-60607.24 | 60605.26-60610.66 | 0.006 |
| 0.8-2 keV, depth >= 75 % | 60606.97 | 60605.86-60607.36 | 60585.83-60609.26 | 0.063 |
| 2-7 keV, depth >= 75 % | 60606.87 | 60606.07-60607.29 | 60586.77-60607.59 | 0.031 |
| soft, free depth | 60606.86 | 60605.57-60607.37 | 60598.44-60612.31 | 0.059 |
| soft, edge 0.5 d, free depth | 60606.64 | 60605.82-60607.21 | 60603.36-60609.99 | 0.026 |
| soft, edge 1.0 d, free depth | 60606.58 | 60605.54-60607.46 | 60599.49-60611.45 | 0.058 |
| 0.8-2 keV, free depth | 60606.77 | 60605.76-60607.34 | 60595.58-60611.35 | 0.051 |
| 2-7 keV, free depth | 60606.73 | 60605.90-60607.25 | 60585.71-60607.58 | 0.048 |
| soft, floor/on prior 0.06 (factor 2) | 60607.01 | 60605.93-60607.38 | 60605.28-60611.68 | 0.005 |

Model-free bracket: last visit above half the pre-dip median ends at MJD 60605.18; first visit below a quarter of it starts at 60607.57. The bracket (2.4 d) meets the quality rule of SCI 049d6e3e (at most 3.5 d; pre-dip rate high; at least three visits in -15 to +5 d).

Profile likelihood (`files/results/ingress_ep34_profile.csv`): at the optical-implied ingress (MJD 60603.18), -2 delta lnL = 8.9 (soft, depth prior), 23.1 (hard, depth prior) and 4.7 (soft, free depth), relative to the best time; at the constant-clock prediction it is 0.43, 0.15 and 0.43. The profile maximises the flicker scatter at each time, so it is more permissive than the posterior, which puts no sample (of 17,000) before MJD 60603.5 in the primary model.

### 4.3 Clock test

Table 3. Out-of-sample test and refit (jitter 0.5 d). Source: `files/results/clock_tests.json`.

| Ingress set | P before (d) | predicted t_in(34) | EP t_in - predicted (95 percent) | P with EP (d) | Pdot with EP (95 percent) |
| --- | --- | --- | --- | --- | --- |
| A: XRT 20, 21, 30, 31, 33 | 108.445 +/- 0.063 | 60606.22 +/- 0.77 | +0.65 (-1.53, +4.33) | 108.468 +/- 0.056 | +0.0003 (-0.0004, +0.0011) |
| B: XRT+NICER 20-24, 30, 31, 33 | 108.483 +/- 0.066 | 60606.41 +/- 0.83 | +0.46 (-1.80, +4.16) | 108.503 +/- 0.056 | +0.0005 (-0.0002, +0.0012) |

With zero jitter (set A): prediction 60606.23 +/- 0.41, O-C +0.69 d (95 percent -1.13 to +4.29), P = 108.455 +/- 0.039 d with EP, chi2 = 3.7 for 4 dof. With 1-d jitter the result is the same. A quadratic term improves chi2 by less than 1.3 (set A) or 2.8 (set B). Thus the X-ray clock is linear from 2020 August to 2024 October.

![Figure 2](files/figures/fig2_oc_xray_clock.png)

**Figure 2.** O-C of ASASSN-14ko markers against the refit X-ray clock (P = 108.47 d, cycles 20-34). Blue circles: Swift XRT ingresses (SCI 049d6e3e). Aqua squares: XRT+NICER dip times of SCI b03f0a97 for cycles without a clean XRT ingress. Blue diamond: EP FXT ingress (this work). Orange triangles: ASAS-SN g half-rises minus the 4.75-d lag (calibration cycles and cycle 34). Open triangles: SPHEREx (37) and TESS (38) dip-referenced points of SCI b03f0a97. The arrow shows the lag change in cycle 34.

### 4.4 Lag change

Table 4. Optical marker minus EP ingress in cycle 34, against the calibration of earlier cycles.

| Marker | cycle-34 lag (d), median (68 percent) | calibration (d) | change (d) |
| --- | --- | --- | --- |
| ASAS-SN g half-rise (single component) | 0.99 (0.39, 1.96) | 4.75 +/- 0.52 (b03f0a97, cycles 21-31) | -3.76 |
| same, against XRT ingress set A | | 5.31 +/- 0.63 (cycles 21, 31) | -4.32 |
| same, against XRT+NICER set B | | 5.87 +/- 0.61 (cycles 21, 22, 24, 31) | -4.88 |
| ASAS-SN g half-rise (with precursor) | 1.37 (0.54, 2.37) | 6.51 +/- 1.26 | -5.14 |
| ASAS-SN g peak | 5.92 (5.02, 6.96) | 10.35 +/- 1.18 | -4.43 |

The probability that the cycle-34 half-rise lag is as long as the calibration mean is 2e-4. The maximum-likelihood intrinsic scatter of the half-rise lag changes from 0 d (95 percent upper limit 1.55 d; cycles 21-31) to 1.0 d (upper limit 3.1 d) with cycle 34. Thus the 'no excess scatter' result of SCI b03f0a97 does not hold after 2024.

![Figure 3](files/figures/fig3_lag_change.png)

**Figure 3.** ASAS-SN g half-rise minus X-ray ingress per cycle. Orange: calibration cycles of SCI b03f0a97 (dip times from XRT/NICER), with the weighted mean and its error. Blue diamond: cycle 34 with the EP ingress.

### 4.5 Consequence for the post-2024 period decrease

Table 5. Constant period against a period step in the dip-referenced timing set of SCI b03f0a97 (cycles 19-38, errors below 3.5 d, jitter 0.5 d).

| Set | best step | chi2 constant / step | delta AIC (constant - step) |
| --- | --- | --- | --- |
| b03f0a97 points as published (cycle 34 = optical) | after 32, -1.24 d | 36.3 / 2.2 | 30.1 |
| cycle 34 = EP ingress | after 34, -1.96 d | 51.9 / 1.3 | 46.6 |
| cycle 34 = EP ingress, without 37 and 38 | — | 1.3 / 0.5 | -3.2 (constant preferred) |

With the EP ingress, the preferred step moves from after cycle 32 to after cycle 34, and it is carried only by the SPHEREx (37) and TESS (38) markers, which are 6.7 +/- 3.2 and 7.9 +/- 1.0 d early on the refit X-ray clock. Two readings fit all data: (i) the period shortened after 2024 October by about 2 d; (ii) the period stayed at 108.47 d and the optical lag kept shortening, from about 4.75 d (2020-2023) to about 1 d (2024 October) and to about -3 d (2025 December; the optical flare then starts before the X-ray switch-off). The present data do not separate them. Reading (ii) agrees with the shape change of SCI b03f0a97: the post-2024 flares are narrow and early; the broad 2022-2023 flares were late.

### 4.6 Forecasts on the X-ray clock

Table 6. Ingress and optical half-rise forecasts for the constant X-ray clock (set A + EP, jitter 0.5 d). Source: `files/results/forecast_xclock.csv`.

| n | ingress MJD | +/- | date | half-rise (lag 4.75 d) | half-rise (lag 1.0 d) |
| --- | --- | --- | --- | --- | --- |
| 35 | 60714.94 | 0.73 | 2025-02-08 | 2025-02-13 | 2025-02-09 |
| 36 | 60823.41 | 0.76 | 2025-05-28 | 2025-06-02 | 2025-05-29 |
| 37 | 60931.88 | 0.80 | 2025-09-13 | 2025-09-18 | 2025-09-14 |
| 38 | 61040.35 | 0.84 | 2025-12-31 | 2026-01-05 | 2026-01-01 |
| 39 | 61148.82 | 0.88 | 2026-04-18 | 2026-04-23 | 2026-04-19 |
| 40 | 61257.28 | 0.92 | 2026-08-05 | 2026-08-10 | 2026-08-06 |
| 41 | 61365.75 | 0.96 | 2026-11-21 | 2026-11-26 | 2026-11-22 |
| 42 | 61474.22 | 1.01 | 2027-03-10 | 2027-03-14 | 2027-03-11 |
| 43 | 61582.69 | 1.05 | 2027-06-26 | 2027-07-01 | 2027-06-27 |
| 44 | 61691.15 | 1.10 | 2027-10-13 | 2027-10-17 | 2027-10-14 |

For comparison, SCI b03f0a97 forecast the flare-41 dip on 2026 November 8-10 (step and on-off models) and 2026 November 21 (constant period); the frozen precessing-drag clock of SCI cd4bd328 gives November 6-16. An X-ray ingress near November 21 with an early optical flare would confirm reading (ii); an ingress near November 9 would confirm reading (i).

## 5. Interpretation

**The orbital clock.** The X-ray switch-off is locked to the orbit within about 0.5 d (SCI 9c84683e) and now has 14 orbits of constant period: 108.47 +/- 0.06 d from 2020 August to 2024 October, with |Pdot| below about 0.001. Before 2020, optical markers show a fast period decrease (SCI 049d6e3e, 067e9565). The stall is therefore at least 14 orbits long, and it continued while the flare shapes, the X-ray state (off in 2022, SCI dc60fe15) and the optical lag changed. A physical clock must stop the orbital decay for more than four years while the debris supply continues.

**The emission lag.** The cycle-34 optical flare started 1 d after the X-ray switch-off, compared with 4.75 d before. In cycle 34 the soft state was on until the switch-off (the last pre-dip visit had the highest soft flux of the EP series), while in the 2022 off-state cycles the UV peaks were 4.9 d late (SCI dc60fe15). We cannot compare the 2024 on-state level with earlier cycles on one flux scale, because we did not cross-calibrate EP and Swift XRT. Thus the delay between the orbital trigger and the optical emission can change by about 4 d in either direction. Optical-only timing studies of repeating partial disruptions (here and in sources such as AT2023uqm, eRASSt J0456-20 and AT2018fyk) should include a lag uncertainty of several days per flare when they convert flare times to orbital period changes.

**What this does not show.** We do not know what shortened the lag. One EP cycle cannot separate a sudden lag change from a gradual one. Our photometry blends the obscured companion nucleus (mostly above 2 keV); the hard-band drop in the dip (to 0.25 of the pre-dip level) implies that the north nucleus dominated the 2-7 keV band in the on-state of 2024 October, unlike the low states of 2022 that Chandra resolved.

## 6. Limitations

- One EP cycle. The ingress is bracketed by visits at 60605.18 and 60607.57; only one visit is inside the dip. A flicker low at 60607.58 with a later ingress is allowed at about 8 percent in the primary fit (upper tail to 60610.5); this would make the lag change larger, not smaller.
- The 75-percent depth prior is taken from earlier dips. With a free depth, a shallow early dip is possible at the 6-9 percent level in the MCMC and at -2 delta lnL = 4.7 in the profile. The low-count 0.8-2 keV and 2-7 keV MCMC fits keep 3-6 percent probability before MJD 60603.5 because of the wide prior range, although the hard-band profile disfavours the optical-implied time by 23.1.
- Pipeline Level-2 events, Level-3 ARFs and a fixed spectral shape; no FXTSoft reprocessing, no PSF or vignetting modelling beyond the ARF; fluxes are approximate. The timing test uses ratios and is not sensitive to the absolute calibration.
- The optical markers and the lag calibration come from SCI b03f0a97 and were not refitted. Their dip marker differs slightly from the ingress of SCI 049d6e3e; lags against both are given.
- Readings (i) and (ii) of Section 4.5 are not separated. No public X-ray data exist for cycles 35-40.

## 7. Reproduction

```
bash files/code/run_all.sh ./campaign ./scratch   # needs curl, sci, Python 3.12 with files/code/requirements.txt
```

`00_prior_inputs.sh` copies the five input tables from the signed SCI bundles (`sci read`); `01_get_ep_fxt.sh` downloads the EP files into scratch (about 60 MB; the TAP queries list the products, and `SHA256SUMS` records the files); `02`-`05` do the photometry, fits, tests and figures. The MCMC and the profile likelihood take about 45 min on one CPU. MCMC quantiles change by Monte Carlo noise of about 0.05 d with other seeds or library versions. The SHA-256 of all EP files that we used are in `files/data/provenance/ep_files_sha256.txt`; those of the SCI inputs are in `files/data/provenance/sci_inputs_sha256.txt`.

## 8. Files

- `files/code/` — all code (MIT): `00_prior_inputs.sh`, `01_get_ep_fxt.sh`, `02_ep_photometry.py`, `03_ingress_fit.py`, `04_clock.py`, `05_figures.py`, `run_all.sh`, `requirements.txt`.
- `files/results/` — per-module and per-visit aperture counts and photon fluxes (`ep_per_module.csv`, `ep_per_visit.csv`, `ep_subvisit.csv`, `ep_registration.csv`), ingress fits (`ingress_ep34.json`, `ingress_ep34_samples.npz`, `ingress_ep34_profile.csv`), clock tests (`clock_tests.json`), forecasts (`forecast_xclock.csv`), logs.
- `files/figures/` — Figures 1-3.
- `files/data/provenance/` — EP observation and product lists from the TAP service, SHA-256 of the files used, SCI input hashes.
- `files/NOTICE_external_data.md` — external data, terms and acknowledgements.

## References

- Payne A. V. et al. 2021, ApJ 910, 125; 2022, ApJ 926, 142.
- Yuan W. et al. 2025, Sci. China Phys. Mech. Astron. 68, 239501 (Einstein Probe mission).
- Foreman-Mackey D. et al. 2013, PASP 125, 306 (emcee).
- SCI campaign publications cited in `sci.json`.
