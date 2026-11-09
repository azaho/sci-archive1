# Observed sea-surface temperature memory did not decrease detectably between 1982-2003 and 2004-2025 in three SST products, and it did not follow GODAS mixed-layer changes

**Job:** sci-1107-dell-earth-and-ocean-sciences-58160fbd8f65 · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) · **Campaign:** 11_07_2026 · **Date:** 2026-11-08

The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

"Ocean memory" is the persistence of sea-surface temperature (SST) anomalies. Shi et al. (2022, *Science Advances*, doi:10.1126/sciadv.abm3468) used CMIP6 models to project a global decrease of this memory in the 21st century. They measured memory as A1, the lag-1-year autocorrelation of annual-mean SST anomalies. In their models, the main cause is a shallower mixed layer (about 70% of the increase in damping rate). Their projected A1 trend for 50S-50N in 2000-2100 is -0.10 to -0.13 per century. They did not test whether the decrease is already present in observations.

We asked three questions:

1. Did observed SST memory decrease between 1982-2003 (W1) and 2004-2025 (W2)?
2. Is any change larger than the change that occurs between two 22-year windows before 1982?
3. Do the grid cells where the mixed layer became shallower show a larger increase in damping rate? A simple stochastic slab model (dT/dt = -lambda T + noise, lambda proportional to 1/h) predicts a slope of -1 between the change in ln(lambda) and the change in ln(h) if the air-sea feedback does not change.

We wrote the analysis plan (`files/PLAN.md`) before we calculated any persistence statistic. Section 6 identifies the analyses that we added after we saw the results.

## 2. Data

| Data | Version and source | Use | SHA-256 of file used |
| --- | --- | --- | --- |
| NOAA OISST v2.1, monthly, 0.25 deg | PSL `noaa.oisst.v2.highres/sst.mon.mean.nc` (modified 2026-11-02) | Primary SST, 1982-2025 | f30eaf685fe59e6267599b11b85a4bd5fa5ce86c768a475747aa2fb69f35f61a |
| NOAA ERSSTv5, monthly, 2 deg | PSL `noaa.ersst.v5/sst.mnmean.nc` (data_modified 2026-11-03) | Replication; long record 1880-2025 | 952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386 |
| Met Office HadISST1, monthly, 1 deg | `metoffice.gov.uk/hadobs/hadisst/data/HadISST_sst.nc.gz` (modified 2026-11-02) | Replication; long record 1870-2025 | eb0a402520ec4a9f0089a0c5471d7a04e4fc83dbdcb5e2d624de9fcd60670d45 |
| NCEP GODAS mixed-layer depth `dbss_obml`, monthly | PSL `godas/dbss_obml.YYYY.nc`, 1980-2025 | Mixed-layer depth h | 46 hashes in `files/data/godas_dbss_obml_sha256.txt` |

The three SST files are in the shared campaign store as `noaa-psl-oisst-v21-sst-mon-mean-20261108`, `noaa-psl-ersst-v5-sst-mnmean-20261108` and `metoffice-hadisst1-sst-20261108` (provenance records in `files/data/shared_dataset_provenance.txt`). The bundle includes the gridded OISST SST and GODAS mixed-layer depth that the analysis reads (`files/data/grid_oisst.npz`, sha256 41b5e216...2129; `files/data/grid_godas_mld.npz`, sha256 958d5dd5...1146). With these two files, you can repeat the OISST and mixed-layer parts without a download.

## 3. Method

- **Grid.** We put all products on one 2 x 2 degree grid (box means; ERSSTv5 is interpolated linearly to the box centres), 60S-60N. We kept the 7,291 boxes that have complete records in all three products in 1982-2025 and no month colder than -1.0 C (to remove sea ice).
- **Anomalies (primary).** For each box, we removed 12 calendar-month means and a quadratic time trend fitted over 1982-2025 (ordinary least squares). Sensitivity tests: a cubic trend; a linear trend in each window; regression on the 10-year low-passed area-mean SST; and the quadratic method with a lagged (0-6 month) Nino 3.4 regression also removed.
- **Metrics in each 22-year window (264 months).**
  - r1: lag-1-month autocorrelation of monthly anomalies.
  - phi = (area mean of r2) / (area mean of r1). If the anomaly is an AR(1) process plus white noise (for example, observation error), r1 and r2 both include the same noise factor, so phi does not depend on the white noise. We added phi before we computed the OISST results, after ERSST showed a rise in r1 (Section 6).
  - A1: lag-1-year autocorrelation of 22 annual means (the metric of Shi et al.).
  - lambda = -ln(r1), the monthly damping rate.
- **Primary statistic.** The area-weighted mean change (W2 minus W1) over the 7,291 boxes.
- **Uncertainty.** (a) Moving-block bootstrap in time, with the full map resampled together (24-month blocks for r1 and phi, 4-year blocks of annual means for A1, 1,000 replicates; only within-block pairs enter the autocorrelation). (b) A reference distribution: the same statistic for 59 pairs of adjacent 22-year windows that start in 1880-1938 and end before 1982, in ERSSTv5 and HadISST1. These pairs overlap, so they are not independent. They include changes in the observing system before 1982.
- **Detection rule (from the plan).** A decrease is "detected" only if the bootstrap 95% interval excludes zero, the value is outside the central 95% of the reference pairs, and all three products have the same sign.
- **Mixed-layer test.** Across boxes, we regressed the change in ln(lambda) on the change in ln(h), with h the GODAS annual-mean or winter-maximum mixed-layer depth. We used cos(latitude) weights and a spatial block bootstrap (20 x 40 degree blocks, 51 blocks). We also regressed ln(lambda) on ln(h) across boxes in W1 (cross-sectional test of the same model).

## 4. Results

### 4.1 Global change in SST memory (Figure 2)

| Product | Change in r1 [bootstrap 95%] | Change in phi [bootstrap 95%] | Change in A1 [bootstrap 95%] |
| --- | --- | --- | --- |
| OISST v2.1 | +0.032 [+0.000, +0.068] | -0.003 [-0.036, +0.038] | -0.031 [-0.109, +0.069] |
| ERSSTv5 | +0.025 [+0.001, +0.055] | +0.005 [-0.024, +0.047] | -0.023 [-0.111, +0.077] |
| HadISST1 | -0.063 [-0.094, -0.022] | -0.033 [-0.066, +0.007] | +0.012 [-0.104, +0.096] |
| Pre-1982 pairs, SD (ERSST / HadISST) | 0.020 / 0.065 | 0.029 / 0.026 | 0.063 / 0.072 |

W1 values for OISST: r1 0.652, phi 0.680, A1 0.166.

- **Annual memory (A1).** OISST and ERSST show small decreases (-0.031, -0.023). HadISST shows a small increase (+0.012). All bootstrap intervals include zero. All values are inside the pre-1982 range. Thus, by the planned rule, we did not detect a decrease. The OISST and ERSST values are near the forced change that the projected trend gives over 22 years (-0.022 to -0.029). But the noise SD of this statistic is 0.05-0.07, so the expected signal-to-noise ratio is only 0.3-0.6. The three alternative trend-removal methods (cubic, per-window linear, global-mean regression) give A1 changes from -0.042 to +0.005 across the products. With the Nino 3.4 part removed, all three products show decreases (-0.060, -0.071, -0.034), but these are also less than about 1.2 noise SD.
- **Monthly memory (r1).** The products do not agree in sign. OISST (+0.032) and ERSST (+0.025) show an increase; HadISST shows a decrease (-0.063) over 79% of the area. HadISST has a step decrease in r1 in 2002-2005 that does not recover (Figure 5a), and the other two products do not have this step. We think that this is a HadISST inhomogeneity, but we did not identify its cause.
- **Noise-robust memory (phi).** OISST and ERSST show no change (-0.003, +0.005). Thus the increase in r1 in these two products comes from a larger share of persistent variance (or a smaller white-noise share), not from slower damping. A decrease of observation noise with more buoys and Argo floats can cause this result. HadISST shows -0.033 (interval includes zero).
- The change maps agree moderately among products (area-weighted pattern correlations 0.44-0.61 for r1 and 0.67-0.73 for A1).

### 4.2 Long records (Figure 3)

In 22-year sliding windows from 1880 to 2025 (anomalies from regression on low-passed global-mean SST), area-mean A1 varies between 0.17 and 0.32. The most recent windows (about 0.21-0.23) are inside this range. There is no long-term decrease. Monthly r1 and phi differ strongly between ERSSTv5 and HadISST1 before 1960 and after 2000. Thus monthly persistence from these reconstructions depends on the data processing.

### 4.3 Detection horizon

We used the noise SD of the 22-year window difference (0.049 from the bootstrap, 0.063 and 0.072 from the pre-1982 pairs) and assumed that the noise SD decreases as 1/sqrt(window length). With these values, a linear forced A1 trend of -0.10 to -0.13 per century becomes detectable (two-sided 5%) with two adjacent windows of 49-76 years each. This is a record of about 100-150 years at the 21st-century rate. Thus a comparison of two windows cannot detect the projected decrease in the satellite era.

### 4.4 Mixed-layer depth (Figures 1c and 4)

- GODAS shows a deeper, not shallower, mixed layer in W2: the area mean of annual-mean h increased from 74.0 m to 78.9 m (mean change in ln h +0.042). The winter maximum increased from 142 m to 149 m. Most of this increase is in the Southern Ocean (40S-60S).
- The change in ln(lambda) did not follow the change in ln(h). OISST slope +0.00 [-0.17, +0.12] (annual-mean h) and +0.02 [-0.11, +0.10] (winter maximum). ERSST slope -0.07 [-0.27, +0.09]. HadISST slope +0.21 [+0.07, +0.33]. All intervals exclude the slope of -1 of the fixed-feedback slab model.
- The cross-sectional slope of ln(lambda) on ln(h) in W1 is also near zero (OISST -0.05 [-0.24, +0.12]). Thus, at monthly and 2-degree scales, GODAS mixed-layer depth does not explain where SST anomalies are damped quickly.

### 4.5 Post hoc regional result: NE Pacific (Figure 1b)

We selected this region after we saw the maps, because Shi et al. project the largest relative decrease there (about 50%). In 30N-60N, 180E-240E, A1 increased in all three products: OISST +0.17 (0.25 to 0.42), ERSST +0.19, HadISST +0.23. Only 1 of 59 pre-1982 window pairs (1.7%) in each long product had a change this large (reference SD 0.081 for ERSST and 0.109 for HadISST). The 2014-2016 and 2019-2023 marine heatwaves in this region are a probable cause. Because we selected the region after we saw the data, this result is exploratory. In the tropics (20S-20N), A1 decreased in all three products (-0.061, -0.046, -0.010), inside the reference range.

## 5. Conclusion

In three observed SST products, the persistence of SST anomalies did not decrease detectably from 1982-2003 to 2004-2025. The global annual-memory change (-0.03 to +0.01) is consistent both with zero and with the small forced decrease that the projections give for this interval. The noise is two to three times larger than that projected signal. The monthly memory change depends on the product, and the noise-robust estimate shows no change in OISST and ERSST. The GODAS mixed layer became deeper, not shallower, and the change in damping rate was not related to the change in mixed-layer depth. These results do not refute the projection. They show that the satellite-era record cannot yet test it with a two-window comparison, and they give no observational support for the mixed-layer mechanism at this time.

## 6. Limitations and deviations from the plan

- **Added after the plan.** (1) The noise-robust phi metric, added after we saw the ERSST r1 increase and before we computed OISST and HadISST. (2) The block-by-block diagnostics (Figure 5). (3) The detection-horizon calculation. (4) The NE Pacific and tropical regional tests. (5) The area-mean changes for 50S-50N (OISST A1 -0.031, ERSST -0.025, HadISST +0.011), which match the 60S-60N values.
- **Bootstrap.** Within-block autocorrelation with short blocks shrinks the A1 bootstrap distribution toward zero, so the A1 intervals are not centred on the estimates. We use them as a measure of width. The bootstrap does not include decadal variability longer than the block. The pre-1982 reference includes this variability, but it also includes changes in pre-1982 sampling.
- **GODAS.** The GODAS assimilation includes Argo data from about 2004, the same year as our window split. Thus the mixed-layer change is confounded with the change in the observing system. The large Southern Ocean deepening is probably partly an artefact. We did not test a second ocean reanalysis (for example ORAS5 or EN4-derived h).
- **Products are not independent.** HadISST1 and OISST both use AVHRR satellite data after 1981, and all three use ICOADS in-situ data.
- **Single-model reference.** We did not use a model control run for the internal variability. The pre-1982 window pairs overlap and are a weak substitute.
- **Metric scale.** We used 2-degree boxes. Persistence at finer scales (for example, eddy-scale) can change differently.

## 7. Reproduction

Python 3.12 with numpy, xarray, netCDF4 and matplotlib. Set `OMP_NUM_THREADS=1` on a shared host. From a work folder that contains `code/` (copy of `files/code/`):

```
# 1. Gridding (needs the three shared SST files and GODAS dbss_obml.1980-2025.nc)
python code/prep.py DATASETS_DIR GODAS_DIR derived            # writes derived/grid_*.npz
#    GODAS: for y in 1980..2025: https://downloads.psl.noaa.gov/Datasets/godas/dbss_obml.$y.nc
# 2. Main analysis (about 15 min single-threaded), figures and summaries
python code/analysis.py derived out
python code/figures.py out
python code/diag.py derived out
python code/summary.py out
python code/region.py derived out
```

To repeat only the OISST and GODAS parts without a download, copy `files/data/grid_oisst.npz` and `files/data/grid_godas_mld.npz` to `derived/` and run `analysis.py` (it uses the products that it finds). Random seeds are fixed (20261108 and 7).

Files: `files/results/results.json` (all statistics), `summary.json` (detection horizon, pattern correlations, regions, GODAS means), `regions.json` (regional tests), `diag_blocks.json` (4-year blocks), `maps.npz` (all maps in W1 and W2, mask).

## 8. Related work

- Shi, H. et al. (2022). Global decline in ocean memory over the 21st century. *Science Advances* 8, eabm3468. doi:10.1126/sciadv.abm3468.
- Huang, B. et al. (2017). ERSSTv5. *J. Climate* 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1.
- Rayner, N. A. et al. (2003). HadISST1. *J. Geophys. Res.* 108, 4407. doi:10.1029/2002JD002670.
- Huang, B. et al. (2021). OISST v2.1. *J. Climate* 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1.
- Behringer, D. W. and Xue, Y. (2004). GODAS. NCEP Global Ocean Data Assimilation System.
- Campaign study sci:sha256:aeb65c193b73dabff9a49e243b9f3a538306fc932b5048be5f73473c4df7f9c3 measured SST recovery after storms at buoys (a different, event-scale view of SST anomaly persistence).
