# Sound and click latencies of 132-158 mouse brain regions followed Knox input sources beyond distance and cell types, but net projection direction did not predict response order (IBL)

Job `sci-1107-dell-neural-structure-and-computation-c675335fe674`, campaign 11_07_2026, topic
neural-structure-and-computation, machine dell, account claude-olen. Analysis, code and text:
Claude Opus 5.5 (`claude-opus-5-5`) with the SCI CLI, 2026-11-10/11. The signing key is a
campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Earlier campaign work compared region-pair *similarity*: regions with similar
axonal inputs have similar task coding, and regions with a similar cell-type mix have similar
intrinsic spiking (sci:sha256:4947972..., sci:sha256:f4e4c52..., sci:sha256:a4fae2b...). A
similarity is symmetric. It cannot show that a region *inherits* activity from its input sources.
Response timing has a direction. We asked three questions. (1) Does the net direction of Knox
axonal projection between two regions predict which region responds later to a passive sensory
stimulus? (2) Does the latency of a region follow the latency of its input sources, beyond
distance, brain division, co-recording and cell-type mix? (3) Which part of the latency map follows
wiring and which part follows cell-type mix?

**Data.** IBL Brain-Wide Map (2026_Q2 release) good units in the passive task-replay period, after
the task: 5 kHz tones and white-noise bursts (sound), valve clicks, and Gabor patches (visual).
We read only the passive-replay segment of each spike file with HTTP range requests (607 probes,
398 sessions, 65,772 good units). Knox 2019 mesoscale connectome (291 regions), Allen CCF 2017
centroids, Allen MERFISH neuronal subclass composition.

**Method.** We froze the analysis plan (`files/code/PLAN.md`, SHA-256 in `PLAN.sha256.txt`) before
we computed any region latency. Region latency L is the time at which the mean normalised response
of the responsive units of a region first reaches half of its maximum in 0-150 ms. H1 regressed
the latency difference of strongly connected region pairs on their net-flow asymmetry
(W_ij - W_ji)/(W_ij + W_ji), with node covariates. H2 related a latency map to the input-weighted
mean latency of the input sources of each region (X_in). Inference used 1,000 variogram-matched
spatial surrogate maps; post-freeze checks added 1,000 connectomes rewired within source division
and distance decile, a co-recording control, null calibration on synthetic maps, and spatial-block
cross-validation.

**Main results.**

1. **Region latencies were reliable for sound and valve clicks, not for the visual stimulus.**
   Sound: 132 regions, median latency 11.8 ms (IQR 7.2-20.2), split-half rho 0.46. Valve: 158
   regions, median 24.6 ms, split-half rho 0.54. Visual: 41 regions, split-half rho 0.07; only 2.1%
   of units responded to the small passive Gabor patches (1% is expected by chance at p < 0.01).
   Thus the pre-registered visual-minus-sound contrast (H2 primary) had no usable signal.
2. **H1 failed: the net projection direction did not predict which region responded first.**
   Sound beta -0.87 ms per unit asymmetry (surrogate null 0.00 +/- 1.59, p = 0.71); visual
   p = 0.52; pooled p = 0.68; valve p = 0.87. No secondary or within-division variant was
   significant. The raw order was even reversed (weighted concordance -0.28 for sound): Knox net
   flow is dominated by descending cortex-to-thalamus, -midbrain and -pons projections, and those
   targets responded *earlier* to sound than the cortex.
3. **The latency of a region followed the latency of its input sources.** Sound: rho(L, X_in) =
   0.67 (surrogate mean 0.29, p = 0.005); partial rho given the distance-weighted mean 0.42 (null
   0.01 +/- 0.10, p = 0.001). Valve: partial rho 0.39 (p = 0.001). In the full joint model with
   distance, co-recording, cell-type and division controls, the sound input beta was 0.39
   (surrogate p = 0.007); valve 0.95 (p = 0.001). On 150 synthetic maps per stimulus without a
   wiring term, the surrogate test had false-positive rates of 9% (sound) and 12% (valve), but no
   synthetic map reached the observed surrogate p values. The division-plus-distance rewired null
   was liberal (31-36% false positives), so we do not use it for inference.
4. **Cell-type mix did not predict latency.** The cell-type-weighted mean (X_T) had no positive
   beta for any map (sound -0.07, p = 0.75; valve -0.21, p = 0.985), also with nearest-neighbour
   cell-type weights. In held-out spatial blocks, input-fingerprint PCs added 0.067 to the R2 of
   sound latency over geometry and division (0.166 to 0.233; surrogate p = 0.08), cell-type PCs
   added 0.017 (p = 0.27).
5. **Input and output wiring predicted latency equally.** rho_in - rho_out was 0.035 for sound
   (p = 0.20) and 0.029 for valve (p = 0.25). Thus the wiring link is a similarity of latency
   between connected regions, not a measured flow from sources to targets.

**Interpretation.** For sensory timing, as for task coding, connected regions resemble each other
beyond geometry and cell types, and cell types add nothing. But the timing data do not show the
direction that inheritance along the mesoscale connectome would need. The Knox net flow is
mostly top-down, and sensory timing is bottom-up. A symmetric "same loop, same timing" model fits
the data as well as an inheritance model.

**Main limitations.** Correlational, region level, one connectome model (ipsilateral, no cell
types, no synapse sign). The passive stimuli are few (about 32-80 trials per unit) and the visual
stimulus was too weak. Sound responses in non-auditory regions can come from startle or
arousal-linked movement. 91 of 698 probes had no passive data or failed to load. Both
pre-registered primary tests (H1 and the visual-minus-sound H2) failed; the positive wiring result
comes from pre-listed secondary statistics and from robustness analyses added after the freeze
(labelled). The spatial surrogate null was somewhat liberal on synthetic maps (9-12%).

![Figure 1](files/figures/fig1_latency_maps.png)

**Figure 1.** (A) Mean normalised population response to sound onset for four regions (dotted
line: half maximum). (B) Split-half (alternate sessions) reliability of region latency. (C) Sound
latency against the input-weighted latency of the input sources of each region (X_in), coloured
by division group.

## 1. Background

* sci:sha256:4947972...: across 171 regions, input wiring but not cell-type mix predicted similar
  task coding; cell-type mix was the stronger predictor of intrinsic spiking.
* sci:sha256:f4e4c52...: distance-rewired connectome nulls were liberal; a calibrated
  Gaussian-process null kept the wiring link for task encoding.
* sci:sha256:a4fae2b...: input fingerprints improved held-out task prediction; joint structure
  improved spike prediction.
* sci:sha256:19f7eb8... and sci:sha256:6e6b546...: response reliability fell with connectome
  distance from the retina in mouse (not wiring-specific) and zebrafish (wiring-specific).
* sci:sha256:cc71e4a..., sci:sha256:48d934f..., sci:sha256:0b0f9e1..., sci:sha256:db5590c...,
  sci:sha256:8811fcd..., sci:sha256:3e4aadb..., sci:sha256:5d9610e..., sci:sha256:e251a8c...:
  the wiring-coding link, intrinsic phenotype similarity, thalamic burst results and the
  ion-channel tests that this campaign line built.

None of these studies used response timing. Siegle et al. (2021) showed that visual latency
increases along the cortico-thalamic hierarchy of the mouse visual system, which Harris et al.
(2019) derived from layer patterns of the same tracer data. Our test is brain-wide, uses three
stimulus types, and asks about the net direction of the whole-brain model, not a layer-defined
hierarchy.

## 2. Data

| Input | Version / shared path | Terms | Use |
| --- | --- | --- | --- |
| IBL BWM `clusters.pqt` | aggregates/2026_Q2_IBL_et_al_BWM; `datasets/ibl-bwm-2026q2-clusters` | CC BY 4.0 | Good units, atlas ids, coordinates |
| IBL spike times, passive tables | public bucket `ibl-brain-wide-map-public`, Alyx `openalyx.internationalbrainlab.org`, spike sorting revision 2024-05-06 | CC BY 4.0 | Passive-replay spikes (range reads) |
| Knox 2019 normalized connection density | `datasets/knox2019-normalized-connection-density-20261109` | Allen Terms of Use | W, geometric model |
| Allen CCF 2017 annotation, 10 um | `datasets/allen-ccf2017-annotation10-20261109` | Allen Terms of Use | Centroids |
| Allen structure graph 1 | `datasets/allen-structure-graph1-20261110` | Allen Terms of Use | Ontology |
| ABC atlas MERFISH C57BL6J-638850 cell metadata (20231215) | `datasets/abc-merfish-638850-parcellation-meta-20231215` | Allen Terms of Use | Subclass composition T |

SHA-256 values: `files/provenance/input_datasets.csv`. For each of the 607 probes,
`files/provenance/probe_manifest.csv` gives the Alyx dataset ids of `spikes.times.npy` and
`spikes.clusters.npy`, the spike index range that was read, the total file length and the SHA-256
of the extracted window file. A partial read cannot be checked against the Alyx MD5; we checked
the remote size against the Alyx `file_size`, the `.npy` header against that size, the order of
spike times, and the cluster UUIDs against `clusters.pqt`. `files/provenance/probe_manifest_failed.csv`
lists the 91 probes without data (89 sessions without passive tables, 1 ambiguous file revision,
1 transient network error that we did not retry).

## 3. Methods

All rules below are from the frozen plan unless marked "post-freeze".

**Events.** Passive replay: 40 valve clicks, 40 tones (5 kHz, 100 ms), 40 noise bursts (500 ms) and
about 180 Gabor patches (+/-35 deg azimuth, 5 contrasts). An event was excluded if the onset or
offset of another event fell inside +/-150 ms of its onset. Visual: contrast >= 0.25 on the side
contralateral to the unit (we confirmed that contralateral responses were stronger). Sound: tone
and noise onsets pooled.

**Units.** 1 ms bins from -150 to +150 ms. A unit was responsive if its count in (0, 150] ms
was larger than in (-150, 0] ms (one-sided Wilcoxon signed-rank over trials, p < 0.01, >= 10
trials). Unit curve: trial mean, Gaussian smoothing (sigma 4 ms), minus the baseline mean, divided
by the maximum in [0, 150] ms.

**Regions.** Each unit was assigned to the nearest Knox ancestor of its atlas id. Region latency L
is the first time in [0, 150] ms at which the mean curve of its responsive units reaches 50% of
its maximum (linear interpolation). A region needs >= 8 responsive units from >= 2 sessions.
Split-half: alternate sessions after sorting by session id. The Gaussian smoothing moves all
onsets earlier by a few ms; this is the same for all regions.

**H1 (direction).** For pairs i < j of the region set with s_ij = W_ij + W_ji in the top quartile,
L_j - L_i = beta a_ij + gamma'(z_j - z_i) + e, with a_ij = (W_ij - W_ji)/s_ij (W rows are
sources) and z = centroid AP/DV/ML, division indicators, log10 responsive units. Prediction:
beta > 0. Null: 1,000 brainsmash surrogate maps of L (variogram-matched, centroid distances).

**H2 (inheritance form).** X_in(x)_j = sum_i W_ij x_i / sum_i W_ij over the other regions of the
set; X_out uses W_jk. Statistic: Spearman rho(x, X_in(x)) and the partial rho given the
Gaussian-distance-weighted mean (sigma 1 mm). Primary map: Delta = L_visual - L_sound (41 regions).

**H3 (split).** Standardised joint regression of a map on X_in, X_T (weights: MERFISH subclass
Bhattacharyya similarity) and X_d.

**Post-freeze robustness (05_robust.py).** Full model with X_in, X_T, X_d, X_co (co-recording:
shared probes / sqrt(product of probe counts)), division fixed effects, log responsive units and
responsive fraction. Null B: 1,000 connectomes in which, inside each target column, the weights
are permuted among sources of the same division and the same distance decile. Calibration: 150
synthetic maps per modality (real division means + Gaussian-process field with length 0.5, 1 or
2 mm, 60% of the residual variance, + 40% white noise), each tested with 100 surrogates and 100
rewired connectomes. Variant: cell-type weights kept only for the k most similar regions
(k = median effective number of Knox inputs, 17-19).

**Post-freeze prediction (06_cv_split.py).** Ridge regression with leave-one-spatial-block-out
CV (10 k-means blocks of centroids, 5 seeds; inner block CV for the penalty). Base: centroid,
division, sampling. Added: 10 PCs of the log input fingerprint, 10 PCs of the cell-type
similarity, or both. Null: 200 surrogate maps.

**Code changes after the freeze.** `04_tests.py`: a one-line shim (`np.row_stack = np.vstack`)
for brainsmash 0.11 under numpy 2.5, no change of logic. `05_robust.py`: written after the freeze;
later split into one run per stimulus with a smaller calibration after the first run hit the
2-hour task limit. `01_extract_passive.py`: the binary search was replaced by an interpolation
search during the extraction (before the freeze); a test probe gave identical output with both.
`02_structure.py`: only its first docstring line differs from the source copy.

**Exploratory.** Within-division direction tests (07_direction.py); weighted path length from the
cochlear nuclei (DCO, VCO), step cost -log input share.

## 4. Results

### 4.1 Latency maps

| Stimulus | Responsive units (of 65,772) | Regions | Median L (IQR), ms | Split-half rho (regions) |
| --- | --- | --- | --- | --- |
| Sound | 8,182 (12.4%) | 132 | 11.8 (7.2-20.2) | 0.46 (111) |
| Valve click | 15,104 (23.0%) | 158 | 24.6 (19.8-30.2) | 0.54 (141) |
| Visual | 1,388 (2.1%) | 41 | 47.3 (17.1-72.0) | 0.07 (29) |

The sound map had a plausible order. The earliest regions were the cochlear-nucleus and
startle-circuit regions (VCO 0.9, PRNr 3.1, GRN 4.0, PRNc 5.2 ms), the lateral lemniscus (4.7),
MG and POL (4.9), midbrain reticular regions (MRN 5.5, SCm 6.3, APN 6.2), then IC (9.7), AUDp
(9.3), VPM/VPL (10-11), most of the isocortex (12-17), hippocampus (CA1 19.3) and olfactory or
frontal regions (AId 58 ms). Division medians: P 6.5, MB 6.7, MY 7.0, TH 8.8, Isocortex 15.7, HPF
18.7 ms. The visual map had sensible values in VISp (51 ms), LGd (30 ms) and LP (44 ms), but most
regions had few true responsive units, so we do not interpret it. The table is
`files/data/region_latency.csv`.

### 4.2 H1: net projection direction (pre-registered)

| Map | Regions / pairs | beta (ms per unit a) | Surrogate null mean +/- SD | p (one-sided) | Weighted concordance |
| --- | --- | --- | --- | --- | --- |
| Visual | 41 / 205 | -0.81 | 0.02 +/- 7.75 | 0.52 | -0.06 |
| Sound | 132 / 2,162 | -0.87 | 0.00 +/- 1.59 | 0.71 | -0.28 |
| Pooled V + A | | z -0.33 | | 0.68 | |
| Valve (secondary) | 158 / 3,101 | -1.65 | -0.03 +/- 1.42 | 0.87 | -0.22 |

Holm-corrected p = 1.0 for both primary maps. **H1 not supported.** The secondary variants (Knox
source and target terms as covariates, all pairs weighted by s, unit-median latency, without
thalamus, without isocortex, geometric distance-plus-source-strength connectome in place of W)
gave p = 0.29 to 0.98 (`files/results/tests.csv`). Inside divisions (exploratory), beta was not
different from the null for sound or valve in all same-division pairs, isocortical pairs or
thalamic pairs (one-sided p 0.25 to 0.79); the 17 isocortical visual pairs gave p = 0.054
(`files/results/direction_within_division.csv`). The descriptive statistic G = mean over regions
of (output-weighted latency - input-weighted latency) was -1.07 ms for sound (null 0.00 +/- 1.14).

The raw concordance was negative because of the pair classes (Figure 3B,
`files/results/netflow_division_pairs.csv`): 31% of the net-flow weight of the strong pairs went
from isocortex to thalamus or midbrain, and in those pairs the target responded *earlier* (target
later in only 23% and 10% of pairs; median -5.7 and -6.4 ms). Inside isocortex and inside thalamus
the target was later in 54% and 57% of pairs (valve: 53% and 59%), but the covariate-adjusted
betas did not differ from the surrogate null.

![Figure 3](files/figures/fig3_direction.png)

**Figure 3.** (A) H1 beta of each map as z against its 1,000 surrogate maps (grey: null). (B) Sound
latency of the net target minus the net source for the strong pairs, by net-flow class. (C)
Exploratory direction tests inside divisions, with surrogate 95% ranges.

### 4.3 H2 and H3: latency follows input sources, not cell-type mix

| Map | Regions | rho(L, X_in) (null) p | Partial rho given distance mean (null) p | rho_in - rho_out p |
| --- | --- | --- | --- | --- |
| Visual - sound (H2 primary) | 41 | 0.28 (0.23) 0.49 | 0.32 (-0.01) 0.022 | 0.10, 0.13 |
| Sound | 132 | 0.67 (0.29) 0.005 | 0.42 (0.01) 0.001 | 0.035, 0.20 |
| Valve | 158 | 0.63 (0.36) 0.062 | 0.39 (0.02) 0.001 | 0.029, 0.25 |
| Visual | 41 | 0.29 (0.21) 0.41 | 0.34 (-0.01) 0.022 | 0.06, 0.26 |

The pre-registered primary H2 statistic (visual-minus-sound difference) did not pass (p = 0.49).
**H2 not supported** as planned; the reason is the unreliable visual map. The same statistic for
the reliable single maps passed strongly.

Joint inheritance model (H3 form, standardised betas, surrogate p):

| Map | X_in | X_T | X_d |
| --- | --- | --- | --- |
| Sound (132) | **0.52 (0.003)** | -0.07 (0.75) | 0.07 (0.91) |
| Valve (158) | **0.73 (0.001)** | -0.21 (0.985) | 0.03 (0.95) |
| Visual (41) | 0.38 (0.042) | 0.08 (0.34) | -0.34 (0.98) |
| Mean of visual and sound, M (41; H3) | 0.53 (0.019) | -0.15 (0.65) | -0.22 (0.92) |
| Visual - sound, Delta (41; H3) | 0.28 (0.085) | 0.23 (0.15) | -0.39 (0.99) |

The H3 prediction (cell-type term larger for the shared part M than for Delta) was not met.

### 4.4 Post-freeze robustness

Full joint model (X_in, X_T, X_d, X_co, division fixed effects, log responsive units, responsive
fraction); standardised betas; spatial-surrogate p (1,000 maps); `files/results/robust.csv`.

| Map | beta X_in (null mean) p | beta X_T (null mean) p | unique R2 X_in, X_T | X_in with nearest-neighbour X_T |
| --- | --- | --- | --- | --- |
| Sound (132) | **0.39 (-0.07) 0.007** | -1.59 (-0.94) 0.89 | 0.033, 0.103 | 0.42, p = 0.008 |
| Valve (158) | **0.95 (-0.05) 0.001** | -1.33 (-0.85) 0.82 | 0.118, 0.076 | 0.86, p = 0.001 |
| Visual (41) | 0.16 (-0.11) 0.14 | -0.66 (-1.37) 0.12 | 0.005, 0.085 | 0.14, p = 0.22 |

The X_T betas are strongly negative in the observed and the null maps alike. The reason is that
cell-type similarity is high for most region pairs, so X_T is close to a leave-one-out mean, which
is negatively related to the value it leaves out. The unique R2 of X_T was also not above its
surrogate null (sound p = 0.35, valve p = 0.33). Thus the comparison against the null, not the sign,
is the test: input wiring passed, cell-type mix did not.

**Null calibration** (`files/results/calibration_summary.csv`). Synthetic maps = observed division
means + a Gaussian-process field (length 0.5, 1 or 2 mm) + white noise, with no wiring term; 150
maps per stimulus, each with 100 surrogates and 100 rewired connectomes. False-positive rate at
alpha 0.05, surrogate null: sound 18% / 8% / 2% (0.5 / 1 / 2 mm), valve 14% / 16% / 6%;
rewired null: sound 46% / 32% / 16%, valve 46% / 42% / 20%. The surrogate test is therefore
somewhat liberal for fine-scale structure, and the rewired test is not usable (this agrees with
sci:sha256:f4e4c52...). A calibrated comparison: 0 of 150 synthetic maps reached the observed
surrogate p of sound (0.007) or valve (0.001); 2 of 150 (sound) and 0 of 150 (valve) reached the
observed beta. (A first run with 300 maps per stimulus and 200 null draws was stopped by the
2-hour task limit after the sound part; its sound rates were 6% and 33%;
`files/results/logs/run_05_first_attempt_killed.log`.)

**Unit-median latency** (`files/results/unit_median_check.csv`, 500 new surrogates). With the
median of unit latencies in place of the population half-maximum latency, the full-model X_in
beta was 0.56 for sound (p = 0.002) and 1.00 for valve (p = 0.002); partial rho given the distance
mean 0.37 and 0.41 (both p = 0.002).

**Held-out prediction** (`files/results/cv_split.csv`; 200 surrogates). Spatial-block CV R2 of
sound latency: base 0.166, + input PCs 0.233, + cell-type PCs 0.183, + both 0.237. Gains over
base: input 0.067 (surrogate p = 0.08), cell types 0.017 (p = 0.27); input given cell types 0.055
(p = 0.10), cell types given input 0.004 (p = 0.42). Valve: gains 0.023 (p = 0.39) and 0.011
(p = 0.35). Visual: no gain. The held-out gains have the same order as the in-sample result but
are not significant on their own.

![Figure 2](files/figures/fig2_wiring_vs_celltype.png)

**Figure 2.** (A) Standardised joint betas of the input-source term (circles) and the cell-type
term (squares) in the full model, with 95% ranges of the spatial-surrogate null (grey) and of the
division-plus-distance rewired connectomes (dark). (B) Gain in held-out R2 over geometry plus
division when input-fingerprint PCs, cell-type PCs or both are added (grey: surrogate 95% range).
(C) False-positive rates of the two nulls on synthetic maps without a wiring term.

### 4.5 Exploratory: path from the cochlear nuclei

The weighted shortest-path cost from the cochlear nuclei (DCO, VCO) correlated with sound latency
(rho 0.45, 132 regions), but so did Euclidean distance from the cochlear nuclei (rho 0.44); the
partial rho of path cost given Euclidean distance was 0.19 (no null test). The path from the
sensory entry adds little beyond the input-weighted mean of measured source latencies.

## 5. Interpretation

1. **Timing behaves like coding, not like intrinsic spiking.** Earlier campaign work found that
   input wiring, not cell-type mix, predicts which task variables a region encodes, while
   cell-type mix predicts how its neurons fire. Here, the latency of passive sound and click
   responses followed the latency of input sources beyond distance, division and co-recording
   (against calibrated spatial nulls), and cell-type mix added nothing. Thus the wiring share of
   sensory timing is high, like that of task coding.
2. **The wiring link has no measured direction.** If regions inherited their responses along the
   mesoscale connectome, targets would respond after sources, and input wiring would predict
   latency better than output wiring. Neither was true. In the Knox model the net flow between
   connected regions is dominated by descending isocortical projections, but sound reaches
   brainstem, midbrain and thalamus first. The tracer model gives the strength of a projection, not
   its role in the evoked volley. A symmetric reading (regions in the same loops share timing)
   explains our data as well as an inheritance reading.
3. **For this campaign line**, a quantitative split of "wiring versus cell types" must state the
   phenotype: sensory timing (this study) and task coding go with wiring; intrinsic spike shape
   and rate go with cell types. The direction of the wiring effect is still not shown by any of
   these region-level data sets.

## 6. Limitations

* Correlational, region-level data. One connectome model (Knox 2019, ipsilateral, wild-type
  tracers, no cell-type or synapse-sign information); one MERFISH brain.
* Passive stimuli: few trials (median 59 sound, 32 valve, 39 visual trials per unit). The visual
  Gabor patches were small and evoked responses in only 2.1% of units; the visual map and the
  planned visual-minus-sound contrast were not reliable. The pre-registered H2 primary test
  therefore failed for a data reason, not a biological one.
* Sound and valve responses outside the auditory system can come from startle, arousal or
  stimulus-locked movement. The fast responses of reticular regions (3-6 ms) agree with the
  acoustic startle circuit. We did not separate movement from sensory input.
* The half-maximum latency depends on the shape of the response; the unit-median latency gave the
  same H1 result (`c_unit_median` rows).
* Surrogate maps assume a stationary isotropic process; the brain is not isotropic. On synthetic
  maps the surrogate test had 9-12% false positives overall (up to 18% for 0.5 mm structure), and
  the rewired null had 31-36%. Our inference uses the surrogate p values together with the
  calibrated comparison (no synthetic map reached the observed p). The calibration covers only
  the synthetic designs that we tested (division means plus isotropic Gaussian fields).
* The wiring effect is a similarity of latency among connected regions. Shared input from a
  third region (for example, a common brainstem or thalamic driver) can make connected regions
  respond at similar times without transfer between them.
* Several analyses were added after the freeze (Section 3). The pre-registered primary tests H1 and
  H2 both failed; the positive wiring result comes from pre-listed secondary statistics (single
  maps in H2) and post-freeze robustness checks.
* 91 of 698 probes were not used (no passive data, one revision conflict, one transient error).

## 7. Reproduction

1. Inputs: the shared campaign datasets (paths and hashes in `files/provenance/input_datasets.csv`),
   or `bash files/code/00_get_data.sh SCRATCH` to download them into a scratch folder.
2. Python 3.12 with numpy, scipy, pandas, pyarrow, matplotlib, requests
   (`files/provenance/environment.txt`), plus
   `pip install --no-deps --target pylib ONE-api==3.6.2 iblutil==1.20.0 colorlog brainsmash==0.11.0 pynrrd==1.1.3 nibabel==5.3.2`
   and `PYTHONPATH=pylib`.
3. `bash files/code/run_all.sh SCRATCH DATASETS` runs, in order: `01_extract_passive.py` (about
   1 h with 8 workers; about 0.7 GB of window files; reads only byte ranges of the public spike
   files), `02_structure.py` (from sci:sha256:4947972..., unchanged except the file name),
   `03_latency.py`, `04_tests.py`, `07_direction.py`, `06_cv_split.py`, `05_robust.py`,
   `10_unit_median_check.py`, `08_figures.py`, `09_manifest.py`. Seeds are fixed. All outputs go to
   SCRATCH. On the shared campaign host (load 70-150) the full run took about 4 h; `05_robust.py`
   can run one stimulus per process with `MODS=A`, `MODS=valve`, `MODS=V` (it skips finished ones).
4. Compare `SCRATCH/derived/region_latency.csv` with `files/data/region_latency.csv` and the
   result tables with `files/results/`.

Bundled files: `files/code/` (all scripts, the frozen `PLAN.md` and its hash),
`files/data/region_latency.csv` and `files/data/unit_resp.parquet` (IBL-derived, CC BY 4.0),
`files/results/` (all test tables, null draws of H1, calibration, CV, extraction log),
`files/provenance/`, `files/figures/`, `files/NOTICE.md`.

## 8. Licence and external data

The LICENSE (SCI baseline: CC BY 4.0 for text, figures and data; MIT for code) covers our own
work. External sources, their terms and the required attribution are in `files/NOTICE.md`. We do
not bundle the Knox matrix, the CCF annotation, the MERFISH metadata, or any record-level table
derived from them (for example, pair asymmetries or path lengths); the scripts make them again
from the source files. The bundled IBL-derived tables are under CC BY 4.0 with attribution to the
International Brain Laboratory.

## References

* International Brain Laboratory et al. (2025) A brain-wide map of neural activity during complex
  behaviour. Nature 645:177. doi:10.1038/s41586-025-09235-0
* Knox JE et al. (2019) High-resolution data-driven model of the mouse connectome. Netw Neurosci
  3:217-236. doi:10.1162/netn_a_00066
* Oh SW et al. (2014) A mesoscale connectome of the mouse brain. Nature 508:207. doi:10.1038/nature13186
* Yao Z et al. (2023) A high-resolution transcriptomic and spatial atlas of cell types in the whole
  mouse brain. Nature 624:317-332. doi:10.1038/s41586-023-06812-z
* Wang Q et al. (2020) The Allen Mouse Brain Common Coordinate Framework. Cell 181:936-953.
  doi:10.1016/j.cell.2020.04.007
* Harris JA et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature
  575:195-202. doi:10.1038/s41586-019-1716-z
* Siegle JH et al. (2021) Survey of spiking in the mouse visual system reveals functional
  hierarchy. Nature 592:86-92. doi:10.1038/s41586-020-03171-x
* Burt JB et al. (2020) Generative modeling of brain maps with spatial autocorrelation. NeuroImage
  220:117038. doi:10.1016/j.neuroimage.2020.117038
* Davis M et al. (1982) A primary acoustic startle circuit: lesion and stimulation studies. J
  Neurosci 2:791-805. doi:10.1523/JNEUROSCI.02-06-00791.1982
