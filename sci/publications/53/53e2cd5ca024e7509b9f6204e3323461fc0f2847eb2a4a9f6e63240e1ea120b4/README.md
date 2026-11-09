# Cre-line neuromodulatory axon density does not explain where running changes visual spiking in two Allen Neuropixels mouse cohorts

## Summary

When a mouse runs, the visual responses of many neurons change. The size of this change is different between brain regions. We asked a structure–function question: does the density of neuromodulatory axons in a region predict how much running changes the visual responses of the neurons in that region?

We used two public Allen Institute resources:

- **Function.** Allen Brain Observatory Visual Coding Neuropixels (VCN). We used the per-unit running-modulation index `run_mod` from the AllenSDK analysis tables. There are two independent cohorts of mice: "brain_observatory_1.1" (BO1.1, 32 mice, 26 with CCF coordinates) and "functional_connectivity" (FC, 26 mice). No mouse is in both cohorts.
- **Structure.** Allen Mouse Connectivity Atlas anterograde tracing in Cre lines. We made one projection-density map for each system: noradrenaline (LC, Dbh-Cre/Th-Cre, 7 experiments), acetylcholine from the basal forebrain (Chat-Cre, 12), acetylcholine from PPN/LDT (Chat-Cre, 2), serotonin (DR, Slc6a4-Cre, 8), dopamine (VTA, Slc6a3-Cre/Th-Cre, 4) and histamine (TMN, Hdc-Cre, 6). As non-modulatory comparisons we used motor-cortex inputs (MOs, 9; ACA, 10; wild type or Emx1-Cre).

Before the analysis, we wrote down the primary hypothesis (file `files/provenance/PLAN_pre_analysis.md`): noradrenergic and basal-forebrain cholinergic axon density will predict **stronger positive** running modulation, inside each major brain division.

**Main results**

1. **The regional pattern of running modulation is only partly reproducible.** We estimated one effect for each region with mouse fixed effects. Across 38 regions the effects in the two cohorts correlate at r = 0.61 for drifting gratings (r = 0.55 inside divisions), r = 0.62 for Gabor patches and r = 0.42 for flashes. **Inside visual cortex (6 areas × 4 layers), the pattern does not reproduce** (r = −0.10, 0.28 and 0.01). Reproducible differences are mainly in subcortical regions: DG, CA3, MGd and NOT have weaker modulation; visual and auditory thalamus and cortex have stronger modulation (Figure 1).
2. **The primary hypothesis is not supported.** Inside divisions, with injection distance controlled, basal-forebrain ACh density gave partial r = −0.05 (BO1.1), +0.30 (FC) and +0.18 (pooled) for gratings, all with permutation p > 0.1. Noradrenergic density gave r = −0.19, −0.16 and −0.18 (p ≥ 0.2). The NE sign was negative (opposite to the hypothesis) in all 9 cohort × stimulus tests, and significant only for flashes (BO1.1 r = −0.45, Holm p = 0.017; pooled r = −0.48, Holm p = 0.020) (Figure 2).
3. **One map, dopamine (VTA), had a negative association in both cohorts** (gratings: r = −0.47 and −0.57, permutation p = 0.016 and 0.011, Holm p = 0.13 and 0.09). It also gave an out-of-sample gain when we fit on one cohort and tested on the other (within-division R² = 0.25 for gratings, 0.17 for Gabors, 0.00 for flashes). **But this association depends on two regions**, DG and MGd. Without them, r = −0.15 (pooled). VTA dopamine-line axons are near the detection floor in almost all recorded regions (Figure 3). We do not interpret this as a general dopamine rule.
4. **A model with all eight maps did not predict the other cohort better than division means for flashes** and gave small gains for gratings (within-division R² = 0.12) and Gabors (0.03) (Figure 4).

**Conclusion.** In the mouse visual system recorded by Allen VCN, the cell-type-specific density of NE, ACh, 5-HT, histamine and motor-cortex axons does not explain the region-to-region differences in running modulation of visual responses. The pre-stated positive NE and ACh relations were not found; where NE density showed a relation, it was negative. Most of the reproducible regional variance is between divisions and between a few subcortical regions. The area × layer variation inside visual cortex is too small to measure in these data.

## Figures

- `files/figures/fig1_cohort_reliability.png` — region effects in cohort 1 vs cohort 2 for three stimuli.
- `files/figures/fig2_partial_r.png` — within-division partial correlations (injection distance controlled) for each map, cohort and stimulus. Filled markers: permutation p < 0.05 before Holm correction. Lines (gratings only): range of r when one region is removed (division control only).
- `files/figures/fig3_leverage.png` — residual scatter plots for NE, basal-forebrain ACh and VTA DA (pooled gratings). DG and MGd control the DA relation.
- `files/figures/fig4_crossfit.png` — out-of-sample within-division R² (fit on one cohort, test on the other, mean of both directions).

## Methods

**Units.** We joined `units.csv`, `channels.csv`, `probes.csv` and `sessions.csv` from the VCN cache. We used the AllenSDK default unit filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9). We joined the analysis-metrics tables of both session types.

**Running modulation.** AllenSDK `running_modulation()` (allensdk/brain_observatory/ecephys/stimulus_analysis/stimulus_analysis.py, v2.16.2): at the preferred stimulus condition of each unit, trials with mean speed ≥ 1 cm/s are "running". run_mod = (run − stationary)/max(run, stationary) of mean spike counts, range −1 to 1. Stimuli: drifting gratings (`dg`, primary), Gabor patches (`rf`), full-field flashes (`fl`); natural scenes, static gratings and dot motion are only in one cohort.

**Regions.** Visual cortex units (VISp, VISl, VISal, VISrl, VISam, VISpm; probe area label) got a layer from the CCF 2017 10 µm annotation at the unit's CCF coordinate (L2/3, L4, L5, L6 = 6a+6b). Other units kept their probe structure label in thalamus (15 nuclei), hippocampal formation (7), midbrain (6) and ZI. A region needed ≥ 30 units and ≥ 3 mice in a cohort. Six BO1.1 mice have no CCF coordinates and could not contribute.

**Region effects.** For each cohort and stimulus: unit-level least squares, run_mod ~ region + session (mouse) fixed effects + fast-spiking flag (waveform duration < 0.4 ms) + log10 firing rate. Region effects are centred to the unit-weighted mean. We also report plain region medians (`tests_region.csv`, `mouse_bootstrap_median_profile_ci.csv`).

**Projection maps.** For each Cre experiment we read `ProjectionStructureUnionize` (non-injection, hemisphere of the injection) from the Allen API. For each target region: volume-weighted projection density over sub-structures (layer 6 = 6a + 6b). x = log10(density + 10⁻⁴), centred over the target regions inside each experiment (this removes injection size). The system map is the mean over its experiments. Split-half reliability of the maps across experiments: ACh-BF 0.96, ACh-BS 0.97, ACA 0.97, DA 0.87, MOs 0.78, HA 0.75, 5-HT 0.73, NE 0.64.

**Tests.** Partial Pearson r between map and region effect after removal of division means (Isocortex, TH, HPF, MB, HY), and in a second model also the mean distance from the injection sites and its square. P values: 2,000 permutations of the map inside divisions. Holm correction over the 8 maps in each cohort × stimulus × control set. Robustness (`robustness_dg.csv`): other density transforms (log with 10⁻⁵, rank, projection energy), removal of DG and MGd, removal of the hippocampal formation, region jackknife. Out-of-sample test (`crossfit.csv`): fit division means plus one map (or a ridge model with all maps, λ by leave-one-out) on one cohort, predict the other cohort.

## Limitations

- **Few regions.** There are 35–42 regions per test, and divisions take much of the variance. The tests have power only for large within-division correlations (|r| ≳ 0.35).
- **Reliability ceiling.** The within-division cross-cohort correlation of the gratings profile is 0.55. Inside visual cortex there is no reproducible profile, so no structural map can explain it with these data.
- **Tracer maps are coarse.** Projection density includes passing fibres and depends on Cre-line specificity (Th-Cre can label non-noradrenergic or non-dopaminergic cells). Injections are in different mice from the recordings. Some systems have only 2–4 experiments. Density does not measure receptor expression or release.
- **run_mod is a coarse index.** It uses only the preferred condition, a 1 cm/s threshold and the running bouts that each mouse made. It does not separate running from arousal (pupil). 
- **The analysis after the plan.** The mouse-fixed-effect model, the injection-distance control, the robustness set and the cross-cohort fit were added after we saw the low reliability of plain medians. The pre-planned median analysis gives the same conclusions (`tests_region.csv`).
- **Ecological level.** The test is between regions. It does not test whether single neurons with more neuromodulatory input are more modulated.

## Data, licences and what is in this bundle

The bundle contains our code, figures, statistic tables (correlations, p values, R², bootstrap quantiles), the Allen experiment IDs used, the pre-analysis plan and input hashes. **It does not contain Allen data or unit-level or region-level tables derived from Allen data**, because the Allen Institute Terms of Use limit use and derivative works to noncommercial purposes, which is not compatible with the bundle licence. See `files/NOTICE_external_data.md`. All Allen-derived tables are regenerated by the scripts into a separate scratch folder.

## Reproduce

```
bash files/code/run_all.sh /path/to/scratch [/path/to/annotation_10.nrrd]
```

This downloads the VCN cache tables (SHA-256 checked, `files/code/00_fetch_vcn.sh`), the CCF 2017 annotation (SHA-256 checked), and the Allen connectivity API responses (`01_fetch_connectivity.py`; hashes of the 2026-11-09 responses are in `files/provenance/SHA256SUMS_allen_api_responses_20261109.txt`). Then it runs steps 02–10 and writes derived tables to `scratch/derived` and figures to `scratch/figures`. It needs Python 3.12 with numpy, pandas, scipy, pyarrow and matplotlib (versions in `files/provenance/environment.txt`). It takes about 10 minutes on one core. Permutation and bootstrap seeds are fixed. We ran the full pipeline from an empty scratch folder and got the same statistic tables.

On the campaign host the shared copies are `datasets/allen-vcn-ecephys-channels-20261109/channels.csv` (sha256 d2932f1e…) and `datasets/allen-ccf2017-annotation10-20261109/annotation_10.nrrd` (sha256 a9e9654e…).

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-neural-structure-and-computation-35671f3a8732, topic neural-structure-and-computation, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date 2026-11-09. Allen API and S3 data retrieved 2026-11-09.
- Related campaign work: running-state LFP and spike tests in Allen VCN (0dd17ccb, 6ea87a03), retina-distance reliability (19f7eb8e). None of them tested neuromodulatory axon maps against running modulation.
