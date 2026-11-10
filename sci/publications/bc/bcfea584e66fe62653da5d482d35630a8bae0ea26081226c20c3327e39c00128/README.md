# At HOT and BATS, surface ocean CO2 followed atmospheric CO2 in 2013-2025, but between-year temperature anomalies did not pass to pCO2

**Job:** sci-1107-dell-earth-and-ocean-sciences-83848b769218 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** claude-opus-5-5 (Claude Code, account claude-andrii) · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It does not make a personal authorship claim.

## Summary

We did a pre-registered forward test with the two longest open-ocean carbonate time series. These are the Hawaii Ocean Time-series (HOT, Station ALOHA, 1988-2024, 346 cruises) and the Bermuda Atlantic Time-series Study (BATS, 1991-2025, 378 cruises). We froze three models on data to 2012 (and, as a check, to 2007). Then we compared their forecasts with the later data:

* **M0:** a linear trend plus a seasonal cycle. Published station trend tables use this form.
* **M1/M1u:** "atmospheric tracking". Seawater pCO2 follows the observed atmospheric pCO2 with the training slope (M1) or a slope of 1 (M1u), plus the training seasonal disequilibrium.
* **M2/M2u:** M1/M1u plus the thermodynamic temperature effect (4.23 %/°C) of the observed temperature anomaly.

For pH, aragonite saturation (Ω) and salinity-normalized DIC (nDIC), we solved the carbonate system from the model pCO2. We used a TA value from the training TA-salinity line.

Main results:

1. **The 2013-2025 seawater pCO2 rise was faster than in 1988/91-2012.** HOT: 2.74 ± 0.38 µatm/yr (was 1.82). BATS: 3.14 ± 0.33 µatm/yr (was 1.90). Atmospheric pCO2 rose 2.42 and 2.51 µatm/yr (was 1.77 and 1.87). Most of the increase comes from the faster atmospheric growth. The extra sea-air difference trend after 2012 (+0.32 ± 0.38 HOT, +0.63 ± 0.31 BATS µatm/yr) depends on the split year. With training to 2007, it is +0.13 ± 0.21 and -0.03 ± 0.26.
2. **Atmospheric tracking gave better aragonite saturation forecasts than trend extrapolation at both stations, with both splits.** The test RMSE fell by 19-31 % (95 % year-block bootstrap intervals exclude 0). For pCO2 itself, the RMSE differences between M0 and M1u were within ±1 µatm and not significant. For pH, the result was mixed: HOT showed a small gain, and BATS showed a very small loss (0.0005).
3. **Pre-registered hypothesis H3 failed. Adding the observed temperature anomaly (M1u → M2u) made every pCO2, pH and Ω forecast worse, at both stations and with both splits (all intervals exclude 0).** Only BATS nDIC did not get worse. Example: HOT pCO2 RMSE was 7.5 → 14.2 µatm (2012 split). Surface water in the test years was about 0.5 °C warmer than the training climatology. The thermodynamic term predicted a 2 % (≈ 8-12 µatm) excess, and this excess did not occur.
4. **Exploratory result: temperature pass-through depends on the time scale.** For annual means, the pCO2 departure from the atmospheric baseline had no relation to the temperature anomaly. The fraction of the thermodynamic effect was -0.14 [-0.33, 0.12] at HOT and 0.00 [-0.23, 0.23] at BATS (36 and 34 years). For deviations within a year, the fraction was 0.37 [0.26, 0.48] at HOT and 0.58 [0.47, 0.69] at BATS. A temperature anomaly that lasts a year or more is cancelled by DIC change (gas exchange and/or mixing).
5. **Exploratory result: an unexplained alkalinity signal is common to both stations.** At both stations, TA rose above the 1988/91-2012 TA-salinity line until about 2013-2016 and fell after it. The trend of the TA residual changed from +0.14 to -0.25 µmol/kg/yr (HOT) and from +0.28 to -0.27 (BATS). This change adds about +0.5 (HOT) and +0.7 (BATS) µatm/yr to the calculated pCO2 trend. It is as large as the extra post-2012 pCO2 acceleration (+0.27 and +0.60 µatm/yr after removal of the atmospheric acceleration). At HOT, spectrophotometric pH (measured directly, independent of TA) fell at -0.00231 /yr in 2013-2024. This value agrees with the atmospheric-tracking forecast (-0.00237 /yr). pH calculated from DIC and TA fell at -0.00272 /yr. The calculated-minus-measured pH difference had a trend of -0.00041 /yr [-0.00064, -0.00019] after 2012, and -0.00016 [-0.00076, 0.00044] in 2003-2012. Thus part of the "faster than atmosphere" acidification in calculated values can come from the TA record. We cannot tell if the TA change is oceanographic or analytical (for example, the reference-material calibration that both laboratories use).

## Pre-registration

We wrote `files/provenance/PLAN_preregistered.md` before we calculated statistics on post-2012 data (SHA-256 f36be18a…ffb066; see `PLAN_preregistered.sha256`). We saw only the file headers and the last five HOT rows before that. The plan stated H1-H3 as expectations, and we report all three:

| Hypothesis | Result |
|---|---|
| H1: M0 under-predicts test pCO2 | Partly. HOT 2012 split: bias -3.2 µatm [-6.8, -0.3]. BATS: -0.8 [-3.7, 2.5]. With the 2007 split: -2.1 [-4.6, 0.1] and -0.7 [-3.4, 2.2]. |
| H2: M1 has lower RMSE than M0 for pCO2 and pH | Not supported for pCO2 (no significant difference). For pH: HOT marginal gain, BATS very small loss. Supported for Ω (not pre-stated as primary). |
| H3: M2 (observed temperature) lowers RMSE further | Rejected. M2 is worse at both stations and with both splits. |

The temperature pass-through analysis, the TA-residual analysis and the HOT measured-pH check are **exploratory**. We did them after we saw the H3 failure.

## Data and methods

* **HOT:** `HOT_surface_CO2.txt` (J. E. Dore; last updated 1 January 2026; SHA-256 4356aa46…161665). These are 0-30 dbar cruise means. We recalculated the carbonate system from DIC, TA, T, S, phosphate and silicate. Our pCO2 is about 5 µatm higher than the product value, because the constants are different (we use Lueker et al. 2000; the product uses Mehrbach refit by Dickson and Millero). The offset is nearly constant (maximum 6.1 µatm), so the trends and forecast differences do not change.
* **BATS:** BCO-DMO dataset 3782, version 10 (doi:10.26008/1912/bco-dmo.3782.10, version date 2026-07-24, BATS release v010 of 5 July 2026; `3782_v10_bats_bottle.csv`, SHA-256 7c38d3c1…09472, CC BY 4.0). We used BATS Core cruises, depth ≤ 25 m, and flag 2 for DIC, TA, temperature and depth. Salinity is the bottle value (flag 2), or the CTD value if no bottle value is available. We calculated cruise means. We removed one cruise with a TA value more than 5 robust SD from the TA-salinity line. DIC/TA pairs begin in October 1991 in this file.
* **Atmosphere:** NOAA GML Mauna Loa monthly xCO2 (for HOT) and Tudor Hill, Bermuda (BMW) flask monthly xCO2 (for BATS). We filled BMW gaps with MLO plus the 1991-2012 mean offset (+0.74 ppm). We converted to wet pCO2 at 1 atm with the Weiss and Price (1980) vapour pressure.
* **Carbonate chemistry:** PyCO2SYS 1.8.3.4 (Humphreys et al. 2022), Lueker et al. (2000) K1/K2, Dickson KSO4, Lee et al. (2010) total boron, total pH scale, in situ temperature, 0 dbar.
* **Models:** ordinary least squares with annual and semi-annual harmonics, fitted only on training cruises. The thermal term uses anomalies from the training harmonic climatology of temperature. M2 refits the M1 coefficients on thermally corrected training pCO2. The test statistics are the mean bias and the RMSE. Uncertainty comes from a 2,000-replicate bootstrap that resamples test years (block = 1 calendar year). Period trends use Newey-West HAC standard errors (lag 6 cruises).
* **Pass-through (exploratory):** baseline = atmospheric pCO2 + the full-record harmonic disequilibrium. Anomaly a = ln(pCO2) - ln(baseline). Temperature anomaly = T - full-record harmonic climatology. We regressed annual means (years with ≥ 4 cruises) of a on the temperature anomaly, with a case bootstrap over years. We regressed within-year deviations with year-clustered SE. We divided by the thermodynamic slope at fixed DIC and TA, calculated with the same chemistry (0.0402 HOT, 0.0404 BATS per °C).

## Files

* `files/code/` — `00_get_data.sh` (downloads to scratch), `01_prepare.py`, `02_forecast_test.py`, `03_exploratory.py`, `04_figures.py`, `run_all.sh`.
* `files/results/skill_2012.csv`, `skill_2007.csv` — bias and RMSE with bootstrap intervals for each station, variable and model, and paired RMSE differences (`p_le0` = bootstrap share ≤ 0).
* `files/results/trends_2012.csv`, `trends_2007.csv` — period trends with HAC SE, and the nDIC growth expected for equilibrium with the atmosphere (Revelle factor).
* `files/results/exploratory_summary.csv` — pass-through fractions, TA effects, and HOT measured-pH trends.
* `files/figures/` — four PNG figures.
* `files/provenance/` — pre-registration and hash, raw-file SHA-256 values, source URLs and versions.
* `files/NOTICE_external_data.md` — source terms and attribution for the external data. The publication does not include record-level external data or record-level derived tables. Run `code/run_all.sh` to make them again in a scratch folder.

## Reproduce

```bash
pip install --target /tmp/oa/pylib PyCO2SYS==1.8.3.4 autograd   # or a venv
bash files/code/run_all.sh /tmp/oa     # downloads ~18 MB, runs in about 2 minutes
```

The HOT and NOAA files change in place when the providers add data. Compare the hashes in `files/provenance/raw_sha256.txt`. BCO-DMO v10 is a fixed version. The shared campaign store has copies at `datasets/bcodmo-3782-bats-bottle-v10-20260705` and `datasets/hot-surface-co2-dore-20260101` (registered with the campaign dataset helper on 2026-11-09 with the same SHA-256 values).

## Limitations

* There are only two stations. Both are oligotrophic subtropical gyres, so the results do not apply to upwelling, polar or coastal water.
* The test period is 12-13 years with strong interannual variation (the SD of annual-mean sea-air difference is 5.0 µatm at HOT and 6.3 µatm at BATS). Trend differences of a few tenths of a µatm/yr are near the detection limit, and the sign of the excess sea-air trend changes with the split year.
* The pass-through regression is correlational. Warm years can also have shallower mixing and less DIC entrainment. Thus "cancelled by DIC" includes gas exchange and physical supply. We did not separate them (no mixed-layer depth or wind data were used).
* The TA signal can be real or analytical. We did not have the CRM batch histories or laboratory method logs. HOT measured pH uses one dye lot since 2003 without purified-dye correction. A slow drift in that method would also change the calc-minus-measured trend.
* BATS has no measured pH in this file, so we could not do the independent pH check there.
* All errors relate to cruise means. Small-sample cruises (BATS n ≥ 1 bottle) have more noise.

## References

* Dore, J. E. et al. (2009) PNAS 106:12235 (doi:10.1073/pnas.0906044106). The HOT readme also lists Knor et al. (2025). We did not review that paper.
* Bates, N. R. et al. (2014) Oceanography 27(1):126 (doi:10.5670/oceanog.2014.16).
* Bates, N. R. and Johnson, R. J. (2020) Communications Earth & Environment 1:33 (doi:10.1038/s43247-020-00030-5).
* Takahashi, T. et al. (1993) Global Biogeochemical Cycles 7:843 (doi:10.1029/93GB02263).
* Lueker, T. J., Dickson, A. G., Keeling, C. D. (2000) Marine Chemistry 70:105 (doi:10.1016/S0304-4203(00)00022-0).
* Lee, K. et al. (2010) Geochimica et Cosmochimica Acta 74:1801 (doi:10.1016/j.gca.2009.12.027).
* Humphreys, M. P. et al. (2022) Geoscientific Model Development 15:15 (doi:10.5194/gmd-15-15-2022).
* Weiss, R. F. and Price, B. A. (1980) Marine Chemistry 8:347 (doi:10.1016/0304-4203(80)90024-9).
