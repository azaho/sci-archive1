# ASASSN-14ko flares in 2022-2025 drift later than the published decaying-period ephemeris; the period stays near 108 days

**Job:** sci-1107-dell-astronomy-dda9744aec7a. **Topic:** astronomy. **Campaign:** 11_07_2026. **Machine:** dell. **Model:** Claude Opus 5.5 (`claude-opus-5-5`), working as an automated SCI campaign worker. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

ASASSN-14ko is a periodic nuclear transient in the Seyfert galaxy ESO 253-G003 (z = 0.042). Its optical flares repeat every 105 to 115 days. Payne et al. (2021, 2022) fitted the peak times of the 2014-2021 flares with a period that decreases at a constant rate:

t(n) = t0 + n P0 + n^2 P0 Pdot / 2 + n^3 P0 Pdot^2 / 6, with t0 = JD 2456852, P0 = 115.2 d, Pdot = -0.0026 +/- 0.0006.

The value Pdot = -0.0026 is the main observed constraint for many models of this source: repeated partial tidal disruption, star-disc drag (Linial & Quataert 2024), and stellar mass-loss models (Bandopadhyay et al. 2026). These papers use the 2022 value. We found no published timing update with flares after 2022.

We ask: **Did the flares from 2022 to 2025 occur at the times that the published ephemeris predicts? Does the period continue to decrease at Pdot = -0.0026?**

This is an out-of-sample forecast test. The ephemeris was published in June 2022 (arXiv:2206.11278) and used flares up to November 2021 (flare n = 24 in our numbering). All flares with n >= 25 are new data for the model.

## 2. Data

| Data | Source | Span used | Role |
| --- | --- | --- | --- |
| Published peak times n = 0-24 | Payne et al. 2021 Table 3; Payne et al. 2022 Sec. 3 | 2014-07 to 2021-11 | Training set, as in the original fit |
| ASAS-SN g-band aperture photometry | ASAS-SN Sky Patrol v2, asas_sn_id 661431833080 (RA 81.3223, Dec -46.0053), retrieved 2026-11-09 | 2017-09 to 2025-02-07 (MJD 58022-60709) | New peak times n = 25-34; method check on n = 11-24 |
| TESS SPOC FFI cutouts (TESScut, 25x25 px; 30-min cadence in S4-6, 10-min in S31-33, 200-s in S87 and S98) | MAST TESScut, sectors 4, 5, 6, 31, 32, 33, 87, 98 | 2018-10 to 2026-01 | New peak time n = 38 (Sector 98); method check on n = 14 and n = 21 |
| Swift UV/optical peak dates | Huang et al. 2023 (arXiv:2310.03236), text | 2023 | Independent check of n = 28 and n = 29 |

The Sky Patrol light curve ends on 2025-02-07. On 2026-11-03 the Sky Patrol service announced a full rebuild of its catalogs and light curves, with possible changes of asas_sn_id. For this reason we archive the exact light curve that we used (`files/data/raw/asassn_skypatrol_14ko_661431833080.csv`). The TESScut FITS files (600 MB) are not in the bundle. `files/code/00_get_data.sh` downloads them again, and `files/data/raw/SHA256SUMS_inputs.txt` gives the SHA-256 of the files that we used.

## 3. Method

1. **ASAS-SN preparation** (`01_asassn_prepare.py`). We keep good-quality g-band points with flux error < 0.3 mJy. We remove small additive camera offsets (at most 0.027 mJy, `asassn_camera_offsets.csv`). The flares add about 0.5-1.5 mJy to a host-plus-nucleus flux of about 3.2 mJy.
2. **ASAS-SN peak times** (`02_flare_times.py`). For each flare number n, we search +/-45 d around a neutral constant-period ephemeris. This ephemeris is a linear fit to the published n <= 24 peaks, so the search window does not favour the tested model. We measure the peak with two methods:
   - *template*: a fixed-shape profile (half-Gaussian rise, sigma = 5.1 d; exponential decline, tau = 14.9 d; the shape is fitted jointly to 16 well-sampled flares) with free peak time, amplitude and baseline. The error comes from a residual bootstrap.
   - *poly5*: a fifth-order polynomial, as used by Payne et al., with a point bootstrap.
   A flare is "well sampled" if it has at least 4 points in the 15 d before and the 15 d after the peak. The total error per flare is the template error, half the template-polynomial difference, and 0.8 d jitter (the jitter of Payne et al.) in quadrature.
3. **Method calibration.** For eight well-sampled training flares (n = 12-24), our template times are 0.89 +/- 0.66 d later than the published times. We subtract this offset from the new times. The result does not change without the subtraction (Table 3, V3).
4. **TESS photometry** (`03_tess_phot.py`, `04_tess_diffimg.py`, `05_tess_peaks.py`). For each cadence, we subtract a sky level (median of the faintest 30% of pixels more than 5 px from the target) and sum a 3x3-pixel aperture. We bin to 0.25 d. Difference images (flare minus quiet) show the position of the excess. We fit a half-Gaussian-rise plus exponential-decline flare with a constant or linear baseline. We use 12 variants (three windows, with and without high-sky bins, with and without slope). The peak time is the median of the variants.
5. **Forecast test** (`06_timing_test.py`). We compare the new peak times with three forecasts made only from the training data: (a) the exact published ephemeris (Payne22); (b) our refit of the same model to the 20 published ASAS-SN peaks (Pdot refit); (c) a constant period fitted to the same peaks. The forecast uncertainty comes from the fit covariance (Monte Carlo). We also fit Pdot to the flares n >= 21 only. We scale its error by sqrt(chi2/dof) because the timing scatter is larger than the formal errors.
6. **Robustness** (`07_robustness.py`): polynomial peaks; running-median maxima; exclusion of the broad March 2022 flare (n = 25); no offset correction; inclusion of the poorly sampled flare n = 33; TESS alone.

## 4. Results

### 4.1 The TESS Sector 98 flare (December 2025 - January 2026)

TESS Sector 98 (MJD 60988-61045) contains the predicted time of flare n = 38 (MJD 61020.0 = 2025-12-10 for the published ephemeris). The flux in the 3x3 aperture is flat near the predicted date. It starts to rise at MJD 61033 and reaches a broad maximum at **MJD 61040.4** (2026-01-01). The rise is about 50 e-/s, similar to the 2018 and 2020 TESS flares (31-67 e-/s). The difference image (MJD 61040-61045 minus 61020-61029) shows a point source at the nucleus. Its centroid is 0.5 px from the target position (Figure 2). Thus the brightening is a flare of ASASSN-14ko and not scattered light. The peak is +20.5 d later than the published forecast (z = 3.4 with an observation error of 3.1 d and a forecast error of 5.2 d).

Method check: our TESS method gives 58437.1 (range 58433.9-58437.9) for the 2018 flare and 59202.6 for the 2020 flare. Payne et al. (2022) give 58435.0 and 59205.6 from a better difference-imaging pipeline. Our TESS times are thus correct to about 3 d. We add a 3-d systematic error. Sector 87 (MJD 60662-60689) has no flare. All models predict flare n = 35 after MJD 60705.

### 4.2 ASAS-SN peak times 2022-2025 and the forecast scores

Table 1. New peak times and O-C (observed minus calculated) in days. Training: published peaks n <= 24.

| n | Instrument | Observed MJD | Error | O-C Payne22 | O-C Pdot refit | O-C constant P |
| --- | --- | --- | --- | --- | --- | --- |
| 25 | ASAS-SN g | 59629.8 | 2.2 | -10.2 | -12.0 | -20.3 |
| 27 | ASAS-SN g | 59851.2 | 1.8 | -4.1 | -6.8 | -20.4 |
| 28 | ASAS-SN g | 59962.7 | 1.1 | +0.2 | -3.1 | -19.7 |
| 29 | ASAS-SN g | 60071.6 | 5.0 | +2.1 | -1.7 | -21.5 |
| 30 | ASAS-SN g | 60184.2 | 1.8 | +8.0 | +3.7 | -19.7 |
| 31 | ASAS-SN g | 60291.1 | 1.6 | +8.4 | +3.5 | -23.6 |
| 32 | ASAS-SN g | 60395.5 | 1.1 | +6.7 | +1.2 | -30.0 |
| 33* | ASAS-SN g | 60508.3 | 1.2 | +13.6 | +7.5 | -28.0 |
| 34 | ASAS-SN g | 60612.6 | 1.1 | +12.3 | +5.5 | -34.4 |
| 38 | TESS S98 | 61040.4 | 3.1 | +20.5 | +10.8 | -49.7 |

\*n = 33 is poorly sampled (one point before the peak) and is not in the main set. Flare n = 26 fell in a seasonal gap. Flares n = 35-37 occurred after the Sky Patrol data end.

Table 2. Forecast scores for the nine well-sampled new flares.

| Forecast (from training data only) | Mean O-C (d) | RMS O-C (d) | chi2 (9 flares) | Median abs(z) |
| --- | --- | --- | --- | --- |
| Constant period, 110.78 d | -26.6 | 28.2 | 1678 | 12.7 |
| Payne et al. 2022 published ephemeris | +4.9 | 9.9 | 66 | 2.8 |
| Same model, refit to the 20 published peaks (Pdot = -0.00233 +/- 0.00020) | +0.1 | 6.5 | 47 | 1.5 |

The two independent Swift UV peaks of Huang et al. (2023), MJD 59962 (n = 28) and 60070 (n = 29), agree with our ASAS-SN times (59962.7 and 60071.6) within 2 d.

Our findings:

1. **A constant period fails completely.** All new flares occur 20-50 d earlier than a constant 110.8-d period predicts. Thus the period decrease from 2014 to 2021 was real.
2. **The published decaying-period ephemeris drifts.** Relative to the published ephemeris, the O-C values increase from -10 d (March 2022) to +20.5 d (January 2026). The linear trend is **+2.2 +/- 0.2 d per cycle** (errors scaled by sqrt(chi2/dof)). This trend is present in all variants: +2.05 to +2.42 d per cycle (Table 3). The refit of the same model also gives a positive trend in O-C (from -12 d to +11 d).
3. **The period did not continue to decrease after 2021.** A fit to the flares n >= 21 (2020-12 to 2026-01, 13 flares) gives Pdot = -0.0002 +/- 0.0008 (scaled error). This is consistent with zero. The difference from the published -0.0026 +/- 0.0006 is 2.4-2.8 sigma in the variants. A constant period fits the n >= 21 flares as well as a decaying period: **P = 108.18 +/- 0.15 d**. The published model gives 104.5 d for the period at n = 38. The local period (Figure 3) decreases from about 112.5 d (2018) to 107.6 d (2021-2022). After that, it varies between about 107 and 110 d with no net decrease.
4. **The timing scatter is larger than the measurement errors.** After the trend is removed, the residuals are a few days, for example the early broad flare of March 2022 (n = 25) and the late flare n = 33. Thus a smooth timing law is only an approximation. Some of this scatter can come from flare structure (early bumps and rebrightenings, Huang et al. 2023) that moves the measured peak.

Table 3. Robustness variants (comparison with the published ephemeris; Pdot from flares n >= 21).

| Variant | Flares | O-C trend (d/cycle) | Pdot (n >= 21) | Pdot difference from -0.0026 (sigma) |
| --- | --- | --- | --- | --- |
| V0 base (template, offset removed) | 9 | +2.20 +/- 0.23 | -0.0002 +/- 0.0008 | 2.5 |
| V1 polynomial peaks | 9 | +2.13 +/- 0.26 | -0.0003 +/- 0.0007 | 2.5 |
| V2 without n = 25 | 8 | +2.05 +/- 0.25 | -0.0004 +/- 0.0006 | 2.5 |
| V3 no offset correction | 9 | +2.18 +/- 0.23 | -0.0003 +/- 0.0007 | 2.4 |
| V5 with poorly sampled n = 33 | 10 | +2.31 +/- 0.24 | -0.0001 +/- 0.0008 | 2.6 |
| V6 running-median maxima | 9 | +2.42 +/- 0.25 | -0.0000 +/- 0.0007 | 2.8 |
| V4 TESS n = 38 only | 1 | O-C = +20.5 d, z = 3.4 | - | - |

For all data (2014-2026), a model with a changing Pdot (Pdot + Pddot) is better than a constant Pdot (BIC 100.9 against 112.0; chi2 87.4/25 against 101.9/26). Its Pddot is positive. Thus the period decrease slows down.

### 4.3 Forecast for the next flares

`files/data/derived/forecast_2026_2027.csv` gives the predicted peak times of flares n = 39-44 from three updated fits, which include all the data. The predicted peaks are different by up to 25 d. Thus each new flare is a clear test:

| n | Payne22 | Pdot (all data) | Pdot + Pddot | Constant P (n >= 21) |
| --- | --- | --- | --- | --- |
| 40 | 61228 (2026-07-07) | 61247 +/- 3 | 61255 +/- 5 | 61262 +/- 2 (2026-08-09) |
| 41 | 61332 (2026-10-18) | 61352 +/- 3 | 61362 +/- 6 | 61370 +/- 2 (2026-11-25) |
| 42 | 61435 (2027-01-30) | 61457 +/- 3 | 61469 +/- 7 | 61478 +/- 3 (2027-03-13) |

The errors are formal fit errors. Add about +/-5 d for the observed timing scatter. The source is visible from the southern hemisphere for most of the year, except about May to July.

## 5. Interpretation

The data agree with a period that decreased by about 5-6 d from 2016 to 2021 and then stayed at 107-110 d from 2021 to 2026. They do not agree with a constant Pdot = -0.0026 through 2026. A model that needs a steady orbital decay of this size (for example steady drag from a stable accretion disc, Linial & Quataert 2024) must also explain why the decay stopped or slowed. Possible reasons are a change of the disc density near the pericentre, a change of the stellar mass loss per passage, or a non-orbital source of timing noise. We did not test these physical models. Our result is a timing measurement and a forecast test only. Physical models should use the period history in `local_periods.csv` and the peak times in `all_peak_times_used.csv`, not one constant Pdot.

## 6. Limitations

- The ASAS-SN data are Sky Patrol aperture fluxes, not image-subtraction photometry. The host galaxy is in the aperture. This adds noise but does not shift the peak time much (method offset 0.9 +/- 0.7 d on the training flares).
- "Peak time" is not well defined for flares with bumps and rebrightenings. Different estimators move individual peaks by 1-5 d (Table 3). The trend result holds for all estimators that we tried.
- The TESS peak time has a 3-d systematic error from our simple aperture photometry. The S98 sector ends 5 d after the maximum, so the decline is only partly sampled. The flux was still rising at MJD 61039, so the peak cannot be earlier than about 61039, which is 19 d after the published forecast.
- After 2025-02-07 we have only one flare (TESS n = 38). Flares n = 35-37 and n = 39-41 have no data in this study. ATLAS forced photometry, Swift UVOT archives and the rebuilt Sky Patrol can add these flares.
- The published errors have no covariance matrix. For the uncertainty of the published forecast we used the covariance of our refit of the same model to the same peaks.
- The O-C trend and the n >= 21 Pdot are not fully independent of the choice to start the segment at n = 21. With n >= 17 the fitted Pdot is -0.0008 +/- 0.0002 (formal), which is also smaller in magnitude than -0.0026.

## 7. Side check: AT2023uqm

We first planned to test the predicted sixth flare of the periodic nuclear transient AT2023uqm (ZTF23abikzfr; Wang et al. 2025, arXiv:2510.26561: first peak near MJD 61280 = 2026-08-28). This test was not possible with public ZTF alerts. ALeRCE has no ZTF alerts within 1 deg of the source (RA 347.66, Dec +34.90) after MJD 61160 (2026-04-19). At other Dec +35 test positions the last alerts are at MJD 61028 (RA 300) and 61228 (RA 20). At Dec 0 to +10 the alerts continue to MJD 61352-61353 (2026-11). The 2026 public ZTF alert stream thus did not cover this position during the predicted flare. The queries are in `files/data/side_check_at2023uqm/`. This is a statement about public alert coverage only. It says nothing about whether the flare occurred.

## 8. Reproduction

1. Make an empty working directory W. Copy `files/code/*` to `W/code/` and `files/data/raw/published_peaks.csv` to `W/out/`.
2. In W, run `bash code/00_get_data.sh`. It downloads the TESScut cutouts and the Sky Patrol light curve. Because Sky Patrol is being rebuilt, copy `files/data/raw/asassn_skypatrol_14ko_661431833080.csv` to `W/raw/asassn/14ko_661431833080.csv` to use the exact data of this study.
3. Run `bash code/run_all.sh`. It runs steps 01-08. The run takes about 3 minutes on one core. The outputs go to `W/out/` and the figures to `W/result/files/figures/`.

Software: Python 3.12, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, pandas 3.1.1, matplotlib 3.11.2, skypatrol (pyasassn) 0.6.20. Random seeds are fixed in the scripts.

Files:
- `files/data/derived/timing_table.csv`: new peak times, forecasts, O-C.
- `files/data/derived/asassn_flare_times.csv`: all ASAS-SN peak fits (template and polynomial, sampling flags).
- `files/data/derived/tess_peaks.json`, `tess_peak_variants_*.csv`, `tess_diffimages.json`, `tess_s*.csv`: TESS photometry and fits.
- `files/data/derived/timing_summary.json`, `robustness.json`, `local_periods.csv`, `all_peak_times_used.csv`, `forecast_2026_2027.csv`.
- `files/data/derived/log_06.txt`, `log_07.txt`: console output.

## 9. References

- Payne, A. V. et al. 2021, ApJ 910, 125, "ASASSN-14ko is a Periodic Nuclear Transient in ESO 253-G003" (arXiv:2009.03321).
- Payne, A. V. et al. 2022, "Chandra, HST/STIS, NICER, Swift, and TESS Detail the Flare Evolution of the Repeating Nuclear Transient ASASSN-14ko" (arXiv:2206.11278).
- Huang, S. et al. 2023, "Dissonance in harmony: the UV/optical periodic outbursts of ASASSN-14ko exhibit repeated bumps and rebrightenings" (arXiv:2310.03236).
- Linial, I. & Quataert, E. 2024, "Period evolution of repeating transients in galactic nuclei" (arXiv:2309.15849).
- Bandopadhyay, A. et al. 2026, "Repeating Nuclear Transients from Repeating Partial Tidal Disruption Events" (arXiv:2603.04559).
- Wang, Y. et al. 2025, "A Star's Death by a Thousand Cuts: The Runaway Periodic Eruptions of AT2023uqm" (arXiv:2510.26561).
- Hart, K. et al. 2023, "ASAS-SN Sky Patrol v2.0" (arXiv:2304.03791).
- Brasseur, C. E. et al. 2019, Astrocut / TESScut (ascl:1905.007).
