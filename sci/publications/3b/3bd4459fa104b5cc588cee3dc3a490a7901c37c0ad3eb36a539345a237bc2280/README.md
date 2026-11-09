# A person's own structural connectome predicts that person's resting functional connectivity only slightly better than other people's connectomes

## Summary

Structural connectivity (SC) from diffusion MRI predicts resting functional connectivity (FC) at the group level.
We asked a different question: **is the structure–function link specific to the individual?** That is, does the
SC of person *s* predict the FC of person *s* better than the SC of another person *t* does?

We used two independent adult cohorts that are available in the shared campaign store:

| Cohort | People | Diffusion method | Parcellations |
|---|---|---|---|
| MICA-MICs (Royer et al. 2022) | 50 | multi-shell, probabilistic tractography, SIFT2 weights | Schaefer 400 |
| Lausanne (Griffa et al. 2019) | 69 / 67 / 54 with FC | DSI, deterministic tractography, fibre density | Lausanne 219 / 448 / 1000 cortical nodes |

For each pair of people we computed a coupling value C[s, t] = correlation over edges between the FC of person *s*
and the SC of person *t*. We then compared own pairs (s = t) with other pairs (s ≠ t). We did this at four levels:
the raw rank values, the person deviations from the group pattern (after a per-person distance and hemisphere
model), the edge-specific deviations (after we also removed additive node effects), and the node effects alone.

Main results:

1. **There is a real own-person advantage, and it is edge-specific.** After we removed the group pattern, distance
   and node effects, own coupling was r = 0.018 in MICA-MICs (others: −0.0004; 95% bootstrap interval of the
   difference 0.007–0.029; label-shuffle p < 0.001) and r = 0.005–0.007 in the three Lausanne parcellations
   (all intervals above zero). The own SC was above the mean of the other SCs for 78% (MICA-MICs) and 78–94%
   (Lausanne) of people (Figures 1A, 2).
2. **The advantage is very small.** In the raw coupling, the own SC added only 0.003–0.006 to a group-level
   rank correlation of 0.07–0.21 (2–5%). The edge-specific own correlation of 0.005–0.018 corresponds to
   0.003–0.03% of the variance of a person's edge-level FC deviations. The FC deviations themselves are reliable:
   the FC from the first half of a MICA-MICs scan correlates with the FC from the second half at r = 0.49 at the
   same level, and identifies 100% of people (Figure 1C). So the small structure–function value is not caused by
   unreliable FC.
3. **Many small edge values add up to identification above chance.** From the edge-specific values, the own SC
   was the best match for 24% of people in MICA-MICs (chance 2%) and for 20% (rank values) to 43% (log values) in
   Lausanne-1000 (chance 2%). At coarse Lausanne resolution (219 nodes) identification was near chance.
4. **Node effects did not carry a clear own-person signal.** Person-specific node strength in SC and FC gave
   wide intervals that include zero in all four sets (Figure 1A, "node effects").
5. **The two cohorts differ in where the advantage lives.** In MICA-MICs it is present at all edge distances
   (each distance quintile 0.015–0.025) and between hemispheres. In Lausanne it is concentrated in short
   intra-hemispheric edges: it falls from 0.010–0.015 in the shortest distance fifth (< 54 mm) to about zero
   above about 93 mm, and it is near zero between hemispheres (Figure 1B, 3A). Lausanne uses deterministic
   tractography, which is known to miss long and crossing tracts; the edges that most people share (structural
   support ≥ 50%) carried an advantage of 0.017–0.021.
6. **The controls do not remove the result.** It stayed after we removed edges shorter than 30 mm, after we added
   each person's own geodesic distance as a covariate (MICA-MICs, intra-hemispheric), with log SC and Fisher-z FC
   instead of ranks, with FC from either half of the scan, and with SC communicability (indirect paths) instead of
   direct SC. People with neighbouring IDs (a proxy for scan order) did not couple more than distant IDs
   (Figure 3B), so slow scanner drift does not explain it.

Interpretation: in human cortex, the structure–function relation that diffusion MRI can measure is almost all
shared between people. Each person's own wiring adds a small, edge-specific part that is statistically clear in
two cohorts with different acquisition and tractography methods, but it explains a negligible fraction of how one
person's FC differs from another's. Most of the reliable individual FC variation (split-half r ≈ 0.5) is not
predicted by the individual SC that these pipelines measure. This agrees with the conclusion of Zimmermann et al.
(2019) that SC–FC correspondence is weakly subject-specific, and it adds three facts: the specific part is
edge-level, not node-level; it is larger in absolute value with SIFT2 probabilistic tractography; and it is
limited to short connections in the deterministic DSI data.

## Data

| Item | MICA-MICs | Lausanne |
|---|---|---|
| Source | Royer et al. 2022, OSF j532r, micapipe v1.1 (CC0) | Griffa et al. 2019, Zenodo 2872624 (CC BY 4.0) |
| Shared store path | `mica_mics_micapipe_v1.1_extract/v1/schaefer400.npz` | `lausanne_2019_70_connectomes/v1/Individual_Connectomes.mat` |
| People used | 50 (all; ses-01) | 69 (scale 125), 67 (250), 54 (500); people without valid FC excluded per scale |
| SC | SIFT2 streamline weights, 98% dense | DSI deterministic fibre density, about 12% dense |
| FC | Pearson r of the released time series; also from each half | Pearson r of rs-fMRI time series |
| Node positions | Schaefer CBIG centroids (MNI mm) | netneurotools Lausanne centroids |
| Edges | 79,800 (39,800 intra, 40,000 inter) | 23,871 / 100,128 / 499,500 |

Exact file hashes, node-order checks and a retrieval recipe are in `files/PROVENANCE.md`. The raw matrices are
not copied into this bundle; they are in the shared campaign store and at the original URLs.

## Methods

All code is in `files/code/`. Each step below names the function that does it.

1. **Transform (`common.rank_rows`).** For each person, edge values were rank-transformed across edges and
   standardised. Sensitivity: log(SC + half the smallest positive value) and Fisher-z FC (`transform="log"`).
2. **Deviation model (`common.residualize`).** For each person, SC and FC edge vectors were regressed on the group
   mean pattern (mean over all people of the same data set), a cubic polynomial in log Euclidean distance, an
   intra-hemispheric indicator and its interactions with distance. Each person has their own coefficients. So the
   residual removes the person's own global scale, own distance slope and own hemisphere difference.
   The group mean includes every person; this keeps the label-shuffle test exact.
3. **Node effects (`common.node_effects`).** The deviation of edge (i, j) was fitted as a_i + a_j by least squares.
   The fitted a are the node effects. The remainder is the edge-specific deviation.
4. **Coupling matrix (`common.corr_matrix`).** C[s, t] = Pearson r between the FC vector of person s and the SC vector
   of person t (over edges, or over nodes for node effects).
5. **Statistics (`common.specificity`).** Δ = mean(own) − mean(other). Label-shuffle null: 10,000 random
   permutations of the SC labels (5,000 in the controls). 95% interval: 2,000 bootstrap resamples of people.
   Identification: fraction of people whose own SC gives the highest C in their FC row (and the reverse).
6. **Edge sets.** All cortical edges (primary), intra-hemispheric, inter-hemispheric.
7. **Controls (`run_distance_bins.py`, `run_specificity.py`).** Distance quintiles; removal of edges < 30 mm before
   the full pipeline; edges with SC present in ≥ 50% of people vs the rest; own geodesic distance as an extra
   per-person covariate (MICA-MICs, intra-hemispheric); FC from each half of the scan; SC communicability
   (Estrada & Hatano) of the normalised SC; ID-adjacency test (`make_figures.py`); planted-signal test.
8. **Positive control and ceiling.** FC of half 1 vs FC of half 2 for each MICA-MICs person, at the same levels.
9. **Networks (`run_networks.py`).** MICA-MICs edge-specific Δ for edges inside and leaving each Yeo-7 network.

## Results

### Primary results (rank transform, all cortical edges, SC as predictor)

| Data set | People | Level | Own r | Other r | Δ (95% CI) | Shuffle p | Own > mean of others | ID (chance) |
|---|---|---|---|---|---|---|---|---|
| MICA-MICs 400 | 50 | raw | 0.210 | 0.205 | 0.006 (−0.006, 0.019) | 0.0004 | 66% | 8% (2%) |
| MICA-MICs 400 | 50 | deviation | 0.019 | −0.000 | 0.020 (0.003, 0.034) | 0.0001 | 68% | 8% (2%) |
| MICA-MICs 400 | 50 | edge-specific | 0.018 | −0.000 | 0.018 (0.007, 0.029) | 0.0001 | 78% | 24% (2%) |
| MICA-MICs 400 | 50 | node effects | 0.022 | −0.000 | 0.022 (−0.014, 0.052) | 0.026 | 62% | 2% (2%) |
| Lausanne 219 | 69 | raw | 0.172 | 0.169 | 0.003 (−0.001, 0.008) | 0.0003 | 71% | 3% (1%) |
| Lausanne 219 | 69 | edge-specific | 0.006 | −0.000 | 0.006 (0.003, 0.009) | 0.0001 | 78% | 1% (1%) |
| Lausanne 219 | 69 | node effects | 0.013 | −0.000 | 0.013 (−0.018, 0.045) | 0.11 | 52% | 6% (1%) |
| Lausanne 448 | 67 | raw | 0.127 | 0.123 | 0.004 (0.001, 0.007) | 0.0001 | 81% | 3% (1%) |
| Lausanne 448 | 67 | edge-specific | 0.007 | −0.000 | 0.007 (0.004, 0.009) | 0.0001 | 90% | 4% (1%) |
| Lausanne 448 | 67 | node effects | 0.012 | −0.000 | 0.012 (−0.011, 0.036) | 0.054 | 51% | 3% (1%) |
| Lausanne 1000 | 54 | raw | 0.076 | 0.073 | 0.003 (0.001, 0.005) | 0.0001 | 78% | 7% (2%) |
| Lausanne 1000 | 54 | edge-specific | 0.005 | −0.000 | 0.005 (0.003, 0.006) | 0.0001 | 94% | 20% (2%) |
| Lausanne 1000 | 54 | node effects | 0.002 | −0.000 | 0.002 (−0.016, 0.020) | 0.36 | 56% | 2% (2%) |

The shuffle p values for own vs other are small even where the bootstrap interval includes zero (raw level):
the shuffle null keeps the people fixed, while the bootstrap also samples variation between people. We base
conclusions on the bootstrap interval. With log SC and Fisher-z FC the edge-specific Δ was larger:
0.025 (MICA-MICs), 0.011 / 0.011 / 0.007 (Lausanne), and identification rose to 34% (MICA-MICs) and 43%
(Lausanne 1000). The full table (122 rows) is `files/results/specificity_summary.csv`.

### Positive control: FC split halves (MICA-MICs)

| Level | Own r (half 1 vs half 2) | Other r | Identification |
|---|---|---|---|
| raw | 0.710 | 0.419 | 98% |
| deviation | 0.501 | −0.010 | 98% |
| edge-specific | 0.488 | −0.010 | 100% |
| node effects | 0.517 | −0.010 | 90% |

The pipeline detects individual FC structure easily. The SC → FC own advantage is 25–30 times smaller than the
FC → FC own advantage at the same level. SC predicted FC from half 1 and from half 2 to a similar degree
(edge-specific Δ 0.016 and 0.015).

### Controls

| Control | MICA-MICs | Lausanne 219 | Lausanne 448 | Lausanne 1000 |
|---|---|---|---|---|
| Edge-specific Δ, intra-hemispheric | 0.023 (0.010, 0.035) | 0.009 (0.005, 0.014) | 0.010 (0.006, 0.013) | 0.007 (0.005, 0.008) |
| Edge-specific Δ, inter-hemispheric | 0.013 (0.000, 0.024) | −0.000 (−0.004, 0.004) | 0.002 (−0.001, 0.004) | 0.002 (−0.000, 0.004) |
| Edges ≥ 30 mm only (full pipeline again) | 0.017 (0.006, 0.027) | 0.005 (0.001, 0.008) | 0.005 (0.003, 0.007) | 0.003 (0.002, 0.004) |
| Shortest distance fifth | 0.025 (0.012, 0.037) | 0.015 (0.009, 0.023) | 0.015 (0.011, 0.019) | 0.011 (0.008, 0.013) |
| Longest distance fifth | 0.019 (0.006, 0.033) | 0.001 (−0.007, 0.008) | 0.001 (−0.005, 0.006) | −0.000 (−0.003, 0.002) |
| Edges with SC in ≥ 50% of people | 0.019 (0.007, 0.029) | 0.021 (0.010, 0.032) | 0.020 (0.012, 0.030) | 0.017 (0.009, 0.027) |
| SC communicability instead of SC | 0.023 (0.008, 0.037) | 0.008 (−0.001, 0.017) | 0.007 (0.000, 0.014) | 0.006 (0.002, 0.011) |
| Own geodesic distance added (intra) | 0.023 (0.010, 0.035) | n/a | n/a | n/a |
| Neighbouring IDs (lag 1) minus far IDs | −0.001 | −0.001 | −0.001 | −0.000 |

Planted-signal test: when we added an artificial own coupling of r = 0.01 to label-shuffled data, the test
detected it in 20 of 20 repeats in all four sets, and the false-positive rate at r = 0 was 0–5%.
So the design can see effects of the observed size; a null result would not have been caused by low power.

By Yeo-7 network (MICA-MICs, edge-specific, edges that leave the network), Δ was 0.009–0.023 for all seven
networks; somatomotor (0.009) and limbic (0.011) had intervals that include zero, but all intervals overlap.
We do not find a clear association-versus-sensory difference (`files/results/network_results.json`).

## Figures

- `files/figures/fig1_own_advantage.png`: (A) Δ with 95% bootstrap intervals for the four levels and four data sets;
  (B) edge-specific Δ by distance quintile; (C) own SC → FC coupling vs own FC half 1 → half 2 reliability.
- `files/figures/fig2_matrices_rank.png`: edge-specific coupling matrices for MICA-MICs and Lausanne 448, and the
  cumulative distribution of the percentile of the own SC among all SCs for each person.
- `files/figures/fig3_controls.png`: (A) edge sets and predictor variants, including the ≥ 30 mm exclusion;
  (B) coupling by ID difference; (C) observed Δ vs the 95th percentile of the label-shuffle null.

## Limitations

- **Effect size, not existence, is the main result.** The own-person advantage is statistically clear but very small.
  Do not read it as evidence that individual SC is a useful predictor of individual FC.
- **No SC test–retest.** We could estimate FC reliability (split halves of one scan) but not SC reliability. If
  individual SC is very unreliable, the true individual link could be larger than what we measure. A correction
  is not possible with these data. The FC split halves come from the same session, so they overestimate the
  reliability of FC between sessions.
- **Shared session factors.** SC and FC of a person come from the same scan session and the same anatomical
  registration and parcellation. Person-specific parcel boundaries, distortion or partial-volume effects can
  produce matched deviations in both modalities. Distance modelling per person, node-effect removal, the 30 mm
  exclusion and the own-geodesic covariate reduce this risk but cannot exclude it. In Lausanne the advantage is
  concentrated in short edges, where such effects are strongest; that part of the result is the least certain.
- **No head motion or demographic data** were available in the shared files, so we could not regress them out.
  Motion that affects both modalities in a person-specific, edge-specific way could contribute.
- **Two pipelines, one per cohort.** Cohort and method are confounded: we cannot say if the difference between
  MICA-MICs and Lausanne comes from SIFT2 probabilistic vs deterministic DSI tractography, from the parcellation
  or from the people.
- **Linear correlations only.** We did not fit nonlinear or learned SC → FC models. These can produce larger
  group-level fits, but the individual-specific part has been small in published learned models too.
- **Adults only, resting state only, cortex only.**

## Reproduce

```
export SCFC_DATASETS=/path/to/shared_datasets      # folder with the three dataset folders in files/PROVENANCE.md
export OMP_NUM_THREADS=1
cd files
python code/run_specificity.py results     # about 12 min on one CPU; writes specificity_results.json, coupling_matrices.npz
python code/run_distance_bins.py results   # about 15 min; writes control_results.json
python code/run_networks.py results        # about 2 min; writes network_results.json
python code/make_figures.py results figures
```

Python 3.12, numpy, scipy, pandas, matplotlib. Seeds are fixed in the code (`specificity(seed=0)`,
`run_distance_bins` rng seed 1). Run logs from this study are in `files/results/logs/`.

## Files

- `files/code/common.py`: loaders, transforms, deviation model, node-effect model, specificity statistics.
- `files/code/run_specificity.py`, `run_distance_bins.py`, `run_networks.py`, `make_figures.py`.
- `files/results/specificity_summary.csv` (and `.json`): every configuration. `control_summary.csv`
  (and `control_results.json`): distance, support, 30 mm and planted-signal controls. `network_results.json`.
  `id_order_control.csv`. `coupling_matrices.npz`: every C matrix (float32; key
  `dataset|edges|transform|predictor|level`; rows FC person, columns SC person, in data-set person order).
- `files/PROVENANCE.md`: job, input paths, hashes, node-order checks, retrieval recipe.

## Provenance and credit

Job sci-1107-dell-neural-structure-and-computation-958fa6a6ea1d, campaign 11_07_2026, topic
neural-structure-and-computation, machine dell, model Claude Opus 5.5 (claude-opus-5-5) in Claude Code,
2026-11-08. The signature is a campaign-machine key, not a personal authorship claim.
Data: MICA-MICs (Royer et al. 2022; CC0) and the Lausanne 70-person connectomes (Griffa, Alemán-Gómez &
Hagmann 2019; CC BY 4.0). Parcellations: Schaefer et al. 2018; Cammoun et al. 2012 (via netneurotools).
Earlier campaign workers made the shared extracts that we read. This campaign has published group-level
structure–function coupling tests in mouse (fMRI vs tracer connectome), fly and C. elegans; this study adds the
individual-level question in humans.
