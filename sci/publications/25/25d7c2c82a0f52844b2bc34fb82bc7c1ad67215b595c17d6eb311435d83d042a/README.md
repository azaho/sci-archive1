# Omori decay exponent p did not increase with surface heat flow in California, Japan or global aftershock sequences; Japan and global samples showed a decrease

**Job:** sci-1107-dell-earth-and-ocean-sciences-1ee63e7587eb · **Topic:** earth-and-ocean-sciences · **Machine:** dell · **Campaign:** 11_07_2026 · **Model:** Claude Opus 5.5 (claude-opus-5-5) in Claude Code · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Kisslinger and Jones (1991) reported that aftershock rates decay faster (higher Omori p) where surface heat flow is high, in 39 southern California sequences. Damage-rheology models (Ben-Zion and Lyakhovsky 2006) predict the same direction, and also fewer aftershocks at high heat flow. Later studies disagree on productivity (Yang and Ben-Zion 2009 and Enescu et al. 2009: lower at high heat flow; Nandan et al. 2017: higher). We tested both predictions in three independent samples with the new IHFC Global Heat Flow Database (release 2024, version 2026.03):

* California-Nevada, USGS ComCat, mainshocks M4.0 or larger, 1986-2025: 501 sequences, 17,318 aftershocks.
* Japan, JMA unified catalog, mainshocks M4.5 or larger, 2000-2024: 176 sequences, 4,133 aftershocks.
* Global, ComCat, shallow mainshocks M6.5 or larger, 1995-2025: 158 sequences, 3,594 aftershocks.

We fit lambda(t) = mu + K t^-p to each sequence. The background rate mu came from the 5 years before the mainshock. A pooled likelihood let p change linearly with log10 of the local median heat flow, with controls for magnitude, depth and year. We used a cluster bootstrap over spatial cells for the 95% intervals. We fixed the plan before the first heat-flow fit (`files/analysis_plan.md`).

**Main result.** The change in p per tenfold increase in heat flow was:

| Sample | Slope of p on log10(heat flow) | 95% cluster-bootstrap interval | Decision for H1 (slope > 0) |
| --- | --- | --- | --- |
| California-Nevada | +0.14 | -0.23 to +0.43 | not supported (interval includes 0) |
| Japan | -0.59 | -0.88 to -0.09 | not supported; opposite sign |
| Global M6.5+ | -0.29 | -0.43 to -0.04 | not supported; opposite sign |

The three slopes are not the same (Cochran Q = 8.2, p = 0.016). The random-effects mean is -0.24 (-0.60 to +0.11). Thus these data do not support a general rule that aftershocks decay faster in hot crust. In Japan and in the global sample, the decay was slower where heat flow was higher.

**Productivity** (aftershocks above background, per unit Omori integral) also did not change in one common direction. Per tenfold heat flow, it changed by a factor of 1.9 (0.5 to 6.9) in California-Nevada, 4.1 (1.9 to 9.1) in Japan and 0.42 (0.21 to 0.84) globally.

**Main limitations.** The negative slope in Japan depends on the background term. It disappears when the background is set to zero (+0.12, -0.31 to +0.61). It stays when we keep only sequences with a small background (-0.69, -1.07 to +0.07), and outside the 2011-2020 Tohoku zone (-0.65, -1.27 to -0.15). The global slope weakens with a low-background subset (-0.14, -0.28 to +0.14) or with a 200 km heat-flow radius (-0.15, -0.28 to +0.05). At these scales, heat flow is also a marker of tectonic setting (forearc, arc, rift, ridge). Thus this study cannot isolate a temperature effect.

## Figures

* `files/figures/fig1_map.png`: analysed mainshocks, colored by local median heat flow, on the heat-flow sites.
* `files/figures/fig2_p_by_heatflow.png`: top, pooled p in heat-flow terciles; bottom, stacked rate above background for each tercile.
* `files/figures/fig3_robustness.png`: slope of p and of ln(productivity) on log10(heat flow) for all settings.

## Question and prior work

* Kisslinger, C. and Jones, L. M. (1991), J. Geophys. Res. 96(B7), 11947-11958, doi:10.1029/91JB01200. They found high p in the Salton Trough (high heat flow) and low p in low-heat-flow areas of southern California.
* Ben-Zion, Y. and Lyakhovsky, V. (2006), Geophys. J. Int. 165, 197-210. Damage rheology predicts faster decay and fewer aftershocks in hotter, more viscous crust.
* Yang, W. and Ben-Zion, Y. (2009), Geophys. J. Int. 177, 481-491, doi:10.1111/j.1365-246X.2009.04145.x. Stacked southern California productivity decreased with heat flow.
* Enescu, B., Hainzl, S. and Ben-Zion, Y. (2009), Bull. Seismol. Soc. Am. 99. The ETAS alpha exponent was smaller at high heat flow.
* Nandan, S. et al. (2017), arXiv:1706.08922. California ETAS fits gave higher productivity at high heat flow.
* Marsan and Bean (as described by Ouillon and Sornette 2005, J. Geophys. Res. 110, B04306) reported a positive p-heat-flow relation in nine global subregions.

Earlier campaign work studied aftershock productivity persistence (sci:sha256:2182948c...), decay start times (sci:sha256:c8ed26f5...) and time to background against strain rate (sci:sha256:a665789a...). None of them used heat flow.

Pre-set hypotheses:
* H1: the slope of p on log10(heat flow) is positive in each sample.
* H2: productivity decreases with heat flow.

## Data

| Input | Source and version | Use |
| --- | --- | --- |
| Heat flow | IHFC Global Heat Flow Database, Release 2024, v2026.03 (GFZ Data Services, doi:10.5880/fidgeo.2024.014, CC BY 4.0). Shared dataset `datasets/ihfc-ghfdb-r2024-v202603-gfz`, ZIP SHA-256 3442369a... | 70,383 parent sites with 0 < q <= 1000 mW/m2 |
| California-Nevada catalog | USGS ComCat FDSN, box 30-43 N, 127-113 W, M >= 2.0, 1981-2026-11-09 (252,697 events) | Archived in `files/data/raw/comcat_ca_m2.0_1981_2026.tar.gz` |
| Japan catalog | JMA unified hypocenter files h1998-h2024, natural events (subinfo 1), 4,597,609 events | Shared datasets `datasets/jma-hypocenter-hYYYY-20261109` (staged by this job); hashes in `files/data/provenance_inputs.json` |
| Global catalog | ComCat M >= 4.5, 1973-2026, exact bytes reused from sci:sha256:2182948c... (294,099 events) | Hashes in `files/data/provenance_inputs.json` |
| Volcanoes | Smithsonian GVP Holocene volcanoes (shared dataset `datasets/gvp-votw-holocene-volcanoes-wfs-20261109`) | Exploratory control only |

## Method

**Mainshocks.** California-Nevada: M >= 4.0, depth <= 25 km, inside 31.5-42.5 N and 125.5-114 W, 1986-2025. Japan: M >= 4.5, depth <= 30 km, inside 30-46 N and 128-147 E, 2000-2024. Global: M >= 6.5, depth <= 40 km, 1995-2025. An event is not a mainshock if an event of equal or larger magnitude occurred in the 365 days before, within max(r_i, r_j). Here r = max(r_min, 2 L) and L is the Wells and Coppersmith (1994) rupture length (r_min = 10 km for CA and JP, 30 km for GL). A later event of equal or larger magnitude inside r ends the window. We removed sequences whose window became shorter than 10 days.

**Aftershocks.** Events inside r, at depth <= mainshock depth limit + 30 km, with M >= max(Mc, Mm - 3), with Mc = 2.0 (CA, JP) and 4.5 (GL). The fit window is t1 to 100 days, with t1 = 0.1 day (CA, JP) or 0.5 day (GL). This avoids most of the short-term incompleteness after the mainshock.

**Background.** mu is the median of the yearly counts (same zone and cutoff) in the 5 years before t0 - 30 days, divided by 365.25. The median is robust to one earlier sequence in the zone. Settings `bg_mean` and `bg_zero` replace it with the 5-year mean or with zero.

**Heat flow.** The median q of all GHFDB parent sites within 50 km (CA, JP) or 100 km (GL) of the epicentre, if there are at least 3 sites. The variable z = log10(q / 60 mW/m2).

**Model.** For sequence i, lambda_i(t) = mu_i + K_i t^-p_i on [t1, T2_i], with mu_i fixed. The pooled model sets p_i = a + beta z_i + controls (model B: magnitude, depth, year; model A: none; model C: also log background rate). Each K_i is free. We profile the K_i out with a Newton solver that is vectorized over sequences, and we maximize over the p coefficients with L-BFGS. A synthetic test (`files/code/test_pooled.py`, 200 sequences, true slope 0.20) gave 0.197 (0.187 to 0.207). Sequences with at least 5 events enter the fit. A capped variant gives each sequence weight min(1, 50 / n_i), so that a few large sequences cannot control the result.

**Uncertainty.** Profile-likelihood intervals assume that all sequences share one p for a given heat flow. Individual p values have extra scatter (tau^2 = 0.04-0.08), so profile intervals are too narrow. Our decision intervals come from a cluster bootstrap. We resampled 1-degree cells (CA, JP) or 5-degree cells (GL), with 200 replicates for the main fits and 60-100 for the other settings. A second estimator is a random-effects (DerSimonian-Laird) meta-regression of individual p values (sequences with n >= 10), with cluster-robust standard errors.

**Productivity (H2).** Negative binomial GLM of the count above background, round(n - mu (T2 - t1)), with offset log of the Omori integral at the region p. Covariates are z, magnitude, Mm - cutoff, depth and year. The standard errors are cluster-robust by cell.

## Results

### Sample

| Sample | Candidates | Removed (earlier larger event) | Kept | With heat flow and >= 5 events | Events | Cells |
| --- | --- | --- | --- | --- | --- | --- |
| California-Nevada | 2,340 | 1,315 | 965 | 501 | 17,318 | 56 |
| Japan | 2,939 | 2,218 | 648 | 176 | 4,133 | 60 |
| Global M6.5+ | 978 | 253 | 703 | 158 | 3,594 | 80 |

In Japan, most kept sequences are offshore and have no heat-flow site within 50 km. The 176 analysed sequences have median heat flow 59 mW/m2 (10-90%: 32-115). The values are 83 (57-184) in California-Nevada and 54 (29-93) globally.

### Pooled p by heat-flow tercile

| Sample | Tercile | Heat flow range (median), mW/m2 | Sequences | Events | Pooled p | Capped p | Largest sequence share |
| --- | --- | --- | --- | --- | --- | --- | --- |
| CA | 1 | 30-74 (59) | 176 | 4179 | 0.92 | 0.95 | 0.08 |
| CA | 2 | 74-115 (83) | 158 | 4972 | 0.78 | 0.85 | 0.13 |
| CA | 3 | 117-400 (159) | 167 | 8167 | 0.92 | 0.94 | 0.05 |
| JP | 1 | 20-44 (34) | 59 | 1068 | 1.10 | 1.09 | 0.16 |
| JP | 2 | 45-79 (59) | 58 | 1588 | 1.07 | 1.02 | 0.11 |
| JP | 3 | 80-282 (103) | 59 | 1477 | 0.81 | 0.89 | 0.20 |
| GL | 1 | 10-44 (33) | 54 | 1653 | 1.14 | 1.14 | 0.11 |
| GL | 2 | 45-64 (54) | 51 | 970 | 1.06 | 1.06 | 0.08 |
| GL | 3 | 65-206 (83) | 53 | 971 | 1.06 | 1.08 | 0.13 |

In California-Nevada, p is not monotonic in heat flow: the middle tercile has the lowest p. In Japan, the high-heat-flow tercile (80-282 mW/m2, mostly the volcanic arc and back-arc crust) has p = 0.81, against 1.10 in the low tercile (mostly the forearc, many of them in the Tohoku region). Globally, the low tercile has the highest p (1.14).

### Slope of p on log10(heat flow)

| Sample | Model B pooled (bootstrap 95%) | Capped likelihood (bootstrap 95%) | Meta-regression of individual p (95%) | p at 60 mW/m2 (model A) |
| --- | --- | --- | --- | --- |
| California-Nevada | +0.14 (-0.23, +0.43) | +0.06 (-0.18, +0.30) | +0.03 (-0.20, +0.26), n = 317 | 0.85 |
| Japan | -0.59 (-0.88, -0.09) | -0.40 (-0.71, -0.06) | -0.43 (-0.75, -0.11), n = 96 | 0.99 |
| Global M6.5+ | -0.29 (-0.43, -0.04) | -0.27 (-0.43, -0.02) | -0.29 (-0.50, -0.08), n = 103 | 1.07 |

The profile-likelihood interval for California-Nevada (+0.08 to +0.19) excludes zero. The bootstrap interval does not. The difference comes from the between-sequence scatter of p. Thus we use the bootstrap interval for the decision.

### Productivity

| Sample | ln(productivity) per log10(heat flow) | Factor per tenfold heat flow (95%) |
| --- | --- | --- |
| California-Nevada | +0.66 | 1.9 (0.5 to 6.9) |
| Japan | +1.42 | 4.1 (1.9 to 9.1) |
| Global M6.5+ | -0.87 | 0.42 (0.21 to 0.84) |

H2 (fewer aftershocks at high heat flow) holds only in the global sample. Japan shows the opposite sign.

### Robustness

All rows use model B. Intervals are cluster-bootstrap 95% intervals, except where marked "profile". "expl." marks exploratory checks that were not in the fixed plan. They were added after we saw the main result.

| Setting | California-Nevada | Japan | Global M6.5+ |
| --- | --- | --- | --- |
| main | +0.14 [-0.23, +0.43], n=501 | -0.59 [-0.88, -0.09], n=176 | -0.29 [-0.43, -0.04], n=158 |
| capped likelihood (50 ev.) | +0.06 [-0.18, +0.30], n=501 | -0.40 [-0.71, -0.06], n=176 | -0.27 [-0.43, -0.02], n=158 |
| model C (+background) | +0.15 [+0.09, +0.21] (profile), n=501 | -0.53 [-0.66, -0.40] (profile), n=176 | -0.29 [-0.40, -0.17] (profile), n=158 |
| hf radius x0.5 | +0.27 [-0.32, +0.43], n=308 | -0.79 [-1.25, -0.34], n=64 | -0.33 [-0.83, -0.00], n=47 |
| hf radius x2 | -0.17 [-0.57, +0.19], n=523 | -0.82 [-1.18, -0.48], n=268 | -0.15 [-0.28, +0.05], n=315 |
| no geothermal hf sites | +0.17 [-0.22, +0.59], n=486 | -0.49 [-0.85, -0.12], n=166 | -0.27 [-0.47, -0.03], n=156 |
| Mc+0.5 | +0.17 [-0.12, +0.57], n=300 | -0.57 [-0.85, -0.17], n=117 | -0.59 [-0.81, -0.04], n=70 |
| Mmin+0.5 | +0.11 [-0.31, +0.47], n=199 | -0.63 [-1.24, -0.07], n=88 | -0.29 [-0.46, -0.00], n=78 |
| bg_mean | +0.13 [-0.26, +0.48], n=501 | -0.60 [-0.87, -0.18], n=176 | -0.32 [-0.48, -0.06], n=158 |
| bg_zero | -0.12 [-0.60, +0.50], n=501 | +0.12 [-0.31, +0.61], n=176 | -0.25 [-0.39, -0.07], n=158 |
| dM2 | +0.23 [-0.04, +0.42], n=330 | -0.97 [-1.84, +0.22], n=57 | -0.23 [-0.57, +0.20], n=79 |
| r_x2 | +0.02 [-0.35, +0.44], n=475 | -0.48 [-0.88, +0.14], n=145 | -0.29 [-0.39, +0.03], n=167 |
| t1x0.3 | +0.10 [-0.14, +0.37], n=525 | -0.29 [-0.48, +0.05], n=186 | -0.14 [-0.24, +0.03], n=168 |
| t1x3 | +0.16 [-0.22, +0.51], n=477 | -0.84 [-1.30, -0.07], n=162 | -0.41 [-0.61, -0.09], n=142 |
| t2_30 | +0.12 [-0.16, +0.42], n=402 | -0.48 [-0.72, -0.07], n=142 | -0.39 [-0.66, +0.03], n=129 |
| t2_365 | +0.02 [-0.19, +0.28], n=630 | -0.68 [-1.47, -0.13], n=217 | -0.29 [-0.48, -0.16], n=181 |
| +foreshock flag (expl.) | +0.14 [-0.25, +0.44], n=501 | -0.59 [-0.86, -0.17], n=176 | -0.29 [-0.43, -0.07], n=158 |
| +volcano<=30 km (expl.) | +0.13 [-0.27, +0.45], n=501 | -0.73 [-1.01, -0.03], n=176 | -0.29 [-0.44, -0.06], n=158 |
| foreshock-free only (expl.) | -0.36 [-0.61, -0.10], n=217 | -0.16 [-0.44, +0.17], n=87 | -0.25 [-0.44, +0.09], n=109 |
| low-background subset (expl.) | +0.08 [-0.34, +0.41], n=208 | -0.69 [-1.07, +0.07], n=79 | -0.14 [-0.28, +0.14], n=104 |
| outside Tohoku zone 2011-20 (expl.) | - | -0.65 [-1.27, -0.15], n=123 | - |

Settings: `Mc+0.5` (files: `Mc_p0.5`) raises the cutoff floor to 2.5 (CA, JP) or 5.0 (GL); `Mmin+0.5` (files: `Mmin_p0.5`) raises the mainshock threshold by 0.5; `dM2` limits the cutoff to Mm - 2; `r_x2` doubles the zone radius; `t1x0.3`, `t1x3` scale the fit start; `t2_30`, `t2_365` change the window end; `bg_mean`, `bg_zero` change the background; `hf radius` halves or doubles the heat-flow radius; `no geothermal hf sites` drops sites from geothermal exploration; `capped likelihood` limits each sequence to the weight of 50 events.

Summary of the 20-21 rows per sample: in California-Nevada, 17 of 20 slopes are positive. Only two intervals exclude zero: the `foreshock-free` bootstrap interval (negative) and the model C profile interval (positive, but too narrow). In Japan, 15 of 21 intervals are below zero. The exception that matters is `bg_zero`. In the global sample, 13 of 20 intervals are below zero and no slope is positive.

### Exploratory checks on the negative slopes

* **Background.** In Japan, with mu = 0 the slope is +0.12 (-0.31, +0.61). The median expected background share of the counts is 0.21 and 0.29 in the low and middle heat-flow terciles, but 0.02 in the high tercile. Without a background term, these background events enter the power law, and the pooled p of the low tercile decreases from 1.10 to 0.74. In the subset where the expected background is less than 10% of the observed count, mu has little effect. The slope there is -0.69 (-1.07, +0.07, n = 79). Outside the Tohoku zone during 2011-2020 (34.5-41.5 N, east of 139 E), the slope is -0.65 (-1.27, -0.15, n = 123). Thus the decaying Tohoku background does not explain the Japanese result. But the result is sensitive to how the background is modelled.
* **Volcanoes.** An indicator for a Holocene volcano within 30 km does not remove the Japanese slope (-0.73, -1.01 to -0.03).
* **Foreshocks.** 284 of the 501 California-Nevada sequences have at least one event above the cutoff in the 7 days before the mainshock. This is common in the Salton Trough and near geothermal fields. In the foreshock-free subset, the California-Nevada slope becomes negative: -0.36 (-0.61, -0.10, n = 217). The Japanese slope becomes -0.16 (-0.44, +0.17).
* **Global.** The global slope weakens in the low-background subset (-0.14, -0.28 to +0.14) and with a 200 km heat-flow radius (-0.15, -0.28 to +0.05).

## Interpretation

These samples do not show that aftershock sequences decay faster where the crust is hotter. The Kisslinger and Jones (1991) pattern (high p in the Salton Trough) is partly present in our California data: the high-heat-flow tercile has a higher p than the middle tercile. But the low-heat-flow tercile has the same p, and the slope is not different from zero. When we remove sequences with foreshock activity, the California slope is negative. In Japan and in the global sample, the slope is negative in most settings. In Japan, the slope is also negative in independent subsets (outside the Tohoku zone, low background). A possible explanation is that high-heat-flow crust in volcanic arcs and rifts has more fluid-driven, swarm-like activity, which decays slowly. But the volcano indicator did not explain the Japanese slope, and we did not test fluids directly.

The productivity results do not agree in sign across samples. Thus a single heat-flow rule for productivity is not supported. This agrees with the disagreement between Yang and Ben-Zion (2009) and Nandan et al. (2017).

## Limitations

1. Heat flow is a surface measurement with large local scatter. The local median within 50-100 km is a rough proxy for temperature at the hypocentre. The sign of the California slope changes with the radius (25 km: +0.27; 100 km: -0.17).
2. Heat flow correlates with tectonic setting, depth of the seismogenic zone, network density and background activity. Controls for magnitude, depth, year and background rate cannot remove all these differences.
3. Only 176 of 648 kept Japanese sequences have heat-flow sites within 50 km; the sample is mostly onshore and near-coast.
4. The global catalog is complete only at M 4.5 or more, and early aftershocks of large events are missing. We start the fit at 0.5 day and test 0.15 and 1.5 days.
5. The Omori-Utsu model with a constant background is a simplification. It ignores secondary triggering (ETAS) and non-stationary background. The `bg_zero` result shows that the Japanese slope depends on the background term.
6. Exploratory checks were chosen after we saw the main result. They describe the result; they do not confirm it.
7. ComCat magnitudes are mixed types (ML, Md, Mw); JMA uses Mj.

## Reproduction

1. Get the inputs (see `files/data/provenance.json`): the shared GHFDB ZIP, the 27 JMA yearly ZIPs, the global ComCat tarball from sci:sha256:2182948c..., and the California tarball in this bundle (or run `files/code/fetch_comcat_ca.sh`).
2. Put them in the layout in the header of `files/code/run_all.sh` and run it from the work folder. It runs all steps: 01_prepare (input tables), 02_sequences (11 settings x 3 samples), 05 (exploratory subsets), 03_analysis (fits), 03b_boot (cluster bootstraps), 04_figures and 06_summary.
3. Python 3.12 and the packages in `files/code/environment.txt`. The main fits take minutes; the bootstraps take about one CPU-day in total and run in parallel.

## Files

* `files/results/summary.json`: key numbers. `files/results/analysis_<setting>_<sample>.json`: all fits. `files/results/robustness_table.csv`: Figure 3 values. `files/results/terciles_*.csv`, `files/results/sample_*_main.csv` (analysed sequences with heat flow and individual fits). `files/results/boot/*.json`: bootstrap replicates.
* `files/data/derived/seq/seq_<sample>_<setting>.parquet`: all kept sequences per setting. `files/data/derived/aftershock_times_main.parquet`: event times (days after the mainshock) in the fit window for the main setting. `counts_*.json`: selection counts.
* `files/data/raw/`: California ComCat download and per-file SHA-256. `files/data/provenance.json`, `files/data/provenance_inputs.json`: sources, versions and hashes.
* `files/code/`: all code. `files/analysis_plan.md`: the plan fixed before the first heat-flow fit.
