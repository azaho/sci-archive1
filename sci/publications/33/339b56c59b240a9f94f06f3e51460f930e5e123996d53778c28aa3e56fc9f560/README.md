# TESS 2-minute light curves from 2018 to 2026 show no beta Pictoris-like exocomet transits in 24 other spectroscopic exocomet host stars

## Summary

Many A-type stars show variable absorption lines that astronomers attribute to evaporating exocomets ("falling evaporating bodies"). Only beta Pictoris (beta Pic) has many photometric exocomet transits in TESS data: Lecavelier des Etangs et al. (2022) list 30 events in 156 days of 2018-2021 data. HD 172555 has one CHEOPS transit. Nobody has done a systematic search of TESS data for the other spectroscopic hosts.

We did this test. We used all SPOC 2-minute light curves (sectors 1 to 107, July 2018 to August 2026) of the 30 stars in Table 1 of Iglesias et al. (2025). 29 stars have 2-minute data (169 sector light curves). We also used 52 control A stars that have no exocomet reports (222 light curves). The controls match the hosts in TESS magnitude, effective temperature and number of sectors. We removed the delta Scuti pulsations, and then we searched with a matched filter. The filter uses the 1-D exocomet model of Lecavelier des Etangs et al. (2022). Brightening events, found with the same filter and the same rules, give the false-alarm rate. Fixed vetting rules remove events near data gaps, momentum dumps, flagged cadences, high or changing background, and centroid excursions. To get the completeness, we injected the 30 published beta Pic events into every light curve (24,671 injections).

Main results (threshold D >= 5, vetted):

1. **beta Pic 2018-2021 (positive control).** The search finds 3 vetted dimming events and 1 vetted brightening event. The injection model expects 3.9 detected events. All 3 dimming events agree in time with published events (BTJD 1458.9, 1486.1 and 2177.2).
2. **24 other confirmed or candidate hosts.** The search finds **0 vetted dimming events and 3 vetted brightening events in 2,102 days**. At the beta Pic 2018-2021 rate, the expected number is **71 detected events**. The 95% upper limit on the pooled event rate is **1.9% of the beta Pic rate**. If the event depth decreases with stellar area, (R_betaPic/R_star)^2, the limit is 4.6%. Across all tested variants (thresholds 5 to 7, with and without vetting, same or radius-scaled depth, and a self-calibration to the beta Pic rate that this pipeline measures), the limit is between 2.5% and 30%.
3. **HD 172555** (the second confirmed exocomet host). We find no vetted dimming event in 7 sectors (2023-2026). The expected number is 4.8. The upper limit is 0.29 times the beta Pic rate (0.24 to 1.4 in the variants).
4. **Matched control A stars.** They give 8 vetted dimming and 13 vetted brightening events in 4,526 days. Thus the method does not make a dimming excess in ordinary A stars.
5. **beta Pic 2024-2025 (sectors 87, 95, 98; out-of-sample).** We find 0 vetted dimming events. The expected number is 3.1 (one-sided Poisson p = 0.043). This deficit is weak. It is not significant relative to the beta Pic count that this pipeline measures in 2018-2021, and it disappears at higher thresholds (p = 0.065 at D >= 6, p = 0.15 at D >= 7).
6. **All host dimming candidates with D >= 6 are instrumental.** We inspected the 10 such events outside beta Pic 2018-2021 (8 stars) and the beta Pic sector 98 event. Examples: a background spike that doubles the sky level (phi Gem, sector 45, a 0.15% dip); settling after momentum dumps (HD 172555 sector 66, 5 Vul sector 54); edges of orbits (HD 172555 sector 104, 49 Cet sector 97); scattered light (HD 85905 sector 99, beta Pic sector 98, beta Car sector 63, HD 38056 sector 107); and a PDC step after flagged data (HD 42111 sector 87).

Conclusion: in TESS broadband photometry, beta Pic-like exocomet transits at the 1e-4 to 2e-3 depth level are rare or absent in the other stars with spectroscopic exocomet signatures. The pooled rate is at least 3 times lower than the beta Pic rate, and at least 40 times lower under the primary analysis. This agrees with the idea that spectroscopy and photometry sample different comet populations (gas near the star vs dust at about 1 au), or that beta Pic is exceptional. Five candidate hosts (kappa Cen, 2 And, HD 148283, HD 42111, rho Vir) and the two false-positive hosts (HR 10, phi Leo) have zero measured completeness, mostly because of strong stellar variability; they do not constrain the result. HD 58647 has no 2-minute data.

## Figures

- `files/fig2_expected_vs_observed.png`: for each host, the expected number of beta Pic-like detections (blue) and the observed vetted dimming (orange) and brightening (gray) events.
- `files/fig1_betapic_lightcurves.png`: beta Pic light curves after pulsation removal, with the published event times and this search's detections. Sectors 5, 6 and 33 are in-sample. Sectors 87, 95 and 98 are out-of-sample.
- `files/fig4_dim_vs_bright.png`: vetted dimming and brightening events per 1000 days as a function of the threshold, for the other hosts, the controls and beta Pic.
- `files/fig3_completeness.png`: injection-recovery fraction as a function of the injected absorption depth.
- `files/results/vetting_diagnostics/*.png`: diagnostic panels (pulsation-cleaned PDCSAP flux, SAP flux, background, centroids, quality flags, other stars on the same camera) for the 11 inspected host candidates.

## Table: per-star results (threshold 5, vetted, same depth as beta Pic)

Completeness is the fraction of injected beta Pic events that the search recovers and the vetting keeps. "Expected" = (30 / 156 d) x exposure x completeness. Upper limit = 95% profile-likelihood limit on the rate ratio, with the brightening count as the false-alarm term.

| Star | Class | Tmag | Sectors | Exposure (d) | Completeness | N dim | N bright | Expected (beta Pic rate) | 95% upper limit on rate / beta Pic |
|---|---|---|---|---|---|---|---|---|---|
| delta Crv | candidate | 2.6 | 5 | 108 | 0.53 | 0 | 0 | 10.9 | 0.12 |
| HD 38056 | candidate | 6.4 | 7 | 166 | 0.29 | 0 | 0 | 9.4 | 0.14 |
| 5 Vul | candidate | 5.7 | 4 | 86 | 0.48 | 0 | 0 | 7.9 | 0.17 |
| beta Car | candidate | 2.0 | 9 | 198 | 0.21 | 0 | 0 | 7.9 | 0.17 |
| lambda Gem | candidate | 3.5 | 5 | 100 | 0.36 | 0 | 0 | 6.8 | 0.20 |
| HD 85905 | candidate | 6.2 | 7 | 146 | 0.19 | 0 | 0 | 5.4 | 0.25 |
| HD 172555 | confirmed | 4.6 | 7 | 142 | 0.17 | 0 | 1 | 4.8 | 0.29 |
| HD 37306 | candidate | 6.1 | 3 | 78 | 0.31 | 0 | 0 | 4.7 | 0.29 |
| 49 Cet | candidate | 5.6 | 3 | 75 | 0.30 | 0 | 0 | 4.3 | 0.32 |
| beta Pic 2018-2021 | confirmed | 3.7 | 7 | 148 | 0.14 | 3 | 1 | 3.9 | 1.53 |
| beta Pic 2024-2025 | confirmed | 3.7 | 3 | 77 | 0.21 | 0 | 0 | 3.1 | 0.43 |
| HD 24966 | candidate | 6.9 | 3 | 55 | 0.21 | 0 | 0 | 2.3 | 0.60 |
| HD 225200 | candidate | 6.4 | 6 | 118 | 0.07 | 0 | 0 | 1.7 | 0.80 |
| HD 138629 | unclear | 4.9 | 6 | 85 | 0.09 | 0 | 0 | 1.5 | 0.89 |
| HD 156623 | candidate | 7.2 | 6 | 126 | 0.06 | 0 | 0 | 1.5 | 0.93 |
| phi Gem | candidate | 4.9 | 5 | 100 | 0.06 | 0 | 0 | 1.1 | 1.27 |
| HD 145964 | candidate | 6.4 | 1 | 16 | 0.31 | 0 | 0 | 1.0 | 1.42 |
| c Aql | candidate | 5.7 | 2 | 30 | 0.10 | 0 | 0 | 0.6 | 2.22 |
| alpha Pic | unclear | 3.0 | 43 | 923 | 0.00 | 0 | 0 | 0.6 | 2.36 |
| HD 32297 | candidate | 8.0 | 1 | 22 | 0.08 | 0 | 0 | 0.4 | 3.77 |
| HR 4796 | candidate | 5.8 | 3 | 68 | 0.02 | 0 | 0 | 0.2 | 5.59 |
| HD 21620 | candidate | 6.2 | 1 | 14 | 0.09 | 0 | 0 | 0.2 | 5.90 |
| theta Hya | candidate | 4.0 | 4 | 77 | 0.01 | 0 | 1 | 0.2 | 6.59 |
| HD 148283 | candidate | 5.4 | 5 | 78 | 0.00 | 0 | 0 | 0.0 | - |
| 2 And | candidate | 4.9 | 5 | 115 | 0.00 | 0 | 0 | 0.0 | - |
| HR 10 | false positive | 6.1 | 4 | 84 | 0.00 | 0 | 0 | 0.0 | - |
| HD 42111 | candidate | 5.6 | 3 | 63 | 0.00 | 0 | 1 | 0.0 | - |
| kappa Cen | candidate | 2.0 | 5 | 103 | 0.00 | 0 | 0 | 0.0 | - |
| phi Leo | false positive | 4.3 | 5 | 102 | 0.00 | 0 | 0 | 0.0 | - |
| rho Vir | candidate | 4.8 | 1 | 18 | 0.00 | 0 | 0 | 0.0 | - |

Pooled results for all variants are in `files/results/pooled.csv` (vetted), `files/results/pooled_novet.csv` (no vetting) and `files/results/calibrated_limits.csv` (self-calibrated).

| Variant | Other hosts: N dim / N bright | Expected | 95% UL (same depth) | 95% UL (radius-scaled) | Self-calibrated UL (same / scaled) |
|---|---|---|---|---|---|
| vetted, D >= 5 (primary) | 0 / 3 | 71.1 | 0.019 | 0.046 | 0.025 / 0.044 |
| vetted, D >= 6 | 0 / 2 | 55.8 | 0.024 | 0.064 | 0.033 / 0.069 |
| vetted, D >= 7 | 0 / 2 | 44.5 | 0.030 | 0.086 | 0.029 / 0.058 |
| no vetting, D >= 5 | 16 / 18 | 129.7 | 0.061 | 0.137 | 0.078 / 0.116 |
| no vetting, D >= 6 | 10 / 11 | 104.4 | 0.065 | 0.154 | 0.187 / 0.304 |
| no vetting, D >= 7 | 7 / 7 | 86.3 | 0.075 | 0.190 | 0.164 / 0.288 |

## Methods

**Targets.** We used all 30 stars in Table 1 of Iglesias et al. (2025, Space Sci. Rev. 221, 122): 2 confirmed hosts (beta Pic, HD 172555), 24 candidates, 2 unclear cases (alpha Pic, HD 138629) and 2 known false positives (HR 10, phi Leo). We got the TIC IDs from the MAST TIC (brightest TIC source within 36 arcsec of the HD name) and the list of SPOC 120-s light curves from MAST (`files/code/01_targets.py`). Multi-sector data-validation products were removed. HD 58647 has no SPOC 2-minute data.

**Controls.** We selected 52 control stars from TIC dwarfs with Tmag 3-7.5 and Teff 7500-11500 K that have 2-minute targets in the TESS target lists of sectors 1-107. For each host (except beta Pic), we took 2 random stars from the 10 best matches in Tmag, Teff and number of sectors (seed 20261108; `files/code/01b_controls.py`). Controls are not checked for debris discs. One control (TIC 113583603) is an eclipsing binary (dips of 10-17%). A fixed rule (any event deeper than 1%) removes it from pooled numbers.

**Light-curve processing** (`files/code/exolib.py`, `03_search.py`). We used PDCSAP flux, QUALITY = 0, and split the data at gaps > 0.5 d. We normalized each segment. Then we found pulsation frequencies above 1.5 cycles/day by iterative prewhitening (Lomb-Scargle on a 1-day running-median residual, amplitude S/N >= 4.5, up to 80 frequencies per sector). We fit all frequencies with a cubic polynomial per segment, and subtracted only the sinusoids. Then we binned the data to 10 minutes.

**Matched filter.** For start times t0 on a 0.02-d grid and 20 templates (Delta t = 0.10, 0.20, 0.35, 0.60 d; beta = 2, 4, 8, 16, 30 per day; the Lecavelier et al. 2022 model with unit peak), we fit the template depth together with a quadratic baseline over [t0 - 0.7 d, t0 + 2.8 d] in one segment. We require 70% coverage in the event and data after the event. S = depth / formal error. We divide each template column by its robust standard deviation over all t0 in the sector (red-noise correction). D = max over templates of S (dimming). B = max over templates of -S (brightening). Peaks are local maxima separated by more than 0.5 d. A peak is removed if a stronger peak of opposite sign is within 1 d (fit "shoulders").

**Vetting rules** (`exolib.vet_flags`, `07_vet.py`). An event fails if the window [t0 - 0.5, t0 + L + 0.3] contains a gap > 0.1 d, a segment edge or a momentum dump (QUALITY bit 32). It also fails if more than 10% of cadences in [t0 - 0.3, t0 + L + 0.3] have QUALITY > 0, if the median background is more than 1.5 times the sector median, or if the background or either centroid has an excursion above 8 robust sigma relative to a quadratic fit over +-1.5 d. We set these rules after we looked at the diagnostic plots of the strongest candidates (phi Gem, HD 172555, HD 85905, 5 Vul, 49 Cet, beta Pic sector 98). Because of this, we also report all results without vetting. The same rules apply to dimming events, brightening events and injected events.

**Injection-recovery** (`04_inject.py`). In each light curve we did 24 rounds of 3 injections. The injection start times are random valid grid points where the original D < 4. Each injection uses one of the 30 Lecavelier et al. (2022) events (their K, Delta t and beta). Rounds alternate between the same depth and depth x (1.54 Rsun / R_star)^2. After the injection, we refit the pulsation amplitudes (with fixed frequencies), and we computed D within +-0.3 d of the injected start. An injection counts as recovered if D >= threshold and the vetting passes at its time.

**Statistics** (`08_stats.py`). Expected = (30 / 156 d) x exposure x completeness, with the rate from Lecavelier et al. (2022). For each unit: n_dim ~ Poisson(b + rho x Expected), n_bright ~ Poisson(b). We give the one-sided 95% profile-likelihood upper limit on rho (b profiled analytically). The self-calibrated limit multiplies this by (expected / observed) for beta Pic 2018-2021 in the same variant (`13_calibrated.py`). A fully internal two-sample ratio (`12_direct_ratio.py`) is not constrained, because the beta Pic 2018-2021 dimming-minus-brightening count (3 vs 1) is not significant by counts alone. The match of all 3 beta Pic detections to published event times shows that these detections are real. A threshold-free dimming-minus-brightening asymmetry (`10_asymmetry.py`) is too noisy to separate the groups (`files/results/asymmetry_summary.txt`).

**Detrending check** (`s1_detrend_variants.py`). Per-orbit prewhitening (15-100 or 1.5-100 cycles/day, S/N >= 4, up to 150 frequencies), with or without a 1-day cubic-spline detrend (as in Lecavelier et al. 2022), recovers the same 5-6 of the 29 covered published beta Pic events above the brightening maximum of alpha Pic and beta Pic (about 4.5). Thus the detection limit comes from red noise on 0.2-2 day time scales, not from the pulsation model. Our search detects published events with absorption depth above about 3.5e-4 well, and most events near 1e-4 to 2e-4 poorly.

## Limitations

- The search finds only the deeper part of the beta Pic event population. The 30 published events have absorption depths from 1.1e-4 to 2e-3, and the injection completeness is about 0.05-0.1 below 2e-4. The limits therefore apply to the beta Pic population as a whole, mostly through its deeper events.
- Lecavelier et al. (2022) identified their events with their own method. If some of their small events are noise, the true beta Pic rate is lower, and the limits become weaker. The self-calibrated and no-vetting variants show the size of this effect (limits up to 0.30).
- Exocomet transit depth depends on the comet orbit, tail geometry and stellar size. We test only two depth scalings. Hosts that are much larger or hotter than beta Pic (kappa Cen, HD 58647, B-type stars) are not well represented by beta Pic events.
- Seven hosts have almost zero completeness because of strong low-frequency variability (for example SPB or gamma Dor pulsation, rotation). alpha Pic, the beta Pic analog in Lecavelier et al. (2022), also has very low completeness in this pipeline.
- We set the vetting rules after we inspected candidates. They remove about 40% of the exposure. The no-vetting variant does not have this problem and gives the same conclusion.
- We used only 2-minute SPOC data. We did not use FFI-only sectors (for example HD 172555 in sector 13) or 20-second data. We did not do pixel-level (target pixel file) analysis. We checked the candidates with SAP flux, background, centroid and quality data only.
- The beta Pic 2024-2025 deficit is weak and depends on the threshold. It needs more sectors to test a real change in comet activity.

## Data provenance and reproduction

- Job: sci-1107-dell-astronomy-20a4aa0db2e5; campaign 11_07_2026; topic astronomy; machine dell; account claude-andrii; model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- TESS SPOC 2-minute light curves (product version as served on 2026-11-08/09) from `https://archive.stsci.edu/missions/tess/tid/sNNNN/...`. The exact URLs are in `files/data_provenance/products.csv` (hosts, 169 files) and `products_controls.csv` (controls, 222 files). SHA-256 hashes of all 391 FITS files are in `files/data_provenance/lightcurve_sha256.txt`. The FITS files (734 MB) are not in the bundle and are not in the shared dataset store.
- TIC v8.2 queries through astroquery 0.4.11 (`Catalogs.query_object`, `Catalogs.query_criteria`). The control pool is in `files/data_provenance/tic_bright_A.csv`.
- TESS 2-minute target lists `https://tess.mit.edu/public/target_lists/2m/all_targets_SNNN_v1.csv` (sectors 1-107), and per-sector file-name patterns from `https://archive.stsci.edu/missions/tess/download_scripts/sector/tesscurl_sector_N_lc.sh`.
- Published event parameters: Extended Data Table 2 of Lecavelier des Etangs et al. (2022), copied into `files/code/04_inject.py`. Literature PDF hashes are in `files/data_provenance/literature_pdf_sha256.txt`.
- Software: Python 3.12, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas 3.1.1, matplotlib 3.11.2, astroquery 0.4.11.

To reproduce (from a work directory that contains `code/`):

```
python code/01_targets.py data                    # needs astroquery; writes targets.csv, products list
python code/01b_controls.py $PWD                  # after the target lists and tic_bright_A.csv are in data/
python code/01c_control_products.py $PWD
bash code/02_download.sh data/products.csv data/lc
bash code/02_download.sh data/products_controls.csv data/lc_ctrl
python code/03_search.py data/lc data/npz 20
python code/03_search.py data/lc_ctrl data/npz_ctrl 20
python code/04_inject.py data/lc data/npz data/inj 22 24 data/targets.csv,data/controls.csv
python code/04_inject.py data/lc_ctrl data/npz_ctrl data/inj_ctrl 22 24 data/targets.csv,data/controls.csv
mkdir -p results && python code/05_events.py results data/npz:host data/npz_ctrl:control
python code/07_vet.py 22
python code/08_stats.py 5 6 7 ; python code/08_stats.py --novet 5 6 7
python code/13_calibrated.py ; python code/12_direct_ratio.py ; python code/10_asymmetry.py
python code/09_fig_betapic.py results/fig1_betapic_lightcurves.png ; python code/11_figures.py
python code/06_vet_plot.py <lc.fits> <t0> <label> <out.png> data/lc data/lc_ctrl
```

The injection random seeds use Python `hash()` of the file name. Set `PYTHONHASHSEED=0` to get the same injection positions in each run. In this run the hash seed was not fixed, so a rerun gives statistically equal but not identical injection tables.
