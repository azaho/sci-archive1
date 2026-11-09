# In mouse postsubiculum (31 mice), head-direction cells connect slightly more often to fast-spiking cells with similar tuning; a synthetic-connection control shows the bias is not detection power

## Summary

We used the postsubiculum (PoSub) recordings of Duszkiewicz et al. (2024), which are on DANDI:000939 and have 31 mice. We identified putative excitatory connections from head-direction (HD) cells to fast-spiking (FS) cells with the cross-correlogram (CCG) rule of the original paper. We then tested whether the probability of a connection increases with the similarity of the wake HD tuning curves of the two cells ("like-to-like" wiring).

Spike-timing detection has a known problem: the statistical power to detect a connection depends on how much the two cells fire together, and co-tuned cells fire together more. Thus a like-to-like pattern can come from the detector and not from the wiring. To measure this effect, we added synthetic connections with a known efficacy to every HD-to-FS pair in the real spike trains and applied the same detection rule. These "injection nulls" give the like-to-like pattern that wiring with no tuning preference would produce after detection.

Main results:

1. We found 1,070 putative connections in 23,813 HD-to-FS pairs (4.5%; 1,533 HD cells, 414 FS cells, 31 mice). The connection rate increased with tuning similarity: rate ratio (RR) 1.10 per SD of similarity (95% mouse-bootstrap CI 1.05-1.15), with probe distance as a covariate and with one fixed effect for each FS cell. The rate was 3.7% in the lowest two similarity deciles and 5.2-6.1% in the highest two.
2. Detection power does not cause this pattern. Similarity-blind synthetic connections gave RR 0.96-0.99 (fixed efficacy) and 1.00-1.03 (efficacy that scales with FS activity). The observed RR was 1.07-1.15 times the null RR in all six null scenarios (all bootstrap CIs above 1). A model with a per-pair detection-probability offset gave RR 1.06-1.17 per SD.
3. The detected inputs of an FS cell predict its tuning only weakly. For the 145 FS cells with 3 or more detected HD inputs (30 mice), the correlation between the FS tuning curve and the summed tuning of its inputs was 0.14 (CI 0.09-0.21), against 0.01-0.05 for detection-weighted random input sets. The difference is clear, but only 7-10% of FS cells were above the 95th percentile of their own null.
4. The bias held for a cross-validated similarity measure, for similarity in a second open field, for connections detected only in wake, and for both probe cohorts (angled probes: 17 mice; vertical probes: 14 mice, CI touches 1 against one null). It was weaker and uncertain for connections detected only in NREM sleep. It was absent in the third of FS cells with the strongest HD tuning (RR 1.00, CI 0.88-1.11). Connection strength did not change with similarity (Spearman rho -0.01 to 0.06). 21 of 31 mice had a per-mouse RR above the null.
5. The bias was present both in connections with a one-sided CCG peak and in connections with excess counts at negative lags too. Thus, shared fast input to both cells can be a part of the cause. Spike timing alone cannot separate this from direct synapses.

The bias is small. The data agree with the view of Duszkiewicz et al. (2024) that FS tuning comes from local HD input. But the inputs are not a fully random sample of local HD cells: a weak preference for co-tuned partners is present.

![Main result](files/figures/fig1_main.png)

## Question and prior work

Duszkiewicz et al. (2024, Nat. Neurosci., doi:10.1038/s41593-024-01588-5) showed that PoSub FS interneurons have HD tuning with the same Fourier signature as the local HD cells. They proposed that FS tuning comes from local excitatory input. Their model used random weighted sums of HD inputs. They detected putative HD-to-FS connections with CCGs. They did not test whether the probability of connection depends on the tuning of the two cells, or whether the identified inputs of one FS cell predict its tuning curve. (We read their paper and their figure code on figshare 24921252 to confirm this.)

Like-to-like wiring between excitatory cells and interneurons is a general question in cortex (for example, in MICrONS mouse visual cortex; see campaign publication sci:sha256:c59a7cc9c394931da48264dbdd64f4dd2ef21ea50f820313c35558be9be14d07). A campaign study of rat grid cells (sci:sha256:2fbb19dfa2e2234dfa281f1b5e38f2f7db7a5b739e1b3eab123c787068d68706) found much stronger phase-dependent CCG connections between grid cells. Spike-timing studies seldom measure how detection power changes with co-firing. This study adds that control.

## Data

- DANDI:000939, version 0.261016.2310, "Large-scale recordings of head direction cells in mouse postsubiculum" (Duszkiewicz, Skromne Carrasco, Peyrache), CC BY 4.0. One session for each of 31 mice; 64-channel linear H5 probes; open field (square, and a triangle for 20 mice), two home-cage sleep epochs, and an optogenetic epoch in 9 mice.
- We read only the units table (spike times, the authors' cell labels `is_head_direction`, `is_fast_spiking`, `is_excitatory`, mean waveforms), electrode positions, epochs, sleep scoring and head direction with HTTP range reads (60-150 MB per 13-30 GB file). We did not read raw voltage or LFP data.
- `files/provenance/dandi000939_assets.csv` gives the asset ID, path, size, DANDI SHA-256, S3 URL, and the SHA-256 of each local extract.
- The MATLAB detection code is in figshare doi:10.6084/m9.figshare.24921252 (CC BY 4.0). We ported the detection rule to Python.

## Methods

**Cell classes.** We used the cell labels of the dataset. HD cells are excitatory cells with significant HD tuning; FS cells are fast-spiking putative interneurons.

**Tuning curves.** We used samples from the first open-field epoch when speed was above 2 cm/s. We used 60 bins of 6 degrees and circular Gaussian smoothing (SD 1 bin) of counts and occupancy. Tuning similarity is the Pearson correlation of the two curves. The cross-validated similarity correlates the first-half curve of one cell with the second-half curve of the other cell, and the reverse.

**Connection detection (same rule as Duszkiewicz et al. 2024).** For each ordered pair (excitatory pre, FS post) we counted FS spikes at lags of +-25 ms in 0.2-ms bins. We excluded spikes in optogenetic epochs. The baseline is the hollowed-Gaussian convolution of Stark and Abeles (2009): window 41 bins, hollow fraction 0.6, reflected edges. A connection requires two consecutive bins above the Poisson bound (alpha 0.01) of the window maximum of the baseline at 0-2 ms. It also requires peak latency above 0.5 ms and no significant peak at negative lags. We also applied the same rule to presynaptic spikes from wake epochs only and from NREM epochs only.

**Statistical model.** We used conditional Poisson regression (equal to a multinomial logit) with one stratum for each FS cell. This removes all FS-cell effects (rate, isolation, depth, the number of candidate partners). Covariates were tuning similarity and the distance between the peak channels of the two cells, both standardised. For 95% CIs we resampled mice with replacement (1,000 resamples).

**Synthetic-connection injection (detection null).** For each of the 23,813 HD-to-FS pairs we added synthetic FS spikes after presynaptic spikes at latency 1.0 ms (SD 0.2 ms, clipped to 0.6-1.8 ms). Then we applied the detection rule again. We used two efficacy models: (a) fixed: each HD spike causes an FS spike with probability q; (b) FS-gain: the probability is q multiplied by the FS count within +-10 ms of the HD spike, divided by its mean (the transmission scales with FS activity). We used q = 0.004, 0.008, 0.016, which are the 25th, 50th and 75th percentiles of the excess spikes per presynaptic spike of the detected connections. The injected pairs are detected at rates of 40-82%. If wiring ignores tuning, the observed connections are a sample of pairs with these detection probabilities. Thus, the RR of the detection outcome is the null RR. We compared observed and null RR with a joint mouse bootstrap. As a second method, we fitted the observed connections with an offset log(p_det), where p_det is a smoothed per-pair detection probability (logistic fit of the injection outcome on baseline count, presynaptic spikes, FS rate, distance and similarity).

**Input-sum test.** For each FS cell with 3 or more detected HD inputs, we summed the z-scored tuning curves of the inputs and correlated the sum with the FS tuning curve. Null sets have the same size and come from all HD cells of the session (uniform), or are drawn with probability proportional to p_det (detection-weighted). We used 2,000 draws for each FS cell.

**Peak shape.** For each detected connection we calculated the excess over baseline at +0.4 to +2.0 ms and at -2.0 to -0.4 ms, and the number of significant bins at 0-4 ms. We then refitted the model separately for one-sided peaks (no excess at negative lags; 701 connections) and two-sided peaks (365 connections; 4 connections had no excess on either side).

## Results

### 1. Connection rate and tuning similarity

| Measure | RR per SD (95% CI) |
|---|---|
| Observed, similarity only | 1.11 (1.06-1.16) |
| Observed, similarity + distance | 1.10 (1.05-1.15) |
| Null, fixed efficacy q = 0.004 / 0.008 / 0.016 | 0.96 / 0.96 / 0.99 |
| Null, FS-gain efficacy q = 0.004 / 0.008 / 0.016 | 1.03 / 1.01 / 1.00 |
| Observed / null, fixed efficacy | 1.15 (1.10-1.20) / 1.14 (1.09-1.19) / 1.12 (1.06-1.17) |
| Observed / null, FS-gain efficacy | 1.07 (1.02-1.11) / 1.10 (1.04-1.14) / 1.11 (1.05-1.15) |
| Detection-offset model, fixed efficacy | 1.17 (1.11-1.21) / 1.15 (1.09-1.20) / 1.11 (1.05-1.16) |
| Detection-offset model, FS-gain efficacy | 1.06 (1.01-1.11) / 1.08 (1.03-1.13) / 1.10 (1.04-1.14) |

(Null rows use similarity + distance. `files/results/results_null.json` has all values and p-values.)

The fixed-efficacy null is below 1 because co-tuned pairs have a higher CCG baseline, and a fixed number of extra spikes is then less significant. The FS-gain null is near 1. In both cases detection does not make co-tuned connections easier to find, so the observed bias is not a detection artefact.

A simple regression that adds the baseline count and the number of presynaptic spikes as covariates gives RR 0.94 (0.87-1.01). We do not use this model. The baseline count in the 0.5-2 ms window is partly a result of the tuning similarity (co-tuned cells fire together), and the smoothing kernel also includes the synaptic peak. Thus it is not a clean nuisance variable. The injection test measures its effect on detection directly.

### 2. Input sums

| Null | Mean null r | Observed - null (95% CI) | FS cells above own 95th percentile |
|---|---|---|---|
| Uniform random HD sets | 0.04 | 0.10 (0.05-0.16) | 7% |
| Detection-weighted, fixed q = 0.008 | 0.01 | 0.13 (0.08-0.19) | 10% |
| Detection-weighted, FS-gain q = 0.008 | 0.05 | 0.10 (0.04-0.15) | 8% |

Observed mean r = 0.14 (0.09-0.21), 145 FS cells, 30 mice. Most FS tuning is not predicted by the few inputs that we can detect (a median of 5 per FS cell). Most inputs are probably not detected.

### 3. Robustness and generalisation

![Robustness](files/figures/fig2_robust.png)

| Check | Connections / pairs (mice) | Observed RR | Obs/null fixed | Obs/null FS-gain |
|---|---|---|---|---|
| Main | 1070 / 23813 (31) | 1.10 (1.05-1.15) | 1.14 (1.09-1.19) | 1.10 (1.04-1.14) |
| Cross-validated similarity | 1070 / 23813 (31) | 1.09 (1.04-1.14) | 1.14 (1.08-1.19) | 1.09 (1.03-1.14) |
| Similarity in second open field | 753 / 19543 (20) | 1.07 (1.01-1.12) | 1.11 (1.05-1.16) | 1.07 (1.01-1.12) |
| Wake-only detection | 1070* / 23813 (31) | 1.08 (1.02-1.13) | 1.11 (1.06-1.18) | 1.07 (1.01-1.13) |
| NREM-only detection | 1070* / 23813 (31) | 1.09 (1.00-1.16) | 1.13 (1.03-1.20) | 1.08 (0.99-1.15) |
| Angled-probe cohort | 684 / 18591 (17) | 1.11 (1.04-1.16) | 1.15 (1.08-1.20) | 1.11 (1.04-1.16) |
| Vertical-probe cohort | 386 / 5222 (14) | 1.09 (0.99-1.18) | 1.12 (1.03-1.21) | 1.06 (0.98-1.15) |
| FS tuning strength, low third | 443 / 7893 | 1.15 (1.06-1.24) | 1.17 (1.09-1.25) | 1.14 (1.06-1.23) |
| FS tuning strength, middle third | 344 / 8225 | 1.14 (1.06-1.26) | 1.18 (1.09-1.31) | 1.13 (1.05-1.25) |
| FS tuning strength, high third | 283 / 7695 | 1.00 (0.88-1.11) | 1.06 (0.93-1.19) | 1.00 (0.88-1.11) |
| One-sided CCG peaks (no negative-lag excess) | 701 | 1.07 (1.00-1.13) | 1.11 (1.04-1.17) | 1.07 (0.99-1.12) |
| Two-sided CCG peaks | 365 | 1.15 (1.04-1.26) | 1.19 (1.08-1.30) | 1.14 (1.03-1.25) |

*The count shows all-spike connections; wake-only and NREM-only detection found 820 and 657 connections. The interaction between similarity and FS tuning strength (mean vector length) was 0.95 per SD (0.89-1.01). Among detected connections, the CCG z-score, peak ratio and excess per presynaptic spike did not change with similarity (Spearman rho -0.03 to 0.06, p > 0.06). The per-mouse RR (descriptive) was above the FS-gain null in 21 of 31 mice (median RR 1.11).

## Interpretation

- HD-to-FS wiring in PoSub has a weak, detection-robust like-to-like bias: about 10% more connections per SD of tuning similarity. The connection rate in the most similar pairs is about 1.4 to 1.6 times the rate in the least similar pairs.
- The bias does not change connection strength. It is not present for the FS cells with the strongest tuning. Thus, a simple rule "sharper FS tuning comes from more co-tuned input" does not agree with these data.
- The FS tuning curve agrees only weakly with the sum of its detected inputs. This agrees with the view that FS cells pool many local HD inputs, most of which are not detected by CCGs.

## Limitations

- CCG connections are putative. Spike timing cannot separate direct synapses from shared fast input. The bias was at least as large in two-sided CCG peaks as in one-sided peaks. Thus, a part of it can come from shared input (for example from the anterior thalamus) and not from direct HD-to-FS synapses.
- The injection model adds spikes at one fixed latency distribution and assumes that the efficacy is independent of tuning similarity. It does not model spike-sorting loss of near-coincident spikes, or connections with longer latencies.
- The efficacy levels come from the detected connections. Weaker real connections, which we cannot detect, have unknown similarity dependence.
- Each mouse has one session. FS cells with fewer than 3 detected inputs are not in the input-sum test. The NREM-only and vertical-cohort estimates are imprecise.
- We used the dataset's cell labels and spike sorting without changes. We tested PoSub only. We did not test ADN, other species or other regions.

## Reproduction

All code is in `files/code`. It uses Python 3.12 with numpy, scipy, pandas, h5py, statsmodels and matplotlib (versions in `files/provenance/python_packages.txt`). The scripts write only to the current directory (or `HD_WORKDIR`). Do not run them inside the publication folder.

```bash
mkdir -p /scratch/hd && cd /scratch/hd
bash <publication>/files/code/run_all.sh
```

Steps: `01_fetch_dandi000939.py` (HTTP range extraction, about 1.1 GB of local npz files), `02_session.py` (CCGs, detection, tuning curves), `04_injection.py` (synthetic connections), `03_aggregate.py`, `05_null_compare.py`, `06_robust.py`, `08_peakshape.py`, `07_figures.py`. Random seeds are fixed. Bootstrap CIs can change in the third decimal with other library versions.

Derived evidence in `files/results`:

- `pairs_hd_fs_with_injection.csv.gz`: one row for each HD-to-FS pair: detection outputs for all/wake/NREM spikes, similarity measures, distance, rates, injection outcomes and smoothed detection probabilities.
- `units_all.csv`, `tuning_curves_6deg.csv.gz`: unit table and wake tuning curves.
- `results_main.json`, `results_null.json`, `results_robust.json`, `results_peakshape.json`, `decile_table.csv`, `per_mouse.csv`, `input_sum_*.csv`, `conn_shape.csv`.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-6f5868f4d600, topic neural-structure-and-computation, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- External data and attribution: see `files/NOTICE-external-data.md`.
