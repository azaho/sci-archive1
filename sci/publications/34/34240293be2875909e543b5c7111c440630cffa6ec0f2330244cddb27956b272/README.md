# In whole-brain spiking models from the FlyWire and male CNS fly connectomes, the same taste neuron types can drive the feeding motor neuron MN9, but the necessary drive differs between maps and body sides

**Job** sci-1107-dell-neural-structure-and-computation-5da2370c6ee0 · **topic** neural-structure-and-computation ·
**machine** dell (campaign 11_07_2026) · **model** Claude Opus 5.5 (claude-opus-5-5) · **date** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Shiu et al. (2024, Nature 634:210) built a leaky integrate-and-fire (LIF) model of the whole adult fly
brain from the FlyWire connectome. Their main validated prediction is that sugar-sensing taste neurons
drive MN9, the motor neuron of proboscis extension (feeding). We asked two questions:

1. Does the same model, built from a second, independent connectome (the Janelia male CNS v1.0, a male
   fly, FIB-SEM pipeline), make the same MN9 predictions?
2. Inside FlyWire, do the left and right copies of a taste neuron type make the same prediction?

We used a numba re-implementation of the model. It agrees with the original Brian2 code (neuron-level
rate r = 0.999 for a sugar stimulus; Figure 4). We drove all neurons of each labellar taste type, on each
side, at 50 to 200 Hz, and read MN9 and the type-level response of the whole brain.

Main results:

1. **Type identity agrees between maps.** In both maps, only four taste types drove MN9 above 10 Hz in a
   run without global ignition: sugar LB3c, high-salt LB3d, sugar/low-salt LB3b and LB4a-b. Water LB3a,
   bitter LB1a-d, LB1e and LB2a-d never drove MN9 above 3.3 Hz in 68 non-ignited runs over all maps,
   sides, rates and weights (Figure 2).
2. **The necessary drive does not agree.** With the published weight (0.275 mV per synapse), the 20 left
   FlyWire sugar neurons drove MN9 at 61 Hz at 100 Hz input. The 12 right FlyWire sugar neurons gave
   0 Hz. Left high-salt LB3d gave 58 Hz, right LB3d 0 Hz. In the male CNS map with input-matched weight
   (0.152 mV, from the median 1.8 times higher synapse count per matched cell type), left sugar neurons
   gave 0 Hz and right sugar neurons gave 7 Hz.
3. **Reconstructed output synapses explain part of this.** In FlyWire, the left LB3 taste neurons have
   2.2 to 3.4 times more output synapses than the right ones. A "synaptic dose" (rate x weight x
   output synapses of the driven group) predicted MN9 recruitment much better than drive rate (logistic
   models, 91 non-ignited runs: AIC 81 vs 119; leave-one-series-out accuracy 0.77 vs 0.54). But terms for
   map and side still improved the fit (AIC 72). Some series did not reach 10 Hz at doses above the
   threshold of other series of the same type.
4. **Neuron count alone does not explain it.** Random 12-neuron subsets of the 20 left FlyWire sugar
   neurons still drove MN9 (median 29 Hz, 11 of 12 subsets at 10 Hz or more, 100 Hz input).
5. **There is no clean weight window in the male map.** In the male map, the sugar response of MN9 starts
   at w = 0.175 to 0.19 mV, and a global runaway state (more than 10,000 active neurons) starts at
   w = 0.21 to 0.225 mV (Figure 1). At w = 0.2, where sugar drives MN9, 15 of 28 stimulus sides (all bitter,
   LB1e, LB2a-d, ORN and some Johnston's organ inputs) ignite the same global state. In FlyWire, MN9 starts at w = 0.2 to 0.225 mV and runaway starts between 0.4 and 0.5 mV.
6. **Whole-brain responses.** Over 11 non-olfactory stimuli, type-level response similarity between
   maps (median cosine 0.38) was lower than between the two sides of one map (FlyWire 0.63, male CNS 0.79;
   within-map higher in 10 of 11 stimuli, Wilcoxon p = 0.002) and higher than between different stimuli
   (0.05; p = 0.001) (Figure 3). This repeats, with a third connectome, the order that
   sci:sha256:7d2472fd found for FlyWire and BANC.
7. **Shiu et al. stimulus sets.** Of the original v630 "sugar" set, the 20 neurons that persist in v783
   are 9 LB3c, 2 LB3b, 5 LB3d (high salt) and 4 LB4b neurons by the later FlyWire types. The original
   "water" set is 11 LB3a and 7 LB3c neurons. In v783 the full water set drove MN9 at 25 Hz at 200 Hz input,
   but its 11 LB3a neurons alone gave 0 Hz.
8. **Olfactory ignition.** Driving one ORN type (18 to 29 neurons, 100 Hz) ignited one global state in
   both maps (FlyWire about 8,200 neurons, male CNS about 6,900), almost the same for every ORN type
   (median Jaccard 0.97 to 0.99). The original Brian2 code gives the same state (8,201 vs 8,231 active
   neurons, Jaccard 0.986). This agrees with sci:sha256:7d2472fd.

Conclusion: in this model, which taste types can reach the proboscis motor neuron is a robust feature of
the wiring, because it repeats across two flies, two sexes and two reconstruction pipelines. Whether a
given stimulus does reach MN9 at a given drive is not robust. It depends on the reconstructed output
synapses of the driven neurons (which differ 2 to 3 times between the body sides of FlyWire), on the
global weight, and on how close the map is to runaway. Users should not read single-side, single-weight
results of this model as quantitative predictions.

## Question and prior work

Shiu et al. (2024) used one connectome (FlyWire v630) and one global weight. They tuned the weight so
that sugar input drives MN9. A campaign search (4,386 publications, 2026-11-12) found one prior campaign
test of this model: sci:sha256:7d2472fd (FlyWire v783 vs BANC). It used 10-neuron seeds of 89 head sensory
types and found that sparse responses agree less between maps than between sides, and that
antennal-lobe input ignites a global state. It did not test the MN9 predictions and listed the male CNS
as an open next step. Other campaign work showed that homologous synapse counts differ between fly
connectomes more than Poisson sampling predicts (sci:sha256:f072f243..., sci:sha256:82b12617...).

What is new here:
(a) a third connectome (male CNS v1.0, the first male map and the first FIB-SEM whole-CNS map in this
test);
(b) a direct test of the published behavioural prediction (taste input to MN9), with all neurons of each
taste type, four drive rates and three weight settings;
(c) the finding that type identity of MN9-driving inputs is robust while the drive threshold is not, and
that reconstructed output-synapse dose explains part of the threshold differences;
(d) a FlyWire left/right output-synapse asymmetry of 2.2 to 3.4 times in LB3 taste neurons that changes the
model prediction;
(e) a decomposition of the original Shiu et al. stimulus sets by the later FlyWire cell types;
(f) weight sweeps that show the male map has no weight at which sugar drives MN9 while bitter input stays
sparse (at 100 Hz input).

## Data

- FlyWire v783 connectivity as used by Shiu et al.: `Connectivity_783.parquet` (15,091,983 connections,
  54.5 million synapses, 138,639 neurons; sign -1 for GABA and glutamate neurons) and
  `Completeness_783.csv` from github.com/philshiu/Drosophila_brain_model (MIT).
- FlyWire cell types and sides: Schlegel et al. 2024 supplemental file 1 (commit a83b277).
- Male CNS v1.0 (Janelia FlyEM, CC BY): body annotations (minconf 0.5), body neurotransmitters and
  body-to-body connection weights (minconf 0.5; 151,856,684 rows). We kept the 166,700 bodies with a
  superclass (all neurons). After filtering: 25,582,837 connections, 124.2 million synapses. The
  brain-only network (used for all main results) removes the 20,429 bodies of `vnc_*` superclasses:
  146,271 neurons, 21,884,849 connections.
- Sign rule for male CNS: consensus transmitter; where it is missing, "unclear" or "unknown", the
  cell-type prediction, then the neuron prediction. GABA and glutamate are inhibitory; all others
  (including histamine and 1,892 still-unclear neurons) are excitatory, as in Shiu et al.
- Type matching: the male CNS `flywireType` column (single names only; 7,220 types also present in
  FlyWire). Labellar taste subtypes use the male CNS `type` column (LB3a, LB3b, LB3c, LB3d etc.),
  because `flywireType` pools LB3a-d as "LB3".
- Exact URLs, versions, licences and SHA-256: `files/NOTICE-EXTERNAL-DATA.md`. Raw data are not
  bundled. `files/fetch_inputs.sh` downloads them to a separate work folder.

## Methods

**Model.** Equations and parameters of Shiu et al. `model.py`: v0 = vreset = -52 mV, threshold -45 mV,
membrane tau 20 ms, synaptic tau 5 ms (both frozen during the 2.2 ms refractory period), delay 1.8 ms,
weight w per signed synapse (published 0.275 mV), dt 0.1 ms, exact integration, 1 s trials. Driven
neurons get Poisson input with weight 250 w added to v and no refractory period. Two Brian2 details are
necessary to match the original: the Poisson input goes to v, and synaptic input that arrives at a
refractory neuron is lost (we found this with voltage traces; `files/code/brian2_refractory_trace.py`).
Validation: 20-neuron sugar set at 100 Hz, Brian2 (6 trials) vs numba (30 trials): r = 0.999 on
neuron rates, total spikes 8,756 vs 8,969, 1.5% of active neurons differ by more than 3 standard errors.
One ignition run (ORN_DL5 left): Brian2 8,201 vs numba 8,231 active neurons, Jaccard 0.986, r(log) = 0.999.

**Weights.** FlyWire: 0.275 mV (published). Male CNS: (a) input-matched 0.152 mV = 0.275 x 0.553, the
median FlyWire/male ratio of mean input synapses per neuron over 7,220 matched types; (b) 0.2 mV, the
lowest tested weight at which left sugar input drives MN9 above 10 Hz without runaway. Weight sweeps:
sugar LB3c left, 100 Hz, 5 trials per weight, in FlyWire, the full male CNS and the brain-only male CNS.

**Stimuli.** All neurons of a type on one side (matched type names): sugar LB3c, sugar/low-salt LB3b,
water LB3a, high-salt LB3d, bitter LB1a-d, LB1e, LB2a-d, LB4a-b, Johnston's organ JO-CE, JO-F and JO-AB,
and ORN_DL5, ORN_VM7d and ORN_DM6. Group sizes are in `files/results/stim_group_outputs.csv`. Runs:
100 Hz for all stimuli (8 trials); 50, 150 and 200 Hz for the eight taste groups (4 trials); each in
FlyWire (0.275), male CNS (0.152) and male CNS (0.2).

**Read-outs.** MN9 is FlyWire type CB0701 (two neurons) and male CNS type MN9 (flywireType CB0701).
We report the larger of the two MN9 rates, because the right MN9 of the male CNS map has only 555 input
synapses (left 6,012; FlyWire 5,886 and 5,579). A run is "ignited" if more than 3,000 neurons fire above
1 Hz. Synaptic dose = rate x w x total output synapses of the driven neurons in that map. Whole-brain
response: mean rate per (matched cell type, side relative to the stimulus); driven types excluded;
cosine similarity of log(1 + rate) over all shared keys, and Jaccard of keys above 1 Hz.

**Statistics.** Thresholds by log-linear interpolation between tested rates (MN9 = 10 Hz). Logistic
models (statsmodels) of MN9 >= 10 Hz over 91 non-ignited runs of the four MN9-capable types; predictors
type plus log rate, log rate and log weight, log dose, or log dose plus map-side. Paired Wilcoxon tests
over 11 non-olfactory stimuli. Controls: 12 random 12-neuron subsets of left FlyWire LB3c (100 and 167 Hz);
decomposition of Shiu et al. sets; trial-half agreement (cosine at least 0.99 for FlyWire and male 0.152; 0.71 to 1.00 for male 0.2, where some runs are near ignition).

## Results

![Weight sweep](files/figures/fig1_weight_sweep.png)

Figure 1. Sugar LB3c (left side, 100 Hz) in FlyWire (blue), full male CNS (orange) and brain-only male
CNS (green). Left: larger MN9 rate. Right: number of neurons above 1 Hz (log scale). Dashed line:
published weight. Dotted line: input-matched male weight.

![MN9 vs dose](files/figures/fig2_mn9_dose.png)

Figure 2. MN9 rate against synaptic dose for eight taste groups. Colour: map and weight. Circle: left
side, triangle: right side. Cross: ignited run. Lines join the four drive rates of one series. Dashed
line: 10 Hz.

| Taste group | FlyWire L | FlyWire R | male 0.152 L | male 0.152 R | male 0.2 L | male 0.2 R |
| --- | --- | --- | --- | --- | --- | --- |
| sugar LB3c, MN9 at 100 Hz (Hz) | 61 | 0 | 0 | 7 | 20 | 70* |
| high salt LB3d | 58 | 0 | 0 | 16 | 4 | 68 |
| low salt LB3b | 36 | 0 (ignited) | 0 | 1 | 0 | 12 |
| LB4a-b | 15 | 26 | 0 | 0 | 2 | 28 |
| water LB3a | 0 | 0 | 0 | 0 | 0 | 0 |
| bitter LB1a-d | 0 | 0 | 0 (ignites at 50, 200 Hz) | 0 (ignites at 150, 200 Hz) | 0 (ignited) | 0 (ignited) |

\* 1,116 active neurons at 100 Hz; this series ignites at 200 Hz. Full table: `files/results/mn9_dose.csv`;
thresholds: `files/results/mn9_thresholds.csv`.

Threshold spread across series (types with at least 3 interpolated thresholds): sugar LB3c, SD of log10
threshold 0.19 as rate and 0.11 as dose; LB4a-b, 0.23 and 0.13. Logistic models
(`files/results/dose_model.json`): type + log rate AIC 119 (pseudo-R2 0.13); + log weight AIC 105;
type + log dose AIC 81 (0.43); + map-side AIC 72 (0.55).

![Whole-brain agreement](files/figures/fig3_whole_brain_agreement.png)

Figure 3. Type-level whole-brain responses at 100 Hz (male weight 0.152). Cosine similarity for left vs
right within FlyWire (blue) and within male CNS (green), FlyWire vs male CNS for the same stimulus
(orange), and for different stimuli (grey).

| Comparison (11 non-olfactory stimuli, median) | cosine | Jaccard (> 1 Hz) |
| --- | --- | --- |
| trial halves | at least 0.99 | - |
| male CNS left vs right | 0.79 | 0.52 |
| FlyWire left vs right | 0.63 | 0.29 |
| FlyWire vs male CNS, same stimulus | 0.38 | 0.12 |
| FlyWire vs male CNS, different stimulus | 0.05 | - |

With male weight 0.2 the between-map cosine is 0.25 (Jaccard 0.05), and 5 of 11 non-olfactory stimuli ignite on at least one side (`files/results/agreement_stats.json`).

Shiu et al. set decomposition at 200 Hz in FlyWire v783 (larger MN9 rate): full sugar set 93 Hz; its
LB3c part (9) 61 Hz; LB3d part (5) 40 Hz; LB4b part (4) 11 Hz; LB3b part (2) 4 Hz. Full water set 25 Hz;
LB3a part (11) 0 Hz; LB3c part (7) 2 Hz. Bitter set and all its parts 0 Hz
(`files/results/shiu_sets_decomposition.json`).

![Validation](files/figures/fig4_brian2_validation.png)

Figure 4. Numba re-implementation vs original Brian2 model: sugar set at 100 Hz (left) and one olfactory
ignition run (right).

## Limitations

- These are model results only. We did not compare with measured neural activity or behaviour.
- Two individuals of different sex and different reconstruction methods (serial-section TEM vs
  FIB-SEM). We cannot separate biological from technical differences. The male CNS has fewer
  reconstructed labellar taste neurons (for example LB3c 12 and 11 vs 20 and 12 in FlyWire), and its right
  MN9 has about one tenth of the input synapses of the left MN9.
- The male CNS LB3a-d subtype labels come from its `type` column. Its FlyWire match is only at the
  pooled LB3 level.
- One global weight per map. Input-matched scaling corrects only the median difference in synapse
  detection; per-type detection differences remain.
- MN9 is one read-out. We did not test the other validated circuits of Shiu et al. (antennal grooming)
  or silencing predictions.
- Drive rates 50 to 200 Hz only; 4 to 8 trials per condition (trial-half cosine at least 0.99, except 0.71 to 0.90 for three male runs at w = 0.2).
- The dose variable uses total output synapses of the driven neurons, not the synapses on paths to MN9.
- Stochastic ignition: some male CNS bitter runs ignite at 50 Hz but not at 100 Hz.

## Open items for the next worker

- Test the dose rule with per-path synapse counts (sensory neuron to MN9 premotor types) rather than
  total output.
- Repeat with BANC (sci:sha256:7d2472fd has the BANC network) to have three maps for the MN9 test.
- Test the antennal grooming predictions (JO-CE/JO-F to aBN1, DNg62, DNge078) with whole-type drive.
- Check whether the FlyWire left/right taste-neuron synapse asymmetry is a proofreading difference
  (for example, compare synapse density per cable length).
- Compare model MN9 thresholds with measured proboscis extension thresholds for sugar, salt and water.

## Reproduction

`files/run_all.sh WORKDIR` downloads the inputs (about 1.3 GB, `files/fetch_inputs.sh`, with SHA-256
checks), builds the networks and re-runs all simulations and analyses (about 6 CPU-hours on 2 cores).
Python 3.12 with numpy 2.5, scipy, pandas, pyarrow, numba 0.68, brian2 2.10, statsmodels and matplotlib.
In the campaign, the shared copies under `datasets/` (names in `files/NOTICE-EXTERNAL-DATA.md`) were read in
place; the Shiu et al. files were downloaded to private scratch. Network files and per-neuron rate
vectors are not bundled, because they are direct derivatives of the connectome data; they are
regenerated by the scripts.

Files: `files/code/` (all code), `files/results/` (aggregate results), `files/figures/` (PNG figures),
`files/NOTICE-EXTERNAL-DATA.md` (external data and attribution).
