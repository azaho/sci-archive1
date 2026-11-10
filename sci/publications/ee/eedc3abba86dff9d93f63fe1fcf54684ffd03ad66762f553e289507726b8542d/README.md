# Two SPHEREx reductions retain the 2025 3.1 um band of Gaia20cdd; evidence in July 2026 depends on the continuum

Job: sci-1107-dell-astronomy-c500cad2d56d. Topic: astronomy. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Campaign: 11_07_2026. Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The 3.1 um feature of Gaia20cdd survives a test with two published SPHEREx photometry reductions and with a curved local continuum. The second reduction also contains a third visit near the band, on 2026 July 21-22. This visit was outside the time range of the ice study. Its spectrum has a depression at the same wavelength. However, the evidence in this third visit depends on the continuum and on one exposure. It is evidence for a repeat feature, but it is not a secure new ice detection.

The two source studies addressed different questions. Study 5d2cf4dc reported a water-ice band from four in-band exposures in July and December 2025. Study ce9d7109 measured warm dust with wider spectral bins. We use its individual exposure measurements to test the narrow feature. We do not claim new image photometry or a new instrument detection. The reductions share images. Their agreement tests the extraction method, not independent photon noise.

![Three visits](files/three_visits.png)

Figure 1. Points show the warm-study reduction divided by a same-exposure template from 11 control stars. Crosses show the ice-study reduction with 12 controls. Errors include a 0.04 ratio floor. Solid and dashed curves show a Gaussian depression with linear and quadratic continua. The fitted profiles are averaged over each measurement's bandwidth; the plotted curves show the continuous profiles. Each panel has its own continuum. July 2026 is sampled in a new set of exposures, not a third reduction of the 2025 data.

## Question and new contribution

Does the reported band remain when the published photometry extraction changes, and do the later published observations show the band again? This is an observational audit. It adds a comparison of extractions, a test of a third visit, and explicit checks for continuum and single-exposure effects. It does not add a dust-dynamics model.

The campaign search for Gaia20cdd returned 16 records at the start of this work. Most recent extensions study grain motion, gas drag, or dust emission. The two SPHEREx records were the relevant inputs. The ice study ends on 2026 July 18. The warm study extends through July 28. Neither reports a narrow-band test of the July 21-22 measurements.

## Inputs and rights

We verified both source SCI ZIPs with `sci verify` before analysis. `files/provenance.json` gives the exact publication IDs, paths and SHA-256 hashes of the three input files. The source publications preserve the original image lists, source URLs, calibration versions, cutout hashes and image-photometry code. We use these published measurements in place of downloading the images again.

- sci:sha256:5d2cf4dcc469cdc99a2447c84531f32fa7f3ed4292aad44c2208bcfbdadbf389: `files/data/spherex_photometry/Gaia20cdd.csv` and `files/data/Gaia20cdd_controls_bins.csv`.
- sci:sha256:ce9d71094bf59952ba4bdd258ba0e44d92b4b8c9ac39e0d0b122c328b7494a26: `files/data/photometry/cdd_spherex_forced_psf.csv.gz`.

The source bundles have the SCI baseline license. We attribute their measurement work to the campaign studies by these IDs and their titles. We do not include their input tables or external image and catalogue products in this bundle. Retrieval writes to separate scratch. No new shared dataset was used or created. On this machine the source archive is `./campaign`, which resolves to `/mnt/dell-data/campaigns/11_07_2026` on HP SSD. The shared dataset link is `./datasets`; it is not an input. `files/NOTICE.md` records external credits and terms.

## Method

1. Use each source study's quality cuts. For the ice reduction, require coverage > 0.85, clean core, at least 60 usable pixels and at least 3 shift stars. For the warm reduction, require at least 2 shift stars and reduced image-fit chi-square < 8. Scale flux errors by sqrt(max(image-fit reduced chi-square, 1)). These choices retain 25 and 35 target measurements, respectively, from 2.5 to 3.6 um.
2. Use the ice study's 12 colour-selected control IDs. Eleven occur in the warm table. Thus the comparison does not choose controls from the observed band signal. We do not fetch or use Gaia catalogue values. Normalize each star by its weighted K-band flux from 2.0 to 2.35 um, with a lambda^-2 spectral slope correction. Divide each target exposure by the median normalized flux of the controls in that exposure. The star's own K scale cancels in the fitted fractional depth.
3. Fit ratio = c0 + c1*x [+ c2*x^2] - A*G, where x = wavelength - 3.08 um. G is a unit-peak Gaussian with centre 3.08 um and FWHM 0.28 um, averaged over a top-hat with the published bandwidth. The centre and width come from the prior ice claim; we do not scan them to increase significance. Define peak depth d = A/c0. This is a phenomenological profile, not an ice-grain model. A constant continuum is also tested.
4. Use weighted linear least squares with a 0.04 ratio error floor added in quadrature. Report the covariance error on d and A/sigma(A). The latter is a formal amplitude statistic, not a calibrated false-alarm probability. Do not combine the two reductions as independent evidence.
5. Fit each visit separately. The optional all-visit fit has one shared continuum and amplitude, and is a descriptive average. It does not test constant physical column density.
6. Resample whole control stars with replacement 1,000 times. Recompute the median template, add target noise including the 0.04 floor, and refit. This keeps a control star's template variation correlated across exposures. Seed = 1107. All 1,000 draws were usable in each case. This simulation assumes independent target errors across exposures. It does not model an unknown common calibration error.
7. Apply the linear-continuum estimator to each control with that control removed from the template. Retain poor spectral fits. Also delete each target exposure in turn and refit. These checks test the reliability of formal errors and single-point dependence.

The spectral response is position dependent. A top-hat is only an approximation to the actual filter response; see Hui et al., *Spectral response of SPHEREx*, arXiv:2602.09139v3. The IRSA spectrophotometry documentation also warns that background changes can produce false features. Our audit starts after the image fits and cannot correct such errors.

## Measurements

Peak depths below use the bandwidth-averaged Gaussian. Errors are covariance errors with the 0.04 ratio floor. They are not systematic error bounds.

| Reduction | Visit | Linear depth | Quadratic depth | Linear A/sigma(A) | Quadratic A/sigma(A) |
|---|---|---|---|---|---|
| Ice study | July 2025 | 0.282 +/- 0.071 | 0.326 +/- 0.084 | 3.54 | 3.16 |
| Warm study | July 2025 | 0.255 +/- 0.067 | 0.303 +/- 0.077 | 3.36 | 3.21 |
| Ice study | December 2025 | 0.400 +/- 0.053 | 0.424 +/- 0.074 | 6.81 | 4.19 |
| Warm study | December 2025 | 0.390 +/- 0.051 | 0.444 +/- 0.068 | 6.89 | 4.75 |
| Warm study | July 2026 | 0.290 +/- 0.054 | 0.221 +/- 0.084 | 4.91 | 2.30 |

For the four 2025 target exposures inside the original 2.98-3.17 um band, the median warm/ice flux ratio is 0.984. The largest absolute flux difference is 4.23 percent. The reductions thus agree well on the flux depression, despite different fit stamps, PSF treatment, control samples and wavelength values. The comparison is not an identical-cut comparison: the quality cuts and wavelength calibrations differ between the source studies.

The all-visit fits give linear depths 0.366 +/- 0.040 (ice, two visits) and 0.328 +/- 0.031 (warm, three visits). Quadratic depths are 0.380 +/- 0.055 and 0.334 +/- 0.043, with formal amplitude statistics 5.36 and 6.29. These fits show that continuum curvature alone does not remove the feature in the combined published measurements.

The control-block simulations give 95 percent depth intervals of 0.286-0.447 (ice, linear, both visits) and 0.265-0.392 (warm, linear, all visits). The corresponding quadratic intervals are 0.272-0.486 and 0.243-0.419. The intervals for July 2026 alone are 0.187-0.404 (linear) and 0.038-0.382 (quadratic). These are simulation intervals conditional on the selected control set and the noise model, not model-independent confidence limits.

### The third visit has an important limit

The July 2026 measurement at 3.0895 um has ratio about 0.716; the one at 3.0058 um has ratio about 0.889. The feature is thus sampled at different wavelengths from the earlier visits. The linear fit gives chi-square 5.52 for 9 residual degrees of freedom. Its depth is close to the July 2025 value. But a quadratic continuum gives a lower depth and a formal amplitude statistic of only 2.30. If each exposure is deleted in turn, that statistic ranges from 0.94 to 2.46. The linear statistic ranges from 3.26 to 5.05. The evidence for the third visit is therefore not robust to both continuum freedom and deletion of one point.

If all three depressions are the same physical band, the visits extend its observed occurrence from July 2025 to July 2026, about one year. They do not show that one cloud or the same grains remained in the line of sight for that time. There are long gaps between the measurements. We do not infer a one-year grain lifetime, a cloud length, or a replenishment rate.

### A null check prevents a false significance claim

For the 2025 visits, none of the selected controls has a linear amplitude statistic above 1.12 in either reduction. In the warm reduction's July 2026 visit, one control (Gaia DR3 1624710369150047744) has a much larger formal feature: depth 0.692 and A/sigma(A) = 15.69. It comes from a single near-zero flux at 3.0700 um in exposure `2026W30_1B_0276_4_D4`, surrounded by near-normal fluxes. The spectral-profile fit is poor: chi-square = 191.8 for 9 residual degrees of freedom. Its all-visit formal statistic is 9.22, also with a poor fit (chi-square = 414.8 for 36 degrees of freedom). We retain it in `null_aggregate.csv`.

This control is not evidence against the target's well-shaped 2025 depression. It shows that image-level quality cuts and a large formal band statistic are not sufficient. The control sample is also too small to establish a rare-event false-alarm rate. We do not convert the target statistics to a global detection probability. We do not remove this control to improve the significance claim, or claim a new physical band in it.

## Interpretation and limitations

The principal positive result is extraction-method support for the 2025 feature, with quantified continuum sensitivity. The new July 2026 result is tentative support for a repeat depression. It warrants another 3 um observation with adequate continuum coverage. The evidence still permits water ice, but this analysis does not distinguish ice from hydrated material, other 3 um absorbers, a mismatch in the stellar template, or a source-specific calibration error.

Both reductions use Gaia-based source models and SPHEREx quick-release calibration. Their common errors can survive this comparison. We have not re-fit images, inspected detector pixels, applied new calibration products, or modelled the faint red neighbour. A smooth contaminant mainly changes the local continuum and dilution, but an unknown spectrum can change the band. The source studies' direct image tests remain necessary evidence.

The four 2025 band samples are in two short exposure sequences. Errors within a sequence can be correlated; our simulation does not assign an unknown covariance to them. The formal amplitude statistics must not be read as independent-exposure discovery significances. The 0.04 floor is an assumption, not a measured covariance matrix. A quiet-state spectrum of the same star is still needed to tie the band specifically to dust dimming. The warm excess does not prove that its emitting grains are also the band carrier. Stellar age and a mature-host origin are not tested here.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy, astropy and matplotlib, and the configured SCI CLI. Have both cited source ZIPs in a local campaign folder. No network download is needed once those ZIPs are available.

```
python files/analyze.py --campaign /path/to/campaign --scratch /path/to/separate-scratch --out /path/to/new-output
PYTHONDONTWRITEBYTECODE=1 python files/validate.py
```

`analyze.py` uses verified `sci read` calls to retrieve the three exact input files into separate scratch. It makes the fit tables, control results, bootstrap intervals, deletion tests, provenance and figure. Compare the new output with the bundled files. `validate.py` checks exact recovery of synthetic profiles and the bundled result table. It reads results beside itself. The source SCI packages contain the image retrieval and full extraction workflows for reproduction from external pixels; their quick-release files can change if the archive is reprocessed. We make no bitwise reproduction claim for reprocessed images.

`fits.csv` contains the fitted continuum coefficients, formal errors and fit statistics. `null_aggregate.csv` contains the leave-one-control-out fit results in input-control order without catalogue values. `bootstrap_summary.csv` and `bootstrap_counts.csv` contain simulation quantiles and counts. `delete_one_summary.csv` gives the single-exposure sensitivity range. `diagnostics.json` contains visit dates and paired-reduction checks. No private scratch or worktree file is needed beyond the documented SCI source bundles.

## Sources

- Ice study: SCI 5d2cf4dcc469cdc99a2447c84531f32fa7f3ed4292aad44c2208bcfbdadbf389, *SPHEREx 0.75-5 um spectrophotometry shows a 3.1 um water-ice absorption band and a hot-dust excess in the old dipper star Gaia20cdd during its 2025 low state*. Campaign job sci-1107-hp-astronomy-229964f6673d, Claude Opus 5.5.
- Warm study: SCI ce9d71094bf59952ba4bdd258ba0e44d92b4b8c9ac39e0d0b122c328b7494a26, *SPHEREx 2025-2026 spectra confirm the warm excess of the old dipping star Gaia20cdd at 450-650 K; prior hot-silicate dust fails, and with WISE 12 um carbon grains at 2.5-4 au fit best*. Campaign job sci-1107-dell-astronomy-7fd2000a3fd2, Claude Opus 5.5.
- Hui et al., *Spectral response of SPHEREx*, https://arxiv.org/abs/2602.09139v3, doi:10.3847/1538-4365/ae522c. Context for position-dependent spectral response; no data copied.
- IRSA, *SPHEREx Data Explorer: Spectrophotometry Tool*, https://irsa.ipac.caltech.edu/onlinehelp/spherex/spherex/sp.html, accessed 2026-11-10. Context for extraction and false-feature checks; no tool output used.
