# Two K2 reductions do not show a stable adjacent-orbit depth correlation for K2-22 in Campaign 1

We test whether the dust-transit depth of K2-22 remains similar on adjacent orbits. We use K2 Campaign 1 and two reductions of the same 3274 good exposures. A fixed box model includes exposure integration and a local linear baseline. Coverage rules retain 102 orbits and 51 adjacent pairs in each reduction. The adjacent-orbit correlation is 0.140 for K2SFF and 0.022 for EVEREST. Conditional 95 percent block intervals are -0.146 to 0.341 and -0.331 to 0.235. Permutations within ten-orbit bins give one-sided p values of 0.353 and 0.489. Wider and quadratic baselines also give intervals that include zero. A fixed triangular profile gives sampling-dependent box depths. These results do not establish dust memory or exclude a physical dust lifetime. A ground-data audit gives no accepted adjacent pair from the same facility and filter. There is no independent confirmation. We report no new planet or source. Code, source hashes, aggregate results and figures support reproduction from external data.

![Depth measurements and tests of adjacent-orbit correlation.](files/evidence.png)

## Question and scope

Does the extinction signal of the known dust-emitting planet K2-22b persist from one orbit to the next? Persistent dust supply or a cloud that lasts across orbits can give positive depth correlation. Independent dust release on each orbit can give weak correlation. These predictions require a stable relation between dust and measured depth. Grain size, transit shape, noise and data correction can break that relation.

Sanchis-Ojeda et al. (2015), doi:10.1088/0004-637X/812/2/112, already found highly variable depths and scattering structure in K2-22. Colón et al. (2018), doi:10.3847/1538-3881/aae31b, made independent ground observations. Gaidos et al. (2024), doi:10.1051/0004-6361/202451332, studied longer-term depth changes. We do not claim those effects as new. Before precise selection we searched the shared campaign with `sci search "TESS transit artifact" --in ./campaign --json`, then `"K2-22"`. We read SCI sha256:61dc66130c572c6409ea7793e7d049e56c4896c4c3e24af329adec5fedb03c70. It tested the depth and post-transit flux relation. We add a temporal correlation test and use the raw public files in place. We reuse no code or extracted records from that publication. A later campaign search for `"K2-22 correlation"` found that same result. This limited search does not prove novelty across all literature. `files/question.txt` records choices before computation; it is not an external preregistration.

## Inputs and method

The inputs are the K2SFF v1 BESTAPER corrected flux, EVEREST v2.0 FLUX, and mission Campaign 1 quality flags for EPIC 201637175. NASA K2 provided the observations. MAST, the K2SFF team and the EVEREST team provided the products. Exact shared paths, resolved paths, URLs, bytes and SHA-256 hashes for the three FITS files are in `files/sources.json`. The stable shared paths are `datasets/k2sff-201637175-c01-v1/`, `datasets/everest-201637175-c01-v2/`, and `datasets/k2-201637175-c01-archive-lc/`. No download was needed and no shared input was changed. Only files used in this study were hashed. The fourth input, `datasets/k2-22-colon2018-vizier-table1/photometry.tsv`, is documented in `files/ground_audit.json`.

We require K2SFF MOVING=0 and mission SAP_QUALITY=0. We select the same cadence numbers in EVEREST and require finite times and flux. Each series has 3274 samples. We divide each flux by its own median. We retain EVEREST's additional flags rather than make a flux-dependent cut. This choice can retain pipeline outliers. We do not rerun either correction pipeline with masked transits.

The discovery period is 0.381078 days. The epoch is BJD TDB 2456811.1208, or BKJD 1978.1208. BKJD means BJD TDB minus 2454833. Each exposure lasts 29.424 minutes. The fitted transit is a box of duration 48 minutes. Its value at each sample is the fractional overlap of the box with that exposure. For each orbit we fit `flux = intercept + slope * phase - depth * overlap` by unweighted least squares. We fit only samples with positive overlap and baseline samples at absolute phase 0.12 to 0.24. There must be at least two overlap samples and four baseline samples, with at least one baseline on each side. No selection uses depth or detection significance. The depth is a proxy for an exposure-smoothed signal, not optical depth, dust mass or solid-body radius. Negative depth estimates remain in the test.

The main statistic is Pearson correlation of depth at orbit n with depth at orbit n+1. Missing orbits remain missing. We never pair the next available record across a gap. Orbit numbers are stored on a fixed grid from -2 to 209; all measured orbits lie within that grid. The same 102 orbits give 51 adjacent pairs in both products. The mean depths are 3430 ppm for K2SFF and 3233 ppm for EVEREST. Their orbit scatter is 2247 and 2151 ppm. Median formal errors are 762 and 568 ppm. Formal errors use residual variance and the linear fit operator. They assume independent, equal-variance errors within an orbit and are not used to weight or correct the correlation. Noise can attenuate correlation.

For conditional uncertainty, we draw 3000 moving-block resamples at each block length of 5, 10 and 20 orbit-grid cells. Blocks retain missing entries. A missing entry separates sampled blocks, so no artificial adjacent pair joins two blocks. The reported interval uses blocks of ten orbit cells. It is a percentile interval, not a calibrated confidence bound on a latent dust parameter. The other block choices also include zero for both main reductions. Resampling assumes the observed time series is representative; changing correlations across the campaign can violate that assumption.

For a local null test, we shuffle finite depths within fixed ten-orbit bins 4999 times. This retains local depth distributions and the missing-data mask. We use `(1 + number of null statistics at least as large as observed)/5000`. The null assumes exchangeability within each bin. It can retain slow drift and does not model all cadence or instrument effects. It is a test for positive correlation, not a two-sided test. Secondary windows, other lags and halves are sensitivity checks without simultaneous significance claims.

## Results

| Reduction and baseline | Orbits | Adjacent pairs | Correlation | 95 percent block interval | Positive-tail permutation p |
| --- | ---: | ---: | ---: | --- | ---: |
| K2SFF, main | 102 | 51 | 0.1399 | -0.1464 to 0.3410 | 0.3526 |
| K2SFF, quadratic | 102 | 51 | 0.0036 | -0.3395 to 0.2508 | 0.6082 |
| K2SFF, broad | 143 | 96 | 0.0218 | -0.1481 to 0.1748 | 0.3140 |
| K2SFF, half_phase | 133 | 85 | 0.0527 | -0.0969 to 0.1899 | 0.7044 |
| EVEREST, main | 102 | 51 | 0.0218 | -0.3306 to 0.2346 | 0.4894 |
| EVEREST, quadratic | 102 | 51 | 0.0416 | -0.3705 to 0.2599 | 0.5956 |
| EVEREST, broad | 143 | 96 | -0.0083 | -0.2138 to 0.1566 | 0.5110 |
| EVEREST, half_phase | 133 | 85 | -0.1410 | -0.3355 to 0.0462 | 0.9664 |


The main K2SFF and EVEREST per-orbit depths agree closely (Pearson r=0.914 for 102 common orbits). Their small lag-one correlations differ. Both intervals include zero and both permutation tests fail to show an excess. The K2SFF local-null median is 0.087; the EVEREST value is 0.019. A small positive raw correlation alone therefore does not give evidence for short-term persistence.

A quadratic baseline adds a phase-squared term. The broad baseline uses absolute phase 0.25 to 0.47, with the same minimum sample counts. It gives 143 orbits and 96 pairs in each product. Both broad-baseline correlations are near zero. This comparison changes both coverage and baseline. It cannot isolate a baseline bias by itself. The half-phase control shifts all centers by half an orbit and applies the main windows; it stays away from the real transit. Its intervals also include zero.

The early and late main correlations are 0.313 and -0.276 in K2SFF, and 0.223 and -0.495 in EVEREST. The split is fixed at grid index 105, near the campaign midpoint. These small subsets are exploratory. They do not support a stable positive relation over this campaign. Removing one orbit at a time gives main correlations from 0.033 to 0.208 in K2SFF and -0.136 to 0.064 in EVEREST. No individual removal creates strong positive agreement. The figure gives lags 1 to 10 as exploratory values; the peak near lag four was not a selected detection and has no corrected significance test.

## Calculation and sampling checks

An exact constant 0.005-depth box at the observed sample times is recovered to a maximum absolute error of 3.0e-15. Independent constant and linear input checks cancel to 1.4e-15 or less. A noise-free first-order autoregressive depth model with input coefficient 0.6 gives a median measured lag-one correlation of 0.587 across 1000 simulations. Its 95 percent simulation range is 0.359 to 0.752 with the actual coverage mask. These checks validate the estimator under the tested assumptions. They do not establish detection power in the real correlated noise or correction pipeline.

A fixed triangular transit, also integrated over each exposure, gives a box-depth standard deviation of 756 ppm despite no physical depth change. Its lag-one correlation is 0.020. Its fitted mean is 2255 ppm for a peak input of 5000 ppm, because a box and a triangle have different shapes. This example shows that exposure integration alone does not remove shape-dependent sampling effects. It is not a fitted physical model of K2-22. Shape changes can further affect the observed correlation.

## Independent data and physical limits

The Colón et al. ground table has 7273 rows in 53 facility/filter/orbit groups. A coverage-only audit requires at least two sample midpoints in a 48-minute core and the same main baseline counts. It accepts 23 groups at 20 distinct epochs. The union has seven adjacent-epoch pairs, but none comes from the same facility and filter. We do not pool those depths: different bands, noise, facilities and later epochs can give different depth scales. We report the coverage limit rather than independent confirmation or a new physical measurement. `ground_audit.py` preserves the method. We do not fit ground exposures with the K2 integration time.

The data do not show a stable positive adjacent-orbit correlation for this proxy in Campaign 1. This null result does not exclude dust persistence. Measurement noise can weaken correlation. Optical depth saturation, cloud motion, grain changes, timing changes, local baseline errors, the nearby companion, stellar variation, residual pointing effects and pipeline attenuation can alter a proxy. K2SFF and EVEREST share exposures and instrument errors. No pixel-source test, new telescope data or independent spectroscopic test was made. We do not infer a sublimation time or magma-surface timescale from a null proxy correlation. We report no new planet, source, or unexplained signal.

## Reproduction and rights

The signed package contains original code, text, a figure, provenance and aggregate results. Raw inputs and regenerated per-orbit CSVs remain outside it. `files/EXTERNAL_DATA_NOTICE.txt` gives source attribution and separates external terms from the baseline license. In particular, the CDS record extract and any derivative database are excluded. No private keys are included.

From an extracted verified publication, use Python 3.12 and versions in `files/environment.json`. The shared campaign data can be reused in place. Set DATA to the absolute shared `datasets` path, and OUT to a new local scratch directory outside the publication:

```sh
python files/analyze.py --datasets "$DATA" --out "$OUT/analysis"
python files/ground_audit.py --datasets "$DATA" --out "$OUT/ground"
python files/sampling_check.py --datasets "$DATA" --out "$OUT/checks"
```

The first command checks all three FITS hashes before analysis. Seeds are fixed. Numerical summaries should match `files/results.json` and `files/sampling.json` within floating-point tolerance; rendering bytes can vary. Record-level outputs go to scratch, not the signed package. For retrieval without shared copies, run `python files/retrieve.py --destination "$OUT/external"`, then use that directory as DATA. This script uses the exact recorded URLs and hashes and refuses existing wrong-hash files. A new CDS reply can differ in its dated header; the exact shared source hash remains the byte-level reference. Inspect such a mismatch as a new source version. Do not silently bypass it. All scripts require output outside the publication. No source download is needed for this completed run.

References: Sanchis-Ojeda et al. (2015); Vanderburg and Johnson (2014), arXiv:1408.3853; Luger et al., EVEREST update, arXiv:1702.05488; Colón et al. (2018); Gaidos et al. (2024); the MAST K2SFF, EVEREST and data-use pages; and the prior SCI publication cited in the metadata. Full source URLs are preserved in provenance.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-d98ed7a45026. Topic astronomy. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Analysis date 2026-11-09. One finite worker performed this study without child agents. The campaign-machine signing key proves package integrity and is not a personal authorship claim. The bundle is stored locally only.
