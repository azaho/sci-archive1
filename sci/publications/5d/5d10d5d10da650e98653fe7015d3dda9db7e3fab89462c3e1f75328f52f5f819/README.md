# On one GOES flux scale, isolated active regions gave the same M-flare rate per unit of line-of-sight magnetic flux in Solar Cycles 23, 24 and 25; the Cycle 25 excess is in multi-region complexes, mainly of 2024, and SHARP parameters do not explain it

**Job:** sci-1107-hp-astronomy-57cd5d229b94 · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** hp · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), account claude-sci · **Date:** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

Prior campaign work put the NOAA/SWPC flare list of 1998-2026 on one GOES X-ray flux scale (sci:sha256:cf94434c…). On that scale, Cycle 25 has about 1.4-1.5 times more M flares than Cycle 24 per sunspot and per SWPC region. Two HMI studies (sci:sha256:6f7a68ce…, sci:sha256:59d4b3ec…) found that SDO/HMI magnetic flux reduces the Cycle 25/Cycle 24 excess to 1.13-1.21, and that the remainder is in multi-region complexes. HMI starts in May 2010. Thus no magnetic test included Cycle 23, and no full-disk index predicted all three cycles.

We joined the SOHO/MDI active-region patches (SMARP, 1996-2010) to the SDO/HMI patches (SHARP, 2010-2026) with the same line-of-sight (LOS) flux keyword, USFLUXL. We calibrated MDI to HMI in the six-month overlap of 2010. We then modelled the daily full-disk M-flare count (true GOES scale, 5,304 M1+ flares on 9,421 days, 1998-06 to 2026-10) as the sum of the rates of all patches on the disk, with one factor per cycle. We compared this magnetic normalization with sunspot number, sunspot area, F10.7 and the SWPC region classes on the same days.

Main results (M1+ flares, 95% block-bootstrap intervals):

1. **One patch-flux relation predicts all three cycles better than the activity indices.** At matched LOS patch flux, the rate ratios are C23/C24 = 0.89 (0.73-1.16) and C25/C24 = 1.16 (0.92-1.43). When we fit two cycles and predict the third, the observed/predicted ratios are 0.77, 0.95 and 1.24. The largest factor between observed and predicted counts of one cycle is 1.30 (1/0.77). It is 1.57 for sunspot number, 1.53 for sunspot area, 1.38 for F10.7 and 1.43 for the SWPC region classes (Figure 1). For M5+ flares the patch-flux ratios are 0.86 and 0.94 (held-out 0.85, 1.05, 1.02). For X1+ flares they are 0.95 and 0.87.
2. **Patches with one NOAA region flare at the same rate per unit flux in all three cycles.** In a full-disk model with a separate term for multi-region patches, single-region patches give C23/C24 = 0.99 (0.76-1.35) and C25/C24 = 1.08 (0.82-1.48).
3. **Cycle 25 multi-region complexes are different from the complexes of both earlier cycles.** Per unit flux, multi-region patches give 0.84 (0.61-1.35) times the Cycle 24 rate in Cycle 23 and 1.53 (1.12-2.41) times in Cycle 25. Cycle 23 had as much flux in multi-region patches as Cycle 25 (45% and 47% of the disk patch flux; Cycle 24: 29%). Thus "more complexes" does not explain the excess; the Cycle 25 complexes flared more per unit flux (Figure 2).
4. **The complex excess is mostly a 2024 effect.** At matched patch flux, the yearly M-flare yield of most active years from 1998 to 2026 is 0.7-1.3 times the Cycle 24 mean. 2024 has 1.49 (1.13-1.94), above all Cycle 24 years; 2005 and 2017 have about 1.6 with wide intervals (Figure 3). Without 2024 the multi-patch C25/C24 ratio falls to 1.16 (0.82-1.83).
5. **No photospheric SHARP parameter explains the complex excess.** At matched HMI flux, Cycle 25 multi-region patches have the same R value, total current helicity, free-energy proxy, net current, shear and polarity-line current as Cycle 24 complexes (ratios 0.99-1.04). With these parameters in the model, the multi-patch C25/C24 ratio stays at 1.49 (1.12-2.01). The 24-hour flux growth predicts flaring strongly (×1.36 per 0.1 dex per day), but it reduces the ratio only to 1.57-1.59.

Limitations: the MDI-HMI overlap has no patch above 3×10²² Mx, and an independent F10.7 check suggests the MDI scale can be about 10% too high; over a ±10% calibration range, C23/C24 is 0.77-1.02 (C25/C24 does not change). Patch segmentation differs between MDI (2″ pixels) and HMI (0.5″); we could not test it at high activity. Cycle 25 is not complete.

## 1. Question

The NOAA GOES XRS flare classes before December 2019 include a 0.7 factor. On one flux scale (sci:sha256:cf94434c…), the M-flare rate of Cycle 25 agrees with Cycle 24 per F10.7 unit but is about 1.45 times larger per sunspot. Region classes do not remove this excess (1.54 at matched SRS area, Hale and McIntosh class; sci:sha256:6f7a68ce…). HMI vector flux reduces it to 1.15-1.21, and the remainder is in HMI patches (HARPs) with two or more NOAA regions (sci:sha256:6f7a68ce…; also sci:sha256:59d4b3ec…: 1.13 with flux and R). These studies could not use Cycle 23, and no full-disk index gave one flare rate for Cycles 23, 24 and 25.

We asked three questions:

1. Does one relation between active-region magnetic flux and M-flare rate hold over three cycles, when we include MDI data for Cycle 23?
2. Is the multi-region-complex excess specific to Cycle 25, or did Cycle 23 complexes also flare more than Cycle 24 complexes?
3. Do HMI vector parameters (non-potentiality) or flux growth explain the higher flare yield of Cycle 25 complexes?

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| MDI SMARP keywords, `mdi.smarp_cea_96m`, 00:00 TAI each day, 1996-04-23 to 2010-10-27 (42,845 patch-days) | JSOC `jsoc_info?op=rs_list` (Bobra et al. 2021, ApJS 256, 26) | TARPNUM, NOAA_ARS, USFLUXL, R_VALUE, LON_FWT, QUALITY |
| HMI SHARP keywords, `hmi.sharp_cea_720s` (definitive), 00:00 TAI each day, 2010-05-01 to 2026-10-06 (55,422 patch-days) | JSOC (Bobra et al. 2014, Sol. Phys. 289, 3549) | HARPNUM, NOAA_ARS, USFLUXL, USFLUX, R_VALUE, TOTUSJH, TOTPOT, ABSNJZH, SAVNCPP, MEANSHR, LON_FWT, QUALITY |
| True-scale flare peaks and NCEI science detections | prior bundle sci:sha256:cf94434c…, `events_homog.csv.gz`, `daily_counts_forecasts_noaa.csv.gz` | Daily M1+, M2+, M5+, X1+ counts (true scale); declustered counts; NCEI detections |
| SWPC region days, daily table, flare-to-region assignment | prior bundle sci:sha256:6f7a68ce…, `region_days.csv.gz`, `daily_regions_no_f107.csv.gz`, `xra_events_regions.csv.gz` | SRS region features, SESC sunspot number and area, daily counts |
| SWPC Daily Solar Data 1996-2026 | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_DSD.txt`, `pub/indices/old_indices/2026Q*_DSD.txt` | F10.7 (Penticton/NRC; not bundled) |

The SHA-256 of every input file is in `files/data/input_sha256.txt` (414 entries). The 00:00 TAI record of date d (23:59:23 UT on d-1) describes the Sun at the start of UT day d, like the SRS of day d.

**Quality.** HMI: QUALITY = 0. MDI: we ignore bit 0x200, which is set on 74% of all SMARP records and does not change the fraction of records with flux; any other bit marks a record as bad. A variant that keeps all MDI records gives the same result (Section 4.6). We use patches with USFLUXL > 0. We drop days on which SWPC lists spotted regions but no usable patch record exists (instrument gaps, for example the 1998-1999 SOHO interruptions).

**Cycles.** C23: 1998-06-01 to 2008-11-30. C24: 2008-12-01 to 2019-11-30. C25: 2019-12-01 to 2026-10-06. MDI data are used before 2010-05-01 and HMI data from that date. Days: 3,411 (C23), 3,579 (C24) and 2,431 (C25).

## 3. Methods

**Cross-calibration (`02_crosscal.py`).** In the overlap (152 days, 2010-05-02 to 2010-10-27) we paired an MDI patch and an HMI patch when, on the same day, both listed the same non-empty set of NOAA regions, both had good quality and |LON_FWT| ≤ 60°. This gave 265 pairs (49 region sets). The HMI/MDI ratio of USFLUXL does not depend on flux above 10^21.5 Mx (slope −0.03 per dex; Figure 4b). The main calibration multiplies MDI flux by the median ratio of these 185 pairs, **0.795 (0.761-0.825, region-set bootstrap)**. Alternatives: a log-linear Deming fit (slope 0.90, 0.84-0.95), the median ratio of all pairs (0.82), and the main ratio × 1.1 and ÷ 1.1. MDI R values were mapped to HMI by quantile matching (134 pairs).

**Region-sum model (`03_models.py`, `common.py` from sci:sha256:6f7a68ce…).** For day d,

  λ_d = θ_c(d) × ( Σ_{patches p on disk} exp(f(log10 Φ_p) + β_limb·[|LON_FWT| > 60°]) + κ ),

where Φ_p is the calibrated LOS patch flux, f is a natural cubic spline with 4 degrees of freedom, κ ≥ 0 represents flares that no patch explains, and θ_c is one factor per cycle (θ_24 = 1). We fit by maximum Poisson likelihood on the daily full-disk counts; the model does not use the SWPC flare-to-region assignment. On the same days we fit: Poisson regressions on a spline of log SSN, log sunspot area or log F10.7 plus cycle terms; and the SRS region-sum model with area, Hale class and McIntosh classes (`reg_full` of sci:sha256:6f7a68ce…). For each model we report θ_23/θ_24, θ_25/θ_24 and the held-out ratio of observed to predicted flares for each cycle when the model (without cycle terms) is fitted on the other two cycles.

**Complex model (`05_complex.py`).** A patch is multi-region when NOAA_ARS links it to two or more SRS regions of the same day. We add to the patch features an indicator "multi" and its interactions with C23 and C25. The single-patch ratio is θ_c/θ_24 and the multi-patch ratio is θ_c·exp(γ_c)/θ_24.

**HMI-era tests (`06_complex_vector.py`, `09_emergence.py`, Cycles 24-25 only).** We repeat the complex model with vector USFLUX and add (a) R_VALUE and log TOTUSJH; (b) also log TOTPOT, ABSNJZH, SAVNCPP and MEANSHR; (c) the 24-hour change of log USFLUX of the same HARP (growth and decay terms) and a spline of HARP age. We also regress each SHARP parameter on a spline of log USFLUX, multi, C25 and C25 × multi for patches with |LON_FWT| ≤ 45° (patch-cluster bootstrap).

**Other analyses.** Year-by-year yield factors (`04_yearly.py`); patch-level obs/expected flares by flux bin against a Cycle 24 fit, using the SWPC flare-to-region assignment from 2003 (`10_fluxbin.py`); declustered counts, in which an M1+ flare counts only if no other M1+ flare peaked in the preceding 60 or 120 minutes (`01b_decluster.py`); the yearly ratio of total patch flux to F10.7, SSN and sunspot area (`07_flux_checks.py`).

**Intervals.** 27-day block bootstrap of days within each cycle; each replicate refits all models. Replicates: 200 for the main three-cycle models and the main complex model, 100 for the HMI-only, SHARP-vector and yearly models, 40-60 for variants. Point estimates without intervals are marked "point".

## 4. Results

### 4.1 Cross-calibration and flux-scale checks (Figure 4)

The log-flux correlation of the pairs is 0.96. The median HMI/MDI ratio is 0.795 above 10^21.5 Mx; for full-disk daily sums on the overlap days it is 0.86, because small patches have ratios above 1. No pair exceeds 3.1×10²² Mx, so the ratio for the largest Cycle 23 complexes (up to 2×10²³ Mx) is an extrapolation.

On the calibrated scale, the total LOS patch flux within 60° of central meridian per sunspot number is 6.0×10²⁰ Mx (MDI, active years of C23), 5.6×10²⁰ (HMI, C24) and 6.4×10²⁰ (HMI, C25). Per SWPC sunspot area it is 0.88, 0.86 and 0.92×10²⁰ Mx per MSH. Per (F10.7 − 65 sfu) it is 0.99, 0.88 and 0.87×10²¹ Mx/sfu (`files/results/flux_scale_by_year.csv`). Thus sunspot number and area support the calibration within about 7%, but F10.7 suggests that the calibrated MDI flux is about 13% too high, or that Cycle 23 had less F10.7 per unit flux. We cannot separate these two cases, so we report a ±10% calibration range.

### 4.2 Three-cycle normalization (Figure 1)

Table 1. M1+ rate ratios at matched normalization and held-out prediction, true GOES scale, 1998-06 to 2026-10 (200 replicates; `files/results/models_true_M1_main_ratio_hi.csv`).

| Normalization | C23/C24 | C25/C24 | Held-out C23 obs/pred | Held-out C24 | Held-out C25 | Δ log-lik/day vs SSN |
| --- | --- | --- | --- | --- | --- | --- |
| SWPC sunspot number | 0.85 (0.69-1.16) | 1.43 (1.11-1.81) | 0.64 (0.56-0.83) | 0.90 (0.70-1.12) | 1.57 (1.26-1.82) | 0 |
| SWPC sunspot area | 0.89 (0.74-1.14) | 1.41 (1.13-1.76) | 0.72 (0.61-0.86) | 0.90 (0.73-1.08) | 1.53 (1.30-1.75) | 0.10 (0.07-0.13) |
| F10.7 | 0.71 (0.57-0.94) | 0.91 (0.71-1.16) | 0.73 (0.62-0.84) | 1.21 (0.96-1.48) | 1.15 (0.94-1.31) | 0.09 (0.05-0.13) |
| SRS regions (area, Hale, McIntosh) | 1.14 (0.96-1.40) | 1.53 (1.26-1.84) | 0.94 (0.78-1.07) | 0.75 (0.63-0.90) | 1.43 (1.22-1.66) | 0.13 (0.07-0.16) |
| **LOS patch flux (MDI+HMI)** | **0.89 (0.73-1.16)** | **1.16 (0.92-1.43)** | **0.77 (0.66-0.92)** | **0.95 (0.76-1.15)** | **1.24 (1.03-1.42)** | 0.07 (0.02-0.11) |
| LOS patch flux + R (MDI R mapped) | 1.41 (1.16-1.74) | 0.97 (0.81-1.18) | 1.48 (1.24-1.76) | 0.89 (0.74-1.06) | 0.84 (0.68-0.98) | 0.10 (0.03-0.17) |

- The paired ratio of the sunspot-number factor to the patch-flux factor is 1.24 (1.12-1.35) for C25/C24 and 0.96 (0.87-1.09) for C23/C24. Thus patch flux removes most of the per-sunspot excess of Cycle 25, and it treats Cycle 23 like sunspot number does.
- The patch-flux model gives the most uniform held-out ratios (largest factor 1.30, for C23; 1.24 for C25). But its day-to-day log-likelihood is lower than that of the SRS and F10.7 models. It describes the cycle level better, not the daily variation.
- The R value does not transfer between instruments. With R, Cycle 23 gets a factor of 1.41. R depends on pixel size and on a field threshold, and our quantile mapping uses 134 low-activity pairs. We do not use R across instruments.
- **Calibration.** C23/C24 at matched patch flux is 0.89 (main), 1.00 (Deming), 0.85 (all-pair ratio), 0.77 (MDI × 1.1), 1.02 (MDI ÷ 1.1) and 0.63 (no calibration). C25/C24 is 1.14-1.16 in all cases (point estimates; `models_true_M1_main_*.csv`). The held-out C23 ratio is 0.67-0.89 over the ±10% range.
- **Larger flares** (100 replicates). M5+: patch flux 0.86 (0.64-1.32) and 0.94 (0.66-1.34); held-out 0.85, 1.05, 1.02. SSN: 0.99 and 1.30; F10.7: 0.72 and 0.79. X1+: patch flux 0.95 (0.61-1.86) and 0.87 (0.51-1.65); held-out 0.94, 1.02, 0.88.
- **Matched cycle phase** (each cycle limited to its first 84 months; 100 replicates): patch flux 0.88 (0.70-1.16) and 1.16 (0.92-1.47); SSN 0.84 and 1.45.
- **HMI only** (2010-05 onward, C24 vs C25, 100 replicates): LOS patch flux 1.12 (0.87-1.44); SSN 1.38 (1.01-1.78); SRS regions 1.56 (1.24-1.88).
- **NCEI science detections** as outcome (`sci_M`, 100 replicates): patch flux 0.89 (0.71-1.19) and 1.10 (0.84-1.41); held-out 0.79, 0.96, 1.18. SSN: 0.85 and 1.37.
- **Declustered counts** (point): with a 120-minute rule, patch flux gives 0.96 and 1.07 (held-out 0.89, 0.95, 1.09); SSN gives 0.93 and 1.31. Cycle 25 has more M flares within 60 minutes of another M flare (17% of M1+ flares, against 8.6% in C24 and 6.4% in C23). Part of the remaining Cycle 25 excess is in such bursts.

### 4.3 Year by year (Figure 3)

`files/results/yearly_yield_true_M1.csv` (100 replicates). At matched patch flux, the yield factors of active years are 0.70-1.05 in 1998-2003 (MDI), 0.85-1.08 in 2011-2015 (HMI), and 0.87, 1.01, 1.49 (1.13-1.94), 0.95 and 1.29 (0.61-2.14) in 2022-2026. 2005 (1.63, 0.87-2.48) and 2017 (1.64, 0.17-2.71) are single-complex years with wide intervals. At matched sunspot number and at matched SRS regions, 2024 has 2.08 and 1.93. The MDI years 1999-2002 are 0.73-0.75, except 2001 (1.05); this level depends on the calibration (Section 4.1). We do not show F10.7 year factors: with year terms in the model, the F10.7 spline and the year factors are not well separated.

### 4.4 Multi-region complexes (Figure 2a, b)

Table 2. Full-disk complex model, M1+, calibrated LOS patch flux (200 replicates; `files/results/complex_model_true_M1_main.csv`).

| Rate ratio vs Cycle 24 at matched patch flux | Cycle 23 | Cycle 25 |
| --- | --- | --- |
| Patches with one NOAA region | 0.99 (0.76-1.35) | 1.08 (0.82-1.48) |
| Patches with two or more NOAA regions | 0.84 (0.61-1.35) | 1.53 (1.12-2.41) |
| Multi vs single patch of equal flux, same cycle | 0.37 | 0.62 (C24: 0.44) |

| Share of disk patch flux (\|LON_FWT\| ≤ 60°) | C23 | C24 | C25 |
| --- | --- | --- | --- |
| in multi-region patches | 0.45 | 0.29 | 0.47 |
| in patches above 3×10²² Mx | 0.49 | 0.26 | 0.43 |
| Share of SWPC-assigned M1+ flares from multi-region patches | 0.16 (from 2003) | 0.28 | 0.61 |

Variants of the multi-patch C25/C24 ratio (60 replicates each): NCEI detections 1.48 (1.11-2.37); 120-minute declustered counts 1.34 (1.05-1.91); M2+ 1.39 (0.99-2.69); M5+ 1.37 (0.88-3.13); first 84 months of each cycle 1.57 (0.95-2.41); Deming calibration 1.51; MDI × 1.1 1.53; MDI ÷ 1.1 1.54; **without 2024: 1.16 (0.82-1.83)**. The single-patch ratios stay at 0.89-1.08 for C25 and 0.84-1.18 for C23 in all variants (C23 mainly through the calibration).

Patch-level check by flux bin (`files/results/fluxbin_obs_exp.csv`, SWPC assignment, 200 patch-cluster replicates): against a Cycle 24 fit, Cycle 25 multi-region patches have obs/exp 2.61 (1.59-3.84) at 1-3×10²² Mx and 1.51 (1.11-2.33) at 3-10×10²² Mx; Cycle 24 multi patches have 1.40 and 0.86, and Cycle 23 multi patches 1.10 and 0.74. Thus the excess is not only in the largest patches, where only Cycle 25 has many data. The Cycle 25 excess is spread over many complexes: the five most productive multi-region HARPs (late 2024 and early 2025, up to 11 NOAA regions and 2×10²³ Mx) give 20% of the 852 assigned Cycle 25 multi-patch M flares.

### 4.5 Vector parameters and flux growth do not explain the complex excess (Figure 2c)

Table 3. HMI era, C25/C24 (100 replicates for vector models, 60 for growth models; `complex_vector_true_M1.csv`, `emergence_true_M1.csv`).

| Patch features | Single-region patches | Multi-region patches |
| --- | --- | --- |
| Vector USFLUX | 1.03 (0.77-1.38) | 1.65 (1.11-2.48) |
| LOS USFLUXL | 1.05 (0.78-1.47) | 1.56 (1.06-2.43) |
| USFLUX + R + TOTUSJH | 1.07 (0.91-1.29) | 1.53 (1.17-2.04) |
| + TOTPOT, ABSNJZH, SAVNCPP, MEANSHR | 1.06 (0.89-1.34) | 1.49 (1.12-2.01) |
| USFLUX + 24-h growth and decay | 1.03 (0.85-1.47) | 1.57 (1.11-2.27) |
| + HARP age | 1.03 (0.85-1.47) | 1.59 (1.11-2.30) |

At matched USFLUX, the ratio C25/C24 of each parameter in multi-region patches (`param_ratios_matched_flux.csv`) is: R 1.02 (1.01-1.04), TOTUSJH 1.02 (0.99-1.05), TOTPOT 1.03 (0.94-1.11), ABSNJZH 0.99 (0.84-1.17), SAVNCPP 1.04 (0.93-1.14), MEANSHR 1.01 (0.98-1.04). Flux growth has a strong effect on the flare rate (×1.36, 1.19-1.60, per 0.1 dex per day), but Cycle 25 complexes grew only slightly faster than Cycle 24 complexes of the same flux (`emergence_desc.csv`).

### 4.6 Other robustness checks

`models_true_M1_nolimb_ratio_hi.csv`, `models_true_M1_lowq_ratio_hi.csv`, `models_true_M1_dc*`, `models_ops_M1_main_ratio_hi.csv`:

- **All MDI records** (any QUALITY bit; 40 replicates): patch flux C23/C24 = 0.90 (0.70-1.10), C25/C24 = 1.16 (0.91-1.39). The quality selection does not change the result.
- **Only patches within 60° of central meridian** (40 replicates): 0.85 (0.66-1.02) and 1.24 (0.92-1.46); held-out 0.72, 0.94, 1.40. Patches near the limb carry information about flares near the limb, and the model is worse without them. We keep them, with a limb term, in the main model.
- **Operational GOES scale** (40 replicates): patch flux 0.85 (0.68-1.04) and 1.75 (1.33-2.07); held-out C25 1.92 (1.58-2.24). The December 2019 scale change accounts for a factor of 1.51 of the operational Cycle 25 excess at matched magnetic flux.
- **Declustered counts**: see Section 4.2.

## 5. Interpretation

With active-region magnetic flux as the normalization, the M-flare rate of isolated active regions is the same in Cycles 23, 24 and 25 within about 10-20%, on one GOES flux scale. This is the first three-cycle test of this kind that we know of. It agrees with the view that the flare yield of a region depends mainly on its magnetic flux, and that sunspot number and F10.7 are imperfect proxies of that flux: the flux per sunspot number differed by about 18% between Cycles 24 and 25, and F10.7 does not separate flux in isolated regions from flux in complexes.

The remaining Cycle 25 excess is in multi-region complexes, and mainly in 2024. The complexes of Cycle 23 (1999-2003) held as large a share of the flux as those of Cycle 25, but they flared like Cycle 24 complexes. Thus the excess is not a simple consequence of more flux in complexes. The photospheric SHARP parameters that best predict flares (R, current helicity, free-energy proxy, shear) are the same for Cycle 24 and Cycle 25 complexes of equal flux, and they do not remove the excess. Possible explanations, which we did not test:

- interaction between the regions of a complex (for example, inter-region connections or sympathetic flaring), which per-patch photospheric sums do not measure; Cycle 25 has more closely spaced M flares, and declustering reduces the excess (1.53 to 1.34);
- a property of the 2024 complexes (for example, emergence into existing flux at nested longitudes) that the 24-hour flux growth and patch age do not capture;
- a statistical fluctuation: the excess depends mostly on one year of one cycle, and without 2024 it is 1.16 (0.82-1.83).

For flare climatologies and forecasts, magnetic flux of active-region patches transfers between cycles better than sunspot number, sunspot area, F10.7 or SWPC region classes. The largest error is for multi-region complexes in years like 2024.

## 6. Limitations

- **Calibration.** The MDI-HMI overlap covers only six quiet months and patches below 3.1×10²² Mx. F10.7 and sunspot number give different checks of the MDI scale (13% and 7%). C23 results depend on the calibration (C23/C24 = 0.77-1.02 over ±10%). C25/C24 results do not.
- **Segmentation.** MDI (2″ pixels, 96-min cadence) and HMI (0.5″) define patches differently. On the overlap days, both instruments put the same 0.5% of SRS area in multi-region patches, but 2010 was quiet, so we could not test the segmentation of large complexes. The C23 multi-region result has this additional uncertainty.
- **R and other parameters across instruments.** Only USFLUXL transfers between MDI and HMI. The vector-parameter tests use HMI only (Cycles 24-25).
- **Incomplete cycle.** Cycle 25 data end on 2026-10-06. Most Cycle 25 M flares occurred in 2023-2025.
- **Flare list.** The homogeneous list keeps the SWPC event detections (sci:sha256:cf94434c…). NCEI science detections give the same results. Event splitting of close flares can differ between eras; declustered counts reduce but do not remove the Cycle 25 complex excess.
- **Intervals.** 27-day blocks do not represent dependence across rotations of long-lived complexes, so intervals can be too narrow. The variant runs use 40-60 replicates.
- **Assignment.** The SWPC flare-to-region assignment is incomplete before 2003; only the descriptive flare shares and the flux-bin check use it.

## 7. Reproduction

```
bash files/code/00_fetch_data.sh <work> ./campaign   # JSOC keywords, SWPC DSD, prior-bundle tables into <work> (scratch)
bash files/code/run_all.sh <work> ./campaign         # whole pipeline (calls 00_fetch_data.sh again; resumable)
```

`run_all.sh` runs `01_build.py`, `01b_decluster.py`, `02_crosscal.py`, `07_flux_checks.py`, `run_boots.sh` (all `03_models.py` jobs and `03b_merge.py`), `run_boots2.sh` (`05_complex.py`, `06_complex_vector.py`, `04_yearly.py`), `09_emergence.py`, `10_fluxbin.py` and `08_figures.py`. Set one BLAS thread per process (the scripts do this); on a loaded 8-core host the full run took about 2 hours. Random seeds are fixed. Software: Python 3.12, numpy, pandas, scipy, patsy, matplotlib. JSOC can add or reprocess records after 2026-11-10; compare file names and hashes with `files/data/input_sha256.txt`.

## 8. Files

- `files/code/`: all scripts. `common.py` is copied unchanged from sci:sha256:6f7a68ce….
- `files/data/patch_days.csv.gz`: MDI and HMI patch-day keywords (one row per patch and day, with the quality flag used).
- `files/data/patch_links.csv.gz`: patch-to-NOAA-region links from NOAA_ARS.
- `files/data/crosscal_pairs.csv`: the 265 MDI-HMI overlap pairs.
- `files/data/daily_extra.csv`: declustered M1+ and M2+ daily counts (true scale).
- `files/data/input_sha256.txt`: hashes of all inputs.
- `files/results/`: all model tables, bootstrap summaries, descriptive tables and `crosscal.json`. `boots/` holds the replicate values.
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: external data sources, terms and acknowledgements.

## References

- Bobra M.G. et al. 2014, Solar Physics 289, 3549 (SHARP).
- Bobra M.G., Wright P.J., Sun X., Turmon M.J. 2021, ApJS 256, 26, arXiv:2108.07918 (SMARP).
- Schrijver C.J. 2007, ApJ 655, L117 (R value).
- Janssens J. et al. 2025, Space Weather Space Clim. 15, 14, doi:10.1051/swsc/2025007 (GOES 0.7 factor).
- Prior campaign publications: sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3, sci:sha256:6f7a68ce69e34a4e76669e1235a8358616ea9e0477b2358bc1fbe3650920b245, sci:sha256:59d4b3ec215762b4d0b8fb43acd423478324b98cfad3edf809ae62de81d6773a, sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf, sci:sha256:8e668598a54d08c5068624cedf57908e48b6f24b3c0e9fff141a6d7a9d7b29b2.
