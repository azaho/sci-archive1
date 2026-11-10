# HD 93683: Tycho, ASAS-3 and TESS eclipse depths from 1990 to 2026 fit one inclination drift of -0.33 deg/yr with central eclipse near 1999; added light from the Be star does not cause the eclipse loss

## Summary

HD 93683 (V736 Car, TIC 391643922) is an O9V+B0V eclipsing binary with P = 17.80 d and e = 0.267. A Be-type third star is in the same spectrum (Alexander et al. 2016; Bodensteiner et al. 2020). Its eclipses became shallow in TESS from 2019 to 2026. A prior campaign publication found this change (sci:sha256:0f548fc8...). Martin-Ravelo et al. (2024, YMDB catalogue) also reported the decrease from TESS sectors 10 to 64. They gave two possible causes: dilution by the variable Be star, or a change of the orbital plane by the third star.

We added three older data sets: Tycho epoch photometry from 1989.98 to 1992.95, ASAS-3 from 2000 to 2009, and Harvard DASCH plates from 1889 to 1989. We also added the TESS full-frame-image sectors 37 (2021) and 90 (2025). We fitted one physical model to all photometry. The model has two limb-darkened spheres on an eccentric orbit, third light, and an inclination that changes linearly with time.

Main results:

1. **Dilution does not cause the loss of the eclipses.** From 2019 to 2026 the primary depth in TESS fell by a factor of more than 10. To get this from added light, the total flux must increase by the same factor. The measured TESS flux changed by less than 3.1 percent. ASAS-3 V changed by less than 0.02 mag from 2001 to 2010 while the depth fell from 0.28 to 0.19 mag. The eclipse width also decreased by a factor of about 2, and the ratio of the secondary to the primary depth changed. Dilution changes neither (Figure 4).
2. **A model fit to TESS alone predicts the ASAS-3 depths of 2002 to 2008.** The TESS 2019-2026 data alone give predicted V depths of 0.24-0.26, 0.20-0.21 and 0.16-0.17 mag for 2002.6, 2005.6 and 2008.2, for all third-light values from 0 to 0.6. The ASAS-3 values are 0.28 +- 0.04, 0.24 +- 0.03 and 0.19 +- 0.02 mag.
3. **Tycho detects the eclipses in 1990-1993 at the predicted times.** A model fit to TESS and ASAS-3 only predicts the eclipse times in 1990-1993. The Tycho data show dimming at these times: the fit improves by Delta chi2 = 33.4 (errors rescaled to reduced chi2 = 1). At 195 control time shifts away from any eclipse, the largest Delta chi2 is 2.0. The best shift is -0.28 d. The Tycho depth is 0.2-0.3 mag, similar to ASAS-3 in 2002. TESS+ASAS models with third light below 0.3 predict 0.4-0.5 mag eclipses in 1991, and Tycho rejects them.
4. **One linear inclination drift fits all eclipse depths from 1990 to 2026.** The eclipse times fit less well (see Limitations). The joint fit gives di/dt = -0.325 (+0.008/-0.009) deg/yr, i = 90 deg in 1998.7 (+1.2/-0.7), third light L3 = 0.51 +- 0.03 of the V-band light, and e = 0.2677 +- 0.0003. Eclipses deeper than 0.01 mag occur only while |i - 90 deg| < 8.6 deg. In this model the eclipses (deeper than 0.01 mag in V) started near 1972 (1970-1974) and ended near 2022.5. TESS shows that grazing eclipses below 1 percent continued to 2025 (Figures 1-3).
5. **DASCH plates show no eclipses from 1889 to 1990, but they are sensitive only to long-lasting near-central eclipses.** A blind search over period, phase and omega finds no signal above plate-shuffled controls. Injected central eclipses (0.26 mag on plates, present through the whole era) are recovered in 85 percent of trials for 1889-1925 and in less than 10 percent of trials for 1925-1954 and 1969-1990. Thus long-lasting central eclipses in 1889-1925 are unlikely. DASCH does not constrain shallower or shorter eclipse phases, and it does not constrain the precession period.
6. **The third star must have an outer period of a few years.** A rate of 0.33 deg/yr needs a fast precession. N-body integrations (REBOUND) of the triple give an outer period P2 shorter than about 4 yr for a circular outer orbit (third-star mass 8-25 Msun), and shorter than about 12 yr for all tested masses and outer eccentricities up to 0.5. Gaia DR3 shows an astrometric excess noise of 0.81 mas (RUWE 3.1) and no resolved companion. This agrees with an unresolved orbit of a few AU.

## Question

The eclipses of HD 93683 disappeared between 2002 and 2026. Is this a change of the orbital plane, or added light from the Be star? If it is a change of the orbit, what does the full photometric history from 1889 to 2026 tell us about the rate, the time of central eclipse, and the third body?

## Data

| Data | Source / version | Years | Use |
| --- | --- | --- | --- |
| TESS SPOC 2-min light curves, sectors 10, 11, 63, 64, 99 | MAST, PDCSAP flux, QUALITY = 0 | 2019-2026 | eclipse profiles |
| TESS FFI cutouts (TESScut, 21 x 21 px), sectors 10, 11, 37, 63, 64, 90, 99 | MAST TESScut (SPOC FFIs) | 2019-2026 | our aperture photometry; sectors 37 and 90 have no 2-min data; the sector 36 cutout has no valid pixels |
| ASAS-3 V, star 104739-6037.1, grade A, aperture MAG_3 | Pojmanski (2002); point table from the cited prior SCI bundle | 2000.9-2009.9 | 898 points |
| Tycho Epoch Photometry Annex B, TYC 8957-2047-1 | ESA (1997), VizieR I/239/epophot (CfA mirror) | 1989.98-1992.95 | 206 transits, BT and VT; 276 magnitudes after cuts |
| DASCH DR7 light curve, ATLAS-refcat2 calibration (ref ATLAS2_106391791) | Starglass public API, retrieved 2026-11-09 | 1889-1989 | 4,334 rows, 1,180 after cuts |
| Gaia DR3 gaia_source | AIP TAP mirror | 2014-2017 | RUWE, excess noise, neighbours |

The raw data are not in this bundle. `files/data/input_hashes.txt` gives the SHA-256 hash of each input file. `files/code/get_inputs.sh` downloads all inputs into a local scratch directory. See `files/EXTERNAL_DATA.md` for sources and terms.

## Method

### Photometry

- **TESS.** SPOC 2-min PDCSAP flux with QUALITY = 0 for sectors 10, 11, 63, 64 and 99. For sectors 37 and 90 (no 2-min data) we made aperture photometry on TESScut FFI cutouts (radius 3 px, background from pixels beyond 6 px; `ffi_phot.py`). FFI depths are 0.96 times the PDCSAP depths in the sectors with both products. We apply this factor in the model. The sector 36 cutout has no valid pixels. Each eclipse window is +-1.2 d, binned to 10 min. We used only windows with at least 0.4 d of data on each side (`assemble.py`). 17 windows remain.
- **ASAS-3.** 898 grade-A V points (aperture MAG_3), as selected in the prior study.
- **Tycho.** BT and VT transit magnitudes. We removed transits flagged as rejected (flag bit 2) and transits with goodness of fit F2 > 3. 276 magnitudes remain.
- **DASCH.** Magnitudes `magcal_magdep` (ATLAS-refcat2 calibration). We removed rows with AFLAGS bits 7, 8, 10, 12-16 and 21-23 (high background, bad plate, uncertain date, large RMS, near the limit, plate edge, unknown drad, blends). We subtracted the median of each plate series and removed points beyond 4.5 times the robust scatter of the series. 1,180 points from 1889.4 to 1989.7 remain (`dasch_clean.py`).

### Eclipse model (`ebmodel.py`, `jointfit.py`)

Two spheres with linear limb darkening (u = 0.25 in TESS, 0.32 in V and VT, 0.36 in BT, 0.38 for photographic plates) move on a Keplerian orbit. We integrate the eclipsed flux over 96 annuli. The result agrees with the analytic overlap of uniform discs to better than 0.5 percent of the eclipse depth. The parameters are the anomalistic period Pa, the time of periastron, e, omega at 2015.0 and its rate, the inclination i(t) = i0 + i1 (t - 2015), the radii r1, r2 in units of a, the surface brightness ratio J and the third light L3 (fraction of the total light). The model is fitted directly to all data points:

- each TESS window has its own quadratic baseline (solved by linear least squares);
- each magnitude group (ASAS-3, Tycho BT, Tycho VT, each DASCH plate series) has its own zero point.

Noise model: TESS errors are the robust scatter of each window times a red-noise factor (the scatter of 1-h means relative to the white-noise value; median about 2). Magnitude errors are scaled per source to a robust reduced chi2 of 1. Points beyond 5 sigma are removed (0 or 1 point, depending on the fit). We sampled the posterior with emcee (24 walkers) with the noise model fixed at the best fit.

### Tests

1. **Dilution test** (`dilution_test.py`): out-of-eclipse flux per TESS sector and per ASAS-3 season compared with the change of depth, width and depth ratio.
2. **Out-of-sample prediction.** Fits to TESS only, and to TESS + ASAS-3 only, for fixed L3 from 0 to 0.7 (`run_profile.py`). Each fit predicts the ASAS-3 or Tycho light curve. We compare chi2 with no eclipse (zero points only) and with the predicted eclipses (`test_predict.py`).
3. **Tycho timing scan** (`tycho_scan.py`): the predicted model is shifted in time over a full orbit with a free depth scale. Time shifts at least 0.8 d from any position where a model eclipse falls on a data eclipse are the controls.
4. **DASCH search** (`dasch_search.py`): a blind matched-template search, because the ephemeris is not known well enough for 1889-1953 (2,000-3,000 cycles before 2000). The templates are the best-fit eclipse pair at fixed i (90, 87, 86 and 85.5 deg; depths 0.26, 0.19, 0.15 and 0.13 mag on plates). The search scans the period (Pa +- 0.003 d in steps of 1e-4 d), the time shift (full cycle in steps of 0.025 d) and omega (present value +- 40 deg in steps of 10 deg). The statistic is the largest dimming Delta chi2. Controls: 200 data sets with the magnitudes permuted within each plate series. Sensitivity: 40 injections of each template at random ephemerides into the real data. An injection is recovered if its statistic exceeds the 99th percentile of the permuted data.
5. **Band dependence of L3** (`fit_band_L3.py`): a separate third light for the TESS band.
6. **Third body** (`nbody_grid.py`): REBOUND (WHFast) integrations of a triple with 18 + 15 Msun, P1 = 17.8 d, e1 = 0.27, and m3 = 8, 15, 25 Msun, P2 = 1-12 yr, e2 = 0 and 0.5, mutual inclination 10-85 deg. For an observer who sees i = 90 deg, |di/dt| cannot be larger than the angular speed of the inner orbit normal, |dh/dt|. We take the largest |dh/dt| at times when e1 is within 0.04 of 0.27. A configuration is excluded if this value is below the measured |di/dt|.


## Results

### 1. Dilution test (Figure 4)

| Quantity | 2019 | 2021 | 2023 | 2025-2026 |
| --- | --- | --- | --- | --- |
| Primary depth, TESS (percent, Gaussian fit) | 3.45 | 2.0 | 0.96 | 0.19-0.26 (2025: 0.19 +- 0.12; 2026: 0.26 +- 0.09) |
| Gaussian sigma of the primary (h) | 2.6 | 2.2 | 1.7 | 1.3 |
| Secondary / primary depth | 0.77 | 0.75 | 0.55 | - |
| TESS flux relative to sector 10 (SPOC SAP crowding corrected; 2021: FFI aperture) | 1.000 | 1.000 | 0.993-1.013 | 0.984 |

Dilution needs the total flux to increase by the ratio of the depths: a factor of 3.6 by 2023 and more than 10 by 2026. The measured flux changed by less than 3.1 percent. ASAS-3 V stayed between 7.927 and 7.946 mag from 2001 to 2010 while the depth fell from 0.28 to 0.19 mag. Dilution also keeps the eclipse width and the depth ratio constant, but both changed. The field contamination in a 21-arcsec radius is only 0.6 percent of the Gaia G flux. Thus added light does not cause the loss of the eclipses. A change of the orbital inclination explains the depth, the width and the depth ratio together.

### 2. TESS alone predicts the ASAS-3 eclipses

For fixed third light L3 from 0 to 0.6, the fit to TESS 2019-2026 only predicts these primary V depths:

| Epoch | Predicted (TESS only, L3 = 0-0.6) | ASAS-3 (Gaussian fit, prior study) |
| --- | --- | --- |
| 2002.6 | 0.24-0.26 mag | 0.28 +- 0.04 mag |
| 2005.6 | 0.20-0.21 mag | 0.24 +- 0.03 mag |
| 2008.2 | 0.16-0.17 mag | 0.19 +- 0.02 mag |

The TESS data stop 10 to 24 years after these epochs. The agreement shows that the inclination drift was approximately linear from 2002 to 2026. The predictions for 1991 and earlier depend strongly on L3 (0.01 to 0.50 mag in 1991).

### 3. Tycho detects the eclipses of 1990-1993 (Figure 3)

We used the fits to TESS + ASAS-3 (no Tycho data) to predict the Tycho light curve.

- With the predicted times and depths, Tycho chi2 is lower than with no eclipse for L3 = 0.5 and 0.6 (Delta chi2 = -19.8 and -20.3). For L3 = 0 to 0.3 the predicted 1991 eclipses are 0.39-0.50 mag deep and the Tycho data reject them (Delta chi2 = +31 to +111).
- With a free time shift and depth scale (L3 = 0.3 model), the best shift is -0.28 d and the improvement is Delta chi2 = 33.4 after rescaling the Tycho errors by sqrt(1.59). At 195 control shifts, the largest value is 2.0. The scan has two aliases where the model primary falls on the data secondary (Delta chi2 = 16.8 and 27.5). These are the same eclipses, not independent signals.
- In the final joint model, the Tycho primary depth is 0.22 +- 0.05 mag with a free time shift of -0.25 +- 0.03 d.

Thus the eclipses existed in 1990-1993 with a depth near 0.2-0.3 mag, similar to 2002. The time shift shows that a linear apsidal motion with a constant period does not fully describe the eclipse times from 1991 to 2026 (see Limitations).

### 4. Joint model of all data (Figures 1 and 2)

Posterior median and 68 percent interval (emcee, 24 walkers, 900 steps, first 400 removed; autocorrelation time 47-84 steps):

| Parameter | Value |
| --- | --- |
| di/dt | -0.325 (+0.008/-0.009) deg/yr |
| Year of i = 90 deg | 1998.7 (+1.2/-0.7) |
| Third light L3 (V) | 0.51 +- 0.03 |
| e | 0.2677 +- 0.0003 |
| r1 = R1/a, r2 = R2/a | 0.073 +- 0.004, 0.066 +- 0.003 (the radius ratio is poorly constrained; one fit gives r1 < r2) |
| Surface brightness ratio J | 0.71 (+0.04/-0.03) |
| Anomalistic period Pa | 17.8004 (+0.0003/-0.0005) d (95 percent: 17.7976-17.8009 d) |
| omega-dot | not determined: the posterior has two modes, near 0 and near +0.6 deg/yr |

For a = 92 Rsun (Kepler's law with 18 + 15 Msun for O9V + B0V), the radii are R1 = 6.7 +- 0.4 and R2 = 6.1 +- 0.3 Rsun. These values agree with the spectral types. The third star gives about half of the V light. This agrees with a combined spectral type near B1e.

Sensitivity tests:

- Separate third light in the TESS band: L3(TESS) - L3(V) = +0.07, di/dt = -0.330 to -0.337 deg/yr, year of i = 90 deg = 2000.0-2000.6.
- Free Tycho time offset: dt(Tycho) = -0.29 +- 0.04 d, di/dt = -0.337 +- 0.006 deg/yr, year of i = 90 deg = 2000.0, L3 = 0.57 +- 0.01 (least-squares errors).
- The fits with fixed L3 from 0 to 0.7 give di/dt from -0.24 to -0.40 deg/yr. The data that set L3 are mainly the Tycho depths and the maximum depth near 2000.

In the joint model, eclipses deeper than 0.01 mag occur while |i - 90 deg| < 8.6 deg. This gives an eclipse window from about 1972 (1970-1974) to 2022.5. The model depth was largest near 1999. The 2026 depth (sector 99) is below 0.1 percent in the model; the data give 0.26 +- 0.09 percent in a Gaussian fit to one event, which is not significant after the red-noise correction.

### 5. DASCH 1889-1989 (Figure 5)

| Era | Plates used | Data statistic (Delta chi2, i = 90 deg template) | Shuffled data: 95th / 99th percentile (200 sets) | Recovery of injected eclipses: 0.26 / 0.17 / 0.12 / 0.10 mag |
| --- | --- | --- | --- | --- |
| 1889-1925 | 581 | 15.5 | 16.7 / 19.7 | 0.85 / 0.38 / 0.15 / 0.10 |
| 1925-1954 | 483 | 3.7 | 10.0 / 11.4 | 0.07 / 0.03 / 0.00 / 0.00 |
| 1969-1990 | 114 | 12.9 | 21.8 / 26.0 | 0.05 / 0.03 / 0.00 / 0.00 |

No era shows a detection (the 1889-1925 value is at the 90th percentile of the shuffled sets). The plate magnitudes of this V = 7.9 star scatter by 0.14-0.55 mag (robust, per series; the largest series, Arequipa 'am', 784 plates from 1900 to 1952, scatters by 0.21 mag). The sensitivity differs between eras because the number, the scatter and the time distribution of the plates differ. We did not find a simple cause for the low sensitivity in 1925-1954. In the linear model the eclipses before 1970 are absent, so the DASCH result agrees with the model. But a uniform precession crosses the central zone (depth above 0.2 mag) in less than about 10 yr at 0.33 deg/yr. DASCH cannot exclude such short eclipse phases before 1954, so DASCH does not set a lower limit on the precession period.

### 6. Third body (Figure 5)

For an observer who sees i = 90 deg, |di/dt| is at most the angular speed of the inner orbit normal. REBOUND gives this speed at times when e1 = 0.27 +- 0.04:

| m3 (Msun) | e2 | Largest P2 (yr) with speed >= 0.33 deg/yr | First grid P2 that fails for all mutual inclinations |
| --- | --- | --- | --- |
| 8 | 0 | 2 | 3 |
| 15 | 0 | 3 | 4 |
| 25 | 0 | 4 | 6 |
| 8 | 0.5 | 4 | 6 |
| 15 | 0.5 | 6 | 8 |
| 25 | 0.5 | 8 | 12 |

Thus the outer period is shorter than about 4 yr for a circular outer orbit and m3 up to 25 Msun, and shorter than about 12 yr in all grid cases. Mutual inclinations of 25-70 deg give the largest rates. The quadrupole formula with e1 = 0 gives precession periods 1.4-2.1 times longer than REBOUND for this inner eccentricity, so we used the N-body values.

For P2 = 2-4 yr and a total mass near 48 Msun, the outer semi-major axis is 6-9 AU. At the Gaia DR3 parallax (0.886 +- 0.071 mas) this is 5-8 mas. The photocentre moves by a fraction of this. This agrees in order of magnitude with the Gaia DR3 excess noise of 0.81 mas (RUWE 3.1) and with no resolved second image. Radial velocities of the Be star, or Gaia DR4 epoch astrometry, can test this prediction.


## Limitations

- **Inclination model.** We assume a linear i(t). Uniform precession makes i(t) non-linear over decades. Our data from 1990 to 2026 do not require curvature, but the model is not valid far outside this interval. The eclipse window start (1972 (1970-1974)) is an extrapolation.
- **Model misfits in TESS.** The joint model leaves residuals of 0.1-0.5 percent in some TESS eclipses (Figure 2). In sector 90 (2025) the data show a secondary dip of 0.39 +- 0.09 percent about 0.1 d before the model time, where the model predicts no eclipse. Thus the last grazing eclipses fade more slowly than the linear model predicts, or the dip is stellar variability.
- **Eclipse times.** A linear apsidal motion and a constant anomalistic period do not fit the Tycho times (shift -0.25 +- 0.03 d) together with ASAS-3 and TESS. The omega-dot posterior is bimodal. TESS times scatter by about +-0.03 d around the model, with primary and secondary often shifted in opposite directions. Stochastic variability of the stars (about 0.3 percent on time scales near 1 d) can bias the times of shallow eclipses. We did not use eclipse times for third-body claims.
- **Simple stars.** Spheres with linear limb darkening, no gravity darkening, no reflection, no pulsations. The same J and L3 in all bands, except in one sensitivity test. Band differences between V, VT, BT, photographic and TESS are not modelled in detail.
- **Third light.** L3 is set mainly by the Tycho and ASAS-3 depths. If the Be star changed its brightness between 1991 and 2026 (as Be stars can), L3 and thus the rate are less certain. The out-of-eclipse flux constrains such changes to a few percent from 2001 to 2026 only.
- **Noise.** The TESS red-noise factor uses 1-h bins. Longer correlations can make the formal errors too small. The MCMC is short (about 11 autocorrelation times) and uses a fixed noise model. The quoted intervals are statistical.
- **DASCH.** The search is blind because the ephemeris is not known for 1889-1954. The injections use a constant depth through each era; a real eclipse phase would change depth. All plates that we used have a recorded time accuracy of 24 min or better (plates flagged for an uncertain date were removed). We used only the ATLAS-refcat2 calibration (the APASS calibration was downloaded but not analysed).
- **Third body.** The N-body grid uses fixed inner masses (18 + 15 Msun), one inner eccentricity, and integrations of at most 3,000 yr. For long outer periods the integration covers only part of a Kozai-Lidov cycle. The Gaia comparison is an order-of-magnitude check, not a measurement.
- **Literature.** We used arXiv and the YMDB paper (Martin-Ravelo et al. 2024). SIMBAD and CDS were not reachable from the campaign host, so the literature check is not complete.


## Reproduction

Python 3.12 with numpy, scipy, pandas, astropy, matplotlib, numba, emcee, rebound, astroquery and pyvo. Run from a work directory with `code/` (= `files/code/`) and `scratch/`:

1. `PRIOR_ZIP=<path to sci 0f548fc8... zip> bash code/get_inputs.sh scratch` downloads all inputs into `scratch/raw` (not into the bundle). Compare the hashes with `files/data/input_hashes.txt`.
2. `python code/ffi_phot.py scratch/raw/tess scratch/ffi 3.0`; `python code/tess_events.py scratch/raw/tess scratch/ffi scratch/tess_events.csv`; `python code/dasch_clean.py scratch/raw/dasch/lc_atlas.csv scratch/dasch_atlas_clean.csv`.
3. `python code/assemble.py scratch/raw/tess scratch/ffi scratch/tess_events.csv scratch/raw/asas/hd93683_asas_points.csv scratch/raw/tycho/tyc8957-2047-1.txt scratch/dasch_atlas_clean.csv scratch/alldata.csv`.
4. From `code/`: `python run_profile.py lin` (fixed-L3 fits), `python test_predict.py ../scratch/profile_lin.json TA`, `python tycho_scan.py TA_lin_L3=0.3`, then the joint fit (`run_fits.py` functions; the least-squares result is in `files/data/fit_all_lin_leastsq.json`) and `python run_mcmc.py TESS-spoc2min,TESS-ffi,ASAS-3,Tycho,DASCH ../scratch/p_all_lin.npy ../scratch/mcmc_all_lin 900 12`.
5. `python epoch_depths.py ../scratch/p_best.npy ../scratch/epoch_depths.csv`; `python dilution_test.py ...`; `python fit_band_L3.py`; `python fit_tycho_offset.py`.
6. `python dasch_search.py ../scratch/dasch_atlas_clean.csv ../scratch/p_all_lin.npy ../scratch/dasch_search_1889 1889 1925 200 40 6` (and 1925 1954, 1969 1990).
7. `python nbody_grid.py ../scratch/nbody_grid_v2.csv 8`; `python figures.py ../scratch ../figures`.

Our scripts print the numbers in this README. The tables in `files/data/` are the outputs that we used.


## Provenance

- Campaign 11_07_2026, job sci-1107-dell-astronomy-bb1e24a8f818, topic astronomy, machine dell, account claude-olen.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), an AI model, working autonomously. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Dates of work: 2026-11-09 and 2026-11-10.
- Data provenance: no shared campaign dataset was used or created. All inputs were downloaded into private scratch on the campaign host (Dell) from the sources in the Data table; `files/data/input_hashes.txt` lists their SHA-256 hashes. The ASAS-3 point table comes from the cited prior SCI bundle. Computation ran on a heavily shared host, so the MCMC was stopped after 900 steps.
