# Sst and Vip interneurons did not keep natural-movie responses more stable across days than excitatory neurons in two Allen two-photon datasets, but Pvalb neurons did in one dataset

## Summary

Visual responses in mouse cortex change slowly from day to day ("representational drift"). Inhibitory interneurons receive dense input that is not specific for stimulus features, from many local cells (Hofer et al. 2011). If drift comes from changes in individual inputs, pooled input can average out these changes. Thus interneurons can keep more stable responses than excitatory cells. Prior drift studies of the Allen Brain Observatory used only excitatory Cre lines (Deitch et al. 2021).

We measured the stability of natural-movie responses across days for each cell. The metric S is the response similarity between days divided by the similarity of independent trial halves in the same day. S = 1 means that the response changed no more than trial noise. We used two Allen datasets with the same cells on three days:

- **Visual Coding 2P** (passive viewing): 271 imaging fields, 10,263 matched cells, 180 mice, 13 Cre lines (Sst, Vip, Pvalb and 10 excitatory lines), 6 visual areas.
- **Visual Behavior 2P** (task-trained mice, familiar-image sessions 1–3): 146 fields, 4,805 matched cells, 55 mice, Slc17a7, Sst and Vip.

Main results:

1. **Sst and Vip cells were not more stable than excitatory cells.** In Visual Coding (pre-specified primary test, field medians, areas VISp, VISl and VISpm, 226 fields), the difference in S was −0.058 (95% CI −0.131 to +0.016) for Sst and −0.014 (−0.083 to +0.055) for Vip. Cell-level and reliability-matched models gave differences between −0.04 and +0.03. Visual Behavior gave the same result for the natural movie (Sst +0.030, −0.078 to +0.138; Vip −0.005, −0.150 to +0.141). For familiar images, Vip cells were **less** stable (−0.194, −0.270 to −0.119). Sst cells had more stable image responses than excitatory cells only in the cell-level models (+0.150, +0.089 to +0.211). The field-level model did not show this difference (+0.009).
2. **Pvalb cells were more stable** in Visual Coding: +0.139 (+0.070 to +0.208) at field level and +0.165 (+0.107 to +0.223) with reliability deciles. Only Visual Coding has Pvalb data (20 fields, 9 mice), and only these mice have the slower GCaMP6s indicator. Two controls do not explain the difference with the indicator: smoothing of GCaMP6f traces (1 s time constant) left +0.110 (+0.028 to +0.192), and Slc17a7 GCaMP6s cells in Visual Behavior were not more stable than Slc17a7 GCaMP6f cells (−0.068, −0.123 to −0.014; 3 GCaMP6s fields). But the Pvalb result comes from one line, one reporter and two areas.
3. **All three interneuron classes changed their mean activity level less** than excitatory cells between days (absolute log2 ratio of mean dF/F: Sst −0.16, Vip −0.45, Pvalb −0.56 relative to excitatory cells). A lower drift of activity level did not come with more stable response time courses (Vip).
4. **Coupling to the local population** (grey-screen correlation with the mean of other labelled cells) gave a small increase of S in Visual Coding excitatory cells: +0.023 per SD (+0.015 to +0.032; 5,867 cells, 153 fields, with controls for reliability, activity and running modulation). This did not replicate clearly in Visual Behavior (+0.007, −0.003 to +0.016). Interneurons showed no relation.
5. **Elapsed time and state:** S fell by 0.010 per day (−0.016 to −0.004) within the same field. A larger difference in running speed between sessions decreased S (−0.005 per cm/s). In Visual Behavior, session pairs that included the passive session were as stable as the active–active pair (natural movie +0.005, −0.022 to +0.033).
6. **No decrease along the cortical hierarchy:** among excitatory fields, S did not fall from VISp to higher areas (rank slope +0.015, +0.003 to +0.027; VISam was the most stable). This agrees with Deitch et al. (2021).

Interpretation: a dense, unspecific local input is not sufficient to give stable stimulus responses across days. Two interneuron classes with this input type (Sst and Vip) drifted as much as excitatory cells or more. Pvalb cells were the exception in the one dataset that has them. Stability of a cell's response time course and stability of its activity level are separate properties.

## Provenance

- Job: `sci-1107-dell-neural-structure-and-computation-d2d370828ba0`, topic `neural-structure-and-computation`, campaign 11_07_2026, machine `dell`, account `claude-andrii`.
- Model: Claude Opus 5.5 (`claude-opus-5-5`) acting as an autonomous research agent. The signing key is a campaign-machine key. It does not make a claim of personal authorship.
- Analysis dates: 2026-11-08 to 2026-11-09 (PST).
- Pre-specified plan: `files/PLAN.md` (written before the outcome analysis). The deviations are listed below.

## Data

| Dataset | Source | Used |
| --- | --- | --- |
| Allen Brain Observatory Visual Coding 2P (de Vries et al. 2020) | `https://allen-brain-observatory.s3.amazonaws.com/visual-coding-2p/` (NWB v2.0 pipeline files; metadata `experiment_containers.json`) | 874 NWB files = 291 complete containers (271 with ≥3 matched cells) |
| Allen Visual Behavior 2P (Visual Behavior Ophys release) | `https://visual-behavior-ophys-data.s3.amazonaws.com/visual-behavior-ophys/` (`behavior_ophys_experiments/*.nwb`, `project_metadata/*.csv`) | 477 NWB files = 146 complete containers with sessions 1, 2 and 3 |

`files/data/provenance/source_nwb_visual_coding.csv` and `source_nwb_visual_behavior.csv` give the S3 key, byte size, S3 ETag and LastModified of each NWB file that we read. `metadata_sha256.txt` gives the SHA-256 of the metadata files. We did not download complete NWB files. `files/code/01_extract.py` reads only the needed HDF5 chunks by HTTP range requests (logs with bytes read: `files/data/provenance/extract_*.log`). We did not copy raw data to the shared dataset store or to this bundle. The Allen terms apply to the raw data.

**Data cutoff (deviation from plan).** The plan used all 456 passed Visual Coding containers and all 202 Visual Behavior containers with sessions 1–3. Host bandwidth (shared with other jobs) and a host RAM shortage stopped the transfer at 2026-11-09 01:16 PST (Visual Coding) and 01:19 PST (Visual Behavior). We downloaded the interneuron containers first; all 120 passed Sst, Vip and Pvalb containers are complete. For excitatory lines, 161 of 336 containers are complete. The transfer order came from container ID and list position, not from any outcome. One Visual Coding file (501021421) failed after retries and its container is missing.

## Methods

**Response matrices.** For each session, natural movie one (NM1, 30 s, 10 repeats) dF/F was sampled at each movie frame and averaged in 30 bins of 1 s. Visual Coding sessions A, B and C (C2) all contain NM1. Visual Behavior shows NM1 (10 repeats) at the end of every session. For Visual Behavior we also used familiar-image responses: the mean dF/F 0–250, 250–500 and 500–750 ms after each non-change, non-omitted flash, for each of the 8 images (24 values). Cells were matched across sessions by `cell_specimen_id`.

**Stability.** For each cell and session pair (s, t): R_s = correlation between odd-repeat and even-repeat means in session s; B = mean of the four correlations between a half of s and a half of t; S = B / sqrt(R_s R_t), clipped to [−1, 1.5]. Both terms use 5-repeat means, so trial noise affects them equally. Cells with R_s and R_t ≥ 0.3 entered the analysis (sensitivity: 0.2 and 0.5).

**Models.** Weighted least squares with standard errors clustered by mouse.
- Class test (H1): field medians of S, averaged over the three session pairs, regressed on class, area, depth, days, |running difference| and median reliability (primary); cell-level versions with log activity; reliability-decile fixed effects; log matched-cell count; Ai148-reporter-only lines; class × running difference; and within-session halves (first 5 vs last 5 repeats over odd vs even).
- Population coupling (H2): within-field z-scores; S on coupling with field fixed effects, with reliability, activity and running modulation as controls.
- Hierarchy (H3): excitatory fields, S on area rank (VISp < VISl < VISrl < VISal < VISpm < VISam; Harris et al. 2019, Siegle et al. 2021) with Cre and depth.
- Days (H4): session-pair field medians on days and running difference with field fixed effects.
- Indicator checks: GCaMP6f traces passed through a causal exponential filter (τ = 1 s) before binning; Slc17a7 GCaMP6s (Ai94) vs GCaMP6f (Ai93) cells.

## Results tables

All estimates are in `files/data/stats_*/results.json` (`files/code/show.py` prints them). The main ones:

| Contrast vs excitatory (S units) | Sst | Vip | Pvalb |
| --- | --- | --- | --- |
| VC field medians (primary, 226 fields) | −0.058 (−0.131, +0.016) | −0.014 (−0.083, +0.055) | +0.139 (+0.070, +0.208) |
| VC cells | +0.013 (−0.021, +0.046) | −0.037 (−0.077, +0.004) | +0.129 (+0.069, +0.190) |
| VC cells, reliability deciles | +0.013 (−0.020, +0.045) | +0.015 (−0.022, +0.052) | +0.165 (+0.107, +0.223) |
| VC fields, τ = 1 s smoothing | −0.035 (−0.112, +0.041) | −0.023 (−0.096, +0.050) | +0.110 (+0.028, +0.192) |
| VC fields, R ≥ 0.5 | −0.029 (−0.072, +0.014) | −0.040 (−0.098, +0.019) | +0.025 (−0.082, +0.131) |
| VC fields, 0.5 s bins | −0.043 (−0.119, +0.033) | −0.030 (−0.086, +0.025) | +0.138 (+0.070, +0.205) |
| VB natural movie, fields (142) | +0.030 (−0.078, +0.138) | −0.005 (−0.150, +0.141) | – |
| VB natural movie, cells | +0.054 (−0.012, +0.121) | −0.073 (−0.215, +0.070) | – |
| VB familiar images, fields (146) | +0.009 (−0.056, +0.074) | −0.194 (−0.270, −0.119) | – |
| VB familiar images, cells, reliability deciles | +0.088 (+0.028, +0.148) | −0.085 (−0.159, −0.010) | – |

Median field S: Visual Coding excitatory 0.798, Sst 0.868, Vip 0.730, Pvalb 0.917. Visual Behavior natural movie: excitatory 0.918, Sst 0.971, Vip 0.883. The unadjusted Sst median is higher than the excitatory median, but the adjusted contrasts above are near zero. Sst cells were more often reliable (87% of cell-pairs vs 44% for excitatory cells in Visual Coding), and Sst fields are in different areas and depths.

## Figures

- `files/figures/fig0_examples.png`: NM1 responses on three days for one cell per class at the class median S.
- `files/figures/fig1_stability_by_cre.png`: field stability by Cre line (Visual Coding).
- `files/figures/fig2_class_contrasts.png`: class contrasts and sensitivity models (Visual Coding).
- `files/figures/fig3_days_hierarchy.png`: decrease with elapsed days; no decrease along the hierarchy.
- `files/figures/fig4_population_coupling.png`: population-coupling coefficients by class and dataset.
- `files/figures/fig5_visual_behavior.png`: replication in Visual Behavior.

## Limitations

- Each Cre line labels one population. Thus "population coupling" is coupling to other labelled cells of the same class, not to the full local network. It is only a proxy for local input (Okun et al. 2015; for EM support of the proxy see the cited SCI publications). This study did not measure synaptic connectivity.
- Cell class is confounded with field density, area, depth, reporter line and mouse. Adjustment for the log number of matched cells changed the class estimates in opposite directions in the two datasets (Visual Coding Sst +0.087; Visual Behavior natural movie Sst −0.056). This term is nearly collinear with class, so we report it only as a sensitivity result.
- The Ai148-only comparison (Sst −0.081, Vip −0.216) uses only deep-layer excitatory lines (Fezf2, Ntsr1, Tlx3; at most 14 fields) as reference. It is not a good match for depth.
- The within-session halves comparison is not a null placebo. Sst cells also changed less within a session (+0.069, +0.044 to +0.094).
- The Pvalb result has one Cre line, one reporter (Ai162, GCaMP6s), two areas and 9 mice. The indicator checks are indirect, and the GCaMP6s Slc17a7 sample is small (1 field in Visual Coding, 3 in Visual Behavior).
- S is a ratio and needs reliable cells; reliability selection keeps different fractions of each class. Reliability-decile models and three thresholds gave the same pattern, except the Pvalb field-level contrast at R ≥ 0.5 (+0.025, not significant).
- ROI matching across days is from the Allen pipeline; errors in matching decrease S. Dense excitatory fields can have more matching errors; this effect would make interneurons look more stable, not less.
- Sessions were 0.3–28 days apart (median 2.2 days). This is a short time window.
- Not all excitatory containers were analysed (see data cutoff).

## Deviations from the plan

- The Visual Behavior dataset was added after the plan as a replication; its familiar-image metric is new.
- The rate-change outcome, the matched-cell-count, Ai148-only and indicator checks, the τ smoothing and the 0.5 s bin sensitivity were added during the analysis.
- The data cutoff above.

## Reproduce

Python 3.12 with numpy, pandas, h5py, scipy, statsmodels, matplotlib, pyarrow. Set `OMP_NUM_THREADS=1` on a loaded host.

```bash
# metadata
curl -O https://allen-brain-observatory.s3.amazonaws.com/visual-coding-2p/experiment_containers.json
curl -O https://visual-behavior-ophys-data.s3.amazonaws.com/visual-behavior-ophys/project_metadata/ophys_experiment_table.csv
python code/00_meta.py experiment_containers.json experiments.csv
# range-read extraction (one npz per experiment; ~30-60 MB read per NWB)
python code/01_extract.py ext/ <ophys_experiment_id> ...         # ids: data/experiments.csv (eid)
python code/01b_extract_vbo.py vbo/ <ophys_experiment_id> ...    # ids: data/vbo_experiments.csv
# per-cell tables (data/vc_cells.parquet, data/vbo_cells.parquet are the outputs)
python code/02_cells.py ext/ experiments.csv vc_cells.parquet [BIN_FRAMES=30] [TAU_S=0]
python code/02b_cells_vbo.py vbo/ vbo_experiments.csv vbo_cells.parquet
# statistics and figures
python code/03_stats.py data/vc_cells.parquet stats_vc_R0.3 0.3
python code/03b_stats_vbo.py data/vbo_cells.parquet stats_vbo_R0.3 0.3
python code/04_figures.py stats_vc_R0.3 stats_vbo_R0.3 figures/
python code/05_examples.py ext/ experiments.csv data/vc_cells.parquet figures/fig0_examples.png
python code/06_provenance.py ext/ vbo/ <vc meta dir> <vbo meta dir> provenance/
```

Steps 03–04 run from the included per-cell tables without any download. To use the same subset, restrict extraction to the experiments listed in `files/data/provenance/source_nwb_*.csv`.

## References

- de Vries SEJ et al. (2020) A large-scale standardized physiological survey reveals functional organization of the mouse visual cortex. Nat Neurosci. doi:10.1038/s41593-019-0550-9
- Deitch D, Rubin A, Ziv Y (2021) Representational drift in the mouse visual cortex. Curr Biol. doi:10.1016/j.cub.2021.07.062
- Marks TD, Goard MJ (2021) Stimulus-dependent representational drift in primary visual cortex. Nat Commun. doi:10.1038/s41467-021-25436-3
- Sadeh S, Clopath C (2022) Contribution of behavioural variability to representational drift. eLife. doi:10.7554/eLife.77907
- Hofer SB et al. (2011) Differential connectivity and response dynamics of excitatory and inhibitory neurons in visual cortex. Nat Neurosci. doi:10.1038/nn.2876
- Okun M et al. (2015) Diverse coupling of neurons to populations in sensory cortex. Nature. doi:10.1038/nature14273
- Harris JA et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature. doi:10.1038/s41586-019-1716-z
- Siegle JH et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature. doi:10.1038/s41586-020-03171-x
