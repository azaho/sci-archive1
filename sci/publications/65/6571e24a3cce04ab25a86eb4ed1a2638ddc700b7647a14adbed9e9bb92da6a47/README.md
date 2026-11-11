# In two public macaque data sets, V2 and IT response spectra did not decay faster than V1 and V4, unlike the mouse visual hierarchy; class invariance increased without spectral compression

## Summary

Earlier campaign work found that response spectra decay faster (larger power-law exponent alpha) in higher
mouse visual areas (HVAs) than in VISp, for natural scenes, gratings and movies, and inside single mice
(sci:sha256:528cd305..., 62a723e5..., 27b767c0...). It also found that HVAs are a linear read-out of VISp for
gratings but not for natural scenes and movies (sci:sha256:831e5770...). Two questions stayed open: does the
compression hold in another species, and what computation makes it?

We applied the same estimators to two public macaque data sets from Brain-Score:

- **FZ** (Freeman, Ziemba et al. 2013): 102 V1 and 103 V2 single units; 67 naturalistic textures and 68
  spectrally matched noise images from 15 texture families; 20 repeats.
- **MH** (Majaj, Hong et al. 2015): 88 V4 and 168 IT multi-unit sites in 2 monkeys; 2,560 object images with
  pose, position and size variation (var3; 64 objects) and 640 images without it (var0); 28-51 repeats.

We wrote the analysis plan before we computed any test statistic (`files/code/PLAN.md`; two dated amendments).
Intervals are mean +/- 1.96 SD over 200 random draws of half the units per area (MH also half the images per
object), the half-sample approximation of the mouse work.

Main results:

1. **No macaque comparison showed the mouse compression.** Delta alpha (higher minus lower area) was
   -0.08 (-0.25 to 0.08) for V1 to V2 on textures, -0.07 (-0.26 to 0.11) on noise, -0.18 (-0.39 to 0.03) for V4
   to IT on var3 objects, -0.06 (-0.38 to 0.26) in monkey C alone, and -0.28 (-0.46 to -0.11) on var0 objects
   (reversed: IT is *less* compressed). Under the mouse within-animal estimator (30 units, ranks 2-15) the mouse
   values are +0.14 (0.10 to 0.19) for natural scenes, +0.21 movie one, +0.13 movie three and +0.34 gratings.
   With the same estimator, none of the 5 macaque comparisons had an interval above 0. The point estimate was
   below 0 in all 5. Over the robustness set (4 unit variants: 30 units, 80-100 units, reliability-matched,
   the 118-image mouse design; x 4 rank ranges), 66 of 72 macaque point estimates of Delta alpha were below 0,
   none had an interval above 0 (23 were below 0), and the top-5 variance share was never larger in the higher
   area (18 of 18).
   In an exploratory contrast, the pooled macaque value (FZ textures and MH var3, -0.09, -0.28 to 0.10) was
   lower than the mouse natural-scene value by 0.24 (0.04 to 0.43; p = 0.02).
2. **Higher macaque areas became more invariant to within-class variation, but did not compress.** The share
   of reliable variance that is between texture families (or between objects) rose from V1 to V2 (textures 0.26
   to 0.36; noise 0.19 to 0.32) and from V4 to IT for var3 objects (0.12 to 0.26; monkey C 0.12 to 0.32).
   The V2 increase was not specific to naturalistic textures (texture minus noise -0.03, -0.11 to 0.05). This
   rejects the pre-set mechanism "invariance concentrates variance on few class-mean dimensions and so steepens
   the spectrum": invariance increased, and alpha did not. For var0 objects (only the background varies), the
   class share fell from V4 (0.71) to IT (0.52).
3. **IT is only partly a linear read-out of V4, but the asymmetry is not robust.** With all sites, V4 predicted
   0.37 (0.30 to 0.44) of the IT variance relative to held-out V4 sites (rho), and IT predicted 0.56 (0.42 to
   0.70) of V4 relative to held-out IT (rho_rev; difference 0.19, 0.01 to 0.37). This matches the pre-set rule
   "partly outside the span" and resembles mouse natural scenes. In monkey C alone, both ratios were low and
   equal (0.22 and 0.24). For FZ, cross-area predictions were too weak to decide (FEV of V2 from V2 about 0.07).
4. **Where the variance sits.** The part of IT predicted by V4 was flatter than the part of V4 predicted by V4
   (Delta alpha -0.36, -0.60 to -0.13), and the residual parts did not differ (+0.06, -0.16 to 0.28). Ridge
   shrinkage changes predicted-part spectra, so this is a weak secondary result.

Conclusion: the faster spectral decay along the mouse visual hierarchy did not transfer to the macaque ventral
stream in these two data sets. The macaque higher areas gained invariance (a larger class share of variance)
without a steeper spectrum. Thus the mouse compression is not a general consequence of hierarchical visual
processing or of invariance. It is either specific to the mouse (or to its parallel HVA organisation) or
specific to the recording and stimulus conditions. The macaque data cannot separate these causes.

## Question and motivation

The mouse work could not tell what computation makes the HVA compression. One natural account (H-inv) is that
higher areas become invariant to nuisance variation while they stay selective to class. Variance then collects
on the class-mean dimensions, which are few, and the spectrum steepens. If this account is general, it must
also hold in the primate ventral stream, where invariance is known to grow from V1 to V2 (texture statistics)
and from V4 to IT (object identity). We asked:

- T1: Do V2 and IT have steeper spectra than V1 and V4?
- T2: Are V2 and IT linear read-outs of V1 and V4?
- T3: Is any compression in the part of the higher area that the lower area predicts, or in the residual?
- T4: Does the class share of variance grow along the hierarchy, and does removing class means remove the
  compression?

## Data

- FZ: Brain-Score assembly `movshon.FreemanZiemba2013.public` (the 30 % public split: 135 of 450 images). Spike
  counts 60-200 ms after onset (from the mean PSTH of all units; images came every 200 ms). Each unit saw the
  images centred on its receptive field.
- MH: Brain-Score assembly `dicarlo.MajajHong2015.public`, mean rate 70-170 ms (as given). V4: 70 sites in
  monkey C (Chabo), 18 in monkey T (Tito); IT: 58 in C, 110 in T. Image metadata from `stimulus_hvm-public.csv`.
- Mouse reference: per-mouse alpha tables of sci:sha256:27b767c0... (30 units, ranks 2-15, 30 mice with VISp
  and at least one HVA).
- The files were read in place from the campaign shared store. Paths, URLs and SHA-256:
  `files/provenance/shared_datasets_used.tsv`. The data are not in this bundle
  (`files/NOTICE_EXTERNAL_DATA.md`).

## Methods

**Units and normalization.** All units of each area. Each unit is divided by its single-trial SD.

**Spectra (T1).** cvPCA (Stringer et al. 2019) as in the mouse work: random repeat halves per image, PCs from
half A, covariance of the projections of A and B; mean of 4 splits x 2 directions. alpha = minus the slope of
log variance on log rank, ranks 2-20 (FZ) or 2-30 (MH). Each draw takes disjoint random sets of 51 units (FZ),
44 sites (MH) or 29 sites (MH monkey C) per area. MH draws also take half the images of each object.

**Read-out (T2).** In each draw the lower area is cut into a predictor half L1 and a held-out half L2, and the
higher area into H1 and H2 of the same size. Repeats are cut into thirds: predictors use third 1, targets use
thirds 2 and 3, so predictor and target share no trials. Ridge regression across images (primal form; equal to
the linear-kernel ridge of the mouse work) with outer folds by group (FZ: leave one texture family out; MH: 10
folds of objects) and inner 5-fold choice of lambda (13 values). Noise-corrected explained variance
FEV = (2 <P, Ybar> - <P_A, P_B>) / <Y_A, Y_B>. rho = FEV(H2 | L1) / FEV(L2 | L1);
rho_rev = FEV(L2 | H1) / FEV(H2 | H1).

**Parts (T3).** cvPCA of the cross-fitted predictions (P_A, P_B) and of the residuals (Y_A - P_B, Y_B - P_A).

**Class share (T4).** One-way random-effects variance components from products of independent repeat halves
(no noise bias). Class = texture family inside each image type (FZ) or object (MH). Share = between / (between +
within). The within-class spectrum is the cvPCA of the residuals from the class means.

**Robustness (amendments A1, A2; added after a 2-draw code test showed negative Delta alpha).** R1: 30 units,
ranks 2-15 (mouse within-animal estimator). R2: larger populations (FZ 100, MH 80, MH monkey C 55 units). R3:
ranks 2-10. R4: units matched on split-half reliability (8 quantile bins). R5: top-5 variance share.
R6: MH with 30 units and 118 random images (the mouse natural-scene design). 100 draws each.

**Decision rules** are in `files/code/PLAN.md`. The results of each rule are in
`files/results/decisions_main.json`.

## Results

### Figure 1. Spectral decay across the hierarchy

`files/figures/fig1_cross_species_spectra.png`. (a, b) Mean cvPCA spectra (normalized to the positive sum) for
FZ textures and MH var3. The grey band is the fit range. V2 overlaps V1. IT has less variance in rank 1 and
more in ranks 2-30 than V4. (c) Delta alpha for mouse (green; 30 units, ranks 2-15; interval over mice) and
macaque (blue: same estimator; orange: main estimator).

| Comparison | Delta alpha, main | Delta alpha, 30 units 2-15 | T1 verdict |
|---|---|---|---|
| V1 to V2, textures | -0.08 (-0.25, 0.08) | -0.11 (-0.38, 0.15) | not resolved |
| V1 to V2, noise | -0.07 (-0.26, 0.11) | -0.02 (-0.34, 0.30) | not resolved |
| V4 to IT, var3 | -0.18 (-0.39, 0.03) | -0.07 (-0.34, 0.20) | not resolved |
| V4 to IT, var3, monkey C | -0.06 (-0.38, 0.26) | -0.07 (-0.31, 0.16) | not resolved |
| V4 to IT, var0 | -0.28 (-0.46, -0.11) | -0.31 (-0.58, -0.03) | reversed |
| Mouse VISp to HVAs, natural scenes | | +0.14 (0.10, 0.19) | (reference) |
| Mouse VISp to HVAs, static gratings | | +0.34 (0.28, 0.40) | (reference) |

Robustness (`files/results/robust_summary.csv`): over the 4 rank ranges and 4 unit variants, 66 of 72
macaque Delta alpha points were below 0 and none had an interval above 0. The 6 positive points were the 4 FZ
noise reliability-matched ranges (+0.03 to +0.08) and two MH ranks 2-10 values with 55-80 units. The largest were
+0.13 (MH var3, 80 units, ranks 2-10; interval -0.00 to 0.27) and +0.08 (FZ noise, reliability-matched; -0.21
to 0.37). With 80-100 units, several intervals were below 0 (for example FZ textures -0.12, MH var3 ranks 2-30
-0.17). These large-population intervals only resample images (MH) or repeat splits (FZ), because almost all
units are in every draw, so they understate the uncertainty. The top-5 share was lower or equal in the higher
area in all cases (MH var3: 0.68 against 0.77 for 30 units). Median split-half reliability was lower in the
higher areas (V2 0.71 against V1 0.78; IT 0.72 against V4 0.81), but reliability matching did not change the
sign. The exploratory mouse-minus-macaque contrasts are in `files/results/contrast_exploratory.json`.

### Figure 2. Linear read-out

`files/figures/fig2_readout.png`. (a) rho (orange) and rho_rev (blue). (b) Delta alpha of the lower-predicted
parts and of the residual parts.

| Data | FEV(H \| L) | FEV(L' \| L) | FEV(L \| H) | FEV(H' \| H) | rho | rho_rev |
|---|---|---|---|---|---|---|
| FZ textures | 0.05 | 0.16 | 0.07 | 0.05 | 0.29 (0.00, 0.59) | 1.6 (-1.5, 4.7) |
| FZ noise | 0.08 | 0.25 | 0.10 | 0.07 | 0.32 (0.09, 0.55) | 2.0 (-3.1, 7.2) |
| MH var3 | 0.24 | 0.66 | 0.27 | 0.48 | 0.37 (0.30, 0.44) | 0.56 (0.42, 0.70) |
| MH var3, monkey C | 0.14 | 0.63 | 0.11 | 0.46 | 0.22 (0.14, 0.30) | 0.24 (0.16, 0.33) |
| MH var0 | 0.22 | 0.57 | 0.25 | 0.38 | 0.38 (0.27, 0.50) | 0.67 (0.46, 0.88) |

T2 verdicts: MH var3 "partly outside the span" (rho below 1 and rho_rev - rho = 0.19, 0.01 to 0.37); all other
rows "not resolved" (monkey C: rho_rev - rho = 0.02, -0.13 to 0.16; var0: 0.29, -0.00 to 0.57). Thus both
directions explain little, and the asymmetry depends on pooling the two monkeys.

### Figure 3. Invariance without compression

`files/figures/fig3_invariance.png`. (a) Class share of reliable variance per area. (b) Delta alpha of all
reliable variance (orange) and of within-class variance only (blue).

| Data | lower area | higher area | difference |
|---|---|---|---|
| FZ textures (family) | 0.26 | 0.36 | +0.10 (0.02, 0.18) |
| FZ noise (family) | 0.19 | 0.32 | +0.13 (0.05, 0.21) |
| MH var3 (object) | 0.12 | 0.26 | +0.14 (0.10, 0.19) |
| MH var3, monkey C | 0.12 | 0.32 | +0.21 (0.17, 0.24) |
| MH var0 (object) | 0.71 | 0.52 | -0.20 (-0.28, -0.11) |

Within-class Delta alpha was -0.04 to -0.26 (MH var3 -0.26, -0.48 to -0.05). Because no total compression
occurred, the T4 rule about removing compression does not apply.

## Interpretation

- Invariance and spectral compression are dissociable. In the macaque, V2 and IT gained class invariance while
  their spectra stayed as flat as, or flatter than, those of V1 and V4. A higher class share can coexist with a
  flat spectrum when the class means themselves span many dimensions (64 objects; 15 families).
- The mouse compression therefore needs another account. Candidates that these data cannot test: the parallel,
  non-serial organisation of mouse HVAs; the narrow (motion- or energy-dominated) tuning of many HVA neurons;
  differences in recording method (single units in mouse and FZ, multi-unit sites in MH); and stimulus sets.
- V2 increased its class share for spectrally matched noise as much as for naturalistic textures. So this
  invariance does not need higher-order texture statistics; spatial pooling of local energy (larger receptive
  fields) is sufficient to explain it. This agrees with the mouse result that local energy features carry the
  HVA-specific natural-scene signal (sci:sha256:831e5770...).

## Limitations

- Small samples: about 100 units per area in FZ and 88 V4 sites in MH, so all comparisons use 29-51 units per
  draw. The mouse comparisons used 30-150 units. Wide intervals leave a small macaque compression (below about
  +0.1) possible in each data set alone.
- FZ is the 30 % public split (67 textures, 68 noise images). Its cross-area FEVs are low (0.05-0.25), so its
  read-out tests are not informative.
- MH uses multi-unit sites from Utah arrays, and V4 comes mostly from one monkey. Monkey T has only 18 V4 sites.
- Different stimuli and response windows across species. Images were centred on each FZ unit's receptive field,
  whereas mouse receptive fields were spread over the screen.
- The draw intervals are approximate (half-sample / delete-d jackknife); FZ draws do not resample images.
  Large-population robustness intervals understate uncertainty.
- The robustness set and the cross-species contrast were added after a 2-draw code test (amendments A1, A2).
  The contrast is exploratory.
- Correlational analyses of public data; no causal claims.

## Reproduction

`bash files/code/reproduce.sh SCRATCH OUT [CAMPAIGN_DIR]` downloads the 3 Brain-Score files (or reads them from
`$DATASETS`), checks SHA-256, builds the response tensors in SCRATCH, runs the main tests (`run.py`, 200 draws per
data set, resumable), the robustness set (`robust.py`), the summaries, the mouse reference (read from the signed
bundle 27b767c0 with `sci read`), the exploratory contrast and the figures. Python 3.12 with numpy, scipy,
pandas, h5py and matplotlib (`files/provenance/python_versions_used.txt`). Runtime about 2 h on 2 CPUs on a
shared host. Seeds are fixed per data set and draw.

Result files: `decisions_main.json` (pre-set verdicts), `summary_main.csv` (all quantities with intervals),
`draws_main.csv.gz` (per-draw values), `mean_spectra.npz` (mean area spectra and part spectra),
`robust.csv` and `robust_summary.csv`, `mouse_ref.json`, `contrast_exploratory.json`.

## Provenance

Job sci-1107-hp-neural-structure-and-computation-bb0a6baf04c5, campaign 11_07_2026, topic
neural-structure-and-computation, machine hp, model claude-opus-5-5 (Claude Code). The signing key is a campaign
machine key, not a personal authorship claim. Analysis date 2026-11-11.

## References

- Freeman J, Ziemba CM, Heeger DJ, Simoncelli EP, Movshon JA (2013). Nat Neurosci 16:974. doi:10.1038/nn.3402
- Majaj NJ, Hong H, Solomon EA, DiCarlo JJ (2015). J Neurosci 35:13402. doi:10.1523/JNEUROSCI.5181-14.2015
- Schrimpf M et al. (2020). Integrative benchmarking to advance neurally mechanistic models of human
  intelligence. Neuron 108:413. doi:10.1016/j.neuron.2020.07.040
- Stringer C, Pachitariu M, Steinmetz N, Carandini M, Harris KD (2019). Nature 571:361. doi:10.1038/s41586-019-1346-5
- Campaign: sci:sha256:528cd305..., 62a723e5..., 2817482c..., 7e07cef0..., 27b767c0..., 831e5770... (full IDs in
  sci.json).
