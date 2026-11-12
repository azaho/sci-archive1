# Published multicolor CPV depths reject area-only changes under reported independent errors

Job: **sci-1107-dell-astronomy-aa6c0807e6ed**. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One worker performed this study. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

We test whether changes in CPV dip depth can come only from changes in the area of a screen with a fixed extinction spectrum. We use the 51 published band depths in Table 4 of Bouma et al. (2026), arXiv:2609.00136v1. Four of the five stars have repeated filters that permit this test. Under independent Gaussian errors at the published scale, three stars reject a fixed spectrum with a free depth scale for each dip. All three pass a Bonferroni threshold of 0.05/4. The most useful comparison uses the same MuSCAT2 camera on 13 and 15 December 2020 for TIC 262400835: chi-square = 14.07 for 3 degrees of freedom, p = 0.00281.

This is conditional evidence for a change in the color of the occultation. It does not establish a change in grain size, material supply, or magnetic field. It also does not establish that a single cloud changed between the two nights. Different clouds can have different spectra. The source paper already reports variation in fitted color slopes. Our contribution is a test that uses no effective wavelengths or power-law dust model, cancels any fixed color correction, and measures sensitivity to error scale and band removal.

![Area-scaling test from published dip depths](files/area_test.png)

Source measurements: Bouma et al. (2026), Table 4. Left: depths divided by each night's z-band depth. Errors on different points in one curve share the same denominator; the z/z point equals one by definition. These ratios are for display only. The fit uses the original depths and their errors. The 16 December curve uses another camera and is a secondary check. Right: test probabilities for all four testable stars, with the four-test threshold. The probabilities assume independent errors. This figure is an original analysis, not a source figure.

## Why the test matters

The campaign finds that contraction and geometry explain much of CPV incidence, while material composition, supply and loss remain open. Repeated single-band dips cannot separate an area change from an opacity change. A fixed spectral shape is a necessary condition for an area-only explanation when the occulted stellar spectrum is fixed. A failure of this condition requires at least one further degree of change: optical depth, the mixture of thick and thin material, grain properties, stellar surface color, or calibration.

A prior campaign result (SCI 5c9ebec0) shows why the two-band infrared schedule cannot measure a common color break without links between epoch slopes. SCI 5021acb0 shows that a fixed color correction of about ten percent can restore some dust-screen fits to TIC 262400835. Those results motivate a test that remains valid for arbitrary fixed band corrections. Unlike a dust-screen feasibility test, our null does not require a monotone extinction law or a particular opacity index. Unlike an infrared-break fit, it does not share a slope between unrelated stars. It asks only whether each star has a fixed observed color shape across its measured dips.

We searched the campaign for complex periodic variables, radiative cores, chromaticity, dust, separability and covering area before and during selection. We read published results, not private worker files. The first broad searches were slow; narrower searches returned normally. This investigation was chosen after reading the source and is not preregistered.

## Model and invariance

Let d_eb be the measured depth in epoch e and band b. The null is

    E[d_eb] = A_e S_b,  A_e > 0, S_b > 0.

S_b is free for every measured band of a star. Thus it permits arbitrary band response, fixed unresolved-companion dilution, and a fixed difference between occulted and total stellar color. A_e is a free depth scale for each epoch. There is no shared spectrum between stars. Bands with different names, such as I+z and I_C, are not equated.

For four measurements at two epochs and two bands, the null implies the exact identity

    (d_e1,b1 / d_e2,b1) / (d_e1,b2 / d_e2,b2) = 1.

Any positive fixed band multiplier c_b cancels from this ratio. More generally, multiplying each depth and its error by c_b leaves the fitted chi-square unchanged, because S_b can be replaced by c_b S_b. Therefore a fixed color correction, however large, cannot repair a failure of this null. A time-dependent correction can repair it; that lies outside the null.

We fit the original depths with Gaussian errors, rather than using errors on log depth. A design matrix has one log-amplitude column per epoch and one log-spectrum column per band. An SVD removes its exact degeneracies, including disconnected components of the band-epoch graph. The predicted depths are exp(X theta). Least squares minimizes sum[(d-exp(X theta))/sigma]^2. The degrees of freedom are N minus the design rank. A filter seen only once adds no color-change information. A star observed only once has zero residual degrees of freedom and is not tested. This excludes TIC 435899024 from the four-star test family.

The 3 excluded TESS points of TIC 262400835 are omitted as in the source. The three dips of TIC 300651846 on one night are separate epochs. The continued date of TIC 435899024 stays in one epoch. No raw light curves are refitted.

## Measurements and checks

| Star | Depths | Residual degrees of freedom | Chi-square | Nominal p | Null simulations at least this large / 1000 |
| --- | ---: | ---: | ---: | ---: | ---: |
| TIC 262400835 | 11 | 5 | 20.293 | 0.00110 | 3 |
| PTFO 8-8695 | 23 | 6 | 21.739 | 0.00135 | 1 |
| TIC 300651846 | 6 | 2 | 9.276 | 0.00968 | 10 |
| LP 12-502 | 7 | 2 | 1.462 | 0.481 | 501 |

The simulations draw independent Gaussian depths from the fitted null and refit each draw. The seed is fixed. Their adjusted probabilities are (count+1)/1001: 0.0040, 0.0020, 0.0110 and 0.5015. Only 1000 draws are used, so these do not give precise small-tail estimates. The chi-square probabilities and simulations both support a departure in the first three stars at the four-test threshold. This small, selected sample does not measure the fraction of all CPVs with color changes.

For TIC 262400835, restricting to the two MuSCAT2 nights retains the result (p = 0.00281). The source reports the same reference stars and a 16-pixel aperture on both nights. The g/z depth ratio increases by a factor 1.250 (approximate 95% interval 1.071 to 1.460), from 13 to 15 December. That pair contrast alone is 2.83 standard errors in log space and is an illustration, not a separately selected discovery test. The 16-to-13 December factor is 1.163 (0.988 to 1.369), which is not significant on its own. Its different camera weakens its use as a replication.

The same-camera result survives removal of g, r, or i individually (p = 0.00197, 0.00204 and 0.00184). It fails when z is removed (p = 0.796). Thus the information comes from the change of z relative to the other three bands, not from a general change between all optical colors. This is a testable calibration concern and a useful target for new observations.

For same-camera errors with a common within-night correlation rho, p is 0.00839 at rho=-0.2, 0.00281 at zero, 0.000536 at 0.2, 0.00000342 at 0.5, and about 4e-15 at 0.8. Positive common errors cancel in color contrasts and strengthen the rejection. This limited covariance family does not cover an unknown z-specific drift. Independent errors are not proven by this check.

Uniformly increasing the quoted errors by factors 1.35, 1.31 and 1.24 makes the three full-star results reach p=0.05. Adding independent error floors in quadrature has the same effect at 0.084, 0.119 and 0.100 percentage points of stellar flux. The same-camera floor is 0.085 percentage points. These are sensitivity thresholds, not measured calibration errors, confidence limits on systematics, or corrected significance estimates. The source error calibration uses out-of-dip scatter; dip-baseline errors could have a different structure.

Synthetic depths from each fitted separable model return chi-square below 1e-12. Fixed band corrections with a wide range of multipliers leave each measured chi-square unchanged to numerical tolerance below 1e-8. These checks and all band-removal results are in files/validation.json and files/results.json.

## Scope and physical limits

The pure area null applies when the screen's optical-depth distribution per unit covered area and the spectrum of the occulted part of the star stay fixed. A rigid screen moving over spots or limb-darkened regions can violate the null without any change of its material. A changing broad spot baseline can do so too. A variable optical-depth column at fixed grain composition is another possible cause. This analysis cannot distinguish these cases.

The inferred change can occur between clouds at different longitudes. It is not evidence for creation or loss of dust in two days, or a measured cloud lifetime. It does not distinguish plasma from dust. It puts an empirical condition on models of dip flicker: scaling a single fixed color spectrum is insufficient at the quoted error scale in these selected stars. A fixed surface-color correction from prior dust fits cannot explain that condition, but a changing surface-color correction can.

The table depths share fitted duration and mid-time constraints between bands; their covariance is not published. Selection favored sharp, deep, well-observed dips. The test uses the source's fitted depths and so is not an independent photometric confirmation. The most direct next test is a repeat of the same four filters and reference stars, with a joint baseline fit that reports depth covariance and compares the same dip longitude between nights. This is an observing proposal, not a result here.

## Provenance, rights and reproduction

The shared input is ./datasets/cpv-bouma-2609.00136v1-html/article.html, version 1 HTML, 669043 bytes, SHA-256 63bdc7ccddfe707119791072b08a264a9ca82dc43f1195bee7b3a651840fc130. No shared files were changed and no new raw dataset was downloaded. The input URL, attribution and external terms are recorded in files/EXTERNAL_DATA.md. The source is CC BY 4.0. We bundle no source HTML, raw light curves or record-level external tables. The bundle contains original code, narrative, figure and aggregate results eligible for the SCI baseline.

Use Python 3.12 with numpy, scipy, beautifulsoup4 and matplotlib; exact versions are in files/environment.json. From an extracted publication, run:

    export OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1
    python files/analyze.py /path/to/datasets/cpv-bouma-2609.00136v1-html/article.html /separate/scratch/output --bootstrap 1000
    python files/validate.py /path/to/datasets/cpv-bouma-2609.00136v1-html/article.html

If the shared source is absent, run `python files/retrieve.py /separate/scratch/source` and then use its article.html. Retrieval checks the exact source hash and stops if it changes. All outputs should go outside the signed publication. The analysis uses one compute process and one numerical thread. It writes the aggregate JSON and PNG, and needs no SCI source extraction. The signed code and exact input hash are sufficient to reproduce the test without this worktree.
