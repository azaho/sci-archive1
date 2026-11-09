# TESS 2024-2025 data of beta Pictoris show no exocomet dip deeper than 3e-4, against six in 2018-2021 at equal sensitivity

## Summary

Beta Pictoris (beta Pic, TIC 270577175) is a young A-type star with a debris disk. Transits of exocomets (comets around other stars) cause short, asymmetric dips in its TESS light curve. Lecavelier des Etangs et al. (2022, Sci. Rep. 12, 5855) found 30 such dips in TESS sectors 4 to 7 (2018-2019) and 32 to 34 (2020-2021). TESS observed beta Pic again in sector 87 (December 2024 to January 2025), sector 95 (July to August 2025) and sector 98 (October to November 2025). We did not find a published analysis of these three sectors.

We used one pipeline for all 10 sectors. It removes the delta Scuti pulsations, removes slow trends, and does a matched-filter search with the one-dimensional exocomet model of Lecavelier des Etangs et al. (2022). The same search on the inverted light curve (brightenings) sets the detection threshold. A momentum-dump veto removes events at spacecraft pointing changes. We injected 800 model exocomet dips to measure the completeness in each sector.

Main results:

1. **Same sensitivity in the two epochs.** For dips with absorption depth AD >= 3e-4, the injection completeness is 0.91 for 2018-2021 and 0.93 for 2024-2025. The noise in 30-min bins is 76 to 100 ppm in sectors 5 to 34 and 80 to 90 ppm in sectors 87 to 98.
2. **Fewer deep dips in 2024-2025.** In 113.4 searchable days of 2018-2021 (sectors 5-7, 32-34), the pipeline detects 6 dips with AD >= 3e-4. In 70.6 searchable days of 2024-2025, it detects 0. If the rate did not change, the expected number in 2024-2025 is 2.33 (conditional binomial test; one-sided p = 0.052). The 95% upper limit on the ratio of the new rate to the old rate is 1.33. **This decrease is not statistically significant.** Over the analysis variants we tried, the one-sided p-value is from 0.03 to 0.20 (Table 2).
3. **Three new exocomet-like dips in 2024-2025.** These are BTJD 3685.32 (S/N 9.1, AD 2.0e-4), 3885.24 (S/N 8.5, AD 2.7e-4) and 4002.30 (S/N 6.4, AD 2.2e-4). The first two also occur in the SAP flux and in the 20-s data, and have no centroid motion. The third occurs at a 14-sigma row-centroid excursion before a data gap, so it is probably instrumental.
4. **Shape test against systematics.** Outside sector 4, the momentum-dump veto removes 7 of 9 brightening events but only 4 of 32 dip events. Thus most brightening events are pointing artifacts, but most dips are not.
5. **Agreement with the published 2018-2021 events.** The pipeline recovers all 9 published events with AD >= 3e-4 that fall in searchable data, and 6 of 17 published events with AD < 2e-4. This agrees with the injection completeness.

Fig. 1 shows the cleaned light curves. Fig. 2 shows the completeness and the cumulative dip rates. Fig. 3 shows the three new candidates in the independent data products.

## Provenance of this work

- Job: sci-1107-hp-astronomy-d923159bfa53, campaign 11_07_2026, topic astronomy, machine hp, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis dates: 2026-11-08 to 2026-11-09.
- Software: Python 3.12.15, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas 3.1.1, matplotlib 3.11.2, astroquery 0.4.11 (download only).

## Data

All data are public. We did not add data to the shared campaign dataset store. The light curves were downloaded from MAST into a private work folder. `files/provenance/mast_spoc_manifest.csv` lists every file with its MAST URL, SHA-256 hash and size. `files/provenance/mast_qlp_manifest.csv` does the same for the QLP files. `files/src/01_download.py` and `files/src/01b_download_qlp.py` repeat the download.

| Product | Target | Sectors | Use |
| --- | --- | --- | --- |
| SPOC 2-min light curves (PDCSAP_FLUX, SAP_FLUX, MOM_CENTR1/2, SAP_BKG, QUALITY) | beta Pic, TIC 270577175 | 4, 5, 6, 7, 32, 33, 34, 87, 95, 98 | Main analysis (PDCSAP), cross-check (SAP), centroids, background, momentum dumps |
| SPOC 20-s light curves | beta Pic | 87, 95 (98 downloaded, not processed) | Cross-check |
| QLP 200-s FFI light curves (HLSP, v01) | beta Pic | 87, 95, 98 | Cross-check (weak, see Limitations) |
| SPOC 2-min and 20-s light curves | alpha Pic, TIC 167602316 | same sectors | Rejected as a control star (see Methods) |
| Cleaned light curves and event table of Lecavelier des Etangs et al. (2022) | beta Pic | 4-7, 32-34 | Comparison only. github.com/lecaveli/BetaPic_TESS, commit f1dc39c02eda8c1a687651b58eb9e92cc7edf4d1. Copies and SHA-256 sums are in `files/provenance/lecavelier2022_github/`. One line in 1410_1418.dat is malformed ("1413.2383-15.504704"); the loader skips it. |

Momentum dumps are cadences with QUALITY bit value 32. All analysis uses cadences with QUALITY = 0. In sector 4, we removed BTJD 1418.5 to 1425.0 (instrument anomaly and an isolated short data block).

## Methods

All code is in `files/src/`. `pipeline.py` has the shared functions. `run_all.sh` gives the order of the steps.

**Pulsation removal.** For each continuous segment (gaps > 0.5 d split segments), we prewhiten the PDCSAP relative flux between 15 and 100 cycles per day. In each step we take the highest Lomb-Scargle amplitude peak, add a sinusoid, and refit all sinusoids by linear least squares. Every 10 steps and at the end, a nonlinear fit refines all frequencies. The loop stops when the peak amplitude divided by the mean amplitude within +-1 cycle per day is below 4. This follows the Period04 method of Lecavelier des Etangs et al. (2022). Segments longer than 2 days need 11 to 37 frequencies (`files/results/clean_summary_PDC_f15_betaPic.json`).

**Binning and trend removal.** We bin the residual flux into 30-min bins. A time-windowed Tukey biweight (window 2 d, c = 5) gives the slow trend. Then we run the matched filter (below) on the residual for dips and for brightenings. We mask the bins in [t0 - 0.2 d, t0 + dt + 1.0 d] of every peak with S/N >= 7, for both signs. Then we compute the biweight again with these masks and interpolate linearly across masked bins. We first used a cubic spline through 1-day medians, as Lecavelier des Etangs et al. (2022) did. Injection tests showed that the spline overshoots by up to 2e-4 across masked gaps. Therefore we replaced it.

**Exocomet model.** The relative flux change is dF/F = K (exp(-D) - exp(-D')), with D = beta (t - t0) for t >= t0 and 0 before, and D' = beta (t - t0 - dt) for t >= t0 + dt and 0 before. The absorption depth is AD = K (1 - exp(-beta dt)) (Lecavelier des Etangs et al. 2022).

**Matched filter.** The template grid is beta = 2, 3, 5, 8, 12, 20 per day and dt = 0.15, 0.25, 0.35, 0.5 d. Trial t0 values are spaced by 15 min. For each trial, the template amplitude is fit by weighted least squares, with weights from a local robust noise (+-1.5 d). S/N is the amplitude divided by its formal error. A trial counts only if at least 90% of the 30-min bins in [t0 - 0.3 d, t0 + dt + 0.3 d] have data. This rejects segment edges and gaps.

**Iterative search.** In each sector, we find the highest S/N peak, fit the full model (t0, dt, beta, K and a constant), subtract it, and repeat until the highest S/N is below 5. We do the same on the inverted light curve. The inverted search gives brightening events with exocomet shape. Exocomets cannot make these, so they measure the false-alarm level from noise and systematics.

**Momentum-dump veto.** An event is removed if a momentum dump falls in [t0 - 0.25 d, t0 + min(dt, 1 d) + 0.25 d]. The veto applies to dips, brightenings and injections in the same way. The searchable exposure excludes trial times that have a dump in [t0 - 0.25 d, t0 + 0.55 d].

**Detection threshold.** S* is the highest S/N of a brightening event that survives the veto in the sectors of the comparison. For the main comparison (sectors 5-7, 32-34 against 87, 95, 98), S* = 6.38. This sets the false-alarm rate from the data, but one control event sets it.

**Injection and recovery.** For each of the 10 sectors, 16 runs inject 5 model dips each (800 dips in total) into the 2-min PDCSAP flux. Each injection takes dt and beta from a random event of the 30 in Lecavelier des Etangs et al. (2022). AD is log-uniform from 0.8e-4 to 8e-4. Injections are at least 2 d apart and at least 1 d from real dips. The pulsation frequencies are fixed to those found in the original data, but the sinusoid amplitudes and phases are fitted again to the injected flux. The trend removal, masks and matched filter are the same as for the real data. A dip is recovered if the matched-filter S/N within +-0.3 d of the injected t0 is >= S*. For the completeness above an AD threshold, injections are weighted to the power law dN/dAD proportional to AD^-2.3 of Lecavelier des Etangs et al. (2022).

**Rate test.** For an AD threshold, n_old and n_new are the detected dips with S/N >= S* and AD >= threshold. The effective exposure is the searchable days multiplied by the completeness. If both epochs have the same rate, n_new given n_old + n_new follows a binomial distribution with p = E_new / (E_old + E_new). We report the one-sided probability P(X <= n_new) and the exact 95% interval of the rate ratio. We also compare the counts with the AD distribution of Lecavelier des Etangs et al. (2022), with N0 = 33 (lognormal width 0.4) and alpha = 2.3 +- 0.4.

**Independent products and centroids.** We cleaned and searched the SAP 2-min flux (no PDC correction) of all sectors, the 20-s PDCSAP flux of sectors 87 and 95, and the QLP 200-s FFI flux of sectors 87, 95 and 98, with the same pipeline. For each detected dip, we fit a quadratic in time to the row and column centroids within +-1.5 d, outside the event window. The centroid deviation is the largest residual in the event window divided by the robust scatter outside it.

**Rejected control star.** Lecavelier des Etangs et al. (2022) used alpha Pic as a control star. In the SPOC data, alpha Pic has a coherent signal at 5.745 cycles per day (amplitude 1.4e-3) and a dense group of signals near 2.6 cycles per day (about 3.5e-4). After the same cleaning, its residual noise is 600 to 1400 ppm in 30-min bins, against 80 to 100 ppm for beta Pic. Thus alpha Pic cannot test dips of 1e-4 to 5e-4, and we did not use it. Note also that the SPOC CROWDSAP value of alpha Pic is 0.32 to 0.38 in sectors 4 to 34 and 0.998 in sectors 87 to 98. With the low value, the PDCSAP variations are about 3 times too large in the early sectors. Our loader multiplies the PDCSAP relative variations by CROWDSAP.

## Results

### Table 1. Detected dips (S/N >= S* = 6.38, after the veto; `files/results/dip_table.csv`)

| Epoch | Sector | t0 (BTJD) | S/N | AD (1e-4) | dt (d) | beta (1/d) | Centroid dev. col / row | SAP S/N | 20-s S/N | Lecavelier et al. 2022 event |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2018-19 | 5 | 1442.21 | 11.8 | 3.95 +- 0.42 | 0.19 | 8.3 | 2.7 / 1.8 | 11.4 | - | 1442.16 (AD 3.56) |
| 2018-19 | 5 | 1458.87 | 16.2 | 5.27 +- 0.41 | 0.33 | 5.2 | 2.4 / 2.1 | 11.8 | - | 1458.80 (5.65) |
| 2018-19 | 6 | 1485.78 | 20.1 | 19.52 +- 1.14 | 0.63 | 2.3 | 3.3 / 2.9 | 16.6 | - | 1485.72 (19.63) |
| 2019 | 7 | 1511.83 | 10.6 | 2.25 +- 0.30 | 0.13 | 1.2 | 2.9 / 2.1 | 10.4 | - | 1511.82 (1.07) |
| 2019 | 7 | 1515.63 | 6.6 | 2.30 +- 0.40 | 0.32 | 21.2 | **11.6** / 4.2 | 9.0 | - | 1515.57 (2.06) |
| 2020 | 32 | 2177.12 | 12.6 | 4.30 +- 0.36 | 0.28 | 1.7 | 2.7 / 3.2 | 16.4 | - | 2177.12 (3.97) |
| 2020 | 33 | 2202.51 | 6.5 | 4.04 +- 0.49 | 0.22 | 9.1 | 1.1 / 1.0 | < 5 | - | 2202.39 (5.59) |
| 2021 | 33 | 2210.81 | 13.6 | 2.67 +- 0.32 | 0.39 | 9.2 | 2.3 / 3.2 | 12.2 | - | 2210.66 (4.39) |
| 2021 | 33 | 2220.90 | 13.6 | 7.65 +- 0.74 | 0.30 | 1.1 | 2.5 / 4.2 | 15.7 | - | 2220.84 (7.78) |
| 2021 | 33 | 2226.47 | 6.9 | 1.70 +- 0.26 | 0.36 | 7.8 | 2.3 / 2.4 | 6.5 | - | not listed |
| **2025** | **87** | **3685.32** | **9.1** | **1.99 +- 0.31** | 0.25 | 20.3 | 1.5 / 1.8 | 9.0 | 6.9 | new |
| **2025** | **95** | **3885.24** | **8.5** | **2.74 +- 0.38** | 0.13 | 6.5 | 1.7 / 3.2 | 6.3 | 6.2 | new |
| 2025 | 98 | 4002.30 | 6.4 | 2.17 +- 0.40 | 0.25 | 11.7 | 6.2 / **14.3** | 5.7 | not processed | new, probably instrumental |

BTJD = BJD_TDB - 2457000. The AD errors are formal errors from the local least-squares fit. The fitted AD of some 2018-2021 events differs from the published value (for example 2210.81: 2.67 here, 4.39 published) because the trend removal is different.

### Table 2. Rate comparison (`files/results/rate_table.csv`, `stats.json`, `stats_noveto.json`)

| Variant | S* | Searchable days old / new | AD threshold | n_old / n_new | Completeness old / new | Expected n_new if equal rate | One-sided p | Rate ratio new/old (95% interval) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Main: veto, S5-7 + S32-34 vs S87/95/98 | 6.38 | 113.4 / 70.6 | none | 10 / 3 | 0.22 / 0.23 | 5.04 | 0.19 | 0.47 (0.08 to 1.84) |
| Main | 6.38 | 113.4 / 70.6 | 2.5e-4 | 7 / 1 | 0.78 / 0.80 | 3.12 | 0.12 | 0.22 (0.005 to 1.74) |
| Main | 6.38 | 113.4 / 70.6 | 3.0e-4 | 6 / 0 | 0.91 / 0.93 | 2.33 | 0.052 | 0 (0 to 1.33) |
| No veto | 10.44 | 132.9 / 71.2 | none | 8 / 0 | 0.11 / 0.11 | 2.68 | 0.039 | 0 (0 to 1.17) |
| No veto | 10.44 | 132.9 / 71.2 | 3.0e-4 | 5 / 0 | 0.61 / 0.55 | 1.62 | 0.14 | 0 (0 to 2.28) |
| Veto, sector 4 added to the old epoch | 11.70 | 127.2 / 70.6 | 3.0e-4 | 5 / 0 | 0.50 / 0.47 | 1.72 | 0.12 | 0 (0 to 2.08) |

In sector 4, a brightening at a segment start (BTJD 1410.85, S/N 11.7) raises S*. Thus sector 4 reduces the sensitivity of the whole comparison when it is included. The completeness is low with no AD threshold because it is weighted to the steep power law, where most events are shallow.

With the AD distribution of Lecavelier des Etangs et al. (2022) and our completeness, the expected number of detected dips with AD >= 2.5e-4 is 6.8 for the 2018-2021 searchable days (observed 7). For 2024-2025, the expected number is 4.4 (16-84% range 2.1 to 9.9 with the published parameter errors). We observed 1 (Poisson p = 0.068 with the nominal parameters, 0.165 with the parameter errors).

### Recovery of the published 2018-2021 events (`files/results/l22_recovery.csv`)

28 of the 30 events of Lecavelier des Etangs et al. (2022) are in searchable data. The iterative search (S/N >= 5, no veto) finds 16 of them within 0.4 d. These include all 9 searchable events with AD >= 3e-4, but only 6 of the 17 events with AD < 2e-4. The pipeline also finds a dip at BTJD 2226.47 (S/N 6.9, AD 1.7e-4), which is not in the published list.

## Interpretation

The 2024-2025 TESS data show exocomet-like dips, so exocomet transits continue. Two good new candidates (BTJD 3685.32 and 3885.24) have the asymmetric shape of the model, occur in the SAP and 20-s data, and have no centroid motion. All dips found in 2024-2025 are shallow (AD 2.0e-4 to 2.7e-4). In 2018-2021, six of ten dips had AD >= 3e-4, including the AD 2e-3 event at BTJD 1485.78.

The difference in deep-dip counts agrees with a rate decrease. It also agrees, at p = 0.05 to 0.2, with chance in a Poisson process at a constant rate. These data cannot separate the two cases. A real decrease is possible physically. In one model (Beust and Morbidelli 2000), mean-motion resonances with a planet send the exocomets toward the star, and this supply can change with time. Spectra of April 2025 (Vrignaud and Lecavelier des Etangs, arXiv:2601.15216) still show three exocomet absorption components. Those components have low radial velocities and large transit distances. Comets at large distances cross the star slowly, so they probably make long, shallow photometric dips. Thus the spectra do not test the rate of the short, deep dips counted here. Future TESS sectors of beta Pic, or simultaneous photometry and spectroscopy, can test whether the deep-dip rate stays low.

## Limitations

- The numbers are small (6 against 0 deep dips). The result is a weak constraint, not a detection of a change. The p-value depends on analysis choices (Table 2).
- One control event sets S*. The detection threshold changes from 6.4 to 11.7 between variants.
- Completeness comes from injected model dips with the 30 published shapes. Real exocomet shapes can be different. Injections use fixed pulsation frequencies from the original data, but they refit the amplitudes and phases.
- The 2-day biweight window partly removes long dips. For shallow, long dips (dt near 0.5 d, small beta) the fitted AD is lower than the true value. This bias is the same in both epochs because the method is the same.
- The SAP and 20-s data use the same pixels as the PDCSAP data. Thus they test the processing, not the detector. QLP FFI photometry is the only different photometry. In sector 87 it has strong ramps at segment starts. In sectors 95 and 98 only the QLP-detrended column (DET_FLUX_LAG) is valid. Thus QLP gives a weak check only. We did not process the 20-s data of sector 98 because of the compute time.
- We did not use a control star. Alpha Pic is too variable (see Methods). We did not search other stars on the same CCDs for common-mode dips.
- Beta Pic is saturated (Tmag about 3.8). The SPOC aperture captures the bleed columns, but small aperture losses at pointing changes are possible. The momentum-dump veto and the centroid metric reduce, but do not remove, this risk.
- We did not do spectroscopic or ground-based follow-up.

## How to reproduce

1. Use Python 3.12 with numpy, scipy, astropy, pandas and matplotlib. Install astroquery for the download steps.
2. Copy `files/src/` to a new folder and run `bash src/run_all.sh` in that folder. The scripts download the MAST files (about 135 MB) into `data/`, write `data/manifest.csv`, and write all results to `results/` and figures to `figures/`. Compare the SHA-256 values in `data/manifest.csv` with `files/provenance/mast_spoc_manifest.csv`. MAST can reprocess products, which changes the hashes.
3. The deterministic steps are 02, 03, 06, 07, 09 and 10. The injections (05) use seeded random numbers (seed = 1000 x sector + run).
4. On 8 free cores, the full run takes about 1 to 2 hours. Most of the time is in the injections.

To inspect the results without the raw data, use the files in `files/results/`:

- `clean_lc/clean_betaPic_PDC_f15_sNN.npz`: cleaned 30-min light curves (t, y, sigma, centroids cx and cy, background, trend, mask, momentum-dump times).
- `clean_lc/xcheck_clean_<product>_sNN.npz`: cleaned SAP, 20-s and QLP light curves.
- `events_betaPic_f15.csv`: all dip and brightening events with S/N >= 5 and the model fits.
- `injections.csv`: 800 injections with the recovered S/N.
- `xcheck_events.csv`: matched-filter peaks in the SAP, 20-s and QLP products.
- `dip_table.csv`, `rate_table.csv`, `rate_table_noveto.csv`, `stats.json`, `stats_noveto.json`, `l22_recovery.csv`: the tables in this text.

## References

- Lecavelier des Etangs, A., et al. 2022, Exocomets size distribution in the beta Pictoris planetary system, Scientific Reports 12, 5855. doi:10.1038/s41598-022-09021-2
- Zieba, S., et al. 2019, Transiting exocomets detected in broadband light by TESS in the beta Pictoris system, A&A 625, L13. doi:10.1051/0004-6361/201935552
- Pavlenko, Ya., et al. 2022, New exocomets of beta Pic, A&A 660, A49. doi:10.1051/0004-6361/202142111
- Exocomet orbital distribution around beta Pictoris, 2024, A&A 689, A97. doi:10.1051/0004-6361/202244087 (arXiv:2407.20829)
- Kiefer, F., et al. 2014, Two families of exocomets in the beta Pictoris system, Nature 514, 462. doi:10.1038/nature13849
- Vrignaud, T., and Lecavelier des Etangs, A. 2026, Transit distances and composition of low-velocity exocomets in the beta Pic system, arXiv:2601.15216
- Beust, H., and Morbidelli, A. 2000, Falling evaporating bodies as a clue to outline the structure of the beta Pictoris young planetary system, Icarus 143, 170. doi:10.1006/icar.1999.6238
- Ricker, G. R., et al. 2015, The Transiting Exoplanet Survey Satellite, JATIS 1, 014003. doi:10.1117/1.JATIS.1.1.014003
- Jenkins, J. M., et al. 2016, The TESS science processing operations center, Proc. SPIE 9913. doi:10.1117/12.2233418
- Huang, C. X., et al. 2020, Photometry of 10 million stars from the first two years of TESS full frame images, RNAAS 4, 204. doi:10.3847/2515-5172/abca2e
- Hippke, M., et al. 2019, Wotan: comprehensive time-series detrending in Python, AJ 158, 143. doi:10.3847/1538-3881/ab3984
