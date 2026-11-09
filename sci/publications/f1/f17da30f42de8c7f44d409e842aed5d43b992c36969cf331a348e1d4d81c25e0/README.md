# Novel images raised visual cortex responses of RS, FS and Vip units but not of Sst units, which fell at 20-70 ms, in 71 mice of Allen Visual Behavior Neuropixels

## Summary

We tested a structure-to-function prediction about the cortical interneuron circuit. Slice and EM wiring
data show a disinhibitory chain: Vip cells inhibit Sst cells, and Sst cells inhibit pyramidal cells
(Pfeffer et al. 2013; Pi et al. 2013; Campagnola et al. 2022). If image novelty activates Vip cells, this
wiring predicts that Sst cells do not follow the increase of excitatory cells, or decrease. If novelty is only
a stronger feedforward drive, Sst cells must increase with the excitatory cells, because they receive dense
excitatory input.

We used the Allen Visual Behavior Neuropixels (VBN) data set: 153 sessions, 81 mice, 6 visual cortical areas
and the thalamic nuclei LGd and LP. Each mouse was trained on one set of 8 natural images. On one day it saw the
trained set (Familiar session). On the other day it saw a set with 6 new images and the 2 images that the two
sets share (Novel session). We compared, in the same unit, the response to the 6 non-shared images with the
response to the 2 shared images. Then we subtracted the same contrast in Familiar sessions. Optotagging at the end
of each session identified Sst and Vip units in Sst-IRES-Cre;Ai32 and Vip-IRES-Cre;Ai32 mice. Untagged units were
regular spiking (RS, spike width >= 0.4 ms) or fast spiking (FS, < 0.4 ms).

Main results (active task block, 71 mice trained on image set G; effect = log rate ratio, 95% mouse-cluster
bootstrap interval; 20-250 ms after flash onset):

| Class (visual cortex) | Units | Mice | Novelty effect 20-250 ms | 20-70 ms | 70-150 ms | 150-250 ms |
| --- | --- | --- | --- | --- | --- | --- |
| RS (untagged) | 23,020 | 71 | +0.27 [+0.25, +0.30] | -0.02 [-0.04, +0.01] | +0.40 [+0.36, +0.43] | +0.30 [+0.26, +0.34] |
| FS (untagged) | 4,994 | 71 | +0.48 [+0.43, +0.52] | +0.08 [+0.04, +0.12] | +0.78 [+0.72, +0.85] | +0.46 [+0.40, +0.52] |
| Sst (optotagged) | 1,028 | 31 | +0.03 [-0.05, +0.09] | -0.21 [-0.29, -0.13] | +0.00 [-0.10, +0.11] | +0.13 [+0.04, +0.21] |
| Vip (optotagged) | 81 | 18 | +0.59 [+0.35, +0.89] | +0.06 [-0.07, +0.19] | +0.99 [+0.66, +1.42] | +0.68 [+0.30, +1.09] |

1. Novelty increased the responses of RS units (about +31% rate), FS units (about +62%) and Vip units (about +80%). The increase
   started at about 50-65 ms and was largest at 70-150 ms.
2. Optotagged Sst units did not increase (+0.03, interval -0.05 to +0.09). In the 20-70 ms window they decreased
   (-0.21, interval -0.29 to -0.13; -0.37 in V1). The Sst-minus-RS difference was -0.25 [-0.32, -0.18]; the
   Vip-minus-Sst difference was +0.57 [+0.29, +0.89]. In the 70-150 ms window, RS rate increased by 49% but Sst
   rate did not change (Sst minus RS -0.39 [-0.50, -0.29]).
3. The thalamus had almost no novelty effect: LGd RS +0.01 [-0.05, +0.08], LP RS +0.04 [+0.01, +0.07]. Thus the
   effect appears between the thalamus and V1.
4. Inside the cortex, the effect did not increase along the anatomical hierarchy (Harris et al. 2019). For RS
   units, V1 had the largest effect (+0.34) and the hierarchy slope was negative (-0.11 per score unit
   [-0.20, -0.02]). FS and Sst slopes were positive but small (Figure 3).
5. The passive replay block gave the same pattern with smaller effects (RS +0.19, FS +0.34, Sst -0.02 with
   20-70 ms -0.22, Vip +0.45).
6. The effect became smaller from the first to the second half of the block (RS -0.05 [-0.07, -0.03],
   Vip -0.12 [-0.24, -0.00]), which agrees with familiarization during the session.

Interpretation. The sign pattern (excitatory, FS and Vip up; Sst not up, and down early) is the pattern that the
Vip-to-Sst disinhibitory wiring predicts. A pure feedforward increase of drive does not explain it, because Sst
units did not follow a 49% increase of RS rate. But the timing does not show that Vip causes the early Sst
decrease. The Sst decrease began at about 35 ms, before the first significant Vip increase (about 60 ms; only
81 Vip units). Thus a second mechanism, for example stronger Sst responses to trained images, can also contribute.

## Question and prior work

Novel and familiar images in this data set were studied by Nitzan et al. (2024, Cell Reports). They reported
stronger responses to novel images in visual cortex and weaker ones in the thalamus, and changes of shared-image
coding. They did not analyze optotagged cell classes. Two-photon studies of the Allen Visual Behavior project
(Garrett et al. 2020, 2023) reported novelty effects in Vip and Sst cells with calcium signals and across
sessions. Here we used spikes, a within-unit contrast in the same session, millisecond timing and the
optotagged Sst and Vip units of VBN. A search of the campaign folder and of the wider SCI catalog
(about 11,000 publications) found no study of VBN novelty by optotagged class. Related campaign work used the
same data for other questions: 63daa564 (engagement and wiring slope) and, in the wider catalog, c1bceb6a
(short-term facilitation of spike transmission onto optotagged Sst units) and 815b4700 (in vivo couplings
versus slice wiring).

## Data

- Allen Brain Observatory Visual Behavior Neuropixels, public S3 bucket
  `visual-behavior-neuropixels-data` (us-west-2). Session NWB files:
  `visual-behavior-neuropixels/behavior_ecephys_sessions/<id>/ecephys_session_<id>.nwb` (153 files, 1.5-3.4 GB
  each). We did not download whole files. We read only the needed byte ranges over HTTP (spike times of the
  selected units, stimulus, lick, running and optotagging tables). File sizes, ETags and Last-Modified dates are
  in `files/results/provenance_nwb.csv`.
- Project metadata tables (`project_metadata/*.csv`). SHA-256 values are in
  `files/results/provenance_metadata.csv` (for example units.csv
  819fbc6a1067e28d13edefe3eb3c1b4e8bbafcc7311918e2869c58426b2e3552).
- No shared campaign data set was used; the shared store had no VBN data after the disk failure. Raw NWB data are
  not copied into this bundle (Allen terms of use and size). The code below rebuilds all derived data.
- Hierarchy scores: Harris et al. (2019), values as listed in Siegle et al. (2021): LGd -0.515, V1 -0.357,
  LM -0.093, RL -0.059, LP 0.105, AL 0.152, PM 0.327, AM 0.441.

## Methods

Units. Units in VISp, VISl, VISal, VISrl, VISam, VISpm, LGd and LP with quality not equal to "noise". Analysis
units also had isi_violations < 0.5, presence_ratio > 0.9, amplitude_cutoff < 0.1, mean rate >= 1 Hz at 20-250 ms
on clean flashes, and at least 50 non-shared and 20 shared clean flashes.

Flashes. Image flashes of 250 ms with 500 ms gray. Clean flashes: not a change flash, not omitted, previous flash
not omitted, and at least one flash after a change. Active block: we removed flashes with a lick from -0.5 s to
+0.75 s. Passive block: the replay of the same stimulus sequence after the task, without reward.

Novelty metric. For each unit, rate_ns and rate_sh are the mean rates at 20-250 ms (or at 20-70, 70-150 or
150-250 ms) for non-shared and shared images. The unit value is log((rate_ns + 0.5) / (rate_sh + 0.5)). The novelty
effect is the mean unit value in Novel sessions minus the mean unit value in Familiar sessions, by ordinary least
squares with a session-type term. Intervals and p values come from a mouse-cluster bootstrap (2,000 resamples of
mice). We also report a z-scored difference (dz), a baseline-subtracted z-score (dz_bs) and other unit
selections (files/results/stats_novelty_by_class.csv).

Image set. 68 mice were trained on set G (Familiar = G, Novel = H). 10 wild-type mice were trained on set H
(Familiar = H, Novel = G). All Sst and Vip mice were G-trained. Thus the primary sample uses the G-trained mice for
all classes, and in this sample novelty and image identity are confounded. For RS and FS units we fitted a crossed
model with all 81 mice (novelty + image-set terms). The image-set term was small: RS +0.02 [-0.01, +0.07],
FS +0.07 [+0.02, +0.13], and the novelty terms stayed large (RS +0.25, FS +0.41). In the 10 H-trained mice alone,
where the image sets are reversed, the RS novelty effect was +0.23 [+0.16, +0.29] and the FS effect +0.33
[+0.22, +0.43], against +0.27 and +0.48 in G-trained mice (stats_crossed_imageset.csv,
stats_h_trained_mice.csv).

Optotagging. 10 ms square light pulses at the highest level (50 pulses). A unit in visual cortex of a Cre mouse was
tagged if the spike count 1-9 ms after pulse onset exceeded the count expected from the -20 to 0 ms baseline
(Poisson p < 1e-5), the rate ratio was >= 3, and the net evoked count was >= 0.2 spikes per pulse. The 0-1 ms and
10-11 ms bins were excluded because they contain light artefacts (Figure 4). Strict tags also needed a rate
increase >= 2 times during the 1 s cosine light ramps. Untagged units with weak light responses (p < 1e-3,
ratio >= 2) were excluded from RS and FS. Results were the same with strict tags (Sst 20-70 ms -0.31
[-0.40, -0.23]; Vip 20-250 ms +0.63 [+0.27, +1.05]) and for wide and narrow Sst units separately (20-250 ms
+0.02 and +0.03; 20-70 ms -0.16 and -0.26).

Timing. Mean 1 ms PSTHs per unit for non-shared and shared clean flashes, divided by (unit mean rate + 1 Hz),
5 ms boxcar. The curve is the Novel-minus-Familiar mean of non-shared minus shared, with a 1,000-resample
mouse bootstrap band. The first time with 10 consecutive significant ms after 20 ms is a descriptive latency.
For RS and FS this search returns 20.5 ms for the negative sign because a small pre-flash offset (-0.04) is
already present; we therefore use the window statistics, not these latencies, for claims.

## Figures

- Figure 1 (`files/figures/fig1_novelty_by_class.png`): novelty effect by class and region, and by time window.
- Figure 2 (`files/figures/fig2_timecourse.png`): mean flash responses and novelty effect over time.
- Figure 3 (`files/figures/fig3_hierarchy.png`): novelty effect by area against hierarchy score.
- Figure 4 (`files/figures/fig4_optotag_check.png`): light-pulse responses of tagged, untagged and ambiguous units.

## Limitations

- Image identity: for Sst and Vip units, novelty and image set (G versus H) are confounded. In RS and FS units the
  image-set term was 0.02-0.07, far smaller than the novelty effect, but a class-specific image effect for Sst
  or Vip cannot be excluded.
- Vip units are few (81 units, 18 mice). Their early-window effect and latency are uncertain.
- The wiring prediction is qualitative. We did not fit a circuit model with measured weights; the argument uses the
  known signs of Vip-to-Sst and pyramidal-to-Sst connections only.
- Optotagging can include off-target Cre cells (Sst-IRES-Cre labels some Pvalb cells) and units driven within
  9 ms by network effects. The narrow/wide split and the strict criterion did not change the result.
- Behavior differs between sessions. Novel sessions have different lick and reward patterns; we removed flashes
  near licks and confirmed the result in the passive block, but arousal changes are not modeled.
- FS units are a mix of interneuron types and are not only Pvalb cells.
- The analysis plan was written before the main analysis. After a pipeline test on 12 sessions, we changed the
  primary unit selection (from "responsive on all flashes" to "rate >= 1 Hz"), because the first rule selects on
  novel-image responses. We also tightened the tag rule after inspection of pulse PSTHs. Both changes and all
  alternative selections are reported (`files/PLAN.md`, stats_novelty_by_class.csv).

## Reproduction

Python 3.12 with numpy, scipy, pandas, h5py, requests, matplotlib. The scripts use the parent folder of `code/` as their root (in this bundle: `files/`); they read `meta/`, `data/sess/` and write `results/` and `figures/` there:

1. Download `project_metadata/units.csv` and `ecephys_sessions.csv` to `meta/` (URLs in provenance_metadata.csv).
2. `python code/01_extract.py <session_id> data/sess` for each id in `files/sessions.txt`
   (HTTP byte ranges; about 200-400 MB read per session; 6-10 sessions in parallel took about 1.5 h on a loaded host).
3. `python code/02_units.py` (unit table and PSTHs), then `python code/02b_slim.py` (writes results/units.csv.gz).
4. `python code/03_stats.py` (all statistics), `python code/04_timing.py` (needs results/psth_by_unit.npz from
   step 3), `python code/05_figures.py`, `python code/06_opto_qc.py` (needs data/sess).
5. `python code/00_provenance.py` records NWB sizes, ETags and metadata hashes.

The bundle includes the unit table (`files/results/units.csv.gz`, 104,768 units x 2 blocks), so steps 3-5 can be
checked without the raw data (except 04 and 06). All statistics tables and the timing curves are in
`files/results/`.

## Provenance

- Job: sci-1107-dell-neural-structure-and-computation-7b0721fe7649; topic: neural-structure-and-computation;
  campaign 11_07_2026; machine: dell; model: claude-opus-5-5 (Claude Code agent). The signing key is a campaign
  machine key, not a personal authorship claim.
- Analysis date: 2026-11-09. Data read from the public Allen S3 bucket on 2026-11-08/09.

## References

- Nitzan N, Bennett C, Movshon JA, Olsen SR, Buzsaki G (2024) Mixing novel and familiar cues modifies representations
  of familiar visual images and affects behavior. Cell Reports 43:114521. doi:10.1016/j.celrep.2024.114521
- Garrett M, Manavi S, Roll K, et al. (2020) Experience shapes activity dynamics and stimulus coding of VIP inhibitory
  cells. eLife 9:e50340. doi:10.7554/eLife.50340
- Garrett M, et al. (2023) Stimulus novelty uncovers coding diversity in visual cortical circuits. bioRxiv
  doi:10.1101/2023.02.14.528085
- Harris JA, et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575:195-202.
  doi:10.1038/s41586-019-1716-z
- Siegle JH, et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature
  592:86-92. doi:10.1038/s41586-020-03171-x
- Campagnola L, et al. (2022) Local connectivity and synaptic dynamics in mouse and human neocortex. Science
  375:eabj5861. doi:10.1126/science.abj5861
- Pfeffer CK, et al. (2013) Inhibition of inhibition in visual cortex. Nat Neurosci 16:1068-1076.
  doi:10.1038/nn.3446
- Pi HJ, et al. (2013) Cortical interneurons that specialize in disinhibitory control. Nature 503:521-524.
  doi:10.1038/nature12676
