# Oxygen loss at 200-300 m off southern California did not continue in 2007-2020, but oxygen stayed low

Job sci-1107-hp-earth-and-ocean-sciences-2f3f20fe8fb6 (campaign 11_07_2026, topic earth-and-ocean-sciences, machine hp, model Claude Opus 5.5 in Claude Code). The campaign-machine key signs this bundle. The signature is not a personal authorship claim.

## Question

Bograd et al. (2008) reported that dissolved oxygen (O2) below the mixed layer off southern California decreased in 1984-2006, and that the hypoxic boundary moved up toward the surface. We asked three questions:

1. Did the 1984-2006 decrease continue after 2006? We used 2007-2020 as an out-of-sample test period.
2. Was the decrease caused by vertical motion of density surfaces ("heave"), or by lower O2 on fixed density surfaces (a change of water properties)?
3. How do the 1984-2020 values compare with the 1950-1983 CalCOFI record?

## Data

- CalCOFI bottle database, 1949-03 to 2021-05, CSV release of 16 October 2023 (calcofi.org). We used the shared copy `/mnt/dell-data/shared_datasets/calcofi-bottle-db-194903-202105-csv-16oct2023/` (SHA-256 `1d074d05...07b7`). This is the latest release on the CalCOFI bottle-database page on 2026-11-09.
- NOAA NCEI ERSSTv5 PDO index (shared copy) and the NPGO index (o3d.org, update of 21 September 2026; copy in `files/data/NPGO.txt`). We used these two indices only for a secondary, exploratory test.
- Natural Earth 10 m land (map coastline only).

`files/provenance.json` gives the URLs, SHA-256 values, and the hash of each bundle file.

## Method

**Stations and casts.** We used the six core CalCOFI lines (76.7, 80.0, 83.3, 86.7, 90.0, 93.3). We kept the 56 stations with 40 or more valid O2 values at 300 m in 1949-2020. We did not use 2021 because it has only winter and spring cruises. We used only bottle records that CalCOFI marks as observed (RecInd = 3).

**O2 quality.** From 2018, about half of the deep bottle O2 values come from the CTD O2 sensor at the bottle depth (quality code 6). Before 2018, almost all values are titrations (blank code). The primary analysis accepts codes blank and 6, with a maximum gap of 80 m between the two bottles used for an interpolation. The sensitivity analysis accepts titration values only, with a maximum gap of 130 m. Both analyses have 14 test years.

**Per-cast variables** (`files/code/01_build_profiles.py`):
- O2, temperature, and potential density (sigma-theta) at 100-500 m, by linear interpolation in depth.
- O2 and depth on the density surfaces sigma-theta 26.3-26.9, by linear interpolation in density.
- Depth of the hypoxic boundary, which is the first downward crossing of 60 umol/kg (about 1.4 ml/L, the Bograd et al. threshold).

**Regional annual index.** For each variable, we fit a two-way fixed-effects model: value = year effect + (station x quarter) effect. The year effect is the regional annual anomaly. It is not sensitive to which stations and seasons a year sampled. We set the 1984-2006 mean to zero. We kept a year only if it had 15 or more casts. To get the sampling uncertainty, we resampled cruises within each year (200 replicates).

**Heave split** (300 m and 200 m). For each station, we computed a 1984-2020 relation between O2 and density. For each cast, the total O2 at depth z is the sum of two parts:
- heave part = O2 that the station relation predicts at the observed density at depth z;
- along-isopycnal part = observed O2 minus the heave part.

Both parts go through the same fixed-effects model, so the two annual indices add to the total index.

**Tests** (`files/code/02_analyze.py`). We fixed the primary variable (O2 at 300 m, all stations), the training period (1984-2006), and the test period (2007-2020) before we examined the test period. We calculated these values:
- OLS slopes for each period, with 95% intervals from a moving-block bootstrap of the residuals (block = 3 years, 4,000 replicates), and the interval of the slope difference.
- Out-of-sample error of three forecasts for 2007-2020: (a) the 1984-2006 trend extrapolated, (b) the 2002-2006 mean held flat, and (c) the 1984-2006 mean. For (a) relative to (b), we give the MSE ratio with a 3-year block bootstrap over the test years.
- A descriptive two-segment (continuous) fit to 1984-2020, with the break year chosen by least squares from 1990-2015. The break year comes from the data, so it is not a test.
- Context: the mean for 1950-1983 compared with the mean for 2007-2020 (bootstrap over years), and the slopes of all 23-year windows that have 15 or more years of data.

We repeated the tests for the inshore stations (station number 60 or less) and for the offshore stations, and for O2 at 200 m and 400 m, on sigma-theta 26.4, 26.6, and 26.8, and for the depth of the hypoxic boundary.

## Results

Units are umol/kg for O2 and metres for depth. Brackets give 95% intervals. All values are from the primary analysis, all 56 stations, and 9,734 casts with O2 at 300 m, unless the text gives a different source.

| Series | Slope 1984-2006 (/yr) | Slope 2007-2020 (/yr) | Slope difference | MSE ratio, trend / flat |
|---|---|---|---|---|
| O2 at 300 m (primary) | -0.80 [-1.28, -0.33] | +0.24 [-0.34, 0.85] | +1.04 [0.29, 1.79] | 0.86 [0.69, 1.40] |
| O2 at 200 m | -1.03 [-1.49, -0.56] | +0.84 [0.06, 1.64] | [0.97, 2.80] | 3.18 [0.89, 6.42] |
| O2 at 400 m | -0.28 [-0.60, 0.03] | -0.11 [-0.42, 0.20] | [-0.26, 0.61] | 0.82 [0.57, 1.07] |
| O2 on sigma-theta 26.4 | -0.95 [-1.21, -0.67] | +0.22 [-0.19, 0.61] | [0.67, 1.64] | 4.97 [0.56, 21.4] |
| O2 on sigma-theta 26.6 | -0.90 [-1.22, -0.55] | +0.01 [-0.33, 0.34] | [0.40, 1.36] | 0.54 [0.35, 0.76] |
| O2 on sigma-theta 26.8 | -0.33 [-0.51, -0.16] | -0.25 [-0.49, 0.00] | [-0.21, 0.40] | 0.55 [0.37, 0.78] |
| Hypoxic boundary depth | -1.82 [-3.03, -0.66] | +1.02 [-0.60, 2.67] | [0.83, 4.75] | 0.80 [0.66, 1.06] |

**1. The decrease did not continue after 2006, but O2 did not return to the 1984-2006 level.**
- At 300 m, the 2007-2020 slope was +0.24 per year, and its interval includes zero. This slope is different from the 1984-2006 slope of -0.80 per year.
- In the out-of-sample test, the extrapolated trend did not clearly perform better than the flat 2002-2006 mean (MSE ratio 0.86 [0.69, 1.40]). Thus, the primary forecast test is inconclusive.
- O2 continued to decrease to a minimum in 2012 (-25.8 relative to the 1984-2006 mean). The best single break for 1984-2020 is 2012 for most series. For O2 at 200 m, at 300 m, and on sigma-theta 26.4 and 26.6, the two-segment fits give slopes of approximately -1.0 umol/kg per year before 2012 and +0.3 to +1.6 umol/kg per year after 2012.
- Mean values for 2007-2020 stayed below the 2002-2006 mean: -5.1 at 300 m, -5.6 on sigma-theta 26.6, and -15 m for the hypoxic boundary.
- In 1984-2006, the hypoxic boundary moved up by 1.82 m per year (about 42 m in 23 years). In 2012, the boundary was 67 m shallower than the 1984-2006 mean. In 2013-2020, it was 36 m shallower.
- At 200 m, O2 increased in 2007-2020 (+0.84 per year). The extrapolated trend had 3.2 times the error of the flat forecast.
- On the deepest surface (sigma-theta 26.8) and at 400 m, the slow decrease did not stop (-0.25 and -0.11 per year in 2007-2020). The extrapolated trend had lower error than the flat forecast on sigma-theta 26.8 (MSE ratio 0.55 [0.37, 0.78]).

**2. Most of the decrease was on density surfaces, not heave.**
- At 300 m, the along-isopycnal part gave -0.74 of the -0.80 per year slope in 1984-2006 (93%). The heave part gave -0.06 per year.
- The along-isopycnal part explained 87% of the 1984-2020 variance of the annual 300 m index. At 200 m, it explained 71%.
- In 2007-2020, the heave part changed sign. Density surfaces moved down in 2014-2016 and in 2019, and the heave part gave +0.32 per year at 300 m and +0.50 per year at 200 m. Thus, most of the partial recovery at 200 m came from heave. Along density surfaces, O2 stayed approximately constant at a low level (sigma-theta 26.6: +0.01 per year).
- In 1984-2006, O2 on sigma-theta 26.6 decreased at all 55 stations that had sufficient data (median -0.83 per year). In 2007-2020, the median station slope was -0.04 per year, and 32 of 55 stations had negative slopes (Figure 2).
- The inshore and offshore groups gave the same pattern. The inshore 1984-2006 slope at 300 m was -0.59 per year, and the offshore slope was -0.99 per year. In both groups, the slope difference excludes zero.

**3. Long-record context.**
- The 1950-1983 data are sparse in the 1970s (there is no 300 m index for 1969-1976 or for 1979-1982).
- The 1984-1990 mean at 300 m (+2.1) was higher than the 1950-1983 mean (-6.5). Thus, the 1984-2006 decrease started from a high period.
- The 2007-2020 mean (-16.5) was 10.0 lower than the 1950-1983 mean (interval of the difference -13.6 to -6.7). Thus, the post-2006 values are low relative to the full record, not only relative to the 1980s.
- All 23-year windows that start in 1979 or later have negative slopes. The steepest window is 1991-2013 (-1.62 per year). Windows that start before 1979 have positive slopes, but they have only 15-19 years of data.

**4. Climate indices (secondary, exploratory).** The annual 300 m index had correlations with the same-year PDO of r = 0.28 in 1984-2006 and r = 0.74 in 2007-2020. The correlations with the NPGO were negative (r = -0.36 to -0.63 at lags 0-4 years in 1984-2006). Regressions on these indices that we fit to 1984-2006 did not forecast 2007-2020 better than the flat mean (test RMSE 15-18, flat RMSE 6.4). This is because the indices do not capture the step to low values. We did not test a mechanism for the stop of the decrease near 2012.

**Sensitivity.** The titration-only analysis (`files/results/sensitivity_bottle_only_gap130/`) gave the same conclusions. At 300 m, the slopes were -0.80 per year (1984-2006) and +0.44 per year [-0.15, 1.05] (2007-2020). The slope difference was [0.48, 1.99]. The MSE ratio was 1.10 [0.71, 2.51]. On sigma-theta 26.6, the 2007-2020 slope was +0.07 [-0.26, 0.41]. The along-isopycnal share of the 1984-2006 slope at 300 m was 93%.

## Interpretation

The CalCOFI data agree with the 1984-2006 decrease that Bograd et al. (2008) reported. These data also agree with the continued decrease in later reports (Bograd et al. 2015). The new evidence in this study is the 2007-2020 test period:
- Within 200-300 m, the decrease stopped after a minimum in about 2012. It did not reverse along density surfaces.
- The partial recovery at fixed depths after 2012 came mostly from the downward motion of density surfaces in warm years, not from a return of high-O2 water.
- A linear extrapolation of the 1984-2006 trend was not a reliable forecast at 200-300 m. A low, flat level fit the 2007-2020 data at least equally well.
- Below 300 m (sigma-theta 26.8 and 400 m), a slow decrease continued.

These results agree with explanations that put the main control on the properties of the source water on density surfaces, for example decadal changes in the California Undercurrent water (Bograd et al. 2015; Pozo Buil and Di Lorenzo 2017). They do not agree with explanations that put the main control on isopycnal heave.

## Limitations

- The study region is the southern California CalCOFI grid only. The test period is 14 annual values, so the slope intervals are wide.
- The block bootstrap uses 3-year blocks, and it does not fully represent decadal autocorrelation. Treat the intervals as approximate.
- The 2012 break year comes from the data. Use it only as a description.
- The O2 method changed in 2018 (CTD sensor values at bottle depths). The titration-only sensitivity analysis agrees, but a small bias in the 2018-2020 data is possible.
- The heave split uses a fixed station O2-density relation from 1984-2020 and a linear interpolation. It does not include mixing or diapycnal processes.
- The 1950-1983 comparison uses fewer years and a different station coverage. The fixed-effects model corrects only the station and season composition.
- 2021 and later years are not in the CalCOFI release that we used.
- We did not test biological O2 use, nutrients, or advection directly.

## Reproduce

```
cd files
bash code/run_all.sh        # set CALCOFI, PDO, LAND to local copies if the shared paths are not available
```

The run takes approximately 10 minutes on 8 cores, with a fixed random seed. We ran the script again from the raw inputs and compared the outputs to the files in `files/results/` (see the Reproduction check section). The per-cast tables (`files/data/cast_vars_*.parquet`) let you inspect the results without the raw ZIP file.

## Reproduction check

On 2026-11-09, we ran `code/run_all.sh` again from the raw shared inputs into a new folder. All eight primary output files and the three main sensitivity files (`trend_tests.csv`, `annual_index.csv`, `summary.json`) were byte-identical to the files in this bundle.

## Files

- `files/code/`: the three analysis scripts and `run_all.sh`.
- `files/data/`: the per-cast derived variables for both O2 quality modes, and the NPGO index copy.
- `files/results/primary/`: the annual indices (`annual_index.csv`), the cast counts, all test statistics (`trend_tests.csv`, `summary.json`), the cruise-bootstrap standard errors, the 23-year window slopes, the climate-index lags, and the station slopes.
- `files/results/sensitivity_bottle_only_gap130/`: the same outputs for the titration-only analysis.
- `files/figures/`: Figures 1 and 2.
- `files/provenance.json`: the inputs, hashes, software versions, and job details.

## References

- Bograd, S. J., et al. (2008). Oxygen declines and the shoaling of the hypoxic boundary in the California Current. GRL. doi:10.1029/2008GL034185
- Bograd, S. J., et al. (2015). Changes in source waters to the Southern California Bight. Deep-Sea Res. II. doi:10.1016/j.dsr2.2014.04.009
- Ren, A. S., et al. (2018). A sixteen-year decline in dissolved oxygen in the central California Current. Sci. Rep. doi:10.1038/s41598-018-25341-8
- Deutsch, C., et al. (2011). Climate-forced variability of ocean hypoxia. Science. doi:10.1126/science.1202422
- Pozo Buil, M., and Di Lorenzo, E. (2017). Decadal dynamics and predictability of oxygen and subsurface tracers in the California Current System. GRL. doi:10.1002/2017GL072931
- Di Lorenzo, E., et al. (2008). North Pacific Gyre Oscillation links ocean climate and ecosystem change. GRL. doi:10.1029/2007GL032838
