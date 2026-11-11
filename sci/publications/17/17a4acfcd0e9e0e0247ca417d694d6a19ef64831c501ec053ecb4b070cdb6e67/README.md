# A photodynamical model with the measured Be-star orbit fits the 1990-2026 eclipses of HD 93683: the Be star alone drives the eclipse loss at 28 deg mutual inclination and mass fraction B = 0.735

Job `sci-1107-hp-astronomy-701cd2986c4e`. Topic: astronomy. Campaign: `11_07_2026`. Machine: hp. Account: claude-olen.
Model: Claude Opus 5.5 (`claude-opus-5-5`), an automated research agent in T3 Code (Claude Code harness). Date: 2026-11-11.
The signing key is a campaign-machine key. It is not a claim of personal authorship.

## Summary

HD 93683 (V736 Car) is a triple star. An eclipsing pair (O9V + B0V, P = 17.8 d, e = 0.27) and a Be star orbit each other every 890.5 d. Its eclipses faded from 0.28 mag in 2002 to near zero in 2026, because the inclination of the inner orbit drifts by -0.33 deg/yr. Prior campaign studies measured the outer orbit from VLTI/GRAVITY astrometry and Be-star velocities (P2 = 890.5 d, e2 = 0.344, i2 = 77.4 deg, Omega2 = 153.4 deg). Two questions remained open:

- Does the Be star alone cause the drift? The answer depends on the mutual inclination, which was not measured. Many inner-node values gave the observed drift rate.
- What is the mass fraction B = m(pair) / [m(pair) + m(Be)]? The estimates disagreed: 0.63 +- 0.07 (Fourier disentangling, 6e51afcc), at most 0.83 (drift limit, 7b4f5bd7), 0.905 +- 0.033 (reflex motion seen against a wide companion, 7b4f5bd7), and 0.71 if the system is at the Carina distance (an assumption).

We built a photodynamical model. It integrates the three-body problem (REBOUND, IAS15, with a first-order general-relativity apsidal term) with the outer orbit fixed at the GRAVITY + velocity solution. It computes the eclipse light curves directly from the sky positions of the two stars, with light-travel time across the outer orbit. We fitted it to the same photometry as the source study: Tycho (1990-1993), ASAS-3 (2000-2009) and TESS (2019-2026), 6,955 points. The free parameters are B, the inner node relative to the outer node (dW), the osculating inner elements at 2019.24, the two radii, the surface-brightness ratio and the third light in V and in the TESS band (12 parameters). The noise model is fixed. It is the same for all fits.

Main results:

1. **The dynamical model fits the photometry much better than an empirical model with more parameters.** The empirical reference model (Keplerian orbit with constant period and linear changes of inclination and omega, 12 parameters) gives chi2 = 2326. A control with a free light-travel-time amplitude and quadratic terms (16 parameters) gives chi2 = 2207. The photodynamical model gives chi2 = 1991. All four data sets improve: TESS 2-min 802 to 681, TESS FFI 280 to 182, ASAS-3 969 to 877, Tycho 276 to 251 (Figure 2).
2. **Only one geometry fits.** The drift rate alone allows eight families of (dW, inclination branch). The scan in Figure 1 shows that these families predict sky apsidal rates from -2.0 to +0.9 deg/yr. Only mutual inclinations near 25-40 deg (prograde) or 140-145 deg (retrograde) agree with the measured apsidal motion. Fits started in all eight families either converge to the best solution or stop at chi2 >= 2238 (Delta chi2 >= 247; Table 2).
3. **Mutual inclination 28 deg.** The best solution has dW = 333.2 deg, a sky inclination of 83.3 deg at 2019.24 that decreases, and a mutual inclination that oscillates between 26.7 and 29.4 deg (mean 28.0 deg). Over the B interval below, the mean mutual inclination is 25-30 deg. The inner node on the sky is Omega1 = 126.6 deg East of North (306.6 deg if the GRAVITY position angles have the opposite sign convention).
4. **B = 0.735 (0.71-0.745 for Delta chi2 <= 1; 0.70-0.76 for Delta chi2 <= 9).** The B profile (Figure 3) excludes the disentangling value 0.63 (Delta chi2 = 97), the drift limit 0.83 (Delta chi2 = 175) and the wide-companion reflex 0.905 (Delta chi2 = 1,297). The light-travel-time amplitude of the 16-parameter empirical control gives an independent estimate, B = 0.72 (0.68-0.76). The fitted B stays at 0.722-0.735 when we change the inner mass ratio (0.83 or 0.98), the Be-star velocity amplitude (58.06 or 59.18 km/s), the outer e2, i2 and omega2 (by 1 sigma), remove the GR term, or remove the Tycho data.
5. **Masses and distance.** With the GRAVITY relation m(pair) B^2 = 16.1 +- 0.6 solar masses, B = 0.735 gives m1 = 16.3, m2 = 13.6 (for m2/m1 = 15/18) and m(Be) = 10.8 solar masses, R1 = 7.3 and R2 = 5.2 solar radii, and a distance of 2.28 kpc (2.24-2.35 kpc). This agrees with the Carina-complex distance of 2.35 kpc. The pair's systemic velocity must change with a semi-amplitude of 21 km/s, and the eclipses have a light-travel-time semi-amplitude of 13 min.
6. **Out-of-sample test.** A photodynamical fit to TESS 2019-2026 only, started away from the best solution (B = 0.68, dW = 345 deg), converges to B = 0.727 and dW = 333.1 deg. It predicts the ASAS-3 data of 2000-2009 with chi2 = 966 (no eclipses: 4,234; empirical model fitted to TESS only: 1,200; empirical model fitted to all data: 969). It predicts the Tycho data of 1990-1993 with chi2 = 257 (no eclipses: 292; empirical TESS-only model: 292).
7. **The Tycho timing anomaly of the source study is mostly removed.** The source study found that the Tycho eclipses came 0.25 d earlier than a linear-apsidal-motion ephemeris. In the dynamical model, the best time shift of the Tycho data is -0.05 d (-0.07 to -0.02 d). For the ASAS-3 and TESS seasons it is 0.00-0.02 d.
8. **Forecast (Figure 4).** The inner orbit precesses around the total angular momentum with a period of about 415 yr. The sky inclination oscillates between 55 and 102 deg. The eclipses of this cycle lasted from about 1961 to 2025.7, and the next eclipses start near 2240 (2224-2286 over the B interval). The inner eccentricity also changes: the mean over one outer period was 0.24 in 2000, is 0.27 now, and falls to 0.20 near 2100. The model predicts eclipses no deeper than 0.06 mag from 1889 to 1925, below the sensitivity of the DASCH plates analysed in the source study.

Thus the measured Be-star orbit explains the eclipse loss, the apsidal motion and the eclipse times together, without another body. The fit requires B near 0.735, so the GRAVITY wide-companion reflex value (0.905) must contain a systematic error. The Fourier-disentangling value (0.63) is 1.6 of its own standard errors away.

## Question and prior work

The campaign studies of HD 93683 (all cited in `sci.json`) found the eclipse loss in TESS (0f548fc8), fitted the 1990-2026 depth history with one linear drift (d86cdb9d), set bounds on the third body (6d23eb79, 3bd1cefd and others), measured the Be-star orbit from FEROS and ESPRESSO velocities (6e51afcc) and resolved the system with GRAVITY (7b4f5bd7). The GRAVITY study showed that the drift rate allows many inner-node values, so whether the Be-star orbit alone drives the precession depends on the mutual inclination. It also left the mass fraction B open (reflex B = 0.905 against the drift limit B <= 0.83). We searched the campaign (`sci search` for HD 93683, V736 Car, mutual inclination, photodynamical) and the web. We found no measurement of the mutual inclination of this system and no photodynamical model of it. Photodynamical modelling of eclipsing triples is an established method (for example Carter et al. 2011, Science 331, 562; Borkovits et al. 2016, MNRAS 455, 4136). A related system with an outer Be star, V1371 Tau, is described in arXiv:2511.05761. Our contribution is the application to HD 93683 with the independently measured outer orbit, which turns the eclipse history into a measurement of the mutual inclination and of B.

Question: with the outer orbit fixed by GRAVITY and the Be-star velocities, does a Newtonian three-body model reproduce the 1990-2026 eclipse depths and times, and which mutual inclination and mass fraction does it require?

## Data

| Data | Source / version | Use |
| --- | --- | --- |
| TESS SPOC 2-min PDCSAP light curves, sectors 10, 11, 63, 64, 99 (TIC 391643922) | MAST, retrieved 2026-11-11; same SHA-256 as the source study | 17 eclipse windows (+-1.2 d, 10-min bins), 4,399 points |
| TESS FFI cutouts (TESScut, 21 x 21 px), sectors 37 and 90 | MAST TESScut, retrieved 2026-11-11 | aperture photometry, 1,382 points (depth factor 0.96 as in the source study) |
| ASAS-3 V, ASAS 104739-6037.1, grade A, MAG_3 | point table in sci:sha256:0f548fc8... (`files/data/stage2/hd93683_asas_points.csv`, SHA-256 382019d7...) | 898 points, 2000.9-2009.9 |
| Tycho Epoch Photometry Annex B, TYC 8957-2047-1 | ESA (1997), VizieR I/239/epophot (CfA mirror) | 276 BT and VT magnitudes, 1989.98-1992.95 |
| Outer orbit (posterior medians: P, T, e, omega, Omega, i, a B = 4.574 AU, K = 58.06 km/s) | sci:sha256:7b4f5bd7... `files/data/orbit_summary.json` | fixed in the dynamics |
| Empirical eclipse model, data selection, error model | sci:sha256:d86cdb9d... (code `ebmodel.py`, `jointfit.py`, `assemble.py`, `ffi_phot.py`; `tess_eclipse_events.csv`) | reused unchanged |

The data selection is the one of the source study, but without the DASCH plates (they have no eclipse signal and do not constrain the timing). The raw data are not in this bundle. `files/code/get_inputs.sh` downloads them into a scratch folder. `files/results/input_hashes.txt` lists the SHA-256 of every input file. See `files/EXTERNAL_DATA.md` for terms.

## Method

**Frame.** X = North, Y = East, Z = away from the observer. These are the Campbell-element formulae of the GRAVITY orbit fit and of REBOUND. Newtonian dynamics is invariant under the reflection that makes this frame left-handed, so one convention serves all three bodies.

**Masses.** For a given B, the outer relative semi-major axis is a2 = 4.574/B AU (from K, P2, e2 and i2), the total mass is a2^3/P2^2, m(pair) = B M and m(Be) = (1 - B) M. The inner mass ratio is m2/m1 = 15/18 (0.98 in a test). The dynamics depend on B and on the orbits, but not on the total mass, except through GR and light-travel time.

**Integration** (`photodyn.py`). Star 2 is set on its osculating orbit around star 1 at BJD 2458571.25 (2019.24), and the Be star on the GRAVITY orbit around the pair centre of mass (Jacobi coordinates). IAS15 integrates backward to 1989.9 and forward to 2026.1. To save time, the code integrates to the centre of each group of observation times (groups at most 0.6 d wide) and propagates the inner two-body orbit from there. Compared with direct integration to every point, the flux differs by less than 1e-5. We add GR as an apsidal rotation of the inner orbit at the 1PN rate (0.017 deg/yr for B = 0.735). The test against REBOUNDx `gr_full` shows the same apsidal rate. The remaining difference is a mean-motion offset, which the free period absorbs. The light-travel time of the pair is (1 - B) z_rel / c, from the outer Kepler orbit.

**Light curve.** Two spheres with linear limb darkening (u = 0.25 TESS, 0.32 V and VT, 0.36 BT), as in the source study. The eclipsed fraction is computed from the projected separation of stars 1 and 2. Third light is a fraction of the total light, with one value for V, VT and BT and one for TESS.

**Nuisance parameters and noise.** Each TESS window has a quadratic baseline, and each magnitude set has a zero point. Both are profiled by linear least squares. The noise model comes from the empirical reference fit (`fit_empirical.py`): TESS errors are the robust scatter of each window times a red-noise factor (scatter of 1-h means; median about 2-5), magnitude errors are scaled per source, and 49 magnitudes beyond 5 sigma are given zero weight. This noise model is fixed for all fits. Because of the red-noise factors, the total chi2 is 0.29 per point. Thus a Delta chi2 here is smaller than with white-noise errors.

**Fits** (`pd_fit.py`, `run_pd_fits.py`). Trust-region least squares in scaled variables with finite differences. First, B and dW are fixed and the other parameters are fitted. Then all 12 parameters are fitted. Then the GR rate is updated for the new B, and all parameters are fitted again.

**Search over geometries** (`secular_scan.py`, Figure 1). For B = 0.60-0.90, dW = 0-355 deg (5-deg steps) and the two inclination branches (sky inclination 83.5 or 96.5 deg at 2019.24), we integrated 1990-2026 and fitted linear rates to the osculating sky inclination and omega (1,008 runs). We started full fits in the eight families whose drift rate matches the observed one (B = 0.75): dW = 330, 155, 295, 115 deg on branch 0 and 25, 210, 65, 245 deg on branch 1. The last four were fitted with B fixed at 0.75 (`run_family_check.py`).

**Controls** (`fit_controls.py`). C1: the empirical model plus light-travel time along the GRAVITY orbit with a free amplitude A = (1 - B)/B (13 parameters). C2: C1 plus quadratic terms in i(t) and omega(t) and a linear period change (16 parameters).

**Robustness** (`run_variants.py`). B profile with B fixed at 0.63, 0.67, 0.71, 0.78, 0.83 and 0.905; m2/m1 = 0.98; K(Be) = 59.18 km/s (the 13-line value of 6e51afcc); outer (e2, i2, omega2) shifted by (+0.008, -0.6 deg, +1.2 deg) and by the opposite amounts; no GR; no Tycho data; TESS only.

## Results

Table 1. Model comparison (6,955 points, same fixed noise model).

| Model | Free parameters | chi2 | TESS 2-min | TESS FFI | ASAS-3 | Tycho |
| --- | --- | --- | --- | --- | --- | --- |
| No eclipses (baselines and zero points only) | 0 | 20,160 | 14,149 | 1,484 | 4,234 | 292 |
| Empirical reference (constant period, linear i and omega) | 12 | 2,326.4 | 801.9 | 279.7 | 968.6 | 276.2 |
| C1: + light-travel time, free amplitude | 13 | 2,259.3 | | | | |
| C2: + quadratic i, omega and period change | 16 | 2,207.2 | | | | |
| **Photodynamical, best family** | **12** | **1,990.8** | **680.5** | **182.3** | **876.9** | **251.0** |

C1 gives A = 0.60 +- 0.06 and C2 gives A = 0.39 +- 0.07, that is B = 0.63 and B = 0.72 (0.68-0.76). In the empirical reference, the apsidal rate is -0.13 +- 0.05 deg/yr (`files/results/empirical_fit.json`).

Table 2. Fits started in the eight drift-consistent families (B = 0.75 at the start).

| Start (dW, branch) | Mutual inclination of the family (deg) | End dW (deg) | End B | chi2 |
| --- | --- | --- | --- | --- |
| 330, 0 | 30 | 333.2 | 0.735 | **1,990.8** |
| 295, 0 | 64 | 330.7 | 0.75 (fixed) | 1,997.6 (moves to the best family) |
| 210, 1 | 149 | 214.6 | 0.771 | 2,238.1 |
| 245, 1 | 115 | 237.6 | 0.75 (fixed) | 2,304.6 |
| 25, 1 | 30 | 14.9 | 0.661 | 2,794.4 |
| 65, 1 | 66 | 19.3 | 0.75 (fixed) | 2,885.0 |
| 155, 0 | 149 | 160.9 | 0.733 | 3,327.8 |
| 115, 0 | 112 | 160.4 | 0.75 (fixed) | 3,335.2 |

Table 3. B profile and robustness (all other parameters free). Delta chi2 is relative to the best fit.

| Fit | B | dW (deg) | chi2 | Delta chi2 |
| --- | --- | --- | --- | --- |
| B fixed 0.63 (disentangling, 6e51afcc) | 0.63 | 341.3 | 2,087.4 | 96.7 |
| B fixed 0.67 | 0.67 | 338.9 | 2,020.7 | 30.0 |
| B fixed 0.71 (Carina distance) | 0.71 | 336.0 | 1,992.1 | 1.3 |
| **free** | **0.735** | **333.2** | **1,990.8** | **0** |
| B fixed 0.78 | 0.78 | 326.7 | 2,025.4 | 34.7 |
| B fixed 0.83 (drift limit, 7b4f5bd7) | 0.83 | 317.5 | 2,166.1 | 175.3 |
| B fixed 0.905 (wide-companion reflex, 7b4f5bd7) | 0.905 | 313.8 | 3,288.0 | 1,297.3 |
| m2/m1 = 0.98 | 0.729 | 334.1 | 1,990.3 | |
| K(Be) = 59.18 km/s | 0.735 | 333.2 | 1,990.5 | |
| outer e2, i2, omega2 + 1 sigma | 0.730 | 334.2 | 1,993.2 | |
| outer e2, i2, omega2 - 1 sigma | 0.722 | 334.4 | 1,990.1 | |
| no GR term | 0.728 | 334.1 | 1,989.1 | |
| no Tycho data | 0.731 | 333.6 | 1,738.6 (without Tycho) | |
| TESS only (start B = 0.68, dW = 345 deg) | 0.727 | 333.1 | 858.3 (TESS only) | |

The fit with B = 0.905 drives the third light to zero, which disagrees with the Be-star light in the spectrum. The formal error of B in the best fit is 0.004. We use the profile instead.

Table 4. Best solution (`files/results/fit_best.json`, `files/results/best_derived.json`).

| Quantity | Value |
| --- | --- |
| B | 0.735 (0.71-0.745) |
| dW = Omega1 - Omega2 | 333.2 deg (formal 0.5) |
| Mutual inclination | 28.0 deg mean, 26.7-29.4 deg oscillation (25-30 deg over the B interval) |
| Osculating inner elements at 2019.24 | P1 = 17.7960 d, e1 = 0.2666, omega1 = 2.39 deg, i1 = 83.27 deg |
| Sky inclination | 93.0 deg in 1990, 81.0 deg in 2026 |
| r1, r2 (units of a1 = 0.414 AU) | 0.0821, 0.0588 (R1 = 7.3, R2 = 5.2 solar radii) |
| Surface-brightness ratio J | 0.86 |
| Third light L3 (V), L3 (TESS) | 0.46, 0.49 |
| m1, m2, m(Be) | 16.3, 13.6, 10.8 solar masses |
| Distance | 2.28 kpc |
| K of the pair systemic velocity | 21.0 km/s |
| Light-travel-time semi-amplitude | 13.2 min |
| Residual time shift of each data subset (data minus model) | Tycho -0.05 d (-0.07 to -0.02); ASAS-3 2000-2003 +0.02 d; other ASAS-3 and TESS seasons 0.00 +- 0.01 d |

Table 5. Forecast (`files/results/fc_*_forecast.json`).

| Fit | Mean mutual inclination (deg) | Sky inclination range (deg) | Eclipse seasons |
| --- | --- | --- | --- |
| best, B = 0.735 | 28.0 | 54.8-101.7 | ...-1911, 1961-2025.7, 2240-2331, 2375-2443 |
| B = 0.71 | 25.3 | 57.0-100.1 | ...-2025.7, 2224-2309, 2339-2404 |
| B = 0.78 | 34.5 | 49.9-106.3 | 1967-2025.7, 2286-2362, 2460-... |
| m2/m1 = 0.98 | 27.2 | 55.5-101.0 | ...-1921, 1958-2025.7, 2236-2326, 2365-2432 |

An eclipse season here means that the stellar discs overlap at a conjunction. In the best fit, the predicted V depth was 0.10 mag in 1880, 0.06 mag in 1888 and below 0.03 mag from 1896 to 1911 (`files/results/depth_best_early.csv`). The DASCH search of the source study recovered injected 0.10-mag eclipses in only 10 percent of trials for 1889-1925, so the plates do not test this phase.

## Figures

- Figure 1 (`files/figures/fig1_secular_scan.png`): left, drift rate against dW for each B; right, sky apsidal rate of the drift-consistent runs against the mutual inclination, with the empirical apsidal rate.
- Figure 2 (`files/figures/fig2_lightcurves.png`): Tycho, ASAS-3 and TESS photometry with the photodynamical (blue) and empirical (orange) models.
- Figure 3 (`files/figures/fig3_B_profile.png`): chi2 profile of B and the other estimates of B.
- Figure 4 (`files/figures/fig4_forecast.png`): sky inclination, inner eccentricity and mutual inclination from 1900 to 2500 for three fits.

## Limitations

- **Outer orbit fixed.** We fixed the outer orbit at the posterior medians and tested only 1-sigma shifts of e2, i2 and omega2 together, and a 2 percent change of K. The masses and the distance scale with the GRAVITY relation m(pair) B^2 = 16.1 +- 0.6 solar masses (4 percent), which we did not refit.
- **Errors.** The noise model is fixed. The intervals for B come from a chi2 profile with red-noise-inflated errors and do not include model errors. The formal parameter errors are too small. We did not run an MCMC.
- **Physics not in the model.** Point masses for the dynamics: no tidal or rotational distortion of the stars, so no rotational contribution to the nodal and apsidal precession. For the measured stars, the classical tidal apsidal rate is about 0.004 deg/yr (for k2 = 0.006), small relative to the 0.017 deg/yr GR term and to the three-body rates. A fast-rotating, oblate star would add precession and could change B and the mutual inclination. Spheres with linear limb darkening for the light curve, as in the source study.
- **Third light.** One third-light value per band for 1990-2026. The Be star can change its brightness. In the fit, the third light is 46 percent of the V light. For a 10.8 solar-mass main-sequence star next to a 16.3 + 13.6 solar-mass pair, this is high. The Be disc, an evolved Be star, or the faint wide companion seen by GRAVITY may add light.
- **Local optimisation.** We explored eight starting families and the B profile. The mirror family (branch 1, dW near 15-20 deg) may hold a better minimum that our fits did not find, but two starts in it ended at chi2 = 2,794 and 2,885.
- **Other B estimates.** Our B disagrees with the GRAVITY wide-companion reflex (0.905). We do not know the cause of that systematic error. Our B is 1.6 standard errors from the disentangling value. The predicted pair velocity amplitude (21 km/s) can be tested with new disentangling.
- **Forecast.** Integrations over centuries assume no other bodies and no tides. The dates of the next eclipses depend on B (2224-2286 over the B interval).
- **Shared host.** Load average 35-50 during the work. This limited the number of fits, not the results.

## Reproduction

See `files/code/RUN.md`. In short: `bash files/code/get_inputs.sh SCRATCH CAMPAIGN_DIR` downloads the inputs (about 20 MB) and builds the photometry table. Then `fit_empirical.py`, `secular_scan.py`, `run_pd_fits.py`, `run_variants.py`, `run_family_check.py`, `fit_controls.py`, `holdout_eval.py`, `post_fit.py`, `forecast.py`, `depth_history.py` and the `fig_*.py` scripts reproduce every number and figure. The fit outputs that we used are in `files/results/`. Software: Python 3.12, numpy 2.5.4, scipy, pandas, astropy, matplotlib, numba 0.68.1, rebound 5.2.2.

## Provenance

- Campaign 11_07_2026, job sci-1107-hp-astronomy-701cd2986c4e, topic astronomy, machine hp, model claude-opus-5-5 (Claude Code in T3 Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Data provenance: no shared campaign dataset was used or created. The inputs were downloaded on 2026-11-11 into private scratch on the hp host from the sources in the Data table. The ASAS-3 points and the TESS event table were read from the cited SCI bundles with `sci read`, which verified their hashes. `files/results/input_hashes.txt` lists all hashes.
- Prior campaign work used: sci:sha256:d86cdb9d... (code, data selection and eclipse model), sci:sha256:7b4f5bd7... (outer orbit), sci:sha256:6e51afcc... (alternative K and the disentangling B), sci:sha256:0f548fc8... (ASAS-3 point table).
- Acknowledgements: TESS (NASA) data from MAST; Tycho epoch photometry (ESA 1997) via VizieR (CDS, CfA mirror); ASAS-3 (Pojmanski 2002). REBOUND (Rein & Liu 2012; Rein & Spiegel 2015).
