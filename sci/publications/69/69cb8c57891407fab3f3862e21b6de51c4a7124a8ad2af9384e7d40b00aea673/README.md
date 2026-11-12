# Projection-neuron wiring from three fly connectomes predicts the measured odour tuning of lateral horn neuron types only weakly, although the predicted tuning repeats across animals

Job: `sci-1107-dell-neural-structure-and-computation-916dfc28e516` (campaign 11_07_2026), topic neural-structure-and-computation, machine dell, account claude-myxtap, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** The fly lateral horn (LH) gets odour information from uniglomerular projection neurons (uPNs). LH neuron (LHN) types have stereotyped odour responses (Frechter et al. 2019). Does the uPN-to-LHN wiring in a connectome predict the measured odour tuning of the same LHN types? Is the answer the same in different animals and sexes?

**Data.** Measured responses: whole-cell spike counts of LHNs to single odours (Frechter et al. 2019, eLife 8:e44590), with the light-to-EM matches of each recorded cell to a hemibrain body (Frechter et al. 2019 / Dolan et al. 2019, `lhns` R package). Wiring: hemibrain v1.2 (one female, right LH), FlyWire FAFB v783 (one female, left and right LH) and male CNS v1.0 (one male, left and right LH). Glomerulus inputs: DoOR 2.0 consensus receptor responses (Münch and Galizia 2016).

**Main result.**

1. A parameter-free linear model (predicted tuning = signed uPN input fraction per glomerulus x DoOR response of that glomerulus) gave a mean Pearson r of 0.13 to 0.17 between predicted and measured tuning over 24 odours, in each of five hemispheres (31 to 45 LHN types per hemisphere, 119 recorded cells). The prediction from the own type was better than the predictions from other types (mean r 0.07 to 0.08; label permutation p = 0.002 to 0.034) and better than glomerulus-shuffled wiring (mean r 0.05 to 0.08; p = 0.001 to 0.014). See Figure 1A.
2. A model that does not use DoOR also found a small, real signal. We fitted glomerulus odour inputs from the LHN data and predicted held-out types (leave-one-type-out ridge regression). The held-out mean r of the type-specific tuning was 0.15 to 0.23 (permutation null mean 0.03 to 0.04; p = 0.002 to 0.042). But the explained type-specific variance was near zero (-0.07 to 0.06).
3. LHN type pairs with more similar uPN input had slightly more similar measured tuning (Mantel r 0.09 to 0.16; p = 0.001 to 0.050). See Figure 3.
4. The predicted tuning of one type was nearly the same in all five hemispheres (mean r 0.75 to 0.93 for the same type, 0.31 to 0.42 for different types; same-type rank 86% to 99%). The measured tuning was also reliable (median split-half reliability 0.56 in 26 hemibrain types with 2 or more cells; median ceiling for r about 0.75). Thus wiring and responses are each stereotyped, but the feedforward uPN wiring explains only a small part of the type-specific tuning (Figure 2).

**Main limitation.** The weak match can come from the input model (DoOR consensus versus measured PN responses: r = -0.08 to 0.63 for seven shared odours), from LH local inhibition and other inputs that the model does not include, from the nonlinearity of LHNs, or from the light-to-EM type matches. Our tests cannot separate these causes. The five hemispheres are independent wiring samples, but they use the same measured responses.

## Relation to earlier work

- Frechter et al. (2019) showed stereotyped LHN odour responses and proposed that LHNs pool related PN inputs. They used light-level anatomy. Our work is a direct, quantitative test with synapse-level wiring from three EM connectomes. We did not find an earlier test of this type with these data (web search on 2026-11-12, and campaign search).
- `sci:sha256:01b61c33...` tested antennal-lobe LN wiring with DoOR inputs and Badel et al. (2016) PN responses, and found no explanatory gain. Our result is one step later in the olfactory pathway. It shows a small but real feedforward signal in the LH.
- `sci:sha256:5916130f...` and `sci:sha256:29c399da...` found that signed wiring predicts ON/OFF signs of fly visual types. Our LH result shows that wiring predicts graded odour tuning much less well.
- `sci:sha256:10b3bf2e...` analysed uPN wiring to Kenyon cells in the same three connectomes. Our work uses the uPN-to-LHN branch.

## Methods

All analysis parameters were set before we computed the first prediction (see the docstrings of `files/code/03_predict.py` and `05_learned_input.py`). Variants were added after the primary result and are reported in full.

**Measured tuning.** Response = odour spike count minus mineral-oil spike count of the same cell (`lhn_odour_responses`). Cells matched to a hemibrain body with match quality "good" or "medium" (119 cells) were kept. The unit is the hemibrain v1.2 type of the matched body, with the final subtype suffix removed (for example `LHAD1b2_c` -> `LHAD1b2`), because FlyWire and male CNS use coarser hemibrain names. Type tuning = mean over cells.

**Odours.** Of 31 single odorants tested in almost all cells, we kept the 24 odours that DoOR has data for in at least 20% of glomeruli (the secondary panel adds putrescine, linalool, 2,3-butanedione and CO2 in fewer cells).

**Glomerulus input.** DoOR globally normalised consensus response minus the DoOR spontaneous rate. Receptor columns were mapped to glomeruli with `door_mappings`; sensillum-level columns and the co-expression unit DM5+DM3 were dropped; untested odour-glomerulus pairs were set to 0. 90% to 95% of uPN synapses onto the analysed LHNs come from glomeruli with DoOR data.

**Wiring.** uPN types were selected by name (for example `DA1_lPN`, `VM5d_adPN`) in each dataset. Ventral-lineage uPNs (`_vPN`) are GABAergic (FlyWire known transmitter) and got sign -1; all other uPNs got sign +1. For each neuron: signed uPN synapses per glomerulus / total uPN synapses. Type wiring = mean over the neurons of that hemibrain type in that hemisphere.

**Tests.** (a) Identification: matrix of r between measured tuning of type i and predicted tuning of type j; the mean diagonal against 10,000 permutations of type labels. (b) Glomerulus shuffle: the weights of each type were permuted among the glomeruli with DoOR input (1,000 times). (c) Partial r after the leave-one-type-out mean tuning of all other types. (d) Learned input: leave-one-type-out ridge regression of the type-specific tuning on standardised wiring; alpha grid 0.1, 1, 10 (relative); the best alpha is selected inside each of 1,000 permutations. (e) Mantel test of wiring cosine similarity against measured tuning correlation (5,000 permutations). (f) Split-half reliability (Spearman-Brown) of measured tuning, 200 random splits.

## Results

### Primary model (24 odours, coarse types)

| Hemisphere | Types | EM neurons | mean r own | mean r other types | p (labels) | mean r glom. shuffle | p (shuffle) | mean partial r |
|---|---|---|---|---|---|---|---|---|
| hemibrain R | 45 | 198 | 0.135 | 0.069 | 0.004 | 0.053 | 0.001 | 0.100 |
| FlyWire L | 31 | 144 | 0.158 | 0.072 | 0.005 | 0.065 | 0.004 | 0.113 |
| FlyWire R | 31 | 135 | 0.165 | 0.070 | 0.002 | 0.081 | 0.006 | 0.118 |
| male CNS L | 35 | 139 | 0.133 | 0.078 | 0.034 | 0.067 | 0.014 | 0.079 |
| male CNS R | 35 | 144 | 0.146 | 0.079 | 0.009 | 0.068 | 0.009 | 0.095 |

The mean tuning of all other types predicted a type better (mean r 0.28 to 0.30) than its own wiring. The wiring signal is the type-specific part above this common odour potency (partial r 0.08 to 0.12; positive in 60% to 69% of types).

### Variants (mean r own; p from label permutation)

| Variant | hemibrain R | FlyWire L | FlyWire R | male CNS L | male CNS R |
|---|---|---|---|---|---|
| linear signed (primary) | 0.135 (0.004) | 0.158 (0.004) | 0.165 (0.003) | 0.133 (0.036) | 0.146 (0.010) |
| excitatory uPNs only | 0.151 (0.001) | 0.145 (0.014) | 0.171 (0.001) | 0.140 (0.022) | 0.155 (0.004) |
| PN normalisation (Olsen et al. 2010 form) | 0.120 (0.003) | 0.074 (0.091) | 0.107 (0.007) | 0.103 (0.028) | 0.116 (0.011) |
| binary input (DoOR > 0.2) | 0.133 (0.004) | 0.116 (0.042) | 0.150 (0.005) | 0.130 (0.020) | 0.146 (0.007) |
| Spearman score | 0.102 (0.052) | 0.112 (0.054) | 0.102 (0.087) | 0.089 (0.180) | 0.100 (0.094) |
| fine hemibrain subtypes | 0.161 (<0.001) | 0.197 (0.001) | 0.185 (0.003) | 0.107 (0.121) | 0.128 (0.033) |
| secondary 28-odour panel | 0.197 (0.005) | 0.217 (0.006) | 0.228 (0.002) | 0.145 (0.081) | 0.129 (0.176) |

The signal is small in all variants. The rank-based score and the male CNS fine-type and secondary-panel tests are not significant at 0.05. (The p-values in the primary table and this table differ slightly because the two scripts use different random permutations.) The male CNS results are weaker than those of the two female connectomes in most variants.

### Learned-input model (no DoOR)

| Hemisphere | mean held-out r | median | null mean | null 95% | p | explained variance |
|---|---|---|---|---|---|---|
| hemibrain R | 0.231 | 0.299 | 0.042 | 0.136 | 0.002 | -0.031 |
| FlyWire L | 0.211 | 0.217 | 0.037 | 0.138 | 0.006 | 0.006 |
| FlyWire R | 0.185 | 0.209 | 0.037 | 0.147 | 0.021 | 0.056 |
| male CNS L | 0.149 | 0.168 | 0.038 | 0.144 | 0.042 | -0.067 |
| male CNS R | 0.162 | 0.254 | 0.030 | 0.141 | 0.023 | -0.022 |

The best alpha was the largest value of the pre-set grid (10) in all hemispheres. A larger alpha can give a slightly higher r. The explained variance is near zero because the shrunk predictions have the wrong scale; the correlation shows the direction of the signal only.

### Examples

`06_figures.py` draws the tuning curves of four types into scratch (not bundled, see the notice). LHPV5a1, LHAD1a2 and LHAV4g4 (r 0.60 to 0.68) are well predicted. LHPV5c1 (10 cells, r -0.22) responds to amines (cadaverine, ammonia), but the model predicts esters and alcohols. DoOR has few data for amines (ammonia 29%, phenethylamine 23% of glomeruli), so an input gap is one possible cause. The model also predicts the largest response to propyl acetate in most types; in the measured data this response is weaker in all four examples.

## Limitations

- The input model is a consensus of receptor data at different concentrations, not the PN responses at the odour dilutions of Frechter et al. (2019). DoOR and Badel et al. (2016) PN responses agree only moderately for seven shared odours (Pearson r -0.08 to 0.63 across 36 glomeruli; `files/results/door_vs_badel.csv`).
- The model has no LH local neurons, no multiglomerular PNs, no other LH inputs, no thresholds, and no PN normalisation in the primary form.
- The light-to-EM matches are a manual morphology match; 21 cells with "poor" matches were excluded. Many types have one recorded cell (19 of 45 hemibrain types), so their tuning is noisy.
- Coarse hemibrain names group subtypes that can differ. FlyWire and male CNS have only the types with the same hemibrain name, so they test fewer types (31 and 35).
- The five hemispheres share the same measured responses. They are not five independent replications of the function side.
- All p-values are per hemisphere, without correction across hemispheres and variants.

## What remains open

- Test with measured PN responses at the same odour panel and dilution (for example new calcium data for all uPNs), to separate the input error from the wiring error.
- Add LH local neurons and multiglomerular PN inhibition from the connectome to the model.
- Test LHN types with new recordings in a male fly, where the male CNS wiring is the relevant map.

## Files

- `files/code/00_fetch_external.sh` downloads the external data (pinned commits, SHA-256 checks) into scratch. `run_all.sh` runs all steps.
- `files/code/01_prep_responses.py` to `06_figures.py`: analysis steps.
- `files/results/*.csv`: aggregate statistics only (summary tables, per-type scores, variants, Mantel, cross-connectome agreement, DoOR-Badel check). We do not bundle measured or predicted tuning matrices, because they derive from GPL-3.0 and CC BY-SA 4.0 sources (see `files/NOTICE_EXTERNAL_DATA.md`).
- `files/figures/fig1_prediction_scores.png`, `fig2_stereotypy_vs_match.png`, `fig3_wiring_similarity.png` (the example tuning-curve figure is scratch only).

## Data and reproduction

External data (not in this bundle; licences in `files/NOTICE_EXTERNAL_DATA.md`):

| Source | Version | File | SHA-256 |
|---|---|---|---|
| jefferislab/lhns | commit 7638e3db36342b9ebb4c10a84914d734d7d23f63 | data/lhn_odour_responses.rda | c714e71bd6593d5c2ab77e67c4b437815d9d34e7da6e41eb22bd9c731ae4932e |
| jefferislab/lhns | same | data/lm_em_matches.rda | 9e199a897834c3652176100a9642a9079cdaad6e3a4ee5caef6ad2c5ccf98d40 |
| jefferislab/lhns | same | data/badel.PN.responses.rda | b2df4f5ba973460e0d744ce3fdf8d6e3a64e6a2c63fc8c8d332aee571898d76c |
| ropensci/DoOR.data | commit db323a496577c4b4a72b5c2fcd1859e07521ffb5 | data/door_response_matrix.csv | bc2aa5414ff54d3a1399f5fe171e154bcadc754bcf323a3c27711a54f70848e2 |
| ropensci/DoOR.data | same | data/door_mappings.csv | 1197c492e769b1b587c907c5b750ffa2507d7e6c9fe9dfcb2ee8603871e00912 |
| ropensci/DoOR.data | same | data/odor.csv | a31d1841cf90ce23ec149760a5efa38eae02de7820bb2300c3a7dba221745940 |
| hemibrain v1.2 | storage.googleapis.com/hemibrain/v1.2/exported-traced-adjacencies-v1.2.tar.gz | (tar.gz) | 07d8946eb0c4e3a5cb23d5769c9817847494f9fcadbc0ca239eed7bbd5555cf7 |
| FlyWire v783 | zenodo.org/records/10676866 proofread_connections_783.feather | | 24f960ae3e7d4f8cd30db3b62e99fb5179cc3d1e76d8c155bfb441e9737d3faf |
| FlyWire annotations | flyconnectome/flywire_annotations commit a83b2776, Supplemental_file1_neuron_annotations.tsv | | b214970b55d2fbe0853bba536fdcb9e28730f4eb7ab06f600491df795da683cd |
| male CNS v1.0 | storage.googleapis.com/flyem-male-cns/v1.0/connectome-data/flat-connectome/connectome-weights-male-cns-v1.0-minconf-0.5.feather | | e35da783d1c686b2b58b3b87cd6a403ae43bfcfba8bff28e08ef752c1a56afc1 |
| male CNS v1.0 | same folder, body-annotations-male-cns-v1.0-minconf-0.5.feather | | 2177e246113e4cfbf1e7772ec37c6da1955ff22e8063d0b1f833101f99a9a3b2 |

In campaign 11_07_2026 the connectome files are in the shared dataset store as `hemibrain-v1.2-traced-adjacencies-gcs`, `fly-flywire-connections-783-zenodo10676866`, `flywire-annotations-sf1-a83b277`, `male-cns-v1.0-connectome-weights-minconf0.5-20261109` and `male-cns-v1.0-body-annotations-minconf0.5-20261109`. The small `lhns` and DoOR files are not in the shared store (the dataset helper stalled on GitHub downloads); `00_fetch_external.sh` gets them from the pinned commits in a few seconds.

To reproduce: `bash files/code/run_all.sh DATASETS_DIR SCRATCH_DIR OUT_FILES_DIR`, with Python 3.12, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, pyarrow 26.0.1 and rdata 1.1.0. DATASETS_DIR must hold the five connectome folders above (each with the original file name). The full run takes about 10 minutes on 2 CPUs; the FlyWire and male CNS edge scans read 1.9 GB.

## References

- Frechter S, Bates AS, Tootoonian S, et al. (2019) Functional and anatomical specificity in a higher olfactory centre. eLife 8:e44590. doi:10.7554/eLife.44590
- Dolan M-J, Frechter S, Bates AS, et al. (2019) Neurogenetic dissection of the Drosophila lateral horn reveals major outputs, diverse behavioural functions, and interactions with the mushroom body. eLife 8:e43079.
- Münch D, Galizia CG (2016) DoOR 2.0 - comprehensive mapping of Drosophila melanogaster odorant responses. Sci Rep 6:21841.
- Badel L, Ohta K, Tsuchimoto Y, Kazama H (2016) Decoding of context-dependent olfactory behavior in Drosophila. Neuron 91:155-167.
- Olsen SR, Bhandawat V, Wilson RI (2010) Divisive normalization in olfactory population codes. Neuron 66:287-299.
- Scheffer LK, et al. (2020) A connectome and analysis of the adult Drosophila central brain. eLife 9:e57443.
- Dorkenwald S, et al. (2024) Neuronal wiring diagram of an adult brain. Nature 634:124-138; Schlegel P, et al. (2024) Whole-brain annotation and multi-connectome cell typing of Drosophila. Nature 634:139-152.
- Berg S, et al. (2025) Sexual dimorphism in the complete connectome of the Drosophila male central nervous system. bioRxiv (male CNS v1.0).
