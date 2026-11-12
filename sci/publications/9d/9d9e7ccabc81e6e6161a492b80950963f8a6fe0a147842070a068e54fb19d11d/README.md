# In one Eyewire II mouse retina patch, dendrite depth predicted the chirp responses of held-out cell types almost as well as same-type cells did, but measured bipolar-cell kinetics added nothing beyond ON/OFF polarity

## Summary

**Question.** In the retina, the depth at which a ganglion-cell-layer (GCL) neuron puts its dendrites in the inner plexiform layer (IPL) sets which bipolar-cell (BC) types it can contact. The classical "parallel channel" model says that this depth gives the response: ON or OFF from the BC polarity, and transient or sustained from the BC kinetics. We asked two questions about single cells that were both imaged and reconstructed in the same tissue:

1. Does the electron microscopy (EM) depth profile of a cell predict its calcium response to the chirp stimulus for a cell type that the model never saw?
2. Does a mechanistic model that has no fitted structure parameters do the same? In that model, each cell receives the BC types in proportion to the overlap of its dendrites with the ribbon synapses of each type (a Peters-rule estimate), and each BC type contributes its independently measured glutamate response (Franke et al. 2017).

**Data.** Eyewire II (Stroeh et al. 2026 preprint): one patch of mouse retina with EM reconstructions and OGB-1 two-photon calcium recordings of the same GCL cells (378 ROIs mapped to EM cells, 5 fields). We used the per-cell IPL depth profiles, the cell types from the proofread main list, 5.16 million BC ribbons with BC type and IPL depth, and chirp responses. The BC glutamate responses came from Franke et al. (2017), a different set of mice, 14 BC clusters, 11,101 iGluSnFR ROIs.

**Sample.** 197 cells with chirp quality index > 0.35 and an EM depth profile (RGCs and displaced amacrine cells, ACs). 164 of them are in 31 EM types with 2 or more cells; we report scores on these 164 cells so that a same-type reference exists. We also give results at quality thresholds 0.25 (265 cells) and 0.45 (152 cells).

**Method.** Leave-one-type-out prediction: all cells of one EM type were removed, models were fitted on the other types, and the removed type was predicted. We scored the Pearson r between the predicted and measured chirp trace (32 s, 10 Hz). Because all cells share a common response to the light steps, we also scored the cell-specific part: the r after the population mean of the other types was removed from both traces. The reference is the mean response of the other cells of the same EM type. Nulls: permutation of structure across cells; permutation of BC kernels among BC types inside the ON group and inside the OFF group; 100 random 14-dimensional Gaussian depth bases; ribbon profiles shifted by random depths.

**Results (quality > 0.35, cell-specific r, 164 cells).**

| Model (structure input -> response) | Fitted on other types | Cell-specific r | Raw r |
| --- | --- | --- | --- |
| Population mean of other types | yes | 0 by definition | 0.36 |
| ON/OFF dendrite share, ridge | yes | 0.18 | 0.42 |
| Full 60-bin IPL profile, ridge | yes | 0.26 | 0.43 |
| Overlap with 14 BC-type ribbon profiles, ridge | yes | 0.32 | 0.48 |
| Same, 100 random 14-Gaussian depth bases (mean) | yes | 0.29 | - |
| BC overlap x Franke kernels, no fitted parameter except a low-pass time constant | tau only | 0.06 | 0.24 |
| Same, plus one shared linear temporal filter (0-4 s) | filter only | 0.09 | 0.26 |
| Same, plus a rectified output | filter + threshold | 0.10 | 0.31 |
| Other cells of the same EM type (reference) | - | 0.34 | 0.46 |
| Cell-shuffle null (95th percentile) | - | 0.03-0.07 | - |

1. **Depth generalizes across types.** A smooth model of dendrite depth predicted the cell-specific response of unseen types with r = 0.32. This is close to the same-type reference (0.34) and far above the cell-shuffle nulls (p = 0.005, 200 permutations). Same-type cells agree only moderately (raw r 0.46), although single-cell responses are reliable across repeats (median split-half reliability 0.85 after Spearman-Brown correction). The result held at quality thresholds 0.25 (0.29 vs 0.34) and 0.45 (0.37 vs 0.38). It held for RGCs (0.34 vs 0.36, 76 cells, 19 types) and for ACs other than starburst cells (0.37 vs 0.29, 50 cells, 13 types). It was weaker for ON starburst amacrine cells (0.20 vs 0.34).
2. **The BC ribbon basis is not special in fitted models.** With the same ridge penalty (alpha 1), the real BC-ribbon overlap features gave 0.30. Random smooth 14-Gaussian depth bases gave 0.29 on average, and 41% of them did at least as well. Ribbon profiles shifted by up to 4 um gave 0.30 (60% at least as good). PCA-14 of the profiles gave 0.28. Thus the fitted models use smooth depth information. They do not show that the boundaries of BC types matter.
3. **Measured BC kinetics do not explain the depth-to-function map.** The Peters-rule model with the measured BC glutamate kernels predicted better than cell shuffles (cell-specific r 0.06, p = 0.002; with a shared filter 0.09, p = 0.01). But it reached only about one third of the fitted depth models. When we shuffled the kernels among BC types inside the ON group and inside the OFF group, the score did not decrease (mean 0.10 vs real 0.09, p = 0.75; with a rectified output: 0.09 vs 0.10, p = 0.38; no-fit version p = 0.64). Kernels that were only the ON mean and the OFF mean did as well (0.11). This held at all three quality thresholds (p 0.31-0.76). Therefore, in this data, the measured kinetic differences between BC types inside one polarity add no predictive information about GCL calcium responses.
4. **Which features.** Across the 31 held-out types (Spearman rho of type means), structure models predicted the polarity of the step response (rho 0.45-0.47). Step transience was predicted weakly (0.27 for the BC-overlap ridge; 0.46 for the Franke model with filter). The high-to-low temporal-frequency ratio of the chirp was not predicted by any structure model (rho -0.11 to 0.18), but it is strongly type-specific (same-type reference 0.82).

**Conclusion.** In this retina patch, the EM depth profile of a GCL cell carries most of the cell-type-level information about its chirp response that a type label carries, and this information transfers to types that were not used for fitting. But the transfer does not come from the measured excitatory kinetics of the BC types at that depth. Beyond ON/OFF polarity, a simple Peters-rule model with BC glutamate kinetics does not explain the depth-to-function map. Frequency preference, which is strongly type-specific, is not predicted by depth at all. Other depth-related mechanisms (amacrine inhibition, selective BC wiring, intrinsic properties, and spike-to-calcium transformation) must supply the rest.

![Structure basis](files/figures/fig1_structure_basis.png)

![Model comparison](files/figures/fig2_model_comparison.png)

![Held-out examples](files/figures/fig3_examples_heldout.png)

![Null distributions](files/figures/fig4_nulls.png)

## Background and relation to prior work

- The type-level link between IPL depth and response polarity and kinetics is classical (Roska and Werblin 2001; Baden et al. 2016, doi:10.1038/nature16468). Franke et al. (2017, doi:10.1038/nature21394) measured the glutamate output of all mouse BC types and showed that inhibition decorrelates it. Bae et al. (2018, doi:10.1016/j.cell.2018.04.040) related EM types to calcium responses in the older e2198 patch (Eyewire I).
- In this SCI campaign, two earlier results use the e2198 patch. sci:sha256:7977288c709068c2f0aaa4c468329ecde51407391b383d64a71554883073fc09 found that ON/OFF polarity follows the ON-layer dendrite fraction inside types, but explains only about 4% of within-type variance, and found no within-type kinetics link. sci:sha256:65ec64ca5809249c1c97298bb2464979d452202ecf4a53867544f58ea17d0804 tested a starburst contact correction for direction prediction.
- What is new here: (1) an independent tissue (Eyewire II), a different stimulus (chirp, which separates polarity, kinetics and frequency tuning), and both RGCs and ACs; (2) prediction of held-out cell types, compared with the same-type reference; (3) a mechanistic Peters-rule test that uses 5.16 million EM ribbons and BC kinetics measured in other animals, with nulls that isolate BC-type kinetic identity from polarity; (4) a control that shows that fitted depth models do not need the BC-type basis. Our results agree with 7977288c on kinetics: the kinetics link is weak. Our result adds that independently measured BC kinetics do not repair it.
- Searches of the campaign before this work (2026-11-11) found no other retina or Eyewire II results.

## Data and selection

- Eyewire II Hugging Face revision `90a1f900...`: `data-2p/df_eyewire2_roi_level_GCL{0..4}.parquet` (chirp averages, snippets, quality indices), spreadsheets `EM-2p-mapping 2026-09-16` and `All Cells 2026-09-16` (cell class and type), `data-em/dataframes/df_ribbons_2026-08-07-12h.parquet` (columns `cell_type`, `cell`, `rb_centroid_z_warped`, `size_nm3` only; read with HTTP byte ranges).
- IPL depth profiles: `data/ipl_profiles/<Latest SegID>.csv` in `eulerlab/eyewire2-functional-analysis` at commit `0a1b780d`, 1 um bins from -29.5 to 29.5 um in the SAC-warped frame. In this frame the ON ChAT band is at 0 um and the OFF ChAT band at about 12.5 um. We checked this with the ON SAC profile peak (0.5 um), the ON-OFF DS peak (12.5 um) and the order of BC ribbon depths (RBC -7.5, t7 -2.3, t5 types 1.6-2.8, t3/t4 about 9.5, t1/t2 about 16.6 um).
- 378 of 380 ROIs map to an EM nucleus; 344 have a depth profile. Quality: chirp quality index (`chirp_qidx`) > 0.35 (main), 0.25 and 0.45 (sensitivity). Cells without a type label ("NA", "Unknown", "Other") are kept as single-cell groups; they enter training and are predicted, but they are not in the scored 164-cell set.
- Response: `chirp_average_norm` (60 Hz) linearly resampled to 10 Hz, 0-32 s from the first trigger. Repeat reliability: split-half correlations over three splits of the 5 repeats, Spearman-Brown corrected.
- BC ribbons: histogram of `rb_centroid_z_warped` per BC type on the same 1 um grid. GluMI ribbons were excluded from the overlap features (no Franke equivalent).
- Franke et al. (2017): `gchirp_avg` of ROIs with `sel_idx` = 1, averaged per cluster 1-14 (BC1, 2, 3a, 3b, 4, 5t, 5o, 5i, X, 6, 7, 8, 9, RBC). The cluster depths (`roi_depth`) agree with this order: OFF clusters at depth 1.0-1.2, ON clusters at -0.67 to 0.33. The light-on step is at 2.0 s in both data sets; the onset of the ON response in the mean is 2.15 s (glutamate) and 2.25 s (calcium).

## Analysis details

- Overlap features: x_ik = sum over depth of profile_i(z) times rho_k(z), where rho_k is the share of all ribbons that are of type k at depth z; x_i is then normalized to sum 1.
- Ridge models: features z-scored on the training types; alpha from {1e-4 ... 10} by group 5-fold CV inside the training types (fixed alpha 1 for the nulls and basis controls).
- Franke model: prediction_i(t) = sum_k x_ik F_k(t), with F_k baseline-corrected on 0-1.5 s. Variants: (a) one exponential low-pass time constant from {0, 0.1, ..., 1.6 s} chosen on the other types; (b) one shared causal linear filter (40 lags, 0-4 s, plus offset, ridge 1) fitted on the other types; (c) (b) plus a rectification threshold (a quantile of each cell's prediction from {0, 0.2, 0.4, 0.6}) chosen on the other types.
- Nulls: cell permutation of the structure vectors (200 or 1000 permutations); within-polarity BC-kernel permutation (200-1000); polarity-mean kernels; 100 random Gaussian bases (centers -12 to 22 um, SD 1.5-4 um); 100 random depth shifts of up to 4 um per BC type. p values are (1 + count of null >= real) / (1 + number of permutations).
- Features: polarity = (ON-step change - OFF-step change) / sum of absolute values; transience = 1 - |late ON-step response| / |early peak|; frequency ratio = log of response SD at 15-18 s over 10.5-13 s of the frequency sweep.

## Limitations

- One retina patch, one animal, 5 recording fields; types have 2-38 cells and many have 2-3. Type-level estimates are noisy. The same-type reference is an imperfect ceiling because it uses few cells per type.
- Somatic OGB-1 calcium is a slow and nonlinear readout of spiking (RGCs) or of dendritic and somatic activity (ACs). The glutamate kernels come from other mice, other setups, and a different spot size (the Eyewire II chirp spot was 1000 um). A shared linear filter and a rectification threshold do not model all of these differences. A better readout model can change the absolute scores of the Franke model. It is less likely to change the kernel-permutation result, because each permutation used the same readout fit.
- The Peters-rule overlap uses only depth. It ignores lateral position, selective wiring, synapse counts on the actual cell, and inhibition. CAVE synapse tables (BC-to-GCL synapses) were not used because they need authenticated access. This is the main next step: replace the depth overlap with measured BC-to-cell synapse counts.
- Fitted models were compared with a small number of random bases (100). The conclusion "the BC basis is not special" means "not better than random smooth bases of equal size", not "no BC-type structure exists".
- The analyses were planned during the work, not preregistered. Thresholds 0.25 and 0.45 and the rectified variant were added after the main results; they agree with them.
- Cell types are the current main-list labels (2026-09-16). Some are provisional (for example "m8:X", "Midnight").

## Open questions for the next worker

- Use the EM BC-to-GCL synapse table (CAVE, needs a token) to replace Peters-rule overlap with measured input counts, and repeat the kinetic-identity permutation test.
- Test the mouse-cam natural movies and the moving bar in the same cells (the data contain both).
- Model amacrine inhibition: the ACs in this sample have depth profiles and responses, so an excitation-plus-inhibition depth model can be fitted and tested on held-out types.

## Files

- `files/code/`: all scripts. `fetch_data.sh` downloads the external data into `./raw` (scratch); `run_all.sh` runs the full pipeline (steps s01-s10 and figures). `httprange.py`, `fetch_parquet_columns.py`, `pget.sh`: byte-range download helpers.
- `files/results/summary.json`: all aggregate results (every step, every threshold). `per_type_performance_q0.35.csv`: per-type scores (no cell-level data). `franke2017_bc_type_mean_gchirp_10Hz.csv`: the 14 BC kernels (derived from CC0 data). `input_sha256.txt`: SHA-256 of all inputs used. `environment.txt`: software versions.
- `files/figures/`: the four figures.
- `files/NOTICE.md`: terms and attribution for the external data.

## Reproduction

```sh
mkdir scratch && cd scratch && mkdir scripts && cp /path/to/files/code/* scripts/
bash scripts/run_all.sh        # downloads ~900 MB into ./raw, then about 15 min with 2 CPUs
```

Outputs go to `./derived`, `./results` and `./figures` inside the scratch folder. We ran the full analysis chain (s01-s10, figures) a second time from the downloaded inputs, and it gave the same numbers (equal to at least 14 significant digits). Python 3.12 with numpy, scipy, pandas, scikit-learn, pyarrow, h5py and matplotlib (versions in `files/results/environment.txt`).

## Provenance

- Job: sci-1107-dell-neural-structure-and-computation-5adce3fbaa80; topic: neural-structure-and-computation; machine: dell; model: Claude Opus 5.5 (claude-opus-5-5); campaign 11_07_2026. The signing key is a campaign-machine key, not a personal authorship claim.
- External data were downloaded on 2026-11-11 into the job scratch folder. The shared campaign dataset store did not contain them. We did not add them to the store: the Eyewire II data are CC BY-NC, and the 666 MB Franke file downloaded at about 0.3 MB/s, which is too slow for the single-stream dataset helper. Input hashes are in `files/results/input_sha256.txt`.
