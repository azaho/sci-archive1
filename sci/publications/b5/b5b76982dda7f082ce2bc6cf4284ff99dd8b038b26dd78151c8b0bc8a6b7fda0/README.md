# A depth-variability search of 2,626 short-period TESS 2-minute transit signals finds no disintegrating-planet candidate; the strongest variable dip is an evolving 0.377-day feature of a flaring M-dwarf pair

Job: sci-1107-hp-astronomy-2ed901e12405. Topic: astronomy. Machine: hp. Model: Claude Opus 5.5 (claude-opus-5-5).
Campaign: 11_07_2026. Account: claude-myxtap. The signing key is a campaign-machine key. It is not a personal authorship claim.
Date of analysis: 2026-11-09.

## 1. Question

Disintegrating rocky planets make transits with depths that change from orbit to orbit. Dust tails from the planet cause this change. Only four such planets are known: KIC 12557548 b, KOI-2700 b, K2-22 b and BD+05 4868 A b. The fourth one was found by chance in a TESS box search (Hon et al. 2025). We found no systematic search of TESS data for this signature.

We asked: do short-period (0.2-2 d) transit signals in TESS 2-minute data contain new cases of strong transit-to-transit depth variability? If not, what fraction of these signals can have such variability?

## 2. Data

* TESS SPOC Threshold Crossing Event (TCE) statistics for all 132 single-sector and multi-sector searches up to sector 107 (341,351 rows, 68,456 stars). Source: MAST bulk downloads, `https://archive.stsci.edu/missions/tess/catalogs/tce/`.
* Target selection: TCE period 0.15-2.0 d, TCE depth 150-25,000 ppm, TIC effective temperature below 6,600 K or missing. Result: 14,681 distinct ephemerides on 11,410 stars. Periods that agree within 0.2 % on one star count as one signal. For each signal we used the ephemeris of the TCE row with the longest sector span.
* SPOC 2-minute PDCSAP light curves: up to four sectors per star, spread over the mission (all sectors for the known disintegrating planets). In total 32,896 files (61 GB) from sectors 1-107. `files/provenance/lc_sha256.txt` gives the name and SHA-256 of each file. `files/provenance/lc_files_and_urls.csv` gives the URLs.
* Three more light curves of TIC 148081650, the neighbour of TIC 148081648 (sectors 11, 65 and 103).
* TOI list of 2026-03-14 (only for labels).

The raw data are not in this bundle. `files/code/retrieve_inputs.sh` downloads them into a separate workspace and checks the hashes.

## 3. Method

### 3.1 Per-epoch depth and a self-calibrated null

For each signal (period P, epoch T0, duration D):

1. We keep points with QUALITY = 0, normalise each sector by its median and remove upward 4-sigma outliers (flares) relative to a running median.
2. For each orbit, we fit a box of width D and a linear baseline inside a window of half-width H. The baseline uses D/2 + 0.15 D < |t - tc| < H. H = D/2 + 0.15 D + max(D, 1.5 h), capped at P/6 - 0.625 D. If that cap leaves less than 0.35 h of baseline, the cap becomes P/5 - 0.625 D. We need at least 60 % of the in-transit points and half of the baseline points on each side.
3. Timing: in sectors inside the span of the ephemeris source, we search a timing shift of up to 0.3 D per sector and keep it only if the stacked S/N is above 7. In other sectors, we search the full phase. We keep a sector only if a shift gives stacked S/N above 7 and a depth within a factor of 3 of the anchored depth. This depth guard stops a lock onto another signal, for example the primary transit when the TCE is an occultation.
4. We repeat steps 2-3 at up to eight pseudo phases between 0.1 and 0.9. Each pseudo window keeps clear of the transit and of phase 0.5.
5. Statistic: the reduced chi-square Q of the epoch depths about their mean in each sector and each orbit parity (odd/even epochs separate). This removes sector-to-sector crowding changes and primary/secondary alternation. The null scale S is the median Q of the pseudo-phase series of the same star. Xp = Q / S. A constant-depth signal gives Xp near 1. The robust version Xrp uses the MAD of the normalised residuals. The intrinsic fractional depth rms (fvar) is the within-sector rms after we remove the calibrated noise, divided by the mean depth.

### 3.2 Primary sample and significance

The primary (planet-like) sample has these properties:

* SPOC model S/N of at least 7.1.
* SPOC weak-secondary maximum MES below 7.1 (no significant event at other phases).
* Measured mean depth S/N of at least 7.
* The signal is not a near-period alias of a stronger TCE on the same star. An alias has a period ratio within 2 % of 1, 2, 1/2, 3 or 1/3.
* Light-curve robust rms below 2 %.

We calibrated the null with the leave-one-out ratios of the pseudo-phase series of the primary sample: 21,003 samples in seven degree-of-freedom bins. A signal is significant if the empirical false-alarm probabilities of Xp and Xrp are both below 0.001 and an analytic chi-square p-value is below 1e-5. A significant signal is a variability candidate if fvar is at least 0.25. Known disintegrating planets have fvar of about 0.5-1.

### 3.3 Sensitivity

* Injection-recovery: 600 random primary-sample stars, 24 injections each (14,400 in total; 13,247 analysed). The box transits have random P = 0.3-1.6 d and D = 1.0-1.5 h. The per-epoch depth is dbar * max(0, 1 + f * g) with g ~ N(0, 1) and f = 0, 0.25, 0.5 or 1. We ran the full pipeline with the injected ephemeris and the same thresholds.
* Real controls: KIC 12557548 b, K2-22 b and KOI-2700 b have SPOC 2-minute data (Tmag 14.0-15.0). BD+05 4868 A has no 2-minute light curve in sectors 1-107.

## 4. Results

### 4.1 Sample

* 7,869 of the 14,681 signals (6,730 stars) were testable. Most of the 6,805 untestable signals have a duty cycle D/P above about 0.12 (median 0.15). Such long dips do not fit a transit of a dwarf star at these periods. They are mostly contact, ellipsoidal or pulsating variables.
* The primary sample has 2,626 signals on 2,615 stars (median Tmag 11.0, P = 0.20-2.00 d). The median calibrated per-transit S/N is 2.7.

### 4.2 Depth-variability statistic

The Xp distribution of the primary sample agrees with the pseudo-phase null (Figure 1, right). The 99.9 % null quantile of Xp is 2.6-3.7 for signals with at least 40 degrees of freedom. Nine signals are significant:

| TIC | P (d) | Tmag | per-transit S/N | Xp | fvar | Classification |
|---|---|---|---|---|---|---|
| 148081648 | 0.377037 | 12.04 | 4.4 | 5.8 | 0.50 | evolving dip of a flaring M-dwarf pair (Section 4.4) |
| 41233766 | 0.570548 | 9.82 | 6.1 | 3.6 | 0.25 | part of a periodic stellar waveform with beats (Section 4.5) |
| 444335503 | 1.202320 | 6.17 | 41 | 31 | 0.14 | deep eclipse, odd/even 27 sigma, not a TOI |
| 148877735 | 1.803720 | 9.32 | 31 | 12 | 0.10 | deep transit or eclipse, not a TOI |
| 220359766 | 1.759860 | 8.12 | 33 | 7.5 | 0.08 | deep eclipse, odd/even 13 sigma, not a TOI |
| 19342878 | 1.332810 | 10.80 | 34 | 9.0 | 0.08 | TOI-6101.01 (PC) |
| 1129033 | 1.360030 | 9.63 | 51 | 9.5 | 0.05 | WASP-77 A b |
| 468574941 | 1.497190 | 11.00 | 39 | 4.2 | 0.04 | TOI-2046 b |
| 293435336 | 1.809880 | 9.03 | 61 | 5.5 | 0.04 | WASP-76 b |

Seven significant signals are bright giant-planet transits or eclipses with per-transit S/N of 30-60. Their depth jitter is 4-14 %. At this S/N, small timing, ingress-sampling, spot-crossing and baseline errors of the box model are detectable. This jitter is far below the 25 % floor, and we do not interpret it as physical.

Two signals pass the variability floor. Neither is a planet.

During development, three more formal outliers showed pipeline failure modes. We fixed them with the rules in Section 3:

* WASP-18 b: the TCE is the occultation, and the full-phase search locked onto the primary transit. The depth guard fixes this.
* TIC 293081694: the TCE at 1.25866 d is a near-period alias of a 1.25396 d eclipsing binary on the same star. The alias rule fixes this.
* TIC 1716020176: a blended eclipsing binary (CROWDSAP 0.27, 8-sigma in-transit centroid shift) whose re-phased sectors locked onto a 15 % eclipse. The depth guard fixes this.

### 4.3 Sensitivity and limit

Figure 2 and `files/data/injection_recovery_table.csv` give the recovery fraction against the measured per-transit S/N:

* Constant-depth injections (f = 0) are flagged in 0.0-0.4 % of cases in every S/N bin.
* KIC 12557548 b-like variability (f = 1, true rms/mean about 0.8 after clipping at zero): 14 % at S/N 1-2, 81 % at S/N 2-4 and 99 % at S/N 4-8.
* f = 0.5: 30 % at S/N 2-4 and 85 % at S/N 4-8.
* f = 0.25: at most 12 %. The 25 % floor makes this case undetectable.

We sum the recovery probability over the S/N distribution of the primary sample. This gives an effective sample of 1,631 signals for f = 1 and 985 signals for f = 0.5. No planet-like variable-depth signal was found. Thus, at 95 % confidence, fewer than 0.18 % (f = 1) and 0.30 % (f = 0.5) of the short-period SPOC 2-minute TCE signals in the primary sample carry such variability (Poisson limit 3 / N_eff).

The three known disintegrating planets are detected as transits, but their per-transit S/N in TESS is only 0.33-0.38. Their Xp of 1.14-1.21 is not significant (Figure 1, squares). This agrees with the injection result: at Tmag 14-15, TESS cannot measure the depth variability of these planets orbit by orbit.

### 4.4 TIC 148081648 / TIC 148081650: an evolving 0.377-day dip

TIC 148081648 (Tmag 12.04, Gaia DR3 6007612585055066368, a two-parameter Gaia solution, BP = 14.01, RP = 11.96) and TIC 148081650 (Tmag 12.77, TIC Teff 3739 K, parallax 6.62 mas, about 151 pc) are 5.2 arcsec apart. TESS does not resolve them. Our aperture tests (`tic148_source.py`) cannot assign the dip to one of the two stars. Figure 3 and `files/vetting/` show the evidence.

* A sharp dip (Gaussian sigma 0.14-0.55 h) recurs with P = 0.3770348 +/- 0.0000004 d. It is present in sector 11 (2019), sector 65 (2023) and sector 103 (2026). The error is inflated by sqrt(chi2/dof) = 3.0. The dip time wanders by up to 12 minutes from a linear ephemeris.
* The dip depth changes: 1.1 % and 0.85 % in the two orbits of sector 11, 1.05 % and 0.43 % in sector 65 (target-aperture PDCSAP, Gaussian fits), and about 0.65 % in sector 103 (neighbour aperture). In sector 103 a broad 6 ppt depression appears near phase 0.25, and the sharp dip is weak.
* In sector 65 the per-cycle depth falls from a median of 10.8 ppt (29 cycles) to 4.3 ppt (31 cycles). The largest flare of the sector (peak 20 %, BTJD 3080.26) occurs at the last deep dip, just before the orbit gap (BTJD 3080.63-3082.00). After the gap the dip is shallower, broader and 10 minutes later. The broad hump near phase 0.4 keeps the same amplitude (about 3 ppt). A change of dilution or aperture would scale the hump as well. Thus the change is specific to the dip.
* The light curves also contain a second period of 0.588 d (dominant in sector 11) and frequent flares (up to 41 % peak in sector 103). These are signs of two rapidly rotating, active M dwarfs. The pair lies toward Upper Centaurus-Lupus (Galactic l about 333 deg, b about +17 deg) at about 150 pc. Our analysis does not test membership.

Interpretation: this behaviour matches the complex periodic variables (CPVs) of Bouma et al. (2024). CPVs are young, rapidly rotating M dwarfs with sharp dips at the rotation period, and flares appear to cause sudden dip collapses. A disintegrating planet would need a period equal to a stellar rotation period and a dip that collapses at a flare. That is less likely, but we cannot exclude it. A grazing eclipsing binary cannot explain a 2.5-fold depth change between two consecutive TESS orbits while the rest of the waveform stays constant. We report the pair as a new CPV-like candidate, not as a planet candidate. We found no literature mention of either star. The prior campaign CPV search (sci:sha256:22057485...) did not include these stars, because it required a Gaia parallax for the selected star.

### 4.5 TIC 41233766

The main photometric period of this F-type star (TIC Teff about 6070 K) is 0.5706 d in all four sectors. That is the TCE period. The light curve also has its harmonic at 0.285 d and side peaks at 0.55-0.59 d. The "transit" is one feature of a periodic stellar waveform (1.3-1.5 ppt rms). The depth modulation follows a slow beat pattern. This is not a transit of a disintegrating body.

## 5. Limitations

* The search is limited to SPOC 2-minute targets and to signals that SPOC already detected as TCEs. A disintegrating planet with a low mean depth, or one in a quiescent state, may have no TCE. BD+05 4868 A b is an example: it has only full-frame-image data.
* We test within-sector variability only. Variability on time scales longer than a sector (for example quiescent phases of weeks) adds little to Xp. The injected depths are independent from orbit to orbit.
* The box model with a linear baseline is simple. At per-transit S/N above about 30, it gives a few-percent depth jitter. The 25 % floor removes this, but it also removes real low-amplitude variability.
* The primary-sample cuts (weak-secondary MES, alias rule, rms below 2 %, Teff below 6,600 K, duty cycle) remove many systems. The limit applies only to the primary sample.
* We use at most four sectors per star.
* The calibrated per-transit S/N in the injection study is lower than the nominal S/N, by a factor of about 0.3, because of red noise. We report all results against the measured, calibrated S/N.
* For TIC 148081648/50, the source star of the dip is not known, the orbit gap hides the exact time of the sector 65 change, and we have no spectra. The CPV interpretation needs confirmation, for example by time-resolved spectroscopy (H-alpha) and higher-resolution photometry.

## 6. Files

* `files/figures/fig1_survey.png`, `fig2_injections.png`, `fig3_tic148.png`: the display figures.
* `files/data/primary_sample_scored.csv`: the 2,626 primary signals with all statistics, null false-alarm probabilities and flags.
* `files/data/survey_all_signals.csv`: all 14,681 signals (status, statistics, run source).
* `files/data/pseudo_phase_null_samples.csv`, `thresholds.json`: the null calibration.
* `files/data/injections.csv`, `injection_recovery_table.csv`: the injection-recovery test.
* `files/data/controls_result.csv`, `controls_eph.json`: the known disintegrating planets.
* `files/data/epoch_depths_significant_signals.csv`: the per-epoch depths of the nine significant signals.
* `files/data/tic148_detail.json`: per-orbit dip fits, flare list, ephemeris and per-cycle depths for TIC 148081648/50.
* `files/data/targets_from_spoc_tce.csv`, `alias_flags.csv`, `lc_variability.csv`: target list and filters.
* `files/vetting/`: vetting sheets for the two variability candidates.
* `files/code/`: all analysis code; `REPRODUCE.md` gives the steps; `retrieve_inputs.sh` gets the inputs.
* `files/provenance/`: SHA-256 hashes and URLs of all inputs.
* `files/NOTICE_EXTERNAL_DATA.md`: sources and attribution of external data.

## 7. Reproduction

Run `bash files/code/retrieve_inputs.sh WS files` to download the inputs into a workspace WS outside this folder. Then follow `files/code/REPRODUCE.md`. The analysis needs about 61 GB of disk space and a few hours on 8 cores.

## 8. Acknowledgements and data rights

This work uses data from the TESS mission (NASA Explorer program), obtained from MAST at STScI, and the TESS Input Catalog. Gaia DR3 values are quoted for one star. See `files/NOTICE_EXTERNAL_DATA.md`. The bundle contains no raw light curves.
