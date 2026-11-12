# In 32 Allen Neuropixels mice, higher-area natural-scene signal that VISp misses is present from the first response, is not a VISp timing effect, is shared with LP and is partly RF coverage

## Summary

Higher mouse visual areas (HVAs) have response spectra that decay faster than VISp. The prior work
(sci:sha256:831e5770...) found that, for natural scenes and natural movies, a large part of the reliable HVA signal
is not a linear read-out of the VISp population of other mice, and that the other HVAs predict each HVA better than
VISp does. We tested four explanations of this "HVA-specific" signal with the same 11,559 units in all 32 Allen
Visual Coding Neuropixels `brain_observatory_1.1` mice. The analysis plan was written before any new response
statistic was computed (`files/code/PLAN.md`; four dated amendments).

Main results (intervals: mean +/- 1.96 SD over random 16/16 splits of the mice):

1. **Not a VISp time-course effect (test A1).** A VISp read-out that can use five 50 ms time bins (and, for movies,
   the preceding 250 ms bin) did not close the gap. Mean HVA ratio rho = FEV(HVA | VISp) / FEV(VISp | VISp) was
   0.61 with the count read-out and 0.61 (0.49 to 0.72) with the time-resolved read-out for natural scenes; 0.91
   and 0.89 (0.70 to 1.08) for movie one; 0.78 and 0.78 (0.57 to 1.00) for movie three. A Gaussian kernel on the
   VISp time-bin features added at most 0.02. Static gratings (positive control): 1.05 (0.98 to 1.11). Same-mouse
   VISp on disjoint trials gave 0.54 (0.44 to 0.63), 0.80 and 0.69 (0.54 to 0.85).
2. **Present from the first response, not built up late (test C1).** With 10 ms spike bins and a causal VISp
   read-out, the natural-scene rho of HVAs was already low at 50-70 ms (0.47, 0.27 to 0.68) and 70-90 ms (0.67,
   0.49 to 0.85) and did not fall later (early minus late -0.03, -0.20 to 0.14). The other-HVA advantage was
   +0.11 (0.06 to 0.16) at 70-90 ms and stayed at +0.10 later. The hierarchy slope of the spectral exponent first
   had an interval above 0 at 90-110 ms (0.27, 0.03 to 0.51). For gratings rho was 1.00 to 1.05 in all windows.
3. **LP (mouse pulvinar) carries part of it (test B1), but its source is not identified.** Adding 150 LP units of
   other mice to 400 VISp units increased the HVA FEV by 0.047 for natural scenes, against 0.007 for 150 more
   VISp units (difference 0.040, 0.010 to 0.070) and 0.096 for 150 units of the other HVAs; for movie three 0.033
   against 0.004 (difference 0.029, 0.009 to 0.049). LP gave about half (0.49 and 0.45) of the other-HVA advantage.
   LP did not help VISp targets (-0.046) or gratings, and gave nothing for movie one. The LP gain rose along the
   hierarchy (slope 0.061, 0.026 to 0.096). With 400 units each, LP predicted natural-scene HVA responses about as
   well as VISp did (FEV ratio 0.83 to 1.57) but VISp responses only 0.42 as well. The LP gain was largest at 50-90 ms (0.06 to 0.08).
   In the same-mouse variant, the effect had the same sign but was not significant (natural scenes 0.020, -0.014
   to 0.054). In an exploratory precedence test, LP spikes *before* a target window did not predict the HVA-specific
   signal (70-90 ms: 0.017, -0.019 to 0.054), while HVA spikes before a window predicted LP at 90-150 ms (0.042 to
   0.044, intervals above 0). Thus the data do not show LP driving HVAs; LP and HVAs share the signal.
4. **Part of the gap is retinotopic coverage (test E).** The recorded VISp units have RF centres in a small part of
   the screen (1,202 of 1,386 significant RFs in azimuth 30-70 and elevation -10 to 30 deg), but many HVA units do
   not (for example 126 of 295 VISrl units have elevation <= -10). HVA units with RFs inside this box were better
   predicted by VISp than HVA units outside it (natural scenes rho +0.14, 0.03 to 0.26; movie three +0.20, 0.05 to
   0.35; movie one +0.16, -0.01 to 0.33; gratings +0.03). This partly challenges the prior statement that the gap
   is not an RF-position mismatch. But inside the box the natural-scene gap remained in most areas (rho VISl 0.73,
   VISrl 0.55, VISal 0.64, VISam 0.70, VISpm 0.94; pre-set verdict inconclusive). For in-box targets LP still added
   more than LGd for movie three (0.018, 0.002 to 0.035) but not significantly for natural scenes (0.028, -0.007
   to 0.064).

Conclusion: the HVA natural-scene signal that the recorded VISp population does not linearly predict is present in
the first 20-40 ms of the HVA response, so it does not need slow recurrent build-up. It is not a temporal re-weighting
of VISp spikes. It is shared with LP (and with other HVAs), and part of it comes from visual-field positions that
the VISp sample does not cover. The spectral compression across areas appears about 20 ms after the onset of the
image-specific signal. These are correlational results in one data set; the direction of the LP-HVA link is not
identified.

## Question and motivation

The prior work proposed that HVAs concentrate variance on "new dimensions" outside the linear span of VISp
(sci:sha256:2817482c..., sci:sha256:831e5770...). Which computation makes these dimensions was open. We asked:

- **H-time.** Is the HVA signal a linear function of VISp *dynamics* (transient vs sustained parts, preceding
  movie frames), which a spike-count read-out cannot use?
- **H-late.** Is the HVA-specific signal made by slow cortical recurrence or feedback? Then it should appear later
  than the VISp-predictable signal.
- **H-LP.** Does it come through the transthalamic route? LP (mouse pulvinar) projects to HVAs and sends them
  signals that differ from the V1 feedforward signals (Blot et al. 2021, Neuron 109, 1996-2008; Beltramo and
  Scanziani 2019, Science 363, 64-69; Tohmi et al. 2014, Curr Biol 24, 587-597).
- **Coverage (added after a check of RF positions, amendment 3/4).** Is part of the gap only that the VISp units
  sample other visual-field positions than the HVA units?

## Data

- Allen Visual Coding Neuropixels, all 32 `brain_observatory_1.1` sessions (one mouse per session), streamed with
  HTTP range reads (`files/provenance/source_nwb_etags.tsv`; ETags identical to the prior work).
- Units: Allen quality filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9) in LGd (961),
  LP (1,540), VISp (2,230), VISl (1,016), VISrl (1,563), VISal (1,675), VISpm (950), VISam (1,624).
- Stimuli: natural scenes (ns; 118 images x 50 repeats; spikes 0-250 ms in 10 ms bins), static gratings (sg; 120
  conditions x 45 repeats; control), natural movie one (nm1; 120 bins of 250 ms x 20 repeats) and three (nm3; 480
  bins x 10 repeats), with 3 sub-bins per 250 ms bin.
- RF centres from `brain_observatory_1.1_analysis_metrics.csv` (the `p_value_rf` and `on_screen_rf` labels are
  swapped in this file; we use the corrected columns, p < 0.01 and on screen).
- Hierarchy scores (Harris et al. 2019, Nature 575, 195-202): VISp -0.357, VISl -0.093, VISrl -0.059, VISal 0.152,
  VISpm 0.327, VISam 0.441.

## Methods

**Common design (as in the prior work).** For each split, the 32 mice are divided at random into a target group G1
(16) and a predictor group G2 (16). Target: 150 random G1 units of one area (50 in test E), repeats split into halves
A and B. Kernel ridge regression across stimulus conditions (10 outer folds, contiguous for movies; ridge lambda by
inner 5-fold CV). Noise-corrected explained variance FEV = (2 <P, Ybar> - <P_A, P_B>) / <Y_A, Y_B> uses only
products across independent halves. Each target unit is scaled by the single-trial SD of its 0-250 ms (or bin)
count; each predictor feature (unit x time block) by its own single-trial SD. Combined predictors are sums of
unit-trace kernels. Hierarchy slope: OLS slope over the 6 cortical areas. Interval: mean +/- 1.96 SD over splits
(the half-sample interval of the prior work). Main mode: predictors from G2 (other mice, all repeats). Same-mouse
mode: predictors are non-target G1 units on repeat third T1; targets use thirds T2 and T3.

**A (time-resolved read-out).** 400 VISp units as counts (C), time bins (T: 5 x 50 ms; movies: 3 sub-bins of the
current and of the preceding bin), C+T (CT, main), and CT plus a Gaussian kernel (median-distance bandwidth).
Splits: ns and sg 40, nm1 30, nm3 16, same-mouse 20 per movie/scene set.

**B (added structures).** VISp-CT400 plus 150 units of LP, LGd, more VISp (size control) or the other HVAs. Gain =
FEV(VISp + X) - FEV(VISp). Also LP400 and LGd400 alone.

**C (timing, ns and sg).** Target windows 30-50, 50-70, 70-90, 90-110, 110-150, 150-250 ms. Causal predictors use
all blocks (0-30 ms and the windows) that end at or before the end of the target window. Per window: signal
variance, rho, other-HVA advantage (400 units), LP gain, cvPCA alpha (ranks 2-20) and its hierarchy slope.

**D (exploratory precedence, ns, 30 splits).** As C, but the added LP, other-HVA (150 units each) or, for the LP
target, HVA (150 units) blocks either end before the target window starts ("lag") or include it ("all").

**E (RF coverage, amendments 3 and 4).** Box B = azimuth 30-70, elevation -10 to 30 deg. Targets: 50 G1 units with
significant RFs inside B ("in") or outside B ("out"). Predictor: 300 G2 VISp units with significant RFs (CT), alone
or plus 150 LP or LGd units. rho normalised by in-box VISp targets. Splits: ns 30, nm1 30, sg 20, nm3 12. A first
design (density-ratio matching of VISp RFs to each HVA) was dropped before it ran on responses because VISp units do
not cover the VISrl field (effective sample 79 of 707).

**Pre-set decision rules** are in `files/code/PLAN.md`. Verdicts (`files/results/stats/*tests*`):

| Test | ns | nm1 | nm3 | sg |
| --- | --- | --- | --- | --- |
| A1 other mice | gap remains | inconclusive | inconclusive | closes (control) |
| A1 same mice | gap remains | inconclusive | gap remains | not run |
| B1 other mice | LP carries HVA-specific signal | LP does not | LP carries | LP does not |
| B1 same mice | LP does not (same sign) | LP does not | LP does not | not run |
| C1 | present from the first response | - | - | other (rho about 1) |
| E1 | inconclusive (in-box 0.72, 0.50-0.93) | inconclusive | inconclusive | "closes" (no gap) |
| E2 | not shown | not shown | LP adds beyond coverage | not shown |

## Results

### Figure 1. Time-resolved VISp read-out (A)

`files/figures/fig1_time_resolved_readout.png`. rho for each HVA and the HVA mean under four VISp read-outs. The four
read-outs give nearly the same values. For natural scenes VISrl (0.37 to 0.39) and VISal (0.56 to 0.58) are lowest.
The VISp residual still holds the movie compression: hierarchy slope of alpha of the residual 0.38 (0.18 to 0.57) for
movie one against 0.17 (0.00 to 0.33) for the CT-predicted part; for movie three the two parts are not separated (0.21
and 0.22) with the CT read-out (`files/results/stats/A_alpha_parts.csv`).

### Figure 2. Added structures (B)

`files/figures/fig2_added_structures.png`. FEV gain over 400 VISp units from 150 units of LP, LGd, more VISp, or
other HVAs, other mice. LP and LGd both help VISrl (natural scenes +0.081 and +0.059), whose RFs lie mostly below the
VISp sample. For the other HVAs LP helps more than LGd. Beyond VISp plus other HVAs, LP added 0.024 (0.006 to 0.043) for
movie three; for natural scenes the value (0.012, -0.003 to 0.028) was not different from 0. Ratios of LP400 or LGd400 to VISp400 FEV
are in `files/results/stats/B_lp_ratio.csv`.

### Figure 3. Timing (C)

`files/figures/fig3_timing.png`. (a) The image-specific signal (variance across images after removal of the common
onset transient) rises over the response in all structures; LGd and LP lead. (b) HVA rho of a causal VISp read-out
per window: low from 50 ms for natural scenes, about 1 for gratings. (c) Other-HVA advantage (blue) and LP gain
(orange). (d) Hierarchy slope of alpha per window.

### Figure 4. RF coverage (E)

`files/figures/fig4_rf_coverage.png`. Top: rho for HVA units with RFs inside (blue) and outside (orange) the VISp
coverage box. Bottom: LP and LGd gains for in-box targets. Not every split has 50 in-box units of VISrl, VISal and
VISpm (21-29 of 30 splits); pre-set means use only areas present in every split (`files/results/stats/E_tests.csv`).

### Figure 5. Temporal precedence (D, exploratory)

`files/figures/fig5_precedence.png`. (a) Gain over the causal VISp read-out for HVA targets from LP or other-HVA
spikes up to the window end (filled) or only before the window (open). (b) The same for the LP target with HVA
spikes. (c) Share of the gain that earlier spikes give. Earlier HVA spikes predicted later LP and HVA signal from
90 ms on; earlier LP spikes did not significantly predict HVA signal in any window.

## Interpretation

- The HVA-specific natural-scene signal is not a re-weighting of VISp spike timing, and it is not built up by
  slow recurrence: it is there in the first image-specific HVA spikes. A fast feedforward nonlinearity, a parallel
  input, or fast recurrence within the first 20-40 ms all remain possible.
- LP shares this signal, more than LGd and more than extra VISp units do, and it helps most at 50-90 ms. This agrees
  with reports that LP sends HVA-specific signals (Blot et al. 2021). But the precedence test does not show LP
  leading; HVA spikes lead LP from 90 ms on, which agrees with cortico-thalamic feedback. Also, LP RFs are large and
  cover more of the visual field than the VISp sample. We therefore read the LP result as "LP is part of the network
  that holds the HVA-specific signal", not as evidence that LP makes it.
- Part of the prior "outside the VISp span" result is a sampling effect: the Allen VISp probes cover a small part
  of the visual field. Natural scenes and movies have spatially local structure, so a population that does not
  sample a position cannot predict signal from it; full-field gratings do not show this effect (in minus out
  +0.03). Future span tests should match RF coverage or use stimuli restricted to jointly covered positions.

## Limitations

- One data set (Allen Visual Coding Neuropixels, 32 mice); 6 cortical areas; the same units as the prior work.
- Predictor populations are finite (150-550 units) and noisy; FEV values of 0.1-0.4 mean that most target signal is
  unexplained by any predictor; gains are small (0.01-0.08).
- Same-mouse tests use only a third of the repeats for predictors and were not significant for LP.
- Split intervals are approximate (overlapping half splits); no correction for the number of tests.
- Test E has few in-box units for VISrl, VISal and VISpm, so its pre-set means use 2-3 areas; the box is coarse
  (RF centres lie on a 10 deg grid).
- LP is a heterogeneous nucleus; we did not separate its subdivisions. LP RFs are large, so part of the LP gain can
  be coverage. Analysis D is exploratory and has no pre-set rule; trial-averaged precedence is weak evidence on
  direction.
- Plan changes made after first results are listed in PLAN.md (amendments 2-4: analysis D added; analysis E added
  and redesigned before it ran).

## Files

- `files/code/`: `extract_multi.py` (NWB streaming; 10 ms bins), `cache4.py` (response cache), `encode4.py`
  (A, B, C), `encode_rf.py` (E), `encode_lag.py` (D), `klib.py` (kernel ridge, FEV, cvPCA), `stats4.py`,
  `stats_extra.py`, `figures4.py`, `figures_extra.py`, `run_all.sh` (how the runs were chained), `reproduce.sh`,
  `PLAN.md`, `ipv4_sitecustomize.py`.
- `files/results/stats/`: summary tables (`A_rho.csv`, `A_tests.csv`, `A_alpha_parts.csv`, `B_gains.csv`,
  `B_tests.csv`, `B_lp_ratio.csv`, `C_windows.csv`, `C_tests.csv`, `D_lag.csv`, `E_rho.csv`, `E_gain.csv`,
  `E_tests.csv`, `E_rf_medians.csv`, `summary_fev.csv`, `tests.json`, `E_tests.json`). Columns: quantity, mean, lo,
  hi (mean +/- 1.96 SD over splits), n_splits.
- `files/results/per_split/`: per-split population scores (FEV, signal variance, alpha) for all analyses.
- `files/provenance/`: NWB URLs, sizes and ETags; SHA-256 of shared metadata files; session IDs; package versions;
  job record.
- `files/NOTICE_EXTERNAL_DATA.md`: external data terms and what is not bundled.

## Reproduction

`bash files/code/reproduce.sh SCRATCH OUT` downloads the public Allen metadata, streams the 32 NWB files (about 15 GB
of range reads), builds the cache in SCRATCH and writes results and figures to OUT. Seeds are fixed per split
(20000 + s main, 30000 + s same-mouse, 40000 + s D, 50000 + s E), and runs are resumable. To redo only statistics
and figures from the bundled per-split rows, split `files/results/per_split/rows_main_same.csv.gz` by its `mode` and
`stim` columns into `rows_<mode>_<stim>_<split>.csv` files (the format of `encode4.py`), then run `stats4.py`,
`stats_extra.py` and the figure scripts.

## Provenance

Campaign 11_07_2026, job sci-1107-hp-neural-structure-and-computation-98185eae81f7, topic
neural-structure-and-computation, machine hp, model claude-opus-5-5 (Claude Code agent). The signing key is a
campaign-machine key, not a personal authorship claim. Data: Allen Institute for Brain Science, Allen Brain
Observatory Visual Coding Neuropixels (Siegle et al. 2021, Nature 592, 86-92).

## References

- Siegle, J.H. et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature 592, 86-92.
- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575, 195-202.
- Blot, A. et al. (2021) Visual intracortical and transthalamic pathways carry distinct information to cortical areas. Neuron 109, 1996-2008.
- Beltramo, R. and Scanziani, M. (2019) A collicular visual cortex: neocortical space for an ancient midbrain visual system. Science 363, 64-69.
- Tohmi, M. et al. (2014) The extrageniculate visual pathway generates distinct response properties in the higher visual areas of mice. Curr Biol 24, 587-597.
- Stringer, C. et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature 571, 361-365.
- Campaign prior work: sci:sha256:528cd3055e8110bfe80850a3d0f4df5233b0107c2e49b127939faec009c029a1,
  sci:sha256:62a723e53ba6232d2885da1ab1758e24642f7b716b47dbd39e6817285d4b0776,
  sci:sha256:2817482cca4da18cf0592fbbf8baaaeb70834cf07a3ef3a53494d5771dc4127d,
  sci:sha256:7e07cef073efcd9bec6989768b67a94241dc669bcebecb9a06123cd0c049bec3,
  sci:sha256:27b767c0f33dba4f164aa11f6d4486c1f34816e7506d58fc1031de22cc34f349,
  sci:sha256:831e577053b183e3eb589498dff71630547c926cc539da7f97267dcfb71a4dc6.
