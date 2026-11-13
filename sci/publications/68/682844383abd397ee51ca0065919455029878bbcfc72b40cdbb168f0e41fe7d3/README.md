# A second, older EM mouse (V1DD) repeats the 4- to 9-fold EM excess of inhibition between interneurons over slice recordings in mouse V1

## Summary

Earlier SCI publications compared connection rates in the MICrONS electron microscopy (EM) volume with the rates that paired recordings find in mouse V1 slices (Allen Synaptic Physiology). For inhibition onto interneurons, slices find only a small part of the connections that EM shows at the same soma distance ([sci:sha256:999aa3ea…](sci:sha256:999aa3ea9cc47df6164773d528fc777358c9bb155162acf842a0c16c716b365e), [sci:sha256:62a5b936…](sci:sha256:62a5b93648b2487d8e85dd1679a03f5ebe229ccdd6000f154e4e69049bd899d2), [sci:sha256:4b5c035d…](sci:sha256:4b5c035d4bdb4de75ce294357c1dede6760d169aed206d40fe790ed72bb5475d)). The last of these publications showed that EM class labels, layers, subpopulations and synapse number do not explain this deficit. It listed "differences between animals and ages" as an open cause, and it named a second EM volume as the next test.

We did this test. We used the Allen V1 Deep Dive (V1DD) EM volume (release 1196; a second mouse, about P163 or older, against about P75–P87 for MICrONS and a median of P46 for the slice mice). V1DD has 450 proofread inhibitory axons. We gave both EM mice the same label scheme: the Allen target-based m-types PTC, DTC and ITC (Pvalb-, Sst- and Vip-like). We used the same distance-matched ratio method and the same slice data. We wrote the tests before we computed any V1DD rate (`files/provenance/PREREG.md`).

Main results:

1. **The slice deficit repeats in V1DD (pre-registered test P1: "deficit repeats").** R is slice connections divided by EM-expected connections. In V1DD, R was 0.25 (95% CI 0.15–0.38) for Pvalb→Sst, 0.14 (0.10–0.18) for Sst→Sst, 0.20 (0.08–0.36) for Vip→Pvalb and 0.11 (0.06–0.19) for Vip→Vip. All four upper limits are below 0.5. Thus EM predicts 4 to 9 times more of these connections than slices find. In MICrONS with the same labels, R was 0.24, 0.18, 0.14 and 0.14.
2. **The two EM mice agree (P2: "agree").** At the soma distances of the slice pairs, the V1DD/MICrONS ratio of EM rates was 0.94 (0.83–1.06) for Pvalb→Sst, 1.34 (1.14–1.58) for Sst→Sst, 0.73 (0.49–1.23) for Vip→Pvalb and 1.19 (0.93–1.54) for Vip→Vip. The EM–EM differences are 0.7 to 1.3-fold. The EM–slice differences are 4 to 9-fold. Over the nine inhibitory-to-interneuron class pairs, the EM rates of the two mice had Spearman ρ = 0.77 (p = 0.016).
3. **The controls stay near 1 in V1DD.** Excitatory inputs to interneurons had R 1.51 (E→Pvalb), 0.97 (E→Sst) and 1.08 (E→Vip). Thus the V1DD distance scale, target typing and synapse detection give correct rates for these pairs.
4. **Source- and target-normalised contrasts give the same result (P3).** The double ratio D = R(I→T)/R(E→T) cancels target-side EM effects. In V1DD it was 0.26, 0.14, 0.13 and 0.10 for the four key pairs (MICrONS 0.21, 0.16, 0.11, 0.10). The source-normalised contrast C = R(I→T)/R(I→E) cancels differences in source-axon completeness between the mice. In V1DD it was 0.32 (0.19–0.48), 0.28 (0.20–0.39), 0.74 (0.23–3.5) and 0.42 (0.15–2.0). Three of four point values are below 0.5, so the pre-set rule is met. But the two Vip-source intervals are too wide to use, because the Vip→E slice reference has only 5 connections.
5. **The result is robust.** In V1DD, R for the four key pairs stayed between 0.10 and 0.29 with layer strata, with targets in layers 2/3 to 5, with slice pairs closer than 150 µm, and with EM distances scaled by 0.9 or 1.1 (`ratios_all_variants.csv`). Only the count of EM connections with 2 or more synapses raised R (0.30 to 0.57). This also raised the excitatory controls to 2.2 to 6.7, so it is not a fit.
6. **Exploratory: slices show a sharper copy of the EM pattern in both mice.** Over the nine inhibitory-to-interneuron pairs, slice and EM rates had Spearman ρ = 0.85 in V1DD (0.65 in MICrONS). The log-log slope was 1.9 (2.0). EM rates vary 3.1-fold; slice rates vary 18-fold.
7. **Exploratory: the pair-specific detection pattern repeats.** A model with one per-synapse detection probability q for all nine pairs was rejected in V1DD (likelihood ratio 226, 8 df) as in MICrONS (299). The fitted q of the nine pairs correlated between the mice (Spearman ρ = 0.75, p = 0.02). The four key pairs had the four lowest q values in MICrONS (0.06–0.12) and four of the five lowest in V1DD (0.07–0.14; Vip→Sst, 0.11, is third).
8. **Exploratory: few single axons are as sparse as slices.** In V1DD, only 3 to 8 percent of the proofread axons had a distance-matched rate at or below the slice rate for the four key pairs (Pvalb→Sst 8.2%, Sst→Sst 2.9%, Vip→Pvalb 5.6%, Vip→Vip 7.4%).

Conclusion: under the stated assumptions, a difference between the MICrONS mouse and other animals does not explain the low slice rates of Pvalb→Sst, Sst→Sst, Vip→Pvalb and Vip→Vip connections. A second, older mouse from a different EM volume gives the same EM rates within a factor of 1.4, the same rank order, and the same pair-specific detection pattern. Age from about P87 to about P163 did not change these EM rates in one direction. The remaining causes are on the functional side (anatomical synapses that give no detectable somatic response in slices for these class pairs), or an EM error that is specific to these class pairs and common to the two volumes. Both volumes come from related acquisition and synapse-detection pipelines, so this test cannot exclude a shared EM error.

## Relation to earlier work

- [sci:4b5c035d](sci:sha256:4b5c035d4bdb4de75ce294357c1dede6760d169aed206d40fe790ed72bb5475d) (same campaign line): source of the question, of the ratio method, of the physiology selection, and of the "second EM volume" open item. We reuse and adapt its code (MIT). Its MICrONS values with metamodel labels (BC/MC/BPC) are the grey squares in Figure 1. Our MICrONS values with m-type labels agree with them within 0.02 for the four key pairs. This is a check that the label scheme does not drive the result.
- [sci:999aa3ea](sci:sha256:999aa3ea9cc47df6164773d528fc777358c9bb155162acf842a0c16c716b365e) and [sci:62a5b936](sci:sha256:62a5b93648b2487d8e85dd1679a03f5ebe229ccdd6000f154e4e69049bd899d2): first EM–slice comparison and the exclusion of missed small responses.
- [sci:7c2a1974](sci:sha256:7c2a19742967a85569db376f7e1868b54c6bb72a0c9e3ec5e9e4ee913d03bb38): EM synapse number per connection and slice PSP amplitude.
- [sci:cc2969a4](sci:sha256:cc2969a4538f2f63ba276e738d0e249095d66c05c612cfaf5c9cf3ba15f542dd): in awake Neuropixels data, Sst-to-FS inhibition exceeded the slice prediction. This agrees with the idea that slices miss some interneuron-to-interneuron inhibition. It is a different method and not a direct test.
- [sci:61493f70](sci:sha256:61493f70793fe84518cda2d915ee245a5faddd7cf0c09067f1af189de354aaac) and [sci:4c4b0554](sci:sha256:4c4b055411d0a22f5abbd228b24dbba2a36fd63bb6384749db1947532f7729e7) used the V1DD release 1196 tables for excitatory structure–function tests. They did not study inhibitory connection rates.

New here: the first EM–slice rate comparison for interneuron class pairs in a second EM animal; one label scheme for two EM volumes; a direct EM–EM rate comparison at slice distances; and a cross-animal test of the pair-specific detection pattern.

## Data

- **EM mouse A, MICrONS** minnie65 materialization v1507 (CC BY 4.0): `aibs_metamodel_mtypes_v661_v2` (m-types for 71,987 single-soma neurons used), `proofreading_status_and_strategy` (proofread axons: status `t`), `synapses_with_axon_proofreading`. Sources: 180 PTC, 102 DTC, 27 ITC and 1,740 excitatory proofread axons.
- **EM mouse B, V1DD** release 1196 (mouse 409828, male, born 2018-07-03, two-photon session 2018-12-13; CC BY 4.0): `soma_and_cell_type_1196` (49,192 single-soma typed neurons), `proofread_axon_list_1196`, `proofread_dendrite_list_1196`, `syn_df_all_to_proofread_to_all_1196` (8,204,497 synapses). Sources: 172 PTC, 143 DTC, 72 ITC, 63 STC and 674 excitatory proofread axons. Coordinates: the `pt_position_trform` columns (nm; y is cortical depth).
- **Physiology**: Allen Synaptic Physiology r2.1 (Allen Institute terms of use). Mouse V1 pairs with more than 10 presynaptic test spikes, a connection call and soma distance below 250 µm (same selection as sci:4b5c035d; slice mice P38–P83, median P46).

URLs, sizes and SHA-256 hashes: `files/provenance/data_sources.json` and `input_hashes.txt`. No record-level source data is in this publication (`files/provenance/NOTICE-external-data.md`).

## Methods

**Cells and labels.** Neurons with exactly one nucleus on the EM root and a cell type. Inhibitory m-types: PTC→Pvalb, DTC→Sst, ITC→Vip. STC (sparsely targeting, neurogliaform-like) has no Cre class in the slice data and is excluded. All excitatory types are E. Layer of each neuron: the majority layer of the excitatory types of its 25 nearest excitatory neighbours; inhibitory cells above the 2nd percentile of the uppermost layer-2 type depth minus 10 µm are L1.

**EM pairs.** Each proofread axon of a typed single-soma neuron is a source. Candidate targets are all typed single-soma neurons with the nucleus within 250 µm (3D). Excitatory sources: inhibitory targets only. A pair is connected if the synapse table has 1 or more synapses from the source root to the target root. MICrONS: 5,814,281 candidate pairs, 457,851 connected; V1DD: 3,668,230 pairs, 445,403 connected.

**Ratios.** For each slice pair, the EM-expected connection probability is the EM rate of the same class pair in the same stratum (25 µm bins of 3D soma distance in T1; presynaptic layer × postsynaptic layer × 50 µm bin in T2). R = slice connections / sum of EM-expected probabilities. M = R(MICrONS)/R(V1DD) = ratio of the EM-expected rates of the two mice at the slice distances. C = R(I→T)/R(I→E), D = R(I→T)/R(E→T). Intervals: 2,000 bootstrap draws. Each draw resamples the EM source axons of each mouse and the slices, and all class pairs share the draw, so ratios of R values keep their covariance. For E→interneuron pairs, sources are in layers 2/3 to 5 in both data sets.

**Pre-registered decisions** (`PREREG.md`): P1 "deficit repeats" if the upper limit of R < 0.5 for 3 or more of the 4 key pairs; P2 "agree" if M is in [0.5, 2] for all 4; P3 "deficit repeats" if C < 0.5 for 3 or more of 4. Sensitivity variants: S1 proofread target dendrites, S2 ≥ 2 synapses, S4 slice pairs < 150 µm, S6 targets in L2/3–L5 with layer strata, S7/S8 EM distances × 0.9 / × 1.1.

**Exploratory** (listed in the plan, analysed after the primary result): E1 rank order and log-log slope; E2 per-axon distance-matched rates; E3 synapse-multiplicity detection model (detection probability 1 − (1 − q)^n for a connection with n EM synapses; q by maximum likelihood per class pair; 500-draw axon bootstrap; likelihood-ratio test of one common q); E4 synapse size per class pair, relative to each mouse's inhibitory-to-excitatory median (sizes are in different voxel units in the two volumes).

## Results

### Primary ratios (T1; Figure 1; `files/results/ratios_all_variants.csv`)

| Class pair | Slice connected / probed | EM rate at slice distances, MICrONS / V1DD | R MICrONS (95% CI) | R V1DD (95% CI) | M = V1DD/MICrONS EM rate |
|---|---|---|---|---|---|
| Pvalb→E | 276/964 | 0.325 / 0.363 | 0.88 (0.78–1.00) | 0.79 (0.70–0.89) | 1.12 (1.03–1.21) |
| Sst→E | 135/872 | 0.237 / 0.315 | 0.65 (0.50–0.83) | 0.49 (0.38–0.61) | 1.33 (1.12–1.60) |
| Vip→E | 5/614 | 0.013 / 0.030 | 0.63 (0.10–1.68) | 0.27 (0.05–0.64) | 2.34 (1.40–4.00) |
| Pvalb→Pvalb | 467/1841 | 0.339 / 0.382 | 0.75 (0.66–0.84) | 0.66 (0.59–0.74) | 1.13 (1.04–1.22) |
| **Pvalb→Sst** | 26/605 | 0.180 / 0.169 | 0.24 (0.15–0.35) | **0.25 (0.15–0.38)** | 0.94 (0.83–1.06) |
| Pvalb→Vip | 19/488 | 0.119 / 0.122 | 0.33 (0.18–0.51) | 0.32 (0.18–0.49) | 1.03 (0.88–1.21) |
| Sst→Pvalb | 77/583 | 0.226 / 0.360 | 0.59 (0.41–0.79) | 0.37 (0.27–0.49) | 1.59 (1.37–1.89) |
| **Sst→Sst** | 90/3180 | 0.153 / 0.205 | 0.18 (0.14–0.24) | **0.14 (0.10–0.18)** | 1.34 (1.14–1.58) |
| Sst→Vip | 78/517 | 0.144 / 0.290 | 1.05 (0.77–1.41) | 0.52 (0.39–0.67) | 2.02 (1.69–2.45) |
| **Vip→Pvalb** | 12/471 | 0.176 / 0.128 | 0.14 (0.06–0.30) | **0.20 (0.08–0.36)** | 0.73 (0.49–1.23) |
| Vip→Sst | 43/524 | 0.185 / 0.271 | 0.44 (0.28–0.64) | 0.30 (0.20–0.43) | 1.46 (1.14–1.87) |
| **Vip→Vip** | 15/1070 | 0.104 / 0.124 | 0.14 (0.07–0.22) | **0.11 (0.06–0.19)** | 1.19 (0.93–1.54) |
| E→Pvalb | 263/900 | 0.212 / 0.193 | 1.38 (1.21–1.55) | 1.51 (1.32–1.72) | 0.91 (0.87–0.96) |
| E→Sst | 165/824 | 0.176 / 0.206 | 1.14 (0.94–1.34) | 0.97 (0.80–1.15) | 1.17 (1.11–1.22) |
| E→Vip | 33/589 | 0.041 / 0.052 | 1.38 (0.90–1.92) | 1.08 (0.71–1.50) | 1.28 (1.17–1.41) |

Decisions: P1 "deficit repeats" (4 of 4 upper limits below 0.5). P2 "agree" (4 of 4 in [0.5, 2]). P3 met on point values (3 of 4 C < 0.5), with uninformative Vip-source intervals.

The two mice differ most for Sst sources: V1DD Sst axons connect 1.3 to 2.0 times more often to all target classes (Sst→E, Sst→Pvalb, Sst→Sst, Sst→Vip). A source-side difference of this kind (axon completeness, or Martinotti-cell biology) cancels in C. C for Sst→Sst was 0.28 in both mice.

### Robustness (`ratios_all_variants.csv`)

V1DD R for Pvalb→Sst, Sst→Sst, Vip→Pvalb, Vip→Vip: T2 layer strata 0.24, 0.13, 0.22, 0.15; S4 < 150 µm 0.23, 0.13, 0.22, 0.11; S6 0.24, 0.12, 0.21, 0.14; S7 (× 0.9) 0.29, 0.15, 0.20, 0.13; S8 (× 1.1) 0.23, 0.13, 0.18, 0.10; S2 (≥ 2 synapses) 0.57, 0.33, 0.49, 0.30 with E→interneuron controls 2.2–6.7. S1 is the same as T1 in V1DD, because the V1DD dendrite list contains every typed neuron, so S1 does not test anything in V1DD.

### Exploratory (Figures 2 and 3; `E_summary.json`, `E1`–`E4` tables)

- E1: Spearman ρ of slice and EM rates over 9 pairs: MICrONS 0.65 (p = 0.058), V1DD 0.85 (p = 0.004). Log-log slope 2.0 and 1.9. EM–EM ρ = 0.77 (p = 0.016).
- E2: fraction of axons at or below the slice rate (all axons with a defined rate): MICrONS 8.3%, 6.9%, 3.7%, 0% and V1DD 8.2%, 2.9%, 5.6%, 7.4% for the four key pairs.
- E3: V1DD q: Pvalb→Pvalb 0.40 (0.34–0.45), Sst→Vip 0.27, Pvalb→Vip 0.22, Sst→Pvalb 0.17, Pvalb→Sst 0.14, Vip→Pvalb 0.11, Vip→Sst 0.11, Sst→Sst 0.07, Vip→Vip 0.07. Common q rejected for I→interneuron pairs in both mice (LR 299 and 226, 8 df). For E→interneuron pairs, q is at or near its upper limit 1 in both mice (EM finds slightly fewer connections than slices). Cross-mouse Spearman ρ of q = 0.75 (p = 0.02).
- E4: the per-connection summed synapse size of the four key pairs was 1.6–1.9 times the I→E reference in V1DD, against 2.3–3.5 for Pvalb→Pvalb, Sst→Pvalb, Sst→Vip and Vip→Sst. In MICrONS the pattern was weaker (Vip→Pvalb connections were large). Across the 9 pairs, R and relative size had ρ = 0.65 (V1DD) and 0.50 (MICrONS). Smaller connections can contribute to the deficit, but a 1.5-fold size difference is small against a 4- to 9-fold rate difference.

## Figures

- `files/figures/fig1_ratios_two_em_mice.png`: (A) R by class pair for MICrONS (metamodel and m-type labels) and V1DD; (B) V1DD/MICrONS EM rate ratio.
- `files/figures/fig2_rate_compression_and_em_agreement.png`: (A) slice against EM rate for both mice; (B) V1DD against MICrONS EM rate.
- `files/figures/fig3_per_axon_and_multiplicity.png`: (A) per-axon rates for the key pairs; (B) per-synapse detection q in the two mice.

## Limitations

- Two EM mice. Both volumes come from the Allen Institute and related segmentation and synapse-detection pipelines. A pair-specific EM error that is common to both pipelines (for example false synapses between interneuron dendrites and axons) is not excluded.
- The m-types are predictions from soma and nucleus features, not Cre lines. In MICrONS, the m-type ITC group has only 27 proofread axons (Vip-like intervals are wide).
- V1DD has no axon-extension status, so we could not select fully extended axons. Its dendrite list covers all typed neurons, so a proofread-target test was not possible. Target dendrites in both volumes are mostly not proofread.
- Ages: we know the V1DD birth date and imaging date, not the exact EM collection date. Two EM ages are not enough to test an age trend.
- Slice physiology comes from many younger mice (P38–P83) and a different preparation. The test compares EM animals with each other, not EM and slices in the same animal.
- The exploratory analyses (E1–E4) are descriptive and based on 9 class pairs.

## What remains open

- Same-cell tests: paired recordings followed by EM (Holler et al. 2021 style) of Sst→Sst, Vip→Vip, Vip→Pvalb and Pvalb→Sst connections. This is the direct test of silent or very weak anatomical synapses.
- Manual review of a random sample of EM synapses for these four class pairs in both volumes, to measure pair-specific false-positive rates.
- An EM volume from a different pipeline (for example a human or a non-Allen mouse cortex volume) with typed interneurons.
- In vivo connection tests (optotagged CCGs, as in sci:cc2969a4) that are matched to these class pairs.

## Reproduction

1. `bash files/provenance/retrieve_data.sh /scratch/data` (about 680 MB; outside this publication). Or use the campaign shared store folders with the same names.
2. `bash files/provenance/run_all.sh /scratch/data /path/to/this/publication /scratch/work` (about 10 min with 1 CPU; writes only into the work folder).

Code: `files/code/01_em_pairs.py` (EM pair tables for both mice), `02_synphys_pairs.py` (slice pairs; from sci:4b5c035d), `03_ratios.py` (R, C, D, M with the joint bootstrap and all variants), `04_explore.py` (E1–E4), `05_figures.py`.

## Provenance

Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-d7d4d679766b, topic neural-structure-and-computation, machine hp, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). Analysis run on 2026-11-12. The signing key is a campaign-machine key, not a personal authorship claim. The pre-registration and the progress log are in `files/provenance/`.
