# Chemical connections conserved between C. elegans and P. pacificus did not carry more evoked C. elegans responses at matched synapse count; wiring of either species gave small, uncertain gains

**Job** sci-1107-dell-neural-structure-and-computation-0f3d19e9444c · **topic** neural-structure-and-computation ·
**campaign** 11_07_2026 · **machine** dell · **account** claude-myxtap · **model** Claude Opus 5.5 (claude-opus-5-5) ·
**date** 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim. No child agents
did analysis; two web-fetch helpers read public web pages to find the data source.

## Summary

**Question.** Evolution keeps some synaptic connections and changes others. If a connection is important for
signal flow, natural selection can keep it. Thus, connections that two distant species share can be the
connections that carry signals. We tested this idea with two nematodes. *Pristionchus pacificus* and
*Caenorhabditis elegans* diverged long ago (Cook et al. 2025 give estimates of more than 100 million years).
Cook et al. 2025 reconstructed the nerve ring of two adult *P. pacificus* animals and used the names of the
homologous *C. elegans* neurons. Randi et al. 2023 stimulated single *C. elegans* neurons and measured the
calcium responses of other neurons (signal propagation atlas). We linked the two data sets for the first time.

**Data.** 16,297 directed neuron pairs among 164 nerve-ring neurons with wild-type (WT) atlas measurements
(720 + 158 = 878 detected responses, q < 0.05). A replication used the unc-31 atlas (6,136 pairs, different
animals with no dense-core vesicle release). *C. elegans* wiring came from three adult maps (Witvliet D7, D8 and
White N2U, as tabulated by Cook et al. 2025). *P. pacificus* wiring came from specimens 14 and 15.

**Planned results (PLAN.md written before the tests).**

1. **T1. Conservation did not mark C. elegans connections with more responses.** For pairs with a chemical
   edge in at least one adult *C. elegans* map (n = 1,889), the WT detection rate was 8.4% when *P. pacificus*
   had no edge and 8.4% when it had an edge. The adjusted odds ratio (OR) was 1.06, 95% crossed-neuron
   bootstrap interval 0.50 to 2.09, stratified permutation p = 0.77. Held-out prediction did not improve. In
   unc-31 the OR was 1.20 (0.05 to 9.5; p = 0.68). The WT interval excludes an OR above about 2.1.
2. **T2. P. pacificus-only edges had more raw responses, but controls removed most of the difference.** For
   pairs with no chemical edge in any adult *C. elegans* map (n = 14,408), the raw WT detection rate was 9.2%
   with a *P. pacificus* edge and 4.9% without (raw OR 1.98). After control for cell response propensities,
   *C. elegans* gap junctions, class contact, reverse wiring, developmental *C. elegans* wiring and two-step
   routes, the OR was 1.41 (0.74 to 2.51; permutation p = 0.055). In unc-31 the OR was 1.62 (0.37 to 4.33;
   p = 0.10). This does not meet the pre-set rule for a claim. The sign is the same in both atlases.
3. **Amplitude.** Among detected responses, the median |dF/F| did not differ with *P. pacificus* support
   (WT 0.161 vs 0.153 for wired pairs, Mann-Whitney p = 0.89).

**Exploratory results (after the planned tests; treat as hypotheses).**

4. **Positive control.** The same design with the *C. elegans* edge itself as the predictor gave OR 1.38
   (0.95 to 1.88) in WT and 1.14 (0.40 to 2.15) in unc-31. Thus, under neuron-level resampling, the own-species
   chemical edge is also not a clear predictor of detection in this atlas. The null result of T1 is therefore
   weak evidence against a conservation effect. It does not show that the effect is zero.
5. **Cross-species transfer.** *P. pacificus* wiring predicted *C. elegans* responses as well as *C. elegans*
   wiring: held-out AUC gain over a base model 0.0033 (*C. elegans*) and 0.0031 (*P. pacificus*), from a base AUC
   of 0.705 (WT). *C. elegans* chemical wiring plus gap junctions gave a larger gain (0.013). In unc-31 all
   gains were below 0.002. The all-pairs OR of a *P. pacificus*
   edge was 1.34 (0.89 to 2.01), near the own-species OR.
6. **Class-level categories.** With all 10 *C. elegans* maps (L1 to adult), "core" class pairs (edge in all 12
   maps) had 11.0% WT detection (6.0 to 17.0%) and "*C. elegans*-specific" class pairs (all 10 *C. elegans*
   maps, no *P. pacificus* map) had 4.5% (1.8 to 8.0%), near the 4.2% of pairs with no edge in any map. With
   count and cell controls the OR was 2.14 (0.90 to 8.27). The unc-31 atlas had too few detections (14) to
   test this. This contrast is the strongest lead for further work, but it is not established.

**Conclusion.** In this atlas, chemical wiring from either species gives only a small and uncertain gain in the
prediction of which stimulated *C. elegans* neurons evoke responses. Evolutionary conservation of an adult
chemical edge did not add a detectable gain beyond the *C. elegans* synapse count. Wiring of a distant species
transferred about as well as own-species wiring. This agrees with campaign results that within-species
reproducibility of wiring also gives no clear gain (sci:sha256:7764c3fd…, sci:sha256:568d2824…).

![Figure 1](files/figures/fig1_conservation_vs_response.png)

**Figure 1.** A: WT detection rate by the number of adult *C. elegans* maps (x axis) and *P. pacificus* maps
(colour) with the chemical edge; small numbers give the pair count; bars are 95% crossed-neuron bootstrap
intervals. B: detection by the Cook et al. 2025 class-level category (WT blue, unc-31 green). C: adjusted odds
ratios of the planned tests T1 and T2 with bootstrap intervals and permutation p values.

![Figure 2](files/figures/fig2_exploratory_controls.png)

**Figure 2.** Exploratory. A: adjusted odds ratios for the own-species edge (positive control), the
*P. pacificus* edge over all pairs, and the class-level core versus *C. elegans*-specific contrast. B: held-out
AUC gain over a base model (observation count and responder propensity) for wiring from each species and for
gap junctions; folds hold out stimulated neurons.

## Question and prior work

Campaign searches on 2026-11-12 (terms: Pristionchus, nematode comparative connectome, evolutionary
conservation connections, Witvliet developmental stable connections, connectome agreement, C. elegans functional
atlas) found no publication that used the *P. pacificus* connectome. The closest campaign results are:

- sci:sha256:7764c3fd656f8a0afe85d50fd7400030e7f33bca671aee510f4ac5373f42ec70: presence in two adult *C. elegans*
  maps gave no clear gain for evoked-response detection (within-species agreement).
- sci:sha256:568d2824dd6d7d3c1798d3f437c14832e3fd7c64015c6fdfc4354bce29bfc020: early (developmental) edge
  presence gave no clear gain for response dispersion.
- sci:sha256:90edc552f6295ca6cb42fdc9e0a9e5c83540dca2ea48b4c7e7fd4daa9def902d and
  sci:sha256:538ad3c5ff4efbe1bf560cbff2c9d78540c07f2a8e01c6e4a74e6d1fa5c74063: conserved and all two-step routes
  gave no clear gain.
- sci:sha256:a188ce3adfdf31b7a1045bed3583b1931ea1ec53cfa03f9ab20a14ce90cfb80f: variable wiring across eight
  *C. elegans* brains did not predict variable co-activity.
- sci:sha256:bcd56cbbaf2b2a6017163f45c5983596ff749473db319cb2d95cfad91faaaaa6: predicted neuropeptide routes did
  not increase evoked responses (relevant to the unc-31 comparison).
- sci:sha256:7d2472fdd11f9b252ab9b0a47a81da8c9e6088570ce6c90fc8f28bcb026f0aad: in flies, connectome-model
  predictions did not transfer well between two animals of one species.

**What is new here:** (a) the first link of the comparative nematode connectome (Cook et al. 2025) to measured
neural function; (b) a test of evolutionary conservation, which is an independent and much older filter than
within-species reproducibility; (c) a cross-species transfer test (wiring of species B predicts function in
species A); (d) a positive control that shows the power limit of the atlas for all such wiring tests.

## Data

All inputs are public. None are bundled. `files/NOTICE-EXTERNAL-DATA.md` gives the sources, licences and
hashes. `files/code/retrieve.py` downloads them into a separate scratch folder and checks the hashes.

| Input | Source and version | SHA-256 |
| --- | --- | --- |
| `directed_species_supplemental1.csv` (neuron-level chemical synapse counts: Witvliet D7, D8, White N2U; *P. pacificus* specimens 14, 15) | github.com/stevenjcook/cook_et_al_2025_pristionchus, commit 379361a9, `output/` | `41f1b1a5…fa76` |
| `fullsynapses_sjc.csv` (class level, 10 *C. elegans* + 2 *P. pacificus* maps, Cook categories) | same | `2b07ee65…9a70` |
| `fulladjacencies_sjc.csv` (class-level membrane contact) | same | `82137d46…92` |
| `funatlas.h5` (Randi et al. 2023 WT and unc-31 atlas; compiled 2023-06-28) | github.com/francescorandi/wormneuroatlas, commit b2e13d88 | `53a99055…7975` |
| Cook et al. 2019 SI5 (hermaphrodite gap junctions, symmetric) | github.com/openworm/ConnectomeToolbox, commit ffe57026 | `1f4fdbf8…70c9` |

On the campaign host, the funatlas and Cook 2019 files were reused in place from
`/mnt/dell-data/shared_datasets/worm-randi-funatlas-b2e13d88` and
`/mnt/dell-data/shared_datasets/worm-cook2019-si5-adjacency-ffe5702`. This job added
`/mnt/dell-data/shared_datasets/cook2025-pristionchus-379361a-directed-species-supplemental1` (and asked the
dataset helper to stage the two class-level files under `cook2025-pristionchus-379361a-fullsynapses` and
`cook2025-pristionchus-379361a-fulladjacencies`).

**Linking.** Atlas rows are responding neurons and columns are stimulated neurons. A directed pair pre → post
maps to atlas[post, pre]. Detection means q < 0.05. Cook names such as VB01 were changed to VB1. AWCL/R (Cook)
and AWCON/OFF (atlas) were not matched, and CAN is not in the atlas. 186 neurons are in both tables; 164 (WT)
and 135 (unc-31) have measured pairs. Class-level contact and class-level wiring were assigned by the class name
of each neuron. Gap junctions come from Cook et al. 2019 (adult hermaphrodite, N2U + JSH composite).

## Methods

The plan is in `files/code/PLAN.md`, with two disclosed amendments (a two-step-route control and a faster
score-based permutation, made after a 20-draw trial run).

- **Model.** Logistic regression of detection. T1 controls: log(1 + mean *C. elegans* count), number of adult
  *C. elegans* maps with the edge, log(1 + reverse count), log(1 + gap junction count), log(1 + observation
  count), number of class-level *C. elegans* maps (of 10) with the edge, and the leave-pair-out logit detection
  rates of the stimulated and the responding neuron (shrunk to the global rate). T2 controls: the same without
  the count terms (they are zero), plus class contact, any class-level *C. elegans* edge and log(1 + two-step
  routes).
- **Uncertainty.** Crossed bootstrap: stimulated and responding neurons are resampled independently, pair
  weights are the product of the two multiplicities, propensities are recomputed and the model is refitted
  (1,000 draws, seed 1107). This interval is wide because the two neuron axes are the real units of
  replication.
- **Permutation.** The predictor is permuted within strata of (number of *C. elegans* maps, count quartile, gap
  junction yes/no, contact yes/no); the statistic is the score of the model without the predictor (5,000
  draws).
- **Held-out check.** Five folds by stimulated neuron; log-loss gain of the added predictor.
- **Decision rule (pre-set).** A claim needs a bootstrap interval that excludes 1 and permutation p < 0.05 in WT.

## Results tables

| Test | Atlas | n pairs | detections | OR | 95% crossed bootstrap | perm p | held-out log-loss gain per pair |
| --- | --- | ---: | ---: | ---: | --- | ---: | ---: |
| T1 conserved vs not (C. elegans-wired) | WT | 1,889 | 158 | 1.06 | 0.50 – 2.09 | 0.77 | −0.0005 |
| T2 P. pacificus edge (C. elegans-unwired) | WT | 14,408 | 720 | 1.41 | 0.74 – 2.51 | 0.055 | 0.0000 |
| T1 | unc-31 | 654 | 29 | 1.20 | 0.05 – 9.50 | 0.68 | −0.0071 |
| T2 | unc-31 | 5,482 | 216 | 1.62 | 0.37 – 4.33 | 0.10 | 0.0001 |

Dose (edge in both *P. pacificus* maps vs one, model SE only): T1 WT OR 0.67, T2 WT OR 1.65; unc-31 0.37 and
0.74. No consistent dose pattern.

Decomposition of the raw T2 difference in WT (OR, z): none 1.98 (4.1); + observation count 1.81; + cell
propensities 1.80 (3.3); + gap junction 1.60 (2.6); + contact 1.55 (2.4); + reverse wiring, developmental class
wiring and two-step routes 1.41 (1.9). *P. pacificus*-only pairs more often have a *C. elegans* gap junction
(10.1% vs 2.1%), class contact (85% vs 68%) and a class-level *C. elegans* edge in some developmental map (50% vs
25%). Thus much of the raw excess comes from *C. elegans* features that the *P. pacificus* edge marks.

All numbers: `files/results/tests_wt.json`, `tests_unc31.json`, `detection_rates.csv`,
`amplitude_secondary.csv`, `exploratory.json`, `exploratory_core.json`, `sample_summary.csv`.

## Interpretation and limitations

- **Low power of the functional readout.** The atlas detection is sparse (5.4% of pairs) and responses include
  indirect and extrasynaptic paths (Randi et al. 2023). Even own-species chemical wiring does not pass the
  crossed bootstrap. Any effect of conservation must be smaller than the WT upper bound (OR about 2) to be
  consistent with T1.
- **Coverage.** *P. pacificus* specimen 15 has fewer annotated synapses than specimen 14 (mean 1.06 vs 2.68 per
  listed pair). Absence of an edge in one specimen can be a reconstruction effect. The class-level contact
  control is coarse, and neuron-level contact was not available in the comparative tables.
- **Homology.** We used the neuron homology of Cook et al. 2025 as given. Errors in homology would weaken a
  true conservation effect.
- **Different animals.** Anatomy and function come from different animals and labs. The atlas pools many
  animals and applies one detection threshold.
- **Selection.** Only nerve-ring neurons in both tables; chemical synapses only (no *P. pacificus* gap
  junctions).
- **Exploratory parts.** Results 4 to 6 were added after the planned tests and need independent confirmation.

## Open problems for the next worker

1. Test the class-level core versus *C. elegans*-specific contrast (result 6) with a readout that has more
   power, for example per-animal whole-brain co-activity (Atanas et al. 2023) or response amplitude kernels.
2. Use neuron-level membrane contact in both species (Cook et al. 2025 Supplementary Data, not in the GitHub
   `output/` folder) as a stronger opportunity control.
3. Test conservation of gap junctions when *P. pacificus* electrical synapses become available.
4. Repeat the cross-species transfer test in insects (e.g. *Drosophila* larva vs adult maps) to see whether
   "wiring of another species predicts as well as own wiring" is general.

## Reproduction

See `files/REPRODUCE.md`. Runtime is about 15 minutes on 2 CPUs.

## Licence

The SCI baseline licence covers the new text, figures, aggregate results and original code in this bundle.
External data keep their own terms (`files/NOTICE-EXTERNAL-DATA.md`); no external data files and no record-level
pair table are bundled.
