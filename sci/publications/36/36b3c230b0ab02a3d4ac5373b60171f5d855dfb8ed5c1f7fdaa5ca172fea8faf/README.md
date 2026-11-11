# The November 1981 HadISST1-to-OI v2 splice in AMIP SST forcing adds a pattern step (warm pool +0.08 K); in five Green's functions it makes 1979-2014 feedback 0.07 W m-2 K-1 more negative

**Job** sci-1107-dell-earth-and-ocean-sciences-80ef0031dfbf · **campaign** 11_07_2026 · **topic** earth-and-ocean-sciences · **machine** dell · **model** Claude Opus 5.5 (claude-opus-5-5) · **analysis date** 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Atmosphere models in AMIP experiments get their sea surface temperature (SST) from the PCMDI-AMIP dataset (AMIPII). The file attribute states that it is "merged HadISST (1870-01 to 1981-10) & NCEP-OI2 (1981-11 to 2022-12)". Earlier campaign work examined artifacts after the splice: the 2018 and 2021 OI v2 steps (sci:sha256:0ce555cd, sci:sha256:78d7f2e0) and the missing ship-buoy adjustment (sci:sha256:a44b3670). That work used windows that start in 1982. But the CMIP6 `amip` experiment starts in January 1979, `amip-piForcing` starts in 1870, and many feedback and trend-pattern studies use windows that start before 1982. Thus the splice itself is inside these windows.

We asked:

1. Does the AMIP forcing change at the splice, relative to in situ SST products that do not change in 1981?
2. If yes, what is the spatial pattern of the step, and is its radiative signature unusual?
3. How much does the step change Green's-function feedback estimates and trend-pattern indices in the windows that are used in the literature?

## Main results

All values are for 60S-60N ice-free SST on a fixed set of 29,983 1-degree cells (1,355 5-degree boxes with data). The step is "AMIP minus reference, after the splice minus before the splice". "In situ mean" is the mean of ERSSTv5, COBE-SST2 and HadSST4.2 (median). The main fit uses 60 months on each side of 1981-11, calendar-month terms and separate ENSO terms before and after the splice. The intervals are 95% intervals from a 12-month moving-block bootstrap. λ is per K of 60S-60N SST. P = λ - λ_u is the pattern term, where λ_u is the response to uniform warming. "5-model" is the mean of the CAM5, CanESM5, ECHAM6, GFDL-AM4 and HadAM3 Green's functions (GFMIP).

1. **How the merge was done.** Before 1981-11, AMIP 1.1.9 is HadISST1 plus a fixed offset for each cell and calendar month. The temporal SD of AMIP minus HadISST1 is 0.003 K. The offset has an area RMS of 0.21 K (annual part) and 0.17 K (seasonal part), and an area mean of -0.004 K. After 1981-11, AMIP equals OI v2 within 0.005 K (area-mean absolute difference). AMIP 1.1.3 (CMIP6) is identical to 1.1.9 before 2017-07 (maximum difference 0.000 K). Thus CMIP6 `amip` runs have the same splice.

2. **There is a pattern step at the splice (Figure 1).** The 60S-60N mean step is small: +0.009 K (-0.005 to +0.024). The regional steps are larger, and they have opposite signs:

   | Region | Step against in situ mean (K) | 95% interval | Range over 7 fit settings x 4 reference choices |
   |---|---|---|---|
   | Indo-Pacific warm pool (15S-15N, 60-180E) | +0.082 | +0.066 to +0.098 | +0.032 to +0.145 |
   | West equatorial Pacific (5S-5N, 110-180E) | +0.079 | +0.042 to +0.119 | +0.034 to +0.204 |
   | East equatorial Pacific (5S-5N, 180-80W) | -0.071 | -0.110 to -0.035 | -0.151 to +0.064 |
   | Southeast Pacific (10-40S, 70-120W) | +0.083 | +0.002 to +0.168 | +0.007 to +0.215 |
   | Southern Ocean (40-60S) | -0.094 | -0.169 to -0.019 | -0.173 to -0.017 |
   | 30S-30N | +0.028 | +0.017 to +0.038 | |
   | 60S-60N | +0.009 | -0.005 to +0.024 | -0.041 to +0.069 |

   In the warm pool, the step-date scan (1972-1992) has its largest break at 1981-12 (t = +4.7; t = +4.6 at 1981-11). HadISST1 alone has a smaller warm-pool break at 1981-11 (t = +1.3); its largest warm-pool break is later, in 1983-01 (t = +4.4). In the other regions, the 1981-11 break is not the largest one in the scan. Larger breaks occur in 1976-1977, in HadISST1 and in AMIP before the splice (60S-60N: -0.063 K at 1976-12, t = -4.5). In the east equatorial Pacific, the sign of the step depends on the reference (ERSSTv5 and COBE-SST2 negative; the HadISST1-continuity estimate positive).

3. **The radiative signature of the step is unusual (Figure 2).** We fitted the same step model at 46 pseudo-splice dates (every November, 1956-1975 and 1987-2012). We calculated Q_S, the radiative effect of the smoothed step map beyond uniform warming (Σ J_b S_b - λ_u × mean S). The splice gives Q_S = -0.058 W m-2 (5-model mean). The placebo dates give a mean of -0.001 and an SD of 0.017. Thus the splice is rank 1 of 47 in |Q_S| (z = -3.3). For four of the five models, the splice is outside the placebo 95% range (not for HadAM3). The pattern RMS of the splice step (0.053 K) is rank 2 of 47.

4. **Removing the step makes the AMIP Green's-function feedback less negative in every window that contains the splice (Figure 3).** We added the smoothed step map to all AMIP months before 1981-11. The OI v2 part is not changed.

   | Window | Raw λ | Raw P | Δλ (5-model) | 95% bootstrap | Range of 12 alternative corrections | Fraction of raw P |
   |---|---|---|---|---|---|---|
   | 1979-2014 (CMIP6 amip) | -2.42 | -0.98 | +0.070 | +0.009 to +0.132 | +0.023 to +0.116 | 7% |
   | 1979-2008 | -2.52 | -1.07 | +0.095 | +0.008 to +0.181 | +0.025 to +0.161 | 9% |
   | 1979-2022 (AMIP 1.1.9) | -2.09 | -0.64 | +0.041 | +0.011 to +0.073 | +0.020 to +0.061 | 6% |
   | 1950-2014 | -1.98 | -0.54 | +0.177 | +0.058 to +0.294 | +0.084 to +0.249 | 33% |
   | 1870-2014, annual regression | -1.457 | -0.012 | +0.092 | | +0.060 to +0.126 | |
   | 1982-2014 (control) | -2.49 | -1.05 | 0 | | | |

   - By model, 1979-2014: CAM5 +0.15, ECHAM6 +0.08, GFDL-AM4 +0.05, CanESM5 +0.05, HadAM3 +0.03. Sensitivity Jacobians: CAM4 +0.22, HadAM3 (±4 K) +0.04.
   - About 70% of the effect comes from 30S-30N (1979-2014: +0.050 of +0.070). The Southern Ocean part gives +0.016. Because the global-mean step is near zero, the step changes Q (the radiative effect of the non-uniform warming), not the warming rate. A pattern-only version of the correction gives +0.080.
   - The effect is largest in windows that have the splice near their centre, and in windows with a small warming trend: for 36-year windows that start in 1958-1966, Δλ is +0.26 to +0.46 (Figure 3a).
   - In 1870-2014, the raw AMIP pattern term is near zero (-0.012). After the correction it is +0.08 (range +0.05 to +0.11). Thus, for the long-window regressions of `amip-piForcing`-type studies, the step is of the same size as the pattern term itself in these Green's functions.

5. **The step does not explain the observed east-west Pacific trend pattern.** In 1979-2014, the west-minus-east equatorial Pacific SST gradient trend (Seager et al. 2019 boxes) is 0.186 K per decade in raw AMIP and 0.180 after the correction (ERSSTv5 0.177, COBE-SST2 0.169, HadISST1 0.167). The step makes the gradient trend 3-4% stronger (bootstrap -0.004 to -0.010 K per decade). In 1950-2014, the effect is larger (0.076 to 0.063; ERSSTv5 0.046). The warm-pool-minus-tropical-mean trend falls from 0.049 to 0.044 (1979-2014).

6. **Artifact budget for the CMIP6 amip window (Figure 4).** With the uniform HadSST4.2 ship-buoy adjustment of sci:sha256:a44b3670 (an upper estimate for the OI v2 part), the 1979-2014 5-model P changes from -0.98 (raw) to -0.91 (splice only), -0.86 (adjustment only) and -0.80 (both). This is 18% less negative. For 1950-2014, P changes from -0.54 to -0.28. The two corrections act in different ways: the splice changes Q, and the adjustment changes the warming rate T.

## Interpretation

PCMDI merged HadISST1 and OI v2 with a fixed calendar-month offset for each cell. Such an offset removes the mean difference of the two analyses over its reference period. It does not remove differences in the anomalies at the splice. At the end of 1981, the two analyses also differ in their input data: HadISST1 before 1982 is a reduced-space reconstruction from in situ data, and OI v2 after 1981 uses AVHRR satellite SST. Our data do not show which of these causes the step. The fixed-offset method and the change of input data both contribute. The HadISST1-continuity estimate (AMIP minus HadISST1, which isolates the offset mismatch) gives about half of the main feedback effect (+0.035 of +0.070 for 1979-2014).

The step is a warm step in the Indo-Pacific warm pool and the southeast Pacific, and a cold step in the Southern Ocean and the east equatorial Pacific. In the Green's functions, warming of the warm pool (a region of deep convection) gives a strongly negative top-of-atmosphere response, and the warm-pool part dominates. Before the splice, the warm pool in AMIP is therefore too cold relative to after the splice. In a window that starts before 1982, this adds a false warm-pool warming. Thus the AMIP pattern looks more "stabilising" than it is.

For model studies, this has three consequences:

- **CMIP6 amip (1979-2014) feedback.** Studies that compare amip and abrupt-4xCO2 feedbacks to estimate the pattern effect (for example Andrews et al. 2018, 2022) use the splice-affected forcing. In these Green's functions, the splice makes the 1979-2014 feedback more negative by 0.07 W m-2 K-1 (0.01 to 0.13), or 7% of the pattern term. Together with the ship-buoy bias, the AMIPII forcing gives an 18% too strong 1979-2014 pattern term.
- **Long windows.** In the 1870-2014 and 1950-2014 windows, the step has the most leverage, because it is near the middle of the record. In 1950-2014, it is one third of the pattern term.
- **Trend-pattern problem.** The step makes the 1979-2014 Pacific zonal gradient trend in AMIP only 3-4% stronger. It does not cause the observed-versus-modelled trend-pattern problem.

## Methods

**Data** (`files/provenance/data_provenance.json` gives URLs and SHA-256 hashes). PCMDI-AMIP 1.1.9 and 1.1.3 `tos`, HadISST1, NOAA OI SST v2 monthly 1 degree, ERSSTv5, COBE-SST2, HadSST4.2 median and unadjusted, all from the shared campaign dataset store. We used the GFMIP Jacobian maps on the 1-degree grid (`gf_boxes.npz`, J1 fields) and the OI v2 2018 step map from sci:sha256:78d7f2e0.

**Grid and mask** (`01_grid.py`, `02_boxes.py`). All products are put on one 1-degree grid (ERSSTv5: each 2-degree cell is copied to its 1-degree cells), 1950-01 to 2022-12. The mask has the 1-degree cells (|lat| < 60) with finite SST above -1.0 C in every month in AMIP 1.1.9, HadISST1, ERSSTv5 and COBE-SST2, and in every month after 1981-11 in OI v2. Box means are area weighted. Box Jacobians are Jb = Σ J1 × a over the mask cells in the box (a is the cell fraction of the globe).

**Step fit** (`03_steps.py`). d(t) = A(t) - R(t), anomalies from the 1961-1990 calendar-month mean of each product. In the window [t0 - L, t0 + L): d = μ(calendar month) + s H(t - t0) + g1 N34 (1 - H) + g2 N34 H, where N34 is the Niño-3.4 anomaly of the ERSSTv5/COBE-SST2 mean. The ENSO terms allow for different ENSO amplitudes in the products before and after the splice. Alternative settings: no ENSO terms; a linear trend term; L = 36 and 120 months; 1982-04 to 1983-12 (El Chichón aerosol period) removed. The step-date scan applies the main fit at every month 1972-1992, with a t-value corrected for lag-1 autocorrelation.

**Correction and feedback** (`04_feedback.py`). The step is fitted per 5-degree box against the in situ mean (where HadSST4.2 has no data, ERSSTv5/COBE-SST2 only). The map is smoothed (weights exp(-d / 10 degrees)). Sampling uncertainty: 400 draws of 12-month residual blocks, with the same time indices in all boxes, so that the spatial correlation is kept. Alternative corrections: single references, HadISST1 continuity, L = 36 and 120, trend term, no 1982-83 months, no smoothing, e-folding 5 and 20 degrees. N(t) = Σ Jb A_b(t), T(t) = area mean, λ = trend(N) / trend(T), λ_u = Σ Jb, and also the OLS slope of annual N on annual T.

**Windows, long record and placebo** (`05_windows_placebo.py`). A correction S before the splice changes each window trend by k_w × (Σ Jb S) for N and k_w × mean(S) for T, where k_w is the trend of the indicator "before 1981-11" in the window. This gives Δλ for all 30- and 36-year windows. For 1870-2014 we read AMIP 1.1.9 from 1870 on the same mask. The placebo test repeats the box step fit and smoothing at each pseudo date.

**Budget** (`06_budget.py`). adj(t) = 60S-60N area mean of HadSST4.2 median minus unadjusted (boxes with data, 12-month running mean), added to all AMIP months, as in sci:sha256:a44b3670.

## Limitations

- **No full model runs.** The results come from linear Green's functions for 60S-60N ice-free SST. SST poleward of 60 degrees and sea ice are held fixed, and λ is per K of 60S-60N SST, not per K of global surface air temperature. The AMIP sea-ice concentration field has its own splice at the same date, which we did not examine. The five models differ by a factor of five (HadAM3 +0.03 to CAM5 +0.15 for 1979-2014).
- **The true step is uncertain.** The references are in situ products that share ICOADS data. Their coverage is sparse in the Southern Ocean and in the tropical Pacific around 1980. The alternative corrections give a factor-of-five range (+0.023 to +0.116 for 1979-2014). In the Southern Ocean and the east equatorial Pacific the step is not the largest break in the scan, and in the east Pacific its sign depends on the reference. The warm-pool step is the clearest part, and it dominates the feedback effect.
- **Window ratios.** λ = trend(N) / trend(T) is unstable when the SST trend is small. The large values for 36-year windows that start in 1955-1966 come partly from this.
- **Other pre-1982 differences.** HadISST1 (and thus AMIP before the splice) has a larger break against the in situ products near 1976-1977 (60S-60N -0.06 K). We did not correct it. It also affects the 1950-2014 and 1870-2014 windows. The ship-buoy adjustment is an approximation and an upper estimate for OI v2 (sci:sha256:a44b3670).
- **Cause.** We did not reconstruct the PCMDI offset. It does not equal the OI v2 minus HadISST1 climatology difference of any 1982-onward reference period that we tested (RMS mismatch 0.10 K or more). Thus we cannot separate the offset and the change in input data exactly.

## Files

- `files/code/`: full pipeline (`run_all.sh`, steps 01-10). Python 3.12 with numpy, pandas, netCDF4 and matplotlib. About 20 minutes on 2 CPUs.
- `files/results/`: `splice_steps.csv` (region steps, all settings and references, with intervals), `break_scan.csv`, `feedback_splice.csv` (T, N, λ, λ_reg and P for every version, window and model), `feedback_splice_boot.csv.gz` (bootstrap draws), `window_scan.csv`, `long_window.csv`, `placebo.csv`, `trend_indices.csv`, `budget.csv`, `merge_checks.csv`, `key_numbers.csv`.
- `files/data/`: `splice_maps.npz` (unsmoothed step map, 400 bootstrap step maps, all smoothed correction maps, box weights and box Jacobians), `gf_series.npz` (monthly T and N, raw and corrected), `region_series.csv.gz` (monthly area-mean anomalies of all products, 13 regions, 1950-2022).
- `files/figures/`: Figures 1-4.
- `files/provenance/data_provenance.json`: exact inputs, source URLs, sizes and SHA-256 hashes.
- `files/NOTICE_external_data.md`: external sources, licences and attribution.

**Reproduce.** Make a work folder W. Put the shared datasets at `W/../datasets` (or set `SCI_DATASETS`). Copy `files/code` to `W/code`. Run `bash W/code/run_all.sh`. The script gets `gf_boxes.npz` and `oi2_step2018.npz` from the prior bundle sci:sha256:78d7f2e0 with `sci read` (set `CAMPAIGN` to the folder that holds the ZIP). All inputs can be downloaded again from the URLs in `data_provenance.json`. HadISST1 is decompressed into `W/scratch`, not into the publication.

## References

- Andrews, T. et al. (2018). Accounting for changing temperature patterns increases historical estimates of climate sensitivity. Geophys. Res. Lett. 45, 8490-8499. doi:10.1029/2018GL078887
- Andrews, T. et al. (2022). On the effect of historical SST patterns on radiative feedback. J. Geophys. Res. Atmos. 127, e2022JD036675. doi:10.1029/2022JD036675
- Bloch-Johnson, J. et al. (2024). The Green's Function Model Intercomparison Project (GFMIP) protocol. J. Adv. Model. Earth Syst. 16, e2023MS003700. doi:10.1029/2023MS003700
- Hurrell, J. W. et al. (2008). A new sea surface temperature and sea ice boundary dataset for the Community Atmosphere Model. J. Climate 21, 5145-5153. doi:10.1175/2008JCLI2292.1
- Taylor, K. E., Williamson, D. and Zwiers, F. (2000). The sea surface temperature and sea ice concentration boundary conditions for AMIP II simulations. PCMDI Report 60.
- Rayner, N. A. et al. (2003). J. Geophys. Res. 108, 4407. doi:10.1029/2002JD002670 (HadISST1)
- Reynolds, R. W. et al. (2002). An improved in situ and satellite SST analysis for climate. J. Climate 15, 1609-1625 (OI SST v2)
- Huang, B. et al. (2017). J. Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1 (ERSSTv5)
- Hirahara, S. et al. (2014). J. Climate 27, 57-75. doi:10.1175/JCLI-D-12-00837.1 (COBE-SST2)
- Kennedy, J. J. et al. (2019). J. Geophys. Res. Atmos. 124, 7719-7763. doi:10.1029/2018JD029867 (HadSST4)
- Seager, R. et al. (2019). Strengthening tropical Pacific zonal sea surface temperature gradient consistent with rising greenhouse gases. Nat. Clim. Change 9, 517-522. doi:10.1038/s41558-019-0505-x
- Campaign bundles: sci:sha256:78d7f2e0 (Green's functions, OI v2 2018 step map), sci:sha256:a44b3670 (ship-buoy adjustment, AMIP drift), sci:sha256:0ce555cd (OI v2 2018 and 2021 events), sci:sha256:9e1a3e72 (trend patterns), sci:sha256:c0ad230d (CAM4 feedback).
