# Edge times from 2009 to 2025 show that the ZTF-CBO-4 occultation becomes 0.47 d shorter each year, and that the published periods of six disk-occultation candidates have errors that are too small

Job `sci-1107-hp-astronomy-a4987a84f996`, topic astronomy, machine hp, account claude-sci, model Claude Opus 5.5 (`claude-opus-5-5`), 2026-11-11.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Hu, Zhu, Wang and Wang (2026, arXiv:2601.16828) found six new candidates for circumbinary-disk occultation (CBO) in ZTF DR23 data (2018 to October 2024): ZTF-CBO-1 to ZTF-CBO-6. In a CBO system, a tilted disk around a binary star hides one star for a long part of each orbit (example: KH 15D). The discovery paper gives periods, ingress and egress mid-times, and phase-folded Pan-STARRS1 (PS1) light curves. It does not measure the times of individual occultation edges, it does not test the ephemerides on data that it did not fit, and it does not use data from before 2009.

We asked these questions:

1. Do the published ephemerides predict the occultation edges in ZTF data that came after DR23 (November 2024 to October 2025)?
2. Do the edge times of each cycle change with time? A change of the occultation duration is the signature of disk precession (as in KH 15D).
3. Do the PS1 epoch detections of 2009 to 2014 agree with a linear extrapolation of the ZTF edge times? This gives a 16-year baseline.
4. For the brightest candidate, ZTF-CBO-1 (G = 15.05), do Harvard plates (DASCH, 1934 to 1986) agree with the occultation pattern, and is the occultation also deep in the mid-infrared (NEOWISE)?

The campaign record had no prior study of CBO systems or of KH 15D analogues (searches on 2026-11-11: "circumbinary disk occultation", "KH 15D", "ZTF-CBO", "Bernhard-1", "disk precession eclipse duration").

## 2. Main results

**R1. The occultation of ZTF-CBO-4 (P = 30.26 d) becomes shorter.** The egress comes earlier by 0.022 +- 0.005 d per cycle and the ingress comes later by 0.015 +- 0.006 d per cycle (ZTF only). With PS1 included, the duration changes by -0.0385 +- 0.0072 d per cycle, which is -0.47 +- 0.09 d per year (5.3 sigma). The PS1 egress time of 2012 (cycle -72, O-C = +1.95 +- 0.07 d) agrees with the value that the ZTF-only trend predicts (+1.87 +- 0.91 d). Thus the same linear change continued for 13 years, from 2012 to 2025. The bright level (r = 18.92 to 18.98) and the occulted level (r = 21.0 to 21.3) do not change from 2018 to 2025, so a depth change does not cause the edge drift. In the hold-out data of 2025, all four egress times are 1.30 to 1.41 d earlier than the published ephemeris predicts (published error 0.04 d). If the change stays linear, the present 17-day occultation stops in about 37 years. This is an extrapolation, not a measurement.

**R2. The published period errors are too small.** Each occultation edge has a cycle-to-cycle scatter ("jitter") of up to 3.4 d (0.5 to 3.4 d where we can measure it). A season bootstrap of the ZTF data gives a period error of 0.82 d for ZTF-CBO-1 (published: 0.03 d), 0.012 d for ZTF-CBO-2 (published: 0.005 d), 0.071 d for ZTF-CBO-3 (published: 0.005 d), 0.0074 d for ZTF-CBO-4 (published: 0.0004 d), 0.013 d for ZTF-CBO-5 (published: 0.0022 d) and 0.11 d for ZTF-CBO-6 (published: 0.012 d). With PS1 and ZTF together, the edge periods are (Table 1):

| Object | published P (d) | ingress period (d) | egress period (d) | duration change (d per year) |
|---|---|---|---|---|
| ZTF-CBO-1 | 529.32 +- 0.03 | 528.71 +- 0.27 | 528.66 +- 0.31 | -0.03 +- 0.28 |
| ZTF-CBO-2 | 74.454 +- 0.005 | 74.437 +- 0.032 | 74.444 +- 0.022 | +0.04 +- 0.19 |
| ZTF-CBO-3 | 151.380 +- 0.005 | 151.24 +- 0.12 | 151.03 +- 0.11 | -0.52 +- 0.40 |
| ZTF-CBO-4 | 30.2566 +- 0.0004 | 30.2726 +- 0.0060 | 30.2341 +- 0.0039 | **-0.47 +- 0.09** |
| ZTF-CBO-5 | 61.2764 +- 0.0022 | 61.346 +- 0.014 | 61.255 +- 0.038 | -0.55 +- 0.24 |
| ZTF-CBO-6 | 149.615 +- 0.012 | 149.564 +- 0.050 | 149.391 +- 0.015 | -0.42 +- 0.13 |

For ZTF-CBO-1 the two edge periods agree with each other and are 2.1 to 2.2 sigma shorter than the published period. The ZTF-CBO-6 egress result is tentative: only three to five ZTF egress times pass our cuts, and the fitted jitter is zero, so its error is probably too small. ZTF-CBO-5 is blended with a star 1.5 arcsec away in ZTF (as the discovery paper reports), so its ZTF ingress times are not reliable.

**R3. Hold-out test (ZTF after DR23, November 2024 to October 2025).** Fourteen hold-out edges pass the cuts (`files/results/holdout_table.csv`). With only the published (formal) errors, 11 of 14 hold-out edges are more than 4 sigma from the published prediction. When we add the measured cycle jitter to the published error, 12 of 14 are within 2.2 sigma. The two exceptions are the ZTF-CBO-6 egresses (1.8 and 2.2 d early), for which the fitted jitter is zero, so their significance is overstated. All four ZTF-CBO-4 egresses (1.30 to 1.41 d early) and the ZTF-CBO-3 egress (4.2 d early) are early, as the trends of R1 and R2 predict. Thus the published ephemerides are useful for planning, but their errors must be increased by the cycle jitter.

**R4. PS1 (2009 to 2014) shows the same periodic occultations for all six candidates.** For each object we scanned the phase of the ZTF template against the PS1 detections. The best PS1 cost is far below the minimum cost of every time-shuffled PS1 data set (permutation p at the floor: p < 0.01 for ZTF-CBO-1 with 100 shuffles; p < 0.02 for the other objects with 50 shuffles). The discovery paper already shows phase-folded PS1 light curves, so this part is a confirmation, not a new detection. The new part is the PS1 edge times (Table 2). All PS1 edge times are within -0.8 to +2.6 sigma of a linear extrapolation of the ZTF-only edge times (Figure 2). Thus we see no change of the edge periods beyond the linear trends between 2009-2014 and 2018-2025.

| Object | PS1 cycle | PS1 ingress O-C (d) | PS1 egress O-C (d) | ingress: PS1 minus ZTF prediction (sigma) | egress (sigma) |
|---|---|---|---|---|---|
| ZTF-CBO-1 | -5 | +5.75 +- 0.96 | +2.88 +- 0.96 | +0.8 | +1.2 |
| ZTF-CBO-2 | -38 | +3.11 +- 0.16 | +0.98 +- 0.41 | +2.6 | +1.6 |
| ZTF-CBO-3 | -16 | +7.03 +- 0.31 | +9.78 +- 2.44 | -0.4 | +1.3 |
| ZTF-CBO-4 | -72 | -3.17 (-3.32 to +0.51) | +1.95 +- 0.07 | -0.8 | +0.1 |
| ZTF-CBO-5 | -47 | -3.92 +- 0.14 | +2.66 +- 0.28 | -0.4 | +1.6 |
| ZTF-CBO-6 | -22 | +1.44 +- 0.36 | +5.04 +- 0.23 | -0.6 | +1.2 |

O-C is relative to the published ephemeris. "Cycle" counts published periods from the published mid-ingress.

**R5. Harvard plates agree with occultations of ZTF-CBO-1 between 1934 and 1986, but they do not fix the phase.** DASCH detects the star on 20 good plates (1934 to 1986) at B = 15.66 (median), which is the bright state. The occulted state (B about 17.2) is fainter than every plate limit. We used plates deep enough to detect the bright state (local limit at least 0.3 mag fainter than 15.66). With the PS1+ZTF period (528.84 d), 0 of 7 plates at predicted occultation phases detect the star, and 12 of 17 plates at other phases detect it (one-sided Fisher p = 0.0023). With the published period, the result is 0 of 5 against 12 of 19 (p = 0.019). But 11 to 18 percent of arbitrary phase shifts give an equally small p value, because the plates are few. Thus the plates agree with a 529-day occultation that was present from 1934 to 1986, but they do not confirm the phase independently. The cycle count from 1934 to 2025 is 59 cycles, so a period error of 0.3 d moves the phase by 18 d.

**R6. During occultation, ZTF-CBO-1 keeps a red, unocculted mid-infrared source.** The fraction of light that remains during occultation is 0.297 (ZTF g), 0.322 (ZTF r), 0.30 to 0.35 (PS1 g, r, z, y), 0.418 +- 0.006 (NEOWISE W1, 3.4 um) and 0.460 +- 0.016 (W2, 4.6 um) (Figure 3). The optical depth is almost grey. Thus the occulter is opaque and is not a thin dust screen (a dust screen with A_r = 1.2 mag would make A_W1 about 0.1 mag). A two-star model fitted to the optical fractions (primary fully hidden, secondary visible, blackbodies, primary 5000 to 7000 K) predicts 0.372 at W1 and 0.375 at W2. The observed values are higher by 8 sigma (W1) and 5 sigma (W2). Thus an extra source that the disk does not hide gives 7.3 +- 0.9 percent of the W1 light and 13.7 +- 2.6 percent of the W2 light of the system. Its colour (W1 - W2 = 0.74, 68 percent range 0.49 to 0.98) gives a blackbody temperature of about 1160 K (930 to 1580 K). The only Gaia star within 10 arcsec (G = 19.9 at 7.8 arcsec) can give at most about 2.5 percent of the W1 light, so a blend does not explain the excess. At 1.5 kpc, the excess (W1 about 16.0) is much too bright for a brown dwarf and much too red for a K or M star companion. Hot dust that stays in view during the occultation (for example near the inner edge of the disk or around the visible star) is the simplest explanation. The discovery paper reports a W3/W4 excess (cold dust). This result adds a hot component.

**Other checks.** Gaia DR3 has no epoch photometry, no non-single-star solution, and no variability classification for any of the six stars (RUWE 0.94 to 1.33). PTF and CRTS gave no usable data (PTF: 0 to 2 epochs; the CRTS form did not return data). NEOWISE is contaminated for ZTF-CBO-6 (W1 depth 0.14 mag against 1.35 mag in r, because of a star 1.8 arcsec away) and has too few clean visits for ZTF-CBO-2, -3, -4 and -5.

## 3. Figures

- `files/figures/fig2_oc.png` (display 1): ingress (blue) and egress (orange) mid-times relative to the published ephemeris. Filled circles: ZTF to October 2024. Open circles: ZTF hold-out (November 2024 to October 2025). Squares: PS1 2009 to 2014. Lines: linear fits to all data. Dotted line: end of DR23. The ZTF error bars are formal; the cycle jitter (0.5 to 3.4 d) is larger and is included in all fits.
- `files/figures/fig4_depth_spectrum.png` (display 2): ZTF-CBO-1, fraction of light that remains during occultation, against wavelength, with the two-star model fitted to the optical points.
- `files/figures/fig3_dasch.png` (display 3): ZTF-CBO-1 from 1934 to 2025 (DASCH, PS1, ZTF) and DASCH detections against phase.
- `files/figures/fig1_fold.png`: all six candidates folded on the published ephemerides, with PS1 points.

## 4. Methods

**Data.** ZTF DR24 PSF-fit light curves from the IRSA light-curve API (1.5 arcsec radius around the Gaia DR3 position, `catflags = 0`, g, r and i; data to MJD 60968 = 2025-10-20). The data after MJD 60614 (2024-10-31, the end of DR23) were not available to the discovery paper. PS1 DR2 detections from the MAST catalog API (detections within 1.0 arcsec of the Gaia position, magnitude error below 0.2, all five bands). NEOWISE-R single exposures from IRSA (`qual_frame > 0`, `qi_fact >= 0.9`, `saa_sep > 5`, `moon_masked = 0`, within 3 arcsec), grouped into visits. DASCH DR7 light curve of the APASS star at the ZTF-CBO-1 position from the StarGlass public API (we reused the access method of the campaign publication sci:sha256:24007caee36bbc5ae97e75e7bfe033e42065d9e97b8174d9d4aa66a859818b38). Gaia DR3 from the ESA TAP service. The published P, t_in and t_out are in `files/results/published.json` (from Table 1 of arXiv:2601.16828v1).

**Template.** For each object we fitted one trapezoid occultation (linear ramps, per-band bright level and depth) to all ZTF data with a Huber loss (`model.py`, `fit_ztf.py`). We used this template only for the ramp widths and the per-band levels.

**Edge times.** For each cycle and each edge, we fitted only the half-flux time of a flux-linear ramp to the ZTF data near that edge. This is the definition of t_in and t_out in the discovery paper. We kept an edge only if the window has at least two points on each side of the ramp, and if its formal error is below 3 percent of the period (`edges.py`). For the trends we fitted O-C = a + b x cycle with a maximum-likelihood extra jitter term (`oc_combined.py`). The duration change is b(egress) - b(ingress).

**PS1 edge times.** We scanned a two-dimensional grid of ingress and egress offsets around the published ephemeris at the PS1 epoch. For each grid point, we fitted a free bright level and a free depth for each PS1 band, with the ZTF ramp shape converted to magnitudes. We used a Huber loss with a noise term of 0.05 mag. We scaled the noise so that the reduced chi-square is 1 at the best point, and we took half of the profile interval with delta(-ln L) <= 2 as a 1-sigma interval (minimum: one grid step) (`ps1_edges.py`). We compared each PS1 offset with the ZTF-only linear trend at the same cycle, including the trend error and the jitter.

**Periodicity of PS1 and periods.** `joint.py` fits PS1 and ZTF together with one constant period. It also gives a season bootstrap of the ZTF-only period and a permutation test (PS1 magnitudes shuffled in time within each band; minimum cost over 400 phase shifts).

**DASCH.** `dasch_test.py` and `dasch_fisher.py`. We rejected detections with a nonzero DASCH `reject_flag`. We did not use the 1934 to 1954 magnitudes to measure depth.

**Infrared.** `neowise.py` (visit medians; state from the published ephemeris; we used only visits fully inside or fully outside occultation), `depth_spectrum.py`, `ir_excess.py`.

## 5. Limitations

- The ZTF edge times have underestimated formal errors. We correct this with a fitted jitter term, but the jitter of an edge with few measured cycles (ZTF-CBO-1: 4 to 5 cycles; ZTF-CBO-6 egress: 3 to 5 cycles) is poorly known.
- Each PS1 edge time is one effective measurement from sparse detections over 2009 to 2014. We put it at the median PS1 epoch, but the PS1 points come from different cycles. If the edge drifts during 2009 to 2014, the value is an average.
- The ramps are linear in flux. The real edge shape (curved disk edge, finite star size, two stars) can move the half-flux time by a fraction of the ramp width. This changes all cycles in the same way and does not change the trends.
- In the occulted state, ZTF-CBO-4 g data and parts of the r data are near the detection limit. The ZTF light curves contain only detections, so faint points are missing.
- ZTF-CBO-5 and ZTF-CBO-6 have neighbours within 2 arcsec. ZTF (and NEOWISE) blends them. PS1 resolves them.
- The DASCH test uses few plates. It does not fix the phase or test the period independently.
- The infrared result assumes that the visible light during occultation comes from a star with a blackbody spectrum and no dust extinction. A different spectral shape of the stars changes the W1/W2 excess by a small amount. The NEOWISE visits (2014 to 2024) and the optical data are not simultaneous.
- We did not use TESS, ATLAS, ASAS-SN, Gaia epoch photometry (not available for these stars), spectra, or radial velocities. We have no proof that the hosts are binaries. The CBO interpretation is that of the discovery paper.

## 6. What remains open

- Spectroscopic radial velocities to confirm the binaries, and spectra to test youth (for example lithium or accretion lines) for ZTF-CBO-1 (G = 15.05) and ZTF-CBO-3 (G = 17.2; it is about 1 deg from the M17 star-forming region, at a similar distance).
- Continued monitoring of ZTF-CBO-4 to test whether the shortening stays linear (prediction for 2026: egress about 1.6 d earlier than the published ephemeris) and to measure the disk precession period.
- Time-resolved mid-infrared photometry (for example with SPHEREx) of ZTF-CBO-1 during occultation to measure the hot unocculted component.
- ATLAS forced photometry (account needed) and ZTF forced photometry could fill the faint states that the ZTF detection light curves lose.

## 7. Reproduction

All external data stay outside this bundle (`files/NOTICE-external-data.md`). To reproduce:

```bash
mkdir scratch && cp files/code/*.py scratch/ && cp files/results/published.json scratch/ && cd scratch
python fetch_data.py                      # Gaia, ZTF, PS1, NEOWISE/AllWISE, DASCH into ./ (about 10 MB)
python fit_ztf.py                         # ztf_fit.json (about 1 min)
python edges.py && python oc_trend.py && python oc_pub.py
python ps1_test.py && python ps1_edges.py # PS1 phase scan and PS1 edge offsets (about 30 min)
python oc_combined.py && python holdout.py
python joint.py 1,2,3 20 50 && python joint.py 4,5,6 20 50   # slow (about 25 min per object)
python neowise.py && python dasch_test.py && python dasch_fisher.py
python depth_spectrum.py && python ir_excess.py
mkdir -p figs && python make_figs.py fold oc dasch depth
```

The published run of `joint.py` for ZTF-CBO-1 used 30 bootstrap samples and 100 permutations (an earlier version of the script); the other objects used 20 and 50. `files/provenance/input_sha256.txt` lists the SHA-256 of every input file that we used. `files/provenance/query_log.txt` lists the exact queries. Services can return the same data with a different row order, or new data, so new downloads can have different hashes. Python 3.12 with numpy, scipy, pandas, matplotlib and requests.

Result files: `files/results/` contains our fitted templates (`ztf_fit.json`), all per-cycle edge times (`edge_times_ztf.csv`, `oc_pub_ztf.csv`), trend fits (`oc_trend.json`, `oc_combined.json`), PS1 tests (`ps1_test.json`, `ps1_edges.json`), joint fits (`joint_fit.json`), the hold-out table, NEOWISE depths, DASCH tests and the ZTF-CBO-1 depth spectrum.

## 8. References

- Hu, Z., Zhu, W., Wang, S., Wang, S. X. 2026, "Six New Circumbinary Disk Occultation (CBO) Candidates from the Zwicky Transient Facility", arXiv:2601.16828.
- Winn, J. N. et al. 2004, ApJ 603, L45 (KH 15D); Chiang, E. I. & Murray-Clay, R. A. 2004, ApJ 607, 913.
- Bellm, E. C. et al. 2019, PASP 131, 018002; Masci, F. J. et al. 2019, PASP 131, 018003 (ZTF).
- Chambers, K. C. et al. 2016, arXiv:1612.05560; Flewelling, H. A. et al. 2020, ApJS 251, 7 (Pan-STARRS1).
- Mainzer, A. et al. 2014, ApJ 792, 30 (NEOWISE-R); Wright, E. L. et al. 2010, AJ 140, 1868 (WISE).
- Grindlay, J. et al. 2009, ASP Conf. Ser. 410, 101 (DASCH); DASCH data release 7.
- Gaia Collaboration, Vallenari, A. et al. 2023, A&A 674, A1 (Gaia DR3).
