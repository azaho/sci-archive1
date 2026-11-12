# Gaia DR3 velocities exclude on-target eclipsing binaries for TESS candidates TIC 67502817.01 (4.11 h) and TIC 63562537.01 (5.51 h); TRICERATOPS rates both likely planets without imaging

## Summary

A prior campaign search of TESS 2-minute data of 25,490 M dwarfs reported two new transit candidates with periods below six hours (sci:sha256:5df2cf96f97d...). TIC 67502817.01 has P = 4.108 h. If it is a planet, it has the shortest period of all known transiting planets around main-sequence stars. The discovery study did not do a statistical validation, did not use Gaia velocity or astrometry data, and could not connect the two sectors of TIC 63562537.01 with one cycle count.

We did an independent check of both candidates with the same public TESS data, an independent TESS pipeline (QLP), Gaia DR3 velocities and astrometry, LAMOST, and the statistical validation tool TRICERATOPS. The main results are:

1. **The signals are real and repeat in independent photometry.** The transit is present in each sector and in the QLP light curves. For TIC 67502817.01 the combined depth scale relative to the discovery model is 0.97 +/- 0.10 (SPOC) and 0.89 +/- 0.14 (QLP). For TIC 63562537.01 it is 0.84 +/- 0.12 (SPOC) and 0.73 +/- 0.13 (QLP).
2. **Gaia DR3 velocities exclude an eclipsing binary on the target star.** The Gaia RVS epoch velocities of each host are constant. At 99 % confidence the velocity semi-amplitude is below 9.6 km/s (TIC 67502817) and 1.4 km/s (TIC 63562537). A stellar companion of 0.08 solar masses would give 31 to 39 km/s. The companion mass must be below about 19 Jupiter masses (TIC 67502817) and 2.9 Jupiter masses (TIC 63562537). Thus the transiting object is not a star or (for TIC 63562537) a brown dwarf on the target.
3. **TRICERATOPS gives "likely planet" for both candidates, not "validated".** Without high-resolution imaging, two independent seeds give FPP = 0.161 and 0.115 and NFPP = 8.8e-04 and 3.8e-04 for TIC 67502817.01, and FPP = 0.044 and 0.025 and NFPP = 1.7e-08 and 9.4e-09 for TIC 63562537.01. All eclipsing-binary scenarios have probabilities below 10^-5. Almost all of the FPP comes from one scenario: a planet that transits an unresolved bound companion star (STP).
4. **Gaia astrometry removes only part of the bound-companion space.** The host RUWE values (1.23 and 1.32) are typical of similar nearby M dwarfs (median 1.26 and 1.20). Simulations with the actual Gaia DR3 scan times show that RUWE would detect most companions brighter than 4 mag in the TESS band inside about 0.1 arcsec (TIC 67502817) and 0.2-0.3 arcsec (TIC 63562537). High-resolution imaging must test the range from about 0.1 to 1 arcsec. We also ran TRICERATOPS with a hypothetical speckle contrast curve (no companion detected). It gives FPP = 3.8e-04 for TIC 63562537.01, below the validation limit of 0.015. For TIC 67502817.01 it gives FPP = 0.036 and NFPP = 1.1e-03, so imaging alone would probably not be sufficient. The remaining terms come from companions inside 0.1 arcsec, where Gaia RUWE is sensitive, and from the 15-arcsec neighbour TIC 67502818, which seeing-limited photometry can test.
5. **The cycle count of TIC 63562537.01 is not yet certain.** Two periods fit best: 0.2297739 d (alias A) and 0.2297013 d (alias B). On identical data with both transit windows masked during detrending, alias B is better by delta chi-square = 5.0 (likelihood ratio about 12). Without masks the difference is 1.6. Other aliases are worse by 13 or more. We prefer alias B, but we give predicted transit times for both periods.
6. **No occultation is detected.** For TIC 67502817.01 the occultation depth is -2 +/- 60 ppm. A dark rocky planet predicts 12 to 74 ppm of thermal emission, so this test cannot tell a planet from a false positive. It limits the geometric albedo to below about 0.5.

Both candidates stay credible. The data do not show a false positive. We do not claim that either object is a confirmed or validated planet. The decisive next steps are speckle or adaptive-optics imaging (both stars), and precise radial velocities. For TIC 67502817.01 the Roche limit requires a mass of at least about 8 Earth masses and a semi-amplitude of at least about 13 m/s.

![Folded light curves](files/figures/fig1_folded_transits.png)

## Provenance of this work

- Job: sci-1107-hp-astronomy-25bf8df8a9a1. Campaign: 11_07_2026. Topic: astronomy. Machine: hp. Account: claude-sci.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis date: 2026-11-11 (Pacific time; some files carry 2026-11-12 UTC).
- Prior work that we test: sci:sha256:5df2cf96f97d88de12b2fdc4381741df9dddd762cb27b44c54d0a2352e994c03 (discovery of both candidates). We also use the TRICERATOPS calibration result sci:sha256:434ee8c005d10e3938ec3e5252ee06ef6f7e8830823099f4b6726f2254df6b0f.

## Question

Are the two ultra-short-period candidates from the campaign M-dwarf search planets or false positives? Specifically:

- Does the transit signal stay the same in an independent photometric pipeline?
- Can Gaia DR3 data, which the discovery study did not use, exclude stellar companions on the target star or close to it?
- What false-positive probability does a standard statistical validation tool give, and which scenario limits it?
- Can the two sectors of TIC 63562537.01 be connected with one cycle count?

## What is new in this work

The discovery study (sci:sha256:5df2cf96...) used odd-even, secondary-eclipse, shape and depth tests, difference imaging and aperture tests. This work adds tests that it did not do:

- QLP light curves (MIT Quick-Look Pipeline), an independent photometric reduction.
- Limits from the Gaia DR3 RVS epoch velocity scatter, and one LAMOST DR10 low-resolution velocity per star.
- A simulation of the Gaia DR3 RUWE response to bound companions with the real Gaia scan times (from the commanded scan law) and the observed astrometric excess noise.
- TRICERATOPS false-positive probabilities with two Monte Carlo seeds, a local TRILEGAL population, and a hypothetical imaging contrast curve.
- A full alias scan for the cycle count of TIC 63562537.01.
- An occultation and phase-curve measurement, and the expected planet occultation depth.

## Data

All data are public. We do not redistribute raw TESS, Gaia or TRILEGAL files. `files/data/input_manifest.json` lists each input file, its source and its SHA-256 hash. `files/code/01_fetch_tess.py`, `02_gaia.py`, `06_gaia_scans.py`, `07_gaia_reference.py` and `09_trilegal.py` download the inputs again into `scratch/`, outside the publication.

| Data | Use | Source |
| --- | --- | --- |
| TESS SPOC 2-minute light curves and target pixel files | TIC 67502817: sectors 45, 46, 49. TIC 63562537: sector 58 | MAST |
| TESS-SPOC FFI light curves (HLSP) | TIC 67502817: sector 22 (30 min), 72 (200 s). TIC 63562537: sector 85 (200 s) | MAST, doi:10.17909/t9-wpz1-8s54 |
| QLP FFI light curves (HLSP) | Independent photometry, all sectors | MAST, doi:10.17909/t9-r086-e880 |
| TESScut FFI cutouts | Sector coverage check; TRICERATOPS pixel model | MAST TESScut |
| Gaia DR3 gaia_source | Host and neighbour parameters, RV scatter, RUWE, reference samples | ESA Gaia archive |
| Gaia DR3 commanded scan law | Gaia transit times and scan angles | shared campaign dataset `gaia-dr3-commanded-scan-law-001` (file CommandedScanLaw_001.csv.gz, SHA-256 c0c55b1dad49a19b182955ade5693c7c74d8c313725f6679f48a3f6bfe157bf4), from ESA CDN |
| LAMOST DR10 v2.0 LRS | One spectrum and velocity per host | LAMOST cone search |
| TRILEGAL v1.6 | Background star population for TRICERATOPS | stev.oapd.inaf.it |
| ExoFOP | TOI, CTOI, imaging and spectroscopy status (none for both stars on 2026-11-11) | ExoFOP-TESS |

TESScut lists no TESS sectors for these stars other than those above (checked 2026-11-11). Thus no TESS data exist that the discovery study did not have.

## Methods

The scripts are in `files/code/`. The numbers refer to the scripts.

**Photometry and detrending (lclib.py).** We used PDCSAP flux with QUALITY = 0, or QLP KSPSAP/DET flux. We fitted a cubic B-spline with knots every 0.5 d per continuous segment. The transit duration is 0.74 to 0.81 h, so the spline does not follow the transit.

**Linear transit, occultation and phase model (03).** For each sector we fitted one linear model: the spline, the discovery transit template with a free scale, a box occultation at phase 0.5 with the transit duration, and sine and cosine terms at P and P/2. We clipped 5-sigma outliers and used the robust scatter as the error.

**Period and alias scan (04).** On spline-detrended flux we scanned the period with a fixed transit template. For each period we folded the data and used a circular cross-correlation over phase to get the best delta chi-square. Steps: 2e-8 d (TIC 67502817) and 2e-7 d (TIC 63562537).

**Fair alias test (16).** For TIC 63562537.01 we detrended each sector once with the transit windows of both aliases masked. Then we fitted P, T0 and Rp/R* for each alias (b and density fixed at the MCMC medians) on the same data points.

**Transit fit (11).** A joint emcee fit (24 walkers, 3,000 steps, 1,000 burn-in) with free P, T0, Rp/R*, b and log stellar density, a circular orbit, and fixed quadratic limb darkening (u1 = 0.36, u2 = 0.22). We integrated the model over each exposure. Then we fitted a mid-time per sector with the shape fixed. For TIC 63562537 we did the fit for both aliases.

**Gaia RV limit (08).** For stars with grvs_mag <= 12, Gaia DR3 gives radial_velocity as the median of the N epoch velocities and radial_velocity_error = sqrt(pi/(2N)) x std(epoch velocities) + 0.11 km/s (Katz et al. 2023). Thus the standard deviation of the epoch velocities follows from the catalogue. As a conservative limit, we assumed that all of this scatter is orbital. A semi-amplitude K is excluded if fewer than 1 % of random sets of N orbital phases give a scatter no larger than the observed value. The Gaia transits occur at phases that are effectively random for periods of a few hours.

**Gaia astrometric sensitivity (06, 07, 10).** We found the Gaia DR3 field-of-view transits of each host in the commanded scan law (FoV centre within 0.35 deg; 29 and 25 transits from 2014-07-25 to 2017-05-28). We simulated 2 x 10^5 bound companions per host: mass uniform from 0.079 solar masses to the host mass, log period from the Raghavan et al. (2010) distribution (10 d to 10^7.5 d), eccentricity uniform from 0 to 0.8, random orientation. The photocentre semi-major axis is a x parallax x (q/(1+q) - f/(1+f)), with q the mass ratio and f the G-band flux ratio from an approximate main-sequence table (Pecaut and Mamajek 2013, 2022 version). We projected the photocentre motion on the scan direction, removed a 5-parameter astrometric fit, and calculated the residual RMS. The observed RUWE and astrometric excess noise (AEN) give the per-observation error sigma = AEN/sqrt(RUWE^2 - 1) (0.133 and 0.153 mas). The predicted RUWE is sqrt(1 + (RMS^2 + AEN^2)/sigma^2). A companion counts as detected if the predicted RUWE is above 1.4 (nominal) or 2.0 (conservative). For comparison we took all Gaia DR3 stars within 20 deg with similar G, BP-RP and parallax > 5 mas (07).

**TRICERATOPS (05, 09).** TRICERATOPS 1.0.21 (Giacalone et al. 2021) with N = 10^6 draws per scenario. Input: the folded light curve of all sectors, binned to 2 minutes, and the SPOC pipeline apertures. Two changes were necessary. (1) Current TESScut files do not have the physical pixel keywords that TRICERATOPS reads. We changed one line so that it uses cutout pixel coordinates and we mapped the SPOC apertures to the cutouts through the sky coordinates. (2) The TRILEGAL server certificate chain did not verify from our host. We ran the TRILEGAL query (same settings as TRICERATOPS) with SSL verification off and gave the saved file to TRICERATOPS. We ran two seeds without imaging. As a forward test we also ran one seed with a hypothetical contrast curve typical of SOAR speckle imaging (delta mag 2.0 at 0.1 arcsec, 3.0 at 0.15, 4.0 at 0.3, 4.5 at 0.5, 5.5 at 1.0 and 6.5 at 3.0 arcsec). This curve is an assumption, not an observation. We also applied the campaign recalibration of TRICERATOPS FPP (sci:sha256:434ee8c0...): logit(p) = -1.46 + 0.50 logit(FPP).

**Occultation expectation (13).** Blackbody planet and star, top-hat band 600-1000 nm, for full heat redistribution and for a dayside without redistribution, plus reflected light A_g (Rp/a)^2.

## Results

### 1. The transit signals in independent photometry

Table 1. Transit depth scale (relative to the discovery transit model) and occultation depth per sector (linear model, 03). `files/results/linear_fit.json`.

| Candidate | Sector | Data | Depth scale | Occultation (ppm) | Data | Depth scale | Occultation (ppm) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TIC 67502817.01 | 22 | TESS-SPOC-FFI | 0.91 +/- 0.34 | -64 +/- 143 | QLP | 0.43 +/- 0.36 | -180 +/- 153 |
| TIC 67502817.01 | 45 | SPOC-2min | 0.79 +/- 0.21 | -96 +/- 132 | QLP | 0.68 +/- 0.29 | -126 +/- 167 |
| TIC 67502817.01 | 46 | SPOC-2min | 1.12 +/- 0.20 | 80 +/- 127 | QLP | 1.21 +/- 0.26 | 336 +/- 148 |
| TIC 67502817.01 | 49 | SPOC-2min | 1.14 +/- 0.21 | 112 +/- 134 | QLP | 0.71 +/- 0.31 | -255 +/- 186 |
| TIC 67502817.01 | 72 | TESS-SPOC-FFI | 0.84 +/- 0.23 | -57 +/- 141 | QLP | 1.17 +/- 0.31 | -172 +/- 192 |
| TIC 63562537.01 | 58 | SPOC-2min | 0.83 +/- 0.15 | 30 +/- 41 | QLP | 0.71 +/- 0.16 | -13 +/- 45 |
| TIC 63562537.01 | 85 | TESS-SPOC-FFI | 0.85 +/- 0.19 | -4 +/- 50 | QLP | 0.77 +/- 0.21 | -16 +/- 56 |

The QLP depths agree with the SPOC depths within the errors. The SPOC per-sector depths agree with one constant depth (chi-square 2.3 for 4 degrees of freedom for TIC 67502817; 0.0 for 1 for TIC 63562537).

### 2. Transit parameters and ephemerides

Table 2. Joint transit fit (11). Errors are 68 % intervals. `files/results/mcmc_fit.json`.

| Parameter | TIC 67502817.01 | TIC 63562537.01, alias A | TIC 63562537.01, alias B |
| --- | --- | --- | --- |
| P (d) | 0.17117297 (-0.00000023 +0.00000022) | 0.22977379 (-0.00000042 +0.00000041) | 0.22970160 (-0.00000045 +0.00000045) |
| T0 (BJD_TDB - 2457000) | 2588.86516 (-0.00039 +0.00047) | 3260.62645 (-0.00064 +0.00062) | 3260.51171 (-0.00081 +0.00069) |
| Rp/R* | 0.0244 (-0.0008 +0.0015) | 0.0164 (-0.0008 +0.0011) | 0.0163 (-0.0008 +0.0012) |
| depth (ppm) | 597 (-39 +74) | 269 (-25 +36) | 265 (-25 +39) |
| b | 0.45 (-0.31 +0.30) | 0.47 (-0.31 +0.30) | 0.44 (-0.31 +0.35) |
| stellar density (g/cm3) | 2.86 (-1.10 +0.62) | 3.95 (-1.98 +1.39) | 3.66 (-2.01 +1.18) |
| Rp (Earth radii; TIC R* = 0.626 and 0.568) | 1.67 | 1.02 | 1.01 |
| best log-likelihood | -27992.2 | -12467.3 | -12455.8 |

The best log-likelihoods of aliases A and B come from differently detrended data (the transit mask depends on the alias). Thus they are not comparable. Section 3 gives a fair comparison.

Per-sector mid-times of TIC 67502817.01 (BTJD, shape fixed): S22 1912.90497 +/- 0.00185; S45 2538.53986 +/- 0.00045; S46 2565.92798 +/- 0.00048; S49 2652.71218 +/- 0.00047; S72 3273.90002 +/- 0.00072. A linear ephemeris gives chi-square 3.1 for 3 degrees of freedom. A quadratic term gives dP/dt = 1.2e-09 +/- 7.6e-10; for a planet of at least 8 Earth masses this sets only a weak lower limit on the stellar tidal quality factor, Q'* > 4e+04 (2 sigma).

The transit-shape density agrees with the catalogue density of the host (TIC: 3.50 g/cm3 for TIC 67502817 and 4.32 g/cm3 for TIC 63562537). Thus the duration agrees with a transit across the target star. A planet around a smaller companion star would have to transit with a different geometry.

### 3. Period and cycle count

![Period scan](files/figures/fig2_period_scan.png)

Figure 2. Delta chi-square of the transit template against the trial period. Grey: single sectors; blue: all sectors.

For TIC 67502817.01 one period is clearly best (delta chi-square 323 against no transit; the nearest alias is worse by more than 143). For TIC 63562537.01 the two best aliases are 0.2297740 d (alias A, the period given first in the discovery study) and 0.2297018 d (alias B). In this scan (no transit mask during detrending) their delta chi-square values differ by only 1.6 in favour of B. The transit-masked detrending of the MCMC fits depends on the assumed alias, so the MCMC log-likelihoods of A and B are not comparable. Thus we also fitted P, T0 and Rp/R* for each alias on identical data, detrended with the union of both sets of transit windows masked (16). Alias B is then better by delta chi-square = 5.0 (likelihood ratio about 12). We prefer alias B, but the evidence is not decisive. The next aliases (0.2296298 d and 0.2298462 d) are worse by 13 and 22. The single-sector periods (S58: 0.229721 d; S85: 0.229750 d) do not choose between A and B. Future transit times for both aliases are in `files/results/ephemeris_predictions.csv`.

### 4. Gaia and LAMOST velocities

Table 3. Velocity limits for an on-target companion (08). `files/results/gaia_rv_limits.json`.

| Quantity | TIC 67502817 | TIC 63562537 |
| --- | --- | --- |
| Gaia DR3 radial_velocity (km/s) | 2.5 +/- 1.7 | 14.8 +/- 0.35 |
| RVS transits N; grvs_mag | 10; 11.42 | 11; 9.94 |
| std of epoch velocities (km/s) | 4.10 | 0.63 |
| median std for similar stars (km/s) | 3.00 (219 stars) | 0.77 (36 stars) |
| rv_chisq_pvalue; rv_amplitude_robust (km/s) | 0.23; 15.1 | 0.49; 3.0 |
| K limit, 99 % (99.73 %) | 9.6 (11.7) km/s | 1.4 (1.7) km/s |
| M2 sin i limit at P; at 2P (Jupiter masses) | 19; 24 | 2.9; 3.6 |
| K of a 0.08 solar-mass companion at P; at 2P | 39.3; 31.2 km/s | 37.4; 29.7 km/s |
| LAMOST DR10 LRS (date, class, velocity) | 2015-01-03, dM0, z = 8.7e-6 (2.6 km/s) | 2016-01-12, dM0, z = 3.85e-5 (11.5 km/s) |

The LAMOST velocities agree with the Gaia values within the LAMOST LRS precision (about 5 km/s). The epoch scatter of TIC 67502817 is near the 72nd percentile of similar stars, and that of TIC 63562537 is near the 22nd percentile. Thus the Gaia data show no sign of a close stellar companion. An eclipsing pair of stars that includes the target would have K of 30 km/s or more. The data exclude this for both stars. For TIC 63562537 the limit also excludes brown dwarfs (M2 sin i < 2.9 Jupiter masses at P). For TIC 67502817 it excludes companions above about 24 Jupiter masses.

### 5. Gaia astrometry and bound companions

![RUWE sensitivity](files/figures/fig3_gaia_ruwe_sensitivity.png)

Figure 3. Fraction of simulated bound companions with predicted RUWE above 1.4.

Table 4. Fraction of simulated companions with TESS-band contrast below 4 mag that Gaia RUWE would detect (10). `files/results/astro_sim_summary.json`.

| Projected separation (arcsec) | TIC 67502817, RUWE > 1.4 (> 2.0) | TIC 63562537, RUWE > 1.4 (> 2.0) |
| --- | --- | --- |
| 0.01-0.05 | 0.90 (0.82) | 0.97 (0.93) |
| 0.05-0.10 | 0.68 (0.42) | 0.94 (0.86) |
| 0.10-0.20 | 0.21 (0.01) | 0.85 (0.65) |
| 0.20-0.40 | 0.00 (0.00) | 0.61 (0.17) |

TIC 63562537 is closer (41.6 pc against 92.7 pc), so the same orbit gives a larger angular motion. Gaia DR3 lists no other source within 15.0 arcsec of TIC 67502817 (the nearest has G = 16.80, 4.0 mag fainter) or within 36 arcsec of TIC 63562537. Both hosts have ipd_frac_multi_peak = 0 and a small ipd_gof_harmonic_amplitude (0.007 and 0.030). Thus Gaia shows no resolved companion. But Gaia does not resolve faint companions closer than about 1 arcsec, and we did not model this limit. The range from about 0.1 to 1 arcsec (9-93 au for TIC 67502817; 4-42 au for TIC 63562537 above 0.3 arcsec) needs high-resolution imaging.

### 6. TRICERATOPS

![Constraints](files/figures/fig4_constraints_summary.png)

Figure 4. Left: TRICERATOPS scenario probabilities (mean of two seeds). Right: Gaia RVS limit on K.

Table 5. TRICERATOPS results (05). `files/results/triceratops/`.

| Candidate | Run | FPP | NFPP | P(TP) | P(PTP+DTP) | P(STP) | P(all EB) | Class |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TIC 67502817.01 | no imaging, seed 1 | 0.16 | 0.00088 | 0.721 | 0.118 | 0.16 | 1e-28 | likely planet |
| TIC 67502817.01 | no imaging, seed 2 | 0.11 | 0.00038 | 0.695 | 0.190 | 0.115 | 1e-21 | likely planet |
| TIC 67502817.01 | hypothetical speckle curve, seed 1 | 0.036 | 0.0011 | 0.904 | 0.060 | 0.0346 | 9e-29 | FPP < 0.5 but NFPP above 0.001 (assumed imaging) |
| TIC 63562537.01 | no imaging, seed 1 | 0.044 | 1.7e-08 | 0.772 | 0.183 | 0.0441 | 7e-19 | likely planet |
| TIC 63562537.01 | no imaging, seed 2 | 0.025 | 9.4e-09 | 0.868 | 0.107 | 0.0252 | 7e-21 | likely planet |
| TIC 63562537.01 | hypothetical speckle curve, seed 1 | 0.00038 | 2.1e-08 | 0.977 | 0.023 | 0.000332 | 4e-19 | validated (assumed imaging) |

Giacalone et al. (2021) classify a candidate as validated if FPP < 0.015 and NFPP < 0.001, and as a likely planet if FPP < 0.5 and NFPP < 0.001. Both candidates are likely planets. They are not validated. The FPP is almost all STP: a planet on a bound companion star. In this scenario the object is still a planet, but its radius and period refer to a different star. EB scenarios on the target or on a companion have probabilities below 10^-5, in agreement with the Gaia velocity result. For TIC 63562537 the nearby-star scenarios (NFPP) are negligible: no Gaia or TIC star within 36 arcsec is bright enough to make the signal. For TIC 67502817 the NFPP (4e-4 to 1.1e-3) is near the 0.001 limit. It comes from TIC 67502818 (T = 16.24, 15 arcsec), which would need an eclipse of several percent. The discovery study found that difference images put the source on the target and that a source at this neighbour fits worse (sum of delta chi-square 79). Ground-based photometry that resolves the two stars can remove this scenario.

The campaign calibration study found that TRICERATOPS FPP values from 2021 were too high on average, mostly at P < 1 d. With its recalibration, the FPP values become 0.093, 0.078 (TIC 67502817.01) and 0.048, 0.036 (TIC 63562537.01). This recalibration was derived from the 2021 TRICERATOPS version and from TOIs, so it is only a sensitivity check here.

### 7. Occultation and phase curve

For TIC 67502817.01 the combined occultation depth is -2 +/- 60 ppm, and the amplitudes at P and P/2 are cos1 -13 +/- 30, sin1 3 +/- 17, cos2 -14 +/- 36, sin2 8 +/- 17 ppm. For TIC 63562537.01 the occultation depth is 17 +/- 32 ppm. The expected thermal occultation of TIC 67502817.01 in the TESS band is 12 ppm (2,080 K, full redistribution) to 74 ppm (2,660 K dayside without redistribution). Reflected light adds 200 ppm x A_g. The 2-sigma upper limit (about 120 ppm) allows any dark planet and limits A_g to below about 0.5. This test cannot separate a planet from a false positive.

## Interpretation

The data favour astrophysical signals on the target or on a star that is not resolved from the target. Systematics are unlikely because the signals repeat in all sectors, cameras and two pipelines. The Gaia velocities remove the most common false-positive class for an ultra-short-period M-dwarf signal: an eclipsing binary that includes the target. The background and nearby-star scenarios are improbable. The remaining open question is whether the transited star is the host or an unresolved bound companion. Gaia astrometry excludes most bright companions inside about 0.1 arcsec (TIC 67502817) and 0.2 arcsec (TIC 63562537). Speckle or adaptive-optics imaging can test 0.1 to 1 arcsec.

If TIC 67502817.01 is a planet on the target, its period (0.17117 d) is shorter than that of KOI-1843.03 (0.1769 d) and K2-137 b (0.1797 d). At a/R* = 1.73, the Roche limit requires a mean density of at least about 9.4 g/cm3 (an iron-rich composition), so the mass is at least about 8 Earth masses and K is at least about 13 m/s (discovery study). Tidal decay at this distance is fast unless the stellar tidal quality factor is large. With the stellar tidal quality factor Q'* = 10^7, the remaining lifetime is about 10 Myr. The timing over 2020-2023 gives only a weak limit on period decay. This is a further reason for follow-up.

## Limitations

- No new TESS sectors exist. Our photometric tests use the same photons as the discovery study, with different reductions. QLP and SPOC use the same FFIs for sectors 22, 72 and 85.
- The Gaia RV limit assumes that the Gaia epoch velocities sample the orbit at random phases, and it treats all scatter as orbital (conservative). It does not test companions on wide orbits.
- The RUWE simulation uses an approximate mass-magnitude table, a simple 5-parameter along-scan model without attitude or calibration noise, and the observed AEN as the noise level. Gaia resolution of companions at 0.3-2 arcsec was not modelled.
- TRICERATOPS needed two local changes (pixel coordinates; local TRILEGAL file). The FPP changes by about 30 % between seeds for TIC 67502817.01. The speckle run uses a hypothetical contrast curve. A real observation is necessary.
- The cycle count of TIC 63562537.01 is not certain (alias B preferred by delta chi-square 1.6 to 5.0, depending on the detrending). Its predicted transit times have two branches.
- Neither candidate is confirmed or validated. Their planetary nature needs high-resolution imaging and precise radial velocities.

## What remains open

- Speckle or AO imaging of both stars (I band or near-infrared). With no companion detected, TIC 63562537.01 would pass the TRICERATOPS validation limit (Section 6). TIC 67502817.01 would also need a check of the 15-arcsec neighbour TIC 67502818 (ground-based photometry at the predicted transit times) and a joint use of the Gaia RUWE limit inside 0.1 arcsec.
- Precise radial velocities: TIC 67502817.01 needs a precision of a few m/s (K >= 13 m/s if it is a planet). TIC 63562537.01 (Earth-size, K about 1.5 m/s for Earth density) is hard.
- Ground-based photometry is difficult (depths 260-600 ppm), but a few transits with a 1-2 m telescope can confirm the depth and resolve the alias of TIC 63562537.01.
- Future TESS sectors, if scheduled, will extend the baseline for period-decay tests.

## Reproduction

1. Create a Python 3.12 environment and install: numpy<2.1, scipy<1.14, astropy, pandas, matplotlib, batman-package, emcee, lightkurve, astroquery, triceratops==1.0.21, mechanicalsoup, setuptools<70.
2. Apply the one-line TRICERATOPS change in `files/code/triceratops_patch.py` (run it once).
3. `06_gaia_scans.py` reads the scan-law file from `../../datasets/gaia-dr3-commanded-scan-law-001/` relative to the code folder; change `SRC` if your copy is elsewhere (download URL https://cdn.gea.esac.esa.int/Gaia/gedr3/auxiliary/commanded_scan_law/CommandedScanLaw_001.csv.gz). Run `files/code/01_fetch_tess.py`, `02_gaia.py`, `06_gaia_scans.py` (needs the Gaia commanded scan law file), `07_gaia_reference.py` and `09_trilegal.py`. They write into `scratch/` beside `code/`. Then run 03, 04, 08, 10, 11, 13, `05_triceratops.py TIC none nocc SEED` and 12 (figures). On our host, IPv6 connections to some archives hang; `files/code/ipv4_sitecustomize.py` forces IPv4.
4. Compare the outputs with `files/results/`.

The run times on 1-2 CPU cores were: TRICERATOPS 35-70 min per seed; MCMC about 1 h; other steps a few minutes.

## Licenses and attribution of external data

See `files/EXTERNAL_DATA_NOTICE.md`. The LICENSE file (SCI baseline) applies to our text, figures, code and derived aggregate results. It does not apply to the external data, which we do not redistribute.
