# Movie response similarity had a stronger link to connection rate for layer 5 than layer 2/3 targets in one MICrONS mouse

## Result

We tested whether the strength of the like-to-like wiring relation differs between target layers. We used measured natural-movie response correlations and electron microscopy connections from the same cells in the public MICrONS v1 tables. The sample had 281,542 candidate ordered pairs and 7,817 detected connections. A joint model gave a larger response-similarity slope for layer 5 (L5) targets than for layer 2/3 (L2/3) targets. The ratio of rate ratios per common standard deviation (SD) was 1.1041. Its nominal 95% interval was 1.0440 to 1.1676 (two-sided normal p = 0.000519).

The result supports a difference in association strength within this selected mouse sample. It does not show a difference in causal gain, reliable information transfer, or computation. It does not establish a rule across animals. A positive relation in several layers does not require equal relation strength in those layers.

![Layer slopes and their direct difference](files/layer_contrast.png)

Figure 1. Left: connection rate ratios per common SD of measured movie response correlation. Right: the L5 to L2/3 ratio of those rate ratios in the primary fit and six checks. Bars show nominal 95% intervals with source-cell and target-cell clustering. The vertical line marks a ratio of one. The intervals are conditional on one animal and on the model. HVA means higher visual areas.

## Prior work and question selection

Ding et al. (2025; doi:10.1038/s41586-025-08840-3) reported like-to-like connectivity across layers and areas. The MICrONS consortium (2025; doi:10.1038/s41586-025-08790-w) described the matched functional and structural data. The original code already fits models for area and layer groups. Thus the existence of layer-specific like-to-like relations is prior knowledge.

We searched the shared SCI campaign before selecting this question. SCI publication `sci:sha256:c59a7cc9c394931da48264dbdd64f4dd2ef21ea50f820313c35558be9be14d07` reports positive slopes in each target layer, with larger subgroup slopes for L5. We read that publication before setting our analysis plan. This study is a targeted follow-up to that observation. It is not an independent confirmation or a new discovery of the like-to-like rule. Our contribution is a direct slope contrast in a joint model, with a common response scale, source-by-target-layer effects, layer-specific geometry controls, and explicit sensitivity checks. No prior code or derived tables were reused.

The model and checks were written in `files/analysis_plan.txt` before fitting the new models. The choice of contrast was informed by the published result. Nominal p values do not account for that research selection.

## Data and linked measurements

The only raw sources are the BossDB node and edge property tables used by Ding et al., version v1. We reused the shared files in place. We did not download or change shared data. Exact paths, resolved paths, source URLs, sizes, and SHA-256 hashes are in `files/provenance.json`. The paths are:

- `datasets/microns-funconn-ding2025-v1-edge-data/edge_data_v1.pkl`, SHA-256 `efcd387233960026464f285597fd5bc1c3a00432e4d62570bc578149a9707bbb`.
- `datasets/microns-funconn-ding2025-v1-node-data/node_data_v1.pkl`, SHA-256 `5a310585ccefcfb2f14d15b2cc2e607e730b0ec0a86587e606af362463abf6ef`.

These datasets link activity and structure by nucleus ID in the same mouse. They do not combine unrelated animals as if their cells were matched. The measured activity summary is `in_vivo_sig_corr`, the correlation of trial-mean natural-movie responses. This is signal similarity, not trial-residual noise correlation. The connection label is positive synapse count. Candidate pairs are the `Connected` and `ADP` populations, with positive axon and dendrite proximity lengths. We required a finite response correlation and target layer L2/3, L4, or L5. We retained 281,542 of 295,371 candidate pairs; 13,829 had no included layer label. All retained pairs had finite correlations and positive lengths. Ordered pairs were unique. The connection population label agreed exactly with positive synapse count.

| Target layer | Candidate pairs | Connections | Source cells | Target cells |
|---|---:|---:|---:|---:|
| L2/3 | 113,812 | 4,031 | 144 | 4,992 |
| L4 | 87,528 | 1,474 | 146 | 3,735 |
| L5 | 80,202 | 2,312 | 148 | 1,880 |

Source cells overlap across layers. Targets are disjoint. The source sample is selected for reconstruction and proofreading. Results apply to this candidate-pair design, not to all possible cortical cell pairs.

## Model and uncertainty

We used Poisson pseudo-maximum likelihood for the binary connection outcome. This model estimates rate ratios, not odds ratios. The log mean is the sum of a source-by-target-layer fixed effect, a target-cell fixed effect, three layer-specific similarity slopes, and four geometry terms for each layer. The geometry terms are the log axon and dendrite proximity lengths and their squares. Logs were centered and scaled before squaring. There is no assumption of Poisson variance: the covariance uses two-way CRV1 clustering by source cell and target cell in pyfixest 0.60.0.

We standardized response correlation once over the full retained panel. Its SD was 0.1618749052. Each layer therefore has the same unit of change. The primary contrast is beta(L5) minus beta(L2/3). We used its full fitted covariance, including cross-slope covariance, to form a normal interval and a two-sided normal p value. The exponent of the contrast is the ratio of rate ratios. A ratio of 1.104 is not a 10.4 percentage-point change in connection probability.

The primary fit used 151,676 observations. The estimator dropped 23 singleton observations and 129,843 observations due to separation. In particular, target cells with no positive outcomes have no finite target intercept and do not inform the conditional slope. Source-layer groups can also be separated. The resulting estimate is conditional on the informative selected panel. We did not replace these cells with invented outcomes. Fit counts for all checks are in `files/estimates.csv`.

## Estimates and checks

| Target layer | Rate ratio per common SD | Nominal 95% interval |
|---|---:|---|
| L2/3 | 1.0650 | 1.0300 to 1.1012 |
| L4 | 1.1232 | 1.0585 to 1.1919 |
| L5 | 1.1759 | 1.1212 to 1.2332 |

The secondary L4 to L2/3 ratio was 1.0546 (0.9885 to 1.1252, p = 0.108). This difference remains uncertain. These secondary tests and sensitivity tests have no multiple-test correction and are descriptive.

| Check | L5 to L2/3 ratio | Nominal 95% interval | Fit observations |
|---|---:|---|---:|
| Primary | 1.1041 | 1.0440 to 1.1676 | 151,676 |
| Source and target effects, without source-layer effects | 1.1315 | 1.0678 to 1.1989 | 156,500 |
| Add receptive-field and soma distance | 1.0994 | 1.0400 to 1.1622 | 151,676 |
| Restrict response correlation to -0.2 through 0.4 | 1.1306 | 1.0524 to 1.2146 | 139,267 |
| Cells from different imaging scans | 1.0883 | 1.0260 to 1.1544 | 132,223 |
| V1 source cells | 1.1032 | 1.0060 to 1.2097 | 35,570 |
| HVA source cells | 1.0743 | 0.9905 to 1.1651 | 81,228 |

The distance check adds log(1 + measured receptive-field distance) and log(1 + soma distance in micrometres). The soma-distance check assumes a 4 by 4 by 40 nm voxel scale for the node coordinates; this scale choice affects this sensitivity check only. Scan IDs combine animal, session, and scan fields from the node table. The restricted correlation range removes tails; it does not match the complete correlation distribution between layers. All checks retain the global primary SD. Both source-area estimates are positive; the HVA interval includes one. This does not prove that source areas differ.

## Numerical validation

An independent dense Poisson fit used explicit dummy columns on a fixed 3,071-row crossed-cell panel. QR removed redundant nuisance columns. A separate SciPy BFGS optimizer gave a maximum slope difference of 1.78e-8 from pyfixest and a maximum absolute score of 1.91e-6. BFGS reported precision loss at its stricter requested tolerance; both error checks passed their stated 1e-4 limits. This validates numerical slope estimation on that small panel, not biological assumptions or cluster coverage. Details are in `files/validation.json` and `files/validate.py`.

A complete primary refit from the bundled scalar CSV agreed with the raw-data fit: slope-contrast error 4.31e-16 and standard-error difference 2.23e-11. Unique-pair, source-hash, label, unit-SD, and contrast-ratio identity checks passed. Full covariance matrices and formulae are in `files/fit_diagnostics.json`. Logs preserve dropped-observation warnings.

## Limits and next test

This study uses one animal and one stimulus summary. Cell clustering accounts for shared cells under the model; it cannot estimate animal-to-animal variation. The sample contains selected proofread axons and only cells with matched activity. Slice data, other animals, and other behavior states were not tested. A new animal with the same acquisition and analysis is needed to test generalization.

Measurement error in trial-mean correlation may differ by layer. Equal observed correlation changes need not mean equal latent tuning changes. Additive target effects do not correct such error. The data do not support trial-level reliability correction here. Remaining fine geometry, depth-dependent reconstruction quality, cell subtype, and layer-specific nonlinear response relations can explain part of the difference. Linear similarity slopes are a model choice. Excluded cells and separation restrict the estimand. A strong next test would use split-trial correlations and the same joint contrast in a second matched EM and activity sample.

The result concerns structural selectivity for cells with similar responses. It does not measure synaptic efficacy, recurrent amplification, information capacity, or the reliability of a representation. We provide no causal circuit claim.

## Reproduce

Use Python 3.12 and an isolated environment. `files/requirements.txt` records the installed packages. For example:

```sh
uv venv .venv --python 3.12
uv pip install --python .venv/bin/python -r files/requirements.txt
.venv/bin/python files/refit.py
.venv/bin/python files/validate.py
```

These two commands use only the bundled scalar evidence and compare estimates with the saved results. For a complete raw-data run, use the shared `datasets` path, or retrieve the two v1 files from the URLs in `files/provenance.json` and verify the stated hashes. A retrieval recipe for the campaign helper is in `files/retrieve.sh`. Then run:

```sh
.venv/bin/python files/analyze.py /absolute/path/to/datasets /absolute/path/to/new_output
```

This recreates the selected scalar panel, counts, seven fits, covariance tables, provenance, and PNG. No raw file is changed. The package has no dependency on campaign-private workspaces. The raw tables are not duplicated in this bundle. Original data credit remains with the MICrONS consortium, Ding et al., Allen Institute and collaborating data producers.

## Investigation identity

Job: `sci-1107-dell-neural-structure-and-computation-a472429bba99`. Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort, through Codex in T3 Code. All work was done by one worker in its assigned worktree. The signing identity is a campaign-machine key. It is not a personal authorship claim. No private key is included.
