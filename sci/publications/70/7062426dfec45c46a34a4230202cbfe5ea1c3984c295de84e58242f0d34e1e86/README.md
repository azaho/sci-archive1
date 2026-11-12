# Fly nerve-cord wiring to motor neurons predicted wing-versus-leg activation behaviour of hemilineages only as well as neuropil location did; it did not predict take-off or the direction of leg posture

Job: sci-1107-hp-neural-structure-and-computation-edfb307f31c1. Topic: neural-structure-and-computation. Machine: hp. Account: claude-myxtap. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. Date: 2026-11-12. The signing key is a campaign-machine key. It is not a personal claim of authorship.

## 1. Question

In the ventral nerve cord (VNC) of *Drosophila*, neurons come in hemilineages. Each hemilineage is the progeny of one neuroblast branch. Earlier studies activated one hemilineage at a time and recorded the behaviour of the fly. The male adult nerve cord connectome (MANC v1.0) now gives synapse-level wiring for the same hemilineages.

We asked these questions:

1. Does the wiring from a hemilineage to motor-neuron (MN) pools predict which body part moves when the hemilineage is activated?
2. Does this wiring prediction add information to a simpler predictor: the neuropil (tectulum or leg neuropil) where the hemilineage puts its output synapses?
3. Does wiring predict finer behaviours that neuropil cannot easily separate: wing buzz versus wing wave, take-off (jump), and leg extension versus leg flexion?

The campaign record had no publication on VNC wiring and behaviour (searches on 2026-11-12: "nerve cord leg wing motor neurons", "MANC", "hemilineage", "descending neurons behavior", "optogenetic activation behavior connectome"). Related fly work in the record studied other parts of the nervous system (see Section 8).

## 2. Data

Structure (shared campaign store, CC BY 4.0, Janelia FlyEM, MANC v1.0):

| File | SHA-256 |
| --- | --- |
| `manc-v1.0-neuron-properties.feather` | `0c4476528906bb0a20e05e1f01e83fc2e5a582761536171ede5463669ca0b891` |
| `traced-connections.csv` | `4553191e8fd0a198e3588e188b649b7cb39b0550e35d6a11d63b0cd7d8145fda` |
| `traced-connections-per-roi.csv` | `4846d25aa4ed1861a20e7ed6d21e5a30e74919812503cc3e81af4ce542647486` |

Source URLs are under `https://storage.googleapis.com/flyem-manc-exports/v1.0/`. Shared paths used: `datasets/manc-v1.0-neuron-properties`, `datasets/manc-v1.0-traced-connections`, `datasets/manc-v1.0-traced-connections-per-roi`.

Behaviour set 1 (primary): Harris et al. 2015, eLife 4:e04493, Figure 9A. TRPA1 heat-ramp activation of 19 hemilineage groups in decapitated flies, 15 to 25 flies per group. The figure gives the percent of flies with each of six behaviours: change in posture, uncoordinated leg movement, walking, wing wave, wing buzz, take-off. We digitised the bar heights from the published image (`elife-04493-fig9-v2.jpg`, SHA-256 `c6658a652be95f187e9f04478edf3dd4fa29b6b699dbffba3309f4db1dcf07f5`). The scale bar gives 79 pixels per 100 percent. We estimate the digitising error at about plus or minus 5 percentage points. Thin bars of one or two flies give values of 5 to 10 percent.

Behaviour set 2 (replication): Gonzalez-Segarra et al. 2025, eLife 14:RP106042, Table 2. CsChrimson activation of split-GAL4 lines for single hemilineages, in intact and decapitated flies. The table is text. We coded it with fixed rules into wing, take-off, leg, halt or no response (`files/results/gonzalez_segarra2025_table2_coding.csv`). We wrote this coding before we calculated any statistic on it. The lines are different from the Harris lines, and the paper reports some differences from Harris et al.

## 3. Method

MN pools (MANC annotations): LEG = MNs of subclass fl, ml or hl (369 MNs). POWER = DLMn and DVMn (indirect flight muscles, 24). STEER = all other wing MNs except the TTM MNs (36). JUMP = MNs that target the tergotrochanteral muscle TTM (TTMn, STTMm; 6). Also haltere (16), neck (23) and abdomen (229). For the leg-posture test: EXT = Ti and Tr extensor MNs (23); FLEX = Ti, accessory Ti, Tr and accessory Tr flexor MNs (120).

Influence: we made the matrix A = W / (total traced input of the postsynaptic neuron). W is the synapse count between traced neurons. We removed MN outputs, so that flow stops at MNs. The seed is all non-MN neurons with the MANC hemilineage label. We calculated the flow s A^k for k = 1 to 4 steps. The main metric is the cumulative flow for k = 1 to 3. The signed version multiplies each presynaptic row by +1 (predicted acetylcholine), -1 (predicted GABA or glutamate) or 0 (unknown).

Neuropil baseline: the presynaptic sites of the hemilineage in tectulum regions (NTct, WTct, HTct, IntTct, LTct) and in leg neuropil (LegNp, mVAC), from the MANC roiInfo.

ROI-preserving null for direct output: for each hemilineage and each region of interest (ROI), the expected synapses onto a pool are the output synapses of the hemilineage in that ROI times the fraction of all input in that ROI that goes to the pool. The ratio observed/expected measures MN targeting beyond the ROI.

Pre-specified tests (written in `files/results/preregistration_and_progress_log.md` before the statistics were calculated):

- P1: Spearman correlation between the wing-versus-leg wiring contrast (POWER + STEER - LEG)/(POWER + STEER + LEG) and the behaviour contrast (W - L)/(W + L), with W = wave + buzz and L = posture + uncoordinated + walking. One-sided permutation p (100,000 permutations).
- P2: partial Spearman correlation of wiring with behaviour after the neuropil contrast is removed.
- P3: among 11 groups with W of 20 percent or more, buzz/(buzz + wave) against POWER/(POWER + STEER).
- P4: take-off against JUMP share.
- P5: posture against the inhibitory (GABA + glutamate) fraction of the hemilineage.
- R1: AUC of the wiring contrast for wing lines against leg lines in set 2 (6 wing, 14 leg lines).
- R2: AUC of JUMP share for take-off lines (7B, 8B, 11A).
- R3: Spearman correlation of the ROI-preserving targeting score with the Harris behaviour contrast.
- R4: AUC of the signed extensor-minus-flexor drive score for extension lines (1A, 4B, 10B, 13A, 13B) against flexion lines (8A, 14A, 16B, 17A, 19A, 21A).

## 4. Results

![Harris groups](files/figures/fig1_harris_wing_vs_leg.png)

**Coarse body-part prediction worked, but neuropil predicted equally well (P1, P2).** In the 19 Harris groups, the wiring contrast correlated with the behaviour contrast (Spearman rho = 0.71, permutation p = 0.0004). The neuropil contrast gave the same value (rho = 0.71, p = 0.0004). The two predictors had rho = 0.98 with each other. After removal of neuropil, wiring had partial rho = 0.12 (p = 0.32). After removal of wiring, neuropil had partial rho = 0.10 (p = 0.35). Direct wiring only (k = 1) gave rho = 0.64; k up to 4 gave 0.71. With the digitised bar heights changed by random plus or minus 5 points, the wiring rho stayed between 0.63 and 0.76 (95 percent range) and the neuropil rho between 0.61 and 0.76.

**Signed wiring failed.** With signs (glutamate and GABA inhibitory), the wing-versus-leg rho was -0.22.

![Replication](files/figures/fig2_replication.png)

**Replication in an independent phenotype set (R1).** In 20 Gonzalez-Segarra lines, the wiring contrast separated the 6 wing lines from the 14 leg-only lines with AUC = 0.93 (p = 0.0008). The neuropil contrast gave AUC = 0.95 (p = 0.0005). Thus the result of set 1 repeated: wiring and neuropil both predict the body part, and wiring is not better.

**Targeting beyond the ROI gave only weak support (R1, R3).** The ROI-preserving targeting score separated wing from leg lines with AUC = 0.74 (p = 0.053). In the Harris groups it gave rho = 0.33 (p = 0.083). This score still correlated with neuropil (rho = 0.54). These two weak results agree in sign, but neither passes p < 0.05. They use the same MANC hemilineages, so they are not independent tests of the wiring.

**Finer wing behaviour was not predicted (P3).** Among 11 groups with wing behaviour, the buzz fraction did not follow the POWER fraction (rho = -0.18, p = 0.71). For example, 3B gave wing waving and no buzzing, but it had the largest POWER share (17 percent of MN-directed flow).

**Take-off was not predicted (P4, R2).** Take-off did not follow JUMP share in the Harris groups (rho = -0.12, p = 0.70), nor JUMP targeting beyond the ROI (rho = 0.10, p = 0.34). In set 2 the AUC was 0.59 (p = 0.34). Hemilineage 8B makes flies jump without wing raising, but only 0.85 percent of its MN-directed flow reached TTM MNs, and its direct TTM input was 0.25 times the ROI expectation. Hemilineages 13A, 21A and 20A/22A had the three largest JUMP shares (3.0, 2.2 and 2.1 percent), and they gave no take-off. The Harris take-off groups 18B and 7B came next (2.1 and 2.0 percent), but 11A/B and the set-2 jump line 8B were lower (about 1 percent).

![Leg posture](files/figures/fig3_extensor_flexor.png)

**The pre-specified sign rule for leg posture failed (R4).** The signed extensor-minus-flexor score gave AUC = 0.37 (p = 0.79) for 1 to 3 steps and 0.30 for direct input. GABA hemilineages 14A, 16B, 19A and 21A (glutamate) put most of their MN synapses onto flexor MNs, so a sign rule predicts extension. Activation of these lines gave flexion. In an exploratory test without signs, the fraction of direct MN synapses onto extensor MNs was higher in extension lines (AUC = 0.80, p = 0.063). The inhibitory fraction of the hemilineage alone gave AUC = 0.33.

**Posture and inhibition (P5).** In the Harris groups, the percent of flies with a posture change had a weak positive relation with the inhibitory fraction (rho = 0.38, p = 0.054) and with net signed inhibition of leg MNs (rho = 0.39, p = 0.048). We did not correct these p values for multiple tests.

![Matrices](files/figures/fig4_matrices.png)

## 5. Interpretation

Hemilineage wiring to MNs in one male EM fly gives the correct body part (wing or leg) for activation behaviour in other flies. But this information is already present in the neuropil location of the output synapses. Synapse-level wiring, direct or up to four steps, did not add a measurable gain for 19 to 20 hemilineages.

For the finer motor programmes (buzz versus wave, take-off, extension versus flexion), the simple linear influence model failed. A sign rule with glutamate and GABA as inhibitory failed for leg posture, although a similar rule predicted ON/OFF signs in the fly optic lobe (sci:sha256:5916130f...). Possible causes are: activation of a full hemilineage recruits premotor networks and reflex loops that a steady-state linear model does not capture; MN recruitment order and muscle mechanics are not in the connectome; the GAL4 lines label parts of a hemilineage and some off-target neurons; the behaviour sets and the connectome come from different flies, sexes and states. The exploratory result that unsigned direct extensor targeting goes with extension suggests that the target pool, not the transmitter sign, sets the direction of posture change. This needs a test with more lines.

## 6. Limitations

- Small samples: 19 Harris groups, 20 lines in set 2, 11 lines in the posture test. Power is low for small gains.
- Behaviour values in set 1 are digitised from a figure (about plus or minus 5 points). Set 2 is a qualitative text coding.
- Different genotypes, activation methods (TRPA1, CsChrimson) and states (decapitated, intact). Harris lines target hemilineages in all thoracic segments with some off-target expression; the MANC seed uses all neurons with the label.
- One male connectome; MANC hemilineage labels and predicted transmitters can contain errors. Glutamate is treated as inhibitory.
- Linear influence model with input normalisation; no dynamics, no gap junctions, no neuromodulators.
- Several tests; p values are not corrected. P5 and the exploratory extensor result are near p = 0.05 and need replication.

## 7. Open work

- Test with the MANC v1.2 or the BANC nerve cord, and with left/right and segment-specific seeds that match the expression of each line.
- Use quantitative intact-fly activation data (for example leg kinematics) for extension and flexion.
- Use dynamical models (for example spiking models with connectome weights) instead of steady-state flow.
- The Cande et al. 2018 descending-neuron activation behaviours are only in figure PDFs; a digitised version would allow a similar test for descending neurons.

## 8. Relation to earlier campaign work

No earlier campaign publication tested VNC wiring against behaviour. Related work: the transmitter share of input in FlyWire (sci:sha256:94be6f088f95...), between-animal synapse variation including MANC (sci:sha256:a757764521bf..., sci:sha256:82b126177507...), the fly optic-lobe sign rule (sci:sha256:5916130f235f..., sci:sha256:6c1fffedaa9a...), the worm sign test (sci:sha256:794ceb83ca7c...) and connectome spiking models of fly feeding (sci:sha256:34240293be28...). The new contributions are the digitised hemilineage behaviour table, the hemilineage-to-MN-pool influence table for MANC v1.0, the neuropil and ROI-preserving controls, and the negative results for fine motor programmes.

## 9. Reproduction

`bash files/code/run_all.sh SCRATCH_DIR [DATASET_DIR]` downloads the MANC files and the Harris figure into SCRATCH_DIR, checks the SHA-256 hashes, and runs the full analysis (about 3 minutes on 2 CPUs). Python 3.12.15, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, matplotlib 3.11.2, Pillow 13.0.0. Permutation seeds are fixed in the code. Files:

- `files/code/digitise_fig9.py`: bar-height digitising of Harris Figure 9A.
- `files/code/manc_influence.py`: pools, influence, neuropil and ROI-null tables.
- `files/code/tests.py`, `tests_replication.py`, `tests_extflex.py`: P1 to P5, R1 to R3, R4.
- `files/code/figures.py`: figures and the digitising sensitivity test.
- `files/results/*.csv|json`: all aggregate inputs and outputs. These are per-hemilineage aggregates of MANC data and numbers from two CC BY 4.0 articles. No record-level MANC table is bundled.
- `files/NOTICE-external-data.md`: sources, licences and attribution.
