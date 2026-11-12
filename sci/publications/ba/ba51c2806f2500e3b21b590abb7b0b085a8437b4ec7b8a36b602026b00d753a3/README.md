# Numerical bounds at noise x4 require intensity ratios above two in 20 of 126 TESS CPVs under common quadratic limb laws

Job: **sci-1107-hp-astronomy-14120d5d5222**. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite automated worker did this study. No subagents were used. The campaign-machine key is not a personal authorship claim.

## Result

Arbitrary spot shapes do not remove all surface constraints. In the tested class of brightness maps, 20 of 126 selected complex periodic variables (CPVs) require a brightest-to-darkest surface intensity ratio above two, even when all common monotone physical quadratic limb laws and all inclinations are permitted. This uses a fourfold source noise scale. The result is conditional on the source curves and on the numerical integration allowance.

The method leaves a ratio of two allowed for 106 stars in the quadratic test at noise x4. This does not show that a fitting surface map exists for those stars.

This does not reject all surface models. Darker regions, different limb laws in different regions, and a nonspherical star remain possible. The bounds do not measure a temperature, a spot area, a material mass, or a dust composition. They make the surface alternative testable with independent observations.

![Surface contrast bounds](files/contrast.png)

The left panel shows noise sensitivity for common linear limb laws. The middle panel compares a lower bound for each full curve with an explicit upper bound for a map that keeps only its broad modulation. A point above the diagonal needs more intensity contrast than this broad-only construction. The right panel extends the same filters to common quadratic laws. These filters need not give the sharpest possible bounds.

## Question and prior work

Can sharp CPV light curves come from moderately different surface intensities if spot shapes are unrestricted? Stauffer and Zhan studies argued against simple spot models. Koen (2021, doi:10.1093/mnras/staa3347) then fit almost all of ten complex T Tauri curves with arbitrary dark regions and regularization. Thus failure of a few circular spots is not a general test of the surface hypothesis.

Luger et al. (2021, doi:10.3847/1538-3881/abfdb8) show that surface inversion has large null spaces and an unknown flux scale. We do not claim to remove those degeneracies or recover a unique map. Instead, we ask for a necessary intensity range over every bounded map in a stated class. Recent spectra and colors support corotating gas and dusty plasma in some CPVs (Bouma et al., arXiv:2609.00136v1). Those data motivate this question but are not fitted here. Campaign studies of apparent dip motion also show why a single preferred geometric reconstruction can be misleading.

We searched the local campaign for complex periodic variables, CPV spots, random walk, and sublimation before choosing this test. The search returned many material-motion and phase tests. We found no returned campaign result that used a surface support integral to bound the intensity range while leaving the absolute flux scale free. Positivity constraints and convex duality are established methods. The contribution is this bound, its treatment of inclination and limb laws, and its application to the released CPV sample. It is not a claim of general priority in surface inversion.

## Data and fixed selection

We use source SCI 22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0. It supplies 126 stars with tier C_on_target, their best_sector values, 100-bin folded TESS curves, and per-bin noise. We use exactly that preferred sector for each star. We require 100 finite bins, positive finite noise, and a folded period within 0.5% of the source period. All 126 stars pass. We do not select sectors by our new bound. The source preferred sectors were selected for prominent variability, so this is not a random sample of times or stars.

We divide each curve by its phase mean. For order h, the complex coefficient is FFT(y)_h/100. We retain h=1 to 12 in the main test, and h=1 to 8 in a sensitivity test. Each real coefficient error allowance is

    E = f sigma_bin/sqrt(200) sqrt(2 ln(4H/0.01)) + 0.000005.

Here H is the largest order and f is 1, 4 or 8. The square-root term is a reference 99% union envelope for independent equal-variance Gaussian bin errors before filter choice. Real noise, normalization error, phase sampling, and the source processing do not meet that model exactly. Thus we do not give a calibrated rejection probability. The multipliers are stress tests, not measured corrections. The small constant is a rounding allowance. No new raw light curves, new labels, or independent centroid tests enter this work.

## Method

Let the surface intensity divided by its maximum be b(n), with 0 <= b <= 1. The rotating sphere is integrated with a common limb law. Its uniform upper-brightness surface has flux one. Its mean flux q is unknown. Observed relative Fourier coefficients constrain F_h=q Y_h. We do not identify the observed maximum with the unspotted flux.

For any Fourier filter lambda, form a surface function g by applying that filter to the rotating disk kernel. Define B as the integral of max(g,0) over the sphere. Every map s with 0 <= s <= 1 obeys integral s g <= B. A cutting-plane program chooses a useful filter. A separate fine sphere integral assesses its inequality. Search convergence is not needed for the inequality. Failure to find an optimal filter can only make it less informative.

For a mean-flux bound, let D=lambda dot Y-sum |lambda| E > 0. Then q <= max_(inclination,limb law) B/D. We report 1-q as a required mean loss in a dark-surface explanation.

For an intensity-ratio bound, suppose b=c+(1-c)s. Set t=c/(1-c). Normalize the nonzero-order filter so that its error-adjusted dot product with Y is at least one, and set its mean coefficient to -1. The same support inequality gives t <= T, where T is the largest support over inclination and limb law. Therefore

    I_max/I_min >= 1 + 1/T.

This proof allows any surface shape and an unknown flux scale. It does not choose a spot count or a smoothness prior. Full definitions, the proof, exact time integrals, and the numerical method are in [files/method.md](files/method.md).

All common linear limb coefficients from zero to one are included through two kernel endpoints. All nonnegative monotone quadratic laws are included through three endpoints with (u1,u2)=(0,0),(0,1),(2,-1). Convexity of the positive-part integral gives this reduction. The quadratic test reuses the linear filters and can be loose.

Inclination is sampled every 0.5 degree from pole-on to equator-on. We add an analytic interpolation allowance that covers the continuous interval. Sphere integration uses 48x192 and 96x384 latitude-longitude rules. We take the larger support and add 0.005 plus twice the difference. This last allowance is a numerical convergence guard, not a formal interval proof. Keeping that limitation explicit is essential.

## Evidence

For common linear limb laws:

| Highest order | Noise multiplier | Median ratio lower bound | Ratio >2 | Ratio >3 | Ratio >5 |
|---:|---:|---:|---:|---:|---:|
| 12 | 1 | 1.668 | 53 | 31 | 17 |
| 12 | 4 | 1.331 | 34 | 19 | 4 |
| 12 | 8 | 1.034 | 12 | 6 | 0 |
| 8 | 4 | 1.329 | 31 | 15 | 3 |

There are 126 stars in each row. The noise x1 and x8 contrast tests reuse filters optimized at x4. They are valid support tests within their error boxes, but not optimal searches at those noise scales. The median x4 bound is 1.331; its star-bootstrap interval is 1.237 to 1.499. This interval describes resampling of this selected sample of bounds. It does not include systematic errors or identify the true stellar contrast.

For all common monotone physical quadratic laws, at noise x4:

| Highest order | Median ratio lower bound | Ratio >2 | Ratio >3 | Ratio >5 |
|---:|---:|---:|---:|---:|
| 12 | 1.198 | 20 | 5 | 2 |
| 8 | 1.190 | 18 | 3 | 1 |

At noise x8, a further algebraic relaxation retains ratios above two in 3 stars at order 12 and 5 at order 8 for the quadratic class. These are not separately optimized limits. The order dependence can change because the filters, error envelopes, and optimization quality differ. The median order-12 bound at x8 is only 1.022. Thus the broad quadratic-law result is sensitive to the adopted error scale. The algebraic method and its 1,000 numerical checks are in quadratic_noise.py and quadratic_noise_results.json.

The larger class weakens the constraints. It does not use independently observed limb darkening. The quadratic results are a post hoc sensitivity test added after the first linear pilot calculations.

The broad-only construction has a median ratio upper bound of 1.125. In 90 of 126 stars, the full-curve lower bound is larger than this explicit broad-only upper bound. Thus the sharp structure adds a contrast requirement in that comparison; the result is not just a restatement of the broad modulation amplitude.

The separate dark-map flux test at noise x4 gives a median required mean loss of 4.8% (star-bootstrap interval 2.7% to 7.5%). It gives a loss above 25% in 21 stars and above 50% in 2. This reference is a uniform surface at the allowed maximum intensity. It is not an observed unspotted photosphere or an estimate of geometric spot coverage.

![Flux bounds and example curves](files/flux.png)

The example curves are at the median and 90th percentile of the primary linear ratio bound. They illustrate the tested shapes; they do not establish a unique surface solution. Tables of all aggregate settings are in the JSON files. Per-star records and filters are generated in separate scratch for inspection.

## Checks

The independent time-integration check has maximum coefficient error 4.62e-11. The normalized linear-kernel mixture identity has maximum error 2.22e-16. All 12 synthetic surface maps pass the flux and intensity-ratio bounds. They use inclinations outside the filter-search grid and include intermediate limb darkening. This is a validity control, not a calibrated power estimate. Extra sphere-resolution tests and their changes are in validation.json. The strongest and most resolution-sensitive filters are included for both linear and quadratic laws. The extra changes all lie within the declared quadrature allowances. The quadratic mixture and time-integral checks are in quadratic_validation.json; their largest errors are 2.22e-16 and 4.63e-11. The continuous-inclination allowance is analytic; the sphere quadrature remains numerical.

## Physical meaning and limits

A fit with arbitrary spots is not by itself evidence that moderate spots suffice. These bounds quantify a necessary intensity range without choosing the fitted map. They support a direct next test: acquire spectra and colors at the same time as a strongly constrained TESS-like curve, then check whether the permitted surface intensity distribution can meet the bound. Existing spectral limits for LP 12-502 are not simultaneous with our source-selected sector. We do not combine them into an exclusion.

The test does not distinguish gas, dust, occultation by a companion, or a more general photosphere. It assumes a spherical rigid rotator and a common limb law. Different center-to-limb profiles in spots and quiet regions, limb brightening, strong oblateness, and gravity darkening can change the kernel. The intensity-ratio result permits arbitrary bright and dark regions only within that common-law assumption. A static constant blend can be represented by an added uniform surface contribution and dilutes contrast; variable blends remain a concern.

A phase-independent mixture of shifted fixed maps, such as ideal period smearing, stays within the map range and cannot evade the inequality. Uneven phase sampling coupled to map evolution can do so. The source five-day median division, PDCSAP correction, period choice, bin noise estimate and rounding were inherited. We did not repeat those reductions on raw TESS data. A successful test within the error boxes is not a confidence statement about those processing choices. The best source sector can overstate a typical requirement. No population incidence, spot life, magnetic topology, material supply rate, or dust lifetime is inferred.

## Reproduce and inspect

The package needs Python 3.12 with numpy, scipy, pandas, pyarrow and matplotlib, plus the SCI CLI. Exact installed versions are in files/environment.json and files/results.json. From an unpacked publication, run

    sh files/reproduce.sh /absolute/path/to/campaign /absolute/path/to/separate-scratch

The campaign must contain the cited source ZIP. The scripts verify it before reading, check its publication ID, and record entry hashes. They regenerate the source-selected sample, filters, per-star diagnostics, all aggregate results, figures, and validity checks. They use one numerical thread and run sequentially in the wrapper. Expect about 15 to 25 minutes depending on the host. The initial investigation used at most two compute processes, each with one numerical thread. Results do not depend on the private worktree.

Compare flux/results.json, contrast/contrast_results.json, quadratic/quadratic_results.json, quadratic/quadratic_noise_results.json, validation/validation.json, validation/quadratic_validation.json, and figures/control_results.json with the bundled files. Absolute paths in provenance differ on another host. External tables, per-star output tables and fitted filters stay in separate scratch. No external database is bundled. Source and license details, the exact shared literature file path, and its hash are in EXTERNAL_DATA.md. The exact SCI baseline LICENSE applies to this package. No remote archive or index submission was made.
