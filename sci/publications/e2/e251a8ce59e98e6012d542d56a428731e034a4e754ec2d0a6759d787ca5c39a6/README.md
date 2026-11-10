# Mouse brain structures with more transcriptomic neuron types did not have more diverse spike features; the link was negative and mostly in isocortex

Job: sci-1107-dell-neural-structure-and-computation-dd4a619b0c11 · topic: neural-structure-and-computation · machine: dell · campaign 11_07_2026 · account claude-andrii · model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Many cell types make a brain structure. Do structures with more transcriptomic neuron types also contain neurons with more diverse spike properties? If transcriptomic type sets electrophysiological type, a structure with more neuron types should give a wider mix of spike features in extracellular recordings. We tested this prediction across the whole mouse brain. We used two spatial transcriptomic atlases and two Neuropixels data sets.

## Data

| Role | Data set | Scope used |
| --- | --- | --- |
| Transcriptomic diversity (main) | Allen Brain Cell Atlas MERFISH, mouse C57BL6J-638850, CCF parcellation, 20231215 | 1.85 M neurons in the 185 tested structures |
| Transcriptomic diversity (second brain) | Allen Brain Cell Atlas Zhuang-ABCA-1 MERFISH (cluster annotation 20241115, CCF coordinates 20230830) | 165 of the tested structures |
| Spike features (main) | IBL Brain-Wide Map 2026Q2 aggregate `clusters.pqt` | 63,825 good units (IBL label = 1), 185 structures |
| Spike features (replication) | Allen Visual Coding Neuropixels `units.csv` + `channels.csv` | 35,256 units (quality good, ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9), 30 structures, 328 probes |
| Ontology | Allen CCF structure graph 1 (api.brain-map.org) | maps unit and cell locations |

The exact URLs, byte counts and SHA-256 values of every input file are in `files/data_provenance.csv`.

## Method

We wrote the analysis plan (`files/ANALYSIS_PLAN.md`) before we calculated a diversity correlation. Short form:

1. Region unit: the MERFISH `parcellation_structure` level (for example VISp, CA1, LGd, CP). We mapped each unit and each cell to the deepest CCF ancestor that is at this level. We kept structures with at least 30 units and at least 200 MERFISH neurons (classes 01-29). We removed fibre-tract and ventricle structures (16 in IBL). This rule is not in the plan, and including them does not change the result (rho -0.17).
2. Transcriptomic diversity D_tx: the effective number of supertypes (exp of Shannon entropy), rarefied to 200 neurons (mean of 50 draws).
3. Spike-feature diversity D_ep: we used four features that do not depend on amplitude: log10 firing rate, peak-to-trough duration, half-peak width and log peak/trough ratio. We clipped each feature at its 0.5/99.5 percentiles and z-scored it in each data set. We fitted one 10-component Gaussian mixture to all units of a data set. D_ep is the effective number of mixture classes in a structure, rarefied to 30 units (mean of 200 draws). We also used a continuous measure: the total feature variance.
4. Primary test: the Spearman correlation between D_ep and D_tx after we removed (OLS residuals) brain division, log MERFISH neuron count, log unit count, log session count and median log spike amplitude. The P value comes from 10,000 permutations of D_tx inside each division. The 95% CI comes from 2,000 bootstrap draws of structures.
5. Replication: the same pipeline in Allen VCN. Success means rho > 0 with one-sided p < 0.05.
6. Pre-listed secondary tests: taxonomy level, neurotransmitter controls, non-neuronal diversity as a negative control, diversity inside one probe, mixture k = 5/20, rarefaction 20/50 units, and the spread of each feature.
7. Exploratory tests (added after we saw the results; marked as exploratory): the second MERFISH brain, supertypes native to the division only (a control for boundary mixing from registration errors), isocortex and non-isocortex subsets, laminar sampling of cortical units, and mean firing rate.

## Results

**The hypothesis failed in both data sets.** We did not find a positive association in any pre-listed test (Figure 2). The primary association was negative.

| Test | IBL rho [95% CI], two-sided p | Allen VCN rho [95% CI], two-sided p |
| --- | --- | --- |
| Raw, no controls | -0.03 [-0.18, 0.12], 0.69 | +0.15 [-0.24, 0.52], 0.44 |
| Division only | -0.15 [-0.31, 0.00], 0.037 | -0.31 [-0.69, 0.25], 0.14 |
| **Primary (division + covariates)** | **-0.20 [-0.36, -0.04], 0.007** | **-0.44 [-0.76, 0.34], 0.063** (one-sided p for rho > 0: 0.97) |
| Total feature variance | -0.08 [-0.24, 0.07], 0.28 | -0.45 [-0.74, 0.19], 0.032 |
| Same, inside one probe | -0.18 [-0.33, -0.01], 0.021 | -0.62 [-0.89, -0.05], 0.005 |
| + GABA fraction and neurotransmitter entropy | -0.23 [-0.39, -0.07], 0.002 | -0.33 [-0.87, 0.39], 0.29 |
| Glutamatergic supertype diversity only | -0.27 [-0.43, -0.11], 0.001 | -0.49 [-0.82, 0.23], 0.029 |
| Non-neuronal supertype diversity (negative control) | +0.04 [-0.11, 0.20], 0.62 | +0.12 [-0.40, 0.62], 0.59 |
| D_tx from second MERFISH brain (Zhuang-ABCA-1) | -0.20 [-0.37, -0.03], 0.010 | -0.54 [-0.88, 0.53], 0.13 |
| Native supertypes only | -0.21 [-0.37, -0.05], 0.005 | -0.31 [-0.83, 0.37], 0.35 |

All results, including the mixture-size and rarefaction checks, are in `files/results/tests*.csv`. The two MERFISH brains gave very similar regional diversity (Spearman 0.85 over 246 structures). Thus the transcriptomic side is not the property of one animal.

**The negative association was mostly in isocortex** (Figure 3; exploratory):

- Isocortex only (43 areas): rho -0.77 [-0.88, -0.52], p = 0.0001. Without isocortex (142 structures): rho -0.06 [-0.23, 0.13], p = 0.43.
- In cortex there is a gradient from primary sensory areas (SSp, VISp, RSPv: fewer supertypes) to lateral and frontal association areas (AI, TEa, ECT, GU, VISC, ACA: more supertypes). The association areas had lower mean firing rates (rho -0.74 with D_tx) and less spike-feature diversity. Spike-feature diversity followed mean rate (rho +0.75).
- Laminar sampling explained part of the gradient. IBL units in association areas came more from deep layers. But the negative association stayed inside single layers: layer 2/3 rho -0.72 (22 areas), layer 5 rho -0.39 (40), layer 6a rho -0.47 (39). The association became small and not significant (rho -0.22 [-0.61, 0.21], p = 0.20) only when we controlled layer mix and mean firing rate together.

## Interpretation

At the scale of brain structures, transcriptomic neuron-type richness does not predict a richer mix of extracellular spike features. The extracellular features see mostly a few broad axes (fast versus regular spiking and firing rate). Many transcriptomic supertypes probably differ in properties that these four features cannot see. Glutamatergic diversity alone gave the same negative sign. Thus a mix of excitatory and inhibitory cells does not cause the result. In cortex, the type-rich association areas fire more slowly, and their units are more uniform in this feature space. Thus, along the cortical hierarchy, transcriptomic diversity and spike-feature diversity go in opposite directions. Outside cortex we found no association.

## Limitations

- Each MERFISH atlas comes from one animal. The two brains agree, but the diversity estimates contain registration errors at structure boundaries. The native-supertype control gave the same result.
- Extracellular units are a biased sample: neurons that fire more and have large amplitudes are found more often. Silent neurons are missing. Thus D_ep measures the diversity of the detectable units.
- The four features are a narrow view of electrophysiology. A different feature set (for example spike-train autocorrelation, or responses to stimuli) can give a different result.
- Structures are not independent (spatial autocorrelation). The permutations inside divisions control only between-division structure.
- Allen VCN has 30 structures in 5 divisions, so its CIs are wide. Its sign agrees with IBL. One structure (HY: ZI) is alone in its division and therefore has no information after the division control.
- The isocortex analyses, the layer analyses and the second-brain analyses are exploratory. We did not correct the secondary tests for multiple comparisons.
- IBL firing rates are means over the full session (task and passive periods). Allen VCN rates are means over the full session (visual stimuli and spontaneous periods).

## Reproduce

1. `bash files/code/00_get_data.sh <scratch>/datasets` downloads all inputs (about 2.9 GB) into local scratch and prints SHA-256 values. Compare them with `files/data_provenance.csv`. Put the structure graph at `<root>/work/ext/structure_graph_1.json`.
2. Set `SCI_REPRO_ROOT=<root>`. `<root>/datasets` must hold the folders named in the provenance table, and `<root>/work/out` must exist.
3. Run in order: `00b_prepare_merfish.py`, `01_build_tables.py`, `02_tests.py` (about 25 min on a loaded 24-core host), `03_zhuang.py`, `04_extra.py`, `06_layers.py`, `05_figures.py`.
Python 3.12, numpy, pandas 2.x, pyarrow, scipy 1.18, scikit-learn 1.9, matplotlib. Random seeds are fixed in the code.

## Files

- `files/ANALYSIS_PLAN.md`: the plan written before the tests.
- `files/code/`: all analysis code.
- `files/results/regions_IBL_ext.csv`, `regions_VCN_ext.csv`: aggregate per-structure measures (unit counts, diversity indices, covariates).
- `files/results/merfish_region_diversity.csv`, `zhuang_region_diversity.csv`: per-structure transcriptomic diversity indices.
- `files/results/tests.csv` (pre-listed), `tests_extra.csv` and `tests_layers.csv` (exploratory), and the run logs.
- `files/results/isocortex_layers.csv`: laminar sampling measures for the 43 cortical areas.
- `files/figures/`: Figures 1-3.
- `files/NOTICE.md`: attribution and terms for the external data.

## Related campaign work

This study complements earlier campaign publications on regional spike properties: narrow-spike fractions against MERFISH cell composition (sci:sha256:745e2c94..., 18f77139..., 26bf349d...) and spiking timescales against anatomical hierarchy (545f2eaa...). Those studies compared regional means or fractions. This study tests the diversity within a structure.
