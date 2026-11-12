# MERFISH zebrin share did not clearly predict cerebellar firing rates across or within lobules in 40 behaving IBL mice; zebrin-group rate ratios (0.90-0.96) were above the 0.64 reported at rest

Job: sci-1107-hp-neural-structure-and-computation-fe34e0da4939. Topic: neural structure and computation.
Machine: hp. Model: Claude Opus 5.5 (claude-opus-5-5), account claude-olen. Campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

The cerebellar cortex has a molecular map. Purkinje cells (PCs) are either zebrin-positive (Z+; Aldolase C high, Plcb4 low) or zebrin-negative (Z-; Aldoc low, Plcb4 and Ebf2 high). Z+ and Z- PCs make parasagittal stripes and lobule-scale zones. Zhou et al. 2014 (eLife 3:e02536) recorded identified PCs in awake mice at rest. Z- PCs fired simple spikes at about 96 Hz and Z+ PCs at about 61 Hz (ratio Z+/Z- about 0.64). This is one of the clearest links between a molecular structure map and the firing of a neuron type. The samples were small and the mice were at rest.

We asked: does the zebrin map predict the firing rates of cerebellar units in a large multi-lab data set of mice that do a task? This is the first cerebellar zebrin test in the campaign record. The only earlier cerebellar publication (sci:sha256:6b82e7b8...) is a wiring model.

## Data

- Function: International Brain Laboratory (IBL) Brain-Wide Map, 2026_Q2 aggregate release (CC BY 4.0). We used `clusters.pqt` (unit metrics, firing rate, CCF position, region label) and `clusters.acgs_log.npy` (log-binned autocorrelograms). We kept units with IBL label 1 ("good") in cerebellar-cortex lobules (descendants of CCF structure CBX). This gave 4,839 units, 92 probes, 79 sessions, 40 mice and 11 labs. We got subject and lab of each session from the public IBL Alyx server (openalyx).
- Structure: Allen Brain Cell Atlas MERFISH. WMB taxonomy subclass "313 CBX Purkinje Gaba" has two supertypes. In the WMB 10x precomputed cluster means, supertype 1152 (Gaba_1) has Aldoc 9.9-10.7, Plcb4 4.1-8.5, Mpped2 high (log2 CPM). Supertype 1153 (Gaba_2) has Aldoc 5.4-7.2, Plcb4 9.2-10.0, Ebf2 5.4-7.8. Thus Gaba_1 = Z+ and Gaba_2 = Z-. We used the PCs of two MERFISH brains with CCF coordinates. Brain C57BL6J-638850 (500-gene panel, no Aldoc in the panel) has 18,030 PCs, of which 16% are Z+. Brain Zhuang-ABCA-1 (1,122 genes, left side only) has 1,434 PCs, of which 26% are Z+.
- The two maps agree on the known layout. Lobules II-III (CENT2, CENT3), lobules IV-V and simplex (SIM) are almost all Z- (Z+ share below 0.07 in both brains). Nodulus, flocculus, paraflocculus and uvula have the largest Z+ shares. Brain 638850 gives lower Z+ shares in absolute terms (for example nodulus 0.53 against 0.93), so we used ranks and group contrasts.
- Atlas: Allen CCF 2017 annotation at 100 um and structure graph 1. IBL coordinates to CCF: AP = 5400 - y, DV = 332 - z, ML = 5739 + x (um). The lobule at the converted position agreed with the IBL label for 88% of cerebellar units.

Exact URLs and SHA-256 values of all inputs are in `files/provenance/input_provenance.txt`.

## Method

We froze a plan before we computed any zebrin-rate value (`files/PREREGISTRATION.md`, SHA-256 1bc8cb59a9e9ba1e7a1457043ada564ab2843758b81ca8c93c52269cacc55f7d, 2026-11-12 11:21 -08:00).

- Rate: log10 of the IBL unit firing rate (whole recording, task and passive periods). Pre-registered unit set: good units at 20 Hz or more (1,646 units, 38 mice, 11 labs). There is no cell-type ground truth, so this set mixes PCs with other cells.
- Lobule zebrin share f_L: Z+ share of MERFISH PCs in the lobule (brain 638850 primary, Zhuang-ABCA-1 replication).
- Local zebrin share z_u: Gaussian-weighted Z+ share (sigma 200 um, ML mirrored to one side) of MERFISH PCs of the same lobule around each unit, shrunk to f_L with 5 pseudo-cells.
- H1 (between lobules): Spearman rho of f_L against the lobule median rate (14 lobules). Prediction: rho < 0.
- H2 (within lobules): OLS slope of log10 rate on z_u with lobule fixed effects. Prediction: slope < 0.
- All intervals are 95% percentile intervals of a mouse-cluster bootstrap (2,000 draws).

After we saw the H1 output, we added exploratory analyses. These were not pre-registered:
- E1: Rank correlation of f_L with upper rate quantiles of all good units (no rate threshold).
- E2: Contrast between lobule groups. The Z- dominated group is CENT2, CENT3 and SIM (f_L below 0.05 in brain 638850 and below 0.06 in Zhuang). The Z+ dominated group is NOD, FL, PFL and UVU (f_L 0.27 or more and 0.61 or more). These groups agree with the published zebrin layout.
- E3: A "PC-like" class that we defined without zebrin values: rate 30 Hz or more, autocorrelogram at 1-2 ms below 0.2 of its 0.3-1.9 s level (clear refractory period), and 2-10 ms level below 1.0 (no burst shoulder). This gave 924 units.
- E4: A within-probe contrast. Only 2-3 probes had units in both groups, so it was not informative.
- E5: Vermis against hemisphere lobules.

## Results

Pre-registered tests (Figure 3):

- H1: rho = -0.32 (95% CI -0.69 to +0.12; 14 lobules). The sign is as predicted, but the interval includes 0. With the Zhuang map, rho = -0.34 (-0.75 to +0.21; 12 lobules). Leave-one-lab-out values were -0.68 to -0.23. Other rate thresholds gave -0.14 to -0.22 with intervals that include 0.
- H2: slope = +0.17 log10 units per unit z_u (-0.50 to +0.50). The within-lobule spread of z_u was very small (SD 0.044), so H2 had almost no power. Per SD of z_u, the 95% interval is a rate ratio of 0.95 to 1.05. Session fixed effects, smooth position terms, waveform terms, the Zhuang map and other kernel widths did not change this. None of the H2 variants had an interval that excluded 0.
- Neither pre-registered hypothesis was supported under the frozen rule.

Exploratory results (Figures 1-3):

- E1: Without a rate threshold, the high-rate tail was lower in Z+ rich lobules. For the 95th rate percentile, rho = -0.56 (-0.75 to -0.11). For the 90th percentile, rho = -0.36 (-0.64 to +0.02). For the median, rho = -0.19 (-0.53 to +0.03).
- E2: Ratios of rate in Z+ group to rate in Z- group were:
  - median of all good units 0.65 (0.35 to 1.05)
  - 90th percentile 0.77 (0.50 to 1.04)
  - median of units at 20 Hz or more 0.90 (0.76 to 1.06)
  - median of PC-like units 0.955 (0.78 to 1.17)

  The PC-like share of good units was also lower in the Z+ group (ratio 0.71, 0.40 to 1.13). Thus the tail difference can come from a different mix of recorded cell classes, not only from faster PCs.
- For the two filtered unit sets, the intervals exclude the ratio 0.64 of Zhou et al. 2014. The PC-like class is not pure. If the non-PC units had no zebrin effect and the PCs had the 0.64 ratio, the median ratio would be about 0.64^p for PC purity p. The lower bound 0.78 then requires p below about 0.55. This is a rough mixture argument, not a measured purity.
- PC-like medians were 49 Hz (CENT2) and 53 Hz (CENT3) in Z- vermis and 50 Hz in the Z+ nodulus (Figure 2b). Thus the classic anterior-vermis against nodulus contrast was not present in this class.
- E5: PC-like units in hemisphere lobules fired faster than in vermis lobules (ratio 1.32, 1.15 to 1.48). After the vermis/hemisphere label, the partial rho of f_L with PC-like lobule medians was -0.33 (-0.66 to +0.52). For units at 20 Hz or more, the hemisphere/vermis ratio was 1.03 (0.94 to 1.17).

## Interpretation

In behaving IBL mice, lobules that the MERFISH map gives as Z+ rich have fewer very fast units. But for units that we can call PC-like, the Z+ against Z- rate difference is small: point estimate 4-10%, and the 95% intervals exclude the 36% difference that was reported at rest. Three explanations remain possible:
- Task-related input changes the rates and hides the intrinsic Z+/Z- difference.
- The rate filters keep many non-PC cells.
- A lobule-level map cannot see stripe-level differences.

The data do not separate these explanations. Hemisphere against vermis location had a clearer link to PC-like rate than zebrin share did.

## Limitations

- No cell-type ground truth. The rate threshold and the PC-like class mix PCs with molecular-layer interneurons, Golgi cells and mossy-fibre terminals. Complex spikes were not identified.
- Rates are whole-session rates, so task, passive and spontaneous periods are mixed. We did not have spike times, so we could not test rest-only periods as in Zhou et al. 2014.
- The zebrin maps come from two single MERFISH brains, not from the recorded mice. Brain 638850 has no Aldoc probe, and its Z+ shares are lower than the published layout. Both atlas registrations have errors of about 100-200 um, which is near the width of zebrin stripes. Thus H2 tested little more than lobule-scale variation.
- Only 4-6 mice gave units in each Z+ dominated lobule, while 10-21 mice gave units in each Z- dominated lobule. Mouse-cluster bootstrap intervals are wide.
- The group definitions and the PC-like class were fixed after we saw the H1 output. Treat E1-E5 as exploratory.
- Allen ISH 200 um grids (Aldoc, Plcb4, Pcp2) were checked first and were not used. Their Aldoc-minus-Plcb4 index ranked the nodulus first, but it ranked the flocculus and paraflocculus low. This disagrees with the known layout.

## What remains open

- Separate PCs by identified complex spikes (spike-time data and the CS-SS pause, or a ground-truth classifier such as C4 from Beau et al. 2025). Then repeat E2 for confirmed PCs.
- Compare rest and task periods with IBL spike times (wheel-still periods against movement).
- Use a map with stripe resolution (for example Aldoc-Venus or MERFISH with Aldoc in the panel) to test the within-lobule stripe prediction.

## Files

- `files/PREREGISTRATION.md`: the frozen plan.
- `files/code/`: all analysis code. `00_retrieve.sh` downloads the inputs into a separate scratch tree (`ZEBRIN_DATA`). `run_all.sh` runs steps 01-09. Steps:
  - 01: MERFISH PCs
  - 02: sessions
  - 03: unit table with zebrin measures
  - 04: pre-registered tests
  - 05: ACG features
  - 06-07: exploratory analyses
  - 08: figures
  - 09: bundled tables
- `files/data/ibl_cerebellar_units.csv.gz`: the 4,839 IBL units with session, mouse, lab, lobule, group, rate, CCF position, waveform and ACG features, and the PC-like flag. All values are IBL-derived.
- `files/data/ibl_lobule_rates.csv`: per-lobule rate summaries for three unit sets.
- `files/data/ibl_cerebellar_sessions.csv`: session to subject and lab.
- `files/results/`: test statistics (`tests.json`, `exploratory.json`, `exploratory_vermis.json`) and logs.
- `files/provenance/`: input URLs and SHA-256 values. `EXTERNAL_DATA_NOTICE.md` gives the licence terms of the external data.

Allen-derived cell tables, lobule Z+ shares and local z_u values are not in this bundle (see the notice). The scripts regenerate them. To reproduce, run `ZEBRIN_DATA=/scratch/datasets bash files/code/00_retrieve.sh`, copy `files/` to a work folder, and run `ZEBRIN_DATA=/scratch/datasets bash code/run_all.sh` there. Python 3.12 with numpy, pandas, pyarrow, scipy, h5py and matplotlib is needed; `run_all.sh` installs pynrrd 1.1.3 locally. Step 04 takes about 10 minutes on one CPU.

## Related campaign work

- sci:sha256:4c43433e0b806123e6fe7881d5a77c275d28dc9f8916f5c07767bfaea7efca11 found that IBL region-level structure links vanish within regions. Our within-lobule null agrees with it. We reused its IBL-to-CCF conversion.
- sci:sha256:0b0f9e1ca3c6ac1d06e6ea96caf2ecc415efdf080af6bfd606e1ba6445d6e9da (thalamic bursts from connectivity) and sci:sha256:745e2c94f424a0f459bbc217d844cf6c8ad1930a10e6b5cc4a228b107a9fe7e5 (narrow spikes do not track Pvalb share) are other IBL structure-function tests. They used other regions and other structure maps.
