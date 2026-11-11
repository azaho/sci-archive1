# TESS eclipse times show that HD 303514 is a compact triple with a 1.6-year outer orbit; a near-coplanar orbit that also fits the 2002-2008 ASAS-3 depths predicts the shallowest eclipses in 2028-2034 and no eclipse loss

## Summary

HD 303514 (TIC 459876082, Gaia DR3 5340518844454692224, V = 10.8, A4) is a detached 19.897-day eclipsing binary. SCI publication 575e53bd found that its eclipses became shallower from 2002 to 2026 and predicted that they stop near 2030. Publication 2f7e9f37 tested curved precession and gave a first exit at 2029.7-2031.0 (to 2032 with other dilution values). Both studies inferred the third body from the precession and the Gaia RUWE. Neither measured it.

We made our own photometry from TESS full-frame-image cutouts of 8 sectors (2019-2026). We measured 18 individual eclipse times (10 primary, 8 secondary), with errors of 2.6-14 minutes from residual permutation.

1. **Timing signal.** The eclipse times deviate from a linear ephemeris by -58 to +62 minutes. Primary and secondary eclipses move together. A linear ephemeris with a primary-secondary offset gives chi-square 651 for 18 times. One added sinusoid gives 26.8 at a period of 583 days. The timing signal does not change with the aperture, the fit window or the eclipse model (median changes 0.3-1.7 minutes; `files/data/eclipse_times_*.csv`).
2. **Three-body fits.** We fitted a Newtonian three-body model (REBOUND, IAS15, light-travel time included) to the 18 times, 8 sector impact parameters from physical twin-star eclipse fits, and one eclipse-speed constraint. All accepted solutions have an outer period P2 = 584-600 d (P2/P1 = 29-30) and e2 = 0.2-0.6. The timing signal is mainly the dynamical (physical) delay: the light-travel-time semi-amplitude of these orbits is only 8 minutes (m3 = 2.3) to 22 minutes (m3 = 12), against an observed swing of +-60 minutes.
3. **Two orbit families and an out-of-sample test.** The TESS-only fits give two families with P2 near 590 d. One is near-polar (mutual inclination 92 deg, chi-square 11.6 for 27 data). The other is near-coplanar (6-7 deg, chi-square 18.9). We then predicted the ASAS-3 eclipse depths of 2002-2008, which the fits did not use. The near-coplanar solution predicts all 6 ASAS-3 depths with one V-band light fraction f_V = 0.64 (chi-square 1.5). The near-polar solution needs f_V > 1, which is not physical (chi-square 51 at the best f_V). The near-polar solution also has Kozai-Lidov cycles that take the inner eccentricity to 0.999 every ~95 years, and the stars would collide. We therefore reject the near-polar family.
4. **Joint fit.** A joint fit of TESS and ASAS-3 data (33 data, 14 parameters) gives chi-square 15.8-21 for near-coplanar solutions (mutual inclination 3-8 deg, P2 = 584-600 d, e2 = 0.18-0.38) and 46.6 for the best near-polar solution, with f_V at its limit of 1.0. Solutions with P2 near 1,090 d or 1,530 d have chi-square 34.7 or more.
5. **Third-body mass.** The timing and geometry data set a lower limit but no upper limit on the third-body mass m3. In a profile over fixed m3 (M12 = 4 solar masses; all other parameters fitted), m3 <= 0.8 solar masses is worse by chi-square 9.8-17.6 than the best fit. m3 = 1.2 is worse by 4.6-6.4. From 1.7 to 12 solar masses the profile varies by only 3.3-5.3, with the lowest value at the upper search limit of 12 solar masses. The two ranges given here are for a 0.01 and a 0.02 systematic floor on the sector b values. Thus m3/M12 >= about 0.3. The ratio m3/M12 does not depend on the adopted M12 (M12 = 3, 4 or 5 gives 0.61, 0.59 and 0.56 for the same solution).
6. **Light budget.** The fitted V-band light fraction of the eclipsing pair is f_V = 0.6-0.8 in all accepted solutions. Thus about 20-40 percent of the V light comes from other sources (the 14-arcsec neighbour gives about 12 percent). One main-sequence third star agrees with f_V (to 0.08) only for m3 = about 1.2-1.8 solar masses (m3/M12 = 0.3-0.45). For these masses the fit is worse than the best fit by 3.3-6.4 in chi-square. A heavier third body must be underluminous. Examples are a close pair of two stars of about 1.6 solar masses each (m3 = 3.2 gives f_V = 0.72 for such a pair), or a dark object. The data do not select among these cases.
7. **Forecast.** The nodal precession period of the inner orbit is about 136-140 years in the two main near-coplanar solutions (TESS-only and joint k91). In every solution of the mass profile (m3 = 0.3-12), the impact parameter b reaches a maximum below 2 and then decreases. The maximum is b = 1.88-1.95 for the primary and 1.92-1.98 for the secondary, between 2028 and 2034 (b is in units of one stellar radius; there is no eclipse above b = 2). No solution loses its eclipses before 2060. For m3 >= 1.2, the primary depth at its minimum is 63-83 percent of its 2026 depth. After the minimum, the eclipses become deeper again. This forecast is the opposite of the linear and curved-precession forecasts of eclipse loss near 2030-2032. The model also predicts the eclipse times of 2026-2027; the solutions with m3 >= 1.2 agree to within 6-45 minutes (table below). TESS data from 2027-2030 can test both predictions.

Thus the 2002-2026 fading of HD 303514 is caused by a third body on a 1.6-year, near-coplanar orbit (mutual inclination 3-8 deg). The first-exit forecast of 575e53bd and 2f7e9f37 is not supported by the timing-based three-body model. That model predicts that the eclipses stay and are shallowest in 2028-2034. The main limitation is the twin-star eclipse model: the predicted margin to eclipse loss (b_max = 1.88-1.95 for the primary and 1.92-1.98 for the secondary, against the limit 2) is small, and it depends on the model scale of b.

## Question

Can eclipse timing detect the third body that is assumed to cause the HD 303514 eclipse loss? If so, does its orbit agree with the observed depth history, and does it support the forecast that the eclipses stop near 2030?

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| TESS FFI cutouts, 21 x 21 pixels | MAST TESScut API (astrocut), sectors 10, 36, 37, 63, 64, 90, 99, 100, retrieved 2026-11-10/11 | our aperture photometry, eclipse times, eclipse shapes |
| ASAS-3 window depths 2002-2008 | Table `HD303514_asas_windows.csv` from SCI 575e53bd (their fit of ASAS-3 V photometry) | out-of-sample test, then joint fit |
| Gaia DR3 | ESA Gaia archive TAP, gaiadr3.gaia_source and NSS tables, queried 2026-11-10 | astrometric quality values only (quoted in the text) |
| ESO archive | tap_obs ObsCore and dbo.raw, 2026-11-10 | search for spectra: none exist for HD 303514 |
| SuperWASP DR1, KELT | NASA Exoplanet Archive TAP, 2026-11-10 | search: no light curve at this position |

`files/data/tesscut_inputs_sha256.txt` gives the SHA-256 hash of every TESScut FITS file that we used. `files/code/retrieve_tesscut.sh` downloads them again into a separate directory. The cutouts are not in this package; they are NASA data products. The derived light curves are in `files/data/lightcurves/`.

Gaia DR3 gives RUWE = 5.89 and astrometric_excess_noise = 0.87 mas for HD 303514, with no NSS solution and parallax 0.687 +- 0.097 mas. It also gives ipd_frac_multi_peak = 82: in 82 percent of the scans the image has more than one peak. This value indicates a resolved companion at about 0.1-1 arcsec. A resolved companion can increase the RUWE by itself. Thus the RUWE is not clean evidence for the 1.6-year third body. At about 1.2-1.5 kpc, the outer orbit (about 2.8 AU) has an angular size of about 2 mas, which Gaia cannot resolve. The Gaia RV data (4 transits, rv_amplitude_robust 20.8 km/s, rv_chisq_pvalue 6e-4) show variability, as a 19.9-day binary will.

## Method

### Photometry (`photometry.py`)

For each sector we subtract a per-cadence background (median of the faintest 40 percent of pixels more than 5 pixels from the target). The aperture is the pixel set within 3.5 pixels of the target with median flux above 20 percent of the central pixel. Two fixed circular apertures (radius 1.5 and 2.5 pixels) are robustness variants. The 14-arcsec Gaia neighbour (G = 12.7) is always inside the aperture. The cadence is 1800 s (sector 10), 600 s (36, 37) and 200 s (63-100).

### Eclipse times (`eclipse_times.py`)

We fit each eclipse in a +-0.75-day window with a symmetric phenomenological profile (Mikulasek 2015) times a quadratic baseline, integrated over the exposure time. The time error is the larger of the formal error (scaled by the reduced chi-square) and the scatter of the times from 39 cyclic shifts of the residuals (residual permutation). This error includes correlated noise. We use the 18 eclipses with full coverage and error below 20 minutes. One eclipse (sector 64, secondary, cycle 153) has a degenerate shape fit (error 39 minutes) and we do not use it. Robustness variants: apertures of radius 1.5 and 2.5 pixels, a +-1.0-day window, and times from the physical twin model (below).

### Eclipse geometry per sector (`twin_model.py`, `eclipse_phys.py`)

The primary and secondary depths are similar, so we model two equal stars (same radius R and surface brightness, quadratic limb darkening u1 = u2 = 0.25 in the TESS band). The projected separation is s(t) = sqrt(b^2 + v^2 (t - tc)^2) in units of R. For each sector we fit one impact parameter b and one light fraction f, plus a time and a quadratic baseline for each eclipse. The speed v is one global value from a grid search over all sectors (v = 5.35 R/day; chi-square changes by only 6 from 5.25 to 7.0, so v is weak). b comes mainly from the eclipse duration. f is strongly correlated with b (correlation 0.95) and differs between sectors, because the apertures differ.

### Three-body model (`triple.py`, `fit_triple.py`)

The model has two equal stars of total mass M12 = 4.0 solar masses (twin A4 stars, about 2.0 solar masses each) and a third body m3. It integrates the Newtonian three-body problem with REBOUND IAS15 from an epoch BTJD 2800 forward and backward. A Newton iteration finds each conjunction (minimum projected separation of the inner pair). The observed time includes the light-travel time across the outer orbit. The model gives the time, the impact parameter b = separation / R, and the projected speed at each observed eclipse. Free parameters: m3, inner osculating period, e1 cos w1, e1 sin w1, inner sky inclination, primary conjunction time, outer period P2, sqrt(e2) cos w2, sqrt(e2) sin w2, outer inclination, outer node relative to the inner node, outer mean anomaly, and R (in AU). The data are 18 times, 8 sector b values (sector error plus 0.01 in quadrature for model error), and the speed v = 5.35 +- 0.6 R/day. A WHFast integrator was tested and rejected: its timing errors were 60-500 s.

The search used 96 random starts (P2 log-uniform from 100 to 4000 d, random e2, angles and m3), each with a bounded trust-region least-squares fit, followed by long refinements of the 16 best end points. A second set of 10 starts (P2 150-3000 d, other seed) found the same 590-day modes.

### Out-of-sample test and joint fit

For the ASAS-3 test, each TESS-only solution is integrated back to 2000. The model V depth is f_V times the twin-star loss at the model b (V-band limb darkening u1 = 0.4, u2 = 0.25), averaged over every 6th cycle inside each of the three ASAS-3 windows of 575e53bd (2000.9-2003.5, 2003.5-2006.0, 2006.0-2010.0). One free f_V (the V-band light fraction of the eclipsing pair) is fitted. In the joint fit, f_V (0.2-1.0) is a 14th parameter and the 6 ASAS-3 depths are added to the data. For the ASAS-3 era, b is calculated from osculating inner elements (r at conjunction times |cos i| / R, WHFast). This value agrees with the full conjunction search to 0.0002 (primary) and 0.006-0.013 (secondary), which is small compared with the depth errors.

### Mass profile and light budget (`profile_m3.py`, `profile_forecast.py`, `profile_table.py`)

We fixed m3 at 11 values from 0.3 to 12 solar masses and fitted the other 13 parameters of the joint model. Each m3 was started from three joint solutions (m3 = 0.51, 2.34 and 12) with at most 100 evaluations (pass 1). Two further passes started from the best high-mass solutions (m3 = 6.5 and 12; at most 150 evaluations). The profile value at each m3 is the lowest chi-square from all 47 fits. Some fits stopped at the evaluation limit, so the profile values are upper limits on the true profile. We also give the profile with a 0.02 (instead of 0.01) systematic floor on the sector b values, without refitting.

For the light budget we calculate the V-band light fraction that one main-sequence third star gives: f_V,light = 0.88 L12 / (L12 + L3). Here 0.88 is the share of HD 303514 in the ASAS aperture from the Gaia flux of the 14-arcsec neighbour (575e53bd). L12 = 2 R^2 (Teff/5772)^4 with the fitted R and Teff = 8300 K (A4), and L3 is from the main-sequence mass-luminosity relation of Eker et al. (2018, MNRAS 479, 5491). Bolometric corrections are ignored. We call a mass light-consistent if |f_V - f_V,light| <= 0.08.

An ensemble MCMC (emcee, 42 walkers, differential-evolution moves) started in three solutions did not mix between them (acceptance 5 percent after 200 steps; walkers stayed near m3 = 0.5, 2.3 and 12). We stopped it and used the profile instead. The stopped chain is in `files/results/mcmc_multimode_stopped.npz`.

## Results

### Eclipse times

| Sector | Type | Cycle | BTJD | O - C (min) | error (min) |
| --- | --- | --- | --- | --- | --- |
| 10 | primary | 79 | 1572.47545 | +8.2 | 3.9 |
| 10 | primary | 80 | 1592.37109 | +5.9 | 4.4 |
| 36 | primary | 115 | 2288.74005 | -44.1 | 2.6 |
| 36 | secondary | 115 | 2298.90605 | -17.6 | 3.6 |
| 37 | primary | 116 | 2308.63566 | -46.5 | 3.4 |
| 37 | primary | 117 | 2328.53616 | -41.8 | 3.4 |
| 63 | secondary | 151 | 3015.21686 | -3.4 | 4.8 |
| 63 | primary | 152 | 3024.96749 | -2.0 | 3.6 |
| 63 | secondary | 152 | 3035.12846 | +17.3 | 4.8 |
| 64 | primary | 153 | 3044.87516 | +13.0 | 4.1 |
| 64 | primary | 154 | 3064.78314 | +28.5 | 5.9 |
| 90 | secondary | 188 | 3751.46014 | +61.6 | 8.4 |
| 90 | secondary | 189 | 3771.34776 | +47.7 | 7.4 |
| 99 | secondary | 203 | 4049.83599 | -57.7 | 9.3 |
| 99 | secondary | 204 | 4069.74498 | -40.9 | 11.5 |
| 100 | primary | 205 | 4079.48759 | -51.0 | 10.4 |
| 100 | secondary | 205 | 4089.63745 | -47.7 | 8.4 |
| 100 | primary | 206 | 4099.39232 | -40.2 | 14.4 |

O - C is relative to P = 19.89724781 d and T0 = BTJD 0.58719509 (primary), secondary at phase 0.51 (the ephemeris of 575e53bd). Figure 1 shows the times and two three-body solutions.

![Figure 1](files/figures/fig1_eclipse_times.png)

*Figure 1. Top: TESS eclipse-time residuals (black: primary; open: secondary) and the near-coplanar (blue) and near-polar (red) fits to TESS data only. Bottom: data minus model.*

### Sector impact parameters

| Sector | Year | b | error | light fraction f | error |
| --- | --- | --- | --- | --- | --- |
| 10.0 | 2019.27 | 1.697 | 0.013 | 0.54 | 0.04 |
| 36.0 | 2021.22 | 1.762 | 0.008 | 0.67 | 0.04 |
| 37.0 | 2021.28 | 1.773 | 0.009 | 0.63 | 0.04 |
| 63.0 | 2023.22 | 1.838 | 0.003 | 0.91 | 0.03 |
| 64.0 | 2023.30 | 1.818 | 0.006 | 0.56 | 0.03 |
| 90.0 | 2025.23 | 1.876 | 0.007 | 0.66 | 0.06 |
| 99.0 | 2026.05 | 1.878 | 0.008 | 0.62 | 0.07 |
| 100.0 | 2026.13 | 1.869 | 0.006 | 0.58 | 0.05 |

### Orbit families

| Solution | Data | chi-square | P2 (d) | e2 | m3 (Msun, M12 = 4) | mutual incl. (deg) | f_V | Result |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Near-coplanar (k91) | TESS only (27) | 18.90 | 593.7 | 0.26 | 2.31 | 7.1 | 0.64 (ASAS test) | predicts the 6 ASAS-3 depths: chi-square 1.5 |
| Near-polar (k43) | TESS only (27) | 11.61 | 586.8 | 0.28 | 2.45 | 91.6 | >1 needed | ASAS test chi-square 51; Kozai-Lidov e1 to 0.999: rejected |
| Near-coplanar (k91) | joint (33) | 20.90 | 593.5 | 0.26 | 2.34 | 6.1 | 0.71 | accepted |
| Near-coplanar (k56 path) | joint (33) | 15.76 | 600.0 | 0.18 | 12 (limit) | 2.9 | 0.62 | best fit; third body must be dark or underluminous |
| Near-coplanar (k56) | joint (33) | 27.67 | 584.2 | 0.62 | 0.51 | 6.4 | 1.00 | worse |
| Near-polar (k43) | joint (33) | 46.56 | 580.5 | 0.33 | 1.99 | 92.5 | 1.00 (limit) | rejected |
| P2 near 1,530 d | joint (33) | 34.72 | 1531 | - | 12 (limit) | - | - | rejected |
| P2 near 1,090 d | joint (33) | 54.4-69.7 | 1091-1115 | - | 5.4-5.8 | - | - | rejected |

Number of data in parentheses. In the TESS-only fits there are 13 parameters, in the joint fits 14. The M12-scale test of the joint k91 solution gives chi-square 20.91 (M12 = 3) and 20.89 (M12 = 5).

![Figure 2](files/figures/fig2_geometry_forecast.png)

*Figure 2. Left: impact parameter b from TESS sector fits (black), from ASAS-3 depths with the fitted f_V (grey, not used in the TESS-only fits), and model histories of near-coplanar and near-polar solutions. Right: inner eccentricity and mutual inclination over +-300 years.*

### Third-body mass profile

| m3 (Msun) | m3/M12 | chi-square | delta (b floor 0.01) | delta (b floor 0.02) | P2 (d) | e2 | mutual incl. (deg) | f_V fitted | f_V for one MS star | max b primary (year) | max b secondary | primary depth at minimum / 2026 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.3 | 0.075 | 33.40 | 17.6 | 17.1 | 584.6 | 0.63 | 11.4 | 1.00 | 0.88 | 1.947 (2032.8) | 1.977 | 0.26 |
| 0.5 | 0.125 | 26.72 | 11.0 | 9.8 | 563.9 | 0.59 | 8.7 | 0.84 | 0.88 | 1.924 (2034.0) | 1.957 | 0.44 |
| 0.8 | 0.200 | 26.88 | 11.1 | 9.8 | 568.5 | 0.46 | 7.5 | 0.92 | 0.88 | 1.931 (2031.0) | 1.981 | 0.36 |
| 1.2 | 0.300 | 22.12 | 6.4 | 4.6 | 583.3 | 0.38 | 7.8 | 0.81 | 0.85 | 1.894 (2032.0) | 1.956 | 0.79 |
| 1.7 | 0.425 | 21.09 | 5.3 | 3.3 | 589.0 | 0.31 | 7.0 | 0.75 | 0.77 | 1.896 (2029.8) | 1.936 | 0.73 |
| 2.3 | 0.575 | 20.90 | 5.1 | 2.9 | 593.3 | 0.26 | 6.2 | 0.71 | 0.58 | 1.887 (2029.8) | 1.927 | 0.74 |
| 3.2 | 0.800 | 20.84 | 5.1 | 4.1 | 592.9 | 0.24 | 4.5 | 0.72 | 0.32 | 1.900 (2029.5) | 1.933 | 0.63 |
| 4.5 | 1.125 | 18.96 | 3.2 | 2.8 | 593.8 | 0.21 | 4.5 | 0.60 | 0.11 | 1.886 (2028.5) | 1.918 | 0.73 |
| 6.5 | 1.625 | 17.48 | 1.7 | 1.6 | 596.1 | 0.19 | 3.6 | 0.62 | 0.03 | 1.885 (2028.5) | 1.918 | 0.77 |
| 9 | 2.250 | 16.47 | 0.7 | 0.7 | 597.8 | 0.18 | 3.3 | 0.60 | 0.01 | 1.881 (2028.0) | 1.916 | 0.83 |
| 12 | 3.000 | 15.76 | 0.0 | 0.0 | 600.0 | 0.18 | 2.9 | 0.62 | 0.00 | 1.885 (2028.0) | 1.918 | 0.82 |

![Figure 3](files/figures/fig3_mass_profile_forecast.png)

*Figure 3. Top left: chi-square profile in m3 (dotted 1, dashed 4). Top right: fitted V-band light fraction (black) and the fraction expected for one main-sequence third star (red, band +-0.08). Bottom left: predicted primary (solid) and secondary (dashed) impact parameters of the profile solutions (thick lines: light-consistent masses 1.2 and 1.7). Bottom right: predicted eclipse times 2026-2027.*

### Forecast

All 11 profile solutions keep b < 2 until at least 2060 (`files/results/profile/forecast.csv`, `b_forecast/`). The near-coplanar solutions with m3 >= 1.2 predict these eclipse times, relative to the ephemeris of Figure 1 (range over the profile solutions with m3 = 1.2-12; `files/results/profile/oc_forecast.csv`):

| Eclipse | Cycle | Year | BTJD | Predicted O - C (min) |
| --- | --- | --- | --- | --- |
| primary | 212 | 2026.49 | 4218.8 | -20 to +17 |
| primary | 216 | 2026.70 | 4298.4 | +34 to +69 |
| primary | 220 | 2026.92 | 4378.0 | +21 to +66 |
| primary | 224 | 2027.14 | 4457.6 | +0 to +42 |
| primary | 228 | 2027.36 | 4537.1 | -24 to +6 |
| primary | 232 | 2027.57 | 4616.7 | -49 to -30 |
| secondary | 214 | 2026.62 | 4268.8 | +14 to +48 |
| secondary | 222 | 2027.06 | 4427.9 | +20 to +26 |
| secondary | 230 | 2027.49 | 4587.1 | -48 to -35 |

The 2026 dates are after our last data (sector 100, March 2026) and were not used. A linear-drift model predicts eclipse depths that fall to zero near 2030. The three-body model predicts that the primary stays at 63-83 percent of its 2026 depth or deeper before the eclipses deepen again. The secondary comes closer to contact (b up to 1.92-1.98) and becomes very shallow. In the main solution (joint k91) the shallowest eclipses occur near 2029.9 at b = 1.885 (primary) and 1.929 (secondary).

## Interpretation

To our knowledge (the literature search of 575e53bd and the campaign archive), the eclipse timing gives the first direct detection of the third body of HD 303514. The period ratio P2/P1 = 30 makes the system a compact hierarchical triple. In such a triple the nodal precession period is short (here about 136-140 years), and the change of the eclipse geometry since 2002 follows directly from the orbit that the timing measures. The TESS impact parameters alone could not separate a linear drift from a turning point. The three-body orbit predicts the turning point. The ASAS-3 depths, which the timing fits did not use, then agree with the near-coplanar orbit and reject the near-polar one.

The forecast of eclipse loss near 2030 in the source publications assumed a straight or slowly curved drift in a free precession model. With the measured outer orbit, the precession cycle is short enough that the inclination turns before contact is lost. The margin to contact is small (0.05-0.12 in units of R for the primary and 0.02-0.08 for the secondary), so the forecast is sensitive to the eclipse-shape model; this is stated in the limitations.

The mass result is a lower limit (m3/M12 >= about 0.3) with a mild dynamical preference for a heavier third body. A light-consistent single main-sequence third star (m3 = 1.2-1.8 solar masses, an F- or late A-type star) is worse than the best fit by 3.3-6.4 in chi-square; this difference is comparable to the change caused by the assumed b systematic floor. We therefore do not claim a heavy or dark third body. Radial velocities can decide: the systemic velocity of the inner pair has a semi-amplitude K12 = 2 pi a12 sin i2 / (P2 sqrt(1-e2^2)) of about 13 km/s for m3 = 1.5 and about 49 km/s for m3 = 12 (M12 = 4, P2 = 590 d), on a 1.6-year cycle.

## Limitations

- The third-body mass is degenerate with e2 and the orientation in the timing data. We give a profile with a lower limit, not a measured mass. Radial velocities of the inner pair or Gaia DR4 epoch astrometry can measure it.
- The profile values come from local fits that sometimes stopped at the evaluation limit; they are upper limits, and the true profile can be lower at some masses.
- The twin-star eclipse model assumes equal stars, a fixed limb darkening and one global speed. The sector b values depend on these assumptions. The b margin to eclipse loss (0.05-0.12 for the primary, 0.02-0.08 for the secondary) is comparable to plausible systematic errors of this model, so the "no loss" forecast is model-dependent at this level.
- The ASAS-3 depths are a published aggregate (575e53bd) with assumed window limits. Our averaging over every 6th cycle approximates their fold.
- The search used 106 random starts and local fits. It is not a proof of a global minimum. The MCMC of all modes did not mix between them (acceptance 5 percent, separate islands at m3 = 0.5, 2.3 and 12), so we do not give posterior probabilities across modes.
- M12 = 4 is assumed from the spectral type. The ratio m3/M12 changes by less than 10 percent for M12 = 3-5.
- Errors on eclipse times use residual permutation. The TESS sector 99-100 eclipses are shallow (0.4 percent) and have errors of 8-14 minutes.
- Tides, general relativity, stellar rotation and the resolved Gaia companion are not modelled. Their effects on the 7-year timing are expected to be small (apsidal periods of order 10^5-10^6 years from tides and GR).
- All analysis was done by an AI model (one analyst). Classification steps were automatic.

## Reproduction

See `files/REPRODUCE.md`.

## Provenance

- Job sci-1107-dell-astronomy-b0255a0422c4, campaign 11_07_2026, topic astronomy, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Builds on SCI 575e53bd97d3bf41769932250f0702d481c2a7b004d3e78e63fdf9c0118d4586 (discovery and ASAS-3 depths) and 2f7e9f37cf9b0c374980f84c993d79da289d91bdb335277d932a356202a2dede (curved precession forecast).
- External data terms: `files/EXTERNAL_DATA_NOTICE.md`.
