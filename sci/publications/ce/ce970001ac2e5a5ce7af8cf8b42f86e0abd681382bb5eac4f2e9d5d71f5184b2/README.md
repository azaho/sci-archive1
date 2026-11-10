# TESS data from 2018 to 2026 show repeat events for 36 of 164 K2 single-transit candidates, give one period for 6 systems, and limit TOI-5560.01 (EPIC 211924561) to 70.25 or 140.49 days

## Summary

LaCourse & Jacobs (2018) listed 164 single transit and eclipse events in K2 Campaigns 0 to 14. Each event occurred one time in K2, so its period was not known. TESS observed most of these stars again from 2018 to 2026. We searched all available TESS light curves of the 163 stars for a second event with the K2 shape. We also searched all K2 campaigns of each star.

Main results:

1. **36 candidates show a repeat event in TESS.** 35 events have SNR 15 or more and match the K2 depth and duration. One candidate (EPIC 211924561) has two weaker TESS dips that agree with the K2 ephemeris. Seven other candidates show a repeat only in a later K2 campaign. We consider one of these seven (EPIC 203865172) not credible.
2. **Six systems have one allowed period** after we apply all K2 and TESS coverage: EPIC 202071902 (22.9041 d), EPIC 202072917 (34.7456 d), EPIC 248811085 (49.2501 d), EPIC 211411112 (62.5946 d), EPIC 246089124 (73.9624 d) and EPIC 246696483 (182.2453 d). Five more systems have two to four allowed periods. All six single-period systems have companions larger than 2 Jupiter radii, so most are probably eclipsing binaries.
3. **EPIC 211924561 = TIC 238606535 = TOI-5560.01.** Four events of the same depth (0.23 %) and duration (3.1 h) occur in K2 C5 (2015), K2 C16 (2017), TESS S46 (2021) and TESS S72 (2023). Only two periods agree with all four events and with all coverage: **140.494 d and 70.247 d**. The ExoFOP TOI table gives a maximum period of 702.47 d for this candidate. The companion radius is about 0.88 Jupiter radii if the signal is on the target and not diluted.
4. **VSX periods are not correct for 10 recovered eclipsing stars.** VSX lists periods from 3.49 to 18.8 d for these EPIC stars. K2 and TESS coverage excludes each of these periods, and the observed epochs do not agree with them.
5. **Duration-based period estimates predict too many TESS repeats for deep events.** A small-planet duration model with TIC stellar densities predicts 20.6 secure TESS repeats among 50 candidates with depth 5 % or more. We observe 15 (p = 0.027). For depths below 5 %, prediction and observation agree. This agrees with large (stellar) companions, which make the eclipse longer for a given period.
6. **Non-detections give period limits.** For 76 candidates TESS had sensitive data but showed no repeat. TESS removes a median 17 % of the log-period range from the K2 minimum period to 3000 d. For 23 candidates it removes 25 % or more.

The planet-like candidates (depth below 1 %, 35 candidates with stellar density) are mostly too shallow for TESS. The model predicts 1.06 secure repeats and we observe 1.

## Data

| Data | Source | Use |
|---|---|---|
| Candidate list | LaCourse & Jacobs 2018, RNAAS 2, 28 (arXiv:1802.05823), Table 1 from the arXiv LaTeX source | K2 epoch, depth, duration |
| K2 long-cadence light curves (PDCSAP) | MAST, K2 mission products, all campaigns of each star (225 files) | K2 event refit, K2 repeats, K2 coverage |
| TESS SPOC 2-min light curves | MAST (132 sector light curves used) | search |
| TESS-SPOC FFI light curves | MAST HLSP, doi:10.17909/t9-wpz1-8s54 (62 used) | search |
| QLP FFI light curves | MAST HLSP, doi:10.17909/t9-r086-e880 (153 used; SAP flux) | search |
| TESScut FFI cutouts | MAST TESScut API (164 sectors with no pipeline light curve) | own 3x3-pixel aperture photometry |
| TIC v8.2 | MAST Catalogs | cross-match, Tmag, stellar radius, mass, Teff |
| ExoFOP TOI and CTOI tables | ExoFOP, downloaded 2026-11-09 | known TESS candidates |
| VSX | AAVSO VSX through the VizieR CfA mirror (B/vsx/vsx) | known periods |
| Published period estimates | Sandford et al. 2019 (arXiv:1908.08548), Dholakia et al. 2020 (doi:10.3847/1538-3881/ab594c), Giles et al. 2018 (arXiv:1806.08757) | prediction test |

The TESS data span sectors 2 to 98 and one segment that MAST labels sector 1751 (2026-01-15 to 2026-01-22). In total we used 511 sector light curves for 158 candidates. Six candidates had no TESS data. `files/data/input_provenance.csv` gives the file name, byte count, SHA-256 and MAST URI of every downloaded file (1,085 files, 617 MB). The raw light curves are not in this bundle. `files/code/run_all.sh` downloads them again into local scratch.

## Method

All times are BKJD = BJD_TDB - 2454833. TESS time is BTJD + 2167.

**Cross-match.** We took K2 coordinates from MAST and matched each EPIC star to the nearest TIC v8.2 source. All 163 matches are closer than 1 arcsec.

**K2 refit.** For each event we fitted a trapezoid and a quadratic baseline to the K2 PDCSAP flux. We used the lightkurve default quality bitmask (1130799). We merged the two halves of C10 and C11. We then scanned all K2 campaigns of the star with the fitted template. The scan gives the K2 event SNR, other K2 events, and K2 sensitivity intervals. The K2 scan recovers 139 of 163 events at SNR 7 or more. For the other events we used the LaCourse & Jacobs depth and duration as the template.

**TESS search.** For each sector we chose one light curve in this order: SPOC 2-min, TESS-SPOC, QLP, own TESScut photometry. We binned 20-s and 2-min data to 10 min. We moved the K2 trapezoid template over the data in steps of 1/8 of the duration. At each step we fitted a linear (quadratic for durations above 0.5 d) baseline and a depth in a window of the duration plus one duration (minimum 0.3 d) on each side. We required 60 % of the in-event cadences and baseline data on both sides. We divided each depth error by the robust scatter of all depth/error values in the sector (empirical SNR). A dip is a local maximum with SNR 7 or more. We kept the brightenings (SNR -7 or less) as a control.

**Sensitivity intervals.** A time is "covered" if an event with the K2 depth would have SNR 10 or more there. For QLP SAP flux and TESScut photometry we reduced the expected depth by the TIC flux of neighbours within 21 arcsec. We also kept a stricter set at expected SNR 20.

**Injection-recovery.** We injected 10 K2-shaped events per sector at random times (5,090 in total). The search recovered 99.9 % of the 3,080 injections in covered intervals and 23 % of the others (Figure 4, left).

**Shape test and control.** A TESS dip matches the K2 event if its depth is 0.5 to 2 times the expected depth and a free trapezoid fit gives 0.6 to 1.6 times the K2 duration. We applied the same test to the brightenings with the flux mirrored. At SNR 7 to 15, 14 dips and 9 brightenings pass. At SNR 15 or more, 49 dips and 2 brightenings pass (Figure 4, right). Thus we call only shape-matched dips with SNR 15 or more "secure". We chose this threshold after we saw the control counts.

**Period solutions.** We combined the secure epochs: the K2 event, K2 repeats (SNR 15 or more, depth and duration match), and secure TESS dips. For each N we tested P = (last - first epoch)/N. A period is allowed if all epochs agree within the larger of 3 timing errors and 0.05 durations, and if no other predicted epoch falls in a K2 or TESS covered interval. If no period was allowed, we repeated the test with only the epochs whose depth is 0.8 to 1.25 times the K2 depth. Weak TESS dips (SNR 7 to 15) were then compared with the allowed periods. We measured their chance agreement with 300 random TESS data times.

**Period limits and duration-based prediction.** For each candidate we marked all periods from 1 to 20,000 d for which an epoch other than the K2 event falls in a covered interval. We then drew a Monte Carlo period posterior for a small companion. The draws use a log-uniform period, uniform impact parameter, Kipping (2013) eccentricity distribution and the TIC stellar density with 25 % scatter. The weights are the transit probability, the 1/P chance of a K2 transit, the K2 non-detections and the fit to the observed duration. The posterior mass of periods with an epoch in a TESS covered interval is the predicted probability of a TESS repeat. We added these probabilities over the 104 candidates with a TIC density and compared the sum with the observed count (Poisson-binomial distribution).

## Results

### Overview

| Status | Candidates |
|---|---|
| TESS repeat, SNR 15 or more | 35 |
| TESS repeats on the K2 ephemeris, SNR 8 to 11 (EPIC 211924561) | 1 |
| Repeat only in a later K2 campaign | 7 |
| TESS sensitive, no repeat | 76 |
| No sensitive TESS data | 45 |

Figure 1 shows the status against K2 depth and TESS magnitude. The TESS repeats occur almost only for depths above 1 %. The 45 candidates with no sensitive data have a median depth of 0.35 %.

### Period solutions

| EPIC | TIC | Epochs used | Allowed periods (d) | Depth | Companion radius (R_Jup) |
|---|---|---|---|---|---|
| 202071902 | 57051340 | K2 C0, TESS S44, S71 | 22.9041 | 9.0 % | 5.6 |
| 202072917 | 308255000 | K2 C0, TESS S6, S43, S45, S1751 | 34.7456 | 24.7 % | 15.8 |
| 248811085 | 349987241 | K2 C14, TESS S46, S72 | 49.2501 | 9.0 % | 4.6 |
| 211411112 | 437034781 | K2 C5, K2 C16, TESS S46 | 62.5946 | 2.3 % | 2.2 |
| 246089124 | 49603732 | K2 C12, TESS S70, S92 | 73.9624 | 13.6 % | 4.9 |
| 246696483 | 436612436 | K2 C13, TESS S43, S70 | 182.2453 | 5.7 % | 4.1 |
| 202137580 | 238479066 | K2 C0, TESS S44, S72 | 69.4295 or 34.7148 | 6.3 % | 19.7 |
| 211894612 | 14678155 | K2 C5, K2 C18, TESS S44 | 111.4331 or 55.7166 | 4.3 % | 5.4 |
| 211924561 | 238606535 | K2 C5, K2 C16 (+ TESS S46, S72 weak) | 140.494 or 70.247 | 0.23 % | 0.88 |
| 247967714 | 268396693 | K2 C13, TESS S44, S71 | 185.6267, 92.8133, 61.8756 | 25.3 % | 6.0 |
| 212012030 | 14394716 | K2 C5, K2 C18, TESS S71 | 220.3218, 110.1609, 73.4406, 55.0804 | 20.0 % | 3.9 |

`files/data/catalog.csv` gives the TIC numbers and all values. Companion radius is sqrt(depth) times the TIC stellar radius. It ignores limb darkening, grazing geometry and dilution. Figure 3 shows all K2 and TESS data of the six single-period systems folded on their periods. In each case the K2 and TESS eclipses agree in depth and shape, and no eclipse occurs at other phases near the primary.

For EPIC 202072917 the predicted epochs agree with all four TESS eclipses from 2019 to 2026, and no other eclipse occurs in eight sectors. EPIC 202137580 has a 2.2-day flat-bottomed eclipse. The flux drops at the end of TESS S45 (BKJD 4705), at the predicted epoch of the 34.71-d alias. This point is at a sector edge, so we do not use it.

Seven recovered systems give no common period. These are EPIC 211598816, 211498244, 211489484, 210823406, 202126877, 220605820 and 215307988. EPIC 211498244 and 211489484 show eclipses of two different depths, so they are probably eclipsing binaries with primary and secondary eclipses. EPIC 211598816 is not a single-event star in our K2 reduction: K2 C5 shows several short dips of similar depth. EPIC 220605820 and 215307988 show a second event in the same K2 campaign.

### EPIC 211924561 (TOI-5560.01)

Figure 2 shows the four events. The K2 C16 repeat has K2 SNR 20 and a depth ratio of 0.90. The K2 pair (983.455 d apart) and all coverage allow nine periods, 983.455/N d. The two TESS dips (SPOC 2-min, SNR 11.4 and 8.0, depth ratios 0.99 and 0.90) agree only with N = 7 (140.494 d) and N = 14 (70.247 d). The chance that a random TESS data time agrees with one of the nine periods is 0.7 % and 0.3 % for the two dips. The S46 dip is the TESS single transit for which this TOI was alerted (TBJD about 2568). Dholakia et al. (2020) searched the C5 singles for repeats in C16 and C18 by eye. They did not report this star.

The host is an F star (TIC Teff 6780 K, radius 1.88 R_sun). A circular orbit with P = 70 to 140 d and a central transit gives a duration of about 13 to 16 h. The observed duration is 3.1 h. Thus the transit is probably grazing (high impact parameter) or the orbit is eccentric. A grazing transit makes the true companion radius larger than 0.88 R_Jup. We did not do pixel-level tests for this star. The K2 photometry uses 4-arcsec pixels and gives the same depth as TESS. This supports a source on or very near the target.

### VSX periods

VSX lists eclipse or variable periods for 15 recovered stars (`files/data/vsx_period_check.csv`). For 10 EPIC stars of type E, EA, EA/RS or VAR, the listed period (3.49 to 18.80 d) is excluded by our K2 and TESS coverage, and the observed epochs do not agree with it. For example, VSX gives 3.842 d for EPIC 202072917; our data give 34.7456 d. For HN Gem (EPIC 202073476, 51.261 d) the K2 and TESS events are half a period apart. Thus they can be the primary and secondary eclipses of the VSX orbit. Four other VSX entries are rotation or other variability periods, which need not agree with an eclipse period.

### Prediction test

Figure 5 compares predicted and observed TESS repeats for the 104 candidates with a TIC stellar density.

| Depth class | n | Predicted secure repeats (95 % range) | Observed | P(obs <= observed) |
|---|---|---|---|---|
| below 1 % | 35 | 1.06 (0-2) | 1 | 0.74 |
| 1 to 5 % | 19 | 5.71 (3-9) | 7 | 0.89 |
| 5 % or more | 50 | 20.61 (15-26) | 15 | 0.027 |
| all | 104 | 27.37 (21-33) | 23 | 0.11 |

With the looser definition (any shape-matched dip at SNR 7 or more, epochs at expected SNR 10 or more), the deep class gives 22.9 predicted and 16 observed (p = 0.010). We did eight tests (four classes, two definitions), so the deep-class result is moderate evidence. The deficit agrees with stellar companions: their radius makes the eclipse longer, and the small-companion model then gives a period that is too short.

We also tested published period estimates (`files/data/published_predictions_test.csv`). TESS removes 42 % of the Sandford et al. (2019) 68 % interval for EPIC 201635132 (103 to 169 d) and 5 % for EPIC 203311200. For EPIC 204634789, 248847494 (also Giles et al. 2018) and the five Dholakia et al. (2020) C5 candidates, TESS removes less than 2 % of the interval. These candidates are too shallow for TESS. Thus TESS does not test these predictions. For EPIC 211351543 our K2 coverage excludes the Dholakia et al. median period. Our K2 search did not detect their shallow (0.05 %) repeat, so this exclusion can be an effect of our K2 noise model.

## Limitations

- We did not do pixel-level (difference-image) tests for each TESS event. TESS pixels are 21 arcsec. A nearby eclipsing binary can cause a dip on the target. The depth agreement with K2 (4-arcsec pixels) reduces but does not remove this risk.
- The K2 PDCSAP quality mask removes many in-event cadences, and K2 roll systematics remain. Our K2 scan does not recover 24 of the 163 events at SNR 7. For these we used the published depth and duration. Some published values are probably typographical errors (for example a depth above 100 % for EPIC 204100531).
- Some K2 "repeats" are short systematic features. We excluded EPIC 203865172 by inspection.
- The coverage threshold (expected SNR 10) uses an empirical noise scale. Injections test our own search. They do not test the pipeline detrending of the SPOC, TESS-SPOC and QLP products.
- The dilution correction for QLP and TESScut is approximate (TIC flux within 21 arcsec).
- The period solver assumes one strictly periodic eclipse. Eclipse-timing variations, secondary eclipses of similar depth and eccentric binaries can give no solution or a wrong solution.
- The duration-based prediction uses TIC densities with an assumed 25 % scatter and a small-companion model. It is not valid for eclipsing binaries.
- We chose the SNR 15 secure threshold after we saw the control counts.
- We did not use radial velocities or ground-based photometry. We give no planet confirmation.

## Files

- `files/data/catalog.csv`: one row per candidate (164 rows): TIC, Tmag, our K2 template (t0, duration, depth), TESS status, period limits, period solutions, companion radius, TOI/CTOI identifiers.
- `files/data/period_solutions.csv`: epochs used, allowed periods (up to 40 listed), weak-dip tests.
- `files/data/period_constraints.csv`: minimum allowed period from K2 alone and K2 + TESS, fraction of log period removed by TESS, Monte Carlo prediction.
- `files/data/tess_dips_vetted.csv`, `tess_brightenings_control.csv`: all TESS events at |SNR| 7 or more, with shape-test values.
- `files/data/k2_refits_and_coverage.csv`, `k2_other_events.csv`: K2 refits, K2 sensitivity intervals and other K2 events.
- `files/data/tess_search_intervals_dips_injections.json`: TESS sensitivity intervals (SNR 10 and 20), dips, brightenings and all injections.
- `files/data/population_test.json`, `population_table.csv`, `published_predictions_test.csv`, `vsx_period_check.csv`, `tess_sectors.csv`.
- `files/data/input_provenance.csv`: SHA-256 of every downloaded input file.
- `files/code/`: all analysis code (`stlib.py` and numbered scripts) and `run_all.sh`.
- `files/figures/`: Figures 1 to 5.
- `files/EXTERNAL_DATA_NOTICE.md`: sources, licenses and attribution of external data.

## Reproduction

1. Make an empty directory. Copy `files/code` into it as `code/`.
2. Use Python 3.12 with numpy, scipy, pandas, astropy, matplotlib, requests, astroquery and lightkurve.
3. Run `bash code/run_all.sh`. The script downloads the arXiv sources, ExoFOP tables, K2 and TESS light curves and TESScut cutouts into `scratch/` and `src/`. The complete run takes about 2 to 3 hours, mostly for downloads.
4. Compare the hashes of your downloads with `files/data/input_provenance.csv`. MAST can reprocess products. The ExoFOP tables change daily.
5. Compare your outputs with `files/data/`. The Monte Carlo and injection steps use fixed random seeds.

## Provenance

- Job: sci-1107-hp-astronomy-d849e1bcc215; topic: astronomy; campaign 11_07_2026; machine: hp; account: claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis dates: 2026-11-09. TESS data were the products available at MAST on that date.
- Related campaign publications: the same method for Kepler single transits (sci:sha256:e8b4dc705fcd37bb721bc1fc69f364ebafa174184c1e5172373571c7c68a37aa) and for single-transit TOIs (sci:sha256:d9f224da56fe0d0b41ca406203e26ffc5c99b6806a710273bb2267025c1dc810). This work uses independent code.
