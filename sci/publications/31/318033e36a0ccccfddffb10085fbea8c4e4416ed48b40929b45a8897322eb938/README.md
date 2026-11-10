# SWPC M-flare probabilities increased gradually in 2022-2026 at fixed region content, by about the removed GOES 0.7 factor; region climatologies trained on the legacy scale under-forecast Cycle 25 by 1.42

**Job:** sci-1107-dell-astronomy-b84f521c9704 · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), account claude-olen · **Date:** 2026-11-10.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

In December 2019, GOES-16 became the primary NOAA X-ray satellite, and NOAA stopped the 0.7 factor on the 1-8 Å flux. Two earlier campaign publications used one homogeneous (true, science-quality) flux scale for 1998-2026:

- sci:sha256:cf94434c… found that the SWPC day-1 M-class probabilities were too low in 2020-2024 (observed/forecast 1.23) and closer to calibration in 2025-2026 (0.93). It could not tell if SWPC adjusted its forecasts or if the cycle phase caused the change.
- sci:sha256:83acab80… (a sibling job) found that, on one scale, Cycle 25 regions give 1.61 times more M flares than Cycle 24 regions of the same McIntosh and magnetic class.

We used the SWPC Solar Region Summaries (46,754 region-days, 1998-2026), the SWPC event list with region numbers and the true-scale peak flux of each event. We built a fixed Poisson region climatology (McIntosh class components, Mount Wilson class, spot area), trained on Cycles 23-24. We used it for two purposes: (1) as a forecast that we verify across the scale change, and (2) as a measure of the "region content" of each day. With (2) we compared the issued SWPC probabilities at the same region content and the same recent flare activity.

Main results (95% intervals from bootstraps of 27-day blocks):

- **SWPC probabilities increased gradually at fixed region content.** Relative to the Cycle 24 relation, the logit of the SWPC day-1 M probability changed by -0.10 (2020), -0.12 (2021), +0.18 (2022), +0.37 (2023), +0.52 (2024), +0.72 (2025) and +0.76 (2026) (Figure 1). For 2025-2026 against 2020-2024 the change is +0.51 (0.41-0.61). In the complementary log-log scale this is a Poisson rate factor of 1.54 (1.41-1.69) after March 2025, with persistence controls. This is close to the removed factor (1/0.7 = 1.43).
- **We did not find a single step.** The best single step is in March 2025 (bootstrap range December 2024 to May 2025). But a local test of 8 months before and 8 months after it gives only 1.07 (0.84-1.40). Steps of the same size occur in 6% (3 of 49) of the windows of the same length in Cycles 23-24. In Cycle 23, SWPC probabilities were also high in 2000-2005 (+0.3 to +0.7) and returned to the Cycle 24 level in 2006. In Cycle 25 they continued to increase in the declining phase. Thus the data agree with a gradual adaptation by the forecasters to the larger flux scale. They do not show a dated method change, and they do not exclude other causes.
- **The SWPC increase did not follow a change in region productivity.** At matched region class, Cycle 25 regions give 1.67 (1.37-2.04) times the Cycle 24 M rate in 2020-2024 and 1.38 (1.01-1.89) in 2025-2026. The productivity did not increase when the forecasts increased.
- **X-class probabilities did not change in the same way.** The SWPC X-class rate factor after March 2025 is 1.10 (0.95-1.30).
- **Region climatologies inherit the scale step.** A McIntosh class-rate climatology trained on the 1998-2019 counts on the legacy (operational) scale under-forecasts the Cycle 25 M1+ days by 1.42 (1.34-1.51) (Figure 2). The same model trained on true-scale counts gives 1.05 (0.98-1.12). For X1+ days the values are 1.52 (1.14-1.92) and 1.01 (0.75-1.28). With outcomes and training on one scale, the calibration still changes from Cycle 24 to Cycle 25 by 1.30 (1.17-1.47). This agrees with the higher productivity per class.
- **Independent replication.** Our own code gives the same region productivity as the sibling study: 1.61 (1.28-1.97) at matched class (observed/expected, true scale), and 1.57 (1.29-1.91) from a Poisson regression (Figure 3). The composition per sunspot is 0.95 (0.81-1.14). With F10.7 added to the matched region content, the Cycle 25 excess becomes 1.23 (0.99-1.64).

Limitations: SWPC procedures are not public, so we cannot identify the cause of the change. The region-content index comes from a model, and its errors can change with the cycle phase. Two complete cycles and one incomplete cycle. 15-24% of M flares are not attributed to a region in the SRS of the same day.

## 1. Question

The removal of the 0.7 factor changed the outcome scale of all NOAA flare forecasts. The earlier work showed that the SWPC M probabilities were too low in 2020-2024 and were close to calibration in 2025-2026. We asked:

1. At the same sunspot-region content and the same recent flare activity, did the SWPC M probabilities change after 2019? If yes, when, by how much, and as a step or gradually?
2. How large is the error of a region class-rate climatology (McIntosh Poisson rates, for example Bloomfield et al. 2012) that is trained on the legacy scale and used in Cycle 25? How much error remains after training on the true scale?

A verification of SWPC forecasts for 1998-2024 (arXiv:2508.01114) did not examine the scale change. Janssens et al. (2025, SWSC 15, 14) gave McIntosh rates on the corrected scale for 1976-2019, but did not test them on Cycle 25. Pietrow (2026, arXiv:2608.04537) pooled the region rates of Cycles 23-25 without a scale correction. We did not find a public SWPC notice about a 2025 change of the flare probabilities.

## 2. Data

| Data | Source | Use | Terms |
| --- | --- | --- | --- |
| SWPC Solar Region Summary (SRS), 1996-01-02 to 2026-11-10 | `ftp://ftp.swpc.noaa.gov/pub/warehouse/YYYY/YYYY_SRS.tar.gz`, `.../2026/SRS/` | Region number, location, area, McIntosh class, spot count, Mount Wilson class | NOAA, public domain |
| SWPC edited event lists, 1998-05 to 2026-11-09 | `.../warehouse/YYYY/YYYY_events.tar.gz`, `.../2026/2026_events/` | 54,503 XRA 1-8 Å events with region number | NOAA, public domain |
| SWPC Daily Solar Data (DSD) | `.../warehouse/YYYY/YYYY_DSD.txt`, `pub/indices/old_indices/2026Q*_DSD.txt` | SESC sunspot number and area; F10.7 (only for one aggregate test) | NOAA; F10.7 from NRC Canada, not bundled |
| True-scale peak flux of each event; SWPC RSGA day-1 probabilities | sci:sha256:cf94434c…, `files/data/events_homog.csv.gz`, `files/data/daily_counts_forecasts_noaa.csv.gz` | All 54,503 events joined; RSGA M and X probabilities | Derived from NOAA public-domain data |

The SHA-256 of each of the 721 input files is in `files/data/input_sha256.txt`. `files/NOTICE.md` gives the sources and terms.

## 3. Methods

**Region-days (`01_parse_regions.py`, `02_region_table.py`).** We read section I of each SRS. The SRS issued at 0030 UT on day D gives the regions at 2400 UT of day D-1. The outcome of a region-day is the number of XRA events that SWPC attributed to that region (own line, or another line of the same event group) with peak on UT day D. We counted on the operational scale and on the true scale (legacy = true × 0.7). Cycles: C23 1998-06-01 to 2008-11-30, C24 2008-12-01 to 2019-11-30, C25 2019-12-01 to 2026-11-08 (20,109, 12,128 and 12,967 region-days). The share of true-scale M1+ flares that are attributed to a region in the same-day SRS is 0.76 (C23), 0.83 (C24) and 0.85 (C25) (`files/data/attribution_by_cycle.csv`).

**Region climatology (`04_forecast.py`).** Model A: the M1+ (or X1+) rate of each full McIntosh class in the C23-C24 region-days (classes with fewer than 50 region-days pooled to Zurich class and penumbra, then to Zurich class). Model B: a Poisson regression with McIntosh components (Z, p, c), Mount Wilson class (alpha, beta, beta-gamma, any delta) and a 4-df spline of log spot area. Each model was trained twice: with legacy-scale counts (the pre-2020 operational classes) and with true-scale counts. The full-disk probability for day D is 1 - exp(-Σλ) over the regions. We verified it against outcomes on the operational, true and legacy scales with the observed/forecast ratio, the Brier skill score against the sample climatology and reliability tables.

**SWPC at fixed region content (`06_swpc_adjustment.py`, `06b_swpc_robustness.py`).** The SWPC day-1 M probability for day D (RSGA issued 2200 UT on day D-1) is compared with the model-B probability from the same regions (legacy-scale training). The model: logit(p_SWPC) = spline(logit p_region) + prior-day M flare + period (or year) term, by least squares. The period term is the shift of the SWPC probability at the same region content. Robustness: a complementary log-log response (the shift is then the log of a Poisson rate factor), more persistence terms (log number of M flares on D-1, on D-3 to D-1 and on D-27 to D-1), a local window around the best step, a placebo search for the largest single step in Cycles 23-24, and the same test for X-class probabilities. Intervals: 27-day block bootstrap (1,000 or 500 replicates).

**Replication of region productivity (`03_productivity.py`, `03b_disk_f107.py`).** Poisson regressions of region-day counts on cycle and nested sets of region descriptors, with intervals from region-clustered standard errors; a decomposition of the full-disk excess per sunspot number into composition (expected count from the C24 model) and productivity (observed/expected), with a 27-day block bootstrap (150 replicates); and full-disk daily models with the C24-expected count and a spline of log F10.7.

## 4. Results

### 4.1 SWPC probabilities at fixed region content (Figure 1)

Table 1. Shift of logit(SWPC day-1 M probability) against Cycle 24, at matched region content and prior-day M flare (`files/results/swpc_shift_by_period.csv`).

| Period | Days | Shift | 95% CI | Probability at the C24 median 0.20 |
| --- | --- | --- | --- | --- |
| C23 (2000-10 to 2008-11) | 2,978 | +0.23 | 0.14 to 0.32 | 0.24 |
| C25, 2019-12 to 2024-12 | 1,849 | +0.12 | 0.04 to 0.20 | 0.22 |
| C25, 2025-01 to 2026-11 | 669 | +0.63 | 0.53 to 0.75 | 0.32 |
| 2025-26 against 2020-24 | | +0.51 | 0.41 to 0.61 | |

With the true-scale-trained index, the shifts are +0.24, +0.12 and +0.60. The yearly shifts are in `swpc_shift_by_year.csv`. They increase each year from 2021 to 2026 (Figure 1a).

Table 2. The change in March 2025, within Cycle 25 (`files/results/swpc_robustness.csv`).

| Test | Shift | 95% CI | As a rate factor |
| --- | --- | --- | --- |
| logit, prior-day M | +0.48 | 0.35 to 0.62 | |
| cloglog, prior-day M | +0.44 | 0.33 to 0.55 | 1.55 (1.38-1.74) |
| cloglog, all persistence terms | +0.43 | 0.34 to 0.53 | 1.54 (1.41-1.69) |
| cloglog, local window 2024-07 to 2025-11 | +0.07 | -0.18 to 0.34 | 1.07 (0.84-1.40) |
| X class, cloglog | +0.10 | -0.05 to 0.26 | 1.10 (0.95-1.30) |

The single-step search on the monthly residuals gives March 2025 (+0.55; 98% of bootstrap replicates within 3 months). But the local window test does not show a step, and the largest single step in Cycle 25 (0.46) is equalled or exceeded in 3 of 49 windows of the same length in Cycles 23-24 (`swpc_placebo_steps.csv`). Thus the change is gradual, or it is a step that the noise hides.

Table 3. Calibration on operational outcomes (`files/results/swpc_vs_climatology_skill.csv`).

| Period | SWPC obs/fc | SWPC BSS | Climatology (true-scale training) obs/fc | BSS | Climatology (legacy-scale training) obs/fc | BSS |
| --- | --- | --- | --- | --- | --- | --- |
| C23 | 0.79 | 0.31 | 0.70 | 0.23 | 0.95 | 0.30 |
| C24 | 0.79 | 0.23 | 0.62 | 0.14 | 0.87 | 0.23 |
| C25, 2020-24 | 1.23 | 0.41 | 1.08 | 0.40 | 1.46 | 0.34 |
| C25, 2025-26 | 0.93 | 0.10 | 0.95 | 0.10 | 1.32 | 0.08 |

In Cycles 23-24, SWPC behaved like a legacy-scale climatology that is about 10% too high. In 2025-2026, the SWPC calibration is the same as that of the true-scale climatology. All forecasts have low skill in 2025-2026.

### 4.2 Region climatology across the scale change (Figure 2)

Table 4. McIntosh class-rate climatology (model A), day-1 full disk, Cycle 25 (`files/results/forecast_verification.csv`).

| Class | Training scale | Outcome | Obs/fc | 95% CI | BSS |
| --- | --- | --- | --- | --- | --- |
| M1+ | legacy | operational | 1.42 | 1.34-1.51 | 0.24 |
| M1+ | true | operational | 1.05 | 0.98-1.12 | 0.29 |
| M1+ | legacy | legacy | 1.11 | 1.02-1.21 | 0.25 |
| X1+ | legacy | operational | 1.52 | 1.14-1.92 | 0.04 |
| X1+ | true | operational | 1.01 | 0.75-1.28 | 0.04 |

Model B gives the same values within 0.02 for M1+ (1.41 and 1.04). In the training cycles the true-scale climatology is 0.96 (C23) and 0.81 (C24) on true outcomes: Cycle 24 was less productive per class than the pooled training data. The calibration change from C24 to C25 is 1.71 (1.50-1.93) with legacy training and operational outcomes, and 1.30 (1.17-1.47) with training and outcomes on the true scale (`forecast_calibration_change.csv`).

### 4.3 Replication of region productivity (Figure 3)

Table 5. Cycle 25/Cycle 24 rate ratio per region-day at matched McIntosh (Z, p, c), Mount Wilson class and area (`files/results/glm_cycle_ratios.csv`, `glm_sensitivity.csv`).

| Outcome | Ratio | 95% CI |
| --- | --- | --- |
| M1+, operational list | 2.40 | 1.94-2.95 |
| M1+, true scale | 1.57 | 1.29-1.91 |
| M5+, true scale | 1.27 | 0.94-1.73 |
| X1+, true scale | 1.21 | 0.78-1.87 |
| M1+, regions within 60° of central meridian | 1.57 | 1.25-1.97 |
| M1+, C24 limited to its first 83 months | 1.55 | 1.27-1.88 |
| M1+, C25 2020-2024 only | 1.67 | 1.37-2.04 |
| M1+, C25 2025-2026 only | 1.38 | 1.01-1.89 |

The C23/C24 ratio is 1.09 (0.92-1.31). The decomposition (`decomposition.csv`) gives a productivity of 1.61 (1.28-1.97) and a composition per sunspot number of 1.05 (0.87-1.23), or 0.95 (0.81-1.14) stratified by sunspot number. These values agree with sci:sha256:83acab80… (1.61 and 0.96), which used different code.

Full-disk daily models (`disk_f107_models.csv`): with the C24-expected count alone, the C25/C24 ratio is 1.58 (1.30-2.00). With the expected count and a spline of log F10.7, it is 1.23 (0.99-1.64). With F10.7 alone it is 0.91 (0.70-1.29). F10.7 per region also increased: the monthly regression gives 140 sfu at 6 regions in C25, against 131-134 sfu in C23-C24 (`f107_per_region_descriptor.csv`). Thus F10.7 carries part of the flare-relevant information that the sunspot classes do not show.

## 5. Interpretation

From 2020 to 2021, SWPC issued M probabilities with the same relation to region content as in Cycle 24. Because the outcomes after December 2019 are on the larger true scale, these forecasts were too low. From 2022 to 2026, the SWPC probabilities at the same region content increased each year. By 2025-2026 the increase was a rate factor of about 1.5, the size of the removed factor. The SWPC calibration then became the same as that of a climatology trained on true-scale counts. The region productivity did not increase at the same time. Thus the increase agrees with a gradual correction for the flux scale, for example by forecasters who see more M flares than they expect. It does not agree with a forecast that follows a change in the regions. The data cannot show whether it was an intended change.

Users of class-based flare climatologies must train and verify them on one flux scale. A climatology with pre-2020 operational counts gives Cycle 25 M and X probabilities that are about 1.4-1.5 times too low. On the true scale, the remaining cycle-to-cycle change (about 1.3 at the day level, 1.6 at the region-day level for Cycle 25 against Cycle 24) is real for sunspot classes, and F10.7 explains part of it.

## 6. Limitations

- SWPC does not publish its procedure. We cannot identify a cause. Other causes of the increase are possible, for example new tools, staff changes or the high flare rate of 2024.
- The region-content index is a model. If its errors change with the cycle phase or with region types, the SWPC shift includes them. Cycle 23 shows that shifts of +0.2 to +0.7 also occur without a scale change.
- The step tests have little power: monthly residuals are noisy, and the local window has only 482 days.
- SRS classes are subjective. A change of the classification practice changes the index. We did not test this.
- 15-24% of M flares are not in the same-day SRS. The region models do not predict these flares; the full-disk outcomes include them.
- The bootstrap uses 27-day blocks. Longer dependence can make the intervals too narrow.
- Cycle 25 is incomplete (data to 2026-11-08).

## 7. Reproduction

```
bash files/code/run_all.sh <work_dir> <campaign_dir>
```

`run_all.sh` extracts two files from sci:sha256:cf94434c…, downloads the SWPC files into `<work_dir>/raw/swpc` with `00_fetch_data.sh` (scratch, never the bundle), and runs steps 01-06 and the figures. Without the downloads, a reader can rerun steps 03-06 from the bundled tables: copy `files/data/region_days.csv.gz`, `disk_days.csv.gz` and `disk_forecasts.csv.gz` to `<work_dir>/derived/` (step 03b also needs `dsd_daily.csv` from step 01, because F10.7 is not bundled). Software: Python 3.12, numpy, pandas 3, statsmodels, patsy, matplotlib. Random seeds are fixed. The 2026 SWPC directories grow; compare names and hashes with `files/data/input_sha256.txt`.

## 8. Files

- `files/code/`: all scripts (00-06, `run_all.sh`).
- `files/data/region_days.csv.gz`: 46,754 SRS region-days with class, area, location and flare counts on each scale.
- `files/data/disk_days.csv.gz`: daily full-disk counts (all and region-attributed), region sums, SWPC sunspot number and area.
- `files/data/disk_forecasts.csv.gz`: daily climatology probabilities (models A and B, legacy and true training) and outcomes.
- `files/data/attribution_by_cycle.csv`, `files/data/input_sha256.txt`.
- `files/results/`: all result tables named in Section 4.
- `files/figures/`: Figures 1-5 (Figure 4: decomposition; Figure 5: class mix and rates).
- `files/NOTICE.md`: external data sources and terms.

## References

- sci:sha256:cf94434cc907d929fe2342675f1f0b92b966e8804019441c0241614b7d55cbb3 (homogeneous GOES flare list and SWPC verification).
- sci:sha256:83acab80e0c80464dd153756dd3de2e1cdbfcbfe1e623c93da6908704d294d9e (Cycle 25 region productivity with HMI).
- sci:sha256:d8fe105441f4a8deb0890611a7a4970adb89bee39e6907d41713aa800780c4cf (629-day clock test with the same scale correction).
- Janssens J. et al. 2025, Space Weather Space Clim. 15, 14, doi:10.1051/swsc/2025007.
- Bloomfield D.S. et al. 2012, ApJL 747, L41, doi:10.1088/2041-8205/747/2/L41.
- Verification of the NOAA SWPC solar flare forecast (1998-2024), arXiv:2508.01114.
- Pietrow A.G.M. 2026, arXiv:2608.04537.
