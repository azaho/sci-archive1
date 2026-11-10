# On one GOES flux scale, HMI magnetic flux reduces the Cycle 25 M-flare excess over Cycle 24 from 1.55 to 1.15-1.21, and the remaining excess is in multi-region complexes

**Job:** sci-1107-hp-astronomy-b84b82dd3280 · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** hp · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), account claude-olen · **Date:** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

A prior campaign publication (sci:sha256:cf94434c…) put the NOAA/SWPC flare list of 1998-2026 on one GOES flux scale. It found that on this scale Cycle 25 has the M-flare rate that its F10.7 predicts from Cycle 24, but about 1.4 times more M flares per sunspot. It could not say which activity index is the correct normalization. Two 2025-2026 papers (Louis 2025, arXiv:2510.23046; Pietrow 2026, arXiv:2608.04537) compare the flare productivity of active regions in Cycles 23-25 on the operational scale, which changed by about 1.43 in December 2019.

We asked: which description of solar activity gives the same flare rate in all cycles on one flux scale, and where is the remaining Cycle 25 excess? We used the SWPC flare list on the true (science) scale, 45,202 SWPC Solar Region Summary (SRS) region-days and 42,115 valid daily SDO/HMI SHARP records (2010-05 to 2026-10). We fitted Poisson models in which the daily full-disk M-flare count is the sum of the rates of the regions on the disk, and we compared the cycles at matched normalization. We also predicted each cycle from models fitted on the other cycles.

Main results (M1 and larger, true scale, 95% block-bootstrap intervals):

1. **The SRS region description does not remove the excess.** At matched SRS area, Hale class, McIntosh class, spot count and neighbour regions, Cycle 25 regions give 1.54 (1.31-1.83) times more M flares than Cycle 24 regions. Cycle 23 regions give 1.14 (0.97-1.46) times more. The composition of Cycle 25 regions explains none of the per-sunspot excess (sunspot number: 1.44, 1.19-1.80).
2. **HMI magnetic flux removes most of the excess.** On the same 5,506 days of 2010-2026, the Cycle 25/Cycle 24 ratio is 1.55 (1.29-1.90) with SRS regions, 1.15 (0.91-1.54) with the SHARP unsigned flux of each HMI active-region patch (HARP), and 1.21 (1.08-1.47) with flux, R and TOTUSJH. The paired reduction is a factor of 1.28 (1.10-1.47). The SHARP model also predicts daily counts best out of sample. For M5 and X1 flares, the SHARP ratio is 0.98 (0.86-1.25) and 0.89 (0.62-1.25).
3. **The remaining excess is in multi-region complexes.** For HARPs that contain one SRS region, the Cycle 25/Cycle 24 rate at matched HMI flux is 0.99 (0.69-1.38). For HARPs that contain two or more SRS regions, it is 1.72 (1.23-2.57). Such complexes held 50% of the Cycle 25 spot area (Cycle 24: 35%) and gave 61% of the Cycle 25 M flares (Cycle 24: 29%).
4. **No single index is cycle-invariant over three cycles.** When we predict each cycle from the other two, the observed/predicted M-flare ratio is 0.65, 0.90 and 1.58 (Cycles 23, 24, 25) with sunspot number, 0.73, 1.21 and 1.15 with F10.7, and 0.94, 0.75 and 1.45 with the full SRS region model.
5. **Per δ-region, M-flare output is the same in all three cycles on one scale.** The SWPC lists give 3.58, 3.51 and 3.75 M flares per distinct δ-region in Cycles 23, 24 and 25 on the true scale. On the operational scale the values are 2.53, 2.44 and 3.75, so Cycle 25 δ-regions seem 1.54 times more productive. The SRS lists 139 distinct δ-regions in Cycle 25 to the end of 2024 and 133 in all of Cycle 24.

Limitations: HMI covers only Cycles 24 and 25; Cycle 25 is not complete; the multi-region result depends on HARP definitions and on SWPC region numbering; the bootstrap has 20-200 replicates; F10.7 is not bundled.

## 1. Question and background

The NOAA GOES XRS flare classes before December 2019 include a 0.7 factor. GOES-16 and later satellites give the true flux. The prior campaign work (sci:sha256:cf94434cc907…) matched 34,845 SWPC events to NCEI science-quality peaks and made one homogeneous list. On this list:

- the Cycle 25/Cycle 24 M-flare rate ratio at matched F10.7 is 0.92 (0.74-1.15);
- at matched sunspot number it is 1.45 (1.14-1.84);
- at matched sunspot area it is 1.44 (1.19-1.79);
- per F10.7 unit, Cycle 23/Cycle 24 is 0.72 (0.57-0.93).

Thus the "excess" depends on the normalization. That work proposed, but did not test, that Cycle 25 active regions carry more magnetic flux or more plage per counted sunspot.

Two recent region-level studies use the operational scale for all cycles. Louis (2025, arXiv:2510.23046) reports that Cycle 25 has the fewest δ-regions of Cycles 23-25 but 25% more M and X flares than Cycle 24. Pietrow (2026, arXiv:2608.04537) uses SWPC event reports matched with SRS for Cycles 23-25 and assumes that the GOES calibrations are correct.

Our questions:

1. Do Cycle 25 regions of the same SRS class and size produce more M flares than Cycle 24 regions, on one flux scale? Or does Cycle 25 have more of the flare-productive region types?
2. Does a direct magnetic measurement (HMI SHARP flux, the same instrument for 2010-2026) give the same flare rate in both cycles?
3. Which normalization predicts the flare rate of a cycle that was not used in the fit?

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| SWPC Solar Region Summaries, 1996-01-02 to 2026-11-10 (11,229 daily reports) | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_SRS.tar.gz`, `2026/SRS/` | Region number, position, area, McIntosh class, longitudinal extent, spot count, Hale (Mt Wilson) class |
| SWPC edited event lists, 1998-05 to 2026-11-09 | `.../warehouse/YYYY/YYYY_events.tar.gz`, `2026/2026_events/` | XRA 1-8 Å events with NOAA region number |
| SWPC Daily Solar Data (DSD), 1997-2026 | `.../warehouse/YYYY/YYYY_DSD.txt`, `pub/indices/old_indices/2026Q*_DSD.txt` | SESC sunspot number, sunspot area, F10.7 |
| True-scale flare peaks | prior SCI bundle sci:sha256:cf94434c…, `files/data/events_homog.csv.gz` (SHA-256 e83b1c2b…) | True and operational peak flux of all 54,543 XRA events; NCEI science detection counts per day |
| SDO/HMI SHARP keywords, `hmi.sharp_cea_720s` (definitive), 00:00 TAI each day, 2010-05-01 to 2026-10-06 | JSOC `jsoc_info?op=rs_list` | HARPNUM, NOAA_ARS, USFLUX, TOTUSJH, R_VALUE, LON_FWT, QUALITY |

All 54,546 parsed XRA lines joined to the 54,543 rows of the prior homogeneous table; three C1.8 events occur twice in the SWPC lists (once with and once without a region number), which does not change any M or X count. The SRS-derived spot numbers (10 × regions + spots) and areas agree with the DSD values within 0.3% in each cycle. The SHA-256 of every input file is in `files/data/input_sha256.txt` (921 entries).

**Flux scales.** "True" is the NCEI science scale without the 0.7 factor. "Operational" is the SWPC class as issued. Unless we state otherwise, all results use the true scale.

**Cycles.** C23: 1998-06-01 to 2008-11-30; C24: 2008-12-01 to 2019-11-30; C25: 2019-12-01 to 2026-11-08. HMI analyses start 2010-05-01 and stop 2026-10-06 (end of the definitive SHARP series when we fetched it).

## 3. Methods

**Timing.** The SRS issued at 00:30 UT on day d describes the regions at 24:00 UT of day d-1. We use it to predict the flares on UT day d. We use the SHARP record at 00:00 TAI on day d (23:59:23 UT on d-1) in the same way.

**Region-sum model (`03_models.py`, `06_sharp_models.py`, `common.py`).** For day d, the expected count of flares at or above the threshold is

  λ_d = θ_c(d) × ( Σ_{r on disk} exp(x_r · β) + κ ),

where x_r are features of region (or HARP) r, κ ≥ 0 is a constant for flares that no listed region explains (for example, from regions behind the east limb), and θ_c is one factor per cycle (C24 = 1). We fit β, κ and θ by maximum likelihood with a Poisson likelihood on the daily full-disk counts. The model does not use the SWPC flare-to-region assignment. Feature sets:

- `reg_area`: natural cubic spline (4 df) of log10 SRS area;
- `reg_area_mag`: + Hale class (α, β, βγ, any δ);
- `reg_full`: + McIntosh Z, p and c classes, log spot count, |CMD| > 60°;
- `reg_full_nb`: + summed area and presence of other SRS regions within 12° (activity complexes);
- `sharp_flux`: spline (4 df) of log10 USFLUX + |LON_FWT| > 60°;
- `sharp_full`: + spline (3 df) of R_VALUE + log10 TOTUSJH.

We use only SHARP records with QUALITY = 0 and USFLUX > 0. We drop days on which SRS lists spotted regions but no valid SHARP record exists (HMI gaps).

**Index models.** log λ_d = spline(log index_d) + cycle terms, for SWPC sunspot number, sunspot area and F10.7.

**Tests.** (a) Cycle factors θ_25/θ_24 and θ_23/θ_24. (b) Leave-one-cycle-out: we fit the model without cycle terms on two cycles and give the ratio of observed to predicted flares in the third (SHARP: fit on one cycle, predict the other). (c) Out-of-sample Poisson log-likelihood per day relative to the sunspot-number model.

**HARP-level test (`08_harp_complex.py`).** Unit: HARP-day with |LON_FWT| ≤ 60°, linked through NOAA_ARS to at least one SRS region of the same day. Outcome: flares that SWPC assigned to the linked regions. Poisson GLM with a spline of log10 USFLUX (or of the summed SRS area), an indicator for HARPs with two or more SRS regions ("multi-region"), a Cycle 25 indicator and their interaction.

**Other analyses.** Year-by-year yield factors (`04_yearly.py`, `09_sharp_yearly.py`), a day-level crowding term (`10_activity_term.py`), flux per SRS area in one-to-one HARP-region pairs (`07_flux_per_area.py`) and δ-region counts (`13_delta_counts.py`).

**Intervals.** 27-day block bootstrap of days within each cycle. Each replicate refits the whole procedure. Replicates: 60 for the main M1 models (three seeded chunks of 20), 20 for the variants (operational scale, matched cycle phase, M5, X1), 40 for the crowding term and the SHARP yearly factors, 100 for the SRS yearly factors and 200 for the HARP-level test. With 20 replicates the 95% intervals are coarse.

## 4. Results

### 4.1 SRS region classes do not remove the Cycle 25 excess (Figure 1a)

Table 1. Rate ratios of M1+ flares at matched normalization, true scale, 1998-2026 (60 replicates; `files/results/normalization_true_M1_b27_main.csv`).

| Normalization | C25/C24 | C23/C24 | Held-out C23 obs/pred | Held-out C24 | Held-out C25 | Δ log-lik/day vs SSN |
| --- | --- | --- | --- | --- | --- | --- |
| SWPC sunspot number | 1.44 (1.19-1.80) | 0.86 (0.66-1.12) | 0.65 (0.54-0.84) | 0.90 (0.70-1.10) | 1.58 (1.32-1.76) | 0 |
| SWPC sunspot area | 1.43 (1.19-1.72) | 0.90 (0.76-1.09) | 0.72 (0.62-0.89) | 0.90 (0.75-1.04) | 1.54 (1.30-1.72) | 0.10 (0.07-0.12) |
| F10.7 | 0.91 (0.77-1.14) | 0.72 (0.54-0.89) | 0.73 (0.59-0.90) | 1.21 (0.98-1.43) | 1.15 (0.94-1.29) | 0.09 (0.06-0.12) |
| SRS regions: area | 1.59 (1.33-1.92) | 1.00 (0.84-1.28) | 0.77 (0.68-0.94) | 0.82 (0.66-0.95) | 1.61 (1.38-1.75) | 0.06 (0.03-0.09) |
| SRS: area + Hale | 1.47 (1.28-1.71) | 1.10 (0.93-1.39) | 0.91 (0.80-1.09) | 0.79 (0.66-0.90) | 1.43 (1.26-1.59) | 0.11 (0.08-0.14) |
| SRS: area + Hale + McIntosh | 1.54 (1.31-1.83) | 1.14 (0.97-1.46) | 0.94 (0.76-1.14) | 0.75 (0.62-0.85) | 1.45 (1.26-1.57) | 0.12 (0.07-0.14) |
| SRS: ... + neighbours ≤ 12° | 1.54 (1.30-1.84) | 1.14 (0.97-1.46) | 0.94 (0.76-1.14) | 0.76 (0.62-0.86) | 1.46 (1.26-1.62) | 0.12 (0.06-0.14) |

- The region features improve the daily predictions (higher log-likelihood than sunspot number), but the Cycle 25 factor stays at 1.47-1.59. The ratio of the sunspot-number factor to the full-region factor is 0.94 (0.83-1.06). Thus a different mix of region types in Cycle 25 explains none of the per-sunspot excess. With the region models, Cycle 24 is the cycle with the fewest M flares per region; Cycle 23 is similar to or slightly above Cycle 24.
- The neighbour term changes the factor by 0.998 (0.975-1.021).
- Matched cycle phase (cycle months 0-83 only; 20 replicates): full region model C25/C24 1.49 (1.31-1.74), F10.7 0.83 (0.69-1.04).
- On the operational scale the full region model gives C25/C24 = 2.37 (1.92-2.80). The flux-scale change accounts for a factor of 1.54 of this.
- X1+ flares (20 replicates): C25/C24 is 1.21 (0.92-1.59) with the full region model, 1.26 (0.94-1.88) with sunspot number and 0.76 (0.50-1.20) with F10.7. No normalization shows a clear X-flare excess on one scale.
- A day-level crowding term (log10 of total SRS area or of SSN) is positive, but it lowers the C25/C24 factor of the full region model only to 1.40-1.48 (`files/results/activity_term.csv`).

### 4.2 HMI SHARP flux removes most of the excess (Figure 1b)

Table 2. C25/C24 M1+ rate ratio on the same 5,506 days of 2010-05 to 2026-10 (60 replicates; `files/results/sharp_models_true_M1_main.csv`).

| Normalization | C25/C24 | Fit on C24, predict C25 (obs/pred) | Δ log-lik/day vs SSN |
| --- | --- | --- | --- |
| SWPC sunspot number | 1.38 (1.05-1.79) | 1.46 (1.13-1.99) | 0 |
| F10.7 | 0.82 (0.65-1.05) | 0.87 (unstable) | 0.12 |
| SRS regions: area | 1.55 (1.24-1.99) | 1.57 (1.25-2.02) | 0.01 (-0.06-0.06) |
| SRS regions: full | 1.55 (1.29-1.90) | 1.61 (unstable) | 0.05 |
| HMI SHARP: unsigned flux | 1.15 (0.91-1.54) | 1.13 (0.90-1.57) | 0.09 (0.03-0.16) |
| HMI SHARP: flux + R + TOTUSJH | 1.21 (1.08-1.47) | 1.24 (1.11-1.61) | 0.22 (0.13-0.34) |

"Unstable": in some bootstrap replicates a rare McIntosh class or the extreme F10.7 values of Cycle 25 do not occur in the Cycle 24 training days, and the extrapolated prediction fails. We give the point estimate only.

- The paired ratio of the SRS-full factor to the SHARP-full factor is 1.28 (1.10-1.47). The ratio to the SHARP-flux factor is 1.35 (1.19-1.49).
- The SHARP-full model has the highest out-of-sample log-likelihood of all models.
- Matched cycle phase (C24 months 0-83; 20 replicates): SHARP flux 1.16 (0.98-1.37), SHARP full 1.19 (1.10-1.37), SRS full 1.54 (1.35-1.78).
- M5+ (20 replicates): SHARP full 0.98 (0.86-1.25), SRS full 1.31 (1.04-1.68). X1+: SHARP full 0.89 (0.62-1.25), SRS full 1.23 (0.73-2.00). With HMI flux, Cycle 25 shows no excess of large flares.
- With a day-level term for the total HMI flux on the disk, the SHARP-full factor is 1.14 (0.93-1.31). The term is positive (0.55, 0.23-0.96 per dex): at the same HARP fluxes, crowded days give more M flares.

### 4.3 Year by year (Figure 2)

Figure 2 shows the yield factor of each year at matched SRS regions (1998-2026) and at matched SHARP parameters (2010-2026); the mean of the Cycle 24 years is 1 (`files/results/yearly_yield.csv`, 100 replicates; `sharp_yearly_yield.csv`, 40 replicates). We merged quiet years (2008-2009, 2018-2019) and put 2019-12 into 2020.

- At matched SRS regions (true scale), the active years of Cycles 23 and 24 have factors 0.76-1.31, except 2001 (1.47, 1.15-1.83). The Cycle 25 years have 1.16 (2022), 1.44 (1.18-1.73, 2023), 2.00 (1.67-2.48, 2024), 1.25 (1.01-1.59, 2025) and 1.45 (0.76-2.06, 2026 to November).
- NCEI science-quality detections of one primary satellite, which use a different detection algorithm, give the same factors (for example 2024: 1.91, 1.58-2.38). Thus the Cycle 25 excess at matched SRS regions is not a property of the SWPC event list.
- On the operational scale, the Cycle 25 years have factors 1.77-3.07.
- At matched SHARP parameters, the Cycle 24 active years have 0.89-1.19 and the Cycle 25 years have 1.00 (2022), 1.20 (1.00-1.51, 2023), 1.35 (1.16-1.65, 2024), 1.12 (0.90-1.27, 2025) and 1.27 (0.76-1.67, 2026). Only 2024 is clearly above the Cycle 24 range.
- Declining-phase and minimum years (2006-2008, 2016, 2018-2020) have low factors in all models. Thus the flare yield of a region depends on cycle phase, and a comparison of an incomplete cycle with a complete one must match the phase (Section 4.1, 4.2).

### 4.4 The remaining excess is in multi-region complexes (Figure 3)

Table 3. HARP-level Poisson model, |LON_FWT| ≤ 60°, 13,825 HARP-days (200 replicates; `files/results/harp_complex_M1.csv`).

| Quantity | Cycle 24 | Cycle 25 |
| --- | --- | --- |
| HARP-days, single-region / multi-region | 5,424 / 1,135 | 5,424 / 1,842 |
| M1+ flares, single / multi | 482 / 196 | 535 / 839 |
| Share of SRS spot area in multi-region HARPs | 0.35 (0.29-0.39) | 0.50 (0.45-0.55) |
| Share of M1+ flares from multi-region HARPs | 0.29 (0.19-0.39) | 0.61 (0.52-0.70) |
| HMI flux per SRS area (10²⁰ Mx/MSH), single / multi | 0.97 / 1.01 | 1.09 / 1.19 |

| C25/C24 rate per HARP-day | Single-region HARPs | Multi-region HARPs |
| --- | --- | --- |
| At matched HMI flux, true scale | 0.99 (0.69-1.38) | 1.72 (1.23-2.57) |
| At matched SRS area, true scale | 1.19 (0.81-1.71) | 2.29 (1.64-3.40) |
| At matched HMI flux, operational scale | 1.41 (0.98-1.98) | 3.00 (2.11-4.68) |
| At matched HMI flux + δ flag, true scale | 1.00 (0.74-1.33) | 1.78 (1.36-2.62) |

- Isolated regions produced the same number of M flares per unit of HMI flux in both cycles.
- In Cycle 24, a multi-region HARP gave fewer M flares than a single-region HARP of the same total flux (ratio 0.48, 0.32-0.66). In Cycle 25 this deficit was much smaller (0.48 × 1.72 / 0.99 ≈ 0.82).
- For X1+ flares (68 in C25, 42 in C24) the ratios are 0.96 (0.46-2.18) for single and 0.88 (0.40-2.80) for multi-region HARPs (`harp_complex_X1.csv`).
- The SRS description agrees: on δ region-days, Cycle 25 gave 1.11 M flares per region-day against 0.98 in Cycle 24 (1.13 times). On non-δ region-days, it gave 4.7 M flares per 1000 SSN-days against 2.7 (C24) and 3.0 (C23) (`files/results/delta_counts_by_cycle.csv`).

### 4.5 Checks of the HMI flux scale (Figure 4)

- The daily total SHARP flux within 60° of central meridian divided by (F10.7 − 65 sfu) is 0.76-1.10 × 10²¹ Mx/sfu in every year with mean SSN ≥ 30 from 2010 to 2026, with no step between the cycles (`files/results/daily_totals_by_year.csv`). F10.7 is an independent radio measurement. Thus a drift of the HMI flux scale does not explain the result.
- For one-to-one HARP-region pairs (8,673 pairs), the flux per SRS area at matched area, McIntosh class, Hale class and position is 1.05 (1.00-1.11) times higher in Cycle 25 (cluster-robust OLS). Year factors relative to 2014 are 0.81-1.13 and show no step at December 2019 (2025 is low at 0.82).
- The total HMI flux per sunspot number was 5.7-6.8 × 10²⁰ Mx in 2011-2015 and 7.6-8.8 × 10²⁰ Mx in 2022-2024. Most of the extra Cycle 25 flux was in HARPs with several NOAA regions.

### 4.6 δ-regions and the operational scale

Table 4. SWPC SRS δ-regions (`files/results/delta_counts_by_cycle.csv`).

| | C23 (from 1998-06) | C24 | C25 to 2024-12 | C25 to 2026-11 |
| --- | --- | --- | --- | --- |
| Distinct δ-regions | 177 | 133 | 139 | 217 |
| δ-regions per 1000 SSN-days | 0.49 | 0.67 | 1.00 | 1.04 |
| M1+ per δ-region, true scale | 3.58 | 3.51 | 3.86 | 3.75 |
| M1+ per δ-region, operational scale | 2.53 | 2.44 | 3.86 | 3.75 |
| X1+ per δ-region, true scale | 0.50 | 0.31 | 0.30 | 0.26 |

On the operational scale Cycle 25 δ-regions seem about 1.5 times more M-productive than Cycle 23 and 24 δ-regions. On one scale they are equal within about 10%. The SWPC SRS does not support the statement that Cycle 25 has fewer δ-regions than Cycle 24; Louis (2025) used a different region catalogue (Solar Monitor), which can explain the difference.

## 5. Interpretation

On one flux scale, the Cycle 25 M-flare "excess" per sunspot is not an excess of flare-productive SRS region types, and it is not an excess of flares from isolated regions of a given magnetic flux. A larger fraction of the Cycle 25 flux and spot area was in large multi-region magnetic complexes (for example, the 2024 complexes), and these complexes gave more M flares per unit flux than the Cycle 24 complexes. SWPC counts the regions of such a complex separately, so normalizations that are based on spots or on SRS regions do not see the complex. HMI SHARP patches do. With HMI flux, the remaining Cycle 25/Cycle 24 factor is 1.15-1.21 for M1+ flares and about 1 for M5+ and X1+ flares. A day-level crowding term lowers it to 1.14 (0.93-1.31).

F10.7 tracks the total HMI flux with a constant ratio in 2010-2026, and F10.7 gives a C25/C24 factor below 1 (0.82-0.91). Thus the total flux on the disk over-corrects, and the distribution of the flux into patches and complexes matters. F10.7 also fails between Cycles 23 and 24 (0.72). No single full-disk index gives a cycle-invariant M-flare rate over Cycles 23-25. A cycle-invariant normalization needs magnetic information at the scale of active-region patches.

For forecasting: flare climatologies by McIntosh or Hale class that were fitted on GOES-1 to GOES-15 classes under-predict GOES-R era counts by about 1.5 because of the flux scale. On one scale, per-class rates still differ between cycles by 1.1-1.5, mainly through multi-region complexes.

## 6. Limitations

- HMI covers only Cycles 24 and 25. We could not test Cycle 23 with magnetic flux (MDI was not used).
- Cycle 25 is not complete. Most of its M flares occurred in 2023-2024 (905 of 2,108 true-scale M flares in 2024). The results can change as the decline phase continues.
- The multi-region classification depends on HARP definitions and on how SWPC numbers regions within one complex. The full-disk SHARP model does not use NOAA numbers and gives the same conclusion (1.15-1.21).
- The NOAA_ARS keyword lists the NOAA regions of a HARP; we linked them to the SRS regions of the same day. HARPs without a NOAA number take part in the full-disk model but not in the HARP-level test.
- The residual M1 factor of 1.15-1.21 that disappears at M5 can have instrumental parts near the M1 threshold (for example, differences between the GOES-15 and GOES-R event detection). The NCEI detections agree with the SWPC list at matched SRS regions, but we did not fit the SHARP models to the NCEI detections.
- The SWPC flare-to-region assignment is incomplete before 2003 (51-87% for M flares); only the HARP-level test and Table 4 use it.
- Bootstrap replicates: 20 for the variants. Blocks of 27 days do not represent dependence across rotations of long-lived complexes; intervals can be too narrow.
- The models use one constant factor per cycle and assume additive regions; the crowding test shows that additivity is approximate.

## 7. Reproduction

```
bash files/code/00_fetch_data.sh <work> ./campaign      # SWPC, JSOC and prior-bundle inputs into <work> (scratch)
python -I files/code/01_parse.py <work>
python -I files/code/02_tables.py <work>
python -I files/code/02b_neighbours.py <work> 12
python -I files/code/05_sharp_parse.py <work>
python -I files/code/07_flux_per_area.py <work>
for s in 0 1 2; do BOOT_SEED=$s BOOT_CHUNK_ONLY=1 python -I files/code/03_models.py <work> 20 true M1 27 main & done
for s in 0 1 2; do BOOT_SEED=$s BOOT_CHUNK_ONLY=1 python -I files/code/06_sharp_models.py <work> 20 true_M1 main & done
BOOT_CHUNK_ONLY=1 python -I files/code/03_models.py <work> 20 true M1 27 phase      # also: true X1, ops M1
BOOT_CHUNK_ONLY=1 python -I files/code/06_sharp_models.py <work> 20 true_M1 phase   # also: true_M5, true_X1 main
wait
python -I files/code/12_merge_boots.py <work>; python -I files/code/12b_paired.py <work>
python -I files/code/04_yearly.py <work> 100
python -I files/code/08_harp_complex.py <work> 200 M1; python -I files/code/08_harp_complex.py <work> 200 X1
python -I files/code/09_sharp_yearly.py <work> 40
python -I files/code/10_activity_term.py <work> 40
python -I files/code/13_delta_counts.py <work>
python -I files/code/11_figures.py <work> <work>/figs
```

`04_yearly.py` also reads the prior bundle file `daily_counts_forecasts_noaa.csv.gz` at `<work>/prior/cf94434cc907/files/data/` (the fetch script writes it there). Set `OMP_NUM_THREADS=1`. Software: Python 3.12, numpy 2.5, pandas 3.1, scipy, statsmodels 0.15, patsy 1.0, matplotlib 3.11. Random seeds are fixed. Compare the input file names and hashes with `files/data/input_sha256.txt`; later SWPC 2026 files, NCEI reissues and JSOC reprocessing can change the inputs.

## 8. Files

- `files/code/`: all scripts (`common.py` holds the region-sum model).
- `files/data/region_days.csv.gz`: 45,202 SRS region-days (1998-06 to 2026-11) with features, neighbour terms and assigned flare counts on three scales.
- `files/data/xra_events_regions.csv.gz`: 54,546 XRA events with NOAA region and operational, true and legacy peak flux.
- `files/data/daily_regions_no_f107.csv.gz`: daily counts and region summaries (F10.7 removed).
- `files/data/sharp_harp_days.csv.gz`, `sharp_harp_noaa_links.csv.gz`: SHARP keywords at 00 TAI per HARP-day and the HARP-NOAA links.
- `files/data/input_sha256.txt`: hashes of all inputs.
- `files/results/`: all result tables named in the text; `files/results/boots/` holds the raw bootstrap replicates.
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: sources and terms of external data.

## 9. Provenance

Automated research agent (model claude-opus-5-5, account claude-olen) in SCI campaign 11_07_2026, job sci-1107-hp-astronomy-b84b82dd3280, topic astronomy, machine hp, 2026-11-10. Inputs were fetched on 2026-11-10 from NOAA SWPC (FTP), JSOC (HTTP keyword service) and the local campaign copy of the prior SCI bundle. The signing key is a campaign-machine key.
