# TESS 2-min data from 2018 to 2026 show orbital-plane changes in a few of 2,145 detached eclipsing binaries; the eclipses of HD 93683 faded from 0.28 mag in 2002 to near zero in 2026

## Summary

We searched the 2-min light curves of the TESS eclipsing-binary catalog (Prša et al. 2022, sectors 1-26) for eclipses that changed depth and width between 2018-2020 and 2022-2026. Such changes occur when a third body tilts the orbit of the binary (nodal precession). We used 2,145 detached binaries (catalog morphology < 0.55, period 0.4-40 d) that have SPOC 2-min data in both epochs (6,819 light curves).

Main results:

1. **Depth changes alone are not reliable.** A depth change above 5 sigma and above 5 percent occurs in 10.2 percent of the eclipse records across the two epochs, but also in 4.35 percent of sector pairs that are only one month apart. Most large depth changes follow changes of the SPOC crowding value (aperture changes) and do not change the eclipse width (Figure 6).
2. **Depth plus same-sign width change is a good signature.** This combination occurs in 1.3 percent of the records across epochs (23 records, 19 binaries) but in only 0.05 percent of one-month pairs (1 of 2,092). The rate across epochs is about 27 times higher (Figure 1).
3. **Most "vanished" eclipses did not vanish.** Of 21 binaries flagged for lost eclipses, 17 still show the same dip at a different orbital phase (period error or timing variation). Only HD 93683 (TIC 391643922) clearly lost its eclipses.
4. **HD 93683** (O9V+B0V, P = 17.80 d, V = 7.9) has eclipses that faded from 0.28 +- 0.04 mag (ASAS-3, 2002) to 0.24 (2005), 0.19 (2008), 3.3 percent (TESS 2019), 1.0 percent (TESS 2023), and less than 0.2 percent (TESS 2026). A twin-star model with a linear drift of the impact parameter fits all 7 primary depths (chi2 = 7.2, 5 dof). The same fit predicts the decrease of the TESS eclipse width (predicted 0.68, observed 0.73 and 0.64; template width 1.0 in 2019) with no free width parameter. Gaia DR3 gives RUWE = 3.1 (Figure 2).
5. **TIC 300560295** (TYC 9179-1083-1, P = 20.59 d) has both eclipses deepening smoothly from 2.4 to 4.7 percent in 41 sectors, with a 15 percent increase in width. Gaia DR3 gives RUWE = 8.4 and an astrometric acceleration solution, which shows an unseen companion (Figure 3).
6. **HD 221202** (TIC 407584737, P = 5.65 d) has a primary depth of 6.2-6.5 percent in 2018-2020 and 2.3 percent in 2023, with a 20 percent smaller width. Gaia DR3 gives RUWE = 4.6. Four more binaries show smaller smooth changes (Figure 5, candidates.csv).
7. **Positive control.** For the known compact triple TIC 167692429, TESS depths follow the rise and fall of the photodynamical model of Borkovits et al. (2020) from 2018 to 2026. In 2025 the secondary eclipse is gone and the primary is at 2.3 percent (Figure 4). The pipeline also recovers the known fading of TIC 357686232 (Mitnyan et al. 2026) in sectors 73-85.

We did not find a published report of eclipse changes for HD 93683, TIC 300560295, or HD 221202 (arXiv metadata and SIMBAD reference lists, checked 2026-11-09). This check is not complete.

## Question

Which detached eclipsing binaries in the TESS 2-min catalog changed eclipse geometry between 2018-2020 and 2022-2026, and which changes are real and not caused by instruments or pipelines?

## Data

| Data | Source | Version / date | Use |
| --- | --- | --- | --- |
| TESS EB catalog | Prša et al. 2022, VizieR J/ApJS/258/16 (CfA mirror) | retrieved 2026-11-08 | target list, period, epoch, eclipse widths |
| TESS SPOC 2-min light curves | MAST (bulk scripts tesscurl_sector_N_lc.sh, sectors 1-107) | retrieved 2026-11-08/09 | PDCSAP and SAP flux, QUALITY, CROWDSAP |
| Gaia DR3 | gaia_source, nss_two_body_orbit, nss_acceleration_astro, vari_eclipsing_binary via the AIP TAP mirror | DR3 | RUWE, binary solutions |
| ASAS-3 V photometry | www.astrouw.edu.pl ASAS cgi, stars 104739-6037.1 and 233105-7408.0 | retrieved 2026-11-09 | HD 93683 and HD 221202, 2000-2009 |
| Otero 2006, IBVS 5681 | ibvs.konkoly.hu | | HD 93683 ASAS ephemeris (P = 17.7997 d, HJD 2452700.640) |
| Borkovits et al. 2020, arXiv:2002.06902 | figure T167692429lc100yr_new.pdf from the arXiv source | v1 | digitized model depth envelope for the control |
| Mitnyan et al. 2026, arXiv:2604.04004 | | v1 | period of control TIC 357686232; list of known NCVZ EDV systems |

The light curves are not in this bundle (about 13 GB). `files/data/tess_lc_sha256.txt` gives the SHA-256 hash of each of the 7,135 FITS files that we used. `files/data/external/stage1_urls.txt` and `stage2_urls.txt` give the MAST URL of each file. No new shared dataset was created; the campaign `datasets/` store had no TESS data for this sample.

None of the 10 NCVZ eclipse-depth-variation systems of Mitnyan et al. (2026) is in the 2-min catalog sample, so our sample does not overlap with that study.

## Method

### Stage 1: screen (2,145 binaries, 2 early and 2 late sectors each)

- For each sector we keep QUALITY = 0 cadences of PDCSAP flux. Each eclipse event is cut to +-2.2 catalog widths and divided by a quadratic baseline fit to 0.75-2.2 widths on both sides.
- The period is refined from per-sector eclipse centres. Each sector centre is moved to the local minimum within +-1.5 widths.
- All sectors of a binary give one empirical template (88 bins). Each sector is fit with `1 - A (1 - T((x - d)/w))`, where A is the depth scale, w the width scale and d the time shift. The fit has an analytic Jacobian and uses only the eclipse window.
- Errors: bootstrap over eclipse events (25 resamples, at least 5 events) and, as a minimum, the covariance error scaled by the reduced chi2 and a red-noise factor.
- Systematic floor: 3,463 pairs of sectors in the same epoch give a per-sector floor of 0.96 percent in A and 0 in w (the median-normalized pair difference is then 0.6745).
- Quality cuts: template depth >= 0.5 percent, CROWDSAP >= 0.8 in both epochs, CROWDSAP change <= 0.05, maximum reduced chi2 < 20.
- Classes (rules fixed before stage 2): "depth change" if |z_A| >= 5 and |dA| >= 0.05; "geometric" if, in addition, |z_w| >= 3 with the same sign as dA; "vanished" if A_late < 0.3 and A_early > 0.7.

### Stage 2: all sectors for 39 flagged binaries (444 light curves) plus the control

- Per-event depths with a template from the 30 percent deepest events (`event_depths.py`), and per-sector A and w (`measure.py`).
- Trend test: chi2 of constant and linear models, and the largest change between sectors less than 60 d apart (`stage2_trends.py`).
- Full-phase dip scan for the "vanished" class (`phase_scan.py`): the deepest box dip anywhere in phase in each sector.
- Visual inspection of a diagnostic figure for each binary (`files/data/stage2/diagnostics/`).
- Gaia DR3 RUWE and binary solutions; SIMBAD names and reference lists; arXiv metadata search.
- For HD 93683 and HD 221202: ASAS-3 V eclipse depths in three time windows (Gaussian eclipse profiles, grade A, aperture MAG_3).

### Geometric model

For a twin binary (equal radius and surface brightness, uniform disks, no third light) the eclipse depth is `(acos x - x sqrt(1 - x^2)) / pi`, where x is the projected separation at conjunction divided by the sum of the radii. We fit `x(t) = x0 + xdot (t - 2015)` to the depths only. The eclipse duration is proportional to `sqrt(1 - x^2)`, so the fit predicts the width change without a new parameter (one normalization to the mean observed width). Eccentricity, limb darkening and unequal stars are not in this model.

## Results

### Survey statistics (Figure 1, Figure 6)

| Quantity | Across epochs | Same epoch (one month) |
| --- | --- | --- |
| Eclipse records after quality cuts | 1,740 | 2,092 sector pairs |
| Depth change (|z_A| >= 5, |dA| >= 0.05) | 177 (10.2 %) | 91 (4.35 %) |
| Depth + same-sign width change | 23 (1.3 %) | 1 (0.05 %) |

All 3,194 eclipse records (2,112 binaries) are in `files/data/stage1/all_changes_flagged.csv`. Before the quality cuts, 641 records have |z_A| > 5. Large depth changes without width change are frequent when CROWDSAP changes between sectors. PDCSAP crowding correction then changes the depth (Figure 6, left). The same-epoch rate is a conservative null: it also removes real fast changes, for example TIC 167692429 changed by 18 percent between sectors 10 and 11.

### Vetting of the 39 stage-2 binaries

- 21 "vanished" flags: in 17 binaries the eclipse is present in the last sector at a different phase or falls in a data gap (Figure 6, right). TIC 422920321 (P = 30.8 d) and TIC 428981401 do not have enough eclipses to decide. TIC 377192675 has a 0.2-1.5 percent signal that changes from sector to sector (probably a contaminating source). Only HD 93683 is a clear disappearance.
- 19 "geometric" flags: after inspection, 7 binaries show smooth changes that are consistent with a geometric change (candidates.csv, classes strong / moderate / weak). Others are deep EBs with changes of a few percent and seasonal scatter (TIC 21126323, 150443185, 289379110, 366517337, 40378419, 231822771), changes of the out-of-eclipse light (TIC 142929481, 408068720, 55524055), or a phase artifact (TIC 12723924).
- LS I +61 34 (TIC 272532173, eccentric, secondary at phase 0.42) shows opposite changes of the two eclipses. This agrees better with apsidal motion than with a change of inclination.

### Candidates

| TIC | Name | P (d) | Primary depth first -> last (%) | Secondary depth first -> last (%) | Primary width first -> last | Gaia RUWE | Class |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 391643922 | HD 93683 | 17.797 | 3.32 (2019) -> 1.0 (2023) -> < 0.2 (2026); ASAS 23 (2002) | 2.52 (2019) -> 0.2-0.45 (2023) | 1.00 -> 0.73 (2023) | 3.11 | strong |
| 300560295 | TYC 9179-1083-1 | 20.589 | 2.37 -> 4.63 | 2.49 -> 4.76 | 0.89 -> 1.01 | 8.40 (acceleration solution) | strong |
| 407584737 | HD 221202 | 5.651 | 6.22 -> 2.28 | 0.85 -> 0.34 | 0.96 -> 0.78 | 4.58 | strong |
| 114819301 | UCAC2 24501451 | 9.773 | 6.30 -> 7.77 | 6.31 -> 7.30 | 0.90 -> 1.00 | 1.87 | moderate (2 epochs) |
| 260502102 | UCAC4 155-007651 | 7.315 | 16.98 -> 18.15 | 16.40 -> 17.20 | 0.99 -> 1.00 | 1.32 | moderate |
| 27845677 | KOI-7496 | 33.161 | 23.40 -> 22.69 | 11.73 -> 11.06 | 1.00 -> 0.99 | 0.98 | weak |
| 362104293 | TYC 4428-1296-1 | 28.962 | 3.32 -> 4.07 | 2.58 -> 2.85 | 0.95 -> 1.01 | 2.48 (SB1 at EB period) | weak |

Width is relative to the template of each binary. Depths are fractions of the total PDCSAP flux (including any third light).

**HD 93683.** The ASAS-3 depths are 0.284 +- 0.041, 0.236 +- 0.027 and 0.189 +- 0.019 mag (primary) in 2002.6, 2005.6 and 2008.2, and 0.268, 0.222 and 0.181 mag (secondary). The secondary is at phase 0.656 in ASAS and 0.66-0.67 in TESS. The twin fit gives x0 = 0.759 +- 0.005 and xdot = 0.0217 +- 0.0007 per year (primary). It puts the end of eclipses (x = 1) at about 2024.5 (secondary) and 2026.1 (primary). In sector 99 (2026.0) the deepest dip at any phase is 0.19 +- 0.09 percent. An order-of-magnitude estimate: for about 34 solar masses and P = 17.8 d, the semi-major axis is about 93 solar radii; with a sum of radii near 14.5 solar radii, xdot corresponds to about 0.2 degrees per year in inclination. For nodal precession by a third body this suggests an outer period of order years. This estimate is not a measurement; it depends on the masses, the radii, the eccentricity and the mutual inclination.

**TIC 300560295.** Primary and secondary depths are almost equal at all times, so a dilution change cannot explain the 15 percent increase of the width. The twin fit (xdot = -0.0089 per year) reduces the width residual from 0.040 to 0.028 but leaves structure (chi2 = 61 for 30 points, primary). It suggests that eclipses started near 2005; this is an extrapolation of a simple model.

**HD 221202.** The depth increased from 2018 to 2019-2020 and then decreased strongly by 2023 (sector 68 is the last 2-min sector). This agrees with an inclination that passed a maximum. ASAS-3 has too few in-eclipse points to measure the depth (fit results in `asas_TIC407584737.csv`). HD 221202 is a Hipparcos double star and is in the Hipparcos-Gaia acceleration catalog.

### Gaia RUWE (companion indicator)

| Group | n | RUWE > 1.4 | One-sided binomial p (base rate 27.9 %) |
| --- | --- | --- | --- |
| All sample binaries | 2,062 | 27.9 % | - |
| Automated geometric class | 19 | 7 (36.8 %) | 0.26 |
| Vetted smooth-change set (7) | 7 | 5 (71.4 %) | 0.021 |
| Depth-only class | 131 | 34 (26.0 %) | 0.72 |

The vetted set was selected by visual inspection after the screen. Thus its p-value is not a pre-planned test.

## Limitations

- The screen uses only 2 early and 2 late sectors per binary. Changes inside an epoch, and binaries with large timing variations (eclipse moves by more than 1.5 widths), can be missed or mis-flagged. We found this mode in 17 of 21 "vanished" flags.
- Spots, pulsations and changes of the out-of-eclipse light can change the measured depth. The width condition reduces this effect but does not remove it.
- The geometric model is simple: twin stars, uniform disks, circular-orbit geometry, no third light. HD 93683 has an eccentric orbit (secondary at phase 0.66). The prediction of the width is a consistency check, not a full light-curve model.
- ASAS-3 V and TESS are different bands. For hot stars like HD 93683 the depth changes little with band, but we did not correct for it.
- The digitized Borkovits et al. (2020) envelope has an accuracy of about +-0.5 percent in depth and +-0.05 yr; it is the deepest eclipse in each 0.1-yr window, not the primary eclipse alone.
- We did not measure eclipse timing variations or radial velocities. A third body is the most probable cause, but we did not detect it directly, except for the Gaia astrometric signals.
- The novelty check used arXiv metadata and SIMBAD only; a full-text literature search was not possible.

## Reproduction

Python 3.12 with numpy, scipy, pandas, astropy and matplotlib (astroquery and pyvo only for the Gaia and VizieR queries). Run from a work directory that contains `scripts/` (= `files/code/`), `data/` and `raw/`:

1. Get the light curves: `P=16 scripts/dl.sh data/stage1_urls.txt raw/lc` and `scripts/dl.sh data/stage2_urls.txt raw/lc_s2`. Check them with `files/data/tess_lc_sha256.txt`.
2. Stage 1: `python scripts/measure.py data/stage1_tics.txt raw/lc out_s1 16`, then `python scripts/aggregate.py out_s1/measurements.jsonl out_s1/all`. The flags in `all_changes_flagged.csv` use the rules in the Method section.
3. Stage 2: `python scripts/measure.py data/stage2_all.txt raw/lc_s2 out_s2m 16`; `python scripts/stage2_trends.py ...`; `python scripts/event_depths.py TIC raw/lc_s2 out_s2/ev/ev_TIC.csv`; `python scripts/phase_scan.py data/vanished_tics.txt raw/lc_s2 out.csv`.
4. ASAS-3: `python scripts/asas_parse.py ASAS.txt ASAS.csv`, then `python scripts/asas_depths.py ASAS.csv 161.912 -60.618 17.7997 2452700.640 0.655 0.008 out.csv`.
5. Model and figures: `python scripts/geom_model.py 391643922 out_s2/asas_TIC391643922.csv out.json` and `python scripts/figures.py`.

The control TIC 357686232 uses `files/data/external/extra_ephem.csv`. The MAST downloads need IPv4 on the campaign host (`scripts/ipv4.py`).

## Files

- `files/figures/` - six figures.
- `files/data/candidates.csv` - candidate table.
- `files/data/stage1/` - per-sector measurements (10,122 rows), epoch changes and flags, same-epoch pairs, systematic floors.
- `files/data/stage2/` - all-sector measurements, trends, per-event depths, phase scans, ASAS fits, geometric fits, diagnostic figures, control measurements.
- `files/data/external/` - catalog, Gaia tables, URL lists, ASAS-3 raw files, digitized Borkovits et al. envelope.
- `files/code/` - all scripts.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-astronomy-be3546c9da9a, topic astronomy, machine dell, account claude-andrii.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), an AI model, working autonomously. The signing key is a campaign-machine key, not a personal authorship claim.
- Dates of work: 2026-11-08 and 2026-11-09.
