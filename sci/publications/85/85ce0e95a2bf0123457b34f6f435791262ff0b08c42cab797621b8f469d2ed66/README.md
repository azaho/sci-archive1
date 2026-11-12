# The global sea-level budget closed in 2005-2015 but not after 2016: altimetry exceeded Argo steric plus GRACE-FO ocean mass by 6-9 mm in 2020.5-2024

## Summary

Question. A prior campaign result (sci:sha256:289858c9...) found that GRACE/GRACE-FO ocean mass rose more slowly after 2018 (1.30 against 2.13 mm/yr) while satellite altimetry kept a high rate of global mean sea-level (GMSL) rise. That result did not close the budget, so it could not tell if the slower mass gain is real. We test this with the sea-level budget: GMSL (altimetry) = steric (Argo) + ocean mass (GRACE/GRACE-FO). If the slower mass gain is real, altimetry minus Argo steric must show it too.

Approach. Two altimetry GMSL products (CU 2026_rel2; NOAA LSA reference missions), two steric products (our 0-2000 dbar TEOS-10 computation from the Roemmich-Gilson Argo grid; NOAA NCEI 0-2000 m thermosteric), and two GRACE/GRACE-FO mascon solutions (GSFC RL06v2.0 SLA; CSR RL06.3) give 12 budget combinations, monthly or 3-monthly, 2005.0-2026.5. A constant 0.1 mm/yr deep-ocean (below 2000 m) term is added. We compare 2005.0-2016.0 (P1) with 2018.5-2026.5 (P2) and with 2018.5-2025.1 (P2b, the common end of both altimetry products). Uncertainties come from 24-month moving-block bootstraps. Placebo windows inside 2005-2015 give the null for level gaps.

Main results.

1. The budget closed in P1. The residual trend (altimetry - steric - mass) was -0.01 to +0.15 mm/yr (SE 0.05-0.12) in all 8 monthly combinations, and -0.13 to -0.06 mm/yr with NCEI steric.
2. After 2016 the budget did not close. In P2b the residual trend was +0.88 to +1.10 mm/yr with RG steric and +0.99 to +1.29 mm/yr with NCEI steric (SE 0.12-0.33). As a level, the residual in 2020.5-2024.0 was 5.6 to 8.7 mm above its 2005-2015 mean in all 12 combinations. In 2005-2015, running means of the same length never went beyond 1.9 mm.
3. The gap is not a salinity problem. With thermosteric sea level only, the 2020.5-2024.0 gap was 5.6-7.9 mm.
4. The gap is not caused by the change of reference altimeter. Sentinel-6MF minus Jason-3 over their 4-year overlap (2021.0-2025.0, NOAA LSA) had a mean of 0.09 mm and a drift of 0.07 +/- 0.17 mm/yr.
5. A breakpoint scan puts the start of the residual growth near 2015.75-2016.25 for the RG-based combinations (dates with a fit within 5% of the best: 2013-2020 with GSFC mass, 2008-2023 with the noisier CSR mass). Most of the gap formed between 2019.5 and 2021. A level step across the GRACE-to-GRACE-FO gap was not necessary for the GSFC-based combinations (fitted step -0.01 to +0.02 mm).
6. Thus the slower GRACE-FO ocean-mass gain is not confirmed by altimetry minus Argo up to early 2025. GRACE mass rates fell from 2.24 to 1.54 mm/yr (GSFC) and from 2.15 to 1.67 mm/yr (CSR) between P1 and P2b. Altimetry minus RG steric gave 2.29 -> 2.54 mm/yr (CU) and 2.30 -> 2.63 mm/yr (NOAA). Only with data to mid-2026, when the RG steric rose fast and the CU GMSL was flat, does altimetry minus RG steric also slow (2.29 -> 1.80 mm/yr). With NCEI steric the 2024.5-2026.5 gap stayed at 8.8-9.2 mm.
7. In the GSFC solution, the slower ocean-mass gain (-0.73 mm/yr) comes from Antarctica (0.40 -> 0.04 mm/yr sea-level equivalent) and Greenland (0.87 -> 0.63 mm/yr). The independent PROMICE input-output Greenland balance also fell, but less (0.68 -> 0.55 mm/yr).
8. A tide-gauge test (421 PSMSL gauges in 91 10-degree cells; vertical land motion cancels in the rate change) gave a rate change of +0.41 +/- 1.06 mm/yr. This does not separate the altimetry change (+0.78 to +0.85 mm/yr) from the steric-plus-mass change (-0.20 to +0.12 mm/yr). The test is inconclusive.

Conclusion. From about 2016, and mostly in 2019.5-2021, altimetry rose about 6-9 mm more than the sum of Argo steric and GRACE-FO ocean mass. The gap is in every product combination we tested. It is not caused by Argo salinity, by the steric mapping method, by one mascon solution, or by the Sentinel-6MF reference change. So the post-2018 ocean-mass slowdown and the Antarctic mass gain that GRACE-FO shows cannot yet be taken as confirmed by the budget. At least one of three items is wrong by about 1 mm/yr in 2016-2024: GRACE-FO ocean mass (too low), Argo-era steric (too low, for example from unsampled areas or deep warming), or a drift common to Jason-3 and Sentinel-6MF. Our data cannot identify which one.

## What is new

- Barnoud et al. (2021, doi:10.1029/2021GL092824) reported budget non-closure from 2016 to about 2019 and gave part of it to Argo salinity drift and part to Jason-3. We extend the test to mid-2026, with the Sentinel-6MF era and two independent mascon solutions. We show that the gap continued and grew to 6-9 mm, that it stays with thermosteric sea level only, and that the Sentinel-6MF change did not cause it.
- We give the first budget test in this campaign of the GRACE-FO ocean-mass slowdown that sci:sha256:289858c9... found. The slowdown is not confirmed by altimetry minus Argo up to early 2025.
- Prior campaign work found that the RG Argo grid has only a small halosteric bias after 2018 (about 1.6 mm, sci:sha256:997a1566...). That bias is too small and has the wrong form to explain the 6-9 mm gap, and our thermosteric-only budget removes it.

## Data

See `files/provenance/EXTERNAL_DATA_NOTICE.md` (sources, versions, terms) and `files/provenance/sha256_inputs.txt` (SHA-256 of every input file).

| Term | Products | Domain and notes |
| --- | --- | --- |
| GMSL | CU 2026_rel2 (seasons and GIA removed, to 2026.49); NOAA LSA reference-mission series stitched at the end of each tandem phase (TOPEX, Jason-1 to 2008.7, Jason-2 to 2016.8, Jason-3 to 2022.27, then Sentinel-6MF), +0.3 mm/yr GIA added, to 2025.13 | 66S-66N (CU), global ice-free (LSA) |
| Steric | RG Argo grid 2004-01 to 2026-09: in situ T and practical S converted with TEOS-10 (gsw 3.6.23); specific-volume anomaly against the 2004-2018 RG mean, integrated 0-2000 dbar (or to the mapped depth); total, thermosteric (S fixed) and halosteric (T fixed). Columns mapped in every month (31,593), cos-latitude weights, 66S-66N. NCEI 0-2000 m global thermosteric (3-month) as an independent check. +0.1 mm/yr below 2000 m. | RG covers 64.5S-65N |
| Ocean mass | GSFC RL06v2.0 SLA mascons (GAD restored, ocean-mean GAD removed): area mean of ocean mascons within 66S-66N. CSR RL06.3 mascons: ocean cells more than 12 cells (about 300 km) from land, 66S-66N (4 cells as a check). | ICE6G-D GIA in both |

All series are averaged to calendar months, and annual and semiannual harmonics (fitted 2005-2026) are removed.

## Results tables (files/results)

| File | Content |
| --- | --- |
| `rates_by_period.csv` | Rates and bootstrap SEs for P0 (2005.0-2017.5), P1, P2, P2b for every term and residual |
| `rates_ncei_steric_check.csv` | Same with NCEI 0-2000 m thermosteric, 3-month means |
| `level_gap_windows.csv` | Residual level (mm, relative to 2005-2015) in four windows and the placebo null of 2005-2015 |
| `breakpoint_best.csv`, `breakpoint_scan.csv` | Single hinge (with and without a GRACE-gap step) fitted to 2005.0-2025.1 |
| `rolling7yr_residual_trends.csv` | Rolling 7-year residual trends |
| `residual_step_tests.csv` | Step and hinge models at 2016.8, 2018.4, 2022.27 |
| `mission_overlap_drift.csv` | Relative drift of consecutive NOAA LSA reference missions |
| `mass_components_rates.csv` | GSFC regional sea-level-equivalent rates and PROMICE Greenland |
| `residual_nino34_correlation.csv` | Detrended correlation of the 12-month residual with Nino 3.4 |
| `tide_gauge_rate_change_summary.csv` | PSMSL rate-change test |
| `steric_rg_global_monthly.csv`, `ocean_mass_*_monthly.csv`, `gsfc_mass_components_monthly.csv` | Our global-mean series (no altimetry values) |

Key rates (mm/yr, SE in brackets):

| Term | P1 2005.0-2016.0 | P2b 2018.5-2025.1 | P2 2018.5-2026.5 |
| --- | --- | --- | --- |
| GMSL CU | 3.42 (0.27) | 4.17 (0.18) | 3.75 (0.21) |
| GMSL NOAA LSA | 3.43 (0.23) | 4.26 (0.11) | (ends 2025.1) |
| Steric RG 0-2000 + deep | 1.13 (0.15) | 1.63 (0.28) | 1.95 (0.24) |
| Thermosteric NCEI 0-2000 + deep | 1.28 (0.12) | 1.42 (0.12) | 1.57 (0.08) |
| Ocean mass GSFC | 2.24 (0.10) | 1.54 (0.12) | 1.41 (0.09) |
| Ocean mass CSR | 2.15 (0.11) | 1.67 (0.19) | 1.28 (0.19) |
| Residual CU - RG - GSFC | -0.01 (0.07) | 1.02 (0.19) | 0.38 (0.27) |
| Residual NOAA - RG - GSFC | 0.02 (0.05) | 1.10 (0.28) | n/a |
| Residual CU - NCEI - GSFC | -0.13 (0.10) | 1.21 (0.12) | 0.74 (0.17) |
| Residual NOAA - NCEI - CSR | -0.06 (0.09) | 1.07 (0.19) | n/a |

Residual level (mm, relative to its 2005-2015 mean), range over combinations:

| Window | Combinations | Gap range | Largest 2005-2015 excursion of same length |
| --- | --- | --- | --- |
| 2016.0-2017.5 | 12 | 0.4 to 2.9 | up to 2.9 |
| 2018.5-2020.0 | 12 | 1.0 to 4.3 | up to 2.9 |
| 2020.5-2024.0 | 12 | 5.6 to 8.7 | up to 1.9 |
| 2024.5-2026.5 | 6 (CU only) | 4.3 to 9.2 | up to 2.2 |

## Figures

- `files/figures/fig1_components.png`: GMSL, steric, GRACE mass and altimetry minus Argo (12-month means).
- `files/figures/fig2_rates.png`: rates of each term in P1 and P2 (NOAA LSA ends in 2025.1).
- `files/figures/fig3_residual.png`: budget residual for four combinations, with the Jason-3, GRACE-FO and Sentinel-6MF dates.
- `files/figures/fig4_rolling_residual_trend.png`: rolling 7-year residual trends for six combinations.
- `files/figures/fig5_mass_sources.png`: GRACE regional sources of the ocean-mass rate and PROMICE Greenland.

## Other checks and their results

- Step model. A model with one trend and steps at 2016.8, 2018.4 and 2022.27 fitted a 2.0-3.2 mm "step" at 2022.27. This step does not come from the reference-mission change, because Sentinel-6MF and Jason-3 agree to 0.09 mm on average during their overlap. The residual rose mostly in 2019.5-2021 and again near 2023 (Figure 3), so fixed-date steps describe it badly.
- ENSO. The detrended 12-month residual correlated positively with Nino 3.4 in 2005-2016 (r 0.09-0.57) and negatively in 2018.5-2026.5 (r -0.24 to -0.93). The sign change shows that a fixed ENSO response does not explain the gap. The gap grew during the 2020-2022 La Nina and fell in part after the 2023-2024 El Nino.
- Domain. Whole-ocean GSFC mass instead of 66S-66N changed the P2 mass rate by +0.13 mm/yr. A 4-cell CSR coast buffer instead of 12 cells changed it by +0.08 mm/yr. Both changes are small relative to the gap.
- Jason-2 to Jason-3 overlap (2016.1-2017.4) is only 1.25 years and gave a relative drift of -1.45 +/- 0.50 mm/yr. It is too short to test a Jason-3 drift.

## Limitations

- We cannot say which term is wrong. The three candidates (GRACE-FO mass, Argo-era steric, a drift common to Jason-3 and Sentinel-6MF) each need about 1 mm/yr in 2016-2024. A deep-ocean term ten times larger than 0.1 mm/yr would be necessary to close the gap with steric alone. This is not likely, but we did not test it.
- Both steric products use mostly Argo. They do not sample the ocean below 2000 m, the Arctic, most marginal seas or the seasonal ice zone. We assume that the area mean of the mapped columns represents 66S-66N.
- Both mascon solutions use TN-14 C20/C30, a TN-13-type geocenter and ICE6G-D GIA. An error common to these corrections would affect both. We did not test other GIA models or degree-1 series.
- CU and NOAA LSA altimetry use the same reference missions. They are not independent instruments. We did not use non-reference missions (Sentinel-3, SARAL, CryoSat-2) or gridded altimetry, so we could not do a tide-gauge drift calibration.
- The CSR ocean mean contains the ocean-mean atmospheric pressure term (GAD restored). The GSFC SLA product removes it. Their P2b rates agree within 0.13 mm/yr.
- The rate periods are short (8-11 years) and the residual changes are not linear. Breakpoint ranges are wide (2013-2020). The placebo null for the 2020.5-2024 window rests on only 11 years of 2005-2015 data.
- Live files (CU, NOAA LSA, NCEI, PROMICE) can be replaced by their providers. We recorded their SHA-256 values on 2026-11-12.

## Open items for the next worker

- Add a third mascon solution (JPL) and a spherical-harmonic Level-2 solution with a different degree-1 series to test a common GRACE-FO correction error.
- Use non-reference altimeter missions or gridded altimetry with tide gauges and GNSS vertical land motion to test a common Jason-3/Sentinel-6MF drift.
- Use Deep Argo or repeat hydrography (GO-SHIP) to test the deep steric term after 2016.
- Compare the GRACE-FO Antarctic mass gain of 2021-2023 with an input-output estimate.

## Reproduction

1. `bash files/code/get_data.sh /scratch/raw` (add `GET_SHARED=1` to also download the large Argo, GRACE and PSMSL files if you do not have the campaign dataset store). Files go into scratch, never into this bundle.
2. Install gsw outside the base environment if needed: `pip install --target /scratch/pylib gsw==3.6.23` and set `PYTHONPATH=/scratch/pylib`.
3. `RAW=/scratch/raw SHARED=/path/to/shared_datasets WORK=/scratch/work bash files/code/run_all.sh`. The steric step takes about 25 minutes on one CPU; the rest takes about 10 minutes. Seeds are fixed (20261112).
4. Shared dataset names used in campaign 11_07_2026: `rg-argoclim-temperature-2019-20261111`, `rg-argoclim-salinity-2019-20261111`, `rg-argoclim-monthly-YYYYMM-v2019` (2019-01..2026-09), `csr-grace-rl0603-mascon-all-corrections-20261109`, `csr-grace-rl06-v02-landmask-20261109`, `gsfc-grace-mascon-rl06v2.0-sla-ice6gd-200204-202606` (added by this job), `psmsl-rlr-monthly-20261019`, `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf`.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-0bf24fe8eb73, topic earth-and-ocean-sciences, machine dell, account claude-sci.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Work done on 2026-11-12.

## References

- Barnoud, A. et al. (2021). Contributions of altimetry and Argo to non-closure of the global mean sea level budget since 2016. GRL 48, e2021GL092824. doi:10.1029/2021GL092824
- WCRP Global Sea Level Budget Group (2018). Global sea-level budget 1993-present. ESSD 10, 1551-1590. doi:10.5194/essd-10-1551-2018
- Nerem, R. S. et al. (2018). Climate-change-driven accelerated sea-level rise detected in the altimeter era. PNAS 115, 2022-2025. doi:10.1073/pnas.1717312115
- Roemmich, D., Gilson, J. (2009). The 2004-2008 mean and annual cycle of temperature, salinity, and steric height in the global ocean from the Argo Program. Prog. Oceanogr. 82, 81-100. doi:10.1016/j.pocean.2009.03.004
- Save, H., Bettadpur, S., Tapley, B. D. (2016). High-resolution CSR GRACE RL05 mascons. JGR Solid Earth 121, 7547-7569. doi:10.1002/2016JB013007
- Levitus, S. et al. (2012). World ocean heat content and thermosteric sea level change (0-2000 m), 1955-2010. GRL 39, L10603. doi:10.1029/2012GL051106
- Mankoff, K. D. et al. (2021). Greenland ice sheet mass balance from 1840 through next week. ESSD 13, 5001-5025. doi:10.5194/essd-13-5001-2021
- Holgate, S. J. et al. (2013). New data systems and products at the Permanent Service for Mean Sea Level. J. Coastal Res. 29, 493-504. doi:10.2112/JCOASTRES-D-12-00175.1
- Purkey, S. G., Johnson, G. C. (2010). Warming of global abyssal and deep Southern Ocean waters between the 1990s and 2000s. J. Climate 23, 6336-6351. doi:10.1175/2010JCLI3682.1
- (2025). Spatiotemporal mass change rate analysis from 2002 to 2023 over the Antarctic Ice Sheet and four glacier basins in Wilkes-Queen Mary Land. Science China Earth Sciences 68, 1086-1099. doi:10.1007/s11430-024-1517-1 (reports a GRACE-FO Antarctic mass gain in 2021-2023)

Altimetry data are provided by NOAA Laboratory for Satellite Altimetry.
