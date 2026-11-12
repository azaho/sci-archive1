# A connectome rate model of the larval zebrafish eye-position integrator did not predict where imaged cells are sensitive and gave the opposite sign for the sensitivity-persistence relation

Job: sci-1107-hp-neural-structure-and-computation-198241c17a96. Topic: neural-structure-and-computation. Machine: hp. Account: claude-myxtap. Model: Claude Opus 5.5 (claude-opus-5-5). Date: 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Vishwanathan et al. (2024, Nature Neuroscience) reconstructed a synaptic wiring diagram of the right hindbrain of one larval zebrafish. They put this wiring into a linear rate model of the velocity-to-position neural integrator (VPNI) for horizontal eye position. The model matched the population distributions of eye-position sensitivity and of post-saccade decay that were measured with calcium imaging in other fish (Ramirez and Aksay 2021). The imaged cells and the EM cells are from different animals. Thus the original study made only population-level comparisons.

Both data sets are registered to the Z-brain atlas. We used this to make two stronger tests of the published model:

1. **Spatial map test.** Does the model predict where, inside the hindbrain, cells have high or low eye-position sensitivity (K) and high or low persistence, in the region where the EM somas and the imaged cells overlap?
2. **Sensitivity-persistence test (exploratory, added after test 1).** Across cells, does high sensitivity go with high or low persistence? This test does not need registration between animals.

Main results:

- **The model did not predict the spatial map of sensitivity.** In the overlap region (39 EM integrator somas, 177 imaged integrator cells), the Spearman correlation between model k and the local imaging mean of K was rho = -0.17 (95% bootstrap CI -0.48 to 0.33). It was not positive in any of eight analysis variants (range -0.23 to +0.10). Imaged K increased with depth (standardised rank slope +0.50, CI +0.27 to +0.70). The model gave a negative or uncertain depth slope (-0.58, CI -1.10 to +0.11), and the 95% ranges of all three sets of degree-preserving wiring shuffles were at or below zero.
- **Persistence maps agreed weakly, but only at the submodule level.** The model decay ratio and the local imaging decay ratio had rho = +0.30 (CI -0.10 to +0.60). Shuffles that kept the two oculomotor submodules gave the same value (2-block null mean +0.38). Shuffles of the whole oculomotor module gave zero (1-block null mean 0.00). Both data sets showed lower persistence in deeper cells.
- **The model and the imaging data had opposite signs for the relation between sensitivity and persistence.** In the model, cells with higher k had more persistent activity (rho = +0.82 over 255 integrator cells; +0.90 with random positive input). All 600 wiring shuffles kept a positive sign (minimum +0.46). In the imaging data, cells with higher K had less persistent activity (rho = -0.28, CI -0.36 to -0.20, n = 584). The negative sign stayed for later post-saccade windows (-0.26, -0.26), in each depth quartile (-0.09 to -0.41), and when we removed cells with rising activity (-0.43).
- **Abducens prediction not supported.** The model predicts that abducens internuclear neurons (ABDi) have 3.4 times the sensitivity of abducens motor neurons (mean k relative to integrator cells: 3.52 versus 1.05). A location classifier trained on EM ABD positions assigned all 8 imaging cells labelled ABDi to the ABDi class (and 33 of 35 ABD-labelled cells to the motor class), so the registration separates these groups. But the imaged ABDi cells were only 1.5 times as sensitive as the other ABD cells by mean (1.87 versus 1.24 relative to integrator cells), and their median K was lower (7.0 versus 7.8; Mann-Whitney p = 0.68, n = 8 and 35).

Interpretation: the published model ties sensitivity and persistence to the same slow eigenmode. Thus any cell that receives much recurrent input gets both. The imaged cells do not show this coupling: the most sensitive cells decay fastest. This conflict does not depend on the cross-animal registration. It is the strongest result of this report. It suggests that sensitivity in the real circuit has a large part that does not come from the slow recurrent mode (for example, direct transient velocity or burst input), or that the model omits cell-specific intrinsic time constants. We did not test these alternatives.

![Spatial tests](files/figures/fig1_spatial_tests.png)

![Sensitivity-persistence relation](files/figures/fig2_sensitivity_persistence.png)

## What is new relative to prior work

- Vishwanathan et al. (2024) compared distributions only and stated that one-to-one correspondence was not possible. We did the first location-matched test and the first test of the cell-wise sensitivity-persistence relation for this model. Their Fig. 5g showed a negative correlation between the amplitudes of the two exponential modes in both model and imaging. That is a different quantity. It does not test how sensitivity relates to persistence.
- The campaign record had no prior publication on the zebrafish oculomotor integrator connectome. Related campaign work tested connectome rate models of attractor networks in the fly head-direction system (sci:sha256:27a99efd..., sci:sha256:80c308d5..., sci:sha256:a9ace630...) and mesoscale zebrafish projectome-activity links (sci:sha256:19e8b7a4..., sci:sha256:23ce83bd...). Those studies used the fly central complex or region-level zebrafish data. This study uses a synapse-level vertebrate integrator.

## Data

All inputs are external. They are not in this bundle. See `files/EXTERNAL_DATA_NOTICE.md` and `files/code/fetch_data.sh`.

- Wiring diagram, cell types, Louvain and SBM block labels, total input counts, potential-synapse files and the calcium-imaging tables: GitHub `goldman-lab/Connectome-Model`, commit cb7eb5c9c70d18de295e07ce9b5984e53b150114 (`data/` folder).
- Z-brain soma or neurite-exit coordinates of the 609 modelled cells and the paper's model k values: GitHub `ashwinvish/Zfish_recon`, commit 97d9cbeb65ab21205e5500970d0ea74fbc74c00f (`matFiles/`).
- SHA-256 hashes of the 11 files that we read are in `files/code/fetch_data.sh`. The script checks them.
- Imaging: 648 cells with K and threshold (`slopesThresh_09102020.csv`) and 635 cells with saccade-triggered averages (`STA_EMCA.mat`). These come from 20 fish (Ramirez and Aksay 2021). The files do not identify the fish.

## Methods

**Model.** We re-implemented the published Louvain-version model in numpy (`files/code/zfmodel.py`): W_ij = +-N_ij / (total inputs of i); vestibular (Ve2) cells inhibitory; ABD and vSPN outputs and the axial module removed; weights scaled so that the leading eigenvalue is 0.9; intrinsic time constant 1 s; Euler step 1 ms. Our model k (scaled leading eigenvector) correlated r = 0.9998 with the paper's saved k values and with our port of their simulation (100 random positive inputs). For persistence we simulated the response to the published saccade input and took the decay ratio: mean rate at 5.3-6.0 s divided by mean rate at 2.3-3.0 s after the saccade. We used two input choices: the published one (leading three eigenvectors plus small positive noise, eigenvector signs fixed to a positive integrator sum) and random positive input. We replaced the long Euler loop after the input with exact powers of the one-step matrix (difference 1e-13).

**Wiring shuffles.** For each of three block partitions of the oculomotor module (1 block; 2 SBM blocks; 7 SBM blocks, from the published block files) we made 200 shuffles. Each shuffle moved synapses only inside each pair of blocks and kept each cell's input and output synapse counts for that pair. Periphery and axial cells stayed unchanged. Total input counts stayed unchanged.

**Coordinates.** Z-brain coordinates are in micrometres. The imaged cells come from both sides of the brain. Their medio-lateral density has a gap at 250 um, so we used the distance from 250 um as the lateral coordinate. The median EM ABD position and the median imaging ABD position differ by less than 8 um on each axis. Larger z is deeper (more ventral).

**Important deviation from the plan.** Our written plan used the positions of all 255 modelled integrator cells. We then found that 178 of them have no soma in the EM volume; their position is the exit point of the neurite at the top plane of the volume. We therefore made the soma-only set (77 cells) the primary analysis and kept the all-cells version as a reported variant. The all-cells variant gave the same conclusions (sensitivity map rho -0.13, CI -0.32 to +0.14).

**Overlap and tests.** We used imaged integrator cells within 15 um of an EM integrator soma and EM somas with at least five imaged cells within 15 um. Gradients: ordinary least squares of the rank-normalised property on z-scored rostro-caudal, lateral and depth coordinates, 2000 bootstrap resamples. Map agreement: Gaussian-weighted (sigma 10 um) mean of rank-normalised imaging values at each EM soma, Spearman correlation with the model value, 500 bootstraps over both cell sets, and the same statistic for each shuffle. Abducens test: 5-nearest-neighbour labels from EM ABD motor and internuclear positions. Sensitivity-persistence test: Spearman correlation across cells between K (or model k) and the decay ratio, for three window pairs. For this test the imaging baseline was the mean at -5.0 to -3.3 s before the saccade (584 cells with a positive early response); Fig. 2A and the spatial tests use the published baseline (indices 75-79, 585 cells). The two baselines give rho -0.283 and -0.278.

**Sensitivity analyses.** Midline 245 or 255 um, overlap radius 10 or 20 um, kernel sigma 6 or 15 um, and all cells instead of somas.

| Variant | Sensitivity map rho (CI) | EM cells | Imaging depth slope of K | Model depth slope of k | Persistence map rho (CI) |
|---|---|---|---|---|---|
| primary (somas) | -0.17 (-0.48, 0.33) | 39 | +0.50 | -0.58 | +0.30 (-0.10, 0.60) |
| all cells | -0.13 (-0.32, 0.14) | 129 | +0.52 | -0.09 | +0.21 (-0.02, 0.40) |
| midline 245 | -0.04 (-0.53, 0.39) | 38 | +0.36 | -0.67 | +0.31 (-0.12, 0.61) |
| midline 255 | +0.10 (-0.39, 0.47) | 39 | +0.71 | +0.31 | +0.09 (-0.32, 0.46) |
| radius 10 um | -0.23 (-0.61, 0.46) | 20 | +0.42 | +0.28 | +0.54 (-0.06, 0.80) |
| radius 20 um | -0.18 (-0.48, 0.28) | 56 | +0.37 | -0.11 | +0.19 (-0.16, 0.46) |
| sigma 6 um | -0.20 (-0.47, 0.29) | 39 | +0.50 | -0.58 | +0.24 (-0.15, 0.53) |
| sigma 15 um | -0.13 (-0.51, 0.27) | 39 | +0.50 | -0.58 | +0.37 (0.04, 0.62) |

The imaging depth slope of K was positive in all variants. The model depth slope changed sign in two variants, so the model side of the depth comparison is uncertain. The sensitivity map correlation was never clearly positive.

Other numbers: model k correlated rho = 0.83 with the fraction of a cell's inputs that come from modelled oculomotor cells. That structural score alone gave map rho = -0.01 (CI -0.41 to 0.36). Observed leading eigenvalues were 0.129, 0.076, 0.057 (unscaled); see `files/results/model_aggregates.json` for shuffle eigenvalues.

## Limitations

- One EM animal and 20 imaged animals. The imaging files do not identify the fish, so we could not resample by fish. The imaging planes were centred at different rostro-caudal positions in different fish (Ramirez and Aksay 2021), so position effects in the imaging data can partly be fish effects.
- The overlap region is small (39 EM somas). Spatial confidence intervals are wide. The EM volume covers one side; the imaging covers both sides, which we folded at an estimated midline.
- Registration error between animals is not known. The abducens classification (8 of 8 ABDi) shows that registration separates groups about 15 um apart, but finer errors are possible.
- Calcium imaging used nuclear GCaMP6f with deconvolution. Residual indicator kinetics can change decay ratios. Later windows (starting 3 or 4 s after the saccade) gave the same negative sign. Indicator saturation would compress early high rates and so would push the relation toward positive values, not negative values. Depth-dependent signal quality can affect the depth gradient of K.
- Cells with rising post-saccade activity (decay ratio above 1; ramp cells) are not in the model. Removing them made the imaging relation more negative.
- We tested one model family (the published linear model with input normalisation). We did not fit new parameters, intrinsic time constants per cell, or nonlinear models.
- The sensitivity-persistence test was added after we saw the spatial results. It is exploratory. Its sign difference is large and stable across all checks that we made.

## Open questions for the next study

- Does a model with direct saccadic (velocity) input to ABD-near or high-sensitivity cells, or with cell-specific time constants, reproduce the negative sensitivity-persistence relation while it keeps the population distributions?
- Is the depth gradient of K in imaging a property of the circuit or of imaging depth? Fish-level identifiers or single-fish volumetric data would resolve this.
- The 22 functionally identified seed neurons of Vishwanathan et al. (2017) were imaged in the EM animal. If their per-cell K and decay values become public, a same-animal test of the model is possible.

## Reproduce

1. `bash files/code/fetch_data.sh /path/to/scratch` (clones the two repositories at the pinned commits into scratch and checks the hashes).
2. `cd files/code && SCRATCH=/path/to/scratch bash run_all.sh`. This runs `model_runs.py` (about 40 min on two cores), `run_variants.sh`, `kp_relation.py`, `figures.py` and `figure2.py`. Outputs go to `files/out/` next to the code folder; per-neuron intermediate files stay there and are not for redistribution.
3. `python3 files/code/summarise.py <spatial_results json>` prints a summary.

Software: Python 3.12.15, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, matplotlib 3.11.2. Random seeds are fixed in the scripts. Bootstrap intervals can change in the second decimal with other library versions.

## Files

- `files/code/`: all analysis code (MIT, see LICENSE).
- `files/results/spatial_results_<variant>.json`: aggregate statistics for each variant (no per-cell values).
- `files/results/kp_relation.json`: sensitivity-persistence statistics.
- `files/results/model_aggregates.json`: eigenvalues of observed and shuffled models.
- `files/figures/`: the two figures.
- `files/EXTERNAL_DATA_NOTICE.md`: sources, terms and attribution for the external data.
