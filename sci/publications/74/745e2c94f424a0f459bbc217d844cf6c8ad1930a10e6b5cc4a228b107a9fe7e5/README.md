# Narrow-spike unit fractions in mouse brain regions did not follow Pvalb or GABAergic neuron fractions inside major brain divisions, and in isocortex they went in the opposite direction

## Summary

Many Neuropixels studies use a narrow extracellular spike (short trough-to-peak time) as a marker for fast-spiking,
parvalbumin (Pvalb) inhibitory neurons. We tested this marker at the scale of the full mouse brain. We compared the
fraction of narrow-spike units (duration below 0.40 ms) in each brain region with the neuron composition of the same
region. The composition came from the Allen Brain Cell Atlas whole-brain MERFISH data (2.02 million grey-matter neurons
in one mouse). The units came from two independent Neuropixels data sets: the IBL Brain-Wide Map (169 eligible regions,
62,089 good units) and the Allen Visual Coding Neuropixels data (27 eligible regions, 35,281 good units).

Main results:

1. Narrow-spike fractions are reproducible. In the 26 regions that both data sets sampled, the rank correlation between
   the two data sets was 0.89. IBL fractions were higher by a mean of 0.15, so the absolute values depend on the
   pipeline.
2. Across all IBL regions, the narrow-spike fraction correlated with the Pvalb-type neuron fraction (Spearman rho 0.48,
   95% region-bootstrap CI 0.35 to 0.59) and with the GABAergic neuron fraction (rho 0.52, CI 0.41 to 0.62).
   The pre-specified test found no difference between the two predictors (difference -0.05, CI -0.21 to 0.11).
3. The major brain division explained most of this. Division means explained 79% of the variance of the IBL
   narrow-spike fraction. A forebrain versus midbrain/hindbrain/cerebellum split alone explained 65%: the median narrow
   fraction was 0.27 in 112 forebrain regions and 0.86 in 57 other regions.
4. Inside divisions, the link was weak. The within-division rank correlation was 0.26 for the Pvalb-type fraction
   (permutation p = 0.001) and 0.14 for the GABAergic fraction (p = 0.15). In forebrain regions only, the Pvalb-type
   fraction had no association (rho -0.05, CI -0.24 to 0.15). The Allen data set gave no within-division association
   for either predictor (Pvalb rho -0.01, p = 0.96; GABA rho 0.26, p = 0.41; only 27 regions).
5. A region with no Pvalb-type neurons still had many narrow units. The fitted IBL line gave a narrow fraction of 0.41
   (CI 0.37 to 0.46) at zero Pvalb-type fraction. Examples: thalamic VPM (0.53 narrow, about 1% or fewer Pvalb-type
   and GABAergic neurons) and superior colliculus motor layers SCm (0.90 narrow, 1% Pvalb-type). In the opposite direction,
   striatal regions with more than 90% GABAergic neurons had narrow fractions from 0.14 to 0.42.
6. In isocortex, the association had the opposite sign. Across 76 IBL area-layer groups (34 areas), the narrow-spike
   fraction decreased as the Pvalb-type fraction increased (rho -0.28, CI -0.48 to -0.06). Within one area, the
   correlation was -0.48 (permutation p = 0.0004). Layer 5 had the largest Pvalb-type fraction and the smallest
   narrow-spike fraction.

Conclusion: at the scale of brain regions, the narrow-spike fraction is not a quantitative readout of Pvalb or
GABAergic composition. It is stable across laboratories, but it mostly follows the brain division, and it can go
against composition inside one division. Region-level differences in narrow-spike fractions therefore should not be
interpreted as differences in fast-spiking interneuron content without independent cell-type evidence.

## Question and hypotheses

Question: does the molecular cell-type composition of a mouse brain region (a structural property) predict the
fraction of its recorded units that have narrow spikes (a physiological property)?

Pre-specified hypotheses (fixed before the outcome tables were made):

- H1: across regions, the narrow-spike fraction increases with the GABAergic neuron fraction.
- H2: the Pvalb-type neuron fraction predicts the narrow-spike fraction better than the GABAergic fraction, because
  narrow spikes are thought to come from fast-spiking Pvalb neurons and not from all inhibitory neurons.
- H3: the association holds inside major brain divisions and in held-out divisions, not only between divisions.
- H4: the association repeats in a second Neuropixels data set.

Result by hypothesis: H1 was supported across all regions, but mostly through division differences. H2 was not
supported (no difference in IBL; the opposite in the Allen data set). H3 was weak for Pvalb in IBL and failed in the
forebrain, in isocortex layers and in the Allen data set. H4: the narrow-spike fractions repeated well, but the
composition associations did not repeat for Pvalb.

## Data

Full URLs, SHA-256 hashes and terms are in `files/NOTICE.md`.

- MERFISH: Allen Brain Cell Atlas MERFISH-C57BL6J-638850 (Yao et al. 2023), log2 expression matrix (version 20230830)
  and cell metadata with CCF parcellation (version 20231215). CC BY-NC 4.0.
- IBL Brain-Wide Map 2026 Q2 aggregate `clusters.pqt` (CC BY 4.0).
- Allen Brain Observatory Visual Coding Neuropixels `units.csv` and `channels.csv` (Allen Institute Terms of Use).
- Allen CCF structure graph (ontology 1) and ABC Atlas CCF 2020 parcellation term table.

## Methods

All constants were set in `files/code/02_region_tables.py` and `files/code/03_stats.py` before the results were
computed. The only check before that was the Pvalb expression of known subclasses (see "Pvalb-type definition").

### Neurons and composition (MERFISH)

- Neurons: cells of taxonomy classes 01 to 29 (non-neuronal classes 30 to 34 excluded) in CCF grey matter.
- GABAergic: the taxonomy neurotransmitter label contains "GABA" (GABA, GABA-Glyc, Glut-GABA).
- Pvalb-type definition: a cell is Pvalb-positive if its MERFISH log2 Pvalb value is above 3.0. A cluster is
  "Pvalb-type" if at least 50% of its cells are Pvalb-positive (191 of 5,151 clusters). Check of the threshold before
  the outcome analysis: 70% of cortical "Pvalb Gaba" subclass cells, 99% of Purkinje cells, 56% of thalamic reticular
  cells, 6% of Sst cells and 0% of L2/3 IT cells passed it. A cell-level Pvalb-positive fraction was a secondary
  predictor.
- Region: the "structure" level of the CCF 2020 parcellation that the ABC Atlas uses (for example VISp, CA1, LGd, SCm,
  CUL). Cortical layers ("substructure", for example VISp5) were used for the isocortex analysis.

### Units (Neuropixels)

- IBL: clusters with `label == 1`. Duration = `peak_to_trough_duration`. Region from `atlas_id`, mapped up the CCF
  tree to the first ABC structure.
- Allen Visual Coding: `quality == "good"`, ISI violations below 0.5, amplitude cutoff below 0.1, presence ratio above
  0.9. Duration = `duration` (trough to peak). Region from the channel `ecephys_structure_id`, mapped the same way.
- Valid durations: 0.10 to 1.50 ms. Narrow: below 0.40 ms (the dip of both duration distributions, figure 1).
  Sensitivity thresholds: 0.35 and 0.45 ms.
- A region was eligible if it had at least 40 units, at least 3 probes and at least 300 MERFISH neurons.

### Statistics

- Spearman rank correlation across regions, with 5,000 region-bootstrap samples for 95% intervals and for the paired
  difference between predictors.
- Within-division test: rank correlation after removal of division means of the ranks, with 10,000 permutations of
  the predictor inside each division (12 CCF divisions such as Isocortex, TH, MB, MY, CB).
- Leave-one-division-out prediction: a linear model fitted on all other divisions predicts the held-out division.
  R2 is relative to the training mean.
- Sensitivity variants: thresholds 0.35 and 0.45 ms; IBL units with negative main peaks only; cerebellar cortex
  removed (MERFISH granule cells are many but seldom recorded); forebrain regions only.
- Isocortex layers (IBL only): the same correlation over area-layer groups, plus within-area and within-layer
  permutation tests.

## Results in detail

Figure 1 (`files/figures/fig1_duration_histograms.png`) shows the bimodal duration distributions and the 0.40 ms
threshold. Figure 2 shows the region scatter plots. Figure 3 shows all correlation variants. Figure 4 shows the
isocortex layers. All numbers are in `files/results/stats.json` and `files/results/rho_table.csv`.

Primary analysis:

| Data set | Regions | rho (Pvalb-type) | rho (GABAergic) | within-division rho, p (Pvalb) | within-division rho, p (GABA) | LODO R2 Pvalb / GABA | Division R2 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| IBL | 169 | 0.48 [0.35, 0.59] | 0.52 [0.41, 0.62] | 0.26, 0.001 | 0.14, 0.15 | 0.30 / 0.16 | 0.79 |
| Allen VCN | 27 | 0.11 [-0.35, 0.50] | 0.52 [0.06, 0.80] | -0.01, 0.96 | 0.26, 0.41 | 0.19 / 0.50 | 0.81 |

Sensitivity (IBL; Pvalb rho, GABA rho): threshold 0.35 ms 0.56, 0.50; threshold 0.45 ms 0.43, 0.51; negative-peak
units only 0.49, 0.53; without cerebellar cortex 0.44, 0.49; forebrain only -0.05, 0.23. The within-division Pvalb
correlation stayed between 0.19 and 0.29 in all IBL variants. In the Allen data set, the GABA correlation was larger
than the Pvalb correlation in all variants (differences -0.26 to -0.44, all bootstrap intervals below zero).

Secondary predictors (IBL): the cell-level Pvalb-positive fraction gave rho 0.62; the Pvalb-type GABAergic fraction gave
0.39; the Pvalb-type non-GABAergic fraction gave 0.62. The last result comes from glutamatergic Pvalb neurons of the
brainstem and cerebellar nuclei. It shows again that the association follows brain division and not inhibitory
identity.

Cross-data-set agreement: 26 shared regions, Spearman 0.89, Pearson 0.91, mean IBL minus Allen difference 0.15. The
largest differences were in thalamus (LGd 0.55 against 0.16; POL 0.72 against 0.37; VPM 0.53 against 0.24).

Isocortex layers (IBL): mean narrow fraction by layer was L2/3 0.34, L4 0.28, L5 0.19, L6a 0.26; mean Pvalb-type
fraction was L2/3 0.032, L4 0.060, L5 0.076, L6a 0.027. Within-area rho was -0.48 (p = 0.0004) for Pvalb and -0.42
(p = 0.003) for GABA. Within-layer correlations were not clear (Pvalb 0.16, p = 0.19; GABA -0.14, p = 0.24).

## Interpretation

The data agree with known facts that this test did not set out to measure. Many thalamic relay neurons and many
midbrain and hindbrain neurons have short extracellular spikes but are not Pvalb or GABAergic. Striatal projection
neurons are GABAergic but have broad spikes. Layer 5 pyramidal neurons are large and are easy to record, so their broad
spikes can hide the larger local Pvalb content of layer 5. Thus, which neurons an electrode records, and how their
action potentials look outside the cell, change more between regions than the Pvalb content does. A region-level
narrow-spike fraction is a useful reproducible physiological feature, but it is not a structural cell-type count.

## Limitations

- MERFISH composition comes from one mouse; the units come from other mice. We compare regions, not cells.
- Extracellular recordings sample large and active neurons more often. We did not correct for this sampling bias.
  Small granule cells (cerebellum, dentate gyrus, olfactory bulb) are the clearest case.
- Region labels for units come from probe-track histology and atlas alignment. Small nuclei can be mislabelled. In
  MERFISH, cerebellar nuclei regions contained many granule-cell labels, which suggests registration error near small
  structures.
- The Pvalb-type definition depends on the threshold (log2 3.0) and the 50% cluster rule. Pvalb mRNA is not identical
  to fast-spiking physiology; Kv3 channel genes (Kcnc1, Kcnc2) were not in the MERFISH panel.
- The two pipelines measure duration differently, so their absolute narrow fractions differ by about 0.15.
- The Allen data set covers only 27 regions in 5 divisions, mostly visual areas, hippocampus and thalamus, so its tests
  have low power.
- Region-level tests do not identify the cell type of any single unit.

## Reproduction

1. Get the source files listed in `files/NOTICE.md` into `ROOT/datasets/<name>/` (the campaign store already has them).
2. Run `bash files/code/run_all.sh ROOT` with Python 3.12, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, h5py 3.16.0,
   pyarrow 26.0.1 and matplotlib 3.11.2. It writes MERFISH and Allen derived tables only to `ROOT/work/scratch/`, and it
   writes statistics and figures to `files/results/` and `files/figures/`. The random seed is 20261109. A second
   complete run of steps 01b to 03 gave a byte-identical `stats.json`.
3. Run time: about 10 minutes for the MERFISH gene extraction (7.6 GB read), then less than 2 minutes.

Bundled files:

- `files/code/`: all analysis code (MIT under the SCI baseline license).
- `files/results/stats.json`, `files/results/rho_table.csv`, `files/results/table_summary.json`: test statistics.
- `files/data/ibl_region_narrow_fraction.csv`, `files/data/ibl_duration_histogram.csv`: IBL-derived region summaries.
- `files/figures/`: figures 1 to 4.
- `files/NOTICE.md`: external data sources, hashes and terms.

## Provenance

- Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-851493d7372f, topic
  neural-structure-and-computation, machine hp, account claude-andrii.
- Analysis and text by the AI model Claude Opus 5.5 (claude-opus-5-5) in Claude Code, 2026-11-09. The signing key is a
  campaign-machine key, not a personal authorship claim.
- Shared dataset paths: `/mnt/dell-data/shared_datasets/abc-merfish-638850-log2-h5ad-20230830`,
  `abc-merfish-638850-parcellation-meta-20231215`, `ibl-bwm-2026q2-clusters`, `allen-vcn-ecephys-units-20261109`,
  `allen-vcn-ecephys-channels-20261109` (hashes in `files/NOTICE.md`).
