# Hemibrain and FlyWire head-direction wiring share a ring form

## Summary

We examined the wiring of the fly head-direction circuit in two adult *Drosophila* connectomes: hemibrain v1.2 (one female fly, right hemibrain, central complex complete) and FlyWire v783 (one female fly, whole brain). We used six cell types: EPG, EPGt, PEG, PEN1 (PEN_a), PEN2 (PEN_b) and Delta7. There were 152 such neurons in hemibrain and 155 in FlyWire.

Ring-attractor models of this circuit need four wiring properties. (1) The neurons have an orderly map of angle. (2) Excitation is local in angle. (3) Inhibition is broad and is strongest at the opposite angle. (4) PEN neurons from the left and the right protocerebral bridge (PB) shift their ellipsoid body (EB) output in opposite directions. These properties are known from the hemibrain. We asked whether they repeat in a second animal with the same numbers, and whether the whole signed network has a leading cosine mode pair. We also asked whether neuron-level variation in the wiring makes that mode pair more symmetric than random variation of the same size.

Main results:

1. **A label-free angle map.** A spectral ring embedding of EB-only wiring gave each columnar neuron an angle. In hemibrain, this angle agreed with the PB glomerulus label. The median error for EPG neurons was 4.9 degrees (left) and 5.6 degrees (right), and the maximum error was 16 degrees (Figure 1A).
2. **PB wiring agrees with the EB map in both brains.** The PB-only partner similarity of same-side EPG pairs decreased with the EB angle difference. The Spearman correlation was -0.84 in hemibrain and -0.72 in FlyWire (permutation p < 0.001 for both; Figure 1B). A separate embedding from PB-only wiring placed EPG neurons a median 6.5 degrees (hemibrain) and 9.9 degrees (FlyWire) from their EB angle. The PB and EB wiring use different synapses, so this is an independent check.
3. **PEN outputs shift by side; PEG outputs do not.** We compared the mean EB angle of the EPG targets of each neuron in the EB with the mean EB angle of its EPG inputs in the PB. Mean shifts were: PEN1 +58 / -56 degrees (left / right PB) and PEN2 +52 / -54 degrees in hemibrain; PEN1 +54 / -53 degrees and PEN2 +50 / -48 degrees in FlyWire. Every PEN neuron with data had the sign of its side (hemibrain 37 of 37, FlyWire 41 of 41). PEG shifts were near 0 (between -3 and +1 degrees) in both brains (Figure 1C). The shift is slightly larger than one glomerulus (45 degrees).
4. **Delta7 inhibition is cosine-shaped and opposite.** The two-step weight EPG -> Delta7 -> EPG in the PB fitted a first circular harmonic with R2 = 0.98 (hemibrain) and 0.90 (FlyWire). The peak was at 178 and 176 degrees from the source. The pair-level vector strength was 0.35 and 0.41. The 99th percentile of an angle-permutation null was 0.049 and 0.057 (p < 0.001 for both, 5,000 permutations). Direct EPG -> EPG wiring in the EB is local: 89% (hemibrain) and 94% (FlyWire) of the binned weight is within 22.5 degrees (Figure 2).
5. **A cosine mode pair leads the signed network.** We made a signed linear network J (Delta7 negative, all others positive; weights are fractions of each neuron's input from these types). Its second and third eigenvalues by real part had eigenvectors that were cosine patterns over EPG angle. The cosine fraction h was 0.95 and 0.87 (hemibrain) and 0.97 and 0.95 (FlyWire). The next mode was well below the pair (0.385 against 0.581 in hemibrain; 0.506 against 0.653 in FlyWire). When we moved neurons off their angles within each type and side, h fell to a mean of 0.09 (p = 0.001 for both brains). The first eigenvalue is a mostly uniform mode (Figure 3A, B).
6. **Neuron-level variation does not make the mode pair more symmetric (null result).** The ring-pair eigenvalue split was 2.4% in hemibrain and 4.2% in FlyWire. With hemibrain glomerulus-label angles, a type x side x angle average of J had a split of 2.1% to 2.3%. Random within-type placement of the residual variation gave a median split of 2.8% to 3.3% (p = 0.28 to 0.39). Thus the real variation is not tuned to keep the pair degenerate. With connectome-inferred angles the same test gave p = 0.009 (hemibrain) and p = 0.061 (FlyWire). But the label check shows that this low p value came from angle noise in the averaged reference model, not from compensation in the wiring (Figure 3C). We report the inferred-angle result only as a caution about this type of test.

## Data

| Source | Version | Shared path (campaign) | SHA-256 |
| --- | --- | --- | --- |
| FlyWire proofread connections | v783, Zenodo 10676866 | `datasets/fly-flywire-connections-783-zenodo10676866/proofread_connections_783.feather` | `24f960ae3e7d4f8cd30db3b62e99fb5179cc3d1e76d8c155bfb441e9737d3faf` |
| FlyWire neuron annotations (Schlegel et al. 2024, Supplemental file 1) | git a83b277 | `datasets/flywire-annotations-sf1-a83b277/Supplemental_file1_neuron_annotations.tsv` | `b214970b55d2fbe0853bba536fdcb9e28730f4eb7ab06f600491df795da683cd` |
| hemibrain traced adjacencies (neuPrint export) | v1.2 | `datasets/hemibrain-v1.2-traced-adjacencies-gcs/exported-traced-adjacencies-v1.2.tar.gz` | `07d8946eb0c4e3a5cb23d5769c9817847494f9fcadbc0ca239eed7bbd5555cf7` |

This job added the hemibrain archive to the shared dataset store with the campaign dataset helper. The source URL is `https://storage.googleapis.com/hemibrain/v1.2/exported-traced-adjacencies-v1.2.tar.gz`.

The package contains the head-direction subsets that the analysis uses (`files/data/`). It does not contain the full source files. `files/provenance.json` gives the hashes of the subsets and a retrieval recipe.

Cell types and sides come from the annotations. In hemibrain, the PB side and glomerulus come from the instance name, for example `EPG(PB08)_L3`. In hemibrain, the soma side (from Supplemental file 5 of the FlyWire annotations, `https://raw.githubusercontent.com/flyconnectome/flywire_annotations/main/supplemental_files/Supplemental_file5_hemibrain_meta.csv`) agrees with the PB side for all EPG, EPGt and PEN neurons, and for 17 of 18 PEG neurons. FlyWire has no glomerulus labels for these types. Thus all FlyWire angles come from wiring. Neurotransmitter signs: Delta7 is glutamatergic (41 of 42 FlyWire Delta7 neurons have a glutamate prediction) and we treat it as inhibitory. All other types are cholinergic and we treat them as excitatory. EB and PB synapses come from the neuropil column (FlyWire) or the primary ROI table (hemibrain). Synapses outside a primary ROI are put in a third group, OTHER.

## Methods

**Angle convention (hemibrain).** We fitted the label-to-angle map from hemibrain EB EPG -> EPG wiring. EPG R_k neurons connect most to L_(9-k) and L_(10-k). Thus R_k = (k - 1) x 45 degrees and L_k = (8 - k) x 45 + 22.5 degrees. Glomerulus 9 has the angle of glomerulus 1.

**EB embedding.** For each columnar neuron (EPG, EPGt, PEG, PEN1, PEN2) we made a profile of its square-root EB input and output synapse counts with all head-direction neurons. The affinity is the cosine similarity of profiles plus the normalised, symmetrised direct EB wiring. The angle is atan2 of the two leading non-trivial eigenvectors of the normalised affinity. The two eigenvalues were 0.814 and 0.800 (hemibrain) and 0.870 and 0.831 (FlyWire). The third was 0.475 and 0.570. Thus the ring is clear in both brains. The embedding has an arbitrary rotation and reflection. For hemibrain, we aligned it to the labels with EPG neurons only. For FlyWire, the reflection is not known. All FlyWire statements use angle differences or the sign of the left PB relative to the right PB, which do not change with reflection. One FlyWire EPGt neuron had no EB wiring among these types and has no angle.

**PEN shift.** PB input angle = synapse-weighted circular mean of the EB angles of a neuron's EPG inputs in the PB. EB output angle = the same mean over its EPG targets in the EB. The shift is the circular difference. Bootstrap intervals (2,000 resamples of neurons) are in `files/results/wiring_results.json`. In hemibrain, the shift relative to the glomerulus label gave the same mean values within 5 degrees for PEN groups and within 7 degrees for PEG groups.

**Delta7 profile.** A[i, d] = synapses EPG i -> Delta7 d in the PB, divided by all EPG input to d. B[d, j] = synapses Delta7 d -> EPG j in the PB. M = AB. We normalised each row of M, then averaged it in 16 bins of angle difference and fitted a + b cos + c sin + second harmonic. The permutation test shuffles EPG angles and uses the pair-level vector strength.

**Signed network and spectrum.** J[post, pre] = sign(pre) x synapses / (all head-direction synapses onto post), with all ROIs. For each of the top 8 eigenvectors (by real part) we computed the cosine fraction over EPG neurons: h = (|sum v exp(-i theta)|^2 + |sum v exp(i theta)|^2) / (N sum |v|^2). The ring pair is the two modes with the largest h. Split = |lambda_a - lambda_b| / mean(|lambda_a|, |lambda_b|). Angles for the model: EPG and EPGt use the EB angle. PEN and PEG use the PB input angle. Delta7 uses the circular mean angle of its EPG inputs in the PB.

**Split null.** J_sym is the mean of J over all neuron pairs with the same pre and post type-side group (Delta7: type only) and the same angle-difference bin. R = J - J_sym is the neuron-level variation. With inferred angles, R is 45% (hemibrain) and 63% (FlyWire) of the Frobenius norm of J. The null is J_sym + R[p, p], where p permutes neurons within each group (1,000 permutations). We also changed the analysis choices (8 or 32 bins, K = 6 or 12 modes, raw counts, connections of 3 or more synapses only; 300 permutations each; `files/results/spectrum_robustness.csv`). With inferred angles, the hemibrain p value stayed between 0.007 and 0.027 and the FlyWire p value was between 0.040 and 0.249. The real split was always below the null median. The label-angle check (`files/results/hemibrain_label_angle_check.json`) shows that this pattern is an artefact of the reference model.

**Exploratory dynamics (not evidence).** We also tried a saturating rate model, `tau dr/dt = -r + clip(gE J+ r + gI J- r + b, 0, 1)`, started from 24 bump positions. In no tested setting did the bumps stay at their start angles. This was also true for the symmetrised network, so the model is not a valid test of attractor stability. It does not include ring neurons, other inputs or adaptation. We keep the script and its output (`files/code/exploratory_bump_model.py`, `files/results/exploratory_bump_model_*.txt`) to record this, but we make no claim from it.

## Limitations

- There are only two animals, and each connectome is one fly. The FlyWire comparison is a replication in a second animal, not a population estimate.
- FlyWire has about 4.7 times fewer PB synapses than hemibrain for the same cell types (16,275 against 76,221 here). The median EPG input to a PEN neuron in the PB is 11 to 17 synapses in FlyWire, against 62 to 77 in hemibrain. Thus FlyWire PEN shifts have wider intervals, and the PB-based tests are weaker in FlyWire. The ratio of EB synapses is about 1.9. The cause (detection or neuropil assignment) is not tested here.
- FlyWire angles come only from wiring. We validated the method in hemibrain, but not with FlyWire anatomy, because the FlyWire synapse coordinate file (9.5 GB) was too slow to download on this host. The FlyWire reflection is not known.
- The tests are about wiring structure. We did not use neural activity data. The link to function is through ring-attractor theory and published physiology, not through a new measurement.
- The linear network uses synapse counts as weights, fixed signs from transmitter predictions, and only six cell types. Ring neurons, other central complex types, gap junctions, receptor types and neuromodulation are not in the model. The spectrum results depend on these choices. The cosine mode pair was present with raw counts as well (hemibrain h = 0.70 and 0.58; FlyWire h = 0.90 and 0.75).
- The PEN shift of 48 to 58 degrees is a synapse-weighted mean. It can be slightly different from a shift measured by glomerulus or wedge counts.

## Reproduction

From `files/`, run `sh run_all.sh` (Python 3.12 with numpy, pandas, matplotlib and pyarrow). The script recomputes every number in this README and the figures from the bundled subsets. The permutation steps take about 10 to 30 minutes on a loaded 8-core host. To rebuild the subsets from the shared source files, run `code/extract_flywire.py` and `code/load_data.py` from a folder that has the shared `datasets/` folder one level up (see `files/provenance.json`).

Files:

- `files/code/load_data.py`: loaders, cell types, signs, ROI groups.
- `files/code/angles.py`: label angles, EB embedding and alignment.
- `files/code/analysis_wiring.py`: results 1 to 4 -> `results/wiring_results.json` and CSV tables.
- `files/code/model.py`, `files/code/analysis_spectrum.py`: result 5 and the inferred-angle split test -> `results/spectrum_results.json`.
- `files/code/robustness_spectrum.py`, `files/code/label_angle_check.py`: result 6 checks.
- `files/code/figures.py`: the three figures.
- `files/code/extract_flywire.py`: makes the FlyWire subsets from the shared files.

## Provenance

Job sci-1107-hp-neural-structure-and-computation-8e2d8d20e4de, topic neural-structure-and-computation, campaign 11_07_2026, machine hp. The analysis was done by the model Claude Opus 5.5 (claude-opus-5-5) through Claude Code on 2026-11-09. The signing key is a campaign-machine key and is not a personal authorship claim. Data provenance is in the table above and in `files/provenance.json`.
