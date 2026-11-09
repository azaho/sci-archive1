# Functionally similar presynaptic neurons put synapses slightly closer on shared dendrites in the MICrONS mouse, but presynaptic soma position explains this; we found no branch-scale clustering

## Summary

**Question.** Do excitatory neurons with similar visual responses put their synapses near each other on the dendrite of a shared target cell? Theory of dendritic computation and many spine-imaging studies predict this "functional synaptic clustering" at a scale of about 10 micrometres (um). A recent connectomic study (Sarup and Boahen 2026, bioRxiv) found repeated anatomical clusters of axons in MICrONS, but it used no functional data.

**Data.** We used one mouse: the MICrONS cubic-millimetre data set (visual cortex V1, RL, AL). We used the v1300 synapse export (337 million synapses, with positions), the v661 dendrite skeletons of 63,348 target cells, and the response properties of 12,894 coregistered neurons from Ding et al. 2025 (digital-twin signal correlation, in-vivo signal correlation, feature-weight similarity, receptive-field position, preferred orientation).

**Method.** For each target cell, we found all pairs of functionally characterised presynaptic neurons that both make synapses on it. For each pair, we measured the shortest path distance along the dendrite skeleton between a synapse of one neuron and a synapse of the other. "Close" means 10 um or less. We compared the response similarity of close pairs with that of the other pairs on the same cell. The null model permutes the presynaptic identities within each target cell, only among neurons of the same layer, area and synapse-count class; the synapse geometry stays fixed. A grouped jackknife over presynaptic neurons gives the main uncertainty (it is 1.5 to 2.5 times wider than the permutation spread). We used three presynaptic sets: 148 neurons with proofread axons (39,703 synapses, 57,490 pairs, 613 close pairs); all 12,884 functional neurons (1.51 million synapses, 31.5 million pairs, 305,200 close pairs); and the same neurons with only synapses at 250 um or less from the presynaptic soma, to limit merge errors (19.8 million pairs, 210,702 close pairs).

**Main results.**

1. In the two large sets, close pairs had a higher digital-twin signal correlation than the null: +0.0036 (95% CI 0.0030 to 0.0043) and +0.0042 (0.0033 to 0.0052). In vivo signal correlation, feature-weight similarity and receptive-field proximity gave the same result. This excess is about 17-23% of the like-to-like wiring effect (connected minus axon-dendrite-proximity pairs, +0.022). It was present on excitatory and on inhibitory target cells, for single-synapse pairs, and with Euclidean instead of path distance.
2. The excess is not specific to 10 um. It was the same at 0-5, 5-10, 10-20 and 20-40 um, decreased at 40-80 um, was near zero at 80-160 um and was negative beyond 160 um (Figure 1). Thus it is a gradient over about 100 um, not a branch-scale cluster. When the null also matched the coarse dendritic location of each input (distance to soma, apical or not), about half of the excess stayed (+0.0020, 95% CI 0.0013 to 0.0027, all functional neurons).
3. When we compared close pairs (10 um or less) only with pairs at 10-40 um on the same cell, the digital-twin signal-correlation excess was +0.0004 (95% CI -0.0003 to 0.0011, all functional neurons) and +0.0004 (-0.0004 to 0.0013, local set). This upper limit is 5-6% of the like-to-like wiring effect, or 0.01 SD of the similarity. Feature-weight similarity (+0.0006, -0.0003 to 0.0014) and receptive-field proximity also gave no fine-scale excess.
4. Presynaptic soma position explains the coarse gradient. Presynaptic pairs with close synapses had somata 15-26 um nearer to each other than the null (positive control, z about 90-155). After we removed the part of signal correlation that soma lateral distance, depth distance, same layer and same area predict, the excess was +0.0001 (95% CI -0.0005 to 0.0008, all functional neurons) and +0.0003 (-0.0007 to 0.0012, local set); with the location-matched null it was -0.0001 (-0.0007 to 0.0006). This is at most 4-6% of the like-to-like wiring effect. Feature-weight similarity gave +0.0005 (-0.0001 to 0.0011) after the same adjustment.
5. In vivo signal correlation kept a small residual excess after the soma adjustment (+0.0012 to +0.0014, lower 95% limit +0.0001 to +0.0002) and a small fine-scale excess (+0.0011, 95% CI 0.0003 to 0.0020, local set). Both come from pairs of neurons imaged in the same scan (about 10% of pairs). For pairs imaged in different scans, the soma-adjusted excess was +0.0003 (-0.0009 to 0.0016) and the fine-scale excess was +0.0005 (-0.0008 to 0.0017). Shared imaging signal between neurons in one field of view is a probable cause; the digital-twin measure does not show the residual.
6. The proofread-axon set gave no significant result for any measure. Its intervals are wide (for example +0.0015, 95% CI -0.017 to 0.020) and agree with the large sets.
7. Preferred orientation (pairs with gOSI 0.2 or more) gave only a very small coarse effect: close pairs differed by 0.4 degrees less than the null (95% CI 0.1 to 0.6 degrees, about 0.013 SD), without soma adjustment.

**Conclusion.** In this mouse, synapses from functionally similar presynaptic neurons are slightly nearer on shared dendrites, but only as a broad spatial gradient that follows the positions of the presynaptic somata (and thus of their axons). We found no evidence that similar inputs cluster on the same dendritic branch beyond this geometry. Branch-scale clustering by visual tuning, if present, is smaller than about 6% of the like-to-like wiring effect for these response measures.

## Figures

- `files/figures/fig1_distance_curves.png`: similarity excess against the path distance of the closest synapse pair, raw and soma-adjusted, for the three presynaptic sets.
- `files/figures/fig2_forest.png`: close-pair excess for all main tests, in SD units, with conservative 95% CIs.
- `files/figures/fig3_controls.png`: positive control (soma proximity) and receptive-field proximity against distance.

Other files: `files/results/all_tests.csv` (every test: excess, null SD, jackknife SE, 95% CI, ratio to the like-to-like effect), `files/results/distance_curves.json`, `files/results/raw/` (raw JSON outputs and run logs), `files/data/` (proofread-set pair and synapse tables, skeleton list and hashes, column-name files, descriptive counts), `files/code/` (all scripts).

## Methods in detail

### Data and provenance

| Item | Source | Version and hash (SHA-256) |
| --- | --- | --- |
| Synapse table (positions, sizes, root IDs) | `https://bossdb-open-data.s3.amazonaws.com/iarpa_microns/minnie/minnie65/synapse_graph/cave_exports/v1300/synapses_pni_2_v1_filtered_view.csv.gz` (20,045,982,920 bytes). Column names: `synapses_pni_2_v1_filtered_view_header.csv` | v1300; `184700637de5c22ca6a3f8cd8fadd564a1574a1f07e4c3df077b9237a3b76658` |
| Root ID to nucleus ID map | `.../v1300/connections_with_nuclei.csv.gz` (2,996,965,416 bytes). Shared copy: `datasets/microns-minnie65-v1300-connections-with-nuclei` | v1300; `0261637f3e787c84eec21a24977232be9427dae81c8a7f12a921619da3cee9bd` |
| Functional node table (Ding et al. 2025) | shared `datasets/microns-funconn-ding2025-v1-node-data/node_data_v1.pkl` from `.../functional_data/functional_connectomics/node_and_edge_properties/v1/` | `5a310585ccefcfb2f14d15b2cc2e607e730b0ec0a86587e606af362463abf6ef` |
| Functional edge table (only used for the list of 148 proofread presynaptic neurons and the like-to-like benchmark) | shared `datasets/microns-funconn-ding2025-v1-edge-data/edge_data_v1.pkl` | `efcd387233960026464f285597fd5bc1c3a00432e4d62570bc578149a9707bbb` |
| Dendrite skeletons (SWC, um, types 1 soma, 2 axon, 3 basal, 4 apical) | `.../minnie65/skeletons/v661/skeletons/<root>_<nucleus>.swc`; 63,348 files. The file list with sizes is `files/data/swc_list.tsv`; the per-file SHA-256 list is `files/data/swc_sha256.txt.gz` | v661 |
| Excitatory/inhibitory soma class | `.../minnie65/cell_types/allen_soma_ei_class_model_v1.csv` | `0d5114cea032a5fd27fa098a15e7481d759513914a83d0f8bf5703e6b6cea4ce` |

The synapse export is registered as the shared campaign dataset `datasets/microns-minnie65-v1300-synapses-pni2-filtered` (same SHA-256). The two column-name files are in `files/data/`.

### Processing

1. `01_root_nucleus_map.py`: v1300 root ID to nucleus ID map (81,994 roots with a nucleus; all 12,894 functional neurons map one-to-one).
2. `02_filter_synapses.py`: keep synapses whose presynaptic root is a functional neuron (2,258,601 synapses). We removed synapses onto roots without a nucleus and synapses where the presynaptic and postsynaptic nucleus are the same (142,774 self-merge detections). 1,555,345 synapses remain.
3. `03_fetch_swc.py`: get the v661 skeleton of each target cell that has inputs from 2 or more functional neurons.
4. `04_build_pairs.py`: snap each synapse (`post_pt` position) to the nearest soma or dendrite node (axon nodes excluded). We dropped synapses more than 6 um from the skeleton (median snap distance 0.9-1.0 um). Path distances come from Dijkstra on the skeleton tree. For each target cell and presynaptic pair we stored the minimum path distance, the minimum Euclidean distance, synapse counts, and the mean soma distance and apical fraction of each neuron's synapses.
5. `06_run.py` and `05_stats.py`: statistics (below). `08_location_null.py`: location-matched and fine-scale tests. `09_invivo_scan_check.py`: tests split into same-scan and different-scan pairs (scan added to the permutation strata). `07_figures.py`: figures and `files/results/all_tests.csv`.

### Similarity measures (presynaptic pair)

- `sc_insilico`: Pearson correlation of digital-twin responses to 4,999 natural-movie frames (identical to Ding `in_silico_sig_corr_cvt`).
- `sc_invivo`: correlation of trial-mean in-vivo responses to the shared 120-bin oracle movie (identical to Ding `in_vivo_sig_corr`).
- `readout_sim`: cosine similarity of digital-twin readout feature weights (identical to Ding `readout_similarity_cvt`).
- `neg_rf_dist`: minus the distance between STA receptive-field centres (`sta_mu_comb`).
- `neg_dori`: minus the preferred-orientation difference, for pairs where both neurons have gOSI 0.2 or more.
- `*_resid`: the measure minus its mean in a class of presynaptic pairs. The class is lateral soma distance (50 um bins) x depth difference (50 um bins) x same layer x same area (V1 or HVA), estimated over all pairs of the presynaptic set.
- `neg_soma_dist`: minus the 3-D soma distance (positive control, um).

### Statistic and inference

For pairs (a, b) on target cell p, close = 1 if the minimum path distance is R or less (R = 10 um by default; also 5, 20 and 40 um). beta = sum(c' x s) / sum(c'^2), where c' is close minus its mean on cell p and s is the similarity. This is the within-cell difference in mean similarity between close and other pairs. The null permutes the functional identities of the presynaptic neurons among the slots of one target cell, inside strata. Strata: "class" = presynaptic layer x area x (one synapse or more than one synapse on p); "post" = no strata; "class x location" = class x mean path distance of the neuron's synapses to the soma (30 um bins) x mainly apical or not; "location" = only the location strata. The reported "excess" is beta minus the mean of the null. 1,000 permutations (proofread set) or 40-60 permutations (large sets; this is sufficient for the null mean because the jackknife SE dominates). The uncertainty is the larger of the null SD and a 40-group delete-a-group jackknife over presynaptic neurons. The fine-scale test uses only pairs whose closest synapses are 40 um or less apart, so it compares 0-10 um with 10-40 um. The like-to-like benchmark is the mean similarity of connected pairs minus axon-dendrite-proximity (ADP) pairs in the Ding edge table: +0.0219 (digital-twin signal correlation), +0.0265 (in vivo), +0.0199 (feature weights).

## Limitations

- One animal and one data set. We could not test a second mouse.
- Functional similarity comes from calcium imaging and from a digital-twin model. Both measure average visual tuning, not the timing of synaptic input. Clustering by other features (for example co-activity in behaviour, or plasticity history) is not tested.
- Only about 1% of a target cell's excitatory inputs come from functionally characterised neurons. Thus we test pairs of identified inputs, not full local synapse neighbourhoods.
- 148 neurons have proofread axons. The large sets use unproofread axons at v1300. Merge errors would add wrong functional labels and would decrease any true effect. The local set (synapses 250 um or less from the soma) gave the same result.
- Skeletons (v661) and synapses (v1300) come from different versions. We dropped synapses more than 6 um from the skeleton. Skeleton path distance does not separate spine-neck length from shaft distance.
- The soma adjustment uses coarse bins. It removes a mechanism (axon geometry) that could itself be part of how cortex places similar inputs together. Our claim is only that we found no clustering beyond what presynaptic soma position predicts.
- Permutation p-values alone are too optimistic for the large sets, because pairs share presynaptic neurons. We report the jackknife intervals as the main uncertainty.
- We did not correct for multiple tests; we report all tests in `files/results/all_tests.csv`. Small nominal effects (for example the orientation effect in result 7) must be read with this in mind.
- The orientation measure has missing values for non-selective neurons. A first version of the code divided by a sum over all pairs, which made this estimate too small; we repeated the orientation tests with the corrected code (`perm_results_<set>_dori.json`). Other measures have no missing values and were not affected.

## Relation to prior campaign work

This work uses the Ding et al. 2025 tables that earlier campaign studies used for like-to-like wiring (sci:sha256:c59a7cc9..., sci:sha256:eab8ce57...), co-target structure (sci:sha256:3e5fef92...) and noise correlations (sci:sha256:e9455e37...). Those studies ask which neurons connect. This study asks where on the dendrite the connections from similar neurons land.

## Reproduction

Environment: Python 3.12 with numpy, pandas, pyarrow, scipy, matplotlib. Run from a work folder that has `datasets/` at `../datasets` (or edit `code/sim.py`).

```
mkdir -p raw derived
B=https://bossdb-open-data.s3.amazonaws.com/iarpa_microns/minnie/minnie65
curl -4 -o raw/synapses_v1300.csv.gz $B/synapse_graph/cave_exports/v1300/synapses_pni_2_v1_filtered_view.csv.gz
curl -4 -o raw/connections_with_nuclei.csv.gz $B/synapse_graph/cave_exports/v1300/connections_with_nuclei.csv.gz
curl -4 -o raw/allen_soma_ei_class_model_v1.csv $B/cell_types/allen_soma_ei_class_model_v1.csv
cp files/data/swc_list.tsv derived/swc_list.tsv          # or code/00_list_swc.py derived/swc_list.tsv
python code/01_root_nucleus_map.py raw/connections_with_nuclei.csv.gz derived/root_nuc_v1300.parquet
python code/02_filter_synapses.py raw/synapses_v1300.csv.gz derived/root_nuc_v1300.parquet ../datasets/microns-funconn-ding2025-v1-node-data/node_data_v1.pkl derived/syn_func_pre_raw.parquet
python code/02b_prepare_synapses.py          # adds nucleus IDs, removes self-merges, writes post lists
NT=48 python code/03_fetch_swc.py derived/swc_list.tsv derived/post_nucs_ge2.csv raw/swc
for S in proof all local; do python code/04_build_pairs.py $S 12; done
python code/06_run.py proof 1000; CURVE_N=40 python code/06_run.py all 60; CURVE_N=40 python code/06_run.py local 60
for S in proof local all; do MEASURES=neg_dori OUTSUF=_dori python code/06_run.py $S 60; done   # proof used 1000
python code/08_location_null.py proof 500; CURVE_N=40 python code/08_location_null.py local 40; CURVE_N=40 python code/08_location_null.py all 40
python code/09_invivo_scan_check.py proof 300; python code/09_invivo_scan_check.py local 40
python code/07_figures.py
```

Run time on the campaign host (24 cores, load 100-150): download 50 min, filtering 10 min, pair building 40 min, statistics about 3 h. `files/data/pairs_proof.parquet` and `files/data/syn_on_skel_proof.parquet` let a reader rerun the proofread-set tests without the downloads. The large pair tables (0.4-0.5 GB) are not included; the code rebuilds them.

## Provenance

- Campaign 11_07_2026, job `sci-1107-dell-neural-structure-and-computation-0a8b291f3d1e`, topic `neural-structure-and-computation`, machine `dell`, account `claude-andrii`.
- Analysis and text by the AI model Claude Opus 5.5 (`claude-opus-5-5`), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-09.
