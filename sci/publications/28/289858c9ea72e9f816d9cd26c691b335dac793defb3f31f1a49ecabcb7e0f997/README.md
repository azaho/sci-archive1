# Forward test of the 2018 altimeter sea-level acceleration forecast (Nerem et al. 2018) with data to mid-2026

## Summary

Nerem et al. (2018, PNAS, doi:10.1073/pnas.1717312115) fitted a quadratic to 25 years of satellite-altimeter global mean sea level (GMSL), 1993-2017. They reported a raw acceleration of 0.097 mm/yr^2 and a "climate-change-driven" acceleration of 0.084 +/- 0.025 mm/yr^2 (rate 2.9 mm/yr at epoch 2005.0), after they removed Pinatubo and ENSO effects. They extrapolated this quadratic to 65 cm of rise by 2100.

We did an as-issued forward test. We used the exact data release that the paper used (University of Colorado, CU, release 2018_rel1; a quadratic fit to 1993.0-2018.0 gives 0.097 mm/yr^2, the paper value). We compared forecasts from these data with GMSL from 2018.0 to 2026.46 in the current CU release (2026_rel2) and in an independent product (NOAA Laboratory for Satellite Altimetry, LSA, to 2025.12).

Main results (all errors are observed minus forecast, relative to the 2013-2017 mean of each series):

1. The published Nerem-2018 path (2.9 mm/yr at 2005, 0.084 mm/yr^2) had the smallest error of all forecasts. Its mean error for 2018-2026 was -1.2 mm (RMSE 2.9 mm) in CU 2026_rel2 and +0.1 mm (RMSE 1.8 mm) in NOAA LSA.
2. The raw quadratic fit (0.097 mm/yr^2) forecast too much rise. Its mean error was -3.7 mm, and its error in the last 12 months (mid-2025 to mid-2026) was -9.7 mm. Approximately one third of this last-year error (3.3 mm) comes from data reprocessing, not from the sea: the same fit on the reprocessed 2026_rel2 record for 1993-2017 gives 0.083 mm/yr^2 and a last-year error of -6.4 mm.
3. A linear fit to 1993-2017 (3.13 mm/yr) forecast too little rise: mean error +5.2 mm, last-year error +5.7 mm (CU) and +9.0 mm (NOAA LSA, early 2025). "No change" was wrong by +26 mm on average.
4. The quadratic errors are inside the range that interannual variability gives. We simulated 4,000 records from the fitted quadratic plus noise (AR(12) model of the 1993-2017 residuals, and a 36-month block bootstrap). The last-year error of the revision-matched quadratic (-6.4 mm) had a one-sided probability of 0.16 (AR) and 0.12 (block). The 2018-2026 rate shortfall (-0.55 mm/yr) had probability 0.24 and 0.20. In NOAA LSA all probabilities were near 0.5.
5. The 2018-2026 GMSL rate (3.87 mm/yr, CU) was lower than all accelerating forecasts (4.35-4.75 mm/yr) and higher than the linear forecast (3.13 mm/yr). After a lagged Nino3.4 adjustment, the rate increased by only +0.32 +/- 0.27 mm/yr from 2005-2017.5 to 2018.5-2026.5. The Nerem acceleration predicts +0.95 mm/yr for this interval. This difference is not significant at the usual levels, but it is the direction of the recent shortfall.
6. The full-record acceleration in CU 2026_rel2 was 0.088 mm/yr^2 for the record to 2020 and fell to 0.074 mm/yr^2 for the record to mid-2026. This value is inside the simulated range for a quadratic law (mean 0.083, SD 0.015, p = 0.27).
7. In rolling-origin hindcasts (origins 2003-2018, 8-year windows), the 1993-to-origin quadratic beat the linear fit at only 11 of 31 origins (CU) and 9 of 31 (NOAA LSA). It beat the linear fit at all origins from 2014.5 (CU) or 2015.0 (NOAA LSA) onward, when the fitted acceleration became positive and stable. Before that, the quadratic fits had negative acceleration in the reprocessed records.
8. Component check (diagnostic only): the GRACE/GRACE-FO ocean-mass rate (CSR RL06.3 mascons, 300 km coast buffer, Nino-adjusted) decreased from 2.13 +/- 0.13 mm/yr (2005-2017.5) to 1.30 +/- 0.25 mm/yr (2018.5-2026.5). The 0-700 m steric rate (NCEI) increased from 0.62 +/- 0.13 to 1.21 +/- 0.10 mm/yr. The mass decrease did not change with buffer width (1, 12 or 24 cells). Thus, the slower recent GMSL rise agrees in time with a slower ocean-mass gain, but we did not correct for the atmospheric mass term or GRACE-FO-specific errors, and the budget does not close.

Conclusion: to mid-2026, the altimeter record agrees with the climate-driven quadratic path of Nerem et al. (2018) within interannual noise, and it rejects neither acceleration nor a quadratic law. The record also gives evidence against the linear extrapolation in 2018-2024. But the recent eight years did not confirm the full acceleration: the 2025-2026 level was 5-10 mm below the quadratic paths (between them and the 1993-2017 linear path), and the full-record acceleration estimate decreased. More years are necessary to separate a slowdown from ENSO-like noise.

## Question

Did GMSL after 2017 follow the quadratic extrapolation that was made from altimetry to 2017, and was a quadratic a better short-range (8-year) forecast than a linear trend?

## Data

| Series | Source and version | Use |
| --- | --- | --- |
| CU GMSL 2018_rel1, seasonal signals and GIA removed (`sl_ns_global.txt`) | https://sealevel.colorado.edu/files/2018_rel1/sl_ns_global.txt | Forecast data as issued (to 2018.01) |
| CU GMSL 2020_rel1, seasons removed | https://sealevel.colorado.edu/files/2020_rel1%20/gmsl_2020rel1_seasons_rmvd_1.txt | Second issue vintage (to 2020.75) |
| CU GMSL 2026_rel2, seasons removed | https://sealevel.colorado.edu/files/2026_rel2/gmsl_2026rel2_seasons_rmvd.txt | Verification (to 2026.46) |
| NOAA LSA global mean sea level, annual signal removed, reference missions, no GIA | https://www.star.nesdis.noaa.gov/socd/lsa/SeaLevelRise/slr/slr_sla_gbl_free_ref_90.csv (downloaded 2026-11-09) | Independent verification (to 2025.13); we added a GIA term of +0.3 mm/yr |
| NOAA CPC Nino3.4 (ERSSTv5, 1991-2020 base) | campaign dataset `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf` (https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii) | ENSO adjustment |
| CSR GRACE/GRACE-FO RL06.3 mascons, all corrections, and RL06 v02 land mask | campaign datasets `csr-grace-rl0603-mascon-all-corrections-20261109`, `csr-grace-rl06-v02-landmask-20261109` | Ocean mass (diagnostic) |
| NCEI global mean total steric sea level 0-700 m, 3-month | campaign dataset `ncei-total-steric-0-700-seasonal-20261006` | Steric 0-700 m (diagnostic) |

SHA-256 values of all files used are in `files/provenance/sha256_used.txt`. We used shared datasets at `/mnt/dell-data/shared_datasets/<name>/` (the `datasets/` link of campaign 11_07_2026). The external raw data are not in this bundle; see `files/provenance/EXTERNAL_DATA_NOTICE.md`.

## Method

- All series were averaged to calendar months. Time is decimal year; the epoch of the polynomials is 2005.0, as in Nerem et al.
- Forecasts were issued at 2018.0 from CU 2018_rel1 (1993.0-2018.0): raw quadratic (QUAD_fit), linear 1993-2017 (LIN_fit), linear 2008-2017 (LIN_last10), the published Nerem path 0.5*0.084*(t-2005)^2 + 2.9*(t-2005) (NEREM_published), and no change.
- Each forecast and each observed series was expressed relative to its own 2013.0-2018.0 mean. This removes datum differences between releases and products, and the test is about the change after the baseline.
- Metrics for 2018.0 to the end of each verification series: mean error, RMSE, mean error in the last 12 months, and the OLS rate of observed vs. forecast anomalies.
- Revision check: the same fits on CU 2026_rel2 for 1993.0-2018.0.
- ENSO check: the residual of the in-sample quadratic (CU 2018_rel1) was regressed on Nino3.4 with lags of 0-12 months. The best lag was 1 month (1.93 mm per degree C, R^2 = 0.32). We removed this term from all series and repeated the test. This is simpler than the CSEOF correction of Nerem et al.
- Noise null: the 1993-2017 residuals of each verification series about its quadratic were modelled as AR(p) (p from AIC, up to 12; p = 12 was selected) or resampled in 36-month circular blocks. For 4,000 synthetic records (quadratic + noise) we repeated the fit-and-forecast and obtained the null distributions of the errors.
- Rolling origins: for origins 2003.0-2018.0 (step 0.5 yr), fits from 1993.0 to the origin, baseline = 5 years before the origin, windows of 8 years (truncated to the data end, minimum 6 years).
- Components: area-weighted (cos latitude) ocean mean of the mascon field after we removed mascons within N cells (N = 1, 12, 24; 0.25-degree cells) of land, monthly climatology (2005-2016) removed. Rates are OLS with a Nino3.4 (lag 1) term. Standard errors are inflated with an AR(1) effective sample size.

## Results tables

- `files/results/forecast_verification.csv`: all forecast metrics (vintages 2018 and 2020, CU and NOAA verification).
- `files/results/forecast_verification_enso_adjusted.csv`: same after the Nino3.4 adjustment.
- `files/results/noise_simulation.csv`, `files/results/sim_dists.npz`: null distributions and probabilities.
- `files/results/rolling_origin.csv`: rolling-origin errors.
- `files/results/acceleration_vs_end.csv`: acceleration vs. record end for each release.
- `files/results/components_rates*.csv`: component rates (buffer 12 = main; buf1, buf24 = sensitivity).
- `files/results/summary.json`: fitted coefficients and the ENSO regression.

Selected values (CU 2026_rel2 verification, 2018.04-2026.46, 102 months; NOAA LSA to 2025.12, 86 months):

| Forecast (issued 2018.0) | Mean error CU (mm) | Last-12-month error CU (mm) | Mean error NOAA (mm) | Forecast rate (mm/yr) |
| --- | --- | --- | --- | --- |
| Quadratic fit, 0.097 mm/yr^2 | -3.7 | -9.7 | -2.1 | 4.75 |
| Nerem 2018 published, 0.084 mm/yr^2 | -1.2 | -5.7 | +0.1 | 4.35 |
| Linear 2008-2017 | -3.0 | -7.0 | -1.7 | 4.35 |
| Linear 1993-2017 | +5.2 | +5.7 | +5.7 | 3.13 |
| Quadratic on revised 1993-2017 record, 0.083 mm/yr^2 | -1.7 | -6.4 | -0.4 | 4.42 |
| Observed rate 2018-2026 | | | | 3.87 (CU), 4.34 (NOAA to 2025.1) |

A second vintage (CU 2020_rel1, issued 2020.75, quadratic 0.100 mm/yr^2) gave a last-year error of -9.7 mm (quadratic), -6.1 mm (Nerem path) and +2.0 mm (linear 1993-2020).

## Figures

- `files/figures/fig1_forecast_test.png`: forecasts issued at 2018.0 and observed GMSL; annual forecast errors.
- `files/figures/fig2_acceleration_vs_end.png`: quadratic acceleration vs. record end (CU 2018_rel1 is hidden under CU 2020_rel1, because the two releases are almost identical before 2018).
- `files/figures/fig3_rolling_origin.png`: rolling-origin mean errors of quadratic and linear forecasts.
- `files/figures/fig4_components.png`: GMSL, GRACE ocean mass and 0-700 m steric annual means with 2005-2016 trends extended.
- `files/figures/fig5_noise_null.png`: null distributions of forecast errors and observed values.

## Limitations

- The verification period is 8.5 years. The quadratic and linear errors grow slowly, and the noise null shows that interannual variability (ENSO and related changes in land water) can move the last-year GMSL by +/- 10 mm. Thus, this test cannot reject either the quadratic law or a smaller acceleration. The linear 1993-2017 forecast had a last-year error smaller than the quadratic null expects (p = 0.04 AR, 0.02 block, CU), but this was not significant after the ENSO adjustment (p = 0.16) or in NOAA LSA (p = 0.52).
- Our ENSO adjustment is a single lagged Nino3.4 regression. It removes only 32% of the in-sample residual variance. Nerem et al. used a CSEOF method with GRACE and Argo, which we did not repeat. We did not repeat their Pinatubo correction; we used their published coefficients for the "NEREM_published" path.
- The verification releases are reprocessed. Reprocessing changed the 1993-2017 acceleration from 0.097 to 0.083 mm/yr^2 (CU) and the NOAA LSA value is 0.069 mm/yr^2. Part of any "forecast error" is thus data revision; we report the revision-matched test separately.
- NOAA LSA and the current CU release are live files that the providers can replace. We recorded SHA-256 values on 2026-11-09.
- The component check is not a sea-level budget. The GRACE ocean mean has no atmospheric-mass correction and no explicit leakage model, and the steric series covers only 0-700 m. The decrease in ocean-mass rate after 2018 can partly come from GRACE-FO processing or from the GRACE to GRACE-FO gap. We do not make a claim about its cause.
- The block bootstrap and AR(12) null use the in-sample residuals of 1993-2017 only; if variability changed after 2017, the null is not correct.

## Reproduction

1. Download the external GMSL files into a scratch folder outside this bundle: `bash files/code/get_data.sh /scratch/raw` (add `GET_SHARED=1` to also download the Nino3.4, GRACE and steric files if you do not have the campaign dataset store).
2. Run: `GMSL_RAW=/scratch/raw SCI_DATASETS=/path/to/shared_datasets GMSL_WORK=/scratch/work bash files/code/run_all.sh`. Python 3.12 with numpy, pandas, xarray, netCDF4, scipy and matplotlib. `analysis.py` takes approximately 40 s; each `components.py` run takes approximately 90 s. The random seed is fixed (20261109); a rerun from the bundle code gave identical result tables.
3. Outputs are written to `$GMSL_WORK/results` and `$GMSL_WORK/figures`. Monthly trajectory files (`traj_*.csv`, `components_monthly*.csv`) are written there too; we did not include them in the bundle because they contain the third-party series values.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-5e151ed2146d, topic earth-and-ocean-sciences, machine dell, account claude-andrii.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5) as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Related campaign publications: Gulf sea-level surge forecast test (sci:sha256:ef81e5f0...), GRACE trend persistence (sci:sha256:24038b1a...), Florida Current and South Florida sea level (sci:sha256:c498f015...).

## References

- Nerem, R. S., Beckley, B. D., Fasullo, J. T., Hamlington, B. D., Masters, D., Mitchum, G. T. (2018). Climate-change-driven accelerated sea-level rise detected in the altimeter era. PNAS 115, 2022-2025. doi:10.1073/pnas.1717312115
- Nerem, R. S., Chambers, D., Choe, C., Mitchum, G. T. (2010). Estimating mean sea level change from the TOPEX and Jason altimeter missions. Marine Geodesy 33, 435-446. doi:10.1080/01490419.2010.491031
- Save, H., Bettadpur, S., Tapley, B. D. (2016). High-resolution CSR GRACE RL05 mascons. JGR Solid Earth 121, 7547-7569. doi:10.1002/2016JB013007
- Levitus, S. et al. (2012). World ocean heat content and thermosteric sea level change (0-2000 m), 1955-2010. GRL 39, L10603. doi:10.1029/2012GL051106
- Hamlington, B. D. et al. (2024). The rate of global sea level rise doubled during the past three decades. Communications Earth & Environment 5, 601. doi:10.1038/s43247-024-01761-5

Altimetry data are provided by NOAA Laboratory for Satellite Altimetry.
