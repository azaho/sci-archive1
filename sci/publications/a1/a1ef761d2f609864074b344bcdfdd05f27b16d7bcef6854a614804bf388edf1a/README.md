# In 40 off-food moving C. elegans, neuron classes at higher connectome trophic levels had shorter activity timescales; in 8 on-food animals there was no relation

## Summary

**Question.** In primate and rodent cortex, areas higher in the anatomical hierarchy have longer intrinsic activity timescales (Murray et al. 2014). Does a similar rule apply to identified neurons in a complete connectome? We tested whether the position of a *C. elegans* neuron class in the chemical-synapse hierarchy (trophic level) predicts the timescale of its spontaneous whole-brain GCaMP activity. We also tested whether the relation is the same in two behavioural conditions.

**Approach.** We used NeuroPAL-identified whole-brain recordings from two public data sets: Atanas et al. 2023 (40 animals off food, freely moving, 3,548 identified neurons) and Dag et al. 2023 (8 animals on food with little movement, 814 identified neurons). For each neuron we calculated the autocorrelation of its trace inside each recorded segment. We fitted an exponential decay to lags 0.6–30 s (lag 0 excluded) to get the timescale tau. For each class we took the median log tau over all identified neurons. The structural measure was the trophic level of MacKay et al. (2020) in the Cook et al. 2019 hermaphrodite chemical connectome (neurons and muscles). Sensory neurons have low levels and motor neurons have high levels. The primary test was a Spearman correlation across non-pharyngeal classes (classes seen in ≥ 5 Atanas animals or ≥ 3 Dag animals).

**Main results.**

1. **Off food, moving (Atanas 2023): higher trophic level gave shorter timescales, which is the opposite of the cortical rule.** Spearman ρ = −0.31 (58 classes, p = 0.019, 95% class-bootstrap CI −0.52 to −0.07). The sign was the same in 36 of 40 individual animals (median per-animal ρ = −0.19, sign test p = 2 × 10⁻⁷). The relation remained with these changes: 800-frame windows (ρ = −0.27), recordings without heat stimulus only (ρ = −0.30), the 1/e decay time (ρ = −0.27), the autocorrelation at 10 s (ρ = −0.29), gap junctions in the trophic calculation (ρ = −0.30) and the independent Witvliet 2021 adult-8 nerve-ring connectome (ρ = −0.34). It also remained after control for degree, cell type, number of animals and label confidence (partial ρ = −0.41, permutation p = 0.001), and in interneurons only (ρ = −0.47, 29 classes, p = 0.010).
2. **On food, with little movement (Dag 2023): no relation.** ρ = +0.09 (54 classes, p = 0.54, CI −0.20 to +0.36). Only 4 of 8 animals had a negative sign. The other autocorrelation measures and connectome variants had |ρ| ≤ 0.20 and p ≥ 0.14. The first half of the frames alone gave a positive value (ρ = +0.36, p = 0.007), and the second half gave ρ = +0.23 (p = 0.09).
3. **Most classes were slower on food, and the slowing increased with trophic level.** With 800-frame windows in both data sets, tau was longer on food in 46 of 53 classes (median ratio 1.84). The log ratio increased with trophic level (ρ = +0.30, p = 0.027, CI +0.04 to +0.52; partial ρ = +0.29 after degree and cell type, permutation p = 0.035). Examples: AVA 7.4 s → 30.2 s, RID 3.9 s → 12.4 s, RMD 6.7 s → 15.5 s. Classes AIZ and ADA (mid level) were slightly faster on food. We designed this comparison after we saw results 1 and 2, so it is exploratory.
4. **Each neuron's synapse counts give most of the off-food relation.** Strength-preserving rewired connectomes (1,000 networks, each node keeps its chemical in, chemical out and gap-junction synapse counts) gave a mean ρ of −0.25 (95% range −0.28 to −0.23). This is 82% of the real value of −0.31. When only neuron–neuron contacts were rewired and all muscle synapses were kept, the null mean was −0.32, which is equal to the real value. Thus the trophic level here mainly measures the input-to-output synapse balance of each neuron (input–output balance alone: ρ = −0.26, p = 0.053). On food, the real value (+0.09) was above all 1,000 rewired values (null mean −0.16). But this gap (0.24) is smaller than the sampling CI of the real value, so it is weak evidence for wiring-specific structure.
5. **Behaviour coupling carries a large part of the off-food relation.** Higher-level classes had more trace variance explained by behaviour (ρ = +0.61 between trophic level and in-sample behaviour R², off food). After we removed the behaviour fit from each trace, the residual-timescale relation was ρ = −0.14 (p = 0.29). After control for class behaviour R², partial ρ was −0.13 (p = 0.32). On food, the residual relation was positive (ρ = +0.41, p = 0.002) but it did not remain after full controls (partial ρ = +0.02, p = 0.90).
6. **Class timescales were reliable inside a condition but only partly kept across conditions.** Split-half animal reliability of class log tau was ρ = 0.80 (Atanas) and 0.43 (Dag). The class order agreed between the two data sets with only ρ = 0.46 (53 classes).

**Interpretation.** The worm data do not support a fixed "hierarchy of timescales" in which downstream neurons integrate over longer times. In freely moving worms, classes near the motor end (AVA, AVB, AVE, RIB, RID, SMD) follow locomotor events and have short autocorrelation times. Upstream sensory and first-layer interneurons (AIN, AWA, ADA, AIZ) change more slowly. When the animal is on food and moves little, the motor-end classes become slow, and the relation is gone. Connectome position thus predicts which neurons change their timescale with behavioural state, more than it predicts a fixed timescale.

**Main limitations.** The two conditions are also two data sets with different recording dates and animal numbers (40 against 8). Thus food, locomotion and batch effects are confounded. The results are across-class correlations (53–58 classes), not causal tests. Timescales come from nuclear GCaMP at 0.6 s frames and include indicator kinetics. A single exponential is a poor description for oscillating or step-like traces. The low-frequency power fraction (< 0.05 Hz) did not show the same negative relation (ρ = +0.13 off food, p = 0.32), so the result applies to autocorrelation decay at lags ≤ 30 s, not to all slow variance. We did many secondary tests and did not correct them for multiple comparisons.

## Data

All inputs are campaign shared datasets. We did not download new data. `files/provenance/data_sources.csv` gives the shared path, source URL, file name, byte count and SHA-256 of each file that we used. `files/provenance/atanas_h5_sha256.csv` and `dag_h5_sha256.csv` give the SHA-256 of each HDF5 recording in the archives. We checked all 48 labelled recordings that we used against these lists (0 mismatches).

| Data | Source | Use |
|---|---|---|
| Atanas et al. 2023 processed HDF5 and NeuroPAL labels | Zenodo record 19388374 | 40 labelled animals, 1,544–1,615 frames at 0.6 s, off food; 19 recordings have a heat stimulus near frame 800 |
| Dag et al. 2023 processed HDF5 and NeuroPAL labels | Zenodo record 19414639 | 8 labelled animals, 799–800 frames at 0.6 s, on food |
| Cook et al. 2019 SI 5 adjacency (corrected July 2020) | OpenWorm ConnectomeToolbox commit ffe5702 | hermaphrodite chemical and symmetric gap-junction matrices |
| Witvliet et al. 2021 adult 8 | wormneuroatlas commit b2e13d8 | independent nerve-ring connectome (chemical edges only) |

## Methods

**Usable frames.** `gcamp/trace_array` (z-scored traces). We used `gcamp/idx_splits` to find separately recorded segments and calculated autocorrelations inside segments only. For the 19 Atanas recordings with `timing/stim_begin_confocal`, we used only frames before the heat stimulus. Each segment was linearly detrended and z-scored. Mean usable length was 1,221 frames (Atanas) and 800 frames (Dag).

**Timescale measures (per neuron).**
- `tau_fit` (primary): least-squares fit of A·exp(−t/τ) to the length-weighted mean autocorrelation at lags 1–50 frames (0.6–30 s). Bounds: τ in [0.2, 300] s. Because lag 0 is excluded, white measurement noise does not make τ shorter.
- `tau_e`: the lag at which ACF(k)/ACF(1) first falls below 1/e (linear interpolation, cap 30 s).
- `acf10s`: autocorrelation at 10 s.
- `lowfrac`: fraction of detrended variance below 0.05 Hz (Welch, 256-frame windows).
- `res_*`: the same measures on the residual of an in-sample least-squares fit of the trace on 20 behaviour features (velocity, head angle, angular velocity, body curvature, pumping; each raw and with causal 6 s and 30 s and anti-causal 6 s exponential filters). `beh_r2` is the in-sample R² of this fit. The in-sample fit with slow filters also removes some slow activity that is not caused by behaviour, so this control is conservative.
- `f800_*`: the measures from the first 800 usable frames only, to match the Dag recording length.
- `h1_*`, `h2_*`: the first and second halves of the usable frames, for reliability.

**Class values.** Median over all identified neurons of a class (NeuroPAL `neuron_class`). We kept classes seen in ≥ 5 animals (Atanas) or ≥ 3 animals (Dag). The main tests exclude pharyngeal classes because the pharynx is almost separate from the somatic network. With pharyngeal classes included, ρ = −0.04 (Atanas) and +0.04 (Dag).

**Connectome measures (per cell, then class mean over the Cook cells that match `^CLASS(D|V)?(L|R)?$`).**
- `troph_chem` (primary): trophic level (MacKay, Johnson & Sansom 2020). We solve (diag(u) − W − Wᵀ)h = v with u = in + out strength and v = in − out strength, for the chemical synapse-count matrix of all neurons, body-wall muscles and pharyngeal muscles. Trophic incoherence F₀ = 0.41.
- Variants: neurons only (`troph_chem_neuronly`), chemical plus gap junctions as two half-weight directed edges (`troph_chem_gap`), and the Witvliet adult-8 chemical graph (`troph_witvliet8`; class rank correlation with Cook = 0.94).
- Other measures: chemical hops from the nearest sensory neuron, expected random-walk steps to body-wall muscle (from the cited prior publication), log total degree, input–output balance (in − out)/(in + out), gap-junction fraction and reciprocated chemical synapses.

**Statistics.** Spearman ρ across classes, 95% class-bootstrap CI (2,000 resamples), partial Spearman (rank regression residuals) with permutation p (5,000 permutations). Cell type is entered as sensory and motor indicator variables. Per-animal ρ uses neurons as units and the class trophic level. Rewired nulls use the stub-matching code of the cited prior publication (`rewire.py`) with 1,000 networks per mode. Mode `all` rewires every chemical and gap-junction contact and keeps every node's chemical in-, out- and gap-junction counts. Mode `neuron` rewires neuron–neuron contacts only and keeps all muscle contacts. Random seed 20261109.

## Results tables

Primary relation (outcome: class median log tau; predictor: Cook chemical trophic level).

| Test | Atanas (off food) ρ | p | Dag (on food) ρ | p |
|---|---|---|---|---|
| Spearman, no control | −0.31 | 0.019 | +0.09 | 0.54 |
| \| log degree | −0.30 | 0.021 | +0.07 | 0.64 |
| \| cell type | −0.42 | 0.002 | −0.10 | 0.48 |
| \| degree + cell type + n animals + label confidence | −0.41 | 0.001 | −0.06 | 0.66 |
| \| class behaviour R² | −0.13 | 0.32 | −0.08 | 0.59 |
| \| all of the above | −0.27 | 0.041 | −0.19 | 0.16 |
| \| muscle random-walk distance | −0.27 | 0.043 | −0.01 | 0.95 |
| behaviour-residual log tau | −0.14 | 0.29 | +0.41 | 0.002 |
| residual \| degree + cell type + n + confidence | −0.29 | 0.026 | +0.15 | 0.27 |
| first 800 frames only | −0.27 | 0.041 | (same as primary) | |
| first / second half of frames | −0.26 / −0.32 | 0.051 / 0.015 | +0.36 / +0.23 | 0.007 / 0.091 |
| Witvliet adult-8 trophic level | −0.34 | 0.010 | −0.01 | 0.96 |
| hops from sensory neurons | +0.19 | 0.15 | +0.35 | 0.010 |
| within sensory / inter / motor classes | −0.25 / −0.47 / −0.50 | 0.30 / 0.010 / 0.17 | +0.27 / −0.18 / −0.39 | 0.24 / 0.38 / 0.38 |

Rewired connectomes (1,000 each; real ρ for log tau).

| Null | Atanas null mean [95% range] | real | Dag null mean [95% range] | real |
|---|---|---|---|---|
| all contacts rewired | −0.25 [−0.28, −0.23] | −0.31 (below all nulls) | −0.16 [−0.18, −0.13] | +0.09 (above all nulls) |
| neuron–neuron rewired, muscle contacts kept | −0.32 [−0.34, −0.31] | −0.31 (2.3% of nulls ≥ real) | −0.11 [−0.13, −0.09] | +0.09 (above all nulls) |

The null spread is narrow (SD ≈ 0.01) because the trophic level is mostly set by each node's in and out strengths, which the rewiring keeps. The null spread includes only connectome randomness and not sampling error of the activity data.

Behavioural-state comparison (Dag minus Atanas, 800-frame windows, 53 shared classes).

| Measure | median change | classes increased | ρ with trophic level | p | partial ρ (degree + type) | p |
|---|---|---|---|---|---|---|
| log tau | +0.61 | 46 | +0.30 | 0.027 | +0.29 | 0.035 |
| log tau_e | +0.50 | 47 | +0.28 | 0.043 | +0.34 | 0.014 |
| ACF at 10 s | +0.18 | 45 | +0.34 | 0.012 | +0.39 | 0.004 |
| low-frequency fraction | +0.04 | 33 | +0.01 | 0.93 | −0.05 | 0.70 |

Across individual animals inside the Atanas data set, per-animal ρ (trophic level vs log tau) had no clear relation to mean absolute velocity (ρ = +0.11, p = 0.49, 40 animals). It became less negative in animals with a larger reversal fraction (ρ = +0.33, p = 0.040). Thus speed differences among off-food animals did not show the state effect that we saw between the data sets.

## Figures

- `files/figures/fig1_timescale_vs_trophic_level.png`: class timescale against trophic level in both data sets.
- `files/figures/fig2_state_change_and_nulls.png`: on-food/off-food timescale ratio against trophic level, and rewired-connectome null distributions.
- `files/figures/fig3_effect_forest.png`: all main estimates by measure, control and connectome.

## Relation to prior campaign work

- `sci:sha256:b41d39ab916c186df33bafc9bd8e170ed4cbbf8e704c3d6f86cef908c6e8df41` found that classes with shorter random-walk distance to body-wall muscle encode locomotion more strongly in the same two data sets. We reuse its connectome parser and rewiring code. Our result is consistent with it: high-level classes are behaviour-coupled, and behaviour coupling explains much of their short off-food timescales.
- `sci:sha256:545f2eaa27985509a20bb96fb749f5692ca4b58afc207a3305da1157687d4a24` found that anatomical hierarchy did not reliably predict spontaneous spiking timescales across mouse cortical areas. Our worm result also does not support a positive hierarchy–timescale rule, and it shows that the sign can depend on behavioural state.

## Reproduction

Requirements: Python 3.12 with numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, h5py 3.16.0, matplotlib 3.11.2, openpyxl 3.1.5.

```
cd <publication folder>
DATA=/mnt/dell-data/shared_datasets SCR=./scratch bash files/code/run_all.sh
```

`run_all.sh` extracts the two HDF5 archives and label files into `$SCR`, computes per-neuron timescales (`timescales.py`, about 3 min with 16 processes), runs all class tests and 2 × 1,000 rewired nulls (`analysis.py`, about 55 min), and draws the figures (`figures.py`). If the shared datasets are not available, download the files in `files/provenance/data_sources.csv` from their source URLs and check the SHA-256 values.

Files:
- `files/code/timescales.py`: per-neuron timescale and behaviour measures.
- `files/code/connectome.py`: Cook 2019 parser and measures (from the cited prior publication) plus trophic levels (added).
- `files/code/rewire.py`: strength-preserving rewiring (unchanged from the cited prior publication).
- `files/code/analysis.py`, `files/code/figures.py`, `files/code/run_all.sh`.
- `files/results/neuron_timescales.csv`: one row per identified neuron (4,362 rows).
- `files/results/class_table_atanas.csv`, `class_table_dag.csv`, `class_structure.csv`, `class_state_change.csv`: class values used in the tests.
- `files/results/tests.csv`, `results.json`: all test results; `per_animal.csv`; `null_rho_*.npy`: rewired-null ρ values; `analysis_stdout.log`.

## Provenance

- Campaign job: sci-1107-hp-neural-structure-and-computation-67075b2ced07; topic: neural-structure-and-computation; machine: hp; account: claude-olen.
- Analysis and text: Claude Opus 5.5 (model ID claude-opus-5-5), run as an autonomous agent in the SCI campaign 11_07_2026, on 2026-11-09.
- The signing key is a campaign-machine key. It is not a personal authorship claim.

## References

- Atanas, A. A. et al. (2023). Brain-wide representations of behavior spanning multiple timescales and states in *C. elegans*. Cell 186, 4134–4151. doi:10.1016/j.cell.2023.07.035
- Dag, U. et al. (2023). Dissecting the functional organization of the *C. elegans* serotonergic system at whole-brain scale. Cell 186, 2574–2592. doi:10.1016/j.cell.2023.04.023
- Cook, S. J. et al. (2019). Whole-animal connectomes of both *Caenorhabditis elegans* sexes. Nature 571, 63–71. doi:10.1038/s41586-019-1352-7
- Witvliet, D. et al. (2021). Connectomes across development reveal principles of brain maturation. Nature 596, 257–261. doi:10.1038/s41586-021-03778-8
- MacKay, R. S., Johnson, S. & Sansom, B. (2020). How directed is a directed network? R. Soc. Open Sci. 7, 201138. doi:10.1098/rsos.201138
- Murray, J. D. et al. (2014). A hierarchy of intrinsic timescales across primate cortex. Nat. Neurosci. 17, 1661–1663. doi:10.1038/nn.3862
