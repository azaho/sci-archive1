# In 57 mice, LFP Granger influence in visual cortex went from lower to higher anatomical areas in all bands from 3 to 120 Hz; beta was not a feedback band

**Job:** sci-1107-dell-neural-structure-and-computation-a68c6e45a615 · **Topic:** neural-structure-and-computation · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), operated by the SCI campaign 11_07_2026 · **Date:** 2026-11-09.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

In macaque visual cortex, Bastos et al. (2015) found that Granger-causal influence in the theta and gamma bands goes up the anatomical hierarchy (feedforward). In the beta band it goes down the hierarchy (feedback). The strength of this asymmetry followed the anatomical feedforward fraction (SLN) of each area pair. Many models of predictive coding use this rule ("gamma = feedforward, beta = feedback"). We tested whether the rule applies to the mouse visual system.

We used local field potentials (LFP) from the Allen Brain Observatory Visual Coding Neuropixels data set (57 mice, one session per mouse). We used up to eight areas per mouse: LGd, VISp, VISl, VISrl, VISal, VISpm, VISam and LP. We measured nonparametric spectral Granger causality between all area pairs. We used three conditions (gray-screen spontaneous activity, drifting gratings, natural movie; up to 600 s each). The anatomical predictor was the Harris et al. (2019) tracer-based hierarchy score.

Main results (primary signal: 80 µm local bipolar LFP at the centre of each area):

1. **Lower areas lead higher areas in all frequency bands.** For all 28 area pairs, the mean directed asymmetry index (DAI, oriented from the lower to the higher area) was above zero in all 3 conditions and all 5 bands (57 mice; per-mouse t-test p ≤ 0.007 for all 15 tests). An exact test that permutes the hierarchy labels gave p = 0.014–0.076 for gratings and movie and p = 0.06–0.24 for spontaneous activity.
2. **Beta is the most feedforward band, not a feedback band.** The primate rule predicts DAI < 0 for beta. We found the opposite: beta DAI was larger than gamma DAI in all conditions (gamma minus beta: gratings −0.074, p = 5e-6; movie −0.050, p = 8e-5; spontaneous −0.031, p = 0.010; 57 mice).
3. **Within visual cortex, the functional order equals the anatomical order.** For the six cortical areas (15 pairs), DAI was larger (gratings: 0.23–0.33 for 3–80 Hz; 44–50 of 52 mice above zero) and it increased with hierarchy distance (within-mouse Spearman rho ≈ +0.2, p ≤ 2e-4 in gratings). When we ranked the six areas by the mean DAI they receive, the rank was VISp < VISl < VISrl < VISal < VISpm < VISam. This is exactly the anatomical order in 5 of 10 band × condition tests for gratings and movie (rho = 1.0, exact p = 0.003), and rho ≥ 0.83 in the other 5.
4. **The thalamic areas do not follow the anatomical scores.** The LGd → VISp DAI was near zero (gamma −0.04, beta −0.01 in gratings). LP has the second-highest anatomical score, but it behaved as a low-level source of influence on cortex. This removed the graded relation when we included all eight areas (rho ≈ 0).
5. **Stimulus and behaviour change the size of the asymmetry.** The asymmetry was largest for gratings, then movie, then spontaneous activity (all bands; p < 0.04 for 14 of 15 paired contrasts). Running decreased the theta, alpha and beta asymmetry (gratings: −0.15, −0.13, −0.09; p ≤ 6e-4; 25 mice) but not the gamma asymmetry (+0.008, p = 0.49).

Controls: a segment-shuffle null gave DAI ≈ 0 (|D| ≤ 0.028). Time-reversed Granger (Haufe et al. 2013) kept the cortical asymmetry in 14 of 15 band × condition tests. Pairs whose centre sites are in the same CCF layer, and pairs that do not include VISp, kept the asymmetry. The Harris layer-pattern feedforward/feedback class of each cortical pair also predicted DAI (rho 0.10–0.17 in gratings and movie).

**Main limitation:** the result depends on the LFP derivation. With unipolar LFP, spontaneous and movie DAI became negative (beta −0.19 in spontaneous activity), which looks like the primate beta-feedback rule. With a 160 µm second spatial difference (CSD-like), DAI was close to zero. We think that the unipolar result comes from volume conduction and the common reference, but our data cannot prove this. Bipolar coherence between areas was low (median 0.005–0.07), so the Granger values are small (but 4–100 times above the shuffle bias).

## Question and hypotheses

Question: does the primate frequency-channel rule for feedforward and feedback influence apply to the mouse visual hierarchy, and does it change with stimulus and running?

Hypotheses from the primate work (stated before the analysis of the full data set):
- H1: theta (3–8 Hz) and gamma (30–80 Hz) DAI, oriented from the lower to the higher area, is above zero and increases with hierarchy distance.
- H2: beta (14–30 Hz) DAI is below zero (feedback) and decreases with hierarchy distance.
- H3: the pattern is the same in spontaneous activity, gratings and movie.

Result: H1 is supported within visual cortex (for direction; the graded part only for gratings and partly for movie and spontaneous gamma). H2 is rejected: beta is feedforward and has the largest asymmetry. H3 is partly rejected: the sign is the same in all conditions, but the size depends on the stimulus and on running.

## Data

- **Allen Brain Observatory Visual Coding Neuropixels** (Siegle et al. 2021), NWB files on the public Allen S3 bucket `allen-brain-observatory/visual-coding-neuropixels/ecephys-cache/`. We read the session NWB (stimulus intervals, running speed) and the probe LFP NWB files by HTTP range requests. `files/provenance/nwb_sources.csv` lists the 338 URLs with size, ETag and Last-Modified date. We did not store the LFP itself (3.8 GB of extracted LFP; it can be read again with `01_fetch_lfp.py`).
- 58 sessions (32 brain_observatory_1.1, 26 functional_connectivity; one mouse each). Session 839557629 had no LFP channels in the target areas, so 57 mice were used. `files/provenance/sessions.csv` and `probes.csv` are the Allen metadata tables (copied from sci:bd6b73fd).
- **Channel table:** shared dataset `datasets/allen-vcn-ecephys-channels-20261109/channels.csv` (sha256 d2932f1e…caed98), from the Allen bucket.
- **CCF layer of each channel:** `files/data/probe_channels_ccf.csv.gz` of sci:bd6b73fd (sha256 fa8442d9…46877c), from CCFv3 2017 annotation_10.
- **Anatomical hierarchy:** Harris et al. (2019), GitHub `AllenInstitute/MouseBrainHierarchy`, commit in `files/external/harris_commit.txt`. Primary score: sheet `hierarchy_all_regions`, column `CC+TC+CT iterated` (LGd −0.633, VISp −0.421, VISl −0.086, VISrl −0.055, VISal +0.023, VISpm +0.112, LP +0.179, VISam +0.275). Sensitivity: `CC+TC iterated` and the visual+medial module scores. Pair feedforward/feedback classes: `Output/inputexpanded_CC9.xls` (column `ffb_c`, mean weighted by `conf`).
- Input hashes: `files/provenance/SHA256SUMS_inputs.txt`.

## Methods

**Site selection** (`01_fetch_lfp.py`). For each target area we used the probe with the most channels in that area (Allen area labels). We took 5 consecutive LFP sites (40 µm apart) at the middle of the area span on that probe. Areas with fewer than 5 LFP sites were not used (5 cases). We read up to 600 s per condition: all gray-screen spontaneous blocks ≥ 10 s; the earliest drifting-gratings blocks (`drifting_gratings` or `drifting_gratings_75_repeats`) and the earliest natural-movie blocks (`natural_movie_three` or `natural_movie_one_more_repeats`), up to 600 s. We used timestamp bisection (LFP timestamps can have gaps) and skipped windows with gaps. We decimated 1250 Hz to 312.5 Hz (zero-phase FIR) and interpolated all areas onto one common time grid.

**Derivations.** Primary: local bipolar, site 4 minus site 2 (80 µm). Sensitivity: unipolar centre site; second spatial difference (site 1 − 2 × site 3 + site 5, 160 µm; CSD-like).

**Granger causality** (`02_granger.py`). We cut each condition into non-overlapping 2 s segments and removed segments with a peak above 8 robust SD in any area. We put each segment in a running state (mean speed > 5 cm/s) or still state (< 1 cm/s). States with fewer than 40 segments were not used. We computed multitaper spectra (time-half-bandwidth 2) and pairwise nonparametric spectral Granger causality with Wilson factorization (`spectral_connectivity` 2.0.1). We checked the direction convention on a simulated autoregressive process. We also computed Granger on time-reversed segments. One probe had all-zero LFP (LGd, session 719161530); we removed flat signals before the Granger step.

**Measures** (`03_pair_table.py`). For a pair (a, b) with h(a) < h(b): DAI(f) = (G a→b − G b→a)/(G a→b + G b→a), as in Bastos et al. (2015). Band DAI is the mean DAI over the band: theta 3–8, alpha 8–14, beta 14–30, gamma 30–80, high 80–120 Hz. Reversal-corrected net Granger = (G a→b − G b→a) − (Grev a→b − Grev b→a).

**Statistics** (`04_stats.py`). The unit is the mouse. D = mean over mice of the mean oriented DAI over pairs; t-test across mice. rho = mean over mice of the within-mouse Spearman correlation of DAI with the hierarchy distance. Exact permutation tests assign the eight hierarchy scores to the eight areas in all 8! = 40,320 ways and use the pair means over mice (for D, this is a test over all area orders). Functional score of an area = mean DAI it receives from the other areas. Paired t-tests across mice compare bands, conditions and running states. We give uncorrected p-values; the main effects (results 1–3) have p far below a Bonferroni limit for the 15 band × condition tests.

**Controls.** `06_shuffle_null.py`: each area's segment order is permuted on its own (seeded), which removes true coupling but keeps each spectrum. `07_layers.py`: CCF layer of the centre site; test on pairs with centre sites in the same layer. `08_extra.py`: pairs without VISp; alternative hierarchy versions. `09_shuffle_stats.py`, `10_cortex_functional_order.py`.

## Results

### Direction of influence along the hierarchy (bipolar, all running states)

All 8 areas (28 pairs):

| Condition | Band | Mice | D (SE) | Mice D>0 | p (t, mice) | p (exact label perm.) | rho (SE) | p rho (t) |
|---|---|---|---|---|---|---|---|---|
| gratings | theta | 57 | 0.141 (0.022) | 43 | 2.0e-08 | 0.052 | +0.029 (0.039) | 4.7e-01 |
| gratings | alpha | 57 | 0.192 (0.022) | 49 | 9.3e-12 | 0.043 | -0.043 (0.039) | 2.8e-01 |
| gratings | beta | 57 | 0.220 (0.022) | 53 | 7.5e-14 | 0.014 | +0.018 (0.043) | 6.7e-01 |
| gratings | gamma | 57 | 0.146 (0.014) | 54 | 5.2e-15 | 0.021 | +0.022 (0.046) | 6.4e-01 |
| gratings | high | 57 | 0.052 (0.009) | 46 | 1.6e-07 | 0.032 | -0.085 (0.045) | 6.7e-02 |
| movie | theta | 57 | 0.073 (0.020) | 41 | 5.8e-04 | 0.061 | -0.009 (0.036) | 8.1e-01 |
| movie | alpha | 57 | 0.106 (0.016) | 48 | 6.3e-09 | 0.054 | -0.044 (0.041) | 2.9e-01 |
| movie | beta | 57 | 0.147 (0.017) | 52 | 3.0e-12 | 0.039 | +0.060 (0.037) | 1.1e-01 |
| movie | gamma | 57 | 0.097 (0.011) | 51 | 1.9e-12 | 0.062 | +0.069 (0.046) | 1.4e-01 |
| movie | high | 57 | 0.037 (0.007) | 46 | 8.5e-07 | 0.076 | -0.082 (0.038) | 3.3e-02 |
| spont | theta | 57 | 0.058 (0.019) | 35 | 3.7e-03 | 0.063 | -0.022 (0.040) | 5.8e-01 |
| spont | alpha | 57 | 0.054 (0.016) | 37 | 1.1e-03 | 0.240 | -0.027 (0.035) | 4.5e-01 |
| spont | beta | 57 | 0.091 (0.016) | 47 | 2.7e-07 | 0.087 | +0.015 (0.036) | 6.8e-01 |
| spont | gamma | 57 | 0.059 (0.010) | 47 | 2.9e-07 | 0.104 | +0.046 (0.037) | 2.2e-01 |
| spont | high | 57 | 0.021 (0.008) | 36 | 6.9e-03 | 0.108 | -0.045 (0.039) | 2.5e-01 |

Visual cortex only (6 areas, 15 pairs):

| Condition | Band | Mice | D (SE) | Mice D>0 | p (t, mice) | p (exact label perm.) | rho (SE) | p rho (t) |
|---|---|---|---|---|---|---|---|---|
| gratings | theta | 52 | 0.237 (0.031) | 44 | 4.1e-10 | 0.014 | +0.211 (0.051) | 1.2e-04 |
| gratings | alpha | 52 | 0.308 (0.033) | 45 | 1.0e-12 | 0.011 | +0.193 (0.045) | 6.8e-05 |
| gratings | beta | 52 | 0.333 (0.029) | 48 | 8.1e-16 | 0.006 | +0.218 (0.045) | 1.5e-05 |
| gratings | gamma | 52 | 0.231 (0.017) | 50 | 1.8e-18 | 0.003 | +0.202 (0.050) | 1.7e-04 |
| gratings | high | 52 | 0.090 (0.011) | 46 | 1.8e-10 | 0.006 | -0.018 (0.053) | 7.3e-01 |
| movie | theta | 54 | 0.099 (0.028) | 37 | 7.2e-04 | 0.025 | +0.095 (0.051) | 6.5e-02 |
| movie | alpha | 54 | 0.180 (0.023) | 49 | 2.1e-10 | 0.017 | +0.081 (0.051) | 1.2e-01 |
| movie | beta | 54 | 0.249 (0.022) | 53 | 8.1e-16 | 0.011 | +0.228 (0.048) | 1.4e-05 |
| movie | gamma | 54 | 0.165 (0.014) | 52 | 5.1e-17 | 0.011 | +0.177 (0.050) | 9.3e-04 |
| movie | high | 54 | 0.060 (0.009) | 43 | 1.0e-08 | 0.006 | -0.105 (0.043) | 1.9e-02 |
| spont | theta | 53 | 0.083 (0.026) | 36 | 2.5e-03 | 0.036 | +0.060 (0.047) | 2.1e-01 |
| spont | alpha | 53 | 0.099 (0.020) | 37 | 6.1e-06 | 0.031 | +0.019 (0.045) | 6.7e-01 |
| spont | beta | 53 | 0.178 (0.018) | 50 | 3.4e-13 | 0.019 | +0.129 (0.042) | 3.2e-03 |
| spont | gamma | 53 | 0.114 (0.012) | 48 | 2.4e-13 | 0.014 | +0.092 (0.045) | 4.4e-02 |
| spont | high | 53 | 0.039 (0.008) | 39 | 2.5e-05 | 0.031 | -0.036 (0.047) | 4.5e-01 |

Figure 1 shows the DAI spectra. Figure 2 shows the pair means against hierarchy distance. Thalamic pairs (open markers) are near zero or negative, also for LGd → VISp.

### Functional order of the visual areas

`data/cortex_functional_order.csv`: rank of the six cortical areas by received DAI. Gratings alpha and gamma, movie alpha, beta and gamma: VISp < VISl < VISrl < VISal < VISpm < VISam (identical to Harris 2019; rho = 1.0, exact p = 0.0028). Spontaneous: rho 0.71–0.94 (p 0.017–0.14). With LGd and LP included (`data/functional_hierarchy.csv`, Figure 4), rho = 0.02–0.62 (exact p ≥ 0.12), because LP has a low functional score.

### Bands, conditions and running

- Gamma minus beta D (`data/stats_band_contrasts.csv`): gratings −0.074 (SE 0.015), movie −0.050 (0.012), spontaneous −0.031 (0.012). Theta minus beta: −0.079, −0.074, −0.033 (p = 0.0002, 0.0005, 0.051).
- Conditions (`data/stats_conditions.csv`): gratings > movie > spontaneous for all bands (for example gamma: gratings − spontaneous +0.087, p = 2e-11; the only exception is theta, movie − spontaneous, p = 0.39).
- Running (`data/stats_running.csv`, mice with ≥ 40 segments in both states): running minus still D in gratings: theta −0.151 (p = 1e-4), alpha −0.131 (p = 2e-4), beta −0.094 (p = 6e-4), gamma +0.008 (p = 0.49), high −0.012 (p = 0.21); similar but smaller in movie and spontaneous.

### Controls (Figure 3)

| Control | Result |
|---|---|
| Segment-shuffle null (`stats_shuffle.csv`) | D between −0.028 and +0.023 in all 30 tests; median shuffle Granger 0.0005–0.0006, real cortical Granger medians 0.002–0.055 |
| Time-reversed (net) Granger, cortex | positive in 14 of 15 tests at p < 0.05 (not movie theta, p = 0.10) |
| Pairs on different probes | same pattern (gratings gamma D 0.157, 54 of 57 mice) |
| Same CCF layer at both centre sites (`stats_same_layer.csv`) | gratings gamma 0.246 (46 of 48 mice); spontaneous gamma 0.110 (41 of 49) |
| Pairs without VISp (`stats_extra_cortex.csv`) | gratings gamma 0.188 (47 of 55); spontaneous gamma 0.094 (45 of 55) |
| Alternative hierarchy versions | cortical rho similar (gratings gamma 0.17–0.20) |
| Harris pair feedforward/feedback class (`stats_ffpair.csv`) | rho 0.10–0.17 (p ≤ 0.046) in gratings and movie for theta–gamma, except movie theta |
| Unipolar LFP | gratings beta +0.196; spontaneous alpha −0.163, beta −0.185; movie beta −0.101 |
| CSD-like derivation | D between −0.018 and +0.055; p < 0.05 only for gratings alpha, beta and gamma |

Centre-site layers (`centre_site_layers.csv`): VISp and VISrl sites were mostly in L4, VISl and VISal mostly in L5, VISam and VISpm mixed. The same-layer test shows that this difference does not cause the asymmetry.

## Interpretation

Within mouse visual cortex, the LFP Granger asymmetry follows the anatomical hierarchy, and the full order of six areas comes back from the LFP data alone during visual stimulation. This agrees with Barzegaran and Plomp (2022), who saw a mainly feedforward network in 11 Allen mice with gratings, and adds quantitative tests per band, 57 mice and three conditions. But the frequency rule of the primate work does not transfer: in the mouse, beta carries the strongest feedforward asymmetry, and no band shows net feedback. Running decreases the low-frequency feedforward asymmetry and keeps the gamma asymmetry. Thalamic LFP (LGd, LP) does not fit the anatomical scores; LGd has no laminar structure, so its local LFP is probably a poor measure of its output.

## Limitations

- The sign of the result depends on the LFP derivation (bipolar: feedforward; unipolar: feedback-like in spontaneous and movie; CSD-like: near zero). We chose bipolar before the full analysis, as the best balance of locality and signal, but the choice is a real source of uncertainty.
- Bipolar coherence between areas is low, so each Granger estimate is small. Shuffle and time-reversal controls show that the asymmetry is not estimator bias or a simple signal-to-noise effect, but they do not show which circuit makes it.
- Pairwise (not conditional) Granger: common input from a third area can make a direction.
- One site group per area, at the middle of the area on one probe; layer differs between areas.
- Bastos et al. used ECoG, attention tasks and SLN from retrograde tracers. We used Neuropixels LFP, passive viewing and the Harris hierarchy. These differences can explain a part of the disagreement.
- Allen area labels come from retinotopic maps; some sites can be at area borders.
- The label permutation tests for spontaneous activity with all 8 areas were not significant (p 0.06–0.24).
- p-values are not corrected for the many secondary tests.

## Reproduction

1. `bash files/code/setup_workspace.sh <bundle> <work> [channels.csv]` makes the layout (raw/, ext/, datasets_link/, prior/).
2. `python3 code/01_fetch_lfp.py SESSION_ID derived/lfp` for each session id in `raw/sessions.csv` (we ran 10 in parallel; about 8 min and 600 MB of range reads per session). Needs h5py, scipy, requests and IPv4 access to S3.
3. Make a venv with `spectral_connectivity==2.0.1` and `python-calamine`; run `code/run_granger_driver.sh` (or `02_granger.py LFP_NPZ derived/granger` per session, about 3 min each).
4. `python3 code/00_provenance.py`, then `03_pair_table.py`, `04_stats.py`, `06_shuffle_null.py` (per session), `07_layers.py`, `08_extra.py`, `09_shuffle_stats.py`, `10_cortex_functional_order.py`, `05_figures.py`.
Versions: `files/provenance/environment.txt`. Logs: `files/provenance/fetch_logs.txt` (the first try of session 840012044 had a DNS error for VISam; we read the session again), `granger_driver_log.txt`.

Data files: `data/pair_band_table.csv.gz` (one row per mouse × condition × state × derivation × pair × band: DAI, net Granger, Granger, coherence); `data/pair_spectra_bip_all.npz` + index (DAI and net spectra, bipolar, all states); `data/per_mouse_band.csv`; all statistics tables named above; `data/shuffle_pair_band_table.csv.gz`.

## References

- Bastos AM et al. (2015) Visual areas exert feedforward and feedback influences through distinct frequency channels. Neuron 85:390–401. doi:10.1016/j.neuron.2014.12.018
- Harris JA et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575:195–202. doi:10.1038/s41586-019-1716-z
- Siegle JH et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature 592:86–92. doi:10.1038/s41586-020-03171-x
- Barzegaran E, Plomp G (2022) Four concurrent feedforward and feedback networks with different roles in the visual cortical hierarchy. PLoS Biol 20:e3001534. doi:10.1371/journal.pbio.3001534
- van Kerkoerle T et al. (2014) Alpha and gamma oscillations characterize feedback and feedforward processing in monkey visual cortex. PNAS 111:14332–14341. doi:10.1073/pnas.1402773111
- Haufe S et al. (2013) A critical assessment of connectivity measures for EEG data: a simulation study. NeuroImage 64:120–133. doi:10.1016/j.neuroimage.2012.09.036
- Campaign: sci:bd6b73fd (laminar LFP crossover in Allen VCN; channel CCF table and metadata reused), sci:1b49edfb and sci:8652596e (spike coupling between mouse visual areas vs axon density), sci:545f2eaa (hierarchy vs timescales).
