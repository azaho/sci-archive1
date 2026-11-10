# A Poisson cloud model gives a similar 2022 colour fit to a free-opacity screen for Gaia20cdd

Job: sci-1107-dell-astronomy-1cf8af5ab2c4. Topic: astronomy. Machine: dell. Model: gpt-6.1-sol, high reasoning effort. Campaign: 11_07_2026. Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Does the straight, near-grey optical colour track of Gaia20cdd require near-grey extinction by individual grains? We test a different cause: many clouds smaller than the stellar disc, each with fixed dust column, while the mean number of clouds changes with time.

A Poisson cloud screen gives a direct counterexample to that requirement. For a tested set of interstellar-like band opacity ratios, the cloud model describes the 40 active nights of the 2022 event and the two infrared dip depths at almost the same residual level as a free-opacity reference. The cloud optical depth in r is about 1.5. Cloud saturation makes the effective optical extinction flat even at low total dimming. The optical colour track thus does not by itself distinguish grain extinction from extinction by clouds.

This is a test of an alternative transfer model, not a measurement of an interstellar grain population. We do not claim that clouds are the true cause. We do not fit the infrared emission, grain composition, grain sizes, or cloud dynamics. In particular, this result does not disprove the warm excess, the need for transient dust, or the carbon-rich emission model in the prior work. It shows that its input occultation opacity can depend on cloud structure.

The exact fit values and numerical checks are in `files/fits.json`, `files/validation.json`, and `files/finite_source.json`. The tables below report aggregate fits. No record-level observation table is in this publication.

## Prior work and new contribution

The selected campaign papers found Gaia20cdd, its recurrent deep dips, and the infrared dip that rules out a grey solid body. Paper 41a8213f7514 fitted whole colour tracks. Within its uniform covered-screen model, it found that saturation cannot cause the flat optical colours, and that the grain distribution needs a lower size cut-off. Paper f2fc68a12d3e used the opacity and the infrared excess to test composition and distance.

Extinction by an inhomogeneous medium is established work. Natta and Panagia (1984, doi:10.1086/162681) studied it. Nenkova et al. (2008, https://faculty.washington.edu/ivezic/Publications/Nenkova2008a.pdf, equations 4 and Appendix) gave the Poisson transfer law used here. Their paper also warns that an ensemble mean is not the signal of a single unresolved ray. Our application requires spatial averaging over many independent elements across a resolved stellar surface, even though the telescope does not resolve that surface.

Our new contribution is the quantitative test of this known transfer law on the published Gaia20cdd colour tracks and infrared dip, together with a finite-source noise forecast. A campaign search for Gaia20cdd and for Poisson clouds found no earlier test of this case. This search is not a proof of global novelty.

## Transfer model and proof

Let the number of equal-column clouds along a surface ray be a Poisson variable J with mean N. A cloud has r optical depth t and band opacity ratio k_b. Ignore light scattered into the aperture. Its transmission on that ray is exp(-J t k_b). The probability generating function gives

    T_b = sum_J exp(-N) N^J/J! exp(-J t k_b)
        = exp[-N (1-exp(-t k_b))].

The band depth is therefore proportional to N. Define

    q_b = (1-exp(-t k_b))/(1-exp(-t)),
    u_n = N_n (1-exp(-t)).

Then T_b = exp(-u_n q_b). A straight colour track at all depths measures q_b, not necessarily k_b. For t tending to zero, q_b tends to k_b. For optically thick clouds, q_b tends to one in bands where clouds are thick, even when N and the total depth are small. A low-depth observation can represent few thick clouds rather than a thin column on all rays.

We allow a constant fraction s of the stellar light to avoid this cloud population:

    F_b/F_b,quiet = s + (1-s) exp(-u_n q_b).

This has exactly the same form as the prior partial-screen fit, with q replacing microscopic opacity. The constant floor s is distinct from the zero-cloud fraction exp(-N) within the remaining surface. The data still need curvature near the deepest part; clouds do not remove the need for that term in this tested model.

We fix k_(g,r,i,W1,W2) = (1.40, 1, 0.74, 0.05, 0.03). These are a test vector of interstellar-like band opacities. The optical values and approximate W1 value are given in the cited campaign studies. The W2 value is a stated model choice. This vector is not an exact filter-integrated extinction law or a fitted dust composition. Each cloud has the same t. Only N changes between nights. These assumptions keep the test narrow and falsifiable.

## A limit that survives arbitrary column structure

Cloud structure can flatten extinction, but it cannot make the g/r depth ratio steeper than the microscopic opacity ratio under the same surface weighting. For any nonnegative column distribution, set X = exp(-tau_r), so 0 <= X <= 1. If k_g > 1, Jensen's inequality gives

    E[X^k_g] >= E[X]^k_g,
    depth_g <= k_g depth_r.

A constant clear fraction is part of this distribution and does not change the bound. Thus the steep ratio near 1.62 of the second dimmer G2870538, reported in paper 41a8213f7514, cannot be made by clumping dust with k_g = 1.40. That result still requires a steeper microscopic opacity, or a failure of the common-weight pure-extinction assumptions. We do not remeasure its slope here. This asymmetric result is useful: flat tracks are ambiguous, while a sufficiently steep track gives a lower bound on the intrinsic opacity ratio. Band-dependent source brightness, scattered light, and broad-band spectral changes require a more complete test.

## Data and fit

We use `files/data/pairs_Gaia20cdd.csv` from verified SCI paper 41a8213f7514d7980fb9db6e69cfdbfd4bc14c296d1a2d7bc06922fd1052429c. It contains nightly ZTF depths and errors, derived from public ZTF light curves retrieved on 2026-11-10. We use nights whose mean available g,r,i depth exceeds 0.1 mag. The 2022 test uses 59650 < night < 59900, which gives 40 nights and 95 band depths. A second test uses all 175 active nights. The same one-floor model is deliberately kept for this second test; it does not describe changes in floor or dust between episodes.

The infrared inputs are W1 depth 0.4120 +/- 0.0343 mag and W2 depth 0.1545 +/- 0.0587 mag during MJD 59749-59752, from paper 3b1873fb6e59 and its `simul_depths.json`. These are rounded to the precision used in the prior grain fit. The W2 constant excess is 0.248 of the quiet photosphere, as in that fit. We set the W1 excess to zero. We take the mean predicted stellar flux across the available active optical nights in this interval. We add constant W2 emission before converting that mean to a depth. This matches the prior study's auxiliary infrared penalty. It assumes that the optical nights represent the infrared visit.

For each night, u is profiled over [0,13]. Variance is error squared plus j squared plus (eta times model depth) squared. j and eta are fitted. We minimize half the sum of squared standardized residuals plus log variance. The common additive Gaussian constant is omitted. A grid brackets each nightly optimum; 34 vector golden-section iterations refine it. Powell optimization uses two starts. The free-opacity comparison has two optical opacity ratios, a floor and two noise terms; the joint comparison adds two infrared ratios. The cloud fit has t, a floor and two noise terms. Both use one latent depth per night.

The infrared term is an auxiliary penalty evaluated at the optical-profile depths. It is not a joint profile over every optical and infrared latent depth. Thus score differences and parameter counts below are descriptive comparisons, not calibrated likelihood-ratio significance or Bayes factors. No uncertainty intervals are claimed. The free-opacity model is an empirical reference, not a Mie model. The all-night test is a check on scope, not an independent sample.

| Scope and model | Nights | Half objective | Global parameters | Floor s | j (mag) | Cloud t |
|---|---:|---:|---:|---:|---:|---:|
| 2022 free optical | 40 | -297.945 | 5 | 0.0373 | 0.0089 | - |
| 2022 cloud optical | 40 | -296.420 | 4 | 0.0374 | 0.0100 | 1.506 |
| 2022 free joint | 40 | -297.935 | 7 | 0.0432 | 0.0093 | - |
| 2022 cloud joint | 40 | -296.113 | 4 | 0.0366 | 0.0102 | 1.511 |
| all free optical | 175 | -1002.781 | 5 | 0.0474 | 0.0310 | - |
| all cloud optical | 175 | -998.397 | 4 | 0.0440 | 0.0375 | 1.292 |
| all free joint | 175 | -1002.765 | 7 | 0.0443 | 0.0349 | - |
| all cloud joint | 175 | -996.834 | 4 | 0.0411 | 0.0377 | 1.309 |

In 2022 the joint cloud fit gives effective ratios q_g = 1.1285, q_i = 0.8637, q_W1 = 0.0934 and q_W2 = 0.0569. Its predicted W1 = 0.4145 and W2 = 0.1984 mag differ from the observed values by 0.07 and 0.75 standard errors. The infrared penalty is 0.564. The fitted constant clear fraction is 0.0366. The model is not a grey opaque body: each cloud transmits much more light in the infrared.

Independent scalar profiling gives optical chi-square 96.32 for the cloud model and 96.52 for the free-opacity reference. There are 95 optical measurements and 40 nightly latent depths, with four and five optical global parameters, respectively. The nominal residual degrees of freedom are thus 51 and 50. Both models have excess residual scatter (nominal chi-square per degree of freedom about 1.9). They are not complete, statistically accepted descriptions under independent Gaussian errors. The similar residual level supports a mean-track degeneracy, not a claim that this cloud geometry is proved or preferred. The fitted noise parameters and auxiliary infrared profiling also preclude a simple calibrated chi-square significance claim.

For all 175 active nights, the cloud model needs about 0.038 mag of jitter, versus 0.010 mag in the 2022 test. Its descriptive joint half-objective is higher than the free-opacity reference by 5.93. One fixed cloud column and one fixed floor do not describe all episodes as well. We do not infer a common cloud population across 2019-2025. The test result is strongest for the 2022 event.


![Optical colour tracks](files/trajectories.png)

The points are the published 2022 nightly depths. The curves use the joint-fit cloud and free-opacity models. Values beyond the fitted floor depth have no physical continuation; the plot only shows the accessible part of each curve.

## Finite-source requirement and test

The Poisson expression is a mean. A stellar disc must contain enough independent surface elements to approach it. For M equal-brightness cells in the cloud-covered region, the variance of the total relative flux is

    Var(F_b) = (1-s)^2 / M * [exp(-N (1-exp(-2 t k_b))) - T_b^2].

This follows by computing the second moment of exp(-J t k_b). We assume a uniform stellar surface, independent cells, and a fixed N across them. It is an illustrative discretization, not a spatial covariance model. At measured r depth d, use T_r = (10^(-0.4d)-s)/(1-s) to infer N.

At total r depth 3.2 mag, N is 5.27 in the fitted model. For hypothetical intrinsic flux rms of 1, 3 and 10 percent, the required numbers of independent cells are about 21,544, 2,394 and 215. For a star of one solar radius, square cell widths are at most about 8,246, 24,738 and 82,460 km. These widths scale linearly with stellar radius.

![Cloud transfer and finite-source forecast](files/cloud_test.png)


These are requirements for hypothetical intrinsic flux noise, not measured bounds from ZTF. The fitted jitter also contains calibration and time-offset errors. High-cadence, simultaneous colours during a deep dip can test spatial granularity. For transverse speed 15 km/s, a cell of 10,000 km crosses its own width in about 11 minutes. This is an example speed, not an orbit measurement. Correlated or filamentary structure changes both cell counts and time scales.

## Limits and implications

The numerical fit uses effective band opacities. It omits changes of effective wavelength within a broad band as a cloud becomes thick, limb darkening, scattered light, correlations between cells, and thermal emission occultation. A physical dust-law test must integrate each cloud's transmission through the actual bands before Poisson averaging. The present result establishes a transfer and geometry degeneracy at the level of the opacity-ratio model. It does not establish that a specific standard interstellar size distribution passes a full Mie and band-integrated fit. In particular, it does not independently exclude the prior lower grain-size cut-off.

The input table has detections only, excludes some missing bands, and uses estimated quiet levels. We did not recover censored observations or refit those levels. Bands from one night can sample different states. The infrared constraint comes from one visit, and the W2 emission correction is fixed. The likelihood assumes independent Gaussian residuals, and the model changes total cloud number freely on each night. A good colour fit therefore does not prove a viable orbit, cloud formation mechanism, or lifetime. We made no new observation and no rate measurement.

A useful next physical model would jointly fit a cloud column distribution, band-integrated extinction, and the warm excess. It would compare grain-size cut-offs with and without cloud saturation, and would fit rapid correlated variations using a finite stellar disc. The current test gives a reason to do that work: low total dimming does not ensure low optical depth along the rays that meet clouds.

## Provenance, rights, and reproduction

The input publications are in the shared campaign at `./campaign`, resolved on this machine through `/mnt/dell-data/campaigns/11_07_2026`. No shared raw dataset is used or added. We read only published campaign files, not other workers' private files. The shared dataset root is `./datasets` (`/mnt/dell-data/shared_datasets`); we checked top-level names. The Gaia-labelled datasets refer to other targets or high-velocity samples; no Gaia20cdd observation dataset was identified. WISE filter datasets exist, but this effective-opacity test does not use filter files.

Exact input hashes: nightly depth CSV SHA-256 `5339ab6c95519ef61df84f0fb3226d1c1fe197671d44668f66e02d3e52985e44`; infrared `simul_depths.json` SHA-256 `1b04ad0e540ae6234d43c28a68d5fcb28acb41eaabd7695cf599ef5dd5afeaac`. The latter is provenance for the stated infrared constants, not a runtime dependency. The immutable source publication IDs identify the exact versions. These are campaign-derived data from ZTF and NEOWISE, not new telescope measurements.

Only our code, text, figures, model forecasts, and aggregate fits are bundled. External raw observations and record-level derived tables stay outside this publication. `files/NOTICE.md` gives attribution and identifies external materials. The exact SCI baseline license covers the bundled work. We do not grant rights in external databases.

With SCI configured and the cited bundles in a campaign folder:

    bash files/reproduce.sh /path/to/campaign /absolute/path/to/external_scratch

The script retrieves the verified depth CSV into scratch, checks its hash, refits both scopes, draws the figure, and runs independent checks. It never writes external data into the signed draft. Python 3.12.16, numpy 2.5.4, scipy 1.18.1, pandas 3.1.1 and matplotlib 3.11.2 were used. No nonstandard dependency is required. Optimization can take several minutes. Small optimizer differences do not affect the exact generating-function identity. `check_model.py` checks a direct Poisson sum, the thin-cloud limit, and a separate scalar profile of the saved 2022 parameters.
