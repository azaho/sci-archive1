# A TESS 2-minute search of 4,265 white dwarfs within 100 pc finds no new on-target transiting planet; it recovers WD 1856+534 b, finds a new blended M-dwarf eclipsing binary, and shows that asteroids cause many single dips

## Summary

We searched TESS 2-minute SPOC light curves of white dwarfs (WDs) within 100 pc for transits and eclipses. The sample has 4,265 Gaia WDs (4,311 TIC targets). The data are 22,150 sector light curves from sectors 1 to 107.

The main results are:

1. The search recovers the known giant planet WD 1856+534 b (P = 1.408 d) with high significance. This is our positive control.
2. The search finds no new periodic transit or eclipse that is on the WD. Of 276 WDs with a transit-like detection, automated tests remove 259. Manual inspection removes 16 of the 17 remaining WDs. The last WD is WD 1856+534.
3. Most strong detections come from other stars in the aperture. In the median sector, the WD supplies only 34 % of the flux in the photometric aperture (CROWDSAP). The SPOC crowding correction then scales a small dip from a neighbour into a deep "transit" of the WD.
4. Difference imaging shows that a 17.1235 d eclipse in the aperture of GALEX J081240.0-760437 (TIC 804762481) comes from the M dwarf Gaia DR3 5210617837762868864, 20 arcsec from the WD. We found no entry for this eclipsing binary in SIMBAD, VSX, the Gaia DR3 eclipsing-binary table or the Gaia DR3 non-single-star orbit table. We report it as a new eclipsing-binary candidate.
5. The same method shows that a 9.135 d signal in the aperture of HE 0330-0002 comes from the known eclipsing binary HD 22064, 107 arcsec away. This is a second test of the method.
6. Many isolated single dips occur when an asteroid moves near the target. The background pixels increase, the background subtraction becomes too large, and the target flux decreases. At 26 of 200 dip times, a known asteroid brighter than V = 16 is among the three nearest asteroids within 6 arcmin. At 200 control times, this occurs 0 times (Fisher exact p = 1.3e-8).
7. Injection-recovery tests give the search completeness. With these data, we set 95 % upper limits on the fraction of WDs that have a transiting-size planet. For 4 to 15 Earth radii and P = 0.15 to 1 d, the limit is 1.7 %. For 1 to 4 Earth radii and P = 0.15 to 1 d, the limit is 9.2 %. For 4 to 15 Earth radii and P = 1 to 13 d, WD 1856+534 b gives a median rate of 4.3 % (95 % upper limit 12 %).

## Provenance of this work

- Job: sci-1107-hp-astronomy-d71e39b0c59a. Campaign: 11_07_2026. Topic: astronomy. Machine: hp.
- Model: Claude Opus 5.5 (claude-opus-5-5), which worked as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis dates: 2026-11-07 to 2026-11-08.
- The campaign shared dataset store did not contain astronomy data. We downloaded all inputs from public archives (see "Data and retrieval").

## Question

TESS observed several thousand WDs at 2-minute cadence. A planet or a small star that passes in front of a WD blocks a large fraction of its light for a few minutes to about one hour. Only one transiting giant planet (WD 1856+534 b) and some debris systems are known. We asked:

- Does a uniform search of all public TESS 2-minute WD light curves (sectors 1 to 107) find new transiting planets, eclipsing companions or unexplained dips?
- What are the main sources of false signals, and can we explain them physically?
- What completeness does the search have, and which occurrence limits follow?

## Method

### Sample

1. We took the Gaia EDR3 WD catalogue of Gentile Fusillo et al. (2021), with P_WD > 0.75 and parallax > 10 mas (16,676 WDs).
2. We matched these WDs to the TESS 2-minute target lists of sectors 1 to 56 (radius 3 arcsec, positions at epoch 2015.5 and 2000.0). We removed matches where TESS magnitude minus Gaia G is outside -1.5 to +1.0. 4,315 TIC targets remained.
3. For these TIC targets, we took all SPOC 2-minute light curves from the MAST bulk download scripts of sectors 1 to 107. This gave 22,150 files for 4,313 TIC targets. All downloads were successful. We kept TIME, PDCSAP_FLUX, PDCSAP_FLUX_ERR, QUALITY, SAP_FLUX, SAP_BKG, MOM_CENTR1/2 and the header keyword CROWDSAP. We recorded the SHA-256 of each FITS file.

Limitation: WDs that TESS first observed at 2-minute cadence after sector 56 are not in the sample. Their later light curves are included only if TESS also observed them in sectors 1 to 56.

### Light-curve cleaning

For each sector, we used QUALITY = 0 cadences. We divided PDCSAP flux by its median and by a running median of 0.3 d. We removed upward outliers above 4 robust standard deviations (flares, cosmic rays). We also removed dips deeper than 1.5 + 5 robust standard deviations. An occultation cannot remove more than the full flux of the target, so such dips are not physical.

### Periodic search (BLS)

- We used astropy BoxLeastSquares on 6-minute bins. The durations were 6, 10, 16, 25, 40 and 60 minutes. The period range was 0.15 to 13 d. The frequency grid is dense enough for WD transit durations (phase error smaller than about 2/3 of the duration for duration = 0.008 d x P^(1/3)).
- Because of the compute limit (one CPU per job), we ran BLS on the first and last sector of each target. This is 8,073 sectors. Each sector has at least two transits for P < 13 d.
- We kept three peaks per sector and masked rational aliases (a/b with a <= 10, b <= 5) of stronger peaks.
- Detection: depth SNR >= 9 and SDE >= 12. We set these thresholds before we inspected candidates.

### Vetting

Automated tests on each detection:

- Shape: we compared a box model with a two-harmonic sinusoid at the same period. We rejected detections where the box does not fit at least two times better (in delta chi-squared).
- Periodogram: we rejected detections where the Lomb-Scargle peak is at P/n (pulsation or rotation).
- Physical depth: we rejected a fitted depth >= 1.3. A depth larger than the full WD flux shows that the signal comes from another star, or that the data have a systematic error.
- Duration: we rejected durations longer than 1.3 times the maximum eclipse duration of the WD by a companion with radius <= 0.5 solar radii. We used the mass-radius relation of Nauenberg (1972).
- Repetition: we searched each other sector of the same target at the same period (+/- 0.2 %). We rejected detections that did not repeat with SNR > 7 in any other sector.
- We also recorded single-event dominance, odd/even depth difference, secondary eclipse, centroid shifts and background change.

We inspected the 17 remaining WDs by eye. For candidates that repeat in many sectors, we stacked all sectors and measured the depth of each event. Where necessary, we downloaded target pixel files and made difference images (mean out-of-eclipse image minus mean in-eclipse image). We fitted a 2-D Gaussian to the difference image and compared its position with Gaia DR3 sources. We searched SIMBAD (CfA mirror), VSX and Gaia DR3 for catalogue entries.

### Single-dip search

We applied a box matched filter (4, 10 and 30 minutes) to all 22,113 usable sectors at 2-minute resolution. For dips with z > 8, we counted dips in other targets of the same sector within 0.1 d. Such coincidences show spacecraft systematics. For the 200 strongest isolated dips, we queried IMCCE SkyBoT for known asteroids within 6 arcmin of the target, with TESS as the observer (code C57). We used the dip time and a control time 3 d away in the same sector.

### Injection-recovery and occurrence limits

We injected 1,200 transits into real cleaned sectors that we chose at random from the BLS set. The model is an exact two-circle overlap of an opaque planet and a uniform WD disk, with 2-minute exposure smearing. We drew P log-uniform in 0.15 to 13 d, Rp log-uniform in 0.3 to 15 Earth radii and the impact parameter uniform over transiting geometries. The WD mass came from the catalogue. Then we ran the same BLS and the same automated cuts. A recovery is a peak within 0.2 % of P, P/2 or 2P that passes the cuts. For each bin, the expected number of detections is N_WD x mean(p_transit x recovered), with N_WD = 4,265. We then used a Poisson likelihood with a flat prior.

## Results

### Detection funnel

| Step | Count |
| --- | --- |
| BLS sectors searched | 8,073 |
| TIC targets searched with BLS | 4,311 |
| TIC targets with any detection (SNR >= 9, SDE >= 12) | 525 |
| TIC targets with a transit-like or odd/even detection (vetted) | 276 |
| rejected: periodogram peak at P/n | 39 |
| rejected: sinusoid fits as well as box | 58 |
| rejected: depth >= 1.3 | 100 |
| rejected: duration too long for a WD eclipse | 30 |
| rejected: no repetition in other sectors | 32 |
| passed automated vetting, inspected by eye | 17 |
| new on-target periodic transit or eclipse | 0 |
| known planet recovered (WD 1856+534 b) | 1 |

Full table: `files/results/funnel.csv`. Per-target reasons: `files/results/classification.csv`.

### Result of manual inspection (17 WDs)

| TIC | WD | Result |
| --- | --- | --- |
| 267574918 | WD 1856+534 | Known planet. BLS P = 1.40797 d (sector 14). Repeats in 12 of 12 other sectors tested. |
| 804762481 | GALEX J081240.0-760437 | Blend. New eclipsing binary candidate Gaia DR3 5210617837762868864 (see below). |
| 453828065 | HE 0330-0002 | Blend. Known eclipsing binary HD 22064 (VSX EA, P = 9.134881 d), 107 arcsec away. Difference imaging puts the dip source 5 to 19 arcsec from HD 22064 and 100 to 109 arcsec from the WD. |
| 1201364356 | BD+76 614B | Blend with the bright primary BD+76 614 (G = 9.5, 5.7 arcsec, Gaia variable flag). The eclipses last several hours. The WD supplies 0.6 % of the aperture flux. |
| 1101440031, 6087507 | BD+30 2592B, BD+22 879C | Blend with a bright primary star, plus noise at data-segment edges. |
| 321768853, 281574678, 67812488, 1717843537, 1101874829 | | Systematics at data-segment edges. They do not repeat. |
| 283414280 | | One deep event controls the signal. It does not repeat. |
| 357686299, 320936968, 219826764, 60878053 | | Low SNR. They repeat in at most 1 of 3 to 12 other sectors. |
| 1100360772 | LP 560-73 | Weak single-sector signal (SNR 9 to 10, about 2 h at P = 4.28 d). There are no other sectors. Not confirmed. |

Plots: `files/results/vet_manual/`.

### New eclipsing binary in the aperture of TIC 804762481

The BLS first found P = 8.566 d. A stack of all 14 sectors (2020 to 2025) shows eclipses only at even epochs. The odd-epoch depth is 0.007 +/- 0.010 and the even-epoch depth is 0.384 +/- 0.009. Thus the true period is 17.12 d. A trapezoid fit to all sectors (eclipses masked during detrending) gives:

| Parameter | Value |
| --- | --- |
| P | 17.123503 +/- 0.000019 d |
| T0 | BTJD 2037.7911 +/- 0.0014 (BJD_TDB - 2457000) |
| T14 | 2.52 +/- 0.08 h |
| Depth (relative to the crowding-corrected WD flux) | 0.42 +/- 0.01 |
| Secondary eclipse at phase 0.5 | depth < 0.059 (3 sigma, same units) |

Difference images in sectors 39, 65, 93 and 97 put the dip source 0.9 to 2.5 arcsec from Gaia DR3 5210617837762868864. This star has G = 16.39, BP-RP = 2.79, parallax 6.40 mas (156 pc), Teff_gspphot = 3,380 K and RUWE 0.99. The dip source is 18 to 23 arcsec (9 to 19 sigma) from the WD. The TESS camera orientation is different in each sector, but the fitted position stays on the same Gaia source. Thus the eclipse is on the M dwarf, not on the WD. The absolute magnitude of the M dwarf (M_G = 10.4) is approximately 0.5 to 0.8 mag above the main sequence for its colour. Two similar M dwarfs can cause this, but our comparison is approximate. The eclipse lasts 2.5 h and has a long ingress (ingress fraction 0.52). This agrees with a grazing eclipse in a binary of two low-mass stars. A spectroscopic orbit is necessary to confirm the system.

We could not measure the eclipse depth on the M dwarf, because we did not model the fraction of its flux in the WD aperture.

### Single dips and asteroids

- 1,672 sector light curves have a single dip with z > 8. 774 of these dips occur within 0.1 d of dips in at least two other targets of the same sector. This shows that most dips are spacecraft or scattered-light systematics.
- For the 200 strongest isolated dips, 26 dip times have a known asteroid with V < 16 among the three nearest asteroids within 6 arcmin. The control times have 0 such cases (Fisher exact p = 1.3e-8). 40 dips have a background excess larger than 5 robust sigma within 0.15 d.
- Example: TIC 37993251 in sector 98. The asteroid (1342) Siegena (V = 11.5) was 176 arcsec from the target at the dip time. The background increased, the SAP flux decreased below zero, and then the SAP flux increased when the asteroid passed through the aperture (figure `fig_examples.png`, right panel).
- Explanation: a bright moving object in the background annulus makes the background estimate too large. SPOC subtracts this background from the target pixels, so the target flux decreases. This can look like a deep transit of the WD that lasts 0.5 to 2 h.
- We did not vet the remaining isolated dips one by one. `files/results/single_events_z8.csv` and `files/results/asteroid_test.csv` contain them.

### Completeness and occurrence limits

| Rp (Earth radii) | P (d) | Injections | Completeness | mean(p_tr x C) | Detections | Median rate | 95 % upper limit |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0.3 to 1 | 0.15 to 1 | 176 | 0.07 | 0.0010 | 0 | 0.17 | 0.74 |
| 0.3 to 1 | 1 to 13 | 207 | 0.04 | 0.0001 | 0 | 1.2 | 5.4 |
| 1 to 4 | 0.15 to 1 | 151 | 0.40 | 0.0076 | 0 | 0.021 | 0.092 |
| 1 to 4 | 1 to 13 | 245 | 0.26 | 0.0013 | 0 | 0.13 | 0.55 |
| 4 to 15 | 0.15 to 1 | 182 | 0.84 | 0.0406 | 0 | 0.004 | 0.017 |
| 4 to 15 | 1 to 13 | 239 | 0.65 | 0.0091 | 1 | 0.043 | 0.12 |

The rate is the number of planets per WD in each bin, for a population that is log-uniform in P and Rp inside the bin. For planets smaller than 1 Earth radius, the data give no useful constraint.

## Figures

- `files/figures/fig_examples.png`: positive control (WD 1856+534 b, 23 sectors folded on the Vanderburg et al. 2020 ephemeris) and two false-positive types.
- `files/figures/fig_diffimage_804762481.png`: difference images that put the 17.12 d eclipse on the M dwarf.
- `files/figures/fig_eb_804762481.png`: folded eclipse and secondary-eclipse scan.
- `files/figures/fig_follow_804762481.png`: odd/even epochs, depth of each event and centroid shifts.
- `files/figures/fig_diffimage_453828065.png`: difference images that put the HE 0330-0002 signal on HD 22064.
- `files/figures/fig_completeness.png`: injection-recovery.
- `files/figures/fig_sample.png`: noise and crowding of the sample.

## Limitations

- BLS used only the first and last sector of each target (8,073 of 22,113 usable sectors). The repetition test used up to 12 more sectors. A multi-sector BLS would be more sensitive to shallow signals.
- The period range is 0.15 to 13 d. Single transits of longer-period bodies are only in the single-dip list, and we did not vet them one by one.
- The completeness uses the automated cuts only. The shape, periodogram, duration and repetition tests were not applied to the injections. Real transits normally pass these tests, but the true completeness can be slightly lower.
- The depth cut (>= 1.3) assumes that the SPOC crowding correction is approximately correct. If CROWDSAP is too small by more than 30 %, a real total occultation of the WD can fail this cut.
- About 64 % of sectors have CROWDSAP < 0.5. For these WDs, a real WD transit and a blend can look the same in the light curve. Only pixel data or higher-resolution data can separate them. We made difference images only for the multi-sector candidates.
- The ZTF test was not informative. We folded ZTF photometry on single-sector TESS ephemerides. The period errors over the 6-year ZTF baseline are too large, and even WD 1856+534 b shows no ZTF dip with this method (`files/results/external_checks.csv`). Gaia neighbour queries failed (HTTP 503) for most targets in that step. We repeated the Gaia queries by hand for the two difference-imaging targets.
- The asteroid test reports only the three nearest asteroids at each epoch, so the V < 16 count is a lower limit.
- The sample is the TESS 2-minute target list, which depends on guest-investigator proposals. It is not a volume-complete sample.

## Data and retrieval

No shared-store dataset was used. The external inputs are:

| Input | Source | Record in this package |
| --- | --- | --- |
| Gaia EDR3 WD catalogue | VizieR J/MNRAS/508/3877/maincat (CfA mirror), query: Pwd > 0.75 and Plx > 10 | `data/gf21_wd_100pc.tsv.gz`, SHA-256 in `data/gf21_wd_100pc_sha256.txt` |
| TESS 2-minute and 20-second target lists, S1 to S56 | https://tess.mit.edu/wp-content/uploads/all_targets_S###_v1.csv and all_targets_20s_S###_v1.csv | `data/tess_targetlists_sha256.txt` |
| MAST bulk light-curve scripts, S1 to S107 | https://archive.stsci.edu/missions/tess/download_scripts/sector/tesscurl_sector_N_lc.sh | `data/mast_lc_download_scripts_sha256.txt` |
| 22,150 SPOC light curves | MAST URLs | `data/lc_urls.csv.gz`, SHA-256 per FITS file in `data/lc_sha256.tsv.gz` |
| 6 target pixel files | MAST URLs | `data/tpf_urls.txt`, `data/tpf_sha256.txt` |
| Gaia DR3 neighbours | ESA Gaia TAP | `results/gaia_nb_*.csv` |
| Asteroid positions | IMCCE SkyBoT conesearch, observer C57 | `results/asteroid_test.csv` |
| Object types | SIMBAD (CfA mirror), VSX (VizieR CfA mirror) | `results/external_checks.csv`, text above |

## Reproduce

Software: Python 3.12 with the versions in `files/code/requirements.txt`. Set OMP_NUM_THREADS=1.

1. Make a work directory with sub-directories `code`, `data`, `results`. Copy `files/code/*.py` into `code`.
2. Download the WD catalogue to `data/gf21_wd_100pc.tsv`:
   `https://vizier.cfa.harvard.edu/viz-bin/asu-tsv?-source=J/MNRAS/508/3877/maincat&-out=GaiaEDR3,RA_ICRS,DE_ICRS,Plx,e_Plx,pmRA,pmDE,Gmag,BP-RP,Pwd,TeffH,loggH,MassH,TeffHe,MassHe&Pwd=>0.75&Plx=>10&-out.max=unlimited`
3. Download the target lists to `data/targetlists/` and the MAST scripts to `data/scripts/` (URLs above). Compare them with the SHA-256 lists.
4. Run `code/01_crossmatch.py`. Then build `data/lc_urls.csv` (or use the copy in this package) and run `code/02_download.py` (about 2.5 h, 14 GB of FITS that the script reduces to 8 GB of npz files).
5. Run `03_search.py 0 2` and `03_search.py 1 2` (about 3 CPU-hours each), `04_inject.py 1 600` and `04_inject.py 2 600`, `05_candidates.py`, `06_vet.py`, `08_refine.py`, `07_external.py survivors_auto.csv`, `11_completeness.py`.
6. Run the follow-up: `13_follow_804762481.py [TIC P]`, `14_diffimage.py` (needs the TPFs in `data/tpf/`), `15_eb_ephemeris.py`, `09_single_plots.py`, `10_asteroids.py 200`, `16_classify.py`, `12_figures.py`.

The compressed files `results/search_shard*.jsonl.gz`, `results/inject_*.jsonl.gz` and `results/bls_peaks.csv.gz` contain the raw search and injection output. Thus you can check all later steps without the light curves.

## References

- Gentile Fusillo N. P. et al. 2021, MNRAS 508, 3877 (Gaia EDR3 WD catalogue).
- Vanderburg A. et al. 2020, Nature 585, 363 (WD 1856+534 b).
- Ricker G. R. et al. 2015, JATIS 1, 014003 (TESS).
- Kovacs G., Zucker S., Mazeh T. 2002, A&A 391, 369 (BLS).
- Astropy Collaboration 2022, ApJ 935, 167.
- Gaia Collaboration, Vallenari A. et al. 2023, A&A 674, A1 (Gaia DR3).
- Nauenberg M. 1972, ApJ 175, 417 (WD mass-radius relation).
- Berthier J. et al. 2006, ASP Conf. Ser. 351, 367 (SkyBoT).
- Watson C. L. et al. 2006, VSX.
- "The frequency of transiting planetary systems around polluted white dwarfs", 2024, arXiv:2407.21743 (TESS transit search of 313 polluted WDs; related prior work).
