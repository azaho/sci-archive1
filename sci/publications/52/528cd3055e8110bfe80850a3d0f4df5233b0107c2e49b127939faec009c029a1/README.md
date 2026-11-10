# Natural-image response spectra decay faster in higher mouse visual areas

## Summary

We measured how the reliable stimulus variance of mouse visual populations spreads across dimensions.
We used responses to the same 118 natural images in two public Allen Brain Observatory datasets:
Visual Coding Neuropixels (32 mice, 11,559 quality units in 8 visual structures) and Visual Coding
two-photon (193 mice, 38,466 excitatory cells in 6 cortical areas). For each area we calculated the
cross-validated PCA (cvPCA) eigenspectrum (Stringer et al. 2019) and fitted its decay exponent alpha
over ranks 2 to 30. We compared alpha with the anatomical hierarchy score of Harris et al. (2019), which
comes from the laminar patterns of tracer-defined connections.

Main result: alpha increased along the anatomical hierarchy. In Neuropixels pseudo-populations of 300 units,
alpha was 0.67 in LGd, 0.81 in VISp and 0.96 in VISam. The Spearman correlation with the hierarchy score
was 0.88 over 8 structures (p = 0.004). The slope was 0.27 alpha units per hierarchy unit, with a 95% mouse
bootstrap interval of 0.15 to 0.34. For the 6 cortical areas only, the slope was 0.20 (0.08 to 0.29).
The two-photon data gave the same direction: alpha was 0.61 in VISp and 1.11 in VISam, slope 0.55
(0.31 to 0.78). Inside 12 Cre-line and depth strata the slope was 0.54 (0.38 to 0.69), and all 9 strata
with at least 4 areas had a positive rank correlation.

Thus higher areas put more of their reliable image-driven variance into the first few dimensions. Their
codes for these images are lower-dimensional and smoother. The trend stayed after we matched unit
reliability, inside fixed reliability bands, after a simulation-based correction of estimator bias, in a
later response window, and inside cortical layers. The evidence is weaker inside single mice in cortex
(see Limitations).

## Question

Connectivity defines a hierarchy of mouse visual areas (Harris et al. 2019). Does the geometry of the
population code for natural images change along this structural hierarchy? Stringer et al. (2019)
found a power-law spectrum with alpha near 1 in mouse V1. They argued that alpha sets a balance between
expressive (flat) and smooth (steep) codes. We asked whether alpha changes in a regular way from thalamus
(LGd) through V1 to higher cortical areas, and whether the result repeats across animals, recording
methods, cell classes and cortical layers.

## Data

- Allen Visual Coding Neuropixels, all 32 `brain_observatory_1.1` sessions (one mouse per session).
  Units: Allen quality filters (ISI violations < 0.5, amplitude cutoff < 0.1, presence ratio > 0.9) in
  LGd, LP, VISp, VISl, VISrl, VISal, VISpm and VISam. Unit counts per structure: 950 to 2,230, from 20 to
  32 mice. Response: spike count 0 to 250 ms after image onset. Each image had 50 repeats.
- Allen Visual Coding two-photon, three_session_B experiments in containers that were not marked as failed,
  excitatory Cre lines only (Cux2, Slc17a7, Emx1, Rorb, Nr5a1, Rbp4, Ntsr1, Fezf2, Scnn1a, Tlx3):
  336 experiments, 193 mice. Response: mean dF/F from 2-photon frame 1 to frame 14 after onset
  (about 33 to 500 ms). Each experiment is one mouse and one area.
- Allen CCF 2017 annotation (10 um), used to give a cortical layer to each Neuropixels unit from its channel
  coordinates.
- Hierarchy scores (Harris et al. 2019, as used by Siegle et al. 2021): LGd -0.515, VISp -0.357,
  VISl -0.093, VISrl -0.059, LP 0.105, VISal 0.152, VISpm 0.327, VISam 0.441.

The Allen files are not in this bundle (see `files/NOTICE_EXTERNAL_DATA.md`). The exact session and
experiment identifiers, file URLs, byte counts, S3 ETags and SHA-256 hashes are in `files/provenance/`.
We streamed only the needed parts of each NWB file with HTTP range reads.

## Method

1. We scaled each unit by its single-trial standard deviation.
2. For each image, we split the 50 repeats at random into two halves of 25 and averaged each half.
3. cvPCA: we found principal components of half A (118 images by N units) and projected both halves on
   them. The covariance of the two projections gives the reliable variance of each dimension. We used both
   split directions and averaged over 4 or more splits.
4. We fitted alpha as minus the slope of log variance on log rank over ranks 2 to 30. We fixed this range
   before any area comparison, from a spectrum of all areas pooled together. We also report ranks 1 to 10,
   2 to 20 and 5 to 50, and the fraction of reliable variance in the first 5 dimensions ("top-5").
5. Pooled analysis: for each structure we combined units from all mice into one pseudo-population. This is
   valid for cvPCA because all mice saw the same images. We drew 300 units 50 times. For intervals we
   resampled mice with replacement (200 replicates; the same mouse sample for all areas in one replicate).
6. Within-mouse analysis: for each mouse and structure with at least 30 units we averaged spectra over 20
   draws of 30 units (ranks 2 to 15). A second version used only units with split-half image-tuning
   correlation r >= 0.6 (20 units, ranks 2 to 12). We fitted linear mixed models with a random intercept
   per mouse.
7. Controls for signal-to-noise ratio (SNR):
   (a) reliability matching: the same distribution of unit reliability in every structure;
   (b) fixed reliability bands (r < 0.3, 0.3 to 0.6, 0.6 to 0.8, r >= 0.8), 120 units each;
   (c) simulation: synthetic populations with a known power-law spectrum and the measured noise level of each
       structure, analyzed with the same pipeline, then used to correct the observed alpha.
8. Other controls: a 50 to 250 ms window; layer strata (L2/3, L4, L5, L6 from CCF; 50 units per area and
   layer; model alpha ~ hierarchy + layer); two-photon Cre-line and depth strata (100 cells per stratum and
   area; mixed model with a random intercept per stratum); two-photon reliability bands.
9. Exploratory: running (> 5 cm/s) versus stationary (< 1 cm/s) repeats, 8 repeats per image per state,
   in the 6 to 10 sessions with enough repeats of both states.

## Results

Figure 1 (`files/figures/fig1_spectra_alpha_hierarchy.png`): (a) spectra; (b) alpha against hierarchy for both
datasets; (c) alpha inside unit-reliability bands. Figure 2 (`files/figures/fig2_robustness.png`): (a) hierarchy
slope in all analyses; (b) the simulation calibration; (c) alpha inside cortical layers.

### Pooled Neuropixels populations (300 units per structure)

| Structure | Hierarchy | alpha (ranks 2-30) | 95% mouse bootstrap | top-5 fraction | alpha (ranks 1-10) | alpha (ranks 5-50) |
| --- | --- | --- | --- | --- | --- | --- |
| LGd | -0.515 | 0.672 | 0.647-0.829 | 0.259 | 0.434 | 0.902 |
| VISp | -0.357 | 0.813 | 0.774-0.907 | 0.347 | 0.681 | 1.042 |
| VISl | -0.093 | 0.786 | 0.763-0.908 | 0.327 | 0.603 | 1.067 |
| VISrl | -0.059 | 0.906 | 0.860-1.032 | 0.367 | 0.649 | 1.196 |
| LP | 0.105 | 0.903 | 0.835-1.046 | 0.375 | 0.698 | 1.152 |
| VISal | 0.152 | 0.899 | 0.841-1.005 | 0.358 | 0.613 | 1.194 |
| VISpm | 0.327 | 0.932 | 0.878-1.085 | 0.392 | 0.731 | 1.200 |
| VISam | 0.441 | 0.962 | 0.907-1.048 | 0.375 | 0.636 | 1.225 |

- Spearman rho with hierarchy: 0.88 (8 structures, p = 0.004); 0.89 (6 cortical areas, p = 0.019).
- Top-5 fraction: rho 0.81 (p = 0.015); bootstrap slope 0.053 to 0.131.
- Mean of five higher cortical areas minus VISp: +0.095 (0.015 to 0.158). VISp minus LGd: +0.107
  (-0.000 to 0.224). LP minus VISp: +0.087 (-0.052 to 0.226).
- Fit range: ranks 2-20 and 5-50 gave the same order (rho 0.90 and 0.93). Ranks 1-10 gave no clear cortical
  trend (rho 0.09 over 6 cortical areas). Thus the cortical difference is mainly in ranks above about 5.

### Controls

| Analysis | Hierarchy slope of alpha | Note |
| --- | --- | --- |
| Pooled, 8 structures | 0.27 (0.15 to 0.34) | mouse bootstrap |
| Pooled, 6 cortical areas | 0.20 (0.08 to 0.29) | mouse bootstrap |
| Reliability-matched units | 0.23 | rho 0.88; LP alpha fell from 0.90 to 0.82 |
| Simulation-corrected alpha | 0.23 | bias at true alpha 1 was -0.08 to -0.10 in every structure |
| 50-250 ms window | 0.26 | rho 0.95 |
| Layer-adjusted, 6 cortical areas | 0.39 (0.19 to 0.54) | session bootstrap; L6 alpha +0.37 versus L2/3 |
| Within mouse, 30 units, 8 structures | 0.14 (0.06 to 0.22) | 21 of 28 mice positive rho |
| Same, with reliability and rate covariates | 0.03 (-0.05 to 0.10) | covariates are collinear with hierarchy |
| Within mouse, 20 reliable units, 8 structures | 0.075 (0.014 to 0.135) | 16 of 22 mice positive |
| Within mouse, 20 reliable units, cortex | 0.024 (-0.041 to 0.089) | 12 of 18 mice positive |
| Two-photon pooled, 6 areas | 0.55 (0.31 to 0.78) | mouse bootstrap within area |
| Two-photon Cre-line x depth strata | 0.54 (0.38 to 0.69) | 12 strata, mixed model |

In the highest Neuropixels reliability band (r >= 0.8), alpha was 0.68 in LGd, 0.86 in VISp, 0.93 in VISal,
0.98 in VISpm and 1.01 in VISam. Inside each layer, alpha in VISpm and VISam was higher than in VISp
(for example L2/3: 0.85 in VISp, 1.10 in VISam; L5: 0.96 and 1.09). In two-photon reliability bands the
slopes were 0.23 (r 0.2-0.5), 0.22 (r 0.5-0.75) and 0.60 (r >= 0.75, 5 areas).

The simulation showed that alpha estimates from 118 images are biased low (about -0.09 at a true alpha of 1)
and that this bias is almost the same for all structures (Figure 2b). Most of the bias comes from the finite
image set, not from trial noise. The correction therefore does not remove the area differences.

Exploratory running test: in VISal, VISam, VISpm and VISrl, alpha was 0.08 to 0.19 higher in running repeats
than in stationary repeats. In LGd, LP, VISp and VISl the difference was below 0.02. Only 6 to 10 mice had
enough repeats, and we did not calculate intervals. We do not make a claim from this test.

## Interpretation

Along the connectivity-defined hierarchy, the reliable responses to natural images become concentrated in
fewer dimensions. This agrees with a gradual pooling of features in higher areas, which makes the code
smoother over images. The result connects a structural property (hierarchical position from tracer
connectivity) with a property of the population code. The test is correlational and at the level of areas.

## Limitations

- Only 118 images. Absolute alpha values are biased and are not comparable with the 2,800-image values of
  Stringer et al. (2019). The spectra are curved on log-log axes, so alpha depends on the fit range. We
  report several ranges; the area order held for ranks 2-20, 2-30 and 5-50 but not for ranks 1-10 in cortex.
- Area-level tests use only 8 (or 6) structures. The hierarchy score is one summary of connectivity.
  Other area properties that change along the hierarchy (receptive-field size, receptive-field position on
  the screen, response latency, firing rate) can also explain the result. We did not control
  receptive-field size or position.
- Pooled populations combine units from different mice. Within single mice in cortex the effect was not clear
  with 20 to 30 units. Small populations resolve only the first 12 to 15 ranks, where the pooled data also
  showed no clear cortical trend. In small populations, alpha also depended strongly on unit reliability.
- The SNR simulation uses Gaussian noise and a pure power-law signal. Real spike noise is not Gaussian.
- 14% to 38% of cortical Neuropixels units had no CCF coordinates and were not in the layer test. CCF layer
  labels can be wrong near borders.
- In two-photon data VISrl was unusual: one dimension held 80% of the reliable variance (top-5 0.80),
  with a wide interval. We kept it in all tests.
- Two-photon dF/F at 500 ms includes part of the response to the next image. The two methods give different
  absolute alpha values; we compare only the direction and the area order.

## Reproduction

Run `bash files/code/reproduce.sh SCRATCH_DIR OUT_DIR` with Python 3.12 and the packages in
`files/code/requirements.txt`. The script downloads metadata and streams the NWB files into SCRATCH_DIR
(about 15 GB of HTTP reads), then writes all CSV/JSON results and both figures into OUT_DIR. Random seeds are
fixed in each script. The run took about 2 hours on 6 cores of a shared machine. Allen may change hosted
files; compare against `files/provenance/source_files.tsv` and the ETag lists.

Main bundled results: `files/results/vcn/stats_vcn.json`, `summary_pooled.csv`, `layer_stats.json`,
`mouse_hr_stats.json`, and `files/results/ophys/stats_ophys.json`, `summary_ophys_pooled.csv`,
`ophys_reltier_stats.json`. `spectra.npz` files hold the cvPCA spectra of every draw.

## Provenance

- Campaign 11_07_2026; job sci-1107-hp-neural-structure-and-computation-d022231fb507; topic
  neural-structure-and-computation; machine hp; account claude-andrii; model Claude Opus 5.5
  (claude-opus-5-5). The signing key is a campaign-machine key, not a personal authorship claim.
- Shared campaign datasets used in place: `allen-vcn-ecephys-channels-20261109` (channels.csv, SHA-256
  d2932f1e...caed98) and `allen-ccf2017-annotation10-20261109` (annotation_10.nrrd, SHA-256 a9e9654e...ef24c).
- Related campaign work: regions farther from the retina had less reliable visual responses; hierarchy did not
  predict spontaneous timescales after laminar sampling was considered. We used both results to design the
  reliability and layer controls.

## References

- Stringer, C., Pachitariu, M., Steinmetz, N., Carandini, M., Harris, K.D. (2019) High-dimensional geometry of
  population responses in visual cortex. Nature 571, 361-365. doi:10.1038/s41586-019-1346-5.
- Harris, J.A. et al. (2019) Hierarchical organization of cortical and thalamic connectivity. Nature 575,
  195-202. doi:10.1038/s41586-019-1716-z.
- Siegle, J.H. et al. (2021) Survey of spiking in the mouse visual system reveals functional hierarchy.
  Nature 592, 86-92. doi:10.1038/s41586-020-03171-x.
- de Vries, S.E.J. et al. (2020) A large-scale standardized physiological survey reveals functional
  organization of the mouse visual cortex. Nature Neuroscience 23, 138-151. doi:10.1038/s41593-019-0550-9.
- Wang, Q. et al. (2020) The Allen Mouse Brain Common Coordinate Framework: a 3D reference atlas. Cell 181, 936-953.
  doi:10.1016/j.cell.2020.04.007.
- Pospisil, D.A., Pillow, J.W. (2024) Revisiting the high-dimensional geometry of population responses in
  visual cortex. bioRxiv. doi:10.1101/2024.02.16.580726.
