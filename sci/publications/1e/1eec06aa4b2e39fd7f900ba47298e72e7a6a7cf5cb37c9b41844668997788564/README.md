# TESS eclipse times from 2018 to 2025 do not agree with nine published circumbinary-companion timing models of seven post-common-envelope binaries

Job: sci-1107-hp-astronomy-6e951c3606fb (campaign 11_07_2026, topic astronomy, machine hp). Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim. Date of work: 2026-11-09.

## Summary

Many short-period eclipsing post-common-envelope binaries (PCEBs) show eclipse timing variations (ETVs). Authors often explain the ETVs with the light-travel-time (LTT) effect of circumbinary planets or brown dwarfs. A valid LTT model must predict future eclipse times. Pulley et al. (2025) tested 18 recent models with ground-based timings, but they did not use TESS timings, because they thought that TESS timings have too much scatter.

We measured 5,489 primary-eclipse times of 11 PCEBs in 44 TESS sectors (2018 to 2025) with one symmetric-template method. We then did these tests:

1. **TESS timing quality (positive result).** The sector timing uncertainty is 0.06 to 2.1 s for 10 of the 11 systems (V471 Tau: 4 to 10 s). For the sdB + M-dwarf systems, the scatter of single-eclipse times agrees with their formal errors (median reduced chi-square 0.77 to 1.13 per system). 20-s and 120-s data give the same sector times within the errors (24 comparisons; all within 1.8 sigma). Full-frame-image (FFI) times agree with 120-s times (RR Cae: -0.09 +/- 0.39 s) after a target-specific barycentric correction. TESS times agree with published ground times of the same months to -4.6 to +1.6 s (5 comparisons). Thus, TESS timings are sufficiently precise to test LTT models.
2. **Model predictions (negative result for all nine LTT models).** We tested nine published LTT models (HW Vir, HS0705+6700, DE CVn, V471 Tau, NY Vir, NSVS 07826147, Kepler-451 x 3). In TESS sectors after the end of each model's data, the TESS times differ from the predictions by up to 189 s (HW Vir), 115 s (HS0705+6700), 80 s (DE CVn), 52 s (V471 Tau), 21 s (NY Vir), 7 s (NSVS 07826147) and 7 s (Kepler-451, Esmer et al. 2022). Each difference is many times the TESS uncertainty (chi-square 79 for 5 sectors to 10^7 for 1 sector). The two newest Kepler-451 models (Er et al. 2026) were fitted to these TESS data. They still leave an 18-s swing in the TESS residuals, and a free linear ephemeris correction leaves 3.0 to 3.3 s RMS (chi-square 46 and 55 for 6 degrees of freedom).
3. **Quadratic ephemerides of Pulley et al. (2025).** RR Cae TESS times from October to December 2025 are 30 s later than the prediction, 4 to 6 months after the end of their data. The printed QS Vir quadratic coefficient (-8.6 x 10^-13 d) gives a 911-s difference. A positive coefficient gives -46 s, which agrees with the authors' own O-C figure (about -45 s near cycle 80,000). We conclude that the printed sign is probably a typographical error.
4. **TESS-only period changes.** Over 2 to 7 years, TESS alone detects curvature in the O-C diagram of RR Cae, NY Vir, Kepler-451, DE CVn, NSVS 07826147 and V471 Tau (delta chi-square 13 to 3,222 for one added parameter). HS0705+6700 shows no curvature (TESS linear-ephemeris RMS 0.73 s over 4.0 years).

We report no new planet. The results agree with the conclusion of Pulley et al. (2025): published LTT models of PCEBs do not predict later eclipse times. The new contribution is a homogeneous, independent set of space-based timings, a validation of their precision, and tests of four models that Pulley et al. did not test (HW Vir Esmer et al. 2021 at TESS epochs, Kepler-451 Esmer et al. 2022, Kepler-451 Er et al. 2026, V471 Tau Kundra et al. 2022).

## Question

Do published LTT (circumbinary companion) models of eclipsing PCEBs predict the eclipse times that TESS measured after the models were published? Are TESS eclipse timings precise and accurate enough for this test?

## Data

- **TESS SPOC light curves** (120 s and 20 s; PDCSAP flux; quality flag 0) for 11 targets, sectors 3 to 97: 67 files from MAST. `files/results/provenance.json` gives the file names, MAST URIs and SHA-256 hashes. TESS data are NASA data without copyright restrictions. We do not redistribute the FITS files.
- **TESS FFI cutouts** (MAST TESScut, 15 x 15 pixels) for sectors without SPOC data and for overlap checks: NSVS 07826147 (S77, S78), RR Cae (S97, S98), HW Vir (S46; S91 is unusable, because the target is outside the science pixels of the cutout). Hashes are in `provenance.json`.
- **TESS spacecraft ephemeris** from JPL Horizons (id -95), for the target-specific barycentric correction of FFI times.
- **Model parameters** from the papers listed in the references (arXiv sources; URLs and SHA-256 hashes of the downloaded source files are in `provenance.json`). `files/code/models.py` contains the parameter values. We do not redistribute the papers or their timing tables. `files/code/05_extract_checkdata.py` extracts the timing tables into local scratch from the arXiv sources.

The 11 targets and their TIC numbers: HW Vir (156618553), NY Vir (175402069), NSVS 14256825 (404635917), NSVS 07826147 (148785530), HS0705+6700 (99641129), Kepler-451 (271164763), QS Vir (287346045), RR Cae (219244444), NN Ser (172608008), DE CVn (446175401), V471 Tau (456863710).

## Method

**Eclipse timing** (`code/timing.py`, `code/03_run_timing.py`). For each target and cadence:

1. We normalized each sector and divided it by a running median (window max(1 d, 5 P)) of the out-of-eclipse flux.
2. We folded the data on a reference linear ephemeris. We found the eclipse centre as the symmetry centre of the folded profile: for each trial centre, we fitted the antisymmetric part of the profile with a line (a baseline slope) and kept the centre with the smallest remaining antisymmetry.
3. We built a symmetric empirical template (the folded profile, averaged with its mirror image) inside a fixed phase window. Because the template is symmetric, a fitted shift measures the time of the eclipse centre.
4. For each eclipse, we fitted the shift, with an offset, a linear slope and a depth scale. These three parameters are solved linearly at each trial shift. The shift uncertainty comes from the curvature of the profile chi-square, multiplied by max(1, reduced chi-square)^0.5. We rejected eclipses with less than 80 % of the expected points or without points on both sides of the eclipse centre.
5. For each sector, we combined the single-eclipse times relative to the reference ephemeris with a weighted mean and 4-sigma clipping (`code/07_analyze.py`). The sector uncertainty is the larger of the scaled formal error and the standard error of the scatter.

We used the 120-s data as the primary data set, and FFI data only for sectors without 120-s data. All times are BJD_TDB at mid-exposure.

**FFI time correction** (`code/barycorr.py`, `code/04_ffi_phot.py`). The TIMECORR column of TESScut cutouts is the barycentric correction for a reference position, not for the target. For HW Vir in S46, it differs from the SPOC target correction by 30 to 36 s. We replaced it: t = TIME - TIMECORR + (r_TESS . n_target)/c, with the TESS position from JPL Horizons. Our correction agrees with the SPOC TIMECORR of HW Vir to 0.006 s. The applied shifts were -18 to +35 s for the five cutouts that we used.

**Model conventions** (`code/models.py`, `code/06_check_conventions.py`). The papers use different LTT formulas (with or without the Irwin e sin(omega) term; omega of the binary or of the companion). For each model with ambiguous terms, we calculated the residuals of the paper's own tabulated eclipse times for each option. We used the option with the smallest RMS. With the chosen options, the median residual of each paper's own data is -3.7 to +7.1 s (+7.1 s for Kepler-451, Esmer et al. 2022, whose ground times have a 13-s robust scatter; all options give 30.6 to 30.7 s RMS there) (`files/results/convention_checks.csv`). For DE CVn (Han et al. 2018), the table label "2 beta = -1.22 x 10^-11" must be read as the E^2 coefficient: the other reading gives 56 s RMS on the authors' own times, against 10 s. For Er et al. (2026), we used the published formula without the e sin(omega) term. The paper does not report the fitted corrections to T0, the binary period and the quadratic term, so we used the linear ephemeris of its equations 1 and 2.

**Model test** (`code/07_analyze.py`, `code/08_extra_tests.py`). For each model and TESS sector we calculated TESS minus model. We classified a sector as "after data end" if it starts after the last data that the model used. We also removed a best-fit linear function of cycle number from the residuals. This step absorbs errors in T0 and the period, such as rounding or unreported corrections. A model with the correct shape then gives residuals near the TESS errors.

## Results

### 1. TESS timings are precise and agree with ground timings (Figure 2)

| Target | Sectors | Eclipses | Median sector error (s) | Median single-eclipse error (s) | Median reduced chi-square |
| --- | --- | --- | --- | --- | --- |
| HW Vir | 1 | 193 | 0.06 | 0.75 | 1.13 |
| NY Vir | 4 | 695 | 0.39 | 4.8 | 0.77 |
| NSVS 14256825 | 2 | 283 | 0.43 | 5.0 | 0.83 |
| NSVS 07826147 | 5 | 431 | 0.27 | 2.5 | 0.79 |
| HS0705+6700 | 5 | 1,011 | 0.82 | 11.3 | 0.83 |
| Kepler-451 | 8 | 1,579 | 1.25 | 17.0 | 0.92 |
| RR Cae | 7 | 672 | 0.27 | 2.1 | 0.97 |
| DE CVn | 5 | 241 | 1.47 | 8.7 | 0.84 |
| QS Vir | 1 | 104 | 1.14 | 4.4 | 3.33 |
| NN Ser | 1 | 83 | 3.07 | 10.5 | 7.99 |
| V471 Tau | 5 | 197 | 5.53 | 6.6 | 20.2 |

For the white-dwarf eclipses of V471 Tau, QS Vir and NN Ser, the ingress and egress last about one minute. At 120-s cadence the formal single-eclipse errors are then too small, and we used the scatter-based sector errors. Kepler-451 single-eclipse errors (17 s) agree with the 16.7 s that Er et al. (2026) report for their TESS times. The large single-eclipse scatter that some authors report is thus a property of single eclipses. A sector of about 200 eclipses gives about 1 s.

Cross-checks (`files/results/crosschecks.csv`): 20-s minus 120-s sector times are within 1.3 s for all systems except V471 Tau (-9.3 +/- 5.6, -8.2 +/- 4.7, +7.2 +/- 4.3 s). All 24 differences are within 1.8 sigma. FFI minus 120-s: RR Cae S97 -0.09 +/- 0.39 s; HW Vir S46 (600-s FFI) -0.24 +/- 5.3 s.

TESS minus ground (same model as reference; `files/results/tess_vs_ground.csv`): HW Vir S46 vs Mai & Mutel (2022), -4.6 s (one ground time, 17 d later); HS0705+6700 S20 and S47 vs Mai & Mutel (2022), -3.4 and -2.9 s (one ground time each, 8 and 26 d away); Kepler-451 S40 vs Esmer et al. (2022), -2.5 +/- 2.1 s (19 ground times); NSVS 07826147 S24 vs Wolf et al. (2021), +1.6 +/- 1.0 s (5 ground times). One ground eclipse of Kepler-451 in November 2019 (two filters) is 82 s from both the model and the TESS times of S14 and S15. We think that this ground time is an outlier. The mean of the five good comparisons is -2.4 s. We cannot exclude a systematic offset of a few seconds between TESS and ground clocks. This offset is much smaller than the model failures below.

### 2. Published LTT models do not predict the TESS times (Figure 1)

| Model | Data end | TESS sectors in span / after | Mean TESS - model after data end (s) | Max abs after (s) | chi-square after | RMS after free linear term (s) |
| --- | --- | --- | --- | --- | --- | --- |
| HW Vir, Esmer et al. 2021 (2 LTT + quadratic) | 2019-03 | 0 / 1 | +189.0 | 189.0 | 1.0e7 (1 sector) | - |
| HS0705+6700, Mai & Mutel 2022 (1 LTT + quadratic) | 2022-02 | 2 / 3 | -97.4 | 115.3 | 38,174 | 9.8 (chi-square 701, 3 dof) |
| DE CVn, Han et al. 2018 (sine + quadratic) | 2017-05 | 0 / 5 | -53.5 | 79.8 | 7,760 | 1.9 (chi-square 10.4, 3 dof) |
| V471 Tau, Kundra et al. 2022 (1 LTT + dP/dt) | 2020-09 | 0 / 5 | -37.0 | 51.5 | 286 | 9.6 (chi-square 18.0, 3 dof) |
| NY Vir, Er et al. 2021 (2 LTT + quadratic) | 2021-03 | 1 / 3 | -8.2 | 21.2 | 3,102 | 2.2 (chi-square 119, 2 dof) |
| NSVS 07826147, Wolf et al. 2021 (1 LTT) | 2020-09 | 1 / 4 | -6.1 | 6.9 | 1,397 | 1.4 (chi-square 58, 3 dof) |
| Kepler-451, Esmer et al. 2022 (3 LTT + quadratic) | 2021-09 | 3 / 5 | +4.3 | 7.2 | 78 | 3.9 (chi-square 85, 6 dof) |
| Kepler-451, Er et al. 2026, DS-A (2 LTT) | 2024-08 | 8 / 0 | (in span: -2.5) | - | - | 3.0 (chi-square 46, 6 dof) |
| Kepler-451, Er et al. 2026, DS-B (3 LTT) | 2024-08 | 8 / 0 | (in span: -2.2) | - | - | 3.3 (chi-square 55, 6 dof) |

All seven models with post-data TESS sectors fail. The failures are 2 to 13 times the semi-amplitudes of the smallest LTT terms of the Kepler-451 and NSVS 07826147 models (1.3 to 4.3 s), and 189 s for HW Vir 2.7 years after its data end. For DE CVn, most of the difference is a linear drift (-8.4 s per 1000 cycles). A period correction would remove it, but the model did not predict it. For HS0705+6700, V471 Tau, NY Vir and both Kepler-451 models of Er et al. (2026), the residuals keep a shape that a linear correction does not remove.

We could not test some models: Brown-Sevilla et al. (2021) give the reference period of HW Vir with 7 decimals (rounding error up to 500 s by 2025), and Baycroft et al. (2023) give no reference epoch. Mai & Mutel (2022) do not give their HW Vir model parameters.

### 3. Pulley et al. (2025) quadratic ephemerides

TESS residuals in the span of their data (2018 to 2025) agree with the trends in their O-C figures (for example, NY Vir: TESS +26.6 s in April 2025, figure about +25 s; RR Cae: TESS -13 s in 2018-2020, figure about -15 to -20 s). The two RR Cae sectors after their data end (October and December 2025) are +29.5 and +30.8 s from the prediction. QS Vir: see Summary item 3.

### 4. TESS-only O-C curvature (Figure 3)

| Target | Sectors | Span (yr) | chi-square, linear | Delta chi-square (quadratic) | RMS linear (s) |
| --- | --- | --- | --- | --- | --- |
| RR Cae | 7 | 7.2 | 3,235 (5 dof) | 3,222 | 6.0 |
| NY Vir | 4 | 5.0 | 307 (2 dof) | 307 | 3.4 |
| Kepler-451 | 8 | 5.1 | 176 (6 dof) | 167 | 5.8 |
| DE CVn | 5 | 4.5 | 89 (3 dof) | 85 | 5.6 |
| NSVS 07826147 | 5 | 4.0 | 15.9 (3 dof) | 13.6 | 0.75 |
| V471 Tau | 5 | 2.2 | 18.5 (3 dof) | 12.6 | 9.7 |
| HS0705+6700 | 5 | 4.0 | 4.2 (3 dof) | 0.2 | 0.73 |

The V471 Tau curvature depends on two groups of sectors with a 2-year gap, so its shape is not constrained. For HS0705+6700, the TESS times from 2020 to 2024 agree with a constant period. This agrees with the low recent activity that Pulley et al. (2025) report for this system.

## Interpretation

The TESS data confirm, with an independent instrument and one homogeneous method, that LTT models of PCEBs do not predict later eclipse times, even 1 to 3 years after their data end. The period changes continue (item 4), but they do not follow the predicted Keplerian shapes. Thus, the data do not support the circumbinary planets that these models propose. The data do not exclude companions with other orbits, or a combination of companions and magnetic (Applegate-type) effects in the M-dwarf or K-dwarf secondaries. We did not test magnetic models quantitatively.

## Limitations

- TESS gives only one to eight sectors per system, so the tests use few epochs. HW Vir has only one usable sector.
- Some model parameters are rounded in the papers. Where a paper does not give fitted ephemeris corrections (Er et al. 2026), the absolute predictions are uncertain; the free-linear-term RMS addresses this.
- The convention choice uses only the paper's own tabulated times. For Er et al. (2026) there are only 6 printed times, and for NY Vir 4.
- The QS Vir sign correction is our inference from the authors' figure. The authors did not confirm it.
- A systematic offset of a few seconds between TESS and ground timings cannot be excluded (mean of 5 comparisons -2.4 s).
- Single-eclipse errors at 120 s are too small for short white-dwarf ingress and egress; we used scatter-based sector errors for those systems.
- We did not search for new eclipsing PCEBs or new companions.

## Reproducibility

Requirements: Python 3.12 with numpy, scipy, pandas, astropy, matplotlib, astroquery 0.4.11, lightkurve 2.6 (only for imports), `curl`, `unzip`, `pdftotext`. Run from a scratch folder that contains `code/`:

```
bash code/run_all.sh
```

This script downloads the TESS data and the arXiv sources into local scratch folders (`data/`, `lit/`), measures the eclipse times and writes `results/` and `figs/`. Network services: MAST (light curves, TESScut, TIC), JPL Horizons, arXiv. A full run takes about 1 hour on 11 cores. MAST and arXiv file versions can change; compare the hashes with `files/results/provenance.json`.

Files in this bundle:

- `files/code/`: all code (MIT license through the SCI baseline license).
- `files/results/ecl_<target>_<cadence>.csv`: single-eclipse TESS times (BJD_TDB, error in days, cycle, sector).
- `files/results/sec_*.csv`, `tess_sector_times.csv`: sector times (column `primary` marks the data set used for model tests).
- `model_residuals.csv`, `model_summary.csv`, `model_linear_detrended.csv`: model tests.
- `crosschecks.csv`, `scatter_tests.csv`, `tess_vs_ground.csv`, `tess_only_ephemeris.csv`, `convention_checks.csv`, `conventions_*.json`: checks.
- `provenance.json`: source files, URLs and SHA-256 hashes.
- `files/figs/`: the three figures.

## External data and attribution

This bundle contains our own measurements from TESS data and aggregate numbers. It does not contain third-party files. TESS data: NASA TESS mission, MAST (STScI); TESS data are without copyright restrictions. The model parameters in `files/code/models.py` are numerical values cited from the papers below, with attribution. The published eclipse-time tables are not redistributed; `05_extract_checkdata.py` regenerates them locally from the arXiv sources.

## References

- Pulley D., Sharp I. D., Mallett J., von Harrach S. 2025, arXiv:2507.06748.
- Esmer E. M. et al. 2021, A&A 648, A85, arXiv:2103.00062 (HW Vir).
- Mai X., Mutel R. L. 2022, MNRAS 517, L108, arXiv:2110.14869 (HS0705+6700; HW Vir times).
- Esmer E. M. et al. 2022, MNRAS 511, 5207, arXiv:2202.02118 (Kepler-451).
- Er H. et al. 2026, arXiv:2606.26817 (Kepler-451).
- Han Z.-T. et al. 2018, ApJ 868, 53, arXiv:1811.08625 (DE CVn).
- Kundra E. et al. 2022, MNRAS 517, 1031, arXiv:2210.01464 (V471 Tau).
- Er H., Ozdonmez A., Nasiroglu I. 2021, MNRAS 507, 809, arXiv:2107.07003 (NY Vir).
- Wolf M. et al. 2021, A&A 647, A65, arXiv:2101.08475 (NSVS 07826147).
- Brown-Sevilla S. B. et al. 2021, MNRAS 506, 2122, arXiv:2106.15632; Baycroft T. A. et al. 2023, arXiv:2309.05716 (HW Vir; not testable).
- Irwin J. B. 1952, ApJ 116, 211.
