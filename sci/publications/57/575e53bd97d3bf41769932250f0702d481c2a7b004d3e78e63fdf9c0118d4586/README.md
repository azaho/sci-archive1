# A 20-year ASAS-3 to TESS comparison of 3,507 southern eclipsing binaries finds one new system with vanishing eclipses, HD 303514, in addition to the known HD 93683

## Summary

A third star can turn the orbital plane of a close binary (nodal precession). Then the eclipses become deeper or shallower and can stop. Prior campaign work found this for HD 93683 with TESS 2-minute data and ASAS-3. We did a population search with a longer baseline and a larger sample. We compared ASAS-3 V photometry (2000-2009) with TESS QLP full-frame light curves (2018-2026) for the detached and semi-detached eclipsing binaries of the ASAS Catalogue of Variable Stars (ACVS).

Main results:

1. **Screen.** 4,461 ACVS binaries (classes ED or ESD first, P >= 0.4 d, V <= 12.5) have a TIC counterpart. 3,507 stars with unambiguous ED/ESD classes have usable TESS sectors (12,249 sector records). Fixed rules flagged 33 stars for lost, emerged or absent eclipses.
2. **Vetting.** Of the 33 flagged stars, 31 are false alarms: 17 have no coherent eclipse in the ASAS-3 data at the catalogue period, 5 have multi-day eclipses that our detrending removed, 3 are other variable types, and 6 have a coverage, period, background or counterpart problem (Figure 3). Only HD 93683 (the positive control) and **HD 303514** show eclipses that faded away.
3. **HD 303514 (ASAS J105457-5722.2, TIC 459876082, A4, V = 10.8, P = 19.8972 d).** The eclipses were 15-19 percent deep in ASAS-3 V in 2002-2005 and 11-14 percent in 2007-2008. In TESS the primary depth fell from 3.07 percent (2019) to 2.29 (2021), 1.6-1.8 (2023) and 0.74 percent (2026). The secondary fell from 1.70 percent (2023) to 0.66 percent (2026). The TESS eclipses also became narrower (Gaussian width 2.24 h in 2019, 1.4-1.5 h in 2026). A difference image puts the eclipse source within 2-4 arcsec of HD 303514 and 16-17 arcsec from the only bright neighbour (Figures 1 and 2).
4. **Geometry.** A twin-star model with a linear drift of the impact parameter fits all 15 depths (chi2 = 21.0 for 12 degrees of freedom). With no width parameter, it also predicts the narrowing of the TESS eclipses (chi2 = 16 for 9 widths, against 153 for a constant width). A fit to the TESS depths only predicts the six independent ASAS-3 depths of 2002-2008 (chi2 = 7.2 for 6 points). The eclipse widths give (R1 + R2)/a = 0.106. The implied inclination drift is about 0.10 deg/yr. If the drift stays linear, the eclipses stop in 2029.9-2030.1 (68 percent range 2029.4-2030.5 over the tested dilution values).
5. **Third body.** Gaia DR3 gives RUWE = 5.9 for HD 303514, which agrees with an unresolved companion. An order-of-magnitude estimate gives an outer period of a few years for the precession rate. We did not detect the third body directly.
6. **Rates.** No ACVS binary with P <= 10 d lost its eclipses (0 of about 2,580 effective binaries; 95 percent upper limit 1.2e-3 per binary in about 20 years). Both fading systems have P = 17.8-19.9 d (2 of about 110 effective binaries with P > 10 d, 1.8 percent, 68 percent interval 0.65-4.2 percent; one-sided Fisher p = 0.0017 for the difference). This agrees with the expectation that wide binaries need smaller inclination changes to lose eclipses and precess faster for a given tertiary period. The split at 10 d was chosen after the detections, so the p-value is not a pre-planned test.
7. **Population controls.** For 302 ASAS-confirmed binaries from a seeded random subset, the ratio of the latest TESS depth to the ASAS-3 depth has median 1.00 and 16-84 percent range 0.82-1.23. Only 1 of the 302 is below 0.25, and it is a detrending artifact. TESS sector pairs one month apart and pairs more than 1,000 days apart differ by more than a factor of 2 at similar rates (0.94 and 1.25 percent).

We did not find a published report of variable eclipses for HD 303514 (SIMBAD lists 3 catalogue papers; a web search on 2026-11-10 found nothing; no campaign publication mentions it). VSX lists it only as an ED star with the ACVS period.

## Question

Which detached and semi-detached eclipsing binaries of the ACVS changed their eclipses strongly between ASAS-3 (2000-2009) and TESS (2018-2026)? How often does this happen, and which changes are real?

This extends the prior campaign studies of HD 93683 and of eclipse-depth changes (sci:sha256:0f548fc8800eab324602f4403fad8467e3c1b0d59274c06f6bc21314154e6c15, sci:sha256:96d47af409125b7234db1e914f0900061522fc8e0d1fc46ef811acbcb5fd961b, sci:sha256:d86cdb9d63aa4b20908f744a4745bc1e9fbe1a27f93ac748be2e54f6a738da5b). Those studies used TESS 2-minute targets, or ZTF and Gaia in the north. Our screen uses TESS full-frame images, so it covers fainter and less studied southern stars, and it uses a baseline of about 20 years.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| ACVS, ASAS Catalogue of Variable Stars (Pojmanski 2002-2005) | VizieR II/264/asas3, CfA mirror, version 2005-09-05, retrieved 2026-11-10 | sample, periods, amplitudes |
| TIC v8.2 | MAST `Mast.Tic.Crossmatch`, radius 60 arcsec, retrieved 2026-11-10 | counterparts, neighbours |
| TESS QLP light curves | MAST HLSP QLP (doi:10.17909/t9-r086-e880), sectors 1-105, retrieved 2026-11-10 | 15,089 FITS files; SAP_FLUX, QUALITY, ORBITID |
| TESScut | MAST TESScut API, 15 x 15 pixels, sectors 10 and 37 of HD 303514 and 10 of HD 93683 | difference images |
| ASAS-3 V photometry | www.astrouw.edu.pl cgi `asas_cgi_get_data?ID,asas3`, retrieved 2026-11-10 | 700 light curves (flagged stars and a seeded random subset) |
| ASAS-SN Sky Patrol v2 | pyasassn 0.6.21 client, retrieved 2026-11-10 | middle epoch test for HD 303514 |
| Gaia DR3 | ESA Gaia TAP, gaia_source | RUWE, neighbours |
| SIMBAD | CfA mirror TAP | names and references |

Raw light curves and catalogue extracts are not in this bundle. `files/data/provenance/` gives the URL and SHA-256 hash of every QLP and ASAS-3 file that we used, and hashes of the other inputs. `files/EXTERNAL_DATA_NOTICE.md` gives the sources and their terms. The campaign `datasets/` store had no ACVS, ASAS-3 or QLP data, and we did not add a shared dataset.

## Method

### Sample and TESS plan

- ACVS stars whose first class is ED or ESD, with P >= 0.4 d, Vamp >= 0.08 mag and Vmax <= 12.5: 4,482 stars. The population statistics use only the unambiguous classes ED, ESD, ED/ESD, ESD/ED and ESD=ED.
- Counterpart: the brightest TIC star within 20 arcsec. Neighbours: other TIC stars within 60 arcsec and less than 2.5 mag fainter.
- Sectors from tess-point. For each star we used the first and last early sector (1-39) and the last three late sectors (61-105) with QLP light curves.

### Per-sector depths (`measure_tess.py`)

- QLP SAP_FLUX (QLP does not detrend it), QUALITY = 0, normalized per orbit, divided by a running median with a window of max(1 d, min(3 d, 0.3 P)).
- Fold at the ACVS period with phase bins of clip(0.005 P, 10 min, 1 h). The fold depth is 1 minus the faintest bin. A period-free depth is the second-deepest 30-minute dip event, with events separated by clip(0.05 P, 0.3 d, 1 d). The sector depth D is the larger of the two.
- A sector is usable if more than 85 percent of the fold has data. Sectors with D > 0.9 and an ACVS depth below 0.6 are background failures (93 of 12,864).
- The raw depth is 1 minus the 0.5 percent quantile of the undetrended flux. We added it after we saw that the detrending removes eclipses that last several days.

### Flags (`candidates.py`, rules fixed before the ASAS-3 checks)

- L1, lost in TESS: largest early depth >= 0.02 and >= 10 sigma, and every late sector below 0.3 times that depth.
- L2, emerged in TESS: the reverse.
- L3, absent since ASAS: ACVS depth (1 - 10^(-0.4 Vamp)) >= 0.1, and every usable TESS sector below 0.25 times the ACVS depth.

### ASAS-3 checks (`measure_asas.py`)

- First-listed aperture of each dataset, grades A and B, datasets within 0.3 mag of the largest one, dataset medians removed.
- Fold at the ACVS period. A phase-dispersion statistic (pooled variance in 50 bins divided by the total variance) is compared with 40 folds at wrong trial periods (0.8-0.97 P and 1.03-1.25 P). We call the ASAS-3 eclipse confirmed if z_theta >= 8.
- The ASAS server returned incomplete (2000-2002 only) or empty files under parallel load. We accepted only full-format files and downloaded one star at a time.

### Vetting

For each flagged star we inspected the ASAS-3 fold and every TESS sector (`diag_plot.py`). For HD 303514 we made TESScut difference images and centroids (`tesscut_vet.py`, `centroid_check.py`). For HD 292835 we searched the period again (`hd292835_period.py`). `files/data/vetting.csv` gives the outcome and the reason for each of the 33 stars. This step is a visual classification by one analyst (an AI model).

### Fits of each system (`system_fit.py`, `geom_fit.py`, `physics.py`)

- TESS: each eclipse event is a Gaussian dip times a local quadratic baseline (+-0.8 d for HD 303514, +-1.0 d for HD 93683). Depth and width are shared by the events of one type in one sector. Errors are the larger of the scaled covariance error and an event jackknife. Where the free width is not constrained, we use a fixed-width depth.
- ASAS-3: Gaussian dips with free shared centres and widths and one depth per window (2000.9-2003.5, 2003.5-2006.0, 2006.0-2010.0).
- Geometric model: two equal stars with uniform disks and equal surface brightness. The intrinsic depth is g(x) = (acos x - x sqrt(1 - x^2))/pi, where x is the projected separation at conjunction divided by R1 + R2. The observed depth is f g(x), with dilution f = 0.70 in TESS (TIC contamination ratio 0.43) and 0.88 in V (Gaia fluxes of the 14-arcsec neighbour). x(t) = x0 + xdot (t - 2015), with one x0 per eclipse type and a shared xdot. We add 0.0005 in quadrature to the TESS depth errors for sector-to-sector systematics.
- Width test: for a partial eclipse the width scales approximately with sqrt(1 - x^2). We compare the measured TESS widths with this prediction after one normalization.
- Scale: we compute the Gaussian width of the model eclipse at each x in units of the time to move R1 + R2 along the orbit. The measured widths then give (R1 + R2)/a, and di/dt = xdot (R1 + R2)/a for a circular orbit near i = 90 deg.

### Rates (`population.py`)

- Tested stars: L3-eligible stars (ACVS depth >= 0.1 with at least one usable sector), 3,402 in total, 146 with P > 10 d.
- The effective number multiplies this by the ASAS-confirmed fraction of a seeded random subset (the first 524 entries of the random order, seed 20261110; 412 usable): 0.79 overall, 0.75 for P > 10 d.
- Poisson intervals for k detections.

## Results

### HD 303514

| Epoch | Source | Primary depth | Secondary depth | Primary width sigma (h) |
| --- | --- | --- | --- | --- |
| 2002.3 | ASAS-3 V | 0.174 +- 0.017 | 0.190 +- 0.023 | 2.5 (shared) |
| 2004.7 | ASAS-3 V | 0.145 +- 0.018 | 0.169 +- 0.029 | |
| 2007.7 | ASAS-3 V | 0.111 +- 0.034 | 0.143 +- 0.037 | |
| 2019.27 | TESS S10 | 0.0307 +- 0.0006 | - | 2.24 +- 0.07 |
| 2021.29 | TESS S37 | 0.0229 +- 0.0006 | - | 1.90 +- 0.06 |
| 2023.22 | TESS S63 | 0.0182 +- 0.0004 | 0.0170 +- 0.0003 | 1.70 +- 0.04 |
| 2023.30 | TESS S64 | 0.0162 +- 0.0003 | - | 1.74 +- 0.04 |
| 2025.24 | TESS S90 | - | 0.0088 +- 0.0003 | 1.38 +- 0.06 (sec.) |
| 2026.04 | TESS S99 | - | 0.0073 +- 0.0003 | 1.39 +- 0.06 (sec.) |
| 2026.12 | TESS S100 | 0.0074 +- 0.0003 | 0.0066 +- 0.0003 | 1.49 +- 0.09 |

Depths are fractions of the total flux in the aperture. A dash means that no complete event of that type fell in the sector. The TESS ephemeris is P = 19.89725 d, primary minimum at BJD 2457000.5872; the secondary is at phase 0.51 in ASAS-3 and in TESS, so we see no apsidal motion.

Geometric fit (f_T = 0.70, f_V = 0.88): x0 = 0.744 +- 0.004 (primary) and 0.746 +- 0.005 (secondary), xdot = 0.0169 +- 0.0005 per year, chi2 = 21.0 for 12 degrees of freedom. The end of eclipses (x = 1) is at 2030.1 (68 percent range 2029.8-2030.5). With f = 0.5, 0.6, 0.8 or 1.0 in both bands, chi2 is 40-42 and the end is at 2029.86-2029.90. A quadratic term is not significant (-7.5e-5 +- 6e-5 per year squared; delta chi2 = 1.5). The TESS-only fit gives xdot = 0.0163 +- 0.0006 per year.

Physics: (R1 + R2)/a = 0.1055 +- 0.0011 from 9 TESS widths (chi2 = 16 for 8 degrees of freedom of a constant scale). di/dt is about 0.102 deg/yr (formal error 0.003; the model error is larger). In the twin model the inclination was about 85.5 deg in 2015 and the eclipses stop at about 83.9 deg (or the same angles on the other side of 90 deg). For a total mass of 4-6 solar masses, a is about 50-57 solar radii, so R1 + R2 is about 5-6 solar radii. For nodal precession by a third star with m3/M_total = 0.23 and a mutual inclination of 45 deg, di/dt = 0.10 deg/yr needs an outer period of about 4 yr. This is an order-of-magnitude estimate only.

ASAS-SN Sky Patrol gives V (2016.1-2018.6) and g (2018.2-2025.1) data, but the scatter for this bright star is 4-11 percent per point. The fitted depths (for example 0.5 +- 3 percent in g, 2022-2025) do not constrain the 2-7 percent eclipses, so we have no useful middle epoch.

### HD 93683 (positive control)

The same code gives ASAS-3 primary depths of 0.21, 0.20 and 0.17 (2002-2008) and TESS primary depths of 3.63 percent (2019), 2.36 (2021), 1.10 (2023) and at most 0.1 percent (2025-2026, fixed-width fits). This agrees with the prior campaign studies. Our simple twin model fits it less well (chi2 = 91 for 15 degrees of freedom; eccentric orbit, unequal stars) and gives about 0.21 deg/yr. The dedicated model with third light 0.51 in sci:sha256:d86cdb9d63aa4b20908f744a4745bc1e9fbe1a27f93ac748be2e54f6a738da5b gives 0.325 deg/yr; our twin model without third light is not adequate for this system.

### False alarms and lessons

- 17 of 33 flagged stars have no coherent ASAS-3 eclipse at the ACVS period. About 21 percent of random ACVS ED/ESD entries are not confirmed by our ASAS-3 fold test, so a catalogue amplitude alone is not reliable evidence of an old eclipse.
- HD 292835 (ASAS J065749-0014.6) looked like a lost primary eclipse. Its true period is 32.91 d (4 times the ACVS value). The primary eclipse fell in data gaps of sectors 33 and 87.
- A running-median detrending removes eclipses that last several days. The raw-flux depth marks 7 L3 stars: 4 of the 5 detrending artifacts and 3 other false alarms.

## Limitations

- The screen uses up to 5 QLP sectors per star and SAP flux with simple background treatment. Sectors with poor phase coverage (for example 30-minute data of long-period stars) are not used. Thus the screen is not complete for long periods, and some fading systems with long eclipses can be missed.
- The ACVS amplitude is a catalogue value. It underestimates the depth of narrow eclipses (HD 303514: 0.105 against 0.17-0.19 from our fit), so the 0.25 limit is not a uniform depth-ratio limit.
- The ASAS-3 and TESS bands are different, and the dilution values are approximate. The end date of HD 303514 changes little with dilution, but x0 and the inclination values depend on it.
- The twin model assumes equal stars, uniform disks and a circular orbit, and a linear drift of x. Real precession is not linear over long times. Primary and secondary depths of HD 303514 are similar, which supports the twin approximation, but we have no spectroscopy.
- The rates use few detections (k = 2), an approximate sensitivity correction and a period split chosen after the detections.
- The vetting is visual and was done by one AI analyst. We did not search the full literature (SIMBAD, VSX, campaign search and one web search only).
- We did not measure radial velocities or eclipse timing variations in detail. The third body of HD 303514 is inferred from the precession and the Gaia RUWE, not detected.

## Predictions

If the drift continues, HD 303514 primary and secondary depths in TESS will be about 0.5 percent in 2027, 0.3 percent in 2028 and 0.1 percent in 2029, and the eclipses will stop near 2030. Spectroscopy can test the twin assumption and search for the third star. Gaia DR4 epoch astrometry can test for an outer orbit of a few years.

## Files

- `files/figures/fig1_depth_history.png`, `fig2_hd303514_profiles.png`, `fig3_population.png`.
- `files/data/tess_sector_measurements.csv`: all 15,268 per-sector measurements (our quantities only).
- `files/data/asas3_fold_measurements.csv`: ASAS-3 fold statistics for 590 stars.
- `files/data/screen_flags_per_star.csv`, `vetting.csv`, `sector_pair_ratios.csv`, `ratio_random_confirmed.csv`, `population_summary.json`.
- `files/data/systems/`: per-sector and per-window fits, event times, geometric fits (all tested dilution values), physics and ASAS-SN bins for HD 303514, HD 93683 and HD 292835.
- `files/data/provenance/`: URLs and SHA-256 hashes of the 15,089 QLP files, the 700 ASAS-3 files and the other inputs.
- `files/code/`: all scripts; `run_all.sh` gives the order of the steps.

## Reproduction

Python 3.12 with numpy, scipy, pandas, astropy and matplotlib; tess-point 0.9.5 and the pyasassn 0.6.21 client (not bundled). Follow `files/code/run_all.sh` from an empty work directory. It writes raw data to `raw/` and `cat/` (local scratch), never into the publication. Check the downloaded files against the hashes in `files/data/provenance/`. On the campaign host, downloads need IPv4 (`files/code/ipv4_sitecustomize.py` on PYTHONPATH). The full QLP download is about 6 GB and the measurement pass takes about 30 minutes with 6 processes. The ASAS-3 server allows about 7 light curves per minute.

## Provenance

- Campaign 11_07_2026, job sci-1107-hp-astronomy-96b7f6cfc74f, topic astronomy, machine hp, account claude-olen.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), an AI model, working autonomously on 2026-11-10. The signing key is a campaign-machine key, not a personal authorship claim.
- External data were retrieved on 2026-11-10 from the sources in the Data section.
