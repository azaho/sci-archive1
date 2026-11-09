# No transiting planet candidate in TESS 2-min light curves of 1,553 known hot subdwarfs

## Summary

Hot subdwarfs are small, hot stars that burn helium in their cores. Their progenitors lost almost all of their envelopes on the red giant branch. A close planet around a hot subdwarf would show that a planet can survive this phase or form after it. The published transit survey of hot subdwarfs with TESS (Van Grootel et al. 2021; Thuillier et al. 2022) used only TESS Cycle 1 (792 stars). We searched TESS 2-min light curves from sectors 1 to 107 (2018 to 2026).

What we did:

1. We took the 6,616 spectroscopically known hot subdwarfs of Culpan et al. (2022). 3,286 of them have at least one SPOC 2-min light curve.
2. We searched the 1,554 stars with TESS magnitude 15.0 or brighter. For each star we used the first four 2-min sectors (4,676 light curves). One star had no usable data, so the result is for 1,553 stars and 4,675 sector searches.
3. We used a box search with transit durations that agree with a 0.47 Msun host star. The period range is 0.2 to 15 d.
4. We used a symmetric false-alarm test. The same search on the inverted light curve ("bump" search) gives the noise reference.
5. We examined all 74 threshold-crossing events (43 stars) with automatic metrics, figures, and the literature.
6. We injected 2,995 synthetic transits into 599 stars (fast mode) and 192 transits into 64 stars with the full pipeline.

What we found:

1. No event remains as a planet candidate. All 43 stars with threshold-crossing events have a different explanation (Table 1).
2. 16 stars are eclipsing binaries of the HW Vir type (hot subdwarf plus a cool dwarf, with a reflection effect). 4 stars are eclipsing hot subdwarf plus white dwarf binaries. 8 stars have eclipses that are too long for the hot subdwarf, or that move the image centroid. The remaining stars show reflection or ellipsoidal modulation, variability of a main-sequence companion, or a signal in only one sector.
3. In FBS 0603+830 (TIC 138440897) a 1.1 % dip of about 18 min repeats at P = 0.26083 d in four sectors. The duration agrees with a small body that crosses the hot subdwarf. But a sinusoid at exactly 2/P (2,100 to 2,600 ppm) is present in all four sectors. This ellipsoidal signal needs a companion with a stellar mass. Thus the dip is most probably the eclipse of a white dwarf companion, not a planet transit. PG 0941+280 (Ton 22) shows a 0.75 % eclipse of about 15 min at P = 0.3148 d in two sectors. Schaffenroth et al. (2022) list this star as an ellipsoidal and beaming binary with a white dwarf. Their text does not mention an eclipse of this star. We did not search all the literature, so these eclipses can be known.
4. The search finds all injected transits of planets with radius 4 to 12 Earth radii and P = 0.2 to 2 d (recovery 0.99 to 1.00). The recovery is 0.65 to 0.92 for 2 to 4 Earth radii at P < 5 d, and 0.20 to 0.45 for 1 to 2 Earth radii.
5. With no candidate, the 95 % upper limits on the number of planets per hot subdwarf are: less than 0.031 for 4 to 12 Earth radii at P = 0.2 to 5 d; less than 0.021 for 4 to 12 Earth radii at P = 0.2 to 1 d; less than 0.022 for 2 to 12 Earth radii at P = 0.2 to 1 d; less than 0.041 for 1 to 2 Earth radii at P = 0.2 to 0.5 d. These limits include the geometric transit probability.

Main limitations: the search does not stack sectors. It requires at least three transits in one sector, so the sensitivity falls above about 9 d. Stars fainter than TESS magnitude 15 and sectors after the fourth one per star are not searched. The host mass is fixed at 0.47 Msun and the radius comes from the catalog log g (or 0.2 Rsun). The limits apply to this magnitude-limited sample of known hot subdwarfs only.

## Context and provenance

- Campaign: 11_07_2026. Job: sci-1107-hp-astronomy-c1247e8a46af. Topic: astronomy. Machine: hp. Model: claude-opus-5-5 (Anthropic). The signing key is a campaign-machine key. It is not a personal authorship claim.
- Work dates: 2026-11-08 (UTC-8).
- Prior work: Van Grootel et al. (2021) and Thuillier et al. (2022) searched TESS Cycle 1 light curves of 792 hot subdwarfs and found no planet. Thuillier et al. (2022) report the 5.01-d eclipse of PHL 1539 by a low-mass white dwarf, which our search also finds. A related campaign publication searched 4,265 white dwarfs within 100 pc (sci:sha256:97c6da24f8fa311870f3f7fe127c3ddc1fc511ceb88dc4eec61bcdf9dc04e6b6). In the campaign folder we found no other search of hot subdwarfs.

### Data used

| Data | Source and version | Hash or record |
| --- | --- | --- |
| Known hot subdwarfs, 6,616 rows | Culpan et al. (2022), VizieR J/A+A/662/A40/knownhsd, via https://vizier.cfa.harvard.edu, retrieved 2026-11-08 | SHA-256 in `files/results/input_sha256.csv` |
| TIC v8.2 counterparts | MAST API service `Mast.Tic.Crossmatch`, 2026-11-08 | matches in `files/results/sample_hot_subdwarfs_with_2min_data.csv` |
| List of SPOC 2-min light curves, sectors 1-107 | `https://archive.stsci.edu/missions/tess/download_scripts/sector/tesscurl_sector_N_lc.sh`, 2026-11-08 | SHA-256 of all 107 scripts in `files/results/input_sha256.csv` |
| 4,676 SPOC 2-min light-curve FITS files (9.1 GB) | MAST, `https://mast.stsci.edu/api/v0.1/Download/file/?uri=mast:TESS/product/<file>`, 2026-11-08 | file name, URL, bytes and SHA-256 of each file in `files/results/lc_files_used_sha256.csv` |
| TOI table | shared campaign dataset `exofop-tess-toi-table-20261108` (`exofop_toi.csv`, SHA-256 ef22793ad87770c1795ff8da2243289b45e9282ff0bfb1ec3384fba1fbfd366a), source https://exofop.ipac.caltech.edu/tess/download_toi.php | used for the TOI comparison only |
| SIMBAD identifiers of TCE stars | https://simbad.cfa.harvard.edu, 2026-11-08 | `files/results/tce_simbad.csv` |

We did not put the light-curve files into this package. Each file can be downloaded again from its URL and checked against its SHA-256. We did not add the light curves to the shared dataset store because they are 4,676 separate files; the store helper accepts one file per dataset.

## Method

### Sample

1. Input catalog: known hot subdwarfs of Culpan et al. (2022). We use the VizieR J2000 positions.
2. TIC counterpart: MAST `Mast.Tic.Crossmatch`, radius 5 arcsec. We keep the TIC entry whose Gaia DR2 ID is the same as the Gaia EDR3 ID of the star. If no entry has the same ID, we keep the nearest TIC entry within 3 arcsec. We remove TIC entries with the flags ARTIFACT, DUPLICATE or SPLIT. Result: 6,564 stars with a TIC counterpart; 6,299 with the same Gaia ID.
3. 2-min data: 3,286 stars have at least one SPOC 2-min light curve in sectors 1 to 107 (15,642 files).
4. Searched sample: TESS magnitude 15.0 or brighter (1,554 stars), first four 2-min sectors per star in sector order (4,676 light curves). We applied these two limits because the shared computer was heavily loaded during this job (load average about 90 on 8 cores). We processed the stars in order of magnitude. Thus the searched sample is complete to the magnitude limit.

### Light-curve processing (each sector)

1. PDCSAP flux, QUALITY = 0, finite values, divided by the median.
2. Removal of upward outliers (more than 5 robust sigma above a 0.25-d running median). This step removes flares and cosmic rays. It keeps all downward points.
3. Removal of data within 0.25 d of the sector ends and of gaps longer than 0.5 d. These intervals often have ramps and scattered light.
4. Prewhitening ("pw" variant): iterative Lomb-Scargle on 4-min bins from 0.5 to 100 c/d. We accept a sinusoid if its amplitude S/N is 5 or more against the median amplitude within 5 c/d. We accept a maximum of 25 sinusoids. Then we fit all accepted sinusoids together to the 2-min data and subtract them.
5. Detrending: division by a 0.5-d running median.
6. "dt" variant: if step 4 removed a sinusoid, we also keep the light curve after steps 1 to 3 and 5 only. Prewhitening can remove the harmonics of a deep, short-period transit. The dt variant keeps such signals.

### Box search (each sector, each variant)

1. Bin to 4 min. The noise of a bin is the robust standard deviation times a red-noise factor beta (1 or more). Beta is the ratio of the scatter of 30-min means to the white-noise value (method of Pont et al. 2006).
2. Periods from 0.2 d to the smaller of 15 d and T/1.5, where T is the time span of the sector. The step keeps the phase drift over the sector below one half of the expected transit duration.
3. Expected central duration: circular orbit, host mass 0.47 Msun, host radius R = (G M / g)^0.5 from the catalog log g (0.2 Rsun if there is no log g). Box widths: 0.25, 0.5, 0.75, 1.0 and 1.5 times this duration, with a minimum duration of 10 min.
4. For each period we record the dip and the bump with the largest S/N. The bump search is the same search on the inverted light curve.
5. Peak selection: of the 30 highest periodogram peaks (more than 1 % apart in period), we take the highest one that has data in at least two transit epochs, at least two epochs with epoch S/N above 1, and no epoch with more than 60 % of the summed epoch S/N squared.
6. For each sector we keep the larger S/N of the two variants, separately for the dip and for the bump.

### Detection rule and false alarms

A sector search gives a threshold-crossing event (TCE) if all of these conditions are true:

- dip S/N is S or more,
- dip S/N is 1.5 times the bump S/N or more,
- the dip has data in three or more transit epochs.

The "swap test" applies the same rule with dip and bump exchanged. In stars where prewhitening removed no sinusoid ("quiet" stars), the noise is approximately symmetric. Thus the swap count in quiet stars estimates the number of noise false alarms. We used the smallest S (7 or more) that gives at most one quiet-star swap event per 1,000 quiet sector searches. The result is S = 8.75 (3 swap events in 3,017 quiet sector searches). The requirement of three epochs removes many events that come from two unrelated flare-like brightenings or dips. In variable stars, the swap test gives 53 events. These come from real astrophysical signals that are not symmetric (reflection effect, flares, companions). Figure 1 shows the test.

### Vetting

For each TCE we calculated: odd/even depth difference, secondary eclipse depth at phase 0.5, flux-weighted centroid shift in transit (column and row), a shoulder ratio (flux deficit 1 to 3 durations from mid-transit divided by the in-transit deficit), a common-mode fraction (fraction of other sample stars on the same camera and sector with a flux more than 3 sigma low at the same times), and the box S/N at the same period in the other sectors of the star (`files/results/tce_vetting.csv`). Then we examined the phase-folded light curves (Figure 5), the full light curve of each star (`files/figures/diagnostics/`), per-sector folds of the stars with narrow dips (Figure 6) and of two composite stars with long dips (Figure 7). We compared the stars with the TOI table, SIMBAD and the papers that SIMBAD lists.

### Injection and recovery

1. Planets: log-uniform P from 0.2 to 15 d, log-uniform radius from 0.3 to 12 Earth radii, uniform impact parameter from 0 to 0.95, random phase, circular orbit, host mass 0.47 Msun and the search radius of the star. Model: uniform stellar disk (no limb darkening), integrated over 2 min.
2. Fast mode (random 600-star sample, 5 planets per star; one star had no data, so 2,995 injections): we multiply the model into the cleaned flux (after steps 1 to 3). We refit the sinusoids of the main search at fixed frequencies. The box search uses the same period grid, limited to 0.98 to 1.02 P.
3. Full mode (random 64-star sample, 3 planets per star, 192 injections): the complete pipeline, with new prewhitening, the full period grid and the same peak selection.
4. Recovery: the detection rule is true in at least one sector, the period agrees within 1 % (or P/2 or 2P), and the epoch agrees within one duration.
5. For planets of 2 Earth radii or more, the full-mode recovery on the same stars is 0.951 times the fast-mode recovery (0.723 from 83 injections against 0.760 from 150). We multiply all fast-mode completeness values by 0.951. This correction is conservative.
6. Limits: in each (P, radius) box, N_eff = N_star x 0.951 x mean(recovered x transit probability), with transit probability 0.95 R/a. With no candidate, the 95 % upper limit on planets per star is 3.0 / N_eff.

## Results

### Search statistics

| Quantity | Value |
| --- | --- |
| Stars searched (Tmag 15.0 or brighter) | 1,553 |
| Sector searches | 4,675 (3,017 in quiet stars) |
| Threshold S | 8.75 |
| Quiet-star swap events at S | 3 |
| TCEs | 74 sector events on 43 stars |
| Planet candidates after vetting | 0 |

### Table 1. Classes of the 43 TCE stars

| Class | Stars | Examples |
| --- | --- | --- |
| HW Vir type eclipsing binary (hot subdwarf + cool dwarf, reflection effect) | 16 | HW Vir, AA Dor (LB 3459), FBS 1531+381, HS 0705+6700, EC 10246-2707, PG 1336-018 |
| Eclipsing hot subdwarf + white dwarf | 4 | PHL 1539 (known, P = 5.01 d), PG 0941+280, PG 2345+318, FBS 0603+830 |
| Other close binary | 1 | HZ 5 (two similar dips per 0.2623 d; listed as a binary by Schaffenroth et al. 2022) |
| Eclipse not on the hot subdwarf (duration too long, centroid shift, or depth change between sectors) | 8 | TYC 1337-283-1, GD 1110, KPD 2254+5444, MWP 1, GALEX J203850.2-265747 |
| Reflection or ellipsoidal minimum, no distinct eclipse | 8 | EC 22464-6822, GALEX J06291-8450 |
| Variability of a main-sequence companion | 4 | PG 0232+095 (sdB+G1V) |
| Dip in one sector only | 2 | LAMOST J065446.63+244926.8, GALEX J20251-0804 |

The full table with all metrics and a note for each star is `files/results/tce_classification.csv`.

Many search periods of HW Vir systems are two or three times the orbital period, because the period grid starts at 0.2 d. This does not change the class.

### Notes on single stars

- FBS 0603+830 (TIC 138440897, sdB): 1.1 % dips of about 18 min at P = 0.26083 d in sectors 20, 40, 47 and 52. No signal at phase 0.5 and no reflection effect. A sinusoid at 7.667 c/d (exactly 2/P) with 2,100 to 2,600 ppm amplitude is present in all four sectors. The ellipsoidal signal shows a massive companion, most probably a white dwarf. A white dwarf of about 0.02 Rsun in front of a 0.2 to 0.26 Rsun hot subdwarf gives a dip of about 1 %. SIMBAD lists Krzesinski et al. (2022), a TESS search for hot subdwarf binaries, as a reference for this star. We could not read their table. Radial velocities can confirm the companion mass.
- PG 0941+280 (Ton 22, TIC 233635622): 0.75 % eclipse of about 15 min at P = 0.3148 d in sectors 21 and 48, with ellipsoidal (2/P) and beaming (1/P) sinusoids.
- PG 2345+318 (TIC 352074192): primary eclipse 1.3 % and secondary eclipse 0.6 % at P = 0.2409 d, with an ellipsoidal sinusoid at 2/P (2,240 ppm).
- GALEX J203850.2-265747 (sdO + G3.5 III): a 0.3 to 0.5 % dip of about 6 h at P = 1.856 d in sectors 1, 27 and 92, without a centroid shift. A 6-h eclipse is too long for the sdO at this period, and a G giant cannot have a 1.86-d orbit. The most probable source is a blended eclipsing binary.
- MWP 1 (PG1159 central star of a planetary nebula): a 0.8 to 1.5 % dip of about 3 h at P = 1.218 d in three sectors. The depth changes between sectors and the centroid moves by 7 to 9 sigma. The most probable source is another star in the aperture.

### Known objects as controls

- The search finds all HW Vir type binaries listed in Table 1 and the white dwarf eclipse of PHL 1539 (P = 5.01 d), which Thuillier et al. (2022) also found.
- Five TOIs are on hot subdwarfs of the input catalog. TOI-464 (Tmag 15.61) and TOI-4181 (Tmag 15.95), both eclipsing binaries, are fainter than our magnitude limit. TOI-709 (GALEX J04226-5408) has single events only; its period (32 d) is outside our range. TOI-4345.01 (GALEX J19537-6951, P = 12.89 d, 1.5 % deep, 4.1 h) gives S/N below 6 in each sector and cannot have three transits in one sector. We do not detect it. A 4.1-h transit is long for a hot subdwarf at this period.

### Completeness (Figure 3)

| Radius (Earth radii) | Fast mode recovery | Full mode recovery |
| --- | --- | --- |
| 0.3-0.5 | 0.00 | 0.00 |
| 0.5-1 | 0.04 | 0.00 |
| 1-2 | 0.23 | 0.16 |
| 2-4 | 0.63 | 0.58 |
| 4-8 | 0.86 | 0.82 |
| 8-12 | 0.88 | 0.81 |

These values are for all periods from 0.2 to 15 d. The recovery for P = 5 to 15 d is lower (0.52 to 0.56 for 4 to 12 Earth radii), because the rule needs three transits in one sector.

### Occurrence limits (Figure 4)

| Radius (Earth radii) | P (d) | Completeness | N_eff | 95 % upper limit (planets per star) |
| --- | --- | --- | --- | --- |
| 4-12 | 0.2-5 | 0.99 | 96.5 | 0.031 |
| 4-12 | 0.2-1 | 1.00 | 144.1 | 0.021 |
| 2-12 | 0.2-1 | 0.93 | 137.4 | 0.022 |
| 2-4 | 0.2-1 | 0.83 | 126.9 | 0.024 |
| 1-2 | 0.2-0.5 | 0.45 | 74.1 | 0.041 |
| 4-12 | 5-15 | 0.54 | 11.9 | 0.25 |

Limits for smaller boxes are in `files/results/completeness_occurrence.csv`.

## Limitations

1. The search uses each sector separately. Stacking of sectors would find smaller planets.
2. The rule needs three transits in one sector. Thus the sensitivity is low for P above about 9 d, and single or double transits are not reported.
3. We did not search stars fainter than TESS magnitude 15 (1,732 stars with 2-min data) or the 5th and later sectors of a star.
4. The host mass (0.47 Msun) is fixed. The host radius comes from log g, or is 0.2 Rsun if log g is missing. Hot subdwarfs with a larger radius have longer transits; the widest box (1.5 times the expected duration) can then be too short.
5. PDCSAP flux corrects for light from other stars with a model. Errors in this correction change the depths. In crowded fields (for example the Galactic bulge) the normalization can fail.
6. The fast injection mode does not model a stronger false peak at another period and does not model new sinusoids from a deep transit. We correct its completeness with the full-mode ratio (0.951, from 83 and 150 injections). The statistical uncertainty of this ratio is about 0.07.
7. The injection model has no limb darkening and only circular orbits.
8. The limits assume that the planets are in the searched (P, radius) box with a log-uniform distribution, and that the sample is representative. Many stars in the sample are binaries. A planet in a close binary can have a different occurrence.
9. Classification of the TCEs used figures and literature that we could reach. We did not get new spectra or radial velocities. Some eclipses that we describe may already be published.
10. The swap test estimates noise false alarms. It does not estimate astrophysical false positives. We examined every TCE to address these.

## Reproduction

1. Make a Python 3.12 environment with `files/code/requirements.txt`.
2. Make the directory layout `<root>/.venv` and `<root>/work/src`, and copy `files/code/*` to `work/src/`.
3. Run `work/src/run_all.sh`. This script downloads the catalog, the MAST lists and the light curves, and runs all steps in order. Computation time: about 3 CPU-hours for the search and 1 CPU-hour for the injections on one core per process. Set `OMP_NUM_THREADS=1`.
4. Check the downloaded light curves against `files/results/lc_files_used_sha256.csv`. MAST can reprocess light curves; a changed file has a different hash.

To inspect the results without new computation, use:

- `files/results/summary.json`: main numbers.
- `files/results/sectors.csv`: one row per sector search (dip and bump results, both variants).
- `files/raw_search_output/search_*.jsonl`: raw search output, with the removed sinusoid frequencies.
- `files/results/tces.csv`, `tce_vetting.csv`, `tce_classification.csv`, `tce_simbad.csv`: TCEs, metrics and classes.
- `files/results/injections_fast.csv`, `injections_full.csv`, `files/raw_search_output/inject_*.jsonl`: injections.
- `files/results/completeness_occurrence.csv`, `headline_limits.csv`: completeness and limits.
- `files/results/threshold_scan.csv`, `swap_false_alarms.csv`: threshold test.
- `files/figures/`: Figures 1 to 7 and one diagnostic figure per TCE star.

## Figures

- Figure 1 (`fig1_snr_swap_test.png`): dip S/N against bump S/N for all sector searches, and the number of events against the threshold.
- Figure 2 (`fig2_sample_noise.png`): magnitude distribution and noise per 30 min.
- Figure 3 (`fig3_completeness.png`): recovery of injected transits.
- Figure 4 (`fig4_occurrence_limits.png`): 95 % upper limits on planets per star.
- Figure 5 (`fig5_tce_fold_grid.png`): phase-folded light curves of the 43 TCE stars.
- Figure 6 (`fig6_narrow_dip_stars.png`): per-sector folds at phase 0 and 0.5 for eight stars with narrow dips.
- Figure 7 (`fig7_composite_long_dips.png`): per-sector folds for GALEX J203850.2-265747 and GALEX J17368+2806.

## References

- Barlow B. N. et al. 2019, RNAAS 3, 81: A hot subdwarf B star eclipsed by a low-mass white dwarf in TESS.
- Culpan R. et al. 2022, A&A 662, A40: Hot subdwarf stars studied with Gaia (VizieR J/A+A/662/A40).
- Krzesinski J. et al. 2022, MNRAS 516, 1509: A search for hot subdwarf binaries in data from TESS.
- Kupfer T. et al. 2015, MNRAS 450, 3514: New binaries among UV-selected hot subdwarf stars.
- Pont F., Zucker S., Queloz D. 2006, MNRAS 373, 231: The effect of red noise on planetary transit detection.
- Schaffenroth V. et al. 2022, A&A 666, A182: Hot subdwarfs in close binaries observed from space I.
- Thuillier A. et al. 2022, A&A 664, A113: A search for transiting planets around hot subdwarfs II (TESS Cycle 1).
- Van Grootel V. et al. 2021, A&A 650, A205: A search for transiting planets around hot subdwarfs I.
