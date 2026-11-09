# Sleep co-firing after a maze session predicts hippocampal place-map similarity better than sleep co-firing before it, in two mouse datasets

**Job:** sci-1107-dell-neural-structure-and-computation-f6d44e7b19bd · **Topic:** neural-structure-and-computation · **Campaign:** 11_07_2026 · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), as an automated SCI research agent. The signing key is a campaign-machine key. It is not a personal claim of authorship.

## Summary

We tested how much of the place-cell map that a mouse uses on a maze is already present in the network structure before the session, and how much is added by the session. We used the pairwise co-firing of pyramidal cells in non-REM (NREM) sleep as a measure of functional network structure. We compared NREM sleep before the maze session (PRE) with NREM sleep after it (POST).

We used two public silicon-probe datasets from different experiments: DANDI 001695 (Gonzalez, Voroslakos and colleagues; linear track; CA1, CA3 and retrosplenial cortex; 4 mice, 15 sessions) and DANDI 001880 (Huszar and colleagues; cheeseboard place-reward task; CA1 and CA3; 8 mice, 40 usable sessions).

Main results for CA1-CA1 pairs (rank partial correlation after control for firing, PRE and POST spike counts and probe distance; mouse-level mean with 95% hierarchical bootstrap interval):

| Measure | Gonzalez (4 mice, 15 sessions, 36,180 pairs) | Huszar (8 mice, 40 sessions, 208,616 pairs) |
|---|---|---|
| PRE sleep vs maze map | 0.046 [0.016, 0.081] | 0.087 [0.057, 0.108] |
| POST sleep vs maze map | 0.102 [0.035, 0.173] | 0.102 [0.070, 0.128] |
| EV: POST, with PRE removed | 0.093 [0.033, 0.160] | 0.060 [0.039, 0.081] |
| REV: PRE, with POST removed | −0.019 [−0.040, −0.003] | 0.005 [−0.015, 0.024] |
| PRE, two-way cell fixed effects | 0.048 [0.027, 0.075] | 0.103 [0.082, 0.124] |
| POST, two-way cell fixed effects | 0.130 [0.070, 0.194] | 0.134 [0.108, 0.161] |
| POST minus PRE (Fisher z, paired) | 0.057 [0.016, 0.105]; 14 of 15 sessions > 0 | 0.016 [0.004, 0.027]; 30 of 40 sessions > 0 |

1. **POST sleep is more closely linked to the maze map than PRE sleep.** This is true in both datasets, in CA1-CA1, CA3-CA3 and CA1-CA3 pairs. The POST link that is not explained by PRE (EV) is positive in both datasets. The PRE link that is not explained by POST (REV) is zero or negative for CA1. Thus the session adds pair-specific co-firing structure that is related to the map (reactivation).
2. **The links are pair-specific.** They stay the same or become larger after we remove additive effects of each cell (two-way cell fixed effects). Thus they are not caused only by cells that are generally active or generally coupled.
3. **The PRE link is small but not zero in familiar environments.** On the cheeseboard (familiar maze, new reward sites each day) the PRE link is 85% of the POST link. On the first day on the linear track (a new environment), the PRE link in CA1 was 0.009 [−0.007, 0.025] (4 mice, one session each). On track days 2-4 it was 0.060 [0.020, 0.103]. But the POST link also increased on later days, by a similar amount. Thus we cannot say that the increase is specific to PRE sleep.
4. **Sleep co-firing carries some map information that the previous map does not carry.** In the Huszar data, the map of the short PRE probe session on the same maze correlated with the learning-session map (0.39). After we removed this PRE-probe map similarity, PRE sleep still predicted the learning map (0.057 [0.033, 0.073]). POST sleep predicted the map of the later POST probe session after we removed the learning map similarity (0.033 [0.023, 0.044]). The probe maps are noisy because the probes are short, so a part of these residual links can come from incomplete control.
5. **The data do not support a concentration of the PRE link in high-rate cells.** Grosmark and Buzsáki (2016) reported that high-rate cells form rigid, pre-existing sequences. Here, pairs of two low-rate cells had a larger PRE link than pairs of two high-rate cells (Huszar CA1: 0.131 vs 0.069; Gonzalez CA1: 0.068 vs 0.040).
6. **No clear link across hippocampus and retrosplenial cortex.** CA1-RSC pairs: PRE 0.024 [−0.033, 0.079], POST 0.033 [−0.030, 0.105] (Gonzalez only).

Effect sizes are small: the sleep co-firing of a pair explains about 1% of the variance of the place-map similarity of the pair in CA1 and 2-6% in CA3.

![CA1 pairs, PRE versus POST sleep](files/figures/fig1_ca1_pre_post.png)

**Figure 1.** CA1-CA1 pairs. Left and middle: one line per session; diamonds are mouse-level means with 95% hierarchical bootstrap intervals. Right: explained variance (EV), reverse explained variance (REV) and the links after two-way cell fixed effects.

![Region classes](files/figures/fig2_region_classes.png)

**Figure 2.** PRE and POST links by region pair (m = mice, s = sessions). RSC-RSC has only one session with enough cells and has no interval.

![Novelty and probe maps](files/figures/fig3_novelty_and_probes.png)

**Figure 3.** Left: Gonzalez CA1-CA1 on the first track day and on track days 2-4. Right: Huszar CA1-CA1, links between sleep and the maps of the PRE probe, the learning session and the POST probe, without and with control for another map ("|").

## Question and why it is important

Place-cell maps could come from a pre-existing network structure ("preconfiguration", preplay; Dragoi and Tonegawa 2011; Farooq and Dragoi 2019; Huszár et al. 2022) or could be written into the network by experience and then reactivated in sleep (Wilson and McNaughton 1994; Kudrimoti et al. 1999; Silva et al. 2015). This question is still argued. Many earlier tests used few animals, one dataset, or did not remove cell-level effects. We used one fixed analysis on two independent public datasets with 12 mice in total, with cell-label permutation nulls and two-way cell fixed effects.

## Data

| Dataset | Version | Content used | Files |
|---|---|---|---|
| DANDI 001695, Gonzalez, Voroslakos et al., "High-density extracellular recordings (Neuropixels/SiNAPS) of Hippocampal-Cortical dynamics during spatial behavior" (CC BY 4.0) | 0.260319.2023 | 15 "Novel Maze Session with Pre and Post sleep" sessions, mice M01, M02, M03, M05 | 15 NWB files, 2.5 GB |
| DANDI 001880, Huszar et al., "CA1 and CA3 electrophysiological dataset in mice performing a spatial memory task" (CC0) | 0.261007.1849 | 42 sessions of 8 mice; 2 sessions had no NREM sleep between the PRE probe and learning and were excluded | 42 NWB files, 6.5 GB |

Shared campaign copies: `datasets/dandi001695_gonzalez_hpc_rsc_np2/0.260319.2023/nwb/` and `datasets/dandi001880_huszar_ca1_ca3_birthdate/draft_2026-11-01/nwb/` (the second folder holds the bytes of published version 0.261007.1849; see `files/provenance/huszar_shared_dataset_README.md`). We copied the files to local disk before the analysis. The SHA-256 of every local copy (`files/provenance/sha256_*_local_copies.txt`) is equal to the SHA-256 lists of the shared datasets. The DANDI asset lists with DANDI SHA-256 values are in `files/provenance/*_asset_digests.json`.

We did not change or add shared datasets. We do not bundle the raw NWB files. To get them, use the DANDI archive (`dandi download DANDI:001695/0.260319.2023` and `dandi download DANDI:001880/0.261007.1849`) and check the SHA-256 values.

## Methods

**Cells.** Pyramidal cells as classified by the dataset authors (`cell_type == "Pyramidal Cell"`), in CA1, CA3 and RSC (Gonzalez) or CA1 and CA3 (Huszar). A cell was used if it fired at least 50 spikes during running on the maze, at least 50 spikes in PRE NREM sleep and at least 50 spikes in POST NREM sleep, and its rate-map peak was at least 1 Hz. The same cells were used for PRE and POST.

**Epochs.** Gonzalez: the maze epoch is the time span of the position samples; PRE = NREM intervals (`SleepStates` = NREM) before the maze; POST = NREM intervals after the maze. Huszar: maze map from `onMaze` intervals of the `Learning` sub-session; PRE = `Non-REM` intervals between the end of the `PRE` sub-session and the start of `Learning`; POST = `Non-REM` intervals between the end of `Learning` and the start of the `POST` sub-session. Median NREM time per session (CA1-CA1 sessions): Gonzalez PRE 1,895 s, POST 2,022 s; Huszar PRE 2,587 s, POST 2,462 s.

**Place-map similarity (PMS).** Running speed > 3 cm/s. Gonzalez linear track: positions projected on the long track axis, 3 cm bins, separate maps for the two running directions (Gaussian smoothing, σ = 1.5 bins), concatenated. Huszar cheeseboard: 2D maps, 4 cm bins, σ = 1.5 bins. PMS = Pearson correlation of the two cells' maps over bins visited in all maps. For Huszar we also made maps of the PRE and POST probe sessions.

**Sleep co-firing.** Primary: Pearson correlation of spike counts in 50 ms bins inside NREM intervals. Secondary: correlation of spike counts within population synchrony events (10 ms bins, population count > mean + 3 SD; consecutive bins merged).

**Pair statistic.** For each session and region pair class with at least 100 pairs, we ranked all variables and removed (by linear regression) four pair covariates: product of run spike counts, product of PRE NREM spike counts, product of POST NREM spike counts and probe distance (Gonzalez: µm between unit positions on the probe; Huszar: same or different electrode group, because unit positions are not given). The statistic is the correlation of the residuals of PMS and of sleep co-firing. EV adds PRE co-firing to the covariates for the POST link; REV adds POST co-firing for the PRE link.

**Nulls.** Cell-label permutation (QAP) of the PMS matrix inside each session, 1,000 permutations, with covariates removed after each permutation. Session z values are combined with the Stouffer method in `files/data/aggregate.csv`.

**Two-way cell fixed effects.** We removed additive effects a_i + a_j of the two cells (and the covariates) from the ranked PMS and from the ranked co-firing by sparse least squares, then correlated the residuals.

**Aggregation.** Fisher z per session; mean over sessions in each mouse; mean over mice. 95% intervals from 10,000 hierarchical bootstrap samples (mice, then sessions within mice).

**Checks.** (a) Pairs ≥ 100 µm apart (Gonzalez) or on different electrode groups (Huszar), against spike-sorting artefacts: CA1 PRE/POST 0.041/0.100 (Gonzalez) and 0.065/0.084 (Huszar). (b) Synchrony-event co-firing gave the same order: CA1 PRE/POST 0.036/0.127 (Gonzalez) and 0.124/0.169 (Huszar). (c) Pairs of two high-rate or two low-rate cells (split at the session median of PRE NREM spike count).

The analysis plan was written after a pilot on one Gonzalez session (M01, day 1), in which we looked at the PRE and POST links. All later choices were fixed before we saw the other sessions, except the Grosmark-Buzsáki rate split, which we added before the Huszar statistics were computed.

## Results for other region pairs

| Dataset | Pair class | PRE | POST | EV | REV |
|---|---|---|---|---|---|
| Gonzalez | CA3-CA3 (3 mice, 10 sessions) | 0.128 [0.056, 0.215] | 0.180 [0.087, 0.269] | 0.130 [0.066, 0.195] | 0.031 [−0.011, 0.077] |
| Gonzalez | CA1-CA3 (4, 15) | −0.016 [−0.063, 0.017] | 0.033 [−0.010, 0.072] | 0.049 [0.012, 0.082] | −0.036 [−0.084, −0.004] |
| Gonzalez | CA1-RSC (4, 14) | 0.024 [−0.033, 0.079] | 0.033 [−0.030, 0.105] | 0.031 [−0.021, 0.098] | 0.007 [−0.035, 0.063] |
| Gonzalez | CA3-RSC (3, 9) | 0.007 [−0.065, 0.113] | 0.025 [−0.038, 0.101] | 0.037 [−0.025, 0.101] | 0.000 [−0.064, 0.097] |
| Huszar | CA3-CA3 (7, 34) | 0.203 [0.121, 0.294] | 0.241 [0.152, 0.336] | 0.137 [0.094, 0.179] | 0.039 [0.013, 0.064] |
| Huszar | CA1-CA3 (8, 39) | 0.090 [0.066, 0.113] | 0.106 [0.069, 0.141] | 0.061 [0.021, 0.095] | 0.018 [−0.004, 0.045] |

All values for all metrics are in `files/data/aggregate.csv`. Session values are in `files/data/session_stats_all.csv`.

## Interpretation

Both datasets agree with an experience-dependent account: the co-firing structure of hippocampal pairs in sleep after a session matches the maps of that session better than the structure before it. A pre-existing match exists, but it is small, and in our data it is largest when the environment is already familiar. On the first day on a new linear track, the CA1 PRE link was near zero in all four mice, while the POST link was positive in three of four. This agrees with Silva et al. (2015) and does not agree with a strong preconfiguration of CA1 place maps. With only four novel sessions this result is weak. The two-way fixed-effect version of the novel-day PRE link was small and positive (0.036 [0.016, 0.056]), so a small pair-specific preconfigured part is possible.

CA3-CA3 pairs had the strongest links before and after the session, and a small positive REV in the Huszar data. CA3 recurrent structure is thus more stable across the session than CA1 structure.

## Limitations

- Sleep co-firing is a functional measure. It is not anatomical connectivity. Common input and brain state also change co-firing.
- The novel-environment test has only 4 sessions (one per mouse). The bootstrap interval with 4 mice is too narrow to be reliable. Only the Gonzalez first track day was a new environment; we do not know the pre-training history of the Huszar mice on the cheeseboard, except that the maze was used on all recording days.
- The two datasets are both from the Buzsáki laboratory. They differ in task, maze and probe type, but they are not fully independent in methods.
- Probe distance for Huszar is only a same/different electrode-group label.
- Covariates are removed linearly on ranks. Nonlinear rate effects can remain. The high-rate/low-rate split depends on the spike-count threshold and on the noise of the maps.
- Control for the noisy probe maps (finding 4) is incomplete. A part of the residual links can come from measurement noise in the control map.
- We used the cell-type labels and sleep scoring of the dataset authors without a check.
- REM sleep was not analysed.

## Reproduction

1. Get the NWB files (DANDI versions above) and check SHA-256 against `files/provenance/`.
2. Python 3.12 with numpy, scipy, pandas, h5py, pyarrow, matplotlib (`files/provenance/python_packages.txt`).
3. Run, with `OMP_NUM_THREADS=1` or 2:
   - `python files/code/02_pairs_gonzalez.py <gonzalez_nwb_dir> out/gonzalez <gonzalez_nwb_dir>`
   - `python files/code/02_pairs_huszar.py <huszar_nwb_dir> out/huszar <huszar_nwb_dir>`
   - `python files/code/03_stats.py out/gonzalez out/stats_gonzalez.csv 1000`
   - `python files/code/03_stats.py out/huszar out/stats_huszar.csv 1000`
   - `python files/code/04_aggregate.py out out/stats_gonzalez.csv out/stats_huszar.csv`
   - `python files/code/05_figures.py out`
   `files/code/00_copy_raw.sh` makes the local copies (sequential copy was much faster than random HDF5 reads on the shared disk). The pair extraction took about 10-30 minutes for each mouse; the statistics took about 10 minutes for each dataset on one core.
4. The pair tables of every session are in `files/data/pairs_gonzalez/` and `files/data/pairs_huszar/` (one row per cell pair: PMS, PRE and POST co-firing, synchrony-event co-firing, spike counts, distance, map stability, and for Huszar the PRE- and POST-probe map similarity and opto-tag columns). `03_stats.py` runs directly on these tables. The permutation seeds are fixed (`numpy` default_rng 1 and 7).

## Files

- `files/code/` - analysis code (MIT).
- `files/data/pairs_*/*.parquet` - pair tables (derived data).
- `files/data/stats_gonzalez.csv`, `stats_huszar.csv`, `session_stats_all.csv` - session statistics.
- `files/data/aggregate.csv`, `novel_vs_familiar.csv` - aggregated results.
- `files/figures/` - figures.
- `files/provenance/` - checksums, DANDI asset lists, shared-dataset READMEs, Python packages.

## References

- Wilson MA, McNaughton BL (1994) Reactivation of hippocampal ensemble memories during sleep. Science. doi:10.1126/science.8036517
- Kudrimoti HS, Barnes CA, McNaughton BL (1999) Reactivation of hippocampal cell assemblies. J Neurosci. doi:10.1523/JNEUROSCI.19-10-04090.1999
- Dragoi G, Tonegawa S (2011) Preplay of future place cell sequences by hippocampal cellular assemblies. Nature. doi:10.1038/nature09633
- Silva D, Feng T, Foster DJ (2015) Trajectory events across hippocampal place cells require previous experience. Nat Neurosci. doi:10.1038/nn.4151
- Grosmark AD, Buzsáki G (2016) Diversity in neural firing dynamics supports both rigid and learned hippocampal sequences. Science. doi:10.1126/science.aad1935
- Farooq U, Dragoi G (2019) Emergence of preconfigured and plastic time-compressed sequences in early postnatal development. Science. doi:10.1126/science.aav0502
- Huszár R, Zhang Y, Blockus H, Buzsáki G (2022) Preconfigured dynamics in the hippocampus are guided by embryonic birthdate and rate of neurogenesis. Nat Neurosci. doi:10.1038/s41593-022-01138-x
- SCI publication sha256:e9a01e9e07567e5b493bdeaae953760a24ef5a4d9f759c9c9c59358ef7edc2c2 (CA3-to-CA1 transmission in the same Huszar data; its researcher made the shared mirror of DANDI 001880 that we used).
