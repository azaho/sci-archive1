# Eclipsing binaries occur only in the red-excess class of 9,786 Gaia DR3 astrometric white-dwarf-candidate binaries; TESS shows no signal at predicted outer conjunctions

Job: sci-1107-dell-astronomy-965027326fea (campaign 11_07_2026, topic astronomy, machine dell). Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim. Date of work: 2026-11-08.

## Summary

Shahaf et al. (2024) used Gaia DR3 astrometric orbits (periods 45 to 1,000 days) to find 9,786 binaries whose faint companion is not a single main-sequence star. They divided the sample with Gaia synthetic photometry. 3,166 systems have no red colour excess (NCE). The authors identify most of these companions as white dwarfs (WDs). 6,620 systems have a red colour excess (RCE). The authors identify these companions mostly as close pairs of M dwarfs, that is, hierarchical triples. We did two independent tests of this division.

1. **Conjunction test (null result).** We propagated the full Gaia orbit covariance to the times when the companion passes in front of the star or behind it (conjunctions) in the TESS era. We then searched 970 TESS sector light curves of the 261 most edge-on systems. We expected 23.4 aligned conjunctions on usable TESS data (8.2 for NCE). We found no signal at any predicted conjunction. The test has almost no power for WD self-lensing pulses (expected detections 0.22), because the pulses are short (0.2 to 0.6 d) and small (0.1 to 0.8 %) for these faint stars (median G = 14.2). If each aligned conjunction gave an eclipse 5 % deep, we would expect 9.7 detections (Poisson probability of zero is 6 x 10^-5).
2. **Eclipsing-binary test (positive result).** The Gaia DR3 eclipsing-binary table contains 21 of 6,620 RCE systems and 0 of 3,166 NCE systems (Fisher one-sided p = 2.7 x 10^-4; p = 6 x 10^-4 in a permutation test stratified in G magnitude and parallax). Our TESS periodic search finds clear eclipses in 12 of 189 RCE systems and 0 of 72 NCE systems (p = 0.019). Eleven of these 12 eclipsing systems are not in the Gaia DR3 eclipsing-binary table. Difference images put the eclipses on the target star.
3. **Orientation test (positive result).** The outer (astrometric) orbits of the 21 Gaia eclipsing systems are closer to edge-on than the other RCE orbits: mean |cos i| is 0.295 against 0.519 (Mann-Whitney p = 1.6 x 10^-4). An inner eclipsing orbit must be near edge-on. Thus this result agrees with partial alignment of the inner and outer orbits. A simple model gives a mutual-inclination scale of about 15 to 30 degrees and rejects isotropic orientations (2 delta lnL = 11).

Results 2 and 3 support the Shahaf et al. division: close eclipsing binaries occur in the RCE class and not in the NCE (probable WD) class. In some systems the eclipsing pair can be the bright component, not the faint companion (see Limitations). We report no new planet, no self-lensing binary and no new compact object.

## Question

Gaia DR3 gives astrometric orbits for thousands of solar-type stars with unseen companions of about 0.6 solar masses. These companions are probably WDs, and the sample is a large new population of AU-scale WD + main-sequence binaries. The classification of each system depends on the Gaia orbit and on photometric models. We asked these questions:

- Do the Gaia orbit inclinations and conjunction times predict observable TESS events: self-lensing pulses for WD companions, or eclipses for luminous companions?
- Do independent eclipse data support the separation of RCE systems (probable triples) from NCE systems (probable WDs)?

Prior work: Yamaguchi, El-Badry and Sorabella (2024, arXiv:2410.13939) searched TESS-SPOC light curves with T < 10.5 (sectors 1 to 69) for non-repeating self-lensing pulses. They also checked Gaia non-single-star solutions within 5 degrees of edge-on. We extend this to the Shahaf et al. sample at all magnitudes, with the full Gaia covariance and quantitative injection-recovery. The test of eclipsing binaries by triage class is, to our knowledge, new.

## Data

- Shahaf et al. (2024) Table A1 (9,786 sources, primary mass m1 and red-excess probability Pr(red); NCE means Pr(red) < 56 %). Source: arXiv:2309.15143 source tarball. We do not redistribute it; `files/provenance.json` gives the URL and SHA-256 hashes.
- Gaia DR3 `nss_two_body_orbit` (8,937 Orbital and 849 AstroSpectroSB1 solutions), `gaia_source`, `vari_eclipsing_binary`, `vari_classifier_result`, and neighbour lists. Source: ESA Gaia archive TAP, retrieved 2026-11-08.
- TESS full-frame-image cutouts (11 x 11 pixels; SPOC calibrated FFIs) from MAST TESScut: 987 sector cutouts for 262 systems, sectors 1 to 108. We do not redistribute them (18 GB). `files/data/cutout_hashes.csv` gives the SHA-256 of each downloaded file.

## Method

**Orbit Monte Carlo** (`code/02_orbit_mc.py`, `code/02b_orbit_mc_refined.py`). For each source we drew 4,000 samples of the orbit parameters from the Gaia covariance (parameter order from the Gaia `nsstools` package). From the Thiele-Innes elements we computed cos i, the argument of periastron and the photocentre semi-major axis. We assumed a dark companion and solved for its mass. Then we calculated the relative orbit, the stellar radius (main-sequence relation), the impact parameter at each conjunction, the transit duration, and the self-lensing amplitude 2 (R_E/R*)^2. We propagated both conjunction times (argument of latitude 90 and 270 degrees) into the TESS era. Astrometry alone cannot tell which conjunction puts the companion in front, so we tested both and gave each a probability of 0.5 for lensing. The sum of the alignment probabilities over all 9,786 systems is 25.1. Isotropic orbits give 27. This shows no strong bias toward edge-on orbits. Check (`code/10_check_omega.py`): for the 849 AstroSpectroSB1 solutions, omega from (A, B, F, G) agrees with omega from (C, H) to a median of 3 degrees (modulo 180). C and H are in AU in the DR3 table.

**Selection and photometry** (`code/03` to `code/06`, `code/08`). 805 systems have an alignment probability above 10^-4. We computed the probability that each conjunction falls inside each TESS sector that observes the system. We downloaded the 987 sector cutouts that carry 89 % of the expected number of aligned conjunctions. The SPOC FFI cutouts are not background-subtracted. Thus we subtracted a sky value per cadence from the faint outer pixels. We made photometry in three apertures (1 pixel, plus-shaped 5 pixels, 3 x 3 pixels). For each light curve, a coarse noise scan selected the aperture with the lowest box noise after a dilution correction. The dilution correction uses Gaia neighbours and a Gaussian PSF (sigma 0.6 pixel). The scan used noise only, not signal.

**Conjunction-window search** (`code/07_search.py`, `code/09_analyze.py`, `code/lcsearch.py`). At each trial time, a local least-squares fit gives a box amplitude. The fit uses a quadratic baseline and four regressors (sky, two centroids, ring flux) in a window of +/-max(1 d, 2 durations). We used two box durations. We normalised the amplitude-to-error ratio by its robust scatter in each light curve (z). The test window for each conjunction is the predicted time +/- (3 sigma + duration). We calibrated false alarms with 1,000 windows of the same width at random places in random light curves of the sample (pooled controls). A detection needs a per-window false-alarm probability below 0.003. We injected 24 limb-darkened self-lensing pulses per window (impact parameter 0 to 0.9) with the predicted amplitude and duration. A pulse counts as recovered when it passes the same threshold. An analytic box-noise calculation agrees with the injections (correlation 0.90). We used this calculation for eclipses 1 % and 5 % deep.

**Periodic eclipse search** (`code/14_bls.py`, `code/19` to `code/22`). We detrended each sector with a 1-day running median and binned it to at least 10 minutes. We ran box least squares (period 0.3 to 13 d). We ran the same search on sign-inverted flux as a control. A detection needs SDE >= 10, depth S/N >= 7, at least 3 events, an eclipse-like duty cycle (duration/period < 0.25), and a difference-image centroid on the target. We folded each detection at P and 2P to find the period.

**Gaia statistics** (`code/15` to `code/18`). We used a Fisher exact test and a permutation test stratified in G magnitude (0.5 mag bins) and parallax (quartiles) for the eclipsing-binary rates. For the orientation test we used Mann-Whitney and permutation tests on |cos i|. The mutual-inclination model is isotropic outer orbits plus a Rayleigh tilt for the inner orbit, conditioned on inner eclipses (|cos i_in| < 0.3, 0.5 or 0.75).

## Results

### 1. No signal at predicted conjunctions (Figure 1)

| Quantity | All (261 systems) | NCE (72) | RCE (189) |
| --- | --- | --- | --- |
| Conjunction windows tested | 1,389 | 376 | 1,013 |
| Expected aligned conjunctions on usable data | 23.4 | 8.2 | 15.2 |
| Expected detected self-lensing pulses (if all WD) | 0.22 | 0.15 | 0.07 |
| Expected detected 1 % eclipses (if opaque companion) | 4.2 | 2.7 | 1.4 |
| Expected detected 5 % eclipses (if opaque companion) | 9.7 | 3.8 | 5.9 |
| Windows with pulse p < 0.003 (expected false alarms 4.2) | 4 | 2 | 2 |
| Windows with dip p < 0.003 (expected false alarms 4.2) | 2 | 0 | 2 |
| Vetted conjunction signals | 0 | 0 | 0 |

Six windows pass the threshold. This agrees with the false-alarm expectation. Visual vetting (`results/window_vetting_notes.csv`) shows that four are steps at data gaps or scattered-light ramps. The other two are short eclipses of an inner binary in Gaia DR3 2272770494020883328. These eclipses recur every 3.03 d in five sectors (below our periodic-search threshold). They are not a single event at the outer conjunction.

Interpretation: TESS FFI photometry cannot test WD self-lensing in this sample. The median pulse recovery is 2 %. The pulses are 0.1 to 0.8 % for 0.2 to 0.6 d, against sky-dominated noise at G of about 14. Absence of a deep eclipse at 23 aligned conjunctions is a stronger result. It does not agree with companions that are single opaque bodies of stellar size: the expected number of 5 % eclipses is 9.7, and 0 occur. This agrees with dark (WD) companions. In a triple, the two inner stars move on an inner orbit of several solar radii, so their transits at the outer conjunction can be shorter, multiple or absent. Thus the RCE result is only a weak, model-dependent constraint on triples.

### 2. Eclipsing binaries occur only in the RCE class (Figures 2a and 3)

| Test | RCE | NCE | p (one-sided) |
| --- | --- | --- | --- |
| Gaia DR3 `vari_eclipsing_binary` (all 9,786) | 21 / 6,620 | 0 / 3,166 | 2.7 x 10^-4 (Fisher); 6 x 10^-4 (stratified permutation) |
| TESS periodic eclipses (261 near-edge-on systems) | 12 / 189 | 0 / 72 | 0.019 (Fisher) |

The 12 TESS eclipsing systems (`results/tess_eclipsing_systems.csv`) have periods of 1.12 to 5.62 d. Gaia DR3 2300756878878756480 has a period of 0.417 d, which agrees with its Gaia DR3 period of 0.41683 d. Eclipse depths are 0.26 to 8 % of the total light. Most show two nearly equal eclipses per orbit, as expected for a pair of similar stars. The difference-image centroids are 1 to 7 arcsec from the target (pixel size 21 arcsec). The exception is Gaia DR3 3607734737223982208, at 13 arcsec. Gaia DR3 5551128170748701696 has a G = 13.7 neighbour at 12 arcsec, and its signal is quasi-sinusoidal (not counted). The inverted-flux control gives detections in only three systems, all with real periodic variability. Two other Gaia DR3 eclipsing binaries in the TESS set give SDE 8.5 to 10 at aliases of their Gaia periods (just below our threshold). Thus our threshold is conservative.

The 21 Gaia eclipsing binaries have periods of 0.22 to 1.55 d (mostly contact-binary periods). In 8 of 21, the Gaia model depth of the primary eclipse is more than 0.15 mag. A faint companion pair in a triple cannot give such a deep eclipse of the total light. For those systems, the eclipsing pair probably supplies most of the light. Then the astrometric "primary" is itself a close binary, and its single-star mass is wrong. Both cases put an additional close stellar binary in the RCE systems. This agrees with the conclusion of Shahaf et al. that RCE systems are often not WD binaries.

### 3. Outer orbits of eclipsing systems are closer to edge-on (Figure 2b)

For the 21 Gaia eclipsing systems, mean |cos i| of the outer orbit is 0.295 (median 0.254). For the 6,599 other RCE systems it is 0.519 (median 0.538). Mann-Whitney p = 1.6 x 10^-4. The permutation p for the mean is 5 x 10^-5. The KS test against isotropic orbits gives p = 5 x 10^-4. 71 % of the eclipsing systems have |cos i| < 0.3, against 27 % of the others. The Gaia uncertainty of cos i for these systems is small (median 0.028). For an inner eclipse cutoff |cos i_in| < 0.3 or 0.5, the Rayleigh mutual-inclination scale is about 20 degrees (approximate 95 % range 15 to 30 degrees). For a cutoff of 0.75 the scale is smaller (2 to 15 degrees). Isotropic orientation is rejected (2 delta lnL = 11). These are approximate grid likelihoods from 21 systems.

## Limitations

- The conjunction test has low power for self-lensing. A null result does not limit the WD fraction. The eclipse expectation assumes one opaque body of stellar size at the outer conjunction. Inner-binary motion in triples weakens this assumption.
- Stellar radii come from a simple main-sequence mass-radius relation and the Shahaf et al. primary masses. The alignment probability uses a Gaussian approximation to the cos i distribution and assumes that the Gaia covariances are correct. Gaia DR3 uncertainties can be underestimated. The total expected number of aligned conjunctions does not depend strongly on this.
- The pooled false-alarm calibration treats all light curves as equivalent after the per-light-curve normalisation. Windows at sector edges are more often affected by systematics. We removed such events by vetting, not by the statistic.
- The TESS eclipse comparison uses only the near-edge-on subset, with 1 to 7 sectors per system. The NCE count is small (72), so the TESS test alone gives p = 0.019. RCE systems are at lower Galactic latitude and more crowded, but difference images put the eclipses on the targets.
- Catalogue cross-matches with VSX and the TESS eclipsing-binary catalogue failed, because VizieR mirrors were not reachable from the host. Thus some of the 11 eclipsing systems that are not in the Gaia DR3 table can be known in other catalogues. We do not claim discovery priority.
- We did not obtain spectra or radial velocities. Thus we cannot say which component eclipses in each system.
- The orientation test uses Gaia's own eclipse classification, which depends on magnitude and number of epochs. This selection does not depend on the outer-orbit inclination.

## Reproduction

1. Create a Python 3.12 environment with numpy, scipy, pandas, astropy, astroquery, matplotlib and nsstools 0.1.12. Set OMP_NUM_THREADS=1.
2. Download `https://arxiv.org/src/2309.15143v2` and extract `table_I.dat` to `raw/arxiv_src/x/`. Check its hash in `provenance.json`.
3. Run the scripts in `code/` in numeric order from a work directory that contains `code/`, `data/`, `raw/`, `results/` and `scratch/`. Network steps are 01, 03, 05, 08 and 15. To skip step 01, use `data/gaia_nss_tableI.csv.gz`. Step 05 downloads about 18 GB. The seeds are fixed. `code/12_vet_plot.py` makes the vetting plots.
4. To check only the main statistics without downloads, run `code/16_eb_stats.py`, `code/17_coplanarity.py` and `code/18_mutual_inclination.py` on the included files, and run `code/22_final_stats.py` on the included result tables.

## Files

- `code/`: all analysis scripts.
- `data/`: Gaia inputs, orbit Monte Carlo summaries (`orbit_summary.csv` for all 9,786 systems; `orbit_summary_refined.csv` with values for each conjunction), sector coverage, dilution, box-least-squares results, combined window results, and cutout hashes.
- `results/`: summary statistics, window and injection tables, vetting tables and notes, eclipsing-binary lists, orientation tests, and figures.
- `lightcurves/`: derived light curves (`.npz`: time in BTJD, flux in three apertures, ring flux, sky, centroids) for all sectors of the 13 eclipsing systems (12 plus the sub-threshold 2272770494020883328) and for the vetted systematic windows.
- `provenance.json`: data sources, retrieval dates, hashes, software versions, job and model data.

## References

- Shahaf S. et al. 2024, MNRAS 529, 3729: Triage of the Gaia DR3 astrometric orbits. II. A census of white dwarfs (arXiv:2309.15143).
- Shahaf S. et al. 2023, MNRAS 518, 2991: Triage of the Gaia DR3 astrometric orbits. I (arXiv:2209.00828).
- Yamaguchi N., El-Badry K., Sorabella N. 2024: A search for self-lensing binaries with TESS (arXiv:2410.13939).
- Gaia Collaboration, Arenou F. et al. 2023, A&A 674, A34: Gaia DR3 stellar multiplicity (arXiv:2206.05595).
- Mowlavi N. et al. 2023, A&A 674, A16: Gaia DR3 first catalogue of eclipsing-binary candidates (arXiv:2211.00929).
- Brasseur C. E. et al. 2019: Astrocut / TESScut (ascl:1905.007).
