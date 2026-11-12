# A Moon-phase bias near the ZTF detection limit explains the 30-day signal of SN 2020sgf, and SN Ia controls pass a periodicity test as often as stripped-envelope supernovae

Job: sci-1107-dell-astronomy-5d826df4365b. Topic: astronomy. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal claim of authorship.

## 1. Question

Horowicz, Ofek and Gal-Yam (2026, arXiv:2608.18207) searched 34 Type Ib/c supernovae (SNe) from the Zwicky Transient Facility (ZTF) for periodic brightness changes. They found three two-band detections: SN 2022jli (12.4 d), SN 2022esa (34 d) and SN 2020sgf (30 to 36 d, or 56 to 60 d). They used these detections to say that about 20 percent of stripped-envelope SNe can have binary-driven periodic modulation. Two of the three periods are near the 29.53-day lunar synodic period. For SN 2020sgf, the residuals had a negative correlation with the Moon illumination. The authors did not find the cause and they left the Moon test for future work. They did not use a control class of supernovae that we do not expect to be periodic.

We tested these questions:

1. Do ZTF supernova photometry residuals change with the Moon phase? If yes, for which supernovae, and why?
2. Can a Moon effect make 25 to 38 d "periods" in the cubic-baseline-plus-sinusoid test?
3. Does the same test give "periodic" detections in normal SNe Ia and SNe II (control classes) as often as in stripped-envelope SNe (SESN)?
4. Do the published candidates (SN 2020sgf, SN 2022esa, SN 2022jli, SN 2019tsf) survive a Moon term and a more flexible baseline?

No earlier campaign publication studies supernova light curves (campaign search on 2026-11-12 for "supernova", "SN Ia", "stripped-envelope", "ZTF Bright Transient Survey"). This work is new in the campaign record.

## 2. Data

- Sample: the ZTF Bright Transient Survey (BTS) catalog of SNe with peak magnitude 18.5 or brighter (7,427 SNe, downloaded 2026-11-12). We used all 2,121 SNe that are not normal "SN Ia", and 800 random "SN Ia" (pandas random_state=1) as a control. We added SN 2022jli (ZTF22aapubuy) and SN 2019tsf (ZTF19ackjszs), which are not in this BTS list. ALeRCE had no light curve for 2 objects. Total: 2,921 light curves.
- Photometry: ZTF public alert photometry (PSF photometry on difference images) from the ALeRCE broker API v1 (`https://api.alerce.online/ztf/v1/objects/<ZTFID>/lightcurve`), with detections, 5-sigma limits (`diffmaglim`) and non-detection limits. Downloaded 2026-11-12. We used only positive detections with real-bogus score rb >= 0.3 (the `drb` score is often 0 or absent in the ALeRCE v1 output).
- Moon geometry: astropy 8.0.2 at Palomar (illuminated fraction from the Sun-Moon elongation, Moon altitude, Moon separation, synodic phase).
- Horowicz et al. used forced photometry from the Lasair broker. We did not have forced photometry. Alert photometry has a 5-sigma detection cut. Section 4.1 shows that this cut is the main source of the Moon bias.

## 3. Method

Decline window: for each SN and band (g, r), from the brightest detection to the first gap longer than 50 d, at most 300 d after peak (no 300 d limit for the four named SNe, as in Horowicz et al.).

**Moon residual test (script 03).** We fitted a weighted cubic polynomial to the detections of each light curve with at least 12 detections (error floor 0.015 mag). We regressed the residuals on Moon illuminated fraction inside each light curve, with a cluster bootstrap over SNe. We split the points by a Moon-independent brightness measure: the "dark-time margin" (the median limit of the light curve at Moon-down or illumination < 0.25 epochs, minus the smooth model magnitude). We also split the points by Moon above or below the horizon. To predict the bias of the detection cut alone, we simulated each light curve: the smooth model at every epoch (detections and non-detections), Gaussian noise from the epoch limit, a detection only if the simulated magnitude is brighter than the epoch limit, and a new cubic fit (3 realisations). Residuals with |r| > 0.5 mag were removed in data and simulation.

**Periodicity test (script 04), after Horowicz et al.** For each light curve with at least 20 detections: a joint fit of a polynomial baseline plus a sinusoid at each trial frequency, from P = 3 d to P = T/2.5, frequency step 1/(5T). The errors are scaled by sqrt(reduced chi-square) when it is above 1. A detection has p < 1e-4 (chi-square, 2 degrees of freedom) and amplitude above sigma_res/sqrt(N). A two-band detection has g and r detections with |Pg - Pr| < P^2/T. Variants:

- v0: cubic baseline, all detections (the Horowicz et al. rule).
- v1: cubic baseline, only detections at least 1 mag above the epoch limit.
- v2: cubic baseline plus a linear Moon-illumination term.
- v4: degree-5 polynomial baseline (Horowicz et al. tested degrees 3 to 6).
- v5: degree-5 baseline plus the Moon term.
- sim: v0 on the truncation-only simulations (no intrinsic periodicity).

For every best fit we calculated the correlation between the fitted sinusoid and the Moon illumination at the observation epochs (negative = brighter at full Moon). Script 09 applies the Horowicz et al. white-noise residual bootstrap (2,000 resamples, FAP < 5e-4) to all v0 two-band detections. Script 08 injects sinusoids (12.5, 30, 45 d; semi-amplitude 0.03, 0.07, 0.15 mag) into the real light curves.

Classes: SESN = Ib, Ic, Ic-BL, Ib/c, IIb, Ibn, Icn, Ib-pec, Ic-pec. Ia control = SN Ia, Ia-91T, Ia-91bg. II = SN II, IIP, IIL, II-pec. SN 2022esa (Ia-CSM) is in the class "other".

## 4. Results

### 4.1 The Moon bias is a detection-limit effect (Figure 1)

The median 5-sigma limit at full Moon with the Moon up is 0.8 (r) to 1.1 (g) mag shallower than with the Moon down. It does not change when the Moon is down (Figure 1a). Residual slope versus illumination (mag per unit illuminated fraction; negative = brighter at full Moon), all classes, 1,585 SNe, 67,303 detections:

| Dark-time margin | Moon up: data | Moon up: truncation simulation | Moon down: data |
| --- | --- | --- | --- |
| < 0.5 mag | -0.193 +- 0.024 | -0.233 +- 0.021 | -0.012 +- 0.011 |
| 0.5-1 mag | -0.079 +- 0.012 | -0.134 +- 0.009 | +0.004 +- 0.007 |
| 1-1.5 mag | -0.029 +- 0.007 | -0.039 +- 0.005 | +0.005 +- 0.006 |
| 1.5-2.5 mag | -0.008 +- 0.004 | -0.005 +- 0.002 | +0.008 +- 0.004 |
| > 2.5 mag | +0.008 +- 0.007 | -0.001 +- 0.001 | +0.008 +- 0.006 |

(Full table, also for SN Ia and core-collapse SNe separately: `files/results/moon_slopes.csv`.)

Near the limit, SNe look brighter at full Moon, but only when the Moon is up. The detection-cut simulation gives the same sign and size. The cause is selection: at full Moon the limit is shallower, so only the positive noise excursions of a faint SN become alerts. For SNe more than 1.5 mag above the dark-time limit, the slope is within +-0.02 mag per unit illumination. A direct moonlight error in the photometry of bright points is therefore at most about 0.01 mag in semi-amplitude. The published candidate semi-amplitudes are 0.07 to 0.20 mag.

### 4.2 Fits at 25 to 38 d lock to the Moon phase (Figure 3b)

With all detections, the best-fit sinusoids with periods of 25 to 38 d are brighter at full Moon in 181 of 294 light curves (binomial p = 9e-5; degree-5 baseline: 145 of 212, p = 9e-8). Best fits at other periods show no lock (581 of 1,132, p = 0.39). When we keep only detections at least 1 mag above the limit, the lock goes away (71 of 127, p = 0.21). With a Moon term (v5) it also goes away (107 of 202, p = 0.44). Thus the near-limit selection puts lunar-phase power into the 25 to 38 d range. The stacked periodograms (Figure 2) are dominated by a different effect: the power rises to long periods because a polynomial cannot follow the light-curve shape (baseline misfit). The truncation-only simulation, which has no misfit, gives a flat periodogram and no detections (0 of 1,516 light curves).

### 4.3 Control supernovae pass the periodicity test as often as SESN (Figure 3a)

Two-band detections per object with g and r light curves:

| Rule | SESN | SN Ia (control) | SN II |
| --- | --- | --- | --- |
| v0 cubic | 7/53 (13%) | 6/90 (7%) | 9/255 (4%) |
| v0 + bootstrap FAP < 5e-4 | 4/53 (8%) | 1/90 (1%) | 6/255 (2%) |
| v2 cubic + Moon | 4/53 (8%) | 8/90 (9%) | 8/255 (3%) |
| v4 degree 5 | 5/53 (9%) | 0/90 (0%) | 9/255 (4%) |
| v5 degree 5 + Moon | 1/53 (2%) | 1/90 (1%) | 7/255 (3%) |

Single-band detection fractions are 16% (SESN, 26/160) and 17% (SN Ia, 43/252) under v0 (Fisher p = 0.89). They are also equal under v1, v2, v4 and v5 (Fisher p = 0.21 to 1.0; `files/results/class_summary.csv`). The Horowicz et al. rate, 3/34 (8.8%), is in the range of the SN Ia control (0 to 9% for the different baselines). SNe Ia are not expected to have binary modulation. Their detections come at 22 to 44 d, where the r-band secondary maximum and the cubic baseline misfit put power. Detections in SNe II come at 50 to 90 d, from the plateau drop. The white-noise bootstrap does not remove these false detections, because a misfit residual is correlated in time and the bootstrap destroys this correlation. In 9 of 9 SN II two-band detections the bootstrap FAP is at most 0.1, and in 6 of 9 it is below 5e-4.

The SESN that pass v0 with bootstrap FAP < 5e-4 are SN 2020sgf (Moon, section 4.4), AT 2024afyu (80 d, about T/3, not found at degree 5), SN 2025oq (31 to 34 d; it moves to 45 d with p = 1e-3 at degree 5) and SN 2025mlx (25 to 27 d, only 2.5 cycles in 68 d, Moon-locked with r = -0.86 and -0.67, and not significant with points 1 mag above the limit). Only SN 2022jli is a two-band detection in all of v0, v2, v4 and v5 among the SESN. The other objects that pass in all four variants are SNe II and SLSNe-I with periods of 29 to 90 d (`files/results/dual_sets.json`), which are plateau drops and known SLSN bumps.

Injection tests (`files/results/injection_recovery_summary.csv`) give a single-band recovery of 36 to 65 percent at 0.15 mag and 8 to 38 percent at 0.07 mag for SESN light curves. In SN Ia light curves, the "recovery" of a 0.03 mag signal at 30 d (24 percent) is higher than at 12.5 d (1 percent), because false detections near 30 d are frequent.

### 4.4 The named supernovae (Figure 4, `files/results/named_sne.csv`)

| SN | band | N | r(resid, illum) | v0: P (d), p | v4 degree 5: P, p, r(sin, illum) | v5 degree 5 + Moon: P, p |
| --- | --- | --- | --- | --- | --- | --- |
| 2020sgf | g | 89 | -0.29 (perm. p = 0.005) | 61.1, 1e-10 | 30.0, 2e-8, -0.97 | 61.1, 0.03 |
| 2020sgf | r | 99 | -0.25 (p = 0.017) | 55.8, 2e-9 | 29.4, 3e-9, -0.99 | 64.7, 0.01 |
| 2022esa | g | 34 | -0.38 (p = 0.027) | 32.7, 3e-4 | 34.5, 3e-5, -0.19 | 36.5, 3e-5 |
| 2022esa | r | 34 | -0.22 (p = 0.21) | 34.2, 5e-5 | 36.3, 3e-5, -0.09 | 36.3, 4e-5 |
| 2022jli | g | 95 | -0.20 (p = 0.05) | 12.6, 3e-12 | 12.6, 2e-13, -0.08 | 12.6, 2e-13 |
| 2022jli | r | 86 | -0.18 (p = 0.09) | 12.4, 5e-6 | 12.4, 4e-7, -0.10 | 12.4, 3e-7 |
| 2019tsf | g | 16 | -0.14 (p = 0.61) | 30.0, 0.56 | 15.6, 0.59 | 5.6, 0.59 |
| 2019tsf | r | 20 | +0.02 (p = 0.94) | 56.6, 0.002 | 47.9, 0.009 | 50.4, 0.01 |

- **SN 2020sgf.** The alerts reproduce the published signal. With a degree-5 baseline the period is 30.0 d (g) and 29.4 d (r), the lunar period. The fitted sinusoid is in phase with the Moon (brighter at full Moon, r = -0.97 and -0.99). When one linear Moon term is added, the signal is no longer significant (p = 0.03 and 0.01, threshold 1e-4). In g, 80 percent of the decline points are less than 1 mag above the limit, where section 4.1 predicts a bias of about -0.1 to -0.2 mag per unit illumination. With the cubic baseline, the best periods are 56 to 61 d. These come mainly from one 0.25 mag bump at MJD 59150 (at full Moon, 2020 October 31). The Moon term does not remove that bump. We conclude that the 30-day periodicity of SN 2020sgf is a lunar artefact of near-limit photometry. The single bump can be real.
- **SN 2022esa.** The 33 to 36 d signal stays in all variants (v5 p = 3e-5 and 4e-5). It is not in phase with the Moon (r = -0.19 to +0.03), and its points are 2 to 3 mag above the limit, where the Moon bias is small. A Moon artefact does not explain it. Its period is 22 percent longer than the lunar period, so 3 to 4 cycles cannot fully separate it from a lunar term. The brightness maxima are 5 d before, 5 d before and 5 d after full Moon. It remains a candidate that needs a test with a different survey.
- **SN 2022jli** (positive control). The 12.5 d period is recovered in all variants (p = 1e-12 in g). There is no Moon dependence.
- **SN 2019tsf.** The alerts have too few points (16 and 20). We could not test its 55 d signal.

## 5. Conclusions

1. In ZTF alert photometry of supernovae, a Moon-phase bias exists only near the 5-sigma limit and only when the Moon is up. Its size agrees with a detection-cut simulation. For points more than 1.5 mag above the dark-time limit, any Moon effect is below about 0.01 mag in semi-amplitude.
2. This bias makes lunar-phased 25 to 38 d fits. It explains the 30-day periodicity of SN 2020sgf. One Moon term removes that signal.
3. The cubic-plus-sinusoid rule with a white-noise bootstrap gives two-band "periodic" detections in normal SNe Ia (0 to 9 percent, depending on baseline) at about the rate that Horowicz et al. found in SESN (8.8 percent). With a degree-5 baseline and a Moon term, the SESN rate (1/53) equals the SN Ia rate (1/90). Our data give no evidence for a periodic SESN sub-population beyond SN 2022jli. They also do not exclude one: the recovery of 0.07 mag signals is low (8 to 38 percent).
4. SN 2022jli (12.5 d) is robust. SN 2022esa (34 to 36 d) is not explained by the Moon and remains open.

## 6. Limitations

- We used alert photometry with a 5-sigma cut, not forced photometry. Forced photometry with a lower cut has a smaller, but not zero, truncation bias if points are converted to magnitudes only when the flux is positive or above a S/N cut. We did not test forced photometry or the Lasair data of Horowicz et al.
- The illuminated fraction is a simple Moon model. Moon altitude, Moon-target separation and clouds also change the limit. The linear Moon term cannot remove a non-linear selection effect in all cases.
- Our windows end at 300 d; Horowicz et al. used up to 1000 d. Our sample (53 two-band SESN) differs from theirs (34 dual-band SESN with z <= 0.05). We did not do their population-synthesis comparison.
- The SN Ia control is not a perfect null for r-band shape (secondary maximum), but this is the point: smooth, non-periodic structure gives detections.
- We did not test independent surveys (ATLAS, ASAS-SN, Gaia). An ATLAS check of SN 2022esa is the next step. The ATLAS forced-photometry server needs an account.
- The BTS catalog and the ALeRCE database change with time. The exact light-curve files that we used are identified by SHA-256 in `files/provenance/lightcurve_manifest_sha256.csv`; a later download can differ.

## 7. Files

- `files/code/`: all scripts (`01_fetch_lightcurves.py` to `09_bootstrap_fap.py`, `lcfit.py`) and `run_all.sh`. Python 3.12.16, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas 3.1.1, matplotlib 3.11.2. Downloads go to `./scratch`, never into this bundle.
- `files/results/moon_slopes.csv`: Moon slopes by class, dark-time margin and Moon altitude, with the truncation-simulation prediction.
- `files/results/periodicity_per_lightcurve.csv`: best period, p-value, amplitude, minimal detectable amplitude, minimum p at 25-38 d, Moon correlation, for each light curve and variant (ZTF ID, band, BTS type). No photometry.
- `files/results/class_summary.csv`, `bootstrap_fap.csv`, `dual_sets.json`, `injection_recovery_summary.csv`, `named_sne.csv`.
- `files/figures/`: Figures 1 to 4.
- `files/provenance/`: SHA-256 of the BTS catalog file, the sample list and every light-curve file that we used.
- `files/NOTICE.md`: attribution and terms of the external data.

Reproduce: `bash files/code/run_all.sh` in an empty folder (about 1 h of download at 2 parallel requests, then about 30 min of computation on 2 CPUs).

## 8. What remains open

- Test SN 2022esa and the four other bootstrap-passing SESN with ATLAS forced photometry (o and c bands) and with ZTF forced photometry.
- Repeat the population test with ZTF forced photometry, with a flux-space model and no S/N cut, which removes the truncation bias.
- Use a non-periodic control class (SNe Ia, SNe II) and a red-noise (block) bootstrap for every future periodic-SN search.
