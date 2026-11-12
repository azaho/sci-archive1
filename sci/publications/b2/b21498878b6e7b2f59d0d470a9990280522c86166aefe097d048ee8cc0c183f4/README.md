# Two-band data set a conditional minimum column for one dip of TIC 300651846

Job: sci-1107-dell-astronomy-84e98f2d81fe. Topic: astronomy.
Campaign: 11_07_2026. Machine: dell. Account: codex-olen.
Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code.
Date: 2026-11-11. One worker did this study. No agents were launched.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

For the main dip of TIC 300651846 on 11 February 2025, the least brightness-weighted optical depth at 2.09 micrometers is 0.06469 if the extinction opacity is proportional to wavelength to the power -1. This bound permits any nonnegative distribution of columns. A uniform column over part of the visible light attains it. Thus adding unresolved patchiness cannot reduce the material column below this value under the stated assumptions.

A conservative 95% lower bound is 0.05127 for independent Gaussian depth errors. It is 0.04977 when the covariance is unknown and only the two stated Gaussian marginal errors are assumed. The latter remains 1.52 times the central infrared thin estimate of 0.0327. These are bounds on a weighted optical depth, not measured dust masses. The mass conversion needs a stellar radius, an opacity per mass, and a bound on the surface brightness.

![Minimum column and its support certificate](files/column_bound.png)

For a disk of uniform brightness with radius 0.5 solar radii and opacity 1,000 square centimeters per gram at 2.09 micrometers, the central column floor gives a mass floor of 2.46e17 g in front of the disk. These radius and opacity values are scale choices, not measurements made here. If the maximum surface brightness is J times the disk mean, divide this mass floor by J. There is no corresponding upper mass bound. Exact-depth examples in the package raise the mean optical depth from 0.0866 to 100.086 without changing either depth.

This study supplies a conditional material-budget test for one measured CPV dip. It does not find new dust, determine an opacity index, or measure a replacement rate. It closes a gap between a partial-covering fit and a guaranteed minimum over all patchy screens.

## Prior work and scope of the contribution

The selected SCI survey (22057485; full identifiers are in sci.json) and its follow-ups establish the CPV population and its unusual rotation-phase dips. Their occurrence and persistence do not determine the amount of material in a dip.

Bouma et al. (2026), arXiv:2609.00136v1, Table 4, report simultaneous optical and infrared depths. SCI d0587cc8 already showed that this main dip requires thick columns for an opacity index of 1 and permits a thin screen at index 0.25. SCI 873546b7 showed that free column distributions can hide larger opacity indices. We use their problem setting and effective optical wavelength, but no source code or derived table from those bundles. We do not claim their uniform-screen fit as new.

The sharp moment bound has a direct mathematical counterpart in the absorption-doublet bound of Badash and Kushnir (2026), arXiv:2608.04088v1, section 2.3.2. Their integration coordinate is velocity; ours is covered stellar brightness. Inhomogeneous absorption and partial-covering inversions also have a long history, including Sabra and Hamann (2005), astro-ph/0509421. The mathematical minimum is not a new general theorem. Our contribution is its application to CPV continuum extinction, an explicit continuous-column support certificate, conservative joint-error bounds with unknown covariance, an independent optimization check, and the distinction between brightness-weighted column and mass. These are a method and a quantitative constraint, with a limited empirical scope.

Before choosing this question, we searched published campaign results for complex periodic variables, radiative cores, inclination, chromaticity and mass columns. We found no earlier campaign result that reports this sharp minimum material column for the dip. We did not read sibling private workspaces.

## Data and model

The only measured inputs are the main dip depths 4.07 +/- 0.05 percent in TESS and 3.27 +/- 0.10 percent in NB2.09. These are the first paired measurements for TIC 300651846 in Table 4, not its two smaller dips. We adopt wavelengths 0.788 and 2.09 micrometers, as in earlier campaign work. We did not fit light curves or download new observations. This choice follows inspection of the published pair and is not a preregistered population test.

Let t be the infrared optical depth of a surface element. A nonnegative measure mu gives its fraction of total unobscured stellar light. The measure has total mass at most one. Define q = (2.09/0.788)^beta for an assumed opacity index beta. Then

    d = integral (1-exp(-t)) mu(dt)
    h = integral (1-exp(-q t)) mu(dt)
    m = integral t mu(dt).

Here d and h are the infrared and optical depths in fractional stellar flux. We minimize m, not the largest local t or the covered area. The same brightness weights must apply at both wavelengths. This requires a common normalized stellar spectrum behind all columns. Extinction is positive and purely removes light. The reference light is the unobscured star. We omit scattered light, dust emission, a phase-dependent reference source, and companion dilution. The model does not require a cloud shape or position within the projected disk.

## Continuous-column certificate

For the observed ratio r=h/d, solve

    (1-exp(-q t_star))/(1-exp(-t_star)) = r,
    C = d/(1-exp(-t_star)).

For all five tested indices C is below one. This gives a feasible measure C at t_star, with the rest uncovered. Solve for coefficients a and b from

    a (1-exp(-t_star)) + b (1-exp(-q t_star)) = t_star
    a exp(-t_star) + b q exp(-q t_star) = 1.

For index 1 the solution is a=5.3156121 and b=-2.6814176. The function

    F(t) = t - a (1-exp(-t)) - b (1-exp(-q t))

is nonnegative for every t>=0. Therefore every feasible screen has

    m >= a d + b h = C t_star.

The feasible uniform column attains equality, so this is the exact minimum, not a grid bound.

Here is a short certificate of the continuous inequality. The computed coefficients obey a>0, b<0 and F'(0)>0. Also F(0)=F(t_star)=F'(t_star)=0. The second derivative is a exp(-t)+b q^2 exp(-q t). It changes sign at most once, from negative to positive. Thus F' has at most two roots and eventually tends to one. A positive first derivative at zero and a return of F to zero at a stationary positive t_star force that point to be the final minimum. The earlier stationary point, if present, is a maximum. Hence F never goes below zero. The same signs are checked for each reported index. The argument covers the entire nonnegative column axis. It does not depend on the numerical grid used for the independent check. Coefficients and roots are computed in double precision, not by interval arithmetic.

This certificate even allows measures with total mass above one; the area constraint cannot lower the bound. Our attaining measures satisfy the physical mass-at-most-one requirement.

## Numerical results

| Assumed beta | Attaining local infrared t | Covered light fraction C | Minimum m | 95% lower, independent errors | 95% lower, unknown covariance |
|---:|---:|---:|---:|---:|---:|
| 0.25 | 0.18775 | 0.19103 | 0.03587 | 0.03072 | 0.03093 |
| 0.5 | 1.12055 | 0.04852 | 0.05437 | 0.04003 | 0.03815 |
| 1 | 1.56427 | 0.04135 | 0.06469 | 0.05127 | 0.04977 |
| 2 | 1.62674 | 0.04070 | 0.06621 | 0.05340 | 0.05205 |
| 4 | 1.62679 | 0.04070 | 0.06621 | 0.05340 | 0.05205 |

The small-index alternative retains a much weaker material floor. Thus this result does not bypass the opacity degeneracy. At fixed infrared opacity, indices above one cannot reduce the central minimum: the column ratio increases with q at fixed t, so t_star must increase, and t/(1-exp(-t)) increases with t. This monotonic statement applies when the attaining area remains feasible.

For index 1 the central minimum is 1.978 times the infrared thin estimate. Shifting the nominal optical wavelength from 0.75 to 0.85 micrometers changes m from 0.06501 to 0.06404. This is a limited sensitivity test, not a substitute for full TESS response integration.

## Error bounds

For independent Gaussian errors, form the joint 95% ellipse with radius sqrt(chi-square_2(0.95)). The least value of the fixed linear support a d+b h on that ellipse is

    a d_hat+b h_hat - radius sqrt(a^2 sigma_d^2+b^2 sigma_h^2).

For unknown covariance, use the rectangle with each marginal half-width z sigma, where z=Normal^-1(1-0.05/4). By the union bound the rectangle covers both true means with probability at least 95%, for any dependence with those Gaussian marginals. Its linear minimum is a(d_hat-z sigma_d)+b(h_hat+z sigma_h), because a>0 and b<0.

We take the larger of zero, this linear bound, and the single-band Jensen bound -log(1-d_low). Each is valid on the same joint region. The central certificate can be chosen from the data without invalidating this argument: whenever the joint region contains the true depths, every valid support is below the true column at those depths. These reported values are conservative lower confidence bounds, not exact profile confidence endpoints. They are not posterior intervals or a dust-detection significance. The same joint region supports the tested indices together, conditional on whichever opacity model is true. The package also gives covariance sensitivity at correlations -0.9, -0.5, 0, 0.5 and 0.9.

## Mass, hidden material and supply

For a spatially uniform infrared opacity per mass kappa, write local optical depth as kappa times surface mass density. If the common normalized surface intensity has maximum J relative to its disk mean, then

    M_front >= pi R_star^2 m/kappa/J.

For a uniform disk J=1. For any finite known J this follows by comparing the brightness-weighted and area-weighted integrals, even if material covers the brightest part. An unknown and arbitrarily high J removes this mass guarantee. Wavelength-dependent surface structure can also break the earlier common-weight model itself.

For beta=1 the central mass floor is

    2.46e17 g (R_star/0.5 R_sun)^2 (kappa/1000 cm^2 g^-1)^-1 / J.

The unknown-covariance lower confidence bound replaces 2.46e17 by 1.89e17 g. These values refer only to material projected on the stellar disk at this dip. They exclude no dust composition without an independent opacity. Off-disk material can add mass. A gas-to-dust ratio would multiply a dust mass but is not measured here.

The upper mass is unbounded in the screen model. The code gives positive measures at t_star/2 and 2 t_star plus a small fixed light fraction 0.0001 at a tail column T. It adjusts the first two fractions to preserve both central depths exactly. For T from 10 to 1e6, all fractions are positive and sum to about 0.04337. The numerical depth error is below 1e-15. As T tends to infinity the adjusted fractions approach positive constants, while m grows as 0.0001 T. Each finite member has finite mass. These examples do not claim dynamical viability of such columns; they show why two depths give a floor but no ceiling.

A replacement rate would need a separate mass residence time. Pattern changes, dip motion and host recurrence do not supply it. For illustration only, complete replacement of the central minimum mass every 30 days would require at least 9.49e10 g/s at the scale values above. We make no empirical claim of that replacement rate.

## Validation and limits

A separate linear program uses 2,002 candidate columns, including the exact attaining column, and enforces both depths and total covered light at most one. It agrees with the analytic minimum within 1e-8 for each index. Including the attaining column checks primal feasibility and dual consistency; it is not an independent continuum proof. A dense dual check agrees with the analytic sign argument. Tail constructions preserve both depths. A fresh repeat produces identical results and figure bytes on this environment.

The dominant limits are physical. TESS is broad but this test uses a nominal wavelength. Real filter integration, a non-power-law opacity, stellar spots with different colors, wavelength-dependent limb darkening, companions, scattering and a different photometric reference can alter the result. SCI 43138ccf gives a concrete example of the surface-color problem for another CPV. Published depth errors may omit baseline systematics. Gaussian marginal errors and the source depth extraction are assumed, not tested with raw photometry. There is one selected dip. We do not generalize the numerical mass scale to all CPVs.

## Reproduction and rights

The external input is reused in place at `./datasets/cpv-bouma-2609.00136v1-html/article.html`, resolved to the shared HP SSD dataset object. Its exact path, version and SHA-256 are in files/results.json and files/NOTICE.txt. No existing shared data were changed. No external article, spectrum, record table or derivative database is bundled. The package contains original code, narrative, a figure and aggregate fit/certificate results. The external paper is credited separately and retains its own terms.

From the extracted publication, use a separate output folder:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --source /path/to/datasets/cpv-bouma-2609.00136v1-html/article.html --out /tmp/cpv-column-repeat

If the shared input is unavailable, first run `python files/retrieve.py /tmp/cpv-column-source`. It retrieves the exact version and checks the source hash. An HTML service change can prevent a byte match even if the table is unchanged; the code stops in that case. Do not write into the signed publication. Python 3.12, numpy, scipy, matplotlib and beautifulsoup4 are needed. The calculation takes seconds in one process. Exact installed versions are in files/results.json and files/environment.txt. Compare results.json and column_bound.png, allowing only the input absolute path to differ if the input is moved.
