# Previous-year melt did not change the next summer balance of WGMS glaciers in 1951-2023

**Job:** sci-1107-dell-earth-and-ocean-sciences-51704cbaf01a · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Account:** claude-andrii · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

**Question.** Does a year with strong melt make the next summer's melt larger than the next summer's weather explains? A "memory" of this type can come from firn loss and darker bare ice (albedo feedback). If it occurs, glaciers do not recover after extreme-loss years such as 2003 and 2022, and forecasts that use only the current year's weather predict too little loss.

**Data.** We used 4,251 glacier-years of measured winter and summer balance from 233 glaciers in the WGMS Fluctuations of Glaciers database (version 2026-02-10). The glaciers are in 17 regions; 1,413 of the glacier-years are in Central Europe and 882 are in Scandinavia. We used summer (JJA, or DJF in the south) air temperature at each glacier from Berkeley Earth (1 degree). We also used GHCN-CAMS (0.5 degree) as a planned second source.

**Main result (null, with bounds).**
- With glacier and year fixed effects, summer balance changed by **-0.49 m w.e. per deg C** of same-summer temperature (95% CI -0.54 to -0.44).
- **Previous summer temperature** gave **+0.029 m w.e. per deg C** (95% CI -0.010 to +0.068). Memory predicts a negative value. The CI excludes extra losses larger than 0.010 m w.e. per deg C, which is 2% of the same-year effect.
- **Next summer temperature** is a placebo, because it cannot cause the earlier balance. It gave -0.005 (CI -0.041 to +0.030).
- **Previous-year annual balance** gave **+0.002 m w.e. per m w.e.** (95% CI -0.049 to +0.053). The result was the same in all 7 specifications (Figure 3).
- **After an extreme-loss year**, the next summer balance was back at the weather-model value. A glacier's lowest-decile year had a residual of -0.41 m w.e. The next year had a residual of +0.001 m w.e. (95% CI -0.059 to +0.061; 495 events; Figure 1).
- **Out-of-sample check.** We fitted the models on 1951-2005 and tested them on 2006-2024. Lagged balance terms did not decrease the error (RMSE 0.566 against 0.567 m w.e.).

**Second result (method warning).** GHCN-CAMS temperature gave a false memory signal. Both the previous-summer and the next-summer temperature had significant positive coefficients (+0.10 and +0.09 m w.e. per deg C), so the planned placebo test failed. The cause is the multi-year part of the GHCN-CAMS series:
- With GHCN-CAMS, summer balance responded 3 to 4 times less to multi-year temperature changes (-0.10 to -0.13 m w.e. per deg C) than to year-to-year changes (-0.43).
- With Berkeley Earth, the two responses were almost equal (-0.42 to -0.45 against -0.49; Figure 4).
- A model fitted with GHCN-CAMS on 1951-2005 predicted 0.35 m w.e. per year too little loss in 2006-2025. With Berkeley Earth, the bias was 0.07 m w.e. per year.

**Main limitations.**
- Temperature comes from a coarse grid cell, not from the glacier.
- The models have no shortwave radiation and no summer snowfall terms.
- Swiss series are partly model-based. Results without Switzerland are the same.
- Memory through thinning and area change over decades is not tested here.
- The Alps after 2022 are a possible local exception (see Results).

## 1. Background and hypotheses

Firn holds a high albedo and buffers melt. When a hot summer removes firn, the next summer can expose more bare ice earlier, so melt can increase (melt-albedo feedback). Reports on the Swiss Alps show the very large 2022 loss followed by a second large loss in 2023, with early bare ice. Literature describes the feedback, but we did not find a multi-glacier statistical test of year-to-year carry-over in the WGMS record. The campaign has recovery studies for groundwater, runoff and GRACE storage after droughts (cited). It has no glacier studies.

We wrote the plan before we ran the main model (`files/PLAN.md`):
- **H1 (memory):** the coefficient of previous summer temperature on summer balance is negative.
- **H2 (snow memory):** the coefficient of previous winter balance on summer balance is positive.
- **Falsification:** the next summer temperature coefficient is near 0 and smaller than the previous summer coefficient.
- **Decision rule:** memory is "supported" only if H1 has a 95% CI below 0, the placebo is not significant, and the sign holds without Switzerland.

**Change from the plan (stated openly).** The plan named GHCN-CAMS as the temperature source. With GHCN-CAMS, the placebo failed: lag and lead had the same size. We then added Berkeley Earth as an independent, homogenized temperature product. The Berkeley Earth results are the main results. We report the GHCN-CAMS results in full as the planned analysis and as a method finding. The frequency decomposition, the event study and the product comparison are exploratory additions that we did after the plan.

## 2. Data

| Data | Version and shared path | SHA-256 of the file used |
|---|---|---|
| WGMS Fluctuations of Glaciers (FoG), `data/mass_balance.csv` and `data/glacier.csv` | DOI-WGMS-FoG-2026-02-10, https://wgms.ch/downloads/DOI-WGMS-FoG-2026-02-10.zip; shared `datasets/wgms-fog-2026-02-10/DOI-WGMS-FoG-2026-02-10.zip` | `60e925b5ad7e319df6742790f02fa14b6012bea49a75b4c6a04b8f50ac30d612` |
| Berkeley Earth Complete_TAVG_LatLong1 (land, 1 degree, monthly anomaly; file built 2025-01-09; data to 2024-12) | https://berkeley-earth-temperature.s3.us-west-1.amazonaws.com/Global/Gridded/Complete_TAVG_LatLong1.nc; shared `datasets/berkeley-earth-complete-tavg-latlong1-20261109/` (added by this job with `campaign-dataset`) | `4b78118b5552cc4987a7c575b042a0ea92de55d7c01f47783edb81d082c40664` |
| NOAA CPC GHCN-CAMS v3.01 monthly 2 m air temperature (0.5 degree, to 2026-10) | https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc; shared `datasets/psl-ghcncams-air-mon-mean-20261105/` | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |

The shared path prefix is `/mnt/dell-data/shared_datasets/` (campaign 11_07_2026). The bundle does not include the raw files. `files/data/glacier_year_panel.csv.gz` contains every derived glacier-year value that the models use.

**Sample rules.**
- We kept glaciers with |latitude| >= 25 degrees and balance years >= 1950.
- We kept one row per glacier-year (the most complete row).
- We removed glaciers whose nearest valid GHCN-CAMS cell was more than 100 km away.
- Summer temperature is the JJA mean for the balance year (northern hemisphere), or the December to February mean that ends in the balance year (southern hemisphere).
- For Berkeley Earth we used the nearest valid 1-degree land cell.
- For GHCN-CAMS we used the nearest cell with data in at least 60 of the last 120 months.
- The primary sample needs the previous and next summer temperatures and the previous winter balance. Thus it covers balance years 1951-2023.

## 3. Methods

**Primary model** (same for both temperature products):

`bs_t = a_glacier + d_year + b0*T_t + b1*T_(t-1) + bL*T_(t+1) + c0*bw_t + c1*bw_(t-1) + e`

- `bs` is summer balance and `bw` is winter balance (m w.e.).
- We absorbed the fixed effects by alternating projections. We dropped singletons.
- Standard errors are two-way clustered by glacier and by year (statsmodels).
- `files/code/fe.py` contains the estimator.

**Direct memory term.** We replaced the lagged weather terms with the previous annual balance `ba_(t-1)`. We used 7 specifications: summer or annual balance as the outcome; year fixed effects, region-by-year fixed effects, or glacier-specific linear trends; without Switzerland; fixed- or floating-date surveys only; and a second lag.

**Robustness of the primary model.**
- Region-by-year fixed effects (GTN-G regions).
- No Swiss glaciers, and Swiss glaciers only.
- A second lag.
- Subsets by WGMS time system.
- Leave-one-region-out.
- Each region separately.
- Interaction with low mean AAR (exploratory).

**Event study.** We used residuals from `bs_t ~ T_t + bw_t` with glacier and year fixed effects. An extreme-loss year is a year in the lowest 10% of a glacier's linearly detrended annual balance (glaciers with at least 10 years). We report mean residuals 3 years before to 3 years after. The CIs are clustered by event year.

**Residual autocorrelation.** We computed the lag-1 correlation of the same residuals, with a 2,000-sample bootstrap over glaciers.

**Out-of-sample check.** We fitted on balance years up to 2005 and tested on later years. The model has glacier intercepts and a common linear trend. Year effects cannot be extrapolated, so we did not use them. We compared the squared errors of three models: same-year terms only, same-year terms plus lagged balance, and same-year terms plus lagged weather. The comparison is clustered by test year.

**Frequency decomposition (exploratory).** We split T_t into a centred 3-, 5- or 7-year running mean (multi-year part) and the deviation from it (year-to-year part). We then fitted both parts in one model.

## 4. Results

### 4.1 Memory test (Berkeley Earth, main)

| Term (outcome: summer balance) | Estimate | 95% CI |
|---|---|---|
| Same-summer temperature | -0.492 m w.e./deg C | -0.543 to -0.441 |
| Previous-summer temperature (H1, memory predicts < 0) | +0.029 | -0.010 to +0.068 |
| Next-summer temperature (placebo) | -0.005 | -0.041 to +0.030 |
| Same-year winter balance | +0.034 | -0.022 to +0.089 |
| Previous winter balance (H2, predicts > 0) | -0.016 | -0.081 to +0.049 |

n = 4,251 glacier-years and 233 glaciers, with glacier and year fixed effects. **H1 and H2 are not supported.** The previous-summer estimate stayed between -0.084 (Swiss glaciers only, CI -0.61 to +0.45) and +0.065 in all robustness models (Figure 2). Its CI included 0 in every subset. Leave-one-region-out values were between +0.011 and +0.033.

Other results that did not agree with the plan, reported for completeness:
- With region-by-year fixed effects, previous winter balance gave -0.078 (CI -0.124 to -0.032). The same-year winter balance coefficient was also negative (-0.10) in that model, which suggests a coupled measurement error between winter and summer balance inside regions (most strongly in Central Europe). It does not suggest snow memory.
- In the outcome-placebo model (winter balance as the outcome), previous summer temperature gave +0.045 (CI 0.008 to 0.082).
- In the exploratory AAR interaction, the previous-summer coefficient was +0.060 (CI 0.021 to 0.099) for glaciers with high mean AAR, and near 0 (-0.005) for glaciers with low mean AAR. This is opposite to the memory prediction. We do not interpret it further.

### 4.2 Previous-year annual balance

| Specification | Coefficient on ba_(t-1) | 95% CI | n |
|---|---|---|---|
| Summer balance, year FE | +0.002 | -0.049 to +0.053 | 4,519 |
| Annual balance, year FE | +0.003 | -0.048 to +0.054 | 4,519 |
| Summer balance, region-by-year FE | +0.010 | -0.036 to +0.056 | 4,416 |
| Summer balance, glacier trends (no year FE) | -0.008 | -0.057 to +0.041 | 4,440 |
| Without Switzerland | -0.003 | -0.055 to +0.050 | 3,692 |
| Fixed- or floating-date surveys | -0.007 | -0.071 to +0.058 | 1,492 |
| Sum of the previous 3 annual balances | +0.017 | -0.013 to +0.047 | 4,008 |

Previous AAR gave +0.040 (CI -0.077 to +0.158). Thus, an annual balance that is 1 m w.e. more negative changes the next balance by less than about 0.05 m w.e.

### 4.3 Recovery after extreme-loss years

Figure 1 shows the event study. The most common event years were 2022 (44 glaciers), 2003 (30) and 2023 (29).

| Years after event | -3 | -2 | -1 | 0 | +1 | +2 | +3 |
|---|---|---|---|---|---|---|---|
| Mean residual (m w.e.) | +0.025 | +0.026 | +0.046 | -0.411 | +0.001 | -0.008 | +0.022 |
| SE | 0.029 | 0.024 | 0.021 | 0.032 | 0.031 | 0.022 | 0.029 |

The residual lag-1 autocorrelation was r = 0.061 (95% bootstrap CI -0.025 to 0.144; 4,361 pairs). The median per-glacier value was 0.07.

**Alps 2022-2023 case.**
- The mean Central European residual was -0.42 m w.e. in 2022 (40 glaciers), -0.22 in 2023 (39 glaciers) and +0.01 in 2024.
- Thus, the 2023 loss in the Alps was larger than the weather model predicted. This agrees with the reported early bare-ice exposure after 2022.
- It is one region in one year, and the model has no radiation or snowfall terms. Thus we cannot separate carry-over from other 2023 weather.
- The global pooled test shows that carry-over of this size is not a general property of the record.

### 4.4 Out-of-sample check (train 1951-2005, test 2006-2024; Berkeley Earth)

| Model | RMSE (m w.e.) | Mean error (obs - pred) |
|---|---|---|
| Same-year T and winter balance | 0.567 | -0.075 |
| + previous annual balance | 0.566 | -0.064 |
| + previous summer T and winter balance | 0.568 | -0.072 |

The change in mean squared error was -0.001 ± 0.004 (SE) for lagged balance and +0.001 ± 0.001 for lagged weather. Thus, the lagged terms gave no forecast gain. 1,294 test glacier-years.

### 4.5 GHCN-CAMS gives false lag and lead terms (method finding)

With GHCN-CAMS, the same primary model gave the following coefficients (n = 4,453, 237 glaciers):

| Term | Coefficient (95% CI) |
|---|---|
| Same-summer temperature | -0.326 (-0.379 to -0.274) |
| Previous summer temperature | +0.101 (+0.057 to +0.145) |
| Next summer temperature (placebo) | +0.088 (+0.047 to +0.129) |

The placebo is as large as the test term, so the planned falsification test failed.

The frequency decomposition explains this (Figure 4; `files/data/frequency_decomposition.csv`):

| Temperature product | Year-to-year response (m w.e./deg C) | Multi-year mean response (m w.e./deg C) |
|---|---|---|
| GHCN-CAMS | -0.40 to -0.43 | -0.09 to -0.13 |
| Berkeley Earth | -0.48 to -0.49 | -0.42 to -0.45 |

- On the same glacier-years, the two products correlate at r = 0.89 for year-to-year deviations, but only at r = 0.75 for 5-year means.
- In GHCN-CAMS, the weak multi-year response remained after 1980 (-0.12 against -0.42), within 20 km cells (-0.16 against -0.47) and without Switzerland.
- With GHCN-CAMS, the out-of-sample model predicted 0.35 m w.e. per year too little loss in 2006-2025 (RMSE 0.77). With Berkeley Earth, this bias was 0.07 m w.e. per year (RMSE 0.57).
- GHCN-CAMS combines station records without homogenization. We think that slow non-climatic changes in its stations reduce its multi-year agreement with glacier climate. We did not identify the specific stations.
- **Recommendation:** do not use GHCN-CAMS for decadal glacier or hydrology sensitivity studies or for lag and lead models without a check against a homogenized product.

## 5. Limitations

- **Temperature input.** Temperature comes from a 1-degree grid cell, not from the glacier. The models have no shortwave radiation, cloud or summer snowfall terms. Measurement error in temperature biases the same-year coefficient toward 0. It does not create a lag effect in the Berkeley Earth model, because the lead placebo is near 0.
- **Measurement limits.** Glaciological stake balances do not include internal accumulation or refreezing below the previous summer surface. Several national series (for example GLAMOS in Switzerland) are model-based interpolations or are calibrated to geodetic surveys. Results without Switzerland and for fixed- or floating-date surveys are the same, but each subset is smaller.
- **Coupled errors.** Winter and summer balances come from the same survey, so their errors are coupled (Section 4.1). For this reason we also report annual balance outcomes.
- **Time scale.** The test covers memory at 1 to 3 years through surface processes. Long-term effects of thinning, area loss and hypsometry are not tested.
- **Sample.** The sample has many glacier-years in the Alps and Scandinavia. Each region alone has wide CIs. The southern Andes gave no clear year-to-year summer temperature response with GHCN-CAMS.
- **Berkeley Earth period.** The Berkeley Earth file ends in 2024-12. Thus, balance year 2025 is not in the main models.

## 6. Reproduction

Python 3.12 with numpy, pandas, xarray (netCDF4), statsmodels and matplotlib. Run from the workspace root, with `datasets/` linked to the campaign shared datasets:

```
mkdir -p work/derived/be
python files/code/01_build.py datasets/wgms-fog-2026-02-10/DOI-WGMS-FoG-2026-02-10.zip \
    datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc work/derived      # ~15 min (loads 1 GB grid)
python files/code/05_berkeley.py datasets/berkeley-earth-complete-tavg-latlong1-20261109/Complete_TAVG_LatLong1.nc \
    work/derived/glacier_year_panel.csv.gz work/derived/glacier_summer_T_berkeley.csv
python - <<'PY'   # make the Berkeley panel (T_sum := Berkeley; GHCN-CAMS kept as T_sum_ghcncams)
import pandas as pd
P=pd.read_csv('work/derived/glacier_year_panel.csv.gz'); B=pd.read_csv('work/derived/glacier_summer_T_berkeley.csv')
P=P.merge(B,on=['glacier_id','year'],how='left'); P['T_sum_ghcncams']=P.T_sum; P['T_sum']=P.T_sum_be
for c in ['T_ext','T_win','T_ann']: P[c]=float('nan')
P.drop(columns=['T_sum_be']).to_csv('work/derived/glacier_year_panel_berkeley.csv.gz',index=False,float_format='%.4f')
PY
python files/code/02_models.py work/derived/glacier_year_panel.csv.gz work/derived              # GHCN-CAMS (planned)
python files/code/03_followup.py work/derived/glacier_year_panel.csv.gz work/derived
python files/code/02_models.py work/derived/glacier_year_panel_berkeley.csv.gz work/derived/be  # Berkeley Earth (main)
python files/code/03_followup.py work/derived/glacier_year_panel_berkeley.csv.gz work/derived/be
python files/code/04_freq_robust.py work/derived/glacier_year_panel.csv.gz work/derived work/derived/glacier_summer_T_berkeley.csv
python files/code/06_figures.py work/derived files/figures files/data
```

Without the raw files, `files/data/glacier_year_panel.csv.gz` gives the same models. It contains the Berkeley Earth summer temperature in `T_sum`, the GHCN-CAMS value in `T_sum_ghcncams`, and all WGMS balance fields. You can run `02_models.py` and `03_followup.py` on it directly. For the GHCN-CAMS runs, first copy `T_sum_ghcncams` into `T_sum`.

## 7. Files

- `files/PLAN.md`: the analysis plan, written before the main model.
- `files/code/`: `01_build.py` (panel), `05_berkeley.py` (Berkeley temperature), `fe.py` (estimator), `02_models.py` (planned models), `03_followup.py` (memory bounds, event study, autocorrelation, out-of-sample, frequency), `04_freq_robust.py` (frequency robustness and product comparison), `06_figures.py`.
- `files/data/glacier_year_panel.csv.gz`: the glacier-year panel (all glaciers and years; the models drop missing values).
- `files/data/model_results_berkeley.json`, `followup_results_berkeley.json`: main results.
- `files/data/model_results_ghcncams.json`, `followup_results_ghcncams.json`, `models_ghcncams.log`: planned GHCN-CAMS results.
- `files/data/frequency_robustness.json`, `frequency_decomposition.csv`, `model_coefficients.csv`: all coefficients in long format.
- `files/data/event_study_rows_berkeley.csv.gz`, `same_year_residuals_berkeley.csv.gz`: event-study inputs.
- `files/figures/fig1_event_study.png`, `fig2_memory_coefficients.png`, `fig3_lagged_balance.png`, `fig4_frequency_products.png`.

## References

- WGMS (2026): Fluctuations of Glaciers Database. World Glacier Monitoring Service, Zurich. DOI-WGMS-FoG-2026-02-10.
- Rohde, R. A. and Hausfather, Z. (2020): The Berkeley Earth Land/Ocean Temperature Record. Earth Syst. Sci. Data 12, 3469-3479. doi:10.5194/essd-12-3469-2020.
- Fan, Y. and van den Dool, H. (2008): A global monthly land surface air temperature analysis for 1948-present. J. Geophys. Res. 113, D01103. doi:10.1029/2007JD008470.
- Naegeli, K. and Huss, M. (2017): Sensitivity of mountain glacier mass balance to changes in bare-ice albedo. Ann. Glaciol. 58(75), 119-129. doi:10.1017/aog.2017.25.
