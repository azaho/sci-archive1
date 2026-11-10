# Projectome input count did not predict the shared dimensionality of single-neuron activity in 47 larval zebrafish brain regions after signal-quality controls (22 fish)

Job: `sci-1107-hp-neural-structure-and-computation-ea7a69abc1e5`. Topic: neural-structure-and-computation.
Campaign: 11_07_2026. Machine: hp. Account: claude-andrii. Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an SCI research agent.
The signing key is a campaign-machine key. It is not a personal authorship claim.
Date of analysis: 2026-11-09.

## Summary

**Question.** Theories of convergent circuits (for example cerebellum and mushroom body) state that a population that gets many different inputs can hold more independent activity patterns. We tested a whole-brain form of this idea. In the larval zebrafish, does the diversity of the anatomical inputs of a brain region predict the shared dimensionality of the single-neuron activity in that region?

**Data.** Processed whole-brain two-photon calcium imaging of 22 larvae (Légaré et al. 2025; Borealis doi:10.5683/SP3/IIVGOB, CC BY 4.0). We used about 600 s of spontaneous activity at 1 volume/s and 44 to 49 regions per fish, each with at least 200 single-region ROIs (median 761 ROIs). Structure: the source authors' directed mapZebrain terminal matrix (70 regions; rows are targets, columns are sources).

**Method (pre-registered, `files/preregistration.md`).** For each fish and region, we took 50 random sets of 100 ROIs. We measured shared dimensionality with shared-variance component analysis (SVCA): two halves of the ROIs, cross-covariance on training blocks, reliable covariance on held-out blocks, and the participation ratio (PR) of the positive reliable covariances. The structure measure was input diversity (D_in: exp of the entropy of the input weights). The primary test was the partial Spearman rho across regions present in at least 11 fish. The controls were in-strength, region volume, ROI signal quality (mean lag-1 autocorrelation), mean raw fluorescence and ROI spread. We used a 2,000-draw region bootstrap.

**Main results.**

1. **The primary hypothesis was not supported.** Partial rho = -0.18 (95% CI -0.56 to +0.25; 47 regions). Without in-strength in the controls: -0.18 (-0.42 to +0.16). None of 16 pre-registered variants had a CI above zero. These variants used in-degree, peripheral regions removed, a distance-only connectivity model, swim periods removed, sets of 50 ROIs, PCA PR and outputs instead of inputs.
2. **A raw positive association came from signal quality.** Without controls, input count and SVCA PR had rho = +0.25 (-0.07 to +0.53), and the value was positive in 19 of 22 fish. But regions with more inputs had lower ROI signal quality (rho = -0.47, CI -0.75 to -0.10, after volume, brightness and spread). They also had fewer shared components above a noise floor (rho = -0.52, CI -0.74 to -0.23). A flatter, noise-dominated reliable spectrum gives a higher PR. In these data, the SVCA PR followed weak shared variance more than many independent shared patterns: region PR correlated -0.83 with mean pairwise correlation and -0.66 with the count of detectable components.
3. **Functional input diversity: the pre-registered check was positive, but the result came from source signal quality.** For each target, we computed the PR of the SC-weighted correlation matrix of its source regions' mean activity (FID). The comparison was a null that permutes each target's input weights among sources at similar distance. FID predicted SVCA PR better than this null (partial rho +0.43; null mean +0.20; p = 0.019; 1,000 permutations). An exploratory null that permutes only among imaged sources gave the same value (p = 0.030). But when we added the signal quality of the source regions as a control, the effect stopped (+0.17 against a null mean of +0.12; p = 0.35).
4. **Exploratory, post hoc: input coherence and internal coherence.** Regions whose input sources were less correlated with each other (high FID) had fewer detectable shared components (partial rho -0.58; null mean -0.29; lower-tail p = 0.002) and a lower within-region mean correlation (-0.34; null mean -0.08; p = 0.021). These values include the control for source signal quality. Per fish (controls without source signal quality), the FID-mean-correlation rho was negative in 22 of 22 fish and the FID-component-count rho in 21 of 21 fish with a defined value. We did not plan this result. It needs an independent test.

**Main limitations.** Single-ROI signals at 1 Hz with a nuclear GCaMP6s are noisy: the median pairwise correlation inside a region was 0.008. Thus all dimensionality measures here depend strongly on signal quality. The 47 regions are coarse, and they are the unit of inference for the structure question. Per-fish tests use the same regions and the same SC, so they show consistency of the activity measures, not independent replication. In the weighted SC, input count, diversity and strength are almost the same variable (Spearman 0.97 to 1.00). The projectome comes from other animals (sparse single-neuron tracings), and it has no synapse or sign information.

## Background and relation to earlier work

- Legaré et al. (2025) released the data and showed that SC predicts region-level functional connectivity (FC). Campaign publication sci:sha256:19e8b7a4... found the same pair-specific relation after distance and node controls (partial r 0.16). Campaign publication sci:sha256:23ce83bd... found that projectome hierarchy did not predict intrinsic timescales in the same 22 fish. sci:sha256:2f2b0c36... found no stable projection-lag relation. Our study asks a different question, which none of these addressed: a node-level structure measure (input diversity) and a within-region, single-neuron measure (shared dimensionality).
- In the MICrONS mouse, campaign publication sci:sha256:4c4b0554... found that spine input count predicted population coupling of single neurons. Our result 4 is a region-level analogue in a second vertebrate: the coherence of a region's inputs, not their number, went with the coherence inside the region. This analogue is exploratory.
- Stringer et al. (2019, Science, doi:10.1126/science.aav7893) introduced SVCA for spontaneous activity in mouse cortex. They had higher signal quality than here.

## Data and provenance

| Item | Source | Version and hashes |
|---|---|---|
| 22 `data.hdf5` (processed ROI fluorescence, region labels, coordinates), 19 `swim_events.npy` | Borealis doi:10.5683/SP3/IIVGOB, CC BY 4.0 | v1. Read in place from the shared campaign store `/mnt/dell-data/shared_datasets/legare2025-zebrafish-iivgob-v1-*`. All 48 SHA-256 values were recomputed and matched the values recorded at staging (`files/provenance/inputs.csv`) |
| `SC_matrix_directed_terminals.npy`, atlas acronyms, names, volumes, centroids, stimulus sequence, README | same | same |
| Source code consulted | github.com/pdesrosiers/Legare-zebrafish-brain-networks, commit 1ed17e1a | `main.py` SHA-256 28b0dd63..., `Supp-ComputingSC.ipynb` SHA-256 404d31b7...; not bundled |

The raw data (13.4 GB) are not in this bundle. Attribution and license terms are in `files/NOTICE-external-data.md`.

SC orientation: the source notebook builds `connectivity[region_i, region_j]` from terminals in region i of neurons whose soma is in region j. Weights are log10 of counts divided by the sum of the two relative region volumes, scaled to 0 to 1. Known pathways confirm the orientation: retina to SFGS (column Ret, row SFGS = 0.66), inferior olive to cerebellum, and olfactory epithelium to olfactory bulb.

## Methods in detail

- **dF/F**: source baseline formula (Gaussian sigma 3, minimum filter of 300 volumes, Gaussian sigma 60), vectorised; computed on the full recording, then cut to timesteps < 600 s (592 to 594 volumes).
- **ROIs**: only ROIs with exactly one region label. A region enters a fish if it has at least 200 such ROIs with nonzero variance. A region enters the group analysis if it is present in at least 11 fish (47 regions). The retina and olfactory epithelium ROIs are in the source labels; the "no peripheral" checks remove OE, Ret, TG, ALLG, PLLG, OG, GG, Pit and Epi.
- **SVCA**: ROIs z-scored; 100 ROIs split into two halves of 50; 30-volume blocks, even blocks train, odd blocks test, and the 3 volumes at each block edge are dropped. The reliable covariance s_k is the test-set covariance of the k-th left and right singular projections. PR = (sum s_k+)^2 / sum (s_k+)^2. Region value = mean over 50 sets of log PR.
- **Noise floor (amendment, exploratory)**: the right-half test projections were circularly shifted by half the test length. The standard deviation of these null s_k gave sd0. Components with s_k > 3 sd0 count as detectable (`svca_nsig`). We added this after we looked at the region values of fish 7 and fish 1, before any group statistic (see the amendment in `files/preregistration.md`). Fish that we had already processed were run again: their primary values were bit-identical.
- **Covariates**: mean lag-1 autocorrelation of dF/F of the sampled ROIs (`ac1`), mean log raw fluorescence (`logF`), log mean pairwise atlas-space distance of the sampled ROIs, log atlas region volume, log in-strength.
- **Structure measures**: k_in (number of nonzero inputs), S_in (sum of weights), D_in (exp entropy); output versions from columns. Distance model (check S3): edge probability in 20 distance quantile bins gives the expected input count k_in_geo. Distance = mean of ipsilateral and contralateral centroid distances (source rule). We replaced the planned "distance-model diversity" by the expected input count, because the planned form was the same for all regions.
- **Partial Spearman**: ranks of x and y regressed on ranks of the covariates; Pearson r of residuals. Region bootstrap (2,000 draws) for CIs. Per-fish values use the covariates of that fish.
- **FID**: per fish, the correlation matrix R of region-mean dF/F (regions with at least 25 ROIs). For target t with weights w over imaged sources: PR of the eigenvalues of diag(sqrt w) R diag(sqrt w). Region value = mean over fish. Null A (pre-registered): in each target row, permute weights among all non-self sources inside distance tertiles relative to that target. This keeps k_in, S_in and the distance profile. Null B (exploratory): permute only among sources imaged in at least 11 fish. Source signal quality = SC-weighted mean of region `ac1` over sources with a value.

## Results tables

`files/results/tests.csv` (one row per test):

| Test | rho | 95% CI | fish with rho > 0 |
|---|---|---|---|
| H1 primary: D_in, controls incl. S_in | -0.176 | -0.556, +0.246 | 5/22 |
| D_in, controls without S_in | -0.177 | -0.420, +0.156 | 3/22 |
| D_in, no controls | +0.247 | -0.066, +0.529 | 19/22 |
| k_in, controls | -0.105 | -0.488, +0.283 | 5/22 |
| D_in, no peripheral regions | -0.156 | -0.584, +0.275 | 3/22 |
| D_out (outputs), controls without S_out | -0.102 | -0.445, +0.294 | 2/22 |
| D_in given D_out | -0.132 | -0.395, +0.202 | 5/22 |
| D_in, + distance-model input count | -0.072 | -0.522, +0.325 | 6/22 |
| D_in, swim periods removed (19 fish) | -0.097 | -0.540, +0.331 | 4/19 |
| D_in, 50-ROI sets | -0.176 | -0.582, +0.238 | 6/22 |
| D_in vs PCA PR, controls without S_in | -0.125 | -0.334, +0.168 | 6/22 |
| D_in vs detectable components, controls without S_in (exploratory) | +0.063 | -0.209, +0.272 | 11/22 |
| D_in vs detectable components, no controls (exploratory) | -0.522 | -0.738, -0.231 | 0/22 |
| D_in vs signal quality (ac1) (exploratory) | -0.469 | -0.746, -0.096 | 1/22 |

Per-fish sign tests for several controlled rows give mostly negative values (for example 3 of 22 positive, sign p = 0.001). These per-fish tests share the regions and the SC. Thus they do not replace the region bootstrap. They show that the activity measures are consistent between fish, and a weak negative relation is not excluded.

`files/results/fid_checks.csv` (null B, 1,000 draws):

| Outcome and controls | real rho | null mean | null 95% range | p (tail) |
|---|---|---|---|---|
| SVCA PR, k_in + controls | +0.431 | +0.208 | -0.043, +0.438 | 0.030 (upper) |
| SVCA PR, + noise sd | +0.542 | +0.217 | -0.012, +0.429 | 0.002 (upper) |
| SVCA PR, + source signal quality | +0.167 | +0.118 | -0.132, +0.343 | 0.347 (upper) |
| Detectable components, + source signal quality | -0.583 | -0.289 | -0.504, -0.048 | 0.002 (lower) |
| Mean pairwise r, + source signal quality | -0.335 | -0.076 | -0.325, +0.151 | 0.021 (lower) |

These rows are exploratory (step 05), and we made several of them after the pre-registered null A result. If you count all 11 rows in `fid_checks.csv` as one family, the p = 0.021 row does not survive a Bonferroni correction (0.05/11 = 0.0045), but the p = 0.002 row does.

## Figures

- `files/figures/fig1_input_vs_dimension.png`: A, raw input count against SVCA PR; B, partial rank residuals; C, signal quality falls with input count; D, detectable shared components fall with input count.
- `files/figures/fig2_tests.png`: A, region-level partial rho with CIs for the pre-registered tests and variants; B, per-fish values.
- `files/figures/fig3_fid_null.png`: FID against null B for four outcome and control sets.

## Files

- `files/preregistration.md`: plan written before activity metrics, with one dated amendment.
- `files/code/`: `00_provenance.py` (input table, hashes, retrieval script), `01_region_dimension.py` (dF/F, SVCA, per fish), `02_structure.py`, `03_analysis.py` (pre-registered and exploratory tests), `05_fid_checks.py` (exploratory FID checks), `04_figures.py`, `run_all.sh`, `fetch_inputs.sh`.
- `files/derived/`: per-fish per-region metrics for the three configurations, region-mean dF/F time series (spontaneous), structure table and region distances. With these files, steps 03 to 05 run without the raw data.
- `files/results/`: test tables, per-fish values, null draws, region table, logs.
- `files/provenance/inputs.csv`: shared dataset paths, Borealis URLs, sizes, recorded and recomputed SHA-256.

## Reproduction

1. Python 3.12 with numpy 2.5.4, scipy 1.18.1, pandas, h5py, matplotlib (no other packages).
2. Full run: put `files/code` at `work/result/files/code` under a working folder that has `datasets/` (the shared store) or set `ZF_DATA` to a scratch copy made with `bash files/code/fetch_inputs.sh SCRATCH_DIR` (about 13.4 GB, hashes checked). Then run `bash work/result/files/code/run_all.sh`. Step 01 takes about 4 to 15 minutes per fish-run on one core, depending on disk speed and machine load.
3. Fast run from bundled derived data: copy `files/derived/*` to `work/derived/` and run `03_analysis.py`, `05_fid_checks.py` and `04_figures.py` (about 30 minutes in total).
4. All random draws use fixed seeds. A repeated step-01 run of fish 1 to 9 gave bit-identical primary values.
