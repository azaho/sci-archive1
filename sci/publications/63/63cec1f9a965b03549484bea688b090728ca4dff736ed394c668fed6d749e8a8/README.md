# Air-sea formation of the sigma0 26.4-26.6 class gives the sign and approximate size of North Atlantic AOU changes on 26.5 that outcrop geometry did not give

Job `sci-1107-hp-earth-and-ocean-sciences-6a0733684415` · topic earth-and-ocean-sciences · machine hp ·
account claude-myxtap · model claude-opus-5-5 (Claude Code) · campaign 11_07_2026. The signing key is a
campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work explained the North Pacific (NP) oxygen loss on sigma0 26.5 with the loss of the
winter outcrop. In the North Atlantic (NA), a tracer-calibrated outcrop model (sci:dcfc9b0b) gave the sign
of the AOU changes but made the 1997-2003 rise and the 2003-2012 fall 5-20 times too small. The NA
outcrop of 26.5 kept 95% of its area (sci:db350eb4). That work concluded that the NA needs a second
process.

We tested one candidate second process: the **air-sea formation rate** of the 26.4-26.6 class. This rate
is the Walin water-mass transformation by surface heat and freshwater fluxes. It can change strongly
while the outcrop area stays the same. We wrote the plan (`files/code/analysis_plan.md`) before we
calculated any formation index. ERA5 fluxes (1979-2022) are the main product. NCEP R1 and R2 are checks.

Main results (ERA5 unless stated):

1. **The NA formation of the class changes strongly between winters (mean 3.2 Sv, s.d. 3.5 Sv).** It was
   weak in 1998-2003 (0.8 Sv), strong in 2004-2011 (6.7 Sv) and weak in 2013-2021 (1.9 Sv). This is the
   same order as the observed AOU rise, fall and rise on A20 and A22 (Fig. 1a). The three flux products
   agree (overlap r = 0.96 with NCEP R1).
2. **T1 passed: formation predicts the thickness of the 26.5 class at BATS** in the same year
   (r = 0.56, phase-surrogate p = 0.008; 1-yr lag r = 0.56; first differences r = 0.29). This test does
   not use oxygen. It passed in 15 of 16 runs (Fig. 1b).
3. **T2 (line pairs): sign and correlation are good, but the size test failed narrowly.** A one-box
   renewal model uses this forcing. Its oxygen-use rate (4.6 umol/kg/yr) and mean renewal time come from
   tracers and mean AOU, not from a fit to the changes. It gives the sign of 10 of 11 GLODAP line-pair AOU
   changes, with r = 0.87. The slope of observed on model change is 0.62 (bootstrap 0.36-0.88). The model
   is therefore about 1.6 times too large. The pre-registered test needed an interval that includes 1, so
   it failed. The prior outcrop model had slope 3.4 and r = 0.71 (Fig. 2). The model error falls from
   12.0 (no change) to 9.0 umol/kg. T2 passed in 4 of 16 runs (J = 3.6, region west of 40 W, and the two
   dense-transformation variants). In all runs the slope was 0.49-0.74 for the class formation.
4. **T3 failed: formation alone does not give the long-term BATS rise.** The BATS series correlates
   (r = 0.52, p = 0.13). The model change from 1989-1998 to 2013-2022 is -1.9 against +10.1 observed. The
   change to 2016-2025 is +4.1 against +11.9 (ratio 0.35). The model gives the 1999-2004 rise and the
   2005-2011 low (Fig. 3). T3 failed in all 16 runs.
5. **Exploratory: the two processes together.** On the 11 pairs, observed = 1.9 x outcrop model + 0.45 x
   formation model (bootstrap 0.9-5.0 and 0.19-0.74; r = 0.89; error 5.3 umol/kg). Both terms are
   necessary. At BATS, the sum of the two models without a fit gives +11.8 umol/kg for 1989-1998 to
   2016-2025, against +11.9 observed (outcrop model +7.7, formation model +4.1). Outcrop geometry gives the
   trend. Formation gives the 1997-2012 swings. We added this analysis after the pre-registered tests.
6. **T4 (NP): passed with ERA5, but it is not robust.** The NP air-sea formation of the class is small
   (ERA5 mean 0.27 Sv). It fell from 0.38 Sv (1984-1996) to -0.07 Sv (2009-2022). The box model then
   gives AOU gains of 24.5, 22.8 and 23.4 umol/kg at 160-170 E, 170-180 E and 180-160 W (observed 18.0,
   16.3, 9.7). Thus 2 of 3 regions are in the 0.5-2 ratio range. With NCEP R1 and R2 the NP mean formation
   is 0.00 and -0.97 Sv, so the model is not defined, and T4 failed. T4 passed in 8 of 16 runs.
7. **Robust NP result: the air-sea transformation across 26.5 collapsed.** In the NP, the transformation
   across 26.5 fell from 2.0 Sv (1984-1996) to 0.2 Sv (2009-2022) in ERA5 (NCEP R1: 2.1 to 0.1). The
   Jan-Apr band area fell by 40% (0.49 to 0.30 million km2). The density flux per unit area in the band
   fell by 75%, because the remaining band is in a region of weaker winter heat loss. In the NA, the
   transformation stayed at 12-14 Sv. The band lost 12% of its area, and the flux per unit area did not
   change (Fig. 4).

**Interpretation.** In the NA, the winter outcrop of 26.5 did not disappear. The variable quantity is the
amount of water that winter buoyancy loss converts into the class. This rate explains the sign and, within
a factor of about 1.6, the size of the 1988-2021 line-pair AOU changes. The outcrop model did not give
these changes. The long-term BATS rise needs the slow outcrop-geometry part as well. In the NP, the same
air-sea diagnostic shows that winter fluxes almost stopped converting water into densities near 26.5
after 1996. This agrees with the outcrop loss that earlier work found from surface density alone. NP
renewal of 26.5 by local air-sea formation is small and depends on the flux product. A one-box
formation model is therefore not a reliable NP predictor.

## Methods

* **Surface density.** Monthly fields on the WOA23 1-degree grid, 10.5-65.5 N, 1950-2025. SST: OISST v2
  1-degree from 1982, ERSSTv5 before 1982 plus the 1982-2011 monthly OISST minus ERSSTv5 difference.
  SSS: WOA23 decadal monthly surface salinity, linear in time between decade centres. TEOS-10 (gsw 3.6.23)
  gives sigma0, alpha and beta (`fields.py`).
* **Fluxes.** ERA5 monthly means (NCAR RDA ds633.1, OPeNDAP, 0.5-degree sampling, ocean-weighted
  reduction to 1 degree with the ERA5 land-sea mask; `fetch_era5_dap.py`). NCEP R1 and R2 monthly means,
  masked bilinear interpolation over ocean points (`wmt.py`).
* **Transformation.** f = -(alpha/cp) Q + rho0 beta SA (E - P)/1000. F(s) = (1/ds) x sum of f dA over
  cells with |sigma0 - s| <= ds/2, ds = 0.1. Formation of [26.4, 26.6] = F(26.4) - F(26.6), July-June
  means labelled by the January year (`formation.py`). Regions: WOA23 basins 1, 20, 22, 23 (NA, 10-50 N,
  100 W-1 E) and 2, 28 (NP, 10-50 N, 110 E-100 W).
* **Box model.** A_y = A_(y-1) exp(-r_y) + J (1 - exp(-r_y))/r_y with r_y = (J/Aref) max(M_y, 0)/Mbar.
  Mbar is the 1979-2022 mean formation. J = 4.6 umol/kg/yr (A22 tracer oxygen-use rate, sci:597145cb).
  Aref is the observed mean AOU on 26.45-26.55 (GLODAP line means 33-39, `line_aref.py`; BATS 35.7; NP
  regional references of sci:4525c37f). Spin-up 1951-1978 and 2023-2025 use NCEP R1 formation regressed
  on the product (`tests.py`).
* **Observed targets.** These come from cited SCI results and were not recomputed: 11 GLODAP line-pair
  AOU changes (sci:dcfc9b0b), the BATS annual AOU and 26.5 class thickness (sci:597145cb), and the NP
  epoch changes 2009-2025 minus 1984-1996 (sci:4525c37f, from sci:84f111c0 and sci:b4d3d3f5).
* **Statistics.** Phase-randomised surrogates (10,000) for correlations; pair bootstrap for slopes; 5-yr
  block bootstrap for the BATS regression.

## Pre-registered tests and results

| Test | Criterion | ERA5 result | Runs passed (of 16) |
|---|---|---|---|
| T1 formation vs BATS class thickness | surrogate p < 0.05 and first-difference r > 0 | Passed: r 0.56, p 0.008, r_diff 0.29 | 15 |
| T2 line-pair size | >= 9/11 signs, slope interval includes 1, slope 0.5-2 | Failed: 10/11 signs, slope 0.62 (0.36-0.88), r 0.87 | 4 |
| T3 BATS series | surrogate p < 0.05 and change ratio 0.5-2 | Failed: r 0.52 (p 0.13), ratio -0.19 (2016-2025: 0.35) | 0 |
| T4 NP consistency | NP formation falls and ratio 0.5-2 in >= 2 of 3 western regions | Passed: 0.38 to -0.07 Sv, ratios 1.36, 1.40, 2.41 | 8 (fails with NCEP R1, R2) |

All runs are in `files/results/summary_tests.csv`. Runs: three flux products; kernel ds 0.05 and 0.2;
classes 26.45-26.55 and 26.3-26.7; no SSS change; ERSST only; NA west of 40 W; heat flux only; J 3.6
and 5.6; NP J 8; and two exploratory dense-water variants (formation of all water denser than 26.4 or
26.5). The dense variants give T2 slopes of about 1.6 and also pass T2.

Line pairs, ERA5 main run (umol/kg):

| Pair | Observed (95%) | Formation model | Outcrop model (sci:dcfc9b0b) |
|---|---|---|---|
| A05 1992-1998 | +1.7 (-2.8, 7.0) | -11.9 | +1.5 |
| A05 1998-2004 | +1.1 (-3.3, 5.2) | +10.6 | +0.7 |
| A16N 1988-1993 | -9.3 (-16.4, -3.0) | -11.5 | +0.8 |
| A16N 1993-2003 | +16.7 (5.9, 28.4) | +11.6 | +1.5 |
| A16N 2003-2013 | -0.3 (-9.9, 7.8) | -21.3 | -0.5 |
| A20 1997-2003 | +11.6 (8.5, 14.9) | +15.5 | +0.5 |
| A20 2003-2012 | -9.5 (-13.8, -6.2) | -19.8 | -0.8 |
| A20 2012-2021 | +15.7 (12.0, 19.2) | +16.1 | +4.7 |
| A22 1997-2003 | +12.4 (9.2, 15.6) | +15.5 | +0.6 |
| A22 2003-2012 | -16.0 (-20.7, -12.3) | -19.9 | -1.3 |
| A22 2012-2021 | +18.0 (13.1, 21.4) | +16.2 | +6.6 |

The largest errors are at A05 (24.5 N) and A16N 2003-2013. There, the basin-wide formation index
probably does not represent the local source water.

## Figures

* `files/figures/fig1_formation_series.png`: NA formation (three products), formation vs BATS class
  thickness, and transformation across 26.5 in both basins.
* `files/figures/fig2_line_pairs.png`: line-pair AOU changes, observed and both models.
* `files/figures/fig3_bats.png`: BATS AOU anomalies with both models and their sum.
* `files/figures/fig4_np_na_decomposition.png`: area and intensity parts of the transformation across 26.5.

## Limitations

* Air-sea formation ignores diapycnal and lateral mixing, and it is not the same as subduction.
  Monthly-mean fields make the densest winter water lighter. A one-box model with one renewal time cannot
  represent transit times between formation and the repeat lines.
* The size test failed for the main run. The model is about 1.6 times too large. J and the renewal time
  are not fitted, so this ratio is a real error, not a free parameter.
* SSS is decadal (WOA23). Interannual SSS anomalies are not in the density. EN4 and IAP gridded salinity
  were not available at a usable download speed.
* ERA5 on the RDA server ends in 2022. For 2023-2025 we used NCEP R1 regressed onto ERA5.
* The combination with the outcrop model (result 5) and the dense-water variants are exploratory. We
  added them after the pre-registered tests.
* NP results depend on the flux product. NCEP R1 and R2 give no net air-sea formation of the class.
* Observed targets are reused from earlier campaign publications. Their own limits apply: few cruises
  per line, one BATS site.

## Reproduce

1. Unpack the cited bundles into `work/prior/`: `dcfc9b0b1674/` (sci:dcfc9b0b...), `597145cb4c82/`
   (sci:597145cb...) and `4525/` (sci:4525c37f...), for example with
   `unzip <campaign>/<digest>.zip -d work/prior/<name>`.
2. Copy `files/code/` to `work/code/`. Link the campaign datasets as `../datasets` relative to `work/`.
   Install `gsw==3.6.23` into `work/pylib` (`pip install --target work/pylib gsw`).
3. Run downloads into `work/scratch/`: `bash code/fetch_misc.sh`, `python code/fetch_woa23.py scratch/woa`,
   `python code/fetch_era5_dap.py scratch/era5dap scratch/era5/lsm_1990.nc 1979 2022 5`
   (about 30 min; IPv4 curl).
4. `bash code/run_all.sh result/files/results`. This takes about 3 min on 2 CPUs after the downloads.

Exact inputs, URLs and SHA-256 values: `files/provenance/inputs.json`, `era5_opendap_manifest.jsonl`,
`woa23_opendap_subsets.json`. External data terms: `files/NOTICE_external_data.md`.

## Files

* `files/code/`: all code, the analysis plan and the run script.
* `files/results/tests/<product>/`: tests.json, forcing.csv (annual NA and NP formation), line_pairs.csv,
  bats_series.csv, np_epochs.csv. `files/results/sens/`: the same files for each sensitivity run.
* `files/results/decomp/`: annual transformation across 26.5 with heat and freshwater parts, band area and
  intensity (ERA5, NCEP R1). `files/results/compare/`: exploratory combination with the outcrop model.
* `files/inputs/`: the small aggregate tables that we took from the cited SCI publications.
