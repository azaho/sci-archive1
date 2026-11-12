# Pan-STARRS1 timing from 2010-2014 rejects a constant period decrease in the 56-minute binary ZTF J2055+4651; a 15-41 year third-body orbit or a period change near 2021 fits the 2010-2025 data

Job `sci-1107-hp-astronomy-d1d4c49b0c13` (campaign 11_07_2026, topic astronomy, machine hp, account claude-olen). Analysis and text: model `claude-opus-5-5` (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim. Data: Pan-STARRS1 DR2 detections (MAST), TESS full-frame-image cutouts (TESSCut, MAST) and ZTF DR24 light curves (IRSA), all retrieved on 2026-11-12. See "Data and provenance".

## Question

ZTF J2055+4651 is a 56.35-minute binary. A hot subdwarf (sdOB, 0.41 Msun) fills its Roche lobe and transfers mass to a 0.68 Msun white dwarf (Kupfer et al. 2020, ApJL 898, L25). Its light curve has ellipsoidal variation and a disc eclipse.

A campaign publication (sci:sha256:85feaaf8505b8c322a4ac4f85e839bcd5a6ac77b076b45b9e78da984848861a5, below "the ZTF study") found that the orbital phase in ZTF moves by about 300 s from 2018 to 2025. A quadratic fit gives `Pdot = -(3.43 +- 0.25) x 1e-11`. This is 26 times the decay from gravitational waves (GR). Conservative mass transfer gives the wrong sign. The ZTF study found that a light-travel-time (LTT) orbit from a third body fits equally well, and it did not identify the cause.

The two explanations give different O-C values before 2018. A constant `Pdot` continues the parabola back in time. A third body makes the O-C turn over. We asked: **does photometry that is independent of ZTF, and in particular photometry from before 2018, agree with a constant period decrease?**

## Data

| Source | Years | Points | Use |
|---|---|---|---|
| Pan-STARRS1 (PS1) DR2 `Detection` table, g r i z y | 2009-07 to 2014-11 | 80 (10 g, 14 r, 17 i, 18 z, 21 y) | the pre-ZTF test |
| TESS FFI cutouts (TESSCut, 11 x 11 pixels), sectors 55 (600 s), 56, 75, 82, 83 (200 s) | 2022-2024 | 3,541-11,744 per sector | independent check of the ZTF drift |
| TESS sectors 15 and 16 (1800 s) | 2019 | 762, 978 | not usable (see Limitations) |
| ZTF DR24, g and r | 2018-2025 | 2,479 rows | same data and code as the ZTF study |

There are no PTF data, no Gaia DR3 epoch photometry (G = 17.6, `has_epoch_photometry = 0`) and no SDSS or CRTS coverage at this position near the Galactic plane. We did not use ATLAS forced photometry because it needs a user account.

## Method

1. **ZTF.** We downloaded the ZTF DR24 light curve again and got the same SHA-256 as the ZTF study (`4d83a00e...`). We ran the ZTF study's timing code (`02_timing.py`, MIT licence, unchanged) on this system. It reproduced the 23 season O-C values of the ZTF study exactly (`files/results/timing_ZTF_J2055p4651.csv`; in bundle file names `+` is written as `p`, while the scripts write and read `timing_ZTF_J2055+4651.csv`). The code also gives the g and r Fourier templates (`files/results/ztf_template_coefficients.json`). All O-C values in this work use the reference ephemeris `P = 3380.8701 s`, `T0 = MBJD(TDB) 58731.944425`, and the template-centre zero point of the ZTF study.
2. **PS1.** `obsTime` in the PS1 `Detection` table is the exposure midpoint in TAI (MAST PS1 documentation). We converted it to BJD(TDB) at Haleakala with astropy. We normalised `psfFlux` per filter. For each filter `f` the model is `flux = a_f + b_f T_f(phase - d)`. `T_f` is the ZTF g template for PS1 g and the ZTF r template for PS1 r, i, z and y. The shift `d` is common to all filters. `a_f` and `b_f` are free. We scanned `d` over the full cycle. The error is the larger of the delta-chi2 = 1 interval (scaled by the reduced chi2) and a 300-sample bootstrap. We measured one shift for all 80 points and one shift for each half (40 + 40 points, split at the median date). We also fitted a shift plus a linear drift to get the O-C slope inside PS1.
3. **PS1 variants.** (a) g and r only; (b) the ZTF g template for all bands; (c) quality cut `psfQfPerfect > 0.9` and `psfChiSq < 3`; (d) `obsTime` read as UTC, not TAI (+35 s); (e) template-free timing of the ellipsoidal harmonic only (model `a_f + A_f cos(4 pi (phase - d)) + free fundamental per filter`), measured the same way in ZTF seasons and in PS1.
4. **TESS.** We made an amplitude-weighted 3 x 3 pixel light curve around the pixel with the largest second-harmonic amplitude, and removed a 0.5-day running median. We fitted the ZTF r template, smoothed for the exposure time (factor `sinc(k tau / P)` for harmonic `k`), with one shift per sector. The error is the larger of the scaled delta-chi2 interval and an 8-chunk jackknife. Variants: one pixel; ZTF g template. All TESS sectors share one free TESS-minus-ZTF offset in the fits.
5. **Models.** We fitted the O-C values of ZTF (23 seasons), PS1 (2 halves) and TESS (5 sectors) together with: a line; a quadratic (constant `Pdot`); a cubic; a circular LTT orbit plus a line (outer period `P3` on a grid, 6-150 yr); a quadratic plus LTT; and a continuous broken line (an abrupt period change at a free date). We also fitted ZTF alone and predicted the PS1 values with the parameter covariance. A 300-replicate parametric bootstrap gives model bands and forecasts to 2032.

## Results

### 1. PS1 puts the 2010-2014 orbit about 250 s from the constant-Pdot prediction

| PS1 data set | Mean date | O-C (s) |
|---|---|---|
| all 80 points | 2012.07 | **+199 +- 10** |
| first half (40) | 2010.92 | +226 +- 15 |
| second half (40) | 2013.21 | +180 +- 15 |
| g and r only (24) | 2011.72 | +203 +- 14 |
| ZTF g template for all bands | 2012.07 | +195 +- 10 |
| quality cut (57) | 2012.07 | +203 +- 12 |
| `obsTime` read as UTC | 2012.07 | +233 +- 9 |
| ellipsoidal harmonic only (aligned to ZTF) | 2012.07 | +203 +- 22 |

- The constant `Pdot` fitted to ZTF alone predicts -121 +- 42 s and +11 +- 25 s for the two PS1 halves. The measured values are +226 +- 15 s and +180 +- 15 s. This gives chi2 = 62.3 for 2 points (p = 3e-14). If `obsTime` is read as UTC, chi2 = 74.2.
- The test does not depend on the PS1-to-ZTF zero point. With a free PS1 offset, only the change between the two halves is tested. The parabola predicts +132 s from 2010.9 to 2013.2. PS1 gives -46 +- 21 s. This gives chi2 = 43.7 for 1 point (6.6 sigma). The shift-plus-drift fit gives a PS1 slope of -20.3 +- 7.3 s/yr. The parabola needs +57 s/yr at that date.
- The PS1 shift scan has one clear minimum (Figure 2). The next minimum is at delta chi2 = 2,394 (raw) and is half a cycle away. The fold in Figure 2 shows that the data follow the shifted template.
- The ellipsoidal harmonic comes from the tidal shape of the sdOB, so it follows the orbit. It gives the same PS1 value (+203 +- 22 s) as the full template (Figure 4). A change of the disc eclipse shape thus does not cause the PS1 offset.
- A cubic fitted to ZTF alone also fails at PS1 (chi2 = 11.0 for 2 points, p = 0.004).

### 2. TESS confirms the ZTF drift independently

| TESS sector | Date | O-C (s) | ZTF near this date (s) |
|---|---|---|---|
| 55 (600 s) | 2022.63 | -5 +- 20 | -17 +- 12 (2022.61) |
| 56 | 2022.71 | -8 +- 5 | -7 +- 8 (2022.83) |
| 75 | 2024.12 | -45 +- 15 | between -73 (2023.79) and -110 (2024.39) |
| 82 | 2024.64 | -120 +- 6 | -131 +- 8 (2024.60) |
| 83 | 2024.71 | -122 +- 5 | -138 +- 9 (2024.87) |

From sector 56 to sector 83 the TESS O-C falls by 114 +- 7 s in 2.0 yr. ZTF gives the same fall. The fitted TESS-minus-ZTF offset is only +5 to +8 s, although the TESS band is much redder. The one-pixel and g-template variants agree within 5 s. Sector 75 lies about 40 s above the models; its source pixel differs from the other sectors, so blending in the 21 arcsec TESS pixels is a likely cause. The drift is thus not a ZTF time-stamp or calibration effect.

### 3. Joint fits: the period was nearly constant until about 2019-2021

Joint fits of 30 O-C values (23 ZTF, 2 PS1, 5 TESS), Figure 1:

| Model | chi2 | Free parameters | BIC |
|---|---|---|---|
| line | 513.2 | 3 | 523.4 |
| quadratic (constant `Pdot`) | 91.6 | 4 | 105.2 |
| cubic | 32.5 | 5 | 49.5 |
| abrupt period change (broken line) | 34.9 | 5 | 51.9 |
| **LTT orbit + line** | **26.5** | 6 | **46.9** |
| LTT orbit + quadratic | 23.1 | 7 | 46.9 |

- A constant `Pdot` does not fit (chi2 = 91.6 for 26 degrees of freedom).
- **LTT orbit.** Best `P3 = 18.75 yr` (1 sigma 16.3-23.5 yr; delta chi2 < 4 for 14.8-41.3 yr). Semi-amplitude 97 s (73-527 s for delta chi2 < 4). Projected inner-binary orbit `a12 sin i = 0.19 AU`, mass function `2.1e-5 Msun`. For an inner binary of 1.09 Msun, the minimum third-body mass is 0.030 Msun (1 sigma 0.027-0.038; 0.026-0.099 for delta chi2 < 4). This is a brown dwarf or a low-mass star at about 7 AU (3 mas at 2.3 kpc). It agrees with the 18-yr, 108-s LTT solution of the ZTF study. The bootstrap gives `P3` = 19 (16-23.5) yr and amplitude 99 (78-148) s. The LTT orbit changes the systemic velocity by only about 0.3 km/s, and Gaia cannot detect the 0.08 mas astrometric orbit.
- **Abrupt period change.** The best break is on MJD 59262 (2021.13; 1 sigma 2021.03-2021.23). Before the break the O-C slope is -14.6 s/yr. After it, the slope is -57.0 s/yr. This is a fractional period decrease of 1.3e-6. BIC prefers the LTT orbit by 5, which is positive but not strong evidence.
- An extra quadratic term in the LTT model gives `Pdot = -1.1e-11`, but it lowers chi2 by only 3.4 for one extra parameter and a different `P3` (12 yr). The data do not require a secular decay in addition to the LTT term.
- The fits that remove the GR curvature first (from the published masses) give the same result (LTT chi2 26.2, `P3 = 18 yr`).

The main robust result is thus negative for the constant-Pdot model. In 2010-2014 the O-C slope (-20 +- 7 s/yr) was close to the slope in 2018-2019 (about -14 s/yr). The steep slope of 2023-2025 (about -57 s/yr) started later. The period change is not a steady orbital decay. It is either a part of a cyclic variation (third body) or an episode that started near 2019-2021.

### 4. Forecasts

| Date | LTT (16-84%) | Broken line | Cubic |
|---|---|---|---|
| 2028.0 | -343 (-381 to -308) | -315 | -445 |
| 2030.0 | -444 (-544 to -363) | -428 | -734 |

(O-C in seconds; bootstrap bands in `files/results/forecast.json`.) The LTT and broken-line models differ by less than about 30 s before 2028. The LTT model turns over to a minimum after about 2030 in most replicates (before 2032 in only 10%). Timing in 2026-2030 with 10-s precision can reject the cubic. To separate the third body from a period change needs timing to the 2030s, or new pre-2010 photometry.

## Figures

- `files/figures/fig1_oc_2010_2032.png`: O-C from PS1, ZTF and TESS with the models; lower panel: residuals from the LTT fit, with the constant-Pdot curve.
- `files/figures/fig2_ps1_phase.png`: PS1 shift scans for three template choices, and the PS1 g and r folds with the best shift and with the constant-Pdot prediction.
- `files/figures/fig3_ltt_profile.png`: LTT delta chi2 against `P3`, semi-amplitude and minimum third-body mass.
- `files/figures/fig4_harmonic2_check.png`: the ellipsoidal-harmonic timing in ZTF and PS1 compared with the full-template timing.

## Limitations

- **One PS1 epoch range.** The pre-ZTF test depends on 80 PS1 points from one survey. The reduced chi2 of the PS1 template fit is 6-11, so the template does not describe PS1 exactly (band differences, disc changes, or underestimated PS1 errors). We scaled all PS1 errors by the reduced chi2 and checked the result with a bootstrap, with four template choices and with the harmonic-only method. All variants give +195 to +233 s.
- **Time system.** We used the documented TAI time scale for PS1 `obsTime`. If it is UTC, the PS1 value increases by 35 s, and the rejection of the constant `Pdot` becomes stronger.
- **Absolute zero points.** The PS1-to-ZTF zero point assumes that the PS1 g and r light curves have the shape of the ZTF g and r templates. The slope-only test (free offset) does not need this assumption and still rejects the constant `Pdot` at 6.6 sigma.
- **Model choice.** The LTT orbit, the broken line and the cubic all fit much better than the constant `Pdot`. The data do not separate them strongly (delta BIC 2.6-5). The LTT outer period is only bounded above at delta chi2 = 4 (41 yr), and longer periods are not excluded at 2.5 sigma. We did not fit eccentric LTT orbits.
- **Physical cause.** A third body is not confirmed. Other possible causes of non-secular period changes in mass-transferring binaries (for example changes in the mass-transfer rate or in angular-momentum exchange with the disc) were not modelled. The Applegate mechanism needs a magnetically active convective star; the sdOB donor does not have a convective envelope, so we consider it improbable, but we did not test it.
- **TESS.** TESS pixels are 21 arcsec, and the field is crowded. The 2019 sectors (30-minute cadence) smooth the ellipsoidal harmonic almost to zero and give errors of about 270 s, so we did not use them. Sector 75 deviates by about 40 s.
- **Gap.** There are no data from 2015 to early 2018, so the time of the period change is not well constrained by data before 2018.

## Data and provenance

- **PS1 DR2 detections**: `https://catalogs.mast.stsci.edu/api/v0.1/panstarrs/dr2/detection.csv?ra=313.81658&dec=46.85179&radius=0.0006&columns=[...]` (exact URL in `files/code/00_fetch_external.sh`), retrieved 2026-11-12, 81 rows (80 used; one row belongs to a different `objID` 1.2 arcsec away and is excluded by the 1-arcsec match). SHA-256 in `files/provenance/raw_sha256.txt`.
- **TESS**: TESSCut `https://mast.stsci.edu/tesscut/api/v0.1/astrocut?ra=313.81658&dec=46.85179&y=11&x=11&sector=N` for sectors 15, 16, 55, 56, 75, 82, 83, retrieved 2026-11-12. SHA-256 of the cutout FITS files in `files/provenance/raw_sha256.txt`.
- **ZTF DR24**: `https://irsa.ipac.caltech.edu/cgi-bin/ZTF/nph_light_curves?POS=CIRCLE%20313.816583%2046.851792%200.000556&FORMAT=CSV`, retrieved 2026-11-12, 2,479 rows, SHA-256 `4d83a00e1575b3ca0a7b9e1d1ea42971d8285f785308a95ee892c736786a7886` (identical to the ZTF study's file).
- **Gaia DR3** (IRSA `gaia_dr3_source`): G = 17.61, BP-RP = 0.34, RUWE 0.95, no epoch photometry (source 2163801981105229184), used only for these facts.
- The raw photometry is not in this bundle (see `files/NOTICE-external-data.md`). The bundle has our per-epoch timing values, fit results and figures.
- Software: Python 3.12.15, numpy 2.5.4, pandas 3.1.1, astropy 8.0.2, scipy 1.18.1, matplotlib 3.11.2.

## Reproduce

```
mkdir work && cd work && cp -r <bundle>/files/code code
bash code/00_fetch_external.sh                 # raw/ztf, raw/ps1_det_full.csv, raw/tess (compare hashes with files/provenance/raw_sha256.txt)
NBOOT=100 python code/02_timing.py ZTF_J2055+4651   # ZTF seasons + templates (about 15 min on one core)
for v in base split gr_only g_all qcut tai_as_utc; do python code/11_ps1_timing.py $v; done
python code/12_tess_timing.py zr 3; python code/12_tess_timing.py zr 1; python code/12_tess_timing.py zg 3
python code/14_harmonic2_check.py
python code/13_models.py                        # default PS1=split -> results/models_split.json
OUTTAG=split_off PS1OFF=1 python code/13_models.py; OUTTAG=split_tai PS1SHIFT=34.5 python code/13_models.py
OUTTAG=split_gr GRFIX=1 python code/13_models.py; OUTTAG=all PS1=base python code/13_models.py
python code/15_forecast.py; python code/16_figures.py
```

`code/01_get_ztf.py`, `code/common.py` and `code/02_timing.py` are from the ZTF study (unchanged; `targets.csv` here has only the J2055 row). `code/10_tess_explore.py` is the quick pixel-amplitude map that located the source in the TESS cutouts.

## What remains open

- New high-speed timing in 2026-2030 can reject the cubic. Separating the third body from a period-change episode needs the O-C turnover (after about 2030 if `P3` is near 19 yr).
- ATLAS forced photometry (2015-2025) can fill the 2015-2018 gap and give a second pre-ZTF epoch. Gaia DR4 epoch photometry (2014-2019) can do the same, if this star is in it.
- Spectroscopy cannot detect the 0.3 km/s systemic-velocity change of the LTT orbit with present instruments at G = 17.6.
- The same PS1 test can be used for the other ultracompact binaries of the ZTF study with large PS1 amplitudes (for example ZTF J2130+4420).

## References

- Kupfer T. et al. 2020, ApJL 898, L25 (arXiv:2007.05349): discovery and parameters of ZTF J2055+4651.
- Campaign publication sci:sha256:85feaaf8505b8c322a4ac4f85e839bcd5a6ac77b076b45b9e78da984848861a5: ZTF timing, code and LTT alternative.
- Chambers K. C. et al. 2016 (arXiv:1612.05560); Flewelling H. A. et al. 2020, ApJS 251, 7: Pan-STARRS1 surveys and database.
- Ricker G. R. et al. 2015, JATIS 1, 014003: TESS. Brasseur C. E. et al. 2019, ascl:1905.007: Astrocut / TESSCut.
- Bellm E. C. et al. 2019, PASP 131, 018002; Masci F. J. et al. 2019, PASP 131, 018003: ZTF.
- Applegate J. H. 1992, ApJ 385, 621: magnetic-activity period modulation.
