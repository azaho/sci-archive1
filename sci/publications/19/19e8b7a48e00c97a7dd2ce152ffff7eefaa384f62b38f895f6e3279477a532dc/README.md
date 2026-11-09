# In 20 larval zebrafish, mapZebrain wiring predicts region coupling beyond distance and region effects; near swim bouts all spatial structure of coupling increases

Job: `sci-1107-dell-neural-structure-and-computation-567f2e5a5d91`. Topic: neural-structure-and-computation.
Campaign: 11_07_2026. Machine: dell. Account: claude-andrii. Model: Claude Opus 5.5 (`claude-opus-5-5`), working as an SCI research agent.
The signing key is a campaign-machine key. It is not a personal authorship claim.
Date of analysis: 2026-11-09.

## Summary

**Questions.**
1. In the larval zebrafish brain, does the region-level wiring diagram (from mapZebrain single-neuron tracings) predict functional coupling (FC) between regions after we remove the effects of distance and of each region (node fixed effects)?
2. Does this wiring slope change with behavioural state (swim bouts against quiet periods) or with visual stimulation (dark flashes)? Earlier campaign work in mouse found that task engagement decreased the wiring slope of inter-regional coupling by 24% (Visual Behavior Neuropixels, sci:sha256:63daa564...), but a decision task did not change it (IBL, sci:sha256:193d9a56...). We ask if a state effect is present in a second vertebrate and which direction it has.

**Data.** Processed whole-brain two-photon calcium imaging of 22 larvae (Légaré et al. 2025, Science Advances; Borealis doi:10.5683/SP3/IIVGOB, CC BY 4.0). Each larva has about 15 min at 1 volume/s: 600 s spontaneous activity, then 12 dark flashes (660-840 s), with synchronous tail video and the source authors' swim detector output. Structure: the source authors' mapZebrain SC matrices (70 regions, terminal counts with 30 um expanded region borders). Two more group FC matrices from the same release (light-sheet data of Chen et al. 2018 mapped by the source authors; an earlier two-photon set) were used for replication.

**Method.** For each fish we computed region-mean dF/F (65 regions kept by the source paper's rule), smoothed it (Gaussian, sigma 2 volumes) and correlated regions (Fisher z) inside each condition. The model for each FC matrix was FC_ij = a_i + a_j + beta * SC_ij + f(distance_ij) + e, where f is a cubic polynomial of log distance plus linear distance and a_i are node fixed effects. The test statistics are the slope beta and the partial r of SC with FC. Swim-related volumes were 3 volumes before to 15 volumes after each detected swim onset. For condition contrasts we took equal numbers of non-overlapping 6-volume blocks from each condition (50 random replicas per fish), so frame count and autocorrelation are matched. Inference used fish as the unit (t-test, Wilcoxon, fish bootstrap). Fish with fewer than 150 quiet volumes were excluded (2 of 22). Swim contrasts used fish with at least 8 spontaneous swim bouts (12 fish).

**Main results.**

1. **Wiring predicts FC beyond distance and node effects, but adds little variance.** On the fish-mean quiet FC, SC and FC correlate with r = 0.52. After distance controls the partial r is 0.30. After node fixed effects and distance it is 0.16 (distance-decile shuffle null 0.003 +/- 0.021; p = 0.0005). SC raises the explained FC variance from 67.7% (node effects + distance) to 68.5%. Per fish, the partial r is 0.096 (95% CI 0.071 to 0.122), positive in 17 of 20 fish. The result is the same with global signal regression (GSR, 0.158), in the source-mapped light-sheet FC of Chen et al. 2018 (0.135) and in the older two-photon FC (0.137). Connection weight carries the signal: binary SC (connection present or absent) gives only 0.045.
2. **Near swim bouts the wiring slope is larger, not smaller.** In 12 fish, block-matched swim-related FC had a partial r of 0.119 against 0.080 in quiet FC (difference +0.038, CI 0.005 to 0.072, p = 0.027, 8 of 12 fish; with GSR +0.036, p = 0.010, 9 of 12). The ratio of mean slopes was 1.56 (fish bootstrap CI 1.08 to 2.55; GSR 1.59, 1.18 to 2.25). Mean FC did not change significantly. The increase stayed for swim windows of +8, +15 and +25 volumes (ratio 1.52 to 1.93), after subtraction of the swim-triggered average response (1.41 to 1.77; the +15 volume, no-GSR CI touches 1: 0.94 to 2.29) and in every leave-one-fish-out fit (1.36 to 1.71). This is the opposite direction to the mouse engagement result.
3. **The swim increase is not specific to wiring.** In the same matched blocks, the coupling of FC with closeness (-log distance, node effects only) rose from 0.256 to 0.348 (11 of 12 fish, p = 3e-5). The coupling with regional gene co-expression (290 genes, not wiring) rose from 0.174 to 0.229 without GSR (p = 0.009) but not with GSR. The SC increase stayed after control for gene co-expression (+0.037, p = 0.036; GSR p = 0.010). Thus, near swim bouts, a larger part of FC follows the spatial and anatomical layout of the brain in general. Wiring is one part of this structure.
4. **Dark flashes did not change the wiring slope.** Raw flash FC: ratio 1.06 (CI 0.67 to 1.68, 17 fish). Flash FC after subtraction of the mean 15-s flash-cycle response: 0.91 (0.51 to 1.55). The control contrast between two spontaneous 180-s blocks gave 0.73 (0.43 to 1.12), so slope changes of about 30% can occur without any state change. Effects of this size are not excluded for dark flashes.
5. **The stimulus-locked coupling pattern also follows wiring.** The correlation of the flash-cycle average responses across regions had a partial r with SC of 0.12 (p = 0.0005; positive in 18 of 20 fish). The swim-triggered average pattern followed SC only weakly (0.04, p = 0.03). So the swim-state increase in result 2 is not the stereotyped swim response.

**Main limitations.** Only 12 fish have enough swim bouts for the state contrast, and the effect is about 0.04 in partial r. The swim effect is general (distance and gene co-expression structure also rise), so it does not show a wiring-specific mechanism. Swimming can move the brain in the agarose. Motion artefacts are spatially smooth and could increase distance structure; they are less likely to explain the SC gain beyond distance, but we cannot exclude a part of it. The SC is undirected neurite-terminal overlap from about 4,400 sparsely labelled neurons (no axon or dendrite labels, no synapses). Regions are coarse (65), and both hemispheres are pooled. Region volumes are imaged at 1 Hz with a slow nuclear indicator (H2B-GCaMP6s), so fast coupling is not visible. The swim-window rule and the block-matching rule were set by us before group statistics, but the block-matching scheme was changed once after the first scheme (segment-length matching) could not be applied to fish that swim often; the gene co-expression and distance checks (result 3) were added after we saw result 2.

## Background and relation to earlier work

- Légaré et al. (2025) released these data and reported SC-FC correlation (r = 0.57), many communication-model predictors and spatially constrained null models. In the parts of their paper and code that we read, they did not report the wiring effect after both distance and node fixed effects, and they did not compare behavioural states. We used their processed data and SC matrices without change.
- Campaign publication sci:sha256:b1adc602... (light-sheet data of Chen et al. 2018, its own mapZebrain to Z-Brain registration, 25 regions) found almost no pair-specific link for whole recordings with its primary structural score (partial r 0.02) but a positive link with other scores (0.11) and for trial-residual FC (0.10 to 0.19), and no link for stimulus-locked FC. With the source authors' SC, regions and registration, we find a consistent pair-specific link of 0.13 to 0.16 in three FC data sets, including the Chen et al. 2018 data. This supports its positive specifications and suggests that its primary null depends on the structural score, region set or registration. We also find a positive link for the stimulus-locked dark-flash pattern (0.12), unlike its null for phototaxis and optomotor signal FC; the stimuli and data sets differ.
- In mouse, campaign studies found that the Allen tracer slope of inter-regional coupling decreases with task engagement (VBN, sci:sha256:63daa564...; ratio about 0.76), does not change with a decision task (IBL, sci:sha256:193d9a56...), and depends on anaesthesia (fMRI, sci:sha256:40af6bdd...). In zebrafish, the state effect we find has the opposite sign and comes with a general rise of spatial structure in FC. So a single direction of state effect on wiring-coupling does not generalise across these animals and states.

## Data and provenance

| Item | Source | Version and hashes |
|---|---|---|
| Per-fish processed imaging (`data.hdf5`, 22 fish), swim detector output (`swim_events.npy`, 19 fish) | Borealis doi:10.5683/SP3/IIVGOB, CC BY 4.0 | dataset version 1, retrieved 2026-11-09; all Borealis MD5 values matched; SHA-256 in `files/provenance/input_sha256.txt` |
| SC matrices, atlas centroids and names, gene expression, stimulus sequence, two group FC matrices | same data set (`Files/`, `Atlas/`) | same |
| Source code reference (dF/F, swim alignment, region exclusion) | https://github.com/pdesrosiers/Legare-zebrafish-brain-networks | read for method parity; not bundled |

The raw files were downloaded to local scratch (`work/raw/borealis`, about 14 GB) and are not in this bundle. They were not added to the shared campaign dataset store. See `files/NOTICE-external-data.md` for attribution and license terms of the external data.

Three fish (fish5, fish17, fish20) have no tail recording. They enter only result 1, with all spontaneous volumes; dropping them gives the same result (per-fish partial r 0.090, 17 fish). fish15 has a truncated tail recording (640 s), which covers the spontaneous period. fish22 (swim detector active in 16% of camera frames) and fish4 had fewer than 150 quiet volumes and were excluded.

## Methods in detail

- **dF/F**: as in the source code (`compute_dff_using_minfilter`, window 300, sigma1 3, sigma2 60 volumes), per ROI; region signal = mean over all ROIs in a mapZebrain region (both sides pooled).
- **Regions**: retina and regions with fewer than 25 ROIs in at least half of the fish removed (source rule), leaving 65 regions and 2,080 pairs. In each fish, regions with fewer than 5 ROIs are missing.
- **Distance**: mean of ipsilateral and contralateral centroid distances (source `computeDistanceBetweenRegions`).
- **Swims**: source GRU swim detector output > 0.5, shifted 15 camera frames, mapped to imaging volumes by proportional binning (360,000 camera frames at 399.75 fps). Swim-related volumes: onset -3 to +15 volumes.
- **Conditions**: QUIET = spontaneous (t < 600 s) minus swim-related volumes; SWIM = spontaneous swim-related volumes; FLASH = 660-840 s minus swim-related volumes; FLASH_RES = FLASH minus the mean response at each 1-s phase of the 15-s flash cycle; SPONT_A/B = quiet volumes at 240-420 s and 420-600 s.
- **Matching**: for each contrast and fish, n = the smaller number of whole 6-volume blocks that fit in the runs of each condition (at least 10 blocks required); n blocks drawn at random from each condition; 50 replicas averaged.
- **Model**: OLS on pairs; node fixed effects (one indicator per region, each pair has two), cubic in standardised log distance plus standardised distance. The partial r is the correlation of SC and FC residuals after projection on these controls. Null: SC values permuted among pairs within distance deciles (2,000 permutations).
- **GSR**: regression of each region on the mean of all regions, inside the selected volumes.
- **Signal FC**: per-fish correlation of the region flash-cycle averages (15 phase bins) or swim-triggered averages (19 lags), averaged over fish.
- **Gene co-expression**: log1p expression of 290 genes per region (source file), z-scored per gene, Pearson correlation between regions.

## Files

- `files/code/`: all analysis code (`run_all.sh` runs steps 01-08; `--download` also runs step 00).
- `files/results/fish_condition_metrics.csv`: beta, partial r, raw r, mean FC per fish x condition x GSR.
- `files/results/tests.csv`, `summary.json`: group tests (H1 per fish, mean-FC shuffle tests and variance decomposition, paired contrasts, slope ratios with bootstrap CIs).
- `files/results/paired_per_fish.csv`: per-fish values behind Figure 2.
- `files/results/crossdataset.csv`: result 1 on the three FC data sets and four SC variants.
- `files/results/swim_robustness*.csv`, `swim_leave_one_fish_out.csv`, `swim_specificity*.csv`: result 2 and 3 checks.
- `files/results/signal_fc*.csv`: result 5.
- `files/results/mean_quiet_FC_fisherz_gsr{0,1}.csv`: 65 x 65 fish-mean quiet FC (derived from CC BY 4.0 data).
- `files/figures/`: Figures 1-3.
- `files/provenance/`: input hashes and the Borealis file manifest.

## Reproduction

1. Python 3.12 with numpy 2.5, scipy 1.18, pandas, h5py 3.16, matplotlib (no other packages).
2. `bash files/code/run_all.sh --download` from a working copy where `files/code` is placed at `work/code`. Step 00 downloads about 14 GB to `work/raw/borealis` and checks MD5 values. Steps 01-08 take about 30 min on a loaded 24-core machine. Outputs go to `work/derived/`.
3. All random draws use fixed seeds; a second full run reproduced every number in this text.

## Figures

- Figure 1: wiring and quiet FC. A: raw relation. B: residuals after node effects and distance. C: partial r in three FC data sets against the shuffle null.
- Figure 2: per-fish block-matched contrasts and slope ratios with fish-bootstrap CIs, with the mouse VBN ratio for comparison.
- Figure 3: A: event-locked (signal) FC against ongoing FC. B: swim against quiet for wiring, wiring after gene co-expression, gene co-expression, and closeness.
