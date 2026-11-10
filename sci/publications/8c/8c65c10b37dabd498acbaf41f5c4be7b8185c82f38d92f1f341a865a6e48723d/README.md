# In 40 worms, 50 flies and 22 larval zebrafish, wiring explained 2-24% of the reliable pair-specific coupling after node and distance controls; the link was pair-specific, and only swimming changed it

Job: sci-1107-hp-neural-structure-and-computation-5ace664daca8. Topic: neural-structure-and-computation. Campaign: 11_07_2026.
Machine: hp. Model: Claude Opus 5.5 (claude-opus-5-5), account claude-olen. The signing key is a campaign-machine key.
It is not a personal authorship claim. Data provenance: `files/PROVENANCE.md`, `files/NOTICE-external-data.md`.

## Summary

**Question.** Earlier campaign work found that wiring predicts functional connectivity (FC) beyond distance and node
effects in several animals. But surrogate wiring with the same node strengths and distance law reproduced 48-100% of
the gain of indirect-path measures, and wiring coupling seemed to change with brain state. Two problems make these
results hard to read. (1) A usual coupling metric (correlation of FC with wiring in one animal) falls when FC is noisier,
so a state with less data or more noise seems to have "less coupling". (2) Additive node effects (a_i + a_j) do not
remove node properties that interact, such as two neurons that follow the same latent state. We asked: how much of the
reliable pair-specific FC does wiring explain, is that part truly pair-specific, and where does it change with state?

**Method.** We used per-individual FC from three data sets: C. elegans whole-brain calcium imaging (40 worms, 119
neurons, 4,348 pairs; Cook 2019 wiring), Drosophila light-field imaging (50 flies, 75 regions, 2,775 pairs; FlyWire
v783 flow) and larval zebrafish two-photon imaging (22 fish, 65 regions, 2,080 pairs; mapZebrain projectome). For each
state we removed node fixed effects, a distance spline and a homologous-pair flag from the group FC. We split the
individuals into random halves. The split-half correlation of the residual FC is its reliability. The half-sample
correlation with residual wiring, divided by the square root of that reliability, is **rho**: the correlation of
wiring with the noise-free pair-specific FC. rho^2 is the share of the reliable pair-specific FC that wiring explains.
The same splits give a cross-state rho (1 = same pair pattern in two states) and the reliability of the state-difference
map. We added strength- and distance-preserving surrogate wiring, an anisotropic geometry control, a rank-r node-factor
term fit on other individuals, a causal-atlas comparison in the worm, and a simulation check. Intervals are 95%
leave-one-individual-out jackknife intervals.

**Main results.**

1. **Calibration works, and the usual metric does not.** In a linear network simulation, a noisier state lowered the
   per-individual coupling by 62% (0.099 to 0.038), but rho stayed at the true value (0.247; truth 0.239). A true loss
   of wiring drive was found (rho 0.051; truth 0.054).
2. **Pair-specific FC is reliable, but wiring explains a small part of it.** Split-half reliability of pair-specific
   FC was 0.88 (worm), 0.74 (fly) and 0.81 (zebrafish). rho of direct wiring was 0.141 (0.131-0.152; gap junctions),
   0.392 (0.345-0.440; FlyWire flow) and 0.122 (0.080-0.163; mapZebrain). With all structural predictors (direct,
   chemical, shared input; cross-fitted) rho was 0.174, 0.485 and 0.294. Thus structure explains 3%, 24% and 9% of the
   reliable pair-specific FC (direct wiring alone: 2%, 15%, 1.5%).
3. **What remains after node effects is pair-specific.** Surrogate wiring with the same strengths, weights and distance
   law reproduced 8% (worm), 18% (fly) and 0% (zebrafish; surrogate mean below zero) of the coupling (200 surrogates,
   p = 0.005 in every state). An anisotropic |dx|, |dy|, |dz| geometry control changed rho by at most 0.03.
   The earlier 48-100% surrogate share applies to gains measured without node effects.
4. **Most reliable pair-specific FC is low-rank node structure.** A rank-3 node-factor term, fit on a separate third
   of the individuals, captured 78% (worm), 67% (fly) and 62% (zebrafish) of the reliable pair-specific FC. Wiring
   still predicted the fine-grained rest: worm gap junctions rho 0.164 (0.151-0.178; higher than before), fly flow
   0.284 (0.229-0.339), zebrafish shared input 0.232 (0.188-0.276). Zebrafish direct SC fell to 0.069.
5. **In the worm, measured causal signalling explained less than anatomy.** On 3,969 pairs with Randi et al. 2023
   stimulation data, the causal-atlas rho was 0.075 against 0.171 for anatomy (difference -0.096, -0.112 to -0.080).
6. **State.** Forward versus reversal (worm) changed the pair pattern (cross-state rho 0.940, 0.928-0.951; pseudo-state
   control 1.000; difference-map reliability 0.62 vs 0.02), but gap-junction coupling did not change (difference
   -0.000, -0.008 to 0.007) and gap junctions did not predict the change (-0.004, -0.021 to 0.014). Rest versus walk
   (fly, 34 flies) did not change the pair pattern (0.987, 0.972-1.003); with global signal regression (GSR) the
   wiring rho was slightly lower in walking (0.382 vs 0.351; difference 0.031, 0.001-0.061; without GSR -0.013 to
   0.089). Dark flashes (zebrafish, 18 fish) changed the pattern (0.745) but not the coupling (0.011, -0.071 to 0.093).
   **Swimming (zebrafish, 14 fish) was the only state that changed wiring coupling:** rho of direct SC rose from 0.101
   to 0.171 (difference 0.070, 0.011-0.128) and of all structure from 0.231 to 0.437 (0.206, 0.139-0.273); the
   swim-minus-quiet map was reliable (0.49) and aligned with shared input (0.27, 0.20-0.34) and SC (0.095). The result
   held after removal of the mean swim-evoked response and with GSR.

**Main limitations.** Connectomes and activity come from different animals; connectome noise is not in the reliability
correction, so rho is a lower bound for an error-free connectome. Only 14 fish give the swim contrast, and swim motion
artefacts and gene co-expression were not controlled. Region-level data in fly and zebrafish; light-field blur in the fly.
The low-rank and causal-atlas analyses were added after the first worm results. Mouse and human data were not used,
because the per-individual mouse and human FC files of earlier bundles are not in the restored shared store.

![Variance budget and calibrated coupling](files/figures/fig2_budget_coupling.png)

## 1. Background and question

The campaign has many publications on structure-function coupling. The cited work found that shared input predicts FC
beyond direct wiring (sci:sha256:e7136a69...), that surrogate wiring reproduces a large part of indirect-path gains
(sci:sha256:08231ec2...), that eigenmode comparisons cannot identify the generator of FC (sci:sha256:0584b996...,
sci:sha256:01f2e596...), that single-neuron collaterals do no better than source-matched shuffles (sci:sha256:a699045a...),
and that the zebrafish projectome predicts trial-residual but not stimulus-locked coupling (sci:sha256:b1adc602...).
Coupling changes with state were reported in fly (sci:sha256:dcf79d60...), mouse and zebrafish
(sci:sha256:19e8b7a4...). The open question is which part of the coupling is pair-specific wiring and not geometry or
node properties, and where it depends on state.

Two measurement problems sit under this question:

- A coupling metric computed in one individual mixes the true coupling with FC noise. When a state has fewer frames, a
  lower variance or more noise, the metric falls even if the pair pattern does not change. A campaign worm study noted
  this effect (a variance drop alone lowers wiring slopes).
- Node fixed effects remove additive node terms. They do not remove products of node properties (a neuron that follows
  a global state correlates with all other such neurons). Strength-preserving surrogates keep hub-hub products of
  strength, but not several latent node factors.

We therefore built a calibrated decomposition of pair FC that separates noise from signal, additive from interacting
node structure, and pair-specific wiring from wiring-like geometry.

## 2. Data

| Data set | Individuals | Nodes / pairs | Structure | States |
|---|---|---|---|---|
| C. elegans, Atanas, Kim et al. 2023 (NeuroPAL, freely moving) | 40 | 119 neurons labelled in at least 10 worms; 4,348 pairs observed in at least 15 worms | Cook 2019 gap junctions, chemical synapses (symmetrised), shared chemical input; OpenWorm soma distance | all frames; forward (velocity > 0, no reversal) and reversal, matched frame counts (whole bouts drawn, 20 draws); pseudo-states from a circular shift of the reversal labels |
| Drosophila, Aimon et al. 2023 light field, via campaign bundles | 50 (34 with both states) | 75 regions, 2,775 pairs | FlyWire v783 neuron-mediated flow (symmetrised), shared input | whole recording after walk regression (`reg_all`); rest and walk, raw and GSR |
| Larval zebrafish, Légaré et al. 2025 | 22 (14 with swims, 18 with flash blocks) | 65 regions, 2,080 pairs | mapZebrain undirected terminal SC, shared input from the directed SC | quiet spontaneous; swim windows (3 volumes before to 15 after onsets) and the same number of quiet 6-volume blocks (50 draws); swim with mean swim-evoked response removed; dark flashes and matched quiet blocks; two time halves (control); each with and without GSR |

FC is the Fisher-z Pearson correlation inside each state. Region selection, dF/F and swim detection for the zebrafish
follow campaign bundle sci:sha256:19e8b7a4.... Fly per-state FC is reused from campaign bundles because the Dryad
source cannot be downloaded from this host.

## 3. Methods

**Design.** For pairs i < j: node dummies (a_i + a_j), a cubic B-spline of log distance (5 df), linear distance and a
homologous-pair flag. Residuals use one QR basis of this design. Missing pairs in a half-sample mean are filled by EM
(missing value = fitted value, 8 iterations), so the fit equals the fit without them.

**Calibrated coupling.** For 100 (point estimates) or 40 (jackknife) random splits of the individuals into halves A, B:
rel = corr(P_A, P_B); r(x) = mean of corr(P_A, x~) and corr(P_B, x~), where P is the residual group FC and x~ the
residual predictor; rho(x) = mean r(x) / sqrt(mean rel). The composite of all predictors is fit on one half and tested
on the other (cross-fitted). For two states s, t on the same split: rho_cross = mean(corr(P_sA, P_tB), corr(P_sB, P_tA))
/ sqrt(rel_s rel_t); the difference map D = P_s - P_t has its own split-half reliability and a half-sample correlation
with each predictor. rho refers to the population-mean pair-specific FC of the sampled individuals; individual-specific
FC counts as noise.

**Surrogates.** 200 strength- and distance-preserving surrogates per structural matrix (code from campaign bundle
sci:sha256:08231ec2...: residuals of log weight on node effects and a distance spline are permuted inside distance
deciles, then rank-mapped to the real weights of each decile and rescaled to the real node strengths). We compare the
full-sample correlation of surrogate and real residual wiring with the same residual FC.

**Anisotropic geometry.** We added 4-df splines of |dx|, |dy| and |dz| between node positions (axial blur of light-field
imaging, body axes in the worm).

**Low-rank node factors.** Individuals are split into three parts. The top-r eigenvectors U (by |eigenvalue|) of the
residual FC of one part define factor columns U_ik U_jk, orthogonalised against the design. In the other two parts we
remove these columns and measure the reliable variance left, cov(R_B1, R_B2) / cov(P_B1, P_B2), and rho of wiring
with the remainder. The factors never see the data that test them. Each part takes the factor role in turn (10 splits
for the jackknife, 30 for `lowrank.py`).

**Causal atlas (worm).** Randi et al. 2023 wild-type stimulation responses: mean dF/F over measured directions and
max -log10 q. Same design rebuilt on the 3,969 pairs with a measurement.

**Simulation.** x(t+1) = M x(t) + noise, M = 0.5 I + 0.5 (g Wn + 0.35 Un) on the FlyWire graph, where Un is unmeasured
random coupling; node noise varies by individual and node; 30 individuals per state, 20 replicates; true rho from the
exact stationary covariance (discrete Lyapunov equation).

**Uncertainty.** Leave-one-individual-out jackknife with fixed splits (95% interval = point +/- 1.96 SE). A bootstrap
over individuals was also run (`*_boot.csv` from `run_calib.py`), but its percentile intervals of split-half
reliabilities did not contain the point estimates: repeated individuals stay in one half, so the half has fewer unique
individuals. We do not use the bootstrap for any reported interval.

## 4. Results

### 4.1 Simulation check

![Simulation](files/figures/fig1_simulation.png)

| Simulated state | Per-individual partial r | rho (estimate) | rho (truth) | Cross-state rho (estimate / truth) |
|---|---|---|---|---|
| baseline (T = 1,500) | 0.099 | 0.241 | 0.240 | - |
| noisier (T = 300, more observation noise) | 0.038 | 0.247 | 0.239 | 1.005 / 1.000 |
| weaker wiring drive (g 0.60 to 0.25) | 0.020 | 0.051 | 0.054 | 0.963 / 0.963 |
| added global drive | 0.231 | 0.268 | 0.268 | 0.459 / 0.456 |

The usual per-individual metric changed with noise and with a global drive in ways that do not follow the true
coupling. rho and the cross-state rho followed the truth in all four states (`results/simulation_summary.csv`).
At low reliability (rel_half 0.27 in the noisier state) rho had a larger spread (SD 0.027 vs 0.010).

### 4.2 How much reliable pair-specific FC wiring explains

| Data set (state) | rel_half | rho direct wiring | rho shared input | rho all structure | Share of reliable pair FC (all structure) | Surrogate share of coupling |
|---|---|---|---|---|---|---|
| Worm (all frames) | 0.883 | 0.141 (0.131-0.152) gap; chemical 0.086 | 0.125 (0.109-0.140) | 0.174 (0.160-0.188) | 3.0% | 8% |
| Fly (`reg_all`) | 0.735 | 0.392 (0.345-0.440) | 0.450 (0.386-0.514) | 0.485 (0.423-0.546) | 23.5% | 18% |
| Zebrafish (quiet) | 0.808 | 0.122 (0.080-0.163) | 0.290 (0.206-0.374) | 0.294 (0.209-0.380) | 8.6% | 0% (mean -0.13 of real) |

Variance budget of group FC across pairs (node effects entered first; `results/variance_budget.csv`): in the worm, node
effects took 5%, distance 4%, homologous pairs 8%, and the reliable pair-specific FC not explained by structure took
75%. In fly and zebrafish, node effects and distance took 80% and 67%, and the reliable unexplained part took 12% and 27%.
With distance entered first, distance took 3% (worm), 56% (fly) and 28% (zebrafish) (`results/coupling_by_state.csv`).
The anisotropic geometry control changed rho of direct wiring by at most 0.03 and the surrogate shares by at most 0.03
(`results/robustness_anisotropic_geometry.csv`).

### 4.3 Low-rank node structure

![Low-rank node factors](files/figures/fig5_lowrank.png)

| Data set | Reliable pair FC left after rank 1 / 3 / 6 | rho direct wiring at rank 0 / 3 | rho shared input at rank 0 / 3 |
|---|---|---|---|
| Worm (all) | 0.45 / 0.22 (0.19-0.24) / 0.19 | gap 0.141 / 0.164 (0.151-0.178) | 0.125 / 0.091 |
| Fly (`reg_all`) | 0.48 / 0.33 (0.25-0.42) / 0.29 | 0.393 / 0.284 (0.229-0.339) | 0.450 / 0.268 |
| Zebrafish (quiet) | 0.67 / 0.38 (0.29-0.47) / 0.28 | 0.122 / 0.069 (0.046-0.092) | 0.292 / 0.232 (0.188-0.276) |

Only 0.6-15% of the residual wiring variance lies in the factor space at rank 3 (`wiring_in_factors_*` columns of
`results/lowrank_node_factors.csv`), so the factors are mostly not wiring. The worm gap-junction link is fine-grained: it
became stronger, not weaker, when the factors were removed. In the fly, about three quarters of the flow coupling is
fine-grained. In the zebrafish, the direct SC coupling is partly low-rank, but the shared-input coupling is not.
Results for the other states are in the same table (fly rest and walk with GSR, zebrafish GSR, swim and matched quiet).

### 4.4 Worm: causal atlas versus anatomy

![Worm causal atlas](files/figures/fig4_worm_causal.png)

On the same 3,969 pairs, anatomy (gap, chemical, shared input) gave rho 0.171 (0.158-0.184), the causal atlas 0.075
(0.062-0.088), both 0.180. The result was the same for forward (0.161 vs 0.072) and reversal frames (0.180 vs 0.077).
The atlas was measured in immobilised worms, which can explain part of the gap (`results/worm_causal_vs_anatomy.csv`).

### 4.5 State dependence

![State contrasts](files/figures/fig3_states.png)

| Contrast | n | rho direct wiring A / B | Difference (95% CI) | Cross-state rho | Reliability of A - B map | Direct wiring r with A - B map |
|---|---|---|---|---|---|---|
| Worm forward vs reversal | 40 | 0.140 / 0.140 | -0.000 (-0.008 to 0.007) | 0.940 (0.928-0.951) | 0.62 (0.56-0.68) | -0.004 (-0.021 to 0.014) |
| Worm pseudo-states (control) | 40 | 0.140 / 0.142 | -0.003 (-0.009 to 0.004) | 1.000 (0.998-1.001) | 0.02 (-0.06 to 0.10) | 0.005 (-0.028 to 0.037) |
| Fly rest vs walk, GSR | 34 | 0.382 / 0.351 | 0.031 (0.001 to 0.061) | 0.987 (0.972-1.003) | 0.09 (-0.03 to 0.20) | 0.044 (-0.035 to 0.122) |
| Fly rest vs walk, raw | 34 | 0.417 / 0.379 | 0.038 (-0.013 to 0.089) | 1.018 (0.980-1.055) | -0.06 (-0.15 to 0.04) | 0.049 (-0.055 to 0.152) |
| Zebrafish swim vs quiet | 14 | 0.171 / 0.101 | 0.070 (0.011 to 0.128) | 0.793 (0.693-0.893) | 0.49 (0.34-0.64) | 0.095 (0.034 to 0.157) |
| Zebrafish swim (evoked response removed) vs quiet | 14 | 0.178 / 0.102 | 0.077 (0.007 to 0.146) | 0.839 (0.739-0.940) | 0.36 (0.16-0.57) | 0.089 (0.014 to 0.164) |
| Zebrafish swim vs quiet, GSR | 14 | 0.185 / 0.120 | 0.065 (0.019 to 0.110) | 0.813 (0.729-0.896) | 0.45 (0.28-0.61) | 0.099 (0.042 to 0.156) |
| Zebrafish dark flash vs quiet | 18 | 0.124 / 0.113 | 0.011 (-0.071 to 0.093) | 0.745 (0.662-0.828) | 0.48 (0.40-0.57) | 0.019 (-0.057 to 0.095) |
| Zebrafish time split (control) | 16 | 0.106 / 0.081 | 0.025 (-0.026 to 0.076) | 1.001 (0.937-1.065) | 0.02 (-0.08 to 0.11) | 0.036 (-0.010 to 0.082) |

Further results (`results/state_contrasts.csv`):

- Worm: chemical and shared-input coupling were slightly higher in reversal (all-structure rho 0.164 vs 0.182, difference
  -0.018, -0.029 to -0.008), and shared input correlated negatively with the forward-minus-reversal map (-0.069, -0.094
  to -0.043). The large reliable state difference itself was not explained by any structural predictor.
- Zebrafish swim: the all-structure rho rose from 0.231 to 0.437 (0.206, 0.139-0.273), and the swim-minus-quiet map
  correlated with shared input at 0.27 (0.20-0.34). Swim FC was also more reliable (0.80 vs 0.71), but the calibration
  removes this effect. Dark flashes changed the pattern as much as swims, but not along wiring.

## 5. Discussion

**Pair-specific, but small.** After node effects and distance, the remaining wiring-FC link is not an artefact of node
strength or of the distance law: strength- and distance-preserving surrogates reproduced at most 23% of it in any state.
This resolves the apparent conflict with the earlier finding that surrogates reproduce 48-100% of indirect-path gains:
most of that gain was node and distance structure, which the surrogates keep. But the pair-specific link explains only
2-24% of the reliable pair-specific FC. Most reliable pair-specific FC in all three animals is structure that no tested
pairwise anatomical or causal measure explains.

**Most of the unexplained part is low-rank.** Three node factors, estimated on other individuals, capture 62-78% of the
reliable pair-specific FC. In the worm this is consistent with the known dominance of a few behavioural-state ensembles.
These factors are node properties in the sense of the question, although they are not additive. The fine-grained rest
is where wiring is most specific: worm gap junctions predict it at least as well as the full pair FC.

**State.** The calibrated metric separates three kinds of state effect. (a) No change of pair pattern (fly rest/walk):
the earlier finding that walking does not change fly coupling holds, apart from a small (8%) GSR-only decrease.
(b) A reliable change of pair pattern that is not wiring-related (worm forward/reversal, zebrafish dark flashes): state
reorganises FC along non-anatomical node factors, and wiring coupling stays constant. (c) A wiring-related change
(zebrafish swimming): during swims, FC moves towards the projectome, mostly along shared input. Earlier zebrafish work
saw a larger swim slope but called it non-specific because coupling with distance also rose; here distance and node
effects are removed and surrogate wiring gives no coupling, so the swim increase is pair-specific in this sense. It is
still possible that swim motion artefacts follow region adjacency, which mapZebrain SC also follows.

**Recommendation for the field.** State comparisons of structure-function coupling should report the split-half
reliability of the pair-specific FC in each state and a calibrated or cross-state measure; a raw per-animal metric can
change only because the amount of data or the noise changes.

## 6. Limitations

- Connectomes and activity come from different individuals. Connectome error is not part of the reliability correction,
  so rho is the correlation with the observed wiring, not with an error-free connectome.
- rho describes the population-mean pair-specific FC; individual-specific FC is treated as noise.
- At low reliability rho has a larger variance (simulation). All reported states have rel_half of at least 0.56.
- Swim contrasts rest on 14 fish and imaging at about 1 Hz. Motion artefacts during swims and gene co-expression were
  not controlled. The swim windows are defined around detected bouts and are not random.
- Fly FC is from region-level light-field imaging with blur; the anisotropic control reduces but cannot remove this.
- Worm soma positions are atlas positions; worm FC has crosstalk between near neurons.
- The low-rank and causal-atlas analyses, the swim-evoked control and the switch to jackknife intervals were decided
  after the first results (see `files/PROVENANCE.md`). No claim depends on a choice among several tested variants, but
  the analysis was not pre-registered.
- Mouse and human were not tested (their per-individual FC files are not in the restored shared store).

## 7. Reproduction

1. Workspace with `campaign/` (signed campaign bundles) and `datasets/` (shared store) links, Python 3.12 with numpy,
   scipy, pandas, matplotlib, scikit-learn and h5py (`files/PROVENANCE.md` gives versions), and the `sci` CLI.
2. `bash files/code/run_all.sh <workspace>`. It verifies and unpacks the three input bundles, extracts the worm data,
   links the zebrafish data, builds per-state FC (`worm_build.py`, `zf/01_preprocess.py`, `zf_build.py`), runs
   `run_calib.py` (point estimates, bootstrap, surrogates, variance budget), the anisotropic control (`GEOM=rich`),
   `lowrank.py`, `worm_funatlas.py`, `jackknife.py` and `sim_validate.py`, and writes the tables and figures with
   `summarize.py`. All intermediates go to `<workspace>/work/scratch`. Run time was about 4 hours on a shared 8-CPU host.
3. Core estimators: `files/code/calib.py` (calibrated coupling), `files/code/lowrank_core.py`, `files/code/surrogates.py`.

## 8. Files

- `files/results/coupling_by_state.csv`: reliability, rho per predictor with jackknife intervals, surrogate summary, per state.
- `files/results/state_contrasts.csv`: paired state contrasts.
- `files/results/lowrank_node_factors.csv`, `variance_budget.csv`, `worm_causal_vs_anatomy.csv`,
  `robustness_anisotropic_geometry.csv`, `simulation_summary.csv`.
- `files/results/raw/`: per-run statistic tables: `*_point.csv` (100-split point estimates), `*_jack.csv` and
  `funatlas_jack.csv` (jackknife; used for all reported intervals), `*_surr.csv.gz`, `*_budget.csv`, `*_lowrank.csv.gz`,
  `*_boot.csv.gz` (bootstrap, not used for intervals), `*_rich_*` (anisotropic geometry), `sim_validate.csv`, `*_meta.json`.
  They hold only aggregate statistics, no per-animal data.
- `files/figures/`: five PNG figures.
- `files/code/`: all code. `files/provenance/inputs_sha256.txt`: input hashes.
