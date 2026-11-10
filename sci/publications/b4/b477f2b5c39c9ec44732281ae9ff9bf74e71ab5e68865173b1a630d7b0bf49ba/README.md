# In the mouse caudoputamen, where cell types are uniform, the voxel input map did not predict local task coding beyond a calibrated null, except for feedback (IBL, 2,646 units)

Job sci-1107-dell-neural-structure-and-computation-948eea15ebf0, campaign 11_07_2026, topic
neural-structure-and-computation, machine dell. Analysis, code and text: Claude Opus 5.5
(`claude-opus-5-5`) with the SCI CLI, 2026-11-10. The signing key is a campaign-machine key. It is
not a personal authorship claim.

## Summary

**Question.** Earlier campaign work compared whole mouse brain regions. It found that the axonal input
of a region predicts which task variables the region encodes (sci:sha256:cc71e4a4...,
sci:sha256:49479722..., sci:sha256:f4e4c521...). But across regions, input wiring and cell-type
composition change together (rank correlation 0.73 in sci:sha256:48d934f4...). Thus those tests cannot
separate wiring from cell identity. We did a sharper test. Inside one region whose neurons are one
class, the caudoputamen (CP), different positions get different axonal input. If specific wiring sets
the coding content, units at a CP position that gets more input from regions that encode variable k
must encode k more strongly, relative to their other variables.

**Data.** IBL Brain-Wide Map 2026_Q2: spike times of 2,646 good CP units (74 probes, 69 sessions; all
in the left hemisphere) and of 31,439 units in 60 regions (344 probes) for a brain-wide secondary test.
Knox et al. 2019 voxel connectome (100 um). Published BWM region decoding scores. Allen MERFISH cell
types.

**Method.** For each unit and task variable (stimulus side, choice, feedback, block prior), a
condition-combined Mann-Whitney selectivity |z|. For each unit position, the input-predicted map
X[v, k] = the input-weighted mean of the BWM decoding score of variable k over all source regions, with
the voxel-model input to that 100 um voxel as the weight. The statistic beta is the match between
selectivity and X after removal of unit and variable means, with a distance-weighted control. The plan
was frozen and hashed before any selectivity value was computed (`files/code/PLAN.md`).
Primary null (null A): permute the BWM scores among source regions within brain divisions. This keeps
the input topography, and changes only which source encodes what.

**Main results.**

1. **H1 not supported.** In CP, beta = 0.049 (session bootstrap 95% CI 0.003 to 0.086), but null A
   gave p = 0.082 (null mean 0.003, SD 0.032). The pre-registered rule needed p < 0.05.
2. **Calibration.** On 200 synthetic smooth CP maps without wiring dependence, null A had a
   false-positive rate of 0.07 (0.03 to 0.12 by length scale). The second planned null (distance-decile
   rewiring per voxel, null B) had a rate of 0.39. Its p = 0.001 for H1 is thus not evidence. Null B
   loses the spatial smoothness of the real predictor.
3. **Sensitivity.** Over 11 variants (input form, windows, controls, leave one variable out), beta was
   0.045 to 0.090 and p was 0.013 to 0.13. Without feedback, beta fell to -0.007 (p = 0.74).
4. **Feedback is the exception (exploratory).** Per variable, feedback selectivity matched its
   input-predicted map: beta = 0.17 (null A p = 0.003; Holm p = 0.012). With linear or quadratic
   position controls, it became 0.26 and 0.20 (p = 0.001 and 0.003). Choice matched weakly (0.09, Holm
   p = 0.10; 0.11 to 0.13 with position controls, p = 0.008 to 0.021). Stimulus did not match (0.03),
   and block prior went in the opposite direction (-0.06).
5. **There is a CP coding map to explain, but it is weak.** The selectivity profile of a unit was
   predicted by units of other sessions at nearby positions (r = 0.08, p = 0.001). Split-half
   reliability of 300 um bin profiles was 0.19. The input-predicted map agreed with this reliable map
   for feedback (r = 0.72) and choice (0.23), not for stimulus (0.07), and opposite for block prior
   (-0.46).
6. **Cell types do not vary much inside CP (exploratory).** MERFISH neuronal subclass composition of
   300 um CP bins was nearly the same everywhere (mean Bhattacharyya coefficient 0.97). Between 87 bins,
   coding-profile similarity followed input similarity beyond distance (partial rho 0.10, bin
   permutation p = 0.049) but not composition similarity (-0.03, p = 0.66).
7. **Brain-wide within-region test (S1) not supported.** Over 60 regions, the pooled within-region beta
   was 0.014 (null A p = 0.051). 31 of 60 regions were above their null mean, and 3 had p < 0.05
   (chance gives 3). Per variable (exploratory), only feedback matched: beta = 0.047 (p = 0.007), and
   0.034 without CP (p = 0.016 uncorrected; about 0.06 after Holm correction over 4 variables).

**Conclusion.** Inside the caudoputamen, where the cell-type mix is nearly constant, the mesoscale
input map does not predict the local profile of task coding in general. The region-level link between
wiring and coding (cc71e4a4, 49479722) does not transfer to the within-region scale as a general rule.
One part does transfer: CP positions that get more input from feedback-encoding sources, mostly
midbrain and motor cortex, have more feedback-selective units. This holds beyond position, and weakly
in other regions. The evidence is exploratory and needs confirmation in independent data.

![Figure 1](files/figures/fig1_cp_maps_primary.png)

## 1. Background

The connectivity-fingerprint hypothesis states that the inputs and outputs of an area set its function
(Passingham et al. 2002). The striatum is a strong test case. Its principal neurons (D1 and D2 spiny
projection neurons) are similar at all positions, but its cortical and subcortical input is
topographic (Hintiryan et al. 2016; Hunnicutt et al. 2016; Foster et al. 2021). Striatal activity
follows the activity of the cortex that projects to it (Peters et al. 2021). We asked a different
question: does the anatomical input map, combined with what each source region encodes in the same
task, predict where in CP each task variable is encoded?

Prior campaign results that this work builds on:

* sci:sha256:0b0f9e1c...: cortical input share predicted thalamic burst firing across 27 nuclei.
* sci:sha256:cc71e4a4...: input-weighted source encoding predicted region encoding in IBL (182 regions)
  and Steinmetz 2019 data. We use the same predictor at the voxel scale.
* sci:sha256:19f7eb8e... and sci:sha256:6e6b5461...: reliability gradients from the retina; rewired
  graphs did as well as real wiring in mouse.
* sci:sha256:e251a8ce...: transcriptomic type number did not predict spike-feature diversity.
* sci:sha256:48d934f4...: input similarity and cell-type similarity both predicted spiking phenotypes;
  they are strongly correlated across regions.
* sci:sha256:49479722...: input wiring, not cell-type mix, predicted region-level coding similarity.
* sci:sha256:f4e4c521...: distance-rewired nulls were liberal; a calibrated null kept wiring links for
  task encoding. Our null B result repeats this warning at the voxel scale.

## 2. Data

| Input | Version / shared path | Terms |
| --- | --- | --- |
| IBL BWM `clusters.pqt`, `trials.pqt` | aggregates/2026_Q2_IBL_et_al_BWM; `datasets/ibl-bwm-2026q2-*` | CC BY 4.0 |
| IBL spike times per probe (`spikes.times`, `spikes.clusters`, `clusters.uuids`) | public S3, revision 2024-05-06; URLs and MD5 in `files/provenance/spike_sources.csv` | CC BY 4.0 |
| IBL BWM region scores `region_info.csv` | GitHub int-brain-lab/paper-brain-wide-map, commit de37454 | CC BY 4.0 |
| Knox 2019 voxel model `weights.csv.gz`, `nodes.csv.gz` | `datasets/knox2019-voxel-model-{weights,nodes}-20261110` | Allen Terms of Use |
| Knox 2019 region matrix (region list) | `datasets/knox2019-normalized-connection-density-20261109` | Allen Terms of Use |
| Allen CCF 2017 annotation, 100 um | `datasets/allen-ccf2017-annotation100-20261110` | Allen Terms of Use |
| Allen structure graph 1 | api.brain-map.org, read 2026-11-10 | Allen Terms of Use |
| ABC atlas MERFISH C57BL6J-638850 metadata (20231215) | `datasets/abc-merfish-638850-parcellation-meta-20231215` | Allen Terms of Use |

SHA-256 values are in `files/provenance/input_sha256.txt`. We added the voxel model and the 100 um
annotation to the shared campaign dataset store with the campaign dataset helper.

## 3. Methods

### 3.1 Spike counts and selectivity (`10_fetch_counts.py`, `12_selectivity.py`)

For every good unit (IBL label 1), spike counts in fixed windows of every trial. Trials with
`bwm_include`. Selectivity is the condition-combined Mann-Whitney z (sum of U - E[U] over strata
divided by the square root of the summed tie-corrected variance):

| Variable | Window | Groups | Strata |
| --- | --- | --- | --- |
| stimulus | stimOn + 0-0.1 s | stimulus side (contrast > 0) | choice x block |
| choice | firstMovement - 0.1-0 s | left vs right | stimulus side x block |
| feedback | feedback + 0-0.2 s | correct vs error | choice |
| prior | stimOn - 0.4 to -0.1 s | block 0.8 vs 0.2 | none |

The outcome is |z|, converted to rank-normal scores per variable.

### 3.2 Input-predicted coding map (`11_voxel_inputs.py`, `lib.py`)

The Knox voxel model gives the input to each 100 um target voxel from each source voxel (weights x
nodes; source mask: right hemisphere; voxel order as in `mcmodels`). We summed source voxels into the
291 Knox regions and checked the mask size against the model (226,346 source and 448,962 target voxels,
exact match). Unit positions: CCF = bregma (5739, 5400, 332 um) + IBL x, -y, -z; units in the left
hemisphere are mirrored. At 100 um, 85% of units fell in a voxel with the same atlas label as the IBL
label. Y[s, k] is the rank-normal BWM score (`stim_dec`, `choice_dec`, `fback_dec`, `prior_dec_ep`) of
185 source regions. X[v, k] = sum_s w(s -> v) Y[s, k] / sum_s w(s -> v), without the target region.
The distance control Xd uses weights exp(-d / 1 mm) from source centroids.

Sanity check of the input map: in CP, somatosensory and motor input was lateral, ACA input medial,
visual input dorsomedial, and auditory input posterior (tail), as in the tracer literature.

### 3.3 Tests (`13_tests.py`)

Model: selectivity = unit FE + variable FE + beta X + beta_d Xd. Both sides are demeaned two ways and
standardized. H1 used CP units. S1 used all Knox regions with at least 150 units from 8 sessions, with
region x variable FE (only within-region variation). Null A: 1,000 permutations of Y within Cosmos
divisions. Null B: 1,000 rewirings that shuffle each voxel's input weights among sources in the same
distance decile. Session bootstrap: 1,000 resamples. Calibration (S2): 200 synthetic outcome maps, one
independent Gaussian random field per variable (length scales 0.3, 0.6, 1.0 mm) plus equal noise.

Exploratory additions after the H1 result (labelled as such): `15_cp_topography.py`,
`16_cp_pervariable.py`, `18_s1_pervariable.py`, and the bin analysis `14_cp_celltypes.py` (S4, planned
as exploratory). All deviations are in `files/code/AMENDMENTS.md`.

## 4. Results

### 4.1 Pre-registered tests

| Test | n | beta | Null A mean (SD) | Null A p | Null B p (not valid) |
| --- | --- | --- | --- | --- | --- |
| H1, CP | 2,646 units, 69 sessions, 923 voxels | 0.049 | 0.003 (0.032) | 0.082 | 0.001 |
| S1, 60 regions, within-region | 31,439 units | 0.014 | -0.001 (0.009) | 0.051 | 0.001 |

H1 session bootstrap 95% CI: 0.003 to 0.086. Calibration false-positive rates at alpha 0.05 (S2):

| Length scale | Null A | Null B |
| --- | --- | --- |
| 0.3 mm | 0.06 | 0.42 |
| 0.6 mm | 0.03 | 0.39 |
| 1.0 mm | 0.12 | 0.36 |

Null A was close to nominal, but liberal at the longest scale. Thus, its p values are approximate and,
if anything, too small. This makes the H1 null result stronger, not weaker.

### 4.2 Sensitivity (CP, null A)

![Figure 2](files/figures/fig2_variables_sensitivity.png)

| Variant | beta | p |
| --- | --- | --- |
| primary | 0.049 | 0.082 |
| ipsi + contra input | 0.051 | 0.066 |
| sqrt weights | 0.047 | 0.128 |
| isocortex sources only | 0.055 | 0.042 |
| wider windows | 0.045 | 0.068 |
| distance control 0.5 / 2 mm | 0.051 / 0.047 | 0.070 / 0.075 |
| no distance control | 0.052 | 0.063 |
| without stimulus / choice / feedback / prior | 0.075 / 0.048 / -0.007 / 0.090 | 0.054 / 0.120 / 0.740 / 0.013 |

The pooled estimate is stable, near the edge of significance, and depends on feedback.

### 4.3 Per variable (exploratory, CP)

| Variable | beta | null A p (Holm) | + linear position | + quadratic position |
| --- | --- | --- | --- | --- |
| stimulus | 0.034 | 0.245 (0.49) | 0.043 (p 0.28) | -0.008 (p 0.61) |
| choice | 0.090 | 0.033 (0.10) | 0.114 (p 0.008) | 0.128 (p 0.021) |
| feedback | 0.173 | 0.003 (0.012) | 0.258 (p 0.001) | 0.198 (p 0.003) |
| prior | -0.063 | 0.94 (0.94) | -0.083 (p 0.91) | -0.085 (p 0.95) |

Feedback selectivity also increased toward ventral (r = 0.09) and lateral (r = 0.10) CP. The position
controls show that the match is not only this gradient. The input-predicted feedback map follows the
share of midbrain input (r = 0.68 across CP units). Each midbrain source with tracer input to CP (SNc,
SNr, MRN, PPN, RR) had a share that correlated with feedback selectivity at r = 0.14 to 0.17. These
sources have high BWM feedback scores. A dopaminergic reward signal is one plausible explanation, but
the voxel model cannot separate SNc from neighbouring injection sites, and this was not a planned test.

### 4.4 Brain-wide within-region test (S1)

![Figure 3](files/figures/fig3_brainwide_within_region.png)

Per region (exploratory), the betas spread around zero; the largest were in PIR (0.14, p = 0.001), LP
(0.05, p = 0.001) and EPd (0.06, p = 0.017). Per variable over the 60 regions: stimulus 0.023
(p = 0.048), choice -0.005 (0.74), feedback 0.047 (0.007), prior -0.016 (0.87). Without CP (59
regions): feedback 0.034 (p = 0.016), stimulus 0.021 (0.059).

## 5. Interpretation

1. The question was whether specific wiring, not geometry or cell type, sets regional physiology. Inside
   CP, cell type is nearly fixed. If wiring set coding content in general, the input map should have
   predicted the local coding profile. It did not beyond a calibrated null. Thus, the region-level
   wiring-coding match does not imply a general within-region rule at the mesoscale.
2. Feedback is the exception. It is the only variable whose within-CP map followed the input map in
   all checks, and it was the strongest variable in the region-level work as well (49479722: the coding
   link depended mostly on feedback decoding). A widely projecting reward or outcome signal from a few
   source groups is easier to trace through anatomy than stimulus or choice information.
3. Block prior went in the opposite direction. The BWM prior scores are high in many cortical and
   subcortical sources, and the prior code may arise from local or recurrent processes rather than
   from the sources with the strongest prior decoding.
4. Methods lesson: a null that rewires each voxel independently was badly liberal (39% false
   positives). Null distributions for within-region maps must keep the spatial smoothness of the
   predictor. This agrees with the region-level finding of f4e4c521.

## 6. Limitations

* Power. The CP coding map is weak (bin split-half r = 0.19; cross-session prediction r = 0.08), so a
  small real effect can stay below significance. The bootstrap interval of H1 excludes zero, but the
  calibrated null does not.
* The Knox voxel model interpolates between about 400 wild-type tracer experiments. Its within-region
  detail is limited, and it has no cell-type or synapse-sign information. Small sources (for example,
  SNc versus SNr) are not well separated.
* The BWM region scores are decoding scores of the same IBL data set, so sources and targets share
  mice and sessions. They come from other regions than the target.
* Unit positions come from histology alignment; the label agreement at 100 um was 85%.
* All CP units are in the left hemisphere; the input model is ipsilateral from the right hemisphere
  (mirrored), and contralateral input changed little.
* S1 used 344 of 698 probes because of download speed (fixed cutoff; see AMENDMENTS). The per-region
  results have few units per region.
* Exploratory per-variable results were chosen after the H1 result. They need confirmation in
  independent data (for example, other striatal Neuropixels data sets).
* Selectivity is |z|; the sign of the response (for example, contralateral preference) is not used.

## 7. Reproduction

1. `bash files/code/00_get_data.sh /path/scratch` downloads all inputs except spike times (about
   2.4 GB) and prints SHA-256 values. Compare them with `files/provenance/input_sha256.txt`.
2. Install pynrrd 1.1.3 (`pip install --no-deps --target pylib pynrrd==1.1.3`; `PYTHONPATH=pylib`).
   Other versions are in `files/provenance/environment.txt`.
3. `SCRATCH=/path/scratch SCI_DATASETS=/path/scratch/datasets bash files/code/run_all.sh`. The first
   step downloads spike times of the 344 probes in `files/provenance/probes_used.txt` (about 86 GB in
   transit; only small count files are kept). Seeds are fixed. Outputs go to `SCRATCH/derived`,
   `SCRATCH/results` and `SCRATCH/figures`. With one thread, H1 with calibration and sensitivity takes
   about 7 minutes and S1 about 30 minutes.
4. To check results without spike downloads, use `files/data/unit_selectivity.csv.gz` (copy it to
   `SCRATCH/derived/`), then run steps 11 and 13-18.

Bundled files:

* `files/code/`: all scripts, `PLAN.md`, its hash log `PLAN.sha256.txt`, and `AMENDMENTS.md`.
* `files/data/` (IBL-derived, CC BY 4.0): `unit_selectivity.csv.gz` (52,502 units, z for the primary
  and wide windows), `cp_bins.csv` (mean selectivity profile of 87 CP bins).
* `files/results/`: all test results, null distributions, calibration table, per-region table, logs.
* `files/provenance/`: input hashes, spike source URLs and MD5, probes used and failed, cutoff time,
  environment.

## 8. Licence and external data

The LICENSE (SCI baseline: CC BY 4.0 for text, figures and data; MIT for code) covers our own work.
External sources, their terms and required attribution are listed in `files/NOTICE.md`. Allen-derived
tables are not bundled; the scripts make them again.

## References

* International Brain Laboratory et al. (2025) A brain-wide map of neural activity during complex
  behaviour. Nature. doi:10.1038/s41586-025-09235-0
* Knox JE et al. (2019) High-resolution data-driven model of the mouse connectome. Netw Neurosci
  3:217-236. doi:10.1162/netn_a_00066
* Oh SW et al. (2014) A mesoscale connectome of the mouse brain. Nature 508:207-214.
  doi:10.1038/nature13186
* Yao Z et al. (2023) A high-resolution transcriptomic and spatial atlas of cell types in the whole
  mouse brain. Nature 624:317-332. doi:10.1038/s41586-023-06812-z
* Wang Q et al. (2020) The Allen Mouse Brain Common Coordinate Framework. Cell 181:936-953.
  doi:10.1016/j.cell.2020.04.007
* Hintiryan H et al. (2016) The mouse cortico-striatal projectome. Nat Neurosci 19:1100-1114.
  doi:10.1038/nn.4332
* Hunnicutt BJ et al. (2016) A comprehensive excitatory input map of the striatum reveals novel
  functional organization. eLife 5:e19103. doi:10.7554/eLife.19103
* Foster NN et al. (2021) The mouse cortico-basal ganglia-thalamic network. Nature 598:188-194.
  doi:10.1038/s41586-021-03993-3
* Peters AJ et al. (2021) Striatal activity topographically reflects cortical activity. Nature
  591:420-425. doi:10.1038/s41586-020-03166-8
* Steinmetz NA et al. (2019) Distributed coding of choice, action and engagement across the mouse
  brain. Nature 576:266-273. doi:10.1038/s41586-019-1787-x
* Passingham RE, Stephan KE, Kotter R (2002) The anatomical basis of functional localization in the
  cortex. Nat Rev Neurosci 3:606-616. doi:10.1038/nrn893
