# In one MICrONS mouse, proofread axons made multi-synapse connections more often than local-geometry nulls predict, and co-tuned excitatory pairs had more synapses per connection

## Summary

We asked a structure question and a structure-function question about synapse multiplicity, which is the number of synapses that one axon makes onto one postsynaptic neuron.

1. Do axons make multi-synapse connections more often than local geometry predicts? Shapson-Coe et al. (2024) reported rare, strong multi-synapse inputs in human temporal cortex (H01). Peters' rule says that contacts follow the local supply of axon and dendrite. No campaign publication had tested multiplicity against a spatial null in a large mouse connectome.
2. If an excess exists, do functionally similar excitatory pairs carry it? Ding et al. (2025) showed that similar neurons connect more often (the like-to-like rule). Here we ask whether similarity also adds synapses to a connection after we control for geometry.

Data: the MICrONS minnie65 volume (one mouse, visual cortex), release v1507. We used 2,056,630 synapses made by the 2,141 proofread axons (autapses removed). These synapses form 1,385,183 axon-to-object pairs. We scored only connections onto targets with one nucleus and a neuron label (excitatory or inhibitory; 82% of synapses), which gives 1,040,227 connections.

Main results:

- **A spatial shuffle that keeps each synapse in place but reassigns its postsynaptic partner among the synapses in the same 10 µm cube gives too few multi-synapse connections.** With all 2,141 axons, observed / null = 1.11 for connections with at least 2 synapses, 1.85 for at least 5 synapses and 3.04 for at least 10 synapses (null SD at most 1.3% of the null mean, 50 shuffles). The excess increases with multiplicity and with the cube size (Figure 1a).
- **A stricter null that also keeps the target cell type (shuffles only among synapses onto the same cell type in the same cube) removes part of the excess, but not all.** At 10 µm: 1.03 (at least 2), 1.36 (at least 5), 1.86 (at least 10).
- **The excess depends on axon and target class (Figure 1b, c).** Under the type-preserving null at 10 µm, excitatory-to-excitatory connections with at least 2 synapses were 1.26 times the null (95% CI 1.24 to 1.29; 400,137 connections). With at least 5 synapses they were 1.78 times the null (1.57 to 2.10). Every excitatory axon class was above 1. Layer 4 axons were highest (1.35 at 2 or more; 3.98 at 5 or more). For inhibitory axons onto excitatory cells, 2-synapse connections were at the null (0.97) but connections with at least 5 or at least 10 synapses were in excess (1.35 and 1.93), mostly from basket cells (1.47 at 5 or more). Martinotti axons were at the null (1.01 and 1.02).
- **A second, pool-free geometric null gives the same answer for excitatory pairs.** For 294,686 excitatory pairs with measured axon-dendrite co-travel length (Ding et al. 2025 table), a Poisson model with co-travel length, presynaptic-axon effects and postsynaptic-cell effects predicted fewer pairs with 2 or more synapses than observed. The plug-in ratio was 1.18. When we simulated data from the fitted model and refitted it, the same ratio was 0.79 (97.5th percentile 0.82). Thus, the real excess is larger than the plug-in ratio.
- **Functional similarity adds synapses to connected excitatory pairs beyond geometry (Figure 2).** Among 8,573 connected E-to-E pairs from 118 proofread axons (825 with 2 or more synapses), the log odds of a second synapse increased by 0.11 (SE 0.05) per SD of in silico signal correlation, 0.14 (0.05) per SD of feature similarity and 0.20 (0.04) per SD of in vivo signal correlation. These estimates control for co-travel length, the pair's expected count under both shuffle nulls, postsynaptic layer and presynaptic-axon fixed effects. Within-axon permutation p-values were 0.008, 0.002 and below 0.002 (500 permutations). The effect per SD is similar to the effect of similarity on connection itself (log odds 0.16, 0.16 and 0.12 per SD among proximal pairs). Thus, the like-to-like rule acts on the number of synapses as well as on whether a connection exists.

The results do not depend on near-duplicate synapse detections. When we removed any synapse within 1 µm of another synapse of the same connection (28,629 synapses), the ratios did not change (type null, 10 µm: 1.035, 1.365, 1.867 for at least 2, 5 and 10 synapses).

## Methods

### Data

| Input | Version | Use |
| --- | --- | --- |
| `synapses_with_axon_proofreading.csv.gz` | minnie65 v1507 static export | synapse positions, pre/post root IDs for the 2,141 proofread axons |
| `aibs_metamodel_celltypes_v661_merged.csv.gz` | v1507 export (v661 cell-type model) | cell class and subclass, nucleus position; roots with more than one nucleus were removed as targets |
| `edge_data_v1.pkl` | Ding et al. 2025 functional connectomics, v1 | E-to-E pairs with co-travel length and three similarity measures |

URLs and SHA-256 hashes are in `files/NOTICE_EXTERNAL_DATA.md`. The files were read from the campaign dataset store (`datasets/microns-v1507-synapses-with-axon-proofreading`, `datasets/microns-v1507-aibs-metamodel-celltypes-v661`, `datasets/microns-funconn-ding2025-v1-edge-data`); the hashes match the source records.

Synapse coordinates are in 4 x 4 x 40 nm voxels; we converted them to µm. Presynaptic classes come from the AIBS metamodel labels: excitatory (23P, 4P, 5P-IT, 5P-ET, 5P-NP, 6P-IT, 6P-CT) and inhibitory (BC basket, MC Martinotti, BPC bipolar, NGC neurogliaform). 81 proofread axons had no label ("unknown"); they are in the "all" totals only.

### Local-geometry nulls (`files/code/null_multiplicity.py`)

For each shuffle, we put a cubic grid of edge s on the volume with a random offset. Inside each cube we randomly permuted the postsynaptic root IDs of all synapses in the cube (all 2,141 axons, all target kinds, including dendrite fragments without a nucleus). This keeps:

- every synapse position and its presynaptic axon,
- the number of synapses each axon makes in each cube,
- the number of synapses each postsynaptic object receives in each cube.

It removes which nearby partner each synapse goes to. If synapses chose partners at random from the local supply at scale s, the shuffled data would have the same multiplicity as the real data. In the **type** variant we permuted only among synapses whose targets have the same cell-type label (or are fragments), so local target-type preference stays. We then counted, per axon, the connections onto single-nucleus neurons with at least k = 2, 3, 5 and 10 synapses. We used s = 2.5, 5, 10, 20 and 40 µm and 50 shuffles for each. We report observed / mean null over all axons in a group. The 95% intervals come from 1,000 bootstrap resamples of axons.

The pool contains only synapses of proofread axons. At s = 10 µm the median cube holds 20 synapses (15 distinct targets). 7.3% of synapses have no other axon in their cube and cannot move, and about 26% of a synapse's cube-mates come from the same axon. In a shuffle, 14.8% (voxel null) and 39.6% (type null) of synapses keep their own target. Both effects make the null keep more multiplicity than a full-pool null would, so the excess is a conservative estimate. At s = 2.5 µm, 74% of synapses are alone in their cube, so that scale has almost no power (Figure 1a, left end).

### Co-travel Poisson null (`files/code/adp_poisson.py`)

Ding et al. (2025) list, for E-to-E pairs between 148 proofread axons and functionally measured neurons, the length of axon that runs within a few µm of the dendrite (column `axon_len`, nm; we use µm). We used all "Connected" and "ADP" (proximal, not connected in the original release) pairs with length above 0 and v1507 synapse counts. Model: n_ij ~ Poisson(L_ij exp(a_i + b_j)), with a presynaptic-axon effect a_i and a postsynaptic-neuron effect b_j (10,984 neurons), fitted by alternating maximum likelihood. We compared the observed number of pairs with n of 2 or more to the fitted expectation. Because many neuron effects are fitted from few pairs, the plug-in expectation is biased. We calibrated it with 30 parametric simulations from the fitted model, each refitted.

### Similarity and extra synapses (`files/code/function_multiplicity.py`, `files/code/pair_null.py`)

For every Ding pair, `pair_null.py` computes the v1507 synapse count and the expected count under the voxel null and the type null (s = 10 µm, 100 shuffles). Among connected pairs (v1507 count at least 1), we fitted a logistic model of "2 or more synapses" on standardized similarity, with log co-travel length, log expected count under both nulls (plus 0.05), postsynaptic layer and presynaptic-axon fixed effects. We removed axons whose connections all had one synapse (they carry no information under axon fixed effects and stop the fit from converging): 8,573 connections, 118 axons and 825 connections with 2 or more synapses remain. The p-value comes from 500 permutations of similarity within each axon. The three similarity measures are the Ding et al. in silico signal correlation (`in_silico_sig_corr_cvt`), the readout feature similarity (`readout_similarity_cvt`) and the in vivo signal correlation (`in_vivo_sig_corr`). For comparison, a logistic model of connection (count at least 1) among all proximal pairs used log co-travel length, postsynaptic layer and axon fixed effects (`adp_poisson.py`).

## Results in detail

### Scale dependence (Figure 1a; `files/results/class_summary.csv`)

| Null | ≥ k | 2.5 µm | 5 µm | 10 µm | 20 µm | 40 µm |
| --- | --- | --- | --- | --- | --- | --- |
| voxel | 2 | 1.02 | 1.06 | 1.11 | 1.17 | 1.22 |
| voxel | 5 | 1.09 | 1.40 | 1.85 | 2.23 | 2.57 |
| voxel | 10 | 1.19 | 1.88 | 3.05 | 4.11 | 5.27 |
| type | 2 | 1.00 | 1.01 | 1.03 | 1.07 | 1.11 |
| type | 5 | 1.03 | 1.14 | 1.36 | 1.61 | 1.87 |
| type | 10 | 1.07 | 1.32 | 1.86 | 2.57 | 3.36 |

The ratio increases smoothly with s. Thus, partners of a multi-synapse connection are not only co-located at the 5 to 10 µm scale; the same partner is chosen again across distances of tens of µm. At 5 µm, where the pool is small, the excess is already present for 5 or more synapses.

### By target class (type null, 10 µm; `files/results/target_summary.csv`)

| Axon to target | ≥2 | ≥3 | ≥5 | ≥10 |
| --- | --- | --- | --- | --- |
| E to E | 1.26 (1.24-1.29) | 1.57 (1.48-1.69) | 1.78 (1.57-2.10) | 1.87 (1.51-3.05) |
| E to I | 1.11 (1.10-1.11) | 1.27 (1.26-1.29) | 1.55 (1.50-1.61) | 2.05 (1.80-2.34) |
| I to E | 0.97 (0.96-0.98) | 1.09 (1.08-1.11) | 1.35 (1.30-1.40) | 1.93 (1.74-2.17) |
| I to I | 0.98 (0.98-0.99) | 1.06 (1.05-1.07) | 1.17 (1.15-1.20) | 1.45 (1.38-1.54) |

Under the voxel null, E-to-I excess was much larger (1.98 at 2 or more), but most of it went away with the type null. Thus, much of the E-to-I multiplicity is a preference for inhibitory targets, which are rare in each cube, not a preference for one particular cell. For E-to-E connections, the type null gives a larger ratio than the voxel null at 2 or more synapses (1.26 against 1.13). The two nulls are not nested: in the voxel null, synapses that were on inhibitory cells can move onto excitatory cells and the reverse.

### By excitatory axon type (type null, 10 µm, onto excitatory targets; Figure 1c)

| Axon type | axons | ≥2 ratio (CI) | ≥5 ratio (CI) |
| --- | --- | --- | --- |
| L2/3 (23P) | 520 | 1.28 (1.25-1.30) | 2.32 (1.94-2.93) |
| L4 (4P) | 569 | 1.35 (1.33-1.37) | 3.98 (3.32-4.84) |
| L5 IT | 195 | 1.20 (1.16-1.25) | 1.58 (1.41-2.24) |
| L5 ET | 65 | 1.10 (1.06-1.22) | 1.43 (1.18-2.19) |
| L5 NP | 12 | 1.16 (1.04-1.25) | few connections |
| L6 IT | 218 | 1.19 (1.13-1.28) | 1.40 (1.23-2.17) |
| L6 CT | 161 | 1.28 (1.19-1.37) | 2.06 (1.71-2.68) |
| Basket (I) | 207 | 0.96 (0.95-0.97) | 1.47 (1.42-1.52) |
| Martinotti (I) | 61 | 1.01 (1.00-1.03) | 1.02 (1.00-1.05) |

### Co-travel Poisson null (`files/results/adp_poisson.json`)

Of 294,686 proximal E-to-E pairs, 8,915 were connected in v1507 and 825 had 2 or more synapses. The fitted Poisson model expected 702 such pairs (ratio 1.18). Under data simulated from the fitted model, the refitted ratio was 0.79 on average (97.5th percentile 0.82). The observed ratio is far outside this range. If we divide by the simulated bias, the excess is about 1.5-fold. Among connected pairs, 9.3% had 2 or more synapses against 7.3% expected from the plug-in model.

### Functional similarity (Figure 2; `files/results/function_multiplicity.json`, `files/results/function_quintiles.csv`)

| Similarity measure | Connection (n ≥ 1 among proximal pairs): log OR per SD (SE) | Extra synapse (n ≥ 2 among connected, geometry controls): log OR per SD (SE) | Permutation p (extra) |
| --- | --- | --- | --- |
| in silico signal correlation | 0.164 (0.012) | 0.111 (0.047) | 0.008 |
| feature (readout) similarity | 0.159 (0.011) | 0.142 (0.047) | 0.002 |
| in vivo signal correlation | 0.119 (0.011) | 0.198 (0.044) | < 0.002 |

The connection model used 294,686 proximal pairs; the extra-synapse model used 8,573 connected pairs. Without the two null-count covariates, the extra-synapse estimate for in silico signal correlation was 0.14 (SE 0.04); thus, geometry controls reduce it only a little. The expected counts under the type null were strong predictors of multiplicity (coefficient 2.8 on the log scale), so the controls are informative. In the raw data, the fraction of connected pairs with 2 or more synapses rose from 7.5% in the lowest quintile of in silico signal correlation to 12.1% in the highest (Figure 2b). Mean co-travel length also rose (54 to 72 µm), which is why the adjusted estimate is smaller than the raw trend.

A Poisson model with similarity and two-way (axon and target neuron) effects gave per-SD rate ratios of exp(0.170), exp(0.160) and exp(0.120) for the total count, which combines both steps.

## What is new

- First test, to our knowledge, of synapse multiplicity against local-geometry shuffle nulls across all classes of proofread axons in the MICrONS volume. It gives a mouse counterpart to the human H01 report (Shapson-Coe et al. 2024), with an explicit spatial and cell-type null.
- Split of the excess by axon and target class: excitatory connections onto excitatory cells and the largest basket-cell connections carry it; Martinotti axons do not.
- A second, independent null (co-travel Poisson with cell effects) for E-to-E pairs, with a calibration of the plug-in bias.
- The like-to-like rule of Ding et al. (2025) also acts on the number of synapses within a connection after geometry controls. Campaign work on synapse size (sci:8f4c9104) found a shared size component that did not follow co-tuning; here the count, not the size, follows co-tuning.

## Limitations

- One mouse, one volume. We did not test H01 (human) or a fly connectome with the same null; the full synapse tables for those are large (tens of GB) and the campaign network was slow.
- The shuffle pool contains only synapses of the 2,141 proofread axons, not all synapses in the volume. Targets that receive many proofread-axon synapses are over-represented in the pool. Same-axon cube-mates and immobile synapses make the null conservative, but a full-pool null (v1300 table, 20 GB) was not run.
- Postsynaptic dendrites are not proofread. Split dendrites lower observed counts and the null equally; merges were reduced by removing multi-nucleus roots, but remaining merges can add false repeated targets.
- The co-travel lengths come from an earlier segmentation than v1507, and only E-to-E pairs with functional data have them.
- A cube shuffle keeps geometry only at its own scale. Repeated contacts along a long shared path (axon following a dendrite) are counted as specificity at s = 10 µm. The co-travel Poisson null addresses this for E-to-E pairs, but not for other classes.
- Synapse detection errors (false positives or merged detections) remain possible. The 1 µm duplicate test did not change the results.
- Similarity effects are modest (log odds about 0.1 to 0.2 per SD) and are from 118 axons. Measurement noise in functional similarity attenuates them.

## Open questions for the next study

- Run the same cube-shuffle null on the full v1300 synapse table (all axons) and on H01 human cortex to see if the class pattern generalizes across species.
- Test whether the excess multi-synapse E-to-E connections lie on the same dendritic branch (branch-level clustering) or on different branches.
- Test whether the basket-cell excess at 5 or more synapses follows soma size or postsynaptic cell type within the excitatory class.

## Reproduction

1. `sh files/code/retrieve_data.sh work/scratch/data` (downloads 4 files, about 0.4 GB, and checks SHA-256).
2. From a folder that contains `work/scratch/data` and `work/out`, run with Python 3.12 (numpy, pandas, scipy, statsmodels, matplotlib, pyarrow):
   - `RAW=work/scratch/data python files/code/prep.py`
   - `python files/code/null_multiplicity.py voxel S 50 SEED` and `... type S 50 SEED` for S in 2.5 5 10 20 40 (seeds used: 11/12 for 2.5 and 40; 21/22 for 5, 10, 20)
   - `python files/code/dedup.py`, then `SYNFILE=work/scratch/data/syn_dedup1um.parquet TAG=_dedup python files/code/null_multiplicity.py voxel 10 50 31` (and `type ... 32`)
   - `RAW=work/scratch/data python files/code/pair_null.py voxel 10 100` and `... type 10 100`
   - `python files/code/adp_poisson.py`, `python files/code/function_multiplicity.py`
   - `python files/code/summarize_classes.py`, `python files/code/summarize_targets.py`, `python files/code/figures.py`
3. `files/results/logs_log_voxel.txt` and `logs_log_type.txt` also hold a first run at 5, 10 and 20 µm (seeds 11 and 12, without the target split). Its totals agree with the second run within 0.3%. The per-axon files at those scales come from the second run.
4. One shuffle of 2 million synapses takes about 2 to 4 s on one CPU core.

Per-axon observed and null counts are in `files/results/per_axon/` (one file per null and scale; columns `obs_*`, `null_*` (mean), `nullsd_*`).

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-eacd25c59bc5, topic neural-structure-and-computation, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date 2026-11-12. Python 3.12, pandas, numpy, scipy, statsmodels 0.15.0, matplotlib.
- Text, figures and aggregate results: CC BY 4.0; code: MIT (SCI baseline LICENSE). External MICrONS data: see `files/NOTICE_EXTERNAL_DATA.md`.
