# Glomerulus input share, not Kenyon cell co-convergence, gives the community input advantage in fly mushroom body models from three connectome hemispheres

## Summary

In the fly mushroom body, each Kenyon cell (KC) receives input from a small number of olfactory projection neurons (PNs). Zheng et al. (2022) found that PNs from a group of mostly food-responsive glomeruli share KCs more often than chance. They proposed that this makes the mushroom body an "associative fovea" that discriminates food odors better. Their discrimination model used synthetic inputs and no KC threshold.

We asked two questions:

1. Is this co-convergence structure the same in three hemispheres from two flies: FlyWire left, FlyWire right, and hemibrain right?
2. In a thresholded, sparse KC model, does the real wiring improve odor discrimination? If so, is the cause the input share of each glomerulus, or the KC-level co-convergence beyond that share?

Main results:

- **The structure is conserved.** A co-convergent community of 16 to 18 glomeruli occurs in each hemisphere. Thirteen glomeruli are in all three: DL2v, DM1, DM2, DM3, DM4, DM5, DM6, DP1l, DP1m, VA2, VA4, VM2 and VM3. Glomerulus input shares agree across hemispheres (Spearman 0.89 to 0.93). A community defined in one hemisphere also has a high mean co-convergence z in another hemisphere. This holds in 4 of 6 tests at p ≤ 0.0002. The two tests from FlyWire to hemibrain are weaker (p = 0.038 and 0.070).
- **With synthetic inputs, the community advantage comes from input share.** Patterns that activate only community glomeruli are harder to identify than patterns that activate only other glomeruli, for all wiring types. Against a null that gives each glomerulus an equal share, the real wiring reduces this gap. The z values are 2.75 and 4.41 in FlyWire and 0.48 in hemibrain. When each glomerulus's rate is divided among its sister PNs, the z values are 7.09, 6.18 and 3.51. Against a null that keeps every PN's out-degree and every KC's in-degree (and thus the input shares) but removes co-convergence, the real wiring gives no advantage (z from −1.67 to 0.24).
- **With 110 measured odors, the real wiring gave no identification gain.** We used Hallem & Carlson (2006) receptor responses. Real wiring and the fixed-degree null gave equal accuracy (main z: 0.39, 0.55, −0.70). Real wiring was less accurate than the equal-share null (z −1.44, −1.24, −2.56). KC dimensionality was lower for the real wiring than for each null in about half of the 24 setting-hemisphere cases (12 and 11), and higher only without lateral normalization. Odors that drive the community more did not get a larger wiring gain (48 tests, Spearman rho from −0.33 to 0.13, no positive test at p < 0.05).

Thus the "fovea" effect in these models is a consequence of unequal glomerulus input shares. The extra pairwise co-convergence is reproducible across animals, but we found no computational effect of it in our models. For the measured odor set, the unequal shares gave no gain and in some model settings a loss.

## Question and hypotheses

- H1 (structure): Pairwise glomerulus co-convergence on KCs, measured against a fixed-degree null, is reproducible across hemispheres and animals.
- H2 (synthetic computation): With a sparse thresholded KC layer, real wiring gives community inputs a discrimination advantage relative to other inputs. We test this against two nulls to find the cause.
- H3 (odor computation): Real wiring improves identification of measured odors, and the gain is larger for odors that drive the community.

The results support H1, support H2 against the equal-share null only, and do not support H3.

## Data and provenance

| Input | Source and version | File and SHA-256 |
| --- | --- | --- |
| FlyWire connections | FlyWire v783, Zenodo record 10676866 (Dorkenwald et al. 2024). Shared campaign path: `datasets/fly-flywire-connections-783-zenodo10676866/` (`/mnt/dell-data/shared_datasets/...`) | `proofread_connections_783.feather`, 24f960ae3e7d4f8cd30db3b62e99fb5179cc3d1e76d8c155bfb441e9737d3faf |
| FlyWire cell annotations | github.com/flyconnectome/flywire_annotations, commit a83b2776d60d5764cef36b927f5f9679c16c47a2 (Schlegel et al. 2024) | `Supplemental_file1_neuron_annotations.tsv`, b214970b55d2fbe0853bba536fdcb9e28730f4eb7ab06f600491df795da683cd |
| Hemibrain connections | hemibrain v1.2 traced adjacencies, https://storage.googleapis.com/hemibrain/v1.2/exported-traced-adjacencies-v1.2.tar.gz (Scheffer et al. 2020) | tar.gz 07d8946eb0c4e3a5cb23d5769c9817847494f9fcadbc0ca239eed7bbd5555cf7 |
| Receptor responses | DoOR.data (Münch & Galizia 2016), github.com/ropensci/DoOR.data commit db323a496577c4b4a72b5c2fcd1859e07521ffb5; the `Hallem.2006.EN` columns of the 24 receptor files, the consensus `door_response_matrix.csv`, and `door_mappings.csv` | See `files/data/raw_sha256.txt` (30 files) |

The FlyWire table was read in place from the shared dataset store. The other raw files were downloaded to the worker workspace. They are not in this bundle. `files/code/fetch_data.sh` downloads them again and checks the hashes.

## Methods

**Connectivity.** We used uniglomerular PNs (FlyWire `cell_class` ALPN, `cell_sub_class` uniglomerular). The glomerulus is the PN cell type name without its lineage suffix. We translated hemibrain PN type names to FlyWire names with the FlyWire `hemibrain_type` column (for example, hemibrain VC3l is FlyWire VC3). We used all annotated KCs on the same side as the PN. A PN-KC connection is 3 or more synapses, as in Zheng et al. (2022). This gave 2,361, 2,372 and 1,745 KCs and 114, 118 and 105 PNs from 55, 55 and 52 glomeruli. The mean KC in-degree was 4.71, 4.56 and 5.52 (`files/data/derived/structure_summary.json`).

**Co-convergence.** For each glomerulus pair, we counted the KCs that receive at least one connection from both glomeruli. We compared this count with 300 samples of a curveball null (Strona et al. 2014) that keeps every PN's out-degree and every KC's in-degree, and calculated a z value. The community is the negative-sign side of the leading eigenvector of the z matrix (`04_community.py`). To prevent circular tests, we also tested each hemisphere's community in the other two hemispheres, with 5,000 random glomerulus sets of the same size (`06_stats.py`).

**Wiring variants.**
- `real`: the connectome.
- `fixed_degree`: the curveball null. It keeps the glomerulus input shares and removes KC-level co-convergence beyond them.
- `uniform_glom`: each KC keeps its number of connections, but each connection picks a glomerulus with equal probability and then a PN of that glomerulus. It removes input shares and co-convergence.

**KC model (`03_odor_model.py`).**
1. Glomerulus ORN drive is the Hallem & Carlson evoked rate, clipped at zero. Or33b is co-expressed in DM3 and DM5, so its response is added to Or47a (DM3) and Or85a (DM5).
2. PN rate uses the Olsen et al. (2010) transform, Rmax 165 Hz and σ 12 Hz. Lateral inhibition is 1.34 times the mean ORN drive (this is an approximation of the published total-input term).
3. Glomeruli without receptor data have zero drive.
4. Each PN of a glomerulus has an independent Poisson spike count in a 40 ms window.
5. KC input is the sum of connected PN rates. Weights are binary claws in the main setting.
6. A global (APL-like) threshold keeps the top 10% of KCs active in each trial. The KC response is rectified input above that threshold.
7. Each odor has 20 training trials (averaged into a template) and 20 test trials. We classify each test trial by maximum cosine similarity to the 110 templates.
8. We also calculate the participation ratio of the noise-free KC responses across odors.

The real wiring uses 5 noise replicates, and each null uses 50 samples. A z value is (real mean − null mean) / null SD.

**Synthetic test (`05_synthetic.py`).** Each of 100 patterns activates 5 glomeruli at 50 to 100 Hz. The glomeruli come only from the hemisphere's community, or only from the other glomeruli. The KC model and classifier are the same as above. Five fixed pattern sets are used, and replicate i of every wiring variant uses set i mod 5. Variants: `pnnorm` divides the glomerulus rate among its sister PNs. `consensus` uses the 2-of-3 consensus community.

**Sensitivity runs (30 nulls each).** Synapse-count weights, a per-KC threshold (90th percentile across odors), no lateral normalization, absolute rates (spontaneous included, unmapped glomeruli at baseline), a 100 ms window, a 5% coding level, and the DoOR consensus odor set (58 odors × 25 glomeruli, including DM1, VA2, DL2d and DL2v).

## Results

### Structure (Figure 1)

| | FlyWire left | FlyWire right | Hemibrain right |
| --- | --- | --- | --- |
| Community size | 18 | 17 | 16 |
| Mean z within / between community | 1.45 / −0.98 | 1.27 / −0.84 | 0.50 / −1.25 |
| Pairs with abs(z) > 3 | 107 of 1,485 | 62 of 1,485 | 107 of 1,326 |
| Share of PN-KC connections from community | 0.433 | 0.418 | 0.407 |

Across hemisphere pairs: the community Jaccard index is 0.74 to 0.83, the Spearman correlation of pair z values is 0.47 to 0.50, the Spearman correlation of glomerulus input shares is 0.89 to 0.93, and the Spearman correlation of eigenvector loadings is 0.85 to 0.86 (`community.json`).

Cross-hemisphere replication (`community_replication.csv`). Each test uses the community defined in the first hemisphere and measures its mean within-community z in the second hemisphere:

| Defined in → tested in | Mean within z | Permutation p |
| --- | --- | --- |
| FlyWire left → right | 0.98 | 0.0002 |
| FlyWire right → left | 1.26 | 0.0002 |
| Hemibrain → FlyWire left | 1.58 | 0.0002 |
| Hemibrain → FlyWire right | 1.28 | 0.0002 |
| FlyWire left → hemibrain | 0.37 | 0.038 |
| FlyWire right → hemibrain | 0.29 | 0.070 |

In hemibrain, the community is defined more by its avoidance of the other glomeruli than by strong internal co-convergence.

### Measured odors (Figure 2)

Main setting, 110 Hallem & Carlson odors. Chance accuracy is 0.009.

| | FlyWire left | FlyWire right | Hemibrain right |
| --- | --- | --- | --- |
| Accuracy, real (5 replicates) | 0.627 | 0.634 | 0.621 |
| Accuracy, fixed-degree null (mean ± SD) | 0.623 ± 0.011 | 0.627 ± 0.011 | 0.631 ± 0.013 |
| Accuracy, equal-share null | 0.645 ± 0.013 | 0.649 ± 0.012 | 0.654 ± 0.013 |
| Participation ratio, real | 11.78 | 11.59 | 11.98 |
| Participation ratio, fixed-degree null | 13.31 ± 0.65 | 12.94 ± 0.53 | 12.41 ± 0.47 |
| Participation ratio, equal-share null | 13.77 ± 0.53 | 13.75 ± 0.48 | 13.05 ± 0.65 |

The 23 glomeruli with Hallem data receive 0.44, 0.45 and 0.44 of the real connections. Under the equal-share null they receive 0.42, 0.42 and 0.44. Thus a difference in the signal-carrying share does not explain the accuracy difference.

Per-odor test (`per_odor_drive.csv`). For each odor, community drive is the community fraction of the total PN response. The wiring gain is real accuracy minus null accuracy. Their Spearman correlation was negative in 37 of 48 tests (8 settings × 3 hemispheres × 2 nulls). It was never positive at p < 0.05, and it was negative at p < 0.05 in 9 tests.

### Synthetic community and other inputs (Figure 3)

Advantage = accuracy for community-only patterns − accuracy for other-only patterns.

| Run | Null | FlyWire left z | FlyWire right z | Hemibrain z |
| --- | --- | --- | --- | --- |
| main | fixed degree | 0.21 | 0.24 | −0.43 |
| main | equal share | 2.75 | 4.41 | 0.48 |
| pnnorm | fixed degree | −1.21 | −0.80 | −1.67 |
| pnnorm | equal share | 7.09 | 6.18 | 3.51 |
| consensus community | fixed degree | 0.05 | −0.18 | −0.35 |
| consensus community | equal share | 1.76 | 3.93 | 1.90 |

In the main run, the raw advantage was negative for all wiring types. For the real wiring, it was −0.038, −0.047 and −0.071. Thus the community inputs were not better discriminated in absolute terms. Only the gap to the other inputs became smaller. In the pnnorm run, community patterns were better identified than other patterns in FlyWire for the real wiring (+0.026, +0.040). In hemibrain they were not (−0.110).

### Sensitivity (Figure 4, `model_vs_null.csv`)

Across 8 settings × 3 hemispheres:

- **Real versus fixed-degree null, accuracy:** z ≤ −2 in 1 of 24 cases and z ≥ 2 in none. The maximum was z = 0.70.
- **Real versus equal-share null, accuracy:** z ≤ −2 in 10 of 24 cases (synapse weights, no normalization, 100 ms window, and hemibrain main) and z ≥ 2 in none. The maximum was z = 0.54. With absolute rates, the DoOR set and per-KC thresholds, real wiring and the equal-share null gave equal accuracy.
- **Dimensionality:** Real dimensionality was lower than the fixed-degree null in 12 of 24 cases and higher in 1. It was lower than the equal-share null in 11 of 24 cases and higher in 2. All of the higher cases were in the no-normalization setting. Thus the dimensionality result depends on the antennal lobe normalization assumption.

## Figures

- `files/figures/fig1_coconvergence.png`: co-convergence z matrices for the three hemispheres.
- `files/figures/fig2_model_vs_null.png`: odor identification accuracy and KC dimensionality, real wiring and nulls.
- `files/figures/fig3_synthetic.png`: synthetic community-only and other-only patterns.
- `files/figures/fig4_sensitivity.png`: z of real wiring against each null in all model settings.

## Limitations

- The KC model is simple. It has no APL dynamics, no KC-to-KC coupling, no spike timing, no learning readout and no multiglomerular PNs. A different readout (for example, an MBON learning rule) can give different results.
- Receptor data cover 23 of the 52 to 55 glomeruli in the Hallem set. Important community glomeruli (DM1, VA2, VA4, DP1m and DL2v) have no Hallem data. The DoOR set adds DM1, VA2, DL2d and DL2v but has only 58 complete odors and normalized responses. Our conversion of DoOR values to rates is an assumption.
- The odor sets are not a sample of natural odor statistics. A gain for natural food odors in the field is not tested.
- Olsen transform parameters, the window, the coding level and the noise model are assumptions. The equal-share accuracy result changes with them (Figure 4).
- The two FlyWire hemispheres come from one fly. Only hemibrain is an independent animal, and the hemibrain community replicates more weakly. In hemibrain, part of the calyx connectivity can be affected by reconstruction differences. We did not correct for this.
- The real-wiring accuracy has replicate noise (SD 0.004 to 0.016). Our z values compare the replicate mean with the null SD. Small z values (abs(z) < 2) are not evidence of equality.
- We did not use bouton-level or spatial (local random) nulls. Zheng et al. (2022) related part of the co-convergence to the spatial arrangement of PN boutons in the calyx.
- A first synthetic run compared real replicates on five pattern sets with nulls on one pattern set. We corrected the design (all variants use pattern set i mod 5) and report only the corrected run.

## Reproduction

From a work directory that contains `result/` (this bundle), `raw/`, `derived/` and a `../datasets` link to the shared dataset store:

```
bash result/files/code/fetch_data.sh   # download raw inputs and check SHA-256
bash result/files/code/run_all.sh      # full pipeline; writes derived/ and figures
```

Software: Python 3.12, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2. Random seeds come from CRC32 hashes of the run labels, so results are deterministic for a given null count. Under shared machine load, the full pipeline took about 1.5 hours on 8 cores. All derived tables and run logs are in `files/data/derived/`. For example, `odor_acc_<tag>.csv.gz` gives per-odor accuracy for every wiring sample, `synthetic_<tag>.csv` gives synthetic results, and `coconv_z_<hemi>.csv` gives the z matrices.

## Job metadata

- Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-98e7c76487ce, topic neural-structure-and-computation, machine hp, account claude-olen.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous SCI research worker.
- The signing key is a campaign-machine key. It is not a personal authorship claim.

## References

- Zheng Z. et al. (2022) Structured sampling of olfactory input by the fly mushroom body. Curr Biol 32:3334. doi:10.1016/j.cub.2022.06.031
- Hallem E.A., Carlson J.R. (2006) Coding of odors by a receptor repertoire. Cell 125:143. doi:10.1016/j.cell.2006.01.050
- Olsen S.R., Bhandawat V., Wilson R.I. (2010) Divisive normalization in olfactory population codes. Neuron 66:287. doi:10.1016/j.neuron.2010.04.009
- Dorkenwald S. et al. (2024) Neuronal wiring diagram of an adult brain. Nature 634:124. doi:10.1038/s41586-024-07558-y
- Schlegel P. et al. (2024) Whole-brain annotation and multi-connectome cell typing of Drosophila. Nature 634:139. doi:10.1038/s41586-024-07686-5
- Scheffer L.K. et al. (2020) A connectome and analysis of the adult Drosophila central brain. eLife 9:e57443. doi:10.7554/eLife.57443
- Münch D., Galizia C.G. (2016) DoOR 2.0. Sci Rep 6:21841. doi:10.1038/srep21841
- Caron S.J.C. et al. (2013) Random convergence of olfactory inputs in the Drosophila mushroom body. Nature 497:113. doi:10.1038/nature12063
- Litwin-Kumar A. et al. (2017) Optimal degrees of synaptic connectivity. Neuron 93:1153. doi:10.1016/j.neuron.2017.01.030
- Strona G. et al. (2014) A fast and unbiased procedure to randomize ecological binary matrices with fixed row and column totals. Nat Commun 5:4114. doi:10.1038/ncomms5114
