# WPC Excessive Rainfall Outlooks for 2021-2026 matched their rain-above-flash-flood-guidance probabilities at 5 km scale, but flood reports were 1.4-2.5 times fewer, and flash flood guidance changed the meaning of the definition by region

Job sci-1107-dell-earth-and-ocean-sciences-56c590da2ed4, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell,
account claude-myxtap, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a
personal authorship claim.

## Summary

The NOAA Weather Prediction Center (WPC) Excessive Rainfall Outlook (ERO) gives the probability that rainfall exceeds
flash flood guidance (FFG) within 40 km (25 mi) of a point. The categories are Marginal (at least 5%), Slight (at least
15%), Moderate (at least 40%) and High (at least 70%). In August 2026, the NWS proposed a fifth category, Enhanced (25%)
(PNS 26-57). The previous campaign work did not test this product. We tested it against three truths and against a
union of the three:

- T1: MRMS radar-gauge rainfall above FFG. This is the stated definition of the product.
- T2: MRMS rainfall above the 5-year average recurrence interval (ARI). This truth does not use FFG.
- T3: NWS flash flood Local Storm Reports (LSRs). These need a human observer.
- T4: the union of T1, T2 and T3. This is a public analogue of the WPC Unified Flood Verification System, without
  USGS stream gauges.

We wrote and hashed the plan before we compared any forecast with any outcome (files/plan/PLAN.md, SHA-256
586ffc49ce02f277586ab6bbefc9fc760f410e0bdc76ae9c178e72cab1357ec5, 2026-11-11T18:47:48Z).

Data: 2,093 Day 1 outlooks (0830 UTC issuance, 2021-01-01 to 2026-10-31), a 20 km grid with 19,270 CONUS points, and
40.3 million point-days. The 95% intervals come from a day-block bootstrap.

Main results:

1. **Against its own definition, the ERO was calibrated.** At a 5 km (0.05 degree) scale, the T1 event frequency
   was in the stated range in all five classes (Figure 1). The values were: no area 0.42% (below 5%), Marginal 8.0%
   (7.7-8.2%), Slight 22.3% (21.6-23.1%), Moderate 50.1% (45.7-54.3%) and High 79.4% (67.2-89.1%, 34 days).
   Days 2-5 were also in range for Marginal and Slight (Figure 5).
2. **The calibration verdict depends on the spatial scale of "rain exceeds FFG".** If any 1 km pixel above FFG
   counts, Marginal is 20.2% and Slight is 40.3%, which is above both ranges. If the ratio must be 150% or more,
   Marginal is 3.1% and Slight is 11.4%, which is below both ranges. An exploratory check of 20 warm-season days
   showed that our 3-hourly sampling found 74% of the T1 events that hourly sampling found. With hourly sampling,
   Marginal (11.3%) and Slight (28.1%) stayed in range, but they moved up.
3. **Against flash flood reports, the ERO over-forecast.** T3 frequencies were Marginal 2.0%, Slight 8.4% and
   Moderate 27.6%. These are 2.5, 1.8 and 1.45 times below the lower bounds of the ranges. Only High (63.5%) was in
   range. NCEI Storm Events gave the same result. Reports captured 4.5% of T1 events in the least populated quintile
   and 29.9% in the most populated quintile. The logistic slope was 0.88 (0.83-0.92) per tenfold population.
4. **The union truth T4 was in range in all classes:** Marginal 13.8%, Slight 30.0%, Moderate 58.2% and High 90.3%.
   Against the ARI truth T2, Moderate (26.3%) and High (46.2%) were below the ranges.
5. **FFG changes the meaning of the definition by region.** Inside ERO areas, the ratio of T1 events to T2 events
   (5-year ARI) changed 7.6-fold between River Forecast Centers (RFCs): 0.28 in CNRFC and 2.09 in LMRFC (Figure 2c).
   In the West, rain is above the 5-year ARI much more often than it is above FFG. In the lower Mississippi and the
   Southeast, the opposite is true.
6. **RFC boundaries (pre-registered H3, supported).** Grid points within 50 km of a shared RFC boundary gave a mean
   jump in T1 frequency of 0.299 (|ln ratio|), against 0.191 for T2. The difference was 0.107 (0.070-0.132). The ERO
   itself jumped only 0.053. In an exploratory placebo, we compared each jump with the jump over the same distance
   inside one RFC. With this placebo, the excess at RFC boundaries was 0.070 (0.036-0.095) for T1, 0.024 (0.003-0.049)
   for T2 and -0.001 for the ERO. For ln(T1/T2), the boundary excess was 0.047 (0.023-0.076). Thus part of the T1
   jump is a step at RFC boundaries, but most of the regional difference is a broad west-east gradient. The largest
   steps were at the CNRFC/NWRFC boundary (ln(T1/T2) step 1.05, against 0.39 inside the RFCs) and at the MARFC/OHRFC
   boundary (0.74 against 0.12).
7. **Enhanced tier (secondary S1).** Slight points within 40 km of a Moderate area had a T1 frequency of 34.1%
   (31.5-36.8%). Slight points farther away had 21.8% (21.0-22.5%). By the pre-registered rule, the current Slight
   class thus contains a level of 25% or more that the forecasters already mark. But these points were only 4.5% of
   Slight point-days. Points 40 km or more inside the Slight edge (24.8%, 23.8-25.7%) did not meet the rule.
8. **Between-RFC spread (pre-registered H4, not supported).** The SD of ln(observed/expected) over RFCs was 0.33
   for T1 and 0.38 for T2. Thus the T1 regional calibration was not more variable than the T2 regional calibration.
   The two truths had different regional patterns (Figure 4).

Conclusion: the ERO is calibrated against the quantity in its definition, at the scale that WPC uses for verification.
The product is not calibrated against flood reports, which miss most rain-above-FFG events outside cities. The
definition itself is not uniform. Each RFC computes FFG with its own method, and the same category corresponds to
different rainfall rarity in different regions. The forecasts do not show these steps, but the verification truth
does.

## Background

Erickson et al. (2021, doi:10.1175/WAF-D-20-0020.1) verified the ERO for 2015-2019 against Stage IV rainfall above FFG
and against the full UFVS. They found the ERO reliable against FFG exceedances, with fractional coverage at or above
the upper end of the old ranges (5-10%, 10-20%, 20-50%, above 50%) for the full UFVS. WPC then changed the ranges to
5/15/40/70% (ERO Product Description Document, April 2023). Clark et al. (2014, doi:10.1175/WAF-D-12-00124.1)
showed that the skill of FFG against flood reports changes between RFCs. We know of no independent verification of
the redefined ERO. We know of no test of whether FFG differences between RFCs change the meaning of ERO verification.
This work continues the campaign series on operational hazard products. In that series, sparse observations
(sci:sha256:844f22ed..., PTWC tsunami gauges) and report density (sci:sha256:afeada0c..., SPC hail reports) caused
apparent miscalibration. The CRW attribution study (sci:sha256:1ab16218...) traced an error to the product rules.

## Data

All inputs are US Government works or public archives of them (files/EXTERNAL_DATA_NOTICE.md). Raw files are not
bundled. files/results/input_hashes.csv and files/results/mrms_input_files.csv.gz give the SHA-256 of every input file
(25,783 MRMS files and 24 other files).

- ERO polygons, Days 1-5, cake layers, from the Iowa Environmental Mesonet (IEM) archive (type E), downloaded
  2026-11-11. Primary: Day 1 outlooks of IEM cycle 8 (0830 UTC initial issuance), valid 12 UTC to 12 UTC. If a cycle
  had more than one product, we used the last one. Day 4 and Day 5 outlooks are in the archive from 2023-05-19.
- MRMS FLASH_QPE_FFGMAX (the maximum over 1, 3 and 6 h of the ratio of MRMS QPE to the RFC FFG mosaic, in percent) from
  NOAA Open Data on AWS. We used 8 samples per day, at 15, 18, 21, 00, 03, 06, 09 and 12 UTC.
- MRMS FLASH_QPE_ARIMAX (the maximum ARI over 30 min to 24 h, in years), 4 samples per day at 18, 00, 06 and 12 UTC.
- IEM Local Storm Reports of type FLASH FLOOD (36,679 reports in 2021-2026, all areas). Sensitivity: FLASH FLOOD plus
  FLOOD, and NCEI Storm Events flash floods (24,601 events, to 2026-07-31).
- 2020 Census tract population centres; NWS RFC boundaries rf05mr24.

Days excluded: 37 dates with no cycle-8 product or with incomplete MRMS samples (listed by
files/code/analyze.py from files/derived/*.npz).

## Methods

- Grid: 20 km EPSG:5070 grid. We kept 19,270 points where at least 90% of the 0.05-degree MRMS blocks within 40 km had
  valid FFG. This removes some coastal and border points.
- Forecast at a point: the highest category whose polygon contains the point.
- T1: at least one 0.05-degree block (5 by 5 MRMS pixels, about 5 km, near the 4 km Stage IV scale of WPC
  verification) whose block-mean ratio reached 100% at a sample time, with block centre within 40 km.
- T2: the same with block-mean ARI of 5 years or more. T3: at least one flash flood LSR within 40 km in the 12-12 UTC
  window.
- Frequencies are pooled over point-days in each category. We also give the event-averaged coverage that WPC uses
  (mean over days). It gave similar values: 7.8%, 21.5%, 47.8% and 67.8% for T1 (MRGL to HIGH); the High value is
  just below 70%, and we did not compute an interval for it (files/results/H1_H2_reliability_primary.csv).
- Boundary test: 22 pairs of adjacent RFCs with at least 200 km of shared boundary. Side bands are 0-50 km from the
  other RFC. D = mean of |ln(fA/fB)| weighted by the number of boundary points.
- Uncertainty: 500 day-block bootstrap draws (200 for the population slope, 300 for E3).
- Code: files/code. Daily MRMS processing (mrms_daily.py, with a minimal PNG-GRIB2 decoder grib2png.py), grid and
  forecasts (build_inputs.py), neighbourhood events (build_truth.py), pre-registered statistics (analyze.py),
  exploratory statistics (explore.py, cadence_check.py), figures (figures.py).

## Pre-registered results

| Test | Planned criterion | Result | Verdict |
| --- | --- | --- | --- |
| H1 T1 by category, Day 1 | interval overlaps range | none 0.42%, MRGL 8.0%, SLGT 22.3%, MDT 50.1%, HIGH 79.4% | In range, all five |
| H2 T3 reports | expected below T1 | MRGL 2.0%, SLGT 8.4%, MDT 27.6%, HIGH 63.5% | Supported; below ranges for MRGL-MDT |
| H2 T4 union | expected above T1 | MRGL 13.8%, SLGT 30.0%, MDT 58.2%, HIGH 90.3% | Supported; in range |
| H2 T2 ARI 5 yr | (no direction) | MRGL 10.2%, SLGT 17.7%, MDT 26.3%, HIGH 46.2% | MDT and HIGH below range |
| H3 boundary D(T1) - D(T2) | > 0, CI excludes 0 | 0.107 (0.070-0.132) | Supported |
| H4 SD ln R over RFCs, T1 vs T2 | T1 larger | 0.333 (0.306-0.363) vs 0.382 (0.360-0.407) | Not supported |
| S1 Enhanced tier | one subgroup >= 25%, other < 25% | near MDT 34.1%, far 21.8%; inner 24.8%, edge 18.4% | Met for MDT proximity only |
| S2 Days 2-5 | ranges | MRGL 8.8-9.3%, SLGT 20.4-22.5% (T1) | In range |
| S3 report capture slope | (estimate) | 0.88 (0.83-0.92) per tenfold population | Strong population effect |

Sensitivity runs for H1 (files/results/H1_sensitivity.csv):

| Truth or subset | MRGL | SLGT | MDT |
| --- | --- | --- | --- |
| T1 primary (block mean >= 100%) | 8.0% | 22.3% | 50.1% |
| T1 >= 1 pixel at 1 km | 20.2% (above) | 40.3% (above) | 65.6% |
| T1 >= 5 pixels | 15.5% (above) | 34.0% | 60.4% |
| T1 >= 25 pixels | 9.7% | 25.6% | 53.2% |
| T1 ratio >= 75% | 15.7% (above) | 36.0% | 63.1% |
| T1 ratio >= 150% | 3.1% (below) | 11.4% (below) | 35.5% (below) |
| T2 ARI 2 yr / 10 yr | 17.4% / 6.2% | 28.7% / 11.2% | 40.6% / 17.7% |
| T3 with FLOOD reports | 3.0% | 11.2% | 34.0% |
| T3 NCEI Storm Events | 1.7% | 7.0% | 23.7% |
| T1 warm season (May-Sep) | 8.2% | 22.1% | 46.9% |
| T1 by year 2021-2026 | 6.6-10.6% | 20.6-26.2% | 38.4-62.9% |
| T1, Day 1 1600 UTC update | 7.6% | 22.1% | 51.3% |

The T1 verdict was in range in each year and for the 1600 UTC update.

## Exploratory results (decided after the primary results)

- E1 placebo for H3: files/results/E1_placebo_summary.csv. The difference-in-differences (T1 excess minus T2 excess)
  was 0.046 (0.003-0.075).
- E2 FFG-to-ARI event ratio inside ERO areas by RFC: files/results/E2_rfc_ffg_ari.csv. CNRFC 0.28, CBRFC 0.44, MARFC
  0.74, NWRFC 0.77, NERFC 0.78, WGRFC 0.83, NCRFC 1.06, MBRFC 1.07, ABRFC 1.16, SERFC 1.29, OHRFC 1.51, LMRFC 2.09.
- E3 jump of ln(T1/T2) across versus within RFCs: 0.252 against 0.206; excess 0.047 (0.023-0.076). The excess was
  0.048 with 2-year ARI and 0.046 with 10-year ARI.
- E4 sampling cadence: on 20 random warm-season days, 3-hourly samples found 74.5% of the hourly T1 events. No
  3-hourly event was missing from the hourly set. Point-day frequencies with hourly samples: none 1.4%, MRGL 11.3%,
  SLGT 28.1%, MDT 44.6% (558 point-days). Thus the primary T1 frequencies are lower bounds. A shift of about 1.3 times
  keeps all classes in range.

## Deviations from the plan

- The population slope uses log10(pop40 + 100), because some grid points have no population within 40 km.
- In the H3 table we also give T1, T2 and T3 at fixed ERO category (MRGL or above) and four extra truth pairs.
- E1-E4 were not planned. We label them exploratory.

## Limitations

- MRMS FLASH ratios are not the Stage IV-based FFG exceedances that WPC uses. MRMS QPE has its own regional biases.
  The 5 km block mean is our approximation of the WPC verification scale. The verdict depends on this scale (main
  result 2).
- Our MRMS samples are 3-hourly (FFG) and 6-hourly (ARI). They miss some short exceedances (E4). The 6-hour ratio at
  15 UTC includes 3 hours of the previous day.
- The ARI truth uses the ARI grids inside MRMS FLASH. These come from NOAA Atlas 14 where it exists and from other
  sources elsewhere. Thus T2 also has regional method steps. We did not use USGS stream gauges, so T4 is not the
  full UFVS.
- RFC boundaries often follow drainage divides and mountain ridges, where climate can change. The placebo reduces
  this problem but does not remove it.
- LSR and Storm Events locations are approximate. Report density depends on population (main result 3).
- The ERO archive is a third-party parse (IEM) of NWS products. The High class has only 34 Day 1 dates.

## Reproduction

1. `bash files/code/fetch_data.sh SCRATCH` (writes all inputs into SCRATCH, not into this folder).
2. `python files/code/mrms_daily.py FFGMAX 2021-01-01 2026-10-31 SCRATCH/mrms/FFGMAX 3` and
   `python files/code/mrms_daily.py ARIMAX 2021-01-01 2026-10-31 SCRATCH/mrms/ARIMAX 6` (streams about 25,800 files
   from NOAA AWS; about 10 CPU hours).
3. `python files/code/build_inputs.py SCRATCH SCRATCH/mrms/FFGMAX/20210101.npz SCRATCH/inputs`
4. `python files/code/build_truth.py SCRATCH/inputs SCRATCH/mrms/FFGMAX FFGMAX SCRATCH/truth_ffg.npz` and the same
   for ARIMAX.
5. `python files/code/analyze.py SCRATCH/inputs SCRATCH/truth_ffg.npz SCRATCH/truth_ari.npz SCRATCH/gis/rf05mr24.zip OUT`,
   then explore.py with the same arguments, and figures.py.

Steps 1-4 can be skipped: files/derived holds the grid (grid.npz, nbmatrix.npz), the forecast categories
(ero_d*_c*.npz), the report events (reports.npz) and the T1/T2 event grids (truth_ffg.npz, truth_ari.npz, bit-packed
per date). With these files and the RFC shapefile, analyze.py and explore.py reproduce all tables. Python 3.12 with
numpy, scipy, pandas, geopandas, shapely 2, pyproj, statsmodels, matplotlib and Pillow.

## Files

- files/plan: pre-registered plan and its hash.
- files/results: all tables (H = pre-registered primary, S = secondary, E = exploratory), meta.json, input hashes.
- files/figures: fig1_reliability, fig2_maps, fig3_boundary, fig4_rfc_calibration, fig5_lead_time.
- files/derived: grid-level derived data (see Reproduction).
- files/code: all code.
- files/EXTERNAL_DATA_NOTICE.md: sources, versions and terms of the external data.

## References

- Erickson, M. J., B. Albright, and J. A. Nelson, 2021: Verifying and redefining the Weather Prediction Center's
  Excessive Rainfall Outlook forecast product. Wea. Forecasting, 36, 325-340, doi:10.1175/WAF-D-20-0020.1.
- Erickson, M. J., et al., 2019: Verification results from the 2017 HMT-WPC Flash Flood and Intense Rainfall
  Experiment. J. Appl. Meteor. Climatol., doi:10.1175/JAMC-D-19-0097.1.
- Clark, R. A., J. J. Gourley, Z. L. Flamig, Y. Hong, and E. Clark, 2014: CONUS-wide evaluation of National Weather
  Service flash flood guidance products. Wea. Forecasting, 29, 377-392, doi:10.1175/WAF-D-12-00124.1.
- NWS, 2023: Excessive Rainfall Outlook Product Description Document (April 2023).
- NWS, 2026: Public Information Statement 26-57, proposed changes to the ERO (5 August 2026).
