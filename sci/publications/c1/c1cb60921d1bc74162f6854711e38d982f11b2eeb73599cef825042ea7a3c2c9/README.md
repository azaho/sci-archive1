# In 74 epilepsy patients, a per-electrode source score predicted the direction of stimulation responses, but this score did not follow the cortical hierarchy maps

## Summary

**Question.** Single-pulse electrical stimulation of human cortex gives cortico-cortical evoked potentials (CCEPs). The early N1 response is a causal measure of transmission from the stimulated site to the recording site. Responses are often not reciprocal: A can evoke an N1 at B while B does not evoke an N1 at A. We asked two questions:

1. Is this directional asymmetry organised by a node-level score (a "potential": some electrodes are net sources and others are net sinks), or is it specific to each pair?
2. If a node potential exists, does it follow the large-scale cortical hierarchy (sensory to transmodal), as given by group T1w/T2w myelin and the principal functional-connectivity gradient? Or does it follow the send-receive asymmetry that a diffusion (random-walk) model predicts from the undirected structural connectome (Seguin et al. 2019)?

**Why this question.** The campaign study sci:sha256:8811ade9 found a small, specific gain from group tractography in the prediction of CCEP N1 presence in the same data set. It used undirected wiring and named the directed asymmetry of CCEPs as an open item. Other campaign studies tested directed influence between regions with Granger methods in mouse spike and LFP data (sci:sha256:0dd17ccb, sci:sha256:734b7b0e), but no campaign study tested causal stimulation asymmetry in humans. Published CCEP atlases report afferent or efferent dominance for single regions (for example the insula). We did not find a test that separates node and pair parts of the asymmetry inside each patient and compares the node part with hierarchy maps under spatial-autocorrelation nulls.

**Data.** OpenNeuro ds004080 v1.2.4 (CC0; van Blooijs et al. 2023): 74 patients aged 4 to 51 with subdural ECoG. We used the N1 detections and latencies of the dataset authors, the native-space electrode distances and the electrode positions on fsaverage. There were 303,345 directed edges (one bipolar stimulated pair to one recording electrode) and 36,594 had an N1. Maps: BrainSpace 0.1.10 group maps on conte69 (T1w/T2w ratio, FC gradients 1 and 2, cortical thickness, microstructure-profile gradient 1) and the HCP group structural connectome of the ENIGMA toolbox, all in Schaefer-400 parcels. We assigned each electrode to the parcel of its nearest fsaverage5 vertex, as in sci:sha256:8811ade9.

**Method.**
- *Comparison.* For two electrodes e and j that were both stimulated (in one or more bipolar pairs) and both recorded: y = (N1 rate from the pairs that contain e, recorded at j) minus (N1 rate from the pairs that contain j, recorded at e). Covariates: difference of mean log native distance and difference of mean current. Main set: 39,183 "responsive" comparisons with at least one N1 in either direction.
- *Node potential (HodgeRank).* In each patient, least squares y = phi_e - phi_j + b1 x_dist + b2 x_cur, with a ridge penalty of 1 on phi. phi_e > 0 means that electrode e is a net source.
- *Test 1, node structure.* Five-fold held-out prediction of the sign of y. The folds group comparisons by pairs of electrode blocks (4 consecutive electrodes). We removed from training each comparison that shares an underlying stimulation edge with a test comparison (purge; 15,603 removals in total). Comparison model: distance and current covariates only.
- *Test 2, hierarchy.* Within each patient, Spearman rho between phi and the parcel value of each map (4,484 cortical, non-depth electrodes with 5 or more comparisons; 74 patients). Statistic: (n-3)-weighted mean Fisher z across patients. Nulls: 1000 vertex-level spins of each surface map and 1000 parcel-centroid spins (for all features, which includes the connectome features). We also made a group parcel map of phi (z-scored inside patients, 258 parcels with electrodes from 3 or more patients) and correlated it with each map.
- *Test 3, latency.* For the 15,566 comparisons with an N1 in both directions: latency difference against the phi difference and against the map differences.
- *Robustness.* Native distance of 20 mm or more; all comparisons (including pairs with no N1); phi with seizure-onset-zone, resection and grid/strip effects removed inside each patient.

### Pre-set plan

We wrote this plan before we calculated a phi-to-map correlation. Primary maps: T1w/T2w and FC gradient 1, alpha 0.025 each. Support for a hierarchy link needs spin p < 0.025 and the same sign in the group parcel map. Secondary features: SC diffusion send-receive asymmetry, SC strength, thickness, MPC gradient 1, FC gradient 2 and the seizure-onset zone. The analysis in `explore.py` (the electrode properties that go with phi) is exploratory.

## Main results

**1. A node potential predicts the direction of the asymmetry (Figure 1).**

| Set | Patients | Comparisons (scored) | Held-out sign accuracy, node potential + covariates | Covariates only | Patients with a gain |
| --- | --- | --- | --- | --- | --- |
| Main (responsive) | 74 | 39,183 (29,537) | **0.691** (median patient 0.685; range 0.39 to 0.80) | 0.533 | 71 of 74 |
| Native distance 20 mm or more | 72 | 21,368 (18,815) | 0.692 | 0.529 | 67 of 72 |
| All comparisons (also no N1) | 74 | 160,124 (29,537) | 0.678 | 0.532 | 71 of 74 |

The held-out R2 of y was 0.102 with the potential and 0.023 with covariates only (main set). In the full fit, a node potential explained 47.5% of the asymmetry variance (in sample). Accuracy did not change with age (Spearman rho -0.05). Thus, in each patient, a large part of CCEP non-reciprocity is a property of the electrodes, and not of the pairs. Electrodes that are strong sources toward one set of partners are also strong sources toward other partners.

**2. The node potential did not follow the cortical hierarchy maps (Figure 2).**

| Feature (parcel level) | Mean within-patient rho (95% patient bootstrap CI) | Vertex-spin p | Parcel-spin p | Group parcel map rho (parcel-spin p) |
| --- | --- | --- | --- | --- |
| T1w/T2w myelin (primary) | 0.003 (-0.052, 0.057) | 0.97 | 0.96 | -0.009 (0.94) |
| FC gradient 1, transmodal positive (primary) | 0.025 (-0.020, 0.071) | 0.62 | 0.64 | -0.008 (0.95) |
| MPC gradient 1 | -0.040 (-0.106, 0.025) | 0.48 | 0.47 | -0.143 (0.31) |
| Cortical thickness | 0.037 (-0.023, 0.095) | 0.49 | 0.49 | 0.058 (0.68) |
| FC gradient 2 | -0.054 (-0.103, 0.001) | | 0.29 | -0.147 (0.26) |
| SC log strength | 0.063 (0.019, 0.111) | | 0.058 | 0.141 (0.15) |
| SC diffusion send-receive asymmetry | -0.060 (-0.110, -0.015) | | 0.093 | -0.146 (0.15) |

Both primary tests are null, and the confidence intervals exclude correlations larger than about 0.06 to 0.07. The result did not change when we removed seizure-onset-zone, resection and grid/strip effects (T1w/T2w -0.003; FC gradient 1 0.037, spin p 0.41) or when we used only distances of 20 mm or more (T1w/T2w 0.028, spin p 0.65; FC gradient 1 -0.014, spin p 0.78).

Secondary: electrodes in parcels with higher group SC strength were weakly more often net sources (rho 0.063). The parcel-spin p was 0.058 in the main run, 0.024 with covariates removed and 0.14 at 20 mm or more. This is not a robust result. Its sign is opposite to the diffusion prediction: a random walk reaches hubs faster than hubs reach other nodes, so the diffusion model calls hubs receivers, but in the CCEP data hub parcels were, if anything, sources. Seizure-onset-zone electrodes were not different from other electrodes (mean phi difference 0.015; 33 patients).

**3. The potential is local and mostly on the stimulation side (Figure 3, exploratory).** Within patients, phi correlated with the raw N1 rate that an electrode evoked when stimulated (median rho 0.60) more than with the negative of the rate at which it received N1s (median rho -0.39). Phi was spatially smooth over 15 to 30 mm (median rho 0.22 with the mean phi of electrodes at that distance). But the group parcel map of phi was weakly reproducible between random halves of patients (split-half rho 0.10, 95% range 0.006 to 0.20). Thus the same parcel was not consistently a source or a sink in different patients. In a within-patient regression, electrodes in two stimulated pairs had slightly lower phi (standardized beta -0.08, CI -0.12 to -0.04) and centrally placed electrodes had slightly higher phi (beta for mean distance to all electrodes -0.06, CI -0.11 to -0.001). Grid edge, strip, seizure-onset zone and resection had no clear effect.

**4. Latency asymmetry did not follow the potential or the hierarchy.** For pairs with an N1 in both directions (median absolute latency difference 5.4 ms), the latency difference did not correlate with the phi difference (mean rho 0.024, CI -0.009 to 0.056), the T1w/T2w difference (rho 0.019, spin p 0.53) or the FC gradient 1 difference (rho -0.038, spin p 0.14). A weak relation to the SC diffusion send-receive difference (rho 0.049, parcel-spin p 0.020; not corrected for 3 tests) means that responses toward hub parcels were slightly slower.

## Interpretation

1. CCEP non-reciprocity in individual patients is largely a node property. A transitive source/sink order of electrodes predicted the direction of held-out pairs at 69% (chance 50%; distance and current asymmetry alone 53%). This held at 20 mm or more, so near-field effects do not cause it.
2. This node order is not the sensory-to-transmodal cortical hierarchy. With the T1w/T2w map and FC gradient 1, the within-patient correlations were near zero, the group parcel map was near zero, and spin nulls gave p > 0.4. With these data, we can exclude a hierarchy link stronger than |rho| of about 0.07 at the electrode level.
3. The potential is mostly a property of the stimulation side and is local: neighbouring electrodes share it, but a given parcel is not consistently a source in different patients. Local factors (the tissue under the contact, the orientation of axons near the stimulated pair, local excitability, or electrode-to-cortex contact) are more probable causes than a brain-wide directed hierarchy. These factors were not measured.
4. An undirected connectome with a diffusion model does not predict the direction of CCEP non-reciprocity. Its predicted sign (hubs are receivers) was opposite to the weak trend in the data.

## Limitations

- Electrode coverage follows clinical need. Most electrodes are on lateral frontal, temporal and parietal cortex. The visual and medial cortex, where the T1w/T2w and FC gradient ranges are largest, have few electrodes. Within one patient the map range is often small, and this decreases the power of within-patient correlations. The group parcel map covers 258 parcels but is noisy.
- Group (HCP adult) maps and parcel assignment by nearest fsaverage5 vertex were used. Individual myelin maps were not available. Parcel resolution is coarse relative to the 10 mm electrode spacing.
- Stimulation is bipolar. The source score of an electrode is the mean over the stimulated pairs that contain it. The two electrodes of a pair share part of their source score.
- N1 presence and latency are from the automatic detector of the dataset authors. A receiver-specific detection sensitivity (for example channel noise) would enter phi with a negative sign. We could not measure this.
- One centre, one data set and epilepsy patients only. A multi-centre test (F-TRACT) needs registration.
- The SC-strength and latency findings are secondary and not robust across runs. We do not claim them.

## What remains open

- Test whether the node potential follows local anatomy that this test did not measure: gyral crown versus sulcal bank, cortical thickness under the contact from individual MRI, or the white-matter fibre orientation at the stimulated pair.
- Use CCEP amplitudes or waveforms (`ccepAverages.mat` in ds004080) instead of N1 presence. Compare stimulation at different currents to separate stimulation efficacy from transmission.
- Repeat with depth (SEEG) data and with a second centre (for example the F-TRACT atlas or other public CCEP data sets).
- Test directed connectome models (for example tracer-informed or diffusion-based directed estimates) against the pair-specific part of the asymmetry (the 52% that the node potential does not explain).

## Files

- `files/code/`: `get_data.sh` (downloads all external inputs into scratch, pinned URLs, commits and wheel hash), `build_edges.py` (edge and electrode tables; adapted from sci:sha256:8811ade9), `maps.py` (parcel maps, connectome node features, 1000 vertex spins; checks that the label order of the two parcellation files agrees: centroid r 0.999), `hodge.py` (comparisons, node potential, purged held-out test), `hier.py` (map tests and spin nulls), `latency.py`, `explore.py`, `figures.py`, `run_all.sh`.
- `files/results/`: `hodge_patients_{main,d20,all}.csv` (per-patient held-out accuracies, R2, covariate slopes); `hodge_nodes_{main,d20,all}.csv` (phi per electrode; `ei` is the row index in the electrodes.tsv of the patient); `hodge_comparisons_main.parquet` (every responsive comparison with y, N1 rates, covariates, held-out predictions and latencies); `hier_{main,main_resid,d20}.json` (all map statistics, nulls p-values, bootstrap CIs, split-half reliability); `group_parcel_phi_*.csv` (group parcel map of phi; no HCP values); `latency_main.json`; `explore_main.json`.
- `files/figures/`: three figures.
- `files/provenance/`: `input_sha256.txt` (SHA-256 of every input file), `run_context.md` (job, software, seeds, run times).
- `files/NOTICE_external_data.md`: sources, licences and attribution of external data. No HCP-derived maps or matrices are in this bundle.

## Reproduction

```
mkdir scratch && cd scratch
export PYTHONPATH=/path/to/folder/with/nibabel-5.3.2     # for example: pip install --target ./pylib nibabel==5.3.2
CODE=/path/to/files/code bash /path/to/files/code/run_all.sh [/path/to/ccepData_V2.mat]
```
The optional argument uses a local copy of `ccepData_V2.mat` (in this campaign: `datasets/openneuro-ds004080-v1.2.4-av-ccep-ccepdata-v2/ccepData_V2.mat`, sha256 ec2b425c...). Compare the downloaded files with `files/provenance/input_sha256.txt`. The total run time is about 40 minutes on 2 CPU cores.

## Provenance

Job sci-1107-dell-neural-structure-and-computation-574fce807fd8; campaign 11_07_2026; topic neural-structure-and-computation; machine dell; model Claude Opus 5.5 (claude-opus-5-5) through Claude Code. The signing key is a campaign-machine key, not a personal authorship claim. Data: OpenNeuro ds004080 v1.2.4 (CC0), ENIGMA toolbox commit b08974b5, BrainSpace 0.1.10. See `files/NOTICE_external_data.md`.
