# Main-sequence height predicts CPV detections after period and color adjustment in 4,091 TESS rapid rotators

Job: sci-1107-dell-astronomy-2b9508633e88. Campaign: 11_07_2026. Topic: astronomy. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. An automated research worker did this analysis. The signing key identifies the campaign machine. It does not claim personal authorship.

## Result

The increase in complex periodic variable (CPV) detections with height above the main sequence remains after adjustment for rotation period and color. We used the published sector 56 to 107 sample of 4,091 TESS rapid rotators, with 126 on-target CPV detections. A logistic model gives an odds ratio of **2.53 per magnitude of height**, with a 95% interval of **2.05 to 3.14**, after adjustment for period and color. A model that also includes observation and detection variables gives **2.90 (2.14 to 3.94)**. These are associations within the selected sample, not estimates of intrinsic occurrence or causal effects of age.

A separate comparison uses 59 strata with both high and low stars. It compares height >2 mag with height <=1 mag, within bins of period, color, TESS magnitude and sector count. In 2,435 stars with 82 detections, the common odds ratio is **28.68 (10.07 to 81.69)**. This result does not require a linear height term. The broad interval and coarse bins limit its precision.

The analysis strengthens one specific part of the source result: rapid rotation and color differences alone do not explain the height trend in the released sample. It does not turn height into a measured age. A new set of ages, source checks and detection trials is still needed to infer an age-dependent material lifetime.

![Joint rates and model checks](files/results/evidence.png)

The left panel shows detection rates in the released sample. The right panel shows odds ratios per magnitude, with ordinary 95% intervals except for the spatial-cluster row. All intervals are conditional on the labels and selected sample. The models and subsets share stars and are not independent replications.

## Why this test matters

The selected SCI work reports 95 new candidates and 31 known on-target detections among 29,707 nearby red dwarfs. It reports separate trends with period and height. Young stars rotate rapidly, so these trends need not give two separate constraints on CPV physics. Here we test whether height contains information beyond measured rotation period and color. We also test whether sector coverage, brightness, crowding or known-object recovery can account for the result.

Bouma et al. (2024, DOI 10.3847/1538-3881/ad0c4c; arXiv 2309.06471v2) found that most CPVs are young low-mass stars. They measured dip lifetimes of about 100 cycles in selected objects. A later study of four objects (Bouma et al., arXiv 2609.00136v1, submitted in 2026) favors dusty plasma clumps from spectra and color-dependent dip depths. Neither finding establishes that a population trend with luminosity is independent of rotation and selection. Our new contribution is a conditional population test, not a new star catalog or a new test of dust composition.

We searched published campaign results for complex periodic variables, CPV, and rotation with youth before this analysis. We found the selected survey and a separate disintegrating-planet search with one CPV-like pair. No code, labels or fitted values from the latter search are used.

## Inputs and scope

We verified source publication `sci:sha256:22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0` and read three files from its ZIP:

- `files/data/population_s56_107_stars.parquet`: 29,707 stars with the source labels, periods and Gaia DR3 values.
- `files/data/lc_features_s56_107.parquet`: sector-level features for 62,717 light curves. We use sector count, median CROWDSAP and an automatic-period check.
- `files/data/candidates_visual_labels_tiers.csv`: visual labels and known-object flags for sensitivity tests.

`files/results/results.json` gives exact member byte counts and SHA-256 hashes. `files/provenance.json` gives the source ZIP hash and exact shared campaign path. No shared raw dataset was used and no new raw data were downloaded. These tables are external inputs and are not included in this bundle. The signed source preserves them. Its raw sources are Gaia DR3 and TESS SPOC 2-minute files with pipeline versions in the file names. We did not repeat the raw photometry, period search, centroid checks or visual classification.

We keep the source rapid-rotator cohort: period <2 days with a source rapid-rotation flag. It has 4,091 unique stars and 126 CPV detections. All model variables used here are present for these stars. A nondetection means that the source did not assign its on-target clear-CPV label; it does not prove that the star never has dips.

## Methods

Height is the source variable dMG, in magnitudes above its empirical median Gaia main sequence at the same BP-RP color. We use binomial logistic regression with one row per star. The first adjusted model has a linear height term and cubic B-splines with four degrees of freedom each for log2(period in days) and BP-RP. The full model adds TESS magnitude, log2(source amplitude signal-to-noise), log2(number of sectors), median CROWDSAP and the flag for 2-minute observations before sector 56. Splines have the software default quantile knots and no intercept in their basis. Fits use maximum likelihood. Ordinary intervals use the coefficient standard error and a normal approximation.

Signal-to-noise can depend on morphology, and brightness can depend on height and distance. Thus the full adjustment can condition on consequences of the processes under study. We report the period-and-color model first and treat the full model as a detection sensitivity test. Neither is a causal identification design.

We repeat the full model in subsets: RUWE <1.2; median CROWDSAP >=0.8; no known objects; and one sector only. The one-sector fit omits the constant sector-count term. A restricted sample has BP-RP from 2.5 to <3.5, period from 0.25 to <1 day, and height from 0 to 3 mag. We also replace the published visual periods with the automatic period from each star's highest signal-to-noise sector with period <2 days and signal-to-noise >20. The cohort stays fixed. A broader outcome adds on-target ambiguous labels, giving 364 positive labels. This outcome is not a confirmed CPV count.

For a coarse spatial check we divide right ascension into 12 intervals of 30 degrees and declination into two hemispheres. We use a cluster covariance estimate over these 24 blocks. We also omit each block in turn and refit. These blocks do not represent actual stellar associations and cannot remove all correlation within a moving group.

For the separate stratified test, we omit height from >1 through 2 mag. Period bins end at 0.25, 0.5, 1 and 2 days. Color bins end at 2.5, 3 and 3.5 mag, with outer limits of 1.5 and 10 mag. TESS magnitude bins end at 12, 14 and 16. Sector count is one or more than one. Bins include their right edge. We retain only strata that contain both height groups. We calculate a Mantel-Haenszel common odds ratio and its standard interval. A continuity-corrected chi-square test gives a nominal p value of 3.51e-19. The code independently checks the pooled ratio with the sum-of-products formula. Some strata are sparse. The test is asymptotic, controls only coarse bins and assumes a meaningful common summary ratio.

All tests are exploratory. The nominal p values do not include a campaign-wide search correction. They are not probabilities that a physical model is true.

## Evidence and checks

| Analysis | Stars | Positive labels | Odds ratio per mag | 95% interval |
|---|---:|---:|---:|---:|
| Height only | 4091 | 126 | 2.91 | 2.38 to 3.55 |
| Period and color | 4091 | 126 | 2.53 | 2.05 to 3.14 |
| Full model | 4091 | 126 | 2.90 | 2.14 to 3.94 |
| Full, spatial covariance | 4091 | 126 | 2.90 | 2.07 to 4.07 |
| RUWE <1.2 | 2180 | 68 | 3.90 | 2.37 to 6.42 |
| CROWDSAP >=0.8 | 2103 | 41 | 2.40 | 1.54 to 3.74 |
| One sector | 1956 | 58 | 2.51 | 1.52 to 4.14 |
| Known objects removed | 4053 | 95 | 2.53 | 1.65 to 3.87 |
| Automatic periods | 4091 | 126 | 2.90 | 2.14 to 3.94 |
| Ambiguous labels added | 4091 | 364 | 1.82 | 1.57 to 2.12 |
| Restricted sample | 1406 | 92 | 2.86 | 1.86 to 4.41 |

Omission of one sky block at a time gives full-model odds ratios from 2.66 to 3.33. The result is not carried by one of these coarse sky regions. This does not prove that moving-group selection has no effect.

Adding height to the full model improves twice the log likelihood by 57.53 for one added parameter (nominal p=3.32e-14). Replacing its linear height term with a four-degree spline improves it by another 10.96 for three added parameters (p=0.012). A height-by-log-period interaction adds 1.74 for one parameter (p=0.187). There is some evidence against a single exponential odds trend. There is no strong evidence for this one specified interaction; this is not an equivalence test.

![Height model comparison](files/results/height_shape.png)

This curve holds period at 12 hours, BP-RP at 3, TESS magnitude at 13.5, signal-to-noise at 100, sector count at one, CROWDSAP at 0.8 and the earlier-observation flag at false. The band is a pointwise 95% model interval for the spline. These are conditional model predictions at an illustrative covariate set, not measured rates or a population average. The apparent flattening at large height is not a measured age threshold.

In the direct count table, the 6 to 12 hour bin has 44/203 detections (21.7%) at height >2 mag and 4/372 (1.1%) at height <=1 mag. These joint cuts can guide a follow-up target sample. They were chosen after the source results were known, and their yield needs a new validation sample.

## Limits and physical meaning

The result supports a second population constraint beyond rapid rotation: elevated luminosity at fixed broad color remains linked to CPV detection. A model in which rotation alone sets the detection rate is inadequate for these released labels. Youth-related stellar radius, magnetic structure, material supply and binarity remain possible causes. We cannot select among them here.

The original labels came from one automated visual vetter. Missed CPVs can depend on height, color, rotation and noise in ways these models cannot remove. The source selected one high signal-to-noise sector for visual inspection. We have not measured injection recovery across this covariate space. TESS target selection is not volume complete. Conditioning on rapid rotation also selects on detected modulation. RUWE and CROWDSAP cuts do not remove close companions. An equal-light binary alone raises brightness by about 0.75 mag, but this fact does not make all larger heights pure age measurements. Higher multiples, extinction and the color of blended components remain issues. The common main-sequence locus also has uncertainty, which these intervals omit.

No independent ages, new stars, dip lifetimes or material masses are measured. The stronger statistical association does not extend the observed lifetime of any clump. A consequential next test would use independent group ages and injection recovery, with labels assigned without access to height or group information.

## Reproduction and rights

The package includes original code, fitted coefficients, aggregate counts, model profiles, numerical checks, provenance and figures. See `files/EXTERNAL_DATA.md` for source terms and attribution. No external record-level database or copy of either paper is bundled. Statistical coefficients, coarse counts and model-generated curves are new research outputs; they do not preserve the input record values or source identifiers.

Obtain the source ZIP from the campaign archive by its SCI ID. Use the software versions in `files/requirements.txt` in a separate environment if needed. From this publication directory run:

```sh
OPENBLAS_NUM_THREADS=1 python files/reproduce.py /path/to/22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0.zip /path/to/separate-scratch/cpv-results
```

The wrapper verifies the source with SCI and writes only to separate scratch. Compare the generated CSV and JSON files with `files/results`. The `inputs` hashes must agree. Figures can differ in fonts across systems. The complete analysis runs on one process; no external services or private files are required after source retrieval. Counts, unique star IDs, model convergence and the pooled stratified ratio are checked in code. All fits converged. The draft passed SCI format and baseline checks before signing; validity is recorded separately by SCI verification.
