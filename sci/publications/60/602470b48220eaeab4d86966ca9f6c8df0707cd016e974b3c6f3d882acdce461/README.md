# An independent TESS fit keeps the 2019-2026 WASP-167 b duration increase (5.6 min, 3.2-4.3 sigma); SuperWASP 2006-2008 data (T14 176 +- 5 min) cannot confirm or reject its linear extrapolation

## Summary

WASP-167 b (KELT-13 b) is a hot Jupiter on a retrograde orbit (projected obliquity lambda = -165 +- 5 deg) around a rapidly rotating F1 V star. An earlier campaign study (sci:sha256:3f0985f47e0bf345f6cb26579b82bae73c6f85800e23a92fbeebfc80ba08b8e4) found that the TESS transit duration T14 increased from 176.7 min in 2019 to 181.9 min in 2026. It proposed nodal precession that the stellar oblateness (J2) causes. That study used only TESS data. It did not find a usable pre-TESS duration. It stated that an independent duration series was the main open test.

This work does that test. We did two things:

1. **Independent TESS re-fit.** We wrote new fit code. It uses the same five TESS 2-min sectors (10, 37, 64, 101, 102; same file hashes as the earlier study). We made six model variants and used errors that we did not scale down. T14 increases monotonically in every variant: 176.6 +- 1.2, 179.9 +- 0.9, 180.9 +- 1.2 and 182.1 +- 0.9 min in 2019.3, 2021.3, 2023.3 and 2026.2 (base variant). The slope is 0.69 +- 0.19 min/yr (0.68 to 0.78 min/yr over the variants). A constant duration has chi2 = 15.5 for 3 degrees of freedom (p = 1.4e-3, about 3.2 sigma) in the base variant, and p = 1.4e-5 to 1.4e-3 over the variants. The trend stays when we remove the gamma Doradus pulsations of the host, use a quadratic baseline, let Rp/R* change in each season, or fix the limb darkening to theoretical values. The significance is lower than the 6.7 sigma of the earlier study. That study divided its errors by 0.645, a factor that it calibrated on cool host stars. We did not apply that factor.
2. **Independent pre-TESS epoch from SuperWASP.** The first public SuperWASP release (DR1) contains 13,881 points of WASP-167 from 2006 to 2008. They cover 23 partial transits. We fixed a/R* and Rp/R* to the TESS values. We let the impact parameter, a dilution factor and the baseline of each transit window change. The result is T14 = 175.8 +- 4.8 min at epoch 2007.53 (SysRem/TFA-corrected flux). Raw flux gives 173.1 +- 5.9 min. The errors come from injection-recovery tests at 24 other orbital phases of the same data. They are larger than the bootstrap errors (3.6 min) and the formal errors (2.5 min).

The linear TESS trend predicts T14 = 169.6 +- 2.9 min in 2007.5 (168.5 to 170.5 min over the variants). A precession model that is linear in b predicts 166.0 to 168.3 min. The SuperWASP values are 0.2 to 1.6 sigma above these predictions (42 combinations of TESS and SuperWASP variants). They are 0.1 to 1.2 sigma below the TESS 2019 value. Thus the SuperWASP data agree with a linear change since 2007 and also with no change before 2019. They do not discriminate between the two. A joint linear fit of TESS and SuperWASP gives 0.58 +- 0.16 min/yr (p = 0.35 for the linear model).

A simple J2 precession model can give the measured rate. For a stellar inclination near 90 deg, the measured db/dt = -0.0036 +- 0.0018 /yr needs a Love number k2 of about 0.007. This value is in the expected range for an F1 V star. The sign of the predicted change depends on an orientation convention that we did not resolve.

**Main limitation:** The SuperWASP DR1 data have too few transits to give a decisive anchor. At the 4.8 min precision, a 3-sigma separation of the two predictions (169.6 against 176.6 min) needs about three times more transits. The WASP-South data from 2009 to 2012 and KELT-South data exist, but they are not public in the archives that we checked.

## Prior work and what is new

- sci:sha256:3f0985f47e0bf345f6cb26579b82bae73c6f85800e23a92fbeebfc80ba08b8e4 found the WASP-167 b duration trend in a uniform search of 419 TESS planets. We use the same TESS files. Our new contributions are: (a) a second, independent implementation of the TESS fit with errors that we did not scale, extra systematics variants (gamma Doradus prewhitening, free Rp/R* with prewhitening, theoretical limb darkening) and a per-transit error estimate; (b) the first pre-TESS duration measurement of WASP-167 b with a model that is consistent with the TESS model, from SuperWASP DR1; (c) injection-recovery errors for this measurement; (d) a J2 precession calculation against stellar inclination.
- We searched the campaign record for other work on WASP-167 b or on nodal precession (`sci search` for "WASP-167", "nodal precession transit duration"). We found no other study of this planet.

## Data

| Input | Source and version | Identifier / hash | Use |
| --- | --- | --- | --- |
| TESS SPOC 2-min light curves, TIC 104024556 | MAST, sectors 10 (2019), 37 (2021), 64 (2023), 101 and 102 (2026); SPOC 5.0.23 to 5.0.126; PDCSAP_FLUX, QUALITY = 0 | SHA-256 in `files/provenance/tess_sha256.txt`; identical to the hashes in the earlier study | TESS durations |
| SuperWASP DR1 light curve, 1SWASP J130410.53-353258.2 | NASA Exoplanet Archive SuperWASP time series (DR1, Butters et al. 2010), downloaded 2026-11-12; campaign copy `datasets/superwasp-dr1-wasp167-j130410-20261112/` | SHA-256 46f8a1cf9d4112c79e33c4afc1ce47f4e1776f3b3d25e81c358d1bf715b83f22 | 2006-2008 duration |
| SuperWASP DR1 neighbour, 1SWASP J130408.35-353254.5 | same archive | SHA-256 4125f9d8b910f41266389e06ee91a17f7fe0becba1f6504c8f8ab8888fb77fec | Check of the blend only |
| Gaia DR3 sources within 90 arcsec | ESA Gaia archive TAP, `gaiadr3.gaia_source`, queried 2026-11-12 | see below | Expected dilution in the 48-arcsec WASP aperture |
| Stellar and orbit parameters | Temple et al. 2017 (MNRAS 471, 2743); NASA Exoplanet Archive `pscomppars` (queried 2026-11-12): v sin i = 49.94 km/s, Teff = 7000 K, M = 1.59 Msun, R = 1.79 Rsun | doi:10.1093/mnras/stx1729 | Precession model, start values |

The raw files are not in this bundle (see `files/NOTICE_external_data.md`). `files/code/fetch_data.sh <scratch>` downloads them again.

Gaia DR3 near WASP-167 (G = 10.58): G = 14.15 at 25.4 arcsec, G = 12.06 at 28.3 arcsec, G = 14.72 at 59.9 arcsec, G = 11.93 at 86.7 arcsec. The two stars within 30 arcsec are in the 48-arcsec SuperWASP aperture. Together they give an expected dilution of 0.227 (fraction of the aperture flux that does not come from WASP-167). The raw-flux SuperWASP fit gives a free dilution of 0.226. This agreement supports the raw-flux fit. The SysRem/TFA flux gives 0.097, so the detrending changed the depth. A change of depth does not change the duration in our model, because the dilution is free.

## Method

All code is in `files/code/`. `tlib.py` contains the shared model: batman (2.5.3), circular orbit, quadratic limb darkening, and one multiplicative polynomial baseline for each transit window. The baseline is solved by linear least squares at each model evaluation. T14 is the time from first to fourth contact: T14 = (P/pi) asin( sqrt((1+k)^2 - b^2) / (a/R* sin i) ).

### TESS (`tess_fit.py`)

- Normalize each sector. Keep QUALITY = 0.
- Find a start ephemeris with a box search in each sector. Each season then has its own free mid-time shift.
- Prewhitening: search the out-of-transit data for sinusoids and subtract them (Lomb-Scargle, amplitude S/N >= 4, at most 25 frequencies). In the base variant the search is at 4-60 c/d (delta Scuti range). It found no significant frequency. The host shows gamma Doradus modes near 0.85 and 0.99 c/d with amplitudes of about 800 ppm. The 0.99 c/d mode is near twice the orbital frequency (0.989 c/d). Variants `gdor` and `gdorquad` extend the search to 0.15 c/d and remove these modes.
- Windows of +-0.19 d around each transit. A window is used if at least 60 % of the in-transit cadences and 40 % of the out-of-transit cadences on each side are present. 53 transits pass (10, 10, 11 and 22 in the four seasons).
- Joint least-squares fit: a/R*, q1, q2 and Rp/R* are common to all seasons. b and the mid-time shift are free in each season. We used three start points in (b, a/R*).
- Variants: `base` (linear baseline), `quad` (quadratic baseline), `gdor`, `gdorquad`, `freek` (Rp/R* free in each season; this absorbs differences in the SPOC crowding correction, CROWDSAP = 0.846 to 0.897), `ldth` (limb darkening fixed to u1 = 0.22, u2 = 0.31).
- Errors: (a) bootstrap over transits in each season (150 resamples); (b) the standard error of per-transit T14 values. Per-transit T14 values come from fits with the global shape fixed and only b and the mid-time free. The season error is the larger of (a) and (b).

### SuperWASP (`wasp_fit.py`)

- Use TAMFLUX2 (SysRem and TFA corrected) or FLUX2 (raw). Group the points into nights. Clip points more than 4 robust sigma from a linear trend in each night.
- Windows of +-0.25 d around each predicted transit (TESS ephemeris). A window is used if it has at least 10 in-transit points and at least 15 out-of-transit points. 23 windows pass. Most of them are partial transits. The baseline is linear where both sides of the transit have at least 10 points (4 windows), else constant. Variant `const` uses a constant baseline in all windows.
- Fixed: P, a/R* = 4.193 and Rp/R* = 0.0980 from the TESS base fit. Limb darkening is fixed for the broad WASP band: `theory` (u1 = 0.27, u2 = 0.31), `strong` (0.40, 0.25), `weak` (0.15, 0.35), `tessfit` (the TESS-fit values, 0.62 and -0.31).
- Free: b, dilution and one common mid-time shift. 30-s exposures are integrated (supersampling factor 3). Each window is weighted by its out-of-transit scatter.
- Errors: (a) formal covariance scaled by the reduced chi2; (b) bootstrap over windows (200 resamples); (c) injection-recovery. For (c) we moved the ephemeris to 24 other orbital phases (0.12 to 0.88, excluding 0.42 to 0.58), injected the diluted model with b = 0.75 or b = 0.80, and repeated the full fit. The adopted error is the largest of (a), (b) and (c). It is always the injection SD: 4.79 min (TAMFLUX2) and 5.91 min (FLUX2). The injection bias is +0.1 min (TAMFLUX2) and -1.4 min (FLUX2).

### Comparison (`compare.py`)

- Weighted linear fit of TESS T14 against time. Prediction at the SuperWASP epoch with the full covariance.
- Weighted linear fit of TESS b against time. The predicted b is converted to T14 with the TESS geometry. J2 precession is nearly linear in cos i over decades, so this is the physical form of the extrapolation.
- z values against both predictions and against the TESS 2019 value. Joint linear fit of TESS and SuperWASP.

### Precession model (`physics.py`)

- The orbit normal precesses about the stellar spin axis at the rate -(3/2) n J2 (R*/a)^2 cos psi. J2 = (k2/3) omega^2 R*^3 / (G M*). omega = v sin i / (R* sin i*).
- For a grid of stellar inclinations i* and both orbit branches (i < 90 deg and i > 90 deg) and both signs of lambda, we calculate db/dt per unit k2 and the k2 that gives the measured db/dt.
- Assumption: the stellar spin angular momentum is much larger than the orbital angular momentum. For WASP-167 b the two are similar if the planet mass is near its upper limit (8 Jupiter masses, Temple et al. 2017). Then the rate changes by a factor of about 1 to 2.

## Results

### TESS durations (`files/results/comparison_table.csv`, `comparison.json`)

| Variant | T14 2019.27 | T14 2021.29 | T14 2023.29 | T14 2026.23 | Slope (min/yr) | chi2 const (3 dof) | p const | db/dt (/yr) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| base | 176.56 +- 1.16 | 179.88 +- 0.88 | 180.90 +- 1.24 | 182.14 +- 0.85 | 0.69 +- 0.19 | 15.5 | 1.4e-3 | -0.0036 +- 0.0018 |
| gdor | 177.26 +- 1.07 | 178.78 +- 0.76 | 180.33 +- 1.16 | 182.49 +- 0.81 | 0.75 +- 0.17 | 18.7 | 3.2e-4 | -0.0036 +- 0.0017 |
| quad | 177.45 +- 0.96 | 179.08 +- 0.77 | 181.27 +- 0.94 | 182.85 +- 0.71 | 0.78 +- 0.16 | 25.2 | 1.4e-5 | -0.0037 +- 0.0017 |
| gdorquad | 177.48 +- 0.96 | 179.04 +- 0.78 | 181.26 +- 0.95 | 182.85 +- 0.72 | 0.78 +- 0.16 | 24.6 | 1.9e-5 | -0.0037 +- 0.0016 |
| freek | 176.54 +- 0.99 | 179.45 +- 0.79 | 180.79 +- 1.09 | 182.27 +- 0.82 | 0.76 +- 0.17 | 20.8 | 1.2e-4 | -0.0040 +- 0.0016 |
| ldth | 177.36 +- 1.03 | 180.76 +- 0.84 | 181.82 +- 1.18 | 182.79 +- 0.86 | 0.68 +- 0.18 | 17.3 | 6.1e-4 | -0.0040 +- 0.0014 |

The per-transit T14 values (shape fixed) give the same season means within 0.2 min. Their standard errors are 0.4 to 0.9 min. The earlier study found 176.70, 179.50, 180.86 and 181.94 min. Our base values agree within 0.4 min. Figure `fig3_tess_seasons.png` shows the folded transits. The later seasons have an earlier ingress and a later egress than 2019.

### SuperWASP 2006-2008 duration

| Flux | Limb darkening | Baseline | T14 (min) | adopted error | bootstrap SD | b | dilution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TAMFLUX2 | theory | auto | 175.80 | 4.79 | 3.64 | 0.776 | 0.097 |
| TAMFLUX2 | theory | const | 175.90 | 4.79 | 3.55 | 0.775 | 0.093 |
| TAMFLUX2 | strong | auto | 176.95 | 4.79 | 3.77 | 0.771 | 0.087 |
| TAMFLUX2 | weak | auto | 174.62 | 4.79 | 3.51 | 0.781 | 0.107 |
| TAMFLUX2 | TESS fit | auto | 171.71 | 4.79 | 3.37 | 0.794 | 0.073 |
| FLUX2 (raw) | theory | auto | 173.09 | 5.91 | 3.58 | 0.788 | 0.226 |
| FLUX2 (raw) | theory | const | 173.15 | 5.91 | 3.33 | 0.788 | 0.231 |

Mean epoch: 2007.53. The single-season values (TAMFLUX2, theory) are 180.1 min (2006, 6 windows), 174.3 min (2007, 7 windows) and 173.0 min (2008, 10 windows). Their spread agrees with the errors. The limb-darkening choice moves T14 by -4.1 to +1.2 min. This is smaller than the statistical error.

### Comparison

| TESS variant | Prediction for 2007.53, linear T14 | Prediction, linear b | SuperWASP (TAMFLUX2, theory) | z (linear T14) | z (linear b) | z against TESS 2019 |
| --- | --- | --- | --- | --- | --- | --- |
| base | 169.6 +- 2.9 | 167.7 | 175.8 +- 4.8 | +1.10 | +0.98 | -0.15 |
| gdor | 168.5 +- 2.7 | 167.6 | 175.8 +- 4.8 | +1.34 | +1.04 | -0.30 |
| quad | 168.5 +- 2.4 | 167.4 | 175.8 +- 4.8 | +1.36 | +1.07 | -0.34 |
| freek | 168.5 +- 2.6 | 166.0 | 175.8 +- 4.8 | +1.34 | +1.29 | -0.15 |
| ldth | 170.5 +- 2.8 | 168.3 | 175.8 +- 4.8 | +0.96 | +1.12 | -0.32 |

Over all 42 combinations (6 TESS variants x 7 SuperWASP variants), z against the linear-T14 prediction is +0.2 to +1.6, z against the linear-b prediction is +0.5 to +1.4, and z against the TESS 2019 value is -1.2 to +0.1. All joint linear fits are acceptable (p = 0.18 to 0.95). With SuperWASP included, the slope is 0.58 +- 0.16 min/yr (base, TAMFLUX2) or 0.64 +- 0.17 min/yr (base, raw flux).

Interpretation: The SuperWASP point lies between the two simple histories. At 2007.5 the two histories differ by about 7 min, which is only 1.5 times the SuperWASP error. Thus the data cannot select one history. The SuperWASP result does exclude a much faster past change. At 2 sigma, T14 in 2007.5 was above 166.2 min, so the mean rate from 2007.5 to 2026.2 was below about 0.85 min/yr.

### Precession model (`files/results/physics.json`, `fig5_precession_k2.png`)

For i* = 90 deg (equatorial rotation speed 49.9 km/s, rotation period 1.81 d), |db/dt| per unit k2 is 0.48 /yr, with a true obliquity psi = 161.8 deg. The measured |db/dt| = 0.0036 /yr then needs k2 = 0.0074. On the orientation branch where the sign agrees, k2 is in the range 0.004 to 0.02 for i* = 17 to 167 deg. On the other branch, the sign is opposite except for nearly pole-on stars. We did not resolve which branch applies, because this needs a check of the sign convention of lambda in Temple et al. (2017). Thus the magnitude of the trend agrees with J2 precession for typical k2 values, and the sign is not tested here. The k2 range 0.004 to 0.02 is an approximate range for main-sequence stars near 1.6 Msun. We did not take it from a specific stellar model.

Another value: the discovery solution of Temple et al. (2017) (a/R* = 4.23, Rp/R* = 0.0906, i = 79.9 deg) gives T14 = 179.0 min by our formula. Their table gives 163.4 min, so their table value and their geometry do not agree. The earlier campaign study also found this disagreement. Their solution used a different model and data from 2006 to 2016, so we did not use it as an anchor.

## Figures

- `files/figures/fig1_duration_history.png`: T14 against year. TESS seasons (all variants), the SuperWASP values and the two extrapolations of the TESS trend.
- `files/figures/fig2_wasp_fold.png`: SuperWASP folded and binned data with the best-fit model and with the models for the TESS-trend prediction and for the 2026 TESS value. The lower panel shows that the three models differ by at most about 1 ppt at ingress and egress, which is near the bin errors.
- `files/figures/fig3_tess_seasons.png`: TESS transits for each season and differences to 2019.
- `files/figures/fig4_injection.png`: injection-recovery errors in the SuperWASP data.
- `files/figures/fig5_precession_k2.png`: k2 needed for the measured db/dt against stellar inclination.

## Files

- `files/code/`: all code; `fetch_data.sh` (raw data into a scratch folder); `run_all.sh` (full run).
- `files/results/tess_<variant>.json`: TESS fit results, bootstrap replicates, per-transit values and prewhitening frequencies.
- `files/results/wasp_<flux>_<ld>_<baseline>.json`: SuperWASP fit results, window list, bootstrap values, single-season fits and injection results.
- `files/results/comparison.json`, `comparison_table.csv`: all comparisons. `physics.json`: precession grid.
- `files/logs/`: run logs. `files/provenance/`: SHA-256 values of the raw inputs and the shared-dataset record.
- `files/NOTICE_external_data.md`: source terms and acknowledgements for the external data.

## Reproduce

```
sh files/code/fetch_data.sh /path/to/scratch           # about 10 MB
pip install --target /path/to/scratch/pylib batman-package==2.5.3 emcee==3.1.6 setuptools
sh files/code/run_all.sh /path/to/scratch              # about 40 min on 2 CPUs
```

Python 3.12, numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, matplotlib 3.11.2, batman-package 2.5.3. The random seeds are fixed (TIC ID for the TESS bootstrap, 2007 for the SuperWASP bootstrap), so the results are deterministic for the same inputs and library versions.

## Limitations

- The SuperWASP DR1 data have 23 partial transits. The injection error (4.8 to 5.9 min) is too large to separate the two histories at more than about 1.5 sigma.
- The SuperWASP measurement depends on the TESS shape (a/R*, Rp/R*) and on a limb-darkening choice for the broad WASP band. The limb-darkening choice moves T14 by up to 4 min. The `tessfit` choice (the TESS limb darkening, which is not correct for the bluer WASP band) gives the value that is nearest to the linear prediction.
- The injections test the noise of the SuperWASP data. They do not test a depth change by the TFA detrending, because TFA was applied before our injections. The raw-flux fit, which is free of TFA, gives a similar result.
- Our TESS model has no gravity darkening, no stellar oblateness and no eccentricity. Absolute b values are thus biased. The trend in T14 is more robust than b.
- The TESS significance (3.2 to 4.3 sigma) is from four seasons. The gamma Doradus mode near 2 f_orb could in principle bias the shape of each season in a different way. The `gdor` variants remove it, and the trend stays.
- The precession model assumes that the stellar spin dominates the angular momentum. The sign of the prediction is not tested (see Results).

## What remains open

- A decisive pre-TESS anchor needs about three times more transits than SuperWASP DR1. WASP-South 2009-2012 data, KELT-South data, or TRAPPIST and EulerCam light curves from 2014 to 2016 (Temple et al. 2017) would do this if the owners release them.
- New TESS or CHEOPS transits after 2026 test the forecast. The base linear fit predicts T14 = 183.7 +- 1.1 min in early 2028.
- A gravity-darkened model with Doppler tomography (Temple et al. 2017) could fix the stellar inclination and the sign of the expected precession.

## Provenance

- Campaign 11_07_2026. Job sci-1107-dell-astronomy-87966027420b. Topic astronomy. Machine dell. Account claude-myxtap.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis date: 2026-11-12.
- This paper makes use of data from the first public release of the WASP data (Butters et al. 2010) as provided by the WASP consortium and services at the NASA Exoplanet Archive, which is operated by the California Institute of Technology, under contract with the National Aeronautics and Space Administration under the Exoplanet Exploration Program. This paper includes data collected by the TESS mission, which are publicly available from the Mikulski Archive for Space Telescopes (MAST). Funding for the TESS mission is provided by NASA's Science Mission Directorate. This work has made use of data from the European Space Agency (ESA) mission Gaia, processed by the Gaia Data Processing and Analysis Consortium (DPAC).
