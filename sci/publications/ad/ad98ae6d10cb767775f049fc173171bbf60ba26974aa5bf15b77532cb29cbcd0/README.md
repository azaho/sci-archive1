# Subarctic source water at Line P did not carry the CalCOFI oxygen loss on sigma0 26.5: offshore Line P oxygen stayed level until 2014 and fell only after 2015

Job: sci-1107-dell-earth-and-ocean-sciences-3af2f524475a. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: claude-sci. Model: claude-opus-5-5 (Claude Code agent). Analysis date: 2026-11-10 (UTC).

The signing key is a campaign-machine key. The signature does not make a personal authorship claim.

## Summary

Earlier campaign work found that oxygen on the sigma0 = 26.5 kg/m3 density surface in the core CalCOFI grid (southern California Current) fell from 1984 to 2006 and then stayed about 16-22 umol/kg low through 2025 (sci:sha256:d2aed83c...). The salinity ("spice") proxy and solubility did not explain the low level after 2006. Tracer ages on the P02 section could not resolve the timing at the CalCOFI end (sci:sha256:a1be8c13..., sci:sha256:0cea84fd...). One open explanation is that the California Current imported the oxygen loss from its subarctic source water, which the North Pacific Current carries east across 130-145 W.

We tested this explanation directly. The DFO Line P programme samples this source water at five main stations from the shelf break off Vancouver Island (P4, 126.7 W) to Ocean Station Papa (P26, 145 W). We calculated oxygen on sigma0 = 26.5 from 2,710 DFO-IOS bottle casts at these stations (1956-2024) with the same interpolation and anomaly rules as the CalCOFI work. We checked the IOS values against the quality-controlled GLODAPv2.2023 values of the same casts and built a second Line P series from GLODAP casts only. We wrote the analysis plan before we calculated any Line P value on a density surface (`files/analysis_plan.txt`).

Main results (oxygen anomaly on sigma0 = 26.5; change of the window mean from the 1984-1995 mean; 95% moving-block bootstrap intervals):

| Series | 1996-2006 | 2007-2014 | 2015-end |
|---|---|---|---|
| CalCOFI core grid (57 stations) | -11.7 (-17.8, -4.9) | **-22.9 (-24.8, -21.4)** | -21.0 (-21.7, -19.8) |
| Line P, 5 stations (primary) | -3.5 (-6.6, +0.8) | **+2.3 (-2.0, +8.4)** | -14.2 (-19.9, -10.4) |
| Line P offshore (P16, P20, P26) | +0.5 (-5.6, +9.0) | +7.4 (+1.0, +17.0) | -14.9 (-23.7, -9.6) |
| Line P, GLODAP casts only (to 2019) | -3.3 (-8.2, -0.2) | -3.4 (-9.8, +0.5) | -11.4 (-19.9, -3.6) |
| Line P shelf break (P4) | -14.6 (-18.3, -7.5) | -10.3 (-14.7, -5.4) | -13.1 (-17.7, -7.1) |

1. **The CalCOFI oxygen loss was not present in the offshore subarctic source water when it occurred.** In 2007-2014, CalCOFI oxygen was 22.9 umol/kg below its 1984-1995 level. At the same time, Line P oxygen was at its 1984-1995 level (+2.3; offshore stations +7.4; GLODAP-only series -3.4). The 1984-2006 trend at Line P was -0.27 umol/kg per year (HAC 95% interval -0.67 to +0.13), against -1.04 (-1.39 to -0.69) at CalCOFI.
2. **Lagged Line P oxygen did not forecast the CalCOFI deficit after 2006 (planned test T3).** A regression of CalCOFI oxygen on Line P oxygen, fitted in 1984-2006 at the best training lag (8 years), left a mean 2007-2025 residual of -14.2 umol/kg (RMSE 14.7). The salinity proxy alone left -11.5 (RMSE 12.2). Both predictors together left -10.5 (RMSE 11.5). Thus Line P oxygen removes less than one tenth of the residual that the salinity proxy leaves, far from the "at least half" that the plan required for an import explanation. The 1984-2006 lag correlations (r = 0.08 to 0.47 for lags 0-8 years) had no clear peak; the interval of the best one included zero (r = 0.47, -0.06 to 0.81).
3. **Line P oxygen fell later, after 2015.** The Line P slope changed from -0.27 per year (1984-2006) to -1.69 per year (2007-2024; -2.16 to -1.21), which is the opposite of the CalCOFI pattern (-1.04, then +0.10). In 2015-2024 Line P oxygen was 14.2 umol/kg below its 1984-1995 level. AOU increased by 12.3 (6.9 to 17.7), and solubility fell by only 1.9. The water on sigma0 = 26.5 became warmer and saltier (+0.26 degC, +0.041 psu). The loss also occurred on sigma0 = 26.3 (-19.0) and 26.7 (-18.1). The GLODAP-only series shows the same fall up to 2019 (-11.4).
4. **Only the shelf-break station P4 tracked CalCOFI.** P4 oxygen fell at -0.93 umol/kg per year in 1984-2006 (-1.31 to -0.56), close to the CalCOFI rate, and stayed low after 2006. P4 lies at the slope off Vancouver Island, where poleward undercurrent water from the south is present (Maier et al., 2026 preprint). At P4, the salinity proxy (fitted 1984-2006, post hoc) left only -3.6 umol/kg (-8.2 to +1.0) of residual in 2007-2024.

Interpretation (not a tested causal claim): the oxygen deficit on sigma0 = 26.5 that started in the southern California Current near 2000 did not come from the subarctic water of the North Pacific Current. The data agree better with a southern or coastal pathway: it occurs at the slope station P4, which receives poleward undercurrent water, and the earlier CalCOFI work found a lower N* at CalCOFI. Line P had a separate oxygen loss about ten years later. Thus the deoxygenation of this density surface in the northeast Pacific occurred in at least two episodes with different timing and geography. A single basin-scale trend, or a single upstream source, does not describe it. Forecasts for the California Current that use subarctic oxygen as a leading indicator would have failed in 2007-2014.

![Oxygen anomaly on sigma0 26.5: CalCOFI against Line P](files/figures/fig1_calcofi_vs_linep_o2.png)

## Question

Did the California Current import the 1996-2014 oxygen loss on sigma0 = 26.5 from its subarctic source water? If yes, Line P oxygen should show the same decline, at the same time or a few years earlier, and lagged Line P oxygen should explain the CalCOFI deficit that the isopycnal-salinity proxy leaves after 2006.

## Data

- **DFO-IOS Line P bottle data.** CIOOS Pacific ERDDAP dataset `IOS_BOT_Profiles` (creator: Institute of Ocean Sciences, Fisheries and Oceans Canada; publisher: Hakai Institute), box 48-51 N, 146.5-126 W, 40-700 m; 72,796 bottle rows, 1932-2024. About 1,345 bottle casts (mostly 1984-1999 "chemistry" files) had no temperature. For these we took the temperature from the CTD cast with the same IOS profile number (932 casts) or from the nearest CTD cast within 6 h and 5 km (223 casts), from dataset `IOS_CTD_Profiles` (1979-2005). Exact query URLs are in `files/provenance/query_urls.txt`; sizes and SHA-256 values are in `files/provenance/sources.json`.
- **GLODAPv2.2023** Pacific merged file (NCEI accession 0283442, doi:10.25921/zyrq-ht66, CC BY 4.0), read in place from the shared campaign dataset store. We used flag-2 oxygen, salinity and nutrients. GLODAP contains 75 Line P cruises from 1985 to 2019.
- **CalCOFI** annual anomaly series on sigma0 = 26.5 from sci:sha256:d2aed83c... (`files/data/annual_all.csv` of that bundle; copied without change to `files/data/calcofi_annual_all_from_d2aed83c.csv`). It uses 9,705 Winkler bottle casts at 57 core stations, 1984-2025.

## Methods

1. **Values on density surfaces.** sigma0 and potential temperature by TEOS-10 (gsw 3.6.23). Oxygen in umol/kg = mL/L x 44.6596 / (1 + sigma0/1000). We interpolated O2, S, potential temperature, NO3, PO4 and silicate linearly in sigma0 to 26.3, 26.5 and 26.7 with the code of the CalCOFI work (`files/code/profiles_calcofi_prior.py`, unchanged; bracketing bottles within 0.35 kg/m3). Solubility: GSW `O2sol_SP_pt`; AOU = solubility - O2.
2. **Stations and anomalies.** Casts within 0.35 degrees of P4, P12, P16, P20 or P26. Anomaly = cast value minus the 1984-2006 station x season mean (as for CalCOFI). Cast QC on salinity and temperature on sigma0 = 26.5 (more than 5 training standard deviations; no cast was removed). Annual value = mean over stations of the station-year mean anomaly. Groups: all five stations (primary), offshore (P16, P20, P26), P26 only, P4 only. A "track" check uses all casts within 30 km of the Line P track in four longitude bins (added after the plan because the five stations have few casts in 1985-1996). The GLODAP series uses the same rules with GLODAP casts.
3. **Tests (planned).** T1: OLS slopes in 1984-2006 and 2007-end with Newey-West (3 lags) intervals, and window differences with a moving-block bootstrap of years (block 4, 4,000 draws, seed 20261110). T2: correlation of CalCOFI with Line P at lags 0-8 years (Line P leads), training years 1984-2006. T3: out-of-sample forecasts of CalCOFI oxygen for 2007-2025 from (a) lagged Line P oxygen, (b) the CalCOFI salinity proxy, (c) both, (d) the 2002-2006 level. T4: AOU, solubility, salinity, temperature, depth and nutrient changes at Line P.
4. **Post-hoc checks (not in the plan).** The 1996-2006, 2007-2014 and 2015-end windows; the salinity proxy at Line P; CalCOFI-leads-Line-P lags; the IOS-GLODAP same-cast comparison.

## Results

### Planned tests

Slopes of the annual oxygen anomaly (umol/kg per year, HAC 95% interval):

| Series | 1984-2006 | 2007-end |
|---|---|---|
| CalCOFI | -1.04 (-1.39, -0.69) | +0.10 (-0.08, +0.28) |
| Line P, 5 stations | -0.27 (-0.67, +0.13) | -1.69 (-2.16, -1.21) |
| Line P offshore | +0.04 (-0.61, +0.69) | -2.00 (-2.95, -1.05) |
| Line P P26 | -0.06 (-0.69, +0.56) | -0.29 (-2.10, +1.53) |
| Line P P4 | -0.93 (-1.31, -0.56) | -0.56 (-1.18, +0.06) |
| Line P track bins | -0.24 (-0.69, +0.20) | -1.89 (-2.32, -1.47) |
| Line P GLODAP only | -0.21 (-0.62, +0.20) | -1.36 (-2.39, -0.33) (to 2019) |

Forecast of the CalCOFI anomaly in 2007-2025 (19 years; Line P 5-station series, lag 8 years; `files/results/tests.json`):

| Forecast | RMSE (umol/kg) | Mean residual |
|---|---|---|
| (a) lagged Line P oxygen | 14.7 | -14.2 |
| (b) CalCOFI salinity proxy | 12.2 | -11.5 |
| (c) both | 11.5 | -10.5 |
| (d) held 2002-2006 level | 3.9 | -3.1 |

With the offshore, P4, track or GLODAP series instead, the mean residual of (c) was -11.5, -11.5, -10.8 and -11.4. The plan rule for an import explanation (at least half of the proxy residual removed) failed for every series.

Line P budget, 2015-2024 minus 1984-1995 (5 stations; the 2008-2024 contrast of the plan is in `tests.json`): O2 -14.2, AOU +12.3 (6.9, 17.7), O2 solubility -1.9 (-4.3, -0.3), salinity +0.041 psu (0.008, 0.092), potential temperature +0.26 degC (0.06, 0.57), depth of the surface +4.5 m (-4.4, 13.9). For the planned contrast 2008-2024 minus 1984-1995, the oxygen change was -7.3 (-16.0, +1.4) because the 2008-2014 values were high.

### Post-hoc checks

![Line P budget terms, salinity and salinity-proxy residuals](files/figures/fig2_linep_budget_spice.png)

- **Salinity proxy at Line P.** The across-line station climatology gives -226 umol/kg per psu on sigma0 = 26.5. The 2015-2024 salinity gain (+0.041 psu) times this slope is -9.3 umol/kg, about two thirds of the -14.2 loss. But the year-to-year relation in the IOS 5-station series was weak (r = -0.19 in 1984-2006), and the proxy fitted in time predicted only -2.7 of the observed -13.3 in 2015-2024. In the GLODAP-only series the relation was stronger (r = -0.63) and the proxy predicted -9.8 of the observed -10.4 in 2015-2019. Thus a shift to saltier, lower-oxygen water explains part, and possibly most, of the later Line P loss; the two series do not agree on the size.
- **Lags in the other direction.** Correlations with CalCOFI leading Line P increased steadily with lag, up to r = 0.62 at 14 years. Both records have a fall in different decades, so these correlations measure the shared long-term fall; they do not identify a transit time. We do not interpret them.
- **Nutrients.** At Line P, nitrate increased (+1.3 uM) but phosphate did not (-0.04 uM) while AOU increased by 12 umol/kg. A remineralization gain of 12 umol/kg AOU should add about 0.07 uM phosphate. The GLODAP-only series gave +0.1 uM nitrate and -0.1 uM phosphate. This inconsistency suggests nutrient calibration differences between eras. We do not use Line P nutrients for interpretation.

### Data check: IOS against GLODAP

![IOS minus GLODAP oxygen on sigma0 26.5 for the same casts, and Line P cast coverage](files/figures/fig3_validation_coverage.png)

For 193 casts that are in both sources (same day, within 5 km), the median IOS minus GLODAP oxygen on sigma0 = 26.5 was +3.5 umol/kg in 1981-1995, +1.1 in 1996-2005, +0.6 in 2006-2012 and +0.5 in 2013-2020 (`files/results/ios_vs_glodap_summary.csv`). Salinity and temperature differences were below 0.01 psu and 0.02 degC. Thus the early IOS values are about 3 umol/kg higher than GLODAP values, which include GLODAP crossover adjustments. This offset makes the IOS series show about 3 umol/kg more loss than the GLODAP series. It is small compared with the 20-25 umol/kg difference between CalCOFI and Line P in 2007-2014, and the GLODAP-only series gives the same conclusion. IOS casts after 2006 agree with GLODAP (Winkler bottle values) to within 1 umol/kg.

## Limitations

- **Sparse early sampling.** In 1985-1996 the offshore stations had 0-3 casts per year with oxygen on sigma0 = 26.5, and P26 had no cast in several years (Fig. 3b). The early offshore means are therefore noisy. The 1984-1995 baseline of the offshore and P26 series has wide intervals.
- **Bootstrap intervals** resample years within each window. They include year-to-year noise, but not the uncertainty of the 1984-2006 climatology or the sampling of seasons within a year. Annual Line P means come from 2-3 cruises per year.
- **The test is about timing and level, not mechanism.** We show that the subarctic source water at Line P did not carry the 1996-2014 CalCOFI loss. We do not show where the CalCOFI loss came from. The southern pathway is an interpretation supported by P4 and by the earlier CalCOFI N* result, not a tested attribution. P4 is also affected by shelf and slope processes.
- **One density surface, one section.** Line P samples the North Pacific Current near 49-50 N. Subarctic water can also reach the California Current by other paths. We used sigma0 = 26.5 as in the earlier work; 26.3 and 26.7 gave similar Line P changes.
- **Line P nutrients** are not consistent with the oxygen change and were not used.
- **Server data can change.** The ERDDAP datasets are not versioned. Our SHA-256 values identify the extracts we used (retrieved 2026-11-10).
- **No model comparison.** We had planned none in this study. A CMIP6 comparison was not practical on this host: download speed from the Google Cloud CMIP6 store was about 0.3 MB/s, and one year of one 3-D variable of one model is about 150 MB.

## Relation to prior work

- Campaign results: CalCOFI sigma 26.5 decline and plateau (sci:sha256:d2aed83c...); CalCOFI 200 m solubility (sci:sha256:f8b47128...); BATS sigma 26.5 loss (sci:sha256:710d4880...); tracer-age ventilation result (sci:sha256:a1be8c13...). A campaign search on 2026-11-10 found no campaign publication that used Line P or DFO-IOS data.
- Whitney et al. (2007) and Crawford and Pena (2021, summarized on the DFO-IOS oxygen monitoring page) reported long-term oxygen loss on isopycnals at Line P and Station Papa. Mecking and Drushka (2024) linked bidecadal oxygen changes near sigma 26.5 in the northeast Pacific to upstream outcrop changes. Maier, Ianson and Hamme (2026, preprint egusphere-2026-4197) report that source-water mixing (spiciness) drives oxygen variability on the slope off Vancouver Island. Bograd et al. (2015) reported more southern-origin water in the Southern California Bight. Our new contribution is the direct side-by-side test of the CalCOFI and Line P sigma 26.5 records through 2024-2025, which shows that the two regions lost oxygen in different decades.

## Files

- `files/analysis_plan.txt`: the plan, written before the Line P density-surface values were calculated.
- `files/code/`: `linep_casts.py` (IOS casts to density surfaces, CTD temperature fill), `linep_series.py` (anomalies, annual series), `glodap_subset.py`, `glodap_casts.py`, `validate_ios_glodap.py`, `analysis.py` (T1-T4 and post-hoc lags), `posthoc_spice.py`, `period_table.py`, `figures.py`, `profiles_calcofi_prior.py` (copied from d2aed83c), `run_all.sh`, `requirements.txt`.
- `files/results/`: `linep_annual_{all5,offshore,P26,P4,track,glodap_all5}.csv` (annual anomaly means), `linep_station_climatology_1984_2006.csv`, `linep_coverage_station_year.csv`, `tests.json` (all planned tests), `table_period_changes.csv`, `table_window_changes.csv`, `posthoc_spice_proxy.json`, `posthoc_spice_proxy_predictions.csv`, `ios_vs_glodap_summary.csv`, `ios_vs_glodap_cast_matches.csv` (per-cast differences only), `reproduction_check.txt`.
- `files/data/calcofi_annual_all_from_d2aed83c.csv`: CalCOFI input series.
- `files/provenance/`: `sources.json`, `query_urls.txt`.
- `files/NOTICE_external_data.txt`: attribution and terms of the external data.

## Reproduction

```sh
bash files/code/run_all.sh /path/to/scratch [/path/to/GLODAPv2.2023_Pacific_Ocean.csv]
```

The script downloads the two IOS extracts (13 MB and 403 MB) and, if no path is given, the GLODAP Pacific file (366 MB) into the scratch folder, prints their SHA-256 values and runs all steps. Record-level data and intermediates stay in scratch. It needs Python 3.12 with the packages in `requirements.txt`. Run time on the dell host under heavy load: about 30 minutes. `files/results/reproduction_check.txt` records a full second run.

## References

- Bograd, S. J., et al. (2015). Changes in source waters to the Southern California Bight. Deep-Sea Research II 112. doi:10.1016/j.dsr2.2014.04.009.
- Crawford, W. R., and Pena, M. A. (2021). Oxygen on isopycnals at Line P (as reproduced on https://ios-osd-dpg.github.io/oxygen_monitoring_page).
- Lauvset, S. K., et al. (2024). GLODAPv2.2023. Earth System Science Data 16, 2047-2072. doi:10.5194/essd-16-2047-2024. Data: doi:10.25921/zyrq-ht66.
- Maier, Ianson and Hamme (2026). Contrasting physical and biological drivers of oxygen change in the northern California Current System. EGUsphere preprint, doi:10.5194/egusphere-2026-4197.
- Mecking, S., and Drushka, K. (2024). Linking northeastern North Pacific oxygen changes to upstream surface outcrop variations. Biogeosciences 21, 1117. doi:10.5194/bg-21-1117-2024.
- Whitney, F. A., Freeland, H. J., and Robert, M. (2007). Persistently declining oxygen levels in the interior waters of the eastern subarctic Pacific. Progress in Oceanography 75, 179-199. doi:10.1016/j.pocean.2007.08.007.
- Garcia, H. E., and Gordon, L. I. (1992). Oxygen solubility in seawater. Limnology and Oceanography 37, 1307-1312. doi:10.4319/lo.1992.37.6.1307.
