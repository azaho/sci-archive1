# HadISST1 and AMIP 1.1.9 SST warm 13-26% too slowly at 60S-60N in 1982-2022 (ship-buoy bias), so their Green's-function pattern effect is 0.12-0.16 W m-2 K-1 too strong; HadISST1 steps in June 2020

**Job** sci-1107-hp-earth-and-ocean-sciences-4495ad5e1988 · **campaign** 11_07_2026 · **topic** earth-and-ocean-sciences · **machine** hp · **model** Claude Opus 5.5 (claude-opus-5-5) · **analysis date** 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## Question

Atmosphere models get their observed SST from two boundary datasets: HadISST1 (Met Office) and PCMDI-AMIP (AMIPII). After 1981, AMIPII comes from NOAA OI SST v2. Studies of the historical "pattern effect" force models with these datasets, and the result changes from one SST dataset to the next (Andrews et al. 2022; Modak and Mauritsen 2023). Earlier campaign work (sci:sha256:78d7f2e0) found the same spread in five Green's functions: over 1982-2022, the pattern term goes from -0.50 to -0.75 W m-2 K-1. HadISST1 gives the most negative value.

We asked two questions:

1. Do documented input changes in the two AMIP datasets cause artifacts?
2. Does the spread of the pattern term between SST products come from their SST patterns, or from their different warming rates?

The Met Office service notes for HadISST1 give the input changes. In situ data come from HadSST2 until 2020 and from unadjusted HadSST4 from January 2021. "No adjustment is made to account for changing ship biases and the known offset between buoy and ship measurements". The satellite source changed from NOAA to Met Office MetOp retrievals in June 2020 ("no obvious discontinuity"). The sea-ice source changed in January 2009. OI SST v2 also uses unadjusted ship and buoy data.

## Main results

All values are for 60S-60N ice-free SST on a fixed set of 1366 5-degree boxes, monthly, 1982-2022 unless stated otherwise. P is the Green's-function pattern term (feedback minus the uniform-warming feedback, per K of 60S-60N SST), as a 5-model mean (CAM5, CanESM5, ECHAM6, GFDL-AM4, HadAM3). The 95% intervals come from a 3-year moving-block bootstrap.

1. **HadISST1 warms 0.028-0.047 K per decade too slowly. The missing ship-buoy adjustment explains most of this.**
   - The 60S-60N trend is 0.094 K per decade in HadISST1 and 0.110 in AMIP 1.1.9. It is 0.122 in ERSSTv5, 0.127 in ESA CCI v3 (satellite only, no in situ data), 0.137 in step-corrected DOISST and 0.142 in COBE-SST2. Thus HadISST1 warms 26% and AMIP 1.1.9 13% slower than CCI.
   - HadSST4.2 median minus HadSST4.2 unadjusted is the bias adjustment that HadISST1 does not apply. Over 1982-2022 it gives -0.025 K per decade of false cooling. The time history agrees with the observed drift: about -0.11 K from 1983 to 2016, against -0.15 K in HadISST1 minus the in situ reference (Figure 1).
   - When we add this adjustment, the drift of HadISST1 changes from -0.033 to -0.008 against CCI, from -0.028 to -0.003 against ERSSTv5, and from -0.047 to -0.023 against COBE-SST2.
   - At 146 tropical moorings (1993-2022), HadISST1 minus buoy drifts by -0.025 K per decade (-0.056 to +0.005). The adjusted version drifts by +0.009.
   - For AMIP 1.1.9 / OI v2 the drift is smaller: -0.018 against CCI, -0.012 against ERSSTv5, -0.032 against COBE-SST2. At the moorings OI v2 has no drift (-0.004), because it follows the buoys there. The full adjustment over-corrects OI v2 (+0.007 against CCI, +0.030 at the moorings). For OI v2, the adjustment is therefore an upper estimate.
   - The spatially resolved adjustment did not improve the box-level trend maps against CCI or ERSSTv5 (demeaned RMS unchanged). The uniform adjustment is thus our main version. The spatial version is a sensitivity test.

2. **The spread of the pattern term between products is mostly a spread of warming rate ("dilution").**
   - P = Q / T. Here Q is the radiative effect of the non-uniform part of the warming (trend of N minus λ_u times trend of T) and T is the 60S-60N SST trend. A near-uniform drift changes T but leaves Q almost unchanged.
   - Across the six published products (HadISST1, AMIP 1.1.9, ERSSTv5, COBE-SST2, DOISST, CCI), P correlates with 1/T with r = -0.92 (1982-2022) and r = -0.91 (1982-2014). For four of the five models, r is -0.85 to -0.96 (ECHAM6: -0.53).
   - Q is similar in all products: -0.069 to -0.085 W m-2 per decade, while T goes from 0.094 to 0.171. At one common T, the range of P falls from 0.25 to 0.13 W m-2 K-1 (1982-2022) and from 0.45 to 0.21 (1982-2014) (Figure 2).
   - HadISST1 has the most negative P (-0.75) only because it has the lowest T. Its Q (-0.071) is the same as that of AMIP 1.1.9 and close to CCI (-0.069). At the reference trends (0.122-0.142), HadISST1 and AMIP 1.1.9 both give P = -0.50 to -0.58.

3. **The bias correction makes the AMIP-dataset pattern effect weaker by 0.12-0.16 W m-2 K-1 (1982-2022) and by 0.15-0.19 (1982-2014).**
   - Uniform adjustment only, 1982-2022: HadISST1 P changes from -0.750 to -0.595 (difference -0.155; all five model intervals exclude zero). AMIP 1.1.9 changes from -0.647 to -0.528 (-0.119; five of five).
   - Uniform adjustment only, 1982-2014 (the CMIP6 amip-piForcing period): HadISST1 changes from -1.18 to -0.98 (-0.19). AMIP 1.1.9 changes from -1.03 to -0.88 (-0.15).
   - With the step corrections as well, HadISST1 gives -0.62 and AMIP 1.1.9 gives -0.46 (1982-2022).
   - With the spatial adjustment, the values are -0.49 and -0.34. This is an upper estimate, because the adjustment pattern changes Q through the west-east Pacific weights of the Green's functions.
   - Against CCI, the raw HadISST1 P is more negative by 0.21 (four of five model intervals exclude zero). After the correction the difference is 0.08 (two of five).

4. **HadISST1 has a warm step at its June 2020 satellite-source change (Figure 3).**
   - In a break scan of HadISST1 minus the in situ mean (ERSSTv5, COBE-SST2, HadSST4.2), the largest 60S-60N and 20-60S breaks after the drift correction fall in 2020-06: +0.030 K (t = 4.2) and +0.053 K (t = 3.7).
   - Against CCI, which uses no in situ data, the 2020-06 step is +0.088 K at 20-60S (t = 4.3) and +0.103 K at 40-60S (t = 4.4).
   - At the moorings, HadISST1 minus buoy rises by +0.09 K from 2018-06..2020-05 to 2020-06..2022-12 (tropical east Pacific +0.14 K). CCI changes by -0.005 K and ERSSTv5 by +0.03 K.
   - Box fits with in situ data give +0.09 K at 40-60S and +0.08 K in the tropical east Pacific at 2020-06. In situ data show a partial return (-0.05 K) in 2021-01, when the in situ source changed. CCI shows a second warm step at that date, so the split between the two dates depends on the reference.
   - The step warms the east Pacific and the Southern Ocean. It therefore makes P less negative: removing it makes HadISST1 P more negative by 0.05 (1982-2022) and 0.11 (2001-2022; five of five models). Thus the step partly offsets the drift effect in recent windows.

5. **The OI v2 / AMIP 1.1.9 mid-2018 Southern Hemisphere cold step (sci:sha256:9e1a3e72) is confirmed against CCI.** The CCI comparison was not available in 78d7f2e0. The break scan of AMIP 1.1.9 minus CCI has its 60S-60N maximum at 2018-07 (-0.045 K, t = -3.8) and its 20-60S maximum at 2018-04. Against in situ data the step is -0.084 K at 20-60S (t = -9.1). Its removal changes 1982-2022 P by +0.08 and 2001-2022 P by +0.23 (five of five models).

## What this means

- The observational spread in the historical pattern effect from SST datasets mixes two things: the SST pattern and the warming rate. A Green's-function or AMIP estimate normalised by the dataset's own warming inherits any near-uniform drift as a proportional error in the pattern term. Because of a known, documented bias, HadISST1 is the product with the lowest 1982-2022 warming.
- With a correct warming rate, HadISST1 and AMIP 1.1.9 do not give a stronger pattern effect than the other products. Their pattern term at the reference warming (-0.50 to -0.58) lies inside the range of ERSSTv5, COBE-SST2, CCI and corrected DOISST (-0.51 to -0.67).
- Pattern-effect and feedback studies that use HadISST1 after June 2020 should allow for its warm step, as studies with AMIP 1.1.9 after mid-2018 should allow for its cold step.

## Methods

**Data.** Monthly HadISST1 (to 2026-09), PCMDI-AMIP 1.1.9 tos (to 2022-12), OI SST v2 1-degree, ERSSTv5, COBE-SST2 and DOISST v2.1 come from the shared campaign store and are put on a common 1-degree grid and 5-degree boxes (60S-60N, fixed ice-free mask; code 01, 02 from 9e1a3e72). We use HadSST4.2 median and unadjusted 5-degree anomalies. ESA SST CCI Analysis L4 v3.0.1 (CDR to 2021, ICDR 2022 to 2024-06) was read for every 6th day at one pixel per 1-degree cell (fetch_cci.py, 03). Sixteen coastal boxes never reach 80% CCI cover, so we fill them each month from neighbouring CCI boxes (e-folding 5 degrees). The step-corrected DOISST boxes come from 9e1a3e72, the 5-degree Green's functions (GFMIP) from 78d7f2e0, and GTMBA daily mooring SST from 87b87a67.

**Adjustment (10_adjust.py).** adj = HadSST4 median - HadSST4 unadjusted. We smooth adj in space (weights exp(-d/10 degrees) over boxes with data, plus 5 and 20 degrees as tests) and in time (12-month running mean). The uniform version uses the 60S-60N area mean of adj. Adjusted product = product + adj. Steps are fitted per box against the in situ mean (and separately against CCI) after the adjustment: HadISST1 at 2020-06 and 2021-01 (window 2016-2025), OI v2 at 2018-06 (window 2010-2022). The step maps are smoothed (e-folding 10 degrees) and subtracted.

**Feedback (20_feedback.py).** N(t) = Σ J_b A_b(t) (box Jacobians of each model), T(t) = area-weighted mean anomaly. λ = trend(N)/trend(T), λ_u = Σ J_b, P = λ - λ_u, Q = trend(N) - λ_u trend(T). Version differences use a 3-year moving-block bootstrap of annual means (500 draws per model). "Range at common T" = (max Q - min Q) / mean T over the product set.

**Validation (30_moorings.py, 40_validate.py).** Drift = OLS trend of version minus reference (region means and box maps). Mooring check: two-way (buoy offset + common month) model of product minus buoy at 146 GTMBA moorings. Break scan: mean shift in ±36-month windows, with a t-value corrected for lag-1 autocorrelation, for each month 2003-2023.

## Limitations

- **Unknown true trend.** The references disagree: ERSSTv5 0.122, CCI 0.127, corrected DOISST 0.137, COBE-SST2 0.142 K per decade (1982-2022), and ERSSTv5 is low in 1982-2014 (0.094). The size of the bias in the AMIP datasets therefore has an uncertainty of about ±0.01 K per decade. The resulting P uncertainty is about ±10%.
- **Approximate adjustment.** HadISST1 used HadSST2 (not unadjusted HadSST4) until 2020. Its satellite data are tied to in situ data only on large scales, and near buoys it follows the buoys. The HadSST4 adjustment is therefore an approximation. It matches HadISST1 better than OI v2, which it over-corrects. We used only the HadSST4 median, not its 200-member ensemble.
- **60S-60N Green's functions only.** These are linear Green's functions for 60S-60N ice-free SST. The SST poleward of 60 degrees and sea ice are held fixed. The feedback is per K of 60S-60N SST, not per K of global near-surface air temperature. Full AMIP simulations include sea ice and the polar oceans (where HadISST1 also has a 2009 sea-ice discontinuity). Andrews et al. (2022) found a less negative post-1980 feedback in models forced with HadISST1 than with AMIPII. This study does not explain that result.
- **Models.** The five Green's functions differ by a factor of about 3. The dilution correlation is weaker for ECHAM6 (r = -0.53).
- **Short-window noise.** The 2001-2022 values of P are close to zero and noisy, so the drift effect is not clear there.
- **2020-2021 split.** The split of the HadISST1 step between 2020-06 and 2021-01 depends on the reference. CCI has a CDR-to-ICDR change in 2022, and the in situ products have their own errors. The moorings are assimilated in all products, so they test the analyses only near buoys.

## Files

- `files/code/`: full pipeline (`run_all.sh`; steps 01-90). Python 3.12 with numpy, pandas, netCDF4, matplotlib. `fetch_cci.py` writes only to local scratch. `ipv4/sitecustomize.py` forces IPv4 name resolution on hosts with broken IPv6.
- `files/results/`: `feedback_by_version.csv` (T, N, λ, P, Q for every version, period and model); `feedback_differences.csv` (bootstrap intervals); `dilution_spread.csv`, `dilution_by_model.csv`; `drift_vs_refs.csv`, `drift_rms.csv`; `mooring_checks.csv`; `break_scan.csv`; `adjust_summary.csv`; `key_numbers.csv`.
- `files/data/`: `feedback_series.npz` (monthly T and N series of all versions); `region_series.csv.gz` (monthly region means of the main versions); `trend_maps_1982_2022.npz`; `adjust_fields_f32.npz` (HadSST4 adjustment, smoothed adjustment, uniform series, step maps); `cci_boxes_f32.npz` (CCI 5-degree monthly box means).
- `files/figures/`: Figures 1-4. `files/provenance/data_provenance.json` holds the exact inputs, URLs and SHA-256 hashes. `files/NOTICE_external_data.md` lists the external sources and licences.

**Reproduce.** Make a work folder W with the shared datasets at `W/../datasets`. Get the four prior-bundle files given in `run_all.sh` with `sci read`. Copy `files/code` to `W/code` and run `bash W/code/run_all.sh`. The CCI download (about 1 h at 8 streams) is the slow step. All other steps take minutes on 2 CPUs.

## References

- Andrews, T. et al. (2022). On the effect of historical SST patterns on radiative feedback. J. Geophys. Res. Atmos. 127, e2022JD036675. doi:10.1029/2022JD036675
- Bloch-Johnson, J. et al. (2024). The Green's Function Model Intercomparison Project (GFMIP) protocol. J. Adv. Model. Earth Syst. 16, e2023MS003700. doi:10.1029/2023MS003700
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate applications. Sci. Data 11, 326. doi:10.1038/s41597-024-03147-w
- Kennedy, J. J. et al. (2019). An ensemble data set of sea surface temperature change from 1850: HadSST.4.0.0.0. J. Geophys. Res. Atmos. 124, 7719-7763. doi:10.1029/2018JD029867
- Lewis, N. and Mauritsen, T. (2021). Negligible unforced historical pattern effect on climate feedback strength found in HadISST-based AMIP simulations. J. Climate 34, 39-55. doi:10.1175/JCLI-D-19-0941.1
- Modak, A. and Mauritsen, T. (2023). Better-constrained climate sensitivity when accounting for dataset dependency on pattern effect estimates. Atmos. Chem. Phys. 23, 7535-7549. doi:10.5194/acp-23-7535-2023
- Rayner, N. A. et al. (2003). Global analyses of sea surface temperature, sea ice, and night marine air temperature since the late nineteenth century. J. Geophys. Res. 108, 4407. doi:10.1029/2002JD002670
- Reynolds, R. W. et al. (2002). An improved in situ and satellite SST analysis for climate. J. Climate 15, 1609-1625.
- Met Office Hadley Centre, HadISST service notes: https://www.metoffice.gov.uk/hadobs/hadisst/servicenotes.html
- Campaign bundles: sci:sha256:78d7f2e0 (Green's functions, DOISST/OI v2 feedback), sci:sha256:9e1a3e72 (trend patterns, OI v2 2018 step), sci:sha256:87b87a67 (mooring data), sci:sha256:e2e438dd, sci:sha256:b93b5f64, sci:sha256:9fca62cd, sci:sha256:e75ccf52 (DOISST mean steps and anchoring).
