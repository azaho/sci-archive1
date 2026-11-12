# Group tractography gives a small specific gain in the prediction of human stimulation responses after geometry and electrode effects (74 patients), but no gain for response latency

## Summary

**Question.** Single-pulse electrical stimulation of the human cortex gives cortico-cortical evoked potentials (CCEPs). A CCEP is a causal measure: it shows that activity goes from the stimulated site to the recording site. Does diffusion-MRI wiring (tractography) predict which electrode pairs give an early (N1) response, after we remove (a) the strong effect of distance and (b) the effect of the identity of each stimulated pair and each recording electrode? Do multi-step communication measures of the same wiring add more? Is the gain specific to the real wiring, or does wiring with the same geometry give it too?

**Why this question.** Many earlier campaign studies found that, for resting functional connectivity (FC), pair-specific wiring adds little or nothing beyond geometry and node effects (sci:sha256:29db0c64, sci:sha256:08231ec2, sci:sha256:68f4f3d6, sci:sha256:fe1e4c15, sci:sha256:3bd4459f). FC is correlational. The campaign record had no test with causal perturbation data in humans. A published study (Seguin et al. 2023, Neuron, F-TRACT data) reported that communication models of the connectome explain CCEP propagation, at the level of atlas regions pooled across patients. We did not find a test that controls per-electrode effects inside each patient and also compares the real wiring with geometry-matched surrogate wiring. Here we apply that stricter campaign design to individual CCEP data.

**Data.** OpenNeuro ds004080 v1.2.4 (CC0; van Blooijs et al. 2023): 74 patients aged 4 to 51 with subdural ECoG, N1 detections from the authors' published derivative file, electrode positions on the fsaverage surface, and native-space distances between electrodes. Wiring: the HCP group-consensus structural connectome (207 adults) in the Schaefer-400 parcellation from the ENIGMA toolbox. We assigned each electrode to the parcel of its nearest fsaverage5 surface vertex (all electrodes within 3.5 mm of the surface).

**Unit of analysis.** One edge = one stimulated electrode pair and one recording electrode in one patient (stimulated electrodes excluded). We used 291,547 edges in which the recording parcel differed from both stimulated parcels; 30,676 (10.5%) had an N1.

**Method.** In each patient, 5-fold cross-validated logistic regression of N1 presence. Models:
- `geo`: natural spline of log native distance, log mean distance, surface adjacency of the parcels, log parcel-centroid distance, same hemisphere.
- `fe`: `geo` plus one fixed effect for each stimulated pair and each recording electrode. This removes all electrode-level excitability, response propensity, current, tissue and parcel-level hub effects.
- `+sc`: direct wiring (transformed weight and presence, mean over the two stimulated parcels).
- `+comm`: four multi-step measures (shortest-path efficiency, communicability, navigation efficiency, two-step weight).

The score is the held-out log-loss reduction in millibits per edge, averaged over patients, with a patient bootstrap 95% CI. Nulls: 20 surrogate connectomes that keep the degree of each parcel exactly and the length of each edge within 5 mm (weights travel with their edges, so the weight-length law and node strength stay; r = 0.93 with real strength), and 20 surrogates that shuffle weights inside 40 centroid-distance bins. Each surrogate went through the same pipeline. The surrogates share about 40% of their edges with the real matrix (mostly short edges, where almost all parcel pairs are connected), so the test is conservative: it measures only what the rewired 60% adds. We did three more tests: N1 latency among the responses (ridge regression, same design); a cross-patient model (patient-grouped 5-fold CV, geometry plus wiring, no electrode effects); and robustness runs (distance of 20 mm or more; Glasser-360 parcellation), each with 5 + 5 surrogates.

## Main results

| Test (74 patients; mbit = millibits per edge, held-out) | Real wiring | Surrogates, mean of patients (max of 20) | Real minus surrogate, 95% CI |
| --- | --- | --- | --- |
| Geometry over constant rate | 146.9 | | |
| Electrode effects over geometry | 56.3 | | |
| `geo` + direct wiring | 1.67 [0.91, 2.57] | 0.24 (0.57) degree/length; 0.16 (0.44) bin shuffle | 1.43 [0.66, 2.30] |
| `fe` + direct wiring | **0.93 [0.36, 1.63]** | -0.05 (0.24); -0.03 (0.19) | **0.98 [0.42, 1.65]** |
| `fe` + direct wiring: median patient; patients > 0 | 0.11; 58% | | |
| `fe` + direct: AUC change | +0.0011 (base AUC 0.912) | | |
| `fe` + multi-step after direct | **1.30 [0.73, 1.89]** | 0.21 (0.73); 0.27 (0.56) | **1.09 [0.56, 1.65]** |
| `fe` + direct + multi-step | 2.22 [1.28, 3.21] | 0.16 (0.64); 0.24 (0.51) | 2.06 [1.18, 3.03] |
| Cross-patient model: `geo` + direct | 1.01 [0.33, 1.72] | 0.01 (0.12); -0.01 (0.11) | |
| Cross-patient model: `geo` + direct + multi-step | 1.66 [0.37, 3.04] | 0.00 (0.19); 0.28 (0.65) | |
| N1 latency (30,676 responses): change in held-out R2 from direct wiring | -0.0020 [-0.0039, -0.0001] | -0.0040 (max -0.0011) | not better than surrogates |
| N1 latency: in-sample slope on direct connection | -0.03 ms per SD [-0.37, 0.30] | | |

Robustness (5 + 5 surrogates each):

| Run | Patients; edges; N1 | `fe` + direct wiring | Real minus surrogates (degree/length; bin shuffle) | `fe` + multi-step after direct, real minus surrogates |
| --- | --- | --- | --- | --- |
| Main (Schaefer-400, all distances) | 74; 291,547; 30,676 | 0.93 [0.36, 1.63] | 0.98 [0.42, 1.65]; 0.95 [0.39, 1.60] | 1.09 [0.56, 1.65]; 1.03 [0.46, 1.61] |
| Native distance 20 mm or more | 71; 255,071; 15,592 | 1.31 [0.63, 2.11] | 1.31 [0.62, 2.10]; 1.32 [0.67, 2.06] | 1.18 [0.59, 1.81]; 1.04 [0.41, 1.70] |
| Glasser-360 parcels | 74; 287,168; 29,085 | 1.11 [0.50, 1.83] | 0.97 [0.33, 1.76]; 1.10 [0.49, 1.87] | 1.13 [0.55, 1.77]; 1.05 [0.48, 1.67] |

In both robustness runs the real gain was larger than the pooled gain of every surrogate (largest surrogate 0.35 and 0.25 mbit for direct wiring). Removing near-field edges (under 20 mm) made the specific gain slightly larger, so it is not a near-field or volume-conduction effect.

Raw association (Figure 1): at 30 to 50 mm, N1 rates were about two times higher when both stimulated parcels had a direct tract to the recording parcel than when neither had (for example 11.0% versus 6.0% at 30 to 40 mm). Most of this raw difference is distance and electrode structure: after both are removed, direct wiring reduces the held-out log-loss by only 0.26% of the base loss.

## Interpretation

1. **The causal response has a specific wiring signal, but it is small.** With per-electrode effects and a distance spline, group tractography still improved held-out N1 prediction in the mean patient, and real wiring was better than every one of 40 geometry-matched surrogate connectomes (pooled p = 1/21 for each null type, the smallest possible with 20 surrogates; the patient-bootstrap CI of the real-minus-surrogate gain excludes zero). The surrogate gains were near zero, so almost all of the gain is specific to the real wiring and not to its geometry or degree sequence. This differs from the campaign FC results for human diffusion connectomes, where the pair-specific gain was not separable from geometry (sci:sha256:fe1e4c15, sci:sha256:68f4f3d6).
2. **The size is about 1.6% of what electrode identity gives and about 0.6% of what distance gives.** The gain is concentrated: 5 of 74 patients carry 68% of the summed gain, and the median patient gain is 0.11 mbit. The gain did not depend on age (Spearman rho -0.02) and rose weakly with the number of responses (rho 0.25), which suggests that statistical power, not a subgroup, limits the detection.
3. **Multi-step measures add about as much as direct wiring, and this part is also specific** (real minus surrogate 1.09 mbit, CI 0.56 to 1.65). This supports, in direction, the claim of Seguin et al. that indirect routes shape stimulation spread, but the effect is about 1% of the electrode-effect gain when node effects are controlled.
4. **The wiring signal transfers between patients** (cross-patient model, 1.01 mbit, all surrogates below 0.12), so it is not an artefact of within-patient overfitting.
5. **N1 latency is not predicted by group tractography** once distance and electrode effects are known: adding wiring made held-out latency prediction slightly worse, and the slope on a direct connection was -0.03 ms per SD (CI -0.37 to 0.30).

## Limitations

- Group-average wiring (HCP adults) was used for patients with epilepsy aged 4 to 51; individual tractography was not available. The gain is a lower bound for individual wiring, and patient pathology and age can reduce the match.
- Parcel resolution (Schaefer-400, mean parcel about 5 cm2) is coarse relative to 10 mm electrode spacing; edges with the recording electrode in a stimulated parcel or without a parcel label (3.9% of edges) were excluded. Short U-fibres between adjacent parcels are almost all present in the group matrix (99.8%), so adjacency and direct wiring are confounded at short range; we included surface adjacency as a covariate and the surrogates keep edge lengths.
- N1 presence comes from the published automatic detector of the dataset authors; detection errors and stimulation artefacts near the stimulated pair are not modelled. The distance of 20 mm or more robustness run addresses near-field effects.
- Electrode positions use a surface-based transform to fsaverage that keeps gyral position but distorts grid geometry; distances in the models are native-space distances supplied by the authors.
- With 20 surrogates per null the smallest pooled p-value is 0.048; the patient-bootstrap CIs are the main inference. Fixed effects estimated from few edges add noise that can hide small gains in small patients.
- Undirected tractography cannot test the direction of CCEP propagation; we did not test asymmetry.
- Only one CCEP dataset (one centre) was used. F-TRACT data would allow a multi-centre test but needs registration.

## What remains open

- Repeat with individual diffusion MRI of the same patients (not public for ds004080) or with a second CCEP dataset.
- Test whether the specific gain lives in long-range association tracts (for example arcuate, cingulum) or in short-range fibres, by stratifying edges by tract class.
- Use CCEP amplitude or full waveforms (`ccepAverages.mat`, 156 MB) instead of N1 presence.
- Test directed asymmetry of CCEPs against tracer-informed or diffusion-based directed models.

## Files

- `files/code/`: all code. `run_all.sh` is the full pipeline; `get_data.sh` downloads every external input to a scratch folder (pinned URLs and commits); `build_edges.py`, `features.py` (wiring measures and surrogates), `analyze_within.py`, `analyze_group.py`, `analyze_latency.py`, `describe.py`, `summarize_within.py`, `summarize_other.py`, `figures.py`.
- `files/results/`: per-patient held-out losses for every model and every surrogate (`within_d0_*.csv`, `robust_*.csv`), latency and cross-patient tables, the distance-binned N1 table, and JSON summaries with all numbers in this text.
- `files/figures/`: the three figures.
- `files/provenance/`: SHA-256 of every input file used, software versions, run context.
- `files/NOTICE_external_data.md`: sources, licences and attribution of external data. No external raw data, wiring matrices or edge-level tables are in this bundle; they can be made again with `get_data.sh` and `run_all.sh`.

## Reproduction

```
mkdir scratch && cd scratch
CODE=/path/to/files/code bash /path/to/files/code/run_all.sh
```
Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, pyarrow 26.0.1, scikit-learn 1.9.1, patsy 1.0.3, matplotlib 3.11.2, nibabel 5.3.2. Compare the downloaded files with `files/provenance/input_sha256.txt`. The surrogates use fixed seeds (1, 2; 7 for Glasser), and the cross-validation splits use seed 0.

## Provenance

Job sci-1107-dell-neural-structure-and-computation-7d442c08d5b7; campaign 11_07_2026; topic neural-structure-and-computation; machine dell; model Claude Opus 5.5 (claude-opus-5-5) through Claude Code. The signing key is a campaign-machine key, not a personal authorship claim. The ds004080 derivative file `ccepData_V2.mat` (sha256 ec2b425c...) is also in the shared campaign store at `datasets/openneuro-ds004080-v1.2.4-av-ccep-ccepdata-v2`.
