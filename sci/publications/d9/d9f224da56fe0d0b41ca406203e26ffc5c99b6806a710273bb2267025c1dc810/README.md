# TESS data to sector 107 show repeat transits for six single-transit TOIs and limit the periods of 58 others

**Job:** sci-1107-hp-astronomy-a6d973259fa3 · **Topic:** astronomy · **Machine:** hp · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026 · **Date:** 2026-11-09

The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

The TESS Object of Interest (TOI) catalog lists 109 candidates that have only one transit. Their catalog period is 0. Many of these TOIs were found in 2018–2023. TESS then observed many of the same stars again, in sectors to 107 (2026). We asked two questions:

1. Do the later TESS data (or earlier data that the TOI search did not use) contain a second transit of the same depth and duration?
2. If not, which orbital periods do the existing non-detections remove?

A second transit changes an unknown period into a finite list of aliases. This makes follow-up with radial velocities or ground photometry practical.

## 2. Main results

- **Data:** We used 2,982 public light-curve files (SPOC 2-min, TESS-SPOC FFI and QLP FFI) for the 108 host stars, sectors 1–107. The search used one light curve for each sector: 1,099 sector light curves in total.
- **Validation:** 22 of the TOIs now have published periods. All 22 published periods are inside our allowed period sets.
  - We recovered second transits at the published epochs for TOI-561 e, HD 152843 c, TOI-2447 b and NGTS-30 b.
  - The published 60.33-d period of the brown dwarf TOI-2490 b (Henderson et al. 2024) is one of the 9 aliases that we derive.
  - The first version of our exclusion rule failed for K2-26 b; section 4.3 describes why.
- **Repeat transits in six TOIs with no published period** (Figure 1, Table 1). Each new event was checked in two independent photometry pipelines, or was already reported by Planet Hunters TESS (PHT).
  - **TOI-3500.02:** two new transits in sectors 90 (2025) and 101 (2026), identical to the sector 64 event. The period is 350.313/n d. Nine aliases remain: 350.31, 175.16, 116.77, 87.58, 70.06, 58.39, 50.04, 35.03 and 18.44 d.
  - **TOI-790.03:** a second 17.4-h transit in sector 96 (2025). Only two periods remain: 363.43 d and 726.86 d. A circular orbit with impact parameter 0 gives 370 d from the duration and the stellar density, so the 363-d alias is favoured. The star also has two other TOIs (41.0 d and 199.6 d).
  - **TOI-6663.01:** a new transit in sector 74. Together with the sector 47 event and a sector 20 event that PHT reported, the period is 739.82/n d, with 14 aliases. PHT noted that the flat bottom can also indicate an eclipsing-binary secondary.
  - **TOI-2534.01:** a new transit in sector 103 (2026), 2,827.80 d after the sector 1 event. 27 aliases remain; 17 of them are in the circular-orbit range of 64–236 d.
  - **TOI-6667.01:** an earlier transit in the sector 1 FFI data (2018), 755.06 d before the catalog event. Five aliases remain: 755.06, 377.53, 251.69, 151.01 and 75.51 d. Only 75.51 d and 151.01 d are near the circular-orbit range (24–134 d).
  - **TOI-6890.01:** the catalog epoch (BTJD 2256.5) is 0.15 d after the first cadence of sector 35, and we classify it as a probable ramp artefact. The repeating signal is a different 1.2–1.7 ppt, 8.8-h dip at BTJD 1524.57 (S8), 2259.14 (S35), 2993.84 (S62) and 3728.61 (S89, QLP only), with separations 734.57, 734.70 and 734.78 d (P = 734.68/n d). The dips are shallow; we cannot exclude a systematic error, but they do not occur at a fixed time after sector start.
- **Period limits:** 58 TOIs have a catalog event that we measure at SNR ≥ 8 and a valid reference depth, and are not catalogued as false positives. For these, the TESS non-detections remove all periods shorter than a median of 30.5 d (interquartile range 17.7–44.7 d). The median allowed fraction of log-period is 0 at 3–30 d, 0.17 at 30–100 d, 0.64 at 100–300 d and 0.88 at 300–1,000 d (Figure 3).
- **Null result for automatic detection:** dip events and brightening events of SNR ≥ 7 occur at similar rates. Thus SNR alone cannot identify a real second transit. Most of the 71 vetted dip events failed the independent-pipeline, depth, duration or background tests (Table 2).

**Table 1. Systems with two or more accepted transit events (BTJD = BJD_TDB − 2457000).**

| TOI | TIC | Tmag | Events (BTJD) | Depth (ppt) | Dur. (h) | Allowed periods (d) | Circular range b = 0–0.9 (d) |
|---|---|---|---|---|---|---|---|
| 3500.02 | 443666343 | 10.8 | 3056.710, 3757.340, 4107.647 | 6.9–7.6 | 7.9 | 9 (18.44–350.31) | 46–263 |
| 790.03 | 308994098 | 9.0 | 3203.661, 3930.521 | 2.3–2.4 | 17.4 | 363.43, 726.86 | 370–2,745 |
| 6663.01 | 415732733 | 10.6 | 1858.839, 2598.660, 3338.478 | 3.5–4.9 | 7.1 | 14 (35.23–739.82) | no stellar mass |
| 2534.01 | 219332978 | 10.8 | 1346.568, 4174.366 | 4.3–4.6 | 8.5 | 27 (64.27–2,827.80) | 24–159 |
| 6667.01 | 161169240 | 12.1 | 1328.263, 2083.318 | 8.4–8.7 | 6.7 | 75.51, 151.01, 251.69, 377.53, 755.06 | 24–134 |
| 6890.01 | 5364106 | 11.1 | 1524.566, 2259.136, 2993.839, 3728.614 | 1.2–1.7 | 8.8 | 734.68/n, n ≤ 244 (not limited) | 55–451 |

The complete alias lists are in `files/results/alias_systems.json` and `files/results/joint_aliases.csv`.

## 3. Method

### 3.1 Sample and data

- **TOI catalog:** the ExoFOP-TESS TOI table, downloaded 2026-11-09 (SHA-256 `6dadbbfc3e67105ac7bd7f10fad346554447ff5865dd0a80a7f78fcbb336ee48`, 8,175 rows). We selected all 109 rows with `Period (days) == 0`; they are on 108 stars. `files/data/exofop_toi_extract_20261109.csv` keeps the fields we used, for these rows and for the other TOIs on the same stars.
- **Light curves:** we queried MAST CAOM for each TIC and downloaded every SPOC 2-min `*_lc.fits`, TESS-SPOC `*_lc.fits` and QLP `*_llc.fits` file: 2,982 files, 2.91 GB. `files/data/lightcurve_manifest.csv.gz` gives the MAST URI, size and SHA-256 of each file.
- **One light curve per sector:** we used SPOC 2-min first, then TESS-SPOC, then QLP.
  - SPOC and TESS-SPOC: PDCSAP flux with QUALITY = 0.
  - QLP: SAP flux with QUALITY = 0. We did our own baseline fit, so that every source has the same treatment.
  - Data with a cadence shorter than 10 min were binned to 10 min.
- **Other planets on the same star:** we masked the transits of other TOIs on the star that have a period (± one duration). We never masked the single event itself.

### 3.2 Box search

For each TOI we used the catalog duration D and moved a box of width D across all data in steps of D/8.

- **Depth:** a straight line was fitted to sidebands of width max(D, 0.2 d) on both sides of the box. The depth is the line value minus the mean in-box flux. This local fit does not lose transit depth. A running-median filter of width 3D removed about 2/3 of the depth of the TOI-561 e event, so we did not use it.
- **Empirical SNR:** depth / (σ / √coverage). σ is the robust scatter (1.4826 × MAD) of all box depths in that sector, so the SNR includes red noise.
- **Known event:** the highest SNR within ±D/2 of the catalog epoch.
- **Candidate events:** local SNR maxima ≥ 7, more than D from the catalog epoch.
- **Inverted search:** we did the same search on inverted flux to estimate the false-alarm rate.

### 3.3 Period exclusion

A time is *excluded* when all of these conditions are true:

- The box coverage is ≥ 0.5.
- A dip of the conservative depth would have SNR ≥ 7 at that time.
- The measured depth is less than half of the conservative depth.

The conservative depth is the known-event depth × (1 − 2/SNR). We apply no exclusion when the known-event SNR is below 8.

A trial period P (3–3,000 d, log grid fine enough for a D/8 timing tolerance across the full time span) is removed if any epoch T0 + nP (n ≠ 0) falls on an excluded time. `files/results/allowed_period_intervals.csv.gz` lists the allowed intervals for each TOI.

### 3.4 Vetting of candidate events

We vetted all 71 "clean" events of SNR ≥ 7 on TOIs that are not catalogued as false positives or false alarms. A clean event is not at a segment edge, has 1/3–3 times the known depth, and has no brightening event of similar SNR within 1.5 d. In every pipeline that covers the event time, we measured:

- the box depth and SNR;
- the best duration in the range 0.4–2.5 D;
- the flux-weighted centroid change;
- the background change.

An event is **confirmed** when all four tests pass:

1. **Independent pipeline:** SNR ≥ 5 in an independent pipeline (QLP against the SPOC family).
2. **Depth:** 0.5–2 times the TOI-event depth in the same pipeline.
3. **Duration:** best duration 0.55–1.75 D.
4. **Background:** the background does not rise during the event (background change ≤ 8σ). A rising background can make a false dip after background subtraction.

An event is **single-pipeline** when no second pipeline covers it and tests 2–4 pass. We then did these checks by eye and with code:

- We looked at every confirmed event in plots.
- We tested whether events fall at the same time after sector start (`files/results/event_sector_phase.csv`).
- We removed events that belong to another TOI on the same star.

For systems with two or more accepted events, we fitted linear ephemerides with integer cycle numbers. A trial period was kept when the maximum O−C is less than D/4 (D/3 for the shallow TOI-6890.01 dips) and no predicted epoch falls on an excluded time. The exclusion uses the smallest event depth, reduced by 2σ.

The circular-orbit range uses T14 = (1 + k) R* (4 / (π G M*))^(1/3) P^(1/3) √(1 − b²/(1 + k)²). It uses the TOI-catalog stellar mass and radius, with b = 0 and b = 0.9. Eccentric orbits can be outside this range, so we did not use it to remove aliases.

### 3.5 Literature check

- **NASA Exoplanet Archive:** we queried `pscomppars` for the 108 TICs (2026-11-09; extract in `files/data/`). We matched a TOI to a planet when its epoch is within 3σ + 0.1 d of a predicted transit.
- **Removed coincidental matches:**
  - TOI-125.04: the TOI comment calls it a separate single event.
  - TOI-941.02: the event overlaps a transit of TOI-941 b but is a different signal.
- **Web searches:** we found TOI-2490 b (Henderson et al. 2024). We found no published period for TOI-3500, TOI-790.03, TOI-6663, TOI-2534, TOI-6667 or TOI-6890. The CTOI notes say "period predicted to be around 600 days" for TOI-790.03 and "additional transit in FFI S20" for TOI-6663.01.

## 4. Other findings, rejections and cautions

### 4.1 Rejected or unresolved events

- **TOI-3713.02 (S59) and TOI-790.03 (S63, QLP):** the candidates come with large background rises (+50σ) and are absent in the other pipeline. They are scattered-light artefacts.
- **TOI-2007.01 (S74):** the event is on a ramp at the start of a data segment. QLP shows a 15-ppt ramp. We rejected it by eye, although the automatic tests passed it.
- **TOI-3724.01:** two extra dips (S59 at 2928.28 and S73 at 3294.66) are in SPOC and QLP. They have a duration of 0.55 D and a depth ratio of 0.72–0.76, and their times do not agree with one period through the catalog epoch. They can be a second body or an eclipsing companion. They are unresolved.
- **TOI-6697.01 and TOI-6697.02 (HD 114082):** each one's "candidate" is the event of the other single TOI. The two singles are different events, not one planet.
- **TOI-941.02:** the catalog event overlaps a transit of TOI-941 b. Our depth at the epoch is set by TOI-941 b (7.7 ppt against the reported 1 ppt), and the S5 event is next to a TOI-941 b transit. We do not use this TOI.
- **Weak events:** for TOI-2298.01, TOI-2433.01 and TOI-7399.01, the second-pipeline SNR is only 5–8. We do not claim these events.
- **TOI-2011.03:** an extra 0.23-ppt dip in S12 is not on the ephemeris of HD 136352 d. It is weak.

### 4.2 TOI-6695 b timing

The S8, S34, S61 and S88 transits are separated by 723.89, 724.01 and 724.07 d (9 cycles each, mean period near 80.44 d). The archive value 80.389 d does not connect them within the transit duration. This suggests transit-timing variations or a revised period. Our strict period exclusion is not valid for such systems.

### 4.3 Validation change

With the first rule (raw known depth, no SNR floor), 21 of 22 published periods were allowed. K2-26 b was removed: its catalog event has SNR 6.2, and its measured depth (4.0 ppt) is larger than the depth of its neighbour transits (0.9–1.4 ppt). This is the winner's-curse bias of a selected peak. We changed to the conservative rule in section 3.3 after we saw this failure. The validation is therefore not fully blind.

### 4.4 Centroids

Formal centroid shifts did not separate planets from artefacts. The confirmed planet HD 152843 c shows 9–13σ formal shifts. We report the centroid values but did not use them.

## 5. Limitations

- We did no pixel-level vetting, difference imaging or ground follow-up. A repeat event that agrees in depth and duration does not prove a planet. Eclipsing binaries on the target or on a nearby star can give the same result. TOI-6663.01 and TOI-6667.01 have flat bottoms and large depths.
- The period exclusion assumes a strict period and a box shape. TTVs (see TOI-6695 b), grazing V-shaped transits and depth changes between sectors can remove true periods.
- Masked transits of other planets leave allowed windows at their periods. For example, the minimum allowed period of TOI-941.02 is the 8.51-d period of TOI-941 b.
- 40 TOIs have a known-event SNR below 8 in our measurement, so we give no period limits for them. This includes some confirmed planets (TOI-561 e, Kepler-134 b, Wolf 503 b).
- TESS revisits a field after about one or two years. Thus most event pairs are separated by about 700–750 d, and many aliases remain.
- MAST holdings at download time reached sector 107. Some 2026 sectors were not yet available for all stars.
- The catalog snapshot is from 2026-11-09. The TOI team can have updated periods since then.

## 6. Reproduction

1. Run `files/code/run_all.sh`. It downloads the catalogs and light curves into a separate `scratch/` folder, never into the signed draft, and then runs the search, vetting, classification, aliases and figures. The search takes about 1 h with 5 processes on a loaded 8-core machine.
2. Check the downloaded light curves against `files/data/lightcurve_manifest.csv.gz`.
3. The bundled catalog extracts allow the same TOI selection without the live catalog.

Code files:

- `mast.py`, `query_all.py`, `download.py`: MAST queries and downloads.
- `lcio.py`: light-curve reading and binning.
- `search.py`: box search and period exclusion.
- `recompute.py`: conservative exclusion from the saved scans.
- `match_literature.py`, `summarise.py`: archive matching and summary tables.
- `vet.py`: per-event checks in each pipeline.
- `classify.py`: event classes.
- `sector_phase.py`: sector-phase test.
- `alias_multi.py`: joint aliases.
- `intervals.py`, `figures.py`, `manifest.py`: output tables, figures and the file manifest.

The vetting event list is the set of `clean == True` rows of `files/results/candidate_events.csv` on TOIs not dispositioned FP or FA. The `results/repeat_transit_systems.csv` file is an automatic first pass. It still contains the TOI-941.02 and TOI-6697 cases that section 4.1 resolves; `alias_systems.json` is the final table.

## 7. Files

- `files/figures/fig3_repeat_transits.png`: all events of the six multi-event systems.
- `files/figures/fig4_alias_sets.png`: allowed periods with circular-orbit ranges and published periods.
- `files/figures/fig1_allowed_periods.png`: allowed and excluded periods for the 58 TOIs with valid limits.
- `files/figures/fig2_allowed_fraction_bands.png`: allowed fraction by period band.
- `files/figures/vet_toi*.png`: each event of the six systems in each pipeline.
- `files/results/`: TOI summary, candidate events, vetting, classes, sector phases, literature validation, joint aliases and allowed intervals.
- `files/data/`: catalog extracts and the light-curve manifest.

## 8. Data sources and credits

- **TESS mission data** from MAST (NASA). SPOC 2-min light curves: Jenkins et al. 2016, doi:10.1117/12.2233418.
- **TESS-SPOC FFI HLSP:** Caldwell et al. 2020, doi:10.17909/t9-wpz1-8s54.
- **QLP HLSP:** Huang et al. 2020, doi:10.17909/t9-r086-e880.
- **ExoFOP-TESS** TOI and CTOI tables (NASA/IPAC). TOI catalog: Guerrero et al. 2021, doi:10.3847/1538-4365/abefe1.
- **NASA Exoplanet Archive** `pscomppars` (NASA/IPAC), doi:10.26133/NEA13.
- **Literature periods:** see `files/results/literature_validation.csv`; TOI-2490 b: Henderson et al. 2024, arXiv:2408.04475.

See `files/NOTICE.md` for the terms of the external data.
