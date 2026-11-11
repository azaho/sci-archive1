# Sigma0 26.5 oxygen loss began near 1990 at 160 E-180, where the winter outcrop shrank; oxygen there follows outcrop area at a 1-yr lag; 4 of 7 CMIP6 models do not ventilate 26.5 (1950-2025)

Job sci-1107-dell-earth-and-ocean-sciences-e165a0dff78e, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found a persistent oxygen (O2) low on the sigma0 = 26.5 kg/m3 surface off southern California (CalCOFI) since 2007. The low is mostly a loss inside water types (sci:sha256:ea67ca59...). Ship data showed that the loss occurred along the North Pacific Current path from 180 W to the coast, with an earlier start in the west (sci:sha256:b4d3d3f5...). Floats showed that the offshore loss continued to 2026 (sci:sha256:72c350c9..., sci:sha256:e7596e2a...). Two questions stayed open: where does the within-type loss start, and why do climate models not make it?

We extended the World Ocean Database (WOD) ship analysis west to 140 E (20-50 N). We measured the winter outcrop of the 26.5 class in the northwest and central Pacific. We compared oxygen with the outcrop in time, out of sample, and in seven CMIP6 models.

Main results (sigma0 26.5; changes are 2009-2025 minus 1984-1996; 95% cruise-bootstrap intervals):

1. **The winter outcrop of sigma0 26.5 shrank.** In 30-50 N, 140 E-150 W, the January-April surface density of raw WOD ship casts fell by 0.15 kg/m3 against the WOA23 climatology (1984-1996: +0.014, -0.004 to +0.028; 1997-2008: -0.160, -0.181 to -0.132; 2009-2025: -0.134, -0.158 to -0.118). In the EN4.2.2 analysis, the area with winter surface sigma0 >= 26.5 fell from 1.39 (1.01-1.94) to 0.37 (0.23-0.53) million km2 (-73%), and the mean outcrop latitude at 150 E-170 W moved north from 40.7 to 42.6 N. At the same casts, ship data fell 0.05 kg/m3 more than EN4, so the EN4 change is not an artefact of the change to Argo sampling.
2. **The loss started at 160 E-180 near 1990, not at the outcrop near Japan.** Within-type O2 fell by 13-18 umol/kg in every western region (for example 140 E-180, 28-42 N: -16.8, -19.4 to -14.1; near-outcrop water 36-46 N, 145-180 E: -16.4, -21.0 to -13.2). In 1950-1983 it was within 3.5 umol/kg of 1984-1996 in most western regions, but 8-13 umol/kg higher at 36-46 N, 160-180 E, where the decline started first. The midpoint of the decline (ramp model) was 1989 (1979-1990) at 36-46 N, 170-180 E and 1991.5 (1980.5-2010) at 160-170 E. In the same years and places, the 26.4-26.6 layer thinned by 20-30 m. West of 160 E the decline came late: 2010.5 (2009.5-2014) at 36-46 N, 145-180 E and 2013.5 (2010.5-2014) at 145-160 E. From 170 E to the CalCOFI band the midpoint moved east at 0.14 yr per degree (-0.07 to 0.24; 86% of draws positive), about 2 cm/s, and reached CalCOFI near 2000.
3. **In the 160 E-180 ventilation region, oxygen follows the outcrop area with a lag of about 1 year.** With the EN4 outcrop area, detrended correlations of within-type O2 were r = 0.45 (36-46 N, 160-170 E; surrogate p = 0.003), 0.55 (28-42 N, 170-180 E; p = 0.004) and 0.52 (160-170 E; p = 0.027) at a lag of 1 year. The correlation is present in the ship era (1950-1999: 0.46-0.54) and in the Argo era (2000-2025: 0.34-0.66). Downstream the best lag was 5-6 years at 130-170 W (r = 0.52-0.71; only 130-140 W had p < 0.05, p = 0.024). At CalCOFI the lag was not resolved (p = 0.28).
4. **The outcrop explains part of the California low, but it does not forecast it better than persistence.** Fitted on 1950-2006, a lag model with the EN4 area >= 26.5 had the physical sign at CalCOFI (lag 8 yr, training r = 0.64) and forecast a 2007-2025 mean of -7.1 umol/kg against -14.6 observed (test RMSE 10.2; persistence 3.7). The pre-specified outcrop-window index forecast only -2.9. Across 14 regions, the pre-specified lag test passed in 2 (window index) and 4 (area >= 26.5) regions, all west of 180. A memory-kernel model (exploratory) passed in 6-8 regions, but not at CalCOFI.
5. **Most CMIP6 models do not ventilate sigma0 26.5 in the open North Pacific.** In 4 of 7 models (ACCESS-ESM1-5, CanESM5, CESM2, MPI-ESM1-2-LR), the winter surface density at 40-50 N, 150-170 E was 0.23-0.51 kg/m3 lower than in EN4, and the area >= 26.5 in the box was 0-0.12 million km2 in 1984-1996 (EN4: 1.39). The other three (GFDL-ESM4, IPSL-CM6A-LR, MRI-ESM2-0) have an outcrop, but its 2009-2025/1984-1996 ratio was 0.64-0.80 (EN4: 0.27). No 13-yr to 17-yr epoch pair in these three runs (1950-2025) fell below 0.54 (EN4: 0.23).

Interpretation: the within-type loss on sigma0 26.5 started where this density class is subducted in the central North Pacific (160 E-180, about 36-46 N, the dense Central Mode Water region). Winter surface water there became lighter, the outcrop of 26.5 shrank, less newly ventilated water entered the class, and the class thinned. The oxygen change then moved east with the flow and reached California about 10 years later. This agrees with the earlier water-type and float results and gives them a source and a mechanism. Models can miss the loss for two reasons that add to the low oxygen use per year of age found before (sci:sha256:66c86fe2...): most models do not ventilate this density in the open North Pacific, and the models that do ventilate it lose much less outcrop area than observed. The outcrop record does not explain the exact size and the steady level of the CalCOFI low after 2007; local circulation and mixing in the California Current also have an effect.

![Fig. 1](files/figures/fig1_maps.png)

## Question, hypotheses and tests

| Test | Hypothesis | Prediction | Result |
|---|---|---|---|
| T1 origin | The loss starts at the ventilation source and moves downstream | Earliest decline in the west; later to the east | Supported for 160 E-180 (1989-1992), then east to CalCOFI (about 2000). Not supported for the region near Japan (decline 2010-2014) |
| T2 preformed O2 | The loss is in the outcrop water itself | Near-outcrop loss as large and as early as downstream | Rejected for the early loss: near-outcrop water (36-46 N, 145-180 E) changed by -3.9 (-7.7 to -1.1) in 1997-2008, against -8.6 (36-46 N) and -9.3 (28-42 N) at 160-170 E |
| T3 outcrop | The 26.5 outcrop shrank before and during the loss | Smaller area and lower winter density after the mid-1990s | Supported: ship -0.15 kg/m3; EN4 area -73% |
| T4 lag forecast | Lagged outcrop area forecasts 2007-2025 O2 | Test RMSE below persistence, physical sign | Mixed: passes in 2-4 of 14 regions (west of 180); fails at CalCOFI |
| T5 models | CMIP6 models reproduce the outcrop and its shrinkage | Model outcrop area and ratio near EN4 | Rejected: 4 of 7 have no outcrop; 3 of 7 shrink by 20-36% |

T2 is limited: we did not calculate preformed O2. We used the timing and size of the near-outcrop within-type change as the test.

## Data

- **World Ocean Database 2023** (NOAA NCEI, public domain): OSD (bottle) and CTD observed-level files for WMO squares 1214-1217, 1314-1317 and 1414-1417 (20-50 N, 140-180 E; downloaded 2026-11-10; 135,118 casts with values on sigma0 26.2-26.8 and 153,513 cast-surface values with O2), and squares 7314-7317 and 7414-7417 read in place from the campaign store for the winter surface casts. Hashes: `files/provenance/wod_*.sha256`.
- **World Ocean Atlas 2023** monthly 1-degree climatology, January-April temperature and salinity (public domain).
- **EN4.2.2 g10 objective analyses** (Met Office; Non-Commercial Government Licence), January-April of 1950-2026, read with HTTP range requests. EN4 data and EN4-derived series are not in this bundle (see `files/NOTICE_external_data.md`).
- **CMIP6** Omon tos and sos, r1i1p1f1, historical + ssp245, seven models (CC BY 4.0), Google Cloud public Zarr.
- **Prior campaign results**: band series, onset draws and cell map of sci:sha256:b4d3d3f5... (28-42 N, 120-180 W); CalCOFI annual index of sci:sha256:d73b9f65....

## Methods

1. **Isopycnal values (west)** (`extract_wod.py`, from sci:b4d3d3f5): WOD quality flag 0; TEOS-10 sigma0 (gsw 3.6.23); linear interpolation to sigma0 26.2-26.8 with one level on each side within 100 m.
2. **Regional year series, epochs, onset** (`code/wod/`, from sci:b4d3d3f5, unchanged except the region set): cruise x 2.5 x 5 degree cell x quarter means; least squares with a quadratic latitude-longitude surface, quarter effects, year effects and a CTD offset; year effects relative to 1984-1996. Within-type O2 = O2 - b S, with b the within-cell O2-salinity slope of 1950-1996 in each region. Epoch changes and ramp-model midpoints (t0 = 1978-2015, duration 2-20 yr) use 300 bootstrap draws of cruises. Western regions: bands 28-42 N in 10-degree steps from 140 E to 180 (B140E-B170E); 36-46 N at 145-160 E (N145E), 160-170 E (N160E), 170-180 E (N170E) and 145-180 E (KOE_N); 25-36 N, 140-180 E (STG_W); 28-42 N, 140-180 E (W140_180).
3. **Winter surface casts** (`extract_surface.py`): January-April ship casts at 30-50 N; shallowest accepted level within 0-12 m.
4. **Public outcrop index** (`wod_outcrop_index.py`): ship sigma0 minus the WOA23 sigma0 of the same 1-degree cell and month; mean over 5 x 5 degree cells of cruise means for each year (delta). Box 30-50 N, 140 E-150 W, without the Sea of Japan and the Sea of Okhotsk. An area version shifts the WOA23 January-April maximum density map by delta. This assumes a uniform anomaly, so the area saturates at zero in many years after 1997.
5. **EN4 outcrop index** (`outcrop_index.py`, results not bundled): annual maximum of January-April top-level (5 m) sigma0 in each 1 x 1 degree cell; area with sigma0 in 26.4-26.6 (window, the pre-specified index) and >= 26.5, the southernmost latitude of 26.5 at 150 E-170 W, and the mean maximum density at 40-50 N, 150-170 E. Check against raw ship casts: `surface_check.py`.
6. **Lag structure** (`lag_structure.py`, exploratory): correlation of annual within-type O2 with the 3-yr mean outcrop index at lags 0-20 yr, raw and linearly detrended. Significance: 2000 (raw) phase-randomised surrogates of the index with the same power spectrum; p is the share of surrogates whose maximum over all lags is at least the observed maximum. Sub-period check: `split_period.py`.
7. **Out-of-sample test** (`outcrop_forecast.py`, pre-specified in `code/PLAN.md`): O2(t) = a + b U(t - L), L = 0-20 yr by leave-one-out error on 1950-2006; test on 2007-2025 against persistence of the 2002-2006 mean. Pass: test RMSE below persistence and b > 0. Exploratory memory kernel: U weighted by exp(-j/tau) over j = 0-30 yr, tau = 1-20 yr.
8. **CMIP6** (`cmip_outcrop.py`): the same indices from January-April tos and sos, moved to the 1-degree grid by the nearest model cell (at most 150 km).

Plan and changes: `code/PLAN.md` was written before we calculated western O2 values or outcrop-O2 fits. After the first results we added (a) within-type O2 to the epoch and onset tests, (b) the 36-46 N longitude split (N145E, N160E, N170E), (c) the memory-kernel model, the lag-structure and sub-period tests, (d) the public ship index and the EN4 surface check, and (e) the CMIP6 comparison. Item (d) became the bundled index because the EN4 terms do not permit CC BY redistribution of EN4-derived series.

## Results

### Outcrop change (`files/results/wod_outcrop/`, `files/results/en4_statistics/surface_check_epochs.csv`)

| Index | 1950-1983 | 1984-1996 | 1997-2008 | 2009-2025 |
|---|---|---|---|---|
| Ship surface sigma0 minus WOA23 (kg/m3), 95% CI | +0.008 (-0.011, +0.016) | +0.014 (-0.004, +0.028) | -0.160 (-0.181, -0.132) | -0.134 (-0.158, -0.118) |
| EN4 area sigma0 >= 26.5 (million km2) | 1.34 | 1.39 | 0.92 | 0.37 |
| EN4 area 26.4-26.6 (million km2) | 1.69 | 1.81 | 1.76 | 1.12 |
| EN4 mean max sigma0, 40-50 N, 150-170 E | 26.52 | 26.49 | 26.47 | 26.40 |
| EN4 outcrop latitude of 26.5, 150 E-170 W (N) | 41.7 | 40.7 | 41.3 | 42.6 |

The EN4 area >= 26.5 had minima in 1995-1997, 2010-2011 and 2014-2015 and decreased by 0.35 million km2 per decade over 1980-2025. These minima agree with Mecking and Drushka (2024, doi:10.5194/bg-21-1117-2024), who studied the 26.4-26.7 outcrop and Station P oxygen.

![Fig. 2](files/figures/fig2_outcrop_index.png)

### Western oxygen (`files/results/west/epochs_26.5.csv`, `onset_26.5.csv`)

| Region | Within-type O2, 1997-2008 | Within-type O2, 2009-2025 | Total O2, 2009-2025 | Midpoint, within-type (95%) | Layer 26.4-26.6, 2009-2025 (m) |
|---|---|---|---|---|---|
| N170E 36-46 N, 170-180 E | +5.6 (-8.3, +23.8), n = 6 | -1.6 (-29.4, +39.9), n = 3 | - | 1989 (1979-1990) | thinning, midpoint 1988 |
| N160E 36-46 N, 160-170 E | -8.6 (-15.5, -2.9) | -16.1 (-26.8, -10.8) | - | 1991.5 (1980.5-2010) | - |
| B170E 28-42 N, 170-180 E | -3.6 (-15.6, +11.6) | -13.2 (-25.2, -0.5) | -13.7 (-25.5, -1.0) | 1989 (1988-2006.8) | -18.6 (-22.7, -10.8) |
| B160E 28-42 N, 160-170 E | -9.3 (-13.6, -3.1) | -17.9 (-22.6, -9.9) | -15.1 (-20.6, -6.9) | 1999 (1988.5-2008.3) | -18.0 (-24.4, -10.4) |
| KOE_N 36-46 N, 145-180 E | -3.9 (-7.7, -1.1) | -16.4 (-21.0, -13.2) | -7.8 (-12.4, -3.7) | 2010.5 (2009.5-2014) | -0.4 (-3.1, +3.2) |
| N145E 36-46 N, 145-160 E | -4.1 (-8.1, -0.9) | -16.9 (-21.3, -12.5) | - | 2013.5 (2010.5-2014) | - |
| B140E 28-42 N, 140-150 E | -10.1 (-12.5, -7.7) | -16.1 (-19.6, -13.3) | -5.0 (-10.3, -0.6) | 1995 (1993-2010.5) | +1.8 (-1.1, +5.1) |
| STG_W 25-36 N, 140-180 E | -7.6 (-9.7, -5.4) | -15.4 (-17.8, -12.4) | -9.2 (-11.9, -5.3) | 2003 (1995.5-2005) | -5.0 (-6.4, -3.4) |
| W140_180 28-42 N, 140-180 E | -8.2 (-10.4, -6.1) | -16.8 (-19.4, -14.1) | -8.4 (-12.5, -4.3) | 2004 (1994-2012) | -0.3 (-2.3, +2.0) |

Units umol/kg; n = ship cruises with O2 in the epoch where it is small. The N170E region has few cruises after 1996, so its epoch changes are uncertain; its midpoint comes from the full annual series. In the west, the isopycnal became fresher and colder (salinity -0.1) and 20-39 m deeper. The fresher water type carries more O2, so the total change is smaller than the within-type change near Japan. The eastern bands of sci:b4d3d3f5 lost 20-38 umol/kg (total O2), with midpoints 1992-2004.

![Fig. 4](files/figures/fig4_timing_lag.png)

### Oxygen against the outcrop (`files/results/en4_statistics/lag_structure.csv`, `split_period_en4.csv`)

| Region | Best lag (yr) | r | Detrended r | Surrogate p (detrended) | Detrended r, 1950-1999 | Detrended r, 2000-2025 |
|---|---|---|---|---|---|---|
| N160E 36-46 N, 160-170 E | 1 | 0.66 | 0.45 | 0.003 | 0.53 | 0.40 |
| B160E 28-42 N, 160-170 E | 1 | 0.70 | 0.52 | 0.027 | 0.46 | 0.60 |
| B170E 28-42 N, 170-180 E | 1 | 0.48 | 0.55 | 0.004 | 0.48 | 0.66 (n = 9) |
| W140_180 28-42 N, 140-180 E | 1 | 0.71 | 0.54 | 0.062 | 0.54 | 0.34 |
| B140 28-42 N, 130-140 W | 6 | 0.74 | 0.71 | 0.024 | 0.47 | - |
| B160 28-42 N, 150-160 W | 5-6 | 0.73 | 0.66 | 0.12 | 0.34 | - |
| CalCOFI within-type index | 0-2 | 0.66 | 0.56 | 0.28 | - | - |

EN4 area >= 26.5, within-type O2. Near Japan (N145E, KOE_N) the best detrended lag was 19 yr (p = 0.03); we do not interpret this lag as physical. With the public ship index the correlations were weaker (detrended N160E r = 0.28, p = 0.19), because the sparse casts sample different places each year; only its epoch change is robust.

![Fig. 3](files/figures/fig3_oxygen_vs_outcrop.png)

### Out-of-sample forecasts (`files/results/en4_statistics/outcrop_forecast_best.csv`, `files/results/wod_outcrop/forecast/`)

At CalCOFI (observed 2007-2025 mean -14.6; persistence RMSE 3.7; training-mean RMSE 15.5): EN4 window lag model -2.9 (RMSE 14.1), EN4 area >= 26.5 lag model -7.1 (10.2), its kernel model -22.8 (11.4); ship-index lag model -5.7 (9.4), kernel -19.9 (7.3). No model beats persistence at CalCOFI. Passes of the pre-specified lag model: EN4 window 2 of 14 regions (B170E, W140_180), EN4 area 4 of 14 (B170E, N145E, STG_W, W140_180), ship index 4 of 14. Exploratory kernel models passed in 6-8 of 14, including the CalCOFI band (B120) for the ship index (-26.6 vs -24.0; RMSE 4.2 vs 5.8).

![Fig. 5](files/figures/fig5_forecast_test.png)

### CMIP6 (`files/results/cmip/`, `files/results/synthesis/cmip_outcrop_summary.csv`)

| Run | Area >= 26.5, 1984-1996 | Ratio 2009-2025/1984-1996 | Lowest ratio, all epoch pairs 1950-2025 | Max sigma0 40-50 N, 150-170 E, 1984-1996 (bias vs EN4) | Change |
|---|---|---|---|---|---|
| EN4.2.2 (observed) | 1.39 | 0.27 | 0.23 | 26.49 | -0.09 |
| GFDL-ESM4 | 1.07 | 0.64 | 0.61 | 26.48 (-0.01) | -0.04 |
| IPSL-CM6A-LR | 2.14 | 0.75 | 0.54 | 26.60 (+0.11) | -0.06 |
| MRI-ESM2-0 | 3.98 | 0.80 | 0.80 | 26.67 (+0.18) | -0.03 |
| ACCESS-ESM1-5 | 0.12 | 0.10 | 0.10 | 26.18 (-0.31) | -0.11 |
| CanESM5 | 0.00 | - | - | 26.26 (-0.23) | -0.13 |
| MPI-ESM1-2-LR | 0.07 | 0.54 | 0.26 | 26.18 (-0.31) | -0.00 |
| CESM2 | 0.00 | - | - | 25.98 (-0.51) | -0.14 |

Areas in million km2, densities in kg/m3. Single members (r1i1p1f1), historical to 2014 and SSP2-4.5 to 2025.

## Limitations

- EN4 is an objective analysis. It relaxes to climatology where data are few, mostly before 1990 in winter. The raw ship check supports the epoch change, but the ship index alone is too noisy to resolve the year-to-year lag structure. The strongest correlation results therefore depend on EN4.
- Surface density is a proxy for the winter mixed-layer density, and outcrop area is a proxy for subduction. We did not calculate subduction rates, preformed O2 or water age.
- We searched over lags, indices and regions. The surrogate test corrects for the lag search in each series, not for the number of regions and indices. Many tests do not reach p < 0.05, and the CalCOFI forecast fails against persistence.
- Ship O2 data are sparse at 160 E-180 after 1996 (3-33 cruises per epoch) and dense near Japan. Onset intervals at 160-180 E are wide.
- The within-type slope b is estimated per region from 1950-1996 data. In the west, mixing of Oyashio and Kuroshio waters gives large slopes (-113 to +6 umol/kg per salinity unit), so the within-type and total changes differ.
- The CMIP6 test uses one member per model; internal variability in the 2009-2025 epoch is not sampled. The model indices do not include the subarctic north of 50 N, where some models outcrop 26.5. We did not use model O2.
- The forecast and lag tests use published regional series of sci:b4d3d3f5 for the east and our own series for the west, with the same code.

## Reproduction

`files/code/run_all.sh SCRATCH RESULTS SHARED_DATASETS_ROOT` runs the full pipeline (about 1.5 h on 12 cores; downloads about 0.5 GB of WOD, 0.5 GB of WOA23, 0.3 GB of EN4 ranges and 2.5 GB of CMIP6 chunks into SCRATCH). Software versions: `files/code/requirements.txt`. gsw, wodpy and numcodecs go to a private folder named by EXTRA_PYLIB (the scripts run with `python -I`). The CalCOFI index and the eastern band results come from the cited publications (`sci read <zip> --file ...`). EN4-derived intermediate files stay in SCRATCH. Input hashes: `files/provenance/`. Terms and attribution of external data: `files/NOTICE_external_data.md`.

## Attribution

Text, figures and aggregate results: SCI baseline license (CC BY 4.0); code: MIT. The reused code from sci:sha256:b4d3d3f5... and sci:sha256:cc75ea4e... is under the same terms. EN.4.2.2 data were obtained from https://www.metoffice.gov.uk/hadobs/en4/ and are (c) British Crown Copyright, Met Office, provided under a Non-Commercial Government Licence; they are not redistributed here. CMIP6 output: CC BY 4.0, WCRP and the modelling groups. WOD and WOA23: NOAA NCEI.
