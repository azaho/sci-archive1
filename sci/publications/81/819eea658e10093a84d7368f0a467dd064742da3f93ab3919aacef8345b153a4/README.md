# Noise steps cause 30-55% of the 1982-2025 marine heatwave duration rise in OISST v2.1, hide a peak-intensity rise and reverse the cold-spell duration trend at 60S-60N; heatwave-day trends are robust

## Summary

NOAA daily OISST v2.1 (DOISST) is the standard data set for marine heatwave (MHW) and marine cold spell (MCS) statistics. Earlier campaign studies showed that the fast (day-to-day) variance of OISST changes in steps at satellite input changes, and that these steps cause most of the reported rise in daily SST memory (sci:sha256:f50dc28f, sci:sha256:87b87a67, sci:sha256:69a00227). We asked: which standard MHW and MCS statistics does this artifact change, by how much, and what trend remains after the artifact is removed?

We did these steps:

1. We measured the anomaly power spectrum of OISST in six input segments, for 29,129 ice-free native 0.25-degree pixels (one pixel per 1-degree box, 60S-60N, 1982-2025). We compared OISST with 173 moored buoys (NDBC and GTMBA) on the same 128-day windows.
2. We made a noise-homogenised version of OISST with two methods. Each method changes only periods shorter than about 32 days (taper to zero at 64 days), so the seasonal cycle, interannual change and the warming trend stay the same.
   - **match**: in each segment, we filter (where the segment has more power) or add Gaussian noise (where it has less power) so that the spectrum agrees with the 2016-01-01 to 2020-07-06 segment. This segment agrees best with the buoys.
   - **add-noise**: we only add noise, so that every segment has the spectrum of the 1985-2006 (Pathfinder AVHRR) segment. This method does not remove any data, but it makes all years as noisy as the noisiest long segment.
3. We calculated the standard Hobday et al. (2016) statistics (fixed 1983-2012 baseline, 90th/10th percentile thresholds, 5-day minimum, 2-day gap join) on the published and on the homogenised data. Our vectorised code agrees with the reference code (ecjoliver/marineHeatWaves) to better than 2e-11 on synthetic data.
4. We tested the methods on synthetic data where the truth is known, and on 127 long-record buoys on matched days.

## Main results

All trends are 1982-2025 OLS trends per decade of area-weighted 60S-60N means. The intervals are 95% moving-block bootstrap ranges (3-year blocks). "Effect" is the trend of (published minus match); its interval comes from the same bootstrap. The three noise realisations differ by less than 0.003 in every trend in this table.

| Statistic (per decade) | Published OISST | Homogenised: match | Homogenised: add-noise | Effect (published minus match) |
|---|---|---|---|---|
| MHW frequency (events/yr) | +0.66 (0.54 to 0.77) | +0.85 (0.73 to 0.97) | +0.97 | -0.20 (-0.26 to -0.13) |
| MHW mean duration (days) | +4.45 (2.83 to 6.14) | +3.12 (1.95 to 4.29) | +1.99 | +1.33 (0.56 to 2.09) |
| MHW days per year | +21.0 (15.3 to 26.8) | +21.8 (16.3 to 27.3) | +18.5 | -0.8 (-1.6 to -0.1) |
| MHW area fraction | +0.058 | +0.060 | +0.051 | -0.002 |
| MHW mean intensity (C) | -0.007 (-0.016 to 0.002) | +0.016 (0.006 to 0.025) | +0.016 | -0.022 (-0.028 to -0.016) |
| MHW max intensity (C) | +0.006 (-0.010 to 0.022) | +0.053 (0.034 to 0.072) | +0.057 | -0.047 (-0.060 to -0.034) |
| MHW cumulative intensity (C days/yr) | +30.0 | +31.1 | +28.8 | -1.0 (-1.6 to -0.5) |
| MCS frequency (events/yr) | -0.73 | -0.64 | -0.68 | -0.08 (-0.11 to -0.06) |
| MCS mean duration (days) | +0.75 (0.24 to 1.25) | -0.28 (-0.68 to 0.14) | -0.17 | +1.03 (0.75 to 1.30) |
| MCS days per year | -7.7 | -8.8 | -7.7 | +1.1 (0.9 to 1.3) |
| MCS max intensity (C) | +0.004 (-0.021 to 0.029) | -0.046 (-0.066 to -0.026) | -0.031 | +0.049 (0.037 to 0.062) |
| Annual maximum of SST minus climatology (C) | +0.108 (0.073 to 0.144) | +0.207 (0.175 to 0.240) | +0.187 | -0.099 (-0.117 to -0.080) |
| Annual minimum of SST minus climatology (C) | +0.291 (0.244 to 0.338) | +0.184 (0.153 to 0.215) | +0.213 | +0.107 (0.084 to 0.129) |
| tau10 memory (days), control | +2.33 (1.63 to 3.01) | +0.34 (-0.12 to 0.81) | +0.30 | +1.99 (1.38 to 2.57) |
| MHW duration on detrended SST (days) | +1.80 (0.92 to 2.69) | +0.62 (-0.18 to 1.44) | +0.42 | +1.17 (0.72 to 1.61) |
| MHW frequency on detrended SST | -0.22 (-0.34 to -0.09) | -0.06 (-0.18 to 0.06) | -0.07 | -0.16 (-0.19 to -0.12) |

**R1. The artifact is at periods shorter than about one month.** Relative to the 2016-2020 segment, the median OISST pixel had 1.75-1.85 times the power at 4-8 day periods in 1985-2006, and 0.22-0.32 times the power in 2021-2025 (Figure 1a). The segments agree within about 15% at periods of 64 days and more. On the same windows at the buoys, OISST had 2.0-2.7 times the buoy power at 3-8 days in 1985-2006, 1.0-1.1 times in 2016-2020 and 0.19-0.51 times in 2021-2025. At 32-128 days the ratio was 0.9-1.1 in all main segments (Figure 1b). Thus OISST was noisier than the buoys before 2007 and smoother than the buoys after October 2021.

**R2. Heatwave and cold-spell durations and counts are affected; heatwave days are not.** The published OISST gives a MHW duration trend that is 1.33 days per decade (30%) larger than the match result, and 2.46 days per decade (55%) larger than the add-noise result. The duration effect is positive in 86% of the ocean area (Figure 5). The published MHW frequency trend is 23% smaller than the match result (frequency effect negative in 89% of the area). Thus the artifact joins heatwaves into fewer and longer events. For cold spells, the published OISST gives a rise of mean duration (+0.75 days per decade); after homogenisation the trend is -0.28 (match) or -0.17 (add-noise), and both intervals include zero. The trends of MHW days, MHW area fraction and MHW cumulative intensity change by less than 5% (match) or 12% (add-noise). The MCS-day decrease becomes 14% larger (match) or does not change (add-noise). This agrees with the bounds in sci:sha256:825d6796, which certify the sign of the heatwave-day trend.

**R3. The artifact hides a rise in heatwave peak intensity.** Noisy early years give high peaks above the threshold; smooth late years give low peaks. Thus the published OISST gives no trend in MHW maximum intensity (+0.006 C per decade). After homogenisation, the trend is +0.053 (match) or +0.057 (add-noise) C per decade. In the tropics (20S-20N), the published trend is negative (-0.044, -0.066 to -0.021) and the match trend is positive (+0.025, 0.002 to 0.048). The trend of the annual maximum anomaly is approximately doubled (+0.108 to +0.207 C per decade), and the trend of the annual minimum anomaly falls by about one third (+0.291 to +0.184). Thus the published OISST makes the warm extremes warm too slowly and the cold extremes warm too fast. The same signs occur in all three regions (tropics, 20N-60N, 20S-60S; `trend_table.csv`).

**R4. A synthetic test shows that the homogenisation gives the correct trends.** We made 400 synthetic cells with a known truth (seasonal cycle, 0.15 C per decade warming, slow and fast AR(1) parts). We added OISST-like errors that change at the same dates (white plus red noise that decreases in steps, and a 7-day running mean in the last segment) (Figure 6). With no real change of memory, the match method gave MHW duration +1.34 days per decade against +1.40 for the homogeneous target (truth plus constant 2016-2020 error). The inhomogeneous record gave +2.04. For MHW frequency: 0.92 against 0.95 (inhomogeneous 0.87); max intensity: 0.035 against 0.038 (inhomogeneous -0.046); MCS duration: -0.66 against -0.66 (inhomogeneous -0.07); tau10: -0.16 against -0.02 (inhomogeneous +1.00). The add-noise method recovered its own (noisier) target equally well, but this target has smaller duration and day trends than the truth (duration 1.09 against 1.55). Thus the add-noise trends are low estimates, and we use the match method as the main estimate. In a second scenario with a real memory increase (slow decay time 15 to 25 days), the MHW statistics were again correct within 10%. But both methods kept only about one third of the real tau10 trend (0.30 against 0.82). Thus a homogenised tau10 trend is a lower bound, while the MHW statistics are not strongly biased by this effect.

**R5. The buoys agree with the homogenised OISST for duration, peak intensity and memory.** At 127 buoys (52 NDBC, 75 GTMBA; at least 10 station-years over at least 15 years), with the same days and the same rules for both sources (climatology from all matched years; events end at data gaps), the per-buoy median trends were (Figure 4):

| Per-buoy median trend (per decade) | Buoy | Published OISST | Match | Add-noise | Published minus buoy (median, 95% CI; Wilcoxon p) | Match minus buoy |
|---|---|---|---|---|---|---|
| MHW mean duration (days) | +1.45 | +2.11 | +1.56 | +0.93 | +0.49 (0.06 to 1.13; p = 0.29) | -0.16 (-0.64 to 0.58; p = 0.60) |
| MHW max intensity (C) | +0.008 | -0.037 | +0.028 | +0.039 | -0.055 (-0.077 to -0.031; p = 6e-5) | +0.013 (-0.013 to 0.035; p = 0.22) |
| tau10 (days) | +0.25 | +1.39 | -0.20 | -0.43 | +1.14 (0.77 to 1.79; p = 5e-9) | -0.50 (-0.80 to 0.00; p = 0.009) |
| MCS frequency (events/yr) | -0.42 | -0.61 | -0.58 | -0.55 | -0.18 (-0.24 to -0.05; p = 8e-5) | -0.10 (-0.16 to 0.02; p = 0.009) |
| MHW frequency (events/yr) | +0.54 | +0.60 | +0.64 | +0.68 | +0.07 (-0.06 to 0.12; p = 0.23) | +0.08 (0.01 to 0.16; p = 0.02) |
| MHW days per year | +11.2 | +12.1 | +12.8 | +11.1 | +1.1 (0.4 to 2.3; p = 4e-4) | +1.3 (0.2 to 2.1; p = 0.003) |

The homogenisation removes the clear biases of the published OISST in peak intensity and memory (lag-1 autocorrelation: published minus buoy +0.017 per decade, p = 3e-22; match minus buoy -0.002). For duration, the per-buoy scatter is large, and the paired test is not significant. The medians agree with R2. The MHW-day difference stays after homogenisation. It is related to a separate inhomogeneity: on matched days, OISST warms 0.034 C per decade faster than the buoys (median; GTMBA +0.043, NDBC -0.012). A robust regression of the MHW-day difference on this offset gives +0.80 +/- 0.41 days per year per decade (match) at zero offset (`buoy_mean_offset_trend.csv`). The tau10 result agrees with R4: homogenisation removes some real change, and the true tau10 trend at these buoys is small (+0.25 days per decade).

**R6. Sensitivity.** With a cutoff period of 16 or 64 days instead of 32, the match MHW duration trend was +3.30 or +3.16 days per decade (add-noise: +2.21 or +1.99). The MHW max intensity trend was +0.052 to +0.060 in all four variants, and the MCS duration trend was -0.05 to -0.27. tau10 was the most sensitive (+0.28 to +0.98).

## Interpretation

The OISST v2.1 input steps reach the standard marine heatwave statistics, not only the memory statistics. The statistics that depend on event structure (count, duration) and on the tails of daily anomalies (peak intensity, annual extremes) are biased. Statistics that mostly count exceedance days (MHW days, area fraction, cumulative intensity) are robust, because the mean warming dominates them. A study that uses published OISST with the standard method (for example Oliver et al. 2018) will get an MHW-duration trend that is 1.4 to 2.2 times the homogenised trend (30-55% of the published trend is artifact) and an MHW-frequency trend that is 23-33% too small. It will miss a global rise of MHW peak intensity of about 0.05 C per decade, and in the tropics it will report the wrong sign. It will also report a false lengthening of cold spells. After homogenisation, the real changes are: more frequent heatwaves (+0.85 events per year per decade), longer heatwaves (+3.1 days per decade, mostly from the mean warming; +0.6 days per decade and not significant on detrended SST), more intense heatwave peaks (+0.05 C per decade), a much smaller tau10 rise (+0.3 days per decade; lower bound), and fewer cold spells with no clear change in their duration.

## Limitations

- The homogenisation corrects only the second-order (spectral) properties of the fast variance. Added noise is independent of the ocean; sci:sha256:48ad9d2c showed that the OISST response to real buoy changes also changes between eras. Thus the method cannot recover lost real signal at a given day, and statistics that depend on the covariance with a second variable (for example, ecological impact studies) are not corrected.
- The method assumes that the change in sub-monthly power between segments is not real. The buoys support this assumption (studies above and Figure 1b), but they sample only the tropical moorings and US waters. Real change in intraseasonal variability between segments would be removed. Long-period (more than 64 days) inhomogeneities, such as the mean-warming offset at the buoys, are not corrected.
- The reference segment (2016-01-01 to 2020-07-06) is only 4.5 years long and contains the end of the 2015-2016 El Nino. Its sub-monthly spectrum includes natural variability of that period. The 1982-1984 segment is short, and its power estimate is noisy.
- The segment dates are partly documented (2007-01-01, 2016-01-01, 2021-10-01) and partly from change-point searches in sci:sha256:87b87a67 (1985-01-12, 2020-07-07). Smaller steps inside a segment are not corrected.
- Buoys are OISST inputs, so the buoy test is not fully independent. The per-buoy trends have much scatter, and many paired tests for duration and frequency are not significant. The buoy climatology uses all matched years, not the 1983-2012 baseline.
- Bootstrap intervals use annual global means with 3-year blocks. They do not include the uncertainty of the homogenisation method itself (R4, R6 give an estimate).
- We used one 0.25-degree pixel per 1-degree box. Box-mean data have less noise and would give smaller effects.
- Chunks 21 and 26-28 of the 30 grid chunks were calculated as four sub-chunks each (`05b_subchunks.py`) because the machine was heavily loaded. The method is the same, but these chunks use different random seeds. The noise realisations change trends by less than 0.003.

## Figures

- `files/figures/fig3_reach.png`: 1982-2025 trends of 18 statistics for published and homogenised OISST, with 95% intervals.
- `files/figures/fig1_spectral_ratios.png`: (a) median OISST power by segment relative to 2016-2020; (b) OISST power relative to buoy power on the same windows.
- `files/figures/fig4_buoy_trend_differences.png`: per-buoy trend differences, OISST minus buoy, for published and homogenised OISST.
- `files/figures/fig2_global_series.png`: annual 60S-60N means of six statistics; dotted lines show segment boundaries.
- `files/figures/fig5_trend_maps.png`: maps of MHW duration and frequency trends, published, homogenised and difference.
- `files/figures/fig6_synthetic.png`: synthetic test trends for truth, homogeneous targets, inhomogeneous data and both methods.

## Methods

**Data.** OISST v2.1 AVHRR-only daily files (`sst.day.mean.YYYY.nc`, NOAA PSL, 1982-2025) from the shared campaign datasets. We read the pixel at index (1::4, 1::4) of the 0.25-degree grid (the "pt" sample of sci:sha256:87b87a67). We kept pixels at 60S-60N with valid data on all 16,071 days and minimum SST above -1.0 C: 29,129 pixels. The buoy inputs (parsed daily NDBC and GTMBA SST, and OISST at the nearest 0.25-degree pixel for 1982-2025) come from the signed bundle sci:sha256:87b87a67. We removed days with |buoy - OISST| of 5 C or more. We kept 173 buoys with at least 900 matched days.

**Spectra.** Anomaly = SST minus a least-squares fit of a constant, a linear trend and three annual harmonics (1982-2025). For each pixel and segment: Welch periodogram, 128-day Hann windows, 50% overlap, linear detrend, then a 5-bin running mean in frequency. Segments: 1982-01-01, 1985-01-12, 2007-01-01, 2016-01-01, 2020-07-07, 2021-10-01, 2026-01-01.

**Homogenisation (`code/degrade.py`).** Taper w(f) = 1 for periods up to Pc, 0 for periods of 2 Pc and more, cosine in log frequency between them (Pc = 32 days; sensitivity 16 and 64). Add-noise: noise spectrum D = max(0, S_1985-2006 - S_seg) w, made by FFT of Gaussian white noise. Match: in each segment, gain 1 - w (1 - sqrt(min(1, S_ref/S_seg))) on the anomaly (mirror-extended, segment mean and trend removed and then restored), plus noise with spectrum max(0, S_ref - S_seg) w. Then the removed fit is added back. We checked the result: after match, the median segment ratios at 2-16 days are 0.97-1.04 (`spectra_grid.json`).

**MHW and MCS statistics (`code/mhwlib.py`).** These follow Hobday et al. (2016) and the reference code: leap-year day of year; all values within +/- 5 days of each baseline day; 90th (MHW) or 10th (MCS) percentile; Feb 29 as the mean of the neighbours; 31-day periodic running mean; events of 5 days or more; join gaps of 2 days or less. Events count in the year when they start. Per year and pixel: count, mean duration, total days, mean of event mean and max intensity, sum of cumulative intensity, fraction of days in events, and the annual maximum and minimum of SST minus climatology. For the "detrended" variants, we removed the fitted linear trend before detection. Controls: yearly lag-1 and lag-10 autocorrelation (year mean removed, pairs inside the year), tau10 = -10/ln(r10), and day-to-day variance.

**Statistics.** Area weights cos(latitude). Duration and intensity means use only pixel-years with events. OLS trends per decade, with a moving-block bootstrap of residuals (3-year blocks, 4,000 draws). Per-buoy trends are OLS over station-years with at least 300 valid days; counts and days are per 365.25 valid days. Paired tests use Wilcoxon signed-rank tests and bootstrap intervals of the median (5,000 draws).

## Reproduction

Python 3.12 with numpy 2, scipy, pandas, matplotlib and statsmodels. Make a work directory WORK with `WORK/code` (copy `files/code/` there) and a `datasets` link at `WORK/../datasets`, or set `OISST_DIR`.

```
bash code/get_inputs.sh <path to 87b87a67...zip>      # buoy inputs from the prior SCI bundle into WORK/prior
for y in $(seq 1982 2025); do python3 code/01_extract.py $y; done   # pixel sample, hashes checked
python3 code/04_build_matrix.py                         # 29,129 x 16,071 matrix
python3 code/02_buoy_load.py && python3 code/03_buoy_spectra.py
OMP_NUM_THREADS=1 python3 code/05_grid_metrics.py 12    # main grid run (about 2 CPU-hours per 1,000 pixels)
python3 code/06_buoy_mhw.py && python3 code/09_buoy_stats.py && python3 code/09b_buoy_mean_trend.py
python3 code/07_synthetic.py
python3 code/08_aggregate.py && python3 code/11_cell_trends.py && python3 code/10_figures.py
bash code/get_reference_mhw.sh /tmp/mhwref && python3 code/00_validate_mhwlib.py /tmp/mhwref/mhw_ref_np2   # optional check
```

`run_extract_all.sh` is the loop that we used to wait for shared files that were still downloading. `05b_subchunks.py` computes chosen chunks in sub-chunks (used for chunks 21 and 26-28).

## Files

- `files/code/`: all code that we used.
- `files/results/trend_table.csv`: trends, intervals and effects per statistic, region (global, tropics, north, south) and method.
- `files/results/global_series.csv`: annual regional means for all 15 versions.
- `files/results/cell_trends.csv.gz`: per-pixel 1982-2025 trends of the mapped statistics for published, add-noise and match versions.
- `files/results/buoy_mhw_station_years.csv`, `buoy_mhw_trends.csv`, `buoy_mhw_stats.json`, `buoy_mean_offset_trend.csv`, `buoy_spectra.json`: buoy test.
- `files/results/spectra_grid.json`: area-weighted and median segment spectra before and after homogenisation.
- `files/results/synthetic.json`: synthetic test series and trends.
- `files/results/validate_mhwlib.json`: comparison with the reference MHW code.
- `files/provenance/data_provenance.json`: shared dataset names, paths, source URLs, byte counts and SHA-256 of the 44 OISST files, and SHA-256 of the prior-bundle inputs.

## Data sources and terms

See `NOTICE.md`. We do not include raw OISST or raw buoy files. All OISST and buoy data are NOAA products (US Government works). The derived tables in this bundle are our own aggregates.

## Provenance

- Campaign 11_07_2026; job sci-1107-dell-earth-and-ocean-sciences-9ed40c48038a; topic earth-and-ocean-sciences; machine dell; account claude-olen.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis dates: 2026-11-09 to 2026-11-10. OISST files: shared datasets `noaa-psl-oisst-v21-highres-sst-day-mean-YYYY-20261109` (downloaded 2026-11-09 by the campaign dataset helper); all 44 SHA-256 values agree with the dataset provenance records.

## References

- Hobday, A. J. et al. (2016). A hierarchical approach to defining marine heatwaves. Progress in Oceanography 141, 227-238. doi:10.1016/j.pocean.2015.12.014
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. Journal of Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Reynolds, R. W. et al. (2007). Daily high-resolution-blended analyses for sea surface temperature. Journal of Climate 20, 5473-5496. doi:10.1175/2007JCLI1824.1
- Oliver, E. C. J. et al. (2018). Longer and more frequent marine heatwaves over the past century. Nature Communications 9, 1324. doi:10.1038/s41467-018-03732-9
- Lee, C. et al. (2025). Observed multi-decadal increase in the surface ocean's thermal inertia. Nature Climate Change 15, 308-314. doi:10.1038/s41558-025-02245-w
- Reference MHW code: https://github.com/ecjoliver/marineHeatWaves (commit d7292bf), used only for validation.
