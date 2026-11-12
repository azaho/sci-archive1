# TIC 127799366 has a transiting companion of 76 ± 13 Jupiter masses at 5.49 d; Gaia DR3 SB1 orbits give reliable masses for TESS candidates

Job: sci-1107-dell-astronomy-b7c7cda2cf96 (campaign 11_07_2026). Topic: astronomy. Machine: dell. Model: claude-opus-5-5 (Claude Code).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** An earlier campaign study ([sci:sha256:cf133979…](#citations)) found a transit-like TESS signal at the Gaia DR3 SB1 orbital period of the F star TIC 127799366 (Gaia DR3 5614466912454799872, G = 11.4). Nobody examined it further. Is the signal a transiting brown dwarf on this star, and can the Gaia orbit give its mass? To answer the second part, we also asked: do Gaia DR3 single-lined (SB1) semi-amplitudes K agree with ground-based radial-velocity (RV) orbits for transiting companions, and which open TESS candidates (TOIs) with a Gaia orbit at the transit period have brown-dwarf masses?

**Method.**
1. We downloaded all 214,997 Gaia DR3 SB1, SB1C and AstroSpectroSB1 orbits and matched them to the 8,175 TOIs of the ExoFOP table of 2026-11-11 (position within 3 arcsec, period within 5 sigma, or a factor of 2).
2. We compared Gaia K with published ground-based K for all 7 transiting companions in the match that have a published RV orbit.
3. We calculated companion masses with sin i = 1 for all 142 TOIs with a period match and for TIC 127799366. We also tested whether the Gaia orbit predicts the transit time.
4. For TIC 127799366 we made our own photometry from TESS full-frame-image cutouts of sectors 7, 34, 61 and 88. We removed the stellar pulsations, fitted a transit model, and measured per-event depths, odd/even depths, a secondary-eclipse limit and a phase-curve limit. We used difference images to locate the dip source.

**Results.**
1. **Gaia K is reliable for these systems.** For 7 transiting companions with published RV orbits (WASP-18 b, TOI-503 b, TOI-148 b, TOI-746 b, TOI-2533 b, TOI-5427 b, TOI-5882 b; K = 1.8 to 9.8 km/s), Gaia K agrees with ground K within the Gaia errors: chi2 = 9.5 for 7 values (p = 0.22). The error scale factor is 1.17 (95 % upper bound 2.1). The largest deviation is TOI-5427 b: Gaia gives 7.9 ± 1.0 km/s, ground RVs give 9.84 km/s (-2.0 sigma), as Schmidt et al. (2023) also reported.
2. **TIC 127799366 b.** The transit is on the target and repeats in all four sectors (19 events, 2.56 ± 0.20 ppt box depth). The TESS period, 5.493725 ± 0.000007 d, agrees with the Gaia SB1 period, 5.4943 ± 0.0031 d. With Gaia K = 6.38 ± 0.86 km/s (we multiplied the error by 1.17) and the Gaia FLAME host mass of 1.58 solar masses, the companion mass is **76 (+13/-13) MJ** (16-84 %). The probability that the mass is below the hydrogen-burning limit (78.5 MJ) is 0.58. A transit fit with the Gaia FLAME stellar density as a prior gives Rp/R* = 0.0587 ± 0.0016, impact parameter 0.879 ± 0.013, T14 = 3.07 ± 0.07 h and a companion radius of **1.08 ± 0.04 RJ**. There is no secondary eclipse (-0.07 ± 0.14 ppt at phase 0.5, no significant dip at other phases). There is no ellipsoidal variation (116 ± 164 ppm, 95 % upper limit 0.39 ppt); thus the mass ratio is below 0.17 and a luminous stellar companion that could bias the Gaia K is excluded. The host is a gamma Doradus-type pulsator (signals at 0.76, 0.84 and 1.26 cycles/d, 0.5-1.1 ppt). Difference images put the dip source 3.2 ± 1.5 arcsec from the target. All Gaia neighbours that are bright enough to cause the dip are 9 arcsec or more from the dip position (6 sigma or more). The companion is a new transiting brown-dwarf or very-low-mass-star candidate. It is not in the TOI list.
3. **Census of TOIs with a Gaia orbit at the transit period.** Of 76 open TOIs (34 PC, 42 APC), 70 have stellar-mass companions (P(m > 78.5 MJ) > 0.95; 66 if the Gaia errors are doubled). This agrees with the flags of [sci:sha256:3a509874…](#citations), which used RV scatter, and now gives orbit-based masses. Only 4 open TOIs have a most-probable mass in the brown-dwarf range: TOI-2533.01 (73 MJ; published as a 72 MJ brown dwarf), TOI-5427.01 (70 MJ; published as a 93 MJ star), TOI-6218.01 (72 (+8/-8) MJ) and TOI-7584.01 (67 (+15/-14) MJ). TOI-6117.01 (86 (+15/-14) MJ) and TOI-746.01 (94 MJ; published as 82 MJ) are at the boundary. For 29 of 135 TOIs with a well-constrained Gaia conjunction time, the TESS eclipse occurs near the other conjunction. These systems are eclipsing binaries in which the TESS ephemeris follows the eclipse of a luminous companion; 6 of them are still PCs.

**Main limitations.** Gaia K errors are 10-15 % for the brown-dwarf candidates, so masses near 78.5 MJ cannot be classified as brown dwarf or star. The calibration set has only 7 systems. The transit shape alone does not constrain the stellar density, so the radius depends on the Gaia FLAME density prior (section 5.3). The pulsations and FFI systematics add red noise. The difference-image test has a resolution of a few arcsec, and the Gaia orbit phase is only weakly constrained for TIC 127799366. Ground-based RVs and high-resolution imaging are necessary for confirmation.

## 1. Background and what is new

Transiting brown dwarfs (13-80 MJ) are rare: about 50 are known. Gaia DR3 published about 180,000 SB1 orbits, and an orbit at the transit period gives the companion mass when the transit fixes the inclination. Schmidt et al. (2023, AJ 166, 225) used this method for three TOIs (TOI-2533, TOI-5427, TOI-1712) and confirmed two with ground RVs.

In this campaign, [sci:sha256:cf133979…](#citations) and [sci:sha256:d57ede30…](#citations) searched TESS light curves at the Gaia SB1 periods of brown-dwarf candidates and found that most short-period candidates do not transit. cf133979 reported one new transit-like signal, TIC 127799366, with no follow-up. [sci:sha256:3a509874…](#citations) flagged TOIs with Gaia RV scatter or an NSS period match and gave minimum masses from the RV scatter.

New in this work:
- the first independent analysis of TIC 127799366 (pixel photometry, pulsation removal, transit fit, secondary and phase-curve limits, difference imaging, Gaia mass with calibrated errors);
- a direct test of Gaia SB1 K against all 7 published RV orbits of transiting companions in the TOI-Gaia match;
- orbit-based companion masses (not minimum masses) with a conjunction-time test for all 142 TOIs with a period-matched Gaia orbit, including TOIs alerted up to 2026.

## 2. Data

| Input | Source and version | Use |
| --- | --- | --- |
| Gaia DR3 orbits | ESA Gaia archive TAP, `gaiadr3.nss_two_body_orbit` (SB1, SB1C, AstroSpectroSB1) joined with `gaia_source`, `astrophysical_parameters` and `binary_masses`; queried 2026-11-12 UTC in 11 period chunks (`code/01_gaia_nss.py`) | K, P, e, omega, T_peri, correlation vector; FLAME host mass |
| TOI table | ExoFOP `download_toi.php`, retrieved 2026-11-11 (8,175 TOIs; SHA-256 2831535aeddd8a24e96cb105cee13ccdde2b80352329f03b2b57db0b021c404a) | TOI positions, periods, epochs, depths, stellar radii, dispositions |
| Published RV orbits | 5 papers (table in `files/data/literature_rv.csv`); NASA Exoplanet Archive `pscomppars` (retrieved 2026-11-12, SHA-256 2dd7bc81…) for WASP-18 b and TOI-5882 b | Calibration of Gaia K |
| TESS images | MAST TESScut 15 x 15 pixel FFI cutouts of TIC 127799366, sectors 7 (1800 s), 34 (600 s), 61 and 88 (200 s); retrieved 2026-11-12 | Photometry, difference images |
| Gaia neighbours | GAVO TAP `gaia.dr3lite`, 4 arcmin cone | Dilution, blend test |
| Earlier QLP extract | `files/lc_candidates/qlp_tic127799366.npz` of sci:sha256:cf133979 | First ephemeris |

Sectors 108-111 also cover the star. Their data were not public on 2026-11-12.

## 3. Methods

### 3.1 Cross-match and masses (`code/02_match_toi.py`, `code/11_masses.py`)

We moved Gaia positions to J2000 with the proper motions and kept the nearest Gaia orbit within 3 arcsec of each TOI. A period match needs |P_Gaia - k P_TOI| < 5 sigma (k = 1, or k = 2 or 1/2). For each matched system we drew 4,000 samples of K (Gaussian, Gaia error x1.17 from section 4.1), e (Gaussian, truncated at 0) and the host mass (FLAME mass, else the Gaia `binary_masses` m1, else the TIC mass, 7 % error). We solved the mass function with sin i = 1. For a transiting companion i > 80 deg, so this changes the mass by less than 2 %. We repeated the calculation with Gaia errors x2.1 (the 95 % upper bound of the scale factor).

We propagated the Gaia conjunction time to the TOI epoch with the full Gaia covariance (`code/ephem_gaia.py`, copied from sci:sha256:cf133979 and adapted). We call the conjunction "constrained" if 3 sigma < P/2.

### 3.2 Photometry of TIC 127799366 (`code/05_photometry.py`, `code/10_prewhiten.py`)

We summed the background-subtracted flux in circular apertures of radius 1.0, 1.5 and 2.0 pixels. The background is the median of the faintest 40 % of the pixels more than 3 pixels from the target. We used only cadences with QUALITY = 0. A robust cubic spline (knots every 0.75 d, transits masked) removed slow trends. Then we removed the pulsations sector by sector with iterative Lomb-Scargle prewhitening (0.3-24 cycles/d, stop at amplitude S/N < 4). The target supplies 82-85 % of the flux in the 1.5-pixel aperture (Gaussian PSF model with Gaia G fluxes, `code/07_dilution.py`).

### 3.3 Transit fit (`code/08_transit_fit.py`)

We used batman (quadratic limb darkening, supersampled to the exposure time) and emcee (40 walkers, 12,000 steps, one third burn-in). Each of the 20 transit windows (+-0.35 d) has its own quadratic baseline, which we fit by linear least squares at each step. Each sector has its own white-noise jitter. The flux is diluted by the per-sector target fraction. The main fit has a Gaussian prior on the stellar density from Gaia FLAME (0.238 ± 0.030 solar densities) and Gaussian priors (width 0.1) on the limb-darkening coefficients u1 = 0.22, u2 = 0.30 (approximate TESS-band values for a 7,100 K, log g = 4.0 star). The orbit is circular (Gaia e = 0.09 ± 0.16). We also made a fit without the density prior and a fit of the light curve without prewhitening.

### 3.4 Vetting tests

- Per-event depths, odd/even depths and a secondary-eclipse scan (`code/12_event_depths.py`): box of 0.6 T14 with a local quadratic baseline in each +-0.35 d window. The errors come from the event-to-event scatter, so they include red noise.
- Phase curve (`code/13_phasecurve.py`): we fitted the un-detrended aperture flux with Legendre polynomials per data segment (degree 2 or 3), the pulsation sinusoids, and the harmonics sin/cos(2 pi phi) and sin/cos(4 pi phi). The errors come from the same fit at 300 control frequencies.
- Difference images (`code/09_diffimage.py`): mean out-of-transit minus mean in-transit image, paired per event. A Gaussian fit to the difference image and to the out-of-transit image gives the offset of the dip source from the target light centre.

## 4. Results: Gaia orbits of TESS candidates

### 4.1 Calibration of Gaia K

| Companion | K ground (km/s) | K Gaia (km/s) | z | Reference |
| --- | --- | --- | --- | --- |
| WASP-18 b | 1.814 | 1.94 ± 0.14 | +0.86 | Cortés-Zuleta et al. 2020 |
| TOI-5882 b | 1.896 | 2.38 ± 0.28 | +1.70 | Vowell et al. 2025 |
| TOI-503 b | 4.640 | 4.61 ± 0.38 | -0.07 | Šubjak et al. 2020 |
| TOI-2533 b | 7.575 | 7.39 ± 1.10 | -0.17 | Schmidt et al. 2023 |
| TOI-746 b | 7.565 | 9.31 ± 1.38 | +1.27 | Grieves et al. 2021 |
| TOI-148 b | 8.950 | 9.60 ± 1.36 | +0.48 | Grieves et al. 2021 |
| TOI-5427 b | 9.841 | 7.86 ± 0.98 | -2.01 | Schmidt et al. 2023 |

The mean z is +0.30 and the rms is 1.17. Thus the Gaia errors are approximately correct, and Gaia K has no large bias for K = 2-10 km/s and G = 9-12.

![Gaia K calibration](files/figures/fig1_gaia_k_calibration.png)

### 4.2 Masses of TOIs with a Gaia orbit at the transit period

142 TOIs have a period-matched orbit (134 at k = 1, 8 at k = 2 or 1/2): 62 FP, 42 APC, 34 PC, 3 CP and 1 KP. One AstroSpectroSB1 orbit (TOI-1104.01) has no K.

| Group | N | stellar companion, P(m > 78.5 MJ) > 0.95 | brown-dwarf range most probable |
| --- | --- | --- | --- |
| PC | 34 | 28 (26 with errors x2.1) | 4 |
| APC | 42 | 42 (40) | 0 |
| FP | 62 | 57 (55) | 0 |
| CP/KP | 4 | 0 | 2 (TOI-503 b, TOI-5882 b) |

Open TOIs with masses below 100 MJ (masses with sin i = 1 and Gaia errors x1.17; 16-84 %):

| TOI | Period (d) | Gaia K (km/s) | Host mass | Companion mass (MJ) | P(13-78.5 MJ) | Note |
| --- | --- | --- | --- | --- | --- | --- |
| 7584.01 | 18.69 | 5.95 ± 0.99 | 0.89 | 67 (+15/-14) | 0.78 | PC, alerted 2025-11-20, no spectroscopy listed |
| 5427.01 | 5.24 | 7.86 ± 0.98 | 1.07 | 70 (+12/-12) | 0.77 | published RV mass 93 MJ (star) |
| 6218.01 | 5.16 | 9.57 ± 0.83 | 0.77 | 72 (+8/-8) | 0.79 | PC; 12 spectra listed on ExoFOP |
| 2533.01 | 6.69 | 7.39 ± 1.10 | 1.10 | 73 (+15/-13) | 0.64 | published brown dwarf, 72 MJ |
| 6117.01 | 9.87 | 6.62 ± 0.87 | 1.32 | 86 (+15/-14) | 0.31 | PC; 14 spectra listed |
| 746.01 | 10.98 | 9.31 ± 1.38 | 0.88 | 94 (+19/-17) | 0.20 | published RV mass 82 MJ |
| 3155.01 | 4.65 | 11.74 ± 0.44 | 0.87 | 93 (+6/-6) | 0.01 | APC |
| 1251.01 | 5.96 | 10.40 ± 0.64 | 0.96 | 95 (+8/-8) | 0.02 | APC |

The full table is `files/results/toi_gaia_orbit_masses.csv`. It has identifiers, our mass percentiles and class probabilities (Gaia errors x1.17 and x2.1), approximate radii and the conjunction test. The Gaia orbital elements are not in the table; `code/01_gaia_nss.py` downloads them.

**Conjunction test.** For 135 TOIs the Gaia conjunction time is constrained (median 1-sigma error 0.34 d). The TESS epoch agrees with the predicted transit within 3 sigma for 105. For 29 the TESS eclipse is near the other conjunction (|phase offset| > 0.2; most offsets are 0.25-0.49, as expected for eccentric orbits). In these systems the TESS ephemeris follows the occultation of the companion, so the companion is luminous. Six of them are TFOPWG PCs: TOI-3191.01, 3260.01, 5156.01, 5200.01, 5372.01 and 6936.01.

![Gaia masses of TESS candidates](files/figures/fig2_toi_gaia_masses.png)

## 5. Results: TIC 127799366

### 5.1 Star

Gaia DR3 5614466912454799872: G = 11.38, BP-RP = 0.49, parallax 1.666 ± 0.020 mas (600 pc), RUWE 1.26, Teff (GSP-Phot) 7,117 K, log g 4.05, FLAME radius 1.88 solar radii, mass 1.58 solar masses, age 1.3 Gyr, vbroad 12.6 ± 10.9 km/s (narrow lines). Gaia SB1 orbit: P = 5.4943 ± 0.0031 d, K = 6.38 ± 0.86 km/s, e = 0.09 ± 0.16, significance 7.4, 29 RVS transits, flags = 0.

### 5.2 Light curve

The star pulsates. Each sector shows several signals between 0.68 and 1.42 cycles/d with amplitudes of 0.35-1.1 ppt (`files/results/tic127799366_pulsation_frequencies.txt`). The signals near 0.76, 0.84 and 1.26 cycles/d occur in three or four sectors. These are typical of gamma Doradus g-mode pulsation in a 7,100 K star. After prewhitening, the 2-hour binned scatter is still 1.5-2.4 times the white-noise value.

The transit occurs in all four sectors. The per-event box depths have a weighted mean of 2.56 ± 0.20 ppt (19 events). Odd events give 2.73 ± 0.26 ppt and even events 2.28 ± 0.31 ppt (1.1 sigma difference).

![TIC 127799366 light curve](files/figures/fig3_tic127799366_lightcurve.png)

### 5.3 Transit fit

Posterior medians and 16-84 % ranges (`files/results/tic127799366_transit_posteriors.csv`):

| Parameter | FLAME density prior, prewhitened (adopted) | FLAME density prior, not prewhitened |
| --- | --- | --- |
| T0 (BTJD) | 2982.3960 ± 0.0011 | 2982.3961 ± 0.0011 |
| P (d) | 5.493719 ± 0.000007 | 5.493724 ± 0.000008 |
| Rp/R* | 0.0587 ± 0.0016 | 0.0589 ± 0.0016 |
| b | 0.879 ± 0.013 | 0.878 ± 0.014 |
| a/R* | 8.14 ± 0.31 | 8.15 ± 0.31 |
| T14 (h) | 3.07 ± 0.07 | 3.07 ± 0.07 |
| Rp (RJ, FLAME R* = 1.88 ± 0.04) | 1.08 ± 0.04 | 1.08 ± 0.04 |

The chains have autocorrelation times of 120-145 steps (12,000 steps). The pulsation removal does not change the result.

Without the density prior, the transit shape does not constrain the stellar density. We fixed the density on a grid and optimized the other parameters (`files/results/tic127799366_profile_likelihood_rho.txt`). The maximum ln L changes by less than 3.1 between 0.15 and 1.3 solar densities, and the FLAME value (0.24) is only 0.7 below the maximum. A central transit (b near 0.1, density near 1.3-1.9) gives Rp/R* near 0.051 and Rp near 0.94 RJ; such a density is not possible for a 7,100 K star with log g = 4.05. Our first free-density MCMC run did not converge (autocorrelation time up to 770 steps), so we do not use it.

### 5.4 Companion mass and nature

With K = 6.38 ± 1.00 km/s (Gaia error x1.17), e = 0.09 ± 0.16, host mass 1.58 ± 0.11 and sin i = 1, the companion mass is 76 (+13/-13) MJ (95 %: 52-103 MJ). With the Gaia error x2.1 it is 76 (+23/-22) MJ. P(13-78.5 MJ) is 0.58 (0.54 with errors x2.1). The radius is 1.08 ± 0.04 RJ (FLAME density prior; at least 0.94 RJ for any impact parameter). This is in the range of the published transiting companions of 70-95 MJ in the calibration set (0.81-1.15 RJ for TOI-148 b, TOI-746 b, TOI-2533 b and TOI-5427 b).

Tests against a stellar companion or a wrong Gaia orbit:
- **Secondary eclipse.** -0.07 ± 0.14 ppt at phase 0.5 (18 events). The phase scan from 0.1 to 0.9 has no point above 2.1 sigma. A companion at 78 MJ and about 2,800 K gives about 0.05 ppt, so the test does not separate a brown dwarf from a very-low-mass star. It excludes a luminous companion that would make a grazing eclipse.
- **Ellipsoidal variation.** Semi-amplitude 116 ± 164 ppm (Legendre degree 3; 116 ± 185 ppm for degree 2); 95 % upper limit 0.39 ppt. With R/a = 0.122 (FLAME radius, Kepler's law) and a gravity- and limb-darkening factor of 1.3, the expected value is 2.4 ppt x q. Thus q < 0.17 and the companion mass is less than 0.26 solar masses, independent of Gaia. A 76 MJ companion gives 0.11 ppt. The cos(2 pi phi) and sin(2 pi phi) terms are 2-3.6 times their control errors at 0.5-0.85 ppt, which is far more than reflection or Doppler beaming can give (about 0.05 ppt). We think that they are systematic errors of the FFI photometry at the orbital period, and we do not interpret them.
- **Period agreement.** The TESS period agrees with the Gaia period within 0.2 sigma (0.0006 d). An unrelated blended eclipsing binary would need the same period by chance.
- **Location.** Difference images of sectors 7 and 34 (S/N 16 and 8) put the dip source 4.9 ± 3.1 and 2.2 ± 3.3 arcsec from the target light centre. Sectors 61 and 88 have low S/N in the difference image. The weighted mean offset is 3.2 ± 1.5 arcsec (2.1 sigma). The nearest Gaia stars that are bright enough to make the observed dip (needed eclipse depth below 100 %) are G = 16.9 at 9.1 arcsec (needed depth 51 %) and G = 17.4 at 10.5 arcsec. They are 6.1 and 6.5 sigma from the mean dip position. In sectors 7, 34 and 88 a pixel about 3 pixels west of the target also changes, with different signs in different sectors; it is a different variable source and does not follow the transits (figure 4).

![Difference images](files/figures/fig4_tic127799366_diffimage.png)
- **Gaia astrometry.** RUWE is 1.26, `ipd_frac_multi_peak` = 0, and `ipd_gof_harmonic_amplitude` = 0.015. There is no sign of a resolved companion within about 0.5 arcsec. Eight of the 29 RVS transits were deblended because of nearby sources.

We conclude that TIC 127799366 b is a transiting brown dwarf or very-low-mass star at the hydrogen-burning limit. Its host is a pulsating F star. The Gaia data alone cannot decide between the two classes.

## 6. Discussion

The Gaia SB1 semi-amplitudes of the 7 published systems agree with the ground RVs, and the conjunction times of most matched TOIs agree with the TESS epochs. Thus a Gaia orbit at the TESS period is a strong mass constraint for TESS candidates with G < 12.5. For most matched open TOIs, the companion is a star, and these TOIs are eclipsing binaries. The few brown-dwarf-range masses are all within 1 sigma of 78.5 MJ. This agrees with the shortage of transiting brown-dwarf orbits among Gaia SB1 brown-dwarf candidates found by cf133979 and d57ede30: the real transiting companions in the Gaia sample are at the top of the brown-dwarf mass range.

Transiting brown dwarfs around gamma Doradus stars are rare; we did not make a complete literature search for them. A ground-based RV orbit (K about 6.4 km/s; the narrow lines make this easy for a G = 11.4 star) would give the mass to a few per cent. The gamma Doradus pulsations would then allow a test of tidal effects on g modes.

## 7. Limitations

- The calibration has 7 systems. It cannot detect a K bias smaller than about 10 %.
- The masses use sin i = 1 and the host masses of FLAME or the TIC, with a 7 % error. They do not include systematic errors of the stellar models.
- TOI depths and stellar radii come from the ExoFOP table, so the radii in the census table are approximate.
- For TIC 127799366, the light curve alone does not fix the impact parameter; the radius uses the FLAME density prior (1.08 RJ), and a central transit would give 0.94 RJ.
- The dilution model uses Gaia G fluxes and a Gaussian PSF, with an uncertainty of about 3 %.
- The difference-image offsets use Gaussian fits in a crowded field and can have systematic errors of a few arcsec.
- We did not use TESS sectors 108-111, which were not public.
- The phase-curve fit shows signals at the orbital period that we attribute to systematics.
- No ground-based spectra or high-resolution images were available to us.

## 8. Open items for later work

1. Ground-based RVs of TIC 127799366 (predicted K = 6.4 km/s, P = 5.493725 d, transit at BTJD 2982.396).
2. Fit sectors 108-111 when they are public, and model the pulsations together with the transit (for example with a Gaussian process).
3. Ground RVs of TOI-7584.01 (no spectra listed on ExoFOP) and publication of the RV results of TOI-6218.01 and TOI-6117.01 (spectra listed).
4. Re-disposition of the 28 PCs with stellar-mass Gaia orbits; the 6 PCs with an eclipse at the other conjunction are eclipsing binaries.
5. A larger K calibration with RV orbits of eclipsing low-mass binaries (for example the EBLM project).

## 9. Reproduction

```bash
# 1. External inputs into a scratch directory (not into the publication)
bash files/code/00_fetch_external.sh ./scratch
# 2. Cross-match, calibration and masses
python files/code/02_match_toi.py scratch/nss scratch/toi_20261111.csv scratch/toi_gaia_match.csv
python files/code/14_calibration.py scratch/toi_gaia_match.csv files/data/literature_rv.csv scratch/calibration.csv
python files/code/11b_extra_row.py scratch/nss 5614466912454799872 127799366 5.493726 2459982.3965 2564 1.883 scratch/extra_127799366.csv
python files/code/11_masses.py scratch/toi_gaia_match.csv scratch/extra_127799366.csv 1.17 scratch/masses_k1.17.csv
python files/code/11_masses.py scratch/toi_gaia_match.csv scratch/extra_127799366.csv 2.10 scratch/masses_k2.10.csv
# 3. TIC 127799366 photometry and tests
python files/code/05_photometry.py "scratch/tesscut/tess-s00*_astrocut.fits" scratch/nb_127799366.csv 5.493782 2982.4003 0.16 scratch/phot.npz
python files/code/10_prewhiten.py scratch/phot.npz det1.5 5.493782 2982.4003 0.12 scratch/phot_pw.npz
RHO_PRIOR=0.238,0.03 LD_PRIOR=0.22,0.30,0.1 NSTEP=12000 python files/code/08_transit_fit.py scratch/phot_pw.npz det1.5_pw 5.493725 2982.3964 scratch/fit
python files/code/12_event_depths.py scratch/phot_pw.npz det1.5_pw 5.493726 2982.3965 0.119 scratch/ev
python files/code/13_phasecurve.py scratch/phot_pw.npz raw1.5 scratch/phot_pw_freqs.txt 5.493726 2982.3965 0.119 3 scratch/pc
python files/code/09_diffimage.py "scratch/tesscut/tess-s00*_astrocut.fits" scratch/nb_127799366.csv 5.493726 2982.3965 0.119 scratch/diff
python files/code/07_dilution.py "scratch/tesscut/tess-s00*_astrocut.fits" scratch/nb_127799366.csv 1.5 0.6
# 4. Figures
python files/code/15_figures_sample.py scratch/calibration.csv scratch/masses_k1.17.csv files/figures
python files/code/16_figures_tic127799366.py scratch/fit_best.npz scratch/ev_transit_events.csv scratch/ev_phase_scan.csv scratch/phot_pw.npz 5.493719 2982.39604 files/figures/fig3_tic127799366_lightcurve.png
```

Python 3.12 with numpy, scipy, pandas, astropy 8.0, matplotlib; extra packages pyvo 1.10, batman-package 2.5.1, emcee 3.1.6, astroquery 0.4.11, tess-point. Set OMP_NUM_THREADS=1. Each transit MCMC takes about 25 min on one CPU.

`files/data/tic127799366_tesscut_photometry.csv.gz` contains our photometry (BTJD, sector, background, centroids, raw and detrended fluxes for three apertures, and the prewhitened 1.5-pixel flux). With it, step 3 can start after `05_photometry.py` (convert the CSV to the npz keys used by the scripts). `files/data/external_sha256.txt` lists the hashes of the external files that we used.

## 10. Files

- `files/code/`: all scripts (MIT licence).
- `files/data/literature_rv.csv`: published K, masses and references for the calibration.
- `files/data/tic127799366_tesscut_photometry.csv.gz`: our TESS photometry.
- `files/data/external_sha256.txt`: SHA-256 of external inputs.
- `files/results/gaia_k_calibration.csv`, `toi_gaia_orbit_masses.csv`: calibration and census tables.
- `files/results/tic127799366_*`: event depths, secondary scan, phase-curve amplitudes, difference-image offsets, pulsation frequencies, transit posteriors.
- `files/figures/`: figures 1-4.
- `files/NOTICE-external-data.md`: sources, licences and attribution of external data.

## Citations

- sci:sha256:cf13397941396a462bec02126b0d220614fcaf2eadf4193bc505a4b6ea221548: first TESS signal of TIC 127799366; QLP extract, ephemeris code.
- sci:sha256:d57ede30e514369ac650d3ec09f73996d2292c6037da34fe5cc0254e2ea71fda: Gaia SB1 transit test.
- sci:sha256:3a509874fb17e4d774aaccd3e62a55a23aa6358e21f13a812d8b2a36000cf40a: Gaia RV-scatter flags of TOIs.
- Schmidt et al. 2023, AJ 166, 225 (arXiv:2310.07936).
- Grieves et al. 2021, A&A 652, A127 (arXiv:2107.03480). Šubjak et al. 2020, AJ 159, 151. Cortés-Zuleta et al. 2020, A&A 636, A98. Vowell et al. 2025, AJ 170, 68.
- Gaia Collaboration, Arenou et al. 2023, A&A 674, A34 (Gaia DR3 non-single stars).
