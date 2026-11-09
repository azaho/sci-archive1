# GRACE land water storage rose faster than it fell at 1-24 month lags in 2002-2026; rain-driven linear models did not reproduce the 12-month asymmetry

## Summary

**Question.** Is the change of total land water storage (TWS) symmetric in time? That is, do storage deficits (droughts) form and end at the same speed? If the change is not symmetric, does the skewness of rain explain the asymmetry?

**Data.** CSR GRACE/GRACE-FO RL06.3 mascon TWS, April 2002 to June 2026. We used 2,168 land cells of 2.5 x 2.5 degrees between 56 S and 75 N, without Greenland and Antarctica. We used GPCP v2.3 monthly precipitation for the forcing, and GHCN-CAMS temperature to find cold cells.

**Method.** For each cell, we removed the mean, a linear trend, and the annual and semi-annual cycles. Then we calculated the skewness of the storage change over a lag of L months, x(t+L) - x(t), for L = 1 to 24. For a process that is symmetric in time (reversible), this skewness is zero. A positive value shows fast rises and slow falls. We also found deficit and surplus events and compared their development time with their recovery time. We tested the global mean against 1,000 Fourier surrogates. These surrogates keep the spectrum of each cell and all cross-spectra between cells, but they are reversible. We also used a sign-flip test on 111 spatial blocks of 15 degrees. To explain the result, we drove three rain models with observed GPCP anomalies: a linear single store, a linear model with two poles (ARX), and an ARX whose rain gain changes with the storage state.

**Main results.**

1. TWS is not symmetric in time. The area-weighted mean skewness of storage change was positive at all 24 lags: 0.076 at L = 1 and 0.099 at L = 12. The 95% surrogate range was -0.018 to 0.019 at L = 1 and -0.038 to 0.039 at L = 12 (surrogate p = 0.001, the smallest possible value with 1,000 surrogates; block sign-flip p < 0.001). Both missions showed the result separately: GRACE (2002-2017) gave 0.039, 0.055 and 0.088 at L = 1, 6 and 12. GRACE-FO (2018-2026) gave 0.072, 0.115 and 0.074 (all surrogate p <= 0.006).
2. With a linear trend, deficits ended faster than they formed, and surpluses formed faster than they decayed. For 8,455 deficit events (trough at least 1 SD below zero), the mean ln(recovery time / development time) was -0.059 (surrogate 95% range -0.047 to 0.043; p = 0.010; block p = 0.005). This is a recovery approximately 6% shorter than the development. For 8,131 surplus events, the value was +0.098 (p = 0.003). The asymmetry increased with deficit depth: -0.039, -0.059 and -0.082 for the shallow, middle and deep thirds of events. **This deficit result is not robust:** with a quadratic trend, the deficit value was only -0.026, inside the surrogate range of the main run. The surplus value (+0.096) and the skewness did not change much.
3. The asymmetry is a property of dry regions. At L = 12, the mean skewness was 0.19 in arid cells (annual rain < 400 mm) and 0.22 in semi-arid cells (400-1000 mm), both p = 0.001. It was 0.013 in humid cells (p = 0.66) and 0.055 in cold cells (coldest month < -3 C; p = 0.08).
4. Skewed rain explains the short-lag asymmetry but not the year-scale asymmetry. Monthly GPCP anomalies had positive skewness on 97% of the land area (mean 1.08). The rain-driven models gave a larger skewness than observed at L = 1 (0.26 to 0.37 against 0.076), but they gave only 0.018 to 0.041 at L = 12 against 0.099, and -0.037 to -0.005 at L = 24 against 0.074. The 12-month change of 12-month rain totals was almost symmetric (skewness 0.020). The rain gain in the deficit state was not different from the gain in the surplus state (difference -0.013 mm/mm, 95% block bootstrap interval -0.063 to 0.037). A placebo with a linear model gave +0.030, so this method does not have a negative bias.

**Interpretation.** Land water storage fills in pulses and drains slowly, and droughts end faster than they start. At monthly lags, the skewness of rain through a linear store gives enough asymmetry to explain this. At 6 to 24 month lags, these rain models explain less than half of the observed asymmetry. Thus a part of the year-scale asymmetry has a different cause. Possible causes, which we did not test, are human water use (more pumping during droughts makes the declines slower), lake and reservoir dynamics, and nonlinear groundwater recharge that is not a function of the TWS sign.

**Main limitations.** GRACE resolution is approximately 300 km, so the 2,168 cells are not independent; the block tests account for this only approximately. The record has 24 years, so few multi-year events occur in each cell. GRACE noise and leakage can change the skewness. A trend that is not linear changes the deficit-event result (see the robustness section). Because the host computer was overloaded, the complete surrogate tests ran only for the linear trend. The other trend variants have only observed values. The climate classes are approximate. We did not include human water use or river and lake data.

## Data

| Dataset (shared campaign path) | Source | SHA-256 of file used |
|---|---|---|
| `datasets/csr-grace-rl0603-mascon-all-corrections-20261108/CSR_GRACE_GRACE-FO_RL0603_Mascons_all-corrections.nc` | CSR GRACE/GRACE-FO RL06.3 mascons (label RL0603rc24cE, created 2026-10-07), https://download.csr.utexas.edu/outgoing/grace/RL0603_mascons/ | `d4bd8b7364fb34d871198001563c70d344792cb7b0a577c04f8b91c713741292` |
| `datasets/csr-grace-rl06-v02-landmask-20261108/CSR_GRACE_GRACE-FO_RL06_Mascons_v02_LandMask.nc` | CSR RL06 mascon land mask, same URL folder | `65ddd8f3c7f7633c3a34f904e196307f71e4994e11ceb64f9337275908ff2f3b` |
| `datasets/noaa-psl-gpcp-v23-precip-mon-mean-20261108/precip.mon.mean.nc` | GPCP v2.3 monthly precipitation, NOAA PSL, https://downloads.psl.noaa.gov/Datasets/gpcp/precip.mon.mean.nc (file last-modified 2026-07-20; data to 2026-06). This worker added it with `campaign-dataset`. | `d31c53ab8180a883bd01442212948c3db4372d481b94a90e69d3d86bb65d7f68` |
| `datasets/noaa-psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` | GHCN-CAMS monthly 2 m air temperature, NOAA PSL, https://downloads.psl.noaa.gov/Datasets/ghcncams/air.mon.mean.nc | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |

The package does not copy the raw files. `files/data/input_sha256.txt` has the hashes.
To get the files again, download the URLs above and compare the hashes.

## Methods in detail

**Panel (`files/code/prep.py`).** We read the CSR RL06.3 mascon grid (0.25 degree; one month at a time) and made the mean over blocks of 10 x 10 grid points. This gives the GPCP 2.5 degree grid. Each GRACE solution goes to the calendar month of its midpoint. If two solutions had the same month (2011-10 and 2015-04), the later one went to the next month, which had no solution (2011-11 and 2015-05). The land fraction comes from the CSR land mask. Annual rain (1981-2020 GPCP climatology) and the coldest-month mean temperature (1981-2020 GHCN-CAMS, regridded to 2.5 degrees) give the climate classes.

**Cells and time.** We kept cells with land fraction >= 0.75, latitude 56 S to 75 N, not Greenland, and with complete rain data: 2,168 cells. The time window is 2002-04 to 2026-06 (the end of GPCP). The 11-month gap between missions (2017-07 to 2018-05) divides the record into two segments. In each segment, we filled gaps of 3 months or less (22 months in total) by linear interpolation. No difference crosses the gap between missions.

**Anomalies.** For each cell, an ordinary least-squares fit on the observed months removes a constant, a linear trend, and annual and semi-annual harmonics. The robustness variants use a quadratic trend, or a linear trend plus a separate offset for GRACE-FO.

**Irreversibility statistics (`files/code/analyze.py`).**
- g(L): the sample skewness of x(t+L) - x(t), for all pairs inside one segment, L = 1 to 24 months. A time-reversible process gives g = 0 in expectation, whatever its marginal distribution.
- f(L): the fraction of positive changes minus 0.5. This is a statistic that is not sensitive to large values.
- Events: on a 3-month centred running mean (which is symmetric in time), a deficit event is a run of negative values that has zero or positive values on the two sides and a trough at or below -1 SD of the cell anomaly. Development D = trough month - last non-negative month before the run. Recovery R = first non-negative month after the run - trough month. Surplus events are the same for -x. The cell statistic is the mean of ln(R/D).
- Global value: the mean over cells, with cos(latitude) weights.

**Null tests.**
1. Common-phase Fourier surrogates. For each segment, we multiplied the Fourier transform of all cells by the same random phases. This keeps the power spectrum of each cell and the cross-spectra between cells (thus the spatial correlation), and it gives reversible Gaussian series. 1,000 surrogates for g and f, the first 300 also for events. The p-values are two-sided: (1 + count(|null| >= |obs|)) / (N + 1). Cell p-values used the same surrogates, with Benjamini-Hochberg FDR at q = 0.05.
2. Block sign-flip. Each 15 x 15 degree block (111 blocks) gives its contribution to the weighted mean, and random sign changes of the blocks give the null distribution (20,000 draws). Time reversal changes the sign of each statistic, so this test does not need a Gaussian assumption.
3. Mission replication: each segment alone, with 500 surrogates.
4. Year jackknife: we removed all differences that end in one calendar year and calculated the result again.

**Rain models (`files/code/mechanism.py`).** P' is the GPCP anomaly (monthly climatology and linear trend removed). The models are fitted on observed consecutive months:
- Single store: x(t) - x(t-1) = b0 P'(t) + b1 P'(t-1) - k x(t-1) + c.
- Two-pole ARX: x(t) = a1 x(t-1) + a2 x(t-2) + sum over j = 0..5 of bj P'(t-j) + c. All 2,168 fits were stable.
- Threshold ARX: the same as the two-pole ARX, plus terms in P'(t-j) times I(x(t-1) < 0) and a constant for the deficit state.
We simulated each model from the observed P' for 2002-2026, processed the output as the GRACE data (same detrending, same segments) and calculated g(L). Controls: P' changed to a Gaussian series with the same ranks and SD ("rain made Gaussian"), and P' with the opposite sign (this gives the opposite sign of g). A placebo for the gain test fits the threshold model to a linear ARX simulation plus white noise with the residual SD. The spatial correlations use a block bootstrap with 15-degree blocks (2,000 draws).

## Results tables

### Global mean skewness by lag (linear trend, 1,000 surrogates)

| L (months) | 1 | 3 | 6 | 9 | 12 | 18 | 24 |
|---|---|---|---|---|---|---|---|
| observed g(L) | 0.076 | 0.083 | 0.102 | 0.093 | 0.099 | 0.075 | 0.074 |
| surrogate 2.5% | -0.018 | -0.022 | -0.031 | -0.038 | -0.038 | -0.043 | -0.043 |
| surrogate 97.5% | 0.019 | 0.021 | 0.031 | 0.033 | 0.039 | 0.044 | 0.046 |
| block sign-flip p | 0.0004 | 0.0002 | <0.0001 | 0.0001 | <0.0001 | 0.015 | 0.038 |

The surrogate p-value was <= 0.007 at all 24 lags. The block sign-flip p-value was < 0.05 at all lags except L = 22 (p = 0.051). The fraction of positive changes was smaller than 0.5 at all lags (-0.002 to -0.008); this is the expected result for fast rises and slow falls, but the effect is small, and the surrogate p-value was < 0.05 only at L = 1-12 and 22-24.

Area with positive g: 56% of the land area at L = 1 and 57% at L = 12. Cells with FDR-significant positive g: 9.6% of the area at L = 1 and 5.8% at L = 12. Cells with FDR-significant negative g: 3.4% and 1.6%.

### Climate classes (L = 1, 12, 24)

| class | cells | area fraction | g(1) | p | g(12) | p | g(24) | p | deficit ln(R/D) | p |
|---|---|---|---|---|---|---|---|---|---|---|
| arid (< 400 mm/yr) | 350 | 0.197 | 0.111 | 0.001 | 0.192 | 0.001 | 0.207 | 0.001 | -0.128 | 0.013 |
| semi-arid (400-1000 mm/yr) | 314 | 0.170 | 0.171 | 0.001 | 0.223 | 0.001 | 0.199 | 0.001 | +0.027 | 0.55 |
| humid (> 1000 mm/yr) | 468 | 0.276 | 0.051 | 0.001 | 0.013 | 0.66 | -0.012 | 0.66 | +0.058 | 0.13 |
| cold (coldest month < -3 C) | 1,036 | 0.357 | 0.031 | 0.026 | 0.055 | 0.082 | 0.009 | 0.87 | -0.153 | 0.003 |

The event result and the skewness result do not agree in all classes. In semi-arid cells, g is large, but the event ratio is near zero. In cold cells, g is small, but deficits end clearly faster than they form. The two statistics measure different parts of the dynamics (all changes against threshold events), so we report both.

### Events

| | n | median D (months) | median R (months) | fraction R < D | fraction R > D | weighted mean ln(R/D) | surrogate 95% range | p (surrogate / block) |
|---|---|---|---|---|---|---|---|---|
| deficits | 8,455 | 7 | 6 | 0.478 | 0.429 | -0.059 | -0.047 to 0.043 | 0.010 / 0.005 |
| surpluses | 8,131 | 6 | 7 | 0.433 | 0.466 | +0.098 | -0.042 to 0.048 | 0.003 / 0.001 |

Deficit depth thirds (depth in units of the cell SD): 1.00-1.26 SD, ln(R/D) = -0.039, n = 2,819; 1.26-1.69 SD, -0.059; 1.69-4.54 SD, -0.082. These tercile values are pooled over events without a separate test.

### Rain models: global mean g(L)

| L | GRACE observed | single store | two-pole ARX | threshold ARX | ARX, rain made Gaussian |
|---|---|---|---|---|---|
| 1 | 0.076 | 0.372 | 0.307 | 0.260 | 0.044 |
| 3 | 0.083 | 0.173 | 0.239 | 0.204 | 0.037 |
| 6 | 0.102 | 0.059 | 0.116 | 0.100 | 0.024 |
| 12 | 0.099 | 0.023 | 0.041 | 0.018 | 0.008 |
| 24 | 0.074 | -0.005 | -0.022 | -0.037 | -0.047 |

Other numbers: median one-step R^2 was 0.29 for the single store and 0.55 for the ARX; the median single-store k was 0.36 per month (time scale near 3 months). The weighted spatial correlation of observed g(12) with rain skewness was 0.14 (95% block bootstrap 0.07 to 0.23), and with the single-store g(12) it was 0.27 (0.19 to 0.34). In arid cells, the observed g(12) was 0.19 and the ARX g(12) was 0.04; in semi-arid cells, 0.22 and 0.07.

GRACE noise is reversible and decreases the observed skewness, mostly at L = 1. This can explain why the models give more skewness than observed at short lags. Noise cannot explain why the models give less skewness than observed at 12 and 24 months.

## Robustness

### Trend treatment (observed values, `files/code/robust_trend.py`)

| trend | g(1) | g(6) | g(12) | g(24) | deficit ln(R/D) | surplus ln(R/D) |
|---|---|---|---|---|---|---|
| linear (main) | 0.076 | 0.102 | 0.099 | 0.074 | -0.059 | +0.098 |
| quadratic | 0.076 | 0.097 | 0.087 | 0.055 | -0.026 | +0.096 |
| linear + GRACE-FO offset | 0.077 | 0.104 | 0.099 | 0.074 | -0.074 | +0.096 |
| main surrogate 97.5% (linear) | 0.019 | 0.031 | 0.039 | 0.046 | -0.047 / 0.043 (2.5% / 97.5%) | 0.048 |

All skewness values stay above the 97.5% surrogate value of the main run. The deficit-event value with a quadratic trend (-0.026) is inside the main surrogate range. Thus, we do not claim that deficit recovery is faster when the trend is not linear. A within-segment offset does not change g(L) at L = 12 or 24, because the offset cancels in differences inside one segment.

We started complete surrogate runs (100 surrogates) for the quadratic, offset and no-trend variants. The host had a load average near 90 and full swap, and the runs stopped at the 2-hour job limit. We did not use partial results. The no-trend variant has no result.

### Year jackknife (linear trend)

When we removed the differences that end in one calendar year, g(1) stayed between 0.050 (without 2024) and 0.091 (without 2025). g(12) stayed between 0.083 (without 2017) and 0.118 (without 2025). One year does not cause the global result. `files/results/robustness_summary.json` gives all values.

### Spatial pattern

Figure 1 shows the largest positive g(12) in the Sahel, East Africa, southern Africa, eastern Australia, the interior western United States, central Asia and north-east Siberia. Some of these regions had known wet episodes in the record (for example, East Africa in 2019-2020 and eastern Australia in 2010-2011). We did not test which episodes control each cell value. Negative values occur in parts of northern Canada, the Middle East, north India and the Tibetan Plateau. Some of these regions have strong human or glacier mass trends. The field is noisy: only 5.8% of the land area is FDR-significant positive at L = 12.

## Limitations

- **Resolution and dependence.** The native GRACE resolution is approximately 300 km and the 2.5-degree cells overlap in information. The surrogates keep the observed cross-correlation, and the block test uses 111 blocks. However, the blocks are also correlated across their borders, so the block p-values can be too small.
- **Short record.** 24 years with an 11-month gap. Multi-year events are few in each cell. Skewness depends on large events, so a small number of wet episodes can control a cell value.
- **Gaussian surrogates.** Fourier surrogates are Gaussian. Their spread of the skewness statistic can be different from a reversible process with heavy tails. The block sign-flip test does not need this assumption and agrees.
- **Event definition.** The events depend on the detrending, the 1 SD threshold and the 3-month smoothing. The deficit result changes with the trend model.
- **Mechanism tests.** The rain models are simple and use GPCP only (no evaporation, snow, river inflow, irrigation or pumping). The failure of these models at 12-24 months does not identify the real cause. Human water use, lakes and reservoirs, and nonlinear recharge are candidate causes that we did not test.
- **GRACE processing.** CSR mascon regularisation and leakage between land and ocean can change local values. We did not compare with JPL or GSFC mascons.
- **Climate classes.** The classes use simple thresholds on GPCP annual rain and GHCN-CAMS temperature.

## Reproduce

Python 3.12.16 with numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, xarray 2026.9.0, netCDF4 1.7.5.1.post1, matplotlib 3.11.2. Set one thread (`OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1`). Random seeds are fixed in the code.

```
# 1. panel from raw files (DATASETS = folder with the four dataset folders named in the Data table)
python -I files/code/prep.py DATASETS panel.npz                     # same content as files/data/panel_2p5deg.npz
# 2. main analysis, 1,000 surrogates, linear trend (approx. 70 min on a loaded host)
python -I files/code/analyze.py panel.npz out 1000 linear
# 3. rain models
python -I files/code/mechanism.py out/irreversibility_linear_arrays.npz out/mechanism_linear.json out/mechanism_linear_cells.npz
# 4. trend robustness (observed values)
python -I files/code/robust_trend.py out/irreversibility_linear_arrays.npz out/robust_trend.json
# 5. figures, jackknife and cell table
python -I files/code/make_figures.py out figures
python -I files/code/export_cells.py out/irreversibility_linear_arrays.npz out/mechanism_linear_cells.npz cells_linear.csv
```

To start from the included panel, use `files/data/panel_2p5deg.npz` in step 2.

## Files

- `files/code/`: all analysis code (prep, analyze, mechanism, robust_trend, make_figures, export_cells).
- `files/data/panel_2p5deg.npz`: the derived 2.5-degree monthly panel (TWS in mm, GPCP rain in mm/month, land fraction, climate fields, month index). `files/data/input_sha256.txt`: hashes of the raw input files.
- `files/results/irreversibility_linear.json`: all global, class, mission, event and test results. `irreversibility_linear_arrays.npz`: cell statistics, anomalies, surrogate global values. `mechanism_linear.json` and `mechanism_linear_cells.npz`: rain-model results. `robust_trend.json`, `robustness_summary.json`: robustness. `cells_linear.csv`: one row for each cell. Logs of the runs.
- `files/figures/`: Figures 1-4.

## Figures

- Figure 1 (`fig1_map_lag12_skewness.png`): skewness of 12-month storage changes for each cell; dots show FDR q < 0.05.
- Figure 2 (`fig2_lag_skewness.png`): global mean skewness at lags 1-24 against the reversible surrogate range, with each mission separately (a), and for each climate class (b).
- Figure 3 (`fig3_mechanism_models.png`): observed skewness and the skewness of the rain-driven models.
- Figure 4 (`fig4_event_durations.png`): distribution of log2(recovery / development) for deficit and surplus events (a), and area-weighted mean ln(R/D) with the surrogate range (b). The depth-tercile bars are pooled means over events, not area-weighted.

## Provenance

- Campaign 11_07_2026, job `sci-1107-syam1-earth-and-ocean-sciences-867207075624`, topic earth-and-ocean-sciences, machine syam1, account claude-olen.
- Model: Claude Opus 5.5 (`claude-opus-5-5`), working through the Claude Code harness. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-08. The GPCP file was added to the shared campaign dataset store as `noaa-psl-gpcp-v23-precip-mon-mean-20261108` by this job.
- Related campaign work: a campaign result used GRACE seasonal loads for earthquake timing; others studied runoff after droughts in reference catchments. As far as we know, no earlier campaign result tested the time asymmetry of GRACE storage.

## References

- Save, H., Bettadpur, S., Tapley, B. D. (2016). High-resolution CSR GRACE RL05 mascons. J. Geophys. Res. Solid Earth 121, 7547-7569. doi:10.1002/2016JB013007. CSR RL06.3 mascon data: doi:10.15781/cgq9-nh24.
- Adler, R. F. et al. (2018). The Global Precipitation Climatology Project (GPCP) monthly analysis (new version 2.3) and a review of 2017 global precipitation. Atmosphere 9, 138. doi:10.3390/atmos9040138.
- Fan, Y., van den Dool, H. (2008). A global monthly land surface air temperature analysis for 1948-present. J. Geophys. Res. 113, D01103. doi:10.1029/2007JD008470.
- Theiler, J. et al. (1992). Testing for nonlinearity in time series: the method of surrogate data. Physica D 58, 77-94. doi:10.1016/0167-2789(92)90102-S.
- Thomas, A. C., Reager, J. T., Famiglietti, J. S., Rodell, M. (2014). A GRACE-based water storage deficit approach for hydrological drought characterization. Geophys. Res. Lett. 41, 1537-1545. doi:10.1002/2014GL059323.
- Singh, Reager and Behrangi (2021). GRACE-based estimate of drought recovery time from the precipitation needed to refill storage. Hydrol. Earth Syst. Sci. 25, 511-526. doi:10.5194/hess-25-511-2021.
