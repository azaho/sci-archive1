# In awake mice, putative LGN-to-V1 connections go mostly to fast-spiking layer 4 cells and follow retinotopy only weakly

Job: `sci-1107-dell-neural-structure-and-computation-037f22842a8f` (campaign 11_07_2026). Topic: neural structure and computation. Machine: dell. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a claim of personal authorship.

## 1. Question

Studies in the cat and the rabbit found rules for the monosynaptic connections from the dorsal lateral geniculate nucleus (LGN, LGd) to primary visual cortex (V1):

1. Connections occur mostly when the receptive fields (RFs) of the two cells overlap (Reid and Alonso 1995).
2. ON-centre LGN cells connect to ON subregions, and OFF cells to OFF subregions (Reid and Alonso 1995).
3. Fast-spiking (FS) interneurons in layer 4 receive more and stronger thalamic input than regular-spiking (RS) cells (Swadlow 2003).
4. The first spike of a thalamic burst, and spikes after long silence, have higher efficacy than spikes after a short interval (Swadlow and Gusev 2001). In the cat, a second spike after a short interval can also have higher efficacy (Usrey, Alonso and Reid 2000).
5. Thalamocortical efficacy changes with the alert state (Bereshpolova et al. 2011; Stoelzel et al. 2009 reported stability).

We tested which of these rules apply to the awake mouse. We used two public Allen Institute Neuropixels data sets that record LGd and V1 (VISp) at the same time. We used spike cross-correlograms (CCGs) to find putative monosynaptic connections. One data set gave the tests and the second data set gave an independent replication.

## 2. Data

| Data set | Sessions used | Mice | LGd units | VISp units | LGd-VISp pairs |
| --- | --- | --- | --- | --- | --- |
| Allen Brain Observatory Visual Coding Neuropixels (VCN) | 27 (all with >=5 LGd and >=10 VISp units) | 27 | 1,243 | 1,932 | 86,182 |
| Allen Brain Observatory Visual Behavior Neuropixels (VBN) | 43 (first such session of each mouse) | 43 | 1,153 | 2,598 | 68,309 |

We also used LP (lateral posterior nucleus) units as a control presynaptic population (VCN 1,395 units, 95,211 LP-VISp pairs; VBN 778 units, 46,376 pairs).

Unit filter: Allen `quality == good`, ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9 (VBN also `valid_data`). FS = waveform duration < 0.4 ms (20% of VCN and 17% of VBN VISp units). Layer: Allen CCF 2017 annotation (10 um) at the unit peak-channel CCF coordinate; if the label was not a VISp layer, a relative depth inside the VISp extent of the probe. RF centre: centroid of the 9 x 9 Gabor response map (0-250 ms, values above 50% of the peak after median subtraction), chi-square p < 0.001 for both units; the same code ran on both data sets (on VCN it agreed with the Allen `azimuth_rf`/`elevation_rf`, r = 0.78/0.75). ON/OFF index: (ON - OFF)/(ON + OFF) of baseline-subtracted full-field flash responses; "same sign" means |index| > 1/3 with equal sign in both units.

Spike times came from the session NWB files by HTTP range reads (only the LGd/VISp/LP units). The analysis window was the full visual-stimulus period (VCN: invalid intervals removed; optotagging excluded in both data sets).

## 3. Method

- CCG of every LGd (or LP) unit against every VISp unit in a session, +-50 ms, 0.5 ms bins.
- Baseline: partially hollow Gaussian convolution (SD 10 ms, hollow fraction 0.6; Stark and Abeles 2009).
- Detection (putative connection): peak in the 1-4 ms window above baseline with Poisson p < 0.001 (Bonferroni over 6 bins) and above the largest anticausal (-4 to -1 ms) bin with p < 0.0026.
- Efficacy: excess VISp spikes in 1-4 ms per 1000 presynaptic spikes. Relative gain: excess divided by the baseline count in the same window. Asymmetry: causal minus anticausal excess.
- Pair models: logistic regression (detected yes/no) with session fixed effects and log spike counts of both units (detection power), standard errors clustered by mouse. Mean efficacy and asymmetry: OLS with session fixed effects, clustered by mouse. Rates and means: 95% CI from a bootstrap over mice.
- Spike-class analysis (detected LGd-VISp connections only): we split presynaptic spikes into burst first spikes (>=100 ms silence, next ISI <= 4 ms), later burst spikes, and tonic spikes by preceding ISI (<10, 10-30, 30-100, >=100 ms). We also split by running speed (stationary < 0.5 cm/s, running > 5 cm/s). We pooled class CCGs over connections and bootstrapped over mice.
- Robustness: strict detection (p < 1e-5 and p < 1e-4), pairs on different probes only (VCN had 15,908 same-probe LGd-VISp pairs; VBN had none), and a sharp-peak detector with a narrow baseline (SD 3 ms). The pooled FS CCGs show a ~60 Hz rhythm (peaks near -14 and +18 ms, Figure 1), probably the LGN narrowband gamma (Saleem et al. 2017). The narrow baseline removes most of this rhythm, so only sharp causal peaks remain.

## 4. Results

### 4.1 Few pairs show a putative connection; most go to FS cells

| | VCN | VBN |
| --- | --- | --- |
| Detected LGd-VISp pairs | 415 / 86,182 (0.48%) | 355 / 68,309 (0.52%) |
| FS targets | 326 / 18,118 (1.8%) | 218 / 12,016 (1.8%) |
| RS targets | 89 / 68,064 (0.13%) | 137 / 56,293 (0.24%) |
| LP-VISp control (all targets) | 38 / 95,211 (0.04%) | 56 / 46,376 (0.12%) |
| Odds ratio FS vs RS (logistic, 95% CI) | 7.5 (5.5-10.3) | 4.1 (2.7-6.3) |
| FS layer 4 detection rate | 3.7% | 3.0% |
| FS units with >= 1 detected LGd input | 17% | 20% |
| RS units with >= 1 detected LGd input | 4.2% | 3.5% |
| Median peak lag, FS / RS target | 2.75 / 3.25 ms | 2.75 / 3.25 ms |
| Median efficacy of detected connections, FS / RS (per 1000 spikes) | 6.5 / 1.6 | 5.3 / 2.6 |

The FS preference stayed in all robustness variants (odds ratio 4-12, Figure 4). It also stayed for the threshold-free measures: mean asymmetry over all pairs was higher for FS targets by 0.26 (VCN, p = 0.003) and 0.19 (VBN, p = 0.03) excess spikes per 1000. Detected connections onto FS cells were also stronger than those onto RS cells (+6.5 per 1000 in VCN, +3.3 in VBN, both p < 0.001). The LP control gave a detection rate 4-12 times lower than LGd, and its pooled CCGs had no causal peak (Figure 1).

### 4.2 Layer 4 receives more detected input than layers 5 and 6

Relative to layer 4 targets, the odds ratio of a detected connection was 0.28 (L5) and 0.16 (L6) in VCN, and 0.39 (L5) and 0.39 (L6) in VBN (all p < 0.01). Layer 2/3 did not differ clearly from layer 4 (0.67 and 0.72, p > 0.3). The layer assignment comes from probe registration to the CCF and has an error of about one layer near boundaries, so the L2/3-versus-L4 contrast is weak.

### 4.3 Retinotopy has only a weak effect; ON/OFF sign match has no consistent effect

- RF distance: with the main detector, the odds ratio per 10 degrees of RF-centre distance was 0.85 (p = 0.15, VCN) and 0.88 (p = 0.06, VBN). With the sharp-peak detector it was 0.71 (p = 0.009) and 0.77 (p = 0.04). The FS detection rate fell from 2.8-3.5% at 0-10 degrees to 0.7-1.0% at more than 45 degrees (Figure 2). Detected connections still occurred at RF distances above 30 degrees. RF centres come from a coarse 10-degree Gabor grid, and FS RFs are large. Thus the data support a graded retinotopic preference, not an RF-overlap requirement as in the cat.
- ON/OFF sign: same-sign pairs did not have a consistent advantage. The odds ratio was 1.36 (p = 0.16) and 0.96 (strict) in VCN, and 1.87 (p = 0.06) and 2.02 (strict, p = 0.02) in VBN. Mean efficacy did not change with sign match in either data set. The flash index is a crude measure of ON/OFF subregions.

### 4.4 Spike history: spikes after 10-30 ms intervals are less effective

For detected connections, the relative gain of tonic spikes after a 30-100 ms interval was higher than after a 10-30 ms interval: ratio 1.23 (95% CI 1.14-1.29) in VCN and 1.26 (1.06-1.68) in VBN with the main baseline, and 1.14 (1.04-1.21) and 1.18 (1.03-1.50) with the sharp baseline. This agrees with short-term depression that recovers within about 100 ms.

The burst rule was not robust. With the main baseline, burst first spikes had 2.3 times (1.7-2.8) the efficacy of tonic spikes after >= 100 ms silence in VCN, and 1.4 times (0.97-2.2) in VBN. With the sharp baseline, the ratio was 0.97 (0.68-1.27) and 0.56 (0.26-1.17). Thus part of the burst advantage was broad co-firing, not a sharp synaptic effect. The sharp baseline can also remove part of a true burst effect, because the later burst spikes add post-synaptic spikes near the window. We cannot separate these two possibilities with these data. Results for spikes after < 10 ms intervals also changed with the baseline (Figure 3, data file `spikeclass_stats*.json`).

### 4.5 Running does not change the relative gain

Relative gain during running versus stationary periods: 0.88 (0.69-1.04) VCN and 0.96 (0.85-1.07) VBN with the main baseline; 1.13 (0.89-1.29) and 1.05 (0.90-1.17) with the sharp baseline. Absolute efficacy (excess spikes per presynaptic spike) was higher during running in VBN (1.7-1.9 times) and with the sharp baseline in VCN (1.24), because VISp cells fire more during running. We found no evidence of state-dependent depression of the thalamocortical gain. This agrees with the stability reported in the awake rabbit (Stoelzel et al. 2009).

## 5. Interpretation

In the awake mouse, the cat/rabbit rule that thalamic input goes preferentially to fast-spiking layer 4 interneurons generalizes and replicates in two independent data sets. The cat rule that connections need RF overlap and matched ON/OFF sign does not generalize in a strict form: the mouse data show a graded retinotopic preference and no consistent sign rule. Single LGN-to-V1 connections in the mouse are weak (median 0.5-0.7% excess spikes per presynaptic spike onto FS cells, 0.2-0.3% onto RS cells). This agrees with high convergence of many weak thalamic inputs onto each mouse V1 cell. Short-term depression at 10-30 ms intervals is a consistent dynamic rule; the burst advantage depends on the analysis method.

## 6. Limitations

- CCG peaks are putative connections. Correlated firing of neighbouring LGN cells (shared retinal input, ~60 Hz rhythm) can make a peak for a pair that has no direct synapse. The sharp-peak detector reduces but does not remove this risk.
- Detection depends on spike counts. FS cells fire more. We included log spike counts in all logistic models and also used threshold-free efficacy measures, but residual power differences can remain.
- FS/RS classification from waveform width is approximate (some Pvalb cells are broad, and some excitatory cells are narrow).
- Layer labels come from CCF registration of probe tracks; boundary errors are likely.
- RF mapping is coarse (10-degree grid, 20-degree Gabors). This weakens the retinotopy and sign tests. The ON/OFF index uses full-field flashes, not subregion maps.
- VCN and VBN use different stimuli, and VBN mice did a task. VCN sessions include several Cre lines; we did not test genotype effects.
- Only one session per mouse; no test across days.

## 7. Files

| Path | Content |
| --- | --- |
| `files/code/` | All analysis code (Python 3.12, numpy, scipy, pandas, statsmodels, h5py, requests, matplotlib). `run_all.sh` runs the full pipeline. |
| `files/results/vcn_pair_stats.json`, `vbn_pair_stats.json` | Aggregate rates, bootstrap CIs and model coefficients by target class, layer, RF distance and ON/OFF sign. |
| `files/results/spikeclass_stats.json`, `spikeclass_stats_sd3ms.json` | Spike-class efficacy with the main and the sharp baseline. |
| `files/results/sharp_kernel_print.txt`, `robustness_forest.csv` | Sharp-peak detector results and the robustness estimates of Figure 4. |
| `files/results/population_ccg.npz` | Pooled CCG sums by group (Figure 1). |
| `files/results/*_stats_print.txt` | Printed console output of the statistics scripts. |
| `files/figures/` | Figures 1-4 (PNG). |
| `files/provenance/` | Source URLs, sizes, ETags of the 70 NWB files, and SHA-256 hashes of the metadata tables. |
| `files/NOTICE_external_data.md` | Terms and attribution for the Allen Institute data, which this bundle does not contain. |

Record-level derived tables (per-unit tuning, per-pair CCG statistics, spike times) are not in this bundle, because the Allen Institute Terms of Use permit redistribution of derived works only for noncommercial purposes. `run_all.sh` regenerates them into a separate local scratch folder.

## 8. How to reproduce

```bash
export LGNV1_WORK=/path/to/scratch      # never the publication folder
cp -r files/code "$LGNV1_WORK/code"
# optional: point to local copies, otherwise the download script fetches them into $LGNV1_WORK/raw
export LGNV1_CCF_NRRD=$LGNV1_WORK/raw/annotation_10.nrrd
export LGNV1_VCN_CHANNELS=$LGNV1_WORK/raw/channels.csv
NPROC=8 bash "$LGNV1_WORK/code/run_all.sh"
```

The run reads about 4-5 GB by HTTP range requests from the public Allen S3 buckets (about 1-2 min per session), and the CCG step takes about 3-10 CPU-minutes per session. Compare the metadata hashes with `files/provenance/metadata_sources.csv` and the NWB ETags with `files/provenance/nwb_sources.csv`. The exact structure-ontology URL is `https://api.brain-map.org/api/v2/data/query.json?criteria=model::Structure,rma::criteria,[graph_id$eq1],rma::options[num_rows$eqall]` (the CSV uses `;` in place of `,` in this URL).

## 9. Related work in this campaign

- `cc2969a4`: in vivo cell-class connectivity from opto-tagged CCGs in the same Allen data sets (intracortical; this study adds the thalamocortical input).
- `6ea87a03`: LGd/LP versus cortex in Fano-factor quenching in VCN/VBN.
- `0dd17ccb`, `734b7b0e`, `63daa564`: area-level directed coupling and wiring in Allen and IBL data.
