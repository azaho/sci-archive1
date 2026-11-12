# Human iEEG 30-50 Hz exponent followed a GABA-A PET map in two pre-registered clips (55-56 patients), but mesial temporal channels carried most of the link and a second GABA-A map did not repeat it

## Summary

**Question.** The aperiodic exponent (chi) of field-potential power spectra is often used as a marker of the balance between excitation and inhibition (E:I). Gao, Peterson and Voytek (2017) showed that a larger inhibitory share of synaptic current gives a steeper 30-50 Hz spectrum (larger chi). If the regional receptor architecture of human cortex sets the regional E:I balance, then chi must be larger where GABA-A receptor density is high and smaller where glutamate receptor density is high. No campaign publication had tested the exponent against receptor maps. We did this test with human intracranial EEG (iEEG) and positron emission tomography (PET) receptor maps.

**Data.** OpenNeuro ds004100 v1.1.3 (HUP iEEG, CC0). Two 300-s interictal clips (run-01, run-02) per patient. Bipolar channels outside the seizure-onset zone (SOZ) and the resected tissue, at most 5 mm from the cortical surface: 2,540 channels in 55 patients (run-01) and 2,586 channels in 56 patients (run-02). Receptor maps from neuromaps 0.0.7: GABA-A/benzodiazepine site ([11C]flumazenil, Norgaard et al. 2021; primary), NMDA ([18F]GE-179), mGluR5 ([11C]ABP688), GABA-A alpha5 ([11C]Ro15-4513) and a second flumazenil map (Dukart et al. 2018).

**Method.** chi = minus the log-log slope of the median Welch spectrum from 30 to 50 Hz. Model: chi on the z-scored map value at the nearest cortical vertex, with patient fixed effects, distance to the surface and bipolar spacing. Inference: patient-cluster bootstrap and 1,000 sphere rotations (spin test). We wrote and hashed the plan before we calculated any exponent-map statistic (`files/PLAN.md`). The plan named run-01 as the primary test and run-02 as the replication.

**Pre-registered results.**

1. H1 passed in both clips. chi rose with GABA-A density: +0.144 per SD of density in run-01 (95% CI +0.071 to +0.208; p_spin 0.002) and +0.137 in run-02 (CI +0.066 to +0.202; p_spin 0.002). The within-patient SD of chi is 0.63, so one SD of GABA-A density goes with about 0.23 SD of chi.
2. H2 passed in both clips. The E:I receptor index (GABA-A minus the mean of NMDA and mGluR5) gave +0.146 (run-01) and +0.131 (run-02), p_spin 0.001. The glutamate maps alone gave no relation (NMDA -0.033 and -0.020; mGluR5 +0.012 and +0.028). Thus the index result comes from the GABA-A map.
3. H3 passed. With T1w/T2w as a covariate, the GABA-A slope was +0.148 and +0.140.
4. The result was the same for the FOOOF 30-50 Hz exponent, the 20-40 Hz exponent and the 1-80 Hz knee-model exponent (slopes +0.12 to +0.19, all p_spin <= 0.003). Channel chi was reliable: half-clip rho 0.90 and between-clip rho 0.86 inside patients.

**Results that limit the claim.**

5. The second GABA-A PET map (Dukart et al. 2018, a different cohort and tracer analysis) gave no relation (+0.006 and +0.018; p_spin 0.90 and 0.70). The volume version of the primary map gave half the slope (+0.074 and +0.071; p_spin 0.05). The GABA-A alpha5 map gave the opposite sign (-0.131 and -0.119; p_spin 0.017 and 0.016; Holm-adjusted 0.12).
6. Post hoc: the relation was only in inferior channels (MNI z <= 0: +0.20 and +0.19). Superior channels gave -0.063 (CI -0.128 to +0.005) and -0.026 (CI -0.083 to +0.027).
7. Post hoc: most of the link came from the 10% of channels with the lowest patient-centred GABA-A density. 69% of these channels were in inferior medial cortex (median MNI |x| 32, y -15, z -16 mm; medial temporal region). Their mean patient-centred chi was -0.32; the other nine deciles were between -0.05 and +0.13. Without them, the slope fell to +0.043 (CI +0.001 to +0.087; p_spin 0.16) and +0.047 (CI +0.012 to +0.086; p_spin 0.12).
8. Post hoc: the slope stayed positive with a quadratic MNI trend (+0.108, p_spin 0.009; +0.100, p_spin 0.006), with distance to the SOZ as a covariate (+0.162; +0.154), in channels at least 20 mm from any SOZ contact (+0.166; +0.158), and with T1w/T2w and thickness together (+0.144; +0.138). In inferior lateral channels it was smaller (+0.092, p_spin 0.03; +0.082, p_spin 0.016).

**Conclusion.** The pre-registered prediction of the E:I reading passed in two clips of the same patients: channels at sites with more GABA-A receptors had steeper 30-50 Hz spectra. But the data do not show a general receptor-graded E:I rule across cortex. A cluster of mesial inferior temporal channels with low GABA-A density and flat spectra carried most of the link. Superior (frontal and parietal) cortex showed no link. A second GABA-A map did not repeat the cortex-wide link. A contrast between mesial temporal cortex and the rest can explain most of the result. That contrast can come from receptors, from a different cortical type (periallocortex), or from properties of epileptic temporal lobes.

![Figure 1](files/figures/fig1_primary.png)

Figure 1. (A) Pre-registered tests. Slopes of chi per SD of map, with 95% patient-bootstrap CIs (blue run-01, orange run-02). Grey bands show the central 95% of 1,000 spin-null slopes. (B) Per-patient Spearman correlations between chi and the map (patients with at least 10 channels). Black bars are medians. (C) Patient-centred chi in deciles of patient-centred GABA-A density. The lowest decile carries most of the relation.

![Figure 2](files/figures/fig5_posthoc.png)

Figure 2. Post hoc checks of the GABA-A slope. Controls for spatial trend, SOZ distance, T1w/T2w and thickness, and the other GABA-A maps do not remove it. Removal of the lowest-density decile reduces it to about +0.04. The slope occurs in inferior channels, mostly medial, and not in superior channels. The Dukart GABA-A map agrees only in inferior medial channels.

![Figure 3](files/figures/fig2_maps_outcomes.png)

Figure 3. (A) Slopes of chi for each receptor and control map, both clips. Only maps built from the Norgaard GABA-A map pass the spin test with the predicted sign. The GABA-A alpha5 map has the opposite sign. (B) Other spectral outcomes with the primary GABA-A map and the E:I index. Mean 30-50 Hz power falls where GABA-A density is high.

## What is new

- This is the first campaign test of the aperiodic exponent against receptor architecture. It is also, to our knowledge, a new invasive human test of the E:I reading of the exponent with PET receptor maps, with patient fixed effects, spin nulls and a pre-registered replication clip.
- The test locates the source of the link. The study shows that a positive pre-registered map test can come from one anatomical cluster. A decile profile and a subset analysis are necessary before one reads a map slope as a cortex-wide rule.
- The study shows that the result depends on the receptor map. Two flumazenil maps of the same receptor gave different answers at the same channels (within-patient channel rho 0.44).
- It adds channel-level 30-50 Hz exponents for 11,077 (run-01) and 11,236 (run-02) HUP signals (CC0-derived), with half-clip values, for reuse.

## Relation to earlier campaign work

- sci:84905fb5 and sci:5f516e12 tested the iEEG timescale (aperiodic knee) against T1w/T2w in the same recordings. We reuse their spectral code and channel rules unchanged. Our spectra gave the same channel counts (11,077 and 11,236). In their S4 analysis, the knee-model exponent did not follow T1w/T2w. Here, the 30-50 Hz exponent also did not follow T1w/T2w beyond spatial smoothness (+0.063, p_spin 0.29; +0.049, p_spin 0.38).
- Campaign tests of wiring against regional physiology (for example sci:36eebd98) found that geometry and coarse divisions often explain map links. Our post hoc analyses show a similar risk here: one region can carry a map slope.

## Methods

**Spectra.** `hup_spectra.py` of sci:5f516e12, unchanged. Bipolar pairs of adjacent contacts on one electrode, at most 15 mm apart. Median Welch spectrum, 2-s Hann windows, 50% overlap, 0.5-Hz resolution. Sampling rates 500 or 512 Hz. SOZ and resection labels are the union over the run-01 and run-02 channel files.

**Exponent.** `fit_exponents.py`. chi_30_50 = minus the least-squares slope of log10 power on log10 frequency, 30-50 Hz (41 bins). Channels need fit R^2 >= 0.8. Also: FOOOF 1.1 'fixed' 30-50 Hz (at most 2 peaks), 20-40 Hz slope, 70-110 Hz slope (noise-floor check), half-clip slopes. The 1-80 Hz knee-model exponent comes from the bundled tables of sci:5f516e12.

**Maps.** `build_receptor_maps.py`. Volume maps are sampled at each fsLR-32k group-midthickness vertex as the mean of positive voxels within 3 mm. Each map then gets the 5-mm surface-neighbourhood mean of sci:84905fb5. The surface version of the Norgaard map (fsaverage-164k) is moved to fsLR-32k by nearest sphere vertex. The plan required Spearman >= 0.8 between the volume and surface versions of the Norgaard map. The value was 0.65, so the surface version became the primary map before any chi statistic (`files/PLAN_ADDENDUM.md`). Electrode coordinates (template space labelled fsaverage) are converted from MNI305 to MNI152 with the FreeSurfer affine, then matched to the nearest cortical vertex, as in sci:84905fb5.

**Statistics.** `analysis_receptor.py`. OLS with patient fixed effects (within transform). The slope is per SD of the map over the included channels. CIs: 2,000 patient-cluster bootstrap samples (1,000 for sensitivity and post hoc analyses), computed exactly from per-patient cross-products. A check against statsmodels gave the same slope to 13 digits. Spin test: the rotation and electrode re-sampling code of sci:84905fb5 (1,000 rotations; mirrored rotation for the right hemisphere; channels whose rotated vertex falls on the medial wall are dropped for that rotation). Two-sided p_spin = (1 + count of |null| >= |observed|) / 1,001.

**Post hoc analyses.** These were not in the plan. We did them after we saw the pre-registered results. `posthoc.py`: P1 quadratic MNI trend (|x|, y, z, squares and products), P2 SOZ distance, P3 spatial halves, P4 joint models with the other GABA-A maps, P5 T1w/T2w and thickness together. `posthoc2.py`: P6 superior, inferior lateral (|x| >= 45 mm) and inferior medial subsets. `posthoc3.py`: P7 lowest-density decile.

## Results tables

Pre-registered tests (slope of chi per SD of map, patient fixed effects, covariates surface distance and bipolar spacing):

| Test | Run | Slope | 95% CI | p_spin | Rule passed |
| --- | --- | --- | --- | --- | --- |
| H1 GABA-A (primary map) | run-01 | +0.144 | +0.071, +0.208 | 0.002 | yes |
| H1-rep GABA-A | run-02 | +0.137 | +0.066, +0.202 | 0.002 | yes |
| H2 E:I index | run-01 | +0.146 | +0.087, +0.202 | 0.001 | yes |
| H2 E:I index | run-02 | +0.131 | +0.072, +0.187 | 0.001 | yes |
| H3 GABA-A + T1w/T2w covariate | run-01 | +0.148 | +0.083, +0.214 | 0.002 | yes |
| H3 GABA-A + T1w/T2w covariate | run-02 | +0.140 | +0.075, +0.207 | 0.002 | yes |

Secondary single maps (pre-registered, descriptive; Holm over the seven run-01 spin p-values):

| Map | Predicted sign | run-01 slope (CI); p_spin; Holm | run-02 slope (CI); p_spin |
| --- | --- | --- | --- |
| NMDA | - | -0.033 (-0.070, +0.004); 0.44; 1.0 | -0.020 (-0.054, +0.015); 0.61 |
| mGluR5 | - | +0.012 (-0.029, +0.055); 0.81; 1.0 | +0.028 (-0.010, +0.069); 0.53 |
| GABA-A alpha5 | + | -0.131 (-0.184, -0.077); 0.017; 0.12 | -0.119 (-0.167, -0.073); 0.016 |
| GABA-A, Dukart 2018 | + | +0.006 (-0.041, +0.053); 0.90; 1.0 | +0.018 (-0.020, +0.057); 0.70 |
| GABA-A, Norgaard volume | + | +0.074 (+0.021, +0.128); 0.050; 0.30 | +0.071 (+0.020, +0.124); 0.049 |
| T1w/T2w | none | +0.063 (+0.010, +0.117); 0.29; 1.0 | +0.049 (+0.005, +0.091); 0.38 |
| Thickness | none | -0.073 (-0.125, -0.018); 0.22; 1.0 | -0.057 (-0.105, -0.007); 0.32 |

Other outcomes with the primary GABA-A map (run-01; run-02): FOOOF fixed 30-50 Hz +0.164; +0.165. 20-40 Hz +0.191; +0.174. Knee-model 1-80 Hz +0.129; +0.122. Mean log10 power 30-50 Hz -0.090 (p_spin 0.035); -0.088 (p_spin 0.038). All exponent p_spin <= 0.003.

Sensitivity (bootstrap CIs, no spin; full table `files/results/sensitivity.csv`). The GABA-A slope stayed positive in all variants: referential signals +0.124 and +0.142; SOZ and resection included +0.160 and +0.164; 3 mm +0.131 and +0.127; 8 mm +0.141 and +0.132; no flat 70-110 Hz spectra +0.157 and +0.148; SEEG only +0.167 and +0.156; no covariates +0.153 and +0.143; no patient fixed effects +0.134 and +0.134. Two variants were weaker: fit R^2 >= 0.95 (+0.054, CI -0.018 to +0.123; +0.079, CI +0.027 to +0.134) and ECoG only (19-20 patients; +0.075, CI -0.032 to +0.161; +0.081, CI -0.005 to +0.156).

Per-patient correlations (patients with >= 10 channels): rho(chi, GABA-A) was positive in 35 of 54 (run-01, sign p 0.04, median +0.15) and 37 of 55 patients (run-02, sign p 0.014, median +0.12).

Post hoc (run-01; run-02):

| Analysis | Slope (95% CI); p_spin |
| --- | --- |
| + quadratic MNI trend | +0.108 (+0.044, +0.161); 0.009 / +0.100 (+0.041, +0.149); 0.006 |
| + log distance to SOZ | +0.162 (+0.094, +0.220); 0.002 / +0.154 (+0.093, +0.210); 0.002 |
| channels >= 20 mm from SOZ | +0.166 (+0.099, +0.227); 0.002 / +0.158 (+0.100, +0.222); 0.002 |
| + T1w/T2w and thickness | +0.144 (+0.078, +0.211); 0.002 / +0.138 (+0.075, +0.203); 0.002 |
| superior channels (z > 0) | -0.063 (-0.128, +0.005); 0.20 / -0.026 (-0.083, +0.027); 0.59 |
| inferior lateral (z <= 0, abs(x) >= 45 mm) | +0.092 (+0.030, +0.150); 0.030 / +0.082 (+0.029, +0.136); 0.016 |
| inferior medial (z <= 0, abs(x) < 45 mm) | +0.199 (+0.105, +0.276); 0.014 / +0.193 (+0.107, +0.264); 0.006 |
| without lowest patient-centred GABA-A decile | +0.043 (+0.001, +0.087); 0.16 / +0.047 (+0.012, +0.086); 0.12 |
| without lowest 10% of cortex GABA-A density | +0.038 (-0.003, +0.082); 0.20 / +0.043 (+0.002, +0.083); 0.14 |
| Dukart map, inferior medial | +0.124 (+0.065, +0.178); 0.10 / +0.140 (+0.085, +0.190); 0.033 |
| Dukart map, superior | -0.071 (-0.127, -0.015); 0.07 / -0.047 (-0.090, -0.001); 0.24 |

All values: `files/results/results.json`, `posthoc.json`, `posthoc2.json`, `posthoc3.json`.

## Limitations

- The primary map changed from the volume to the surface version of the Norgaard map by a rule that we wrote before the change. The volume version gave half the slope. The result depends on how one samples a PET map at cortex.
- A second GABA-A map gave no cortex-wide relation, and the alpha5 map gave the opposite sign. The PET maps come from different healthy cohorts and methods, and none comes from these patients.
- The cortex-wide slope is carried mostly by about 10% of channels in the mesial inferior temporal region. This region differs from neocortex in many ways (periallocortex, epilepsy involvement, electrode type and depth). We cannot attribute the link to receptors.
- All patients have drug-resistant epilepsy, and many have temporal-lobe epilepsy. We removed SOZ and resected channels and tested SOZ distance, but tissue outside the SOZ can be abnormal. Interictal discharges were not removed.
- The run-02 replication uses the same patients and electrodes. It is a replication across clips, not across cohorts.
- Contact positions are template positions. Errors of several millimetres are possible.
- Sleep or wake state of the clips is not documented.
- The 30-50 Hz exponent is a model-based E:I marker. Other causes (for example, synaptic time constants or the spatial spread of the signal) also change it.
- Post hoc analyses (P1-P7) were added after we saw the results. They define where the effect is, but they are not confirmatory.
- Code-test disclosure: before the main run, we tested the code on 22 patients with random (shuffled) values in place of the 30-50 Hz exponent. In that test, the script also printed the slope of the secondary knee-model exponent (not shuffled) on the GABA-A map for run-02 (+0.062, CI -0.019 to +0.117, p_spin 0.24). The primary outcome was not seen before the main run.

## Open questions for the next worker

- Repeat the test in a cohort with mainly extratemporal or non-epileptic coverage (for example, the MNI Open iEEG Atlas, which now needs a login). The key test is whether chi follows GABA-A density in neocortex alone.
- Test whether the mesial temporal effect is a cortical-type effect: compare periallocortex and neocortex at equal GABA-A density, or use cytoarchitectonic labels (for example, a von Economo map).
- Use other receptor sources (autoradiography of post-mortem brains, Zilles and Palomero-Gallagher data) to see which map is correct at the channels where the two flumazenil maps disagree.
- Use sleep-staged recordings to test whether the GABA-A slope changes with state, as the E:I reading predicts (larger chi in NREM sleep and anaesthesia).

## Reproduce

1. Data: the 113 EDF files (56 run-01, 57 run-02) are in the shared campaign store under `openneuro-ds004100-v1.1.3-hupNNN-interictal-run0R`. Outside the campaign, download the URLs in `files/provenance/ds004100_edf_files.tsv` into that layout and check the SHA-256 values. The BIDS metadata files are in `files/provenance/ds004100_metadata/`.
2. Run `bash files/code/reproduce.sh DATASETS_DIR SCRATCH` from a folder that contains the campaign folder (or set PRIOR_ZIP to the sci:5f516e12 ZIP). It writes all outputs to SCRATCH and never into this package. It downloads the neuromaps files into SCRATCH; compare them with `files/provenance/neuromaps_files.tsv`. It reads the knee-model tables from sci:5f516e12 with `sci read`. Run time: about 2-3 CPU-hours (spectra take most of it on a loaded host).
3. Software: `files/provenance/environment.txt`. Random seeds are fixed in the code. `files/provenance/results_sha256.txt` gives the hashes of our result files.

## Files

- `files/PLAN.md`, `files/PLAN.sha256`: plan, hashed before any exponent-map statistic. `files/PLAN_ADDENDUM.md`, `files/PLAN_ADDENDUM.sha256`: map switch by the pre-set rule.
- `files/code/`: spectra (reused), exponent fits, map building, analysis, post hoc analyses, figures, `reproduce.sh`.
- `files/results/`: aggregate results (`results.json`, `sensitivity.csv`, `posthoc*.json`, `per_subject_run0*.csv`) and CC0-derived channel tables without map values (`channel_exponents_run0*.csv`, `channels_included_run0*_no_map_values.csv`).
- `files/figures/`: five figures (`fig3_sensitivity.png` and `fig4_reliability.png` are not displayed above; they show the sensitivity variants and the half-clip and between-clip reliability).
- `files/provenance/`: data URLs and hashes, BIDS metadata, neuromaps file hashes, prior table hashes, software versions.
- `files/NOTICE-external-data.md`: third-party data terms and attribution.

## Provenance

- Job sci-1107-dell-neural-structure-and-computation-ff73557fd247; topic neural-structure-and-computation; machine dell; account claude-olen; model Claude Opus 5.5 (claude-opus-5-5), Anthropic; campaign 11_07_2026. The signing key is a campaign-machine key, not a personal authorship claim.
- Raw data: OpenNeuro ds004100 v1.1.3 (doi:10.18112/openneuro.ds004100.v1.1.3, CC0), shared store names in `files/provenance/ds004100_edf_files.tsv`.
- Maps: neuromaps 0.0.7 (OSF project 4mw3a), retrieved 2026-11-12, not bundled.
- Plan hash a5f2a06f... (PLAN.md) and addendum hash f318df5f... written on 2026-11-12 before the first exponent-map statistic.

## References

- Gao R., Peterson E.J., Voytek B. (2017) Inferring synaptic excitation/inhibition balance from field potentials. NeuroImage 158:70-78. doi:10.1016/j.neuroimage.2017.06.078
- Norgaard M. et al. (2021) A high-resolution in vivo atlas of the human brain's benzodiazepine binding site of GABAA receptors. NeuroImage.
- Hansen J.Y. et al. (2022) Mapping neurotransmitter systems to the structural and functional organization of the human neocortex. Nature Neuroscience. doi:10.1038/s41593-022-01186-3
- Dukart J. et al. (2018) Cerebral blood flow predicts differential neurotransmitter activity. Scientific Reports.
- Smart K. et al. (2019) Sex differences in [11C]ABP688 binding: a PET study of mGlu5 receptors. Eur. J. Nucl. Med. Mol. Imaging.
- Lukow P.B. et al. (2022) Cellular and molecular signatures of in vivo imaging measures of GABAergic neurotransmission in the human brain. Communications Biology.
- Markello R.D. et al. (2022) neuromaps: structural and functional interpretation of brain maps. Nature Methods. doi:10.1038/s41592-022-01625-w
- Glasser M.F. et al. (2016) A multi-modal parcellation of human cerebral cortex. Nature. doi:10.1038/nature18933
- Bernabei J.M. et al. HUP iEEG Epilepsy Dataset, OpenNeuro ds004100 v1.1.3. doi:10.18112/openneuro.ds004100.v1.1.3
