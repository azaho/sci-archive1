# Axonal input predicts which task variables a mouse brain region encodes

**Short answer.** In the IBL Brain-Wide Map (182 regions, 5 task variables), a region encodes a task variable more strongly when its strongest axonal input sources (Knox 2019 mesoscale connectome) also encode that variable. This is true beyond distance, shared probes and coarse brain division. The pre-specified coefficient is +0.34 SD of encoding per SD of input-weighted source encoding. Permutation p = 0.001 against two nulls: wiring labels shuffled within brain divisions, and inputs shuffled among sources at equal distance. The result replicates in an independent data set (Steinmetz et al. 2019, 57 regions, 4 variables): +0.37, one-sided p = 0.004. In that data set, the match holds for stimulus, choice and feedback, but not for wheel speed.

Job: `sci-1107-dell-neural-structure-and-computation-2713cf474ca7`. Topic: neural-structure-and-computation. Machine: dell. Model: Claude Opus 5.5 (`claude-opus-5-5`). Date: 2026-11-09. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Task variables (stimulus side, choice, feedback, wheel movement, block prior) are encoded in many brain regions. The IBL Brain-Wide Map (BWM) shows that these representations are widespread. But it does not test whether the anatomical connectome sets *which* region encodes *which* variable.

Hypothesis: long-range axons carry specific information. If this is true, a region must encode a variable more strongly when the regions that send it input encode that same variable. The test must remove three alternatives:

1. Some regions encode all variables strongly (for example, because they have many neurons). A region fixed effect removes this.
2. Nearby regions are similar for reasons that are not axonal (spatial smoothness, electrode localization error). A distance-weighted neighbour term and a distance-preserving null remove this.
3. Regions that the same probe records share the same mouse, session and behaviour. A probe co-recording neighbour term removes this.

Prior campaign work linked mesoscale wiring to spike *co-variation* (cae100c0, 193d9a56, 29db0c64). This study asks a different question: does wiring predict the *content* of the regional code?

## 2. Data

| Data | Version | Use |
| --- | --- | --- |
| IBL BWM per-region results, `brainwidemap/meta/region_info.csv` | GitHub `int-brain-lab/paper-brain-wide-map`, commit `de37454` (2025-03-27) | Region decoding scores for 5 variables |
| IBL BWM clusters aggregate `2024_Q2_IBL_et_al_BWM/clusters.pqt` | public S3 | Probe co-recording counts (good units, label = 1) |
| Knox et al. 2019 normalized connection density | Allen download; shared campaign dataset `knox2019-normalized-connection-density-20261109` | Weights W[source -> target], 291 regions |
| Allen CCF 2017 annotation, 10 um | shared dataset `allen-ccf2017-annotation10-20261109` | Region centroids (one hemisphere, 40 um grid) |
| Allen structure ontology (graph 1) | `api.brain-map.org` | Map fine labels to Knox regions |
| Steinmetz et al. 2019, Neuromatch npz release (3 files, 39 sessions, 10 mice) | OSF `agvxh`, `uv3mw`, `ehmw2` | Replication |

SHA-256 values of all input files are in `files/provenance/sha256.txt`. The external data is not in this bundle (see section 8 and `files/NOTICE.md`). `files/code/get_data.sh` downloads it into a local scratch folder.

## 3. Method

The pre-analysis plan is `files/code/PLAN.md`. I wrote it before I fitted any model.

**Encoding matrix.** Y[r, v] is the BWM decoding score of variable v in region r: `stim_dec`, `choice_dec`, `fback_dec`, `speed_dec`, `prior_dec_ep`. I converted each variable to z-scored ranks across regions. The analysis uses 182 regions that are both in the BWM decoding table and in the Knox region list. The panel has 910 region-variable values. (19 BWM regions are not Knox regions, for example cerebellar lobule subdivisions. I did not use them.)

**Network predictor.** X_in[r, v] = sum_s W[s -> r] Y[s, v] / sum_s W[s -> r]. Here s are the other analysed regions and W is the Knox ipsilateral normalized connection density. X_in is the input-weighted mean encoding of v among the sources of r.

**Controls.** Each control is a neighbour mean of the same form with a different weight matrix:
- X_dist: weights exp(-d / 1 mm), with d the centroid distance.
- X_corec: weights = number of BWM probe insertions that have at least one good unit in both regions (692 probes).
- X_div: weights = 1 for regions in the same Cosmos division (10 divisions).

**Model.** OLS: Y ~ region fixed effects + variable fixed effects + X_in + X_dist + X_corec + X_div. All predictors are z-scored. Because of the region fixed effects, beta_in measures only the variable-specific match: does r encode *more of v than of its other variables* when its sources do the same?

**Inference.**
- Null A (pre-specified): permute Knox region labels (rows and columns together) within Cosmos divisions, 1,000 times. Recompute X_in and refit.
- Null B (added after the first result, as a stricter test): for each target, shuffle input weights among sources in the same distance decile (or 20-quantile). This null keeps the weight-distance profile of each region. Only *which* sources at a given distance give input changes.
- The neighbour-mean construction gives a negative mechanical bias under null A (null mean -0.07). For this reason, I report beta_in against the permutation distributions and not against zero. Region-clustered SEs are also given for reference.

**Replication (Steinmetz 2019).** For each session and region (at least 5 units, mapped to Knox regions), I calculated cross-validated decoding scores. Each score is the 5-fold score minus the mean of 10 label-shuffle scores:
- stimulus side: logistic regression on spike counts 0-100 ms after stimulus onset, trials with unequal contrast;
- choice: logistic regression on counts 100-0 ms before movement onset, left versus right;
- feedback: logistic regression on counts 0-200 ms after feedback, reward versus error;
- wheel speed: ridge regression of |wheel| per 50 ms bin, 0-1 s after stimulus onset, with trial-grouped folds.

Region score = mean over sessions. The model, controls (co-recording = shared sessions) and nulls are the same as for IBL. The pre-specified test is one-sided (beta_in > 0).

## 4. Results

### 4.1 Primary test (IBL BWM)

| Model | beta_in | Null mean (SD) | Permutation p |
| --- | --- | --- | --- |
| Primary, null A (shuffle in division) | **0.337** | -0.074 (0.075) | 0.001 (two-sided) |
| Primary, null B (distance decile) | 0.337 | 0.004 (0.043) | 0.001 |
| Primary, null B (distance 20-quantile) | 0.337 | 0.034 (0.047) | 0.001 |
| No controls | 0.361 | 0.057 (0.055) | 0.001 |

The observed coefficient is above all 1,000 values of each null distribution (Figure 2). The control terms have small coefficients in the primary model: distance -0.03, co-recording +0.09, division -0.01. Specific axonal input explains the variable-specific similarity better than proximity or shared probes.

Figure 1 shows the pattern without the controls. After I removed each region's mean, the encoding of each variable correlates most with the input-weighted encoding of the *same* variable among its sources (IBL diagonal: stimulus 0.29, choice 0.22, feedback 0.46, wheel speed 0.25, block prior 0.15).

### 4.2 Sensitivity (IBL; all 1,000 permutations of null A)

| Variant | beta_in | p |
| --- | --- | --- |
| Manifold-distance scores (3 variables) | 0.49 | 0.001 |
| Euclidean-distance scores (3 variables) | 0.59 | 0.001 |
| GLM scores (4 variables) | 0.34 | 0.029 |
| Composite of all analyses | 0.55 | 0.001 |
| Distance scale 0.5 mm / 2 mm | 0.31 / 0.38 | 0.001 / 0.001 |
| Ipsi + contra weights | 0.33 | 0.001 |
| Top-10 inputs, binary | 0.32 | 0.001 |
| Wheel velocity in place of speed | 0.36 | 0.001 |
| Only inputs from the same division | 0.28 | 0.003 |
| Only inputs from other divisions | 0.23 | 0.003 |
| Leave out stim / choice / fback / speed / prior | 0.41 / 0.32 / 0.29 / 0.34 / 0.35 | 0.001-0.016 |
| Inputs and outputs in one model | in 0.26 (p 0.002); out 0.12 (p 0.077) | |
| log10(W / min + 1) weights (pre-specified) | -1.42, equal to its null (-1.40) | 0.39 |
| Post hoc: log weights above the median only | 0.28 | 0.044 |

One pre-specified variant failed as a test. The log10(W / min + 1) transform makes nearly all weights the same. X_in then becomes nearly the leave-one-out mean, and this is collinear with the fixed effects. Its coefficient equals its null mean, so it has no information. A post hoc log transform of only the above-median weights gives a positive result again. The effect is present with both within-division and between-division inputs, so it is not only a cortico-cortical or thalamo-cortical effect. Input weighting gives a larger coefficient than output weighting. But I did not test the in-out difference formally, and the output term is not excluded.

### 4.3 Replication (Steinmetz 2019)

| Model | Regions | beta_in | Null A mean (SD), one-sided p | Null B mean (SD), one-sided p |
| --- | --- | --- | --- | --- |
| Primary (>= 1 session) | 57 | **0.373** | -0.081 (0.154), 0.004 | 0.033 (0.084), 0.001 |
| No controls | 57 | 0.419 | 0.020 (0.130), 0.002 | |
| Regions with >= 2 sessions | 39 | 0.588 | -0.097 (0.174), 0.001 | 0.040 (0.073), 0.001 |

All four leave-one-variable-out fits stay positive (0.29-0.41, one-sided p 0.002-0.014). The diagonal of Figure 1 (right) is positive for stimulus (0.34), choice (0.26) and feedback (0.45). It is near zero for wheel speed (0.03). In Steinmetz, wheel-speed encoding follows the *choice* encoding of the sources (0.44). My wheel-speed decoder (|wheel| from the 0-1 s window) is probably not specific to movement vigour in that task. The wheel-speed part of the result thus did not replicate.

Figure 3 shows all models as the excess over the null mean.

## 5. Interpretation

Across two independent data sets, different labs and different decoders, the mesoscale connectome predicts the *content* of regional task codes. A region encodes the variables that its strongest axonal sources encode. This is specific to the variable, and the proximity, shared recording and division structure do not explain it. This agrees with a simple routing principle: information about a task variable is distributed along the axonal projections from regions that represent it. The principle applies at the level of whole brain regions in mice that do a visual decision task.

## 6. Limitations

- **Correlational and region-level.** The test cannot show that information flows along these axons. Shared inputs from a third region, or shared cell-type composition of connected regions, can also make connected regions encode the same variables. The data cannot separate these.
- **Knox weights** come from a voxel model of wild-type tracer experiments. They do not give cell-type specificity or synapse sign (excitatory or inhibitory). Regions that are absent from the Knox list (19 BWM regions) were not used.
- **BWM scores** are summary values from the published analyses. Their uncertainty is not part of my model. Regions with few neurons have noisier scores. The region fixed effect removes their mean but not their noise.
- **Null B was added after the first result.** It is stricter than the pre-specified null, and both give p = 0.001. But it is not pre-registered.
- **Effect size.** beta_in of 0.34 SD is moderate. Most of the variance of regional encoding is not explained by the wiring term.
- **Replication scope.** Steinmetz 2019 has 57 regions (39 with at least 2 sessions), 4 variables, and no block prior. Its wheel-speed result does not support the hypothesis.
- **Same anatomy in both tests.** Both data sets use the same Knox connectome. Thus, the replication is independent in the activity data only.

## 7. Reproduce

1. `bash files/code/get_data.sh /path/to/scratch/raw` downloads the IBL, ontology and Steinmetz files and prints their SHA-256 values. Compare them with `files/provenance/sha256.txt`. The Knox and CCF files come from the Allen URLs in the script (or from the shared campaign datasets).
2. Put the code in a folder `code/` next to `raw/` (or set `BWM_RAW`). Set `SCI_DATASETS` to the folder that holds the two Allen datasets. Install `pynrrd` (I used `uv pip install --target pylib pynrrd` and `PYTHONPATH=pylib`).
3. Run in order: `python 01_build_ibl.py`, `python 02_fit_ibl.py 1000`, `python 03_steinmetz_scores.py`, `python 04_fit_steinmetz.py 1000 1`, `python 04_fit_steinmetz.py 1000 2`, `python 05_figures.py`. Set `OMP_NUM_THREADS=1`. Outputs go to `derived/` and `figures/`.

Software: Python 3.12, numpy 2.5.4, pandas 3.1.1, scikit-learn 1.9.1, scipy 1.18.1, matplotlib 3.11.2, pynrrd 1.1.3. Seeds are fixed in the code. The Steinmetz decoding uses fixed CV seeds and per-session shuffle seeds.

Files in this bundle:
- `files/results/ibl_models.csv`: all IBL models (beta, clustered SE, permutation p, null mean and SD, control coefficients).
- `files/results/steinmetz_models_min{1,2}.csv`: replication models.
- `files/results/steinmetz_session_region_scores.csv`: my decoding scores for each session and region (262 rows). `steinmetz_region_scores_min{1,2}.csv`: region means.
- `files/results/null_betas.npz`: all permutation null coefficients that the figures use.
- `files/results/*.log`: run logs.
- `files/code/`: all analysis code and the pre-analysis plan.

## 8. External data and licences

See `files/NOTICE.md`. The IBL region table, the IBL clusters table, the Knox matrix, the CCF annotation and the Steinmetz npz files are not in this bundle. The tables of IBL region scores, Knox sub-matrices and region centroids that I made from them are also not in this bundle. The scripts make them again from the source files.
