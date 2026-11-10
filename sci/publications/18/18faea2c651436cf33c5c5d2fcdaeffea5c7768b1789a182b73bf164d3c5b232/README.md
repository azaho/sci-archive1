# The MICrONS in-degree link to calcium timescale repeats, but it follows the signal fraction of the trace; after controls, more inputs do not give longer timescales

Job: sci-1107-dell-neural-structure-and-computation-f7d7f9751e97. Topic: neural-structure-and-computation. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Zenari et al. (2026, arXiv:2603.04149) give a theory in which neurons with a higher in-degree have slower activity (longer intrinsic timescales). As data support, they report that in the MICrONS mouse visual cortex dataset, proofread neurons with a higher in-degree have a wider autocorrelation of the raw calcium trace during the monitor-off period (Spearman rho about 0.16, p about 1e-4). They report no controls.

We repeated the measurement on 12,726 functionally matched excitatory neurons in 13 MICrONS scans. We then tested if the relation stays after controls for imaging signal quality, activity, cell type, position and scan.

Main results:

1. **The published correlation repeats.** In 890 neurons with proofread dendrites, the in-degree from nucleus-attached neurons with extended axons has Spearman rho = 0.163 (p < 1e-5) with the half-width at half-maximum (HWHM) of the autocorrelation. The published value is 0.164.
2. **The HWHM measures the signal fraction of the trace, not a decay time.** Imaging noise lowers the autocorrelation at all lags above zero. The HWHM is therefore set mostly by the autocorrelation at lag 1 (ACF1, the signal fraction of the variance): Spearman 0.96 over neurons (Fig. 1b). For 50% of the neurons, ACF1 is below 0.5 and the HWHM is shorter than one imaging frame (0.16 s). In a model with the same true decay time, the HWHM changes about tenfold when only the noise changes (Fig. 1a).
3. **In-degree predicts the signal fraction, and this gives the published correlation.** In each of the 13 scans, the in-degree correlates with HWHM almost exactly as it correlates with ACF1 (difference at most 0.02; Fig. 1c). When we add ACF1 to the model, the in-degree slope on log HWHM goes from +0.162 (95% CI 0.088 to 0.237) to -0.009 (-0.035 to 0.016) in proofread neurons. In all neurons it goes from +0.123 to -0.021 (Fig. 2). ACF1 also contains part of the timescale. Thus, we also used a control set without the autocorrelation: brightness, activity sparseness, oracle-clip reliability, cell type, area, position and nucleus volume. With these controls, the slope is +0.001 (-0.021 to 0.023) in all neurons and -0.020 (-0.069 to 0.029) in proofread neurons.
4. **A noise-robust timescale does not increase with in-degree.** We normalized the autocorrelation at lag 1 instead of lag 0, which removes white imaging noise. We then measured the time to half of that value. This decay time has a median of 2.2 s. It has no raw correlation with in-degree (rho = 0.005 in all neurons; 0.037, p = 0.28, in proofread neurons). After all pre-set controls the slope is small and *negative*: -0.104 (-0.135 to -0.073) in all neurons, -0.089 (-0.178 to -0.000) in proofread neurons, and negative in layer 2/3 and layer 4 neurons separately. The pre-set test for support of the theory (positive slope, CI above zero, same sign in L2/3 and L4) failed. When we also control for the total number of input synapses (dendrite size), the in-degree slope is -0.025 (-0.093 to 0.044). Thus, the number of presynaptic partners has no clear effect beyond dendrite size.
5. **Other measures agree.** Excitatory in-degree, inhibitory in-degree, all-nucleus in-degree and synapse counts gave no positive slope on the spontaneous timescale (Fig. 3). On residuals of repeated movie clips (trial minus repeat mean), the in-degree slope was +0.030 (-0.007 to 0.066). After removal of 5 population modes it was +0.025 (-0.020 to 0.070). The in-degree from the 148 axon-proofread functional neurons of Ding et al. had no positive correlation with HWHM (rho = -0.049 in all neurons, 0.007 in proofread neurons).

Conclusion: in this dataset, the in-degree/timescale correlation in calcium data is not evidence that in-degree sets intrinsic timescales. The correlation is explained by the signal fraction of the trace, together with cell type, position and brightness. With a noise-robust measure and controls, neurons with more inputs do not have longer timescales. If anything, they have slightly shorter ones. This result does not test the theory itself. It removes one empirical support for it.

## Pre-registration and changes

PLAN.md was written before any timescale was computed. Its SHA-256 and UTC time are in files/provenance/PLAN.sha256.txt. We stated before the analysis that the raw HWHM depends on noise. We saw that in the first scan (HWHM vs ACF1 rho 0.997) before the anatomy-activity join. The tests in files/code/05_models.py follow the plan. Changes and additions:

- **Added after the pre-set models (exploratory):** files/code/06_sensitivity.py. S1 is the control set without the autocorrelation. S2 is a spline for ACF1. S3 excludes censored decay times and ACF1 < 0.1. S4 models ACF1 as the outcome. S5 is split-half reliability. S6 gives per-scan correlations. Reason: ACF1 contains part of the true timescale, so a control by ACF1 alone can remove a real effect. S1 shows that the HWHM result does not depend on that control.
- **Bug fix:** the first run of 05_models.py also listed ACF1 as a secondary outcome while ACF1 was a covariate. These rows had slope 0 by construction and unstable p-values. We removed them before we wrote the text. ACF1 as an outcome is in S4.
- "Proofread neurons" in Zenari et al. means neurons with proofread axons and dendrites (MICrONS release v1412). The public static exports have no axon-proofreading table. We used (a) neurons with proofread dendrites (v1507 flag) as the sample and (b) presynaptic nucleus-attached neurons with at least 1,000 output synapses in the v1300 graph (3,327 neurons) as a proxy for the proofread presynaptic set. Our replication value (0.163) is very near the published value, but the sets are not the same.

## Data

- MICrONS minnie65 (one mouse, about 1 mm^3 of V1, RL and AL). Functional matching and unit ids from the Ding et al. 2025 node table (12,894 neurons in 13 scans). Fluorescence traces from DANDI:000402. We read only the fluorescence chunks by HTTP byte ranges (files/code/01_extract_scan.py, adapted from SCI e9455e37).
- Wiring from the v1300 CAVE export `connections_with_nuclei` (303,245,723 pre-post root pairs). Presynaptic E/I type from the Allen soma E/I model v1. Cell type, nucleus volume and dendrite proofreading flag from the anatomy table of SCI 4c4b0554 (v1507/v661 tables).
- Exact URLs, versions, hashes and a regeneration recipe: files/provenance/DATA_SOURCES.md.

Scans (session, scan): (4,7) (5,6) (5,7) (6,2) (6,4) (6,6) (6,7) (7,3) (7,5) (8,5) (9,3) (9,4) (9,6). The monitor-off period after the last clip was 535-1,452 s per scan (files/provenance/scan_facts/). Frame interval was 0.159 s, except 0.116 s and 0.104 s in session 9.

## Methods

**Timescales (files/code/03_timescales.py).** Spontaneous epoch: all frames later than 1 s after the last stimulus clip. Raw fluorescence, mean removed and linearly detrended. Biased autocorrelation (ACF) up to 10 s by FFT.
- HWHM: first lag where ACF (normalized at lag 0) is at or below 0.5, linear interpolation.
- Noise-robust decay time: ACF divided by ACF1; time from lag 1 to the first crossing of 0.5, interpolated. This is undefined if ACF1 <= 0.05. It is censored at 10 s (1.9% of neurons; 0.7% undefined).
- Covariates from the same epoch: ACF1; sparseness (fraction of frames with AR(1)-deconvolved signal above 3 robust SD, decay 1 s); mean raw fluorescence.
- Oracle residuals: 6 clips x 10 repeats x 9.5 s. Residual = trial minus repeat mean at the same frame. ACF pooled over the 60 trials, up to 4 s. "Private" residuals: the top 5 principal components of all units of the scan are regressed out.
- Split-half reliability of each measure: first vs second half of the spontaneous epoch.

**Wiring (files/code/02_anatomy.py, 04_join.py).** For each functional neuron (post):
- k_in: the number of distinct nucleus-attached presynaptic neurons;
- k_ext: the same, limited to presynaptic neurons with >= 1,000 output synapses;
- excitatory and inhibitory in-degree and synapse counts, from the soma E/I model;
- total input synapses (all fragments).
Self-connections are removed.

**Models (files/code/05_models.py).** OLS of the z-scored log timescale on the z-scored log(1 + in-degree). Controls are added in steps: scan fixed effects; ACF1; sparseness and mean fluorescence; cell type (23P, 4P, 5P-IT, 5P-ET, 5P-NP, 6P), area, B-splines of depth (df 4) and of the two tangential coordinates (df 3 each); log nucleus volume; log total input synapses. Confidence intervals are cluster-robust by scan (13 clusters). HC3 intervals are also in the tables. Samples: all excitatory neurons; 23P; 4P; dendrite-proofread neurons.

## Figures

- files/figures/fig1_hwhm_is_snr.png: (a) HWHM against signal fraction for fixed true decay times, from a model ACF; (b) observed HWHM against ACF1; (c) per scan, the in-degree correlation with HWHM against the in-degree correlation with ACF1.
- files/figures/fig2_control_sequence.png: in-degree slope as controls are added, for HWHM and for the noise-robust decay time.
- files/figures/fig3_forest_full.png: full-model slopes for 7 wiring predictors and 4 timescale measures.

## Results files

- files/results/h1_spearman.csv: replication correlations.
- files/results/regressions.csv: all pre-set models (step, sample, outcome, predictor, beta, HC3 and cluster CIs).
- files/results/sensitivity.csv: S1-S4.
- files/results/reliability.csv: split-half and cross-measure correlations.
- files/results/per_scan.csv: per-scan correlations.
- files/derived/neuron_table.csv.gz: one row per functional neuron, with timescale measures, covariates and wiring counts. This table is enough to recompute every table and figure.

## Limitations

- One mouse and one dataset. No second connectome with matched activity was available on this machine (the V1DD data used by earlier campaign work is not in the current shared dataset store).
- Calcium imaging at 6-10 Hz with GCaMP6s. The noise-robust decay time still contains the indicator decay. Its split-half reliability is moderate (Spearman 0.35). Its correlation with the oracle-residual decay time is low (0.09), so "timescale" depends on the epoch and the method. A spike-based test is necessary for a final answer.
- The small negative slope of the noise-robust time on in-degree can come from residual measurement effects (this time correlates 0.43 with ACF1). We do not claim that more inputs shorten timescales.
- In-degree in a partly proofread volume is incomplete. Our presynaptic set (nucleus-attached, >= 1,000 output synapses) is a proxy for the proofread set of Zenari et al. Most of these extended axons are inhibitory (median k_ext 86, of which 9 excitatory). Excitatory-only in-degree gave the same result.
- We did not repeat the Zenari HWHM pipeline exactly. Their data release (v1412), coregistration table and normalization (dF/F) differ from ours. Our raw-fluorescence HWHM gave nearly the same correlation, and HWHM is unchanged by a constant scaling of the trace.
- Cluster-robust intervals with 13 clusters can be too narrow. HC3 intervals are given as a check, and the conclusions are the same.

## Reproduce

Quick (no raw data, about 5 minutes): in an empty scratch folder, copy files/code to ./code, then
`python code/00_rebuild_from_table.py <bundle>/files/derived/neuron_table.csv.gz && python code/05_models.py && python code/06_sensitivity.py && python code/07_figures.py`.
We ran this check: all numbers in results/ were reproduced within 1e-5 (rounding of the CSV table).

Full: follow files/provenance/DATA_SOURCES.md. The node map for 01 and 03 is:
`pd.read_pickle('node_data_v1.pkl')[['nucleus_id','brain_area','proofread_status','nucleus_x','nucleus_y','nucleus_z','hva','layer','cc_max_cvt','cc_abs_cvt','cc_norm_cvt','scan_session','scan_idx','unit_id','osi_cvt_monet_full','gosi_cvt_monet_full']].to_parquet('raw/node_map.parquet')`.
Downloads go to local scratch, never into the signed bundle.

## Licence and external data

Our code (MIT), text, figures and derived tables (CC BY 4.0) are under the SCI baseline LICENSE. The derived per-neuron table and the results come from third-party data under CC BY 4.0. See files/NOTICE-external-data.md for the required attribution.
