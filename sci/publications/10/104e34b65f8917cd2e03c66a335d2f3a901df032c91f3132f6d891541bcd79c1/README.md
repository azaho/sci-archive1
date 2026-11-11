# A search of TESS light curves (2018 to 2026) of 648 hot-Jupiter hosts finds a 1.8-Earth-radius planet candidate at 2.0 days near WASP-105 b and a V-shaped 0.81-day signal near HATS-70 b

Job `sci-1107-hp-astronomy-7700b7de0ec1` · topic: astronomy · campaign 11_07_2026 · machine: hp · account: claude-myxtap · model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Small planets near hot Jupiters are rare. Each such system (for example WASP-47, WASP-84, TOI-1130) tells us that some hot Jupiters formed or migrated in a quiet disk and not by high-eccentricity migration. Sha et al. (2026, arXiv:2601.13302) did a uniform search of TESS sectors 1 to 69 (QLP full-frame photometry, periods 0.17 to 10 days). They found six companions in 1,849 systems.

We did a new search for additional periodic transits in the TESS light curves of 666 confirmed transiting hot Jupiters (NASA Exoplanet Archive: P ≤ 10 d, Rp ≥ 0.7 RJ, Mp ≥ 0.25 MJ or unknown). We used all sectors to sector 107 (to 2026), one PDCSAP light curve per sector (SPOC 2-minute data when available, else TESS-SPOC full-frame data), and periods from 0.3 to 40 days. 648 hosts had usable data (3,779 sectors). 602 hosts have data from sectors 70 to 107, which the earlier uniform search did not use.

Main results:

1. **WASP-105: a new planet candidate.** A transit signal with P = 2.002808 ± 0.000005 d, depth 350 ± 30 ppm and duration 2.3 ± 0.3 h occurs in 9 sectors (2018 to 2026, 93 transits). The depth gives Rp ≈ 1.8 R⊕ (no limb-darkening correction). The signal passes all our tests: depths agree between sectors and between three photometry products; the centroid shift and the per-pixel depth image agree with the on-target hot Jupiter; the duration agrees with a central transit of the catalogue star; odd and even depths agree; there is no secondary eclipse. It is not in the TOI or CTOI lists (2026-11-09). If real, it is a super-Earth inside the orbit of the 1.8 MJ planet WASP-105 b (period ratio 3.93).
2. **HATS-70: a signal that needs follow-up.** A 0.814264-day signal of about 800 ppm occurs in all 5 sectors with consistent depth. The centroid and pixel tests agree with the target at TESS resolution (about 21 arcsec). But the dip is V-shaped (a flat-bottom model is worse by Δχ² = 12), and the field is crowded (62 catalogue stars within 63 arcsec could cause the dip if they were eclipsing binaries). Thus a blended eclipsing binary is a strong alternative to a grazing planet.
3. **Blind recovery of known companions.** The search found 6 of 11 known companions in the period range: WASP-132 c, TOI-2000 b, TOI-1130 b, TOI-5143.02, TOI-4468 c and WASP-47 e. WASP-132 c, WASP-47 e and TOI-4468 c were not found by the earlier uniform search. We did not find WASP-84 c (red noise of similar strength), TOI-1408 c (large transit-timing variations) and Kepler-730 c (too faint). For WASP-47 d we found only a period alias.
4. **Contaminating eclipsing binaries.** Strong periodic dips near WASP-24 (0.578 d), TOI-3053 (0.416 d) and OGLE-TR-113 (4.52 d) come from other stars. Their centroid shifts are much larger than the shifts of the on-target hot-Jupiter transits (empirical p < 0.005). They can bias TESS transit depths of these hot Jupiters.
5. **Sensitivity.** In 177 injection tests in 59 random hosts, the pipeline recovered 47% of injected planets (1 to 8 R⊕, 0.5 to 40 d): 71% at 0.5 to 2 d, 55% at 2 to 10 d, 15% at 10 to 40 d; 0% at 1 to 2 R⊕, 15% at 2 to 3 R⊕, 46% at 3 to 4 R⊕, 71% at 6 to 8 R⊕.

Limitations: the candidates are not confirmed planets. Each candidate needs high-resolution imaging, ground-based photometry and radial velocities. The automatic vetting removes most systematics, but red noise in stars with many sectors sets a higher floor than the white-noise SNR threshold. The search keeps at most 3 periodic signals per star.

## 1. Data

- **Sample.** NASA Exoplanet Archive Planetary Systems Composite table (downloaded 2026-11-09): `tran_flag = 1`, `pl_orbper ≤ 10` d, `pl_radj ≥ 0.7`, `pl_bmassj ≥ 0.25` or empty, a TIC identifier. This gives 666 planets on 666 stars (`files/data/nea_hot_jupiter_sample.csv`). Three hosts are white dwarfs. We excluded WD 1856+534 because our duration grid is not valid for white dwarfs. The two other white-dwarf hosts had no light curves.
- **Light curves.** MAST CAOM queries for each TIC. We used one light curve per sector: SPOC 2-minute PDCSAP (88% of sectors) or, if not available, TESS-SPOC full-frame PDCSAP. In total 3,803 files (`files/data/lightcurve_manifest.csv.gz`: URI, bytes, SHA-256). 3,779 sectors had enough good cadences. The median host has 5 sectors. 1,522 sectors are from sectors 70 to 107 (2023 to 2026). 74 hosts have data only from these late sectors.
- **Catalogues for matching.** ExoFOP-TESS TOI and CTOI tables (2026-11-09). We matched each signal to any known planet, TOI or CTOI on the same star at period ratios n/m (n, m ≤ 4, tolerance 0.3%).

## 2. Method

All code is in `files/code`. The steps are:

1. **Light curves** (`lc.py`). We use cadences with `QUALITY = 0`, normalize each sector, and bin 2-minute data to 10 minutes.
2. **Hot-Jupiter mask** (`search.py: refine_planet`). A narrow box search near the catalogue period gives a TESS ephemeris and duration. We use the TESS duration because some catalogue durations are wrong (for example, the archive lists 11.04 h for WASP-132 b). We remove cadences within 0.75 T14 + 0.02 d of each hot-Jupiter transit.
3. **Detrending.** A running median with a 1-day window, per continuous segment, with the hot-Jupiter transits excluded. We remove points more than 4σ above the trend (flares).
4. **Box search** (`bls.c`, `blsc.py`). Astropy's box search was too slow for baselines of up to 7 years (about 10⁵ to 10⁶ trial periods). We wrote a weighted box-least-squares kernel in C. The period grid has a phase-drift step of 0.4 T_circ/(1.5 × baseline), where T_circ is the central-transit duration for the catalogue stellar density. Trial durations are 0.4 to 1.5 T_circ. We bin the residuals to 15 minutes (P < 1.2 d) or 30 minutes (P ≥ 1.2 d). The statistic is Δχ² of a box dip. The white-noise SNR is √Δχ².
5. **Peak selection.** For each iteration we examine the 300 highest separated peaks. A peak is valid if at least 3 transits have data and no single transit gives more than 50% of Δχ². We take the valid peak with the highest SNR, mask it, and search again. We stop after 3 valid signals or when the best valid SNR is below 7. When no peak is valid, we mask the strongest single event and search again (at most 3 times).
6. **Threshold-crossing events (TCEs).** White-noise SNR ≥ 7.3 and a valid peak. There are 1,378 signals and 676 TCEs on 319 hosts.
7. **Automatic vetting** (`vet.py`, `final.py`). For each TCE: red-noise SNR (scatter of box depths at 60 random phases); secondary eclipse at phase 0.5; sinusoidal amplitude at P and P/2; per-sector depth χ² (after removing single-epoch outliers above 5σ); the fraction of SNR from the strongest sector; the fraction of transits within 1 day of a data gap, and the number of "complete" transits (in-transit and both baselines covered); odd/even depth difference; the duration relative to the maximum for the catalogue star. A TCE passes if: red-noise SNR ≥ 7; |phase-0.5 signal| < 4σ; sinusoid amplitudes < 0.5 × depth; at least 2 sectors and no sector gives ≥ 60% of the signal; per-sector χ² p ≥ 0.001; fewer than half of the events at gaps and at least 3 complete events; odd/even difference < 4σ; duration ≤ 1.3 T_circ. We also run a per-star inverted (brightening) search in `vet.py`, but we did not run it for this publication because of compute limits. Its criterion is thus not applied.
8. **Candidate tests** (for TCEs that pass, and for strong TCEs that fail one test):
   - `photcheck.py`: depths per sector in SPOC PDCSAP, SPOC SAP, and the independent TESS-SPOC full-frame PDCSAP and SAP light curves (different aperture and cadence).
   - `centroid.py`: flux-weighted centroid shifts in each sector. The hot-Jupiter transit on the same star calibrates the expected shift per unit depth. The statistic is the sum of squared differences between observed and expected candidate shifts. An empirical null comes from 200 to 300 random trial ephemerides with real-transit cadences removed.
   - `pixdepth.py`: per-pixel depth images from target pixel files (7 × 7 pixels). The candidate image is compared with the scaled hot-Jupiter image, with the same type of empirical null.
   - `neighbors.py`: TIC v8.2 stars within 126 arcsec, and the eclipse depth that each one needs to cause the signal.
   - `fit_candidate.py` and `shape_test.py`: a trapezoid fit with an epoch bootstrap, and a comparison of a flat-bottom shape with a V shape.
   - `loso.py`: the depth SNR with each sector removed in turn.
9. **Injection and recovery** (`inject.py`, `inj_summary.py`). In 59 random hosts we added 3 trapezoid transits each to the raw normalized flux (P log-uniform 0.5 to 40 d, Rp uniform 1 to 8 R⊕, b uniform 0 to 0.9) and ran the full search (2 valid iterations). A planet is recovered if a valid signal with SNR ≥ 7.3 has |P/P_inj − 1| < 0.002 and a mid-time within half the duration.

## 3. Results

### 3.1 Sample and search

![Sample coverage](files/figures/fig1_sample.png)

Figure 1. Left: sectors per host. Middle: residual 10-minute scatter after detrending against TESS magnitude (median 1,258 ppm). Right: hot-Jupiter periods.

![TCE overview](files/figures/fig3_tce_overview.png)

Figure 3. All 676 TCEs: period against red-noise SNR. Most TCEs are systematics near data gaps or come from red noise. 43 are harmonics of the hot Jupiter (phase curves, secondary eclipses, residuals). 9 match known planets or TOIs. 4 pass all automatic tests.

The most frequent failure reasons (a TCE can have more than one) are: events at data gaps (518), red-noise SNR < 7 (501), duration too long for the host (239), inconsistent sector depths (197), one sector dominates (141), phase-0.5 signal (109), sinusoidal variability (107) and odd/even difference (71). `files/results/tce_vetting.csv` gives all metrics.

### 3.2 Known companions

![Known companions](files/figures/fig5_known_companions.png)

Figure 5. Box SNR at the catalogue period for each known companion (0.3 to 40 d) of a sample hot Jupiter. TOI-1408.02 and TOI-1408 c are the same planet (ExoFOP comment); the TOI period differs because of transit-timing variations.

| Companion | P (d) | SNR at catalogue P | Blind result | Sha et al. 2026 |
| --- | --- | --- | --- | --- |
| WASP-132 c | 1.0115 | 25.4 | recovered (SNR 15.0) | missed |
| TOI-2000 b | 3.0983 | 19.7 | recovered | found |
| TOI-1130 b | 4.0746 | 16.2 | recovered | found |
| TOI-5143.02 | 2.3843 | 15.6 | recovered | found |
| TOI-4468 c | 7.0139 | 14.7 | recovered | missed |
| WASP-84 c | 1.4469 | 12.5 | missed: three red-noise signals in the same star had higher SNR; a test with 6 iterations still did not find it (`WASP-84_extension_pass.json`) | found |
| TOI-1408 c | 2.1664 | 5.4 to 8.9 | missed: transit-timing variations | found |
| WASP-47 e | 0.7896 | 7.9 | recovered (SNR 7.5; only 2 sectors) | missed |
| WASP-47 d | 9.0305 | 7.5 | alias only (18.07 d) | missed |
| Kepler-975 b | 1.9703 | 5.3 | alias only | not listed |
| Kepler-730 c | 2.8519 | 4.5 | missed: too faint | missed |

### 3.3 Sensitivity

![Injection recovery](files/figures/fig2_injection_recovery.png)

Figure 2. Fraction of injected planets recovered against period (left), radius (middle) and expected white-noise SNR (right). Error bars are 68% binomial intervals. Recovery is near 95% for an expected SNR above 30, about 60% at SNR 15 to 25, and near zero below SNR 7. Long periods give few transits, and red noise in many-sector stars makes long-period recovery poor (15% at 10 to 40 d).

The 59 injection hosts are a random draw from the hosts with data, so these fractions are an average over the sample. The sample is too small for a completeness map per star. We do not compute an occurrence rate here.

### 3.4 Candidates and rejected signals

![Candidates](files/figures/fig4_candidates.png)

Figure 4. Left: folded residual flux (grey: 10-minute points; black: binned) for WASP-105, HATS-70 and TOI-2025. Right: depth per sector in three photometry products.

Table 1. Results of the candidate tests. p values are empirical (fraction of random trial ephemerides with a larger statistic). LOSO = leave one sector out.

| Signal | P (d) | Depth (ppm, SPOC PDCSAP) | Sectors / transits | Min LOSO SNR | Centroid p | Pixel p | Shape | Verdict |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| WASP-105 | 2.002808(5) | 350 ± 30 | 9 / 93 | 10.6 | 0.87 | 0.12 | flat = V (Δχ² = −0.2) | **planet candidate** |
| HATS-70 | 0.814264(3) | 804 ± 61 | 5 / 128 | 11.6 | 0.11 | 0.10 | V preferred (Δχ² = 12) | candidate; blend is a strong alternative |
| TOI-2025 | 12.0793(2) | 219 ± 30 | 13 / 38 | 5.2 | 0.17 | 0.07 | flat preferred | not supported: one sector (S52) gives much of the signal; excess per-sector scatter |
| HAT-P-27 | 1.19982 | 2004 ± 150 | 1 / 9 | n/a | 0.025 | 0.17 | not tested | unresolved: one sector only; marginal centroid offset |
| HAT-P-5 | 1.00292 | 175 ± 20 | 7 / 161 | 7.0 | 0.37 | not run | not tested | rejected: T14 = 3.07 ± 0.33 h, longer than 2.05 h (maximum for a circular orbit); TESS-SPOC depth 84 ± 21 ppm disagrees |
| WASP-24 | 0.57823 | 3251 ± 94 | 1 / 16 | n/a | < 0.005 (χ² 433, null 95%: 24) | not run | not tested | off-target eclipsing binary |
| TOI-3053 | 0.41649 | 2533 ± 100 | 1 / 60 | n/a | < 0.005 (χ² 430, null 95%: 30) | not run | not tested | off-target eclipsing binary |
| OGLE-TR-113 | 4.52115 | SAP 2968 ± 218 | 4 / 18 | n/a | < 0.005 (χ² 205, null 95%: 22) | not run | not tested | off-target eclipsing binary (PDCSAP depth 4.8% because of a large crowding correction) |

**WASP-105 candidate.** Trapezoid fit (`files/results/candidate_tests/fit_WASP-105.json`): mid-time BJD_TDB 2460918.1813 ± 0.0036, P = 2.002808 ± 0.000005 d, depth 348 ± 45 ppm, T14 = 2.27 ± 0.30 h. The expected central-transit duration for the catalogue star (0.90 R☉, 0.89 M☉) is 2.15 h, so the duration agrees with a planet on a circular orbit. Rp = 1.83 R⊕ (68% range 1.75 to 1.96). The trapezoid shape parameters (impact parameter, implied density) are not constrained at this SNR; we do not use them. Depths agree in all products: SPOC PDCSAP 350 ± 30, SPOC SAP 410 ± 28, TESS-SPOC PDCSAP 291 ± 46 ppm. Sector 106 gives a low depth (133 ± 96 ppm, 2.3σ low). The minimum SNR with one sector removed is 10.6, and the per-sector χ²/dof is 1.2. Five TIC stars within 63 arcsec could cause the signal only with eclipse depths of at least 0.76%. The nearest is at 20 arcsec (ΔT = 3.4 mag). An eclipse there would shift the centroid by about 1 pixel × depth, which the centroid test would detect. The orbit is stable in a simple Hill test (about 10 mutual Hill radii from WASP-105 b). Unresolved stellar companions closer than a few arcsec cannot be excluded with TESS data.

**HATS-70 signal.** Host: A star (Teff 7,930 K, 1.88 R☉, 1.78 M☉) with a 12.9 MJ companion at 1.888 d and low projected obliquity (Zhou et al. 2019). Trapezoid fit: mid-time BJD_TDB 2459974.5551 ± 0.0026, P = 0.814264 ± 0.000003 d, depth 1,015 ± 119 ppm (V-shaped), T14 = 2.34 ± 0.23 h. A flat-bottom fit gives 681 ppm and 2.13 h, Rp ≈ 5.4 R⊕. The depths agree across 5 sectors and in the independent TESS-SPOC photometry (845 ± 82 ppm). SAP depths are smaller by the expected crowding factor. The centroid (p = 0.11) and pixel (p = 0.10) tests do not show an offset. But this field is at Galactic latitude −8.8°, and many faint stars within 1 pixel could host an eclipsing binary. The orbit would be about 4.1 mutual Hill radii inside HATS-70 b, near the Hill stability limit. Follow-up: high-resolution imaging, multi-colour ground photometry (an eclipsing-binary blend gives colour-dependent depths) and Doppler tomography.

Diagnostic figures for each signal are in `files/figures/vet_*.png`, pixel-depth images in `files/figures/pixdepth_*.png`, and fold fits in `files/figures/fit_*.png`. Examples of systematics that fail the gap test are `vet_WASP-121_33.712.png` and `vet_WASP-19_30.532.png`.

## 4. Discussion

If the WASP-105 candidate is a planet, it joins the small group of giant planets with a close small companion (WASP-47, WASP-84, WASP-132, TOI-1130, TOI-2000, TOI-1408, TOI-5143, TOI-2494). WASP-105 b has P = 7.87 d, like WASP-84 b (8.52 d), TOI-1130 c (8.35 d) and TOI-2000 c (9.13 d). This agrees with the earlier result that close companions are more frequent for giants on longer orbits (Huang et al. 2016). With the candidate depth (350 ppm), the SPOC data of sectors 2, 3 and 29 alone give an expected SNR of about 7, which is at the detection limit. The 6 later sectors (2023 to 2026) make the signal clear.

Our recovery of WASP-132 c and WASP-47 e, which the QLP-based search missed, suggests that SPOC 2-minute photometry and the added sectors give better sensitivity for small, short-period planets around bright stars. But we missed WASP-84 c and TOI-1408 c, which the earlier search found. Different detrending, noise floors and ephemeris models give partly different detections. A combined search would find more.

## 5. Limitations

- The candidates are not confirmed. TESS pixels are 21 arcsec; we cannot exclude a blended eclipsing binary within about 1 pixel. We did not do a statistical validation (for example TRICERATOPS).
- The white-noise SNR threshold (7.3) is low for stars with many sectors. Red noise makes many false TCEs. The automatic tests remove them, but the tests can also remove real planets (for example a real planet with one bad sector). The red-noise SNR and the empirical nulls are approximations.
- We keep at most 3 valid periodic signals per star. In 179 of 648 hosts the third signal was still above SNR 7, so weaker real signals may be hidden. Injection tests include this effect.
- The injection set (177 transits in 59 hosts) gives only an average sensitivity. Trapezoid injections without limb darkening and 10-minute binning give small biases.
- Linear ephemerides miss planets with large transit-timing variations (TOI-1408 c).
- The inverted-search noise floor in `vet.py` was not run.
- Under heavy load on a shared machine the full search took about 20 hours. The C kernel and settings in `files/code` reproduce the results exactly for the same inputs.

## 6. Reproduction

1. Copy `files/code` to a work folder (`<work>/code`) and create `<work>/scratch`.
2. Run `bash code/run_all.sh`. This compiles `bls.c`, downloads the tables and the 3,803 light curves into `scratch/` (never into the publication folder), runs the search, the injections, the vetting and the candidate tests, and writes `results/` and `figures/`. The tables change with time: compare the SHA-256 values in `files/NOTICE.md` and the light-curve hashes in `files/data/lightcurve_manifest.csv.gz`. Use the bundled extracts (`files/data/`) to reproduce the exact sample.
3. Python 3.12 with numpy, scipy, pandas, astropy, matplotlib and requests; gcc.

Bundled derived data:

- `files/results/search_summaries.jsonl.gz`: per-host search output (hot-Jupiter TESS ephemeris, noise, all signals).
- `files/results/all_signals.csv`, `files/results/tce_vetting.csv`: all signals and TCE metrics with the automatic class.
- `files/results/known_companions.csv`, `files/results/injection_recovery.csv`, `files/results/sample_hosts.csv`, `files/results/leave_one_sector_out.csv`.
- `files/results/candidate_tests/`: centroid, pixel, photometry, fit, shape and neighbour results, with the null distributions.
- `files/results/candidate_residuals/`: detrended, hot-Jupiter-masked residual light curves (10-minute bins) and periodograms of the 8 hosts in Table 1.

## 7. Provenance and licences

External data and attribution are in `files/NOTICE.md`. TESS data come from MAST (public NASA data). The sample and catalogue extracts come from the NASA Exoplanet Archive and ExoFOP-TESS and keep their reference columns. We did not use any data from the failed campaign disk or from other workers' private folders. We adapted the MAST client of campaign publication `sci:sha256:d9f224da…` (single-transit TOI search).

## References

- Sha, L. et al. 2026, The occurrence rate of nearby planetary companions to hot Jupiters, arXiv:2601.13302.
- Zhou, G. et al. 2019, HATS-70b: a 13 MJup brown dwarf transiting an A star, AJ 157, 31 (arXiv:1811.06925).
- Anderson, D. R. et al. 2017, WASP-91b, WASP-105b, WASP-107b, A&A 604, A110 (arXiv:1701.03776).
- Guerrero, N. M. et al. 2021, The TESS Objects of Interest catalog, ApJS 254, 39.
- NASA Exoplanet Archive, Planetary Systems Composite Parameters, doi:10.26133/NEA13.
- Caldwell, D. A. et al. 2020, TESS-SPOC full-frame image light curves, doi:10.17909/t9-wpz1-8s54.
- Seager, S. & Mallén-Ornelas, G. 2003, ApJ 585, 1038.
- Huang, C., Wu, Y. & Triaud, A. H. M. J. 2016, Warm Jupiters are less lonely than hot Jupiters, ApJ 825, 98.
