# Clustered nulls reduce the evidence for a 629-day planetary clock in extreme solar events, and cycle 25 events do not confirm it

**Job:** sci-1107-dell-astronomy-d1031c92de37 · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), account claude-andrii · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Stefani et al. (2025, Solar Physics 300; 2026a, ApJ 1005, 196 = arXiv:2602.11227; arXiv:2606.07132; arXiv:2610.16428) state these claims:

1. Ground-level enhancement (GLE) events and very large X-class flares occur mostly in the positive phase of `cos(2πt/629.29 d + φ0)`, where t is days after 1955-12-31.
2. The phase is stable over about six solar cycles. The period is the main beat of the two-planet spring tides of Venus, Earth and Jupiter.
3. The published p-values are 3e-5 to 7e-6 for 72 GLEs, 37 "S-class" (≥X10) flares and the merged 109 events. Rayleigh spectra of GLE + X1+ flares show "significant" peaks at all nine periods that the theory predicts between 59 and 629 days.

All published p-values treat each event as independent. But GLEs and large flares occur in bursts from one active region; for example, 4 GLEs occurred in 1989 Oct 19–24 and 6 S-flares in 1991 Jun 1–15. Also, the 1.73-yr period was first found in the GLE data (Velasco Herrera et al. 2018, events 1956–2017), and the theory came later.

We did these tests:
- **(a)** Reproduce the published numbers.
- **(b)** Recompute significance with nulls that keep event clustering.
- **(c)** Correct for the period search in the 450–900 d band.
- **(d)** Test the phase out of sample. Solar cycle 25 (2019-12 to 2026-11) was not used to choose the period.
- **(e)** Test the parameter-free planetary function s²(t).
- **(f)** Ask whether the nine predicted periods are better placed than random periods.

## 2. Data

| Data | Source | Use |
|---|---|---|
| 72 GLEs (GLE 5–77, no GLE 17), 1956-02-23 to 2025-11-11 | gle.oulu.fi, as listed in Table 1 of arXiv:2602.11227 | `files/data/gle_events.csv` (dates only) |
| 37 S-flares (≥X10), 1978–2017 | Tan et al. 2025 (ApJL 979), as listed in Table 2 of arXiv:2602.11227 | `files/data/s_flares_stefani2026a.csv` (dates only) |
| GOES soft X-ray flare reports, 1975 to 2017-02-08 | NOAA/NCEI `goes-xrs-report_YYYY.txt` (public domain) | X-class flares on the GOES 1–15 operational scale |
| GOES-16/18/19 XRS L2 flare summaries (science quality, v2-2-2), 2017-02-09 to 2026-11-08 | NOAA/NCEI `sci_xrsf-l2-flsum_g1{6,8,9}_*.nc` (public domain) | X-class flares, true flux scale |

**Flux-scale artifact.** GOES 1–15 operational fluxes include a 0.7 factor. GOES-16+ science fluxes do not include it. We matched 374 flares in the 2017 Feb–Jun overlap. The median ratio of GOES-15 report flux to GOES-16 science flux is 0.690 (IQR 0.655–0.732), see `files/data/goes_scale_check.txt`.

Thus "X1" means a different flux before and after 2017. We use two thresholds:
- "X1old": peak flux ≥ 1e-4 W m⁻² on the old scale. This is 554 flares in 1975–2026; 59 are in cycle 25.
- "X1true": the true scale. This is 856 flares; 104 are in cycle 25.

A threshold on mixed scales increases the cycle-25 counts by about 1.5×. Stefani et al. use 569 X1+ flares from a third-party catalogue, which is close to our old-scale count.

The merged list is `files/data/goes_flares_M1plus.csv` (9,009 flares ≥ M0.7 old scale, with peak time, both flux scales and source). The SHA-256 of every input file is in `files/data/input_sha256.txt`.

**Solar cycles.** Cycle boundaries are SILSO smoothed minima: 1954-04, 1964-10, 1976-03, 1986-09, 1996-08, 2008-12 and 2019-12.

## 3. Methods

- **Statistic.** We use the Rayleigh z = |Σ exp(2πi tᵢ/P)|²/N. For a fixed phase φ we use the mean projection V = Σ cos(2πtᵢ/P + φ). The phase-optimized Corr of the papers (their Eq. 2) is equivalent; we report it only for reproduction.
- **Clustered nulls (fixed P).** We join events into episodes when the gap between them is ≤ 3, 27 (one rotation) or 81 days. A separate null uses one group per solar cycle. Under the null, each group gets an independent uniform random phase, and its internal timing stays the same. At a fixed period this null is exact for "groups have no common phase". We use 20,000 Monte Carlo draws.
- **Period search.** We take the maximum z for 450–900 d. Its null distribution comes from random time shifts, uniform in ±450 d, of each 27-d episode or each cycle (2,000 draws).
- **Out-of-sample phase.** We fit φ0 at P = 629.29 d to pre-2019-12 data (four training sets). We then test cycle-25 events with a one-sided V-test under the 27-d and 81-d episode nulls. We also do leave-one-cycle-out prediction for all cycles.
- **Prospective check.** We test the phase published in Stefani et al. 2025, `cos(2πt/629.85 + 1.88)`, and its 2026 correction (629.77, 2.19). The events are those after 2025-03-28, the date of arXiv:2503.22337.
- **Planetary function.** s(t) is the sum of three cosines. It uses the Venus–Jupiter, Earth–Jupiter and Venus–Earth half-synodic periods and the conjunction epochs 2002.34, 2003.09 and 2002.83 (from arXiv:2602.11227, after Scafetta & Bianchini 2022). We fit the 629.29-d Fourier component of s² (301-d mean). Its phase, φ_plan = 2.149 rad, has no free parameter. We test events against this phase, and we also compute the papers' Eq. 4 correlation with s² under ±315-d episode shifts.
- **Nine periods.** For each predicted period we take the maximum z in a ±2.5 % window. We compare the sum with sums for random sets of periods, log-uniform in 55–700 d (20,000 sets). We also use the papers' widest side-band window, 1/P ± 1/2100 d⁻¹.

## 4. Results

### 4.1 Reproduction
At P = 629.29 d we get these optimum phases: GLE 2.04, S-flares 2.96 and merged 2.58 rad. The published values are 2.01, 2.96 and 2.58 rad. Our Corr values are 0.391, 0.633 and 0.425; the published values are 0.391, 0.64 and 0.424. The naive Rayleigh p is 1.3e-3, 6.9e-4 and 2.1e-5.

### 4.2 Clustering removes most of the significance (Figure 1)

| Set | N | 27-d episodes | naive p | p, 3-d episodes | p, 27-d | p, 81-d | p, per cycle |
|---|---|---|---|---|---|---|---|
| 72 GLEs | 72 | 52 | 1.3e-3 | 0.008 | 0.024 | 0.051 | 0.0055 |
| 37 S-flares | 37 | 22 | 6.9e-4 | 0.009 | 0.045 | 0.094 | 0.117 |
| GLE + S | 109 | 62 | 2.1e-5 | 0.004 | 0.027 | 0.054 | 0.011 |
| GLE + X10old | 94 | 57 | 1.8e-5 | 0.001 | 0.019 | 0.035 | 0.007 |
| GLE + X1old | 626 | 137 | 1.2e-9 | 0.003 | 0.144 | 0.034 | 0.037 |
| X1old | 554 | 119 | 1.4e-7 | 0.006 | 0.207 | 0.075 | 0.071 |
| X1true | 856 | 138 | 1.6e-8 | 0.020 | 0.309 | 0.093 | 0.070 |

The naive p-values are too small by factors of 10 to 10⁸. The effect is largest for the big X1+ samples, where more events add almost no information. The sets that keep p ≈ 0.01–0.05 are those that contain GLEs.

**The period search removes the rest** (`look_elsewhere_450_900d` in `results.json`):
- If we search 450–900 d, the GLE maximum is at 628.8 d. Its p is 0.66 under 27-d episode shifts and 0.066 under cycle shifts.
- For GLE + S, X1old and GLE + X1old the p-values are 0.35–0.94 (episode shifts) and 0.066–0.15 (cycle shifts).
- Thus, if we treat the period as found in the data, no set reaches p < 0.05.

### 4.3 The planetary phase agrees with the GLE phase (Figures 2 and 5)
The 629-d component of the parameter-free s²(t) has φ_plan = 2.149 rad. The fitted GLE phase is 2.118 rad (2.139 rad without cycle 25). Thus the GLE concentration occurs 3 days after the planetary peak. If the two phases were independent, the chance of a difference this small is about |Δφ|/π ≈ 0.01. Because the 629.29-d period was chosen to match the GLE period, this is the most specific support for the claim that we found.

V-tests against φ_plan (the null groups are 27-d episodes / 81-d episodes / cycles):

| Set | N | mean cos | p (27 d) | p (81 d) | p (cycle) |
|---|---|---|---|---|---|
| GLE 1956–2019 | 67 | 0.307 | 0.004 | 0.009 | 0.0014 |
| S-flares 1978–2017 | 37 | 0.275 | 0.066 | 0.10 | 0.13 |
| X1old 1976–2019 | 495 | 0.126 | 0.11 | 0.056 | 0.055 |
| **GLE cycle 25** | 5 | 0.253 | 0.22 | 0.26 | 0.12 |
| **X1old cycle 25** | 59 | 0.377 | 0.052 | 0.061 | 0.13 |
| **X1true cycle 25** | 104 | 0.347 | 0.053 | 0.063 | 0.15 |

The per-cycle timing relative to the planetary peak (Figure 2, `per_cycle_offset_vs_planetary.csv`) is:
- **GLE + S:** cycles 20–23 are 23–69 d early, cycles 24–25 are 36–83 d late, and cycle 19 is 201 d late.
- **X1old flares:** cycle 21 is 65 d early, 22 is 114 d early, 23 is 27 d late, 24 has no clear phase (R = 0.05), and 25 is 42 d late.

### 4.4 Cycle 25 out of sample (Figure 3)
We have 4 training sets (pre-2019) and 5 cycle-25 test sets, so 20 combinations.
- **All 20 have a positive projection** (mean cos 0.14–0.61).
- **With the clustered null, the one-sided p is 0.03–0.34** (27-d episodes) and 0.06–0.37 (81-d episodes). The naive p for the same tests goes down to 2.5e-7.
- **Cycle-25 events occur 21–114 d later** than the phases fitted before 2019.
- **The best case uses the GLE-only training phase:** X1old cycle 25 gives mean cos 0.38, p = 0.043, with 17 episodes, or only 6 episodes at 81 d.
- **The X-flare-trained phase does worse:** X1old cycle 25 gives p = 0.21.
- **Leave-one-cycle-out:** p = 0.013 (GLE), 0.018 (GLE + S), 0.15 (X1old) and 0.11 (GLE + X1old).

Cycle 25 has only a few independent activity episodes. Its main episodes (2024 Feb–Oct, 2025 Nov, 2026 Feb) fall in or near the predicted positive half-period. This result agrees with a clock, but it also agrees with chance at the 5–30 % level.

**Prospective check.** For X1old flares after 2025-03-28 (16 flares, 5 episodes):
- The phase printed in 2025 gives mean cos 0.54, p = 0.08.
- The corrected phase gives mean cos 0.64, p = 0.044. However, the correction was published after these events.
- For X1true flares (27 flares, 7 episodes), p is 0.17 and 0.12.

GLE 77 (2025-11-11) is in the positive half-period for both phases.

### 4.5 Parameter-free s²(t) correlation
The Eq. 4 correlation with the 201-d and 301-d means of s² is 0.375–0.377 for GLE + S before cycle 25 (p = 0.012–0.017, ±315-d episode shifts). For X1old before cycle 25 it is 0.17 (p = 0.12). In cycle 25 it is 0.32–0.54 for X1 flares (p = 0.035–0.11) and 0.10–0.48 for GLE 73–77 (p = 0.06–0.42). The raw spiky s² does not correlate with GLE + S before cycle 25 (p = 0.28).

### 4.6 The nine predicted periods are not special (Figure 4)
- **The naive threshold is crossed almost everywhere.** For GLE + X1old, z exceeds the naive p = 0.001 line on 19 % of the 55–700 d axis. The 27-d episode-shift null gives 34 % on average.
- **No peak is significant after the search.** The largest peak (z = 27.4 at 144 d) is far below the 95 % null maximum (z = 68).
- **Central ±2.5 % windows.** The nine periods score higher than random sets of periods: p = 0.054 (GLE + S), 0.017 (GLE + X1old) and 0.073 (GLE + X3old). Two periods drive this result: P629, and P146, which is next to the Rieger period (~154 d) that was known before. Without these two, the seven new periods give p = 0.08, 0.24 and 0.23. For GLE + X1old, P292 is at the 3.5th percentile of random periods.
- **Side-band windows.** With the side-band windows that the papers use, the predicted periods do no better than random periods (p = 0.34–0.68).

## 5. Conclusion
- **Not a clock.** The published evidence for a phase-stable 629-day "clock" in extreme solar events depends mostly on two things: treating clustered events as independent, and fixing a period that the GLE data suggested.
- **Without those two choices,** the 629-d phase concentration of GLEs is moderate (p ≈ 0.005–0.05 at a fixed period). It is not significant after a search of the 450–900 d band. X-class flares alone show only weak concentration.
- **The planetary phase agrees with the GLE phase to within a few days.** This is a real coincidence at about the 1 % level, and it is the strongest support for the claim that we found.
- **Cycle 25 does not confirm the clock.** Its X-class flares lean toward the predicted phase (mean cos about 0.35, p ≈ 0.05), but with only 6–22 independent episodes this result is not conclusive.
- **The seven new tidal periods have no support** that is better than chance.

**How to test this properly:** apply the planetary phase, fixed now, to cycle 26 (about 2030–2036), and count independent episodes, not flares.

## 6. Limitations
- The GLE and S-flare dates come from the tables of Stefani et al. 2026a. We did not check them independently against gle.oulu.fi, which is a JavaScript application, or against Tan et al. 2025.
- Episode grouping by time gap is a proxy for active-region grouping. The GOES-R flare summaries do not give region numbers. The results change with the gap (Table 4.2), and we report all values.
- The cycle-level null has only 4–7 units. The episode null ignores possible coupling between episodes (for example, non-periodic quasi-biennial surges). Thus it can still overstate significance.
- Before 1975 the X-flare data do not exist. The 1975–1976 GOES report coverage is partial. Old-scale X-flare magnitudes before 1980 have one significant digit.
- We used only the 0.7 correction for the scale change. We did not apply cross-calibration between satellites within the GOES 1–15 series.
- The planetary phase test assumes the epochs and the s² form of arXiv:2602.11227. We did not test other tidal models, other lags, or the field-dependent model of arXiv:2606.07132.
- The "~1 %" phase coincidence is a post-hoc estimate. It is not a pre-registered test.

## 7. Reproduce
```
python3.12 -m venv .venv && .venv/bin/pip install numpy pandas xarray netCDF4 matplotlib
bash files/code/00_fetch_data.sh /tmp/raw              # NOAA/NCEI files into scratch, never into the bundle
python files/code/01_build_goes_catalog.py /tmp/raw out/data    # also copy files/data/{gle_events,s_flares_stefani2026a}.csv into out/data
python files/code/02_analysis.py out/data out/results           # ~10-20 min (Monte Carlo)
python files/code/04_planetary_phase_and_placement.py out/data out/results
python files/code/03_figures.py out/data out/results out/figures
```
Versions used: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, xarray 2026.9.0, netCDF4 1.7.5.1, matplotlib 3.11.2. The Monte Carlo seeds are fixed. NCEI re-issues the GOES-R flare-summary files with new end dates; to reproduce our exact 2026 tail, compare with `input_sha256.txt`.

### Files
- `files/data/`: event tables, the merged GOES flare list, the scale check and input hashes.
- `files/results/results.json`: all numbers in Sections 4.1–4.6.
- `files/results/results_planetary_placement.json`: the planetary V-tests, the period-placement test and the prospective check.
- `files/results/per_cycle_*.csv`: per-cycle phases and timing lags.
- `files/results/*.npy`: Rayleigh spectra and the s² grid.
- `files/figures/`: Figures 1–5.
- `files/code/`: all code.
- `files/NOTICE.md`: external data sources and terms.

## References
- Stefani F., Horstmann G.M., Mamatsashvili G., Weier T. 2025, Solar Physics 300, doi:10.1007/s11207-025-02521-0 (arXiv:2503.22337).
- Stefani F. et al. 2026a, ApJ 1005, 196, doi:10.3847/1538-4357/ae75b6 (arXiv:2602.11227).
- Stefani F. et al. 2026b, arXiv:2606.07132. Stefani F. et al. 2026c, arXiv:2610.16428.
- Velasco Herrera V.M. et al. 2018, New Astronomy 60, 7, doi:10.1016/j.newast.2017.09.007.
- Tan B. et al. 2025, ApJL 979, doi:10.3847/2041-8213/ada611.
- Gurgenashvili E. et al. 2016, ApJ 826, 55 (Rieger-period dependence on cycle strength).
- Rieger E. et al. 1984, Nature 312, 623.
- NOAA/NCEI GOES XRS flare reports and GOES-R XRS L2 flare summaries.
