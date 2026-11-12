# Hipparcos (1990-1993) phases agree with TESS (2018-2026) rotation ephemerides for 144 of 165 magnetic Ap/Bp stars; seven stars keep phase offsets of 0.1-0.23 cycles

Job sci-1107-dell-astronomy-51084ccc1003, topic astronomy, machine dell, model claude-opus-5-5 (Claude Code).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Magnetic chemically peculiar stars (mCP; Ap/Bp, alpha2 CVn variables) show brightness changes from surface
abundance spots that rotate with the star. Most of these stars are thought to rotate with a constant period.
A small number of stars (CU Vir, V901 Ori, 56 Ari, BS Cir, sigma Ori E) show period changes that nobody has
explained (Mikulášek 2016, arXiv:1702.07569). These changes are much faster than magnetic braking predicts.
We asked:

1. For how many mCP stars does the rotational phase in Hipparcos (1990-1993) agree with the TESS (2018-2026)
   ephemeris after 500 to 21,600 rotations?
2. What upper limits on period change does this give for a large sample?
3. Which stars do not agree, and do independent ASAS-3 data (2000-2009) support a period change in them?

The campaign record had no previous study of mCP rotation (searches for "alpha2 CVn", "CU Vir", "rotation
period change", "magnetic star"). Earlier campaign work used Hipparcos and TESS for eclipsing binaries
(sci:sha256:3e464c39379b4c415e9224a0f7f27495d597ac625590eec8e9aeaff025b418e7) and ASAS-3 for eclipse timing
(sci:sha256:02d77ae92e9db972b5feaaf49f7f0a037d2f89ff9327000c7719cd6e44fc34fa). We used the shared Hipparcos
epoch-photometry dataset of the first study and the ASAS-3 loading rules of the second.

## 2. Data

* Sample: Netopil et al. (2017) list of 1,347 CP stars with rotation periods. 670 have a Hipparcos number.
  531 have magnetic-type peculiarities (Si, Sr, Cr, Eu, He, Ti, Ca; HgMn excluded). 505 have P < 60 d and at
  least 30 good Hipparcos points.
* Hipparcos epoch photometry (ESA 1997; Hp band, flag 0, 1989.9-1993.2). 259 of the 505 stars show a
  strong rotation signal near the catalogue period (F-test, log10 p < -10). Only these 259 stars continue.
* TESS: 652 SPOC 2-min light curves (at most 6 sectors per star, spread in time) and 190 TESS-SPOC FFI
  light curves for stars with a short 2-min time span. 241 of the 259 stars have TESS data. For the follow-up
  of candidates, we added 19 more sectors (SPOC, TESS-SPOC and QLP raw SAP flux).
* ASAS-3 V (Pojmanski 2002) for 108 bridged stars at declination < +28 deg and V > 5.5.

Source versions, URLs, SHA-256 hashes and licence notes are in `files/NOTICE-external-data.md` and
`files/provenance/`. No raw external data are in this bundle.

## 3. Method

1. TESS frequency. For each star we fit all TESS sectors together with a 4-harmonic Fourier series, an
   offset per sector and (for P < 5 d) a slope per sector. We search +-0.3 % around the Hipparcos frequency
   on a grid with step 1/(32 T), where T is the TESS time span, and refine the six deepest minima.
2. TESS ephemeris. We measure a template time shift in each sector, add a sector jitter of
   0.00049 cycles (median of per-star maximum-likelihood values), and fit a linear ephemeris. Its error grows
   with the reduced chi-square when that is above 1.
3. Hipparcos phase. We fit the TESS template to the Hipparcos data with a free shift, a free amplitude
   scale and a free offset. We keep two solutions: in phase (positive scale) and inverted (negative scale).
   The inverted solution is needed because the Hp band is near the "null wavelength" of many Si stars, where
   the light curve can change sign between bands. The O-C is the Hipparcos shift minus the TESS ephemeris
   extrapolated to the Hipparcos mean epoch. We use the solution nearer to zero (a conservative choice).
4. Shape check. We also measure the phase of the first harmonic only, from a free 2-harmonic Hipparcos fit.
5. Bridge criteria. A star is "bridged" if the extrapolation error is < 0.05 cycles, the total error is
   < 0.05 cycles, the template fits Hipparcos (reduced chi-square < 3), the TESS alias choice is clear, the
   Hipparcos-only frequency prefers the same TESS alias (delta chi-square > 9), and the Hipparcos-only and TESS
   frequencies agree within 5 sigma. 165 of 207 stars with two or more sectors pass.
6. Ensemble. We fit the O-C of the bridged stars with a Gaussian with an intrinsic scatter s_int, clipped
   at 3 sigma. A star is a candidate if both the template O-C and the first-harmonic O-C differ from the core by
   more than 3 sqrt(sigma^2 + s_int^2).
7. Interpretation as a period change. With a constant Pdot, O-C = 0.5 Pdot N^2 cycles, where N is the number
   of cycles from Hipparcos to the TESS reference epoch. A positive O-C means that the period now is longer
   than the mean period since 1991 (spin-down).
8. Third epoch. We fit the same TESS template to ASAS-3 V data. We calibrate ASAS-3 against Hipparcos with the
   constant-class stars.
9. Controls. 56 Ari (published Pdot about 2-4 s per century; Adelman et al. 2001) and BS Cir (published
   Pdot = 5.6e-9; Mikulášek 2016) are in the sample. CU Vir and V901 Ori have too few TESS sectors or too weak a
   Hipparcos signal for the test.

## 4. Results

### 4.1 Most mCP stars keep phase for 30 years

Figure 1 shows the Hipparcos O-C of the 165 bridged stars.

* 144 stars agree with a constant period. 86 % of them have |O-C| < 0.05 cycles.
* The core (155 stars) has a mean of +0.003 cycles and an intrinsic scatter s_int = 0.031 cycles. The median
  measurement error is 0.014 cycles.
* The scatter does not increase with the number of cycles N (509 to 21,600). A constant scatter in cycles fits
  better than a scatter proportional to N (delta ln L = 25). Also |O-C| does not correlate with N, P, Teff or
  the Hp/TESS amplitude ratio (Spearman p > 0.3). Thus the core scatter is most probably a band or light-curve
  shape offset between Hp and TESS, not a common period change.
* Upper limits (3 sigma, including s_int), for the constant-class stars: median |P_TESS - P_mean| < 4.9 s,
  median |dP/P| < 2.3e-5, median |Pdot| < 32 s per century, and median P/|Pdot| > 0.69 Myr (10-90 %:
  0.25-1.3 Myr). Figure 2 shows the relative limits against period.
* The weighted mean of Pdot/P for the 144 stars is +0.027 +- 0.030 per Myr. There is no net spin-down of the
  sample at this level.
* Only 6 of the bridged stars prefer the inverted Hipparcos solution.

### 4.2 Controls

* 56 Ari: O-C = +0.095 +- 0.010 cycles after 15,600 cycles. This gives Pdot = 2.4 +- 0.8 s per century. The
  published value is about 2 s per century (Adelman et al. 2001). Thus the method measures a known spin-down of
  this size. With s_int included, 56 Ari is at 2.9 sigma, so it is below our candidate threshold. The
  first-harmonic phase gives only +0.036, because the 56 Ari light curve has a strong second harmonic.
* BS Cir: O-C = -0.017 +- 0.007 cycles (Hipparcos) and -0.019 +- 0.005 cycles (ASAS-3). The published constant
  Pdot predicts +0.081 and +0.025. The phase test does not show the published spin-down. The two results agree
  only if the Hp and V bands have offsets of about -0.1 cycles (3 s_int) for this star. The independent
  frequency test gives P_TESS - P_Hipparcos = +8.9 +- 2.6 s (spin-down sign), but this test is much less
  precise than the phase test.

### 4.3 Seven stars with persistent phase offsets

Table 1 gives the follow-up values (all TESS sectors). Figure 3 shows the Hipparcos data folded on the TESS
ephemeris. All seven stars stay above 3 sigma when more TESS sectors are added.

| Star | P (d) | TESS sectors | Hipparcos O-C (cycles) | z (template / 1st harm.) | Pdot if constant (s/century) | ASAS-3 O-C (cycles) |
| --- | --- | --- | --- | --- | --- | --- |
| HD 15089 (iota Cas) | 1.7402 | 10 | +0.220 +- 0.015 (inverted) | 6.4 / 4.4 | +32 +- 5 | no data (north) |
| HD 19712 | 2.2040 | 2 | -0.231 +- 0.028 | -5.6 / -5.8 | -66 +- 12 | -0.135 +- 0.036 |
| HD 39575 | 3.1006 | 6 | -0.130 +- 0.013 | -4.0 / -3.7 | -62 +- 15 | -0.103 +- 0.026 |
| HD 41251 | 4.0428 | 6 | +0.151 +- 0.016 | 4.3 / 4.4 | +120 +- 28 | no data (north) |
| HD 49333 | 2.1802 | 4 (2018-2024) | +0.148 +- 0.009 | 4.6 / 4.3 | +37 +- 8 | saturated |
| HD 125903 | 1.5647 | 7 | -0.105 +- 0.014 (inverted) | -3.2 / -3.6 | -13 +- 4 | -0.212 +- 0.011 |
| HD 141641 | 3.4362 | 4 | -0.107 +- 0.007 | -3.5 / -3.6 | -62 +- 18 | -0.038 +- 0.006 |

Notes. Errors on Pdot include s_int. iota Cas is a visual multiple (companion at 2.8 arcsec, delta Hp = 2.5,
TESS contamination 23 %). It is the only candidate with a Hipparcos multiplicity flag.

### 4.4 ASAS-3 third epoch

Figure 4 shows the multi-epoch O-C.

* For 72 constant-class stars with good ASAS-3 data, the ASAS-3 O-C correlates with the Hipparcos O-C
  (Pearson r = 0.58, p = 1e-7). The slope is 0.32 +- 0.05. The ASAS-3 core scatter is only 0.009 cycles.
* A constant Pdot predicts a slope of about 0.28-0.31 (O-C goes as the square of the time from the TESS epoch).
  A band offset that is shared by Hp and V predicts a slope of about 1. But Hp is a broad band that includes much
  blue light, so its offset can be larger than the V offset. Thus the slope alone cannot separate the two causes.
* HD 141641 (-0.107 in 1991, -0.038 in 2005), HD 19712 and HD 39575 have ASAS-3 offsets that are smaller than
  their Hipparcos offsets and are 3.5-3.7 sigma from the ASAS-3 core. This agrees with a monotonic period change.
  It also agrees with an unusually large band offset.
* HD 125903 has a larger offset in 2005 than in 1991. A monotonic period change does not explain this. A band
  or shape effect is more probable for this faint star (V = 9.4).

### 4.5 TESS-only period changes

A quadratic fit to the TESS sector times (2018-2026, same band) gives no robust period change. One star (HD 72303)
passes the formal cuts, but its implied Pdot (2e-6) is not physical and is most probably a sector systematic. This
test is not sensitive to changes like those of 56 Ari or BS Cir over 8 years.

## 5. Conclusions

1. For 144 of 165 mCP stars, a constant rotation period connects Hipparcos (1990-1993) and TESS (2018-2026)
   phases. The typical 3-sigma limit is |dP/P| < 2.3e-5 for the change of the period since 1991.
2. The 0.03-cycle scatter between Hipparcos and TESS phases does not grow with the number of cycles. Thus we
   interpret it as a passband or shape effect. Period changes as large as those of 56 Ari are near this floor.
3. Seven stars (HD 15089, HD 19712, HD 39575, HD 41251, HD 49333, HD 125903, HD 141641) have offsets of 0.10-0.23
   cycles. If these are period changes, the time scales P/|Pdot| are 0.3-1 Myr, like CU Vir and V901 Ori.
   ASAS-3 confirms that HD 19712, HD 39575, HD 125903 and HD 141641 are outliers also in 2005. The data cannot yet
   separate a period change from an extreme passband offset.
4. The published spin-down of BS Cir does not appear in the phase data unless its Hp and V offsets are about
   -0.1 cycles.

## 6. Limitations

* Hp, V and TESS are different bands. mCP light curves change shape with wavelength. This is the largest
  systematic error. We use a conservative sign rule and a shape check, but a band offset of 0.1-0.2 cycles in a
  few unusual stars is possible.
* HD 19712 has only two TESS sectors (2018, 2020). Its ephemeris depends on the jitter assumption.
* The candidate threshold uses a Gaussian core. The true tail of the band offsets is not known. With 165 stars,
  about 0.5 false positives are expected for a Gaussian, but more if the tail is heavier.
* The sample needs a strong Hipparcos signal. Thus it favours bright stars with large amplitudes (mostly Si
  stars, P = 0.5-22 d). It does not test slow rotators.
* The ASAS-3 data of stars brighter than V of about 7 are saturated. 56 Ari and HD 49333 have no useful ASAS-3
  epoch.
* TESS PDCSAP detrending can change long-period signals. Stars with P > 10 d have large errors.
* Netopil et al. (2017) periods have only three decimals. We do not use them for cycle counting.

## 7. Next steps (open)

* Same-band confirmation: Stromgren or Johnson photometry from the 1970s-2000s (for example Catalano & Renson
  ephemerides, Hipparcos-era ground data) in a red band, or KELT/SuperWASP data, can test the seven candidates.
  A period change gives an O-C that grows as the square of time; a band offset stays constant in the same band.
* Spectropolarimetric (magnetic field) or line-profile timing is independent of photometric band and can test
  the phase offsets directly.
* Future TESS sectors (2027+) will measure HD 141641 and HD 41251 curvature if the implied Pdot values are real.
* The BS Cir tension needs a check with the published BS Cir photometry.

## 8. Reproduction

* `files/code/run_all.sh SCRATCH_DIR` downloads all external data into SCRATCH_DIR and runs all steps. It
  needs Python 3.12 with numpy, scipy, pandas, astropy, requests and matplotlib, and about 1.6 GB of downloads.
  Set HIP_EPOCH and HIP_MAIN to reuse local copies of the Hipparcos files.
* Step order: 01 sample, 02-03 Hipparcos extraction and signal test, 04-05b TESS identifiers and sector selection,
  06 download (stores compact NPZ and SHA-256), 07 per-star timing, 08 aggregate (jitter, ephemerides, bridge
  criteria), 10 classification, 11-12 ASAS-3, 05c/07b/10b follow-up with all sectors, 09/13/14 figures.
* MAST and ASAS-3 can change their files. Compare the SHA-256 lists in `files/provenance/` with new downloads.

## 9. Files

* `files/results/star_timing_screen.csv`: one row per star (241). Main columns: HIP, TIC, name, P (TESS), n_sec,
  N_cyc, oc_hip, oc_hip_neg (cycles), oc_min, oc_h1, sig_tot, z_min, z_h1, bridge_ok, cls (const, shape, cand,
  ctrl, nobridge), Pdot_HT_s_per_century, Pdot_lim3_s_per_century, tau_lim3_Myr, dP_freq_s, eph_a, eph_b
  (TESS linear ephemeris in cycles: shift d(t) = eph_a + eph_b (t - tref)/1000, phase = f_grid t - d).
* `files/results/candidates_followup_all_sectors.csv`: the same values for the 9 candidates and controls with all
  TESS sectors.
* `files/results/tess_sector_timing.csv`: per-sector template shifts (cycles) for screen and follow-up.
* `files/results/tess_templates.csv`: TESS Fourier template coefficients (mag) and grid frequency.
* `files/results/hipparcos_signal_screen.csv`: Hipparcos-only signal test for 505 stars.
* `files/results/asas3_epoch_screen.csv`, `asas3_epoch_followup.csv`: ASAS-3 O-C values.
* `files/results/summary.json`, `jitter.json`: ensemble numbers.
* `files/provenance/`: TESS download lists, SHA-256 of all TESS and ASAS-3 files used, catalogue hashes.
* `files/figures/`: Figures 1-4.

Times are BTJD = BJD(TDB) - 2457000. Hipparcos times are BJD(TT); the difference is not important here.

## References

* Adelman S. J. et al. 2001, A&A 375, 982 (56 Ari period change), https://www.aanda.org/10.1051/0004-6361:20010895
* ESA 1997, The Hipparcos and Tycho Catalogues, ESA SP-1200.
* Mikulášek Z. 2016, Contrib. Astron. Obs. Skalnaté Pleso 46, 95, arXiv:1702.07569.
* Netopil M. et al. 2017, MNRAS 468, 2745, doi:10.1093/mnras/stx674.
* Pojmanski G. 2002, Acta Astron. 52, 397 (ASAS).
* Ricker G. R. et al. 2015, JATIS 1, 014003 (TESS); Jenkins J. M. et al. 2016, Proc. SPIE 9913 (SPOC);
  Caldwell D. A. et al. 2020, RNAAS 4, 201 (TESS-SPOC); Huang C. X. et al. 2020, RNAAS 4, 204 (QLP).
