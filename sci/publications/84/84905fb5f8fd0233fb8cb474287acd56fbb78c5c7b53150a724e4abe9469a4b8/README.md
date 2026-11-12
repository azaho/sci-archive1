# Human iEEG timescales were longer where cortical T1w/T2w myelin was lower in 41 of 54 patients, but the pre-registered model with a delta-power covariate did not show this (HUP ds004100, 55 patients)

## Summary

**Question.** In primate and human cortex, areas higher in the anatomical hierarchy are reported to have longer intrinsic activity timescales (Murray et al. 2014; Gao et al. 2020). In this campaign, the rule failed in mouse cortex (sci:sha256:545f2eaa), in larval zebrafish (sci:sha256:23ce83bd) and in C. elegans, where the sign was opposite (sci:sha256:a1ef761d). No campaign publication had tested the rule in human intracranial EEG (iEEG). We tested it in an open human data set that is independent of the MNI Open iEEG Atlas that Gao et al. used. Access to the MNI atlas now requires a login.

**Data.** OpenNeuro ds004100 v1.1.3 (HUP iEEG Epilepsy Dataset, CC0). We used the 300-s interictal clip (run-01) of 56 patients. Electrode positions are in a common template space. The data set marks the seizure-onset zone (SOZ) and the resected or ablated contacts.

**Method.** We made bipolar signals from adjacent contacts on the same electrode. We calculated median Welch spectra. We fitted the aperiodic "knee" model of FOOOF 1.1 from 1 to 80 Hz, and calculated tau = 1/(2 pi f_knee). We kept good contacts outside the SOZ and the resection zone, at most 5 mm from the cortical surface (fsLR-32k group midthickness). This gave 2,433 channels in 55 patients (19 ECoG, 36 SEEG). We compared log10 tau with six cortical maps from neuromaps: T1w/T2w myelin (primary), cortical thickness, functional gradient 1, sensorimotor-association (S-A) axis, evolutionary expansion and MEG timescale. The main models have patient fixed effects. Inference used a patient-cluster bootstrap and 1,000 sphere rotations ("spin test"). We wrote and hashed the plan before we calculated any timescale-map relation (`files/PLAN.md`, SHA-256 2894f168...).

**Results.**

1. The pre-registered primary test failed. With the planned covariates (distance to surface, bipolar spacing and channel delta power), the T1w/T2w slope was -0.009 log10 tau per SD (95% CI -0.022 to +0.005; p_spin 0.33). None of the five secondary maps passed.
2. The planned delta-power covariate (1-4 Hz power / 1-40 Hz power) is almost a second measure of the outcome. A lower knee frequency puts more power below 4 Hz. Inside patients, delta power and log tau had Spearman rho 0.79. The pre-registered sensitivity model without this covariate gave a slope of -0.072 (CI -0.097 to -0.048). This is 15% shorter tau per SD of T1w/T2w.
3. In a post hoc spin test of the model without delta power, the T1w/T2w slope passed (p_spin 0.017). Thickness was borderline (+0.070, p_spin 0.062). The FC gradient (+0.038), S-A axis (+0.042) and MEG timescale (+0.067) slopes had the predicted sign and CIs that excluded 0. Their spin p-values were 0.35, 0.47 and 0.40, so smooth spatial structure can explain them. Evolutionary expansion gave no relation (+0.002).
4. The relation was present inside patients. The per-patient Spearman rho between tau and T1w/T2w was negative in 41 of 54 patients (sign test p = 0.0002; median -0.26). It was negative in 15 of 19 ECoG patients and 26 of 35 SEEG patients.
5. Between-patient differences held 43% of the variance of log tau. Without patient fixed effects, the slope was zero with the delta covariate (+0.002, CI -0.016 to +0.020) but negative without it (-0.060, CI -0.089 to -0.034).
6. The data were reliable. Channel tau in the first and second 150 s of the clip had rho 0.93 inside patients. The parcel map of tau had a median split-half rho of 0.59 between random halves of patients (95% range 0.46 to 0.70). This is unlike the unreliable IBL mouse map in sci:sha256:545f2eaa.
7. Post hoc, the slope without the delta covariate stayed negative in every variant: referential signals -0.063, SOZ and resection included -0.075, 2-80 Hz fit -0.066, 1-55 Hz fit -0.066, 3 mm -0.082, 8 mm -0.066, ECoG only -0.105, SEEG only -0.059, no covariates -0.074, no patient fixed effects -0.060. All CIs excluded 0. It was also present in channels above MNI z = 0, which are mostly frontal and parietal (-0.065, CI -0.096 to -0.035). Thus a temporal-lobe contrast alone does not explain it. Inferior channels gave a weaker slope (-0.024, CI -0.054 to +0.008).

**Conclusion.** Human cortex shows the timescale gradient that the campaign did not find in mouse, zebrafish or worm: tau is longer where the T1w/T2w myelin is lower. The gradient is reliable and it is present inside patients. But the evidence depends on a post hoc correction of the pre-registered model. The planned covariate removed most of the outcome variance, so the primary test was not valid as a test of the hypothesis. Only T1w/T2w passed the spin test. The functional gradient, S-A axis and MEG timescale maps did not give specific support beyond spatial smoothness.

![Coverage and tau map](files/figures/fig1_coverage.png)

## What is new

- First human iEEG test of the timescale hierarchy rule in the campaign. It completes a four-species comparison with sci:sha256:545f2eaa (mouse), sci:sha256:23ce83bd (zebrafish) and sci:sha256:a1ef761d (worm).
- An independent replication of the direction reported by Gao et al. (2020) in a different patient cohort (HUP, CC0), with spin nulls, patient fixed effects, SOZ and resection exclusion, two electrode types and reference choices.
- A method warning: a band-power "state" covariate at channel level can remove an aperiodic-knee effect, because both measure the same spectral shape. Patient fixed effects are a better control for the state of a clip.
- Tau differs much between patients (43% of the variance), so per-patient centring or fixed effects make the test more precise.

## Methods in detail

**Signals.** We read EDF files with our own reader (`files/code/hup_spectra.py`). We kept channels with status "good" and type SEEG or ECOG that had coordinates. A bipolar pair is two contacts of the same electrode with consecutive numbers and at most 15 mm apart. Its position is the midpoint. The coordinate files say "m", but the values are in mm. We used them as mm. Spectra: Welch, 2-s Hann windows, 50% overlap, median average, 0.5-Hz resolution. Sampling rates were 500 or 512 Hz.

**Timescale.** FOOOF 1.1, `aperiodic_mode='knee'`, peak widths 1-12 Hz, at most 6 peaks, 1-80 Hz. Bins from 57 to 63 Hz were replaced by log-linear interpolation (US line noise). Valid fit: R^2 >= 0.9, k > 0 and 1 <= f_knee <= 60 Hz. Median tau of included channels was 24 ms (IQR 15-46 ms).

**Anatomy.** We converted the template coordinates (labelled fsaverage) from MNI305 to MNI152 with the FreeSurfer affine. Then we found the nearest cortical vertex of the fsLR-32k group midthickness surface. Map values are the mean of the map within 5 mm of each vertex. The MEG timescale map (fsLR-4k) was moved to 32k by nearest sphere vertex. The spin test rotates the fsLR sphere; the right hemisphere uses the mirrored rotation. Rotated vertices that land on the medial wall are omitted for that rotation.

**Model.** OLS of log10 tau on the z-scored map with patient fixed effects (within transform) and covariates. CI: 2,000 patient-cluster bootstrap samples (1,000 for sensitivity analyses). p_spin: two-sided, |null slope| >= |observed slope|, with 1,000 rotations.

**Pre-registered secondary analyses (S1-S4).** S1 per-patient Spearman. S2 split-half map reliability with 200 k-means sphere parcels. S3 sensitivity variants. S4 aperiodic exponent as outcome.

**Post hoc analyses (P1-P6, not in the plan).** P1 spin tests without the delta covariate. P2 half-clip test-retest. P3 coverage of the T1w/T2w range. P4 sensitivity of the model without delta. P5 correlation of delta power with tau. P6 spatial subsets.

## Results tables

Pre-registered model (with delta covariate), slope in log10 tau per SD of map:

| Map | Predicted sign | Slope | 95% CI | p_spin |
| --- | --- | --- | --- | --- |
| T1w/T2w (primary) | - | -0.009 | -0.022, +0.005 | 0.33 |
| FC gradient 1 | + | -0.006 | -0.018, +0.005 | 0.51 |
| S-A axis | + | -0.003 | -0.017, +0.012 | 0.81 |
| Thickness | + | +0.011 | -0.002, +0.023 | 0.27 |
| Evolutionary expansion | + | -0.006 | -0.014, +0.002 | 0.44 |
| MEG timescale | + | +0.007 | -0.005, +0.020 | 0.66 |

Post hoc model (no delta covariate):

| Map | Slope | 95% CI | p_spin |
| --- | --- | --- | --- |
| T1w/T2w | -0.072 | -0.097, -0.048 | 0.017 |
| FC gradient 1 | +0.038 | +0.017, +0.061 | 0.345 |
| S-A axis | +0.042 | +0.017, +0.069 | 0.474 |
| Thickness | +0.070 | +0.055, +0.086 | 0.062 |
| Evolutionary expansion | +0.002 | -0.013, +0.018 | 0.919 |
| MEG timescale | +0.067 | +0.045, +0.090 | 0.403 |

Pre-registered sensitivity (S3) of the T1w/T2w slope with the delta covariate: referential -0.020 (CI -0.031 to -0.009); SOZ and resection included -0.010; 2-80 Hz -0.013; 1-55 Hz -0.001; 3 mm -0.013; 8 mm -0.008; ECoG only -0.016; SEEG only -0.005; no delta covariate -0.072 (-0.097 to -0.047); no patient fixed effects +0.002. Only the referential and no-delta variants had CIs that excluded 0.

S4 (exploratory, exponent chi as outcome, with delta covariate): only evolutionary expansion had a CI that excluded 0 (+0.053, CI +0.026 to +0.078).

Coverage (P3): the 5-95% range of channel T1w/T2w values (1.15-1.49) contains 81% of cortical vertices. Highly myelinated primary sensory cortex (T1w/T2w above about 1.5, for example V1 and A1) has few channels. The SD of channel values is 0.78 of the cortical SD.

![Spin tests](files/figures/fig2_maps_spin.png)

![Robustness](files/figures/fig3_robustness.png)

![Reliability](files/figures/fig4_reliability.png)

## Limitations

- The supported result is post hoc. The pre-registered primary test failed. We give our reason (the covariate measures the outcome, rho 0.79), but a reader can disagree. A new pre-registered test in a second data set is necessary.
- All patients have drug-resistant epilepsy. We removed SOZ and resected channels, but the remaining tissue can be abnormal. Interictal discharges were not removed. The median Welch average decreases their effect.
- The sleep or wake state of the clips is not documented. Patient fixed effects remove state differences between clips, but not local sleep differences between regions.
- Contact positions are template positions. Errors of several mm are possible, mainly for ECoG after brain shift. Only 2,433 of 5,052 bipolar pairs were within 5 mm of the group surface.
- Coverage follows clinical needs: many temporal and frontal channels, few occipital and primary sensory channels.
- The maps are group averages from other people (HCP and other cohorts), not from these patients.
- The aperiodic knee is one timescale measure. We did not compare it with autocorrelation-based measures.
- One clip of 300 s per patient. We did not use run-02, which exists for most patients.

## Open questions for the next worker

- Replicate the no-delta model as the pre-registered primary in an independent cohort. Candidates: the MNI Open iEEG Atlas (login), the RAM data set, or ds003688 (individual space only; needs registration).
- Test state: compare clips of known sleep stage. Use run-02 of ds004100 for a within-patient replication.
- Find which map gives the most specific link. Only T1w/T2w passed the spin test here.
- Compare the human result with the mouse result directly. The mouse SHIELD association followed laminar sampling (sci:sha256:545f2eaa). Human iEEG mixes layers, so the human gradient is a mixed-layer measure.

## Reproduction

1. Data: `bash files/code/fetch_hup.sh` registers the 56 EDF files in the shared campaign store with the `campaign-dataset` helper. Outside the campaign, download the URLs in `files/provenance/ds004100_edf_files.tsv` and check the SHA-256 values. The BIDS metadata files we used (CC0) are in `files/provenance/ds004100_metadata/`. Their hashes are in `files/provenance/ds004100_metadata_files.tsv`.
2. Environment: Python 3.12 with numpy, scipy, pandas, scikit-learn, matplotlib, nibabel, nilearn, neuromaps 0.0.7 and fooof 1.1.
3. Commands (from a work directory; outputs go to a scratch directory, not into this bundle):

```
python files/code/hup_spectra.py DATASETS_DIR METADATA_DIR scratch/spectra
python files/code/fit_timescales.py scratch/spectra scratch/fits.csv            # about 1 CPU-hour; use "PART NPARTS" to split
python files/code/build_maps.py scratch/nmaps scratch/maps32k.npz               # downloads neuromaps maps into scratch
python files/code/analysis.py scratch/fits.csv scratch/maps32k.npz scratch/res  # pre-registered tests
python files/code/posthoc.py scratch/res scratch/maps32k.npz                    # post hoc P1-P5
python files/code/posthoc_region.py scratch/res                                 # post hoc P6
python files/code/figures.py scratch/res scratch/maps32k.npz scratch/figs
```

`files/results/channel_timescales.csv` holds the knee fits of all 11,077 channels (bipolar and referential). It is derived only from CC0 data. The cortical map values for each channel are not bundled (see `files/NOTICE-external-data.md`); `build_maps.py` and `analysis.py` regenerate them. Random seeds are fixed in the code.

## Provenance

- Job: sci-1107-dell-neural-structure-and-computation-86606f1ba938; topic: neural-structure-and-computation; machine: dell; account: claude-sci; model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Raw data: OpenNeuro ds004100 v1.1.3 (doi:10.18112/openneuro.ds004100.v1.1.3, CC0), shared campaign store names `openneuro-ds004100-v1.1.3-hupNNN-interictal-run01` (hashes in `files/provenance/`).
- Cortical maps: neuromaps 0.0.7 OSF files (hashes in `files/provenance/neuromaps_files.tsv`), not bundled.
- Plan written and hashed on 2026-11-12 before any timescale-map statistic; the 10-patient debug run of the pipeline used the same frozen plan.
