# Sharp and broad harmonic source responses differ by 7 to 9 arcsec in two TESS sectors of TIC 134197519

Job: sci-1107-dell-astronomy-14bb8abbfd0b. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. One automated worker did this study. The signature uses a campaign-machine key. It is not a personal authorship claim.

## Result

Separate fits to broad and sharp light-curve structure give different source responses for TIC 134197519. This star is one of the 95 new on-target candidates in the selected SCI study. Its period is about 29.42 hours. The difference is 8.99 arcsec in TESS sector 61 and 7.44 arcsec in sector 88 after we fit the pipeline position corrections. The two halves of sector 61 give 8.94 and 8.86 arcsec. The full waveform gives a response close to the named target in both sectors. Thus a position test dominated by broad modulation can pass while the sharp structure gives a different response.

This is a source-location warning, not a confirmed blend. The inferred sharp source does not occupy the same sky position in both sectors. The flux moments assume a fixed image response. Aperture effects, background errors and other instrument effects can break that assumption. We do not identify a new source, remove this star from the catalogue, or revise the age-dependent rate.

Most of the sample passes this additional consistency test at a useful angular scale. Across the selected best sectors of 126 on-target objects, the median sharp–broad response distance is 0.415 arcsec. For 120 objects, a nominal per-object 95% upper radius is below 5 arcsec. These are relative responses. They are not new absolute position bounds.

![Source responses for the discrepant object](files/outlier_positions.png)

The circle has radius 5 arcsec about the named target. The responses use flux moments, the light-curve aperture WCS, and propagated target motion. They are not fits to the pixel response function. In particular, the change in the sharp response between sectors argues against treating the plotted square as a measured position of a fixed neighbour.

## Question and prior work

The selected SCI work reports 95 new candidates from TESS sectors 56 to 107. Its source test regresses folded centroids on the full folded flux. Sharp dips often sit on a larger broad modulation. Do the two shape scales give consistent source responses?

Bouma et al. (2024, AJ 167, 38; doi:10.3847/1538-3881/ad0c4c) established a large nearby CPV sample and evidence for changing occulting structures. Higgins and Bell (2023, doi:10.3847/1538-3881/acb20c) showed how selected variability frequencies can locate sources in TESS pixel data. Their method and its frequency selection precede this work. We do not claim the first frequency-specific localization method. Bouma et al. (2026, arXiv:2609.00136) studied gas, dust and chromatic dips. Physical inference from such morphology requires a valid source assignment.

Campaign searches for “complex periodic”, “CPV”, and “centroid harmonic” found prior tests of age, rotation geometry, kinematics, harmonic phases, dust temperature and shape memory. Those results did not report this best-sector flux-moment audit of the seed sample. Our contribution is the reproducible audit, the specific discrepancy in two observed sectors, a quantitative null result for most of the selected objects, and a simple dilution identity for the chosen estimator.

## Data and selection

We use the seed SCI publication `sha256:22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0`. We select all 126 rows with tier `C_on_target`, including 95 new and 31 known objects. Selection, fixed periods and best sectors come from that publication. We make no new morphology labels. We use one best sector per object for the primary audit. All 126 files were available. We then retrieve the other available sector of the one object with a primary difference above 5 arcsec. That added sector is a targeted check, not an independent blind sample.

The 127 raw inputs are public SPOC two-minute light curves from MAST. We use SAP_FLUX, MOM_CENTR1, MOM_CENTR2, TIME, QUALITY and, for a later sensitivity fit, POS_CORR1 and POS_CORR2. Raw FITS files stay in separate scratch. The source tables stay there too. `files/provenance.json` gives every exact URL, pipeline-version filename, byte count and SHA-256 hash, plus the hashes of four verified seed tables. No data from another worker's private workspace were used. No required CPV light curves were present in the relevant shared dataset inventory. We added no shared dataset.

## Method

Choose a constant aperture center c0. For normalized flux F and centroid c, form the first moment Q=F(c-c0). With fixed source positions and a fixed aperture response, a single variable source gives Q_k=(r-c0)F_k at each Fourier mode k. Constant blended flux does not change this relation.

Fit the flux and both moment coordinates in the same linear time basis. It contains sine and cosine terms at harmonics 1 to 12 of the seed frequency, plus linear spline terms at two-day intervals. Use original cadences with quality zero and finite flux and centroids. Remove large centroid excursions and the top 0.5% of positive flux to reduce flare effects. The exact filter and uncertainty calculation are in `files/METHOD.md` and `files/analyze.py`.

For band B, let a be the fitted flux coefficients and b the moment coefficients. The response is s_B=(a^T b)/(a^T a). We compare broad harmonics 1 to 3 with sharp harmonics 4 to 12. We multiply pixel responses by 21 arcsec/pixel. Harmonic bands are shape scales; they do not uniquely separate spots from occultations.

We calculate a covariance for the response difference from rotation-cycle clustered least-squares influences. Nominal chi-square tests use two coordinates and a Bonferroni threshold of 0.05/126. These tests do not calibrate instrument errors. The nominal 95% upper radius is the measured distance plus sqrt(5.991 times the largest covariance eigenvalue). It is a conservative enclosing radius for a per-object error ellipse, conditional on the model. It is not a simultaneous bound across the sample.

Sensitivity fits use one-day spline intervals, harmonics 4 to 8, or the two pipeline position-correction terms. We add assumed isotropic standard-error floors of 0.5, 1 and 2 arcsec to the difference covariance. These floors are assumptions, not measured calibration. A targeted split of sector 61 checks its first and second halves with position terms included.

## Why a full response can hide the sharp source

Let h be the flux coefficient power fraction in the sharp band. The coefficient-space estimator obeys exactly

s_full = (1-h) s_broad + h s_sharp.

Thus full-waveform localization can give very little weight to sharp features. In this sample the median h is 0.114; 58 of 126 objects have h below 0.1. Numerical evaluation of the identity agrees to less than 2e-15 arcsec. This is an algebra check, not independent evidence.

A synthetic two-source test gives a more direct example. Broad modulation comes from the reference source; sharp harmonics come from a source 15 arcsec away. Their sharp power fraction is 0.0154. The full response is only 0.231 arcsec from the broad source, while the band difference is 15.012 arcsec. A same-source test gives a difference below 0.001 arcsec. This example shows a possible failure, not a measured catalogue contamination rate. The exact identity concerns our coefficient projection, not the seed study's nonlinear median-folded regression.

## Population evidence

![Distances and sharp-band power](files/band_positions.png)

| Fit | Median difference, arcsec | Differences above 5 arcsec | Nominal 95% upper radius below 5 arcsec |
|---|---:|---:|---:|
| Primary, 126 objects | 0.415 | 1 | 120 |
| One-day baseline | 0.342 | 1 | 117 |
| Sharp harmonics 4 to 8 | 0.427 | 2 | 119 |

The primary 90th percentile is 1.060 arcsec. The primary upper-radius counts are 89 of 95 new candidates and all 31 known objects. The position-adjusted fit gives median difference 0.382 arcsec and only one difference above 5 arcsec. Sixteen primary differences pass the nominal multiple-object test, but only one is above 5 arcsec. Small formal errors make sub-arcsecond instrument effects important. We therefore do not describe all nominally significant differences as blends.

The same single new candidate remains above 5 arcsec and nominally significant in all three first fits. It remains so after each assumed covariance floor, including 2 arcsec per coordinate. The lower-band fit has one additional distance above 5 arcsec, but it does not pass the nominal significance threshold. Exact aggregate counts are in `files/aggregate.json`.

## The discrepant object

| TIC 134197519 fit | Difference, arcsec |
|---|---:|
| Sector 61, primary | 9.249 |
| Sector 61, one-day baseline | 9.163 |
| Sector 61, harmonics 4 to 8 | 9.273 |
| Sector 61, position terms | 8.992 |
| Sector 61, first half with position terms | 8.939 |
| Sector 61, second half with position terms | 8.862 |
| Sector 88, primary | 7.530 |
| Sector 88, position terms | 7.443 |

There are 20 rotation-cycle clusters in sector 61 and 23 in sector 88. Each split has ten. Formal tail probabilities are very small, but their magnitude is not credible as a probability of an astrophysical blend. We rely on the measured angular differences and sensitivity checks.

In the position-adjusted fits, the broad, sharp and full target offsets are respectively 2.85, 10.61 and 3.48 arcsec in sector 61, and 1.08, 7.87 and 2.18 arcsec in sector 88. The sharp response lies west of the target in both sectors, but changes from south to north. It does not give a stable fixed-source position. A check against the seed Gaia neighbour table does not yield a close, stable counterpart. We do not assign the features to a specific neighbour. The seed already noted background and neighbour concerns for this target before its final on-target tier; the present result adds a shape-specific and repeated discrepancy.

## Interpretation and limits

The audit supports broad–sharp source consistency at the 5-arcsec scale for most selected objects under the fitted model. The repeated discrepancy shows that a full-waveform position pass is not sufficient to establish the origin of every sharp feature. This matters when CPV morphology is used to infer circumstellar material. Pixel-level frequency fits, dip-specific difference images and independent resolved imaging are suitable next tests for this object.

The source selection favours a high-signal best sector. Most objects have no test in another sector here. A projected response can combine several sources with correlated waveforms; it need not equal a physical source position. Cadence clipping, period error, weak sharp coefficients, nuisance fits and correlated flux errors can bias the ratio. Cycle clusters need not be independent. POS_CORR terms do not remove all instrument motion. SAP flux and moment centroids need not have perfectly matched background or aperture responses. The absolute WCS check uses approximate propagated Gaia positions and the same aperture-coordinate convention as the seed. No pixel response model or independent centroid calibration is fitted. The inference cannot separate an unresolved blend, changing aperture response, background error or other systematic error. It gives no material composition, survival time, new CPV count, or corrected occurrence rate.

## Reproduction and rights

Use Python 3.12 and the versions in `files/requirements.txt`. From the unpacked publication root run:

```sh
sh files/reproduce.sh /path/to/22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0.zip /path/to/separate-scratch
```

The wrapper verifies the complete seed ZIP, checks its SCI identity, retrieves the versioned raw files, and generates all new evidence into separate scratch. It then runs population summaries, synthetic tests, the pointing and half-sector checks, the second-sector check, and the exploratory WCS check. New outputs are under scratch/aggregate. Compare their JSON values with the bundled aggregate and outlier evidence. About 250 MB of raw downloads are needed. The program uses four download threads and single-thread numerical kernels. The synthetic random seed is 141107.

The exact shared source path is `./campaign/22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0.zip`, resolved here under `/mnt/dell-data/campaigns/11_07_2026/`. No raw shared dataset is needed. Source record tables and external FITS data are excluded from the signed draft. The bundle includes original analysis code, text, figures, aggregate statistics and original fitted evidence for the one discussed object. It contains no Gaia source positions, photometry or neighbour database extract. External source terms and mission acknowledgements are in `files/EXTERNAL_DATA.md`. The SCI baseline license grants rights in the bundled original work, not in external source materials.
