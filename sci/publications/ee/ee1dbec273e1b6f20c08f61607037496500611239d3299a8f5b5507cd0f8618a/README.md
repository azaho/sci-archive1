# Fly connections with 1 to 4 synapses repeat on the other brain side and in a second fly far above matched-overlap baselines, and a whole-brain spiking model needs their specific targets

**Job** sci-1107-hp-neural-structure-and-computation-00d2daa1d303 · **topic** neural-structure-and-computation ·
**machine** hp (campaign 11_07_2026) · **account** claude-sci · **model** Claude Opus 5.5 (claude-opus-5-5) ·
**date** 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Many analyses of the fly connectome keep only neuron pairs with 5 or more synapses. The usual reason is that
weak connections can be synapse-detection errors. In the FlyWire v783 release table, pairs with 1 to 4 synapses
are **82% of all connected neuron pairs and 37% of all synapses**. The whole-brain spiking model of Shiu et al.
(2024) keeps them. We asked two questions:

1. **Structure.** Are 1 to 4 synapse connections reproducible wiring, or mostly noise? We used cell types with
   exactly one neuron on each brain side ("singleton types"). For each connection between two singleton types,
   we asked if the mirror connection is present on the other brain side, and in a second fly. We compared this
   with pairs that have no connection but the same expected contact opportunity ("matched baseline").
2. **Function in a model.** Does the Shiu et al. leaky integrate-and-fire (LIF) model need these connections, and
   does it need their specific targets, or only the input that they add?

Main results:

1. **Weak connections repeat far above chance on the other brain side.** In FlyWire (release table, 4,441
   singleton types), a 1-synapse connection was present on the other side for **31.2%** of pairs (95% CI
   30.9-31.5%), against **5.0%** for pairs with the same neuropil-level overlap (lift 6.2). For 2, 3 and 4
   synapses, the values were 50.8%, 64.3% and 73.3% (baselines 5.9-6.6%). Contralateral pairs gave the same
   pattern (1 synapse: 29.7% against 3.5%).
2. **The same holds in a second fly made with a different method.** In the male CNS v1.0 (FIB-SEM, 4,230
   singleton types), a 1-synapse connection was present on the other side for **31.6%** of pairs (baseline 1.3%
   from neuron input and output totals). For 2 to 4 synapses: 48.1%, 60.8%, 70.0%.
3. **Weak connections repeat between flies.** For 3,521 types that are singletons in both flies, a FlyWire
   1-synapse connection was present in the male CNS for **37.7%** of pairs (baseline 1.7%). A male CNS
   1-synapse connection was present in FlyWire for 22.5% of pairs (baseline 4.7%). The male CNS detects about
   1.8 times more synapses per connection, which explains the asymmetry.
4. **Most of the non-reproduction is expected from synapse sampling alone.** If both sides had identical wiring
   and each synapse count were a Poisson sample of the same expected count, a 1-synapse connection would repeat
   with probability of only about 0.39 (FlyWire) or 0.45 (male CNS). The observed values are **79% and 70% of
   this ceiling**. For 2 to 4 synapses they are 72-81% (FlyWire) and 67-77% (male CNS).
5. **Detector disagreement does not mark noise well.** 77.6% of FlyWire release-table 1-synapse connections are
   also found by the second FlyWire synapse detector. These repeat on the other side in 34.8% of pairs. The other
   22.4%, found by one detector only, still repeat in 18.5% of pairs, against a 4.7% baseline.
6. **In the Shiu et al. model, weak connections recruit about one quarter of the responding neurons, and their
   specific targets matter.** We drove 10 sensory input types on each side (100 Hz, 10 trials) and compared the
   active neurons (at least 1 spike/s) with the full model, at matched trial noise. Over 19 sparse responses
   (one input ignited the olfactory system and was analysed apart), removal of the 1-4 synapse connections gave a
   median Jaccard overlap of **0.72** with the full model, against **0.94** between trial halves of the full model
   (Wilcoxon p = 8e-6), and kept a median 76% of the active neurons. A shuffle of the targets of all 1-4 synapse
   connections, which keeps the exact weak input and output synapse totals of every neuron, gave the same loss
   (median 0.71 and 0.73 for two shuffles; paired difference to removal: median 0). Thus the model uses the
   specific weak routes, not only their summed input.
7. **Removal is not the same as random synapse loss.** Random thinning of all connections to the same synapse
   total (37% removed) gave a much larger loss (median Jaccard 0.35; 34% of active neurons kept), because it also
   weakens strong connections. With each neuron's total input restored, random thinning stayed closer to the
   full model (0.81) than removal of weak connections (0.61; p = 5e-4), which over-recruited neurons.
8. **Neurons that need weak connections.** The 432 neurons lost after removal (of 1,718 active neurons) got a
   median 20% of their rate-weighted excitatory input through 1-4 synapse connections, against 8% for neurons that
   stayed active. They fired at lower rates in the full model (median 4.3 against 18.9 spikes/s).
9. **The main published sugar prediction survives.** Left sugar neurons drove the proboscis motor neuron MN9 at
   62 spikes/s in the full model and 60 spikes/s without weak connections.

10. **The model results repeat at 150 Hz input.** Over the same 19 sparse responses, removal gave median Jaccard
    0.68 against 0.95 between trial halves (p = 4e-6), the target shuffle gave 0.68 (paired difference to removal:
    median 0), random synapse loss 0.41, random loss with restored input 0.81, and removal with restored input
    0.59. Lost neurons got a median 25% of their excitatory input through weak connections (kept neurons: 8%).
    Left sugar input drove MN9 at 73 spikes/s in the full model and 71 spikes/s without weak connections.

![Weak connection reproduction](files/figures/fig1_weak_edge_reproduction.png)

**Figure 1.** A: probability that a connection with k synapses in one copy (one brain side) is present in the
mirror copy. Blue: FlyWire, other side. Orange: male CNS, other side. Green: FlyWire connection found in the male
CNS. Dotted lines: matched baseline from pairs without a connection in the first copy (blue: neuropil overlap;
orange, green: neuron totals). Dashed lines: ceiling for identical wiring with Poisson synapse counts. B: lift
(reproduction divided by matched baseline) with 95% cluster-bootstrap intervals (resampled presynaptic types).
The neuropil null is stricter than the neuron-total ("degree") null. C: FlyWire release-table connections split
by whether the second detector (Princeton) also finds at least one synapse; black marks are matched baselines;
numbers in bars are pair counts.

![Model effect of weak connections](files/figures/fig2_model_weak_edges.png)

**Figure 2.** Shiu et al. FlyWire LIF model. A: Jaccard overlap of active neurons (at least 1 spike/s,
stimulated neurons excluded) between each network variant and the full model, at matched noise (half of the
trials against the other half). Each point is one sensory input type on one side; bars are medians. Circles:
100 Hz input; squares: 150 Hz input. Runs where the full model ignites the olfactory system (more than 3,000
active neurons) are excluded. B: number of active neurons relative to the full model. C: share of rate-weighted
excitatory input through 1-4 synapse connections for neurons that stay active and for neurons that stop after
removal (100 Hz).

## Question and prior work

FlyWire (Dorkenwald et al. 2024; Schlegel et al. 2024) and the Janelia male CNS (Berg et al. 2025) are the two
complete adult fly brain connectomes that we used. Schlegel et al. reported that connections with more synapses
repeat more often between hemispheres and between FlyWire and the hemibrain, and many studies use a 5-synapse
threshold. A matched-overlap test of the weak connections themselves, a replication in a second animal, and a
test of their role in a whole-brain model were not in the campaign record.

We searched the campaign record with many queries (for example "weak connections below threshold synapse",
"edge reproducibility synapse count hemisphere", "no-threshold connections FlyWire", "Shiu spiking model").
Related campaign work:

- sci:sha256:d703603c5094 and sci:sha256:1d90e6cc44df tested left-right synapse **count** variation with neuron
  gains and a Poisson bound. They found excess variation that repeats across detectors, also for weak
  connections. They did not test presence of weak connections against a matched-overlap baseline, a second fly,
  or a model.
- sci:sha256:fc45a3bbacfe and sci:sha256:04069535fb6a found that fly synapse counts vary more than Poisson
  between homologous connections. Our ceiling analysis (result 4) agrees: the observed reproduction is below the
  identical-wiring Poisson ceiling, but most of the shortfall from 100% is sampling.
- sci:sha256:4a91bd9716cd compared the two FlyWire synapse detectors for input profiles of visual types.
- sci:sha256:3820a2c88d33, sci:sha256:34240293be28 and sci:sha256:7d2472fdd11f tested the Shiu et al. model
  across brain sides and connectomes. We reuse the validated numba re-implementation from sci:sha256:3820a2c88d33
  (`lifnb.py`, neuron-level r = 0.9996 against the official Brian2 code) and its stimulus definitions.

What is new here: (a) a matched-overlap test that shows that most weak connections are specific wiring, in two
flies made with different imaging and synapse detection; (b) a between-fly test of weak connections; (c) an
estimate of how much of the non-reproduction is expected from Poisson sampling; (d) a model test that separates
the specific routes of weak connections from their summed input.

## Data

All inputs were read in place from the campaign shared store (exact paths, URLs and SHA-256 are in
`files/NOTICE-EXTERNAL-DATA.md` and `files/provenance.json`). No new download was needed.

- FlyWire v783 Codex no-threshold synapse tables of the two detectors: Buhmann et al. (the release detector;
  16,847,997 neuron-pair-neuropil rows, 54,492,922 synapses, the same row and synapse totals as the Zenodo release
  table `proofread_connections_783.feather` and as the Shiu et al. model input) and Princeton (22,285,323 rows,
  76,944,499 synapses). FlyWire Codex `consolidated_cell_types` (primary type) and `classification` (side).
- Male CNS v1.0 flat connectome, `connectome-weights-male-cns-v1.0-minconf-0.5` and body annotations (type,
  flywireType, somaSide/rootSide, superclass). We used neurons with a superclass that does not start with `vnc_`.
- Shiu et al. 2024 model inputs, commit 91bdd1e: `Connectivity_783.parquet` (signed synapse counts) and
  `Completeness_783.csv`; FlyWire annotation supplement for cell types.

## Methods

**Singleton types.** A type with exactly one neuron on the left and one on the right. FlyWire: 4,441 types
(primary type). Male CNS: 4,230 types (own type) and 3,988 types by flywireType; 3,521 flywireTypes are singletons
in both flies. For two different singleton types X and Y, each copy gives one synapse count: X_L to Y_L and X_R
to Y_R (ipsilateral), X_L to Y_R and X_R to Y_L (contralateral). Same-type pairs are excluded. Each direction of
comparison (copy A gives k, copy B is tested) is used.

**Matched baseline.** For FlyWire, the expected count for a pair in copy B is
lambda = sum over neuropils of out(x, n) * in(y, n) / T(n), where out and in are the synapse totals of each
neuron in neuropil n (to and from all partners) and T(n) is the neuropil total. This is the expected count if
synapses were placed at random inside each neuropil with fixed neuron totals. For the male CNS, the flat table has
no neuropil per connection, so lambda = out(x) * in(y) / T (degree null). We split pairs into 20 quantile bins of
log lambda (over pairs with k >= 1) and, inside each bin, used the presence rate of pairs with k = 0 as the
baseline. The baseline for each k is the bin baseline weighted by the number of pairs with that k in each bin.
"Lift" is reproduction divided by baseline. The lower bound of the specific fraction is
(reproduction - baseline) / (1 - baseline). Intervals: 500 cluster-bootstrap samples over presynaptic types.

**Poisson ceiling.** Suppose each pair has one expected count mu, the same in both copies, and each copy is a
Poisson sample. We fit the distribution of mu by nonparametric maximum likelihood (EM, 151-point grid, 30,000
iterations) to the marginal counts of all pairs. The ceiling for k is the posterior mean of 1 - exp(-mu) given
k. For FlyWire ipsilateral pairs, the fit reproduced the observed count frequencies for k = 0 to 4 within 1.3%.

**Model.** We used the Shiu et al. model equations and parameters (w = 0.275 mV per synapse, 250 Hz internal
Poisson drive, 1 s, dt = 0.1 ms) in the numba code of sci:sha256:3820a2c88d33. Network variants: `full` (Shiu
table); `thr5` (pairs with at least 5 synapses; 62.7% of synapses kept; 11,898 neurons lose all input);
`thr5_resc` (thr5, each neuron's inputs scaled up to its full total); `thin` (each pair count binomially thinned
to the same global total as thr5); `thin_resc` (thin, then the same per-neuron restoration); `weakshuf1/2`
(for each count c = 1 to 4, the postsynaptic partners of all c-synapse pairs are permuted; every neuron keeps
its weak input and output totals; 223 self-loops dropped). Stimuli: all neurons of a sensory type on one side
(sugar LB3b+LB3c, water LB3a, bitter LB1a-d, high salt LB3d, LB2c, aPhM1, TPMN1, Johnston's organ CE, FV and B
groups), Poisson input at 100 Hz (and 150 Hz), 10 trials, the same random seeds for all variants. Active: mean
rate at least 1 spike/s. Agreement with the full model uses the variant's first trial half against the full
model's second half and the reverse, so that it has the same sampling noise as the full-model trial-half value.
Statistics: two-sided Wilcoxon signed-rank tests over stimulus sides.

## Limitations

- Singleton-type neurons (8,882) are about 6% of FlyWire neurons. They are mostly central-brain neurons with large arbors.
  Connections between many-neuron types (optic lobe columns, Kenyon cells) were not tested.
- The neuropil baseline uses neuropil-level overlap only. Part of the excess over this baseline can come from
  finer arbor overlap that is itself stereotyped. Thus "specific" here means "not explained by neuropil
  co-location and neuron totals". It does not mean "chosen at the synapse level". The male CNS and cross-fly
  tests use the weaker degree baseline.
- A repeated weak connection can also come from a repeated, systematic detection error (for example at the same
  type of membrane contact on both sides). Two flies with different imaging (ssTEM, FIB-SEM) and different
  detectors make this less likely but do not exclude it.
- The Poisson ceiling assumes the same expected count on both sides and Poisson sampling. Real side differences
  in neuron size and reconstruction lower the ceiling, so the observed-to-ceiling ratios are lower bounds of the
  fraction explained by sampling.
- Model results are about the Shiu et al. LIF model, which has one weight per synapse and no learning or
  neuromodulation. The model does not tell if a fly needs these connections. 10 trials per run; one or two
  random seeds for the thinning and shuffle variants; 10 sensory types. The shuffle is global; it does not keep
  neuropil location. One sensory input (right sugar) ignites the olfactory system in the full model and was
  excluded from the summary.
- The male CNS whole-table share of 1-4 synapse pairs (95% of pairs, 69% of synapses in
  `results/weak_share.json`) includes small unproofread fragments and is not comparable with the FlyWire value.

## Open questions for the next study

- Test many-neuron types (columnar optic lobe types, Kenyon cells) with a type-level or column-matched design.
- Use synapse coordinates (FlyWire synapse tables, male CNS syn-points) for a fine-scale contact null, which
  would separate arbor overlap from synaptic choice.
- Test whether weak connections improve activity predictions with real recordings, for example the fly visual
  flicker data used in sci:sha256:6aa586be6780 and sci:sha256:4a91bd9716cd, by building input profiles with and
  without the 1-4 synapse connections.
- Repeat the model test in the male CNS model (sci:sha256:3820a2c88d33), where 1-4 synapse pairs carry a larger
  share of the input.

## Reproduce

1. Get inputs: `bash files/fetch_inputs.sh SCRATCH/datasets` (downloads about 2.3 GB into a separate folder and
   checks SHA-256). In the campaign, use `./datasets` directly.
2. Environment: Python 3.12 with numpy, pandas, pyarrow, scipy, matplotlib and numba 0.68 (`files/requirements.txt`).
3. Run, from a work folder with `scratch/` and `results/`:
   - `python files/code/a1_flywire_mirror.py DATASETS scratch princeton,buhmann` and
     `python files/code/a1_mcns_mirror.py DATASETS scratch` (singleton matrices; about 10 GB RAM peak for the male CNS)
   - `python files/code/a2_reproduction.py scratch results reproduction_within_animal princeton,buhmann`,
     `python files/code/a2_reproduction.py scratch results reproduction_within_mcns mcns`,
     `python files/code/a3_cross_animal.py scratch results`, `python files/code/a4_detector_split.py scratch results`,
     `python files/code/a5_poisson_ceiling.py scratch results`, `python files/code/a6_weak_share.py DATASETS results/weak_share.json`
   - `python files/code/b1_prep_models.py DATASETS scratch/models` and
     `python files/code/b1b_weakshuf.py DATASETS scratch/models 1,2`
   - `python files/code/b2_run_panel.py files/code scratch/models scratch/runs full,thr5,thr5_resc,thin,thin_resc,weakshuf1,weakshuf2 100 10 sugar,water,bitter,salt_high,LB2c,aPhM1,TPMN1,JO_CE,JO_FV,JO_B`
     (and the same at 150 Hz for full,thr5,thin,thin_resc,thr5_resc,weakshuf1), about 1-2 h on 2 CPUs
   - `python files/code/b3_compare.py scratch/models scratch/runs 100 results/model_panel_100hz.csv`,
     `python files/code/b4_stats.py scratch/models scratch/runs 100 results/model_panel_100hz.csv results/model_100hz`
     (same for 150)
   - `python files/code/fig1_structure.py results figures`, `python files/code/fig2_model.py results figures`

## Files

- `files/results/reproduction_within_animal.csv`, `reproduction_within_mcns.csv`, `reproduction_cross_animal.csv`,
  `reproduction_detector_split.csv`: aggregate reproduction tables for each k bin (columns: n_pairs,
  p_reproduce with CI, p_matched_baseline, lift with CI, specific_frac_min with CI, mean_cB).
- `files/results/poisson_ceiling.csv`, `weak_share.json`.
- `files/results/model_panel_*hz.csv` (per stimulus side and variant), `model_*hz_stats.json`,
  `model_100hz_lost_neurons.csv` (model neuron index in the Shiu `Completeness_783.csv` order, rate, weak input
  share, lost flag).
- `files/code/` (all analysis code; `lifnb.py` and `stimuli.py` are from sci:sha256:3820a2c88d33), `files/figures/`,
  `files/fetch_inputs.sh`, `files/provenance.json`, `files/NOTICE-EXTERNAL-DATA.md`.

## References

- Shiu P.K. et al. 2024. A Drosophila computational brain model reveals sensorimotor processing. Nature 634:210. doi:10.1038/s41586-024-07763-9
- Dorkenwald S. et al. 2024. Neuronal wiring diagram of an adult brain. Nature 634:124. doi:10.1038/s41586-024-07558-y
- Schlegel P. et al. 2024. Whole-brain annotation and multi-connectome cell typing of Drosophila. Nature 634:139. doi:10.1038/s41586-024-07686-5
- Buhmann J. et al. 2021. Automatic detection of synaptic partners in a whole-brain Drosophila electron microscopy data set. Nat Methods 18:771. doi:10.1038/s41592-021-01183-7
- Berg S. et al. 2025. Sexual dimorphism in the complete connectome of the Drosophila male central nervous system. bioRxiv doi:10.1101/2025.10.09.680999
