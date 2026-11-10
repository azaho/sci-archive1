# In 32 Allen Neuropixels mice, higher-area spectral compression for natural scenes and movies is absent on VISp axes but present on other higher-area axes; pooled VISp units do not reproduce it

## Summary

Earlier work found that response spectra decay faster (larger exponent alpha) in areas that are higher in the
anatomical mouse visual hierarchy. This occurs for natural scenes, static gratings and two natural movies
(sci:sha256:528cd305..., sci:sha256:62a723e5...). Receptive-field (RF) size, RF position and RF-based model
units did not explain most of it. Saved spectra alone cannot show where in stimulus space the compression is
(sci:sha256:b00225bf..., sci:sha256:bf04e82f...). We used the trial-level responses of the same 32 mice
(11,559 units, 8 structures) to ask two questions:

- **Q1, geometry.** Does a higher area put its reliable variance on the dominant stimulus axes of VISp (a
  "low-pass" of the VISp representation), or on other axes?
- **Q2, computation.** Can a simple pooling of real VISp units (each model unit is the mean of m VISp units of
  one mouse) give the alpha of higher areas for all four stimulus sets?

We measured the variance of a target population on the stimulus axes of a different basis population.
The axes come from one third of the trials, and the target variance comes from the other two thirds, so the
estimate has no noise bias. Main results (hierarchy slopes over the 6 cortical areas, 95% half-sample
intervals over mice):

1. **Gratings: most of the compression is on VISp axes.** On VISp axes the slope of alpha was 0.45 (0.25
   to 0.64), 69% (43% to 94%) of the slope on same-area axes (0.65). By the pre-set rule, the grating
   compression "lies on VISp axes". Exploratory: the VISp axes that the higher areas kept were the
   phase-invariant ones (Spearman 0.44 to 0.69 in VISl, VISal, VISpm and VISam).
2. **Natural scenes and movies: the compression is not on VISp axes.** On VISp axes the slope was 0.01
   (-0.17 to 0.20) for natural scenes, 0.08 (-0.08 to 0.24) for movie one and 0.00 (-0.15 to 0.15) for movie
   three. On same-area axes it was 0.14 (-0.01 to 0.29), 0.28 (0.15 to 0.42) and 0.17 (0.04 to 0.30). The
   difference was significant for movie one (0.20; 0.06 to 0.34). For natural scenes (0.13; -0.07 to 0.32) and
   movie three (0.17; -0.03 to 0.36) the pre-set rule gives "inconclusive".
3. **Exploratory: these axes are shared by higher areas and by mice. RF position does not explain them.**
   With bases from other mice, the advantage of own-area axes over VISp axes still grew with hierarchy
   (natural scenes 0.18, -0.00 to 0.36; gratings 0.20; movie one 0.20; movie three 0.14). On the axes of the
   other cortical areas, the natural-scene and movie slopes were as large as on own-area axes (difference
   -0.04, 0.03, -0.02). RF-position matching of targets to the VISp basis changed the hierarchy slope on VISp axes by 0.012
   or less.
4. **Pooled VISp units do not reproduce the higher areas.** Within m <= 13, no pooling rule (random, nearest RF,
   most similar drifting-grating tuning) reached the alpha of VISrl, VISal, VISpm or VISam for the four sets.
   Tuning-similar pooling met the pre-set criteria for VISl and LP only. This rule also raised the grating
   phase-invariant share from 0.79 to 0.88. All pooling models stayed aligned with VISp axes. Exploratory
   threshold and energy nonlinearities did not make an own-axis advantage (all values -0.21 to +0.01, against
   +0.08 to +0.17 in higher areas).

Conclusion: for gratings, higher areas mostly keep the phase-invariant part of the VISp representation. For
natural scenes and movies, the faster spectral decay is on stimulus axes that the higher areas share with
each other and across mice. These axes are not the dominant VISp axes. Simple linear or pointwise-nonlinear
pooling of the recorded VISp units does not make them. All results are correlational and use 6 cortical areas.

## Question and motivation

The spectral exponent alpha tells how fast reliable variance falls over dimensions, but not which dimensions
carry it. Two very different computations give a steeper spectrum in a higher area:

- **Low-pass inheritance.** The higher area keeps the dominant stimulus dimensions of VISp and attenuates the
  weak ones (for example by pooling over spatial phase or position). Then the higher area is steeper also when
  we measure it on VISp's own axes.
- **New features.** The higher area computes features that VISp represents only weakly, and these features have
  a steep spectrum. Then the steepness appears on the higher area's own axes but not on VISp axes.

Earlier work in this campaign showed that saved aggregate spectra cannot separate these cases
(sci:sha256:b00225bf..., sci:sha256:bf04e82f...). Trial-level responses can. We also asked whether a simple
pooling model of real VISp units can make the higher-area spectra. We wrote the analysis plan before we
computed any new spectrum (`files/code/PLAN.md`) and added four dated amendments (see "Changes to the plan").

## Data

- Allen Visual Coding Neuropixels, all 32 `brain_observatory_1.1` sessions (one mouse per session). We streamed
  spike times from the 32 NWB files with HTTP range reads. The S3 ETags are the same as in
  sci:sha256:62a723e5... (`files/provenance/vcn_nwb_etags.tsv`).
- Units: Allen quality filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9) in LGd (961
  units, 20 mice), LP (1,540; 21), VISp (2,230; 32), VISl (1,016; 24), VISrl (1,563; 28), VISal (1,675; 24),
  VISpm (950; 20) and VISam (1,624; 26). Total 11,559, as in the prior work.
- Stimulus sets: natural scenes (ns; 118 images, 50 repeats, 0-250 ms), static gratings (sg; 6 orientations x 5
  spatial frequencies x 4 phases, 45 repeats, 0-250 ms), natural movie one (nm1; 120 bins of 250 ms, 20
  repeats), natural movie three (nm3; 480 bins of 250 ms, 10 repeats). Drifting gratings (8 directions x 5
  temporal frequencies, 15 repeats, 0-2 s) were used only to define tuning similarity in the pooling model.
- RF metrics: `brain_observatory_1.1_analysis_metrics.csv`. RF-defined units have an RF permutation p < 0.01
  and an on-screen RF centre. In this CSV the labels `p_value_rf` and `on_screen_rf` are swapped (booleans in
  `p_value_rf`, three-decimal p-values in `on_screen_rf`); we used the corrected reading, as in the prior work.
- Hierarchy scores (Harris et al. 2019): LGd -0.515, VISp -0.357, VISl -0.093, VISrl -0.059, LP 0.105,
  VISal 0.152, VISpm 0.327, VISam 0.441.

The Allen files and all record-level derivatives are not in this bundle (`files/NOTICE_EXTERNAL_DATA.md`).

## Methods

**Units and estimator.** We scaled each unit by its single-trial SD. alpha is minus the OLS slope of log
variance on log rank over ranks 2 to 30. The hierarchy slope is the OLS slope of alpha on the hierarchy score
(6 cortical areas, primary; 8 structures, secondary). "Own axes" alpha is the standard cvPCA (split halves of
the repeats, 4 splits, both directions).

**Cross-basis spectrum (Q1).** For a basis population B and a disjoint target population A we split the repeat
indices into thirds T1, T2 and T3 (one split for all conditions, so trials of units recorded at the same time
stay disjoint). The stimulus axes u_k are the left singular vectors of the centred, trial-averaged responses of B
on T1, ordered by B variance. The variance of A on axis k is v_k = sum over units of (u_k' A_T2)(u_k' A_T3) /
n_conditions. Because T2 and T3 have independent noise, v_k estimates the signal variance of A on u_k without
noise bias. We used 4 random splits. Populations: 200 target units and 200 basis units, drawn without
overlap. For each area A we computed:
- alpha_{A|VISp}: on the axes of 200 VISp units (for the VISp target, other VISp units);
- alpha_{A|A*}: on the axes of 200 other units of A (same-area reference; it has the same basis noise);
- F10: the fraction of total reliable variance on the top 10 axes;
- the full 8 x 8 basis x target matrix (full sample, 10 draws).

Pre-set decision rule (per stimulus set): with s_V = slope of alpha_{A|VISp} and s_S = slope of alpha_{A|A*},
the compression "lies on VISp axes" if the s_V interval excludes 0 and s_V/s_S >= 0.5; it "lies on new axes" if
the s_V interval includes 0 and the s_S - s_V interval excludes 0; otherwise "inconclusive".

**VISp pooling models (Q2).** A model unit is the mean of m SD-scaled VISp units of one mouse on the same trials,
then SD-scaled again. Pool rules: rand (random units), rf (an RF-defined seed unit and its m-1 nearest RF
centres), tune (a seed unit and the m-1 units with the highest drifting-grating tuning correlation). Pools are
disjoint: each VISp unit enters at most one pool of a population, and pool sources are disjoint from the VISp
basis units. m = 1, 2, 3, 5, 8, 13; populations of 100 model units, compared with 100-unit data populations.
For each model population we computed own-axes alpha, alpha on VISp axes and the grating phase-invariant share
(the cross-validated share of grating variance in the phase-averaged responses). A noise-matched variant
added Gaussian trial noise to give each model unit the signal fraction of a single VISp unit (m = 1, 3, 8).
m*(A, set) is the m at which the model curve reaches the data alpha (linear interpolation in log m).
Pre-set rule: a pooling rule "accounts" for area A if, at the median m* over the four sets, the model alpha is
inside the data interval for at least 3 of 4 sets and the model phase share is inside its data interval.

**Exploratory tests (added after the first results; see "Changes to the plan").**
- *RF alignment* (`rfalign.py`): RF-defined units only. 100 VISp basis units; 80 target units of each cortical
  area either at random or matched one-to-one to basis RF centres (greedy nearest neighbour); self basis from
  100 other RF-defined units of the area (full sample). An offset curve shifted the target RF centres by up to
  40 degrees from the basis RF centres inside VISp.
- *Mouse split* (`mousesplit.py`): 100 random splits of the mice into two groups of 16. Targets (150 units) from
  one group. Bases (150 units) either from other units of the same mice or from the other mice. All 8 x 8 pairs.
- *Nonlinear pooling* (`nonlin.py`): pool outputs lin (mean), thr (max(mean - q, 0), q = 60th percentile) and
  energy (mean of max(x - q, 0)^2 over units, a complex-cell-like output). The "self" basis of a model is a
  second model population of the same kind from the other half of the VISp units. 6 full-sample draws and 30
  half-samples.
- *Grating axes* (`transfer.py`, stage axes): for each of the first 30 VISp grating axes, the share of the axis
  in the phase-constant subspace, and the ratio of target to VISp variance on the axis.

**Uncertainty.** As in the prior work, we did not use a mouse bootstrap, because duplicated mice put identical
units into one population and inflate alpha. We used half-sampling: 100 draws of 16 of the 32 mice without
replacement (same draw for all areas); interval = full-sample point +/- 1.96 SD over half-samples. Areas with
too few units in a half-sample were skipped in that draw. For the mouse-split test, each split already uses two
disjoint halves; we report the mean over 100 splits +/- 1.96 SD over splits. This is an approximate interval.

## Results

### Figure 1. Cross-basis spectra

`files/figures/fig1_cross_basis.png`: (a) natural-scene variance of four cortical targets on the VISp axes; (b-e)
alpha on own axes (cvPCA), on same-area axes (other units) and on VISp axes against hierarchy, with
half-sample intervals and cortical fit lines.

Cortical hierarchy slopes (95% half-sample intervals; `files/results/q1_slopes.csv`):

| Set | Own axes (cvPCA) | Same-area axes s_S | VISp axes s_V | s_S - s_V | s_V / s_S | Pre-set verdict |
| --- | --- | --- | --- | --- | --- | --- |
| Natural scenes | 0.19 (0.08, 0.30) | 0.14 (-0.01, 0.29) | 0.01 (-0.17, 0.20) | 0.13 (-0.07, 0.32) | 0.10 (undefined) | inconclusive |
| Static gratings | 0.66 (0.46, 0.87) | 0.65 (0.44, 0.86) | 0.45 (0.25, 0.64) | 0.20 (0.03, 0.38) | 0.69 (0.43, 0.94) | on VISp axes |
| Natural movie one | 0.35 (0.21, 0.49) | 0.28 (0.15, 0.42) | 0.08 (-0.08, 0.24) | 0.20 (0.06, 0.34) | 0.29 (-0.42, 1.00) | on new axes |
| Natural movie three | 0.23 (0.12, 0.33) | 0.17 (0.04, 0.30) | 0.00 (-0.15, 0.15) | 0.17 (-0.03, 0.36) | 0.02 (undefined) | inconclusive |

- The own-axes slopes reproduce the prior work (there with 300 units: 0.19, 0.69, 0.32, 0.21).
- Over all 8 structures the VISp-axis slopes were larger (0.17, 0.82, 0.24, 0.19), and the rule gave "on VISp
  axes" for gratings and both movies. This is because LGd has low alpha on every basis (it is the lowest
  point); the cortical result is the relevant test of the cortical trend.
- Per-area values (`q1_area.csv`). Natural scenes, alpha on VISp axes: VISp 0.76, VISl 0.59, VISrl 0.45,
  VISal 0.55, VISpm 0.74, VISam 0.65. On same-area axes: 0.77, 0.69, 0.81, 0.80, 0.83, 0.87. Thus on VISp axes
  the higher areas are *less* concentrated than VISp itself, although they are more concentrated on their own axes.
- Gratings, alpha on VISp axes: VISp 1.36, VISl 1.50, VISrl 1.41, VISal 1.57, VISpm 1.69, VISam 1.68. Thus the
  higher areas are more concentrated on VISp's own top axes than VISp is.
- Grating axes (exploratory, `axes_gain.csv`): across the first 30 VISp axes, the target/VISp variance ratio
  went with the phase-constant share of the axis (Spearman 0.59 VISl, 0.44 VISal, 0.68 VISpm, 0.69 VISam; -0.06
  VISrl; -0.89 LGd). Higher areas keep the phase-invariant VISp axes and attenuate the phase-dependent ones.

### Figure 2. VISp pooling models

`files/figures/fig2_pooling_models.png`: (a-d) alpha of 100-unit VISp pool populations against m, for three
pool rules (solid: plain; dashed: noise-matched), with the 100-unit data alpha of each area (dotted lines);
(e) grating phase-invariant share against m; (f) m* by area and stimulus set (points above 13: not reached).

| Set | VISp model, m = 1 | Best model, largest m | Data, 100 units: VISp / VISl / VISrl / VISal / VISpm / VISam |
| --- | --- | --- | --- |
| Natural scenes | 0.90 | 1.05 (tune, m = 13) | 0.91 / 0.92 / 1.06 / 1.04 / 1.06 / 1.10 |
| Static gratings | 1.52 | 1.77 (tune, m = 13) | 1.55 / 1.83 / 1.79 / 1.89 / 1.99 / 2.04 |
| Natural movie one | 1.13 | 1.26 (tune, m = 13) | 1.15 / 1.22 / 1.30 / 1.26 / 1.47 / 1.47 |
| Natural movie three | 0.78 | 0.98 (rf, m = 8) | 0.80 / 0.82 / 1.03 / 0.98 / 0.97 / 1.03 |

- Random and RF-local pools did not change grating alpha (1.46 to 1.54 for all m). Only tuning-similar pools
  raised it (1.54 to 1.77) and raised the phase-invariant share (0.79 to 0.88; data VISp 0.80, VISl 0.89,
  VISal 0.90, VISpm 0.92, VISam 0.92).
- For natural scenes and movies, all three rules raised alpha slowly, by 0.1 to 0.2 at m = 8 to 13.
- Pre-set test (`q2_tests.csv`): tune pooling "accounts" for VISl (median m* 5.1) and LP (2.2); with matched
  noise it accounts for LP only. No rule accounts
  for VISrl, VISal, VISpm or VISam. Random and RF pools account for no area other than VISp itself.
- The noise-matched variants gave the same pattern, so the result is not an effect of the higher SNR of pooled
  units.
- All pool models stayed aligned with VISp: their alpha on VISp axes rose with m (natural scenes, tune: 0.76 to
  0.84), while the data of higher areas on VISp axes were at or below VISp (100-unit populations: 0.44 to 0.75;
  VISp 0.75; `nonlin_rows.csv`).
- An exploratory variant with overlapping pools was dropped: with a finite source sample it made identical model
  units, and alpha rose to 4 to 14 (the same artefact as duplicated units in a mouse bootstrap).

### Figure 3. Area-specific axes

`files/figures/fig3_area_axes.png`: (a) natural-scene alpha of each target on the axes of each basis area (full
sample); (b) cortical hierarchy slope of the own-axis advantage alpha(own-area axes) - alpha(VISp axes) with
bases from the same mice or from other mice, and of alpha(own-area axes) - mean alpha(other cortical axes) with
bases from other mice; (c) the own-axis advantage of higher areas (mean of 5), VISp and VISp pool models
(m = 3, tune rule), with half-sample intervals.

Mouse split, cortical hierarchy slopes (mean over 100 splits, +/- 1.96 SD; `mousesplit_slopes.csv`):

| Set | Own-area axes, other mice | VISp axes, other mice | Other cortical axes, other mice | Own vs VISp, same mice | Own vs VISp, other mice | Own vs other cortical, other mice |
| --- | --- | --- | --- | --- | --- | --- |
| Natural scenes | 0.17 (0.02, 0.32) | -0.01 (-0.19, 0.17) | 0.21 (0.10, 0.32) | 0.22 (0.03, 0.40) | 0.18 (-0.00, 0.36) | -0.04 (-0.22, 0.14) |
| Static gratings | 0.62 (0.42, 0.82) | 0.42 (0.23, 0.62) | 0.45 (0.27, 0.62) | 0.21 (0.04, 0.38) | 0.20 (0.04, 0.35) | 0.17 (0.01, 0.33) |
| Natural movie one | 0.28 (0.10, 0.45) | 0.08 (-0.10, 0.26) | 0.25 (0.14, 0.37) | 0.21 (0.06, 0.36) | 0.20 (0.04, 0.36) | 0.03 (-0.14, 0.19) |
| Natural movie three | 0.17 (0.01, 0.33) | 0.03 (-0.14, 0.19) | 0.19 (0.09, 0.30) | 0.18 (0.01, 0.34) | 0.14 (-0.05, 0.34) | -0.02 (-0.18, 0.14) |

- The own-axis advantage was almost the same with bases from other mice. Thus the axes are a property of the
  area, not of the individual mice or of shared trial noise.
- For natural scenes and movies, the axes of the *other* cortical areas gave slopes as large as own-area axes.
  Only VISp axes did not. Higher areas share a set of stimulus axes that VISp does not emphasize. For gratings,
  part of the advantage is specific to each area (0.17).
- RF alignment (`rf_align.csv`, `rf_align_slopes.csv`): one-to-one RF matching to the VISp basis reduced the
  mean RF-centre distance from 5 to 8 degrees to 1 to 3.5 degrees (VISrl 6.7 degrees; few RF-defined VISrl units
  are near the VISp RFs). It changed the slope on VISp axes by -0.001 (ns), 0.01 (sg), 0.01 (nm1) and 0.01 (nm3);
  all intervals include 0. With RF-matched targets, the natural-scene own-axis advantage was VISl 0.01, VISrl
  0.16, VISal 0.17, VISpm 0.19, VISam 0.22 (full sample).
- Inside VISp, a requested RF offset of 40 degrees (achieved about 17 to 25 degrees, because the VISp RFs cover
  a limited field) lowered the natural-scene alpha on the basis axes by about 0.04 to 0.09 and F10 from 0.37 to
  0.29-0.36, and did not lower it for gratings (`rf_offset.csv`). RF position
  thus matters for natural-image axes, but the matching shows that it does not explain the higher-area axes.
- Nonlinear pooling (`nonlin_summary.csv`, m = 3, tune): the own-axis advantage of models was -0.05 to +0.01
  (linear), -0.10 to -0.01 (threshold) and -0.21 to -0.09 (energy), against +0.17 (0.04, 0.29) natural scenes,
  +0.08 (-0.03, 0.18) gratings, +0.09 (-0.00, 0.18) movie one and +0.10 (0.01, 0.19) movie three for the mean
  of the higher areas. Threshold and energy outputs also lowered alpha (natural scenes, tune, m = 3: 0.88 and 0.79
  against 0.94 for linear pools).

## Interpretation

The trial-level data separate two parts of the hierarchy trend that the saved spectra could not separate.

1. For gratings, higher areas keep and sharpen the dominant VISp axes. The kept axes are the phase-invariant
   ones. Pooling of VISp units with similar tuning gives the same direction of change (higher alpha and higher
   phase-invariant share). This agrees with a complex-cell-like pooling over phase from VISp, but the pooled
   VISp model reached only about the level of VISl within m <= 13.
2. For natural scenes and movies, the steeper spectra are on axes that higher areas share with each other and
   across mice, but that are weak in VISp. On VISp axes, higher areas are even less concentrated than VISp.
   Thus the higher areas do not only filter the VISp representation. They give most variance to stimulus
   features that VISp represents with little variance. These features are not set by RF position, and the
   recorded VISp units do not make them by linear pooling, rectification or squaring.

Possible sources of the shared higher-area axes are inputs that do not go through the recorded VISp
populations (for example LP or direct LGd inputs), recurrent computation among higher areas, or nonlinear features of many VISp neurons that our
small pools (m <= 13 of about 60 recorded VISp units per mouse) cannot sample. Our tests do not separate these
options.

## Limitations

- Correlational, area-level tests with 6 cortical areas. The hierarchy score is one summary of connectivity.
- For natural scenes and movie three the pre-set Q1 rule gave "inconclusive": the VISp-axis slope was near 0,
  but the same-area minus VISp-axis difference had an interval that included 0. The natural-scene and movie
  conclusion rests on the consistent pattern over three sets, on movie one, and on the exploratory mouse-split
  test with bases from other cortical areas.
- The cross-basis alpha depends on the quality of the basis axes (200 units, one third of the trials; movie
  three has only 3 repeats per third). This noise is the same for all targets on one basis, so comparisons on
  one basis are fair, but absolute cross-basis alpha values are lower than own-axis values.
- On VISp axes, the VISp target is a same-area target. This gives VISp an advantage on its own basis. We
  therefore also compared each area with its own-area basis and with the bases of other areas.
- Pooling models use only the recorded VISp units (about 60 to 70 per mouse), so m <= 13 with disjoint pools. A
  real higher-area neuron pools from many more VISp neurons. We cannot exclude that much larger or differently
  weighted pools reach the higher-area alpha. Overlapping pools could not be tested without duplicate-unit
  artefacts.
- The RF alignment test uses the coarse Allen RF map (10-degree grid) and only RF-defined units (11% to 62% of
  units). The mouse-split intervals come from the spread over splits, an approximation.
- The four exploratory tests (RF alignment, mouse split, nonlinear pooling, grating axes) were added after we
  saw the first results. They need independent confirmation.
- One data set (Allen Neuropixels). We did not repeat the tests in the two-photon data.

## Changes to the plan

`files/code/PLAN.md` holds the plan (written about 04:12 PST on 2026-11-10, before any new spectrum) and four
amendments: (1) 100-unit model populations and disjoint pools, after a 5-session pipeline test showed duplicate
artefacts with overlapping pools; (2) the RF alignment test, after the full-sample 8 x 8 matrix; (3) the mouse
split test, after the RF alignment result; (4) the nonlinear pooling test with a reduced number of half-samples,
because of host load. The planned Q1 and Q2 analyses and decision rules did not change.

## Reproduction

Run `bash files/code/reproduce.sh SCRATCH_DIR OUT_DIR` with Python 3.12, numpy, scipy, pandas, h5py,
matplotlib and remfile 0.1.15 (`files/code/requirements.txt`; versions used: `files/provenance/python_versions_used.txt`).
The script downloads the Allen metadata, streams about 15 GB from the public Allen S3 bucket into SCRATCH_DIR,
and writes all results and figures into OUT_DIR. All random seeds are fixed in the code. On the campaign host
(8 cores, load 30 to 50 from other jobs) the extraction took about 20 minutes with 6 streams, and the analyses
took about 4 hours in total.

Code: `extract_multi.py` (NWB streaming), `cache2.py` (response cache), `mlib.py` (cvPCA estimator, from the
prior work), `xlib.py` (cross-basis spectrum, pools, phase share), `transfer.py` (Q1, Q2, 8 x 8 matrix, grating
axes), `rfalign.py`, `mousesplit.py`, `nonlin.py`, `stats2.py` (Q1/Q2 statistics and decision rules),
`stats3.py` (RF alignment and mouse split), `stats4.py` (nonlinear pooling), `figures2.py`.

Result files (all aggregate statistics of populations, no Allen record-level data): `q1_slopes.csv`,
`q1_area.csv`, `q2_curves.csv`, `q2_tests.csv`, `q2_mstar_rows.csv`, `matrix.csv`, `axes_gain.csv`,
`rf_align.csv`, `rf_align_slopes.csv`, `rf_offset.csv`, `mousesplit.csv`, `mousesplit_slopes.csv`,
`nonlin_summary.csv`, `stats.json`, per-draw rows (`transfer_rows.csv`, `matrix_rows.csv`, `axes_rows.csv`,
`rf_align_rows.csv`, `rf_offset_rows.csv`, `mousesplit_rows.csv`, `mousesplit_rows_wide.csv`,
`nonlin_rows.csv`) and mean spectra (`transfer_spectra.npz`; keys `stim|population|kind`).

## Provenance

- Campaign 11_07_2026; job sci-1107-hp-neural-structure-and-computation-75e2d735db49; topic
  neural-structure-and-computation; machine hp; account claude-olen; model Claude Opus 5.5 (claude-opus-5-5).
  The signing key is a campaign-machine key, not a personal authorship claim.
- Shared campaign datasets used in place: `datasets/allen-vcn-ecephys-units-20261109/units.csv` (SHA-256
  1dffbe8d...f078), `datasets/allen-vcn-ecephys-channels-20261109/channels.csv` (d2932f1e...ed98),
  `datasets/allen-vcn-ecephys-bo11-analysis-metrics-20261109/brain_observatory_1.1_analysis_metrics.csv`
  (a5335a7a...5209). `probes.csv` and `sessions.csv` were downloaded on 2026-11-10 to private scratch. Full
  hashes, URLs and the NWB ETags are in `files/provenance/`.
- Analyses ran on 2026-11-10 (PST).

## References

- Stringer, C. et al. (2019) High-dimensional geometry of population responses in visual cortex. Nature 571,
  361-365. doi:10.1038/s41586-019-1346-5.
- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575,
  195-202. doi:10.1038/s41586-019-1716-z.
- Siegle, J.H. et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy. Nature
  592, 86-92. doi:10.1038/s41586-020-03171-x.
- Semedo, J.D. et al. (2019) Cortical areas interact through a communication subspace. Neuron 102, 249-259.
  doi:10.1016/j.neuron.2019.01.026.
- Prior campaign work: sci:sha256:528cd3055e8110bfe80850a3d0f4df5233b0107c2e49b127939faec009c029a1 (source
  finding), sci:sha256:62a723e53ba6232d2885da1ab1758e24642f7b716b47dbd39e6817285d4b0776 (stimulus generality, RF
  controls, model twins, phase invariance), sci:sha256:b00225bfa7494f6ddb391eb7fc07b397a1de5c807d1aadfb8547f25ff7c8cd82
  and sci:sha256:bf04e82fe4d22c952f24191caecedfb0de21df41724015dbdeee7b798fb58c59 (limits of saved spectra),
  sci:sha256:39fdce5888169dfdc22376ddb8c02fc68aa3f6f22472bd136e6f6b445608b6f4 (VISl-VISp crossover),
  sci:sha256:19f7eb8e97c3c505c7176cf992bc2c93b3ce4d8f97552f8f4484e6f79a14ea73 (reliability and distance from the
  retina).
