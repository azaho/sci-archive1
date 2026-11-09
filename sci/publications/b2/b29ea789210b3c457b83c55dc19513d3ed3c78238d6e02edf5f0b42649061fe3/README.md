# ASASSN-14ko flares in 2023-2025 occur up to 21 days later than the Payne et al. 2022 ephemeris predicts, and the period decrease became slower after 2021

**Job:** sci-1107-dell-astronomy-47d9bed7bab4 (campaign 11_07_2026), topic astronomy, machine dell, model claude-opus-5-5 (Claude Code), account claude-andrii. The signing key is a campaign-machine key. It is not a personal authorship claim. Date of analysis: 2026-11-09.

## Summary

ASASSN-14ko is a nuclear transient in the Seyfert galaxy ESO 253-G003 (z = 0.042). Its optical and UV flares repeat with a period of approximately 115 d. Payne et al. (2021, 2022) found that the period decreases. Their published timing model (Payne et al. 2022, fit to flares up to 2021 November) is

t(n) = t0 + n P0 + n^2 P0 Pdot / 2 + n^3 P0 Pdot^2 / 6, with t0 = JD 2456852, P0 = 115.2 d, Pdot = -0.0026.

The value of Pdot is an important constraint for repeating partial tidal disruption models and for star-disk interaction models of this source. We did an out-of-sample test of this ephemeris with 2022-2025 data that the model did not use:

* ASAS-SN Sky Patrol v2 g-band photometry (to 2025 February),
* our own aperture photometry of 382 Swift/UVOT visits (2020-2026, UVW2/UVM2/UVW1),
* TESS full-frame-image photometry of sectors 4-6, 31-33, 87 and 98 (sector 98: 2025 October-November).

Main results:

1. **The published Payne et al. 2022 ephemeris fails after 2022.** After we remove the fixed offset of each timing estimator (calibrated on 2018-2021 flares), the flares occur later than the prediction by +3 to +6 d in 2022-2023, by +6 to +17 d in 2023-2024, and by +21 d in 2025 November (TESS sector 98, cycle n = 38). Three instruments and three timing markers agree (Figure 1, Figure 3).
2. **The period decrease became slower after about 2021.** From the clean markers (Swift UVW2 peak, optical half-rise time), the local period decreased by 0.41 +/- 0.09 d per cycle in 2018-2021 and by 0.12 +/- 0.06 d per cycle in 2021-2025 (difference z = 2.7, approximate). The mean local period at cycles 31-38 (2023-2025) is 107.45 +/- 0.32 d. The Payne et al. 2022 model predicts 105.3 d there (Figure 2).
3. **The strength of the evidence for a change in Pdot depends on the data set.** A re-fit of the published 2014-2021 peak times with a free timing jitter (1.66 d) gives Pdot = -0.00214 +/- 0.00027. Its wide forecast spread (3-8 d) agrees with all 2022-2025 Swift-UV and optical-rise times (p = 0.26). A re-fit with the Payne et al. 2022 error treatment (0.8 d jitter) gives Pdot = -0.00234 +/- 0.00019. The 2024-2025 flares are 2.1-2.3 sigma late for that re-fit (optical-rise series p = 0.003). In joint fits, a model in which Pdot changes near cycle 23 (2021) is preferred to a constant Pdot by Delta BIC = 4.8 (published + Swift UV only) to 32 (Swift UV + optical rise).
4. **Forecast.** If the 2023-2025 period stays constant, the next optical peaks occur near 2026-11-18 (n = 41), 2027-03-06 (n = 42) and 2027-06-21 (n = 43), with +/- 2 d statistical error. The Payne et al. 2022 model gives 2026-10-18, 2027-01-30 and 2027-05-13. Observations in 2026-2027 can discriminate between these forecasts directly.

We do not claim a physical cause. Possible causes are stochastic changes of the orbit at each pericentre passage (expected for a star that loses mass at each passage), or a change of the drag from the accretion disk. The data do not discriminate between these causes.

## Data

| Data | Coverage | Access | Use |
| --- | --- | --- | --- |
| ASAS-SN Sky Patrol v2 light curve, asas_sn_id 661431833080 (aperture photometry, V 2014-2018, g 2017-2025) | 2014-05-07 to 2025-02-02 | `pyasassn` SkyPatrolClient cone search, RA 81.32558, Dec -46.00583, radius 0.003 deg, deployment 0.6.20 | `files/data/raw/asassn_skypatrol_14ko.csv` (included) |
| Swift/UVOT level-2 sky images (`*_sk.img.gz`), UVW2/UVM2/UVW1, 1112 files from 382 observations (target IDs 00013499 (248 obs), 00037354 (91), 00097093 (40), 00080355 (6), 00033529 (5), 00089761 (1)) | 2020-04 to 2026-02 | HEASARC archive `https://heasarc.gsfc.nasa.gov/FTP/swift/data/obs/<YYYY_MM>/<obsid>/uvot/image/` | not included (5.0 GB); list, URLs and SHA-256 in `files/data/derived/raw_inputs_sha256.csv` |
| TESS FFI cubes, 31 x 31 px cutouts | sectors 4, 5, 6, 31, 32, 33, 87, 98 | `astrocut.cube_cut` on `s3://stpubdata/tess/public/mast/tess-sNNNN-C-C-cube.fits` (anonymous AWS) | not included (0.95 GB); SHA-256 in the same file; derived light curves are included |
| Published peak times | 21 flares, 2014-2021 | Payne et al. 2021 Table 3; Payne et al. 2022 Section III | `files/data/derived/times_published.csv` and `files/code/common.py` |

The TESScut web service returned HTTP 504 on 2026-11-09. For this reason we cut the TESS pixels from the public AWS cubes. The ASAS-SN Sky Patrol v1 service (image subtraction, up to date) requires a reCAPTCHA. We did not use it. We did not have access to ATLAS forced photometry. Thus no ground-based optical data after 2025-02-02 are in this study.

## Method

All code is in `files/code/`. Cycle numbers n follow the Payne et al. 2022 model (n = 0 is the 2014 July flare; n = 24 is the 2021 November flare, the last flare in the Payne et al. 2022 fit).

**ASAS-SN timing (`time_asassn.py`).** We use good-quality points with flux error < 0.5 mJy. For each predicted flare we take the window [prediction - 60 d, prediction + 75 d] and calculate three markers. Each marker has 400 bootstrap draws.
* template time T: a shift of a median flare template. We made the template from the training g-band flares (n <= 24) aligned on the published peak times. The fit has a free amplitude and a linear baseline.
* poly5 peak: the maximum of a 5th-order polynomial within +/- 25 d of T (the Payne et al. method).
* asymmetric profile (Gaussian rise, exponential decay, linear baseline): peak time and half-maximum rise time t_half = tp - sigma_r sqrt(2 ln 2).

**Swift/UVOT photometry (`uvot_phot.py`, `time_uvot.py`).** We use a 5 arcsec aperture on the nucleus and a sky annulus of 60-90 arcsec, outside the host galaxy. We apply the coincidence-loss correction of Poole et al. (2008). We combine the snapshots of each observation, weighted by exposure. We remove visits with a rate below half of the 10th percentile (the nucleus was outside the exposed area). The UV flares have a sharp peak. The peak time is the vertex of a parabola through the visits within +/- 3 d of the brightest visit. We require visits on both sides within 4 d. For cycle 33 the neighbouring visits are 6.5 and 4.5 d away. For that cycle we use the brightest visit with error (gap)/sqrt(12) = 3.2 d.

**TESS photometry (`time_tess.py`).** We use an aperture of r <= 1.6 px and a per-cadence sky from the fainter 60% of pixels in a 4-9 px annulus (the cutouts have no background subtraction). We use QUALITY = 0 and remove cadences with strong scattered light. A sigmoid fit to the rise gives t_half, with errors from a 1-d block bootstrap. The difference image of sector 98 puts the brightening on the nucleus pixel. For the cycle-14 flare, TESS gives t_half = MJD 58430.92 +/- 0.06 and ASAS-SN gives 58430.93 +/- 1.5. Thus the two instruments agree.

**Timing series.** We use these series in the tests:
* `uvpeak`: Swift UVW2 peak, n = 20-33, 11 flares.
* `rise`: half-rise time of flares with a sharp rise (sigma_r < 8 d), ASAS-SN g + TESS, n = 5-38, 14 flares.
* `template`: 17 flares.
* `poly5`: 16 flares.
* `published`: 21 flares.

In 2022-2023 (n = 25-30) the optical flares had a slow rise with early bumps (as reported by Huang et al. 2023, 2025). The template and poly5 markers have a bias for these flares, because their flare shape is different from the template. For this reason we give the most weight to the UV-peak and rise markers. Each series has a constant offset from the published peak scale. We calibrate it as the median difference on the common training cycles 12-24: uvpeak -2.66 +/- 0.28 d, rise -3.93 +/- 0.49 d, template +0.87 +/- 0.38 d.

**Tests (`ephemeris.py`, `payne22_like.py`, `period_evolution.py`, `forecast_next.py`).**
* Forecast test: we fit the quadratic ephemeris to the published n <= 24 peak times with emcee. Then we predict n >= 25 and calculate chi^2 with the full predictive covariance (parameter covariance + jitter + measurement error + offset error).
* Model comparison: constant Pdot, cubic, and broken (two Pdot values, continuous period, scan of the break cycle) for each series and for joint fits with per-series offsets and jitters.
* Local periods: from consecutive well-timed flares (dn <= 4), with a 1 d jitter for each flare time. We fit a line to these periods separately for 2018-2021 and 2021-2025.

## Results

### Out-of-sample offsets from the published Payne et al. 2022 ephemeris

O - C = observed time - estimator offset - Payne et al. 2022 prediction (days):

| n | date | Swift UVW2 peak | optical half-rise | ASAS-SN template |
| --- | --- | --- | --- | --- |
| 27 | 2022-09 | +2.9 | | -4.9 (broad flare) |
| 28 | 2023-01 | +3.0 | | -0.9 (broad flare) |
| 29 | 2023-05 | +3.5 | | |
| 30 | 2023-08 | +4.5 | | |
| 31 | 2023-12 | +5.7 | +6.4 (ASAS-SN) | +8.4 |
| 32 | 2024-03 | (no Swift peak coverage) | +7.8 (ASAS-SN) | +5.6 |
| 33 | 2024-07 | +16.8 +/- 3.2 | | |
| 34 | 2024-10 | | +11.7 (ASAS-SN) | +12.1 |
| 38 | 2025-11 | | +20.8 (TESS S98) | |

In the training period (n = 20-24) the UV-peak O - C has a scatter of 0.23 d. For cycle 33, Swift saw the quiescent level (6.9-7.9 c/s) until MJD 60496, at the time of the predicted UV peak. The peak (17.7 c/s) occurred on MJD 60508.8 (Figure 3b). For cycle 38, TESS saw the rise start near MJD 61033. The rise had the same shape as the cycle-14 rise in 2018, but 17 d later relative to the prediction (Figure 3a).

### Forecast tests of re-fitted constant-Pdot models (training: published n <= 24)

| training fit | Pdot | test series | chi^2 / N | p |
| --- | --- | --- | --- | --- |
| free jitter (1.66 d) | -0.00214 +/- 0.00027 | Swift UV peak | 7.8 / 6 | 0.26 |
| free jitter | | optical rise | 5.2 / 4 | 0.26 |
| jitter 0.8 d (Payne et al. 2022 treatment) | -0.00234 +/- 0.00019 | Swift UV peak | 10.8 / 6 | 0.094 |
| jitter 0.8 d | | optical rise | 16.2 / 4 | 0.003 |
| free jitter | | template / poly5 | 134 / 7, 61 / 7 | < 1e-9 (biased by broad 2022 flares) |

Our re-fits do not give Pdot = -0.0026 exactly. Payne et al. 2022 also used TESS peak times, and we do not have their exact likelihood. A constant Pdot near -0.0021 is not excluded by the forecast test alone. The reason is that the predictive spread of that model at 2025 is +/- 8 d.

### Period evolution (Swift UV peak + optical rise)

| era | number of periods | dP/dn (d/cycle) | Pdot |
| --- | --- | --- | --- |
| 2018-2021 (n_mid <= 24) | 11 | -0.41 +/- 0.09 | -0.0039 +/- 0.0008 |
| 2021-2025 (n_mid >= 24) | 9 | -0.12 +/- 0.06 | -0.0011 +/- 0.0005 |

Mean local period at n_mid >= 28 (7 periods, mean n = 34.6): 107.45 +/- 0.32 d. Payne et al. 2022 model: 105.31 d (chi^2 = 51 for 7 periods). Free-jitter re-fit: 106.38 d (chi^2 = 17). Consecutive periods share one flare time, so these chi^2 values are approximate.

### Joint model comparison (per-series offsets and jitters)

| series | N | BIC constant Pdot | BIC cubic | BIC broken | break cycle | Pdot before -> after |
| --- | --- | --- | --- | --- | --- | --- |
| published + UV + rise | 46 | 232.8 | 217.9 | 212.6 | 23.0 | -0.0026 -> -0.0009 |
| published + UV | 32 | 149.4 | 149.9 | 144.6 | 30.0 | -0.0022 -> +0.018 (one point, n = 33) |
| published + rise | 35 | 188.1 | 185.7 | 180.9 | 22.5 | -0.0027 -> -0.0008 |
| UV + rise | 25 | 120.3 | 87.7 | 88.0 | 20.5 | -0.0033 -> -0.0008 |

The broken model in the published + UV fit has its break at n = 30. Only the single n = 33 point controls that fit, so we do not interpret it. A random-walk-period (Kalman filter) model was also fit (`model_comparison.csv`). The optimizer did not reliably find the nested q -> 0 solution for the template and poly5 series, so we do not use that model.

### Forecast of the next flares (`forecast_next_flares.csv`)

| n | constant 2023-2025 period (peak scale) | with 2021-2025 dP/dn | Payne et al. 2022 |
| --- | --- | --- | --- |
| 39 | 2026-04-18 +/- 1.5 d | 2026-04-17 | 2026-03-25 |
| 40 | 2026-08-03 +/- 1.7 d | 2026-08-02 | 2026-07-07 |
| 41 | 2026-11-18 +/- 1.9 d | 2026-11-17 | 2026-10-18 |
| 42 | 2027-03-06 +/- 2.1 d | 2027-03-04 | 2027-01-30 |
| 43 | 2027-06-21 +/- 2.3 d | 2027-06-18 | 2027-05-13 |

The errors are statistical only. The flare-to-flare timing jitter is 1-3 d, and the period can change again, so the real uncertainty is larger. The half-rise time occurs approximately 4 d before the peak.

## Figures

* `files/figures/fig1_oc_payne22.png`: O - C relative to the Payne et al. 2022 ephemeris for all series.
* `files/figures/fig2_local_period.png`: local period against cycle number, with linear fits for the two eras.
* `files/figures/fig3_light_curve_evidence.png`: light curves aligned on the Payne et al. 2022 predictions. (a) TESS 2018 and 2025 rises. (b) Swift UVW2 for cycles 21, 30 and 33. (c) ASAS-SN g stacks for 2020-2021 and 2023-2024.

## Limitations

* No ground-based optical data after 2025-02-02 are in this study. The 2025 November point comes from TESS only. The 2025 sector-98 light curve ends at MJD 61045.4, before the decline of the flare. Thus we use the rise time and not the peak time.
* Flare shapes changed in 2022-2023 (slow rises, bumps, rebrightenings). A "flare time" is not unique for these flares. We use several markers with constant offsets. If the delay between the true clock (for example, the pericentre passage) and a marker changes with the flare shape, part of the measured drift can come from this change and not from the orbit.
* The estimator offsets come from 5-8 common training flares. Our marker times for 2018-2021 are more precise than the published times. The fits that use our training-era times find a steeper early Pdot (-0.0033 to -0.0039) than the fits that use the published times (-0.0021 to -0.0023). This difference is part of the reason why the evidence for a change depends on the data set.
* Our Swift photometry is a simple aperture photometry and not the HEASoft `uvotsource` pipeline. The rates are relative values. We use them only for timing.
* The early-era (2014-2017) V-band timings are poor, because ASAS-SN had a low cadence then. They do not have an important effect on the 2018-2025 period analysis.
* Local periods share flare times, so the errors in the era comparison are approximate.

## Reproduce

```
uv venv --python 3.12 venv && . venv/bin/activate
uv pip install -r files/code/requirements.txt      # exact versions: files/code/pip_freeze.txt
cd files && mkdir -p raw out fig
cp data/raw/asassn_skypatrol_14ko.csv data/raw/swift_obslist.csv raw/   # or re-download ASAS-SN with pyasassn
bash code/fetch_swift_uvot.sh                       # 1112 files, 5 GB
python code/fetch_tess_s3.py raw/tess_s3            # 8 sectors from the AWS cubes
NBOOT=400 python code/time_asassn.py
python code/uvot_phot.py && python code/time_uvot.py
python code/time_tess.py
python code/ephemeris.py && python code/payne22_like.py
python code/period_evolution.py && python code/forecast_next.py
python code/make_figures.py
```

The scripts read and write `raw/`, `out/` and `fig/` next to the `code/` folder (see `common.py`). Compare the SHA-256 values in `raw_inputs_sha256.csv` to check the inputs. The ASAS-SN Sky Patrol team announced a rebuild of its catalogs in 2026 November, so a new download can differ. Use the included CSV for an exact reproduction.

## Files

* `files/code/`: all analysis code, requirements and pip freeze.
* `files/data/raw/`: ASAS-SN light curve, Swift observation list, Swift download target list.
* `files/data/derived/`: flare-time tables (`asassn_flare_times.csv`, `uvot_flare_times.csv`, `tess_rise_times.csv`, `times_*.csv`), UVOT photometry (`uvot_lc.csv`, `uvot_snapshots.csv`), TESS light curves (`tess_lc_local_sNNNN.csv`), test outputs (`forecast_residuals*.csv`, `payne22_like_*.json/csv`, `model_comparison.csv`, `joint_*.csv`, `ephemeris_summary.json`, `local_periods.csv`, `period_evolution.json`, `forecast_next_flares.csv`), logs, and the SHA-256 list of all raw inputs.

## References

* Payne A. V. et al. 2021, arXiv:2009.03321 (discovery of the periodicity and of Pdot).
* Payne A. V. et al. 2022, arXiv:2206.11278 (the tested ephemeris).
* Payne A. V. et al. 2021b, arXiv:2104.06414.
* Huang S. et al. 2023, arXiv:2310.03236; Huang S. et al. 2025, arXiv:2506.15039 (flare-shape changes, Swift monitoring).
* Linial I. & Quataert E. 2024, arXiv:2309.15849 (period evolution from star-disk interaction).
* Bandopadhyay A. et al. 2024, arXiv:2406.03675; 2026, arXiv:2603.04559 (repeating partial TDE models).
* Poole T. S. et al. 2008, MNRAS 383, 627 (UVOT coincidence loss).
* Hart K. et al. 2023, arXiv:2304.03791 (ASAS-SN Sky Patrol v2).
