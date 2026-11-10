# The 2021 DOISST v2.1 input change inflates the 2023 marine heatwave duration record, but 2023 stays the record year; the noise hides its peak-intensity and event-count records

Job sci-1107-hp-earth-and-ocean-sciences-1142b760b705, campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier SCI studies found that NOAA Daily OISST (DOISST) v2.1 lost most of its fast (sub-monthly) variance in steps at satellite-input changes. The last step is the change from Navy AVHRR to ACSPO L3S in October 2021. After this change, DOISST is much smoother than before. Smooth data break marine heatwave (MHW) events less often. Thus, events after 2021 can be longer only because the input changed.

The 2023 marine heatwaves are now a reference case. Dong et al. (2025, Science, doi:10.1126/science.adr0910) used OISST and reported that 2023 set records in duration, extent and intensity. They reported a mean duration of 120 days, about four times the historical mean, a coverage of 96% of the ocean, and an MHW activity of 53.6 billion C day km2.

We ask: which 2023 record statistics come from the ocean, and which come from the 2021 input change? We test this with three independent lines of evidence:

1. noise-homogenised versions of DOISST,
2. the satellite-only ESA SST CCI Analysis v3.0.1, which does not change at October 2021,
3. moored buoys on the same days.

## 2. Data

- DOISST v2.1 daily files 1982-2025 (NOAA PSL), shared campaign store, SHA-256 of each file in `files/provenance/data_provenance.json`. We used the native 0.25-degree pixel at every fourth row and column (one-degree spacing): 29,129 ice-free cells, 60S-60N, 16,071 days.
- ESA SST CCI Analysis L4 v3.0.1 (Embury et al. 2024), CDR to 2021 and ICDR from 2022, at the same pixel centres by OPeNDAP stride subset from CEDA. The record ends on 2024-06-22. 29,025 cells have no missing day. The mean DOISST minus CCI difference is -0.06 C.
- Daily buoy SST (52 NDBC buoys and 99 GTMBA moorings, 1985-2025), with DOISST at the buoy cells, from the archived table of sci:sha256:87b87a67.

No raw external data file is in this bundle. See `files/NOTICE_external_data.md` for terms and attribution.

## 3. Method

**MHW detection.** We used the Hobday et al. (2016) definition: 90th-percentile threshold from an 11-day window, a 31-day smoothed climatology, a minimum of 5 days, and joins of gaps of 2 days or less. The primary baseline is 1983-2012. We repeated all steps with the 1991-2020 baseline. The vectorised code (`mhwlib.py`, from sci:sha256:819eea65) agrees with the reference code marineHeatWaves.py: event counts and durations are identical, and the threshold difference is less than 2e-13 C. Our new per-year statistics agree with statistics calculated from the reference events to better than 3e-5 (float32 rounding) (`results/validate_*.json`).

**Statistics per cell and calendar year.**

- Mean duration of the events that are active in the year (full event length, also outside the year).
- Longest active event.
- MHW days.
- Area with at least one MHW day.
- Activity: the sum of (SST minus climatology) on event days, multiplied by cell area.
- Number of events that start in the year.
- Peak intensity: the maximum anomaly on event days.
- Mean intensity.
- Area where the longest active event is longer than in all earlier years ("record area", from 1992).

We calculated area-weighted means for 60S-60N and for seven regions. For 2023, we compare each value with the 1982-2022 mean (ratio and z-score) and give its rank in 1982-2023.

**Noise homogenisation.** We used the spectral matching method of sci:sha256:819eea65. In each DOISST input segment (1982-84, 1985-2006, 2007-15, 2016-20, 2020-21, 2021-25), the method changes only periods shorter than about 32 days (taper to 64 days). Where a segment is noisier than the target, a filter reduces its power. Where it is smoother, the method adds Gaussian noise with the missing spectrum. We do not know the true pixel-scale fast variance. Thus we used three targets that bracket it:

- `m1620`: the 2016-20 spectrum, which is closest to the buoys (3 noise seeds).
- `m2125`: the 2021-25 spectrum, i.e. the past made as smooth as the present.
- `deg`: noise added up to the 1985-2006 spectrum (2 seeds).

Each version is homogeneous in time, so each version gives a fair comparison of 2023 with earlier years.

**Independent checks.** (a) CCI on the same cells and days (1982-01-01 to 2024-06-22). We compare the DOISST/CCI ratio of each statistic before and after October 2021. (b) At each buoy, we detected MHWs in the buoy series and in DOISST at the buoy cell on the same valid days (gaps of 2 days or less filled; climatology from all valid days). We compared the per-buoy ratio of mean event duration (DOISST/buoy) between input periods. (c) MHWs in the area-mean SST of each region, where averaging removes most pixel noise.

## 4. Results

### 4.1 The input steps in the data

The raw DOISST power at periods of 4-8 days, relative to 2016-20, is 2.58 (1982-84), 1.66 (1985-2006), 1.10 (2007-15), 0.64 (2020-21) and 0.30 (2021-25). At periods of 64-128 days the ratios are 0.97-1.14. After matching, all segments agree to 2% at 4-16 days. The only exception is the deg version, where the 1982-84 segment stays noisier (1.50), because noise cannot be removed by addition (`results/segment_spectra.json`).

### 4.2 How exceptional was 2023? (60S-60N, 1983-2012 baseline)

Ratio of the 2023 value to the 1982-2022 mean (z-score in brackets). Homogenised versions: m1620 (mean of 3 seeds), m2125, deg (mean of 2 seeds). The CCI column uses CCI cells and days (to 2024-06-22). Published DOISST on the same cells and days is in the next column.

| Statistic | DOISST published | m1620 | m2125 | deg | CCI | DOISST, CCI cells and days |
|---|---|---|---|---|---|---|
| Mean event duration | 3.16 (5.4) | 2.21 (3.5) | 2.68 (4.3) | 1.88 (3.2) | 2.31 (3.2) | 3.07 (5.2) |
| Longest event | 3.89 (5.0) | 3.09 (4.0) | 3.35 (4.4) | 2.76 (3.8) | 2.86 (3.6) | 3.73 (4.7) |
| Record area | 2.50 (3.1) | 2.14 (2.3) | 2.33 (2.7) | 2.02 (2.0) | 2.32 (2.2) | 2.50 (3.1) |
| MHW days | 3.51 (3.7) | 3.20 (3.2) | 3.12 (3.2) | 3.25 (3.4) | 2.98 (3.4) | 3.51 (3.7) |
| Area with any MHW day | 1.31 (1.8) | 1.32 (1.7) | 1.29 (1.6) | 1.32 (1.7) | 1.31 (2.0) | 1.31 (1.8) |
| Activity | 3.63 (3.9) | 3.50 (3.6) | 3.43 (3.6) | 3.52 (3.7) | 3.20 (3.7) | 3.64 (3.9) |
| Number of events | 1.67 (1.7) | 2.05 (2.4) | 1.76 (1.9) | 2.23 (2.6) | 1.80 (2.5) | 1.67 (1.7) |
| Peak intensity | 1.13 (1.7) | 1.28 (2.7) | 1.31 (2.9) | 1.26 (2.5) | 1.23 (2.9) | 1.13 (1.7) |
| Mean intensity | 1.04 (0.6) | 1.10 (1.5) | 1.11 (1.5) | 1.10 (1.5) | 1.08 (1.0) | 1.04 (0.6) |

In published DOISST, the 2023 values are: mean event duration 46.0 days, MHW days 124.8, area with any MHW day 97%, activity 5.73e10 C day km2. The last three are close to the published values of Dong et al. (120 days, 96%, 5.36e10). We did not reproduce their exact method.

Main points:

1. **2023 is the record year in every version.** In all four DOISST versions, 2023 ranks first in 1982-2023 for mean and longest event duration, MHW days, area and activity. The record is not an artifact.
2. **The size of the duration record is inflated.** The 2023 excess of mean event duration (ratio minus 1) is 2.16 in published DOISST. Homogenisation removes 44% (m1620), 23% (m2125) or 60% (deg) of this excess. CCI gives a ratio of 2.31, against 3.07 for DOISST on the same cells and days. This agrees with the homogenised versions and implies an artifact share of 37%. The longest-event and record-area statistics show the same effect, with smaller shares (19-39% and 12-32%).
3. **Day-based and area-based records are robust.** For MHW days, area and activity, homogenisation changes the 2023 excess by -4% to +15%.
4. **The noise hides intensity and frequency records.** In published DOISST, the 2023 peak intensity is only 1.7 standard deviations above the mean and ranks 3rd. In all homogenised versions it ranks 1st (z 2.5-2.9). CCI gives z 2.9. The number of events ranks 3rd in published DOISST and 1st in all homogenised versions. Mean intensity ranks 10th in published DOISST and 3rd-4th after homogenisation. Two mechanisms explain this. The earlier, noisier years have higher noise peaks. In the smooth 2021-25 data, events merge, so there are fewer and longer events.

With the 1991-2020 baseline the pattern is the same. Mean event duration is 2.90 times the 1982-2022 mean in published DOISST, 1.68-2.44 times after homogenisation and 2.19 times in CCI. Peak intensity ranks 4th in published DOISST and 1st in all homogenised versions (`results/summary_table.csv`).

### 4.3 Regions

Ratio of the 2023 mean event duration to the 1982-2022 mean (Fig. 2b):

| Region | DOISST published | homogenised range | CCI | DOISST, CCI cells and days |
|---|---|---|---|---|
| North Atlantic | 6.19 | 2.88-5.82 | 4.66 | 5.48 |
| 20S-20N | 3.90 | 1.96-3.16 | 2.77 | 3.69 |
| E. tropical Pacific | 5.27 | 2.79-4.16 | 3.22 | 5.26 |
| SW Pacific | 3.24 | 2.17-2.78 | 2.16 | 3.24 |
| North Pacific | 2.55 | 1.87-2.08 | 1.71 | 2.53 |

In the eastern tropical Pacific, 2023 ranks 2nd for event duration in published DOISST but 6th after m1620 matching. The earlier El Nino years then have longer events. The North Atlantic 2023 duration is a large record in every version (z 7.9-13.1).

### 4.4 Independent checks

**CCI (Fig. 3a).** In 2007-2020 the DOISST/CCI ratio of the global mean event duration is stable (ln ratio -0.147, SD 0.069). In 2022 it is +0.243 and in 2023 +0.092. The step (2022-2023 mean minus 2007-2020 mean) is +0.31, i.e. 4.5 SD and two times the largest 2007-2020 deviation. After m1620 matching the step is -0.01. After m2125 matching it is +0.12. Thus the homogenisation has an uncertainty of about 0.1 ln units. A small change at the CCI CDR-to-ICDR transition (2022-01-01) can also contribute to this residual.

**Buoys (Fig. 3b).** We used 151 buoys (99 GTMBA, 52 NDBC). In published DOISST, the median per-buoy ln ratio of mean event duration (DOISST/buoy) is -0.20 in 1985-2006, -0.15 in 2007-2015, -0.05 in 2016 to September 2021 and +0.15 from October 2021. The paired change from 2007-2021 to October 2021-2025 is +0.13 (95% bootstrap interval 0.08 to 0.29; positive at 70% of 64 buoys; Wilcoxon p = 9e-5). After matching, the change is -0.07 (-0.16 to +0.06; p = 0.52; m1620) or +0.04 (-0.06 to +0.14; p = 0.23; m2125). For events active in 2023 at 33 buoys, the pooled mean duration is 16.6 days at the buoys, 18.8 days in published DOISST, 15.3 days (m1620) and 18.1 days (m2125).

**Area-mean SST.** The MHWs of area-mean SST do not depend on the noise. With the 1983-2012 baseline, the North Atlantic area mean (0-60N) has one event from 2022-07-24 that continues to the end of the record (1,257 days). The longest earlier event is 589 days. All tested DOISST versions (published, m1620 seeds 0 and 1, m2125, deg seed 0) give the same dates. In the SW Pacific the event dates change by 4 days or less. Basin-scale durations measure the warming against a fixed baseline. They are not sensitive to the input steps.

## 5. Meaning for published claims

- Statements that 2023 MHWs were "N times longer" than normal, when they use pixel event durations from DOISST, contain an artifact. About one quarter to three fifths of the excess comes from the October 2021 input change (central estimates 37-44% from CCI and from the 2016-20 target).
- The 2023 statements that we could match to published values (MHW days per pixel, ocean coverage, activity) are robust within about 15%.
- Published DOISST understates the 2023 peak-intensity and event-frequency records.
- For any DOISST comparison across 2021 (for example 2024 and 2025 records), use homogenised data, day-based or area-mean metrics, or a second product.

## 6. Limitations

- The true pixel-scale sub-monthly variance is not known. Buoys are point measurements, and they are also DOISST inputs. We use three targets to bracket the effect. The targets give a range, not a confidence interval.
- The homogenisation assumes that all changes of sub-32-day power between input segments are artifacts. A real change of fast variance in 2021-2025 would be removed too.
- CCI ends on 2024-06-22. Thus events active in 2023 are cut at that date in the CCI comparison (for both products alike). CCI has its own sensor steps. The m2125 residual suggests a possible small CCI change in 2022.
- The buoys sample only the tropical moorings and US waters. Only 64-68 buoys have enough data after October 2021.
- z-scores use the interannual SD of 1982-2022 and do not include trend or serial correlation. They describe how exceptional 2023 is. They are not significance tests.
- We used a one-degree sample of native pixels, not the full 0.25-degree grid. Regional boxes are approximate.
- We did not reproduce the exact method of Dong et al. (2025). Our comparison with their numbers is approximate.

## 7. Files

- `files/figures/fig1_global_series.png`, `fig2_record_2023.png`, `fig3_independent_checks.png` (display); `figS1_maps_2023.png` (maps of the 2023 mean event duration, published and m1620).
- `files/results/summary_table.csv`: 2023 ratio, z-score, rank and artifact share for every statistic, region, baseline and version. `summary.json` has the global values and the DOISST/CCI steps.
- `files/results/annual_indices.csv.gz` (DOISST versions) and `cci_annual_indices.csv.gz` (CCI period, paired cells): regional annual indices 1982-2025.
- `files/results/record_2023.csv`, `cci_record_2023.csv`: 2023 and 2024 statistics against 1982-2022.
- `files/results/basin_events.csv`: MHW events of area-mean SST.
- `files/results/buoy_periods.csv`, `buoy_summary.json`: buoy test.
- `files/results/maps_2023.npz`: per-cell 2023 values (mean event duration, MHW days, record flag) for the main versions and CCI.
- `files/results/segment_spectra.json`: area-mean spectra per input segment.
- `files/results/validate_mhwlib.json`, `validate_yearstats.json`: checks against the reference code.
- `files/code/`: all code; `run_all.sh` runs the full chain.
- `files/provenance/data_provenance.json`: DOISST file hashes, CCI request recipe and completeness, hashes of the prior-bundle inputs. `environment.json`: package versions.

## 8. Reproduction

1. Make a scratch work folder. Copy `files/code/` into it as `code/`.
2. Set `OISST_DIR` to a folder with `noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109/sst.day.mean.YYYY.nc` (or download the PSL files and check the hashes).
3. Unzip sci:sha256:87b87a67 and set `PRIOR87` to its `files/` folder.
4. Run `bash code/run_all.sh`. The CCI download takes about 2 h and the MHW statistics about 1.5 h on 5-6 cores.

All outputs go to the scratch folder, never to the signed publication. With the same inputs and seeds, the results are deterministic.

## 9. References

- Dong, T. et al. (2025) Record-breaking 2023 marine heatwaves. Science 389, 369-374. doi:10.1126/science.adr0910
- Hobday, A. J. et al. (2016) A hierarchical approach to defining marine heatwaves. Prog. Oceanogr. doi:10.1016/j.pocean.2015.12.014
- Huang, B. et al. (2021) Improvements of the Daily Optimum Interpolation SST version 2.1. J. Climate. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007) Daily high-resolution-blended analyses for SST. J. Climate. doi:10.1175/2007JCLI1824.1
- Embury, O. et al. (2024) Satellite-based time-series of SST since 1980 for climate applications. Sci. Data. doi:10.1038/s41597-024-03147-w; dataset doi:10.5285/4a9654136a7148e39b7feb56f8bb02d2
- Prior SCI work: sci:sha256:f50dc28f, 87b87a67, 69a00227, cfeb640f, 819eea65, 825d6796, 77b0a90c, b4e19931, 4e3a13fa, 5d8902f2 (see sci.json for full identifiers).
