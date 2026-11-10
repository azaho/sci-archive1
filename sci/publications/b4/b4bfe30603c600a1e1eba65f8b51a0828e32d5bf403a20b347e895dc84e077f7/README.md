# Thalamus-to-visual-cortex spike links in the mouse follow tracer axon density only in a compressed form, and LP gives fewer links to V1 than to higher visual areas

Job: `sci-1107-dell-neural-structure-and-computation-c2c040314861` (campaign 11_07_2026). Topic: neural structure and computation. Machine: dell. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a claim of personal authorship.

## 1. Question

Anterograde tracer experiments give the mesoscale axon density from each thalamic nucleus to each cortical area. Neuropixels recordings give short-latency spike links between single units. Do these two scales agree?

We tested this on the two thalamic nuclei of the mouse visual system and six visual cortical areas:

- LGd (dorsal lateral geniculate nucleus) sends most of its axons to V1 (VISp). Its axon density in V1 is about 40 to 900 times its density in the higher areas.
- LP (lateral posterior nucleus, mouse pulvinar) sends axons to V1 and to all higher areas (LM = VISl, RL = VISrl, AL = VISal, PM = VISpm, AM = VISam). In V1, most LP axons end in layer 1 and layer 5.

Pre-specified tests:

1. **Thalamus leads (main test).** The rate of thalamus-leading spike links (cortical spike +1 to +4 ms after the thalamic spike) increases with the tracer density from the nucleus to the area. Primary model: two-way fixed effects (nucleus and area), so that only the nucleus-by-area pattern can give the slope.
2. **Cortex leads.** The rate of cortex-leading links (-4 to -1 ms) increases with the tracer density from the area to the nucleus.
3. **Target layer.** For each nucleus, the layer distribution of the linked cortical units follows the layer distribution of the tracer-labelled axons.

Campaign work before this study found no relation between tracer density and fast spike links between cortical areas (`1b49edfb`, `8652596e`). An LGN-to-V1 study (`2c36aa37`) found that LGd links go mostly to fast-spiking layer 4 cells and used LP-to-V1 pairs as a low-rate control. This study adds the thalamus-to-cortex and cortex-to-thalamus routes, with large anatomical contrasts.

## 2. Data

| Data set | Sessions (one per mouse) | LGd units | LP units | Cortical units (6 areas) | Thalamus-cortex pairs |
| --- | --- | --- | --- | --- | --- |
| Allen Brain Observatory Visual Coding Neuropixels (VC; passive viewing) | 46 | 1,311 | 2,527 | 12,997 | 1,049,307 |
| Allen Visual Behavior Neuropixels (VBN; change-detection task and passive replay) | 69 (first eligible session of each mouse) | 1,048 | 1,259 | 22,747 | 768,943 |

- Unit filter: Allen `quality == good`, ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9 (VBN also `valid_data`), at least 100 spikes in the analysis window. Session filter: at least 5 thalamic (LGd + LP) and 10 cortical units.
- Analysis window: from the first to the last stimulus epoch (VBN includes the task and the passive replay). We removed all invalid intervals and the optotagging epoch.
- Fast-spiking (FS) cortical unit: waveform duration < 0.4 ms. Layer: Allen CCF 2017 annotation (10 um) at the unit CCF coordinate; if no layer label, the relative depth inside the area on that probe.
- Anatomy: Allen Mouse Connectivity Atlas, through the Allen Brain Atlas API (projection-structure unionizes, ipsilateral hemisphere). Density = normalized projection volume (projection volume in the target / injection volume). We found that many "LP" injections also label LGd and many "LGd" injections also label LP (up to 44% of the injection volume). Thus, before we fitted any model on the full data, we selected the **clean-injection** estimate as primary: experiments with >= 50% of the injection in the named nucleus, < 5% in the other nucleus, < 5% in isocortex, and no Gad2-Cre line (12 LGd and 7 LP experiments; median per route). Alternatives: an unmixing fit (non-negative least squares over LGd, LP and other injected volume, 39 experiments), the median of all experiments, and the Knox et al. (2019) voxel-model region matrix. For the cortex-to-thalamus direction we used the median of all experiments with a primary injection in each area (18 to 283 per area) and the Knox matrix. Layer shares: median share of the labelled axon volume of the area in each layer (clean injections).

## 3. Method

- **CCG.** For each thalamic unit and each cortical unit of the same session: cross-correlogram, +-50 ms, 0.5 ms bins. Baseline: partially hollow Gaussian (SD 10 ms, hollow fraction 0.6; Stark and Abeles 2009).
- **Link.** Thalamus leads: the largest bin at +1 to +4 ms is above the baseline (Poisson p < 0.001, Bonferroni over 6 bins) and above the largest bin at -4 to -1 ms (p < 0.0026). Cortex leads: the mirror test. These are the rules of `2c36aa37`.
- **Variants.** Strict thresholds (p < 1e-5 and 1e-4); a sharp baseline (SD 3 ms) that removes broad co-firing and rhythms; a 1 to 7 ms window; pairs on different probes only; and a **control lag** (the same test at +21 to +24 ms against -24 to -21 ms). No monosynaptic peak is expected at the control lag, so it measures how much broad, asymmetric co-firing alone can give.
- **Models.** Logistic regression of link (yes/no) per pair: log10 density + nucleus fixed effect + area fixed effect (primary, "two-way FE") or nucleus only ("nucleus FE"), plus log spike counts of both units, FS cortical unit, and session fixed effects. Standard errors clustered by mouse. To keep the fits fast, each fit used all links and 25 random non-links per link (case-control sampling; the slope stays consistent and the sampling constant goes into the fixed effects). Cell-level permutation test: we fitted one effect per nucleus-area route (12 routes), then permuted the 6 area densities inside each nucleus (720 x 720 = 518,400 relabellings) and re-computed the two-way-FE slope.
- **Analyses added after first results** (exploratory, defined after we saw the results of a partial run on 11 VC sessions): models without V1, models for each nucleus alone, the V1-versus-higher-area contrast for each nucleus, and the leave-one-area-out slope.

## 4. Results

### 4.1 Link rates per route

Thalamus leads (+1 to +4 ms). Control = same test at the +21 to +24 ms control lag.

| Route | Tracer density (clean) | VC pairs | VC links (%) | VC control (%) | VBN pairs | VBN links (%) | VBN control (%) |
|---|---|---|---|---|---|---|---|
| LGd to V1 | 5.45 | 86,402 | 415 (0.480) | 0.164 | 62,649 | 341 (0.544) | 0.198 |
| LGd to LM | 0.123 | 39,016 | 39 (0.100) | 0.054 | 62,848 | 252 (0.401) | 0.286 |
| LGd to RL | 0.0606 | 60,824 | 100 (0.164) | 0.081 | 39,991 | 97 (0.243) | 0.087 |
| LGd to AL | 0.032 | 46,425 | 39 (0.084) | 0.045 | 61,781 | 288 (0.466) | 0.191 |
| LGd to PM | 0.0398 | 45,318 | 21 (0.046) | 0.035 | 66,641 | 88 (0.132) | 0.141 |
| LGd to AM | 0.00595 | 70,699 | 69 (0.098) | 0.035 | 58,402 | 39 (0.067) | 0.122 |
| LP to V1 | 0.904 | 164,756 | 72 (0.044) | 0.043 | 77,247 | 94 (0.122) | 0.056 |
| LP to LM | 0.404 | 90,047 | 151 (0.168) | 0.043 | 71,597 | 215 (0.300) | 0.035 |
| LP to RL | 0.175 | 123,805 | 107 (0.086) | 0.033 | 46,893 | 69 (0.147) | 0.038 |
| LP to AL | 0.265 | 104,071 | 75 (0.072) | 0.033 | 71,284 | 173 (0.243) | 0.041 |
| LP to PM | 0.431 | 79,075 | 42 (0.053) | 0.028 | 78,419 | 85 (0.108) | 0.031 |
| LP to AM | 0.242 | 138,869 | 60 (0.043) | 0.031 | 71,191 | 58 (0.082) | 0.038 |

In total: VC 1,190 thalamus-leading links (0.11% of pairs), VBN 1,799 (0.23%). Figure 1 shows the rates against density. Figure 2 shows the pooled CCGs of the detected links. In VC, the links from LP to LM, RL and AL have a sharp peak at 1.5 to 2.5 ms, which agrees with a monosynaptic connection. In VBN the pooled peaks are wider.

### 4.2 Test 1: thalamus-leading links increase with tracer density, but much less than density

| Model (outcome: thalamus-leading link) | VC odds ratio per 10-fold density (95% CI) | VBN odds ratio per 10-fold density (95% CI) |
| --- | --- | --- |
| **Primary: two-way FE, clean-injection tracer** | **2.59 (1.58-4.24), p = 0.0002** | **1.92 (1.47-2.52), p = 2e-6** |
| Cell-level permutation (518,400), one-sided p | 0.045 | 0.0013 |
| Nucleus FE only | 1.71 (1.27-2.29) | 1.47 (1.26-1.71) |
| Unmixed (NNLS) tracer density | 3.41 (1.80-6.44) | 2.33 (1.63-3.33) |
| All-injection tracer median | 3.21 (1.70-6.05) | 2.28 (1.63-3.18) |
| Knox 2019 model density | 8.4 (0.32-225), p = 0.20 | 17.8 (3.3-97) |
| Sharp baseline (SD 3 ms) | 2.17 (1.31-3.59) | 1.57 (1.04-2.36) |
| Strict thresholds | 3.66 (1.19-11.3) | 2.23 (1.41-3.54) |
| 1 to 7 ms window | 2.66 (1.64-4.32) | 1.96 (1.49-2.58) |
| Different-probe pairs only | 2.11 (1.24-3.61) | 1.77 (1.33-2.34) |
| Control lag +21 to +24 ms (null check) | 1.66 (1.32-2.08) | 0.91 (0.67-1.22) |

The pre-specified test passed in both data sets and with all tracer estimates. The Knox matrix gives a weak contrast between LGd-to-V1 and LGd-to-LM (equal values), so its slope is very uncertain. The effect is **compressed**: the odds of a link increase with density to a power of about 0.2 to 0.4 (slope in natural-log units 0.17 to 0.41). Across the 12 routes, tracer density spans a factor of about 900. The link rates span a factor of about 10.

In VC, the control lag also gave a positive slope (1.66). Thus part of the VC slope comes from broad, asymmetric co-firing, which is strongest for LGd and V1 (Figure 1, open markers). The sharp-baseline variant, which removes most of this co-firing, kept the effect in both data sets.

### 4.3 Where the density rule holds and where it fails (exploratory)

V1-versus-higher-area contrast for each nucleus (odds ratio of a link in V1 relative to the mean of the five higher areas; the same pair-level controls):

| Nucleus | Tracer density ratio V1 / higher areas (clean) | VC odds ratio (95% CI) | VBN odds ratio (95% CI) | VC sharp baseline | VBN sharp baseline |
| --- | --- | --- | --- | --- | --- |
| LGd | about 150 | 4.05 (2.33-7.05) | 2.60 (1.68-4.02) | 3.25 (1.70-6.22) | 2.61 (1.48-4.58) |
| LP | about 3.1 | **0.49 (0.34-0.71)** | 0.77 (0.53-1.10) | **0.56 (0.40-0.77)** | 0.91 (0.52-1.58) |

- **LGd** gives more links to V1 than to the higher areas, as the anatomy predicts. But the difference is only 2.6 to 4 times, not 150 times. LGd units also link to higher areas at 0.05 to 0.47% of pairs. In VBN, many of these LGd-to-higher-area links are near the control-lag rate.
- **LP to V1 is the main exception.** All tracer estimates give LP a denser projection to V1 than to any higher area. But LP-to-V1 pairs had fewer links than LP-to-higher-area pairs (VC odds ratio 0.49; VBN 0.77, CI includes 1). In VC the LP-to-V1 link rate (0.044%) is equal to its control-lag rate (0.043%). Thus, for LP, the dense V1 projection does not give detectable fast spike links.
- **Without V1** (five higher areas only), the two-way-FE slope was not significant (VC 0.78, 0.26-2.28; VBN 1.44, 0.81-2.53). Leave-one-area-out: when we removed V1, the VC slope changed sign (-0.47 log-odds per log10 density); the VBN slope stayed positive (0.63). Removal of any other area did not change the sign. Thus, in VC, the pre-specified result depends on the LGd-to-V1 route.
- **Inside LP, among higher areas only**, density predicted links in VBN (odds ratio 3.1 per 10-fold density, 1.3-7.5, p = 0.01; NNLS density 8.8, 3.4-22.9) and gave a positive but not significant estimate in VC (3.9, 0.7-22; NNLS 6.7, 2.0-22.1). With the sharp baseline neither data set was significant.

### 4.4 Test 2: cortex-leading links do not follow anatomy and fail a validity check

| Model (outcome: cortex-leading link) | VC | VBN |
| --- | --- | --- |
| Two-way FE, tracer density area to nucleus | 1.40 (0.88-2.23), p = 0.15 | 1.14 (0.79-1.62), p = 0.49 |
| Cell-level permutation, one-sided p (tracer; Knox) | 0.22; 0.19 | 0.29; 0.13 |
| Knox density, two-way FE | 2.58 (0.77-8.6) | 2.20 (0.75-6.5) |
| Different-probe pairs, two-way FE | 1.30 (0.82-2.07) | 0.99 (0.69-1.41) |

The pre-specified test failed. Cortex-leading link rates (VC 0.02-0.15%, VBN 0.05-0.25%) were close to the control-lag rates of the same routes (VC 0.01-0.09%, VBN 0.04-0.22%). Corticothalamic axons come from pyramidal cells in layers 5 and 6. But FS cortical units had more cortex-leading links than regular-spiking units (odds ratio 1.52 in VC, p = 0.03; 1.61 in VBN, p < 0.001), and layer 5 and layer 6 regular-spiking units did not differ (interaction with nucleus: VC 0.95, VBN 0.90). Thus most cortex-leading peaks are probably shared input or co-firing, not corticothalamic connections. This CCG method cannot measure corticothalamic connections in these data.

### 4.5 Test 3: target layers

- **LGd to V1:** layer 4 had the highest link rate in both data sets (VC 0.89%, VBN 0.99%). Relative to layer 4: layer 5 odds ratio 0.33 (VC) and 0.35 (VBN), layer 6 0.18 and 0.43. Tracer axons are spread across layers 2/3 to 6 (28%, 30%, 19%, 20%), so the links prefer layer 4 more than the axon volume does. This repeats `2c36aa37`.
- **LGd to higher areas:** most tracer-labelled LGd axon volume is in layer 6 (median 53%). The link rates were similar in all layers (VBN) or highest in layer 2/3 (VC, odds ratio 3.8 relative to layer 4).
- **LP:** LP axons are mostly in layers 1 and 5 (V1: 33% and 24%; higher areas: 24% and 31%). Links had no clear layer preference (all layer odds ratios relative to layer 4 had p > 0.06). Only 7 units had a CCF layer 1 label, and the layer analysis excluded layer 1, so we cannot test the layer 1 input.
- FS cortical units received more thalamus-leading links than regular-spiking units in all routes (odds ratio 4.1 in VC, 2.9 in VBN).

Figure 4 shows the rates by layer.

## 5. Interpretation

At the level of whole routes, mesoscale tracer density predicts the rate of fast thalamus-to-cortex spike links in the awake mouse, in passive and task data sets, with several detection rules and tracer estimates. This differs from the cortex-to-cortex null result of `1b49edfb` and `8652596e`, probably because the thalamic routes have much larger anatomical contrasts. But the relation is weak and compressed: a 10-fold increase in axon density gives only a 1.5 to 2.6 times increase in the odds of a link.

The data show two limits of axon density as a predictor of functional input:

1. LP axons to V1 are dense but end mostly in layer 1 and layer 5a, on distal dendrites. Such inputs can be strong in total but invisible to a spike CCG of single pairs. LP axons to the higher areas gave more and sharper links. Thus the location of the synapses on the target cell, not only the axon volume, controls the detectable spike transmission.
2. LGd links to the higher areas occur at rates far above what the very low axon density predicts. Some are probably broad co-firing (VBN control-lag rates are high), and some can come from LGd shell cells or disynaptic paths.

The cortex-to-thalamus direction cannot be measured with this method. Cortex-leading peaks occur near the control rate and come more from FS cells, which do not project to the thalamus.

## 6. Limitations

- A CCG peak is a putative link, not a proven synapse. Shared input, rhythms (LGd shows a ~60 Hz rhythm) and slow co-firing can give peaks. The control lag and the sharp baseline show that broad co-firing contributes, mainly for LGd routes and in VC.
- There are only 2 nuclei x 6 areas = 12 routes. The route-level tests have few degrees of freedom, and in VC one route (LGd to V1) controls the primary result.
- Tracer densities come from other mice, from a few experiments per nucleus (12 LGd and 7 LP clean injections), and from Cre lines with different labelled populations. The clean-injection rule was our choice. The three tracer estimates agree on the order of routes, but the Knox voxel model does not.
- Probe positions were not matched in retinotopy across areas. RF overlap can change link rates (`2c36aa37` found a graded RF-distance effect).
- Detection depends on spike counts. All models control for log spike counts, but residual power differences between areas and nuclei can remain.
- FS/RS class is from waveform width. Layer labels come from CCF registration and can be wrong near boundaries; layer 1 is almost not sampled.
- Case-control sampling of non-links adds a small random component to each estimate (seed fixed).
- The exploratory analyses in section 4.3 were defined after we saw partial results. Treat them as hypotheses.

## 7. Files

| Path | Content |
| --- | --- |
| `files/code/` | Full pipeline (Python 3.12 with numpy, scipy, pandas, pyarrow, statsmodels, h5py, requests, matplotlib). `run_all.sh` runs all steps. `httpfile.py` and the CCG rules come from `2c36aa37`. |
| `files/results/vcn_stats.json`, `vbn_stats.json` | Route-level rates with mouse-bootstrap CIs, route effects, all model estimates, permutation results, layer analyses. |
| `files/results/*_contrasts.json` | V1-versus-higher-area contrasts per nucleus (section 4.3). |
| `files/results/*_print.txt` | Console output of the statistics and assembly scripts. |
| `files/results/*_pooled_ccg.npz` | Sums of CCG counts and baselines over all pairs and over detected links, per direction, nucleus, area and FS class (Figure 2). |
| `files/results/anatomy_route_summary.csv` | Our route-level tracer summaries (clean, NNLS, all-experiment medians, layer shares, cortex-to-thalamus medians by Cre line). It does not include the Knox matrix values. |
| `files/figures/` | Figures 1-4. |
| `files/provenance/` | URLs, sizes and ETags of the 115 NWB files; SHA-256 of all metadata tables, the CCF annotation, the Knox matrix and the cached Allen API responses that we used. |
| `files/NOTICE_external_data.md` | Terms and attribution for the Allen Institute data, which this bundle does not contain. |

Record-level derived tables (spike times, per-unit and per-pair tables, per-experiment tracer values) are not in this bundle, because the Allen Institute Terms of Use permit derivative works only for noncommercial purposes. The code regenerates them in a separate scratch folder.

## 8. How to reproduce

```bash
export THX_WORK=/path/to/scratch        # never the publication folder
cp -r files/code "$THX_WORK/code"
NPROC=8 bash "$THX_WORK/code/run_all.sh"
python "$THX_WORK/code/09_summarize.py" vcn vbn
```

The run reads about 15-25 GB by HTTP range requests from the public Allen S3 buckets (1-9 min per session) and makes about 3,000 small Allen Brain Atlas API requests in batches. The CCG step takes about 1-3 CPU-minutes per session. The statistics take about 10-40 min per data set. Compare the hashes and ETags with `files/provenance/`. In this campaign, the VC units and channels tables, the CCF annotation and the Knox matrix came from the shared campaign datasets `allen-vcn-ecephys-units-20261109`, `allen-vcn-ecephys-channels-20261109`, `allen-ccf2017-annotation10-20261109` and `knox2019-normalized-connection-density-20261109` (same SHA-256 as in `metadata_sources.csv`); `00_download_metadata.sh` downloads them from the original URLs if these copies are not present. Allen API responses can change if Allen updates the atlas; the hashes of the responses we used are recorded.

## 9. Related campaign work

- `2c36aa37`: LGN-to-V1 connection rules in the same data sets (method source).
- `1b49edfb`, `8652596e`: tracer density did not predict fast spike links between cortical visual areas.
- `cc2969a4`: in vivo class-specific connectivity from optotagged CCGs.
- `6ea87a03`: LGd/LP versus cortex in Fano-factor quenching in VC/VBN.
