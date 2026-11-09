# Gaia DR3 transit-table periods are sampling aliases for 161 of 174 known planets; TESS gives the true period and a disposition for 35 of 40 unconfirmed candidates

Job: `sci-1107-dell-astronomy-ab3bf154c694`. Campaign: `11_07_2026`. Topic: astronomy. Machine: dell. Account: claude-andrii.
Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an autonomous SCI research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Summary

The Gaia DR3 table `gaiadr3.vari_planetary_transit` gives a transit period, a reference time, a depth and a duration for 214 sources. The sources are 173 known planets and 41 new candidates (Gaia-1 b and Gaia-2 b are now confirmed). ESA withdrew the first version of the table in June 2022 and replaced it on 7 February 2023. The replacement table has the same name.

We tested the current table against three independent data sets:

1. Literature ephemerides of the 174 sources that are now hosts of confirmed planets (NASA Exoplanet Archive).
2. The Gaia DR3 G-band epoch photometry of all 214 sources.
3. TESS light curves (TESS-SPOC, QLP and SPOC; at most 8 sectors per source; 992 light curves).

Main results:

* **The periods are aliases for most known planets.** The Gaia period agrees with the literature period (within 0.1 %) for only 13 of 174 known planets. For 13 more, the ratio is a small-integer fraction. For the other 148, the ratio is not a simple fraction (range 0.011 to 13.0). The reference time agrees with the literature ephemeris (within 0.5 transit durations) for all 13 planets with a correct period. Thus the 2023 replacement corrected the reference times: in the withdrawn table, the reference time agrees for only 1 of these 13 planets.
* **Gaia saw the transits; the period search failed.** For 158 of the 161 known planets with a wrong period, the Gaia epochs that the table ephemeris puts in transit are significantly dimmed (more than 3 sigma). The literature ephemeris also finds the dimmed epochs (152 of 161). A median of 75 % of the in-transit epochs under the table ephemeris are also inside a true transit. These planets have a median of only 3 Gaia field-of-view transits inside a transit, against 6 for the 13 planets with a correct period. A few points in transit cannot fix the period, so the table period is one of many aliases that fit the same points. The withdrawn table ephemeris finds dimming for only 17 of 174 known planets.
* **TESS recovers every known planet that it observed** (173 of 173). The best TESS period equals the literature period for 170. The TESS signal-to-noise ratio at the Gaia period is low for most known planets (Figure 4).
* **The 40 unconfirmed Gaia candidates.** We use the same rules for all sources. We check the rules on the known planets. Results:
  * 13 have a TESS transit that is linked to the dimmed Gaia epochs and that has no eclipsing-binary (EB) indicator. Eight of these are TESS Objects of Interest (TOIs): TOI-572.01, 2906.01, 3531.01, 4968.01, 5839.01 (TFOPWG: false positive), 5905.01, 5964.01 and 6409.01. **Five are not TOIs and not in the NASA or exoplanet.eu catalogues** (Table 2, Figure 5).
  * 10 have a linked TESS signal with EB indicators. Examples: a Gaia SB1 orbit with the TESS period (Gaia DR3 4535127268607000320, K1 = 22 km/s), a Gaia SB2 orbit at twice the TESS period (Gaia DR3 3450611154067089408), deep secondary eclipses, or companion radius above 2 Jupiter radii. One of these sources is the known Kepler EB KIC 11517719.
  * 7 show no TESS transit. For 6 of these, a transit with the Gaia depth would have a TESS signal-to-noise ratio of 66 to 442. TESS thus does not confirm these Gaia events.
  * 5 have no TESS light curve in the SPOC, TESS-SPOC or QLP products.
  * 5 are not decided: 3 TESS transits that are not linked to the Gaia epochs, 1 TESS signal that is broad stellar variability, and 1 source with fewer than 3 TESS transit epochs.
* **For 15 of the 23 linked unconfirmed candidates, the Gaia period is an alias.** TESS gives the true period.

Figure 1 and Figure 2 show the period and epoch tests. Figure 3 shows the TESS data of all 35 unconfirmed candidates with TESS light curves. Figure 5 shows the five new non-TOI planet candidates.

## 2. Question

Can users trust the period and the reference time in the corrected Gaia DR3 planetary-transit table? Do independent TESS data confirm the 41 new Gaia candidates, and what are their true periods?

We did not find a published test of the corrected table against literature ephemerides. Panahi et al. (2022) used early TESS full-frame images to check some candidates. TESS has since observed most of the sky again. The TESS-SPOC and QLP products now cover many more sectors.

## 3. Data

All data are public. Section 8 gives the hashes and the retrieval recipe.

| Data | Source | Use |
| --- | --- | --- |
| `gaiadr3.vari_planetary_transit` (current; solution_id 375523436409132247) and `gaiadr3.vari_planetary_transit_13june2022` (withdrawn) | ESA Gaia archive TAP, retrieved 2026-11-08 | Gaia ephemerides |
| `gaiadr3.gaia_source`, `astrophysical_parameters` (FLAME radius), `nss_two_body_orbit`, `vari_summary`, `vari_classifier_result` | ESA Gaia archive TAP | Star data, SB1/SB2 orbits |
| `gaiadr3.epoch_photometry` (G band), 214 sources | AIP Gaia mirror TAP (`https://gaia.aip.de/tap`). The ESA DataLink server returned HTTP 503 during this work. | Gaia in-transit epochs |
| TESS light curves, 992 files: 622 TESS-SPOC, 315 QLP, 55 SPOC 120 s | MAST | Independent photometry |
| TIC v8 cone search (14.4 arcsec) | MAST Catalogs | TIC ID, Tmag, contamination ratio, neighbours |
| NASA Exoplanet Archive `pscomppars` (6,464 planets) | Exoplanet Archive TAP, 2026-11-08 | Known planets, literature ephemerides |
| ExoFOP TOI table | Shared campaign dataset `datasets/exofop-tess-toi-table-20261108/exofop_toi.csv` (sha256 `ef22793a...fd366a`) | TOI status |
| exoplanet.eu catalogue (CSV) | `https://exoplanet.eu/catalog/csv/` (sha256 `4b835f52...9038ff`) | Positional check only |
| VSX | VizieR mirror at CfA | Known variable stars |

Data selection for TESS: for each sector we use one product, in this order of preference: TESS-SPOC, QLP, SPOC 120 s. We do not use 20 s data. When more than 8 sectors exist, we keep the first and the last sector and space the others evenly in time. We used this cap because the network bandwidth was approximately 250 kB/s.

## 4. Methods

All code is in `files/code/`. The scripts run in the order of Section 9.

**4.1 Known-planet ephemeris test** (`known_ephem.py`). We match each Gaia source to the NASA archive by Gaia DR3 ID, then by TIC ID, then by position (3 arcsec). For each host we use the transiting planet with the largest depth. We compare the Gaia period with the literature period. We propagate the literature ephemeris to the Gaia reference time and express the offset in units of the literature transit duration. We do this for the current and for the withdrawn table. The Gaia time scale is BJD(TCB) - 2455197.5.

**4.2 Gaia epoch test** (`gaia_fold.py`). We remove epochs with `variability_flag_g_reject`. For an ephemeris (P, T0, T14) we compute the mean magnitude change of the epochs inside the transit window, and its significance against the robust scatter of the other epochs. A null comes from 200 random phase shifts. We apply this to the table ephemeris (current and withdrawn) and to the independent ephemeris (literature, or TESS for unconfirmed candidates). We also count how many in-transit epochs under the table ephemeris are inside a literature transit.

**4.3 TESS search** (`vet.py`). We normalise each sector. We remove trends with a wotan biweight filter (window clip(3 T14_Gaia, 0.5, 1.5) d). We clip outliers above 4 sigma and bin to 5 minutes. A box least squares (BLS) search runs in three parts:

* Around k x P_Gaia for k = 1/3, 1/2, 2/3, 1, 3/2, 2, 3 (+-0.3 %). The same grid on the inverted flux gives an empirical noise level.
* Around the literature period or the TOI period (+-0.05 %), when one exists.
* An independent search from 0.3 to 15 d on the longest set of consecutive sectors, refined on all sectors.

The best signal is the one with the highest BLS SNR. A detection needs SNR >= 10 and SNR >= 1.5 x the largest inverted-flux SNR.

**4.4 Per-transit diagnostics** (`refine.py`). For each transit epoch we measure depth = median(local baseline, 0.75 to 2.5 T14 from centre) - mean(central 50 % of the transit). Odd/even and phase-0.5 depths use the mean of the per-epoch values and their empirical standard error. This error includes correlated noise. A first white-noise version flagged bright planets incorrectly (for example 12 sigma for TOI-3531.01). We do not use that version.

**4.5 Gaia-TESS link** (`link.py`). A TESS ephemeris must cover approximately 1,000 to 3,000 cycles to reach the Gaia epochs (2014 to 2017). We scan trial periods in +-3 sigma_P around the TESS period (sigma_P from a linear fit to per-sector transit times). For each trial we compute the dimming significance S of the Gaia epochs in the TESS transit window (2 or more epochs needed). The statistic is S_max over the scan. The null repeats the scan with 500 random phase shifts of T0. A link needs p < 0.01. When one parity of the TESS signal has no dip (odd/even fraction > 0.8), we double the period first.

**4.6 Classification** (`classify.py`). Rules, in order:

* D0: no TESS light curve.
* D1: no TESS detection.
* D2: duty cycle T14/P > 0.12 (broad variability, not a transit).
* E: fewer than 3 TESS transit epochs.
* C: no Gaia link.
* B: one or more EB indicators. The indicators are: odd/even difference > 3 sigma and > 10 % of the depth; phase-0.5 depth > 3 sigma and > 5 % of the primary depth; companion radius > 2.0 R_J (TESS depth, Gaia FLAME stellar radius, no limb darkening); depth > 5 %; Gaia SB1/SB2 orbit with K1 > 5 km/s.
* A: none of the above.

The thresholds are in `files/results/classification_thresholds.json`.

**4.7 Calibration on known planets.** The rules flag 8 of 173 known planets with at least one EB indicator: secondary 3 (Kepler-490 b, KELT-1 b, WASP-37 b), radius > 2 R_J 6, depth > 5 % 2, odd/even 0, Gaia SB 0. The Gaia-TESS link succeeds for 131 of 173 known planets (76 %). Thus a missing link ("C") is weak evidence against a candidate. Most failures come from planets with only one Gaia epoch in transit.

**4.8 Visual review.** We made a diagnostic sheet for each unconfirmed candidate (`files/diagnostics/<source_id>.png`). Each sheet shows the full-phase fold, odd/even, phase 0.5, a fold at 2P and the Gaia epochs at the TESS ephemeris. We used the sheets to find faults in the first automatic version (Section 4.4), not to change single classes by hand.

## 5. Results

### 5.1 Period and reference time (174 known planets)

![Figure 1](files/figures/fig1_known_period_epoch.png)

Figure 1. A: Ratio of the Gaia DR3 period to the literature period. Blue: 13 planets that agree within 0.1 %. B: Offset of the Gaia reference time from the nearest literature transit, in transit durations, for the current and the withdrawn table.

| Quantity | Value |
| --- | --- |
| Sources that match a confirmed planet in the NASA archive (2026-11-08) | 174 (Gaia DR3 lists 173 known planets and 41 new candidates; Gaia-1 b and Gaia-2 b are now confirmed) |
| Gaia period within 0.1 % of literature | 13 |
| Small-integer ratio (not 1) | 13 (1/3: 3, 2/7: 2, 1/4: 2, 1/2, 1/6, 1/8, 3/4, 7/8, 5/2: 1 each) |
| Reference time within 0.5 T14, P correct, current table | 13 of 13 (largest offset 0.35 T14) |
| Same, withdrawn table | 1 of 13 |
| Gaia `num_in_transit` median: correct P / wrong P / unconfirmed | 18 / 9 / 15 |

The 13 planets with a correct period are WASP-18 b, KELT-1 b, Gaia-1 b, Gaia-2 b, HATS-52 b, WASP-96 b, MASCARA-1 b, HATS-24 b, KELT-7 b, KELT-16 b, WASP-22 b, WASP-54 b and HATS-26 b.

### 5.2 Gaia epoch photometry shows the transits

![Figure 2](files/figures/fig2_gaia_epochs_alias.png)

Figure 2. A, B: Gaia G epochs of HAT-P-55 b folded at the literature period (3.5852 d) and at the Gaia table period (1.0147 d). The same four dimmed epochs (orange) are in transit at both periods. C: Dimming significance at the table ephemeris against the literature ephemeris for 174 known planets. Crosses: withdrawn-table ephemeris.

For the 161 known planets with a wrong period:

* the table ephemeris finds dimming > 3 sigma for 158;
* the literature ephemeris finds dimming > 3 sigma for 152;
* for 72, all in-transit epochs under the table ephemeris are inside a literature transit; for 118, half or more are;
* the withdrawn table ephemeris finds dimming > 3 sigma for 15.

The data thus support this explanation: the Gaia photometry contains the true transits, but the sparse Gaia sampling (a median of 3 in-transit epochs) lets many periods fit the same points. The table reports one of these aliases.

### 5.3 TESS check of the Gaia period

![Figure 4](files/figures/fig4_tess_snr_gaia_vs_best.png)

Figure 4. TESS BLS SNR at the Gaia period (+-0.3 %) against the best TESS SNR. Points on the diagonal have the Gaia period as the best TESS period. Known planets with a wrong Gaia period fall below the diagonal. Some still have SNR > 10 at the Gaia period, because deep transits fall partly into a wrong box.

### 5.4 The 40 unconfirmed candidates

![Figure 3](files/figures/fig3_new_candidates_tess_folds.png)

Figure 3. TESS light curves of the 35 unconfirmed candidates with TESS data, folded at the best TESS period. Colour: blue A, orange B, green C or E, grey D.

Table 1. Classes of the 40 unconfirmed candidates. Full data: `files/results/final_classification.csv`.

| Class | N | Gaia DR3 source_id (TESS period, d; note) |
| --- | --- | --- |
| A, planet-like, Gaia-linked, TOI | 8 | 2177849036734191744 (3.8100; TOI-3531.01 APC), 5735158757648658048 (2.3383; TOI-572.01 APC; phase-0.5 depth 0.5 ppt at 3.7 sigma, below the 5 % rule), 1982512068675148032 (3.9816; TOI-5964.01 PC), 5578530470116727936 (1.5304; TOI-6409.01 PC), 6061984878216187904 (2.2358; TOI-4968.01 PC), 5622845431584511744 (3.7063; TOI-2906.01 PC; Gaia P 2.5664), 1761329598050642432 (3.0235; TOI-5905.01 PC; Gaia P = 2 x TESS P), 4513959402068710656 (2.5411; TOI-5839.01 FP; neighbour EB Gaia DR3 4513959402068712448 and a Tmag 13.1 star at 13 arcsec) |
| A, planet-like, Gaia-linked, not a TOI | 5 | see Table 2 |
| B, EB indicators | 10 | 3450611154067089408 (2.9479; Gaia SB2C P = 5.8959 d, K1 = 73 km/s; true P = 5.896 d), 4535127268607000320 (7.0605; Gaia SB1 P = 7.0623 d, K1 = 22 km/s), 2015499135507395328 (1.6925; secondary 1.1 ppt), 460792064645351168 (1.8448; secondary 1.2 ppt), 6076338109120572032 (6.6370; odd/even 47 %, true P = 13.27 d), 4895643593611507584 (3.6485; depth 5.6 %), 2134884520357421824 (2.4957; KIC 11517719, VSX EA; RUWE 4.1), 435993129634439936 (2.2801; VSX EA), 66046877505607424 (1.2329; V shape, R = 2.3 R_J), 2930070089987088384 (2.4172; R = 2.7 R_J) |
| C, TESS transit not linked | 3 | 5348534425968598400 (6.6570; TOI-1991.01 FP; Gaia SB1 P = 6.659 d, K1 = 10 km/s; Gaia depth 18.6 mmag not seen), 4136481216073713280 (1.8164; one TESS sector; p_link = 0.09; Tmag 14.3 neighbour at 3.3 arcsec), 4677436783705094912 (13.79 or 27.57; weak) |
| D1, no TESS transit | 7 | 1622997463177004928 (expected SNR 442), 5481880275596734592 (311), 2196955937473897856 (146), 915921914974730368 (103), 5058575995484206592 (67), 5594445630358459648 (66), 4224807772566402560 (26; P = 16.3 d, partial coverage) |
| D2, broad variability | 1 | 2685725036820337408 |
| E, < 3 TESS epochs | 1 | 3215209257907330560 |
| D0, no TESS light curve | 5 | 4441830580248083328, 980773034927503104, 4368717970447788800, 1218568950151657216, 1797039953308437376 |

"Expected SNR" is the white-noise SNR that TESS would give for a box transit with the Gaia depth and duration at the Gaia period. These values are large. Thus TESS does not confirm these Gaia events. Possible causes are outliers in the sparse Gaia data or a wrong Gaia period with a duration that the BLS grid did not cover. We cannot separate these causes.

### 5.5 Five new planet candidates

![Figure 5](files/figures/fig5_non_toi_candidates.png)

Figure 5. Top: TESS flux folded at the final period. Bottom: Gaia G epochs folded at the same ephemeris. Orange points are inside the TESS transit window. The dashed line is the TESS depth.

Table 2. Class-A candidates that are not TOIs. Depths are TESS per-epoch means with empirical errors. R_p uses the Gaia FLAME stellar radius and no limb darkening. T0 is in BTJD = BJD - 2457000. Full data: `files/results/new_planet_candidates.csv`.

| Gaia DR3 | TIC | G | P_Gaia (d) | P_TESS+Gaia (d) | T0 (BTJD) | Depth (ppt) | Odd / even (ppt) | Phase 0.5 (ppt) | R_star (R_sun) | R_p (R_J) | Gaia epochs in transit | TESS epochs |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 5345417757181174144 | 93622019 | 12.57 | 2.8317 | 2.12388 | 1573.702 | 11.1 +- 0.2 | 11.2 / 11.0 | 0.1 +- 0.2 | 1.41 | 1.48 | 7 | 58 |
| 5431056347037926784 | 4638108 | 12.79 | 2.2086 | 2.20828 | 1520.076 | 16.0 +- 0.4 | 15.9 / 16.1 | -0.4 +- 0.3 | 1.44 | 1.81 | 5 | 37 |
| 5836096154165283712 | 87433458 | 12.82 | 1.6157 | 1.61548 | 1626.777 | 12.5 +- 0.4 | 12.7 / 12.3 | 0.4 +- 0.4 | 1.54 | 1.71 | 5 | 64 |
| 5432318139709900160 | 44997521 | 13.81 | 3.5497 | 3.54939 | 1546.486 | 22.0 +- 1.6 | 21.7 / 22.3 | 1.1 +- 1.4 | 0.80 | 1.17 | 4 | 40 |
| 6081267254094015616 | 169468881 | 12.56 | 2.0238 | 17.69188 | 2349.524 | 11.2 +- 0.5 | - / 11.4 | 0.1 +- 0.5 | 1.80 | 1.89 | 2 | 6 |

Notes:

* Gaia DR3 5345417757181174144: flat-bottomed transit with no secondary and equal odd/even depths. The Gaia period is 4/3 of the true period.
* Gaia DR3 5431056347037926784: V-shaped transit and R_p = 1.8 R_J. This can be a grazing EB. The TIC contamination ratio is 1.26, with a Tmag 15.6 star at 4.6 arcsec.
* Gaia DR3 5836096154165283712: TIC contamination ratio 1.42. A VSX eclipsing binary (Gaia DR3 5836096158575285888, P = 0.393 d) is nearby. Its period does not match.
* Gaia DR3 5432318139709900160: faintest source (G = 13.8). The TESS data are noisy.
* Gaia DR3 6081267254094015616: TESS shows a 1.1 % dip only on alternate epochs of an 8.846 d search period. The period is therefore 17.69 d, or a longer period that 17.69 d divides. Only 6 TESS epochs and 2 Gaia epochs constrain it. If confirmed, this is a warm giant planet.

For all five, the TESS signal falls on dimmed Gaia epochs of the resolved Gaia source (p_link = 0.002, the smallest value that 500 null trials can give). Gaia resolves stars at the arcsecond level. This makes a blend with a TESS neighbour more than a few arcseconds away improbable. It does not exclude a bound or chance companion closer than approximately 1 arcsec. RUWE is 0.86 to 1.06 for all five.

## 6. Interpretation

The corrected Gaia DR3 transit table is a reliable list of sources whose Gaia photometry contains transit-like dimmings. For most known planets it is not a reliable list of ephemerides. The cause is the Gaia scanning law, which gives few in-transit epochs, not the documented 2022 error. The 2023 correction fixed the reference times. The periods of the known planets were not changed (210 of 214 periods are equal in both tables). Users who need ephemerides should combine the Gaia epochs with an independent time series, as we do here with TESS.

The same alias problem applies to the new candidates. For 15 of the 23 unconfirmed candidates with a linked TESS signal, the Gaia period is not the true period.

## 7. Limitations

* **TESS products.** We used at most 8 sectors per source and only the SPOC, TESS-SPOC and QLP products. Five candidates have no such light curve. A pixel-level analysis (centroids, difference images) was not done. QLP and TESS-SPOC fluxes have different dilution corrections. Depths and radii can therefore be biased by tens of percent in crowded fields.
* **No limb darkening and no transit model fit.** Radii are from box depths and the Gaia FLAME radius. The 2 R_J rule flags 6 of 173 known planets.
* **Link test.** It succeeds for 76 % of known planets. Class C is thus weak evidence against a candidate.
* **Detrending.** The biweight filter makes small bumps next to long transits (Figure 5). These do not change the depth by more than its error, but they can bias the phase-0.5 depth for broad signals.
* **Non-detections.** The expected SNR assumes white noise and full phase coverage. It is too high for long periods (for example 16.3 d).
* **Vetting depth.** "Planet-like" means only that our tests found no EB indicator. It is not a confirmation. The five new candidates need radial velocities and high-resolution imaging.
* **Gaia epoch photometry** came from the AIP mirror, because the ESA DataLink server was not available. The AIP table has no `rejected_by_photometry` column; we used `variability_flag_g_reject` only.
* **Computing.** The host was heavily shared (load above 500 on 24 cores). This did not change the results. It limited the number of null trials to 500.

## 8. Provenance and hashes

Shared campaign dataset used in place: `datasets/exofop-tess-toi-table-20261108/exofop_toi.csv`, sha256 `ef22793ad87770c1795ff8da2243289b45e9282ff0bfb1ec3384fba1fbfd366a` (source `https://exofop.ipac.caltech.edu/tess/download_toi.php?sort=toi&output=csv`).

Files in this bundle (sha256):

* `files/data/gaia_dr3_vari_planetary_transit.ecsv`: `7638ac02740ad305d9a531fc805eb50bed780604ff15a0a8ea03608d2f63bb50`
* `files/data/gaia_dr3_vari_planetary_transit_13june2022.ecsv`: `7a5ac1861e6c82ca936b8b688483276bea3936f0fb9e7c34d5889fa3dd7606de`
* `files/data/gaia_dr3_source_214.ecsv`: `6ac668929d4148415c63fbec4b33a74c2c155e8acb04d1eee89993c9b9fd81f3`
* `files/data/gaia_nss_two_body_orbit_full.ecsv`: `c8e3c6d2c6de5d92cdda3ad26163ddde58f28962227564518d61e75710025f18`
* `files/data/nasa_pscomppars.csv`: `c23b38fa2c7c306056381a06436620d1e0255b6e3314b393a90f35618d5d3d4d` (retrieved 2026-11-08 16:16 UTC)
* exoplanet.eu CSV (not included): `4b835f52d097599f3593751f352c6ab8c53236ff3ec78b770b8b85cb489038ff`

TESS light curves are not included (655 MB). `files/results/tess_lightcurve_manifest.csv` lists, for each of the 992 files, the MAST URI, the download URL, the size and the sha256. The Gaia G epoch photometry of all 214 sources is in `files/data/gaia_dr3_epoch_photometry_G_214.csv` (times in BJD(TCB) - 2455197.5).

Software: Python 3.12, numpy 2.5.4, astropy 8.0.2 (BoxLeastSquares), pandas 2.3.3, scipy 1.18.1, matplotlib 3.11.2, lightkurve 2.6.0, astroquery 0.4.11, wotan 2.1.

## 9. Reproduction

```
uv venv --python 3.12 --system-site-packages .venv && . .venv/bin/activate && uv pip install astroquery lightkurve wotan
# layout: work/code (these scripts), work/data, work/results; ../datasets holds the shared TOI table
python code/fetch_gaia_tables.py        # Gaia DR3 tables (ESA TAP, asynchronous); NASA archive URL is in the file
python code/search_tess.py 12            # TIC match + TESS product lists -> data/search/
python code/download_tess.py 8           # light-curve download plan and MAST download -> data/lc/
python code/fetch_gaia_epoch_aip.py      # Gaia G epochs (AIP TAP) -> data/gaia_epoch/
python code/crossmatch.py                # NASA archive / TOI cross-match
python code/known_ephem.py               # Section 4.1
python code/run_vet.py --force           # Section 4.3 (calls vet.py)
python code/gaia_fold.py                 # Section 4.2
python code/summarize.py                 # combined table
python code/refine.py                    # Section 4.4
python code/link.py                      # Section 4.5
python code/classify.py                  # Section 4.6-4.7
python code/final_numbers.py             # numbers.json
python code/fig_known.py; python code/fig_new.py; python code/fig_cands.py; python code/diag.py
```

To check the TESS inputs, compare the sha256 of each downloaded file with `tess_lightcurve_manifest.csv`. The Gaia ESA archive gave HTTP 503 for synchronous jobs during this work; use asynchronous jobs.

## 10. Related campaign work

* `sci:sha256:987dcc64327f9be8bea39fd94eb38a0faf60622c9e28a514f449820e95182c81` matched Gaia DR3 eclipsing binaries to TOIs. That study used the Gaia EB table. We use the transit table.
* `sci:sha256:d57ede30e514369ac650d3ec09f73996d2292c6037da34fe5cc0254e2ea71fda` used TESS at Gaia DR3 SB1 conjunction times. We use Gaia SB1/SB2 orbits as an EB indicator.
