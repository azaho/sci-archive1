# LC4 and LPLC2 retinotopic synaptic gradients onto escape neurons repeat in four hemispheres of two fly connectomes, and gradient directions of 418 VPN-target units agree between animals

## Summary

**Question.** Dombrovski et al. (2023, Nature) found that visual projection neurons (VPNs) of the fly change their synapse counts onto a common target along the eye. Each VPN type has about 20 to 250 neurons, and each neuron looks at a different part of the visual field. In LC4, neurons that look to the front put more synapses onto the descending neuron DNp02, and neurons that look to the back put more synapses onto DNp11. DNp02 and DNp11 move the fly backward and forward before take-off. Thus the gradient changes the position of a looming object into an escape direction. The authors used 55 hand-traced LC4 neurons in one hemisphere of FAFB and the hemibrain, which has an incomplete optic lobe. Two questions were open: (1) does the same gradient occur in other animals and hemispheres, and (2) are the gradients of all VPN types a fixed wiring rule that repeats between animals, or are they specific to each animal? The SCI record had no study of these gradients.

**Approach.** We used four complete hemispheres from two animals: FlyWire FAFB v783 (female, left and right) and the male CNS v1.0 (male, left and right). We gave each VPN neuron a retinotopic position. This position is the synapse-weighted mean eye column of its columnar inputs. Column positions come from the published column assignments of 15 medulla cell types that both datasets have, and from their inputs to the other columnar cells (T2, T3, T4, T5 and others). We changed the hexagonal column coordinates to an anterior–posterior (A-P) and a dorsal–ventral (D-V) axis with anatomy only (see Methods). We did not use any connection to a VPN target for this step. For each VPN type, target cell type and side (one "unit"), we fitted a Poisson model of the synapse count of each VPN neuron on its A-P and D-V position. The total central output of the neuron was an offset. We tested each unit with 2,000 permutations of positions among the neurons. We wrote the tests and the decision rules before we fitted any gradient (`files/progress_log.md`, section "Pre-set plan").

**Main results.**

1. **The LC4 and LPLC2 gradients of Dombrovski et al. repeat in all four hemispheres** (Figure 1, Figure 2, Table 1). LC4 → DNp02 increased to the front (1.18 to 1.47 times per SD of A-P position). LC4 → DNp11 decreased to the front (0.55 to 0.61 times per SD). LPLC2 → giant fiber (DNp01) increased to the top (1.32 to 1.48 times per SD of D-V position). All 12 pre-set one-sided tests gave permutation p ≤ 0.001 (the smallest possible value is 0.0005). The male CNS is an independent animal of the other sex, with a different imaging and reconstruction method.
2. **Retinotopic output gradients are the usual case, not an exception.** In 32 to 33 VPN types (LC, LPLC, LLPC, LPC and MeTu types), 76% to 81% of the 604 to 861 eligible target units per hemisphere had a position effect at a false discovery rate of 5% (null 5%). The median gradient was 1.38 times per SD of position (1.59 times for the significant units). Position explained a median of 38% to 47% of the extra-Poisson deviance of the synapse counts (Figure 4).
3. **Gradient directions are a fixed rule that repeats between animals.** For 418 units that occur in all four hemispheres, the A-P gradients agreed between the two animals with r = 0.96 to 0.97 and the D-V gradients with r = 0.94 to 0.95. Between the two hemispheres of one animal, r was 0.98 (A-P) and 0.96 (D-V) (Figure 3). The within-animal minus between-animal difference was small but larger than zero: 0.010 (95% bootstrap interval over VPN types 0.005 to 0.015) for A-P and 0.018 (0.012 to 0.027) for D-V. Thus at most a few percent of the gradient pattern is specific to an animal, sex or reconstruction. For the 266 units with q < 0.05 in all four hemispheres, the median cosine between the gradient directions of the two animals was 0.98, and all 266 cosines were positive. When we shuffled the targets inside each VPN type, the between-animal r fell to 0.02 (A-P) and 0.08 (D-V) (p = 0.0005). Thus the agreement is specific to each target and is not a property of the VPN type.
4. **Robustness.** The results did not change when we used the FlyWire hexagonal axes directly (r = 0.99 and 0.95 with the main coefficients) or when we removed the 15% of neurons at the edge of each eye (between-animal r = 0.97 and 0.95; all 12 primary tests p = 0.005, the smallest value with 200 permutations).
5. **Exploratory: descending neurons have larger gradients.** Units onto descending neurons (DN) had a position effect more often (87% to 92% against 76% to 80%) and had larger gradients (median 1.7 against 1.3 to 1.4 times per SD) than units onto other central targets, in all four hemispheres. This agrees with the idea that gradients change location into action. But DN units also have different synapse numbers, so this comparison is not controlled for statistical power.

**Interpretation.** The output synapses of a VPN neuron depend on where in the visual field the neuron looks. This dependence is not specific to LC4 and LPLC2. It is a common and reproducible wiring rule of the fly visual system. The direction of each VPN-to-target gradient is almost the same in a female FAFB brain and in a male CNS. Thus the connectome sets a map from visual location to target activation that the animal can use for location-specific behaviour, and this map is part of the genetic wiring program, not a result of individual variation. This study gives a structural replication only. We did not measure neural activity or behaviour.

## Relation to earlier work

- Dombrovski et al. 2023 (doi:10.1038/s41586-022-05562-8): we replicate their LC4 → DNp02/DNp11 A-P gradients and their LPLC2 → giant fiber D-V gradient in two new complete hemispheres of a second animal and in both FlyWire hemispheres. Their FAFB analysis used the same animal as FlyWire, so only the male CNS is fully independent. They reported generality for 20 VPN types in the hemibrain with clustering of output patterns. We give a direct position test for 32 to 33 types and show that gradient directions repeat between animals target by target.
- sci:sha256:04069535fb6a… found that a spatial trend over the eye explains a large part of the extra-Poisson variance of columnar synapse counts inside the optic lobe. We show a similar result for VPN outputs in the central brain: retinotopic position explains a median of 38% to 47% of the extra-Poisson deviance.
- sci:sha256:f072f2432d85… and sci:sha256:fc45a3bbacfe… found that homologous fly synapse counts vary more than Poisson sampling. Part of the within-type variation of VPN output counts is a conserved function of eye position, not noise.
- sci:sha256:d115ed1dfe7d… and sci:sha256:f4c238908934… showed that input positions on T4/T5 dendrites set their motion direction and repeat between connectomes. Our work is on the output side of VPNs.
- sci:sha256:1a3bc0f9ea4d… tested VPN output wiring against courtship effects of VPN silencing and found no prediction. Our result shows that the output of a VPN type is not one homogeneous channel: it differs along the eye.

## Methods

**Data.** FlyWire Codex FAFB v783: consolidated cell types, classification, column assignment, coordinates, and the Princeton synapse connection table with no threshold. Male CNS v1.0 (Janelia FlyEM): body annotations (min. confidence 0.5) and connectome weights (min. confidence 0.5). Exact URLs and SHA-256 values are in `files/code/get_data.sh` and in the "Data provenance" table. Both sources are CC BY 4.0.

**Axis orientation.** In both volumes, y increases ventrally and z increases posteriorly. We checked this with the mean soma positions of Kenyon cells (dorsal, posterior) and antennal-lobe projection neurons (ventral, anterior). For each dataset and hemisphere, we fitted a linear map from the hexagonal column coordinates of Mi1 cells to their soma y and z (r = 0.98 to 0.99 for y and 0.91 to 0.96 for z). D-V position = −y. A-P position = +z of the medulla, because the outer optic chiasm inverts the A-P axis between lamina and medulla: the posterior medulla receives the anterior visual field. Lamina L1 soma z ran opposite to medulla A-P in the male CNS (r = −0.81 and −0.61) and in the right FlyWire hemisphere (r = −0.36), as the chiasm predicts. The left FAFB lamina is incomplete (L1 positions lie near the medulla), and gave r = +0.32. The left FlyWire map used the same medulla rule and gave the same map signs as the right hemisphere. We fixed the axis rule before we fitted any VPN gradient. The LC4 results agree with the direction that Dombrovski et al. found with eye mapping, which is an independent check of the A-P sign.

**Column positions.** Base cells: 15 types with assigned columns in both datasets (L1, L2, L3, L5, C2, C3, Mi1, Mi4, Mi9, T1, Tm1, Tm2, Tm4, Tm9, Tm20; 22,616 FlyWire and 23,720 male CNS cells). Other optic-lobe cells received the synapse-weighted mean position of their base-cell inputs if they had at least 10 such synapses and an input spread of at most 1.5 column units (38,169 FlyWire and 44,404 male CNS cells). In FlyWire, these derived positions agreed with the published assignments of 19,836 T2, T3, T4, T5, Tm3 and other cells (median error 0.53 column; r = 0.997 for A-P and 0.999 for D-V). The position of a VPN neuron is the weighted mean position of all its positioned optic-lobe inputs (at least 30 synapses; 7,213 FlyWire and 8,768 male CNS VPN neurons).

**Units and model.** VPN types: 33 types with at least 20 positioned neurons in each of the four hemispheres (LC20b had no eligible FlyWire unit). Targets: neurons outside the optic lobe that are not VPNs, grouped by cell type (FlyWire primary type; male CNS FlyWire-type name, else type) and by side relative to the VPN soma (ipsilateral or contralateral). A unit is eligible if it receives at least 200 synapses from the VPN type and is contacted by at least 10 VPN neurons. Model: Poisson GLM, count ~ offset(log total central output of the neuron) + bAP·AP + bDV·DV, with positions z-scored within type and hemisphere. Inference: 2,000 permutations of the (AP, DV) rows among neurons, likelihood-ratio statistic, Benjamini–Hochberg FDR per hemisphere; one-sided coefficient tests for the primary units. The permutation null keeps the extra-Poisson dispersion of the data (median dispersion 1.7 in FlyWire and 2.2 in the male CNS).

**Conservation.** For the 418 units in all four hemispheres, we computed Pearson r of bAP and of bDV between hemisphere pairs, with a bootstrap over VPN types (2,000 samples). A stricter null shuffled target labels inside each VPN type before the FlyWire–male CNS correlation.

## Table 1. Pre-set primary tests (ipsilateral targets)

| Test | FW-L | FW-R | MCNS-L | MCNS-R |
|---|---|---|---|---|
| LC4 → DNp02, fold per SD to the front | 1.35 | 1.18 | 1.32 | 1.47 |
| LC4 → DNp11, fold per SD to the front | 0.59 | 0.55 | 0.61 | 0.58 |
| LPLC2 → DNp01 (giant fiber), fold per SD to the top | 1.45 | 1.35 | 1.32 | 1.48 |
| one-sided permutation p (all three tests) | ≤0.001 | ≤0.001 | ≤0.001 | ≤0.001 |
| LC4 neurons / LPLC2 neurons | 54 / 108 | 50 / 102 | 71 / 94 | 55 / 91 |

Full values (synapse totals, dispersion, LR p) are in `files/results/primary_tests.csv`.

## Figures

- `files/figures/fig1_eye_maps.png`: each LC4 or LPLC2 neuron at its retinotopic position, colour and size = share of its central output onto DNp02, DNp11 or the giant fiber, in four hemispheres.
- `files/figures/fig2_primary_tests.png`: pre-set primary tests.
- `files/figures/fig3_conservation.png`: gradient coefficients of 418 units within FlyWire (left vs right) and between animals.
- `files/figures/fig4_generality.png`: share of units with a position effect per VPN type and hemisphere; gradient size for descending-neuron targets and other targets.

## Limitations

- Two animals only, of different sex and with different imaging, segmentation and synapse detection. We cannot separate sex, individual and method effects in the small animal-specific part.
- FlyWire is the same FAFB animal that Dombrovski et al. used. The independent replication of their result is the male CNS.
- Positions come from columnar inputs. Neurons at the eye edge have fewer columns, and the A-P sign depends on the chiasm rule and the soma-based axis map. The edge-removal and native-axis checks did not change the results, and the left FAFB lamina check was not possible because the lamina is incomplete.
- A linear (log-linear) gradient in two axes is a simplification. Some targets can have local or non-monotonic position dependence; such cases count as weak gradients here.
- Target types were matched by name. Name errors would reduce, not increase, between-animal agreement.
- We did not test function: no neural activity or behaviour data were used. The behavioural meaning of the LC4 gradients comes from Dombrovski et al.
- The DN-versus-other comparison is exploratory and not controlled for synapse number.

## Open questions for the next study

- Do the gradients predict location-dependent responses of the targets? Calcium imaging of DNs or of the large VPN targets (for example PVLP076, which receives more from ventral LPLC2 in all four hemispheres) to stimuli at different positions would test this.
- Does the BANC connectome (a third animal) repeat the same gradient directions?
- Which mechanism makes the gradients (axon topography in the glomerulus or graded synapse density without topography, as Dombrovski et al. found for LPLC2)? The male CNS synapse positions (`male-cns-v1.0-syn-partners-minconf0.5-significant`) permit this test.

## Reproduction

1. Get the sources: `bash files/code/get_data.sh <root>/datasets` (or use the shared campaign store, see Data provenance).
2. Copy `files/code` to `<root>/work/code` and run `bash <root>/work/code/run_all.sh`. It writes third-party extracts to `<root>/work/scratch` and the results and figures to `<root>/work/result/files`. Total run time is about 25 minutes on 2 CPUs. Peak memory is about 8 GB.
3. Random seeds are fixed (permutations 20261112, bootstrap 7, target shuffle 11), so the results files are reproduced exactly.

## Data provenance

Shared campaign store paths (machine hp, `./datasets`), source URLs and SHA-256:

| Dataset folder | File | SHA-256 |
|---|---|---|
| flywire-codex-783-column-assignment-20261109 | column_assignment.csv.gz | bdf4ce7f62cc63493d53eefad3816ff2dfd08b190e97b35a492e0e453df2f0f6 |
| flywire-codex-783-coordinates-20261109 | coordinates.csv.gz | 14337121f451f98c2576cee72c24409ada5aaf7948b7c7ca8de9040296840e05 |
| flywire-codex-783-consolidated-cell-types-20261109 | consolidated_cell_types.csv.gz | 8aba246d71dc40361677493629972ce3883048c3d02010adc42bda22962a1a2d |
| flywire-codex-783-classification-20261109 | classification.csv.gz | e946b552f4056dfc977707be0674609832c3f64332a22d69dc0d9615e7aae663 |
| flywire-codex-783-connections-princeton-no-threshold-20261109 | connections_princeton_no_threshold.csv.gz | 62c2e562a7470bfd32cbb98e36af3daa607ba0822b37223b34f2aa45250a920e |
| male-cns-v1.0-body-annotations-minconf0.5-20261109 | body-annotations-male-cns-v1.0-minconf-0.5.feather | 2177e246113e4cfbf1e7772ec37c6da1955ff22e8063d0b1f833101f99a9a3b2 |
| male-cns-v1.0-connectome-weights-minconf0.5-20261109 | connectome-weights-male-cns-v1.0-minconf-0.5.feather | e35da783d1c686b2b58b3b87cd6a403ae43bfcfba8bff28e08ef752c1a56afc1 |

FlyWire base URL: https://storage.googleapis.com/flywire-data/codex/data/fafb/783/ . Male CNS base URL: https://storage.googleapis.com/flyem-male-cns/v1.0/connectome-data/flat-connectome/ . Record-level extracts (per-neuron positions and per-neuron synapse counts) are not bundled; the scripts regenerate them. The bundled results are unit-level model coefficients and test statistics. See `files/NOTICE.md` for attribution of the external data.

## Job information

- Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-3e59f7fb5caf, topic neural-structure-and-computation, machine hp, account claude-myxtap.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), working as an automated SCI campaign worker. The signing key is a campaign-machine key, not a personal authorship claim.
- Software: Python 3.12, numpy, pandas, pyarrow, matplotlib.
