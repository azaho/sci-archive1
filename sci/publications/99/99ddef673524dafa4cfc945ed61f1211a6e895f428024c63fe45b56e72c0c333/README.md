# Omori, cutoff and rate-state decay fits to 2011-2018 gave similar 2019-2024 errors in 22 Tohoku-activated cells (JMA M3.5+, depth 60 km or less); no tail shape was clearly better

## Summary

**Question.** After the 2011 Mw 9.0 Tohoku-Oki earthquake, the shape of the late aftershock tail controls how long seismic hazard stays high. A power-law (Omori-Utsu) tail continues slowly for decades. The rate-and-state model of Dieterich (1994) gives an exponential end at a finite time *t_a*. Toda and Stein (2022) also showed that the rate stops ("central shutdown") on the high-slip area and stays high around it. We asked: do these tail shapes give different forecasts that 13 years of data can separate?

**Method.** We used the JMA unified hypocenter catalog (1998-2024) in 1 x 1 degree cells at 34-42 N, 138-146 E, depth 60 km or less, M 3.5 or more. For each cell, the 1998-01-01 to 2011-03-11 rate is the old baseline *r*. We fitted five decay models to the counts from day 10 to 2018-12-31, by Poisson maximum likelihood on log-spaced bins. Then we used each fit to forecast the 2019-2024 count in each cell. We did not use these years in the fit. We compared the forecasts with two reference forecasts: the old baseline only, and "the last three years continue". The main test set is the 22 "activated" cells, where the rate in days 10-365 was 5 or more times the old baseline.

| Code | Model (rate R(t), t in days after the mainshock) | Free parameters |
| --- | --- | --- |
| OB | R = r + K (t + c)^-p (Omori-Utsu decay to the old baseline) | K, p, c |
| OBX | R = r + K (t + c)^-p exp(-t/tau) (Omori-Utsu with exponential cutoff) | K, p, c, tau |
| RS | R = r / (1 - (1 - 1/J) exp(-t/t_a)) (Dieterich 1994, one stress step) | J, t_a |
| OBN | as OB, but the decay goes to a free new level r' | K, p, c, r' |
| RSN | as RS, but toward a free new level r' (changed stressing rate) | J, t_a, r' |
| BG | R = r (old baseline only) | none |
| PERS | rate of the last 3 fit years continues | none |

**Main result.** In the 22 activated cells, the mean absolute log error of the 2019-2024 count was 0.45 (OB), 0.39 (OBX), 0.48 (RS), 0.44 (OBN), 0.45 (RSN), 0.56 (BG) and 0.52 (PERS). The tested paired differences between decay models (RS-OB, OBX-OB, OBN-OB, RSN-RS, RSN-OBN) all had 95% block-bootstrap intervals that included zero. The rate-state minus Omori difference was +0.03 [-0.08, +0.16]. Its interval included zero in all six analysis variants, for activated cells and for all cells (Table 2). The exponential cutoff (OBX) gave the smallest error in most variants, but its gain over OB was small (0.01-0.07). It was clear only when we removed M 6.5+ aftershock windows.

**Other results.**
1. *Training fit shape.* By AIC (difference > 2), Omori-Utsu (OB) was better than one-step rate-state (RS) in 16 of 22 activated cells. RS was better in 4. An exponential cutoff improved the Omori fit in 7 of 22 cells (cutoff times of 111 to 3,670 days). The median Omori exponent p was 1.10 (interquartile range 0.99-1.29).
2. *Bias.* All five decay models forecast too many events in 2019-2024. The mean log bias was -0.20 to -0.35 (primary, activated cells; for example OB -0.35 [-0.58, -0.11]). The old baseline forecast too few (+0.20 [-0.05, +0.53]). Thus the true 2019-2024 rate was between the decay forecasts and the old baseline.
3. *Decay models against the old baseline.* The Omori forecast was better than the old baseline in the median-baseline, M3.0 and masked variants (for example -0.42 [-0.73, -0.17] with the median baseline). In the primary variant the gain (-0.11 [-0.35, +0.16]) was not clear.
4. *Persistence.* "The last three years continue" was clearly worse than the Omori forecast in four of six variants (activated cells). With a fit to 2015 and a 2016-2024 test, it was worse by +0.30 [+0.17, +0.42]. The rate continued to decrease.
5. *A free new level did not help.* In the training data, a free new level (OBN or RSN) improved the fit (AIC difference > 2) in 10 to 14 of 22 activated cells. The median new level was 0.75 times the old baseline. But the free level did not reduce the held-out error. With a fit to 2015, it made the error larger (OBN - OB = +0.13 [-0.02, +0.28]; RSN - RS = +0.12 [+0.00, +0.29]).
6. *Status in 2022-2024.* In the 22 activated cells, the total 2022-2024 rate was 1.65 times the old mean baseline (2.03 times the median baseline). By a Poisson 95% interval, 8 cells were above their old baseline, 5 were below and 9 were not different. The rate in the cell at 38.5 N, 143.5 E, in the high-slip area east of the epicenter, was 0.04 times its old baseline. This agrees with the "central shutdown" of Toda and Stein (2022). None of the fixed-baseline models can show a rate below the old baseline at late times. This cell gave one of the largest forecast errors (9 observed against 104-111 forecast).
7. *The largest under-forecast* was at 37.5 N, 141.5 E (976 observed, 352-558 forecast by OB/OBX/RS). This cell contains the 2021-02-13 M7.3 and 2022-03-16 M7.4 Fukushima-oki intraslab earthquakes and their aftershocks. A decay model of one sequence cannot forecast these new large events.

**Interpretation.** In this catalog, 8 years of post-mainshock data were not sufficient to separate a power-law tail from an exponential (rate-state) tail by the forecast skill 8-14 years after the mainshock. Single-cell differences were large, but they came mainly from two other effects: rates that went below the old baseline, and new large earthquakes. Neither effect is a property of the tail shape. The choice of the baseline (mean or median of 1998-2010) changed the forecast errors more than the choice of the tail shape. Hazard models that use the Tohoku sequence must thus model the baseline and the spatial pattern of shutdown carefully. A tail-shape choice by itself does not give a clear forecast gain at these times.

**Relation to two campaign results from the same day.** Two other campaign publications use the same JMA catalog. Thus they are not independent data. sci:sha256:331923fa... fitted regional Omori-ETAS models at M 4+. It found that the pre-2011 background with a slow Omori decay (p0 = 1.02) forecast 2017-2024 in the forearc outside the high-slip core, and that the core rate fell to 0.17 times its old rate. sci:sha256:1f13650d... found 0.09-0.18 times the old rate where the USGS-model slip was 20 m or more. Our cell-level results agree with both: Omori decay to the old baseline is a good forecast in most activated cells, and the cell at 38.5 N, 143.5 E is far below its old rate. Our new contribution is the cell-level test of tail shape (power law, exponential cutoff, rate-state, free new level) by held-out forecast error.

## Figures

- `files/figures/fig1_rate_ratio_maps.png`: rate relative to the 1998-2011 baseline, days 10-365 (A) and 2022-2024 (B), for each cell with data.
- `files/figures/fig2_rate_histories.png`: binned rates and the five fitted models in six cells, with the held-out years.
- `files/figures/fig3_heldout_errors.png`: per-cell held-out log errors (A) and mean absolute log errors with block-bootstrap 95% intervals across variants (B).

## Tables

**Table 1. Mean absolute held-out log error, ln((obs+1)/(forecast+1)), of the test-period count.** Lower is better. "activated" = rate in days 10-365 at least 5 times the baseline.

| Variant | Subset | n | OB | OBX | RS | OBN | RSN | BG | PERS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| primary | activated | 22 | 0.45 | 0.39 | 0.48 | 0.44 | 0.45 | 0.56 | 0.52 |
| primary | all | 34 | 0.52 | 0.50 | 0.41 | 0.43 | 0.49 | 0.62 | 0.49 |
| median baseline | activated | 23 | 0.32 | 0.27 | 0.39 | 0.45 | 0.47 | 0.74 | 0.52 |
| median baseline | all | 34 | 0.32 | 0.30 | 0.37 | 0.43 | 0.50 | 0.62 | 0.49 |
| M >= 3.0 | activated | 26 | 0.36 | 0.28 | 0.41 | 0.36 | 0.33 | 0.68 | 0.45 |
| M >= 3.0 | all | 45 | 0.55 | 0.51 | 0.40 | 0.33 | 0.33 | 0.74 | 0.40 |
| fit to 2015, test 2016-2024 | activated | 22 | 0.45 | 0.43 | 0.47 | 0.58 | 0.59 | 0.63 | 0.75 |
| fit to 2015, test 2016-2024 | all | 28 | 0.38 | 0.37 | 0.41 | 0.59 | 0.58 | 0.56 | 0.70 |
| M6.5 windows masked | activated | 5 | 0.13 | 0.12 | 0.16 | 0.20 | 0.28 | 0.30 | 0.32 |
| M6.5 windows masked | all | 25 | 0.32 | 0.29 | 0.22 | 0.31 | 0.39 | 0.55 | 0.40 |
| masked + median baseline | activated | 5 | 0.08 | 0.07 | 0.15 | 0.20 | 0.28 | 0.30 | 0.32 |
| masked + median baseline | all | 25 | 0.21 | 0.19 | 0.20 | 0.31 | 0.39 | 0.56 | 0.40 |

**Table 2. Paired differences in mean absolute log error (first model minus second), with 95% intervals from 4,000 bootstrap resamples of 2 x 2 degree cell blocks.** Negative = first model is better.

| Variant | Subset | RS-OB | OBX-OB | OBN-OB | RSN-RS | OB-BG | PERS-OB |
| --- | --- | --- | --- | --- | --- | --- | --- |
| primary | activated | +0.03 [-0.08, +0.16] | -0.05 [-0.15, +0.02] | -0.00 [-0.22, +0.23] | -0.02 [-0.12, +0.12] | -0.11 [-0.35, +0.16] | +0.08 [-0.12, +0.30] |
| primary | all | -0.11 [-0.36, +0.07] | -0.02 [-0.09, +0.04] | -0.09 [-0.32, +0.11] | +0.09 [-0.04, +0.20] | -0.10 [-0.29, +0.08] | -0.03 [-0.29, +0.18] |
| median baseline | activated | +0.07 [-0.03, +0.18] | -0.05 [-0.15, +0.03] | +0.13 [-0.02, +0.31] | +0.08 [-0.04, +0.22] | -0.42 [-0.73, -0.17] | +0.20 [+0.07, +0.38] |
| median baseline | all | +0.05 [-0.02, +0.13] | -0.01 [-0.10, +0.05] | +0.11 [-0.00, +0.24] | +0.12 [+0.02, +0.22] | -0.30 [-0.54, -0.10] | +0.17 [+0.06, +0.30] |
| M >= 3.0 | activated | +0.05 [-0.04, +0.16] | -0.07 [-0.15, +0.00] | +0.01 [-0.19, +0.22] | -0.08 [-0.18, +0.01] | -0.32 [-0.55, -0.13] | +0.10 [-0.05, +0.26] |
| M >= 3.0 | all | -0.15 [-0.34, +0.01] | -0.04 [-0.10, +0.00] | -0.22 [-0.43, -0.01] | -0.07 [-0.15, -0.00] | -0.19 [-0.33, -0.06] | -0.16 [-0.39, +0.06] |
| fit to 2015 | activated | +0.02 [-0.11, +0.15] | -0.02 [-0.07, +0.04] | +0.13 [-0.02, +0.28] | +0.12 [+0.00, +0.29] | -0.18 [-0.41, +0.05] | +0.30 [+0.17, +0.42] |
| fit to 2015 | all | +0.03 [-0.08, +0.13] | -0.01 [-0.05, +0.04] | +0.21 [+0.05, +0.39] | +0.17 [+0.03, +0.34] | -0.19 [-0.40, +0.01] | +0.32 [+0.21, +0.43] |
| masked | activated | +0.03 [-0.06, +0.13] | -0.01 [-0.03, -0.00] | +0.07 [-0.06, +0.16] | +0.11 [-0.08, +0.27] | -0.17 [-0.33, -0.01] | +0.19 [+0.05, +0.30] |
| masked | all | -0.10 [-0.31, +0.02] | -0.03 [-0.04, -0.01] | -0.00 [-0.23, +0.14] | +0.17 [+0.09, +0.24] | -0.23 [-0.47, -0.06] | +0.09 [-0.18, +0.22] |
| masked + median | activated | +0.07 [-0.02, +0.17] | -0.01 [-0.04, +0.01] | +0.12 [+0.04, +0.19] | +0.13 [-0.02, +0.27] | -0.22 [-0.40, -0.03] | +0.24 [+0.09, +0.39] |
| masked + median | all | -0.01 [-0.06, +0.05] | -0.01 [-0.02, -0.00] | +0.10 [+0.04, +0.19] | +0.19 [+0.11, +0.26] | -0.36 [-0.61, -0.18] | +0.20 [+0.11, +0.27] |

The full per-cell results, AIC counts, bias values and 2022-2024 status counts for each variant are in `files/results/summary.json`, `files/results/summary_table.csv` and `files/results/cells_<variant>.csv`.

## Methods in detail

- **Catalog.** JMA unified hypocenter bulletin files `h1998.zip` to `h2024.zip`. We kept only JMA ("J") records. Times are JST. Magnitude is the first magnitude field (mostly Mj, with some Mw/Md). The mainshock time is 2011-03-11 14:46:18.12 JST (catalog M 9.0). We parsed 4,932,674 J records. The study box has 31,543 events at M 3.5+ and 74,163 events at M 3.0+ (depth 60 km or less, 1998-2024).
- **Completeness.** In the study box, the maximum-curvature estimate of completeness for offshore events (east of 142 E) was 4.9 on day 0-1, 4.4 on days 1-3, 3.6 on days 3-10 and 2.7-2.8 from day 10 to day 1,000. Thus we used M 3.5+ from day 10 as the primary choice. The M 3.0+ variant is a check. The annual M 3.0+ counts in south-west Japan are stable from 1998 to 2024, except during known sequences (2005 Fukuoka, 2016 Kumamoto). Thus we did not find a magnitude-scale step at M 3.0+. (The large rise of small events after 2016 is below M 2.5.)
- **Cells.** We used 1 x 1 degree cells. A cell was used if it had 10 or more baseline events, 3 or more years of baseline exposure, and 30 or more events in the fit period. The box starts at 138 E. Thus the 2024 Noto M7.6 sequence (about 137.3 E) is outside it.
- **Fitting.** We used 24 log-spaced bins from day 10 to 2018-12-31 (day 2,852), Poisson likelihood, and L-BFGS-B from a set of start points with one Nelder-Mead polish. We started the nested models (OBX, OBN, RSN) from the optimum of their simpler model. Thus their fit cannot be worse. We integrated the rates over days with 15-day nodes. The baseline r is fixed (not fitted) in OB, OBX and RS.
- **Held-out scoring.** We used the yearly counts for 2019-2024 (the 2016-2024 counts for the "fit to 2015" variant), summed per cell, and the error ln((obs+1)/(forecast+1)). We used block bootstrap over 2 x 2 degree blocks of cells (4,000 resamples, seed 20111311) because nearby cells are not independent.
- **Variants.** (a) median baseline: median of the yearly 1998-2010 rates, which is less sensitive to earlier sequences (2003 Tokachi-oki, 2005 and 2008 Miyagi/Ibaraki-oki, 2008 Iwate-Miyagi). (b) M 3.0+. (c) fit to 2015-12-31 and test 2016-2024. (d) mask: we removed the days within 365 days and within the Gardner-Knopoff distance of each M 6.5+ event (except the mainshock day) from the baseline, fit and test exposure. In the rupture area this removes most of the first year. Thus only 5 cells stay "activated" in the masked variants, and the "all" subset is more informative there.
- **Rate-state t_a and baseline.** For cells with J > 3, the fitted rate-state t_a had a median of 3,150 days (8.6 years, primary). log10 t_a against log10 r had a slope of -0.17 +- 0.18 (primary) and -0.59 +- 0.12 (median baseline). These values are shallower than -1. A slope of -1 would follow if the stressing rate is proportional to the baseline rate in the Dieterich model. But t_a and r are coupled in the fit, and r has sampling error. Thus we do not use this slope as a test.

## Limitations

- **Small and dependent sample.** There are only 22 activated cells, and nearby cells share sequences. The block bootstrap is approximate. The intervals are wide (about +-0.1 to +-0.3 log units). Thus differences smaller than about 0.1 log units cannot be found.
- **Overdispersion.** Poisson likelihood ignores aftershock clustering. Thus the AIC counts are too confident. We use them only as a description of fit shape, not as a test.
- **Secondary sequences.** The decay models describe one cascade. New M 7+ events in 2021-2022 are part of the test period. Masking removes them, but it also removes much of the near-field data.
- **Baseline.** The 1998-2011 baseline contains earlier M 6.5-8.0 sequences and the 2000 Izu swarm. The cell at 34.5 N, 139.5 E has a baseline that the 2000 Izu swarm controls, so its ratios are near 0. The choice of the baseline changed the errors more than the tail shape did.
- **Catalog.** We used one catalog (JMA), one magnitude field and fixed cells. There is no depth separation inside 0-60 km (interface, crustal and shallow intraslab events are mixed). We did not use Coulomb stress models. Thus this study cannot attribute shutdown or activation to a stress change.
- **Horizon.** The test covers 8-14 years after the mainshock. Toda and Stein (2022) suggest decades of surrounding activity. Tails that are different at 30-60 years can look the same at 8-14 years.

## Reproduce

From the worktree root that contains `datasets/` (shared campaign datasets) and this draft at `work/result/`:

```
bash work/result/files/code/00_run_all.sh
```

Steps: `01_parse_jma.py` (parse the 27 JMA zip files into `work/scratch/jma_1998_2024.parquet`), `02_tail_models.py` (six variants; about 20 min each on a loaded 8-core machine; set `NPROC` for worker processes), `03_evaluate.py` (scores, bootstrap, tables), `04_figures.py` (PNG figures), `05_export_events.py` (event subset). Software: Python 3.12.15, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, matplotlib 3.11.2, geopandas 1.2.0.

To get the data without the campaign store, download `https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/hYYYY.zip` for YYYY = 1998-2024 and `https://naciscdn.org/naturalearth/10m/physical/ne_10m_land.zip`. Then put each file at `datasets/jma-hypocenter-hYYYY-20261109/hYYYY.zip` and `datasets/naturalearth-10m-land-v5/ne_10m_land.zip`, each with a `provenance.json` that gives `filename`. JMA can revise these files. Compare the SHA-256 values in `files/data_provenance.json`.

## Files

- `files/code/`: all analysis code (00-05).
- `files/data/jma_events_34-42N_138-146E_d60_m3.csv.gz`: the 74,163 JMA events used (M 3.0+, depth 60 km or less, study box, 1998-2024; time JST). SHA-256 43d8f479920752aa818e4085544306efed34ab26874378134fda6b08ccfa9493.
- `files/data_provenance.json`: shared dataset paths, source URLs, SHA-256 and byte counts for the 27 JMA zip files and the Natural Earth land file (all checked against the stored provenance before use).
- `files/results/runs/<variant>/`: `run.json` (settings, masked events, bin edges) and `cells.csv` (per-cell parameters, fit likelihoods, yearly observed and forecast counts). `runs/primary/curves.json` has the binned rates and fitted curves for Figure 2.
- `files/results/cells_<variant>.csv`, `summary.json`, `summary_table.csv`, `forecast_errors_long.csv`: evaluation outputs.
- `files/figures/`: the three PNG figures.

## Provenance and attribution

- Campaign 11_07_2026, job `sci-1107-hp-earth-and-ocean-sciences-d12f4587475e`, topic earth-and-ocean-sciences, machine `hp`, account claude-andrii. The analysis and text were made by the AI model Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Data: Japan Meteorological Agency, unified hypocenter catalog (seismic bulletin), downloaded 2026-11-09 to the shared campaign dataset store (paths and hashes in `files/data_provenance.json`). Natural Earth 10 m land v5 (public domain), used only for map outlines.
- Prior work: Toda, S. and Stein, R. S. (2022), Central shutdown and surrounding activation of aftershocks from megathrust earthquake stress transfer, Nature Geoscience 15, 494-500 (doi:10.1038/s41561-022-00955-w). Dieterich, J. (1994), A constitutive law for rate of earthquake production and its application to earthquake clustering, JGR 99, 2601-2618 (doi:10.1029/93JB02581). Utsu, T., Ogata, Y. and Matsu'ura, R. S. (1995), The centenary of the Omori formula for a decay law of aftershock activity, J. Phys. Earth 43, 1-33 (doi:10.4294/jpe1952.43.1). Earlier studies, for example Mignan, A. (2015, Geophysical Research Letters), tested cutoff or stretched-exponential tails in single sequences. Related campaign results: a global study of aftershock duration against strain rate (sci:sha256:a665789acaf5...) the Tohoku tide-gauge recovery study (sci:sha256:0d84d0dce76b...) and the two results above. All are cited in sci.json.
