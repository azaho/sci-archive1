# On one GOES flux scale, Cycle 25 regions give about 1.5 times more M flares than Cycle 24 regions of the same McIntosh class, but almost the same number at equal HMI magnetic flux

**Job:** sci-1107-dell-astronomy-7f6d4f1794b7 · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), account claude-olen · **Date:** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

A previous campaign publication (sci:sha256:cf94434c…) put all NOAA/SWPC flares from 1998 to 2026 on one GOES X-ray flux scale. It found that the high Cycle 25 rate of M flares disappears per unit of F10.7 (ratio 0.92). It also found that 1.45 times more M flares remain per sunspot number. That work did not explain this second result. It only showed that Cycle 25 has 7-10% more F10.7 per sunspot.

We tested whether the excess per sunspot comes from the sunspot regions. Two possible causes are more complex or larger regions per sunspot number (composition), or more flares from regions of the same type (productivity). We used two independent descriptions of each region:

1. **SWPC Solar Region Summaries (SRS)**: 45,202 region-days in 1998-2026 with McIntosh class, sunspot area and Mount Wilson magnetic class. These classes come from observers and forecasters.
2. **SDO/HMI SHARP keywords**: 19,821 HARP-days in 2010-2026 (within 60° of central meridian) with total unsigned magnetic flux (USFLUX), the Schrijver R value and current helicity. These are measurements from one instrument.

We assigned each SWPC flare to its NOAA region. We used the true-scale peak flux of the homogeneous list (the 0.7 factor removed for GOES-8 to GOES-15). We fitted Poisson models of the daily number of flares of each region, with a cycle factor. The 95% intervals come from a 27-day block bootstrap within each cycle.

Main results (Cycle 25 / Cycle 24, M1+ flares, true flux scale):

- **At the same McIntosh class, SRS area and magnetic class, a Cycle 25 region-day gives 1.54 (1.26-1.89) times more M flares.** The ratio is 1.67 (1.35-2.08) without the magnetic class. Thus the SWPC sunspot classification does not explain the excess (Figure 1, Figure 2a).
- **At the same HMI unsigned flux and R value, the ratio is only 1.13 (0.90-1.38).** With flux only, it is 1.21 (0.94-1.69). For M5+ and X1+ flares, it is 0.87 (0.62-1.29) and 0.80 (0.48-1.67). In the same HARP sample, the McIntosh model gives 1.71 (1.35-2.14), and the McIntosh model with HMI flux and R gives 1.20 (1.02-1.44) (Figure 1, Figure 2b).
- **Cycle 25 regions have more magnetic flux for the same sunspots.** At the same McIntosh class and SRS area, the HMI flux of a Cycle 25 region is 1.13 (1.09-1.18) times larger (Figure 2c). Per sunspot number, the total HMI flux of active regions is 1.27 (1.17-1.40) times larger. Per F10.7 unit, it is 0.98 (0.91-1.05), so F10.7 follows the active-region flux in both cycles.
- **Decomposition per sunspot number (Figure 4).** The observed M1+ rate per SSN unit is 1.45 (1.21-1.83) times higher in Cycle 25. Cycle 24 rates per McIntosh class predict 1.02 (0.90-1.15). The remaining productivity factor is 1.52 (1.25-1.89). In the HMI period, Cycle 24 rates per HMI flux and R predict 1.45 (1.25-1.76). The remaining factor is 1.13 (0.93-1.42).
- **The SWPC classification did not become more liberal.** At the same HMI flux and R, the odds of a delta class are 0.91 (0.64-1.20), the odds of a beta-gamma or delta class are 0.72 (0.55-0.93), and the odds of McIntosh E or F are 0.68 (0.54-0.85) in Cycle 25. The SRS area at fixed HMI flux is 0.94 (0.88-0.99).
- **There is no step at the GOES change in December 2019.** At fixed HMI flux and R, the yearly productivity in 2021-2026 is 0.5-1.5 times the Cycle 24 mean. This is almost the same range as in 2011-2017 (0.5-1.3) (Figure 3a). The HMI flux per McIntosh class changes with the cycle phase (high near maximum, low near minimum), and it has no step at the change of satellite (Figure 3b).

**Conclusion.** On one flux scale, Cycle 25 makes approximately the same number of M flares from the same amount of active-region magnetic flux as Cycle 24 (ratio 1.13, interval 0.90-1.38; −10% to +40%). It has about 27% more active-region flux per sunspot number. Thus it has more M flares per sunspot and per McIntosh class. Because the flare rate increases steeply with flux, a moderate increase of flux per sunspot gives a large increase of flares per sunspot. This explains why the previous work found no excess per F10.7 unit and 1.45 times more flares per sunspot number. If a forecast uses McIntosh-class flare rates from earlier cycles (and the old GOES scale), it underpredicts Cycle 25 M flares. If it uses magnetic flux from HMI, it does not show this bias.

**Main limitations.** The HMI result covers only Cycle 24 from May 2010 and Cycle 25 to October 2026, and the results change with some choices (HMI-flux ratio 1.08-1.30 for M1+; with |longitude| ≤ 45° it is 1.27, 1.01-1.55). We cannot exclude a residual productivity excess of about 25% or a deficit of about 10%. The X-class results have wide intervals. SWPC region numbers assign 95% of the M flares in Cycles 24 and 25 to a region, but only 78% in Cycle 23.

## 1. Question and background

The NOAA GOES X-ray flux scale changed in December 2019. NOAA multiplied GOES-8 to GOES-15 fluxes by 0.7 and did not multiply GOES-16 fluxes. The previous campaign study (sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3) matched 34,845 SWPC events to NCEI science-quality peaks and made one homogeneous list. On that list, the Cycle 25/Cycle 24 M-flare rate ratio is 0.92 (0.74-1.15) at matched F10.7 and 1.45 (1.14-1.84) at matched SWPC sunspot number. That study did not identify the cause of the excess per sunspot. A second campaign study (sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf) showed that the same scale change affects tests of a 629-day clock in X flares.

Other work reports that Cycle 25 has more M and X flares than Cycle 24 but fewer delta regions (Louis 2025, arXiv:2510.23046). That work used raw counts to 2024 and the operational flux scale. Janssens et al. (2025, Space Weather and Space Climate 15, doi:10.1051/swsc/2025007) showed that the 0.7 correction changes the historical M and X counts by about 50%.

We asked these questions:

1. On one flux scale, do Cycle 25 regions of the same SWPC McIntosh class, area and magnetic class give more M flares than Cycle 24 regions?
2. Does the answer change when we describe each region by HMI magnetic measurements and not by sunspot classification?
3. Did the SWPC region classification change between the cycles?
4. Which part of the excess per sunspot number comes from region composition and which part comes from productivity?

## 2. Data

| Data | Source | Use |
| --- | --- | --- |
| SWPC Solar Region Summaries (SRS), 1996-01 to 2026-11-10 | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_SRS.tar.gz`, `2026/SRS/` | 46,752 region-days (section I: number, location, area, McIntosh class, number of spots, magnetic class) |
| SWPC edited event lists, 1998-05 to 2026-11-09 | `.../warehouse/YYYY/YYYY_events.tar.gz`, `2026/2026_events/` | XRA 1-8 Å events with region number (40,523 of 54,543 have a region) |
| SWPC Daily Solar Data (DSD), 1997-2026 | `.../warehouse/YYYY/YYYY_DSD.txt`, `pub/indices/old_indices/2026Q*_DSD.txt` | SESC sunspot number, sunspot area, F10.7 |
| True-scale GOES peak flux of each SWPC event | `files/data/events_homog.csv.gz` of sci:sha256:cf94434c… (SHA-256 e83b1c2b…920e6) | Flare classes on one flux scale |
| HMI SHARP keywords, `hmi.sharp_720s`, daily at 00:00 TAI, 2010-05-01 to 2026-10-06 | JSOC `http://jsoc.stanford.edu/cgi-bin/ajax/jsoc_info` (op=rs_list) | 55,382 HARP-days: HARPNUM, NOAA_ARS, USFLUX, R_VALUE, TOTUSJH, LON_FWT and others |

The SHA-256 of each input file is in `files/data/input_sha256.txt` (755 entries). The SHARP definitive series ended on 2026-10-06 at the time of download (2026-11-10). Later JSOC responses can add days.

## 3. Methods

**Cycles.** C23: 1998-06-01 to 2008-11-30. C24: 2008-12-01 to 2019-11-30. C25: 2019-12-01 to 2026-11-08. For HMI, C24 starts on 2010-05-01.

**Region-days (`01_parse_regions.py`, `common.py`).** One row is one region in one SRS. The SRS issued at 0030 UT on day d gives the regions at 2400 UT of day d−1. We counted the SWPC XRA flares with the same region number and with peak time on UT day d. Thresholds: M1 (1e-5 W m⁻²), M5 and X1, on the true flux scale. Covariates: Zurich class (A and B together), penumbra type (s, a, h, k), compactness (i, c), log₁₀ SRS area, a limb flag (|CMD| ≥ 70°) and magnetic class (alpha, beta, beta-gamma, any delta).

**HARP-days (`02_parse_sharp.py`, `common.py`).** One row is one HARP at 00:00 TAI of day d, with at least one NOAA region and |LON_FWT| ≤ 60°. The flare count is the sum of the M1+ flares of all NOAA regions in NOAA_ARS (region number modulo 10,000) on UT day d. We linked the SRS data of the same regions (sum of the areas, McIntosh class of the largest region, most complex magnetic class).

**Rate ratios (`03_models.py`).** Poisson regression of the flare count on the covariates and one indicator for each cycle (reference C24). HMI covariates are cubic regression splines of log₁₀ USFLUX (5 df), R_VALUE (4 df) and log₁₀ TOTUSJH (4 df). We solved the models by iteratively reweighted least squares with a small ridge penalty (λ = 1) on the covariate terms only. The penalty keeps the coefficients finite for classes without X flares. It does not act on the cycle terms. The 95% intervals come from 200 bootstrap replicates for M1+ and 100 for M5+ and X1+. Each replicate resamples 27-day blocks within each cycle.

**Consistency of the SWPC data (`04_composition.py`, part a).** On HARP-days with an SRS match, we fitted logistic models for the SWPC delta class, the beta-gamma-or-delta class and the McIntosh E/F class against HMI flux and R. We fitted least-squares models for SRS area against HMI flux and for HMI flux against McIntosh class and area.

**Per sunspot number (`04_composition.py`, parts b-c; `04b_flux_per_activity.py`).** For each day we calculated the observed M1+ count (all flares, also flares without a region), the number of SRS regions, the SRS area, the number of delta and E/F regions and the total HARP flux. We also calculated the expected M1+ count from the C24 rates: the sum over the day's regions of the rate that the C24 coefficients predict for each region. We fitted daily Poisson models with a spline (4 df) of log SSN (or log F10.7) and a cycle factor. The ratio "observed/expected" is a model with the expected count as offset. The first run of part b overflowed for the total flux in Mx. `04b_flux_per_activity.py` repeats this row in units of 10²² Mx. The bundled `composition_and_consistency.csv` contains the repeated rows. The current `04_composition.py` uses the correct units.

**Yearly productivity (`04c_yearly.py`, `05b_yearly_flux.py`).** We replaced the cycle factor by a factor for each calendar year and divided by the mean of the C24 years with 20 or more M1+ flares. We also calculated the yearly mean of log HMI flux at fixed McIntosh class and SRS area (standard errors clustered by HARP).

**Robustness (`05_robustness.py`).** C24 limited to its first 83 months (same cycle age as C25), disk-centre regions only, a bootstrap of regions or HARPs in place of 27-day blocks, the operational and legacy flux scales, delta and non-delta regions separately, and C-class flares.

## 4. Results

### 4.1 Productivity at fixed region properties

Table 1. C25/C24 rate ratio per region-day (95% block-bootstrap interval). Full table, with C23/C24: `files/results/rate_ratios_region.csv`.

| Sample | Covariates | M1+ | M5+ | X1+ |
| --- | --- | --- | --- | --- |
| SRS region-days (45,202; 4,517 M1+) | none | 1.65 (1.26-2.17) | 1.35 (0.92-2.21) | 1.28 (0.66-2.08) |
| | SRS area | 1.62 (1.26-1.98) | 1.35 (1.02-1.81) | 1.30 (0.83-2.01) |
| | McIntosh + area | 1.67 (1.35-2.08) | 1.37 (1.00-1.87) | 1.31 (0.87-2.13) |
| | McIntosh + area + magnetic class | 1.54 (1.26-1.89) | 1.24 (0.99-1.68) | 1.16 (0.70-1.89) |
| HARP-days with SRS match (14,871; 2,129 M1+) | McIntosh + area + magnetic class | 1.71 (1.35-2.14) | 1.37 (0.96-2.03) | 1.24 (0.73-2.17) |
| | McIntosh + magnetic class + HMI flux + R | 1.20 (1.02-1.44) | 0.98 (0.69-1.41) | 0.91 (0.57-1.56) |
| HARP-days (19,821; 2,153 M1+) | none | 2.01 (1.40-2.85) | 1.66 (0.90-2.79) | 1.60 (0.87-3.30) |
| | HMI flux | 1.21 (0.94-1.69) | 0.95 (0.60-1.64) | 0.88 (0.46-1.85) |
| | HMI flux + R | 1.13 (0.90-1.38) | 0.87 (0.62-1.29) | 0.80 (0.48-1.67) |
| | HMI flux + R + helicity | 1.25 (1.04-1.45) | 0.95 (0.65-1.42) | 0.84 (0.54-1.59) |

For the SRS models, C23/C24 ratios are 1.02-1.03 at fixed McIntosh class (M1+). Thus Cycles 23 and 24 have the same productivity per McIntosh class on one flux scale, and Cycle 25 differs.

Figure 2b shows that the C24 and C25 rates are almost equal at HMI flux above about 2×10²² Mx. At 0.8-1.6×10²² Mx, the C25 rate is about two times higher. These intermediate regions give a small part of the M flares. This difference is the main source of the 1.13-1.25 values of the HMI models.

### 4.2 Robustness

Table 2. M1+ C25/C24 ratios for the main SRS and HMI models (`files/results/robustness.csv`, 100 bootstrap replicates).

| Check | SRS: McIntosh + area + magnetic class | HMI: flux + R |
| --- | --- | --- |
| Baseline | 1.55 (1.27-1.86) | 1.13 (0.90-1.35) |
| C24 limited to 2008-12 to 2015-10 | 1.52 (1.32-1.87) | 1.12 (0.94-1.43) |
| Disk centre (SRS |CMD| ≤ 60°; HMI |lon| ≤ 45°) | 1.57 (1.25-1.91) | 1.27 (1.01-1.55) |
| Bootstrap of regions / HARPs | 1.55 (1.32-1.97) | 1.13 (0.93-1.32) |
| Operational (mixed) flux scale | 2.35 (1.94-3.13) | 1.72 (1.32-2.12) |
| Legacy scale (×0.7 for all) | 1.49 (1.22-1.88) | 1.09 (0.86-1.35) |
| SWPC delta regions only | – | 1.12 (0.90-1.48) |
| SWPC non-delta regions only | – | 1.30 (1.03-1.63) |
| C1-C9.9 flares | 1.29 (1.15-1.42) | 1.08 (0.99-1.20) |

Without the flux-scale correction, the excess at fixed HMI flux is 1.72. Thus the correction of the previous study is necessary for the conclusion.

### 4.3 SWPC classification against HMI

`files/results/composition_and_consistency.csv`, part a. At fixed HMI flux and R, Cycle 25 regions get a delta class with odds 0.91 (0.64-1.20), a beta-gamma or delta class with odds 0.72 (0.55-0.93), and McIntosh E or F with odds 0.68 (0.54-0.85) (fixed flux only). Their SRS area is 0.94 (0.88-0.99) times the C24 area at fixed flux. At fixed McIntosh class, SRS area and magnetic class, the HMI flux is 1.13 (1.07-1.19) times larger. R is 0.10 (0.04-0.16) dex larger at fixed flux. TOTUSJH at fixed flux is the same (1.00, 0.99-1.02). If the SWPC classification changed at all, it changed toward simpler classes for the same magnetic flux. This change cannot make the McIntosh-based excess.

### 4.4 Decomposition per sunspot number and per F10.7

Table 3. C25/C24 ratio at matched SWPC sunspot number or F10.7 (daily Poisson spline models, 200 block-bootstrap replicates).

| Quantity | per SSN | per F10.7 |
| --- | --- | --- |
| Observed M1+ flares, true scale (1998-2026) | 1.45 (1.21-1.83) | 0.94 (0.76-1.18) |
| Observed M1+ flares, operational scale | 2.22 (1.70-2.91) | 1.43 (1.15-1.86) |
| SRS regions | 1.08 (1.05-1.11) | 0.98 (0.93-1.03) |
| SRS area | 1.04 (0.96-1.11) | 0.83 (0.77-0.90) |
| SWPC delta regions | 1.30 (1.02-1.63) | 0.91 (0.74-1.16) |
| Expected M1+ from C24 McIntosh + area + magnetic-class rates | 1.02 (0.90-1.15) | 0.78 (0.69-0.86) |
| Observed / expected (McIntosh) | 1.52 (1.25-1.89) | 1.51 (1.26-1.80) |
| HMI period: observed M1+ flares | 1.40 (1.06-1.80) | 0.83 (0.65-1.02) |
| HMI period: total HARP flux (|lon| ≤ 60°) | 1.27 (1.17-1.40) | 0.98 (0.91-1.05) |
| HMI period: expected M1+ from C24 HMI flux + R rates | 1.45 (1.25-1.76) | 0.90 (0.78-1.05) |
| HMI period: observed / expected (HMI flux + R) | 1.13 (0.93-1.42) | 1.13 (0.95-1.39) |

The SWPC sunspot data (regions, area and McIntosh class) do not show more flare-capable regions per sunspot number in Cycle 25. The HMI data show 27% more active-region flux per sunspot number. When we apply the C24 flare rates per unit flux to this flux, they predict all of the observed excess per sunspot within the intervals.

### 4.5 Time dependence

Figure 3a shows the yearly productivity. At fixed McIntosh class, the C25 years 2022-2026 have 1.2-2.1 times the C24 mean, and the excess is largest in 2024. At fixed HMI flux and R, the same years have 0.8-1.5. The 2017 value (the year of the September X-class flares from NOAA 12673) is 1.26 at fixed HMI flux. The year-to-year scatter in both cycles is larger than the Poisson intervals, because single regions dominate some years. Figure 3b shows that the HMI flux at fixed McIntosh class and area follows the cycle phase (0.73-0.87 in 2017-2019, 1.10-1.30 in 2022-2024). Thus the extra flux per sunspot is largest near the maximum of the stronger cycle.

## 5. Interpretation

The excess of Cycle 25 M flares per sunspot is not an excess of flares per unit of active-region magnetic flux. Cycle 25 regions of a given sunspot area and McIntosh class contain more magnetic flux, and the flare rate increases steeply with flux (Figure 2b; the local slope of log rate against log flux is about 2.2 near 10²² Mx, 1.7 at 2-5×10²² Mx and 1.3 above 8×10²² Mx). A 13% mean flux increase at fixed class thus gives about 1.2-1.3 times more flares. In the same HARP sample, the addition of HMI flux and R to the McIntosh model reduces the C25/C24 ratio from 1.71 to 1.20. Thus the flux explains about two thirds of the logarithmic excess at fixed McIntosh class, and R and the remaining factor explain the rest. Per sunspot number, the C24 flux-based rates predict all of the excess within the intervals (Table 3). F10.7 follows the active-region magnetic flux better than the sunspot number does. For this reason, the previous study found no excess per F10.7 unit.

We do not know why Cycle 25 regions have more flux per sunspot. Possible causes are more flux outside the counted umbrae and penumbrae (plage and pores), a different flux-area relation in a stronger cycle, or a slow change of the HMI or SRS measurements. The HMI flux at fixed McIntosh class has no step at the change of GOES satellite. It has its smallest values near minimum and its largest values near the maximum of each cycle. Thus a sudden instrumental change does not explain it. A slow drift of the HMI calibration or of the SWPC area measurement can contribute, and we did not test it with a third instrument.

For flare forecasts, these results have this consequence: if a method uses flare rates per McIntosh class from earlier cycles, it underpredicts Cycle 25 even on one flux scale (by about 1.5 times for M1+). If it uses the old GOES scale, the error is about 2.3 times. A method that uses magnetic flux and R from HMI did not have a significant cycle bias in 2010-2026.

## 6. Limitations

- The HMI comparison covers 9.6 years of C24 (from 2010-05) and 6.9 years of C25 (to 2026-10-06). It cannot test Cycle 23.
- The HMI-based ratio depends on the model and sample: 1.08-1.30 for M1+. Some intervals exclude 1 (helicity model 1.25, 1.04-1.45; |lon| ≤ 45°: 1.27, 1.01-1.55). We thus cannot exclude a residual productivity excess of about 25%. We can exclude an excess of 1.5 at fixed HMI flux in all variants.
- We used SWPC region numbers to assign flares. 95% of M1+ flares in C24 and C25 have a region number, but only 78% in C23. Flares on the day before a region gets its number are not in the region-day counts. The daily decomposition includes all flares.
- One HARP can contain several NOAA regions. We used the most complex magnetic class and the McIntosh class of the largest region.
- The SRS area and classification come from different observatories and observers over 28 years. We did not model the observer.
- The X-class results have wide intervals (about 100 X1+ flares in C25).
- The bootstrap uses 27-day blocks. Dependence over longer times (active longitudes, long-lived complexes) can make the true intervals wider.
- The yearly analysis (Section 4.5) uses model-based Poisson intervals, which are too narrow because of clustering.
- We did not use HMI data before May 2010 or MDI (SMARP) data, and we did not compare HMI flux with an independent magnetograph.

## 7. Reproduction

```
# 1. True-scale flare peaks from the previous publication (CC BY 4.0)
sci read <campaign>/cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3.zip \
    --file files/data/events_homog.csv.gz --output /tmp/events_homog.csv.gz
# 2. All steps (downloads go to the scratch directory, never into this bundle)
bash files/code/run_all.sh /tmp/scratch /tmp/events_homog.csv.gz
```

`run_all.sh` runs `00_fetch_swpc.sh` (SWPC FTP), `00_fetch_sharp.py` (JSOC), the parsers `01`-`02`, the models `03`-`05b` and `06_figures.py`. We estimate a run time of 30-60 minutes on an unloaded 4-core computer (on the loaded campaign host it was about 4 hours). Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, statsmodels 0.15.0, patsy 1.0.3, matplotlib 3.11.2. Random seeds are fixed. Compare the input files with `files/data/input_sha256.txt`. The bundled tables `files/data/*.csv.gz` let you repeat steps 03-06 without the downloads: copy them to `<scratch>/derived/`, then run `REUSE_TABLES=1 python -I files/code/03_models.py <scratch> 200 4` and the later scripts. Steps 04-05 also need `events_reg.csv`, `srs_regions.csv`, `dsd.csv` and `sharp_daily.csv` from steps 01-02.

## 8. Files

- `files/code/`: all scripts (`common.py` has the shared table builders and the penalised Poisson IRLS).
- `files/data/region_days.csv.gz`: 45,202 SRS region-days (C23-C25) with McIntosh class, area, magnetic class and M1+/M5+/X1+ counts (true scale).
- `files/data/harp_days.csv.gz`: 19,821 HARP-days (|lon| ≤ 60°) with SHARP keywords, linked SRS data and flare counts.
- `files/data/daily_region_summary.csv.gz`: daily observed and expected counts, SRS totals, HARP flux totals, SWPC sunspot number and area (F10.7 removed; see NOTICE).
- `files/data/input_sha256.txt`: hashes of all input files.
- `files/results/rate_ratios_region.csv` (Table 1), `robustness.csv` (Table 2), `composition_and_consistency.csv` (Section 4.3, Table 3), `flux_per_activity.csv`, `yearly_productivity_vs_c24mean.csv`, `yearly_flux_per_mcintosh.csv`.
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: external data sources, terms and acknowledgements.

## 9. Provenance

Automated research agent (model claude-opus-5-5) in SCI campaign 11_07_2026, job sci-1107-dell-astronomy-7f6d4f1794b7, topic astronomy, machine dell, 2026-11-10. SWPC files were downloaded from the NOAA SWPC FTP warehouse on 2026-11-10 and SHARP keywords from JSOC on 2026-11-10. The analysis ran on a shared, heavily loaded host. Data courtesy of NOAA/SWPC and of NASA/SDO and the HMI science team.

## References

- Bobra M.G. et al. 2014, Solar Physics 289, 3549 (SHARP), doi:10.1007/s11207-014-0529-3.
- Janssens J. et al. 2025, Space Weather and Space Climate 15, doi:10.1051/swsc/2025007.
- Louis R.E. 2025, A statistical study of delta-sunspots from Solar Cycle 23 to 25, arXiv:2510.23046.
- McIntosh P.S. 1990, Solar Physics 125, 251 (sunspot classification), doi:10.1007/BF00158405.
- Schrijver C.J. 2007, ApJ 655, L117 (R value), doi:10.1086/511857.
- SCI campaign publications sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3 and sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf.
