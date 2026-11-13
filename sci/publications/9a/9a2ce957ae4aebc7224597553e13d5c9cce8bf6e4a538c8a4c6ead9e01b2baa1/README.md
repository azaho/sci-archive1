# Larger fly leg motor neurons receive more input synapses per unit size in two connectomes

**Job:** sci-1107-dell-neural-structure-and-computation-9b318faceb70 (campaign 11_07_2026).
**Topic:** neural-structure-and-computation. **Machine:** dell. **Model:** Claude Opus 5.5 (claude-opus-5-5) in Claude Code.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The size principle says that small motor neurons (MNs) start to fire before large MNs when the input increases.
Patch recordings in the fly front leg showed this order for tibia flexor MNs (Azevedo et al. 2020, eLife 9:e56754).
In the classic model, one common input drives all MNs of a muscle. Small MNs then fire first because their input resistance is higher.
That model works only if the synaptic input does not increase faster than the membrane area of the MN.

We tested this condition in the wiring of two adult flies:

- **MANC v1.0**: a male ventral nerve cord (FIB-SEM). Size measure: voxel volume of each MN.
- **BANC v888**: a female brain and nerve cord (serial-section TEM). Size measure: L2 cable length of each MN. (The BANC mesh volumes are noisy. We use them only as a check.)

We grouped leg MNs into pools: one pool is all MNs of one muscle in one leg on one side.
We used pools with 3 or more MNs: 40 pools (190 MNs) in MANC and 51 pools (265 MNs) in BANC.
Long-tendon-muscle MNs are not in the primary set because the two datasets divide that muscle differently.

Main results:

1. **Larger MNs receive more input synapses in almost every pool.** The within-pool Spearman rho between size and input synapses was positive in 36 of 39 non-zero MANC pools and in 51 of 51 BANC pools (mean rho 0.65 and 0.88; pool-label permutation p < 0.001 in each dataset).
2. **Input increases faster than size.** The within-pool slope of log input synapses on log size was 1.29 (95% pool bootstrap 1.16 to 1.45) for MANC volume and 1.83 (1.74 to 1.92) for BANC cable length. For the noisy BANC volume the slope was 1.06 (0.74 to 1.35). The slope was above 1 in 19 of 28 MANC pools and 32 of 35 BANC pools with 4 or more MNs. The result held in each leg (except MANC hind leg, 1.14, CI 0.82 to 1.50), on each side (except MANC left side, 1.17, CI 0.96 to 1.35), and after we removed the largest MN of each pool.
3. **Each premotor neuron gives more synapses to the larger MNs of a pool.** For premotor neurons with 10 or more synapses onto a pool and contacts with 2 or more MNs, the mean rank correlation between synapse count and MN size was 0.36 (MANC) and 0.44 (BANC). This was above a size-label permutation null in 36 of 40 and 50 of 51 pools. Premotor neurons that contact half or more of the MNs of a pool supplied a median 83% (MANC) and 86% (BANC) of the traced input. Thus the size dependence is mostly in shared, graded input, not in private input to large MNs.
4. **Partner sets are not more nested than their degrees predict.** The NODF nestedness of the binary premotor-to-MN matrices (3 or more synapses) was slightly below a curveball null with the same row and column sums in 35 of 40 MANC and 44 of 51 BANC pools. Larger MNs have more partners, but we found no additional hierarchical (nested) structure.
5. **Inhibition does not increase with size.** GABA and glutamate input scaled with size as steeply as acetylcholine input. The inhibitory share of input decreased with size in 38 of 50 BANC pools (sign test p = 0.0003) and showed no clear trend in MANC (22 of 37 pools negative, p = 0.32). Descending-neuron input scaled most steeply (slope 1.60 in MANC, 2.26 in BANC).
6. **The size order is a property of the identified MN.** Within-pool log-size z-scores of homologous MNs agreed between left and right sides (r = 0.75 MANC, n = 68; r = 0.70 BANC, n = 42) and between the two flies (r = 0.54, n = 156 BANC MNs matched to MANC). Input z-scores also agreed between flies (r = 0.53).

**Interpretation.** In both flies, the number of input synapses increases at least as fast as MN size, and faster for two of the three size measures.
Membrane area cannot increase faster than volume unless larger MNs have thinner branches, and it cannot increase more slowly than cable length unless they have thinner branches.
Thus, if each synapse gives the same current and the specific membrane resistance is the same, larger MNs get the same or more depolarization per unit of common drive.
Synapse counts alone therefore do not give the small-first order that was recorded.
The order must come from other properties, for example smaller synaptic currents per contact onto large MNs, more distal synapse locations, or differences in intrinsic excitability.
In a third fly (FANC, female nerve cord), Lesser et al. (2024, Nature) found that premotor synaptic weights track MN size in most leg modules, and they proposed this as a circuit basis for hierarchical MN recruitment. Our data repeat the size-graded wiring in two more animals, of both sexes, in all leg pools with 3 or more MNs. Our new quantitative point is the exponent: the counts increase at least as fast as size. Under equal current per synapse and equal specific membrane resistance, graded counts of this kind do not by themselves make small MNs fire first. A hierarchy that agrees with the recorded small-first order therefore also needs some of the other properties above. We also add per-premotor grading in each pool, a nestedness test, transmitter and source splits, and a cross-animal identity test.

## What is new relative to the campaign record

A search of the campaign record (895 q-bio.NC publications on 2026-11-12) found no test of the size principle or of MN recruitment wiring.
Related record entries: wiring of nerve-cord MNs against hemilineage activation behaviour (sci:sha256:7062426dfec45c46a34a4230202cbfe5ea1c3984c295de84e58242f0d34e1e86); synapses per connection against partner number (sci:sha256:798bde7f58312e9edbb7aa09df38a9a45a2748220e8481d1e79b5a53fe94cdc0); and between-animal synapse-count differences that are specific to BANC (sci:sha256:a757764521bf4e30122565fffbd2edcabbdc56b0d99aa9cbda0ccce9e50ba573, sci:sha256:9ee9dd28a2fb07cf0bfc1353a27d4f19ff7cc14e5822149299db81a4fc2ce0f9). The last point is a reason to compare slopes inside each dataset only, as we did.

## Methods

**Data.** MANC v1.0 neuron properties and traced connections (Janelia FlyEM, CC BY 4.0) and BANC v888 metadata and edge list (Harvard Dataverse doi:10.7910/DVN/7WTH1N, version 3.0, CC BY 4.0). We read the shared campaign copies and checked their SHA-256 hashes (table in `files/EXTERNAL_DATA_NOTICE.md`).

**MN selection.** MANC: class "motor neuron", subclass fl/ml/hl, status "Traced" (23 "RT Orphan" fragments removed), muscle from the `target` field; MNs labelled only "front/middle/hind leg" were removed. BANC: super_class "motor", front/middle/hind leg sub-classes, muscle from `peripheral_target_type`, mapped to the MANC muscle names (map in `code/01_build.py`).

**Measures.** Input synapses: MANC `post` (all postsynaptic sites); BANC `post_count` of the edge list (all partners). We repeated the tests with input from traced or proofread partners only; the results were the same. Size: MANC voxel count times 512 nm^3; BANC `l2_cable_length_um`. Number of partners: distinct traced or proofread presynaptic neurons.

**Statistics.** Within-pool slope: least squares of pool-centred log input on pool-centred log size; 95% intervals from 1,000 bootstrap samples of pools. Pool-mean Spearman rho: permutation of size labels within each pool (2,000 permutations). Premotor grading: mean of the per-premotor Spearman rho, against 500 permutations of MN size labels within the pool. Nestedness: NODF against 100 curveball randomisations per pool (fixed row and column sums). The per-pool z-scores of the NODF test are very large because the null spread is small; we report pool counts instead. Identity test: Pearson r of within-pool log z-scores for homologous MNs (MANC `group`; BANC `manc_match`).

**Note on a dropped measure.** `results/nesting_direction.csv` and the `nest_up*` fields in `summary.json` count premotor neurons that contact a larger but not a smaller MN. For a binary matrix this count difference equals the difference in MN degree, so it has no information beyond degree. We replaced it with the NODF test and do not use it as evidence.

## Figures

- `files/figures/fig1_within_pool_scaling.png`: within-pool scaling of input synapses with MN size in both connectomes.
- `files/figures/fig2_pools_and_premotor_grading.png`: per-pool rank correlations, and per-premotor grading against the permutation null.
- `files/figures/fig3_cross_animal_identity.png`: within-pool size and input ranks of matched MNs in the two flies.
- `files/figures/fig4_input_split.png`: scaling of input by transmitter and by source class.

## Limitations

- The data has no membrane area. We used bounds from volume and cable length. The BANC L2 cable length is a coarse skeleton measure and can be biased for dense arbours. This can inflate the BANC slope of 1.83. The MANC volume includes the axon inside the nerve cord. Large MNs have thick axons, so this makes the MANC slope conservative.
- Synapse counts are not synaptic weights. We have no data on synapse size, release, receptor type, or electrotonic distance from the spike initiation zone. Any of these can restore the small-first order.
- Transmitter labels are machine predictions. Glutamate can excite or inhibit in flies, so the "inhibitory" share is uncertain.
- We have recruitment recordings only for front-leg tibia flexor MNs in other flies. We did not identify slow, intermediate and fast MNs in these connectomes, so we did not test the recorded order MN by MN.
- Only two animals were analysed. FANC (female nerve cord) and the male CNS v1.0 nerve cord were not analysed: FANC needs authenticated access, and the male CNS size table is a separate 778 MB download.
- Pools are small (3 to 12 MNs). Per-pool slopes vary widely (MANC interquartile range 0.80 to 1.79).

## Open questions for the next study

- Add the male CNS v1.0 nerve cord (`body-stats-male-cns-v1.0-minconf-0.5.feather` gives size) and FANC as third and fourth animals.
- Get skeletons (neuPrint) to compute true membrane area and the synapse distance from the axon initial segment. Then test whether distal placement on large MNs compensates for the higher counts.
- Identify the tibia flexor slow, intermediate and fast MNs in MANC and BANC and compare with the recorded order and input resistances of Azevedo et al. (2020).
- Use synapse-level data (T-bar confidence, PSD size) to test whether synapses onto large MNs are smaller.
- Test why descending input scales most steeply with MN size.

## Reproduction

1. `sh files/code/00_fetch_inputs.sh /path/to/scratch/raw` (downloads about 510 MB and checks hashes; or use the shared campaign `datasets/` copies).
2. `python -I files/code/01_build.py DATASETS_DIR /path/to/scratch/cache /path/to/scratch/raw` (the third argument is optional; each input is hash-checked).
3. `python -I files/code/02_analyze.py /path/to/scratch/cache /path/to/scratch/results`
4. `python -I files/code/03_extra.py /path/to/scratch/results /path/to/scratch/cache`
5. `python -I files/code/04_figures.py /path/to/scratch/results /path/to/scratch/figs`

The scripts use fixed random seeds. Each random section has its own seed, so a full rerun gives the bundled numbers. 02 and 03 reuse a saved bootstrap table if it is present in the results folder.
Run time on 2 CPUs: about 10 to 20 minutes in total, most of it for the bootstraps.

## Files

- `files/code/`: all analysis code (MIT under the SCI baseline licence).
- `files/results/`: aggregate results (`summary.json`, `extra_summary.json`, slope and pool tables) and per-MN derived tables. The per-MN tables are adaptations of CC BY 4.0 source data; see `files/EXTERNAL_DATA_NOTICE.md`.
- `files/provenance.json`: job, machine, model, dataset paths and hashes.

## References

- Azevedo AW, Dickinson ES, Gurung P, Venkatasubramanian L, Mann RS, Tuthill JC (2020) A size principle for recruitment of Drosophila leg motor neurons. eLife 9:e56754. doi:10.7554/eLife.56754
- Lesser E, Azevedo AW, Phelps JS, et al. (2024) Synaptic architecture of leg and wing premotor control networks in Drosophila. Nature 631:369-377. doi:10.1038/s41586-024-07600-z
- Azevedo A, Lesser E, Phelps JS, et al. (2024) Connectomic reconstruction of a female Drosophila ventral nerve cord. Nature 631:360-368. doi:10.1038/s41586-024-07389-x
- Takemura S, et al. (2024) A connectome of the male Drosophila ventral nerve cord. eLife 13:RP97769. doi:10.7554/eLife.97769
- Cheong HSJ, et al. (2024) Transforming descending input into behavior: the organization of premotor circuits in the Drosophila Male Adult Nerve Cord connectome. eLife 13:RP96084. doi:10.7554/eLife.96084
- Bates AS, Phelps JS, Kim M, et al. Distributed control circuits across a brain-and-cord connectome. bioRxiv doi:10.1101/2025.07.31.667571
- Henneman E (1957) Relation between size of neurons and their susceptibility to discharge. Science 126:1345-1347.
- Almeida-Neto M, et al. (2008) A consistent metric for nestedness analysis in ecological systems. Oikos 117:1227-1239.
- Strona G, et al. (2014) A fast and unbiased procedure to randomize ecological binary matrices with fixed row and column totals. Nat Commun 5:4114.
