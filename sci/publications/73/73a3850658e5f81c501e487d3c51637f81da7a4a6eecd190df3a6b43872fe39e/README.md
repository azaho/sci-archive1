# eRASS1 detects X-rays 2.3 times more often in Gaia white-dwarf-candidate astrometric binaries than in matched single stars; the excess is in hot-white-dwarf systems with 0.2-0.5 d TESS periods

Job: sci-1107-dell-astronomy-c8e477750a78 (campaign 11_07_2026, topic astronomy, machine dell). Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim. Date of work: 2026-11-12.

## Summary

Shahaf et al. (2024) used Gaia DR3 astrometric orbits (periods 45 to 1,000 days) to find 9,786 binaries whose faint companion is not a single main-sequence star. They divided the sample with Gaia synthetic photometry: systems with no red colour excess (NCE, probable white-dwarf (WD) companions) and systems with a red excess (RCE, probable hierarchical triples). A campaign study (sci:sha256:6350aef7...) found close eclipsing binaries only in the RCE class.

We used a different and independent signal: coronal X-rays. We compared the eROSITA eRASS1 stellar identifications (HamStar v1.1, Freund et al. 2024) of 5,080 Shahaf systems in the eRASS1-DE half sky with 10 matched single stars per system (matched in G, BP-RP, parallax, ecliptic latitude and Galactic latitude). We also tested 12,866 Gaia astrometric binaries whose companion is securely a main-sequence star (class I, "ABI").

Main results:

1. **X-ray excess in WD candidates.** eRASS1 detects 33 of 1,592 NCE systems. Matched single stars give 14.2 expected detections. The ratio is 2.3 (95% bootstrap interval 1.6-3.3; Poisson p = 1.4e-5). RCE systems give 123 against 39.4 expected (ratio 3.1, 2.6-3.7). ABI systems give no excess: 372 against 402 expected (ratio 0.92, 0.83-1.02).
2. **The NCE excess is in systems with a hot WD.** For primaries below 0.95 solar masses, 10 of 54 NCE systems with the GALEX near-UV excess of Shahaf et al. are X-ray sources. Only 6 of 475 NCE systems with GALEX data and no UV excess are X-ray sources (Fisher p = 2.7e-7). The RCE systems with UV excess give 1 of 38 (NCE against RCE, p = 0.019). About half of the total NCE excess (9.8 of 18.8 excess detections) comes from the 55 UV-excess systems.
3. **The X-ray emitters are kinematically old.** X-ray detected NCE systems have a median tangential velocity of 37 km/s. X-ray detected matched single stars have 22 km/s (Mann-Whitney p = 5e-4). X-ray detected RCE systems are also old (33 against 23 km/s, p = 1e-5). X-ray detected ABI systems have the same kinematics as their detected single stars (24 against 24 km/s, p = 0.56). Thus youth does not explain the NCE and RCE activity.
4. **TESS shows short periods with large amplitude.** In single-sector TESS full-frame-image photometry, 19 of 32 X-ray detected NCE systems show a period below 6 d, and 10 show a period below 1 d. In 28 X-ray detected RCE systems, 10 show a period below 6 d and none below 1 d (Fisher p = 9e-4). The NCE amplitudes are larger (median 2.0 % against 0.4 %, p = 0.018), so the signal comes from the dominant star. All five X-ray detected NCE systems with a hot-WD UV colour (GALEX FUV-NUV < 0.3) have periods of 0.236, 0.330, 0.332, 0.390 and 0.540 d.
5. **One hidden inner binary is confirmed by Gaia velocities.** In Gaia DR3 6416572288572864512 the Gaia RV range (79 km/s) is 4.6 times the range from the astrometric orbit (17 km/s). The 0.3896-d TESS signal is present in sectors 13, 27 and 103 (2019-2026). For the other 14 X-ray detected NCE systems with Gaia RV data, the RV range agrees with the astrometric orbit.
6. **The X-ray spectra are coronal.** eRASS1 band counts give a median hardness HR1 = 0.68 for the detected NCE systems and 0.60 for their detected single stars. No UV-excess NCE system has a supersoft spectrum (HR1 < -0.8). Thus photospheric emission from the WD does not cause the detections.

Interpretation: in Gaia WD-candidate binaries, X-ray activity occurs mainly when the WD is hot, that is, young as a WD. The active stars rotate (or orbit) with periods of 0.2-0.5 d, and they are kinematically old. Two explanations agree with these data: (a) the main-sequence star received mass and angular momentum when the WD formed and now spins fast (accretion spin-up, as proposed for blue lurkers and barium dwarfs); or (b) the hot WD is in a hidden post-common-envelope binary with the visible star, and the astrometric orbit comes from a third body. Gaia RVs favour (b) for one system. We cannot separate (a) and (b) for the others with the present data. The ABI null result shows that astrometric binarity alone does not cause X-ray emission.

## Question

Most of the 3,166 NCE systems of Shahaf et al. (2024) are thought to be main-sequence stars with WD companions at about 1 au. Such orbits are too wide for tides to spin up the main-sequence star. Thus, in an old system, the main-sequence star should be as X-ray quiet as a single star of the same age. Strong X-ray emission at a rate above that of matched single stars needs another cause: youth, spin-up by mass transfer when the WD formed, or a hidden close binary (a triple). We asked:

- Do eRASS1 X-ray detection rates of NCE, RCE and ABI systems differ from those of matched single stars?
- Which system properties (WD temperature from UV, period, primary mass, red-excess probability) carry the excess?
- Do kinematics, Gaia RVs, eRASS1 hardness and TESS light curves separate youth, spin-up and hidden close binaries?

The campaign record had no X-ray test of these systems. The closest prior campaign work is the eclipsing-binary test of the same sample (sci:sha256:6350aef75d67a6f30a959d6a7e67a1d722a609a2423c9f5212547bb343a64f02). We found no published X-ray study of the Shahaf et al. sample in a web search (2026-11-12).

## Data

All sources are public. We do not redistribute third-party records. `files/provenance.json` gives URLs, retrieval dates and SHA-256 hashes.

- Shahaf et al. (2024) Table I (9,786 systems; primary mass, Pr(red)) and Table II (GALEX NUV/FUV and UV-excess flag), from the arXiv source tarball 2309.15143v2. NCE means Pr(red) < 56 %.
- HamStar v1.1 (Freund et al. 2024): Bayesian identifications of eRASS1 Main sources with Gaia DR3 stars ("Likely" 149,311 rows and "Possible" 23,900 rows). Shared campaign copies: `datasets/erosita-dr1-hamstar-likely-v1.1` and `datasets/erosita-dr1-hamstar-possible-v1.1`.
- eRASS1 Main catalogue v1.1 (Merloni et al. 2024): band counts (0.2-0.5, 0.5-1, 1-2 keV) for 643 detected sources, read with HTTP byte ranges (no full download; `code/erass1_rows.py`).
- Gaia DR3 (ESA archive TAP, 2026-11-12): `nss_two_body_orbit` (86,284 orbital solutions with Galactic longitude >= 179.9 deg), `binary_masses`, `gaia_source` (a 1,207,648-star single-star pool: `non_single_star = 0`, RUWE < 1.4, parallax > 0.45 mas, parallax/error > 5, G 5-17, `random_index` < 6e7), `vari_rotation_modulation`, `vari_eclipsing_binary`, `vari_classifier_result`.
- Mamajek main-sequence table (version 2022.04.16) for the class-I bound of the astrometric mass-ratio function.
- TESS full-frame-image cutouts from MAST TESScut (80 files; 9 x 9 pixels; the earliest available sector of 78 stars, plus two later sectors of one star).

## Method

**Samples** (`code/03_samples.py`). We used all Shahaf systems with Galactic longitude >= 179.9 deg (the eRASS1-DE sky): 1,592 NCE and 3,488 RCE systems. We computed the photocentre semi-major axis from the Thiele-Innes constants and the astrometric mass-ratio function (AMRF). For the control class ABI we took Gaia orbital solutions that are not in Table I, with primary mass 0.45-1.2 solar masses, period below 1,000 d, and the parallax, significance, goodness-of-fit and colour-magnitude ranges of Table I. We required AMRF < 0.8 times the maximum AMRF of a single main-sequence companion (computed from the Mamajek mass-luminosity relation). All 5,080 Table I systems are above this maximum (minimum ratio 1.06), which validates the bound.

**Matched controls and X-ray flags** (`code/04_match_xray.py`, `code/05_stats.py`). For each system we took the 10 nearest single stars in scaled coordinates (G/0.25 mag, BP-RP/0.05 mag, log parallax/0.04, ecliptic latitude/3 deg, Galactic latitude/5 deg). Ecliptic latitude sets the eRASS1 exposure. Mean differences between targets and controls are below 0.07 mag in G, 0.01 mag in BP-RP and 0.07 mas in parallax. A star is "detected" if it is a HamStar Likely counterpart (any rank). Variants: Likely or Possible; Likely rank 1 only. The ratio is the target detection rate divided by the mean control rate. The 95 % interval comes from 4,000 bootstrap resamples of the targets with their controls.

**Kinematics** (`code/06_gaia_extra.py`, `code/13_summary.py`). Tangential velocity = 4.74 x total proper motion / parallax. We compared X-ray detected targets with all X-ray detected matched controls.

**Hidden close binaries in Gaia RVs** (`code/08_orbit_rv.py`, `code/09_rv_noise.py`). For a dark companion the photocentre orbit is the orbit of the visible star. We computed its RV semi-amplitude K1 from the astrometric orbit. We simulated the Gaia RV range (`rv_amplitude_robust`) for random epochs with the orbit plus epoch noise. The noise is the median epoch scatter of single control stars in bins of G_RVS and BP-RP (Student-t, 4 degrees of freedom). An RV range with simulated p < 0.002 marks an RV excess, that is, a probable inner close binary. For ABI and RCE stars the companion light makes the photocentre orbit smaller than the stellar orbit, so their flags are only indicative.

**eRASS1 hardness** (`code/07_erass1_bands.py`, `code/14_hardness.py`). HR1 = (C2 - C1)/(C2 + C1) with ML counts C1 (0.2-0.5 keV) and C2 (0.5-1 keV).

**TESS** (`code/10_tesscut.py`, `code/11_tess_rotation.py`, `code/15_neighbours.py`, `code/17_tess_summary.py`). We used all 33 X-ray detected NCE systems (32 have data), 30 random X-ray detected RCE systems with primary mass below 0.95 solar masses (28 have data), and 15 random NCE systems with UV excess and no X-ray detection (14 have data). We made 3 x 3 pixel aperture photometry with a ring background, removed a linear trend in each orbit, clipped 5-sigma outliers, and ran a Lomb-Scargle search from 0.1 to 12 d. A signal is significant if its false-alarm probability is below 0.001 and P < 6 d. We divided the amplitude by the share of target flux in the aperture, which we estimated from Gaia neighbours within 63 arcsec.

## Results

### 1. Detection rates (Figure 1, `results/rates_subgroups.csv`)

| Group | N | Detected | Expected from controls | Ratio (95 % CI) |
| --- | --- | --- | --- | --- |
| NCE | 1,592 | 33 | 14.2 | 2.32 (1.56-3.31) |
| RCE | 3,488 | 123 | 39.4 | 3.12 (2.58-3.71) |
| ABI | 12,866 | 372 | 402.4 | 0.92 (0.83-1.02) |
| NCE with UV excess | 55 | 10 | 0.2 | 50 (14-75) |
| NCE, GALEX, no UV excess | 650 | 6 | 5.6 | 1.07 (0.36-1.90) |
| NCE, no GALEX match | 887 | 17 | 8.4 | 2.02 (1.05-3.33) |
| NCE, P < 300 d | 233 | 14 | 4.3 | 3.26 (1.61-5.88) |
| NCE, P >= 300 d | 1,359 | 19 | 9.9 | 1.92 (1.11-3.01) |
| NCE, primary < 0.75 solar masses | 261 | 15 | 3.3 | 4.55 (2.22-8.62) |
| NCE, primary >= 0.95 solar masses | 336 | 2 | 2.0 | 1.00 (0-3.57) |
| NCE, Pr(red) < 30 % | 543 | 15 | 5.2 | 2.88 (1.57-4.71) |
| NCE, Pr(red) 30-56 % | 1,049 | 18 | 9.0 | 2.00 (1.08-3.24) |

The results do not change with the detection definition: Likely or Possible gives NCE 2.18 (1.43-3.08), RCE 2.99, ABI 0.93; Likely rank 1 gives NCE 2.56, RCE 3.24, ABI 0.97 (`results/rates_det*.json`). The NCE ratio does not increase toward the RCE boundary (Pr(red) 30-56 % gives a smaller ratio than Pr(red) < 30 %). Thus contamination by RCE-like triples near the colour boundary does not explain it.

### 2. UV excess and X-rays (Figure 2)

For primaries below 0.95 solar masses: NCE with UV excess 10/54 detected; NCE with GALEX data and no excess 6/475; RCE with UV excess 1/38; RCE with GALEX data and no excess 30/389. Thus the UV excess predicts X-rays only in the NCE class. If chromospheric activity caused the UV excess, RCE systems with UV excess would also be X-ray sources. Among 36 NCE UV-excess systems with an FUV detection, 21 have FUV-NUV < 0.3 (a WD hotter than about 15,000-20,000 K); 5 of these 21 are X-ray sources. The dark-companion masses of the 10 detected UV-excess systems are 0.32-0.63 solar masses (median of all NCE: 0.61).

### 3. Kinematics (Figure 3)

| Class | Detected targets: median v_t (km/s) | Detected matched single stars | Mann-Whitney p (one-sided) | Fraction v_t > 50 km/s (targets / controls) |
| --- | --- | --- | --- | --- |
| NCE | 37.1 (n = 33) | 21.6 (n = 131) | 5e-4 | 0.27 / 0.11 |
| RCE | 33.1 (n = 123) | 22.9 (n = 333) | 1e-5 | 0.28 / 0.13 |
| ABI | 24.2 (n = 372) | 23.9 (n = 1,212) | 0.56 | 0.12 / 0.13 |

X-ray detected single stars at these distances are mostly young. X-ray detected NCE and RCE systems are kinematically like the older field population. The ABI result shows that the test does not create a difference for binaries in general.

### 4. Gaia RV test for hidden inner binaries (Figure 4)

| Class | Stars with RV range | RV excess, all | X-ray detected with RV range | RV excess among detected |
| --- | --- | --- | --- | --- |
| NCE | 180 | 1 | 15 | 1 |
| RCE | 409 | 26 | 76 | 20 |
| ABI | 4,359 | 226 | 219 | 59 |

In RCE and ABI systems, an RV excess is strongly linked to X-ray detection (26 % of detected against 1.5-4 % of non-detected). This agrees with active, tidally locked inner binaries in triples. If the detected NCE systems behaved like detected RCE and ABI systems, we would expect 4.0 RV excesses in 15; we see 1 (binomial p = 0.06). The test covers only bright stars (G_RVS < 12), so it gives weak evidence.

### 5. TESS periods (Figures 5 and 6, `results/tess_summary.json`, `results/nce_xray_tess_candidates.csv`)

| Group | Stars | Significant, P < 6 d | P < 1 d | Median amplitude (significant) |
| --- | --- | --- | --- | --- |
| NCE, X-ray detected | 32 | 19 | 10 | 2.0 % |
| RCE, X-ray detected (primary < 0.95 solar masses) | 28 | 10 | 0 | 0.41 % |
| NCE, UV excess, not detected | 14 | 4 | 1 | 1.7 % |

The NCE signals are near-sinusoidal at the Lomb-Scargle period. Folding at twice the period does not show unequal minima, so ellipsoidal variation is not likely. We see no eclipses. Two hot-WD systems (6298526800365669632 and 6416572288572864512) have a sharp maximum and a flat minimum. This shape agrees with irradiation of a companion by a hot WD (a reflection effect), but spots can also make it. For 6416572288572864512 the per-sector periods are 0.38961, 0.38988 and 0.38928 d; S13 and S27 combine coherently (joint power 0.52, equal to the single-sector powers).

### 6. X-ray hardness (`results/hardness_summary.csv`)

| Group | n | median HR1 | quartiles | HR1 < -0.8 |
| --- | --- | --- | --- | --- |
| NCE, detected | 34 | 0.68 | 0.36-1.00 | 1 |
| NCE controls, detected | 143 | 0.60 | 0.35-0.89 | 2 |
| NCE with UV excess, detected | 10 | 0.41 | 0.22-0.63 | 0 |
| RCE, detected | 128 | 0.63 | 0.40-0.90 | 1 |
| RCE controls, detected | 361 | 0.69 | 0.41-1.00 | 7 |

The UV-excess systems are slightly softer but not supersoft. Their emission is coronal.

## Discussion

The X-ray excess of NCE systems is real, independent of the detection definition, and concentrated in systems whose WD is hot. A hot WD has a short cooling age (below about 0.1-0.3 Gyr for FUV-NUV < 0.3). The WD masses of 0.3-0.6 solar masses need progenitors that lived more than about 1 Gyr, or binary stripping, and the kinematics are not young. Thus, in these systems, the activity began when the WD formed, not when the system formed. This link supports a binary-interaction origin of the activity.

Two mechanisms remain:

- **Accretion spin-up.** Mass transfer or wind accretion from the WD progenitor spun up the main-sequence star. Magnetic braking then slows the star on a time scale similar to the WD cooling time for the hot-WD subset. This explanation predicts large projected rotation velocities (for P = 0.24-0.54 d, equatorial velocities of about 45-170 km/s for 0.5-0.8 solar-radius stars), no RV variation at the TESS period, and slow loss of phase coherence.
- **Hidden post-common-envelope binaries in triples.** The visible star and the hot WD form a 0.2-0.5 d binary. Another dark body (for example a second WD) makes the astrometric orbit. This explanation predicts RV variations of tens of km/s at the TESS period, a reflection effect that is stronger in red light, and strict phase coherence. Gaia DR3 6416572288572864512 agrees with this case.

Both mechanisms make the NCE sample less "clean" than a set of simple WD + main-sequence binaries with au orbits. Activity of the main-sequence star must be considered in any use of these systems as age or mass-transfer probes. The RCE result supports the triple interpretation of Shahaf et al. (2024) and the campaign eclipse result: X-ray detected RCE systems often show RV excesses, kinematically old ages and small, diluted TESS signals, as expected for active inner pairs of faint stars.

## Limitations

- HamStar is a probabilistic catalogue. Some identifications can be wrong or can belong to a neighbour. We used the same identifications for targets and controls, so chance coincidences cancel to first order.
- eRASS1-DE covers only half of the sky. The detection limit (about 5e-14 erg/s/cm2) allows only active stars (L_X above about 1e29-1e30 erg/s at the median NCE distance of about 540 pc). We did not use upper limits.
- Controls are clean single stars (RUWE < 1.4, no Gaia non-single-star solution). Unresolved binaries in the general population are therefore not in the control pool. The ABI ratio of 0.92 shows that this choice does not create an excess for binaries in general. ABI binaries with P < 300 d have a ratio of 0.80 (0.66-0.94); we do not have an explanation for this small deficit.
- The UV-excess flag and FUV-NUV colours come from Shahaf et al. (2024) Table II (GALEX AIS). We did not re-derive them. GALEX covers only part of the sample.
- The RV test uses Gaia `rv_amplitude_robust` and an empirical noise model. It covers only stars with G_RVS < 12 (15 X-ray detected NCE systems). Its power is low.
- TESS: one sector per star (30-min or 10-min cadence for most), 3 x 3 pixel apertures with crude dilution estimates. Signals with low target flux share (for example 5243252098795757952, share 0.51, amplitude 12 %) can come from a neighbour. We did not do pixel-level centroid tests. Periods above about 6 d are not reliable.
- We did not get spectra. Thus we cannot separate spin-up from hidden close binaries in most systems.
- CDS services (SIMBAD, VizieR) were not reachable from the host. Thus some candidates can be known in catalogues we could not check. We do not claim priority for any single object.

## What remains open

- Spectroscopy of the 5 hot-WD X-ray systems and of the other short-period NCE systems in `results/nce_xray_tess_candidates.csv`: RV curves at the TESS period and projected rotation velocities separate the two mechanisms directly.
- Multi-sector TESS phase-coherence tests and multi-band (ZTF g/r or Gaia epoch BP/RP) amplitude ratios (reflection effects are stronger in red light; spots are stronger in blue light).
- The same test with Gaia DR4 orbits and the full eRASS:5 depth when they are public.

## Reproduction

1. Use Python 3.12 with numpy, scipy, pandas, astropy, matplotlib, statsmodels and requests (versions in `provenance.json`).
2. Make an empty work directory, copy `files/code/` to `code/`, and run `bash code/run_all.sh`. The script downloads the inputs into `raw/` and `scratch/` (outside the signed bundle) and writes `results/`. Gaia TAP needs the `MAXREC` parameter (included in `code/tap.py`); without it anonymous jobs stop at 50,000 rows. TESScut cutouts take about 1 min each. The Gaia single-star pool is a random subset (`random_index` < 6e7), so exact control draws are reproducible.
3. `files/results/` contains all aggregate results that the README quotes. The figures come from `code/12_figures.py` and `code/17_tess_summary.py`.

## Files

- `code/`: all analysis scripts and `run_all.sh`.
- `results/rates_subgroups.csv`, `results/rates_det*.json`: detection rates and ratios.
- `results/summary.json`: UV-link tests, kinematics, RV test, activity levels, dark masses.
- `results/hardness_summary.csv`, `results/rv_noise_model.csv`, `results/tess_summary.json`.
- `results/nce_xray_tess_candidates.csv`: Gaia DR3 identifiers of the 32 X-ray detected NCE systems with TESS data, with our TESS period, amplitude, aperture flux share, and flags (UV excess from Shahaf et al. 2024; Gaia RV excess from our test).
- `figures/fig1`-`fig6`: PNG figures.
- `provenance.json`: sources, URLs, hashes, versions, job and model data.
- `EXTERNAL_DATA_NOTICE.md`: attribution and terms of the external data.

## References

- Shahaf S. et al. 2024, MNRAS 529, 3729 (arXiv:2309.15143): Triage of the Gaia DR3 astrometric orbits. II. A census of white dwarfs.
- Freund S. et al. 2024, A&A 684, A121 (arXiv:2401.17282): The SRG/eROSITA all-sky survey. Identifying the coronal content with HamStar.
- Merloni A. et al. 2024, A&A 682, A34: The eROSITA DR1 all-sky survey.
- Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1: Gaia DR3.
- Gaia Collaboration, Arenou F. et al. 2023, A&A 674, A34: Gaia DR3 stellar multiplicity.
- Halbwachs J.-L. et al. 2023, A&A 674, A9: Gaia DR3 astrometric binary star processing.
- Katz D. et al. 2023, A&A 674, A5: Gaia DR3 radial velocities.
- Pecaut M. J. and Mamajek E. E. 2013, ApJS 208, 9.
- Brasseur C. E. et al. 2019, Astrocut (ascl:1905.007).
- Campaign: sci:sha256:6350aef75d67a6f30a959d6a7e67a1d722a609a2423c9f5212547bb343a64f02.
