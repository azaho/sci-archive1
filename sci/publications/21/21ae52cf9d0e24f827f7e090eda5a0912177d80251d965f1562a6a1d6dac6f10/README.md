# North Pacific oxygen loss on sigma0 26.0-26.7 (2009-2025 vs 1984-1996) equals a 0.06-0.11 kg/m3 lighter AOU-profile shift, 40-70% of winter surface lightening; CalCOFI nitrate drifted vs GLODAP

Job sci-1107-dell-earth-and-ocean-sciences-83962f461166, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found an oxygen (O2) loss on the sigma0 = 26.5 kg/m3 surface off California and along the North Pacific Current. It is mostly a loss inside water types (sci:sha256:ea67ca59...). The loss started near 160 E-180 around 1990, where the winter outcrop of this density shrank, because winter surface water there became 0.15 kg/m3 lighter (sci:sha256:84f111c0...). That study showed a correlation in time. It did not show whether the outcrop change is large enough to make the oxygen loss.

We give a quantitative test. If winter surface water becomes lighter by delta and the ventilation pathways do not change, then water that now reaches a density sigma was ventilated where sigma + delta outcropped before. Tracers that the pathway sets (apparent oxygen utilisation, AOU; nitrate; phosphate) then obey P_late(sigma) = P_ref(sigma + delta). We fit delta to the AOU change on sigma0 26.0-26.7 in each region. This "equivalent density shift" turns the oxygen loss into a density unit. We can then compare it directly with the measured surface lightening. We used 3 independent data sets: World Ocean Database (WOD) ship bottles and CTDs (15-50 N, 120-180 W), GLODAPv2.2023 (also west of 180), and the CalCOFI bottle database.

Main results (changes 2009-2025 minus 1984-1996; 95% cruise-bootstrap intervals; CalCOFI data end in 2021):

1. **O2 loss is equal to a lighter shift of 0.06-0.105 kg/m3 along 28-42 N.** With WOD, delta_AOU was 0.095 (0.082-0.118) at 170-180 W, 0.060 (0.030-0.080) at 160-170 W, 0.080 at 130-160 W, 0.105 (0.100-0.115) at 120-130 W and 0.095 (0.085-0.105) off California. The CalCOFI bottle data gave 0.100 (0.090-0.105) and GLODAP gave 0.06-0.13 in the same regions. The shift was smaller at 42-50 N (0.045) and 20-28 N (0.040). O2 at sigma0 26.5 fell by 10-24 umol/kg. O2 solubility changed by less than 2 umol/kg, so dO2 is approximately -dAOU.
2. **The winter surface lightening is sufficient.** The measured lightening of winter surface water at 30-50 N, 140 E-150 W was 0.148 (0.131-0.171) kg/m3 (ship casts minus WOA23, sci:84f111c0). A full shift of this size gives 28-42 umol/kg more AOU at 26.5, more than observed. The observed shift is 41-71% of the surface lightening along 28-42 N (transfer fraction 0.6 at 120-180 W, 0.68 at CalCOFI). Pre-specified test T2'(a) fails for most regions (the intervals do not include 0.131), so the loss is a partial shift, not a complete one.
3. **Off California the shift follows surface lightening with a lag, but the lag is not resolved.** In 5-yr windows, the CalCOFI shift was -0.005 to 0.010 in 1975-1999, rose to 0.050 in 2000-2004 and 0.085 in 2005-2009, and stayed at 0.095-0.105 in 2010-2021. It was also positive in 1950-1969 (0.025-0.055), when the surface was lighter than in 1984-1996. Annual CalCOFI shifts correlate with the 3-yr mean surface lightening at r = 0.63-0.70 for all lags of 3-13 yr (best lag 11 yr, slope 0.41). Phase-randomised surrogates do not reject chance (p = 0.13; detrended p = 0.25).
4. **The shape of the change supports a shift better than a uniform slowdown at denser levels, not at lighter levels.** Inside the fit range, the shift (R2 0.94-0.99 with WOD) and a change proportional to AOU (uniform slowdown or uniform respiration increase; R2 0.85-0.99) both fit better than a constant offset (R2 0.55-0.90). On held-out denser levels (26.75-26.90), the shift had a smaller error than the proportional shape in 21 of 21 region-data pairs. On held-out lighter levels (25.80-25.95) it was better in only 7 of 22. At the denser levels, a constant offset had the smallest error in 18 of 21. The loss is largest at 26.4-26.7 and decreases below 26.75 faster than any one-parameter shape gives. This agrees with a source in the classes that outcrop in the open North Pacific in winter.
5. **On sigma0 26.5 the water became cooler and fresher from 130 W to 180, as surface warming predicts.** Conservative temperature changed by -0.17 to -0.28 C and absolute salinity by -0.03 to -0.055 g/kg (WOD, 130-180 W). This is the Bindoff-McDougall "pure warming" signature. Near the coast (120-130 W, CalCOFI), the water became warmer and saltier (+0.08 to +0.09 C, +0.015 to +0.017 g/kg).
6. **The nutrient test cannot separate a shift from Redfield respiration offshore. An apparent CalCOFI nitrate deficit agrees with a measurement offset.** A pure shift gives a nitrate:AOU change ratio equal to the vertical ratio (kappa = 1). Redfield respiration on the same path gives kappa = 0.45-0.88. Offshore, kappa_N was 0.6-1.5 with wide intervals. The CalCOFI bottle data gave kappa_N = 0.44 (0.38-0.50), below both. This is the CalCOFI "N:P decrease". GLODAP cruises in the same region gave kappa_N = 0.88 (0.72-1.22). At crossovers (75 km, 45 days) on sigma0 26.6-27.0, CalCOFI nitrate minus GLODAP nitrate changed from +0.05 (1985, 1994) to -0.87 umol/kg (2011, 2013, 2016), with no phosphate change. When we remove this offset change, the CalCOFI ratio becomes 0.112 (kappa_N 0.92). CalCOFI O2 minus GLODAP O2 also changed by -2.1 umol/kg.

Interpretation: on the 26.0-26.7 class, the measured winter surface lightening at the central and western North Pacific outcrop is large enough to give the full basin-wide oxygen loss along the North Pacific Current. The loss is equal to about 60% of a complete shift. This gives a quantity that a model must reproduce: delta_AOU / delta_surface = 0.4-0.7. A model gives the observed loss only if (a) the classes near 26.5 outcrop in its open North Pacific and (b) its winter surface water there becomes lighter by about 0.15 kg/m3. The earlier campaign results show that 4 of 7 CMIP6 models do not meet (a). In the same box metric (maximum winter sigma0 at 40-50 N, 150-170 E, 2009-2025 minus 1984-1996), the 3 models that meet (a) became lighter by 0.03-0.06 kg/m3, which is 34-67% of the EN4 change of 0.093 (sci:84f111c0). If the transfer fraction is the same in a model, these models give 7-15 umol/kg instead of 22 umol/kg off California. The published single-member values of two of them (sci:cc75ea4e: GFDL-ESM4 -15, IPSL-CM6A-LR -3.4 umol/kg) bracket this range, and the two non-outcropping models in that study (ACCESS-ESM1-5, CanESM5) had no loss although their surface became lighter by 0.11-0.13. This is a consistency argument, not a model test: we did not use model O2 here. The shape and time tests support a partial shift, but they do not exclude a contribution from slower circulation or more respiration.

![Fig. 1](files/figures/fig1_aou_profiles.png)

## Question, hypotheses and tests

Plan: `files/code/PLAN.md`. It was written before any profile or fit was calculated. Amendment A (also before any result) replaced the salinity shift by the AOU, nitrate and phosphate shifts, because temperature and salinity on an isopycnal change with the cause of the lightening.

| Test | Hypothesis | Prediction | Result |
|---|---|---|---|
| T1' delta per region and tracer (pre-specified) | The loss is a density shift | One delta per region fits AOU over 26.0-26.7 | Supported for shape inside the fit range (R2 0.94-0.99, WOD), but a proportional shape fits equally well |
| T2'(a) surface magnitude (pre-specified) | delta_AOU = surface lightening 0.131-0.171 | Interval overlaps 0.131 | Not met in most regions: delta_AOU is 0.04-0.105 (WOD). Only GLODAP intervals at 120-130 W, CalCOFI region and 120-180 W reach 0.131. A partial shift (40-70%) |
| T2'(b) nitrate = AOU shift (pre-specified) | delta_NO3 and delta_AOU overlap | Overlapping intervals | Met in GLODAP regions with data; not met in CalCOFI data (nitrate offset, result 6) |
| T2'(c) variance (pre-specified) | Shift explains >= 50% of AOU anomaly | R2 >= 0.5 | Met in all 28-42 N regions |
| T3' O2 budget at 26.5 (pre-specified) | Loss beyond a full shift is positive | dAOU - shift(0.145) > 0 | The opposite: observed dAOU is 7-27 umol/kg (WOD) smaller than a full shift (see `files/results/synthesis/shift_summary_all.csv`, column excess265) |
| T4' spice (pre-specified) | Lightening by warming gives cooler, fresher isopycnals | dCT < 0, dSA < 0 offshore | Supported at 130-180 W; the opposite near the coast |
| Held-out levels (exploratory) | Shift beats proportional off the fit range | Smaller error at 26.75-26.90 and 25.80-25.95 | Denser: 21/21; lighter: 7/22 |
| Lag (exploratory) | CalCOFI shift follows surface lightening | Significant lagged correlation | r = 0.70 at 11 yr, plateau 3-13 yr, surrogate p = 0.13 (not significant) |
| Crossover (exploratory) | CalCOFI nitrate is stable against GLODAP | No change of offset | Offset changed by -0.92 umol/kg (5 cruises against 3) |

## Data

- **World Ocean Database 2023** (NOAA NCEI, public domain): OSD and CTD observed-level files of WMO squares 7212-7217, 7312-7317, 7412-7417, read in place from the campaign store (40 files; URLs and SHA-256 in `files/provenance/input_files.json`). CTDO7412 (40-50 N, 120-130 W, coastal Oregon and Washington) was not used. Its extraction did not finish in 2 h on the loaded host. It does not affect the main regions, except the 40-42 N cells of 120-130 W.
- **GLODAPv2.2023 Pacific** (CC BY 4.0), flag-2 values, 10-55 N, 120 E-110 W: 11,077 casts, 473 cruises.
- **CalCOFI bottle database** 1949-03 to 2021-05 (CC BY 4.0): 28,755 casts with values on the density grid, 388 cruises.
- **Surface lightening index**: WOD January-April ship casts minus World Ocean Atlas 2023, 30-50 N, 140 E-150 W, from sci:sha256:84f111c0... (epoch values: 1984-1996 +0.014; 1997-2008 -0.160; 2009-2025 -0.134 kg/m3; annual series in its `wod_outcrop_index.csv`).

## Methods

1. **Density grid** (`extract_wod_grid.py`, `glodap_grid.py`, `calcofi_grid.py`). For each cast: data source quality flags; TEOS-10 (gsw 3.6.23) absolute salinity, conservative temperature and sigma0; running maximum of sigma0 with depth; linear interpolation of depth, CT, SA, O2, NO3 and PO4 to sigma0 = 25.40-27.20 in steps of 0.05, with one accepted level on each side and a bracket gap of at most 100 m. Levels shallower than 75 m are not used. O2 solubility (gsw.O2sol at zero pressure) and AOU are calculated at each level. CalCOFI nutrients are converted from umol/L to umol/kg.
2. **Cell-matched anomalies** (`shiftlib.py`, `run_shift.py`). Units are cruise x 2.5 lat x 5 lon degree cell means. Reference profiles R_c(sigma) are the means of 1984-1996 units in each cell; late profiles L_c are the means of the units in the late period. The regional anomaly A(sigma) is the mean of L_c - R_c over cells with both, weighted by the number of late units. The regional reference profile Rbar is the integral of the weighted mean vertical (density) gradient of R_c over the same cells.
3. **Shift fit.** S(sigma; delta) = Rbar(sigma + delta) - Rbar(sigma). delta is the least-squares value over sigma0 26.0-26.7, scanned from -0.40 to 0.60 in steps of 0.005. Competing one-parameter shapes: a constant c, and f x R_abs(sigma), with R_abs the weighted mean reference profile (uniform fractional increase of AOU). R2 = 1 - SSE / sum(A^2).
4. **Uncertainty.** 300 bootstrap draws of cruises, separately in the reference and the late period (5-yr windows: 100 draws for CalCOFI and the first six GLODAP windows, 30 draws for WOD and the later GLODAP windows; annual CalCOFI: 30 draws). We give 2.5-97.5 percentiles. With 1-3 cruises in a period, the intervals are too narrow; we show regions with at least 2 late cruises only.
5. **Nutrient ratio test** (`synthesis.py`). Observed change ratio r = least-squares slope through zero of A_NO3 against A_AOU over 26.0-26.7; vertical ratio g = slope of R_abs,NO3 against R_abs,AOU over the same levels; kappa = r / g. Redfield respiration on an unchanged path gives kappa = (16/170 to 16/150) / g; a pure preformed-O2 change gives kappa = 0. Phosphate in the same way (1/170 to 1/150).
6. **Held-out levels** (exploratory). The three shapes are fitted on 26.0-26.7 and compared by RMSE on 26.75-26.90 and 25.80-25.95 for each bootstrap draw.
7. **CalCOFI-GLODAP crossovers** (`crossover_calcofi_glodap.py`, exploratory). CalCOFI casts within 75 km and 45 days of a GLODAP cast at 29-36 N, 116-126 W; per-pair mean difference on sigma0 26.6-27.0 and 26.3-26.6; per-cruise medians; era means.
8. **Lag test** (`lag_transfer.py`, exploratory). Annual CalCOFI delta_AOU against the 3-yr running mean of the surface lightening at lags 0-15 yr; 1000 phase-randomised surrogates of the surface index; p is the share of surrogates whose maximum r over lags is at least the observed maximum.

## Results

Full tables: `files/results/tables.md`; all region x tracer x period values: `files/results/synthesis/shift_summary_all.csv`; anomaly and reference profiles: `files/results/epochs/*_profiles.csv`.

### Equivalent shift, 2009-2025 minus 1984-1996 (selected; all rows in `files/results/tables.md`)

| Region | Data | Cruises ref/late | dO2 at 26.5 (umol/kg) | delta_AOU (kg/m3) | Transfer delta/0.148 |
|---|---|---|---|---|---|
| 28-42 N, 140-160 E | GLODAP | 15/74 | -10.2 (-17.1, +1.2) | 0.055 (0.020, 0.065) | 0.37 |
| 28-42 N, 160 E-180 | GLODAP | 13/40 | -13.5 (-24.0, -5.7) | 0.060 (0.030, 0.085) | 0.41 |
| 28-42 N, 170-180 W | WOD | 46/23 | -15.3 (-18.8, -13.7) | 0.095 (0.082, 0.118) | 0.64 |
| 28-42 N, 160-170 W | WOD | 54/27 | -10.3 (-17.2, -3.0) | 0.060 (0.030, 0.080) | 0.41 |
| 28-42 N, 150-160 W | WOD | 54/19 | -21.4 (-27.5, -15.8) | 0.080 (0.060, 0.095) | 0.54 |
| 28-42 N, 140-150 W | WOD | 23/7 | -24.4 (-29.4, -19.8) | 0.080 (0.065, 0.095) | 0.54 |
| 28-42 N, 130-140 W | WOD | 27/6 | -21.3 (-30.7, -8.2) | 0.080 (0.045, 0.115) | 0.54 |
| 28-42 N, 120-130 W | WOD | 167/48 | -23.7 (-25.8, -21.3) | 0.105 (0.100, 0.115) | 0.71 |
| CalCOFI, 30-35 N | WOD | 97/45 | -22.4 (-24.4, -20.2) | 0.095 (0.085, 0.105) | 0.64 |
| CalCOFI, 30-35 N | CalCOFI | 58/49 | -22.5 (-23.7, -21.1) | 0.100 (0.090, 0.105) | 0.68 |
| CalCOFI, 30-35 N | GLODAP | 4/3 | -28.9 (-47.8, -17.9) | 0.125 (0.085, 0.158) | 0.85 |
| 28-42 N, 120-180 W | WOD | 261/88 | -21.1 (-24.0, -19.0) | 0.090 (0.085, 0.105) | 0.61 |
| 42-50 N, 130-180 W | WOD | 154/63 | -10.9 (-17.0, -4.6) | 0.045 (0.025, 0.065) | 0.30 |
| 20-28 N, 130-180 W | WOD | 242/108 | -12.3 (-14.3, -10.2) | 0.040 (0.035, 0.050) | 0.27 |

In 1997-2008 (surface lightening 0.173), the shift was 0.020 (0.010-0.040) at 170-180 W and 0.035 (0.010-0.060) at 160-170 W, but 0.050-0.065 at 120-160 W and 0.045-0.055 off California (WOD and CalCOFI). Thus in the first decade of the lightening the eastern bands had more equivalent shift than the bands near 180. A simple eastward advection from 160 E-180 does not explain this.

![Fig. 2](files/figures/fig2_equivalent_shift.png)

### Time series

![Fig. 4](files/figures/fig4_time_series.png)

`files/results/windows/` (5-yr windows), `files/results/lag/` (annual CalCOFI series and lag regressions).

### Nutrients and the CalCOFI crossover

![Fig. 3](files/figures/fig3_nutrient_ratio.png)

| Crossover CalCOFI minus GLODAP (umol/kg) | 1984-1996 | 1997-2008 | 2009-2025 |
|---|---|---|---|
| Nitrate, sigma0 26.6-27.0 | +0.05 (2 cruises) | -0.66 (4) | -0.87 (3) |
| Phosphate, sigma0 26.6-27.0 | -0.04 (3) | -0.05 (4) | -0.04 (3) |
| O2, sigma0 26.6-27.0 | -0.79 (3) | -0.55 (4) | -2.89 (3) |

The GLODAP cruises are adjusted to a common reference by crossover analysis; the CalCOFI database values are not. We cannot tell from these data which data set changed. Changes of nitrate relative to phosphate (N:P, N*) in CalCOFI data after the 1990s, such as the decreases of N:P in the Southern California Bight reported by Bograd et al. (2015, Deep-Sea Research II), should be checked against this offset. The CalCOFI O2 loss on 26.5 can be about 2 umol/kg (10%) too large if the O2 offset is in CalCOFI.

## Limitations

- The shift model assumes unchanged pathways and a uniform lightening over all outcrop regions of 26.0-26.7. The only measured lightening is for one box (30-50 N, 140 E-150 W) and for the ship epochs; the eastern outcrops (Gulf of Alaska) are not in it.
- Inside the fit range, a uniform fractional increase of AOU (slower circulation or more respiration) fits as well as the shift. Only the denser held-out levels prefer the shift, and a constant offset is better still there. The tests show that the outcrop change is sufficient in size; they do not show that it is the only cause.
- The lag of the CalCOFI shift behind the surface index is not significant against red-noise surrogates. The annual slope (0.41) is lower than the epoch transfer (0.68), as expected when the predictor is noisy.
- GLODAP has 1-6 cruises per region and period in most offshore bands; its bootstrap intervals are too narrow there. WOD CTD O2 values are used without a per-cruise calibration; the bottle-only WOD results (`wodosd`) are similar.
- The nitrate test is weak offshore (wide intervals). The crossover estimate uses 2-3 GLODAP cruises per era near California.
- The comparison with CMIP6 uses published surface statistics and does not use model O2 in this study. A direct test with model O2 on each model's own outcropping classes is open. The host network gave about 0.05-0.08 MB/s to the CMIP6 store during this job, so we did not download model fields.
- Exploratory analyses (held-out levels, lag, crossovers, 5-yr windows) were added after the first results; they are labelled as such.

## Reproduction

`files/code/run_all.sh SCRATCH SHARED_DATASETS_ROOT CAMPAIGN_DIR` runs the full pipeline (about 4 h on the loaded 23-CPU host; the WOD extraction takes most of the time). It writes all cast-level intermediates to SCRATCH. gsw 3.6.23 and wodpy 1.6.2 go to the folder named by EXTRA_PYLIB; the scripts run with `python -I`. Software versions: `files/code/requirements.txt`. Annual CalCOFI series: `run_annual.sh SCRATCH/res calcofi CC SCRATCH/calcofi_grid.npz`, then `lag_transfer.py`. WOD windows: `run_windows.sh` (30 draws). Tables: `make_tables.py`. Input files and SHA-256: `files/provenance/input_files.json`. External-data terms: `files/NOTICE_external_data.md`.

## Attribution

Text, figures and aggregate results: SCI baseline license. Code: the same terms; `extract_wod_grid.py` is adapted from code in sci:sha256:b4d3d3f5.... WOD 2023 and WOA23: NOAA NCEI. GLODAPv2.2023: Lauvset et al. (2024), CC BY 4.0. CalCOFI: Data from CalCOFI (https://calcofi.org/), CC BY 4.0. Cited campaign publications: sci:sha256:84f111c04cb701ca1a33b3ebf3490356bfecb5c83079f2b5f1615de273baf0b4, sci:sha256:b4d3d3f5534b4c2d6bd3845a14a77ced4774da841c0da86c5517bcfd04a8e3ce, sci:sha256:ea67ca59c8c830609ef22a9e4feaddc1ba6a3e2aa317a0afefc81f17fcfc03e3, sci:sha256:cc75ea4ee42bb0552f162242a833759f9e12e921051e27040dc1af4ff6b89015, sci:sha256:e7596e2a83aa1ee8b6d412ffc4fc94299e9b19d6bc0a40e33a1d4db7cddd3939.
