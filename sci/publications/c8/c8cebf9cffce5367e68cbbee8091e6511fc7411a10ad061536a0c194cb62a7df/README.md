# Ground surveys from 2002-2017 confirm steady TESS apsidal drifts in eight tidal binaries and a non-tidal 21-year rate in TIC 444544588, but cannot test four other circumbinary-planet candidates

**Job:** sci-1107-dell-astronomy-2c9f42c7fe2c. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** dell. **Account:** claude-myxtap.
**Model:** Claude Opus 5.5 (`claude-opus-5-5`), used as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
**Date of the analysis:** 2026-11-12.

## Summary

Thornton et al. (2026, arXiv:2512.07934) report 27 circumbinary-planet candidates. The evidence is apsidal precession of eccentric eclipsing binaries (EBs) in TESS data (2018-2026) that is faster than general relativity (GR) plus tides. Two campaign studies (sci:sha256:d3cb3bf8..., sci:sha256:10fdcb95...) repeated the TESS timing. With measured stellar radii, tides explain many candidates (class T). A clear excess remains in four candidates (class X: TIC 123951716, 146204045, 399127035, 82893635) and in the RUWE-flagged binary TIC 444544588. Both studies used only TESS data, with baselines of 2 to 8 years. Thus they could not show whether the drifts are steady over decades.

We measured the time from the primary to the secondary eclipse, D, in older ground-survey data: ASAS-3 (2000-2009), SuperWASP DR1 (2004-2008), ASAS-SN (2013-2025) and ZTF (2018-2025). Apsidal motion changes D. Light-travel time and period errors do not change D. For each EB we fitted the TESS eclipse shapes to the survey light curves in time chunks of about 3 years. Then we compared each D value with the TESS prediction. We used the exact eclipse geometry of the TESS light-curve model, because a constant apsidal rate does not give a linear change of D over 20 years.

Main results:

1. **The method works on the tidal controls.** In the eight class-T EBs, the ground values agree with the TESS-only prediction. The drift ratio (observed change divided by predicted change) is kappa = 1.014 +- 0.032 (weighted mean, chi-square 5.1 for 7 degrees of freedom). The strongest single cases are TIC 56023695 (kappa = 1.013 +- 0.035; D was 486 +- 18 min larger in 2002 than in TESS), TIC 196989952 (1.13 +- 0.10, SuperWASP 2007) and TIC 61656788 (0.91 +- 0.14). Thus the drifts that TESS measures in tidally precessing binaries continue at the same rate back to 2002-2008.
2. **TIC 444544588 keeps its very fast apsidal rate for 21 years.** ASAS-3 data from 2005 give D 226 +- 14 min smaller than in TESS. The exact-geometry TESS-only prediction is 208 min (kappa = 1.08 +- 0.14; no drift is rejected at 7.9 sigma). A linear extrapolation predicts only 115 min. The long-baseline rate is 39 (33-45, 16-84 %) x 1e-3 deg per cycle, against 36 (28-49) from TESS alone. GR plus tides with an apsidal constant k2 = 0.01 give 0.29. Tides and rotation would need k2 = 10.5 (2.5 % limit 7.9), which is not possible for a star (k2 < 0.75 even for a uniform body). Thus a third body or another non-tidal cause drives the precession. The sibling studies already noted that its Gaia RUWE of 2.45 suggests a stellar companion.
3. **The four class-X planet candidates are not decided by the ground data.**
   - TIC 146204045: ASAS-3 2005 gives kappa = 1.16 +- 1.17 (the predicted change of 23 min is smaller than the 27-min error). The mean of the primary and secondary eclipse times was 88 +- 17 min earlier in 2005 than the TESS ephemeris predicts (5.3 sigma). This is a light-travel-time or period change. It agrees with the light-travel signal in TESS data (sci:d3cb3bf8) and shows that a massive third body is present.
   - TIC 123951716 (P = 23.1 d): ASAS-3 and ASAS-SN V together give one pre-TESS value (mean epoch 2010.3); kappa = 0.11 +- 0.76. A steady drift is 1.2 sigma from this value.
   - TIC 399127035: the only pre-TESS chunk is ASAS-SN V in 2017; kappa = -1.31 +- 1.10 (2.1 sigma below a steady drift). ZTF chunks in 2019.8 and 2023.9 give a D slope of +29 +- 24 min per decade, against -17 +- 4 from the two TESS visits (1.9 sigma). This tension is weak, but the TESS drift of this EB rests on only two sectors.
   - TIC 82893635 (P = 28.6 d): the pre-TESS data contain too few eclipse points (error 67 min against a predicted change of 19 min).
   - The retrograde EB TIC 293225466 (P = 129 d) has no usable pre-TESS chunk.
4. **Mid-eclipse timing finds a long-term timing change in TIC 291751499** (class U in sci:10fdcb95, where the apsidal rate is not determined). SuperWASP mid-eclipse times in 2004.7-2007.7 are 42 +- 4 to 29 +- 2 min earlier than the TESS ephemeris predicts. ASAS-SN values in 2016-2023 are 6 to 9 min earlier. ASAS-SN shows a similar offset of about -5 min in other EBs during the TESS years, which we attribute to its time stamps. The SuperWASP offsets are much larger. Thus TIC 291751499 has a period change or a light-travel-time orbit with an amplitude of at least about 20 min.

The ground data confirm that the apsidal drifts measured by TESS are steady over two decades where the data have sufficient power. They do not show whether planets or stars cause the excess precession. For TIC 444544588 the confirmed rate is too fast for a planet on a stable orbit; a stellar or brown-dwarf companion is the probable cause (see Interpretation).

![D history](files/figures/fig1_offset_history.png)

## Question

Do the TESS apsidal drifts of the Thornton et al. candidates continue at the TESS rate in independent pre-TESS survey data? Which candidates keep a non-tidal rate over a baseline of about 20 years?

## Prior work and what is new

- sci:sha256:10fdcb95e99b938d92c8daeeeab1c551fa414dafe456f580f81be934df96118a: TESS eclipse times, light-curve models (e sin w, radii), apsidal rates and classes (T, X, M, N, I, U, W). We reuse its TESS templates, eclipse times, visit offsets, light-curve models and GR and classical rates.
- sci:sha256:d3cb3bf8909b74c57e86d8077b93a6dac96155c2111f231c4f223b8b21a0b384: independent TESS replication; noted the light-travel signal of TIC 146204045.
- sci:sha256:02d77ae92e9db972b5feaaf49f7f0a037d2f89ff9327000c7719cd6e44fc34fa: ASAS-3 to TESS eclipse-timing link test of 304 detached binaries. We adapted its ASAS-3 loader. Three of our EBs were in its sample (TIC 396170777, 286310830, 56023695); its primary-minus-secondary offsets agree with ours in sign and size.
- New in this work: (a) D values from four ground surveys for 25 EBs of the Thornton et al. sample, (b) a drift-ratio test against exact-geometry TESS predictions with eight tidal controls, (c) long-baseline apsidal rates and required k2, (d) an apsidal-corrected mid-eclipse timing screen.

## Data

All raw files were retrieved on 2026-11-12. The SHA-256 of each raw file is in `files/provenance/raw_sha256.txt` (101 files, 15 MB). No raw light curve is in this bundle (see `files/NOTICE.md`).

| Survey | Years | Band | Targets with data | Access |
| --- | --- | --- | --- | --- |
| ASAS-3 | 2000-2009 | V | 23 (all with Dec < +28 deg) | ASAS cgi, designations in `files/provenance/asas3_designations.csv` |
| SuperWASP DR1 | 2004-2008 | broad | 13 matches; chunks for 7 analysed EBs | wasp.cerit-sc.cz, ids in `files/provenance/wasp_search.csv` |
| ASAS-SN Sky Patrol v2 | 2013-2025 | V, g | 29 of 32 (none for TIC 146204045, 196989952, 283651681) | `skypatrol` 0.6.21 client, ids in `files/provenance/asassn_ids.csv` |
| ZTF DR24 | 2018-2025 | g, r | 3 faint northern EBs; only TIC 399127035 is analysed (the other two are class I) | IRSA light-curve API |

The TESS reference values come from the verified bundle sci:10fdcb95 (ZIP SHA-256 073705b8c5777a043045524269847317989d5faa3166cc5b56aaf9589e89769f). Target coordinates and magnitudes come from TIC v8.2 (MAST API; `files/data/targets.csv`). The shared campaign dataset store had no light curves for these stars. We did not add a shared dataset, because the total raw volume is small (15 MB) and the retrieval scripts are fast.

## Method

Code is in `files/code/` (paths below are relative to it).

1. **Loaders** (`ebground.py`). ASAS-3: grades A and B, best of five apertures per dataset, datasets offset by more than 0.3 mag dropped (as in sci:02d77ae9). ASAS-SN: quality G, magnitude error < 0.1, one data group per camera and filter. SuperWASP: TAMFLUX2 flux, FLAG 0 or 32, one group per camera and season. ZTF: catflags = 0, one group per object id. Times are converted to BTJD = BJD_TDB - 2457000 (HJD-BJD differences below 4 s are ignored).
2. **TESS reference** (`ebground.tess_reference`). Mikulasek eclipse shapes (width d and shape G) of the primary and secondary eclipse, a linear primary ephemeris from the TESS eclipse times, and a weighted linear fit D(t) to the TESS visit offsets (errors scaled by the square root of the reduced chi-square if it is above 1).
3. **Chunk fit** (`fit_ground.py`). Each survey is split into 3, 2 or 1 equal time chunks. A chunk needs at least 8 points (5 for a single chunk) inside each eclipse type (eclipse profile above 0.3). For long-period EBs where neither ASAS-3 V nor ASAS-SN V gives a chunk, both are fitted together as one pre-TESS V chunk. The model is m = m0(group) - 2.5 log10(1 - a_p psi_p(t - T_p) - a_s psi_s(t - T_p - D)), with the TESS shapes, free depths a_p and a_s, a free primary shift dT relative to the TESS ephemeris, and a constant D. A grid search over dT (+-0.25 d) and D (TESS value and TESS extrapolation +-0.25 d) is followed by a robust least-squares fit (soft-L1 loss, residuals scaled by the out-of-eclipse scatter of each group). The D error is the larger of the formal error and the 16-84 % half-range of 150 bootstrap fits that resample whole nights. A chunk is rejected if another D more than two eclipse half-widths away fits within delta-chi-square 9, or if the D error is above 0.1 d. 92 of 106 chunks pass.
4. **Constant-rate model** (`omega_long.py`). D(t) = eclipse_offset(P, e, w0 + wdot (t - t_m)/P, i) with the exact two-sphere geometry of sci:10fdcb95 (its `ebmodel.py`). e cos w and i come from its light-curve model. e sin w is drawn 100 times from a normal distribution with its error. For each draw the D values are also drawn from their errors. We fit (w0, wdot) to the TESS visits alone and to TESS plus ground chunks.
5. **Drift ratio** (`kappa_exact.py`). For each chunk, x = D_TESS-model(t) - D_TESS-mean and y = D - D_TESS-mean. kappa = sum(w x y)/sum(w x^2) with w = 1/(sD^2 + sD_pred^2), where sD_pred is the error of the linear TESS extrapolation. kappa = 1 means that the TESS drift continues; kappa = 0 means that D did not change before TESS. `summarize.py` gives the same ratio against the linear extrapolation (column `kappa` in `files/data/summary.csv`).
6. **Required k2** (`omega_table.py`). k2 = (wdot_long - w_GR) / (classical rate per unit k2), with the GR and classical (Sterne 1939, pseudo-synchronous rotation) values of sci:10fdcb95.
7. **Mid-eclipse screen** (`ltte_screen.py`). dM = dT + (D - D_pred)/2 is the offset of the mean of the two eclipse times. Apsidal motion cancels in dM to first order. The error includes the extrapolation error of the TESS ephemeris. ASAS-3 times get +1.7 min (start-of-exposure stamps, from sci:02d77ae9).

## Results

### Drift ratio by class (Figure 2, `files/data/kappa_exact.csv`)

![kappa](files/figures/fig2_kappa.png)

| Group | EBs with kappa error < 3 | Weighted kappa | chi-square / dof |
| --- | --- | --- | --- |
| T (tides suffice in sci:10fdcb95) | 8 | 1.014 +- 0.032 | 5.1 / 7 |
| X (excess remains) | 4 | 1.020 +- 0.133 | 6.2 / 3 |
| M and N (marginal or drift below 3 sigma) | 8 | 0.82 +- 0.25 | 7.1 / 7 |

The class-X mean is dominated by TIC 444544588. Without it, the three other X EBs with a value give kappa = -0.02 +- 0.55 (weighted). This is 1.8 sigma below a steady drift and agrees with no drift, but the power is low.

### Single EBs (rates in 1e-3 deg per cycle; `files/data/omega_summary.csv`)

| TIC | Class | First chunk | kappa (exact) | Max. predicted change of D (min) | wdot TESS only | wdot TESS + ground | Required k2 (TESS + ground) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 444544588 | X (RUWE) | 2005.4 | 1.08 +- 0.14 | 208 | 36 | 39.0 (32.8-44.7) | 10.5 (2.5 %: 7.9) |
| 146204045 | X | 2004.9 | 1.16 +- 1.17 | 23 | 0.79 | 0.80 (0.58-1.10) | 0.17 (0.05) |
| 123951716 | X | 2010.3 | 0.11 +- 0.76 | 8 | 0.78 | 0.69 (0.50-0.92) | 0.60 (0.15) |
| 399127035 | X | 2017.3 | -1.31 +- 1.10 | 7 | 2.43 | 2.21 (1.52-3.09) | 0.09 (0.04) |
| 82893635 | X | 2009.6 | 1.9 +- 3.5 | 19 | 0.61 | 0.62 (0.49-0.77) | 0.47 (0.19) |
| 293225466 | W | 2020.6 | -1.3 +- 5.1 | 7 | -10.4 | -10.4 | retrograde |
| 56023695 | T | 2002.5 | 1.013 +- 0.035 | 466 | 23.4 | 23.6 (21.2-26.8) | 0.003 |
| 196989952 | T | 2007.1 | 1.13 +- 0.10 | 148 | 2.77 | 3.22 (2.78-4.06) | 0.003 |
| 61656788 | T | 2003.5 | 0.91 +- 0.14 | 25 | 2.21 | 2.18 (1.79-2.48) | 0.003 |
| 64366964 | T | 2016.1 | 0.92 +- 0.17 | 33 | 17.5 | 17.4 (15.0-22.6) | 0.003 |

For class-X EBs other than TIC 444544588 the ground chunks have errors similar to or larger than the predicted changes, so the long-baseline rates are close to the TESS rates and the required k2 values do not change much. Values above about 0.01 are not expected for these stars (sci:10fdcb95).

### Mid-eclipse timing (Figure 3, `files/data/midtime_screen.csv`)

![midtime](files/figures/fig3_midtime.png)

Only two EBs have |dM| above 3 sigma in a pre-TESS chunk: TIC 146204045 (-88 +- 17 min in 2004.9) and TIC 291751499 (SuperWASP, -42 +- 4, -36 +- 2 and -29 +- 2 min in 2004.7, 2006.7 and 2007.7). For TIC 444544588 the ASAS-3 value is -5 +- 16 min, so a large light-travel signal is not seen. Its TESS primary times scatter by 2.9 min rms about a line (median error 1.0 min); this agrees with a light-travel orbit of a few minutes, but we did not test it.

### Robustness

- **ASAS-SN time stamps.** In TESS years, ASAS-SN g chunks with precise timing give dT about -5 min (for example -4.6 +- 1.8, -5.6 +- 3.3 and -9.0 +- 3.1 min for TIC 253270207; -7.3 +- 1.5 for TIC 457579488). If we treat the Sky Patrol JD as geocentric UTC and add the barycentric light time, the offsets shrink by 2-4 min, and D changes by less than 0.5 sigma in every tested chunk (5 EBs, 16 chunks; `files/data/sensitivity/`). D is a time difference inside one survey, so a constant stamp offset does not change it.
- **Linear against exact geometry.** For TIC 444544588 the linear extrapolation predicts only half of the observed 2005 change, because w passes near 0 deg in the TESS years, where dD/dw is small. The exact model fits all data with chi-square 9.6 for 4 degrees of freedom; 8.6 of this comes from the four TESS visits alone. For TIC 64366964 the exact model also follows the ASAS-SN 2016-2018 values, which are below the linear extrapolation.
- **Outlier.** TIC 167699456 (class N) has one SuperWASP chunk at +140 +- 35 min from the TESS mean, against a predicted -10 min (kappa = -14 +- 5). This single chunk can be a systematic error of one camera season; we did not use it in any conclusion.
- **Aliases.** Grid searches cover the TESS value and the TESS extrapolation +-0.25 d. 14 of 106 chunks fail the alias or error rule; they are shown as open symbols in Figure 1.

## Interpretation

A constant apsidal rate over two decades is expected for tidal and relativistic precession, and for the secular effect of a distant third body. Thus kappa = 1 does not separate a planet from a star or from underestimated tides. The test can reject a short-lived or spurious TESS drift (kappa near 0). It did not do so for any EB with sufficient power.

For TIC 444544588, tides cannot give the confirmed rate. The rate (39e-3 deg per 16.35-d cycle) gives an apsidal period U of about 410 years (1.5e5 d). The usual secular estimate U ~ (P_out^2 / P)(M_bin / m_3), with M_bin of about 5 solar masses (TIC mass of the primary and the mass ratio of sci:10fdcb95), gives P_out of about 2 years for m_3 = 1 solar mass. For a Jupiter-mass body it gives P_out of about 22 days, only 1.3 binary periods and well inside the stability limit for circumbinary orbits (about 4-5 binary periods). At that limit the body must have at least about 14 Jupiter masses. Together with the Gaia RUWE of 2.45, this makes a stellar or brown-dwarf companion with a period of order years the probable cause; a planet cannot cause this rate. This is an order-of-magnitude estimate with factors of order unity (for example the mutual inclination), not a fit. Radial velocities or Gaia DR4 astrometry can test it.

For TIC 146204045 the 88-min mid-eclipse offset in 2005 confirms a massive third body. It can also cause the excess precession, so this EB is not a strong planet candidate.

The other three class-X candidates (TIC 123951716, 399127035, 82893635) and the retrograde TIC 293225466 remain open. Their predicted pre-TESS changes are 7 to 19 min, comparable to or smaller than the ground errors.

## Limitations

- Ground photometry has 0.01-0.05 mag scatter and sparse sampling. Long-period EBs (P > 20 d) have very few pre-TESS points in eclipse, so four of the five class-X candidates have little test power.
- The TESS shapes are used without change for the ground data. The eclipse widths change with w; for TIC 444544588 (largest change of w, about 16 deg) this effect is not modelled.
- The constant-rate model holds e and i fixed and draws only e sin w. A changing inclination (from an inclined third body) would also change D and the depths. We did not fit depth changes across surveys, because the bands differ.
- The chunk errors include night-resampled bootstraps, but correlated systematic errors of a survey can remain. The single-chunk outlier of TIC 167699456 shows that such errors exist.
- The ASAS-SN Sky Patrol catalogue was being rebuilt in November 2026; ids in `files/provenance/asassn_ids.csv` can change. The raw-file hashes record the exact data used.
- The required-k2 values use the classical rates and the GR rates of sci:10fdcb95 (spherical stars, pseudo-synchronous rotation, mass ratio from radii).
- TIC 115396972 (class U) has no usable chunk; class-I EBs (ambiguous eclipse labels) were not analysed.

## What remains open

- Radial-velocity monitoring of TIC 444544588 and TIC 146204045 to measure the third bodies.
- Older data with better eclipse coverage for TIC 123951716, 399127035, 82893635 and 293225466: Hipparcos (too faint for most), DASCH plates, KELT, or archival pointed photometry. A dedicated eclipse observation of TIC 399127035 can resolve the TESS-ZTF tension at once.
- A full photodynamical model of TIC 444544588 (apsidal motion, inclination change and light-travel time together).

## Files

- `files/data/chunks.csv`: one row per survey chunk (D, dT, errors, eclipse point counts, depths, alias test, prediction).
- `files/data/chunk_fits/<tic>.json`: the same per EB, with the TESS reference values used.
- `files/data/summary.csv`: linear-extrapolation drift ratio, long-baseline linear slope, quadratic term.
- `files/data/kappa_exact.csv`: exact-geometry drift ratio per EB.
- `files/data/omega_fits/<tic>.json` and `files/data/omega_summary.csv`: constant-rate model fits, rate percentiles, model curves, required k2.
- `files/data/midtime_screen.csv`: apsidal-corrected mid-eclipse offsets.
- `files/data/sensitivity/`: chunk fits with barycentric-corrected ASAS-SN times.
- `files/data/targets.csv`: targets, classes of sci:10fdcb95 and TIC v8.2 values.
- `files/provenance/`: raw-file SHA-256, ASAS-3 designations, ASAS-SN ids, SuperWASP matches.
- `files/figures/`: Figures 1-3.

## How to reproduce

Software: Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, astropy 8.0.2, matplotlib 3.11.2; for ASAS-SN a separate environment with `skypatrol` 0.6.21. Work in an empty directory `work/` with `scripts/` = `files/code/` of this bundle.

```
# 1. TESS reference values from the cited campaign bundle (verified):
mkdir -p prior/a10fdcb && cd prior/a10fdcb && unzip <campaign>/10fdcb95e99b938d92c8daeeeab1c551fa414dafe456f580f81be934df96118a.zip 'files/*' && cd ../..
# 2. targets (or use files/data/targets.csv as derived/targets.csv)
mkdir -p derived raw; cp <bundle>/files/data/targets.csv derived/targets.csv
# 3. raw data into scratch (never into the publication folder)
python -I scripts/asas_fetch.py derived/targets.csv raw/asas3
uv venv venv && VIRTUAL_ENV=venv uv pip install skypatrol==0.6.21 pandas numpy
venv/bin/python scripts/asassn_fetch.py derived/targets.csv raw/asassn
python -I scripts/wasp_search.py derived/targets.csv derived/wasp_search.csv
python -I scripts/wasp_fetch.py derived/wasp_search.csv derived/targets.csv raw/wasp
bash scripts/ztf_fetch.sh raw/ztf
(cd raw && sha256sum -c <bundle>/files/provenance/raw_sha256.txt)
# 4. analysis (about 50 min on 2 CPUs) and figures
bash scripts/run_all.sh
```

The ASAS cgi sometimes returns header-only replies under load; repeat the download if a file is shorter than about 3 kB. ASAS-SN data can differ after the 2026 rebuild of Sky Patrol; compare the hashes.

## References

- Thornton M., Montet B. T., White R., Shao A., Kumar D. T. 2026, arXiv:2512.07934.
- Pojmanski G. 2002, Acta Astron. 52, 397 (ASAS-3).
- Shappee B. J. et al. 2014, ApJ 788, 48; Kochanek C. S. et al. 2017, PASP 129, 104502; Hart K. et al. 2023, arXiv:2304.03791 (ASAS-SN Sky Patrol v2).
- Butters O. W. et al. 2010, A&A 520, L10 (SuperWASP DR1). This paper makes use of data from the DR1 of the WASP data (Butters et al. 2010) as provided by the WASP consortium, and computational resources supplied by the project "e-Infrastruktura CZ" (e-INFRA CZ LM2018140) supported by the Ministry of Education, Youth and Sports of the Czech Republic.
- Masci F. J. et al. 2019, PASP 131, 018003; Bellm E. C. et al. 2019, PASP 131, 018002 (ZTF).
- Stassun K. G. et al. 2019, AJ 158, 138 (TIC).
- Mikulasek Z. 2015, A&A 584, A8. Sterne T. E. 1939, MNRAS 99, 451. Gimenez A. 1985, ApJ 297, 405.
- Campaign publications sci:sha256:10fdcb95e99b938d92c8daeeeab1c551fa414dafe456f580f81be934df96118a, sci:sha256:d3cb3bf8909b74c57e86d8077b93a6dac96155c2111f231c4f223b8b21a0b384, sci:sha256:02d77ae92e9db972b5feaaf49f7f0a037d2f89ff9327000c7719cd6e44fc34fa.
