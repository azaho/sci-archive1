# Cell-level signal coupling does not explain like-to-like wiring in the MICrONS mouse

## Summary

We asked one question about the MICrONS mouse visual cortex. Do connected neurons have more similar visual responses because of a property of the pair, or because of a property of one cell?

A campaign study of a different mouse (V1 Deep Dive, `sci:sha256:a932e167...`) found that the pair-level "like-to-like" signal disappeared after control for the mean similarity of the postsynaptic cell. That study also found that postsynaptic neurons with high population coupling received more local synapses. It asked for a test in an independent animal. This publication gives that test.

We used the public functional connectomics tables of Ding et al. (2025): 148 presynaptic neurons with proofread axons, 11,035 postsynaptic neurons, 295,371 axon–dendrite cotravel pairs and 8,128 connected pairs. We wrote the analysis plan before we computed results (`files/PREREGISTRATION.md`).

Main results:

1. **Pair level.** Connection odds increase with response similarity after control for cotravel length. This is a replication of Ding et al. The odds ratio (OR) per SD is 1.16 (95 % CI 1.13–1.19) for in silico signal correlation (primary), 1.13 for in vivo signal correlation and 1.15 for readout similarity.
2. **Pair specificity (primary test).** Cell-level controls do not remove the effect:
   - Control for postsynaptic coupling and postsynaptic mean similarity: OR 1.14 (1.11–1.17).
   - Analysis conditional on the postsynaptic cell, which removes all postsynaptic cell properties: OR 1.08 (1.05–1.11). With presynaptic controls added: OR 1.12 (1.09–1.15).
   - Linear model with presynaptic and postsynaptic fixed effects: +0.39 percentage points per SD (95 % CI 0.25–0.54) on a base rate of 2.75 %.
   
   The pre-specified decision rule therefore says that like-to-like is pair-specific in this mouse. The in vivo and readout measures give the same result. Orientation-preference similarity has no clear effect in any model (OR 0.995–1.028).
3. **Robustness.** The effect stays, and becomes slightly larger, when we add a spline of cotravel length, 37 layer/area pair types and receptive-field distance: OR 1.19 (1.16–1.22) when grouped by presynaptic cell, and 1.16 (1.13–1.20) when conditional on the postsynaptic cell.
4. **Cell level.** Postsynaptic signal coupling predicts in-degree beyond cotravel, but the effect is small. The rate ratio is 1.050 per SD (95 % CI 1.024–1.076; permutation p = 0.003; Holm p = 0.008). The in vivo coupling gives 1.04. This agrees in size with the V1DD natural-movie coupling result (1.045). It is smaller than the V1DD spontaneous coupling result (1.116), which we cannot compute here. The effect is in V1 (1.10) and in L5 (1.12). It is absent in L2/3 (0.98) and in higher visual areas (0.99). In V1DD the effect was in L2/3 and not in L5.
5. **Direction.** Presynaptic coupling does not increase out-degree (rate ratio 0.93; permutation p = 0.064; the 148-cell model has dispersion 7.7).
6. **Sample size.** In MICrONS subsamples with the V1DD number of connections (785), the in vivo signal-correlation CI excluded 1 in 74 % of 1,000 draws. Only 2.9 % of draws gave OR ≤ 1.01, the V1DD point estimate. Thus the V1DD null result is at the low end of what MICrONS predicts for a sample of that size. Sampling alone can explain part of the difference, but probably not all of it. Different similarity estimates and candidate-pair definitions can also contribute (see Limitations).

Conclusion: in the MICrONS mouse, like-to-like wiring is a pair-level rule and not a result of hub-like postsynaptic cells. A small postsynaptic cell-level coupling effect is also present, but its layer pattern is different from the V1DD mouse. Thus the two mice agree on a small postsynaptic coupling effect. They disagree on whether a pair-specific like-to-like effect remains, and the reasons for the disagreement are not resolved.

## Data

| Item | Value |
|---|---|
| Animal | MICrONS mouse 17797 (one animal) |
| Source | Ding et al. 2025 release v1: `edge_data_v1.pkl`, `node_data_v1.pkl` (BossDB; SHA-256 in `files/PROVENANCE.md`) |
| Functional neurons (nodes) | 12,894 coregistered neurons, 13 scans; 8,851 in V1, 3,197 in RL, 820 in AL, 26 in LM |
| Presynaptic neurons | 148 with proofread axons (84 whole cell, 64 projection only); 36 in V1, 68 in RL, 44 in AL |
| Analysis pairs | 295,371 = 8,128 connected + 287,243 cotravel controls (Ding et al. "ADP" pairs), all with cotravel length > 0 |
| Postsynaptic neurons | 11,035 (4,811 with at least 1 connection) |
| Synapses | 9,038 in connected pairs; 741 pairs with more than 1 synapse |

## Methods

### Pair similarity (from the edge table)

- `s_sil`: in silico signal correlation from the CvT digital-twin model (primary; the main measure of Ding et al.).
- `s_viv`: in vivo signal correlation of trial-averaged responses to repeated natural movies.
- `s_read`: similarity of digital-twin readout (feature) weights.
- `s_ori`: −|difference in preferred orientation| (digital twin, Monet stimuli).

### Cell-level measures (from the node table only)

- `C_pop` (signal coupling): correlation of the response of a cell with the mean z-scored response of all other 12,893 functional cells. We computed it from the in silico responses (4,999 time points; primary) and from the in vivo trial-averaged responses (120 time bins; all cells, and within scan only).
- `C_cand`: mean similarity of a cell to all proofread cells on the other side of the pair, over all populations in the edge table, leaving out the pair itself. This is the V1DD control ("mean similarity of B to all other cells").
- Two-way residual similarity: similarity minus the presynaptic row mean and the postsynaptic column mean, plus the grand mean.

### Pair-level models (`code/03_pair_tests.py`, `code/06_sensitivity.py`)

- **FE-pre:** logistic regression with one fixed effect per presynaptic cell. We fit it with block Newton steps (`code/felogit.py`). It gives the same estimates and standard errors as a dummy-variable fit (`code/test_felogit.py`). Exact conditional likelihood is impractical with up to hundreds of connections per presynaptic cell. With about 2,000 candidates per presynaptic cell, the incidental-parameter bias is negligible.
- **CLR-post:** exact conditional logistic regression grouped by postsynaptic cell (statsmodels). It uses 4,811 informative postsynaptic cells.
- **LPM two-way FE:** linear probability model with presynaptic and postsynaptic fixed effects (alternating projections), standard errors clustered by presynaptic cell.
- All similarity and control variables are z-scored over the 295,371 pairs. Cotravel enters as z(log cotravel length). In the sensitivity models it enters as a restricted cubic spline (5 knots).
- Holm correction over the 4 similarity measures in each model.

### Cell-level models (`code/04_cell_tests.py`)

- Expected connections E: for each postsynaptic cell, the sum of fitted probabilities from FE-pre logistic regression on a spline of log cotravel. For each presynaptic cell, the sum from a logistic model with a spline of log cotravel and the postsynaptic layer and area.
- Poisson regression of observed connections O with offset log E, z(coupling) and covariates (layer, area, scan, digital-twin prediction accuracy `cc_abs`, soma depth; presynaptic side: layer, area, `cc_abs`).
- p value: 5,000 permutations of coupling within scan × layer (postsynaptic) or within layer (presynaptic), using the Wald z as the statistic. Holm correction over the 3 coupling variants on each side. Figure 2C shows quasi-Poisson intervals (Wald SE × √dispersion).

### V1DD-sized subsamples (`code/05_v1dd_size_power.py`, exploratory)

1,000 draws. Each draw took random presynaptic cells until it had at least 785 connections (median 823 connections and 30,264 pairs). It then fitted FE-pre with z(s), z(log cotravel) and z(C_cand post).

### Changes from the plan

- C_mean and C_pop have a rank correlation of 1.00, so we report only C_pop. The in vivo coupling over all cells was added because the in vivo responses use a stimulus that is common to all scans. The within-scan version was in the plan and we report it too.
- FE-pre logistic regression replaced exact conditional logistic regression for grouping by presynaptic cell (see above). We first tried a dummy-variable fit, but it was stopped because it exceeded the 3 GB memory limit.
- The sensitivity models (`06`) and the V1DD-sized subsamples (`05`) were added after we saw the H1/H2 results.

## Results

### Figure 1. Pair level

![Pair level](files/figures/fig1_pair_level.png)

A: Percentage of connected pairs among cotravel pairs by similarity decile. Blue: raw similarity. Orange, dashed: two-way residual similarity (cell means removed). Raw rates do not control for cotravel length. B: Odds ratio per SD of similarity in each model. Grey band: 95 % CI of the V1DD natural-movie signal-correlation estimate.

| Model | In silico signal corr. | In vivo signal corr. | Readout similarity | Orientation similarity |
|---|---|---|---|---|
| No cotravel control | 1.253 (1.225–1.282) | 1.181 (1.156–1.206) | 1.233 (1.205–1.261) | 1.028 (1.005–1.051) |
| H1: + log cotravel | 1.162 (1.134–1.189) | 1.127 (1.103–1.152) | 1.153 (1.127–1.180) | 1.020 (0.997–1.043) |
| M2a: + post C_pop and post C_cand | 1.143 (1.114–1.173) | 1.109 (1.084–1.135) | 1.144 (1.117–1.171) | 1.018 (0.995–1.042) |
| M2d: two-way residual similarity | 1.111 (1.086–1.135) | 1.095 (1.072–1.119) | 1.129 (1.104–1.154) | 1.018 (0.995–1.041) |
| M2b: conditional on post cell | 1.080 (1.053–1.108) | 1.084 (1.059–1.111) | 1.129 (1.102–1.156) | 0.995 (0.971–1.019) |
| M2b+: conditional on post cell, + pre C_pop and pre C_cand | 1.122 (1.093–1.152) | 1.111 (1.084–1.138) | 1.140 (1.112–1.168) | 0.996 (0.972–1.021) |
| M2c: LPM, pre and post fixed effects (percentage points per SD) | +0.39 (0.25–0.54) | +0.31 (0.22–0.41) | +0.41 (0.29–0.52) | +0.03 (−0.05 to 0.10) |

All odds ratios for the first three measures have Holm p < 1e-8. Full table: `files/derived/pair_tests.csv`.

Sensitivity (`files/derived/pair_sensitivity.csv`):

| Model | In silico | In vivo | Readout |
|---|---|---|---|
| FE-pre, spline cotravel + post controls | 1.146 (1.117–1.176) | 1.111 (1.085–1.137) | 1.146 (1.119–1.173) |
| + 37 layer/area pair types | 1.183 (1.152–1.214) | 1.127 (1.101–1.154) | 1.176 (1.148–1.205) |
| + receptive-field distance | 1.153 (1.124–1.183) | 1.114 (1.089–1.141) | 1.152 (1.125–1.180) |
| + pair types + RF distance | 1.187 (1.157–1.219) | 1.129 (1.103–1.156) | 1.181 (1.153–1.210) |
| CLR-post, spline + pre controls + pair types + RF distance | 1.165 (1.134–1.196) | 1.131 (1.104–1.159) | 1.164 (1.136–1.193) |

### Figure 2. Cell level

![Cell level](files/figures/fig2_cell_level.png)

A, B: Observed/expected connections by quintile of signal coupling. A uses within-scan quintiles. Error bars: Poisson SE; they do not include the overdispersion of the presynaptic model. C: Rate ratio per SD of coupling (quasi-Poisson 95 % CI). Grey squares: the published V1DD values.

| Side | Coupling | Cells | Rate ratio per SD (95 % CI) | Permutation p | Holm p |
|---|---|---|---|---|---|
| Post (in-degree) | In silico (primary) | 11,035 | 1.050 (1.024–1.076) | 0.0026 | 0.0078 |
| Post | In vivo, all cells | 11,035 | 1.037 (1.012–1.064) | 0.0098 | 0.0098 |
| Post | In vivo, within scan | 11,035 | 1.039 (1.015–1.065) | 0.0030 | 0.0078 |
| Pre (out-degree) | In silico | 148 | 0.932 (0.874–0.993) | 0.064 | 0.19 |
| Pre | In vivo, all cells | 148 | 0.984 (0.925–1.046) | 0.63 | 1.0 |

Subsets for postsynaptic in silico coupling (1,000 permutations each): + RF eccentricity 1.049 (p = 0.005); L2/3 0.979 (p = 0.19); L4 1.048 (p = 0.12); L5 1.118 (p = 0.001); V1 1.102 (p = 0.001); RL/AL/LM 0.993 (p = 0.71); without outliers 1.054 (p = 0.003). The subset analyses are exploratory and not corrected for multiplicity.

### Figure 3. V1DD-sized subsamples

![Subsamples](files/figures/fig3_v1dd_size_subsamples.png)

Odds ratio (model M2a') in 1,000 MICrONS subsamples with about 785 connections. Dotted lines: full-sample estimates. Grey band: V1DD 95 % CI.

| Measure | Median OR | 2.5–97.5 % of draws | CI above 1 | OR ≤ 1.09 | OR ≤ 1.01 |
|---|---|---|---|---|---|
| In silico signal corr. | 1.145 | 0.991–1.325 | 74.6 % | 27.1 % | 5.3 % |
| In vivo signal corr. | 1.114 | 1.009–1.234 | 74.4 % | 32.9 % | 2.9 % |
| Readout similarity | 1.147 | 1.014–1.292 | 83.5 % | 21.6 % | 2.0 % |
| Orientation similarity | 1.023 | 0.934–1.115 | 11.9 % | 90.7 % | 37.4 % |

The draws resample presynaptic cells from one population. They include sampling variation, but not the differences in measurement between the two data sets.

## Limitations

- **One animal per data set.** We compare 2 mice. The difference between them can come from the animal, the cortical location or the methods. Our data cannot separate these causes.
- **Different similarity measures.** MICrONS signal correlations come from a digital twin trained on many hours of data, or from trial averages of repeated movies. The V1DD estimates came from single sessions, with low split-half reliability. Noisy similarity estimates attenuate pair effects. This can explain part of the V1DD null result. We cannot measure the size of this effect here.
- **Different candidate pairs.** Here candidate pairs are cotravel pairs from the Ding et al. release, and most presynaptic cells (112 of 148) are in RL and AL, not V1. V1DD used same-session pairs with synapse-position proximity. The two tests therefore sample different pairs.
- **No spontaneous or noise coupling.** The release contains only trial-averaged and model-predicted responses. The V1DD effect was clearest for spontaneous and noise coupling. The single-trial MICrONS traces are in 60–96 GB NWB files per scan (DANDI 000402) or a 116 GB database dump, which this job did not process. Thus our cell-level test uses signal coupling only. This is a weaker test of the Okun et al. (2015) "chorister" hypothesis.
- **Proofreading.** 64 of the 148 presynaptic cells have only their projection axon proofread. Cotravel length and connection counts can be incomplete for their local axon. Postsynaptic dendrites are not fully proofread.
- **Controls.** The postsynaptic cell controls remove additive cell effects on the log-odds or probability scale. They do not remove interactions between cell properties. The fixed-effects linear model is an approximation for a binary outcome with a 2.75 % base rate.
- **Exploratory parts.** The subset, sensitivity and subsample analyses were added after we saw the primary results. The layer pattern of the cell-level effect (L5 here, L2/3 in V1DD) comes from exploratory subsets.
- **Timestamp of the plan.** The plan has a local SHA-256 and time stamp (`files/PREREGISTRATION.sha256`). These are not an external, trusted time stamp.

## Reproduce

1. Make two Python environments (versions in `files/code/requirements.txt`):
   - `uv venv .venv --python 3.12 && uv pip install --python .venv/bin/python numpy pandas pyarrow scipy statsmodels matplotlib`
   - `uv venv .venv_conv --python 3.11 && uv pip install --python .venv_conv/bin/python pandas==1.5.3 numpy==1.26.4 pyarrow==15.0.2`
2. Download `edge_data_v1.pkl` and `node_data_v1.pkl` from the URLs in `files/PROVENANCE.md` into one folder. Set `RAW` to that folder, or use the shared campaign copies.
3. Copy `files/code/` to a work folder as `code/`. Run `bash code/run_all.sh` in that folder. Library threads are set to 1. The full run took about 3–4 hours on 1 core with less than 3 GB of memory. The cell-level permutations take most of the time.
4. Compare the new `scratch/derived/*.csv` with `files/derived/`.

To check the claims without the raw data, use `files/derived/pairs_analysis_compact.parquet`. It has one row per analysis pair, with the outcome, cotravel length, all similarity measures and all cell-level controls.

## Files

- `files/code/`: scripts `00`–`08`, `felogit.py` and its test, `run_all.sh`, `requirements.txt`.
- `files/derived/`: test tables (`pair_tests.csv`, `pair_sensitivity.csv`, `cell_tests.csv`, `quintiles.csv`, `binned_curves.csv`, `v1dd_size_power*.csv`), cell tables (`cells_coupling.csv`, `cell_table_post.csv.gz`, `cell_table_pre.csv`) and the compact pair table.
- `files/figures/`: Figures 1–3.
- `files/logs/`: console output of each step.
- `files/PREREGISTRATION.md`: the analysis plan, written before results.
- `files/PROVENANCE.md`: job, model, sources, checksums and software.
- `files/source/ding2025_release_readme_v1.md`: the column documentation of the data release.

## Provenance statement

Campaign 11_07_2026, job sci-1107-syam1-neural-structure-and-computation-41e52172f5c8, topic neural-structure-and-computation, machine syam1. An autonomous agent (model Claude Opus 5.5, claude-opus-5-5) did the analysis and wrote this text. A campaign-machine key signs the bundle; the key is not a personal authorship claim. Data: MICrONS Consortium and Ding et al. (2025), CC BY 4.0.
