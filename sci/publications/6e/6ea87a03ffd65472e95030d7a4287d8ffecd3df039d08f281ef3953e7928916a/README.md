# Local excitatory recurrence did not reliably predict stimulus-evoked variability quenching in 139 mice (Allen Neuropixels)

## Summary

Theory says that recurrent excitatory networks make the drop of spike-count variability (Fano factor, FF) that follows a stimulus onset ("variability quenching"; Churchland et al. 2010). If this is the main mechanism, brain regions with strong local excitatory-to-excitatory (E-E) recurrence must quench more than relay regions that do not have it. We tested this prediction in two public Allen Institute Neuropixels datasets: Visual Coding Neuropixels (VCN, 58 mice) and Visual Behavior Neuropixels (VBN, 81 mice, one session per mouse). We fixed the region groups and the two primary contrasts before we looked at group results (files/ANALYSIS_PLAN.md):

- P1: visual cortex (six areas, strong local E-E recurrence) versus visual thalamus (LGd + LP, no local E-E connections);
- P2: hippocampal CA3 (dense recurrent collaterals) versus CA1 (sparse recurrence).

The measure was the Churchland mean-matched FF of 200 ms spike counts before (-250 to -50 ms) and after (+50 to +250 ms) the stimulus onset. The per-mouse statistic was the relative quench q = 1 - FF_post/FF_pre.

Main results:

1. **P1 was supported in VCN, but it did not replicate for the same stimulus in VBN.** In VCN full-field flashes, visual cortex quenched more than LGd + LP (q 0.178 vs 0.107; paired difference 0.071, mouse-bootstrap 95% CI 0.038 to 0.106, p = 0.0002, 46 mice). The same was true at VCN drifting-grating onsets (0.153 vs 0.053; difference 0.100, CI 0.080 to 0.120). In VBN full-field flashes, the two groups quenched by the same amount (0.192 vs 0.196; difference -0.004, CI -0.037 to 0.029, 57 mice). In absolute FF units, VBN thalamus quenched more than VBN cortex (difference -0.114, CI -0.183 to -0.045). At VBN image changes, cortex quenched more in the passive replay block (difference 0.047, CI 0.019 to 0.077) and the difference was not clear in the active task block (0.024, CI -0.004 to 0.054).
2. **P2 was not supported in either dataset.** CA3 did not quench more than CA1 (VCN flashes -0.013, CI -0.037 to 0.013, 36 mice; VBN flashes -0.013, CI -0.048 to 0.020, 50 mice; same result for gratings and image changes). Neither CA3 nor CA1 quenched by much (q 0.004 to 0.029). Thus the hippocampal contrast cannot test the recurrence idea, because these visual stimuli did not drive the hippocampus.
3. **Quenching followed visual drive more than recurrence.** Across region-group x mouse points, q increased with the log ratio of post- to pre-onset firing rate (Spearman rho 0.28 to 0.45 in all five stimulus sets, p <= 1e-10). Non-visual thalamus, CA1, CA3, DG, subiculum and midbrain groups quenched by -2% to 7%. The feedforward relay LGd quenched by 9% (VCN) to 22% (VBN) after flashes. In VBN this value was approximately equal to VISp (25%).
4. **At equal rate change, the flash difference became zero, but the grating and image-change differences stayed.** In unit-level models with session fixed effects and a quadratic control for the unit's log rate change and log baseline rate, the cortex-minus-thalamus flash difference was 0.012 log-FF units (p = 0.54) in VCN and -0.05 (thalamus quenched more, p = 0.004) in VBN. Thalamus quenched less than cortex at VCN grating onsets (+0.046, p < 0.001) and at VBN image changes (+0.065 active, +0.046 passive, p <= 0.003).
5. **Other controls did not change the result.** Collapse of thalamic bursts (spike after >= 100 ms silence, then ISI <= 4 ms) into single events did not change any primary contrast. Separate analyses of stationary and running trials did not clearly change the primary contrasts (Figure 2). Quench of cortex and of LGd + LP did not co-vary across mice (group level |rho| <= 0.18; area level VISp vs LGd at most rho 0.35, p = 0.06), so cortical quench was not simply inherited from the thalamic quench of the same mouse.
6. **Cortical layers (VCN, secondary).** Layer 2/3 (CCF 2017 annotation) quenched most (flash q 0.190, grating 0.220). This was more than layer 4 (flash +0.031, CI 0.007 to 0.054; grating +0.074, CI 0.052 to 0.098) and stayed after rate-change control (unit-level -0.055 and -0.063 log-FF, p < 0.001). Layers 4, 5 and 6 did not differ clearly.

Conclusion: a feedforward relay without local E-E recurrence (LGd) can quench spike-count variability nearly as much as cortex, and in one of two datasets as much as cortex. Thus local E-E recurrence is not necessary for quenching. Where cortex quenched more than the thalamus (VCN, image changes, layer 2/3), the extra quench is consistent with a recurrent contribution. However, it changed with dataset and stimulus, and part of it followed the size of the rate change. The data do not support a general rule that "more local recurrence gives more quenching" across the mouse regions that we tested.

## Question and motivation

The objective of this campaign topic is to find how circuit structure supports reliable representations and brain dynamics. Variability quenching is a widespread cortical phenomenon (Churchland et al. 2010). Network models make it with recurrent excitatory structure: clustered E assemblies (Litwin-Kumar & Doiron 2012; Deco & Hugues 2012), stabilized supralinear networks (Hennequin et al. 2018) or suppression of chaotic recurrent fluctuations by input (Rajan, Abbott & Sompolinsky 2010). An anatomical prediction that is common to these models has not been tested across brain regions with simultaneous recordings: regions that have strong local E-E recurrence must quench more than relay regions that do not have it. The thalamic relay nuclei (LGd, LP) have almost no local excitatory-to-excitatory connections. CA3 has dense recurrent collaterals and CA1 has few. Allen Neuropixels sessions record visual cortex, visual thalamus and hippocampus at the same time and in the same mouse, so we can make paired comparisons within each mouse.

## Data

- **Allen Brain Observatory Visual Coding Neuropixels (VCN)**: all 58 sessions (58 mice; 32 brain_observatory_1.1, 26 functional_connectivity). Stimuli: 150 full-field flashes (250 ms, black/white, 2 s period) and drifting-grating onsets that followed >= 0.9 s of grey screen (600-630 presentations). Siegle et al. 2021, Nature.
- **Allen Visual Behavior Neuropixels (VBN)**: 81 sessions, the first recorded session of each of the 81 mice (75 familiar-image sessions, 6 novel). Stimuli: 150 passive full-field flashes (250 ms) at the end of the session, and image-change flashes in the active task block and in the passive replay block.
- Units: Allen "good" units that pass the AllenSDK default QC (amplitude cutoff < 0.1, presence ratio > 0.9, ISI violations < 0.5). In the groups that were analysed, VCN gave 36,862 units and VBN 60,472 units.
- Brain areas from the Allen unit/channel tables (structure acronyms). Cortical layers from the unit CCF coordinates and the CCF 2017 10 um annotation volume (shared campaign dataset `datasets/allen-ccf2017-annotation10-20261109/annotation_10.nrrd`, sha256 a9e9654e...).
- The NWB files were not downloaded completely. `code/01_fetch.py` reads the stimulus tables, the running speed and the byte ranges of `units/spike_times` (a contiguous float64 HDF5 dataset) of the QC units with HTTP range requests, and keeps the spikes inside the stimulus windows. We checked this method against direct h5py reads for 8 random units (all identical; `code/01b_validate_fetch.py`). `files/metadata/provenance_nwb_files.csv` gives the URL, size, S3 ETag and Last-Modified time of each of the 139 NWB files. `files/metadata/input_tables.json` gives the URLs and sha256 hashes of the unit, channel, session, ontology and annotation tables.

Region groups (fixed before the results; `code/ff_lib.py`):
visual_cortex = VISp, VISl, VISal, VISrl, VISpm, VISam (+ VIS, VISli, VISmma, VISmmp);
visual_thalamus = LGd (all subdivisions), LP;
other_thalamus = PO, VPM, TH, Eth, POL, MGv, MGd, MGm, SGN, IntG, PIL, LD, VPL;
CA3; CA1; DG; subiculum = SUB, ProS, POST, PRE; midbrain = APN, MB, NOT, SC layers, PPT, OP, MRN, NB, PAG.
A group of a session was used only if it had >= 10 QC units.

## Methods

1. Spike counts of each unit in a pre-onset window (-250 to -50 ms) and a post-onset window (+50 to +250 ms), and in 100 ms windows centered every 25 ms from -450 to +800 ms (time courses).
2. For each unit x stimulus condition (flash colour; grating orientation x temporal frequency x contrast; image name), the mean and variance over trials (>= 5 trials).
3. Mean-matched FF (Churchland et al. 2010): the distribution of mean counts is matched between time points by random deletion of unit-condition points in 0.5-count bins (greatest common distribution). Then FF is the slope of a weighted regression of variance on mean through the origin (weights (n-1)/(2 m^2)). We did 50 repeats for the pre/post statistic and 10 for the time courses.
4. Per mouse and group: q = 1 - FF_post/FF_pre (primary) and FF_pre - FF_post (secondary). Paired contrasts over mice with both groups: mean difference, 5,000-sample mouse bootstrap 95% CI, two-sided one-sample t test.
5. Trial states: all trials (primary); stationary (mean wheel speed < 2 cm/s, -0.5 to +0.5 s) and running (> 5 cm/s) trials (secondary).
6. Burst control: each thalamic-type burst (first spike after >= 100 ms silence, then ISIs <= 4 ms) was replaced by its first spike, in all regions. Then the full analysis was done again.
7. Unit-level models: log(FF_post/FF_pre) of each unit (rate > 1 Hz in both windows) ~ group + log rate ratio + (log rate ratio)^2 + log pre rate + session fixed effects. We used OLS with session-clustered SEs. We also made a direct comparison of cortex and thalamus units in 0.1-wide bins of log rate ratio.
8. Areas (single structure acronyms) and VCN cortical layers (L1-2/3, L4, L5, L6 from CCF 2017) were analysed with the same population method.

## Results tables (files/tables)

| File | Content |
|---|---|
| `paired_contrasts.csv` | All paired contrasts (dataset, variant, event, state, contrast, measure, n mice, means, difference, bootstrap CI, p) |
| `group_quench.csv` | Mean FF_pre, FF_post, q (bootstrap CI) and rates per group/area, per dataset, event and state |
| `pop_*.csv` | Per-session population results (one row per session x event x state x group) |
| `unit_models.csv`, `unit_models_layers.csv`, `unit_rate_matched.csv` | Unit-level models with rate-change control |
| `covariation.csv` | Across-mouse covariation of cortical and thalamic quench; quench vs rate change |
| `layer_quench.csv` | VCN cortical-layer quench and paired layer contrasts |

Key numbers (relative quench q, mean over mice, state = all trials):

| Dataset / event | Visual cortex | LGd + LP | Cortex - thalamus (95% CI) | CA3 | CA1 | CA3 - CA1 (95% CI) |
|---|---|---|---|---|---|---|
| VCN flash | 0.183 (58) | 0.107 (46) | 0.071 (0.038, 0.106) | 0.008 (36) | 0.022 (51) | -0.013 (-0.037, 0.013) |
| VCN grating onset | 0.156 | 0.053 | 0.100 (0.080, 0.120) | 0.012 | 0.017 | -0.005 (-0.017, 0.008) |
| VBN passive flash | 0.200 (81) | 0.196 (57) | -0.004 (-0.037, 0.029) | 0.015 (51) | 0.028 (76) | -0.013 (-0.048, 0.020) |
| VBN image change, active | 0.095 | 0.068 | 0.024 (-0.004, 0.054) | 0.004 | 0.028 | -0.021 (-0.043, 0.001) |
| VBN image change, passive | 0.091 | 0.040 | 0.047 (0.019, 0.077) | 0.018 | 0.026 | -0.006 (-0.025, 0.013) |

(Group means use all mice with that group; paired differences use mice with both groups, so the two numbers do not always subtract exactly.)

## Figures

- `files/figures/fig1_ff_timecourse.png`: mean-matched FF time courses (100 ms windows; matching over all time points, so the levels differ from the pre/post statistic).
- `files/figures/fig2_paired_contrasts.png`: forest plot of the two primary contrasts for all datasets, events, states and the burst control.
- `files/figures/fig3_area_quench.png`: relative quench for each area in VCN (each dot is one mouse).

## Limitations

- Region groups are anatomical categories, not measured recurrence strengths. LP receives strong cortical feedback, and LGd receives cortical layer 6 feedback. Thus "no local E-E recurrence" does not mean "no loop". We did not use a quantitative recurrence measure, because tracer-based intra-region weights are not reliable near the injection site.
- The hippocampal contrast had almost no quenching to compare, because the visual stimuli did not drive CA1/CA3. This null is therefore weak evidence about recurrence.
- The VCN and VBN flash results disagree. Possible causes are differences in behavioural state (most VBN flash trials were running trials and came after a 1 h task; only 11 VBN mice had enough stationary flash trials), probe placement in the thalamus, and genotype mixtures. We did not find which cause is correct.
- FF quench depends on the size and type of the rate change. The unit-level rate controls are linear-quadratic models and cannot remove all differences in response dynamics (for example, oscillatory flash responses; Figure 1).
- Spike sorting errors, drift and unit isolation differences between regions can change FF. We used only units that pass the Allen QC.
- Mice are the unit of inference. VBN mice with two sessions contributed only their first session.
- The layer assignment uses CCF coordinates of the peak channel. Errors of about 50-100 um near the layer borders are possible.

## Relation to prior campaign work

- sci:sha256:74d39c35f4cebf48a929e4f142800ad680f5975f430991c17a664fc68ea06c28 found that gratings reduced shared spike variability in mouse V1 layers 2/3 and 4 but not in 5 and 6. Our layer result (L2/3 quenches most) agrees in part with it. Our layer 4 quench was not larger than our layer 5 quench.
- sci:sha256:5e701d95f15f204001b23b508cc1f1ad83b8ea499c086d81b49ec0760a73d547 related trial-to-trial co-variation between regions to axonal wiring. Our study asks a different question: whether within-region local recurrence sets the quench.

## Reproduce

Copy `files/code` to `code/` in an empty working directory and run the steps below from that directory. Set PYTHONPATH so that `remfile` and `pynrrd` can be imported. Environment: Python 3.12.16, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, h5py 3.16.0, matplotlib 3.11.2, requests 2.34.2, remfile 0.1.15, pynrrd 1.1.3. Runtime: about 2 h download at about 13 MB/s (about 50 GB of byte ranges are read; about 9 GB is stored), and about 1 min of CPU time per session per analysis variant.

```
# 0. metadata tables (URLs and hashes in files/metadata/input_tables.json)
#    raw/sessions.csv, raw/units.csv (VCN cache); raw/vbn/ecephys_sessions.csv, raw/vbn/units.csv; raw/structure_graph_1.json
# 1. spikes in stimulus windows (session lists in files/metadata/)
python code/01_fetch.py vcn data/vcn raw/units.csv datasets/allen-vcn-ecephys-channels-20261109/channels.csv $(cat vcn_sids.txt)
python code/01_fetch.py vbn data/vbn raw/vbn/units.csv none $(cat vbn_sids.txt)
# 2. per-session FF statistics (variants: region / area / layer labels; raw / burst-collapsed)
python code/02_session_ff.py vcn data/vcn out/vcn_region region raw
python code/02_session_ff.py vcn data/vcn out/vcn_region_burst region collapse
python code/02_session_ff.py vcn data/vcn out/vcn_area area raw
python code/02_session_ff.py vbn data/vbn out/vbn_region region raw   # also vbn_region_burst, vbn_area
# 3. layers: python code/03_layers.py annotation_10.nrrd raw/structure_graph_1.json out/vcn_region/*_units.csv.gz out/vcn_unit_layers.csv
#    then make out/vcn_layer_labels.csv (unit_id,label; labels L1-2/3, L4, L5, L6) and
#    python code/02_session_ff.py vcn data/vcn out/vcn_layer out/vcn_layer_labels.csv raw
# 4. statistics and figures
python code/04_stats.py out tables; python code/05_unit_models.py out tables
python code/07_covariation.py tables; python code/08_layers_stats.py out tables
python code/06_figures.py out tables figures
```

`files/derived/` holds the per-session time courses (`tc_*.csv.gz`), the per-unit pre/post means, variances and FFs (`units_*.csv.gz`) and the unit layer labels. With these files and `files/tables/pop_*.csv`, a reader can check all reported numbers without a new download.

## Provenance

- Campaign 11_07_2026; job sci-1107-dell-neural-structure-and-computation-57fbdc4448f7; topic neural-structure-and-computation; machine dell; account claude-andrii; model Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Data: Allen Institute for Brain Science, Visual Coding Neuropixels and Visual Behavior Neuropixels (public S3 buckets `allen-brain-observatory`, `visual-behavior-neuropixels-data`), read on 2026-11-09. Allen data are subject to the Allen Institute terms of use. This bundle has only derived statistics.
- files/ANALYSIS_PLAN.md was written after a code test on one session and before group results.
