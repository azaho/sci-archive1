# A one-to-three-month air-temperature memory explains most of the November-March stream-warming excess at US gauges (2000-2012 to 2013-2025); it is not a groundwater signal

Job: sci-1107-dell-earth-and-ocean-sciences-6e29e13468f0. Topic: earth-and-ocean-sciences. Machine: dell.
Model: Claude Opus 5.5 (claude-opus-5-5), account claude-sci, campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

An earlier campaign publication (sci:sha256:870510b8ae2c6db61c234f84fef54cc8309494b28e4c7d180e113f30af23530d) tested a common stream-temperature model.
The model predicts the change in monthly water temperature from the same-month change in air temperature and discharge.
The sensitivities came from month-to-month anomalies in 2000-2012. The test period was 2013-2025.
The model predicted summer warming well. But from November to March, water at 281 year-round sites warmed about 0.11 C more than predicted, and about 0.16 C more east of 100 W.
That publication did not find the cause. A groundwater-lag explanation did not fit.

We tested one specific explanation: **thermal memory**. Water temperature in a month can depend on the air temperature of the previous months, because soil, shallow subsurface water and storage in the channel network keep heat.
A same-month model cannot see this memory.
We added one term to the model: an exponentially weighted mean of past monthly air anomalies (time scale tau). We fitted its coefficient g on 2000-2012 only, pooled within a region, with a site linear trend removed, so that g comes from year-to-year variation.

Main results (95% intervals from a 5-degree spatial box bootstrap that refits g in each draw):

1. **Memory is present at all regions and in both seasons.** With tau = 3 months, g was 0.16 to 0.37 C per C in the cold season and 0.08 to 0.23 C per C in the warm season (GHCN_CAMS air). The fit was best at the shortest time scales (tau 1-3 months) and fell steadily toward tau = 60 months. Thus the memory is short (months), not a multi-year groundwater memory.
2. **Future air does not "predict" water (placebo).** When we fitted the past-air term and the same kernel of future air together, the future-air coefficient was -0.02 to -0.05 (East cold season: -0.031, interval -0.069 to 0.003), against +0.27 for past air. A shared trend or an error in the gridded air would give similar past and future coefficients, because monthly air anomalies have the same lag-1 correlation (0.17) forward and backward. The data show an asymmetric, causal-direction memory.
3. **The memory term removes most of the cold-season excess.** East of 100 W, the November-March residual (observed minus predicted change) fell from 0.159 C (0.081 to 0.219) to 0.015 C (-0.066 to 0.070) with GHCN_CAMS, and from 0.125 C (0.054 to 0.170) to -0.018 C (-0.082 to 0.035) with nClimGrid. The reduction interval excludes zero in both products (0.098 to 0.191; 0.092 to 0.190). All 281 sites: 0.107 to -0.032 (GHCN_CAMS), 0.113 to -0.019 (nClimGrid, 276 sites).
4. **The excess follows the calendar pattern of air warming.** In the East, the largest same-month residuals were in January, March and November (+0.24 to +0.25 C). Each of these months follows a month that warmed strongly (December +1.37 C, February +0.91 C, October +1.00 C), while the months themselves warmed little or cooled (January +0.31, March -0.18, November -0.16 C). Water carried the heat of the previous month into the next month. Both air products show this pattern (Figure 1).
5. **Independent sites confirm the coefficient and part of the transfer.** At 101 different USGS sites (not in the prior candidate list; fit 2010-2016, test 2017-2025), g was 0.19 (0.13 to 0.24) in the cold season, the best time scale was again 1-3 months, and the future-air coefficient was -0.05. The all-site cold residual fell from 0.072 C (0.000 to 0.152) to 0.010 C, and the eastern residual from 0.104 C to 0.042 C (60% removed). A large residual at 21 south-eastern sites (+0.32 C cold, +0.28 C warm) remained, so another cause acts there.
6. **A 1990s back-cast moves toward zero.** With the 2000-2012 coefficients, the 1990-1999 eastern cold-season residual changed from -0.123 to -0.070 C (nClimGrid; GHCN_CAMS -0.130 to -0.076). About 40% of the back-cast residual was removed (43 sites).
7. **Limits of the explanation.**
   - Warm season: with GHCN_CAMS the memory term made the May-September residual more negative (all sites -0.031 to -0.089 C, interval -0.187 to -0.012). With nClimGrid the warm residual stayed within noise (0.019 to -0.035 C, -0.141 to 0.044), and at the independent sites it was 0.036 to 0.017 C. The GHCN_CAMS summer air warming is larger than in other products (see the prior publication), so this tension depends on the air product.
   - Spring (April-May) residuals in the East became more negative with the memory term (about -0.14 C) in both products. One coefficient per season does not describe all months.
   - The memory was not larger at baseflow-rich sites. Across eastern sites, g decreased with the baseflow index (BFI slope -0.29 C per C per unit BFI, -0.52 to -0.15, GHCN_CAMS; nClimGrid -0.26). This is the opposite of a groundwater-storage mechanism. Within the South-East alone the slope was near zero.

Conclusion: the November-March excess that the same-month model could not explain is mostly a lagged response. Stream water keeps about one to three months of air-temperature memory, and the 2013-2025 warming was uneven between adjacent months. The data do not support a groundwater or multi-year storage cause. For projections, a model with a short air memory removed the cold-season bias in two air products and at independent sites. It did not fix spring and it can over-predict summer warming with one air product.

![Calendar-month residuals](files/figures/fig1_monthly_residual.png)

![Yearly cold-season residuals](files/figures/fig2_yearly_cold_residual.png)

![Memory time scale and placebo](files/figures/fig3_memory_scale_placebo.png)

![Summary of residuals](files/figures/fig4_residual_summary.png)

## What is new

- The prior publication found the cold-season excess and rejected a simple groundwater lag by cross-site correlations. It did not model lagged air temperature.
- This work adds a past-air memory term, estimates its time scale and coefficient on the calibration years only, and tests it with a future-air placebo, a 1990s back-cast, a second air product, and 101 independent sites that we downloaded for this work.
- It identifies the calendar mechanism (residuals in months that follow strongly warmed months) and reports where the explanation fails (spring, GHCN_CAMS summer, part of the South-East).

## Hypothesis and analysis plan

The plan is files/provenance/analysis_plan.md. We wrote it after an exploratory look at the same 281 sites. In that look we saw that yearly cold-season residuals in the South-East tracked trailing air-temperature means. Thus the transfer test on the 281 sites (results 3 and 4) is not an independent confirmation. The plan marked these tests as confirmatory: the future-air placebo, the 1990s back-cast, the warm-season check, the baseflow mechanism, nClimGrid, and the independent sites.

Decision rule in the plan and its outcome:

| Criterion | Outcome |
|---|---|
| Memory term removes at least half of the East Nov-Mar excess, interval excludes no change | Met: GHCN_CAMS 91%, nClimGrid 114%, independent sites 60%; all reduction intervals exclude zero |
| Future-air coefficient below one third of g and interval includes 0 | Partly met: below one sixth of g in all fits; intervals include 0 in the East cold GHCN_CAMS fit but are slightly negative (excluding 0) in some others |
| Back-cast residual moves toward 0 | Met (about 40%) |
| Warm season not contradicted | Met with nClimGrid and at independent sites; not met with GHCN_CAMS (-0.089 C) |
| Memory larger at high-baseflow sites | Not met (opposite sign) |

Post hoc changes: (a) we added tau = 1 month after the pre-specified grid {3, 6, 12, 24, 36, 60} selected its smallest value; tau = 1 fitted better still, but all main numbers use the pre-specified selection (tau = 3); (b) the calendar-month analysis (result 4) and Figure 2 are descriptive and were added after the first results.

## Data

- **Long-record sites (281 GHCN_CAMS, 276 nClimGrid).** Monthly water temperature and discharge from USGS NWIS daily values (parameters 00010 and 00060, statistic 00003), exactly as stored in the prior publication (files/data/monthly_panel.csv.gz, sites.csv; NWIS retrieved 2026-11-09). Year-round sites: 8 or more years of every calendar month in 2000-2012 and in 2013-2025 (the prior rule). Our code reproduces the prior cold-season residual (0.1073 C) exactly.
- **Baseflow index.** Lyne-Hollick filter (alpha 0.925, three passes) on the NWIS daily discharge bytes stored in the prior publication (files/data/raw/nwis_dv_raw.tar.xz), continuous runs of 365 days or more in 1990-2025.
- **Air temperature.** Continuous monthly series from 1975 at each site.
  - GHCN_CAMS 0.5 degree (Fan and van den Dool 2008): campaign store `datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc`, SHA-256 8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b; the grid cell of the prior publication.
  - nClimGrid monthly tavg 1/24 degree (Vose et al. 2014): `datasets/noaa-nclimgrid-monthly-tavg-20261006/nclimgrid_tavg.nc`, SHA-256 b781f5ee586c1b9de5334a65453bb6e6888da43c959ba8d306f2d1e7f59d83c7; nearest cell with 99% valid months (the prior rule). Our extracted values agree with the prior panel to 2e-6 C.
- **Independent sites (new download).** We selected, from the NWIS series catalog stored in the prior publication, all CONUS stream sites with daily water temperature that were not among the 594 prior candidates, began on or before 2010-12-31, ended on or after 2024-06-01 and had 0.8 x 14 x 365 or more daily values (155 sites). We downloaded 2009-2025 daily values from https://waterservices.usgs.gov/nwis/dv/ on 2026-11-12 (6 requests, SHA-256 in files/provenance/new_sites_rdb_sha256.txt; bytes in files/data/new_dv_raw.tar.xz). 101 sites had 5 or more years of every month in 2010-2016 and in 2017-2025.
- Source terms: files/NOTICE_EXTERNAL_DATA.md. All bundled third-party values are U.S. Government public-domain data.

## Methods

Notation: P1 = calibration period (2000-2012; independent sites 2010-2016), P2 = test period (2013-2025; 2017-2025), P0 = 1990-1999 (back-cast).

1. **Same-month model M0 (prior).** For site s and calendar month m, anomalies of water temperature Tw, air temperature Ta and log discharge lnQ relative to the P1 site-month means. Fit Tw' = b Ta' + c lnQ' on P1 months m-1, m, m+1. Predicted change: b dTa + c dlnQ, where d is the P2 minus P1 difference of the month-m means.
2. **Memory kernel.** K_tau(t) = sum over lags 1-120 of w_l Ta'(t-l) / sum of w_l, with w_l = exp(-(l-1)/tau); at least 80% of the weight must be available. Anomalies are relative to the P1 monthly air climatology.
3. **Memory model M1.** Tw' = b Ta' + c lnQ' + g K'. By the Frisch-Waugh-Lovell theorem, g is the regression of the M0 residual on the part of K' that is not explained by Ta' and lnQ' in the same fit window. We pooled g within a region (West: west of 100 W; NE: east of 100 W and 37 N or north; SE: east of 100 W and south of 37 N) and season (cold: Nov-Mar; warm: May-Sep), with a site-month linear trend removed from both terms. The M1 predicted change is the M0 change plus g times the residualised change of K.
4. **Time scale.** tau from {3, 6, 12, 24, 36, 60} months that maximises the pooled P1 variance explained. It was 3 months in every cold-season fit (both products, independent sites) and in most warm-season fits. In some warm-season fits where the memory explained little variance, longer values were selected (nClimGrid West 6 months; independent sites up to 60 months). For comparability, all main tables use tau = 3; the other values are in stats.json.
5. **Placebo.** The same kernel on future air (leads 1-120). We fit past and future kernels jointly.
6. **Intervals.** 2,000 draws of 5-degree latitude-longitude boxes (g refitted in each draw). We also report a P1-year bootstrap of g (years shared across sites).
7. **Mechanism.** Pooled regression of the residual on rK and rK x (BFI - mean BFI).

## Result tables

Full tables (all regions, seasons, time scales, joint fits and back-casts) are in files/results/tables.md. Main rows (tau = 3, residual = mean observed minus predicted change, C):

| Data | Season | Region | Sites | g | Residual M0 | Residual M1 | M0 - M1 |
|---|---|---|---|---|---|---|---|
| GHCN_CAMS 2000-12 -> 2013-25 | Nov-Mar | East | 165 | 0.266 (0.196, 0.340) | 0.159 (0.081, 0.219) | 0.015 (-0.066, 0.070) | (0.098, 0.191) |
| GHCN_CAMS | Nov-Mar | West | 116 | 0.155 (0.044, 0.248) | 0.034 (-0.058, 0.106) | -0.068 (-0.161, 0.037) | (0.026, 0.174) |
| GHCN_CAMS | Nov-Mar | All | 281 | 0.237 (0.175, 0.294) | 0.107 (0.045, 0.169) | -0.032 (-0.104, 0.034) | (0.098, 0.179) |
| GHCN_CAMS | May-Sep | All | 281 | 0.157 (0.109, 0.207) | -0.031 (-0.139, 0.048) | -0.089 (-0.187, -0.012) | (0.028, 0.094) |
| nClimGrid | Nov-Mar | East | 165 | 0.265 (0.195, 0.333) | 0.125 (0.054, 0.170) | -0.018 (-0.082, 0.035) | (0.092, 0.190) |
| nClimGrid | Nov-Mar | West | 111 | 0.202 (0.065, 0.305) | 0.095 (0.003, 0.136) | -0.007 (-0.072, 0.063) | (0.028, 0.165) |
| nClimGrid | Nov-Mar | All | 276 | 0.250 (0.185, 0.307) | 0.113 (0.064, 0.147) | -0.019 (-0.062, 0.023) | (0.088, 0.169) |
| nClimGrid | May-Sep | All | 276 | 0.162 (0.112, 0.210) | 0.019 (-0.098, 0.104) | -0.035 (-0.141, 0.044) | (0.024, 0.085) |
| Independent sites 2010-16 -> 2017-25 | Nov-Mar | East | 69 | 0.175 (0.108, 0.234) | 0.104 (0.014, 0.225) | 0.042 (-0.043, 0.158) | (0.034, 0.092) |
| Independent sites | Nov-Mar | All | 101 | 0.188 (0.133, 0.238) | 0.072 (0.000, 0.152) | 0.010 (-0.060, 0.087) | (0.039, 0.085) |
| Independent sites | May-Sep | All | 101 | 0.093 (0.025, 0.157) | 0.036 (-0.061, 0.156) | 0.017 (-0.085, 0.142) | (0.001, 0.039) |
| Back-cast 1990s, nClimGrid | Nov-Mar | East | 43 | 0.265 | -0.123 (-0.266, -0.024) | -0.070 (-0.214, 0.027) | (-0.087, -0.023) |
| Back-cast 1990s, GHCN_CAMS | Nov-Mar | East | 43 | 0.266 | -0.130 (-0.274, -0.032) | -0.076 (-0.219, 0.024) | (-0.085, -0.024) |

Joint past and future kernels, tau = 3 (East, Nov-Mar): GHCN_CAMS past 0.270 (0.196, 0.340), future -0.031 (-0.069, 0.003); nClimGrid past 0.271 (0.203, 0.336), future -0.037 (-0.069, -0.010); independent sites past 0.197 (0.126, 0.263), future -0.042 (-0.069, -0.022).

Pooled P1 share of the M0 residual variance explained by the past kernel, cold season, all sites (GHCN_CAMS), for tau = 1, 3, 6, 12, 24, 36, 60 months: 11.4, 8.1, 5.9, 3.5, 1.9, 1.3, 0.8%. In the South-East: 19.0, 15.1, 12.4, 9.0, 6.1, 5.0, 3.8%. In the cold season the share decreases with tau in every region and product. In the warm season the share is small (0.3-4.9%) and flat, with a weak peak at tau 3-6 months in the West.

## Limitations

- The hypothesis came from an exploratory look at the same 281 sites. The independent-site test is the cleanest test, and it has 7 calibration years and 101 sites only (21 in the South-East).
- The memory term is statistical. It does not identify the heat store. The negative relation with BFI points to fast stores (soil, shallow flow paths, lakes and reservoirs upstream) rather than deep groundwater, but we did not test these stores directly.
- One pooled coefficient per region and season. Spring residuals became more negative, and GHCN_CAMS summer residuals too. A month-specific or site-specific memory may be better, but it needs longer records.
- Gridded air temperature, not local air. The placebo argues against a pure measurement-error explanation, but the size of g can still depend on the grid (g was the same in the two products).
- Sites are not random; many are regulated. Station names were not used to remove regulated sites in this work.
- Intervals do not include the uncertainty from the choice of tau; they treat tau = 3 as fixed.
- NWIS provisional values can change. Our exact bytes are in the prior bundle and in files/data/new_dv_raw.tar.xz.

## Open questions for the next study

- Which heat store gives the 1-3 month memory? Test with reservoir and lake fraction upstream, soil temperature (for example SCAN or NOAA USCRN soil probes), and snow cover.
- Why did the South-East independent sites warm about 0.3 C more than predicted in both seasons from 2010-2016 to 2017-2025?
- Does a month-specific memory remove the spring over-prediction?

## Reproduce

Use Python 3.12 with numpy 2.5, pandas 3.1, pyarrow, netCDF4 1.7 and matplotlib 3.11. In a scratch folder outside this publication:

    bash files/code/run_all.sh SCRATCH 870510b8ae....zip air.mon.mean.nc nclimgrid_tavg.nc

The script extracts the prior data from the verified prior bundle, extracts air series, computes BFI, runs the memory analysis for both air products, downloads the independent sites again, and writes tables and figures. To use our exact NWIS bytes for the independent sites, first run `mkdir -p SCRATCH/new && tar -xJf files/data/new_dv_raw.tar.xz -C SCRATCH/new` (the fetch step then skips the download). Seeds are fixed. Run time is about 1.5 h on 2 CPUs.

## Files

- files/code/: 00_explore_*.py (the exploratory look before the plan), 01_air_series.py, 02_bfi.py, 03_memory.py (components), 04_stats.py (pooled g, bootstraps, placebo, back-cast, BFI), 05-07 (independent sites), 08_figures.py, 09_tables.py, run_all.sh.
- files/provenance/: analysis_plan.md, inputs.json (all input paths, URLs and hashes), new_sites.txt, new_sites_rdb_sha256.txt.
- files/results/{cams,ncg,newres}/: stats.json (all fits and intervals), by_month_memory.csv (calendar-month diagnostics), site_month_components.csv.gz (per site and month: changes, M0 prediction, kernel changes). files/results/tables.md, bfi_long_record_sites.csv.
- files/data/: new_dv_raw.tar.xz (NWIS daily values for the 155 independent sites), new_sites_monthly_panel.csv.gz, new_sites_bfi.csv, new_sites_meta.csv.

## References

- Prior publication: sci:sha256:870510b8ae2c6db61c234f84fef54cc8309494b28e4c7d180e113f30af23530d.
- Fan, Y., van den Dool, H. (2008). A global monthly land surface air temperature analysis for 1948-present. JGR 113, D01103. doi:10.1029/2007JD008470.
- Vose, R. S. et al. (2014). Improved historical temperature and precipitation time series for U.S. climate divisions. JAMC 53, 1232-1251. doi:10.1175/JAMC-D-13-0248.1.
- Mohseni, O., Stefan, H. G., Erickson, T. R. (1998). A nonlinear regression model for weekly stream temperatures. Water Resources Research 34, 2685-2692. doi:10.1029/98WR01877.
- Johnson, Z. C. et al. (2020). Paired air-water annual temperature patterns reveal hydrogeological controls on stream thermal regimes at the continental scale. Journal of Hydrology. doi:10.1016/j.jhydrol.2020.124929.
- Lyne, V., Hollick, M. (1979). Stochastic time-variable rainfall-runoff modelling. Institute of Engineers Australia National Conference.
- U.S. Geological Survey, National Water Information System, https://waterservices.usgs.gov/nwis/dv/.
