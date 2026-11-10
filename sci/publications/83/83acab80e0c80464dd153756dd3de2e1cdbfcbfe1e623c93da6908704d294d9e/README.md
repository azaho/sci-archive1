# On one GOES flux scale, Cycle 25 active regions produce about 1.6 times more M flares than Cycle 24 regions of the same McIntosh and magnetic class; HMI magnetic measures explain most of this excess

## Summary

A prior SCI publication (sci:sha256:cf94434c…) made one homogeneous GOES flare list for 1998-2026, on the true (science) flux scale. On that scale, Cycle 25 has the same M-flare rate per unit F10.7 as Cycle 24 (ratio 0.92). But Cycle 25 has about 1.45 times more M flares per sunspot (number or area). That publication did not explain this per-sunspot excess. Two explanations are possible:

- **Composition:** Cycle 25 has more large or complex sunspot groups per sunspot count.
- **Productivity:** each Cycle 25 region produces more flares than a Cycle 24 region of the same type.

We attributed the SWPC flares (with their true-scale peak flux) to the active regions of the daily SWPC Solar Region Summary (SRS). This gave 45,202 region-days in 1998-2026. We compared the flare rates of regions with the same McIntosh class, magnetic (Mount Wilson) class and spot area. We then repeated the test with HMI SHARP magnetic parameters (19,838 HARP-days, 2010-2026). This test uses one instrument for Cycles 24 and 25.

Main results (Cycle 25 / Cycle 24, M1 or larger flares, true scale, 95% intervals from a 27-day block bootstrap):

- **Composition does not explain the excess.** The C24 class rates, applied to the regions of each day, predict an M-flare rate per sunspot number in Cycle 25 that is 0.96 (0.82-1.11) times the Cycle 24 value. Per sunspot area it is 0.94 (0.86-1.04). The observed full-disk ratio per sunspot number is 1.45 (1.14-1.82).
- **The excess is in the productivity of each region.** At matched McIntosh class and magnetic class, Cycle 25 regions produced 1.61 (1.32-1.99) times more M flares than Cycle 24 regions. The result is stable in all variants (1.44-1.80): other strata, Cycle 24 at the same cycle age, regions near disk centre only, each hemisphere, and without the 10 most productive regions of each cycle. With the operational flare list, the ratio is 2.44 (1.97-3.02). Thus, about half of the apparent region excess (in logarithm) comes from the removed 0.7 factor, and half is real on one scale.
- **The excess is in M1-M5 flares.** For M5 or larger flares the ratio is 1.24 (0.88-1.74), and for X1 or larger flares it is 1.16 (0.70-2.06). For C1 or larger flares it is 1.33 (1.20-1.46).
- **HMI magnetic measures explain most of the region excess.** At matched SHARP unsigned flux (USFLUX), the Cycle 25/24 ratio is 1.20 (0.88-1.58). At matched current helicity (TOTUSJH) it is 1.13 (0.91-1.41). At matched polarity-inversion-line flux (R_VALUE) it is 1.13 (0.91-1.40). With four magnetic parameters it is 1.22 (1.05-1.46). On the operational scale, the same four-parameter ratio is 1.87 (1.58-2.24).
- **Cycle 25 regions of the same SRS class are magnetically stronger.** At matched McIntosh class, magnetic class and spot area, the Cycle 25 regions have 1.05 (0.99-1.11) times more USFLUX, 1.06 (1.01-1.11) times more TOTUSJH, and 0.14 dex (0.08-0.22) more R_VALUE, which is about 1.4 times more flux near strong-gradient polarity-inversion lines. In the subsample of 10,005 region-days with both SRS and SHARP data, the ratio is 1.28 with SRS terms only, 1.19 with HMI terms only, and 1.04 (lower bound 0.85) with both.
- **Full disk:** Cycle 25 has 1.16 (1.09-1.25) times more SHARP magnetic flux per SWPC sunspot number and 1.19 (1.10-1.31) times more per sunspot area. F10.7 per unit SHARP flux is 1.07 (1.05-1.09) times higher. The M-flare rate per unit of full-disk SHARP flux is 1.25 (1.00-1.51) times the Cycle 24 value, against 1.39 (1.18-1.71) per sunspot number in the same 2010-2026 days.

Interpretation: on one flux scale, the Cycle 25 M-flare excess per sunspot is not a change in the mix of sunspot-group classes. It is a higher flare rate per region of the same class. Cycle 25 regions of a given class carry more magnetic flux and much more flux at strong-gradient polarity-inversion lines. When the regions are matched on HMI magnetic parameters, the excess becomes small (1.1-1.2) and is not clearly different from 1 for single parameters. Sunspot-based indices (number, area, McIntosh class) thus under-count the flare-relevant magnetic flux in Cycle 25 compared with Cycle 24. For forecasts, McIntosh-class flare rates from Cycles 23-24 with operational (x0.7) classes under-predict Cycle 25 operational M-flare rates by a factor of about 2.4. Of this factor, about 1.5 is the flux scale and about 1.6 is the higher productivity per class.

Limitations: two complete cycles and one incomplete cycle; one constant cycle factor per model; SRS classes are subjective and the SWPC classification practice can change; the SRS-HMI subsample is small; HMI calibration was checked only with internal tests (no step in mean field of large regions); 15-17% of M flares in Cycles 24-25 (27% in Cycle 23) could not be attributed to an SRS region of the same day.

## 1. Question and background

The NOAA/SWPC flare classes for GOES-8 to GOES-15 include a 0.7 factor. GOES-16 and later satellites do not use it. The factor was removed in December 2019, at the start of Cycle 25. The prior campaign publication (sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3) matched 34,845 SWPC events to NCEI science-quality peaks and built one homogeneous list on the true scale. With that list, the Cycle 25 excess of M flares per F10.7 unit disappeared (0.92, 0.74-1.15), but an excess per sunspot remained (1.45, 1.14-1.84). That publication said that the remaining excess agrees with 7-10% more F10.7 per sunspot in Cycle 25, but it did not test a mechanism.

We asked:

1. Is the per-sunspot excess a change in the population of regions (composition) or in the flare rate per region of the same type (productivity)?
2. Does an instrument-homogeneous magnetic measure (SDO/HMI, 2010-2026) explain the excess?
3. How large is the error of class-based flare rates (for example, McIntosh Poisson rates) when they are trained on pre-2020 operational classes and used in Cycle 25?

Flare rates per McIntosh class are a standard forecast base (for example, Bloomfield et al. 2012, ApJL 747, L41, with 1988-2008 operational classes). Space-weather summaries of Cycle 25 often compare raw flare counts across the scale change. We did not find a published region-level comparison of Cycles 24 and 25 on one flux scale.

## 2. Data

| Data | Source and version | Use | Terms |
| --- | --- | --- | --- |
| SWPC Solar Region Summary (SRS), 1996-01 to 2026-11-10 | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_SRS.tar.gz`; `.../2026/SRS/` | Daily region number, location, area, McIntosh class, number of spots, magnetic class (valid 00 UT) | US Government work, public domain |
| SWPC edited event lists, 1996-2026-11-09 | `.../warehouse/YYYY/YYYY_events.tar.gz`; `.../2026/2026_events/` | XRA 1-8 Å events with region number | Public domain |
| SWPC Daily Solar Data (DSD) | `.../warehouse/YYYY/YYYY_DSD.txt`; `pub/indices/old_indices/2026Q*_DSD.txt` | F10.7 (Penticton, NRC Canada), SESC sunspot number and area | Public domain (SWPC); F10.7 values not redistributed here |
| Homogeneous flare list and daily table of the prior publication | sci:sha256:cf94434c…, files `events_homog.csv.gz`, `daily_counts_forecasts_noaa.csv.gz` | True-scale and legacy-scale peak flux for each SWPC event; daily full-disk counts | CC BY 4.0 (SCI campaign) |
| HMI SHARP keywords, `hmi.sharp_720s` (definitive), 2010-05-01 to 2026-10-06, one record per HARP at 00:00 TAI | JSOC `http://jsoc.stanford.edu/cgi-bin/ajax/jsoc_info?op=rs_list` | USFLUX, TOTUSJH, TOTPOT, R_VALUE, AREA_ACR, NOAA_ARS, LON_FWT | NASA SDO open data; acknowledgement requested |

The SHA-256 values of all 920 input files are in `files/data/input_sha256.txt`. The 2026 SWPC directories and the JSOC definitive series grow with time.

## 3. Methods

**Parsing (`01_parse_regions.py`).** We read section I ("Regions with Sunspots") of each SRS. The 4-digit region numbers wrap at 10000 in June 2002; we restored the full NOAA numbers. We read all XRA 1-8 Å events with their 4-digit region field and joined them to the prior homogeneous list by date, times, satellite and class (all 54,543 events joined).

**Region-days (`02_region_days.py`).** The SRS issued on UT day D describes the regions at 00 UT of day D. For each region-day, the outcome is the number of SWPC flares from that region with peak on day D, on the operational, true and legacy (true x 0.7) scales. Cycles: C23 1998-06-01 to 2008-11-30, C24 2008-12-01 to 2019-11-30, C25 2019-12-01 to 2026-11-08. We have 20,109, 12,126 and 12,967 region-days (2,776, 1,738 and 1,812 regions) with 1,709, 1,014 and 1,794 attributed true-scale M flares. Of all true-scale M flares with a region number, the region was in the SRS of the same day for 72.5% (C23), 83.2% (C24) and 84.5% (C25). In C23, only 78% of the M flares have a region number (C24 96%, C25 95%). Thus C23 region rates are biased low by about 15% relative to C24 and C25. The C24/C25 comparison has the same attribution rate.

**Region productivity (`03_region_models.py`, `06_sensitivity.py`).** (a) Indirect standardisation: for each cycle, the observed count divided by the expected count, where the expected count uses the C24 rate of each stratum (McIntosh class x magnetic class: alpha, beta, beta-gamma, any delta). (b) Poisson regression with McIntosh components (Z, p, c), magnetic class, a spline of log area and a cycle term. Intervals: bootstrap of 27-day blocks within each cycle (300 replicates for the main results). The regression bootstrap had degenerate replicates; we report only its point estimates. Sensitivity variants are in `files/results/sensitivity_oe.csv`.

**Composition (`03_region_models.py`).** We fitted the Poisson model on C24 regions only and applied it to the regions of each day. The sum over regions, E24(d), is the flare rate that day d would have with C24 productivity. We fitted daily counts and E24 against a spline of log(activity index) plus cycle terms (sunspot number, sunspot area, F10.7). The cycle term for E24 is the composition ratio.

**HMI SHARP (`00b_fetch_sharp.py`, `04_parse_sharp.py`, `05_sharp_models.py`, `08_class_flux.py`).** For each HARP at 00:00 TAI we added the flares of all NOAA regions in NOAA_ARS with peak on that UT day. We used HARPs with a NOAA number and flux-weighted longitude within 60° of the central meridian. We fitted Poisson models with splines of log USFLUX, log TOTUSJH, R_VALUE, or all four of log USFLUX, log TOTUSJH, R_VALUE and log TOTPOT, plus a cycle term. For the class-flux test, we joined HARPs that contain exactly one NOAA region to the SRS region-day and fitted (i) the magnetic parameters against the SRS terms plus cycle (least squares) and (ii) flare counts against SRS terms, HMI terms, or both, plus cycle. For the full disk, we summed USFLUX of all HARPs within 60° of the central meridian. Stability check: the yearly median of USFLUX/AREA_ACR for large central HARPs is 1.25-1.81 x 10^19 Mx per micro-hemisphere in all years, with no step at 2019-2020 (`hmi_stability_mean_field.csv`).

## 4. Results

### 4.1 Rates by class (Figure 1)

At the same modified Zurich class, the C25/C24 rate ratio is 2.4 for classes B and C, 1.8 for D, 1.6 for E and 1.17 for F. By magnetic class, the C25/C24 rate ratio is 1.28 (alpha), 2.29 (beta), 1.28 (beta-gamma) and 1.13 (delta). C25 has more delta region-days (732 against 475). Thus the excess is largest in regions of intermediate size and complexity. Full tables for each McIntosh class and cycle, on the true and legacy scales, are in `files/results/mcintosh_rates_by_cycle.csv`.

### 4.2 Productivity and composition

Table 1. Cycle 25 / Cycle 24 ratio of M1+ flare rates (95% block-bootstrap interval).

| Quantity | Ratio |
| --- | --- |
| Full disk, per SWPC sunspot number | 1.45 (1.14-1.82) |
| Full disk, M flares from SRS regions only, per sunspot number | 1.44 (1.09-1.84) |
| Composition per sunspot number (C24-productivity expectation) | 0.96 (0.82-1.11) |
| Composition per sunspot area | 0.94 (0.86-1.04) |
| Region productivity, O/E at matched McIntosh x magnetic class, true scale | 1.61 (1.32-1.99) |
| Same, operational list | 2.44 (1.97-3.02) |
| Same, legacy (x0.7) scale on both cycles | 1.55 (1.18-2.03) |
| Same, Poisson regression with area spline (point estimate) | 1.58 |
| Full disk, per F10.7 | 0.93 (0.72-1.15) |
| Composition per F10.7 | 0.70 (0.61-0.78) |

Per sunspot, the composition ratio is close to 1. Thus the full-disk excess per sunspot (1.45) agrees with the productivity excess per region (1.61), and not with a change in the class mix. Per F10.7, the composition ratio is 0.70: Cycle 25 has fewer (or less flare-prone) sunspot groups per F10.7 unit. The product of the composition ratio (0.70) and the productivity ratio (1.61) is 1.13, which agrees with the observed 0.93 (0.72-1.15) within the intervals. Thus the "no excess per F10.7" result of the prior study is the product of two effects that cancel: fewer or smaller spot groups per F10.7 and more flares per spot group.

Sensitivity (`sensitivity_oe.csv`): strata of McIntosh class only 1.75; Zurich class only 1.63; Zurich x area bin x magnetic class 1.44 (1.19-1.81); C24 restricted to its first 83 months 1.60; regions within 60° of the central meridian 1.63; without the 5 or 10 most M-productive regions of each cycle 1.68 and 1.74; northern hemisphere 1.80; southern hemisphere 1.43 (1.12-1.81).

The C23/C24 ratio is 1.15 (0.94-1.39) at matched class, but C23 attribution is about 15% lower. Thus C23 regions were probably at least as productive per class as C25 regions. Figure 2 shows annual O/E values. Some C23 years (2000, 2001, 2005) have values of 1.4-1.5, similar to C25 years (1.29-2.03). Most C24 years have values of 0.8-1.2. Thus Cycle 24 can be the cycle with low productivity per class, and Cycle 25 can be a return to the C23 level. The data cannot separate these two descriptions. Figure 2 also shows that the operational-list ratio steps up at the December 2019 scale change.

### 4.3 HMI magnetic parameters (Figures 3, 4)

Table 2. Cycle 25 / Cycle 24 ratios from HMI SHARP (2010-05 to 2026-10).

| Model | True scale | Operational |
| --- | --- | --- |
| Matched USFLUX | 1.20 (0.88-1.58) | 1.83 (1.37-2.41) |
| Matched TOTUSJH | 1.13 (0.91-1.41) | 1.73 (1.45-2.14) |
| Matched R_VALUE | 1.13 (0.91-1.40) | 1.72 (1.44-2.13) |
| Four parameters | 1.22 (1.05-1.46) | 1.87 (1.58-2.24) |
| C1+ flares, four parameters | 1.11 (1.01-1.26) | |

Figure 3 shows that at the largest fluxes (log USFLUX ≥ 22.5) the rates of the two cycles agree within about 10%. The C25 excess is in HARPs with log USFLUX 21.6-22.1 (rate ratio 1.7-2.6). C25 also has more HARP-days with large flux (485 against 172 HARP-days with log USFLUX ≥ 22.75), which is a composition effect in magnetic terms.

Class-flux test (`class_flux_tests.csv`, 10,005 region-days with one NOAA region per HARP): at matched SRS class and area, C25 regions have 1.05 (0.99-1.11) times the USFLUX, 1.06 (1.01-1.11) times the TOTUSJH and +0.14 dex (0.08-0.22) R_VALUE. In this subsample, the M-flare ratio is 1.28 (0.88-2.19) with SRS terms, 1.19 (0.89-1.61) with HMI terms and 1.04 (lower bound 0.85; the upper bound is unstable because of sparse strata) with both. The operational ratio with both sets of terms is 1.56 (1.16-2.56).

Full disk (`fulldisk_flux_normalisation.csv`): per unit SHARP flux, the M rate ratio is 1.25 (1.00-1.51) on the true scale and 1.91 (1.55-2.38) on the operational list. SHARP flux per sunspot number is 1.16 (1.09-1.25) times higher in C25, and per sunspot area 1.19 (1.10-1.31). F10.7 per unit SHARP flux is 1.07 (1.05-1.09) times higher.

## 5. Interpretation

Three steps explain the Cycle 25 flare record relative to Cycle 24:

1. The removed 0.7 factor multiplies operational M counts by about 1.5. This is an artefact.
2. On one flux scale, Cycle 25 sunspot groups of a given class produce about 1.6 times more M flares. The class mix per sunspot did not change.
3. Cycle 25 regions of a given sunspot class have more magnetic flux, more current helicity and much more flux at strong-gradient polarity-inversion lines. Cycle 25 also has about 16-19% more SHARP flux per sunspot number or area. With HMI magnetic parameters, the region excess falls to 1.1-1.2.

Thus a sunspot count or a McIntosh class is a weaker proxy of flare-relevant magnetic flux in Cycle 25 than in Cycle 24. R_VALUE and TOTUSJH are known to be among the best single flare predictors. Their increase at fixed sunspot class agrees with the higher productivity. The higher F10.7 per sunspot (prior study) and per unit SHARP flux (7%, this study) agree with more plage and strong-field area per counted spot.

Consequences:

- Class-based (McIntosh or Mount Wilson) flare rates trained on 1988-2019 operational classes under-predict Cycle 25 operational M-flare rates by about 2.4 (1.5 from the flux scale and 1.6 from productivity). Rates on one scale still under-predict by about 1.6. Models with HMI magnetic parameters are more stable across cycles (residual 1.1-1.2).
- Claims that Cycle 25 regions are "more flare-productive" are true per sunspot class, but most of this is a difference of magnetic content per class, not a new flare mechanism.
- The large flares (M5+ and X1+) show a smaller and not significant excess (1.16-1.24). Thus the effect is mainly in moderate flares.

## 6. Limitations

- Two complete cycles (C23, C24) and one incomplete cycle (C25, to November 2026). Each model has one constant cycle factor.
- SRS classes come from ground observatories and SWPC forecasters. The classification practice can change with time, and we cannot test it independently. HMI tests reduce this problem only for 2010-2026.
- The flare-to-region attribution uses the SWPC region field. 15-17% of M flares in C24-C25 and 27% in C23 are not in the SRS of the same day (for example, flares at the east limb before numbering). C23 results have a known low bias.
- The HMI-SRS subsample is small (780 M flares) and excludes HARPs with more than one NOAA region. Its intervals are wide, and the model with both SRS and HMI terms has an unstable upper bound.
- We checked HMI stability only with internal tests (mean field of large central HARPs by year; SHARP flux per SRS spot area). An HMI calibration drift of a few per cent cannot be excluded. The flare rate increases approximately as USFLUX^1.8, so a 5% flux drift changes the flux-matched ratio by about 10%.
- The Poisson model treats region-days as independent given covariates; the block bootstrap accounts for 27-day dependence but not for longer persistence.
- Flare outcomes are on the UT day of the SRS/SHARP record (0-24 h after 00 UT), not a forecast window in the strict sense.

## 7. Reproduction

```
bash files/code/00_fetch_data.sh <work> <campaign_dir>   # SWPC, JSOC and prior-bundle files into <work> (scratch)
export OMP_NUM_THREADS=1
python -I files/code/01_parse_regions.py <work> <work>/prior
python -I files/code/02_region_days.py <work>
for p in prod:true_M prod:ops_M prod:true_X; do python -I files/code/03_region_models.py <work> <work>/prior 300 $p & done
for p in tables decomp:ssn decomp:area decomp:f107; do python -I files/code/03_region_models.py <work> <work>/prior 200 $p & done; wait
python -I files/code/04_parse_sharp.py <work>
for p in prod:USFLUX prod:TOTUSJH prod:R_VALUE prod:multi fulldisk; do python -I files/code/05_sharp_models.py <work> <work>/prior 200 $p & done
python -I files/code/06_sensitivity.py <work> 300 &
python -I files/code/08_class_flux.py <work> 200 & wait
python -I files/code/07_merge_figures.py <work> <work>/figs
```

The bundled derived tables in `files/data/` let a reader rerun steps 03-08 without the downloads: copy them to `<work>/derived/` and copy the two prior-bundle files to `<work>/prior/files/data/`. The F10.7 column is not bundled; the `decomp:f107` part needs `dsd_daily.csv` from step 01. Software: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, statsmodels 0.15.0, patsy 1.0.3, scipy 1.18.1, matplotlib 3.11.2. Random seeds are fixed (per part, from the CRC32 of the part name).

## 8. Files

- `files/code/`: all scripts (00-08).
- `files/data/region_days.csv.gz`: 45,202 SRS region-days (1998-06 to 2026-11) with McIntosh and magnetic class, area, location and flare counts on three scales.
- `files/data/events_region.csv.gz`: SWPC XRA events with region number and operational, true and legacy peak flux.
- `files/data/sharp_days.csv.gz`: 55,406 daily SHARP keyword records (00 TAI) with attributed flare counts.
- `files/data/daily_expected.csv.gz`, `files/data/daily_sharp_flux.csv.gz`: daily full-disk counts, C24-expected counts, SWPC sunspot number and area, and SHARP flux sums.
- `files/data/input_sha256.txt`: SHA-256 of all input files.
- `files/results/`: all result tables (`region_productivity_ratios.csv`, `sensitivity_oe.csv`, `decomposition_matched_activity.csv`, `sharp_productivity_ratios.csv`, `class_flux_tests.csv`, `fulldisk_flux_normalisation.csv`, `mcintosh_rates_by_cycle.csv`, `annual_oe.csv`, `sharp_rate_by_flux_bin.csv`, `hmi_stability_mean_field.csv`; `parts/` holds the per-part outputs).
- `files/figures/`: Figures 1-4.
- `files/NOTICE.md`: sources and terms of external data.

## 9. Provenance

This work was done by an automated research agent (model claude-opus-5-5, Claude Opus 5.5) in SCI campaign 11_07_2026, job sci-1107-dell-astronomy-402532db2a24, topic astronomy, machine dell, account claude-olen, on 2026-11-10. The signing key is a campaign-machine key. It is not a personal claim of authorship. This work extends sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3 (homogeneous GOES flare list) and relates to sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf (629-day clock test with the same scale correction). Data: NOAA SWPC; SDO/HMI (NASA) via JSOC, Stanford University. F10.7: National Research Council Canada, through SWPC.
