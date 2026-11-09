# TESS 2-min light curves (2019-2026) show transit-duration trends in 6 of 120 planets around hot stars and in 1 of 271 planets around cooler stars; WASP-167 b is a new nodal-precession candidate

## Summary

A planet that orbits a fast-rotating, oblate star on a tilted orbit has an orbit plane that turns slowly (nodal precession). The transit chord then moves across the stellar disk. The impact parameter b changes, and the transit duration T14 changes with it. Before this work, five planets had a published detection: Kepler-13A b (KOI-13 b), WASP-33 b, KELT-9 b, TOI-1518 b and TOI-1355 b. All five orbit hot, fast-rotating stars.

We did a uniform search for secular T14 changes in TESS SPOC 2-min light curves. The data come from sectors 1 to 107 (2018 to 2026). The sample has 419 confirmed short-period planets (P < 10 d) with deep transits (estimated depth >= 0.3 %), host TESS magnitude <= 12.5, and 2-min data in at least two observing seasons that span at least 1.5 yr. For each planet and season, we fit a batman transit model with a shared a/R* and limb darkening. Rp/R*, b and a time offset were free in each season. A linear baseline was fit for each transit. Errors come from a bootstrap over transits. The error scale was calibrated on the cool hosts (Teff <= 5700 K). These stars rotate slowly, so we expect no measurable precession for them.

Main results:

1. **Hot hosts (Teff >= 6250 K) show an excess of duration trends.** With calibrated errors, 6 of 120 hot-host planets have |z| > 3. Only 1 of 271 cooler-host planets (134 cool, 137 intermediate) passes this limit. One-sided Fisher exact p = 0.004. The single cool flag (TOI-1811 b, z = -3.2, two seasons) agrees with the about 1 false flag that we expect by chance in 391 tests.
2. **The method recovers published precession.** Four of the five planets with published precession have |z| >= 3.1. The fifth, WASP-33 b, has z = -3.0. For TOI-1518 b, the published rate (db/dt = -0.0116 +- 0.0036 /yr, from 2019 and 2022 data) predicts the 2024 T14 out of sample: chi2 = 0.1 for 1 dof, against 70.7 for no change. We measure db/dt = -0.0119 +- 0.0009 /yr. For TOI-1355 b we get +0.0163 +- 0.0016 /yr. The discovery paper gives +0.0163 +- 0.0008 /yr from the same 2-min sectors, so this check is not independent. For KELT-9 b, the Doppler-tomography rate of Stephan et al. (2022) predicts a 2019-2024 T14 decrease that agrees with our data (chi2 = 4.4 for 3 dof, against 108.7 for no change).
3. **WASP-167 b (KELT-13 b) is a new precession candidate.** T14 increases monotonically from 176.7 min (2019) to 179.5 (2021), 180.9 (2023) and 181.9 min (2026). The slope is +0.70 +- 0.10 min/yr (calibrated z = 6.7, four seasons, 53 transits). This gives db/dt = -0.0033 +- 0.0005 /yr, so the chord moves toward the stellar centre. The trend stays when we remove the pulsation prewhitening (z = 7.3) and when we use a quadratic baseline (z = 8.9). SAP flux gives the same sign at low precision. The host is a rapidly rotating F1V delta-Scuti/gamma-Dor star with a retrograde orbit (lambda = -165 +- 5 deg, Temple et al. 2017), which is the configuration that drives nodal precession. We found no earlier report of precession for this planet.
4. **HAT-P-70 b is a weaker candidate.** T14 changes by +0.90 +- 0.27 min/yr between 2020 and 2025 (z = 3.4, two seasons only; 2.8 to 3.6 across variants). The host is an A star with v sin i of about 99 km/s and a nearly polar orbit (lambda of about 108-113 deg). One more TESS season is necessary to confirm or reject this trend.
5. **Limits for the other hot-host planets.** For 88 hot-host planets with b > 0.3 and no known precession, the median 3-sigma limit on |db/dt| is 0.0057 /yr (interquartile range 0.0026-0.0105 /yr). Per-planet values are in `files/data/derived/hot_host_trends_limits.csv`.

Main limitations: The planet-level evidence comes from one instrument (TESS). We did not find a usable independent pre-TESS T14 anchor for WASP-167 b. The tabulated discovery duration (163.4 min) does not agree with the duration from the discovery a/R*, Rp/R* and b (173 min), so we did not use it. The model does not include gravity darkening, stellar oblateness or eccentricity. Thus our absolute b values for fast rotators (for example KELT-9 b: 0.40 against 0.19-0.20 from Doppler tomography) are biased. The duration trend is more robust than b itself, but the db/dt values that we derive from it use this biased geometry. The population excess (point 1) comes mostly from the five planets with known precession. If we remove them, 2 of 115 hot-host planets are flagged against 1 of 271 others (p = 0.21).

## Questions and approach

Question: In a uniform TESS 2-min sample, do secular transit-duration changes occur preferentially around hot (fast-rotating) stars, as J2-driven nodal precession predicts? Does the TESS record from 2019 to 2026 show new precessing planets beyond the five that are known?

Pre-set tests:
- **Population test:** compare the fraction of |z_cal| > 3 T14 trends for hot hosts (Teff >= 6250 K, above the Kraft break) with the fraction for cooler hosts.
- **Positive controls:** use the five published precessors. TOI-1518 b is a real out-of-sample test, because the published rate used 2019 and 2022 data, and we compare it with 2024 data.
- **Null calibration:** cool hosts (Teff <= 5700 K) set the error scale.
- **Robustness:** for every flagged or control planet, we repeated the fit with no prewhitening, with a quadratic baseline and with SAP flux. We also made fits for each block of contiguous sectors.

## Data

| Input | Source | Version / identifier | Use |
| --- | --- | --- | --- |
| Planet parameters | NASA Exoplanet Archive `pscomppars` (transiting), snapshot of 2026-11-08 as stored in campaign publication sci:sha256:f0ef9edd19928a25a0cae794dccde12416fe7c02c90b3f82d2460251d2cb1c11 (`files/catalogs/pscomp_transiting.csv`) | sha256 5466bbf0aaac168c98e126b9a2be28fa23184dc5fcd1b2b0d1d4aa0ea92eb538; copy in `files/data/inputs/pscomp_transiting_f0ef.csv` | Sample, initial ephemeris, start values. The NASA Exoplanet Archive and ExoFOP returned HTTP 522 on 2026-11-09, so we reused this verified snapshot. |
| TESS light curves | MAST, SPOC 2-min `*_lc.fits`, PDCSAP_FLUX (SAP_FLUX in one variant), QUALITY = 0 | Sectors 1-107; 2,620 files for 419 stars, downloaded 2026-11-09. File list in `files/data/inputs/lc_files.csv`; SHA-256 of every file in `files/data/inputs/tess_lc_sha256.txt` | All measurements |
| TESS file lists | `https://archive.stsci.edu/missions/tess/download_scripts/sector/tesscurl_sector_N_lc.sh`, N = 1-107 | Downloaded 2026-11-09 (index sha256 79a4ce20...62ad) | File discovery |
| Literature duration (check only) | Campaign shared dataset `datasets/nea-transit-duration-608d8363-20261108/transits.csv` (NASA Exoplanet Archive pscomppars) | sha256 0ec5aaed0cd70150ec732214b0f9423ed88fcf656ede95b2960ea11924597b5f | Pre-TESS T14 check for WASP-167 b and HAT-P-70 b (not used, see Limitations) |
| Published precession rates | Stephan et al. 2022 (ApJ 931, 111) Tables 1 and 3; Watanabe et al. 2024 (PASJ 76, 374); Szabo et al. 2020 (MNRAS 492, L17); TOI-1355 b discovery paper (arXiv:2608.17387) | Values copied by hand into `files/code/controls.py` | Positive controls |

The raw TESS light curves (4.9 GB) are not in this bundle. Use `files/code/download_lc.sh` to get them again, and use `tess_lc_sha256.txt` to verify them.

## Method

Code: `files/code/`. Run the steps from a work directory that contains `raw/`, `out/` and `lc/`, with batman-package 2.5.3 on Python 3.12 (numpy 2.5, scipy, astropy, pandas).

1. `select_sample.py`: Selects transiting planets with P < 10 d, (Rp/R*)^2 >= 0.003 (from pl_radj and st_rad), Tmag <= 12.5, and 2-min data in >= 2 seasons (season gap > 200 d) over >= 547 d. Result: 419 planets (121 hot >= 6250 K, 144 intermediate, 154 cool <= 5700 K).
2. `download_lc.sh` (+ `download_lc_rev.sh`, which downloads the same list in reverse order): MAST downloads.
3. `fit_shapes.py <variant> <nproc>`: For each planet:
   - Load PDCSAP flux with QUALITY = 0 and normalize each sector.
   - Mask the transits of other known planets in the system.
   - Align each season with a box search of the mid-time offset at the catalog period, because some catalog epochs are old. Then refit a linear ephemeris.
   - Prewhiten sinusoids at 4-60 c/d. The sinusoids are fit to out-of-transit data for each sector (up to 25 frequencies, amplitude S/N >= 5). This step removes delta-Scuti pulsations.
   - Cut a window of half-width max(1.25 T14, T14/2 + 0.12 d) around each transit. Keep a transit only if >= 60 % of the in-transit cadences and >= 40 % of the out-of-transit cadences on each side are present. A season needs >= 3 such transits.
   - Joint batman fit (quadratic limb darkening with Kipping q1, q2, circular orbit, 2-min cadence): a/R*, q1 and q2 are shared. Rp/R*, b and a time offset are free in each season. The fit profiles out a multiplicative linear baseline for each transit (quadratic in variant `quad`). We used multi-start in b to avoid local minima of the b-a/R* degeneracy.
   - Per-season T14 = (P/pi) asin( sqrt((1+k)^2 - b^2) / sqrt(a^2 - b^2) ).
   - A second fit lets a/R* change in each season (limb darkening fixed). Its result is `slope_freeT14`.
   - Bootstrap: 40 resamplings of the transit windows with replacement in each season, with a refit each time.
   - Variants: `base`, `nopw` (no prewhitening), `quad`, `sap`, and `sector` (SEASON_GAP = 15 d, one fit for each block of contiguous sectors).
4. `analyze.py <variant>`: Weighted linear trend of T14 against time for each planet. The slope error is the larger of the formal WLS error and the bootstrap-slope spread, with a small-sample correction sqrt(n/(n-1)).
   - Quality cut: Rp/R* spread between seasons <= 20 % and T14 >= 20 min. This cut removed 8 fits, mostly young spotted stars and grazing systems: HIP 67522 b, Kepler-447 b, Kepler-63 b, TOI-1273 b, TOI-269 b, TOI-564 b, TOI-620 b and TOI-837 b. 20 planets had fewer than 2 usable seasons.
   - Calibration: z_cal = z / s, where s = 0.645 is the robust SD (1.4826 MAD) of z for the 134 cool hosts. Check of this scale: for planets with >= 3 seasons, the mean chi2/dof of the linear fit with calibrated errors is 0.82 (cool), 1.04 (intermediate) and 1.02 (hot). Thus the raw bootstrap errors are about 1.5 times too large, and the calibrated errors are consistent with the season-to-season scatter.
   - The relation d|b|/dt = slope / (dT14/db) is evaluated at the mean fitted geometry.
5. `controls.py`: Fixes b for the first season (our fit, or the published b0 for WASP-33 b and KELT-9 b). Then it propagates the published db/dt, converts it to T14 with our a/R* and k, and compares with the later seasons. These comparisons use the conservative uncalibrated bootstrap errors.
6. `robustness.py`, `sector_table.py`, `figures.py`: Variant comparison, per-sector table and figures.

## Results

### Population (base variant, 391 planets that pass the quality cut)

| Host class | N | robust SD of z_cal | N with abs(z_cal) > 3 | Flagged planets |
| --- | --- | --- | --- | --- |
| cool (<= 5700 K) | 134 | 1.00 (by definition) | 1 | TOI-1811 b |
| intermediate | 137 | 0.91 | 0 | none |
| hot (>= 6250 K) | 120 | 1.13 | 6 | TOI-1518 b, KELT-9 b, TOI-1355 b, WASP-167 b, HAT-P-70 b, KOI-13 b |

Hot against the rest: 6/120 against 1/271, one-sided Fisher p = 0.004. Without the five published precessors: 2/115 against 1/271, p = 0.21.

### Planets with abs(z_cal) >= 3 and the controls

| Planet | Teff (K) | Seasons (span, yr) | Mean T14 (min) | dT14/dt (min/yr) | z_cal | mean b (our fit) | d|b|/dt (/yr) | Published |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TOI-1518 b | 7299 | 2 (1.8) | 145.9 | +3.27 +- 0.26 | +12.8 | 0.871 | -0.0119 +- 0.0009 | -0.0116 +- 0.0036 (out of sample) |
| KELT-9 b | 9270 | 4 (4.8) | 231.6 | -0.51 +- 0.04 | -12.4 | 0.397 | +0.0060 +- 0.0005 | +0.0144 +- 0.0025 (sign from Table 1 b values) |
| TOI-1355 b | 8660 | 2 (1.7) | 126.5 | -5.34 +- 0.54 | -9.9 | 0.912 | +0.0163 +- 0.0016 | +0.0163 +- 0.0008 (same data) |
| WASP-167 b | 7000 | 4 (7.0) | 179.6 | +0.70 +- 0.10 | +6.7 | 0.759 | -0.0033 +- 0.0005 | none (new) |
| HAT-P-70 b | 8450 | 2 (5.0) | 221.1 | +0.90 +- 0.27 | +3.4 | 0.549 | -0.0068 +- 0.0020 | none (new, weak) |
| KOI-13 b | 7650 | 5 (4.7) | 196.5 | +0.29 +- 0.09 | +3.1 | 0.282 | -0.0060 +- 0.0019 | -0.011 (Szabo 2020) |
| WASP-33 b | 7430 | 3 (5.0) | 171.5 | -0.23 +- 0.08 | -3.0 | 0.215 | +0.008 +- 0.003 | -0.0143 +- 0.0013 (b crosses 0 near 2019) |
| TOI-1811 b | 4766 | 2 (2.0) | 117.7 | -1.01 +- 0.31 | -3.2 | 0.780 | +0.0075 +- 0.0023 | cool K dwarf; probably chance |

The KELT-9 b and KOI-13 b rates from our photometry are smaller than the published values, because our b is biased high (no gravity darkening in the model) and dT14/db increases with b. The direction agrees with the published values. For WASP-33 b, the published b crosses zero near 2019.9 (Stephan et al. 2022, Table 1), so |b| and T14 must decrease after 2019. Our data show this decrease. Stephan et al. (2022) Table 3 gives -0.0144 +- 0.0025 /yr for KELT-9 b as the 68 % interval but +0.0148 /yr as the best fit. Their Table 1 b values increase from 0.118 (2014) to 0.200 (2019), so we used the positive sign.

### Robustness (calibrated z; full table in `files/data/derived/robustness_table.csv`)

| Planet | base | no prewhitening | quadratic baseline | SAP flux |
| --- | --- | --- | --- | --- |
| TOI-1518 b | +12.8 | +12.6 | +13.5 | +13.2 |
| KELT-9 b | -12.4 | -16.5 | -16.3 | -9.9 |
| TOI-1355 b | -9.9 | -9.9 | -10.8 | -1.4 (SAP noisy) |
| WASP-167 b | +6.7 | +7.3 | +8.9 | +2.3 (SAP noisy) |
| HAT-P-70 b | +3.4 | +3.6 | +2.8 | +0.2 (SAP error x75) |
| KOI-13 b | +3.1 | +3.1 | +2.2 | +2.5 |
| WASP-33 b | -3.0 | -4.8 | -2.1 | -0.6 (SAP noisy) |
| TOI-1811 b | -3.2 | -3.2 | -3.3 | -2.5 |

Fits for each sector block (`files/data/derived/sector_fits.csv`) show that the trends continue inside one year. TOI-1518 b: 146.9 min in sector 77 and 149.1 min in sectors 84-85 (2024). TOI-1355 b: 121.8 min in sectors 77-78 and 119.6 min in sector 84. KELT-9 b: 231.2 min in sector 75 and 229.4 min in sector 82. For WASP-167 b, every sector block is longer than the block before it.

### Physical plausibility for WASP-167 b

For an F1V star with R* of about 1.8 Rsun, a rotation period shorter than the 2.02 d orbit, an apsidal constant k2 of about 0.01-0.03, and a/R* = 4.2, J2 is of the order 5e-5 to 2e-4. The nodal precession rate is (3/2) n J2 (R*/a)^2 cos(psi), of the order 0.1-1 deg/yr. The measured |db/dt| = 0.0033 /yr corresponds to an orbital inclination change of about 0.045 deg/yr (db/dt is approximately (a/R*) di/dt). A near-anti-aligned orbit (lambda = -165 deg) reduces the effect through the geometric factors. Thus the measured rate is in the expected range. A full precession model needs the stellar inclination, which is not known. The trend predicts that T14 will continue to increase by about 0.7 min/yr, to about 183 min by 2028. TESS or CHEOPS can test this forecast.

## Figures

- `files/figures/fig1_z_vs_teff.png`: Calibrated trend significance against host Teff, with z histograms for cool and hot hosts.
- `files/figures/fig2_controls.png`: Measured T14 changes for the five published precessors, compared with the predictions from the published rates.
- `files/figures/fig3_candidates.png`: Per-season T14 and b for WASP-167 b, HAT-P-70 b and TOI-1811 b. The error bars are uncalibrated bootstrap errors, which are conservative by a factor of about 1.5.

## Files

- `files/data/derived/trends_<variant>.csv`: One row for each planet: slope, errors, z, z_cal, chi2, b trend, d|b|/dt and a 3-sigma limit. The `seasons` column holds year:T14:sigma:b:sigma_b:n_transits for each season.
- `files/data/derived/fits_<variant>.jsonl.gz`: Full fit record for each planet (season parameters, bootstrap replicates, red-noise beta, prewhitening count).
- `files/data/derived/summary_<variant>.json`, `calibration.json`: Population statistics.
- `files/data/derived/hot_host_trends_limits.csv`: All 120 hot-host planets with trends and |db/dt| limits.
- `files/data/derived/controls_base.csv`, `robustness_table.csv`, `sector_fits.csv`.
- `files/logs/`: Run logs.

## Reproduce

```
python3 code/select_sample.py                    # needs raw/pscomp_transiting_f0ef.csv and raw/tesscurl/*.sh
sh code/download_lc.sh lc                        # about 4.9 GB; check with tess_lc_sha256.txt
python3 code/fit_shapes.py base 20               # about 2.5 h with 20 processes on a loaded 24-core host
python3 code/analyze.py base                     # writes out/calibration.json (needed by other variants)
for v in nopw quad sap; do python3 code/fit_shapes.py $v 8 @out/robust_set.txt; python3 code/analyze.py $v; done
SEASON_GAP=15 python3 code/fit_shapes.py sector 8 @out/sector_set.txt; python3 code/sector_table.py
python3 code/controls.py base; python3 code/robustness.py
python3 code/figures.py base "WASP-167 b" "HAT-P-70 b" "TOI-1811 b"
```
The bootstrap random seed is the TIC ID, so the results are deterministic for the same inputs and library versions.

## Limitations

- All results use one instrument (TESS) and one pipeline (SPOC PDC). An independent T14 series for WASP-167 b (for example CHEOPS, or archival WASP/KELT photometry fit with the same model) is not part of this work.
- The model is a circular orbit with spherical-star limb darkening. It does not include gravity darkening (KELT-9, KOI-13, MASCARA-4, WASP-33, TOI-1355 and HAT-P-70 are fast rotators), eccentricity (TOI-1355 b, e of about 0.22) or apsidal motion. For a fixed star these effects mostly change the absolute geometry and not the trend. But the conversion from dT14/dt to db/dt depends on the biased b.
- Pulsating hosts (WASP-33, WASP-167, HAT-P-70, KELT-9 after prewhitening) have red-noise beta factors of 1.1-2.8. The transit bootstrap includes this noise, and the no-prewhitening variant gives the same results.
- Many planets have only two seasons, so a linear trend cannot be separated from a single step. The sensitivity is low when b is near 0, because dT14/db goes to 0.
- Sample selection uses catalog values. Teff classes use the pscomppars Teff. We had no v sin i for the full sample, because the Exoplanet Archive was unavailable, so Teff is a proxy for rotation.
- The error calibration assumes that no cool host precesses. If some do, the calibration is conservative.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-astronomy-e35037a95bd5, topic astronomy, machine dell, account claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date 2026-11-09. Python 3.12 research environment of the host, with batman-package 2.5.3 installed into a local directory.
- Related campaign work: sci:sha256:dd04348fcad9296dd08f6abe0d55984cd9d4986d758fafe8712b2d775be0876d (TESS hot-Jupiter mid-times) tested period changes, not durations. sci:sha256:8ecb9990f7282ea1040f88b29800ee2ac4145360aef34a844b14e4db662c8fc2 also tested timing. This work is the first campaign search for duration changes.
