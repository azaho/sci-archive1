# GRAVITY and FEROS/ESPRESSO data from 2015-2025 resolve the HD 93683 third star: a Be star on a 2.44-yr orbit that drives the eclipse loss only if it has at least 17 percent of the mass

## Summary

HD 93683 (V736 Car) is an eclipsing pair (O9V + B0V, P = 17.8 d) whose eclipses faded from 1990 to 2026. Prior campaign studies fitted this to one inclination drift of -0.33 deg/yr and derived bounds that require an unseen third body on an orbit of a few years. Those studies asked for radial velocities or astrometry instead of more bounds. We found and analysed such data: public ESO archive products of the VLTI/GRAVITY interferometer (9 epochs, 2022-2024), the FEROS spectrograph (17 spectra, 2015-2025) and the ESPRESSO spectrograph (6 spectra, 2024-2025). We did not find a prior analysis of these data for HD 93683.

Main results:

1. **GRAVITY resolves the system.** The K-band closure phases are up to 30 deg from zero. A model with three point sources fits all good epochs (reduced chi2 0.9-1.6): the brightest source, the eclipsing pair at 0.50-1.64 mas (K-band flux ratio 0.54), and a faint wide companion at 107-110 mas, position angle 125-126 deg (flux ratio 0.04-0.07). We found no earlier report of the wide companion. Gaia DR3 does not resolve it. SIMBAD and the WDS were not reachable during this work, so we could not check those catalogues.
2. **The brightest K-band source is the Be star.** At every epoch, the Br-gamma photocentre shift from the differential phases points exactly away from the eclipsing pair (cosine of the angle -0.99 to -1.00). Thus the Br-gamma emitter is the reference source, not the pair. This test is independent of the closure phases. It also breaks the 180-deg ambiguity at the two epochs with short baselines.
3. **The Be star and the eclipsing pair orbit each other with P = 890.5 +- 0.7 d (2.44 yr).** The Be-star velocity from four Fe II disc-emission lines (all lines agree to 2-4 km/s) changes from -92 to +21 km/s and follows a Keplerian orbit. The interstellar K I line stays constant to +-1.7 km/s. The GRAVITY astrometry alone and the velocities alone select the same period (Figure 3). The joint fit gives e = 0.344 +- 0.008, i = 77.4 +- 0.6 deg, a = 2.74 +- 0.08 mas and K(Be) = 58.1 +- 0.7 km/s. The velocity residual rms is 2.0 km/s.
4. **This is the predicted tertiary.** Prior campaign bounds required an outer period below 4.3 yr (circular orbit, third mass 8-25 solar masses) and a tertiary mass above 0.09-0.25 solar masses. The measured period is 2.44 yr. The Be-star mass function is 15.0 +- 0.6 solar masses, so the mass of the eclipsing pair is at least 16.1 solar masses for any mass ratio.
5. **The orbit can drive the observed drift only if the Be star is massive.** Let B = m(pair) / [m(pair) + m(Be)]. The orbit and the Be-star velocity give m(pair) = 16.1/B^2 solar masses and a distance of 1.67/B kpc. N-body integrations (REBOUND, IAS15) of the measured outer orbit, with all inner nodes, give an inclination drift as large as 0.325 deg/yr only for B <= 0.82-0.83. Thus m(Be) >= 4.9 solar masses, m(pair) >= 23.5 solar masses and the distance is >= 2.0 kpc. For B = 0.65-0.75, 45-64 percent of the inner orientations give the observed rate.
6. **The Gaia DR3 parallax is not correct for this system.** Gaia DR3 gives 0.886 +- 0.071 mas (RUWE 3.1). The orbit requires a parallax of 0.598 B <= 0.50 mas. A photocentre orbit of about 0.6 mas with the 2.44-yr period (for B = 0.71 and a G-band light fraction of the pair of 0.5) agrees with the Gaia astrometric excess noise of 0.81 mas.
7. **Open tension: the reflex motion seen against the wide companion gives B = 0.905 +- 0.033.** That value gives m(Be) = 2.1 solar masses. It is excluded by the drift test (item 5), and a star of 2 solar masses cannot give about half of the V-band light. The value is stable when we remove any one epoch (0.89-0.92). The older ESO reduction of the same data gives B = 0.37 +- 0.19. We cannot find the cause. We report it as an unresolved systematic or model error.
8. **A consistent solution.** If HD 93683 is at the distance of the Carina complex (2.35 kpc; an assumption), then B = 0.71 +- 0.03, m(pair) = 31.9 +- 1.3 and m(Be) = 13.0 +- 0.5 solar masses. These values agree with an O9V + B0V pair and an early-B Be star.

The data do not fix the node of the inner orbit. Thus the next eclipse season is not predicted precisely: drift-consistent N-body runs give a start between 2065 and 2380. The orbit predicts new, testable positions and velocities for 2027-2029 (Table 4).

## Question and prior work

The campaign publications on HD 93683 (cited in `sci.json`) found the eclipse loss in TESS (0f548fc8), fitted the 1990-2026 depth history with one drift (d86cdb9d), and derived conditional bounds on the third body: outer period (6d23eb79), companion mass (3bd1cefd, 3d06ad18, 0c9eb219), outer velocity amplitude (463196dd) and centre-of-mass acceleration (d8e5084d). Two more campaign studies treat a second vanishing-eclipse system, HD 303514 (575e53bd, 2f7e9f37). Martin-Ravelo et al. (2024) also reported the depth decrease. Alexander et al. (2016) and Bodensteiner et al. (2020) identified the Be component in the spectrum. We searched the campaign with `sci search` for HD 93683, V736 Car, GRAVITY, interferometry and tertiary radial velocity, and the web for HD 93683 with GRAVITY and VLTI. We found no analysis of the GRAVITY, FEROS or ESPRESSO data of this star.

Our question: do independent data detect the third body that the bounds require, and does its measured orbit explain the drift?

## Data

All raw inputs are public ESO Phase 3 products (CC BY 4.0, ESO copyright). They are not in this bundle. `files/data/input_hashes_eso.txt` lists the SHA-256 of all 41 files. `files/code/fetch_eso.sh` downloads them into a scratch folder. See `files/EXTERNAL_DATA.md` for the sources, programme IDs and terms.

| Data | ESO programmes | Dates | Use |
| --- | --- | --- | --- |
| GRAVITY single-field, medium resolution, calibrated OIFITS (ATs), reduction of 2026-10-28 (pipeline 1.9.7) | 108.222E, 110.246X | 2022-03-01, 2023-04-20, 2023-05-18, 2024-01-13, 2024-02-03/04/05, 2024-07-04 | closure phases, V2, differential phases |
| GRAVITY older reduction (2025-12-31 and 2026-03-04 products) | same | same, and 2023-01-20 (high resolution) | robustness test; 2023-01-20 used as an out-of-sample test |
| FEROS 1D spectra (R = 48,000) | 096.A-9039, 0102.A-9010, 0104.A-9001, 0106.A-9009, 0111.A-9002, 115.28JD | 2015-10 to 2025-04 (17) | velocities |
| ESPRESSO 1D spectra (R = 140,000) | 113.26KE, 115.281R | 2024-05 to 2025-06 (6) | velocities |
| Photometric ephemeris of the eclipsing pair | campaign bundle d86cdb9d (`p_best_posterior_max.json`) | 1990-2026 | inner orbit phase, e, omega |
| Gaia DR3 gaia_source (source 5242187050013731200) | VizieR I/355 (CfA mirror) | 2014-2017 | parallax, RUWE, excess noise (values quoted only) |

## Method

### Interferometry (`gravload.py`, `gravfit.py`, `widegrid.py`, `gravfit2.py`, `gravfit_fixf.py`)

We used the science-channel (SC) closure phases and squared visibilities. We removed the Br-gamma (2.155-2.180 um) and He I 2.058 um regions. We added systematic floors of 0.3 deg (closure phase) and 0.02 (V2) in quadrature. The model has point sources: a reference source at the origin, a close companion (x1, y1, f1) and a wide companion (x2, y2, f2). The V2 has one free scale per file, because the V2 calibration of the two ESO reductions differs by up to 25 percent. Steps:

1. Closure-phase grid search for one companion within 40 mas, then least squares.
2. A linearised closure-phase grid search for a faint companion within 150 mas (0.5-mas steps). This search found the wide companion at the same position in 12 of 15 searched files; in the other three the close companion (2022, long baselines) or noise dominated it. The joint fit of step 3 then finds the wide companion at 107-110 mas and position angle 125-126.5 deg in all 16 files.
3. A joint fit of both companions (grid for the close companion with the wide one fixed, then least squares of all parameters).
4. A final fit with the close flux ratio fixed at 0.54, the median of the well-constrained epochs. This removes the strong correlation of separation and flux ratio at the epochs with baselines below 100 m. We list all local minima. At each epoch we keep the solution whose position agrees with the Br-gamma test (in all cases this is also the lowest-chi2 solution).

### Br-gamma photocentre (`brg_shift.py`)

For each baseline we removed a linear function of wavenumber from the differential phase, fitted over the continuum. For each channel we solved for the photocentre offset (dx, dy) from all baselines. We compared the mean offset in the line core (2.1635-2.169 um) with the direction to the close companion.

### Velocities (`rv_measure.py`, `rv_checks.py`, `eb_gamma.py`)

- **Be star.** Fe II 4583, 5169, 5317 and 6456 disc-emission lines: cross-correlation against the mean profile of each line (velocity grid +-400 km/s). The Be-star velocity is the median of the four lines. The error is half their standard deviation. A fitted jitter term is added.
- **H-alpha wing bisector** at 1.3, 1.6 and 2.0 times the continuum, as an independent check.
- **Zero point.** Gaussian fit to the interstellar K I 7699 line.
- **Eclipsing pair.** A global two-component Gaussian model of He II 4541 and 5411 with the photometric ephemeris, one systemic velocity per season (mass ratio free, or fixed at 15/18).

### Orbit (`orbitfit.py`, `orbitgrid.py`, `orbitrefine.py`, `orbitmcmc.py`, `summarise.py`)

The relative orbit of the pair around the Be star uses Campbell elements (x = East, y = North). The Be-star velocity is gamma - K [cos(w + nu) + e cos w]. The wide-companion position relative to the Be star is c + v (t - t0) + B r(t), where r(t) is the relative orbit. Thus B is the reflex of the Be star around the Be + pair centre of mass. First we searched a grid in P (100-4000 d, 700 values), e (31 values) and the time of periastron (72 values). For each grid point the astrometry is linear in the Thiele-Innes constants, the wide track is linear in its five parameters, and the velocity is linear in three parameters. Then we refined the best grid point by least squares with 40 random starts. Last, we sampled the posterior with emcee (48 walkers, 6000 steps, first 3000 removed; autocorrelation 180-590 steps). The error floors of the astrometry, the wide track and the velocities are free parameters.

Derived quantities: a(AU) = K P sqrt(1 - e^2) / (2 pi sin i B); parallax = a(mas)/a(AU); M = a(AU)^3/P^2; m(pair) = B M.

### Dynamics (`nbody_drift.py`, `nbody_bmax.py`)

We used REBOUND (IAS15) integrations of three point masses: the two stars of the pair (masses 18:15, P1 = 17.8007 d, e1 = 0.268, sky inclination 90 deg at 2000.0) and the Be star on the measured outer orbit (least-squares solution). The wide companion is too far away to change the drift. We scanned the unknown inner node (0-355 deg, steps of 5 deg) and the inner argument of periastron (photometric value and +-40 deg), for B = 0.55-0.95. For each run we fitted the slope of the sky inclination of the pair from 2000 to 2026. Runs with |slope| within 0.03 deg/yr of 0.325 deg/yr were integrated to 2400, to find the next time with |i - 90 deg| < 8.6 deg (the eclipse limit of d86cdb9d).

## Results

### 1. Interferometric astrometry (Figures 1 and 5; `files/data/astrometry.csv`)

Table 1. Position of the eclipsing pair relative to the Be star (close flux ratio fixed at 0.54). The formal errors are smaller than the fitted floor of 0.087 mas. Delta chi2(alt) is the chi2 difference to the next local minimum.

| Date | Separation (mas) | PA (deg) | Reduced chi2 | Delta chi2 (alt) | Br-gamma cosine |
| --- | --- | --- | --- | --- | --- |
| 2022-03-01 | 1.637 | 303.1 | 1.61 | 307,877 | -1.00 |
| 2023-04-20 | 1.311 | 350.6 | 1.43 | 6,516 | -1.00 |
| 2023-05-18 | 0.498 | 17.1 | 1.22 | 13 | -1.00 |
| 2024-01-13 | 1.593 | 170.5 | 0.94 | 1,313 | -1.00 |
| 2024-02-03 | 1.401 | 175.5 | 1.18 | - | -1.00 |
| 2024-02-04 | 1.378 | 178.3 | 1.12 | 22,108 | -1.00 |
| 2024-02-05 | 1.384 | 178.1 | 1.21 | 561 | -0.99 |
| 2024-07-04 | 1.276 | 293.0 | 1.06 | - | -1.00 |

The wide companion is at 107.0-109.9 mas and position angle 125.3-126.5 deg at all epochs. Its K-band flux ratio is 0.04-0.07 (about 3 mag fainter than the Be star). The Br-gamma photocentre shift is 0.035-0.10 mas.

**Out-of-sample test.** The epoch 2023-01-20 was not used in any orbit fit. Its data are only in the older ESO reduction, in high spectral resolution, with fewer baselines. Before we fitted these data, the posterior orbit predicted a separation of 2.71 +- 0.07 mas at PA 335.9 +- 1.5 deg. The fit with the close flux ratio fixed at 0.54 gives its lowest chi2 at 2.64 mas, PA 335.8 deg (file ADP.2026-03-04T19:28:17.178; next minimum, the mirror position, Delta chi2 = 7,866). The second file of that night, which lacks three baselines, gives 2.98 mas, PA 338.5 deg. Both agree with the prediction to 0.07 and 0.27 mas (`files/data/gravity_fits/fixf_test_*.json`).

### 2. Velocities (Figure 2; `files/data/rv_raw.csv`, `files/data/rv_be.csv`)

Table 5. Be-star velocity amplitude from each tracer, with the orbit shape (P, T, e, omega) fixed at the least-squares joint orbit (`files/data/rv_checks.json`).

| Tracer | K (km/s) | rms (km/s) |
| --- | --- | --- |
| Fe II 4583 | 54.9 +- 1.8 | 5.2 |
| Fe II 5169 | 56.0 +- 1.1 | 3.3 |
| Fe II 5317 | 56.4 +- 0.8 | 2.3 |
| Fe II 6456 | 59.4 +- 1.0 | 2.9 |
| Fe II 5018 (blended with He I 5016) | 46.7 +- 3.2 | 9.4 |
| Fe II 6516 (weak) | 39.6 +- 8.4 | 24.9 |
| H-alpha bisector at 1.3 / 1.6 / 2.0 x continuum | 67.6 / 62.0 / 61.4 | 4.1 / 3.2 / 3.4 |

The four clean Fe II lines agree within 4.5 km/s. The H-alpha wings give a larger K (61-68 km/s); the outer disc and line asymmetries can change the bisector. The amplitude used in the orbit (58.1 km/s, median of the four clean Fe II lines) lies between them. The interstellar K I line gives 0.2 +- 1.7 km/s (FEROS, 17 spectra) and 0.8 +- 0.5 km/s (ESPRESSO, 6 spectra). Thus the wavelength scales of the two instruments agree to about 1 km/s.

The velocity curve does not depend on one season. When we remove any one of the 8 observing seasons, the best velocity-only period is 889-900 d.

Joint-fit residuals: velocity rms 2.0 km/s (largest 5.7 km/s, the single 2015 spectrum); pair astrometry rms 0.06 mas (East) and 0.09 mas (North), largest 0.22 mas at 2023-05-18 (separation 0.5 mas, the hardest epoch); wide-companion track rms 0.055 mas.

### 3. Orbit (Figure 3; `files/data/orbit_summary.json`)

Table 2. Joint orbit (posterior median and 68 percent interval). omega is for the pair relative to the Be star.

| Parameter | Value |
| --- | --- |
| P | 890.5 +- 0.7 d (2.438 yr) |
| Time of periastron | MJD 60142.8 +- 3.3 (2023-08-14) |
| e | 0.344 +- 0.008 |
| i | 77.4 +- 0.6 deg |
| Omega (node, East of North) | 153.4 +- 1.2 deg |
| omega | 303.5 +- 1.2 deg |
| a | 2.74 +- 0.08 mas |
| K(Be) | 58.1 +- 0.7 km/s |
| Mass function f(m) | 15.0 +- 0.6 solar masses |
| a(AU) x B | 4.57 +- 0.06 AU |
| Parallax / B | 0.598 +- 0.021 mas |
| m(pair) x B^2 | 16.1 +- 0.6 solar masses |
| B from the wide-companion reflex | 0.905 +- 0.033 |
| Fitted floors: astrometry, wide track, velocity jitter | 0.087 mas, 0.072 mas, 0.25 (+0.56/-0.17) km/s |

The velocity-only scan has a second minimum at twice the period (4.9 yr), with Delta chi2 = 15. The astrometry rejects it (Figure 3).

### 4. Mass fraction, masses and distance (Figure 4; `files/data/nbody_bmax.csv`, `files/data/bprofile.csv`)

Table 3. Masses and distance for a given B (68 percent intervals from the orbit posterior).

| B | m(pair) | m(Be) | Distance (kpc) | K(pair) (km/s) | Largest drift (deg/yr) |
| --- | --- | --- | --- | --- | --- |
| 0.60 | 44.7 +- 1.8 | 29.8 +- 1.2 | 2.79 +- 0.10 | 38.7 | 0.83 |
| 0.65 | 38.1 +- 1.5 | 20.5 +- 0.8 | 2.57 +- 0.09 | 31.3 | 0.70 |
| 0.70 | 32.9 +- 1.3 | 14.1 +- 0.6 | 2.39 +- 0.09 | 24.9 | 0.59 |
| 0.71 (2.35 kpc) | 31.9 +- 1.3 | 13.0 +- 0.5 | 2.35 | 23.7 | 0.56 |
| 0.75 | 28.6 +- 1.1 | 9.5 +- 0.4 | 2.23 +- 0.08 | 19.4 | 0.48 |
| 0.80 | 25.2 +- 1.0 | 6.3 +- 0.3 | 2.09 +- 0.08 | 14.5 | 0.37 |
| 0.828 (drift limit) | 23.5 +- 0.9 | 4.9 +- 0.2 | 2.02 +- 0.07 | 12.1 | 0.32 |
| 0.905 (wide reflex) | 19.7 +- 0.8 | 2.1 +- 0.1 | 1.85 +- 0.07 | 6.1 | 0.18 |

The largest drift is over all inner nodes and the three inner omega values. It uses the least-squares orbit (e = 0.366). The rate depends on B, P and e, but not on the total mass. The drift limit B <= 0.828 uses the lower 68 percent edge of the measured rate (0.316 deg/yr). For B = 0.65 and 0.75, the drift-consistent runs have mutual inclinations from 15 to 160 deg. The next eclipse season starts between 2065 and 2253 (B = 0.65) or between 2099 and 2376 (B = 0.75).

**Systemic velocity of the eclipsing pair (He II).** The global two-component He II model (mass ratio fixed at 15/18) gives K1 = 145 +- 3 km/s and seasonal systemic velocities from -31 to +52 km/s, but with reduced chi2 = 10 (`files/data/eb_gamma_q083.json`). These values do not follow the measured orbit for any B. With a free amplitude the best fit has K = 5.5 km/s, and chi2 = 557-753 for 8 seasons for all B from 0.6 to 0.9 (`files/data/bprofile.csv`). The highest values come from the ESPRESSO seasons. We conclude that blends of the two stars, the Be-star spectrum and instrument differences dominate these numbers. They give no information on B.

### 5. Predictions (`files/data/orbit_summary.json`)

Table 4. Predicted position of the pair relative to the Be star and Be-star velocity relative to its systemic velocity.

| Epoch | Separation (mas) | PA (deg) | V(Be) - gamma (km/s) |
| --- | --- | --- | --- |
| 2027.00 | 1.35 +- 0.06 | 300 +- 2 | +7.0 +- 0.6 |
| 2027.25 | 2.32 +- 0.08 | 317 +- 1 | +24.3 +- 0.6 |
| 2027.50 | 2.99 +- 0.08 | 325 +- 1 | +37.9 +- 0.6 |
| 2027.75 | 3.11 +- 0.08 | 331 +- 1 | +46.2 +- 0.5 |
| 2028.00 | 2.41 +- 0.07 | 338 +- 1 | +42.8 +- 0.7 |
| 2028.25 | 0.70 +- 0.06 | 9 +- 5 | +5.8 +- 2.1 |
| 2028.50 | 1.60 +- 0.08 | 146 +- 1 | -61.1 +- 1.3 |
| 2028.75 | 2.05 +- 0.05 | 161 +- 1 | -60.9 +- 1.5 |
| 2029.00 | 1.30 +- 0.04 | 181 +- 1 | -33.6 +- 1.2 |

The systemic velocity of the eclipsing pair must change with semi-amplitude K(pair) = 58.1 (1 - B)/B km/s: 12-31 km/s for B = 0.65-0.83. A disentangling of the pair spectrum over one outer orbit can measure B directly. This removes the main remaining uncertainty.

## Figures

- Figure 1 (`files/figures/fig1_gravity_orbit.png`): GRAVITY positions of the pair relative to the Be star with the orbit, Br-gamma shifts, the held-out 2023-01-20 epoch, and the wide-companion reflex.
- Figure 2 (`files/figures/fig2_be_velocity.png`): Be-star velocities (Fe II, H-alpha) and the interstellar K I line, with the orbit and residuals.
- Figure 3 (`files/figures/fig3_period_scan.png`): chi2 against outer period for astrometry only, velocities only, and all data.
- Figure 4 (`files/figures/fig4_mass_fraction.png`): largest drift against B (N-body), and masses and distance against B.
- Figure 5 (`files/figures/fig5_closure_phases_2022.png`): closure phases of 2022-03-01 with the three-source model.

## Limitations

- **Mass fraction.** The orbit fixes P, e, i, a and K(Be), but not B. The two direct B measurements disagree: the wide-companion reflex (0.905 +- 0.033) against the drift requirement (B <= 0.83) and the light ratio. We do not know which assumption fails. Possible causes are a GRAVITY systematic for a source 108 mas off axis, an unresolved companion of the Be star or of the wide star, or a dynamical driver other than the Be star (for example, a misaligned stellar spin). Our He II systemic velocities do not follow the orbit at any B (chi2 = 557 for 8 seasons), so line blending or instrument offsets dominate them. They give no constraint on B.
- **Drift test assumptions.** Point masses, Newtonian dynamics, no tides or spins, inner mass ratio 18:15, e1 = 0.268, and the photometric drift of d86cdb9d (which is itself a model result). The limit B <= 0.83 uses the least-squares orbit, not the full posterior; the e2 difference changes the rate by about 3 percent.
- **Be-star velocities.** These come from disc emission lines. Disc asymmetry (V/R changes) can shift them. The four Fe II lines and the H-alpha wings agree, and the fit residuals are small (rms 2.0 km/s), but a slow disc change can bias K by a few km/s.
- **Astrometry.** The close-companion flux ratio is fixed at 0.54 in the final fits. The GRAVITY phase sign convention can rotate all positions by 180 deg; this changes Omega by 180 deg but none of the other results. One epoch (2023-05-18) has only Delta chi2 = 13 between the two mirror solutions; the Br-gamma test selects one of them. The ESO reductions of 2025-12/2026-03 give noisier and in some epochs different close-companion positions.
- **MCMC.** The autocorrelation times are 180-590 steps for 3000 kept steps (about 250-800 effective samples). The intervals are approximate.
- **Distance.** The Carina-complex distance used in item 8 of the summary is an assumption about membership.
- **Shared host.** The Dell host had a load average near 150 during this work. This did not change results but limited the number of random starts and MCMC steps.

## Reproduction

1. `bash files/code/fetch_eso.sh files/code/p3list.txt SCRATCH/dl` (downloads about 0.8 GB into a scratch folder; compare with `files/data/input_hashes_eso.txt`).
2. Follow `files/code/RUN.md` in order. The scripts write into the scratch folder. Python 3.12 with numpy 2.5, scipy 1.18, pandas 3.1, astropy 8.0, matplotlib 3.11, emcee 3.1.6 and rebound 5.2.2.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-astronomy-787220e01617, topic astronomy, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Prior work used: the campaign bundles cited in `sci.json`, mainly d86cdb9d (ephemeris, drift, eclipse limit) and the bound studies.
- ESO acknowledgement: based on observations collected at the European Organisation for Astronomical Research in the Southern Hemisphere under the ESO programmes listed above, and on data products from the ESO Science Archive Facility.
