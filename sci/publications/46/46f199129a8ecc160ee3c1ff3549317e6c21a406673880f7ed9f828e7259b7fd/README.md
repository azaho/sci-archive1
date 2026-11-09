# Swift BAT and MAXI monitor light curves show no new X-ray period from 2.1 to 1000 days that both instruments confirm

**Job:** sci-1107-dell-astronomy-c2086b1703de · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

All-sky X-ray monitors record each bright X-ray source every day for many years. A periodic signal in such a light curve can show an orbit, a precessing accretion disk (a "superorbital" period), or a clock that nobody has found yet. A signal can also come from the instrument, from the observing pattern, or from a nearby source.

We asked this question: **Do the public daily light curves of the Swift BAT transient monitor (15-50 keV, 2005-2026) and of MAXI GSC (2-20 keV, 2009-2026) contain periodic signals from 2.1 to 1000 days that are not in the published catalogues, when we require confirmation by a second, independent data set?**

Two instruments on two different spacecraft have different orbits, pointing patterns, detectors and backgrounds. A period that both instruments see at the same frequency is very probably real and astrophysical. A period that only one instrument sees, in many unrelated sources, is very probably instrumental.

## 2. Data

| Data | Source | Span used | Count |
|---|---|---|---|
| Swift BAT transient monitor, daily light curves (`*.lc.fits`, 15-50 keV) | https://swift.gsfc.nasa.gov/results/transients/ (Krimm et al. 2013); files generated 2026-09-30 to 2026-10-21 | MJD 53415-61335 (2005-02-14 to 2026-10-23) | 1,162 files: 1,056 sources + 106 blank-sky positions (`XXX*`) |
| MAXI GSC, daily light curves (`*_g_lc_1day_all.dat`, 2-20 keV) | http://maxi.riken.jp/star_data/ (source list `top/slist.html`), processed to 2026-11-08 | MJD 55051-61353 (2009-08-15 to 2026-11-08) | 457 files |
| Known periods | Neumann et al. 2023 HMXB catalogue (J/A+A/677/A134); Avakyan et al. 2023 LMXB catalogue (J/A+A/675/A199); Fortin et al. 2023 HMXB catalogue with superorbital periods (J/A+A/671/A149); Ritter & Kolb catalogue (B/cb), from the NAOJ VizieR mirror | — | 2,665 orbital + 9 superorbital entries |
| Literature periods missing from those catalogues | `files/code/literature_periods.csv` (18 entries with references, for example Her X-1 35 d, LMC X-4 30.4 d, 4U 1820-30 171 d, SS 433 162 d, Magellanic Cloud orbits) | — | 18 |

We downloaded all files on 2026-11-09. `files/data/raw_sha256.txt` gives the SHA-256 of every raw file that we used (1,627 files). We did not put the raw light curves (450 MB) in this bundle. Section 9 gives the retrieval recipe. The shared campaign dataset store had no X-ray monitor data, so this bundle does not use a shared dataset.

After quality cuts (BAT `DATA_FLAG = 0`; errors below 5 times the median error; at least 300 days), we analysed 1,161 BAT light curves (1,055 sources, 106 blank-sky positions) and 452 MAXI light curves. A position match within 0.3 deg gives 360 sources with both BAT and MAXI data.

## 3. Method

1. **Periodogram.** For each light curve we computed a floating-mean Lomb-Scargle periodogram with "semi-weighting" (Corbet et al.): each error is increased by the excess variance of the source. The frequency grid is 0.001-0.476 cycles/day (1000-2.1 d), with five-fold oversampling of a 22-year span.
2. **Red-noise normalisation.** Many X-ray sources have strong red noise and outbursts. We divided the power by its running median in +-0.1 dex windows of log frequency (divided by ln 2). For white noise this ratio R follows Exp(1). We use the significance S1 = R / ln 10 (that is, -log10 p for one frequency). To find non-sinusoidal signals, such as eclipses and periastron outbursts, we also use S4: the -log10 p of the sum of R over harmonics 1-4 (Gamma(n,1) null). An S4 detection also needs S1 >= 2 at the fundamental. Without this rule, S4 gives false peaks at rational multiples (p/q) of a strong line. For example, the S4 statistic of 4U 1538-52 had a false 4.31-d peak at half of the daily alias of the second orbital harmonic.
3. **Null calibration.**
   * BAT blank-sky positions: the maximum S over 2.1-1000 d is 3.9 (median), 5.0 (95th percentile) and 6.6 (largest of 106). No blank field has S > 7.
   * Common lines: we counted how many unrelated sources have a peak (S > 4) in each frequency cell of width 1/6300 c/d (`instrumental_cells.csv`).
4. **Discovery routes.**
   * **Route A: BAT x MAXI.** A peak with S > 7 in one instrument must have S > 3 within +-1.5/6300 c/d in the other instrument. For a null, we paired each BAT source with an unrelated MAXI source (20 shuffles).
   * **Route B: BAT split-half.** A full-span BAT peak with S > 7 must have S > 3 in both 2005-2015 and 2016-2026.
   * **Route C: BAT out-of-sample.** Discovery in one decade (S1 > 5). Prediction for the other decade: the same frequency with S1 > 3 and, when the extrapolated phase error is below 0.15 cycle, the same phase within +-0.15 cycle. For a null, the second decade came from a random other source (10 shuffles).
   * **Route D: MAXI split-half.** This is the same as route B but for MAXI (2009-2018 and 2018-2026). We use it only to catalogue artifacts, because the shared instrumental comb makes it unreliable (see the results).
5. **Reduction and identification.** We grouped the peaks of each source into independent fundamentals. A peak is "derived" if it is a rational multiple (p/q, q <= 4) of a stronger fundamental, a daily alias |1 - (p/q) f0|, a yearly window side peak f0 +- k/365.25, or a beat of two fundamentals. We then compared each fundamental with catalogued periods of the same object within 0.25 deg. We used harmonics up to 20 for orbital periods and up to 4 for other periods, daily aliases, and orbit-superorbit beats. Because catalogue values are rounded, we allowed a 1 per cent tolerance at the fundamental. A second stage tested these explanations:
   * a catalogued period of a neighbour within 3 deg;
   * for MAXI only, an ISS precession comb line or a sideband f_k +- f_node or f_k +- f_beta;
   * a calendar period k/365.25 d.

   `manual_notes.csv` records our reasoning for each fundamental that the automatic rules did not label.
6. **Sensitivity.** We injected sinusoids into the real BAT and MAXI light curves of 360 matched sources: 4 random periods per source, log-uniform from 2.2 to 900 d, with semi-amplitudes of 0.5-16 mCrab and the same Crab fraction in both bands. Then we applied the route A rule (1,440 injections x 6 amplitudes). The Crab rates are the medians of the monitor light curves: BAT 0.2163 ct/cm2/s and MAXI 3.493 ph/cm2/s.
7. **Census.** For the 110 BAT sources with a catalogued orbital or superorbital period from 2.1 to 1000 d, we recorded whether each route recovers the period (n = 1-4 harmonics).

## 4. Results

### 4.1 No new period passes the independent tests

| Route | Peaks above the primary threshold | Confirmed | Expected false (null) | Independent fundamentals | Catalogued / known | Not catalogued |
|---|---|---|---|---|---|---|
| A: BAT x MAXI (S > 7, confirm S > 3) | 1,982 | 368 | 22 (1.1 per cent, shuffled pairs) | 34 in 28 sources | 34 after manual notes | 0 |
| A, low threshold (S > 5.5, confirm S > 2.5) | 2,743 | 462 | 69 (2.5 per cent) | 41 | 40 | 1 weak (RX J1718.4-4029, 45.4 d) |
| B: BAT split-half (S > 7, halves S > 3) | 326 | 260 | 0 of 3,000+ shuffled peaks | 51 | 50 + 1 calendar (182.6 d) | 0 |
| C: BAT out-of-sample (S1 > 5, predict S1 > 3 + phase) | 431 | 170 | 2.2 (0.52 per cent of 4,249 shuffled) | 48 in 38 sources | 48 after manual notes | 0 |

All periods that we confirm with an independent data set (route A, B or C) are catalogued orbital or superorbital periods, their harmonics, aliases, window side peaks, or orbit-superorbit sidebands. There are 28 sources in route A. They include Vela X-1, 4U 1538-52, XTE J1855-026, OAO 1657-415, GX 301-2, 4U 1907+09, IGR J18483-0311, IGR J17252-3616, IGR J00370+6122, 2S 0114+650, 4U 0728-25, 4U 1909+07 (orbit 4.4 d and superorbital 15.2 d), EXO 2030+375, GX 304-1, IGR J19294+1816, GRO J1008-57 (249.5-d orbit, seen only through its harmonics), 2S 1845-024, SS 433, Cir X-1, Cyg X-1, Her X-1, LMC X-4, SMC X-1 and 4U 1820-30 (171-d superorbital cycle). `files/results/final_fundamentals_7_3.csv` gives the full list.

The items that needed manual identification (`files/code/manual_notes.csv`) are these:
- Her X-1 17.2 d: the second harmonic of the quasi-periodic 35-d cycle.
- SMC X-1 2.13, 3.61-3.64 and 4.18-4.26 d: aliases and sidebands of the 3.892-d orbit with the time-variable 40-65 d superorbital cycle.
- LMC X-4 29.6 d and GX 301-2 40.9 d: side peaks of a time-variable or very strong period.
- IGR J18410-0535 6.35 d: a yearly window side peak of its 6.453-d orbit.
- PSR J1809-2332 182.6 d: exactly half a year, so probably a pointing pattern.

**MAXI J0903-531.** The only recurrence period without a catalogue match is that of the Be/X-ray pulsar MAXI J0903-531. BAT data from 2021-2026 give a period of 59.62 +- 0.17 d (sinusoid, residual bootstrap) or 59.82 d (4 harmonics) (`j0903_period.json`). This value is far from the catalogued 57.0-d orbit (ATel 14730). A ~59-d recurrence in BAT and Fermi GBM was already reported in a HEAD 2023 abstract, so this is **not a new discovery**. Our data extend the record to October 2026 and show that the recurrence stays near 59.6-59.8 d. The MAXI support (S = 3.2) is weak and lies near the 60.3-d ISS beta-angle cycle, so we do not count MAXI as an independent confirmation for this source.

**Weak, unconfirmed list.** At a lower threshold (BAT full S > 5.5, both halves S > 2.5), 15 more BAT fundamentals have no catalogue match and no other identification (`final_splithalf_bat_5.5_2.5.csv`). Examples are IGR J17200-3116 12.57 d (an HMXB with a 328-s pulsar and no published orbit), Fermi J1057-6027 14.0 d and 4U 1901+03 13.8 d. **None of them passes route C or route A.** IGR J17200-3116 has S1 = 4.7 and 2.5 in the two decades, and its neighbour XTE J1720-318 (0.47 deg away) shows a different period (12.46 d). We report this list only as targets for other data. It is not evidence of new periods.

### 4.2 Sensitivity of the null result

Route A recovery of injected sinusoids (per cent; `injection_summary.csv`, Figure 4):

| Period | BAT rms/error | 1 mCrab | 2 mCrab | 4 mCrab | 8 mCrab | 16 mCrab |
|---|---|---|---|---|---|---|
| 2.2-10 d | < 1.2 (262 sources) | 81 | 91 | 98 | 99 | 100 |
| 2.2-10 d | > 2 (41 sources) | 7 | 33 | 61 | 76 | 91 |
| 10-100 d | < 1.2 | 61 | 86 | 91 | 98 | 99 |
| 10-100 d | > 2 | 2 | 9 | 23 | 53 | 72 |
| 100-900 d | < 1.2 | 17 | 52 | 70 | 81 | 89 |
| 100-900 d | > 2 | 0 | 2 | 4 | 11 | 30 |

Thus, for the about 260 quiet matched sources, a coherent sinusoidal modulation with a semi-amplitude of 2 mCrab or more at 2.2-100 d would be found in at least 86 per cent of cases. Long periods and strongly variable sources are much less constrained. Over all injections the recovery is 2, 39, 63, 75, 85 and 90 per cent at 0.5, 1, 2, 4, 8 and 16 mCrab.

### 4.3 Census of catalogued periods

BAT alone (S > 7) recovers 39 per cent of the catalogued orbital periods and 71 per cent of the superorbital periods of the 110 sources (Figure 3, `census.csv`). For the matched sources, route A recovers 34 per cent of orbits (29 of 85) and 80 per cent of superorbital periods (8 of 10). Recovery increases with flux: route A recovers 6 per cent below 1 mCrab, 12 per cent at 1-3 mCrab, 41 per cent at 3-10 mCrab and 55 per cent at 10-30 mCrab (only 4 sources are brighter). Some bright systems do not show their orbit, for example GRS 1915+105 (33.5 d), Cyg X-1 in BAT (5.6 d; MAXI detects it, S = 11, because the absorption dips are soft), GX 13+1, Cyg X-2, X Per and gamma Cas. In these systems the orbit does not modulate the hard X-ray flux strongly, or red noise hides it.

### 4.4 Instrumental and confusion signals

* **The MAXI ISS comb.** At 36.2 d, 46 per cent of all MAXI sources have S1 > 3, and at 72.3 d, 45 per cent do. The largest fraction in BAT sources at any period is 1.1 per cent (Figure 1). The comb has a fundamental of 72.3 d (fit to harmonics 1-10 of the stack; single harmonics give 72.2-72.5 d) and statistically significant harmonics down to the 21st (3.46 d), plus lines near 2, 3 and 4 times 72.3 d. This is the nodal precession period of the ISS orbit. In this cycle the MAXI scan direction and the camera that sees a source change. The MAXI team and earlier papers (for example the gamma Cas study, arXiv:1504.01105; ATel 16787) report the ~70-d and ~35-d lines. Our stack shows that the comb is present in about half of all catalogue sources and extends to at least the 21st harmonic, so it affects MAXI period searches from 3.4 to 300 d.
* **ISS sidebands of real periods.** MAXI also shows real periods shifted by the precession frequency. Vela X-1 has a 7.98-d line (1/8.964 + 1/72.3), and Cen X-3 has a 2.161-d line (f_orb - f_beta, with f_beta = 1/72.3 + 1/365.25, a 60.3-d beta-angle cycle). Figure 2 shows examples. BAT has no such lines.
* **Source confusion.** In MAXI the 3.412-d orbit of 4U 1700-37 appears in GX 349+2 (1.5 deg away) and SAX J1712.6-3739 (1.7 deg). The 10.45-d orbit of OAO 1657-415 appears in XTE J1701-407 (0.8 deg). The 8.37-d orbit of 4U 1907+09 appears in XTE J1908+094 (0.5 deg). The 18.55-d orbit of IGR J18483-0311 appears in EXO 1846-031 (0.3 deg).
* Because of the comb, the MAXI split-half route has a 21 per cent false-persistence rate in shuffled pairs. Thus, a MAXI-only period needs independent confirmation.

## 5. Interpretation

Within the tested range (2.1-1000 d, daily sampling) and within the sensitivity shown in section 4.2, the two all-sky monitors do not contain an unknown coherent X-ray period that both instruments confirm. The known periodic X-ray sky at these time scales is already almost fully catalogued for sources above a few mCrab. Most remaining "new" periods in single-instrument searches are aliases, sidebands, window side peaks, MAXI precession lines or light from a neighbour. A useful practical rule follows: before a MAXI period is accepted, compare it with 72.3/k d, k x 72.3 d, f_k +- 1/72.3 and f_k +- 1/60.3 c/d for known periods f_k of the source, and with the periods of bright sources within about 2 deg.

## 6. Limitations

- Periods below 2.1 d were not searched (daily bins). This excludes most LMXB and CV orbits. The 92-96 min orbit light curves would be needed for them.
- The red-noise normalisation is a running median. It is not a full red-noise model. For strongly variable sources the nominal p values are approximate. Thus we calibrated with blank fields, shuffled sources and injections, but not with source-specific red-noise simulations.
- A quasi-periodic signal (for example a superorbital cycle whose period drifts) loses significance in a full-span periodogram. Our search is therefore most sensitive to coherent clocks.
- The catalogue comparison depends on the catalogues and on a small hand-made literature list. Some "known" labels can be chance matches at high harmonic numbers. We listed every match in `final_*.csv` so that a reader can check each one.
- Route A covers only the 360 sources in both monitor lists. The MAXI list has 457 sources, and on-demand MAXI light curves for other positions were not used.
- BAT light curves of neighbouring sources are fitted together by the BAT pipeline, but leakage between close sources (for example IGR J17200-3116 and XTE J1720-318, 0.47 deg) can still occur.
- The injection test uses sinusoids. Narrow outbursts or eclipses with the same rms are easier to find with S4, so the table is conservative for them.

## 7. Figures

- `files/figures/fig1_common_periods.png`: fraction of sources with S1 > 3 at each period, for MAXI, BAT and BAT blank fields.
- `files/figures/fig2_examples.png`: BAT (up) and MAXI (down) periodograms for Vela X-1 (ISS sideband), GX 349+2 (confusion with 4U 1700-37) and MAXI J0903-531.
- `files/figures/fig3_census.png`: recovery of catalogued periods against BAT flux.
- `files/figures/fig4_injection.png`: injection-recovery curves.

## 8. Files

- `files/code/`: all analysis code (Python 3.12, numpy, scipy, pandas, astropy, matplotlib) and `run_all.sh`.
- `files/results/`: results tables. `meta_*.csv` gives per-light-curve statistics. `coincidences_*`, `classified_*` and `final_fundamentals_*` are for route A, `final_splithalf_*` for routes B and D, and `oos_*` for route C. The other files are `census.csv`, `injection_11.csv`, `injection_summary.csv`, `instrumental_cells.csv`, `calib_summary.json`, `known_periods.csv` and the stacked fractions `stack_frac_*.npy`.
- `files/data/raw_sha256.txt`: hashes of all raw inputs. `files/data/maxi_sources.csv` gives the MAXI source list with coordinates.

## 9. How to reproduce

1. Download the inputs into `raw/` next to `code/`:
   * BAT: parse `https://swift.gsfc.nasa.gov/results/transients/index.html` and `BAT_blank.html` for source paths. Download `https://swift.gsfc.nasa.gov/results/transients/<path>.lc.fits` into `raw/bat_daily/` (about 55 kB/s per connection, so use 24 in parallel).
   * MAXI: parse `http://maxi.riken.jp/top/slist.html` into `raw/maxi_sources.csv` (columns `maxi_id,name,ra,dec`). Download `http://maxi.riken.jp/star_data/<id>/<id>_g_lc_1day_all.dat` into `raw/maxi_daily/`.
   * Catalogues: `http://vizier.nao.ac.jp/viz-bin/asu-tsv?-source=<cat>&-out.all&-out.max=unlimited` for J/A+A/677/A134, J/A+A/675/A199, J/A+A/671/A149 and B/cb. Save them in `raw/catalogs/` with `/` replaced by `_`.
   * The archives are live. Light curves downloaded later contain more days. Thus, compare with `raw_sha256.txt` to see whether the files are identical.
2. Run `bash code/run_all.sh`. On 12 cores at a host load of about 150, the full chain took about 2 hours. The injection test and the shuffles take most of the time.
3. Apply `code/manual_notes.csv` for the fundamentals that the automatic rules did not label.

## 10. References

Krimm et al. 2013, ApJS 209, 14 (BAT transient monitor); Matsuoka et al. 2009, PASJ 61, 999 (MAXI); Neumann et al. 2023, A&A 677, A134; Avakyan et al. 2023, A&A 675, A199; Fortin et al. 2023, A&A 671, A149; Ritter & Kolb 2003, A&A 404, 301; Corbet & Krimm 2013, ApJ 778, 45; Corbet et al. 2021, ATel 14730 (MAXI J0903-531); the HEAD 2023 abstract on MAXI J0903-531 (BAAS 55, 2023n4i116p14); the MAXI precession artifact in arXiv:1504.01105 and arXiv:2206.01505; the literature periods in `literature_periods.csv`.
