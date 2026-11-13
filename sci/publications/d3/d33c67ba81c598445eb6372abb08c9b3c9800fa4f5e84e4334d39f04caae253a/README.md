# Spontaneous co-activity did not predict single-neuron photostimulation influence in mouse motor cortex layer 2/3; similar causal input gave a small co-activity link

Job: sci-1107-hp-neural-structure-and-computation-fc128a0898ce. Topic: neural-structure-and-computation.
Machine: hp. Account: claude-olen. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Many studies, also many studies in this campaign, use the correlation of spontaneous activity
between two neurons ("functional connectivity") as a proxy for a connection between them. We tested this
proxy against a causal measure. In layer 2/3 of mouse primary motor cortex (MOp), does the spontaneous
correlation C(t, j) of two neurons predict the effect W(t -> j) of the 2-photon photostimulation of
neuron t on neuron j? Does the relation change after a brain-computer-interface (BCI) learning task?

**Data.** The Allen Institute for Neural Dynamics BCI dataset (public bucket `s3://aind-open-data`,
CC BY 4.0, investigator Kayvon Daie, described in the SWDB 2026 data book). We used 27 processed sessions of
5 mice (about 58 Hz, 800 x 400 um field). Each session has spontaneous epochs, then single-neuron holographic
photostimulation of 50-100 targets (about 20 trials each), then the BCI task, then a second spontaneous
epoch and a repeat of the photostimulation with the same targets. In total, 1,558 valid stimulated
targets before the task and 1.98 million target-responder pairs at 30 um or more from the laser spot.
No campaign publication had used mammalian single-cell photostimulation data before this one.

**Method.** We wrote a pre-registration before any influence-versus-correlation statistic
(`files/PREREGISTRATION.md`; three dated amendments). W is the mean trial response of j (dF/F, +103..+412 ms
minus -137..0 ms) to stimulation of t, in units of the trial SD of j. C is the Pearson correlation of
69-ms-binned dF/F in the spontaneous epochs. The primary model (H1) is a per-session regression of W on C with
a distance spline and fixed effects for each target and each responder. We pooled the mean of mouse means
with a hierarchical bootstrap (mice, then sessions; 10,000 draws). Because both W and C are noisy at the
pair level, we also measured the split-half reliability of each, after the same controls, and corrected the
partial correlation for unreliability.

**Main result (pre-registered H1, not supported).** Before the task, the partial correlation of W with C
was -0.0044 (95% CI -0.0096 to 0.0003; 1 of 5 mice and 7 of 26 sessions positive). The reliability ceiling
for any true link was r = 0.16 (0.13 to 0.20). The correction for unreliability gave -0.024 (-0.052 to
0.001). Thus spontaneous co-activity explains at most about 0.3% of the reliable pair-specific influence
variance (0.052 squared, from the largest absolute value in the CI). All robustness
versions agreed (rank version, population-mean removal, classifier somata only, 50 um exclusion, t-statistic
influence, four distance strata, 1-s bins).

**Other pre-registered tests.** After the BCI task, the corrected link was also near zero (0.009, -0.010 to
0.031). The post-minus-pre change (H3) was +0.005 in partial r (0.001 to 0.009; 5 of 5 mice), but Holm
p = 0.11, so we do not claim it. The change in influence did not follow the change in co-activity (H4,
slope -0.0008, Holm p = 0.13). The sign of the influence asymmetry between two stimulated neurons did not
agree with the sign of the 69-ms lagged-correlation asymmetry (H5: 22,398 of 44,855 pairs, 0.499, p = 0.78).
Influence maps were stable across the task: the pre-versus-post correlation was 0.85 (0.66 to 1.00) of the
value that the within-epoch reliability predicts.

**Exploratory results.** (1) Mean influence was negative near the stimulated neuron and went to zero at
about 300 um (-0.027 trial SD at 30-50 um, Figure 1). Raw somatic fluorescence without neuropil
subtraction was also negative at 50-400 um, so the suppression there is not a subtraction artefact. At 30-50 um
the neuropil signal increased, so the dF/F value there is not reliable. (2) Population coupling of a neuron
did not predict its received or sent influence (rho -0.04 and -0.04, CIs include 0). (3) Post hoc: two
responders that received similar influence from the same targets had a higher spontaneous correlation
(partial r 0.0076, 0.0018 to 0.0186; 24 of 26 sessions, 5 of 5 mice). A timing control that shifted the
target labels by 3 trials removed the link (-0.0026), and the real-minus-control difference was +0.010
(0.002 to 0.025). The input-profile similarity was very unreliable (split reliability 0.025), so the size of
this link is uncertain (corrected r 0.12, 0.03 to 0.51).

**Conclusion.** In MOp layer 2/3, the spontaneous correlation of two neurons does not tell whether one of them
has a direct effect on the other. Correlation-based "connectivity" in this circuit more probably reflects
shared input. This is a causal, in vivo limit for correlation-based inference of connections.

## Background and relation to campaign work

- Campaign EM studies found that response similarity predicts anatomical connections in the MICrONS mouse
  (sci:sha256:c59a7cc9c394931da48264dbdd64f4dd2ef21ea50f820313c35558be9be14d07, sci:sha256:eab8ce57aa9d50d12c54327bd737b6d67304e2e8291015223a987a93d69661c4) and, with a frame-level measure, in the V1 Deep Dive mouse
  (sci:sha256:8bb073457bc086e9d83054432643758eba498d8d03760b66d3d369632aa4e2fa), while trial-level noise correlation did not predict synapses
  (sci:sha256:e9455e37a00547b613cd8ac12ee466cdd4b5cbc7b7684413cb08d05a9e0ab1dd, sci:sha256:a932e167db12bf26d795ad8563c1a4e69a73735703fecc15fa9b916dcaa6cf42). Our result is causal (photostimulation), not anatomical,
  and it uses spontaneous activity, not stimulus responses. It agrees with the noise-correlation nulls: the
  shared fluctuation of two neurons does not mark a direct effect.
- Campaign whole-brain studies found that wiring explains only a small part of pair-specific functional
  coupling in worm, fly, zebrafish, mouse and human data (sci:sha256:68f4f3d6d1e6b7d273909d7e434fe224f63dce4ad18b78cd94caaf5bd758c46b, sci:sha256:8c65c10b37dabd498acbaf41f5c4be7b8185c82f38d92f1f341a865a6e48723d).
  Our data give the same answer at the single-neuron, causal level in mammalian cortex.
- The only earlier campaign photostimulation work used the C. elegans signal propagation atlas
  (sci:sha256:fbb2992177f3a36ef3a7d7199b1f39b030e515e27731b7f2da0c400d3037159e, sci:sha256:cd13bf50e393d936da951778efe0a2dec719ce9281d185e3f51c2e284a4f8cbf).
- Finkelstein et al. (Nature 2025, doi:10.1038/s41586-025-09758-6) reported local like-to-like excitation
  and longer-range inhibition in ALM. In MOp, under this dataset's protocol, we saw net suppression from 50 to
  about 300 um and no clear net excitation of the population at 30-50 um. We did not test tuning-based
  like-to-like rules. Their DANDI release (001612) has no photostimulation metadata, so we could not use it.

## Figures

- `files/figures/fig1_distance_profile.png`: (A) specific influence vs distance (responder mean from far
  targets removed), before and after the task, mean of mouse means and bootstrap band; (B) percent of single
  pairs with |t| > 3; (C) raw ROI fluorescence, neuropil fluorescence and dF/F responses vs distance in one
  session (767715, 2025-02-10, first 700 trials).
- `files/figures/fig2_influence_vs_coactivity.png`: (A) per-session partial r of W with C (dot, +-1.96/sqrt(n))
  and the reliability ceiling (band); (B) pooled corrected partial r for the four C definitions.
- `files/figures/fig3_reliability_cell_direction.png`: (A) pair-level reliability of W and C; (B) post hoc
  shared-input test with the timing control; (C) direction test (H5).

## Results table (pooled; mean of mouse means; 95% hierarchical bootstrap CI)

| Quantity | Estimate | 95% CI | Mice > 0 | Sessions > 0 |
| --- | --- | --- | --- | --- |
| H1 partial r, W vs C, before task | -0.0044 | -0.0096 to 0.0003 | 1/5 | 7/26 |
| H1 corrected r, before task | -0.024 | -0.052 to 0.001 | | |
| Reliability ceiling r, before task | 0.164 | 0.133 to 0.195 | | |
| W reliability (Spearman-Brown, after controls) | 0.140 | 0.089 to 0.226 | | |
| C reliability (Spearman-Brown, after controls) | 0.245 | 0.186 to 0.305 | | |
| H1 partial r, after task | 0.0015 | -0.0017 to 0.0043 | 4/5 | 15/22 |
| H1 corrected r, after task | 0.009 | -0.010 to 0.031 | | |
| H3 change of partial r (after - before) | 0.0050 | 0.0011 to 0.0090 (Holm p 0.11) | 5/5 | 15/21 |
| H4 slope, change of W on change of C | -0.0008 | -0.0018 to -0.0000 (Holm p 0.13) | 1/5 | 5/21 |
| H5 sign agreement | 0.499 (22,398 / 44,855) | binomial p 0.78 | | |
| W stability, before vs after (ratio to reliability) | 0.85 | 0.66 to 1.00 | 5/5 | 25/25 |
| E1 received influence vs population coupling (rho) | -0.038 | -0.102 to 0.021 | 1/5 | 13/26 |
| E2 sent influence vs population coupling (rho) | -0.045 | -0.169 to 0.066 | 2/5 | 14/26 |
| Post hoc: input-profile similarity vs C (partial r) | 0.0076 | 0.0018 to 0.0186 | 5/5 | 24/26 |
| Same with labels shifted 3 trials | -0.0026 | -0.0082 to 0.0018 | 2/5 | 10/26 |
| Real minus shifted | 0.0102 | 0.0019 to 0.0248 | 5/5 | 21/26 |
| Post hoc: influence reciprocity r (all / < 100 um) | 0.011 / 0.053 | -0.017 to 0.035 / -0.022 to 0.134 | | |

All values are in `files/results/pooled.json`; per-session values are in `files/results/session_table.csv`
and `files/results/per_session*/`.

## Limitations

- Five mice. The hierarchical bootstrap with 5 mice can give CIs that are too narrow. Session-level sign
  counts are given for each quantity.
- Pair-level reliability is low for both measures (about 20 trials per target, about 220 s of spontaneous
  data). The null for H1 is informative only through the reliability correction. A true link below about
  r = 0.05 on the reliable parts cannot be excluded.
- Influence is measured with calcium imaging (GCaMP) at one plane. Responses of 100-400 ms include
  polysynaptic effects. Off-plane neurons can be stimulated; we excluded responders within 30 um of the
  laser spot and repeated the test at 50 um.
- Responder ROIs are soma-like ROIs by area and shape (the AIND classifier marks few ROIs as somata). The
  test with classifier somata only gave the same result.
- Cell type is not known. GCaMP is in excitatory and inhibitory neurons in this dataset.
- The near-target dF/F profile (30-50 um) is affected by neuropil. The distance spline controls distance in
  H1, but distance-dependent artefacts can remain.
- BCI threshold and performance data are not usable from the NWB files (see the SWDB data book), so we did not
  relate any change to learning performance.
- The shared-input result is post hoc and its size is uncertain.

## What remains open

- Does a stimulus-driven or task-driven co-activity measure (not spontaneous) predict influence in this
  dataset? The BCI epoch (not used here) gives task activity.
- Does the conditioned neuron of the BCI task change its influence or its received influence more than
  other neurons? This is the subject of the dataset authors' preprint (doi:10.64898/2026.03.03.709199) and
  we did not test it.
- A pre-registered replication of the shared-input result, with more trials per target, is needed.

## Reproduction

1. Make a work folder outside the signed bundle: `mkdir -p W/code W/scratch/logs` and copy
   `files/code/*` to `W/code/`, `files/provenance/session_order.txt` to `W/scratch/`.
2. Python 3.12 with numpy, scipy, matplotlib. Install numcodecs into a private folder:
   `pip install --target W/pylib numcodecs==0.15.1 --no-deps; pip install --target W/pylib deprecated wrapt --no-deps`.
   If IPv6 is broken on the host, copy `code/ipv4_sitecustomize.py` to `W/ipv4/sitecustomize.py`.
3. `cd W; bash code/run_all.sh` downloads each session's zarr chunks from the public S3 bucket (about
   1.4 GB per session, 2 parallel transfers, about 8 min per session) and writes reduced arrays to
   `W/scratch/sessions/` (raw dF/F is not kept).
4. `bash code/stats_follow.sh` (or `python3 code/session_stats.py`), then `python3 code/shared_input.py` and
   `SHIFT=3 python3 code/shared_input.py`, then `PYTHONPATH=./pylib:./code python3 code/neuropil_check.py`,
   then `python3 code/pool.py` and `python3 code/figures.py` (figures go to `W/result/files/figures`).
5. `files/provenance/sessions_used.json` lists each S3 prefix with the SHA-256 of its `.zmetadata` and
   `data_description.json` on 2026-11-12. The survey of all 31 processed sessions is in
   `files/provenance/survey.json`. Exclusions: mouse 772414 (30 Hz, almost no soma ROIs) and the duplicate
   processing of 731015 2025-01-28 18-56-35.

## Data licence and attribution

See `files/NOTICE.md`. The source data are CC BY 4.0 (Allen Institute for Neural Dynamics). No raw data are
in this bundle; the bundle has only our code, aggregate statistics, figures and text.
