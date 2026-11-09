# Earlier nearby sequences improve out-of-sample forecasts of aftershock counts for global shallow M6+ mainshocks, 2000-2026

Job `sci-1107-dell-earth-and-ocean-sciences-15713dc1f4b9`, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-andrii. Analysis and text by the model claude-opus-5-5 (Claude Opus 5.5) in Claude Code. The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

Two mainshocks of the same magnitude can have very different numbers of aftershocks. Operational aftershock forecasts use a magnitude scaling law and, at most, a coarse tectonic region (Page et al., 2016). We asked one question: **does the aftershock productivity of earlier mainshocks near a new mainshock forecast the productivity of the new sequence, out of sample?**

We used the USGS ComCat global catalog (M 4.5 and larger, 1973 to 8 November 2026) and Global CMT mechanisms. We selected 3,486 shallow (depth 70 km or less) M6+ mainshocks from 1980 to 2026. The outcome is the number of M4.5+ events within 10 days and within a radius of max(50 km, 2 rupture lengths). We made rolling forecasts. For each test year from 2000 to 2026, we fit negative-binomial models only on sequences that ended before 1 January of that year. Then we scored the predictive log-likelihood of each test sequence (1,992 test sequences).

Main results:

1. **Neighbour productivity is the strongest single predictor that we tested.** A shrunken mean of earlier residuals within 200 km (window closed at least 1 year before the new mainshock) increased the out-of-sample log-likelihood by 0.061 nats per sequence (95% CI 0.041 to 0.079) relative to magnitude plus a linear year trend. Depth gave 0.003, GCMT mechanism class gave 0.025, and the prior 5-year background rate gave 0.014. All three together gave 0.058.
2. **The gain stays after control for depth, mechanism and background rate.** The neighbour term added 0.049 nats per sequence (CI 0.032 to 0.066; year-block CI 0.034 to 0.063). The gain was positive in 26 of 27 test years. The cumulative gain was 98 nats.
3. **The forecast is almost calibrated.** The regression slope of the observed residual on the forecast neighbour residual was 0.87 (SE 0.05). The Spearman correlation was 0.38 (n = 1,859 test sequences with neighbours). In the lowest forecast quintile, the median count was 0 and 51% of sequences had no M4.5+ aftershock. The observed total was 0.41 times the magnitude-only expectation. In the highest quintile, the median count was 4, 21% had none, and the observed total was 1.32 times the expectation.
4. **Similarity decreases with distance but not with time.** For pairs of mainshocks at similar depth, the residual correlation was 0.29 (CI 0.26 to 0.33) at less than 50 km, 0.11 at 100 to 200 km, 0.05 at 800 to 1,600 km and -0.01 beyond 3,200 km. Within 200 km, the correlation was 0.14 to 0.17 for lags of 1-3, 3-10, 10-20 and 20-47 years. We did not find a decrease over four decades.
5. **Most of the gain is at a regional scale.** A mean over earlier sequences within 1,000 km added 0.062 nats per sequence beyond depth, mechanism and background. A 100 km term added a further 0.013 (CI 0.006 to 0.022).

Main limitation: part of the signal can be a catalog effect and not physics. Regional differences in detection of M4.5 events, and in magnitude scales, also persist in space and time. A background detection proxy (ratio of M4.5-4.9 to M5+ events within 300 km) decreased the neighbour gain from 0.049 to 0.034 nats (CI 0.020 to 0.047), but did not remove it. With M5+ aftershock counts as the outcome, the gain was 0.014 (CI 0.006 to 0.022) when residuals came from M5+ counts. It was 0.022 (CI 0.013 to 0.032) when residuals came from M4.5+ counts. The 100 km term beyond the 1,000 km term was 0.0045 (CI -0.0003 to 0.0093) for M5+ counts. Thus the regional component is robust, but the local (100 km) component is uncertain for the more complete M5+ counts.

## Figures

- `files/figures/fig3_oos_gain.png`: (a) out-of-sample gain of each predictor in the primary test, (b) gain of the 200 km neighbour term beyond depth, mechanism and background in 19 analysis variants, (c) 1,000 km term and 100 km term beyond it.
- `files/figures/fig2_pair_correlation.png`: residual correlation of earlier-later mainshock pairs as a function of distance (a) and lag (b).
- `files/figures/fig4_calibration.png`: (a) calibration by forecast quintile, (b) cumulative gain over test years.
- `files/figures/fig1_map_local_residual.png`: map of the local mean residual (descriptive, all years pooled, in-sample). The residual is ln((N+0.5)/(mu+0.5)). Its mean is less than zero because counts are skewed. Thus only relative colours have meaning. High values are mostly on the Alpine-Himalayan collision belt and in Japan. Low values are mostly on mid-ocean ridges and oceanic transforms.

## Data

| Input | Source | Version and hash |
| --- | --- | --- |
| ComCat global M4.5+ catalog, 1973-01-01 to 2026-11-08 12:29 UTC | `https://earthquake.usgs.gov/fdsnws/event/1/query`, one CSV query per year, retrieved 2026-11-08 about 13:25 UTC. No year reached the 20,000 row limit. | Archived in this bundle: `files/data/raw/comcat_global_m4.5_1973_2026.tar.gz` (sha256 `19e97634...bfb0`). Per-file hashes are in `files/data/raw/comcat_csv_sha256.txt`. 294,099 events of type earthquake. |
| Global CMT catalog 1976-2020 | `https://www.ldeo.columbia.edu/~gcmt/projects/CMT/catalog/jan76_dec20.ndk`; campaign copy `/mnt/dell-data/shared_datasets/gcmt-ndk-jan76-dec20-20261107/jan76_dec20.ndk` | sha256 `baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4`, 23,016,960 bytes. Not copied into this bundle. |
| Global CMT monthly NDK files, Jan 2021 to Jun 2026 | Entry `files/raw/gcmt_monthly_2021_2026.tar.gz` of SCI bundle `sci:sha256:7184e3ca...c179c1` (original source: GCMT NEW_MONTHLY) | sha256 `f706b68a15917423925340fed8ecedec70f2f998a91914fbc15018449163e593`. Not copied into this bundle. |

Full provenance is in `files/data/provenance.json`. ComCat changes when USGS revises events. A new download can give slightly different numbers, so we archived the exact bytes that we used.

## Methods

**Mainshocks.** ComCat events with M >= 6.0 (preferred magnitude) from 1980 to 2026. We removed an event if an earlier event of equal or larger magnitude occurred in the previous 365 days within the larger of the two aftershock radii. We also removed an event if an equal or larger event occurred in the next 30 days inside its radius (foreshock or doublet; 239 events; kept in one sensitivity test). The aftershock radius is R = max(50 km, 2 L), with L the Wells and Coppersmith (1994) subsurface rupture length, log10 L = -2.44 + 0.59 M. The primary sample has 3,486 mainshocks with depth of 70 km or less and a closed 10-day window.

**Outcome.** N10 = number of ComCat M4.5+ events in (0, 10] days within R.

**Covariates.** (a) Magnitude (M - 6). (b) Year, linear, to absorb network changes. (c) ln(depth + 5 km). (d) GCMT mechanism class from P, T and B plunges (thrust if T plunge >= 50 degrees; normal if P plunge >= 60; strike-slip if B plunge >= 60; other: oblique). We matched GCMT events within 120 s and 150 km (98.7% matched). (e) Background rate: ln((count of M4.5+ events within R in [-5 years, -30 days]) + 1) per year.

**Neighbour predictor.** For a new mainshock i, the neighbours are earlier mainshocks j in the analysis sample that satisfy three conditions: the 10-day window of j closed at least 365 days before i; the epicentral distance is D = 200 km or less; and the depths differ by 40 km or less. Each neighbour gives a residual r_j = ln((N_j + 0.5)/(mu_j + 0.5)), where mu_j comes from the magnitude-plus-year model fitted on the current training set. The predictor is z_i = sum(r_j) / (n_i + k) with k = 1 (shrinkage to zero for few neighbours). An indicator marks mainshocks with no neighbour. Only the observed counts of earlier sequences enter z_i. Thus z_i is known at the time of mainshock i.

**Forecast test.** We used NB2 negative-binomial regression (statsmodels, maximum likelihood). For each test year Y from 2000 to 2026, we fit every model on sequences whose window closed before 1 January Y. Then we computed the predictive log-likelihood of each test sequence in year Y. We report the mean gain in nats per test sequence. We give two 95% intervals: a bootstrap over sequences (2,000 resamples) and a bootstrap over test years (blocks). The model "full-nb" contains magnitude, year, depth, mechanism and background. The model "full" adds the neighbour term.

**Sensitivity variants** (all in `files/results/summary_all.json`). Outcome M5+ (`outcome_M5`). Events after the first 0.25 days only (`outcome_late`). Threshold of M_main - 2 (`outcome_rel`). Radius L + 30 km (`outcome_altR`). 30-day and 1-day windows. D of 100, 400 and 800 km. A gap of 30 days instead of 365. k of 0.5 and 3. All depths with a depth covariate. Test years 2010-2026 only. Foreshock events kept. Detection proxy ln((n(M4.5-4.9)+1)/(n(M5+)+1)) within 300 km over the previous 5 years added to all models (`det_control`). GCMT Mw in place of ComCat magnitude (`gcmt_mag`). Neighbour residuals from M4.5+ counts used to forecast M5+ counts (`cross_z45_yM5`). Local (100 km) and regional (1,000 km) terms together (`local100_vs_reg1000*`).

## Results table

Gain of the neighbour term beyond depth, mechanism and background (nats per test sequence, model "full" minus "full-nb"):

| Variant | n test | Gain | 95% CI (sequences) | 95% CI (years) | Years > 0 | Calibration slope |
| --- | --- | --- | --- | --- | --- | --- |
| primary | 1992 | 0.049 | 0.032 to 0.066 | 0.034 to 0.063 | 26/27 | 0.87 |
| outcome M5+ | 1992 | 0.014 | 0.006 to 0.022 | 0.007 to 0.022 | 21/27 | 0.64 |
| after first 0.25 d | 1992 | 0.037 | 0.023 to 0.051 | 0.022 to 0.051 | 24/27 | 0.86 |
| threshold M_main - 2 | 1992 | 0.042 | 0.027 to 0.057 | 0.029 to 0.056 | 24/27 | 0.81 |
| 30-day window | 1986 | 0.051 | 0.032 to 0.070 | 0.033 to 0.066 | 26/27 | 0.86 |
| D = 100 km | 1992 | 0.044 | 0.032 to 0.056 | 0.035 to 0.052 | 27/27 | 0.82 |
| D = 800 km | 1992 | 0.061 | 0.045 to 0.077 | 0.051 to 0.074 | 26/27 | 0.99 |
| all depths | 2682 | 0.054 | 0.040 to 0.068 | 0.043 to 0.065 | 26/27 | 0.88 |
| test 2010-2026 | 1160 | 0.056 | 0.032 to 0.080 | 0.034 to 0.073 | 16/17 | 0.95 |
| detection proxy control | 1992 | 0.034 | 0.020 to 0.047 | 0.019 to 0.049 | 23/27 | 0.77 |
| GCMT Mw | 1970 | 0.050 | 0.034 to 0.065 | 0.035 to 0.064 | 26/27 | 0.86 |
| M4.5 residuals forecast M5+ counts | 1992 | 0.022 | 0.013 to 0.032 | 0.014 to 0.032 | 23/27 | 0.47 |

Regional and local scale (primary outcome): the 1,000 km term beyond full-nb gave 0.062 (0.045 to 0.078). The 100 km term beyond that gave 0.013 (0.006 to 0.022). With the detection proxy, the values were 0.038 and 0.013 (0.006 to 0.021). For M5+ counts, the values were 0.026 and 0.0045 (-0.0003 to 0.0093).

Sanity check: the fitted magnitude coefficient was 2.33 per magnitude unit in natural-log units (1.01 in log10). This agrees with the usual productivity exponent of about 1. The fitted year trend was +0.25 per decade, which is consistent with improved detection over time. The NB dispersion was about 1.4 to 1.8.

## Interpretation

Aftershock productivity of M6+ mainshocks has a persistent spatial component. This component is larger than the effects of depth, mechanism class and background rate. Its correlation scale is hundreds of kilometres, and it does not decrease over 1 to 47 years. Thus a forecaster can use the residuals of past sequences in a region to update the generic productivity before the new sequence starts. A shrunken mean with k = 1 is well calibrated without tuning. The map shows that productivity is high on the continental collision belt and low on oceanic ridges and transforms. This agrees with the low productivity of oceanic transform faults reported by Boettcher and Jordan (2004), and with the factor-of-10 regional range in Page et al. (2016). Our test does not identify the physical cause. Candidate causes are crustal type, heat flow, fault maturity and fault-network complexity.

## Limitations

- **Catalog heterogeneity.** M4.5 is near the global completeness limit in some regions, and mb and Mw scales differ by region. These differences persist in space and time and can produce the same pattern. Our controls (detection proxy, M5+ outcome, GCMT Mw) reduce the gain by about one third to two thirds but do not remove it. They do not fully remove this possible cause, especially for the local 100 km component.
- **Short-term incompleteness.** M4.5 events are missed in the first hours after large mainshocks. Removing the first 0.25 days decreased the gain to 0.037 but did not remove it.
- **Simple sequence definitions.** We used fixed radii, epicentral distances and simple windows. We did not use ETAS declustering. Secondary sequences inside a 10-day window count as aftershocks.
- **Effect size.** The gain (about 0.05 nats per sequence) is moderate. Single-sequence counts remain highly dispersed (NB alpha about 1.4).
- **Calibration of totals.** Model "full" is calibrated on the log scale. However, in every forecast quintile the summed observed counts are lower than the summed predicted counts (ratio 0.69 to 0.94). A small number of very large sequences dominate these sums.
- We did not compare directly with the published regional parameters of Page et al. (2016). The 1,000 km neighbour mean is a data-driven proxy for such regionalization.

## Reproduce

Run from the publication root with Python 3.12 and the package versions in `files/code/environment.txt`:

```sh
mkdir -p scratch/raw
# put jan76_dec20.ndk in scratch/raw/ and unpack the GCMT monthly tar from sci:sha256:7184e3ca... into scratch/raw/gcmt_monthly/
W=scratch NDK20=scratch/raw/jan76_dec20.ndk MONTHLY=scratch/raw/gcmt_monthly sh files/code/run_all.sh
```

The full run takes less than 2 minutes on one CPU thread. We ran it again from the packaged inputs, and it reproduced the sequence table byte for byte and all summary numbers (`files/results/run_all.log`).

Files:

- `files/code/01_build.py`: catalog, mainshock selection, counts, GCMT matching.
- `files/code/02_forecast.py`: rolling forecasts, all variants, bootstrap intervals.
- `files/code/03_figures.py`: pair correlations, calibration, figures.
- `files/data/derived/sequences.csv.gz`: all 4,911 candidate M6+ mainshocks with counts and covariates.
- `files/data/derived/analysis_sample_primary.csv.gz`: primary sample.
- `files/results/preds_<variant>.csv.gz`: per-test-sequence forecasts and log-likelihoods.
- `files/results/summary_all.json`: all gains and intervals. `coefs_*.csv`: fitted coefficients per fold. `pair_corr_*.csv`, `calibration_quintiles.csv`, `descriptive.json`.

## References

- Page, M. T., van der Elst, N., Hardebeck, J., Felzer, K., Michael, A. J. (2016). Three ingredients for improved global aftershock forecasts. BSSA 106(5).
- Wells, D. L., Coppersmith, K. J. (1994). New empirical relationships among magnitude, rupture length, rupture width, rupture area, and surface displacement. BSSA 84(4).
- Ekstrom, G., Nettles, M., Dziewonski, A. M. (2012). The global CMT project 2004-2010. PEPI 200-201.
- Boettcher, M. S., Jordan, T. H. (2004). Earthquake scaling relations for mid-ocean ridge transform faults. JGR 109.
- Frohlich, C. (1992). Triangle diagrams: ternary graphs to display similarity and diversity of earthquake focal mechanisms. PEPI 75.
- Gomberg, J., Bodin, P. (2021). The productivity of Cascadia aftershock sequences. BSSA.
- Campaign publications: GCMT monthly files from sci:sha256:7184e3ca8e705c7f1821efa1d5a15e4c4783218097677a59a269fcc8859179c1. Related campaign aftershock studies: sci:sha256:c8ed26f5ca7d7484640ca25e043981deb520e2765f0781dd79a3ae3aac4c72ce (decay exponents after large earthquakes) and sci:sha256:676a196eb53efb08dfc0c7c7cd83b6cc1a396a2ba320512b5f840eb4e8382a90 (Ridgecrest decay forecast).
