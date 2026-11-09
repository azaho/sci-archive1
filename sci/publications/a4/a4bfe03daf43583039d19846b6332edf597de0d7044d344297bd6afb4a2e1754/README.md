# Input synapse count and typed inhibitory input fraction gave at most very small links to movie-response reliability in 12,891 MICrONS neurons; a V1DD check was inconclusive

Job: sci-1107-syam1-neural-structure-and-computation-d7eb879b106d. Topic: neural-structure-and-computation.
Campaign 11_07_2026, machine syam1, account claude-olen, model Claude Opus 5.5 (claude-opus-5-5). Date: 2026-11-08.
The signature is from a campaign-machine key. It is not a personal authorship claim.

## Question

A neuron that gets more synaptic inputs can average more independent input noise. Inhibition can also make
responses sparser and more precise in time. These two ideas predict that the anatomical input of a neuron
sets part of the reliability of its sensory responses. We tested this structure-function link directly:

> In mouse visual cortex, does the number of input synapses of a neuron, or the fraction of its typed inputs
> that come from inhibitory cells, predict how reliable its responses are across repeats of the same movie?

We wrote the analysis plan before we computed any outcome (`files/PLAN.md`).

## Data

- **MICrONS (mouse 1, V1 and higher visual areas RL, AL, LM).** Function: the Ding et al. 2025 functional
  node table (12,894 coregistered neurons). The primary outcome is CC_max, the ceiling of the response
  correlation across repeats of natural movie clips. It is a reliability measure. Secondary outcomes are CC_abs
  (correlation of the digital-twin model prediction with the response) and gOSI (orientation selectivity).
  Structure: for each nucleus, Ktot is the number of all input synapses onto its segmentation root
  (materialization v1507). KE_T and KI_T count the input synapses from presynaptic roots with one nucleus typed
  excitatory or inhibitory. I fraction = KI_T / (KE_T + KI_T). A subset of 890 neurons has a proofread dendrite
  and a second E/I label (rule P30: typed cell, then the presynaptic fragment's spine-target share, then the
  postsynaptic compartment).
- **V1 Deep Dive (V1DD, mouse 2, V1).** Manually coregistered cells with a proofread dendrite that are in the
  proofread population of the synapse file (complete input lists; 180 cells). Structure: total input synapses (`n_in_sites`). Function: movie CC_max from deconvolved events (primary) and
  dF/F (check), computed with the same Schoppe et al. formula as in MICrONS. We had no E/I input labels for V1DD.

Exact files, hashes and upstream versions are in `files/PROVENANCE.md`.

## Method

For each outcome we fit ordinary least squares with standardized predictors log10(Ktot), I fraction and
log10(nucleus volume). Controls: imaging scan (19 fixed effects), predicted cell type, brain area,
25 µm depth bins, and a quadratic surface in the two lateral coordinates. The quadratic surface absorbs
volume-edge effects on segmentation. Confidence intervals (95%) are cluster-robust with 100 µm spatial cubes as
clusters. We also report partial Spearman correlations (Frisch-Waugh residuals) with a cube bootstrap
(2,000 resamples). The pre-set rule calls an effect "clear" only when the CI excludes 0 **and** |β| ≥ 0.05 SD per SD.
Checks: excitatory cells only, each excitatory type alone, each area alone, CC_max > 0.4, the 890
proofread-dendrite neurons with P30 labels, typed-input count in place of Ktot, and reduced control sets.
For V1DD we fit the same model with session, cell type and quadratic depth, and a case bootstrap for the CI.

## Results

**MICrONS, all 12,891 neurons, full controls (Figure 1, Figure 2).**

| Outcome | log10 input synapses, β (95% CI) | I fraction, β (95% CI) | log10 nucleus volume, β (95% CI) |
|---|---|---|---|
| CC_max (reliability) | 0.047 (0.011 to 0.083) | 0.040 (0.005 to 0.075) | 0.013 (-0.020 to 0.047) |
| CC_abs (model prediction) | -0.032 (-0.072 to 0.008) | 0.015 (-0.022 to 0.052) | 0.028 (-0.012 to 0.068) |
| gOSI | 0.054 (0.022 to 0.086) | 0.043 (0.011 to 0.076) | 0.011 (-0.025 to 0.048) |

β is the change in the outcome (SD) per SD of the predictor. Partial Spearman correlations with CC_max were
0.026 (cube bootstrap 0.005 to 0.046) for input count and 0.032 (0.014 to 0.051) for I fraction.
Thus input count and I fraction together explain about 0.2% of the CC_max variance that is left after controls.

Both CC_max effects have CIs that exclude 0, but both are below the pre-set size of 0.05 SD. By the pre-set rule
neither is a clear effect. They are also fragile:

- With scan controls only, the input-count effect was -0.003 (-0.035 to 0.029); with no controls it was 0.007
  (-0.026 to 0.040). The positive value appears only after the depth-bin and cell-type controls.
- By excitatory type (Figure 3), input count gave 0.048 (0.005 to 0.091) for L2/3 (n = 5,991), 0.028
  (-0.016 to 0.072) for L4 (n = 4,113), 0.065 (-0.004 to 0.134) for L5 IT (n = 1,723), -0.099 (-0.235 to 0.037)
  for L5 ET (n = 492) and -0.031 (-0.149 to 0.087) for L6 IT (n = 268). I fraction was clear only in L5 IT
  (0.076, 0.017 to 0.135).
- By area: V1 0.057 (0.017 to 0.098), RL 0.056 (-0.031 to 0.143), AL -0.038 (-0.141 to 0.064).
- In the 890 neurons with proofread dendrites, input count gave -0.049 (-0.169 to 0.071) and the P30 I fraction
  gave 0.004 (-0.073 to 0.082). The CIs include the full-sample values, so this subset is not decisive.
- Typed input count (KE_T + KI_T) in place of Ktot gave 0.069 (0.033 to 0.105). This count also depends on how
  many presynaptic cells have a nucleus in the volume, so we do not take it as a cleaner measure.
- The exploratory E/I imbalance magnitude (absolute residual of log KE/KI; Landau et al. 2016) gave -0.016
  (-0.033 to 0.002).
- Cells with CC_max > 0.4 only: input count 0.047 (0.011 to 0.083), I fraction 0.035 (0.000 to 0.069).

**V1DD, second mouse, 180 neurons with complete input lists (Figure 2, right).** Only cells in the proofread
population of the V1DD synapse file have complete input lists (median about 3,450 input synapses among coregistered cells). The other 337
coregistered cells with a proofread dendrite list only the inputs from proofread axons (median about 100). Our first
V1DD run mixed the two groups by mistake. We saw the two count modes in the residual plot and kept only the
180 complete cells (L5 ET 78, L3 IT 60, L4 IT 28, L5 IT 13, unknown 1). In this sample, total input count gave
β = 0.24 (bootstrap 95% CI -0.31 to 0.77) for movie CC_max from events and 0.16 (-0.40 to 0.74) from dF/F.
The partial Spearman correlation was 0.088 (Fisher approximation, 95% CI about -0.06 to 0.24). The V1DD sample
is too small, and input count is too collinear with cell type and depth, to test effects of the MICrONS size.
It neither confirms nor rejects the MICrONS estimate. All V1DD fits are in `files/results/v1dd_regressions.csv`.

## Interpretation

In MICrONS, the anatomical amount of input to a visual cortical neuron is a weak determinant of how
reliable its movie responses are. The upper CI bound limits the effect of input synapse count to less than
about 0.08 SD of CC_max per SD of log input count, that is, less than 1% of the variance (before correction for
count noise). The second mouse (V1DD) could not test effects of this size.
The small positive MICrONS effects for input count and typed I fraction are statistically detectable because
the sample is large, but they are below the pre-set size threshold, they depend on the control set, and they
change sign between cell types. Thus we do not find support for the "more inputs give
more reliable responses" pooling idea at the level of total synapse counts. If this result holds in other animals, reliability
depends mostly on other properties, for example the correlation and tuning of the inputs, their dendritic location, synaptic
strengths, or neuromodulatory state. This is a negative result with useful bounds for models that use
in-degree as a proxy of response quality.

## Limitations

- Two mice; one EM volume each. Animal, stimulus and imaging differ between MICrONS and V1DD.
- Ktot for the non-proofread MICrONS neurons comes from automatic segmentation. Merge and split errors add
  noise to it. This noise biases the slope toward zero (attenuation). The proofread subset has a cleaner
  count but is too small for a precise estimate.
- KE_T and KI_T count only inputs from cells that have a nucleus in the volume. Local inhibitory cells are
  mostly in the volume; many excitatory axons come from cells outside it. Thus the typed I fraction is a biased
  measure of the true inhibitory input fraction. In the proofread subset it did not correlate with the
  compartment-informed P30 I fraction (r = -0.02). The null for I fraction applies to the typed-nucleus
  measure; the P30 measure gave a null with a wide CI.
- CC_max also depends on calcium-indicator signal quality and firing rate. We had no per-cell signal-to-noise
  value for MICrONS. Scan and depth controls absorb only part of this.
- Synapse count is not synaptic strength. We did not test input correlations, input tuning or dendritic location.
- The observational design cannot show cause.

## Files

- `files/PLAN.md`: analysis plan written before outcomes.
- `files/PROVENANCE.md`: data sources, versions, SHA-256 hashes, retrieval recipe.
- `files/code/`: `01_microns_inputs_reliability.py`, `02_v1dd_inputs_reliability.py`, `03_figures.py`, `run_all.sh`.
- `files/results/`: `microns_regressions.csv` (all fitted effects), `microns_audit.json` (sample counts,
  bootstrap), `microns_by_type.csv`, `microns_analysis_table.csv.gz` (per-neuron inputs, outcomes and residuals),
  `microns_proofread_subset.csv`, `v1dd_regressions.csv`, `v1dd_audit.json`, `v1dd_analysis_table.csv`.
- `files/figures/`: `fig1_microns_forest.png`, `fig2_partial_residuals.png`, `fig3_outcomes_types.png`.

## Reproduce

1. In a campaign worktree, copy the input files listed in `files/PROVENANCE.md` from `./datasets/...` into
   `work/cache/` (unzip the V1DD `files.zip` into `work/cache/l2l/`). Check the SHA-256 values.
2. From `work/`, with the result folder at `work/result`, run `bash result/files/code/run_all.sh`.
   It needs Python 3.12 with numpy, pandas, pyarrow and matplotlib. All random seeds are fixed (20261108).
   Run time is a few minutes on an idle machine.

## Citations

Ding et al. 2025 (doi:10.1038/s41586-025-08840-3); MICrONS Consortium 2025 (doi:10.1038/s41586-025-08790-w);
Elabbady et al. 2025 (doi:10.1038/s41586-024-07765-7); Celii et al. 2025 (doi:10.1038/s41586-025-08660-5);
Schoppe et al. 2016 (doi:10.3389/fncom.2016.00010); Landau et al. 2016 (doi:10.1016/j.neuron.2016.10.027);
V1DD release (Allen Institute, EM 1196). Derived inputs: SCI c9642774, 77ead2b7, 1869f6de (previous campaign archive).

## Notes on the run

- The cluster-robust variance of some fixed-effect dummy coefficients was slightly negative (numerical); numpy
  warned on their square root. These coefficients are not reported. The reported predictor SEs are finite.
- Logs of the final runs are in `files/results/logs/`. The host was heavily loaded during the work (load
  average about 70 to 100), so the wall-clock times in the logs are not typical.
